---
title: Sada NuGet Pack a obnovení jako cíle MSBuild
description: Sada NuGet Pack a obnovení může pracovat přímo jako cíle MSBuild s NuGet 4.0 +.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 8403ae38b5d2e907c6f06b162a18cdcd5425565b
ms.sourcegitcommit: 5aa49478dc466c67db5c3edda7c6ce8dcd8ae033
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2019
ms.locfileid: "68817531"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="d97ae-103">Sada NuGet Pack a obnovení jako cíle MSBuild</span><span class="sxs-lookup"><span data-stu-id="d97ae-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="d97ae-104">*NuGet 4.0 +*</span><span class="sxs-lookup"><span data-stu-id="d97ae-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="d97ae-105">Ve formátu [PackageReference](../consume-packages/package-references-in-project-files.md) NuGet 4.0 + může ukládat všechna metadata manifestu přímo do souboru projektu místo použití samostatného `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="d97ae-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="d97ae-106">Pomocí nástroje MSBuild 15.1 + nástroj NuGet je také první třídou občana MSBuild s `pack` cíli `restore` a, jak je popsáno níže.</span><span class="sxs-lookup"><span data-stu-id="d97ae-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="d97ae-107">Tyto cíle vám umožňují pracovat s balíčky NuGet stejně jako s ostatními úlohami nebo cíli MSBuild.</span><span class="sxs-lookup"><span data-stu-id="d97ae-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="d97ae-108">Pokyny k vytvoření balíčku NuGet pomocí nástroje MSBuild najdete v tématu [Vytvoření balíčku NuGet pomocí nástroje MSBuild](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="d97ae-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="d97ae-109">(Pro NuGet 3. x a starší použijte místo toho příkazy [Pack](../reference/cli-reference/cli-ref-pack.md) a [obnovení](../reference/cli-reference/cli-ref-restore.md) prostřednictvím rozhraní příkazového řádku NuGet.)</span><span class="sxs-lookup"><span data-stu-id="d97ae-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="d97ae-110">Pořadí cílového sestavení</span><span class="sxs-lookup"><span data-stu-id="d97ae-110">Target build order</span></span>

<span data-ttu-id="d97ae-111">Vzhledem `pack` k `restore` tomu, že a jsou cíle nástroje MSBuild, můžete k nim přistupovat, abyste mohli vylepšit pracovní postup.</span><span class="sxs-lookup"><span data-stu-id="d97ae-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="d97ae-112">Řekněme například, že chcete po sbalení balíčku zkopírovat do sdílené síťové složky.</span><span class="sxs-lookup"><span data-stu-id="d97ae-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="d97ae-113">To lze provést přidáním následujícího do souboru projektu:</span><span class="sxs-lookup"><span data-stu-id="d97ae-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="d97ae-114">Podobně můžete napsat úlohu MSBuild, napsat vlastní cíl a využít vlastnosti NuGet v úloze MSBuild.</span><span class="sxs-lookup"><span data-stu-id="d97ae-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="d97ae-115">cíl balíčku</span><span class="sxs-lookup"><span data-stu-id="d97ae-115">pack target</span></span>

<span data-ttu-id="d97ae-116">Pro .NET Standard projekty pomocí formátu PackageReference pomocí `msbuild -t:pack` kreslení vstupů ze souboru projektu, který se má použít při vytváření balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="d97ae-116">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="d97ae-117">Následující tabulka popisuje vlastnosti nástroje MSBuild, které lze přidat do souboru projektu v rámci prvního `<PropertyGroup>` uzlu.</span><span class="sxs-lookup"><span data-stu-id="d97ae-117">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="d97ae-118">Tyto úpravy můžete snadno upravit v aplikaci Visual Studio 2017 a novějším kliknutím pravým tlačítkem myši na projekt a výběrem možnosti **Upravit {PROJECT_NAME}** v místní nabídce.</span><span class="sxs-lookup"><span data-stu-id="d97ae-118">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="d97ae-119">Pro přehlednost je tabulka uspořádaná podle ekvivalentní vlastnosti v [ `.nuspec` souboru](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="d97ae-119">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="d97ae-120">Všimněte si, `Owners` že `Summary` nástroj MSBuild `.nuspec` nepodporuje vlastnosti a.</span><span class="sxs-lookup"><span data-stu-id="d97ae-120">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="d97ae-121">Hodnota atributu/NuSpec</span><span class="sxs-lookup"><span data-stu-id="d97ae-121">Attribute/NuSpec Value</span></span> | <span data-ttu-id="d97ae-122">Vlastnost MSBuild</span><span class="sxs-lookup"><span data-stu-id="d97ae-122">MSBuild Property</span></span> | <span data-ttu-id="d97ae-123">Výchozí</span><span class="sxs-lookup"><span data-stu-id="d97ae-123">Default</span></span> | <span data-ttu-id="d97ae-124">Poznámky</span><span class="sxs-lookup"><span data-stu-id="d97ae-124">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="d97ae-125">Id</span><span class="sxs-lookup"><span data-stu-id="d97ae-125">Id</span></span> | <span data-ttu-id="d97ae-126">PackageId</span><span class="sxs-lookup"><span data-stu-id="d97ae-126">PackageId</span></span> | <span data-ttu-id="d97ae-127">Doplňk</span><span class="sxs-lookup"><span data-stu-id="d97ae-127">AssemblyName</span></span> | <span data-ttu-id="d97ae-128">$ (AssemblyName) z MSBuild</span><span class="sxs-lookup"><span data-stu-id="d97ae-128">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="d97ae-129">Version</span><span class="sxs-lookup"><span data-stu-id="d97ae-129">Version</span></span> | <span data-ttu-id="d97ae-130">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="d97ae-130">PackageVersion</span></span> | <span data-ttu-id="d97ae-131">Version</span><span class="sxs-lookup"><span data-stu-id="d97ae-131">Version</span></span> | <span data-ttu-id="d97ae-132">To je semver kompatibilní, například "1.0.0", "1.0.0-beta" nebo "1.0.0-beta-00345"</span><span class="sxs-lookup"><span data-stu-id="d97ae-132">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="d97ae-133">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="d97ae-133">VersionPrefix</span></span> | <span data-ttu-id="d97ae-134">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="d97ae-134">PackageVersionPrefix</span></span> | <span data-ttu-id="d97ae-135">empty</span><span class="sxs-lookup"><span data-stu-id="d97ae-135">empty</span></span> | <span data-ttu-id="d97ae-136">Nastavení PackageVersion přepsání PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="d97ae-136">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="d97ae-137">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="d97ae-137">VersionSuffix</span></span> | <span data-ttu-id="d97ae-138">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="d97ae-138">PackageVersionSuffix</span></span> | <span data-ttu-id="d97ae-139">empty</span><span class="sxs-lookup"><span data-stu-id="d97ae-139">empty</span></span> | <span data-ttu-id="d97ae-140">$ (VersionSuffix) z MSBuild.</span><span class="sxs-lookup"><span data-stu-id="d97ae-140">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="d97ae-141">Nastavení PackageVersion přepsání PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="d97ae-141">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="d97ae-142">Autoři</span><span class="sxs-lookup"><span data-stu-id="d97ae-142">Authors</span></span> | <span data-ttu-id="d97ae-143">Autoři</span><span class="sxs-lookup"><span data-stu-id="d97ae-143">Authors</span></span> | <span data-ttu-id="d97ae-144">Uživatelské jméno aktuálního uživatele</span><span class="sxs-lookup"><span data-stu-id="d97ae-144">Username of the current user</span></span> | |
| <span data-ttu-id="d97ae-145">Vlastníka</span><span class="sxs-lookup"><span data-stu-id="d97ae-145">Owners</span></span> | <span data-ttu-id="d97ae-146">Není k dispozici</span><span class="sxs-lookup"><span data-stu-id="d97ae-146">N/A</span></span> | <span data-ttu-id="d97ae-147">Nepřítomno v NuSpec</span><span class="sxs-lookup"><span data-stu-id="d97ae-147">Not present in NuSpec</span></span> | |
| <span data-ttu-id="d97ae-148">Název</span><span class="sxs-lookup"><span data-stu-id="d97ae-148">Title</span></span> | <span data-ttu-id="d97ae-149">Název</span><span class="sxs-lookup"><span data-stu-id="d97ae-149">Title</span></span> | <span data-ttu-id="d97ae-150">PackageId</span><span class="sxs-lookup"><span data-stu-id="d97ae-150">The PackageId</span></span>| |
| <span data-ttu-id="d97ae-151">Popis</span><span class="sxs-lookup"><span data-stu-id="d97ae-151">Description</span></span> | <span data-ttu-id="d97ae-152">Popis</span><span class="sxs-lookup"><span data-stu-id="d97ae-152">Description</span></span> | <span data-ttu-id="d97ae-153">Popis balíčku</span><span class="sxs-lookup"><span data-stu-id="d97ae-153">"Package Description"</span></span> | |
| <span data-ttu-id="d97ae-154">Úprava</span><span class="sxs-lookup"><span data-stu-id="d97ae-154">Copyright</span></span> | <span data-ttu-id="d97ae-155">Úprava</span><span class="sxs-lookup"><span data-stu-id="d97ae-155">Copyright</span></span> | <span data-ttu-id="d97ae-156">empty</span><span class="sxs-lookup"><span data-stu-id="d97ae-156">empty</span></span> | |
| <span data-ttu-id="d97ae-157">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="d97ae-157">RequireLicenseAcceptance</span></span> | <span data-ttu-id="d97ae-158">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="d97ae-158">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="d97ae-159">false</span><span class="sxs-lookup"><span data-stu-id="d97ae-159">false</span></span> | |
| <span data-ttu-id="d97ae-160">průkaz</span><span class="sxs-lookup"><span data-stu-id="d97ae-160">license</span></span> | <span data-ttu-id="d97ae-161">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="d97ae-161">PackageLicenseExpression</span></span> | <span data-ttu-id="d97ae-162">empty</span><span class="sxs-lookup"><span data-stu-id="d97ae-162">empty</span></span> | <span data-ttu-id="d97ae-163">Odpovídá`<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="d97ae-163">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="d97ae-164">průkaz</span><span class="sxs-lookup"><span data-stu-id="d97ae-164">license</span></span> | <span data-ttu-id="d97ae-165">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="d97ae-165">PackageLicenseFile</span></span> | <span data-ttu-id="d97ae-166">empty</span><span class="sxs-lookup"><span data-stu-id="d97ae-166">empty</span></span> | <span data-ttu-id="d97ae-167">`<license type="file">`Odpovídá.</span><span class="sxs-lookup"><span data-stu-id="d97ae-167">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="d97ae-168">Je možné, že bude nutné explicitně sbalit soubor s odkazem na licenci.</span><span class="sxs-lookup"><span data-stu-id="d97ae-168">You may need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="d97ae-169">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="d97ae-169">LicenseUrl</span></span> | <span data-ttu-id="d97ae-170">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="d97ae-170">PackageLicenseUrl</span></span> | <span data-ttu-id="d97ae-171">empty</span><span class="sxs-lookup"><span data-stu-id="d97ae-171">empty</span></span> | <span data-ttu-id="d97ae-172">`licenseUrl`se už nepoužívá, použijte vlastnost PackageLicenseExpression nebo PackageLicenseFile.</span><span class="sxs-lookup"><span data-stu-id="d97ae-172">`licenseUrl` is being deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="d97ae-173">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="d97ae-173">ProjectUrl</span></span> | <span data-ttu-id="d97ae-174">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="d97ae-174">PackageProjectUrl</span></span> | <span data-ttu-id="d97ae-175">empty</span><span class="sxs-lookup"><span data-stu-id="d97ae-175">empty</span></span> | |
| <span data-ttu-id="d97ae-176">IconUrl</span><span class="sxs-lookup"><span data-stu-id="d97ae-176">IconUrl</span></span> | <span data-ttu-id="d97ae-177">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="d97ae-177">PackageIconUrl</span></span> | <span data-ttu-id="d97ae-178">empty</span><span class="sxs-lookup"><span data-stu-id="d97ae-178">empty</span></span> | |
| <span data-ttu-id="d97ae-179">Značky</span><span class="sxs-lookup"><span data-stu-id="d97ae-179">Tags</span></span> | <span data-ttu-id="d97ae-180">PackageTags</span><span class="sxs-lookup"><span data-stu-id="d97ae-180">PackageTags</span></span> | <span data-ttu-id="d97ae-181">empty</span><span class="sxs-lookup"><span data-stu-id="d97ae-181">empty</span></span> | <span data-ttu-id="d97ae-182">Značky jsou středníky odděleny středníkem.</span><span class="sxs-lookup"><span data-stu-id="d97ae-182">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="d97ae-183">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="d97ae-183">ReleaseNotes</span></span> | <span data-ttu-id="d97ae-184">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="d97ae-184">PackageReleaseNotes</span></span> | <span data-ttu-id="d97ae-185">empty</span><span class="sxs-lookup"><span data-stu-id="d97ae-185">empty</span></span> | |
| <span data-ttu-id="d97ae-186">Úložiště/adresa URL</span><span class="sxs-lookup"><span data-stu-id="d97ae-186">Repository/Url</span></span> | <span data-ttu-id="d97ae-187">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="d97ae-187">RepositoryUrl</span></span> | <span data-ttu-id="d97ae-188">empty</span><span class="sxs-lookup"><span data-stu-id="d97ae-188">empty</span></span> | <span data-ttu-id="d97ae-189">Adresa URL úložiště, která se používá k klonování nebo načtení zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="d97ae-189">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="d97ae-190">Případě *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="d97ae-190">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="d97ae-191">Úložiště/typ</span><span class="sxs-lookup"><span data-stu-id="d97ae-191">Repository/Type</span></span> | <span data-ttu-id="d97ae-192">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="d97ae-192">RepositoryType</span></span> | <span data-ttu-id="d97ae-193">empty</span><span class="sxs-lookup"><span data-stu-id="d97ae-193">empty</span></span> | <span data-ttu-id="d97ae-194">Typ úložiště</span><span class="sxs-lookup"><span data-stu-id="d97ae-194">Repository type.</span></span> <span data-ttu-id="d97ae-195">Příklady: *Git*, *TFS*.</span><span class="sxs-lookup"><span data-stu-id="d97ae-195">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="d97ae-196">Úložiště/větev</span><span class="sxs-lookup"><span data-stu-id="d97ae-196">Repository/Branch</span></span> | <span data-ttu-id="d97ae-197">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="d97ae-197">RepositoryBranch</span></span> | <span data-ttu-id="d97ae-198">empty</span><span class="sxs-lookup"><span data-stu-id="d97ae-198">empty</span></span> | <span data-ttu-id="d97ae-199">Volitelné informace o větvi úložiště</span><span class="sxs-lookup"><span data-stu-id="d97ae-199">Optional repository branch information.</span></span> <span data-ttu-id="d97ae-200">Pro zahrnutí této vlastnosti je nutné zadat také *RepositoryUrl* .</span><span class="sxs-lookup"><span data-stu-id="d97ae-200">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="d97ae-201">Příklad: *Master* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="d97ae-201">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="d97ae-202">Úložiště/potvrzení změn</span><span class="sxs-lookup"><span data-stu-id="d97ae-202">Repository/Commit</span></span> | <span data-ttu-id="d97ae-203">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="d97ae-203">RepositoryCommit</span></span> | <span data-ttu-id="d97ae-204">empty</span><span class="sxs-lookup"><span data-stu-id="d97ae-204">empty</span></span> | <span data-ttu-id="d97ae-205">Volitelné potvrzení změn úložiště nebo sada změn, které označují, na který zdroj byl balíček vytvořen.</span><span class="sxs-lookup"><span data-stu-id="d97ae-205">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="d97ae-206">Pro zahrnutí této vlastnosti je nutné zadat také *RepositoryUrl* .</span><span class="sxs-lookup"><span data-stu-id="d97ae-206">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="d97ae-207">Příklad: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="d97ae-207">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="d97ae-208">PackageType</span><span class="sxs-lookup"><span data-stu-id="d97ae-208">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="d97ae-209">Souhrn</span><span class="sxs-lookup"><span data-stu-id="d97ae-209">Summary</span></span> | <span data-ttu-id="d97ae-210">Není podporováno</span><span class="sxs-lookup"><span data-stu-id="d97ae-210">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="d97ae-211">cílové vstupy balení</span><span class="sxs-lookup"><span data-stu-id="d97ae-211">pack target inputs</span></span>

- <span data-ttu-id="d97ae-212">Ispackable nastavenou</span><span class="sxs-lookup"><span data-stu-id="d97ae-212">IsPackable</span></span>
- <span data-ttu-id="d97ae-213">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="d97ae-213">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="d97ae-214">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="d97ae-214">PackageVersion</span></span>
- <span data-ttu-id="d97ae-215">PackageId</span><span class="sxs-lookup"><span data-stu-id="d97ae-215">PackageId</span></span>
- <span data-ttu-id="d97ae-216">Autoři</span><span class="sxs-lookup"><span data-stu-id="d97ae-216">Authors</span></span>
- <span data-ttu-id="d97ae-217">Popis</span><span class="sxs-lookup"><span data-stu-id="d97ae-217">Description</span></span>
- <span data-ttu-id="d97ae-218">Úprava</span><span class="sxs-lookup"><span data-stu-id="d97ae-218">Copyright</span></span>
- <span data-ttu-id="d97ae-219">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="d97ae-219">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="d97ae-220">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="d97ae-220">DevelopmentDependency</span></span>
- <span data-ttu-id="d97ae-221">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="d97ae-221">PackageLicenseExpression</span></span>
- <span data-ttu-id="d97ae-222">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="d97ae-222">PackageLicenseFile</span></span>
- <span data-ttu-id="d97ae-223">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="d97ae-223">PackageLicenseUrl</span></span>
- <span data-ttu-id="d97ae-224">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="d97ae-224">PackageProjectUrl</span></span>
- <span data-ttu-id="d97ae-225">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="d97ae-225">PackageIconUrl</span></span>
- <span data-ttu-id="d97ae-226">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="d97ae-226">PackageReleaseNotes</span></span>
- <span data-ttu-id="d97ae-227">PackageTags</span><span class="sxs-lookup"><span data-stu-id="d97ae-227">PackageTags</span></span>
- <span data-ttu-id="d97ae-228">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="d97ae-228">PackageOutputPath</span></span>
- <span data-ttu-id="d97ae-229">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="d97ae-229">IncludeSymbols</span></span>
- <span data-ttu-id="d97ae-230">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="d97ae-230">IncludeSource</span></span>
- <span data-ttu-id="d97ae-231">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="d97ae-231">PackageTypes</span></span>
- <span data-ttu-id="d97ae-232">Nástroj</span><span class="sxs-lookup"><span data-stu-id="d97ae-232">IsTool</span></span>
- <span data-ttu-id="d97ae-233">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="d97ae-233">RepositoryUrl</span></span>
- <span data-ttu-id="d97ae-234">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="d97ae-234">RepositoryType</span></span>
- <span data-ttu-id="d97ae-235">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="d97ae-235">RepositoryBranch</span></span>
- <span data-ttu-id="d97ae-236">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="d97ae-236">RepositoryCommit</span></span>
- <span data-ttu-id="d97ae-237">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="d97ae-237">NoPackageAnalysis</span></span>
- <span data-ttu-id="d97ae-238">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="d97ae-238">MinClientVersion</span></span>
- <span data-ttu-id="d97ae-239">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="d97ae-239">IncludeBuildOutput</span></span>
- <span data-ttu-id="d97ae-240">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="d97ae-240">IncludeContentInPack</span></span>
- <span data-ttu-id="d97ae-241">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="d97ae-241">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="d97ae-242">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="d97ae-242">ContentTargetFolders</span></span>
- <span data-ttu-id="d97ae-243">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="d97ae-243">NuspecFile</span></span>
- <span data-ttu-id="d97ae-244">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="d97ae-244">NuspecBasePath</span></span>
- <span data-ttu-id="d97ae-245">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="d97ae-245">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="d97ae-246">scénáře sady Pack</span><span class="sxs-lookup"><span data-stu-id="d97ae-246">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="d97ae-247">Potlačit závislosti</span><span class="sxs-lookup"><span data-stu-id="d97ae-247">Suppress dependencies</span></span>

<span data-ttu-id="d97ae-248">Chcete-li potlačit závislosti balíčků z vygenerovaného `true` balíčku NuGet, nastavte `SuppressDependenciesWhenPacking` na to, které umožní přeskočí všechny závislosti ze generovaného souboru nupkg.</span><span class="sxs-lookup"><span data-stu-id="d97ae-248">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="d97ae-249">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="d97ae-249">PackageIconUrl</span></span>

<span data-ttu-id="d97ae-250">V rámci změny [problému NuGet 352](https://github.com/NuGet/Home/issues/352)se nakonec změní na `PackageIconUrl` `PackageIconUri` a může to být relativní cesta k souboru ikony, který bude zahrnutý v kořenu výsledného balíčku.</span><span class="sxs-lookup"><span data-stu-id="d97ae-250">As part of the change for [NuGet Issue 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="d97ae-251">Výstupní sestavení</span><span class="sxs-lookup"><span data-stu-id="d97ae-251">Output assemblies</span></span>

<span data-ttu-id="d97ae-252">`nuget pack`zkopíruje výstupní `.exe`soubory s příponami `.dll` `.xml` ,,`.winmd`,, a `.pri`. `.json`</span><span class="sxs-lookup"><span data-stu-id="d97ae-252">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="d97ae-253">Výstupní soubory, které jsou zkopírovány, závisí na tom, co `BuiltOutputProjectGroup` nástroj MSBuild poskytuje z cíle.</span><span class="sxs-lookup"><span data-stu-id="d97ae-253">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="d97ae-254">Existují dvě vlastnosti nástroje MSBuild, které lze použít v souboru projektu nebo na příkazovém řádku pro řízení, kde výstupní sestavení jdou:</span><span class="sxs-lookup"><span data-stu-id="d97ae-254">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="d97ae-255">`IncludeBuildOutput`: Logická hodnota, která určuje, zda mají být do balíčku zahrnuty výstupní sestavení sestavení.</span><span class="sxs-lookup"><span data-stu-id="d97ae-255">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="d97ae-256">`BuildOutputTargetFolder`: Určuje složku, do které se mají umístit výstupní sestavení.</span><span class="sxs-lookup"><span data-stu-id="d97ae-256">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="d97ae-257">Výstupní sestavení (a další výstupní soubory) se zkopírují do příslušných složek rozhraní.</span><span class="sxs-lookup"><span data-stu-id="d97ae-257">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="d97ae-258">Odkazy na balíčky</span><span class="sxs-lookup"><span data-stu-id="d97ae-258">Package references</span></span>

<span data-ttu-id="d97ae-259">Viz [odkazy na balíčky v souborech projektu](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="d97ae-259">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="d97ae-260">Odkazy na projekt a projekt</span><span class="sxs-lookup"><span data-stu-id="d97ae-260">Project to project references</span></span>

<span data-ttu-id="d97ae-261">Odkazy na projekt na projekt jsou ve výchozím nastavení považovány za odkazy na balíčky NuGet, například:</span><span class="sxs-lookup"><span data-stu-id="d97ae-261">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="d97ae-262">Do odkazu na projekt můžete také přidat následující metadata:</span><span class="sxs-lookup"><span data-stu-id="d97ae-262">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="d97ae-263">Zahrnutí obsahu do balíčku</span><span class="sxs-lookup"><span data-stu-id="d97ae-263">Including content in a package</span></span>

<span data-ttu-id="d97ae-264">Chcete-li zahrnout obsah, přidejte do existující `<Content>` položky metadata navíc.</span><span class="sxs-lookup"><span data-stu-id="d97ae-264">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="d97ae-265">Ve výchozím nastavení jsou všechny položky typu "obsah" zahrnuty do balíčku, Pokud nepřepíšete záznamy podobné následujícímu:</span><span class="sxs-lookup"><span data-stu-id="d97ae-265">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="d97ae-266">Ve výchozím nastavení je vše přidáno do kořenu `content` a `contentFiles\any\<target_framework>` složky v rámci balíčku a zachovává strukturu relativních složek, pokud nezadáte cestu k balíčku:</span><span class="sxs-lookup"><span data-stu-id="d97ae-266">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="d97ae-267">Pokud chcete kopírovat veškerý obsah pouze na konkrétní kořenové složky (místo `content` a `contentFiles` obojí), můžete použít vlastnost `ContentTargetFolders`MSBuild, která má výchozí hodnotu Content; contentFiles, ale lze ji nastavit na jiné názvy složek.</span><span class="sxs-lookup"><span data-stu-id="d97ae-267">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="d97ae-268">Všimněte si, že pouze zadání "contentFiles `ContentTargetFolders` " v `contentFiles\any\<target_framework>` souboru vloží `contentFiles\<language>\<target_framework>` soubory do `buildAction`nebo na základě.</span><span class="sxs-lookup"><span data-stu-id="d97ae-268">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="d97ae-269">`PackagePath`může se jednat o sadu cílových cest oddělených středníky.</span><span class="sxs-lookup"><span data-stu-id="d97ae-269">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="d97ae-270">Zadáním prázdné cesty k balíčku by se soubor přidal do kořenového adresáře balíčku.</span><span class="sxs-lookup"><span data-stu-id="d97ae-270">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="d97ae-271">Například následující příkaz přidá `libuv.txt` do `content\myfiles`, `content\samples`a kořenovou složku balíčku:</span><span class="sxs-lookup"><span data-stu-id="d97ae-271">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="d97ae-272">K dispozici je také vlastnost `$(IncludeContentInPack)`MSBuild, která má `true`výchozí hodnotu.</span><span class="sxs-lookup"><span data-stu-id="d97ae-272">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="d97ae-273">Pokud je nastavená `false` na libovolný projekt, pak obsah z tohoto projektu není zahrnutý v balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="d97ae-273">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="d97ae-274">Další metadata specifická pro sadu, která můžete nastavit na kterékoli z výše uvedených položek ```<PackageCopyToOutput>``` , ```<PackageFlatten>``` zahrnují a ```CopyToOutput``` které ```Flatten``` ```contentFiles``` sady a hodnoty pro položku ve výstupních nuspec.</span><span class="sxs-lookup"><span data-stu-id="d97ae-274">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="d97ae-275">Kromě položek `<Pack>` obsahu lze metadata a `<PackagePath>` také nastavit na soubory s akcí sestavení kompilovat, EmbeddedResource, ApplicationDefinition, Page, Resource, třídy SplashScreen, vazbě designdata, DesignDataWithDesignTimeCreateableTypes , CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource nebo None.</span><span class="sxs-lookup"><span data-stu-id="d97ae-275">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="d97ae-276">Pokud má balíček při použití vzorů expanze názvů připojit název souboru k cestě k balíčku, musí cesta k balíčku končit znakem oddělovače složky. v opačném případě se cesta k balíčku považuje za úplnou cestu včetně názvu souboru.</span><span class="sxs-lookup"><span data-stu-id="d97ae-276">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="d97ae-277">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="d97ae-277">IncludeSymbols</span></span>

<span data-ttu-id="d97ae-278">Při použití `MSBuild -t:pack -p:IncludeSymbols=true`se zkopírují `.pdb` odpovídající soubory spolu s jinými výstupními `.xml`soubory (`.dll`, `.exe`, `.winmd`,, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="d97ae-278">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="d97ae-279">Všimněte si, `IncludeSymbols=true` že nastavení vytvoří regulární balíček *a* balíček symbolů.</span><span class="sxs-lookup"><span data-stu-id="d97ae-279">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="d97ae-280">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="d97ae-280">IncludeSource</span></span>

<span data-ttu-id="d97ae-281">To je stejné jako `IncludeSymbols`s tím rozdílem, že kopíruje také zdrojové soubory spolu se `.pdb` soubory.</span><span class="sxs-lookup"><span data-stu-id="d97ae-281">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="d97ae-282">Všechny soubory typu `Compile` jsou zkopírovány za účelem `src\<ProjectName>\` zachování struktury složek relativní cesty ve výsledném balíčku.</span><span class="sxs-lookup"><span data-stu-id="d97ae-282">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="d97ae-283">Totéž se také stane u zdrojových souborů, `ProjectReference` které mají `TreatAsPackageReference` nastavené na `false`.</span><span class="sxs-lookup"><span data-stu-id="d97ae-283">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="d97ae-284">Pokud je soubor typu Compile mimo složku projektu, pak je pouze přidán do `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="d97ae-284">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="d97ae-285">Balení licenčního výrazu nebo licenčního souboru</span><span class="sxs-lookup"><span data-stu-id="d97ae-285">Packing a license expression or a license file</span></span>

<span data-ttu-id="d97ae-286">Při použití licenčního výrazu by se měla použít vlastnost PackageLicenseExpression.</span><span class="sxs-lookup"><span data-stu-id="d97ae-286">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="d97ae-287">[Ukázka licenčního výrazu](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="d97ae-287">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="d97ae-288">[Přečtěte si další informace o výrazech licencí a licencích, které jsou přijaty nástrojem NuGet.org](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="d97ae-288">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="d97ae-289">Při balení licenčního souboru musíte použít vlastnost PackageLicenseFile a zadat cestu k balíčku relativní ke kořenu balíčku.</span><span class="sxs-lookup"><span data-stu-id="d97ae-289">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="d97ae-290">Kromě toho je nutné zajistit, aby byl soubor zahrnut do balíčku.</span><span class="sxs-lookup"><span data-stu-id="d97ae-290">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="d97ae-291">Příklad:</span><span class="sxs-lookup"><span data-stu-id="d97ae-291">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```
<span data-ttu-id="d97ae-292">[Ukázka licenčního souboru](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="d97ae-292">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="d97ae-293">Nástroj</span><span class="sxs-lookup"><span data-stu-id="d97ae-293">IsTool</span></span>

<span data-ttu-id="d97ae-294">Při použití `MSBuild -t:pack -p:IsTool=true`aplikace `lib` `tools` jsou všechny výstupní soubory, jak je uvedeno ve scénáři [výstup sestavení](#output-assemblies) , zkopírovány do složky namísto složky.</span><span class="sxs-lookup"><span data-stu-id="d97ae-294">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="d97ae-295">Všimněte si, že se liší od `DotNetCliTool` a, který je určen `PackageType` nastavením v `.csproj` souboru.</span><span class="sxs-lookup"><span data-stu-id="d97ae-295">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="d97ae-296">Balení pomocí. nuspec</span><span class="sxs-lookup"><span data-stu-id="d97ae-296">Packing using a .nuspec</span></span>

<span data-ttu-id="d97ae-297">I když se místo toho doporučuje [Zahrnout všechny vlastnosti](../reference/msbuild-targets.md#pack-target) , které jsou obvykle v `.nuspec` souboru v souboru projektu, můžete `.nuspec` zvolit použití souboru k balení projektu.</span><span class="sxs-lookup"><span data-stu-id="d97ae-297">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="d97ae-298">Pro projekt bez sady SDK, který používá `PackageReference`, je nutné importovat `NuGet.Build.Tasks.Pack.targets` , aby bylo možné spustit úlohu balíčku.</span><span class="sxs-lookup"><span data-stu-id="d97ae-298">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="d97ae-299">Před zabalením souboru nuspec je ještě nutné projekt obnovit.</span><span class="sxs-lookup"><span data-stu-id="d97ae-299">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="d97ae-300">(Projekt ve stylu sady SDK obsahuje cíle balíčku ve výchozím nastavení.)</span><span class="sxs-lookup"><span data-stu-id="d97ae-300">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="d97ae-301">Cílová architektura souboru projektu je nerelevantní a při balení nuspec se nepoužívá.</span><span class="sxs-lookup"><span data-stu-id="d97ae-301">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="d97ae-302">Následující tři vlastnosti MSBuild jsou relevantní pro balení pomocí `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="d97ae-302">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="d97ae-303">`NuspecFile`: relativní nebo absolutní cesta k `.nuspec` souboru, který se používá k balení.</span><span class="sxs-lookup"><span data-stu-id="d97ae-303">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="d97ae-304">`NuspecProperties`: středníkem oddělený seznam dvojic klíč = hodnota.</span><span class="sxs-lookup"><span data-stu-id="d97ae-304">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="d97ae-305">Kvůli způsobu, jakým funguje analýza příkazového řádku nástroje MSBuild, je nutné zadat více vlastností následujícím `-p:NuspecProperties=\"key1=value1;key2=value2\"`způsobem:.</span><span class="sxs-lookup"><span data-stu-id="d97ae-305">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="d97ae-306">`NuspecBasePath`: Základní cesta k `.nuspec` souboru</span><span class="sxs-lookup"><span data-stu-id="d97ae-306">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="d97ae-307">Pokud používáte `dotnet.exe` k balení projektu, použijte příkaz podobný následujícímu:</span><span class="sxs-lookup"><span data-stu-id="d97ae-307">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="d97ae-308">Při použití nástroje MSBuild k sbalení projektu použijte příkaz podobný následujícímu:</span><span class="sxs-lookup"><span data-stu-id="d97ae-308">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="d97ae-309">Všimněte si, že balení nuspec pomocí příkazu dotnet. exe nebo MSBuild také vede k sestavení projektu ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="d97ae-309">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="d97ae-310">K tomu je možné se vyhnout předáním ```--no-build``` vlastnosti do příkazu dotnet. exe, který je ekvivalentem nastavení ```<NoBuild>true</NoBuild> ``` v souboru projektu společně s nastavením ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="d97ae-310">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="d97ae-311">Příkladem souboru *. csproj* pro zabalení souboru nuspec je:</span><span class="sxs-lookup"><span data-stu-id="d97ae-311">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="d97ae-312">Rozšířené body rozšíření pro vytvoření přizpůsobeného balíčku</span><span class="sxs-lookup"><span data-stu-id="d97ae-312">Advanced extension points to create customized package</span></span>

<span data-ttu-id="d97ae-313">`pack` Cíl poskytuje dva Rozšiřovací body, které jsou spuštěny v sestavení specifickém pro vnitřní, cílové rozhraní.</span><span class="sxs-lookup"><span data-stu-id="d97ae-313">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="d97ae-314">Rozšiřující body podporují obsah a sestavení konkrétního cílového rozhraní do balíčku:</span><span class="sxs-lookup"><span data-stu-id="d97ae-314">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="d97ae-315">`TargetsForTfmSpecificBuildOutput`cílové Používá se pro soubory uvnitř `lib` složky nebo složky zadané pomocí. `BuildOutputTargetFolder`</span><span class="sxs-lookup"><span data-stu-id="d97ae-315">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="d97ae-316">`TargetsForTfmSpecificContentInPackage`cílové Použít pro soubory mimo `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="d97ae-316">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="d97ae-317">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="d97ae-317">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="d97ae-318">Napište vlastní cíl a zadejte ho jako hodnotu `$(TargetsForTfmSpecificBuildOutput)` vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="d97ae-318">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="d97ae-319">Pro všechny soubory, které potřebují přejít do `BuildOutputTargetFolder` nástroje (ve výchozím nastavení lib), by měl cíl zapisovat tyto soubory do skupiny `BuildOutputInPackage` Item a nastavit následující dvě hodnoty metadat:</span><span class="sxs-lookup"><span data-stu-id="d97ae-319">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="d97ae-320">`FinalOutputPath`: Absolutní cesta k souboru; Pokud není zadaný, použije se identita k vyhodnocení zdrojové cesty.</span><span class="sxs-lookup"><span data-stu-id="d97ae-320">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="d97ae-321">`TargetPath`:  Volitelné Nastavte, kdy soubor musí přejít do podsložky v rámci `lib\<TargetFramework>` , podobně jako satelitní sestavení, která se nacházejí v odpovídajících složkách kultury.</span><span class="sxs-lookup"><span data-stu-id="d97ae-321">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="d97ae-322">Výchozí hodnota je název souboru.</span><span class="sxs-lookup"><span data-stu-id="d97ae-322">Defaults to the name of the file.</span></span>

<span data-ttu-id="d97ae-323">Příklad:</span><span class="sxs-lookup"><span data-stu-id="d97ae-323">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="d97ae-324">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="d97ae-324">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="d97ae-325">Napište vlastní cíl a zadejte ho jako hodnotu `$(TargetsForTfmSpecificContentInPackage)` vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="d97ae-325">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="d97ae-326">U všech souborů, které se mají zahrnout do balíčku, by měl cíl tyto soubory zapsat do skupiny `TfmSpecificPackageFile` položek a nastavit následující volitelná metadata:</span><span class="sxs-lookup"><span data-stu-id="d97ae-326">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="d97ae-327">`PackagePath`: Cesta, kde by měl být v balíčku výstup souboru.</span><span class="sxs-lookup"><span data-stu-id="d97ae-327">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="d97ae-328">Při přidání více než jednoho souboru do stejné cesty k balíčku vyvolá NuGet vystavení upozornění.</span><span class="sxs-lookup"><span data-stu-id="d97ae-328">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="d97ae-329">`BuildAction`: Akce sestavení, která se má přiřadit k souboru, se vyžaduje jenom v případě, že je `contentFiles` cesta k balíčku ve složce.</span><span class="sxs-lookup"><span data-stu-id="d97ae-329">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="d97ae-330">Výchozí hodnota je None.</span><span class="sxs-lookup"><span data-stu-id="d97ae-330">Defaults to "None".</span></span>

<span data-ttu-id="d97ae-331">Příklad:</span><span class="sxs-lookup"><span data-stu-id="d97ae-331">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="d97ae-332">cíl obnovení</span><span class="sxs-lookup"><span data-stu-id="d97ae-332">restore target</span></span>

<span data-ttu-id="d97ae-333">`MSBuild -t:restore`(které `nuget restore` a `dotnet restore` používají se v projektech .NET Core), obnoví balíčky, na které se odkazuje v souboru projektu, takto:</span><span class="sxs-lookup"><span data-stu-id="d97ae-333">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="d97ae-334">Číst všechny odkazy z projektu na projekt</span><span class="sxs-lookup"><span data-stu-id="d97ae-334">Read all project to project references</span></span>
1. <span data-ttu-id="d97ae-335">Přečtěte si vlastnosti projektu a najděte mezilehlé složky a cílová rozhraní.</span><span class="sxs-lookup"><span data-stu-id="d97ae-335">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="d97ae-336">Předání dat nástroje MSBuild do NuGet. Build. Tasks. dll</span><span class="sxs-lookup"><span data-stu-id="d97ae-336">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="d97ae-337">Spustit obnovení</span><span class="sxs-lookup"><span data-stu-id="d97ae-337">Run restore</span></span>
1. <span data-ttu-id="d97ae-338">Stáhnout balíčky</span><span class="sxs-lookup"><span data-stu-id="d97ae-338">Download packages</span></span>
1. <span data-ttu-id="d97ae-339">Zápis souboru prostředků, cílů a vlastností props</span><span class="sxs-lookup"><span data-stu-id="d97ae-339">Write assets file, targets, and props</span></span>

<span data-ttu-id="d97ae-340">Cíl funguje pouze pro projekty, které používají formát PackageReference. `restore`</span><span class="sxs-lookup"><span data-stu-id="d97ae-340">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="d97ae-341">Nefunguje pro projekty používající `packages.config` formát. místo toho použijte [obnovení NuGet](../reference/cli-reference/cli-ref-restore.md) .</span><span class="sxs-lookup"><span data-stu-id="d97ae-341">It does **not** work for projects using the `packages.config` format; use [nuget restore](../reference/cli-reference/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="d97ae-342">Obnovit vlastnosti</span><span class="sxs-lookup"><span data-stu-id="d97ae-342">Restore properties</span></span>

<span data-ttu-id="d97ae-343">Další nastavení obnovení může pocházet z vlastností MSBuild v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="d97ae-343">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="d97ae-344">Hodnoty lze také nastavit z příkazového řádku pomocí `-p:` přepínače (viz příklady níže).</span><span class="sxs-lookup"><span data-stu-id="d97ae-344">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="d97ae-345">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="d97ae-345">Property</span></span> | <span data-ttu-id="d97ae-346">Popis</span><span class="sxs-lookup"><span data-stu-id="d97ae-346">Description</span></span> |
|--------|--------|
| <span data-ttu-id="d97ae-347">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="d97ae-347">RestoreSources</span></span> | <span data-ttu-id="d97ae-348">Seznam zdrojů balíčků oddělených středníkem.</span><span class="sxs-lookup"><span data-stu-id="d97ae-348">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="d97ae-349">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="d97ae-349">RestorePackagesPath</span></span> | <span data-ttu-id="d97ae-350">Cesta ke složce uživatelských balíčků</span><span class="sxs-lookup"><span data-stu-id="d97ae-350">User packages folder path.</span></span> |
| <span data-ttu-id="d97ae-351">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="d97ae-351">RestoreDisableParallel</span></span> | <span data-ttu-id="d97ae-352">Omezit stahování na jednu po druhé.</span><span class="sxs-lookup"><span data-stu-id="d97ae-352">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="d97ae-353">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="d97ae-353">RestoreConfigFile</span></span> | <span data-ttu-id="d97ae-354">Cesta k `Nuget.Config` souboru, který se má použít</span><span class="sxs-lookup"><span data-stu-id="d97ae-354">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="d97ae-355">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="d97ae-355">RestoreNoCache</span></span> | <span data-ttu-id="d97ae-356">Je-li nastavena hodnota true, nepoužívejte balíčky uložené v mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="d97ae-356">If true, avoids using cached packages.</span></span> <span data-ttu-id="d97ae-357">Viz [Správa globálních balíčků a složek mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="d97ae-357">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="d97ae-358">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="d97ae-358">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="d97ae-359">Pokud má hodnotu true, ignoruje neúspěšné nebo chybějící zdroje balíčků.</span><span class="sxs-lookup"><span data-stu-id="d97ae-359">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="d97ae-360">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="d97ae-360">RestoreFallbackFolders</span></span> | <span data-ttu-id="d97ae-361">Záložní složky používané ve stejném způsobu, jakým se používá složka uživatelských balíčků.</span><span class="sxs-lookup"><span data-stu-id="d97ae-361">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="d97ae-362">RestoreAdditionalProjectSources</span><span class="sxs-lookup"><span data-stu-id="d97ae-362">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="d97ae-363">Další zdroje, které se mají použít při obnovení.</span><span class="sxs-lookup"><span data-stu-id="d97ae-363">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="d97ae-364">RestoreAdditionalProjectFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="d97ae-364">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="d97ae-365">Další záložní složky, které se mají použít při obnovení</span><span class="sxs-lookup"><span data-stu-id="d97ae-365">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="d97ae-366">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="d97ae-366">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="d97ae-367">Vyloučí záložní složky zadané v`RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="d97ae-367">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="d97ae-368">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="d97ae-368">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="d97ae-369">Cesta k `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="d97ae-369">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="d97ae-370">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="d97ae-370">RestoreGraphProjectInput</span></span> | <span data-ttu-id="d97ae-371">Středníkem oddělený seznam projektů, které mají být obnoveny, které by měly obsahovat absolutní cesty.</span><span class="sxs-lookup"><span data-stu-id="d97ae-371">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="d97ae-372">RestoreUseSkipNonexistentTargets</span><span class="sxs-lookup"><span data-stu-id="d97ae-372">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="d97ae-373">Když jsou projekty shromažďovány pomocí nástroje MSBuild, určuje, zda jsou shromažďovány `SkipNonexistentTargets` pomocí optimalizace.</span><span class="sxs-lookup"><span data-stu-id="d97ae-373">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="d97ae-374">Pokud není nastaveno, výchozí hodnota `true`je.</span><span class="sxs-lookup"><span data-stu-id="d97ae-374">When not set, defaults to `true`.</span></span> <span data-ttu-id="d97ae-375">Příčinou je rychlé chování při selhání, když cíle projektu nelze importovat.</span><span class="sxs-lookup"><span data-stu-id="d97ae-375">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="d97ae-376">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="d97ae-376">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="d97ae-377">Výstupní složka, výchozí nastavení `BaseIntermediateOutputPath` `obj` a složka.</span><span class="sxs-lookup"><span data-stu-id="d97ae-377">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="d97ae-378">Příklady</span><span class="sxs-lookup"><span data-stu-id="d97ae-378">Examples</span></span>

<span data-ttu-id="d97ae-379">Příkazový řádek:</span><span class="sxs-lookup"><span data-stu-id="d97ae-379">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="d97ae-380">Soubor projektu:</span><span class="sxs-lookup"><span data-stu-id="d97ae-380">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="d97ae-381">Obnovit výstupy</span><span class="sxs-lookup"><span data-stu-id="d97ae-381">Restore outputs</span></span>

<span data-ttu-id="d97ae-382">Obnovení vytvoří ve složce buildu `obj` následující soubory:</span><span class="sxs-lookup"><span data-stu-id="d97ae-382">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="d97ae-383">Soubor</span><span class="sxs-lookup"><span data-stu-id="d97ae-383">File</span></span> | <span data-ttu-id="d97ae-384">Popis</span><span class="sxs-lookup"><span data-stu-id="d97ae-384">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="d97ae-385">Obsahuje graf závislostí všech odkazů na balíčky.</span><span class="sxs-lookup"><span data-stu-id="d97ae-385">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="d97ae-386">Odkazy na MSBuild props obsažená v balíčcích</span><span class="sxs-lookup"><span data-stu-id="d97ae-386">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="d97ae-387">Odkazy na cíle nástroje MSBuild obsažené v balíčcích</span><span class="sxs-lookup"><span data-stu-id="d97ae-387">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="d97ae-388">Obnovení a sestavování pomocí jednoho příkazu MSBuild</span><span class="sxs-lookup"><span data-stu-id="d97ae-388">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="d97ae-389">Vzhledem k tomu, že nástroj NuGet dokáže obnovit balíčky, které vycházejí z cílů a props nástroje MSBuild, jsou vyhodnocení obnovení a sestavení spouštěna s různými globálními vlastnostmi.</span><span class="sxs-lookup"><span data-stu-id="d97ae-389">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="d97ae-390">To znamená, že následující nastavení bude mít nepředvídatelné a často nesprávné chování.</span><span class="sxs-lookup"><span data-stu-id="d97ae-390">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="d97ae-391">Místo doporučeného přístupu:</span><span class="sxs-lookup"><span data-stu-id="d97ae-391">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="d97ae-392">Stejná logika platí pro jiné cíle podobné `build`.</span><span class="sxs-lookup"><span data-stu-id="d97ae-392">The same logic applies to other targets similar to `build`.</span></span>

### <a name="packagetargetfallback"></a><span data-ttu-id="d97ae-393">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="d97ae-393">PackageTargetFallback</span></span>

<span data-ttu-id="d97ae-394">`PackageTargetFallback` Element umožňuje zadat sadu kompatibilních cílů, které mají být použity při obnovení balíčků.</span><span class="sxs-lookup"><span data-stu-id="d97ae-394">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="d97ae-395">Je navržena tak, aby povolovala balíčkům, které používají dotnet [TxM](../reference/target-frameworks.md) pro práci s kompatibilními balíčky, které nedeklarují dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="d97ae-395">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="d97ae-396">To znamená, že pokud váš projekt používá dotnet TxM, pak všechny balíčky, na kterých závisí, musí mít také hodnotu dotnet TxM, pokud do projektu `<PackageTargetFallback>` nepřidáte, aby bylo možné, aby platformy, které nejsou dotnet, byly kompatibilní s dotnet.</span><span class="sxs-lookup"><span data-stu-id="d97ae-396">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="d97ae-397">Například pokud projekt používá `netstandard1.6` TxM a závislý balíček obsahuje pouze `lib/net45/a.dll` a `lib/portable-net45+win81/a.dll`, projekt se nepodaří sestavit.</span><span class="sxs-lookup"><span data-stu-id="d97ae-397">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="d97ae-398">Pokud je to, co chcete uvést, je druhá knihovna DLL, pak můžete přidat `PackageTargetFallback` tak, aby říkáme `portable-net45+win81` , že je knihovna DLL kompatibilní:</span><span class="sxs-lookup"><span data-stu-id="d97ae-398">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="d97ae-399">Chcete-li deklarovat zálohu pro všechny cíle v projektu, ponechte `Condition` atribut.</span><span class="sxs-lookup"><span data-stu-id="d97ae-399">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="d97ae-400">Můžete také všechny existující `PackageTargetFallback` `$(PackageTargetFallback)` , a to i tak, jak je znázorněno zde:</span><span class="sxs-lookup"><span data-stu-id="d97ae-400">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="d97ae-401">Nahrazení jedné knihovny z grafu obnovení</span><span class="sxs-lookup"><span data-stu-id="d97ae-401">Replacing one library from a restore graph</span></span>

<span data-ttu-id="d97ae-402">Pokud obnovení předává nesprávné sestavení, je možné vyřadit výchozí volbu balíčků a nahradit ji vlastní volbou.</span><span class="sxs-lookup"><span data-stu-id="d97ae-402">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="d97ae-403">Nejprve s nejvyšší úrovní `PackageReference`, vylučte všechny prostředky:</span><span class="sxs-lookup"><span data-stu-id="d97ae-403">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="d97ae-404">Dále přidejte vlastní odkaz na příslušnou místní kopii knihovny DLL:</span><span class="sxs-lookup"><span data-stu-id="d97ae-404">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
