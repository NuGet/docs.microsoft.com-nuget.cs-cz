---
title: Sada NuGet Pack a obnovení jako cíle MSBuild
description: Sada NuGet Pack a obnovení může pracovat přímo jako cíle MSBuild s NuGet 4.0 +.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 4a04c6dd7993fc47bcf7a6fe46236ed700a0d105
ms.sourcegitcommit: e39e5a5ddf68bf41e816617e7f0339308523bbb3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/05/2020
ms.locfileid: "96738926"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="49d91-103">Sada NuGet Pack a obnovení jako cíle MSBuild</span><span class="sxs-lookup"><span data-stu-id="49d91-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="49d91-104">*NuGet 4.0 +*</span><span class="sxs-lookup"><span data-stu-id="49d91-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="49d91-105">Ve formátu [PackageReference](../consume-packages/package-references-in-project-files.md) NuGet 4.0 + může ukládat všechna metadata manifestu přímo do souboru projektu místo použití samostatného `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="49d91-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="49d91-106">Pomocí nástroje MSBuild 15.1 + nástroj NuGet je také první třídou občana MSBuild s `pack` `restore` cíli a, jak je popsáno níže.</span><span class="sxs-lookup"><span data-stu-id="49d91-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="49d91-107">Tyto cíle vám umožňují pracovat s balíčky NuGet stejně jako s ostatními úlohami nebo cíli MSBuild.</span><span class="sxs-lookup"><span data-stu-id="49d91-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="49d91-108">Pokyny k vytvoření balíčku NuGet pomocí nástroje MSBuild najdete v tématu [Vytvoření balíčku NuGet pomocí nástroje MSBuild](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="49d91-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="49d91-109">(Pro NuGet 3. x a starší použijte místo toho příkazy [Pack](../reference/cli-reference/cli-ref-pack.md) a [obnovení](../reference/cli-reference/cli-ref-restore.md) prostřednictvím rozhraní příkazového řádku NuGet.)</span><span class="sxs-lookup"><span data-stu-id="49d91-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="49d91-110">Pořadí sestavení cílů</span><span class="sxs-lookup"><span data-stu-id="49d91-110">Target build order</span></span>

<span data-ttu-id="49d91-111">Vzhledem `pack` k tomu, že a `restore` jsou cíle nástroje MSBuild, můžete k nim přistupovat, abyste mohli vylepšit pracovní postup.</span><span class="sxs-lookup"><span data-stu-id="49d91-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="49d91-112">Řekněme například, že chcete po sbalení balíčku zkopírovat do sdílené síťové složky.</span><span class="sxs-lookup"><span data-stu-id="49d91-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="49d91-113">To lze provést přidáním následujícího do souboru projektu:</span><span class="sxs-lookup"><span data-stu-id="49d91-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="49d91-114">Podobně můžete napsat úlohu MSBuild, napsat vlastní cíl a využít vlastnosti NuGet v úloze MSBuild.</span><span class="sxs-lookup"><span data-stu-id="49d91-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="49d91-115">`$(OutputPath)` je relativní a očekává, že spouštíte příkaz z kořenového adresáře projektu.</span><span class="sxs-lookup"><span data-stu-id="49d91-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="49d91-116">cíl balíčku</span><span class="sxs-lookup"><span data-stu-id="49d91-116">pack target</span></span>

<span data-ttu-id="49d91-117">Pro .NET Standard projekty pomocí formátu PackageReference pomocí `msbuild -t:pack` Kreslení vstupů ze souboru projektu, který se má použít při vytváření balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="49d91-117">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="49d91-118">Následující tabulka popisuje vlastnosti nástroje MSBuild, které lze přidat do souboru projektu v rámci prvního `<PropertyGroup>` uzlu.</span><span class="sxs-lookup"><span data-stu-id="49d91-118">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="49d91-119">Tyto úpravy můžete snadno upravit v aplikaci Visual Studio 2017 a novějším kliknutím pravým tlačítkem myši na projekt a výběrem možnosti **Upravit {PROJECT_NAME}** v místní nabídce.</span><span class="sxs-lookup"><span data-stu-id="49d91-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="49d91-120">Pro přehlednost je tabulka uspořádaná podle ekvivalentní vlastnosti v [ `.nuspec` souboru](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="49d91-120">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="49d91-121">Všimněte si, že nástroj `Owners` `Summary` `.nuspec` MSBuild nepodporuje vlastnosti a.</span><span class="sxs-lookup"><span data-stu-id="49d91-121">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="49d91-122">Hodnota atributu/NuSpec</span><span class="sxs-lookup"><span data-stu-id="49d91-122">Attribute/NuSpec Value</span></span> | <span data-ttu-id="49d91-123">Vlastnost MSBuild</span><span class="sxs-lookup"><span data-stu-id="49d91-123">MSBuild Property</span></span> | <span data-ttu-id="49d91-124">Výchozí</span><span class="sxs-lookup"><span data-stu-id="49d91-124">Default</span></span> | <span data-ttu-id="49d91-125">Poznámky</span><span class="sxs-lookup"><span data-stu-id="49d91-125">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="49d91-126">Id</span><span class="sxs-lookup"><span data-stu-id="49d91-126">Id</span></span> | <span data-ttu-id="49d91-127">PackageId</span><span class="sxs-lookup"><span data-stu-id="49d91-127">PackageId</span></span> | <span data-ttu-id="49d91-128">Doplňk</span><span class="sxs-lookup"><span data-stu-id="49d91-128">AssemblyName</span></span> | <span data-ttu-id="49d91-129">$ (AssemblyName) z MSBuild</span><span class="sxs-lookup"><span data-stu-id="49d91-129">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="49d91-130">Verze</span><span class="sxs-lookup"><span data-stu-id="49d91-130">Version</span></span> | <span data-ttu-id="49d91-131">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="49d91-131">PackageVersion</span></span> | <span data-ttu-id="49d91-132">Verze</span><span class="sxs-lookup"><span data-stu-id="49d91-132">Version</span></span> | <span data-ttu-id="49d91-133">To je semver kompatibilní, například "1.0.0", "1.0.0-beta" nebo "1.0.0-beta-00345"</span><span class="sxs-lookup"><span data-stu-id="49d91-133">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="49d91-134">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="49d91-134">VersionPrefix</span></span> | <span data-ttu-id="49d91-135">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="49d91-135">PackageVersionPrefix</span></span> | <span data-ttu-id="49d91-136">empty</span><span class="sxs-lookup"><span data-stu-id="49d91-136">empty</span></span> | <span data-ttu-id="49d91-137">Nastavení PackageVersion přepsání PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="49d91-137">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="49d91-138">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="49d91-138">VersionSuffix</span></span> | <span data-ttu-id="49d91-139">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="49d91-139">PackageVersionSuffix</span></span> | <span data-ttu-id="49d91-140">empty</span><span class="sxs-lookup"><span data-stu-id="49d91-140">empty</span></span> | <span data-ttu-id="49d91-141">$ (VersionSuffix) z MSBuild.</span><span class="sxs-lookup"><span data-stu-id="49d91-141">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="49d91-142">Nastavení PackageVersion přepsání PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="49d91-142">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="49d91-143">Autoři</span><span class="sxs-lookup"><span data-stu-id="49d91-143">Authors</span></span> | <span data-ttu-id="49d91-144">Autoři</span><span class="sxs-lookup"><span data-stu-id="49d91-144">Authors</span></span> | <span data-ttu-id="49d91-145">Uživatelské jméno aktuálního uživatele</span><span class="sxs-lookup"><span data-stu-id="49d91-145">Username of the current user</span></span> | |
| <span data-ttu-id="49d91-146">Vlastníci</span><span class="sxs-lookup"><span data-stu-id="49d91-146">Owners</span></span> | <span data-ttu-id="49d91-147">–</span><span class="sxs-lookup"><span data-stu-id="49d91-147">N/A</span></span> | <span data-ttu-id="49d91-148">Nepřítomno v NuSpec</span><span class="sxs-lookup"><span data-stu-id="49d91-148">Not present in NuSpec</span></span> | |
| <span data-ttu-id="49d91-149">Nadpis</span><span class="sxs-lookup"><span data-stu-id="49d91-149">Title</span></span> | <span data-ttu-id="49d91-150">Nadpis</span><span class="sxs-lookup"><span data-stu-id="49d91-150">Title</span></span> | <span data-ttu-id="49d91-151">PackageId</span><span class="sxs-lookup"><span data-stu-id="49d91-151">The PackageId</span></span>| |
| <span data-ttu-id="49d91-152">Popis</span><span class="sxs-lookup"><span data-stu-id="49d91-152">Description</span></span> | <span data-ttu-id="49d91-153">Popis</span><span class="sxs-lookup"><span data-stu-id="49d91-153">Description</span></span> | <span data-ttu-id="49d91-154">Popis balíčku</span><span class="sxs-lookup"><span data-stu-id="49d91-154">"Package Description"</span></span> | |
| <span data-ttu-id="49d91-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="49d91-155">Copyright</span></span> | <span data-ttu-id="49d91-156">Copyright</span><span class="sxs-lookup"><span data-stu-id="49d91-156">Copyright</span></span> | <span data-ttu-id="49d91-157">empty</span><span class="sxs-lookup"><span data-stu-id="49d91-157">empty</span></span> | |
| <span data-ttu-id="49d91-158">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="49d91-158">RequireLicenseAcceptance</span></span> | <span data-ttu-id="49d91-159">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="49d91-159">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="49d91-160">false (nepravda)</span><span class="sxs-lookup"><span data-stu-id="49d91-160">false</span></span> | |
| <span data-ttu-id="49d91-161">license</span><span class="sxs-lookup"><span data-stu-id="49d91-161">license</span></span> | <span data-ttu-id="49d91-162">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="49d91-162">PackageLicenseExpression</span></span> | <span data-ttu-id="49d91-163">empty</span><span class="sxs-lookup"><span data-stu-id="49d91-163">empty</span></span> | <span data-ttu-id="49d91-164">Odpovídá `<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="49d91-164">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="49d91-165">license</span><span class="sxs-lookup"><span data-stu-id="49d91-165">license</span></span> | <span data-ttu-id="49d91-166">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="49d91-166">PackageLicenseFile</span></span> | <span data-ttu-id="49d91-167">empty</span><span class="sxs-lookup"><span data-stu-id="49d91-167">empty</span></span> | <span data-ttu-id="49d91-168">Odpovídá `<license type="file">` .</span><span class="sxs-lookup"><span data-stu-id="49d91-168">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="49d91-169">Musíte explicitně sbalit soubor s odkazem na licenci.</span><span class="sxs-lookup"><span data-stu-id="49d91-169">You need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="49d91-170">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="49d91-170">LicenseUrl</span></span> | <span data-ttu-id="49d91-171">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="49d91-171">PackageLicenseUrl</span></span> | <span data-ttu-id="49d91-172">empty</span><span class="sxs-lookup"><span data-stu-id="49d91-172">empty</span></span> | <span data-ttu-id="49d91-173">`PackageLicenseUrl` je zastaralá, použijte vlastnost PackageLicenseExpression nebo PackageLicenseFile.</span><span class="sxs-lookup"><span data-stu-id="49d91-173">`PackageLicenseUrl` is deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="49d91-174">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="49d91-174">ProjectUrl</span></span> | <span data-ttu-id="49d91-175">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="49d91-175">PackageProjectUrl</span></span> | <span data-ttu-id="49d91-176">empty</span><span class="sxs-lookup"><span data-stu-id="49d91-176">empty</span></span> | |
| <span data-ttu-id="49d91-177">Ikona</span><span class="sxs-lookup"><span data-stu-id="49d91-177">Icon</span></span> | <span data-ttu-id="49d91-178">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="49d91-178">PackageIcon</span></span> | <span data-ttu-id="49d91-179">empty</span><span class="sxs-lookup"><span data-stu-id="49d91-179">empty</span></span> | <span data-ttu-id="49d91-180">Musíte explicitně sbalit soubor obrázku odkazované ikony.</span><span class="sxs-lookup"><span data-stu-id="49d91-180">You need to explicitly pack the referenced icon image file.</span></span>|
| <span data-ttu-id="49d91-181">IconUrl</span><span class="sxs-lookup"><span data-stu-id="49d91-181">IconUrl</span></span> | <span data-ttu-id="49d91-182">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="49d91-182">PackageIconUrl</span></span> | <span data-ttu-id="49d91-183">empty</span><span class="sxs-lookup"><span data-stu-id="49d91-183">empty</span></span> | <span data-ttu-id="49d91-184">Pro dosažení nejlepšího prostředí pro starší verze `PackageIconUrl` by se mělo zadat kromě `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="49d91-184">For the best downlevel experience, `PackageIconUrl` should be specified in addition to `PackageIcon`.</span></span> <span data-ttu-id="49d91-185">Delší období, `PackageIconUrl` bude zastaralé.</span><span class="sxs-lookup"><span data-stu-id="49d91-185">Longer term, `PackageIconUrl` will be deprecated.</span></span> |
| <span data-ttu-id="49d91-186">Značky</span><span class="sxs-lookup"><span data-stu-id="49d91-186">Tags</span></span> | <span data-ttu-id="49d91-187">PackageTags</span><span class="sxs-lookup"><span data-stu-id="49d91-187">PackageTags</span></span> | <span data-ttu-id="49d91-188">empty</span><span class="sxs-lookup"><span data-stu-id="49d91-188">empty</span></span> | <span data-ttu-id="49d91-189">Značky jsou středníky odděleny středníkem.</span><span class="sxs-lookup"><span data-stu-id="49d91-189">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="49d91-190">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="49d91-190">ReleaseNotes</span></span> | <span data-ttu-id="49d91-191">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="49d91-191">PackageReleaseNotes</span></span> | <span data-ttu-id="49d91-192">empty</span><span class="sxs-lookup"><span data-stu-id="49d91-192">empty</span></span> | |
| <span data-ttu-id="49d91-193">Úložiště/adresa URL</span><span class="sxs-lookup"><span data-stu-id="49d91-193">Repository/Url</span></span> | <span data-ttu-id="49d91-194">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="49d91-194">RepositoryUrl</span></span> | <span data-ttu-id="49d91-195">empty</span><span class="sxs-lookup"><span data-stu-id="49d91-195">empty</span></span> | <span data-ttu-id="49d91-196">Adresa URL úložiště, která se používá k klonování nebo načtení zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="49d91-196">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="49d91-197">Případě *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="49d91-197">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="49d91-198">Úložiště/typ</span><span class="sxs-lookup"><span data-stu-id="49d91-198">Repository/Type</span></span> | <span data-ttu-id="49d91-199">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="49d91-199">RepositoryType</span></span> | <span data-ttu-id="49d91-200">empty</span><span class="sxs-lookup"><span data-stu-id="49d91-200">empty</span></span> | <span data-ttu-id="49d91-201">Typ úložiště</span><span class="sxs-lookup"><span data-stu-id="49d91-201">Repository type.</span></span> <span data-ttu-id="49d91-202">Příklady: *Git*, *TFS*.</span><span class="sxs-lookup"><span data-stu-id="49d91-202">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="49d91-203">Úložiště/větev</span><span class="sxs-lookup"><span data-stu-id="49d91-203">Repository/Branch</span></span> | <span data-ttu-id="49d91-204">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="49d91-204">RepositoryBranch</span></span> | <span data-ttu-id="49d91-205">empty</span><span class="sxs-lookup"><span data-stu-id="49d91-205">empty</span></span> | <span data-ttu-id="49d91-206">Volitelné informace o větvi úložiště</span><span class="sxs-lookup"><span data-stu-id="49d91-206">Optional repository branch information.</span></span> <span data-ttu-id="49d91-207">Pro zahrnutí této vlastnosti je nutné zadat také *RepositoryUrl* .</span><span class="sxs-lookup"><span data-stu-id="49d91-207">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="49d91-208">Příklad: *Master* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="49d91-208">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="49d91-209">Úložiště/potvrzení změn</span><span class="sxs-lookup"><span data-stu-id="49d91-209">Repository/Commit</span></span> | <span data-ttu-id="49d91-210">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="49d91-210">RepositoryCommit</span></span> | <span data-ttu-id="49d91-211">empty</span><span class="sxs-lookup"><span data-stu-id="49d91-211">empty</span></span> | <span data-ttu-id="49d91-212">Volitelné potvrzení změn úložiště nebo sada změn, které označují, na který zdroj byl balíček vytvořen.</span><span class="sxs-lookup"><span data-stu-id="49d91-212">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="49d91-213">Pro zahrnutí této vlastnosti je nutné zadat také *RepositoryUrl* .</span><span class="sxs-lookup"><span data-stu-id="49d91-213">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="49d91-214">Příklad: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="49d91-214">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="49d91-215">PackageType</span><span class="sxs-lookup"><span data-stu-id="49d91-215">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="49d91-216">Souhrn</span><span class="sxs-lookup"><span data-stu-id="49d91-216">Summary</span></span> | <span data-ttu-id="49d91-217">Nepodporováno</span><span class="sxs-lookup"><span data-stu-id="49d91-217">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="49d91-218">cílové vstupy balení</span><span class="sxs-lookup"><span data-stu-id="49d91-218">pack target inputs</span></span>

- <span data-ttu-id="49d91-219">Ispackable nastavenou</span><span class="sxs-lookup"><span data-stu-id="49d91-219">IsPackable</span></span>
- <span data-ttu-id="49d91-220">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="49d91-220">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="49d91-221">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="49d91-221">PackageVersion</span></span>
- <span data-ttu-id="49d91-222">PackageId</span><span class="sxs-lookup"><span data-stu-id="49d91-222">PackageId</span></span>
- <span data-ttu-id="49d91-223">Autoři</span><span class="sxs-lookup"><span data-stu-id="49d91-223">Authors</span></span>
- <span data-ttu-id="49d91-224">Popis</span><span class="sxs-lookup"><span data-stu-id="49d91-224">Description</span></span>
- <span data-ttu-id="49d91-225">Copyright</span><span class="sxs-lookup"><span data-stu-id="49d91-225">Copyright</span></span>
- <span data-ttu-id="49d91-226">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="49d91-226">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="49d91-227">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="49d91-227">DevelopmentDependency</span></span>
- <span data-ttu-id="49d91-228">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="49d91-228">PackageLicenseExpression</span></span>
- <span data-ttu-id="49d91-229">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="49d91-229">PackageLicenseFile</span></span>
- <span data-ttu-id="49d91-230">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="49d91-230">PackageLicenseUrl</span></span>
- <span data-ttu-id="49d91-231">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="49d91-231">PackageProjectUrl</span></span>
- <span data-ttu-id="49d91-232">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="49d91-232">PackageIconUrl</span></span>
- <span data-ttu-id="49d91-233">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="49d91-233">PackageReleaseNotes</span></span>
- <span data-ttu-id="49d91-234">PackageTags</span><span class="sxs-lookup"><span data-stu-id="49d91-234">PackageTags</span></span>
- <span data-ttu-id="49d91-235">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="49d91-235">PackageOutputPath</span></span>
- <span data-ttu-id="49d91-236">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="49d91-236">IncludeSymbols</span></span>
- <span data-ttu-id="49d91-237">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="49d91-237">IncludeSource</span></span>
- <span data-ttu-id="49d91-238">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="49d91-238">PackageTypes</span></span>
- <span data-ttu-id="49d91-239">Nástroj</span><span class="sxs-lookup"><span data-stu-id="49d91-239">IsTool</span></span>
- <span data-ttu-id="49d91-240">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="49d91-240">RepositoryUrl</span></span>
- <span data-ttu-id="49d91-241">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="49d91-241">RepositoryType</span></span>
- <span data-ttu-id="49d91-242">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="49d91-242">RepositoryBranch</span></span>
- <span data-ttu-id="49d91-243">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="49d91-243">RepositoryCommit</span></span>
- <span data-ttu-id="49d91-244">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="49d91-244">NoPackageAnalysis</span></span>
- <span data-ttu-id="49d91-245">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="49d91-245">MinClientVersion</span></span>
- <span data-ttu-id="49d91-246">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="49d91-246">IncludeBuildOutput</span></span>
- <span data-ttu-id="49d91-247">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="49d91-247">IncludeContentInPack</span></span>
- <span data-ttu-id="49d91-248">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="49d91-248">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="49d91-249">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="49d91-249">ContentTargetFolders</span></span>
- <span data-ttu-id="49d91-250">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="49d91-250">NuspecFile</span></span>
- <span data-ttu-id="49d91-251">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="49d91-251">NuspecBasePath</span></span>
- <span data-ttu-id="49d91-252">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="49d91-252">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="49d91-253">scénáře sady Pack</span><span class="sxs-lookup"><span data-stu-id="49d91-253">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="49d91-254">Potlačit závislosti</span><span class="sxs-lookup"><span data-stu-id="49d91-254">Suppress dependencies</span></span>

<span data-ttu-id="49d91-255">Chcete-li potlačit závislosti balíčků z vygenerovaného balíčku NuGet, nastavte na to, `SuppressDependenciesWhenPacking` `true` které umožní přeskočí všechny závislosti ze generovaného souboru nupkg.</span><span class="sxs-lookup"><span data-stu-id="49d91-255">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="49d91-256">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="49d91-256">PackageIconUrl</span></span>

<span data-ttu-id="49d91-257">`PackageIconUrl` se bude zastaralá za novou [`PackageIcon`](#packageicon) vlastnost.</span><span class="sxs-lookup"><span data-stu-id="49d91-257">`PackageIconUrl` will be deprecated in favor of the new [`PackageIcon`](#packageicon) property.</span></span>

<span data-ttu-id="49d91-258">Počínaje verzí NuGet 5,3 & Visual Studio 2019 verze 16,3, `pack` vyvolá upozornění [NU5048](./errors-and-warnings/nu5048.md) , pokud se jenom metadata balíčku zanesou `PackageIconUrl` .</span><span class="sxs-lookup"><span data-stu-id="49d91-258">Starting with NuGet 5.3 & Visual Studio 2019 version 16.3, `pack` will raise [NU5048](./errors-and-warnings/nu5048.md) warning if the package metadata only specifies `PackageIconUrl`.</span></span>

### <a name="packageicon"></a><span data-ttu-id="49d91-259">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="49d91-259">PackageIcon</span></span>

> [!Tip]
> <span data-ttu-id="49d91-260">Měli byste zadat obojí `PackageIcon` a `PackageIconUrl` pro zajištění zpětné kompatibility se klienty a zdroji, které ještě nepodporují `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="49d91-260">You should specify both `PackageIcon` and `PackageIconUrl` to maintain backward compatibility with clients and sources that do not yet support `PackageIcon`.</span></span> <span data-ttu-id="49d91-261">Visual Studio bude podporovat `PackageIcon` balíčky ze zdroje založeného na složce v budoucí verzi.</span><span class="sxs-lookup"><span data-stu-id="49d91-261">Visual Studio will support `PackageIcon` for packages coming from a folder-based source in a future release.</span></span>

#### <a name="packing-an-icon-image-file"></a><span data-ttu-id="49d91-262">Balení souboru obrázku ikony</span><span class="sxs-lookup"><span data-stu-id="49d91-262">Packing an icon image file</span></span>

<span data-ttu-id="49d91-263">Při balení souboru obrázku ikony je nutné použít `PackageIcon` vlastnost k určení cesty k balíčku vzhledem k kořenu balíčku.</span><span class="sxs-lookup"><span data-stu-id="49d91-263">When packing an icon image file, you need to use `PackageIcon` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="49d91-264">Kromě toho je nutné zajistit, aby byl soubor zahrnut do balíčku.</span><span class="sxs-lookup"><span data-stu-id="49d91-264">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="49d91-265">Velikost souboru obrázku je omezená na 1 MB.</span><span class="sxs-lookup"><span data-stu-id="49d91-265">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="49d91-266">Podporované formáty souborů zahrnují JPEG a PNG.</span><span class="sxs-lookup"><span data-stu-id="49d91-266">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="49d91-267">Doporučujeme, abyste 128 × 128 rozlišení obrazu.</span><span class="sxs-lookup"><span data-stu-id="49d91-267">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="49d91-268">Příklad:</span><span class="sxs-lookup"><span data-stu-id="49d91-268">For example:</span></span>

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

<span data-ttu-id="49d91-269">[Ukázka ikony balíčku](https://github.com/NuGet/Samples/tree/master/PackageIconExample)</span><span class="sxs-lookup"><span data-stu-id="49d91-269">[Package Icon sample](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span></span>

<span data-ttu-id="49d91-270">Pro ekvivalent nuspec se podívejte na [nuspec reference pro Icon](nuspec.md#icon).</span><span class="sxs-lookup"><span data-stu-id="49d91-270">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="49d91-271">Výstupní sestavení</span><span class="sxs-lookup"><span data-stu-id="49d91-271">Output assemblies</span></span>

<span data-ttu-id="49d91-272">`nuget pack` zkopíruje výstupní soubory s příponami,,,, `.exe` `.dll` `.xml` `.winmd` `.json` a `.pri` .</span><span class="sxs-lookup"><span data-stu-id="49d91-272">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="49d91-273">Výstupní soubory, které jsou zkopírovány, závisí na tom, co nástroj MSBuild poskytuje z `BuiltOutputProjectGroup` cíle.</span><span class="sxs-lookup"><span data-stu-id="49d91-273">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="49d91-274">Existují dvě vlastnosti nástroje MSBuild, které lze použít v souboru projektu nebo na příkazovém řádku pro řízení, kde výstupní sestavení jdou:</span><span class="sxs-lookup"><span data-stu-id="49d91-274">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="49d91-275">`IncludeBuildOutput`: Logická hodnota, která určuje, zda mají být do balíčku zahrnuty výstupní sestavení sestavení.</span><span class="sxs-lookup"><span data-stu-id="49d91-275">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="49d91-276">`BuildOutputTargetFolder`: Určuje složku, do které se mají umístit výstupní sestavení.</span><span class="sxs-lookup"><span data-stu-id="49d91-276">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="49d91-277">Výstupní sestavení (a další výstupní soubory) se zkopírují do příslušných složek rozhraní.</span><span class="sxs-lookup"><span data-stu-id="49d91-277">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="49d91-278">Odkazy na balíčky</span><span class="sxs-lookup"><span data-stu-id="49d91-278">Package references</span></span>

<span data-ttu-id="49d91-279">Viz [odkazy na balíčky v souborech projektu](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="49d91-279">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="49d91-280">Odkazy na projekt a projekt</span><span class="sxs-lookup"><span data-stu-id="49d91-280">Project to project references</span></span>

<span data-ttu-id="49d91-281">Odkazy na projekt na projekt jsou ve výchozím nastavení považovány za odkazy na balíčky NuGet, například:</span><span class="sxs-lookup"><span data-stu-id="49d91-281">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="49d91-282">Do odkazu na projekt můžete také přidat následující metadata:</span><span class="sxs-lookup"><span data-stu-id="49d91-282">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="49d91-283">Zahrnutí obsahu do balíčku</span><span class="sxs-lookup"><span data-stu-id="49d91-283">Including content in a package</span></span>

<span data-ttu-id="49d91-284">Chcete-li zahrnout obsah, přidejte do existující položky metadata navíc `<Content>` .</span><span class="sxs-lookup"><span data-stu-id="49d91-284">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="49d91-285">Ve výchozím nastavení jsou všechny položky typu "obsah" zahrnuty do balíčku, Pokud nepřepíšete záznamy podobné následujícímu:</span><span class="sxs-lookup"><span data-stu-id="49d91-285">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="49d91-286">Ve výchozím nastavení je vše přidáno do kořenu `content` a `contentFiles\any\<target_framework>` složky v rámci balíčku a zachovává strukturu relativních složek, pokud nezadáte cestu k balíčku:</span><span class="sxs-lookup"><span data-stu-id="49d91-286">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="49d91-287">Pokud chcete kopírovat veškerý obsah pouze na konkrétní kořenové složky (místo `content` a `contentFiles` obojí), můžete použít vlastnost MSBuild `ContentTargetFolders` , která má výchozí hodnotu Content; contentFiles, ale lze ji nastavit na jiné názvy složek.</span><span class="sxs-lookup"><span data-stu-id="49d91-287">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="49d91-288">Všimněte si, že pouze zadání "contentFiles" v `ContentTargetFolders` souboru vloží soubory do `contentFiles\any\<target_framework>` nebo na `contentFiles\<language>\<target_framework>` základě `buildAction` .</span><span class="sxs-lookup"><span data-stu-id="49d91-288">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="49d91-289">`PackagePath` může se jednat o sadu cílových cest oddělených středníky.</span><span class="sxs-lookup"><span data-stu-id="49d91-289">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="49d91-290">Zadáním prázdné cesty k balíčku by se soubor přidal do kořenového adresáře balíčku.</span><span class="sxs-lookup"><span data-stu-id="49d91-290">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="49d91-291">Například následující příkaz přidá `libuv.txt` do `content\myfiles` , `content\samples` a kořenovou složku balíčku:</span><span class="sxs-lookup"><span data-stu-id="49d91-291">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="49d91-292">K dispozici je také vlastnost MSBuild `$(IncludeContentInPack)` , která má výchozí hodnotu `true` .</span><span class="sxs-lookup"><span data-stu-id="49d91-292">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="49d91-293">Pokud je nastavená na `false` libovolný projekt, pak obsah z tohoto projektu není zahrnutý v balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="49d91-293">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="49d91-294">Další metadata specifická pro sadu, která můžete nastavit na kterékoli z výše uvedených položek, zahrnují ```<PackageCopyToOutput>``` a ```<PackageFlatten>``` které sady ```CopyToOutput``` a ```Flatten``` hodnoty pro ```contentFiles``` položku ve výstupních nuspec.</span><span class="sxs-lookup"><span data-stu-id="49d91-294">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="49d91-295">Kromě položek obsahu `<Pack>` `<PackagePath>` lze metadata a také nastavit na soubory s akcí sestavení kompilovat, EmbeddedResource, ApplicationDefinition, Page, Resource, třídy SplashScreen, vazbě designdata, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource nebo None.</span><span class="sxs-lookup"><span data-stu-id="49d91-295">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="49d91-296">Pokud má balíček při použití vzorů expanze názvů připojit název souboru k cestě k balíčku, musí cesta k balíčku končit znakem oddělovače složky. v opačném případě se cesta k balíčku považuje za úplnou cestu včetně názvu souboru.</span><span class="sxs-lookup"><span data-stu-id="49d91-296">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="49d91-297">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="49d91-297">IncludeSymbols</span></span>

<span data-ttu-id="49d91-298">Při použití se `MSBuild -t:pack -p:IncludeSymbols=true` `.pdb` zkopírují odpovídající soubory spolu s jinými výstupními soubory ( `.dll` , `.exe` , `.winmd` , `.xml` , `.json` , `.pri` ).</span><span class="sxs-lookup"><span data-stu-id="49d91-298">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="49d91-299">Všimněte si, že nastavení `IncludeSymbols=true` vytvoří regulární balíček *a* balíček symbolů.</span><span class="sxs-lookup"><span data-stu-id="49d91-299">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="49d91-300">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="49d91-300">IncludeSource</span></span>

<span data-ttu-id="49d91-301">To je stejné jako `IncludeSymbols` s tím rozdílem, že kopíruje také zdrojové soubory spolu se `.pdb` soubory.</span><span class="sxs-lookup"><span data-stu-id="49d91-301">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="49d91-302">Všechny soubory typu `Compile` jsou zkopírovány za účelem `src\<ProjectName>\` zachování struktury složek relativní cesty ve výsledném balíčku.</span><span class="sxs-lookup"><span data-stu-id="49d91-302">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="49d91-303">Totéž se také stane u zdrojových souborů, `ProjectReference` které mají `TreatAsPackageReference` nastavené na `false` .</span><span class="sxs-lookup"><span data-stu-id="49d91-303">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="49d91-304">Pokud je soubor typu Compile mimo složku projektu, pak je pouze přidán do `src\<ProjectName>\` .</span><span class="sxs-lookup"><span data-stu-id="49d91-304">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="49d91-305">Balení licenčního výrazu nebo licenčního souboru</span><span class="sxs-lookup"><span data-stu-id="49d91-305">Packing a license expression or a license file</span></span>

<span data-ttu-id="49d91-306">Při použití licenčního výrazu by se měla použít vlastnost PackageLicenseExpression.</span><span class="sxs-lookup"><span data-stu-id="49d91-306">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="49d91-307">[Ukázka licenčního výrazu](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="49d91-307">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="49d91-308">[Přečtěte si další informace o výrazech licencí a licencích, které jsou přijaty nástrojem NuGet.org](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="49d91-308">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="49d91-309">Při balení licenčního souboru musíte použít vlastnost PackageLicenseFile a zadat cestu k balíčku relativní ke kořenu balíčku.</span><span class="sxs-lookup"><span data-stu-id="49d91-309">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="49d91-310">Kromě toho je nutné zajistit, aby byl soubor zahrnut do balíčku.</span><span class="sxs-lookup"><span data-stu-id="49d91-310">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="49d91-311">Příklad:</span><span class="sxs-lookup"><span data-stu-id="49d91-311">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="49d91-312">[Ukázka licenčního souboru](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="49d91-312">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="49d91-313">Nástroj</span><span class="sxs-lookup"><span data-stu-id="49d91-313">IsTool</span></span>

<span data-ttu-id="49d91-314">Při použití `MSBuild -t:pack -p:IsTool=true` aplikace jsou všechny výstupní soubory, jak je uvedeno ve scénáři [výstup sestavení](#output-assemblies) , zkopírovány do `tools` složky namísto `lib` složky.</span><span class="sxs-lookup"><span data-stu-id="49d91-314">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="49d91-315">Všimněte si, že se liší od a, `DotNetCliTool` který je určen nastavením `PackageType` v `.csproj` souboru.</span><span class="sxs-lookup"><span data-stu-id="49d91-315">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="49d91-316">Balení pomocí. nuspec</span><span class="sxs-lookup"><span data-stu-id="49d91-316">Packing using a .nuspec</span></span>

<span data-ttu-id="49d91-317">I když se místo toho doporučuje [Zahrnout všechny vlastnosti](../reference/msbuild-targets.md#pack-target) , které jsou obvykle v `.nuspec` souboru v souboru projektu, můžete zvolit použití `.nuspec` souboru k balení projektu.</span><span class="sxs-lookup"><span data-stu-id="49d91-317">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="49d91-318">Pro projekt bez sady SDK, který používá, je `PackageReference` nutné importovat, `NuGet.Build.Tasks.Pack.targets` aby bylo možné spustit úlohu balíčku.</span><span class="sxs-lookup"><span data-stu-id="49d91-318">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="49d91-319">Před zabalením souboru nuspec je ještě nutné projekt obnovit.</span><span class="sxs-lookup"><span data-stu-id="49d91-319">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="49d91-320">(Projekt ve stylu sady SDK obsahuje cíle balíčku ve výchozím nastavení.)</span><span class="sxs-lookup"><span data-stu-id="49d91-320">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="49d91-321">Cílová architektura souboru projektu je nerelevantní a při balení nuspec se nepoužívá.</span><span class="sxs-lookup"><span data-stu-id="49d91-321">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="49d91-322">Následující tři vlastnosti MSBuild jsou relevantní pro balení pomocí `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="49d91-322">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="49d91-323">`NuspecFile`: relativní nebo absolutní cesta k `.nuspec` souboru, který se používá k balení.</span><span class="sxs-lookup"><span data-stu-id="49d91-323">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="49d91-324">`NuspecProperties`: středníkem oddělený seznam dvojic klíč = hodnota.</span><span class="sxs-lookup"><span data-stu-id="49d91-324">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="49d91-325">Kvůli způsobu, jakým funguje analýza příkazového řádku nástroje MSBuild, je nutné zadat více vlastností následujícím způsobem: `-p:NuspecProperties="key1=value1;key2=value2"` .</span><span class="sxs-lookup"><span data-stu-id="49d91-325">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties="key1=value1;key2=value2"`.</span></span>  
1. <span data-ttu-id="49d91-326">`NuspecBasePath`: Základní cesta k `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="49d91-326">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="49d91-327">Pokud používáte `dotnet.exe` k balení projektu, použijte příkaz podobný následujícímu:</span><span class="sxs-lookup"><span data-stu-id="49d91-327">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="49d91-328">Při použití nástroje MSBuild k sbalení projektu použijte příkaz podobný následujícímu:</span><span class="sxs-lookup"><span data-stu-id="49d91-328">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="49d91-329">Všimněte si prosím, že balení nuspec pomocí dotnet.exe nebo MSBuild také vede k sestavení projektu ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="49d91-329">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="49d91-330">K tomu je možné se vyhnout předáním ```--no-build``` vlastnosti do dotnet.exe, což je ekvivalent nastavení ```<NoBuild>true</NoBuild> ``` v souboru projektu spolu s nastavením ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="49d91-330">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="49d91-331">Příkladem souboru *. csproj* pro zabalení souboru nuspec je:</span><span class="sxs-lookup"><span data-stu-id="49d91-331">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="49d91-332">Rozšířené body rozšíření pro vytvoření přizpůsobeného balíčku</span><span class="sxs-lookup"><span data-stu-id="49d91-332">Advanced extension points to create customized package</span></span>

<span data-ttu-id="49d91-333">`pack`Cíl poskytuje dva Rozšiřovací body, které jsou spuštěny v sestavení specifickém pro vnitřní, cílové rozhraní.</span><span class="sxs-lookup"><span data-stu-id="49d91-333">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="49d91-334">Rozšiřující body podporují obsah a sestavení konkrétního cílového rozhraní do balíčku:</span><span class="sxs-lookup"><span data-stu-id="49d91-334">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="49d91-335">`TargetsForTfmSpecificBuildOutput` cíl: použijte pro soubory uvnitř `lib` složky nebo složky zadané pomocí `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="49d91-335">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="49d91-336">`TargetsForTfmSpecificContentInPackage` cíl: použijte pro soubory mimo `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="49d91-336">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="49d91-337">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="49d91-337">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="49d91-338">Napište vlastní cíl a zadejte ho jako hodnotu `$(TargetsForTfmSpecificBuildOutput)` Vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="49d91-338">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="49d91-339">Pro všechny soubory, které potřebují přejít do nástroje `BuildOutputTargetFolder` (ve výchozím nastavení lib), by měl cíl zapisovat tyto soubory do skupiny Item `BuildOutputInPackage` a nastavit následující dvě hodnoty metadat:</span><span class="sxs-lookup"><span data-stu-id="49d91-339">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="49d91-340">`FinalOutputPath`: Absolutní cesta k souboru; Pokud není zadaný, použije se identita k vyhodnocení zdrojové cesty.</span><span class="sxs-lookup"><span data-stu-id="49d91-340">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="49d91-341">`TargetPath`: (Volitelné) nastavte, kdy bude soubor potřebovat přejít do podsložky v rámci `lib\<TargetFramework>` , jako jsou satelitní sestavení, která se nacházejí v odpovídajících složkách kultury.</span><span class="sxs-lookup"><span data-stu-id="49d91-341">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="49d91-342">Výchozí hodnota je název souboru.</span><span class="sxs-lookup"><span data-stu-id="49d91-342">Defaults to the name of the file.</span></span>

<span data-ttu-id="49d91-343">Příklad:</span><span class="sxs-lookup"><span data-stu-id="49d91-343">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="49d91-344">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="49d91-344">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="49d91-345">Napište vlastní cíl a zadejte ho jako hodnotu `$(TargetsForTfmSpecificContentInPackage)` Vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="49d91-345">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="49d91-346">U všech souborů, které se mají zahrnout do balíčku, by měl cíl tyto soubory zapsat do `TfmSpecificPackageFile` skupiny položek a nastavit následující volitelná metadata:</span><span class="sxs-lookup"><span data-stu-id="49d91-346">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="49d91-347">`PackagePath`: Cesta, kde by měl být v balíčku výstup souboru.</span><span class="sxs-lookup"><span data-stu-id="49d91-347">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="49d91-348">Při přidání více než jednoho souboru do stejné cesty k balíčku vyvolá NuGet vystavení upozornění.</span><span class="sxs-lookup"><span data-stu-id="49d91-348">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="49d91-349">`BuildAction`: Akce sestavení, která se má souboru přiřadit, se vyžaduje jenom v případě, že je cesta k balíčku ve `contentFiles` složce.</span><span class="sxs-lookup"><span data-stu-id="49d91-349">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="49d91-350">Výchozí hodnota je None.</span><span class="sxs-lookup"><span data-stu-id="49d91-350">Defaults to "None".</span></span>

<span data-ttu-id="49d91-351">Příklad:</span><span class="sxs-lookup"><span data-stu-id="49d91-351">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="49d91-352">cíl obnovení</span><span class="sxs-lookup"><span data-stu-id="49d91-352">restore target</span></span>

<span data-ttu-id="49d91-353">`MSBuild -t:restore` (které `nuget restore` a `dotnet restore` používají se v projektech .NET Core), obnoví balíčky, na které se odkazuje v souboru projektu, takto:</span><span class="sxs-lookup"><span data-stu-id="49d91-353">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="49d91-354">Číst všechny odkazy z projektu na projekt</span><span class="sxs-lookup"><span data-stu-id="49d91-354">Read all project to project references</span></span>
1. <span data-ttu-id="49d91-355">Přečtěte si vlastnosti projektu a najděte mezilehlé složky a cílová rozhraní.</span><span class="sxs-lookup"><span data-stu-id="49d91-355">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="49d91-356">Předání dat nástroje MSBuild do NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="49d91-356">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="49d91-357">Spustit obnovení</span><span class="sxs-lookup"><span data-stu-id="49d91-357">Run restore</span></span>
1. <span data-ttu-id="49d91-358">Stáhnout balíčky</span><span class="sxs-lookup"><span data-stu-id="49d91-358">Download packages</span></span>
1. <span data-ttu-id="49d91-359">Zápis souboru prostředků, cílů a vlastností props</span><span class="sxs-lookup"><span data-stu-id="49d91-359">Write assets file, targets, and props</span></span>

<span data-ttu-id="49d91-360">`restore`Cíl funguje pro projekty, které používají formát PackageReference.</span><span class="sxs-lookup"><span data-stu-id="49d91-360">The `restore` target works for projects using the PackageReference format.</span></span>
<span data-ttu-id="49d91-361">`MSBuild 16.5+` má také [podporu](#restoring-packagereference-and-packages.config-with-msbuild) pro `packages.config` formát.</span><span class="sxs-lookup"><span data-stu-id="49d91-361">`MSBuild 16.5+` also has [opt-in support](#restoring-packagereference-and-packages.config-with-msbuild) for the `packages.config` format.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="49d91-362">Obnovit vlastnosti</span><span class="sxs-lookup"><span data-stu-id="49d91-362">Restore properties</span></span>

<span data-ttu-id="49d91-363">Další nastavení obnovení může pocházet z vlastností MSBuild v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="49d91-363">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="49d91-364">Hodnoty lze také nastavit z příkazového řádku pomocí `-p:` přepínače (viz příklady níže).</span><span class="sxs-lookup"><span data-stu-id="49d91-364">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="49d91-365">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="49d91-365">Property</span></span> | <span data-ttu-id="49d91-366">Popis</span><span class="sxs-lookup"><span data-stu-id="49d91-366">Description</span></span> |
|--------|--------|
| <span data-ttu-id="49d91-367">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="49d91-367">RestoreSources</span></span> | <span data-ttu-id="49d91-368">Seznam zdrojů balíčků oddělených středníkem.</span><span class="sxs-lookup"><span data-stu-id="49d91-368">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="49d91-369">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="49d91-369">RestorePackagesPath</span></span> | <span data-ttu-id="49d91-370">Cesta ke složce uživatelských balíčků</span><span class="sxs-lookup"><span data-stu-id="49d91-370">User packages folder path.</span></span> |
| <span data-ttu-id="49d91-371">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="49d91-371">RestoreDisableParallel</span></span> | <span data-ttu-id="49d91-372">Omezit stahování na jednu po druhé.</span><span class="sxs-lookup"><span data-stu-id="49d91-372">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="49d91-373">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="49d91-373">RestoreConfigFile</span></span> | <span data-ttu-id="49d91-374">Cesta k `Nuget.Config` souboru, který se má použít</span><span class="sxs-lookup"><span data-stu-id="49d91-374">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="49d91-375">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="49d91-375">RestoreNoCache</span></span> | <span data-ttu-id="49d91-376">Je-li nastavena hodnota true, nepoužívejte balíčky uložené v mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="49d91-376">If true, avoids using cached packages.</span></span> <span data-ttu-id="49d91-377">Viz [Správa globálních balíčků a složek mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="49d91-377">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="49d91-378">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="49d91-378">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="49d91-379">Pokud má hodnotu true, ignoruje neúspěšné nebo chybějící zdroje balíčků.</span><span class="sxs-lookup"><span data-stu-id="49d91-379">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="49d91-380">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="49d91-380">RestoreFallbackFolders</span></span> | <span data-ttu-id="49d91-381">Záložní složky používané ve stejném způsobu, jakým se používá složka uživatelských balíčků.</span><span class="sxs-lookup"><span data-stu-id="49d91-381">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="49d91-382">RestoreAdditionalProjectSources</span><span class="sxs-lookup"><span data-stu-id="49d91-382">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="49d91-383">Další zdroje, které se mají použít při obnovení.</span><span class="sxs-lookup"><span data-stu-id="49d91-383">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="49d91-384">RestoreAdditionalProjectFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="49d91-384">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="49d91-385">Další záložní složky, které se mají použít při obnovení</span><span class="sxs-lookup"><span data-stu-id="49d91-385">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="49d91-386">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="49d91-386">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="49d91-387">Vyloučí záložní složky zadané v `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="49d91-387">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="49d91-388">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="49d91-388">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="49d91-389">Cesta k `NuGet.Build.Tasks.dll` .</span><span class="sxs-lookup"><span data-stu-id="49d91-389">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="49d91-390">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="49d91-390">RestoreGraphProjectInput</span></span> | <span data-ttu-id="49d91-391">Středníkem oddělený seznam projektů, které mají být obnoveny, které by měly obsahovat absolutní cesty.</span><span class="sxs-lookup"><span data-stu-id="49d91-391">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="49d91-392">RestoreUseSkipNonexistentTargets</span><span class="sxs-lookup"><span data-stu-id="49d91-392">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="49d91-393">Když jsou projekty shromažďovány pomocí nástroje MSBuild, určuje, zda jsou shromažďovány pomocí `SkipNonexistentTargets` optimalizace.</span><span class="sxs-lookup"><span data-stu-id="49d91-393">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="49d91-394">Pokud není nastaveno, výchozí hodnota je `true` .</span><span class="sxs-lookup"><span data-stu-id="49d91-394">When not set, defaults to `true`.</span></span> <span data-ttu-id="49d91-395">Příčinou je rychlé chování při selhání, když cíle projektu nelze importovat.</span><span class="sxs-lookup"><span data-stu-id="49d91-395">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="49d91-396">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="49d91-396">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="49d91-397">Výstupní složka, výchozí nastavení `BaseIntermediateOutputPath` a `obj` Složka.</span><span class="sxs-lookup"><span data-stu-id="49d91-397">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| <span data-ttu-id="49d91-398">RestoreForce</span><span class="sxs-lookup"><span data-stu-id="49d91-398">RestoreForce</span></span> | <span data-ttu-id="49d91-399">V projektech založených na PackageReference vynutí vyřešení všech závislostí i v případě, že bylo poslední obnovení úspěšné.</span><span class="sxs-lookup"><span data-stu-id="49d91-399">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="49d91-400">Zadání tohoto příznaku se podobá odstranění `project.assets.json` souboru.</span><span class="sxs-lookup"><span data-stu-id="49d91-400">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="49d91-401">To neobejde mezipaměť HTTP-cache.</span><span class="sxs-lookup"><span data-stu-id="49d91-401">This does not bypass the http-cache.</span></span> |
| <span data-ttu-id="49d91-402">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="49d91-402">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="49d91-403">Výslovný se na použití souboru zámku.</span><span class="sxs-lookup"><span data-stu-id="49d91-403">Opts into the usage of a lock file.</span></span> |
| <span data-ttu-id="49d91-404">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="49d91-404">RestoreLockedMode</span></span> | <span data-ttu-id="49d91-405">Spustit obnovení v uzamčeném režimu.</span><span class="sxs-lookup"><span data-stu-id="49d91-405">Run restore in locked mode.</span></span> <span data-ttu-id="49d91-406">To znamená, že obnovení nebude přehodnocovat závislosti.</span><span class="sxs-lookup"><span data-stu-id="49d91-406">This means that restore will not reevaluate the dependencies.</span></span> |
| <span data-ttu-id="49d91-407">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="49d91-407">NuGetLockFilePath</span></span> | <span data-ttu-id="49d91-408">Vlastní umístění souboru zámku.</span><span class="sxs-lookup"><span data-stu-id="49d91-408">A custom location for the lock file.</span></span> <span data-ttu-id="49d91-409">Výchozí umístění je vedle projektu a je pojmenováno `packages.lock.json` .</span><span class="sxs-lookup"><span data-stu-id="49d91-409">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| <span data-ttu-id="49d91-410">RestoreForceEvaluate</span><span class="sxs-lookup"><span data-stu-id="49d91-410">RestoreForceEvaluate</span></span> | <span data-ttu-id="49d91-411">Vynutí obnovení pro přepočítání závislostí a aktualizaci souboru zámku bez upozornění.</span><span class="sxs-lookup"><span data-stu-id="49d91-411">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> |
| <span data-ttu-id="49d91-412">RestorePackagesConfig</span><span class="sxs-lookup"><span data-stu-id="49d91-412">RestorePackagesConfig</span></span> | <span data-ttu-id="49d91-413">Přepínač opt, který obnovuje projekty pomocí packages.config. Podpora pouze s nástrojem `MSBuild -t:restore` .</span><span class="sxs-lookup"><span data-stu-id="49d91-413">An opt in switch, that restores projects with packages.config. Support with `MSBuild -t:restore` only.</span></span> |

#### <a name="examples"></a><span data-ttu-id="49d91-414">Příklady</span><span class="sxs-lookup"><span data-stu-id="49d91-414">Examples</span></span>

<span data-ttu-id="49d91-415">Příkazový řádek:</span><span class="sxs-lookup"><span data-stu-id="49d91-415">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="49d91-416">Soubor projektu:</span><span class="sxs-lookup"><span data-stu-id="49d91-416">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="49d91-417">Obnovit výstupy</span><span class="sxs-lookup"><span data-stu-id="49d91-417">Restore outputs</span></span>

<span data-ttu-id="49d91-418">Obnovení vytvoří ve složce buildu následující soubory `obj` :</span><span class="sxs-lookup"><span data-stu-id="49d91-418">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="49d91-419">Soubor</span><span class="sxs-lookup"><span data-stu-id="49d91-419">File</span></span> | <span data-ttu-id="49d91-420">Popis</span><span class="sxs-lookup"><span data-stu-id="49d91-420">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="49d91-421">Obsahuje graf závislostí všech odkazů na balíčky.</span><span class="sxs-lookup"><span data-stu-id="49d91-421">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="49d91-422">Odkazy na MSBuild props obsažená v balíčcích</span><span class="sxs-lookup"><span data-stu-id="49d91-422">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="49d91-423">Odkazy na cíle nástroje MSBuild obsažené v balíčcích</span><span class="sxs-lookup"><span data-stu-id="49d91-423">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="49d91-424">Obnovení a sestavování pomocí jednoho příkazu MSBuild</span><span class="sxs-lookup"><span data-stu-id="49d91-424">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="49d91-425">Vzhledem k tomu, že nástroj NuGet dokáže obnovit balíčky, které vycházejí z cílů a props nástroje MSBuild, jsou vyhodnocení obnovení a sestavení spouštěna s různými globálními vlastnostmi.</span><span class="sxs-lookup"><span data-stu-id="49d91-425">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="49d91-426">To znamená, že následující nastavení bude mít nepředvídatelné a často nesprávné chování.</span><span class="sxs-lookup"><span data-stu-id="49d91-426">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="49d91-427">Místo doporučeného přístupu:</span><span class="sxs-lookup"><span data-stu-id="49d91-427">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="49d91-428">Stejná logika platí pro jiné cíle podobné `build` .</span><span class="sxs-lookup"><span data-stu-id="49d91-428">The same logic applies to other targets similar to `build`.</span></span>

### <a name="restoring-packagereference-and-packagesconfig-with-msbuild"></a><span data-ttu-id="49d91-429">Obnovení PackageReference a packages.config pomocí nástroje MSBuild</span><span class="sxs-lookup"><span data-stu-id="49d91-429">Restoring PackageReference and packages.config with MSBuild</span></span>

<span data-ttu-id="49d91-430">Pomocí nástroje MSBuild 16.5 + packages.config jsou také podporovány pro `msbuild -t:restore` .</span><span class="sxs-lookup"><span data-stu-id="49d91-430">With MSBuild 16.5+, packages.config are also supported for `msbuild -t:restore`.</span></span>

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> <span data-ttu-id="49d91-431">`packages.config` obnovení je k dispozici pouze pro `MSBuild 16.5+` , a nikoli s `dotnet.exe`</span><span class="sxs-lookup"><span data-stu-id="49d91-431">`packages.config` restore is only available with `MSBuild 16.5+`, and not with `dotnet.exe`</span></span>

### <a name="packagetargetfallback"></a><span data-ttu-id="49d91-432">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="49d91-432">PackageTargetFallback</span></span>

<span data-ttu-id="49d91-433">`PackageTargetFallback`Element umožňuje zadat sadu kompatibilních cílů, které mají být použity při obnovení balíčků.</span><span class="sxs-lookup"><span data-stu-id="49d91-433">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="49d91-434">Je navržena tak, aby povolovala balíčkům, které používají dotnet [TxM](../reference/target-frameworks.md) pro práci s kompatibilními balíčky, které nedeklarují dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="49d91-434">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="49d91-435">To znamená, že pokud váš projekt používá dotnet TxM, pak všechny balíčky, na kterých závisí, musí mít také hodnotu dotnet TxM, pokud do projektu nepřidáte, aby bylo možné, aby platformy, které `<PackageTargetFallback>` nejsou dotnet, byly kompatibilní s dotnet.</span><span class="sxs-lookup"><span data-stu-id="49d91-435">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="49d91-436">Například pokud projekt používá `netstandard1.6` TxM a závislý balíček obsahuje pouze `lib/net45/a.dll` a `lib/portable-net45+win81/a.dll` , projekt se nepodaří sestavit.</span><span class="sxs-lookup"><span data-stu-id="49d91-436">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="49d91-437">Pokud je to, co chcete uvést, je druhá knihovna DLL, pak můžete přidat `PackageTargetFallback` tak, aby říkáme, že `portable-net45+win81` je knihovna DLL kompatibilní:</span><span class="sxs-lookup"><span data-stu-id="49d91-437">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="49d91-438">Chcete-li deklarovat zálohu pro všechny cíle v projektu, ponechte `Condition` atribut.</span><span class="sxs-lookup"><span data-stu-id="49d91-438">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="49d91-439">Můžete také všechny existující `PackageTargetFallback` , a to i tak, `$(PackageTargetFallback)` jak je znázorněno zde:</span><span class="sxs-lookup"><span data-stu-id="49d91-439">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="49d91-440">Nahrazení jedné knihovny z grafu obnovení</span><span class="sxs-lookup"><span data-stu-id="49d91-440">Replacing one library from a restore graph</span></span>

<span data-ttu-id="49d91-441">Pokud obnovení předává nesprávné sestavení, je možné vyřadit výchozí volbu balíčků a nahradit ji vlastní volbou.</span><span class="sxs-lookup"><span data-stu-id="49d91-441">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="49d91-442">Nejprve s nejvyšší úrovní `PackageReference` , vylučte všechny prostředky:</span><span class="sxs-lookup"><span data-stu-id="49d91-442">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="49d91-443">Dále přidejte vlastní odkaz na příslušnou místní kopii knihovny DLL:</span><span class="sxs-lookup"><span data-stu-id="49d91-443">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
