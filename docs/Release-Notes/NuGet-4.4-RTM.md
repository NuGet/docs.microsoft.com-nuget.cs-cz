---
title: "Poznámky k verzi RTM NuGet 4.4 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: unniravindranathan
ms.date: 08/14/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 5ffca6f6-a126-4407-b22f-1323e7dc44a3
description: "Poznámky k verzi pro NuGet 4.3 RTM, včetně známé problémy, opravy chyb, přidaných funkcí a chcete."
keywords: "NuGet 4.3 RTM poznámky k verzi, opravy chyb známé problémy, přidat funkce, chcete"
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: 479f14db0b402476eccab23283a029a839cf51dd
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="44-rtm-release-notes"></a><span data-ttu-id="7d686-104">4.4 poznámky k verzi RTM</span><span class="sxs-lookup"><span data-stu-id="7d686-104">4.4 RTM Release Notes</span></span>

<span data-ttu-id="7d686-105">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) se dodává s NuGet 4.4 RTM.</span><span class="sxs-lookup"><span data-stu-id="7d686-105">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.4 RTM.</span></span>

## <a name="known-issues"></a><span data-ttu-id="7d686-106">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="7d686-106">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="7d686-107">Problémy s .NET standardní 2.0 pomocí rozhraní .NET Framework & NuGet</span><span class="sxs-lookup"><span data-stu-id="7d686-107">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 
<span data-ttu-id="7d686-108">.NET standard & jeho nástrojů je navržené tak, aby projektech zacílených na rozhraní .NET Framework 4.6.1 může využívat balíčky NuGet & projektech zacílených na standardní rozhraní .NET 2.0 nebo dřívější.</span><span class="sxs-lookup"><span data-stu-id="7d686-108">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="7d686-109">[Tento dokument](https://github.com/dotnet/standard/issues/481) shrnuje problémy kolem tento scénář, plán pro adresování a alternativní řešení můžete nasadit s je aktuální stav nástrojů.</span><span class="sxs-lookup"><span data-stu-id="7d686-109">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="7d686-110">Při používání konzoly Správce balíčků nemusí fungovat klávesa Enter</span><span class="sxs-lookup"><span data-stu-id="7d686-110">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="7d686-111">Problém:</span><span class="sxs-lookup"><span data-stu-id="7d686-111">Issue:</span></span>
<span data-ttu-id="7d686-112">V konzole Správce balíčků občas nefunguje klávesa Enter.</span><span class="sxs-lookup"><span data-stu-id="7d686-112">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="7d686-113">Když toto chování zpozorujete, zjistěte prosím, jak to vypadá s opravou, a poskytněte jakékoli další užitečné informace o postupu, jak tuto chybu reprodukovat.</span><span class="sxs-lookup"><span data-stu-id="7d686-113">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="7d686-114">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="7d686-114">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="7d686-115">Alternativní řešení:</span><span class="sxs-lookup"><span data-stu-id="7d686-115">Workaround:</span></span>
<span data-ttu-id="7d686-116">Před otevřením řešení restartujte Visual Studio a otevřete konzolu PMC.</span><span class="sxs-lookup"><span data-stu-id="7d686-116">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="7d686-117">Případně, zkuste odstranit `project.lock.json` a opakujte obnovení.</span><span class="sxs-lookup"><span data-stu-id="7d686-117">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-will-be-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="7d686-118">Pomocí Správce balíčků Nuget nebudete moct zobrazit, přidat ani aktualizovat DotNetCLITools</span><span class="sxs-lookup"><span data-stu-id="7d686-118">You will be unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="7d686-119">Problém:</span><span class="sxs-lookup"><span data-stu-id="7d686-119">Issue:</span></span>
<span data-ttu-id="7d686-120">Správce balíčků NuGet nezobrazuje a nepovoluje přidat nebo aktualizovat DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="7d686-120">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="7d686-121">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="7d686-121">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="7d686-122">Alternativní řešení:</span><span class="sxs-lookup"><span data-stu-id="7d686-122">Workaround:</span></span>
<span data-ttu-id="7d686-123">V souboru projektu se musí ručně upravit DotNetCLIToolReferences.</span><span class="sxs-lookup"><span data-stu-id="7d686-123">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="7d686-124">Změna cílení cílové verze rozhraní může vést k nekompletnímu IntelliSense</span><span class="sxs-lookup"><span data-stu-id="7d686-124">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="7d686-125">Problém:</span><span class="sxs-lookup"><span data-stu-id="7d686-125">Issue:</span></span>
<span data-ttu-id="7d686-126">Změna cílení cílové verze rozhraní v sadě Visual Studio může vést k nekompletnímu IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="7d686-126">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="7d686-127">To se stává, když jako formát správce balíčků používáte PackageReferences.</span><span class="sxs-lookup"><span data-stu-id="7d686-127">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="7d686-128">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="7d686-128">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="7d686-129">Alternativní řešení:</span><span class="sxs-lookup"><span data-stu-id="7d686-129">Workaround:</span></span>
<span data-ttu-id="7d686-130">Proveďte ruční obnovení.</span><span class="sxs-lookup"><span data-stu-id="7d686-130">Do a manual restore.</span></span>


### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="7d686-131">Balíček v projektu .NET Core, který obsahuje sestavení s neplatným podpisem, může aktivovat nekonečnou smyčku obnovení</span><span class="sxs-lookup"><span data-stu-id="7d686-131">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="7d686-132">Problém:</span><span class="sxs-lookup"><span data-stu-id="7d686-132">Issue:</span></span>
<span data-ttu-id="7d686-133">V některých případech použijete-li balíček, který obsahuje sestavení s neplatným podpisem nebo pokud verze balíčku nastavena, DateTime, burzovní, způsobí auto obnovení balíčku ke spuštění v nekonečné smyčce (dotnet projektu – systém #1457).</span><span class="sxs-lookup"><span data-stu-id="7d686-133">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop (dotnet/project-system#1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="7d686-134">Alternativní řešení:</span><span class="sxs-lookup"><span data-stu-id="7d686-134">Workaround:</span></span>
<span data-ttu-id="7d686-135">Pro tento problém zatím neexistuje alternativní řešení.</span><span class="sxs-lookup"><span data-stu-id="7d686-135">There is no workaround at this time.</span></span>


## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a><span data-ttu-id="7d686-136">Chyby v období NuGet 4.4 RTM</span><span class="sxs-lookup"><span data-stu-id="7d686-136">Issues fixed in NuGet 4.4 RTM timeframe</span></span>

<span data-ttu-id="7d686-137">[K vydání verze RTM 4.3 NuGet](../release-notes/nuget-4.3-RTM.md) -obsahuje seznam všech chyb odstraněných NuGet 4.3 RTM</span><span class="sxs-lookup"><span data-stu-id="7d686-137">[NuGet 4.3 RTM Release Notes](../release-notes/nuget-4.3-RTM.md) - Lists all the issues fixed for NuGet 4.3 RTM</span></span>

<span data-ttu-id="7d686-138">**Funkce:**</span><span class="sxs-lookup"><span data-stu-id="7d686-138">**Feature:**</span></span>

* <span data-ttu-id="7d686-139">Podpora pro zatížení řešení Lightweight ve scénářích NuGet PM uživatelského rozhraní a pomocí PMC - [#5180](https://github.com/NuGet/Home/issues/5180)</span><span class="sxs-lookup"><span data-stu-id="7d686-139">Support for Lightweight Solution Load in PMC and NuGet PM UI scenarios - [#5180](https://github.com/NuGet/Home/issues/5180)</span></span>

* <span data-ttu-id="7d686-140">Cíle msbuild pack musí mít veřejný háku pro spuštěné cíle uživatele před samotné - [#5143](https://github.com/NuGet/Home/issues/5143)</span><span class="sxs-lookup"><span data-stu-id="7d686-140">The msbuild pack target should have a public hook for running user targets before itself - [#5143](https://github.com/NuGet/Home/issues/5143)</span></span>

* <span data-ttu-id="7d686-141">Funkce: Přidání přepínače dependencyVersion k instalaci nuget - [#1806](https://github.com/NuGet/Home/issues/1806)</span><span class="sxs-lookup"><span data-stu-id="7d686-141">Feature: Add dependencyVersion switch to nuget install - [#1806](https://github.com/NuGet/Home/issues/1806)</span></span>

* <span data-ttu-id="7d686-142">uap10.0.todo.0 by měla být mapována na rozhraní .NET 2.0 standardní pro NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)</span><span class="sxs-lookup"><span data-stu-id="7d686-142">uap10.0.TODO.0 should map to .NET Standard 2.0 for NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)</span></span>

* <span data-ttu-id="7d686-143">Podporovat Visual Studio sestavení SKU nástroje msbuild /t:restore - [#5562](https://github.com/NuGet/Home/issues/5562)</span><span class="sxs-lookup"><span data-stu-id="7d686-143">Support Visual Studio Build Tools SKU with msbuild /t:restore - [#5562](https://github.com/NuGet/Home/issues/5562)</span></span>

* <span data-ttu-id="7d686-144">Během obnovení, generuje chybu, pokud .NET 4.6.1 podpora pro standardní rozhraní .NET 2.0 je vyžadována, ale není nainstalován - [#5325](https://github.com/NuGet/Home/issues/5325)</span><span class="sxs-lookup"><span data-stu-id="7d686-144">During restore, generate an error if .NET 4.6.1 support for .NET Standard 2.0 is required but not installed - [#5325](https://github.com/NuGet/Home/issues/5325)</span></span>

* <span data-ttu-id="7d686-145">Balíček ID předponu rezervace uživatelské rozhraní klienta - [#5572](https://github.com/NuGet/Home/issues/5572)</span><span class="sxs-lookup"><span data-stu-id="7d686-145">Package ID prefix reservation client UI - [#5572](https://github.com/NuGet/Home/issues/5572)</span></span>

* <span data-ttu-id="7d686-146">poskytovat lokalizované nuget součásti pro podporu dotnet.exe lokalizace - [#4336](https://github.com/NuGet/Home/issues/4336)</span><span class="sxs-lookup"><span data-stu-id="7d686-146">deliver localized nuget components to support dotnet.exe localization - [#4336](https://github.com/NuGet/Home/issues/4336)</span></span>

<span data-ttu-id="7d686-147">**Chyba:**</span><span class="sxs-lookup"><span data-stu-id="7d686-147">**Bug:**</span></span>

* <span data-ttu-id="7d686-148">Skříně cesty jiný projekt může způsobit ztrátu PackageReferences - obnovení [#5855](https://github.com/NuGet/Home/issues/5855)</span><span class="sxs-lookup"><span data-stu-id="7d686-148">Different project path casings can cause restore to lose PackageReferences - [#5855](https://github.com/NuGet/Home/issues/5855)</span></span>

* <span data-ttu-id="7d686-149">Přesunout kódy chyb s čísla upozornění na rozsah chyba - [#5824](https://github.com/NuGet/Home/issues/5824)</span><span class="sxs-lookup"><span data-stu-id="7d686-149">Move error codes with warning numbers to error range - [#5824](https://github.com/NuGet/Home/issues/5824)</span></span>

* <span data-ttu-id="7d686-150">Oklamání chyba, když se ví, .NET Standard verze není kompatibilní s cílové rozhraní - [#5818](https://github.com/NuGet/Home/issues/5818)</span><span class="sxs-lookup"><span data-stu-id="7d686-150">Misleading error when .NET Standard version is not known to be compatible with target framework  - [#5818](https://github.com/NuGet/Home/issues/5818)</span></span>

* <span data-ttu-id="7d686-151">Testování souborů s licencí matoucí - [#5776](https://github.com/NuGet/Home/issues/5776)</span><span class="sxs-lookup"><span data-stu-id="7d686-151">Test files with confusing licenses - [#5776](https://github.com/NuGet/Home/issues/5776)</span></span>

* <span data-ttu-id="7d686-152">Chybí záhlaví licencí v EndToEnd testování šablony - [#5774](https://github.com/NuGet/Home/issues/5774)</span><span class="sxs-lookup"><span data-stu-id="7d686-152">Missing license headers in EndToEnd test templates - [#5774](https://github.com/NuGet/Home/issues/5774)</span></span>

* <span data-ttu-id="7d686-153">obnovení souboru Packages.config zobrazuje chyby jako NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)</span><span class="sxs-lookup"><span data-stu-id="7d686-153">packages.config restore shows errors as NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)</span></span>

* <span data-ttu-id="7d686-154">instalace nuget.exe by měl mít DisableParallelProcessing na mono - [#5741](https://github.com/NuGet/Home/issues/5741)</span><span class="sxs-lookup"><span data-stu-id="7d686-154">nuget.exe install should have DisableParallelProcessing on mono - [#5741](https://github.com/NuGet/Home/issues/5741)</span></span>

* <span data-ttu-id="7d686-155">instalace nuget.exe nesprávně zakáže ukládání do mezipaměti - [#5737](https://github.com/NuGet/Home/issues/5737)</span><span class="sxs-lookup"><span data-stu-id="7d686-155">nuget.exe install incorrectly disables caching - [#5737](https://github.com/NuGet/Home/issues/5737)</span></span>

* <span data-ttu-id="7d686-156">Spuštění příkazu restore pro zobrazení souboru packages.config, když je obnovení zakázáno nesprávný zpráva – VS [#5718](https://github.com/NuGet/Home/issues/5718)</span><span class="sxs-lookup"><span data-stu-id="7d686-156">VS Running the restore command for packages.config when Restore is disabled displays incorrect message  - [#5718](https://github.com/NuGet/Home/issues/5718)</span></span>

* <span data-ttu-id="7d686-157">VS; Spuštění příkazu restore, když je obnovení zakázáno zobrazí zprávu matoucí - [#5659](https://github.com/NuGet/Home/issues/5659)</span><span class="sxs-lookup"><span data-stu-id="7d686-157">VS; Running the restore command when Restore is disabled displays a confusing message - [#5659](https://github.com/NuGet/Home/issues/5659)</span></span>

* <span data-ttu-id="7d686-158">GetRestoreDotnetCliToolsTask selže, pokud chybí metadata verze - [#5716](https://github.com/NuGet/Home/issues/5716)</span><span class="sxs-lookup"><span data-stu-id="7d686-158">GetRestoreDotnetCliToolsTask fails when missing version metadata - [#5716](https://github.com/NuGet/Home/issues/5716)</span></span>

* <span data-ttu-id="7d686-159">DotNet přidat balíček můžete vymazat prázdné řádky z csproj - [#5697](https://github.com/NuGet/Home/issues/5697)</span><span class="sxs-lookup"><span data-stu-id="7d686-159">dotnet add package can clear empty lines from a csproj  - [#5697](https://github.com/NuGet/Home/issues/5697)</span></span>

* <span data-ttu-id="7d686-160">Názvy zdrojů nastavení přihlašovacích údajů do souboru NuGet.Config jsou velká a malá písmena - [#5695](https://github.com/NuGet/Home/issues/5695)</span><span class="sxs-lookup"><span data-stu-id="7d686-160">Source names of credential settings in NuGet.Config are case sensitive - [#5695](https://github.com/NuGet/Home/issues/5695)</span></span>

* <span data-ttu-id="7d686-161">Povolení GeneratePackageOnBuild odstranit mé celou historii balíčků - [#5676](https://github.com/NuGet/Home/issues/5676)</span><span class="sxs-lookup"><span data-stu-id="7d686-161">Enabling GeneratePackageOnBuild deleted my entire history of packages - [#5676](https://github.com/NuGet/Home/issues/5676)</span></span>

* <span data-ttu-id="7d686-162">Obnovení nebude možné obnovit mono.cecil nebo semver balíčků, ale všechny ostatní balíčky získat obnovit.</span><span class="sxs-lookup"><span data-stu-id="7d686-162">Restore will not restore mono.cecil or semver packages, but all other packages get restored.</span></span><span data-ttu-id="7d686-163"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span><span class="sxs-lookup"><span data-stu-id="7d686-163"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span></span>

* <span data-ttu-id="7d686-164">Chyby a upozornění - chybný při zdroji v není k dispozici.</span><span class="sxs-lookup"><span data-stu-id="7d686-164">Errors and Warnings - bad error when a source in unavailable.</span></span><span data-ttu-id="7d686-165">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span><span class="sxs-lookup"><span data-stu-id="7d686-165">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span></span>

* <span data-ttu-id="7d686-166">[DesignConsistency] Text stav instalace NuGet nevypadá aktuálně správné na tmavým motivem.</span><span class="sxs-lookup"><span data-stu-id="7d686-166">[DesignConsistency] NuGet Installation status text doesn’t look correct on dark theme currently.</span></span><span data-ttu-id="7d686-167"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span><span class="sxs-lookup"><span data-stu-id="7d686-167"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span></span>

* <span data-ttu-id="7d686-168">Aktualizovat balíčky v řešení aktualizací nebo instalace pro všechny projekty - [#5508](https://github.com/NuGet/Home/issues/5508)</span><span class="sxs-lookup"><span data-stu-id="7d686-168">Update packages at solution updates/installs for all the projects - [#5508](https://github.com/NuGet/Home/issues/5508)</span></span>

* <span data-ttu-id="7d686-169">DotNet pack chová odlišně v závislosti na TargetFramework vs TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)</span><span class="sxs-lookup"><span data-stu-id="7d686-169">dotnet pack behaves differently depending on TargetFramework vs TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)</span></span>

* <span data-ttu-id="7d686-170">Knihovny DLL zahrnuty do vnitřní nástroje složky throw upozornění - [#5020](https://github.com/NuGet/Home/issues/5020)</span><span class="sxs-lookup"><span data-stu-id="7d686-170">Included DLLs inside Tools folder throw warnings - [#5020](https://github.com/NuGet/Home/issues/5020)</span></span>

* <span data-ttu-id="7d686-171">NuGet.ContentModel využívá příliš mnoho paměti pro operace s řetězci - [#4714](https://github.com/NuGet/Home/issues/4714)</span><span class="sxs-lookup"><span data-stu-id="7d686-171">NuGet.ContentModel consumes too much memory for string operations - [#4714](https://github.com/NuGet/Home/issues/4714)</span></span>

* <span data-ttu-id="7d686-172">RuntimeEnvironmentHelper.IsLinux vrátí hodnotu true pro OSX - [#4648](https://github.com/NuGet/Home/issues/4648)</span><span class="sxs-lookup"><span data-stu-id="7d686-172">RuntimeEnvironmentHelper.IsLinux returns true for OSX - [#4648](https://github.com/NuGet/Home/issues/4648)</span></span>

* <span data-ttu-id="7d686-173">'dotnet pack' vloží nuspec pod obj místo obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)</span><span class="sxs-lookup"><span data-stu-id="7d686-173">'dotnet pack' puts nuspec under obj instead of obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)</span></span>

* <span data-ttu-id="7d686-174">Nuget velmi pomalé balíček upgradu - [#4534](https://github.com/NuGet/Home/issues/4534)</span><span class="sxs-lookup"><span data-stu-id="7d686-174">Nuget extremely slow package upgrade - [#4534](https://github.com/NuGet/Home/issues/4534)</span></span>

* <span data-ttu-id="7d686-175">Prohlášení CPS synchronizované s obnovením s větší řešení, které nezapnuli dolní limit (lightweight řešení obnovení) - [#4307](https://github.com/NuGet/Home/issues/4307)</span><span class="sxs-lookup"><span data-stu-id="7d686-175">CPS out of sync with Restore with larger solutions that haven't turned on LSL (lightweight solution restore) - [#4307](https://github.com/NuGet/Home/issues/4307)</span></span>

* <span data-ttu-id="7d686-176">SemVer 2.0 - nuget pack s zadaný verze ignoruje metadata (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)</span><span class="sxs-lookup"><span data-stu-id="7d686-176">SemVer 2.0 - nuget pack with provided version ignores metadata (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)</span></span>

* <span data-ttu-id="7d686-177">Nuget.exe (3 +) nainstalovat balíček s číslem verze a ExcludeVersion příznak není balíček aktualizace na novější verzi - [#2405](https://github.com/NuGet/Home/issues/2405)</span><span class="sxs-lookup"><span data-stu-id="7d686-177">Nuget.exe (3.+) install package with Version number and ExcludeVersion flag doesn't update package to newer version - [#2405](https://github.com/NuGet/Home/issues/2405)</span></span>

* <span data-ttu-id="7d686-178">Project.JSON obnovení musí zobrazit upozornění, pokud nejvyšší úrovně balíčky porušují omezení - [#2358](https://github.com/NuGet/Home/issues/2358)</span><span class="sxs-lookup"><span data-stu-id="7d686-178">Project.json restore should warn when top-level packages violate constraints - [#2358](https://github.com/NuGet/Home/issues/2358)</span></span>

* <span data-ttu-id="7d686-179">-ConfigFile není nastavení vlastní konfigurace pro příkaz install - [#1646](https://github.com/NuGet/Home/issues/1646)</span><span class="sxs-lookup"><span data-stu-id="7d686-179">-ConfigFile is not setting custom config on install command - [#1646](https://github.com/NuGet/Home/issues/1646)</span></span>

* <span data-ttu-id="7d686-180">instalace nuget.exe nectí '-DisableParallelProcessing' přepínače - [#1556](https://github.com/NuGet/Home/issues/1556)</span><span class="sxs-lookup"><span data-stu-id="7d686-180">nuget.exe install does not honor '-DisableParallelProcessing' switch - [#1556](https://github.com/NuGet/Home/issues/1556)</span></span>

* <span data-ttu-id="7d686-181">Zakázané zdroje, které DotNet.exe nebo msbuild.exe - stále používá [#5704](https://github.com/NuGet/Home/issues/5704)</span><span class="sxs-lookup"><span data-stu-id="7d686-181">Disabled sources still used by DotNet.exe or msbuild.exe - [#5704](https://github.com/NuGet/Home/issues/5704)</span></span>

* <span data-ttu-id="7d686-182">Opravte zablokování v dolní limit scénář – [#5685](https://github.com/NuGet/Home/issues/5685)</span><span class="sxs-lookup"><span data-stu-id="7d686-182">Fix hangs in LSL scenario - [#5685](https://github.com/NuGet/Home/issues/5685)</span></span>

<span data-ttu-id="7d686-183">**DCR:**</span><span class="sxs-lookup"><span data-stu-id="7d686-183">**DCR:**</span></span>

* <span data-ttu-id="7d686-184">nuget.exe nainstalovat podporu TargetFramework - [#5736](https://github.com/NuGet/Home/issues/5736)</span><span class="sxs-lookup"><span data-stu-id="7d686-184">nuget.exe install TargetFramework support - [#5736](https://github.com/NuGet/Home/issues/5736)</span></span>

* <span data-ttu-id="7d686-185">Přidejte jiný msbuild úloh UserAgent řetězce (msbuild plochy netcore vs) - [#5709](https://github.com/NuGet/Home/issues/5709)</span><span class="sxs-lookup"><span data-stu-id="7d686-185">Add different msbuild task UserAgent strings (netcore vs desktop msbuild) - [#5709](https://github.com/NuGet/Home/issues/5709)</span></span>

* <span data-ttu-id="7d686-186">PackagePathResolver.GetPackageDirectoryName musí být virtuální - [#5700](https://github.com/NuGet/Home/issues/5700)</span><span class="sxs-lookup"><span data-stu-id="7d686-186">PackagePathResolver.GetPackageDirectoryName should be virtual - [#5700](https://github.com/NuGet/Home/issues/5700)</span></span>

* <span data-ttu-id="7d686-187">[DesignConsistency] Složitá zprávy při přidání balíčku NuGet - [#5641](https://github.com/NuGet/Home/issues/5641)</span><span class="sxs-lookup"><span data-stu-id="7d686-187">[DesignConsistency] Confusing message when adding a NuGet package - [#5641](https://github.com/NuGet/Home/issues/5641)</span></span>

* <span data-ttu-id="7d686-188">[Varování a chyby] NoWarn není přechodně procházet skrz P2P odkazy - [#5501](https://github.com/NuGet/Home/issues/5501)</span><span class="sxs-lookup"><span data-stu-id="7d686-188">[Warnings and errors] NoWarn does not flow transitively through P2P references - [#5501](https://github.com/NuGet/Home/issues/5501)</span></span>

* <span data-ttu-id="7d686-189">Prosté řešení zatížení: Běžné jádra pro PM uživatelského rozhraní, pomocí PMC a inicializační vektory * - [#5057](https://github.com/NuGet/Home/issues/5057)</span><span class="sxs-lookup"><span data-stu-id="7d686-189">Lightweight Solution Load: Common Core for PM UI, PMC, and IVs* - [#5057](https://github.com/NuGet/Home/issues/5057)</span></span>

* <span data-ttu-id="7d686-190">Prosté řešení zatížení: Podpora - pomocí PMC - [#5053](https://github.com/NuGet/Home/issues/5053)</span><span class="sxs-lookup"><span data-stu-id="7d686-190">Lightweight Solution Load: Support - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)</span></span>

* <span data-ttu-id="7d686-191">Přidání podpory pro před obnovením MSBuild cíl, který aktivuje Visual Studio – [#4781](https://github.com/NuGet/Home/issues/4781)</span><span class="sxs-lookup"><span data-stu-id="7d686-191">Add support for pre-restore MSBuild target that Visual Studio triggers - [#4781](https://github.com/NuGet/Home/issues/4781)</span></span>

* <span data-ttu-id="7d686-192">Přidejte veřejný cíl do NuGet.targets, které můžete odkazovat pomocí BeforeTargets- [#4634](https://github.com/NuGet/Home/issues/4634)</span><span class="sxs-lookup"><span data-stu-id="7d686-192">Add a public target to NuGet.targets that can be referenced using BeforeTargets - [#4634](https://github.com/NuGet/Home/issues/4634)</span></span>

* <span data-ttu-id="7d686-193">Cíl Pack nelze vytvořit contentFiles akce sestavení správně - [#4166](https://github.com/NuGet/Home/issues/4166)</span><span class="sxs-lookup"><span data-stu-id="7d686-193">Pack target can't create contentFiles with build actions correctly - [#4166](https://github.com/NuGet/Home/issues/4166)</span></span>

* <span data-ttu-id="7d686-194">RestoreOperationLogger.Do blokuje podprocesy z fondu podprocesů - [#5663](https://github.com/NuGet/Home/issues/5663)</span><span class="sxs-lookup"><span data-stu-id="7d686-194">RestoreOperationLogger.Do blocks thread pool threads - [#5663](https://github.com/NuGet/Home/issues/5663)</span></span>

<span data-ttu-id="7d686-195">**Dokumenty:**</span><span class="sxs-lookup"><span data-stu-id="7d686-195">**Docs:**</span></span>

* <span data-ttu-id="7d686-196">Dokumentace pro instalaci příkaz příznaky DependencyVersion a Framework - [#5858](https://github.com/NuGet/Home/issues/5858)</span><span class="sxs-lookup"><span data-stu-id="7d686-196">Docs for Install command DependencyVersion and Framework flags - [#5858](https://github.com/NuGet/Home/issues/5858)</span></span>

* <span data-ttu-id="7d686-197">Aktualizace dokumentace na NuGet upozornění a chyby - [#5857](https://github.com/NuGet/Home/issues/5857)</span><span class="sxs-lookup"><span data-stu-id="7d686-197">Update to docs on NuGet warnings and errors - [#5857](https://github.com/NuGet/Home/issues/5857)</span></span>

## <a name="link-to-github-issues-fixed-in-44-rtm"></a><span data-ttu-id="7d686-198">Odkaz na Githubu chyby v 4.4 RTM</span><span class="sxs-lookup"><span data-stu-id="7d686-198">Link to GitHub issues fixed in 4.4 RTM</span></span>

[<span data-ttu-id="7d686-199">Seznam problémů 1</span><span class="sxs-lookup"><span data-stu-id="7d686-199">Issues List 1</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[<span data-ttu-id="7d686-200">Seznam problémů 2</span><span class="sxs-lookup"><span data-stu-id="7d686-200">Issues List 2</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[<span data-ttu-id="7d686-201">Seznam problémů 3</span><span class="sxs-lookup"><span data-stu-id="7d686-201">Issues List 3</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
