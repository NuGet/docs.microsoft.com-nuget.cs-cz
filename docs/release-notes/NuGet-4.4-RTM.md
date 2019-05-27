---
title: Zpráva k vydání verze NuGet 4.4 RTM
description: Zpráva k vydání verze pro NuGet 4.3 RTM, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 9ea11ad5476b02940b171fdc69ac0bf56598418d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548411"
---
# <a name="nuget-44-rtm-release-notes"></a><span data-ttu-id="7ce7c-103">Zpráva k vydání verze NuGet 4.4 RTM</span><span class="sxs-lookup"><span data-stu-id="7ce7c-103">NuGet 4.4 RTM Release Notes</span></span>

<span data-ttu-id="7ce7c-104">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) se dodává s NuGet 4.4 RTM.</span><span class="sxs-lookup"><span data-stu-id="7ce7c-104">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.4 RTM.</span></span>

## <a name="known-issues"></a><span data-ttu-id="7ce7c-105">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="7ce7c-105">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="7ce7c-106">Problémy s .NET Standard 2.0 pomocí rozhraní .NET Framework a NuGet</span><span class="sxs-lookup"><span data-stu-id="7ce7c-106">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="7ce7c-107">.NET standard a jeho nástroje je navržená tak, že projekty cílené na rozhraní .NET Framework 4.6.1 může spotřebovat balíčky NuGet & projekty cílené na .NET Standard 2.0 nebo dřívější.</span><span class="sxs-lookup"><span data-stu-id="7ce7c-107">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="7ce7c-108">[Tento dokument](https://github.com/dotnet/standard/issues/481) shrnuje problémy kolem tohoto scénáře plánu pro účely řešení a alternativní řešení můžete nasadit s dnešní stavu nástrojů.</span><span class="sxs-lookup"><span data-stu-id="7ce7c-108">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="7ce7c-109">Při používání konzoly Správce balíčků nemusí fungovat klávesa Enter</span><span class="sxs-lookup"><span data-stu-id="7ce7c-109">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="7ce7c-110">Problém</span><span class="sxs-lookup"><span data-stu-id="7ce7c-110">Issue</span></span>

<span data-ttu-id="7ce7c-111">V konzole Správce balíčků občas nefunguje klávesa Enter.</span><span class="sxs-lookup"><span data-stu-id="7ce7c-111">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="7ce7c-112">Když toto chování zpozorujete, zjistěte prosím, jak to vypadá s opravou, a poskytněte jakékoli další užitečné informace o postupu, jak tuto chybu reprodukovat.</span><span class="sxs-lookup"><span data-stu-id="7ce7c-112">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="7ce7c-113">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-113">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="7ce7c-114">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="7ce7c-114">Workaround</span></span>

<span data-ttu-id="7ce7c-115">Před otevřením řešení restartujte Visual Studio a otevřete konzolu PMC.</span><span class="sxs-lookup"><span data-stu-id="7ce7c-115">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="7ce7c-116">Alternativně můžete zkusit odstranění `project.lock.json` a znovu ho obnovit.</span><span class="sxs-lookup"><span data-stu-id="7ce7c-116">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="7ce7c-117">Nejde zobrazit, přidat ani aktualizovat DotNetCLITools pomocí Správce balíčků Nuget</span><span class="sxs-lookup"><span data-stu-id="7ce7c-117">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="7ce7c-118">Problém</span><span class="sxs-lookup"><span data-stu-id="7ce7c-118">Issue</span></span>

<span data-ttu-id="7ce7c-119">Správce balíčků NuGet nezobrazuje a nepovoluje přidat nebo aktualizovat DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="7ce7c-119">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="7ce7c-120">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="7ce7c-120">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="7ce7c-121">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="7ce7c-121">Workaround</span></span>

<span data-ttu-id="7ce7c-122">V souboru projektu se musí ručně upravit DotNetCLIToolReferences.</span><span class="sxs-lookup"><span data-stu-id="7ce7c-122">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="7ce7c-123">Změna cílení verze cílové architektury může vést k nekompletnímu IntelliSense</span><span class="sxs-lookup"><span data-stu-id="7ce7c-123">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="7ce7c-124">Problém</span><span class="sxs-lookup"><span data-stu-id="7ce7c-124">Issue</span></span>

<span data-ttu-id="7ce7c-125">Změna cílení verze cílové architektury v sadě Visual Studio může vést k nekompletnímu IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="7ce7c-125">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="7ce7c-126">To se stává, když jako formát správce balíčků používáte PackageReferences.</span><span class="sxs-lookup"><span data-stu-id="7ce7c-126">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="7ce7c-127">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="7ce7c-127">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="7ce7c-128">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="7ce7c-128">Workaround</span></span>

<span data-ttu-id="7ce7c-129">Proveďte ruční obnovení.</span><span class="sxs-lookup"><span data-stu-id="7ce7c-129">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="7ce7c-130">Balíček v projektu .NET Core, který obsahuje sestavení s neplatným podpisem, může aktivovat nekonečnou smyčku obnovení</span><span class="sxs-lookup"><span data-stu-id="7ce7c-130">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="7ce7c-131">Problém</span><span class="sxs-lookup"><span data-stu-id="7ce7c-131">Issue</span></span>

<span data-ttu-id="7ce7c-132">V některých případech použijete balíček, který obsahuje sestavení s neplatným podpisem, nebo když se verze balíčku nastaví pomocí časovače "DateTime, může to způsobí, že auto obnovení balíčku občas způsobit nekonečnou smyčku (dotnet/project-system #1457).</span><span class="sxs-lookup"><span data-stu-id="7ce7c-132">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop (dotnet/project-system#1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="7ce7c-133">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="7ce7c-133">Workaround</span></span>

<span data-ttu-id="7ce7c-134">Pro tento problém zatím neexistuje alternativní řešení.</span><span class="sxs-lookup"><span data-stu-id="7ce7c-134">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a><span data-ttu-id="7ce7c-135">Problémy opravené ve verzi RTM 4.4 NuGet časový rámec</span><span class="sxs-lookup"><span data-stu-id="7ce7c-135">Issues fixed in NuGet 4.4 RTM timeframe</span></span>

<span data-ttu-id="7ce7c-136">[4.3 RTM poznámkách k verzi NuGet](../release-notes/nuget-4.3-RTM.md) – zobrazí seznam všech problémů stanovené pro verzi RTM 4.3 NuGet</span><span class="sxs-lookup"><span data-stu-id="7ce7c-136">[NuGet 4.3 RTM Release Notes](../release-notes/nuget-4.3-RTM.md) - Lists all the issues fixed for NuGet 4.3 RTM</span></span>

### <a name="features"></a><span data-ttu-id="7ce7c-137">Funkce</span><span class="sxs-lookup"><span data-stu-id="7ce7c-137">Features</span></span>

- <span data-ttu-id="7ce7c-138">Podpora pro zjednodušené načtení řešení v PMC a NuGet PM uživatelského scénáře: [#5180](https://github.com/NuGet/Home/issues/5180)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-138">Support for Lightweight Solution Load in PMC and NuGet PM UI scenarios - [#5180](https://github.com/NuGet/Home/issues/5180)</span></span>

- <span data-ttu-id="7ce7c-139">Cíl nástroje msbuild pack by měl mít veřejný vidlici pro spuštění cíle uživatele před samotný - [#5143](https://github.com/NuGet/Home/issues/5143)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-139">The msbuild pack target should have a public hook for running user targets before itself - [#5143](https://github.com/NuGet/Home/issues/5143)</span></span>

- <span data-ttu-id="7ce7c-140">Funkce: Přidejte přepínač dependencyVersion do instalace nuget – [#1806](https://github.com/NuGet/Home/issues/1806)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-140">Feature: Add dependencyVersion switch to nuget install - [#1806](https://github.com/NuGet/Home/issues/1806)</span></span>

- <span data-ttu-id="7ce7c-141">uap10.0.todo.0 mělo mapovat .NET Standard 2.0 pro NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-141">uap10.0.TODO.0 should map to .NET Standard 2.0 for NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)</span></span>

- <span data-ttu-id="7ce7c-142">Podporovat SKU Visual Studio sestavení nástroje msbuild/t: Restore - [#5562](https://github.com/NuGet/Home/issues/5562)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-142">Support Visual Studio Build Tools SKU with msbuild /t:restore - [#5562](https://github.com/NuGet/Home/issues/5562)</span></span>

- <span data-ttu-id="7ce7c-143">Během obnovení, vygenerují chybu, pokud .NET 4.6.1 podpora .NET Standard 2.0 je vyžadována, ale není nainstalovaná - [#5325](https://github.com/NuGet/Home/issues/5325)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-143">During restore, generate an error if .NET 4.6.1 support for .NET Standard 2.0 is required but not installed - [#5325](https://github.com/NuGet/Home/issues/5325)</span></span>

- <span data-ttu-id="7ce7c-144">Balíček ID předponu rezervace uživatelské rozhraní klienta - [#5572](https://github.com/NuGet/Home/issues/5572)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-144">Package ID prefix reservation client UI - [#5572](https://github.com/NuGet/Home/issues/5572)</span></span>

- <span data-ttu-id="7ce7c-145">doručování součásti lokalizované nuget pro podporu lokalizace dotnet.exe - [#4336](https://github.com/NuGet/Home/issues/4336)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-145">deliver localized nuget components to support dotnet.exe localization - [#4336](https://github.com/NuGet/Home/issues/4336)</span></span>

### <a name="bugs"></a><span data-ttu-id="7ce7c-146">Chyby</span><span class="sxs-lookup"><span data-stu-id="7ce7c-146">Bugs</span></span>

- <span data-ttu-id="7ce7c-147">Cesta písmen jiný projekt může způsobit obnovení přijít o PackageReferences - [#5855](https://github.com/NuGet/Home/issues/5855)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-147">Different project path casings can cause restore to lose PackageReferences - [#5855](https://github.com/NuGet/Home/issues/5855)</span></span>

- <span data-ttu-id="7ce7c-148">Přesunout na rozsah chyby – kódy chyb s čísla upozornění [#5824](https://github.com/NuGet/Home/issues/5824)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-148">Move error codes with warning numbers to error range - [#5824](https://github.com/NuGet/Home/issues/5824)</span></span>

- <span data-ttu-id="7ce7c-149">Když se ví, .NET Standard verze není kompatibilní s cílovou architekturu - zavádějící chyba [#5818](https://github.com/NuGet/Home/issues/5818)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-149">Misleading error when .NET Standard version is not known to be compatible with target framework  - [#5818](https://github.com/NuGet/Home/issues/5818)</span></span>

- <span data-ttu-id="7ce7c-150">Soubory s licencí matoucí – testování [#5776](https://github.com/NuGet/Home/issues/5776)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-150">Test files with confusing licenses - [#5776](https://github.com/NuGet/Home/issues/5776)</span></span>

- <span data-ttu-id="7ce7c-151">Chybí záhlaví licence v EndToEnd testovací šablony - [#5774](https://github.com/NuGet/Home/issues/5774)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-151">Missing license headers in EndToEnd test templates - [#5774](https://github.com/NuGet/Home/issues/5774)</span></span>

- <span data-ttu-id="7ce7c-152">obnovení souboru Packages.config se zobrazí chyby jako NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-152">packages.config restore shows errors as NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)</span></span>

- <span data-ttu-id="7ce7c-153">instalace nuget.exe by měl mít DisableParallelProcessing v mono - [#5741](https://github.com/NuGet/Home/issues/5741)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-153">nuget.exe install should have DisableParallelProcessing on mono - [#5741](https://github.com/NuGet/Home/issues/5741)</span></span>

- <span data-ttu-id="7ce7c-154">instalace nuget.exe nesprávně zakáže ukládání do mezipaměti – [#5737](https://github.com/NuGet/Home/issues/5737)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-154">nuget.exe install incorrectly disables caching - [#5737](https://github.com/NuGet/Home/issues/5737)</span></span>

- <span data-ttu-id="7ce7c-155">VS pro zobrazení souboru packages.config při obnovení zakázáno nesprávná zpráva – spouštění příkazu restore [#5718](https://github.com/NuGet/Home/issues/5718)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-155">VS Running the restore command for packages.config when Restore is disabled displays incorrect message  - [#5718](https://github.com/NuGet/Home/issues/5718)</span></span>

- <span data-ttu-id="7ce7c-156">VS; Spuštění příkazu restore, když je obnovení zakázáno zobrazí zprávu matoucí - [#5659](https://github.com/NuGet/Home/issues/5659)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-156">VS; Running the restore command when Restore is disabled displays a confusing message - [#5659](https://github.com/NuGet/Home/issues/5659)</span></span>

- <span data-ttu-id="7ce7c-157">GetRestoreDotnetCliToolsTask není úspěšné při chybí metadata verze – [#5716](https://github.com/NuGet/Home/issues/5716)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-157">GetRestoreDotnetCliToolsTask fails when missing version metadata - [#5716](https://github.com/NuGet/Home/issues/5716)</span></span>

- <span data-ttu-id="7ce7c-158">DotNet</span><span class="sxs-lookup"><span data-stu-id="7ce7c-158">dotnet</span></span>
  - <span data-ttu-id="7ce7c-159">dotnetcore přidat balíček můžete vymazat prázdné řádky ze souboru csproj - [#5697](https://github.com/NuGet/Home/issues/5697)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-159">dotnetcore add package can clear empty lines from a csproj  - [#5697](https://github.com/NuGet/Home/issues/5697)</span></span>

- <span data-ttu-id="7ce7c-160">Názvy zdrojů nastavení přihlašovacích údajů do souboru NuGet.Config jsou malá a velká písmena - [#5695](https://github.com/NuGet/Home/issues/5695)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-160">Source names of credential settings in NuGet.Config are case sensitive - [#5695](https://github.com/NuGet/Home/issues/5695)</span></span>

- <span data-ttu-id="7ce7c-161">Povolení GeneratePackageOnBuild odstranit celou historii balíčků - [#5676](https://github.com/NuGet/Home/issues/5676)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-161">Enabling GeneratePackageOnBuild deleted my entire history of packages - [#5676](https://github.com/NuGet/Home/issues/5676)</span></span>

- <span data-ttu-id="7ce7c-162">Restore neobnoví balíčky mono.cecil nebo semver, ale všechny ostatní balíčky obnovena.</span><span class="sxs-lookup"><span data-stu-id="7ce7c-162">Restore will not restore mono.cecil or semver packages, but all other packages get restored.</span></span><span data-ttu-id="7ce7c-163"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-163"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span></span>

- <span data-ttu-id="7ce7c-164">Chyby a upozornění - chybný při zdroj není k dispozici.</span><span class="sxs-lookup"><span data-stu-id="7ce7c-164">Errors and Warnings - bad error when a source in unavailable.</span></span><span data-ttu-id="7ce7c-165">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-165">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span></span>

- <span data-ttu-id="7ce7c-166">[DesignConsistency] Instalace NuGet stavový text nevypadá aktuálně správné na tmavý motiv.</span><span class="sxs-lookup"><span data-stu-id="7ce7c-166">[DesignConsistency] NuGet Installation status text doesn’t look correct on dark theme currently.</span></span><span data-ttu-id="7ce7c-167"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-167"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span></span>

- <span data-ttu-id="7ce7c-168">Aktualizovat balíčky v řešení aktualizací nebo instalace pro všechny projekty - [#5508](https://github.com/NuGet/Home/issues/5508)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-168">Update packages at solution updates/installs for all the projects - [#5508](https://github.com/NuGet/Home/issues/5508)</span></span>

- <span data-ttu-id="7ce7c-169">DotNet</span><span class="sxs-lookup"><span data-stu-id="7ce7c-169">dotnet</span></span>
  - <span data-ttu-id="7ce7c-170">balíček dotnetcore chová odlišně v závislosti na vs TargetFramework TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-170">dotnetcore pack behaves differently depending on TargetFramework vs TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)</span></span>

- <span data-ttu-id="7ce7c-171">Zahrnout knihovny DLL uvnitř nástroje pro složku throw upozornění - [#5020](https://github.com/NuGet/Home/issues/5020)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-171">Included DLLs inside Tools folder throw warnings - [#5020](https://github.com/NuGet/Home/issues/5020)</span></span>

- <span data-ttu-id="7ce7c-172">NuGet.ContentModel spotřebovává příliš mnoho paměti pro operace s řetězci - [#4714](https://github.com/NuGet/Home/issues/4714)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-172">NuGet.ContentModel consumes too much memory for string operations - [#4714](https://github.com/NuGet/Home/issues/4714)</span></span>

- <span data-ttu-id="7ce7c-173">RuntimeEnvironmentHelper.IsLinux vrací hodnotu true pro OS x - [#4648](https://github.com/NuGet/Home/issues/4648)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-173">RuntimeEnvironmentHelper.IsLinux returns true for OSX - [#4648](https://github.com/NuGet/Home/issues/4648)</span></span>

- <span data-ttu-id="7ce7c-174">soubor nuspec pod obj místo obj\Debug – vloží "balíčku dotnet" [#4644](https://github.com/NuGet/Home/issues/4644)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-174">'dotnet pack' puts nuspec under obj instead of obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)</span></span>

- <span data-ttu-id="7ce7c-175">Nuget velmi pomalé aktualizaci balíčku - [#4534](https://github.com/NuGet/Home/issues/4534)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-175">Nuget extremely slow package upgrade - [#4534](https://github.com/NuGet/Home/issues/4534)</span></span>

- <span data-ttu-id="7ce7c-176">Prohlášení CPS synchronizovaný s obnovení s větší řešení, které nezapnuli zjednodušeného načtení řešení (obnovení zjednodušeného řešení) – [#4307](https://github.com/NuGet/Home/issues/4307)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-176">CPS out of sync with Restore with larger solutions that haven't turned on LSL (lightweight solution restore) - [#4307](https://github.com/NuGet/Home/issues/4307)</span></span>

- <span data-ttu-id="7ce7c-177">SemVer 2.0 - nuget pack s zadaná verze ignoruje metadata (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-177">SemVer 2.0 - nuget pack with provided version ignores metadata (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)</span></span>

- <span data-ttu-id="7ce7c-178">Nuget.exe (3 +) nainstalujte balíček s číslem verze a ExcludeVersion příznaku neprovede aktualizaci balíčku na novější verzi - [#2405](https://github.com/NuGet/Home/issues/2405)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-178">Nuget.exe (3.+) install package with Version number and ExcludeVersion flag doesn't update package to newer version - [#2405](https://github.com/NuGet/Home/issues/2405)</span></span>

- <span data-ttu-id="7ce7c-179">Project.JSON obnovení musí zobrazit upozornění, pokud nejvyšší úrovně balíčky porušení omezení - [#2358](https://github.com/NuGet/Home/issues/2358)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-179">Project.json restore should warn when top-level packages violate constraints - [#2358](https://github.com/NuGet/Home/issues/2358)</span></span>

- <span data-ttu-id="7ce7c-180">-ConfigFile není nastavení vlastní konfigurace pro příkaz install - [#1646](https://github.com/NuGet/Home/issues/1646)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-180">-ConfigFile is not setting custom config on install command - [#1646](https://github.com/NuGet/Home/issues/1646)</span></span>

- <span data-ttu-id="7ce7c-181">instalace nuget.exe nerespektuje "-DisableParallelProcessing" přepínač - [#1556](https://github.com/NuGet/Home/issues/1556)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-181">nuget.exe install does not honor '-DisableParallelProcessing' switch - [#1556](https://github.com/NuGet/Home/issues/1556)</span></span>

- <span data-ttu-id="7ce7c-182">Zakázané zdrojů i nadále používat DotNet.exe nebo msbuild.exe - [#5704](https://github.com/NuGet/Home/issues/5704)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-182">Disabled sources still used by DotNet.exe or msbuild.exe - [#5704](https://github.com/NuGet/Home/issues/5704)</span></span>

- <span data-ttu-id="7ce7c-183">Opravit. program přestane reagovat ve scénáři zjednodušeného načtení řešení - [#5685](https://github.com/NuGet/Home/issues/5685)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-183">Fix hangs in LSL scenario - [#5685](https://github.com/NuGet/Home/issues/5685)</span></span>

### <a name="dcrs"></a><span data-ttu-id="7ce7c-184">Chcete</span><span class="sxs-lookup"><span data-stu-id="7ce7c-184">DCRs</span></span>

- <span data-ttu-id="7ce7c-185">nuget.exe nainstalovat podporu TargetFramework - [#5736](https://github.com/NuGet/Home/issues/5736)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-185">nuget.exe install TargetFramework support - [#5736](https://github.com/NuGet/Home/issues/5736)</span></span>

- <span data-ttu-id="7ce7c-186">Přidejte jiný msbuild úloh UserAgent řetězce (msbuild klasické pracovní plochy netcore vs) - [#5709](https://github.com/NuGet/Home/issues/5709)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-186">Add different msbuild task UserAgent strings (netcore vs desktop msbuild) - [#5709](https://github.com/NuGet/Home/issues/5709)</span></span>

- <span data-ttu-id="7ce7c-187">PackagePathResolver.GetPackageDirectoryName by měl být virtuální - [#5700](https://github.com/NuGet/Home/issues/5700)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-187">PackagePathResolver.GetPackageDirectoryName should be virtual - [#5700](https://github.com/NuGet/Home/issues/5700)</span></span>

- <span data-ttu-id="7ce7c-188">[DesignConsistency] Matoucí zprávy při přidání balíčku NuGet - [#5641](https://github.com/NuGet/Home/issues/5641)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-188">[DesignConsistency] Confusing message when adding a NuGet package - [#5641](https://github.com/NuGet/Home/issues/5641)</span></span>

- <span data-ttu-id="7ce7c-189">[Upozornění a chyby] NoWarn není přechodně probíhat přes odkazy P2P - [#5501](https://github.com/NuGet/Home/issues/5501)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-189">[Warnings and errors] NoWarn does not flow transitively through P2P references - [#5501](https://github.com/NuGet/Home/issues/5501)</span></span>

- <span data-ttu-id="7ce7c-190">Zjednodušené načtení řešení: Common jádro pro uživatelské rozhraní PM, PMC a vektory IV-- [#5057](https://github.com/NuGet/Home/issues/5057)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-190">Lightweight Solution Load: Common Core for PM UI, PMC, and IVs- - [#5057](https://github.com/NuGet/Home/issues/5057)</span></span>

- <span data-ttu-id="7ce7c-191">Zjednodušené načtení řešení: Podpora - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-191">Lightweight Solution Load: Support - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)</span></span>

- <span data-ttu-id="7ce7c-192">Přidání podpory pro před obnovením cíl nástroje MSBuild, který spustí Visual Studio – [#4781](https://github.com/NuGet/Home/issues/4781)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-192">Add support for pre-restore MSBuild target that Visual Studio triggers - [#4781](https://github.com/NuGet/Home/issues/4781)</span></span>

- <span data-ttu-id="7ce7c-193">Přidat veřejný cíl NuGet.targets, který může být odkazováno pomocí BeforeTargets- [#4634](https://github.com/NuGet/Home/issues/4634)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-193">Add a public target to NuGet.targets that can be referenced using BeforeTargets - [#4634](https://github.com/NuGet/Home/issues/4634)</span></span>

- <span data-ttu-id="7ce7c-194">Cíl Pack nelze contentFiles vytvořit s akcí sestavení správně – [#4166](https://github.com/NuGet/Home/issues/4166)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-194">Pack target can't create contentFiles with build actions correctly - [#4166](https://github.com/NuGet/Home/issues/4166)</span></span>

- <span data-ttu-id="7ce7c-195">RestoreOperationLogger.Do blokuje vláken fondu vláken - [#5663](https://github.com/NuGet/Home/issues/5663)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-195">RestoreOperationLogger.Do blocks thread pool threads - [#5663](https://github.com/NuGet/Home/issues/5663)</span></span>

### <a name="docs"></a><span data-ttu-id="7ce7c-196">Docs</span><span class="sxs-lookup"><span data-stu-id="7ce7c-196">Docs</span></span>

- <span data-ttu-id="7ce7c-197">Dokumentace pro instalaci příkazu DependencyVersion a Framework příznaky - [#5858](https://github.com/NuGet/Home/issues/5858)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-197">Docs for Install command DependencyVersion and Framework flags - [#5858](https://github.com/NuGet/Home/issues/5858)</span></span>

- <span data-ttu-id="7ce7c-198">Aktualizace dokumentace pro NuGet upozornění a chyby - [#5857](https://github.com/NuGet/Home/issues/5857)</span><span class="sxs-lookup"><span data-stu-id="7ce7c-198">Update to docs on NuGet warnings and errors - [#5857](https://github.com/NuGet/Home/issues/5857)</span></span>

## <a name="links-to-github-issues-fixed-in-44-rtm"></a><span data-ttu-id="7ce7c-199">Odkazy na problémy Githubu Vyřešeno ve verzi RTM 4.4</span><span class="sxs-lookup"><span data-stu-id="7ce7c-199">Links to GitHub issues fixed in 4.4 RTM</span></span>

[<span data-ttu-id="7ce7c-200">Seznam problémů, 1</span><span class="sxs-lookup"><span data-stu-id="7ce7c-200">Issues List 1</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[<span data-ttu-id="7ce7c-201">Seznam problémů, 2</span><span class="sxs-lookup"><span data-stu-id="7ce7c-201">Issues List 2</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[<span data-ttu-id="7ce7c-202">Seznam problémů, 3</span><span class="sxs-lookup"><span data-stu-id="7ce7c-202">Issues List 3</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
