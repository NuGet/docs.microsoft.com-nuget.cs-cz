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
# <a name="nuget-40-rc-release-notes"></a><span data-ttu-id="cf240-103">NuGet 4.0 RC poznámky k verzi</span><span class="sxs-lookup"><span data-stu-id="cf240-103">NuGet 4.0 RC Release Notes</span></span>

[<span data-ttu-id="cf240-104">NuGet 3,5 RTM poznámky k verzi</span><span class="sxs-lookup"><span data-stu-id="cf240-104">NuGet 3.5 RTM Release Notes</span></span>](../release-notes/nuget-3.5-RTM.md)

<span data-ttu-id="cf240-105">[NuGet 4.0 RC pro Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) se zaměřuje na přidání podpory pro scénáře .NET Core, adresování klíčových názorů zákazníků a zlepšení výkonu v různých scénářích.</span><span class="sxs-lookup"><span data-stu-id="cf240-105">[NuGet 4.0 RC for Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) is focused on adding support for .NET Core scenarios, addressing key customer feedback and improving performance in a variety of scenarios.</span></span> <span data-ttu-id="cf240-106">Tato verze přináší několik vylepšení, jako je podpora packagereference, NuGet příkazy jako MSBuild cíle, obnovení balíčku na pozadí a další.</span><span class="sxs-lookup"><span data-stu-id="cf240-106">This release brings several improvements like support for PackageReference, NuGet commands as MSBuild targets, background package restore, and more.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="cf240-107">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="cf240-107">Bug Fixes</span></span>

- <span data-ttu-id="cf240-108">Změny chování `dotnet pack --version-suffix foo`  - v [#3838](https://github.com/NuGet/Home/issues/3838)</span><span class="sxs-lookup"><span data-stu-id="cf240-108">Behavioral changes in `dotnet pack --version-suffix foo` - [#3838](https://github.com/NuGet/Home/issues/3838)</span></span>

- <span data-ttu-id="cf240-109">nuget.exe obnovení na vs "15" stroj pouze selže - [#3834](https://github.com/NuGet/Home/issues/3834)</span><span class="sxs-lookup"><span data-stu-id="cf240-109">nuget.exe restore on vs "15" machine only fails - [#3834](https://github.com/NuGet/Home/issues/3834)</span></span>

- <span data-ttu-id="cf240-110">. NETCore soubor nový projekt by měl blokovat sestavení během obnovení - [#3780](https://github.com/NuGet/Home/issues/3780)</span><span class="sxs-lookup"><span data-stu-id="cf240-110">.NETCore file new project should block the build during restore - [#3780](https://github.com/NuGet/Home/issues/3780)</span></span>

- <span data-ttu-id="cf240-111">ASP.NET Základní webová aplikace, migrovaná z VS2015 na VS "15", nelze obnovit.</span><span class="sxs-lookup"><span data-stu-id="cf240-111">ASP.NET Core web app, migrated from VS2015 to VS "15", unable to restore.</span></span><span data-ttu-id="cf240-112"> - [#3773](https://github.com/NuGet/Home/issues/3773)</span><span class="sxs-lookup"><span data-stu-id="cf240-112"> - [#3773](https://github.com/NuGet/Home/issues/3773)</span></span>

- <span data-ttu-id="cf240-113">[Selhání testu] Balíček "jQuery Validation" nelze odinstalovat pomocí pm ui - [#3755](https://github.com/NuGet/Home/issues/3755)</span><span class="sxs-lookup"><span data-stu-id="cf240-113">[Test Failure]Package ‘jQuery Validation’ can’t be uninstalled by PM UI - [#3755](https://github.com/NuGet/Home/issues/3755)</span></span>

- <span data-ttu-id="cf240-114">Při instalaci balíčku do `project.json`UPW , nadřazené projekty by měly být také obnoveny - [#3731](https://github.com/NuGet/Home/issues/3731)</span><span class="sxs-lookup"><span data-stu-id="cf240-114">When a package is installed to UWP `project.json`, parent projects should also be restored - [#3731](https://github.com/NuGet/Home/issues/3731)</span></span>

- <span data-ttu-id="cf240-115">Upravte Cíle NuGet pro protokolování zdrojů balíčku jako vysoké podrobnosti namísto Normal - [#3719](https://github.com/NuGet/Home/issues/3719)</span><span class="sxs-lookup"><span data-stu-id="cf240-115">Modify the NuGet targets to log the package sources as High verbosity instead of Normal - [#3719](https://github.com/NuGet/Home/issues/3719)</span></span>

- <span data-ttu-id="cf240-116">dotnet</span><span class="sxs-lookup"><span data-stu-id="cf240-116">dotnet</span></span>
  - <span data-ttu-id="cf240-117">dotnetcore pack3 by měl obsahovat dokumentaci XML ve výchozím nastavení - [#3698](https://github.com/NuGet/Home/issues/3698)</span><span class="sxs-lookup"><span data-stu-id="cf240-117">dotnetcore pack3 should include XML documentation by default - [#3698](https://github.com/NuGet/Home/issues/3698)</span></span>

- <span data-ttu-id="cf240-118">Dávková aktualizace se nezdaří z uhlavního pásma, pokud je nejprve zdroj bez balíčku a je vybrán veškerý zdroj - [#3696](https://github.com/NuGet/Home/issues/3696)</span><span class="sxs-lookup"><span data-stu-id="cf240-118">Batch update fails from UI when source without the package is first and All source is selected - [#3696](https://github.com/NuGet/Home/issues/3696)</span></span>

- <span data-ttu-id="cf240-119">Nuget pack příkaz neobsahuje všechny soubory - [#3678](https://github.com/NuGet/Home/issues/3678)</span><span class="sxs-lookup"><span data-stu-id="cf240-119">Nuget pack command does not include all files - [#3678](https://github.com/NuGet/Home/issues/3678)</span></span>

- <span data-ttu-id="cf240-120">OOM problém - [#3661](https://github.com/NuGet/Home/issues/3661)</span><span class="sxs-lookup"><span data-stu-id="cf240-120">OOM issue - [#3661](https://github.com/NuGet/Home/issues/3661)</span></span>

- <span data-ttu-id="cf240-121">Část Souboru datových zdrojů projectFileDependencyGroups by měla používat názvy knihoven pro projekty – [#3611](https://github.com/NuGet/Home/issues/3611)</span><span class="sxs-lookup"><span data-stu-id="cf240-121">ProjectFileDependencyGroups section of the assets file should use library names for projects - [#3611](https://github.com/NuGet/Home/issues/3611)</span></span>

- <span data-ttu-id="cf240-122">"dotnet restore" a opakování adresářů - [#3517](https://github.com/NuGet/Home/issues/3517)</span><span class="sxs-lookup"><span data-stu-id="cf240-122">"dotnet restore" and recursing directories - [#3517](https://github.com/NuGet/Home/issues/3517)</span></span>

- <span data-ttu-id="cf240-123">Obnovení3 chyby jsou zaznamenány jako upozornění namísto chyb - [#3503](https://github.com/NuGet/Home/issues/3503)</span><span class="sxs-lookup"><span data-stu-id="cf240-123">Restore3 failures are logged as warnings instead of errors - [#3503](https://github.com/NuGet/Home/issues/3503)</span></span>

- <span data-ttu-id="cf240-124">Problém tfs: "[soubor] nelze nalézt ve vašem pracovním prostoru, nebo nemáte oprávnění k přístupu k němu" - [#2805](https://github.com/NuGet/Home/issues/2805)</span><span class="sxs-lookup"><span data-stu-id="cf240-124">TFS issue: "[file]not be found in your workspace, or you do not have permission to access it" - [#2805](https://github.com/NuGet/Home/issues/2805)</span></span>

- <span data-ttu-id="cf240-125">Zadáním "nuget" <packagename>vs quicklaunch vyhledávacího pole udržuje "nuget" prefix - [#2719](https://github.com/NuGet/Home/issues/2719)</span><span class="sxs-lookup"><span data-stu-id="cf240-125">Typing "nuget <packagename>" in vs quicklaunch search box keeps "nuget " prefix - [#2719](https://github.com/NuGet/Home/issues/2719)</span></span>

- <span data-ttu-id="cf240-126">System.Xml.XmlException: Nerozpoznaný kořenový prvek v části Vlastnosti jádra.</span><span class="sxs-lookup"><span data-stu-id="cf240-126">System.Xml.XmlException: Unrecognized root element in Core Properties part.</span></span> <span data-ttu-id="cf240-127">Řádek 2, pozice 2.</span><span class="sxs-lookup"><span data-stu-id="cf240-127">Line 2, position 2.</span></span><span data-ttu-id="cf240-128"> - [#2718](https://github.com/NuGet/Home/issues/2718)</span><span class="sxs-lookup"><span data-stu-id="cf240-128"> - [#2718](https://github.com/NuGet/Home/issues/2718)</span></span>

- <span data-ttu-id="cf240-129">`.nuspec`s &lt; uvozeným nebo &gt; v textových polích, která se již nevytváří - [#2651](https://github.com/NuGet/Home/issues/2651)</span><span class="sxs-lookup"><span data-stu-id="cf240-129">`.nuspec` with escaped &lt; or &gt; in text fields no longer builds - [#2651](https://github.com/NuGet/Home/issues/2651)</span></span>

- <span data-ttu-id="cf240-130">nuget.exe delete nevyzve k zadání přihlašovacích údajů (je v neinteraktivním režimu) - [#2626](https://github.com/NuGet/Home/issues/2626)</span><span class="sxs-lookup"><span data-stu-id="cf240-130">nuget.exe delete won't prompt for credentials (it's in non-interactive mode) - [#2626](https://github.com/NuGet/Home/issues/2626)</span></span>

- <span data-ttu-id="cf240-131">nuget.exe delete varuje o klíči API pro místní zdroje, i když to nedává smysl - [#2625](https://github.com/NuGet/Home/issues/2625)</span><span class="sxs-lookup"><span data-stu-id="cf240-131">nuget.exe delete warns about API Key for local sources, even though it makes no sense - [#2625](https://github.com/NuGet/Home/issues/2625)</span></span>

- <span data-ttu-id="cf240-132">Při instalaci balíčku EF -pre [došlo](https://github.com/NuGet/Home/issues/2566) k chybě, #2566</span><span class="sxs-lookup"><span data-stu-id="cf240-132">Error experience poor when installing EF -pre package - [#2566](https://github.com/NuGet/Home/issues/2566)</span></span>

- <span data-ttu-id="cf240-133">Visual Studio došlo k pokusu o změnu výběru ve Správci balíčků - [#2551](https://github.com/NuGet/Home/issues/2551)</span><span class="sxs-lookup"><span data-stu-id="cf240-133">Visual Studio crashed attempting after changing selection in Package Manager - [#2551](https://github.com/NuGet/Home/issues/2551)</span></span>

- <span data-ttu-id="cf240-134">dotnet</span><span class="sxs-lookup"><span data-stu-id="cf240-134">dotnet</span></span>
  - <span data-ttu-id="cf240-135">dotnetcore obnovení provádí vyhledávání ID rozlišování malých a velkých písmen v místních úložištích s plochým seznamem při použití plovoucích verzí - [#2516](https://github.com/NuGet/Home/issues/2516)</span><span class="sxs-lookup"><span data-stu-id="cf240-135">dotnetcore restore performs case sensitive Id lookups on flat-list local repositories when floating versions are used - [#2516](https://github.com/NuGet/Home/issues/2516)</span></span>

- <span data-ttu-id="cf240-136">nuget.exe odstranit je přerušeno pro V2 feed - [#2509](https://github.com/NuGet/Home/issues/2509)</span><span class="sxs-lookup"><span data-stu-id="cf240-136">nuget.exe delete is broken for V2 feed - [#2509](https://github.com/NuGet/Home/issues/2509)</span></span>

- <span data-ttu-id="cf240-137">nuget.exe push timeout potřebuje lepší chybovou zprávu - [#2503](https://github.com/NuGet/Home/issues/2503)</span><span class="sxs-lookup"><span data-stu-id="cf240-137">nuget.exe push timeout needs a better error message - [#2503](https://github.com/NuGet/Home/issues/2503)</span></span>

- <span data-ttu-id="cf240-138">Nástroj obnovení bez řádného importu tiše selže.</span><span class="sxs-lookup"><span data-stu-id="cf240-138">Tool restore without proper imports silently fails.</span></span><span data-ttu-id="cf240-139"> - [#2462](https://github.com/NuGet/Home/issues/2462)</span><span class="sxs-lookup"><span data-stu-id="cf240-139"> - [#2462](https://github.com/NuGet/Home/issues/2462)</span></span>

- <span data-ttu-id="cf240-140">NuGet vyzve k zadání přihlašovacích údajů, pokud je soukromý zdroj i při instalaci z nuget.org - [#2346](https://github.com/NuGet/Home/issues/2346)</span><span class="sxs-lookup"><span data-stu-id="cf240-140">NuGet prompts to enter credentials when there is a private feed even when installing from nuget.org - [#2346](https://github.com/NuGet/Home/issues/2346)</span></span>

- <span data-ttu-id="cf240-141">Balíček ApplicationInsights 2.0 je uveden, ale ještě neexistuje – [#2317](https://github.com/NuGet/Home/issues/2317)</span><span class="sxs-lookup"><span data-stu-id="cf240-141">ApplicationInsights 2.0 package is listed but doesn't exist yet - [#2317](https://github.com/NuGet/Home/issues/2317)</span></span>

- <span data-ttu-id="cf240-142">UIDelay ve VS "15" náhled 5 větev - [#3500](https://github.com/NuGet/Home/issues/3500)</span><span class="sxs-lookup"><span data-stu-id="cf240-142">UIDelay in VS "15" preview 5 branch - [#3500](https://github.com/NuGet/Home/issues/3500)</span></span>

- <span data-ttu-id="cf240-143">První Událost OnBuild chybí pro obnovení během sestavení pro UPW - [#3489](https://github.com/NuGet/Home/issues/3489)</span><span class="sxs-lookup"><span data-stu-id="cf240-143">First OnBuild event is missed for Restore during Build for UWP - [#3489](https://github.com/NuGet/Home/issues/3489)</span></span>

- <span data-ttu-id="cf240-144">PowerShell5 přestávky EntityFramework nainstalovat?</span><span class="sxs-lookup"><span data-stu-id="cf240-144">PowerShell5 breaks EntityFramework install?</span></span><span data-ttu-id="cf240-145"> - [#3312](https://github.com/NuGet/Home/issues/3312)</span><span class="sxs-lookup"><span data-stu-id="cf240-145"> - [#3312](https://github.com/NuGet/Home/issues/3312)</span></span>

- <span data-ttu-id="cf240-146">Přidání zdroje do podrobného protokolování (zvažte pro 3.5) - [#3294](https://github.com/NuGet/Home/issues/3294)</span><span class="sxs-lookup"><span data-stu-id="cf240-146">Add source to detailed logging (consider for 3.5) - [#3294](https://github.com/NuGet/Home/issues/3294)</span></span>

- <span data-ttu-id="cf240-147">Parametr NoCache není dodržen v nugetové klientské verzi 3.4+ - [#3074](https://github.com/NuGet/Home/issues/3074)</span><span class="sxs-lookup"><span data-stu-id="cf240-147">NoCache parameter not honored in nuget client version 3.4+ - [#3074](https://github.com/NuGet/Home/issues/3074)</span></span>

- <span data-ttu-id="cf240-148">Když se zprostředkovatele pověření nepodaří načíst ve VS, nepřerušuj nuget – [#2422](https://github.com/NuGet/Home/issues/2422)</span><span class="sxs-lookup"><span data-stu-id="cf240-148">When a credential provider fails to load in VS, don't break NuGet - [#2422](https://github.com/NuGet/Home/issues/2422)</span></span>

## <a name="features"></a><span data-ttu-id="cf240-149">Funkce</span><span class="sxs-lookup"><span data-stu-id="cf240-149">Features</span></span>

- <span data-ttu-id="cf240-150">Nastavit CI pro spuštění x86 - [#3868](https://github.com/NuGet/Home/issues/3868)</span><span class="sxs-lookup"><span data-stu-id="cf240-150">Set up CI to run x86 - [#3868](https://github.com/NuGet/Home/issues/3868)</span></span>

- <span data-ttu-id="cf240-151">Automatické obnovení 3/3: neblokující uI - [#3658](https://github.com/NuGet/Home/issues/3658)</span><span class="sxs-lookup"><span data-stu-id="cf240-151">Auto Restore 3/3: non blocking UI - [#3658](https://github.com/NuGet/Home/issues/3658)</span></span>

- <span data-ttu-id="cf240-152">Auto Restore 2/3: obnovení pozadí na nominaci - [#3657](https://github.com/NuGet/Home/issues/3657)</span><span class="sxs-lookup"><span data-stu-id="cf240-152">Auto Restore 2/3: background restore on nomination - [#3657](https://github.com/NuGet/Home/issues/3657)</span></span>

- <span data-ttu-id="cf240-153">Obnovit refs projektu tak, aby odpovídaly chování sestavení (recurse) - [#3615](https://github.com/NuGet/Home/issues/3615)</span><span class="sxs-lookup"><span data-stu-id="cf240-153">Restore project refs to match build behavior (recurse) - [#3615](https://github.com/NuGet/Home/issues/3615)</span></span>

- <span data-ttu-id="cf240-154">Podpora DPL ve VS "15" - minbar - [#3614](https://github.com/NuGet/Home/issues/3614)</span><span class="sxs-lookup"><span data-stu-id="cf240-154">DPL support in VS "15" - minbar - [#3614](https://github.com/NuGet/Home/issues/3614)</span></span>

- <span data-ttu-id="cf240-155">Přesunout soubor nastavení do programových souborů - [#3613](https://github.com/NuGet/Home/issues/3613)</span><span class="sxs-lookup"><span data-stu-id="cf240-155">Move settings file to Program Files - [#3613](https://github.com/NuGet/Home/issues/3613)</span></span>

- <span data-ttu-id="cf240-156">Generované rekvizity a cíle obnovení vyžadují podporu účasti napříč cíleními – [#3496](https://github.com/NuGet/Home/issues/3496)</span><span class="sxs-lookup"><span data-stu-id="cf240-156">Generated restore props and targets need cross-targeting participation support - [#3496](https://github.com/NuGet/Home/issues/3496)</span></span>

- <span data-ttu-id="cf240-157">Podpora obnovení NuGet pro PackageTargetFallback (f.k.a Imports) - [#3494](https://github.com/NuGet/Home/issues/3494)</span><span class="sxs-lookup"><span data-stu-id="cf240-157">NuGet Restore support for PackageTargetFallback (f.k.a Imports) - [#3494](https://github.com/NuGet/Home/issues/3494)</span></span>

- <span data-ttu-id="cf240-158">Implementace ToolsRef - [#3472](https://github.com/NuGet/Home/issues/3472)</span><span class="sxs-lookup"><span data-stu-id="cf240-158">ToolsRef implementation - [#3472](https://github.com/NuGet/Home/issues/3472)</span></span>

- <span data-ttu-id="cf240-159">Obnovení3 pro rid - [#3465](https://github.com/NuGet/Home/issues/3465)</span><span class="sxs-lookup"><span data-stu-id="cf240-159">Restore3 for a RID - [#3465](https://github.com/NuGet/Home/issues/3465)</span></span>

- <span data-ttu-id="cf240-160">NuGet ui pro podporu přidat nebo odebrat/aktualizovat PackageRefs - [#3457](https://github.com/NuGet/Home/issues/3457)</span><span class="sxs-lookup"><span data-stu-id="cf240-160">NuGet UI to support Add/Remove/Update of PackageRefs - [#3457](https://github.com/NuGet/Home/issues/3457)</span></span>

- <span data-ttu-id="cf240-161">Automatické obnovení 1/3: Implemenation nominace API přes Caching Projektu Obnovit Info - [#3456](https://github.com/NuGet/Home/issues/3456)</span><span class="sxs-lookup"><span data-stu-id="cf240-161">Auto Restore 1/3: Implemenation of Nomination API via Caching Project Restore Info - [#3456](https://github.com/NuGet/Home/issues/3456)</span></span>

- <span data-ttu-id="cf240-162">[0] NuGet Obnovit úlohu & cíle - [#2994](https://github.com/NuGet/Home/issues/2994)</span><span class="sxs-lookup"><span data-stu-id="cf240-162">[0] NuGet Restore Task & Targets - [#2994](https://github.com/NuGet/Home/issues/2994)</span></span>

- <span data-ttu-id="cf240-163">[1] Povolit obnovení úrovně řešení v MSBuild - [#2993](https://github.com/NuGet/Home/issues/2993)</span><span class="sxs-lookup"><span data-stu-id="cf240-163">[1] Enable Solution level restore in MSBuild - [#2993](https://github.com/NuGet/Home/issues/2993)</span></span>

- <span data-ttu-id="cf240-164">Podpora veřejné rozšiřitelnosti poskytovatele pověření v sadě Visual Studio – [#2909](https://github.com/NuGet/Home/issues/2909)</span><span class="sxs-lookup"><span data-stu-id="cf240-164">Support credential provider public extensibility in Visual Studio - [#2909](https://github.com/NuGet/Home/issues/2909)</span></span>

- <span data-ttu-id="cf240-165">Obnovení rekurzivního nugetu - [#2533](https://github.com/NuGet/Home/issues/2533)</span><span class="sxs-lookup"><span data-stu-id="cf240-165">Recursive nuget restore - [#2533](https://github.com/NuGet/Home/issues/2533)</span></span>

- <span data-ttu-id="cf240-166">Nelze načíst Microsoft.TeamFoundation.Client na dev15, je třeba aktualizovat Microsoft.TeamFoundation.Client verze 15.0 pro VS "15" Preview - [#2392](https://github.com/NuGet/Home/issues/2392)</span><span class="sxs-lookup"><span data-stu-id="cf240-166">Can't load Microsoft.TeamFoundation.Client on dev15, need to update Microsoft.TeamFoundation.Client version to 15.0 for VS "15" Preview - [#2392](https://github.com/NuGet/Home/issues/2392)</span></span>

- <span data-ttu-id="cf240-167">Nelze nainstalovat balíček C++ do projektu C++ UWP v náhledu VS "15" - [#2369](https://github.com/NuGet/Home/issues/2369)</span><span class="sxs-lookup"><span data-stu-id="cf240-167">Unable to install C++ package to C++ UWP project in VS "15" Preview - [#2369](https://github.com/NuGet/Home/issues/2369)</span></span>

- <span data-ttu-id="cf240-168">Nupkg musí podporovat \buildCrossTargeting\ složku `.targets`  /  `.props` - a importovat pro "crosstargeting" MSBuild oboru.</span><span class="sxs-lookup"><span data-stu-id="cf240-168">Nupkg needs to support \buildCrossTargeting\ folder - and import `.targets` / `.props` for "crosstargeting" MSBuild scope.</span></span><span data-ttu-id="cf240-169"> - [#3499](https://github.com/NuGet/Home/issues/3499)</span><span class="sxs-lookup"><span data-stu-id="cf240-169"> - [#3499](https://github.com/NuGet/Home/issues/3499)</span></span>

- <span data-ttu-id="cf240-170">ToolsReference Design - [#3462](https://github.com/NuGet/Home/issues/3462)</span><span class="sxs-lookup"><span data-stu-id="cf240-170">ToolsReference Design - [#3462](https://github.com/NuGet/Home/issues/3462)</span></span>

- <span data-ttu-id="cf240-171">Oprava nugetového uznatého pro `.csproj`  - podporu obnovení w/ Reference balíčků v [#3455](https://github.com/NuGet/Home/issues/3455)</span><span class="sxs-lookup"><span data-stu-id="cf240-171">Fix NuGet UI to support restore w/ PackageReferences in `.csproj` - [#3455](https://github.com/NuGet/Home/issues/3455)</span></span>

- <span data-ttu-id="cf240-172">Přidání tlačítka vymazat mezipaměť do nastavení správce balíčků VS - [#3289](https://github.com/NuGet/Home/issues/3289)</span><span class="sxs-lookup"><span data-stu-id="cf240-172">Adding clear cache button to VS package manager settings - [#3289](https://github.com/NuGet/Home/issues/3289)</span></span>

## <a name="dcrs"></a><span data-ttu-id="cf240-173">Řadiče domény</span><span class="sxs-lookup"><span data-stu-id="cf240-173">DCRs</span></span>

- <span data-ttu-id="cf240-174">Obnovení řešení by měla být blokována, zatímco automatické obnovení probíhá.</span><span class="sxs-lookup"><span data-stu-id="cf240-174">Solution Restore should be blocked while auto restore is happening.</span></span><span data-ttu-id="cf240-175"> - [#3797](https://github.com/NuGet/Home/issues/3797)</span><span class="sxs-lookup"><span data-stu-id="cf240-175"> - [#3797](https://github.com/NuGet/Home/issues/3797)</span></span>

- <span data-ttu-id="cf240-176">NetCore nainstalovat z NuGet Package Manager ui nainstaluje do každého TFM , namísto ty, které podporuje balíček - [#3721](https://github.com/NuGet/Home/issues/3721)</span><span class="sxs-lookup"><span data-stu-id="cf240-176">NetCore install from NuGet Package Manager UI installs to every TFM , instead of ones that the package supports - [#3721](https://github.com/NuGet/Home/issues/3721)</span></span>

- <span data-ttu-id="cf240-177">Obnovení nominátor api potřebuje pro podporu DotNetCliToolsReferences příliš.</span><span class="sxs-lookup"><span data-stu-id="cf240-177">Restore nominator API needs to support DotNetCliToolsReferences too.</span></span><span data-ttu-id="cf240-178"> - [#3702](https://github.com/NuGet/Home/issues/3702)</span><span class="sxs-lookup"><span data-stu-id="cf240-178"> - [#3702](https://github.com/NuGet/Home/issues/3702)</span></span>

- <span data-ttu-id="cf240-179">Označte naše VS "15" vsix jako systémkomponenta - [#3700](https://github.com/NuGet/Home/issues/3700)</span><span class="sxs-lookup"><span data-stu-id="cf240-179">Mark our VS "15" vsix as a systemcomponent - [#3700](https://github.com/NuGet/Home/issues/3700)</span></span>

- <span data-ttu-id="cf240-180">Migrovat z odkazování na MS. Vs. Services.Client pro MS. Vs. Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)</span><span class="sxs-lookup"><span data-stu-id="cf240-180">Migrate from referencing MS.VS.Services.Client to MS.VS.Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)</span></span>

- <span data-ttu-id="cf240-181">$(RestoreLegacyPackagesDirectory) by měla být respektována na úrovni projektu obnovením - [#3618](https://github.com/NuGet/Home/issues/3618)</span><span class="sxs-lookup"><span data-stu-id="cf240-181">$(RestoreLegacyPackagesDirectory) should be respected at a project level by restore - [#3618](https://github.com/NuGet/Home/issues/3618)</span></span>

- <span data-ttu-id="cf240-182">Obnovit do projektu s jedním TargetFramework nesmí podmínku rekvizity - [#3588](https://github.com/NuGet/Home/issues/3588)</span><span class="sxs-lookup"><span data-stu-id="cf240-182">Restore to project with single TargetFramework must not condition props - [#3588](https://github.com/NuGet/Home/issues/3588)</span></span>

- <span data-ttu-id="cf240-183">dotnet</span><span class="sxs-lookup"><span data-stu-id="cf240-183">dotnet</span></span>
  - <span data-ttu-id="cf240-184">dotnetcore restore3 foo.csproj by měl následovat projectref závislosti, a obnovit ty taky.</span><span class="sxs-lookup"><span data-stu-id="cf240-184">dotnetcore restore3 foo.csproj should follow projectref dependencies, and restore those too.</span></span> <span data-ttu-id="cf240-185">Jako stavět.</span><span class="sxs-lookup"><span data-stu-id="cf240-185">Like build.</span></span><span data-ttu-id="cf240-186"> - [#3577](https://github.com/NuGet/Home/issues/3577)</span><span class="sxs-lookup"><span data-stu-id="cf240-186"> - [#3577](https://github.com/NuGet/Home/issues/3577)</span></span>

- <span data-ttu-id="cf240-187">"type": "platforma" Závislosti reprezentované jako "type":"package" v souboru zámku - [#2695](https://github.com/NuGet/Home/issues/2695)</span><span class="sxs-lookup"><span data-stu-id="cf240-187">"type": "platform" Dependencies represented as "type":"package" in lock file - [#2695](https://github.com/NuGet/Home/issues/2695)</span></span>

- <span data-ttu-id="cf240-188">nuget.exe Verbose režim by měl ukázat stáhnout url - [#2629](https://github.com/NuGet/Home/issues/2629)</span><span class="sxs-lookup"><span data-stu-id="cf240-188">nuget.exe Verbose mode should show the download url - [#2629](https://github.com/NuGet/Home/issues/2629)</span></span>

- <span data-ttu-id="cf240-189">Přesuňte NuGet xplat na Microsoft.NetCore.App a netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)</span><span class="sxs-lookup"><span data-stu-id="cf240-189">Move NuGet xplat to Microsoft.NetCore.App and netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)</span></span>

- <span data-ttu-id="cf240-190">Push - Při tlačení z příkazového řádku by mělo být možné přepsat symbolový server - [#2348](https://github.com/NuGet/Home/issues/2348)</span><span class="sxs-lookup"><span data-stu-id="cf240-190">Push - It should be possible to override the symbol server when pushing from the command line - [#2348](https://github.com/NuGet/Home/issues/2348)</span></span>

- <span data-ttu-id="cf240-191">Konsolidovat kód pro hledání cesty globálních balíčků – [#2296](https://github.com/NuGet/Home/issues/2296)</span><span class="sxs-lookup"><span data-stu-id="cf240-191">Consolidate code for finding the global packages path - [#2296](https://github.com/NuGet/Home/issues/2296)</span></span>

- <span data-ttu-id="cf240-192">Potřebujete lepší název než potlačitParent - [#2196](https://github.com/NuGet/Home/issues/2196)</span><span class="sxs-lookup"><span data-stu-id="cf240-192">Need a better name than suppressParent - [#2196](https://github.com/NuGet/Home/issues/2196)</span></span>

- <span data-ttu-id="cf240-193">Určit `project.json` název závislosti, který se má použít pro projekty MSBuild - [#1914](https://github.com/NuGet/Home/issues/1914)</span><span class="sxs-lookup"><span data-stu-id="cf240-193">Determine `project.json` dependency name to use for MSBuild projects - [#1914](https://github.com/NuGet/Home/issues/1914)</span></span>

- <span data-ttu-id="cf240-194">Přidat podporu SemVer 2.0.0 do NuGet.Core - [#3383](https://github.com/NuGet/Home/issues/3383)</span><span class="sxs-lookup"><span data-stu-id="cf240-194">Add SemVer 2.0.0 support to NuGet.Core - [#3383](https://github.com/NuGet/Home/issues/3383)</span></span>

- <span data-ttu-id="cf240-195">Povolit přenosité závislosti NuPkgs s `.targets` k dispozici v MSBuild - [#3342](https://github.com/NuGet/Home/issues/3342)</span><span class="sxs-lookup"><span data-stu-id="cf240-195">Allow transitive dependency NuPkgs with `.targets` to be available in MSBuild - [#3342](https://github.com/NuGet/Home/issues/3342)</span></span>

- <span data-ttu-id="cf240-196">Obnovení NuGet z příkazového řádku je výrazně pomalejší než VS - [#3330](https://github.com/NuGet/Home/issues/3330)</span><span class="sxs-lookup"><span data-stu-id="cf240-196">NuGet restore from the commandline is significantly slower than VS - [#3330](https://github.com/NuGet/Home/issues/3330)</span></span>

- <span data-ttu-id="cf240-197">Nastavení ID balíčku a porovnání verzí malá a velká písmena – [#2522](https://github.com/NuGet/Home/issues/2522)</span><span class="sxs-lookup"><span data-stu-id="cf240-197">Make package ID and version comparison case insensitive - [#2522](https://github.com/NuGet/Home/issues/2522)</span></span>

- <span data-ttu-id="cf240-198">NoCache možnost nefunguje `packages.config` pro založené obnovení nebo instalaci (GlobalPackagesFolder) - [#1406](https://github.com/NuGet/Home/issues/1406)</span><span class="sxs-lookup"><span data-stu-id="cf240-198">NoCache option does not work for `packages.config` based restore/install (GlobalPackagesFolder) - [#1406](https://github.com/NuGet/Home/issues/1406)</span></span>

- <span data-ttu-id="cf240-199">FindPackageByIdProstředky prostředky potřebuje výchozí kontext mezipaměti a logger - [#1357](https://github.com/NuGet/Home/issues/1357)</span><span class="sxs-lookup"><span data-stu-id="cf240-199">FindPackageByIdResource resources needs a default cache context and logger - [#1357](https://github.com/NuGet/Home/issues/1357)</span></span>
