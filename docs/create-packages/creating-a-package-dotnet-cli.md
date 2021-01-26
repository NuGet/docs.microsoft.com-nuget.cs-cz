---
title: Vytvoření balíčku NuGet pomocí rozhraní příkazového řádku dotnet
description: Podrobný průvodce procesem navrhování a vytváření balíčku NuGet, včetně klíčových bodů rozhodování, jako jsou soubory a správa verzí.
author: JonDouglas
ms.author: jodou
ms.date: 02/20/2020
ms.topic: conceptual
ms.openlocfilehash: 4771a30ee2ff73e68154d05f1c84efd90b584162
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774480"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a><span data-ttu-id="ab44a-103">Vytvoření balíčku NuGet pomocí rozhraní příkazového řádku dotnet</span><span class="sxs-lookup"><span data-stu-id="ab44a-103">Create a NuGet package using the dotnet CLI</span></span>

<span data-ttu-id="ab44a-104">Bez ohledu na to, co váš balíček používá, nebo jaký kód obsahuje, můžete použít jeden z nástrojů rozhraní příkazového řádku ( `nuget.exe` nebo) `dotnet.exe` k zabalení této funkce do komponenty, kterou lze sdílet a používat v jakémkoli počtu jiných vývojářů.</span><span class="sxs-lookup"><span data-stu-id="ab44a-104">No matter what your package does or what code it contains, you use one of the CLI tools, either `nuget.exe` or `dotnet.exe`, to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="ab44a-105">Tento článek popisuje, jak vytvořit balíček pomocí rozhraní příkazového řádku dotnet.</span><span class="sxs-lookup"><span data-stu-id="ab44a-105">This article describes how to create a package using the dotnet CLI.</span></span> <span data-ttu-id="ab44a-106">Informace o instalaci rozhraní `dotnet` příkazového řádku najdete v tématu [Instalace nástrojů klienta NuGet](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="ab44a-106">To install the `dotnet` CLI, see [Install NuGet client tools](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="ab44a-107">Počínaje sadou Visual Studio 2017 je rozhraní příkazového řádku dotnet součástí úloh .NET Core.</span><span class="sxs-lookup"><span data-stu-id="ab44a-107">Starting in Visual Studio 2017, the dotnet CLI is included with .NET Core workloads.</span></span>

<span data-ttu-id="ab44a-108">Pro projekty .NET Core a .NET Standard, které používají [Formát styly sady SDK](../resources/check-project-format.md)a všechny další projekty ve stylu sady SDK, nástroj NuGet používá informace v souboru projektu přímo k vytvoření balíčku.</span><span class="sxs-lookup"><span data-stu-id="ab44a-108">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span> <span data-ttu-id="ab44a-109">Podrobné kurzy najdete v tématech [vytváření .NET Standard balíčků pomocí příkazu DOTNET CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) nebo [vytváření balíčků .NET Standard pomocí sady Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="ab44a-109">For step-by-step tutorials, see [Create .NET Standard Packages with dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) or [Create .NET Standard Packages with Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span></span>

<span data-ttu-id="ab44a-110">`msbuild -t:pack` je obdobou funkcí `dotnet pack` .</span><span class="sxs-lookup"><span data-stu-id="ab44a-110">`msbuild -t:pack` is functionality equivalent to `dotnet pack`.</span></span> <span data-ttu-id="ab44a-111">Pro sestavení pomocí nástroje MSBuild si přečtěte téma [Vytvoření balíčku NuGet pomocí MSBuild](creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="ab44a-111">To build with MSBuild, see [Create a NuGet package using MSBuild](creating-a-package-msbuild.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ab44a-112">Toto téma se vztahuje na projekty ve [stylu sady SDK](../resources/check-project-format.md) , obvykle v projektech .NET Core a .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="ab44a-112">This topic applies to [SDK-style](../resources/check-project-format.md) projects, typically .NET Core and .NET Standard projects.</span></span>

## <a name="set-properties"></a><span data-ttu-id="ab44a-113">Nastavení vlastností</span><span class="sxs-lookup"><span data-stu-id="ab44a-113">Set properties</span></span>

<span data-ttu-id="ab44a-114">Pro vytvoření balíčku jsou vyžadovány následující vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="ab44a-114">The following properties are required to create a package.</span></span>

- <span data-ttu-id="ab44a-115">`PackageId`, identifikátor balíčku, který musí být jedinečný v rámci Galerie, která hostuje balíček.</span><span class="sxs-lookup"><span data-stu-id="ab44a-115">`PackageId`, the package identifier, which must be unique across the gallery that hosts the package.</span></span> <span data-ttu-id="ab44a-116">Pokud není zadaný, použije se výchozí hodnota `AssemblyName` .</span><span class="sxs-lookup"><span data-stu-id="ab44a-116">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="ab44a-117">`Version`, konkrétní číslo verze ve formátu *hlavní. podverze. Oprava [-přípona]* , kde *-přípona* identifikuje [předběžné verze verzí](prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="ab44a-117">`Version`, a specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md).</span></span> <span data-ttu-id="ab44a-118">Pokud není zadaný, použije se výchozí hodnota 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="ab44a-118">If not specified, the default value is 1.0.0.</span></span>
- <span data-ttu-id="ab44a-119">Název balíčku, jak by měl být zobrazen na hostiteli (například nuget.org)</span><span class="sxs-lookup"><span data-stu-id="ab44a-119">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="ab44a-120">`Authors`, informace o autorovi a vlastníka.</span><span class="sxs-lookup"><span data-stu-id="ab44a-120">`Authors`, author and owner information.</span></span> <span data-ttu-id="ab44a-121">Pokud není zadaný, použije se výchozí hodnota `AssemblyName` .</span><span class="sxs-lookup"><span data-stu-id="ab44a-121">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="ab44a-122">`Company`, název vaší společnosti.</span><span class="sxs-lookup"><span data-stu-id="ab44a-122">`Company`, your company name.</span></span> <span data-ttu-id="ab44a-123">Pokud není zadaný, použije se výchozí hodnota `AssemblyName` .</span><span class="sxs-lookup"><span data-stu-id="ab44a-123">If not specified, the default value is `AssemblyName`.</span></span>

<span data-ttu-id="ab44a-124">V sadě Visual Studio můžete nastavit tyto hodnoty ve vlastnostech projektu (klikněte pravým tlačítkem myši na projekt v Průzkumník řešení, zvolte **vlastnosti** a vyberte kartu **balíček** ).</span><span class="sxs-lookup"><span data-stu-id="ab44a-124">In Visual Studio, you can set these values in the project properties (right-click the project in Solution Explorer, choose **Properties**, and select the **Package** tab).</span></span> <span data-ttu-id="ab44a-125">Tyto vlastnosti lze také nastavit přímo v souborech projektu ( `.csproj` ).</span><span class="sxs-lookup"><span data-stu-id="ab44a-125">You can also set these properties directly in the project files (`.csproj`).</span></span>

```xml
<PropertyGroup>
  <PackageId>AppLogger</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> <span data-ttu-id="ab44a-126">Poskytněte balíčku identifikátor, který je jedinečný v rámci nuget.org nebo jakýkoli ze zdrojů balíčku, který používáte.</span><span class="sxs-lookup"><span data-stu-id="ab44a-126">Give the package an identifier that's unique across nuget.org or whatever package source you're using.</span></span>

<span data-ttu-id="ab44a-127">Následující příklad ukazuje jednoduchý a kompletní soubor projektu s těmito vlastnostmi, které jsou k dispozici.</span><span class="sxs-lookup"><span data-stu-id="ab44a-127">The following example shows a simple, complete project file with these properties included.</span></span> <span data-ttu-id="ab44a-128">(Pomocí příkazu můžete vytvořit nový výchozí projekt `dotnet new classlib` .)</span><span class="sxs-lookup"><span data-stu-id="ab44a-128">(You can create a new default project using the `dotnet new classlib` command.)</span></span>

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

<span data-ttu-id="ab44a-129">Můžete také nastavit volitelné vlastnosti, například, `Title` `PackageDescription` a `PackageTags` , jak je popsáno v tématu [cíle sady MSBuild](../reference/msbuild-targets.md#pack-target), [řízení prostředků závislosti](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)a [vlastnosti metadat NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).</span><span class="sxs-lookup"><span data-stu-id="ab44a-129">You can also set the optional properties, such as `Title`, `PackageDescription`, and `PackageTags`, as described in [MSBuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

> [!NOTE]
> <span data-ttu-id="ab44a-130">Pro balíčky sestavené pro veřejnou spotřebu věnujte zvláštní pozornost vlastnosti **PackageTags** , protože značky můžou ostatním uživatelům najít váš balíček a pochopit, co to dělá.</span><span class="sxs-lookup"><span data-stu-id="ab44a-130">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

<span data-ttu-id="ab44a-131">Podrobnosti o deklarování závislostí a zadání čísel verzí naleznete v tématu [odkazy na balíčky v souborech projektu](../consume-packages/package-references-in-project-files.md) a [Správa verzí balíčků](../concepts/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="ab44a-131">For details on declaring dependencies and specifying version numbers, see [Package references in project files](../consume-packages/package-references-in-project-files.md) and [Package versioning](../concepts/package-versioning.md).</span></span> <span data-ttu-id="ab44a-132">Je také možné Surface prostředků ze závislostí přímo v balíčku pomocí `<IncludeAssets>` `<ExcludeAssets>` atributů a.</span><span class="sxs-lookup"><span data-stu-id="ab44a-132">It is also possible to surface assets from dependencies directly in the package by using the `<IncludeAssets>` and `<ExcludeAssets>` attributes.</span></span> <span data-ttu-id="ab44a-133">Další informace najdete v tématu [řízení prostředků závislosti](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="ab44a-133">For more information, see [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

## <a name="add-an-optional-description-field"></a><span data-ttu-id="ab44a-134">Přidat volitelné pole popisu</span><span class="sxs-lookup"><span data-stu-id="ab44a-134">Add an optional description field</span></span>

[!INCLUDE [add description to package](includes/add-description.md)]

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a><span data-ttu-id="ab44a-135">Vyberte jedinečný identifikátor balíčku a nastavte číslo verze.</span><span class="sxs-lookup"><span data-stu-id="ab44a-135">Choose a unique package identifier and set the version number</span></span>

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="run-the-pack-command"></a><span data-ttu-id="ab44a-136">Spuštění příkazu Pack</span><span class="sxs-lookup"><span data-stu-id="ab44a-136">Run the pack command</span></span>

<span data-ttu-id="ab44a-137">Chcete-li vytvořit balíček NuGet ( `.nupkg` soubor) z projektu, spusťte `dotnet pack` příkaz, který také automaticky vytvoří projekt:</span><span class="sxs-lookup"><span data-stu-id="ab44a-137">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```dotnetcli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="ab44a-138">Výstup zobrazuje cestu k `.nupkg` souboru.</span><span class="sxs-lookup"><span data-stu-id="ab44a-138">The output shows the path to the `.nupkg` file.</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="ab44a-139">Automaticky generovat balíček při sestavení</span><span class="sxs-lookup"><span data-stu-id="ab44a-139">Automatically generate package on build</span></span>

<span data-ttu-id="ab44a-140">Chcete-li automaticky spustit `dotnet pack` při spuštění `dotnet build` , přidejte následující řádek do souboru projektu v rámci `<PropertyGroup>` :</span><span class="sxs-lookup"><span data-stu-id="ab44a-140">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

<span data-ttu-id="ab44a-141">Při spuštění `dotnet pack` v řešení jsou všechny projekty v řešení, které lze zabalit ( [<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) vlastnost nastavena na hodnotu `true` ).</span><span class="sxs-lookup"><span data-stu-id="ab44a-141">When you run `dotnet pack` on a solution, this packs all the projects in the solution that are packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) property is set to `true`).</span></span>

> [!NOTE]
> <span data-ttu-id="ab44a-142">Když balíček automaticky vygenerujete, čas k zabalení zvýší čas sestavení pro váš projekt.</span><span class="sxs-lookup"><span data-stu-id="ab44a-142">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="test-package-installation"></a><span data-ttu-id="ab44a-143">Instalace testovacího balíčku</span><span class="sxs-lookup"><span data-stu-id="ab44a-143">Test package installation</span></span>

<span data-ttu-id="ab44a-144">Před publikováním balíčku obvykle budete chtít otestovat proces instalace balíčku do projektu.</span><span class="sxs-lookup"><span data-stu-id="ab44a-144">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="ab44a-145">Testy zajistěte, aby všechny potřebné soubory byly všechny na správném místě v projektu.</span><span class="sxs-lookup"><span data-stu-id="ab44a-145">The tests make sure that the necessary files all end up in their correct places in the project.</span></span>

<span data-ttu-id="ab44a-146">Instalaci můžete v aplikaci Visual Studio nebo na příkazovém řádku otestovat ručně pomocí [kroků normální instalace balíčku](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span><span class="sxs-lookup"><span data-stu-id="ab44a-146">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ab44a-147">Balíčky jsou neměnné.</span><span class="sxs-lookup"><span data-stu-id="ab44a-147">Packages are immutable.</span></span> <span data-ttu-id="ab44a-148">Pokud problém opravíte, znovu ho změňte a znovu spusťte. při opětovném testování bude stále použita stará verze balíčku, dokud [nevymažete složku globálních balíčků](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) .</span><span class="sxs-lookup"><span data-stu-id="ab44a-148">If you correct a problem, change the contents of the package and pack again, when you retest you will still be using the old version of the package until you [clear your global packages](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) folder.</span></span> <span data-ttu-id="ab44a-149">To je obzvláště důležité při testování balíčků, které nepoužívají jedinečný popisek předprodejní verze pro každé sestavení.</span><span class="sxs-lookup"><span data-stu-id="ab44a-149">This is especially relevant when testing packages that don't use a unique prerelease label on every build.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab44a-150">Další kroky</span><span class="sxs-lookup"><span data-stu-id="ab44a-150">Next Steps</span></span>

<span data-ttu-id="ab44a-151">Po vytvoření balíčku, který je `.nupkg` soubor, můžete ho publikovat do Galerie podle svého výběru, jak je popsáno v tématu [publikování balíčku](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="ab44a-151">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="ab44a-152">Můžete také chtít zvětšit možnosti vašeho balíčku nebo jinak podporovat jiné scénáře, jak je popsáno v následujících tématech:</span><span class="sxs-lookup"><span data-stu-id="ab44a-152">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="ab44a-153">Správa verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="ab44a-153">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="ab44a-154">Podpora více cílových architektur</span><span class="sxs-lookup"><span data-stu-id="ab44a-154">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="ab44a-155">Přidat ikonu balíčku</span><span class="sxs-lookup"><span data-stu-id="ab44a-155">Add a package icon</span></span>](../reference/nuspec.md#icon)
- [<span data-ttu-id="ab44a-156">Transformace zdrojových a konfiguračních souborů</span><span class="sxs-lookup"><span data-stu-id="ab44a-156">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="ab44a-157">Lokalizace</span><span class="sxs-lookup"><span data-stu-id="ab44a-157">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="ab44a-158">Předběžné verze verzí</span><span class="sxs-lookup"><span data-stu-id="ab44a-158">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="ab44a-159">Nastavení typu balíčku</span><span class="sxs-lookup"><span data-stu-id="ab44a-159">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="ab44a-160">Vytváření balíčků pomocí sestavení zprostředkovatele komunikace s objekty COM</span><span class="sxs-lookup"><span data-stu-id="ab44a-160">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="ab44a-161">Nakonec existují další typy balíčků, o kterých byste měli vědět:</span><span class="sxs-lookup"><span data-stu-id="ab44a-161">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="ab44a-162">Nativní balíčky</span><span class="sxs-lookup"><span data-stu-id="ab44a-162">Native Packages</span></span>](../guides/native-packages.md)
- [<span data-ttu-id="ab44a-163">Balíčky symbolů</span><span class="sxs-lookup"><span data-stu-id="ab44a-163">Symbol Packages</span></span>](../create-packages/symbol-packages-snupkg.md)
