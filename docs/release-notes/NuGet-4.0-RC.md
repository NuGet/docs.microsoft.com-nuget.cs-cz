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
# <a name="nuget-40-rc-release-notes"></a><span data-ttu-id="adda6-103">Zpráva k vydání verze NuGet 4.0 RC</span><span class="sxs-lookup"><span data-stu-id="adda6-103">NuGet 4.0 RC Release Notes</span></span>

[<span data-ttu-id="adda6-104">Zpráva k vydání verze NuGet 3.5 RTM</span><span class="sxs-lookup"><span data-stu-id="adda6-104">NuGet 3.5 RTM Release Notes</span></span>](../release-notes/nuget-3.5-RTM.md)

<span data-ttu-id="adda6-105">[NuGet 4.0 RC pro Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) se zaměřuje na přidání podpory pro scénáře .NET Core, adresování zpětné vazby zákazníků a vylepšení výkonu v nejrůznějších scénářích.</span><span class="sxs-lookup"><span data-stu-id="adda6-105">[NuGet 4.0 RC for Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) is focused on adding support for .NET Core scenarios, addressing key customer feedback and improving performance in a variety of scenarios.</span></span> <span data-ttu-id="adda6-106">Tato verze přináší několik vylepšení, jako je podpora pro PackageReference, NuGet příkazy jako cílů MSBuild, obnovení balíčku pozadí a další.</span><span class="sxs-lookup"><span data-stu-id="adda6-106">This release brings several improvements like support for PackageReference, NuGet commands as MSBuild targets, background package restore, and more.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="adda6-107">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="adda6-107">Bug Fixes</span></span>

- <span data-ttu-id="adda6-108">Chování změnami `dotnet pack --version-suffix foo`  -  [#3838](https://github.com/NuGet/Home/issues/3838)</span><span class="sxs-lookup"><span data-stu-id="adda6-108">Behavioral changes in `dotnet pack --version-suffix foo` - [#3838](https://github.com/NuGet/Home/issues/3838)</span></span>

- <span data-ttu-id="adda6-109">obnovení nuget.exe vs "15" počítač selže - [#3834](https://github.com/NuGet/Home/issues/3834)</span><span class="sxs-lookup"><span data-stu-id="adda6-109">nuget.exe restore on vs "15" machine only fails - [#3834](https://github.com/NuGet/Home/issues/3834)</span></span>

- <span data-ttu-id="adda6-110">. Nový projekt NETCore souboru by měly blokovat sestavení během obnovení – [#3780](https://github.com/NuGet/Home/issues/3780)</span><span class="sxs-lookup"><span data-stu-id="adda6-110">.NETCore file new project should block the build during restore - [#3780](https://github.com/NuGet/Home/issues/3780)</span></span>

- <span data-ttu-id="adda6-111">Webové aplikace ASP.NET Core migrované z VS2015 do sady VS "15", se nepovedlo obnovit.</span><span class="sxs-lookup"><span data-stu-id="adda6-111">ASP.NET Core web app, migrated from VS2015 to VS "15", unable to restore.</span></span><span data-ttu-id="adda6-112"> - [#3773](https://github.com/NuGet/Home/issues/3773)</span><span class="sxs-lookup"><span data-stu-id="adda6-112"> - [#3773](https://github.com/NuGet/Home/issues/3773)</span></span>

- <span data-ttu-id="adda6-113">[Selhání testu] Balíček "jQuery ověření" nelze odinstalovat, v uživatelském rozhraní odp. - [#3755](https://github.com/NuGet/Home/issues/3755)</span><span class="sxs-lookup"><span data-stu-id="adda6-113">[Test Failure]Package ‘jQuery Validation’ can’t be uninstalled by PM UI - [#3755](https://github.com/NuGet/Home/issues/3755)</span></span>

- <span data-ttu-id="adda6-114">Když se balíček nainstaluje na UPW `project.json`, má také obnovit projekty nadřazené - [#3731](https://github.com/NuGet/Home/issues/3731)</span><span class="sxs-lookup"><span data-stu-id="adda6-114">When a package is installed to UWP `project.json`, parent projects should also be restored - [#3731](https://github.com/NuGet/Home/issues/3731)</span></span>

- <span data-ttu-id="adda6-115">Úprava cíle NuGet do protokolu zdroje balíčků jako vysokou úroveň podrobností místo normální – [#3719](https://github.com/NuGet/Home/issues/3719)</span><span class="sxs-lookup"><span data-stu-id="adda6-115">Modify the NuGet targets to log the package sources as High verbosity instead of Normal - [#3719](https://github.com/NuGet/Home/issues/3719)</span></span>

- <span data-ttu-id="adda6-116">DotNet</span><span class="sxs-lookup"><span data-stu-id="adda6-116">dotnet</span></span>
  - <span data-ttu-id="adda6-117">dotnetcore pack3 by měl obsahovat dokumentace XML ve výchozím nastavení - [#3698](https://github.com/NuGet/Home/issues/3698)</span><span class="sxs-lookup"><span data-stu-id="adda6-117">dotnetcore pack3 should include XML documentation by default - [#3698](https://github.com/NuGet/Home/issues/3698)</span></span>

- <span data-ttu-id="adda6-118">Dávkové aktualizace nezdaří z uživatelského rozhraní při zdroje bez balíček je první a všechny zdroje je vybrán - [#3696](https://github.com/NuGet/Home/issues/3696)</span><span class="sxs-lookup"><span data-stu-id="adda6-118">Batch update fails from UI when source without the package is first and All source is selected - [#3696](https://github.com/NuGet/Home/issues/3696)</span></span>

- <span data-ttu-id="adda6-119">Příkaz balíčku Nuget neobsahuje všechny soubory – [#3678](https://github.com/NuGet/Home/issues/3678)</span><span class="sxs-lookup"><span data-stu-id="adda6-119">Nuget pack command does not include all files - [#3678](https://github.com/NuGet/Home/issues/3678)</span></span>

- <span data-ttu-id="adda6-120">Problém OOM - [#3661](https://github.com/NuGet/Home/issues/3661)</span><span class="sxs-lookup"><span data-stu-id="adda6-120">OOM issue - [#3661](https://github.com/NuGet/Home/issues/3661)</span></span>

- <span data-ttu-id="adda6-121">ProjectFileDependencyGroups části souboru prostředků by měl použít názvy knihoven pro projekty – [#3611](https://github.com/NuGet/Home/issues/3611)</span><span class="sxs-lookup"><span data-stu-id="adda6-121">ProjectFileDependencyGroups section of the assets file should use library names for projects - [#3611](https://github.com/NuGet/Home/issues/3611)</span></span>

- <span data-ttu-id="adda6-122">"dotnet restore" a recursing adresáře - [#3517](https://github.com/NuGet/Home/issues/3517)</span><span class="sxs-lookup"><span data-stu-id="adda6-122">"dotnet restore" and recursing directories - [#3517](https://github.com/NuGet/Home/issues/3517)</span></span>

- <span data-ttu-id="adda6-123">Restore3 chyby jsou protokolovány jako upozornění místo chyby - [#3503](https://github.com/NuGet/Home/issues/3503)</span><span class="sxs-lookup"><span data-stu-id="adda6-123">Restore3 failures are logged as warnings instead of errors - [#3503](https://github.com/NuGet/Home/issues/3503)</span></span>

- <span data-ttu-id="adda6-124">Problém TFS: "[soubor] nebyly nalezeny ve vašem pracovním prostoru, nebo nemáte oprávnění k přístupu"- [#2805](https://github.com/NuGet/Home/issues/2805)</span><span class="sxs-lookup"><span data-stu-id="adda6-124">TFS issue: "[file]not be found in your workspace, or you do not have permission to access it" - [#2805](https://github.com/NuGet/Home/issues/2805)</span></span>

- <span data-ttu-id="adda6-125">Zadáním "nuget <packagename>" v sadě Visual Studio uchovává rychlé spuštění vyhledávacího pole "nuget" předponu - [#2719](https://github.com/NuGet/Home/issues/2719)</span><span class="sxs-lookup"><span data-stu-id="adda6-125">Typing "nuget <packagename>" in vs quicklaunch search box keeps "nuget " prefix - [#2719](https://github.com/NuGet/Home/issues/2719)</span></span>

- <span data-ttu-id="adda6-126">System.Xml.XmlException: Neznámý kořenový prvek součásti Core Properties.</span><span class="sxs-lookup"><span data-stu-id="adda6-126">System.Xml.XmlException: Unrecognized root element in Core Properties part.</span></span> <span data-ttu-id="adda6-127">Řádek 2, pozice 2.</span><span class="sxs-lookup"><span data-stu-id="adda6-127">Line 2, position 2.</span></span><span data-ttu-id="adda6-128"> - [#2718](https://github.com/NuGet/Home/issues/2718)</span><span class="sxs-lookup"><span data-stu-id="adda6-128"> - [#2718](https://github.com/NuGet/Home/issues/2718)</span></span>

- <span data-ttu-id="adda6-129">`.nuspec` s uvozeny řídicími znaky &lt; nebo &gt; v textové pole již sestavení - [#2651](https://github.com/NuGet/Home/issues/2651)</span><span class="sxs-lookup"><span data-stu-id="adda6-129">`.nuspec` with escaped &lt; or &gt; in text fields no longer builds - [#2651](https://github.com/NuGet/Home/issues/2651)</span></span>

- <span data-ttu-id="adda6-130">Odstranit nuget.exe nezobrazí výzvu pro přihlašovací údaje (je v neinteraktivním režimu) – [#2626](https://github.com/NuGet/Home/issues/2626)</span><span class="sxs-lookup"><span data-stu-id="adda6-130">nuget.exe delete won't prompt for credentials (it's in non-interactive mode) - [#2626](https://github.com/NuGet/Home/issues/2626)</span></span>

- <span data-ttu-id="adda6-131">Odstranit nuget.exe upozorňuje klíč rozhraní API pro místní zdroje, i když nemá žádný smysl - [#2625](https://github.com/NuGet/Home/issues/2625)</span><span class="sxs-lookup"><span data-stu-id="adda6-131">nuget.exe delete warns about API Key for local sources, even though it makes no sense - [#2625](https://github.com/NuGet/Home/issues/2625)</span></span>

- <span data-ttu-id="adda6-132">Špatné zkušenosti chyby při instalaci EF - pre package - [#2566](https://github.com/NuGet/Home/issues/2566)</span><span class="sxs-lookup"><span data-stu-id="adda6-132">Error experience poor when installing EF -pre package - [#2566](https://github.com/NuGet/Home/issues/2566)</span></span>

- <span data-ttu-id="adda6-133">Visual Studio pokusem po změně výběru došlo k chybě ve správci balíčků - [#2551](https://github.com/NuGet/Home/issues/2551)</span><span class="sxs-lookup"><span data-stu-id="adda6-133">Visual Studio crashed attempting after changing selection in Package Manager - [#2551](https://github.com/NuGet/Home/issues/2551)</span></span>

- <span data-ttu-id="adda6-134">DotNet</span><span class="sxs-lookup"><span data-stu-id="adda6-134">dotnet</span></span>
  - <span data-ttu-id="adda6-135">obnovení dotnetcore provádí velká a malá písmena vyhledávání Id v plochém seznamu místních úložišť, když se používají s plovoucí desetinnou čárkou verze - [#2516](https://github.com/NuGet/Home/issues/2516)</span><span class="sxs-lookup"><span data-stu-id="adda6-135">dotnetcore restore performs case sensitive Id lookups on flat-list local repositories when floating versions are used - [#2516](https://github.com/NuGet/Home/issues/2516)</span></span>

- <span data-ttu-id="adda6-136">Odstranit nuget.exe je porušený pro kanál V2 – [#2509](https://github.com/NuGet/Home/issues/2509)</span><span class="sxs-lookup"><span data-stu-id="adda6-136">nuget.exe delete is broken for V2 feed - [#2509](https://github.com/NuGet/Home/issues/2509)</span></span>

- <span data-ttu-id="adda6-137">časový limit nabízených oznámení nuget.exe vyžaduje lepší chybové zprávy - [#2503](https://github.com/NuGet/Home/issues/2503)</span><span class="sxs-lookup"><span data-stu-id="adda6-137">nuget.exe push timeout needs a better error message - [#2503](https://github.com/NuGet/Home/issues/2503)</span></span>

- <span data-ttu-id="adda6-138">Nástroj pro obnovení bez správných importuje bez upozornění selže.</span><span class="sxs-lookup"><span data-stu-id="adda6-138">Tool restore without proper imports silently fails.</span></span><span data-ttu-id="adda6-139"> - [#2462](https://github.com/NuGet/Home/issues/2462)</span><span class="sxs-lookup"><span data-stu-id="adda6-139"> - [#2462](https://github.com/NuGet/Home/issues/2462)</span></span>

- <span data-ttu-id="adda6-140">NuGet vás vyzve k zadání přihlašovacích údajů, když je privátní kanál i v případě, že instalace z webu nuget.org - [#2346](https://github.com/NuGet/Home/issues/2346)</span><span class="sxs-lookup"><span data-stu-id="adda6-140">NuGet prompts to enter credentials when there is a private feed even when installing from nuget.org - [#2346](https://github.com/NuGet/Home/issues/2346)</span></span>

- <span data-ttu-id="adda6-141">Balíček ApplicationInsights 2.0 je uvedena, ale ještě - neexistuje [#2317](https://github.com/NuGet/Home/issues/2317)</span><span class="sxs-lookup"><span data-stu-id="adda6-141">ApplicationInsights 2.0 package is listed but doesn't exist yet - [#2317](https://github.com/NuGet/Home/issues/2317)</span></span>

- <span data-ttu-id="adda6-142">UIDelay v sadě Visual Studio "15" preview 5 větev - [#3500](https://github.com/NuGet/Home/issues/3500)</span><span class="sxs-lookup"><span data-stu-id="adda6-142">UIDelay in VS "15" preview 5 branch - [#3500](https://github.com/NuGet/Home/issues/3500)</span></span>

- <span data-ttu-id="adda6-143">První událost OnBuild chybí pro obnovení během sestavování pro UPW – [#3489](https://github.com/NuGet/Home/issues/3489)</span><span class="sxs-lookup"><span data-stu-id="adda6-143">First OnBuild event is missed for Restore during Build for UWP - [#3489](https://github.com/NuGet/Home/issues/3489)</span></span>

- <span data-ttu-id="adda6-144">Nainstaluje se při PowerShell5 konce objektu EntityFramework?</span><span class="sxs-lookup"><span data-stu-id="adda6-144">PowerShell5 breaks EntityFramework install?</span></span><span data-ttu-id="adda6-145"> - [#3312](https://github.com/NuGet/Home/issues/3312)</span><span class="sxs-lookup"><span data-stu-id="adda6-145"> - [#3312](https://github.com/NuGet/Home/issues/3312)</span></span>

- <span data-ttu-id="adda6-146">Přidání zdroje podrobné protokolování (zvažte pro 3.5) - [#3294](https://github.com/NuGet/Home/issues/3294)</span><span class="sxs-lookup"><span data-stu-id="adda6-146">Add source to detailed logging (consider for 3.5) - [#3294](https://github.com/NuGet/Home/issues/3294)</span></span>

- <span data-ttu-id="adda6-147">Parametr NoCache není zachované verzi klienta nuget 3.4 + - [#3074](https://github.com/NuGet/Home/issues/3074)</span><span class="sxs-lookup"><span data-stu-id="adda6-147">NoCache parameter not honored in nuget client version 3.4+ - [#3074](https://github.com/NuGet/Home/issues/3074)</span></span>

- <span data-ttu-id="adda6-148">Když poskytovatele přihlašovacích údajů se nepodaří načíst v sadě Visual Studio, neovlivní NuGet - [#2422](https://github.com/NuGet/Home/issues/2422)</span><span class="sxs-lookup"><span data-stu-id="adda6-148">When a credential provider fails to load in VS, don't break NuGet - [#2422](https://github.com/NuGet/Home/issues/2422)</span></span>

## <a name="features"></a><span data-ttu-id="adda6-149">Funkce</span><span class="sxs-lookup"><span data-stu-id="adda6-149">Features</span></span>

- <span data-ttu-id="adda6-150">Nastavte průběžnou Integraci pro spuštění x86- [#3868](https://github.com/NuGet/Home/issues/3868)</span><span class="sxs-lookup"><span data-stu-id="adda6-150">Set up CI to run x86 - [#3868](https://github.com/NuGet/Home/issues/3868)</span></span>

- <span data-ttu-id="adda6-151">Automatické obnovení 3/3: jiné blokující prvky UI - [#3658](https://github.com/NuGet/Home/issues/3658)</span><span class="sxs-lookup"><span data-stu-id="adda6-151">Auto Restore 3/3: non blocking UI - [#3658](https://github.com/NuGet/Home/issues/3658)</span></span>

- <span data-ttu-id="adda6-152">Automatické obnovení 2/3: na pozadí obnovení nominace - [#3657](https://github.com/NuGet/Home/issues/3657)</span><span class="sxs-lookup"><span data-stu-id="adda6-152">Auto Restore 2/3: background restore on nomination - [#3657](https://github.com/NuGet/Home/issues/3657)</span></span>

- <span data-ttu-id="adda6-153">Obnovit odolný systém souborů projektu tak, aby odpovídaly chování sestavení (recurse) - [#3615](https://github.com/NuGet/Home/issues/3615)</span><span class="sxs-lookup"><span data-stu-id="adda6-153">Restore project refs to match build behavior (recurse) - [#3615](https://github.com/NuGet/Home/issues/3615)</span></span>

- <span data-ttu-id="adda6-154">V sadě Visual Studio "15" – minbar – podpora DPL [#3614](https://github.com/NuGet/Home/issues/3614)</span><span class="sxs-lookup"><span data-stu-id="adda6-154">DPL support in VS "15" - minbar - [#3614](https://github.com/NuGet/Home/issues/3614)</span></span>

- <span data-ttu-id="adda6-155">Přesunout soubor s nastavením na Program Files - [#3613](https://github.com/NuGet/Home/issues/3613)</span><span class="sxs-lookup"><span data-stu-id="adda6-155">Move settings file to Program Files - [#3613](https://github.com/NuGet/Home/issues/3613)</span></span>

- <span data-ttu-id="adda6-156">Cíle a vlastnosti vygenerované obnovení potřebujete podporu zapojení cílení na různé - [#3496](https://github.com/NuGet/Home/issues/3496)</span><span class="sxs-lookup"><span data-stu-id="adda6-156">Generated restore props and targets need cross-targeting participation support - [#3496](https://github.com/NuGet/Home/issues/3496)</span></span>

- <span data-ttu-id="adda6-157">Podpora obnovení NuGet pro PackageTargetFallback (f.k.a importy) - [#3494](https://github.com/NuGet/Home/issues/3494)</span><span class="sxs-lookup"><span data-stu-id="adda6-157">NuGet Restore support for PackageTargetFallback (f.k.a Imports) - [#3494](https://github.com/NuGet/Home/issues/3494)</span></span>

- <span data-ttu-id="adda6-158">Implementace ToolsRef - [#3472](https://github.com/NuGet/Home/issues/3472)</span><span class="sxs-lookup"><span data-stu-id="adda6-158">ToolsRef implementation - [#3472](https://github.com/NuGet/Home/issues/3472)</span></span>

- <span data-ttu-id="adda6-159">Restore3 pro identifikátorů RID - [#3465](https://github.com/NuGet/Home/issues/3465)</span><span class="sxs-lookup"><span data-stu-id="adda6-159">Restore3 for a RID - [#3465](https://github.com/NuGet/Home/issues/3465)</span></span>

- <span data-ttu-id="adda6-160">NuGet uživatelského rozhraní pro podporu přidat nebo odebrat nebo aktualizovat PackageRefs - [#3457](https://github.com/NuGet/Home/issues/3457)</span><span class="sxs-lookup"><span data-stu-id="adda6-160">NuGet UI to support Add/Remove/Update of PackageRefs - [#3457](https://github.com/NuGet/Home/issues/3457)</span></span>

- <span data-ttu-id="adda6-161">Automatické obnovení 1/3: Implementace nominace rozhraní API prostřednictvím ukládání do mezipaměti projektu obnovit informace o - [#3456](https://github.com/NuGet/Home/issues/3456)</span><span class="sxs-lookup"><span data-stu-id="adda6-161">Auto Restore 1/3: Implemenation of Nomination API via Caching Project Restore Info - [#3456](https://github.com/NuGet/Home/issues/3456)</span></span>

- <span data-ttu-id="adda6-162">Obnovení NuGet [0], úlohy a cíle - [#2994](https://github.com/NuGet/Home/issues/2994)</span><span class="sxs-lookup"><span data-stu-id="adda6-162">[0] NuGet Restore Task & Targets - [#2994](https://github.com/NuGet/Home/issues/2994)</span></span>

- <span data-ttu-id="adda6-163">[1] povolit řešení obnovení na úrovni v nástroji MSBuild - [#2993](https://github.com/NuGet/Home/issues/2993)</span><span class="sxs-lookup"><span data-stu-id="adda6-163">[1] Enable Solution level restore in MSBuild - [#2993](https://github.com/NuGet/Home/issues/2993)</span></span>

- <span data-ttu-id="adda6-164">Podpora rozšiřitelnosti veřejného poskytovatele přihlašovacích údajů v sadě Visual Studio – [#2909](https://github.com/NuGet/Home/issues/2909)</span><span class="sxs-lookup"><span data-stu-id="adda6-164">Support credential provider public extensibility in Visual Studio - [#2909](https://github.com/NuGet/Home/issues/2909)</span></span>

- <span data-ttu-id="adda6-165">Rekurzivní nuget restore - [#2533](https://github.com/NuGet/Home/issues/2533)</span><span class="sxs-lookup"><span data-stu-id="adda6-165">Recursive nuget restore - [#2533](https://github.com/NuGet/Home/issues/2533)</span></span>

- <span data-ttu-id="adda6-166">Nelze načíst Microsoft.TeamFoundation.Client na odkaz na dev15, muset aktualizovat Microsoft.TeamFoundation.Client verzi 15.0 pro VS "15" Preview – [#2392](https://github.com/NuGet/Home/issues/2392)</span><span class="sxs-lookup"><span data-stu-id="adda6-166">Can't load Microsoft.TeamFoundation.Client on dev15, need to update Microsoft.TeamFoundation.Client version to 15.0 for VS "15" Preview - [#2392](https://github.com/NuGet/Home/issues/2392)</span></span>

- <span data-ttu-id="adda6-167">Nepovedlo se nainstalovat balíček C++ k C++ UWP projektu v sadě Visual Studio "15" Preview – [#2369](https://github.com/NuGet/Home/issues/2369)</span><span class="sxs-lookup"><span data-stu-id="adda6-167">Unable to install C++ package to C++ UWP project in VS "15" Preview - [#2369](https://github.com/NuGet/Home/issues/2369)</span></span>

- <span data-ttu-id="adda6-168">Nupkg musí podporovat \buildCrossTargeting\ složka – a importovat `.targets`  /  `.props` pro "crosstargeting" MSBuild oboru.</span><span class="sxs-lookup"><span data-stu-id="adda6-168">Nupkg needs to support \buildCrossTargeting\ folder - and import `.targets` / `.props` for "crosstargeting" MSBuild scope.</span></span><span data-ttu-id="adda6-169"> - [#3499](https://github.com/NuGet/Home/issues/3499)</span><span class="sxs-lookup"><span data-stu-id="adda6-169"> - [#3499](https://github.com/NuGet/Home/issues/3499)</span></span>

- <span data-ttu-id="adda6-170">Návrh ToolsReference – [#3462](https://github.com/NuGet/Home/issues/3462)</span><span class="sxs-lookup"><span data-stu-id="adda6-170">ToolsReference Design - [#3462](https://github.com/NuGet/Home/issues/3462)</span></span>

- <span data-ttu-id="adda6-171">Oprava NuGet uživatelského rozhraní pro podporu obnovení s PackageReferences v `.csproj`  -  [#3455](https://github.com/NuGet/Home/issues/3455)</span><span class="sxs-lookup"><span data-stu-id="adda6-171">Fix NuGet UI to support restore w/ PackageReferences in `.csproj` - [#3455](https://github.com/NuGet/Home/issues/3455)</span></span>

- <span data-ttu-id="adda6-172">Přidání tlačítka Vymazat mezipaměť nastavení Správce balíčků VS - [#3289](https://github.com/NuGet/Home/issues/3289)</span><span class="sxs-lookup"><span data-stu-id="adda6-172">Adding clear cache button to VS package manager settings - [#3289](https://github.com/NuGet/Home/issues/3289)</span></span>

## <a name="dcrs"></a><span data-ttu-id="adda6-173">Chcete</span><span class="sxs-lookup"><span data-stu-id="adda6-173">DCRs</span></span>

- <span data-ttu-id="adda6-174">Řešení obnovení by měly být blokovány, zatímco probíhá automatické obnovení.</span><span class="sxs-lookup"><span data-stu-id="adda6-174">Solution Restore should be blocked while auto restore is happening.</span></span><span data-ttu-id="adda6-175"> - [#3797](https://github.com/NuGet/Home/issues/3797)</span><span class="sxs-lookup"><span data-stu-id="adda6-175"> - [#3797](https://github.com/NuGet/Home/issues/3797)</span></span>

- <span data-ttu-id="adda6-176">Instalace NetCore z uživatelského rozhraní Správce balíčků NuGet nainstaluje do každé TFM místo, které podporuje balíčku - [#3721](https://github.com/NuGet/Home/issues/3721)</span><span class="sxs-lookup"><span data-stu-id="adda6-176">NetCore install from NuGet Package Manager UI installs to every TFM , instead of ones that the package supports - [#3721](https://github.com/NuGet/Home/issues/3721)</span></span>

- <span data-ttu-id="adda6-177">Obnovte nominator rozhraní API musí podporovat DotNetCliToolsReferences příliš.</span><span class="sxs-lookup"><span data-stu-id="adda6-177">Restore nominator API needs to support DotNetCliToolsReferences too.</span></span><span data-ttu-id="adda6-178"> - [#3702](https://github.com/NuGet/Home/issues/3702)</span><span class="sxs-lookup"><span data-stu-id="adda6-178"> - [#3702](https://github.com/NuGet/Home/issues/3702)</span></span>

- <span data-ttu-id="adda6-179">Označit naší sady VS "15" vsix jako systemcomponent - [#3700](https://github.com/NuGet/Home/issues/3700)</span><span class="sxs-lookup"><span data-stu-id="adda6-179">Mark our VS "15" vsix as a systemcomponent - [#3700](https://github.com/NuGet/Home/issues/3700)</span></span>

- <span data-ttu-id="adda6-180">Migrace z odkazující na MS. VS. Services.Client do MS. VS. Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)</span><span class="sxs-lookup"><span data-stu-id="adda6-180">Migrate from referencing MS.VS.Services.Client to MS.VS.Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)</span></span>

- <span data-ttu-id="adda6-181">$(RestoreLegacyPackagesDirectory) by měly dodržovat na úrovni projektu obnovení – [#3618](https://github.com/NuGet/Home/issues/3618)</span><span class="sxs-lookup"><span data-stu-id="adda6-181">$(RestoreLegacyPackagesDirectory) should be respected at a project level by restore - [#3618](https://github.com/NuGet/Home/issues/3618)</span></span>

- <span data-ttu-id="adda6-182">Obnovení do projektu pomocí jedné TargetFramework nesmí podmínky props – [#3588](https://github.com/NuGet/Home/issues/3588)</span><span class="sxs-lookup"><span data-stu-id="adda6-182">Restore to project with single TargetFramework must not condition props - [#3588](https://github.com/NuGet/Home/issues/3588)</span></span>

- <span data-ttu-id="adda6-183">DotNet</span><span class="sxs-lookup"><span data-stu-id="adda6-183">dotnet</span></span>
  - <span data-ttu-id="adda6-184">dotnetcore restore3 foo.csproj by měl postupujte podle projectref závislostí a těch obnovení příliš.</span><span class="sxs-lookup"><span data-stu-id="adda6-184">dotnetcore restore3 foo.csproj should follow projectref dependencies, and restore those too.</span></span> <span data-ttu-id="adda6-185">Stejně jako sestavení.</span><span class="sxs-lookup"><span data-stu-id="adda6-185">Like build.</span></span><span data-ttu-id="adda6-186"> - [#3577](https://github.com/NuGet/Home/issues/3577)</span><span class="sxs-lookup"><span data-stu-id="adda6-186"> - [#3577](https://github.com/NuGet/Home/issues/3577)</span></span>

- <span data-ttu-id="adda6-187">"type": "platformy" závislosti reprezentované jako "type": "balíček" v souboru zámku - [#2695](https://github.com/NuGet/Home/issues/2695)</span><span class="sxs-lookup"><span data-stu-id="adda6-187">"type": "platform" Dependencies represented as "type":"package" in lock file - [#2695](https://github.com/NuGet/Home/issues/2695)</span></span>

- <span data-ttu-id="adda6-188">režim podrobného vypisování nuget.exe by se zobrazit soubor ke stažení adresa url – [#2629](https://github.com/NuGet/Home/issues/2629)</span><span class="sxs-lookup"><span data-stu-id="adda6-188">nuget.exe Verbose mode should show the download url - [#2629](https://github.com/NuGet/Home/issues/2629)</span></span>

- <span data-ttu-id="adda6-189">Přesunout NuGet xplat pro balíčky Microsoft.NetCore.App a netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)</span><span class="sxs-lookup"><span data-stu-id="adda6-189">Move NuGet xplat to Microsoft.NetCore.App and netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)</span></span>

- <span data-ttu-id="adda6-190">Push – bude možné přepsat server symbolů při odesílání z příkazového řádku - [#2348](https://github.com/NuGet/Home/issues/2348)</span><span class="sxs-lookup"><span data-stu-id="adda6-190">Push - It should be possible to override the symbol server when pushing from the command line - [#2348](https://github.com/NuGet/Home/issues/2348)</span></span>

- <span data-ttu-id="adda6-191">Sloučit kód pro vyhledání globálních balíčků cesta - [#2296](https://github.com/NuGet/Home/issues/2296)</span><span class="sxs-lookup"><span data-stu-id="adda6-191">Consolidate code for finding the global packages path - [#2296](https://github.com/NuGet/Home/issues/2296)</span></span>

- <span data-ttu-id="adda6-192">Třeba názvu lepší než suppressParent - [#2196](https://github.com/NuGet/Home/issues/2196)</span><span class="sxs-lookup"><span data-stu-id="adda6-192">Need a better name than suppressParent - [#2196](https://github.com/NuGet/Home/issues/2196)</span></span>

- <span data-ttu-id="adda6-193">Určení `project.json` název závislosti pro projekty MSBuild - [#1914](https://github.com/NuGet/Home/issues/1914)</span><span class="sxs-lookup"><span data-stu-id="adda6-193">Determine `project.json` dependency name to use for MSBuild projects - [#1914](https://github.com/NuGet/Home/issues/1914)</span></span>

- <span data-ttu-id="adda6-194">Přidání podpory SemVer 2.0.0 NuGet.Core - [#3383](https://github.com/NuGet/Home/issues/3383)</span><span class="sxs-lookup"><span data-stu-id="adda6-194">Add SemVer 2.0.0 support to NuGet.Core - [#3383](https://github.com/NuGet/Home/issues/3383)</span></span>

- <span data-ttu-id="adda6-195">Povolit přechodné závislosti NuPkgs s `.targets` k dispozici v nástroji MSBuild - [#3342](https://github.com/NuGet/Home/issues/3342)</span><span class="sxs-lookup"><span data-stu-id="adda6-195">Allow transitive dependency NuPkgs with `.targets` to be available in MSBuild - [#3342](https://github.com/NuGet/Home/issues/3342)</span></span>

- <span data-ttu-id="adda6-196">Obnovení NuGet řádku je výrazně pomalejší než VS - [#3330](https://github.com/NuGet/Home/issues/3330)</span><span class="sxs-lookup"><span data-stu-id="adda6-196">NuGet restore from the commandline is significantly slower than VS - [#3330](https://github.com/NuGet/Home/issues/3330)</span></span>

- <span data-ttu-id="adda6-197">Provést porovnání ID a verzi balíčku malá a velká písmena - [#2522](https://github.com/NuGet/Home/issues/2522)</span><span class="sxs-lookup"><span data-stu-id="adda6-197">Make package ID and version comparison case insensitive - [#2522](https://github.com/NuGet/Home/issues/2522)</span></span>

- <span data-ttu-id="adda6-198">Možnost NoCache nefunguje pro `packages.config` na základě obnovení/install (GlobalPackagesFolder) - [#1406](https://github.com/NuGet/Home/issues/1406)</span><span class="sxs-lookup"><span data-stu-id="adda6-198">NoCache option does not work for `packages.config` based restore/install (GlobalPackagesFolder) - [#1406](https://github.com/NuGet/Home/issues/1406)</span></span>

- <span data-ttu-id="adda6-199">Prostředky FindPackageByIdResource potřebuje výchozí kontext mezipaměti a protokolování - [#1357](https://github.com/NuGet/Home/issues/1357)</span><span class="sxs-lookup"><span data-stu-id="adda6-199">FindPackageByIdResource resources needs a default cache context and logger - [#1357](https://github.com/NuGet/Home/issues/1357)</span></span>
