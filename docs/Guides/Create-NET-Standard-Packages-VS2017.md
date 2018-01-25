---
title: "Vytvoření balíčků NuGet standardní 2.0 .NET s Visual Studio 2017 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 05/23/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Návod začátku do konce, vytváření balíčků NuGet pro standardní 2.0 rozhraní .NET pomocí nástroje NuGet 4.x a Visual Studio 2017."
keywords: "Vytvoření balíčku, .NET Standard balíčky .NET Core"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: aae38dd141c688a6eccc18cabea9e8245dbc36c5
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
---
# <a name="create-net-standard-20-packages-with-visual-studio-2017"></a><span data-ttu-id="e58b7-104">Vytvoření balíčků standardní rozhraní .NET 2.0 s Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="e58b7-104">Create .NET Standard 2.0 packages with Visual Studio 2017</span></span>

<span data-ttu-id="e58b7-105">*Platí pro NuGet 4.x+ a MSBuild 15.3 + v souladu s Visual Studio 2017 Update 3 nebo novější. U starších verzí Visual Studio 2017, tyto pokyny platí pro standardní 1.4 .NET 1.6 změnou \<TargetFramework\> vlastnost. Viz také [vytvořit .NET standardní balíčky s Visual Studiem 2015](../guides/create-net-standard-packages-vs2015.md) pro práci s NuGet 3.x+.*</span><span class="sxs-lookup"><span data-stu-id="e58b7-105">*Applies to NuGet 4.x+ and MSBuild 15.3+ as provided with Visual Studio 2017 Update 3 and later. For earlier versions of Visual Studio 2017, these instructions apply to .NET Standard 1.4 to 1.6 by changing the \<TargetFramework\> property. Also see [Create .NET Standard Packages with Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md) for working with NuGet 3.x+.*</span></span>

<span data-ttu-id="e58b7-106">[Standardní knihovny .NET](/dotnet/articles/standard/library) je formální specifikaci rozhraní API technologie .NET by měla být k dispozici pro všechny moduly runtime rozhraní .NET, tím větší jednotnost vytváří v ekosystému .NET.</span><span class="sxs-lookup"><span data-stu-id="e58b7-106">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="e58b7-107">Standardní knihovny .NET definuje jednotnou sadu BCL (základní třída knihovna) rozhraní API pro všechny platformy .NET implementovat, nezávisle na zatížení.</span><span class="sxs-lookup"><span data-stu-id="e58b7-107">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="e58b7-108">Ji umožňuje vývojářům vytvářet PCLs, které jsou použitelné pro všechny moduly runtime rozhraní .NET, a snižuje, pokud není eliminuje direktivy specifické pro platformu Podmíněná kompilace v sdíleného kódu.</span><span class="sxs-lookup"><span data-stu-id="e58b7-108">It enables developers to produce PCLs that are usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="e58b7-109">Tento průvodce vás provede procesem vytváření balíčku nuget cílení na rozhraní .NET standardní knihovny 2.0 s Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="e58b7-109">This guide walks you through creating a nuget package targeting .NET Standard Library 2.0 with Visual Studio 2017.</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="e58b7-110">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="e58b7-110">Pre-requisites</span></span>

<span data-ttu-id="e58b7-111">Tento postup vyžaduje Visual Studio 2017 Update 3 se **vývoj pro různé platformy .NET Core** zatížení.</span><span class="sxs-lookup"><span data-stu-id="e58b7-111">This walkthrough requires Visual Studio 2017 Update 3 with the **.NET Core cross-platform development** workload.</span></span> <span data-ttu-id="e58b7-112">Edice Community můžete nainstalovat zdarma z [visualstudio.com](https://www.visualstudio.com/), nebo použijte edice Professional a Enterprise.</span><span class="sxs-lookup"><span data-stu-id="e58b7-112">You can install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/), or use the Professional and Enterprise editions.</span></span>

<span data-ttu-id="e58b7-113">Vyžadují pracovního vytížení, zobrazí se následující v instalačním programu sady Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="e58b7-113">The require workload appears as follows in the Visual Studio installer:</span></span>

![Vývoj pro různé platformy zatížení .NET core v instalačním programu Visual Studio](media/NuGet4-01-Workload.png)

## <a name="create-the-net-standard-class-library-project"></a><span data-ttu-id="e58b7-115">Vytvořte standardní rozhraní .NET projektu knihovny tříd</span><span class="sxs-lookup"><span data-stu-id="e58b7-115">Create the .NET Standard class library project</span></span>

1. <span data-ttu-id="e58b7-116">V sadě Visual Studio **soubor > Nový > projekt**, rozbalte **Visual C# > .NET Standard** uzlu, vyberte **knihovny tříd (Net Standard)**, změňte název na AppLogger, a Klikněte na tlačítko OK.</span><span class="sxs-lookup"><span data-stu-id="e58b7-116">In Visual Studio, **File > New > Project**, expand the **Visual C# > .NET Standard** node, select **Class Library (Net Standard)**, change the name to AppLogger, and click OK.</span></span>

    ![Vytvoření nového projektu knihovny tříd](media/NuGet4-02-NewProject.png)

1. <span data-ttu-id="e58b7-118">Změnit konfiguraci sestavení na **verze**.</span><span class="sxs-lookup"><span data-stu-id="e58b7-118">Change the build configuration to **Release**.</span></span>
1. <span data-ttu-id="e58b7-119">Klikněte pravým tlačítkem myši `AppLogger` projekt v Průzkumníku řešení, vyberte **vlastnosti**, vyberte **sestavení** kartě, zaškrtněte políčko pro **souborů dokumentace XML**a nastavte Název souboru k právě `AppLogger.xml`.</span><span class="sxs-lookup"><span data-stu-id="e58b7-119">Right-click the `AppLogger` project in Solution Explorer, select **Properties**, select the **Build** tab, check the box for **XML documentation file**, and set the filename to just `AppLogger.xml`.</span></span> <span data-ttu-id="e58b7-120">Potom uložte projekt.</span><span class="sxs-lookup"><span data-stu-id="e58b7-120">Then save the project.</span></span>

1. <span data-ttu-id="e58b7-121">Přidat kód pro součásti, například následující (který jasně právě výstupy zpráv do konzoly):</span><span class="sxs-lookup"><span data-stu-id="e58b7-121">Add your code to the component, such as the following (which clearly just outputs messages to the console):</span></span>

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                Console.WriteLine(text);
            }
        }
    }
    ```

1. <span data-ttu-id="e58b7-122">Sestavení projektu (s konfigurací verzi) a zkontrolujte, že jsou v rámci vytváří soubory DLL a XML `bin\Release\netstandard2.0` složky.</span><span class="sxs-lookup"><span data-stu-id="e58b7-122">Build the project (with the Release configuration) and check that DLL and XML files are produced within the `bin\Release\netstandard2.0` folder.</span></span>

## <a name="edit-metadata-in-the-csproj-file"></a><span data-ttu-id="e58b7-123">Upravit metadata v souboru .csproj</span><span class="sxs-lookup"><span data-stu-id="e58b7-123">Edit metadata in the .csproj file</span></span>

<span data-ttu-id="e58b7-124">S projekty NuGet 4.0 a .NET Core, metadata balíčků je obsažena přímo v `.csproj` souboru místo externích souborů, jako `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="e58b7-124">With NuGet 4.0 and .NET Core projects, package metadata is contained directly in the `.csproj` file instead of external files such as a `.nuspec`.</span></span> <span data-ttu-id="e58b7-125">Úplný popis této metadat se nachází v [NuGet pack a obnovit jako cíle MSBuild](../schema/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="e58b7-125">A full description of that metadata is found in [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md#pack-target).</span></span>

1. <span data-ttu-id="e58b7-126">Klikněte pravým tlačítkem na projekt v Průzkumníku řešení, vyberte **upravit AppLogger.csproj**a pak upravte první skupinu vlastnost k přidání informací balíčku, například následující:</span><span class="sxs-lookup"><span data-stu-id="e58b7-126">Right-click the project in Solution Explorer, select **Edit AppLogger.csproj**, and then edit the first property group to include package information such as the following:</span></span>

    ```xml
    <PropertyGroup>
        <TargetFramework>netstandard2.0</TargetFramework>
        <PackageId>AppLogger.YOUR_NAME</PackageId>
        <PackageVersion>1.0.0</PackageVersion>
        <Authors>YOUR_NAME</Authors>
        <Description>Awesome application logging utility</Description>
        <PackageRequireLicenseAcceptance>false</PackageRequireLicenseAcceptance>
        <PackageReleaseNotes>First release</PackageReleaseNotes>
        <Copyright>Copyright 2017 (c) Contoso Corporation. All rights reserved.</Copyright>
        <PackageTags>logger logging logs</PackageTags>
    </PropertyGroup>
    ```

1. <span data-ttu-id="e58b7-127">Uložte projekt, pak pravým tlačítkem na řešení a vyberte **sestavit řešení** znovu vygenerovat všechny soubory pro balíček, tentokrát s metadaty správné.</span><span class="sxs-lookup"><span data-stu-id="e58b7-127">Save the project, then right-click the solution and select **Build Solution** to again generate all the files for the package, this time with the correct metadata.</span></span>

## <a name="package-the-component"></a><span data-ttu-id="e58b7-128">Balíček součásti</span><span class="sxs-lookup"><span data-stu-id="e58b7-128">Package the component</span></span>

<span data-ttu-id="e58b7-129">NuGet 4.0 podporuje cíl pack pomocí nástroje MSBuild verze 15.1 + (včetně nástroje MSBuild 15.3 jako součást Visual Studio 2017 Update 3) Pokud projekt obsahuje metadata potřebný balíček, jak byl přidán v předchozí části.</span><span class="sxs-lookup"><span data-stu-id="e58b7-129">NuGet 4.0 supports a pack target using MSBuild version 15.1+ (including MSBuild 15.3 as part of Visual Studio 2017 Update 3) when the project contains the necessary package metadata, as was added in the previous section.</span></span> <span data-ttu-id="e58b7-130">K vyvolání MSBuild tímto způsobem, jednoduše zadejte cíl pack na příkazovém řádku ve stejné složce jako `.csproj` souboru:</span><span class="sxs-lookup"><span data-stu-id="e58b7-130">To invoke MSBuild in this way, simply specify the pack target on the command line in the same folder as the `.csproj` file:</span></span>

    msbuild /t:pack /p:Configuration=Release

<span data-ttu-id="e58b7-131">Další možnosti s `msbuild /t:pack`, soubory obsahu, symboly, například včetně a zdrojový kód, najdete v části [NuGet pack a obnovit jako cíle MSBuild](../schema/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="e58b7-131">For additional options with `msbuild /t:pack`, such as including content files, symbols, and source code, see [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md#pack-target).</span></span>

<span data-ttu-id="e58b7-132">V každém případě výše uvedeného příkazu generuje `AppLogger.YOUR_NAME.1.0.0.nupkg` v `bin\Release` složky ve výchozím nastavení, jako je sestavení pro tuto konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="e58b7-132">In any case, the command above generates `AppLogger.YOUR_NAME.1.0.0.nupkg` in the `bin\Release` folder by default, as it builds that configuration.</span></span> <span data-ttu-id="e58b7-133">V případě vynechání `/p` přepínače, bude výchozí konfigurace `Debug`.</span><span class="sxs-lookup"><span data-stu-id="e58b7-133">If you omit the `/p` switch, the default configuration will be `Debug`.</span></span> 

<span data-ttu-id="e58b7-134">Otevření tohoto souboru v nástroje, jako [Explorer balíček NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) a rozšiřování všechny uzly, zobrazí se následující obsah:</span><span class="sxs-lookup"><span data-stu-id="e58b7-134">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you'll see the following contents:</span></span>

![Průzkumník balíček NuGet zobrazující AppLogger balíčku](media/NuGet4-03-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="e58b7-136">A `.nupkg` soubor je právě soubor ZIP s jiné rozšíření.</span><span class="sxs-lookup"><span data-stu-id="e58b7-136">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="e58b7-137">Můžete také zkontrolovat obsah balíčku, potom změnou `.nupkg` k `.zip`, ale nezapomeňte obnovit rozšíření před balíčku se nahrávají na nuget.org.</span><span class="sxs-lookup"><span data-stu-id="e58b7-137">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="e58b7-138">Pokud chcete zpřístupnit vašeho balíčku jinými vývojáři, postupujte podle pokynů [publikování balíčku](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="e58b7-138">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="e58b7-139">Související témata</span><span class="sxs-lookup"><span data-stu-id="e58b7-139">Related topics</span></span>

- <span data-ttu-id="e58b7-140">[Balíček odkazy v souborech projektu](../consume-packages/package-references-in-project-files.md) popisuje všechny podrobnosti o popisující vašeho balíčku přímo v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="e58b7-140">[Package References in Project Files](../consume-packages/package-references-in-project-files.md) describes all the details of describing your package directly in the project file.</span></span>
- <span data-ttu-id="e58b7-141">[NuGet pack a obnovit jako cíle MSBuild](../schema/msbuild-targets.md) popisuje všechny možnosti použití `msbuild /t:pack` k vytvoření balíčku.</span><span class="sxs-lookup"><span data-stu-id="e58b7-141">[NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md) describes all the options for using `msbuild /t:pack` to create the package.</span></span>
- [<span data-ttu-id="e58b7-142">Standardní knihovny .NET dokumentaci</span><span class="sxs-lookup"><span data-stu-id="e58b7-142">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="e58b7-143">Portování do .NET Core z rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="e58b7-143">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
