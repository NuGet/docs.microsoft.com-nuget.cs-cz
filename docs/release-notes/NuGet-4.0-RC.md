---
title: Zpráva k vydání verze NuGet 4.0 RC
description: Zpráva k vydání verze pro NuGet 4.0 RC, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 02/03/2017
ms.topic: conceptual
ms.reviewer: ananguar
ms.openlocfilehash: 2d0bb6356c0a20843bdc884b68f5f61838b82e73
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549243"
---
# <a name="nuget-40-rc-release-notes"></a>Zpráva k vydání verze NuGet 4.0 RC

[Zpráva k vydání verze NuGet 3.5 RTM](../release-notes/nuget-3.5-RTM.md)

[NuGet 4.0 RC pro Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) se zaměřuje na přidání podpory pro scénáře .NET Core, adresování zpětné vazby zákazníků a vylepšení výkonu v nejrůznějších scénářích. Tato verze přináší několik vylepšení, jako je podpora pro PackageReference, NuGet příkazy jako cílů MSBuild, obnovení balíčku pozadí a další.

## <a name="bug-fixes"></a>Opravy chyb

- Chování změnami `dotnet pack --version-suffix foo`  -  [#3838](https://github.com/NuGet/Home/issues/3838)

- obnovení nuget.exe vs "15" počítač selže - [#3834](https://github.com/NuGet/Home/issues/3834)

- . Nový projekt NETCore souboru by měly blokovat sestavení během obnovení – [#3780](https://github.com/NuGet/Home/issues/3780)

- Webové aplikace ASP.NET Core migrované z VS2015 do sady VS "15", se nepovedlo obnovit. - [#3773](https://github.com/NuGet/Home/issues/3773)

- [Selhání testu] Balíček "jQuery ověření" nelze odinstalovat, v uživatelském rozhraní odp. - [#3755](https://github.com/NuGet/Home/issues/3755)

- Když se balíček nainstaluje na UPW `project.json`, má také obnovit projekty nadřazené - [#3731](https://github.com/NuGet/Home/issues/3731)

- Úprava cíle NuGet do protokolu zdroje balíčků jako vysokou úroveň podrobností místo normální – [#3719](https://github.com/NuGet/Home/issues/3719)

- DotNet
  - dotnetcore pack3 by měl obsahovat dokumentace XML ve výchozím nastavení - [#3698](https://github.com/NuGet/Home/issues/3698)

- Dávkové aktualizace nezdaří z uživatelského rozhraní při zdroje bez balíček je první a všechny zdroje je vybrán - [#3696](https://github.com/NuGet/Home/issues/3696)

- Příkaz balíčku Nuget neobsahuje všechny soubory – [#3678](https://github.com/NuGet/Home/issues/3678)

- Problém OOM - [#3661](https://github.com/NuGet/Home/issues/3661)

- ProjectFileDependencyGroups části souboru prostředků by měl použít názvy knihoven pro projekty – [#3611](https://github.com/NuGet/Home/issues/3611)

- "dotnet restore" a recursing adresáře - [#3517](https://github.com/NuGet/Home/issues/3517)

- Restore3 chyby jsou protokolovány jako upozornění místo chyby - [#3503](https://github.com/NuGet/Home/issues/3503)

- Problém TFS: "[soubor] nebyly nalezeny ve vašem pracovním prostoru, nebo nemáte oprávnění k přístupu"- [#2805](https://github.com/NuGet/Home/issues/2805)

- Zadáním "nuget <packagename>" v sadě Visual Studio uchovává rychlé spuštění vyhledávacího pole "nuget" předponu - [#2719](https://github.com/NuGet/Home/issues/2719)

- System.Xml.XmlException: Neznámý kořenový prvek součásti Core Properties. Řádek 2, pozice 2. - [#2718](https://github.com/NuGet/Home/issues/2718)

- `.nuspec` s uvozeny řídicími znaky &lt; nebo &gt; v textové pole již sestavení - [#2651](https://github.com/NuGet/Home/issues/2651)

- Odstranit nuget.exe nezobrazí výzvu pro přihlašovací údaje (je v neinteraktivním režimu) – [#2626](https://github.com/NuGet/Home/issues/2626)

- Odstranit nuget.exe upozorňuje klíč rozhraní API pro místní zdroje, i když nemá žádný smysl - [#2625](https://github.com/NuGet/Home/issues/2625)

- Špatné zkušenosti chyby při instalaci EF - pre package - [#2566](https://github.com/NuGet/Home/issues/2566)

- Visual Studio pokusem po změně výběru došlo k chybě ve správci balíčků - [#2551](https://github.com/NuGet/Home/issues/2551)

- DotNet
  - obnovení dotnetcore provádí velká a malá písmena vyhledávání Id v plochém seznamu místních úložišť, když se používají s plovoucí desetinnou čárkou verze - [#2516](https://github.com/NuGet/Home/issues/2516)

- Odstranit nuget.exe je porušený pro kanál V2 – [#2509](https://github.com/NuGet/Home/issues/2509)

- časový limit nabízených oznámení nuget.exe vyžaduje lepší chybové zprávy - [#2503](https://github.com/NuGet/Home/issues/2503)

- Nástroj pro obnovení bez správných importuje bez upozornění selže. - [#2462](https://github.com/NuGet/Home/issues/2462)

- NuGet vás vyzve k zadání přihlašovacích údajů, když je privátní kanál i v případě, že instalace z webu nuget.org - [#2346](https://github.com/NuGet/Home/issues/2346)

- Balíček ApplicationInsights 2.0 je uvedena, ale ještě - neexistuje [#2317](https://github.com/NuGet/Home/issues/2317)

- UIDelay v sadě Visual Studio "15" preview 5 větev - [#3500](https://github.com/NuGet/Home/issues/3500)

- První událost OnBuild chybí pro obnovení během sestavování pro UPW – [#3489](https://github.com/NuGet/Home/issues/3489)

- Nainstaluje se při PowerShell5 konce objektu EntityFramework? - [#3312](https://github.com/NuGet/Home/issues/3312)

- Přidání zdroje podrobné protokolování (zvažte pro 3.5) - [#3294](https://github.com/NuGet/Home/issues/3294)

- Parametr NoCache není zachované verzi klienta nuget 3.4 + - [#3074](https://github.com/NuGet/Home/issues/3074)

- Když poskytovatele přihlašovacích údajů se nepodaří načíst v sadě Visual Studio, neovlivní NuGet - [#2422](https://github.com/NuGet/Home/issues/2422)

## <a name="features"></a>Funkce

- Nastavte průběžnou Integraci pro spuštění x86- [#3868](https://github.com/NuGet/Home/issues/3868)

- Automatické obnovení 3/3: jiné blokující prvky UI - [#3658](https://github.com/NuGet/Home/issues/3658)

- Automatické obnovení 2/3: na pozadí obnovení nominace - [#3657](https://github.com/NuGet/Home/issues/3657)

- Obnovit odolný systém souborů projektu tak, aby odpovídaly chování sestavení (recurse) - [#3615](https://github.com/NuGet/Home/issues/3615)

- V sadě Visual Studio "15" – minbar – podpora DPL [#3614](https://github.com/NuGet/Home/issues/3614)

- Přesunout soubor s nastavením na Program Files - [#3613](https://github.com/NuGet/Home/issues/3613)

- Cíle a vlastnosti vygenerované obnovení potřebujete podporu zapojení cílení na různé - [#3496](https://github.com/NuGet/Home/issues/3496)

- Podpora obnovení NuGet pro PackageTargetFallback (f.k.a importy) - [#3494](https://github.com/NuGet/Home/issues/3494)

- Implementace ToolsRef - [#3472](https://github.com/NuGet/Home/issues/3472)

- Restore3 pro identifikátorů RID - [#3465](https://github.com/NuGet/Home/issues/3465)

- NuGet uživatelského rozhraní pro podporu přidat nebo odebrat nebo aktualizovat PackageRefs - [#3457](https://github.com/NuGet/Home/issues/3457)

- Automatické obnovení 1/3: Implementace nominace rozhraní API prostřednictvím ukládání do mezipaměti projektu obnovit informace o - [#3456](https://github.com/NuGet/Home/issues/3456)

- Obnovení NuGet [0], úlohy a cíle - [#2994](https://github.com/NuGet/Home/issues/2994)

- [1] povolit řešení obnovení na úrovni v nástroji MSBuild - [#2993](https://github.com/NuGet/Home/issues/2993)

- Podpora rozšiřitelnosti veřejného poskytovatele přihlašovacích údajů v sadě Visual Studio – [#2909](https://github.com/NuGet/Home/issues/2909)

- Rekurzivní nuget restore - [#2533](https://github.com/NuGet/Home/issues/2533)

- Nelze načíst Microsoft.TeamFoundation.Client na odkaz na dev15, muset aktualizovat Microsoft.TeamFoundation.Client verzi 15.0 pro VS "15" Preview – [#2392](https://github.com/NuGet/Home/issues/2392)

- Nepovedlo se nainstalovat balíček C++ k C++ UWP projektu v sadě Visual Studio "15" Preview – [#2369](https://github.com/NuGet/Home/issues/2369)

- Nupkg musí podporovat \buildCrossTargeting\ složka – a importovat `.targets`  /  `.props` pro "crosstargeting" MSBuild oboru. - [#3499](https://github.com/NuGet/Home/issues/3499)

- Návrh ToolsReference – [#3462](https://github.com/NuGet/Home/issues/3462)

- Oprava NuGet uživatelského rozhraní pro podporu obnovení s PackageReferences v `.csproj`  -  [#3455](https://github.com/NuGet/Home/issues/3455)

- Přidání tlačítka Vymazat mezipaměť nastavení Správce balíčků VS - [#3289](https://github.com/NuGet/Home/issues/3289)

## <a name="dcrs"></a>Chcete

- Řešení obnovení by měly být blokovány, zatímco probíhá automatické obnovení. - [#3797](https://github.com/NuGet/Home/issues/3797)

- Instalace NetCore z uživatelského rozhraní Správce balíčků NuGet nainstaluje do každé TFM místo, které podporuje balíčku - [#3721](https://github.com/NuGet/Home/issues/3721)

- Obnovte nominator rozhraní API musí podporovat DotNetCliToolsReferences příliš. - [#3702](https://github.com/NuGet/Home/issues/3702)

- Označit naší sady VS "15" vsix jako systemcomponent - [#3700](https://github.com/NuGet/Home/issues/3700)

- Migrace z odkazující na MS. VS. Services.Client do MS. VS. Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)

- $(RestoreLegacyPackagesDirectory) by měly dodržovat na úrovni projektu obnovení – [#3618](https://github.com/NuGet/Home/issues/3618)

- Obnovení do projektu pomocí jedné TargetFramework nesmí podmínky props – [#3588](https://github.com/NuGet/Home/issues/3588)

- DotNet
  - dotnetcore restore3 foo.csproj by měl postupujte podle projectref závislostí a těch obnovení příliš. Stejně jako sestavení. - [#3577](https://github.com/NuGet/Home/issues/3577)

- "type": "platformy" závislosti reprezentované jako "type": "balíček" v souboru zámku - [#2695](https://github.com/NuGet/Home/issues/2695)

- režim podrobného vypisování nuget.exe by se zobrazit soubor ke stažení adresa url – [#2629](https://github.com/NuGet/Home/issues/2629)

- Přesunout NuGet xplat pro balíčky Microsoft.NetCore.App a netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)

- Push – bude možné přepsat server symbolů při odesílání z příkazového řádku - [#2348](https://github.com/NuGet/Home/issues/2348)

- Sloučit kód pro vyhledání globálních balíčků cesta - [#2296](https://github.com/NuGet/Home/issues/2296)

- Třeba názvu lepší než suppressParent - [#2196](https://github.com/NuGet/Home/issues/2196)

- Určení `project.json` název závislosti pro projekty MSBuild - [#1914](https://github.com/NuGet/Home/issues/1914)

- Přidání podpory SemVer 2.0.0 NuGet.Core - [#3383](https://github.com/NuGet/Home/issues/3383)

- Povolit přechodné závislosti NuPkgs s `.targets` k dispozici v nástroji MSBuild - [#3342](https://github.com/NuGet/Home/issues/3342)

- Obnovení NuGet řádku je výrazně pomalejší než VS - [#3330](https://github.com/NuGet/Home/issues/3330)

- Provést porovnání ID a verzi balíčku malá a velká písmena - [#2522](https://github.com/NuGet/Home/issues/2522)

- Možnost NoCache nefunguje pro `packages.config` na základě obnovení/install (GlobalPackagesFolder) - [#1406](https://github.com/NuGet/Home/issues/1406)

- Prostředky FindPackageByIdResource potřebuje výchozí kontext mezipaměti a protokolování - [#1357](https://github.com/NuGet/Home/issues/1357)
