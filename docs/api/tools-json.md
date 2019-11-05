---
title: Tools. JSON pro zjišťování verzí NuGet. exe
description: Koncový bod pro
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: a186db9727bdfd1b55bf73a1f29283352555dede
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/05/2019
ms.locfileid: "73611020"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a>Tools. JSON pro zjišťování verzí NuGet. exe

V současné době existuje několik způsobů, jak na svém počítači získat nejnovější verzi nástroje NuGet. exe, která umožňuje skriptovat. Balíček [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) můžete například stáhnout a extrahovat z NuGet.org. To má složitost, protože buď vyžaduje, abyste už měli nástroj NuGet. exe (pro `nuget.exe install`), nebo musíte rozbalit soubor. nupkg pomocí základního nástroje pro rozbalení a vyhledat binární soubor uvnitř.

Pokud již máte NuGet. exe, můžete také použít `nuget.exe update -self`, ale to vyžaduje, abyste měli existující kopii NuGet. exe. Tento přístup také aktualizuje na nejnovější verzi. Neumožňuje použití konkrétní verze.

Koncový bod `tools.json` je k dispozici pro řešení potíží s zaváděním a pro řízení verze souboru NuGet. exe, který stáhnete. Tato možnost se dá použít v prostředích CI/CD nebo ve vlastních skriptech ke zjišťování a stažení všech vydaných verzí NuGet. exe.

Koncový bod `tools.json` lze načíst pomocí neověřeného požadavku HTTP (např. `Invoke-WebRequest` v PowerShellu nebo `wget`). Dá se analyzovat pomocí deserializace JSON a následné adresy URL pro stahování NuGet. exe můžete také načíst pomocí neověřených požadavků HTTP.

Koncový bod se dá načíst pomocí metody `GET`:

    GET https://dist.nuget.org/tools.json

[Schéma JSON](https://json-schema.org/) pro koncový bod je k dispozici zde:

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a>Základě

Odpověď je dokument JSON obsahující všechny dostupné verze nástroje NuGet. exe.

Kořenový objekt JSON má následující vlastnost:

Name      | Typ             | Požadováno
--------- | ---------------- | --------
nuget.exe | pole objektů | Ano

Každý objekt v poli `nuget.exe` má následující vlastnosti:

Name     | Typ   | Požadováno | Poznámky
-------- | ------ | -------- | -----
verze  | odkazy řetězců | Ano      | Řetězec SemVer 2.0.0
Adresa URL      | odkazy řetězců | Ano      | Absolutní adresa URL pro stažení této verze souboru NuGet. exe
Skladiště    | odkazy řetězců | Ano      | Řetězec výčtu
nahrávaný | odkazy řetězců | Ano      | Přibližné časové razítko ISO 8601, kdy byla verze zpřístupněna

Položky v poli budou seřazeny sestupně, SemVer 2.0.0 objednávka. Tato záruka má snížit zatížení klienta, který má zájem o nejvyšší číslo verze. To ale znamená, že seznam není seřazený v chronologickém pořadí. Pokud je například nižší hlavní verze zavedená v pozdější době než vyšší hlavní verze, tato služba se v horní části seznamu nezobrazí. Pokud chcete nejnovější verzi vydanou *časovým razítkem*, jednoduše seřaďte pole pomocí `uploaded`ho řetězce. To funguje, protože časové razítko `uploaded` je ve formátu [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) , který lze seřadit chronologicky pomocí lexicographical řazení (tj. jednoduché řazení řetězců).

Vlastnost `stage` určuje, jak prověřené Tato verze nástroje. 

Skladiště              | Význam
------------------ | ------
EarlyAccessPreview | Ještě není vidět na [webové stránce Stáhnout](https://www.nuget.org/downloads) a měly by je ověřit partneři.
Vydáno           | K dispozici na webu pro stahování, ale ještě není doporučováno pro rozsáhlou spotřebu
ReleasedAndBlessed | K dispozici na webu pro stahování a doporučuje se pro spotřebu

Jedním jednoduchým přístupem k nejnovějším a doporučeným verzím je první verze v seznamu, která má `stage` hodnotu `ReleasedAndBlessed`. To funguje, protože verze jsou seřazené v SemVer 2.0.0 pořadí.

Balíček `NuGet.CommandLine` v nuget.org se obvykle aktualizuje jenom pomocí `ReleasedAndBlessed` verzí.

### <a name="sample-request"></a>Ukázková žádost

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [tools-json.json](./_data/tools-json.json)]
