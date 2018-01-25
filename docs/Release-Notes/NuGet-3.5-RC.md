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
# <a name="nuget-35-rc-release-notes"></a><span data-ttu-id="1348b-104">Poznámky k verzi RC NuGet 3.5</span><span class="sxs-lookup"><span data-stu-id="1348b-104">NuGet 3.5 RC Release Notes</span></span>

<span data-ttu-id="1348b-105">[Poznámky k verzi 3.5 Beta2 NuGet](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5 – poznámky k verzi RTM](../release-notes/nuget-3.5-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="1348b-105">[NuGet 3.5-Beta2 Release Notes](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM Release Notes](../release-notes/nuget-3.5-RTM.md)</span></span>

<span data-ttu-id="1348b-106">3.5 verze je zaměřena na zlepšení kvality a výkonu klienty NuGet.</span><span class="sxs-lookup"><span data-stu-id="1348b-106">3.5 release is focused on improving quality and performance of NuGet clients.</span></span> <span data-ttu-id="1348b-107">Kromě toho jsme poslali několik funkcí, jako je podpora pro [záložní složky](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) podporovat v `.nuspec` a další.</span><span class="sxs-lookup"><span data-stu-id="1348b-107">In addition, we have shipped a few features like support for [Fallback folders](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) support in `.nuspec` and more.</span></span>

[<span data-ttu-id="1348b-108">Seznam problémů</span><span class="sxs-lookup"><span data-stu-id="1348b-108">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5 RC")

## <a name="bug-fixes"></a><span data-ttu-id="1348b-109">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="1348b-109">Bug Fixes</span></span>

* <span data-ttu-id="1348b-110">Instalace a obnovení balíčku selže s "balíček obsahuje více `.nuspec` soubory."</span><span class="sxs-lookup"><span data-stu-id="1348b-110">Install/restore of a package fails with "Package contains multiple `.nuspec` files."</span></span><span data-ttu-id="1348b-111"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="1348b-111"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="1348b-112">nuget pack vynuceně přidá `.tt` soubory do složky obsahu bez ohledu na to, co - [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="1348b-112">nuget pack forcefully adds `.tt` files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="1348b-113">nuget pack csproj (s `project.json`) dojde k chybě, pokud nejsou žádné packOptions a vlastníka v souboru JSON - [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="1348b-113">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="1348b-114">balíček nuget pro `project.json` ignoruje packOptions značky souhrn, autoři, vlastníky atd - [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="1348b-114">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="1348b-115">nuget pack ignoruje závislosti ve výstupu `.nuspec` pro `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="1348b-115">nuget pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="1348b-116">Aktualizaci více balíčků s vrácení ponechá projektu v narušeném stavu - [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="1348b-116">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="1348b-117">ContentFiles ve všech nebyly přidány pro projekty monikerů netstandard - [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="1348b-117">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="1348b-118">Nelze vytvořit balíček knihovny cílení na rozhraní .net standardní správně – [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="1348b-118">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="1348b-119">Soubor -> Nový Projekt -> selže projektu knihovny tříd (přenositelností) v VS2015 a Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="1348b-119">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="1348b-120">Chyba nuGet - 1.0.0-\* není platný řetězec verze - [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="1348b-120">NuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="1348b-121">Najít balíček nepodaří zobrazení, ale funguje Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="1348b-121">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="1348b-122">Chyba při "Install-Package jquery.validation" na dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="1348b-122">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="1348b-123">Pokud je nainstalované VS 2015 s aktualizací 3 na VS, které používá NuGet dojde k chybě verze 3.5.0 - [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="1348b-123">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="1348b-124">Balíček uživatelského rozhraní správce: po aktualizaci balíčku nezobrazuje nová verze- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="1348b-124">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="1348b-125">-ApiKey na odstranění příkazového řádku pro čtení nebo neposílají v 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="1348b-125">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="1348b-126">Nesprávný řetězec: stabilní verze balíčku by neměla mít na závislost na předběžné verzi.</span><span class="sxs-lookup"><span data-stu-id="1348b-126">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="1348b-127"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="1348b-127"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="1348b-128">Vytvoření projektu get PCL (net46 a windows 10) NullRef výjimka.</span><span class="sxs-lookup"><span data-stu-id="1348b-128">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="1348b-129"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="1348b-129"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="1348b-130">Aktualizace Nuget by měl poskytovat informativní zprávy, když hodnota allowedVersions omezení - je omezený na vyšší verzi [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="1348b-130">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="1348b-131">Modul plug-in přihlašovacích údajů byl ukončen s chybou -1 / Chyba stahování balíčku při použití poskytovatelé přihlašovacích údajů pro více zdrojů - [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="1348b-131">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="1348b-132">nuget pack - závislost balíčku chybí Newtonsoft.Json - [#2876](https://github.com/NuGet/Home/issues/2876)</span><span class="sxs-lookup"><span data-stu-id="1348b-132">nuget pack - Missing Newtonsoft.Json package dependency - [#2876](https://github.com/NuGet/Home/issues/2876)</span></span>

* <span data-ttu-id="1348b-133">Chyby v ExecuteSynchronizedCore na systému Linux nebo MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span><span class="sxs-lookup"><span data-stu-id="1348b-133">Bug in ExecuteSynchronizedCore on Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span></span>

* <span data-ttu-id="1348b-134">VS nepodporuje proměnné prostředí v repositoryPath (nuget.exe nemá) - [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="1348b-134">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="1348b-135">Vyřešte problémy s - [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="1348b-135">Fix Accessibility Issues - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="1348b-136">Přenosné rozhraní s rozděleným profily byly zamítnuty.</span><span class="sxs-lookup"><span data-stu-id="1348b-136">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="1348b-137"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="1348b-137"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="1348b-138">Správce balíčků NuGet by mělo být zřejmé tento seznam možností v balíčcích podrobností se nevztahuje na `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="1348b-138">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="1348b-139">NuGet 3.3.0 aktualizace nezdaří s ' dodatečné omezení... definované v souboru packages.config téhle operaci brání. "</span><span class="sxs-lookup"><span data-stu-id="1348b-139">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="1348b-140"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="1348b-140"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="1348b-141">Instalace balíčku z místního zdroje, který neexistuje vyvolává neplatnou zpráva – [#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="1348b-141">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="1348b-142">"Upgrade ostupné" filtr zobrazuje upgrady, které porušují omezení verze - [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="1348b-142">"Upgrade vailable" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

## <a name="performance-improvements"></a><span data-ttu-id="1348b-143">Zvýšení výkonu</span><span class="sxs-lookup"><span data-stu-id="1348b-143">Performance Improvements</span></span>

* <span data-ttu-id="1348b-144">Výkonu: Zlepšení ContentModel cílový framework analýza - [#3162](https://github.com/NuGet/Home/issues/3162)</span><span class="sxs-lookup"><span data-stu-id="1348b-144">Performance: Improve ContentModel target framework parsing - [#3162](https://github.com/NuGet/Home/issues/3162)</span></span>

* <span data-ttu-id="1348b-145">Výkon: Vyhněte se čtení `runtime.json` soubory pro obnovení, které nemají identifikátorů RID [#3150](https://github.com/NuGet/Home/issues/3150).</span><span class="sxs-lookup"><span data-stu-id="1348b-145">Performance: Avoid reading `runtime.json` files for restores that do not have RIDs [#3150](https://github.com/NuGet/Home/issues/3150).</span></span> <span data-ttu-id="1348b-146">Na počítačích CI obnovení, které webové aplikace ASP.NET snížit z více než 15 sekund do 3 sekund vzorku.</span><span class="sxs-lookup"><span data-stu-id="1348b-146">On CI machines, restore of a sample ASP.NET Web Application reduced from over 15 secs to 3 secs.</span></span>

* <span data-ttu-id="1348b-147">Výkonu: Čas načtení init.ps1 Konzola správce balíčků [#2956](https://github.com/NuGet/Home/issues/2956).</span><span class="sxs-lookup"><span data-stu-id="1348b-147">Performance: Package Manager Console init.ps1 load time [#2956](https://github.com/NuGet/Home/issues/2956).</span></span> <span data-ttu-id="1348b-148">Čas otevření PackageManagerConsole vylepšení v některých případech z 132s 10s.</span><span class="sxs-lookup"><span data-stu-id="1348b-148">Time to open PackageManagerConsole improved in some cases from 132s to 10s.</span></span>

* <span data-ttu-id="1348b-149">Řešení problémů s výkonem ReSharper v aktualizaci NuGet - [#3044](https://github.com/NuGet/Home/issues/3044): na ukázkový projekt čas potřebný k instalaci balíčků zmenšeny z 140s 68s.</span><span class="sxs-lookup"><span data-stu-id="1348b-149">Solve ReSharper performance issues in NuGet Update - [#3044](https://github.com/NuGet/Home/issues/3044): On a sample project, time taken to install packages reduced from 140s to 68s.</span></span>

## <a name="dcrs"></a><span data-ttu-id="1348b-150">DCRs</span><span class="sxs-lookup"><span data-stu-id="1348b-150">DCRs</span></span>

* <span data-ttu-id="1348b-151">NuGet je potřeba upozornit uživatele, že upgrade nebo instalace v dotnet tfm, na základě PCL může způsobit problémy - [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="1348b-151">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="1348b-152">Upozornit chybná instalace nebo aktualizace pro projekt s tfm = "dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="1348b-152">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="1348b-153">Přidání podpory netcoreapp11 a netstandard17 - [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="1348b-153">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="1348b-154">Tisk obsahu hlavičky NuGet upozornění do konzoly v nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span><span class="sxs-lookup"><span data-stu-id="1348b-154">Print NuGet-Warning header contents to console in nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span></span>

* <span data-ttu-id="1348b-155">Assemblymetadata – atribut využívají pro `.nuspec` token náhrady - [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="1348b-155">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>

* <span data-ttu-id="1348b-156">Odebrat vlastnost uzamčeném zámek souboru - [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="1348b-156">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="1348b-157">Symbol balíčky někdy nesmí být použita v instalaci nebo aktualizaci #2807</span><span class="sxs-lookup"><span data-stu-id="1348b-157">Symbol packages should not ever be used in install or update #2807</span></span>

## <a name="features"></a><span data-ttu-id="1348b-158">Funkce</span><span class="sxs-lookup"><span data-stu-id="1348b-158">Features</span></span>

* <span data-ttu-id="1348b-159">Podporu pro záložní balíček složky - [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="1348b-159">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="1348b-160">Návrh a implementaci představu o typu balíčku pro podporu nástroje balíčky - [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="1348b-160">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="1348b-161">Rozhraní API pro získání cesty ke složce globální balíčky - [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="1348b-161">API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="1348b-162">Nativní balíčky aktualizovat podporu - [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="1348b-162">Native packages update support - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>
