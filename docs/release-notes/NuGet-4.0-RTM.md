---
title: Poznámky k verzi NuGet 4,0 RTM
description: Poznámky k verzi pro NuGet 4,0 RTM, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: anangaur
ms.author: anangaur
ms.date: 03/03/2017
ms.topic: conceptual
ms.openlocfilehash: c3ec5c20e5175edd315de20ca98c7a106c51809e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776275"
---
# <a name="nuget-40-rtm-release-notes"></a><span data-ttu-id="166a4-103">Poznámky k verzi NuGet 4,0 RTM</span><span class="sxs-lookup"><span data-stu-id="166a4-103">NuGet 4.0 RTM Release Notes</span></span>

<span data-ttu-id="166a4-104">[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) obsahuje NuGet 4,0, který přidává podporu pro .NET Core, má spoustu kvalitních oprav a zvyšuje výkon.</span><span class="sxs-lookup"><span data-stu-id="166a4-104">[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.0 which adds support for .NET Core, has a bunch of quality fixes and improves performance.</span></span> <span data-ttu-id="166a4-105">Tato verze také přináší několik vylepšení, jako je podpora PackageReference, příkazů NuGet jako cílů MSBuild, obnovení balíčku na pozadí a další.</span><span class="sxs-lookup"><span data-stu-id="166a4-105">This release also brings several improvements like support for PackageReference, NuGet commands as MSBuild targets, background package restores, and more.</span></span>

## <a name="known-issues"></a><span data-ttu-id="166a4-106">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="166a4-106">Known issues</span></span>

### <a name="nuget-restore-may-fail-when-you-have-multiple-projects-referencing-another-project-in-a-solution"></a><span data-ttu-id="166a4-107">Když máte několik projektů, které se odkazují na jiný projekt v řešení, může selhat obnovení NuGet</span><span class="sxs-lookup"><span data-stu-id="166a4-107">NuGet restore may fail when you have multiple projects referencing another project in a solution</span></span>

#### <a name="issue"></a><span data-ttu-id="166a4-108">Problém</span><span class="sxs-lookup"><span data-stu-id="166a4-108">Issue</span></span>

<span data-ttu-id="166a4-109">Pokud v řešení máte odkazy na stejný projekt s jinou velikostí písmen nebo s jinými relativními cestami, obnovení NuGet nemusí fungovat.</span><span class="sxs-lookup"><span data-stu-id="166a4-109">NuGet restore may not work if, in a solution, you have project references to the same project with different casing or with different relative paths.</span></span> [<span data-ttu-id="166a4-110">NuGet#4574</span><span class="sxs-lookup"><span data-stu-id="166a4-110">NuGet#4574</span></span>](https://github.com/NuGet/Home/issues/4574)

#### <a name="workaround"></a><span data-ttu-id="166a4-111">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="166a4-111">Workaround</span></span>

<span data-ttu-id="166a4-112">Opravte velikost písmen nebo relativní cesty tak, aby pro všechny odkazy na projekt byly stejné.</span><span class="sxs-lookup"><span data-stu-id="166a4-112">Fix the casings or relative paths to be the same for all project references.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="166a4-113">Při používání konzoly Správce balíčků nemusí fungovat klávesa Enter</span><span class="sxs-lookup"><span data-stu-id="166a4-113">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="166a4-114">Problém</span><span class="sxs-lookup"><span data-stu-id="166a4-114">Issue</span></span>

<span data-ttu-id="166a4-115">V konzole Správce balíčků občas nefunguje klávesa Enter.</span><span class="sxs-lookup"><span data-stu-id="166a4-115">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="166a4-116">Když toto chování zpozorujete, zjistěte prosím, jak to vypadá s opravou, a poskytněte jakékoli další užitečné informace o postupu, jak tuto chybu reprodukovat.</span><span class="sxs-lookup"><span data-stu-id="166a4-116">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="166a4-117">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="166a4-117">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="166a4-118">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="166a4-118">Workaround</span></span>

<span data-ttu-id="166a4-119">Před otevřením řešení restartujte Visual Studio a otevřete konzolu PMC.</span><span class="sxs-lookup"><span data-stu-id="166a4-119">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="166a4-120">Případně zkuste `project.lock.json` obnovení a znovu obnovit.</span><span class="sxs-lookup"><span data-stu-id="166a4-120">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="in-net-core-projects-you-may-end-up-in-infinite-restore-loop-when-you-use-a-package-containing-an-assembly-with-an-invalid-signature"></a><span data-ttu-id="166a4-121">Pokud v projektech .NET Core použijete balíček, který obsahuje sestavení s neplatným podpisem, můžete uvíznout v nekonečné smyčce obnovování</span><span class="sxs-lookup"><span data-stu-id="166a4-121">In .NET Core projects, you may end up in infinite restore loop when you use a package containing an assembly with an invalid signature</span></span>

#### <a name="issue"></a><span data-ttu-id="166a4-122">Problém</span><span class="sxs-lookup"><span data-stu-id="166a4-122">Issue</span></span>

<span data-ttu-id="166a4-123">Když použijete balíček, který obsahuje sestavení s neplatným obsahem, nebo když se verze balíčku nastaví pomocí časovače DateTime, automatické obnovení balíčku běží v nekonečné smyčce.</span><span class="sxs-lookup"><span data-stu-id="166a4-123">Occassionally, when you use a package containing an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes package auto-restore to run in infinite loop.</span></span> [<span data-ttu-id="166a4-124">NuGet#4542</span><span class="sxs-lookup"><span data-stu-id="166a4-124">NuGet#4542</span></span>](https://github.com/NuGet/Home/issues/4542)

#### <a name="workaround"></a><span data-ttu-id="166a4-125">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="166a4-125">Workaround</span></span>

<span data-ttu-id="166a4-126">Pro tento problém zatím neexistuje alternativní řešení.</span><span class="sxs-lookup"><span data-stu-id="166a4-126">There is no workaround at this time.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="166a4-127">Pomocí Správce balíčků NuGet nemůžete zobrazit, přidat ani aktualizovat DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="166a4-127">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="166a4-128">Problém</span><span class="sxs-lookup"><span data-stu-id="166a4-128">Issue</span></span>

<span data-ttu-id="166a4-129">Správce balíčků NuGet nezobrazuje a nepovoluje přidat nebo aktualizovat DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="166a4-129">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="166a4-130">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="166a4-130">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="166a4-131">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="166a4-131">Workaround</span></span>

<span data-ttu-id="166a4-132">V souboru projektu se musí ručně upravit DotNetCLIToolReferences.</span><span class="sxs-lookup"><span data-stu-id="166a4-132">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="nuget-restore-will-fail-when-you-set-packageid-property-for-projects"></a><span data-ttu-id="166a4-133">Když pro projekty nastavíte vlastnost PackageId, obnovení NuGet se nepovede</span><span class="sxs-lookup"><span data-stu-id="166a4-133">NuGet restore will fail when you set PackageId property for projects</span></span>

#### <a name="issue"></a><span data-ttu-id="166a4-134">Problém</span><span class="sxs-lookup"><span data-stu-id="166a4-134">Issue</span></span>

<span data-ttu-id="166a4-135">Obnovení NuGet v sadě Visual Studio nerespektuje pro projekty .NET Core vlastnost projektů PackageId.</span><span class="sxs-lookup"><span data-stu-id="166a4-135">For .NET Core projects, NuGet restore in Visual Studio does not respect PackageId property of projects.</span></span> [<span data-ttu-id="166a4-136">NuGet#4586</span><span class="sxs-lookup"><span data-stu-id="166a4-136">NuGet#4586</span></span>](https://github.com/NuGet/Home/issues/4586)

#### <a name="workaround"></a><span data-ttu-id="166a4-137">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="166a4-137">Workaround</span></span>

<span data-ttu-id="166a4-138">Spusťte obnovení pomocí příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="166a4-138">Run restore using the command-line.</span></span>

### <a name="when-your-project-does-not-have-obj-folder-package-restore-may-fail"></a><span data-ttu-id="166a4-139">Pokud váš projekt nemá složku obj, nemusí se povést obnovit balíček</span><span class="sxs-lookup"><span data-stu-id="166a4-139">When your project does not have 'obj' folder, package restore may fail</span></span>

#### <a name="issue"></a><span data-ttu-id="166a4-140">Problém</span><span class="sxs-lookup"><span data-stu-id="166a4-140">Issue</span></span>

<span data-ttu-id="166a4-141">Pokud se odstraní složka obj, sadě Visual Studio se nepovede obnovit PackageReferences.</span><span class="sxs-lookup"><span data-stu-id="166a4-141">Visual Studio fails to restore PackageReferences when 'obj' folder has been deleted.</span></span> [<span data-ttu-id="166a4-142">NuGet#4528</span><span class="sxs-lookup"><span data-stu-id="166a4-142">NuGet#4528</span></span>](https://github.com/NuGet/Home/issues/4528)

#### <a name="workaround"></a><span data-ttu-id="166a4-143">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="166a4-143">Workaround</span></span>

<span data-ttu-id="166a4-144">Vytvořte složku obj ručně a obnovení by mělo fungovat.</span><span class="sxs-lookup"><span data-stu-id="166a4-144">Create 'obj' folder manually and the restore should work.</span></span>

### <a name="manually-updating-packages-using-update-package-in-console-may-fail"></a><span data-ttu-id="166a4-145">Ruční aktualizace balíčků pomocí Update-Package v konzole může selhat</span><span class="sxs-lookup"><span data-stu-id="166a4-145">Manually updating packages using Update-Package in console may fail</span></span>

#### <a name="issue"></a><span data-ttu-id="166a4-146">Problém</span><span class="sxs-lookup"><span data-stu-id="166a4-146">Issue</span></span>

<span data-ttu-id="166a4-147">Ruční použití Update-Package v konzole funguje pro projekty, které se právě převedly, jenom jednou.</span><span class="sxs-lookup"><span data-stu-id="166a4-147">Using Update-Package manually in the console only works once for PackageReferences projects that were just converted.</span></span> [<span data-ttu-id="166a4-148">NuGet#4431</span><span class="sxs-lookup"><span data-stu-id="166a4-148">NuGet#4431</span></span>](https://github.com/NuGet/Home/issues/4431)

#### <a name="workaround"></a><span data-ttu-id="166a4-149">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="166a4-149">Workaround</span></span>

<span data-ttu-id="166a4-150">Pro tento problém zatím neexistuje alternativní řešení.</span><span class="sxs-lookup"><span data-stu-id="166a4-150">There is no workaround at this time.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="166a4-151">Změna cílení verze cílové architektury může vést k nekompletnímu IntelliSense</span><span class="sxs-lookup"><span data-stu-id="166a4-151">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="166a4-152">Problém</span><span class="sxs-lookup"><span data-stu-id="166a4-152">Issue</span></span>

<span data-ttu-id="166a4-153">Změna cílení verze cílové architektury v sadě Visual Studio může vést k nekompletnímu IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="166a4-153">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="166a4-154">To se stává, když jako formát správce balíčků používáte PackageReferences.</span><span class="sxs-lookup"><span data-stu-id="166a4-154">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="166a4-155">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="166a4-155">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="166a4-156">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="166a4-156">Workaround</span></span>

<span data-ttu-id="166a4-157">Proveďte ruční obnovení.</span><span class="sxs-lookup"><span data-stu-id="166a4-157">Do a manual restore.</span></span>

### <a name="msbuild-trestore-fails-when-a-project-targeting-net461-references-another-project-targeting-netstandard"></a><span data-ttu-id="166a4-158">Když projekt, který cílí na .NET461, odkazuje na jiný projekt, který cílí na .NETStandard, příkaz msbuild /t:restore nebude úspěšný</span><span class="sxs-lookup"><span data-stu-id="166a4-158">msbuild /t:restore fails when a project targeting .NET461 references another project targeting .NETStandard</span></span>

#### <a name="issue"></a><span data-ttu-id="166a4-159">Problém</span><span class="sxs-lookup"><span data-stu-id="166a4-159">Issue</span></span>

<span data-ttu-id="166a4-160">Když projekt založený na PackageReference, který cílí na .NET461, odkazuje na jiný projekt založený na PackageReference, který cílí na .NETStandard, příkaz msbuild /t:restore nebude úspěšný.</span><span class="sxs-lookup"><span data-stu-id="166a4-160">msbuild /t:restore fails when a PackageReferenece based project targeting .NET461 references another PackageReference based project targeting .NETStandard.</span></span>  [<span data-ttu-id="166a4-161">NuGet#4532</span><span class="sxs-lookup"><span data-stu-id="166a4-161">NuGet#4532</span></span>](https://github.com/NuGet/Home/issues/4532)

#### <a name="workaround"></a><span data-ttu-id="166a4-162">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="166a4-162">Workaround</span></span>

<span data-ttu-id="166a4-163">Pro tento problém zatím neexistuje alternativní řešení.</span><span class="sxs-lookup"><span data-stu-id="166a4-163">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a><span data-ttu-id="166a4-164">Problémy opravené v časovém rámci NuGet 4,0 RTM</span><span class="sxs-lookup"><span data-stu-id="166a4-164">Issues fixed in NuGet 4.0 RTM timeframe</span></span>

<span data-ttu-id="166a4-165">[Poznámky k verzi nuget 4,0 RC](../release-notes/nuget-4.0-RC.md) – seznam všech problémů opravených pro NUGET 4,0 RC</span><span class="sxs-lookup"><span data-stu-id="166a4-165">[NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md) - Lists all the issues fixed for NuGet 4.0 RC</span></span>

### <a name="features"></a><span data-ttu-id="166a4-166">Funkce</span><span class="sxs-lookup"><span data-stu-id="166a4-166">Features</span></span>

- <span data-ttu-id="166a4-167">Lokalizace řetězců v NuGet. Core. sln – [#2041](https://github.com/NuGet/Home/issues/2041)</span><span class="sxs-lookup"><span data-stu-id="166a4-167">Localize strings in NuGet.Core.sln - [#2041](https://github.com/NuGet/Home/issues/2041)</span></span>

- <span data-ttu-id="166a4-168">NuGet nutí načíst projekty webové aplikace v režimu LSL – [#4258](https://github.com/NuGet/Home/issues/4258)</span><span class="sxs-lookup"><span data-stu-id="166a4-168">Nuget forces to load web application projects in LSL mode - [#4258](https://github.com/NuGet/Home/issues/4258)</span></span>

- <span data-ttu-id="166a4-169">Podpora autoreference PackageReference k blokování změn verze v uživatelském rozhraní pro balíčky nainstalované sadou SDK – [#4044](https://github.com/NuGet/Home/issues/4044)</span><span class="sxs-lookup"><span data-stu-id="166a4-169">AutoReferenced PackageReference support to block version changes in UI for "sdk installed" packages - [#4044](https://github.com/NuGet/Home/issues/4044)</span></span>

- <span data-ttu-id="166a4-170">Správně komunikovat PackageSpec. Version pro všechny závislosti projektu (PackageRef) – [#3902](https://github.com/NuGet/Home/issues/3902)</span><span class="sxs-lookup"><span data-stu-id="166a4-170">Correctly communicate PackageSpec.Version for any project dependencies (PackageRef) - [#3902](https://github.com/NuGet/Home/issues/3902)</span></span>

- <span data-ttu-id="166a4-171">Podpora pro odebrání odkazů na `.csproj` z příkazového řádku (s) – [#4101](https://github.com/NuGet/Home/issues/4101)</span><span class="sxs-lookup"><span data-stu-id="166a4-171">support for removing references into `.csproj` from commandline(s) - [#4101](https://github.com/NuGet/Home/issues/4101)</span></span>

- <span data-ttu-id="166a4-172">Podpora obnovení pro projekty PackageReference (normální a xplat) a zjednodušené načtení řešení – [#4003](https://github.com/NuGet/Home/issues/4003)</span><span class="sxs-lookup"><span data-stu-id="166a4-172">Support restore for PackageReference projects (normal and xplat) and Lightweight Solution Load - [#4003](https://github.com/NuGet/Home/issues/4003)</span></span>

- <span data-ttu-id="166a4-173">Podpora přidávání odkazů do `.csproj` příkazového řádku (CommandLine) – [#3751](https://github.com/NuGet/Home/issues/3751)</span><span class="sxs-lookup"><span data-stu-id="166a4-173">support for adding references into `.csproj` from commandline(s) - [#3751](https://github.com/NuGet/Home/issues/3751)</span></span>

- <span data-ttu-id="166a4-174">Podpora obnovení NuGet pro zjednodušené načtení řešení pro `packages.config` nebo `project.json`  -  [#3711](https://github.com/NuGet/Home/issues/3711)</span><span class="sxs-lookup"><span data-stu-id="166a4-174">Support NuGet restore for Lightweight Solution Load for `packages.config` or `project.json` - [#3711](https://github.com/NuGet/Home/issues/3711)</span></span>

- <span data-ttu-id="166a4-175">Podpora contentFiles v souboru NuGet generovaných cíli – [#3683](https://github.com/NuGet/Home/issues/3683)</span><span class="sxs-lookup"><span data-stu-id="166a4-175">contentFiles support in nuget generated targets file - [#3683](https://github.com/NuGet/Home/issues/3683)</span></span>

- <span data-ttu-id="166a4-176">Vytvoření mono CI pro nuget.exe ověřování na Macu pomocí MSBuild- [#3646](https://github.com/NuGet/Home/issues/3646)</span><span class="sxs-lookup"><span data-stu-id="166a4-176">Establish a Mono CI for nuget.exe validation on Mac using MSBuild - [#3646](https://github.com/NuGet/Home/issues/3646)</span></span>

- <span data-ttu-id="166a4-177">Přesune NuGet z verze V2 NuGet. základní závislosti – [#3645](https://github.com/NuGet/Home/issues/3645)</span><span class="sxs-lookup"><span data-stu-id="166a4-177">Move NuGet off of v2 NuGet.Core dependencies - [#3645](https://github.com/NuGet/Home/issues/3645)</span></span>

### <a name="bugs"></a><span data-ttu-id="166a4-178">Chyby</span><span class="sxs-lookup"><span data-stu-id="166a4-178">Bugs</span></span>

- <span data-ttu-id="166a4-179">Obnovení NuGet v aplikaci Visual Studio nerespektuje vlastnost PackageId projektů – [#4586](https://github.com/NuGet/Home/issues/4586)</span><span class="sxs-lookup"><span data-stu-id="166a4-179">NuGet restore in Visual Studio does not respect PackageId property of projects - [#4586](https://github.com/NuGet/Home/issues/4586)</span></span>

- <span data-ttu-id="166a4-180">Při přidávání balíčku do balíčku VSIX došlo k chybě ProjectSystemCache NuGet – [#4545](https://github.com/NuGet/Home/issues/4545)</span><span class="sxs-lookup"><span data-stu-id="166a4-180">NuGet ProjectSystemCache error when adding package in vsix package - [#4545](https://github.com/NuGet/Home/issues/4545)</span></span>

- <span data-ttu-id="166a4-181">Sada vyvolá výjimku, pokud se v projektu používá IncludeSource s více TFM- [#4536](https://github.com/NuGet/Home/issues/4536)</span><span class="sxs-lookup"><span data-stu-id="166a4-181">Pack throws exception if IncludeSource is used in a project with multiple TFMs - [#4536](https://github.com/NuGet/Home/issues/4536)</span></span>

- <span data-ttu-id="166a4-182">VS 2017 RC3 selhání při použití aktualizace ze správy balíčků na úrovni řešení – [#4474](https://github.com/NuGet/Home/issues/4474)</span><span class="sxs-lookup"><span data-stu-id="166a4-182">VS 2017 RC3 crashes on using update from Solution-wide package management - [#4474](https://github.com/NuGet/Home/issues/4474)</span></span>

- <span data-ttu-id="166a4-183">Nelze odinstalovat nově nainstalovaný balíček – [#4435](https://github.com/NuGet/Home/issues/4435)</span><span class="sxs-lookup"><span data-stu-id="166a4-183">Cannot uninstall newly installed package  - [#4435](https://github.com/NuGet/Home/issues/4435)</span></span>

- <span data-ttu-id="166a4-184">Při migraci na PackageRef mají hybridní řešení nezvyklé chování při obnovení – [#4433](https://github.com/NuGet/Home/issues/4433)</span><span class="sxs-lookup"><span data-stu-id="166a4-184">When migrating to PackageRef, hybrid solutions have strange restore behavior - [#4433](https://github.com/NuGet/Home/issues/4433)</span></span>

- <span data-ttu-id="166a4-185">Sestavování po spuštění operace NuGet (instalace, aktualizace, obnovení) může způsobit, že systém přestane reagovat [#4420](https://github.com/NuGet/Home/issues/4420)</span><span class="sxs-lookup"><span data-stu-id="166a4-185">Building soon after starting NuGet operation (install, update, restore), can cause VS to Hang - [#4420](https://github.com/NuGet/Home/issues/4420)</span></span>

- <span data-ttu-id="166a4-186">Uživatelské rozhraní přestane zablokovat inicializaci NuGet. SolutionRestoreManager. RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)</span><span class="sxs-lookup"><span data-stu-id="166a4-186">UI Hang - Deadlock initializing NuGet.SolutionRestoreManager.RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)</span></span>

- <span data-ttu-id="166a4-187">příkaz pro přidání balíčku by měl přidat verzi jako atribut namísto prvku [#4325](https://github.com/NuGet/Home/issues/4325)</span><span class="sxs-lookup"><span data-stu-id="166a4-187">add package command should add version as attribute instead of element - [#4325](https://github.com/NuGet/Home/issues/4325)</span></span>

- <span data-ttu-id="166a4-188">dotnet</span><span class="sxs-lookup"><span data-stu-id="166a4-188">dotnet</span></span>
  - <span data-ttu-id="166a4-189">dotnetcore Restore foo. sln – neúspěšná, když konfigurace v SLN způsobují duplicitní projekty (ale rozdílové konfigurace) v grafu obnovit – [#4316](https://github.com/NuGet/Home/issues/4316)</span><span class="sxs-lookup"><span data-stu-id="166a4-189">dotnetcore Restore foo.sln -- fails when configurations in SLN cause duplicate (but diff config) projects in restore graph - [#4316](https://github.com/NuGet/Home/issues/4316)</span></span>

- <span data-ttu-id="166a4-190">Balíčky pouze s obsahem – [#3668](https://github.com/NuGet/Home/issues/3668)</span><span class="sxs-lookup"><span data-stu-id="166a4-190">Content only packages - [#3668](https://github.com/NuGet/Home/issues/3668)</span></span>

- <span data-ttu-id="166a4-191">Ve výchozím nastavení se z možnosti selektor formátu balíčku odsouhlasí – [#4468](https://github.com/NuGet/Home/issues/4468)</span><span class="sxs-lookup"><span data-stu-id="166a4-191">By default opt out of package format selector option - [#4468](https://github.com/NuGet/Home/issues/4468)</span></span>

- <span data-ttu-id="166a4-192">Výkon: CreateUAP_CSharp_VS. 01.1. Create Project Duration_TotalElapsedTime by 3 153,570 MS (149,1%).</span><span class="sxs-lookup"><span data-stu-id="166a4-192">Perf: CreateUAP_CSharp_VS.01.1.Create project regressed Duration_TotalElapsedTime by 3,153.570 ms (149.1%).</span></span> <span data-ttu-id="166a4-193">Směrný plán 26129,02 – [#4452](https://github.com/NuGet/Home/issues/4452)</span><span class="sxs-lookup"><span data-stu-id="166a4-193">Baseline 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)</span></span>

- <span data-ttu-id="166a4-194">Výkon: ManagedLangs_CS_DDRIT .0300. znovu sestavit řešení Duration_TotalElapsedTime o 1,5 sec.</span><span class="sxs-lookup"><span data-stu-id="166a4-194">Perf: ManagedLangs_CS_DDRIT.0300.Rebuild Solution regressed Duration_TotalElapsedTime by 1.5sec.</span></span> <span data-ttu-id="166a4-195">Směrný plán 26105 – [#4441](https://github.com/NuGet/Home/issues/4441)</span><span class="sxs-lookup"><span data-stu-id="166a4-195">Baseline 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)</span></span>

- <span data-ttu-id="166a4-196">V projektech s více TFM se nezdařila její jmenování – [#4419](https://github.com/NuGet/Home/issues/4419)</span><span class="sxs-lookup"><span data-stu-id="166a4-196">Nomination fails in multi-TFM projects - [#4419](https://github.com/NuGet/Home/issues/4419)</span></span>

- <span data-ttu-id="166a4-197">Výkon: WebForms_DDRIT .1200. zavřít řešení VM_ImagesInMemory_Total_devenv podle 3,000ho počtu (0,5%).</span><span class="sxs-lookup"><span data-stu-id="166a4-197">Perf: WebForms_DDRIT.1200.Close Solution regressed VM_ImagesInMemory_Total_devenv by 3.000 Count (0.5%).</span></span> <span data-ttu-id="166a4-198">Směrný plán 26123,04 – [#4408](https://github.com/NuGet/Home/issues/4408)</span><span class="sxs-lookup"><span data-stu-id="166a4-198">Baseline 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)</span></span>

- <span data-ttu-id="166a4-199">Upozornění vsfeedback-Pack při cílení na netcoreapp 1.1 – [#4397](https://github.com/NuGet/Home/issues/4397)</span><span class="sxs-lookup"><span data-stu-id="166a4-199">vsfeedback - Pack warnings when targeting netcoreapp1.1 - [#4397](https://github.com/NuGet/Home/issues/4397)</span></span>

- <span data-ttu-id="166a4-200">PathTooLongException při pokusu o přidání balíčku NuGet do prázdné ASP.NET Core webové aplikace – [#4391](https://github.com/NuGet/Home/issues/4391)</span><span class="sxs-lookup"><span data-stu-id="166a4-200">PathTooLongException when trying to add a NuGet package to empty ASP.NET Core web application - [#4391](https://github.com/NuGet/Home/issues/4391)</span></span>

- <span data-ttu-id="166a4-201">Sada se spouští příliš často – dotnet.</span><span class="sxs-lookup"><span data-stu-id="166a4-201">Pack runs too often -- dotnet</span></span>
  - <span data-ttu-id="166a4-202">sada dotnetcore Pack se nezdařila s cyklickými závislostmi v grafu závislosti cíle zahrnující cílovou sadu "Pack" – [#4381](https://github.com/NuGet/Home/issues/4381)</span><span class="sxs-lookup"><span data-stu-id="166a4-202">dotnetcore pack fails with There is a circular dependency in the target dependency graph involving target "Pack"  - [#4381](https://github.com/NuGet/Home/issues/4381)</span></span>

- <span data-ttu-id="166a4-203">Sada se spouští příliš často – vygeneruje se balíček NuGet nezahrnuje všechny konfigurace – [#4380](https://github.com/NuGet/Home/issues/4380)</span><span class="sxs-lookup"><span data-stu-id="166a4-203">Pack runs too often -- Generate NuGet package doesn't include all the configurations  - [#4380](https://github.com/NuGet/Home/issues/4380)</span></span>

- <span data-ttu-id="166a4-204">NullReferenceException přidání nugetu s packageref v projektu C++ – [#4378](https://github.com/NuGet/Home/issues/4378)</span><span class="sxs-lookup"><span data-stu-id="166a4-204">NullReferenceException adding  nuget with packageref in  C++  project - [#4378](https://github.com/NuGet/Home/issues/4378)</span></span>

- <span data-ttu-id="166a4-205">Usnadnění: Předčítání nepopisuje políčko pro výběr projektů pro instalaci balíčku do [#4366](https://github.com/NuGet/Home/issues/4366)</span><span class="sxs-lookup"><span data-stu-id="166a4-205">Accessibility : Narrator does not narrate the checkbox to select the projects to install the package to - [#4366](https://github.com/NuGet/Home/issues/4366)</span></span>

- <span data-ttu-id="166a4-206">NuGet VS17 se neúspěšně připojuje k kanálům VSO/VSTS – VS chyba 365798- [#4365](https://github.com/NuGet/Home/issues/4365)</span><span class="sxs-lookup"><span data-stu-id="166a4-206">NuGet VS17 sporadically fails connecting to VSO/VSTS feeds - VS Bug 365798 - [#4365](https://github.com/NuGet/Home/issues/4365)</span></span>

- <span data-ttu-id="166a4-207">contentFiles načíst výstup do špatného umístění, pokud PackagePath Určuje cestu jako "contentFiles" – [#4348](https://github.com/NuGet/Home/issues/4348)</span><span class="sxs-lookup"><span data-stu-id="166a4-207">contentFiles get output to wrong location if PackagePath specifies path as "contentFiles" - [#4348](https://github.com/NuGet/Home/issues/4348)</span></span>

- <span data-ttu-id="166a4-208">Cílová sada připojí vlastnost PackageVersion pomocí VersionSuffix- [#4324](https://github.com/NuGet/Home/issues/4324)</span><span class="sxs-lookup"><span data-stu-id="166a4-208">Pack target appends PackageVersion property with VersionSuffix - [#4324](https://github.com/NuGet/Home/issues/4324)</span></span>

- <span data-ttu-id="166a4-209">Zadání cesty k balíčku nefunguje se sadou dotnet Pack – [#4321](https://github.com/NuGet/Home/issues/4321)</span><span class="sxs-lookup"><span data-stu-id="166a4-209">Specifying package path doesn't work with dotnet pack - [#4321](https://github.com/NuGet/Home/issues/4321)</span></span>

- <span data-ttu-id="166a4-210">NuGet výstupuje spoustu upozornění o duplicitních importech během obnovení- [#4304](https://github.com/NuGet/Home/issues/4304)</span><span class="sxs-lookup"><span data-stu-id="166a4-210">NuGet outputs a bunch of warnings about duplicate imports during restore - [#4304](https://github.com/NuGet/Home/issues/4304)</span></span>

- <span data-ttu-id="166a4-211">Volba "formát správce balíčků NuGet" v dialogovém okně vypadá špatný motiv – [#4300](https://github.com/NuGet/Home/issues/4300)</span><span class="sxs-lookup"><span data-stu-id="166a4-211">Choose "NuGet Package Manager Format" dialog looks bad under dark theme - [#4300](https://github.com/NuGet/Home/issues/4300)</span></span>

- <span data-ttu-id="166a4-212">Chyba VS při obnovení buildu – [#4298](https://github.com/NuGet/Home/issues/4298)</span><span class="sxs-lookup"><span data-stu-id="166a4-212">VS crash on build restore - [#4298](https://github.com/NuGet/Home/issues/4298)</span></span>

- <span data-ttu-id="166a4-213">Zablokování sady Visual Studio Pokud přidáte TFM v targetFramework, uložte a pak sestavíte.</span><span class="sxs-lookup"><span data-stu-id="166a4-213">Visual Studio deadlocks if you add TFM in targetframeworks, save, then build.</span></span> <span data-ttu-id="166a4-214">10% času – [#4295](https://github.com/NuGet/Home/issues/4295)</span><span class="sxs-lookup"><span data-stu-id="166a4-214">10% of time - [#4295](https://github.com/NuGet/Home/issues/4295)</span></span>

- <span data-ttu-id="166a4-215">sada NuGet Pack neúspěšně zavedla výstup zprávy o úspěchu při vybalení projektu [#4294](https://github.com/NuGet/Home/issues/4294)</span><span class="sxs-lookup"><span data-stu-id="166a4-215">nuget pack does not output success message on packing a project successfully - [#4294](https://github.com/NuGet/Home/issues/4294)</span></span>

- <span data-ttu-id="166a4-216">PackTask se nepovedlo kvůli chybě System. IO. Compression 4,1 – [#4290](https://github.com/NuGet/Home/issues/4290)</span><span class="sxs-lookup"><span data-stu-id="166a4-216">PackTask fails due to System.IO.Compression 4.1 not being found - [#4290](https://github.com/NuGet/Home/issues/4290)</span></span>

- <span data-ttu-id="166a4-217">Sada se spouští příliš často – PackTask se často nedaří a je to konflikt přístupu k souboru – [#4289](https://github.com/NuGet/Home/issues/4289)</span><span class="sxs-lookup"><span data-stu-id="166a4-217">Pack runs too often -- PackTask frequently fails with file access conflict - [#4289](https://github.com/NuGet/Home/issues/4289)</span></span>

- <span data-ttu-id="166a4-218">NuGet otevře okno výstup během obnovení na pozadí – [#4274](https://github.com/NuGet/Home/issues/4274)</span><span class="sxs-lookup"><span data-stu-id="166a4-218">NuGet opens the output window during background restore - [#4274](https://github.com/NuGet/Home/issues/4274)</span></span>

- <span data-ttu-id="166a4-219">Eliminujte ServiceProvider jako nebezpečný vzor kódování (což může způsobit zablokování) – [#4268](https://github.com/NuGet/Home/issues/4268)</span><span class="sxs-lookup"><span data-stu-id="166a4-219">Eliminate ServiceProvider as dangerous coding pattern (which can cause hangs) - [#4268](https://github.com/NuGet/Home/issues/4268)</span></span>

- <span data-ttu-id="166a4-220">Výkon a UIHang – zlepšení čtení DownloadTimeoutStream – [#4266](https://github.com/NuGet/Home/issues/4266)</span><span class="sxs-lookup"><span data-stu-id="166a4-220">Perf/UIHang - Improve DownloadTimeoutStream reads - [#4266](https://github.com/NuGet/Home/issues/4266)</span></span>

- <span data-ttu-id="166a4-221">Zablokování sady Visual Studio při pokusu zavřít projekt před dokončením obnovení NuGet – [#4257](https://github.com/NuGet/Home/issues/4257)</span><span class="sxs-lookup"><span data-stu-id="166a4-221">Visual Studio deadlocks if you attempt to close a project before NuGet restore has finished - [#4257](https://github.com/NuGet/Home/issues/4257)</span></span>

- <span data-ttu-id="166a4-222">Problémy s PackTask a balícími `.nuspec`  -  [#4250](https://github.com/NuGet/Home/issues/4250)</span><span class="sxs-lookup"><span data-stu-id="166a4-222">Issues with PackTask and packing `.nuspec` - [#4250](https://github.com/NuGet/Home/issues/4250)</span></span>

- <span data-ttu-id="166a4-223">[vsfeedback] Balíčky NuGet se nedají přeložit v novém projektu (musí se restartovat Visual Studio) – [#4217](https://github.com/NuGet/Home/issues/4217)</span><span class="sxs-lookup"><span data-stu-id="166a4-223">[vsfeedback] Cannot resolve nuget packages on new project (needs to restart visual studio) - [#4217](https://github.com/NuGet/Home/issues/4217)</span></span>

- <span data-ttu-id="166a4-224">[vsfeedback] Rozevírací seznam verze, který zobrazuje dostupné verze balíčku, potýká a zůstane v synchronizaci s vybraným balíčkem nuGet...- [#4198](https://github.com/NuGet/Home/issues/4198)</span><span class="sxs-lookup"><span data-stu-id="166a4-224">[vsfeedback] The "Version" drop down that shows available package versions, struggles to stay in-sync with the selected nuGet package...  - [#4198](https://github.com/NuGet/Home/issues/4198)</span></span>

- <span data-ttu-id="166a4-225">NuGet. klient by měl používat JoinableTaskFactory CPS při interakci se serverem CPS, aby se zabránilo zablokování – [#4185](https://github.com/NuGet/Home/issues/4185)</span><span class="sxs-lookup"><span data-stu-id="166a4-225">Nuget.Client should use CPS JoinableTaskFactory when interacting with CPS to prevent deadlocks - [#4185](https://github.com/NuGet/Home/issues/4185)</span></span>

- <span data-ttu-id="166a4-226">3.5.0 NuGet se nebalí `.targets` z balíčku – [#4171](https://github.com/NuGet/Home/issues/4171)</span><span class="sxs-lookup"><span data-stu-id="166a4-226">NuGet 3.5.0 not unpacking `.targets` from package - [#4171](https://github.com/NuGet/Home/issues/4171)</span></span>

- <span data-ttu-id="166a4-227">dotnet</span><span class="sxs-lookup"><span data-stu-id="166a4-227">dotnet</span></span>
  - <span data-ttu-id="166a4-228">dotnetcore Pack nepodporuje nadpis v `.csproj`  -  [#4150](https://github.com/NuGet/Home/issues/4150)</span><span class="sxs-lookup"><span data-stu-id="166a4-228">dotnetcore pack does not support title in `.csproj` - [#4150](https://github.com/NuGet/Home/issues/4150)</span></span>

- <span data-ttu-id="166a4-229">Install-Package má za následek chybovou dialog v VS2017 RC – [#4127](https://github.com/NuGet/Home/issues/4127)</span><span class="sxs-lookup"><span data-stu-id="166a4-229">Install-Package results in error dialog in VS2017 RC - [#4127](https://github.com/NuGet/Home/issues/4127)</span></span>

- <span data-ttu-id="166a4-230">Aktualizace balíčku pro projekt .NET Core vypadá jako nefunguje, protože uživatelské rozhraní nezíská aktualizaci CPS z jeho jmenovaného.</span><span class="sxs-lookup"><span data-stu-id="166a4-230">Updating a package for .net core project appears to not work, as the UI doesn't get the CPS update from the nominate.</span></span><span data-ttu-id="166a4-231"> - [#4035](https://github.com/NuGet/Home/issues/4035)</span><span class="sxs-lookup"><span data-stu-id="166a4-231"> - [#4035](https://github.com/NuGet/Home/issues/4035)</span></span>

- <span data-ttu-id="166a4-232">Vylepšit nevyřešené upozornění na odkaz – [#3955](https://github.com/NuGet/Home/issues/3955)</span><span class="sxs-lookup"><span data-stu-id="166a4-232">Improve unresolved reference warning - [#3955](https://github.com/NuGet/Home/issues/3955)</span></span>

- <span data-ttu-id="166a4-233">dotnet</span><span class="sxs-lookup"><span data-stu-id="166a4-233">dotnet</span></span>
  - <span data-ttu-id="166a4-234">dotnetcore Pack – ProjectReference ztratí informace o verzi – [#3953](https://github.com/NuGet/Home/issues/3953)</span><span class="sxs-lookup"><span data-stu-id="166a4-234">dotnetcore pack - ProjectReference loses version information - [#3953](https://github.com/NuGet/Home/issues/3953)</span></span>

- <span data-ttu-id="166a4-235">Vytvoření aplikace UWP vytvoření projektu & opětovného sestavení celkových uplynulých časových regresí – [#3873](https://github.com/NuGet/Home/issues/3873)</span><span class="sxs-lookup"><span data-stu-id="166a4-235">Create UWP app create project & rebuild total elapsed time regressions - [#3873](https://github.com/NuGet/Home/issues/3873)</span></span>

- <span data-ttu-id="166a4-236">Zpráva o úspěšném obnovení se zobrazí i po chybě při obnovení.</span><span class="sxs-lookup"><span data-stu-id="166a4-236">Successful restore message is displayed even after error during restore.</span></span><span data-ttu-id="166a4-237"> - [#3799](https://github.com/NuGet/Home/issues/3799)</span><span class="sxs-lookup"><span data-stu-id="166a4-237"> - [#3799](https://github.com/NuGet/Home/issues/3799)</span></span>

- <span data-ttu-id="166a4-238">Opětovné publikování NuGet. CommandLine 3.4.4 do Nuget.org- [#2931](https://github.com/NuGet/Home/issues/2931)</span><span class="sxs-lookup"><span data-stu-id="166a4-238">re-Publish Nuget.CommandLine 3.4.4 to Nuget.org - [#2931](https://github.com/NuGet/Home/issues/2931)</span></span>

- <span data-ttu-id="166a4-239">Při migraci se projekty mění z `project.json` na a---obnovení se nepovede. `.csproj` [#4297](https://github.com/NuGet/Home/issues/4297)</span><span class="sxs-lookup"><span data-stu-id="166a4-239">On Migrate, projects change from `project.json` to `.csproj` --- restore fails - [#4297](https://github.com/NuGet/Home/issues/4297)</span></span>

- <span data-ttu-id="166a4-240">Neúspěšné obnovení při nově vytvořeném projektu xUnit test- [#4296](https://github.com/NuGet/Home/issues/4296)</span><span class="sxs-lookup"><span data-stu-id="166a4-240">Restore failing on newly created xunit Test project  - [#4296](https://github.com/NuGet/Home/issues/4296)</span></span>

- <span data-ttu-id="166a4-241">Základní projekty můžou zablokovat, uzamknout uživatelské rozhraní při otevření [#4269](https://github.com/NuGet/Home/issues/4269)</span><span class="sxs-lookup"><span data-stu-id="166a4-241">Core projects can hang, lock up UI on open - [#4269](https://github.com/NuGet/Home/issues/4269)</span></span>

- <span data-ttu-id="166a4-242">Oprava souboru cílů pro úlohy sestavení – [#4267](https://github.com/NuGet/Home/issues/4267)</span><span class="sxs-lookup"><span data-stu-id="166a4-242">fix targets file for build tasks - [#4267](https://github.com/NuGet/Home/issues/4267)</span></span>

- <span data-ttu-id="166a4-243">Seznam chyb obsahuje chybu po sestavení řešení, které uvolní odkazovaný projekt – [#4208](https://github.com/NuGet/Home/issues/4208)</span><span class="sxs-lookup"><span data-stu-id="166a4-243">Error list has error after build solution which unload the referenced project - [#4208](https://github.com/NuGet/Home/issues/4208)</span></span>

- <span data-ttu-id="166a4-244">MSB4057: cíl "_GenerateRestoreGraphProjectEntry" v projektu neexistuje.</span><span class="sxs-lookup"><span data-stu-id="166a4-244">MSB4057: The target "_GenerateRestoreGraphProjectEntry" does not exist in the project.</span></span><span data-ttu-id="166a4-245"> - [#4194](https://github.com/NuGet/Home/issues/4194)</span><span class="sxs-lookup"><span data-stu-id="166a4-245"> - [#4194](https://github.com/NuGet/Home/issues/4194)</span></span>

- <span data-ttu-id="166a4-246">vsfeedback: uživatelské rozhraní správce NuGet pro zhroucení řešení při výběru všech projektů – [#4191](https://github.com/NuGet/Home/issues/4191)</span><span class="sxs-lookup"><span data-stu-id="166a4-246">vsfeedback: nuget manager ui for solution crashes when you select all projects - [#4191](https://github.com/NuGet/Home/issues/4191)</span></span>

- <span data-ttu-id="166a4-247">nuget.exe MSBuildPath v případě, že dojde k koncovému lomítku – [#4180](https://github.com/NuGet/Home/issues/4180)</span><span class="sxs-lookup"><span data-stu-id="166a4-247">nuget.exe msbuildpath fails when there is a trailing slash - [#4180](https://github.com/NuGet/Home/issues/4180)</span></span>

- <span data-ttu-id="166a4-248">vsfeedback: obnovení NuGetu udělit několik upozornění na projekt pro projekt LinqToTwitter – [#4156](https://github.com/NuGet/Home/issues/4156)</span><span class="sxs-lookup"><span data-stu-id="166a4-248">vsfeedback: NuGet restore give several project reference warnings for LinqToTwitter project - [#4156](https://github.com/NuGet/Home/issues/4156)</span></span>

- <span data-ttu-id="166a4-249">Sada `.csproj` nezahrnuje atribut minClientVersion- [#4135](https://github.com/NuGet/Home/issues/4135) .</span><span class="sxs-lookup"><span data-stu-id="166a4-249">Pack from `.csproj` does not include the minClientVersion attribute  - [#4135](https://github.com/NuGet/Home/issues/4135)</span></span>

- <span data-ttu-id="166a4-250">NuGet.Build.Tasks.Pack.dll zaslané zpoždění podepsané v VS2017 (d15rel 26014,00) – [#4122](https://github.com/NuGet/Home/issues/4122)</span><span class="sxs-lookup"><span data-stu-id="166a4-250">NuGet.Build.Tasks.Pack.dll shipped delay signed in VS2017 (d15rel 26014.00) - [#4122](https://github.com/NuGet/Home/issues/4122)</span></span>

- <span data-ttu-id="166a4-251">VSFeedback: obnovení selhalo pro projekt VS 2015 generovaný s CMake 3.7.1- [#4114](https://github.com/NuGet/Home/issues/4114)</span><span class="sxs-lookup"><span data-stu-id="166a4-251">VSFeedback: Restore fails for a VS 2015 project generated with CMake 3.7.1 - [#4114](https://github.com/NuGet/Home/issues/4114)</span></span>

- <span data-ttu-id="166a4-252">VSFeedback: Restore Errors může skrývat více kompletních chybových zpráv, které může sestavení poskytnout – [#4113](https://github.com/NuGet/Home/issues/4113)</span><span class="sxs-lookup"><span data-stu-id="166a4-252">VSFeedback: Restore errors can obscure more complete error messages that build could give - [#4113](https://github.com/NuGet/Home/issues/4113)</span></span>

- <span data-ttu-id="166a4-253">[VSFeedback] Při obnovování balíčků NuGet pro webový projekt došlo k chybě: hodnota nemůže být null.</span><span class="sxs-lookup"><span data-stu-id="166a4-253">[VSFeedback] Error occurred while restoring NuGet packages for website project: Value cannot be null.</span></span><span data-ttu-id="166a4-254"> - [#4092](https://github.com/NuGet/Home/issues/4092)</span><span class="sxs-lookup"><span data-stu-id="166a4-254"> - [#4092](https://github.com/NuGet/Home/issues/4092)</span></span>

- <span data-ttu-id="166a4-255">Migrace vyvolá výjimku "Object Reference Exception" v NuGet. PackageManagement. VisualStudio. SolutionRestoreWorker- [#4067](https://github.com/NuGet/Home/issues/4067)</span><span class="sxs-lookup"><span data-stu-id="166a4-255">Migration Throws "Object reference Exception" in NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker - [#4067](https://github.com/NuGet/Home/issues/4067)</span></span>

- <span data-ttu-id="166a4-256">dotnet</span><span class="sxs-lookup"><span data-stu-id="166a4-256">dotnet</span></span>
  - <span data-ttu-id="166a4-257">sada dotnetcore Pack by měla zabalit nástroje s verzemi, na které byl balíček sestaven – [#4063](https://github.com/NuGet/Home/issues/4063)</span><span class="sxs-lookup"><span data-stu-id="166a4-257">dotnetcore pack should pack tools with the versions that the package was built against - [#4063](https://github.com/NuGet/Home/issues/4063)</span></span>

- <span data-ttu-id="166a4-258">Nové obnovení na pozadí: zapisuje milisekundy do stavového řádku, když trvá obnovení s [#4036](https://github.com/NuGet/Home/issues/4036)</span><span class="sxs-lookup"><span data-stu-id="166a4-258">New background restore writes milliseconds to status bar when it takes seconds to restore - [#4036](https://github.com/NuGet/Home/issues/4036)</span></span>

- <span data-ttu-id="166a4-259">Překlepy při pokusu o vyřešení všech odkazů na projekt – [#4018](https://github.com/NuGet/Home/issues/4018)</span><span class="sxs-lookup"><span data-stu-id="166a4-259">Typo on failed to resolve all project references - [#4018](https://github.com/NuGet/Home/issues/4018)</span></span>

- <span data-ttu-id="166a4-260">Povolit pracovní postupy PCM v referenčních scénářích balíčku – [#4016](https://github.com/NuGet/Home/issues/4016)</span><span class="sxs-lookup"><span data-stu-id="166a4-260">Enable PCM workflows in package reference scenarios - [#4016](https://github.com/NuGet/Home/issues/4016)</span></span>

- <span data-ttu-id="166a4-261">Nelze nalézt nainstalované balíčky v uživatelském rozhraní Správce balíčků – [#4015](https://github.com/NuGet/Home/issues/4015)</span><span class="sxs-lookup"><span data-stu-id="166a4-261">Can not find installed packages in package manager UI - [#4015](https://github.com/NuGet/Home/issues/4015)</span></span>

- <span data-ttu-id="166a4-262">dotnet</span><span class="sxs-lookup"><span data-stu-id="166a4-262">dotnet</span></span>
  - <span data-ttu-id="166a4-263">sada dotnetcore Pack se nezdařila, pokud je PackagePath prázdné – [#3993](https://github.com/NuGet/Home/issues/3993)</span><span class="sxs-lookup"><span data-stu-id="166a4-263">dotnetcore pack fails when PackagePath is empty - [#3993](https://github.com/NuGet/Home/issues/3993)</span></span>

- <span data-ttu-id="166a4-264">Úloha obnovení se ve scénáři více uživatelů nezdařila – [#3897](https://github.com/NuGet/Home/issues/3897)</span><span class="sxs-lookup"><span data-stu-id="166a4-264">Restore task fails in an multi user scenario - [#3897](https://github.com/NuGet/Home/issues/3897)</span></span>

- <span data-ttu-id="166a4-265">Nelze změnit typ obsahu při balení pomocí úlohy NuGet Pack Task- [#3895](https://github.com/NuGet/Home/issues/3895)</span><span class="sxs-lookup"><span data-stu-id="166a4-265">Cannot change Content type when packing using NuGet Pack Task - [#3895](https://github.com/NuGet/Home/issues/3895)</span></span>

- <span data-ttu-id="166a4-266">Výchozí kopie ContentFiles nejsou správné pro MsBuild/t: Pack- [#3894](https://github.com/NuGet/Home/issues/3894)</span><span class="sxs-lookup"><span data-stu-id="166a4-266">Default Copy of ContentFiles are incorrect for MsBuild /t:pack - [#3894](https://github.com/NuGet/Home/issues/3894)</span></span>

- <span data-ttu-id="166a4-267">Nainstalovat balíček obnovení dvojitým protokolem zpráva obnovení balíčků – [#3785](https://github.com/NuGet/Home/issues/3785)</span><span class="sxs-lookup"><span data-stu-id="166a4-267">Install package restore double logs the restoring packages message - [#3785](https://github.com/NuGet/Home/issues/3785)</span></span>

- <span data-ttu-id="166a4-268">Remove Guardrails – obnovení oddílu runtimes by mělo platit jenom pro aktuální projekt – [#3768](https://github.com/NuGet/Home/issues/3768)</span><span class="sxs-lookup"><span data-stu-id="166a4-268">Remove Guardrails - Restore of "runtimes" section should only apply to the current project - [#3768](https://github.com/NuGet/Home/issues/3768)</span></span>

- <span data-ttu-id="166a4-269">Úloha balíčku vloží soubory obsahu v obsahu/a contentFiles/- [#3718](https://github.com/NuGet/Home/issues/3718)</span><span class="sxs-lookup"><span data-stu-id="166a4-269">Pack task puts content files in both 'content/' and 'contentFiles/' - [#3718](https://github.com/NuGet/Home/issues/3718)</span></span>

- <span data-ttu-id="166a4-270">dotnet</span><span class="sxs-lookup"><span data-stu-id="166a4-270">dotnet</span></span>
  - <span data-ttu-id="166a4-271">dotnetcore Pack3 má dodatečné rozdělení značek – [#3701](https://github.com/NuGet/Home/issues/3701)</span><span class="sxs-lookup"><span data-stu-id="166a4-271">dotnetcore pack3 does extra tag splitting - [#3701](https://github.com/NuGet/Home/issues/3701)</span></span>

- <span data-ttu-id="166a4-272">dotnet</span><span class="sxs-lookup"><span data-stu-id="166a4-272">dotnet</span></span>
  - <span data-ttu-id="166a4-273">dotnetcore Pack: při balení projektů s odkazy na balíčky dojde k duplicitnímu upozornění importu – [#3665](https://github.com/NuGet/Home/issues/3665)</span><span class="sxs-lookup"><span data-stu-id="166a4-273">dotnetcore pack: packing projects with package references results in duplicate import warning - [#3665](https://github.com/NuGet/Home/issues/3665)</span></span>

- <span data-ttu-id="166a4-274">Obnovit protokolování VS nezobrazuje se vždy [#3633](https://github.com/NuGet/Home/issues/3633)</span><span class="sxs-lookup"><span data-stu-id="166a4-274">Restore logging in VS doesn't always show - [#3633](https://github.com/NuGet/Home/issues/3633)</span></span>

- <span data-ttu-id="166a4-275">text v nápovědě pro místní prostředí NuGet se pořád zmiňují balíčky v mezipaměti – [#3592](https://github.com/NuGet/Home/issues/3592)</span><span class="sxs-lookup"><span data-stu-id="166a4-275">nuget locals help text still mentioned packages cache - [#3592](https://github.com/NuGet/Home/issues/3592)</span></span>

- <span data-ttu-id="166a4-276">Restore3 Couples PackageReferences s TargetFramework.</span><span class="sxs-lookup"><span data-stu-id="166a4-276">Restore3 couples PackageReferences with TargetFrameworks.</span></span><span data-ttu-id="166a4-277"> - [#3504](https://github.com/NuGet/Home/issues/3504)</span><span class="sxs-lookup"><span data-stu-id="166a4-277"> - [#3504](https://github.com/NuGet/Home/issues/3504)</span></span>

- <span data-ttu-id="166a4-278">NuGet vybere neočekávanou verzi nástroje MSBuild v sadě VS "15" Preview 4 – vývoj.</span><span class="sxs-lookup"><span data-stu-id="166a4-278">Nuget picks unexpected version of MSBuild in VS "15" Preview 4 dev.</span></span> <span data-ttu-id="166a4-279">příkazový řádek – [#3408](https://github.com/NuGet/Home/issues/3408)</span><span class="sxs-lookup"><span data-stu-id="166a4-279">command prompt - [#3408](https://github.com/NuGet/Home/issues/3408)</span></span>

- <span data-ttu-id="166a4-280">Při neúspěšném obnovení se zapisují soubory targets/props- [#3399](https://github.com/NuGet/Home/issues/3399)</span><span class="sxs-lookup"><span data-stu-id="166a4-280">Write out targets/props files on failed restore - [#3399](https://github.com/NuGet/Home/issues/3399)</span></span>

- <span data-ttu-id="166a4-281">NuGet během obnovování nerespektuje stejné překrytí popisovačem, když běží v sadě VS 15 Command Prompt – [#3387](https://github.com/NuGet/Home/issues/3387)</span><span class="sxs-lookup"><span data-stu-id="166a4-281">NuGet during restore doesn't respect the same compat shims as MSBuild when running in VS 15 command prompt - [#3387](https://github.com/NuGet/Home/issues/3387)</span></span>

- <span data-ttu-id="166a4-282">Opětovné povolení PackFromProjectWithDevelopmentDependencySet pro VS15- [#3272](https://github.com/NuGet/Home/issues/3272)</span><span class="sxs-lookup"><span data-stu-id="166a4-282">Re-enable PackFromProjectWithDevelopmentDependencySet for VS15 - [#3272](https://github.com/NuGet/Home/issues/3272)</span></span>

- <span data-ttu-id="166a4-283">Problémy s Blendem s využitím NuGet – [#4043](https://github.com/NuGet/Home/issues/4043)</span><span class="sxs-lookup"><span data-stu-id="166a4-283">Blend problems with NuGet - [#4043](https://github.com/NuGet/Home/issues/4043)</span></span>

- <span data-ttu-id="166a4-284">Integrace 4.0.0.2067 do úložišť CLI a sady SDK k dodávání pomocí RC2- [#4029](https://github.com/NuGet/Home/issues/4029)</span><span class="sxs-lookup"><span data-stu-id="166a4-284">Integrate 4.0.0.2067 into CLI and SDK repos to ship with RC2 - [#4029](https://github.com/NuGet/Home/issues/4029)</span></span>

- <span data-ttu-id="166a4-285">VS přestane reagovat při vytváření nové základní aplikace konzoly, uzavření řešení, otevření řešení a zavření řešení – [#4008](https://github.com/NuGet/Home/issues/4008)</span><span class="sxs-lookup"><span data-stu-id="166a4-285">VS Hangs when you Create new Core Console App, Close Solution, Open Solution and Close Solution  - [#4008](https://github.com/NuGet/Home/issues/4008)</span></span>

- <span data-ttu-id="166a4-286">Zablokování zablokuje otevírání projektu proti d15prerel. 25916.01- [#3982](https://github.com/NuGet/Home/issues/3982)</span><span class="sxs-lookup"><span data-stu-id="166a4-286">Hitting hang opening project against d15prerel.25916.01 - [#3982](https://github.com/NuGet/Home/issues/3982)</span></span>

- <span data-ttu-id="166a4-287">Oprava příkazu dotnet/nuget.exeho dokumentu nebo zprávy o nápovědě – [#3919](https://github.com/NuGet/Home/issues/3919)</span><span class="sxs-lookup"><span data-stu-id="166a4-287">Fix dotnet/nuget.exe locals doc/help message - [#3919](https://github.com/NuGet/Home/issues/3919)</span></span>

- <span data-ttu-id="166a4-288">Prozkoumejte PackTask a vyhledejte problémy s koncovým nebo úvodním [#3906](https://github.com/NuGet/Home/issues/3906) prázdných znaků.</span><span class="sxs-lookup"><span data-stu-id="166a4-288">Inspect PackTask for issues with trailing or leading whitespace - [#3906](https://github.com/NuGet/Home/issues/3906)</span></span>

- <span data-ttu-id="166a4-289">dotnet</span><span class="sxs-lookup"><span data-stu-id="166a4-289">dotnet</span></span>
  - <span data-ttu-id="166a4-290">dotnetcore Pack je balení z obj, nikoli z přihrádky – [#3880](https://github.com/NuGet/Home/issues/3880)</span><span class="sxs-lookup"><span data-stu-id="166a4-290">dotnetcore pack is packing from obj not bin - [#3880](https://github.com/NuGet/Home/issues/3880)</span></span>

- <span data-ttu-id="166a4-291">dotnet</span><span class="sxs-lookup"><span data-stu-id="166a4-291">dotnet</span></span>
  - <span data-ttu-id="166a4-292">sada dotnetcore Pack vždy ukazuje, jak nastavit verzi ProjectReference na 1.0.0- [#3874](https://github.com/NuGet/Home/issues/3874)</span><span class="sxs-lookup"><span data-stu-id="166a4-292">dotnetcore pack always seems to set ProjectReference version to 1.0.0 - [#3874](https://github.com/NuGet/Home/issues/3874)</span></span>

- <span data-ttu-id="166a4-293">dotnet</span><span class="sxs-lookup"><span data-stu-id="166a4-293">dotnet</span></span>
  - <span data-ttu-id="166a4-294">sada dotnetcore Pack se nezdařila s odkazy na projekt a <TargetFramework>  -  [#3865](https://github.com/NuGet/Home/issues/3865)</span><span class="sxs-lookup"><span data-stu-id="166a4-294">dotnetcore pack fails with project references and <TargetFramework> - [#3865](https://github.com/NuGet/Home/issues/3865)</span></span>

- <span data-ttu-id="166a4-295">LockRecursionException v ProjectSystemCache. TryGetProjectNameByShortName- [#3861](https://github.com/NuGet/Home/issues/3861)</span><span class="sxs-lookup"><span data-stu-id="166a4-295">LockRecursionException in ProjectSystemCache.TryGetProjectNameByShortName - [#3861](https://github.com/NuGet/Home/issues/3861)</span></span>

- <span data-ttu-id="166a4-296">Oříznout prázdné znaky z vlastností MSBuild – [#3819](https://github.com/NuGet/Home/issues/3819)</span><span class="sxs-lookup"><span data-stu-id="166a4-296">Trim whitespace from MSBuild properties - [#3819](https://github.com/NuGet/Home/issues/3819)</span></span>

- <span data-ttu-id="166a4-297">Konsolidovat dvě události projektu, které byly vyvolány při načtení projektu – [#3759](https://github.com/NuGet/Home/issues/3759)</span><span class="sxs-lookup"><span data-stu-id="166a4-297">Consolidate the two project events raised on project load - [#3759](https://github.com/NuGet/Home/issues/3759)</span></span>

- <span data-ttu-id="166a4-298">Knihovny P2P v `project.assets.json` souboru mají nesprávnou verzi [#3748](https://github.com/NuGet/Home/issues/3748)</span><span class="sxs-lookup"><span data-stu-id="166a4-298">P2P libraries in `project.assets.json` file have incorrect Version - [#3748](https://github.com/NuGet/Home/issues/3748)</span></span>

- <span data-ttu-id="166a4-299">Selhání obnovení kvůli nereagující kanálu a nedostupnému balíčku- [#3672](https://github.com/NuGet/Home/issues/3672)</span><span class="sxs-lookup"><span data-stu-id="166a4-299">Restore crash due to unresponsive feed and unavailable package - [#3672](https://github.com/NuGet/Home/issues/3672)</span></span>

- <span data-ttu-id="166a4-300">nuget.exe může reagovat na velké množství chybového výstupu nástroje MSBuild – [#3572](https://github.com/NuGet/Home/issues/3572)</span><span class="sxs-lookup"><span data-stu-id="166a4-300">nuget.exe could hang on a large amount of MSBuild error output - [#3572](https://github.com/NuGet/Home/issues/3572)</span></span>

- <span data-ttu-id="166a4-301">Obnovení na buildu pro Blend selže poprvé, úspěšná podruhé (v případě pevného scénáře VS) – [#2121](https://github.com/NuGet/Home/issues/2121)</span><span class="sxs-lookup"><span data-stu-id="166a4-301">Restore-on-build for Blend fails first time, succeeds second time (VS scenario fixed) - [#2121](https://github.com/NuGet/Home/issues/2121)</span></span>

### <a name="dcrs"></a><span data-ttu-id="166a4-302">Chcete odeslat obecnou</span><span class="sxs-lookup"><span data-stu-id="166a4-302">DCRs</span></span>

- <span data-ttu-id="166a4-303">migrace souboru VSIX z VSIX VSIX na V3 VSIX – [#4196](https://github.com/NuGet/Home/issues/4196)</span><span class="sxs-lookup"><span data-stu-id="166a4-303">migrate vsix from v2 vsix to v3 vsix - [#4196](https://github.com/NuGet/Home/issues/4196)</span></span>

- <span data-ttu-id="166a4-304">NuGet by měl mít mechanismus pro získání cesty k souboru zámku v MSBuild- [#3351](https://github.com/NuGet/Home/issues/3351)</span><span class="sxs-lookup"><span data-stu-id="166a4-304">NuGet should have a mechanism for getting the path to the lock file in MSBuild - [#3351](https://github.com/NuGet/Home/issues/3351)</span></span>

- <span data-ttu-id="166a4-305">Přidat assety sestavení do TFM kontroly kompatibility a souboru prostředků Asset- [#3296](https://github.com/NuGet/Home/issues/3296)</span><span class="sxs-lookup"><span data-stu-id="166a4-305">Add build assets to the TFM compatibility check and assets file - [#3296](https://github.com/NuGet/Home/issues/3296)</span></span>

- <span data-ttu-id="166a4-306">Definování nové ProjectCapability "balíčku" v cílech balíčku pro povolení funkcí souvisejících s balíčky – [#4146](https://github.com/NuGet/Home/issues/4146)</span><span class="sxs-lookup"><span data-stu-id="166a4-306">Define a new ProjectCapability "Pack" in Pack targets for enabling Package related capabilities - [#4146](https://github.com/NuGet/Home/issues/4146)</span></span>

- <span data-ttu-id="166a4-307">Spustit balíček jako cíl po sestavení s podmínkou pro vlastnost MSBuild GeneratePackageOnBuild- [#4145](https://github.com/NuGet/Home/issues/4145)</span><span class="sxs-lookup"><span data-stu-id="166a4-307">Run Pack as a post build target conditioned on "GeneratePackageOnBuild" MSBuild property - [#4145](https://github.com/NuGet/Home/issues/4145)</span></span>

- <span data-ttu-id="166a4-308">K vytvoření konkrétního projektu NuGet použijte RestoreProjectStyle vlastnosti NuGet – [#4134](https://github.com/NuGet/Home/issues/4134)</span><span class="sxs-lookup"><span data-stu-id="166a4-308">Use NuGet property RestoreProjectStyle to create specific NuGet project - [#4134](https://github.com/NuGet/Home/issues/4134)</span></span>

- <span data-ttu-id="166a4-309">Přizpůsobit obnovení pro změny odkazů na přenositelné projekty – [#4076](https://github.com/NuGet/Home/issues/4076)</span><span class="sxs-lookup"><span data-stu-id="166a4-309">Adapt Restore for Transitive Project References change - [#4076](https://github.com/NuGet/Home/issues/4076)</span></span>

- <span data-ttu-id="166a4-310">Přidání vlastností NuGet do cílového souboru pro projekty jiné než UWP – [#4030](https://github.com/NuGet/Home/issues/4030)</span><span class="sxs-lookup"><span data-stu-id="166a4-310">Add NuGet properties in target file for non-UWP projects - [#4030](https://github.com/NuGet/Home/issues/4030)</span></span>

- <span data-ttu-id="166a4-311">Podpora UWP TargetPlatformVersion – [#3923](https://github.com/NuGet/Home/issues/3923)</span><span class="sxs-lookup"><span data-stu-id="166a4-311">UWP TargetPlatformVersion support - [#3923](https://github.com/NuGet/Home/issues/3923)</span></span>

- <span data-ttu-id="166a4-312">Oznamovat metadata odkazů projektu na systém projektů NuGet – [#3922](https://github.com/NuGet/Home/issues/3922)</span><span class="sxs-lookup"><span data-stu-id="166a4-312">Communicate project reference metadata to NuGet project system - [#3922](https://github.com/NuGet/Home/issues/3922)</span></span>

- <span data-ttu-id="166a4-313">Přidat uživatelské rozhraní pro režim balení – [#3921](https://github.com/NuGet/Home/issues/3921)</span><span class="sxs-lookup"><span data-stu-id="166a4-313">Add UI for packaging mode - [#3921](https://github.com/NuGet/Home/issues/3921)</span></span>

- <span data-ttu-id="166a4-314">Starší verze `.csproj` potřebuje NugetTargetMoniker a RuntimeIdentifiers nastavené v proj/targets – [#3854](https://github.com/NuGet/Home/issues/3854)</span><span class="sxs-lookup"><span data-stu-id="166a4-314">Legacy `.csproj` needs NugetTargetMoniker and RuntimeIdentifiers set in proj/targets - [#3854](https://github.com/NuGet/Home/issues/3854)</span></span>

- <span data-ttu-id="166a4-315">Instalační balíček se může překrývat s automatickým obnovením – [#3836](https://github.com/NuGet/Home/issues/3836)</span><span class="sxs-lookup"><span data-stu-id="166a4-315">Install package may overlap with auto-restore - [#3836](https://github.com/NuGet/Home/issues/3836)</span></span>

- <span data-ttu-id="166a4-316">QueryStatus místní nabídky se nestane, když VSPackage není načten – [#3835](https://github.com/NuGet/Home/issues/3835)</span><span class="sxs-lookup"><span data-stu-id="166a4-316">Context menu QueryStatus doesn't happen when VSPackage is not loaded - [#3835](https://github.com/NuGet/Home/issues/3835)</span></span>

- <span data-ttu-id="166a4-317">Obnovení řešení a obnovení buildu se pořád zobrazují dialogy – [#3789](https://github.com/NuGet/Home/issues/3789)</span><span class="sxs-lookup"><span data-stu-id="166a4-317">Solution Restore and Build Restore still show dialogs - [#3789](https://github.com/NuGet/Home/issues/3789)</span></span>

- <span data-ttu-id="166a4-318">Izolace verze VSSDK v NuGet. buildy řešení klientů – [#3890](https://github.com/NuGet/Home/issues/3890)</span><span class="sxs-lookup"><span data-stu-id="166a4-318">Isolate VSSDK version in NuGet.Clients solution build - [#3890](https://github.com/NuGet/Home/issues/3890)</span></span>

## <a name="links-to-github-issues-fixed-in-rtm"></a><span data-ttu-id="166a4-319">Odkazy na problémy GitHubu opravené ve verzi RTM</span><span class="sxs-lookup"><span data-stu-id="166a4-319">Links to GitHub issues fixed in RTM</span></span>
[<span data-ttu-id="166a4-320">Seznam problémů 1</span><span class="sxs-lookup"><span data-stu-id="166a4-320">Issues list 1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RTM")  
[<span data-ttu-id="166a4-321">Seznam problémů 2</span><span class="sxs-lookup"><span data-stu-id="166a4-321">Issues list 2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC4")  
[<span data-ttu-id="166a4-322">Seznam problémů 3</span><span class="sxs-lookup"><span data-stu-id="166a4-322">Issues list 3</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC3")  
[<span data-ttu-id="166a4-323">Seznam problémů 4</span><span class="sxs-lookup"><span data-stu-id="166a4-323">Issues list 4</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC2")  
[<span data-ttu-id="166a4-324">Seznam problémů 5</span><span class="sxs-lookup"><span data-stu-id="166a4-324">Issues list 5</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC")
