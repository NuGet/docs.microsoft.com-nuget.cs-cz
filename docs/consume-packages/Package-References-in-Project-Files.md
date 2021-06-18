---
title: Formát NuGet PackageReference (odkazy na balíčky v souborech projektu)
description: Podrobnosti o NuGet PackageReference v souborech projektu, které podporuje NuGet 4.0 + a VS2017 a .NET Core 2,0
author: nkolev92
ms.author: nikolev
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: c7b963352e0e9640844a213767a58c883ed0eeb9
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323710"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="ffb2e-103">Odkazy na balíčky ( `PackageReference` ) v souborech projektu</span><span class="sxs-lookup"><span data-stu-id="ffb2e-103">Package references (`PackageReference`) in project files</span></span>

<span data-ttu-id="ffb2e-104">Odkazy na balíčky, použití `PackageReference` uzlu, Správa závislostí NuGet přímo v souborech projektu (na rozdíl od samostatného `packages.config` souboru).</span><span class="sxs-lookup"><span data-stu-id="ffb2e-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="ffb2e-105">Použití PackageReference, jak je voláno, nemá vliv na jiné aspekty NuGet; například nastavení v `NuGet.Config` souborech (včetně zdrojů balíčků) jsou stále aplikována, jak je vysvětleno v tématu [běžné konfigurace NuGet](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="ffb2e-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Common NuGet configurations](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="ffb2e-106">Pomocí PackageReference můžete také použít podmínky nástroje MSBuild pro výběr odkazů na balíčky na cílové rozhraní nebo jiná seskupení.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, or other groupings.</span></span> <span data-ttu-id="ffb2e-107">Umožňuje také jemně odstupňovanou kontrolu nad závislostmi a tokem obsahu.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="ffb2e-108">(Další podrobnosti najdete v tématu Další informace o [sadě NuGet Pack a obnovení jako cíle MSBuild](../reference/msbuild-targets.md).)</span><span class="sxs-lookup"><span data-stu-id="ffb2e-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

## <a name="project-type-support"></a><span data-ttu-id="ffb2e-109">Podpora typu projektu</span><span class="sxs-lookup"><span data-stu-id="ffb2e-109">Project type support</span></span>

<span data-ttu-id="ffb2e-110">Ve výchozím nastavení se PackageReference používá pro projekty .NET Core, .NET Standard projekty a projekty UWP cílené na Windows 10 Build 15063 (Creators Update) a novější, s výjimkou projektů v jazyce C++ UWP.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="ffb2e-111">Projekty .NET Framework podporují PackageReference, ale aktuálně mají výchozí hodnotu `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="ffb2e-111">.NET Framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="ffb2e-112">Chcete-li použít PackageReference, [migrujte](../consume-packages/migrate-packages-config-to-package-reference.md) závislosti z nástroje `packages.config` do souboru projektu a pak odeberte packages.config.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-112">To use PackageReference, [migrate](../consume-packages/migrate-packages-config-to-package-reference.md) the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

<span data-ttu-id="ffb2e-113">ASP.NET aplikace, které cílí na úplné .NET Framework, zahrnují jenom [omezené podpory](https://github.com/NuGet/Home/issues/5877) pro PackageReference.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-113">ASP.NET apps targeting the full .NET Framework include only [limited support](https://github.com/NuGet/Home/issues/5877) for PackageReference.</span></span> <span data-ttu-id="ffb2e-114">Typy projektů C++ a JavaScript nejsou podporovány.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-114">C++ and JavaScript project types are unsupported.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="ffb2e-115">Přidání PackageReference</span><span class="sxs-lookup"><span data-stu-id="ffb2e-115">Adding a PackageReference</span></span>

<span data-ttu-id="ffb2e-116">Přidejte závislost do souboru projektu pomocí následující syntaxe:</span><span class="sxs-lookup"><span data-stu-id="ffb2e-116">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="ffb2e-117">Řízení verze závislosti</span><span class="sxs-lookup"><span data-stu-id="ffb2e-117">Controlling dependency version</span></span>

<span data-ttu-id="ffb2e-118">Konvence pro určení verze balíčku je stejná jako při použití `packages.config` :</span><span class="sxs-lookup"><span data-stu-id="ffb2e-118">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="ffb2e-119">V příkladu výše 3.6.0 označuje všechny verze, které jsou >= 3.6.0 s upřednostněním pro nejnižší verzi, jak je popsáno v tématu [Správa verzí balíčků](../concepts/package-versioning.md#version-ranges).</span><span class="sxs-lookup"><span data-stu-id="ffb2e-119">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../concepts/package-versioning.md#version-ranges).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="ffb2e-120">Použití PackageReference pro projekt bez PackageReferences</span><span class="sxs-lookup"><span data-stu-id="ffb2e-120">Using PackageReference for a project with no PackageReferences</span></span>

<span data-ttu-id="ffb2e-121">Upřesnit: Pokud nemáte v projektu nainstalované žádné balíčky (žádné PackageReferences v souboru projektu a žádný soubor packages.config), ale chcete, aby se projekt obnovil jako PackageReferenceový styl, můžete v souboru projektu nastavit RestoreProjectStyle vlastností projektu na PackageReference.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-121">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="ffb2e-122">To může být užitečné, pokud odkazujete na projekty, které jsou PackageReference styly (existující projekty csproj nebo sady SDK).</span><span class="sxs-lookup"><span data-stu-id="ffb2e-122">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="ffb2e-123">Tím umožníte, aby balíčky, na které tyto projekty odkazují, byly "transitně" odkazovány vaším projektem.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-123">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="packagereference-and-sources"></a><span data-ttu-id="ffb2e-124">PackageReference a zdroje</span><span class="sxs-lookup"><span data-stu-id="ffb2e-124">PackageReference and sources</span></span>

<span data-ttu-id="ffb2e-125">V projektech PackageReference se v době obnovení vyřeší verze přenosných závislostí.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-125">In PackageReference projects, the transitive dependency versions are resolved at restore time.</span></span> <span data-ttu-id="ffb2e-126">V takovém případě musí být v projektech PackageReference k dispozici všechny zdroje pro všechna obnovení.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-126">As such, in PackageReference projects all sources need to be available for all restores.</span></span> 

## <a name="floating-versions"></a><span data-ttu-id="ffb2e-127">Plovoucí verze</span><span class="sxs-lookup"><span data-stu-id="ffb2e-127">Floating Versions</span></span>

<span data-ttu-id="ffb2e-128">[Plovoucí verze](../concepts/dependency-resolution.md#floating-versions) jsou podporované pomocí `PackageReference` :</span><span class="sxs-lookup"><span data-stu-id="ffb2e-128">[Floating versions](../concepts/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="ffb2e-129">Řízení prostředků závislosti</span><span class="sxs-lookup"><span data-stu-id="ffb2e-129">Controlling dependency assets</span></span>

<span data-ttu-id="ffb2e-130">Je možné, že použijete závislost čistě jako ve vývojovém prostředí a nechcete ji vystavit pro projekty, které budou spotřebovávat váš balíček.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-130">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="ffb2e-131">V tomto scénáři můžete `PrivateAssets` k řízení tohoto chování použít metadata.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-131">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="ffb2e-132">Následující Tagy metadat řídí prostředky závislostí:</span><span class="sxs-lookup"><span data-stu-id="ffb2e-132">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="ffb2e-133">Značka</span><span class="sxs-lookup"><span data-stu-id="ffb2e-133">Tag</span></span> | <span data-ttu-id="ffb2e-134">Description</span><span class="sxs-lookup"><span data-stu-id="ffb2e-134">Description</span></span> | <span data-ttu-id="ffb2e-135">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="ffb2e-135">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ffb2e-136">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="ffb2e-136">IncludeAssets</span></span> | <span data-ttu-id="ffb2e-137">Tyto prostředky budou spotřebovány.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-137">These assets will be consumed</span></span> | <span data-ttu-id="ffb2e-138">Vše</span><span class="sxs-lookup"><span data-stu-id="ffb2e-138">all</span></span> |
| <span data-ttu-id="ffb2e-139">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="ffb2e-139">ExcludeAssets</span></span> | <span data-ttu-id="ffb2e-140">Tyto prostředky nebudou spotřebovány.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-140">These assets will not be consumed</span></span> | <span data-ttu-id="ffb2e-141">žádné</span><span class="sxs-lookup"><span data-stu-id="ffb2e-141">none</span></span> |
| <span data-ttu-id="ffb2e-142">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="ffb2e-142">PrivateAssets</span></span> | <span data-ttu-id="ffb2e-143">Tyto prostředky budou spotřebovány, ale nebudou se přesměrovat do nadřazeného projektu.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-143">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="ffb2e-144">contentFiles; analyzátory; sestavit</span><span class="sxs-lookup"><span data-stu-id="ffb2e-144">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="ffb2e-145">Přípustné hodnoty pro tyto značky jsou následující, s více hodnotami oddělenými středníkem s výjimkou `all` a, `none` které se musí objevit sami:</span><span class="sxs-lookup"><span data-stu-id="ffb2e-145">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="ffb2e-146">Hodnota</span><span class="sxs-lookup"><span data-stu-id="ffb2e-146">Value</span></span> | <span data-ttu-id="ffb2e-147">Popis</span><span class="sxs-lookup"><span data-stu-id="ffb2e-147">Description</span></span> |
| --- | ---
| <span data-ttu-id="ffb2e-148">kompilovat</span><span class="sxs-lookup"><span data-stu-id="ffb2e-148">compile</span></span> | <span data-ttu-id="ffb2e-149">Obsah `lib` složky a určuje, zda je projekt kompilován proti sestavením v rámci složky</span><span class="sxs-lookup"><span data-stu-id="ffb2e-149">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="ffb2e-150">modul runtime</span><span class="sxs-lookup"><span data-stu-id="ffb2e-150">runtime</span></span> | <span data-ttu-id="ffb2e-151">Obsah `lib` `runtimes` složky a určuje, zda budou tato sestavení zkopírována do výstupního adresáře sestavení</span><span class="sxs-lookup"><span data-stu-id="ffb2e-151">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="ffb2e-152">contentFiles</span><span class="sxs-lookup"><span data-stu-id="ffb2e-152">contentFiles</span></span> | <span data-ttu-id="ffb2e-153">Obsah `contentfiles` složky</span><span class="sxs-lookup"><span data-stu-id="ffb2e-153">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="ffb2e-154">sestavení</span><span class="sxs-lookup"><span data-stu-id="ffb2e-154">build</span></span> | <span data-ttu-id="ffb2e-155">`.props` a `.targets` ve `build` složce</span><span class="sxs-lookup"><span data-stu-id="ffb2e-155">`.props` and `.targets` in the `build` folder</span></span> |
| <span data-ttu-id="ffb2e-156">buildMultitargeting</span><span class="sxs-lookup"><span data-stu-id="ffb2e-156">buildMultitargeting</span></span> | <span data-ttu-id="ffb2e-157">*(4,0)* `.props` a `.targets` ve `buildMultitargeting` složce pro cílení na různé architektury</span><span class="sxs-lookup"><span data-stu-id="ffb2e-157">*(4.0)* `.props` and `.targets` in the `buildMultitargeting` folder, for cross-framework targeting</span></span> |
| <span data-ttu-id="ffb2e-158">buildTransitive</span><span class="sxs-lookup"><span data-stu-id="ffb2e-158">buildTransitive</span></span> | <span data-ttu-id="ffb2e-159">*(5.0 +)* `.props` a `.targets` ve `buildTransitive` složce pro prostředky, jejichž přenos do libovolného náročného projektu se protéká.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-159">*(5.0+)* `.props` and `.targets` in the `buildTransitive` folder, for assets that flow transitively to any consuming project.</span></span> <span data-ttu-id="ffb2e-160">Podívejte se na stránku [funkce](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) .</span><span class="sxs-lookup"><span data-stu-id="ffb2e-160">See the [feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) page.</span></span> |
| <span data-ttu-id="ffb2e-161">analyzátory</span><span class="sxs-lookup"><span data-stu-id="ffb2e-161">analyzers</span></span> | <span data-ttu-id="ffb2e-162">Analyzátory .NET</span><span class="sxs-lookup"><span data-stu-id="ffb2e-162">.NET analyzers</span></span> |
| <span data-ttu-id="ffb2e-163">nativní</span><span class="sxs-lookup"><span data-stu-id="ffb2e-163">native</span></span> | <span data-ttu-id="ffb2e-164">Obsah `native` složky</span><span class="sxs-lookup"><span data-stu-id="ffb2e-164">Contents of the `native` folder</span></span> |
| <span data-ttu-id="ffb2e-165">žádné</span><span class="sxs-lookup"><span data-stu-id="ffb2e-165">none</span></span> | <span data-ttu-id="ffb2e-166">Žádná z výše uvedených verzí se nepoužívá.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-166">None of the above are used.</span></span> |
| <span data-ttu-id="ffb2e-167">Vše</span><span class="sxs-lookup"><span data-stu-id="ffb2e-167">all</span></span> | <span data-ttu-id="ffb2e-168">Všechny výše uvedené (kromě `none` )</span><span class="sxs-lookup"><span data-stu-id="ffb2e-168">All of the above (except `none`)</span></span> |

<span data-ttu-id="ffb2e-169">V následujícím příkladu je vše kromě souborů obsahu z balíčku spotřebováno projektem a vše kromě souborů obsahu a analyzátory by vedlo k nadřazenému projektu.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-169">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <IncludeAssets>all</IncludeAssets>
        <ExcludeAssets>contentFiles</ExcludeAssets>
        <PrivateAssets>contentFiles;analyzers</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="ffb2e-170">Všimněte si, že protože `build` není součástí `PrivateAssets` , cíle a props *budou* tok do nadřazeného projektu.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-170">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="ffb2e-171">Vezměte v úvahu například, že odkaz výše se používá v projektu, který vytváří balíček NuGet s názvem AppLogger.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-171">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="ffb2e-172">AppLogger může využívat cíle a props z `Contoso.Utility.UsefulStuff` , jako mohou projekty, které využívají AppLogger.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-172">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

> [!NOTE]
> <span data-ttu-id="ffb2e-173">Když `developmentDependency` je v souboru nastavená na `true` `.nuspec` , označí balíček jako součást jedinou pro vývoj, která zabrání zahrnutí balíčku jako závislosti v jiných balíčcích.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-173">When `developmentDependency` is set to `true` in a `.nuspec` file, this marks a package as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="ffb2e-174">Pomocí PackageReference *(NuGet 4,8 +)* tento příznak také znamená, že vyloučí prostředky při kompilaci z kompilace.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-174">With PackageReference *(NuGet 4.8+)*, this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="ffb2e-175">Další informace najdete v tématu [Podpora DevelopmentDependency pro PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span><span class="sxs-lookup"><span data-stu-id="ffb2e-175">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="ffb2e-176">Přidání podmínky PackageReference</span><span class="sxs-lookup"><span data-stu-id="ffb2e-176">Adding a PackageReference condition</span></span>

<span data-ttu-id="ffb2e-177">Podmínku můžete použít k určení, zda je balíček zahrnut, kde podmínky mohou používat jakoukoli proměnnou MSBuild nebo proměnnou definovanou v souboru TARGETS nebo props.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-177">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="ffb2e-178">V předsoučasném případě je však podporována pouze `TargetFramework` Proměnná.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-178">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="ffb2e-179">Řekněme například, že cílíte `netstandard1.4` i na `net452` , ale máte závislost, která je platná pouze pro `net452` .</span><span class="sxs-lookup"><span data-stu-id="ffb2e-179">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="ffb2e-180">V takovém případě nechcete, aby `netstandard1.4` projekt, který váš balíček spotřebovává, přidal tuto nepotřebnou závislost.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-180">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="ffb2e-181">Tomu zabráníte tak, že zadáte podmínku v následujícím `PackageReference` příkladu:</span><span class="sxs-lookup"><span data-stu-id="ffb2e-181">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="ffb2e-182">Balíček sestavený pomocí tohoto projektu zobrazí, že Newtonsoft.Jsv je součástí pouze závislosti pro `net452` cíl:</span><span class="sxs-lookup"><span data-stu-id="ffb2e-182">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![Výsledek použití podmínky v PackageReference s VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="ffb2e-184">Podmínky lze také použít na `ItemGroup` úrovni a budou platit pro všechny podřízené `PackageReference` prvky:</span><span class="sxs-lookup"><span data-stu-id="ffb2e-184">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="generatepathproperty"></a><span data-ttu-id="ffb2e-185">GeneratePathProperty</span><span class="sxs-lookup"><span data-stu-id="ffb2e-185">GeneratePathProperty</span></span>

<span data-ttu-id="ffb2e-186">Tato funkce je k dispozici pro NuGet **5,0** nebo vyšší a pro Visual Studio 2019 **16,0** nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-186">This feature is available with NuGet **5.0** or above and with Visual Studio 2019 **16.0** or above.</span></span>

<span data-ttu-id="ffb2e-187">V některých případech je žádoucí, aby odkazovaly na soubory v balíčku z cíle MSBuild.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-187">Sometimes it is desirable to reference files in a package from an MSBuild target.</span></span>
<span data-ttu-id="ffb2e-188">V `packages.config` projektech založených na projektech jsou balíčky nainstalovány ve složce relativní vzhledem k souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-188">In `packages.config` based projects, the packages are installed in a folder relative to the project file.</span></span> <span data-ttu-id="ffb2e-189">V PackageReference jsou však balíčky [spotřebovány](../concepts/package-installation-process.md) ze složky *Global-Packages* , která se může lišit v závislosti na počítači.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-189">However in PackageReference, the packages are [consumed](../concepts/package-installation-process.md) from the *global-packages* folder, which can vary from machine to machine.</span></span>

<span data-ttu-id="ffb2e-190">Za účelem přemostění NuGet představila vlastnost, která odkazuje na umístění, ze kterého se balíček spotřebuje.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-190">To bridge that gap, NuGet introduced a property that points to the location from which the package will be consumed.</span></span>

<span data-ttu-id="ffb2e-191">Příklad:</span><span class="sxs-lookup"><span data-stu-id="ffb2e-191">Example:</span></span>

```xml
  <ItemGroup>
      <PackageReference Include="Some.Package" Version="1.0.0" GeneratePathProperty="true" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgSome_Package)\something.exe" />
  </Target>
````

<span data-ttu-id="ffb2e-192">Kromě toho NuGet automaticky vygeneruje vlastnosti pro balíčky obsahující složku Tools.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-192">Additionally NuGet will automatically generate properties for packages containing a tools folder.</span></span>

```xml
  <ItemGroup>
      <PackageReference Include="Package.With.Tools" Version="1.0.0" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgPackage_With_Tools)\tools\tool.exe" />
  </Target>
```

<span data-ttu-id="ffb2e-193">Vlastnosti nástroje MSBuild a identity balíčku nemají stejná omezení, takže Identita balíčku musí být změněna na popisný název MSBuild, který je opraven slovem `Pkg` .</span><span class="sxs-lookup"><span data-stu-id="ffb2e-193">MSBuild properties and package identities do not have the same restrictions so the package identity needs to be changed to an MSBuild friendly name, prefixed by the word `Pkg`.</span></span>
<span data-ttu-id="ffb2e-194">Chcete-li ověřit přesný název generované vlastnosti, podívejte se do vygenerovaného souboru [NuGet. g. props](../reference/msbuild-targets.md#restore-outputs) .</span><span class="sxs-lookup"><span data-stu-id="ffb2e-194">To verify the exact name of the property generated, look at the generated [nuget.g.props](../reference/msbuild-targets.md#restore-outputs) file.</span></span>

## <a name="packagereference-aliases"></a><span data-ttu-id="ffb2e-195">PackageReference aliasy</span><span class="sxs-lookup"><span data-stu-id="ffb2e-195">PackageReference Aliases</span></span>

<span data-ttu-id="ffb2e-196">V některých vzácných instancích budou různé balíčky obsahovat třídy ve stejném oboru názvů.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-196">In some rare instances different packages will contain classes in the same namespace.</span></span> <span data-ttu-id="ffb2e-197">Počínaje verzí NuGet 5,7 & Visual Studio 2019 Update 7, který je ekvivalentní s ProjectReference, PackageReference podporuje [`Aliases`](/dotnet/api/microsoft.codeanalysis.projectreference.aliases) .</span><span class="sxs-lookup"><span data-stu-id="ffb2e-197">Starting with NuGet 5.7 & Visual Studio 2019 Update 7, equivalent to ProjectReference, PackageReference supports [`Aliases`](/dotnet/api/microsoft.codeanalysis.projectreference.aliases).</span></span>
<span data-ttu-id="ffb2e-198">Ve výchozím nastavení nejsou k dispozici žádné aliasy.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-198">By default no aliases are provided.</span></span> <span data-ttu-id="ffb2e-199">Když je zadán alias, *všechna* sestavení pocházející z balíčku s poznámkami musí být odkazována aliasem.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-199">When an alias is specified, *all* assemblies coming from the annotated package with need to be referenced with an alias.</span></span>

<span data-ttu-id="ffb2e-200">Můžete se podívat na ukázkové použití na [NuGet\Samples](https://github.com/NuGet/Samples/tree/main/PackageReferenceAliasesExample)</span><span class="sxs-lookup"><span data-stu-id="ffb2e-200">You can look at sample usage at [NuGet\Samples](https://github.com/NuGet/Samples/tree/main/PackageReferenceAliasesExample)</span></span>

<span data-ttu-id="ffb2e-201">V souboru projektu zadejte aliasy následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="ffb2e-201">In the project file, specify the aliases as follows:</span></span>

```xml
  <ItemGroup>
    <PackageReference Include="NuGet.Versioning" Version="5.8.0" Aliases="ExampleAlias" />
  </ItemGroup>
```

<span data-ttu-id="ffb2e-202">a v kódu ho použijte následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="ffb2e-202">and in the code use it as follows:</span></span>

```cs
extern alias ExampleAlias;

namespace PackageReferenceAliasesExample
{
...
        {
            var version = ExampleAlias.NuGet.Versioning.NuGetVersion.Parse("5.0.0");
            Console.WriteLine($"Version : {version}");
        }
...
}

```

## <a name="nuget-warnings-and-errors"></a><span data-ttu-id="ffb2e-203">Upozornění a chyby NuGetu</span><span class="sxs-lookup"><span data-stu-id="ffb2e-203">NuGet warnings and errors</span></span>

<span data-ttu-id="ffb2e-204">*Tato funkce je dostupná pro NuGet **4.3** nebo vyšší a s Visual Studio 2017 **15.3** nebo vyšší.*</span><span class="sxs-lookup"><span data-stu-id="ffb2e-204">*This feature is available with NuGet **4.3** or above and with Visual Studio 2017 **15.3** or above.*</span></span>

<span data-ttu-id="ffb2e-205">V mnoha scénářích balíčků a obnovení se všechna upozornění a chyby NuGet kódují a začínají na `NU****` .</span><span class="sxs-lookup"><span data-stu-id="ffb2e-205">For many pack and restore scenarios, all NuGet warnings and errors are coded, and start with `NU****`.</span></span> <span data-ttu-id="ffb2e-206">Všechna upozornění a chyby NuGetu jsou uvedená v [referenční](../reference/errors-and-warnings.md) dokumentaci.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-206">All NuGet warnings and errors are listed in the [reference](../reference/errors-and-warnings.md) documentation.</span></span>

<span data-ttu-id="ffb2e-207">NuGet pozoruje následující vlastnosti upozornění:</span><span class="sxs-lookup"><span data-stu-id="ffb2e-207">NuGet observes the following warning properties:</span></span>

- <span data-ttu-id="ffb2e-208">`TreatWarningsAsErrors`– zachází se všemi upozorněními jako s chybami</span><span class="sxs-lookup"><span data-stu-id="ffb2e-208">`TreatWarningsAsErrors`, treat all warnings as errors</span></span>
- <span data-ttu-id="ffb2e-209">`WarningsAsErrors`– zacházení s konkrétními upozorněními jako s chybami</span><span class="sxs-lookup"><span data-stu-id="ffb2e-209">`WarningsAsErrors`, treat specific warnings as errors</span></span>
- <span data-ttu-id="ffb2e-210">`NoWarn`– skryje konkrétní upozornění, ať už celého projektu, nebo celého balíčku.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-210">`NoWarn`, hide specific warnings, either project-wide or package-wide.</span></span>

<span data-ttu-id="ffb2e-211">Příklady:</span><span class="sxs-lookup"><span data-stu-id="ffb2e-211">Examples:</span></span>

```xml
<PropertyGroup>
    <TreatWarningsAsErrors>true</TreatWarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <WarningsAsErrors>$(WarningsAsErrors);NU1603;NU1605</WarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <NoWarn>$(NoWarn);NU5124</NoWarn>
</PropertyGroup>
...
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0" NoWarn="NU1605" />
</ItemGroup>
```

### <a name="suppressing-nuget-warnings"></a><span data-ttu-id="ffb2e-212">Potlačení upozornění NuGetu</span><span class="sxs-lookup"><span data-stu-id="ffb2e-212">Suppressing NuGet warnings</span></span>

<span data-ttu-id="ffb2e-213">Přestože se doporučuje vyřešit všechna upozornění NuGetu během operací balíčku a obnovení, v určitých situacích je jejich potlačení zaručuje.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-213">While it is recommended that you resolve all NuGet warnings during your pack and restore operations, in certain situations suppressing them is warranted.</span></span>
<span data-ttu-id="ffb2e-214">Pokud chcete potlačit projekt upozornění v celém projektu, zvažte následující:</span><span class="sxs-lookup"><span data-stu-id="ffb2e-214">To suppress a warning project wide, consider doing:</span></span>

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
    <NoWarn>$(NoWarn);NU5104</NoWarn>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1"/>
</ItemGroup>
```

<span data-ttu-id="ffb2e-215">Někdy se upozornění vztahují pouze na určitý balíček v grafu.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-215">Sometimes warnings apply only to a certain package in the graph.</span></span> <span data-ttu-id="ffb2e-216">Můžeme se rozhodnout toto upozornění potlačit selektivně tak, že do `NoWarn` položky PackageReference přidáme .</span><span class="sxs-lookup"><span data-stu-id="ffb2e-216">We can choose to suppress that warning more selectively by adding a `NoWarn` on the PackageReference item.</span></span> 

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1" NoWarn="NU1603" />
</ItemGroup>
```

#### <a name="suppressing-nuget-package-warnings-in-visual-studio"></a><span data-ttu-id="ffb2e-217">Potlačení upozornění balíčku NuGet v Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ffb2e-217">Suppressing NuGet package warnings in Visual Studio</span></span>

<span data-ttu-id="ffb2e-218">V Visual Studio můžete také potlačit [upozornění prostřednictvím](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) integrovaného vývojového prostředí.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-218">When in Visual Studio, you can also [suppress warnings](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) through the IDE.</span></span>

## <a name="locking-dependencies"></a><span data-ttu-id="ffb2e-219">Zamykání závislostí</span><span class="sxs-lookup"><span data-stu-id="ffb2e-219">Locking dependencies</span></span>

<span data-ttu-id="ffb2e-220">*Tato funkce je dostupná pro NuGet **4.9** nebo vyšší a s Visual Studio 2017 **15.9** nebo vyšší.*</span><span class="sxs-lookup"><span data-stu-id="ffb2e-220">*This feature is available with NuGet **4.9** or above and with Visual Studio 2017 **15.9** or above.*</span></span>

<span data-ttu-id="ffb2e-221">Vstup pro obnovení NuGetu je sada odkazů na balíčky ze souboru projektu (hlavní úroveň nebo přímé závislosti) a výstupem je úplné uzavření všech závislostí balíčku, včetně tranzitivních závislostí.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-221">Input to NuGet restore is a set of Package References from the project file (top-level or direct dependencies) and the output is a full closure of all the package dependencies including transitive dependencies.</span></span> <span data-ttu-id="ffb2e-222">NuGet se pokusí vždy vytvořit stejné úplné uzavření závislostí balíčku, pokud se vstupní seznam PackageReference nezměnil.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-222">NuGet tries to always produce the same full closure of package dependencies if the input PackageReference list has not changed.</span></span> <span data-ttu-id="ffb2e-223">Existují však některé scénáře, kdy to nemůže udělat.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-223">However, there are some scenarios where it is unable to do so.</span></span> <span data-ttu-id="ffb2e-224">Příklad:</span><span class="sxs-lookup"><span data-stu-id="ffb2e-224">For example:</span></span>

* <span data-ttu-id="ffb2e-225">Při použití plovoucích verzí, jako je `<PackageReference Include="My.Sample.Lib" Version="4.*"/>` .</span><span class="sxs-lookup"><span data-stu-id="ffb2e-225">When you use floating versions like `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span></span> <span data-ttu-id="ffb2e-226">I když se zde záměrem při každém obnovení balíčků vrátit na nejnovější verzi, existují scénáře, kdy uživatelé vyžadují, aby byl graf uzamčený na určitou nejnovější verzi, a s plovoucí desetinnou čárkou na novější verzi, pokud je k dispozici, při explicitním gestu.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-226">While the intention here is to float to the latest version on every restore of packages, there are scenarios where users require the graph to be locked to a certain latest version and float to a later version, if available, upon an explicit gesture.</span></span>
* <span data-ttu-id="ffb2e-227">Publikovaná je novější verze balíčku, která odpovídá požadavkům na verzi PackageReference.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-227">A newer version of the package matching PackageReference version requirements is published.</span></span> <span data-ttu-id="ffb2e-228">Například</span><span class="sxs-lookup"><span data-stu-id="ffb2e-228">E.g.</span></span> 

  * <span data-ttu-id="ffb2e-229">Den 1: Pokud jste zadali , ale verze dostupné v úložištích NuGet byly `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` 4.1.0, 4.2.0 a 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-229">Day 1: if you specified `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` but the versions available on the NuGet repositories were 4.1.0, 4.2.0 and 4.3.0.</span></span> <span data-ttu-id="ffb2e-230">V tomto případě by se NuGet vyřešil na verzi 4.1.0 (nejbližší minimální verze).</span><span class="sxs-lookup"><span data-stu-id="ffb2e-230">In this case, NuGet would have resolved to  4.1.0 (nearest minimum version)</span></span>

  * <span data-ttu-id="ffb2e-231">2. den: Publikovaná verze 4.0.0.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-231">Day 2: Version 4.0.0 gets published.</span></span> <span data-ttu-id="ffb2e-232">NuGet teď najde přesnou shodu a začne se překládání na verzi 4.0.0.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-232">NuGet will now find the exact match and start resolving to 4.0.0</span></span>

* <span data-ttu-id="ffb2e-233">Z úložiště se odebere given package version (verze balíčku).</span><span class="sxs-lookup"><span data-stu-id="ffb2e-233">A given package version is removed from the repository.</span></span> <span data-ttu-id="ffb2e-234">Přestože nuget.org odstranění balíčků nepovoluje, ne všechna úložiště balíčků mají tato omezení.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-234">Though nuget.org does not allow package deletions, not all package repositories have this constraints.</span></span> <span data-ttu-id="ffb2e-235">Výsledkem je, že NuGet najde nejlepší shodu, když se nemůže přeložit na odstraněnou verzi.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-235">This results in NuGet finding the best match when it cannot resolve to the deleted version.</span></span>

### <a name="enabling-lock-file"></a><span data-ttu-id="ffb2e-236">Povolení souboru zámku</span><span class="sxs-lookup"><span data-stu-id="ffb2e-236">Enabling lock file</span></span>

<span data-ttu-id="ffb2e-237">Pokud chcete zachovat úplné uzavření závislostí balíčků, můžete se přihlásit k funkci souboru zámku nastavením vlastnosti MSBuild `RestorePackagesWithLockFile` pro váš projekt:</span><span class="sxs-lookup"><span data-stu-id="ffb2e-237">In order to persist the full closure of package dependencies you can opt-in to the lock file feature by setting the MSBuild property `RestorePackagesWithLockFile` for your project:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="ffb2e-238">Pokud je tato vlastnost nastavená, obnovení NuGet vygeneruje soubor zámku – soubor v kořenovém adresáři projektu se `packages.lock.json` seznamem všech závislostí balíčku.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-238">If this property is set, NuGet restore will generate a lock file - `packages.lock.json` file at the project root directory that lists all the package dependencies.</span></span> 

> [!Note]
> <span data-ttu-id="ffb2e-239">Jakmile projekt obsahuje soubor v kořenovém adresáři, soubor zámku se vždy používá s obnovením, i když `packages.lock.json` vlastnost `RestorePackagesWithLockFile` není nastavená.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-239">Once a project has `packages.lock.json` file in its root directory, the lock file is always used with restore even if the property `RestorePackagesWithLockFile` is not set.</span></span> <span data-ttu-id="ffb2e-240">Dalším způsobem, jak se k této funkci přihlásit, je vytvořit fiktivní prázdný soubor v kořenovém adresáři `packages.lock.json` projektu.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-240">So another way to opt-in to this feature is to create a dummy blank `packages.lock.json` file in the project's root directory.</span></span>

### <a name="restore-behavior-with-lock-file"></a><span data-ttu-id="ffb2e-241">`restore` chování se zamykacím souborem</span><span class="sxs-lookup"><span data-stu-id="ffb2e-241">`restore` behavior with lock file</span></span>
<span data-ttu-id="ffb2e-242">Pokud je pro projekt k dispozici soubor zámku, NuGet použije tento soubor zámku ke spuštění `restore` .</span><span class="sxs-lookup"><span data-stu-id="ffb2e-242">If a lock file is present for project, NuGet uses this lock file to run `restore`.</span></span> <span data-ttu-id="ffb2e-243">NuGet rychle zkontroluje, jestli v závislostech balíčků došlo k žádným změnám, jak je uvedeno v souboru projektu (nebo v souborech závislých projektů), a pokud k žádným změnám došlo, pouze obnoví balíčky uvedené v souboru zámku.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-243">NuGet does a quick check to see if there were any changes in the package dependencies as mentioned in the project file (or dependent projects' files) and if there were no changes it just restores the packages mentioned in the lock file.</span></span> <span data-ttu-id="ffb2e-244">Neexistuje žádné opětovné vyhodnocení závislostí balíčků.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-244">There is no re-evaluation of package dependencies.</span></span>

<span data-ttu-id="ffb2e-245">Pokud NuGet zjistí změnu v definovaných závislostech, jak je uvedeno v souborech projektu, znovu vyhodnotí graf balíčku a aktualizuje soubor zámku tak, aby odrážel nový uzavření balíčku pro projekt.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-245">If NuGet detects a change in the defined dependencies as mentioned in the project file(s), it re-evaluates the package graph and updates the lock file to reflect the new package closure for the project.</span></span>

<span data-ttu-id="ffb2e-246">V případě CI/CD a dalších scénářů, kdy nechcete měnit závislosti balíčku za běhu, můžete to provést nastavením `lockedmode` na `true` :</span><span class="sxs-lookup"><span data-stu-id="ffb2e-246">For CI/CD and other scenarios, where you would not want to change the package dependencies on the fly, you can do so by setting the `lockedmode` to `true`:</span></span>

<span data-ttu-id="ffb2e-247">Pokud dotnet.exe, spusťte:</span><span class="sxs-lookup"><span data-stu-id="ffb2e-247">For dotnet.exe, run:</span></span>

```
> dotnet.exe restore --locked-mode
```

<span data-ttu-id="ffb2e-248">Pokud msbuild.exe, spusťte:</span><span class="sxs-lookup"><span data-stu-id="ffb2e-248">For msbuild.exe, run:</span></span>

```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

<span data-ttu-id="ffb2e-249">Tuto podmíněnou vlastnost MSBuild můžete nastavit také v souboru projektu:</span><span class="sxs-lookup"><span data-stu-id="ffb2e-249">You may also set this conditional MSBuild property in your project file:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

<span data-ttu-id="ffb2e-250">Pokud je uzamčený režim , obnovení buď obnoví přesné balíčky uvedené v souboru zámku, nebo selže, pokud jste po vytvoření souboru zámku aktualizovali definované `true` závislosti balíčku pro projekt.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-250">If locked mode is `true`, restore will either restore the exact packages as listed in the lock file or fail if you updated the defined package dependencies for the project after lock file was created.</span></span>

### <a name="make-lock-file-part-of-your-source-repository"></a><span data-ttu-id="ffb2e-251">Zmknutí souboru jako součásti zdrojového úložiště</span><span class="sxs-lookup"><span data-stu-id="ffb2e-251">Make lock file part of your source repository</span></span>
<span data-ttu-id="ffb2e-252">Pokud aplikaci tvoříte, spustitelný soubor a na začátku řetězu závislostí se nachází sporý projekt, zkontrolujte soubor zámku v úložišti zdrojového kódu, aby ho NuGet mohl využít během obnovení.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-252">If you are building an application, an executable and the project in question is at the start of the dependency chain then do check in the lock file to the source code repository so that NuGet can make use of it during restore.</span></span>

<span data-ttu-id="ffb2e-253">Pokud je ale váš projekt projekt knihovny, který dodáte, nebo společný  projekt kódu, na kterém závisí jiné projekty, neměli byste se v rámci zdrojového kódu účastnit souboru zámku.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-253">However, if your project is a library project that you do not ship or a common code project on which other projects depend upon, you **should not** check in the lock file as part of your source code.</span></span> <span data-ttu-id="ffb2e-254">Zachování souboru zámku není škodou, ale během obnovování/sestavování projektu, který závisí na tomto projektu společného kódu, se nemusí použít závislosti uzamčeného balíčku pro společný projekt kódu, jak je uvedeno v souboru zámku.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-254">There is no harm in keeping the lock file but the locked package dependencies for the common code project may not be used, as listed in the lock file, during the restore/build of a project that depends on this common-code project.</span></span>

<span data-ttu-id="ffb2e-255">Např.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-255">Eg.</span></span>

```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```

<span data-ttu-id="ffb2e-256">Pokud má závislost na verzi a také odkazuje na verzi , pak soubor zámku pro zobrazí závislost `ProjectA` `PackageX` na verzi `2.0.0` `ProjectB` `PackageX` `1.0.0` `ProjectB` `PackageX` `1.0.0` .</span><span class="sxs-lookup"><span data-stu-id="ffb2e-256">If `ProjectA` has a dependency on a `PackageX` version `2.0.0` and also references `ProjectB` that depends on `PackageX` version `1.0.0`, then the lock file for `ProjectB` will list a dependency on `PackageX` version `1.0.0`.</span></span> <span data-ttu-id="ffb2e-257">Pokud je však sestaven, bude jeho soubor zámku obsahovat závislost na verzi, a ne tak, jak je uvedeno v `ProjectA` `PackageX` souboru zámku pro **`2.0.0`**  `1.0.0` `ProjectB` .</span><span class="sxs-lookup"><span data-stu-id="ffb2e-257">However, when `ProjectA` is built, its lock file will contain a dependency on `PackageX` version **`2.0.0`** and **not** `1.0.0` as listed in the lock file for `ProjectB`.</span></span> <span data-ttu-id="ffb2e-258">Proto má soubor zámků společného projektu kódu nad balíčky vyřešené pro projekty, které na tomto projektu závisejí, jen malé říci.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-258">Thus, the lock file of a common code project has little say over the packages resolved for projects that depend on it.</span></span>

### <a name="lock-file-extensibility"></a><span data-ttu-id="ffb2e-259">Rozšiřitelnost souboru zámků</span><span class="sxs-lookup"><span data-stu-id="ffb2e-259">Lock file extensibility</span></span>

<span data-ttu-id="ffb2e-260">Pomocí souboru zámku můžete řídit různé chování obnovení, jak je popsáno níže:</span><span class="sxs-lookup"><span data-stu-id="ffb2e-260">You can control various behaviors of restore with lock file as described below:</span></span>

| <span data-ttu-id="ffb2e-261">NuGet.exe možnosti</span><span class="sxs-lookup"><span data-stu-id="ffb2e-261">NuGet.exe option</span></span> | <span data-ttu-id="ffb2e-262">možnost dotnet</span><span class="sxs-lookup"><span data-stu-id="ffb2e-262">dotnet option</span></span> | <span data-ttu-id="ffb2e-263">Ekvivalentní možnost nástroje MSBuild</span><span class="sxs-lookup"><span data-stu-id="ffb2e-263">MSBuild equivalent option</span></span> | <span data-ttu-id="ffb2e-264">Description</span><span class="sxs-lookup"><span data-stu-id="ffb2e-264">Description</span></span> |
|:--- |:--- |:--- |:--- |
| `-UseLockFile` |`--use-lock-file` | <span data-ttu-id="ffb2e-265">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="ffb2e-265">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="ffb2e-266">Vyjádí výslovný souhlas s použitím souboru zámku.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-266">Opts into the usage of a lock file.</span></span> |
| `-LockedMode` | `--locked-mode` | <span data-ttu-id="ffb2e-267">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="ffb2e-267">RestoreLockedMode</span></span> | <span data-ttu-id="ffb2e-268">Povolí uzamčený režim obnovení.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-268">Enables locked mode for restore.</span></span> <span data-ttu-id="ffb2e-269">To je užitečné ve scénářích CI/CD, kde chcete opakovatelná sestavení.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-269">This is useful in CI/CD scenarios where you want repeatable builds.</span></span>|   
| `-ForceEvaluate` | `--force-evaluate` | <span data-ttu-id="ffb2e-270">RestoreForceEvaluate</span><span class="sxs-lookup"><span data-stu-id="ffb2e-270">RestoreForceEvaluate</span></span> | <span data-ttu-id="ffb2e-271">Tato možnost je užitečná u balíčků s plovoucí verzí definovanou v projektu.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-271">This option is useful with packages with floating version defined in the project.</span></span> <span data-ttu-id="ffb2e-272">Obnovení NuGet ve výchozím nastavení při každém obnovení automaticky aktualizuje verzi balíčku, pokud s touto možností nespouštěte obnovení.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-272">By default, NuGet restore will not update the package version automatically upon each restore unless you run restore with this option.</span></span> |
| `-LockFilePath` | `--lock-file-path` | <span data-ttu-id="ffb2e-273">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="ffb2e-273">NuGetLockFilePath</span></span> | <span data-ttu-id="ffb2e-274">Definuje vlastní umístění souboru zámku pro projekt.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-274">Defines a custom lock file location for a project.</span></span> <span data-ttu-id="ffb2e-275">NuGet ve výchozím nastavení podporuje `packages.lock.json` v kořenovém adresáři.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-275">By default, NuGet supports `packages.lock.json` at the root directory.</span></span> <span data-ttu-id="ffb2e-276">Pokud máte ve stejném adresáři více projektů, NuGet podporuje soubor zámku specifický pro projekt. `packages.<project_name>.lock.json`</span><span class="sxs-lookup"><span data-stu-id="ffb2e-276">If you have multiple projects in the same directory, NuGet supports project specific lock file `packages.<project_name>.lock.json`</span></span> |

## <a name="assettargetfallback"></a><span data-ttu-id="ffb2e-277">AssetTargetFallback</span><span class="sxs-lookup"><span data-stu-id="ffb2e-277">AssetTargetFallback</span></span>

<span data-ttu-id="ffb2e-278">Vlastnost umožňuje zadat další kompatibilní verze architektury pro projekty, na které projekt odkazuje, a balíčky `AssetTargetFallback` NuGet, které váš projekt využívá.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-278">The `AssetTargetFallback` property lets you specify additional compatible framework versions for projects that your project references and NuGet packages that your project consumes.</span></span>

<span data-ttu-id="ffb2e-279">Pokud pomocí příkazu zadáte závislost balíčku, ale tento balíček neobsahuje prostředky, které jsou kompatibilní s cílovou architekturou vašich projektů, vlastnost `PackageReference` se pro vás `AssetTargetFallback` hraje.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-279">If you specify a package dependency using `PackageReference` but that package doesn't contain assets that are compatible with your projects's target framework, the `AssetTargetFallback` property comes into play.</span></span> <span data-ttu-id="ffb2e-280">Kompatibilita odkazovaného balíčku se znovu prověří pomocí každé cílové architektury, která je zadaná v `AssetTargetFallback` .</span><span class="sxs-lookup"><span data-stu-id="ffb2e-280">The compatibility of the referenced package is rechecked using each target framework that's specified in `AssetTargetFallback`.</span></span>
<span data-ttu-id="ffb2e-281">Pokud se na objekt nebo odkazuje prostřednictvím , bude vyvoláno upozornění `project` `package` `AssetTargetFallback` [NU1701.](../reference/errors-and-warnings/NU1701.md)</span><span class="sxs-lookup"><span data-stu-id="ffb2e-281">When a `project` or a `package` is referenced through `AssetTargetFallback`, the [NU1701](../reference/errors-and-warnings/NU1701.md) warning will be raised.</span></span>

<span data-ttu-id="ffb2e-282">Příklady ovlivnění kompatibility najdete `AssetTargetFallback` v následující tabulce.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-282">Refer to the table below for examples of how `AssetTargetFallback` affects compatibility.</span></span>

| <span data-ttu-id="ffb2e-283">Rozhraní projektu</span><span class="sxs-lookup"><span data-stu-id="ffb2e-283">Project framework</span></span> | <span data-ttu-id="ffb2e-284">AssetTargetFallback</span><span class="sxs-lookup"><span data-stu-id="ffb2e-284">AssetTargetFallback</span></span> | <span data-ttu-id="ffb2e-285">Architektury balíčků</span><span class="sxs-lookup"><span data-stu-id="ffb2e-285">Package frameworks</span></span> | <span data-ttu-id="ffb2e-286">Výsledek</span><span class="sxs-lookup"><span data-stu-id="ffb2e-286">Result</span></span> |
|-------------------|---------------------|--------------------|--------|
| <span data-ttu-id="ffb2e-287"> .NET Framework 4.7.2</span><span class="sxs-lookup"><span data-stu-id="ffb2e-287">.NET Framework 4.7.2</span></span> | | <span data-ttu-id="ffb2e-288">.NET Standard 2.0</span><span class="sxs-lookup"><span data-stu-id="ffb2e-288">.NET Standard 2.0</span></span> | <span data-ttu-id="ffb2e-289">.NET Standard 2.0</span><span class="sxs-lookup"><span data-stu-id="ffb2e-289">.NET Standard 2.0</span></span> |
| <span data-ttu-id="ffb2e-290">Aplikace .NET Core 3.1</span><span class="sxs-lookup"><span data-stu-id="ffb2e-290">.NET Core App 3.1</span></span> | | <span data-ttu-id="ffb2e-291">.NET Standard 2.0, .NET Framework 4.7.2</span><span class="sxs-lookup"><span data-stu-id="ffb2e-291">.NET Standard 2.0, .NET Framework 4.7.2</span></span> | <span data-ttu-id="ffb2e-292">.NET Standard 2.0</span><span class="sxs-lookup"><span data-stu-id="ffb2e-292">.NET Standard 2.0</span></span> |
| <span data-ttu-id="ffb2e-293">Aplikace .NET Core 3.1</span><span class="sxs-lookup"><span data-stu-id="ffb2e-293">.NET Core App 3.1</span></span> | | <span data-ttu-id="ffb2e-294"> .NET Framework 4.7.2</span><span class="sxs-lookup"><span data-stu-id="ffb2e-294">.NET Framework 4.7.2</span></span> | <span data-ttu-id="ffb2e-295">Nekompatibilní, selhání s [`NU1202`](../reference/errors-and-warnings/NU1202.md)</span><span class="sxs-lookup"><span data-stu-id="ffb2e-295">Incompatible, fail with [`NU1202`](../reference/errors-and-warnings/NU1202.md)</span></span> |
| <span data-ttu-id="ffb2e-296">Aplikace .NET Core 3.1</span><span class="sxs-lookup"><span data-stu-id="ffb2e-296">.NET Core App 3.1</span></span> | <span data-ttu-id="ffb2e-297">net472, net471</span><span class="sxs-lookup"><span data-stu-id="ffb2e-297">net472;net471</span></span> | <span data-ttu-id="ffb2e-298"> .NET Framework 4.7.2</span><span class="sxs-lookup"><span data-stu-id="ffb2e-298">.NET Framework 4.7.2</span></span> | <span data-ttu-id="ffb2e-299">.NET Framework 4.7.2 s [`NU1701`](../reference/errors-and-warnings/NU1701.md)</span><span class="sxs-lookup"><span data-stu-id="ffb2e-299">.NET Framework 4.7.2 with [`NU1701`](../reference/errors-and-warnings/NU1701.md)</span></span> |

<span data-ttu-id="ffb2e-300">Pomocí lze zadat více architektur `;` jako oddělovač.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-300">Multiple frameworks can be specified using `;` as a delimiter.</span></span> <span data-ttu-id="ffb2e-301">Pokud chcete přidat záložní rozhraní, můžete provést následující akce:</span><span class="sxs-lookup"><span data-stu-id="ffb2e-301">To add a fallback framework you can do the following:</span></span>

```xml
<AssetTargetFallback Condition=" '$(TargetFramework)'=='netcoreapp3.1' ">
    $(AssetTargetFallback);net472;net471
</AssetTargetFallback>
```

<span data-ttu-id="ffb2e-302">Pokud chcete přepsat místo přidávání k existujícím hodnotám, můžete toto nastavení `$(AssetTargetFallback)` `AssetTargetFallback` ponechat vypnuté.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-302">You can leave off `$(AssetTargetFallback)` if you wish to overwrite, instead of add to the existing `AssetTargetFallback` values.</span></span>

> [!NOTE]
> <span data-ttu-id="ffb2e-303">Pokud používáte projekt založený [na sadě .NET SDK,](/dotnet/core/sdk)jsou nakonfigurované odpovídající hodnoty a není nutné je `$(AssetTargetFallback)` nastavovat ručně.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-303">If you are using a [.NET SDK based project](/dotnet/core/sdk), appropriate `$(AssetTargetFallback)` values are configured and you do not need to set them manually.</span></span>
>
> <span data-ttu-id="ffb2e-304">`$(PackageTargetFallback)` byla dřívější funkce, která se pokusila tuto výzvu řešit, ale v podstatě je porušená a *neměla* by se používat.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-304">`$(PackageTargetFallback)` was an earlier feature that attempted to address this challenge, but it is fundamentally broken and *should* not be used.</span></span> <span data-ttu-id="ffb2e-305">Pokud chcete `$(PackageTargetFallback)` migrovat z `$(AssetTargetFallback)` na , stačí změnit název vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="ffb2e-305">To migrate from `$(PackageTargetFallback)` to `$(AssetTargetFallback)`, simply change the property name.</span></span>
