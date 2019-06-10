---
title: Formát NuGet PackageReference (odkazy na balíček v souborech projektu)
description: Podrobnosti na NuGet PackageReference v souborech projektu podporuje NuGet 4.0 + a VS2017 a .NET Core 2.0
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: c2dfce8de6b28aaee99e3d5ab75cd28950a8cb0f
ms.sourcegitcommit: b8c63744252a5a37a2843f6bc1d5917496ee40dd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812835"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="98ab9-103">Odkazy na balíček (PackageReference) v souborech projektu</span><span class="sxs-lookup"><span data-stu-id="98ab9-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="98ab9-104">Balíček odkazů pomocí nástroje `PackageReference` uzlu, správě závislostí NuGet přímo v rámci projektových souborů (na rozdíl od samostatné `packages.config` souboru).</span><span class="sxs-lookup"><span data-stu-id="98ab9-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="98ab9-105">Pomocí PackageReference, jako je volána, nemá vliv na ostatní aspekty NuGet; například nastavení v `NuGet.config` soubory (včetně zdroje balíčků) se uplatní, jak je vysvětleno v [konfigurace chování Nugetu](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="98ab9-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="98ab9-106">S PackageReference můžete také použít podmínky nástroje MSBuild zvolit odkazy na balíček na cílovou architekturu, konfigurace, platformy nebo další seskupení.</span><span class="sxs-lookup"><span data-stu-id="98ab9-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="98ab9-107">Umožňuje také pro detailní kontrolu nad závislostí a obsahu toku.</span><span class="sxs-lookup"><span data-stu-id="98ab9-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="98ab9-108">(Další podrobnosti najdete v [NuGet aktualizací Service pack a obnovení jako cílů MSBuild](../reference/msbuild-targets.md).)</span><span class="sxs-lookup"><span data-stu-id="98ab9-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

## <a name="project-type-support"></a><span data-ttu-id="98ab9-109">Podpora typu projektu</span><span class="sxs-lookup"><span data-stu-id="98ab9-109">Project type support</span></span>

<span data-ttu-id="98ab9-110">Ve výchozím nastavení je použít PackageReference pro projekty .NET Core, .NET Standard projekty a projekty UPW cílení na Windows 10 sestavení 15063 (Creators Update) a novější, s výjimkou projekty C++ UWP.</span><span class="sxs-lookup"><span data-stu-id="98ab9-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="98ab9-111">Projekty rozhraní .NET framework podporují PackageReference, ale nyní jako výchozí `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="98ab9-111">.NET Framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="98ab9-112">Použití PackageReference, [migrovat](../reference/migrate-packages-config-to-package-reference.md) závislosti z `packages.config` do souboru projektu, odstraňte soubor packages.config.</span><span class="sxs-lookup"><span data-stu-id="98ab9-112">To use PackageReference, [migrate](../reference/migrate-packages-config-to-package-reference.md) the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

<span data-ttu-id="98ab9-113">Aplikace ASP.NET cílí na úplné rozhraní .NET Framework obsahují pouze [omezenou podporu](https://github.com/NuGet/Home/issues/5877) pro PackageReference.</span><span class="sxs-lookup"><span data-stu-id="98ab9-113">ASP.NET apps targeting the full .NET Framework include only [limited support](https://github.com/NuGet/Home/issues/5877) for PackageReference.</span></span> <span data-ttu-id="98ab9-114">C++a typy projektů jazyka JavaScript se nepodporují.</span><span class="sxs-lookup"><span data-stu-id="98ab9-114">C++ and JavaScript project types are unsupported.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="98ab9-115">Přidávání PackageReference</span><span class="sxs-lookup"><span data-stu-id="98ab9-115">Adding a PackageReference</span></span>

<span data-ttu-id="98ab9-116">Přidáte závislost v souboru projektu pomocí následující syntaxe:</span><span class="sxs-lookup"><span data-stu-id="98ab9-116">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="98ab9-117">Řízení verze závislosti</span><span class="sxs-lookup"><span data-stu-id="98ab9-117">Controlling dependency version</span></span>

<span data-ttu-id="98ab9-118">Konvence pro určení verze balíčku je stejný jako při použití `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="98ab9-118">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="98ab9-119">V předchozím příkladu 3.6.0 znamená, že všechny verze, která je > = 3.6.0 s předností nejnižší verze, jak je popsáno na [Správa verzí balíčků](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="98ab9-119">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="98ab9-120">Pomocí projektu s PackageReferences žádné PackageReference</span><span class="sxs-lookup"><span data-stu-id="98ab9-120">Using PackageReference for a project with no PackageReferences</span></span>
<span data-ttu-id="98ab9-121">Pokročilé: Pokud jste žádné balíčky nainstalované v projektu (žádné PackageReferences v souboru projektu) a žádný soubor packages.config, ale chcete projekt tak, aby se obnovit jako PackageReference styl, můžete nastavit vlastnost projektu RestoreProjectStyle na PackageReference v projektu soubor.</span><span class="sxs-lookup"><span data-stu-id="98ab9-121">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
<span data-ttu-id="98ab9-122">To může být užitečné, pokud se budete odkazovat na projekty, které jsou PackageReference ve stylu (existující csproj nebo projekty založenými na sadu SDK).</span><span class="sxs-lookup"><span data-stu-id="98ab9-122">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="98ab9-123">Tato možnost povolí balíčky, které odkazují tyto projekty, do "přechodně" odkazuje váš projekt.</span><span class="sxs-lookup"><span data-stu-id="98ab9-123">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="floating-versions"></a><span data-ttu-id="98ab9-124">Plovoucí verze</span><span class="sxs-lookup"><span data-stu-id="98ab9-124">Floating Versions</span></span>

<span data-ttu-id="98ab9-125">[Plovoucí verze](../consume-packages/dependency-resolution.md#floating-versions) podporují `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="98ab9-125">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="98ab9-126">Řízení závislosti prostředků</span><span class="sxs-lookup"><span data-stu-id="98ab9-126">Controlling dependency assets</span></span>

<span data-ttu-id="98ab9-127">Může používat závislost čistě jako vývojové prostředí a nemusí chcete je zveřejnit, která do projektů, které budou využívat vašeho balíčku.</span><span class="sxs-lookup"><span data-stu-id="98ab9-127">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="98ab9-128">V tomto scénáři můžete použít `PrivateAssets` metadat a řídit tak toto chování.</span><span class="sxs-lookup"><span data-stu-id="98ab9-128">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="98ab9-129">Následující značky metadat určovat závislost prostředky:</span><span class="sxs-lookup"><span data-stu-id="98ab9-129">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="98ab9-130">Značka</span><span class="sxs-lookup"><span data-stu-id="98ab9-130">Tag</span></span> | <span data-ttu-id="98ab9-131">Popis</span><span class="sxs-lookup"><span data-stu-id="98ab9-131">Description</span></span> | <span data-ttu-id="98ab9-132">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="98ab9-132">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98ab9-133">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="98ab9-133">IncludeAssets</span></span> | <span data-ttu-id="98ab9-134">Tyto prostředky budou využívat.</span><span class="sxs-lookup"><span data-stu-id="98ab9-134">These assets will be consumed</span></span> | <span data-ttu-id="98ab9-135">všechny</span><span class="sxs-lookup"><span data-stu-id="98ab9-135">all</span></span> |
| <span data-ttu-id="98ab9-136">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="98ab9-136">ExcludeAssets</span></span> | <span data-ttu-id="98ab9-137">Tyto prostředky nebude využívat.</span><span class="sxs-lookup"><span data-stu-id="98ab9-137">These assets will not be consumed</span></span> | <span data-ttu-id="98ab9-138">žádná</span><span class="sxs-lookup"><span data-stu-id="98ab9-138">none</span></span> |
| <span data-ttu-id="98ab9-139">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="98ab9-139">PrivateAssets</span></span> | <span data-ttu-id="98ab9-140">Tyto prostředky budou využívat, ale nebude směrovat do nadřazeného projektu</span><span class="sxs-lookup"><span data-stu-id="98ab9-140">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="98ab9-141">contentfiles; analyzátory; sestavení</span><span class="sxs-lookup"><span data-stu-id="98ab9-141">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="98ab9-142">Povolené hodnoty pro tyto značky jsou následujícím způsobem s více hodnotami, které jsou odděleny středníkem s výjimkou s `all` a `none` který musí být uvedena samy o sobě:</span><span class="sxs-lookup"><span data-stu-id="98ab9-142">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="98ab9-143">Value</span><span class="sxs-lookup"><span data-stu-id="98ab9-143">Value</span></span> | <span data-ttu-id="98ab9-144">Popis</span><span class="sxs-lookup"><span data-stu-id="98ab9-144">Description</span></span> |
| --- | ---
| <span data-ttu-id="98ab9-145">Kompilace</span><span class="sxs-lookup"><span data-stu-id="98ab9-145">compile</span></span> | <span data-ttu-id="98ab9-146">Obsah `lib` složky a ovládací prvky, jestli můžete zkompilovat váš projekt proti sestavení ve složce</span><span class="sxs-lookup"><span data-stu-id="98ab9-146">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="98ab9-147">modul runtime</span><span class="sxs-lookup"><span data-stu-id="98ab9-147">runtime</span></span> | <span data-ttu-id="98ab9-148">Obsah `lib` a `runtimes` složky a ovládací prvky, jestli tato sestavení bude zkopírována do sestavení výstupního adresáře</span><span class="sxs-lookup"><span data-stu-id="98ab9-148">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="98ab9-149">contentFiles</span><span class="sxs-lookup"><span data-stu-id="98ab9-149">contentFiles</span></span> | <span data-ttu-id="98ab9-150">Obsah `contentfiles` složky</span><span class="sxs-lookup"><span data-stu-id="98ab9-150">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="98ab9-151">sestavení</span><span class="sxs-lookup"><span data-stu-id="98ab9-151">build</span></span> | <span data-ttu-id="98ab9-152">Vlastnosti a cíle ve `build` složky</span><span class="sxs-lookup"><span data-stu-id="98ab9-152">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="98ab9-153">Analyzátory</span><span class="sxs-lookup"><span data-stu-id="98ab9-153">analyzers</span></span> | <span data-ttu-id="98ab9-154">Analyzátory .NET</span><span class="sxs-lookup"><span data-stu-id="98ab9-154">.NET analyzers</span></span> |
| <span data-ttu-id="98ab9-155">nativní</span><span class="sxs-lookup"><span data-stu-id="98ab9-155">native</span></span> | <span data-ttu-id="98ab9-156">Obsah `native` složky</span><span class="sxs-lookup"><span data-stu-id="98ab9-156">Contents of the `native` folder</span></span> |
| <span data-ttu-id="98ab9-157">žádná</span><span class="sxs-lookup"><span data-stu-id="98ab9-157">none</span></span> | <span data-ttu-id="98ab9-158">Žádná z výše uvedených se používají.</span><span class="sxs-lookup"><span data-stu-id="98ab9-158">None of the above are used.</span></span> |
| <span data-ttu-id="98ab9-159">všechny</span><span class="sxs-lookup"><span data-stu-id="98ab9-159">all</span></span> | <span data-ttu-id="98ab9-160">Všechny výš uvedené (s výjimkou `none`)</span><span class="sxs-lookup"><span data-stu-id="98ab9-160">All of the above (except `none`)</span></span> |

<span data-ttu-id="98ab9-161">V následujícím příkladu se všechno kromě soubory obsahu z balíčku by být využívány službou projektu a všechno, co s výjimkou souborů obsahu a analyzátory by tok na nadřazený projekt.</span><span class="sxs-lookup"><span data-stu-id="98ab9-161">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="98ab9-162">Upozorňujeme, že `build` není součástí `PrivateAssets`, zaměřuje a props *bude* tok, který nadřazeného projektu.</span><span class="sxs-lookup"><span data-stu-id="98ab9-162">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="98ab9-163">Zvažte například, že výše uvedené odkaz se používá v projektu, který vytvoří balíček NuGet s názvem AppLogger.</span><span class="sxs-lookup"><span data-stu-id="98ab9-163">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="98ab9-164">AppLogger může spotřebovat cíle a vlastnosti z `Contoso.Utility.UsefulStuff`, jak můžete projektech, které využívají AppLogger.</span><span class="sxs-lookup"><span data-stu-id="98ab9-164">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="98ab9-165">Přidání podmínky PackageReference</span><span class="sxs-lookup"><span data-stu-id="98ab9-165">Adding a PackageReference condition</span></span>

<span data-ttu-id="98ab9-166">Můžete použít podmínku pro ovládací prvek, jestli balíček je zahrnuta, pokud podmínky můžete použít jakoukoli proměnnou MSBuild nebo Proměnná definovaná v souboru cílů nebo vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="98ab9-166">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="98ab9-167">Ale v současnosti pouze `TargetFramework` proměnná je podporována.</span><span class="sxs-lookup"><span data-stu-id="98ab9-167">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="98ab9-168">Předpokládejme například, že vývoji cílíte `netstandard1.4` stejně jako `net452` , ale mají závislost, kterou lze použít pouze pro `net452`.</span><span class="sxs-lookup"><span data-stu-id="98ab9-168">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="98ab9-169">V tomto případě nechcete `netstandard1.4` projekt, který se spotřebovává balíček pro přidání tohoto zbytečné závislosti.</span><span class="sxs-lookup"><span data-stu-id="98ab9-169">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="98ab9-170">Chcete-li tomu zabránit, určíte podmínku na `PackageReference` následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="98ab9-170">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="98ab9-171">Balíček vytvořené pomocí tohoto projektu se zobrazí, že je jako závislost pouze pro Newtonsoft.Json `net452` cíl:</span><span class="sxs-lookup"><span data-stu-id="98ab9-171">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![Výsledek použití podmínku na PackageReference s VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="98ab9-173">Podmínek je také možné použít na `ItemGroup` úrovně a má platit pro všechny podřízené objekty `PackageReference` prvky:</span><span class="sxs-lookup"><span data-stu-id="98ab9-173">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="locking-dependencies"></a><span data-ttu-id="98ab9-174">Uzamčení závislosti</span><span class="sxs-lookup"><span data-stu-id="98ab9-174">Locking dependencies</span></span>
<span data-ttu-id="98ab9-175">*Tato funkce je k dispozici s NuGet **4.9** nebo vyšší a sadou Visual Studio 2017 **15.9** nebo vyšší.*</span><span class="sxs-lookup"><span data-stu-id="98ab9-175">*This feature is available with NuGet **4.9** or above and with Visual Studio 2017 **15.9** or above.*</span></span>

<span data-ttu-id="98ab9-176">Vstup pro obnovení NuGet je sada odkazy na balíčky ze souboru projektu (závislosti nejvyšší úrovně a direct) a výstup je úplné uzavření všechny závislosti balíčků, včetně přechodné závislosti.</span><span class="sxs-lookup"><span data-stu-id="98ab9-176">Input to NuGet restore is a set of Package References from the project file (top-level or direct dependencies) and the output is a full closure of all the package dependencies including transitive dependencies.</span></span> <span data-ttu-id="98ab9-177">NuGet se pokusí vždy vytvořila stejný úplný uzavření závislosti balíčků, pokud nedošlo ke změně vstupní seznam PackageReference.</span><span class="sxs-lookup"><span data-stu-id="98ab9-177">NuGet tries to always produce the same full closure of package dependencies if the input PackageReference list has not changed.</span></span> <span data-ttu-id="98ab9-178">Existují však některé scénáře, kdy je to možné.</span><span class="sxs-lookup"><span data-stu-id="98ab9-178">However, there are some scenarios where it is unable to do so.</span></span> <span data-ttu-id="98ab9-179">Příklad:</span><span class="sxs-lookup"><span data-stu-id="98ab9-179">For example:</span></span>

* <span data-ttu-id="98ab9-180">Při použití s plovoucí desetinnou čárkou, jako je verze `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span><span class="sxs-lookup"><span data-stu-id="98ab9-180">When you use floating versions like `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span></span> <span data-ttu-id="98ab9-181">I když jsou záměr zde uvolnění na nejnovější verzi na každý obnovení balíčků, jsou scénáře, kdy uživatelé vyžadují graf tak, aby být pevně nastavené na určitého nejnovější verzi a plovoucí desetinnou čárkou na novější verzi, pokud je k dispozici na explicitní gest.</span><span class="sxs-lookup"><span data-stu-id="98ab9-181">While the intention here is to float to the latest version on every restore of packages, there are scenarios where users require the graph to be locked to a certain latest version and float to a later version, if available, upon an explicit gesture.</span></span>
* <span data-ttu-id="98ab9-182">Je publikovaný novější verzi balíčku požadavky na odpovídající verzi PackageReference.</span><span class="sxs-lookup"><span data-stu-id="98ab9-182">A newer version of the package matching PackageReference version requirements is published.</span></span> <span data-ttu-id="98ab9-183">Například</span><span class="sxs-lookup"><span data-stu-id="98ab9-183">E.g.</span></span> 

  * <span data-ttu-id="98ab9-184">Dne 1: Pokud jste zadali `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` ale byly k dispozici verze na úložiště NuGet 4.1.0, 4.2.0 a 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="98ab9-184">Day 1: if you specified `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` but the versions available on the NuGet repositories were 4.1.0, 4.2.0 and 4.3.0.</span></span> <span data-ttu-id="98ab9-185">V takovém případě by byly vyřešeny NuGet do 4.1.0 (nejbližší minimální verze)</span><span class="sxs-lookup"><span data-stu-id="98ab9-185">In this case, NuGet would have resolved to  4.1.0 (nearest minimum version)</span></span>

  * <span data-ttu-id="98ab9-186">Dne 2: Získá publikované verze 4.0.0.</span><span class="sxs-lookup"><span data-stu-id="98ab9-186">Day 2: Version 4.0.0 gets published.</span></span> <span data-ttu-id="98ab9-187">NuGet teď najít přesnou shodu a začít překládat 4.0.0</span><span class="sxs-lookup"><span data-stu-id="98ab9-187">NuGet will now find the exact match and start resolving to 4.0.0</span></span>

* <span data-ttu-id="98ab9-188">Verze daného balíčku bude odebrána z úložiště.</span><span class="sxs-lookup"><span data-stu-id="98ab9-188">A given package version is removed from the repository.</span></span> <span data-ttu-id="98ab9-189">Když nuget.org neumožňuje balíček odstranění, ne všechna úložiště balíčků nastavit toto omezení.</span><span class="sxs-lookup"><span data-stu-id="98ab9-189">Though nuget.org does not allow package deletions, not all package repositories have this constraints.</span></span> <span data-ttu-id="98ab9-190">Výsledkem je najít nejlepší shodu při nelze přeložit na odstraněné verze NuGet.</span><span class="sxs-lookup"><span data-stu-id="98ab9-190">This results in NuGet finding the best match when it cannot resolve to the deleted version.</span></span>

### <a name="enabling-lock-file"></a><span data-ttu-id="98ab9-191">Povolení soubor zámku</span><span class="sxs-lookup"><span data-stu-id="98ab9-191">Enabling lock file</span></span>
<span data-ttu-id="98ab9-192">Aby bylo možné zachovat Úplné uzavření závislosti balíčků můžete můžete vyjádřit výslovný souhlas s funkcí soubor zámku nastavením vlastnosti MSBuild `RestorePackagesWithLockFile` pro váš projekt:</span><span class="sxs-lookup"><span data-stu-id="98ab9-192">In order to persist the full closure of package dependencies you can opt-in to the lock file feature by setting the MSBuild property `RestorePackagesWithLockFile` for your project:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="98ab9-193">Pokud je tato vlastnost nastavena, obnovení NuGet vygeneruje soubor zámku - `packages.lock.json` souboru v kořenovém adresáři projektu, který obsahuje seznam všech balíčků závislostí.</span><span class="sxs-lookup"><span data-stu-id="98ab9-193">If this property is set, NuGet restore will generate a lock file - `packages.lock.json` file at the project root directory that lists all the package dependencies.</span></span> 

> [!Note]
> <span data-ttu-id="98ab9-194">Jakmile je projekt `packages.lock.json` soubor v kořenovém adresáři soubor zámku je vždy využít i v případě obnovení vlastnost `RestorePackagesWithLockFile` není nastaven.</span><span class="sxs-lookup"><span data-stu-id="98ab9-194">Once a project has `packages.lock.json` file in its root directory, the lock file is always used with restore even if the property `RestorePackagesWithLockFile` is not set.</span></span> <span data-ttu-id="98ab9-195">Dalším způsobem, jak vyjádřit výslovný souhlas s touto funkcí je vytvořte fiktivního prázdný `packages.lock.json` souboru v kořenovém adresáři projektu.</span><span class="sxs-lookup"><span data-stu-id="98ab9-195">So another way to opt-in to this feature is to create a dummy blank `packages.lock.json` file in the project's root directory.</span></span>

### <a name="restore-behavior-with-lock-file"></a><span data-ttu-id="98ab9-196">`restore` chování s soubor zámku</span><span class="sxs-lookup"><span data-stu-id="98ab9-196">`restore` behavior with lock file</span></span>
<span data-ttu-id="98ab9-197">Pokud se nachází soubor zámku pro projekt, NuGet používá ke spuštění tohoto uzamknout souboru `restore`.</span><span class="sxs-lookup"><span data-stu-id="98ab9-197">If a lock file is present for project, NuGet uses this lock file to run `restore`.</span></span> <span data-ttu-id="98ab9-198">NuGet nemá Rychlá kontrola, zda byly změny v závislosti balíčků, jak je uvedeno v souboru projektu (nebo soubory závislých projektů) a pokud nejsou žádné změny jenom obnoví balíčky uvedené v souboru zámku.</span><span class="sxs-lookup"><span data-stu-id="98ab9-198">NuGet does a quick check to see if there were any changes in the package dependencies as mentioned in the project file (or dependent projects' files) and if there were no changes it just restores the packages mentioned in the lock file.</span></span> <span data-ttu-id="98ab9-199">Neexistuje žádné opakované vyhodnocení závislosti balíčků.</span><span class="sxs-lookup"><span data-stu-id="98ab9-199">There is no re-evaluation of package dependencies.</span></span>

<span data-ttu-id="98ab9-200">NuGet zjistí změnu v definované závislostí, jak je uvedeno v souborech projektů, znovu vyhodnotí grafu balíčku a aktualizuje soubor zámku tak, aby odrážely nový balíček uzavření pro projekt.</span><span class="sxs-lookup"><span data-stu-id="98ab9-200">If NuGet detects a change in the defined dependencies as mentioned in the project file(s), it re-evaluates the package graph and updates the lock file to reflect the new package closure for the project.</span></span>

<span data-ttu-id="98ab9-201">Pro CI/CD a další scénáře, ve kterém by chcete změnit závislosti balíčků v reálném čase, můžete to provést nastavením `lockedmode` k `true`:</span><span class="sxs-lookup"><span data-stu-id="98ab9-201">For CI/CD and other scenarios, where you would not want to change the package dependencies on the fly, you can do so by setting the `lockedmode` to `true`:</span></span>

<span data-ttu-id="98ab9-202">Pro dotnet.exe spusťte:</span><span class="sxs-lookup"><span data-stu-id="98ab9-202">For dotnet.exe, run:</span></span>
```
> dotnet.exe restore --locked-mode
```

<span data-ttu-id="98ab9-203">Msbuild.exe spusťte tento příkaz:</span><span class="sxs-lookup"><span data-stu-id="98ab9-203">For msbuild.exe, run:</span></span>
```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

<span data-ttu-id="98ab9-204">Může také nastavit podmíněné vlastnost MSBuild v souboru projektu:</span><span class="sxs-lookup"><span data-stu-id="98ab9-204">You may also set this conditional MSBuild property in your project file:</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

<span data-ttu-id="98ab9-205">Pokud uzamčeném režimu `true`, obnovení bude obnovení přesné balíčků, jak je uvedeno v souboru zámku nebo selhat, pokud jste aktualizovali závislosti definované balíčků pro projekt, po vytvoření souboru zámku.</span><span class="sxs-lookup"><span data-stu-id="98ab9-205">If locked mode is `true`, restore will either restore the exact packages as listed in the lock file or fail if you updated the defined package dependencies for the project after lock file was created.</span></span>

### <a name="make-lock-file-part-of-your-source-repository"></a><span data-ttu-id="98ab9-206">Zařazení zamknout soubor zdrojového úložiště</span><span class="sxs-lookup"><span data-stu-id="98ab9-206">Make lock file part of your source repository</span></span>
<span data-ttu-id="98ab9-207">Pokud vytváříte aplikaci, spustitelný soubor a dotyčný projektu je na začátku řetězu závislostí zkontrolujte v souboru zámku na úložiště zdrojového kódu tak, aby NuGet můžete využít během obnovení.</span><span class="sxs-lookup"><span data-stu-id="98ab9-207">If you are building an application, an executable and the project in question is at the start of the dependency chain then do check in the lock file to the source code repository so that NuGet can make use of it during restore.</span></span>

<span data-ttu-id="98ab9-208">Ale pokud váš projekt je projekt knihovny, který jste Nedodávejte nebo běžné projekt kódu na další projekty se závisí na vás **by neměla** jako součást vašeho zdrojového kódu se změnami soubor zámku.</span><span class="sxs-lookup"><span data-stu-id="98ab9-208">However, if your project is a library project that you do not ship or a common code project on which other projects depend upon, you **should not** check in the lock file as part of your source code.</span></span> <span data-ttu-id="98ab9-209">Neexistuje nezpůsobily žádné potíže ochraně souboru zámku ale závislosti uzamčené balíčků pro běžné projekt kódu nesmí být použit, jak je uvedeno v souboru zámku během obnovení/sestavení projektu, který závisí na tomto společný kód projektu.</span><span class="sxs-lookup"><span data-stu-id="98ab9-209">There is no harm in keeping the lock file but the locked package dependencies for the common code project may not be used, as listed in the lock file, during the restore/build of a project that depends on this common-code project.</span></span>

<span data-ttu-id="98ab9-210">Např.</span><span class="sxs-lookup"><span data-stu-id="98ab9-210">Eg.</span></span>
```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```
<span data-ttu-id="98ab9-211">Pokud `ProjectA` závislý na `PackageX` verze `2.0.0` a také odkazuje na `ProjectB` , který závisí na `PackageX` verze `1.0.0`, pak soubor zámku pro `ProjectB` zobrazí seznam závislost na `PackageX` verze `1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="98ab9-211">If `ProjectA` has a dependency on a `PackageX` version `2.0.0` and also references `ProjectB` that depends on `PackageX` version `1.0.0`, then the lock file for `ProjectB` will list a dependency on `PackageX` version `1.0.0`.</span></span> <span data-ttu-id="98ab9-212">Ale když `ProjectA` vytvořili, platnost zámku soubor bude obsahovat závislost na `PackageX` verze **`2.0.0`** a **není** `1.0.0` jak je uvedeno v souboru zámku pro `ProjectB`.</span><span class="sxs-lookup"><span data-stu-id="98ab9-212">However, when `ProjectA` is built, its lock file will contain a dependency on `PackageX` version **`2.0.0`** and **not** `1.0.0` as listed in the lock file for `ProjectB`.</span></span> <span data-ttu-id="98ab9-213">Proto soubor zámku běžné kódového projektu má málo say přeložit pro projekty, které jsou na ní závislé balíčky.</span><span class="sxs-lookup"><span data-stu-id="98ab9-213">Thus, the lock file of a common code project has little say over the packages resolved for projects that depend on it.</span></span>

### <a name="lock-file-extensibility"></a><span data-ttu-id="98ab9-214">Rozšíření souboru zámku</span><span class="sxs-lookup"><span data-stu-id="98ab9-214">Lock file extensibility</span></span>
<span data-ttu-id="98ab9-215">Jak je popsáno níže, můžete se soubor zámku ovládání různého chování obnovení:</span><span class="sxs-lookup"><span data-stu-id="98ab9-215">You can control various behaviors of restore with lock file as described below:</span></span>

| <span data-ttu-id="98ab9-216">Možnost</span><span class="sxs-lookup"><span data-stu-id="98ab9-216">Option</span></span> | <span data-ttu-id="98ab9-217">Ekvivalentní možnosti MSBuild</span><span class="sxs-lookup"><span data-stu-id="98ab9-217">MSBuild equivalent option</span></span> | 
|:---  |:--- |
| `--use-lock-file` | <span data-ttu-id="98ab9-218">Bootstraps použít soubor zámku pro projekt.</span><span class="sxs-lookup"><span data-stu-id="98ab9-218">Bootstraps use of lock file for a project.</span></span> <span data-ttu-id="98ab9-219">Můžete také nastavit `RestorePackagesWithLockFile` vlastnost v souboru projektu</span><span class="sxs-lookup"><span data-stu-id="98ab9-219">You can alternatively set `RestorePackagesWithLockFile` property in the project file</span></span> | 
| `--locked-mode` | <span data-ttu-id="98ab9-220">Umožňuje uzamčeném režimu pro obnovení.</span><span class="sxs-lookup"><span data-stu-id="98ab9-220">Enables locked mode for restore.</span></span> <span data-ttu-id="98ab9-221">To je užitečné ve scénářích CI/CD, kde byste chtěli získání opakovatelných sestavení.</span><span class="sxs-lookup"><span data-stu-id="98ab9-221">This is useful in CI/CD scenarios where you would like to get the repeatable builds.</span></span> <span data-ttu-id="98ab9-222">To může být také tak, že nastavíte `RestoreLockedMode` vlastnosti nástroje MSBuild `true`</span><span class="sxs-lookup"><span data-stu-id="98ab9-222">This can be also by setting the `RestoreLockedMode` MSBuild property to `true`</span></span> |  
| `--force-evaluate` | <span data-ttu-id="98ab9-223">Tato možnost je užitečná s balíčky verzí s plovoucí desetinnou čárkou definované v projektu.</span><span class="sxs-lookup"><span data-stu-id="98ab9-223">This option is useful with packages with floating version defined in the project.</span></span> <span data-ttu-id="98ab9-224">Ve výchozím nastavení, obnovení NuGet se neaktualizuje automaticky při každé obnovení verze balíčku není-li spustit obnovení s `--force-evaluate` možnost.</span><span class="sxs-lookup"><span data-stu-id="98ab9-224">By default, NuGet restore will not update the package version automatically upon each restore unless you run restore with `--force-evaluate` option.</span></span> |
| `--lock-file-path` | <span data-ttu-id="98ab9-225">Definuje vlastní zámek umístění souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="98ab9-225">Defines a custom lock file location for a project.</span></span> <span data-ttu-id="98ab9-226">To můžete také dosáhnout nastavením vlastnosti MSBuild `NuGetLockFilePath`.</span><span class="sxs-lookup"><span data-stu-id="98ab9-226">This can be also achieved by setting the MSBuild property `NuGetLockFilePath`.</span></span> <span data-ttu-id="98ab9-227">Ve výchozím nastavení podporuje NuGet `packages.lock.json` v kořenovém adresáři.</span><span class="sxs-lookup"><span data-stu-id="98ab9-227">By default, NuGet supports `packages.lock.json` at the root directory.</span></span> <span data-ttu-id="98ab9-228">Pokud máte více projektů ve stejném adresáři, NuGet podporuje konkrétní zámek souboru projektu `packages.<project_name>.lock.json`</span><span class="sxs-lookup"><span data-stu-id="98ab9-228">If you have multiple projects in the same directory, NuGet supports project specific lock file `packages.<project_name>.lock.json`</span></span> |
