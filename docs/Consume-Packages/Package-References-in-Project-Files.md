---
title: Formát NuGet PackageReference (odkazů balíčku v souborech projektu) | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/16/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Podrobnosti o NuGet PackageReference v souborech projektu podporuje NuGet 4.0 + a VS2017 a .NET Core 2.0
keywords: Závislosti balíčků NuGet, balíček odkazuje projektu soubory, PackageReference, souboru packages.config, VS2017, Visual Studio 2017, NuGet 4, .NET Core 2.0
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 99caf371ca1bd85e6af4e879741e3e2caab6e860
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="5ad18-104">Balíček odkazuje (PackageReference) v souborech projektu</span><span class="sxs-lookup"><span data-stu-id="5ad18-104">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="5ad18-105">Balíček odkazů, pomocí `PackageReference` uzlu, Správa závislostí NuGet přímo v souborech projektu (oproti samostatné `packages.config` souboru).</span><span class="sxs-lookup"><span data-stu-id="5ad18-105">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="5ad18-106">Použití PackageReference, jako je volána, nemá vliv dalších aspektů NuGet; například nastavení v `NuGet.Config` soubory (včetně zdroje balíčků) jsou stále použít, jak je popsáno v [konfigurace chování NuGet](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="5ad18-106">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="5ad18-107">S PackageReference můžete taky podmínky nástroje MSBuild vybrat balíček odkazuje na cílové rozhraní, konfigurace, platformu nebo jiných seskupení.</span><span class="sxs-lookup"><span data-stu-id="5ad18-107">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="5ad18-108">Umožňuje také pro jemně odstupňovanou kontrolu nad závislosti a obsahu toku.</span><span class="sxs-lookup"><span data-stu-id="5ad18-108">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="5ad18-109">(Další podrobnosti najdete v [NuGet pack a obnovit jako cíle MSBuild](../reference/msbuild-targets.md).)</span><span class="sxs-lookup"><span data-stu-id="5ad18-109">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

<span data-ttu-id="5ad18-110">Ve výchozím nastavení PackageReference se používá pro projekty .NET Core, .NET Standard projekty a UWP projektech zacílených na Windows 10 sestavení 15063 (Creators aktualizace) a novější, s výjimkou projektů C++ UWP.</span><span class="sxs-lookup"><span data-stu-id="5ad18-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="5ad18-111">Projekty rozhraní .NET framework úplnou podporu PackageReference, ale aktuálně výchozí `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="5ad18-111">.NET full framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="5ad18-112">Chcete-li použít PackageReference, migrujte závislostí z `packages.config` v souboru projektu odeberte souboru Packages.config je.</span><span class="sxs-lookup"><span data-stu-id="5ad18-112">To use PackageReference, migrate the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="5ad18-113">Přidání PackageReference</span><span class="sxs-lookup"><span data-stu-id="5ad18-113">Adding a PackageReference</span></span>

<span data-ttu-id="5ad18-114">Přidáte závislost v souboru projektu pomocí následující syntaxe:</span><span class="sxs-lookup"><span data-stu-id="5ad18-114">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="5ad18-115">Řízení verze závislosti</span><span class="sxs-lookup"><span data-stu-id="5ad18-115">Controlling dependency version</span></span>

<span data-ttu-id="5ad18-116">Konvence pro určení verze balíčku je stejný jako při použití `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="5ad18-116">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="5ad18-117">V předchozím příkladu 3.6.0 znamená všechny verze, která je > = 3.6.0 s předvolby pro nejnižší verze, jak je popsáno na [Správa verzí balíčku](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="5ad18-117">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="floating-versions"></a><span data-ttu-id="5ad18-118">Plovoucí verze</span><span class="sxs-lookup"><span data-stu-id="5ad18-118">Floating Versions</span></span>

<span data-ttu-id="5ad18-119">[Plovoucí verze](../consume-packages/dependency-resolution.md#floating-versions) podporují `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="5ad18-119">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="5ad18-120">Řízení závislostí prostředky</span><span class="sxs-lookup"><span data-stu-id="5ad18-120">Controlling dependency assets</span></span>

<span data-ttu-id="5ad18-121">Může používat závislost čistě jako harness vývoj a nemusí chtějí zpřístupnit, projekty, které bude využívat vašeho balíčku.</span><span class="sxs-lookup"><span data-stu-id="5ad18-121">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="5ad18-122">V tomto scénáři můžete použít `PrivateAssets` metadata, aby bylo toto chování.</span><span class="sxs-lookup"><span data-stu-id="5ad18-122">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="5ad18-123">Následující značky metadata řídit prostředky závislost:</span><span class="sxs-lookup"><span data-stu-id="5ad18-123">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="5ad18-124">Značka</span><span class="sxs-lookup"><span data-stu-id="5ad18-124">Tag</span></span> | <span data-ttu-id="5ad18-125">Popis</span><span class="sxs-lookup"><span data-stu-id="5ad18-125">Description</span></span> | <span data-ttu-id="5ad18-126">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="5ad18-126">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5ad18-127">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="5ad18-127">IncludeAssets</span></span> | <span data-ttu-id="5ad18-128">Tyto prostředky budou využívat.</span><span class="sxs-lookup"><span data-stu-id="5ad18-128">These assets will be consumed</span></span> | <span data-ttu-id="5ad18-129">všechny</span><span class="sxs-lookup"><span data-stu-id="5ad18-129">all</span></span> |
| <span data-ttu-id="5ad18-130">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="5ad18-130">ExcludeAssets</span></span> | <span data-ttu-id="5ad18-131">Tyto prostředky nebudou využívat.</span><span class="sxs-lookup"><span data-stu-id="5ad18-131">These assets will not be consumed</span></span> | <span data-ttu-id="5ad18-132">žádná</span><span class="sxs-lookup"><span data-stu-id="5ad18-132">none</span></span> |
| <span data-ttu-id="5ad18-133">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="5ad18-133">PrivateAssets</span></span> | <span data-ttu-id="5ad18-134">Tyto prostředky budou využívat, ale nebude tok nadřazený projekt</span><span class="sxs-lookup"><span data-stu-id="5ad18-134">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="5ad18-135">contentfiles; analyzátorů; sestavení</span><span class="sxs-lookup"><span data-stu-id="5ad18-135">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="5ad18-136">Povolené hodnoty pro tyto značky jsou následující, s více hodnotami, které jsou odděleny středníkem kromě s `all` a `none` která se musí nacházet ve vlastní účet:</span><span class="sxs-lookup"><span data-stu-id="5ad18-136">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="5ad18-137">Hodnota</span><span class="sxs-lookup"><span data-stu-id="5ad18-137">Value</span></span> | <span data-ttu-id="5ad18-138">Popis</span><span class="sxs-lookup"><span data-stu-id="5ad18-138">Description</span></span> |
| --- | ---
| <span data-ttu-id="5ad18-139">compile</span><span class="sxs-lookup"><span data-stu-id="5ad18-139">compile</span></span> | <span data-ttu-id="5ad18-140">Obsah `lib` složky</span><span class="sxs-lookup"><span data-stu-id="5ad18-140">Contents of the `lib` folder</span></span> |
| <span data-ttu-id="5ad18-141">modul runtime</span><span class="sxs-lookup"><span data-stu-id="5ad18-141">runtime</span></span> | <span data-ttu-id="5ad18-142">Obsah `runtimes` složky</span><span class="sxs-lookup"><span data-stu-id="5ad18-142">Contents of the `runtimes` folder</span></span> |
| <span data-ttu-id="5ad18-143">contentFiles</span><span class="sxs-lookup"><span data-stu-id="5ad18-143">contentFiles</span></span> | <span data-ttu-id="5ad18-144">Obsah `contentfiles` složky</span><span class="sxs-lookup"><span data-stu-id="5ad18-144">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="5ad18-145">sestavení</span><span class="sxs-lookup"><span data-stu-id="5ad18-145">build</span></span> | <span data-ttu-id="5ad18-146">Props a cílem v `build` složky</span><span class="sxs-lookup"><span data-stu-id="5ad18-146">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="5ad18-147">Analyzátory</span><span class="sxs-lookup"><span data-stu-id="5ad18-147">analyzers</span></span> | <span data-ttu-id="5ad18-148">Analyzátory rozhraní .NET</span><span class="sxs-lookup"><span data-stu-id="5ad18-148">.NET analyzers</span></span> |
| <span data-ttu-id="5ad18-149">nativní</span><span class="sxs-lookup"><span data-stu-id="5ad18-149">native</span></span> | <span data-ttu-id="5ad18-150">Obsah `native` složky</span><span class="sxs-lookup"><span data-stu-id="5ad18-150">Contents of the `native` folder</span></span> |
| <span data-ttu-id="5ad18-151">žádná</span><span class="sxs-lookup"><span data-stu-id="5ad18-151">none</span></span> | <span data-ttu-id="5ad18-152">Žádná z výše uvedeného se používají.</span><span class="sxs-lookup"><span data-stu-id="5ad18-152">None of the above are used.</span></span> |
| <span data-ttu-id="5ad18-153">všechny</span><span class="sxs-lookup"><span data-stu-id="5ad18-153">all</span></span> | <span data-ttu-id="5ad18-154">Všechny výše uvedené (s výjimkou `none`)</span><span class="sxs-lookup"><span data-stu-id="5ad18-154">All of the above (except `none`)</span></span> |

<span data-ttu-id="5ad18-155">V následujícím příkladu se všechno kromě soubory z balíčku obsahu by být využívány službou projektu a všechno kromě souborů obsahu a analyzátory by tok nadřazený projekt.</span><span class="sxs-lookup"><span data-stu-id="5ad18-155">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="5ad18-156">Všimněte si, že protože `build` není součástí `PrivateAssets`, cílem a props *bude* toku nadřazený projekt.</span><span class="sxs-lookup"><span data-stu-id="5ad18-156">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="5ad18-157">Například vezměte v úvahu, že odkaz na výše uvedené se používá v projektu, který NuGet balíček s názvem AppLogger sestavení.</span><span class="sxs-lookup"><span data-stu-id="5ad18-157">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="5ad18-158">AppLogger spotřebovat cílů a props z `Contoso.Utility.UsefulStuff`, jak můžete projekty, které využívají AppLogger.</span><span class="sxs-lookup"><span data-stu-id="5ad18-158">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="5ad18-159">Přidáním PackageReference podmínky</span><span class="sxs-lookup"><span data-stu-id="5ad18-159">Adding a PackageReference condition</span></span>

<span data-ttu-id="5ad18-160">Můžete vytvořit podmínku, kterou chcete řízení a zda balíček je součástí, kde podmínky můžete použít všechny nástroje MSBuild proměnná nebo Proměnná definovaná v souboru cíle nebo props.</span><span class="sxs-lookup"><span data-stu-id="5ad18-160">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="5ad18-161">Ale na v současné době pouze `TargetFramework` proměnné je podporována.</span><span class="sxs-lookup"><span data-stu-id="5ad18-161">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="5ad18-162">Řekněme například, že cílení `netstandard1.4` a také `net452` , ale mají závislost, kterou lze použít pouze u `net452`.</span><span class="sxs-lookup"><span data-stu-id="5ad18-162">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="5ad18-163">V takovém případě nechcete, aby `netstandard1.4` projekt, který využívá vašeho balíčku pro přidání tohoto nepotřebné závislosti.</span><span class="sxs-lookup"><span data-stu-id="5ad18-163">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="5ad18-164">Chcete-li tomu zabránit, zadejte podmínku na `PackageReference` následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="5ad18-164">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="5ad18-165">Balíček vytvořená s využitím tohoto projektu se zobrazí, zda jsou zahrnuty jako závislost pouze pro Newtonsoft.json `net452` cíl:</span><span class="sxs-lookup"><span data-stu-id="5ad18-165">A package built using this project will show that Newtonsoft.json is included as a dependency only for a `net452` target:</span></span>

![Výsledek použití podmínku na PackageReference s VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="5ad18-167">Podmínky lze použít také v `ItemGroup` úrovni a budou platit pro všechny podřízené objekty `PackageReference` prvky:</span><span class="sxs-lookup"><span data-stu-id="5ad18-167">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
