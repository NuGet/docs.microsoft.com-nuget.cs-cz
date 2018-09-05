---
title: Formát NuGet PackageReference (odkazy na balíček v souborech projektu)
description: Podrobnosti na NuGet PackageReference v souborech projektu podporuje NuGet 4.0 + a VS2017 a .NET Core 2.0
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 9ae8e8dc4e7e901acacffed8b7dfb4162c5ad2b6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551387"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="5b9b2-103">Odkazy na balíček (PackageReference) v souborech projektu</span><span class="sxs-lookup"><span data-stu-id="5b9b2-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="5b9b2-104">Balíček odkazů pomocí nástroje `PackageReference` uzlu, správě závislostí NuGet přímo v rámci projektových souborů (na rozdíl od samostatné `packages.config` souboru).</span><span class="sxs-lookup"><span data-stu-id="5b9b2-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="5b9b2-105">Pomocí PackageReference, jako je volána, nemá vliv na ostatní aspekty NuGet; například nastavení v `NuGet.Config` soubory (včetně zdroje balíčků) se uplatní, jak je vysvětleno v [konfigurace chování Nugetu](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="5b9b2-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="5b9b2-106">S PackageReference můžete také použít podmínky nástroje MSBuild zvolit odkazy na balíček na cílovou architekturu, konfigurace, platformy nebo další seskupení.</span><span class="sxs-lookup"><span data-stu-id="5b9b2-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="5b9b2-107">Umožňuje také pro detailní kontrolu nad závislostí a obsahu toku.</span><span class="sxs-lookup"><span data-stu-id="5b9b2-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="5b9b2-108">(Další podrobnosti najdete v [NuGet aktualizací Service pack a obnovení jako cílů MSBuild](../reference/msbuild-targets.md).)</span><span class="sxs-lookup"><span data-stu-id="5b9b2-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

<span data-ttu-id="5b9b2-109">Ve výchozím nastavení je použít PackageReference pro projekty .NET Core, .NET Standard projekty a projekty UPW cílení na Windows 10 sestavení 15063 (Creators Update) a novější, s výjimkou projekty C++ UWP.</span><span class="sxs-lookup"><span data-stu-id="5b9b2-109">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="5b9b2-110">Projekty .NET framework úplné podporují PackageReference, ale nyní jako výchozí `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="5b9b2-110">.NET full framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="5b9b2-111">Použití PackageReference migrovat závislosti z `packages.config` do souboru projektu, odstraňte soubor packages.config.</span><span class="sxs-lookup"><span data-stu-id="5b9b2-111">To use PackageReference, migrate the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="5b9b2-112">Přidávání PackageReference</span><span class="sxs-lookup"><span data-stu-id="5b9b2-112">Adding a PackageReference</span></span>

<span data-ttu-id="5b9b2-113">Přidáte závislost v souboru projektu pomocí následující syntaxe:</span><span class="sxs-lookup"><span data-stu-id="5b9b2-113">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="5b9b2-114">Řízení verze závislosti</span><span class="sxs-lookup"><span data-stu-id="5b9b2-114">Controlling dependency version</span></span>

<span data-ttu-id="5b9b2-115">Konvence pro určení verze balíčku je stejný jako při použití `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="5b9b2-115">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="5b9b2-116">V předchozím příkladu 3.6.0 znamená, že všechny verze, která je > = 3.6.0 s předností nejnižší verze, jak je popsáno na [Správa verzí balíčků](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="5b9b2-116">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="5b9b2-117">Pomocí projektu s PackageReferences žádné PackageReference</span><span class="sxs-lookup"><span data-stu-id="5b9b2-117">Using PackageReference for a project with no PackageReferences</span></span>
<span data-ttu-id="5b9b2-118">Pokročilé: Pokud jste žádné balíčky nainstalované v projektu (žádné PackageReferences v souboru projektu) a žádný soubor packages.config, ale chcete projekt tak, aby se obnovit jako PackageReference styl, můžete nastavit vlastnost RestoreProjectStyle projektu na PackageReference v váš soubor projektu.</span><span class="sxs-lookup"><span data-stu-id="5b9b2-118">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
<span data-ttu-id="5b9b2-119">To může být užitečné, pokud se budete odkazovat na projekty, které jsou PackageReference ve stylu (existující csproj nebo projekty založenými na sadu SDK).</span><span class="sxs-lookup"><span data-stu-id="5b9b2-119">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="5b9b2-120">Tato možnost povolí balíčky, které odkazují tyto projekty, do "přechodně" odkazuje váš projekt.</span><span class="sxs-lookup"><span data-stu-id="5b9b2-120">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="floating-versions"></a><span data-ttu-id="5b9b2-121">Plovoucí verze</span><span class="sxs-lookup"><span data-stu-id="5b9b2-121">Floating Versions</span></span>

<span data-ttu-id="5b9b2-122">[Plovoucí verze](../consume-packages/dependency-resolution.md#floating-versions) podporují `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="5b9b2-122">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="5b9b2-123">Řízení závislosti prostředků</span><span class="sxs-lookup"><span data-stu-id="5b9b2-123">Controlling dependency assets</span></span>

<span data-ttu-id="5b9b2-124">Může používat závislost čistě jako vývojové prostředí a nemusí chcete je zveřejnit, která do projektů, které budou využívat vašeho balíčku.</span><span class="sxs-lookup"><span data-stu-id="5b9b2-124">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="5b9b2-125">V tomto scénáři můžete použít `PrivateAssets` metadat a řídit tak toto chování.</span><span class="sxs-lookup"><span data-stu-id="5b9b2-125">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="5b9b2-126">Následující značky metadat určovat závislost prostředky:</span><span class="sxs-lookup"><span data-stu-id="5b9b2-126">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="5b9b2-127">Značka</span><span class="sxs-lookup"><span data-stu-id="5b9b2-127">Tag</span></span> | <span data-ttu-id="5b9b2-128">Popis</span><span class="sxs-lookup"><span data-stu-id="5b9b2-128">Description</span></span> | <span data-ttu-id="5b9b2-129">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="5b9b2-129">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5b9b2-130">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="5b9b2-130">IncludeAssets</span></span> | <span data-ttu-id="5b9b2-131">Tyto prostředky budou využívat.</span><span class="sxs-lookup"><span data-stu-id="5b9b2-131">These assets will be consumed</span></span> | <span data-ttu-id="5b9b2-132">všechny</span><span class="sxs-lookup"><span data-stu-id="5b9b2-132">all</span></span> |
| <span data-ttu-id="5b9b2-133">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="5b9b2-133">ExcludeAssets</span></span> | <span data-ttu-id="5b9b2-134">Tyto prostředky nebude využívat.</span><span class="sxs-lookup"><span data-stu-id="5b9b2-134">These assets will not be consumed</span></span> | <span data-ttu-id="5b9b2-135">žádná</span><span class="sxs-lookup"><span data-stu-id="5b9b2-135">none</span></span> |
| <span data-ttu-id="5b9b2-136">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="5b9b2-136">PrivateAssets</span></span> | <span data-ttu-id="5b9b2-137">Tyto prostředky budou využívat, ale nebude směrovat do nadřazeného projektu</span><span class="sxs-lookup"><span data-stu-id="5b9b2-137">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="5b9b2-138">contentfiles; analyzátory; sestavení</span><span class="sxs-lookup"><span data-stu-id="5b9b2-138">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="5b9b2-139">Povolené hodnoty pro tyto značky jsou následujícím způsobem s více hodnotami, které jsou odděleny středníkem s výjimkou s `all` a `none` který musí být uvedena samy o sobě:</span><span class="sxs-lookup"><span data-stu-id="5b9b2-139">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="5b9b2-140">Hodnota</span><span class="sxs-lookup"><span data-stu-id="5b9b2-140">Value</span></span> | <span data-ttu-id="5b9b2-141">Popis</span><span class="sxs-lookup"><span data-stu-id="5b9b2-141">Description</span></span> |
| --- | ---
| <span data-ttu-id="5b9b2-142">Kompilace</span><span class="sxs-lookup"><span data-stu-id="5b9b2-142">compile</span></span> | <span data-ttu-id="5b9b2-143">Obsah `lib` složky a ovládací prvky, jestli můžete zkompilovat váš projekt proti sestavení ve složce</span><span class="sxs-lookup"><span data-stu-id="5b9b2-143">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="5b9b2-144">modul runtime</span><span class="sxs-lookup"><span data-stu-id="5b9b2-144">runtime</span></span> | <span data-ttu-id="5b9b2-145">Obsah `lib` a `runtimes` složky a ovládací prvky, jestli tato sestavení bude zkopírována do sestavení výstupního adresáře</span><span class="sxs-lookup"><span data-stu-id="5b9b2-145">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="5b9b2-146">contentFiles</span><span class="sxs-lookup"><span data-stu-id="5b9b2-146">contentFiles</span></span> | <span data-ttu-id="5b9b2-147">Obsah `contentfiles` složky</span><span class="sxs-lookup"><span data-stu-id="5b9b2-147">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="5b9b2-148">sestavení</span><span class="sxs-lookup"><span data-stu-id="5b9b2-148">build</span></span> | <span data-ttu-id="5b9b2-149">Vlastnosti a cíle ve `build` složky</span><span class="sxs-lookup"><span data-stu-id="5b9b2-149">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="5b9b2-150">Analyzátory</span><span class="sxs-lookup"><span data-stu-id="5b9b2-150">analyzers</span></span> | <span data-ttu-id="5b9b2-151">Analyzátory .NET</span><span class="sxs-lookup"><span data-stu-id="5b9b2-151">.NET analyzers</span></span> |
| <span data-ttu-id="5b9b2-152">nativní</span><span class="sxs-lookup"><span data-stu-id="5b9b2-152">native</span></span> | <span data-ttu-id="5b9b2-153">Obsah `native` složky</span><span class="sxs-lookup"><span data-stu-id="5b9b2-153">Contents of the `native` folder</span></span> |
| <span data-ttu-id="5b9b2-154">žádná</span><span class="sxs-lookup"><span data-stu-id="5b9b2-154">none</span></span> | <span data-ttu-id="5b9b2-155">Žádná z výše uvedených se používají.</span><span class="sxs-lookup"><span data-stu-id="5b9b2-155">None of the above are used.</span></span> |
| <span data-ttu-id="5b9b2-156">všechny</span><span class="sxs-lookup"><span data-stu-id="5b9b2-156">all</span></span> | <span data-ttu-id="5b9b2-157">Všechny výš uvedené (s výjimkou `none`)</span><span class="sxs-lookup"><span data-stu-id="5b9b2-157">All of the above (except `none`)</span></span> |

<span data-ttu-id="5b9b2-158">V následujícím příkladu se všechno kromě soubory obsahu z balíčku by být využívány službou projektu a všechno, co s výjimkou souborů obsahu a analyzátory by tok na nadřazený projekt.</span><span class="sxs-lookup"><span data-stu-id="5b9b2-158">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="5b9b2-159">Upozorňujeme, že `build` není součástí `PrivateAssets`, zaměřuje a props *bude* tok, který nadřazeného projektu.</span><span class="sxs-lookup"><span data-stu-id="5b9b2-159">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="5b9b2-160">Zvažte například, že výše uvedené odkaz se používá v projektu, který vytvoří balíček NuGet s názvem AppLogger.</span><span class="sxs-lookup"><span data-stu-id="5b9b2-160">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="5b9b2-161">AppLogger může spotřebovat cíle a vlastnosti z `Contoso.Utility.UsefulStuff`, jak můžete projektech, které využívají AppLogger.</span><span class="sxs-lookup"><span data-stu-id="5b9b2-161">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="5b9b2-162">Přidání podmínky PackageReference</span><span class="sxs-lookup"><span data-stu-id="5b9b2-162">Adding a PackageReference condition</span></span>

<span data-ttu-id="5b9b2-163">Můžete použít podmínku pro ovládací prvek, jestli balíček je zahrnuta, pokud podmínky můžete použít jakoukoli proměnnou MSBuild nebo Proměnná definovaná v souboru cílů nebo vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="5b9b2-163">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="5b9b2-164">Ale v současnosti pouze `TargetFramework` proměnná je podporována.</span><span class="sxs-lookup"><span data-stu-id="5b9b2-164">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="5b9b2-165">Předpokládejme například, že vývoji cílíte `netstandard1.4` stejně jako `net452` , ale mají závislost, kterou lze použít pouze pro `net452`.</span><span class="sxs-lookup"><span data-stu-id="5b9b2-165">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="5b9b2-166">V tomto případě nechcete `netstandard1.4` projekt, který se spotřebovává balíček pro přidání tohoto zbytečné závislosti.</span><span class="sxs-lookup"><span data-stu-id="5b9b2-166">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="5b9b2-167">Chcete-li tomu zabránit, určíte podmínku na `PackageReference` následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="5b9b2-167">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="5b9b2-168">Balíček vytvořené pomocí tohoto projektu se zobrazí, že je jako závislost pouze pro Newtonsoft.Json `net452` cíl:</span><span class="sxs-lookup"><span data-stu-id="5b9b2-168">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![Výsledek použití podmínku na PackageReference s VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="5b9b2-170">Podmínek je také možné použít na `ItemGroup` úrovně a má platit pro všechny podřízené objekty `PackageReference` prvky:</span><span class="sxs-lookup"><span data-stu-id="5b9b2-170">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
