---
title: "Poznámky k verzi RC NuGet 4.0 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/17/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: fa64825d-5908-4abe-9792-d70766d6e2ff
description: "Poznámky k verzi pro NuGet 4.0 RC včetně známé problémy, opravy chyb, přidaných funkcí a chcete."
keywords: "NuGet 4.0 k vydání verze RC, opravy chyb známé problémy, přidat funkce, chcete"
ms.reviewer: kraigb
ms.openlocfilehash: aa1c43be7ac0640bb5e118a162616acb36d44a83
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="40-rc-release-notes"></a><span data-ttu-id="9ba3a-104">4.0 poznámky k verzi RC</span><span class="sxs-lookup"><span data-stu-id="9ba3a-104">4.0 RC Release Notes</span></span>

[<span data-ttu-id="9ba3a-105">Poznámky k verzi 3.5 RTM NuGet</span><span class="sxs-lookup"><span data-stu-id="9ba3a-105">NuGet 3.5 RTM Release Notes</span></span>](../release-notes/nuget-3.5-RTM.md)

<span data-ttu-id="9ba3a-106">[RC 4.0 NuGet pro Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) se zaměřuje na přidání podpory pro scénáře .NET Core, připomínkami klíče zákazníků a zlepšení výkonu v řadě scénářů.</span><span class="sxs-lookup"><span data-stu-id="9ba3a-106">[NuGet 4.0 RC for Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) is focused on adding support for .NET Core scenarios, addressing key customer feedback and improving performance in a variety of scenarios.</span></span> <span data-ttu-id="9ba3a-107">Tato verze přináší několik vylepšení, jako je podpora pro PackageReference, NuGet příkazy jako cíle MSBuild, obnovení balíčků pozadí a další.</span><span class="sxs-lookup"><span data-stu-id="9ba3a-107">This release brings several improvements like support for PackageReference, NuGet commands as MSBuild targets, background package restore, and more.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="9ba3a-108">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="9ba3a-108">Bug Fixes</span></span>

* <span data-ttu-id="9ba3a-109">Chování změny v `dotnet pack --version-suffix foo`  -  [#3838](https://github.com/NuGet/Home/issues/3838)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-109">Behavioral changes in `dotnet pack --version-suffix foo` - [#3838](https://github.com/NuGet/Home/issues/3838)</span></span>

* <span data-ttu-id="9ba3a-110">obnovení nuget.exe vs "15" počítač selže - [#3834](https://github.com/NuGet/Home/issues/3834)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-110">nuget.exe restore on vs "15" machine only fails - [#3834](https://github.com/NuGet/Home/issues/3834)</span></span>

* <span data-ttu-id="9ba3a-111">. Nový projekt NETCore soubor by měl blokovat sestavení během obnovení - [#3780](https://github.com/NuGet/Home/issues/3780)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-111">.NETCore file new project should block the build during restore - [#3780](https://github.com/NuGet/Home/issues/3780)</span></span>

* <span data-ttu-id="9ba3a-112">Webové aplikace ASP.NET Core migrovaná z VS2015 VS "15", nelze obnovit.</span><span class="sxs-lookup"><span data-stu-id="9ba3a-112">ASP.NET Core web app, migrated from VS2015 to VS "15", unable to restore.</span></span><span data-ttu-id="9ba3a-113"> - [#3773](https://github.com/NuGet/Home/issues/3773)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-113"> - [#3773](https://github.com/NuGet/Home/issues/3773)</span></span>

* <span data-ttu-id="9ba3a-114">[Chyba testu] Balíček 'jQuery ověření, nelze je odinstalovat pomocí uživatelského rozhraní PM - [#3755](https://github.com/NuGet/Home/issues/3755)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-114">[Test Failure]Package ‘jQuery Validation’ can’t be uninstalled by PM UI - [#3755](https://github.com/NuGet/Home/issues/3755)</span></span>

* <span data-ttu-id="9ba3a-115">Při instalaci balíčku do UWP `project.json`, projekty nadřazené by měl být obnovena - [#3731](https://github.com/NuGet/Home/issues/3731)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-115">When a package is installed to UWP `project.json`, parent projects should also be restored - [#3731](https://github.com/NuGet/Home/issues/3731)</span></span>

* <span data-ttu-id="9ba3a-116">Úprava cíle NuGet do protokolu zdroje balíčku jako vysoké podrobností místo normální – [#3719](https://github.com/NuGet/Home/issues/3719)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-116">Modify the NuGet targets to log the package sources as High verbosity instead of Normal - [#3719](https://github.com/NuGet/Home/issues/3719)</span></span>

* <span data-ttu-id="9ba3a-117">DotNet pack3 by měla obsahovat dokumentace XML ve výchozím nastavení - [#3698](https://github.com/NuGet/Home/issues/3698)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-117">dotnet pack3 should include XML documentation by default - [#3698](https://github.com/NuGet/Home/issues/3698)</span></span>

* <span data-ttu-id="9ba3a-118">Dávková aktualizace selže z uživatelského rozhraní, když je první zdroj bez balíček a všechny zdroj vybraný - [#3696](https://github.com/NuGet/Home/issues/3696)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-118">Batch update fails from UI when source without the package is first and All source is selected - [#3696](https://github.com/NuGet/Home/issues/3696)</span></span>

* <span data-ttu-id="9ba3a-119">Příkaz pack Nuget nezahrnuje všechny soubory - [#3678](https://github.com/NuGet/Home/issues/3678)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-119">Nuget pack command does not include all files - [#3678](https://github.com/NuGet/Home/issues/3678)</span></span>

* <span data-ttu-id="9ba3a-120">Problém OOM - [#3661](https://github.com/NuGet/Home/issues/3661)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-120">OOM issue - [#3661](https://github.com/NuGet/Home/issues/3661)</span></span>

* <span data-ttu-id="9ba3a-121">ProjectFileDependencyGroups část souboru, prostředky měli používat názvy knihoven pro projekty - [#3611](https://github.com/NuGet/Home/issues/3611)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-121">ProjectFileDependencyGroups section of the assets file should use library names for projects - [#3611](https://github.com/NuGet/Home/issues/3611)</span></span>

* <span data-ttu-id="9ba3a-122">"dotnet restore" a recursing adresáře - [#3517](https://github.com/NuGet/Home/issues/3517)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-122">"dotnet restore" and recursing directories - [#3517](https://github.com/NuGet/Home/issues/3517)</span></span>

* <span data-ttu-id="9ba3a-123">Selhání Restore3 jsou protokolovány jako upozornění místo chyby - [#3503](https://github.com/NuGet/Home/issues/3503)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-123">Restore3 failures are logged as warnings instead of errors - [#3503](https://github.com/NuGet/Home/issues/3503)</span></span>

* <span data-ttu-id="9ba3a-124">Problém sady TFS: "[soubor] není možné najít v pracovním prostoru, nebo nemáte oprávnění k přístupu"- [#2805](https://github.com/NuGet/Home/issues/2805)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-124">TFS issue: "[file]not be found in your workspace, or you do not have permission to access it" - [#2805](https://github.com/NuGet/Home/issues/2805)</span></span>

* <span data-ttu-id="9ba3a-125">Zadejte "nuget <packagename>" v sadě vs quicklaunch vyhledávacího pole udržuje předponu "nuget" - [#2719](https://github.com/NuGet/Home/issues/2719)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-125">Typing "nuget <packagename>" in vs quicklaunch search box keeps "nuget " prefix - [#2719](https://github.com/NuGet/Home/issues/2719)</span></span>

* <span data-ttu-id="9ba3a-126">System.Xml.XmlException: Nerozpoznaný kořenový element v části základní vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="9ba3a-126">System.Xml.XmlException: Unrecognized root element in Core Properties part.</span></span> <span data-ttu-id="9ba3a-127">Řádek 2, pozice 2.</span><span class="sxs-lookup"><span data-stu-id="9ba3a-127">Line 2, position 2.</span></span><span data-ttu-id="9ba3a-128"> - [#2718](https://github.com/NuGet/Home/issues/2718)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-128"> - [#2718](https://github.com/NuGet/Home/issues/2718)</span></span>

* <span data-ttu-id="9ba3a-129">`.nuspec`s uvozený &lt; nebo &gt; v textové pole už sestavení - [#2651](https://github.com/NuGet/Home/issues/2651)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-129">`.nuspec` with escaped &lt; or &gt; in text fields no longer builds - [#2651](https://github.com/NuGet/Home/issues/2651)</span></span>

* <span data-ttu-id="9ba3a-130">odstranění nuget.exe nebude vyzvat k zadání pověření (je v interaktivním režimu) - [#2626](https://github.com/NuGet/Home/issues/2626)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-130">nuget.exe delete won't prompt for credentials (it's in non-interactive mode) - [#2626](https://github.com/NuGet/Home/issues/2626)</span></span>

* <span data-ttu-id="9ba3a-131">odstranění nuget.exe upozorňuje klíč rozhraní API pro místní zdroje, i když nemá smysl - [#2625](https://github.com/NuGet/Home/issues/2625)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-131">nuget.exe delete warns about API Key for local sources, even though it makes no sense - [#2625](https://github.com/NuGet/Home/issues/2625)</span></span>

* <span data-ttu-id="9ba3a-132">Chyba prostředí nízká při instalaci balíčku EF - pre - [#2566](https://github.com/NuGet/Home/issues/2566)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-132">Error experience poor when installing EF -pre package - [#2566](https://github.com/NuGet/Home/issues/2566)</span></span>

* <span data-ttu-id="9ba3a-133">Visual Studio došlo k chybě, pokus po změně výběr v Správce balíčků - [#2551](https://github.com/NuGet/Home/issues/2551)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-133">Visual Studio crashed attempting after changing selection in Package Manager - [#2551](https://github.com/NuGet/Home/issues/2551)</span></span>

* <span data-ttu-id="9ba3a-134">Obnovení DotNet. Pokud jsou použity plovoucí verze - provede velká a malá písmena Id vyhledávání v dvojrozměrném seznamu místní úložiště [#2516](https://github.com/NuGet/Home/issues/2516)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-134">Dotnet restore performs case sensitive Id lookups on flat-list local repositories when floating versions are used - [#2516](https://github.com/NuGet/Home/issues/2516)</span></span>

* <span data-ttu-id="9ba3a-135">odstranění nuget.exe je porušený pro informační kanál V2 - [#2509](https://github.com/NuGet/Home/issues/2509)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-135">nuget.exe delete is broken for V2 feed - [#2509](https://github.com/NuGet/Home/issues/2509)</span></span>

* <span data-ttu-id="9ba3a-136">časový limit nabízené nuget.exe musí lepší chybová zpráva - [#2503](https://github.com/NuGet/Home/issues/2503)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-136">nuget.exe push timeout needs a better error message - [#2503](https://github.com/NuGet/Home/issues/2503)</span></span>

* <span data-ttu-id="9ba3a-137">Nástroj obnovení bez správné importuje bez upozornění selže.</span><span class="sxs-lookup"><span data-stu-id="9ba3a-137">Tool restore without proper imports silently fails.</span></span><span data-ttu-id="9ba3a-138"> - [#2462](https://github.com/NuGet/Home/issues/2462)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-138"> - [#2462](https://github.com/NuGet/Home/issues/2462)</span></span>

* <span data-ttu-id="9ba3a-139">NuGet vás vyzve k zadání přihlašovacích údajů, když je privátní informačního kanálu i v případě, že instalace z nuget.org - [#2346](https://github.com/NuGet/Home/issues/2346)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-139">NuGet prompts to enter credentials when there is a private feed even when installing from nuget.org - [#2346](https://github.com/NuGet/Home/issues/2346)</span></span>

* <span data-ttu-id="9ba3a-140">Balíček ApplicationInsights 2.0, je uvedena, ale ještě - neexistuje [#2317](https://github.com/NuGet/Home/issues/2317)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-140">ApplicationInsights 2.0 package is listed but doesn't exist yet - [#2317](https://github.com/NuGet/Home/issues/2317)</span></span>

* <span data-ttu-id="9ba3a-141">UIDelay v sadě VS "15" preview 5 větve - [#3500](https://github.com/NuGet/Home/issues/3500)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-141">UIDelay in VS "15" preview 5 branch - [#3500](https://github.com/NuGet/Home/issues/3500)</span></span>

* <span data-ttu-id="9ba3a-142">První událost OnBuild je provedena obnovení během vytváření sestavení pro UPW - [#3489](https://github.com/NuGet/Home/issues/3489)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-142">First OnBuild event is missed for Restore during Build for UWP - [#3489](https://github.com/NuGet/Home/issues/3489)</span></span>

* <span data-ttu-id="9ba3a-143">Zalomení PowerShell5 EntityFramework nainstalovat?</span><span class="sxs-lookup"><span data-stu-id="9ba3a-143">PowerShell5 breaks EntityFramework install?</span></span><span data-ttu-id="9ba3a-144"> - [#3312](https://github.com/NuGet/Home/issues/3312)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-144"> - [#3312](https://github.com/NuGet/Home/issues/3312)</span></span>

* <span data-ttu-id="9ba3a-145">Přidání zdroje podrobné protokolování (zvažte pro 3.5) - [#3294](https://github.com/NuGet/Home/issues/3294)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-145">Add source to detailed logging (consider for 3.5) - [#3294](https://github.com/NuGet/Home/issues/3294)</span></span>

* <span data-ttu-id="9ba3a-146">Parametr NoCache není dodržení ve verzi klienta nuget 3.4 + - [#3074](https://github.com/NuGet/Home/issues/3074)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-146">NoCache parameter not honored in nuget client version 3.4+ - [#3074](https://github.com/NuGet/Home/issues/3074)</span></span>

* <span data-ttu-id="9ba3a-147">Pokud poskytovatel pověření se nepodaří načíst v sadě VS, nemusíte rozdělit NuGet - [#2422](https://github.com/NuGet/Home/issues/2422)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-147">When a credential provider fails to load in VS, don't break NuGet - [#2422](https://github.com/NuGet/Home/issues/2422)</span></span>


## <a name="features"></a><span data-ttu-id="9ba3a-148">Funkce</span><span class="sxs-lookup"><span data-stu-id="9ba3a-148">Features</span></span>

* <span data-ttu-id="9ba3a-149">Nastavení spuštění x86-CI [#3868](https://github.com/NuGet/Home/issues/3868)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-149">Set up CI to run x86 - [#3868](https://github.com/NuGet/Home/issues/3868)</span></span>

* <span data-ttu-id="9ba3a-150">Automatické obnovení 3/3: bez blokující uživatelské rozhraní – [#3658](https://github.com/NuGet/Home/issues/3658)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-150">Auto Restore 3/3: non blocking UI - [#3658](https://github.com/NuGet/Home/issues/3658)</span></span>

* <span data-ttu-id="9ba3a-151">Automatické obnovení 2/3: pozadí obnovení navrženém - [#3657](https://github.com/NuGet/Home/issues/3657)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-151">Auto Restore 2/3: background restore on nomination - [#3657](https://github.com/NuGet/Home/issues/3657)</span></span>

* <span data-ttu-id="9ba3a-152">Obnovení projektu odolný systém souborů tak, aby odpovídaly chování sestavení (recurse) - [#3615](https://github.com/NuGet/Home/issues/3615)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-152">Restore project refs to match build behavior (recurse) - [#3615](https://github.com/NuGet/Home/issues/3615)</span></span>

* <span data-ttu-id="9ba3a-153">DPL podporují v sadě VS "15" – minbar - [#3614](https://github.com/NuGet/Home/issues/3614)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-153">DPL support in VS "15" - minbar - [#3614](https://github.com/NuGet/Home/issues/3614)</span></span>

* <span data-ttu-id="9ba3a-154">Přesunout soubor s nastavením pro soubory programu - [#3613](https://github.com/NuGet/Home/issues/3613)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-154">Move settings file to Program Files - [#3613](https://github.com/NuGet/Home/issues/3613)</span></span>

* <span data-ttu-id="9ba3a-155">Vygenerovaný obnovení props a cíle potřebují podporu zapojení cílení na mezi - [#3496](https://github.com/NuGet/Home/issues/3496)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-155">Generated restore props and targets need cross-targeting participation support - [#3496](https://github.com/NuGet/Home/issues/3496)</span></span>

* <span data-ttu-id="9ba3a-156">Obnovení NuGet podpora PackageTargetFallback (f.k.a importy) - [#3494](https://github.com/NuGet/Home/issues/3494)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-156">NuGet Restore support for PackageTargetFallback (f.k.a Imports) - [#3494](https://github.com/NuGet/Home/issues/3494)</span></span>

* <span data-ttu-id="9ba3a-157">Implementace ToolsRef - [#3472](https://github.com/NuGet/Home/issues/3472)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-157">ToolsRef implementation - [#3472](https://github.com/NuGet/Home/issues/3472)</span></span>

* <span data-ttu-id="9ba3a-158">Restore3 pro identifikátor RID - [#3465](https://github.com/NuGet/Home/issues/3465)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-158">Restore3 for a RID - [#3465](https://github.com/NuGet/Home/issues/3465)</span></span>

* <span data-ttu-id="9ba3a-159">NuGet uživatelského rozhraní pro podporu přidat nebo odebrat nebo aktualizace PackageRefs - [#3457](https://github.com/NuGet/Home/issues/3457)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-159">NuGet UI to support Add/Remove/Update of PackageRefs - [#3457](https://github.com/NuGet/Home/issues/3457)</span></span>

* <span data-ttu-id="9ba3a-160">Automatické obnovení 1/3: Implementace navrženém rozhraní API prostřednictvím ukládání do mezipaměti projektu obnovit informace o - [#3456](https://github.com/NuGet/Home/issues/3456)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-160">Auto Restore 1/3: Implemenation of Nomination API via Caching Project Restore Info - [#3456](https://github.com/NuGet/Home/issues/3456)</span></span>

* <span data-ttu-id="9ba3a-161">Obnovení [0] NuGet úloh & cíle - [#2994](https://github.com/NuGet/Home/issues/2994)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-161">[0] NuGet Restore Task & Targets - [#2994](https://github.com/NuGet/Home/issues/2994)</span></span>

* <span data-ttu-id="9ba3a-162">[1] povolit řešení obnovení na úrovni v nástroji MSBuild - [#2993](https://github.com/NuGet/Home/issues/2993)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-162">[1] Enable Solution level restore in MSBuild - [#2993](https://github.com/NuGet/Home/issues/2993)</span></span>

* <span data-ttu-id="9ba3a-163">Podporu rozšiřitelnosti veřejného poskytovatele přihlašovacích údajů v sadě Visual Studio – [#2909](https://github.com/NuGet/Home/issues/2909)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-163">Support credential provider public extensibility in Visual Studio - [#2909](https://github.com/NuGet/Home/issues/2909)</span></span>

* <span data-ttu-id="9ba3a-164">Rekurzivní nuget restore - [#2533](https://github.com/NuGet/Home/issues/2533)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-164">Recursive nuget restore - [#2533](https://github.com/NuGet/Home/issues/2533)</span></span>

* <span data-ttu-id="9ba3a-165">Nelze načíst Microsoft.TeamFoundation.Client na dev15, nutné aktualizovat verzi Microsoft.TeamFoundation.Client 15.0 pro VS "15" Preview – [#2392](https://github.com/NuGet/Home/issues/2392)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-165">Can't load Microsoft.TeamFoundation.Client on dev15, need to update Microsoft.TeamFoundation.Client version to 15.0 for VS "15" Preview - [#2392](https://github.com/NuGet/Home/issues/2392)</span></span>

* <span data-ttu-id="9ba3a-166">Nelze nainstalovat balíček C++ do C++ UWP projektu v sadě VS "15" Preview – [#2369](https://github.com/NuGet/Home/issues/2369)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-166">Unable to install C++ package to C++ UWP project in VS "15" Preview - [#2369](https://github.com/NuGet/Home/issues/2369)</span></span>

* <span data-ttu-id="9ba3a-167">Nupkg musí podporovat \buildCrossTargeting\ složky - a importovat `.targets`  /  `.props` pro "crosstargeting" MSBuild oboru.</span><span class="sxs-lookup"><span data-stu-id="9ba3a-167">Nupkg needs to support \buildCrossTargeting\ folder - and import `.targets` / `.props` for "crosstargeting" MSBuild scope.</span></span><span data-ttu-id="9ba3a-168"> - [#3499](https://github.com/NuGet/Home/issues/3499)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-168"> - [#3499](https://github.com/NuGet/Home/issues/3499)</span></span>

* <span data-ttu-id="9ba3a-169">Návrh ToolsReference - [#3462](https://github.com/NuGet/Home/issues/3462)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-169">ToolsReference Design - [#3462](https://github.com/NuGet/Home/issues/3462)</span></span>

* <span data-ttu-id="9ba3a-170">Opravte NuGet uživatelského rozhraní pro podporu obnovení s PackageReferences v `.csproj`  -  [#3455](https://github.com/NuGet/Home/issues/3455)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-170">Fix NuGet UI to support restore w/ PackageReferences in `.csproj` - [#3455](https://github.com/NuGet/Home/issues/3455)</span></span>

* <span data-ttu-id="9ba3a-171">Přidání tlačítko Vymazat mezipaměť nastavení správce balíčku VS - [#3289](https://github.com/NuGet/Home/issues/3289)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-171">Adding clear cache button to VS package manager settings - [#3289](https://github.com/NuGet/Home/issues/3289)</span></span>

## <a name="dcrs"></a><span data-ttu-id="9ba3a-172">Chcete</span><span class="sxs-lookup"><span data-stu-id="9ba3a-172">DCRs</span></span>

* <span data-ttu-id="9ba3a-173">Řešení obnovení by se zablokovat, zatímco se děje automatického obnovení.</span><span class="sxs-lookup"><span data-stu-id="9ba3a-173">Solution Restore should be blocked while auto restore is happening.</span></span><span data-ttu-id="9ba3a-174"> - [#3797](https://github.com/NuGet/Home/issues/3797)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-174"> - [#3797](https://github.com/NuGet/Home/issues/3797)</span></span>

* <span data-ttu-id="9ba3a-175">Při instalaci NetCore z uživatelského rozhraní Správce balíčků NuGet nainstaluje do každé TFM místo ta, která podporuje balíček - [#3721](https://github.com/NuGet/Home/issues/3721)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-175">NetCore install from NuGet Package Manager UI installs to every TFM , instead of ones that the package supports - [#3721](https://github.com/NuGet/Home/issues/3721)</span></span>

* <span data-ttu-id="9ba3a-176">Obnovte nominator musí podporovat DotNetCliToolsReferences příliš rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="9ba3a-176">Restore nominator API needs to support DotNetCliToolsReferences too.</span></span><span data-ttu-id="9ba3a-177"> - [#3702](https://github.com/NuGet/Home/issues/3702)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-177"> - [#3702](https://github.com/NuGet/Home/issues/3702)</span></span>

* <span data-ttu-id="9ba3a-178">Označit naše VS "15" vsix jako systemcomponent - [#3700](https://github.com/NuGet/Home/issues/3700)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-178">Mark our VS "15" vsix as a systemcomponent - [#3700](https://github.com/NuGet/Home/issues/3700)</span></span>

* <span data-ttu-id="9ba3a-179">Migrujte z odkazující na MS. VS. Services.Client k MS. VS. Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-179">Migrate from referencing MS.VS.Services.Client to MS.VS.Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)</span></span>

* <span data-ttu-id="9ba3a-180">$(RestoreLegacyPackagesDirectory) respektuje na úrovni projektu obnovením - [#3618](https://github.com/NuGet/Home/issues/3618)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-180">$(RestoreLegacyPackagesDirectory) should be respected at a project level by restore - [#3618](https://github.com/NuGet/Home/issues/3618)</span></span>

* <span data-ttu-id="9ba3a-181">Obnovení do projektu s jeden TargetFramework nesmí podmínky props - [#3588](https://github.com/NuGet/Home/issues/3588)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-181">Restore to project with single TargetFramework must not condition props - [#3588](https://github.com/NuGet/Home/issues/3588)</span></span>

* <span data-ttu-id="9ba3a-182">DotNet restore3 foo.csproj by měl postupujte podle projectref závislosti a ty příliš obnovit.</span><span class="sxs-lookup"><span data-stu-id="9ba3a-182">dotnet restore3 foo.csproj should follow projectref dependencies, and restore those too.</span></span> <span data-ttu-id="9ba3a-183">Jako sestavení.</span><span class="sxs-lookup"><span data-stu-id="9ba3a-183">Like build.</span></span><span data-ttu-id="9ba3a-184"> - [#3577](https://github.com/NuGet/Home/issues/3577)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-184"> - [#3577](https://github.com/NuGet/Home/issues/3577)</span></span>

* <span data-ttu-id="9ba3a-185">"typ": "platformy" závislosti reprezentován jako "typ": "balíček" v souboru zámku - [#2695](https://github.com/NuGet/Home/issues/2695)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-185">"type": "platform" Dependencies represented as "type":"package" in lock file - [#2695](https://github.com/NuGet/Home/issues/2695)</span></span>

* <span data-ttu-id="9ba3a-186">Podrobný režim nuget.exe by měl zobrazit stahování adresy url - [#2629](https://github.com/NuGet/Home/issues/2629)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-186">nuget.exe Verbose mode should show the download url - [#2629](https://github.com/NuGet/Home/issues/2629)</span></span>

* <span data-ttu-id="9ba3a-187">Přesunout NuGet xplat Microsoft.NetCore.App a netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-187">Move NuGet xplat to Microsoft.NetCore.App and netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)</span></span>

* <span data-ttu-id="9ba3a-188">Push – musí být možné přepsat na symbol server při nabízení z příkazového řádku - [#2348](https://github.com/NuGet/Home/issues/2348)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-188">Push - It should be possible to override the symbol server when pushing from the command line - [#2348](https://github.com/NuGet/Home/issues/2348)</span></span>

* <span data-ttu-id="9ba3a-189">Konsolidovat kód pro hledání na globální balíčky cesta - [#2296](https://github.com/NuGet/Home/issues/2296)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-189">Consolidate code for finding the global packages path - [#2296](https://github.com/NuGet/Home/issues/2296)</span></span>

* <span data-ttu-id="9ba3a-190">Třeba lepší název než suppressParent - [#2196](https://github.com/NuGet/Home/issues/2196)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-190">Need a better name than suppressParent - [#2196](https://github.com/NuGet/Home/issues/2196)</span></span>

* <span data-ttu-id="9ba3a-191">Určení `project.json` název závislostí pro projektů MSBuild - [#1914](https://github.com/NuGet/Home/issues/1914)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-191">Determine `project.json` dependency name to use for MSBuild projects - [#1914](https://github.com/NuGet/Home/issues/1914)</span></span>

* <span data-ttu-id="9ba3a-192">Přidání podpory SemVer 2.0.0 do NuGet.Core - [#3383](https://github.com/NuGet/Home/issues/3383)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-192">Add SemVer 2.0.0 support to NuGet.Core - [#3383](https://github.com/NuGet/Home/issues/3383)</span></span>

* <span data-ttu-id="9ba3a-193">Povolit přenositelné závislostí NuPkgs s `.targets` být k dispozici v nástroji MSBuild - [#3342](https://github.com/NuGet/Home/issues/3342)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-193">Allow transitive dependency NuPkgs with `.targets` to be available in MSBuild - [#3342](https://github.com/NuGet/Home/issues/3342)</span></span>

* <span data-ttu-id="9ba3a-194">NuGet restore z příkazovému řádku je podstatně pomalejší než VS - [#3330](https://github.com/NuGet/Home/issues/3330)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-194">NuGet restore from the commandline is significantly slower than VS - [#3330](https://github.com/NuGet/Home/issues/3330)</span></span>

* <span data-ttu-id="9ba3a-195">Provést porovnání ID a verzi balíčku malá a velká písmena - [#2522](https://github.com/NuGet/Home/issues/2522)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-195">Make package ID and version comparison case insensitive - [#2522](https://github.com/NuGet/Home/issues/2522)</span></span>

* <span data-ttu-id="9ba3a-196">NoCache možnost není k dispozici pro `packages.config` obnovení nebo instalace (GlobalPackagesFolder) - [#1406](https://github.com/NuGet/Home/issues/1406)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-196">NoCache option does not work for `packages.config` based restore/install (GlobalPackagesFolder) - [#1406](https://github.com/NuGet/Home/issues/1406)</span></span>

* <span data-ttu-id="9ba3a-197">Prostředky FindPackageByIdResource musí mít výchozí kontext mezipaměti a protokolování - [#1357](https://github.com/NuGet/Home/issues/1357)</span><span class="sxs-lookup"><span data-stu-id="9ba3a-197">FindPackageByIdResource resources needs a default cache context and logger - [#1357](https://github.com/NuGet/Home/issues/1357)</span></span>
