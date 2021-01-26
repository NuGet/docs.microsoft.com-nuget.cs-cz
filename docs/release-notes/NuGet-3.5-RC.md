---
title: Poznámky k verzi 3,5 RC
description: Poznámky k verzi pro NuGet 3,5 RC, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 04ec402df5ff993b405bb710abf26e1cdc850703
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780196"
---
# <a name="nuget-35-rc-release-notes"></a>Poznámky k verzi NuGet 3,5 RC

[Beta2 NuGet 3,5 – poznámky](../release-notes/nuget-3.5-Beta2.md)  |  k verzi [Poznámky k verzi pro NuGet 3,5 – RTM](../release-notes/nuget-3.5-RTM.md)

verze 3,5 se zaměřuje na zlepšení kvality a výkonu klientů NuGet. Kromě toho jsme dodali několik funkcí, jako je podpora [záložních složek](https://github.com/NuGet/Home/issues/2899), podpora [PackageType](https://github.com/NuGet/Home/issues/2476) v `.nuspec` a dalších.

[Seznam problémů](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a>Opravy chyb

* Instalace nebo obnovení balíčku se nepovede a balíček obsahuje více `.nuspec` souborů. - [#3231](https://github.com/NuGet/Home/issues/3231)

* sada NuGet Pack nuceně přidává `.tt` soubory do složky obsahu bez ohledu na to, co [#3203](https://github.com/NuGet/Home/issues/3203)

* Chyba sady NuGet Pack csproj (with `project.json` ), pokud v souboru JSON nejsou žádné packOptions a Owner – [#3180](https://github.com/NuGet/Home/issues/3180)

* sada NuGet Pack pro `project.json` ignoruje značky packOptions, jako jsou souhrn, autoři, vlastníci atd. [#3161](https://github.com/NuGet/Home/issues/3161)

* sada NuGet Pack ignoruje závislosti ve výstupu `.nuspec` pro `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* Aktualizace více balíčků s vrácením změn ponechá projekt v nefunkčním stavu – [#3139](https://github.com/NuGet/Home/issues/3139)

* ContentFiles v případě, že nejsou přidány pro projekty netstandard – [#3118](https://github.com/NuGet/Home/issues/3118)

* Nelze zabalit správně cílení knihovny na .NET standard- [#3108](https://github.com/NuGet/Home/issues/3108)

* Soubor – > nový projekt – > knihovna tříd (přenosná) projekt se nezdařil v VS2015 a Dev15- [#3094](https://github.com/NuGet/Home/issues/3094)

* Chyba NuGet – 1.0.0-* není platný řetězec verze – [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-Package se nepovede zobrazit, ale funguje Install-Package [#3068](https://github.com/NuGet/Home/issues/3068)

* Chyba při instalaci balíčku jQuery. ověření na dev15- [#3061](https://github.com/NuGet/Home/issues/3061)

* Při instalaci VS 2015 Update 3 na VS, kde se používá chyba NuGet verze 3.5.0 – [#3053](https://github.com/NuGet/Home/issues/3053)

* Uživatelské rozhraní Správce balíčků: po aktualizaci balíčku nezobrazuje novou verzi [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey při odstraňování příkazového řádku není přečten/odeslán v 3.5.0-beta- [#3037](https://github.com/NuGet/Home/issues/3037)

* Nesprávný řetězec: stabilní verze balíčku by neměla mít v závislosti na předběžné verzi. - [#3030](https://github.com/NuGet/Home/issues/3030)

* Vytváření projektu PCL (net46 a Windows 10) pro získání výjimky NullRef. - [#3014](https://github.com/NuGet/Home/issues/3014)

* Aktualizace NuGet by měla poskytnout informativní zprávu, pokud je vyšší verze omezená omezením hodnota allowedversions- [#3013](https://github.com/NuGet/Home/issues/3013)

* Modul plug-in přihlašovacích údajů se ukončil s chybou-1/při stahování balíčku při použití zprostředkovatelů přihlašovacích údajů s více zdroji – [#2885](https://github.com/NuGet/Home/issues/2885)

* NuGet Pack – chybějící Newtonsoft.Jsu závislosti balíčku – [#2876](https://github.com/NuGet/Home/issues/2876)

* Chyba v ExecuteSynchronizedCore v systému Linux/MacOS + mono- [#2860](https://github.com/NuGet/Home/issues/2860)

* VS nepodporuje proměnné prostředí v repositoryPath (nuget.exe) – [#2763](https://github.com/NuGet/Home/issues/2763)

* Oprava problémů s přístupností – [#2745](https://github.com/NuGet/Home/issues/2745)

* Přenosná rozhraní s rozdělenými profily se odmítnou. - [#2734](https://github.com/NuGet/Home/issues/2734)

* Správce balíčků NuGet by měl zrušit zaškrtnutí tohoto seznamu možností v podrobnostech balíčků se nevztahuje na `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* Aktualizace NuGet 3.3.0 se nezdařila s dodatečným omezením... definované v packages.config zabrání této operaci. ' - [#1816](https://github.com/NuGet/Home/issues/1816)

* Instalace balíčku z místního zdroje, který neexistuje, vyvolá nefalešnou zprávu- [#1674](https://github.com/NuGet/Home/issues/1674)

* Filtr "k disstupnému upgradu" zobrazuje upgrady, které porušují omezení verze – [#1094](https://github.com/NuGet/Home/issues/1094)

## <a name="performance-improvements"></a>Zvýšení výkonu

* Výkon: zlepšení analýzy cílového rozhraní ContentModel – [#3162](https://github.com/NuGet/Home/issues/3162)

* Výkon: Vyhněte se čtení `runtime.json` souborů pro obnovení, které nemají identifikátorů rid [#3150](https://github.com/NuGet/Home/issues/3150). V počítačích CI se obnoví Ukázková webová aplikace v ASP.NET z více než 15 sekund na 3 sekundy.

* Výkon: konzola správce balíčků init.ps1 čas načítání [#2956](https://github.com/NuGet/Home/issues/2956). Čas na otevření PackageManagerConsole v některých případech od 132s po desítkách.

* Řešení problémů s výkonem v důsledku aktualizace NuGet- [#3044](https://github.com/NuGet/Home/issues/3044): na ukázkovém projektu se zkrátí doba potřebná k instalaci balíčků z 140s na 68s.

## <a name="dcrs"></a>Chcete odeslat obecnou

* NuGet potřebuje, aby uživatelé věděli, že při upgradu nebo instalaci v dotnet TFM může dojít k problémům – [#3138](https://github.com/NuGet/Home/issues/3138)

* Upozorňovat na neplatnou instalaci/upgrade pro Project w/TFM = "dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)

* Přidání podpory netcoreapp11 a netstandard17 – [#2998](https://github.com/NuGet/Home/issues/2998)

* Vytisknout obsah záhlaví NuGet-Warning do konzoly v nuget.exe- [#2934](https://github.com/NuGet/Home/issues/2934)

* Využití atributu AssemblyMetadata – pro `.nuspec` nahrazení tokenů – [#2851](https://github.com/NuGet/Home/issues/2851)

* Odeberte uzamčenou vlastnost ze souboru zámku – [#2379](https://github.com/NuGet/Home/issues/2379)

* Balíčky symbolů by se neměly nikdy používat při instalaci nebo aktualizaci #2807

## <a name="features"></a>Funkce

* Podpora pro složky záložních balíčků – [#2899](https://github.com/NuGet/Home/issues/2899)

* Navrhněte a implementujte fiktivní typ balíčku, který podporuje balíčky nástrojů – [#2476](https://github.com/NuGet/Home/issues/2476)

* Rozhraní API pro získání cesty ke složce globálních balíčků – [#2403](https://github.com/NuGet/Home/issues/2403)

* Podpora aktualizací nativních balíčků – [#1291](https://github.com/NuGet/Home/issues/1291)
