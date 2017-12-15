---
title: NuGet PackageReference v souborech projektu sady Visual Studio | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 5a554e9d-1266-48c2-92e8-6dd00b1d6810
description: Podrobnosti o NuGet PackageReference v souborech projektu podporuje NuGet 4.0 + a VS2017
keywords: "Závislosti balíčků NuGet, balíček odkazuje projektu soubory, PackageReference, souboru packages.config, project.json, VS2017, Visual Studio 2017, NuGet 4"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c8fc9e558557af444d9a35ace36d043a5f6382a7
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="e0f35-104">Balíček odkazuje (PackageReference) v souborech projektu</span><span class="sxs-lookup"><span data-stu-id="e0f35-104">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="e0f35-105">Balíček odkazů, pomocí `PackageReference` uzlu, umožňují spravovat závislosti NuGet přímo v rámci soubory projektu, místo nutnosti samostatné `packages.config` nebo `project.json` souboru.</span><span class="sxs-lookup"><span data-stu-id="e0f35-105">Package references, using the `PackageReference` node, allow you to manage NuGet dependencies directly within project files, rather than needing a separate `packages.config` or `project.json` file.</span></span> <span data-ttu-id="e0f35-106">Tato metoda neovlivňuje dalších aspektů NuGet; například nastavení v `NuGet.Config` soubory (včetně zdroje balíčků) jsou stále použít, jak je popsáno v [konfigurace chování NuGet](Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="e0f35-106">This method doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](Configuring-NuGet-Behavior.md).</span></span>

> [!Important]
> <span data-ttu-id="e0f35-107">V současné době balíček odkazuje jsou podporovány ve Visual Studio 2017 pouze pro projekty .NET Core, .NET Standard projekty a UWP projektech zacílených na Windows 10 sestavení 15063 (Creators aktualizace).</span><span class="sxs-lookup"><span data-stu-id="e0f35-107">At present, package references are supported in Visual Studio 2017 only, for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update).</span></span>

<span data-ttu-id="e0f35-108">`PackageReference` Přístup umožňuje používat podmínky nástroje MSBuild vybrat balíček odkazuje na cílové rozhraní, konfigurace, platformu nebo jiných seskupení.</span><span class="sxs-lookup"><span data-stu-id="e0f35-108">The `PackageReference` approach allows you to use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="e0f35-109">Umožňuje také pro jemně odstupňovanou kontrolu nad závislosti a obsahu toku.</span><span class="sxs-lookup"><span data-stu-id="e0f35-109">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="e0f35-110">Z hlediska chování a [řešení závislostí](Dependency-Resolution.md), je stejná jako `project.json`.</span><span class="sxs-lookup"><span data-stu-id="e0f35-110">In terms of behavior and [dependency resolution](Dependency-Resolution.md), it is the same as using `project.json`.</span></span>

<span data-ttu-id="e0f35-111">Další informace o integraci s odkazů balíčku v souborech projektu nástroje MSBuild v [NuGet pack a obnovit jako cíle MSBuild](../schema/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="e0f35-111">For more details on the integration of MSBuild with package references in project files, see [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md).</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="e0f35-112">Přidání PackageReference</span><span class="sxs-lookup"><span data-stu-id="e0f35-112">Adding a PackageReference</span></span>

<span data-ttu-id="e0f35-113">Přidáte závislost v souboru projektu pomocí následující syntaxe:</span><span class="sxs-lookup"><span data-stu-id="e0f35-113">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />    
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="e0f35-114">Řízení verze závislosti</span><span class="sxs-lookup"><span data-stu-id="e0f35-114">Controlling dependency version</span></span>

<span data-ttu-id="e0f35-115">Konvence pro určení verze balíčku je stejný jako při použití `packages.config` nebo `project.json`:</span><span class="sxs-lookup"><span data-stu-id="e0f35-115">The convention for specifying the version of a package is the same as when using `packages.config` or `project.json`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="e0f35-116">V předchozím příkladu 3.6.0 znamená všechny verze, která je > = 3.6.0 s předvolby pro nejnižší verze, jak je popsáno na [Správa verzí balíčku](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="e0f35-116">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="floating-versions"></a><span data-ttu-id="e0f35-117">Plovoucí verze</span><span class="sxs-lookup"><span data-stu-id="e0f35-117">Floating Versions</span></span>

<span data-ttu-id="e0f35-118">[Plovoucí verze](../consume-packages/dependency-resolution.md#floating-versions) podporují `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="e0f35-118">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="e0f35-119">Řízení závislostí prostředky</span><span class="sxs-lookup"><span data-stu-id="e0f35-119">Controlling dependency assets</span></span>

<span data-ttu-id="e0f35-120">Může používat závislost čistě jako harness vývoj a nemusí chtějí zpřístupnit, projekty, které bude využívat vašeho balíčku.</span><span class="sxs-lookup"><span data-stu-id="e0f35-120">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="e0f35-121">V tomto scénáři můžete použít `PrivateAssets` metadata, aby bylo toto chování.</span><span class="sxs-lookup"><span data-stu-id="e0f35-121">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="e0f35-122">Následující značky metadata řídit prostředky závislost:</span><span class="sxs-lookup"><span data-stu-id="e0f35-122">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="e0f35-123">Značka</span><span class="sxs-lookup"><span data-stu-id="e0f35-123">Tag</span></span> | <span data-ttu-id="e0f35-124">Popis</span><span class="sxs-lookup"><span data-stu-id="e0f35-124">Description</span></span> | <span data-ttu-id="e0f35-125">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="e0f35-125">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e0f35-126">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="e0f35-126">IncludeAssets</span></span> | <span data-ttu-id="e0f35-127">Tyto prostředky budou využívat.</span><span class="sxs-lookup"><span data-stu-id="e0f35-127">These assets will be consumed</span></span> | <span data-ttu-id="e0f35-128">všechny</span><span class="sxs-lookup"><span data-stu-id="e0f35-128">all</span></span> |
| <span data-ttu-id="e0f35-129">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="e0f35-129">ExcludeAssets</span></span> | <span data-ttu-id="e0f35-130">Tyto prostředky nebudou využívat.</span><span class="sxs-lookup"><span data-stu-id="e0f35-130">These assets will not be consumed</span></span> | <span data-ttu-id="e0f35-131">žádná</span><span class="sxs-lookup"><span data-stu-id="e0f35-131">none</span></span> | 
| <span data-ttu-id="e0f35-132">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="e0f35-132">PrivateAssets</span></span> | <span data-ttu-id="e0f35-133">Tyto prostředky budou využívat, ale nebude tok nadřazený projekt</span><span class="sxs-lookup"><span data-stu-id="e0f35-133">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="e0f35-134">contentfiles; analyzátorů; sestavení</span><span class="sxs-lookup"><span data-stu-id="e0f35-134">contentfiles;analyzers;build</span></span> |


<span data-ttu-id="e0f35-135">Povolené hodnoty pro tyto značky jsou následující, s více hodnotami, které jsou odděleny středníkem kromě s `all` a `none` která se musí nacházet ve vlastní účet:</span><span class="sxs-lookup"><span data-stu-id="e0f35-135">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="e0f35-136">Hodnota</span><span class="sxs-lookup"><span data-stu-id="e0f35-136">Value</span></span> | <span data-ttu-id="e0f35-137">Popis</span><span class="sxs-lookup"><span data-stu-id="e0f35-137">Description</span></span> |
| --- | ---
| <span data-ttu-id="e0f35-138">Kompilace</span><span class="sxs-lookup"><span data-stu-id="e0f35-138">compile</span></span> | <span data-ttu-id="e0f35-139">Obsah `lib` složky</span><span class="sxs-lookup"><span data-stu-id="e0f35-139">Contents of the `lib` folder</span></span> |
| <span data-ttu-id="e0f35-140">modul runtime</span><span class="sxs-lookup"><span data-stu-id="e0f35-140">runtime</span></span> | <span data-ttu-id="e0f35-141">Obsah `runtime` složky</span><span class="sxs-lookup"><span data-stu-id="e0f35-141">Contents of the `runtime` folder</span></span> |
| <span data-ttu-id="e0f35-142">contentFiles</span><span class="sxs-lookup"><span data-stu-id="e0f35-142">contentFiles</span></span> | <span data-ttu-id="e0f35-143">Obsah `contentfiles` složky</span><span class="sxs-lookup"><span data-stu-id="e0f35-143">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="e0f35-144">sestavení</span><span class="sxs-lookup"><span data-stu-id="e0f35-144">build</span></span> | <span data-ttu-id="e0f35-145">Props a cílem v `build` složky</span><span class="sxs-lookup"><span data-stu-id="e0f35-145">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="e0f35-146">Analyzátory</span><span class="sxs-lookup"><span data-stu-id="e0f35-146">analyzers</span></span> | <span data-ttu-id="e0f35-147">Analyzátory rozhraní .NET</span><span class="sxs-lookup"><span data-stu-id="e0f35-147">.NET analyzers</span></span> |
| <span data-ttu-id="e0f35-148">nativní</span><span class="sxs-lookup"><span data-stu-id="e0f35-148">native</span></span> | <span data-ttu-id="e0f35-149">Obsah `native` složky</span><span class="sxs-lookup"><span data-stu-id="e0f35-149">Contents of the `native` folder</span></span> |
| <span data-ttu-id="e0f35-150">žádná</span><span class="sxs-lookup"><span data-stu-id="e0f35-150">none</span></span> | <span data-ttu-id="e0f35-151">Žádná z výše uvedeného se používají.</span><span class="sxs-lookup"><span data-stu-id="e0f35-151">None of the above are used.</span></span> |
| <span data-ttu-id="e0f35-152">všechny</span><span class="sxs-lookup"><span data-stu-id="e0f35-152">all</span></span> | <span data-ttu-id="e0f35-153">Všechny výše uvedené (s výjimkou `none`)</span><span class="sxs-lookup"><span data-stu-id="e0f35-153">All of the above (except `none`)</span></span> |

<span data-ttu-id="e0f35-154">V následujícím příkladu se všechno kromě soubory z balíčku obsahu by být využívány službou projektu a všechno kromě souborů obsahu a analyzátory by tok nadřazený projekt.</span><span class="sxs-lookup"><span data-stu-id="e0f35-154">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="e0f35-155">Všimněte si, že protože `build` není součástí `PrivateAssets`, cílem a props *bude* toku nadřazený projekt.</span><span class="sxs-lookup"><span data-stu-id="e0f35-155">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="e0f35-156">Například vezměte v úvahu, že odkaz na výše uvedené se používá v projektu, který NuGet balíček s názvem AppLogger sestavení.</span><span class="sxs-lookup"><span data-stu-id="e0f35-156">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="e0f35-157">AppLogger spotřebovat cílů a props z `Contoso.Utility.UsefulStuff`, jak můžete projekty, které využívají AppLogger.</span><span class="sxs-lookup"><span data-stu-id="e0f35-157">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="e0f35-158">Přidáním PackageReference podmínky</span><span class="sxs-lookup"><span data-stu-id="e0f35-158">Adding a PackageReference condition</span></span>

<span data-ttu-id="e0f35-159">Můžete vytvořit podmínku, kterou chcete řízení a zda balíček je součástí, kde podmínky můžete použít všechny nástroje MSBuild proměnná nebo Proměnná definovaná v souboru cíle nebo props.</span><span class="sxs-lookup"><span data-stu-id="e0f35-159">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="e0f35-160">Ale na v současné době pouze `TargetFramework` proměnné je podporována.</span><span class="sxs-lookup"><span data-stu-id="e0f35-160">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="e0f35-161">Řekněme například, že cílení `netstandard1.4` a také `net452` , ale mají závislost, kterou lze použít pouze u `net452`.</span><span class="sxs-lookup"><span data-stu-id="e0f35-161">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="e0f35-162">V takovém případě nechcete, aby `netstandard1.4` projekt, který využívá vašeho balíčku pro přidání tohoto nepotřebné závislosti.</span><span class="sxs-lookup"><span data-stu-id="e0f35-162">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="e0f35-163">Chcete-li tomu zabránit, zadejte podmínku na `PackageReference` následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="e0f35-163">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />    
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="e0f35-164">Balíček vytvořená s využitím tohoto projektu se zobrazí, zda jsou zahrnuty jako závislost pouze pro Newtonsoft.json `net452` cíl:</span><span class="sxs-lookup"><span data-stu-id="e0f35-164">A package built using this project will show that Newtonsoft.json is included as a dependency only for a `net452` target:</span></span>

![Výsledek použití podmínku na PackageReference s VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="e0f35-166">Podmínky lze použít také v `ItemGroup` úrovni a budou platit pro všechny podřízené objekty `PackageReference` prvky:</span><span class="sxs-lookup"><span data-stu-id="e0f35-166">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
