---
title: 3.5 zpráva k vydání verze RC
description: Zpráva k vydání verze pro NuGet 3.5 RC, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 52c443ecd79c9108203f5a3c327078ce9e28b95b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548535"
---
# <a name="nuget-35-rc-release-notes"></a><span data-ttu-id="8f1ce-103">Zpráva k vydání verze NuGet 3.5 RC</span><span class="sxs-lookup"><span data-stu-id="8f1ce-103">NuGet 3.5 RC Release Notes</span></span>

<span data-ttu-id="8f1ce-104">[Zpráva k vydání verze NuGet 3.5 Beta2](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5 – zpráva k vydání verze RTM](../release-notes/nuget-3.5-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="8f1ce-104">[NuGet 3.5-Beta2 Release Notes](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM Release Notes](../release-notes/nuget-3.5-RTM.md)</span></span>

<span data-ttu-id="8f1ce-105">3.5 verze se zaměřuje na vylepšení kvality a výkonu klientů NuGet.</span><span class="sxs-lookup"><span data-stu-id="8f1ce-105">3.5 release is focused on improving quality and performance of NuGet clients.</span></span> <span data-ttu-id="8f1ce-106">Kromě toho jsme poslali několik funkcí, jako je podpora [záložní složky](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) podporují v `.nuspec` a provádění dalších akcí.</span><span class="sxs-lookup"><span data-stu-id="8f1ce-106">In addition, we have shipped a few features like support for [Fallback folders](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) support in `.nuspec` and more.</span></span>

[<span data-ttu-id="8f1ce-107">Seznam problémů</span><span class="sxs-lookup"><span data-stu-id="8f1ce-107">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a><span data-ttu-id="8f1ce-108">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="8f1ce-108">Bug Fixes</span></span>

* <span data-ttu-id="8f1ce-109">Instalace a obnovení balíčku selže s "balíček obsahuje více `.nuspec` soubory."</span><span class="sxs-lookup"><span data-stu-id="8f1ce-109">Install/restore of a package fails with "Package contains multiple `.nuspec` files."</span></span><span data-ttu-id="8f1ce-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="8f1ce-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="8f1ce-111">balíček nuget vynuceně přidá `.tt` soubory do složky obsahu bez ohledu na to, co - [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="8f1ce-111">nuget pack forcefully adds `.tt` files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="8f1ce-112">balíček nuget souboru csproj (s `project.json`) dojde k chybě, pokud neexistují žádné packOptions a vlastník v souboru JSON - [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="8f1ce-112">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="8f1ce-113">balíček nuget pro `project.json` packOptions značky jako souhrn, autory, vlastníci atd – ignoruje [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="8f1ce-113">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="8f1ce-114">balíček nuget ignoruje závislosti ve výstupu `.nuspec` pro `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="8f1ce-114">nuget pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="8f1ce-115">Aktualizaci více balíčků s vrácení zpět opustí projektu je porušený - [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="8f1ce-115">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="8f1ce-116">ContentFiles za nejsou přidány pro projekty netstandard – [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="8f1ce-116">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="8f1ce-117">Nelze vytvořit balíček knihovny cílené na .net Standard správně – [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="8f1ce-117">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="8f1ce-118">Soubor -> Nový Projekt -> selže projekt knihovny tříd (přenosná) ve VS2015 a odkaz na Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="8f1ce-118">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="8f1ce-119">Chyba nuGet – 1.0.0-\* není platný řetězec verze - [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="8f1ce-119">NuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="8f1ce-120">Vyhledání balíčku selže zobrazení, ale funguje Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="8f1ce-120">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="8f1ce-121">Chyba při "Install-Package jquery.validation" na odkaz na dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="8f1ce-121">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="8f1ce-122">Při nainstalované VS 2015 s aktualizací 3 na VS, které používá NuGet dojde k chybě verze 3.5.0 - [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="8f1ce-122">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="8f1ce-123">Uživatelské rozhraní Správce balíčků: Nová verze nezobrazuje po aktualizaci balíčku- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="8f1ce-123">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="8f1ce-124">-ApiKey na příkazovém řádku delete není pro čtení/poslaná 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="8f1ce-124">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="8f1ce-125">Řetězce není správný: stabilní verze balíčku by neměla mít na předběžnou verzi závislosti.</span><span class="sxs-lookup"><span data-stu-id="8f1ce-125">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="8f1ce-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="8f1ce-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="8f1ce-127">Vytváří se získat projekt PCL (net46 a windows 10) NullRef výjimky.</span><span class="sxs-lookup"><span data-stu-id="8f1ce-127">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="8f1ce-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="8f1ce-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="8f1ce-129">Nuget aktualizace by měla poskytnout informativní zprávy, když hodnota allowedVersions omezení – je omezený na vyšší verzi rozhraní [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="8f1ce-129">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="8f1ce-130">Plugin přihlašovacích údajů se ukončil s chybou -1 / Chyba při stahování balíčku při použití poskytovatelé přihlašovacích údajů s více zdroji - [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="8f1ce-130">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="8f1ce-131">balíček nuget - Newtonsoft.Json chybějící závislost balíčku - [#2876](https://github.com/NuGet/Home/issues/2876)</span><span class="sxs-lookup"><span data-stu-id="8f1ce-131">nuget pack - Missing Newtonsoft.Json package dependency - [#2876](https://github.com/NuGet/Home/issues/2876)</span></span>

* <span data-ttu-id="8f1ce-132">Chyby v ExecuteSynchronizedCore na Linux nebo MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span><span class="sxs-lookup"><span data-stu-id="8f1ce-132">Bug in ExecuteSynchronizedCore on Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span></span>

* <span data-ttu-id="8f1ce-133">VS nepodporuje proměnné prostředí v repositoryPath (nuget.exe nepodporuje) - [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="8f1ce-133">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="8f1ce-134">Oprava problémů s přístupností – [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="8f1ce-134">Fix Accessibility Issues - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="8f1ce-135">Přenosná rozhraní s pomlčkou profily odmítají.</span><span class="sxs-lookup"><span data-stu-id="8f1ce-135">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="8f1ce-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="8f1ce-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="8f1ce-137">Správce balíčků NuGet by mělo být zřejmé tento seznam možností v balíčcích podrobností se nedá použít u `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="8f1ce-137">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="8f1ce-138">Aktualizace NuGet 3.3.0 selže s '... Další omezení definované v souboru packages.config téhle operaci brání. "</span><span class="sxs-lookup"><span data-stu-id="8f1ce-138">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="8f1ce-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="8f1ce-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="8f1ce-140">Instalace balíčku z místního zdroje, který neexistuje, vyvolá výjimku neplatného zpráva – [#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="8f1ce-140">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="8f1ce-141">Filtr "Upgrade dostupné" zobrazuje upgrady, které narušují omezení verze - [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="8f1ce-141">"Upgrade vailable" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

## <a name="performance-improvements"></a><span data-ttu-id="8f1ce-142">Zvýšení výkonu</span><span class="sxs-lookup"><span data-stu-id="8f1ce-142">Performance Improvements</span></span>

* <span data-ttu-id="8f1ce-143">Výkonu: Zlepšení vlastnost ContentModel cílové rozhraní framework analýza kódu - [#3162](https://github.com/NuGet/Home/issues/3162)</span><span class="sxs-lookup"><span data-stu-id="8f1ce-143">Performance: Improve ContentModel target framework parsing - [#3162](https://github.com/NuGet/Home/issues/3162)</span></span>

* <span data-ttu-id="8f1ce-144">Výkon: Vyhněte se čtení `runtime.json` soubory pro obnovení, které nemají identifikátorů RID [#3150](https://github.com/NuGet/Home/issues/3150).</span><span class="sxs-lookup"><span data-stu-id="8f1ce-144">Performance: Avoid reading `runtime.json` files for restores that do not have RIDs [#3150](https://github.com/NuGet/Home/issues/3150).</span></span> <span data-ttu-id="8f1ce-145">Na počítačích CI obnovení ukázku, kterou webová aplikace ASP.NET se zkrátilo z více než 15 sekund na 3 sekundy.</span><span class="sxs-lookup"><span data-stu-id="8f1ce-145">On CI machines, restore of a sample ASP.NET Web Application reduced from over 15 secs to 3 secs.</span></span>

* <span data-ttu-id="8f1ce-146">Výkonu: Doba načtení konzoly Správce balíčků init.ps1 [#2956](https://github.com/NuGet/Home/issues/2956).</span><span class="sxs-lookup"><span data-stu-id="8f1ce-146">Performance: Package Manager Console init.ps1 load time [#2956](https://github.com/NuGet/Home/issues/2956).</span></span> <span data-ttu-id="8f1ce-147">Vylepšená doba otevření PackageManagerConsole v některých případech z 132s 10s.</span><span class="sxs-lookup"><span data-stu-id="8f1ce-147">Time to open PackageManagerConsole improved in some cases from 132s to 10s.</span></span>

* <span data-ttu-id="8f1ce-148">Řešte problémy s výkonem ReSharper v NuGet pro sadu Vs11 – [#3044](https://github.com/NuGet/Home/issues/3044): na ukázkového projektu a čas potřebný k instalaci balíčků redukovaným z 140s k 68s.</span><span class="sxs-lookup"><span data-stu-id="8f1ce-148">Solve ReSharper performance issues in NuGet Update - [#3044](https://github.com/NuGet/Home/issues/3044): On a sample project, time taken to install packages reduced from 140s to 68s.</span></span>

## <a name="dcrs"></a><span data-ttu-id="8f1ce-149">Chcete</span><span class="sxs-lookup"><span data-stu-id="8f1ce-149">DCRs</span></span>

* <span data-ttu-id="8f1ce-150">NuGet je potřeba uživatelům sdělit, že upgrade nebo instalace v dotnet tfm na základě PCL může způsobit problémy se - [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="8f1ce-150">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="8f1ce-151">Upozornit chybný instalace/aktualizace pro projekt plánovaným bodem obnovení kratším tfm = "dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="8f1ce-151">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="8f1ce-152">Přidání podpory netcoreapp11 a netstandard17 - [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="8f1ce-152">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="8f1ce-153">Vytisknout obsah záhlaví NuGet upozornění do konzoly v nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span><span class="sxs-lookup"><span data-stu-id="8f1ce-153">Print NuGet-Warning header contents to console in nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span></span>

* <span data-ttu-id="8f1ce-154">Využijte assemblymetadata – atribut pro `.nuspec` token nahrazení - [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="8f1ce-154">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>

* <span data-ttu-id="8f1ce-155">Odeberte vlastnost uzamčená ze souboru zámku – [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="8f1ce-155">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="8f1ce-156">Balíčky symbolů by neměl být nikdy nepoužil v instalaci nebo aktualizaci #2807</span><span class="sxs-lookup"><span data-stu-id="8f1ce-156">Symbol packages should not ever be used in install or update #2807</span></span>

## <a name="features"></a><span data-ttu-id="8f1ce-157">Funkce</span><span class="sxs-lookup"><span data-stu-id="8f1ce-157">Features</span></span>

* <span data-ttu-id="8f1ce-158">Podpora pro použití náhradní lokality balíček složky – [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="8f1ce-158">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="8f1ce-159">Návrh a implementace hodnoty typu balíčku pro podporu nástroje balíčky - [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="8f1ce-159">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="8f1ce-160">Rozhraní API k získání cesty ke složce globálních balíčků - [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="8f1ce-160">API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="8f1ce-161">Nativní balíčky podpora - update [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="8f1ce-161">Native packages update support - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>
