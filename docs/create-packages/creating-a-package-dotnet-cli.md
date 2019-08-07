---
title: Vytvoření balíčku NuGet pomocí rozhraní příkazového řádku dotnet
description: Podrobný průvodce procesem navrhování a vytváření balíčku NuGet, včetně klíčových bodů rozhodování, jako jsou soubory a správa verzí.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 8222e1edfa13951d2fda9a2384d93bba38ef4979
ms.sourcegitcommit: ba8ad1bd13a4bba3df94374e34e20c425a05af2f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2019
ms.locfileid: "68833298"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a><span data-ttu-id="20cd7-103">Vytvoření balíčku NuGet pomocí rozhraní příkazového řádku dotnet</span><span class="sxs-lookup"><span data-stu-id="20cd7-103">Create a NuGet package using the dotnet CLI</span></span>

<span data-ttu-id="20cd7-104">Bez ohledu na to, co váš balíček používá, nebo jaký kód obsahuje, můžete použít jeden z nástrojů rozhraní `nuget.exe` příkazového řádku (nebo `dotnet.exe`) k zabalení této funkce do komponenty, kterou lze sdílet a používat v jakémkoli počtu jiných vývojářů.</span><span class="sxs-lookup"><span data-stu-id="20cd7-104">No matter what your package does or what code it contains, you use one of the CLI tools, either `nuget.exe` or `dotnet.exe`, to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="20cd7-105">Tento článek popisuje, jak vytvořit balíček pomocí rozhraní příkazového řádku dotnet.</span><span class="sxs-lookup"><span data-stu-id="20cd7-105">This article describes how to create a package using the dotnet CLI.</span></span> <span data-ttu-id="20cd7-106">Informace o instalaci `dotnet` rozhraní příkazového řádku najdete v tématu [Instalace nástrojů klienta NuGet](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="20cd7-106">To install the `dotnet` CLI, see [Install NuGet client tools](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="20cd7-107">Počínaje sadou Visual Studio 2017 je rozhraní příkazového řádku dotnet součástí úloh .NET Core.</span><span class="sxs-lookup"><span data-stu-id="20cd7-107">Starting in Visual Studio 2017, the dotnet CLI is included with .NET Core workloads.</span></span>

<span data-ttu-id="20cd7-108">Pro projekty .NET Core a .NET Standard, které používají [Formát styly sady SDK](../resources/check-project-format.md)a všechny další projekty ve stylu sady SDK, nástroj NuGet používá informace v souboru projektu přímo k vytvoření balíčku.</span><span class="sxs-lookup"><span data-stu-id="20cd7-108">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span> <span data-ttu-id="20cd7-109">Podrobné kurzy najdete v tématech [vytváření .NET Standard balíčků pomocí příkazu DOTNET CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) nebo [vytváření balíčků .NET Standard pomocí sady Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="20cd7-109">For step-by-step tutorials, see [Create .NET Standard Packages with dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) or [Create .NET Standard Packages with Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span></span>

<span data-ttu-id="20cd7-110">`msbuild -t:pack`je obdobou `dotnet pack`funkcí.</span><span class="sxs-lookup"><span data-stu-id="20cd7-110">`msbuild -t:pack` is functionality equivalent to `dotnet pack`.</span></span> <span data-ttu-id="20cd7-111">Pro sestavení pomocí nástroje MSBuild si přečtěte téma [Vytvoření balíčku NuGet pomocí MSBuild](creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="20cd7-111">To build with MSBuild, see [Create a NuGet package using MSBuild](creating-a-package-msbuild.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="20cd7-112">Toto téma se vztahuje na projekty ve [stylu sady SDK](../resources/check-project-format.md) , obvykle v projektech .NET Core a .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="20cd7-112">This topic applies to [SDK-style](../resources/check-project-format.md) projects, typically .NET Core and .NET Standard projects.</span></span>

## <a name="set-properties"></a><span data-ttu-id="20cd7-113">Nastavit vlastnosti</span><span class="sxs-lookup"><span data-stu-id="20cd7-113">Set properties</span></span>

<span data-ttu-id="20cd7-114">Pro vytvoření balíčku jsou vyžadovány následující vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="20cd7-114">The following properties are required to create a package.</span></span>

- <span data-ttu-id="20cd7-115">`PackageId`, identifikátor balíčku, který musí být jedinečný v rámci Galerie, která hostuje balíček.</span><span class="sxs-lookup"><span data-stu-id="20cd7-115">`PackageId`, the package identifier, which must be unique across the gallery that hosts the package.</span></span> <span data-ttu-id="20cd7-116">Pokud není zadaný, použije se výchozí hodnota `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="20cd7-116">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="20cd7-117">`Version`, konkrétní číslo verze ve formátu *hlavní. podverze. Oprava [-přípona]* , kde *-přípona* identifikuje [předběžné verze verzí](prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="20cd7-117">`Version`, a specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md).</span></span> <span data-ttu-id="20cd7-118">Pokud není zadaný, použije se výchozí hodnota 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="20cd7-118">If not specified, the default value is 1.0.0.</span></span>
- <span data-ttu-id="20cd7-119">Název balíčku, jak by měl být zobrazen na hostiteli (například nuget.org)</span><span class="sxs-lookup"><span data-stu-id="20cd7-119">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="20cd7-120">`Authors`, informace o autorovi a vlastníka.</span><span class="sxs-lookup"><span data-stu-id="20cd7-120">`Authors`, author and owner information.</span></span> <span data-ttu-id="20cd7-121">Pokud není zadaný, použije se výchozí hodnota `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="20cd7-121">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="20cd7-122">`Company`, název vaší společnosti.</span><span class="sxs-lookup"><span data-stu-id="20cd7-122">`Company`, your company name.</span></span> <span data-ttu-id="20cd7-123">Pokud není zadaný, použije se výchozí hodnota `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="20cd7-123">If not specified, the default value is `AssemblyName`.</span></span>

<span data-ttu-id="20cd7-124">V sadě Visual Studio můžete nastavit tyto hodnoty ve vlastnostech projektu (klikněte pravým tlačítkem myši na projekt v Průzkumník řešení, zvolte **vlastnosti**a vyberte kartu **balíček** ).</span><span class="sxs-lookup"><span data-stu-id="20cd7-124">In Visual Studio, you can set these values in the project properties (right-click the project in Solution Explorer, choose **Properties**, and select the **Package** tab).</span></span> <span data-ttu-id="20cd7-125">Tyto vlastnosti lze také nastavit přímo v souborech projektu (`.csproj`).</span><span class="sxs-lookup"><span data-stu-id="20cd7-125">You can also set these properties directly in the project files (`.csproj`).</span></span>

```xml
<PropertyGroup>
  <PackageId>AppLogger</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> <span data-ttu-id="20cd7-126">Poskytněte balíčku identifikátor, který je jedinečný v rámci nuget.org nebo jakýkoli ze zdrojů balíčku, který používáte.</span><span class="sxs-lookup"><span data-stu-id="20cd7-126">Give the package an identifier that's unique across nuget.org or whatever package source you're using.</span></span>

<span data-ttu-id="20cd7-127">Následující příklad ukazuje jednoduchý a kompletní soubor projektu s těmito vlastnostmi, které jsou k dispozici.</span><span class="sxs-lookup"><span data-stu-id="20cd7-127">The following example shows a simple, complete project file with these properties included.</span></span> <span data-ttu-id="20cd7-128">(Pomocí `dotnet new classlib` příkazu můžete vytvořit nový výchozí projekt.)</span><span class="sxs-lookup"><span data-stu-id="20cd7-128">(You can create a new default project using the `dotnet new classlib` command.)</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
  </PropertyGroup>
</Project>
```

<span data-ttu-id="20cd7-129">Můžete také nastavit volitelné vlastnosti, například `Title` `PackageDescription`, `PackageTags`a, jak je popsáno v tématu [cíle sady MSBuild](../reference/msbuild-targets.md#pack-target), [řízení prostředků závislosti](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)a [vlastnosti metadat NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).</span><span class="sxs-lookup"><span data-stu-id="20cd7-129">You can also set the optional properties, such as `Title`, `PackageDescription`, and `PackageTags`, as described in [MSBuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

> [!NOTE]
> <span data-ttu-id="20cd7-130">Pro balíčky sestavené pro veřejnou spotřebu věnujte zvláštní pozornost vlastnosti **PackageTags** , protože značky můžou ostatním uživatelům najít váš balíček a pochopit, co to dělá.</span><span class="sxs-lookup"><span data-stu-id="20cd7-130">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

<span data-ttu-id="20cd7-131">Podrobnosti o deklarování závislostí a zadání čísel verzí naleznete v tématu [odkazy na balíčky v souborech projektu](../consume-packages/package-references-in-project-files.md) a [Správa verzí balíčků](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="20cd7-131">For details on declaring dependencies and specifying version numbers, see [Package references in project files](../consume-packages/package-references-in-project-files.md) and [Package versioning](../reference/package-versioning.md).</span></span> <span data-ttu-id="20cd7-132">Je také možné Surface prostředků ze závislostí přímo v balíčku pomocí `<IncludeAssets>` atributů a. `<ExcludeAssets>`</span><span class="sxs-lookup"><span data-stu-id="20cd7-132">It is also possible to surface assets from dependencies directly in the package by using the `<IncludeAssets>` and `<ExcludeAssets>` attributes.</span></span> <span data-ttu-id="20cd7-133">Další informace najdete v Seee [řízení prostředků závislostí](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="20cd7-133">For more information, seee [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a><span data-ttu-id="20cd7-134">Vyberte jedinečný identifikátor balíčku a nastavte číslo verze.</span><span class="sxs-lookup"><span data-stu-id="20cd7-134">Choose a unique package identifier and set the version number</span></span>

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="run-the-pack-command"></a><span data-ttu-id="20cd7-135">Spuštění příkazu Pack</span><span class="sxs-lookup"><span data-stu-id="20cd7-135">Run the pack command</span></span>

<span data-ttu-id="20cd7-136">Chcete-li vytvořit balíček NuGet ( `.nupkg` soubor) z projektu, `dotnet pack` spusťte příkaz, který také automaticky vytvoří projekt:</span><span class="sxs-lookup"><span data-stu-id="20cd7-136">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```cli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="20cd7-137">Výstup zobrazuje cestu k `.nupkg` souboru.</span><span class="sxs-lookup"><span data-stu-id="20cd7-137">The output shows the path to the `.nupkg` file.</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="20cd7-138">Automaticky generovat balíček při sestavení</span><span class="sxs-lookup"><span data-stu-id="20cd7-138">Automatically generate package on build</span></span>

<span data-ttu-id="20cd7-139">Chcete-li `dotnet pack` automaticky spustit při `dotnet build`spuštění, přidejte následující řádek do souboru projektu v rámci `<PropertyGroup>`:</span><span class="sxs-lookup"><span data-stu-id="20cd7-139">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

<span data-ttu-id="20cd7-140">Při spuštění `dotnet pack` v řešení jsou všechny projekty v řešení, které lze zabalit ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) vlastnost nastavena na `true`hodnotu).</span><span class="sxs-lookup"><span data-stu-id="20cd7-140">When you run `dotnet pack` on a solution, this packs all the projects in the solution that are packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) property is set to `true`).</span></span>

> [!NOTE]
> <span data-ttu-id="20cd7-141">Když balíček automaticky vygenerujete, čas k zabalení zvýší čas sestavení pro váš projekt.</span><span class="sxs-lookup"><span data-stu-id="20cd7-141">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="test-package-installation"></a><span data-ttu-id="20cd7-142">Instalace testovacího balíčku</span><span class="sxs-lookup"><span data-stu-id="20cd7-142">Test package installation</span></span>

<span data-ttu-id="20cd7-143">Před publikováním balíčku obvykle budete chtít otestovat proces instalace balíčku do projektu.</span><span class="sxs-lookup"><span data-stu-id="20cd7-143">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="20cd7-144">Testy zajistí, že všechny soubory v projektu budou mít všechny na správném místě.</span><span class="sxs-lookup"><span data-stu-id="20cd7-144">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="20cd7-145">Instalaci můžete v aplikaci Visual Studio nebo na příkazovém řádku otestovat ručně pomocí [kroků normální instalace balíčku](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span><span class="sxs-lookup"><span data-stu-id="20cd7-145">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="20cd7-146">Balíčky jsou neměnné.</span><span class="sxs-lookup"><span data-stu-id="20cd7-146">Packages are immutable.</span></span> <span data-ttu-id="20cd7-147">Pokud problém opravíte, znovu ho změňte a znovu spusťte. při opětovném testování bude stále použita stará verze balíčku, dokud nevymažete složku [globálních balíčků](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) .</span><span class="sxs-lookup"><span data-stu-id="20cd7-147">If you correct a problem, change the contents of the package and pack again, when you retest you will still be using the old version of the package until you [clear your global packages](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) folder.</span></span> <span data-ttu-id="20cd7-148">To je obzvláště důležité při testování balíčků, které nepoužívají jedinečný popisek předprodejní verze pro každé sestavení.</span><span class="sxs-lookup"><span data-stu-id="20cd7-148">This is especially relevant when testing packages that don't use a unique prerelease label on every build.</span></span>

## <a name="next-steps"></a><span data-ttu-id="20cd7-149">Další kroky</span><span class="sxs-lookup"><span data-stu-id="20cd7-149">Next Steps</span></span>

<span data-ttu-id="20cd7-150">Po vytvoření balíčku, který je `.nupkg` soubor, můžete ho publikovat do Galerie podle svého výběru, jak je popsáno v tématu [publikování balíčku](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="20cd7-150">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="20cd7-151">Můžete také chtít zvětšit možnosti vašeho balíčku nebo jinak podporovat jiné scénáře, jak je popsáno v následujících tématech:</span><span class="sxs-lookup"><span data-stu-id="20cd7-151">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="20cd7-152">Správa verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="20cd7-152">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="20cd7-153">Podpora více cílových architektur</span><span class="sxs-lookup"><span data-stu-id="20cd7-153">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="20cd7-154">Transformace zdrojových a konfiguračních souborů</span><span class="sxs-lookup"><span data-stu-id="20cd7-154">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="20cd7-155">Lokalizace</span><span class="sxs-lookup"><span data-stu-id="20cd7-155">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="20cd7-156">Předběžné verze verzí</span><span class="sxs-lookup"><span data-stu-id="20cd7-156">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="20cd7-157">Nastavení typu balíčku</span><span class="sxs-lookup"><span data-stu-id="20cd7-157">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="20cd7-158">Vytváření balíčků pomocí sestavení zprostředkovatele komunikace s objekty COM</span><span class="sxs-lookup"><span data-stu-id="20cd7-158">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="20cd7-159">Nakonec existují další typy balíčků, o kterých byste měli vědět:</span><span class="sxs-lookup"><span data-stu-id="20cd7-159">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="20cd7-160">Nativní balíčky</span><span class="sxs-lookup"><span data-stu-id="20cd7-160">Native Packages</span></span>](../create-packages/native-packages.md)
- [<span data-ttu-id="20cd7-161">Balíčky symbolů</span><span class="sxs-lookup"><span data-stu-id="20cd7-161">Symbol Packages</span></span>](../create-packages/symbol-packages.md)
