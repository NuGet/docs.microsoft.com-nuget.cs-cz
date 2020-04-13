---
title: Formát NuGet PackageReference (odkazy na balíček v souborech projektu)
description: Podrobnosti o NuGet PackageReference v projektových souborech podporovaných NuGet 4.0+ a VS2017 a .NET Core 2.0
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: a5833df60c5f7905359f421141347b1237f45d86
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428868"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="0a047-103">Odkazy na balíčky (PackageReference) v souborech projektu</span><span class="sxs-lookup"><span data-stu-id="0a047-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="0a047-104">Odkazy na balíčky `PackageReference` pomocí uzlu spravují závislosti NuGet přímo v rámci `packages.config` souborů projektu (na rozdíl od samostatného souboru).</span><span class="sxs-lookup"><span data-stu-id="0a047-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="0a047-105">Použití PackageReference, jak se nazývá, nemá vliv na jiné aspekty NuGet; například nastavení `NuGet.config` v souborech (včetně zdrojů balíčků) jsou stále použita, jak je vysvětleno v [běžných konfiguracích NuGet](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="0a047-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.config` files (including package sources) are still applied as explained in [Common NuGet configurations](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="0a047-106">S PackageReference, můžete také použít MSBuild podmínky zvolit odkazy na balíček na cílové rozhraní nebo jiné seskupení.</span><span class="sxs-lookup"><span data-stu-id="0a047-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, or other groupings.</span></span> <span data-ttu-id="0a047-107">Umožňuje také jemně odstupňovanou kontrolu nad závislostmi a tok obsahu.</span><span class="sxs-lookup"><span data-stu-id="0a047-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="0a047-108">(Další podrobnosti naleznete [v balíčku NuGet pack a obnovení jako cíle MSBuild](../reference/msbuild-targets.md).)</span><span class="sxs-lookup"><span data-stu-id="0a047-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

## <a name="project-type-support"></a><span data-ttu-id="0a047-109">Podpora typu projektu</span><span class="sxs-lookup"><span data-stu-id="0a047-109">Project type support</span></span>

<span data-ttu-id="0a047-110">Ve výchozím nastavení packagereference se používá pro projekty .NET Core, .NET Standard projekty a UPW projekty zaměřené na Windows 10 Sestavení 15063 (Creators Update) a novější, s výjimkou projektů C++ UpWP.</span><span class="sxs-lookup"><span data-stu-id="0a047-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="0a047-111">Projekty rozhraní .NET Framework podporují odkaz `packages.config`packagereference, ale aktuálně je ve výchozím nastavení .</span><span class="sxs-lookup"><span data-stu-id="0a047-111">.NET Framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="0a047-112">Chcete-li použít PackageReference, `packages.config` [migrujte](../consume-packages/migrate-packages-config-to-package-reference.md) závislosti z do souboru projektu a odeberte soubor packages.config.</span><span class="sxs-lookup"><span data-stu-id="0a047-112">To use PackageReference, [migrate](../consume-packages/migrate-packages-config-to-package-reference.md) the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

<span data-ttu-id="0a047-113">ASP.NET aplikace, které cílí na úplnou architekturu .NET Framework, zahrnují pouze [omezenou podporu](https://github.com/NuGet/Home/issues/5877) pro PackageReference.</span><span class="sxs-lookup"><span data-stu-id="0a047-113">ASP.NET apps targeting the full .NET Framework include only [limited support](https://github.com/NuGet/Home/issues/5877) for PackageReference.</span></span> <span data-ttu-id="0a047-114">Typy projektů jazyka C++ a JavaScript nejsou podporovány.</span><span class="sxs-lookup"><span data-stu-id="0a047-114">C++ and JavaScript project types are unsupported.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="0a047-115">Přidání odkazu na balíček</span><span class="sxs-lookup"><span data-stu-id="0a047-115">Adding a PackageReference</span></span>

<span data-ttu-id="0a047-116">Přidejte závislost do souboru projektu pomocí následující syntaxe:</span><span class="sxs-lookup"><span data-stu-id="0a047-116">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="0a047-117">Řízení verze závislostí</span><span class="sxs-lookup"><span data-stu-id="0a047-117">Controlling dependency version</span></span>

<span data-ttu-id="0a047-118">Konvence pro určení verze balíčku je stejná jako `packages.config`při použití :</span><span class="sxs-lookup"><span data-stu-id="0a047-118">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="0a047-119">Ve výše uvedeném příkladu 3.6.0 znamená libovolnou verzi, která je >=3.6.0 s předvolbou pro nejnižší verzi, jak je popsáno v [package versioning](../concepts/package-versioning.md#version-ranges).</span><span class="sxs-lookup"><span data-stu-id="0a047-119">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../concepts/package-versioning.md#version-ranges).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="0a047-120">Použití Odkazu packagereference pro projekt bez odkazů na balíček</span><span class="sxs-lookup"><span data-stu-id="0a047-120">Using PackageReference for a project with no PackageReferences</span></span>

<span data-ttu-id="0a047-121">Upřesnit: Pokud nemáte v projektu nainstalovány žádné balíčky (žádné odkazy na balíčky v souboru projektu a žádný soubor packages.config), ale chcete projekt obnovit jako styl PackageReference, můžete v souboru projektu nastavit vlastnost projektu RestoreProjectStyle na PackageReference.</span><span class="sxs-lookup"><span data-stu-id="0a047-121">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="0a047-122">To může být užitečné, pokud odkazujete na projekty, které jsou stylem PackageReference (existující projekty ve stylu csproj nebo SDK).</span><span class="sxs-lookup"><span data-stu-id="0a047-122">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="0a047-123">To umožní balíčky, které tyto projekty odkazují, které mají být "tranzively" odkazuje váš projekt.</span><span class="sxs-lookup"><span data-stu-id="0a047-123">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="packagereference-and-sources"></a><span data-ttu-id="0a047-124">PackageReference a zdroje</span><span class="sxs-lookup"><span data-stu-id="0a047-124">PackageReference and sources</span></span>

<span data-ttu-id="0a047-125">V projektech PackageReference jsou v době obnovení vyřešeny přenosité verze závislostí.</span><span class="sxs-lookup"><span data-stu-id="0a047-125">In PackageReference projects, the transitive dependency versions are resolved at restore time.</span></span> <span data-ttu-id="0a047-126">Jako takové v PackageReference projekty všechny zdroje musí být k dispozici pro všechny obnoví.</span><span class="sxs-lookup"><span data-stu-id="0a047-126">As such, in PackageReference projects all sources need to be available for all restores.</span></span> 

## <a name="floating-versions"></a><span data-ttu-id="0a047-127">Plovoucí verze</span><span class="sxs-lookup"><span data-stu-id="0a047-127">Floating Versions</span></span>

<span data-ttu-id="0a047-128">[Plovoucí verze](../concepts/dependency-resolution.md#floating-versions) jsou `PackageReference`podporovány s :</span><span class="sxs-lookup"><span data-stu-id="0a047-128">[Floating versions](../concepts/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="0a047-129">Řízení prostředků závislostí</span><span class="sxs-lookup"><span data-stu-id="0a047-129">Controlling dependency assets</span></span>

<span data-ttu-id="0a047-130">Závislost můžete používat čistě jako vývojový svazek a možná nebudete chtít vystavit, že projekty, které budou využívat váš balíček.</span><span class="sxs-lookup"><span data-stu-id="0a047-130">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="0a047-131">V tomto scénáři můžete `PrivateAssets` použít metadata k řízení tohoto chování.</span><span class="sxs-lookup"><span data-stu-id="0a047-131">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="0a047-132">Následující značky metadat řídí prostředky závislostí:</span><span class="sxs-lookup"><span data-stu-id="0a047-132">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="0a047-133">Značka</span><span class="sxs-lookup"><span data-stu-id="0a047-133">Tag</span></span> | <span data-ttu-id="0a047-134">Popis</span><span class="sxs-lookup"><span data-stu-id="0a047-134">Description</span></span> | <span data-ttu-id="0a047-135">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="0a047-135">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0a047-136">Zahrnout datové zdroje</span><span class="sxs-lookup"><span data-stu-id="0a047-136">IncludeAssets</span></span> | <span data-ttu-id="0a047-137">Tato aktiva budou spotřebována</span><span class="sxs-lookup"><span data-stu-id="0a047-137">These assets will be consumed</span></span> | <span data-ttu-id="0a047-138">Vše</span><span class="sxs-lookup"><span data-stu-id="0a047-138">all</span></span> |
| <span data-ttu-id="0a047-139">Vyloučit majetek</span><span class="sxs-lookup"><span data-stu-id="0a047-139">ExcludeAssets</span></span> | <span data-ttu-id="0a047-140">Tato aktiva nebudou spotřebována</span><span class="sxs-lookup"><span data-stu-id="0a047-140">These assets will not be consumed</span></span> | <span data-ttu-id="0a047-141">Žádná</span><span class="sxs-lookup"><span data-stu-id="0a047-141">none</span></span> |
| <span data-ttu-id="0a047-142">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="0a047-142">PrivateAssets</span></span> | <span data-ttu-id="0a047-143">Tyto prostředky budou spotřebovány, ale nebudou tok do nadřazeného projektu</span><span class="sxs-lookup"><span data-stu-id="0a047-143">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="0a047-144">contentfiles;analyzátory;sestavení</span><span class="sxs-lookup"><span data-stu-id="0a047-144">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="0a047-145">Přípustné hodnoty pro tyto značky jsou následující, s více hodnotami `none` oddělenými středníkem s výjimkou a `all` které se musí objevit samy od sebe:</span><span class="sxs-lookup"><span data-stu-id="0a047-145">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="0a047-146">Hodnota</span><span class="sxs-lookup"><span data-stu-id="0a047-146">Value</span></span> | <span data-ttu-id="0a047-147">Popis</span><span class="sxs-lookup"><span data-stu-id="0a047-147">Description</span></span> |
| --- | ---
| <span data-ttu-id="0a047-148">kompilovat</span><span class="sxs-lookup"><span data-stu-id="0a047-148">compile</span></span> | <span data-ttu-id="0a047-149">Obsah `lib` složky a určuje, zda projekt může kompilovat proti sestavení ve složce</span><span class="sxs-lookup"><span data-stu-id="0a047-149">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="0a047-150">modul runtime</span><span class="sxs-lookup"><span data-stu-id="0a047-150">runtime</span></span> | <span data-ttu-id="0a047-151">`lib` Obsah `runtimes` a složky a určuje, zda budou tato sestavení zkopírována do výstupního adresáře sestavení.</span><span class="sxs-lookup"><span data-stu-id="0a047-151">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="0a047-152">contentFiles</span><span class="sxs-lookup"><span data-stu-id="0a047-152">contentFiles</span></span> | <span data-ttu-id="0a047-153">Obsah `contentfiles` složky</span><span class="sxs-lookup"><span data-stu-id="0a047-153">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="0a047-154">sestavení</span><span class="sxs-lookup"><span data-stu-id="0a047-154">build</span></span> | <span data-ttu-id="0a047-155">`.props`a `.targets` ve `build` složce</span><span class="sxs-lookup"><span data-stu-id="0a047-155">`.props` and `.targets` in the `build` folder</span></span> |
| <span data-ttu-id="0a047-156">buildMultitargeting</span><span class="sxs-lookup"><span data-stu-id="0a047-156">buildMultitargeting</span></span> | <span data-ttu-id="0a047-157">*(4.0)* `.props` `.targets` a `buildMultitargeting` ve složce pro cílení napříč rámci</span><span class="sxs-lookup"><span data-stu-id="0a047-157">*(4.0)* `.props` and `.targets` in the `buildMultitargeting` folder, for cross-framework targeting</span></span> |
| <span data-ttu-id="0a047-158">buildTransitive</span><span class="sxs-lookup"><span data-stu-id="0a047-158">buildTransitive</span></span> | <span data-ttu-id="0a047-159">*(5.0+)* `.props` `.targets` a `buildTransitive` ve složce pro prostředky, které plynule proudí do jakéhokoli náročného projektu.</span><span class="sxs-lookup"><span data-stu-id="0a047-159">*(5.0+)* `.props` and `.targets` in the `buildTransitive` folder, for assets that flow transitively to any consuming project.</span></span> <span data-ttu-id="0a047-160">Podívejte se na stránku [funkcí.](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior)</span><span class="sxs-lookup"><span data-stu-id="0a047-160">See the [feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) page.</span></span> |
| <span data-ttu-id="0a047-161">Analyzátory</span><span class="sxs-lookup"><span data-stu-id="0a047-161">analyzers</span></span> | <span data-ttu-id="0a047-162">Analyzátory .NET</span><span class="sxs-lookup"><span data-stu-id="0a047-162">.NET analyzers</span></span> |
| <span data-ttu-id="0a047-163">nativní</span><span class="sxs-lookup"><span data-stu-id="0a047-163">native</span></span> | <span data-ttu-id="0a047-164">Obsah `native` složky</span><span class="sxs-lookup"><span data-stu-id="0a047-164">Contents of the `native` folder</span></span> |
| <span data-ttu-id="0a047-165">Žádná</span><span class="sxs-lookup"><span data-stu-id="0a047-165">none</span></span> | <span data-ttu-id="0a047-166">Nic z výše uvedeného se nepoužívá.</span><span class="sxs-lookup"><span data-stu-id="0a047-166">None of the above are used.</span></span> |
| <span data-ttu-id="0a047-167">Vše</span><span class="sxs-lookup"><span data-stu-id="0a047-167">all</span></span> | <span data-ttu-id="0a047-168">Všechny výše uvedené `none`(kromě )</span><span class="sxs-lookup"><span data-stu-id="0a047-168">All of the above (except `none`)</span></span> |

<span data-ttu-id="0a047-169">V následujícím příkladu by projekt spotřeboval vše kromě souborů obsahu z balíčku a vše kromě souborů obsahu a analyzátorů by tok do nadřazeného projektu.</span><span class="sxs-lookup"><span data-stu-id="0a047-169">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="0a047-170">Všimněte `build` si, že `PrivateAssets`vzhledem k tomu, že není součástí , cíle a rekvizity *bude* tok do nadřazeného projektu.</span><span class="sxs-lookup"><span data-stu-id="0a047-170">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="0a047-171">Zvažte například, že výše uvedený odkaz se používá v projektu, který vytváří balíček NuGet s názvem AppLogger.</span><span class="sxs-lookup"><span data-stu-id="0a047-171">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="0a047-172">AppLogger může spotřebovat cíle `Contoso.Utility.UsefulStuff`a rekvizity z , stejně jako projekty, které spotřebovávají AppLogger.</span><span class="sxs-lookup"><span data-stu-id="0a047-172">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

> [!NOTE]
> <span data-ttu-id="0a047-173">Pokud `developmentDependency` je `true` nastavena `.nuspec` na v souboru, to označí balíček jako závislost pouze pro vývoj, který zabraňuje balíček zahrnuty jako závislost v jiných balíčcích.</span><span class="sxs-lookup"><span data-stu-id="0a047-173">When `developmentDependency` is set to `true` in a `.nuspec` file, this marks a package as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="0a047-174">S PackageReference *(NuGet 4.8+)* tento příznak také znamená, že vyloučí prostředky kompilace v době kompilace.</span><span class="sxs-lookup"><span data-stu-id="0a047-174">With PackageReference *(NuGet 4.8+)*, this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="0a047-175">Další informace naleznete v [tématu DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span><span class="sxs-lookup"><span data-stu-id="0a047-175">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="0a047-176">Přidání podmínky PackageReference</span><span class="sxs-lookup"><span data-stu-id="0a047-176">Adding a PackageReference condition</span></span>

<span data-ttu-id="0a047-177">Podmínku můžete použít k řízení, zda je součástí balíčku, kde podmínky můžete použít libovolnou proměnnou MSBuild nebo proměnnou definovanou v souboru cílů nebo rekvizit.</span><span class="sxs-lookup"><span data-stu-id="0a047-177">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="0a047-178">V současné době je `TargetFramework` však podporována pouze proměnná.</span><span class="sxs-lookup"><span data-stu-id="0a047-178">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="0a047-179">Řekněme například, že `netstandard1.4` cílíte stejně jako `net452` ale máte `net452`závislost, která je použitelná pouze pro .</span><span class="sxs-lookup"><span data-stu-id="0a047-179">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="0a047-180">V takovém případě nechcete, `netstandard1.4` aby projekt, který spotřebovává váš balíček, přidal tuto zbytečnou závislost.</span><span class="sxs-lookup"><span data-stu-id="0a047-180">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="0a047-181">Chcete-li tomu zabránit, zadejte podmínku `PackageReference` následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="0a047-181">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="0a047-182">Balíček postavený pomocí tohoto projektu ukáže, že Newtonsoft.Json je `net452` zahrnut jako závislost pouze pro cíl:</span><span class="sxs-lookup"><span data-stu-id="0a047-182">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![Výsledek použití Condition on PackageReference s VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="0a047-184">Podmínky mohou být také `ItemGroup` použity na úrovni `PackageReference` a budou se vztahovat na všechny podřízené prvky:</span><span class="sxs-lookup"><span data-stu-id="0a047-184">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="generatepathproperty"></a><span data-ttu-id="0a047-185">GeneratePathProperty</span><span class="sxs-lookup"><span data-stu-id="0a047-185">GeneratePathProperty</span></span>

<span data-ttu-id="0a047-186">Tato funkce je k dispozici s NuGet **5.0** nebo vyšší a s Visual Studio 2019 **16.0** nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="0a047-186">This feature is available with NuGet **5.0** or above and with Visual Studio 2019 **16.0** or above.</span></span>

<span data-ttu-id="0a047-187">Někdy je žádoucí odkazovat na soubory v balíčku z cíle MSBuild.</span><span class="sxs-lookup"><span data-stu-id="0a047-187">Sometimes it is desirable to reference files in a package from an MSBuild target.</span></span>
<span data-ttu-id="0a047-188">V `packages.config` projektech založených na balíčcích jsou balíčky nainstalovány ve složce vzhledem k souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="0a047-188">In `packages.config` based projects, the packages are installed in a folder relative to the project file.</span></span> <span data-ttu-id="0a047-189">Vbalíčcích Však v PackageReference balíčky jsou [spotřebovány](../concepts/package-installation-process.md) ze složky *globální balíčky,* které se mohou lišit od počítače k počítači.</span><span class="sxs-lookup"><span data-stu-id="0a047-189">However in PackageReference, the packages are [consumed](../concepts/package-installation-process.md) from the *global-packages* folder, which can vary from machine to machine.</span></span>

<span data-ttu-id="0a047-190">Chcete-li překlenout tuto mezeru, NuGet představil vlastnost, která odkazuje na umístění, ze kterého bude balíček spotřebována.</span><span class="sxs-lookup"><span data-stu-id="0a047-190">To bridge that gap, NuGet introduced a property that points to the location from which the package will be consumed.</span></span>

<span data-ttu-id="0a047-191">Příklad:</span><span class="sxs-lookup"><span data-stu-id="0a047-191">Example:</span></span>

```xml
  <ItemGroup>
      <PackageReference Include="Some.Package" Version="1.0.0" GeneratePathProperty="true" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgSome_Package)\something.exe" />
  </Target>
````

<span data-ttu-id="0a047-192">Navíc NuGet bude automaticky generovat vlastnosti pro balíčky obsahující složky nástrojů.</span><span class="sxs-lookup"><span data-stu-id="0a047-192">Additionally NuGet will automatically generate properties for packages containing a tools folder.</span></span>

```xml
  <ItemGroup>
      <PackageReference Include="Package.With.Tools" Version="1.0.0" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgPackage_With_Tools)\tools\tool.exe" />
  </Target>
````

<span data-ttu-id="0a047-193">Vlastnosti MSBuild a identity balíčků nemají stejná omezení, takže identitu balíčku je třeba změnit na `Pkg`popisný název MSBuild, předponou slovem .</span><span class="sxs-lookup"><span data-stu-id="0a047-193">MSBuild properties and package identities do not have the same restrictions so the package identity needs to be changed to an MSBuild friendly name, prefixed by the word `Pkg`.</span></span>
<span data-ttu-id="0a047-194">Chcete-li ověřit přesný název generované vlastnosti, podívejte se na generovaný soubor [nuget.g.props.](../reference/msbuild-targets.md#restore-outputs)</span><span class="sxs-lookup"><span data-stu-id="0a047-194">To verify the exact name of the property generated, look at the generated [nuget.g.props](../reference/msbuild-targets.md#restore-outputs) file.</span></span>

## <a name="nuget-warnings-and-errors"></a><span data-ttu-id="0a047-195">Upozornění a chyby NuGet</span><span class="sxs-lookup"><span data-stu-id="0a047-195">NuGet warnings and errors</span></span>

<span data-ttu-id="0a047-196">*Tato funkce je k dispozici s NuGet **4.3** nebo vyšší a s Visual Studio 2017 **15.3** nebo vyšší.*</span><span class="sxs-lookup"><span data-stu-id="0a047-196">*This feature is available with NuGet **4.3** or above and with Visual Studio 2017 **15.3** or above.*</span></span>

<span data-ttu-id="0a047-197">Pro mnoho scénářů pack a obnovení všechna upozornění nuget `NU****`a chyby jsou kódovány a začínat .</span><span class="sxs-lookup"><span data-stu-id="0a047-197">For many pack and restore scenarios, all NuGet warnings and errors are coded, and start with `NU****`.</span></span> <span data-ttu-id="0a047-198">Všechna upozornění a chyby NuGet jsou uvedeny v [referenční](../reference/errors-and-warnings.md) dokumentaci.</span><span class="sxs-lookup"><span data-stu-id="0a047-198">All NuGet warnings and errors are listed in the [reference](../reference/errors-and-warnings.md) documentation.</span></span>

<span data-ttu-id="0a047-199">NuGet dodržuje následující vlastnosti upozornění:</span><span class="sxs-lookup"><span data-stu-id="0a047-199">NuGet observes the following warning properties:</span></span>

- <span data-ttu-id="0a047-200">`TreatWarningsAsErrors`, považovat všechna varování za chyby</span><span class="sxs-lookup"><span data-stu-id="0a047-200">`TreatWarningsAsErrors`, treat all warnings as errors</span></span>
- <span data-ttu-id="0a047-201">`WarningsAsErrors`, považovat konkrétní varování za chyby</span><span class="sxs-lookup"><span data-stu-id="0a047-201">`WarningsAsErrors`, treat specific warnings as errors</span></span>
- <span data-ttu-id="0a047-202">`NoWarn`, skryjte konkrétní varování, ať už v rámci celého projektu, nebo v rámci celého balíčku.</span><span class="sxs-lookup"><span data-stu-id="0a047-202">`NoWarn`, hide specific warnings, either project-wide or package-wide.</span></span>

<span data-ttu-id="0a047-203">Příklady:</span><span class="sxs-lookup"><span data-stu-id="0a047-203">Examples:</span></span>

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

### <a name="suppressing-nuget-warnings"></a><span data-ttu-id="0a047-204">Potlačení upozornění NuGet</span><span class="sxs-lookup"><span data-stu-id="0a047-204">Suppressing NuGet warnings</span></span>

<span data-ttu-id="0a047-205">Zatímco je doporučeno vyřešit všechna upozornění NuGet během operace balení a obnovení, v určitých situacích jejich potlačení je oprávněné.</span><span class="sxs-lookup"><span data-stu-id="0a047-205">While it is recommended that you resolve all NuGet warnings during your pack and restore operations, in certain situations suppressing them is warranted.</span></span>
<span data-ttu-id="0a047-206">Chcete-li potlačit celý projekt upozornění, zvažte provedení:</span><span class="sxs-lookup"><span data-stu-id="0a047-206">To suppress a warning project wide, consider doing:</span></span>

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
    <NoWarn>$(NoWarn);NU5104</NoWarn>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1"/>
</ItemGroup>
```

<span data-ttu-id="0a047-207">Někdy se upozornění vztahují pouze na určitý balíček v grafu.</span><span class="sxs-lookup"><span data-stu-id="0a047-207">Sometimes warnings apply only to a certain package in the graph.</span></span> <span data-ttu-id="0a047-208">Můžeme se rozhodnout potlačit toto upozornění `NoWarn` selektivně přidáním položky PackageReference.</span><span class="sxs-lookup"><span data-stu-id="0a047-208">We can choose to suppress that warning more selectively by adding a `NoWarn` on the PackageReference item.</span></span> 

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1" NoWarn="NU1603" />
</ItemGroup>
```

#### <a name="suppressing-nuget-package-warnings-in-visual-studio"></a><span data-ttu-id="0a047-209">Potlačení upozornění balíčku NuGet v sadě Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0a047-209">Suppressing NuGet package warnings in Visual Studio</span></span>

<span data-ttu-id="0a047-210">Když v sadě Visual Studio, můžete také [potlačit upozornění](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) prostřednictvím ide.</span><span class="sxs-lookup"><span data-stu-id="0a047-210">When in Visual Studio, you can also [suppress warnings](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) through the IDE.</span></span>

## <a name="locking-dependencies"></a><span data-ttu-id="0a047-211">Zamykání závislostí</span><span class="sxs-lookup"><span data-stu-id="0a047-211">Locking dependencies</span></span>

<span data-ttu-id="0a047-212">*Tato funkce je k dispozici s NuGet **4.9** nebo vyšší a s Visual Studio 2017 **15.9** nebo vyšší.*</span><span class="sxs-lookup"><span data-stu-id="0a047-212">*This feature is available with NuGet **4.9** or above and with Visual Studio 2017 **15.9** or above.*</span></span>

<span data-ttu-id="0a047-213">Vstup do NuGet obnovení je sada odkazů na balíček ze souboru projektu (nejvyšší úrovně nebo přímé závislosti) a výstup je úplné uzavření všech závislostí balíčku, včetně přenositých závislostí.</span><span class="sxs-lookup"><span data-stu-id="0a047-213">Input to NuGet restore is a set of Package References from the project file (top-level or direct dependencies) and the output is a full closure of all the package dependencies including transitive dependencies.</span></span> <span data-ttu-id="0a047-214">NuGet se pokusí vždy vytvořit stejné úplné uzavření závislostí balíčku, pokud se nezměnil vstupní seznam PackageReference.</span><span class="sxs-lookup"><span data-stu-id="0a047-214">NuGet tries to always produce the same full closure of package dependencies if the input PackageReference list has not changed.</span></span> <span data-ttu-id="0a047-215">Existují však některé scénáře, kde není schopen tak učinit.</span><span class="sxs-lookup"><span data-stu-id="0a047-215">However, there are some scenarios where it is unable to do so.</span></span> <span data-ttu-id="0a047-216">Příklad:</span><span class="sxs-lookup"><span data-stu-id="0a047-216">For example:</span></span>

* <span data-ttu-id="0a047-217">Při použití plovoucí verze `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`jako .</span><span class="sxs-lookup"><span data-stu-id="0a047-217">When you use floating versions like `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span></span> <span data-ttu-id="0a047-218">Zatímco záměrem je zde plovoucí na nejnovější verzi na každé obnovení balíčků, existují scénáře, kde uživatelé vyžadují, aby graf být uzamčen na určitou nejnovější verzi a plovoucí na novější verzi, pokud je k dispozici, na explicitní gesto.</span><span class="sxs-lookup"><span data-stu-id="0a047-218">While the intention here is to float to the latest version on every restore of packages, there are scenarios where users require the graph to be locked to a certain latest version and float to a later version, if available, upon an explicit gesture.</span></span>
* <span data-ttu-id="0a047-219">Je publikována novější verze balíčku odpovídajícího požadavkům na verzi PackageReference.</span><span class="sxs-lookup"><span data-stu-id="0a047-219">A newer version of the package matching PackageReference version requirements is published.</span></span> <span data-ttu-id="0a047-220">Například</span><span class="sxs-lookup"><span data-stu-id="0a047-220">E.g.</span></span> 

  * <span data-ttu-id="0a047-221">Den 1: Pokud `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` jste zadali, ale verze dostupné v úložištích NuGet byly 4.1.0, 4.2.0 a 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="0a047-221">Day 1: if you specified `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` but the versions available on the NuGet repositories were 4.1.0, 4.2.0 and 4.3.0.</span></span> <span data-ttu-id="0a047-222">V tomto případě by NuGet vyřešeny na 4.1.0 (nejbližší minimální verze)</span><span class="sxs-lookup"><span data-stu-id="0a047-222">In this case, NuGet would have resolved to  4.1.0 (nearest minimum version)</span></span>

  * <span data-ttu-id="0a047-223">Den 2: Verze 4.0.0 dostane zveřejněny.</span><span class="sxs-lookup"><span data-stu-id="0a047-223">Day 2: Version 4.0.0 gets published.</span></span> <span data-ttu-id="0a047-224">NuGet nyní najde přesnou shodu a začne řešit na 4.0.0</span><span class="sxs-lookup"><span data-stu-id="0a047-224">NuGet will now find the exact match and start resolving to 4.0.0</span></span>

* <span data-ttu-id="0a047-225">Daná verze balíčku je odebrána z úložiště.</span><span class="sxs-lookup"><span data-stu-id="0a047-225">A given package version is removed from the repository.</span></span> <span data-ttu-id="0a047-226">Přestože nuget.org neumožňuje odstranění balíčků, ne všechny úložiště balíčků mají tato omezení.</span><span class="sxs-lookup"><span data-stu-id="0a047-226">Though nuget.org does not allow package deletions, not all package repositories have this constraints.</span></span> <span data-ttu-id="0a047-227">To má za následek NuGet hledání nejlepší shody, když nelze přeložit na odstraněnou verzi.</span><span class="sxs-lookup"><span data-stu-id="0a047-227">This results in NuGet finding the best match when it cannot resolve to the deleted version.</span></span>

### <a name="enabling-lock-file"></a><span data-ttu-id="0a047-228">Povolení souboru zámku</span><span class="sxs-lookup"><span data-stu-id="0a047-228">Enabling lock file</span></span>

<span data-ttu-id="0a047-229">Chcete-li zachovat úplné uzavření závislostí balíčků, můžete se přihlásit k funkci uzamčení souboru nastavením vlastnosti `RestorePackagesWithLockFile` MSBuild pro váš projekt:</span><span class="sxs-lookup"><span data-stu-id="0a047-229">In order to persist the full closure of package dependencies you can opt-in to the lock file feature by setting the MSBuild property `RestorePackagesWithLockFile` for your project:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="0a047-230">Pokud je tato vlastnost nastavena, Obnovení NuGet vygeneruje soubor zámku - `packages.lock.json` soubor v kořenovém adresáři projektu, který obsahuje seznam všech závislostí balíčku.</span><span class="sxs-lookup"><span data-stu-id="0a047-230">If this property is set, NuGet restore will generate a lock file - `packages.lock.json` file at the project root directory that lists all the package dependencies.</span></span> 

> [!Note]
> <span data-ttu-id="0a047-231">Jakmile má `packages.lock.json` projekt soubor v kořenovém adresáři, soubor zámku `RestorePackagesWithLockFile` se vždy používá s obnovením i v případě, že vlastnost není nastavena.</span><span class="sxs-lookup"><span data-stu-id="0a047-231">Once a project has `packages.lock.json` file in its root directory, the lock file is always used with restore even if the property `RestorePackagesWithLockFile` is not set.</span></span> <span data-ttu-id="0a047-232">Takže další způsob, jak se přihlásit k této `packages.lock.json` funkci, je vytvořit fiktivní prázdný soubor v kořenovém adresáři projektu.</span><span class="sxs-lookup"><span data-stu-id="0a047-232">So another way to opt-in to this feature is to create a dummy blank `packages.lock.json` file in the project's root directory.</span></span>

### <a name="restore-behavior-with-lock-file"></a><span data-ttu-id="0a047-233">`restore`chování se souborem zámku</span><span class="sxs-lookup"><span data-stu-id="0a047-233">`restore` behavior with lock file</span></span>
<span data-ttu-id="0a047-234">Pokud je pro projekt k dispozici soubor zámku, `restore`použije nuget tento soubor zámku ke spuštění .</span><span class="sxs-lookup"><span data-stu-id="0a047-234">If a lock file is present for project, NuGet uses this lock file to run `restore`.</span></span> <span data-ttu-id="0a047-235">NuGet provádí rychlou kontrolu, zda došlo k nějaké změny v závislostech balíčku, jak je uvedeno v souboru projektu (nebo soubory závislé projekty) a pokud nedošlo k žádné změny pouze obnoví balíčky uvedené v souboru zámku.</span><span class="sxs-lookup"><span data-stu-id="0a047-235">NuGet does a quick check to see if there were any changes in the package dependencies as mentioned in the project file (or dependent projects' files) and if there were no changes it just restores the packages mentioned in the lock file.</span></span> <span data-ttu-id="0a047-236">Neexistuje žádné přehodnocení závislostí balíčků.</span><span class="sxs-lookup"><span data-stu-id="0a047-236">There is no re-evaluation of package dependencies.</span></span>

<span data-ttu-id="0a047-237">Pokud NuGet zjistí změnu definovaných závislostí, jak je uvedeno v souboru projektu, přehodnotí graf balíčku a aktualizuje soubor zámku tak, aby odrážel nové uzavření balíčku pro projekt.</span><span class="sxs-lookup"><span data-stu-id="0a047-237">If NuGet detects a change in the defined dependencies as mentioned in the project file(s), it re-evaluates the package graph and updates the lock file to reflect the new package closure for the project.</span></span>

<span data-ttu-id="0a047-238">Pro CI/CD a další scénáře, kde byste nechtěli měnit závislosti balíčků za běhu, `lockedmode` `true`můžete tak učinit nastavením na :</span><span class="sxs-lookup"><span data-stu-id="0a047-238">For CI/CD and other scenarios, where you would not want to change the package dependencies on the fly, you can do so by setting the `lockedmode` to `true`:</span></span>

<span data-ttu-id="0a047-239">Pro dotnet.exe spusťte:</span><span class="sxs-lookup"><span data-stu-id="0a047-239">For dotnet.exe, run:</span></span>

```
> dotnet.exe restore --locked-mode
```

<span data-ttu-id="0a047-240">Pro msbuild.exe spusťte:</span><span class="sxs-lookup"><span data-stu-id="0a047-240">For msbuild.exe, run:</span></span>

```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

<span data-ttu-id="0a047-241">Tuto podmíněnou vlastnost MSBuild můžete také nastavit v souboru projektu:</span><span class="sxs-lookup"><span data-stu-id="0a047-241">You may also set this conditional MSBuild property in your project file:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

<span data-ttu-id="0a047-242">Pokud je `true`uzamčen režim , obnovení buď obnoví přesné balíčky, jak jsou uvedeny v souboru zámku, nebo se nezdaří, pokud jste aktualizovali definované závislosti balíčků pro projekt po vytvoření souboru zámku.</span><span class="sxs-lookup"><span data-stu-id="0a047-242">If locked mode is `true`, restore will either restore the exact packages as listed in the lock file or fail if you updated the defined package dependencies for the project after lock file was created.</span></span>

### <a name="make-lock-file-part-of-your-source-repository"></a><span data-ttu-id="0a047-243">Nastavení souboru zámku do zdrojového úložiště</span><span class="sxs-lookup"><span data-stu-id="0a047-243">Make lock file part of your source repository</span></span>
<span data-ttu-id="0a047-244">Pokud vytváříte aplikaci, spustitelný soubor a dotyčný projekt je na začátku řetězce závislostí, pak zkontrolujte soubor zámku do úložiště zdrojového kódu, aby jej NuGet mohl využít během obnovení.</span><span class="sxs-lookup"><span data-stu-id="0a047-244">If you are building an application, an executable and the project in question is at the start of the dependency chain then do check in the lock file to the source code repository so that NuGet can make use of it during restore.</span></span>

<span data-ttu-id="0a047-245">Pokud je však projekt projekt knihovny, který nedodáváte, nebo projekt společného kódu, na kterém závisí jiné projekty, **neměli** byste zamykat soubor jako součást zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="0a047-245">However, if your project is a library project that you do not ship or a common code project on which other projects depend upon, you **should not** check in the lock file as part of your source code.</span></span> <span data-ttu-id="0a047-246">Neexistuje žádná náhrada zachycování souboru zámku, ale uzamčený balíček závislostí pro společný kód projektu nemusí být použity, jak je uvedeno v souboru zámku, během obnovení nebo sestavení projektu, který závisí na tomto projektu společného kódu.</span><span class="sxs-lookup"><span data-stu-id="0a047-246">There is no harm in keeping the lock file but the locked package dependencies for the common code project may not be used, as listed in the lock file, during the restore/build of a project that depends on this common-code project.</span></span>

<span data-ttu-id="0a047-247">Např.</span><span class="sxs-lookup"><span data-stu-id="0a047-247">Eg.</span></span>

```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```

<span data-ttu-id="0a047-248">Pokud `ProjectA` má závislost na `PackageX` `2.0.0` verzi a `ProjectB` také odkazy, `1.0.0`které závisí na `ProjectB` `PackageX` verzi , pak `PackageX` `1.0.0`soubor zámku pro bude seznam závislost na verzi .</span><span class="sxs-lookup"><span data-stu-id="0a047-248">If `ProjectA` has a dependency on a `PackageX` version `2.0.0` and also references `ProjectB` that depends on `PackageX` version `1.0.0`, then the lock file for `ProjectB` will list a dependency on `PackageX` version `1.0.0`.</span></span> <span data-ttu-id="0a047-249">Však `ProjectA` při vytvoření, jeho zámek soubor bude `PackageX` **`2.0.0`** obsahovat závislost na verzi `ProjectB`a **není** `1.0.0` uvedeno v souboru zámku pro .</span><span class="sxs-lookup"><span data-stu-id="0a047-249">However, when `ProjectA` is built, its lock file will contain a dependency on `PackageX` version **`2.0.0`** and **not** `1.0.0` as listed in the lock file for `ProjectB`.</span></span> <span data-ttu-id="0a047-250">Proto zámek soubor uspolečného projektu kódu má málo co říci nad balíčky vyřešen pro projekty, které jsou na něm závislé.</span><span class="sxs-lookup"><span data-stu-id="0a047-250">Thus, the lock file of a common code project has little say over the packages resolved for projects that depend on it.</span></span>

### <a name="lock-file-extensibility"></a><span data-ttu-id="0a047-251">Rozšiřitelnost souboru zamykat</span><span class="sxs-lookup"><span data-stu-id="0a047-251">Lock file extensibility</span></span>

<span data-ttu-id="0a047-252">Můžete řídit různé chování obnovení pomocí souboru zámku, jak je popsáno níže:</span><span class="sxs-lookup"><span data-stu-id="0a047-252">You can control various behaviors of restore with lock file as described below:</span></span>

| <span data-ttu-id="0a047-253">NuGet.exe, volba</span><span class="sxs-lookup"><span data-stu-id="0a047-253">NuGet.exe option</span></span> | <span data-ttu-id="0a047-254">dotnet, volba</span><span class="sxs-lookup"><span data-stu-id="0a047-254">dotnet option</span></span> | <span data-ttu-id="0a047-255">Ekvivalentní možnost MSBuild</span><span class="sxs-lookup"><span data-stu-id="0a047-255">MSBuild equivalent option</span></span> | <span data-ttu-id="0a047-256">Popis</span><span class="sxs-lookup"><span data-stu-id="0a047-256">Description</span></span> |
|:--- |:--- |:--- |:--- |
| `-UseLockFile` |`--use-lock-file` | <span data-ttu-id="0a047-257">ObnovitPackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="0a047-257">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="0a047-258">Přihlásí se k použití souboru zámku.</span><span class="sxs-lookup"><span data-stu-id="0a047-258">Opts into the usage of a lock file.</span></span> |
| `-LockedMode` | `--locked-mode` | <span data-ttu-id="0a047-259">Obnovit uzamčený režim</span><span class="sxs-lookup"><span data-stu-id="0a047-259">RestoreLockedMode</span></span> | <span data-ttu-id="0a047-260">Povolí uzamčený režim pro obnovení.</span><span class="sxs-lookup"><span data-stu-id="0a047-260">Enables locked mode for restore.</span></span> <span data-ttu-id="0a047-261">To je užitečné ve scénářích CI/CD, kde chcete opakovatelné sestavení.</span><span class="sxs-lookup"><span data-stu-id="0a047-261">This is useful in CI/CD scenarios where you want repeatable builds.</span></span>|   
| `-ForceEvaluate` | `--force-evaluate` | <span data-ttu-id="0a047-262">ObnovitVyhodnocení síly</span><span class="sxs-lookup"><span data-stu-id="0a047-262">RestoreForceEvaluate</span></span> | <span data-ttu-id="0a047-263">Tato možnost je užitečná u balíčků s plovoucí verzí definovanou v projektu.</span><span class="sxs-lookup"><span data-stu-id="0a047-263">This option is useful with packages with floating version defined in the project.</span></span> <span data-ttu-id="0a047-264">Ve výchozím nastavení NuGet obnovení nebude aktualizovat verzi balíčku automaticky při každém obnovení, pokud spustíte obnovení s touto možností.</span><span class="sxs-lookup"><span data-stu-id="0a047-264">By default, NuGet restore will not update the package version automatically upon each restore unless you run restore with this option.</span></span> |
| `-LockFilePath` | `--lock-file-path` | <span data-ttu-id="0a047-265">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="0a047-265">NuGetLockFilePath</span></span> | <span data-ttu-id="0a047-266">Definuje vlastní umístění souboru zámku pro projekt.</span><span class="sxs-lookup"><span data-stu-id="0a047-266">Defines a custom lock file location for a project.</span></span> <span data-ttu-id="0a047-267">Ve výchozím nastavení `packages.lock.json` podporuje NuGet v kořenovém adresáři.</span><span class="sxs-lookup"><span data-stu-id="0a047-267">By default, NuGet supports `packages.lock.json` at the root directory.</span></span> <span data-ttu-id="0a047-268">Pokud máte více projektů ve stejném adresáři, NuGet podporuje soubor uzamčení specifické pro projekt`packages.<project_name>.lock.json`</span><span class="sxs-lookup"><span data-stu-id="0a047-268">If you have multiple projects in the same directory, NuGet supports project specific lock file `packages.<project_name>.lock.json`</span></span> |
