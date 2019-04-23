---
title: Balíček NuGet a obnovení jako cílů MSBuild
description: Balíček NuGet a obnovení můžete pracovat přímo jako cílů MSBuild s NuGet 4.0 +.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 1e89aeb46f2538d46c013561a51a41702b2472d8
ms.sourcegitcommit: 6b71926f062ecddb8729ef8567baf67fd269642a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/22/2019
ms.locfileid: "59932096"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="00982-103">Balíček NuGet a obnovení jako cílů MSBuild</span><span class="sxs-lookup"><span data-stu-id="00982-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="00982-104">*NuGet 4.0 +*</span><span class="sxs-lookup"><span data-stu-id="00982-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="00982-105">S formátem PackageReference NuGet 4.0 + můžete ukládat všechny manifestu metadata přímo v rámci souboru projektu namísto spouštění samostatné `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="00982-105">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="00982-106">Pomocí nástroje MSBuild 15.1 +, Správce balíčků NuGet je také prvotřídní občany MSBuild s `pack` a `restore` cílí, jak je popsáno níže.</span><span class="sxs-lookup"><span data-stu-id="00982-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="00982-107">Tyto cíle umožňují pracovat s NuGet, stejně jako u jakékoli úlohy nástroje MSBuild nebo cíl.</span><span class="sxs-lookup"><span data-stu-id="00982-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="00982-108">(Pro NuGet 3.x a dříve, použít [pack](../tools/cli-ref-pack.md) a [obnovení](../tools/cli-ref-restore.md) příkazy přes rozhraní příkazového řádku NuGet místo.)</span><span class="sxs-lookup"><span data-stu-id="00982-108">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="00982-109">Pořadí sestavení cílů</span><span class="sxs-lookup"><span data-stu-id="00982-109">Target build order</span></span>

<span data-ttu-id="00982-110">Protože `pack` a `restore` jsou cíle nástroje MSBuild, dostanete je k vylepšení pracovního postupu.</span><span class="sxs-lookup"><span data-stu-id="00982-110">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="00982-111">Řekněme například, že chcete zkopírovat balíček do sdílené síťové složky po zabalení ho.</span><span class="sxs-lookup"><span data-stu-id="00982-111">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="00982-112">Můžete to udělat přidáním následujícího kódu v souboru projektu:</span><span class="sxs-lookup"><span data-stu-id="00982-112">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="00982-113">Podobně můžete napsat úlohu nástroje MSBuild, psát vlastní cílové a využívat NuGet vlastnosti v úkolu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="00982-113">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="00982-114">cíl balíčku</span><span class="sxs-lookup"><span data-stu-id="00982-114">pack target</span></span>

<span data-ttu-id="00982-115">Pro projekty .NET Standard ve formátu PackageReference, pomocí `msbuild -t:pack` nakreslí vstupů ze souboru projektu k použití při vytváření balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="00982-115">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="00982-116">Následující tabulka popisuje vlastnosti nástroje MSBuild, které mohou být přidány do souboru projektu v rámci první `<PropertyGroup>` uzlu.</span><span class="sxs-lookup"><span data-stu-id="00982-116">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="00982-117">Můžete provádět tyto úpravy snadno v sadě Visual Studio 2017 a novější kliknutím pravým tlačítkem myši projekt a výběrem **upravit {project_name}** v místní nabídce.</span><span class="sxs-lookup"><span data-stu-id="00982-117">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="00982-118">Pro usnadnění práce je uspořádaný v tabulce rovnocenné vlastností v [ `.nuspec` souboru](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="00982-118">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="00982-119">Všimněte si, že `Owners` a `Summary` vlastnosti z `.nuspec` nejsou podporovány nástrojem MSBuild.</span><span class="sxs-lookup"><span data-stu-id="00982-119">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="00982-120">Hodnota atributu/NuSpec</span><span class="sxs-lookup"><span data-stu-id="00982-120">Attribute/NuSpec Value</span></span> | <span data-ttu-id="00982-121">MSBuild Property</span><span class="sxs-lookup"><span data-stu-id="00982-121">MSBuild Property</span></span> | <span data-ttu-id="00982-122">Výchozí</span><span class="sxs-lookup"><span data-stu-id="00982-122">Default</span></span> | <span data-ttu-id="00982-123">Poznámky</span><span class="sxs-lookup"><span data-stu-id="00982-123">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="00982-124">ID</span><span class="sxs-lookup"><span data-stu-id="00982-124">Id</span></span> | <span data-ttu-id="00982-125">PackageId</span><span class="sxs-lookup"><span data-stu-id="00982-125">PackageId</span></span> | <span data-ttu-id="00982-126">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="00982-126">AssemblyName</span></span> | <span data-ttu-id="00982-127">$(AssemblyName) MSBuild</span><span class="sxs-lookup"><span data-stu-id="00982-127">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="00982-128">Version</span><span class="sxs-lookup"><span data-stu-id="00982-128">Version</span></span> | <span data-ttu-id="00982-129">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="00982-129">PackageVersion</span></span> | <span data-ttu-id="00982-130">Version</span><span class="sxs-lookup"><span data-stu-id="00982-130">Version</span></span> | <span data-ttu-id="00982-131">Toto je semver kompatibilní, například "1.0.0", "1.0.0-beta" nebo "1.0.0-beta-00345"</span><span class="sxs-lookup"><span data-stu-id="00982-131">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="00982-132">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="00982-132">VersionPrefix</span></span> | <span data-ttu-id="00982-133">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="00982-133">PackageVersionPrefix</span></span> | <span data-ttu-id="00982-134">empty</span><span class="sxs-lookup"><span data-stu-id="00982-134">empty</span></span> | <span data-ttu-id="00982-135">Nastavení PackageVersion přepíše PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="00982-135">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="00982-136">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="00982-136">VersionSuffix</span></span> | <span data-ttu-id="00982-137">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="00982-137">PackageVersionSuffix</span></span> | <span data-ttu-id="00982-138">empty</span><span class="sxs-lookup"><span data-stu-id="00982-138">empty</span></span> | <span data-ttu-id="00982-139">$(VersionSuffix) from MSBuild.</span><span class="sxs-lookup"><span data-stu-id="00982-139">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="00982-140">Nastavení PackageVersion přepíše PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="00982-140">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="00982-141">Autoři</span><span class="sxs-lookup"><span data-stu-id="00982-141">Authors</span></span> | <span data-ttu-id="00982-142">Autoři</span><span class="sxs-lookup"><span data-stu-id="00982-142">Authors</span></span> | <span data-ttu-id="00982-143">Uživatelské jméno aktuálního uživatele</span><span class="sxs-lookup"><span data-stu-id="00982-143">Username of the current user</span></span> | |
| <span data-ttu-id="00982-144">Vlastníci</span><span class="sxs-lookup"><span data-stu-id="00982-144">Owners</span></span> | <span data-ttu-id="00982-145">Není k dispozici</span><span class="sxs-lookup"><span data-stu-id="00982-145">N/A</span></span> | <span data-ttu-id="00982-146">Není k dispozici v souboru NuSpec</span><span class="sxs-lookup"><span data-stu-id="00982-146">Not present in NuSpec</span></span> | |
| <span data-ttu-id="00982-147">Název</span><span class="sxs-lookup"><span data-stu-id="00982-147">Title</span></span> | <span data-ttu-id="00982-148">Název</span><span class="sxs-lookup"><span data-stu-id="00982-148">Title</span></span> | <span data-ttu-id="00982-149">ID balíčku</span><span class="sxs-lookup"><span data-stu-id="00982-149">The PackageId</span></span>| |
| <span data-ttu-id="00982-150">Popis</span><span class="sxs-lookup"><span data-stu-id="00982-150">Description</span></span> | <span data-ttu-id="00982-151">Popis</span><span class="sxs-lookup"><span data-stu-id="00982-151">Description</span></span> | <span data-ttu-id="00982-152">"Balíček popis"</span><span class="sxs-lookup"><span data-stu-id="00982-152">"Package Description"</span></span> | |
| <span data-ttu-id="00982-153">Copyright</span><span class="sxs-lookup"><span data-stu-id="00982-153">Copyright</span></span> | <span data-ttu-id="00982-154">Copyright</span><span class="sxs-lookup"><span data-stu-id="00982-154">Copyright</span></span> | <span data-ttu-id="00982-155">empty</span><span class="sxs-lookup"><span data-stu-id="00982-155">empty</span></span> | |
| <span data-ttu-id="00982-156">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="00982-156">RequireLicenseAcceptance</span></span> | <span data-ttu-id="00982-157">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="00982-157">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="00982-158">false</span><span class="sxs-lookup"><span data-stu-id="00982-158">false</span></span> | |
| <span data-ttu-id="00982-159">Licence</span><span class="sxs-lookup"><span data-stu-id="00982-159">license</span></span> | <span data-ttu-id="00982-160">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="00982-160">PackageLicenseExpression</span></span> | <span data-ttu-id="00982-161">empty</span><span class="sxs-lookup"><span data-stu-id="00982-161">empty</span></span> | <span data-ttu-id="00982-162">Odpovídá `<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="00982-162">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="00982-163">Licence</span><span class="sxs-lookup"><span data-stu-id="00982-163">license</span></span> | <span data-ttu-id="00982-164">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="00982-164">PackageLicenseFile</span></span> | <span data-ttu-id="00982-165">empty</span><span class="sxs-lookup"><span data-stu-id="00982-165">empty</span></span> | <span data-ttu-id="00982-166">Odpovídá `<license type="file">`.</span><span class="sxs-lookup"><span data-stu-id="00982-166">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="00982-167">Budete muset explicitně pack odkazovaná licenční soubor.</span><span class="sxs-lookup"><span data-stu-id="00982-167">You may need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="00982-168">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="00982-168">LicenseUrl</span></span> | <span data-ttu-id="00982-169">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="00982-169">PackageLicenseUrl</span></span> | <span data-ttu-id="00982-170">empty</span><span class="sxs-lookup"><span data-stu-id="00982-170">empty</span></span> | <span data-ttu-id="00982-171">`licenseUrl` je zastaralé, použijte vlastnost PackageLicenseExpression nebo PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="00982-171">`licenseUrl` is being deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="00982-172">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="00982-172">ProjectUrl</span></span> | <span data-ttu-id="00982-173">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="00982-173">PackageProjectUrl</span></span> | <span data-ttu-id="00982-174">empty</span><span class="sxs-lookup"><span data-stu-id="00982-174">empty</span></span> | |
| <span data-ttu-id="00982-175">IconUrl</span><span class="sxs-lookup"><span data-stu-id="00982-175">IconUrl</span></span> | <span data-ttu-id="00982-176">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="00982-176">PackageIconUrl</span></span> | <span data-ttu-id="00982-177">empty</span><span class="sxs-lookup"><span data-stu-id="00982-177">empty</span></span> | |
| <span data-ttu-id="00982-178">Značky</span><span class="sxs-lookup"><span data-stu-id="00982-178">Tags</span></span> | <span data-ttu-id="00982-179">PackageTags</span><span class="sxs-lookup"><span data-stu-id="00982-179">PackageTags</span></span> | <span data-ttu-id="00982-180">empty</span><span class="sxs-lookup"><span data-stu-id="00982-180">empty</span></span> | <span data-ttu-id="00982-181">Značky jsou oddělené středníky.</span><span class="sxs-lookup"><span data-stu-id="00982-181">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="00982-182">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="00982-182">ReleaseNotes</span></span> | <span data-ttu-id="00982-183">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="00982-183">PackageReleaseNotes</span></span> | <span data-ttu-id="00982-184">empty</span><span class="sxs-lookup"><span data-stu-id="00982-184">empty</span></span> | |
| <span data-ttu-id="00982-185">Adresa Url úložiště /</span><span class="sxs-lookup"><span data-stu-id="00982-185">Repository/Url</span></span> | <span data-ttu-id="00982-186">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="00982-186">RepositoryUrl</span></span> | <span data-ttu-id="00982-187">empty</span><span class="sxs-lookup"><span data-stu-id="00982-187">empty</span></span> | <span data-ttu-id="00982-188">Adresa URL úložiště klonování nebo získat zdrojový kód.</span><span class="sxs-lookup"><span data-stu-id="00982-188">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="00982-189">Příklad: *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="00982-189">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="00982-190">Úložiště/typu</span><span class="sxs-lookup"><span data-stu-id="00982-190">Repository/Type</span></span> | <span data-ttu-id="00982-191">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="00982-191">RepositoryType</span></span> | <span data-ttu-id="00982-192">empty</span><span class="sxs-lookup"><span data-stu-id="00982-192">empty</span></span> | <span data-ttu-id="00982-193">Typ úložiště.</span><span class="sxs-lookup"><span data-stu-id="00982-193">Repository type.</span></span> <span data-ttu-id="00982-194">Příklady: *git*, *tfs*.</span><span class="sxs-lookup"><span data-stu-id="00982-194">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="00982-195">Úložiště a větve</span><span class="sxs-lookup"><span data-stu-id="00982-195">Repository/Branch</span></span> | <span data-ttu-id="00982-196">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="00982-196">RepositoryBranch</span></span> | <span data-ttu-id="00982-197">empty</span><span class="sxs-lookup"><span data-stu-id="00982-197">empty</span></span> | <span data-ttu-id="00982-198">Informace o volitelných úložišti větev</span><span class="sxs-lookup"><span data-stu-id="00982-198">Optional repository branch information.</span></span> <span data-ttu-id="00982-199">*RepositoryUrl* musí být také zadána pro tuto vlastnost, která mají být zahrnuty.</span><span class="sxs-lookup"><span data-stu-id="00982-199">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="00982-200">Příklad: *hlavní* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="00982-200">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="00982-201">Úložiště na potvrzení</span><span class="sxs-lookup"><span data-stu-id="00982-201">Repository/Commit</span></span> | <span data-ttu-id="00982-202">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="00982-202">RepositoryCommit</span></span> | <span data-ttu-id="00982-203">empty</span><span class="sxs-lookup"><span data-stu-id="00982-203">empty</span></span> | <span data-ttu-id="00982-204">Volitelné úložiště potvrzení změn nebo sadu změn k označení, které zdroje balíčku byla vytvořena.</span><span class="sxs-lookup"><span data-stu-id="00982-204">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="00982-205">*RepositoryUrl* musí být také zadána pro tuto vlastnost, která mají být zahrnuty.</span><span class="sxs-lookup"><span data-stu-id="00982-205">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="00982-206">Příklad: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="00982-206">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="00982-207">PackageType</span><span class="sxs-lookup"><span data-stu-id="00982-207">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="00982-208">Souhrn</span><span class="sxs-lookup"><span data-stu-id="00982-208">Summary</span></span> | <span data-ttu-id="00982-209">Není podporováno</span><span class="sxs-lookup"><span data-stu-id="00982-209">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="00982-210">vstupy cíl balíčku</span><span class="sxs-lookup"><span data-stu-id="00982-210">pack target inputs</span></span>

- <span data-ttu-id="00982-211">IsPackable</span><span class="sxs-lookup"><span data-stu-id="00982-211">IsPackable</span></span>
- <span data-ttu-id="00982-212">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="00982-212">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="00982-213">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="00982-213">PackageVersion</span></span>
- <span data-ttu-id="00982-214">PackageId</span><span class="sxs-lookup"><span data-stu-id="00982-214">PackageId</span></span>
- <span data-ttu-id="00982-215">Autoři</span><span class="sxs-lookup"><span data-stu-id="00982-215">Authors</span></span>
- <span data-ttu-id="00982-216">Popis</span><span class="sxs-lookup"><span data-stu-id="00982-216">Description</span></span>
- <span data-ttu-id="00982-217">Copyright</span><span class="sxs-lookup"><span data-stu-id="00982-217">Copyright</span></span>
- <span data-ttu-id="00982-218">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="00982-218">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="00982-219">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="00982-219">DevelopmentDependency</span></span>
- <span data-ttu-id="00982-220">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="00982-220">PackageLicenseExpression</span></span>
- <span data-ttu-id="00982-221">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="00982-221">PackageLicenseFile</span></span>
- <span data-ttu-id="00982-222">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="00982-222">PackageLicenseUrl</span></span>
- <span data-ttu-id="00982-223">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="00982-223">PackageProjectUrl</span></span>
- <span data-ttu-id="00982-224">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="00982-224">PackageIconUrl</span></span>
- <span data-ttu-id="00982-225">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="00982-225">PackageReleaseNotes</span></span>
- <span data-ttu-id="00982-226">PackageTags</span><span class="sxs-lookup"><span data-stu-id="00982-226">PackageTags</span></span>
- <span data-ttu-id="00982-227">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="00982-227">PackageOutputPath</span></span>
- <span data-ttu-id="00982-228">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="00982-228">IncludeSymbols</span></span>
- <span data-ttu-id="00982-229">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="00982-229">IncludeSource</span></span>
- <span data-ttu-id="00982-230">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="00982-230">PackageTypes</span></span>
- <span data-ttu-id="00982-231">IsTool</span><span class="sxs-lookup"><span data-stu-id="00982-231">IsTool</span></span>
- <span data-ttu-id="00982-232">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="00982-232">RepositoryUrl</span></span>
- <span data-ttu-id="00982-233">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="00982-233">RepositoryType</span></span>
- <span data-ttu-id="00982-234">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="00982-234">RepositoryBranch</span></span>
- <span data-ttu-id="00982-235">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="00982-235">RepositoryCommit</span></span>
- <span data-ttu-id="00982-236">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="00982-236">NoPackageAnalysis</span></span>
- <span data-ttu-id="00982-237">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="00982-237">MinClientVersion</span></span>
- <span data-ttu-id="00982-238">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="00982-238">IncludeBuildOutput</span></span>
- <span data-ttu-id="00982-239">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="00982-239">IncludeContentInPack</span></span>
- <span data-ttu-id="00982-240">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="00982-240">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="00982-241">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="00982-241">ContentTargetFolders</span></span>
- <span data-ttu-id="00982-242">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="00982-242">NuspecFile</span></span>
- <span data-ttu-id="00982-243">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="00982-243">NuspecBasePath</span></span>
- <span data-ttu-id="00982-244">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="00982-244">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="00982-245">scénáře aktualizací Service Pack</span><span class="sxs-lookup"><span data-stu-id="00982-245">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="00982-246">Potlačit závislosti</span><span class="sxs-lookup"><span data-stu-id="00982-246">Suppress dependencies</span></span>

<span data-ttu-id="00982-247">Chcete-li potlačit závislosti balíčků z vygenerované balíčku NuGet, nastavte `SuppressDependenciesWhenPacking` k `true` ta vám umožní ze souboru generovaného nupkg přeskočí všechny závislosti.</span><span class="sxs-lookup"><span data-stu-id="00982-247">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="00982-248">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="00982-248">PackageIconUrl</span></span>

<span data-ttu-id="00982-249">Jako součást změn pro [NuGet problém 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` se nakonec změní na `PackageIconUri` a může být relativní cesta k souboru ikony, který bude zahrnut v kořenovém adresáři výsledný balíček.</span><span class="sxs-lookup"><span data-stu-id="00982-249">As part of the change for [NuGet Issue 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="00982-250">Výstup sestavení</span><span class="sxs-lookup"><span data-stu-id="00982-250">Output assemblies</span></span>

<span data-ttu-id="00982-251">`nuget pack` kopíruje výstupní soubory s příponami `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, a `.pri`.</span><span class="sxs-lookup"><span data-stu-id="00982-251">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="00982-252">Výstupní soubory, které jsou zkopírovány závisí na MSBuild poskytuje od `BuiltOutputProjectGroup` cíl.</span><span class="sxs-lookup"><span data-stu-id="00982-252">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="00982-253">Existují dvě vlastnosti nástroje MSBuild, které můžete použít v souboru projektu nebo příkazového řádku do ovládacího prvku kam se obrátit výstupní sestavení:</span><span class="sxs-lookup"><span data-stu-id="00982-253">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="00982-254">`IncludeBuildOutput`: Logická hodnota, která určuje, zda sestavení výstupu sestavení by měl být součástí balíčku.</span><span class="sxs-lookup"><span data-stu-id="00982-254">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="00982-255">`BuildOutputTargetFolder`: Určuje složku, ve kterém by měl být umístěn výstup sestavení.</span><span class="sxs-lookup"><span data-stu-id="00982-255">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="00982-256">Výstup sestavení (a ostatních výstupních souborů) jsou zkopírovány do složky jejich příslušných rozhraní framework.</span><span class="sxs-lookup"><span data-stu-id="00982-256">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="00982-257">Odkazy na balíček</span><span class="sxs-lookup"><span data-stu-id="00982-257">Package references</span></span>

<span data-ttu-id="00982-258">Zobrazit [balíček odkazy v souborech projektu](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="00982-258">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="00982-259">Projekt do odkazů projektu</span><span class="sxs-lookup"><span data-stu-id="00982-259">Project to project references</span></span>

<span data-ttu-id="00982-260">Projekt tak, aby projekt odkazy jsou považovány za ve výchozím nastavení jako odkazy na balíčky nuget, třeba:</span><span class="sxs-lookup"><span data-stu-id="00982-260">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="00982-261">Můžete také přidat následující metadata pro odkaz na projekt:</span><span class="sxs-lookup"><span data-stu-id="00982-261">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="00982-262">Včetně obsahu v balíčku</span><span class="sxs-lookup"><span data-stu-id="00982-262">Including content in a package</span></span>

<span data-ttu-id="00982-263">Zahrnout obsah, přidat ke stávající navíc metadat `<Content>` položky.</span><span class="sxs-lookup"><span data-stu-id="00982-263">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="00982-264">Ve výchozím nastavení vše, co typu "Obsah" získá součástí balíčku nepřepíšete s položkami, jako je následující:</span><span class="sxs-lookup"><span data-stu-id="00982-264">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="00982-265">Ve výchozím nastavení, všechno, co přidá do kořenového adresáře `content` a `contentFiles\any\<target_framework>` složky v rámci balíčku a zachová relativní složka struktury, pokud zadáte cestu k balíčku:</span><span class="sxs-lookup"><span data-stu-id="00982-265">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="00982-266">Pokud chcete kopírovat veškerý obsah pouze na konkrétní kořenové složky (místo `content` a `contentFiles` obojí), můžete použít vlastnost MSBuild `ContentTargetFolders`, která má výchozí hodnotu "obsah; contentFiles", ale může být nastaven na jiné názvy složek.</span><span class="sxs-lookup"><span data-stu-id="00982-266">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="00982-267">Poznámka: aby pouze zadáním "contentFiles" v `ContentTargetFolders` umístí soubory s pod `contentFiles\any\<target_framework>` nebo `contentFiles\<language>\<target_framework>` na základě `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="00982-267">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="00982-268">`PackagePath` může být sadu cílových cest oddělený středníkem.</span><span class="sxs-lookup"><span data-stu-id="00982-268">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="00982-269">Zadání cesty ke prázdný balíček by přidejte soubor do kořenového adresáře balíčku.</span><span class="sxs-lookup"><span data-stu-id="00982-269">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="00982-270">Například následující přidá `libuv.txt` k `content\myfiles`, `content\samples`a kořenový adresář balíčku:</span><span class="sxs-lookup"><span data-stu-id="00982-270">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="00982-271">K dispozici je také vlastnost MSBuild `$(IncludeContentInPack)`, která má výchozí hodnotu `true`.</span><span class="sxs-lookup"><span data-stu-id="00982-271">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="00982-272">Pokud je nastavené na `false` pro žádný projekt, pak obsah z tohoto projektu nejsou součástí balíčku nuget.</span><span class="sxs-lookup"><span data-stu-id="00982-272">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="00982-273">Zahrnuje další konkrétní metadata aktualizací Service pack, kterou můžete nastavit na některou z výše uvedených položek ```<PackageCopyToOutput>``` a ```<PackageFlatten>``` který nastaví ```CopyToOutput``` a ```Flatten``` hodnoty na ```contentFiles``` záznam v souboru nuspec výstup.</span><span class="sxs-lookup"><span data-stu-id="00982-273">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="00982-274">Kromě obsahu položky `<Pack>` a `<PackagePath>` metadat lze nastavit také pro soubory s akcí sestavení kompilace, EmbeddedResource, označení třídy ApplicationDefinition, stránky, prostředek, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes , CodeAnalysisDictionary AndroidAsset, AndroidResource, BundleResource nebo žádný.</span><span class="sxs-lookup"><span data-stu-id="00982-274">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="00982-275">U balíčku k názvu souboru připojit k vaše cesta k balíčku, při použití vzorů podpory zástupných znaků cesta balíčku musí končit složky oddělovací znak, jinak cesta k balíčku je považován za úplnou cestu včetně názvu souboru.</span><span class="sxs-lookup"><span data-stu-id="00982-275">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="00982-276">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="00982-276">IncludeSymbols</span></span>

<span data-ttu-id="00982-277">Při použití `MSBuild -t:pack -p:IncludeSymbols=true`, odpovídající `.pdb` soubory se zkopírují spolu s ostatních výstupních souborů (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="00982-277">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="00982-278">Poznámka: Toto nastavení `IncludeSymbols=true` vytvoří regulárních balíček *a* balíček symbolů.</span><span class="sxs-lookup"><span data-stu-id="00982-278">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="00982-279">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="00982-279">IncludeSource</span></span>

<span data-ttu-id="00982-280">To je stejný jako `IncludeSymbols`, s tím rozdílem, že zkopíruje zdrojové soubory společně s `.pdb` i soubory.</span><span class="sxs-lookup"><span data-stu-id="00982-280">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="00982-281">Všechny soubory typu `Compile` se překopírují `src\<ProjectName>\` zachovává strukturu složek relativní cesta výsledný balíček.</span><span class="sxs-lookup"><span data-stu-id="00982-281">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="00982-282">Stejné dojde také pro zdrojové soubory žádné `ProjectReference` obsahující `TreatAsPackageReference` nastavena na `false`.</span><span class="sxs-lookup"><span data-stu-id="00982-282">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="00982-283">Pokud kompilovat soubor typu je mimo složku projektu, pak je právě přidali do `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="00982-283">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="00982-284">Balení výrazu licence nebo licenční soubor</span><span class="sxs-lookup"><span data-stu-id="00982-284">Packing a license expression or a license file</span></span>

<span data-ttu-id="00982-285">Při použití výrazu licence, PackageLicenseExpression vlastnost použít.</span><span class="sxs-lookup"><span data-stu-id="00982-285">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="00982-286">[Ukázka výrazu licence](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="00982-286">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="00982-287">[Další informace o výrazech licencí a licencí, které jsou přijaty NuGet.org](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="00982-287">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="00982-288">Při balení licenční soubor, budete muset použít vlastnost PackageLicenseFile zadat cesta k balíčku, vzhledem ke kořenové složce balíčku.</span><span class="sxs-lookup"><span data-stu-id="00982-288">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="00982-289">Kromě toho budete muset Ujistěte se, že je soubor součástí balíčku.</span><span class="sxs-lookup"><span data-stu-id="00982-289">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="00982-290">Příklad:</span><span class="sxs-lookup"><span data-stu-id="00982-290">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```
<span data-ttu-id="00982-291">[Ukázkový soubor licence](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="00982-291">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="00982-292">IsTool</span><span class="sxs-lookup"><span data-stu-id="00982-292">IsTool</span></span>

<span data-ttu-id="00982-293">Při použití `MSBuild -t:pack -p:IsTool=true`, všechny výstupní soubory, jak je uvedeno v [výstupní sestavení](#output-assemblies) scénáři se zkopírují do `tools` složky namísto `lib` složky.</span><span class="sxs-lookup"><span data-stu-id="00982-293">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="00982-294">Všimněte si, že se liší od `DotNetCliTool` který je určený nastavením `PackageType` v `.csproj` souboru.</span><span class="sxs-lookup"><span data-stu-id="00982-294">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="00982-295">Použití souboru .nuspec balení</span><span class="sxs-lookup"><span data-stu-id="00982-295">Packing using a .nuspec</span></span>

<span data-ttu-id="00982-296">Můžete použít `.nuspec` souboru se zabalit váš projekt, za předpokladu, že soubor projektu sadu SDK k importu `NuGet.Build.Tasks.Pack.targets` tak, aby úloha sady mohou být provedeny.</span><span class="sxs-lookup"><span data-stu-id="00982-296">You can use a `.nuspec` file to pack your project provided that you have a SDK project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="00982-297">Je stále potřeba obnovit projekt předtím, než můžete sbalit soubor nuspec.</span><span class="sxs-lookup"><span data-stu-id="00982-297">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="00982-298">Cílové rozhraní projektu souboru je bezvýznamná a nepoužívá se při balení souboru nuspec.</span><span class="sxs-lookup"><span data-stu-id="00982-298">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="00982-299">Následující tři vlastnosti nástroje MSBuild jsou relevantní pro balení, použití `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="00982-299">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="00982-300">`NuspecFile`: relativní nebo absolutní cesta k `.nuspec` souboru se používají pro balení.</span><span class="sxs-lookup"><span data-stu-id="00982-300">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="00982-301">`NuspecProperties`: středníkem oddělený seznam klíč = dvojice hodnot.</span><span class="sxs-lookup"><span data-stu-id="00982-301">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="00982-302">Kvůli způsobu, jakým MSBuild příkazového řádku analýzy funguje, musí být více vlastností zadán následujícím způsobem: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="00982-302">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="00982-303">`NuspecBasePath`: Základní cesta pro `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="00982-303">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="00982-304">Pokud používáte `dotnet.exe` se zabalit váš projekt, použijte příkaz podobný tomuto:</span><span class="sxs-lookup"><span data-stu-id="00982-304">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="00982-305">Pokud se váš projekt zabalit pomocí nástroje MSBuild, použijte příkaz podobný tomuto:</span><span class="sxs-lookup"><span data-stu-id="00982-305">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="00982-306">Mějte prosím na paměti, že balení nuspec pomocí dotnet.exe nebo msbuild také vede k sestavení projektu ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="00982-306">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="00982-307">To se můžete vyhnout tím, že předáte ```--no-build``` vlastnost dotnet.exe, což je ekvivalentní nastavení ```<NoBuild>true</NoBuild> ``` v souboru projektu se nastavení ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` v souboru projektu</span><span class="sxs-lookup"><span data-stu-id="00982-307">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file</span></span>

<span data-ttu-id="00982-308">Příklad souboru csproj se zabalit soubor nuspec je:</span><span class="sxs-lookup"><span data-stu-id="00982-308">An example of a csproj file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="00982-309">Pokročilé Rozšiřovací body vytvořit přizpůsobený balíček</span><span class="sxs-lookup"><span data-stu-id="00982-309">Advanced extension points to create customized package</span></span>

<span data-ttu-id="00982-310">`pack` Cílové poskytuje dva Rozšiřovací body, které běží v vnitřní, cílové rozhraní framework konkrétního sestavení.</span><span class="sxs-lookup"><span data-stu-id="00982-310">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="00982-311">Rozšiřovací body podporují včetně obsahu konkrétní cílové rozhraní framework a sestavení do balíčku:</span><span class="sxs-lookup"><span data-stu-id="00982-311">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="00982-312">`TargetsForTfmSpecificBuildOutput` Cíl: Použití pro soubory `lib` složka nebo složka zadaná pomocí `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="00982-312">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="00982-313">`TargetsForTfmSpecificContentInPackage` Cíl: Použití souborů mimo `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="00982-313">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="00982-314">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="00982-314">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="00982-315">Napsat vlastní cíl a určit ji jako hodnotu `$(TargetsForTfmSpecificBuildOutput)` vlastnost.</span><span class="sxs-lookup"><span data-stu-id="00982-315">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="00982-316">Pro všechny soubory, které je potřeba, abyste přešli do `BuildOutputTargetFolder` (lib ve výchozím nastavení), cíl by měl zápisu těchto souborů do element ItemGroup `BuildOutputInPackage` a nastavte následující dvě hodnoty metadat:</span><span class="sxs-lookup"><span data-stu-id="00982-316">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="00982-317">`FinalOutputPath`: Absolutní cestu k souboru; Pokud se nezadá, identita se používá k vyhodnocení cestu ke zdroji.</span><span class="sxs-lookup"><span data-stu-id="00982-317">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="00982-318">`TargetPath`:  (Volitelné) Nastavit, pokud je třeba soubor přejděte do podsložky v rámci `lib\<TargetFramework>` , jako jsou satelitní sestavení tohoto go ve složkách, jejich příslušné jazykové verze.</span><span class="sxs-lookup"><span data-stu-id="00982-318">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="00982-319">Výchozí hodnota je název souboru.</span><span class="sxs-lookup"><span data-stu-id="00982-319">Defaults to the name of the file.</span></span>

<span data-ttu-id="00982-320">Příklad:</span><span class="sxs-lookup"><span data-stu-id="00982-320">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="00982-321">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="00982-321">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="00982-322">Napsat vlastní cíl a určit ji jako hodnotu `$(TargetsForTfmSpecificContentInPackage)` vlastnost.</span><span class="sxs-lookup"><span data-stu-id="00982-322">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="00982-323">Pro všechny soubory, které chcete zahrnout do balíčku, cíl zápisu těchto souborů do element ItemGroup `TfmSpecificPackageFile` a nastavte následující volitelná metadata:</span><span class="sxs-lookup"><span data-stu-id="00982-323">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="00982-324">`PackagePath`: Cesta kde soubor by měl být výstup v balíčku.</span><span class="sxs-lookup"><span data-stu-id="00982-324">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="00982-325">NuGet vydá upozornění, pokud více než jeden soubor je přidaný do stejného umístění balíčku.</span><span class="sxs-lookup"><span data-stu-id="00982-325">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="00982-326">`BuildAction`: Akce sestavení, která má přiřadit k souboru, požadováno, pouze pokud cesta k balíčku v `contentFiles` složky.</span><span class="sxs-lookup"><span data-stu-id="00982-326">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="00982-327">Výchozí hodnota je "None".</span><span class="sxs-lookup"><span data-stu-id="00982-327">Defaults to "None".</span></span>

<span data-ttu-id="00982-328">Příklad:</span><span class="sxs-lookup"><span data-stu-id="00982-328">An example:</span></span>
```xml
<PropertyGroup>
  <TargetsForTfmSpecificContentInPackage>$(TargetsForTfmSpecificContentInPackage);CustomContentTarget</TargetsForTfmSpecificContentInPackage>
</PropertyGroup>

<Target Name="CustomContentTarget">
  <ItemGroup>
    <TfmSpecificPackageFile Include="abc.txt">
      <PackagePath>mycontent/$(TargetFramework)</PackagePath>
    </TfmSpecificPackageFile>
    <TfmSpecificPackageFile Include="Extensions/ext.txt" Condition="'$(TargetFramework)' == 'net46'">
      <PackagePath>net46content</PackagePath>
    </TfmSpecificPackageFile>  
  </ItemGroup>
</Target>  
```

## <a name="restore-target"></a><span data-ttu-id="00982-329">Cíl obnovení</span><span class="sxs-lookup"><span data-stu-id="00982-329">restore target</span></span>

<span data-ttu-id="00982-330">`MSBuild -t:restore` (což `nuget restore` a `dotnet restore` použití s projekty .NET Core), obnoví balíčky, které jsou popsána v souboru projektu následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="00982-330">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="00982-331">Číst všechny odkazy typu projekt na projekt</span><span class="sxs-lookup"><span data-stu-id="00982-331">Read all project to project references</span></span>
1. <span data-ttu-id="00982-332">Přečtěte si vlastnosti projektu k vyhledání zprostředkující složky a cílové architektury</span><span class="sxs-lookup"><span data-stu-id="00982-332">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="00982-333">Předání dat MSBuild NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="00982-333">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="00982-334">Spustit obnovení</span><span class="sxs-lookup"><span data-stu-id="00982-334">Run restore</span></span>
1. <span data-ttu-id="00982-335">Stáhnout balíčky</span><span class="sxs-lookup"><span data-stu-id="00982-335">Download packages</span></span>
1. <span data-ttu-id="00982-336">Zápis souboru prostředků, cíle a vlastnosti</span><span class="sxs-lookup"><span data-stu-id="00982-336">Write assets file, targets, and props</span></span>

<span data-ttu-id="00982-337">`restore` Cílit funguje **pouze** pro projekty používající formát PackageReference.</span><span class="sxs-lookup"><span data-stu-id="00982-337">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="00982-338">Provádí **není** pro projekty pomocí fungují `packages.config` formát; použijte [obnovení nuget](../tools/cli-ref-restore.md) místo.</span><span class="sxs-lookup"><span data-stu-id="00982-338">It does **not** work for projects using the `packages.config` format; use [nuget restore](../tools/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="00982-339">Obnovit vlastnosti</span><span class="sxs-lookup"><span data-stu-id="00982-339">Restore properties</span></span>

<span data-ttu-id="00982-340">Nastavení další obnovení mohou pocházet z vlastnosti nástroje MSBuild v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="00982-340">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="00982-341">Hodnoty lze také nastavit pomocí příkazového řádku `-p:` přepnout (Další příklady naleznete níže).</span><span class="sxs-lookup"><span data-stu-id="00982-341">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="00982-342">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="00982-342">Property</span></span> | <span data-ttu-id="00982-343">Popis</span><span class="sxs-lookup"><span data-stu-id="00982-343">Description</span></span> |
|--------|--------|
| <span data-ttu-id="00982-344">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="00982-344">RestoreSources</span></span> | <span data-ttu-id="00982-345">Středníkem oddělený seznam zdroje balíčků.</span><span class="sxs-lookup"><span data-stu-id="00982-345">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="00982-346">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="00982-346">RestorePackagesPath</span></span> | <span data-ttu-id="00982-347">Cesta ke složce balíčků uživatele.</span><span class="sxs-lookup"><span data-stu-id="00982-347">User packages folder path.</span></span> |
| <span data-ttu-id="00982-348">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="00982-348">RestoreDisableParallel</span></span> | <span data-ttu-id="00982-349">Limit se stáhne do postupně po jednom.</span><span class="sxs-lookup"><span data-stu-id="00982-349">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="00982-350">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="00982-350">RestoreConfigFile</span></span> | <span data-ttu-id="00982-351">Cesta k `Nuget.Config` souboru a aplikovat.</span><span class="sxs-lookup"><span data-stu-id="00982-351">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="00982-352">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="00982-352">RestoreNoCache</span></span> | <span data-ttu-id="00982-353">Při hodnotě true se vyhnete použitím balíčky v mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="00982-353">If true, avoids using cached packages.</span></span> <span data-ttu-id="00982-354">Zobrazit [Správa globálních balíčků a složek mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="00982-354">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="00982-355">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="00982-355">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="00982-356">Při hodnotě true se ignoruje neúspěšné nebo chybějící zdroje balíčků.</span><span class="sxs-lookup"><span data-stu-id="00982-356">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="00982-357">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="00982-357">RestoreFallbackFolders</span></span> | <span data-ttu-id="00982-358">Záložní složky použít stejným způsobem balíčky uživatele, který se používá složka.</span><span class="sxs-lookup"><span data-stu-id="00982-358">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="00982-359">RestoreAdditionalProjectSources</span><span class="sxs-lookup"><span data-stu-id="00982-359">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="00982-360">Další zdroje k použití během obnovení.</span><span class="sxs-lookup"><span data-stu-id="00982-360">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="00982-361">RestoreAdditionalProjectFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="00982-361">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="00982-362">Použití náhradní lokality použít další složky při obnovení.</span><span class="sxs-lookup"><span data-stu-id="00982-362">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="00982-363">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="00982-363">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="00982-364">Vyloučí záložní složky zadané v `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="00982-364">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="00982-365">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="00982-365">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="00982-366">Cesta k `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="00982-366">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="00982-367">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="00982-367">RestoreGraphProjectInput</span></span> | <span data-ttu-id="00982-368">Středníkem oddělený seznam projekty k obnovení, který by měl obsahovat absolutní cesty.</span><span class="sxs-lookup"><span data-stu-id="00982-368">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="00982-369">RestoreUseSkipNonexistentTargets</span><span class="sxs-lookup"><span data-stu-id="00982-369">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="00982-370">Pokud projekty jsou shromažďovány prostřednictvím Určuje, zda jsou jsou shromažďovány, pomocí nástroje MSBuild `SkipNonexistentTargets` optimalizace.</span><span class="sxs-lookup"><span data-stu-id="00982-370">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="00982-371">Pokud není nastavený, výchozí hodnota je `true`.</span><span class="sxs-lookup"><span data-stu-id="00982-371">When not set, defaults to `true`.</span></span> <span data-ttu-id="00982-372">Důsledkem je typu fail-fast chování při cíle projektu nelze importovat.</span><span class="sxs-lookup"><span data-stu-id="00982-372">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="00982-373">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="00982-373">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="00982-374">Výstupní složky, jako výchozí se použije `BaseIntermediateOutputPath` a `obj` složky.</span><span class="sxs-lookup"><span data-stu-id="00982-374">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="00982-375">Příklady</span><span class="sxs-lookup"><span data-stu-id="00982-375">Examples</span></span>

<span data-ttu-id="00982-376">Příkazový řádek:</span><span class="sxs-lookup"><span data-stu-id="00982-376">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="00982-377">Soubor projektu:</span><span class="sxs-lookup"><span data-stu-id="00982-377">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="00982-378">Obnovit výstupy</span><span class="sxs-lookup"><span data-stu-id="00982-378">Restore outputs</span></span>

<span data-ttu-id="00982-379">Obnovení vytvoří následující soubory v sestavení `obj` složky:</span><span class="sxs-lookup"><span data-stu-id="00982-379">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="00982-380">Soubor</span><span class="sxs-lookup"><span data-stu-id="00982-380">File</span></span> | <span data-ttu-id="00982-381">Popis</span><span class="sxs-lookup"><span data-stu-id="00982-381">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="00982-382">Obsahuje všechny odkazy na balíčky v grafu závislostí.</span><span class="sxs-lookup"><span data-stu-id="00982-382">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="00982-383">Odkazy na vlastnosti MSBuild součástí balíčků</span><span class="sxs-lookup"><span data-stu-id="00982-383">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="00982-384">Odkazy na obsažených v balíčcích cíle nástroje MSBuild</span><span class="sxs-lookup"><span data-stu-id="00982-384">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="00982-385">Obnovení a vytváření pomocí jednoho příkazu MSBuild</span><span class="sxs-lookup"><span data-stu-id="00982-385">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="00982-386">Skutečnost, že NuGet můžete obnovit balíčky, které přinášejí cíle nástroje MSBuild a vlastnosti, obnovit a hodnocení sestavení se spouštějí s různými vlastnostmi globální.</span><span class="sxs-lookup"><span data-stu-id="00982-386">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="00982-387">To znamená, že následující bude mít nepředvídatelné a často nesprávné chování.</span><span class="sxs-lookup"><span data-stu-id="00982-387">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="00982-388">Místo toho je doporučený postup:</span><span class="sxs-lookup"><span data-stu-id="00982-388">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="00982-389">Stejná logika platí mířící podobný `build`.</span><span class="sxs-lookup"><span data-stu-id="00982-389">The same logic applies to other targets similar to `build`.</span></span>

### <a name="packagetargetfallback"></a><span data-ttu-id="00982-390">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="00982-390">PackageTargetFallback</span></span>

<span data-ttu-id="00982-391">`PackageTargetFallback` Element slouží k určení sady cílů kompatibilní se použije při obnovování balíčků.</span><span class="sxs-lookup"><span data-stu-id="00982-391">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="00982-392">Je navržen tak, aby balíčky, které používají dotnet [TxM](../reference/target-frameworks.md) pro práci s kompatibilní balíčky, které není deklarovat dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="00982-392">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="00982-393">To znamená, pokud váš projekt používá dotnet TxM, pak všechny balíčky, které závisí na musí také mít dotnet TxM, pokud přidáte `<PackageTargetFallback>` do vašeho projektu, aby bylo možné povolit bez dotnet platformy se kvůli kompatibilitě s dotnet.</span><span class="sxs-lookup"><span data-stu-id="00982-393">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="00982-394">Například, pokud projekt používá `netstandard1.6` TxM a závislý balíček obsahuje pouze `lib/net45/a.dll` a `lib/portable-net45+win81/a.dll`, pak se nepodaří sestavit projekt.</span><span class="sxs-lookup"><span data-stu-id="00982-394">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="00982-395">Pokud chcete přenést druhém knihovny DLL, pak můžete přidat `PackageTargetFallback` následujícím způsobem, aby říct, že `portable-net45+win81` je kompatibilní knihovny DLL:</span><span class="sxs-lookup"><span data-stu-id="00982-395">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="00982-396">Chcete-li deklarovat jako základní pro všechny cíle ve vašem projektu, vynechat `Condition` atribut.</span><span class="sxs-lookup"><span data-stu-id="00982-396">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="00982-397">Můžete taky rozšířit, všechny existující `PackageTargetFallback` zahrnutím `$(PackageTargetFallback)` jak je znázorněno zde:</span><span class="sxs-lookup"><span data-stu-id="00982-397">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="00982-398">Nahrazení jedna knihovna z grafu obnovení</span><span class="sxs-lookup"><span data-stu-id="00982-398">Replacing one library from a restore graph</span></span>

<span data-ttu-id="00982-399">Pokud obnovení přináší na špatné sestavení, je možné, že výchozí volba balíčky a nahraďte ho vlastní možnost vyloučit.</span><span class="sxs-lookup"><span data-stu-id="00982-399">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="00982-400">První s nejvyšší úrovní `PackageReference`, vyloučit všechny prostředky:</span><span class="sxs-lookup"><span data-stu-id="00982-400">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="00982-401">V dalším kroku přidejte vlastní odkaz na příslušné místní kopie knihovny DLL:</span><span class="sxs-lookup"><span data-stu-id="00982-401">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
