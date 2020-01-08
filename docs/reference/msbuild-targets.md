---
title: Sada NuGet Pack a obnovení jako cíle MSBuild
description: Sada NuGet Pack a obnovení může pracovat přímo jako cíle MSBuild s NuGet 4.0 +.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 2c2b5b21569e2644154670d502146f1e0f9c4c81
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/25/2019
ms.locfileid: "75385011"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="eea6d-103">Sada NuGet Pack a obnovení jako cíle MSBuild</span><span class="sxs-lookup"><span data-stu-id="eea6d-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="eea6d-104">*NuGet 4.0 +*</span><span class="sxs-lookup"><span data-stu-id="eea6d-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="eea6d-105">Ve formátu [PackageReference](../consume-packages/package-references-in-project-files.md) NuGet 4.0 + může ukládat všechna metadata manifestu přímo do souboru projektu místo použití samostatného souboru `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="eea6d-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="eea6d-106">Pomocí nástroje MSBuild 15.1 + nástroj NuGet je také první třídou občana MSBuild s `pack` a cíli `restore`, jak je popsáno níže.</span><span class="sxs-lookup"><span data-stu-id="eea6d-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="eea6d-107">Tyto cíle vám umožňují pracovat s balíčky NuGet stejně jako s ostatními úlohami nebo cíli MSBuild.</span><span class="sxs-lookup"><span data-stu-id="eea6d-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="eea6d-108">Pokyny k vytvoření balíčku NuGet pomocí nástroje MSBuild najdete v tématu [Vytvoření balíčku NuGet pomocí nástroje MSBuild](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="eea6d-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="eea6d-109">(Pro NuGet 3. x a starší použijte místo toho příkazy [Pack](../reference/cli-reference/cli-ref-pack.md) a [obnovení](../reference/cli-reference/cli-ref-restore.md) prostřednictvím rozhraní příkazového řádku NuGet.)</span><span class="sxs-lookup"><span data-stu-id="eea6d-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="eea6d-110">Pořadí cílového sestavení</span><span class="sxs-lookup"><span data-stu-id="eea6d-110">Target build order</span></span>

<span data-ttu-id="eea6d-111">Vzhledem k tomu, že `pack` a `restore` jsou cíle nástroje MSBuild, můžete k nim přistupovat, abyste mohli vylepšit pracovní postup.</span><span class="sxs-lookup"><span data-stu-id="eea6d-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="eea6d-112">Řekněme například, že chcete po sbalení balíčku zkopírovat do sdílené síťové složky.</span><span class="sxs-lookup"><span data-stu-id="eea6d-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="eea6d-113">To lze provést přidáním následujícího do souboru projektu:</span><span class="sxs-lookup"><span data-stu-id="eea6d-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="eea6d-114">Podobně můžete napsat úlohu MSBuild, napsat vlastní cíl a využít vlastnosti NuGet v úloze MSBuild.</span><span class="sxs-lookup"><span data-stu-id="eea6d-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="eea6d-115">`$(OutputPath)` je relativní a očekává, že spouštíte příkaz z kořenového adresáře projektu.</span><span class="sxs-lookup"><span data-stu-id="eea6d-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="eea6d-116">cíl balíčku</span><span class="sxs-lookup"><span data-stu-id="eea6d-116">pack target</span></span>

<span data-ttu-id="eea6d-117">Pro .NET Standard projekty pomocí formátu PackageReference pomocí `msbuild -t:pack` kreslí vstupy ze souboru projektu, které se použijí při vytváření balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="eea6d-117">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="eea6d-118">Následující tabulka popisuje vlastnosti MSBuild, které lze přidat do souboru projektu v prvním `<PropertyGroup>` uzlu.</span><span class="sxs-lookup"><span data-stu-id="eea6d-118">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="eea6d-119">Tyto úpravy můžete snadno upravit v aplikaci Visual Studio 2017 a novějším kliknutím pravým tlačítkem myši na projekt a výběrem možnosti **Upravit {PROJECT_NAME}** v místní nabídce.</span><span class="sxs-lookup"><span data-stu-id="eea6d-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="eea6d-120">Pro přehlednost je tabulka uspořádána podle odpovídající vlastnosti v [souboru`.nuspec`](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="eea6d-120">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="eea6d-121">Všimněte si, že nástroj MSBuild nepodporuje vlastnosti `Owners` a `Summary` z `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="eea6d-121">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="eea6d-122">Hodnota atributu/NuSpec</span><span class="sxs-lookup"><span data-stu-id="eea6d-122">Attribute/NuSpec Value</span></span> | <span data-ttu-id="eea6d-123">Vlastnost MSBuild</span><span class="sxs-lookup"><span data-stu-id="eea6d-123">MSBuild Property</span></span> | <span data-ttu-id="eea6d-124">Výchozí</span><span class="sxs-lookup"><span data-stu-id="eea6d-124">Default</span></span> | <span data-ttu-id="eea6d-125">Poznámky</span><span class="sxs-lookup"><span data-stu-id="eea6d-125">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="eea6d-126">Id</span><span class="sxs-lookup"><span data-stu-id="eea6d-126">Id</span></span> | <span data-ttu-id="eea6d-127">PackageId</span><span class="sxs-lookup"><span data-stu-id="eea6d-127">PackageId</span></span> | <span data-ttu-id="eea6d-128">Doplňk</span><span class="sxs-lookup"><span data-stu-id="eea6d-128">AssemblyName</span></span> | <span data-ttu-id="eea6d-129">$ (AssemblyName) z MSBuild</span><span class="sxs-lookup"><span data-stu-id="eea6d-129">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="eea6d-130">Version</span><span class="sxs-lookup"><span data-stu-id="eea6d-130">Version</span></span> | <span data-ttu-id="eea6d-131">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="eea6d-131">PackageVersion</span></span> | <span data-ttu-id="eea6d-132">Version</span><span class="sxs-lookup"><span data-stu-id="eea6d-132">Version</span></span> | <span data-ttu-id="eea6d-133">To je semver kompatibilní, například "1.0.0", "1.0.0-beta" nebo "1.0.0-beta-00345"</span><span class="sxs-lookup"><span data-stu-id="eea6d-133">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="eea6d-134">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="eea6d-134">VersionPrefix</span></span> | <span data-ttu-id="eea6d-135">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="eea6d-135">PackageVersionPrefix</span></span> | <span data-ttu-id="eea6d-136">empty</span><span class="sxs-lookup"><span data-stu-id="eea6d-136">empty</span></span> | <span data-ttu-id="eea6d-137">Nastavení PackageVersion přepsání PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="eea6d-137">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="eea6d-138">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="eea6d-138">VersionSuffix</span></span> | <span data-ttu-id="eea6d-139">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="eea6d-139">PackageVersionSuffix</span></span> | <span data-ttu-id="eea6d-140">empty</span><span class="sxs-lookup"><span data-stu-id="eea6d-140">empty</span></span> | <span data-ttu-id="eea6d-141">$ (VersionSuffix) z MSBuild.</span><span class="sxs-lookup"><span data-stu-id="eea6d-141">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="eea6d-142">Nastavení PackageVersion přepsání PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="eea6d-142">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="eea6d-143">Autoři</span><span class="sxs-lookup"><span data-stu-id="eea6d-143">Authors</span></span> | <span data-ttu-id="eea6d-144">Autoři</span><span class="sxs-lookup"><span data-stu-id="eea6d-144">Authors</span></span> | <span data-ttu-id="eea6d-145">Uživatelské jméno aktuálního uživatele</span><span class="sxs-lookup"><span data-stu-id="eea6d-145">Username of the current user</span></span> | |
| <span data-ttu-id="eea6d-146">Vlastníci</span><span class="sxs-lookup"><span data-stu-id="eea6d-146">Owners</span></span> | <span data-ttu-id="eea6d-147">NEUŽÍVÁ SE.</span><span class="sxs-lookup"><span data-stu-id="eea6d-147">N/A</span></span> | <span data-ttu-id="eea6d-148">Nepřítomno v NuSpec</span><span class="sxs-lookup"><span data-stu-id="eea6d-148">Not present in NuSpec</span></span> | |
| <span data-ttu-id="eea6d-149">Název</span><span class="sxs-lookup"><span data-stu-id="eea6d-149">Title</span></span> | <span data-ttu-id="eea6d-150">Název</span><span class="sxs-lookup"><span data-stu-id="eea6d-150">Title</span></span> | <span data-ttu-id="eea6d-151">PackageId</span><span class="sxs-lookup"><span data-stu-id="eea6d-151">The PackageId</span></span>| |
| <span data-ttu-id="eea6d-152">Popis</span><span class="sxs-lookup"><span data-stu-id="eea6d-152">Description</span></span> | <span data-ttu-id="eea6d-153">Popis</span><span class="sxs-lookup"><span data-stu-id="eea6d-153">Description</span></span> | <span data-ttu-id="eea6d-154">Popis balíčku</span><span class="sxs-lookup"><span data-stu-id="eea6d-154">"Package Description"</span></span> | |
| <span data-ttu-id="eea6d-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="eea6d-155">Copyright</span></span> | <span data-ttu-id="eea6d-156">Copyright</span><span class="sxs-lookup"><span data-stu-id="eea6d-156">Copyright</span></span> | <span data-ttu-id="eea6d-157">empty</span><span class="sxs-lookup"><span data-stu-id="eea6d-157">empty</span></span> | |
| <span data-ttu-id="eea6d-158">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="eea6d-158">RequireLicenseAcceptance</span></span> | <span data-ttu-id="eea6d-159">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="eea6d-159">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="eea6d-160">false</span><span class="sxs-lookup"><span data-stu-id="eea6d-160">false</span></span> | |
| <span data-ttu-id="eea6d-161">license</span><span class="sxs-lookup"><span data-stu-id="eea6d-161">license</span></span> | <span data-ttu-id="eea6d-162">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="eea6d-162">PackageLicenseExpression</span></span> | <span data-ttu-id="eea6d-163">empty</span><span class="sxs-lookup"><span data-stu-id="eea6d-163">empty</span></span> | <span data-ttu-id="eea6d-164">Odpovídá `<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="eea6d-164">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="eea6d-165">license</span><span class="sxs-lookup"><span data-stu-id="eea6d-165">license</span></span> | <span data-ttu-id="eea6d-166">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="eea6d-166">PackageLicenseFile</span></span> | <span data-ttu-id="eea6d-167">empty</span><span class="sxs-lookup"><span data-stu-id="eea6d-167">empty</span></span> | <span data-ttu-id="eea6d-168">Odpovídá `<license type="file">`.</span><span class="sxs-lookup"><span data-stu-id="eea6d-168">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="eea6d-169">Musíte explicitně sbalit soubor s odkazem na licenci.</span><span class="sxs-lookup"><span data-stu-id="eea6d-169">You need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="eea6d-170">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="eea6d-170">LicenseUrl</span></span> | <span data-ttu-id="eea6d-171">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="eea6d-171">PackageLicenseUrl</span></span> | <span data-ttu-id="eea6d-172">empty</span><span class="sxs-lookup"><span data-stu-id="eea6d-172">empty</span></span> | <span data-ttu-id="eea6d-173">`PackageLicenseUrl` je zastaralá, použijte vlastnost PackageLicenseExpression nebo PackageLicenseFile.</span><span class="sxs-lookup"><span data-stu-id="eea6d-173">`PackageLicenseUrl` is deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="eea6d-174">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="eea6d-174">ProjectUrl</span></span> | <span data-ttu-id="eea6d-175">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="eea6d-175">PackageProjectUrl</span></span> | <span data-ttu-id="eea6d-176">empty</span><span class="sxs-lookup"><span data-stu-id="eea6d-176">empty</span></span> | |
| <span data-ttu-id="eea6d-177">Ikona</span><span class="sxs-lookup"><span data-stu-id="eea6d-177">Icon</span></span> | <span data-ttu-id="eea6d-178">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="eea6d-178">PackageIcon</span></span> | <span data-ttu-id="eea6d-179">empty</span><span class="sxs-lookup"><span data-stu-id="eea6d-179">empty</span></span> | <span data-ttu-id="eea6d-180">Musíte explicitně sbalit soubor obrázku odkazované ikony.</span><span class="sxs-lookup"><span data-stu-id="eea6d-180">You need to explicitly pack the referenced icon image file.</span></span>|
| <span data-ttu-id="eea6d-181">IconUrl</span><span class="sxs-lookup"><span data-stu-id="eea6d-181">IconUrl</span></span> | <span data-ttu-id="eea6d-182">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="eea6d-182">PackageIconUrl</span></span> | <span data-ttu-id="eea6d-183">empty</span><span class="sxs-lookup"><span data-stu-id="eea6d-183">empty</span></span> | <span data-ttu-id="eea6d-184">Pro dosažení nejlepšího prostředí pro starší verze by měla být kromě `PackageIcon`určena `PackageIconUrl`.</span><span class="sxs-lookup"><span data-stu-id="eea6d-184">For the best downlevel experience, `PackageIconUrl` should be specified in addition to `PackageIcon`.</span></span> <span data-ttu-id="eea6d-185">Už se `PackageIconUrl` zastaralá.</span><span class="sxs-lookup"><span data-stu-id="eea6d-185">Longer term, `PackageIconUrl` will be deprecated.</span></span> |
| <span data-ttu-id="eea6d-186">Značky</span><span class="sxs-lookup"><span data-stu-id="eea6d-186">Tags</span></span> | <span data-ttu-id="eea6d-187">PackageTags</span><span class="sxs-lookup"><span data-stu-id="eea6d-187">PackageTags</span></span> | <span data-ttu-id="eea6d-188">empty</span><span class="sxs-lookup"><span data-stu-id="eea6d-188">empty</span></span> | <span data-ttu-id="eea6d-189">Značky jsou středníky odděleny středníkem.</span><span class="sxs-lookup"><span data-stu-id="eea6d-189">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="eea6d-190">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="eea6d-190">ReleaseNotes</span></span> | <span data-ttu-id="eea6d-191">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="eea6d-191">PackageReleaseNotes</span></span> | <span data-ttu-id="eea6d-192">empty</span><span class="sxs-lookup"><span data-stu-id="eea6d-192">empty</span></span> | |
| <span data-ttu-id="eea6d-193">Úložiště/adresa URL</span><span class="sxs-lookup"><span data-stu-id="eea6d-193">Repository/Url</span></span> | <span data-ttu-id="eea6d-194">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="eea6d-194">RepositoryUrl</span></span> | <span data-ttu-id="eea6d-195">empty</span><span class="sxs-lookup"><span data-stu-id="eea6d-195">empty</span></span> | <span data-ttu-id="eea6d-196">Adresa URL úložiště, která se používá k klonování nebo načtení zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="eea6d-196">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="eea6d-197">Příklad: *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="eea6d-197">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="eea6d-198">Úložiště/typ</span><span class="sxs-lookup"><span data-stu-id="eea6d-198">Repository/Type</span></span> | <span data-ttu-id="eea6d-199">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="eea6d-199">RepositoryType</span></span> | <span data-ttu-id="eea6d-200">empty</span><span class="sxs-lookup"><span data-stu-id="eea6d-200">empty</span></span> | <span data-ttu-id="eea6d-201">Typ úložiště</span><span class="sxs-lookup"><span data-stu-id="eea6d-201">Repository type.</span></span> <span data-ttu-id="eea6d-202">Příklady: *Git*, *TFS*.</span><span class="sxs-lookup"><span data-stu-id="eea6d-202">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="eea6d-203">Úložiště/větev</span><span class="sxs-lookup"><span data-stu-id="eea6d-203">Repository/Branch</span></span> | <span data-ttu-id="eea6d-204">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="eea6d-204">RepositoryBranch</span></span> | <span data-ttu-id="eea6d-205">empty</span><span class="sxs-lookup"><span data-stu-id="eea6d-205">empty</span></span> | <span data-ttu-id="eea6d-206">Volitelné informace o větvi úložiště</span><span class="sxs-lookup"><span data-stu-id="eea6d-206">Optional repository branch information.</span></span> <span data-ttu-id="eea6d-207">Pro zahrnutí této vlastnosti je nutné zadat také *RepositoryUrl* .</span><span class="sxs-lookup"><span data-stu-id="eea6d-207">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="eea6d-208">Příklad: *Master* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="eea6d-208">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="eea6d-209">Úložiště/potvrzení změn</span><span class="sxs-lookup"><span data-stu-id="eea6d-209">Repository/Commit</span></span> | <span data-ttu-id="eea6d-210">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="eea6d-210">RepositoryCommit</span></span> | <span data-ttu-id="eea6d-211">empty</span><span class="sxs-lookup"><span data-stu-id="eea6d-211">empty</span></span> | <span data-ttu-id="eea6d-212">Volitelné potvrzení změn úložiště nebo sada změn, které označují, na který zdroj byl balíček vytvořen.</span><span class="sxs-lookup"><span data-stu-id="eea6d-212">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="eea6d-213">Pro zahrnutí této vlastnosti je nutné zadat také *RepositoryUrl* .</span><span class="sxs-lookup"><span data-stu-id="eea6d-213">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="eea6d-214">Příklad: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="eea6d-214">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="eea6d-215">PackageType</span><span class="sxs-lookup"><span data-stu-id="eea6d-215">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="eea6d-216">Přehled</span><span class="sxs-lookup"><span data-stu-id="eea6d-216">Summary</span></span> | <span data-ttu-id="eea6d-217">Není podporováno</span><span class="sxs-lookup"><span data-stu-id="eea6d-217">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="eea6d-218">cílové vstupy balení</span><span class="sxs-lookup"><span data-stu-id="eea6d-218">pack target inputs</span></span>

- <span data-ttu-id="eea6d-219">Ispackable nastavenou</span><span class="sxs-lookup"><span data-stu-id="eea6d-219">IsPackable</span></span>
- <span data-ttu-id="eea6d-220">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="eea6d-220">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="eea6d-221">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="eea6d-221">PackageVersion</span></span>
- <span data-ttu-id="eea6d-222">PackageId</span><span class="sxs-lookup"><span data-stu-id="eea6d-222">PackageId</span></span>
- <span data-ttu-id="eea6d-223">Autoři</span><span class="sxs-lookup"><span data-stu-id="eea6d-223">Authors</span></span>
- <span data-ttu-id="eea6d-224">Popis</span><span class="sxs-lookup"><span data-stu-id="eea6d-224">Description</span></span>
- <span data-ttu-id="eea6d-225">Copyright</span><span class="sxs-lookup"><span data-stu-id="eea6d-225">Copyright</span></span>
- <span data-ttu-id="eea6d-226">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="eea6d-226">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="eea6d-227">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="eea6d-227">DevelopmentDependency</span></span>
- <span data-ttu-id="eea6d-228">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="eea6d-228">PackageLicenseExpression</span></span>
- <span data-ttu-id="eea6d-229">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="eea6d-229">PackageLicenseFile</span></span>
- <span data-ttu-id="eea6d-230">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="eea6d-230">PackageLicenseUrl</span></span>
- <span data-ttu-id="eea6d-231">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="eea6d-231">PackageProjectUrl</span></span>
- <span data-ttu-id="eea6d-232">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="eea6d-232">PackageIconUrl</span></span>
- <span data-ttu-id="eea6d-233">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="eea6d-233">PackageReleaseNotes</span></span>
- <span data-ttu-id="eea6d-234">PackageTags</span><span class="sxs-lookup"><span data-stu-id="eea6d-234">PackageTags</span></span>
- <span data-ttu-id="eea6d-235">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="eea6d-235">PackageOutputPath</span></span>
- <span data-ttu-id="eea6d-236">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="eea6d-236">IncludeSymbols</span></span>
- <span data-ttu-id="eea6d-237">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="eea6d-237">IncludeSource</span></span>
- <span data-ttu-id="eea6d-238">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="eea6d-238">PackageTypes</span></span>
- <span data-ttu-id="eea6d-239">Nástroj</span><span class="sxs-lookup"><span data-stu-id="eea6d-239">IsTool</span></span>
- <span data-ttu-id="eea6d-240">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="eea6d-240">RepositoryUrl</span></span>
- <span data-ttu-id="eea6d-241">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="eea6d-241">RepositoryType</span></span>
- <span data-ttu-id="eea6d-242">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="eea6d-242">RepositoryBranch</span></span>
- <span data-ttu-id="eea6d-243">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="eea6d-243">RepositoryCommit</span></span>
- <span data-ttu-id="eea6d-244">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="eea6d-244">NoPackageAnalysis</span></span>
- <span data-ttu-id="eea6d-245">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="eea6d-245">MinClientVersion</span></span>
- <span data-ttu-id="eea6d-246">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="eea6d-246">IncludeBuildOutput</span></span>
- <span data-ttu-id="eea6d-247">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="eea6d-247">IncludeContentInPack</span></span>
- <span data-ttu-id="eea6d-248">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="eea6d-248">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="eea6d-249">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="eea6d-249">ContentTargetFolders</span></span>
- <span data-ttu-id="eea6d-250">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="eea6d-250">NuspecFile</span></span>
- <span data-ttu-id="eea6d-251">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="eea6d-251">NuspecBasePath</span></span>
- <span data-ttu-id="eea6d-252">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="eea6d-252">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="eea6d-253">scénáře sady Pack</span><span class="sxs-lookup"><span data-stu-id="eea6d-253">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="eea6d-254">Potlačit závislosti</span><span class="sxs-lookup"><span data-stu-id="eea6d-254">Suppress dependencies</span></span>

<span data-ttu-id="eea6d-255">Chcete-li potlačit závislosti balíčků z generovaného balíčku NuGet, nastavte `SuppressDependenciesWhenPacking` na `true`, které umožní přeskočí všechny závislosti ze generovaného souboru nupkg.</span><span class="sxs-lookup"><span data-stu-id="eea6d-255">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="eea6d-256">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="eea6d-256">PackageIconUrl</span></span>

<span data-ttu-id="eea6d-257">místo nové vlastnosti [`PackageIcon`](#packageicon) `PackageIconUrl` bude zastaralá.</span><span class="sxs-lookup"><span data-stu-id="eea6d-257">`PackageIconUrl` will be deprecated in favor of the new [`PackageIcon`](#packageicon) property.</span></span>

<span data-ttu-id="eea6d-258">Počínaje verzí NuGet 5,3 & Visual Studio 2019 verze 16,3, `pack` vyvolá upozornění [NU5048](./errors-and-warnings/nu5048.md) , pokud metadata balíčku určují jenom `PackageIconUrl`.</span><span class="sxs-lookup"><span data-stu-id="eea6d-258">Starting with NuGet 5.3 & Visual Studio 2019 version 16.3, `pack` will raise [NU5048](./errors-and-warnings/nu5048.md) warning if the package metadata only specifies `PackageIconUrl`.</span></span>

### <a name="packageicon"></a><span data-ttu-id="eea6d-259">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="eea6d-259">PackageIcon</span></span>

> [!Tip]
> <span data-ttu-id="eea6d-260">Pro zajištění zpětné kompatibility se klienty a zdroji, které ještě nepodporují `PackageIcon`, byste měli zadat jak `PackageIcon`, tak `PackageIconUrl`.</span><span class="sxs-lookup"><span data-stu-id="eea6d-260">You should specify both `PackageIcon` and `PackageIconUrl` to maintain backward compatibility with clients and sources that do not yet support `PackageIcon`.</span></span> <span data-ttu-id="eea6d-261">Visual Studio bude podporovat `PackageIcon` pro balíčky ze zdroje založeného na složce v budoucí verzi.</span><span class="sxs-lookup"><span data-stu-id="eea6d-261">Visual Studio will support `PackageIcon` for packages coming from a folder-based source in a future release.</span></span>

#### <a name="packing-an-icon-image-file"></a><span data-ttu-id="eea6d-262">Balení souboru obrázku ikony</span><span class="sxs-lookup"><span data-stu-id="eea6d-262">Packing an icon image file</span></span>

<span data-ttu-id="eea6d-263">Při balení souboru obrázku ikony je nutné použít vlastnost `PackageIcon` a zadat cestu k balíčku relativní ke kořenu balíčku.</span><span class="sxs-lookup"><span data-stu-id="eea6d-263">When packing an icon image file, you need to use `PackageIcon` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="eea6d-264">Kromě toho je nutné zajistit, aby byl soubor zahrnut do balíčku.</span><span class="sxs-lookup"><span data-stu-id="eea6d-264">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="eea6d-265">Velikost souboru obrázku je omezená na 1 MB.</span><span class="sxs-lookup"><span data-stu-id="eea6d-265">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="eea6d-266">Podporované formáty souborů zahrnují JPEG a PNG.</span><span class="sxs-lookup"><span data-stu-id="eea6d-266">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="eea6d-267">Doporučujeme, abyste 64 × 64 rozlišení obrazu.</span><span class="sxs-lookup"><span data-stu-id="eea6d-267">We recommend an image resolution of 64x64.</span></span>

<span data-ttu-id="eea6d-268">Příklad:</span><span class="sxs-lookup"><span data-stu-id="eea6d-268">For example:</span></span>

```xml
<PropertyGroup>
    ...
    <PackageIcon>icon.png</PackageIcon>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="images\icon.png" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

<span data-ttu-id="eea6d-269">[Ukázka ikony balíčku](https://github.com/NuGet/Samples/tree/master/PackageIconExample)</span><span class="sxs-lookup"><span data-stu-id="eea6d-269">[Package Icon sample](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span></span>

<span data-ttu-id="eea6d-270">Pro ekvivalent nuspec se podívejte na [nuspec reference pro Icon](nuspec.md#icon).</span><span class="sxs-lookup"><span data-stu-id="eea6d-270">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="eea6d-271">Výstupní sestavení</span><span class="sxs-lookup"><span data-stu-id="eea6d-271">Output assemblies</span></span>

<span data-ttu-id="eea6d-272">`nuget pack` zkopíruje výstupní soubory s rozšířeními `.exe`, `.dll`, `.xml`, `.winmd`, `.json`a `.pri`.</span><span class="sxs-lookup"><span data-stu-id="eea6d-272">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="eea6d-273">Výstupní soubory, které jsou zkopírovány, závisí na tom, co nástroj MSBuild poskytuje z cíle `BuiltOutputProjectGroup`.</span><span class="sxs-lookup"><span data-stu-id="eea6d-273">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="eea6d-274">Existují dvě vlastnosti nástroje MSBuild, které lze použít v souboru projektu nebo na příkazovém řádku pro řízení, kde výstupní sestavení jdou:</span><span class="sxs-lookup"><span data-stu-id="eea6d-274">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="eea6d-275">`IncludeBuildOutput`: logická hodnota, která určuje, zda mají být do balíčku zahrnuty výstupní sestavení sestavení.</span><span class="sxs-lookup"><span data-stu-id="eea6d-275">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="eea6d-276">`BuildOutputTargetFolder`: Určuje složku, do které se mají umístit výstupní sestavení.</span><span class="sxs-lookup"><span data-stu-id="eea6d-276">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="eea6d-277">Výstupní sestavení (a další výstupní soubory) se zkopírují do příslušných složek rozhraní.</span><span class="sxs-lookup"><span data-stu-id="eea6d-277">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="eea6d-278">Odkazy na balíčky</span><span class="sxs-lookup"><span data-stu-id="eea6d-278">Package references</span></span>

<span data-ttu-id="eea6d-279">Viz [odkazy na balíčky v souborech projektu](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="eea6d-279">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="eea6d-280">Odkazy na projekt a projekt</span><span class="sxs-lookup"><span data-stu-id="eea6d-280">Project to project references</span></span>

<span data-ttu-id="eea6d-281">Odkazy na projekt na projekt jsou ve výchozím nastavení považovány za odkazy na balíčky NuGet, například:</span><span class="sxs-lookup"><span data-stu-id="eea6d-281">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="eea6d-282">Do odkazu na projekt můžete také přidat následující metadata:</span><span class="sxs-lookup"><span data-stu-id="eea6d-282">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="eea6d-283">Zahrnutí obsahu do balíčku</span><span class="sxs-lookup"><span data-stu-id="eea6d-283">Including content in a package</span></span>

<span data-ttu-id="eea6d-284">Chcete-li zahrnout obsah, přidejte do existující položky `<Content>` další metadata.</span><span class="sxs-lookup"><span data-stu-id="eea6d-284">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="eea6d-285">Ve výchozím nastavení jsou všechny položky typu "obsah" zahrnuty do balíčku, Pokud nepřepíšete záznamy podobné následujícímu:</span><span class="sxs-lookup"><span data-stu-id="eea6d-285">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="eea6d-286">Ve výchozím nastavení se vše přidá do kořenu `content` a `contentFiles\any\<target_framework>` složky v rámci balíčku a zachová relativní strukturu složek, pokud nezadáte cestu k balíčku:</span><span class="sxs-lookup"><span data-stu-id="eea6d-286">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="eea6d-287">Chcete-li zkopírovat veškerý obsah pouze do konkrétní kořenové složky (místo `content` a `contentFiles` obojí), můžete použít vlastnost MSBuild `ContentTargetFolders`, která má výchozí hodnotu "Content; contentFiles", ale lze ji nastavit na jiné názvy složek.</span><span class="sxs-lookup"><span data-stu-id="eea6d-287">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="eea6d-288">Všimněte si, že pouze zadání "contentFiles" v `ContentTargetFolders` vloží soubory do `contentFiles\any\<target_framework>` nebo `contentFiles\<language>\<target_framework>` na základě `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="eea6d-288">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="eea6d-289">`PackagePath` může být sada cílových cest oddělená středníky.</span><span class="sxs-lookup"><span data-stu-id="eea6d-289">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="eea6d-290">Zadáním prázdné cesty k balíčku by se soubor přidal do kořenového adresáře balíčku.</span><span class="sxs-lookup"><span data-stu-id="eea6d-290">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="eea6d-291">Například následující příkaz přidá `libuv.txt` do `content\myfiles`, `content\samples`a kořenového adresáře balíčku:</span><span class="sxs-lookup"><span data-stu-id="eea6d-291">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="eea6d-292">K dispozici je také vlastnost MSBuild `$(IncludeContentInPack)`, která má výchozí hodnotu `true`.</span><span class="sxs-lookup"><span data-stu-id="eea6d-292">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="eea6d-293">Pokud je toto nastavení nastaveno na `false` na jakémkoli projektu, pak obsah z tohoto projektu není součástí balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="eea6d-293">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="eea6d-294">Další metadata specifická pro sadu, která můžete nastavit na některou z výše uvedených položek, zahrnují ```<PackageCopyToOutput>``` a ```<PackageFlatten>```, které nastaví ```CopyToOutput``` a ```Flatten``` hodnoty na ```contentFiles``` položce ve výstupním nuspec.</span><span class="sxs-lookup"><span data-stu-id="eea6d-294">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="eea6d-295">Kromě položek obsahu lze metadata `<Pack>` a `<PackagePath>` také nastavit na soubory s akcí sestavení kompilovat, EmbeddedResource, ApplicationDefinition, Page, Resource, třídy SplashScreen, vazbě designdata, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource nebo None.</span><span class="sxs-lookup"><span data-stu-id="eea6d-295">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="eea6d-296">Pokud má balíček při použití vzorů expanze názvů připojit název souboru k cestě k balíčku, musí cesta k balíčku končit znakem oddělovače složky. v opačném případě se cesta k balíčku považuje za úplnou cestu včetně názvu souboru.</span><span class="sxs-lookup"><span data-stu-id="eea6d-296">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="eea6d-297">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="eea6d-297">IncludeSymbols</span></span>

<span data-ttu-id="eea6d-298">Při použití `MSBuild -t:pack -p:IncludeSymbols=true`se odpovídající soubory `.pdb` zkopírují spolu s jinými výstupními soubory (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="eea6d-298">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="eea6d-299">Všimněte si, že nastavení `IncludeSymbols=true` vytvoří regulární balíček *a* balíček symbolů.</span><span class="sxs-lookup"><span data-stu-id="eea6d-299">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="eea6d-300">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="eea6d-300">IncludeSource</span></span>

<span data-ttu-id="eea6d-301">To je stejné jako u `IncludeSymbols`s tím rozdílem, že kopíruje zdrojové soubory společně s `.pdb` soubory.</span><span class="sxs-lookup"><span data-stu-id="eea6d-301">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="eea6d-302">Všechny soubory typu `Compile` se zkopírují do `src\<ProjectName>\` zachovávání struktury složek relativní cesty ve výsledném balíčku.</span><span class="sxs-lookup"><span data-stu-id="eea6d-302">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="eea6d-303">Totéž se taky stane u zdrojových souborů `ProjectReference`, které mají `TreatAsPackageReference` nastavené na `false`.</span><span class="sxs-lookup"><span data-stu-id="eea6d-303">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="eea6d-304">Pokud je soubor typu kompilovat mimo složku projektu, pak je pouze přidán do `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="eea6d-304">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="eea6d-305">Balení licenčního výrazu nebo licenčního souboru</span><span class="sxs-lookup"><span data-stu-id="eea6d-305">Packing a license expression or a license file</span></span>

<span data-ttu-id="eea6d-306">Při použití licenčního výrazu by se měla použít vlastnost PackageLicenseExpression.</span><span class="sxs-lookup"><span data-stu-id="eea6d-306">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="eea6d-307">[Ukázka licenčního výrazu](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="eea6d-307">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="eea6d-308">[Přečtěte si další informace o výrazech licencí a licencích, které jsou přijaty nástrojem NuGet.org](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="eea6d-308">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="eea6d-309">Při balení licenčního souboru musíte použít vlastnost PackageLicenseFile a zadat cestu k balíčku relativní ke kořenu balíčku.</span><span class="sxs-lookup"><span data-stu-id="eea6d-309">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="eea6d-310">Kromě toho je nutné zajistit, aby byl soubor zahrnut do balíčku.</span><span class="sxs-lookup"><span data-stu-id="eea6d-310">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="eea6d-311">Příklad:</span><span class="sxs-lookup"><span data-stu-id="eea6d-311">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="eea6d-312">[Ukázka licenčního souboru](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="eea6d-312">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="eea6d-313">Nástroj</span><span class="sxs-lookup"><span data-stu-id="eea6d-313">IsTool</span></span>

<span data-ttu-id="eea6d-314">Při použití `MSBuild -t:pack -p:IsTool=true`se všechny výstupní soubory, jak je uvedeno ve scénáři [výstupních sestavení](#output-assemblies) , zkopírují do složky `tools` namísto složky `lib`.</span><span class="sxs-lookup"><span data-stu-id="eea6d-314">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="eea6d-315">Všimněte si, že se liší od `DotNetCliTool`, která je určena nastavením `PackageType` v souboru `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="eea6d-315">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="eea6d-316">Balení pomocí. nuspec</span><span class="sxs-lookup"><span data-stu-id="eea6d-316">Packing using a .nuspec</span></span>

<span data-ttu-id="eea6d-317">I když se místo toho doporučuje [Zahrnout všechny vlastnosti](../reference/msbuild-targets.md#pack-target) , které jsou obvykle v souboru `.nuspec` v souboru projektu, můžete zvolit použití `.nuspec` souboru k balení projektu.</span><span class="sxs-lookup"><span data-stu-id="eea6d-317">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="eea6d-318">Pro projekt bez sady SDK, který používá `PackageReference`, je nutné importovat `NuGet.Build.Tasks.Pack.targets`, aby bylo možné spustit úlohu balíčku.</span><span class="sxs-lookup"><span data-stu-id="eea6d-318">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="eea6d-319">Před zabalením souboru nuspec je ještě nutné projekt obnovit.</span><span class="sxs-lookup"><span data-stu-id="eea6d-319">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="eea6d-320">(Projekt ve stylu sady SDK obsahuje cíle balíčku ve výchozím nastavení.)</span><span class="sxs-lookup"><span data-stu-id="eea6d-320">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="eea6d-321">Cílová architektura souboru projektu je nerelevantní a při balení nuspec se nepoužívá.</span><span class="sxs-lookup"><span data-stu-id="eea6d-321">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="eea6d-322">Následující tři vlastnosti MSBuild jsou relevantní pro balení pomocí `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="eea6d-322">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="eea6d-323">`NuspecFile`: relativní nebo absolutní cesta k souboru `.nuspec`, který se používá pro balení.</span><span class="sxs-lookup"><span data-stu-id="eea6d-323">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="eea6d-324">`NuspecProperties`: středníkem oddělený seznam dvojic klíč = hodnota.</span><span class="sxs-lookup"><span data-stu-id="eea6d-324">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="eea6d-325">Kvůli způsobu, jakým funguje analýza příkazového řádku nástroje MSBuild, je nutné zadat více vlastností následujícím způsobem: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="eea6d-325">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="eea6d-326">`NuspecBasePath`: základní cesta k souboru `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="eea6d-326">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="eea6d-327">Při použití `dotnet.exe` k balení projektu použijte příkaz podobný následujícímu:</span><span class="sxs-lookup"><span data-stu-id="eea6d-327">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="eea6d-328">Při použití nástroje MSBuild k sbalení projektu použijte příkaz podobný následujícímu:</span><span class="sxs-lookup"><span data-stu-id="eea6d-328">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="eea6d-329">Všimněte si, že balení nuspec pomocí příkazu dotnet. exe nebo MSBuild také vede k sestavení projektu ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="eea6d-329">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="eea6d-330">K tomu je možné se vyhnout předáním vlastnosti ```--no-build``` příkazu dotnet. exe, který je ekvivalentem nastavení ```<NoBuild>true</NoBuild> ``` v souboru projektu společně s nastavením ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="eea6d-330">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="eea6d-331">Příkladem souboru *. csproj* pro zabalení souboru nuspec je:</span><span class="sxs-lookup"><span data-stu-id="eea6d-331">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="eea6d-332">Rozšířené body rozšíření pro vytvoření přizpůsobeného balíčku</span><span class="sxs-lookup"><span data-stu-id="eea6d-332">Advanced extension points to create customized package</span></span>

<span data-ttu-id="eea6d-333">`pack` cíl poskytuje dva Rozšiřovací body, které jsou spuštěny v sestavení specifickém pro vnitřní, cílové rozhraní.</span><span class="sxs-lookup"><span data-stu-id="eea6d-333">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="eea6d-334">Rozšiřující body podporují obsah a sestavení konkrétního cílového rozhraní do balíčku:</span><span class="sxs-lookup"><span data-stu-id="eea6d-334">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="eea6d-335">`TargetsForTfmSpecificBuildOutput` cíl: používá se pro soubory uvnitř `lib` složky nebo složky zadané pomocí `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="eea6d-335">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="eea6d-336">`TargetsForTfmSpecificContentInPackage` cíl: použít pro soubory mimo `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="eea6d-336">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="eea6d-337">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="eea6d-337">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="eea6d-338">Napište vlastní cíl a zadejte ho jako hodnotu vlastnosti `$(TargetsForTfmSpecificBuildOutput)`.</span><span class="sxs-lookup"><span data-stu-id="eea6d-338">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="eea6d-339">Pro všechny soubory, které potřebují přejít do `BuildOutputTargetFolder` (lib ve výchozím nastavení), by měl cíl tyto soubory zapsat do skupiny položek `BuildOutputInPackage` a nastavit následující dvě hodnoty metadat:</span><span class="sxs-lookup"><span data-stu-id="eea6d-339">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="eea6d-340">`FinalOutputPath`: absolutní cesta k souboru; Pokud není zadaný, použije se identita k vyhodnocení zdrojové cesty.</span><span class="sxs-lookup"><span data-stu-id="eea6d-340">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="eea6d-341">`TargetPath`: (volitelné) nastavte, když soubor potřebuje přejít do podsložky v rámci `lib\<TargetFramework>`, jako jsou satelitní sestavení, která se nacházejí v odpovídajících složkách kultury.</span><span class="sxs-lookup"><span data-stu-id="eea6d-341">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="eea6d-342">Výchozí hodnota je název souboru.</span><span class="sxs-lookup"><span data-stu-id="eea6d-342">Defaults to the name of the file.</span></span>

<span data-ttu-id="eea6d-343">Příklad:</span><span class="sxs-lookup"><span data-stu-id="eea6d-343">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="eea6d-344">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="eea6d-344">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="eea6d-345">Napište vlastní cíl a zadejte ho jako hodnotu vlastnosti `$(TargetsForTfmSpecificContentInPackage)`.</span><span class="sxs-lookup"><span data-stu-id="eea6d-345">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="eea6d-346">U všech souborů, které se mají zahrnout do balíčku, by měl cíl tyto soubory zapsat do skupiny položek `TfmSpecificPackageFile` a nastavit následující volitelná metadata:</span><span class="sxs-lookup"><span data-stu-id="eea6d-346">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="eea6d-347">`PackagePath`: cesta, kde by měl být v balíčku výstup souboru.</span><span class="sxs-lookup"><span data-stu-id="eea6d-347">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="eea6d-348">Při přidání více než jednoho souboru do stejné cesty k balíčku vyvolá NuGet vystavení upozornění.</span><span class="sxs-lookup"><span data-stu-id="eea6d-348">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="eea6d-349">`BuildAction`: akce sestavení, která se má přiřadit k souboru, se vyžaduje jenom v případě, že je cesta k balíčku ve složce `contentFiles`.</span><span class="sxs-lookup"><span data-stu-id="eea6d-349">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="eea6d-350">Výchozí hodnota je None.</span><span class="sxs-lookup"><span data-stu-id="eea6d-350">Defaults to "None".</span></span>

<span data-ttu-id="eea6d-351">Příklad:</span><span class="sxs-lookup"><span data-stu-id="eea6d-351">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="eea6d-352">cíl obnovení</span><span class="sxs-lookup"><span data-stu-id="eea6d-352">restore target</span></span>

<span data-ttu-id="eea6d-353">`MSBuild -t:restore` (které `nuget restore` a `dotnet restore` použít s projekty .NET Core), obnoví balíčky, na které se odkazuje v souboru projektu, takto:</span><span class="sxs-lookup"><span data-stu-id="eea6d-353">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="eea6d-354">Číst všechny odkazy z projektu na projekt</span><span class="sxs-lookup"><span data-stu-id="eea6d-354">Read all project to project references</span></span>
1. <span data-ttu-id="eea6d-355">Přečtěte si vlastnosti projektu a najděte mezilehlé složky a cílová rozhraní.</span><span class="sxs-lookup"><span data-stu-id="eea6d-355">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="eea6d-356">Předání dat nástroje MSBuild do NuGet. Build. Tasks. dll</span><span class="sxs-lookup"><span data-stu-id="eea6d-356">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="eea6d-357">Spustit obnovení</span><span class="sxs-lookup"><span data-stu-id="eea6d-357">Run restore</span></span>
1. <span data-ttu-id="eea6d-358">Stáhnout balíčky</span><span class="sxs-lookup"><span data-stu-id="eea6d-358">Download packages</span></span>
1. <span data-ttu-id="eea6d-359">Zápis souboru prostředků, cílů a vlastností props</span><span class="sxs-lookup"><span data-stu-id="eea6d-359">Write assets file, targets, and props</span></span>

<span data-ttu-id="eea6d-360">`restore` cíl funguje **pouze** pro projekty, které používají formát PackageReference.</span><span class="sxs-lookup"><span data-stu-id="eea6d-360">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="eea6d-361">Pro projekty **, které používají** formát `packages.config`, nefunguje. místo toho použijte [obnovení NuGet](../reference/cli-reference/cli-ref-restore.md) .</span><span class="sxs-lookup"><span data-stu-id="eea6d-361">It does **not** work for projects using the `packages.config` format; use [nuget restore](../reference/cli-reference/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="eea6d-362">Obnovit vlastnosti</span><span class="sxs-lookup"><span data-stu-id="eea6d-362">Restore properties</span></span>

<span data-ttu-id="eea6d-363">Další nastavení obnovení může pocházet z vlastností MSBuild v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="eea6d-363">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="eea6d-364">Hodnoty lze také nastavit z příkazového řádku pomocí přepínače `-p:` (viz příklady níže).</span><span class="sxs-lookup"><span data-stu-id="eea6d-364">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="eea6d-365">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="eea6d-365">Property</span></span> | <span data-ttu-id="eea6d-366">Popis</span><span class="sxs-lookup"><span data-stu-id="eea6d-366">Description</span></span> |
|--------|--------|
| <span data-ttu-id="eea6d-367">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="eea6d-367">RestoreSources</span></span> | <span data-ttu-id="eea6d-368">Seznam zdrojů balíčků oddělených středníkem.</span><span class="sxs-lookup"><span data-stu-id="eea6d-368">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="eea6d-369">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="eea6d-369">RestorePackagesPath</span></span> | <span data-ttu-id="eea6d-370">Cesta ke složce uživatelských balíčků</span><span class="sxs-lookup"><span data-stu-id="eea6d-370">User packages folder path.</span></span> |
| <span data-ttu-id="eea6d-371">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="eea6d-371">RestoreDisableParallel</span></span> | <span data-ttu-id="eea6d-372">Omezit stahování na jednu po druhé.</span><span class="sxs-lookup"><span data-stu-id="eea6d-372">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="eea6d-373">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="eea6d-373">RestoreConfigFile</span></span> | <span data-ttu-id="eea6d-374">Cesta k souboru `Nuget.Config`, který se má použít</span><span class="sxs-lookup"><span data-stu-id="eea6d-374">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="eea6d-375">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="eea6d-375">RestoreNoCache</span></span> | <span data-ttu-id="eea6d-376">Je-li nastavena hodnota true, nepoužívejte balíčky uložené v mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="eea6d-376">If true, avoids using cached packages.</span></span> <span data-ttu-id="eea6d-377">Viz [Správa globálních balíčků a složek mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="eea6d-377">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="eea6d-378">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="eea6d-378">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="eea6d-379">Pokud má hodnotu true, ignoruje neúspěšné nebo chybějící zdroje balíčků.</span><span class="sxs-lookup"><span data-stu-id="eea6d-379">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="eea6d-380">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="eea6d-380">RestoreFallbackFolders</span></span> | <span data-ttu-id="eea6d-381">Záložní složky používané ve stejném způsobu, jakým se používá složka uživatelských balíčků.</span><span class="sxs-lookup"><span data-stu-id="eea6d-381">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="eea6d-382">RestoreAdditionalProjectSources</span><span class="sxs-lookup"><span data-stu-id="eea6d-382">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="eea6d-383">Další zdroje, které se mají použít při obnovení.</span><span class="sxs-lookup"><span data-stu-id="eea6d-383">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="eea6d-384">RestoreAdditionalProjectFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="eea6d-384">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="eea6d-385">Další záložní složky, které se mají použít při obnovení</span><span class="sxs-lookup"><span data-stu-id="eea6d-385">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="eea6d-386">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="eea6d-386">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="eea6d-387">Vyloučí záložní složky zadané v `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="eea6d-387">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="eea6d-388">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="eea6d-388">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="eea6d-389">Cesta k `NuGet.Build.Tasks.dll`</span><span class="sxs-lookup"><span data-stu-id="eea6d-389">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="eea6d-390">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="eea6d-390">RestoreGraphProjectInput</span></span> | <span data-ttu-id="eea6d-391">Středníkem oddělený seznam projektů, které mají být obnoveny, které by měly obsahovat absolutní cesty.</span><span class="sxs-lookup"><span data-stu-id="eea6d-391">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="eea6d-392">RestoreUseSkipNonexistentTargets</span><span class="sxs-lookup"><span data-stu-id="eea6d-392">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="eea6d-393">Když jsou projekty shromažďovány pomocí nástroje MSBuild, určuje, zda jsou shromažďovány pomocí optimalizace `SkipNonexistentTargets`.</span><span class="sxs-lookup"><span data-stu-id="eea6d-393">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="eea6d-394">Pokud není nastavená, výchozí hodnota je `true`.</span><span class="sxs-lookup"><span data-stu-id="eea6d-394">When not set, defaults to `true`.</span></span> <span data-ttu-id="eea6d-395">Příčinou je rychlé chování při selhání, když cíle projektu nelze importovat.</span><span class="sxs-lookup"><span data-stu-id="eea6d-395">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="eea6d-396">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="eea6d-396">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="eea6d-397">Výstupní složka, výchozí nastavení pro `BaseIntermediateOutputPath` a složku `obj`.</span><span class="sxs-lookup"><span data-stu-id="eea6d-397">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| <span data-ttu-id="eea6d-398">RestoreForce</span><span class="sxs-lookup"><span data-stu-id="eea6d-398">RestoreForce</span></span> | <span data-ttu-id="eea6d-399">V projektech založených na PackageReference vynutí vyřešení všech závislostí i v případě, že bylo poslední obnovení úspěšné.</span><span class="sxs-lookup"><span data-stu-id="eea6d-399">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="eea6d-400">Zadání tohoto příznaku se podobá odstranění souboru `project.assets.json`.</span><span class="sxs-lookup"><span data-stu-id="eea6d-400">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="eea6d-401">To neobejde mezipaměť HTTP-cache.</span><span class="sxs-lookup"><span data-stu-id="eea6d-401">This does not bypass the http-cache.</span></span> |
| <span data-ttu-id="eea6d-402">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="eea6d-402">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="eea6d-403">Výslovný se na použití souboru zámku.</span><span class="sxs-lookup"><span data-stu-id="eea6d-403">Opts into the usage of a lock file.</span></span> |
| <span data-ttu-id="eea6d-404">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="eea6d-404">RestoreLockedMode</span></span> | <span data-ttu-id="eea6d-405">Spustit obnovení v uzamčeném režimu.</span><span class="sxs-lookup"><span data-stu-id="eea6d-405">Run restore in locked mode.</span></span> <span data-ttu-id="eea6d-406">To znamená, že obnovení nebude přehodnocovat závislosti.</span><span class="sxs-lookup"><span data-stu-id="eea6d-406">This means that restore will not reevaluate the dependencies.</span></span> |
| <span data-ttu-id="eea6d-407">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="eea6d-407">NuGetLockFilePath</span></span> | <span data-ttu-id="eea6d-408">Vlastní umístění souboru zámku.</span><span class="sxs-lookup"><span data-stu-id="eea6d-408">A custom location for the lock file.</span></span> <span data-ttu-id="eea6d-409">Výchozí umístění je vedle projektu a má název `packages.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="eea6d-409">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| <span data-ttu-id="eea6d-410">RestoreForceEvaluate</span><span class="sxs-lookup"><span data-stu-id="eea6d-410">RestoreForceEvaluate</span></span> | <span data-ttu-id="eea6d-411">Vynutí obnovení pro přepočítání závislostí a aktualizaci souboru zámku bez upozornění.</span><span class="sxs-lookup"><span data-stu-id="eea6d-411">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> | 

#### <a name="examples"></a><span data-ttu-id="eea6d-412">Příklady</span><span class="sxs-lookup"><span data-stu-id="eea6d-412">Examples</span></span>

<span data-ttu-id="eea6d-413">Příkazový řádek:</span><span class="sxs-lookup"><span data-stu-id="eea6d-413">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="eea6d-414">Soubor projektu:</span><span class="sxs-lookup"><span data-stu-id="eea6d-414">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="eea6d-415">Obnovit výstupy</span><span class="sxs-lookup"><span data-stu-id="eea6d-415">Restore outputs</span></span>

<span data-ttu-id="eea6d-416">Obnovení vytvoří ve složce Build `obj` následující soubory:</span><span class="sxs-lookup"><span data-stu-id="eea6d-416">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="eea6d-417">Soubor</span><span class="sxs-lookup"><span data-stu-id="eea6d-417">File</span></span> | <span data-ttu-id="eea6d-418">Popis</span><span class="sxs-lookup"><span data-stu-id="eea6d-418">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="eea6d-419">Obsahuje graf závislostí všech odkazů na balíčky.</span><span class="sxs-lookup"><span data-stu-id="eea6d-419">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="eea6d-420">Odkazy na MSBuild props obsažená v balíčcích</span><span class="sxs-lookup"><span data-stu-id="eea6d-420">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="eea6d-421">Odkazy na cíle nástroje MSBuild obsažené v balíčcích</span><span class="sxs-lookup"><span data-stu-id="eea6d-421">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="eea6d-422">Obnovení a sestavování pomocí jednoho příkazu MSBuild</span><span class="sxs-lookup"><span data-stu-id="eea6d-422">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="eea6d-423">Vzhledem k tomu, že nástroj NuGet dokáže obnovit balíčky, které vycházejí z cílů a props nástroje MSBuild, jsou vyhodnocení obnovení a sestavení spouštěna s různými globálními vlastnostmi.</span><span class="sxs-lookup"><span data-stu-id="eea6d-423">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="eea6d-424">To znamená, že následující nastavení bude mít nepředvídatelné a často nesprávné chování.</span><span class="sxs-lookup"><span data-stu-id="eea6d-424">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="eea6d-425">Místo doporučeného přístupu:</span><span class="sxs-lookup"><span data-stu-id="eea6d-425">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="eea6d-426">Stejná logika platí i pro jiné cíle, podobně jako u `build`.</span><span class="sxs-lookup"><span data-stu-id="eea6d-426">The same logic applies to other targets similar to `build`.</span></span>

### <a name="packagetargetfallback"></a><span data-ttu-id="eea6d-427">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="eea6d-427">PackageTargetFallback</span></span>

<span data-ttu-id="eea6d-428">Element `PackageTargetFallback` umožňuje zadat sadu kompatibilních cílů, které se mají použít při obnovování balíčků.</span><span class="sxs-lookup"><span data-stu-id="eea6d-428">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="eea6d-429">Je navržena tak, aby povolovala balíčkům, které používají dotnet [TxM](../reference/target-frameworks.md) pro práci s kompatibilními balíčky, které nedeklarují dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="eea6d-429">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="eea6d-430">To znamená, že pokud váš projekt používá dotnet TxM, pak všechny balíčky, na kterých závisí, musí mít také hodnotu dotnet TxM, pokud nepřidáte `<PackageTargetFallback>` do projektu, aby bylo umožněno kompatibilitu platforem, které nejsou dotnet, pomocí dotnet.</span><span class="sxs-lookup"><span data-stu-id="eea6d-430">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="eea6d-431">Například pokud projekt používá `netstandard1.6` TxM a závislý balíček obsahuje pouze `lib/net45/a.dll` a `lib/portable-net45+win81/a.dll`, projekt se nepodaří sestavit.</span><span class="sxs-lookup"><span data-stu-id="eea6d-431">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="eea6d-432">Pokud je to, co chcete uvést, je druhá knihovna DLL, pak můžete přidat `PackageTargetFallback` následujícím způsobem, aby se říká, že je knihovna DLL `portable-net45+win81` kompatibilní:</span><span class="sxs-lookup"><span data-stu-id="eea6d-432">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="eea6d-433">Chcete-li deklarovat zálohu pro všechny cíle v projektu, ponechte atribut `Condition`.</span><span class="sxs-lookup"><span data-stu-id="eea6d-433">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="eea6d-434">Existující `PackageTargetFallback` můžete také roztáhnout tak, že zahrnete `$(PackageTargetFallback)`, jak je znázorněno zde:</span><span class="sxs-lookup"><span data-stu-id="eea6d-434">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="eea6d-435">Nahrazení jedné knihovny z grafu obnovení</span><span class="sxs-lookup"><span data-stu-id="eea6d-435">Replacing one library from a restore graph</span></span>

<span data-ttu-id="eea6d-436">Pokud obnovení předává nesprávné sestavení, je možné vyřadit výchozí volbu balíčků a nahradit ji vlastní volbou.</span><span class="sxs-lookup"><span data-stu-id="eea6d-436">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="eea6d-437">Nejprve s `PackageReference`nejvyšší úrovně vylučte všechny prostředky:</span><span class="sxs-lookup"><span data-stu-id="eea6d-437">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="eea6d-438">Dále přidejte vlastní odkaz na příslušnou místní kopii knihovny DLL:</span><span class="sxs-lookup"><span data-stu-id="eea6d-438">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
