---
title: "Index služby, NuGet rozhraní API | Microsoft Docs"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Index služby je vstupní bod rozhraní API HTTP NuGet a vytvoří výčet možností serveru."
keywords: "Rozhraní API NuGet vstupní bod, NuGetA PI koncový bod zjišťování"
ms.reviewer:
- karann
- unnir
ms.openlocfilehash: 9d0bb421c163520df4a1f0e9f3f71aab823aace3
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/02/2018
---
# <a name="service-index"></a>Index služby

Index služby je dokument JSON, který je vstupní bod pro zdroje balíčku NuGet a umožňuje implementace klienta ke zjištění schopnosti zdroji balíčku. Index služby je objekt JSON s dvěma požadované vlastnosti: `version` (verze schématu indexu služby) a `resources` (koncových bodů nebo možnosti zdrojových souborů balíčku).

index služby nuget.org je umístěn v `https://api.nuget.org/v3/index.json`.

## <a name="versioning"></a>Správa verzí

`version` Hodnota je řetězec parseable verze SemVer 2.0.0, který označuje verzi schématu indexu služby.
Rozhraní API vyžaduje, aby řetězec verze má hlavní verzi počet `3`. Při provedení změn pevné na schéma indexu služby, zvýší se podverze řetězec verze.

Každý prostředek v indexu služby je verzí nezávisle na verzi schématu indexu služby.

Aktuální verze schématu `3.0.0-beta.1`.

## <a name="http-methods"></a>Metody HTTP

Index služba je přístupná pomocí metody HTTP `GET` a `HEAD`.

## <a name="resources"></a>Prostředky

`resources` Vlastnost obsahuje pole prostředků nepodporuje tento zdroj balíčku.

### <a name="resource"></a>Prostředek

Prostředek je objektem ve `resources` pole. Reprezentuje verzí schopností zdroje balíčku. Prostředek má následující vlastnosti:

Název          | Typ   | Požadováno | Poznámky
------------- | ------ | -------- | -----
@id           | odkazy řetězců | Ano      | Adresa URL prostředku
@type         | odkazy řetězců | Ano      | Řetězcová konstanta představující typ prostředku
comment       | odkazy řetězců | Ne       | Lidské čitelný popis prostředku

`@id` Je adresa URL, která musí být absolutní a buď musí mít schéma protokolu HTTP nebo HTTPS.

`@type` Slouží k identifikaci konkrétní protokol bude použit při interakci s prostředků. Typ prostředku je neprůhledný řetězec, ale obvykle má formát:

    {RESOURCE_NAME}/{RESOURCE_VERSION}

Klienti se očekává, pevné kódu `@type` hodnoty, pochopit a jejich vyhledat ve zdroji balíčku služby index. Přesné `@type` hodnoty v současnosti jsou uvedené na dokumenty odkaz jednotlivých prostředků uvedené v [přehled rozhraní API](overview.md#resources-and-schema).

Z důvodu této dokumentace, bude v dokumentaci o různých prostředků v podstatě seskupené podle `{RESOURCE_NAME}` nachází v indexu služby, která je analogií seskupení podle scénáře. 

Není potřeba, aby každý prostředek má jedinečnou `@id` nebo `@type`. Je implementace klienta k určení, který prostředek se má přednost oproti jinému. Jednou z možných implementací je, že prostředky na stejné nebo kompatibilní `@type` mohou být používány kruhového dotazování v případě selhání nebo serveru chyb připojení.

### <a name="sample-request"></a>Ukázková žádost

GET https://api.nuget.org/v3/index.json

### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [service-index.json](./_data/service-index.json)]
