---
title: Tools.JSON pro zjišťování nuget.exe verze
description: Koncový bod pro
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: 003139abac7808dbdaef4aa66119e09772db2b4f
ms.sourcegitcommit: b6efd4b210d92bf163c67e412ca9a5a018d117f0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/26/2019
ms.locfileid: "56852530"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a>Tools.JSON pro zjišťování nuget.exe verze

V současné době existuje několik způsobů, jak získat nejnovější verzi programu nuget.exe na svém počítači skriptovatelný způsobem. Například můžete stáhnout a extrahovat [ `NuGet.CommandLine` ](https://www.nuget.org/packages/NuGet.CommandLine/) balíček z webu nuget.org. To má některé složitost, protože se buď vyžaduje, že už máte nuget.exe (pro `nuget.exe install`) nebo máte rozbalit .nupkg nástrojem základní unzip a vyhledejte binární vnitřní.

Pokud už máte nuget.exe, můžete také použít `nuget.exe update -self`, ale tento proces také vyžaduje s existující kopie nuget.exe. Tento přístup můžete rovněž aktualizuje na nejnovější verzi. Neumožňuje použít konkrétní verzi.

`tools.json` Koncový bod je k dispozici pro obě samozaváděcí problém vyřešit a poskytnout kontrolu verze programu nuget.exe, který můžete stáhnout. To lze vyhledat a stáhnout všechny vydané verze programu nuget.exe použít v prostředích CI/CD nebo vlastní skripty.

`tools.json` Koncového bodu můžete načíst pomocí neověřené žádosti protokolu HTTP (například `Invoke-WebRequest` v prostředí PowerShell nebo `wget`). Může být analyzován pomocí deserializátor JSON a následné nuget.exe pro stažení adresy URL můžete načíst taky pomocí neověřené požadavky HTTP.

Koncový bod můžete načíst pomocí `GET` metody:

    GET https://dist.nuget.org/tools.json

[Schématu JSON](http://json-schema.org/) pro koncový bod je k dispozici zde:

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a>Odpověď

Odpověď je dokument JSON obsahující všechny dostupné verze programu nuget.exe.

Kořenový objekt JSON má následující vlastnost:

Název      | Typ             | Požadováno
--------- | ---------------- | --------
nuget.exe | Pole objektů | ano

Každý objekt v `nuget.exe` pole má následující vlastnosti:

Název     | Typ   | Požadováno | Poznámky
-------- | ------ | -------- | -----
verze  | odkazy řetězců | ano      | Řetězec SemVer 2.0.0
url      | odkazy řetězců | ano      | Absolutní adresa URL pro stahování tato verze programu nuget.exe
fáze    | odkazy řetězců | ano      | Řetězec výčtu
Nahrání | odkazy řetězců | ano      | Přibližné časové razítko ISO 8601 z verze kdy byl k dispozici

Položky v poli budou seřazeny v sestupném pořadí SemVer 2.0.0. Aby se snížila zátěž klienta, který je uvažujete o nejvyšší číslo verze je určená této záruky. Ale to znamená, že seznam není seřazen v chronologickém pořadí. Například pokud nižší hlavní verze se obsluhují na datum pozdější než vyšší hlavní verze, tuto upravenou verzí se nezobrazí v horní části seznamu. Pokud chcete na nejnovější verzi vydal *časové razítko*, jednoduše seřadit pole pomocí `uploaded` řetězec. Tento postup funguje, protože `uploaded` časové razítko není v [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) formát, který lze seřadit chronologicky pomocí lexicographical řazení (to znamená jednoduchým řetězcem řazení).

`stage` Vlastnost určuje, jak prověřené je tato verze nástroje. 

Fáze              | Význam
------------------ | ------
EarlyAccessPreview | Nejsou ještě viditelné na [webové stránce pro stažení](https://www.nuget.org/downloads) a by měl být ověřen od partnerů
Všeobecně dostupné           | K dispozici na webu Stažení ale ještě není doporučeno pro šíření celou spotřebu
ReleasedAndBlessed | K dispozici na serveru pro stahování a je doporučena pro využití

Jeden jednoduchým přístupem k nutnosti na nejnovější verzi, doporučená verze je v seznamu, který se má provést první verze `stage` hodnotu `ReleasedAndBlessed`. Tento postup funguje, protože verze jsou seřazeny podle SemVer 2.0.0.

`NuGet.CommandLine` Balíčků na nuget.org je obvykle pouze aktualizován `ReleasedAndBlessed` verze.

### <a name="sample-request"></a>Ukázková žádost

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [tools-json.json](./_data/tools-json.json)]
