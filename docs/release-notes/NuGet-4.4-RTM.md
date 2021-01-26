---
title: Poznámky k verzi NuGet 4,4 RTM
description: Poznámky k verzi pro NuGet 4,3 RTM, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 970a920a401b8a74c04d84cbad9933c54e3cd19e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776288"
---
# <a name="nuget-44-release-notes"></a><span data-ttu-id="fab44-103">Zpráva k vydání verze NuGet 4,4</span><span class="sxs-lookup"><span data-stu-id="fab44-103">NuGet 4.4 Release Notes</span></span>

<span data-ttu-id="fab44-104">[Visual Studio 2017 15,4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) obsahuje NUGET 4,4 RTM.</span><span class="sxs-lookup"><span data-stu-id="fab44-104">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.4 RTM.</span></span>

## <a name="summary-whats-new-in-440"></a><span data-ttu-id="fab44-105">Shrnutí: co je nového v 4.4.0</span><span class="sxs-lookup"><span data-stu-id="fab44-105">Summary: What's New in 4.4.0</span></span>

## <a name="summary-whats-new-in-442"></a><span data-ttu-id="fab44-106">Shrnutí: co je nového ve funkci 4.4.2</span><span class="sxs-lookup"><span data-stu-id="fab44-106">Summary: What's New in 4.4.2</span></span>

* <span data-ttu-id="fab44-107">Oprava zabezpečení: oprávnění k souborům vytvořeným uvnitř ~/.NuGet jsou příliš otevřená [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757) .</span><span class="sxs-lookup"><span data-stu-id="fab44-107">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>

## <a name="summary-whats-new-in-443"></a><span data-ttu-id="fab44-108">Shrnutí: co je nového v 4.4.3</span><span class="sxs-lookup"><span data-stu-id="fab44-108">Summary: What's New in 4.4.3</span></span>

* <span data-ttu-id="fab44-109">Oprava zabezpečení: soubory uvnitř NUPKGs můžou mít relativní cestu nad [#7906](https://github.com/NuGet/Home/issues/7906) ADRESÁŘem nupkg.</span><span class="sxs-lookup"><span data-stu-id="fab44-109">Security Fix: Files inside of NUPKGs can have a relative path above the NUPKG directory [#7906](https://github.com/NuGet/Home/issues/7906)</span></span>

## <a name="known-issues"></a><span data-ttu-id="fab44-110">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="fab44-110">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="fab44-111">Problémy s .NET Standard 2,0 s .NET Framework & NuGet</span><span class="sxs-lookup"><span data-stu-id="fab44-111">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="fab44-112">.NET Standard & jeho nástrojů bylo navrženo tak, aby projekty, které cílí na .NET Framework 4.6.1, mohly využívat balíčky NuGet & projektech cílících na .NET Standard 2,0 nebo starší.</span><span class="sxs-lookup"><span data-stu-id="fab44-112">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="fab44-113">[Tento dokument](https://github.com/dotnet/standard/issues/481) shrnuje problémy v tomto scénáři, plán pro jejich adresování a alternativní řešení, která můžete nasadit s dnešním stavem nástrojů.</span><span class="sxs-lookup"><span data-stu-id="fab44-113">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="fab44-114">Při používání konzoly Správce balíčků nemusí fungovat klávesa Enter</span><span class="sxs-lookup"><span data-stu-id="fab44-114">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="fab44-115">Problém</span><span class="sxs-lookup"><span data-stu-id="fab44-115">Issue</span></span>

<span data-ttu-id="fab44-116">V konzole Správce balíčků občas nefunguje klávesa Enter.</span><span class="sxs-lookup"><span data-stu-id="fab44-116">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="fab44-117">Když toto chování zpozorujete, zjistěte prosím, jak to vypadá s opravou, a poskytněte jakékoli další užitečné informace o postupu, jak tuto chybu reprodukovat.</span><span class="sxs-lookup"><span data-stu-id="fab44-117">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="fab44-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="fab44-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="fab44-119">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="fab44-119">Workaround</span></span>

<span data-ttu-id="fab44-120">Před otevřením řešení restartujte Visual Studio a otevřete konzolu PMC.</span><span class="sxs-lookup"><span data-stu-id="fab44-120">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="fab44-121">Případně zkuste `project.lock.json` obnovení a znovu obnovit.</span><span class="sxs-lookup"><span data-stu-id="fab44-121">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="fab44-122">Pomocí Správce balíčků NuGet nemůžete zobrazit, přidat ani aktualizovat DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="fab44-122">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="fab44-123">Problém</span><span class="sxs-lookup"><span data-stu-id="fab44-123">Issue</span></span>

<span data-ttu-id="fab44-124">Správce balíčků NuGet nezobrazuje a nepovoluje přidat nebo aktualizovat DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="fab44-124">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="fab44-125">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="fab44-125">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="fab44-126">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="fab44-126">Workaround</span></span>

<span data-ttu-id="fab44-127">V souboru projektu se musí ručně upravit DotNetCLIToolReferences.</span><span class="sxs-lookup"><span data-stu-id="fab44-127">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="fab44-128">Změna cílení verze cílové architektury může vést k nekompletnímu IntelliSense</span><span class="sxs-lookup"><span data-stu-id="fab44-128">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="fab44-129">Problém</span><span class="sxs-lookup"><span data-stu-id="fab44-129">Issue</span></span>

<span data-ttu-id="fab44-130">Změna cílení verze cílové architektury v sadě Visual Studio může vést k nekompletnímu IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="fab44-130">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="fab44-131">To se stává, když jako formát správce balíčků používáte PackageReferences.</span><span class="sxs-lookup"><span data-stu-id="fab44-131">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="fab44-132">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="fab44-132">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="fab44-133">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="fab44-133">Workaround</span></span>

<span data-ttu-id="fab44-134">Proveďte ruční obnovení.</span><span class="sxs-lookup"><span data-stu-id="fab44-134">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="fab44-135">Balíček v projektu .NET Core, který obsahuje sestavení s neplatným podpisem, může aktivovat nekonečnou smyčku obnovení</span><span class="sxs-lookup"><span data-stu-id="fab44-135">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="fab44-136">Problém</span><span class="sxs-lookup"><span data-stu-id="fab44-136">Issue</span></span>

<span data-ttu-id="fab44-137">Když použijete balíček, který obsahuje sestavení s neplatným podpisem, nebo když je verze balíčku nastavená pomocí časovače DateTime, může při automatickém obnovení balíčku občas vzniknout nekonečná smyčka (dotnet/project-system#1457).</span><span class="sxs-lookup"><span data-stu-id="fab44-137">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop (dotnet/project-system#1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="fab44-138">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="fab44-138">Workaround</span></span>

<span data-ttu-id="fab44-139">Pro tento problém zatím neexistuje alternativní řešení.</span><span class="sxs-lookup"><span data-stu-id="fab44-139">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a><span data-ttu-id="fab44-140">Problémy opravené v časovém rámci NuGet 4,4 RTM</span><span class="sxs-lookup"><span data-stu-id="fab44-140">Issues fixed in NuGet 4.4 RTM timeframe</span></span>

<span data-ttu-id="fab44-141">Zpráva k [vydání verze nuget 4,3 RTM](../release-notes/nuget-4.3-RTM.md) – seznam všech problémů opravených pro NUGET 4,3 RTM</span><span class="sxs-lookup"><span data-stu-id="fab44-141">[NuGet 4.3 RTM Release Notes](../release-notes/nuget-4.3-RTM.md) - Lists all the issues fixed for NuGet 4.3 RTM</span></span>

### <a name="features"></a><span data-ttu-id="fab44-142">Funkce</span><span class="sxs-lookup"><span data-stu-id="fab44-142">Features</span></span>

- <span data-ttu-id="fab44-143">Podpora zjednodušeného načtení řešení ve scénářích uživatelského rozhraní PMC a NuGet PM – [#5180](https://github.com/NuGet/Home/issues/5180)</span><span class="sxs-lookup"><span data-stu-id="fab44-143">Support for Lightweight Solution Load in PMC and NuGet PM UI scenarios - [#5180](https://github.com/NuGet/Home/issues/5180)</span></span>

- <span data-ttu-id="fab44-144">Cíl sady MSBuild Pack musí mít veřejný zavěšení pro spouštění cílových uživatelů před samotným [#5143](https://github.com/NuGet/Home/issues/5143)</span><span class="sxs-lookup"><span data-stu-id="fab44-144">The msbuild pack target should have a public hook for running user targets before itself - [#5143](https://github.com/NuGet/Home/issues/5143)</span></span>

- <span data-ttu-id="fab44-145">Funkce: Přidání přepínače dependencyVersion do instalace NuGet – [#1806](https://github.com/NuGet/Home/issues/1806)</span><span class="sxs-lookup"><span data-stu-id="fab44-145">Feature: Add dependencyVersion switch to nuget install - [#1806](https://github.com/NuGet/Home/issues/1806)</span></span>

- <span data-ttu-id="fab44-146">UAP 10.0. TODO. 0 by se měl mapovat na .NET Standard 2,0 pro NuGet – [#5684](https://github.com/NuGet/Home/issues/5684)</span><span class="sxs-lookup"><span data-stu-id="fab44-146">uap10.0.TODO.0 should map to .NET Standard 2.0 for NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)</span></span>

- <span data-ttu-id="fab44-147">Podpora Visual Studio Build Tools SKU pomocí nástroje MSBuild/t: Restore- [#5562](https://github.com/NuGet/Home/issues/5562)</span><span class="sxs-lookup"><span data-stu-id="fab44-147">Support Visual Studio Build Tools SKU with msbuild /t:restore - [#5562](https://github.com/NuGet/Home/issues/5562)</span></span>

- <span data-ttu-id="fab44-148">Při obnovení vygenerujte chybu, pokud je vyžadována podpora .NET 4.6.1 pro .NET Standard 2,0, ale není nainstalovaná – [#5325](https://github.com/NuGet/Home/issues/5325)</span><span class="sxs-lookup"><span data-stu-id="fab44-148">During restore, generate an error if .NET 4.6.1 support for .NET Standard 2.0 is required but not installed - [#5325](https://github.com/NuGet/Home/issues/5325)</span></span>

- <span data-ttu-id="fab44-149">Uživatelské rozhraní klienta rezervace předpony ID balíčku – [#5572](https://github.com/NuGet/Home/issues/5572)</span><span class="sxs-lookup"><span data-stu-id="fab44-149">Package ID prefix reservation client UI - [#5572](https://github.com/NuGet/Home/issues/5572)</span></span>

- <span data-ttu-id="fab44-150">doručovat lokalizované součásti NuGet, aby podporovaly dotnet.exe lokalizace [#4336](https://github.com/NuGet/Home/issues/4336)</span><span class="sxs-lookup"><span data-stu-id="fab44-150">deliver localized nuget components to support dotnet.exe localization - [#4336](https://github.com/NuGet/Home/issues/4336)</span></span>

### <a name="bugs"></a><span data-ttu-id="fab44-151">Chyby</span><span class="sxs-lookup"><span data-stu-id="fab44-151">Bugs</span></span>

- <span data-ttu-id="fab44-152">Různá písmena v cestě k projektu můžou způsobit ztrátu PackageReferences [#5855](https://github.com/NuGet/Home/issues/5855)</span><span class="sxs-lookup"><span data-stu-id="fab44-152">Different project path casings can cause restore to lose PackageReferences - [#5855](https://github.com/NuGet/Home/issues/5855)</span></span>

- <span data-ttu-id="fab44-153">Přesunout kódy chyb s čísly upozornění do rozsahu chyb – [#5824](https://github.com/NuGet/Home/issues/5824)</span><span class="sxs-lookup"><span data-stu-id="fab44-153">Move error codes with warning numbers to error range - [#5824](https://github.com/NuGet/Home/issues/5824)</span></span>

- <span data-ttu-id="fab44-154">Zavádějící chyba, pokud .NET Standard verze není známa jako kompatibilní s cílovou architekturou- [#5818](https://github.com/NuGet/Home/issues/5818)</span><span class="sxs-lookup"><span data-stu-id="fab44-154">Misleading error when .NET Standard version is not known to be compatible with target framework  - [#5818](https://github.com/NuGet/Home/issues/5818)</span></span>

- <span data-ttu-id="fab44-155">Testovací soubory s nematoucími licencemi – [#5776](https://github.com/NuGet/Home/issues/5776)</span><span class="sxs-lookup"><span data-stu-id="fab44-155">Test files with confusing licenses - [#5776](https://github.com/NuGet/Home/issues/5776)</span></span>

- <span data-ttu-id="fab44-156">Chybějící hlavičky licencí v šablonách testů EndToEnd – [#5774](https://github.com/NuGet/Home/issues/5774)</span><span class="sxs-lookup"><span data-stu-id="fab44-156">Missing license headers in EndToEnd test templates - [#5774](https://github.com/NuGet/Home/issues/5774)</span></span>

- <span data-ttu-id="fab44-157">packages.config Restore zobrazuje chyby jako NU1000- [#5743](https://github.com/NuGet/Home/issues/5743)</span><span class="sxs-lookup"><span data-stu-id="fab44-157">packages.config restore shows errors as NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)</span></span>

- <span data-ttu-id="fab44-158">nuget.exe instalace by měla mít DisableParallelProcessing na mono- [#5741](https://github.com/NuGet/Home/issues/5741)</span><span class="sxs-lookup"><span data-stu-id="fab44-158">nuget.exe install should have DisableParallelProcessing on mono - [#5741](https://github.com/NuGet/Home/issues/5741)</span></span>

- <span data-ttu-id="fab44-159">nuget.exe instalace nesprávně zakáže ukládání do mezipaměti – [#5737](https://github.com/NuGet/Home/issues/5737)</span><span class="sxs-lookup"><span data-stu-id="fab44-159">nuget.exe install incorrectly disables caching - [#5737](https://github.com/NuGet/Home/issues/5737)</span></span>

- <span data-ttu-id="fab44-160">VS spuštění příkazu RESTORE pro packages.config při zakázaném obnovení zobrazuje nesprávnou zprávu- [#5718](https://github.com/NuGet/Home/issues/5718)</span><span class="sxs-lookup"><span data-stu-id="fab44-160">VS Running the restore command for packages.config when Restore is disabled displays incorrect message  - [#5718](https://github.com/NuGet/Home/issues/5718)</span></span>

- <span data-ttu-id="fab44-161">INFRASTRUKTURA Spuštění příkazu RESTORE v případě zakázaného obnovení zobrazí nematoucí zprávu [#5659](https://github.com/NuGet/Home/issues/5659)</span><span class="sxs-lookup"><span data-stu-id="fab44-161">VS; Running the restore command when Restore is disabled displays a confusing message - [#5659](https://github.com/NuGet/Home/issues/5659)</span></span>

- <span data-ttu-id="fab44-162">GetRestoreDotnetCliToolsTask se nezdařila, pokud chybí metadata verze – [#5716](https://github.com/NuGet/Home/issues/5716)</span><span class="sxs-lookup"><span data-stu-id="fab44-162">GetRestoreDotnetCliToolsTask fails when missing version metadata - [#5716](https://github.com/NuGet/Home/issues/5716)</span></span>

- <span data-ttu-id="fab44-163">dotnet</span><span class="sxs-lookup"><span data-stu-id="fab44-163">dotnet</span></span>
  - <span data-ttu-id="fab44-164">dotnetcore přidat balíček může vymazat prázdné řádky z csproj- [#5697](https://github.com/NuGet/Home/issues/5697)</span><span class="sxs-lookup"><span data-stu-id="fab44-164">dotnetcore add package can clear empty lines from a csproj  - [#5697](https://github.com/NuGet/Home/issues/5697)</span></span>

- <span data-ttu-id="fab44-165">Názvy zdrojů nastavení přihlašovacích údajů v NuGet.Config rozlišují velká a malá písmena – [#5695](https://github.com/NuGet/Home/issues/5695)</span><span class="sxs-lookup"><span data-stu-id="fab44-165">Source names of credential settings in NuGet.Config are case sensitive - [#5695](https://github.com/NuGet/Home/issues/5695)</span></span>

- <span data-ttu-id="fab44-166">Povolení GeneratePackageOnBuild odstranilo celou historii balíčků – [#5676](https://github.com/NuGet/Home/issues/5676)</span><span class="sxs-lookup"><span data-stu-id="fab44-166">Enabling GeneratePackageOnBuild deleted my entire history of packages - [#5676](https://github.com/NuGet/Home/issues/5676)</span></span>

- <span data-ttu-id="fab44-167">Při obnovení se neobnoví balíčky mono. Cecil nebo semver, ale všechny ostatní balíčky se obnoví.</span><span class="sxs-lookup"><span data-stu-id="fab44-167">Restore will not restore mono.cecil or semver packages, but all other packages get restored.</span></span><span data-ttu-id="fab44-168"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span><span class="sxs-lookup"><span data-stu-id="fab44-168"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span></span>

- <span data-ttu-id="fab44-169">Chyby a upozornění – chybná chyba, pokud zdroj není k dispozici.</span><span class="sxs-lookup"><span data-stu-id="fab44-169">Errors and Warnings - bad error when a source in unavailable.</span></span><span data-ttu-id="fab44-170">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span><span class="sxs-lookup"><span data-stu-id="fab44-170">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span></span>

- <span data-ttu-id="fab44-171">[DesignConsistency] Text stavu instalace NuGet nevypadá v současné době v tmavém motivu správně.</span><span class="sxs-lookup"><span data-stu-id="fab44-171">[DesignConsistency] NuGet Installation status text doesn’t look correct on dark theme currently.</span></span><span data-ttu-id="fab44-172"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span><span class="sxs-lookup"><span data-stu-id="fab44-172"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span></span>

- <span data-ttu-id="fab44-173">Aktualizace balíčků v řešení aktualizace/instalace pro všechny projekty – [#5508](https://github.com/NuGet/Home/issues/5508)</span><span class="sxs-lookup"><span data-stu-id="fab44-173">Update packages at solution updates/installs for all the projects - [#5508](https://github.com/NuGet/Home/issues/5508)</span></span>

- <span data-ttu-id="fab44-174">dotnet</span><span class="sxs-lookup"><span data-stu-id="fab44-174">dotnet</span></span>
  - <span data-ttu-id="fab44-175">sada dotnetcore Pack se chová odlišně v závislosti na TargetFramework a TargetFramework – [#5281](https://github.com/NuGet/Home/issues/5281)</span><span class="sxs-lookup"><span data-stu-id="fab44-175">dotnetcore pack behaves differently depending on TargetFramework vs TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)</span></span>

- <span data-ttu-id="fab44-176">Zahrnuté knihovny DLL ve složce nástroje vyvolávají upozornění – [#5020](https://github.com/NuGet/Home/issues/5020)</span><span class="sxs-lookup"><span data-stu-id="fab44-176">Included DLLs inside Tools folder throw warnings - [#5020](https://github.com/NuGet/Home/issues/5020)</span></span>

- <span data-ttu-id="fab44-177">NuGet. ContentModel spotřebovává pro řetězcové operace příliš mnoho paměti – [#4714](https://github.com/NuGet/Home/issues/4714)</span><span class="sxs-lookup"><span data-stu-id="fab44-177">NuGet.ContentModel consumes too much memory for string operations - [#4714](https://github.com/NuGet/Home/issues/4714)</span></span>

- <span data-ttu-id="fab44-178">RuntimeEnvironmentHelper. pro Linux vrátí hodnotu true pro OSX- [#4648](https://github.com/NuGet/Home/issues/4648)</span><span class="sxs-lookup"><span data-stu-id="fab44-178">RuntimeEnvironmentHelper.IsLinux returns true for OSX - [#4648](https://github.com/NuGet/Home/issues/4648)</span></span>

- <span data-ttu-id="fab44-179">příkaz dotnet Pack vloží nuspec do obj místo obj\Debug- [#4644](https://github.com/NuGet/Home/issues/4644)</span><span class="sxs-lookup"><span data-stu-id="fab44-179">'dotnet pack' puts nuspec under obj instead of obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)</span></span>

- <span data-ttu-id="fab44-180">Vysoce pomalý upgrade balíčku NuGet – [#4534](https://github.com/NuGet/Home/issues/4534)</span><span class="sxs-lookup"><span data-stu-id="fab44-180">Nuget extremely slow package upgrade - [#4534](https://github.com/NuGet/Home/issues/4534)</span></span>

- <span data-ttu-id="fab44-181">Služba CPS není synchronizovaná s obnovením s většími řešeními, která nebyla zapnutá LSL (zjednodušené obnovení řešení) – [#4307](https://github.com/NuGet/Home/issues/4307)</span><span class="sxs-lookup"><span data-stu-id="fab44-181">CPS out of sync with Restore with larger solutions that haven't turned on LSL (lightweight solution restore) - [#4307](https://github.com/NuGet/Home/issues/4307)</span></span>

- <span data-ttu-id="fab44-182">SemVer 2,0 – balíček NuGet s poskytnutou verzí ignoruje metadata (3.5.0-RTM-1938) – [#3643](https://github.com/NuGet/Home/issues/3643)</span><span class="sxs-lookup"><span data-stu-id="fab44-182">SemVer 2.0 - nuget pack with provided version ignores metadata (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)</span></span>

- <span data-ttu-id="fab44-183">Nuget.exe (3. +) instalovat balíček s číslem verze a příznakem ExcludeVersion neaktualizuje balíček na novější verzi. [#2405](https://github.com/NuGet/Home/issues/2405)</span><span class="sxs-lookup"><span data-stu-id="fab44-183">Nuget.exe (3.+) install package with Version number and ExcludeVersion flag doesn't update package to newer version - [#2405](https://github.com/NuGet/Home/issues/2405)</span></span>

- <span data-ttu-id="fab44-184">Project.jspři obnovení by měla upozorňovat na porušení omezení balíčků nejvyšší úrovně – [#2358](https://github.com/NuGet/Home/issues/2358)</span><span class="sxs-lookup"><span data-stu-id="fab44-184">Project.json restore should warn when top-level packages violate constraints - [#2358](https://github.com/NuGet/Home/issues/2358)</span></span>

- <span data-ttu-id="fab44-185">– ConfigFile nenastavuje vlastní konfiguraci příkazu install- [#1646](https://github.com/NuGet/Home/issues/1646)</span><span class="sxs-lookup"><span data-stu-id="fab44-185">-ConfigFile is not setting custom config on install command - [#1646](https://github.com/NuGet/Home/issues/1646)</span></span>

- <span data-ttu-id="fab44-186">nuget.exe instalace nedodržuje přepínač-DisableParallelProcessing- [#1556](https://github.com/NuGet/Home/issues/1556)</span><span class="sxs-lookup"><span data-stu-id="fab44-186">nuget.exe install does not honor '-DisableParallelProcessing' switch - [#1556](https://github.com/NuGet/Home/issues/1556)</span></span>

- <span data-ttu-id="fab44-187">Zakázané zdroje pořád používané DotNet.exe nebo msbuild.exe- [#5704](https://github.com/NuGet/Home/issues/5704)</span><span class="sxs-lookup"><span data-stu-id="fab44-187">Disabled sources still used by DotNet.exe or msbuild.exe - [#5704](https://github.com/NuGet/Home/issues/5704)</span></span>

- <span data-ttu-id="fab44-188">Oprava chyb ve scénáři LSL – [#5685](https://github.com/NuGet/Home/issues/5685)</span><span class="sxs-lookup"><span data-stu-id="fab44-188">Fix hangs in LSL scenario - [#5685](https://github.com/NuGet/Home/issues/5685)</span></span>

### <a name="dcrs"></a><span data-ttu-id="fab44-189">Chcete odeslat obecnou</span><span class="sxs-lookup"><span data-stu-id="fab44-189">DCRs</span></span>

- <span data-ttu-id="fab44-190">nuget.exe instalaci podpory TargetFramework – [#5736](https://github.com/NuGet/Home/issues/5736)</span><span class="sxs-lookup"><span data-stu-id="fab44-190">nuget.exe install TargetFramework support - [#5736](https://github.com/NuGet/Home/issues/5736)</span></span>

- <span data-ttu-id="fab44-191">Přidejte různé řetězce UserAgent úlohy MSBuild (Netcore vs Desktop MSBuild) – [#5709](https://github.com/NuGet/Home/issues/5709)</span><span class="sxs-lookup"><span data-stu-id="fab44-191">Add different msbuild task UserAgent strings (netcore vs desktop msbuild) - [#5709](https://github.com/NuGet/Home/issues/5709)</span></span>

- <span data-ttu-id="fab44-192">PackagePathResolver. GetPackageDirectoryName by měl být Virtual- [#5700](https://github.com/NuGet/Home/issues/5700)</span><span class="sxs-lookup"><span data-stu-id="fab44-192">PackagePathResolver.GetPackageDirectoryName should be virtual - [#5700](https://github.com/NuGet/Home/issues/5700)</span></span>

- <span data-ttu-id="fab44-193">[DesignConsistency] Matoucí zpráva při přidávání balíčku NuGet – [#5641](https://github.com/NuGet/Home/issues/5641)</span><span class="sxs-lookup"><span data-stu-id="fab44-193">[DesignConsistency] Confusing message when adding a NuGet package - [#5641](https://github.com/NuGet/Home/issues/5641)</span></span>

- <span data-ttu-id="fab44-194">[Upozornění a chyby] Žádné upozornění neprobíhá přes odkazy na P2P na cestě. [#5501](https://github.com/NuGet/Home/issues/5501)</span><span class="sxs-lookup"><span data-stu-id="fab44-194">[Warnings and errors] NoWarn does not flow transitively through P2P references - [#5501](https://github.com/NuGet/Home/issues/5501)</span></span>

- <span data-ttu-id="fab44-195">Zjednodušené načtení řešení: Common Core for PM UI, PMC a Ideographic-- [#5057](https://github.com/NuGet/Home/issues/5057)</span><span class="sxs-lookup"><span data-stu-id="fab44-195">Lightweight Solution Load: Common Core for PM UI, PMC, and IVs- - [#5057](https://github.com/NuGet/Home/issues/5057)</span></span>

- <span data-ttu-id="fab44-196">Zjednodušené načtení řešení: support-PMC- [#5053](https://github.com/NuGet/Home/issues/5053)</span><span class="sxs-lookup"><span data-stu-id="fab44-196">Lightweight Solution Load: Support - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)</span></span>

- <span data-ttu-id="fab44-197">Přidání podpory pro předem obnovený cíl MSBuild, který spouští Visual Studio – [#4781](https://github.com/NuGet/Home/issues/4781)</span><span class="sxs-lookup"><span data-stu-id="fab44-197">Add support for pre-restore MSBuild target that Visual Studio triggers - [#4781](https://github.com/NuGet/Home/issues/4781)</span></span>

- <span data-ttu-id="fab44-198">Přidejte veřejný cíl do NuGet. cíle, na které se dá odkazovat pomocí BeforeTargets- [#4634](https://github.com/NuGet/Home/issues/4634)</span><span class="sxs-lookup"><span data-stu-id="fab44-198">Add a public target to NuGet.targets that can be referenced using BeforeTargets - [#4634](https://github.com/NuGet/Home/issues/4634)</span></span>

- <span data-ttu-id="fab44-199">Cíl sady Pack nemůže vytvořit contentFiles s akcemi sestavení správně – [#4166](https://github.com/NuGet/Home/issues/4166)</span><span class="sxs-lookup"><span data-stu-id="fab44-199">Pack target can't create contentFiles with build actions correctly - [#4166](https://github.com/NuGet/Home/issues/4166)</span></span>

- <span data-ttu-id="fab44-200">Vlákna fondu vláken RestoreOperationLogger.Do bloků vlákna – [#5663](https://github.com/NuGet/Home/issues/5663)</span><span class="sxs-lookup"><span data-stu-id="fab44-200">RestoreOperationLogger.Do blocks thread pool threads - [#5663](https://github.com/NuGet/Home/issues/5663)</span></span>

### <a name="docs"></a><span data-ttu-id="fab44-201">Docs</span><span class="sxs-lookup"><span data-stu-id="fab44-201">Docs</span></span>

- <span data-ttu-id="fab44-202">Dokumentace k příkazům DependencyVersion pro instalaci a příznaky rozhraní – [#5858](https://github.com/NuGet/Home/issues/5858)</span><span class="sxs-lookup"><span data-stu-id="fab44-202">Docs for Install command DependencyVersion and Framework flags - [#5858](https://github.com/NuGet/Home/issues/5858)</span></span>

- <span data-ttu-id="fab44-203">Aktualizace na dokumenty s upozorněními a chybami NuGet – [#5857](https://github.com/NuGet/Home/issues/5857)</span><span class="sxs-lookup"><span data-stu-id="fab44-203">Update to docs on NuGet warnings and errors - [#5857](https://github.com/NuGet/Home/issues/5857)</span></span>

## <a name="links-to-github-issues-fixed-in-44-rtm"></a><span data-ttu-id="fab44-204">Odkazy na problémy GitHubu opravené ve 4,4 RTM</span><span class="sxs-lookup"><span data-stu-id="fab44-204">Links to GitHub issues fixed in 4.4 RTM</span></span>

[<span data-ttu-id="fab44-205">Seznam problémů 1</span><span class="sxs-lookup"><span data-stu-id="fab44-205">Issues List 1</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[<span data-ttu-id="fab44-206">Seznam problémů 2</span><span class="sxs-lookup"><span data-stu-id="fab44-206">Issues List 2</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[<span data-ttu-id="fab44-207">Seznam problémů 3</span><span class="sxs-lookup"><span data-stu-id="fab44-207">Issues List 3</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
