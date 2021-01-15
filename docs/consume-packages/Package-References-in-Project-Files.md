---
title: Formát NuGet PackageReference (odkazy na balíčky v souborech projektu)
description: Podrobnosti o NuGet PackageReference v souborech projektu, které podporuje NuGet 4.0 + a VS2017 a .NET Core 2,0
author: nkolev92
ms.author: nikolev
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: dcaed83ca54e3234702e963ffc2ebbde4cd75b28
ms.sourcegitcommit: 323a107c345c7cb4e344a6e6d8de42c63c5188b7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/15/2021
ms.locfileid: "98235760"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="fde48-103">Odkazy na balíčky (PackageReference) v souborech projektu</span><span class="sxs-lookup"><span data-stu-id="fde48-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="fde48-104">Odkazy na balíčky, použití `PackageReference` uzlu, Správa závislostí NuGet přímo v souborech projektu (na rozdíl od samostatného `packages.config` souboru).</span><span class="sxs-lookup"><span data-stu-id="fde48-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="fde48-105">Použití PackageReference, jak je voláno, nemá vliv na jiné aspekty NuGet; například nastavení v `NuGet.config` souborech (včetně zdrojů balíčků) jsou stále aplikována, jak je vysvětleno v tématu [běžné konfigurace NuGet](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="fde48-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.config` files (including package sources) are still applied as explained in [Common NuGet configurations](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="fde48-106">Pomocí PackageReference můžete také použít podmínky nástroje MSBuild pro výběr odkazů na balíčky na cílové rozhraní nebo jiná seskupení.</span><span class="sxs-lookup"><span data-stu-id="fde48-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, or other groupings.</span></span> <span data-ttu-id="fde48-107">Umožňuje také jemně odstupňovanou kontrolu nad závislostmi a tokem obsahu.</span><span class="sxs-lookup"><span data-stu-id="fde48-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="fde48-108">(Další podrobnosti najdete v tématu Další informace o [sadě NuGet Pack a obnovení jako cíle MSBuild](../reference/msbuild-targets.md).)</span><span class="sxs-lookup"><span data-stu-id="fde48-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

## <a name="project-type-support"></a><span data-ttu-id="fde48-109">Podpora typu projektu</span><span class="sxs-lookup"><span data-stu-id="fde48-109">Project type support</span></span>

<span data-ttu-id="fde48-110">Ve výchozím nastavení se PackageReference používá pro projekty .NET Core, .NET Standard projekty a projekty UWP cílené na Windows 10 Build 15063 (Creators Update) a novější, s výjimkou projektů v jazyce C++ UWP.</span><span class="sxs-lookup"><span data-stu-id="fde48-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="fde48-111">Projekty .NET Framework podporují PackageReference, ale aktuálně mají výchozí hodnotu `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="fde48-111">.NET Framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="fde48-112">Chcete-li použít PackageReference, [migrujte](../consume-packages/migrate-packages-config-to-package-reference.md) závislosti z nástroje `packages.config` do souboru projektu a pak odeberte packages.config.</span><span class="sxs-lookup"><span data-stu-id="fde48-112">To use PackageReference, [migrate](../consume-packages/migrate-packages-config-to-package-reference.md) the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

<span data-ttu-id="fde48-113">ASP.NET aplikace, které cílí na úplné .NET Framework, zahrnují jenom [omezené podpory](https://github.com/NuGet/Home/issues/5877) pro PackageReference.</span><span class="sxs-lookup"><span data-stu-id="fde48-113">ASP.NET apps targeting the full .NET Framework include only [limited support](https://github.com/NuGet/Home/issues/5877) for PackageReference.</span></span> <span data-ttu-id="fde48-114">Typy projektů C++ a JavaScript nejsou podporovány.</span><span class="sxs-lookup"><span data-stu-id="fde48-114">C++ and JavaScript project types are unsupported.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="fde48-115">Přidání PackageReference</span><span class="sxs-lookup"><span data-stu-id="fde48-115">Adding a PackageReference</span></span>

<span data-ttu-id="fde48-116">Přidejte závislost do souboru projektu pomocí následující syntaxe:</span><span class="sxs-lookup"><span data-stu-id="fde48-116">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="fde48-117">Řízení verze závislosti</span><span class="sxs-lookup"><span data-stu-id="fde48-117">Controlling dependency version</span></span>

<span data-ttu-id="fde48-118">Konvence pro určení verze balíčku je stejná jako při použití `packages.config` :</span><span class="sxs-lookup"><span data-stu-id="fde48-118">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="fde48-119">V příkladu výše 3.6.0 označuje všechny verze, které jsou >= 3.6.0 s upřednostněním pro nejnižší verzi, jak je popsáno v tématu [Správa verzí balíčků](../concepts/package-versioning.md#version-ranges).</span><span class="sxs-lookup"><span data-stu-id="fde48-119">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../concepts/package-versioning.md#version-ranges).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="fde48-120">Použití PackageReference pro projekt bez PackageReferences</span><span class="sxs-lookup"><span data-stu-id="fde48-120">Using PackageReference for a project with no PackageReferences</span></span>

<span data-ttu-id="fde48-121">Upřesnit: Pokud nemáte v projektu nainstalované žádné balíčky (žádné PackageReferences v souboru projektu a žádný soubor packages.config), ale chcete, aby se projekt obnovil jako PackageReferenceový styl, můžete v souboru projektu nastavit RestoreProjectStyle vlastností projektu na PackageReference.</span><span class="sxs-lookup"><span data-stu-id="fde48-121">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="fde48-122">To může být užitečné, pokud odkazujete na projekty, které jsou PackageReference styly (existující projekty csproj nebo sady SDK).</span><span class="sxs-lookup"><span data-stu-id="fde48-122">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="fde48-123">Tím umožníte, aby balíčky, na které tyto projekty odkazují, byly "transitně" odkazovány vaším projektem.</span><span class="sxs-lookup"><span data-stu-id="fde48-123">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="packagereference-and-sources"></a><span data-ttu-id="fde48-124">PackageReference a zdroje</span><span class="sxs-lookup"><span data-stu-id="fde48-124">PackageReference and sources</span></span>

<span data-ttu-id="fde48-125">V projektech PackageReference se v době obnovení vyřeší verze přenosných závislostí.</span><span class="sxs-lookup"><span data-stu-id="fde48-125">In PackageReference projects, the transitive dependency versions are resolved at restore time.</span></span> <span data-ttu-id="fde48-126">V takovém případě musí být v projektech PackageReference k dispozici všechny zdroje pro všechna obnovení.</span><span class="sxs-lookup"><span data-stu-id="fde48-126">As such, in PackageReference projects all sources need to be available for all restores.</span></span> 

## <a name="floating-versions"></a><span data-ttu-id="fde48-127">Plovoucí verze</span><span class="sxs-lookup"><span data-stu-id="fde48-127">Floating Versions</span></span>

<span data-ttu-id="fde48-128">[Plovoucí verze](../concepts/dependency-resolution.md#floating-versions) jsou podporované pomocí `PackageReference` :</span><span class="sxs-lookup"><span data-stu-id="fde48-128">[Floating versions](../concepts/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="fde48-129">Řízení prostředků závislosti</span><span class="sxs-lookup"><span data-stu-id="fde48-129">Controlling dependency assets</span></span>

<span data-ttu-id="fde48-130">Je možné, že použijete závislost čistě jako ve vývojovém prostředí a nechcete ji vystavit pro projekty, které budou spotřebovávat váš balíček.</span><span class="sxs-lookup"><span data-stu-id="fde48-130">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="fde48-131">V tomto scénáři můžete `PrivateAssets` k řízení tohoto chování použít metadata.</span><span class="sxs-lookup"><span data-stu-id="fde48-131">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="fde48-132">Následující Tagy metadat řídí prostředky závislostí:</span><span class="sxs-lookup"><span data-stu-id="fde48-132">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="fde48-133">Značka</span><span class="sxs-lookup"><span data-stu-id="fde48-133">Tag</span></span> | <span data-ttu-id="fde48-134">Popis</span><span class="sxs-lookup"><span data-stu-id="fde48-134">Description</span></span> | <span data-ttu-id="fde48-135">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="fde48-135">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fde48-136">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="fde48-136">IncludeAssets</span></span> | <span data-ttu-id="fde48-137">Tyto prostředky budou spotřebovány.</span><span class="sxs-lookup"><span data-stu-id="fde48-137">These assets will be consumed</span></span> | <span data-ttu-id="fde48-138">Vše</span><span class="sxs-lookup"><span data-stu-id="fde48-138">all</span></span> |
| <span data-ttu-id="fde48-139">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="fde48-139">ExcludeAssets</span></span> | <span data-ttu-id="fde48-140">Tyto prostředky nebudou spotřebovány.</span><span class="sxs-lookup"><span data-stu-id="fde48-140">These assets will not be consumed</span></span> | <span data-ttu-id="fde48-141">žádné</span><span class="sxs-lookup"><span data-stu-id="fde48-141">none</span></span> |
| <span data-ttu-id="fde48-142">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="fde48-142">PrivateAssets</span></span> | <span data-ttu-id="fde48-143">Tyto prostředky budou spotřebovány, ale nebudou se přesměrovat do nadřazeného projektu.</span><span class="sxs-lookup"><span data-stu-id="fde48-143">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="fde48-144">contentFiles; analyzátory; sestavit</span><span class="sxs-lookup"><span data-stu-id="fde48-144">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="fde48-145">Přípustné hodnoty pro tyto značky jsou následující, s více hodnotami oddělenými středníkem s výjimkou `all` a, `none` které se musí objevit sami:</span><span class="sxs-lookup"><span data-stu-id="fde48-145">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="fde48-146">Hodnota</span><span class="sxs-lookup"><span data-stu-id="fde48-146">Value</span></span> | <span data-ttu-id="fde48-147">Popis</span><span class="sxs-lookup"><span data-stu-id="fde48-147">Description</span></span> |
| --- | ---
| <span data-ttu-id="fde48-148">kompilovat</span><span class="sxs-lookup"><span data-stu-id="fde48-148">compile</span></span> | <span data-ttu-id="fde48-149">Obsah `lib` složky a určuje, zda je projekt kompilován proti sestavením v rámci složky</span><span class="sxs-lookup"><span data-stu-id="fde48-149">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="fde48-150">modul runtime</span><span class="sxs-lookup"><span data-stu-id="fde48-150">runtime</span></span> | <span data-ttu-id="fde48-151">Obsah `lib` `runtimes` složky a určuje, zda budou tato sestavení zkopírována do výstupního adresáře sestavení</span><span class="sxs-lookup"><span data-stu-id="fde48-151">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="fde48-152">contentFiles</span><span class="sxs-lookup"><span data-stu-id="fde48-152">contentFiles</span></span> | <span data-ttu-id="fde48-153">Obsah `contentfiles` složky</span><span class="sxs-lookup"><span data-stu-id="fde48-153">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="fde48-154">sestavení</span><span class="sxs-lookup"><span data-stu-id="fde48-154">build</span></span> | <span data-ttu-id="fde48-155">`.props` a `.targets` ve `build` složce</span><span class="sxs-lookup"><span data-stu-id="fde48-155">`.props` and `.targets` in the `build` folder</span></span> |
| <span data-ttu-id="fde48-156">buildMultitargeting</span><span class="sxs-lookup"><span data-stu-id="fde48-156">buildMultitargeting</span></span> | <span data-ttu-id="fde48-157">*(4,0)* `.props` a `.targets` ve `buildMultitargeting` složce pro cílení na různé architektury</span><span class="sxs-lookup"><span data-stu-id="fde48-157">*(4.0)* `.props` and `.targets` in the `buildMultitargeting` folder, for cross-framework targeting</span></span> |
| <span data-ttu-id="fde48-158">buildTransitive</span><span class="sxs-lookup"><span data-stu-id="fde48-158">buildTransitive</span></span> | <span data-ttu-id="fde48-159">*(5.0 +)* `.props` a `.targets` ve `buildTransitive` složce pro prostředky, jejichž přenos do libovolného náročného projektu se protéká.</span><span class="sxs-lookup"><span data-stu-id="fde48-159">*(5.0+)* `.props` and `.targets` in the `buildTransitive` folder, for assets that flow transitively to any consuming project.</span></span> <span data-ttu-id="fde48-160">Podívejte se na stránku [funkce](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) .</span><span class="sxs-lookup"><span data-stu-id="fde48-160">See the [feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) page.</span></span> |
| <span data-ttu-id="fde48-161">analyzátory</span><span class="sxs-lookup"><span data-stu-id="fde48-161">analyzers</span></span> | <span data-ttu-id="fde48-162">Analyzátory .NET</span><span class="sxs-lookup"><span data-stu-id="fde48-162">.NET analyzers</span></span> |
| <span data-ttu-id="fde48-163">nativní</span><span class="sxs-lookup"><span data-stu-id="fde48-163">native</span></span> | <span data-ttu-id="fde48-164">Obsah `native` složky</span><span class="sxs-lookup"><span data-stu-id="fde48-164">Contents of the `native` folder</span></span> |
| <span data-ttu-id="fde48-165">žádné</span><span class="sxs-lookup"><span data-stu-id="fde48-165">none</span></span> | <span data-ttu-id="fde48-166">Žádná z výše uvedených verzí se nepoužívá.</span><span class="sxs-lookup"><span data-stu-id="fde48-166">None of the above are used.</span></span> |
| <span data-ttu-id="fde48-167">Vše</span><span class="sxs-lookup"><span data-stu-id="fde48-167">all</span></span> | <span data-ttu-id="fde48-168">Všechny výše uvedené (kromě `none` )</span><span class="sxs-lookup"><span data-stu-id="fde48-168">All of the above (except `none`)</span></span> |

<span data-ttu-id="fde48-169">V následujícím příkladu je vše kromě souborů obsahu z balíčku spotřebováno projektem a vše kromě souborů obsahu a analyzátory by vedlo k nadřazenému projektu.</span><span class="sxs-lookup"><span data-stu-id="fde48-169">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="fde48-170">Všimněte si, že protože `build` není součástí `PrivateAssets` , cíle a props *budou* tok do nadřazeného projektu.</span><span class="sxs-lookup"><span data-stu-id="fde48-170">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="fde48-171">Vezměte v úvahu například, že odkaz výše se používá v projektu, který vytváří balíček NuGet s názvem AppLogger.</span><span class="sxs-lookup"><span data-stu-id="fde48-171">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="fde48-172">AppLogger může využívat cíle a props z `Contoso.Utility.UsefulStuff` , jako mohou projekty, které využívají AppLogger.</span><span class="sxs-lookup"><span data-stu-id="fde48-172">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

> [!NOTE]
> <span data-ttu-id="fde48-173">Když `developmentDependency` je v souboru nastavená na `true` `.nuspec` , označí balíček jako součást jedinou pro vývoj, která zabrání zahrnutí balíčku jako závislosti v jiných balíčcích.</span><span class="sxs-lookup"><span data-stu-id="fde48-173">When `developmentDependency` is set to `true` in a `.nuspec` file, this marks a package as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="fde48-174">Pomocí PackageReference *(NuGet 4,8 +)* tento příznak také znamená, že vyloučí prostředky při kompilaci z kompilace.</span><span class="sxs-lookup"><span data-stu-id="fde48-174">With PackageReference *(NuGet 4.8+)*, this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="fde48-175">Další informace najdete v tématu [Podpora DevelopmentDependency pro PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span><span class="sxs-lookup"><span data-stu-id="fde48-175">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="fde48-176">Přidání podmínky PackageReference</span><span class="sxs-lookup"><span data-stu-id="fde48-176">Adding a PackageReference condition</span></span>

<span data-ttu-id="fde48-177">Podmínku můžete použít k určení, zda je balíček zahrnut, kde podmínky mohou používat jakoukoli proměnnou MSBuild nebo proměnnou definovanou v souboru TARGETS nebo props.</span><span class="sxs-lookup"><span data-stu-id="fde48-177">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="fde48-178">V předsoučasném případě je však podporována pouze `TargetFramework` Proměnná.</span><span class="sxs-lookup"><span data-stu-id="fde48-178">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="fde48-179">Řekněme například, že cílíte `netstandard1.4` i na `net452` , ale máte závislost, která je platná pouze pro `net452` .</span><span class="sxs-lookup"><span data-stu-id="fde48-179">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="fde48-180">V takovém případě nechcete, aby `netstandard1.4` projekt, který váš balíček spotřebovává, přidal tuto nepotřebnou závislost.</span><span class="sxs-lookup"><span data-stu-id="fde48-180">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="fde48-181">Tomu zabráníte tak, že zadáte podmínku v následujícím `PackageReference` příkladu:</span><span class="sxs-lookup"><span data-stu-id="fde48-181">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="fde48-182">Balíček sestavený pomocí tohoto projektu zobrazí, že Newtonsoft.Jsv je součástí pouze závislosti pro `net452` cíl:</span><span class="sxs-lookup"><span data-stu-id="fde48-182">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![Výsledek použití podmínky v PackageReference s VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="fde48-184">Podmínky lze také použít na `ItemGroup` úrovni a budou platit pro všechny podřízené `PackageReference` prvky:</span><span class="sxs-lookup"><span data-stu-id="fde48-184">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="generatepathproperty"></a><span data-ttu-id="fde48-185">GeneratePathProperty</span><span class="sxs-lookup"><span data-stu-id="fde48-185">GeneratePathProperty</span></span>

<span data-ttu-id="fde48-186">Tato funkce je k dispozici pro NuGet **5,0** nebo vyšší a pro Visual Studio 2019 **16,0** nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="fde48-186">This feature is available with NuGet **5.0** or above and with Visual Studio 2019 **16.0** or above.</span></span>

<span data-ttu-id="fde48-187">V některých případech je žádoucí, aby odkazovaly na soubory v balíčku z cíle MSBuild.</span><span class="sxs-lookup"><span data-stu-id="fde48-187">Sometimes it is desirable to reference files in a package from an MSBuild target.</span></span>
<span data-ttu-id="fde48-188">V `packages.config` projektech založených na projektech jsou balíčky nainstalovány ve složce relativní vzhledem k souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="fde48-188">In `packages.config` based projects, the packages are installed in a folder relative to the project file.</span></span> <span data-ttu-id="fde48-189">V PackageReference jsou však balíčky [spotřebovány](../concepts/package-installation-process.md) ze složky *Global-Packages* , která se může lišit v závislosti na počítači.</span><span class="sxs-lookup"><span data-stu-id="fde48-189">However in PackageReference, the packages are [consumed](../concepts/package-installation-process.md) from the *global-packages* folder, which can vary from machine to machine.</span></span>

<span data-ttu-id="fde48-190">Za účelem přemostění NuGet představila vlastnost, která odkazuje na umístění, ze kterého se balíček spotřebuje.</span><span class="sxs-lookup"><span data-stu-id="fde48-190">To bridge that gap, NuGet introduced a property that points to the location from which the package will be consumed.</span></span>

<span data-ttu-id="fde48-191">Příklad:</span><span class="sxs-lookup"><span data-stu-id="fde48-191">Example:</span></span>

```xml
  <ItemGroup>
      <PackageReference Include="Some.Package" Version="1.0.0" GeneratePathProperty="true" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgSome_Package)\something.exe" />
  </Target>
````

<span data-ttu-id="fde48-192">Kromě toho NuGet automaticky vygeneruje vlastnosti pro balíčky obsahující složku Tools.</span><span class="sxs-lookup"><span data-stu-id="fde48-192">Additionally NuGet will automatically generate properties for packages containing a tools folder.</span></span>

```xml
  <ItemGroup>
      <PackageReference Include="Package.With.Tools" Version="1.0.0" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgPackage_With_Tools)\tools\tool.exe" />
  </Target>
```

<span data-ttu-id="fde48-193">Vlastnosti nástroje MSBuild a identity balíčku nemají stejná omezení, takže Identita balíčku musí být změněna na popisný název MSBuild, který je opraven slovem `Pkg` .</span><span class="sxs-lookup"><span data-stu-id="fde48-193">MSBuild properties and package identities do not have the same restrictions so the package identity needs to be changed to an MSBuild friendly name, prefixed by the word `Pkg`.</span></span>
<span data-ttu-id="fde48-194">Chcete-li ověřit přesný název generované vlastnosti, podívejte se do vygenerovaného souboru [NuGet. g. props](../reference/msbuild-targets.md#restore-outputs) .</span><span class="sxs-lookup"><span data-stu-id="fde48-194">To verify the exact name of the property generated, look at the generated [nuget.g.props](../reference/msbuild-targets.md#restore-outputs) file.</span></span>

## <a name="packagereference-aliases"></a><span data-ttu-id="fde48-195">PackageReference aliasy</span><span class="sxs-lookup"><span data-stu-id="fde48-195">PackageReference Aliases</span></span>

<span data-ttu-id="fde48-196">V některých vzácných instancích budou různé balíčky obsahovat třídy ve stejném oboru názvů.</span><span class="sxs-lookup"><span data-stu-id="fde48-196">In some rare instances different packages will contain classes in the same namespace.</span></span> <span data-ttu-id="fde48-197">Počínaje verzí NuGet 5,7 & Visual Studio 2019 Update 7, který je ekvivalentní s ProjectReference, PackageReference podporuje [`Aliases`](/dotnet/api/microsoft.codeanalysis.projectreference.aliases) .</span><span class="sxs-lookup"><span data-stu-id="fde48-197">Starting with NuGet 5.7 & Visual Studio 2019 Update 7, equivalent to ProjectReference, PackageReference supports [`Aliases`](/dotnet/api/microsoft.codeanalysis.projectreference.aliases).</span></span>
<span data-ttu-id="fde48-198">Ve výchozím nastavení nejsou k dispozici žádné aliasy.</span><span class="sxs-lookup"><span data-stu-id="fde48-198">By default no aliases are provided.</span></span> <span data-ttu-id="fde48-199">Když je zadán alias, *všechna* sestavení pocházející z balíčku s poznámkami musí být odkazována aliasem.</span><span class="sxs-lookup"><span data-stu-id="fde48-199">When an alias is specified, *all* assemblies coming from the annotated package with need to be referenced with an alias.</span></span>

<span data-ttu-id="fde48-200">Můžete se podívat na ukázkové použití na [NuGet\Samples](https://github.com/NuGet/Samples/tree/master/PackageReferenceAliasesExample)</span><span class="sxs-lookup"><span data-stu-id="fde48-200">You can look at sample usage at [NuGet\Samples](https://github.com/NuGet/Samples/tree/master/PackageReferenceAliasesExample)</span></span>

<span data-ttu-id="fde48-201">V souboru projektu zadejte aliasy následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="fde48-201">In the project file, specify the aliases as follows:</span></span>

```xml
  <ItemGroup>
    <PackageReference Include="NuGet.Versioning" Version="5.8.0" Aliases="ExampleAlias" />
  </ItemGroup>
```

<span data-ttu-id="fde48-202">a v kódu ho použijte následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="fde48-202">and in the code use it as follows:</span></span>

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

## <a name="nuget-warnings-and-errors"></a><span data-ttu-id="fde48-203">Upozornění a chyby NuGet</span><span class="sxs-lookup"><span data-stu-id="fde48-203">NuGet warnings and errors</span></span>

<span data-ttu-id="fde48-204">*Tato funkce je k dispozici pro NuGet **4,3** nebo vyšší a pro Visual Studio 2017 **15,3** nebo vyšší.*</span><span class="sxs-lookup"><span data-stu-id="fde48-204">*This feature is available with NuGet **4.3** or above and with Visual Studio 2017 **15.3** or above.*</span></span>

<span data-ttu-id="fde48-205">Pro mnoho scénářů sad a obnovení jsou všechna upozornění a chyby NuGet zakódované a začínají na `NU****` .</span><span class="sxs-lookup"><span data-stu-id="fde48-205">For many pack and restore scenarios, all NuGet warnings and errors are coded, and start with `NU****`.</span></span> <span data-ttu-id="fde48-206">Všechna upozornění a chyby NuGet jsou uvedená v [referenční](../reference/errors-and-warnings.md) dokumentaci.</span><span class="sxs-lookup"><span data-stu-id="fde48-206">All NuGet warnings and errors are listed in the [reference](../reference/errors-and-warnings.md) documentation.</span></span>

<span data-ttu-id="fde48-207">NuGet sleduje následující vlastnosti upozornění:</span><span class="sxs-lookup"><span data-stu-id="fde48-207">NuGet observes the following warning properties:</span></span>

- <span data-ttu-id="fde48-208">`TreatWarningsAsErrors`, považovat všechna upozornění za chyby</span><span class="sxs-lookup"><span data-stu-id="fde48-208">`TreatWarningsAsErrors`, treat all warnings as errors</span></span>
- <span data-ttu-id="fde48-209">`WarningsAsErrors`, považovat specifická upozornění za chyby</span><span class="sxs-lookup"><span data-stu-id="fde48-209">`WarningsAsErrors`, treat specific warnings as errors</span></span>
- <span data-ttu-id="fde48-210">`NoWarn`, skryjte konkrétní upozornění, ať už na úrovni projektu, nebo na úrovni balíčku.</span><span class="sxs-lookup"><span data-stu-id="fde48-210">`NoWarn`, hide specific warnings, either project-wide or package-wide.</span></span>

<span data-ttu-id="fde48-211">Příklady:</span><span class="sxs-lookup"><span data-stu-id="fde48-211">Examples:</span></span>

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

### <a name="suppressing-nuget-warnings"></a><span data-ttu-id="fde48-212">Potlačení upozornění NuGet</span><span class="sxs-lookup"><span data-stu-id="fde48-212">Suppressing NuGet warnings</span></span>

<span data-ttu-id="fde48-213">I když se vám doporučuje vyřešit všechna upozornění sady NuGet během operací aktualizace a obnovení, v některých případech je jejich potlačení oprávněné.</span><span class="sxs-lookup"><span data-stu-id="fde48-213">While it is recommended that you resolve all NuGet warnings during your pack and restore operations, in certain situations suppressing them is warranted.</span></span>
<span data-ttu-id="fde48-214">Chcete-li potlačit projekt s upozorněním na šířku, zvažte provedení těchto akcí:</span><span class="sxs-lookup"><span data-stu-id="fde48-214">To suppress a warning project wide, consider doing:</span></span>

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
    <NoWarn>$(NoWarn);NU5104</NoWarn>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1"/>
</ItemGroup>
```

<span data-ttu-id="fde48-215">Upozornění se někdy vztahují jenom na určitý balíček v grafu.</span><span class="sxs-lookup"><span data-stu-id="fde48-215">Sometimes warnings apply only to a certain package in the graph.</span></span> <span data-ttu-id="fde48-216">Můžeme se rozhodnout pro potlačení tohoto upozornění selektivně přidáním `NoWarn` položky na položku PackageReference.</span><span class="sxs-lookup"><span data-stu-id="fde48-216">We can choose to suppress that warning more selectively by adding a `NoWarn` on the PackageReference item.</span></span> 

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1" NoWarn="NU1603" />
</ItemGroup>
```

#### <a name="suppressing-nuget-package-warnings-in-visual-studio"></a><span data-ttu-id="fde48-217">Potlačení upozornění balíčku NuGet v aplikaci Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fde48-217">Suppressing NuGet package warnings in Visual Studio</span></span>

<span data-ttu-id="fde48-218">Při v aplikaci Visual Studio můžete také [potlačit upozornění](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) prostřednictvím integrovaného vývojového prostředí (IDE).</span><span class="sxs-lookup"><span data-stu-id="fde48-218">When in Visual Studio, you can also [suppress warnings](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) through the IDE.</span></span>

## <a name="locking-dependencies"></a><span data-ttu-id="fde48-219">Uzamykání závislostí</span><span class="sxs-lookup"><span data-stu-id="fde48-219">Locking dependencies</span></span>

<span data-ttu-id="fde48-220">*Tato funkce je k dispozici pro NuGet **4,9** nebo vyšší a pro Visual Studio 2017 **15,9** nebo vyšší.*</span><span class="sxs-lookup"><span data-stu-id="fde48-220">*This feature is available with NuGet **4.9** or above and with Visual Studio 2017 **15.9** or above.*</span></span>

<span data-ttu-id="fde48-221">Vstup do obnovení NuGet je sada odkazů na balíčky ze souboru projektu (závislosti na nejvyšší úrovni nebo přímých závislostí) a výstup je plný uzávěr všech závislostí balíčku včetně přenosných závislostí.</span><span class="sxs-lookup"><span data-stu-id="fde48-221">Input to NuGet restore is a set of Package References from the project file (top-level or direct dependencies) and the output is a full closure of all the package dependencies including transitive dependencies.</span></span> <span data-ttu-id="fde48-222">V případě, že se vstupní seznam PackageReference nezměnil, nástroj NuGet se pokusí vždy vydávat stejný plný uzávěr závislostí balíčku.</span><span class="sxs-lookup"><span data-stu-id="fde48-222">NuGet tries to always produce the same full closure of package dependencies if the input PackageReference list has not changed.</span></span> <span data-ttu-id="fde48-223">Existují však situace, kdy to není možné.</span><span class="sxs-lookup"><span data-stu-id="fde48-223">However, there are some scenarios where it is unable to do so.</span></span> <span data-ttu-id="fde48-224">Příklad:</span><span class="sxs-lookup"><span data-stu-id="fde48-224">For example:</span></span>

* <span data-ttu-id="fde48-225">Při použití plovoucích verzí, jako je `<PackageReference Include="My.Sample.Lib" Version="4.*"/>` .</span><span class="sxs-lookup"><span data-stu-id="fde48-225">When you use floating versions like `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span></span> <span data-ttu-id="fde48-226">I když tady je tento záměr na nejnovější verzi v každé obnovy balíčků, existují situace, kdy uživatelé potřebují, aby byl graf uzamčený na určitou nejnovější verzi a aby byl na novější verzi, pokud je k dispozici, po explicitním gestu.</span><span class="sxs-lookup"><span data-stu-id="fde48-226">While the intention here is to float to the latest version on every restore of packages, there are scenarios where users require the graph to be locked to a certain latest version and float to a later version, if available, upon an explicit gesture.</span></span>
* <span data-ttu-id="fde48-227">Je publikovaná novější verze balíčku, která odpovídá požadavkům verze PackageReference.</span><span class="sxs-lookup"><span data-stu-id="fde48-227">A newer version of the package matching PackageReference version requirements is published.</span></span> <span data-ttu-id="fde48-228">Například</span><span class="sxs-lookup"><span data-stu-id="fde48-228">E.g.</span></span> 

  * <span data-ttu-id="fde48-229">Den 1: Pokud jste zadali `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` verze, které jsou k dispozici v úložištích NuGet, byly 4.1.0, 4.2.0 a 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="fde48-229">Day 1: if you specified `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` but the versions available on the NuGet repositories were 4.1.0, 4.2.0 and 4.3.0.</span></span> <span data-ttu-id="fde48-230">V tomto případě se NuGet přeložil na 4.1.0 (nejbližší minimální verzi).</span><span class="sxs-lookup"><span data-stu-id="fde48-230">In this case, NuGet would have resolved to  4.1.0 (nearest minimum version)</span></span>

  * <span data-ttu-id="fde48-231">Den 2: verze 4.0.0 se publikuje.</span><span class="sxs-lookup"><span data-stu-id="fde48-231">Day 2: Version 4.0.0 gets published.</span></span> <span data-ttu-id="fde48-232">NuGet teď najde přesnou shodu a začne řešit na 4.0.0</span><span class="sxs-lookup"><span data-stu-id="fde48-232">NuGet will now find the exact match and start resolving to 4.0.0</span></span>

* <span data-ttu-id="fde48-233">Daná verze balíčku se odebere z úložiště.</span><span class="sxs-lookup"><span data-stu-id="fde48-233">A given package version is removed from the repository.</span></span> <span data-ttu-id="fde48-234">I když nuget.org nepovoluje odstraňování balíčků, ne všechna úložiště balíčků mají tato omezení.</span><span class="sxs-lookup"><span data-stu-id="fde48-234">Though nuget.org does not allow package deletions, not all package repositories have this constraints.</span></span> <span data-ttu-id="fde48-235">Výsledkem je, že NuGet najde nejlepší shodu, když ho nelze vyřešit na odstraněnou verzi.</span><span class="sxs-lookup"><span data-stu-id="fde48-235">This results in NuGet finding the best match when it cannot resolve to the deleted version.</span></span>

### <a name="enabling-lock-file"></a><span data-ttu-id="fde48-236">Povoluje se soubor zámku.</span><span class="sxs-lookup"><span data-stu-id="fde48-236">Enabling lock file</span></span>

<span data-ttu-id="fde48-237">Aby se zachoval úplný konec závislostí balíčku, můžete se přihlásit k funkci zámek souboru nastavením vlastnosti MSBuild `RestorePackagesWithLockFile` pro váš projekt:</span><span class="sxs-lookup"><span data-stu-id="fde48-237">In order to persist the full closure of package dependencies you can opt-in to the lock file feature by setting the MSBuild property `RestorePackagesWithLockFile` for your project:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="fde48-238">Pokud je tato vlastnost nastavená, obnovení NuGet vygeneruje soubor zámku File `packages.lock.json` v kořenovém adresáři projektu, který obsahuje seznam všech závislostí balíčku.</span><span class="sxs-lookup"><span data-stu-id="fde48-238">If this property is set, NuGet restore will generate a lock file - `packages.lock.json` file at the project root directory that lists all the package dependencies.</span></span> 

> [!Note]
> <span data-ttu-id="fde48-239">Jakmile projekt obsahuje `packages.lock.json` soubor ve svém kořenovém adresáři, soubor zámku se vždy používá s obnovením i v případě, že vlastnost není `RestorePackagesWithLockFile` nastavena.</span><span class="sxs-lookup"><span data-stu-id="fde48-239">Once a project has `packages.lock.json` file in its root directory, the lock file is always used with restore even if the property `RestorePackagesWithLockFile` is not set.</span></span> <span data-ttu-id="fde48-240">Další možností, jak se vyjádřit k této funkci, je vytvořit fiktivní prázdný `packages.lock.json` soubor v kořenovém adresáři projektu.</span><span class="sxs-lookup"><span data-stu-id="fde48-240">So another way to opt-in to this feature is to create a dummy blank `packages.lock.json` file in the project's root directory.</span></span>

### <a name="restore-behavior-with-lock-file"></a><span data-ttu-id="fde48-241">`restore` chování se souborem zámku</span><span class="sxs-lookup"><span data-stu-id="fde48-241">`restore` behavior with lock file</span></span>
<span data-ttu-id="fde48-242">Pokud je soubor zámku k dispozici pro projekt, nástroj NuGet používá ke spuštění tento soubor zámku `restore` .</span><span class="sxs-lookup"><span data-stu-id="fde48-242">If a lock file is present for project, NuGet uses this lock file to run `restore`.</span></span> <span data-ttu-id="fde48-243">NuGet provede rychlou kontrolu, jestli se v závislostech balíčku nezměnily žádné změny, jak je uvedeno v souboru projektu (nebo v souborech závislých projektů) a jestli nedošlo k žádným změnám, jenom obnoví balíčky uvedené v souboru zámku.</span><span class="sxs-lookup"><span data-stu-id="fde48-243">NuGet does a quick check to see if there were any changes in the package dependencies as mentioned in the project file (or dependent projects' files) and if there were no changes it just restores the packages mentioned in the lock file.</span></span> <span data-ttu-id="fde48-244">Nedošlo k opakovanému vyhodnocení závislostí balíčku.</span><span class="sxs-lookup"><span data-stu-id="fde48-244">There is no re-evaluation of package dependencies.</span></span>

<span data-ttu-id="fde48-245">Pokud NuGet detekuje změnu v definovaných závislostech, jak je uvedeno v souborech projektu, znovu vyhodnotí graf balíčku a aktualizuje soubor zámku tak, aby odrážel nový uzavření balíčku pro daný projekt.</span><span class="sxs-lookup"><span data-stu-id="fde48-245">If NuGet detects a change in the defined dependencies as mentioned in the project file(s), it re-evaluates the package graph and updates the lock file to reflect the new package closure for the project.</span></span>

<span data-ttu-id="fde48-246">V případě CI/CD a dalších scénářů, kde byste nechtěli změnit závislosti balíčku za běhu, můžete to provést nastavením `lockedmode` na `true` :</span><span class="sxs-lookup"><span data-stu-id="fde48-246">For CI/CD and other scenarios, where you would not want to change the package dependencies on the fly, you can do so by setting the `lockedmode` to `true`:</span></span>

<span data-ttu-id="fde48-247">Pro dotnet.exe spusťte:</span><span class="sxs-lookup"><span data-stu-id="fde48-247">For dotnet.exe, run:</span></span>

```
> dotnet.exe restore --locked-mode
```

<span data-ttu-id="fde48-248">Pro msbuild.exe spusťte:</span><span class="sxs-lookup"><span data-stu-id="fde48-248">For msbuild.exe, run:</span></span>

```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

<span data-ttu-id="fde48-249">Tuto vlastnost podmíněného MSBuild můžete nastavit také v souboru projektu:</span><span class="sxs-lookup"><span data-stu-id="fde48-249">You may also set this conditional MSBuild property in your project file:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

<span data-ttu-id="fde48-250">Pokud je uzamčený režim `true` , obnovení obnoví buď přesné balíčky uvedené v souboru zámku, nebo selže, pokud jste aktualizovali definované závislosti balíčků pro projekt po vytvoření souboru zámku.</span><span class="sxs-lookup"><span data-stu-id="fde48-250">If locked mode is `true`, restore will either restore the exact packages as listed in the lock file or fail if you updated the defined package dependencies for the project after lock file was created.</span></span>

### <a name="make-lock-file-part-of-your-source-repository"></a><span data-ttu-id="fde48-251">Nastavit zámek souboru jako součást zdrojového úložiště</span><span class="sxs-lookup"><span data-stu-id="fde48-251">Make lock file part of your source repository</span></span>
<span data-ttu-id="fde48-252">Pokud vytváříte aplikaci, spustitelný soubor a příslušný projekt jsou na začátku řetězu závislostí a pak proveďte vrácení souboru se zámkem do úložiště zdrojového kódu, aby jej mohla aplikace NuGet využít při obnovení.</span><span class="sxs-lookup"><span data-stu-id="fde48-252">If you are building an application, an executable and the project in question is at the start of the dependency chain then do check in the lock file to the source code repository so that NuGet can make use of it during restore.</span></span>

<span data-ttu-id="fde48-253">Pokud je však projekt knihovnou projektu, který nedodáte nebo se jedná o běžný projekt kódu, na kterém jsou závislé další projekty, **neměli byste** soubory zámku vrátit se změnami jako součást zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="fde48-253">However, if your project is a library project that you do not ship or a common code project on which other projects depend upon, you **should not** check in the lock file as part of your source code.</span></span> <span data-ttu-id="fde48-254">Neexistuje žádný škodný soubor zámku, ale nelze použít uzamčené závislosti balíčku pro běžný projekt kódu, jak je uvedeno v souboru zámku během obnovení nebo sestavení projektu, který je závislý na tomto projektu Common-Code.</span><span class="sxs-lookup"><span data-stu-id="fde48-254">There is no harm in keeping the lock file but the locked package dependencies for the common code project may not be used, as listed in the lock file, during the restore/build of a project that depends on this common-code project.</span></span>

<span data-ttu-id="fde48-255">Např.</span><span class="sxs-lookup"><span data-stu-id="fde48-255">Eg.</span></span>

```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```

<span data-ttu-id="fde48-256">Pokud `ProjectA` má závislost na `PackageX` verzi `2.0.0` a také odkazy `ProjectB` , které závisejí na `PackageX` verzi `1.0.0` , pak soubor zámku pro `ProjectB` bude zobrazovat závislost na `PackageX` verzi `1.0.0` .</span><span class="sxs-lookup"><span data-stu-id="fde48-256">If `ProjectA` has a dependency on a `PackageX` version `2.0.0` and also references `ProjectB` that depends on `PackageX` version `1.0.0`, then the lock file for `ProjectB` will list a dependency on `PackageX` version `1.0.0`.</span></span> <span data-ttu-id="fde48-257">Když je však `ProjectA` sestaven, jeho soubor zámku bude obsahovat závislost na `PackageX` verzi **`2.0.0`** a **nikoli** `1.0.0` , jak je uvedeno v souboru zámku pro `ProjectB` .</span><span class="sxs-lookup"><span data-stu-id="fde48-257">However, when `ProjectA` is built, its lock file will contain a dependency on `PackageX` version **`2.0.0`** and **not** `1.0.0` as listed in the lock file for `ProjectB`.</span></span> <span data-ttu-id="fde48-258">Proto soubor zámku pro běžný projekt kódu trochu říká, že balíčky byly vyřešeny pro projekty, které jsou na ní závislé.</span><span class="sxs-lookup"><span data-stu-id="fde48-258">Thus, the lock file of a common code project has little say over the packages resolved for projects that depend on it.</span></span>

### <a name="lock-file-extensibility"></a><span data-ttu-id="fde48-259">Zamknout rozšíření souboru</span><span class="sxs-lookup"><span data-stu-id="fde48-259">Lock file extensibility</span></span>

<span data-ttu-id="fde48-260">Můžete řídit různá chování při obnovení pomocí souboru zámku, jak je popsáno níže:</span><span class="sxs-lookup"><span data-stu-id="fde48-260">You can control various behaviors of restore with lock file as described below:</span></span>

| <span data-ttu-id="fde48-261">Možnost NuGet.exe</span><span class="sxs-lookup"><span data-stu-id="fde48-261">NuGet.exe option</span></span> | <span data-ttu-id="fde48-262">dotnet – možnost</span><span class="sxs-lookup"><span data-stu-id="fde48-262">dotnet option</span></span> | <span data-ttu-id="fde48-263">Možnost ekvivalentu MSBuild</span><span class="sxs-lookup"><span data-stu-id="fde48-263">MSBuild equivalent option</span></span> | <span data-ttu-id="fde48-264">Popis</span><span class="sxs-lookup"><span data-stu-id="fde48-264">Description</span></span> |
|:--- |:--- |:--- |:--- |
| `-UseLockFile` |`--use-lock-file` | <span data-ttu-id="fde48-265">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="fde48-265">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="fde48-266">Výslovný se na použití souboru zámku.</span><span class="sxs-lookup"><span data-stu-id="fde48-266">Opts into the usage of a lock file.</span></span> |
| `-LockedMode` | `--locked-mode` | <span data-ttu-id="fde48-267">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="fde48-267">RestoreLockedMode</span></span> | <span data-ttu-id="fde48-268">Zapne uzamčený režim pro obnovení.</span><span class="sxs-lookup"><span data-stu-id="fde48-268">Enables locked mode for restore.</span></span> <span data-ttu-id="fde48-269">To je užitečné ve scénářích CI/CD, kde chcete opakovat sestavení.</span><span class="sxs-lookup"><span data-stu-id="fde48-269">This is useful in CI/CD scenarios where you want repeatable builds.</span></span>|   
| `-ForceEvaluate` | `--force-evaluate` | <span data-ttu-id="fde48-270">RestoreForceEvaluate</span><span class="sxs-lookup"><span data-stu-id="fde48-270">RestoreForceEvaluate</span></span> | <span data-ttu-id="fde48-271">Tato možnost je užitečná pro balíčky s plovoucí verzí definovanou v projektu.</span><span class="sxs-lookup"><span data-stu-id="fde48-271">This option is useful with packages with floating version defined in the project.</span></span> <span data-ttu-id="fde48-272">Ve výchozím nastavení při obnovení NuGet nebude automaticky aktualizovat verzi balíčku pro každé obnovení, pokud u této možnosti nespustíte příkaz Restore.</span><span class="sxs-lookup"><span data-stu-id="fde48-272">By default, NuGet restore will not update the package version automatically upon each restore unless you run restore with this option.</span></span> |
| `-LockFilePath` | `--lock-file-path` | <span data-ttu-id="fde48-273">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="fde48-273">NuGetLockFilePath</span></span> | <span data-ttu-id="fde48-274">Definuje vlastní umístění souboru zámku pro projekt.</span><span class="sxs-lookup"><span data-stu-id="fde48-274">Defines a custom lock file location for a project.</span></span> <span data-ttu-id="fde48-275">Ve výchozím nastavení NuGet podporuje `packages.lock.json` v kořenovém adresáři.</span><span class="sxs-lookup"><span data-stu-id="fde48-275">By default, NuGet supports `packages.lock.json` at the root directory.</span></span> <span data-ttu-id="fde48-276">Pokud máte ve stejném adresáři více projektů, NuGet podporuje soubor zámku specifický pro projekt. `packages.<project_name>.lock.json`</span><span class="sxs-lookup"><span data-stu-id="fde48-276">If you have multiple projects in the same directory, NuGet supports project specific lock file `packages.<project_name>.lock.json`</span></span> |

## <a name="assettargetfallback"></a><span data-ttu-id="fde48-277">AssetTargetFallback</span><span class="sxs-lookup"><span data-stu-id="fde48-277">AssetTargetFallback</span></span>

<span data-ttu-id="fde48-278">`AssetTargetFallback`Vlastnost umožňuje určit další kompatibilní verze rozhraní pro projekty, na které projekt odkazuje, a balíčky NuGet, které váš projekt spotřebovává.</span><span class="sxs-lookup"><span data-stu-id="fde48-278">The `AssetTargetFallback` property lets you specify additional compatible framework versions for projects that your project references and NuGet packages that your project consumes.</span></span>

<span data-ttu-id="fde48-279">Pokud zadáte závislost balíčku pomocí `PackageReference` , ale tento balíček neobsahuje prostředky, které jsou kompatibilní s cílovým rozhraním .NET Framework vašich projektů, `AssetTargetFallback` vlastnost se dostane do hry.</span><span class="sxs-lookup"><span data-stu-id="fde48-279">If you specify a package dependency using `PackageReference` but that package doesn't contain assets that are compatible with your projects's target framework, the `AssetTargetFallback` property comes into play.</span></span> <span data-ttu-id="fde48-280">Kompatibilita odkazovaného balíčku je znovu zkontrolována pomocí každé cílové architektury, která je určena v `AssetTargetFallback` .</span><span class="sxs-lookup"><span data-stu-id="fde48-280">The compatibility of the referenced package is rechecked using each target framework that's specified in `AssetTargetFallback`.</span></span>
<span data-ttu-id="fde48-281">V případě `project` , že `package` je odkazováno na nebo `AssetTargetFallback` , se vyvolá upozornění [NU1701](../reference/errors-and-warnings/NU1701.md) .</span><span class="sxs-lookup"><span data-stu-id="fde48-281">When a `project` or a `package` is referenced through `AssetTargetFallback`, the [NU1701](../reference/errors-and-warnings/NU1701.md) warning will be raised.</span></span>

<span data-ttu-id="fde48-282">V následující tabulce najdete příklady `AssetTargetFallback` vlivu kompatibility.</span><span class="sxs-lookup"><span data-stu-id="fde48-282">Refer to the table below for examples of how `AssetTargetFallback` affects compatibility.</span></span>

| <span data-ttu-id="fde48-283">Projektový rámec</span><span class="sxs-lookup"><span data-stu-id="fde48-283">Project framework</span></span> | <span data-ttu-id="fde48-284">AssetTargetFallback</span><span class="sxs-lookup"><span data-stu-id="fde48-284">AssetTargetFallback</span></span> | <span data-ttu-id="fde48-285">Balíčky balíčků</span><span class="sxs-lookup"><span data-stu-id="fde48-285">Package frameworks</span></span> | <span data-ttu-id="fde48-286">Výsledek</span><span class="sxs-lookup"><span data-stu-id="fde48-286">Result</span></span> |
|-------------------|---------------------|--------------------|--------|
| <span data-ttu-id="fde48-287"> .NET Framework 4.7.2</span><span class="sxs-lookup"><span data-stu-id="fde48-287">.NET Framework 4.7.2</span></span> | | <span data-ttu-id="fde48-288">.NET Standard 2,0</span><span class="sxs-lookup"><span data-stu-id="fde48-288">.NET Standard 2.0</span></span> | <span data-ttu-id="fde48-289">.NET Standard 2,0</span><span class="sxs-lookup"><span data-stu-id="fde48-289">.NET Standard 2.0</span></span> |
| <span data-ttu-id="fde48-290">.NET Core – aplikace 3,1</span><span class="sxs-lookup"><span data-stu-id="fde48-290">.NET Core App 3.1</span></span> | | <span data-ttu-id="fde48-291">.NET Standard 2,0, .NET Framework 4.7.2</span><span class="sxs-lookup"><span data-stu-id="fde48-291">.NET Standard 2.0, .NET Framework 4.7.2</span></span> | <span data-ttu-id="fde48-292">.NET Standard 2,0</span><span class="sxs-lookup"><span data-stu-id="fde48-292">.NET Standard 2.0</span></span> |
| <span data-ttu-id="fde48-293">.NET Core – aplikace 3,1</span><span class="sxs-lookup"><span data-stu-id="fde48-293">.NET Core App 3.1</span></span> | | <span data-ttu-id="fde48-294"> .NET Framework 4.7.2</span><span class="sxs-lookup"><span data-stu-id="fde48-294">.NET Framework 4.7.2</span></span> | <span data-ttu-id="fde48-295">Nekompatibilní, selhání s [`NU1202`](../reference/errors-and-warnings/NU1202.md)</span><span class="sxs-lookup"><span data-stu-id="fde48-295">Incompatible, fail with [`NU1202`](../reference/errors-and-warnings/NU1202.md)</span></span> |
| <span data-ttu-id="fde48-296">.NET Core – aplikace 3,1</span><span class="sxs-lookup"><span data-stu-id="fde48-296">.NET Core App 3.1</span></span> | <span data-ttu-id="fde48-297">net472;net471</span><span class="sxs-lookup"><span data-stu-id="fde48-297">net472;net471</span></span> | <span data-ttu-id="fde48-298"> .NET Framework 4.7.2</span><span class="sxs-lookup"><span data-stu-id="fde48-298">.NET Framework 4.7.2</span></span> | <span data-ttu-id="fde48-299">.NET Framework 4.7.2 s [`NU1701`](../reference/errors-and-warnings/NU1701.md)</span><span class="sxs-lookup"><span data-stu-id="fde48-299">.NET Framework 4.7.2 with [`NU1701`](../reference/errors-and-warnings/NU1701.md)</span></span> |

<span data-ttu-id="fde48-300">Pomocí oddělovače lze zadat více rozhraní `;` .</span><span class="sxs-lookup"><span data-stu-id="fde48-300">Multiple frameworks can be specified using `;` as a delimiter.</span></span> <span data-ttu-id="fde48-301">Pro přidání záložního rozhraní můžete provést následující akce:</span><span class="sxs-lookup"><span data-stu-id="fde48-301">To add a fallback framework you can do the following:</span></span>

```xml
<AssetTargetFallback Condition=" '$(TargetFramework)'=='netcoreapp3.1' ">
    $(AssetTargetFallback);net472;net471
</AssetTargetFallback>
```

<span data-ttu-id="fde48-302">`$(AssetTargetFallback)`Pokud chcete přepsat místo přidání do stávajících hodnot, můžete ho nechat vypnuté `AssetTargetFallback` .</span><span class="sxs-lookup"><span data-stu-id="fde48-302">You can leave off `$(AssetTargetFallback)` if you wish to overwrite, instead of add to the existing `AssetTargetFallback` values.</span></span>

> [!NOTE]
> <span data-ttu-id="fde48-303">Pokud používáte [projekt založený na sadě .NET SDK](/dotnet/core/sdk), `$(AssetTargetFallback)` jsou nakonfigurovány správné hodnoty a nemusíte je nastavovat ručně.</span><span class="sxs-lookup"><span data-stu-id="fde48-303">If you are using a [.NET SDK based project](/dotnet/core/sdk), appropriate `$(AssetTargetFallback)` values are configured and you do not need to set them manually.</span></span>
>
> <span data-ttu-id="fde48-304">`$(PackageTargetFallback)` byla dřívější funkce, která se pokusila vyřešit tuto výzvu, ale je zásadní a *neměla by* se používat.</span><span class="sxs-lookup"><span data-stu-id="fde48-304">`$(PackageTargetFallback)` was an earlier feature that attempted to address this challenge, but it is fundamentally broken and *should* not be used.</span></span> <span data-ttu-id="fde48-305">Chcete-li provést migraci z nástroje `$(PackageTargetFallback)` na `$(AssetTargetFallback)` , jednoduše změňte název vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="fde48-305">To migrate from `$(PackageTargetFallback)` to `$(AssetTargetFallback)`, simply change the property name.</span></span>
