---
title: Vytvoření balíčku NuGet pomocí rozhraní se kontinua dotnet CLI
description: Podrobný průvodce procesem navrhování a vytváření balíčku NuGet, včetně klíčových rozhodovacích bodů, jako jsou soubory a správa verzí.
author: karann-msft
ms.author: karann
ms.date: 02/20/2020
ms.topic: conceptual
ms.openlocfilehash: 712e4c7159aa9719052330d8e45f63e18e390325
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "78230574"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a><span data-ttu-id="97205-103">Vytvoření balíčku NuGet pomocí rozhraní se kontinua dotnet CLI</span><span class="sxs-lookup"><span data-stu-id="97205-103">Create a NuGet package using the dotnet CLI</span></span>

<span data-ttu-id="97205-104">Bez ohledu na to, co váš balíček dělá nebo jaký `nuget.exe` kód `dotnet.exe`obsahuje, použijete jeden z nástrojů rozhraní rozhraní rozhraní cli, nebo , k balení této funkce do součásti, která může být sdílena s libovolným počtem jiných vývojářů.</span><span class="sxs-lookup"><span data-stu-id="97205-104">No matter what your package does or what code it contains, you use one of the CLI tools, either `nuget.exe` or `dotnet.exe`, to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="97205-105">Tento článek popisuje, jak vytvořit balíček pomocí rozhraní SE kontinu dotnet CLI.</span><span class="sxs-lookup"><span data-stu-id="97205-105">This article describes how to create a package using the dotnet CLI.</span></span> <span data-ttu-id="97205-106">Informace o `dotnet` instalaci nařízení o nastavení systému řízení o elIt naleznete v [tématu Instalace klientských nástrojů NuGet](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="97205-106">To install the `dotnet` CLI, see [Install NuGet client tools](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="97205-107">Počínaje Visual Studio 2017, dotnet CLI je součástí úloh .NET Core.</span><span class="sxs-lookup"><span data-stu-id="97205-107">Starting in Visual Studio 2017, the dotnet CLI is included with .NET Core workloads.</span></span>

<span data-ttu-id="97205-108">Pro projekty .NET Core a .NET Standard, které používají [formát ve stylu sady SDK](../resources/check-project-format.md), a všechny ostatní projekty ve stylu sady SDK použije aplikace NuGet informace v souboru projektu přímo k vytvoření balíčku.</span><span class="sxs-lookup"><span data-stu-id="97205-108">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span> <span data-ttu-id="97205-109">Podrobné kurzy naleznete v tématu [Vytvoření standardních balíčků .NET pomocí rozhraní SE kontinu pro dotnet NEBO](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) [Vytvoření standardních balíčků .NET pomocí sady Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="97205-109">For step-by-step tutorials, see [Create .NET Standard Packages with dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) or [Create .NET Standard Packages with Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span></span>

<span data-ttu-id="97205-110">`msbuild -t:pack`je funkce ekvivalentní `dotnet pack`.</span><span class="sxs-lookup"><span data-stu-id="97205-110">`msbuild -t:pack` is functionality equivalent to `dotnet pack`.</span></span> <span data-ttu-id="97205-111">Pokud chcete stavět pomocí MSBuild, [přečtěte si informace o vytvoření balíčku NuGet pomocí služby MSBuild](creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="97205-111">To build with MSBuild, see [Create a NuGet package using MSBuild](creating-a-package-msbuild.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="97205-112">Toto téma se týká projektů [ve stylu sady SDK,](../resources/check-project-format.md) obvykle projektů .NET Core a .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="97205-112">This topic applies to [SDK-style](../resources/check-project-format.md) projects, typically .NET Core and .NET Standard projects.</span></span>

## <a name="set-properties"></a><span data-ttu-id="97205-113">Nastavení vlastností</span><span class="sxs-lookup"><span data-stu-id="97205-113">Set properties</span></span>

<span data-ttu-id="97205-114">K vytvoření balíčku jsou vyžadovány následující vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="97205-114">The following properties are required to create a package.</span></span>

- <span data-ttu-id="97205-115">`PackageId`, identifikátor balíčku, který musí být jedinečný v galerii, která je hostitelem balíčku.</span><span class="sxs-lookup"><span data-stu-id="97205-115">`PackageId`, the package identifier, which must be unique across the gallery that hosts the package.</span></span> <span data-ttu-id="97205-116">Pokud není zadán, výchozí `AssemblyName`hodnota je .</span><span class="sxs-lookup"><span data-stu-id="97205-116">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="97205-117">`Version`, konkrétní číslo verze ve tvaru *Major.Minor.Patch[-Přípona],* kde *-Přípona* identifikuje [předběžné verze](prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="97205-117">`Version`, a specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md).</span></span> <span data-ttu-id="97205-118">Pokud není zadán, výchozí hodnota je 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="97205-118">If not specified, the default value is 1.0.0.</span></span>
- <span data-ttu-id="97205-119">Název balíčku, jak by se měl objevit na hostiteli (jako nuget.org)</span><span class="sxs-lookup"><span data-stu-id="97205-119">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="97205-120">`Authors`, informace o autorovi a majiteli.</span><span class="sxs-lookup"><span data-stu-id="97205-120">`Authors`, author and owner information.</span></span> <span data-ttu-id="97205-121">Pokud není zadán, výchozí `AssemblyName`hodnota je .</span><span class="sxs-lookup"><span data-stu-id="97205-121">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="97205-122">`Company`, název vaší společnosti.</span><span class="sxs-lookup"><span data-stu-id="97205-122">`Company`, your company name.</span></span> <span data-ttu-id="97205-123">Pokud není zadán, výchozí `AssemblyName`hodnota je .</span><span class="sxs-lookup"><span data-stu-id="97205-123">If not specified, the default value is `AssemblyName`.</span></span>

<span data-ttu-id="97205-124">V sadě Visual Studio můžete tyto hodnoty nastavit ve vlastnostech projektu (klikněte pravým tlačítkem myši na projekt v Průzkumníku řešení, zvolte **Vlastnosti**a vyberte kartu **Balíček).**</span><span class="sxs-lookup"><span data-stu-id="97205-124">In Visual Studio, you can set these values in the project properties (right-click the project in Solution Explorer, choose **Properties**, and select the **Package** tab).</span></span> <span data-ttu-id="97205-125">Tyto vlastnosti můžete také nastavit přímo`.csproj`v souborech projektu ( ).</span><span class="sxs-lookup"><span data-stu-id="97205-125">You can also set these properties directly in the project files (`.csproj`).</span></span>

```xml
<PropertyGroup>
  <PackageId>AppLogger</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> <span data-ttu-id="97205-126">Podejte balíček identifikátor, který je jedinečný v celé nuget.org nebo jakýkoli zdroj balíčku, který používáte.</span><span class="sxs-lookup"><span data-stu-id="97205-126">Give the package an identifier that's unique across nuget.org or whatever package source you're using.</span></span>

<span data-ttu-id="97205-127">Následující příklad ukazuje jednoduchý, kompletní soubor projektu s těmito vlastnostmi zahrnuty.</span><span class="sxs-lookup"><span data-stu-id="97205-127">The following example shows a simple, complete project file with these properties included.</span></span> <span data-ttu-id="97205-128">(Pomocí `dotnet new classlib` příkazu můžete vytvořit nový výchozí projekt.)</span><span class="sxs-lookup"><span data-stu-id="97205-128">(You can create a new default project using the `dotnet new classlib` command.)</span></span>

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

<span data-ttu-id="97205-129">Můžete `Title`také nastavit volitelné vlastnosti, `PackageDescription`například , `PackageTags`a , jak je popsáno v [cílech balíčku MSBuild](../reference/msbuild-targets.md#pack-target), [Řízení prostředků závislostí](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)a [vlastnosti metadat NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).</span><span class="sxs-lookup"><span data-stu-id="97205-129">You can also set the optional properties, such as `Title`, `PackageDescription`, and `PackageTags`, as described in [MSBuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

> [!NOTE]
> <span data-ttu-id="97205-130">U balíčků vytvořených pro veřejnou spotřebu věnujte zvláštní pozornost vlastnosti **PackageTags,** protože značky pomáhají ostatním najít váš balíček a pochopit, co dělá.</span><span class="sxs-lookup"><span data-stu-id="97205-130">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

<span data-ttu-id="97205-131">Podrobnosti o deklarování závislostí a určení čísel verzí naleznete [v tématu Odkazy na balíčky v souborech projektu](../consume-packages/package-references-in-project-files.md) a [správa verzí balíčků](../concepts/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="97205-131">For details on declaring dependencies and specifying version numbers, see [Package references in project files](../consume-packages/package-references-in-project-files.md) and [Package versioning](../concepts/package-versioning.md).</span></span> <span data-ttu-id="97205-132">Je také možné povrchové prostředky ze závislostí přímo `<IncludeAssets>` `<ExcludeAssets>` v balíčku pomocí atributy a.</span><span class="sxs-lookup"><span data-stu-id="97205-132">It is also possible to surface assets from dependencies directly in the package by using the `<IncludeAssets>` and `<ExcludeAssets>` attributes.</span></span> <span data-ttu-id="97205-133">Další informace naleznete v tématu [Controlling závislost assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="97205-133">For more information, seee [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

## <a name="add-an-optional-description-field"></a><span data-ttu-id="97205-134">Přidání volitelného pole popisu</span><span class="sxs-lookup"><span data-stu-id="97205-134">Add an optional description field</span></span>

[!INCLUDE [add description to package](includes/add-description.md)]

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a><span data-ttu-id="97205-135">Zvolte jedinečný identifikátor balíčku a nastavte číslo verze.</span><span class="sxs-lookup"><span data-stu-id="97205-135">Choose a unique package identifier and set the version number</span></span>

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="run-the-pack-command"></a><span data-ttu-id="97205-136">Spuštění příkazu pack</span><span class="sxs-lookup"><span data-stu-id="97205-136">Run the pack command</span></span>

<span data-ttu-id="97205-137">Chcete-li vytvořit balíček `.nupkg` NuGet (soubor) `dotnet pack` z projektu, spusťte příkaz, který také automaticky vytvoří projekt:</span><span class="sxs-lookup"><span data-stu-id="97205-137">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```dotnetcli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="97205-138">Výstup zobrazuje cestu k `.nupkg` souboru.</span><span class="sxs-lookup"><span data-stu-id="97205-138">The output shows the path to the `.nupkg` file.</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="97205-139">Automaticky generovat balíček při sestavení</span><span class="sxs-lookup"><span data-stu-id="97205-139">Automatically generate package on build</span></span>

<span data-ttu-id="97205-140">Chcete-li `dotnet pack` se `dotnet build`při spuštění automaticky spustit , `<PropertyGroup>`přidejte do souboru projektu následující řádek v části :</span><span class="sxs-lookup"><span data-stu-id="97205-140">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

<span data-ttu-id="97205-141">Při spuštění `dotnet pack` na řešení, to zabalí všechny projekty v[<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) řešení, které `true`jsou sbalitelné ( vlastnost je nastavena na ).</span><span class="sxs-lookup"><span data-stu-id="97205-141">When you run `dotnet pack` on a solution, this packs all the projects in the solution that are packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) property is set to `true`).</span></span>

> [!NOTE]
> <span data-ttu-id="97205-142">Při automatickém generování balíčku čas balení zvyšuje dobu sestavení pro váš projekt.</span><span class="sxs-lookup"><span data-stu-id="97205-142">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="test-package-installation"></a><span data-ttu-id="97205-143">Instalace testovacího balíčku</span><span class="sxs-lookup"><span data-stu-id="97205-143">Test package installation</span></span>

<span data-ttu-id="97205-144">Před publikováním balíčku obvykle chcete otestovat proces instalace balíčku do projektu.</span><span class="sxs-lookup"><span data-stu-id="97205-144">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="97205-145">Testy ujistěte se, že nutně soubory všechny skončí na jejich správných místech v projektu.</span><span class="sxs-lookup"><span data-stu-id="97205-145">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="97205-146">Instalace můžete testovat ručně v sadě Visual Studio nebo na příkazovém řádku pomocí běžných [kroků instalace balíčku](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span><span class="sxs-lookup"><span data-stu-id="97205-146">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="97205-147">Balíčky jsou neměnné.</span><span class="sxs-lookup"><span data-stu-id="97205-147">Packages are immutable.</span></span> <span data-ttu-id="97205-148">Pokud problém opravíte, změňte obsah balíčku a zabalte znovu, když znovu otestujete, budete stále používat starou verzi balíčku, dokud [nevymažete složku globálních balíčků.](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders)</span><span class="sxs-lookup"><span data-stu-id="97205-148">If you correct a problem, change the contents of the package and pack again, when you retest you will still be using the old version of the package until you [clear your global packages](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) folder.</span></span> <span data-ttu-id="97205-149">To je zvláště důležité při testování balíčků, které nepoužívají jedinečný popisek předběžné verze v každém sestavení.</span><span class="sxs-lookup"><span data-stu-id="97205-149">This is especially relevant when testing packages that don't use a unique prerelease label on every build.</span></span>

## <a name="next-steps"></a><span data-ttu-id="97205-150">Další kroky</span><span class="sxs-lookup"><span data-stu-id="97205-150">Next Steps</span></span>

<span data-ttu-id="97205-151">Po vytvoření balíčku, což je `.nupkg` soubor, můžete jej publikovat do galerie podle vašeho výběru, jak je popsáno na [publikování balíčku](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="97205-151">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="97205-152">Můžete také rozšířit možnosti balíčku nebo jinak podporovat jiné scénáře, jak je popsáno v následujících tématech:</span><span class="sxs-lookup"><span data-stu-id="97205-152">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="97205-153">Správa verzí balíčku</span><span class="sxs-lookup"><span data-stu-id="97205-153">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="97205-154">Podpora více cílových architektur</span><span class="sxs-lookup"><span data-stu-id="97205-154">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="97205-155">Přidat ikonu balíčku</span><span class="sxs-lookup"><span data-stu-id="97205-155">Add a package icon</span></span>](../reference/nuspec.md#icon)
- [<span data-ttu-id="97205-156">Transformace zdrojových a konfiguračních souborů</span><span class="sxs-lookup"><span data-stu-id="97205-156">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="97205-157">Lokalizace</span><span class="sxs-lookup"><span data-stu-id="97205-157">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="97205-158">Předběžné verze</span><span class="sxs-lookup"><span data-stu-id="97205-158">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="97205-159">Nastavení typu balíčku</span><span class="sxs-lookup"><span data-stu-id="97205-159">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="97205-160">Vytváření balíčků pomocí meziop sestavení COM</span><span class="sxs-lookup"><span data-stu-id="97205-160">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="97205-161">Nakonec existují další typy balíčků, které mají být vědomi:</span><span class="sxs-lookup"><span data-stu-id="97205-161">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="97205-162">Nativní balíčky</span><span class="sxs-lookup"><span data-stu-id="97205-162">Native Packages</span></span>](../guides/native-packages.md)
- [<span data-ttu-id="97205-163">Balíčky symbolů</span><span class="sxs-lookup"><span data-stu-id="97205-163">Symbol Packages</span></span>](../create-packages/symbol-packages-snupkg.md)
