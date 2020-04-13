---
title: NuGet 4.3 RTM Poznámky k verzi
description: Poznámky k verzi pro NuGet 4.3 RTM včetně známých problémů, oprav chyb, přidaných funkcí a řadičů domény.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 72d707cb9bacd8abbac873ee10b2fd00f233d3cc
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496594"
---
# <a name="nuget-43-release-notes"></a><span data-ttu-id="07c3f-103">NuGet 4.3 Poznámky k verzi</span><span class="sxs-lookup"><span data-stu-id="07c3f-103">NuGet 4.3 Release Notes</span></span>

<span data-ttu-id="07c3f-104">[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) je dodáván s NuGet 4.3 RTM, který přidává podporu pro nové scénáře, jako je například .NET Standard 2.0/.NET Core 2.0, obsahuje mnoho oprav kvality a zlepšuje výkon.</span><span class="sxs-lookup"><span data-stu-id="07c3f-104">[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.3 RTM which adds support for new scenarios such as .NET Standard 2.0/.NET Core 2.0, contains many quality fixes, and improves performance.</span></span> <span data-ttu-id="07c3f-105">Tato verze také přináší několik vylepšení, jako je podpora pro sémantické versioning 2.0.0, MSBuild integrace NuGet upozornění a chyby a další.</span><span class="sxs-lookup"><span data-stu-id="07c3f-105">This release also brings several improvements like support for Semantic Versioning 2.0.0, MSBuild integration of NuGet warnings and errors, and more.</span></span>

## <a name="summary-whats-new-in-430"></a><span data-ttu-id="07c3f-106">Shrnutí: Co je nového v 4.3.0</span><span class="sxs-lookup"><span data-stu-id="07c3f-106">Summary: What's New in 4.3.0</span></span>

## <a name="summary-whats-new-in-431"></a><span data-ttu-id="07c3f-107">Shrnutí: Co je nového v 4.3.1</span><span class="sxs-lookup"><span data-stu-id="07c3f-107">Summary: What's New in 4.3.1</span></span>

* <span data-ttu-id="07c3f-108">Oprava zabezpečení: Oprávnění k souborům vytvořeným uvnitř ~/.nuget jsou příliš otevřená [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span><span class="sxs-lookup"><span data-stu-id="07c3f-108">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>
* <span data-ttu-id="07c3f-109">Oprava zabezpečení: Soubory uvnitř NUPKGs mohou mít relativní cestu nad adresářem NUPKG [#7906](https://github.com/NuGet/Home/issues/7906)</span><span class="sxs-lookup"><span data-stu-id="07c3f-109">Security Fix: Files inside of NUPKGs can have a relative path above the NUPKG directory [#7906](https://github.com/NuGet/Home/issues/7906)</span></span>

## <a name="known-issues"></a><span data-ttu-id="07c3f-110">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="07c3f-110">Known issues</span></span>

### <a name="nuget-restore-may-treat-disabled-package-sources-as-enabled-in-some-cases"></a><span data-ttu-id="07c3f-111">Při obnovení NuGet se v některých případech může se zakázanými zdroji balíčků zacházet, jako by byly povolené</span><span class="sxs-lookup"><span data-stu-id="07c3f-111">NuGet restore may treat disabled package sources as enabled in some cases</span></span>

#### <a name="issue"></a><span data-ttu-id="07c3f-112">Problém</span><span class="sxs-lookup"><span data-stu-id="07c3f-112">Issue</span></span>

<span data-ttu-id="07c3f-113">Následující techniky obnovení příkazového řádku považují zakázané zdroje balíčků za povolené.</span><span class="sxs-lookup"><span data-stu-id="07c3f-113">The following restore command-line techniques treat disabled packages sources as enabled.</span></span> [<span data-ttu-id="07c3f-114">NuGet#5704</span><span class="sxs-lookup"><span data-stu-id="07c3f-114">NuGet#5704</span></span>](https://github.com/NuGet/Home/issues/5704)
- `msbuild /t:restore`
- <span data-ttu-id="07c3f-115">`dotnet restore`(buď s dotnet.exe, který je dodáván s VS, nebo ten, který je dodáván s NetCore SDK 2.0.0)</span><span class="sxs-lookup"><span data-stu-id="07c3f-115">`dotnet restore` (either with dotnet.exe that ships with VS, or the one that comes with NetCore SDK 2.0.0)</span></span>

#### <a name="workaround"></a><span data-ttu-id="07c3f-116">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="07c3f-116">Workaround</span></span>

1. <span data-ttu-id="07c3f-117">Používejte Visual Studio ve verzi 2017 (sestavení 15.3 nebo novější) nebo nástroj NuGet.exe ve verzi 4.3.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="07c3f-117">Use Visual Studio (2017 15.3 or later) or NuGet.exe (v4.3.0 or later)</span></span>
1. <span data-ttu-id="07c3f-118">Zakázaný zdroj odstraňte a dál používejte příkazy msbuild nebo dotnet.exe.</span><span class="sxs-lookup"><span data-stu-id="07c3f-118">Delete your disabled source and continue to use msbuild or dotnet.exe.</span></span>
1. <span data-ttu-id="07c3f-119">Ve svém řešení můžete do konfigurace NuGet.config vložit element Clear a pak definovat zdroje potřebné v daném řešení.</span><span class="sxs-lookup"><span data-stu-id="07c3f-119">For your solution, you could use "Clear" in NuGet.config and then define the sources necessary for that solution.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="07c3f-120">Při používání konzoly Správce balíčků nemusí fungovat klávesa Enter</span><span class="sxs-lookup"><span data-stu-id="07c3f-120">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="07c3f-121">Problém</span><span class="sxs-lookup"><span data-stu-id="07c3f-121">Issue</span></span>

<span data-ttu-id="07c3f-122">V konzole Správce balíčků občas nefunguje klávesa Enter.</span><span class="sxs-lookup"><span data-stu-id="07c3f-122">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="07c3f-123">Když toto chování zpozorujete, zjistěte prosím, jak to vypadá s opravou, a poskytněte jakékoli další užitečné informace o postupu, jak tuto chybu reprodukovat.</span><span class="sxs-lookup"><span data-stu-id="07c3f-123">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="07c3f-124">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="07c3f-124">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="07c3f-125">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="07c3f-125">Workaround</span></span>

<span data-ttu-id="07c3f-126">Před otevřením řešení restartujte Visual Studio a otevřete konzolu PMC.</span><span class="sxs-lookup"><span data-stu-id="07c3f-126">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="07c3f-127">Případně zkuste znovu smažit `project.lock.json` a obnovit.</span><span class="sxs-lookup"><span data-stu-id="07c3f-127">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="07c3f-128">Pomocí Nástroje pro balení Nuget nelze zobrazit, přidat nebo aktualizovat nástroje DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="07c3f-128">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="07c3f-129">Problém</span><span class="sxs-lookup"><span data-stu-id="07c3f-129">Issue</span></span>

<span data-ttu-id="07c3f-130">Správce balíčků NuGet nezobrazuje a nepovoluje přidat nebo aktualizovat DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="07c3f-130">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="07c3f-131">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="07c3f-131">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="07c3f-132">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="07c3f-132">Workaround</span></span>

<span data-ttu-id="07c3f-133">V souboru projektu se musí ručně upravit DotNetCLIToolReferences.</span><span class="sxs-lookup"><span data-stu-id="07c3f-133">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="07c3f-134">Změna cílení verze cílové architektury může vést k nekompletnímu IntelliSense</span><span class="sxs-lookup"><span data-stu-id="07c3f-134">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="07c3f-135">Problém</span><span class="sxs-lookup"><span data-stu-id="07c3f-135">Issue</span></span>

<span data-ttu-id="07c3f-136">Změna cílení verze cílové architektury v sadě Visual Studio může vést k nekompletnímu IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="07c3f-136">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="07c3f-137">To se stává, když jako formát správce balíčků používáte PackageReferences.</span><span class="sxs-lookup"><span data-stu-id="07c3f-137">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="07c3f-138">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="07c3f-138">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="07c3f-139">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="07c3f-139">Workaround</span></span>

<span data-ttu-id="07c3f-140">Proveďte ruční obnovení.</span><span class="sxs-lookup"><span data-stu-id="07c3f-140">Do a manual restore.</span></span>

## <a name="issues-fixed-in-nuget-43-rtm-timeframe"></a><span data-ttu-id="07c3f-141">Problémy opravené v časovém rámci NuGet 4.3 RTM</span><span class="sxs-lookup"><span data-stu-id="07c3f-141">Issues fixed in NuGet 4.3 RTM timeframe</span></span>

<span data-ttu-id="07c3f-142">[NuGet 4.0 RTM Poznámky k verzi](../release-notes/nuget-4.0-RTM.md) - Seznam všech problémů opravených pro NuGet 4.0 RTM</span><span class="sxs-lookup"><span data-stu-id="07c3f-142">[NuGet 4.0 RTM Release Notes](../release-notes/nuget-4.0-RTM.md) - Lists all the issues fixed for NuGet 4.0 RTM</span></span>

### <a name="features"></a><span data-ttu-id="07c3f-143">Funkce</span><span class="sxs-lookup"><span data-stu-id="07c3f-143">Features</span></span>

- <span data-ttu-id="07c3f-144">Zlepšit NuGet Obnovení Perf - Implementovat chytřejší NoOp pro obnovení příkazového řádku a VS - [#5080](https://github.com/NuGet/Home/issues/5080)</span><span class="sxs-lookup"><span data-stu-id="07c3f-144">Improve NuGet Restore Perf - Implement smarter NoOp for command line restores and VS - [#5080](https://github.com/NuGet/Home/issues/5080)</span></span>

- <span data-ttu-id="07c3f-145">NET Core 2.0: Rozhraní SE kontinuu VS/Dotnet CLI by mělo začít používat existující funkce NuGet: FallBack složky - [#4939](https://github.com/NuGet/Home/issues/4939)</span><span class="sxs-lookup"><span data-stu-id="07c3f-145">NET Core 2.0: VS/Dotnet CLI should start using existing NuGet functionality: FallBack folders - [#4939](https://github.com/NuGet/Home/issues/4939)</span></span>

- <span data-ttu-id="07c3f-146">NET Core 2.0: Umožněte uživatelům ignorovat konkrétní upozornění na obnovení (nebo zvýšit na chybu) - [#4898](https://github.com/NuGet/Home/issues/4898)</span><span class="sxs-lookup"><span data-stu-id="07c3f-146">NET Core 2.0: Enable users to ignore specific restore warnings (or elevate to error) - [#4898](https://github.com/NuGet/Home/issues/4898)</span></span>

- <span data-ttu-id="07c3f-147">NET Core 2.0: Lokalizovaná sestavení rozhraní SEkat - [#4896](https://github.com/NuGet/Home/issues/4896)</span><span class="sxs-lookup"><span data-stu-id="07c3f-147">NET Core 2.0: CLI localized assemblies - [#4896](https://github.com/NuGet/Home/issues/4896)</span></span>

- <span data-ttu-id="07c3f-148">NET Core 2.0: Zaregistrujte všechna upozornění/chyby do souboru datových zdrojů (včetně PackageTargetFallback) - [#4895](https://github.com/NuGet/Home/issues/4895)</span><span class="sxs-lookup"><span data-stu-id="07c3f-148">NET Core 2.0: register all warnings/errors to assets file (including PackageTargetFallback) - [#4895](https://github.com/NuGet/Home/issues/4895)</span></span>

- <span data-ttu-id="07c3f-149">Povolit podporu TFM: NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)</span><span class="sxs-lookup"><span data-stu-id="07c3f-149">Enable TFM support: NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)</span></span>

- <span data-ttu-id="07c3f-150">Snížit počet projektů NuGet.Core a NuGet.Client (a tedy knihovny DLL) - [#2446](https://github.com/NuGet/Home/issues/2446)</span><span class="sxs-lookup"><span data-stu-id="07c3f-150">Reduce the number of NuGet.Core and NuGet.Client projects (and thus DLLs) - [#2446](https://github.com/NuGet/Home/issues/2446)</span></span>

- <span data-ttu-id="07c3f-151">Přidat možnost označit nuget upozornění jako chyby - [#2395](https://github.com/NuGet/Home/issues/2395)</span><span class="sxs-lookup"><span data-stu-id="07c3f-151">Add ability to mark nuget warnings as errors - [#2395](https://github.com/NuGet/Home/issues/2395)</span></span>

### <a name="bugs"></a><span data-ttu-id="07c3f-152">Chyby</span><span class="sxs-lookup"><span data-stu-id="07c3f-152">Bugs</span></span>

- <span data-ttu-id="07c3f-153">msbuild /t:pack selže s parametrem "DevelopmentDependency" není podporován úlohou "PackTask" - [#5584](https://github.com/NuGet/Home/issues/5584)</span><span class="sxs-lookup"><span data-stu-id="07c3f-153">msbuild /t:pack fails with The "DevelopmentDependency" parameter is not supported by the "PackTask" task - [#5584](https://github.com/NuGet/Home/issues/5584)</span></span>

- <span data-ttu-id="07c3f-154">Adresářová struktura pro soubory obsahu byla slonována, pokud nepřidáte oddělovač adresářů systému Windows na konci programu PackagePath - [#4795](https://github.com/NuGet/Home/issues/4795)</span><span class="sxs-lookup"><span data-stu-id="07c3f-154">Directory structure for content files flattened if not adding Windows directory separator at the end of PackagePath - [#4795](https://github.com/NuGet/Home/issues/4795)</span></span>

- <span data-ttu-id="07c3f-155">netcore projekty nepodporují nastavení jako developmentDependency - [#4694](https://github.com/NuGet/Home/issues/4694)</span><span class="sxs-lookup"><span data-stu-id="07c3f-155">netcore projects don't support setting as developmentDependency - [#4694](https://github.com/NuGet/Home/issues/4694)</span></span>

- <span data-ttu-id="07c3f-156">RestoreManagerPackage načítají synchronně, který zablokoval vlákno uživatelského rozhraní a zablokování VS - [#4679](https://github.com/NuGet/Home/issues/4679)</span><span class="sxs-lookup"><span data-stu-id="07c3f-156">RestoreManagerPackage being loaded synchronously which blocked UI thread and deadlocked VS - [#4679](https://github.com/NuGet/Home/issues/4679)</span></span>

- <span data-ttu-id="07c3f-157">dotnet</span><span class="sxs-lookup"><span data-stu-id="07c3f-157">dotnet</span></span>
  - <span data-ttu-id="07c3f-158">dotnetcore Restore (& proto msbuild /t:restore) přeskočí projekty s explicitní míchanou závislostí [#4578](https://github.com/NuGet/Home/issues/4578)</span><span class="sxs-lookup"><span data-stu-id="07c3f-158">dotnetcore Restore (& therefore msbuild /t:restore) skips projects with an explicit solution project dependency [#4578](https://github.com/NuGet/Home/issues/4578)</span></span>

- <span data-ttu-id="07c3f-159">Pokud vaše řešení má odkazy na projekt, které odkazují na stejný projekt, s různými písmeny, obnovení nemusí fungovat.</span><span class="sxs-lookup"><span data-stu-id="07c3f-159">If your solution has projectreferences that refer to the same project, with different casing, restore may not work.</span></span> <span data-ttu-id="07c3f-160">To také ovlivňuje různé relativní cesty, bez rozdílu v pouzdře - [#4574](https://github.com/NuGet/Home/issues/4574)</span><span class="sxs-lookup"><span data-stu-id="07c3f-160">This also affects different relative paths, without a difference in casing - [#4574](https://github.com/NuGet/Home/issues/4574)</span></span>

- <span data-ttu-id="07c3f-161">Spustitelné soubory obnovené z balíčků NuGet již nejsou spustitelné s rozhraním .NET Core 2.0 - [#4424](https://github.com/NuGet/Home/issues/4424)</span><span class="sxs-lookup"><span data-stu-id="07c3f-161">Executables restored from NuGet packages are no longer executable with .NET Core 2.0 - [#4424](https://github.com/NuGet/Home/issues/4424)</span></span>

- <span data-ttu-id="07c3f-162">NuGet.exe vypolkne podrobnosti o výjimce při analýzě souboru řešení - [#4411](https://github.com/NuGet/Home/issues/4411)</span><span class="sxs-lookup"><span data-stu-id="07c3f-162">NuGet.exe swallows details of exception when parsing solution file - [#4411](https://github.com/NuGet/Home/issues/4411)</span></span>

- <span data-ttu-id="07c3f-163">Pack umístí soubory obsahu do nesprávného umístění, pokud ContentTargetFolders obsahuje cestu, která končí '/' v systému Windows - [#4407](https://github.com/NuGet/Home/issues/4407)</span><span class="sxs-lookup"><span data-stu-id="07c3f-163">Pack puts content files in wrong location if ContentTargetFolders contains a path that ends with '/' on Windows - [#4407](https://github.com/NuGet/Home/issues/4407)</span></span>

- <span data-ttu-id="07c3f-164">Nelze obnovit DotNetCliToolReference pro nástroje balíček, který se zaměřuje netcoreapp1.1 - [#4396](https://github.com/NuGet/Home/issues/4396)</span><span class="sxs-lookup"><span data-stu-id="07c3f-164">Can't restore a DotNetCliToolReference for a tools package that targets netcoreapp1.1 - [#4396](https://github.com/NuGet/Home/issues/4396)</span></span>

- <span data-ttu-id="07c3f-165">Cli aktualizace Nuget ponechá podmínku verze starého balíčku v souboru projektu (C++) - [#2449](https://github.com/NuGet/Home/issues/2449)</span><span class="sxs-lookup"><span data-stu-id="07c3f-165">Nuget update CLI leaves the old package version condition in project file (C++) - [#2449](https://github.com/NuGet/Home/issues/2449)</span></span>

### <a name="dcrs"></a><span data-ttu-id="07c3f-166">Řadiče domény</span><span class="sxs-lookup"><span data-stu-id="07c3f-166">DCRs</span></span>

- <span data-ttu-id="07c3f-167">Přečtěte si DotnetCliToolTargetFramework z cps nomation - [#5397](https://github.com/NuGet/Home/issues/5397)</span><span class="sxs-lookup"><span data-stu-id="07c3f-167">Read DotnetCliToolTargetFramework from CPS nomation - [#5397](https://github.com/NuGet/Home/issues/5397)</span></span>

- <span data-ttu-id="07c3f-168">Kontrola TPMinV by měla fungovat pro pj styl UPW - [#4763](https://github.com/NuGet/Home/issues/4763)</span><span class="sxs-lookup"><span data-stu-id="07c3f-168">TPMinV check should work for pj style UWP - [#4763](https://github.com/NuGet/Home/issues/4763)</span></span>

- <span data-ttu-id="07c3f-169">Zlepšit popis ui pro balíčky AutoReferenced - [#4471](https://github.com/NuGet/Home/issues/4471)</span><span class="sxs-lookup"><span data-stu-id="07c3f-169">Improve UI description for AutoReferenced packages - [#4471](https://github.com/NuGet/Home/issues/4471)</span></span>

- <span data-ttu-id="07c3f-170">NuGet obnovení je výběr dat kompilace z runtime oddílu.</span><span class="sxs-lookup"><span data-stu-id="07c3f-170">NuGet restore is selecting compile assets from runtime section.</span></span><span data-ttu-id="07c3f-171"> - [#4207](https://github.com/NuGet/Home/issues/4207)</span><span class="sxs-lookup"><span data-stu-id="07c3f-171"> - [#4207](https://github.com/NuGet/Home/issues/4207)</span></span>

- <span data-ttu-id="07c3f-172">Vložit diagnostiku závislostí do souboru zámku - [#1599](https://github.com/NuGet/Home/issues/1599)</span><span class="sxs-lookup"><span data-stu-id="07c3f-172">Put dependency diagnostics in the lock file - [#1599](https://github.com/NuGet/Home/issues/1599)</span></span>

## <a name="links-to-github-issues-fixed-in-43-rtm"></a><span data-ttu-id="07c3f-173">Odkazy na problémy GitHubu opravené v 4.3 RTM</span><span class="sxs-lookup"><span data-stu-id="07c3f-173">Links to GitHub issues fixed in 4.3 RTM</span></span>

[<span data-ttu-id="07c3f-174">Seznam problémů</span><span class="sxs-lookup"><span data-stu-id="07c3f-174">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.3")
