---
title: Sada NuGet Pack a obnovení jako cíle MSBuild
description: Sada NuGet Pack a obnovení může pracovat přímo jako cíle MSBuild s NuGet 4.0 +.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: a9331ad2ea0482737d84f4ea9a9babf95da8d66f
ms.sourcegitcommit: d5cc3f01a92c2d69b794343c09aff07ba9e912e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/05/2019
ms.locfileid: "70385895"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="cddd2-103">Sada NuGet Pack a obnovení jako cíle MSBuild</span><span class="sxs-lookup"><span data-stu-id="cddd2-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="cddd2-104">*NuGet 4.0 +*</span><span class="sxs-lookup"><span data-stu-id="cddd2-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="cddd2-105">Ve formátu [PackageReference](../consume-packages/package-references-in-project-files.md) NuGet 4.0 + může ukládat všechna metadata manifestu přímo do souboru projektu místo použití samostatného `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="cddd2-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="cddd2-106">Pomocí nástroje MSBuild 15.1 + nástroj NuGet je také první třídou občana MSBuild s `pack` cíli `restore` a, jak je popsáno níže.</span><span class="sxs-lookup"><span data-stu-id="cddd2-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="cddd2-107">Tyto cíle vám umožňují pracovat s balíčky NuGet stejně jako s ostatními úlohami nebo cíli MSBuild.</span><span class="sxs-lookup"><span data-stu-id="cddd2-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="cddd2-108">Pokyny k vytvoření balíčku NuGet pomocí nástroje MSBuild najdete v tématu [Vytvoření balíčku NuGet pomocí nástroje MSBuild](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="cddd2-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="cddd2-109">(Pro NuGet 3. x a starší použijte místo toho příkazy [Pack](../reference/cli-reference/cli-ref-pack.md) a [obnovení](../reference/cli-reference/cli-ref-restore.md) prostřednictvím rozhraní příkazového řádku NuGet.)</span><span class="sxs-lookup"><span data-stu-id="cddd2-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="cddd2-110">Pořadí cílového sestavení</span><span class="sxs-lookup"><span data-stu-id="cddd2-110">Target build order</span></span>

<span data-ttu-id="cddd2-111">Vzhledem `pack` k `restore` tomu, že a jsou cíle nástroje MSBuild, můžete k nim přistupovat, abyste mohli vylepšit pracovní postup.</span><span class="sxs-lookup"><span data-stu-id="cddd2-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="cddd2-112">Řekněme například, že chcete po sbalení balíčku zkopírovat do sdílené síťové složky.</span><span class="sxs-lookup"><span data-stu-id="cddd2-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="cddd2-113">To lze provést přidáním následujícího do souboru projektu:</span><span class="sxs-lookup"><span data-stu-id="cddd2-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="cddd2-114">Podobně můžete napsat úlohu MSBuild, napsat vlastní cíl a využít vlastnosti NuGet v úloze MSBuild.</span><span class="sxs-lookup"><span data-stu-id="cddd2-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="cddd2-115">`$(OutputPath)`je relativní a očekává, že spouštíte příkaz z kořenového adresáře projektu.</span><span class="sxs-lookup"><span data-stu-id="cddd2-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="cddd2-116">cíl balíčku</span><span class="sxs-lookup"><span data-stu-id="cddd2-116">pack target</span></span>

<span data-ttu-id="cddd2-117">Pro .NET Standard projekty pomocí formátu PackageReference pomocí `msbuild -t:pack` kreslení vstupů ze souboru projektu, který se má použít při vytváření balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="cddd2-117">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="cddd2-118">Následující tabulka popisuje vlastnosti nástroje MSBuild, které lze přidat do souboru projektu v rámci prvního `<PropertyGroup>` uzlu.</span><span class="sxs-lookup"><span data-stu-id="cddd2-118">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="cddd2-119">Tyto úpravy můžete snadno upravit v aplikaci Visual Studio 2017 a novějším kliknutím pravým tlačítkem myši na projekt a výběrem možnosti **Upravit {PROJECT_NAME}** v místní nabídce.</span><span class="sxs-lookup"><span data-stu-id="cddd2-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="cddd2-120">Pro přehlednost je tabulka uspořádaná podle ekvivalentní vlastnosti v [ `.nuspec` souboru](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="cddd2-120">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="cddd2-121">Všimněte si, `Owners` že `Summary` nástroj MSBuild `.nuspec` nepodporuje vlastnosti a.</span><span class="sxs-lookup"><span data-stu-id="cddd2-121">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="cddd2-122">Hodnota atributu/NuSpec</span><span class="sxs-lookup"><span data-stu-id="cddd2-122">Attribute/NuSpec Value</span></span> | <span data-ttu-id="cddd2-123">Vlastnost MSBuild</span><span class="sxs-lookup"><span data-stu-id="cddd2-123">MSBuild Property</span></span> | <span data-ttu-id="cddd2-124">Výchozí</span><span class="sxs-lookup"><span data-stu-id="cddd2-124">Default</span></span> | <span data-ttu-id="cddd2-125">Poznámky</span><span class="sxs-lookup"><span data-stu-id="cddd2-125">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="cddd2-126">Id</span><span class="sxs-lookup"><span data-stu-id="cddd2-126">Id</span></span> | <span data-ttu-id="cddd2-127">PackageId</span><span class="sxs-lookup"><span data-stu-id="cddd2-127">PackageId</span></span> | <span data-ttu-id="cddd2-128">Doplňk</span><span class="sxs-lookup"><span data-stu-id="cddd2-128">AssemblyName</span></span> | <span data-ttu-id="cddd2-129">$ (AssemblyName) z MSBuild</span><span class="sxs-lookup"><span data-stu-id="cddd2-129">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="cddd2-130">Version</span><span class="sxs-lookup"><span data-stu-id="cddd2-130">Version</span></span> | <span data-ttu-id="cddd2-131">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="cddd2-131">PackageVersion</span></span> | <span data-ttu-id="cddd2-132">Version</span><span class="sxs-lookup"><span data-stu-id="cddd2-132">Version</span></span> | <span data-ttu-id="cddd2-133">To je semver kompatibilní, například "1.0.0", "1.0.0-beta" nebo "1.0.0-beta-00345"</span><span class="sxs-lookup"><span data-stu-id="cddd2-133">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="cddd2-134">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="cddd2-134">VersionPrefix</span></span> | <span data-ttu-id="cddd2-135">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="cddd2-135">PackageVersionPrefix</span></span> | <span data-ttu-id="cddd2-136">empty</span><span class="sxs-lookup"><span data-stu-id="cddd2-136">empty</span></span> | <span data-ttu-id="cddd2-137">Nastavení PackageVersion přepsání PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="cddd2-137">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="cddd2-138">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="cddd2-138">VersionSuffix</span></span> | <span data-ttu-id="cddd2-139">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="cddd2-139">PackageVersionSuffix</span></span> | <span data-ttu-id="cddd2-140">empty</span><span class="sxs-lookup"><span data-stu-id="cddd2-140">empty</span></span> | <span data-ttu-id="cddd2-141">$ (VersionSuffix) z MSBuild.</span><span class="sxs-lookup"><span data-stu-id="cddd2-141">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="cddd2-142">Nastavení PackageVersion přepsání PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="cddd2-142">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="cddd2-143">Autoři</span><span class="sxs-lookup"><span data-stu-id="cddd2-143">Authors</span></span> | <span data-ttu-id="cddd2-144">Autoři</span><span class="sxs-lookup"><span data-stu-id="cddd2-144">Authors</span></span> | <span data-ttu-id="cddd2-145">Uživatelské jméno aktuálního uživatele</span><span class="sxs-lookup"><span data-stu-id="cddd2-145">Username of the current user</span></span> | |
| <span data-ttu-id="cddd2-146">Vlastníka</span><span class="sxs-lookup"><span data-stu-id="cddd2-146">Owners</span></span> | <span data-ttu-id="cddd2-147">Není k dispozici</span><span class="sxs-lookup"><span data-stu-id="cddd2-147">N/A</span></span> | <span data-ttu-id="cddd2-148">Nepřítomno v NuSpec</span><span class="sxs-lookup"><span data-stu-id="cddd2-148">Not present in NuSpec</span></span> | |
| <span data-ttu-id="cddd2-149">Název</span><span class="sxs-lookup"><span data-stu-id="cddd2-149">Title</span></span> | <span data-ttu-id="cddd2-150">Název</span><span class="sxs-lookup"><span data-stu-id="cddd2-150">Title</span></span> | <span data-ttu-id="cddd2-151">PackageId</span><span class="sxs-lookup"><span data-stu-id="cddd2-151">The PackageId</span></span>| |
| <span data-ttu-id="cddd2-152">Popis</span><span class="sxs-lookup"><span data-stu-id="cddd2-152">Description</span></span> | <span data-ttu-id="cddd2-153">Popis</span><span class="sxs-lookup"><span data-stu-id="cddd2-153">Description</span></span> | <span data-ttu-id="cddd2-154">Popis balíčku</span><span class="sxs-lookup"><span data-stu-id="cddd2-154">"Package Description"</span></span> | |
| <span data-ttu-id="cddd2-155">Úprava</span><span class="sxs-lookup"><span data-stu-id="cddd2-155">Copyright</span></span> | <span data-ttu-id="cddd2-156">Úprava</span><span class="sxs-lookup"><span data-stu-id="cddd2-156">Copyright</span></span> | <span data-ttu-id="cddd2-157">empty</span><span class="sxs-lookup"><span data-stu-id="cddd2-157">empty</span></span> | |
| <span data-ttu-id="cddd2-158">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="cddd2-158">RequireLicenseAcceptance</span></span> | <span data-ttu-id="cddd2-159">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="cddd2-159">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="cddd2-160">false</span><span class="sxs-lookup"><span data-stu-id="cddd2-160">false</span></span> | |
| <span data-ttu-id="cddd2-161">průkaz</span><span class="sxs-lookup"><span data-stu-id="cddd2-161">license</span></span> | <span data-ttu-id="cddd2-162">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="cddd2-162">PackageLicenseExpression</span></span> | <span data-ttu-id="cddd2-163">empty</span><span class="sxs-lookup"><span data-stu-id="cddd2-163">empty</span></span> | <span data-ttu-id="cddd2-164">Odpovídá`<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="cddd2-164">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="cddd2-165">průkaz</span><span class="sxs-lookup"><span data-stu-id="cddd2-165">license</span></span> | <span data-ttu-id="cddd2-166">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="cddd2-166">PackageLicenseFile</span></span> | <span data-ttu-id="cddd2-167">empty</span><span class="sxs-lookup"><span data-stu-id="cddd2-167">empty</span></span> | <span data-ttu-id="cddd2-168">`<license type="file">`Odpovídá.</span><span class="sxs-lookup"><span data-stu-id="cddd2-168">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="cddd2-169">Je možné, že bude nutné explicitně sbalit soubor s odkazem na licenci.</span><span class="sxs-lookup"><span data-stu-id="cddd2-169">You may need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="cddd2-170">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="cddd2-170">LicenseUrl</span></span> | <span data-ttu-id="cddd2-171">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="cddd2-171">PackageLicenseUrl</span></span> | <span data-ttu-id="cddd2-172">empty</span><span class="sxs-lookup"><span data-stu-id="cddd2-172">empty</span></span> | <span data-ttu-id="cddd2-173">`PackageLicenseUrl`je zastaralá, použijte vlastnost PackageLicenseExpression nebo PackageLicenseFile.</span><span class="sxs-lookup"><span data-stu-id="cddd2-173">`PackageLicenseUrl` is deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="cddd2-174">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="cddd2-174">ProjectUrl</span></span> | <span data-ttu-id="cddd2-175">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="cddd2-175">PackageProjectUrl</span></span> | <span data-ttu-id="cddd2-176">empty</span><span class="sxs-lookup"><span data-stu-id="cddd2-176">empty</span></span> | |
| <span data-ttu-id="cddd2-177">Ikona</span><span class="sxs-lookup"><span data-stu-id="cddd2-177">Icon</span></span> | <span data-ttu-id="cddd2-178">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="cddd2-178">PackageIcon</span></span> | <span data-ttu-id="cddd2-179">empty</span><span class="sxs-lookup"><span data-stu-id="cddd2-179">empty</span></span> | <span data-ttu-id="cddd2-180">Možná budete muset explicitně sbalit soubor obrázku odkazované ikony.</span><span class="sxs-lookup"><span data-stu-id="cddd2-180">You may need to explicitly pack the referenced icon image file.</span></span>|
| <span data-ttu-id="cddd2-181">IconUrl</span><span class="sxs-lookup"><span data-stu-id="cddd2-181">IconUrl</span></span> | <span data-ttu-id="cddd2-182">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="cddd2-182">PackageIconUrl</span></span> | <span data-ttu-id="cddd2-183">empty</span><span class="sxs-lookup"><span data-stu-id="cddd2-183">empty</span></span> | <span data-ttu-id="cddd2-184">`PackageIconUrl`je zastaralá, použijte vlastnost PackageIcon.</span><span class="sxs-lookup"><span data-stu-id="cddd2-184">`PackageIconUrl` is deprecated, use the PackageIcon property</span></span> |
| <span data-ttu-id="cddd2-185">Značky</span><span class="sxs-lookup"><span data-stu-id="cddd2-185">Tags</span></span> | <span data-ttu-id="cddd2-186">PackageTags</span><span class="sxs-lookup"><span data-stu-id="cddd2-186">PackageTags</span></span> | <span data-ttu-id="cddd2-187">empty</span><span class="sxs-lookup"><span data-stu-id="cddd2-187">empty</span></span> | <span data-ttu-id="cddd2-188">Značky jsou středníky odděleny středníkem.</span><span class="sxs-lookup"><span data-stu-id="cddd2-188">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="cddd2-189">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="cddd2-189">ReleaseNotes</span></span> | <span data-ttu-id="cddd2-190">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="cddd2-190">PackageReleaseNotes</span></span> | <span data-ttu-id="cddd2-191">empty</span><span class="sxs-lookup"><span data-stu-id="cddd2-191">empty</span></span> | |
| <span data-ttu-id="cddd2-192">Úložiště/adresa URL</span><span class="sxs-lookup"><span data-stu-id="cddd2-192">Repository/Url</span></span> | <span data-ttu-id="cddd2-193">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="cddd2-193">RepositoryUrl</span></span> | <span data-ttu-id="cddd2-194">empty</span><span class="sxs-lookup"><span data-stu-id="cddd2-194">empty</span></span> | <span data-ttu-id="cddd2-195">Adresa URL úložiště, která se používá k klonování nebo načtení zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="cddd2-195">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="cddd2-196">Případě *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="cddd2-196">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="cddd2-197">Úložiště/typ</span><span class="sxs-lookup"><span data-stu-id="cddd2-197">Repository/Type</span></span> | <span data-ttu-id="cddd2-198">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="cddd2-198">RepositoryType</span></span> | <span data-ttu-id="cddd2-199">empty</span><span class="sxs-lookup"><span data-stu-id="cddd2-199">empty</span></span> | <span data-ttu-id="cddd2-200">Typ úložiště</span><span class="sxs-lookup"><span data-stu-id="cddd2-200">Repository type.</span></span> <span data-ttu-id="cddd2-201">Příklady: *Git*, *TFS*.</span><span class="sxs-lookup"><span data-stu-id="cddd2-201">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="cddd2-202">Úložiště/větev</span><span class="sxs-lookup"><span data-stu-id="cddd2-202">Repository/Branch</span></span> | <span data-ttu-id="cddd2-203">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="cddd2-203">RepositoryBranch</span></span> | <span data-ttu-id="cddd2-204">empty</span><span class="sxs-lookup"><span data-stu-id="cddd2-204">empty</span></span> | <span data-ttu-id="cddd2-205">Volitelné informace o větvi úložiště</span><span class="sxs-lookup"><span data-stu-id="cddd2-205">Optional repository branch information.</span></span> <span data-ttu-id="cddd2-206">Pro zahrnutí této vlastnosti je nutné zadat také *RepositoryUrl* .</span><span class="sxs-lookup"><span data-stu-id="cddd2-206">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="cddd2-207">Příklad: *Master* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="cddd2-207">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="cddd2-208">Úložiště/potvrzení změn</span><span class="sxs-lookup"><span data-stu-id="cddd2-208">Repository/Commit</span></span> | <span data-ttu-id="cddd2-209">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="cddd2-209">RepositoryCommit</span></span> | <span data-ttu-id="cddd2-210">empty</span><span class="sxs-lookup"><span data-stu-id="cddd2-210">empty</span></span> | <span data-ttu-id="cddd2-211">Volitelné potvrzení změn úložiště nebo sada změn, které označují, na který zdroj byl balíček vytvořen.</span><span class="sxs-lookup"><span data-stu-id="cddd2-211">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="cddd2-212">Pro zahrnutí této vlastnosti je nutné zadat také *RepositoryUrl* .</span><span class="sxs-lookup"><span data-stu-id="cddd2-212">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="cddd2-213">Příklad: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="cddd2-213">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="cddd2-214">PackageType</span><span class="sxs-lookup"><span data-stu-id="cddd2-214">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="cddd2-215">Souhrn</span><span class="sxs-lookup"><span data-stu-id="cddd2-215">Summary</span></span> | <span data-ttu-id="cddd2-216">Není podporováno</span><span class="sxs-lookup"><span data-stu-id="cddd2-216">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="cddd2-217">cílové vstupy balení</span><span class="sxs-lookup"><span data-stu-id="cddd2-217">pack target inputs</span></span>

- <span data-ttu-id="cddd2-218">Ispackable nastavenou</span><span class="sxs-lookup"><span data-stu-id="cddd2-218">IsPackable</span></span>
- <span data-ttu-id="cddd2-219">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="cddd2-219">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="cddd2-220">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="cddd2-220">PackageVersion</span></span>
- <span data-ttu-id="cddd2-221">PackageId</span><span class="sxs-lookup"><span data-stu-id="cddd2-221">PackageId</span></span>
- <span data-ttu-id="cddd2-222">Autoři</span><span class="sxs-lookup"><span data-stu-id="cddd2-222">Authors</span></span>
- <span data-ttu-id="cddd2-223">Popis</span><span class="sxs-lookup"><span data-stu-id="cddd2-223">Description</span></span>
- <span data-ttu-id="cddd2-224">Úprava</span><span class="sxs-lookup"><span data-stu-id="cddd2-224">Copyright</span></span>
- <span data-ttu-id="cddd2-225">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="cddd2-225">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="cddd2-226">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="cddd2-226">DevelopmentDependency</span></span>
- <span data-ttu-id="cddd2-227">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="cddd2-227">PackageLicenseExpression</span></span>
- <span data-ttu-id="cddd2-228">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="cddd2-228">PackageLicenseFile</span></span>
- <span data-ttu-id="cddd2-229">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="cddd2-229">PackageLicenseUrl</span></span>
- <span data-ttu-id="cddd2-230">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="cddd2-230">PackageProjectUrl</span></span>
- <span data-ttu-id="cddd2-231">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="cddd2-231">PackageIconUrl</span></span>
- <span data-ttu-id="cddd2-232">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="cddd2-232">PackageReleaseNotes</span></span>
- <span data-ttu-id="cddd2-233">PackageTags</span><span class="sxs-lookup"><span data-stu-id="cddd2-233">PackageTags</span></span>
- <span data-ttu-id="cddd2-234">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="cddd2-234">PackageOutputPath</span></span>
- <span data-ttu-id="cddd2-235">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="cddd2-235">IncludeSymbols</span></span>
- <span data-ttu-id="cddd2-236">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="cddd2-236">IncludeSource</span></span>
- <span data-ttu-id="cddd2-237">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="cddd2-237">PackageTypes</span></span>
- <span data-ttu-id="cddd2-238">Nástroj</span><span class="sxs-lookup"><span data-stu-id="cddd2-238">IsTool</span></span>
- <span data-ttu-id="cddd2-239">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="cddd2-239">RepositoryUrl</span></span>
- <span data-ttu-id="cddd2-240">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="cddd2-240">RepositoryType</span></span>
- <span data-ttu-id="cddd2-241">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="cddd2-241">RepositoryBranch</span></span>
- <span data-ttu-id="cddd2-242">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="cddd2-242">RepositoryCommit</span></span>
- <span data-ttu-id="cddd2-243">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="cddd2-243">NoPackageAnalysis</span></span>
- <span data-ttu-id="cddd2-244">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="cddd2-244">MinClientVersion</span></span>
- <span data-ttu-id="cddd2-245">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="cddd2-245">IncludeBuildOutput</span></span>
- <span data-ttu-id="cddd2-246">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="cddd2-246">IncludeContentInPack</span></span>
- <span data-ttu-id="cddd2-247">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="cddd2-247">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="cddd2-248">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="cddd2-248">ContentTargetFolders</span></span>
- <span data-ttu-id="cddd2-249">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="cddd2-249">NuspecFile</span></span>
- <span data-ttu-id="cddd2-250">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="cddd2-250">NuspecBasePath</span></span>
- <span data-ttu-id="cddd2-251">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="cddd2-251">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="cddd2-252">scénáře sady Pack</span><span class="sxs-lookup"><span data-stu-id="cddd2-252">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="cddd2-253">Potlačit závislosti</span><span class="sxs-lookup"><span data-stu-id="cddd2-253">Suppress dependencies</span></span>

<span data-ttu-id="cddd2-254">Chcete-li potlačit závislosti balíčků z vygenerovaného `true` balíčku NuGet, nastavte `SuppressDependenciesWhenPacking` na to, které umožní přeskočí všechny závislosti ze generovaného souboru nupkg.</span><span class="sxs-lookup"><span data-stu-id="cddd2-254">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="cddd2-255">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="cddd2-255">PackageIconUrl</span></span>

> [!Important]
> <span data-ttu-id="cddd2-256">PackageIconUrl je zastaralá.</span><span class="sxs-lookup"><span data-stu-id="cddd2-256">PackageIconUrl is deprecated.</span></span> <span data-ttu-id="cddd2-257">Místo toho použijte [PackageIcon](#packing-an-icon-image-file) .</span><span class="sxs-lookup"><span data-stu-id="cddd2-257">Use [PackageIcon](#packing-an-icon-image-file) instead.</span></span>

### <a name="packing-an-icon-image-file"></a><span data-ttu-id="cddd2-258">Balení souboru obrázku ikony</span><span class="sxs-lookup"><span data-stu-id="cddd2-258">Packing an icon image file</span></span>

<span data-ttu-id="cddd2-259">Při balení souboru obrázku ikony musíte použít vlastnost PackageIcon a zadat cestu k balíčku relativní ke kořenu balíčku.</span><span class="sxs-lookup"><span data-stu-id="cddd2-259">When packing an icon image file, you need to use PackageIcon property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="cddd2-260">Kromě toho je nutné zajistit, aby byl soubor zahrnut do balíčku.</span><span class="sxs-lookup"><span data-stu-id="cddd2-260">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="cddd2-261">Velikost souboru obrázku je omezená na 1 MB.</span><span class="sxs-lookup"><span data-stu-id="cddd2-261">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="cddd2-262">Podporované formáty souborů zahrnují JPEG a PNG.</span><span class="sxs-lookup"><span data-stu-id="cddd2-262">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="cddd2-263">Doporučujeme, abyste 64 × 64 rozlišení obrazu.</span><span class="sxs-lookup"><span data-stu-id="cddd2-263">We recommend an image resolution of 64x64.</span></span>

<span data-ttu-id="cddd2-264">Příklad:</span><span class="sxs-lookup"><span data-stu-id="cddd2-264">For example:</span></span>

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

<span data-ttu-id="cddd2-265">[Ukázka ikony balíčku](https://github.com/NuGet/Samples/tree/master/PackageIconExample)</span><span class="sxs-lookup"><span data-stu-id="cddd2-265">[Package Icon sample](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span></span>

<span data-ttu-id="cddd2-266">Pro ekvivalent nuspec se podívejte na [nuspec reference pro Icon](nuspec.md#icon).</span><span class="sxs-lookup"><span data-stu-id="cddd2-266">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="cddd2-267">Výstupní sestavení</span><span class="sxs-lookup"><span data-stu-id="cddd2-267">Output assemblies</span></span>

<span data-ttu-id="cddd2-268">`nuget pack`zkopíruje výstupní `.exe`soubory s příponami `.dll` `.xml` ,,`.winmd`,, a `.pri`. `.json`</span><span class="sxs-lookup"><span data-stu-id="cddd2-268">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="cddd2-269">Výstupní soubory, které jsou zkopírovány, závisí na tom, co `BuiltOutputProjectGroup` nástroj MSBuild poskytuje z cíle.</span><span class="sxs-lookup"><span data-stu-id="cddd2-269">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="cddd2-270">Existují dvě vlastnosti nástroje MSBuild, které lze použít v souboru projektu nebo na příkazovém řádku pro řízení, kde výstupní sestavení jdou:</span><span class="sxs-lookup"><span data-stu-id="cddd2-270">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="cddd2-271">`IncludeBuildOutput`: Logická hodnota, která určuje, zda mají být do balíčku zahrnuty výstupní sestavení sestavení.</span><span class="sxs-lookup"><span data-stu-id="cddd2-271">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="cddd2-272">`BuildOutputTargetFolder`: Určuje složku, do které se mají umístit výstupní sestavení.</span><span class="sxs-lookup"><span data-stu-id="cddd2-272">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="cddd2-273">Výstupní sestavení (a další výstupní soubory) se zkopírují do příslušných složek rozhraní.</span><span class="sxs-lookup"><span data-stu-id="cddd2-273">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="cddd2-274">Odkazy na balíčky</span><span class="sxs-lookup"><span data-stu-id="cddd2-274">Package references</span></span>

<span data-ttu-id="cddd2-275">Viz [odkazy na balíčky v souborech projektu](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="cddd2-275">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="cddd2-276">Odkazy na projekt a projekt</span><span class="sxs-lookup"><span data-stu-id="cddd2-276">Project to project references</span></span>

<span data-ttu-id="cddd2-277">Odkazy na projekt na projekt jsou ve výchozím nastavení považovány za odkazy na balíčky NuGet, například:</span><span class="sxs-lookup"><span data-stu-id="cddd2-277">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="cddd2-278">Do odkazu na projekt můžete také přidat následující metadata:</span><span class="sxs-lookup"><span data-stu-id="cddd2-278">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="cddd2-279">Zahrnutí obsahu do balíčku</span><span class="sxs-lookup"><span data-stu-id="cddd2-279">Including content in a package</span></span>

<span data-ttu-id="cddd2-280">Chcete-li zahrnout obsah, přidejte do existující `<Content>` položky metadata navíc.</span><span class="sxs-lookup"><span data-stu-id="cddd2-280">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="cddd2-281">Ve výchozím nastavení jsou všechny položky typu "obsah" zahrnuty do balíčku, Pokud nepřepíšete záznamy podobné následujícímu:</span><span class="sxs-lookup"><span data-stu-id="cddd2-281">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="cddd2-282">Ve výchozím nastavení je vše přidáno do kořenu `content` a `contentFiles\any\<target_framework>` složky v rámci balíčku a zachovává strukturu relativních složek, pokud nezadáte cestu k balíčku:</span><span class="sxs-lookup"><span data-stu-id="cddd2-282">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="cddd2-283">Pokud chcete kopírovat veškerý obsah pouze na konkrétní kořenové složky (místo `content` a `contentFiles` obojí), můžete použít vlastnost `ContentTargetFolders`MSBuild, která má výchozí hodnotu Content; contentFiles, ale lze ji nastavit na jiné názvy složek.</span><span class="sxs-lookup"><span data-stu-id="cddd2-283">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="cddd2-284">Všimněte si, že pouze zadání "contentFiles `ContentTargetFolders` " v `contentFiles\any\<target_framework>` souboru vloží `contentFiles\<language>\<target_framework>` soubory do `buildAction`nebo na základě.</span><span class="sxs-lookup"><span data-stu-id="cddd2-284">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="cddd2-285">`PackagePath`může se jednat o sadu cílových cest oddělených středníky.</span><span class="sxs-lookup"><span data-stu-id="cddd2-285">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="cddd2-286">Zadáním prázdné cesty k balíčku by se soubor přidal do kořenového adresáře balíčku.</span><span class="sxs-lookup"><span data-stu-id="cddd2-286">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="cddd2-287">Například následující příkaz přidá `libuv.txt` do `content\myfiles`, `content\samples`a kořenovou složku balíčku:</span><span class="sxs-lookup"><span data-stu-id="cddd2-287">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="cddd2-288">K dispozici je také vlastnost `$(IncludeContentInPack)`MSBuild, která má `true`výchozí hodnotu.</span><span class="sxs-lookup"><span data-stu-id="cddd2-288">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="cddd2-289">Pokud je nastavená `false` na libovolný projekt, pak obsah z tohoto projektu není zahrnutý v balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="cddd2-289">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="cddd2-290">Další metadata specifická pro sadu, která můžete nastavit na kterékoli z výše uvedených položek ```<PackageCopyToOutput>``` , ```<PackageFlatten>``` zahrnují a ```CopyToOutput``` které ```Flatten``` ```contentFiles``` sady a hodnoty pro položku ve výstupních nuspec.</span><span class="sxs-lookup"><span data-stu-id="cddd2-290">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="cddd2-291">Kromě položek `<Pack>` obsahu lze metadata a `<PackagePath>` také nastavit na soubory s akcí sestavení kompilovat, EmbeddedResource, ApplicationDefinition, Page, Resource, třídy SplashScreen, vazbě designdata, DesignDataWithDesignTimeCreateableTypes , CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource nebo None.</span><span class="sxs-lookup"><span data-stu-id="cddd2-291">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="cddd2-292">Pokud má balíček při použití vzorů expanze názvů připojit název souboru k cestě k balíčku, musí cesta k balíčku končit znakem oddělovače složky. v opačném případě se cesta k balíčku považuje za úplnou cestu včetně názvu souboru.</span><span class="sxs-lookup"><span data-stu-id="cddd2-292">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="cddd2-293">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="cddd2-293">IncludeSymbols</span></span>

<span data-ttu-id="cddd2-294">Při použití `MSBuild -t:pack -p:IncludeSymbols=true`se zkopírují `.pdb` odpovídající soubory spolu s jinými výstupními `.xml`soubory (`.dll`, `.exe`, `.winmd`,, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="cddd2-294">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="cddd2-295">Všimněte si, `IncludeSymbols=true` že nastavení vytvoří regulární balíček *a* balíček symbolů.</span><span class="sxs-lookup"><span data-stu-id="cddd2-295">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="cddd2-296">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="cddd2-296">IncludeSource</span></span>

<span data-ttu-id="cddd2-297">To je stejné jako `IncludeSymbols`s tím rozdílem, že kopíruje také zdrojové soubory spolu se `.pdb` soubory.</span><span class="sxs-lookup"><span data-stu-id="cddd2-297">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="cddd2-298">Všechny soubory typu `Compile` jsou zkopírovány za účelem `src\<ProjectName>\` zachování struktury složek relativní cesty ve výsledném balíčku.</span><span class="sxs-lookup"><span data-stu-id="cddd2-298">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="cddd2-299">Totéž se také stane u zdrojových souborů, `ProjectReference` které mají `TreatAsPackageReference` nastavené na `false`.</span><span class="sxs-lookup"><span data-stu-id="cddd2-299">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="cddd2-300">Pokud je soubor typu Compile mimo složku projektu, pak je pouze přidán do `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="cddd2-300">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="cddd2-301">Balení licenčního výrazu nebo licenčního souboru</span><span class="sxs-lookup"><span data-stu-id="cddd2-301">Packing a license expression or a license file</span></span>

<span data-ttu-id="cddd2-302">Při použití licenčního výrazu by se měla použít vlastnost PackageLicenseExpression.</span><span class="sxs-lookup"><span data-stu-id="cddd2-302">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="cddd2-303">[Ukázka licenčního výrazu](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="cddd2-303">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="cddd2-304">[Přečtěte si další informace o výrazech licencí a licencích, které jsou přijaty nástrojem NuGet.org](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="cddd2-304">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="cddd2-305">Při balení licenčního souboru musíte použít vlastnost PackageLicenseFile a zadat cestu k balíčku relativní ke kořenu balíčku.</span><span class="sxs-lookup"><span data-stu-id="cddd2-305">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="cddd2-306">Kromě toho je nutné zajistit, aby byl soubor zahrnut do balíčku.</span><span class="sxs-lookup"><span data-stu-id="cddd2-306">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="cddd2-307">Příklad:</span><span class="sxs-lookup"><span data-stu-id="cddd2-307">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="cddd2-308">[Ukázka licenčního souboru](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="cddd2-308">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="cddd2-309">Nástroj</span><span class="sxs-lookup"><span data-stu-id="cddd2-309">IsTool</span></span>

<span data-ttu-id="cddd2-310">Při použití `MSBuild -t:pack -p:IsTool=true`aplikace `lib` `tools` jsou všechny výstupní soubory, jak je uvedeno ve scénáři [výstup sestavení](#output-assemblies) , zkopírovány do složky namísto složky.</span><span class="sxs-lookup"><span data-stu-id="cddd2-310">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="cddd2-311">Všimněte si, že se liší od `DotNetCliTool` a, který je určen `PackageType` nastavením v `.csproj` souboru.</span><span class="sxs-lookup"><span data-stu-id="cddd2-311">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="cddd2-312">Balení pomocí. nuspec</span><span class="sxs-lookup"><span data-stu-id="cddd2-312">Packing using a .nuspec</span></span>

<span data-ttu-id="cddd2-313">I když se místo toho doporučuje [Zahrnout všechny vlastnosti](../reference/msbuild-targets.md#pack-target) , které jsou obvykle v `.nuspec` souboru v souboru projektu, můžete `.nuspec` zvolit použití souboru k balení projektu.</span><span class="sxs-lookup"><span data-stu-id="cddd2-313">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="cddd2-314">Pro projekt bez sady SDK, který používá `PackageReference`, je nutné importovat `NuGet.Build.Tasks.Pack.targets` , aby bylo možné spustit úlohu balíčku.</span><span class="sxs-lookup"><span data-stu-id="cddd2-314">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="cddd2-315">Před zabalením souboru nuspec je ještě nutné projekt obnovit.</span><span class="sxs-lookup"><span data-stu-id="cddd2-315">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="cddd2-316">(Projekt ve stylu sady SDK obsahuje cíle balíčku ve výchozím nastavení.)</span><span class="sxs-lookup"><span data-stu-id="cddd2-316">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="cddd2-317">Cílová architektura souboru projektu je nerelevantní a při balení nuspec se nepoužívá.</span><span class="sxs-lookup"><span data-stu-id="cddd2-317">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="cddd2-318">Následující tři vlastnosti MSBuild jsou relevantní pro balení pomocí `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="cddd2-318">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="cddd2-319">`NuspecFile`: relativní nebo absolutní cesta k `.nuspec` souboru, který se používá k balení.</span><span class="sxs-lookup"><span data-stu-id="cddd2-319">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="cddd2-320">`NuspecProperties`: středníkem oddělený seznam dvojic klíč = hodnota.</span><span class="sxs-lookup"><span data-stu-id="cddd2-320">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="cddd2-321">Kvůli způsobu, jakým funguje analýza příkazového řádku nástroje MSBuild, je nutné zadat více vlastností následujícím `-p:NuspecProperties=\"key1=value1;key2=value2\"`způsobem:.</span><span class="sxs-lookup"><span data-stu-id="cddd2-321">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="cddd2-322">`NuspecBasePath`: Základní cesta k `.nuspec` souboru</span><span class="sxs-lookup"><span data-stu-id="cddd2-322">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="cddd2-323">Pokud používáte `dotnet.exe` k balení projektu, použijte příkaz podobný následujícímu:</span><span class="sxs-lookup"><span data-stu-id="cddd2-323">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="cddd2-324">Při použití nástroje MSBuild k sbalení projektu použijte příkaz podobný následujícímu:</span><span class="sxs-lookup"><span data-stu-id="cddd2-324">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="cddd2-325">Všimněte si, že balení nuspec pomocí příkazu dotnet. exe nebo MSBuild také vede k sestavení projektu ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="cddd2-325">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="cddd2-326">K tomu je možné se vyhnout předáním ```--no-build``` vlastnosti do příkazu dotnet. exe, který je ekvivalentem nastavení ```<NoBuild>true</NoBuild> ``` v souboru projektu společně s nastavením ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="cddd2-326">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="cddd2-327">Příkladem souboru *. csproj* pro zabalení souboru nuspec je:</span><span class="sxs-lookup"><span data-stu-id="cddd2-327">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="cddd2-328">Rozšířené body rozšíření pro vytvoření přizpůsobeného balíčku</span><span class="sxs-lookup"><span data-stu-id="cddd2-328">Advanced extension points to create customized package</span></span>

<span data-ttu-id="cddd2-329">`pack` Cíl poskytuje dva Rozšiřovací body, které jsou spuštěny v sestavení specifickém pro vnitřní, cílové rozhraní.</span><span class="sxs-lookup"><span data-stu-id="cddd2-329">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="cddd2-330">Rozšiřující body podporují obsah a sestavení konkrétního cílového rozhraní do balíčku:</span><span class="sxs-lookup"><span data-stu-id="cddd2-330">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="cddd2-331">`TargetsForTfmSpecificBuildOutput`cílové Používá se pro soubory uvnitř `lib` složky nebo složky zadané pomocí. `BuildOutputTargetFolder`</span><span class="sxs-lookup"><span data-stu-id="cddd2-331">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="cddd2-332">`TargetsForTfmSpecificContentInPackage`cílové Použít pro soubory mimo `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="cddd2-332">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="cddd2-333">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="cddd2-333">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="cddd2-334">Napište vlastní cíl a zadejte ho jako hodnotu `$(TargetsForTfmSpecificBuildOutput)` vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="cddd2-334">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="cddd2-335">Pro všechny soubory, které potřebují přejít do `BuildOutputTargetFolder` nástroje (ve výchozím nastavení lib), by měl cíl zapisovat tyto soubory do skupiny `BuildOutputInPackage` Item a nastavit následující dvě hodnoty metadat:</span><span class="sxs-lookup"><span data-stu-id="cddd2-335">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="cddd2-336">`FinalOutputPath`: Absolutní cesta k souboru; Pokud není zadaný, použije se identita k vyhodnocení zdrojové cesty.</span><span class="sxs-lookup"><span data-stu-id="cddd2-336">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="cddd2-337">`TargetPath`:  Volitelné Nastavte, kdy soubor musí přejít do podsložky v rámci `lib\<TargetFramework>` , podobně jako satelitní sestavení, která se nacházejí v odpovídajících složkách kultury.</span><span class="sxs-lookup"><span data-stu-id="cddd2-337">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="cddd2-338">Výchozí hodnota je název souboru.</span><span class="sxs-lookup"><span data-stu-id="cddd2-338">Defaults to the name of the file.</span></span>

<span data-ttu-id="cddd2-339">Příklad:</span><span class="sxs-lookup"><span data-stu-id="cddd2-339">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="cddd2-340">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="cddd2-340">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="cddd2-341">Napište vlastní cíl a zadejte ho jako hodnotu `$(TargetsForTfmSpecificContentInPackage)` vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="cddd2-341">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="cddd2-342">U všech souborů, které se mají zahrnout do balíčku, by měl cíl tyto soubory zapsat do skupiny `TfmSpecificPackageFile` položek a nastavit následující volitelná metadata:</span><span class="sxs-lookup"><span data-stu-id="cddd2-342">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="cddd2-343">`PackagePath`: Cesta, kde by měl být v balíčku výstup souboru.</span><span class="sxs-lookup"><span data-stu-id="cddd2-343">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="cddd2-344">Při přidání více než jednoho souboru do stejné cesty k balíčku vyvolá NuGet vystavení upozornění.</span><span class="sxs-lookup"><span data-stu-id="cddd2-344">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="cddd2-345">`BuildAction`: Akce sestavení, která se má přiřadit k souboru, se vyžaduje jenom v případě, že je `contentFiles` cesta k balíčku ve složce.</span><span class="sxs-lookup"><span data-stu-id="cddd2-345">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="cddd2-346">Výchozí hodnota je None.</span><span class="sxs-lookup"><span data-stu-id="cddd2-346">Defaults to "None".</span></span>

<span data-ttu-id="cddd2-347">Příklad:</span><span class="sxs-lookup"><span data-stu-id="cddd2-347">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="cddd2-348">cíl obnovení</span><span class="sxs-lookup"><span data-stu-id="cddd2-348">restore target</span></span>

<span data-ttu-id="cddd2-349">`MSBuild -t:restore`(které `nuget restore` a `dotnet restore` používají se v projektech .NET Core), obnoví balíčky, na které se odkazuje v souboru projektu, takto:</span><span class="sxs-lookup"><span data-stu-id="cddd2-349">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="cddd2-350">Číst všechny odkazy z projektu na projekt</span><span class="sxs-lookup"><span data-stu-id="cddd2-350">Read all project to project references</span></span>
1. <span data-ttu-id="cddd2-351">Přečtěte si vlastnosti projektu a najděte mezilehlé složky a cílová rozhraní.</span><span class="sxs-lookup"><span data-stu-id="cddd2-351">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="cddd2-352">Předání dat nástroje MSBuild do NuGet. Build. Tasks. dll</span><span class="sxs-lookup"><span data-stu-id="cddd2-352">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="cddd2-353">Spustit obnovení</span><span class="sxs-lookup"><span data-stu-id="cddd2-353">Run restore</span></span>
1. <span data-ttu-id="cddd2-354">Stáhnout balíčky</span><span class="sxs-lookup"><span data-stu-id="cddd2-354">Download packages</span></span>
1. <span data-ttu-id="cddd2-355">Zápis souboru prostředků, cílů a vlastností props</span><span class="sxs-lookup"><span data-stu-id="cddd2-355">Write assets file, targets, and props</span></span>

<span data-ttu-id="cddd2-356">Cíl funguje pouze pro projekty, které používají formát PackageReference. `restore`</span><span class="sxs-lookup"><span data-stu-id="cddd2-356">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="cddd2-357">Nefunguje **pro** projekty používající `packages.config` formát. místo toho použijte [obnovení NuGet](../reference/cli-reference/cli-ref-restore.md) .</span><span class="sxs-lookup"><span data-stu-id="cddd2-357">It does **not** work for projects using the `packages.config` format; use [nuget restore](../reference/cli-reference/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="cddd2-358">Obnovit vlastnosti</span><span class="sxs-lookup"><span data-stu-id="cddd2-358">Restore properties</span></span>

<span data-ttu-id="cddd2-359">Další nastavení obnovení může pocházet z vlastností MSBuild v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="cddd2-359">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="cddd2-360">Hodnoty lze také nastavit z příkazového řádku pomocí `-p:` přepínače (viz příklady níže).</span><span class="sxs-lookup"><span data-stu-id="cddd2-360">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="cddd2-361">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="cddd2-361">Property</span></span> | <span data-ttu-id="cddd2-362">Popis</span><span class="sxs-lookup"><span data-stu-id="cddd2-362">Description</span></span> |
|--------|--------|
| <span data-ttu-id="cddd2-363">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="cddd2-363">RestoreSources</span></span> | <span data-ttu-id="cddd2-364">Seznam zdrojů balíčků oddělených středníkem.</span><span class="sxs-lookup"><span data-stu-id="cddd2-364">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="cddd2-365">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="cddd2-365">RestorePackagesPath</span></span> | <span data-ttu-id="cddd2-366">Cesta ke složce uživatelských balíčků</span><span class="sxs-lookup"><span data-stu-id="cddd2-366">User packages folder path.</span></span> |
| <span data-ttu-id="cddd2-367">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="cddd2-367">RestoreDisableParallel</span></span> | <span data-ttu-id="cddd2-368">Omezit stahování na jednu po druhé.</span><span class="sxs-lookup"><span data-stu-id="cddd2-368">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="cddd2-369">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="cddd2-369">RestoreConfigFile</span></span> | <span data-ttu-id="cddd2-370">Cesta k `Nuget.Config` souboru, který se má použít</span><span class="sxs-lookup"><span data-stu-id="cddd2-370">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="cddd2-371">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="cddd2-371">RestoreNoCache</span></span> | <span data-ttu-id="cddd2-372">Je-li nastavena hodnota true, nepoužívejte balíčky uložené v mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="cddd2-372">If true, avoids using cached packages.</span></span> <span data-ttu-id="cddd2-373">Viz [Správa globálních balíčků a složek mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="cddd2-373">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="cddd2-374">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="cddd2-374">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="cddd2-375">Pokud má hodnotu true, ignoruje neúspěšné nebo chybějící zdroje balíčků.</span><span class="sxs-lookup"><span data-stu-id="cddd2-375">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="cddd2-376">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="cddd2-376">RestoreFallbackFolders</span></span> | <span data-ttu-id="cddd2-377">Záložní složky používané ve stejném způsobu, jakým se používá složka uživatelských balíčků.</span><span class="sxs-lookup"><span data-stu-id="cddd2-377">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="cddd2-378">RestoreAdditionalProjectSources</span><span class="sxs-lookup"><span data-stu-id="cddd2-378">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="cddd2-379">Další zdroje, které se mají použít při obnovení.</span><span class="sxs-lookup"><span data-stu-id="cddd2-379">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="cddd2-380">RestoreAdditionalProjectFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="cddd2-380">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="cddd2-381">Další záložní složky, které se mají použít při obnovení</span><span class="sxs-lookup"><span data-stu-id="cddd2-381">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="cddd2-382">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="cddd2-382">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="cddd2-383">Vyloučí záložní složky zadané v`RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="cddd2-383">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="cddd2-384">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="cddd2-384">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="cddd2-385">Cesta k `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="cddd2-385">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="cddd2-386">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="cddd2-386">RestoreGraphProjectInput</span></span> | <span data-ttu-id="cddd2-387">Středníkem oddělený seznam projektů, které mají být obnoveny, které by měly obsahovat absolutní cesty.</span><span class="sxs-lookup"><span data-stu-id="cddd2-387">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="cddd2-388">RestoreUseSkipNonexistentTargets</span><span class="sxs-lookup"><span data-stu-id="cddd2-388">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="cddd2-389">Když jsou projekty shromažďovány pomocí nástroje MSBuild, určuje, zda jsou shromažďovány `SkipNonexistentTargets` pomocí optimalizace.</span><span class="sxs-lookup"><span data-stu-id="cddd2-389">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="cddd2-390">Pokud není nastaveno, výchozí hodnota `true`je.</span><span class="sxs-lookup"><span data-stu-id="cddd2-390">When not set, defaults to `true`.</span></span> <span data-ttu-id="cddd2-391">Příčinou je rychlé chování při selhání, když cíle projektu nelze importovat.</span><span class="sxs-lookup"><span data-stu-id="cddd2-391">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="cddd2-392">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="cddd2-392">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="cddd2-393">Výstupní složka, výchozí nastavení `BaseIntermediateOutputPath` `obj` a složka.</span><span class="sxs-lookup"><span data-stu-id="cddd2-393">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="cddd2-394">Příklady</span><span class="sxs-lookup"><span data-stu-id="cddd2-394">Examples</span></span>

<span data-ttu-id="cddd2-395">Příkazový řádek:</span><span class="sxs-lookup"><span data-stu-id="cddd2-395">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="cddd2-396">Soubor projektu:</span><span class="sxs-lookup"><span data-stu-id="cddd2-396">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="cddd2-397">Obnovit výstupy</span><span class="sxs-lookup"><span data-stu-id="cddd2-397">Restore outputs</span></span>

<span data-ttu-id="cddd2-398">Obnovení vytvoří ve složce buildu `obj` následující soubory:</span><span class="sxs-lookup"><span data-stu-id="cddd2-398">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="cddd2-399">Soubor</span><span class="sxs-lookup"><span data-stu-id="cddd2-399">File</span></span> | <span data-ttu-id="cddd2-400">Popis</span><span class="sxs-lookup"><span data-stu-id="cddd2-400">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="cddd2-401">Obsahuje graf závislostí všech odkazů na balíčky.</span><span class="sxs-lookup"><span data-stu-id="cddd2-401">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="cddd2-402">Odkazy na MSBuild props obsažená v balíčcích</span><span class="sxs-lookup"><span data-stu-id="cddd2-402">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="cddd2-403">Odkazy na cíle nástroje MSBuild obsažené v balíčcích</span><span class="sxs-lookup"><span data-stu-id="cddd2-403">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="cddd2-404">Obnovení a sestavování pomocí jednoho příkazu MSBuild</span><span class="sxs-lookup"><span data-stu-id="cddd2-404">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="cddd2-405">Vzhledem k tomu, že nástroj NuGet dokáže obnovit balíčky, které vycházejí z cílů a props nástroje MSBuild, jsou vyhodnocení obnovení a sestavení spouštěna s různými globálními vlastnostmi.</span><span class="sxs-lookup"><span data-stu-id="cddd2-405">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="cddd2-406">To znamená, že následující nastavení bude mít nepředvídatelné a často nesprávné chování.</span><span class="sxs-lookup"><span data-stu-id="cddd2-406">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="cddd2-407">Místo doporučeného přístupu:</span><span class="sxs-lookup"><span data-stu-id="cddd2-407">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="cddd2-408">Stejná logika platí pro jiné cíle podobné `build`.</span><span class="sxs-lookup"><span data-stu-id="cddd2-408">The same logic applies to other targets similar to `build`.</span></span>

### <a name="packagetargetfallback"></a><span data-ttu-id="cddd2-409">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="cddd2-409">PackageTargetFallback</span></span>

<span data-ttu-id="cddd2-410">`PackageTargetFallback` Element umožňuje zadat sadu kompatibilních cílů, které mají být použity při obnovení balíčků.</span><span class="sxs-lookup"><span data-stu-id="cddd2-410">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="cddd2-411">Je navržena tak, aby povolovala balíčkům, které používají dotnet [TxM](../reference/target-frameworks.md) pro práci s kompatibilními balíčky, které nedeklarují dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="cddd2-411">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="cddd2-412">To znamená, že pokud váš projekt používá dotnet TxM, pak všechny balíčky, na kterých závisí, musí mít také hodnotu dotnet TxM, pokud do projektu `<PackageTargetFallback>` nepřidáte, aby bylo možné, aby platformy, které nejsou dotnet, byly kompatibilní s dotnet.</span><span class="sxs-lookup"><span data-stu-id="cddd2-412">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="cddd2-413">Například pokud projekt používá `netstandard1.6` TxM a závislý balíček obsahuje pouze `lib/net45/a.dll` a `lib/portable-net45+win81/a.dll`, projekt se nepodaří sestavit.</span><span class="sxs-lookup"><span data-stu-id="cddd2-413">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="cddd2-414">Pokud je to, co chcete uvést, je druhá knihovna DLL, pak můžete přidat `PackageTargetFallback` tak, aby říkáme `portable-net45+win81` , že je knihovna DLL kompatibilní:</span><span class="sxs-lookup"><span data-stu-id="cddd2-414">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="cddd2-415">Chcete-li deklarovat zálohu pro všechny cíle v projektu, ponechte `Condition` atribut.</span><span class="sxs-lookup"><span data-stu-id="cddd2-415">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="cddd2-416">Můžete také všechny existující `PackageTargetFallback` `$(PackageTargetFallback)` , a to i tak, jak je znázorněno zde:</span><span class="sxs-lookup"><span data-stu-id="cddd2-416">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="cddd2-417">Nahrazení jedné knihovny z grafu obnovení</span><span class="sxs-lookup"><span data-stu-id="cddd2-417">Replacing one library from a restore graph</span></span>

<span data-ttu-id="cddd2-418">Pokud obnovení předává nesprávné sestavení, je možné vyřadit výchozí volbu balíčků a nahradit ji vlastní volbou.</span><span class="sxs-lookup"><span data-stu-id="cddd2-418">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="cddd2-419">Nejprve s nejvyšší úrovní `PackageReference`, vylučte všechny prostředky:</span><span class="sxs-lookup"><span data-stu-id="cddd2-419">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="cddd2-420">Dále přidejte vlastní odkaz na příslušnou místní kopii knihovny DLL:</span><span class="sxs-lookup"><span data-stu-id="cddd2-420">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
