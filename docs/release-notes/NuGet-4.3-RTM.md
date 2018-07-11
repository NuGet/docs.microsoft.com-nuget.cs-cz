---
title: Poznámky k verzi 4.3 RTM NuGet
description: Poznámky k verzi pro NuGet 4.3 RTM, včetně známé problémy, opravy chyb, přidaných funkcí a chcete.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: cb44f47ef0b3bd086f0a681cb2fedc7c5afc42fa
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822653"
---
# <a name="nuget-43-rtm-release-notes"></a><span data-ttu-id="806a4-103">Poznámky k verzi 4.3 RTM NuGet</span><span class="sxs-lookup"><span data-stu-id="806a4-103">NuGet 4.3 RTM Release Notes</span></span>

<span data-ttu-id="806a4-104">[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) se dodává s NuGet 4.3 RTM, která přidává podporu pro nové scénáře, jako je například .NET Standard 2.0 nebo .NET Core 2.0, obsahuje opravy mnoha kvality a zvyšuje výkon.</span><span class="sxs-lookup"><span data-stu-id="806a4-104">[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.3 RTM which adds support for new scenarios such as .NET Standard 2.0/.NET Core 2.0, contains many quality fixes, and improves performance.</span></span> <span data-ttu-id="806a4-105">Tato verze přináší také několik vylepšení, jako je podpora pro sémantické verze 2.0.0, integrace nástroje MSBuild NuGet upozornění a chyb a další.</span><span class="sxs-lookup"><span data-stu-id="806a4-105">This release also brings several improvements like support for Semantic Versioning 2.0.0, MSBuild integration of NuGet warnings and errors, and more.</span></span>

## <a name="known-issues"></a><span data-ttu-id="806a4-106">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="806a4-106">Known issues</span></span>

### <a name="nuget-restore-may-treat-disabled-package-sources-as-enabled-in-some-cases"></a><span data-ttu-id="806a4-107">Při obnovení NuGet se v některých případech může se zakázanými zdroji balíčků zacházet, jako by byly povolené</span><span class="sxs-lookup"><span data-stu-id="806a4-107">NuGet restore may treat disabled package sources as enabled in some cases</span></span>

#### <a name="issue"></a><span data-ttu-id="806a4-108">Problém</span><span class="sxs-lookup"><span data-stu-id="806a4-108">Issue</span></span>

<span data-ttu-id="806a4-109">Následující obnovení příkazového řádku techniky považovat Zakázané balíčky zdroje jako povolené.</span><span class="sxs-lookup"><span data-stu-id="806a4-109">The following restore command-line techniques treat disabled packages sources as enabled.</span></span> [<span data-ttu-id="806a4-110">NuGet#5704</span><span class="sxs-lookup"><span data-stu-id="806a4-110">NuGet#5704</span></span>](https://github.com/NuGet/Home/issues/5704)
- `msbuild /t:restore`
- <span data-ttu-id="806a4-111">`dotnet restore` (buď pomocí dotnet.exe který se dodává s VS nebo ten, který se dodává s NetCore SDK 2.0.0)</span><span class="sxs-lookup"><span data-stu-id="806a4-111">`dotnet restore` (either with dotnet.exe that ships with VS, or the one that comes with NetCore SDK 2.0.0)</span></span>

#### <a name="workaround"></a><span data-ttu-id="806a4-112">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="806a4-112">Workaround</span></span>

1. <span data-ttu-id="806a4-113">Používejte Visual Studio ve verzi 2017 (sestavení 15.3 nebo novější) nebo nástroj NuGet.exe ve verzi 4.3.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="806a4-113">Use Visual Studio (2017 15.3 or later) or NuGet.exe (v4.3.0 or later)</span></span>
1. <span data-ttu-id="806a4-114">Zakázaný zdroj odstraňte a dál používejte příkazy msbuild nebo dotnet.exe.</span><span class="sxs-lookup"><span data-stu-id="806a4-114">Delete your disabled source and continue to use msbuild or dotnet.exe.</span></span>
1. <span data-ttu-id="806a4-115">Ve svém řešení můžete do konfigurace NuGet.config vložit element Clear a pak definovat zdroje potřebné v daném řešení.</span><span class="sxs-lookup"><span data-stu-id="806a4-115">For your solution, you could use "Clear" in NuGet.config and then define the sources necessary for that solution.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="806a4-116">Při používání konzoly Správce balíčků nemusí fungovat klávesa Enter</span><span class="sxs-lookup"><span data-stu-id="806a4-116">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="806a4-117">Problém</span><span class="sxs-lookup"><span data-stu-id="806a4-117">Issue</span></span>

<span data-ttu-id="806a4-118">V konzole Správce balíčků občas nefunguje klávesa Enter.</span><span class="sxs-lookup"><span data-stu-id="806a4-118">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="806a4-119">Když toto chování zpozorujete, zjistěte prosím, jak to vypadá s opravou, a poskytněte jakékoli další užitečné informace o postupu, jak tuto chybu reprodukovat.</span><span class="sxs-lookup"><span data-stu-id="806a4-119">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="806a4-120">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="806a4-120">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="806a4-121">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="806a4-121">Workaround</span></span>

<span data-ttu-id="806a4-122">Před otevřením řešení restartujte Visual Studio a otevřete konzolu PMC.</span><span class="sxs-lookup"><span data-stu-id="806a4-122">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="806a4-123">Případně, zkuste odstranit `project.lock.json` a opakujte obnovení.</span><span class="sxs-lookup"><span data-stu-id="806a4-123">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="806a4-124">Nelze zobrazit, přidat nebo aktualizovat DotNetCLITools pomocí Správce balíčků Nuget</span><span class="sxs-lookup"><span data-stu-id="806a4-124">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="806a4-125">Problém</span><span class="sxs-lookup"><span data-stu-id="806a4-125">Issue</span></span>

<span data-ttu-id="806a4-126">Správce balíčků NuGet nezobrazuje a nepovoluje přidat nebo aktualizovat DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="806a4-126">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="806a4-127">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="806a4-127">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="806a4-128">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="806a4-128">Workaround</span></span>

<span data-ttu-id="806a4-129">V souboru projektu se musí ručně upravit DotNetCLIToolReferences.</span><span class="sxs-lookup"><span data-stu-id="806a4-129">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="806a4-130">Změna cílení cílové verze rozhraní může vést k nekompletnímu IntelliSense</span><span class="sxs-lookup"><span data-stu-id="806a4-130">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="806a4-131">Problém</span><span class="sxs-lookup"><span data-stu-id="806a4-131">Issue</span></span>

<span data-ttu-id="806a4-132">Změna cílení cílové verze rozhraní v sadě Visual Studio může vést k nekompletnímu IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="806a4-132">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="806a4-133">To se stává, když jako formát správce balíčků používáte PackageReferences.</span><span class="sxs-lookup"><span data-stu-id="806a4-133">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="806a4-134">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="806a4-134">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="806a4-135">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="806a4-135">Workaround</span></span>

<span data-ttu-id="806a4-136">Proveďte ruční obnovení.</span><span class="sxs-lookup"><span data-stu-id="806a4-136">Do a manual restore.</span></span>

## <a name="issues-fixed-in-nuget-43-rtm-timeframe"></a><span data-ttu-id="806a4-137">Chyby v období NuGet 4.3 RTM</span><span class="sxs-lookup"><span data-stu-id="806a4-137">Issues fixed in NuGet 4.3 RTM timeframe</span></span>

<span data-ttu-id="806a4-138">[K vydání verze RTM 4.0 NuGet](../release-notes/nuget-4.0-RTM.md) -jsou uvedené všechny problémy opravě pro NuGet 4.0 RTM</span><span class="sxs-lookup"><span data-stu-id="806a4-138">[NuGet 4.0 RTM Release Notes](../release-notes/nuget-4.0-RTM.md) - Lists all the issues fixed for NuGet 4.0 RTM</span></span>

### <a name="features"></a><span data-ttu-id="806a4-139">Funkce</span><span class="sxs-lookup"><span data-stu-id="806a4-139">Features</span></span>

- <span data-ttu-id="806a4-140">Zlepšení výkonu obnovení NuGet - implementace chytřejší nedojde k žádné akci pro obnovení příkazového řádku - a VS [#5080](https://github.com/NuGet/Home/issues/5080)</span><span class="sxs-lookup"><span data-stu-id="806a4-140">Improve NuGet Restore Perf - Implement smarter NoOp for command line restores and VS - [#5080](https://github.com/NuGet/Home/issues/5080)</span></span>

- <span data-ttu-id="806a4-141">Jádro Asp.net 2.0: Produkt VS/Dotnet rozhraní příkazového řádku by se měl spustit pomocí stávajících funkcí NuGet: záložní složky - [#4939](https://github.com/NuGet/Home/issues/4939)</span><span class="sxs-lookup"><span data-stu-id="806a4-141">NET Core 2.0: VS/Dotnet CLI should start using existing NuGet functionality: FallBack folders - [#4939](https://github.com/NuGet/Home/issues/4939)</span></span>

- <span data-ttu-id="806a4-142">Jádro Asp.net 2.0: Povolit uživatelům ignorovat upozornění konkrétní obnovení (nebo zvýšení oprávnění na chybu) - [#4898](https://github.com/NuGet/Home/issues/4898)</span><span class="sxs-lookup"><span data-stu-id="806a4-142">NET Core 2.0: Enable users to ignore specific restore warnings (or elevate to error) - [#4898](https://github.com/NuGet/Home/issues/4898)</span></span>

- <span data-ttu-id="806a4-143">Jádro Asp.net 2.0: Rozhraní příkazového řádku lokalizované sestavení - [#4896](https://github.com/NuGet/Home/issues/4896)</span><span class="sxs-lookup"><span data-stu-id="806a4-143">NET Core 2.0: CLI localized assemblies - [#4896](https://github.com/NuGet/Home/issues/4896)</span></span>

- <span data-ttu-id="806a4-144">Jádro Asp.net 2.0: registrace všech upozornění nebo chyby do souboru prostředků (včetně PackageTargetFallback) - [#4895](https://github.com/NuGet/Home/issues/4895)</span><span class="sxs-lookup"><span data-stu-id="806a4-144">NET Core 2.0: register all warnings/errors to assets file (including PackageTargetFallback) - [#4895](https://github.com/NuGet/Home/issues/4895)</span></span>

- <span data-ttu-id="806a4-145">Povolit podporu TFM: NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)</span><span class="sxs-lookup"><span data-stu-id="806a4-145">Enable TFM support: NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)</span></span>

- <span data-ttu-id="806a4-146">Snižte počet NuGet.Core a NuGet.Client projekty (a tedy knihovny DLL) - [#2446](https://github.com/NuGet/Home/issues/2446)</span><span class="sxs-lookup"><span data-stu-id="806a4-146">Reduce the number of NuGet.Core and NuGet.Client projects (and thus DLLs) - [#2446](https://github.com/NuGet/Home/issues/2446)</span></span>

- <span data-ttu-id="806a4-147">Přidat možnost označte nuget upozornění jako chyby – [#2395](https://github.com/NuGet/Home/issues/2395)</span><span class="sxs-lookup"><span data-stu-id="806a4-147">Add ability to mark nuget warnings as errors - [#2395](https://github.com/NuGet/Home/issues/2395)</span></span>

### <a name="bugs"></a><span data-ttu-id="806a4-148">Chyby</span><span class="sxs-lookup"><span data-stu-id="806a4-148">Bugs</span></span>

- <span data-ttu-id="806a4-149">není podporována selže /t:pack MSBuild s parametrem "DevelopmentDependency" úloha "PackTask" - [#5584](https://github.com/NuGet/Home/issues/5584)</span><span class="sxs-lookup"><span data-stu-id="806a4-149">msbuild /t:pack fails with The "DevelopmentDependency" parameter is not supported by the "PackTask" task - [#5584](https://github.com/NuGet/Home/issues/5584)</span></span>

- <span data-ttu-id="806a4-150">Průmětu struktury adresářů pro soubory obsahu, pokud nebudou přidány oddělovače adresáře systému Windows na konci PackagePath - [#4795](https://github.com/NuGet/Home/issues/4795)</span><span class="sxs-lookup"><span data-stu-id="806a4-150">Directory structure for content files flattened if not adding Windows directory separator at the end of PackagePath - [#4795](https://github.com/NuGet/Home/issues/4795)</span></span>

- <span data-ttu-id="806a4-151">projekty netcore nepodporují nastavení jako developmentDependency - [#4694](https://github.com/NuGet/Home/issues/4694)</span><span class="sxs-lookup"><span data-stu-id="806a4-151">netcore projects don't support setting as developmentDependency - [#4694](https://github.com/NuGet/Home/issues/4694)</span></span>

- <span data-ttu-id="806a4-152">RestoreManagerPackage načítá synchronně který blokovaný vlákna uživatelského rozhraní a zablokována VS - [#4679](https://github.com/NuGet/Home/issues/4679)</span><span class="sxs-lookup"><span data-stu-id="806a4-152">RestoreManagerPackage being loaded synchronously which blocked UI thread and deadlocked VS - [#4679](https://github.com/NuGet/Home/issues/4679)</span></span>

- <span data-ttu-id="806a4-153">DotNet.</span><span class="sxs-lookup"><span data-stu-id="806a4-153">dotnet</span></span>
  - <span data-ttu-id="806a4-154">dotnetcore obnovení (& proto msbuild /t:restore) přeskočí projekty s závislosti projektu explicitní řešení [#4578](https://github.com/NuGet/Home/issues/4578)</span><span class="sxs-lookup"><span data-stu-id="806a4-154">dotnetcore Restore (& therefore msbuild /t:restore) skips projects with an explicit solution project dependency [#4578](https://github.com/NuGet/Home/issues/4578)</span></span>

- <span data-ttu-id="806a4-155">Pokud má vaše řešení projectreferences, která odkazují na stejný projekt v různých velká a malá písmena, nemusí obnovení fungovat.</span><span class="sxs-lookup"><span data-stu-id="806a4-155">If your solution has projectreferences that refer to the same project, with different casing, restore may not work.</span></span> <span data-ttu-id="806a4-156">To ovlivní také různé relativní cesty bez rozdíl v velká a malá písmena - [#4574](https://github.com/NuGet/Home/issues/4574)</span><span class="sxs-lookup"><span data-stu-id="806a4-156">This also affects different relative paths, without a difference in casing - [#4574](https://github.com/NuGet/Home/issues/4574)</span></span>

- <span data-ttu-id="806a4-157">Spustitelné soubory obnovení ze balíčky NuGet jsou již spustitelný soubor s .NET Core 2.0 - [#4424](https://github.com/NuGet/Home/issues/4424)</span><span class="sxs-lookup"><span data-stu-id="806a4-157">Executables restored from NuGet packages are no longer executable with .NET Core 2.0 - [#4424](https://github.com/NuGet/Home/issues/4424)</span></span>

- <span data-ttu-id="806a4-158">NuGet.exe swallows podrobnosti o výjimce, při analýze souboru řešení - [#4411](https://github.com/NuGet/Home/issues/4411)</span><span class="sxs-lookup"><span data-stu-id="806a4-158">NuGet.exe swallows details of exception when parsing solution file - [#4411](https://github.com/NuGet/Home/issues/4411)</span></span>

- <span data-ttu-id="806a4-159">Pack převádí soubory obsahu na nesprávné umístění, pokud ContentTargetFolders obsahuje cestu, která ukončí lomítkem (/) v systému Windows - [#4407](https://github.com/NuGet/Home/issues/4407)</span><span class="sxs-lookup"><span data-stu-id="806a4-159">Pack puts content files in wrong location if ContentTargetFolders contains a path that ends with '/' on Windows - [#4407](https://github.com/NuGet/Home/issues/4407)</span></span>

- <span data-ttu-id="806a4-160">Nelze obnovit DotNetCliToolReference nástrojů balíčků tohoto cíle netcoreapp1.1 - [#4396](https://github.com/NuGet/Home/issues/4396)</span><span class="sxs-lookup"><span data-stu-id="806a4-160">Can't restore a DotNetCliToolReference for a tools package that targets netcoreapp1.1 - [#4396](https://github.com/NuGet/Home/issues/4396)</span></span>

- <span data-ttu-id="806a4-161">Aktualizace Nuget rozhraní příkazového řádku ponechá starý stav verze balíčku v souboru projektu (C++) - [#2449](https://github.com/NuGet/Home/issues/2449)</span><span class="sxs-lookup"><span data-stu-id="806a4-161">Nuget update CLI leaves the old package version condition in project file (C++) - [#2449](https://github.com/NuGet/Home/issues/2449)</span></span>

### <a name="dcrs"></a><span data-ttu-id="806a4-162">Chcete</span><span class="sxs-lookup"><span data-stu-id="806a4-162">DCRs</span></span>

- <span data-ttu-id="806a4-163">Čtení DotnetCliToolTargetFramework z CPS nomation - [#5397](https://github.com/NuGet/Home/issues/5397)</span><span class="sxs-lookup"><span data-stu-id="806a4-163">Read DotnetCliToolTargetFramework from CPS nomation - [#5397](https://github.com/NuGet/Home/issues/5397)</span></span>

- <span data-ttu-id="806a4-164">Kontrola TPMinV by měla fungovat pro styl pj UWP - [#4763](https://github.com/NuGet/Home/issues/4763)</span><span class="sxs-lookup"><span data-stu-id="806a4-164">TPMinV check should work for pj style UWP - [#4763](https://github.com/NuGet/Home/issues/4763)</span></span>

- <span data-ttu-id="806a4-165">Zlepšení uživatelského rozhraní Popis balíčků AutoReferenced - [#4471](https://github.com/NuGet/Home/issues/4471)</span><span class="sxs-lookup"><span data-stu-id="806a4-165">Improve UI description for AutoReferenced packages - [#4471](https://github.com/NuGet/Home/issues/4471)</span></span>

- <span data-ttu-id="806a4-166">Obnovení NuGet je výběr kompilace prostředky z části modulu runtime.</span><span class="sxs-lookup"><span data-stu-id="806a4-166">NuGet restore is selecting compile assets from runtime section.</span></span><span data-ttu-id="806a4-167"> - [#4207](https://github.com/NuGet/Home/issues/4207)</span><span class="sxs-lookup"><span data-stu-id="806a4-167"> - [#4207](https://github.com/NuGet/Home/issues/4207)</span></span>

- <span data-ttu-id="806a4-168">Uveďte Diagnostika závislostí v souboru zámku - [#1599](https://github.com/NuGet/Home/issues/1599)</span><span class="sxs-lookup"><span data-stu-id="806a4-168">Put dependency diagnostics in the lock file - [#1599](https://github.com/NuGet/Home/issues/1599)</span></span>

## <a name="links-to-github-issues-fixed-in-43-rtm"></a><span data-ttu-id="806a4-169">Odkazy na Githubu chyby v 4.3 RTM</span><span class="sxs-lookup"><span data-stu-id="806a4-169">Links to GitHub issues fixed in 4.3 RTM</span></span>

[<span data-ttu-id="806a4-170">Seznam problémů</span><span class="sxs-lookup"><span data-stu-id="806a4-170">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.3")