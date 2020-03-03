---
title: Vytvoření balíčku NuGet pomocí nástroje MSBuild
description: Podrobný průvodce procesem navrhování a vytváření balíčku NuGet, včetně klíčových bodů rozhodování, jako jsou soubory a správa verzí.
author: karann-msft
ms.author: karann
ms.date: 02/20/2020
ms.topic: conceptual
ms.openlocfilehash: 7166d622ef9d3975fc1c931d30caf570a765a6da
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231315"
---
# <a name="create-a-nuget-package-using-msbuild"></a><span data-ttu-id="968ae-103">Vytvoření balíčku NuGet pomocí nástroje MSBuild</span><span class="sxs-lookup"><span data-stu-id="968ae-103">Create a NuGet package using MSBuild</span></span>

<span data-ttu-id="968ae-104">Když vytvoříte balíček NuGet z kódu, zabalíte tuto funkci do komponenty, kterou můžete sdílet s a používat v jakémkoli počtu jiných vývojářů.</span><span class="sxs-lookup"><span data-stu-id="968ae-104">When you create a NuGet package from your code, you package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="968ae-105">Tento článek popisuje, jak vytvořit balíček pomocí nástroje MSBuild.</span><span class="sxs-lookup"><span data-stu-id="968ae-105">This article describes how to create a package using MSBuild.</span></span> <span data-ttu-id="968ae-106">Nástroj MSBuild přináší předinstalované všechny úlohy sady Visual Studio, které obsahují NuGet.</span><span class="sxs-lookup"><span data-stu-id="968ae-106">MSBuild comes preinstalled with every Visual Studio workload that contains NuGet.</span></span> <span data-ttu-id="968ae-107">Kromě toho můžete také použít MSBuild prostřednictvím rozhraní příkazového řádku dotnet s nástrojem [dotnet MSBuild](https://docs.microsoft.com/dotnet/core/tools/dotnet-msbuild).</span><span class="sxs-lookup"><span data-stu-id="968ae-107">Additionally you can also use MSBuild through the dotnet CLI with [dotnet msbuild](https://docs.microsoft.com/dotnet/core/tools/dotnet-msbuild).</span></span>

<span data-ttu-id="968ae-108">Pro projekty .NET Core a .NET Standard, které používají [Formát styly sady SDK](../resources/check-project-format.md)a všechny další projekty ve stylu sady SDK, nástroj NuGet používá informace v souboru projektu přímo k vytvoření balíčku.</span><span class="sxs-lookup"><span data-stu-id="968ae-108">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span>  <span data-ttu-id="968ae-109">Pro projekt bez sady SDK, který používá `<PackageReference>`, NuGet také používá soubor projektu k vytvoření balíčku.</span><span class="sxs-lookup"><span data-stu-id="968ae-109">For a non-SDK-style project that uses `<PackageReference>`, NuGet also uses the project file to create a package.</span></span>

<span data-ttu-id="968ae-110">Projekty ve stylu sady SDK mají ve výchozím nastavení dostupné funkce balíčku.</span><span class="sxs-lookup"><span data-stu-id="968ae-110">SDK-style projects have the pack functionality available by default.</span></span> <span data-ttu-id="968ae-111">Pro projekty PackageReference bez sady SDK je nutné přidat balíček NuGet. Build. Tasks. Pack do závislostí projektu.</span><span class="sxs-lookup"><span data-stu-id="968ae-111">For non SDK-style PackageReference projects, you need to add the NuGet.Build.Tasks.Pack package to the project dependencies.</span></span> <span data-ttu-id="968ae-112">Podrobné informace o cílech sady MSBuild Pack naleznete v tématu [sada NuGet Pack a obnovení jako cíle MSBuild](../reference/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="968ae-112">For detailed information about MSBuild pack targets, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).</span></span>

<span data-ttu-id="968ae-113">Příkaz, který vytváří balíček, `msbuild -t:pack`, je funkce ekvivalentní `dotnet pack`.</span><span class="sxs-lookup"><span data-stu-id="968ae-113">The command that creates a package, `msbuild -t:pack`, is functionality equivalent to `dotnet pack`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="968ae-114">Toto téma se vztahuje na projekty ve [stylu sady SDK](../resources/check-project-format.md) , obvykle v projektech .NET Core a .NET Standard a na projekty ve stylu jiné než SDK, které používají PackageReference.</span><span class="sxs-lookup"><span data-stu-id="968ae-114">This topic applies to [SDK-style](../resources/check-project-format.md) projects, typically .NET Core and .NET Standard projects, and to non-SDK-style projects that use PackageReference.</span></span>

## <a name="set-properties"></a><span data-ttu-id="968ae-115">Nastavení vlastností</span><span class="sxs-lookup"><span data-stu-id="968ae-115">Set properties</span></span>

<span data-ttu-id="968ae-116">Pro vytvoření balíčku jsou vyžadovány následující vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="968ae-116">The following properties are required to create a package.</span></span>

- <span data-ttu-id="968ae-117">`PackageId`, identifikátor balíčku, který musí být jedinečný v rámci Galerie, která hostuje balíček.</span><span class="sxs-lookup"><span data-stu-id="968ae-117">`PackageId`, the package identifier, which must be unique across the gallery that hosts the package.</span></span> <span data-ttu-id="968ae-118">Pokud není zadaný, použije se výchozí hodnota `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="968ae-118">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="968ae-119">`Version`– konkrétní číslo verze ve formátu *hlavní. podverze. Oprava [-přípona]* , kde *-přípona* identifikuje [předběžné verze verzí](prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="968ae-119">`Version`, a specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md).</span></span> <span data-ttu-id="968ae-120">Pokud není zadaný, použije se výchozí hodnota 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="968ae-120">If not specified, the default value is 1.0.0.</span></span>
- <span data-ttu-id="968ae-121">Název balíčku, jak by měl být zobrazen na hostiteli (například nuget.org)</span><span class="sxs-lookup"><span data-stu-id="968ae-121">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="968ae-122">`Authors`, informace o autorovi a vlastníkovi.</span><span class="sxs-lookup"><span data-stu-id="968ae-122">`Authors`, author and owner information.</span></span> <span data-ttu-id="968ae-123">Pokud není zadaný, použije se výchozí hodnota `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="968ae-123">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="968ae-124">`Company`název vaší společnosti.</span><span class="sxs-lookup"><span data-stu-id="968ae-124">`Company`, your company name.</span></span> <span data-ttu-id="968ae-125">Pokud není zadaný, použije se výchozí hodnota `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="968ae-125">If not specified, the default value is `AssemblyName`.</span></span>

<span data-ttu-id="968ae-126">Kromě toho, pokud jste balíte projekty, které nejsou ve stylu sady SDK, které používají PackageReference, je třeba zadat následující:</span><span class="sxs-lookup"><span data-stu-id="968ae-126">Additionally if you are packing non-SDK-style projects that use PackageReference, the following is required:</span></span>

- <span data-ttu-id="968ae-127">`PackageOutputPath`, výstupní složka balíčku vygenerovaného při volání Pack.</span><span class="sxs-lookup"><span data-stu-id="968ae-127">`PackageOutputPath`, the output folder for the package generated when calling pack.</span></span>

<span data-ttu-id="968ae-128">V sadě Visual Studio můžete nastavit tyto hodnoty ve vlastnostech projektu (klikněte pravým tlačítkem myši na projekt v Průzkumník řešení, zvolte **vlastnosti**a vyberte kartu **balíček** ).</span><span class="sxs-lookup"><span data-stu-id="968ae-128">In Visual Studio, you can set these values in the project properties (right-click the project in Solution Explorer, choose **Properties**, and select the **Package** tab).</span></span> <span data-ttu-id="968ae-129">Tyto vlastnosti lze také nastavit přímo v souborech projektu (*. csproj*).</span><span class="sxs-lookup"><span data-stu-id="968ae-129">You can also set these properties directly in the project files (*.csproj*).</span></span>

```xml
<PropertyGroup>
  <PackageId>ClassLibDotNetStandard</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> <span data-ttu-id="968ae-130">Poskytněte balíčku identifikátor, který je jedinečný v rámci nuget.org nebo jakýkoli ze zdrojů balíčku, který používáte.</span><span class="sxs-lookup"><span data-stu-id="968ae-130">Give the package an identifier that's unique across nuget.org or whatever package source you're using.</span></span>

<span data-ttu-id="968ae-131">Následující příklad ukazuje jednoduchý a kompletní soubor projektu s těmito vlastnostmi, které jsou k dispozici.</span><span class="sxs-lookup"><span data-stu-id="968ae-131">The following example shows a simple, complete project file with these properties included.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>ClassLibDotNetStandard</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
  </PropertyGroup>
</Project>
```

<span data-ttu-id="968ae-132">Můžete také nastavit volitelné vlastnosti, například `Title`, `PackageDescription`a `PackageTags`, jak je popsáno v tématu [cíle sady MSBuild](../reference/msbuild-targets.md#pack-target), [řízení prostředků závislosti](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)a [vlastnosti metadat NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).</span><span class="sxs-lookup"><span data-stu-id="968ae-132">You can also set the optional properties, such as `Title`, `PackageDescription`, and `PackageTags`, as described in [MSBuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

> [!NOTE]
> <span data-ttu-id="968ae-133">Pro balíčky sestavené pro veřejnou spotřebu věnujte zvláštní pozornost vlastnosti **PackageTags** , protože značky můžou ostatním uživatelům najít váš balíček a pochopit, co to dělá.</span><span class="sxs-lookup"><span data-stu-id="968ae-133">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

<span data-ttu-id="968ae-134">Podrobnosti o deklarování závislostí a zadání čísel verzí naleznete v tématu [odkazy na balíčky v souborech projektu](../consume-packages/package-references-in-project-files.md) a [Správa verzí balíčků](../concepts/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="968ae-134">For details on declaring dependencies and specifying version numbers, see [Package references in project files](../consume-packages/package-references-in-project-files.md) and [Package versioning](../concepts/package-versioning.md).</span></span> <span data-ttu-id="968ae-135">Je také možné Surface prostředků ze závislostí přímo v balíčku pomocí atributů `<IncludeAssets>` a `<ExcludeAssets>`.</span><span class="sxs-lookup"><span data-stu-id="968ae-135">It is also possible to surface assets from dependencies directly in the package by using the `<IncludeAssets>` and `<ExcludeAssets>` attributes.</span></span> <span data-ttu-id="968ae-136">Další informace najdete v Seee [řízení prostředků závislostí](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="968ae-136">For more information, seee [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

## <a name="add-an-optional-description-field"></a><span data-ttu-id="968ae-137">Přidat volitelné pole popisu</span><span class="sxs-lookup"><span data-stu-id="968ae-137">Add an optional description field</span></span>

[!INCLUDE [add description to package](includes/add-description.md)]

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a><span data-ttu-id="968ae-138">Vyberte jedinečný identifikátor balíčku a nastavte číslo verze.</span><span class="sxs-lookup"><span data-stu-id="968ae-138">Choose a unique package identifier and set the version number</span></span>

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="add-the-nugetbuildtaskspack-package"></a><span data-ttu-id="968ae-139">Přidat balíček NuGet. Build. Tasks. Pack</span><span class="sxs-lookup"><span data-stu-id="968ae-139">Add the NuGet.Build.Tasks.Pack package</span></span>

<span data-ttu-id="968ae-140">Pokud používáte nástroj MSBuild s projektem a PackageReference, který není typu SDK, přidejte do projektu balíček NuGet. Build. Tasks. Pack.</span><span class="sxs-lookup"><span data-stu-id="968ae-140">If you are using MSBuild with a non-SDK-style project and PackageReference, add the NuGet.Build.Tasks.Pack package to your project.</span></span>

1. <span data-ttu-id="968ae-141">Otevřete soubor projektu a přidejte následující za `<PropertyGroup>` element:</span><span class="sxs-lookup"><span data-stu-id="968ae-141">Open the project file and add the following after the `<PropertyGroup>` element:</span></span>

   ```xml
   <ItemGroup>
     <!-- ... -->
     <PackageReference Include="NuGet.Build.Tasks.Pack" Version="5.2.0"/>
     <!-- ... -->
   </ItemGroup>
   ```

2. <span data-ttu-id="968ae-142">Otevřete příkazový řádek pro vývojáře (do **vyhledávacího** pole zadejte **příkaz Developer Command Prompt**).</span><span class="sxs-lookup"><span data-stu-id="968ae-142">Open a Developer command prompt (In the **Search** box, type **Developer command prompt**).</span></span>

   <span data-ttu-id="968ae-143">Obvykle chcete spustit Developer Command Prompt pro Visual Studio z nabídky **Start** , jak bude nakonfigurován se všemi nezbytnými cestami pro MSBuild.</span><span class="sxs-lookup"><span data-stu-id="968ae-143">You typically want to start the Developer Command Prompt for Visual Studio from the **Start** menu, as it will be configured with all the necessary paths for MSBuild.</span></span>

3. <span data-ttu-id="968ae-144">Přepněte do složky obsahující soubor projektu a zadejte následující příkaz pro instalaci balíčku NuGet. Build. Tasks. Pack.</span><span class="sxs-lookup"><span data-stu-id="968ae-144">Switch to the folder containing the project file and type the following command to install the NuGet.Build.Tasks.Pack package.</span></span>

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

   <span data-ttu-id="968ae-145">Ujistěte se, že výstup nástroje MSBuild označuje, že sestavení bylo úspěšně dokončeno.</span><span class="sxs-lookup"><span data-stu-id="968ae-145">Make sure that the MSBuild output indicates that the build completed successfully.</span></span>

## <a name="run-the-msbuild--tpack-command"></a><span data-ttu-id="968ae-146">Spuštění příkazu MSBuild-t:Pack</span><span class="sxs-lookup"><span data-stu-id="968ae-146">Run the msbuild -t:pack command</span></span>

<span data-ttu-id="968ae-147">Chcete-li vytvořit balíček NuGet (`.nupkg` soubor) z projektu, spusťte příkaz `msbuild -t:pack`, který také automaticky vytvoří projekt:</span><span class="sxs-lookup"><span data-stu-id="968ae-147">To build a NuGet package (a `.nupkg` file) from the project, run the `msbuild -t:pack` command, which also builds the project automatically:</span></span>

<span data-ttu-id="968ae-148">Do příkazového řádku pro vývojáře pro Visual Studio zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="968ae-148">In the Developer command prompt for Visual Studio, type the following command:</span></span>

```cmd
# Uses the project file in the current folder by default
msbuild -t:pack
```

<span data-ttu-id="968ae-149">Výstup zobrazuje cestu k souboru `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="968ae-149">The output shows the path to the `.nupkg` file.</span></span>

```output
Microsoft (R) Build Engine version 16.1.76+g14b0a930a7 for .NET Framework
Copyright (C) Microsoft Corporation. All rights reserved.

Build started 8/5/2019 3:09:15 PM.
Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" on node 1 (pack target(s)).
GenerateTargetFrameworkMonikerAttribute:
Skipping target "GenerateTargetFrameworkMonikerAttribute" because all output files are up-to-date with respect to the input files.
CoreCompile:
  ...
CopyFilesToOutputDirectory:
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.dll" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll".
  ClassLib_DotNetStandard -> C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb".
GenerateNuspec:
  Successfully created package 'C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\AppLogger.1.0.0.nupkg'.
Done Building Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" (pack target(s)).

Build succeeded.
    0 Warning(s)
    0 Error(s)

Time Elapsed 00:00:01.21
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="968ae-150">Automaticky generovat balíček při sestavení</span><span class="sxs-lookup"><span data-stu-id="968ae-150">Automatically generate package on build</span></span>

<span data-ttu-id="968ae-151">Chcete-li automaticky spouštět `msbuild -t:pack` při sestavování nebo obnovování projektu, přidejte následující řádek do souboru projektu v rámci `<PropertyGroup>`:</span><span class="sxs-lookup"><span data-stu-id="968ae-151">To automatically run `msbuild -t:pack` when you build or restore the project, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

<span data-ttu-id="968ae-152">Když spustíte `msbuild -t:pack` v řešení, budou všechny projekty v řešení, které lze zabalit (vlastnost[<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) nastavená na `true`).</span><span class="sxs-lookup"><span data-stu-id="968ae-152">When you run `msbuild -t:pack` on a solution, this packs all the projects in the solution that are packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) property is set to `true`).</span></span>

> [!NOTE]
> <span data-ttu-id="968ae-153">Když balíček automaticky vygenerujete, čas k zabalení zvýší čas sestavení pro váš projekt.</span><span class="sxs-lookup"><span data-stu-id="968ae-153">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="test-package-installation"></a><span data-ttu-id="968ae-154">Instalace testovacího balíčku</span><span class="sxs-lookup"><span data-stu-id="968ae-154">Test package installation</span></span>

<span data-ttu-id="968ae-155">Před publikováním balíčku obvykle budete chtít otestovat proces instalace balíčku do projektu.</span><span class="sxs-lookup"><span data-stu-id="968ae-155">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="968ae-156">Testy zajistí, že všechny soubory v projektu budou mít všechny na správném místě.</span><span class="sxs-lookup"><span data-stu-id="968ae-156">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="968ae-157">Instalaci můžete v aplikaci Visual Studio nebo na příkazovém řádku otestovat ručně pomocí [kroků normální instalace balíčku](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span><span class="sxs-lookup"><span data-stu-id="968ae-157">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="968ae-158">Balíčky jsou neměnné.</span><span class="sxs-lookup"><span data-stu-id="968ae-158">Packages are immutable.</span></span> <span data-ttu-id="968ae-159">Pokud problém opravíte, znovu ho změňte a znovu spusťte. při opětovném testování bude stále použita stará verze balíčku, dokud [nevymažete složku globálních balíčků](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) .</span><span class="sxs-lookup"><span data-stu-id="968ae-159">If you correct a problem, change the contents of the package and pack again, when you retest you will still be using the old version of the package until you [clear your global packages](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) folder.</span></span> <span data-ttu-id="968ae-160">To je obzvláště důležité při testování balíčků, které nepoužívají jedinečný popisek předprodejní verze pro každé sestavení.</span><span class="sxs-lookup"><span data-stu-id="968ae-160">This is especially relevant when testing packages that don't use a unique prerelease label on every build.</span></span>

## <a name="next-steps"></a><span data-ttu-id="968ae-161">Další kroky</span><span class="sxs-lookup"><span data-stu-id="968ae-161">Next Steps</span></span>

<span data-ttu-id="968ae-162">Po vytvoření balíčku, který je `.nupkg` soubor, ho můžete publikovat do Galerie podle svého výběru, jak je popsáno v tématu [publikování balíčku](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="968ae-162">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="968ae-163">Můžete také chtít zvětšit možnosti vašeho balíčku nebo jinak podporovat jiné scénáře, jak je popsáno v následujících tématech:</span><span class="sxs-lookup"><span data-stu-id="968ae-163">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="968ae-164">Sada NuGet Pack a obnovení jako cíle MSBuild</span><span class="sxs-lookup"><span data-stu-id="968ae-164">NuGet pack and restore as MSBuild targets</span></span>](../reference/msbuild-targets.md)
- [<span data-ttu-id="968ae-165">Správa verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="968ae-165">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="968ae-166">Podpora více cílových architektur</span><span class="sxs-lookup"><span data-stu-id="968ae-166">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="968ae-167">Transformace zdrojových a konfiguračních souborů</span><span class="sxs-lookup"><span data-stu-id="968ae-167">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="968ae-168">Lokalizace</span><span class="sxs-lookup"><span data-stu-id="968ae-168">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="968ae-169">Předběžné verze verzí</span><span class="sxs-lookup"><span data-stu-id="968ae-169">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="968ae-170">Nastavení typu balíčku</span><span class="sxs-lookup"><span data-stu-id="968ae-170">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="968ae-171">Vytváření balíčků pomocí sestavení zprostředkovatele komunikace s objekty COM</span><span class="sxs-lookup"><span data-stu-id="968ae-171">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="968ae-172">Nakonec existují další typy balíčků, o kterých byste měli vědět:</span><span class="sxs-lookup"><span data-stu-id="968ae-172">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="968ae-173">Nativní balíčky</span><span class="sxs-lookup"><span data-stu-id="968ae-173">Native Packages</span></span>](../guides/native-packages.md)
- [<span data-ttu-id="968ae-174">Balíčky symbolů</span><span class="sxs-lookup"><span data-stu-id="968ae-174">Symbol Packages</span></span>](../create-packages/symbol-packages-snupkg.md)
