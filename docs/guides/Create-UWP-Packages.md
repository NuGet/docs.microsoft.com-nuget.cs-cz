---
title: Vytvoření balíčků NuGet pro Univerzální platforma Windows
description: Kompletní návod k vytváření balíčků NuGet pomocí prostředí Windows Runtime komponenty pro Univerzální platforma Windows.
author: karann-msft
ms.author: karann
ms.date: 03/21/2017
ms.topic: tutorial
ms.openlocfilehash: 1683349faacdf5ad47baafeef3457bbb3bb1baa9
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488990"
---
# <a name="create-uwp-packages"></a><span data-ttu-id="a0897-103">Vytvoření balíčků UPW</span><span class="sxs-lookup"><span data-stu-id="a0897-103">Create UWP packages</span></span>

<span data-ttu-id="a0897-104">[Univerzální platforma Windows (UWP)](https://developer.microsoft.com/windows) poskytuje běžnou aplikační platformu pro každé zařízení s Windows 10.</span><span class="sxs-lookup"><span data-stu-id="a0897-104">The [Universal Windows Platform (UWP)](https://developer.microsoft.com/windows) provides a common app platform for every device that runs Windows 10.</span></span> <span data-ttu-id="a0897-105">V rámci tohoto modelu můžou aplikace pro UWP volat rozhraní API WinRT, která jsou společná pro všechna zařízení, a taky rozhraní API (včetně Win32 a .NET), která jsou specifická pro řadu zařízení, ve které je aplikace spuštěná.</span><span class="sxs-lookup"><span data-stu-id="a0897-105">Within this model, UWP apps can call both the WinRT APIs that are common to all devices, and also APIs (including Win32 and .NET) that are specific to the device family on which the app is running.</span></span>

<span data-ttu-id="a0897-106">V tomto návodu vytvoříte balíček NuGet s nativní komponentou UWP (včetně ovládacího prvku XAML), který lze použít v spravovaných i nativních projektech.</span><span class="sxs-lookup"><span data-stu-id="a0897-106">In this walkthrough you create a NuGet package with a native UWP component (including a XAML control) that can be used in both Managed and Native projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a0897-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="a0897-107">Prerequisites</span></span>

1. <span data-ttu-id="a0897-108">Visual Studio 2017 nebo Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="a0897-108">Visual Studio 2017 or Visual Studio 2015.</span></span> <span data-ttu-id="a0897-109">Nainstalujte si bezplatnou edici 2017 Community Edition od [VisualStudio.com](https://www.visualstudio.com/); můžete použít i edice Professional a Enterprise.</span><span class="sxs-lookup"><span data-stu-id="a0897-109">Install the 2017 Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well.</span></span>

1. <span data-ttu-id="a0897-110">Rozhraní příkazového řádku NuGet</span><span class="sxs-lookup"><span data-stu-id="a0897-110">NuGet CLI.</span></span> <span data-ttu-id="a0897-111">Stáhněte si nejnovější verzi `nuget.exe` z [NuGet.org/downloads](https://nuget.org/downloads)a uložte ji do umístění dle vašeho výběru (stažení je `.exe` přímo).</span><span class="sxs-lookup"><span data-stu-id="a0897-111">Download the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice (the download is the `.exe` directly).</span></span> <span data-ttu-id="a0897-112">Pak přidejte toto umístění do proměnné prostředí PATH, pokud ještě není.</span><span class="sxs-lookup"><span data-stu-id="a0897-112">Then add that location to your PATH environment variable if it isn't already.</span></span>

## <a name="create-a-uwp-windows-runtime-component"></a><span data-ttu-id="a0897-113">Vytvoření komponenty prostředí Windows Runtime UWP</span><span class="sxs-lookup"><span data-stu-id="a0897-113">Create a UWP Windows Runtime component</span></span>

1. <span data-ttu-id="a0897-114">V aplikaci Visual Studio zvolte **soubor > nový > projekt**, rozbalte položku **Visual C++ > Windows > univerzální** uzel, vyberte šablonu **prostředí Windows Runtime součásti (Universal Windows)** , změňte název na ImageEnhancer a klikněte na OK.</span><span class="sxs-lookup"><span data-stu-id="a0897-114">In Visual Studio, choose **File > New > Project**, expand the **Visual C++ > Windows > Universal** node, select the **Windows Runtime Component (Universal Windows)** template, change the name to ImageEnhancer, and click OK.</span></span> <span data-ttu-id="a0897-115">Po zobrazení výzvy přijměte výchozí hodnoty pro cílovou verzi a minimální verzi.</span><span class="sxs-lookup"><span data-stu-id="a0897-115">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

    ![Vytváření nového projektu součásti prostředí Windows Runtime pro UWP](media/UWP-NewProject.png)

1. <span data-ttu-id="a0897-117">Klikněte pravým tlačítkem na projekt v Průzkumník řešení, vyberte **přidat > novou položku**, klikněte na uzel **Visual C++ > XAML** , vyberte **ovládací prvek**s šablonou, změňte název na AwesomeImageControl. cpp a klikněte na tlačítko **Přidat**:</span><span class="sxs-lookup"><span data-stu-id="a0897-117">Right click the project in Solution Explorer, select **Add > New Item**, click the **Visual C++ > XAML** node, select **Templated Control**, change the name to AwesomeImageControl.cpp, and click **Add**:</span></span>

    ![Přidání nové položky ovládacího prvku v šabloně XAML do projektu](media/UWP-NewXAMLControl.png)

1. <span data-ttu-id="a0897-119">Klikněte pravým tlačítkem na projekt v Průzkumník řešení a vyberte **Vlastnosti.**</span><span class="sxs-lookup"><span data-stu-id="a0897-119">Right-click the project in Solution Explorer and select **Properties.**</span></span> <span data-ttu-id="a0897-120">Na stránce Vlastnosti rozbalte položku **Vlastnosti konfigurace > CC++ /** a klikněte na možnost **výstupní soubory**.</span><span class="sxs-lookup"><span data-stu-id="a0897-120">In the Properties page, expand **Configuration Properties > C/C++** and click **Output Files**.</span></span> <span data-ttu-id="a0897-121">V pravém podokně změňte hodnotu pro **Generovat soubory dokumentace XML** na Ano:</span><span class="sxs-lookup"><span data-stu-id="a0897-121">In the pane on the right, change the value for **Generate XML Documentation Files** to Yes:</span></span>

    ![Nastavení generovat soubory dokumentace XML na Ano](media/UWP-GenerateXMLDocFiles.png)

1. <span data-ttu-id="a0897-123">Klikněte pravým tlačítkem na *řešení* , vyberte **dávkové sestavení**a zaškrtněte tři pole pro ladění v dialogovém okně, jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="a0897-123">Right click the *solution* now, select **Batch Build**, check the three Debug boxes in the dialog as shown below.</span></span> <span data-ttu-id="a0897-124">Tím je zajištěno, že při sestavení vygenerujete úplnou sadu artefaktů pro každý cílový systém, který systém Windows podporuje.</span><span class="sxs-lookup"><span data-stu-id="a0897-124">This makes sure that when you do a build, you generate a full set of artifacts for each of the target systems that Windows supports.</span></span>

    ![Dávkové sestavení](media/UWP-BatchBuild.png)

1. <span data-ttu-id="a0897-126">V dialogovém okně dávkové sestavení a kliknutím na **sestavení** ověřte projekt a vytvořte výstupní soubory, které potřebujete pro balíček NuGet.</span><span class="sxs-lookup"><span data-stu-id="a0897-126">In the Batch Build dialog, and click **Build** to verify the project and create the output files that you need for the NuGet package.</span></span>

> [!Note]
> <span data-ttu-id="a0897-127">V tomto návodu použijete pro balíček artefakty ladění.</span><span class="sxs-lookup"><span data-stu-id="a0897-127">In this walkthrough you use the Debug artifacts for the package.</span></span> <span data-ttu-id="a0897-128">V případě neladicího balíčku si místo toho v dialogovém okně dávkové sestavení vyhledejte možnosti vydání a podívejte se na výsledné složky verze v následujících krocích.</span><span class="sxs-lookup"><span data-stu-id="a0897-128">For non-debug package, check the Release options in the Batch Build dialog instead, and refer to the resulting Release folders in the steps that follow.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="a0897-129">Vytvoření a aktualizace souboru. nuspec</span><span class="sxs-lookup"><span data-stu-id="a0897-129">Create and update the .nuspec file</span></span>

<span data-ttu-id="a0897-130">Chcete-li vytvořit `.nuspec` počáteční soubor, proveďte následující tři kroky.</span><span class="sxs-lookup"><span data-stu-id="a0897-130">To create the initial `.nuspec` file, do the three steps below.</span></span> <span data-ttu-id="a0897-131">Následující části vás pak provede dalšími potřebnými aktualizacemi.</span><span class="sxs-lookup"><span data-stu-id="a0897-131">The sections that follow then guide you through other necessary updates.</span></span>

1. <span data-ttu-id="a0897-132">Otevřete příkazový řádek a přejděte do složky, která obsahuje `ImageEnhancer.vcxproj` (Toto je podsložka, ve které je soubor řešení).</span><span class="sxs-lookup"><span data-stu-id="a0897-132">Open a command prompt and navigate to the folder containing `ImageEnhancer.vcxproj` (this will be a subfolder below where the solution file is).</span></span>
1. <span data-ttu-id="a0897-133">Spusťte příkaz NuGet `spec` , který se `ImageEnhancer.nuspec` má vygenerovat (název souboru se povede `.vcxproj` z názvu souboru):</span><span class="sxs-lookup"><span data-stu-id="a0897-133">Run the NuGet `spec` command to generate `ImageEnhancer.nuspec` (the name of the file is taken from the name of the `.vcxproj` file):</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="a0897-134">Otevřete `ImageEnhancer.nuspec` v editoru a aktualizujte ho, aby odpovídal následujícímu, a nahraďte YOUR_NAME příslušnou hodnotou.</span><span class="sxs-lookup"><span data-stu-id="a0897-134">Open `ImageEnhancer.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="a0897-135">Hodnota konkrétně musí být jedinečná napříč NuGet.org (podívejte se na zásady vytváření názvů popsané v tématu [Vytvoření balíčku).](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) `<id>`</span><span class="sxs-lookup"><span data-stu-id="a0897-135">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="a0897-136">Všimněte si také, že je nutné také aktualizovat značky Autor a popis, jinak se zobrazí chyba v průběhu balení.</span><span class="sxs-lookup"><span data-stu-id="a0897-136">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>ImageEnhancer.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>ImageEnhancer</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome Image Enhancer</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>image enhancer imageenhancer</tags>
        </metadata>
    </package>
    ```

> [!Note]
> <span data-ttu-id="a0897-137">Pro balíčky sestavené pro veřejnou spotřebu věnujte zvláštní pozornost `<tags>` prvku, protože tyto značky můžou ostatním uživatelům najít váš balíček a pochopit, co to dělá.</span><span class="sxs-lookup"><span data-stu-id="a0897-137">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

### <a name="adding-windows-metadata-to-the-package"></a><span data-ttu-id="a0897-138">Přidávají se metadata Windows do balíčku.</span><span class="sxs-lookup"><span data-stu-id="a0897-138">Adding Windows metadata to the package</span></span>

<span data-ttu-id="a0897-139">Komponenta prostředí Windows Runtime vyžaduje metadata, která popisují všechny veřejně dostupné typy, což umožňuje ostatním aplikacím a knihovnám využívat součást.</span><span class="sxs-lookup"><span data-stu-id="a0897-139">A Windows Runtime Component requires metadata that describes all of its publicly available types, which makes it possible for other apps and libraries to consume the component.</span></span> <span data-ttu-id="a0897-140">Tato metadata jsou obsažena v souboru WinMD, který je vytvořen při kompilování projektu a musí být součástí balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="a0897-140">This metadata is contained in a .winmd file, which is created when you compile the project and must be included in your NuGet package.</span></span> <span data-ttu-id="a0897-141">Soubor XML s daty technologie IntelliSense je také sestaven současně a měl by být zahrnut také.</span><span class="sxs-lookup"><span data-stu-id="a0897-141">An XML file with IntelliSense data is also built at the same time, and should be included as well.</span></span>

<span data-ttu-id="a0897-142">`<files>` Přidejte`.nuspec` do souboru následující uzel:</span><span class="sxs-lookup"><span data-stu-id="a0897-142">Add the following `<files>` node to the `.nuspec` file:</span></span>

```xml
<package>
    <metadata>
        ...
    </metadata>

    <files>
        <!-- WinMd and IntelliSense files -->
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.winmd" target="lib\uap10.0"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.xml" target="lib\uap10.0"/>
    </files>
</package>
```

### <a name="adding-xaml-content"></a><span data-ttu-id="a0897-143">Přidání obsahu XAML</span><span class="sxs-lookup"><span data-stu-id="a0897-143">Adding XAML content</span></span>

<span data-ttu-id="a0897-144">Chcete-li zahrnout ovládací prvek XAML do komponenty, je nutné přidat soubor XAML, který má výchozí šablonu pro ovládací prvek (jak je vygenerována šablonou projektu).</span><span class="sxs-lookup"><span data-stu-id="a0897-144">To include a XAML control with your component, you need to add the XAML file that has the default template for the control (as generated by the project template).</span></span> <span data-ttu-id="a0897-145">To se `<files>` taky doplní v části:</span><span class="sxs-lookup"><span data-stu-id="a0897-145">This also goes in the `<files>` section:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- XAML controls -->
        <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    </files>
</package>
```

### <a name="adding-the-native-implementation-libraries"></a><span data-ttu-id="a0897-146">Přidání nativních implementačních knihoven</span><span class="sxs-lookup"><span data-stu-id="a0897-146">Adding the native implementation libraries</span></span>

<span data-ttu-id="a0897-147">V rámci vaší komponenty je základní logika typu ImageEnhancer v nativním kódu, který je obsažen v různých `ImageEnhancer.dll` sestaveních, která jsou generována pro každý cílový modul runtime (ARM, x86 a x64).</span><span class="sxs-lookup"><span data-stu-id="a0897-147">Within your component, the core logic of the ImageEnhancer type is in native code, which is contained in the various `ImageEnhancer.dll` assemblies that are generated for each target runtime (ARM, x86, and x64).</span></span> <span data-ttu-id="a0897-148">Pokud je chcete zahrnout do balíčku, odkázat je v `<files>` části spolu s jejich přidruženými zdrojovými soubory. pri:</span><span class="sxs-lookup"><span data-stu-id="a0897-148">To include these in the package, reference them in the `<files>` section along with their associated .pri resource files:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- DLLs and resources -->
        <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm\native"/>
        <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm\native"/>

        <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm64\native"/>
        <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm64\native"/>

        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>

        <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    </files>
</package>
```

### <a name="adding-targets"></a><span data-ttu-id="a0897-149">Přidávání cílů</span><span class="sxs-lookup"><span data-stu-id="a0897-149">Adding .targets</span></span>

<span data-ttu-id="a0897-150">V dalších C++ a v projektech JavaScriptu, které mohou spotřebovat váš balíček NuGet, potřebuje soubor. targets k identifikaci potřebných sestavení a souborů winmd.</span><span class="sxs-lookup"><span data-stu-id="a0897-150">Next, C++ and JavaScript projects that might consume your NuGet package need a .targets file to identify the necessary assembly and winmd files.</span></span> <span data-ttu-id="a0897-151">(C# a Visual Basic projekty automaticky.) Vytvořte tento soubor zkopírováním textu níže do `ImageEnhancer.targets` a uložte ho do stejné složky, ve které je `.nuspec` soubor.</span><span class="sxs-lookup"><span data-stu-id="a0897-151">(C# and Visual Basic projects do this automatically.) Create this file by copying the text below into `ImageEnhancer.targets` and save it in the same folder as the `.nuspec` file.</span></span> <span data-ttu-id="a0897-152">_Poznámka:_ Tento `.targets` soubor musí mít stejný název jako ID balíčku (např `<Id>` . element v `.nupspec` souboru):</span><span class="sxs-lookup"><span data-stu-id="a0897-152">_Note_: This `.targets` file needs to be the same name as the package ID (e.g. the `<Id>` element in the `.nupspec` file):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <PropertyGroup>
        <ImageEnhancer-Platform Condition="'$(Platform)' == 'Win32'">x86</ImageEnhancer-Platform>
        <ImageEnhancer-Platform Condition="'$(Platform)' != 'Win32'">$(Platform)</ImageEnhancer-Platform>
    </PropertyGroup>
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Reference Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0\ImageEnhancer.winmd">
            <Implementation>ImageEnhancer.dll</Implementation>
        </Reference>
    <ReferenceCopyLocalPaths Include="$(MSBuildThisFileDirectory)..\..\runtimes\win10-$(ImageEnhancer-Platform)\native\ImageEnhancer.dll" />
    </ItemGroup>
</Project>
```

<span data-ttu-id="a0897-153">Pak se podívejte `ImageEnhancer.targets` na téma `.nuspec` v souboru:</span><span class="sxs-lookup"><span data-stu-id="a0897-153">Then refer to `ImageEnhancer.targets` in your `.nuspec` file:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- .targets -->
        <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

### <a name="final-nuspec"></a><span data-ttu-id="a0897-154">Finální. nuspec</span><span class="sxs-lookup"><span data-stu-id="a0897-154">Final .nuspec</span></span>

<span data-ttu-id="a0897-155">Konečný `.nuspec` soubor by teď měl vypadat nějak takto, kde znovu YOUR_NAME by mělo být nahrazeno příslušnou hodnotou:</span><span class="sxs-lookup"><span data-stu-id="a0897-155">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>ImageEnhancer.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>ImageEnhancer</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome Image Enhancer</description>
    <releaseNotes>First Release</releaseNotes>
    <copyright>Copyright 2016</copyright>
    <tags>image enhancer imageenhancer</tags>
    </metadata>
    <files>
    <!-- WinMd and IntelliSense -->
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.winmd" target="lib\uap10.0"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.xml" target="lib\uap10.0"/>

    <!-- XAML controls -->
    <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    <!-- DLLs and resources -->
    <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm\native"/>
    <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm\native"/>
    <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm64\native"/>
    <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm64\native"/>     
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    <!-- .targets -->
    <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

## <a name="package-the-component"></a><span data-ttu-id="a0897-156">Zabalení komponenty</span><span class="sxs-lookup"><span data-stu-id="a0897-156">Package the component</span></span>

<span data-ttu-id="a0897-157">Po dokončení `.nuspec` odkazů na všechny soubory, které potřebujete zahrnout do balíčku, jste připraveni `pack` spustit příkaz:</span><span class="sxs-lookup"><span data-stu-id="a0897-157">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack ImageEnhancer.nuspec
```

<span data-ttu-id="a0897-158">Tím vygenerujete `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="a0897-158">This generates `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="a0897-159">Tento soubor otevřete v nástroji jako [Průzkumník balíčků NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) a rozbalíte všechny uzly. zobrazí se následující obsah:</span><span class="sxs-lookup"><span data-stu-id="a0897-159">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![Průzkumník balíčků NuGet zobrazující balíček ImageEnhancer](media/UWP-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="a0897-161">`.nupkg` Soubor je pouze soubor zip s jinou příponou.</span><span class="sxs-lookup"><span data-stu-id="a0897-161">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="a0897-162">Můžete také prošetřit obsah balíčku, potom změnou `.nupkg` na `.zip`, ale nezapomeňte obnovit rozšíření před nahráním balíčku do NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="a0897-162">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="a0897-163">Pokud chcete balíček zpřístupnit ostatním vývojářům, postupujte podle pokynů v tématu [publikování balíčku](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="a0897-163">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="a0897-164">Související témata</span><span class="sxs-lookup"><span data-stu-id="a0897-164">Related topics</span></span>

- [<span data-ttu-id="a0897-165">Odkaz. nuspec</span><span class="sxs-lookup"><span data-stu-id="a0897-165">.nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="a0897-166">Balíčky symbolů</span><span class="sxs-lookup"><span data-stu-id="a0897-166">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="a0897-167">Správa verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="a0897-167">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="a0897-168">Podpora více verzí .NET Framework</span><span class="sxs-lookup"><span data-stu-id="a0897-168">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="a0897-169">Zahrnutí vlastností MSBuild a cílů do balíčku</span><span class="sxs-lookup"><span data-stu-id="a0897-169">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="a0897-170">Vytvoření lokalizovaných balíčků</span><span class="sxs-lookup"><span data-stu-id="a0897-170">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
