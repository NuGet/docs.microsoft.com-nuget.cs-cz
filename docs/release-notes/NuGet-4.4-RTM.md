---
title: NuGet 4.4 RTM Poznámky k verzi
description: Poznámky k verzi pro NuGet 4.3 RTM včetně známých problémů, oprav chyb, přidaných funkcí a řadičů domény.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 3be24a86cc92c4e6d07fcae1dc625a150f28d7b4
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "64498703"
---
# <a name="nuget-44-release-notes"></a><span data-ttu-id="30c46-103">NuGet 4.4 Poznámky k verzi</span><span class="sxs-lookup"><span data-stu-id="30c46-103">NuGet 4.4 Release Notes</span></span>

<span data-ttu-id="30c46-104">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) je dodáván s NuGet 4.4 RTM.</span><span class="sxs-lookup"><span data-stu-id="30c46-104">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.4 RTM.</span></span>

## <a name="summary-whats-new-in-440"></a><span data-ttu-id="30c46-105">Shrnutí: Co je nového v 4.4.0</span><span class="sxs-lookup"><span data-stu-id="30c46-105">Summary: What's New in 4.4.0</span></span>

## <a name="summary-whats-new-in-442"></a><span data-ttu-id="30c46-106">Shrnutí: Co je nového v 4.4.2</span><span class="sxs-lookup"><span data-stu-id="30c46-106">Summary: What's New in 4.4.2</span></span>

* <span data-ttu-id="30c46-107">Oprava zabezpečení: Oprávnění k souborům vytvořeným uvnitř ~/.nuget jsou příliš otevřená [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span><span class="sxs-lookup"><span data-stu-id="30c46-107">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>

## <a name="summary-whats-new-in-443"></a><span data-ttu-id="30c46-108">Shrnutí: Co je nového v 4.4.3</span><span class="sxs-lookup"><span data-stu-id="30c46-108">Summary: What's New in 4.4.3</span></span>

* <span data-ttu-id="30c46-109">Oprava zabezpečení: Soubory uvnitř NUPKGs mohou mít relativní cestu nad adresářem NUPKG [#7906](https://github.com/NuGet/Home/issues/7906)</span><span class="sxs-lookup"><span data-stu-id="30c46-109">Security Fix: Files inside of NUPKGs can have a relative path above the NUPKG directory [#7906](https://github.com/NuGet/Home/issues/7906)</span></span>

## <a name="known-issues"></a><span data-ttu-id="30c46-110">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="30c46-110">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="30c46-111">Problémy s rozhraním .NET Standard 2.0 s rozhraním .NET Framework & NuGet</span><span class="sxs-lookup"><span data-stu-id="30c46-111">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="30c46-112">.NET Standard & jeho nástroje byly navrženy tak, že projekty zaměřené na rozhraní .NET Framework 4.6.1 mohou využívat balíčky NuGet & projekty zaměřené na standard .NET Standard 2.0 nebo starší.</span><span class="sxs-lookup"><span data-stu-id="30c46-112">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="30c46-113">[Tento dokument](https://github.com/dotnet/standard/issues/481) shrnuje problémy kolem tohoto scénáře, plán pro jejich řešení a řešení, která můžete nasadit s dnešním stavem nástrojů.</span><span class="sxs-lookup"><span data-stu-id="30c46-113">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="30c46-114">Při používání konzoly Správce balíčků nemusí fungovat klávesa Enter</span><span class="sxs-lookup"><span data-stu-id="30c46-114">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="30c46-115">Problém</span><span class="sxs-lookup"><span data-stu-id="30c46-115">Issue</span></span>

<span data-ttu-id="30c46-116">V konzole Správce balíčků občas nefunguje klávesa Enter.</span><span class="sxs-lookup"><span data-stu-id="30c46-116">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="30c46-117">Když toto chování zpozorujete, zjistěte prosím, jak to vypadá s opravou, a poskytněte jakékoli další užitečné informace o postupu, jak tuto chybu reprodukovat.</span><span class="sxs-lookup"><span data-stu-id="30c46-117">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="30c46-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="30c46-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="30c46-119">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="30c46-119">Workaround</span></span>

<span data-ttu-id="30c46-120">Před otevřením řešení restartujte Visual Studio a otevřete konzolu PMC.</span><span class="sxs-lookup"><span data-stu-id="30c46-120">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="30c46-121">Případně zkuste znovu smažit `project.lock.json` a obnovit.</span><span class="sxs-lookup"><span data-stu-id="30c46-121">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="30c46-122">Pomocí Nástroje pro balení Nuget nelze zobrazit, přidat nebo aktualizovat nástroje DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="30c46-122">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="30c46-123">Problém</span><span class="sxs-lookup"><span data-stu-id="30c46-123">Issue</span></span>

<span data-ttu-id="30c46-124">Správce balíčků NuGet nezobrazuje a nepovoluje přidat nebo aktualizovat DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="30c46-124">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="30c46-125">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="30c46-125">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="30c46-126">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="30c46-126">Workaround</span></span>

<span data-ttu-id="30c46-127">V souboru projektu se musí ručně upravit DotNetCLIToolReferences.</span><span class="sxs-lookup"><span data-stu-id="30c46-127">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="30c46-128">Změna cílení verze cílové architektury může vést k nekompletnímu IntelliSense</span><span class="sxs-lookup"><span data-stu-id="30c46-128">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="30c46-129">Problém</span><span class="sxs-lookup"><span data-stu-id="30c46-129">Issue</span></span>

<span data-ttu-id="30c46-130">Změna cílení verze cílové architektury v sadě Visual Studio může vést k nekompletnímu IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="30c46-130">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="30c46-131">To se stává, když jako formát správce balíčků používáte PackageReferences.</span><span class="sxs-lookup"><span data-stu-id="30c46-131">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="30c46-132">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="30c46-132">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="30c46-133">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="30c46-133">Workaround</span></span>

<span data-ttu-id="30c46-134">Proveďte ruční obnovení.</span><span class="sxs-lookup"><span data-stu-id="30c46-134">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="30c46-135">Balíček v projektu .NET Core, který obsahuje sestavení s neplatným podpisem, může aktivovat nekonečnou smyčku obnovení</span><span class="sxs-lookup"><span data-stu-id="30c46-135">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="30c46-136">Problém</span><span class="sxs-lookup"><span data-stu-id="30c46-136">Issue</span></span>

<span data-ttu-id="30c46-137">Když použijete balíček, který obsahuje sestavení s neplatným podpisem, nebo když je verze balíčku nastavená pomocí časovače DateTime, může při automatickém obnovení balíčku občas vzniknout nekonečná smyčka (dotnet/project-system#1457).</span><span class="sxs-lookup"><span data-stu-id="30c46-137">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop (dotnet/project-system#1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="30c46-138">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="30c46-138">Workaround</span></span>

<span data-ttu-id="30c46-139">Pro tento problém zatím neexistuje alternativní řešení.</span><span class="sxs-lookup"><span data-stu-id="30c46-139">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a><span data-ttu-id="30c46-140">Problémy opravené v časovém rámci NuGet 4.4 RTM</span><span class="sxs-lookup"><span data-stu-id="30c46-140">Issues fixed in NuGet 4.4 RTM timeframe</span></span>

<span data-ttu-id="30c46-141">[NuGet 4.3 RTM Poznámky k verzi](../release-notes/nuget-4.3-RTM.md) - Seznam všech problémů opravených pro NuGet 4.3 RTM</span><span class="sxs-lookup"><span data-stu-id="30c46-141">[NuGet 4.3 RTM Release Notes](../release-notes/nuget-4.3-RTM.md) - Lists all the issues fixed for NuGet 4.3 RTM</span></span>

### <a name="features"></a><span data-ttu-id="30c46-142">Funkce</span><span class="sxs-lookup"><span data-stu-id="30c46-142">Features</span></span>

- <span data-ttu-id="30c46-143">Podpora pro zjednodušené zatížení řešení ve scénářích PMC a NuGet PM UI – [#5180](https://github.com/NuGet/Home/issues/5180)</span><span class="sxs-lookup"><span data-stu-id="30c46-143">Support for Lightweight Solution Load in PMC and NuGet PM UI scenarios - [#5180](https://github.com/NuGet/Home/issues/5180)</span></span>

- <span data-ttu-id="30c46-144">Cíl msbuild pack by měl mít veřejný háček pro spuštění uživatelských cílů před sebou - [#5143](https://github.com/NuGet/Home/issues/5143)</span><span class="sxs-lookup"><span data-stu-id="30c46-144">The msbuild pack target should have a public hook for running user targets before itself - [#5143](https://github.com/NuGet/Home/issues/5143)</span></span>

- <span data-ttu-id="30c46-145">Funkce: Přidání závislostiVersion přepínač nuget nainstalovat - [#1806](https://github.com/NuGet/Home/issues/1806)</span><span class="sxs-lookup"><span data-stu-id="30c46-145">Feature: Add dependencyVersion switch to nuget install - [#1806](https://github.com/NuGet/Home/issues/1806)</span></span>

- <span data-ttu-id="30c46-146">uap10.0.TODO.0 by měl mapovat na .NET Standard 2.0 pro NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)</span><span class="sxs-lookup"><span data-stu-id="30c46-146">uap10.0.TODO.0 should map to .NET Standard 2.0 for NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)</span></span>

- <span data-ttu-id="30c46-147">Podpora nástroje sestavení sady Visual Studio s ku s msbuild /t:restore - [#5562](https://github.com/NuGet/Home/issues/5562)</span><span class="sxs-lookup"><span data-stu-id="30c46-147">Support Visual Studio Build Tools SKU with msbuild /t:restore - [#5562](https://github.com/NuGet/Home/issues/5562)</span></span>

- <span data-ttu-id="30c46-148">Během obnovení vygenerujte chybu, pokud je vyžadována podpora rozhraní .NET 4.6.1 pro rozhraní .NET Standard 2.0, ale není nainstalována - [#5325](https://github.com/NuGet/Home/issues/5325)</span><span class="sxs-lookup"><span data-stu-id="30c46-148">During restore, generate an error if .NET 4.6.1 support for .NET Standard 2.0 is required but not installed - [#5325](https://github.com/NuGet/Home/issues/5325)</span></span>

- <span data-ttu-id="30c46-149">UI klienta předpony id balíčku - [#5572](https://github.com/NuGet/Home/issues/5572)</span><span class="sxs-lookup"><span data-stu-id="30c46-149">Package ID prefix reservation client UI - [#5572](https://github.com/NuGet/Home/issues/5572)</span></span>

- <span data-ttu-id="30c46-150">Doručují lokalizované nugetové komponenty pro podporu lokalizace dotnet.exe - [#4336](https://github.com/NuGet/Home/issues/4336)</span><span class="sxs-lookup"><span data-stu-id="30c46-150">deliver localized nuget components to support dotnet.exe localization - [#4336](https://github.com/NuGet/Home/issues/4336)</span></span>

### <a name="bugs"></a><span data-ttu-id="30c46-151">Chyby</span><span class="sxs-lookup"><span data-stu-id="30c46-151">Bugs</span></span>

- <span data-ttu-id="30c46-152">Různé cesty projektu kryty může způsobit obnovení ztratit PackageReferences - [#5855](https://github.com/NuGet/Home/issues/5855)</span><span class="sxs-lookup"><span data-stu-id="30c46-152">Different project path casings can cause restore to lose PackageReferences - [#5855](https://github.com/NuGet/Home/issues/5855)</span></span>

- <span data-ttu-id="30c46-153">Přesunout kódy chyb s čísly upozornění do rozsahu chyb - [#5824](https://github.com/NuGet/Home/issues/5824)</span><span class="sxs-lookup"><span data-stu-id="30c46-153">Move error codes with warning numbers to error range - [#5824](https://github.com/NuGet/Home/issues/5824)</span></span>

- <span data-ttu-id="30c46-154">Zavádějící chyba, pokud není známo, že verze rozhraní .NET Standard je kompatibilní s cílovým rozhraním [, #5818](https://github.com/NuGet/Home/issues/5818)</span><span class="sxs-lookup"><span data-stu-id="30c46-154">Misleading error when .NET Standard version is not known to be compatible with target framework  - [#5818](https://github.com/NuGet/Home/issues/5818)</span></span>

- <span data-ttu-id="30c46-155">Testování souborů s matoucími licencemi - [#5776](https://github.com/NuGet/Home/issues/5776)</span><span class="sxs-lookup"><span data-stu-id="30c46-155">Test files with confusing licenses - [#5776](https://github.com/NuGet/Home/issues/5776)</span></span>

- <span data-ttu-id="30c46-156">Chybějící záhlaví licencí v testovacích šablonách EndToEnd - [#5774](https://github.com/NuGet/Home/issues/5774)</span><span class="sxs-lookup"><span data-stu-id="30c46-156">Missing license headers in EndToEnd test templates - [#5774](https://github.com/NuGet/Home/issues/5774)</span></span>

- <span data-ttu-id="30c46-157">packages.config restore zobrazuje chyby jako NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)</span><span class="sxs-lookup"><span data-stu-id="30c46-157">packages.config restore shows errors as NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)</span></span>

- <span data-ttu-id="30c46-158">Nuget.exe instalace by měla mít DisableParallelProcessing na mono - [#5741](https://github.com/NuGet/Home/issues/5741)</span><span class="sxs-lookup"><span data-stu-id="30c46-158">nuget.exe install should have DisableParallelProcessing on mono - [#5741](https://github.com/NuGet/Home/issues/5741)</span></span>

- <span data-ttu-id="30c46-159">Nuget.exe instalace nesprávně zakáže ukládání do mezipaměti - [#5737](https://github.com/NuGet/Home/issues/5737)</span><span class="sxs-lookup"><span data-stu-id="30c46-159">nuget.exe install incorrectly disables caching - [#5737](https://github.com/NuGet/Home/issues/5737)</span></span>

- <span data-ttu-id="30c46-160">VS Spuštění příkazu Obnovení pro packages.config při obnovení je zakázáno zobrazí nesprávnou zprávu - [#5718](https://github.com/NuGet/Home/issues/5718)</span><span class="sxs-lookup"><span data-stu-id="30c46-160">VS Running the restore command for packages.config when Restore is disabled displays incorrect message  - [#5718](https://github.com/NuGet/Home/issues/5718)</span></span>

- <span data-ttu-id="30c46-161">VS; Spuštění příkazu obnovit při zakázání obnovení zobrazí matoucí zprávu - [#5659](https://github.com/NuGet/Home/issues/5659)</span><span class="sxs-lookup"><span data-stu-id="30c46-161">VS; Running the restore command when Restore is disabled displays a confusing message - [#5659](https://github.com/NuGet/Home/issues/5659)</span></span>

- <span data-ttu-id="30c46-162">GetRestoreDotnetCliToolsTask se nezdaří, když chybí metadata verze - [#5716](https://github.com/NuGet/Home/issues/5716)</span><span class="sxs-lookup"><span data-stu-id="30c46-162">GetRestoreDotnetCliToolsTask fails when missing version metadata - [#5716](https://github.com/NuGet/Home/issues/5716)</span></span>

- <span data-ttu-id="30c46-163">dotnet</span><span class="sxs-lookup"><span data-stu-id="30c46-163">dotnet</span></span>
  - <span data-ttu-id="30c46-164">dotnetcore přidat balíček může vymazat prázdné řádky z csproj - [#5697](https://github.com/NuGet/Home/issues/5697)</span><span class="sxs-lookup"><span data-stu-id="30c46-164">dotnetcore add package can clear empty lines from a csproj  - [#5697](https://github.com/NuGet/Home/issues/5697)</span></span>

- <span data-ttu-id="30c46-165">Zdrojové názvy nastavení pověření v Souboru NuGet.Config rozlišují malá a velká písmena – [#5695](https://github.com/NuGet/Home/issues/5695)</span><span class="sxs-lookup"><span data-stu-id="30c46-165">Source names of credential settings in NuGet.Config are case sensitive - [#5695](https://github.com/NuGet/Home/issues/5695)</span></span>

- <span data-ttu-id="30c46-166">Povolení GeneratePackageOnBuild odstranilo celou historii balíčků - [#5676](https://github.com/NuGet/Home/issues/5676)</span><span class="sxs-lookup"><span data-stu-id="30c46-166">Enabling GeneratePackageOnBuild deleted my entire history of packages - [#5676](https://github.com/NuGet/Home/issues/5676)</span></span>

- <span data-ttu-id="30c46-167">Obnovení neobnoví balíčky mono.cecil nebo semver, ale všechny ostatní balíčky budou obnoveny.</span><span class="sxs-lookup"><span data-stu-id="30c46-167">Restore will not restore mono.cecil or semver packages, but all other packages get restored.</span></span><span data-ttu-id="30c46-168"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span><span class="sxs-lookup"><span data-stu-id="30c46-168"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span></span>

- <span data-ttu-id="30c46-169">Chyby a upozornění - chybná chyba, když zdroj není k dispozici.</span><span class="sxs-lookup"><span data-stu-id="30c46-169">Errors and Warnings - bad error when a source in unavailable.</span></span><span data-ttu-id="30c46-170">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span><span class="sxs-lookup"><span data-stu-id="30c46-170">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span></span>

- <span data-ttu-id="30c46-171">[Konzistence návrhu] NuGet Instalace stav ový text nevypadá správně na tmavé téma v současné době.</span><span class="sxs-lookup"><span data-stu-id="30c46-171">[DesignConsistency] NuGet Installation status text doesn’t look correct on dark theme currently.</span></span><span data-ttu-id="30c46-172"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span><span class="sxs-lookup"><span data-stu-id="30c46-172"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span></span>

- <span data-ttu-id="30c46-173">Aktualizace balíčků při aktualizacích/instalacích řešení pro všechny projekty - [#5508](https://github.com/NuGet/Home/issues/5508)</span><span class="sxs-lookup"><span data-stu-id="30c46-173">Update packages at solution updates/installs for all the projects - [#5508](https://github.com/NuGet/Home/issues/5508)</span></span>

- <span data-ttu-id="30c46-174">dotnet</span><span class="sxs-lookup"><span data-stu-id="30c46-174">dotnet</span></span>
  - <span data-ttu-id="30c46-175">dotnetcore pack se chová odlišně v závislosti na TargetFramework vs TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)</span><span class="sxs-lookup"><span data-stu-id="30c46-175">dotnetcore pack behaves differently depending on TargetFramework vs TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)</span></span>

- <span data-ttu-id="30c46-176">Zahrnuté knihovny DLL uvnitř upozornění na vyvolání složky Nástroje - [#5020](https://github.com/NuGet/Home/issues/5020)</span><span class="sxs-lookup"><span data-stu-id="30c46-176">Included DLLs inside Tools folder throw warnings - [#5020](https://github.com/NuGet/Home/issues/5020)</span></span>

- <span data-ttu-id="30c46-177">NuGet.ContentModel spotřebovává příliš mnoho paměti pro operace řetězce - [#4714](https://github.com/NuGet/Home/issues/4714)</span><span class="sxs-lookup"><span data-stu-id="30c46-177">NuGet.ContentModel consumes too much memory for string operations - [#4714](https://github.com/NuGet/Home/issues/4714)</span></span>

- <span data-ttu-id="30c46-178">RuntimeEnvironmentHelper.IsLinux vrátí true pro OSX - [#4648](https://github.com/NuGet/Home/issues/4648)</span><span class="sxs-lookup"><span data-stu-id="30c46-178">RuntimeEnvironmentHelper.IsLinux returns true for OSX - [#4648](https://github.com/NuGet/Home/issues/4648)</span></span>

- <span data-ttu-id="30c46-179">'dotnet pack' klade nuspec pod obj místo obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)</span><span class="sxs-lookup"><span data-stu-id="30c46-179">'dotnet pack' puts nuspec under obj instead of obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)</span></span>

- <span data-ttu-id="30c46-180">Nuget extrémně pomalý upgrade balíčku - [#4534](https://github.com/NuGet/Home/issues/4534)</span><span class="sxs-lookup"><span data-stu-id="30c46-180">Nuget extremely slow package upgrade - [#4534](https://github.com/NuGet/Home/issues/4534)</span></span>

- <span data-ttu-id="30c46-181">Server CPS není synchronizován s obnovením s většími řešeními, která nezapnula LSL (zjednodušené obnovení řešení) – [#4307](https://github.com/NuGet/Home/issues/4307)</span><span class="sxs-lookup"><span data-stu-id="30c46-181">CPS out of sync with Restore with larger solutions that haven't turned on LSL (lightweight solution restore) - [#4307](https://github.com/NuGet/Home/issues/4307)</span></span>

- <span data-ttu-id="30c46-182">SemVer 2.0 - nuget pack s dodaným verzí ignoruje metadata (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)</span><span class="sxs-lookup"><span data-stu-id="30c46-182">SemVer 2.0 - nuget pack with provided version ignores metadata (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)</span></span>

- <span data-ttu-id="30c46-183">Nuget.exe (3.+) instalační balíček s číslem verze a příznakem ExcludeVersion neaktualizuje balíček na novější verzi - [#2405](https://github.com/NuGet/Home/issues/2405)</span><span class="sxs-lookup"><span data-stu-id="30c46-183">Nuget.exe (3.+) install package with Version number and ExcludeVersion flag doesn't update package to newer version - [#2405](https://github.com/NuGet/Home/issues/2405)</span></span>

- <span data-ttu-id="30c46-184">Obnovení aplikace Project.json by mělo upozornit, pokud balíčky nejvyšší úrovně porušují omezení – [#2358](https://github.com/NuGet/Home/issues/2358)</span><span class="sxs-lookup"><span data-stu-id="30c46-184">Project.json restore should warn when top-level packages violate constraints - [#2358](https://github.com/NuGet/Home/issues/2358)</span></span>

- <span data-ttu-id="30c46-185">-ConfigFile nenastavuje vlastní konfiguraci při příkazu install - [#1646](https://github.com/NuGet/Home/issues/1646)</span><span class="sxs-lookup"><span data-stu-id="30c46-185">-ConfigFile is not setting custom config on install command - [#1646](https://github.com/NuGet/Home/issues/1646)</span></span>

- <span data-ttu-id="30c46-186">nuget.exe instalace nerespektuje '-DisableParallelProcessing' přepínač - [#1556](https://github.com/NuGet/Home/issues/1556)</span><span class="sxs-lookup"><span data-stu-id="30c46-186">nuget.exe install does not honor '-DisableParallelProcessing' switch - [#1556](https://github.com/NuGet/Home/issues/1556)</span></span>

- <span data-ttu-id="30c46-187">Zakázané zdroje stále používané dotNet.exe nebo msbuild.exe - [#5704](https://github.com/NuGet/Home/issues/5704)</span><span class="sxs-lookup"><span data-stu-id="30c46-187">Disabled sources still used by DotNet.exe or msbuild.exe - [#5704](https://github.com/NuGet/Home/issues/5704)</span></span>

- <span data-ttu-id="30c46-188">Oprava zablokování ve scénáři LSL - [#5685](https://github.com/NuGet/Home/issues/5685)</span><span class="sxs-lookup"><span data-stu-id="30c46-188">Fix hangs in LSL scenario - [#5685](https://github.com/NuGet/Home/issues/5685)</span></span>

### <a name="dcrs"></a><span data-ttu-id="30c46-189">Řadiče domény</span><span class="sxs-lookup"><span data-stu-id="30c46-189">DCRs</span></span>

- <span data-ttu-id="30c46-190">podpora nuget.exe install TargetFramework - [#5736](https://github.com/NuGet/Home/issues/5736)</span><span class="sxs-lookup"><span data-stu-id="30c46-190">nuget.exe install TargetFramework support - [#5736](https://github.com/NuGet/Home/issues/5736)</span></span>

- <span data-ttu-id="30c46-191">Přidat různé msbuild úkol UserAgent řetězce (netcore vs desktop msbuild) - [#5709](https://github.com/NuGet/Home/issues/5709)</span><span class="sxs-lookup"><span data-stu-id="30c46-191">Add different msbuild task UserAgent strings (netcore vs desktop msbuild) - [#5709](https://github.com/NuGet/Home/issues/5709)</span></span>

- <span data-ttu-id="30c46-192">PackagePathResolver.GetPackageDirectoryName by měl být virtuální - [#5700](https://github.com/NuGet/Home/issues/5700)</span><span class="sxs-lookup"><span data-stu-id="30c46-192">PackagePathResolver.GetPackageDirectoryName should be virtual - [#5700](https://github.com/NuGet/Home/issues/5700)</span></span>

- <span data-ttu-id="30c46-193">[Konzistence návrhu] Matoucí zpráva při přidávání balíčku NuGet - [#5641](https://github.com/NuGet/Home/issues/5641)</span><span class="sxs-lookup"><span data-stu-id="30c46-193">[DesignConsistency] Confusing message when adding a NuGet package - [#5641](https://github.com/NuGet/Home/issues/5641)</span></span>

- <span data-ttu-id="30c46-194">[Varování a chyby] NoWarn neprotéká přechodně přes P2P odkazy - [#5501](https://github.com/NuGet/Home/issues/5501)</span><span class="sxs-lookup"><span data-stu-id="30c46-194">[Warnings and errors] NoWarn does not flow transitively through P2P references - [#5501](https://github.com/NuGet/Home/issues/5501)</span></span>

- <span data-ttu-id="30c46-195">Lehké zatížení řešení: Společné jádro pro PM ui, PMC a IV- - [#5057](https://github.com/NuGet/Home/issues/5057)</span><span class="sxs-lookup"><span data-stu-id="30c46-195">Lightweight Solution Load: Common Core for PM UI, PMC, and IVs- - [#5057](https://github.com/NuGet/Home/issues/5057)</span></span>

- <span data-ttu-id="30c46-196">Lehké zatížení řešení: Podpora - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)</span><span class="sxs-lookup"><span data-stu-id="30c46-196">Lightweight Solution Load: Support - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)</span></span>

- <span data-ttu-id="30c46-197">Přidání podpory pro cíl MSBuild před obnovením, který visual studio aktivuje – [#4781](https://github.com/NuGet/Home/issues/4781)</span><span class="sxs-lookup"><span data-stu-id="30c46-197">Add support for pre-restore MSBuild target that Visual Studio triggers - [#4781](https://github.com/NuGet/Home/issues/4781)</span></span>

- <span data-ttu-id="30c46-198">Přidejte veřejný cíl nuget.targets, na který lze odkazovat pomocí beforetargets - [#4634](https://github.com/NuGet/Home/issues/4634)</span><span class="sxs-lookup"><span data-stu-id="30c46-198">Add a public target to NuGet.targets that can be referenced using BeforeTargets - [#4634](https://github.com/NuGet/Home/issues/4634)</span></span>

- <span data-ttu-id="30c46-199">Cíl balíčku nemůže správně vytvářet contentFiles s akcemi sestavení – [#4166](https://github.com/NuGet/Home/issues/4166)</span><span class="sxs-lookup"><span data-stu-id="30c46-199">Pack target can't create contentFiles with build actions correctly - [#4166](https://github.com/NuGet/Home/issues/4166)</span></span>

- <span data-ttu-id="30c46-200">RestoreOperationLogger.Do blokuje vlákna fondu vláken - [#5663](https://github.com/NuGet/Home/issues/5663)</span><span class="sxs-lookup"><span data-stu-id="30c46-200">RestoreOperationLogger.Do blocks thread pool threads - [#5663](https://github.com/NuGet/Home/issues/5663)</span></span>

### <a name="docs"></a><span data-ttu-id="30c46-201">Docs</span><span class="sxs-lookup"><span data-stu-id="30c46-201">Docs</span></span>

- <span data-ttu-id="30c46-202">Docs for Install příkaz DependencyVersion a Framework příznaky - [#5858](https://github.com/NuGet/Home/issues/5858)</span><span class="sxs-lookup"><span data-stu-id="30c46-202">Docs for Install command DependencyVersion and Framework flags - [#5858](https://github.com/NuGet/Home/issues/5858)</span></span>

- <span data-ttu-id="30c46-203">Aktualizace dokumentů na NuGet upozornění a chyby - [#5857](https://github.com/NuGet/Home/issues/5857)</span><span class="sxs-lookup"><span data-stu-id="30c46-203">Update to docs on NuGet warnings and errors - [#5857](https://github.com/NuGet/Home/issues/5857)</span></span>

## <a name="links-to-github-issues-fixed-in-44-rtm"></a><span data-ttu-id="30c46-204">Odkazy na problémy GitHubu opravené v 4.4 RTM</span><span class="sxs-lookup"><span data-stu-id="30c46-204">Links to GitHub issues fixed in 4.4 RTM</span></span>

[<span data-ttu-id="30c46-205">Seznam problémů 1</span><span class="sxs-lookup"><span data-stu-id="30c46-205">Issues List 1</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[<span data-ttu-id="30c46-206">Seznam problémů 2</span><span class="sxs-lookup"><span data-stu-id="30c46-206">Issues List 2</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[<span data-ttu-id="30c46-207">Seznam problémů 3</span><span class="sxs-lookup"><span data-stu-id="30c46-207">Issues List 3</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
