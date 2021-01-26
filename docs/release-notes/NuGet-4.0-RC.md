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
# <a name="nuget-40-rc-release-notes"></a><span data-ttu-id="bb545-103">Poznámky k verzi NuGet 4,0 RC</span><span class="sxs-lookup"><span data-stu-id="bb545-103">NuGet 4.0 RC Release Notes</span></span>

[<span data-ttu-id="bb545-104">Poznámky k verzi NuGet 3,5 RTM</span><span class="sxs-lookup"><span data-stu-id="bb545-104">NuGet 3.5 RTM Release Notes</span></span>](../release-notes/nuget-3.5-RTM.md)

<span data-ttu-id="bb545-105">[NuGet 4,0 RC for Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) se zaměřuje na přidání podpory pro scénáře .NET Core, adresování klíčových připomínek zákazníků a zlepšení výkonu v nejrůznějších scénářích.</span><span class="sxs-lookup"><span data-stu-id="bb545-105">[NuGet 4.0 RC for Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) is focused on adding support for .NET Core scenarios, addressing key customer feedback and improving performance in a variety of scenarios.</span></span> <span data-ttu-id="bb545-106">Tato vydaná verze přináší několik vylepšení, jako je podpora PackageReference, příkazů NuGet jako cílů MSBuild, obnovení balíčku na pozadí a další.</span><span class="sxs-lookup"><span data-stu-id="bb545-106">This release brings several improvements like support for PackageReference, NuGet commands as MSBuild targets, background package restore, and more.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="bb545-107">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="bb545-107">Bug Fixes</span></span>

- <span data-ttu-id="bb545-108">Změny chování v `dotnet pack --version-suffix foo`  -  [#3838](https://github.com/NuGet/Home/issues/3838)</span><span class="sxs-lookup"><span data-stu-id="bb545-108">Behavioral changes in `dotnet pack --version-suffix foo` - [#3838](https://github.com/NuGet/Home/issues/3838)</span></span>

- <span data-ttu-id="bb545-109">nuget.exe obnovení v počítači vs "15" se nezdařila. [#3834](https://github.com/NuGet/Home/issues/3834)</span><span class="sxs-lookup"><span data-stu-id="bb545-109">nuget.exe restore on vs "15" machine only fails - [#3834](https://github.com/NuGet/Home/issues/3834)</span></span>

- <span data-ttu-id="bb545-110">. Soubor NETCore nový projekt by měl blokovat sestavení během obnovení- [#3780](https://github.com/NuGet/Home/issues/3780)</span><span class="sxs-lookup"><span data-stu-id="bb545-110">.NETCore file new project should block the build during restore - [#3780](https://github.com/NuGet/Home/issues/3780)</span></span>

- <span data-ttu-id="bb545-111">ASP.NET Core webové aplikace migrované z VS2015 do VS "15" nelze obnovit.</span><span class="sxs-lookup"><span data-stu-id="bb545-111">ASP.NET Core web app, migrated from VS2015 to VS "15", unable to restore.</span></span><span data-ttu-id="bb545-112"> - [#3773](https://github.com/NuGet/Home/issues/3773)</span><span class="sxs-lookup"><span data-stu-id="bb545-112"> - [#3773](https://github.com/NuGet/Home/issues/3773)</span></span>

- <span data-ttu-id="bb545-113">[Selhání testu] Balíček jQuery se nedá odinstalovat pomocí uživatelského rozhraní PM – [#3755](https://github.com/NuGet/Home/issues/3755) .</span><span class="sxs-lookup"><span data-stu-id="bb545-113">[Test Failure]Package ‘jQuery Validation’ can’t be uninstalled by PM UI - [#3755](https://github.com/NuGet/Home/issues/3755)</span></span>

- <span data-ttu-id="bb545-114">Při instalaci balíčku do UWP `project.json` by měly být obnoveny i nadřazené projekty – [#3731](https://github.com/NuGet/Home/issues/3731)</span><span class="sxs-lookup"><span data-stu-id="bb545-114">When a package is installed to UWP `project.json`, parent projects should also be restored - [#3731](https://github.com/NuGet/Home/issues/3731)</span></span>

- <span data-ttu-id="bb545-115">Úprava cílů NuGet pro protokolování zdrojů balíčku jako vysoké podrobností místo normálního [#3719](https://github.com/NuGet/Home/issues/3719)</span><span class="sxs-lookup"><span data-stu-id="bb545-115">Modify the NuGet targets to log the package sources as High verbosity instead of Normal - [#3719](https://github.com/NuGet/Home/issues/3719)</span></span>

- <span data-ttu-id="bb545-116">dotnet</span><span class="sxs-lookup"><span data-stu-id="bb545-116">dotnet</span></span>
  - <span data-ttu-id="bb545-117">dotnetcore Pack3 by měl ve výchozím nastavení zahrnovat dokumentaci XML – [#3698](https://github.com/NuGet/Home/issues/3698)</span><span class="sxs-lookup"><span data-stu-id="bb545-117">dotnetcore pack3 should include XML documentation by default - [#3698](https://github.com/NuGet/Home/issues/3698)</span></span>

- <span data-ttu-id="bb545-118">Při prvním použití zdroje bez tohoto balíčku se aktualizace dávky nezdařila z uživatelského rozhraní a je vybrán všechny zdroje – [#3696](https://github.com/NuGet/Home/issues/3696)</span><span class="sxs-lookup"><span data-stu-id="bb545-118">Batch update fails from UI when source without the package is first and All source is selected - [#3696](https://github.com/NuGet/Home/issues/3696)</span></span>

- <span data-ttu-id="bb545-119">Příkaz NuGet Pack nezahrnuje všechny soubory – [#3678](https://github.com/NuGet/Home/issues/3678)</span><span class="sxs-lookup"><span data-stu-id="bb545-119">Nuget pack command does not include all files - [#3678](https://github.com/NuGet/Home/issues/3678)</span></span>

- <span data-ttu-id="bb545-120">Problém OOM – [#3661](https://github.com/NuGet/Home/issues/3661)</span><span class="sxs-lookup"><span data-stu-id="bb545-120">OOM issue - [#3661](https://github.com/NuGet/Home/issues/3661)</span></span>

- <span data-ttu-id="bb545-121">Oddíl ProjectFileDependencyGroups v souboru assets by měl používat názvy knihoven pro projekty – [#3611](https://github.com/NuGet/Home/issues/3611)</span><span class="sxs-lookup"><span data-stu-id="bb545-121">ProjectFileDependencyGroups section of the assets file should use library names for projects - [#3611](https://github.com/NuGet/Home/issues/3611)</span></span>

- <span data-ttu-id="bb545-122">"dotnet restore" a opakují se adresáře – [#3517](https://github.com/NuGet/Home/issues/3517)</span><span class="sxs-lookup"><span data-stu-id="bb545-122">"dotnet restore" and recursing directories - [#3517](https://github.com/NuGet/Home/issues/3517)</span></span>

- <span data-ttu-id="bb545-123">Restore3 chyby se protokolují jako upozornění, nikoli chyby – [#3503](https://github.com/NuGet/Home/issues/3503)</span><span class="sxs-lookup"><span data-stu-id="bb545-123">Restore3 failures are logged as warnings instead of errors - [#3503](https://github.com/NuGet/Home/issues/3503)</span></span>

- <span data-ttu-id="bb545-124">Problém TFS: "[soubor] není ve vašem pracovním prostoru nalezen, nebo nemáte oprávnění k němu přistupovat"- [#2805](https://github.com/NuGet/Home/issues/2805)</span><span class="sxs-lookup"><span data-stu-id="bb545-124">TFS issue: "[file]not be found in your workspace, or you do not have permission to access it" - [#2805](https://github.com/NuGet/Home/issues/2805)</span></span>

- <span data-ttu-id="bb545-125">Zadáním "NuGet <packagename> " do vyhledávacího pole vs rychlé spuštění je "NuGet" prefix- [#2719](https://github.com/NuGet/Home/issues/2719)</span><span class="sxs-lookup"><span data-stu-id="bb545-125">Typing "nuget <packagename>" in vs quicklaunch search box keeps "nuget " prefix - [#2719](https://github.com/NuGet/Home/issues/2719)</span></span>

- <span data-ttu-id="bb545-126">Výjimka System.Xml.Xml: nerozpoznaný kořenový element v části Core Properties.</span><span class="sxs-lookup"><span data-stu-id="bb545-126">System.Xml.XmlException: Unrecognized root element in Core Properties part.</span></span> <span data-ttu-id="bb545-127">Řádek 2, pozice 2</span><span class="sxs-lookup"><span data-stu-id="bb545-127">Line 2, position 2.</span></span><span data-ttu-id="bb545-128"> - [#2718](https://github.com/NuGet/Home/issues/2718)</span><span class="sxs-lookup"><span data-stu-id="bb545-128"> - [#2718](https://github.com/NuGet/Home/issues/2718)</span></span>

- <span data-ttu-id="bb545-129">`.nuspec` s řídicími &lt; a &gt; textovými poli již nejsou vytvářeny [#2651](https://github.com/NuGet/Home/issues/2651)</span><span class="sxs-lookup"><span data-stu-id="bb545-129">`.nuspec` with escaped &lt; or &gt; in text fields no longer builds - [#2651](https://github.com/NuGet/Home/issues/2651)</span></span>

- <span data-ttu-id="bb545-130">nuget.exe při odstraňování se nezobrazí výzva k zadání přihlašovacích údajů (je v neinteraktivním režimu) – [#2626](https://github.com/NuGet/Home/issues/2626)</span><span class="sxs-lookup"><span data-stu-id="bb545-130">nuget.exe delete won't prompt for credentials (it's in non-interactive mode) - [#2626](https://github.com/NuGet/Home/issues/2626)</span></span>

- <span data-ttu-id="bb545-131">nuget.exe odstranit upozorňuje na klíč rozhraní API pro místní zdroje, a to i v případě, že neposkytuje žádný smysl [#2625](https://github.com/NuGet/Home/issues/2625)</span><span class="sxs-lookup"><span data-stu-id="bb545-131">nuget.exe delete warns about API Key for local sources, even though it makes no sense - [#2625](https://github.com/NuGet/Home/issues/2625)</span></span>

- <span data-ttu-id="bb545-132">Při instalaci balíčku EF-pre- [#2566](https://github.com/NuGet/Home/issues/2566) došlo k chybě.</span><span class="sxs-lookup"><span data-stu-id="bb545-132">Error experience poor when installing EF -pre package - [#2566](https://github.com/NuGet/Home/issues/2566)</span></span>

- <span data-ttu-id="bb545-133">Při pokusu o změnu výběru ve Správci balíčků došlo k chybě sady Visual Studio – [#2551](https://github.com/NuGet/Home/issues/2551)</span><span class="sxs-lookup"><span data-stu-id="bb545-133">Visual Studio crashed attempting after changing selection in Package Manager - [#2551](https://github.com/NuGet/Home/issues/2551)</span></span>

- <span data-ttu-id="bb545-134">dotnet</span><span class="sxs-lookup"><span data-stu-id="bb545-134">dotnet</span></span>
  - <span data-ttu-id="bb545-135">dotnetcore Restore při použití plovoucí verze v místních úložištích s nestrukturovaným seznamem provede vyhledávání ID s rozlišením malých a velkých písmen. [#2516](https://github.com/NuGet/Home/issues/2516)</span><span class="sxs-lookup"><span data-stu-id="bb545-135">dotnetcore restore performs case sensitive Id lookups on flat-list local repositories when floating versions are used - [#2516](https://github.com/NuGet/Home/issues/2516)</span></span>

- <span data-ttu-id="bb545-136">Pro informační kanál v2 je nuget.exe odstranění poškozeno. [#2509](https://github.com/NuGet/Home/issues/2509)</span><span class="sxs-lookup"><span data-stu-id="bb545-136">nuget.exe delete is broken for V2 feed - [#2509](https://github.com/NuGet/Home/issues/2509)</span></span>

- <span data-ttu-id="bb545-137">nuget.exe časový limit pro vložení vyžaduje lepší chybovou zprávu – [#2503](https://github.com/NuGet/Home/issues/2503)</span><span class="sxs-lookup"><span data-stu-id="bb545-137">nuget.exe push timeout needs a better error message - [#2503](https://github.com/NuGet/Home/issues/2503)</span></span>

- <span data-ttu-id="bb545-138">Obnovení nástroje bez jakýchkoli řádných importů se nezdařila.</span><span class="sxs-lookup"><span data-stu-id="bb545-138">Tool restore without proper imports silently fails.</span></span><span data-ttu-id="bb545-139"> - [#2462](https://github.com/NuGet/Home/issues/2462)</span><span class="sxs-lookup"><span data-stu-id="bb545-139"> - [#2462](https://github.com/NuGet/Home/issues/2462)</span></span>

- <span data-ttu-id="bb545-140">Při instalaci z nuget.org- [#2346](https://github.com/NuGet/Home/issues/2346) výzvy NuGet k zadání přihlašovacích údajů.</span><span class="sxs-lookup"><span data-stu-id="bb545-140">NuGet prompts to enter credentials when there is a private feed even when installing from nuget.org - [#2346](https://github.com/NuGet/Home/issues/2346)</span></span>

- <span data-ttu-id="bb545-141">Balíček ApplicationInsights 2,0 je uveden, ale ještě neexistuje – [#2317](https://github.com/NuGet/Home/issues/2317)</span><span class="sxs-lookup"><span data-stu-id="bb545-141">ApplicationInsights 2.0 package is listed but doesn't exist yet - [#2317](https://github.com/NuGet/Home/issues/2317)</span></span>

- <span data-ttu-id="bb545-142">UIDelay v sadě VS "15" Preview 5 větví – [#3500](https://github.com/NuGet/Home/issues/3500)</span><span class="sxs-lookup"><span data-stu-id="bb545-142">UIDelay in VS "15" preview 5 branch - [#3500](https://github.com/NuGet/Home/issues/3500)</span></span>

- <span data-ttu-id="bb545-143">První událost při sestavení se pro obnovení nesestavila při sestavování pro UWP – [#3489](https://github.com/NuGet/Home/issues/3489)</span><span class="sxs-lookup"><span data-stu-id="bb545-143">First OnBuild event is missed for Restore during Build for UWP - [#3489](https://github.com/NuGet/Home/issues/3489)</span></span>

- <span data-ttu-id="bb545-144">PowerShell5 ukončí instalaci EntityFramework?</span><span class="sxs-lookup"><span data-stu-id="bb545-144">PowerShell5 breaks EntityFramework install?</span></span><span data-ttu-id="bb545-145"> - [#3312](https://github.com/NuGet/Home/issues/3312)</span><span class="sxs-lookup"><span data-stu-id="bb545-145"> - [#3312](https://github.com/NuGet/Home/issues/3312)</span></span>

- <span data-ttu-id="bb545-146">Přidat zdroj do podrobného protokolování (Zvažte 3,5)- [#3294](https://github.com/NuGet/Home/issues/3294)</span><span class="sxs-lookup"><span data-stu-id="bb545-146">Add source to detailed logging (consider for 3.5) - [#3294](https://github.com/NuGet/Home/issues/3294)</span></span>

- <span data-ttu-id="bb545-147">Parametr nezadané mezipaměti se nedodržuje v klientovi NuGet verze 3.4 a [#3074](https://github.com/NuGet/Home/issues/3074)</span><span class="sxs-lookup"><span data-stu-id="bb545-147">NoCache parameter not honored in nuget client version 3.4+ - [#3074](https://github.com/NuGet/Home/issues/3074)</span></span>

- <span data-ttu-id="bb545-148">Když se poskytovatel přihlašovacích údajů nepovede načíst v VS, Nerušit NuGet- [#2422](https://github.com/NuGet/Home/issues/2422)</span><span class="sxs-lookup"><span data-stu-id="bb545-148">When a credential provider fails to load in VS, don't break NuGet - [#2422](https://github.com/NuGet/Home/issues/2422)</span></span>

## <a name="features"></a><span data-ttu-id="bb545-149">Funkce</span><span class="sxs-lookup"><span data-stu-id="bb545-149">Features</span></span>

- <span data-ttu-id="bb545-150">Nastavení CI pro spuštění x86- [#3868](https://github.com/NuGet/Home/issues/3868)</span><span class="sxs-lookup"><span data-stu-id="bb545-150">Set up CI to run x86 - [#3868](https://github.com/NuGet/Home/issues/3868)</span></span>

- <span data-ttu-id="bb545-151">Automatické obnovení 3/3: uživatelské rozhraní bez blokování [#3658](https://github.com/NuGet/Home/issues/3658)</span><span class="sxs-lookup"><span data-stu-id="bb545-151">Auto Restore 3/3: non blocking UI - [#3658](https://github.com/NuGet/Home/issues/3658)</span></span>

- <span data-ttu-id="bb545-152">Automatické obnovení 2/3: obnovení na pozadí při jmenování – [#3657](https://github.com/NuGet/Home/issues/3657)</span><span class="sxs-lookup"><span data-stu-id="bb545-152">Auto Restore 2/3: background restore on nomination - [#3657](https://github.com/NuGet/Home/issues/3657)</span></span>

- <span data-ttu-id="bb545-153">Obnovit odkazy projektu tak, aby odpovídaly chování sestavení (rekurze) – [#3615](https://github.com/NuGet/Home/issues/3615)</span><span class="sxs-lookup"><span data-stu-id="bb545-153">Restore project refs to match build behavior (recurse) - [#3615](https://github.com/NuGet/Home/issues/3615)</span></span>

- <span data-ttu-id="bb545-154">Podpora DPL v VS "15"-Minbar- [#3614](https://github.com/NuGet/Home/issues/3614)</span><span class="sxs-lookup"><span data-stu-id="bb545-154">DPL support in VS "15" - minbar - [#3614](https://github.com/NuGet/Home/issues/3614)</span></span>

- <span data-ttu-id="bb545-155">Přesunout soubor nastavení do programových souborů – [#3613](https://github.com/NuGet/Home/issues/3613)</span><span class="sxs-lookup"><span data-stu-id="bb545-155">Move settings file to Program Files - [#3613](https://github.com/NuGet/Home/issues/3613)</span></span>

- <span data-ttu-id="bb545-156">Vygenerovaná props a cíle vyžadují podporu pro zapojení do více cílů – [#3496](https://github.com/NuGet/Home/issues/3496)</span><span class="sxs-lookup"><span data-stu-id="bb545-156">Generated restore props and targets need cross-targeting participation support - [#3496](https://github.com/NuGet/Home/issues/3496)</span></span>

- <span data-ttu-id="bb545-157">Podpora obnovení NuGet pro PackageTargetFallback (f. k. a Imports) – [#3494](https://github.com/NuGet/Home/issues/3494)</span><span class="sxs-lookup"><span data-stu-id="bb545-157">NuGet Restore support for PackageTargetFallback (f.k.a Imports) - [#3494](https://github.com/NuGet/Home/issues/3494)</span></span>

- <span data-ttu-id="bb545-158">Implementace ToolsRef – [#3472](https://github.com/NuGet/Home/issues/3472)</span><span class="sxs-lookup"><span data-stu-id="bb545-158">ToolsRef implementation - [#3472](https://github.com/NuGet/Home/issues/3472)</span></span>

- <span data-ttu-id="bb545-159">Restore3 pro identifikátor RID- [#3465](https://github.com/NuGet/Home/issues/3465)</span><span class="sxs-lookup"><span data-stu-id="bb545-159">Restore3 for a RID - [#3465](https://github.com/NuGet/Home/issues/3465)</span></span>

- <span data-ttu-id="bb545-160">Uživatelské rozhraní NuGet pro podporu přidání/odebrání/aktualizace PackageRefs- [#3457](https://github.com/NuGet/Home/issues/3457)</span><span class="sxs-lookup"><span data-stu-id="bb545-160">NuGet UI to support Add/Remove/Update of PackageRefs - [#3457](https://github.com/NuGet/Home/issues/3457)</span></span>

- <span data-ttu-id="bb545-161">Automatické obnovení 1/3: implementaci rozhraní API prostřednictvím ukládání informací o obnovení projektu do mezipaměti – [#3456](https://github.com/NuGet/Home/issues/3456)</span><span class="sxs-lookup"><span data-stu-id="bb545-161">Auto Restore 1/3: Implemenation of Nomination API via Caching Project Restore Info - [#3456](https://github.com/NuGet/Home/issues/3456)</span></span>

- <span data-ttu-id="bb545-162">[0] úloha obnovení NuGet & cíle – [#2994](https://github.com/NuGet/Home/issues/2994)</span><span class="sxs-lookup"><span data-stu-id="bb545-162">[0] NuGet Restore Task & Targets - [#2994](https://github.com/NuGet/Home/issues/2994)</span></span>

- <span data-ttu-id="bb545-163">[1] povolit obnovení na úrovni řešení v MSBuildu – [#2993](https://github.com/NuGet/Home/issues/2993)</span><span class="sxs-lookup"><span data-stu-id="bb545-163">[1] Enable Solution level restore in MSBuild - [#2993](https://github.com/NuGet/Home/issues/2993)</span></span>

- <span data-ttu-id="bb545-164">Podpora veřejné rozšiřitelnosti poskytovatele přihlašovacích údajů v aplikaci Visual Studio – [#2909](https://github.com/NuGet/Home/issues/2909)</span><span class="sxs-lookup"><span data-stu-id="bb545-164">Support credential provider public extensibility in Visual Studio - [#2909](https://github.com/NuGet/Home/issues/2909)</span></span>

- <span data-ttu-id="bb545-165">Rekurzivní obnovení NuGet – [#2533](https://github.com/NuGet/Home/issues/2533)</span><span class="sxs-lookup"><span data-stu-id="bb545-165">Recursive nuget restore - [#2533](https://github.com/NuGet/Home/issues/2533)</span></span>

- <span data-ttu-id="bb545-166">Nelze načíst Microsoft. TeamFoundation. Client na dev15, je třeba aktualizovat Microsoft. TeamFoundation. Client verze na 15,0 pro VS "15" Preview- [#2392](https://github.com/NuGet/Home/issues/2392)</span><span class="sxs-lookup"><span data-stu-id="bb545-166">Can't load Microsoft.TeamFoundation.Client on dev15, need to update Microsoft.TeamFoundation.Client version to 15.0 for VS "15" Preview - [#2392](https://github.com/NuGet/Home/issues/2392)</span></span>

- <span data-ttu-id="bb545-167">Nejde nainstalovat balíček C++ do projektu UWP pro platformu C++ ve verzi VS "15" Preview – [#2369](https://github.com/NuGet/Home/issues/2369)</span><span class="sxs-lookup"><span data-stu-id="bb545-167">Unable to install C++ package to C++ UWP project in VS "15" Preview - [#2369](https://github.com/NuGet/Home/issues/2369)</span></span>

- <span data-ttu-id="bb545-168">Nupkg musí podporovat \buildCrossTargeting\ složku a importovat `.targets`  /  `.props` pro obor "crosstargeting" MSBuild.</span><span class="sxs-lookup"><span data-stu-id="bb545-168">Nupkg needs to support \buildCrossTargeting\ folder - and import `.targets` / `.props` for "crosstargeting" MSBuild scope.</span></span><span data-ttu-id="bb545-169"> - [#3499](https://github.com/NuGet/Home/issues/3499)</span><span class="sxs-lookup"><span data-stu-id="bb545-169"> - [#3499](https://github.com/NuGet/Home/issues/3499)</span></span>

- <span data-ttu-id="bb545-170">Návrh ToolsReference – [#3462](https://github.com/NuGet/Home/issues/3462)</span><span class="sxs-lookup"><span data-stu-id="bb545-170">ToolsReference Design - [#3462](https://github.com/NuGet/Home/issues/3462)</span></span>

- <span data-ttu-id="bb545-171">Opravte uživatelské rozhraní NuGet pro podporu obnovení s PackageReferences v `.csproj`  -  [#3455](https://github.com/NuGet/Home/issues/3455)</span><span class="sxs-lookup"><span data-stu-id="bb545-171">Fix NuGet UI to support restore w/ PackageReferences in `.csproj` - [#3455](https://github.com/NuGet/Home/issues/3455)</span></span>

- <span data-ttu-id="bb545-172">Přidání tlačítka Vymazat mezipaměť do nastavení správce balíčků VS – [#3289](https://github.com/NuGet/Home/issues/3289)</span><span class="sxs-lookup"><span data-stu-id="bb545-172">Adding clear cache button to VS package manager settings - [#3289](https://github.com/NuGet/Home/issues/3289)</span></span>

## <a name="dcrs"></a><span data-ttu-id="bb545-173">Chcete odeslat obecnou</span><span class="sxs-lookup"><span data-stu-id="bb545-173">DCRs</span></span>

- <span data-ttu-id="bb545-174">Při automatickém obnovení by mělo být zablokováno obnovení řešení.</span><span class="sxs-lookup"><span data-stu-id="bb545-174">Solution Restore should be blocked while auto restore is happening.</span></span><span data-ttu-id="bb545-175"> - [#3797](https://github.com/NuGet/Home/issues/3797)</span><span class="sxs-lookup"><span data-stu-id="bb545-175"> - [#3797](https://github.com/NuGet/Home/issues/3797)</span></span>

- <span data-ttu-id="bb545-176">NetCore instalovat z uživatelského rozhraní Správce balíčků NuGet se nainstalují do všech TFM a místo těch, které balíček podporuje – [#3721](https://github.com/NuGet/Home/issues/3721)</span><span class="sxs-lookup"><span data-stu-id="bb545-176">NetCore install from NuGet Package Manager UI installs to every TFM , instead of ones that the package supports - [#3721](https://github.com/NuGet/Home/issues/3721)</span></span>

- <span data-ttu-id="bb545-177">Rozhraní API pro restoreer musí podporovat i DotNetCliToolsReferences.</span><span class="sxs-lookup"><span data-stu-id="bb545-177">Restore nominator API needs to support DotNetCliToolsReferences too.</span></span><span data-ttu-id="bb545-178"> - [#3702](https://github.com/NuGet/Home/issues/3702)</span><span class="sxs-lookup"><span data-stu-id="bb545-178"> - [#3702](https://github.com/NuGet/Home/issues/3702)</span></span>

- <span data-ttu-id="bb545-179">Označení našeho souboru VSIX VS "15" jako SystemComponent- [#3700](https://github.com/NuGet/Home/issues/3700)</span><span class="sxs-lookup"><span data-stu-id="bb545-179">Mark our VS "15" vsix as a systemcomponent - [#3700](https://github.com/NuGet/Home/issues/3700)</span></span>

- <span data-ttu-id="bb545-180">Migrujte z referenčního MS. Infrastruktura. Services. Client do MS. Infrastruktura. Services. Client. Interactive – [#3670](https://github.com/NuGet/Home/issues/3670)</span><span class="sxs-lookup"><span data-stu-id="bb545-180">Migrate from referencing MS.VS.Services.Client to MS.VS.Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)</span></span>

- <span data-ttu-id="bb545-181">$ (RestoreLegacyPackagesDirectory) by se mělo dodržovat na úrovni projektu obnovením- [#3618](https://github.com/NuGet/Home/issues/3618)</span><span class="sxs-lookup"><span data-stu-id="bb545-181">$(RestoreLegacyPackagesDirectory) should be respected at a project level by restore - [#3618](https://github.com/NuGet/Home/issues/3618)</span></span>

- <span data-ttu-id="bb545-182">Obnovení do projektu s jednou TargetFramework nesmí být podmínkou- [#3588](https://github.com/NuGet/Home/issues/3588)</span><span class="sxs-lookup"><span data-stu-id="bb545-182">Restore to project with single TargetFramework must not condition props - [#3588](https://github.com/NuGet/Home/issues/3588)</span></span>

- <span data-ttu-id="bb545-183">dotnet</span><span class="sxs-lookup"><span data-stu-id="bb545-183">dotnet</span></span>
  - <span data-ttu-id="bb545-184">dotnetcore restore3 foo. csproj by měl splňovat závislosti projectref a obnovit je.</span><span class="sxs-lookup"><span data-stu-id="bb545-184">dotnetcore restore3 foo.csproj should follow projectref dependencies, and restore those too.</span></span> <span data-ttu-id="bb545-185">Podobně jako sestavení.</span><span class="sxs-lookup"><span data-stu-id="bb545-185">Like build.</span></span><span data-ttu-id="bb545-186"> - [#3577](https://github.com/NuGet/Home/issues/3577)</span><span class="sxs-lookup"><span data-stu-id="bb545-186"> - [#3577](https://github.com/NuGet/Home/issues/3577)</span></span>

- <span data-ttu-id="bb545-187">"typ": závislosti na platformě reprezentované jako "typ": "balíček" v souboru zámku – [#2695](https://github.com/NuGet/Home/issues/2695)</span><span class="sxs-lookup"><span data-stu-id="bb545-187">"type": "platform" Dependencies represented as "type":"package" in lock file - [#2695](https://github.com/NuGet/Home/issues/2695)</span></span>

- <span data-ttu-id="bb545-188">nuget.exe režimu podrobného zobrazení by se měla zobrazit adresa URL pro stažení – [#2629](https://github.com/NuGet/Home/issues/2629)</span><span class="sxs-lookup"><span data-stu-id="bb545-188">nuget.exe Verbose mode should show the download url - [#2629](https://github.com/NuGet/Home/issues/2629)</span></span>

- <span data-ttu-id="bb545-189">Přesunout NuGet xplat do Microsoft. NetCore. app a netcoreapp 1.0- [#2483](https://github.com/NuGet/Home/issues/2483)</span><span class="sxs-lookup"><span data-stu-id="bb545-189">Move NuGet xplat to Microsoft.NetCore.App and netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)</span></span>

- <span data-ttu-id="bb545-190">Push – při vkládání z příkazového řádku by mělo být možné přepsat server symbolů. [#2348](https://github.com/NuGet/Home/issues/2348)</span><span class="sxs-lookup"><span data-stu-id="bb545-190">Push - It should be possible to override the symbol server when pushing from the command line - [#2348](https://github.com/NuGet/Home/issues/2348)</span></span>

- <span data-ttu-id="bb545-191">Konsolidovat kód pro hledání cesty globálních balíčků – [#2296](https://github.com/NuGet/Home/issues/2296)</span><span class="sxs-lookup"><span data-stu-id="bb545-191">Consolidate code for finding the global packages path - [#2296](https://github.com/NuGet/Home/issues/2296)</span></span>

- <span data-ttu-id="bb545-192">Je potřeba lepší název než suppressParent- [#2196](https://github.com/NuGet/Home/issues/2196)</span><span class="sxs-lookup"><span data-stu-id="bb545-192">Need a better name than suppressParent - [#2196](https://github.com/NuGet/Home/issues/2196)</span></span>

- <span data-ttu-id="bb545-193">Určení `project.json` názvu závislosti, který se má použít pro projekty MSBuild – [#1914](https://github.com/NuGet/Home/issues/1914)</span><span class="sxs-lookup"><span data-stu-id="bb545-193">Determine `project.json` dependency name to use for MSBuild projects - [#1914](https://github.com/NuGet/Home/issues/1914)</span></span>

- <span data-ttu-id="bb545-194">Přidejte podporu 2.0.0 SemVer do NuGet. Core- [#3383](https://github.com/NuGet/Home/issues/3383)</span><span class="sxs-lookup"><span data-stu-id="bb545-194">Add SemVer 2.0.0 support to NuGet.Core - [#3383](https://github.com/NuGet/Home/issues/3383)</span></span>

- <span data-ttu-id="bb545-195">Povolení dostupnosti přenosných závislostí NuPkgs s nástrojem `.targets` v MSBuild- [#3342](https://github.com/NuGet/Home/issues/3342)</span><span class="sxs-lookup"><span data-stu-id="bb545-195">Allow transitive dependency NuPkgs with `.targets` to be available in MSBuild - [#3342](https://github.com/NuGet/Home/issues/3342)</span></span>

- <span data-ttu-id="bb545-196">Obnovení NuGet z příkazového řádku je výrazně pomalejší než v sadě VS- [#3330](https://github.com/NuGet/Home/issues/3330)</span><span class="sxs-lookup"><span data-stu-id="bb545-196">NuGet restore from the commandline is significantly slower than VS - [#3330](https://github.com/NuGet/Home/issues/3330)</span></span>

- <span data-ttu-id="bb545-197">Vyměnit ID a rozlišování velikosti písmen a rozlišovat velká a malá písmena – [#2522](https://github.com/NuGet/Home/issues/2522)</span><span class="sxs-lookup"><span data-stu-id="bb545-197">Make package ID and version comparison case insensitive - [#2522](https://github.com/NuGet/Home/issues/2522)</span></span>

- <span data-ttu-id="bb545-198">Možnost ukládání do mezipaměti nefunguje pro `packages.config` obnovení nebo instalaci (GlobalPackagesFolder) – [#1406](https://github.com/NuGet/Home/issues/1406)</span><span class="sxs-lookup"><span data-stu-id="bb545-198">NoCache option does not work for `packages.config` based restore/install (GlobalPackagesFolder) - [#1406](https://github.com/NuGet/Home/issues/1406)</span></span>

- <span data-ttu-id="bb545-199">Prostředky FindPackageByIdResource musí mít výchozí kontext mezipaměti a protokolovací nástroj- [#1357](https://github.com/NuGet/Home/issues/1357)</span><span class="sxs-lookup"><span data-stu-id="bb545-199">FindPackageByIdResource resources needs a default cache context and logger - [#1357](https://github.com/NuGet/Home/issues/1357)</span></span>
