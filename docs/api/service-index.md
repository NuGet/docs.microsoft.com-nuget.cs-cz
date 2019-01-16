---
title: Služba Index, rozhraní API Nugetu
description: Index služby je vstupní bod rozhraní API HTTP NuGet a vytváří výčet možností serveru.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1dcfb87690b728280b494d4434f9c1d7ee7a7e74
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324718"
---
# <a name="service-index"></a>Index služby

Index služby je dokument JSON, který je vstupním bodem pro zdroj balíčku NuGet a umožňuje implementace klienta ke zjištění schopnosti zdroje balíčku. Index služby je objekt JSON s dvěma požadované vlastnosti: `version` (verze schématu indexu služby) a `resources` (koncové body nebo možnosti zdroje balíčku).

index služby nuget.org se nachází na `https://api.nuget.org/v3/index.json`.

## <a name="versioning"></a>Správa verzí

`version` Hodnota je řetězec SemVer 2.0.0 parseable verze, který označuje verzi schématu indexu služby. Rozhraní API Určuje, zda má řetězec verze číslo hlavní verze `3`. Jak nevýznamných změn schématu indexu služby, zvýší se verze řetězec podverze.

Každý prostředek v indexu služby je označené verzí odděleně od verze schématu indexu služby.

Aktuální verze schématu `3.0.0`. `3.0.0` Je funkčně srovnatelný s starší verze `3.0.0-beta.1` verze, ale se bude upřednostňovat jako jasněji komunikuje stabilní, definice schématu.

## <a name="http-methods"></a>Metody HTTP

Index služby je přístupný pomocí metody HTTP `GET` a `HEAD`.

## <a name="resources"></a>Prostředky

`resources` Vlastnost obsahuje celou řadu prostředků nepodporuje zdroje tohoto balíčku.

### <a name="resource"></a>Prostředek

Prostředek je objekt `resources` pole. Představuje systémovou správou verzí možnost zdroje balíčku. Prostředek má následující vlastnosti:

Název          | Typ   | Požadováno | Poznámky
------------- | ------ | -------- | -----
@id           | odkazy řetězců | ano      | Adresa URL k prostředku
@type         | odkazy řetězců | ano      | Konstanta řetězec představující typ prostředku
comment       | odkazy řetězců | Ne       | Lidské čitelný popis prostředku

`@id` Je adresa URL, která musí být absolutní a musí mít schéma HTTP nebo HTTPS.

`@type` Slouží k identifikaci konkrétní protokol bude použit při interakci s prostředkem. Typ prostředku je neprůhledný řetězec, ale obvykle má formát:

    {RESOURCE_NAME}/{RESOURCE_VERSION}

Klienti se očekává pevný kód `@type` hodnoty mají přehled a je vyhledat v indexu služby zdroje balíčku. Přesné `@type` hodnoty v současnosti jsou uvedené na referenční dokumenty jednotlivé prostředky uvedené v [přehled rozhraní API](overview.md#resources-and-schema).

Pro účely této dokumentaci, se v dokumentaci k různým prostředkům v podstatě seskupené podle `{RESOURCE_NAME}` v indexu služby, která je analogií seskupení podle scénáře. 

Neexistuje žádný požadavek, že každý prostředek má jedinečnou `@id` nebo `@type`. Je implementace klienta, chcete-li určit, který prostředek se má přednost před jiným. Jednu možnou implementaci je, že prostředky se stejným nebo kompatibilní `@type` lze použít v vždy střídat dokola v případě selhání nebo serveru chyb připojení.

### <a name="sample-request"></a>Ukázková žádost

    GET https://api.nuget.org/v3/index.json

### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [service-index.json](./_data/service-index.json)]
