---
title: Poznámky k verzi NuGet 4,0 RC
description: Poznámky k verzi pro NuGet 4,0 RC, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 02/03/2017
ms.topic: conceptual
ms.reviewer: ananguar
ms.openlocfilehash: 44f15e2fc33cca8a3d88af17bf76f1dcc16ca860
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780193"
---
# <a name="nuget-40-rc-release-notes"></a>Poznámky k verzi NuGet 4,0 RC

[Poznámky k verzi NuGet 3,5 RTM](../release-notes/nuget-3.5-RTM.md)

[NuGet 4,0 RC for Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) se zaměřuje na přidání podpory pro scénáře .NET Core, adresování klíčových připomínek zákazníků a zlepšení výkonu v nejrůznějších scénářích. Tato vydaná verze přináší několik vylepšení, jako je podpora PackageReference, příkazů NuGet jako cílů MSBuild, obnovení balíčku na pozadí a další.

## <a name="bug-fixes"></a>Opravy chyb

- Změny chování v `dotnet pack --version-suffix foo`  -  [#3838](https://github.com/NuGet/Home/issues/3838)

- nuget.exe obnovení v počítači vs "15" se nezdařila. [#3834](https://github.com/NuGet/Home/issues/3834)

- . Soubor NETCore nový projekt by měl blokovat sestavení během obnovení- [#3780](https://github.com/NuGet/Home/issues/3780)

- ASP.NET Core webové aplikace migrované z VS2015 do VS "15" nelze obnovit. - [#3773](https://github.com/NuGet/Home/issues/3773)

- [Selhání testu] Balíček jQuery se nedá odinstalovat pomocí uživatelského rozhraní PM – [#3755](https://github.com/NuGet/Home/issues/3755) .

- Při instalaci balíčku do UWP `project.json` by měly být obnoveny i nadřazené projekty – [#3731](https://github.com/NuGet/Home/issues/3731)

- Úprava cílů NuGet pro protokolování zdrojů balíčku jako vysoké podrobností místo normálního [#3719](https://github.com/NuGet/Home/issues/3719)

- dotnet
  - dotnetcore Pack3 by měl ve výchozím nastavení zahrnovat dokumentaci XML – [#3698](https://github.com/NuGet/Home/issues/3698)

- Při prvním použití zdroje bez tohoto balíčku se aktualizace dávky nezdařila z uživatelského rozhraní a je vybrán všechny zdroje – [#3696](https://github.com/NuGet/Home/issues/3696)

- Příkaz NuGet Pack nezahrnuje všechny soubory – [#3678](https://github.com/NuGet/Home/issues/3678)

- Problém OOM – [#3661](https://github.com/NuGet/Home/issues/3661)

- Oddíl ProjectFileDependencyGroups v souboru assets by měl používat názvy knihoven pro projekty – [#3611](https://github.com/NuGet/Home/issues/3611)

- "dotnet restore" a opakují se adresáře – [#3517](https://github.com/NuGet/Home/issues/3517)

- Restore3 chyby se protokolují jako upozornění, nikoli chyby – [#3503](https://github.com/NuGet/Home/issues/3503)

- Problém TFS: "[soubor] není ve vašem pracovním prostoru nalezen, nebo nemáte oprávnění k němu přistupovat"- [#2805](https://github.com/NuGet/Home/issues/2805)

- Zadáním "NuGet <packagename> " do vyhledávacího pole vs rychlé spuštění je "NuGet" prefix- [#2719](https://github.com/NuGet/Home/issues/2719)

- Výjimka System.Xml.Xml: nerozpoznaný kořenový element v části Core Properties. Řádek 2, pozice 2 - [#2718](https://github.com/NuGet/Home/issues/2718)

- `.nuspec` s řídicími &lt; a &gt; textovými poli již nejsou vytvářeny [#2651](https://github.com/NuGet/Home/issues/2651)

- nuget.exe při odstraňování se nezobrazí výzva k zadání přihlašovacích údajů (je v neinteraktivním režimu) – [#2626](https://github.com/NuGet/Home/issues/2626)

- nuget.exe odstranit upozorňuje na klíč rozhraní API pro místní zdroje, a to i v případě, že neposkytuje žádný smysl [#2625](https://github.com/NuGet/Home/issues/2625)

- Při instalaci balíčku EF-pre- [#2566](https://github.com/NuGet/Home/issues/2566) došlo k chybě.

- Při pokusu o změnu výběru ve Správci balíčků došlo k chybě sady Visual Studio – [#2551](https://github.com/NuGet/Home/issues/2551)

- dotnet
  - dotnetcore Restore při použití plovoucí verze v místních úložištích s nestrukturovaným seznamem provede vyhledávání ID s rozlišením malých a velkých písmen. [#2516](https://github.com/NuGet/Home/issues/2516)

- Pro informační kanál v2 je nuget.exe odstranění poškozeno. [#2509](https://github.com/NuGet/Home/issues/2509)

- nuget.exe časový limit pro vložení vyžaduje lepší chybovou zprávu – [#2503](https://github.com/NuGet/Home/issues/2503)

- Obnovení nástroje bez jakýchkoli řádných importů se nezdařila. - [#2462](https://github.com/NuGet/Home/issues/2462)

- Při instalaci z nuget.org- [#2346](https://github.com/NuGet/Home/issues/2346) výzvy NuGet k zadání přihlašovacích údajů.

- Balíček ApplicationInsights 2,0 je uveden, ale ještě neexistuje – [#2317](https://github.com/NuGet/Home/issues/2317)

- UIDelay v sadě VS "15" Preview 5 větví – [#3500](https://github.com/NuGet/Home/issues/3500)

- První událost při sestavení se pro obnovení nesestavila při sestavování pro UWP – [#3489](https://github.com/NuGet/Home/issues/3489)

- PowerShell5 ukončí instalaci EntityFramework? - [#3312](https://github.com/NuGet/Home/issues/3312)

- Přidat zdroj do podrobného protokolování (Zvažte 3,5)- [#3294](https://github.com/NuGet/Home/issues/3294)

- Parametr nezadané mezipaměti se nedodržuje v klientovi NuGet verze 3.4 a [#3074](https://github.com/NuGet/Home/issues/3074)

- Když se poskytovatel přihlašovacích údajů nepovede načíst v VS, Nerušit NuGet- [#2422](https://github.com/NuGet/Home/issues/2422)

## <a name="features"></a>Funkce

- Nastavení CI pro spuštění x86- [#3868](https://github.com/NuGet/Home/issues/3868)

- Automatické obnovení 3/3: uživatelské rozhraní bez blokování [#3658](https://github.com/NuGet/Home/issues/3658)

- Automatické obnovení 2/3: obnovení na pozadí při jmenování – [#3657](https://github.com/NuGet/Home/issues/3657)

- Obnovit odkazy projektu tak, aby odpovídaly chování sestavení (rekurze) – [#3615](https://github.com/NuGet/Home/issues/3615)

- Podpora DPL v VS "15"-Minbar- [#3614](https://github.com/NuGet/Home/issues/3614)

- Přesunout soubor nastavení do programových souborů – [#3613](https://github.com/NuGet/Home/issues/3613)

- Vygenerovaná props a cíle vyžadují podporu pro zapojení do více cílů – [#3496](https://github.com/NuGet/Home/issues/3496)

- Podpora obnovení NuGet pro PackageTargetFallback (f. k. a Imports) – [#3494](https://github.com/NuGet/Home/issues/3494)

- Implementace ToolsRef – [#3472](https://github.com/NuGet/Home/issues/3472)

- Restore3 pro identifikátor RID- [#3465](https://github.com/NuGet/Home/issues/3465)

- Uživatelské rozhraní NuGet pro podporu přidání/odebrání/aktualizace PackageRefs- [#3457](https://github.com/NuGet/Home/issues/3457)

- Automatické obnovení 1/3: implementaci rozhraní API prostřednictvím ukládání informací o obnovení projektu do mezipaměti – [#3456](https://github.com/NuGet/Home/issues/3456)

- [0] úloha obnovení NuGet & cíle – [#2994](https://github.com/NuGet/Home/issues/2994)

- [1] povolit obnovení na úrovni řešení v MSBuildu – [#2993](https://github.com/NuGet/Home/issues/2993)

- Podpora veřejné rozšiřitelnosti poskytovatele přihlašovacích údajů v aplikaci Visual Studio – [#2909](https://github.com/NuGet/Home/issues/2909)

- Rekurzivní obnovení NuGet – [#2533](https://github.com/NuGet/Home/issues/2533)

- Nelze načíst Microsoft. TeamFoundation. Client na dev15, je třeba aktualizovat Microsoft. TeamFoundation. Client verze na 15,0 pro VS "15" Preview- [#2392](https://github.com/NuGet/Home/issues/2392)

- Nejde nainstalovat balíček C++ do projektu UWP pro platformu C++ ve verzi VS "15" Preview – [#2369](https://github.com/NuGet/Home/issues/2369)

- Nupkg musí podporovat \buildCrossTargeting\ složku a importovat `.targets`  /  `.props` pro obor "crosstargeting" MSBuild. - [#3499](https://github.com/NuGet/Home/issues/3499)

- Návrh ToolsReference – [#3462](https://github.com/NuGet/Home/issues/3462)

- Opravte uživatelské rozhraní NuGet pro podporu obnovení s PackageReferences v `.csproj`  -  [#3455](https://github.com/NuGet/Home/issues/3455)

- Přidání tlačítka Vymazat mezipaměť do nastavení správce balíčků VS – [#3289](https://github.com/NuGet/Home/issues/3289)

## <a name="dcrs"></a>Chcete odeslat obecnou

- Při automatickém obnovení by mělo být zablokováno obnovení řešení. - [#3797](https://github.com/NuGet/Home/issues/3797)

- NetCore instalovat z uživatelského rozhraní Správce balíčků NuGet se nainstalují do všech TFM a místo těch, které balíček podporuje – [#3721](https://github.com/NuGet/Home/issues/3721)

- Rozhraní API pro restoreer musí podporovat i DotNetCliToolsReferences. - [#3702](https://github.com/NuGet/Home/issues/3702)

- Označení našeho souboru VSIX VS "15" jako SystemComponent- [#3700](https://github.com/NuGet/Home/issues/3700)

- Migrujte z referenčního MS. Infrastruktura. Services. Client do MS. Infrastruktura. Services. Client. Interactive – [#3670](https://github.com/NuGet/Home/issues/3670)

- $ (RestoreLegacyPackagesDirectory) by se mělo dodržovat na úrovni projektu obnovením- [#3618](https://github.com/NuGet/Home/issues/3618)

- Obnovení do projektu s jednou TargetFramework nesmí být podmínkou- [#3588](https://github.com/NuGet/Home/issues/3588)

- dotnet
  - dotnetcore restore3 foo. csproj by měl splňovat závislosti projectref a obnovit je. Podobně jako sestavení. - [#3577](https://github.com/NuGet/Home/issues/3577)

- "typ": závislosti na platformě reprezentované jako "typ": "balíček" v souboru zámku – [#2695](https://github.com/NuGet/Home/issues/2695)

- nuget.exe režimu podrobného zobrazení by se měla zobrazit adresa URL pro stažení – [#2629](https://github.com/NuGet/Home/issues/2629)

- Přesunout NuGet xplat do Microsoft. NetCore. app a netcoreapp 1.0- [#2483](https://github.com/NuGet/Home/issues/2483)

- Push – při vkládání z příkazového řádku by mělo být možné přepsat server symbolů. [#2348](https://github.com/NuGet/Home/issues/2348)

- Konsolidovat kód pro hledání cesty globálních balíčků – [#2296](https://github.com/NuGet/Home/issues/2296)

- Je potřeba lepší název než suppressParent- [#2196](https://github.com/NuGet/Home/issues/2196)

- Určení `project.json` názvu závislosti, který se má použít pro projekty MSBuild – [#1914](https://github.com/NuGet/Home/issues/1914)

- Přidejte podporu 2.0.0 SemVer do NuGet. Core- [#3383](https://github.com/NuGet/Home/issues/3383)

- Povolení dostupnosti přenosných závislostí NuPkgs s nástrojem `.targets` v MSBuild- [#3342](https://github.com/NuGet/Home/issues/3342)

- Obnovení NuGet z příkazového řádku je výrazně pomalejší než v sadě VS- [#3330](https://github.com/NuGet/Home/issues/3330)

- Vyměnit ID a rozlišování velikosti písmen a rozlišovat velká a malá písmena – [#2522](https://github.com/NuGet/Home/issues/2522)

- Možnost ukládání do mezipaměti nefunguje pro `packages.config` obnovení nebo instalaci (GlobalPackagesFolder) – [#1406](https://github.com/NuGet/Home/issues/1406)

- Prostředky FindPackageByIdResource musí mít výchozí kontext mezipaměti a protokolovací nástroj- [#1357](https://github.com/NuGet/Home/issues/1357)
