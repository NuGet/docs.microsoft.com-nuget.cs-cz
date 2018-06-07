---
title: Formát NuGet PackageReference (odkazů balíčku v souborech projektu)
description: Podrobnosti o NuGet PackageReference v souborech projektu podporuje NuGet 4.0 + a VS2017 a .NET Core 2.0
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 61f447877459764906cf9a2b88b32a8bc0553689
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817668"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="70e38-103">Balíček odkazuje (PackageReference) v souborech projektu</span><span class="sxs-lookup"><span data-stu-id="70e38-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="70e38-104">Balíček odkazů, pomocí `PackageReference` uzlu, Správa závislostí NuGet přímo v souborech projektu (oproti samostatné `packages.config` souboru).</span><span class="sxs-lookup"><span data-stu-id="70e38-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="70e38-105">Použití PackageReference, jako je volána, nemá vliv dalších aspektů NuGet; například nastavení v `NuGet.Config` soubory (včetně zdroje balíčků) jsou stále použít, jak je popsáno v [konfigurace chování NuGet](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="70e38-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="70e38-106">S PackageReference můžete taky podmínky nástroje MSBuild vybrat balíček odkazuje na cílové rozhraní, konfigurace, platformu nebo jiných seskupení.</span><span class="sxs-lookup"><span data-stu-id="70e38-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="70e38-107">Umožňuje také pro jemně odstupňovanou kontrolu nad závislosti a obsahu toku.</span><span class="sxs-lookup"><span data-stu-id="70e38-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="70e38-108">(Další podrobnosti najdete v [NuGet pack a obnovit jako cíle MSBuild](../reference/msbuild-targets.md).)</span><span class="sxs-lookup"><span data-stu-id="70e38-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

<span data-ttu-id="70e38-109">Ve výchozím nastavení PackageReference se používá pro projekty .NET Core, .NET Standard projekty a UWP projektech zacílených na Windows 10 sestavení 15063 (Creators aktualizace) a novější, s výjimkou projektů C++ UWP.</span><span class="sxs-lookup"><span data-stu-id="70e38-109">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="70e38-110">Projekty rozhraní .NET framework úplnou podporu PackageReference, ale aktuálně výchozí `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="70e38-110">.NET full framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="70e38-111">Chcete-li použít PackageReference, migrujte závislostí z `packages.config` v souboru projektu odeberte souboru Packages.config je.</span><span class="sxs-lookup"><span data-stu-id="70e38-111">To use PackageReference, migrate the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="70e38-112">Přidání PackageReference</span><span class="sxs-lookup"><span data-stu-id="70e38-112">Adding a PackageReference</span></span>

<span data-ttu-id="70e38-113">Přidáte závislost v souboru projektu pomocí následující syntaxe:</span><span class="sxs-lookup"><span data-stu-id="70e38-113">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="70e38-114">Řízení verze závislosti</span><span class="sxs-lookup"><span data-stu-id="70e38-114">Controlling dependency version</span></span>

<span data-ttu-id="70e38-115">Konvence pro určení verze balíčku je stejný jako při použití `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="70e38-115">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="70e38-116">V předchozím příkladu 3.6.0 znamená všechny verze, která je > = 3.6.0 s předvolby pro nejnižší verze, jak je popsáno na [Správa verzí balíčku](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="70e38-116">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="70e38-117">Pomocí PackageReference pro projekt se žádné PackageReferences</span><span class="sxs-lookup"><span data-stu-id="70e38-117">Using PackageReference for a project with no PackageReferences</span></span>
<span data-ttu-id="70e38-118">Pokročilé: Pokud jste žádné balíčky nainstalované v projektu (žádné PackageReferences v souboru projektu) a žádný soubor packages.config, ale chcete projekt, který má být obnovena jako PackageReference styl, můžete nastavit vlastnost projektu RestoreProjectStyle k PackageReference v soubor projektu.</span><span class="sxs-lookup"><span data-stu-id="70e38-118">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
<span data-ttu-id="70e38-119">To může být užitečné, pokud odkazujete projekty, které jsou PackageReference ve (stávající csproj nebo projekty stylu SDK).</span><span class="sxs-lookup"><span data-stu-id="70e38-119">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="70e38-120">Tato akce povolí balíčky, které tyto projekty najdete, "přechodně" odkazovat projektu.</span><span class="sxs-lookup"><span data-stu-id="70e38-120">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="floating-versions"></a><span data-ttu-id="70e38-121">Plovoucí verze</span><span class="sxs-lookup"><span data-stu-id="70e38-121">Floating Versions</span></span>

<span data-ttu-id="70e38-122">[Plovoucí verze](../consume-packages/dependency-resolution.md#floating-versions) podporují `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="70e38-122">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="70e38-123">Řízení závislostí prostředky</span><span class="sxs-lookup"><span data-stu-id="70e38-123">Controlling dependency assets</span></span>

<span data-ttu-id="70e38-124">Může používat závislost čistě jako harness vývoj a nemusí chtějí zpřístupnit, projekty, které bude využívat vašeho balíčku.</span><span class="sxs-lookup"><span data-stu-id="70e38-124">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="70e38-125">V tomto scénáři můžete použít `PrivateAssets` metadata, aby bylo toto chování.</span><span class="sxs-lookup"><span data-stu-id="70e38-125">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="70e38-126">Následující značky metadata řídit prostředky závislost:</span><span class="sxs-lookup"><span data-stu-id="70e38-126">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="70e38-127">Značka</span><span class="sxs-lookup"><span data-stu-id="70e38-127">Tag</span></span> | <span data-ttu-id="70e38-128">Popis</span><span class="sxs-lookup"><span data-stu-id="70e38-128">Description</span></span> | <span data-ttu-id="70e38-129">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="70e38-129">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="70e38-130">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="70e38-130">IncludeAssets</span></span> | <span data-ttu-id="70e38-131">Tyto prostředky budou využívat.</span><span class="sxs-lookup"><span data-stu-id="70e38-131">These assets will be consumed</span></span> | <span data-ttu-id="70e38-132">všechny</span><span class="sxs-lookup"><span data-stu-id="70e38-132">all</span></span> |
| <span data-ttu-id="70e38-133">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="70e38-133">ExcludeAssets</span></span> | <span data-ttu-id="70e38-134">Tyto prostředky nebudou využívat.</span><span class="sxs-lookup"><span data-stu-id="70e38-134">These assets will not be consumed</span></span> | <span data-ttu-id="70e38-135">žádná</span><span class="sxs-lookup"><span data-stu-id="70e38-135">none</span></span> |
| <span data-ttu-id="70e38-136">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="70e38-136">PrivateAssets</span></span> | <span data-ttu-id="70e38-137">Tyto prostředky budou využívat, ale nebude tok nadřazený projekt</span><span class="sxs-lookup"><span data-stu-id="70e38-137">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="70e38-138">contentfiles; analyzátorů; sestavení</span><span class="sxs-lookup"><span data-stu-id="70e38-138">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="70e38-139">Povolené hodnoty pro tyto značky jsou následující, s více hodnotami, které jsou odděleny středníkem kromě s `all` a `none` která se musí nacházet ve vlastní účet:</span><span class="sxs-lookup"><span data-stu-id="70e38-139">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="70e38-140">Hodnota</span><span class="sxs-lookup"><span data-stu-id="70e38-140">Value</span></span> | <span data-ttu-id="70e38-141">Popis</span><span class="sxs-lookup"><span data-stu-id="70e38-141">Description</span></span> |
| --- | ---
| <span data-ttu-id="70e38-142">Kompilace</span><span class="sxs-lookup"><span data-stu-id="70e38-142">compile</span></span> | <span data-ttu-id="70e38-143">Obsah `lib` složku a ovládací prvky jestli můžete zkompilovat projektu proti sestavení ve složce</span><span class="sxs-lookup"><span data-stu-id="70e38-143">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="70e38-144">modul runtime</span><span class="sxs-lookup"><span data-stu-id="70e38-144">runtime</span></span> | <span data-ttu-id="70e38-145">Obsah `lib` a `runtimes` složku a ovládací prvky jestli tyto sestavení bude zkopírována do sestavení výstupní adresář</span><span class="sxs-lookup"><span data-stu-id="70e38-145">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="70e38-146">contentFiles</span><span class="sxs-lookup"><span data-stu-id="70e38-146">contentFiles</span></span> | <span data-ttu-id="70e38-147">Obsah `contentfiles` složky</span><span class="sxs-lookup"><span data-stu-id="70e38-147">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="70e38-148">sestavení</span><span class="sxs-lookup"><span data-stu-id="70e38-148">build</span></span> | <span data-ttu-id="70e38-149">Props a cílem v `build` složky</span><span class="sxs-lookup"><span data-stu-id="70e38-149">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="70e38-150">Analyzátory</span><span class="sxs-lookup"><span data-stu-id="70e38-150">analyzers</span></span> | <span data-ttu-id="70e38-151">Analyzátory rozhraní .NET</span><span class="sxs-lookup"><span data-stu-id="70e38-151">.NET analyzers</span></span> |
| <span data-ttu-id="70e38-152">nativní</span><span class="sxs-lookup"><span data-stu-id="70e38-152">native</span></span> | <span data-ttu-id="70e38-153">Obsah `native` složky</span><span class="sxs-lookup"><span data-stu-id="70e38-153">Contents of the `native` folder</span></span> |
| <span data-ttu-id="70e38-154">žádná</span><span class="sxs-lookup"><span data-stu-id="70e38-154">none</span></span> | <span data-ttu-id="70e38-155">Žádná z výše uvedeného se používají.</span><span class="sxs-lookup"><span data-stu-id="70e38-155">None of the above are used.</span></span> |
| <span data-ttu-id="70e38-156">všechny</span><span class="sxs-lookup"><span data-stu-id="70e38-156">all</span></span> | <span data-ttu-id="70e38-157">Všechny výše uvedené (s výjimkou `none`)</span><span class="sxs-lookup"><span data-stu-id="70e38-157">All of the above (except `none`)</span></span> |

<span data-ttu-id="70e38-158">V následujícím příkladu se všechno kromě soubory z balíčku obsahu by být využívány službou projektu a všechno kromě souborů obsahu a analyzátory by tok nadřazený projekt.</span><span class="sxs-lookup"><span data-stu-id="70e38-158">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="70e38-159">Všimněte si, že protože `build` není součástí `PrivateAssets`, cílem a props *bude* toku nadřazený projekt.</span><span class="sxs-lookup"><span data-stu-id="70e38-159">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="70e38-160">Například vezměte v úvahu, že odkaz na výše uvedené se používá v projektu, který NuGet balíček s názvem AppLogger sestavení.</span><span class="sxs-lookup"><span data-stu-id="70e38-160">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="70e38-161">AppLogger spotřebovat cílů a props z `Contoso.Utility.UsefulStuff`, jak můžete projekty, které využívají AppLogger.</span><span class="sxs-lookup"><span data-stu-id="70e38-161">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="70e38-162">Přidáním PackageReference podmínky</span><span class="sxs-lookup"><span data-stu-id="70e38-162">Adding a PackageReference condition</span></span>

<span data-ttu-id="70e38-163">Můžete vytvořit podmínku, kterou chcete řízení a zda balíček je součástí, kde podmínky můžete použít všechny nástroje MSBuild proměnná nebo Proměnná definovaná v souboru cíle nebo props.</span><span class="sxs-lookup"><span data-stu-id="70e38-163">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="70e38-164">Ale na v současné době pouze `TargetFramework` proměnné je podporována.</span><span class="sxs-lookup"><span data-stu-id="70e38-164">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="70e38-165">Řekněme například, že cílení `netstandard1.4` a také `net452` , ale mají závislost, kterou lze použít pouze u `net452`.</span><span class="sxs-lookup"><span data-stu-id="70e38-165">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="70e38-166">V takovém případě nechcete, aby `netstandard1.4` projekt, který využívá vašeho balíčku pro přidání tohoto nepotřebné závislosti.</span><span class="sxs-lookup"><span data-stu-id="70e38-166">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="70e38-167">Chcete-li tomu zabránit, zadejte podmínku na `PackageReference` následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="70e38-167">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="70e38-168">Balíček vytvořená s využitím tohoto projektu se zobrazí, zda jsou zahrnuty jako závislost pouze pro Newtonsoft.json `net452` cíl:</span><span class="sxs-lookup"><span data-stu-id="70e38-168">A package built using this project will show that Newtonsoft.json is included as a dependency only for a `net452` target:</span></span>

![Výsledek použití podmínku na PackageReference s VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="70e38-170">Podmínky lze použít také v `ItemGroup` úrovni a budou platit pro všechny podřízené objekty `PackageReference` prvky:</span><span class="sxs-lookup"><span data-stu-id="70e38-170">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
