---
title: Index služby, rozhraní API NuGet
description: Index služby je vstupním bodem rozhraní NuGet HTTP API a vytvoří výčet schopností serveru.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: c2d4d23313c80c24b537b1df227a9cea6784ef6e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775352"
---
# <a name="service-index"></a>Index služby

Index služby je dokument JSON, který je vstupním bodem pro zdroj balíčku NuGet a umožňuje implementaci klienta zjistit možnosti zdroje balíčku. Index služby je objekt JSON se dvěma požadovanými vlastnostmi: `version` (verze schématu indexu služby) a `resources`  (koncové body nebo funkce zdroje balíčku).

index služby NuGet. org je umístěný na adrese `https://api.nuget.org/v3/index.json` .

## <a name="versioning"></a>Správa verzí

`version`Hodnota je řetězec SemVer 2.0.0 s analýzou verze, který označuje verzi schématu indexu služby. Rozhraní API vyžaduje, aby řetězec verze měl hlavní číslo verze `3` . V rámci schématu indexu služby budou provedeny nepodstatné změny, ale zvýší se vedlejší verze řetězce verze.

Každý prostředek v indexu služby je nezávisle na verzi schématu indexu služby.

Aktuální verze schématu je `3.0.0` . `3.0.0`Verze je funkčně ekvivalentní starší `3.0.0-beta.1` verzi, ale měla by být preferována, protože lépe komunikuje stabilní, definované schéma.

## <a name="http-methods"></a>Metody HTTP

Index služby je přístupný pomocí metod HTTP `GET` a `HEAD` .

## <a name="resources"></a>Zdroje

`resources`Vlastnost obsahuje pole prostředků podporované tímto zdrojem balíčku.

### <a name="resource"></a>Prostředek

Prostředek je objekt v poli `resources` . Představuje možnost verze zdroje balíčku. Prostředek má následující vlastnosti:

Název          | Typ   | Vyžadováno | Poznámky
------------- | ------ | -------- | -----
@id           | řetězec | ano      | Adresa URL prostředku
@type         | řetězec | ano      | Řetězcová konstanta představující typ prostředku
comment       | řetězec | ne       | Lidský čitelný popis prostředku

`@id`Je adresa URL, která musí být absolutní a musí mít buď schéma HTTP, nebo HTTPS.

`@type`Slouží k identifikaci konkrétního protokolu, který se má použít při interakci s prostředkem. Typ prostředku je neprůhledný řetězec, ale obecně má formát:

```
{RESOURCE_NAME}/{RESOURCE_VERSION}
```

U klientů se očekává, že budou zakódovat `@type` hodnoty, které znají, a vyhledají je v indexu služby zdroje balíčku. Přesné `@type` hodnoty používané v současnosti jsou vyhodnoceny na základě dokumentů odkazů na jednotlivé prostředky, které jsou uvedeny v [přehledu rozhraní API](overview.md#resources-and-schema).

V této dokumentaci se dokumentace k různým prostředkům v podstatě seskupí podle toho, jak se `{RESOURCE_NAME}` nachází v indexu služby, což je analogické seskupení podle scénáře. 

Neexistuje žádný požadavek, aby každý prostředek měl jedinečný `@id` nebo `@type` . Je k tomu implementace klienta, aby bylo možné určit, který prostředek se má preferovat jiným. Jednou z možných implementací je, že prostředky stejného nebo kompatibilního typu se `@type` dají použít v kruhovém dotazování v případě selhání připojení nebo chyby serveru.

### <a name="sample-request"></a>Ukázková žádost

```
GET https://api.nuget.org/v3/index.json
```

### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [service-index.json](./_data/service-index.json)]
