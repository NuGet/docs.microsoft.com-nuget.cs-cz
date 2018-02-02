---
title: "3.5 poznámky k verzi RC | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Poznámky k verzi pro NuGet 3.5 RC včetně známé problémy, opravy chyb, přidaných funkcí a chcete."
keywords: "NuGet 3.5 k vydání verze RC, opravy chyb známé problémy, přidat funkce, chcete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: fdb84da5f1648ce4508afe6ddcf04bddd41284d3
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-35-rc-release-notes"></a>Poznámky k verzi RC NuGet 3.5

[Poznámky k verzi 3.5 Beta2 NuGet](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5 – poznámky k verzi RTM](../release-notes/nuget-3.5-RTM.md)

3.5 verze je zaměřena na zlepšení kvality a výkonu klienty NuGet. Kromě toho jsme poslali několik funkcí, jako je podpora pro [záložní složky](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) podporovat v `.nuspec` a další.

[Seznam problémů](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5 RC")

## <a name="bug-fixes"></a>Opravy chyb

* Instalace a obnovení balíčku selže s "balíček obsahuje více `.nuspec` soubory." - [#3231](https://github.com/NuGet/Home/issues/3231)

* nuget pack vynuceně přidá `.tt` soubory do složky obsahu bez ohledu na to, co - [#3203](https://github.com/NuGet/Home/issues/3203)

* nuget pack csproj (s `project.json`) dojde k chybě, pokud nejsou žádné packOptions a vlastníka v souboru JSON - [#3180](https://github.com/NuGet/Home/issues/3180)

* balíček nuget pro `project.json` ignoruje packOptions značky souhrn, autoři, vlastníky atd - [#3161](https://github.com/NuGet/Home/issues/3161)

* nuget pack ignoruje závislosti ve výstupu `.nuspec` pro `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* Aktualizaci více balíčků s vrácení ponechá projektu v narušeném stavu - [#3139](https://github.com/NuGet/Home/issues/3139)

* ContentFiles ve všech nebyly přidány pro projekty monikerů netstandard - [#3118](https://github.com/NuGet/Home/issues/3118)

* Nelze vytvořit balíček knihovny cílení na rozhraní .net standardní správně – [#3108](https://github.com/NuGet/Home/issues/3108)

* Soubor -> Nový Projekt -> selže projektu knihovny tříd (přenositelností) v VS2015 a Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)

* Chyba nuGet - 1.0.0-* není platný řetězec verze - [#3070](https://github.com/NuGet/Home/issues/3070)

* Najít balíček nepodaří zobrazení, ale funguje Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)

* Chyba při "Install-Package jquery.validation" na dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)

* Pokud je nainstalované VS 2015 s aktualizací 3 na VS, které používá NuGet dojde k chybě verze 3.5.0 - [#3053](https://github.com/NuGet/Home/issues/3053)

* Balíček uživatelského rozhraní správce: po aktualizaci balíčku nezobrazuje nová verze- [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey na odstranění příkazového řádku pro čtení nebo neposílají v 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)

* Nesprávný řetězec: stabilní verze balíčku by neměla mít na závislost na předběžné verzi. - [#3030](https://github.com/NuGet/Home/issues/3030)

* Vytvoření projektu get PCL (net46 a windows 10) NullRef výjimka. - [#3014](https://github.com/NuGet/Home/issues/3014)

* Aktualizace Nuget by měl poskytovat informativní zprávy, když hodnota allowedVersions omezení - je omezený na vyšší verzi [#3013](https://github.com/NuGet/Home/issues/3013)

* Modul plug-in přihlašovacích údajů byl ukončen s chybou -1 / Chyba stahování balíčku při použití poskytovatelé přihlašovacích údajů pro více zdrojů - [#2885](https://github.com/NuGet/Home/issues/2885)

* nuget pack - závislost balíčku chybí Newtonsoft.Json - [#2876](https://github.com/NuGet/Home/issues/2876)

* Chyby v ExecuteSynchronizedCore na systému Linux nebo MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)

* VS nepodporuje proměnné prostředí v repositoryPath (nuget.exe nemá) - [#2763](https://github.com/NuGet/Home/issues/2763)

* Vyřešte problémy s - [#2745](https://github.com/NuGet/Home/issues/2745)

* Přenosné rozhraní s rozděleným profily byly zamítnuty. - [#2734](https://github.com/NuGet/Home/issues/2734)

* Správce balíčků NuGet by mělo být zřejmé tento seznam možností v balíčcích podrobností se nevztahuje na `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* NuGet 3.3.0 aktualizace nezdaří s ' dodatečné omezení... definované v souboru packages.config téhle operaci brání. " - [#1816](https://github.com/NuGet/Home/issues/1816)

* Instalace balíčku z místního zdroje, který neexistuje vyvolává neplatnou zpráva – [#1674](https://github.com/NuGet/Home/issues/1674)

* "Upgrade ostupné" filtr zobrazuje upgrady, které porušují omezení verze - [#1094](https://github.com/NuGet/Home/issues/1094)

## <a name="performance-improvements"></a>Zvýšení výkonu

* Výkonu: Zlepšení ContentModel cílový framework analýza - [#3162](https://github.com/NuGet/Home/issues/3162)

* Výkon: Vyhněte se čtení `runtime.json` soubory pro obnovení, které nemají identifikátorů RID [#3150](https://github.com/NuGet/Home/issues/3150). Na počítačích CI obnovení, které webové aplikace ASP.NET snížit z více než 15 sekund do 3 sekund vzorku.

* Výkonu: Čas načtení init.ps1 Konzola správce balíčků [#2956](https://github.com/NuGet/Home/issues/2956). Čas otevření PackageManagerConsole vylepšení v některých případech z 132s 10s.

* Řešení problémů s výkonem ReSharper v aktualizaci NuGet - [#3044](https://github.com/NuGet/Home/issues/3044): na ukázkový projekt čas potřebný k instalaci balíčků zmenšeny z 140s 68s.

## <a name="dcrs"></a>DCRs

* NuGet je potřeba upozornit uživatele, že upgrade nebo instalace v dotnet tfm, na základě PCL může způsobit problémy - [#3138](https://github.com/NuGet/Home/issues/3138)

* Upozornit chybná instalace nebo aktualizace pro projekt s tfm = "dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)

* Přidání podpory netcoreapp11 a netstandard17 - [#2998](https://github.com/NuGet/Home/issues/2998)

* Tisk obsahu hlavičky NuGet upozornění do konzoly v nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)

* Assemblymetadata – atribut využívají pro `.nuspec` token náhrady - [#2851](https://github.com/NuGet/Home/issues/2851)

* Odebrat vlastnost uzamčeném zámek souboru - [#2379](https://github.com/NuGet/Home/issues/2379)

* Symbol balíčky někdy nesmí být použita v instalaci nebo aktualizaci #2807

## <a name="features"></a>Funkce

* Podporu pro záložní balíček složky - [#2899](https://github.com/NuGet/Home/issues/2899)

* Návrh a implementaci představu o typu balíčku pro podporu nástroje balíčky - [#2476](https://github.com/NuGet/Home/issues/2476)

* Rozhraní API pro získání cesty ke složce globální balíčky - [#2403](https://github.com/NuGet/Home/issues/2403)

* Nativní balíčky aktualizovat podporu - [#1291](https://github.com/NuGet/Home/issues/1291)
