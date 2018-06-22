---
title: Poznámky k verzi RC NuGet 4.0
description: Poznámky k verzi pro NuGet 4.0 RTM, včetně známé problémy, opravy chyb, přidaných funkcí a chcete.
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 03/03/2017
ms.topic: conceptual
ms.openlocfilehash: f1c5408f75966068e8fa11e63118426bbf562047
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/28/2018
ms.locfileid: "32045084"
---
# <a name="nuget-40-rtm-release-notes"></a><span data-ttu-id="1845c-103">Poznámky k verzi 4.0 RTM NuGet</span><span class="sxs-lookup"><span data-stu-id="1845c-103">NuGet 4.0 RTM Release Notes</span></span>

<span data-ttu-id="1845c-104">[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) se dodává s 4.0 NuGet, který přidává podporu pro .NET Core, má spoustu kvalita opravy a zvyšuje výkon.</span><span class="sxs-lookup"><span data-stu-id="1845c-104">[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.0 which adds support for .NET Core, has a bunch of quality fixes and improves performance.</span></span> <span data-ttu-id="1845c-105">Tato verze přináší také několik vylepšení, jako je podpora pro PackageReference, příkazy pro balíčky NuGet jako MSBuild cíle, pozadí balíček obnovení a další.</span><span class="sxs-lookup"><span data-stu-id="1845c-105">This release also brings several improvements like support for PackageReference, NuGet commands as MSBuild targets, background package restores, and more.</span></span>

## <a name="known-issues"></a><span data-ttu-id="1845c-106">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="1845c-106">Known issues</span></span>

### <a name="nuget-restore-may-fail-when-you-have-multiple-projects-referencing-another-project-in-a-solution"></a><span data-ttu-id="1845c-107">Když máte několik projektů, které se odkazují na jiný projekt v řešení, může selhat obnovení NuGet</span><span class="sxs-lookup"><span data-stu-id="1845c-107">NuGet restore may fail when you have multiple projects referencing another project in a solution</span></span>

#### <a name="issue"></a><span data-ttu-id="1845c-108">Problém</span><span class="sxs-lookup"><span data-stu-id="1845c-108">Issue</span></span>

<span data-ttu-id="1845c-109">Pokud v řešení máte odkazy na stejný projekt s jinou velikostí písmen nebo s jinými relativními cestami, obnovení NuGet nemusí fungovat.</span><span class="sxs-lookup"><span data-stu-id="1845c-109">NuGet restore may not work if, in a solution, you have project references to the same project with different casing or with different relative paths.</span></span> [<span data-ttu-id="1845c-110">NuGet#4574</span><span class="sxs-lookup"><span data-stu-id="1845c-110">NuGet#4574</span></span>](https://github.com/NuGet/Home/issues/4574)

#### <a name="workaround"></a><span data-ttu-id="1845c-111">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="1845c-111">Workaround</span></span>

<span data-ttu-id="1845c-112">Opravte velikost písmen nebo relativní cesty tak, aby pro všechny odkazy na projekt byly stejné.</span><span class="sxs-lookup"><span data-stu-id="1845c-112">Fix the casings or relative paths to be the same for all project references.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="1845c-113">Při používání konzoly Správce balíčků nemusí fungovat klávesa Enter</span><span class="sxs-lookup"><span data-stu-id="1845c-113">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="1845c-114">Problém</span><span class="sxs-lookup"><span data-stu-id="1845c-114">Issue</span></span>

<span data-ttu-id="1845c-115">V konzole Správce balíčků občas nefunguje klávesa Enter.</span><span class="sxs-lookup"><span data-stu-id="1845c-115">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="1845c-116">Když toto chování zpozorujete, zjistěte prosím, jak to vypadá s opravou, a poskytněte jakékoli další užitečné informace o postupu, jak tuto chybu reprodukovat.</span><span class="sxs-lookup"><span data-stu-id="1845c-116">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="1845c-117">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="1845c-117">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="1845c-118">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="1845c-118">Workaround</span></span>

<span data-ttu-id="1845c-119">Před otevřením řešení restartujte Visual Studio a otevřete konzolu PMC.</span><span class="sxs-lookup"><span data-stu-id="1845c-119">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="1845c-120">Případně, zkuste odstranit `project.lock.json` a opakujte obnovení.</span><span class="sxs-lookup"><span data-stu-id="1845c-120">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="in-net-core-projects-you-may-end-up-in-infinite-restore-loop-when-you-use-a-package-containing-an-assembly-with-an-invalid-signature"></a><span data-ttu-id="1845c-121">Pokud v projektech .NET Core použijete balíček, který obsahuje sestavení s neplatným podpisem, můžete uvíznout v nekonečné smyčce obnovování</span><span class="sxs-lookup"><span data-stu-id="1845c-121">In .NET Core projects, you may end up in infinite restore loop when you use a package containing an assembly with an invalid signature</span></span>

#### <a name="issue"></a><span data-ttu-id="1845c-122">Problém</span><span class="sxs-lookup"><span data-stu-id="1845c-122">Issue</span></span>

<span data-ttu-id="1845c-123">Když použijete balíček, který obsahuje sestavení s neplatným obsahem, nebo když se verze balíčku nastaví pomocí časovače DateTime, automatické obnovení balíčku běží v nekonečné smyčce.</span><span class="sxs-lookup"><span data-stu-id="1845c-123">Occassionally, when you use a package containing an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes package auto-restore to run in infinite loop.</span></span> [<span data-ttu-id="1845c-124">NuGet#4542</span><span class="sxs-lookup"><span data-stu-id="1845c-124">NuGet#4542</span></span>](https://github.com/NuGet/Home/issues/4542)

#### <a name="workaround"></a><span data-ttu-id="1845c-125">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="1845c-125">Workaround</span></span>

<span data-ttu-id="1845c-126">Pro tento problém zatím neexistuje alternativní řešení.</span><span class="sxs-lookup"><span data-stu-id="1845c-126">There is no workaround at this time.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="1845c-127">Nelze zobrazit, přidat nebo aktualizovat DotNetCLITools pomocí Správce balíčků Nuget</span><span class="sxs-lookup"><span data-stu-id="1845c-127">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="1845c-128">Problém</span><span class="sxs-lookup"><span data-stu-id="1845c-128">Issue</span></span>

<span data-ttu-id="1845c-129">Správce balíčků NuGet nezobrazuje a nepovoluje přidat nebo aktualizovat DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="1845c-129">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="1845c-130">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="1845c-130">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="1845c-131">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="1845c-131">Workaround</span></span>

<span data-ttu-id="1845c-132">V souboru projektu se musí ručně upravit DotNetCLIToolReferences.</span><span class="sxs-lookup"><span data-stu-id="1845c-132">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="nuget-restore-will-fail-when-you-set-packageid-property-for-projects"></a><span data-ttu-id="1845c-133">Když pro projekty nastavíte vlastnost PackageId, obnovení NuGet se nepovede</span><span class="sxs-lookup"><span data-stu-id="1845c-133">NuGet restore will fail when you set PackageId property for projects</span></span>

#### <a name="issue"></a><span data-ttu-id="1845c-134">Problém</span><span class="sxs-lookup"><span data-stu-id="1845c-134">Issue</span></span>

<span data-ttu-id="1845c-135">Obnovení NuGet v sadě Visual Studio nerespektuje pro projekty .NET Core vlastnost projektů PackageId.</span><span class="sxs-lookup"><span data-stu-id="1845c-135">For .NET Core projects, NuGet restore in Visual Studio does not respect PackageId property of projects.</span></span> [<span data-ttu-id="1845c-136">NuGet#4586</span><span class="sxs-lookup"><span data-stu-id="1845c-136">NuGet#4586</span></span>](https://github.com/NuGet/Home/issues/4586)

#### <a name="workaround"></a><span data-ttu-id="1845c-137">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="1845c-137">Workaround</span></span>

<span data-ttu-id="1845c-138">Spusťte obnovení pomocí příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="1845c-138">Run restore using the command-line.</span></span>

### <a name="when-your-project-does-not-have-obj-folder-package-restore-may-fail"></a><span data-ttu-id="1845c-139">Pokud váš projekt nemá složku obj, nemusí se povést obnovit balíček</span><span class="sxs-lookup"><span data-stu-id="1845c-139">When your project does not have 'obj' folder, package restore may fail</span></span>

#### <a name="issue"></a><span data-ttu-id="1845c-140">Problém</span><span class="sxs-lookup"><span data-stu-id="1845c-140">Issue</span></span>

<span data-ttu-id="1845c-141">Pokud se odstraní složka obj, sadě Visual Studio se nepovede obnovit PackageReferences.</span><span class="sxs-lookup"><span data-stu-id="1845c-141">Visual Studio fails to restore PackageReferences when 'obj' folder has been deleted.</span></span> [<span data-ttu-id="1845c-142">NuGet#4528</span><span class="sxs-lookup"><span data-stu-id="1845c-142">NuGet#4528</span></span>](https://github.com/NuGet/Home/issues/4528)

#### <a name="workaround"></a><span data-ttu-id="1845c-143">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="1845c-143">Workaround</span></span>

<span data-ttu-id="1845c-144">Vytvořte složku obj ručně a obnovení by mělo fungovat.</span><span class="sxs-lookup"><span data-stu-id="1845c-144">Create 'obj' folder manually and the restore should work.</span></span>

### <a name="manually-updating-packages-using-update-package-in-console-may-fail"></a><span data-ttu-id="1845c-145">Ruční aktualizace balíčků pomocí Update-Package v konzole může selhat</span><span class="sxs-lookup"><span data-stu-id="1845c-145">Manually updating packages using Update-Package in console may fail</span></span>

#### <a name="issue"></a><span data-ttu-id="1845c-146">Problém</span><span class="sxs-lookup"><span data-stu-id="1845c-146">Issue</span></span>

<span data-ttu-id="1845c-147">Ruční použití Update-Package v konzole funguje pro projekty, které se právě převedly, jenom jednou.</span><span class="sxs-lookup"><span data-stu-id="1845c-147">Using Update-Package manually in the console only works once for PackageReferences projects that were just converted.</span></span> [<span data-ttu-id="1845c-148">NuGet#4431</span><span class="sxs-lookup"><span data-stu-id="1845c-148">NuGet#4431</span></span>](https://github.com/NuGet/Home/issues/4431)

#### <a name="workaround"></a><span data-ttu-id="1845c-149">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="1845c-149">Workaround</span></span>

<span data-ttu-id="1845c-150">Pro tento problém zatím neexistuje alternativní řešení.</span><span class="sxs-lookup"><span data-stu-id="1845c-150">There is no workaround at this time.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="1845c-151">Změna cílení cílové verze rozhraní může vést k nekompletnímu IntelliSense</span><span class="sxs-lookup"><span data-stu-id="1845c-151">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="1845c-152">Problém</span><span class="sxs-lookup"><span data-stu-id="1845c-152">Issue</span></span>

<span data-ttu-id="1845c-153">Změna cílení cílové verze rozhraní v sadě Visual Studio může vést k nekompletnímu IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="1845c-153">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="1845c-154">To se stává, když jako formát správce balíčků používáte PackageReferences.</span><span class="sxs-lookup"><span data-stu-id="1845c-154">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="1845c-155">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="1845c-155">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="1845c-156">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="1845c-156">Workaround</span></span>

<span data-ttu-id="1845c-157">Proveďte ruční obnovení.</span><span class="sxs-lookup"><span data-stu-id="1845c-157">Do a manual restore.</span></span>

### <a name="msbuild-trestore-fails-when-a-project-targeting-net461-references-another-project-targeting-netstandard"></a><span data-ttu-id="1845c-158">Když projekt, který cílí na .NET461, odkazuje na jiný projekt, který cílí na .NETStandard, příkaz msbuild /t:restore nebude úspěšný</span><span class="sxs-lookup"><span data-stu-id="1845c-158">msbuild /t:restore fails when a project targeting .NET461 references another project targeting .NETStandard</span></span>

#### <a name="issue"></a><span data-ttu-id="1845c-159">Problém</span><span class="sxs-lookup"><span data-stu-id="1845c-159">Issue</span></span>

<span data-ttu-id="1845c-160">Když projekt založený na PackageReference, který cílí na .NET461, odkazuje na jiný projekt založený na PackageReference, který cílí na .NETStandard, příkaz msbuild /t:restore nebude úspěšný.</span><span class="sxs-lookup"><span data-stu-id="1845c-160">msbuild /t:restore fails when a PackageReferenece based project targeting .NET461 references another PackageReference based project targeting .NETStandard.</span></span>  [<span data-ttu-id="1845c-161">NuGet#4532</span><span class="sxs-lookup"><span data-stu-id="1845c-161">NuGet#4532</span></span>](https://github.com/NuGet/Home/issues/4532)

#### <a name="workaround"></a><span data-ttu-id="1845c-162">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="1845c-162">Workaround</span></span>

<span data-ttu-id="1845c-163">Pro tento problém zatím neexistuje alternativní řešení.</span><span class="sxs-lookup"><span data-stu-id="1845c-163">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a><span data-ttu-id="1845c-164">Chyby v období NuGet 4.0 RTM</span><span class="sxs-lookup"><span data-stu-id="1845c-164">Issues fixed in NuGet 4.0 RTM timeframe</span></span>

<span data-ttu-id="1845c-165">[Poznámky k verzi RC 4.0 NuGet](../release-notes/nuget-4.0-RC.md) -jsou uvedené všechny problémy opravě pro NuGet 4.0 RC</span><span class="sxs-lookup"><span data-stu-id="1845c-165">[NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md) - Lists all the issues fixed for NuGet 4.0 RC</span></span>

### <a name="features"></a><span data-ttu-id="1845c-166">Funkce</span><span class="sxs-lookup"><span data-stu-id="1845c-166">Features</span></span>

- <span data-ttu-id="1845c-167">Lokalizace řetězců v NuGet.Core.sln - [#2041](https://github.com/NuGet/Home/issues/2041)</span><span class="sxs-lookup"><span data-stu-id="1845c-167">Localize strings in NuGet.Core.sln - [#2041](https://github.com/NuGet/Home/issues/2041)</span></span>

- <span data-ttu-id="1845c-168">Vynutí Nuget načíst projekty webových aplikací v režimu dolní limit - [#4258](https://github.com/NuGet/Home/issues/4258)</span><span class="sxs-lookup"><span data-stu-id="1845c-168">Nuget forces to load web application projects in LSL mode - [#4258](https://github.com/NuGet/Home/issues/4258)</span></span>

- <span data-ttu-id="1845c-169">Podpora AutoReferenced PackageReference bloku verzi změny v uživatelském rozhraní pro balíčky "sdk nainstalován" - [#4044](https://github.com/NuGet/Home/issues/4044)</span><span class="sxs-lookup"><span data-stu-id="1845c-169">AutoReferenced PackageReference support to block version changes in UI for "sdk installed" packages - [#4044](https://github.com/NuGet/Home/issues/4044)</span></span>

- <span data-ttu-id="1845c-170">Správně komunikovat PackageSpec.Version pro všechny závislosti projektu (PackageRef) - [#3902](https://github.com/NuGet/Home/issues/3902)</span><span class="sxs-lookup"><span data-stu-id="1845c-170">Correctly communicate PackageSpec.Version for any project dependencies (PackageRef) - [#3902](https://github.com/NuGet/Home/issues/3902)</span></span>

- <span data-ttu-id="1845c-171">Podpora pro odebírání odkazů do `.csproj` z commandline(s) - [#4101](https://github.com/NuGet/Home/issues/4101)</span><span class="sxs-lookup"><span data-stu-id="1845c-171">support for removing references into `.csproj` from commandline(s) - [#4101](https://github.com/NuGet/Home/issues/4101)</span></span>

- <span data-ttu-id="1845c-172">Podpora obnovení pro projekty PackageReference (normální a xplat) a zatížení řešení Lightweight - [#4003](https://github.com/NuGet/Home/issues/4003)</span><span class="sxs-lookup"><span data-stu-id="1845c-172">Support restore for PackageReference projects (normal and xplat) and Lightweight Solution Load - [#4003](https://github.com/NuGet/Home/issues/4003)</span></span>

- <span data-ttu-id="1845c-173">Podpora pro přidání odkazů do `.csproj` z commandline(s) - [#3751](https://github.com/NuGet/Home/issues/3751)</span><span class="sxs-lookup"><span data-stu-id="1845c-173">support for adding references into `.csproj` from commandline(s) - [#3751](https://github.com/NuGet/Home/issues/3751)</span></span>

- <span data-ttu-id="1845c-174">Podpora pro zatížení Lightweight řešení pro obnovení NuGet `packages.config` nebo `project.json`  -  [#3711](https://github.com/NuGet/Home/issues/3711)</span><span class="sxs-lookup"><span data-stu-id="1845c-174">Support NuGet restore for Lightweight Solution Load for `packages.config` or `project.json` - [#3711](https://github.com/NuGet/Home/issues/3711)</span></span>

- <span data-ttu-id="1845c-175">contentFiles podporují v souboru cíle nuget generované - [#3683](https://github.com/NuGet/Home/issues/3683)</span><span class="sxs-lookup"><span data-stu-id="1845c-175">contentFiles support in nuget generated targets file - [#3683](https://github.com/NuGet/Home/issues/3683)</span></span>

- <span data-ttu-id="1845c-176">Vytvoření Mono CI pro ověření nuget.exe v systému Mac pomocí nástroje MSBuild - [#3646](https://github.com/NuGet/Home/issues/3646)</span><span class="sxs-lookup"><span data-stu-id="1845c-176">Establish a Mono CI for nuget.exe validation on Mac using MSBuild - [#3646](https://github.com/NuGet/Home/issues/3646)</span></span>

- <span data-ttu-id="1845c-177">Přesunout z v2 NuGet.Core závislosti - NuGet [#3645](https://github.com/NuGet/Home/issues/3645)</span><span class="sxs-lookup"><span data-stu-id="1845c-177">Move NuGet off of v2 NuGet.Core dependencies - [#3645](https://github.com/NuGet/Home/issues/3645)</span></span>

### <a name="bugs"></a><span data-ttu-id="1845c-178">Chyby</span><span class="sxs-lookup"><span data-stu-id="1845c-178">Bugs</span></span>

- <span data-ttu-id="1845c-179">Obnovení NuGet v sadě Visual Studio nerespektuje PackageId vlastnost projekty - [#4586](https://github.com/NuGet/Home/issues/4586)</span><span class="sxs-lookup"><span data-stu-id="1845c-179">NuGet restore in Visual Studio does not respect PackageId property of projects - [#4586](https://github.com/NuGet/Home/issues/4586)</span></span>

- <span data-ttu-id="1845c-180">Chyba NuGet ProjectSystemCache při přidání balíčku do balíčku vsix - [#4545](https://github.com/NuGet/Home/issues/4545)</span><span class="sxs-lookup"><span data-stu-id="1845c-180">NuGet ProjectSystemCache error when adding package in vsix package - [#4545](https://github.com/NuGet/Home/issues/4545)</span></span>

- <span data-ttu-id="1845c-181">Pack vyvolá výjimku, pokud se používá v projektu s více TFMs - IncludeSource [#4536](https://github.com/NuGet/Home/issues/4536)</span><span class="sxs-lookup"><span data-stu-id="1845c-181">Pack throws exception if IncludeSource is used in a project with multiple TFMs - [#4536](https://github.com/NuGet/Home/issues/4536)</span></span>

- <span data-ttu-id="1845c-182">Balíček správy - VS 2017 RC3 havárií na použití aktualizace z celé řešení [#4474](https://github.com/NuGet/Home/issues/4474)</span><span class="sxs-lookup"><span data-stu-id="1845c-182">VS 2017 RC3 crashes on using update from Solution-wide package management - [#4474](https://github.com/NuGet/Home/issues/4474)</span></span>

- <span data-ttu-id="1845c-183">Nelze odinstalovat, nově nainstalovaný balíček - [#4435](https://github.com/NuGet/Home/issues/4435)</span><span class="sxs-lookup"><span data-stu-id="1845c-183">Cannot uninstall newly installed package  - [#4435](https://github.com/NuGet/Home/issues/4435)</span></span>

- <span data-ttu-id="1845c-184">Při migraci PackageRef, hybridní řešení mají obnovení neobvyklé chování - [#4433](https://github.com/NuGet/Home/issues/4433)</span><span class="sxs-lookup"><span data-stu-id="1845c-184">When migrating to PackageRef, hybrid solutions have strange restore behavior - [#4433](https://github.com/NuGet/Home/issues/4433)</span></span>

- <span data-ttu-id="1845c-185">Vytváření krátce po spuštění NuGet operace (instalace, update, obnovení), může způsobit VS k zablokování - [#4420](https://github.com/NuGet/Home/issues/4420)</span><span class="sxs-lookup"><span data-stu-id="1845c-185">Building soon after starting NuGet operation (install, update, restore), can cause VS to Hang - [#4420](https://github.com/NuGet/Home/issues/4420)</span></span>

- <span data-ttu-id="1845c-186">Zablokování uživatelského rozhraní – zablokování inicializace NuGet.SolutionRestoreManager.RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)</span><span class="sxs-lookup"><span data-stu-id="1845c-186">UI Hang - Deadlock initializing NuGet.SolutionRestoreManager.RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)</span></span>

- <span data-ttu-id="1845c-187">Přidejte balíček příkaz má přidat verze jako atribut místo element - [#4325](https://github.com/NuGet/Home/issues/4325)</span><span class="sxs-lookup"><span data-stu-id="1845c-187">add package command should add version as attribute instead of element - [#4325](https://github.com/NuGet/Home/issues/4325)</span></span>

- <span data-ttu-id="1845c-188">DotNet.</span><span class="sxs-lookup"><span data-stu-id="1845c-188">dotnet</span></span>
  - <span data-ttu-id="1845c-189">Obnovení foo.sln dotnetcore – selže, pokud konfigurace v SLN – způsobit duplicitní (ale konfigurace rozdílové) projekty v grafu obnovení – [#4316](https://github.com/NuGet/Home/issues/4316)</span><span class="sxs-lookup"><span data-stu-id="1845c-189">dotnetcore Restore foo.sln -- fails when configurations in SLN cause duplicate (but diff config) projects in restore graph - [#4316](https://github.com/NuGet/Home/issues/4316)</span></span>

- <span data-ttu-id="1845c-190">Obsahu pouze balíčky - [#3668](https://github.com/NuGet/Home/issues/3668)</span><span class="sxs-lookup"><span data-stu-id="1845c-190">Content only packages - [#3668](https://github.com/NuGet/Home/issues/3668)</span></span>

- <span data-ttu-id="1845c-191">Ve výchozím nastavení vyjádření výslovného nesouhlasu s možností pro výběr formátu balíček - [#4468](https://github.com/NuGet/Home/issues/4468)</span><span class="sxs-lookup"><span data-stu-id="1845c-191">By default opt out of package format selector option - [#4468](https://github.com/NuGet/Home/issues/4468)</span></span>

- <span data-ttu-id="1845c-192">Perf: CreateUAP_CSharp_VS.01.1.Create projekt znovu zahrnut Duration_TotalElapsedTime podle 3,153.570 ms (149.1 %).</span><span class="sxs-lookup"><span data-stu-id="1845c-192">Perf: CreateUAP_CSharp_VS.01.1.Create project regressed Duration_TotalElapsedTime by 3,153.570 ms (149.1%).</span></span> <span data-ttu-id="1845c-193">Základní 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)</span><span class="sxs-lookup"><span data-stu-id="1845c-193">Baseline 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)</span></span>

- <span data-ttu-id="1845c-194">Perf: ManagedLangs_CS_DDRIT.0300.Rebuild řešení který poklesl Duration_TotalElapsedTime podle 1,5 sekundu.</span><span class="sxs-lookup"><span data-stu-id="1845c-194">Perf: ManagedLangs_CS_DDRIT.0300.Rebuild Solution regressed Duration_TotalElapsedTime by 1.5sec.</span></span> <span data-ttu-id="1845c-195">Základní 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)</span><span class="sxs-lookup"><span data-stu-id="1845c-195">Baseline 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)</span></span>

- <span data-ttu-id="1845c-196">Navrženém selže v projektech více TFM - [#4419](https://github.com/NuGet/Home/issues/4419)</span><span class="sxs-lookup"><span data-stu-id="1845c-196">Nomination fails in multi-TFM projects - [#4419](https://github.com/NuGet/Home/issues/4419)</span></span>

- <span data-ttu-id="1845c-197">Perf: WebForms_DDRIT.1200.Close řešení který poklesl VM_ImagesInMemory_Total_devenv podle počtu 3.000 (0,5 %).</span><span class="sxs-lookup"><span data-stu-id="1845c-197">Perf: WebForms_DDRIT.1200.Close Solution regressed VM_ImagesInMemory_Total_devenv by 3.000 Count (0.5%).</span></span> <span data-ttu-id="1845c-198">Základní 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)</span><span class="sxs-lookup"><span data-stu-id="1845c-198">Baseline 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)</span></span>

- <span data-ttu-id="1845c-199">vsfeedback - Pack upozornění při cílení na netcoreapp1.1 - [#4397](https://github.com/NuGet/Home/issues/4397)</span><span class="sxs-lookup"><span data-stu-id="1845c-199">vsfeedback - Pack warnings when targeting netcoreapp1.1 - [#4397](https://github.com/NuGet/Home/issues/4397)</span></span>

- <span data-ttu-id="1845c-200">PathTooLongException při pokusu o přidání balíčku NuGet do prázdné webové aplikace ASP.NET Core - [#4391](https://github.com/NuGet/Home/issues/4391)</span><span class="sxs-lookup"><span data-stu-id="1845c-200">PathTooLongException when trying to add a NuGet package to empty ASP.NET Core web application - [#4391](https://github.com/NuGet/Home/issues/4391)</span></span>

- <span data-ttu-id="1845c-201">Pack spouští příliš často – dotnet.</span><span class="sxs-lookup"><span data-stu-id="1845c-201">Pack runs too often -- dotnet</span></span>
  - <span data-ttu-id="1845c-202">dotnetcore pack nepodaří a dojde k dispozici je cyklická závislost cílové závislosti grafu zahrnující cílové "Pack" - [#4381](https://github.com/NuGet/Home/issues/4381)</span><span class="sxs-lookup"><span data-stu-id="1845c-202">dotnetcore pack fails with There is a circular dependency in the target dependency graph involving target "Pack"  - [#4381](https://github.com/NuGet/Home/issues/4381)</span></span>

- <span data-ttu-id="1845c-203">Pack spouští příliš často – balíček NuGet generovat neobsahuje všechny konfigurace - [#4380](https://github.com/NuGet/Home/issues/4380)</span><span class="sxs-lookup"><span data-stu-id="1845c-203">Pack runs too often -- Generate NuGet package doesn't include all the configurations  - [#4380](https://github.com/NuGet/Home/issues/4380)</span></span>

- <span data-ttu-id="1845c-204">Přidání nuget NullReferenceException s packageref v projektu C++ - [#4378](https://github.com/NuGet/Home/issues/4378)</span><span class="sxs-lookup"><span data-stu-id="1845c-204">NullReferenceException adding  nuget with packageref in  C++  project - [#4378](https://github.com/NuGet/Home/issues/4378)</span></span>

- <span data-ttu-id="1845c-205">Usnadnění: Předčítání není mluvený komentář zaškrtávací políčko Vybrat projekty, které chcete nainstalovat balíček - [#4366](https://github.com/NuGet/Home/issues/4366)</span><span class="sxs-lookup"><span data-stu-id="1845c-205">Accessibility : Narrator does not narrate the checkbox to select the projects to install the package to - [#4366](https://github.com/NuGet/Home/issues/4366)</span></span>

- <span data-ttu-id="1845c-206">NuGet VS17 k selhání připojení k VSO nebo služby VSTS kanály - 365798 chyb VS - [#4365](https://github.com/NuGet/Home/issues/4365)</span><span class="sxs-lookup"><span data-stu-id="1845c-206">NuGet VS17 sporadically fails connecting to VSO/VSTS feeds - VS Bug 365798 - [#4365](https://github.com/NuGet/Home/issues/4365)</span></span>

- <span data-ttu-id="1845c-207">contentFiles získat výstup do nesprávného umístění, pokud PackagePath Určuje cestu jako "contentFiles" - [#4348](https://github.com/NuGet/Home/issues/4348)</span><span class="sxs-lookup"><span data-stu-id="1845c-207">contentFiles get output to wrong location if PackagePath specifies path as "contentFiles" - [#4348](https://github.com/NuGet/Home/issues/4348)</span></span>

- <span data-ttu-id="1845c-208">Cíl Pack připojí PackageVersion vlastnost s VersionSuffix - [#4324](https://github.com/NuGet/Home/issues/4324)</span><span class="sxs-lookup"><span data-stu-id="1845c-208">Pack target appends PackageVersion property with VersionSuffix - [#4324](https://github.com/NuGet/Home/issues/4324)</span></span>

- <span data-ttu-id="1845c-209">Zadat cestu k balíčku nefunguje s aktualizací Service pack dotnet - [#4321](https://github.com/NuGet/Home/issues/4321)</span><span class="sxs-lookup"><span data-stu-id="1845c-209">Specifying package path doesn't work with dotnet pack - [#4321](https://github.com/NuGet/Home/issues/4321)</span></span>

- <span data-ttu-id="1845c-210">NuGet výstupy bunch upozornění o duplicitní importy během obnovení - [#4304](https://github.com/NuGet/Home/issues/4304)</span><span class="sxs-lookup"><span data-stu-id="1845c-210">NuGet outputs a bunch of warnings about duplicate imports during restore - [#4304](https://github.com/NuGet/Home/issues/4304)</span></span>

- <span data-ttu-id="1845c-211">Zvolte vypadá chybný pod tmavý motiv – dialogové okno "Správce balíčků NuGet Format" [#4300](https://github.com/NuGet/Home/issues/4300)</span><span class="sxs-lookup"><span data-stu-id="1845c-211">Choose "NuGet Package Manager Format" dialog looks bad under dark theme - [#4300](https://github.com/NuGet/Home/issues/4300)</span></span>

- <span data-ttu-id="1845c-212">VS dojít k chybě při obnovení sestavení - [#4298](https://github.com/NuGet/Home/issues/4298)</span><span class="sxs-lookup"><span data-stu-id="1845c-212">VS crash on build restore - [#4298](https://github.com/NuGet/Home/issues/4298)</span></span>

- <span data-ttu-id="1845c-213">Visual Studio zablokování Pokud přidáte TFM v targetframeworks, uložte a sestavení.</span><span class="sxs-lookup"><span data-stu-id="1845c-213">Visual Studio deadlocks if you add TFM in targetframeworks, save, then build.</span></span> <span data-ttu-id="1845c-214">10 % času - [#4295](https://github.com/NuGet/Home/issues/4295)</span><span class="sxs-lookup"><span data-stu-id="1845c-214">10% of time - [#4295](https://github.com/NuGet/Home/issues/4295)</span></span>

- <span data-ttu-id="1845c-215">nuget pack není výstup zprávu o úspěchu na balení projektu úspěšně - [#4294](https://github.com/NuGet/Home/issues/4294)</span><span class="sxs-lookup"><span data-stu-id="1845c-215">nuget pack does not output success message on packing a project successfully - [#4294](https://github.com/NuGet/Home/issues/4294)</span></span>

- <span data-ttu-id="1845c-216">PackTask nezdaří z důvodu System.IO.Compression 4.1 nebude nalezen – [#4290](https://github.com/NuGet/Home/issues/4290)</span><span class="sxs-lookup"><span data-stu-id="1845c-216">PackTask fails due to System.IO.Compression 4.1 not being found - [#4290](https://github.com/NuGet/Home/issues/4290)</span></span>

- <span data-ttu-id="1845c-217">Pack spouští příliš často – PackTask často selže s konfliktu přístupu k souboru - [#4289](https://github.com/NuGet/Home/issues/4289)</span><span class="sxs-lookup"><span data-stu-id="1845c-217">Pack runs too often -- PackTask frequently fails with file access conflict - [#4289](https://github.com/NuGet/Home/issues/4289)</span></span>

- <span data-ttu-id="1845c-218">NuGet otevře ve výstupním okně během obnovení pozadí - [#4274](https://github.com/NuGet/Home/issues/4274)</span><span class="sxs-lookup"><span data-stu-id="1845c-218">NuGet opens the output window during background restore - [#4274](https://github.com/NuGet/Home/issues/4274)</span></span>

- <span data-ttu-id="1845c-219">Vyloučit položku ServiceProvider jako nebezpečná kódování vzor, (který může způsobit zablokování) - [#4268](https://github.com/NuGet/Home/issues/4268)</span><span class="sxs-lookup"><span data-stu-id="1845c-219">Eliminate ServiceProvider as dangerous coding pattern (which can cause hangs) - [#4268](https://github.com/NuGet/Home/issues/4268)</span></span>

- <span data-ttu-id="1845c-220">Výkonu nebo UIHang - zlepšení DownloadTimeoutStream čtení - [#4266](https://github.com/NuGet/Home/issues/4266)</span><span class="sxs-lookup"><span data-stu-id="1845c-220">Perf/UIHang - Improve DownloadTimeoutStream reads - [#4266](https://github.com/NuGet/Home/issues/4266)</span></span>

- <span data-ttu-id="1845c-221">Visual Studio zablokování, když zkusíte zavřít projekt dokončil obnovení NuGet - [#4257](https://github.com/NuGet/Home/issues/4257)</span><span class="sxs-lookup"><span data-stu-id="1845c-221">Visual Studio deadlocks if you attempt to close a project before NuGet restore has finished - [#4257](https://github.com/NuGet/Home/issues/4257)</span></span>

- <span data-ttu-id="1845c-222">Problémy s PackTask a okolních `.nuspec`  -  [#4250](https://github.com/NuGet/Home/issues/4250)</span><span class="sxs-lookup"><span data-stu-id="1845c-222">Issues with PackTask and packing `.nuspec` - [#4250](https://github.com/NuGet/Home/issues/4250)</span></span>

- <span data-ttu-id="1845c-223">[vsfeedback] Nelze vyřešit balíčků nuget v novém projektu (vyžaduje restartování sady visual studio) - [#4217](https://github.com/NuGet/Home/issues/4217)</span><span class="sxs-lookup"><span data-stu-id="1845c-223">[vsfeedback] Cannot resolve nuget packages on new project (needs to restart visual studio) - [#4217](https://github.com/NuGet/Home/issues/4217)</span></span>

- <span data-ttu-id="1845c-224">[vsfeedback] "Verze" rozevírací nabídky, které zobrazuje verze balíčku k dispozici, prohry zůstane synchronizovaná s balíček vybrané nuGet... - [#4198](https://github.com/NuGet/Home/issues/4198)</span><span class="sxs-lookup"><span data-stu-id="1845c-224">[vsfeedback] The "Version" drop down that shows available package versions, struggles to stay in-sync with the selected nuGet package...  - [#4198](https://github.com/NuGet/Home/issues/4198)</span></span>

- <span data-ttu-id="1845c-225">Nuget.Client měli použít třída JoinableTaskFactory CPS při interakci s CPS zablokování - [#4185](https://github.com/NuGet/Home/issues/4185)</span><span class="sxs-lookup"><span data-stu-id="1845c-225">Nuget.Client should use CPS JoinableTaskFactory when interacting with CPS to prevent deadlocks - [#4185](https://github.com/NuGet/Home/issues/4185)</span></span>

- <span data-ttu-id="1845c-226">NuGet 3.5.0 není rozbalování `.targets` z balíčku - [#4171](https://github.com/NuGet/Home/issues/4171)</span><span class="sxs-lookup"><span data-stu-id="1845c-226">NuGet 3.5.0 not unpacking `.targets` from package - [#4171](https://github.com/NuGet/Home/issues/4171)</span></span>

- <span data-ttu-id="1845c-227">DotNet.</span><span class="sxs-lookup"><span data-stu-id="1845c-227">dotnet</span></span>
  - <span data-ttu-id="1845c-228">dotnetcore pack nepodporuje název v `.csproj`  -  [#4150](https://github.com/NuGet/Home/issues/4150)</span><span class="sxs-lookup"><span data-stu-id="1845c-228">dotnetcore pack does not support title in `.csproj` - [#4150](https://github.com/NuGet/Home/issues/4150)</span></span>

- <span data-ttu-id="1845c-229">Install-Package výsledkem dialogové okno chyby v VS2017 RC – [#4127](https://github.com/NuGet/Home/issues/4127)</span><span class="sxs-lookup"><span data-stu-id="1845c-229">Install-Package results in error dialog in VS2017 RC - [#4127](https://github.com/NuGet/Home/issues/4127)</span></span>

- <span data-ttu-id="1845c-230">Aktualizace balíčku pro rozhraní .net core projekt se nebude fungovat, jako uživatelské rozhraní není sám aktualizace prohlášení CPS nominate.</span><span class="sxs-lookup"><span data-stu-id="1845c-230">Updating a package for .net core project appears to not work, as the UI doesn't get the CPS update from the nominate.</span></span><span data-ttu-id="1845c-231"> - [#4035](https://github.com/NuGet/Home/issues/4035)</span><span class="sxs-lookup"><span data-stu-id="1845c-231"> - [#4035](https://github.com/NuGet/Home/issues/4035)</span></span>

- <span data-ttu-id="1845c-232">Zlepšení nerozpoznaný odkaz upozornění - [#3955](https://github.com/NuGet/Home/issues/3955)</span><span class="sxs-lookup"><span data-stu-id="1845c-232">Improve unresolved reference warning - [#3955](https://github.com/NuGet/Home/issues/3955)</span></span>

- <span data-ttu-id="1845c-233">DotNet.</span><span class="sxs-lookup"><span data-stu-id="1845c-233">dotnet</span></span>
  - <span data-ttu-id="1845c-234">dotnetcore pack - ProjectReference ztratí informace o verzi - [#3953](https://github.com/NuGet/Home/issues/3953)</span><span class="sxs-lookup"><span data-stu-id="1845c-234">dotnetcore pack - ProjectReference loses version information - [#3953](https://github.com/NuGet/Home/issues/3953)</span></span>

- <span data-ttu-id="1845c-235">Vytvoření aplikace pro UPW & Vytvořit projekt znovu sestavit Celkem uběhlý čas regresí - [#3873](https://github.com/NuGet/Home/issues/3873)</span><span class="sxs-lookup"><span data-stu-id="1845c-235">Create UWP app create project & rebuild total elapsed time regressions - [#3873](https://github.com/NuGet/Home/issues/3873)</span></span>

- <span data-ttu-id="1845c-236">Úspěšné obnovení zpráva se zobrazí i po chybě. během obnovení.</span><span class="sxs-lookup"><span data-stu-id="1845c-236">Successful restore message is displayed even after error during restore.</span></span><span data-ttu-id="1845c-237"> - [#3799](https://github.com/NuGet/Home/issues/3799)</span><span class="sxs-lookup"><span data-stu-id="1845c-237"> - [#3799](https://github.com/NuGet/Home/issues/3799)</span></span>

- <span data-ttu-id="1845c-238">znovu publikovat Nuget.CommandLine 3.4.4 k Nuget.org - [#2931](https://github.com/NuGet/Home/issues/2931)</span><span class="sxs-lookup"><span data-stu-id="1845c-238">re-Publish Nuget.CommandLine 3.4.4 to Nuget.org - [#2931](https://github.com/NuGet/Home/issues/2931)</span></span>

- <span data-ttu-id="1845c-239">Na migraci, změňte projekty z `project.json` k `.csproj` , se nezdaří obnovení - [#4297](https://github.com/NuGet/Home/issues/4297)</span><span class="sxs-lookup"><span data-stu-id="1845c-239">On Migrate, projects change from `project.json` to `.csproj` --- restore fails - [#4297](https://github.com/NuGet/Home/issues/4297)</span></span>

- <span data-ttu-id="1845c-240">Selhání obnovení na nově vytvořený xunit testovacího projektu - [#4296](https://github.com/NuGet/Home/issues/4296)</span><span class="sxs-lookup"><span data-stu-id="1845c-240">Restore failing on newly created xunit Test project  - [#4296](https://github.com/NuGet/Home/issues/4296)</span></span>

- <span data-ttu-id="1845c-241">Základní projekty můžete zablokuje, zamčení uživatelského rozhraní při otevření - [#4269](https://github.com/NuGet/Home/issues/4269)</span><span class="sxs-lookup"><span data-stu-id="1845c-241">Core projects can hang, lock up UI on open - [#4269](https://github.com/NuGet/Home/issues/4269)</span></span>

- <span data-ttu-id="1845c-242">Opravte soubor cíle pro úlohy sestavení – [#4267](https://github.com/NuGet/Home/issues/4267)</span><span class="sxs-lookup"><span data-stu-id="1845c-242">fix targets file for build tasks - [#4267](https://github.com/NuGet/Home/issues/4267)</span></span>

- <span data-ttu-id="1845c-243">Seznam chyb obsahuje chybu po sestavení řešení, které uvolnit odkazované projekt – [#4208](https://github.com/NuGet/Home/issues/4208)</span><span class="sxs-lookup"><span data-stu-id="1845c-243">Error list has error after build solution which unload the referenced project - [#4208](https://github.com/NuGet/Home/issues/4208)</span></span>

- <span data-ttu-id="1845c-244">MSB4057: Cíl "_GenerateRestoreGraphProjectEntry" v projektu neexistuje.</span><span class="sxs-lookup"><span data-stu-id="1845c-244">MSB4057: The target "_GenerateRestoreGraphProjectEntry" does not exist in the project.</span></span><span data-ttu-id="1845c-245"> - [#4194](https://github.com/NuGet/Home/issues/4194)</span><span class="sxs-lookup"><span data-stu-id="1845c-245"> - [#4194](https://github.com/NuGet/Home/issues/4194)</span></span>

- <span data-ttu-id="1845c-246">vsfeedback: Když vyberete všechny projekty - dojde k chybě uživatelského rozhraní správce nuget pro řešení [#4191](https://github.com/NuGet/Home/issues/4191)</span><span class="sxs-lookup"><span data-stu-id="1845c-246">vsfeedback: nuget manager ui for solution crashes when you select all projects - [#4191](https://github.com/NuGet/Home/issues/4191)</span></span>

- <span data-ttu-id="1845c-247">nuget.exe msbuildpath selže, když je koncové lomítko - [#4180](https://github.com/NuGet/Home/issues/4180)</span><span class="sxs-lookup"><span data-stu-id="1845c-247">nuget.exe msbuildpath fails when there is a trailing slash - [#4180](https://github.com/NuGet/Home/issues/4180)</span></span>

- <span data-ttu-id="1845c-248">vsfeedback: obnovení NuGet poskytnout několik upozornění odkaz na projekt pro projekt LinqToTwitter – [#4156](https://github.com/NuGet/Home/issues/4156)</span><span class="sxs-lookup"><span data-stu-id="1845c-248">vsfeedback: NuGet restore give several project reference warnings for LinqToTwitter project - [#4156](https://github.com/NuGet/Home/issues/4156)</span></span>

- <span data-ttu-id="1845c-249">Pack z `.csproj` neobsahuje atribut minClientVersion - [#4135](https://github.com/NuGet/Home/issues/4135)</span><span class="sxs-lookup"><span data-stu-id="1845c-249">Pack from `.csproj` does not include the minClientVersion attribute  - [#4135](https://github.com/NuGet/Home/issues/4135)</span></span>

- <span data-ttu-id="1845c-250">NuGet.Build.Tasks.Pack.dll dodaný zpoždění přihlášení VS2017 (d15rel 26014.00)- [#4122](https://github.com/NuGet/Home/issues/4122)</span><span class="sxs-lookup"><span data-stu-id="1845c-250">NuGet.Build.Tasks.Pack.dll shipped delay signed in VS2017 (d15rel 26014.00) - [#4122](https://github.com/NuGet/Home/issues/4122)</span></span>

- <span data-ttu-id="1845c-251">VSFeedback: Obnovení selže z projektu VS 2015 vygeneroval s CMake 3.7.1 - [#4114](https://github.com/NuGet/Home/issues/4114)</span><span class="sxs-lookup"><span data-stu-id="1845c-251">VSFeedback: Restore fails for a VS 2015 project generated with CMake 3.7.1 - [#4114](https://github.com/NuGet/Home/issues/4114)</span></span>

- <span data-ttu-id="1845c-252">VSFeedback: Chybám při obnovení mohou skrývat podrobnější chybové zprávy, které může poskytnout sestavení - [#4113](https://github.com/NuGet/Home/issues/4113)</span><span class="sxs-lookup"><span data-stu-id="1845c-252">VSFeedback: Restore errors can obscure more complete error messages that build could give - [#4113](https://github.com/NuGet/Home/issues/4113)</span></span>

- <span data-ttu-id="1845c-253">[VSFeedback] Při obnovování balíčků NuGet pro projekt webové stránky došlo k chybě: hodnota nemůže být null.</span><span class="sxs-lookup"><span data-stu-id="1845c-253">[VSFeedback] Error occurred while restoring NuGet packages for website project: Value cannot be null.</span></span><span data-ttu-id="1845c-254"> - [#4092](https://github.com/NuGet/Home/issues/4092)</span><span class="sxs-lookup"><span data-stu-id="1845c-254"> - [#4092](https://github.com/NuGet/Home/issues/4092)</span></span>

- <span data-ttu-id="1845c-255">Migrace vyvolá "Objekt odkaz výjimky" v NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker - [#4067](https://github.com/NuGet/Home/issues/4067)</span><span class="sxs-lookup"><span data-stu-id="1845c-255">Migration Throws "Object reference Exception" in NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker - [#4067](https://github.com/NuGet/Home/issues/4067)</span></span>

- <span data-ttu-id="1845c-256">DotNet.</span><span class="sxs-lookup"><span data-stu-id="1845c-256">dotnet</span></span>
  - <span data-ttu-id="1845c-257">dotnetcore pack by měla pack nástrojů s verzemi, které balíčku byl sestaven s - [#4063](https://github.com/NuGet/Home/issues/4063)</span><span class="sxs-lookup"><span data-stu-id="1845c-257">dotnetcore pack should pack tools with the versions that the package was built against - [#4063](https://github.com/NuGet/Home/issues/4063)</span></span>

- <span data-ttu-id="1845c-258">Nové pozadí obnovení zapisuje milisekund na stavovém řádku při trvá sekund obnovit - [#4036](https://github.com/NuGet/Home/issues/4036)</span><span class="sxs-lookup"><span data-stu-id="1845c-258">New background restore writes milliseconds to status bar when it takes seconds to restore - [#4036](https://github.com/NuGet/Home/issues/4036)</span></span>

- <span data-ttu-id="1845c-259">Máte překlep v Nepodařilo se vyřešit všechny odkazy na - projektu [#4018](https://github.com/NuGet/Home/issues/4018)</span><span class="sxs-lookup"><span data-stu-id="1845c-259">Typo on failed to resolve all project references - [#4018](https://github.com/NuGet/Home/issues/4018)</span></span>

- <span data-ttu-id="1845c-260">Povolte PCM pracovní postupy ve scénářích odkaz na balíček - [#4016](https://github.com/NuGet/Home/issues/4016)</span><span class="sxs-lookup"><span data-stu-id="1845c-260">Enable PCM workflows in package reference scenarios - [#4016](https://github.com/NuGet/Home/issues/4016)</span></span>

- <span data-ttu-id="1845c-261">Nelze najít nainstalované balíčky v balíčku správci uživatelské rozhraní – [#4015](https://github.com/NuGet/Home/issues/4015)</span><span class="sxs-lookup"><span data-stu-id="1845c-261">Can not find installed packages in package manager UI - [#4015](https://github.com/NuGet/Home/issues/4015)</span></span>

- <span data-ttu-id="1845c-262">DotNet.</span><span class="sxs-lookup"><span data-stu-id="1845c-262">dotnet</span></span>
  - <span data-ttu-id="1845c-263">dotnetcore pack selže, když je prázdná - PackagePath [#3993](https://github.com/NuGet/Home/issues/3993)</span><span class="sxs-lookup"><span data-stu-id="1845c-263">dotnetcore pack fails when PackagePath is empty - [#3993](https://github.com/NuGet/Home/issues/3993)</span></span>

- <span data-ttu-id="1845c-264">Obnovení selže úkol ve scénáři s více uživateli - [#3897](https://github.com/NuGet/Home/issues/3897)</span><span class="sxs-lookup"><span data-stu-id="1845c-264">Restore task fails in an multi user scenario - [#3897](https://github.com/NuGet/Home/issues/3897)</span></span>

- <span data-ttu-id="1845c-265">Nelze změnit typ obsahu, když balení pomocí úlohy Pack NuGet- [#3895](https://github.com/NuGet/Home/issues/3895)</span><span class="sxs-lookup"><span data-stu-id="1845c-265">Cannot change Content type when packing using NuGet Pack Task - [#3895](https://github.com/NuGet/Home/issues/3895)</span></span>

- <span data-ttu-id="1845c-266">Výchozí kopie ContentFiles jsou nesprávná pro MsBuild /t:pack - [#3894](https://github.com/NuGet/Home/issues/3894)</span><span class="sxs-lookup"><span data-stu-id="1845c-266">Default Copy of ContentFiles are incorrect for MsBuild /t:pack - [#3894](https://github.com/NuGet/Home/issues/3894)</span></span>

- <span data-ttu-id="1845c-267">Obnovení balíčku instalace dvojité protokoly obnovení balíčků zpráva – [#3785](https://github.com/NuGet/Home/issues/3785)</span><span class="sxs-lookup"><span data-stu-id="1845c-267">Install package restore double logs the restoring packages message - [#3785](https://github.com/NuGet/Home/issues/3785)</span></span>

- <span data-ttu-id="1845c-268">Odebrat ochranného zábradlí – obnovení "moduly runtime" oddílu použít pouze na aktuální projekt – [#3768](https://github.com/NuGet/Home/issues/3768)</span><span class="sxs-lookup"><span data-stu-id="1845c-268">Remove Guardrails - Restore of "runtimes" section should only apply to the current project - [#3768](https://github.com/NuGet/Home/issues/3768)</span></span>

- <span data-ttu-id="1845c-269">Úloha sady převádí soubory obsahu v obou se obsah nebo ' a ' contentFiles nebo '- [#3718](https://github.com/NuGet/Home/issues/3718)</span><span class="sxs-lookup"><span data-stu-id="1845c-269">Pack task puts content files in both 'content/' and 'contentFiles/' - [#3718](https://github.com/NuGet/Home/issues/3718)</span></span>

- <span data-ttu-id="1845c-270">DotNet.</span><span class="sxs-lookup"><span data-stu-id="1845c-270">dotnet</span></span>
  - <span data-ttu-id="1845c-271">dotnetcore pack3 velmi značky rozdělení - [#3701](https://github.com/NuGet/Home/issues/3701)</span><span class="sxs-lookup"><span data-stu-id="1845c-271">dotnetcore pack3 does extra tag splitting - [#3701](https://github.com/NuGet/Home/issues/3701)</span></span>

- <span data-ttu-id="1845c-272">DotNet.</span><span class="sxs-lookup"><span data-stu-id="1845c-272">dotnet</span></span>
  - <span data-ttu-id="1845c-273">dotnetcore pack: balení projekty s balíčkem odkazuje má za následek upozornění duplicitní import - [#3665](https://github.com/NuGet/Home/issues/3665)</span><span class="sxs-lookup"><span data-stu-id="1845c-273">dotnetcore pack: packing projects with package references results in duplicate import warning - [#3665](https://github.com/NuGet/Home/issues/3665)</span></span>

- <span data-ttu-id="1845c-274">Obnovení protokolování v sadě VS není vždy zobrazovat - [#3633](https://github.com/NuGet/Home/issues/3633)</span><span class="sxs-lookup"><span data-stu-id="1845c-274">Restore logging in VS doesn't always show - [#3633](https://github.com/NuGet/Home/issues/3633)</span></span>

- <span data-ttu-id="1845c-275">text nápovědy místní hodnoty – nuget uvedených stále balíčky mezipaměti - [#3592](https://github.com/NuGet/Home/issues/3592)</span><span class="sxs-lookup"><span data-stu-id="1845c-275">nuget locals help text still mentioned packages cache - [#3592](https://github.com/NuGet/Home/issues/3592)</span></span>

- <span data-ttu-id="1845c-276">Restore3 páry v odstupu PackageReferences s TargetFrameworks.</span><span class="sxs-lookup"><span data-stu-id="1845c-276">Restore3 couples PackageReferences with TargetFrameworks.</span></span><span data-ttu-id="1845c-277"> - [#3504](https://github.com/NuGet/Home/issues/3504)</span><span class="sxs-lookup"><span data-stu-id="1845c-277"> - [#3504](https://github.com/NuGet/Home/issues/3504)</span></span>

- <span data-ttu-id="1845c-278">Nuget vybere neočekávanou verzí nástroje MSBuild v sadě VS "15" Preview 4 účelem</span><span class="sxs-lookup"><span data-stu-id="1845c-278">Nuget picks unexpected version of MSBuild in VS "15" Preview 4 dev.</span></span> <span data-ttu-id="1845c-279">příkazový řádek - [#3408](https://github.com/NuGet/Home/issues/3408)</span><span class="sxs-lookup"><span data-stu-id="1845c-279">command prompt - [#3408](https://github.com/NuGet/Home/issues/3408)</span></span>

- <span data-ttu-id="1845c-280">Vypsat soubory cíle nebo props při obnovení se nezdařilo - [#3399](https://github.com/NuGet/Home/issues/3399)</span><span class="sxs-lookup"><span data-stu-id="1845c-280">Write out targets/props files on failed restore - [#3399](https://github.com/NuGet/Home/issues/3399)</span></span>

- <span data-ttu-id="1845c-281">NuGet během obnovení nerespektuje stejné překrytí compat jako MSBuild při spuštění v příkazovém řádku VS 15 - [#3387](https://github.com/NuGet/Home/issues/3387)</span><span class="sxs-lookup"><span data-stu-id="1845c-281">NuGet during restore doesn't respect the same compat shims as MSBuild when running in VS 15 command prompt - [#3387](https://github.com/NuGet/Home/issues/3387)</span></span>

- <span data-ttu-id="1845c-282">Znovu povolit PackFromProjectWithDevelopmentDependencySet pro VS15 - [#3272](https://github.com/NuGet/Home/issues/3272)</span><span class="sxs-lookup"><span data-stu-id="1845c-282">Re-enable PackFromProjectWithDevelopmentDependencySet for VS15 - [#3272](https://github.com/NuGet/Home/issues/3272)</span></span>

- <span data-ttu-id="1845c-283">Inovativně problémy s NuGet - [#4043](https://github.com/NuGet/Home/issues/4043)</span><span class="sxs-lookup"><span data-stu-id="1845c-283">Blend problems with NuGet - [#4043](https://github.com/NuGet/Home/issues/4043)</span></span>

- <span data-ttu-id="1845c-284">Integrovat 4.0.0.2067 do rozhraní příkazového řádku a sady SDK úložiště pro odeslání s RC2 - [#4029](https://github.com/NuGet/Home/issues/4029)</span><span class="sxs-lookup"><span data-stu-id="1845c-284">Integrate 4.0.0.2067 into CLI and SDK repos to ship with RC2 - [#4029](https://github.com/NuGet/Home/issues/4029)</span></span>

- <span data-ttu-id="1845c-285">VS zablokování, když vytvoříte nové základní konzolovou aplikaci, zavřete řešení, otevřete řešení a zavřít řešení - [#4008](https://github.com/NuGet/Home/issues/4008)</span><span class="sxs-lookup"><span data-stu-id="1845c-285">VS Hangs when you Create new Core Console App, Close Solution, Open Solution and Close Solution  - [#4008](https://github.com/NuGet/Home/issues/4008)</span></span>

- <span data-ttu-id="1845c-286">Stiskne zablokování otevření projektu proti d15prerel.25916.01 - [#3982](https://github.com/NuGet/Home/issues/3982)</span><span class="sxs-lookup"><span data-stu-id="1845c-286">Hitting hang opening project against d15prerel.25916.01 - [#3982](https://github.com/NuGet/Home/issues/3982)</span></span>

- <span data-ttu-id="1845c-287">Opravte dotnet/nuget.exe místní hodnoty – zpráva doc/help – [#3919](https://github.com/NuGet/Home/issues/3919)</span><span class="sxs-lookup"><span data-stu-id="1845c-287">Fix dotnet/nuget.exe locals doc/help message - [#3919](https://github.com/NuGet/Home/issues/3919)</span></span>

- <span data-ttu-id="1845c-288">Zkontrolujte PackTask pro problémy se službou koncové nebo počáteční prázdné znaky - [#3906](https://github.com/NuGet/Home/issues/3906)</span><span class="sxs-lookup"><span data-stu-id="1845c-288">Inspect PackTask for issues with trailing or leading whitespace - [#3906](https://github.com/NuGet/Home/issues/3906)</span></span>

- <span data-ttu-id="1845c-289">DotNet.</span><span class="sxs-lookup"><span data-stu-id="1845c-289">dotnet</span></span>
  - <span data-ttu-id="1845c-290">dotnetcore pack je balení z obj není bin - [#3880](https://github.com/NuGet/Home/issues/3880)</span><span class="sxs-lookup"><span data-stu-id="1845c-290">dotnetcore pack is packing from obj not bin - [#3880](https://github.com/NuGet/Home/issues/3880)</span></span>

- <span data-ttu-id="1845c-291">DotNet.</span><span class="sxs-lookup"><span data-stu-id="1845c-291">dotnet</span></span>
  - <span data-ttu-id="1845c-292">dotnetcore pack vždy zdá se, že nastavte ProjectReference verzi 1.0.0 - [#3874](https://github.com/NuGet/Home/issues/3874)</span><span class="sxs-lookup"><span data-stu-id="1845c-292">dotnetcore pack always seems to set ProjectReference version to 1.0.0 - [#3874](https://github.com/NuGet/Home/issues/3874)</span></span>

- <span data-ttu-id="1845c-293">DotNet.</span><span class="sxs-lookup"><span data-stu-id="1845c-293">dotnet</span></span>
  - <span data-ttu-id="1845c-294">dotnetcore pack se nezdaří s odkazy na projekt a <TargetFramework>  -  [#3865](https://github.com/NuGet/Home/issues/3865)</span><span class="sxs-lookup"><span data-stu-id="1845c-294">dotnetcore pack fails with project references and <TargetFramework> - [#3865](https://github.com/NuGet/Home/issues/3865)</span></span>

- <span data-ttu-id="1845c-295">LockRecursionException v ProjectSystemCache.TryGetProjectNameByShortName - [#3861](https://github.com/NuGet/Home/issues/3861)</span><span class="sxs-lookup"><span data-stu-id="1845c-295">LockRecursionException in ProjectSystemCache.TryGetProjectNameByShortName - [#3861](https://github.com/NuGet/Home/issues/3861)</span></span>

- <span data-ttu-id="1845c-296">Oříznout mezery z hodnoty vlastnosti nástroje MSBuild - [#3819](https://github.com/NuGet/Home/issues/3819)</span><span class="sxs-lookup"><span data-stu-id="1845c-296">Trim whitespace from MSBuild properties - [#3819](https://github.com/NuGet/Home/issues/3819)</span></span>

- <span data-ttu-id="1845c-297">Proveďte konsolidaci událostí dvě projektu vyvolá při načítání projektu - [#3759](https://github.com/NuGet/Home/issues/3759)</span><span class="sxs-lookup"><span data-stu-id="1845c-297">Consolidate the two project events raised on project load - [#3759](https://github.com/NuGet/Home/issues/3759)</span></span>

- <span data-ttu-id="1845c-298">Knihovny P2P v `project.assets.json` soubor mít nesprávné verze - [#3748](https://github.com/NuGet/Home/issues/3748)</span><span class="sxs-lookup"><span data-stu-id="1845c-298">P2P libraries in `project.assets.json` file have incorrect Version - [#3748](https://github.com/NuGet/Home/issues/3748)</span></span>

- <span data-ttu-id="1845c-299">Obnovení havárií kvůli reagovat informační kanál a není k dispozici balíčku - [#3672](https://github.com/NuGet/Home/issues/3672)</span><span class="sxs-lookup"><span data-stu-id="1845c-299">Restore crash due to unresponsive feed and unavailable package - [#3672](https://github.com/NuGet/Home/issues/3672)</span></span>

- <span data-ttu-id="1845c-300">nuget.exe může přestat reagovat na velké množství výstupní chyba nástroje MSBuild - [#3572](https://github.com/NuGet/Home/issues/3572)</span><span class="sxs-lookup"><span data-stu-id="1845c-300">nuget.exe could hang on a large amount of MSBuild error output - [#3572](https://github.com/NuGet/Home/issues/3572)</span></span>

- <span data-ttu-id="1845c-301">Obnovení na sestavení pro Blend selže prvním úspěšné podruhé (VS scénář pevné) - [#2121](https://github.com/NuGet/Home/issues/2121)</span><span class="sxs-lookup"><span data-stu-id="1845c-301">Restore-on-build for Blend fails first time, succeeds second time (VS scenario fixed) - [#2121](https://github.com/NuGet/Home/issues/2121)</span></span>

### <a name="dcrs"></a><span data-ttu-id="1845c-302">Chcete</span><span class="sxs-lookup"><span data-stu-id="1845c-302">DCRs</span></span>

- <span data-ttu-id="1845c-303">migrovat vsix ze v2 vsix v3 vsix - [#4196](https://github.com/NuGet/Home/issues/4196)</span><span class="sxs-lookup"><span data-stu-id="1845c-303">migrate vsix from v2 vsix to v3 vsix - [#4196](https://github.com/NuGet/Home/issues/4196)</span></span>

- <span data-ttu-id="1845c-304">NuGet by měl mít mechanismus pro získání cesty k souboru zámku v nástroji MSBuild - [#3351](https://github.com/NuGet/Home/issues/3351)</span><span class="sxs-lookup"><span data-stu-id="1845c-304">NuGet should have a mechanism for getting the path to the lock file in MSBuild - [#3351](https://github.com/NuGet/Home/issues/3351)</span></span>

- <span data-ttu-id="1845c-305">Přidat prostředky sestavení do TFM kompatibility kontroly a prostředky souboru - [#3296](https://github.com/NuGet/Home/issues/3296)</span><span class="sxs-lookup"><span data-stu-id="1845c-305">Add build assets to the TFM compatibility check and assets file - [#3296](https://github.com/NuGet/Home/issues/3296)</span></span>

- <span data-ttu-id="1845c-306">Definovat nové ProjectCapability "Pack" sadě cíle pro povolení balíček související možnosti – [#4146](https://github.com/NuGet/Home/issues/4146)</span><span class="sxs-lookup"><span data-stu-id="1845c-306">Define a new ProjectCapability "Pack" in Pack targets for enabling Package related capabilities - [#4146](https://github.com/NuGet/Home/issues/4146)</span></span>

- <span data-ttu-id="1845c-307">Spustit Pack jako metodu POST směřující sestavení cíl záleží na vlastnosti "GeneratePackageOnBuild" MSBuild - [#4145](https://github.com/NuGet/Home/issues/4145)</span><span class="sxs-lookup"><span data-stu-id="1845c-307">Run Pack as a post build target conditioned on "GeneratePackageOnBuild" MSBuild property - [#4145](https://github.com/NuGet/Home/issues/4145)</span></span>

- <span data-ttu-id="1845c-308">Vlastnost NuGet RestoreProjectStyle použít k vytvoření konkrétní NuGet projektu - [#4134](https://github.com/NuGet/Home/issues/4134)</span><span class="sxs-lookup"><span data-stu-id="1845c-308">Use NuGet property RestoreProjectStyle to create specific NuGet project - [#4134](https://github.com/NuGet/Home/issues/4134)</span></span>

- <span data-ttu-id="1845c-309">Přizpůsobit obnovení přenositelné odkazy na projekt změn - [#4076](https://github.com/NuGet/Home/issues/4076)</span><span class="sxs-lookup"><span data-stu-id="1845c-309">Adapt Restore for Transitive Project References change - [#4076](https://github.com/NuGet/Home/issues/4076)</span></span>

- <span data-ttu-id="1845c-310">Přidání vlastností NuGet v cílový soubor pro projekty bez UWP - [#4030](https://github.com/NuGet/Home/issues/4030)</span><span class="sxs-lookup"><span data-stu-id="1845c-310">Add NuGet properties in target file for non-UWP projects - [#4030](https://github.com/NuGet/Home/issues/4030)</span></span>

- <span data-ttu-id="1845c-311">Podpora UWP TargetPlatformVersion - [#3923](https://github.com/NuGet/Home/issues/3923)</span><span class="sxs-lookup"><span data-stu-id="1845c-311">UWP TargetPlatformVersion support - [#3923](https://github.com/NuGet/Home/issues/3923)</span></span>

- <span data-ttu-id="1845c-312">Komunikaci projekt odkazuje na metadata do systému NuGet projektu - [#3922](https://github.com/NuGet/Home/issues/3922)</span><span class="sxs-lookup"><span data-stu-id="1845c-312">Communicate project reference metadata to NuGet project system - [#3922](https://github.com/NuGet/Home/issues/3922)</span></span>

- <span data-ttu-id="1845c-313">Přidání uživatelského rozhraní pro balení režim – [#3921](https://github.com/NuGet/Home/issues/3921)</span><span class="sxs-lookup"><span data-stu-id="1845c-313">Add UI for packaging mode - [#3921](https://github.com/NuGet/Home/issues/3921)</span></span>

- <span data-ttu-id="1845c-314">Starší verze `.csproj` potřebuje NugetTargetMoniker a RuntimeIdentifiers nastavit v proj/cíle - [#3854](https://github.com/NuGet/Home/issues/3854)</span><span class="sxs-lookup"><span data-stu-id="1845c-314">Legacy `.csproj` needs NugetTargetMoniker and RuntimeIdentifiers set in proj/targets - [#3854](https://github.com/NuGet/Home/issues/3854)</span></span>

- <span data-ttu-id="1845c-315">Instalace balíčku se mohou překrývat s automatického obnovení - [#3836](https://github.com/NuGet/Home/issues/3836)</span><span class="sxs-lookup"><span data-stu-id="1845c-315">Install package may overlap with auto-restore - [#3836](https://github.com/NuGet/Home/issues/3836)</span></span>

- <span data-ttu-id="1845c-316">Kontextové nabídky QueryStatus nedojde, pokud není načtena VSPackage – [#3835](https://github.com/NuGet/Home/issues/3835)</span><span class="sxs-lookup"><span data-stu-id="1845c-316">Context menu QueryStatus doesn't happen when VSPackage is not loaded - [#3835](https://github.com/NuGet/Home/issues/3835)</span></span>

- <span data-ttu-id="1845c-317">Obnovení řešení a sestavení obnovení stále zobrazit dialogová okna - [#3789](https://github.com/NuGet/Home/issues/3789)</span><span class="sxs-lookup"><span data-stu-id="1845c-317">Solution Restore and Build Restore still show dialogs - [#3789](https://github.com/NuGet/Home/issues/3789)</span></span>

- <span data-ttu-id="1845c-318">Izolovat VSSDK verze sestavení řešení NuGet.Clients - [#3890](https://github.com/NuGet/Home/issues/3890)</span><span class="sxs-lookup"><span data-stu-id="1845c-318">Isolate VSSDK version in NuGet.Clients solution build - [#3890](https://github.com/NuGet/Home/issues/3890)</span></span>

## <a name="links-to-github-issues-fixed-in-rtm"></a><span data-ttu-id="1845c-319">Odkazy na Githubu chyby v RTM</span><span class="sxs-lookup"><span data-stu-id="1845c-319">Links to GitHub issues fixed in RTM</span></span>
[<span data-ttu-id="1845c-320">Seznam problémů 1</span><span class="sxs-lookup"><span data-stu-id="1845c-320">Issues list 1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RTM")  
[<span data-ttu-id="1845c-321">Seznam problémů 2</span><span class="sxs-lookup"><span data-stu-id="1845c-321">Issues list 2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC4")  
[<span data-ttu-id="1845c-322">Seznam problémů 3</span><span class="sxs-lookup"><span data-stu-id="1845c-322">Issues list 3</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC3")  
[<span data-ttu-id="1845c-323">Seznam problémů 4</span><span class="sxs-lookup"><span data-stu-id="1845c-323">Issues list 4</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC2")  
[<span data-ttu-id="1845c-324">Seznam problémů 5</span><span class="sxs-lookup"><span data-stu-id="1845c-324">Issues list 5</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC")
