---
title: NuGet 4.0 RC poznámky k verzi
description: Poznámky k verzi pro NuGet 4.0 RC včetně známých problémů, oprav chyb, přidaných funkcí a řadičů domény.
author: karann-msft
ms.author: karann
ms.date: 02/03/2017
ms.topic: conceptual
ms.reviewer: ananguar
ms.openlocfilehash: 2d0bb6356c0a20843bdc884b68f5f61838b82e73
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496647"
---
# <a name="nuget-40-rc-release-notes"></a>NuGet 4.0 RC poznámky k verzi

[NuGet 3,5 RTM poznámky k verzi](../release-notes/nuget-3.5-RTM.md)

[NuGet 4.0 RC pro Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) se zaměřuje na přidání podpory pro scénáře .NET Core, adresování klíčových názorů zákazníků a zlepšení výkonu v různých scénářích. Tato verze přináší několik vylepšení, jako je podpora packagereference, NuGet příkazy jako MSBuild cíle, obnovení balíčku na pozadí a další.

## <a name="bug-fixes"></a>Opravy chyb

- Změny chování `dotnet pack --version-suffix foo`  - v [#3838](https://github.com/NuGet/Home/issues/3838)

- nuget.exe obnovení na vs "15" stroj pouze selže - [#3834](https://github.com/NuGet/Home/issues/3834)

- . NETCore soubor nový projekt by měl blokovat sestavení během obnovení - [#3780](https://github.com/NuGet/Home/issues/3780)

- ASP.NET Základní webová aplikace, migrovaná z VS2015 na VS "15", nelze obnovit. - [#3773](https://github.com/NuGet/Home/issues/3773)

- [Selhání testu] Balíček "jQuery Validation" nelze odinstalovat pomocí pm ui - [#3755](https://github.com/NuGet/Home/issues/3755)

- Při instalaci balíčku do `project.json`UPW , nadřazené projekty by měly být také obnoveny - [#3731](https://github.com/NuGet/Home/issues/3731)

- Upravte Cíle NuGet pro protokolování zdrojů balíčku jako vysoké podrobnosti namísto Normal - [#3719](https://github.com/NuGet/Home/issues/3719)

- dotnet
  - dotnetcore pack3 by měl obsahovat dokumentaci XML ve výchozím nastavení - [#3698](https://github.com/NuGet/Home/issues/3698)

- Dávková aktualizace se nezdaří z uhlavního pásma, pokud je nejprve zdroj bez balíčku a je vybrán veškerý zdroj - [#3696](https://github.com/NuGet/Home/issues/3696)

- Nuget pack příkaz neobsahuje všechny soubory - [#3678](https://github.com/NuGet/Home/issues/3678)

- OOM problém - [#3661](https://github.com/NuGet/Home/issues/3661)

- Část Souboru datových zdrojů projectFileDependencyGroups by měla používat názvy knihoven pro projekty – [#3611](https://github.com/NuGet/Home/issues/3611)

- "dotnet restore" a opakování adresářů - [#3517](https://github.com/NuGet/Home/issues/3517)

- Obnovení3 chyby jsou zaznamenány jako upozornění namísto chyb - [#3503](https://github.com/NuGet/Home/issues/3503)

- Problém tfs: "[soubor] nelze nalézt ve vašem pracovním prostoru, nebo nemáte oprávnění k přístupu k němu" - [#2805](https://github.com/NuGet/Home/issues/2805)

- Zadáním "nuget" <packagename>vs quicklaunch vyhledávacího pole udržuje "nuget" prefix - [#2719](https://github.com/NuGet/Home/issues/2719)

- System.Xml.XmlException: Nerozpoznaný kořenový prvek v části Vlastnosti jádra. Řádek 2, pozice 2. - [#2718](https://github.com/NuGet/Home/issues/2718)

- `.nuspec`s &lt; uvozeným nebo &gt; v textových polích, která se již nevytváří - [#2651](https://github.com/NuGet/Home/issues/2651)

- nuget.exe delete nevyzve k zadání přihlašovacích údajů (je v neinteraktivním režimu) - [#2626](https://github.com/NuGet/Home/issues/2626)

- nuget.exe delete varuje o klíči API pro místní zdroje, i když to nedává smysl - [#2625](https://github.com/NuGet/Home/issues/2625)

- Při instalaci balíčku EF -pre [došlo](https://github.com/NuGet/Home/issues/2566) k chybě, #2566

- Visual Studio došlo k pokusu o změnu výběru ve Správci balíčků - [#2551](https://github.com/NuGet/Home/issues/2551)

- dotnet
  - dotnetcore obnovení provádí vyhledávání ID rozlišování malých a velkých písmen v místních úložištích s plochým seznamem při použití plovoucích verzí - [#2516](https://github.com/NuGet/Home/issues/2516)

- nuget.exe odstranit je přerušeno pro V2 feed - [#2509](https://github.com/NuGet/Home/issues/2509)

- nuget.exe push timeout potřebuje lepší chybovou zprávu - [#2503](https://github.com/NuGet/Home/issues/2503)

- Nástroj obnovení bez řádného importu tiše selže. - [#2462](https://github.com/NuGet/Home/issues/2462)

- NuGet vyzve k zadání přihlašovacích údajů, pokud je soukromý zdroj i při instalaci z nuget.org - [#2346](https://github.com/NuGet/Home/issues/2346)

- Balíček ApplicationInsights 2.0 je uveden, ale ještě neexistuje – [#2317](https://github.com/NuGet/Home/issues/2317)

- UIDelay ve VS "15" náhled 5 větev - [#3500](https://github.com/NuGet/Home/issues/3500)

- První Událost OnBuild chybí pro obnovení během sestavení pro UPW - [#3489](https://github.com/NuGet/Home/issues/3489)

- PowerShell5 přestávky EntityFramework nainstalovat? - [#3312](https://github.com/NuGet/Home/issues/3312)

- Přidání zdroje do podrobného protokolování (zvažte pro 3.5) - [#3294](https://github.com/NuGet/Home/issues/3294)

- Parametr NoCache není dodržen v nugetové klientské verzi 3.4+ - [#3074](https://github.com/NuGet/Home/issues/3074)

- Když se zprostředkovatele pověření nepodaří načíst ve VS, nepřerušuj nuget – [#2422](https://github.com/NuGet/Home/issues/2422)

## <a name="features"></a>Funkce

- Nastavit CI pro spuštění x86 - [#3868](https://github.com/NuGet/Home/issues/3868)

- Automatické obnovení 3/3: neblokující uI - [#3658](https://github.com/NuGet/Home/issues/3658)

- Auto Restore 2/3: obnovení pozadí na nominaci - [#3657](https://github.com/NuGet/Home/issues/3657)

- Obnovit refs projektu tak, aby odpovídaly chování sestavení (recurse) - [#3615](https://github.com/NuGet/Home/issues/3615)

- Podpora DPL ve VS "15" - minbar - [#3614](https://github.com/NuGet/Home/issues/3614)

- Přesunout soubor nastavení do programových souborů - [#3613](https://github.com/NuGet/Home/issues/3613)

- Generované rekvizity a cíle obnovení vyžadují podporu účasti napříč cíleními – [#3496](https://github.com/NuGet/Home/issues/3496)

- Podpora obnovení NuGet pro PackageTargetFallback (f.k.a Imports) - [#3494](https://github.com/NuGet/Home/issues/3494)

- Implementace ToolsRef - [#3472](https://github.com/NuGet/Home/issues/3472)

- Obnovení3 pro rid - [#3465](https://github.com/NuGet/Home/issues/3465)

- NuGet ui pro podporu přidat nebo odebrat/aktualizovat PackageRefs - [#3457](https://github.com/NuGet/Home/issues/3457)

- Automatické obnovení 1/3: Implemenation nominace API přes Caching Projektu Obnovit Info - [#3456](https://github.com/NuGet/Home/issues/3456)

- [0] NuGet Obnovit úlohu & cíle - [#2994](https://github.com/NuGet/Home/issues/2994)

- [1] Povolit obnovení úrovně řešení v MSBuild - [#2993](https://github.com/NuGet/Home/issues/2993)

- Podpora veřejné rozšiřitelnosti poskytovatele pověření v sadě Visual Studio – [#2909](https://github.com/NuGet/Home/issues/2909)

- Obnovení rekurzivního nugetu - [#2533](https://github.com/NuGet/Home/issues/2533)

- Nelze načíst Microsoft.TeamFoundation.Client na dev15, je třeba aktualizovat Microsoft.TeamFoundation.Client verze 15.0 pro VS "15" Preview - [#2392](https://github.com/NuGet/Home/issues/2392)

- Nelze nainstalovat balíček C++ do projektu C++ UWP v náhledu VS "15" - [#2369](https://github.com/NuGet/Home/issues/2369)

- Nupkg musí podporovat \buildCrossTargeting\ složku `.targets`  /  `.props` - a importovat pro "crosstargeting" MSBuild oboru. - [#3499](https://github.com/NuGet/Home/issues/3499)

- ToolsReference Design - [#3462](https://github.com/NuGet/Home/issues/3462)

- Oprava nugetového uznatého pro `.csproj`  - podporu obnovení w/ Reference balíčků v [#3455](https://github.com/NuGet/Home/issues/3455)

- Přidání tlačítka vymazat mezipaměť do nastavení správce balíčků VS - [#3289](https://github.com/NuGet/Home/issues/3289)

## <a name="dcrs"></a>Řadiče domény

- Obnovení řešení by měla být blokována, zatímco automatické obnovení probíhá. - [#3797](https://github.com/NuGet/Home/issues/3797)

- NetCore nainstalovat z NuGet Package Manager ui nainstaluje do každého TFM , namísto ty, které podporuje balíček - [#3721](https://github.com/NuGet/Home/issues/3721)

- Obnovení nominátor api potřebuje pro podporu DotNetCliToolsReferences příliš. - [#3702](https://github.com/NuGet/Home/issues/3702)

- Označte naše VS "15" vsix jako systémkomponenta - [#3700](https://github.com/NuGet/Home/issues/3700)

- Migrovat z odkazování na MS. Vs. Services.Client pro MS. Vs. Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)

- $(RestoreLegacyPackagesDirectory) by měla být respektována na úrovni projektu obnovením - [#3618](https://github.com/NuGet/Home/issues/3618)

- Obnovit do projektu s jedním TargetFramework nesmí podmínku rekvizity - [#3588](https://github.com/NuGet/Home/issues/3588)

- dotnet
  - dotnetcore restore3 foo.csproj by měl následovat projectref závislosti, a obnovit ty taky. Jako stavět. - [#3577](https://github.com/NuGet/Home/issues/3577)

- "type": "platforma" Závislosti reprezentované jako "type":"package" v souboru zámku - [#2695](https://github.com/NuGet/Home/issues/2695)

- nuget.exe Verbose režim by měl ukázat stáhnout url - [#2629](https://github.com/NuGet/Home/issues/2629)

- Přesuňte NuGet xplat na Microsoft.NetCore.App a netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)

- Push - Při tlačení z příkazového řádku by mělo být možné přepsat symbolový server - [#2348](https://github.com/NuGet/Home/issues/2348)

- Konsolidovat kód pro hledání cesty globálních balíčků – [#2296](https://github.com/NuGet/Home/issues/2296)

- Potřebujete lepší název než potlačitParent - [#2196](https://github.com/NuGet/Home/issues/2196)

- Určit `project.json` název závislosti, který se má použít pro projekty MSBuild - [#1914](https://github.com/NuGet/Home/issues/1914)

- Přidat podporu SemVer 2.0.0 do NuGet.Core - [#3383](https://github.com/NuGet/Home/issues/3383)

- Povolit přenosité závislosti NuPkgs s `.targets` k dispozici v MSBuild - [#3342](https://github.com/NuGet/Home/issues/3342)

- Obnovení NuGet z příkazového řádku je výrazně pomalejší než VS - [#3330](https://github.com/NuGet/Home/issues/3330)

- Nastavení ID balíčku a porovnání verzí malá a velká písmena – [#2522](https://github.com/NuGet/Home/issues/2522)

- NoCache možnost nefunguje `packages.config` pro založené obnovení nebo instalaci (GlobalPackagesFolder) - [#1406](https://github.com/NuGet/Home/issues/1406)

- FindPackageByIdProstředky prostředky potřebuje výchozí kontext mezipaměti a logger - [#1357](https://github.com/NuGet/Home/issues/1357)
