---
title: "NuGet pack a obnovit jako cíle MSBuild | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 04/03/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet pack a obnovení můžete pracovat přímo jako cíle MSBuild s NuGet 4.0 +."
keywords: "NuGet a MSBuild NuGet pack cíl, cíl obnovení NuGet"
ms.reviewer:
- karann-msft
ms.openlocfilehash: 169d73709eeb17aade7d99da66bbb4f346f8093f
ms.sourcegitcommit: 24997b5345a997501fff846c9bd73610245ae0a6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/31/2018
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="06623-104">NuGet pack a obnovení jako cíle nástroje MSBuild</span><span class="sxs-lookup"><span data-stu-id="06623-104">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="06623-105">*NuGet 4.0 +*</span><span class="sxs-lookup"><span data-stu-id="06623-105">*NuGet 4.0+*</span></span>

<span data-ttu-id="06623-106">Ve formátu PackageReference NuGet 4.0 + můžete ukládat všechny manifestu metadata přímo v souboru projektu místo pomocí samostatné `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="06623-106">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="06623-107">Pomocí nástroje MSBuild 15.1 + NuGet je také prvotřídní MSBuild občanem s `pack` a `restore` cílem, jak je popsáno níže.</span><span class="sxs-lookup"><span data-stu-id="06623-107">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="06623-108">Tyto cíle umožňují pracovat s NuGet, stejně jako s jinými úlohy nástroje MSBuild nebo cíl.</span><span class="sxs-lookup"><span data-stu-id="06623-108">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="06623-109">(Pro NuGet 3.x a starší, použijte [pack](../tools/cli-ref-pack.md) a [obnovení](../tools/cli-ref-restore.md) příkazy prostřednictvím rozhraní příkazového řádku NuGet místo.)</span><span class="sxs-lookup"><span data-stu-id="06623-109">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="06623-110">Pořadí sestavení cílů</span><span class="sxs-lookup"><span data-stu-id="06623-110">Target build order</span></span>

<span data-ttu-id="06623-111">Protože `pack` a `restore` jsou cíle MSBuild se dostanete k vylepšení vašeho pracovního postupu.</span><span class="sxs-lookup"><span data-stu-id="06623-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="06623-112">Řekněme například, že chcete zkopírovat vašeho balíčku do sdílené síťové složky po balení ho.</span><span class="sxs-lookup"><span data-stu-id="06623-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="06623-113">Můžete to udělat vložením následujícího textu v souboru projektu:</span><span class="sxs-lookup"><span data-stu-id="06623-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
    <Copy
        SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
        DestinationFolder="\\myshare\packageshare\"
        />
</Target>
```

<span data-ttu-id="06623-114">Podobně můžete napsat úlohy nástroje MSBuild, zápis vlastní cíl a využívat vlastnosti NuGet v úlohy nástroje MSBuild.</span><span class="sxs-lookup"><span data-stu-id="06623-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="06623-115">cíl Pack</span><span class="sxs-lookup"><span data-stu-id="06623-115">pack target</span></span>

<span data-ttu-id="06623-116">Při použití pack cíl, který je `msbuild /t:pack`, MSBuild nevykresluje vstupy ze souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="06623-116">When using the pack target, that is, `msbuild /t:pack`, MSBuild draws its inputs from the project file.</span></span> <span data-ttu-id="06623-117">Následující tabulka popisuje vlastnosti nástroje MSBuild, které mohou být přidány do souboru projektu v první `<PropertyGroup>` uzlu.</span><span class="sxs-lookup"><span data-stu-id="06623-117">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="06623-118">Můžete provést tyto úpravy snadno v Visual Studio 2017 a později kliknutím pravým tlačítkem na projekt a výběrem **upravit {název_projektu}** v místní nabídce.</span><span class="sxs-lookup"><span data-stu-id="06623-118">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="06623-119">Pro usnadnění práce v tabulce je seřazená podle vlastnost ekvivalentní v [ `.nuspec` soubor](../schema/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="06623-119">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../schema/nuspec.md).</span></span>

<span data-ttu-id="06623-120">Všimněte si, že `Owners` a `Summary` vlastnosti z `.nuspec` nejsou podporovány pomocí nástroje MSBuild.</span><span class="sxs-lookup"><span data-stu-id="06623-120">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="06623-121">Hodnota atributu/NuSpec</span><span class="sxs-lookup"><span data-stu-id="06623-121">Attribute/NuSpec Value</span></span> | <span data-ttu-id="06623-122">Vlastnosti nástroje MSBuild</span><span class="sxs-lookup"><span data-stu-id="06623-122">MSBuild Property</span></span> | <span data-ttu-id="06623-123">Výchozí</span><span class="sxs-lookup"><span data-stu-id="06623-123">Default</span></span> | <span data-ttu-id="06623-124">Poznámky</span><span class="sxs-lookup"><span data-stu-id="06623-124">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="06623-125">ID</span><span class="sxs-lookup"><span data-stu-id="06623-125">Id</span></span> | <span data-ttu-id="06623-126">ID balíčku</span><span class="sxs-lookup"><span data-stu-id="06623-126">PackageId</span></span> | <span data-ttu-id="06623-127">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="06623-127">AssemblyName</span></span> | <span data-ttu-id="06623-128">$(AssemblyName) z nástroje MSBuild</span><span class="sxs-lookup"><span data-stu-id="06623-128">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="06623-129">Version</span><span class="sxs-lookup"><span data-stu-id="06623-129">Version</span></span> | <span data-ttu-id="06623-130">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="06623-130">PackageVersion</span></span> | <span data-ttu-id="06623-131">Version</span><span class="sxs-lookup"><span data-stu-id="06623-131">Version</span></span> | <span data-ttu-id="06623-132">Toto je semver kompatibilní, například "1.0.0", "1.0.0-beta" nebo "1.0.0-beta-00345"</span><span class="sxs-lookup"><span data-stu-id="06623-132">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="06623-133">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="06623-133">VersionPrefix</span></span> | <span data-ttu-id="06623-134">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="06623-134">PackageVersionPrefix</span></span> | <span data-ttu-id="06623-135">empty</span><span class="sxs-lookup"><span data-stu-id="06623-135">empty</span></span> | <span data-ttu-id="06623-136">Nastavení PackageVersion přepíše PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="06623-136">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="06623-137">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="06623-137">VersionSuffix</span></span> | <span data-ttu-id="06623-138">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="06623-138">PackageVersionSuffix</span></span> | <span data-ttu-id="06623-139">empty</span><span class="sxs-lookup"><span data-stu-id="06623-139">empty</span></span> | <span data-ttu-id="06623-140">$(VersionSuffix) z nástroje MSBuild.</span><span class="sxs-lookup"><span data-stu-id="06623-140">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="06623-141">Nastavení PackageVersion přepíše PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="06623-141">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="06623-142">Autoři</span><span class="sxs-lookup"><span data-stu-id="06623-142">Authors</span></span> | <span data-ttu-id="06623-143">Autoři</span><span class="sxs-lookup"><span data-stu-id="06623-143">Authors</span></span> | <span data-ttu-id="06623-144">Uživatelské jméno aktuálního uživatele</span><span class="sxs-lookup"><span data-stu-id="06623-144">Username of the current user</span></span> | |
| <span data-ttu-id="06623-145">Vlastníci</span><span class="sxs-lookup"><span data-stu-id="06623-145">Owners</span></span> | <span data-ttu-id="06623-146">Není k dispozici</span><span class="sxs-lookup"><span data-stu-id="06623-146">N/A</span></span> | <span data-ttu-id="06623-147">Není k dispozici v NuSpec</span><span class="sxs-lookup"><span data-stu-id="06623-147">Not present in NuSpec</span></span> | |
| <span data-ttu-id="06623-148">Název</span><span class="sxs-lookup"><span data-stu-id="06623-148">Title</span></span> | <span data-ttu-id="06623-149">Název</span><span class="sxs-lookup"><span data-stu-id="06623-149">Title</span></span> | <span data-ttu-id="06623-150">ID balíčku</span><span class="sxs-lookup"><span data-stu-id="06623-150">The PackageId</span></span>| |
| <span data-ttu-id="06623-151">Popis</span><span class="sxs-lookup"><span data-stu-id="06623-151">Description</span></span> | <span data-ttu-id="06623-152">Popis</span><span class="sxs-lookup"><span data-stu-id="06623-152">Description</span></span> | <span data-ttu-id="06623-153">"Balíček popis"</span><span class="sxs-lookup"><span data-stu-id="06623-153">"Package Description"</span></span> | |
| <span data-ttu-id="06623-154">Copyright</span><span class="sxs-lookup"><span data-stu-id="06623-154">Copyright</span></span> | <span data-ttu-id="06623-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="06623-155">Copyright</span></span> | <span data-ttu-id="06623-156">empty</span><span class="sxs-lookup"><span data-stu-id="06623-156">empty</span></span> | |
| <span data-ttu-id="06623-157">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="06623-157">RequireLicenseAcceptance</span></span> | <span data-ttu-id="06623-158">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="06623-158">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="06623-159">false</span><span class="sxs-lookup"><span data-stu-id="06623-159">false</span></span> | |
| <span data-ttu-id="06623-160">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="06623-160">LicenseUrl</span></span> | <span data-ttu-id="06623-161">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="06623-161">PackageLicenseUrl</span></span> | <span data-ttu-id="06623-162">empty</span><span class="sxs-lookup"><span data-stu-id="06623-162">empty</span></span> | |
| <span data-ttu-id="06623-163">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="06623-163">ProjectUrl</span></span> | <span data-ttu-id="06623-164">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="06623-164">PackageProjectUrl</span></span> | <span data-ttu-id="06623-165">empty</span><span class="sxs-lookup"><span data-stu-id="06623-165">empty</span></span> | |
| <span data-ttu-id="06623-166">IconUrl</span><span class="sxs-lookup"><span data-stu-id="06623-166">IconUrl</span></span> | <span data-ttu-id="06623-167">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="06623-167">PackageIconUrl</span></span> | <span data-ttu-id="06623-168">empty</span><span class="sxs-lookup"><span data-stu-id="06623-168">empty</span></span> | |
| <span data-ttu-id="06623-169">Značky</span><span class="sxs-lookup"><span data-stu-id="06623-169">Tags</span></span> | <span data-ttu-id="06623-170">PackageTags</span><span class="sxs-lookup"><span data-stu-id="06623-170">PackageTags</span></span> | <span data-ttu-id="06623-171">empty</span><span class="sxs-lookup"><span data-stu-id="06623-171">empty</span></span> | <span data-ttu-id="06623-172">Značky jsou oddělené středníky.</span><span class="sxs-lookup"><span data-stu-id="06623-172">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="06623-173">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="06623-173">ReleaseNotes</span></span> | <span data-ttu-id="06623-174">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="06623-174">PackageReleaseNotes</span></span> | <span data-ttu-id="06623-175">empty</span><span class="sxs-lookup"><span data-stu-id="06623-175">empty</span></span> | |
| <span data-ttu-id="06623-176">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="06623-176">RepositoryUrl</span></span> | <span data-ttu-id="06623-177">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="06623-177">RepositoryUrl</span></span> | <span data-ttu-id="06623-178">empty</span><span class="sxs-lookup"><span data-stu-id="06623-178">empty</span></span> | |
| <span data-ttu-id="06623-179">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="06623-179">RepositoryType</span></span> | <span data-ttu-id="06623-180">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="06623-180">RepositoryType</span></span> | <span data-ttu-id="06623-181">empty</span><span class="sxs-lookup"><span data-stu-id="06623-181">empty</span></span> | |
| <span data-ttu-id="06623-182">PackageType</span><span class="sxs-lookup"><span data-stu-id="06623-182">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="06623-183">Souhrn</span><span class="sxs-lookup"><span data-stu-id="06623-183">Summary</span></span> | <span data-ttu-id="06623-184">Nepodporováno</span><span class="sxs-lookup"><span data-stu-id="06623-184">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="06623-185">vstupy cíl Pack</span><span class="sxs-lookup"><span data-stu-id="06623-185">pack target inputs</span></span>

- <span data-ttu-id="06623-186">IsPackable</span><span class="sxs-lookup"><span data-stu-id="06623-186">IsPackable</span></span>
- <span data-ttu-id="06623-187">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="06623-187">PackageVersion</span></span>
- <span data-ttu-id="06623-188">ID balíčku</span><span class="sxs-lookup"><span data-stu-id="06623-188">PackageId</span></span>
- <span data-ttu-id="06623-189">Autoři</span><span class="sxs-lookup"><span data-stu-id="06623-189">Authors</span></span>
- <span data-ttu-id="06623-190">Popis</span><span class="sxs-lookup"><span data-stu-id="06623-190">Description</span></span>
- <span data-ttu-id="06623-191">Copyright</span><span class="sxs-lookup"><span data-stu-id="06623-191">Copyright</span></span>
- <span data-ttu-id="06623-192">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="06623-192">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="06623-193">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="06623-193">DevelopmentDependency</span></span>
- <span data-ttu-id="06623-194">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="06623-194">PackageLicenseUrl</span></span>
- <span data-ttu-id="06623-195">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="06623-195">PackageProjectUrl</span></span>
- <span data-ttu-id="06623-196">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="06623-196">PackageIconUrl</span></span>
- <span data-ttu-id="06623-197">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="06623-197">PackageReleaseNotes</span></span>
- <span data-ttu-id="06623-198">PackageTags</span><span class="sxs-lookup"><span data-stu-id="06623-198">PackageTags</span></span>
- <span data-ttu-id="06623-199">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="06623-199">PackageOutputPath</span></span>
- <span data-ttu-id="06623-200">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="06623-200">IncludeSymbols</span></span>
- <span data-ttu-id="06623-201">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="06623-201">IncludeSource</span></span>
- <span data-ttu-id="06623-202">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="06623-202">PackageTypes</span></span>
- <span data-ttu-id="06623-203">IsTool</span><span class="sxs-lookup"><span data-stu-id="06623-203">IsTool</span></span>
- <span data-ttu-id="06623-204">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="06623-204">RepositoryUrl</span></span>
- <span data-ttu-id="06623-205">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="06623-205">RepositoryType</span></span>
- <span data-ttu-id="06623-206">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="06623-206">NoPackageAnalysis</span></span>
- <span data-ttu-id="06623-207">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="06623-207">MinClientVersion</span></span>
- <span data-ttu-id="06623-208">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="06623-208">IncludeBuildOutput</span></span>
- <span data-ttu-id="06623-209">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="06623-209">IncludeContentInPack</span></span>
- <span data-ttu-id="06623-210">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="06623-210">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="06623-211">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="06623-211">ContentTargetFolders</span></span>
- <span data-ttu-id="06623-212">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="06623-212">NuspecFile</span></span>
- <span data-ttu-id="06623-213">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="06623-213">NuspecBasePath</span></span>
- <span data-ttu-id="06623-214">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="06623-214">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="06623-215">scénáře aktualizací Service Pack</span><span class="sxs-lookup"><span data-stu-id="06623-215">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="06623-216">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="06623-216">PackageIconUrl</span></span>

<span data-ttu-id="06623-217">Jako součást změny pro [NuGet problém 2582](https://github.com/NuGet/Home/issues/2582), `PackageIconUrl` bude nakonec změnit tak, aby `PackageIconUri` a může být relativní cesta k ikonu souboru, který bude zahrnut v kořenovém adresáři výsledné balíčku.</span><span class="sxs-lookup"><span data-stu-id="06623-217">As part of the change for [NuGet Issue 2582](https://github.com/NuGet/Home/issues/2582), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="06623-218">Výstup sestavení</span><span class="sxs-lookup"><span data-stu-id="06623-218">Output assemblies</span></span>

<span data-ttu-id="06623-219">`nuget pack`kopie výstupní soubory s příponami `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, a `.pri`.</span><span class="sxs-lookup"><span data-stu-id="06623-219">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="06623-220">Výstupní soubory, které jste zkopírovali závisí na MSBuild poskytuje z `BuiltOutputProjectGroup` cíl.</span><span class="sxs-lookup"><span data-stu-id="06623-220">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="06623-221">Existují dvě vlastnosti nástroje MSBuild, které můžete použít v souboru projektu nebo příkazového řádku na ovládací prvek kde přejděte výstup sestavení:</span><span class="sxs-lookup"><span data-stu-id="06623-221">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="06623-222">`IncludeBuildOutput`: Logická hodnota, která určuje, zda by měl být sestavení výstupu sestavení součástí balíčku.</span><span class="sxs-lookup"><span data-stu-id="06623-222">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="06623-223">`BuildOutputTargetFolder`: Určuje složku, ve kterém má být umístěn výstup sestavení.</span><span class="sxs-lookup"><span data-stu-id="06623-223">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="06623-224">Výstup sestavení (a ostatní výstupní soubory) se zkopírují do jejich odpovídajících framework složky.</span><span class="sxs-lookup"><span data-stu-id="06623-224">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="06623-225">Odkazy na balíček</span><span class="sxs-lookup"><span data-stu-id="06623-225">Package references</span></span>

<span data-ttu-id="06623-226">V tématu [balíček odkazy v souborech projektu](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="06623-226">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="06623-227">Projekt odkazů projektu</span><span class="sxs-lookup"><span data-stu-id="06623-227">Project to project references</span></span>

<span data-ttu-id="06623-228">Projekt odkazů projektu jsou považovány za ve výchozím nastavení jako odkazy na balíček nuget, například:</span><span class="sxs-lookup"><span data-stu-id="06623-228">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="06623-229">Pro odkaz na projekt můžete také přidat následující metadata:</span><span class="sxs-lookup"><span data-stu-id="06623-229">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="06623-230">Včetně obsahu v balíčku</span><span class="sxs-lookup"><span data-stu-id="06623-230">Including content in a package</span></span>

<span data-ttu-id="06623-231">Chcete-li zahrnout obsah, přidejte doplňující metadata do existující `<Content>` položky.</span><span class="sxs-lookup"><span data-stu-id="06623-231">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="06623-232">Ve výchozím nastavení všechno typ, který "Obsah" získá v balíčku zahrnutý Pokud přepíšete s položkami jako následující:</span><span class="sxs-lookup"><span data-stu-id="06623-232">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
    <Content Include="..\win7-x64\libuv.txt">
        <Pack>false</Pack>
    </Content>
 ```

<span data-ttu-id="06623-233">Ve výchozím nastavení, vše, co přidá do kořenového adresáře `content` a `contentFiles\any\<target_framework>` složky v balíčku a uchovává složce relativní struktury, pokud zadáte cestu k balíčku:</span><span class="sxs-lookup"><span data-stu-id="06623-233">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="06623-234">Pokud chcete kopírovat veškerý obsah pouze na konkrétní kořenových složek bylo (místo `content` a `contentFiles` oba), můžete použít vlastnost MSBuild `ContentTargetFolders`, což výchozí nastavení "obsah; contentFiles", ale může být nastavena na žádné jiné názvy složek.</span><span class="sxs-lookup"><span data-stu-id="06623-234">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="06623-235">Všimněte si, aby pouze určení "contentFiles" v `ContentTargetFolders` převádí soubory v `contentFiles\any\<target_framework>` nebo `contentFiles\<language>\<target_framework>` na základě `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="06623-235">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="06623-236">`PackagePath`může být sadu cílových cest oddělený středníkem.</span><span class="sxs-lookup"><span data-stu-id="06623-236">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="06623-237">Zadání cesty prázdný balíček by soubor přidat do kořenového adresáře balíčku.</span><span class="sxs-lookup"><span data-stu-id="06623-237">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="06623-238">Například následující přidá `libuv.txt` k `content\myfiles`, `content\samples`a kořenového adresáře balíčku:</span><span class="sxs-lookup"><span data-stu-id="06623-238">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="06623-239">Je také ve vlastnosti nástroje MSBuild `$(IncludeContentInPack)`, což výchozí nastavení `true`.</span><span class="sxs-lookup"><span data-stu-id="06623-239">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="06623-240">Pokud je nastavena v `false` na jakýkoli projekt, pak obsah z daného projektu nejsou součástí balíček nuget.</span><span class="sxs-lookup"><span data-stu-id="06623-240">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="06623-241">Zahrnuje další konkrétní metadata aktualizací Service pack, kterou můžete nastavit na některou z výše uvedených položek ```<PackageCopyToOutput>``` a ```<PackageFlatten>``` které nastaví ```CopyToOutput``` a ```Flatten``` hodnoty na ```contentFiles``` položku v výstupní soubor nuspec.</span><span class="sxs-lookup"><span data-stu-id="06623-241">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="06623-242">Vedle položky obsahu `<Pack>` a `<PackagePath>` metadata můžete také nastavit na soubory pomocí akce sestavení kompilace, EmbeddedResource, ApplicationDefinition, stránky, prostředků, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes , CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource nebo hodnotu None.</span><span class="sxs-lookup"><span data-stu-id="06623-242">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="06623-243">Pro pack připojit název souboru pro cestu k balíčku, při použití vzory expanze názvů cestu k balíčku musí končit složky oddělovací znak, jinak hodnota cestou balíčku je považován za úplnou cestu včetně názvu souboru.</span><span class="sxs-lookup"><span data-stu-id="06623-243">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="06623-244">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="06623-244">IncludeSymbols</span></span>

<span data-ttu-id="06623-245">Při použití `MSBuild /t:pack /p:IncludeSymbols=true`, odpovídající `.pdb` spolu s další výstupní soubory kopírují soubory (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="06623-245">When using `MSBuild /t:pack /p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="06623-246">Všimněte si, že nastavení `IncludeSymbols=true` vytvoří regulární balíček *a* balíčku symbolů.</span><span class="sxs-lookup"><span data-stu-id="06623-246">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="06623-247">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="06623-247">IncludeSource</span></span>

<span data-ttu-id="06623-248">Je to stejné nastavení jako `IncludeSymbols`kromě toho, že ho zkopíruje zdrojové soubory spolu s `.pdb` i soubory.</span><span class="sxs-lookup"><span data-stu-id="06623-248">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="06623-249">Všechny soubory typu `Compile` se překopírují na `src\<ProjectName>\` zachování struktura složek relativní cestu v výsledné balíčku.</span><span class="sxs-lookup"><span data-stu-id="06623-249">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="06623-250">Stejné také se stane pro zdrojové soubory libovolného `ProjectReference` jehož `TreatAsPackageReference` nastavena na `false`.</span><span class="sxs-lookup"><span data-stu-id="06623-250">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="06623-251">Pokud soubor typu kompilovat, je mimo složku projekt, pak je právě přidali do `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="06623-251">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="istool"></a><span data-ttu-id="06623-252">IsTool</span><span class="sxs-lookup"><span data-stu-id="06623-252">IsTool</span></span>

<span data-ttu-id="06623-253">Při použití `MSBuild /t:pack /p:IsTool=true`, všechny výstupní soubory, jak je uvedeno v [výstup sestavení](#output-assemblies) scénáři se zkopírují do `tools` složky místo `lib` složky.</span><span class="sxs-lookup"><span data-stu-id="06623-253">When using `MSBuild /t:pack /p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="06623-254">Všimněte si, že se to neliší od `DotNetCliTool` , která je určena podle nastavení `PackageType` v `.csproj` souboru.</span><span class="sxs-lookup"><span data-stu-id="06623-254">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="06623-255">Balení pomocí příponou .nuspec</span><span class="sxs-lookup"><span data-stu-id="06623-255">Packing using a .nuspec</span></span>

<span data-ttu-id="06623-256">Můžete použít `.nuspec` soubor pack projektu za předpokladu, že soubor projektu k importu `NuGet.Build.Tasks.Pack.targets` tak, aby úloha sady mohou být provedeny.</span><span class="sxs-lookup"><span data-stu-id="06623-256">You can use a `.nuspec` file to pack your project provided that you have a project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="06623-257">Následující tři vlastnosti nástroje MSBuild jsou relevantní pro balení, použití `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="06623-257">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="06623-258">`NuspecFile`: relativní nebo absolutní cesta k `.nuspec` soubor používá pro okolních.</span><span class="sxs-lookup"><span data-stu-id="06623-258">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="06623-259">`NuspecProperties`: středníky oddělený seznam klíč = hodnota páry.</span><span class="sxs-lookup"><span data-stu-id="06623-259">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="06623-260">Vzhledem ke způsobu MSBuild příkazového řádku analýzy funguje více vlastností se musí zadat následujícím způsobem: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="06623-260">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="06623-261">`NuspecBasePath`: Základní cesta pro `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="06623-261">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="06623-262">Pokud používáte `dotnet.exe` pack projektu, použijte příkaz takto:</span><span class="sxs-lookup"><span data-stu-id="06623-262">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="06623-263">Pokud pomocí nástroje MSBuild pack projektu, použijte příkaz takto:</span><span class="sxs-lookup"><span data-stu-id="06623-263">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

## <a name="restore-target"></a><span data-ttu-id="06623-264">Cíl obnovení</span><span class="sxs-lookup"><span data-stu-id="06623-264">restore target</span></span>

<span data-ttu-id="06623-265">`MSBuild /t:restore`(která `nuget restore` a `dotnet restore` použít s projekty .NET Core), obnoví balíčky, kterou se odkazuje v souboru projektu následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="06623-265">`MSBuild /t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="06623-266">Číst všechny odkazy na projekt na projekt</span><span class="sxs-lookup"><span data-stu-id="06623-266">Read all project to project references</span></span>
1. <span data-ttu-id="06623-267">Přečtěte si vlastnosti projektu najít zprostředkující složku a cíl rozhraní</span><span class="sxs-lookup"><span data-stu-id="06623-267">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="06623-268">Předat msbuild data NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="06623-268">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="06623-269">Spustit obnovení</span><span class="sxs-lookup"><span data-stu-id="06623-269">Run restore</span></span>
1. <span data-ttu-id="06623-270">Stáhnout balíčky</span><span class="sxs-lookup"><span data-stu-id="06623-270">Download packages</span></span>
1. <span data-ttu-id="06623-271">Zápis soubor prostředků, cílů a props</span><span class="sxs-lookup"><span data-stu-id="06623-271">Write assets file, targets, and props</span></span>

### <a name="restore-properties"></a><span data-ttu-id="06623-272">Obnovit vlastnosti</span><span class="sxs-lookup"><span data-stu-id="06623-272">Restore properties</span></span>

<span data-ttu-id="06623-273">Nastavení další obnovení mohou pocházet z vlastnosti nástroje MSBuild v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="06623-273">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="06623-274">Hodnoty můžete také nastavit z příkazového řádku pomocí `/p:` přepínače (viz následující příklady).</span><span class="sxs-lookup"><span data-stu-id="06623-274">Values can also be set from the command line using the `/p:` switch (see Examples below).</span></span>

| <span data-ttu-id="06623-275">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="06623-275">Property</span></span> | <span data-ttu-id="06623-276">Popis</span><span class="sxs-lookup"><span data-stu-id="06623-276">Description</span></span> |
|--------|--------|
| <span data-ttu-id="06623-277">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="06623-277">RestoreSources</span></span> | <span data-ttu-id="06623-278">Seznam oddělený středníkem zdroji balíčků.</span><span class="sxs-lookup"><span data-stu-id="06623-278">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="06623-279">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="06623-279">RestorePackagesPath</span></span> | <span data-ttu-id="06623-280">Cesta ke složce balíčků uživatele.</span><span class="sxs-lookup"><span data-stu-id="06623-280">User packages folder path.</span></span> |
| <span data-ttu-id="06623-281">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="06623-281">RestoreDisableParallel</span></span> | <span data-ttu-id="06623-282">Limit stahování do jeden po druhém.</span><span class="sxs-lookup"><span data-stu-id="06623-282">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="06623-283">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="06623-283">RestoreConfigFile</span></span> | <span data-ttu-id="06623-284">Cesta k `Nuget.Config` lze uplatnit.</span><span class="sxs-lookup"><span data-stu-id="06623-284">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="06623-285">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="06623-285">RestoreNoCache</span></span> | <span data-ttu-id="06623-286">V případě hodnoty true nevyužívá webové mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="06623-286">If true, avoids using the web cache.</span></span> |
| <span data-ttu-id="06623-287">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="06623-287">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="06623-288">V případě hodnoty true ignoruje chybě nebo chybějící zdroje balíčků.</span><span class="sxs-lookup"><span data-stu-id="06623-288">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="06623-289">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="06623-289">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="06623-290">Cesta k `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="06623-290">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="06623-291">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="06623-291">RestoreGraphProjectInput</span></span> | <span data-ttu-id="06623-292">Seznam oddělený středníkem projekty k obnovení, který by měl obsahovat absolutní cesty.</span><span class="sxs-lookup"><span data-stu-id="06623-292">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="06623-293">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="06623-293">RestoreOutputPath</span></span> | <span data-ttu-id="06623-294">Výstupní složky, jako výchozí bude použit `obj` složky.</span><span class="sxs-lookup"><span data-stu-id="06623-294">Output folder, defaulting to the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="06623-295">Příklady</span><span class="sxs-lookup"><span data-stu-id="06623-295">Examples</span></span>

<span data-ttu-id="06623-296">Příkazový řádek:</span><span class="sxs-lookup"><span data-stu-id="06623-296">Command line:</span></span>

```cli
msbuild /t:restore /p:RestoreConfigFile=<path>
```

<span data-ttu-id="06623-297">Soubor projektu:</span><span class="sxs-lookup"><span data-stu-id="06623-297">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
<PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="06623-298">Obnovení výstupy</span><span class="sxs-lookup"><span data-stu-id="06623-298">Restore outputs</span></span>

<span data-ttu-id="06623-299">Obnovení vytvoří následující soubory v sestavení `obj` složky:</span><span class="sxs-lookup"><span data-stu-id="06623-299">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="06623-300">Soubor</span><span class="sxs-lookup"><span data-stu-id="06623-300">File</span></span> | <span data-ttu-id="06623-301">Popis</span><span class="sxs-lookup"><span data-stu-id="06623-301">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="06623-302">Dříve`project.lock.json`</span><span class="sxs-lookup"><span data-stu-id="06623-302">Previously `project.lock.json`</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="06623-303">Odkazy na MSBuild props součástí balíčků</span><span class="sxs-lookup"><span data-stu-id="06623-303">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="06623-304">Odkazy na cíle MSBuild součástí balíčků</span><span class="sxs-lookup"><span data-stu-id="06623-304">References to MSBuild targets contained in packages</span></span> |

### <a name="packagetargetfallback"></a><span data-ttu-id="06623-305">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="06623-305">PackageTargetFallback</span></span>

<span data-ttu-id="06623-306">`PackageTargetFallback` Element umožňuje určit sadu kompatibilní cíle, který se má použít při obnovování balíčků.</span><span class="sxs-lookup"><span data-stu-id="06623-306">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="06623-307">Je navržen tak, aby balíčky, které používají dotnet. [TxM](../schema/target-frameworks.md) k práci s kompatibilní balíčky, které nejsou deklarovat dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="06623-307">It's designed to allow packages that use a dotnet [TxM](../schema/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="06623-308">To znamená, pokud projektu používá dotnet TxM, pak všechny balíčky, které závisí na musí také mít dotnet TxM, pokud přidáte `<PackageTargetFallback>` do projektu, aby bylo možné povolit platformy bez dotnet. aby bylo kompatibilní s dotnet.</span><span class="sxs-lookup"><span data-stu-id="06623-308">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="06623-309">Například, pokud je projekt pomocí `netstandard1.6` TxM a závislý balíček obsahuje pouze `lib/net45/a.dll` a `lib/portable-net45+win81/a.dll`, pak projektu se nepovede.</span><span class="sxs-lookup"><span data-stu-id="06623-309">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="06623-310">Pokud chcete mají být předány se druhé knihovny DLL, pak můžete přidat `PackageTargetFallback` následujícím způsobem. Tím vyjádříte, který `portable-net45+win81` DLL je kompatibilní:</span><span class="sxs-lookup"><span data-stu-id="06623-310">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="06623-311">Deklarovat zálohu pro všechny cíle v projektu, nechte `Condition` atribut.</span><span class="sxs-lookup"><span data-stu-id="06623-311">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="06623-312">Můžete také rozšířit, všechny existující `PackageTargetFallback` zahrnutím `$(PackageTargetFallback)` jak je vidět tady:</span><span class="sxs-lookup"><span data-stu-id="06623-312">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="06623-313">Nahrazení jedna knihovna z obnovení grafu</span><span class="sxs-lookup"><span data-stu-id="06623-313">Replacing one library from a restore graph</span></span>

<span data-ttu-id="06623-314">Pokud obnovení je přináší nesprávný sestavení, je možné pro vyloučení, výchozí výběr balíčků a nahraďte ji metodou dle svého výběru.</span><span class="sxs-lookup"><span data-stu-id="06623-314">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="06623-315">První s nejvyšší úrovní `PackageReference`, vyloučit všechny prostředky:</span><span class="sxs-lookup"><span data-stu-id="06623-315">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
    <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="06623-316">V dalším kroku přidejte vlastní odkaz na příslušné místní kopie knihovny DLL:</span><span class="sxs-lookup"><span data-stu-id="06623-316">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
