---
title: 3.5 zpráva k vydání verze RC
description: Zpráva k vydání verze pro NuGet 3.5 RC, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 52c443ecd79c9108203f5a3c327078ce9e28b95b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548535"
---
# <a name="nuget-35-rc-release-notes"></a>Zpráva k vydání verze NuGet 3.5 RC

[Zpráva k vydání verze NuGet 3.5 Beta2](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5 – zpráva k vydání verze RTM](../release-notes/nuget-3.5-RTM.md)

3.5 verze se zaměřuje na vylepšení kvality a výkonu klientů NuGet. Kromě toho jsme poslali několik funkcí, jako je podpora [záložní složky](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) podporují v `.nuspec` a provádění dalších akcí.

[Seznam problémů](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a>Opravy chyb

* Instalace a obnovení balíčku selže s "balíček obsahuje více `.nuspec` soubory." - [#3231](https://github.com/NuGet/Home/issues/3231)

* balíček nuget vynuceně přidá `.tt` soubory do složky obsahu bez ohledu na to, co - [#3203](https://github.com/NuGet/Home/issues/3203)

* balíček nuget souboru csproj (s `project.json`) dojde k chybě, pokud neexistují žádné packOptions a vlastník v souboru JSON - [#3180](https://github.com/NuGet/Home/issues/3180)

* balíček nuget pro `project.json` packOptions značky jako souhrn, autory, vlastníci atd – ignoruje [#3161](https://github.com/NuGet/Home/issues/3161)

* balíček nuget ignoruje závislosti ve výstupu `.nuspec` pro `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* Aktualizaci více balíčků s vrácení zpět opustí projektu je porušený - [#3139](https://github.com/NuGet/Home/issues/3139)

* ContentFiles za nejsou přidány pro projekty netstandard – [#3118](https://github.com/NuGet/Home/issues/3118)

* Nelze vytvořit balíček knihovny cílené na .net Standard správně – [#3108](https://github.com/NuGet/Home/issues/3108)

* Soubor -> Nový Projekt -> selže projekt knihovny tříd (přenosná) ve VS2015 a odkaz na Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)

* Chyba nuGet – 1.0.0-* není platný řetězec verze - [#3070](https://github.com/NuGet/Home/issues/3070)

* Vyhledání balíčku selže zobrazení, ale funguje Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)

* Chyba při "Install-Package jquery.validation" na odkaz na dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)

* Při nainstalované VS 2015 s aktualizací 3 na VS, které používá NuGet dojde k chybě verze 3.5.0 - [#3053](https://github.com/NuGet/Home/issues/3053)

* Uživatelské rozhraní Správce balíčků: Nová verze nezobrazuje po aktualizaci balíčku- [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey na příkazovém řádku delete není pro čtení/poslaná 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)

* Řetězce není správný: stabilní verze balíčku by neměla mít na předběžnou verzi závislosti. - [#3030](https://github.com/NuGet/Home/issues/3030)

* Vytváří se získat projekt PCL (net46 a windows 10) NullRef výjimky. - [#3014](https://github.com/NuGet/Home/issues/3014)

* Nuget aktualizace by měla poskytnout informativní zprávy, když hodnota allowedVersions omezení – je omezený na vyšší verzi rozhraní [#3013](https://github.com/NuGet/Home/issues/3013)

* Plugin přihlašovacích údajů se ukončil s chybou -1 / Chyba při stahování balíčku při použití poskytovatelé přihlašovacích údajů s více zdroji - [#2885](https://github.com/NuGet/Home/issues/2885)

* balíček nuget - Newtonsoft.Json chybějící závislost balíčku - [#2876](https://github.com/NuGet/Home/issues/2876)

* Chyby v ExecuteSynchronizedCore na Linux nebo MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)

* VS nepodporuje proměnné prostředí v repositoryPath (nuget.exe nepodporuje) - [#2763](https://github.com/NuGet/Home/issues/2763)

* Oprava problémů s přístupností – [#2745](https://github.com/NuGet/Home/issues/2745)

* Přenosná rozhraní s pomlčkou profily odmítají. - [#2734](https://github.com/NuGet/Home/issues/2734)

* Správce balíčků NuGet by mělo být zřejmé tento seznam možností v balíčcích podrobností se nedá použít u `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* Aktualizace NuGet 3.3.0 selže s '... Další omezení definované v souboru packages.config téhle operaci brání. " - [#1816](https://github.com/NuGet/Home/issues/1816)

* Instalace balíčku z místního zdroje, který neexistuje, vyvolá výjimku neplatného zpráva – [#1674](https://github.com/NuGet/Home/issues/1674)

* Filtr "Upgrade dostupné" zobrazuje upgrady, které narušují omezení verze - [#1094](https://github.com/NuGet/Home/issues/1094)

## <a name="performance-improvements"></a>Zvýšení výkonu

* Výkonu: Zlepšení vlastnost ContentModel cílové rozhraní framework analýza kódu - [#3162](https://github.com/NuGet/Home/issues/3162)

* Výkon: Vyhněte se čtení `runtime.json` soubory pro obnovení, které nemají identifikátorů RID [#3150](https://github.com/NuGet/Home/issues/3150). Na počítačích CI obnovení ukázku, kterou webová aplikace ASP.NET se zkrátilo z více než 15 sekund na 3 sekundy.

* Výkonu: Doba načtení konzoly Správce balíčků init.ps1 [#2956](https://github.com/NuGet/Home/issues/2956). Vylepšená doba otevření PackageManagerConsole v některých případech z 132s 10s.

* Řešte problémy s výkonem ReSharper v NuGet pro sadu Vs11 – [#3044](https://github.com/NuGet/Home/issues/3044): na ukázkového projektu a čas potřebný k instalaci balíčků redukovaným z 140s k 68s.

## <a name="dcrs"></a>Chcete

* NuGet je potřeba uživatelům sdělit, že upgrade nebo instalace v dotnet tfm na základě PCL může způsobit problémy se - [#3138](https://github.com/NuGet/Home/issues/3138)

* Upozornit chybný instalace/aktualizace pro projekt plánovaným bodem obnovení kratším tfm = "dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)

* Přidání podpory netcoreapp11 a netstandard17 - [#2998](https://github.com/NuGet/Home/issues/2998)

* Vytisknout obsah záhlaví NuGet upozornění do konzoly v nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)

* Využijte assemblymetadata – atribut pro `.nuspec` token nahrazení - [#2851](https://github.com/NuGet/Home/issues/2851)

* Odeberte vlastnost uzamčená ze souboru zámku – [#2379](https://github.com/NuGet/Home/issues/2379)

* Balíčky symbolů by neměl být nikdy nepoužil v instalaci nebo aktualizaci #2807

## <a name="features"></a>Funkce

* Podpora pro použití náhradní lokality balíček složky – [#2899](https://github.com/NuGet/Home/issues/2899)

* Návrh a implementace hodnoty typu balíčku pro podporu nástroje balíčky - [#2476](https://github.com/NuGet/Home/issues/2476)

* Rozhraní API k získání cesty ke složce globálních balíčků - [#2403](https://github.com/NuGet/Home/issues/2403)

* Nativní balíčky podpora - update [#1291](https://github.com/NuGet/Home/issues/1291)
