---
title: Poznámky k verzi 3,5 RC
description: Poznámky k verzi pro NuGet 3,5 RC, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 04ec402df5ff993b405bb710abf26e1cdc850703
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780196"
---
# <a name="nuget-35-rc-release-notes"></a><span data-ttu-id="5feb4-103">Poznámky k verzi NuGet 3,5 RC</span><span class="sxs-lookup"><span data-stu-id="5feb4-103">NuGet 3.5 RC Release Notes</span></span>

<span data-ttu-id="5feb4-104">[Beta2 NuGet 3,5 – poznámky](../release-notes/nuget-3.5-Beta2.md)  |  k verzi [Poznámky k verzi pro NuGet 3,5 – RTM](../release-notes/nuget-3.5-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="5feb4-104">[NuGet 3.5-Beta2 Release Notes](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM Release Notes](../release-notes/nuget-3.5-RTM.md)</span></span>

<span data-ttu-id="5feb4-105">verze 3,5 se zaměřuje na zlepšení kvality a výkonu klientů NuGet.</span><span class="sxs-lookup"><span data-stu-id="5feb4-105">3.5 release is focused on improving quality and performance of NuGet clients.</span></span> <span data-ttu-id="5feb4-106">Kromě toho jsme dodali několik funkcí, jako je podpora [záložních složek](https://github.com/NuGet/Home/issues/2899), podpora [PackageType](https://github.com/NuGet/Home/issues/2476) v `.nuspec` a dalších.</span><span class="sxs-lookup"><span data-stu-id="5feb4-106">In addition, we have shipped a few features like support for [Fallback folders](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) support in `.nuspec` and more.</span></span>

[<span data-ttu-id="5feb4-107">Seznam problémů</span><span class="sxs-lookup"><span data-stu-id="5feb4-107">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a><span data-ttu-id="5feb4-108">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="5feb4-108">Bug Fixes</span></span>

* <span data-ttu-id="5feb4-109">Instalace nebo obnovení balíčku se nepovede a balíček obsahuje více `.nuspec` souborů.</span><span class="sxs-lookup"><span data-stu-id="5feb4-109">Install/restore of a package fails with "Package contains multiple `.nuspec` files."</span></span><span data-ttu-id="5feb4-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="5feb4-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="5feb4-111">sada NuGet Pack nuceně přidává `.tt` soubory do složky obsahu bez ohledu na to, co [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="5feb4-111">nuget pack forcefully adds `.tt` files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="5feb4-112">Chyba sady NuGet Pack csproj (with `project.json` ), pokud v souboru JSON nejsou žádné packOptions a Owner – [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="5feb4-112">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="5feb4-113">sada NuGet Pack pro `project.json` ignoruje značky packOptions, jako jsou souhrn, autoři, vlastníci atd. [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="5feb4-113">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="5feb4-114">sada NuGet Pack ignoruje závislosti ve výstupu `.nuspec` pro `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="5feb4-114">nuget pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="5feb4-115">Aktualizace více balíčků s vrácením změn ponechá projekt v nefunkčním stavu – [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="5feb4-115">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="5feb4-116">ContentFiles v případě, že nejsou přidány pro projekty netstandard – [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="5feb4-116">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="5feb4-117">Nelze zabalit správně cílení knihovny na .NET standard- [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="5feb4-117">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="5feb4-118">Soubor – > nový projekt – > knihovna tříd (přenosná) projekt se nezdařil v VS2015 a Dev15- [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="5feb4-118">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="5feb4-119">Chyba NuGet – 1.0.0-\* není platný řetězec verze – [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="5feb4-119">NuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="5feb4-120">Find-Package se nepovede zobrazit, ale funguje Install-Package [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="5feb4-120">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="5feb4-121">Chyba při instalaci balíčku jQuery. ověření na dev15- [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="5feb4-121">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="5feb4-122">Při instalaci VS 2015 Update 3 na VS, kde se používá chyba NuGet verze 3.5.0 – [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="5feb4-122">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="5feb4-123">Uživatelské rozhraní Správce balíčků: po aktualizaci balíčku nezobrazuje novou verzi [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="5feb4-123">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="5feb4-124">-ApiKey při odstraňování příkazového řádku není přečten/odeslán v 3.5.0-beta- [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="5feb4-124">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="5feb4-125">Nesprávný řetězec: stabilní verze balíčku by neměla mít v závislosti na předběžné verzi.</span><span class="sxs-lookup"><span data-stu-id="5feb4-125">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="5feb4-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="5feb4-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="5feb4-127">Vytváření projektu PCL (net46 a Windows 10) pro získání výjimky NullRef.</span><span class="sxs-lookup"><span data-stu-id="5feb4-127">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="5feb4-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="5feb4-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="5feb4-129">Aktualizace NuGet by měla poskytnout informativní zprávu, pokud je vyšší verze omezená omezením hodnota allowedversions- [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="5feb4-129">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="5feb4-130">Modul plug-in přihlašovacích údajů se ukončil s chybou-1/při stahování balíčku při použití zprostředkovatelů přihlašovacích údajů s více zdroji – [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="5feb4-130">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="5feb4-131">NuGet Pack – chybějící Newtonsoft.Jsu závislosti balíčku – [#2876](https://github.com/NuGet/Home/issues/2876)</span><span class="sxs-lookup"><span data-stu-id="5feb4-131">nuget pack - Missing Newtonsoft.Json package dependency - [#2876](https://github.com/NuGet/Home/issues/2876)</span></span>

* <span data-ttu-id="5feb4-132">Chyba v ExecuteSynchronizedCore v systému Linux/MacOS + mono- [#2860](https://github.com/NuGet/Home/issues/2860)</span><span class="sxs-lookup"><span data-stu-id="5feb4-132">Bug in ExecuteSynchronizedCore on Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span></span>

* <span data-ttu-id="5feb4-133">VS nepodporuje proměnné prostředí v repositoryPath (nuget.exe) – [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="5feb4-133">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="5feb4-134">Oprava problémů s přístupností – [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="5feb4-134">Fix Accessibility Issues - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="5feb4-135">Přenosná rozhraní s rozdělenými profily se odmítnou.</span><span class="sxs-lookup"><span data-stu-id="5feb4-135">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="5feb4-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="5feb4-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="5feb4-137">Správce balíčků NuGet by měl zrušit zaškrtnutí tohoto seznamu možností v podrobnostech balíčků se nevztahuje na `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="5feb4-137">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="5feb4-138">Aktualizace NuGet 3.3.0 se nezdařila s dodatečným omezením... definované v packages.config zabrání této operaci. '</span><span class="sxs-lookup"><span data-stu-id="5feb4-138">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="5feb4-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="5feb4-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="5feb4-140">Instalace balíčku z místního zdroje, který neexistuje, vyvolá nefalešnou zprávu- [#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="5feb4-140">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="5feb4-141">Filtr "k disstupnému upgradu" zobrazuje upgrady, které porušují omezení verze – [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="5feb4-141">"Upgrade vailable" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

## <a name="performance-improvements"></a><span data-ttu-id="5feb4-142">Zvýšení výkonu</span><span class="sxs-lookup"><span data-stu-id="5feb4-142">Performance Improvements</span></span>

* <span data-ttu-id="5feb4-143">Výkon: zlepšení analýzy cílového rozhraní ContentModel – [#3162](https://github.com/NuGet/Home/issues/3162)</span><span class="sxs-lookup"><span data-stu-id="5feb4-143">Performance: Improve ContentModel target framework parsing - [#3162](https://github.com/NuGet/Home/issues/3162)</span></span>

* <span data-ttu-id="5feb4-144">Výkon: Vyhněte se čtení `runtime.json` souborů pro obnovení, které nemají identifikátorů rid [#3150](https://github.com/NuGet/Home/issues/3150).</span><span class="sxs-lookup"><span data-stu-id="5feb4-144">Performance: Avoid reading `runtime.json` files for restores that do not have RIDs [#3150](https://github.com/NuGet/Home/issues/3150).</span></span> <span data-ttu-id="5feb4-145">V počítačích CI se obnoví Ukázková webová aplikace v ASP.NET z více než 15 sekund na 3 sekundy.</span><span class="sxs-lookup"><span data-stu-id="5feb4-145">On CI machines, restore of a sample ASP.NET Web Application reduced from over 15 secs to 3 secs.</span></span>

* <span data-ttu-id="5feb4-146">Výkon: konzola správce balíčků init.ps1 čas načítání [#2956](https://github.com/NuGet/Home/issues/2956).</span><span class="sxs-lookup"><span data-stu-id="5feb4-146">Performance: Package Manager Console init.ps1 load time [#2956](https://github.com/NuGet/Home/issues/2956).</span></span> <span data-ttu-id="5feb4-147">Čas na otevření PackageManagerConsole v některých případech od 132s po desítkách.</span><span class="sxs-lookup"><span data-stu-id="5feb4-147">Time to open PackageManagerConsole improved in some cases from 132s to 10s.</span></span>

* <span data-ttu-id="5feb4-148">Řešení problémů s výkonem v důsledku aktualizace NuGet- [#3044](https://github.com/NuGet/Home/issues/3044): na ukázkovém projektu se zkrátí doba potřebná k instalaci balíčků z 140s na 68s.</span><span class="sxs-lookup"><span data-stu-id="5feb4-148">Solve ReSharper performance issues in NuGet Update - [#3044](https://github.com/NuGet/Home/issues/3044): On a sample project, time taken to install packages reduced from 140s to 68s.</span></span>

## <a name="dcrs"></a><span data-ttu-id="5feb4-149">Chcete odeslat obecnou</span><span class="sxs-lookup"><span data-stu-id="5feb4-149">DCRs</span></span>

* <span data-ttu-id="5feb4-150">NuGet potřebuje, aby uživatelé věděli, že při upgradu nebo instalaci v dotnet TFM může dojít k problémům – [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="5feb4-150">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="5feb4-151">Upozorňovat na neplatnou instalaci/upgrade pro Project w/TFM = "dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="5feb4-151">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="5feb4-152">Přidání podpory netcoreapp11 a netstandard17 – [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="5feb4-152">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="5feb4-153">Vytisknout obsah záhlaví NuGet-Warning do konzoly v nuget.exe- [#2934](https://github.com/NuGet/Home/issues/2934)</span><span class="sxs-lookup"><span data-stu-id="5feb4-153">Print NuGet-Warning header contents to console in nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span></span>

* <span data-ttu-id="5feb4-154">Využití atributu AssemblyMetadata – pro `.nuspec` nahrazení tokenů – [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="5feb4-154">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>

* <span data-ttu-id="5feb4-155">Odeberte uzamčenou vlastnost ze souboru zámku – [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="5feb4-155">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="5feb4-156">Balíčky symbolů by se neměly nikdy používat při instalaci nebo aktualizaci #2807</span><span class="sxs-lookup"><span data-stu-id="5feb4-156">Symbol packages should not ever be used in install or update #2807</span></span>

## <a name="features"></a><span data-ttu-id="5feb4-157">Funkce</span><span class="sxs-lookup"><span data-stu-id="5feb4-157">Features</span></span>

* <span data-ttu-id="5feb4-158">Podpora pro složky záložních balíčků – [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="5feb4-158">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="5feb4-159">Navrhněte a implementujte fiktivní typ balíčku, který podporuje balíčky nástrojů – [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="5feb4-159">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="5feb4-160">Rozhraní API pro získání cesty ke složce globálních balíčků – [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="5feb4-160">API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="5feb4-161">Podpora aktualizací nativních balíčků – [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="5feb4-161">Native packages update support - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>
