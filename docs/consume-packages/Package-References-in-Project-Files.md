---
title: Formát NuGet PackageReference (odkazy na balíčky v souborech projektu)
description: Podrobnosti o NuGet PackageReference v souborech projektu, které podporuje NuGet 4.0 + a VS2017 a .NET Core 2,0
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: ae80206117eed639140a0c7977043d8330bc37bb
ms.sourcegitcommit: 80cf99f40759911324468be1ec815c96aebf376d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/17/2019
ms.locfileid: "69564563"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="898ff-103">Odkazy na balíčky (PackageReference) v souborech projektu</span><span class="sxs-lookup"><span data-stu-id="898ff-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="898ff-104">Odkazy na balíčky, použití `PackageReference` uzlu, Správa závislostí NuGet přímo v souborech projektu (na rozdíl od samostatného `packages.config` souboru).</span><span class="sxs-lookup"><span data-stu-id="898ff-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="898ff-105">Použití PackageReference, jak je voláno, nemá vliv na jiné aspekty NuGet; například nastavení v `NuGet.config` souborech (včetně zdrojů balíčků) jsou stále aplikována, jak je vysvětleno v tématu [běžné konfigurace NuGet](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="898ff-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.config` files (including package sources) are still applied as explained in [Common NuGet configurations](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="898ff-106">Pomocí PackageReference můžete také použít podmínky nástroje MSBuild k výběru odkazů na balíčky v rámci cílové architektury, konfigurace, platformy nebo dalších seskupení.</span><span class="sxs-lookup"><span data-stu-id="898ff-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="898ff-107">Umožňuje také jemně odstupňovanou kontrolu nad závislostmi a tokem obsahu.</span><span class="sxs-lookup"><span data-stu-id="898ff-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="898ff-108">(Další podrobnosti najdete v tématu Další informace o [sadě NuGet Pack a obnovení jako cíle MSBuild](../reference/msbuild-targets.md).)</span><span class="sxs-lookup"><span data-stu-id="898ff-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

## <a name="project-type-support"></a><span data-ttu-id="898ff-109">Podpora typu projektu</span><span class="sxs-lookup"><span data-stu-id="898ff-109">Project type support</span></span>

<span data-ttu-id="898ff-110">Ve výchozím nastavení se PackageReference používá pro projekty .NET Core, .NET Standard projekty a projekty UWP cílené na Windows 10 Build 15063 (Creators Update) a novější, s výjimkou C++ projektů UWP.</span><span class="sxs-lookup"><span data-stu-id="898ff-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="898ff-111">Projekty .NET Framework podporují PackageReference, ale aktuálně mají `packages.config`výchozí hodnotu.</span><span class="sxs-lookup"><span data-stu-id="898ff-111">.NET Framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="898ff-112">Chcete-li použít [](../consume-packages/migrate-packages-config-to-package-reference.md) PackageReference, migrujte `packages.config` závislosti z nástroje do souboru projektu a pak odeberte soubor Packages. config.</span><span class="sxs-lookup"><span data-stu-id="898ff-112">To use PackageReference, [migrate](../consume-packages/migrate-packages-config-to-package-reference.md) the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

<span data-ttu-id="898ff-113">ASP.NET aplikace, které cílí na úplné .NET Framework, zahrnují jenom [omezené podpory](https://github.com/NuGet/Home/issues/5877) pro PackageReference.</span><span class="sxs-lookup"><span data-stu-id="898ff-113">ASP.NET apps targeting the full .NET Framework include only [limited support](https://github.com/NuGet/Home/issues/5877) for PackageReference.</span></span> <span data-ttu-id="898ff-114">C++a typy projektů JavaScriptu nejsou podporovány.</span><span class="sxs-lookup"><span data-stu-id="898ff-114">C++ and JavaScript project types are unsupported.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="898ff-115">Přidání PackageReference</span><span class="sxs-lookup"><span data-stu-id="898ff-115">Adding a PackageReference</span></span>

<span data-ttu-id="898ff-116">Přidejte závislost do souboru projektu pomocí následující syntaxe:</span><span class="sxs-lookup"><span data-stu-id="898ff-116">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="898ff-117">Řízení verze závislosti</span><span class="sxs-lookup"><span data-stu-id="898ff-117">Controlling dependency version</span></span>

<span data-ttu-id="898ff-118">Konvence pro určení verze balíčku je stejná jako při použití `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="898ff-118">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="898ff-119">V příkladu výše 3.6.0 označuje všechny verze, které jsou > = 3.6.0 s upřednostněním pro nejnižší verzi, jak je popsáno v tématu [Správa verzí balíčků](../concepts/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="898ff-119">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../concepts/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="898ff-120">Použití PackageReference pro projekt bez PackageReferences</span><span class="sxs-lookup"><span data-stu-id="898ff-120">Using PackageReference for a project with no PackageReferences</span></span>
<span data-ttu-id="898ff-121">Upřesnit Pokud nemáte v projektu nainstalované žádné balíčky (žádné PackageReferences v souboru projektu a žádný soubor Packages. config), ale chcete, aby se projekt obnovil jako PackageReferenceový styl, můžete nastavit vlastnost projektu RestoreProjectStyle na PackageReference v projektu. souborů.</span><span class="sxs-lookup"><span data-stu-id="898ff-121">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
<span data-ttu-id="898ff-122">To může být užitečné, pokud odkazujete na projekty, které jsou PackageReference styly (existující projekty csproj nebo sady SDK).</span><span class="sxs-lookup"><span data-stu-id="898ff-122">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="898ff-123">Tím umožníte, aby balíčky, na které tyto projekty odkazují, byly "transitně" odkazovány vaším projektem.</span><span class="sxs-lookup"><span data-stu-id="898ff-123">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="floating-versions"></a><span data-ttu-id="898ff-124">Plovoucí verze</span><span class="sxs-lookup"><span data-stu-id="898ff-124">Floating Versions</span></span>

<span data-ttu-id="898ff-125">[Plovoucí verze](../concepts/dependency-resolution.md#floating-versions) jsou podporované pomocí `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="898ff-125">[Floating versions](../concepts/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="898ff-126">Řízení prostředků závislosti</span><span class="sxs-lookup"><span data-stu-id="898ff-126">Controlling dependency assets</span></span>

<span data-ttu-id="898ff-127">Je možné, že použijete závislost čistě jako ve vývojovém prostředí a nechcete ji vystavit pro projekty, které budou spotřebovávat váš balíček.</span><span class="sxs-lookup"><span data-stu-id="898ff-127">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="898ff-128">V tomto scénáři můžete k řízení tohoto chování `PrivateAssets` použít metadata.</span><span class="sxs-lookup"><span data-stu-id="898ff-128">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="898ff-129">Následující Tagy metadat řídí prostředky závislostí:</span><span class="sxs-lookup"><span data-stu-id="898ff-129">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="898ff-130">Značka</span><span class="sxs-lookup"><span data-stu-id="898ff-130">Tag</span></span> | <span data-ttu-id="898ff-131">Popis</span><span class="sxs-lookup"><span data-stu-id="898ff-131">Description</span></span> | <span data-ttu-id="898ff-132">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="898ff-132">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="898ff-133">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="898ff-133">IncludeAssets</span></span> | <span data-ttu-id="898ff-134">Tyto prostředky budou spotřebovány.</span><span class="sxs-lookup"><span data-stu-id="898ff-134">These assets will be consumed</span></span> | <span data-ttu-id="898ff-135">všechny</span><span class="sxs-lookup"><span data-stu-id="898ff-135">all</span></span> |
| <span data-ttu-id="898ff-136">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="898ff-136">ExcludeAssets</span></span> | <span data-ttu-id="898ff-137">Tyto prostředky nebudou spotřebovány.</span><span class="sxs-lookup"><span data-stu-id="898ff-137">These assets will not be consumed</span></span> | <span data-ttu-id="898ff-138">žádná</span><span class="sxs-lookup"><span data-stu-id="898ff-138">none</span></span> |
| <span data-ttu-id="898ff-139">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="898ff-139">PrivateAssets</span></span> | <span data-ttu-id="898ff-140">Tyto prostředky budou spotřebovány, ale nebudou se přesměrovat do nadřazeného projektu.</span><span class="sxs-lookup"><span data-stu-id="898ff-140">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="898ff-141">contentFiles; analyzátory; sestavit</span><span class="sxs-lookup"><span data-stu-id="898ff-141">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="898ff-142">Přípustné hodnoty pro tyto značky jsou následující, s více hodnotami oddělenými středníkem s výjimkou `all` a, `none` které se musí objevit sami:</span><span class="sxs-lookup"><span data-stu-id="898ff-142">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="898ff-143">Value</span><span class="sxs-lookup"><span data-stu-id="898ff-143">Value</span></span> | <span data-ttu-id="898ff-144">Popis</span><span class="sxs-lookup"><span data-stu-id="898ff-144">Description</span></span> |
| --- | ---
| <span data-ttu-id="898ff-145">sestavení</span><span class="sxs-lookup"><span data-stu-id="898ff-145">compile</span></span> | <span data-ttu-id="898ff-146">`lib` Obsah složky a určuje, zda je projekt kompilován proti sestavením v rámci složky</span><span class="sxs-lookup"><span data-stu-id="898ff-146">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="898ff-147">modul runtime</span><span class="sxs-lookup"><span data-stu-id="898ff-147">runtime</span></span> | <span data-ttu-id="898ff-148">Obsah složky `runtimes` a určuje, zda budou tato sestavení zkopírována do výstupního adresáře sestavení `lib`</span><span class="sxs-lookup"><span data-stu-id="898ff-148">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="898ff-149">contentFiles</span><span class="sxs-lookup"><span data-stu-id="898ff-149">contentFiles</span></span> | <span data-ttu-id="898ff-150">`contentfiles` Obsah složky</span><span class="sxs-lookup"><span data-stu-id="898ff-150">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="898ff-151">sestavení</span><span class="sxs-lookup"><span data-stu-id="898ff-151">build</span></span> | <span data-ttu-id="898ff-152">`.props``.targets` a`build` ve složce</span><span class="sxs-lookup"><span data-stu-id="898ff-152">`.props` and `.targets` in the `build` folder</span></span> |
| <span data-ttu-id="898ff-153">buildMultitargeting</span><span class="sxs-lookup"><span data-stu-id="898ff-153">buildMultitargeting</span></span> | <span data-ttu-id="898ff-154">*(4,0)* `.props` a `.targets` ve`buildMultitargeting` složce pro cílení na různé architektury</span><span class="sxs-lookup"><span data-stu-id="898ff-154">*(4.0)* `.props` and `.targets` in the `buildMultitargeting` folder, for cross-framework targeting</span></span> |
| <span data-ttu-id="898ff-155">buildTransitive</span><span class="sxs-lookup"><span data-stu-id="898ff-155">buildTransitive</span></span> | <span data-ttu-id="898ff-156">*(5.0 +)* `.props` a vesložce`buildTransitive` pro prostředky, jejichž přenos do libovolného náročného projektu se protéká. `.targets`</span><span class="sxs-lookup"><span data-stu-id="898ff-156">*(5.0+)* `.props` and `.targets` in the `buildTransitive` folder, for assets that flow transitively to any consuming project.</span></span> <span data-ttu-id="898ff-157">Podívejte se na stránku [funkce](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) .</span><span class="sxs-lookup"><span data-stu-id="898ff-157">See the [feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) page.</span></span> |
| <span data-ttu-id="898ff-158">analyzátory</span><span class="sxs-lookup"><span data-stu-id="898ff-158">analyzers</span></span> | <span data-ttu-id="898ff-159">Analyzátory .NET</span><span class="sxs-lookup"><span data-stu-id="898ff-159">.NET analyzers</span></span> |
| <span data-ttu-id="898ff-160">nativní</span><span class="sxs-lookup"><span data-stu-id="898ff-160">native</span></span> | <span data-ttu-id="898ff-161">`native` Obsah složky</span><span class="sxs-lookup"><span data-stu-id="898ff-161">Contents of the `native` folder</span></span> |
| <span data-ttu-id="898ff-162">žádná</span><span class="sxs-lookup"><span data-stu-id="898ff-162">none</span></span> | <span data-ttu-id="898ff-163">Žádná z výše uvedených verzí se nepoužívá.</span><span class="sxs-lookup"><span data-stu-id="898ff-163">None of the above are used.</span></span> |
| <span data-ttu-id="898ff-164">všechny</span><span class="sxs-lookup"><span data-stu-id="898ff-164">all</span></span> | <span data-ttu-id="898ff-165">Všechny výše uvedené (kromě `none`)</span><span class="sxs-lookup"><span data-stu-id="898ff-165">All of the above (except `none`)</span></span> |

<span data-ttu-id="898ff-166">V následujícím příkladu je vše kromě souborů obsahu z balíčku spotřebováno projektem a vše kromě souborů obsahu a analyzátory by vedlo k nadřazenému projektu.</span><span class="sxs-lookup"><span data-stu-id="898ff-166">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="898ff-167">Všimněte si, `build` že protože není `PrivateAssets`součástí, cíle a props *budou* tok do nadřazeného projektu.</span><span class="sxs-lookup"><span data-stu-id="898ff-167">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="898ff-168">Vezměte v úvahu například, že odkaz výše se používá v projektu, který vytváří balíček NuGet s názvem AppLogger.</span><span class="sxs-lookup"><span data-stu-id="898ff-168">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="898ff-169">AppLogger může využívat cíle a props z `Contoso.Utility.UsefulStuff`, jako mohou projekty, které využívají AppLogger.</span><span class="sxs-lookup"><span data-stu-id="898ff-169">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

> [!NOTE]
> <span data-ttu-id="898ff-170">Když `developmentDependency` je `true` v`.nuspec` souboru nastavená na, označí balíček jako součást jedinou pro vývoj, která zabrání zahrnutí balíčku jako závislosti v jiných balíčcích.</span><span class="sxs-lookup"><span data-stu-id="898ff-170">When `developmentDependency` is set to `true` in a `.nuspec` file, this marks a package as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="898ff-171">Pomocí PackageReference *(NuGet 4,8 +)* tento příznak také znamená, že vyloučí prostředky při kompilaci z kompilace.</span><span class="sxs-lookup"><span data-stu-id="898ff-171">With PackageReference *(NuGet 4.8+)*, this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="898ff-172">Další informace najdete v tématu [Podpora DevelopmentDependency pro PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span><span class="sxs-lookup"><span data-stu-id="898ff-172">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="898ff-173">Přidání podmínky PackageReference</span><span class="sxs-lookup"><span data-stu-id="898ff-173">Adding a PackageReference condition</span></span>

<span data-ttu-id="898ff-174">Podmínku můžete použít k určení, zda je balíček zahrnut, kde podmínky mohou používat jakoukoli proměnnou MSBuild nebo proměnnou definovanou v souboru TARGETS nebo props.</span><span class="sxs-lookup"><span data-stu-id="898ff-174">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="898ff-175">V předsoučasném případě je však podporována pouze `TargetFramework` proměnná.</span><span class="sxs-lookup"><span data-stu-id="898ff-175">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="898ff-176">Řekněme například, že cílíte `netstandard1.4` `net452` i na, ale máte závislost, která je platná pouze pro `net452`.</span><span class="sxs-lookup"><span data-stu-id="898ff-176">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="898ff-177">V takovém případě nechcete `netstandard1.4` , aby projekt, který váš balíček spotřebovává, přidal tuto nepotřebnou závislost.</span><span class="sxs-lookup"><span data-stu-id="898ff-177">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="898ff-178">Tomu zabráníte tak, že zadáte podmínku `PackageReference` v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="898ff-178">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="898ff-179">Balíček sestavený pomocí tohoto projektu zobrazí, že Newtonsoft. JSON je obsažen pouze jako závislost pro `net452` cíl:</span><span class="sxs-lookup"><span data-stu-id="898ff-179">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![Výsledek použití podmínky v PackageReference s VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="898ff-181">Podmínky lze také použít `ItemGroup` na úrovni a budou platit pro všechny podřízené `PackageReference` prvky:</span><span class="sxs-lookup"><span data-stu-id="898ff-181">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="locking-dependencies"></a><span data-ttu-id="898ff-182">Uzamykání závislostí</span><span class="sxs-lookup"><span data-stu-id="898ff-182">Locking dependencies</span></span>
<span data-ttu-id="898ff-183">*Tato funkce je k dispozici pro NuGet **4,9** nebo vyšší a pro Visual Studio 2017 **15,9** nebo vyšší.*</span><span class="sxs-lookup"><span data-stu-id="898ff-183">*This feature is available with NuGet **4.9** or above and with Visual Studio 2017 **15.9** or above.*</span></span>

<span data-ttu-id="898ff-184">Vstup do obnovení NuGet je sada odkazů na balíčky ze souboru projektu (závislosti na nejvyšší úrovni nebo přímých závislostí) a výstup je plný uzávěr všech závislostí balíčku včetně přenosných závislostí.</span><span class="sxs-lookup"><span data-stu-id="898ff-184">Input to NuGet restore is a set of Package References from the project file (top-level or direct dependencies) and the output is a full closure of all the package dependencies including transitive dependencies.</span></span> <span data-ttu-id="898ff-185">V případě, že se vstupní seznam PackageReference nezměnil, nástroj NuGet se pokusí vždy vydávat stejný plný uzávěr závislostí balíčku.</span><span class="sxs-lookup"><span data-stu-id="898ff-185">NuGet tries to always produce the same full closure of package dependencies if the input PackageReference list has not changed.</span></span> <span data-ttu-id="898ff-186">Existují však situace, kdy to není možné.</span><span class="sxs-lookup"><span data-stu-id="898ff-186">However, there are some scenarios where it is unable to do so.</span></span> <span data-ttu-id="898ff-187">Příklad:</span><span class="sxs-lookup"><span data-stu-id="898ff-187">For example:</span></span>

* <span data-ttu-id="898ff-188">Při použití plovoucích verzí, `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`jako je.</span><span class="sxs-lookup"><span data-stu-id="898ff-188">When you use floating versions like `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span></span> <span data-ttu-id="898ff-189">I když tady je tento záměr na nejnovější verzi v každé obnovy balíčků, existují situace, kdy uživatelé potřebují, aby byl graf uzamčený na určitou nejnovější verzi a aby byl na novější verzi, pokud je k dispozici, po explicitním gestu.</span><span class="sxs-lookup"><span data-stu-id="898ff-189">While the intention here is to float to the latest version on every restore of packages, there are scenarios where users require the graph to be locked to a certain latest version and float to a later version, if available, upon an explicit gesture.</span></span>
* <span data-ttu-id="898ff-190">Je publikovaná novější verze balíčku, která odpovídá požadavkům verze PackageReference.</span><span class="sxs-lookup"><span data-stu-id="898ff-190">A newer version of the package matching PackageReference version requirements is published.</span></span> <span data-ttu-id="898ff-191">Například</span><span class="sxs-lookup"><span data-stu-id="898ff-191">E.g.</span></span> 

  * <span data-ttu-id="898ff-192">Den 1: Pokud jste zadali `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` verze, které jsou k dispozici v úložištích NuGet, byly 4.1.0, 4.2.0 a 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="898ff-192">Day 1: if you specified `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` but the versions available on the NuGet repositories were 4.1.0, 4.2.0 and 4.3.0.</span></span> <span data-ttu-id="898ff-193">V tomto případě se NuGet přeložil na 4.1.0 (nejbližší minimální verzi).</span><span class="sxs-lookup"><span data-stu-id="898ff-193">In this case, NuGet would have resolved to  4.1.0 (nearest minimum version)</span></span>

  * <span data-ttu-id="898ff-194">Den 2: Verze 4.0.0 se publikuje.</span><span class="sxs-lookup"><span data-stu-id="898ff-194">Day 2: Version 4.0.0 gets published.</span></span> <span data-ttu-id="898ff-195">NuGet teď najde přesnou shodu a začne řešit na 4.0.0</span><span class="sxs-lookup"><span data-stu-id="898ff-195">NuGet will now find the exact match and start resolving to 4.0.0</span></span>

* <span data-ttu-id="898ff-196">Daná verze balíčku se odebere z úložiště.</span><span class="sxs-lookup"><span data-stu-id="898ff-196">A given package version is removed from the repository.</span></span> <span data-ttu-id="898ff-197">I když nuget.org nepovoluje odstraňování balíčků, ne všechna úložiště balíčků mají tato omezení.</span><span class="sxs-lookup"><span data-stu-id="898ff-197">Though nuget.org does not allow package deletions, not all package repositories have this constraints.</span></span> <span data-ttu-id="898ff-198">Výsledkem je, že NuGet najde nejlepší shodu, když ho nelze vyřešit na odstraněnou verzi.</span><span class="sxs-lookup"><span data-stu-id="898ff-198">This results in NuGet finding the best match when it cannot resolve to the deleted version.</span></span>

### <a name="enabling-lock-file"></a><span data-ttu-id="898ff-199">Povoluje se soubor zámku.</span><span class="sxs-lookup"><span data-stu-id="898ff-199">Enabling lock file</span></span>
<span data-ttu-id="898ff-200">Aby se zachoval úplný konec závislostí balíčku, můžete se přihlásit k funkci zámek souboru nastavením vlastnosti `RestorePackagesWithLockFile` MSBuild pro váš projekt:</span><span class="sxs-lookup"><span data-stu-id="898ff-200">In order to persist the full closure of package dependencies you can opt-in to the lock file feature by setting the MSBuild property `RestorePackagesWithLockFile` for your project:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="898ff-201">Pokud je tato vlastnost nastavená, obnovení NuGet vygeneruje soubor zámku File `packages.lock.json` v kořenovém adresáři projektu, který obsahuje seznam všech závislostí balíčku.</span><span class="sxs-lookup"><span data-stu-id="898ff-201">If this property is set, NuGet restore will generate a lock file - `packages.lock.json` file at the project root directory that lists all the package dependencies.</span></span> 

> [!Note]
> <span data-ttu-id="898ff-202">Jakmile projekt obsahuje `packages.lock.json` soubor ve svém kořenovém adresáři, soubor zámku se vždy používá s obnovením i v případě, `RestorePackagesWithLockFile` že vlastnost není nastavena.</span><span class="sxs-lookup"><span data-stu-id="898ff-202">Once a project has `packages.lock.json` file in its root directory, the lock file is always used with restore even if the property `RestorePackagesWithLockFile` is not set.</span></span> <span data-ttu-id="898ff-203">Další možností, jak se vyjádřit k této funkci, je vytvořit fiktivní prázdný `packages.lock.json` soubor v kořenovém adresáři projektu.</span><span class="sxs-lookup"><span data-stu-id="898ff-203">So another way to opt-in to this feature is to create a dummy blank `packages.lock.json` file in the project's root directory.</span></span>

### <a name="restore-behavior-with-lock-file"></a><span data-ttu-id="898ff-204">`restore`chování se souborem zámku</span><span class="sxs-lookup"><span data-stu-id="898ff-204">`restore` behavior with lock file</span></span>
<span data-ttu-id="898ff-205">Pokud je soubor zámku k dispozici pro projekt, nástroj NuGet používá ke spuštění `restore`tento soubor zámku.</span><span class="sxs-lookup"><span data-stu-id="898ff-205">If a lock file is present for project, NuGet uses this lock file to run `restore`.</span></span> <span data-ttu-id="898ff-206">NuGet provede rychlou kontrolu, jestli se v závislostech balíčku nezměnily žádné změny, jak je uvedeno v souboru projektu (nebo v souborech závislých projektů) a jestli nedošlo k žádným změnám, jenom obnoví balíčky uvedené v souboru zámku.</span><span class="sxs-lookup"><span data-stu-id="898ff-206">NuGet does a quick check to see if there were any changes in the package dependencies as mentioned in the project file (or dependent projects' files) and if there were no changes it just restores the packages mentioned in the lock file.</span></span> <span data-ttu-id="898ff-207">Nedošlo k opakovanému vyhodnocení závislostí balíčku.</span><span class="sxs-lookup"><span data-stu-id="898ff-207">There is no re-evaluation of package dependencies.</span></span>

<span data-ttu-id="898ff-208">Pokud NuGet detekuje změnu v definovaných závislostech, jak je uvedeno v souborech projektu, znovu vyhodnotí graf balíčku a aktualizuje soubor zámku tak, aby odrážel nový uzavření balíčku pro daný projekt.</span><span class="sxs-lookup"><span data-stu-id="898ff-208">If NuGet detects a change in the defined dependencies as mentioned in the project file(s), it re-evaluates the package graph and updates the lock file to reflect the new package closure for the project.</span></span>

<span data-ttu-id="898ff-209">V případě CI/CD a dalších scénářů, kde byste nechtěli změnit závislosti balíčku za běhu, můžete to provést nastavením `lockedmode` na: `true`</span><span class="sxs-lookup"><span data-stu-id="898ff-209">For CI/CD and other scenarios, where you would not want to change the package dependencies on the fly, you can do so by setting the `lockedmode` to `true`:</span></span>

<span data-ttu-id="898ff-210">Pro příkaz dotnet. exe spusťte:</span><span class="sxs-lookup"><span data-stu-id="898ff-210">For dotnet.exe, run:</span></span>
```
> dotnet.exe restore --locked-mode
```

<span data-ttu-id="898ff-211">Pro MSBuild. exe spusťte:</span><span class="sxs-lookup"><span data-stu-id="898ff-211">For msbuild.exe, run:</span></span>
```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

<span data-ttu-id="898ff-212">Tuto vlastnost podmíněného MSBuild můžete nastavit také v souboru projektu:</span><span class="sxs-lookup"><span data-stu-id="898ff-212">You may also set this conditional MSBuild property in your project file:</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

<span data-ttu-id="898ff-213">Pokud je `true`uzamčený režim, obnovení obnoví buď přesné balíčky uvedené v souboru zámku, nebo selže, pokud jste aktualizovali definované závislosti balíčků pro projekt po vytvoření souboru zámku.</span><span class="sxs-lookup"><span data-stu-id="898ff-213">If locked mode is `true`, restore will either restore the exact packages as listed in the lock file or fail if you updated the defined package dependencies for the project after lock file was created.</span></span>

### <a name="make-lock-file-part-of-your-source-repository"></a><span data-ttu-id="898ff-214">Nastavit zámek souboru jako součást zdrojového úložiště</span><span class="sxs-lookup"><span data-stu-id="898ff-214">Make lock file part of your source repository</span></span>
<span data-ttu-id="898ff-215">Pokud vytváříte aplikaci, spustitelný soubor a příslušný projekt jsou na začátku řetězu závislostí a pak proveďte vrácení souboru se zámkem do úložiště zdrojového kódu, aby jej mohla aplikace NuGet využít při obnovení.</span><span class="sxs-lookup"><span data-stu-id="898ff-215">If you are building an application, an executable and the project in question is at the start of the dependency chain then do check in the lock file to the source code repository so that NuGet can make use of it during restore.</span></span>

<span data-ttu-id="898ff-216">Pokud je však projekt knihovnou projektu, který nedodáte nebo se jedná o běžný projekt kódu, na kterém jsou závislé další projekty, **neměli byste** soubory zámku vrátit se změnami jako součást zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="898ff-216">However, if your project is a library project that you do not ship or a common code project on which other projects depend upon, you **should not** check in the lock file as part of your source code.</span></span> <span data-ttu-id="898ff-217">Neexistuje žádný škodný soubor zámku, ale nelze použít uzamčené závislosti balíčku pro běžný projekt kódu, jak je uvedeno v souboru zámku během obnovení nebo sestavení projektu, který je závislý na tomto projektu Common-Code.</span><span class="sxs-lookup"><span data-stu-id="898ff-217">There is no harm in keeping the lock file but the locked package dependencies for the common code project may not be used, as listed in the lock file, during the restore/build of a project that depends on this common-code project.</span></span>

<span data-ttu-id="898ff-218">EG.</span><span class="sxs-lookup"><span data-stu-id="898ff-218">Eg.</span></span>
```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```
<span data-ttu-id="898ff-219">Pokud `ProjectA` má závislost `PackageX` na verzi `2.0.0` a také odkazy `ProjectB` , které závisejí na `PackageX` verzi `1.0.0`, pak soubor zámku pro `ProjectB` bude zobrazovat závislost na `PackageX` verze `1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="898ff-219">If `ProjectA` has a dependency on a `PackageX` version `2.0.0` and also references `ProjectB` that depends on `PackageX` version `1.0.0`, then the lock file for `ProjectB` will list a dependency on `PackageX` version `1.0.0`.</span></span> <span data-ttu-id="898ff-220">Když `ProjectA` `PackageX` je však sestaven, jeho soubor zámku bude obsahovat závislost na verzi **`2.0.0`** a **nikoli** `1.0.0` , jak je uvedeno v souboru zámku pro `ProjectB`.</span><span class="sxs-lookup"><span data-stu-id="898ff-220">However, when `ProjectA` is built, its lock file will contain a dependency on `PackageX` version **`2.0.0`** and **not** `1.0.0` as listed in the lock file for `ProjectB`.</span></span> <span data-ttu-id="898ff-221">Proto soubor zámku pro běžný projekt kódu trochu říká, že balíčky byly vyřešeny pro projekty, které jsou na ní závislé.</span><span class="sxs-lookup"><span data-stu-id="898ff-221">Thus, the lock file of a common code project has little say over the packages resolved for projects that depend on it.</span></span>

### <a name="lock-file-extensibility"></a><span data-ttu-id="898ff-222">Zamknout rozšíření souboru</span><span class="sxs-lookup"><span data-stu-id="898ff-222">Lock file extensibility</span></span>
<span data-ttu-id="898ff-223">Můžete řídit různá chování při obnovení pomocí souboru zámku, jak je popsáno níže:</span><span class="sxs-lookup"><span data-stu-id="898ff-223">You can control various behaviors of restore with lock file as described below:</span></span>

| <span data-ttu-id="898ff-224">Možnost</span><span class="sxs-lookup"><span data-stu-id="898ff-224">Option</span></span> | <span data-ttu-id="898ff-225">Možnost ekvivalentu MSBuild</span><span class="sxs-lookup"><span data-stu-id="898ff-225">MSBuild equivalent option</span></span> | 
|:---  |:--- |
| `--use-lock-file` | <span data-ttu-id="898ff-226">Slouží k zavedení souboru zámku pro projekt.</span><span class="sxs-lookup"><span data-stu-id="898ff-226">Bootstraps use of lock file for a project.</span></span> <span data-ttu-id="898ff-227">Můžete také nastavit `RestorePackagesWithLockFile` vlastnost v souboru projektu</span><span class="sxs-lookup"><span data-stu-id="898ff-227">You can alternatively set `RestorePackagesWithLockFile` property in the project file</span></span> | 
| `--locked-mode` | <span data-ttu-id="898ff-228">Zapne uzamčený režim pro obnovení.</span><span class="sxs-lookup"><span data-stu-id="898ff-228">Enables locked mode for restore.</span></span> <span data-ttu-id="898ff-229">To je užitečné ve scénářích CI/CD, kde byste chtěli získat opakovaně vytvořená sestavení.</span><span class="sxs-lookup"><span data-stu-id="898ff-229">This is useful in CI/CD scenarios where you would like to get the repeatable builds.</span></span> <span data-ttu-id="898ff-230">To může být také nastavením `RestoreLockedMode` vlastnosti MSBuild na`true`</span><span class="sxs-lookup"><span data-stu-id="898ff-230">This can be also by setting the `RestoreLockedMode` MSBuild property to `true`</span></span> |  
| `--force-evaluate` | <span data-ttu-id="898ff-231">Tato možnost je užitečná pro balíčky s plovoucí verzí definovanou v projektu.</span><span class="sxs-lookup"><span data-stu-id="898ff-231">This option is useful with packages with floating version defined in the project.</span></span> <span data-ttu-id="898ff-232">Ve výchozím nastavení obnovení NuGet při každém obnovení automaticky neaktualizuje verzi balíčku, dokud nespustíte možnost obnovit `--force-evaluate` s možností.</span><span class="sxs-lookup"><span data-stu-id="898ff-232">By default, NuGet restore will not update the package version automatically upon each restore unless you run restore with `--force-evaluate` option.</span></span> |
| `--lock-file-path` | <span data-ttu-id="898ff-233">Definuje vlastní umístění souboru zámku pro projekt.</span><span class="sxs-lookup"><span data-stu-id="898ff-233">Defines a custom lock file location for a project.</span></span> <span data-ttu-id="898ff-234">To lze také dosáhnout nastavením vlastnosti `NuGetLockFilePath`MSBuild.</span><span class="sxs-lookup"><span data-stu-id="898ff-234">This can be also achieved by setting the MSBuild property `NuGetLockFilePath`.</span></span> <span data-ttu-id="898ff-235">Ve výchozím nastavení NuGet podporuje `packages.lock.json` v kořenovém adresáři.</span><span class="sxs-lookup"><span data-stu-id="898ff-235">By default, NuGet supports `packages.lock.json` at the root directory.</span></span> <span data-ttu-id="898ff-236">Pokud máte ve stejném adresáři více projektů, NuGet podporuje soubor zámku specifický pro projekt.`packages.<project_name>.lock.json`</span><span class="sxs-lookup"><span data-stu-id="898ff-236">If you have multiple projects in the same directory, NuGet supports project specific lock file `packages.<project_name>.lock.json`</span></span> |
