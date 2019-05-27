---
title: Zpráva k vydání verze NuGet 4.3 RTM
description: Zpráva k vydání verze pro NuGet 4.3 RTM, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 4bee32995884f4c003ebb963d2fd5b2d04363bab
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551621"
---
# <a name="nuget-43-rtm-release-notes"></a><span data-ttu-id="48084-103">Zpráva k vydání verze NuGet 4.3 RTM</span><span class="sxs-lookup"><span data-stu-id="48084-103">NuGet 4.3 RTM Release Notes</span></span>

<span data-ttu-id="48084-104">[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) se dodává s NuGet 4.3 RTM, který přidává podporu pro nové scénáře, jako například .NET Standard 2.0 a .NET Core 2.0, obsahuje řadu oprav kvality a zvyšuje výkon.</span><span class="sxs-lookup"><span data-stu-id="48084-104">[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.3 RTM which adds support for new scenarios such as .NET Standard 2.0/.NET Core 2.0, contains many quality fixes, and improves performance.</span></span> <span data-ttu-id="48084-105">Tato verze také přináší několik vylepšení jako podporu pro Semantic Versioning 2.0.0, integrace MSBuild NuGet upozornění a chyby a další.</span><span class="sxs-lookup"><span data-stu-id="48084-105">This release also brings several improvements like support for Semantic Versioning 2.0.0, MSBuild integration of NuGet warnings and errors, and more.</span></span>

## <a name="known-issues"></a><span data-ttu-id="48084-106">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="48084-106">Known issues</span></span>

### <a name="nuget-restore-may-treat-disabled-package-sources-as-enabled-in-some-cases"></a><span data-ttu-id="48084-107">Při obnovení NuGet se v některých případech může se zakázanými zdroji balíčků zacházet, jako by byly povolené</span><span class="sxs-lookup"><span data-stu-id="48084-107">NuGet restore may treat disabled package sources as enabled in some cases</span></span>

#### <a name="issue"></a><span data-ttu-id="48084-108">Problém</span><span class="sxs-lookup"><span data-stu-id="48084-108">Issue</span></span>

<span data-ttu-id="48084-109">Následující postupy obnovení příkazového řádku s zdroji balíčků zacházet, jako povolené.</span><span class="sxs-lookup"><span data-stu-id="48084-109">The following restore command-line techniques treat disabled packages sources as enabled.</span></span> [<span data-ttu-id="48084-110">NuGet#5704</span><span class="sxs-lookup"><span data-stu-id="48084-110">NuGet#5704</span></span>](https://github.com/NuGet/Home/issues/5704)
- `msbuild /t:restore`
- <span data-ttu-id="48084-111">`dotnet restore` (buď s příkazem VS dotnet.exe nebo ten, který je součástí sady NetCore SDK 2.0.0)</span><span class="sxs-lookup"><span data-stu-id="48084-111">`dotnet restore` (either with dotnet.exe that ships with VS, or the one that comes with NetCore SDK 2.0.0)</span></span>

#### <a name="workaround"></a><span data-ttu-id="48084-112">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="48084-112">Workaround</span></span>

1. <span data-ttu-id="48084-113">Používejte Visual Studio ve verzi 2017 (sestavení 15.3 nebo novější) nebo nástroj NuGet.exe ve verzi 4.3.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="48084-113">Use Visual Studio (2017 15.3 or later) or NuGet.exe (v4.3.0 or later)</span></span>
1. <span data-ttu-id="48084-114">Zakázaný zdroj odstraňte a dál používejte příkazy msbuild nebo dotnet.exe.</span><span class="sxs-lookup"><span data-stu-id="48084-114">Delete your disabled source and continue to use msbuild or dotnet.exe.</span></span>
1. <span data-ttu-id="48084-115">Ve svém řešení můžete do konfigurace NuGet.config vložit element Clear a pak definovat zdroje potřebné v daném řešení.</span><span class="sxs-lookup"><span data-stu-id="48084-115">For your solution, you could use "Clear" in NuGet.config and then define the sources necessary for that solution.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="48084-116">Při používání konzoly Správce balíčků nemusí fungovat klávesa Enter</span><span class="sxs-lookup"><span data-stu-id="48084-116">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="48084-117">Problém</span><span class="sxs-lookup"><span data-stu-id="48084-117">Issue</span></span>

<span data-ttu-id="48084-118">V konzole Správce balíčků občas nefunguje klávesa Enter.</span><span class="sxs-lookup"><span data-stu-id="48084-118">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="48084-119">Když toto chování zpozorujete, zjistěte prosím, jak to vypadá s opravou, a poskytněte jakékoli další užitečné informace o postupu, jak tuto chybu reprodukovat.</span><span class="sxs-lookup"><span data-stu-id="48084-119">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="48084-120">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="48084-120">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="48084-121">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="48084-121">Workaround</span></span>

<span data-ttu-id="48084-122">Před otevřením řešení restartujte Visual Studio a otevřete konzolu PMC.</span><span class="sxs-lookup"><span data-stu-id="48084-122">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="48084-123">Alternativně můžete zkusit odstranění `project.lock.json` a znovu ho obnovit.</span><span class="sxs-lookup"><span data-stu-id="48084-123">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="48084-124">Nejde zobrazit, přidat ani aktualizovat DotNetCLITools pomocí Správce balíčků Nuget</span><span class="sxs-lookup"><span data-stu-id="48084-124">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="48084-125">Problém</span><span class="sxs-lookup"><span data-stu-id="48084-125">Issue</span></span>

<span data-ttu-id="48084-126">Správce balíčků NuGet nezobrazuje a nepovoluje přidat nebo aktualizovat DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="48084-126">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="48084-127">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="48084-127">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="48084-128">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="48084-128">Workaround</span></span>

<span data-ttu-id="48084-129">V souboru projektu se musí ručně upravit DotNetCLIToolReferences.</span><span class="sxs-lookup"><span data-stu-id="48084-129">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="48084-130">Změna cílení verze cílové architektury může vést k nekompletnímu IntelliSense</span><span class="sxs-lookup"><span data-stu-id="48084-130">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="48084-131">Problém</span><span class="sxs-lookup"><span data-stu-id="48084-131">Issue</span></span>

<span data-ttu-id="48084-132">Změna cílení verze cílové architektury v sadě Visual Studio může vést k nekompletnímu IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="48084-132">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="48084-133">To se stává, když jako formát správce balíčků používáte PackageReferences.</span><span class="sxs-lookup"><span data-stu-id="48084-133">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="48084-134">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="48084-134">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="48084-135">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="48084-135">Workaround</span></span>

<span data-ttu-id="48084-136">Proveďte ruční obnovení.</span><span class="sxs-lookup"><span data-stu-id="48084-136">Do a manual restore.</span></span>

## <a name="issues-fixed-in-nuget-43-rtm-timeframe"></a><span data-ttu-id="48084-137">Problémy opravené ve verzi RTM 4.3 NuGet časový rámec</span><span class="sxs-lookup"><span data-stu-id="48084-137">Issues fixed in NuGet 4.3 RTM timeframe</span></span>

<span data-ttu-id="48084-138">[4.0 RTM poznámkách k verzi NuGet](../release-notes/nuget-4.0-RTM.md) – zobrazí seznam všech problémů stanovené pro NuGet 4.0 RTM</span><span class="sxs-lookup"><span data-stu-id="48084-138">[NuGet 4.0 RTM Release Notes](../release-notes/nuget-4.0-RTM.md) - Lists all the issues fixed for NuGet 4.0 RTM</span></span>

### <a name="features"></a><span data-ttu-id="48084-139">Funkce</span><span class="sxs-lookup"><span data-stu-id="48084-139">Features</span></span>

- <span data-ttu-id="48084-140">Zlepšení výkonu obnovení NuGet - chytřejší NoOp pro implementace pro obnovení příkazového řádku – a VS [#5080](https://github.com/NuGet/Home/issues/5080)</span><span class="sxs-lookup"><span data-stu-id="48084-140">Improve NuGet Restore Perf - Implement smarter NoOp for command line restores and VS - [#5080](https://github.com/NuGet/Home/issues/5080)</span></span>

- <span data-ttu-id="48084-141">.NET Core 2.0: Rozhraní příkazového řádku Dotnet/VS by měla začít používat existující funkce NuGet: záložní složky – [#4939](https://github.com/NuGet/Home/issues/4939)</span><span class="sxs-lookup"><span data-stu-id="48084-141">NET Core 2.0: VS/Dotnet CLI should start using existing NuGet functionality: FallBack folders - [#4939](https://github.com/NuGet/Home/issues/4939)</span></span>

- <span data-ttu-id="48084-142">.NET Core 2.0: Uživatelům umožnit ignorovat upozornění na konkrétní obnovení (nebo zvýšení oprávnění na chybu) - [#4898](https://github.com/NuGet/Home/issues/4898)</span><span class="sxs-lookup"><span data-stu-id="48084-142">NET Core 2.0: Enable users to ignore specific restore warnings (or elevate to error) - [#4898](https://github.com/NuGet/Home/issues/4898)</span></span>

- <span data-ttu-id="48084-143">.NET Core 2.0: Rozhraní příkazového řádku lokalizované sestavení - [#4896](https://github.com/NuGet/Home/issues/4896)</span><span class="sxs-lookup"><span data-stu-id="48084-143">NET Core 2.0: CLI localized assemblies - [#4896](https://github.com/NuGet/Home/issues/4896)</span></span>

- <span data-ttu-id="48084-144">.NET Core 2.0: zaregistrovat všechna upozornění nebo chyby do souboru prostředků (včetně PackageTargetFallback) - [#4895](https://github.com/NuGet/Home/issues/4895)</span><span class="sxs-lookup"><span data-stu-id="48084-144">NET Core 2.0: register all warnings/errors to assets file (including PackageTargetFallback) - [#4895](https://github.com/NuGet/Home/issues/4895)</span></span>

- <span data-ttu-id="48084-145">Povolit podporu TFM: NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)</span><span class="sxs-lookup"><span data-stu-id="48084-145">Enable TFM support: NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)</span></span>

- <span data-ttu-id="48084-146">Snižte počet NuGet.Core NuGet.Client projekty (a tedy knihovny DLL) - [#2446](https://github.com/NuGet/Home/issues/2446)</span><span class="sxs-lookup"><span data-stu-id="48084-146">Reduce the number of NuGet.Core and NuGet.Client projects (and thus DLLs) - [#2446](https://github.com/NuGet/Home/issues/2446)</span></span>

- <span data-ttu-id="48084-147">Přidat možnost označit nuget upozornění jako chyby – [#2395](https://github.com/NuGet/Home/issues/2395)</span><span class="sxs-lookup"><span data-stu-id="48084-147">Add ability to mark nuget warnings as errors - [#2395](https://github.com/NuGet/Home/issues/2395)</span></span>

### <a name="bugs"></a><span data-ttu-id="48084-148">Chyby</span><span class="sxs-lookup"><span data-stu-id="48084-148">Bugs</span></span>

- <span data-ttu-id="48084-149">selže /t:pack MSBuild s parametrem "DevelopmentDependency" nepodporuje úlohou "Packtask se neposkytl" - [#5584](https://github.com/NuGet/Home/issues/5584)</span><span class="sxs-lookup"><span data-stu-id="48084-149">msbuild /t:pack fails with The "DevelopmentDependency" parameter is not supported by the "PackTask" task - [#5584](https://github.com/NuGet/Home/issues/5584)</span></span>

- <span data-ttu-id="48084-150">Plochý adresářovou strukturu souborů obsahu není na konci PackagePath – přidávání oddělovač adresářů Windows [#4795](https://github.com/NuGet/Home/issues/4795)</span><span class="sxs-lookup"><span data-stu-id="48084-150">Directory structure for content files flattened if not adding Windows directory separator at the end of PackagePath - [#4795](https://github.com/NuGet/Home/issues/4795)</span></span>

- <span data-ttu-id="48084-151">projekty netcore nepodporují nastavení jako developmentDependency - [#4694](https://github.com/NuGet/Home/issues/4694)</span><span class="sxs-lookup"><span data-stu-id="48084-151">netcore projects don't support setting as developmentDependency - [#4694](https://github.com/NuGet/Home/issues/4694)</span></span>

- <span data-ttu-id="48084-152">RestoreManagerPackage načítání synchronně který blokovaná vlákna uživatelského rozhraní a zablokována VS - [#4679](https://github.com/NuGet/Home/issues/4679)</span><span class="sxs-lookup"><span data-stu-id="48084-152">RestoreManagerPackage being loaded synchronously which blocked UI thread and deadlocked VS - [#4679](https://github.com/NuGet/Home/issues/4679)</span></span>

- <span data-ttu-id="48084-153">DotNet</span><span class="sxs-lookup"><span data-stu-id="48084-153">dotnet</span></span>
  - <span data-ttu-id="48084-154">dotnetcore obnovení (a tedy msbuild/t: Restore) přeskočí projekty se závislostí projektu řešení explicitní [#4578](https://github.com/NuGet/Home/issues/4578)</span><span class="sxs-lookup"><span data-stu-id="48084-154">dotnetcore Restore (& therefore msbuild /t:restore) skips projects with an explicit solution project dependency [#4578](https://github.com/NuGet/Home/issues/4578)</span></span>

- <span data-ttu-id="48084-155">Pokud má vaše řešení projectreferences má za následek odkazují na stejný projekt s jinou velikostí písmen, obnovení nemusí fungovat.</span><span class="sxs-lookup"><span data-stu-id="48084-155">If your solution has projectreferences that refer to the same project, with different casing, restore may not work.</span></span> <span data-ttu-id="48084-156">To ovlivňuje také jinými relativními cestami, bez rozdílu v malých a velkých písmen - [#4574](https://github.com/NuGet/Home/issues/4574)</span><span class="sxs-lookup"><span data-stu-id="48084-156">This also affects different relative paths, without a difference in casing - [#4574](https://github.com/NuGet/Home/issues/4574)</span></span>

- <span data-ttu-id="48084-157">Spustitelné soubory obnovit z balíčků NuGet už nejsou spustitelný soubor s .NET Core 2.0 - [#4424](https://github.com/NuGet/Home/issues/4424)</span><span class="sxs-lookup"><span data-stu-id="48084-157">Executables restored from NuGet packages are no longer executable with .NET Core 2.0 - [#4424](https://github.com/NuGet/Home/issues/4424)</span></span>

- <span data-ttu-id="48084-158">NuGet.exe pohltila podrobnosti o výjimce při analýze souboru řešení - [#4411](https://github.com/NuGet/Home/issues/4411)</span><span class="sxs-lookup"><span data-stu-id="48084-158">NuGet.exe swallows details of exception when parsing solution file - [#4411](https://github.com/NuGet/Home/issues/4411)</span></span>

- <span data-ttu-id="48084-159">Pack umístí soubory obsahu v nesprávném umístění, pokud ContentTargetFolders obsahuje cestu, která skončí s lomítkem (/) ve Windows – [#4407](https://github.com/NuGet/Home/issues/4407)</span><span class="sxs-lookup"><span data-stu-id="48084-159">Pack puts content files in wrong location if ContentTargetFolders contains a path that ends with '/' on Windows - [#4407](https://github.com/NuGet/Home/issues/4407)</span></span>

- <span data-ttu-id="48084-160">Nelze obnovit DotNetCliToolReference nástroje balíčků tohoto cíle netcoreapp1.1 - [#4396](https://github.com/NuGet/Home/issues/4396)</span><span class="sxs-lookup"><span data-stu-id="48084-160">Can't restore a DotNetCliToolReference for a tools package that targets netcoreapp1.1 - [#4396](https://github.com/NuGet/Home/issues/4396)</span></span>

- <span data-ttu-id="48084-161">Aktualizace rozhraní příkazového řádku Nuget opustí podmínka staré verze balíčku v souboru projektu (C++) - [#2449](https://github.com/NuGet/Home/issues/2449)</span><span class="sxs-lookup"><span data-stu-id="48084-161">Nuget update CLI leaves the old package version condition in project file (C++) - [#2449](https://github.com/NuGet/Home/issues/2449)</span></span>

### <a name="dcrs"></a><span data-ttu-id="48084-162">Chcete</span><span class="sxs-lookup"><span data-stu-id="48084-162">DCRs</span></span>

- <span data-ttu-id="48084-163">Čtení DotnetCliToolTargetFramework z CPS nomation - [#5397](https://github.com/NuGet/Home/issues/5397)</span><span class="sxs-lookup"><span data-stu-id="48084-163">Read DotnetCliToolTargetFramework from CPS nomation - [#5397](https://github.com/NuGet/Home/issues/5397)</span></span>

- <span data-ttu-id="48084-164">Kontrola TPMinV by mělo fungovat pro styl pj UPW – [#4763](https://github.com/NuGet/Home/issues/4763)</span><span class="sxs-lookup"><span data-stu-id="48084-164">TPMinV check should work for pj style UWP - [#4763](https://github.com/NuGet/Home/issues/4763)</span></span>

- <span data-ttu-id="48084-165">Vylepšení uživatelského rozhraní Popis balíčků AutoReferenced - [#4471](https://github.com/NuGet/Home/issues/4471)</span><span class="sxs-lookup"><span data-stu-id="48084-165">Improve UI description for AutoReferenced packages - [#4471](https://github.com/NuGet/Home/issues/4471)</span></span>

- <span data-ttu-id="48084-166">Obnovení NuGet je výběr kompilace prostředků z části modulu runtime.</span><span class="sxs-lookup"><span data-stu-id="48084-166">NuGet restore is selecting compile assets from runtime section.</span></span><span data-ttu-id="48084-167"> - [#4207](https://github.com/NuGet/Home/issues/4207)</span><span class="sxs-lookup"><span data-stu-id="48084-167"> - [#4207](https://github.com/NuGet/Home/issues/4207)</span></span>

- <span data-ttu-id="48084-168">Diagnostika závislostí do souboru zámku - [#1599](https://github.com/NuGet/Home/issues/1599)</span><span class="sxs-lookup"><span data-stu-id="48084-168">Put dependency diagnostics in the lock file - [#1599](https://github.com/NuGet/Home/issues/1599)</span></span>

## <a name="links-to-github-issues-fixed-in-43-rtm"></a><span data-ttu-id="48084-169">Odkazy na Githubu opravených chybách v 4.3 RTM</span><span class="sxs-lookup"><span data-stu-id="48084-169">Links to GitHub issues fixed in 4.3 RTM</span></span>

[<span data-ttu-id="48084-170">Seznam problémů</span><span class="sxs-lookup"><span data-stu-id="48084-170">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.3")
