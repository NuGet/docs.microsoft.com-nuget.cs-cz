---
title: "Poznámky k verzi RC NuGet 4.0 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/17/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Poznámky k verzi pro NuGet 4.0 RC včetně známé problémy, opravy chyb, přidaných funkcí a chcete."
keywords: "NuGet 4.0 k vydání verze RC, opravy chyb známé problémy, přidat funkce, chcete"
ms.reviewer:
- kraigb
ms.openlocfilehash: 9156f75edc9cf72cbb1d122f01d8a071ed56a124
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-40-rc-release-notes"></a>Poznámky k verzi RC NuGet 4.0

[Poznámky k verzi 3.5 RTM NuGet](../release-notes/nuget-3.5-RTM.md)

[RC 4.0 NuGet pro Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) se zaměřuje na přidání podpory pro scénáře .NET Core, připomínkami klíče zákazníků a zlepšení výkonu v řadě scénářů. Tato verze přináší několik vylepšení, jako je podpora pro PackageReference, NuGet příkazy jako cíle MSBuild, obnovení balíčků pozadí a další.

## <a name="bug-fixes"></a>Opravy chyb

- Chování změny v `dotnet pack --version-suffix foo`  -  [#3838](https://github.com/NuGet/Home/issues/3838)

- obnovení nuget.exe vs "15" počítač selže - [#3834](https://github.com/NuGet/Home/issues/3834)

- . Nový projekt NETCore soubor by měl blokovat sestavení během obnovení - [#3780](https://github.com/NuGet/Home/issues/3780)

- Webové aplikace ASP.NET Core migrovaná z VS2015 VS "15", nelze obnovit. - [#3773](https://github.com/NuGet/Home/issues/3773)

- [Chyba testu] Balíček 'jQuery ověření, nelze je odinstalovat pomocí uživatelského rozhraní PM - [#3755](https://github.com/NuGet/Home/issues/3755)

- Při instalaci balíčku do UWP `project.json`, projekty nadřazené by měl být obnovena - [#3731](https://github.com/NuGet/Home/issues/3731)

- Úprava cíle NuGet do protokolu zdroje balíčku jako vysoké podrobností místo normální – [#3719](https://github.com/NuGet/Home/issues/3719)

- DotNet pack3 by měla obsahovat dokumentace XML ve výchozím nastavení - [#3698](https://github.com/NuGet/Home/issues/3698)

- Dávková aktualizace selže z uživatelského rozhraní, když je první zdroj bez balíček a všechny zdroj vybraný - [#3696](https://github.com/NuGet/Home/issues/3696)

- Příkaz pack Nuget nezahrnuje všechny soubory - [#3678](https://github.com/NuGet/Home/issues/3678)

- Problém OOM - [#3661](https://github.com/NuGet/Home/issues/3661)

- ProjectFileDependencyGroups část souboru, prostředky měli používat názvy knihoven pro projekty - [#3611](https://github.com/NuGet/Home/issues/3611)

- "dotnet restore" a recursing adresáře - [#3517](https://github.com/NuGet/Home/issues/3517)

- Selhání Restore3 jsou protokolovány jako upozornění místo chyby - [#3503](https://github.com/NuGet/Home/issues/3503)

- Problém sady TFS: "[soubor] není možné najít v pracovním prostoru, nebo nemáte oprávnění k přístupu"- [#2805](https://github.com/NuGet/Home/issues/2805)

- Zadejte "nuget <packagename>" v sadě vs quicklaunch vyhledávacího pole udržuje předponu "nuget" - [#2719](https://github.com/NuGet/Home/issues/2719)

- System.Xml.XmlException: Nerozpoznaný kořenový element v části základní vlastnosti. Řádek 2, pozice 2. - [#2718](https://github.com/NuGet/Home/issues/2718)

- `.nuspec`s uvozený &lt; nebo &gt; v textové pole už sestavení - [#2651](https://github.com/NuGet/Home/issues/2651)

- odstranění nuget.exe nebude vyzvat k zadání pověření (je v interaktivním režimu) - [#2626](https://github.com/NuGet/Home/issues/2626)

- odstranění nuget.exe upozorňuje klíč rozhraní API pro místní zdroje, i když nemá smysl - [#2625](https://github.com/NuGet/Home/issues/2625)

- Chyba prostředí nízká při instalaci balíčku EF - pre - [#2566](https://github.com/NuGet/Home/issues/2566)

- Visual Studio došlo k chybě, pokus po změně výběr v Správce balíčků - [#2551](https://github.com/NuGet/Home/issues/2551)

- Obnovení DotNet. Pokud jsou použity plovoucí verze - provede velká a malá písmena Id vyhledávání v dvojrozměrném seznamu místní úložiště [#2516](https://github.com/NuGet/Home/issues/2516)

- odstranění nuget.exe je porušený pro informační kanál V2 - [#2509](https://github.com/NuGet/Home/issues/2509)

- časový limit nabízené nuget.exe musí lepší chybová zpráva - [#2503](https://github.com/NuGet/Home/issues/2503)

- Nástroj obnovení bez správné importuje bez upozornění selže. - [#2462](https://github.com/NuGet/Home/issues/2462)

- NuGet vás vyzve k zadání přihlašovacích údajů, když je privátní informačního kanálu i v případě, že instalace z nuget.org - [#2346](https://github.com/NuGet/Home/issues/2346)

- Balíček ApplicationInsights 2.0, je uvedena, ale ještě - neexistuje [#2317](https://github.com/NuGet/Home/issues/2317)

- UIDelay v sadě VS "15" preview 5 větve - [#3500](https://github.com/NuGet/Home/issues/3500)

- První událost OnBuild je provedena obnovení během vytváření sestavení pro UPW - [#3489](https://github.com/NuGet/Home/issues/3489)

- Zalomení PowerShell5 EntityFramework nainstalovat? - [#3312](https://github.com/NuGet/Home/issues/3312)

- Přidání zdroje podrobné protokolování (zvažte pro 3.5) - [#3294](https://github.com/NuGet/Home/issues/3294)

- Parametr NoCache není dodržení ve verzi klienta nuget 3.4 + - [#3074](https://github.com/NuGet/Home/issues/3074)

- Pokud poskytovatel pověření se nepodaří načíst v sadě VS, nemusíte rozdělit NuGet - [#2422](https://github.com/NuGet/Home/issues/2422)

## <a name="features"></a>Funkce

- Nastavení spuštění x86-CI [#3868](https://github.com/NuGet/Home/issues/3868)

- Automatické obnovení 3/3: bez blokující uživatelské rozhraní – [#3658](https://github.com/NuGet/Home/issues/3658)

- Automatické obnovení 2/3: pozadí obnovení navrženém - [#3657](https://github.com/NuGet/Home/issues/3657)

- Obnovení projektu odolný systém souborů tak, aby odpovídaly chování sestavení (recurse) - [#3615](https://github.com/NuGet/Home/issues/3615)

- DPL podporují v sadě VS "15" – minbar - [#3614](https://github.com/NuGet/Home/issues/3614)

- Přesunout soubor s nastavením pro soubory programu - [#3613](https://github.com/NuGet/Home/issues/3613)

- Vygenerovaný obnovení props a cíle potřebují podporu zapojení cílení na mezi - [#3496](https://github.com/NuGet/Home/issues/3496)

- Obnovení NuGet podpora PackageTargetFallback (f.k.a importy) - [#3494](https://github.com/NuGet/Home/issues/3494)

- Implementace ToolsRef - [#3472](https://github.com/NuGet/Home/issues/3472)

- Restore3 pro identifikátor RID - [#3465](https://github.com/NuGet/Home/issues/3465)

- NuGet uživatelského rozhraní pro podporu přidat nebo odebrat nebo aktualizace PackageRefs - [#3457](https://github.com/NuGet/Home/issues/3457)

- Automatické obnovení 1/3: Implementace navrženém rozhraní API prostřednictvím ukládání do mezipaměti projektu obnovit informace o - [#3456](https://github.com/NuGet/Home/issues/3456)

- Obnovení [0] NuGet úloh & cíle - [#2994](https://github.com/NuGet/Home/issues/2994)

- [1] povolit řešení obnovení na úrovni v nástroji MSBuild - [#2993](https://github.com/NuGet/Home/issues/2993)

- Podporu rozšiřitelnosti veřejného poskytovatele přihlašovacích údajů v sadě Visual Studio – [#2909](https://github.com/NuGet/Home/issues/2909)

- Rekurzivní nuget restore - [#2533](https://github.com/NuGet/Home/issues/2533)

- Nelze načíst Microsoft.TeamFoundation.Client na dev15, nutné aktualizovat verzi Microsoft.TeamFoundation.Client 15.0 pro VS "15" Preview – [#2392](https://github.com/NuGet/Home/issues/2392)

- Nelze nainstalovat balíček C++ do C++ UWP projektu v sadě VS "15" Preview – [#2369](https://github.com/NuGet/Home/issues/2369)

- Nupkg musí podporovat \buildCrossTargeting\ složky - a importovat `.targets`  /  `.props` pro "crosstargeting" MSBuild oboru. - [#3499](https://github.com/NuGet/Home/issues/3499)

- Návrh ToolsReference - [#3462](https://github.com/NuGet/Home/issues/3462)

- Opravte NuGet uživatelského rozhraní pro podporu obnovení s PackageReferences v `.csproj`  -  [#3455](https://github.com/NuGet/Home/issues/3455)

- Přidání tlačítko Vymazat mezipaměť nastavení správce balíčku VS - [#3289](https://github.com/NuGet/Home/issues/3289)

## <a name="dcrs"></a>DCRs

- Řešení obnovení by se zablokovat, zatímco se děje automatického obnovení. - [#3797](https://github.com/NuGet/Home/issues/3797)

- Při instalaci NetCore z uživatelského rozhraní Správce balíčků NuGet nainstaluje do každé TFM místo ta, která podporuje balíček - [#3721](https://github.com/NuGet/Home/issues/3721)

- Obnovte nominator musí podporovat DotNetCliToolsReferences příliš rozhraní API. - [#3702](https://github.com/NuGet/Home/issues/3702)

- Označit naše VS "15" vsix jako systemcomponent - [#3700](https://github.com/NuGet/Home/issues/3700)

- Migrujte z odkazující na MS. VS. Services.Client k MS. VS. Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)

- $(RestoreLegacyPackagesDirectory) respektuje na úrovni projektu obnovením - [#3618](https://github.com/NuGet/Home/issues/3618)

- Obnovení do projektu s jeden TargetFramework nesmí podmínky props - [#3588](https://github.com/NuGet/Home/issues/3588)

- DotNet restore3 foo.csproj by měl postupujte podle projectref závislosti a ty příliš obnovit. Jako sestavení. - [#3577](https://github.com/NuGet/Home/issues/3577)

- "typ": "platformy" závislosti reprezentován jako "typ": "balíček" v souboru zámku - [#2695](https://github.com/NuGet/Home/issues/2695)

- Podrobný režim nuget.exe by měl zobrazit stahování adresy url - [#2629](https://github.com/NuGet/Home/issues/2629)

- Přesunout NuGet xplat Microsoft.NetCore.App a netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)

- Push – musí být možné přepsat na symbol server při nabízení z příkazového řádku - [#2348](https://github.com/NuGet/Home/issues/2348)

- Konsolidovat kód pro hledání na globální balíčky cesta - [#2296](https://github.com/NuGet/Home/issues/2296)

- Třeba lepší název než suppressParent - [#2196](https://github.com/NuGet/Home/issues/2196)

- Určení `project.json` název závislostí pro projektů MSBuild - [#1914](https://github.com/NuGet/Home/issues/1914)

- Přidání podpory SemVer 2.0.0 do NuGet.Core - [#3383](https://github.com/NuGet/Home/issues/3383)

- Povolit přenositelné závislostí NuPkgs s `.targets` být k dispozici v nástroji MSBuild - [#3342](https://github.com/NuGet/Home/issues/3342)

- NuGet restore z příkazovému řádku je podstatně pomalejší než VS - [#3330](https://github.com/NuGet/Home/issues/3330)

- Provést porovnání ID a verzi balíčku malá a velká písmena - [#2522](https://github.com/NuGet/Home/issues/2522)

- NoCache možnost není k dispozici pro `packages.config` obnovení nebo instalace (GlobalPackagesFolder) - [#1406](https://github.com/NuGet/Home/issues/1406)

- Prostředky FindPackageByIdResource musí mít výchozí kontext mezipaměti a protokolování - [#1357](https://github.com/NuGet/Home/issues/1357)
