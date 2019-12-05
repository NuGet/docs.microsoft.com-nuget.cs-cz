---
title: Formát NuGet PackageReference (odkazy na balíčky v souborech projektu)
description: Podrobnosti o NuGet PackageReference v souborech projektu, které podporuje NuGet 4.0 + a VS2017 a .NET Core 2,0
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: b6a009832430ee08f51ea1028feb878a39f45222
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825140"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="d612c-103">Odkazy na balíčky (PackageReference) v souborech projektu</span><span class="sxs-lookup"><span data-stu-id="d612c-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="d612c-104">Odkazy na balíčky, pomocí uzlu `PackageReference`, spravujte závislosti NuGet přímo v souborech projektu (na rozdíl od samostatného `packages.config` souboru).</span><span class="sxs-lookup"><span data-stu-id="d612c-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="d612c-105">Použití PackageReference, jak je voláno, nemá vliv na jiné aspekty NuGet; například nastavení v souborech `NuGet.config` (včetně zdrojů balíčků) jsou stále aplikována, jak je vysvětleno v tématu [běžné konfigurace NuGet](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="d612c-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.config` files (including package sources) are still applied as explained in [Common NuGet configurations](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="d612c-106">Pomocí PackageReference můžete také použít podmínky nástroje MSBuild pro výběr odkazů na balíčky na cílové rozhraní nebo jiná seskupení.</span><span class="sxs-lookup"><span data-stu-id="d612c-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, or other groupings.</span></span> <span data-ttu-id="d612c-107">Umožňuje také jemně odstupňovanou kontrolu nad závislostmi a tokem obsahu.</span><span class="sxs-lookup"><span data-stu-id="d612c-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="d612c-108">(Další podrobnosti najdete v tématu Další informace o [sadě NuGet Pack a obnovení jako cíle MSBuild](../reference/msbuild-targets.md).)</span><span class="sxs-lookup"><span data-stu-id="d612c-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

## <a name="project-type-support"></a><span data-ttu-id="d612c-109">Podpora typu projektu</span><span class="sxs-lookup"><span data-stu-id="d612c-109">Project type support</span></span>

<span data-ttu-id="d612c-110">Ve výchozím nastavení se PackageReference používá pro projekty .NET Core, .NET Standard projekty a projekty UWP cílené na Windows 10 Build 15063 (Creators Update) a novější, s výjimkou C++ projektů UWP.</span><span class="sxs-lookup"><span data-stu-id="d612c-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="d612c-111">Projekty .NET Framework podporují PackageReference, ale aktuálně `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="d612c-111">.NET Framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="d612c-112">Chcete-li použít PackageReference, [migrujte](../consume-packages/migrate-packages-config-to-package-reference.md) závislosti z `packages.config` do souboru projektu a pak odeberte soubor Packages. config.</span><span class="sxs-lookup"><span data-stu-id="d612c-112">To use PackageReference, [migrate](../consume-packages/migrate-packages-config-to-package-reference.md) the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

<span data-ttu-id="d612c-113">ASP.NET aplikace, které cílí na úplné .NET Framework, zahrnují jenom [omezené podpory](https://github.com/NuGet/Home/issues/5877) pro PackageReference.</span><span class="sxs-lookup"><span data-stu-id="d612c-113">ASP.NET apps targeting the full .NET Framework include only [limited support](https://github.com/NuGet/Home/issues/5877) for PackageReference.</span></span> <span data-ttu-id="d612c-114">C++a typy projektů JavaScriptu nejsou podporovány.</span><span class="sxs-lookup"><span data-stu-id="d612c-114">C++ and JavaScript project types are unsupported.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="d612c-115">Přidání PackageReference</span><span class="sxs-lookup"><span data-stu-id="d612c-115">Adding a PackageReference</span></span>

<span data-ttu-id="d612c-116">Přidejte závislost do souboru projektu pomocí následující syntaxe:</span><span class="sxs-lookup"><span data-stu-id="d612c-116">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="d612c-117">Řízení verze závislosti</span><span class="sxs-lookup"><span data-stu-id="d612c-117">Controlling dependency version</span></span>

<span data-ttu-id="d612c-118">Konvence pro určení verze balíčku je stejná jako při použití `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="d612c-118">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="d612c-119">V příkladu výše 3.6.0 označuje všechny verze, které jsou > = 3.6.0 s upřednostněním pro nejnižší verzi, jak je popsáno v tématu [Správa verzí balíčků](../concepts/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="d612c-119">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../concepts/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="d612c-120">Použití PackageReference pro projekt bez PackageReferences</span><span class="sxs-lookup"><span data-stu-id="d612c-120">Using PackageReference for a project with no PackageReferences</span></span>

<span data-ttu-id="d612c-121">Upřesnit: Pokud nemáte v projektu nainstalované žádné balíčky (žádné PackageReferences v souboru projektu a žádný soubor Packages. config), ale chcete, aby se projekt obnovil jako PackageReferenceový styl, můžete nastavit RestoreProjectStyle vlastností projektu na PackageReference. soubor projektu.</span><span class="sxs-lookup"><span data-stu-id="d612c-121">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="d612c-122">To může být užitečné, pokud odkazujete na projekty, které jsou PackageReference styly (existující projekty csproj nebo sady SDK).</span><span class="sxs-lookup"><span data-stu-id="d612c-122">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="d612c-123">Tím umožníte, aby balíčky, na které tyto projekty odkazují, byly "transitně" odkazovány vaším projektem.</span><span class="sxs-lookup"><span data-stu-id="d612c-123">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="packagereference-and-sources"></a><span data-ttu-id="d612c-124">PackageReference a zdroje</span><span class="sxs-lookup"><span data-stu-id="d612c-124">PackageReference and sources</span></span>

<span data-ttu-id="d612c-125">V projektech PackageReference se v době obnovení vyřeší verze přenosných závislostí.</span><span class="sxs-lookup"><span data-stu-id="d612c-125">In PackageReference projects, the transitive dependency versions are resolved at restore time.</span></span> <span data-ttu-id="d612c-126">V takovém případě musí být v projektech PackageReference k dispozici všechny zdroje pro všechna obnovení.</span><span class="sxs-lookup"><span data-stu-id="d612c-126">As such, in PackageReference projects all sources need to be available for all restores.</span></span> 

## <a name="floating-versions"></a><span data-ttu-id="d612c-127">Plovoucí verze</span><span class="sxs-lookup"><span data-stu-id="d612c-127">Floating Versions</span></span>

<span data-ttu-id="d612c-128">V `PackageReference`jsou podporovány [plovoucí verze](../concepts/dependency-resolution.md#floating-versions) :</span><span class="sxs-lookup"><span data-stu-id="d612c-128">[Floating versions](../concepts/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="d612c-129">Řízení prostředků závislosti</span><span class="sxs-lookup"><span data-stu-id="d612c-129">Controlling dependency assets</span></span>

<span data-ttu-id="d612c-130">Je možné, že použijete závislost čistě jako ve vývojovém prostředí a nechcete ji vystavit pro projekty, které budou spotřebovávat váš balíček.</span><span class="sxs-lookup"><span data-stu-id="d612c-130">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="d612c-131">V tomto scénáři můžete k řízení tohoto chování použít metadata `PrivateAssets`.</span><span class="sxs-lookup"><span data-stu-id="d612c-131">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="d612c-132">Následující Tagy metadat řídí prostředky závislostí:</span><span class="sxs-lookup"><span data-stu-id="d612c-132">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="d612c-133">Značka</span><span class="sxs-lookup"><span data-stu-id="d612c-133">Tag</span></span> | <span data-ttu-id="d612c-134">Popis</span><span class="sxs-lookup"><span data-stu-id="d612c-134">Description</span></span> | <span data-ttu-id="d612c-135">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="d612c-135">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d612c-136">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="d612c-136">IncludeAssets</span></span> | <span data-ttu-id="d612c-137">Tyto prostředky budou spotřebovány.</span><span class="sxs-lookup"><span data-stu-id="d612c-137">These assets will be consumed</span></span> | <span data-ttu-id="d612c-138">vše</span><span class="sxs-lookup"><span data-stu-id="d612c-138">all</span></span> |
| <span data-ttu-id="d612c-139">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="d612c-139">ExcludeAssets</span></span> | <span data-ttu-id="d612c-140">Tyto prostředky nebudou spotřebovány.</span><span class="sxs-lookup"><span data-stu-id="d612c-140">These assets will not be consumed</span></span> | <span data-ttu-id="d612c-141">žádná</span><span class="sxs-lookup"><span data-stu-id="d612c-141">none</span></span> |
| <span data-ttu-id="d612c-142">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="d612c-142">PrivateAssets</span></span> | <span data-ttu-id="d612c-143">Tyto prostředky budou spotřebovány, ale nebudou se přesměrovat do nadřazeného projektu.</span><span class="sxs-lookup"><span data-stu-id="d612c-143">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="d612c-144">contentFiles; analyzátory; sestavit</span><span class="sxs-lookup"><span data-stu-id="d612c-144">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="d612c-145">Přípustné hodnoty pro tyto značky jsou následující, s více hodnotami oddělenými středníkem s výjimkou `all` a `none`, které se musí objevit sami:</span><span class="sxs-lookup"><span data-stu-id="d612c-145">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="d612c-146">Hodnota</span><span class="sxs-lookup"><span data-stu-id="d612c-146">Value</span></span> | <span data-ttu-id="d612c-147">Popis</span><span class="sxs-lookup"><span data-stu-id="d612c-147">Description</span></span> |
| --- | ---
| <span data-ttu-id="d612c-148">kompilovat</span><span class="sxs-lookup"><span data-stu-id="d612c-148">compile</span></span> | <span data-ttu-id="d612c-149">Obsah složky `lib` a určuje, zda je projekt kompilován proti sestavením v rámci složky</span><span class="sxs-lookup"><span data-stu-id="d612c-149">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="d612c-150">modul runtime</span><span class="sxs-lookup"><span data-stu-id="d612c-150">runtime</span></span> | <span data-ttu-id="d612c-151">Obsah `lib` a `runtimes` složky a určuje, zda budou tato sestavení zkopírována do výstupního adresáře sestavení</span><span class="sxs-lookup"><span data-stu-id="d612c-151">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="d612c-152">contentFiles</span><span class="sxs-lookup"><span data-stu-id="d612c-152">contentFiles</span></span> | <span data-ttu-id="d612c-153">Obsah složky `contentfiles`</span><span class="sxs-lookup"><span data-stu-id="d612c-153">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="d612c-154">Sestavení</span><span class="sxs-lookup"><span data-stu-id="d612c-154">build</span></span> | <span data-ttu-id="d612c-155">`.props` a `.targets` ve složce `build`</span><span class="sxs-lookup"><span data-stu-id="d612c-155">`.props` and `.targets` in the `build` folder</span></span> |
| <span data-ttu-id="d612c-156">buildMultitargeting</span><span class="sxs-lookup"><span data-stu-id="d612c-156">buildMultitargeting</span></span> | <span data-ttu-id="d612c-157">*(4,0)* `.props` a `.targets` ve složce `buildMultitargeting` pro cílení na různé architektury</span><span class="sxs-lookup"><span data-stu-id="d612c-157">*(4.0)* `.props` and `.targets` in the `buildMultitargeting` folder, for cross-framework targeting</span></span> |
| <span data-ttu-id="d612c-158">buildTransitive</span><span class="sxs-lookup"><span data-stu-id="d612c-158">buildTransitive</span></span> | <span data-ttu-id="d612c-159">*(5.0 +)* `.props` a `.targets` ve složce `buildTransitive` pro prostředky, jejichž přenos do libovolného náročného projektu probíhá.</span><span class="sxs-lookup"><span data-stu-id="d612c-159">*(5.0+)* `.props` and `.targets` in the `buildTransitive` folder, for assets that flow transitively to any consuming project.</span></span> <span data-ttu-id="d612c-160">Podívejte se na stránku [funkce](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) .</span><span class="sxs-lookup"><span data-stu-id="d612c-160">See the [feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) page.</span></span> |
| <span data-ttu-id="d612c-161">analyzátory</span><span class="sxs-lookup"><span data-stu-id="d612c-161">analyzers</span></span> | <span data-ttu-id="d612c-162">Analyzátory .NET</span><span class="sxs-lookup"><span data-stu-id="d612c-162">.NET analyzers</span></span> |
| <span data-ttu-id="d612c-163">nativní</span><span class="sxs-lookup"><span data-stu-id="d612c-163">native</span></span> | <span data-ttu-id="d612c-164">Obsah složky `native`</span><span class="sxs-lookup"><span data-stu-id="d612c-164">Contents of the `native` folder</span></span> |
| <span data-ttu-id="d612c-165">žádná</span><span class="sxs-lookup"><span data-stu-id="d612c-165">none</span></span> | <span data-ttu-id="d612c-166">Žádná z výše uvedených verzí se nepoužívá.</span><span class="sxs-lookup"><span data-stu-id="d612c-166">None of the above are used.</span></span> |
| <span data-ttu-id="d612c-167">vše</span><span class="sxs-lookup"><span data-stu-id="d612c-167">all</span></span> | <span data-ttu-id="d612c-168">Všechny výše uvedené (kromě `none`)</span><span class="sxs-lookup"><span data-stu-id="d612c-168">All of the above (except `none`)</span></span> |

<span data-ttu-id="d612c-169">V následujícím příkladu je vše kromě souborů obsahu z balíčku spotřebováno projektem a vše kromě souborů obsahu a analyzátory by vedlo k nadřazenému projektu.</span><span class="sxs-lookup"><span data-stu-id="d612c-169">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="d612c-170">Vzhledem k tomu, že `build` není zahrnuta v `PrivateAssets`, cíle a props *budou* tok do nadřazeného projektu.</span><span class="sxs-lookup"><span data-stu-id="d612c-170">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="d612c-171">Vezměte v úvahu například, že odkaz výše se používá v projektu, který vytváří balíček NuGet s názvem AppLogger.</span><span class="sxs-lookup"><span data-stu-id="d612c-171">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="d612c-172">AppLogger může využívat cíle a props z `Contoso.Utility.UsefulStuff`, jako mohou projekty, které využívají AppLogger.</span><span class="sxs-lookup"><span data-stu-id="d612c-172">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

> [!NOTE]
> <span data-ttu-id="d612c-173">Pokud je `developmentDependency` nastaveno na `true` v souboru `.nuspec`, tento balíček označí jako závislost jenom pro vývoj, což zabrání v zahrnutí balíčku jako závislosti v jiných balíčcích.</span><span class="sxs-lookup"><span data-stu-id="d612c-173">When `developmentDependency` is set to `true` in a `.nuspec` file, this marks a package as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="d612c-174">Pomocí PackageReference *(NuGet 4,8 +)* tento příznak také znamená, že vyloučí prostředky při kompilaci z kompilace.</span><span class="sxs-lookup"><span data-stu-id="d612c-174">With PackageReference *(NuGet 4.8+)*, this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="d612c-175">Další informace najdete v tématu [Podpora DevelopmentDependency pro PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span><span class="sxs-lookup"><span data-stu-id="d612c-175">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="d612c-176">Přidání podmínky PackageReference</span><span class="sxs-lookup"><span data-stu-id="d612c-176">Adding a PackageReference condition</span></span>

<span data-ttu-id="d612c-177">Podmínku můžete použít k určení, zda je balíček zahrnut, kde podmínky mohou používat jakoukoli proměnnou MSBuild nebo proměnnou definovanou v souboru TARGETS nebo props.</span><span class="sxs-lookup"><span data-stu-id="d612c-177">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="d612c-178">V současné době je však podporována pouze proměnná `TargetFramework`.</span><span class="sxs-lookup"><span data-stu-id="d612c-178">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="d612c-179">Řekněme například, že cílíte `netstandard1.4` a také `net452`, ale máte závislost, která je platná pouze pro `net452`.</span><span class="sxs-lookup"><span data-stu-id="d612c-179">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="d612c-180">V takovém případě nechcete, aby `netstandard1.4` projekt, který váš balíček spotřebovává, přidal tuto nepotřebnou závislost.</span><span class="sxs-lookup"><span data-stu-id="d612c-180">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="d612c-181">Tomu zabráníte zadáním podmínky v `PackageReference` následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="d612c-181">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="d612c-182">Balíček sestavený pomocí tohoto projektu zobrazí, že Newtonsoft. JSON je obsažen pouze jako závislost pro cíl `net452`:</span><span class="sxs-lookup"><span data-stu-id="d612c-182">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![Výsledek použití podmínky v PackageReference s VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="d612c-184">Podmínky lze také použít na úrovni `ItemGroup` a budou platit pro všechny podřízené `PackageReference` prvky:</span><span class="sxs-lookup"><span data-stu-id="d612c-184">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="locking-dependencies"></a><span data-ttu-id="d612c-185">Uzamykání závislostí</span><span class="sxs-lookup"><span data-stu-id="d612c-185">Locking dependencies</span></span>
<span data-ttu-id="d612c-186">*Tato funkce je k dispozici pro NuGet **4,9** nebo vyšší a pro Visual Studio 2017 **15,9** nebo vyšší.*</span><span class="sxs-lookup"><span data-stu-id="d612c-186">*This feature is available with NuGet **4.9** or above and with Visual Studio 2017 **15.9** or above.*</span></span>

<span data-ttu-id="d612c-187">Vstup do obnovení NuGet je sada odkazů na balíčky ze souboru projektu (závislosti na nejvyšší úrovni nebo přímých závislostí) a výstup je plný uzávěr všech závislostí balíčku včetně přenosných závislostí.</span><span class="sxs-lookup"><span data-stu-id="d612c-187">Input to NuGet restore is a set of Package References from the project file (top-level or direct dependencies) and the output is a full closure of all the package dependencies including transitive dependencies.</span></span> <span data-ttu-id="d612c-188">V případě, že se vstupní seznam PackageReference nezměnil, nástroj NuGet se pokusí vždy vydávat stejný plný uzávěr závislostí balíčku.</span><span class="sxs-lookup"><span data-stu-id="d612c-188">NuGet tries to always produce the same full closure of package dependencies if the input PackageReference list has not changed.</span></span> <span data-ttu-id="d612c-189">Existují však situace, kdy to není možné.</span><span class="sxs-lookup"><span data-stu-id="d612c-189">However, there are some scenarios where it is unable to do so.</span></span> <span data-ttu-id="d612c-190">Příklad:</span><span class="sxs-lookup"><span data-stu-id="d612c-190">For example:</span></span>

* <span data-ttu-id="d612c-191">Když použijete plovoucí verze, jako je `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span><span class="sxs-lookup"><span data-stu-id="d612c-191">When you use floating versions like `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span></span> <span data-ttu-id="d612c-192">I když tady je tento záměr na nejnovější verzi v každé obnovy balíčků, existují situace, kdy uživatelé potřebují, aby byl graf uzamčený na určitou nejnovější verzi a aby byl na novější verzi, pokud je k dispozici, po explicitním gestu.</span><span class="sxs-lookup"><span data-stu-id="d612c-192">While the intention here is to float to the latest version on every restore of packages, there are scenarios where users require the graph to be locked to a certain latest version and float to a later version, if available, upon an explicit gesture.</span></span>
* <span data-ttu-id="d612c-193">Je publikovaná novější verze balíčku, která odpovídá požadavkům verze PackageReference.</span><span class="sxs-lookup"><span data-stu-id="d612c-193">A newer version of the package matching PackageReference version requirements is published.</span></span> <span data-ttu-id="d612c-194">Například</span><span class="sxs-lookup"><span data-stu-id="d612c-194">E.g.</span></span> 

  * <span data-ttu-id="d612c-195">Den 1: Pokud jste zadali `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` ale verze, které jsou k dispozici v úložištích NuGet, byly 4.1.0, 4.2.0 a 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="d612c-195">Day 1: if you specified `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` but the versions available on the NuGet repositories were 4.1.0, 4.2.0 and 4.3.0.</span></span> <span data-ttu-id="d612c-196">V tomto případě se NuGet přeložil na 4.1.0 (nejbližší minimální verzi).</span><span class="sxs-lookup"><span data-stu-id="d612c-196">In this case, NuGet would have resolved to  4.1.0 (nearest minimum version)</span></span>

  * <span data-ttu-id="d612c-197">Den 2: verze 4.0.0 se publikuje.</span><span class="sxs-lookup"><span data-stu-id="d612c-197">Day 2: Version 4.0.0 gets published.</span></span> <span data-ttu-id="d612c-198">NuGet teď najde přesnou shodu a začne řešit na 4.0.0</span><span class="sxs-lookup"><span data-stu-id="d612c-198">NuGet will now find the exact match and start resolving to 4.0.0</span></span>

* <span data-ttu-id="d612c-199">Daná verze balíčku se odebere z úložiště.</span><span class="sxs-lookup"><span data-stu-id="d612c-199">A given package version is removed from the repository.</span></span> <span data-ttu-id="d612c-200">I když nuget.org nepovoluje odstraňování balíčků, ne všechna úložiště balíčků mají tato omezení.</span><span class="sxs-lookup"><span data-stu-id="d612c-200">Though nuget.org does not allow package deletions, not all package repositories have this constraints.</span></span> <span data-ttu-id="d612c-201">Výsledkem je, že NuGet najde nejlepší shodu, když ho nelze vyřešit na odstraněnou verzi.</span><span class="sxs-lookup"><span data-stu-id="d612c-201">This results in NuGet finding the best match when it cannot resolve to the deleted version.</span></span>

### <a name="enabling-lock-file"></a><span data-ttu-id="d612c-202">Povoluje se soubor zámku.</span><span class="sxs-lookup"><span data-stu-id="d612c-202">Enabling lock file</span></span>
<span data-ttu-id="d612c-203">Aby bylo možné zachovat úplný konec závislostí balíčku, můžete se přihlásit k funkci zámek souboru nastavením vlastnosti MSBuild `RestorePackagesWithLockFile` pro váš projekt:</span><span class="sxs-lookup"><span data-stu-id="d612c-203">In order to persist the full closure of package dependencies you can opt-in to the lock file feature by setting the MSBuild property `RestorePackagesWithLockFile` for your project:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="d612c-204">Pokud je tato vlastnost nastavená, obnovení NuGet vygeneruje soubor zámku File-`packages.lock.json` v kořenovém adresáři projektu, který obsahuje seznam všech závislostí balíčku.</span><span class="sxs-lookup"><span data-stu-id="d612c-204">If this property is set, NuGet restore will generate a lock file - `packages.lock.json` file at the project root directory that lists all the package dependencies.</span></span> 

> [!Note]
> <span data-ttu-id="d612c-205">Jakmile má projekt `packages.lock.json` soubor ve svém kořenovém adresáři, soubor zámku se vždy používá s obnovením i v případě, že vlastnost `RestorePackagesWithLockFile` není nastavena.</span><span class="sxs-lookup"><span data-stu-id="d612c-205">Once a project has `packages.lock.json` file in its root directory, the lock file is always used with restore even if the property `RestorePackagesWithLockFile` is not set.</span></span> <span data-ttu-id="d612c-206">Další možností, jak se vyjádřit k této funkci, je vytvořit v kořenovém adresáři projektu fiktivní prázdný `packages.lock.json` soubor.</span><span class="sxs-lookup"><span data-stu-id="d612c-206">So another way to opt-in to this feature is to create a dummy blank `packages.lock.json` file in the project's root directory.</span></span>

### <a name="restore-behavior-with-lock-file"></a><span data-ttu-id="d612c-207">chování `restore` se souborem zámku</span><span class="sxs-lookup"><span data-stu-id="d612c-207">`restore` behavior with lock file</span></span>
<span data-ttu-id="d612c-208">Pokud je soubor zámku k dispozici pro projekt, NuGet použije tento soubor zámku ke spuštění `restore`.</span><span class="sxs-lookup"><span data-stu-id="d612c-208">If a lock file is present for project, NuGet uses this lock file to run `restore`.</span></span> <span data-ttu-id="d612c-209">NuGet provede rychlou kontrolu, jestli se v závislostech balíčku nezměnily žádné změny, jak je uvedeno v souboru projektu (nebo v souborech závislých projektů) a jestli nedošlo k žádným změnám, jenom obnoví balíčky uvedené v souboru zámku.</span><span class="sxs-lookup"><span data-stu-id="d612c-209">NuGet does a quick check to see if there were any changes in the package dependencies as mentioned in the project file (or dependent projects' files) and if there were no changes it just restores the packages mentioned in the lock file.</span></span> <span data-ttu-id="d612c-210">Nedošlo k opakovanému vyhodnocení závislostí balíčku.</span><span class="sxs-lookup"><span data-stu-id="d612c-210">There is no re-evaluation of package dependencies.</span></span>

<span data-ttu-id="d612c-211">Pokud NuGet detekuje změnu v definovaných závislostech, jak je uvedeno v souborech projektu, znovu vyhodnotí graf balíčku a aktualizuje soubor zámku tak, aby odrážel nový uzavření balíčku pro daný projekt.</span><span class="sxs-lookup"><span data-stu-id="d612c-211">If NuGet detects a change in the defined dependencies as mentioned in the project file(s), it re-evaluates the package graph and updates the lock file to reflect the new package closure for the project.</span></span>

<span data-ttu-id="d612c-212">V případě CI/CD a dalších scénářů, kde byste nechtěli změnit závislosti balíčku, můžete tak učinit nastavením `lockedmode` na `true`:</span><span class="sxs-lookup"><span data-stu-id="d612c-212">For CI/CD and other scenarios, where you would not want to change the package dependencies on the fly, you can do so by setting the `lockedmode` to `true`:</span></span>

<span data-ttu-id="d612c-213">Pro příkaz dotnet. exe spusťte:</span><span class="sxs-lookup"><span data-stu-id="d612c-213">For dotnet.exe, run:</span></span>

```
> dotnet.exe restore --locked-mode
```

<span data-ttu-id="d612c-214">Pro MSBuild. exe spusťte:</span><span class="sxs-lookup"><span data-stu-id="d612c-214">For msbuild.exe, run:</span></span>

```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

<span data-ttu-id="d612c-215">Tuto vlastnost podmíněného MSBuild můžete nastavit také v souboru projektu:</span><span class="sxs-lookup"><span data-stu-id="d612c-215">You may also set this conditional MSBuild property in your project file:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

<span data-ttu-id="d612c-216">Pokud je `true`uzamčený režim, obnovení obnoví buď přesné balíčky uvedené v souboru zámku, nebo selže, pokud jste aktualizovali definované závislosti balíčků pro projekt po vytvoření souboru zámku.</span><span class="sxs-lookup"><span data-stu-id="d612c-216">If locked mode is `true`, restore will either restore the exact packages as listed in the lock file or fail if you updated the defined package dependencies for the project after lock file was created.</span></span>

### <a name="make-lock-file-part-of-your-source-repository"></a><span data-ttu-id="d612c-217">Nastavit zámek souboru jako součást zdrojového úložiště</span><span class="sxs-lookup"><span data-stu-id="d612c-217">Make lock file part of your source repository</span></span>
<span data-ttu-id="d612c-218">Pokud vytváříte aplikaci, spustitelný soubor a příslušný projekt jsou na začátku řetězu závislostí a pak proveďte vrácení souboru se zámkem do úložiště zdrojového kódu, aby jej mohla aplikace NuGet využít při obnovení.</span><span class="sxs-lookup"><span data-stu-id="d612c-218">If you are building an application, an executable and the project in question is at the start of the dependency chain then do check in the lock file to the source code repository so that NuGet can make use of it during restore.</span></span>

<span data-ttu-id="d612c-219">Pokud je však projekt knihovnou projektu, který nedodáte nebo se jedná o běžný projekt kódu, na kterém jsou závislé další projekty, **neměli byste** soubory zámku vrátit se změnami jako součást zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="d612c-219">However, if your project is a library project that you do not ship or a common code project on which other projects depend upon, you **should not** check in the lock file as part of your source code.</span></span> <span data-ttu-id="d612c-220">Neexistuje žádný škodný soubor zámku, ale nelze použít uzamčené závislosti balíčku pro běžný projekt kódu, jak je uvedeno v souboru zámku během obnovení nebo sestavení projektu, který je závislý na tomto projektu Common-Code.</span><span class="sxs-lookup"><span data-stu-id="d612c-220">There is no harm in keeping the lock file but the locked package dependencies for the common code project may not be used, as listed in the lock file, during the restore/build of a project that depends on this common-code project.</span></span>

<span data-ttu-id="d612c-221">Např.</span><span class="sxs-lookup"><span data-stu-id="d612c-221">Eg.</span></span>

```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```

<span data-ttu-id="d612c-222">Pokud má `ProjectA` závislost na `PackageX` verzi `2.0.0` a také odkazuje `ProjectB`, které jsou závislé na `PackageX` verze `1.0.0`, pak soubor zámku pro `ProjectB` zobrazí závislost na `PackageX` verze `1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="d612c-222">If `ProjectA` has a dependency on a `PackageX` version `2.0.0` and also references `ProjectB` that depends on `PackageX` version `1.0.0`, then the lock file for `ProjectB` will list a dependency on `PackageX` version `1.0.0`.</span></span> <span data-ttu-id="d612c-223">Pokud je však `ProjectA` sestaven, jeho soubor zámku bude obsahovat závislost na `PackageX` verze **`2.0.0`** **a `1.0.0`, jak** je uvedeno v souboru zámku pro `ProjectB`.</span><span class="sxs-lookup"><span data-stu-id="d612c-223">However, when `ProjectA` is built, its lock file will contain a dependency on `PackageX` version **`2.0.0`** and **not** `1.0.0` as listed in the lock file for `ProjectB`.</span></span> <span data-ttu-id="d612c-224">Proto soubor zámku pro běžný projekt kódu trochu říká, že balíčky byly vyřešeny pro projekty, které jsou na ní závislé.</span><span class="sxs-lookup"><span data-stu-id="d612c-224">Thus, the lock file of a common code project has little say over the packages resolved for projects that depend on it.</span></span>

### <a name="lock-file-extensibility"></a><span data-ttu-id="d612c-225">Zamknout rozšíření souboru</span><span class="sxs-lookup"><span data-stu-id="d612c-225">Lock file extensibility</span></span>

<span data-ttu-id="d612c-226">Můžete řídit různá chování při obnovení pomocí souboru zámku, jak je popsáno níže:</span><span class="sxs-lookup"><span data-stu-id="d612c-226">You can control various behaviors of restore with lock file as described below:</span></span>

| <span data-ttu-id="d612c-227">Možnost</span><span class="sxs-lookup"><span data-stu-id="d612c-227">Option</span></span> | <span data-ttu-id="d612c-228">Možnost ekvivalentu MSBuild</span><span class="sxs-lookup"><span data-stu-id="d612c-228">MSBuild equivalent option</span></span> | <span data-ttu-id="d612c-229">Popis</span><span class="sxs-lookup"><span data-stu-id="d612c-229">Description</span></span>|
|:---  |:--- |:--- |
| `--use-lock-file` | <span data-ttu-id="d612c-230">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="d612c-230">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="d612c-231">Výslovný se na použití souboru zámku.</span><span class="sxs-lookup"><span data-stu-id="d612c-231">Opts into the usage of a lock file.</span></span> | 
| `--locked-mode` | <span data-ttu-id="d612c-232">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="d612c-232">RestoreLockedMode</span></span> | <span data-ttu-id="d612c-233">Zapne uzamčený režim pro obnovení.</span><span class="sxs-lookup"><span data-stu-id="d612c-233">Enables locked mode for restore.</span></span> <span data-ttu-id="d612c-234">To je užitečné ve scénářích CI/CD, kde chcete opakovat sestavení.</span><span class="sxs-lookup"><span data-stu-id="d612c-234">This is useful in CI/CD scenarios where you want repeatable builds.</span></span>|   
| `--force-evaluate` | <span data-ttu-id="d612c-235">RestoreForceEvaluate</span><span class="sxs-lookup"><span data-stu-id="d612c-235">RestoreForceEvaluate</span></span> | <span data-ttu-id="d612c-236">Tato možnost je užitečná pro balíčky s plovoucí verzí definovanou v projektu.</span><span class="sxs-lookup"><span data-stu-id="d612c-236">This option is useful with packages with floating version defined in the project.</span></span> <span data-ttu-id="d612c-237">Ve výchozím nastavení při obnovení NuGet nebude automaticky aktualizovat verzi balíčku pro každé obnovení, pokud u této možnosti nespustíte příkaz Restore.</span><span class="sxs-lookup"><span data-stu-id="d612c-237">By default, NuGet restore will not update the package version automatically upon each restore unless you run restore with this option.</span></span> |
| `--lock-file-path` | <span data-ttu-id="d612c-238">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="d612c-238">NuGetLockFilePath</span></span> | <span data-ttu-id="d612c-239">Definuje vlastní umístění souboru zámku pro projekt.</span><span class="sxs-lookup"><span data-stu-id="d612c-239">Defines a custom lock file location for a project.</span></span> <span data-ttu-id="d612c-240">Ve výchozím nastavení NuGet podporuje `packages.lock.json` v kořenovém adresáři.</span><span class="sxs-lookup"><span data-stu-id="d612c-240">By default, NuGet supports `packages.lock.json` at the root directory.</span></span> <span data-ttu-id="d612c-241">Pokud máte ve stejném adresáři více projektů, NuGet podporuje soubor zámku určený pro projekt `packages.<project_name>.lock.json`</span><span class="sxs-lookup"><span data-stu-id="d612c-241">If you have multiple projects in the same directory, NuGet supports project specific lock file `packages.<project_name>.lock.json`</span></span> |
