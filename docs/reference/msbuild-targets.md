---
title: Sada NuGet Pack a obnovení jako cíle MSBuild
description: Sada NuGet Pack a obnovení může pracovat přímo jako cíle MSBuild s NuGet 4.0 +.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: d8d1b2ef0185381d16c1bb73035588fe90bcfd14
ms.sourcegitcommit: 9803981c90a1ed954dc11ed71731264c0e75ea0a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2019
ms.locfileid: "68959684"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="1b880-103">Sada NuGet Pack a obnovení jako cíle MSBuild</span><span class="sxs-lookup"><span data-stu-id="1b880-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="1b880-104">*NuGet 4.0 +*</span><span class="sxs-lookup"><span data-stu-id="1b880-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="1b880-105">Ve formátu [PackageReference](../consume-packages/package-references-in-project-files.md) NuGet 4.0 + může ukládat všechna metadata manifestu přímo do souboru projektu místo použití samostatného `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="1b880-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="1b880-106">Pomocí nástroje MSBuild 15.1 + nástroj NuGet je také první třídou občana MSBuild s `pack` cíli `restore` a, jak je popsáno níže.</span><span class="sxs-lookup"><span data-stu-id="1b880-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="1b880-107">Tyto cíle vám umožňují pracovat s balíčky NuGet stejně jako s ostatními úlohami nebo cíli MSBuild.</span><span class="sxs-lookup"><span data-stu-id="1b880-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="1b880-108">Pokyny k vytvoření balíčku NuGet pomocí nástroje MSBuild najdete v tématu [Vytvoření balíčku NuGet pomocí nástroje MSBuild](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="1b880-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="1b880-109">(Pro NuGet 3. x a starší použijte místo toho příkazy [Pack](../reference/cli-reference/cli-ref-pack.md) a [obnovení](../reference/cli-reference/cli-ref-restore.md) prostřednictvím rozhraní příkazového řádku NuGet.)</span><span class="sxs-lookup"><span data-stu-id="1b880-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="1b880-110">Pořadí cílového sestavení</span><span class="sxs-lookup"><span data-stu-id="1b880-110">Target build order</span></span>

<span data-ttu-id="1b880-111">Vzhledem `pack` k `restore` tomu, že a jsou cíle nástroje MSBuild, můžete k nim přistupovat, abyste mohli vylepšit pracovní postup.</span><span class="sxs-lookup"><span data-stu-id="1b880-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="1b880-112">Řekněme například, že chcete po sbalení balíčku zkopírovat do sdílené síťové složky.</span><span class="sxs-lookup"><span data-stu-id="1b880-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="1b880-113">To lze provést přidáním následujícího do souboru projektu:</span><span class="sxs-lookup"><span data-stu-id="1b880-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="1b880-114">Podobně můžete napsat úlohu MSBuild, napsat vlastní cíl a využít vlastnosti NuGet v úloze MSBuild.</span><span class="sxs-lookup"><span data-stu-id="1b880-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="1b880-115">`$(OutputPath)`je relativní a očekává, že spouštíte příkaz z kořenového adresáře projektu.</span><span class="sxs-lookup"><span data-stu-id="1b880-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="1b880-116">cíl balíčku</span><span class="sxs-lookup"><span data-stu-id="1b880-116">pack target</span></span>

<span data-ttu-id="1b880-117">Pro .NET Standard projekty pomocí formátu PackageReference pomocí `msbuild -t:pack` kreslení vstupů ze souboru projektu, který se má použít při vytváření balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="1b880-117">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="1b880-118">Následující tabulka popisuje vlastnosti nástroje MSBuild, které lze přidat do souboru projektu v rámci prvního `<PropertyGroup>` uzlu.</span><span class="sxs-lookup"><span data-stu-id="1b880-118">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="1b880-119">Tyto úpravy můžete snadno upravit v aplikaci Visual Studio 2017 a novějším kliknutím pravým tlačítkem myši na projekt a výběrem možnosti **Upravit {PROJECT_NAME}** v místní nabídce.</span><span class="sxs-lookup"><span data-stu-id="1b880-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="1b880-120">Pro přehlednost je tabulka uspořádaná podle ekvivalentní vlastnosti v [ `.nuspec` souboru](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="1b880-120">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="1b880-121">Všimněte si, `Owners` že `Summary` nástroj MSBuild `.nuspec` nepodporuje vlastnosti a.</span><span class="sxs-lookup"><span data-stu-id="1b880-121">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="1b880-122">Hodnota atributu/NuSpec</span><span class="sxs-lookup"><span data-stu-id="1b880-122">Attribute/NuSpec Value</span></span> | <span data-ttu-id="1b880-123">Vlastnost MSBuild</span><span class="sxs-lookup"><span data-stu-id="1b880-123">MSBuild Property</span></span> | <span data-ttu-id="1b880-124">Výchozí</span><span class="sxs-lookup"><span data-stu-id="1b880-124">Default</span></span> | <span data-ttu-id="1b880-125">Poznámky</span><span class="sxs-lookup"><span data-stu-id="1b880-125">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="1b880-126">Id</span><span class="sxs-lookup"><span data-stu-id="1b880-126">Id</span></span> | <span data-ttu-id="1b880-127">PackageId</span><span class="sxs-lookup"><span data-stu-id="1b880-127">PackageId</span></span> | <span data-ttu-id="1b880-128">Doplňk</span><span class="sxs-lookup"><span data-stu-id="1b880-128">AssemblyName</span></span> | <span data-ttu-id="1b880-129">$ (AssemblyName) z MSBuild</span><span class="sxs-lookup"><span data-stu-id="1b880-129">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="1b880-130">Version</span><span class="sxs-lookup"><span data-stu-id="1b880-130">Version</span></span> | <span data-ttu-id="1b880-131">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="1b880-131">PackageVersion</span></span> | <span data-ttu-id="1b880-132">Version</span><span class="sxs-lookup"><span data-stu-id="1b880-132">Version</span></span> | <span data-ttu-id="1b880-133">To je semver kompatibilní, například "1.0.0", "1.0.0-beta" nebo "1.0.0-beta-00345"</span><span class="sxs-lookup"><span data-stu-id="1b880-133">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="1b880-134">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="1b880-134">VersionPrefix</span></span> | <span data-ttu-id="1b880-135">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="1b880-135">PackageVersionPrefix</span></span> | <span data-ttu-id="1b880-136">empty</span><span class="sxs-lookup"><span data-stu-id="1b880-136">empty</span></span> | <span data-ttu-id="1b880-137">Nastavení PackageVersion přepsání PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="1b880-137">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="1b880-138">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="1b880-138">VersionSuffix</span></span> | <span data-ttu-id="1b880-139">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="1b880-139">PackageVersionSuffix</span></span> | <span data-ttu-id="1b880-140">empty</span><span class="sxs-lookup"><span data-stu-id="1b880-140">empty</span></span> | <span data-ttu-id="1b880-141">$ (VersionSuffix) z MSBuild.</span><span class="sxs-lookup"><span data-stu-id="1b880-141">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="1b880-142">Nastavení PackageVersion přepsání PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="1b880-142">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="1b880-143">Autoři</span><span class="sxs-lookup"><span data-stu-id="1b880-143">Authors</span></span> | <span data-ttu-id="1b880-144">Autoři</span><span class="sxs-lookup"><span data-stu-id="1b880-144">Authors</span></span> | <span data-ttu-id="1b880-145">Uživatelské jméno aktuálního uživatele</span><span class="sxs-lookup"><span data-stu-id="1b880-145">Username of the current user</span></span> | |
| <span data-ttu-id="1b880-146">Vlastníka</span><span class="sxs-lookup"><span data-stu-id="1b880-146">Owners</span></span> | <span data-ttu-id="1b880-147">Není k dispozici</span><span class="sxs-lookup"><span data-stu-id="1b880-147">N/A</span></span> | <span data-ttu-id="1b880-148">Nepřítomno v NuSpec</span><span class="sxs-lookup"><span data-stu-id="1b880-148">Not present in NuSpec</span></span> | |
| <span data-ttu-id="1b880-149">Název</span><span class="sxs-lookup"><span data-stu-id="1b880-149">Title</span></span> | <span data-ttu-id="1b880-150">Název</span><span class="sxs-lookup"><span data-stu-id="1b880-150">Title</span></span> | <span data-ttu-id="1b880-151">PackageId</span><span class="sxs-lookup"><span data-stu-id="1b880-151">The PackageId</span></span>| |
| <span data-ttu-id="1b880-152">Popis</span><span class="sxs-lookup"><span data-stu-id="1b880-152">Description</span></span> | <span data-ttu-id="1b880-153">Popis</span><span class="sxs-lookup"><span data-stu-id="1b880-153">Description</span></span> | <span data-ttu-id="1b880-154">Popis balíčku</span><span class="sxs-lookup"><span data-stu-id="1b880-154">"Package Description"</span></span> | |
| <span data-ttu-id="1b880-155">Úprava</span><span class="sxs-lookup"><span data-stu-id="1b880-155">Copyright</span></span> | <span data-ttu-id="1b880-156">Úprava</span><span class="sxs-lookup"><span data-stu-id="1b880-156">Copyright</span></span> | <span data-ttu-id="1b880-157">empty</span><span class="sxs-lookup"><span data-stu-id="1b880-157">empty</span></span> | |
| <span data-ttu-id="1b880-158">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="1b880-158">RequireLicenseAcceptance</span></span> | <span data-ttu-id="1b880-159">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="1b880-159">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="1b880-160">false</span><span class="sxs-lookup"><span data-stu-id="1b880-160">false</span></span> | |
| <span data-ttu-id="1b880-161">průkaz</span><span class="sxs-lookup"><span data-stu-id="1b880-161">license</span></span> | <span data-ttu-id="1b880-162">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="1b880-162">PackageLicenseExpression</span></span> | <span data-ttu-id="1b880-163">empty</span><span class="sxs-lookup"><span data-stu-id="1b880-163">empty</span></span> | <span data-ttu-id="1b880-164">Odpovídá`<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="1b880-164">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="1b880-165">průkaz</span><span class="sxs-lookup"><span data-stu-id="1b880-165">license</span></span> | <span data-ttu-id="1b880-166">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="1b880-166">PackageLicenseFile</span></span> | <span data-ttu-id="1b880-167">empty</span><span class="sxs-lookup"><span data-stu-id="1b880-167">empty</span></span> | <span data-ttu-id="1b880-168">`<license type="file">`Odpovídá.</span><span class="sxs-lookup"><span data-stu-id="1b880-168">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="1b880-169">Je možné, že bude nutné explicitně sbalit soubor s odkazem na licenci.</span><span class="sxs-lookup"><span data-stu-id="1b880-169">You may need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="1b880-170">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="1b880-170">LicenseUrl</span></span> | <span data-ttu-id="1b880-171">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="1b880-171">PackageLicenseUrl</span></span> | <span data-ttu-id="1b880-172">empty</span><span class="sxs-lookup"><span data-stu-id="1b880-172">empty</span></span> | <span data-ttu-id="1b880-173">`licenseUrl`se už nepoužívá, použijte vlastnost PackageLicenseExpression nebo PackageLicenseFile.</span><span class="sxs-lookup"><span data-stu-id="1b880-173">`licenseUrl` is being deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="1b880-174">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="1b880-174">ProjectUrl</span></span> | <span data-ttu-id="1b880-175">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="1b880-175">PackageProjectUrl</span></span> | <span data-ttu-id="1b880-176">empty</span><span class="sxs-lookup"><span data-stu-id="1b880-176">empty</span></span> | |
| <span data-ttu-id="1b880-177">IconUrl</span><span class="sxs-lookup"><span data-stu-id="1b880-177">IconUrl</span></span> | <span data-ttu-id="1b880-178">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="1b880-178">PackageIconUrl</span></span> | <span data-ttu-id="1b880-179">empty</span><span class="sxs-lookup"><span data-stu-id="1b880-179">empty</span></span> | |
| <span data-ttu-id="1b880-180">Značky</span><span class="sxs-lookup"><span data-stu-id="1b880-180">Tags</span></span> | <span data-ttu-id="1b880-181">PackageTags</span><span class="sxs-lookup"><span data-stu-id="1b880-181">PackageTags</span></span> | <span data-ttu-id="1b880-182">empty</span><span class="sxs-lookup"><span data-stu-id="1b880-182">empty</span></span> | <span data-ttu-id="1b880-183">Značky jsou středníky odděleny středníkem.</span><span class="sxs-lookup"><span data-stu-id="1b880-183">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="1b880-184">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="1b880-184">ReleaseNotes</span></span> | <span data-ttu-id="1b880-185">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="1b880-185">PackageReleaseNotes</span></span> | <span data-ttu-id="1b880-186">empty</span><span class="sxs-lookup"><span data-stu-id="1b880-186">empty</span></span> | |
| <span data-ttu-id="1b880-187">Úložiště/adresa URL</span><span class="sxs-lookup"><span data-stu-id="1b880-187">Repository/Url</span></span> | <span data-ttu-id="1b880-188">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="1b880-188">RepositoryUrl</span></span> | <span data-ttu-id="1b880-189">empty</span><span class="sxs-lookup"><span data-stu-id="1b880-189">empty</span></span> | <span data-ttu-id="1b880-190">Adresa URL úložiště, která se používá k klonování nebo načtení zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="1b880-190">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="1b880-191">Případě *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="1b880-191">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="1b880-192">Úložiště/typ</span><span class="sxs-lookup"><span data-stu-id="1b880-192">Repository/Type</span></span> | <span data-ttu-id="1b880-193">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="1b880-193">RepositoryType</span></span> | <span data-ttu-id="1b880-194">empty</span><span class="sxs-lookup"><span data-stu-id="1b880-194">empty</span></span> | <span data-ttu-id="1b880-195">Typ úložiště</span><span class="sxs-lookup"><span data-stu-id="1b880-195">Repository type.</span></span> <span data-ttu-id="1b880-196">Příklady: *Git*, *TFS*.</span><span class="sxs-lookup"><span data-stu-id="1b880-196">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="1b880-197">Úložiště/větev</span><span class="sxs-lookup"><span data-stu-id="1b880-197">Repository/Branch</span></span> | <span data-ttu-id="1b880-198">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="1b880-198">RepositoryBranch</span></span> | <span data-ttu-id="1b880-199">empty</span><span class="sxs-lookup"><span data-stu-id="1b880-199">empty</span></span> | <span data-ttu-id="1b880-200">Volitelné informace o větvi úložiště</span><span class="sxs-lookup"><span data-stu-id="1b880-200">Optional repository branch information.</span></span> <span data-ttu-id="1b880-201">Pro zahrnutí této vlastnosti je nutné zadat také *RepositoryUrl* .</span><span class="sxs-lookup"><span data-stu-id="1b880-201">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="1b880-202">Příklad: *Master* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="1b880-202">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="1b880-203">Úložiště/potvrzení změn</span><span class="sxs-lookup"><span data-stu-id="1b880-203">Repository/Commit</span></span> | <span data-ttu-id="1b880-204">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="1b880-204">RepositoryCommit</span></span> | <span data-ttu-id="1b880-205">empty</span><span class="sxs-lookup"><span data-stu-id="1b880-205">empty</span></span> | <span data-ttu-id="1b880-206">Volitelné potvrzení změn úložiště nebo sada změn, které označují, na který zdroj byl balíček vytvořen.</span><span class="sxs-lookup"><span data-stu-id="1b880-206">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="1b880-207">Pro zahrnutí této vlastnosti je nutné zadat také *RepositoryUrl* .</span><span class="sxs-lookup"><span data-stu-id="1b880-207">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="1b880-208">Příklad: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="1b880-208">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="1b880-209">PackageType</span><span class="sxs-lookup"><span data-stu-id="1b880-209">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="1b880-210">Souhrn</span><span class="sxs-lookup"><span data-stu-id="1b880-210">Summary</span></span> | <span data-ttu-id="1b880-211">Není podporováno</span><span class="sxs-lookup"><span data-stu-id="1b880-211">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="1b880-212">cílové vstupy balení</span><span class="sxs-lookup"><span data-stu-id="1b880-212">pack target inputs</span></span>

- <span data-ttu-id="1b880-213">Ispackable nastavenou</span><span class="sxs-lookup"><span data-stu-id="1b880-213">IsPackable</span></span>
- <span data-ttu-id="1b880-214">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="1b880-214">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="1b880-215">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="1b880-215">PackageVersion</span></span>
- <span data-ttu-id="1b880-216">PackageId</span><span class="sxs-lookup"><span data-stu-id="1b880-216">PackageId</span></span>
- <span data-ttu-id="1b880-217">Autoři</span><span class="sxs-lookup"><span data-stu-id="1b880-217">Authors</span></span>
- <span data-ttu-id="1b880-218">Popis</span><span class="sxs-lookup"><span data-stu-id="1b880-218">Description</span></span>
- <span data-ttu-id="1b880-219">Úprava</span><span class="sxs-lookup"><span data-stu-id="1b880-219">Copyright</span></span>
- <span data-ttu-id="1b880-220">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="1b880-220">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="1b880-221">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="1b880-221">DevelopmentDependency</span></span>
- <span data-ttu-id="1b880-222">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="1b880-222">PackageLicenseExpression</span></span>
- <span data-ttu-id="1b880-223">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="1b880-223">PackageLicenseFile</span></span>
- <span data-ttu-id="1b880-224">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="1b880-224">PackageLicenseUrl</span></span>
- <span data-ttu-id="1b880-225">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="1b880-225">PackageProjectUrl</span></span>
- <span data-ttu-id="1b880-226">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="1b880-226">PackageIconUrl</span></span>
- <span data-ttu-id="1b880-227">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="1b880-227">PackageReleaseNotes</span></span>
- <span data-ttu-id="1b880-228">PackageTags</span><span class="sxs-lookup"><span data-stu-id="1b880-228">PackageTags</span></span>
- <span data-ttu-id="1b880-229">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="1b880-229">PackageOutputPath</span></span>
- <span data-ttu-id="1b880-230">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="1b880-230">IncludeSymbols</span></span>
- <span data-ttu-id="1b880-231">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="1b880-231">IncludeSource</span></span>
- <span data-ttu-id="1b880-232">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="1b880-232">PackageTypes</span></span>
- <span data-ttu-id="1b880-233">Nástroj</span><span class="sxs-lookup"><span data-stu-id="1b880-233">IsTool</span></span>
- <span data-ttu-id="1b880-234">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="1b880-234">RepositoryUrl</span></span>
- <span data-ttu-id="1b880-235">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="1b880-235">RepositoryType</span></span>
- <span data-ttu-id="1b880-236">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="1b880-236">RepositoryBranch</span></span>
- <span data-ttu-id="1b880-237">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="1b880-237">RepositoryCommit</span></span>
- <span data-ttu-id="1b880-238">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="1b880-238">NoPackageAnalysis</span></span>
- <span data-ttu-id="1b880-239">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="1b880-239">MinClientVersion</span></span>
- <span data-ttu-id="1b880-240">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="1b880-240">IncludeBuildOutput</span></span>
- <span data-ttu-id="1b880-241">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="1b880-241">IncludeContentInPack</span></span>
- <span data-ttu-id="1b880-242">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="1b880-242">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="1b880-243">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="1b880-243">ContentTargetFolders</span></span>
- <span data-ttu-id="1b880-244">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="1b880-244">NuspecFile</span></span>
- <span data-ttu-id="1b880-245">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="1b880-245">NuspecBasePath</span></span>
- <span data-ttu-id="1b880-246">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="1b880-246">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="1b880-247">scénáře sady Pack</span><span class="sxs-lookup"><span data-stu-id="1b880-247">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="1b880-248">Potlačit závislosti</span><span class="sxs-lookup"><span data-stu-id="1b880-248">Suppress dependencies</span></span>

<span data-ttu-id="1b880-249">Chcete-li potlačit závislosti balíčků z vygenerovaného `true` balíčku NuGet, nastavte `SuppressDependenciesWhenPacking` na to, které umožní přeskočí všechny závislosti ze generovaného souboru nupkg.</span><span class="sxs-lookup"><span data-stu-id="1b880-249">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="1b880-250">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="1b880-250">PackageIconUrl</span></span>

<span data-ttu-id="1b880-251">V rámci změny [problému NuGet 352](https://github.com/NuGet/Home/issues/352)se nakonec změní na `PackageIconUrl` `PackageIconUri` a může to být relativní cesta k souboru ikony, který bude zahrnutý v kořenu výsledného balíčku.</span><span class="sxs-lookup"><span data-stu-id="1b880-251">As part of the change for [NuGet Issue 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="1b880-252">Výstupní sestavení</span><span class="sxs-lookup"><span data-stu-id="1b880-252">Output assemblies</span></span>

<span data-ttu-id="1b880-253">`nuget pack`zkopíruje výstupní `.exe`soubory s příponami `.dll` `.xml` ,,`.winmd`,, a `.pri`. `.json`</span><span class="sxs-lookup"><span data-stu-id="1b880-253">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="1b880-254">Výstupní soubory, které jsou zkopírovány, závisí na tom, co `BuiltOutputProjectGroup` nástroj MSBuild poskytuje z cíle.</span><span class="sxs-lookup"><span data-stu-id="1b880-254">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="1b880-255">Existují dvě vlastnosti nástroje MSBuild, které lze použít v souboru projektu nebo na příkazovém řádku pro řízení, kde výstupní sestavení jdou:</span><span class="sxs-lookup"><span data-stu-id="1b880-255">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="1b880-256">`IncludeBuildOutput`: Logická hodnota, která určuje, zda mají být do balíčku zahrnuty výstupní sestavení sestavení.</span><span class="sxs-lookup"><span data-stu-id="1b880-256">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="1b880-257">`BuildOutputTargetFolder`: Určuje složku, do které se mají umístit výstupní sestavení.</span><span class="sxs-lookup"><span data-stu-id="1b880-257">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="1b880-258">Výstupní sestavení (a další výstupní soubory) se zkopírují do příslušných složek rozhraní.</span><span class="sxs-lookup"><span data-stu-id="1b880-258">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="1b880-259">Odkazy na balíčky</span><span class="sxs-lookup"><span data-stu-id="1b880-259">Package references</span></span>

<span data-ttu-id="1b880-260">Viz [odkazy na balíčky v souborech projektu](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="1b880-260">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="1b880-261">Odkazy na projekt a projekt</span><span class="sxs-lookup"><span data-stu-id="1b880-261">Project to project references</span></span>

<span data-ttu-id="1b880-262">Odkazy na projekt na projekt jsou ve výchozím nastavení považovány za odkazy na balíčky NuGet, například:</span><span class="sxs-lookup"><span data-stu-id="1b880-262">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="1b880-263">Do odkazu na projekt můžete také přidat následující metadata:</span><span class="sxs-lookup"><span data-stu-id="1b880-263">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="1b880-264">Zahrnutí obsahu do balíčku</span><span class="sxs-lookup"><span data-stu-id="1b880-264">Including content in a package</span></span>

<span data-ttu-id="1b880-265">Chcete-li zahrnout obsah, přidejte do existující `<Content>` položky metadata navíc.</span><span class="sxs-lookup"><span data-stu-id="1b880-265">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="1b880-266">Ve výchozím nastavení jsou všechny položky typu "obsah" zahrnuty do balíčku, Pokud nepřepíšete záznamy podobné následujícímu:</span><span class="sxs-lookup"><span data-stu-id="1b880-266">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="1b880-267">Ve výchozím nastavení je vše přidáno do kořenu `content` a `contentFiles\any\<target_framework>` složky v rámci balíčku a zachovává strukturu relativních složek, pokud nezadáte cestu k balíčku:</span><span class="sxs-lookup"><span data-stu-id="1b880-267">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="1b880-268">Pokud chcete kopírovat veškerý obsah pouze na konkrétní kořenové složky (místo `content` a `contentFiles` obojí), můžete použít vlastnost `ContentTargetFolders`MSBuild, která má výchozí hodnotu Content; contentFiles, ale lze ji nastavit na jiné názvy složek.</span><span class="sxs-lookup"><span data-stu-id="1b880-268">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="1b880-269">Všimněte si, že pouze zadání "contentFiles `ContentTargetFolders` " v `contentFiles\any\<target_framework>` souboru vloží `contentFiles\<language>\<target_framework>` soubory do `buildAction`nebo na základě.</span><span class="sxs-lookup"><span data-stu-id="1b880-269">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="1b880-270">`PackagePath`může se jednat o sadu cílových cest oddělených středníky.</span><span class="sxs-lookup"><span data-stu-id="1b880-270">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="1b880-271">Zadáním prázdné cesty k balíčku by se soubor přidal do kořenového adresáře balíčku.</span><span class="sxs-lookup"><span data-stu-id="1b880-271">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="1b880-272">Například následující příkaz přidá `libuv.txt` do `content\myfiles`, `content\samples`a kořenovou složku balíčku:</span><span class="sxs-lookup"><span data-stu-id="1b880-272">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="1b880-273">K dispozici je také vlastnost `$(IncludeContentInPack)`MSBuild, která má `true`výchozí hodnotu.</span><span class="sxs-lookup"><span data-stu-id="1b880-273">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="1b880-274">Pokud je nastavená `false` na libovolný projekt, pak obsah z tohoto projektu není zahrnutý v balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="1b880-274">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="1b880-275">Další metadata specifická pro sadu, která můžete nastavit na kterékoli z výše uvedených položek ```<PackageCopyToOutput>``` , ```<PackageFlatten>``` zahrnují a ```CopyToOutput``` které ```Flatten``` ```contentFiles``` sady a hodnoty pro položku ve výstupních nuspec.</span><span class="sxs-lookup"><span data-stu-id="1b880-275">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="1b880-276">Kromě položek `<Pack>` obsahu lze metadata a `<PackagePath>` také nastavit na soubory s akcí sestavení kompilovat, EmbeddedResource, ApplicationDefinition, Page, Resource, třídy SplashScreen, vazbě designdata, DesignDataWithDesignTimeCreateableTypes , CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource nebo None.</span><span class="sxs-lookup"><span data-stu-id="1b880-276">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="1b880-277">Pokud má balíček při použití vzorů expanze názvů připojit název souboru k cestě k balíčku, musí cesta k balíčku končit znakem oddělovače složky. v opačném případě se cesta k balíčku považuje za úplnou cestu včetně názvu souboru.</span><span class="sxs-lookup"><span data-stu-id="1b880-277">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="1b880-278">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="1b880-278">IncludeSymbols</span></span>

<span data-ttu-id="1b880-279">Při použití `MSBuild -t:pack -p:IncludeSymbols=true`se zkopírují `.pdb` odpovídající soubory spolu s jinými výstupními `.xml`soubory (`.dll`, `.exe`, `.winmd`,, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="1b880-279">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="1b880-280">Všimněte si, `IncludeSymbols=true` že nastavení vytvoří regulární balíček *a* balíček symbolů.</span><span class="sxs-lookup"><span data-stu-id="1b880-280">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="1b880-281">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="1b880-281">IncludeSource</span></span>

<span data-ttu-id="1b880-282">To je stejné jako `IncludeSymbols`s tím rozdílem, že kopíruje také zdrojové soubory spolu se `.pdb` soubory.</span><span class="sxs-lookup"><span data-stu-id="1b880-282">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="1b880-283">Všechny soubory typu `Compile` jsou zkopírovány za účelem `src\<ProjectName>\` zachování struktury složek relativní cesty ve výsledném balíčku.</span><span class="sxs-lookup"><span data-stu-id="1b880-283">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="1b880-284">Totéž se také stane u zdrojových souborů, `ProjectReference` které mají `TreatAsPackageReference` nastavené na `false`.</span><span class="sxs-lookup"><span data-stu-id="1b880-284">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="1b880-285">Pokud je soubor typu Compile mimo složku projektu, pak je pouze přidán do `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="1b880-285">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="1b880-286">Balení licenčního výrazu nebo licenčního souboru</span><span class="sxs-lookup"><span data-stu-id="1b880-286">Packing a license expression or a license file</span></span>

<span data-ttu-id="1b880-287">Při použití licenčního výrazu by se měla použít vlastnost PackageLicenseExpression.</span><span class="sxs-lookup"><span data-stu-id="1b880-287">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="1b880-288">[Ukázka licenčního výrazu](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="1b880-288">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="1b880-289">[Přečtěte si další informace o výrazech licencí a licencích, které jsou přijaty nástrojem NuGet.org](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="1b880-289">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="1b880-290">Při balení licenčního souboru musíte použít vlastnost PackageLicenseFile a zadat cestu k balíčku relativní ke kořenu balíčku.</span><span class="sxs-lookup"><span data-stu-id="1b880-290">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="1b880-291">Kromě toho je nutné zajistit, aby byl soubor zahrnut do balíčku.</span><span class="sxs-lookup"><span data-stu-id="1b880-291">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="1b880-292">Příklad:</span><span class="sxs-lookup"><span data-stu-id="1b880-292">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```
<span data-ttu-id="1b880-293">[Ukázka licenčního souboru](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="1b880-293">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="1b880-294">Nástroj</span><span class="sxs-lookup"><span data-stu-id="1b880-294">IsTool</span></span>

<span data-ttu-id="1b880-295">Při použití `MSBuild -t:pack -p:IsTool=true`aplikace `lib` `tools` jsou všechny výstupní soubory, jak je uvedeno ve scénáři [výstup sestavení](#output-assemblies) , zkopírovány do složky namísto složky.</span><span class="sxs-lookup"><span data-stu-id="1b880-295">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="1b880-296">Všimněte si, že se liší od `DotNetCliTool` a, který je určen `PackageType` nastavením v `.csproj` souboru.</span><span class="sxs-lookup"><span data-stu-id="1b880-296">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="1b880-297">Balení pomocí. nuspec</span><span class="sxs-lookup"><span data-stu-id="1b880-297">Packing using a .nuspec</span></span>

<span data-ttu-id="1b880-298">I když se místo toho doporučuje [Zahrnout všechny vlastnosti](../reference/msbuild-targets.md#pack-target) , které jsou obvykle v `.nuspec` souboru v souboru projektu, můžete `.nuspec` zvolit použití souboru k balení projektu.</span><span class="sxs-lookup"><span data-stu-id="1b880-298">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="1b880-299">Pro projekt bez sady SDK, který používá `PackageReference`, je nutné importovat `NuGet.Build.Tasks.Pack.targets` , aby bylo možné spustit úlohu balíčku.</span><span class="sxs-lookup"><span data-stu-id="1b880-299">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="1b880-300">Před zabalením souboru nuspec je ještě nutné projekt obnovit.</span><span class="sxs-lookup"><span data-stu-id="1b880-300">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="1b880-301">(Projekt ve stylu sady SDK obsahuje cíle balíčku ve výchozím nastavení.)</span><span class="sxs-lookup"><span data-stu-id="1b880-301">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="1b880-302">Cílová architektura souboru projektu je nerelevantní a při balení nuspec se nepoužívá.</span><span class="sxs-lookup"><span data-stu-id="1b880-302">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="1b880-303">Následující tři vlastnosti MSBuild jsou relevantní pro balení pomocí `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="1b880-303">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="1b880-304">`NuspecFile`: relativní nebo absolutní cesta k `.nuspec` souboru, který se používá k balení.</span><span class="sxs-lookup"><span data-stu-id="1b880-304">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="1b880-305">`NuspecProperties`: středníkem oddělený seznam dvojic klíč = hodnota.</span><span class="sxs-lookup"><span data-stu-id="1b880-305">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="1b880-306">Kvůli způsobu, jakým funguje analýza příkazového řádku nástroje MSBuild, je nutné zadat více vlastností následujícím `-p:NuspecProperties=\"key1=value1;key2=value2\"`způsobem:.</span><span class="sxs-lookup"><span data-stu-id="1b880-306">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="1b880-307">`NuspecBasePath`: Základní cesta k `.nuspec` souboru</span><span class="sxs-lookup"><span data-stu-id="1b880-307">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="1b880-308">Pokud používáte `dotnet.exe` k balení projektu, použijte příkaz podobný následujícímu:</span><span class="sxs-lookup"><span data-stu-id="1b880-308">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="1b880-309">Při použití nástroje MSBuild k sbalení projektu použijte příkaz podobný následujícímu:</span><span class="sxs-lookup"><span data-stu-id="1b880-309">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="1b880-310">Všimněte si, že balení nuspec pomocí příkazu dotnet. exe nebo MSBuild také vede k sestavení projektu ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="1b880-310">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="1b880-311">K tomu je možné se vyhnout předáním ```--no-build``` vlastnosti do příkazu dotnet. exe, který je ekvivalentem nastavení ```<NoBuild>true</NoBuild> ``` v souboru projektu společně s nastavením ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="1b880-311">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="1b880-312">Příkladem souboru *. csproj* pro zabalení souboru nuspec je:</span><span class="sxs-lookup"><span data-stu-id="1b880-312">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="1b880-313">Rozšířené body rozšíření pro vytvoření přizpůsobeného balíčku</span><span class="sxs-lookup"><span data-stu-id="1b880-313">Advanced extension points to create customized package</span></span>

<span data-ttu-id="1b880-314">`pack` Cíl poskytuje dva Rozšiřovací body, které jsou spuštěny v sestavení specifickém pro vnitřní, cílové rozhraní.</span><span class="sxs-lookup"><span data-stu-id="1b880-314">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="1b880-315">Rozšiřující body podporují obsah a sestavení konkrétního cílového rozhraní do balíčku:</span><span class="sxs-lookup"><span data-stu-id="1b880-315">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="1b880-316">`TargetsForTfmSpecificBuildOutput`cílové Používá se pro soubory uvnitř `lib` složky nebo složky zadané pomocí. `BuildOutputTargetFolder`</span><span class="sxs-lookup"><span data-stu-id="1b880-316">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="1b880-317">`TargetsForTfmSpecificContentInPackage`cílové Použít pro soubory mimo `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="1b880-317">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="1b880-318">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="1b880-318">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="1b880-319">Napište vlastní cíl a zadejte ho jako hodnotu `$(TargetsForTfmSpecificBuildOutput)` vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="1b880-319">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="1b880-320">Pro všechny soubory, které potřebují přejít do `BuildOutputTargetFolder` nástroje (ve výchozím nastavení lib), by měl cíl zapisovat tyto soubory do skupiny `BuildOutputInPackage` Item a nastavit následující dvě hodnoty metadat:</span><span class="sxs-lookup"><span data-stu-id="1b880-320">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="1b880-321">`FinalOutputPath`: Absolutní cesta k souboru; Pokud není zadaný, použije se identita k vyhodnocení zdrojové cesty.</span><span class="sxs-lookup"><span data-stu-id="1b880-321">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="1b880-322">`TargetPath`:  Volitelné Nastavte, kdy soubor musí přejít do podsložky v rámci `lib\<TargetFramework>` , podobně jako satelitní sestavení, která se nacházejí v odpovídajících složkách kultury.</span><span class="sxs-lookup"><span data-stu-id="1b880-322">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="1b880-323">Výchozí hodnota je název souboru.</span><span class="sxs-lookup"><span data-stu-id="1b880-323">Defaults to the name of the file.</span></span>

<span data-ttu-id="1b880-324">Příklad:</span><span class="sxs-lookup"><span data-stu-id="1b880-324">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="1b880-325">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="1b880-325">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="1b880-326">Napište vlastní cíl a zadejte ho jako hodnotu `$(TargetsForTfmSpecificContentInPackage)` vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="1b880-326">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="1b880-327">U všech souborů, které se mají zahrnout do balíčku, by měl cíl tyto soubory zapsat do skupiny `TfmSpecificPackageFile` položek a nastavit následující volitelná metadata:</span><span class="sxs-lookup"><span data-stu-id="1b880-327">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="1b880-328">`PackagePath`: Cesta, kde by měl být v balíčku výstup souboru.</span><span class="sxs-lookup"><span data-stu-id="1b880-328">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="1b880-329">Při přidání více než jednoho souboru do stejné cesty k balíčku vyvolá NuGet vystavení upozornění.</span><span class="sxs-lookup"><span data-stu-id="1b880-329">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="1b880-330">`BuildAction`: Akce sestavení, která se má přiřadit k souboru, se vyžaduje jenom v případě, že je `contentFiles` cesta k balíčku ve složce.</span><span class="sxs-lookup"><span data-stu-id="1b880-330">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="1b880-331">Výchozí hodnota je None.</span><span class="sxs-lookup"><span data-stu-id="1b880-331">Defaults to "None".</span></span>

<span data-ttu-id="1b880-332">Příklad:</span><span class="sxs-lookup"><span data-stu-id="1b880-332">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="1b880-333">cíl obnovení</span><span class="sxs-lookup"><span data-stu-id="1b880-333">restore target</span></span>

<span data-ttu-id="1b880-334">`MSBuild -t:restore`(které `nuget restore` a `dotnet restore` používají se v projektech .NET Core), obnoví balíčky, na které se odkazuje v souboru projektu, takto:</span><span class="sxs-lookup"><span data-stu-id="1b880-334">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="1b880-335">Číst všechny odkazy z projektu na projekt</span><span class="sxs-lookup"><span data-stu-id="1b880-335">Read all project to project references</span></span>
1. <span data-ttu-id="1b880-336">Přečtěte si vlastnosti projektu a najděte mezilehlé složky a cílová rozhraní.</span><span class="sxs-lookup"><span data-stu-id="1b880-336">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="1b880-337">Předání dat nástroje MSBuild do NuGet. Build. Tasks. dll</span><span class="sxs-lookup"><span data-stu-id="1b880-337">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="1b880-338">Spustit obnovení</span><span class="sxs-lookup"><span data-stu-id="1b880-338">Run restore</span></span>
1. <span data-ttu-id="1b880-339">Stáhnout balíčky</span><span class="sxs-lookup"><span data-stu-id="1b880-339">Download packages</span></span>
1. <span data-ttu-id="1b880-340">Zápis souboru prostředků, cílů a vlastností props</span><span class="sxs-lookup"><span data-stu-id="1b880-340">Write assets file, targets, and props</span></span>

<span data-ttu-id="1b880-341">Cíl funguje pouze pro projekty, které používají formát PackageReference. `restore`</span><span class="sxs-lookup"><span data-stu-id="1b880-341">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="1b880-342">Nefunguje pro projekty používající `packages.config` formát. místo toho použijte [obnovení NuGet](../reference/cli-reference/cli-ref-restore.md) .</span><span class="sxs-lookup"><span data-stu-id="1b880-342">It does **not** work for projects using the `packages.config` format; use [nuget restore](../reference/cli-reference/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="1b880-343">Obnovit vlastnosti</span><span class="sxs-lookup"><span data-stu-id="1b880-343">Restore properties</span></span>

<span data-ttu-id="1b880-344">Další nastavení obnovení může pocházet z vlastností MSBuild v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="1b880-344">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="1b880-345">Hodnoty lze také nastavit z příkazového řádku pomocí `-p:` přepínače (viz příklady níže).</span><span class="sxs-lookup"><span data-stu-id="1b880-345">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="1b880-346">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="1b880-346">Property</span></span> | <span data-ttu-id="1b880-347">Popis</span><span class="sxs-lookup"><span data-stu-id="1b880-347">Description</span></span> |
|--------|--------|
| <span data-ttu-id="1b880-348">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="1b880-348">RestoreSources</span></span> | <span data-ttu-id="1b880-349">Seznam zdrojů balíčků oddělených středníkem.</span><span class="sxs-lookup"><span data-stu-id="1b880-349">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="1b880-350">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="1b880-350">RestorePackagesPath</span></span> | <span data-ttu-id="1b880-351">Cesta ke složce uživatelských balíčků</span><span class="sxs-lookup"><span data-stu-id="1b880-351">User packages folder path.</span></span> |
| <span data-ttu-id="1b880-352">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="1b880-352">RestoreDisableParallel</span></span> | <span data-ttu-id="1b880-353">Omezit stahování na jednu po druhé.</span><span class="sxs-lookup"><span data-stu-id="1b880-353">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="1b880-354">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="1b880-354">RestoreConfigFile</span></span> | <span data-ttu-id="1b880-355">Cesta k `Nuget.Config` souboru, který se má použít</span><span class="sxs-lookup"><span data-stu-id="1b880-355">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="1b880-356">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="1b880-356">RestoreNoCache</span></span> | <span data-ttu-id="1b880-357">Je-li nastavena hodnota true, nepoužívejte balíčky uložené v mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="1b880-357">If true, avoids using cached packages.</span></span> <span data-ttu-id="1b880-358">Viz [Správa globálních balíčků a složek mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="1b880-358">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="1b880-359">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="1b880-359">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="1b880-360">Pokud má hodnotu true, ignoruje neúspěšné nebo chybějící zdroje balíčků.</span><span class="sxs-lookup"><span data-stu-id="1b880-360">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="1b880-361">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="1b880-361">RestoreFallbackFolders</span></span> | <span data-ttu-id="1b880-362">Záložní složky používané ve stejném způsobu, jakým se používá složka uživatelských balíčků.</span><span class="sxs-lookup"><span data-stu-id="1b880-362">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="1b880-363">RestoreAdditionalProjectSources</span><span class="sxs-lookup"><span data-stu-id="1b880-363">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="1b880-364">Další zdroje, které se mají použít při obnovení.</span><span class="sxs-lookup"><span data-stu-id="1b880-364">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="1b880-365">RestoreAdditionalProjectFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="1b880-365">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="1b880-366">Další záložní složky, které se mají použít při obnovení</span><span class="sxs-lookup"><span data-stu-id="1b880-366">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="1b880-367">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="1b880-367">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="1b880-368">Vyloučí záložní složky zadané v`RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="1b880-368">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="1b880-369">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="1b880-369">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="1b880-370">Cesta k `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="1b880-370">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="1b880-371">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="1b880-371">RestoreGraphProjectInput</span></span> | <span data-ttu-id="1b880-372">Středníkem oddělený seznam projektů, které mají být obnoveny, které by měly obsahovat absolutní cesty.</span><span class="sxs-lookup"><span data-stu-id="1b880-372">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="1b880-373">RestoreUseSkipNonexistentTargets</span><span class="sxs-lookup"><span data-stu-id="1b880-373">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="1b880-374">Když jsou projekty shromažďovány pomocí nástroje MSBuild, určuje, zda jsou shromažďovány `SkipNonexistentTargets` pomocí optimalizace.</span><span class="sxs-lookup"><span data-stu-id="1b880-374">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="1b880-375">Pokud není nastaveno, výchozí hodnota `true`je.</span><span class="sxs-lookup"><span data-stu-id="1b880-375">When not set, defaults to `true`.</span></span> <span data-ttu-id="1b880-376">Příčinou je rychlé chování při selhání, když cíle projektu nelze importovat.</span><span class="sxs-lookup"><span data-stu-id="1b880-376">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="1b880-377">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="1b880-377">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="1b880-378">Výstupní složka, výchozí nastavení `BaseIntermediateOutputPath` `obj` a složka.</span><span class="sxs-lookup"><span data-stu-id="1b880-378">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="1b880-379">Příklady</span><span class="sxs-lookup"><span data-stu-id="1b880-379">Examples</span></span>

<span data-ttu-id="1b880-380">Příkazový řádek:</span><span class="sxs-lookup"><span data-stu-id="1b880-380">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="1b880-381">Soubor projektu:</span><span class="sxs-lookup"><span data-stu-id="1b880-381">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="1b880-382">Obnovit výstupy</span><span class="sxs-lookup"><span data-stu-id="1b880-382">Restore outputs</span></span>

<span data-ttu-id="1b880-383">Obnovení vytvoří ve složce buildu `obj` následující soubory:</span><span class="sxs-lookup"><span data-stu-id="1b880-383">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="1b880-384">Soubor</span><span class="sxs-lookup"><span data-stu-id="1b880-384">File</span></span> | <span data-ttu-id="1b880-385">Popis</span><span class="sxs-lookup"><span data-stu-id="1b880-385">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="1b880-386">Obsahuje graf závislostí všech odkazů na balíčky.</span><span class="sxs-lookup"><span data-stu-id="1b880-386">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="1b880-387">Odkazy na MSBuild props obsažená v balíčcích</span><span class="sxs-lookup"><span data-stu-id="1b880-387">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="1b880-388">Odkazy na cíle nástroje MSBuild obsažené v balíčcích</span><span class="sxs-lookup"><span data-stu-id="1b880-388">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="1b880-389">Obnovení a sestavování pomocí jednoho příkazu MSBuild</span><span class="sxs-lookup"><span data-stu-id="1b880-389">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="1b880-390">Vzhledem k tomu, že nástroj NuGet dokáže obnovit balíčky, které vycházejí z cílů a props nástroje MSBuild, jsou vyhodnocení obnovení a sestavení spouštěna s různými globálními vlastnostmi.</span><span class="sxs-lookup"><span data-stu-id="1b880-390">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="1b880-391">To znamená, že následující nastavení bude mít nepředvídatelné a často nesprávné chování.</span><span class="sxs-lookup"><span data-stu-id="1b880-391">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="1b880-392">Místo doporučeného přístupu:</span><span class="sxs-lookup"><span data-stu-id="1b880-392">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="1b880-393">Stejná logika platí pro jiné cíle podobné `build`.</span><span class="sxs-lookup"><span data-stu-id="1b880-393">The same logic applies to other targets similar to `build`.</span></span>

### <a name="packagetargetfallback"></a><span data-ttu-id="1b880-394">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="1b880-394">PackageTargetFallback</span></span>

<span data-ttu-id="1b880-395">`PackageTargetFallback` Element umožňuje zadat sadu kompatibilních cílů, které mají být použity při obnovení balíčků.</span><span class="sxs-lookup"><span data-stu-id="1b880-395">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="1b880-396">Je navržena tak, aby povolovala balíčkům, které používají dotnet [TxM](../reference/target-frameworks.md) pro práci s kompatibilními balíčky, které nedeklarují dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="1b880-396">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="1b880-397">To znamená, že pokud váš projekt používá dotnet TxM, pak všechny balíčky, na kterých závisí, musí mít také hodnotu dotnet TxM, pokud do projektu `<PackageTargetFallback>` nepřidáte, aby bylo možné, aby platformy, které nejsou dotnet, byly kompatibilní s dotnet.</span><span class="sxs-lookup"><span data-stu-id="1b880-397">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="1b880-398">Například pokud projekt používá `netstandard1.6` TxM a závislý balíček obsahuje pouze `lib/net45/a.dll` a `lib/portable-net45+win81/a.dll`, projekt se nepodaří sestavit.</span><span class="sxs-lookup"><span data-stu-id="1b880-398">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="1b880-399">Pokud je to, co chcete uvést, je druhá knihovna DLL, pak můžete přidat `PackageTargetFallback` tak, aby říkáme `portable-net45+win81` , že je knihovna DLL kompatibilní:</span><span class="sxs-lookup"><span data-stu-id="1b880-399">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="1b880-400">Chcete-li deklarovat zálohu pro všechny cíle v projektu, ponechte `Condition` atribut.</span><span class="sxs-lookup"><span data-stu-id="1b880-400">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="1b880-401">Můžete také všechny existující `PackageTargetFallback` `$(PackageTargetFallback)` , a to i tak, jak je znázorněno zde:</span><span class="sxs-lookup"><span data-stu-id="1b880-401">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="1b880-402">Nahrazení jedné knihovny z grafu obnovení</span><span class="sxs-lookup"><span data-stu-id="1b880-402">Replacing one library from a restore graph</span></span>

<span data-ttu-id="1b880-403">Pokud obnovení předává nesprávné sestavení, je možné vyřadit výchozí volbu balíčků a nahradit ji vlastní volbou.</span><span class="sxs-lookup"><span data-stu-id="1b880-403">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="1b880-404">Nejprve s nejvyšší úrovní `PackageReference`, vylučte všechny prostředky:</span><span class="sxs-lookup"><span data-stu-id="1b880-404">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="1b880-405">Dále přidejte vlastní odkaz na příslušnou místní kopii knihovny DLL:</span><span class="sxs-lookup"><span data-stu-id="1b880-405">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
