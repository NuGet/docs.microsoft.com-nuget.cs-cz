---
title: Formát NuGet PackageReference (odkazy na balíčky v souborech projektu)
description: Podrobnosti o NuGet PackageReference v souborech projektu, které podporuje NuGet 4.0 + a VS2017 a .NET Core 2,0
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 05ece5f36ff7ae5920960c42cfde8b271dc3e712
ms.sourcegitcommit: fc1b716afda999148eb06d62beedb350643eb346
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/14/2019
ms.locfileid: "69020014"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="e9813-103">Odkazy na balíčky (PackageReference) v souborech projektu</span><span class="sxs-lookup"><span data-stu-id="e9813-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="e9813-104">Odkazy na balíčky, použití `PackageReference` uzlu, Správa závislostí NuGet přímo v souborech projektu (na rozdíl od samostatného `packages.config` souboru).</span><span class="sxs-lookup"><span data-stu-id="e9813-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="e9813-105">Použití PackageReference, jak je voláno, nemá vliv na jiné aspekty NuGet; například nastavení v `NuGet.config` souborech (včetně zdrojů balíčků) jsou stále aplikována, jak je vysvětleno v tématu [běžné konfigurace NuGet](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="e9813-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.config` files (including package sources) are still applied as explained in [Common NuGet configurations](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="e9813-106">Pomocí PackageReference můžete také použít podmínky nástroje MSBuild k výběru odkazů na balíčky v rámci cílové architektury, konfigurace, platformy nebo dalších seskupení.</span><span class="sxs-lookup"><span data-stu-id="e9813-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="e9813-107">Umožňuje také jemně odstupňovanou kontrolu nad závislostmi a tokem obsahu.</span><span class="sxs-lookup"><span data-stu-id="e9813-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="e9813-108">(Další podrobnosti najdete v tématu Další informace o [sadě NuGet Pack a obnovení jako cíle MSBuild](../reference/msbuild-targets.md).)</span><span class="sxs-lookup"><span data-stu-id="e9813-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

## <a name="project-type-support"></a><span data-ttu-id="e9813-109">Podpora typu projektu</span><span class="sxs-lookup"><span data-stu-id="e9813-109">Project type support</span></span>

<span data-ttu-id="e9813-110">Ve výchozím nastavení se PackageReference používá pro projekty .NET Core, .NET Standard projekty a projekty UWP cílené na Windows 10 Build 15063 (Creators Update) a novější, s výjimkou C++ projektů UWP.</span><span class="sxs-lookup"><span data-stu-id="e9813-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="e9813-111">Projekty .NET Framework podporují PackageReference, ale aktuálně mají `packages.config`výchozí hodnotu.</span><span class="sxs-lookup"><span data-stu-id="e9813-111">.NET Framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="e9813-112">Chcete-li použít [](../reference/migrate-packages-config-to-package-reference.md) PackageReference, migrujte `packages.config` závislosti z nástroje do souboru projektu a pak odeberte soubor Packages. config.</span><span class="sxs-lookup"><span data-stu-id="e9813-112">To use PackageReference, [migrate](../reference/migrate-packages-config-to-package-reference.md) the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

<span data-ttu-id="e9813-113">ASP.NET aplikace, které cílí na úplné .NET Framework, zahrnují jenom [omezené podpory](https://github.com/NuGet/Home/issues/5877) pro PackageReference.</span><span class="sxs-lookup"><span data-stu-id="e9813-113">ASP.NET apps targeting the full .NET Framework include only [limited support](https://github.com/NuGet/Home/issues/5877) for PackageReference.</span></span> <span data-ttu-id="e9813-114">C++a typy projektů JavaScriptu nejsou podporovány.</span><span class="sxs-lookup"><span data-stu-id="e9813-114">C++ and JavaScript project types are unsupported.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="e9813-115">Přidání PackageReference</span><span class="sxs-lookup"><span data-stu-id="e9813-115">Adding a PackageReference</span></span>

<span data-ttu-id="e9813-116">Přidejte závislost do souboru projektu pomocí následující syntaxe:</span><span class="sxs-lookup"><span data-stu-id="e9813-116">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="e9813-117">Řízení verze závislosti</span><span class="sxs-lookup"><span data-stu-id="e9813-117">Controlling dependency version</span></span>

<span data-ttu-id="e9813-118">Konvence pro určení verze balíčku je stejná jako při použití `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="e9813-118">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="e9813-119">V příkladu výše 3.6.0 označuje všechny verze, které jsou > = 3.6.0 s upřednostněním pro nejnižší verzi, jak je popsáno v tématu [Správa verzí balíčků](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="e9813-119">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="e9813-120">Použití PackageReference pro projekt bez PackageReferences</span><span class="sxs-lookup"><span data-stu-id="e9813-120">Using PackageReference for a project with no PackageReferences</span></span>
<span data-ttu-id="e9813-121">Upřesnit Pokud nemáte v projektu nainstalované žádné balíčky (žádné PackageReferences v souboru projektu a žádný soubor Packages. config), ale chcete, aby se projekt obnovil jako PackageReferenceový styl, můžete nastavit vlastnost projektu RestoreProjectStyle na PackageReference v projektu. souborů.</span><span class="sxs-lookup"><span data-stu-id="e9813-121">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
<span data-ttu-id="e9813-122">To může být užitečné, pokud odkazujete na projekty, které jsou PackageReference styly (existující projekty csproj nebo sady SDK).</span><span class="sxs-lookup"><span data-stu-id="e9813-122">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="e9813-123">Tím umožníte, aby balíčky, na které tyto projekty odkazují, byly "transitně" odkazovány vaším projektem.</span><span class="sxs-lookup"><span data-stu-id="e9813-123">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="floating-versions"></a><span data-ttu-id="e9813-124">Plovoucí verze</span><span class="sxs-lookup"><span data-stu-id="e9813-124">Floating Versions</span></span>

<span data-ttu-id="e9813-125">[Plovoucí verze](../consume-packages/dependency-resolution.md#floating-versions) jsou podporované pomocí `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="e9813-125">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="e9813-126">Řízení prostředků závislosti</span><span class="sxs-lookup"><span data-stu-id="e9813-126">Controlling dependency assets</span></span>

<span data-ttu-id="e9813-127">Je možné, že použijete závislost čistě jako ve vývojovém prostředí a nechcete ji vystavit pro projekty, které budou spotřebovávat váš balíček.</span><span class="sxs-lookup"><span data-stu-id="e9813-127">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="e9813-128">V tomto scénáři můžete k řízení tohoto chování `PrivateAssets` použít metadata.</span><span class="sxs-lookup"><span data-stu-id="e9813-128">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="e9813-129">Následující Tagy metadat řídí prostředky závislostí:</span><span class="sxs-lookup"><span data-stu-id="e9813-129">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="e9813-130">Značka</span><span class="sxs-lookup"><span data-stu-id="e9813-130">Tag</span></span> | <span data-ttu-id="e9813-131">Popis</span><span class="sxs-lookup"><span data-stu-id="e9813-131">Description</span></span> | <span data-ttu-id="e9813-132">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="e9813-132">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e9813-133">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="e9813-133">IncludeAssets</span></span> | <span data-ttu-id="e9813-134">Tyto prostředky budou spotřebovány.</span><span class="sxs-lookup"><span data-stu-id="e9813-134">These assets will be consumed</span></span> | <span data-ttu-id="e9813-135">všechny</span><span class="sxs-lookup"><span data-stu-id="e9813-135">all</span></span> |
| <span data-ttu-id="e9813-136">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="e9813-136">ExcludeAssets</span></span> | <span data-ttu-id="e9813-137">Tyto prostředky nebudou spotřebovány.</span><span class="sxs-lookup"><span data-stu-id="e9813-137">These assets will not be consumed</span></span> | <span data-ttu-id="e9813-138">žádná</span><span class="sxs-lookup"><span data-stu-id="e9813-138">none</span></span> |
| <span data-ttu-id="e9813-139">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="e9813-139">PrivateAssets</span></span> | <span data-ttu-id="e9813-140">Tyto prostředky budou spotřebovány, ale nebudou se přesměrovat do nadřazeného projektu.</span><span class="sxs-lookup"><span data-stu-id="e9813-140">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="e9813-141">contentFiles; analyzátory; sestavit</span><span class="sxs-lookup"><span data-stu-id="e9813-141">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="e9813-142">Přípustné hodnoty pro tyto značky jsou následující, s více hodnotami oddělenými středníkem s výjimkou `all` a, `none` které se musí objevit sami:</span><span class="sxs-lookup"><span data-stu-id="e9813-142">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="e9813-143">Value</span><span class="sxs-lookup"><span data-stu-id="e9813-143">Value</span></span> | <span data-ttu-id="e9813-144">Popis</span><span class="sxs-lookup"><span data-stu-id="e9813-144">Description</span></span> |
| --- | ---
| <span data-ttu-id="e9813-145">sestavení</span><span class="sxs-lookup"><span data-stu-id="e9813-145">compile</span></span> | <span data-ttu-id="e9813-146">`lib` Obsah složky a určuje, zda je projekt kompilován proti sestavením v rámci složky</span><span class="sxs-lookup"><span data-stu-id="e9813-146">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="e9813-147">modul runtime</span><span class="sxs-lookup"><span data-stu-id="e9813-147">runtime</span></span> | <span data-ttu-id="e9813-148">Obsah složky `runtimes` a určuje, zda budou tato sestavení zkopírována do výstupního adresáře sestavení `lib`</span><span class="sxs-lookup"><span data-stu-id="e9813-148">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="e9813-149">contentFiles</span><span class="sxs-lookup"><span data-stu-id="e9813-149">contentFiles</span></span> | <span data-ttu-id="e9813-150">`contentfiles` Obsah složky</span><span class="sxs-lookup"><span data-stu-id="e9813-150">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="e9813-151">sestavení</span><span class="sxs-lookup"><span data-stu-id="e9813-151">build</span></span> | <span data-ttu-id="e9813-152">`.props``.targets` a`build` ve složce</span><span class="sxs-lookup"><span data-stu-id="e9813-152">`.props` and `.targets` in the `build` folder</span></span> |
| <span data-ttu-id="e9813-153">buildMultitargeting</span><span class="sxs-lookup"><span data-stu-id="e9813-153">buildMultitargeting</span></span> | <span data-ttu-id="e9813-154">`.props``.targets` a`buildMultitargeting` ve složce pro cílení na různé architektury</span><span class="sxs-lookup"><span data-stu-id="e9813-154">`.props` and `.targets` in the `buildMultitargeting` folder, for cross-framework targeting</span></span> |
| <span data-ttu-id="e9813-155">buildTransitive</span><span class="sxs-lookup"><span data-stu-id="e9813-155">buildTransitive</span></span> | <span data-ttu-id="e9813-156">*(5.0 +)* `.props` a vesložce`buildTransitive` pro prostředky, jejichž přenos do libovolného náročného projektu se protéká. `.targets`</span><span class="sxs-lookup"><span data-stu-id="e9813-156">*(5.0+)* `.props` and `.targets` in the `buildTransitive` folder, for assets that flow transitively to any consuming project.</span></span> <span data-ttu-id="e9813-157">Podívejte se na stránku [funkce](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) .</span><span class="sxs-lookup"><span data-stu-id="e9813-157">See the [feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) page.</span></span> |
| <span data-ttu-id="e9813-158">analyzátory</span><span class="sxs-lookup"><span data-stu-id="e9813-158">analyzers</span></span> | <span data-ttu-id="e9813-159">Analyzátory .NET</span><span class="sxs-lookup"><span data-stu-id="e9813-159">.NET analyzers</span></span> |
| <span data-ttu-id="e9813-160">nativní</span><span class="sxs-lookup"><span data-stu-id="e9813-160">native</span></span> | <span data-ttu-id="e9813-161">`native` Obsah složky</span><span class="sxs-lookup"><span data-stu-id="e9813-161">Contents of the `native` folder</span></span> |
| <span data-ttu-id="e9813-162">žádná</span><span class="sxs-lookup"><span data-stu-id="e9813-162">none</span></span> | <span data-ttu-id="e9813-163">Žádná z výše uvedených verzí se nepoužívá.</span><span class="sxs-lookup"><span data-stu-id="e9813-163">None of the above are used.</span></span> |
| <span data-ttu-id="e9813-164">všechny</span><span class="sxs-lookup"><span data-stu-id="e9813-164">all</span></span> | <span data-ttu-id="e9813-165">Všechny výše uvedené (kromě `none`)</span><span class="sxs-lookup"><span data-stu-id="e9813-165">All of the above (except `none`)</span></span> |

<span data-ttu-id="e9813-166">V následujícím příkladu je vše kromě souborů obsahu z balíčku spotřebováno projektem a vše kromě souborů obsahu a analyzátory by vedlo k nadřazenému projektu.</span><span class="sxs-lookup"><span data-stu-id="e9813-166">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="e9813-167">Všimněte si, `build` že protože není `PrivateAssets`součástí, cíle a props *budou* tok do nadřazeného projektu.</span><span class="sxs-lookup"><span data-stu-id="e9813-167">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="e9813-168">Vezměte v úvahu například, že odkaz výše se používá v projektu, který vytváří balíček NuGet s názvem AppLogger.</span><span class="sxs-lookup"><span data-stu-id="e9813-168">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="e9813-169">AppLogger může využívat cíle a props z `Contoso.Utility.UsefulStuff`, jako mohou projekty, které využívají AppLogger.</span><span class="sxs-lookup"><span data-stu-id="e9813-169">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="e9813-170">Přidání podmínky PackageReference</span><span class="sxs-lookup"><span data-stu-id="e9813-170">Adding a PackageReference condition</span></span>

<span data-ttu-id="e9813-171">Podmínku můžete použít k určení, zda je balíček zahrnut, kde podmínky mohou používat jakoukoli proměnnou MSBuild nebo proměnnou definovanou v souboru TARGETS nebo props.</span><span class="sxs-lookup"><span data-stu-id="e9813-171">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="e9813-172">V předsoučasném případě je však podporována pouze `TargetFramework` proměnná.</span><span class="sxs-lookup"><span data-stu-id="e9813-172">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="e9813-173">Řekněme například, že cílíte `netstandard1.4` `net452` i na, ale máte závislost, která je platná pouze pro `net452`.</span><span class="sxs-lookup"><span data-stu-id="e9813-173">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="e9813-174">V takovém případě nechcete `netstandard1.4` , aby projekt, který váš balíček spotřebovává, přidal tuto nepotřebnou závislost.</span><span class="sxs-lookup"><span data-stu-id="e9813-174">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="e9813-175">Tomu zabráníte tak, že zadáte podmínku `PackageReference` v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="e9813-175">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="e9813-176">Balíček sestavený pomocí tohoto projektu zobrazí, že Newtonsoft. JSON je obsažen pouze jako závislost pro `net452` cíl:</span><span class="sxs-lookup"><span data-stu-id="e9813-176">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![Výsledek použití podmínky v PackageReference s VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="e9813-178">Podmínky lze také použít `ItemGroup` na úrovni a budou platit pro všechny podřízené `PackageReference` prvky:</span><span class="sxs-lookup"><span data-stu-id="e9813-178">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="locking-dependencies"></a><span data-ttu-id="e9813-179">Uzamykání závislostí</span><span class="sxs-lookup"><span data-stu-id="e9813-179">Locking dependencies</span></span>
<span data-ttu-id="e9813-180">*Tato funkce je k dispozici pro NuGet **4,9** nebo vyšší a pro Visual Studio 2017 **15,9** nebo vyšší.*</span><span class="sxs-lookup"><span data-stu-id="e9813-180">*This feature is available with NuGet **4.9** or above and with Visual Studio 2017 **15.9** or above.*</span></span>

<span data-ttu-id="e9813-181">Vstup do obnovení NuGet je sada odkazů na balíčky ze souboru projektu (závislosti na nejvyšší úrovni nebo přímých závislostí) a výstup je plný uzávěr všech závislostí balíčku včetně přenosných závislostí.</span><span class="sxs-lookup"><span data-stu-id="e9813-181">Input to NuGet restore is a set of Package References from the project file (top-level or direct dependencies) and the output is a full closure of all the package dependencies including transitive dependencies.</span></span> <span data-ttu-id="e9813-182">V případě, že se vstupní seznam PackageReference nezměnil, nástroj NuGet se pokusí vždy vydávat stejný plný uzávěr závislostí balíčku.</span><span class="sxs-lookup"><span data-stu-id="e9813-182">NuGet tries to always produce the same full closure of package dependencies if the input PackageReference list has not changed.</span></span> <span data-ttu-id="e9813-183">Existují však situace, kdy to není možné.</span><span class="sxs-lookup"><span data-stu-id="e9813-183">However, there are some scenarios where it is unable to do so.</span></span> <span data-ttu-id="e9813-184">Příklad:</span><span class="sxs-lookup"><span data-stu-id="e9813-184">For example:</span></span>

* <span data-ttu-id="e9813-185">Při použití plovoucích verzí, `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`jako je.</span><span class="sxs-lookup"><span data-stu-id="e9813-185">When you use floating versions like `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span></span> <span data-ttu-id="e9813-186">I když tady je tento záměr na nejnovější verzi v každé obnovy balíčků, existují situace, kdy uživatelé potřebují, aby byl graf uzamčený na určitou nejnovější verzi a aby byl na novější verzi, pokud je k dispozici, po explicitním gestu.</span><span class="sxs-lookup"><span data-stu-id="e9813-186">While the intention here is to float to the latest version on every restore of packages, there are scenarios where users require the graph to be locked to a certain latest version and float to a later version, if available, upon an explicit gesture.</span></span>
* <span data-ttu-id="e9813-187">Je publikovaná novější verze balíčku, která odpovídá požadavkům verze PackageReference.</span><span class="sxs-lookup"><span data-stu-id="e9813-187">A newer version of the package matching PackageReference version requirements is published.</span></span> <span data-ttu-id="e9813-188">Například</span><span class="sxs-lookup"><span data-stu-id="e9813-188">E.g.</span></span> 

  * <span data-ttu-id="e9813-189">Den 1: Pokud jste zadali `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` verze, které jsou k dispozici v úložištích NuGet, byly 4.1.0, 4.2.0 a 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="e9813-189">Day 1: if you specified `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` but the versions available on the NuGet repositories were 4.1.0, 4.2.0 and 4.3.0.</span></span> <span data-ttu-id="e9813-190">V tomto případě se NuGet přeložil na 4.1.0 (nejbližší minimální verzi).</span><span class="sxs-lookup"><span data-stu-id="e9813-190">In this case, NuGet would have resolved to  4.1.0 (nearest minimum version)</span></span>

  * <span data-ttu-id="e9813-191">Den 2: Verze 4.0.0 se publikuje.</span><span class="sxs-lookup"><span data-stu-id="e9813-191">Day 2: Version 4.0.0 gets published.</span></span> <span data-ttu-id="e9813-192">NuGet teď najde přesnou shodu a začne řešit na 4.0.0</span><span class="sxs-lookup"><span data-stu-id="e9813-192">NuGet will now find the exact match and start resolving to 4.0.0</span></span>

* <span data-ttu-id="e9813-193">Daná verze balíčku se odebere z úložiště.</span><span class="sxs-lookup"><span data-stu-id="e9813-193">A given package version is removed from the repository.</span></span> <span data-ttu-id="e9813-194">I když nuget.org nepovoluje odstraňování balíčků, ne všechna úložiště balíčků mají tato omezení.</span><span class="sxs-lookup"><span data-stu-id="e9813-194">Though nuget.org does not allow package deletions, not all package repositories have this constraints.</span></span> <span data-ttu-id="e9813-195">Výsledkem je, že NuGet najde nejlepší shodu, když ho nelze vyřešit na odstraněnou verzi.</span><span class="sxs-lookup"><span data-stu-id="e9813-195">This results in NuGet finding the best match when it cannot resolve to the deleted version.</span></span>

### <a name="enabling-lock-file"></a><span data-ttu-id="e9813-196">Povoluje se soubor zámku.</span><span class="sxs-lookup"><span data-stu-id="e9813-196">Enabling lock file</span></span>
<span data-ttu-id="e9813-197">Aby se zachoval úplný konec závislostí balíčku, můžete se přihlásit k funkci zámek souboru nastavením vlastnosti `RestorePackagesWithLockFile` MSBuild pro váš projekt:</span><span class="sxs-lookup"><span data-stu-id="e9813-197">In order to persist the full closure of package dependencies you can opt-in to the lock file feature by setting the MSBuild property `RestorePackagesWithLockFile` for your project:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="e9813-198">Pokud je tato vlastnost nastavená, obnovení NuGet vygeneruje soubor zámku File `packages.lock.json` v kořenovém adresáři projektu, který obsahuje seznam všech závislostí balíčku.</span><span class="sxs-lookup"><span data-stu-id="e9813-198">If this property is set, NuGet restore will generate a lock file - `packages.lock.json` file at the project root directory that lists all the package dependencies.</span></span> 

> [!Note]
> <span data-ttu-id="e9813-199">Jakmile projekt obsahuje `packages.lock.json` soubor ve svém kořenovém adresáři, soubor zámku se vždy používá s obnovením i v případě, `RestorePackagesWithLockFile` že vlastnost není nastavena.</span><span class="sxs-lookup"><span data-stu-id="e9813-199">Once a project has `packages.lock.json` file in its root directory, the lock file is always used with restore even if the property `RestorePackagesWithLockFile` is not set.</span></span> <span data-ttu-id="e9813-200">Další možností, jak se vyjádřit k této funkci, je vytvořit fiktivní prázdný `packages.lock.json` soubor v kořenovém adresáři projektu.</span><span class="sxs-lookup"><span data-stu-id="e9813-200">So another way to opt-in to this feature is to create a dummy blank `packages.lock.json` file in the project's root directory.</span></span>

### <a name="restore-behavior-with-lock-file"></a><span data-ttu-id="e9813-201">`restore`chování se souborem zámku</span><span class="sxs-lookup"><span data-stu-id="e9813-201">`restore` behavior with lock file</span></span>
<span data-ttu-id="e9813-202">Pokud je soubor zámku k dispozici pro projekt, nástroj NuGet používá ke spuštění `restore`tento soubor zámku.</span><span class="sxs-lookup"><span data-stu-id="e9813-202">If a lock file is present for project, NuGet uses this lock file to run `restore`.</span></span> <span data-ttu-id="e9813-203">NuGet provede rychlou kontrolu, jestli se v závislostech balíčku nezměnily žádné změny, jak je uvedeno v souboru projektu (nebo v souborech závislých projektů) a jestli nedošlo k žádným změnám, jenom obnoví balíčky uvedené v souboru zámku.</span><span class="sxs-lookup"><span data-stu-id="e9813-203">NuGet does a quick check to see if there were any changes in the package dependencies as mentioned in the project file (or dependent projects' files) and if there were no changes it just restores the packages mentioned in the lock file.</span></span> <span data-ttu-id="e9813-204">Nedošlo k opakovanému vyhodnocení závislostí balíčku.</span><span class="sxs-lookup"><span data-stu-id="e9813-204">There is no re-evaluation of package dependencies.</span></span>

<span data-ttu-id="e9813-205">Pokud NuGet detekuje změnu v definovaných závislostech, jak je uvedeno v souborech projektu, znovu vyhodnotí graf balíčku a aktualizuje soubor zámku tak, aby odrážel nový uzavření balíčku pro daný projekt.</span><span class="sxs-lookup"><span data-stu-id="e9813-205">If NuGet detects a change in the defined dependencies as mentioned in the project file(s), it re-evaluates the package graph and updates the lock file to reflect the new package closure for the project.</span></span>

<span data-ttu-id="e9813-206">V případě CI/CD a dalších scénářů, kde byste nechtěli změnit závislosti balíčku za běhu, můžete to provést nastavením `lockedmode` na: `true`</span><span class="sxs-lookup"><span data-stu-id="e9813-206">For CI/CD and other scenarios, where you would not want to change the package dependencies on the fly, you can do so by setting the `lockedmode` to `true`:</span></span>

<span data-ttu-id="e9813-207">Pro příkaz dotnet. exe spusťte:</span><span class="sxs-lookup"><span data-stu-id="e9813-207">For dotnet.exe, run:</span></span>
```
> dotnet.exe restore --locked-mode
```

<span data-ttu-id="e9813-208">Pro MSBuild. exe spusťte:</span><span class="sxs-lookup"><span data-stu-id="e9813-208">For msbuild.exe, run:</span></span>
```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

<span data-ttu-id="e9813-209">Tuto vlastnost podmíněného MSBuild můžete nastavit také v souboru projektu:</span><span class="sxs-lookup"><span data-stu-id="e9813-209">You may also set this conditional MSBuild property in your project file:</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

<span data-ttu-id="e9813-210">Pokud je `true`uzamčený režim, obnovení obnoví buď přesné balíčky uvedené v souboru zámku, nebo selže, pokud jste aktualizovali definované závislosti balíčků pro projekt po vytvoření souboru zámku.</span><span class="sxs-lookup"><span data-stu-id="e9813-210">If locked mode is `true`, restore will either restore the exact packages as listed in the lock file or fail if you updated the defined package dependencies for the project after lock file was created.</span></span>

### <a name="make-lock-file-part-of-your-source-repository"></a><span data-ttu-id="e9813-211">Nastavit zámek souboru jako součást zdrojového úložiště</span><span class="sxs-lookup"><span data-stu-id="e9813-211">Make lock file part of your source repository</span></span>
<span data-ttu-id="e9813-212">Pokud vytváříte aplikaci, spustitelný soubor a příslušný projekt jsou na začátku řetězu závislostí a pak proveďte vrácení souboru se zámkem do úložiště zdrojového kódu, aby jej mohla aplikace NuGet využít při obnovení.</span><span class="sxs-lookup"><span data-stu-id="e9813-212">If you are building an application, an executable and the project in question is at the start of the dependency chain then do check in the lock file to the source code repository so that NuGet can make use of it during restore.</span></span>

<span data-ttu-id="e9813-213">Pokud je však projekt knihovnou projektu, který nedodáte nebo se jedná o běžný projekt kódu, na kterém jsou závislé další projekty, **neměli byste** soubory zámku vrátit se změnami jako součást zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="e9813-213">However, if your project is a library project that you do not ship or a common code project on which other projects depend upon, you **should not** check in the lock file as part of your source code.</span></span> <span data-ttu-id="e9813-214">Neexistuje žádný škodný soubor zámku, ale nelze použít uzamčené závislosti balíčku pro běžný projekt kódu, jak je uvedeno v souboru zámku během obnovení nebo sestavení projektu, který je závislý na tomto projektu Common-Code.</span><span class="sxs-lookup"><span data-stu-id="e9813-214">There is no harm in keeping the lock file but the locked package dependencies for the common code project may not be used, as listed in the lock file, during the restore/build of a project that depends on this common-code project.</span></span>

<span data-ttu-id="e9813-215">EG.</span><span class="sxs-lookup"><span data-stu-id="e9813-215">Eg.</span></span>
```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```
<span data-ttu-id="e9813-216">Pokud `ProjectA` má závislost `PackageX` na verzi `2.0.0` a také odkazy `ProjectB` , které závisejí na `PackageX` verzi `1.0.0`, pak soubor zámku pro `ProjectB` bude zobrazovat závislost na `PackageX` verze `1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="e9813-216">If `ProjectA` has a dependency on a `PackageX` version `2.0.0` and also references `ProjectB` that depends on `PackageX` version `1.0.0`, then the lock file for `ProjectB` will list a dependency on `PackageX` version `1.0.0`.</span></span> <span data-ttu-id="e9813-217">Když `ProjectA` `PackageX` je však sestaven, jeho soubor zámku bude obsahovat závislost na verzi **`2.0.0`** a **nikoli** `1.0.0` , jak je uvedeno v souboru zámku pro `ProjectB`.</span><span class="sxs-lookup"><span data-stu-id="e9813-217">However, when `ProjectA` is built, its lock file will contain a dependency on `PackageX` version **`2.0.0`** and **not** `1.0.0` as listed in the lock file for `ProjectB`.</span></span> <span data-ttu-id="e9813-218">Proto soubor zámku pro běžný projekt kódu trochu říká, že balíčky byly vyřešeny pro projekty, které jsou na ní závislé.</span><span class="sxs-lookup"><span data-stu-id="e9813-218">Thus, the lock file of a common code project has little say over the packages resolved for projects that depend on it.</span></span>

### <a name="lock-file-extensibility"></a><span data-ttu-id="e9813-219">Zamknout rozšíření souboru</span><span class="sxs-lookup"><span data-stu-id="e9813-219">Lock file extensibility</span></span>
<span data-ttu-id="e9813-220">Můžete řídit různá chování při obnovení pomocí souboru zámku, jak je popsáno níže:</span><span class="sxs-lookup"><span data-stu-id="e9813-220">You can control various behaviors of restore with lock file as described below:</span></span>

| <span data-ttu-id="e9813-221">Možnost</span><span class="sxs-lookup"><span data-stu-id="e9813-221">Option</span></span> | <span data-ttu-id="e9813-222">Možnost ekvivalentu MSBuild</span><span class="sxs-lookup"><span data-stu-id="e9813-222">MSBuild equivalent option</span></span> | 
|:---  |:--- |
| `--use-lock-file` | <span data-ttu-id="e9813-223">Slouží k zavedení souboru zámku pro projekt.</span><span class="sxs-lookup"><span data-stu-id="e9813-223">Bootstraps use of lock file for a project.</span></span> <span data-ttu-id="e9813-224">Můžete také nastavit `RestorePackagesWithLockFile` vlastnost v souboru projektu</span><span class="sxs-lookup"><span data-stu-id="e9813-224">You can alternatively set `RestorePackagesWithLockFile` property in the project file</span></span> | 
| `--locked-mode` | <span data-ttu-id="e9813-225">Zapne uzamčený režim pro obnovení.</span><span class="sxs-lookup"><span data-stu-id="e9813-225">Enables locked mode for restore.</span></span> <span data-ttu-id="e9813-226">To je užitečné ve scénářích CI/CD, kde byste chtěli získat opakovaně vytvořená sestavení.</span><span class="sxs-lookup"><span data-stu-id="e9813-226">This is useful in CI/CD scenarios where you would like to get the repeatable builds.</span></span> <span data-ttu-id="e9813-227">To může být také nastavením `RestoreLockedMode` vlastnosti MSBuild na`true`</span><span class="sxs-lookup"><span data-stu-id="e9813-227">This can be also by setting the `RestoreLockedMode` MSBuild property to `true`</span></span> |  
| `--force-evaluate` | <span data-ttu-id="e9813-228">Tato možnost je užitečná pro balíčky s plovoucí verzí definovanou v projektu.</span><span class="sxs-lookup"><span data-stu-id="e9813-228">This option is useful with packages with floating version defined in the project.</span></span> <span data-ttu-id="e9813-229">Ve výchozím nastavení obnovení NuGet při každém obnovení automaticky neaktualizuje verzi balíčku, dokud nespustíte možnost obnovit `--force-evaluate` s možností.</span><span class="sxs-lookup"><span data-stu-id="e9813-229">By default, NuGet restore will not update the package version automatically upon each restore unless you run restore with `--force-evaluate` option.</span></span> |
| `--lock-file-path` | <span data-ttu-id="e9813-230">Definuje vlastní umístění souboru zámku pro projekt.</span><span class="sxs-lookup"><span data-stu-id="e9813-230">Defines a custom lock file location for a project.</span></span> <span data-ttu-id="e9813-231">To lze také dosáhnout nastavením vlastnosti `NuGetLockFilePath`MSBuild.</span><span class="sxs-lookup"><span data-stu-id="e9813-231">This can be also achieved by setting the MSBuild property `NuGetLockFilePath`.</span></span> <span data-ttu-id="e9813-232">Ve výchozím nastavení NuGet podporuje `packages.lock.json` v kořenovém adresáři.</span><span class="sxs-lookup"><span data-stu-id="e9813-232">By default, NuGet supports `packages.lock.json` at the root directory.</span></span> <span data-ttu-id="e9813-233">Pokud máte ve stejném adresáři více projektů, NuGet podporuje soubor zámku specifický pro projekt.`packages.<project_name>.lock.json`</span><span class="sxs-lookup"><span data-stu-id="e9813-233">If you have multiple projects in the same directory, NuGet supports project specific lock file `packages.<project_name>.lock.json`</span></span> |
