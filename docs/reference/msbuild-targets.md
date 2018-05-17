---
title: NuGet pack a obnovení jako cíle nástroje MSBuild
description: NuGet pack a obnovení můžete pracovat přímo jako cíle MSBuild s NuGet 4.0 +.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 00d763bcfdd2f3db50378a1e7774eae7a2e1fcd1
ms.sourcegitcommit: 00c4c809c69c16fcf4d81012eb53ea22f0691d0b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="27651-103">NuGet pack a obnovení jako cíle nástroje MSBuild</span><span class="sxs-lookup"><span data-stu-id="27651-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="27651-104">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="27651-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="27651-105">Ve formátu PackageReference NuGet 4.0 + můžete ukládat všechny manifestu metadata přímo v souboru projektu místo pomocí samostatné `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="27651-105">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="27651-106">Pomocí nástroje MSBuild 15.1 + NuGet je také prvotřídní MSBuild občanem s `pack` a `restore` cílem, jak je popsáno níže.</span><span class="sxs-lookup"><span data-stu-id="27651-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="27651-107">Tyto cíle umožňují pracovat s NuGet, stejně jako s jinými úlohy nástroje MSBuild nebo cíl.</span><span class="sxs-lookup"><span data-stu-id="27651-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="27651-108">(Pro NuGet 3.x a starší, použijte [pack](../tools/cli-ref-pack.md) a [obnovení](../tools/cli-ref-restore.md) příkazy prostřednictvím rozhraní příkazového řádku NuGet místo.)</span><span class="sxs-lookup"><span data-stu-id="27651-108">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="27651-109">Pořadí sestavení cílů</span><span class="sxs-lookup"><span data-stu-id="27651-109">Target build order</span></span>

<span data-ttu-id="27651-110">Protože `pack` a `restore` jsou cíle MSBuild se dostanete k vylepšení vašeho pracovního postupu.</span><span class="sxs-lookup"><span data-stu-id="27651-110">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="27651-111">Řekněme například, že chcete zkopírovat vašeho balíčku do sdílené síťové složky po balení ho.</span><span class="sxs-lookup"><span data-stu-id="27651-111">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="27651-112">Můžete to udělat vložením následujícího textu v souboru projektu:</span><span class="sxs-lookup"><span data-stu-id="27651-112">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="27651-113">Podobně můžete napsat úlohy nástroje MSBuild, zápis vlastní cíl a využívat vlastnosti NuGet v úlohy nástroje MSBuild.</span><span class="sxs-lookup"><span data-stu-id="27651-113">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="27651-114">cíl Pack</span><span class="sxs-lookup"><span data-stu-id="27651-114">pack target</span></span>

<span data-ttu-id="27651-115">Pro rozhraní .NET standardní projekty formátu PackageReference, pomocí `msbuild /t:pack` nevykresluje vstupy ze souboru projektu použít při vytváření balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="27651-115">For .NET Standard projects using the PackageReference format, using `msbuild /t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="27651-116">Následující tabulka popisuje vlastnosti nástroje MSBuild, které mohou být přidány do souboru projektu v první `<PropertyGroup>` uzlu.</span><span class="sxs-lookup"><span data-stu-id="27651-116">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="27651-117">Můžete provést tyto úpravy snadno v Visual Studio 2017 a později kliknutím pravým tlačítkem na projekt a výběrem **upravit {název_projektu}** v místní nabídce.</span><span class="sxs-lookup"><span data-stu-id="27651-117">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="27651-118">Pro usnadnění práce v tabulce je seřazená podle vlastnost ekvivalentní v [ `.nuspec` soubor](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="27651-118">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="27651-119">Všimněte si, že `Owners` a `Summary` vlastnosti z `.nuspec` nejsou podporovány pomocí nástroje MSBuild.</span><span class="sxs-lookup"><span data-stu-id="27651-119">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="27651-120">Hodnota atributu/NuSpec</span><span class="sxs-lookup"><span data-stu-id="27651-120">Attribute/NuSpec Value</span></span> | <span data-ttu-id="27651-121">Vlastnosti nástroje MSBuild</span><span class="sxs-lookup"><span data-stu-id="27651-121">MSBuild Property</span></span> | <span data-ttu-id="27651-122">Výchozí</span><span class="sxs-lookup"><span data-stu-id="27651-122">Default</span></span> | <span data-ttu-id="27651-123">Poznámky</span><span class="sxs-lookup"><span data-stu-id="27651-123">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="27651-124">ID</span><span class="sxs-lookup"><span data-stu-id="27651-124">Id</span></span> | <span data-ttu-id="27651-125">ID balíčku</span><span class="sxs-lookup"><span data-stu-id="27651-125">PackageId</span></span> | <span data-ttu-id="27651-126">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="27651-126">AssemblyName</span></span> | <span data-ttu-id="27651-127">$(AssemblyName) z nástroje MSBuild</span><span class="sxs-lookup"><span data-stu-id="27651-127">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="27651-128">Version</span><span class="sxs-lookup"><span data-stu-id="27651-128">Version</span></span> | <span data-ttu-id="27651-129">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="27651-129">PackageVersion</span></span> | <span data-ttu-id="27651-130">Version</span><span class="sxs-lookup"><span data-stu-id="27651-130">Version</span></span> | <span data-ttu-id="27651-131">Toto je semver kompatibilní, například "1.0.0", "1.0.0-beta" nebo "1.0.0-beta-00345"</span><span class="sxs-lookup"><span data-stu-id="27651-131">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="27651-132">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="27651-132">VersionPrefix</span></span> | <span data-ttu-id="27651-133">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="27651-133">PackageVersionPrefix</span></span> | <span data-ttu-id="27651-134">empty</span><span class="sxs-lookup"><span data-stu-id="27651-134">empty</span></span> | <span data-ttu-id="27651-135">Nastavení PackageVersion přepíše PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="27651-135">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="27651-136">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="27651-136">VersionSuffix</span></span> | <span data-ttu-id="27651-137">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="27651-137">PackageVersionSuffix</span></span> | <span data-ttu-id="27651-138">empty</span><span class="sxs-lookup"><span data-stu-id="27651-138">empty</span></span> | <span data-ttu-id="27651-139">$(VersionSuffix) z nástroje MSBuild.</span><span class="sxs-lookup"><span data-stu-id="27651-139">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="27651-140">Nastavení PackageVersion přepíše PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="27651-140">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="27651-141">Autoři</span><span class="sxs-lookup"><span data-stu-id="27651-141">Authors</span></span> | <span data-ttu-id="27651-142">Autoři</span><span class="sxs-lookup"><span data-stu-id="27651-142">Authors</span></span> | <span data-ttu-id="27651-143">Uživatelské jméno aktuálního uživatele</span><span class="sxs-lookup"><span data-stu-id="27651-143">Username of the current user</span></span> | |
| <span data-ttu-id="27651-144">Vlastníci</span><span class="sxs-lookup"><span data-stu-id="27651-144">Owners</span></span> | <span data-ttu-id="27651-145">Není k dispozici</span><span class="sxs-lookup"><span data-stu-id="27651-145">N/A</span></span> | <span data-ttu-id="27651-146">Není k dispozici v NuSpec</span><span class="sxs-lookup"><span data-stu-id="27651-146">Not present in NuSpec</span></span> | |
| <span data-ttu-id="27651-147">Název</span><span class="sxs-lookup"><span data-stu-id="27651-147">Title</span></span> | <span data-ttu-id="27651-148">Název</span><span class="sxs-lookup"><span data-stu-id="27651-148">Title</span></span> | <span data-ttu-id="27651-149">ID balíčku</span><span class="sxs-lookup"><span data-stu-id="27651-149">The PackageId</span></span>| |
| <span data-ttu-id="27651-150">Popis</span><span class="sxs-lookup"><span data-stu-id="27651-150">Description</span></span> | <span data-ttu-id="27651-151">Popis</span><span class="sxs-lookup"><span data-stu-id="27651-151">Description</span></span> | <span data-ttu-id="27651-152">"Balíček popis"</span><span class="sxs-lookup"><span data-stu-id="27651-152">"Package Description"</span></span> | |
| <span data-ttu-id="27651-153">Copyright</span><span class="sxs-lookup"><span data-stu-id="27651-153">Copyright</span></span> | <span data-ttu-id="27651-154">Copyright</span><span class="sxs-lookup"><span data-stu-id="27651-154">Copyright</span></span> | <span data-ttu-id="27651-155">empty</span><span class="sxs-lookup"><span data-stu-id="27651-155">empty</span></span> | |
| <span data-ttu-id="27651-156">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="27651-156">RequireLicenseAcceptance</span></span> | <span data-ttu-id="27651-157">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="27651-157">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="27651-158">false</span><span class="sxs-lookup"><span data-stu-id="27651-158">false</span></span> | |
| <span data-ttu-id="27651-159">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="27651-159">LicenseUrl</span></span> | <span data-ttu-id="27651-160">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="27651-160">PackageLicenseUrl</span></span> | <span data-ttu-id="27651-161">empty</span><span class="sxs-lookup"><span data-stu-id="27651-161">empty</span></span> | |
| <span data-ttu-id="27651-162">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="27651-162">ProjectUrl</span></span> | <span data-ttu-id="27651-163">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="27651-163">PackageProjectUrl</span></span> | <span data-ttu-id="27651-164">empty</span><span class="sxs-lookup"><span data-stu-id="27651-164">empty</span></span> | |
| <span data-ttu-id="27651-165">IconUrl</span><span class="sxs-lookup"><span data-stu-id="27651-165">IconUrl</span></span> | <span data-ttu-id="27651-166">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="27651-166">PackageIconUrl</span></span> | <span data-ttu-id="27651-167">empty</span><span class="sxs-lookup"><span data-stu-id="27651-167">empty</span></span> | |
| <span data-ttu-id="27651-168">Značky</span><span class="sxs-lookup"><span data-stu-id="27651-168">Tags</span></span> | <span data-ttu-id="27651-169">PackageTags</span><span class="sxs-lookup"><span data-stu-id="27651-169">PackageTags</span></span> | <span data-ttu-id="27651-170">empty</span><span class="sxs-lookup"><span data-stu-id="27651-170">empty</span></span> | <span data-ttu-id="27651-171">Značky jsou oddělené středníky.</span><span class="sxs-lookup"><span data-stu-id="27651-171">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="27651-172">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="27651-172">ReleaseNotes</span></span> | <span data-ttu-id="27651-173">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="27651-173">PackageReleaseNotes</span></span> | <span data-ttu-id="27651-174">empty</span><span class="sxs-lookup"><span data-stu-id="27651-174">empty</span></span> | |
| <span data-ttu-id="27651-175">Úložiště nebo adresa Url</span><span class="sxs-lookup"><span data-stu-id="27651-175">Repository/Url</span></span> | <span data-ttu-id="27651-176">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="27651-176">RepositoryUrl</span></span> | <span data-ttu-id="27651-177">empty</span><span class="sxs-lookup"><span data-stu-id="27651-177">empty</span></span> | <span data-ttu-id="27651-178">Úložiště adresa URL používaná ke klonování nebo načíst zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="27651-178">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="27651-179">Příklad: *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="27651-179">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="27651-180">Úložiště/typu</span><span class="sxs-lookup"><span data-stu-id="27651-180">Repository/Type</span></span> | <span data-ttu-id="27651-181">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="27651-181">RepositoryType</span></span> | <span data-ttu-id="27651-182">empty</span><span class="sxs-lookup"><span data-stu-id="27651-182">empty</span></span> | <span data-ttu-id="27651-183">Typ úložiště.</span><span class="sxs-lookup"><span data-stu-id="27651-183">Repository type.</span></span> <span data-ttu-id="27651-184">Příklady: *git*, *tfs*.</span><span class="sxs-lookup"><span data-stu-id="27651-184">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="27651-185">Úložiště nebo větev</span><span class="sxs-lookup"><span data-stu-id="27651-185">Repository/Branch</span></span> | <span data-ttu-id="27651-186">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="27651-186">RepositoryBranch</span></span> | <span data-ttu-id="27651-187">empty</span><span class="sxs-lookup"><span data-stu-id="27651-187">empty</span></span> | <span data-ttu-id="27651-188">Informace o větve volitelné úložiště.</span><span class="sxs-lookup"><span data-stu-id="27651-188">Optional repository branch information.</span></span> <span data-ttu-id="27651-189">*RepositoryUrl* musí být zadaná také pro tuto vlastnost, která mají být zahrnuty.</span><span class="sxs-lookup"><span data-stu-id="27651-189">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="27651-190">Příklad: *hlavní* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="27651-190">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="27651-191">Úložiště a potvrdit</span><span class="sxs-lookup"><span data-stu-id="27651-191">Repository/Commit</span></span> | <span data-ttu-id="27651-192">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="27651-192">RepositoryCommit</span></span> | <span data-ttu-id="27651-193">empty</span><span class="sxs-lookup"><span data-stu-id="27651-193">empty</span></span> | <span data-ttu-id="27651-194">Potvrzení volitelné úložiště nebo sada changeset k označení, které zdroje balíčku byl sestaven s.</span><span class="sxs-lookup"><span data-stu-id="27651-194">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="27651-195">*RepositoryUrl* musí být zadaná také pro tuto vlastnost, která mají být zahrnuty.</span><span class="sxs-lookup"><span data-stu-id="27651-195">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="27651-196">Příklad: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="27651-196">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="27651-197">PackageType</span><span class="sxs-lookup"><span data-stu-id="27651-197">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="27651-198">Souhrn</span><span class="sxs-lookup"><span data-stu-id="27651-198">Summary</span></span> | <span data-ttu-id="27651-199">Nepodporováno</span><span class="sxs-lookup"><span data-stu-id="27651-199">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="27651-200">vstupy cíl Pack</span><span class="sxs-lookup"><span data-stu-id="27651-200">pack target inputs</span></span>

- <span data-ttu-id="27651-201">IsPackable</span><span class="sxs-lookup"><span data-stu-id="27651-201">IsPackable</span></span>
- <span data-ttu-id="27651-202">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="27651-202">PackageVersion</span></span>
- <span data-ttu-id="27651-203">ID balíčku</span><span class="sxs-lookup"><span data-stu-id="27651-203">PackageId</span></span>
- <span data-ttu-id="27651-204">Autoři</span><span class="sxs-lookup"><span data-stu-id="27651-204">Authors</span></span>
- <span data-ttu-id="27651-205">Popis</span><span class="sxs-lookup"><span data-stu-id="27651-205">Description</span></span>
- <span data-ttu-id="27651-206">Copyright</span><span class="sxs-lookup"><span data-stu-id="27651-206">Copyright</span></span>
- <span data-ttu-id="27651-207">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="27651-207">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="27651-208">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="27651-208">DevelopmentDependency</span></span>
- <span data-ttu-id="27651-209">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="27651-209">PackageLicenseUrl</span></span>
- <span data-ttu-id="27651-210">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="27651-210">PackageProjectUrl</span></span>
- <span data-ttu-id="27651-211">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="27651-211">PackageIconUrl</span></span>
- <span data-ttu-id="27651-212">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="27651-212">PackageReleaseNotes</span></span>
- <span data-ttu-id="27651-213">PackageTags</span><span class="sxs-lookup"><span data-stu-id="27651-213">PackageTags</span></span>
- <span data-ttu-id="27651-214">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="27651-214">PackageOutputPath</span></span>
- <span data-ttu-id="27651-215">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="27651-215">IncludeSymbols</span></span>
- <span data-ttu-id="27651-216">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="27651-216">IncludeSource</span></span>
- <span data-ttu-id="27651-217">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="27651-217">PackageTypes</span></span>
- <span data-ttu-id="27651-218">IsTool</span><span class="sxs-lookup"><span data-stu-id="27651-218">IsTool</span></span>
- <span data-ttu-id="27651-219">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="27651-219">RepositoryUrl</span></span>
- <span data-ttu-id="27651-220">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="27651-220">RepositoryType</span></span>
- <span data-ttu-id="27651-221">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="27651-221">RepositoryBranch</span></span>
- <span data-ttu-id="27651-222">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="27651-222">RepositoryCommit</span></span>
- <span data-ttu-id="27651-223">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="27651-223">NoPackageAnalysis</span></span>
- <span data-ttu-id="27651-224">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="27651-224">MinClientVersion</span></span>
- <span data-ttu-id="27651-225">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="27651-225">IncludeBuildOutput</span></span>
- <span data-ttu-id="27651-226">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="27651-226">IncludeContentInPack</span></span>
- <span data-ttu-id="27651-227">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="27651-227">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="27651-228">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="27651-228">ContentTargetFolders</span></span>
- <span data-ttu-id="27651-229">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="27651-229">NuspecFile</span></span>
- <span data-ttu-id="27651-230">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="27651-230">NuspecBasePath</span></span>
- <span data-ttu-id="27651-231">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="27651-231">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="27651-232">scénáře aktualizací Service Pack</span><span class="sxs-lookup"><span data-stu-id="27651-232">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="27651-233">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="27651-233">PackageIconUrl</span></span>

<span data-ttu-id="27651-234">Jako součást změny pro [NuGet problém 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` bude nakonec změnit tak, aby `PackageIconUri` a může být relativní cesta k ikonu souboru, který bude zahrnut v kořenovém adresáři výsledné balíčku.</span><span class="sxs-lookup"><span data-stu-id="27651-234">As part of the change for [NuGet Issue 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="27651-235">Výstup sestavení</span><span class="sxs-lookup"><span data-stu-id="27651-235">Output assemblies</span></span>

<span data-ttu-id="27651-236">`nuget pack` kopie výstupní soubory s příponami `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, a `.pri`.</span><span class="sxs-lookup"><span data-stu-id="27651-236">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="27651-237">Výstupní soubory, které jste zkopírovali závisí na MSBuild poskytuje z `BuiltOutputProjectGroup` cíl.</span><span class="sxs-lookup"><span data-stu-id="27651-237">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="27651-238">Existují dvě vlastnosti nástroje MSBuild, které můžete použít v souboru projektu nebo příkazového řádku na ovládací prvek kde přejděte výstup sestavení:</span><span class="sxs-lookup"><span data-stu-id="27651-238">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="27651-239">`IncludeBuildOutput`: Logická hodnota, která určuje, zda by měl být sestavení výstupu sestavení součástí balíčku.</span><span class="sxs-lookup"><span data-stu-id="27651-239">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="27651-240">`BuildOutputTargetFolder`: Určuje složku, ve kterém má být umístěn výstup sestavení.</span><span class="sxs-lookup"><span data-stu-id="27651-240">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="27651-241">Výstup sestavení (a ostatní výstupní soubory) se zkopírují do jejich odpovídajících framework složky.</span><span class="sxs-lookup"><span data-stu-id="27651-241">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="27651-242">Odkazy na balíček</span><span class="sxs-lookup"><span data-stu-id="27651-242">Package references</span></span>

<span data-ttu-id="27651-243">V tématu [balíček odkazy v souborech projektu](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="27651-243">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="27651-244">Projekt odkazů projektu</span><span class="sxs-lookup"><span data-stu-id="27651-244">Project to project references</span></span>

<span data-ttu-id="27651-245">Projekt odkazů projektu jsou považovány za ve výchozím nastavení jako odkazy na balíček nuget, například:</span><span class="sxs-lookup"><span data-stu-id="27651-245">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="27651-246">Pro odkaz na projekt můžete také přidat následující metadata:</span><span class="sxs-lookup"><span data-stu-id="27651-246">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="27651-247">Včetně obsahu v balíčku</span><span class="sxs-lookup"><span data-stu-id="27651-247">Including content in a package</span></span>

<span data-ttu-id="27651-248">Chcete-li zahrnout obsah, přidejte doplňující metadata do existující `<Content>` položky.</span><span class="sxs-lookup"><span data-stu-id="27651-248">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="27651-249">Ve výchozím nastavení všechno typ, který "Obsah" získá v balíčku zahrnutý Pokud přepíšete s položkami jako následující:</span><span class="sxs-lookup"><span data-stu-id="27651-249">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="27651-250">Ve výchozím nastavení, vše, co přidá do kořenového adresáře `content` a `contentFiles\any\<target_framework>` složky v balíčku a uchovává složce relativní struktury, pokud zadáte cestu k balíčku:</span><span class="sxs-lookup"><span data-stu-id="27651-250">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="27651-251">Pokud chcete kopírovat veškerý obsah pouze na konkrétní kořenových složek bylo (místo `content` a `contentFiles` oba), můžete použít vlastnost MSBuild `ContentTargetFolders`, což výchozí nastavení "obsah; contentFiles", ale může být nastavena na žádné jiné názvy složek.</span><span class="sxs-lookup"><span data-stu-id="27651-251">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="27651-252">Všimněte si, aby pouze určení "contentFiles" v `ContentTargetFolders` převádí soubory v `contentFiles\any\<target_framework>` nebo `contentFiles\<language>\<target_framework>` na základě `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="27651-252">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="27651-253">`PackagePath` může být sadu cílových cest oddělený středníkem.</span><span class="sxs-lookup"><span data-stu-id="27651-253">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="27651-254">Zadání cesty prázdný balíček by soubor přidat do kořenového adresáře balíčku.</span><span class="sxs-lookup"><span data-stu-id="27651-254">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="27651-255">Například následující přidá `libuv.txt` k `content\myfiles`, `content\samples`a kořenového adresáře balíčku:</span><span class="sxs-lookup"><span data-stu-id="27651-255">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="27651-256">Je také ve vlastnosti nástroje MSBuild `$(IncludeContentInPack)`, což výchozí nastavení `true`.</span><span class="sxs-lookup"><span data-stu-id="27651-256">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="27651-257">Pokud je nastavena v `false` na jakýkoli projekt, pak obsah z daného projektu nejsou součástí balíček nuget.</span><span class="sxs-lookup"><span data-stu-id="27651-257">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="27651-258">Zahrnuje další konkrétní metadata aktualizací Service pack, kterou můžete nastavit na některou z výše uvedených položek ```<PackageCopyToOutput>``` a ```<PackageFlatten>``` které nastaví ```CopyToOutput``` a ```Flatten``` hodnoty na ```contentFiles``` položku v výstupní soubor nuspec.</span><span class="sxs-lookup"><span data-stu-id="27651-258">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="27651-259">Vedle položky obsahu `<Pack>` a `<PackagePath>` metadata můžete také nastavit na soubory pomocí akce sestavení kompilace, EmbeddedResource, ApplicationDefinition, stránky, prostředků, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes , CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource nebo hodnotu None.</span><span class="sxs-lookup"><span data-stu-id="27651-259">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="27651-260">Pro pack připojit název souboru pro cestu k balíčku, při použití vzory expanze názvů cestu k balíčku musí končit složky oddělovací znak, jinak hodnota cestou balíčku je považován za úplnou cestu včetně názvu souboru.</span><span class="sxs-lookup"><span data-stu-id="27651-260">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="27651-261">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="27651-261">IncludeSymbols</span></span>

<span data-ttu-id="27651-262">Při použití `MSBuild /t:pack /p:IncludeSymbols=true`, odpovídající `.pdb` spolu s další výstupní soubory kopírují soubory (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="27651-262">When using `MSBuild /t:pack /p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="27651-263">Všimněte si, že nastavení `IncludeSymbols=true` vytvoří regulární balíček *a* balíčku symbolů.</span><span class="sxs-lookup"><span data-stu-id="27651-263">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="27651-264">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="27651-264">IncludeSource</span></span>

<span data-ttu-id="27651-265">Je to stejné nastavení jako `IncludeSymbols`kromě toho, že ho zkopíruje zdrojové soubory spolu s `.pdb` i soubory.</span><span class="sxs-lookup"><span data-stu-id="27651-265">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="27651-266">Všechny soubory typu `Compile` se překopírují na `src\<ProjectName>\` zachování struktura složek relativní cestu v výsledné balíčku.</span><span class="sxs-lookup"><span data-stu-id="27651-266">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="27651-267">Stejné také se stane pro zdrojové soubory libovolného `ProjectReference` jehož `TreatAsPackageReference` nastavena na `false`.</span><span class="sxs-lookup"><span data-stu-id="27651-267">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="27651-268">Pokud soubor typu kompilovat, je mimo složku projekt, pak je právě přidali do `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="27651-268">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="istool"></a><span data-ttu-id="27651-269">IsTool</span><span class="sxs-lookup"><span data-stu-id="27651-269">IsTool</span></span>

<span data-ttu-id="27651-270">Při použití `MSBuild /t:pack /p:IsTool=true`, všechny výstupní soubory, jak je uvedeno v [výstup sestavení](#output-assemblies) scénáři se zkopírují do `tools` složky místo `lib` složky.</span><span class="sxs-lookup"><span data-stu-id="27651-270">When using `MSBuild /t:pack /p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="27651-271">Všimněte si, že se to neliší od `DotNetCliTool` , která je určena podle nastavení `PackageType` v `.csproj` souboru.</span><span class="sxs-lookup"><span data-stu-id="27651-271">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="27651-272">Balení pomocí příponou .nuspec</span><span class="sxs-lookup"><span data-stu-id="27651-272">Packing using a .nuspec</span></span>

<span data-ttu-id="27651-273">Můžete použít `.nuspec` soubor pack projektu za předpokladu, že soubor projektu sady SDK k importu `NuGet.Build.Tasks.Pack.targets` tak, aby úloha sady mohou být provedeny.</span><span class="sxs-lookup"><span data-stu-id="27651-273">You can use a `.nuspec` file to pack your project provided that you have a SDK project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="27651-274">Potřebujete stále obnovení projektu, než můžete pack soubor nuspec.</span><span class="sxs-lookup"><span data-stu-id="27651-274">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="27651-275">Cílový framework projektu soubor je důležité a nepoužívá se při balení nuspec.</span><span class="sxs-lookup"><span data-stu-id="27651-275">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="27651-276">Následující tři vlastnosti nástroje MSBuild jsou relevantní pro balení, použití `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="27651-276">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="27651-277">`NuspecFile`: relativní nebo absolutní cesta k `.nuspec` soubor používá pro okolních.</span><span class="sxs-lookup"><span data-stu-id="27651-277">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="27651-278">`NuspecProperties`: středníky oddělený seznam klíč = hodnota páry.</span><span class="sxs-lookup"><span data-stu-id="27651-278">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="27651-279">Vzhledem ke způsobu MSBuild příkazového řádku analýzy funguje více vlastností se musí zadat následujícím způsobem: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="27651-279">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="27651-280">`NuspecBasePath`: Základní cesta pro `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="27651-280">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="27651-281">Pokud používáte `dotnet.exe` pack projektu, použijte příkaz takto:</span><span class="sxs-lookup"><span data-stu-id="27651-281">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="27651-282">Pokud pomocí nástroje MSBuild pack projektu, použijte příkaz takto:</span><span class="sxs-lookup"><span data-stu-id="27651-282">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="27651-283">Upozorňujeme, že balení nuspec pomocí dotnet.exe nebo msbuild také vede k vytváření projektu ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="27651-283">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="27651-284">Tím se vyhnout předáním ```--no-build``` vlastnost dotnet.exe, která je ekvivalentní nastavení ```<NoBuild>true</NoBuild> ``` v souboru projektu se nastavení ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` v souboru projektu</span><span class="sxs-lookup"><span data-stu-id="27651-284">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file</span></span>

<span data-ttu-id="27651-285">Je například csproj soubor pro soubor nuspec pack:</span><span class="sxs-lookup"><span data-stu-id="27651-285">An example of a csproj file to pack a nuspec file is:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <NoBuild>true</NoBuild>
    <IncludeBuildOutput>false</IncludeBuildOutput>
    <NuspecFile>PATH_TO_NUSPEC_FILE</NuspecFile>
    <NuspecProperties>add nuspec properties here</NuspecProperties>
    <NuspecBasePath>optional to provide</NuspecBasePath>
  </PropertyGroup>
</Project>
```

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="27651-286">Rozšířené body rozšíření pro vytvoření přizpůsobené balíčku</span><span class="sxs-lookup"><span data-stu-id="27651-286">Advanced extension points to create customized package</span></span>

<span data-ttu-id="27651-287">`pack` Cíl poskytuje dva body rozšíření, které běží v informacích o vnitřní, cílový framework konkrétní sestavení.</span><span class="sxs-lookup"><span data-stu-id="27651-287">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="27651-288">Body rozšíření podpory včetně cílový framework konkrétní obsah a sestavení do balíčku:</span><span class="sxs-lookup"><span data-stu-id="27651-288">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="27651-289">`TargetsForTfmSpecificBuildOutput` Cíl: použití pro soubory `lib` nebo složky, zadán pomocí `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="27651-289">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="27651-290">`TargetsForTfmSpecificContentInPackage` Cíl: použití pro soubory mimo `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="27651-290">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="27651-291">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="27651-291">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="27651-292">Napsat vlastní cíl a zadejte jako hodnotu `$(TargetsForTfmSpecificBuildOutput)` vlastnost.</span><span class="sxs-lookup"><span data-stu-id="27651-292">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="27651-293">Pro všechny soubory, které muset přejít do `BuildOutputTargetFolder` (lib ve výchozím nastavení), cíl by měl zápisu těchto souborů do ItemGroup `BuildOutputInPackage` a nastavte tyto dvě hodnoty metadat:</span><span class="sxs-lookup"><span data-stu-id="27651-293">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="27651-294">`FinalOutputPath`: Absolutní cestu k souboru; Pokud není zadaná, identita se používá k vyhodnocení cestu ke zdroji.</span><span class="sxs-lookup"><span data-stu-id="27651-294">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="27651-295">`TargetPath`: (Volitelné) nastavená, pokud je třeba soubor přejděte do podsložky v rámci `lib\<TargetFramework>` , například satelitní sestavení tohoto přejděte v části jejich složky příslušné jazykové verze.</span><span class="sxs-lookup"><span data-stu-id="27651-295">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="27651-296">Výchozí hodnota je název souboru.</span><span class="sxs-lookup"><span data-stu-id="27651-296">Defaults to the name of the file.</span></span>

<span data-ttu-id="27651-297">Příklad:</span><span class="sxs-lookup"><span data-stu-id="27651-297">Example:</span></span>

```xml
<PropertyGroup>
  <TargetsForTfmSpecificBuildOutput>$(TargetsForTfmSpecificBuildOutput);GetMyPackageFiles</TargetsForTfmSpecificBuildOutput>
</PropertyGroup>

<Target Name="GetMyPackageFiles">
  <ItemGroup>
    <BuildOutputInPackage Include="$(OutputPath)cs\$(AssemblyName).resources.dll">
        <TargetPath>cs</TargetPath>
    </BuildOutputInPackage>
  </ItemGroup>
</Target>
```

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="27651-298">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="27651-298">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="27651-299">Napsat vlastní cíl a zadejte jako hodnotu `$(TargetsForTfmSpecificContentInPackage)` vlastnost.</span><span class="sxs-lookup"><span data-stu-id="27651-299">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="27651-300">Pro všechny soubory, které chcete zahrnout do balíčku, cíl zápisu těchto souborů do ItemGroup `TfmSpecificPackageFile` a nastavte následující volitelné metadata:</span><span class="sxs-lookup"><span data-stu-id="27651-300">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="27651-301">`PackagePath`: Cesta kde souboru by se měly zobrazovat v balíčku.</span><span class="sxs-lookup"><span data-stu-id="27651-301">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="27651-302">NuGet vydá upozornění, pokud je více než jeden soubor přidaný do stejné cesty k balíčku.</span><span class="sxs-lookup"><span data-stu-id="27651-302">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="27651-303">`BuildAction`: Akce sestavení přiřadit k souboru, povinné, pokud cesta balíčku je v `contentFiles` složky.</span><span class="sxs-lookup"><span data-stu-id="27651-303">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="27651-304">Výchozí hodnota je "Žádný".</span><span class="sxs-lookup"><span data-stu-id="27651-304">Defaults to "None".</span></span>

<span data-ttu-id="27651-305">Příklad:</span><span class="sxs-lookup"><span data-stu-id="27651-305">An example:</span></span>
```xml
<PropertyGroup>
  <TargetsForTfmSpecificContentInPackage>$(TargetsForTfmSpecificContentInPackage);CustomContentTarget</TargetsForTfmSpecificContentInPackage>
</PropertyGroup>

<Target Name=""CustomContentTarget"">
  <ItemGroup>
    <TfmSpecificPackageFile Include=""abc.txt"">
      <PackagePath>mycontent/$(TargetFramework)</PackagePath>
    </TfmSpecificPackageFile>
    <TfmSpecificPackageFile Include=""Extensions/ext.txt"" Condition=""'$(TargetFramework)' == 'net46'"">
      <PackagePath>net46content</PackagePath>
    </TfmSpecificPackageFile>  
  </ItemGroup>
</Target>  
```

## <a name="restore-target"></a><span data-ttu-id="27651-306">Cíl obnovení</span><span class="sxs-lookup"><span data-stu-id="27651-306">restore target</span></span>

<span data-ttu-id="27651-307">`MSBuild /t:restore` (která `nuget restore` a `dotnet restore` použít s projekty .NET Core), obnoví balíčky, kterou se odkazuje v souboru projektu následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="27651-307">`MSBuild /t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="27651-308">Číst všechny odkazy na projekt na projekt</span><span class="sxs-lookup"><span data-stu-id="27651-308">Read all project to project references</span></span>
1. <span data-ttu-id="27651-309">Přečtěte si vlastnosti projektu najít zprostředkující složku a cíl rozhraní</span><span class="sxs-lookup"><span data-stu-id="27651-309">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="27651-310">Předat msbuild data NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="27651-310">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="27651-311">Spustit obnovení</span><span class="sxs-lookup"><span data-stu-id="27651-311">Run restore</span></span>
1. <span data-ttu-id="27651-312">Stáhnout balíčky</span><span class="sxs-lookup"><span data-stu-id="27651-312">Download packages</span></span>
1. <span data-ttu-id="27651-313">Zápis soubor prostředků, cílů a props</span><span class="sxs-lookup"><span data-stu-id="27651-313">Write assets file, targets, and props</span></span>

<span data-ttu-id="27651-314">`restore` Cíle funguje **pouze** pro projekty PackageReference formátu.</span><span class="sxs-lookup"><span data-stu-id="27651-314">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="27651-315">Provede **není** pracovní pro projekty pomocí `packages.config` formát; použít [obnovení nuget](../tools/cli-ref-restore.md) místo.</span><span class="sxs-lookup"><span data-stu-id="27651-315">It does **not** work for projects using the `packages.config` format; use [nuget restore](../tools/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="27651-316">Obnovit vlastnosti</span><span class="sxs-lookup"><span data-stu-id="27651-316">Restore properties</span></span>

<span data-ttu-id="27651-317">Nastavení další obnovení mohou pocházet z vlastnosti nástroje MSBuild v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="27651-317">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="27651-318">Hodnoty můžete také nastavit z příkazového řádku pomocí `/p:` přepínače (viz následující příklady).</span><span class="sxs-lookup"><span data-stu-id="27651-318">Values can also be set from the command line using the `/p:` switch (see Examples below).</span></span>

| <span data-ttu-id="27651-319">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="27651-319">Property</span></span> | <span data-ttu-id="27651-320">Popis</span><span class="sxs-lookup"><span data-stu-id="27651-320">Description</span></span> |
|--------|--------|
| <span data-ttu-id="27651-321">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="27651-321">RestoreSources</span></span> | <span data-ttu-id="27651-322">Seznam oddělený středníkem zdroji balíčků.</span><span class="sxs-lookup"><span data-stu-id="27651-322">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="27651-323">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="27651-323">RestorePackagesPath</span></span> | <span data-ttu-id="27651-324">Cesta ke složce balíčků uživatele.</span><span class="sxs-lookup"><span data-stu-id="27651-324">User packages folder path.</span></span> |
| <span data-ttu-id="27651-325">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="27651-325">RestoreDisableParallel</span></span> | <span data-ttu-id="27651-326">Limit stahování do jeden po druhém.</span><span class="sxs-lookup"><span data-stu-id="27651-326">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="27651-327">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="27651-327">RestoreConfigFile</span></span> | <span data-ttu-id="27651-328">Cesta k `Nuget.Config` lze uplatnit.</span><span class="sxs-lookup"><span data-stu-id="27651-328">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="27651-329">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="27651-329">RestoreNoCache</span></span> | <span data-ttu-id="27651-330">V případě hodnoty true nevyužívá balíčky v mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="27651-330">If true, avoids using cached packages.</span></span> <span data-ttu-id="27651-331">V tématu [správy globální balíčky a složky mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="27651-331">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="27651-332">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="27651-332">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="27651-333">V případě hodnoty true ignoruje chybě nebo chybějící zdroje balíčků.</span><span class="sxs-lookup"><span data-stu-id="27651-333">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="27651-334">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="27651-334">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="27651-335">Cesta k `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="27651-335">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="27651-336">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="27651-336">RestoreGraphProjectInput</span></span> | <span data-ttu-id="27651-337">Seznam oddělený středníkem projekty k obnovení, který by měl obsahovat absolutní cesty.</span><span class="sxs-lookup"><span data-stu-id="27651-337">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="27651-338">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="27651-338">RestoreOutputPath</span></span> | <span data-ttu-id="27651-339">Výstupní složky, jako výchozí bude použit `obj` složky.</span><span class="sxs-lookup"><span data-stu-id="27651-339">Output folder, defaulting to the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="27651-340">Příklady</span><span class="sxs-lookup"><span data-stu-id="27651-340">Examples</span></span>

<span data-ttu-id="27651-341">Příkazový řádek:</span><span class="sxs-lookup"><span data-stu-id="27651-341">Command line:</span></span>

```cli
msbuild /t:restore /p:RestoreConfigFile=<path>
```

<span data-ttu-id="27651-342">Soubor projektu:</span><span class="sxs-lookup"><span data-stu-id="27651-342">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="27651-343">Obnovení výstupy</span><span class="sxs-lookup"><span data-stu-id="27651-343">Restore outputs</span></span>

<span data-ttu-id="27651-344">Obnovení vytvoří následující soubory v sestavení `obj` složky:</span><span class="sxs-lookup"><span data-stu-id="27651-344">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="27651-345">Soubor</span><span class="sxs-lookup"><span data-stu-id="27651-345">File</span></span> | <span data-ttu-id="27651-346">Popis</span><span class="sxs-lookup"><span data-stu-id="27651-346">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="27651-347">Obsahuje graf závislostí všechny odkazy balíčku.</span><span class="sxs-lookup"><span data-stu-id="27651-347">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="27651-348">Odkazy na MSBuild props součástí balíčků</span><span class="sxs-lookup"><span data-stu-id="27651-348">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="27651-349">Odkazy na cíle MSBuild součástí balíčků</span><span class="sxs-lookup"><span data-stu-id="27651-349">References to MSBuild targets contained in packages</span></span> |

### <a name="packagetargetfallback"></a><span data-ttu-id="27651-350">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="27651-350">PackageTargetFallback</span></span>

<span data-ttu-id="27651-351">`PackageTargetFallback` Element umožňuje určit sadu kompatibilní cíle, který se má použít při obnovování balíčků.</span><span class="sxs-lookup"><span data-stu-id="27651-351">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="27651-352">Je navržen tak, aby balíčky, které používají dotnet. [TxM](../reference/target-frameworks.md) k práci s kompatibilní balíčky, které nejsou deklarovat dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="27651-352">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="27651-353">To znamená, pokud projektu používá dotnet TxM, pak všechny balíčky, které závisí na musí také mít dotnet TxM, pokud přidáte `<PackageTargetFallback>` do projektu, aby bylo možné povolit platformy bez dotnet. aby bylo kompatibilní s dotnet.</span><span class="sxs-lookup"><span data-stu-id="27651-353">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="27651-354">Například, pokud je projekt pomocí `netstandard1.6` TxM a závislý balíček obsahuje pouze `lib/net45/a.dll` a `lib/portable-net45+win81/a.dll`, pak projektu se nepovede.</span><span class="sxs-lookup"><span data-stu-id="27651-354">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="27651-355">Pokud chcete mají být předány se druhé knihovny DLL, pak můžete přidat `PackageTargetFallback` následujícím způsobem. Tím vyjádříte, který `portable-net45+win81` DLL je kompatibilní:</span><span class="sxs-lookup"><span data-stu-id="27651-355">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="27651-356">Deklarovat zálohu pro všechny cíle v projektu, nechte `Condition` atribut.</span><span class="sxs-lookup"><span data-stu-id="27651-356">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="27651-357">Můžete také rozšířit, všechny existující `PackageTargetFallback` zahrnutím `$(PackageTargetFallback)` jak je vidět tady:</span><span class="sxs-lookup"><span data-stu-id="27651-357">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="27651-358">Nahrazení jedna knihovna z obnovení grafu</span><span class="sxs-lookup"><span data-stu-id="27651-358">Replacing one library from a restore graph</span></span>

<span data-ttu-id="27651-359">Pokud obnovení je přináší nesprávný sestavení, je možné pro vyloučení, výchozí výběr balíčků a nahraďte ji metodou dle svého výběru.</span><span class="sxs-lookup"><span data-stu-id="27651-359">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="27651-360">První s nejvyšší úrovní `PackageReference`, vyloučit všechny prostředky:</span><span class="sxs-lookup"><span data-stu-id="27651-360">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="27651-361">V dalším kroku přidejte vlastní odkaz na příslušné místní kopie knihovny DLL:</span><span class="sxs-lookup"><span data-stu-id="27651-361">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
