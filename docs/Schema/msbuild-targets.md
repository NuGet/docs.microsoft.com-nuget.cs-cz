---
title: "NuGet pack a obnovit jako cíle MSBuild | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 4/3/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 86f7e724-2509-4d7d-aa8d-4a3fb913ded6
description: "NuGet pack a obnovení můžete pracovat přímo jako cíle MSBuild s NuGet 4.0 +."
keywords: "NuGet a MSBuild NuGet pack cíl, cíl obnovení NuGet"
ms.reviewer: karann-msft
ms.openlocfilehash: def01380e5bc3bf878e72dd437f52cd033641ca5
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="b1229-104">NuGet pack a obnovení jako cíle nástroje MSBuild</span><span class="sxs-lookup"><span data-stu-id="b1229-104">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="b1229-105">*NuGet 4.0 +*</span><span class="sxs-lookup"><span data-stu-id="b1229-105">*NuGet 4.0+*</span></span>

<span data-ttu-id="b1229-106">NuGet 4.0 + může spolupracovat přímo s informace v `.csproj` souboru bez nutnosti samostatné `.nuspec` nebo `project.json` souboru.</span><span class="sxs-lookup"><span data-stu-id="b1229-106">NuGet 4.0+ can work directly with the information in a `.csproj` file without requiring a separate `.nuspec` or `project.json` file.</span></span> <span data-ttu-id="b1229-107">Všechna metadata, která byla dříve uložená v těchto konfigurační soubory se místo toho uloží `.csproj` souboru přímo, jak je popsáno v tomto poli.</span><span class="sxs-lookup"><span data-stu-id="b1229-107">All the metadata that was previously stored in those configuration files can be instead stored in the `.csproj` file directly, as described here.</span></span>

<span data-ttu-id="b1229-108">Pomocí nástroje MSBuild 15.1 + NuGet je také prvotřídní MSBuild občanem s `pack` a `restore` cílem, jak je popsáno níže.</span><span class="sxs-lookup"><span data-stu-id="b1229-108">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="b1229-109">Tyto cíle umožňují pracovat s NuGet, stejně jako s jinými úlohy nástroje MSBuild nebo cíl.</span><span class="sxs-lookup"><span data-stu-id="b1229-109">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="b1229-110">(Pro NuGet 3.x a starší, použijte [pack](../tools/cli-ref-pack.md) a [obnovení](../tools/cli-ref-restore.md) příkazy prostřednictvím rozhraní příkazového řádku NuGet místo.)</span><span class="sxs-lookup"><span data-stu-id="b1229-110">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

<span data-ttu-id="b1229-111">V tomto tématu:</span><span class="sxs-lookup"><span data-stu-id="b1229-111">In this topic:</span></span>

- [<span data-ttu-id="b1229-112">Pořadí sestavení cílů</span><span class="sxs-lookup"><span data-stu-id="b1229-112">Target build order</span></span>](#target-build-order)
- [<span data-ttu-id="b1229-113">cíl Pack</span><span class="sxs-lookup"><span data-stu-id="b1229-113">pack target</span></span>](#pack-target)
- [<span data-ttu-id="b1229-114">scénáře aktualizací Service Pack</span><span class="sxs-lookup"><span data-stu-id="b1229-114">pack scenarios</span></span>](#pack-scenarios)
- [<span data-ttu-id="b1229-115">Cíl obnovení</span><span class="sxs-lookup"><span data-stu-id="b1229-115">restore target</span></span>](#restore-target)
- [<span data-ttu-id="b1229-116">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="b1229-116">PackageTargetFallback</span></span>](#packagetargetfallback)

## <a name="target-build-order"></a><span data-ttu-id="b1229-117">Pořadí sestavení cílů</span><span class="sxs-lookup"><span data-stu-id="b1229-117">Target build order</span></span>

<span data-ttu-id="b1229-118">Protože `pack` a `restore` jsou cíle MSBuild se dostanete k vylepšení vašeho pracovního postupu.</span><span class="sxs-lookup"><span data-stu-id="b1229-118">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="b1229-119">Řekněme například, že chcete zkopírovat vašeho balíčku do sdílené síťové složky po balení ho.</span><span class="sxs-lookup"><span data-stu-id="b1229-119">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="b1229-120">Můžete to udělat vložením následujícího textu v souboru projektu:</span><span class="sxs-lookup"><span data-stu-id="b1229-120">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
    <Copy
        SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
        DestinationFolder="\\myshare\packageshare\"
        />
</Target>
```

<span data-ttu-id="b1229-121">Podobně můžete napsat úlohy nástroje MSBuild, zápis vlastní cíl a využívat vlastnosti NuGet v úlohy nástroje MSBuild.</span><span class="sxs-lookup"><span data-stu-id="b1229-121">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="b1229-122">cíl Pack</span><span class="sxs-lookup"><span data-stu-id="b1229-122">pack target</span></span>

<span data-ttu-id="b1229-123">Při použití pack cíl, který je `msbuild /t:pack`, MSBuild nevykresluje vstupy z `.csproj` souboru místo `project.json` nebo `.nuspec` soubory.</span><span class="sxs-lookup"><span data-stu-id="b1229-123">When using the pack target, that is, `msbuild /t:pack`, MSBuild draws its inputs from the `.csproj` file rather than `project.json` or `.nuspec` files.</span></span> <span data-ttu-id="b1229-124">Následující tabulka popisuje vlastnosti nástroje MSBuild, které mohou být přidány do `.csproj` soubor v první `<PropertyGroup>` uzlu.</span><span class="sxs-lookup"><span data-stu-id="b1229-124">The table below describes the MSBuild properties that can be added to a `.csproj` file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="b1229-125">Můžete provést tyto úpravy snadno v Visual Studio 2017 a později kliknutím pravým tlačítkem na projekt a výběrem **upravit {název_projektu}** v místní nabídce.</span><span class="sxs-lookup"><span data-stu-id="b1229-125">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="b1229-126">Pro usnadnění práce v tabulce je seřazená podle vlastnost ekvivalentní v [ `.nuspec` soubor](../schema/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="b1229-126">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../schema/nuspec.md).</span></span>

<span data-ttu-id="b1229-127">Všimněte si, že `Owners` a `Summary` vlastnosti z `.nuspec` nejsou podporovány pomocí nástroje MSBuild.</span><span class="sxs-lookup"><span data-stu-id="b1229-127">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>


| <span data-ttu-id="b1229-128">Hodnota atributu/NuSpec</span><span class="sxs-lookup"><span data-stu-id="b1229-128">Attribute/NuSpec Value</span></span> | <span data-ttu-id="b1229-129">Vlastnosti nástroje MSBuild</span><span class="sxs-lookup"><span data-stu-id="b1229-129">MSBuild Property</span></span> | <span data-ttu-id="b1229-130">Výchozí</span><span class="sxs-lookup"><span data-stu-id="b1229-130">Default</span></span> | <span data-ttu-id="b1229-131">Poznámky</span><span class="sxs-lookup"><span data-stu-id="b1229-131">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="b1229-132">ID</span><span class="sxs-lookup"><span data-stu-id="b1229-132">Id</span></span> | <span data-ttu-id="b1229-133">ID balíčku</span><span class="sxs-lookup"><span data-stu-id="b1229-133">PackageId</span></span> | <span data-ttu-id="b1229-134">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="b1229-134">AssemblyName</span></span> | <span data-ttu-id="b1229-135">$(AssemblyName) z nástroje MSBuild</span><span class="sxs-lookup"><span data-stu-id="b1229-135">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="b1229-136">Version</span><span class="sxs-lookup"><span data-stu-id="b1229-136">Version</span></span> | <span data-ttu-id="b1229-137">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="b1229-137">PackageVersion</span></span> | <span data-ttu-id="b1229-138">Version</span><span class="sxs-lookup"><span data-stu-id="b1229-138">Version</span></span> | <span data-ttu-id="b1229-139">Toto je semver kompatibilní, například "1.0.0", "1.0.0-beta" nebo "1.0.0-beta-00345"</span><span class="sxs-lookup"><span data-stu-id="b1229-139">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="b1229-140">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="b1229-140">VersionPrefix</span></span> | <span data-ttu-id="b1229-141">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="b1229-141">PackageVersionPrefix</span></span> | <span data-ttu-id="b1229-142">empty</span><span class="sxs-lookup"><span data-stu-id="b1229-142">empty</span></span> | <span data-ttu-id="b1229-143">Nastavení PackageVersion přepíše PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="b1229-143">Setting PackageVersion will overwrite PackageVersionPrefix</span></span> |
| <span data-ttu-id="b1229-144">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="b1229-144">VersionSuffix</span></span> | <span data-ttu-id="b1229-145">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="b1229-145">PackageVersionSuffix</span></span> | <span data-ttu-id="b1229-146">empty</span><span class="sxs-lookup"><span data-stu-id="b1229-146">empty</span></span> | <span data-ttu-id="b1229-147">$(VersionSuffix) z nástroje MSBuild.</span><span class="sxs-lookup"><span data-stu-id="b1229-147">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="b1229-148">Nastavení PackageVersion přepíše PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="b1229-148">Setting PackageVersion will overwrite PackageVersionSuffix</span></span> | 
| <span data-ttu-id="b1229-149">Autoři</span><span class="sxs-lookup"><span data-stu-id="b1229-149">Authors</span></span> | <span data-ttu-id="b1229-150">Autoři</span><span class="sxs-lookup"><span data-stu-id="b1229-150">Authors</span></span> | <span data-ttu-id="b1229-151">Uživatelské jméno aktuálního uživatele</span><span class="sxs-lookup"><span data-stu-id="b1229-151">Username of the current user</span></span> | |
| <span data-ttu-id="b1229-152">Vlastníci</span><span class="sxs-lookup"><span data-stu-id="b1229-152">Owners</span></span> | <span data-ttu-id="b1229-153">Není k dispozici</span><span class="sxs-lookup"><span data-stu-id="b1229-153">N/A</span></span> | <span data-ttu-id="b1229-154">Není k dispozici v NuSpec</span><span class="sxs-lookup"><span data-stu-id="b1229-154">Not present in NuSpec</span></span> | |
| <span data-ttu-id="b1229-155">Název</span><span class="sxs-lookup"><span data-stu-id="b1229-155">Title</span></span> | <span data-ttu-id="b1229-156">Název</span><span class="sxs-lookup"><span data-stu-id="b1229-156">Title</span></span> | <span data-ttu-id="b1229-157">ID balíčku</span><span class="sxs-lookup"><span data-stu-id="b1229-157">The PackageId</span></span>| |
| <span data-ttu-id="b1229-158">Popis</span><span class="sxs-lookup"><span data-stu-id="b1229-158">Description</span></span> | <span data-ttu-id="b1229-159">Popis</span><span class="sxs-lookup"><span data-stu-id="b1229-159">Description</span></span> | <span data-ttu-id="b1229-160">"Balíček popis"</span><span class="sxs-lookup"><span data-stu-id="b1229-160">"Package Description"</span></span> | |
| <span data-ttu-id="b1229-161">Copyright</span><span class="sxs-lookup"><span data-stu-id="b1229-161">Copyright</span></span> | <span data-ttu-id="b1229-162">Copyright</span><span class="sxs-lookup"><span data-stu-id="b1229-162">Copyright</span></span> | <span data-ttu-id="b1229-163">empty</span><span class="sxs-lookup"><span data-stu-id="b1229-163">empty</span></span> | |
| <span data-ttu-id="b1229-164">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="b1229-164">RequireLicenseAcceptance</span></span> | <span data-ttu-id="b1229-165">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="b1229-165">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="b1229-166">false</span><span class="sxs-lookup"><span data-stu-id="b1229-166">false</span></span> | |
| <span data-ttu-id="b1229-167">Adresa LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="b1229-167">LicenseUrl</span></span> | <span data-ttu-id="b1229-168">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="b1229-168">PackageLicenseUrl</span></span> | <span data-ttu-id="b1229-169">empty</span><span class="sxs-lookup"><span data-stu-id="b1229-169">empty</span></span> | |
| <span data-ttu-id="b1229-170">Adrese ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="b1229-170">ProjectUrl</span></span> | <span data-ttu-id="b1229-171">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="b1229-171">PackageProjectUrl</span></span> | <span data-ttu-id="b1229-172">empty</span><span class="sxs-lookup"><span data-stu-id="b1229-172">empty</span></span> | |
| <span data-ttu-id="b1229-173">IconUrl</span><span class="sxs-lookup"><span data-stu-id="b1229-173">IconUrl</span></span> | <span data-ttu-id="b1229-174">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="b1229-174">PackageIconUrl</span></span> | <span data-ttu-id="b1229-175">empty</span><span class="sxs-lookup"><span data-stu-id="b1229-175">empty</span></span> | |
| <span data-ttu-id="b1229-176">Značky</span><span class="sxs-lookup"><span data-stu-id="b1229-176">Tags</span></span> | <span data-ttu-id="b1229-177">PackageTags</span><span class="sxs-lookup"><span data-stu-id="b1229-177">PackageTags</span></span> | <span data-ttu-id="b1229-178">empty</span><span class="sxs-lookup"><span data-stu-id="b1229-178">empty</span></span> | <span data-ttu-id="b1229-179">Značky jsou oddělené středníky.</span><span class="sxs-lookup"><span data-stu-id="b1229-179">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="b1229-180">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="b1229-180">ReleaseNotes</span></span> | <span data-ttu-id="b1229-181">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="b1229-181">PackageReleaseNotes</span></span> | <span data-ttu-id="b1229-182">empty</span><span class="sxs-lookup"><span data-stu-id="b1229-182">empty</span></span> | |
| <span data-ttu-id="b1229-183">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="b1229-183">RepositoryUrl</span></span> | <span data-ttu-id="b1229-184">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="b1229-184">RepositoryUrl</span></span> | <span data-ttu-id="b1229-185">empty</span><span class="sxs-lookup"><span data-stu-id="b1229-185">empty</span></span> | |
| <span data-ttu-id="b1229-186">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="b1229-186">RepositoryType</span></span> | <span data-ttu-id="b1229-187">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="b1229-187">RepositoryType</span></span> | <span data-ttu-id="b1229-188">empty</span><span class="sxs-lookup"><span data-stu-id="b1229-188">empty</span></span> | |
| <span data-ttu-id="b1229-189">PackageType</span><span class="sxs-lookup"><span data-stu-id="b1229-189">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="b1229-190">Souhrn</span><span class="sxs-lookup"><span data-stu-id="b1229-190">Summary</span></span> | <span data-ttu-id="b1229-191">Nepodporováno</span><span class="sxs-lookup"><span data-stu-id="b1229-191">Not supported</span></span> | | |


### <a name="pack-target-inputs"></a><span data-ttu-id="b1229-192">vstupy cíl Pack</span><span class="sxs-lookup"><span data-stu-id="b1229-192">pack target inputs</span></span>

- <span data-ttu-id="b1229-193">IsPackable</span><span class="sxs-lookup"><span data-stu-id="b1229-193">IsPackable</span></span>
- <span data-ttu-id="b1229-194">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="b1229-194">PackageVersion</span></span>
- <span data-ttu-id="b1229-195">ID balíčku</span><span class="sxs-lookup"><span data-stu-id="b1229-195">PackageId</span></span>
- <span data-ttu-id="b1229-196">Autoři</span><span class="sxs-lookup"><span data-stu-id="b1229-196">Authors</span></span>
- <span data-ttu-id="b1229-197">Popis</span><span class="sxs-lookup"><span data-stu-id="b1229-197">Description</span></span>
- <span data-ttu-id="b1229-198">Copyright</span><span class="sxs-lookup"><span data-stu-id="b1229-198">Copyright</span></span>
- <span data-ttu-id="b1229-199">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="b1229-199">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="b1229-200">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="b1229-200">DevelopmentDependency</span></span>
- <span data-ttu-id="b1229-201">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="b1229-201">PackageLicenseUrl</span></span>
- <span data-ttu-id="b1229-202">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="b1229-202">PackageProjectUrl</span></span>
- <span data-ttu-id="b1229-203">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="b1229-203">PackageIconUrl</span></span>
- <span data-ttu-id="b1229-204">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="b1229-204">PackageReleaseNotes</span></span>
- <span data-ttu-id="b1229-205">PackageTags</span><span class="sxs-lookup"><span data-stu-id="b1229-205">PackageTags</span></span>
- <span data-ttu-id="b1229-206">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="b1229-206">PackageOutputPath</span></span>
- <span data-ttu-id="b1229-207">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="b1229-207">IncludeSymbols</span></span>
- <span data-ttu-id="b1229-208">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="b1229-208">IncludeSource</span></span>
- <span data-ttu-id="b1229-209">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="b1229-209">PackageTypes</span></span>
- <span data-ttu-id="b1229-210">IsTool</span><span class="sxs-lookup"><span data-stu-id="b1229-210">IsTool</span></span>
- <span data-ttu-id="b1229-211">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="b1229-211">RepositoryUrl</span></span>
- <span data-ttu-id="b1229-212">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="b1229-212">RepositoryType</span></span>
- <span data-ttu-id="b1229-213">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="b1229-213">NoPackageAnalysis</span></span>
- <span data-ttu-id="b1229-214">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="b1229-214">MinClientVersion</span></span>
- <span data-ttu-id="b1229-215">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="b1229-215">IncludeBuildOutput</span></span>
- <span data-ttu-id="b1229-216">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="b1229-216">IncludeContentInPack</span></span>
- <span data-ttu-id="b1229-217">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="b1229-217">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="b1229-218">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="b1229-218">ContentTargetFolders</span></span>
- <span data-ttu-id="b1229-219">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="b1229-219">NuspecFile</span></span>
- <span data-ttu-id="b1229-220">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="b1229-220">NuspecBasePath</span></span>
- <span data-ttu-id="b1229-221">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="b1229-221">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="b1229-222">scénáře aktualizací Service Pack</span><span class="sxs-lookup"><span data-stu-id="b1229-222">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="b1229-223">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="b1229-223">PackageIconUrl</span></span>

<span data-ttu-id="b1229-224">Jako součást změny pro [NuGet problém 2582](https://github.com/NuGet/Home/issues/2582), `PackageIconUrl` bude nakonec změnit tak, aby `PackageIconUri` a může být relativní cesta k ikonu souboru, který bude zahrnut v kořenovém adresáři výsledné balíčku.</span><span class="sxs-lookup"><span data-stu-id="b1229-224">As part of the change for [NuGet Issue 2582](https://github.com/NuGet/Home/issues/2582), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="b1229-225">Výstup sestavení</span><span class="sxs-lookup"><span data-stu-id="b1229-225">Output assemblies</span></span>

<span data-ttu-id="b1229-226">`nuget pack`kopie výstupní soubory s příponami `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, a `.pri`.</span><span class="sxs-lookup"><span data-stu-id="b1229-226">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="b1229-227">Výstupní soubory, které jste zkopírovali závisí na MSBuild poskytuje z `BuiltOutputProjectGroup` cíl.</span><span class="sxs-lookup"><span data-stu-id="b1229-227">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="b1229-228">Existují dvě vlastnosti nástroje MSBuild, které můžete použít v souboru projektu nebo příkazového řádku na ovládací prvek kde přejděte výstup sestavení:</span><span class="sxs-lookup"><span data-stu-id="b1229-228">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="b1229-229">`IncludeBuildOutput`: Logická hodnota, která určuje, zda by měl být sestavení výstupu sestavení součástí balíčku.</span><span class="sxs-lookup"><span data-stu-id="b1229-229">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="b1229-230">`BuildOutputTargetFolder`: Určuje složku, ve kterém má být umístěn výstup sestavení.</span><span class="sxs-lookup"><span data-stu-id="b1229-230">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="b1229-231">Výstup sestavení (a ostatní výstupní soubory) se zkopírují do jejich odpovídajících framework složky.</span><span class="sxs-lookup"><span data-stu-id="b1229-231">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="b1229-232">Odkazy na balíček</span><span class="sxs-lookup"><span data-stu-id="b1229-232">Package references</span></span>

<span data-ttu-id="b1229-233">V tématu [balíček odkazy v souborech projektu](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="b1229-233">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="b1229-234">Projekt odkazů projektu</span><span class="sxs-lookup"><span data-stu-id="b1229-234">Project to project references</span></span>

<span data-ttu-id="b1229-235">Projekt odkazů projektu jsou považovány za ve výchozím nastavení jako odkazy na balíček nuget, například:</span><span class="sxs-lookup"><span data-stu-id="b1229-235">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="b1229-236">Pro odkaz na projekt můžete také přidat následující metadata:</span><span class="sxs-lookup"><span data-stu-id="b1229-236">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="b1229-237">Včetně obsahu v balíčku</span><span class="sxs-lookup"><span data-stu-id="b1229-237">Including content in a package</span></span>

<span data-ttu-id="b1229-238">Chcete-li zahrnout obsah, přidejte doplňující metadata do existující `<Content>` položky.</span><span class="sxs-lookup"><span data-stu-id="b1229-238">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="b1229-239">Ve výchozím nastavení všechno typ, který "Obsah" získá v balíčku zahrnutý Pokud přepíšete s položkami jako následující:</span><span class="sxs-lookup"><span data-stu-id="b1229-239">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
    <Content Include="..\win7-x64\libuv.txt">
        <Pack>false</Pack>
    </Content>
 ```

<span data-ttu-id="b1229-240">Ve výchozím nastavení, vše, co přidá do kořenového adresáře `content` a `contentFiles\any\<target_framework>` složky v balíčku a uchovává složce relativní struktury, pokud zadáte cestu k balíčku:</span><span class="sxs-lookup"><span data-stu-id="b1229-240">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">        
    <Pack>true</Pack>
    <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="b1229-241">Pokud chcete kopírovat veškerý obsah pouze na konkrétní kořenových složek bylo (místo `content` a `contentFiles` oba), můžete použít vlastnost MSBuild `ContentTargetFolders`, což výchozí nastavení "obsah; contentFiles", ale může být nastavena na žádné jiné názvy složek.</span><span class="sxs-lookup"><span data-stu-id="b1229-241">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="b1229-242">Všimněte si, aby pouze určení "contentFiles" v `ContentTargetFolders` převádí soubory v `contentFiles\any\<target_framework>` nebo `contentFiles\<language>\<target_framework>` na základě `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="b1229-242">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="b1229-243">`PackagePath`může být sadu cílových cest oddělený středníkem.</span><span class="sxs-lookup"><span data-stu-id="b1229-243">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="b1229-244">Zadání cesty prázdný balíček by soubor přidat do kořenového adresáře balíčku.</span><span class="sxs-lookup"><span data-stu-id="b1229-244">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="b1229-245">Například následující přidá `libuv.txt` k `content\myfiles`, `content\samples`a kořenového adresáře balíčku:</span><span class="sxs-lookup"><span data-stu-id="b1229-245">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="b1229-246">Je také ve vlastnosti nástroje MSBuild `$(IncludeContentInPack)`, což výchozí nastavení `true`.</span><span class="sxs-lookup"><span data-stu-id="b1229-246">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="b1229-247">Pokud je nastavena v `false` na jakýkoli projekt, pak obsah z daného projektu nejsou součástí balíček nuget.</span><span class="sxs-lookup"><span data-stu-id="b1229-247">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="b1229-248">Zahrnuje další konkrétní metadata aktualizací Service pack, kterou můžete nastavit na některou z výše uvedených položek ```<PackageCopyToOutput>``` a ```<PackageFlatten>``` které nastaví ```CopyToOutput``` a ```Flatten``` hodnoty na ```contentFiles``` položku v výstupní soubor nuspec.</span><span class="sxs-lookup"><span data-stu-id="b1229-248">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>


> [!Note]
> <span data-ttu-id="b1229-249">Vedle položky obsahu `<Pack>` a `<PackagePath>` metadata můžete také nastavit na soubory pomocí akce sestavení kompilace, EmbeddedResource, ApplicationDefinition, stránky, prostředků, SplashScreen, DesignData, DesignDataWithDesignTimeCreatableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource nebo žádný.</span><span class="sxs-lookup"><span data-stu-id="b1229-249">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreatableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="b1229-250">Pro pack připojit název souboru pro cestu k balíčku, při použití vzory expanze názvů cestu k balíčku musí končit složky oddělovací znak, jinak hodnota cestou balíčku je považován za úplnou cestu včetně názvu souboru.</span><span class="sxs-lookup"><span data-stu-id="b1229-250">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="b1229-251">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="b1229-251">IncludeSymbols</span></span>

<span data-ttu-id="b1229-252">Při použití `MSBuild /t:pack /p:IncludeSymbols=true`, odpovídající `.pdb` spolu s další výstupní soubory kopírují soubory (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="b1229-252">When using `MSBuild /t:pack /p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="b1229-253">Všimněte si, že nastavení `IncludeSymbols=true` vytvoří regulární balíček *a* balíčku symbolů.</span><span class="sxs-lookup"><span data-stu-id="b1229-253">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="b1229-254">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="b1229-254">IncludeSource</span></span>

<span data-ttu-id="b1229-255">Je to stejné nastavení jako `IncludeSymbols`kromě toho, že ho zkopíruje zdrojové soubory spolu s `.pdb` i soubory.</span><span class="sxs-lookup"><span data-stu-id="b1229-255">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="b1229-256">Všechny soubory typu `Compile` se překopírují na `src\<ProjectName>\` zachování struktura složek relativní cestu v výsledné balíčku.</span><span class="sxs-lookup"><span data-stu-id="b1229-256">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="b1229-257">Stejné také se stane pro zdrojové soubory libovolného `ProjectReference` jehož `TreatAsPackageReference` nastavena na `false`.</span><span class="sxs-lookup"><span data-stu-id="b1229-257">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="b1229-258">Pokud soubor typu kompilovat, je mimo složku projekt, pak je právě přidali do `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="b1229-258">If a file of type Compile, is outside the project folder, then it is just added to `src\<ProjectName>\`.</span></span>

### <a name="istool"></a><span data-ttu-id="b1229-259">IsTool</span><span class="sxs-lookup"><span data-stu-id="b1229-259">IsTool</span></span>

<span data-ttu-id="b1229-260">Při použití `MSBuild /t:pack /p:IsTool=true`, všechny výstupní soubory, jak je uvedeno v [výstup sestavení](#output-assemblies) scénáři se zkopírují do `tools` složky místo `lib` složky.</span><span class="sxs-lookup"><span data-stu-id="b1229-260">When using `MSBuild /t:pack /p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="b1229-261">Všimněte si, že se to neliší od `DotNetCliTool` , která je určena podle nastavení `PackageType` v `.csproj` souboru.</span><span class="sxs-lookup"><span data-stu-id="b1229-261">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="b1229-262">Balení pomocí příponou .nuspec</span><span class="sxs-lookup"><span data-stu-id="b1229-262">Packing using a .nuspec</span></span>

<span data-ttu-id="b1229-263">Můžete použít `.nuspec` soubor pack projektu za předpokladu, že soubor projektu k importu `NuGet.Build.Tasks.Pack.targets` tak, aby úloha sady mohou být provedeny.</span><span class="sxs-lookup"><span data-stu-id="b1229-263">You can use a `.nuspec` file to pack your project provided that you have a project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="b1229-264">Následující tři vlastnosti nástroje MSBuild jsou relevantní pro balení, použití `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="b1229-264">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="b1229-265">`NuspecFile`: relativní nebo absolutní cesta k `.nuspec` soubor používá pro okolních.</span><span class="sxs-lookup"><span data-stu-id="b1229-265">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="b1229-266">`NuspecProperties`: středníky oddělený seznam klíč = hodnota páry.</span><span class="sxs-lookup"><span data-stu-id="b1229-266">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="b1229-267">Vzhledem ke způsobu MSBuild příkazového řádku analýzy funguje více vlastností se musí zadat následujícím způsobem: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="b1229-267">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="b1229-268">`NuspecBasePath`: Základní cesta pro `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="b1229-268">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="b1229-269">Pokud používáte `dotnet.exe` pack projektu, použijte příkaz takto:</span><span class="sxs-lookup"><span data-stu-id="b1229-269">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="b1229-270">Pokud pomocí nástroje MSBuild pack projektu, použijte příkaz takto:</span><span class="sxs-lookup"><span data-stu-id="b1229-270">If using MSBuild to pack your project, use a command like the following:</span></span>

```
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

## <a name="restore-target"></a><span data-ttu-id="b1229-271">Cíl obnovení</span><span class="sxs-lookup"><span data-stu-id="b1229-271">restore target</span></span>

<span data-ttu-id="b1229-272">`MSBuild /t:restore`(která `nuget restore` a `dotnet restore` použít s projekty .NET Core), obnoví balíčky, kterou se odkazuje v souboru projektu následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="b1229-272">`MSBuild /t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="b1229-273">Číst všechny odkazy na projekt na projekt</span><span class="sxs-lookup"><span data-stu-id="b1229-273">Read all project to project references</span></span>
1. <span data-ttu-id="b1229-274">Přečtěte si vlastnosti projektu najít zprostředkující složku a cíl rozhraní</span><span class="sxs-lookup"><span data-stu-id="b1229-274">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="b1229-275">Předat msbuild data NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="b1229-275">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="b1229-276">Spustit obnovení</span><span class="sxs-lookup"><span data-stu-id="b1229-276">Run restore</span></span>
1. <span data-ttu-id="b1229-277">Stáhnout balíčky</span><span class="sxs-lookup"><span data-stu-id="b1229-277">Download packages</span></span>
1. <span data-ttu-id="b1229-278">Zápis soubor prostředků, cílů a props</span><span class="sxs-lookup"><span data-stu-id="b1229-278">Write assets file, targets, and props</span></span>


### <a name="restore-properties"></a><span data-ttu-id="b1229-279">Obnovit vlastnosti</span><span class="sxs-lookup"><span data-stu-id="b1229-279">Restore properties</span></span>

<span data-ttu-id="b1229-280">Nastavení další obnovení mohou pocházet z vlastnosti nástroje MSBuild v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="b1229-280">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="b1229-281">Hodnoty můžete také nastavit z příkazového řádku pomocí `/p:` přepínače (viz následující příklady).</span><span class="sxs-lookup"><span data-stu-id="b1229-281">Values can also be set from the command line using the `/p:` switch (see Examples below).</span></span>

| <span data-ttu-id="b1229-282">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="b1229-282">Property</span></span> | <span data-ttu-id="b1229-283">Popis</span><span class="sxs-lookup"><span data-stu-id="b1229-283">Description</span></span> |
|--------|--------|
| <span data-ttu-id="b1229-284">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="b1229-284">RestoreSources</span></span> | <span data-ttu-id="b1229-285">Seznam oddělený středníkem zdroji balíčků.</span><span class="sxs-lookup"><span data-stu-id="b1229-285">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="b1229-286">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="b1229-286">RestorePackagesPath</span></span> | <span data-ttu-id="b1229-287">Cesta ke složce balíčků uživatele.</span><span class="sxs-lookup"><span data-stu-id="b1229-287">User packages folder path.</span></span> |
| <span data-ttu-id="b1229-288">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="b1229-288">RestoreDisableParallel</span></span> | <span data-ttu-id="b1229-289">Limit stahování do jeden po druhém.</span><span class="sxs-lookup"><span data-stu-id="b1229-289">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="b1229-290">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="b1229-290">RestoreConfigFile</span></span> | <span data-ttu-id="b1229-291">Cesta k `Nuget.Config` lze uplatnit.</span><span class="sxs-lookup"><span data-stu-id="b1229-291">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="b1229-292">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="b1229-292">RestoreNoCache</span></span> | <span data-ttu-id="b1229-293">V případě hodnoty true nevyužívá webové mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="b1229-293">If true, avoids using the web cache.</span></span> |
| <span data-ttu-id="b1229-294">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="b1229-294">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="b1229-295">V případě hodnoty true ignoruje chybě nebo chybějící zdroje balíčků.</span><span class="sxs-lookup"><span data-stu-id="b1229-295">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="b1229-296">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="b1229-296">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="b1229-297">Cesta k `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="b1229-297">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="b1229-298">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="b1229-298">RestoreGraphProjectInput</span></span> | <span data-ttu-id="b1229-299">Seznam oddělený středníkem projekty k obnovení, který by měl obsahovat absolutní cesty.</span><span class="sxs-lookup"><span data-stu-id="b1229-299">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="b1229-300">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="b1229-300">RestoreOutputPath</span></span> | <span data-ttu-id="b1229-301">Výstupní složky, jako výchozí bude použit `obj` složky.</span><span class="sxs-lookup"><span data-stu-id="b1229-301">Output folder, defaulting to the `obj` folder.</span></span> |

<span data-ttu-id="b1229-302">**Příklady**</span><span class="sxs-lookup"><span data-stu-id="b1229-302">**Examples**</span></span>

<span data-ttu-id="b1229-303">Příkazový řádek:</span><span class="sxs-lookup"><span data-stu-id="b1229-303">Command line:</span></span>

```
msbuild /t:restore /p:RestoreConfigFile=<path>
```

<span data-ttu-id="b1229-304">Soubor projektu:</span><span class="sxs-lookup"><span data-stu-id="b1229-304">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
<PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="b1229-305">Obnovení výstupy</span><span class="sxs-lookup"><span data-stu-id="b1229-305">Restore outputs</span></span>

<span data-ttu-id="b1229-306">Obnovení vytvoří následující soubory v sestavení `obj` složky:</span><span class="sxs-lookup"><span data-stu-id="b1229-306">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="b1229-307">Soubor</span><span class="sxs-lookup"><span data-stu-id="b1229-307">File</span></span> | <span data-ttu-id="b1229-308">Popis</span><span class="sxs-lookup"><span data-stu-id="b1229-308">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="b1229-309">Dříve`project.lock.json`</span><span class="sxs-lookup"><span data-stu-id="b1229-309">Previously `project.lock.json`</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="b1229-310">Odkazy na MSBuild props součástí balíčků</span><span class="sxs-lookup"><span data-stu-id="b1229-310">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="b1229-311">Odkazy na cíle MSBuild součástí balíčků</span><span class="sxs-lookup"><span data-stu-id="b1229-311">References to MSBuild targets contained in packages</span></span> |


### <a name="packagetargetfallback"></a><span data-ttu-id="b1229-312">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="b1229-312">PackageTargetFallback</span></span> 

<span data-ttu-id="b1229-313">`PackageTargetFallback` Element umožňuje určit sadu kompatibilní cíle, který se má použít při obnovování balíčků (ekvivalent [ `imports` v `project.json` ](../schema/project-json.md#imports)).</span><span class="sxs-lookup"><span data-stu-id="b1229-313">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages (the equivalent of [`imports` in `project.json`](../schema/project-json.md#imports)).</span></span> <span data-ttu-id="b1229-314">Je navržen tak, aby balíčky, které používají dotnet. [TxM](../schema/target-frameworks.md) k práci s kompatibilní balíčky, které nejsou deklarovat dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="b1229-314">It's designed to allow packages that use a dotnet [TxM](../schema/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="b1229-315">To znamená, pokud projektu používá dotnet TxM, pak všechny balíčky, které závisí na musí také mít dotnet TxM, pokud přidáte `<PackageTargetFallback>` do projektu, aby bylo možné povolit platformy bez dotnet. aby bylo kompatibilní s dotnet.</span><span class="sxs-lookup"><span data-stu-id="b1229-315">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span> 

<span data-ttu-id="b1229-316">Například, pokud je projekt pomocí `netstandard1.6` TxM a závislý balíček obsahuje pouze `lib/net45/a.dll` a `lib/portable-net45+win81/a.dll`, pak projektu se nepovede.</span><span class="sxs-lookup"><span data-stu-id="b1229-316">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="b1229-317">Pokud chcete mají být předány se druhé knihovny DLL, pak můžete přidat `PackageTargetFallback` následujícím způsobem. Tím vyjádříte, který `portable-net45+win81` DLL je kompatibilní:</span><span class="sxs-lookup"><span data-stu-id="b1229-317">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="b1229-318">Deklarovat zálohu pro všechny cíle v projektu, nechte `Condition` atribut.</span><span class="sxs-lookup"><span data-stu-id="b1229-318">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="b1229-319">Můžete také rozšířit, všechny existující `PackageTargetFallback` zahrnutím `$(PackageTargetFallback)` jak je vidět tady:</span><span class="sxs-lookup"><span data-stu-id="b1229-319">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```


### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="b1229-320">Nahrazení jedna knihovna z obnovení grafu</span><span class="sxs-lookup"><span data-stu-id="b1229-320">Replacing one library from a restore graph</span></span>

<span data-ttu-id="b1229-321">Pokud obnovení je přináší nesprávný sestavení, je možné pro vyloučení, výchozí výběr balíčků a nahraďte ji metodou dle svého výběru.</span><span class="sxs-lookup"><span data-stu-id="b1229-321">If a restore is bringing the wrong assembly, it is possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="b1229-322">První s nejvyšší úrovní `PackageReference`, vyloučit všechny prostředky:</span><span class="sxs-lookup"><span data-stu-id="b1229-322">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
    <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="b1229-323">V dalším kroku přidejte vlastní odkaz na příslušné místní kopie knihovny DLL:</span><span class="sxs-lookup"><span data-stu-id="b1229-323">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
