---
title: tools.jspro zjišťování verzí nuget.exe
description: Koncový bod pro
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: eb28ccbc4460663b0f149d2d08e9b47dd69847c7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773819"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a>tools.jspro zjišťování verzí nuget.exe

V současné době existuje několik způsobů, jak na svém počítači získat nejnovější verzi nuget.exe pomocí skriptu. Balíček můžete například stáhnout a extrahovat [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) z NuGet.org. To má složitost, protože buď vyžaduje, abyste již měli nuget.exe (pro `nuget.exe install` ), nebo musíte rozbalit soubor. nupkg pomocí základního nástroje pro rozbalení a vyhledat binární soubor uvnitř.

Pokud již máte nuget.exe, můžete také použít `nuget.exe update -self` existující kopii nuget.exe. Tento přístup také aktualizuje na nejnovější verzi. Neumožňuje použití konkrétní verze.

`tools.json`Koncový bod je k dispozici pro řešení potíží s zaváděním a pro řízení verze nuget.exe, kterou stáhnete. Tato možnost se dá použít v prostředích CI/CD nebo ve vlastních skriptech ke zjišťování a stažení všech vydaných verzí nuget.exe.

`tools.json`Koncový bod se dá načíst pomocí neověřeného požadavku HTTP (třeba `Invoke-WebRequest` v PowerShellu nebo `wget` ). Dá se analyzovat pomocí deserializace JSON a následné nuget.exe adresy URL pro stahování je možné také načíst pomocí neověřených požadavků HTTP.

Koncový bod se dá načíst pomocí `GET` metody:

```
GET https://dist.nuget.org/tools.json
```

[Schéma JSON](https://json-schema.org/) pro koncový bod je k dispozici zde:

```
GET https://dist.nuget.org/tools.schema.json
```

## <a name="response"></a>Odpověď

Odpověď je dokument JSON obsahující všechny dostupné verze nuget.exe.

Kořenový objekt JSON má následující vlastnost:

Název      | Typ             | Vyžadováno
--------- | ---------------- | --------
nuget.exe | pole objektů | ano

Každý objekt v `nuget.exe` poli má následující vlastnosti:

Název     | Typ   | Vyžadováno | Poznámky
-------- | ------ | -------- | -----
verze  | řetězec | ano      | Řetězec SemVer 2.0.0
url      | řetězec | ano      | Absolutní adresa URL pro stažení této verze nuget.exe
skladiště    | řetězec | ano      | Řetězec výčtu
nahrávaný | řetězec | ano      | Přibližné časové razítko ISO 8601, kdy byla verze zpřístupněna

Položky v poli budou seřazeny sestupně, SemVer 2.0.0 objednávka. Tato záruka má snížit zatížení klienta, který má zájem o nejvyšší číslo verze. To ale znamená, že seznam není seřazený v chronologickém pořadí. Pokud je například nižší hlavní verze zavedená v pozdější době než vyšší hlavní verze, tato služba se v horní části seznamu nezobrazí. Pokud chcete nejnovější verzi vydanou pomocí *časového razítka*, jednoduše seřaďte pole podle `uploaded` řetězce. To funguje, protože `uploaded` časové razítko je ve formátu [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) , který lze seřadit chronologicky pomocí lexicographical řazení (tj. jednoduché řazení řetězců).

`stage`Vlastnost určuje, jak prověřené Tato verze nástroje. 

Fáze              | Význam
------------------ | ------
EarlyAccessPreview | Ještě není vidět na [webové stránce Stáhnout](https://www.nuget.org/downloads) a měly by je ověřit partneři.
Vydáno           | K dispozici na webu pro stahování, ale ještě není doporučováno pro rozsáhlou spotřebu
ReleasedAndBlessed | K dispozici na webu pro stahování a doporučuje se pro spotřebu

Jedním jednoduchým přístupem k nejnovějším a doporučeným verzím je první verze v seznamu, který má `stage` hodnotu `ReleasedAndBlessed` . To funguje, protože verze jsou seřazené v SemVer 2.0.0 pořadí.

`NuGet.CommandLine`Balíček v NuGet.org je obvykle aktualizován pouze s `ReleasedAndBlessed` verzemi.

### <a name="sample-request"></a>Ukázková žádost

```
GET https://dist.nuget.org/tools.json
```

### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [tools-json.json](./_data/tools-json.json)]
