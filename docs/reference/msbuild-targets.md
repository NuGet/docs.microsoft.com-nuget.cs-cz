---
title: NuGet zabalit a obnovit jako MSBuild cíle
description: NuGet sada a obnovení může pracovat přímo jako MSBuild cíle s NuGet 4.0 +.
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
no-loc:
- NuGet
- MSBuild
- .nuspec
- nuspec
ms.openlocfilehash: 8ebf0329f9dc7af09a59f1498a934754842df365
ms.sourcegitcommit: 08c5b2c956a1a45f0ea9fb3f50f55e41312d8ce3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/27/2021
ms.locfileid: "108067307"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="88603-103">NuGet zabalit a obnovit jako MSBuild cíle</span><span class="sxs-lookup"><span data-stu-id="88603-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="88603-104">*NuGet verze 4.0 +*</span><span class="sxs-lookup"><span data-stu-id="88603-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="88603-105">Ve formátu [PackageReference](../consume-packages/package-references-in-project-files.md) NuGet 4.0 + může ukládat všechna metadata manifestu přímo do souboru projektu místo použití samostatného `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="88603-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="88603-106">S MSBuild 15.1 + NuGet je také první MSBuild občan třídy s `pack` `restore` cíli a, jak je popsáno níže.</span><span class="sxs-lookup"><span data-stu-id="88603-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="88603-107">Tyto cíle vám umožňují pracovat NuGet stejně jako s jakýmkoli jiným MSBuild úkolem nebo cílem.</span><span class="sxs-lookup"><span data-stu-id="88603-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="88603-108">Pokyny k vytvoření NuGet balíčku pomocí MSBuild najdete v tématu [vytvoření NuGet balíčku pomocí MSBuild ](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="88603-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="88603-109">(Pro NuGet 3. x a starší použijte místo toho příkazy [Pack](../reference/cli-reference/cli-ref-pack.md) a [obnovení](../reference/cli-reference/cli-ref-restore.md) prostřednictvím rozhraní příkazového NuGet řádku.)</span><span class="sxs-lookup"><span data-stu-id="88603-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="88603-110">Pořadí sestavení cílů</span><span class="sxs-lookup"><span data-stu-id="88603-110">Target build order</span></span>

<span data-ttu-id="88603-111">Vzhledem `pack` k tomu, že a `restore` jsou  MSBuild cíle, můžete k nim přistupovat, abyste mohli vylepšit svůj pracovní postup.</span><span class="sxs-lookup"><span data-stu-id="88603-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="88603-112">Řekněme například, že chcete po sbalení balíčku zkopírovat do sdílené síťové složky.</span><span class="sxs-lookup"><span data-stu-id="88603-112">For example, let's say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="88603-113">To lze provést přidáním následujícího do souboru projektu:</span><span class="sxs-lookup"><span data-stu-id="88603-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="88603-114">Podobně můžete napsat MSBuild úlohu, napsat vlastní cíl a využít NuGet vlastnosti v MSBuild úloze.</span><span class="sxs-lookup"><span data-stu-id="88603-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="88603-115">`$(OutputPath)` je relativní a očekává, že spouštíte příkaz z kořenového adresáře projektu.</span><span class="sxs-lookup"><span data-stu-id="88603-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="88603-116">cíl balíčku</span><span class="sxs-lookup"><span data-stu-id="88603-116">pack target</span></span>

<span data-ttu-id="88603-117">Pro projekty .NET, které používají `PackageReference` formát, pomocí `msbuild -t:pack` kreslí vstupy ze souboru projektu, které se mají použít při vytváření NuGet balíčku.</span><span class="sxs-lookup"><span data-stu-id="88603-117">For .NET projects that use the `PackageReference` format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="88603-118">Následující tabulka popisuje MSBuild vlastnosti, které lze přidat do souboru projektu v rámci prvního `<PropertyGroup>` uzlu.</span><span class="sxs-lookup"><span data-stu-id="88603-118">The following table describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="88603-119">Tyto úpravy můžete snadno upravit v aplikaci Visual Studio 2017 a novějším kliknutím pravým tlačítkem myši na projekt a výběrem možnosti **Upravit {PROJECT_NAME}** v místní nabídce.</span><span class="sxs-lookup"><span data-stu-id="88603-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="88603-120">Pro usnadnění práce je tabulka uspořádána podle odpovídající vlastnosti v [ `.nuspec` souboru](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="88603-120">For convenience, the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

> [!NOTE]
> <span data-ttu-id="88603-121">`Owners` a `Summary` vlastnosti z `.nuspec` nejsou podporovány v MSBuild .</span><span class="sxs-lookup"><span data-stu-id="88603-121">`Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="88603-122">Atribut/ nuspec hodnota</span><span class="sxs-lookup"><span data-stu-id="88603-122">Attribute/nuspec Value</span></span> | <span data-ttu-id="88603-123">MSBuild Majetek</span><span class="sxs-lookup"><span data-stu-id="88603-123">MSBuild Property</span></span> | <span data-ttu-id="88603-124">Výchozí</span><span class="sxs-lookup"><span data-stu-id="88603-124">Default</span></span> | <span data-ttu-id="88603-125">Poznámky</span><span class="sxs-lookup"><span data-stu-id="88603-125">Notes</span></span> |
|--------|--------|--------|--------|
| `Id` | `PackageId` | `$(AssemblyName)` | <span data-ttu-id="88603-126">`$(AssemblyName)` Výsledkem MSBuild</span><span class="sxs-lookup"><span data-stu-id="88603-126">`$(AssemblyName)` from MSBuild</span></span> |
| `Version` | `PackageVersion` | <span data-ttu-id="88603-127">Verze</span><span class="sxs-lookup"><span data-stu-id="88603-127">Version</span></span> | <span data-ttu-id="88603-128">To je semver kompatibilní, například `1.0.0` nebo. `1.0.0-beta``1.0.0-beta-00345`</span><span class="sxs-lookup"><span data-stu-id="88603-128">This is semver compatible, for example `1.0.0`, `1.0.0-beta`, or `1.0.0-beta-00345`</span></span> |
| `VersionPrefix` | `PackageVersionPrefix` | <span data-ttu-id="88603-129">empty</span><span class="sxs-lookup"><span data-stu-id="88603-129">empty</span></span> | <span data-ttu-id="88603-130">Nastavení `PackageVersion` přepsání `PackageVersionPrefix`</span><span class="sxs-lookup"><span data-stu-id="88603-130">Setting `PackageVersion` overwrites `PackageVersionPrefix`</span></span> |
| `VersionSuffix` | `PackageVersionSuffix` | <span data-ttu-id="88603-131">empty</span><span class="sxs-lookup"><span data-stu-id="88603-131">empty</span></span> | <span data-ttu-id="88603-132">`$(VersionSuffix)` z MSBuild .</span><span class="sxs-lookup"><span data-stu-id="88603-132">`$(VersionSuffix)` from MSBuild.</span></span> <span data-ttu-id="88603-133">Nastavení `PackageVersion` přepsání `PackageVersionSuffix`</span><span class="sxs-lookup"><span data-stu-id="88603-133">Setting `PackageVersion` overwrites `PackageVersionSuffix`</span></span> |
| `Authors` | `Authors` | <span data-ttu-id="88603-134">Uživatelské jméno aktuálního uživatele</span><span class="sxs-lookup"><span data-stu-id="88603-134">Username of the current user</span></span> | <span data-ttu-id="88603-135">Středníkem oddělený seznam autorů balíčků, které odpovídají názvům profilů v nuget.org. Ty se zobrazují v NuGet galerii na NuGet.org a používají se pro balíčky křížového odkazu stejnými autory.</span><span class="sxs-lookup"><span data-stu-id="88603-135">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| `Owners` | <span data-ttu-id="88603-136">–</span><span class="sxs-lookup"><span data-stu-id="88603-136">N/A</span></span> | <span data-ttu-id="88603-137">Nepřítomno v nuspec</span><span class="sxs-lookup"><span data-stu-id="88603-137">Not present in nuspec</span></span> | |
| `Title` | `Title` | <span data-ttu-id="88603-138">Parametr `PackageId` nahraďte názvem sestavy.</span><span class="sxs-lookup"><span data-stu-id="88603-138">The `PackageId`</span></span> | <span data-ttu-id="88603-139">Popisný název balíčku, který se obvykle používá v uživatelském rozhraní, se zobrazuje jako v nuget.org a správce balíčků v aplikaci Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="88603-139">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> |
| `Description` | `Description` | <span data-ttu-id="88603-140">Popis balíčku</span><span class="sxs-lookup"><span data-stu-id="88603-140">"Package Description"</span></span> | <span data-ttu-id="88603-141">Dlouhý popis pro sestavení.</span><span class="sxs-lookup"><span data-stu-id="88603-141">A long description for the assembly.</span></span> <span data-ttu-id="88603-142">Pokud `PackageDescription` parametr není zadán, tato vlastnost se používá také jako Popis balíčku.</span><span class="sxs-lookup"><span data-stu-id="88603-142">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| `Copyright` | `Copyright` | <span data-ttu-id="88603-143">empty</span><span class="sxs-lookup"><span data-stu-id="88603-143">empty</span></span> | <span data-ttu-id="88603-144">Podrobnosti o autorských právech pro balíček.</span><span class="sxs-lookup"><span data-stu-id="88603-144">Copyright details for the package.</span></span> |
| `RequireLicenseAcceptance` | `PackageRequireLicenseAcceptance` | `false` | <span data-ttu-id="88603-145">Logická hodnota, která určuje, zda klient musí požádat spotřebitele o přijetí licence k balíčku před instalací balíčku.</span><span class="sxs-lookup"><span data-stu-id="88603-145">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> |
| `license` | `PackageLicenseExpression` | <span data-ttu-id="88603-146">empty</span><span class="sxs-lookup"><span data-stu-id="88603-146">empty</span></span> | <span data-ttu-id="88603-147">Odpovídá `<license type="expression">` .</span><span class="sxs-lookup"><span data-stu-id="88603-147">Corresponds to `<license type="expression">`.</span></span> <span data-ttu-id="88603-148">Viz [balení licenčního výrazu nebo licenčního souboru](#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="88603-148">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `license` | `PackageLicenseFile` | <span data-ttu-id="88603-149">empty</span><span class="sxs-lookup"><span data-stu-id="88603-149">empty</span></span> | <span data-ttu-id="88603-150">Cesta k souboru s licencí v rámci balíčku, pokud používáte vlastní licenci nebo licenci, ke které se nepřiřadil identifikátor SPDX</span><span class="sxs-lookup"><span data-stu-id="88603-150">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> <span data-ttu-id="88603-151">Musíte explicitně sbalit soubor s odkazem na licenci.</span><span class="sxs-lookup"><span data-stu-id="88603-151">You need to explicitly pack the referenced license file.</span></span> <span data-ttu-id="88603-152">Odpovídá `<license type="file">` .</span><span class="sxs-lookup"><span data-stu-id="88603-152">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="88603-153">Viz [balení licenčního výrazu nebo licenčního souboru](#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="88603-153">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `LicenseUrl` | `PackageLicenseUrl` | <span data-ttu-id="88603-154">empty</span><span class="sxs-lookup"><span data-stu-id="88603-154">empty</span></span> | <span data-ttu-id="88603-155">`PackageLicenseUrl` je zastaralá.</span><span class="sxs-lookup"><span data-stu-id="88603-155">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="88603-156">Použijte `PackageLicenseExpression` nebo `PackageLicenseFile` místo toho.</span><span class="sxs-lookup"><span data-stu-id="88603-156">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| `ProjectUrl` | `PackageProjectUrl` | <span data-ttu-id="88603-157">empty</span><span class="sxs-lookup"><span data-stu-id="88603-157">empty</span></span> | |
| `Icon` | `PackageIcon` | <span data-ttu-id="88603-158">empty</span><span class="sxs-lookup"><span data-stu-id="88603-158">empty</span></span> | <span data-ttu-id="88603-159">Cesta k obrázku v balíčku, který se má použít jako ikona balíčku</span><span class="sxs-lookup"><span data-stu-id="88603-159">A path to an image in the package to use as a package icon.</span></span> <span data-ttu-id="88603-160">Musíte explicitně sbalit soubor obrázku odkazované ikony.</span><span class="sxs-lookup"><span data-stu-id="88603-160">You need to explicitly pack the referenced icon image file.</span></span> <span data-ttu-id="88603-161">Další informace najdete v tématu [sbalení souboru obrázku ikony](#packing-an-icon-image-file) a [ `icon` metadat](./nuspec.md#icon).</span><span class="sxs-lookup"><span data-stu-id="88603-161">For more information, see [Packing an icon image file](#packing-an-icon-image-file) and [`icon` metadata](./nuspec.md#icon).</span></span> |
| `IconUrl` | `PackageIconUrl` | <span data-ttu-id="88603-162">empty</span><span class="sxs-lookup"><span data-stu-id="88603-162">empty</span></span> | <span data-ttu-id="88603-163">`PackageIconUrl` je zastaralé namísto `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="88603-163">`PackageIconUrl` is deprecated in favor of `PackageIcon`.</span></span> <span data-ttu-id="88603-164">Pro dosažení nejlepšího prostředí pro starší verze byste však měli zadat `PackageIconUrl` kromě `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="88603-164">However, for the best downlevel experience, you should specify `PackageIconUrl` in addition to `PackageIcon`.</span></span> |
| `Readme` | `PackageReadmeFile` | <span data-ttu-id="88603-165">empty</span><span class="sxs-lookup"><span data-stu-id="88603-165">empty</span></span> | <span data-ttu-id="88603-166">Musíte explicitně zabalit odkazovaný soubor Readme.</span><span class="sxs-lookup"><span data-stu-id="88603-166">You need to explicitly pack the referenced readme file.</span></span>|
| `Tags` | `PackageTags` | <span data-ttu-id="88603-167">empty</span><span class="sxs-lookup"><span data-stu-id="88603-167">empty</span></span> | <span data-ttu-id="88603-168">Seznam značek oddělených středníkem, který určuje balíček.</span><span class="sxs-lookup"><span data-stu-id="88603-168">A semicolon-delimited list of tags that designates the package.</span></span> |
| `ReleaseNotes` | `PackageReleaseNotes` | <span data-ttu-id="88603-169">empty</span><span class="sxs-lookup"><span data-stu-id="88603-169">empty</span></span> | <span data-ttu-id="88603-170">Poznámky k verzi balíčku</span><span class="sxs-lookup"><span data-stu-id="88603-170">Release notes for the package.</span></span> |
| `Repository/Url` | `RepositoryUrl` | <span data-ttu-id="88603-171">empty</span><span class="sxs-lookup"><span data-stu-id="88603-171">empty</span></span> | <span data-ttu-id="88603-172">Adresa URL úložiště, která se používá k klonování nebo načtení zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="88603-172">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="88603-173">Příklad: *https://github.com/ NuGet / NuGet . Client. Git*.</span><span class="sxs-lookup"><span data-stu-id="88603-173">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| `Repository/Type` | `RepositoryType` | <span data-ttu-id="88603-174">empty</span><span class="sxs-lookup"><span data-stu-id="88603-174">empty</span></span> | <span data-ttu-id="88603-175">Typ úložiště</span><span class="sxs-lookup"><span data-stu-id="88603-175">Repository type.</span></span> <span data-ttu-id="88603-176">Příklady: `git` (výchozí), `tfs` .</span><span class="sxs-lookup"><span data-stu-id="88603-176">Examples: `git` (default), `tfs`.</span></span> |
| `Repository/Branch` | `RepositoryBranch` | <span data-ttu-id="88603-177">empty</span><span class="sxs-lookup"><span data-stu-id="88603-177">empty</span></span> | <span data-ttu-id="88603-178">Volitelné informace o větvi úložiště</span><span class="sxs-lookup"><span data-stu-id="88603-178">Optional repository branch information.</span></span> <span data-ttu-id="88603-179">`RepositoryUrl` musí být také zadáno pro zahrnutí této vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="88603-179">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="88603-180">Příklad: *Master* ( NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="88603-180">Example: *master* (NuGet 4.7.0+).</span></span> |
| `Repository/Commit` | `RepositoryCommit` | <span data-ttu-id="88603-181">empty</span><span class="sxs-lookup"><span data-stu-id="88603-181">empty</span></span> | <span data-ttu-id="88603-182">Volitelné potvrzení změn úložiště nebo sada změn, které označují, na který zdroj byl balíček vytvořen.</span><span class="sxs-lookup"><span data-stu-id="88603-182">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="88603-183">`RepositoryUrl` musí být také zadáno pro zahrnutí této vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="88603-183">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="88603-184">Příklad: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="88603-184">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| `PackageType` | `<PackageType>CustomType1, 1.0.0.0;CustomType2</PackageType>` | | <span data-ttu-id="88603-185">Určuje zamýšlené použití balíčku.</span><span class="sxs-lookup"><span data-stu-id="88603-185">Indicates the package's intended use.</span></span> <span data-ttu-id="88603-186">Typy balíčků používají stejný formát jako ID balíčků a jsou odděleny `;` .</span><span class="sxs-lookup"><span data-stu-id="88603-186">Package types use the same format as package IDs and are delimited by `;`.</span></span> <span data-ttu-id="88603-187">Typy balíčků můžou být ve verzi s připojením `,` a a [`Version`](/dotnet/api/system.version) řetězcem.</span><span class="sxs-lookup"><span data-stu-id="88603-187">Package types may be versioned by appending a `,` and a [`Version`](/dotnet/api/system.version) string.</span></span> <span data-ttu-id="88603-188">Viz [nastavení NuGet typu balíčku](../create-packages/set-package-type.md) ( NuGet 3.5.0 +).</span><span class="sxs-lookup"><span data-stu-id="88603-188">See [Set a NuGet package type](../create-packages/set-package-type.md) (NuGet 3.5.0+).</span></span> |
| `Summary` | <span data-ttu-id="88603-189">Nepodporováno</span><span class="sxs-lookup"><span data-stu-id="88603-189">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="88603-190">cílové vstupy balení</span><span class="sxs-lookup"><span data-stu-id="88603-190">pack target inputs</span></span>

| <span data-ttu-id="88603-191">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="88603-191">Property</span></span> | <span data-ttu-id="88603-192">Popis</span><span class="sxs-lookup"><span data-stu-id="88603-192">Description</span></span> |
| - | - |
| `IsPackable` | <span data-ttu-id="88603-193">Logická hodnota, která určuje, zda lze projekt zabalit.</span><span class="sxs-lookup"><span data-stu-id="88603-193">A Boolean value that specifies whether the project can be packed.</span></span> <span data-ttu-id="88603-194">Výchozí hodnota je `true`.</span><span class="sxs-lookup"><span data-stu-id="88603-194">The default value is `true`.</span></span> |
| `SuppressDependenciesWhenPacking` | <span data-ttu-id="88603-195">Nastavte na `true` , aby se potlačily závislosti balíčků z vygenerovaného NuGet balíčku.</span><span class="sxs-lookup"><span data-stu-id="88603-195">Set to `true` to suppress package dependencies from the generated NuGet package.</span></span> |
| `PackageVersion` | <span data-ttu-id="88603-196">Určuje verzi, kterou výsledný balíček bude mít.</span><span class="sxs-lookup"><span data-stu-id="88603-196">Specifies the version that the resulting package will have.</span></span> <span data-ttu-id="88603-197">Akceptuje všechny formy NuGet řetězce verze.</span><span class="sxs-lookup"><span data-stu-id="88603-197">Accepts all forms of NuGet version string.</span></span> <span data-ttu-id="88603-198">Výchozí hodnota je hodnota `$(Version)` , to znamená vlastnost `Version` v projektu.</span><span class="sxs-lookup"><span data-stu-id="88603-198">Default is the value of `$(Version)`, that is, of the property `Version` in the project.</span></span> |
| `PackageId` | <span data-ttu-id="88603-199">Určuje název výsledného balíčku.</span><span class="sxs-lookup"><span data-stu-id="88603-199">Specifies the name for the resulting package.</span></span> <span data-ttu-id="88603-200">Pokud tento parametr nezadáte, použije se ve `pack` výchozím nastavení `AssemblyName` jako název balíčku název adresáře nebo.</span><span class="sxs-lookup"><span data-stu-id="88603-200">If not specified, the `pack` operation will default to using the `AssemblyName` or directory name as the name of the package.</span></span> |
| `PackageDescription` | <span data-ttu-id="88603-201">Dlouhý popis balíčku pro zobrazení uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="88603-201">A long description of the package for UI display.</span></span> |
| `Authors` | <span data-ttu-id="88603-202">Středníkem oddělený seznam autorů balíčků, které odpovídají názvům profilů v nuget.org. Ty se zobrazují v NuGet galerii na NuGet.org a používají se pro balíčky křížového odkazu stejnými autory.</span><span class="sxs-lookup"><span data-stu-id="88603-202">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| `Description` | <span data-ttu-id="88603-203">Dlouhý popis pro sestavení.</span><span class="sxs-lookup"><span data-stu-id="88603-203">A long description for the assembly.</span></span> <span data-ttu-id="88603-204">Pokud `PackageDescription` parametr není zadán, tato vlastnost se používá také jako Popis balíčku.</span><span class="sxs-lookup"><span data-stu-id="88603-204">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| `Copyright` | <span data-ttu-id="88603-205">Podrobnosti o autorských právech pro balíček.</span><span class="sxs-lookup"><span data-stu-id="88603-205">Copyright details for the package.</span></span> |
| `PackageRequireLicenseAcceptance` | <span data-ttu-id="88603-206">Logická hodnota, která určuje, zda klient musí požádat spotřebitele o přijetí licence k balíčku před instalací balíčku.</span><span class="sxs-lookup"><span data-stu-id="88603-206">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> <span data-ttu-id="88603-207">Výchozí formát je `false`.</span><span class="sxs-lookup"><span data-stu-id="88603-207">The default is `false`.</span></span> |
| `DevelopmentDependency` | <span data-ttu-id="88603-208">Logická hodnota, která určuje, zda je balíček označen jako jen pro vývoj, což zabrání zahrnutí balíčku jako závislosti v jiných balíčcích.</span><span class="sxs-lookup"><span data-stu-id="88603-208">A Boolean value that specifies whether the package is marked as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="88603-209">S `PackageReference` ( NuGet 4.8 +) Tento příznak také znamená, že prostředky při kompilaci jsou vyloučeny z kompilace.</span><span class="sxs-lookup"><span data-stu-id="88603-209">With `PackageReference` (NuGet 4.8+), this flag also means that compile-time assets are excluded from compilation.</span></span> <span data-ttu-id="88603-210">Další informace najdete v tématu [Podpora DevelopmentDependency pro PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span><span class="sxs-lookup"><span data-stu-id="88603-210">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span> |
| `PackageLicenseExpression` | <span data-ttu-id="88603-211">Identifikátor nebo výraz [licence SPDX](https://spdx.org/licenses/) , například `Apache-2.0` .</span><span class="sxs-lookup"><span data-stu-id="88603-211">An [SPDX license identifier](https://spdx.org/licenses/) or expression, for example, `Apache-2.0`.</span></span> <span data-ttu-id="88603-212">Další informace najdete v tématu [balení licenčního výrazu nebo licenčního souboru](#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="88603-212">For more information, see [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `PackageLicenseFile` | <span data-ttu-id="88603-213">Cesta k souboru s licencí v rámci balíčku, pokud používáte vlastní licenci nebo licenci, ke které se nepřiřadil identifikátor SPDX</span><span class="sxs-lookup"><span data-stu-id="88603-213">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> |
| `PackageLicenseUrl` | <span data-ttu-id="88603-214">`PackageLicenseUrl` je zastaralá.</span><span class="sxs-lookup"><span data-stu-id="88603-214">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="88603-215">Použijte `PackageLicenseExpression` nebo `PackageLicenseFile` místo toho.</span><span class="sxs-lookup"><span data-stu-id="88603-215">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| `PackageProjectUrl` | |
| `PackageIcon` | <span data-ttu-id="88603-216">Určuje cestu ikony balíčku vzhledem k kořenu balíčku.</span><span class="sxs-lookup"><span data-stu-id="88603-216">Specifies the package icon path, relative to the root of the package.</span></span> <span data-ttu-id="88603-217">Další informace najdete v tématu [sbalení souboru obrázku ikony](#packing-an-icon-image-file).</span><span class="sxs-lookup"><span data-stu-id="88603-217">For more information, see [Packing an icon image file](#packing-an-icon-image-file).</span></span> |
| `PackageReleaseNotes` | <span data-ttu-id="88603-218">Poznámky k verzi balíčku</span><span class="sxs-lookup"><span data-stu-id="88603-218">Release notes for the package.</span></span> |
| `PackageReadmeFile` | <span data-ttu-id="88603-219">Soubor Readme pro balíček.</span><span class="sxs-lookup"><span data-stu-id="88603-219">Readme for the package.</span></span> |
| `PackageTags` | <span data-ttu-id="88603-220">Seznam značek oddělených středníkem, který určuje balíček.</span><span class="sxs-lookup"><span data-stu-id="88603-220">A semicolon-delimited list of tags that designates the package.</span></span> |
| `PackageOutputPath` | <span data-ttu-id="88603-221">Určuje výstupní cestu, do které bude zahozen zabalený balíček.</span><span class="sxs-lookup"><span data-stu-id="88603-221">Determines the output path in which the packed package will be dropped.</span></span> <span data-ttu-id="88603-222">Výchozí je `$(OutputPath)`.</span><span class="sxs-lookup"><span data-stu-id="88603-222">Default is `$(OutputPath)`.</span></span> |
| `IncludeSymbols` | <span data-ttu-id="88603-223">Tato logická hodnota označuje, zda má balíček při zabalení projektu vytvořit další balíček symbolů.</span><span class="sxs-lookup"><span data-stu-id="88603-223">This Boolean value indicates whether the package should create an additional symbols package when the project is packed.</span></span> <span data-ttu-id="88603-224">Formát balíčku symbolů je řízen `SymbolPackageFormat` vlastností.</span><span class="sxs-lookup"><span data-stu-id="88603-224">The symbols package's format is controlled by the `SymbolPackageFormat` property.</span></span> <span data-ttu-id="88603-225">Další informace najdete v tématu [IncludeSymbols](#includesymbols).</span><span class="sxs-lookup"><span data-stu-id="88603-225">For more information, see [IncludeSymbols](#includesymbols).</span></span> |
| `IncludeSource` | <span data-ttu-id="88603-226">Tato logická hodnota označuje, zda by měl proces balíčku vytvořit zdrojový balíček.</span><span class="sxs-lookup"><span data-stu-id="88603-226">This Boolean value indicates whether the pack process should create a source package.</span></span> <span data-ttu-id="88603-227">Zdrojový balíček obsahuje zdrojový kód knihovny i soubory PDB.</span><span class="sxs-lookup"><span data-stu-id="88603-227">The source package contains the library's source code as well as PDB files.</span></span> <span data-ttu-id="88603-228">Zdrojové soubory jsou umístěny do `src/ProjectName` adresáře ve výsledném souboru balíčku.</span><span class="sxs-lookup"><span data-stu-id="88603-228">Source files are put under the `src/ProjectName` directory in the resulting package file.</span></span> <span data-ttu-id="88603-229">Další informace najdete v tématu [IncludeSource](#includesource).</span><span class="sxs-lookup"><span data-stu-id="88603-229">For more information, see [IncludeSource](#includesource).</span></span> |
| `PackageType` | |
| `IsTool` | <span data-ttu-id="88603-230">Určuje, zda jsou všechny výstupní soubory zkopírovány do složky *Tools* namísto složky *lib* .</span><span class="sxs-lookup"><span data-stu-id="88603-230">Specifies whether all output files are copied to the *tools* folder instead of the *lib* folder.</span></span> <span data-ttu-id="88603-231">Další informace najdete v tématu [Nástroj](#istool).</span><span class="sxs-lookup"><span data-stu-id="88603-231">For more information, see [IsTool](#istool).</span></span> |
| `RepositoryUrl` | <span data-ttu-id="88603-232">Adresa URL úložiště, která se používá k klonování nebo načtení zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="88603-232">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="88603-233">Příklad: *https://github.com/ NuGet / NuGet . Client. Git*.</span><span class="sxs-lookup"><span data-stu-id="88603-233">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| `RepositoryType` | <span data-ttu-id="88603-234">Typ úložiště</span><span class="sxs-lookup"><span data-stu-id="88603-234">Repository type.</span></span> <span data-ttu-id="88603-235">Příklady: `git` (výchozí), `tfs` .</span><span class="sxs-lookup"><span data-stu-id="88603-235">Examples: `git` (default), `tfs`.</span></span> |
| `RepositoryBranch` | <span data-ttu-id="88603-236">Volitelné informace o větvi úložiště</span><span class="sxs-lookup"><span data-stu-id="88603-236">Optional repository branch information.</span></span> <span data-ttu-id="88603-237">`RepositoryUrl` musí být také zadáno pro zahrnutí této vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="88603-237">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="88603-238">Příklad: *Master* ( NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="88603-238">Example: *master* (NuGet 4.7.0+).</span></span> |
| `RepositoryCommit` | <span data-ttu-id="88603-239">Volitelné potvrzení změn úložiště nebo sada změn, které označují, na který zdroj byl balíček vytvořen.</span><span class="sxs-lookup"><span data-stu-id="88603-239">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="88603-240">`RepositoryUrl` musí být také zadáno pro zahrnutí této vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="88603-240">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="88603-241">Příklad: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="88603-241">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| `SymbolPackageFormat` | <span data-ttu-id="88603-242">Určuje formát balíčku symbolů.</span><span class="sxs-lookup"><span data-stu-id="88603-242">Specifies the format of the symbols package.</span></span> <span data-ttu-id="88603-243">Pokud se "Symbols. nupkg", vytvoří se balíček starších symbolů s příponou *. Symbols. nupkg* obsahující soubory PDB, knihovny DLL a další výstupní soubory.</span><span class="sxs-lookup"><span data-stu-id="88603-243">If "symbols.nupkg", a legacy symbols package is created with a *.symbols.nupkg* extension containing PDBs, DLLs, and other output files.</span></span> <span data-ttu-id="88603-244">Pokud je "snupkg", vytvoří se balíček symbolů snupkg obsahující přenosné soubory PDB.</span><span class="sxs-lookup"><span data-stu-id="88603-244">If "snupkg", a snupkg symbol package is created containing the portable PDBs.</span></span> <span data-ttu-id="88603-245">Výchozí hodnota je "Symbols. nupkg".</span><span class="sxs-lookup"><span data-stu-id="88603-245">The default is "symbols.nupkg".</span></span> |
| `NoPackageAnalysis` | <span data-ttu-id="88603-246">Určuje, že `pack` po sestavení balíčku by neměl spustit analýzu balíčku.</span><span class="sxs-lookup"><span data-stu-id="88603-246">Specifies that `pack` should not run package analysis after building the package.</span></span> |
| `MinClientVersion` | <span data-ttu-id="88603-247">Určuje minimální verzi NuGet klienta, který může nainstalovat tento balíček vynutilý nuget.exe a správcem balíčků sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="88603-247">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> |
| `IncludeBuildOutput` | <span data-ttu-id="88603-248">Tato logická hodnota určuje, zda mají být výstupní sestavení sestavení zabalena do souboru *. nupkg* nebo ne.</span><span class="sxs-lookup"><span data-stu-id="88603-248">This Boolean value specifies whether the build output assemblies should be packed into the *.nupkg* file or not.</span></span> |
| `IncludeContentInPack` | <span data-ttu-id="88603-249">Tato logická hodnota určuje, zda jsou všechny položky, které mají typ, `Content` zahrnuty ve výsledném balíčku automaticky.</span><span class="sxs-lookup"><span data-stu-id="88603-249">This Boolean value specifies whether any items that have a type of `Content` are included in the resulting package automatically.</span></span> <span data-ttu-id="88603-250">Výchozí formát je `true`.</span><span class="sxs-lookup"><span data-stu-id="88603-250">The default is `true`.</span></span> |
| `BuildOutputTargetFolder` | <span data-ttu-id="88603-251">Určuje složku, kam se mají umístit výstupní sestavení.</span><span class="sxs-lookup"><span data-stu-id="88603-251">Specifies the folder where to place the output assemblies.</span></span> <span data-ttu-id="88603-252">Výstupní sestavení (a další výstupní soubory) se zkopírují do příslušných složek rozhraní.</span><span class="sxs-lookup"><span data-stu-id="88603-252">The output assemblies (and other output files) are copied into their respective framework folders.</span></span> <span data-ttu-id="88603-253">Další informace naleznete v tématu [výstupní sestavení](#output-assemblies).</span><span class="sxs-lookup"><span data-stu-id="88603-253">For more information, see [Output assemblies](#output-assemblies).</span></span> |
| `ContentTargetFolders` | <span data-ttu-id="88603-254">Určuje výchozí umístění, kde se mají všechny soubory obsahu nacházet, pokud `PackagePath` nejsou pro ně zadány.</span><span class="sxs-lookup"><span data-stu-id="88603-254">Specifies the default location of where all the content files should go if `PackagePath` is not specified for them.</span></span> <span data-ttu-id="88603-255">Výchozí hodnota je Content; contentFiles.</span><span class="sxs-lookup"><span data-stu-id="88603-255">The default value is "content;contentFiles".</span></span> <span data-ttu-id="88603-256">Další informace najdete v tématu [zahrnutí obsahu do balíčku](#including-content-in-a-package).</span><span class="sxs-lookup"><span data-stu-id="88603-256">For more information, see [Including content in a package](#including-content-in-a-package).</span></span> |
| `NuspecFile` | <span data-ttu-id="88603-257">Relativní nebo absolutní cesta k *.nuspec* souboru, který se používá k balení.</span><span class="sxs-lookup"><span data-stu-id="88603-257">Relative or absolute path to the *.nuspec* file being used for packing.</span></span> <span data-ttu-id="88603-258">Je-li tento parametr zadán, použije se **výhradně** pro informace o balení a žádné informace v projektech se nepoužijí.</span><span class="sxs-lookup"><span data-stu-id="88603-258">If specified, it's used **exclusively** for packaging information, and any information in the projects is not used.</span></span> <span data-ttu-id="88603-259">Další informace naleznete v tématu [balení pomocí .nuspec ](#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="88603-259">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |
| `NuspecBasePath` | <span data-ttu-id="88603-260">Základní cesta k *.nuspec* souboru</span><span class="sxs-lookup"><span data-stu-id="88603-260">Base path for the *.nuspec* file.</span></span> <span data-ttu-id="88603-261">Další informace naleznete v tématu [balení pomocí .nuspec ](#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="88603-261">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |
| `NuspecProperties` | <span data-ttu-id="88603-262">Seznam párů klíč = hodnota oddělený středníkem.</span><span class="sxs-lookup"><span data-stu-id="88603-262">Semicolon separated list of key=value pairs.</span></span> <span data-ttu-id="88603-263">Další informace naleznete v tématu [balení pomocí .nuspec ](#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="88603-263">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |

## <a name="pack-scenarios"></a><span data-ttu-id="88603-264">scénáře sady Pack</span><span class="sxs-lookup"><span data-stu-id="88603-264">pack scenarios</span></span>

### <a name="suppressing-dependencies"></a><span data-ttu-id="88603-265">Potlačení závislostí</span><span class="sxs-lookup"><span data-stu-id="88603-265">Suppressing dependencies</span></span>

<span data-ttu-id="88603-266">Chcete-li potlačit závislosti balíčků z vygenerovaného NuGet balíčku, nastavte na to, `SuppressDependenciesWhenPacking` `true` které umožní přeskočí všechny závislosti ze generovaného souboru nupkg.</span><span class="sxs-lookup"><span data-stu-id="88603-266">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### `PackageIconUrl`

<span data-ttu-id="88603-267">`PackageIconUrl` je zastaralá ve prospěch [`PackageIcon`](#packageicon) Vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="88603-267">`PackageIconUrl` is deprecated in favor of the [`PackageIcon`](#packageicon) property.</span></span> <span data-ttu-id="88603-268">Od NuGet verze 5,3 a sady Visual Studio 2019 verze 16,3 `pack` vyvolá upozornění [NU5048](./errors-and-warnings/nu5048.md) , pokud je určeno pouze metadata balíčku `PackageIconUrl` .</span><span class="sxs-lookup"><span data-stu-id="88603-268">Starting with NuGet 5.3 and Visual Studio 2019 version 16.3, `pack` raises the [NU5048](./errors-and-warnings/nu5048.md) warning if the package metadata only specifies `PackageIconUrl`.</span></span>

### `PackageIcon`

> [!Tip]
> <span data-ttu-id="88603-269">Aby se zachovala zpětná kompatibilita se klienty a zdroji, které ještě nepodporují `PackageIcon` , zadejte obojí `PackageIcon` i `PackageIconUrl` .</span><span class="sxs-lookup"><span data-stu-id="88603-269">To maintain backward compatibility with clients and sources that don't yet support `PackageIcon`, specify both `PackageIcon` and `PackageIconUrl`.</span></span> <span data-ttu-id="88603-270">Visual Studio podporuje `PackageIcon` pro balíčky pocházející ze zdroje založeného na složkách.</span><span class="sxs-lookup"><span data-stu-id="88603-270">Visual Studio supports `PackageIcon` for packages coming from a folder-based source.</span></span>

#### <a name="packing-an-icon-image-file"></a><span data-ttu-id="88603-271">Balení souboru obrázku ikony</span><span class="sxs-lookup"><span data-stu-id="88603-271">Packing an icon image file</span></span>

<span data-ttu-id="88603-272">Při balení souboru obrázku ikony použijte `PackageIcon` vlastnost k určení cesty k souboru ikony vzhledem k kořenu balíčku.</span><span class="sxs-lookup"><span data-stu-id="88603-272">When packing an icon image file, use `PackageIcon` property to specify the icon file path, relative to the root of the package.</span></span> <span data-ttu-id="88603-273">Navíc se ujistěte, že je soubor součástí balíčku.</span><span class="sxs-lookup"><span data-stu-id="88603-273">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="88603-274">Velikost souboru obrázku je omezená na 1 MB.</span><span class="sxs-lookup"><span data-stu-id="88603-274">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="88603-275">Podporované formáty souborů zahrnují JPEG a PNG.</span><span class="sxs-lookup"><span data-stu-id="88603-275">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="88603-276">Doporučujeme, abyste 128 × 128 rozlišení obrazu.</span><span class="sxs-lookup"><span data-stu-id="88603-276">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="88603-277">Například:</span><span class="sxs-lookup"><span data-stu-id="88603-277">For example:</span></span>

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

<span data-ttu-id="88603-278">[Ukázka ikony balíčku](https://github.com/NuGet/Samples/tree/main/PackageIconExample)</span><span class="sxs-lookup"><span data-stu-id="88603-278">[Package Icon sample](https://github.com/NuGet/Samples/tree/main/PackageIconExample).</span></span>

<span data-ttu-id="88603-279">U nuspec ekvivalentu si přečtěte odkaz na [ nuspec ikonu](nuspec.md#icon).</span><span class="sxs-lookup"><span data-stu-id="88603-279">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="packagereadmefile"></a><span data-ttu-id="88603-280">PackageReadmeFile</span><span class="sxs-lookup"><span data-stu-id="88603-280">PackageReadmeFile</span></span>

<span data-ttu-id="88603-281">*Podporováno s **NuGet 5.10.0 Preview 2**  /  **.NET SDK 5.0.300** a novějšími*</span><span class="sxs-lookup"><span data-stu-id="88603-281">*Supported with **NuGet 5.10.0 preview 2** / **.NET SDK 5.0.300** and above*</span></span>

<span data-ttu-id="88603-282">Při balení souboru Readme je potřeba použít `PackageReadmeFile` vlastnost k určení cesty k balíčku vzhledem k kořenu balíčku.</span><span class="sxs-lookup"><span data-stu-id="88603-282">When packing a readme file, you need to use the `PackageReadmeFile` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="88603-283">Kromě toho je nutné se ujistit, že je soubor součástí balíčku.</span><span class="sxs-lookup"><span data-stu-id="88603-283">In addition to this, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="88603-284">Podporované formáty souborů obsahují pouze Markdownu (*. MD*).</span><span class="sxs-lookup"><span data-stu-id="88603-284">Supported file formats include only Markdown (*.md*).</span></span>

<span data-ttu-id="88603-285">Například:</span><span class="sxs-lookup"><span data-stu-id="88603-285">For example:</span></span>

```xml
<PropertyGroup>
    ...
    <PackageReadmeFile>readme.md</PackageReadmeFile>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="docs\readme.md" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

<span data-ttu-id="88603-286">V případě nuspec potřeby si přečtěte [ nuspec referenční informace k souboru Readme](nuspec.md#readme).</span><span class="sxs-lookup"><span data-stu-id="88603-286">For the nuspec equivalent, take a look at [nuspec reference for readme](nuspec.md#readme).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="88603-287">Výstupní sestavení</span><span class="sxs-lookup"><span data-stu-id="88603-287">Output assemblies</span></span>

<span data-ttu-id="88603-288">`nuget pack` zkopíruje výstupní soubory s příponami,,,, `.exe` `.dll` `.xml` `.winmd` `.json` a `.pri` .</span><span class="sxs-lookup"><span data-stu-id="88603-288">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="88603-289">Výstupní soubory, které jsou kopírovány, závisí na tom, co MSBuild poskytuje `BuiltOutputProjectGroup` cíl.</span><span class="sxs-lookup"><span data-stu-id="88603-289">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="88603-290">Existují dvě MSBuild  vlastnosti, které lze použít v souboru projektu nebo na příkazovém řádku pro řízení, kde výstupní sestavení jdou:</span><span class="sxs-lookup"><span data-stu-id="88603-290">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="88603-291">`IncludeBuildOutput`: Logická hodnota, která určuje, zda mají být do balíčku zahrnuty výstupní sestavení sestavení.</span><span class="sxs-lookup"><span data-stu-id="88603-291">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="88603-292">`BuildOutputTargetFolder`: Určuje složku, do které se mají umístit výstupní sestavení.</span><span class="sxs-lookup"><span data-stu-id="88603-292">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="88603-293">Výstupní sestavení (a další výstupní soubory) se zkopírují do příslušných složek rozhraní.</span><span class="sxs-lookup"><span data-stu-id="88603-293">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="88603-294">Odkazy na balíčky</span><span class="sxs-lookup"><span data-stu-id="88603-294">Package references</span></span>

<span data-ttu-id="88603-295">Viz [odkazy na balíčky v souborech projektu](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="88603-295">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="88603-296">Odkazy na projekt a projekt</span><span class="sxs-lookup"><span data-stu-id="88603-296">Project to project references</span></span>

<span data-ttu-id="88603-297">Odkazy na projekt na projekt se považují za výchozí jako NuGet odkazy na balíčky.</span><span class="sxs-lookup"><span data-stu-id="88603-297">Project to project references are considered by default as NuGet package references.</span></span> <span data-ttu-id="88603-298">Například:</span><span class="sxs-lookup"><span data-stu-id="88603-298">For example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="88603-299">Do odkazu na projekt můžete také přidat následující metadata:</span><span class="sxs-lookup"><span data-stu-id="88603-299">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="88603-300">Zahrnutí obsahu do balíčku</span><span class="sxs-lookup"><span data-stu-id="88603-300">Including content in a package</span></span>

<span data-ttu-id="88603-301">Chcete-li zahrnout obsah, přidejte do existující položky metadata navíc `<Content>` .</span><span class="sxs-lookup"><span data-stu-id="88603-301">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="88603-302">Ve výchozím nastavení jsou všechny položky typu "obsah" zahrnuty do balíčku, Pokud nepřepíšete záznamy podobné následujícímu:</span><span class="sxs-lookup"><span data-stu-id="88603-302">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="88603-303">Ve výchozím nastavení je vše přidáno do kořenu `content` a `contentFiles\any\<target_framework>` složky v rámci balíčku a zachovává strukturu relativních složek, pokud nezadáte cestu k balíčku:</span><span class="sxs-lookup"><span data-stu-id="88603-303">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="88603-304">Pokud chcete kopírovat veškerý obsah jenom na konkrétní kořenové složky (místo `content` a `contentFiles` obojí), můžete použít MSBuild vlastnost `ContentTargetFolders` , která má výchozí hodnotu Content; contentFiles, ale dá se nastavit na jiné názvy složek.</span><span class="sxs-lookup"><span data-stu-id="88603-304">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="88603-305">Všimněte si, že pouze zadání "contentFiles" v `ContentTargetFolders` souboru vloží soubory do `contentFiles\any\<target_framework>` nebo na `contentFiles\<language>\<target_framework>` základě `buildAction` .</span><span class="sxs-lookup"><span data-stu-id="88603-305">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="88603-306">`PackagePath` může se jednat o sadu cílových cest oddělených středníky.</span><span class="sxs-lookup"><span data-stu-id="88603-306">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="88603-307">Zadáním prázdné cesty k balíčku by se soubor přidal do kořenového adresáře balíčku.</span><span class="sxs-lookup"><span data-stu-id="88603-307">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="88603-308">Například následující příkaz přidá `libuv.txt` do `content\myfiles` , `content\samples` a kořenovou složku balíčku:</span><span class="sxs-lookup"><span data-stu-id="88603-308">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="88603-309">K dispozici je také MSBuild vlastnost `$(IncludeContentInPack)` , která má výchozí hodnotu `true` .</span><span class="sxs-lookup"><span data-stu-id="88603-309">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="88603-310">Pokud je nastavená na `false` libovolný projekt, pak obsah z tohoto projektu není zahrnutý v balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="88603-310">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="88603-311">Další metadata specifická pro sadu, která můžete nastavit na kterékoli z výše uvedených položek, obsahují ```<PackageCopyToOutput>``` a ```<PackageFlatten>``` které sady ```CopyToOutput``` a ```Flatten``` hodnoty mají ```contentFiles``` položku ve výstupu nuspec .</span><span class="sxs-lookup"><span data-stu-id="88603-311">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="88603-312">Kromě položek obsahu `<Pack>` `<PackagePath>` lze metadata a také nastavit na soubory s akcí sestavení kompilovat, EmbeddedResource, ApplicationDefinition, Page, Resource, třídy SplashScreen, vazbě designdata, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource nebo None.</span><span class="sxs-lookup"><span data-stu-id="88603-312">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="88603-313">Pokud má balíček při použití vzorů expanze názvů připojit název souboru k cestě k balíčku, musí cesta k balíčku končit znakem oddělovače složky. v opačném případě se cesta k balíčku považuje za úplnou cestu včetně názvu souboru.</span><span class="sxs-lookup"><span data-stu-id="88603-313">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="88603-314">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="88603-314">IncludeSymbols</span></span>

<span data-ttu-id="88603-315">Při použití se `MSBuild -t:pack -p:IncludeSymbols=true` `.pdb` zkopírují odpovídající soubory spolu s jinými výstupními soubory ( `.dll` , `.exe` , `.winmd` , `.xml` , `.json` , `.pri` ).</span><span class="sxs-lookup"><span data-stu-id="88603-315">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="88603-316">Všimněte si, že nastavení `IncludeSymbols=true` vytvoří regulární balíček *a* balíček symbolů.</span><span class="sxs-lookup"><span data-stu-id="88603-316">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="88603-317">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="88603-317">IncludeSource</span></span>

<span data-ttu-id="88603-318">To je stejné jako `IncludeSymbols` s tím rozdílem, že kopíruje také zdrojové soubory spolu se `.pdb` soubory.</span><span class="sxs-lookup"><span data-stu-id="88603-318">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="88603-319">Všechny soubory typu `Compile` jsou zkopírovány za účelem `src\<ProjectName>\` zachování struktury složek relativní cesty ve výsledném balíčku.</span><span class="sxs-lookup"><span data-stu-id="88603-319">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="88603-320">Totéž se také stane u zdrojových souborů, `ProjectReference` které mají `TreatAsPackageReference` nastavené na `false` .</span><span class="sxs-lookup"><span data-stu-id="88603-320">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="88603-321">Pokud je soubor typu Compile mimo složku projektu, pak je pouze přidán do `src\<ProjectName>\` .</span><span class="sxs-lookup"><span data-stu-id="88603-321">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="88603-322">Balení licenčního výrazu nebo licenčního souboru</span><span class="sxs-lookup"><span data-stu-id="88603-322">Packing a license expression or a license file</span></span>

<span data-ttu-id="88603-323">Při použití licenčního výrazu použijte `PackageLicenseExpression` vlastnost.</span><span class="sxs-lookup"><span data-stu-id="88603-323">When using a license expression, use the `PackageLicenseExpression` property.</span></span> <span data-ttu-id="88603-324">Ukázku najdete v tématu [Ukázka licenčního výrazu](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="88603-324">For a sample, see [License expression sample](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="88603-325">Další informace o výrazech licencí a licencích, které jsou přijaty organizací NuGet . org, najdete v tématu [metadata licencí](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="88603-325">To learn more about license expressions and licenses that are accepted by NuGet.org, see [license metadata](nuspec.md#license).</span></span>

<span data-ttu-id="88603-326">Při balení licenčního souboru použijte `PackageLicenseFile` vlastnost k určení cesty k balíčku relativní ke kořenu balíčku.</span><span class="sxs-lookup"><span data-stu-id="88603-326">When packing a license file, use `PackageLicenseFile` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="88603-327">Navíc se ujistěte, že je soubor součástí balíčku.</span><span class="sxs-lookup"><span data-stu-id="88603-327">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="88603-328">Například:</span><span class="sxs-lookup"><span data-stu-id="88603-328">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="88603-329">Ukázku najdete v části [Ukázka souboru s licencí](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="88603-329">For a sample, see [License file sample](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample).</span></span>

> [!NOTE]
> <span data-ttu-id="88603-330">`PackageLicenseExpression` `PackageLicenseFile` `PackageLicenseUrl` V jednom okamžiku může být určena pouze jedna z, a.</span><span class="sxs-lookup"><span data-stu-id="88603-330">Only one of `PackageLicenseExpression`, `PackageLicenseFile`, and `PackageLicenseUrl` can be specified at a time.</span></span>

### <a name="packing-a-file-without-an-extension"></a><span data-ttu-id="88603-331">Balení souboru bez přípony</span><span class="sxs-lookup"><span data-stu-id="88603-331">Packing a file without an extension</span></span>

<span data-ttu-id="88603-332">V některých scénářích, jako je například balení souboru s licencí, může být vhodné zahrnout soubor bez přípony.</span><span class="sxs-lookup"><span data-stu-id="88603-332">In some scenarios, like when packing a license file, you might want to include a file without an extension.</span></span>
<span data-ttu-id="88603-333">Z historických důvodů NuGet  &  MSBuild považovat cesty bez přípony jako adresáře.</span><span class="sxs-lookup"><span data-stu-id="88603-333">For historical reasons, NuGet & MSBuild treat paths without an extension as directories.</span></span>

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

<span data-ttu-id="88603-334">[Soubor bez ukázkového rozšíření](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/).</span><span class="sxs-lookup"><span data-stu-id="88603-334">[File without an extension sample](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/).</span></span>

### <a name="istool"></a><span data-ttu-id="88603-335">Nástroj</span><span class="sxs-lookup"><span data-stu-id="88603-335">IsTool</span></span>

<span data-ttu-id="88603-336">Při použití `MSBuild -t:pack -p:IsTool=true` aplikace jsou všechny výstupní soubory, jak je uvedeno ve scénáři [výstup sestavení](#output-assemblies) , zkopírovány do `tools` složky namísto `lib` složky.</span><span class="sxs-lookup"><span data-stu-id="88603-336">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="88603-337">Všimněte si, že se liší od a, `DotNetCliTool` který je určen nastavením `PackageType` v `.csproj` souboru.</span><span class="sxs-lookup"><span data-stu-id="88603-337">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec-file"></a><span data-ttu-id="88603-338">Balení pomocí `.nuspec` souboru</span><span class="sxs-lookup"><span data-stu-id="88603-338">Packing using a `.nuspec` file</span></span>

<span data-ttu-id="88603-339">I když se místo toho doporučuje [Zahrnout všechny vlastnosti](../reference/msbuild-targets.md#pack-target) , které jsou obvykle v `.nuspec` souboru v souboru projektu, můžete zvolit použití `.nuspec` souboru k balení projektu.</span><span class="sxs-lookup"><span data-stu-id="88603-339">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="88603-340">Pro projekt bez sady SDK, který používá, je `PackageReference` nutné importovat, `NuGet.Build.Tasks.Pack.targets` aby bylo možné spustit úlohu balíčku.</span><span class="sxs-lookup"><span data-stu-id="88603-340">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="88603-341">Před zabalením souboru je ještě nutné projekt obnovit nuspec .</span><span class="sxs-lookup"><span data-stu-id="88603-341">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="88603-342">(Projekt ve stylu sady SDK obsahuje cíle balíčku ve výchozím nastavení.)</span><span class="sxs-lookup"><span data-stu-id="88603-342">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="88603-343">Cílová architektura souboru projektu je nerelevantní a nepoužívá se při balení nuspec .</span><span class="sxs-lookup"><span data-stu-id="88603-343">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="88603-344">Následující tři MSBuild vlastnosti jsou relevantní pro balení pomocí `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="88603-344">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="88603-345">`NuspecFile`: relativní nebo absolutní cesta k `.nuspec` souboru, který se používá k balení.</span><span class="sxs-lookup"><span data-stu-id="88603-345">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="88603-346">`NuspecProperties`: středníkem oddělený seznam dvojic klíč = hodnota.</span><span class="sxs-lookup"><span data-stu-id="88603-346">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="88603-347">Z důvodu způsobu, jakým MSBuild funguje analýza příkazového řádku, je nutné zadat více vlastností následujícím způsobem: `-p:NuspecProperties="key1=value1;key2=value2"` .</span><span class="sxs-lookup"><span data-stu-id="88603-347">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties="key1=value1;key2=value2"`.</span></span>  
1. <span data-ttu-id="88603-348">`NuspecBasePath`: Základní cesta k `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="88603-348">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="88603-349">Pokud používáte `dotnet.exe` k balení projektu, použijte příkaz podobný následujícímu:</span><span class="sxs-lookup"><span data-stu-id="88603-349">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="88603-350">Pokud používáte MSBuild k balení projektu, použijte příkaz podobný následujícímu:</span><span class="sxs-lookup"><span data-stu-id="88603-350">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="88603-351">Všimněte si, že balení a nuspec použití dotnet.exe nebo MSBuild také vede k sestavení projektu ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="88603-351">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="88603-352">K tomu je možné se vyhnout předáním ```--no-build``` vlastnosti do dotnet.exe, což je ekvivalent nastavení ```<NoBuild>true</NoBuild> ``` v souboru projektu spolu s nastavením ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="88603-352">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="88603-353">Příkladem souboru *. csproj* pro sbalení nuspec souboru je:</span><span class="sxs-lookup"><span data-stu-id="88603-353">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="88603-354">Rozšířené body rozšíření pro vytvoření přizpůsobeného balíčku</span><span class="sxs-lookup"><span data-stu-id="88603-354">Advanced extension points to create customized package</span></span>

<span data-ttu-id="88603-355">`pack`Cíl poskytuje dva Rozšiřovací body, které jsou spuštěny v sestavení specifickém pro vnitřní, cílové rozhraní.</span><span class="sxs-lookup"><span data-stu-id="88603-355">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="88603-356">Rozšiřující body podporují obsah a sestavení konkrétního cílového rozhraní do balíčku:</span><span class="sxs-lookup"><span data-stu-id="88603-356">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="88603-357">`TargetsForTfmSpecificBuildOutput` cíl: použijte pro soubory uvnitř `lib` složky nebo složky zadané pomocí `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="88603-357">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="88603-358">`TargetsForTfmSpecificContentInPackage` cíl: použijte pro soubory mimo `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="88603-358">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### `TargetsForTfmSpecificBuildOutput`

<span data-ttu-id="88603-359">Napište vlastní cíl a zadejte ho jako hodnotu `$(TargetsForTfmSpecificBuildOutput)` Vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="88603-359">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="88603-360">Pro všechny soubory, které potřebují přejít do nástroje `BuildOutputTargetFolder` (ve výchozím nastavení lib), by měl cíl zapisovat tyto soubory do skupiny Item `BuildOutputInPackage` a nastavit následující dvě hodnoty metadat:</span><span class="sxs-lookup"><span data-stu-id="88603-360">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="88603-361">`FinalOutputPath`: Absolutní cesta k souboru; Pokud není zadaný, použije se identita k vyhodnocení zdrojové cesty.</span><span class="sxs-lookup"><span data-stu-id="88603-361">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="88603-362">`TargetPath`: (Volitelné) nastavte, kdy bude soubor potřebovat přejít do podsložky v rámci `lib\<TargetFramework>` , jako jsou satelitní sestavení, která se nacházejí v odpovídajících složkách kultury.</span><span class="sxs-lookup"><span data-stu-id="88603-362">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="88603-363">Výchozí hodnota je název souboru.</span><span class="sxs-lookup"><span data-stu-id="88603-363">Defaults to the name of the file.</span></span>

<span data-ttu-id="88603-364">Příklad:</span><span class="sxs-lookup"><span data-stu-id="88603-364">Example:</span></span>

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

#### `TargetsForTfmSpecificContentInPackage`

<span data-ttu-id="88603-365">Napište vlastní cíl a zadejte ho jako hodnotu `$(TargetsForTfmSpecificContentInPackage)` Vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="88603-365">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="88603-366">U všech souborů, které se mají zahrnout do balíčku, by měl cíl tyto soubory zapsat do `TfmSpecificPackageFile` skupiny položek a nastavit následující volitelná metadata:</span><span class="sxs-lookup"><span data-stu-id="88603-366">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="88603-367">`PackagePath`: Cesta, kde by měl být v balíčku výstup souboru.</span><span class="sxs-lookup"><span data-stu-id="88603-367">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="88603-368">NuGet vydá upozornění, pokud se ke stejné cestě balíčku přidá více než jeden soubor.</span><span class="sxs-lookup"><span data-stu-id="88603-368">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="88603-369">`BuildAction`: Akce sestavení, která se má souboru přiřadit, se vyžaduje jenom v případě, že je cesta k balíčku ve `contentFiles` složce.</span><span class="sxs-lookup"><span data-stu-id="88603-369">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="88603-370">Výchozí hodnota je None.</span><span class="sxs-lookup"><span data-stu-id="88603-370">Defaults to "None".</span></span>

<span data-ttu-id="88603-371">Příklad:</span><span class="sxs-lookup"><span data-stu-id="88603-371">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="88603-372">cíl obnovení</span><span class="sxs-lookup"><span data-stu-id="88603-372">restore target</span></span>

<span data-ttu-id="88603-373">`MSBuild -t:restore` (které `nuget restore` a `dotnet restore` používají se v projektech .NET Core), obnoví balíčky, na které se odkazuje v souboru projektu, takto:</span><span class="sxs-lookup"><span data-stu-id="88603-373">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="88603-374">Číst všechny odkazy z projektu na projekt</span><span class="sxs-lookup"><span data-stu-id="88603-374">Read all project to project references</span></span>
1. <span data-ttu-id="88603-375">Přečtěte si vlastnosti projektu a najděte mezilehlé složky a cílová rozhraní.</span><span class="sxs-lookup"><span data-stu-id="88603-375">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="88603-376">Předání MSBuild dat do NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="88603-376">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="88603-377">Spustit obnovení</span><span class="sxs-lookup"><span data-stu-id="88603-377">Run restore</span></span>
1. <span data-ttu-id="88603-378">Stáhnout balíčky</span><span class="sxs-lookup"><span data-stu-id="88603-378">Download packages</span></span>
1. <span data-ttu-id="88603-379">Zápis souboru prostředků, cílů a vlastností props</span><span class="sxs-lookup"><span data-stu-id="88603-379">Write assets file, targets, and props</span></span>

<span data-ttu-id="88603-380">`restore`Cíl funguje pro projekty, které používají formát PackageReference.</span><span class="sxs-lookup"><span data-stu-id="88603-380">The `restore` target works for projects using the PackageReference format.</span></span>
<span data-ttu-id="88603-381">`MSBuild 16.5+` má také [podporu](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) pro `packages.config` formát.</span><span class="sxs-lookup"><span data-stu-id="88603-381">`MSBuild 16.5+` also has [opt-in support](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) for the `packages.config` format.</span></span>

> [!NOTE]
> <span data-ttu-id="88603-382">`restore`Cíl [by neměl být spuštěn](#restoring-and-building-with-one-msbuild-command) v kombinaci s `build` cílem.</span><span class="sxs-lookup"><span data-stu-id="88603-382">The `restore` target [should not be run](#restoring-and-building-with-one-msbuild-command) in combination with the `build` target.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="88603-383">Obnovit vlastnosti</span><span class="sxs-lookup"><span data-stu-id="88603-383">Restore properties</span></span>

<span data-ttu-id="88603-384">Další nastavení obnovení může pocházet z MSBuild vlastností v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="88603-384">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="88603-385">Hodnoty lze také nastavit z příkazového řádku pomocí `-p:` přepínače (viz příklady níže).</span><span class="sxs-lookup"><span data-stu-id="88603-385">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="88603-386">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="88603-386">Property</span></span> | <span data-ttu-id="88603-387">Popis</span><span class="sxs-lookup"><span data-stu-id="88603-387">Description</span></span> |
|--------|--------|
| `RestoreSources` | <span data-ttu-id="88603-388">Seznam zdrojů balíčků oddělených středníkem.</span><span class="sxs-lookup"><span data-stu-id="88603-388">Semicolon-delimited list of package sources.</span></span> |
| `RestorePackagesPath` | <span data-ttu-id="88603-389">Cesta ke složce uživatelských balíčků</span><span class="sxs-lookup"><span data-stu-id="88603-389">User packages folder path.</span></span> |
| `RestoreDisableParallel` | <span data-ttu-id="88603-390">Omezit stahování na jednu po druhé.</span><span class="sxs-lookup"><span data-stu-id="88603-390">Limit downloads to one at a time.</span></span> |
| `RestoreConfigFile` | <span data-ttu-id="88603-391">Cesta k `Nuget.Config` souboru, který se má použít</span><span class="sxs-lookup"><span data-stu-id="88603-391">Path to a `Nuget.Config` file to apply.</span></span> |
| `RestoreNoCache` | <span data-ttu-id="88603-392">Je-li nastavena hodnota true, nepoužívejte balíčky uložené v mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="88603-392">If true, avoids using cached packages.</span></span> <span data-ttu-id="88603-393">Viz [Správa globálních balíčků a složek mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="88603-393">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| `RestoreIgnoreFailedSources` | <span data-ttu-id="88603-394">Pokud má hodnotu true, ignoruje neúspěšné nebo chybějící zdroje balíčků.</span><span class="sxs-lookup"><span data-stu-id="88603-394">If true, ignores failing or missing package sources.</span></span> |
| `RestoreFallbackFolders` | <span data-ttu-id="88603-395">Záložní složky používané ve stejném způsobu, jakým se používá složka uživatelských balíčků.</span><span class="sxs-lookup"><span data-stu-id="88603-395">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| `RestoreAdditionalProjectSources` | <span data-ttu-id="88603-396">Další zdroje, které se mají použít při obnovení.</span><span class="sxs-lookup"><span data-stu-id="88603-396">Additional sources to use during restore.</span></span> |
| `RestoreAdditionalProjectFallbackFolders` | <span data-ttu-id="88603-397">Další záložní složky, které se mají použít při obnovení</span><span class="sxs-lookup"><span data-stu-id="88603-397">Additional fallback folders to use during restore.</span></span> |
| `RestoreAdditionalProjectFallbackFoldersExcludes` | <span data-ttu-id="88603-398">Vyloučí záložní složky zadané v `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="88603-398">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| `RestoreTaskAssemblyFile` | <span data-ttu-id="88603-399">Cesta k `NuGet.Build.Tasks.dll` .</span><span class="sxs-lookup"><span data-stu-id="88603-399">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| `RestoreGraphProjectInput` | <span data-ttu-id="88603-400">Středníkem oddělený seznam projektů, které mají být obnoveny, které by měly obsahovat absolutní cesty.</span><span class="sxs-lookup"><span data-stu-id="88603-400">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| `RestoreUseSkipNonexistentTargets`  | <span data-ttu-id="88603-401">Když se projekty shromažďují prostřednictvím MSBuild , zjistí, jestli se shromažďují pomocí `SkipNonexistentTargets` optimalizace.</span><span class="sxs-lookup"><span data-stu-id="88603-401">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="88603-402">Pokud není nastaveno, výchozí hodnota je `true` .</span><span class="sxs-lookup"><span data-stu-id="88603-402">When not set, defaults to `true`.</span></span> <span data-ttu-id="88603-403">Příčinou je rychlé chování při selhání, když cíle projektu nelze importovat.</span><span class="sxs-lookup"><span data-stu-id="88603-403">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| `MSBuildProjectExtensionsPath` | <span data-ttu-id="88603-404">Výstupní složka, výchozí nastavení `BaseIntermediateOutputPath` a `obj` Složka.</span><span class="sxs-lookup"><span data-stu-id="88603-404">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| `RestoreForce` | <span data-ttu-id="88603-405">V projektech založených na PackageReference vynutí vyřešení všech závislostí i v případě, že bylo poslední obnovení úspěšné.</span><span class="sxs-lookup"><span data-stu-id="88603-405">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="88603-406">Zadání tohoto příznaku se podobá odstranění `project.assets.json` souboru.</span><span class="sxs-lookup"><span data-stu-id="88603-406">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="88603-407">To neobejde mezipaměť HTTP-cache.</span><span class="sxs-lookup"><span data-stu-id="88603-407">This does not bypass the http-cache.</span></span> |
| `RestorePackagesWithLockFile` | <span data-ttu-id="88603-408">Výslovný se na použití souboru zámku.</span><span class="sxs-lookup"><span data-stu-id="88603-408">Opts into the usage of a lock file.</span></span> |
| `RestoreLockedMode` | <span data-ttu-id="88603-409">Spustit obnovení v uzamčeném režimu.</span><span class="sxs-lookup"><span data-stu-id="88603-409">Run restore in locked mode.</span></span> <span data-ttu-id="88603-410">To znamená, že obnovení nebude přehodnocovat závislosti.</span><span class="sxs-lookup"><span data-stu-id="88603-410">This means that restore will not reevaluate the dependencies.</span></span> |
| `NuGetLockFilePath` | <span data-ttu-id="88603-411">Vlastní umístění souboru zámku.</span><span class="sxs-lookup"><span data-stu-id="88603-411">A custom location for the lock file.</span></span> <span data-ttu-id="88603-412">Výchozí umístění je vedle projektu a je pojmenováno `packages.lock.json` .</span><span class="sxs-lookup"><span data-stu-id="88603-412">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| `RestoreForceEvaluate` | <span data-ttu-id="88603-413">Vynutí obnovení pro přepočítání závislostí a aktualizaci souboru zámku bez upozornění.</span><span class="sxs-lookup"><span data-stu-id="88603-413">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> |
| `RestorePackagesConfig` | <span data-ttu-id="88603-414">Přepínač pro výslovný souhlas, který obnovuje projekty pomocí packages.config. Podpora pouze s nástrojem `MSBuild -t:restore` .</span><span class="sxs-lookup"><span data-stu-id="88603-414">An opt-in switch, that restores projects with packages.config. Support with `MSBuild -t:restore` only.</span></span> |
| `RestoreUseStaticGraphEvaluation` | <span data-ttu-id="88603-415">Přepínač výslovného souhlasu pro použití statického MSBuild vyhodnocení grafu namísto standardního vyhodnocení.</span><span class="sxs-lookup"><span data-stu-id="88603-415">An opt-in switch to use static graph MSBuild evaluation instead of the standard evaluation.</span></span> <span data-ttu-id="88603-416">Statické vyhodnocení grafu je experimentální funkce, která je výrazně rychlejší pro velké úložiště a řešení.</span><span class="sxs-lookup"><span data-stu-id="88603-416">Static graph evaluation is an experimental feature that's significantly faster for large repos and solutions.</span></span> |

#### <a name="examples"></a><span data-ttu-id="88603-417">Příklady</span><span class="sxs-lookup"><span data-stu-id="88603-417">Examples</span></span>

<span data-ttu-id="88603-418">Příkazový řádek:</span><span class="sxs-lookup"><span data-stu-id="88603-418">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="88603-419">Soubor projektu:</span><span class="sxs-lookup"><span data-stu-id="88603-419">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="88603-420">Obnovit výstupy</span><span class="sxs-lookup"><span data-stu-id="88603-420">Restore outputs</span></span>

<span data-ttu-id="88603-421">Obnovení vytvoří ve složce buildu následující soubory `obj` :</span><span class="sxs-lookup"><span data-stu-id="88603-421">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="88603-422">Soubor</span><span class="sxs-lookup"><span data-stu-id="88603-422">File</span></span> | <span data-ttu-id="88603-423">Description</span><span class="sxs-lookup"><span data-stu-id="88603-423">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="88603-424">Obsahuje graf závislostí všech odkazů na balíčky.</span><span class="sxs-lookup"><span data-stu-id="88603-424">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="88603-425">Odkazy na MSBuild props obsažené v balíčcích</span><span class="sxs-lookup"><span data-stu-id="88603-425">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="88603-426">Odkazy na MSBuild cíle obsažené v balíčcích</span><span class="sxs-lookup"><span data-stu-id="88603-426">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="88603-427">Obnovení a sestavování pomocí jednoho MSBuild příkazu</span><span class="sxs-lookup"><span data-stu-id="88603-427">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="88603-428">Z důvodu faktu, že NuGet může obnovit balíčky, které MSBuild vycházejí z cílů a vlastností, jsou vyhodnocení obnovení a sestavení spouštěny s různými globálními vlastnostmi.</span><span class="sxs-lookup"><span data-stu-id="88603-428">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="88603-429">To znamená, že následující nastavení bude mít nepředvídatelné a často nesprávné chování.</span><span class="sxs-lookup"><span data-stu-id="88603-429">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="88603-430">Místo doporučeného přístupu:</span><span class="sxs-lookup"><span data-stu-id="88603-430">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="88603-431">Stejná logika platí pro jiné cíle podobné `build` .</span><span class="sxs-lookup"><span data-stu-id="88603-431">The same logic applies to other targets similar to `build`.</span></span>

### <a name="restoring-packagereference-and-packagesconfig-projects-with-msbuild"></a><span data-ttu-id="88603-432">Obnovení projektů PackageReference a packages.config pomocí MSBuild</span><span class="sxs-lookup"><span data-stu-id="88603-432">Restoring PackageReference and packages.config projects with MSBuild</span></span>

<span data-ttu-id="88603-433">U MSBuild 16.5 + se taky pro podporuje i packages.config `msbuild -t:restore` .</span><span class="sxs-lookup"><span data-stu-id="88603-433">With MSBuild 16.5+, packages.config are also supported for `msbuild -t:restore`.</span></span>

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> <span data-ttu-id="88603-434">`packages.config` obnovení je k dispozici pouze pro `MSBuild 16.5+` , a nikoli s `dotnet.exe`</span><span class="sxs-lookup"><span data-stu-id="88603-434">`packages.config` restore is only available with `MSBuild 16.5+`, and not with `dotnet.exe`</span></span>

### <a name="restoring-with-msbuild-static-graph-evaluation"></a><span data-ttu-id="88603-435">Obnovení pomocí MSBuild statického vyhodnocení grafu</span><span class="sxs-lookup"><span data-stu-id="88603-435">Restoring with MSBuild static graph evaluation</span></span>

> [!NOTE]
> <span data-ttu-id="88603-436">Pomocí MSBuild 16.6 + NuGet Nástroj přidal experimentální funkci pro použití statického vyhodnocení grafu z příkazového řádku, který významně vylepšuje čas obnovení pro velká úložiště.</span><span class="sxs-lookup"><span data-stu-id="88603-436">With MSBuild 16.6+, NuGet has added an experimental feature to use static graph evaluation from the command line that significantly improves the restore time for large repositories.</span></span>

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

<span data-ttu-id="88603-437">Případně ho můžete povolit nastavením vlastnosti v adresáři. Build. props.</span><span class="sxs-lookup"><span data-stu-id="88603-437">Alternatively you can enable it by setting the property in a Directory.Build.Props.</span></span>

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> <span data-ttu-id="88603-438">Od sady Visual Studio 2019. x a NuGet 5. x se tato funkce považuje za experimentální a výslovný souhlas.</span><span class="sxs-lookup"><span data-stu-id="88603-438">As of Visual Studio 2019.x and NuGet 5.x, this feature is considered experimental and opt-in.</span></span> <span data-ttu-id="88603-439">Pokud bude tato funkce ve výchozím nastavení povolená, postupujte podle [ NuGet /Home # 9803](https://github.com/NuGet/Home/issues/9803) .</span><span class="sxs-lookup"><span data-stu-id="88603-439">Follow [NuGet/Home#9803](https://github.com/NuGet/Home/issues/9803) for details on when this feature will be enabled by default.</span></span>

<span data-ttu-id="88603-440">Statické obnovení grafu mění část obnovení MSBuild, projekt čte a vyhodnocuje, ale nikoli algoritmus obnovení.</span><span class="sxs-lookup"><span data-stu-id="88603-440">Static graph restore changes the msbuild part of restore, the project reading and evaluation, but not the restore algorithm!</span></span> <span data-ttu-id="88603-441">Algoritmus obnovení je stejný u všech NuGet nástrojů ( NuGet . exe, MSBuild . exe, dotnet.exe a Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="88603-441">The restore algorithm is the same across all NuGet tools (NuGet.exe, MSBuild.exe, dotnet.exe and Visual Studio).</span></span>

<span data-ttu-id="88603-442">Ve velmi málo scénářích se statické obnovení grafu může chovat odlišně od aktuálního obnovení a některé deklarované PackageReferences nebo ProjectReferences mohou chybět.</span><span class="sxs-lookup"><span data-stu-id="88603-442">In very few scenarios, static graph restore may behave differently from current restore and certain declared PackageReferences or ProjectReferences might be missing.</span></span>

<span data-ttu-id="88603-443">Pokud chcete při migraci na statický graf obnovit svůj názor, zvažte spuštění:</span><span class="sxs-lookup"><span data-stu-id="88603-443">To ease your mind, as a one time check, when migrating to static graph restore, consider running:</span></span>

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

<span data-ttu-id="88603-444">NuGet neměl *by hlásit* žádné změny.</span><span class="sxs-lookup"><span data-stu-id="88603-444">NuGet should *not* report any changes.</span></span> <span data-ttu-id="88603-445">Pokud se zobrazí nesoulad, uveďte problém na adrese [ NuGet /Home](https://github.com/nuget/home/issues/new).</span><span class="sxs-lookup"><span data-stu-id="88603-445">If you do see a discrepancy, please file an issue at [NuGet/Home](https://github.com/nuget/home/issues/new).</span></span>

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="88603-446">Nahrazení jedné knihovny z grafu obnovení</span><span class="sxs-lookup"><span data-stu-id="88603-446">Replacing one library from a restore graph</span></span>

<span data-ttu-id="88603-447">Pokud obnovení předává nesprávné sestavení, je možné vyřadit výchozí volbu balíčků a nahradit ji vlastní volbou.</span><span class="sxs-lookup"><span data-stu-id="88603-447">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="88603-448">Nejprve s nejvyšší úrovní `PackageReference` , vylučte všechny prostředky:</span><span class="sxs-lookup"><span data-stu-id="88603-448">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="88603-449">Dále přidejte vlastní odkaz na příslušnou místní kopii knihovny DLL:</span><span class="sxs-lookup"><span data-stu-id="88603-449">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
