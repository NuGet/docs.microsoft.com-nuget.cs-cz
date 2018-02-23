---
title: "Vytvoření balíčků NuGet pro univerzální platformu Windows | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/21/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Začátku do konce návod, jak vytvořit balíčky NuGet používání komponent prostředí Windows Runtime pro univerzální platformu Windows."
keywords: "Vytvoření balíčku, balíčky pro UPW, součásti systému Windows Runtime"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6787704d41364a165270d56e8980f24d311b07b3
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/20/2018
---
# <a name="create-uwp-packages"></a><span data-ttu-id="8bfed-104">Vytvořit balíčky UWP</span><span class="sxs-lookup"><span data-stu-id="8bfed-104">Create UWP packages</span></span>

<span data-ttu-id="8bfed-105">[Univerzální platformu Windows (UWP)](https://developer.microsoft.com/windows) poskytuje společné platformě aplikace pro každé zařízení se systémem Windows 10.</span><span class="sxs-lookup"><span data-stu-id="8bfed-105">The [Universal Windows Platform (UWP)](https://developer.microsoft.com/windows) provides a common app platform for every device that runs Windows 10.</span></span> <span data-ttu-id="8bfed-106">V rámci tohoto modelu aplikace UWP můžete volat rozhraní API WinRT, které jsou společné pro všechna zařízení i taky rozhraní API (včetně Win32 a rozhraní .NET), které jsou specifické pro dané řadě zařízení, na kterém aplikace běží.</span><span class="sxs-lookup"><span data-stu-id="8bfed-106">Within this model, UWP apps can call both the WinRT APIs that are common to all devices, and also APIs (including Win32 and .NET) that are specific to the device family on which the app is running.</span></span>

<span data-ttu-id="8bfed-107">V tomto návodu vytvoříte balíček NuGet s nativní UWP komponentou (včetně ovládacího prvku XAML) mohou být používány spravované a nativní projekty.</span><span class="sxs-lookup"><span data-stu-id="8bfed-107">In this walkthrough you create a NuGet package with a native UWP component (including a XAML control) that can be used in both Managed and Native projects.</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="8bfed-108">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="8bfed-108">Pre-requisites</span></span>

1. <span data-ttu-id="8bfed-109">Visual Studio 2017 nebo Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="8bfed-109">Visual Studio 2017 or Visual Studio 2015.</span></span> <span data-ttu-id="8bfed-110">Instalaci edice Community 2017 zdarma z [visualstudio.com](https://www.visualstudio.com/); můžete použít také edice Professional a Enterprise.</span><span class="sxs-lookup"><span data-stu-id="8bfed-110">Install the 2017 Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well.</span></span>

1. <span data-ttu-id="8bfed-111">Rozhraní příkazového řádku NuGet.</span><span class="sxs-lookup"><span data-stu-id="8bfed-111">NuGet CLI.</span></span> <span data-ttu-id="8bfed-112">Stáhněte si nejnovější verzi `nuget.exe` z [nuget.org/downloads](https://nuget.org/downloads), ukládání do umístění podle vaší volby (ke stažení je `.exe` přímo).</span><span class="sxs-lookup"><span data-stu-id="8bfed-112">Download the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice (the download is the `.exe` directly).</span></span> <span data-ttu-id="8bfed-113">Pak přidejte tohoto umístění do vaší proměnné prostředí PATH, pokud již není.</span><span class="sxs-lookup"><span data-stu-id="8bfed-113">Then add that location to your PATH environment variable if it isn't already.</span></span>

## <a name="create-a-uwp-windows-runtime-component"></a><span data-ttu-id="8bfed-114">Vytvoření komponenty prostředí Windows Runtime UWP</span><span class="sxs-lookup"><span data-stu-id="8bfed-114">Create a UWP Windows Runtime component</span></span>

1. <span data-ttu-id="8bfed-115">V sadě Visual Studio, vyberte **soubor > Nový > projekt**, rozbalte **Visual C++ > Windows > Universal** uzlu, vyberte **komponenty prostředí Windows Runtime (Universal Windows)**šablony, změňte název na ImageEnhancer a klikněte na tlačítko OK.</span><span class="sxs-lookup"><span data-stu-id="8bfed-115">In Visual Studio, choose **File > New > Project**, expand the **Visual C++ > Windows > Universal** node, select the **Windows Runtime Component (Universal Windows)** template, change the name to ImageEnhancer, and click OK.</span></span> <span data-ttu-id="8bfed-116">Přijměte výchozí hodnoty pro cílovou verzi a minimální verzi po zobrazení výzvy.</span><span class="sxs-lookup"><span data-stu-id="8bfed-116">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

    ![Vytvoření nového projektu UPW komponenty prostředí Windows Runtime](media/UWP-NewProject.png)

1. <span data-ttu-id="8bfed-118">Klikněte pravým tlačítkem na projekt v Průzkumníku řešení, vyberte **Přidat > Nová položka**, klikněte na tlačítko **Visual C++ > XAML** uzlu, vyberte **Šablonované řízení**, změňte název souboru na AwesomeImageControl.cpp a klikněte na tlačítko **přidat**:</span><span class="sxs-lookup"><span data-stu-id="8bfed-118">Right click the project in Solution Explorer, select **Add > New Item**, click the **Visual C++ > XAML** node, select **Templated Control**, change the name to AwesomeImageControl.cpp, and click **Add**:</span></span>

    ![Přidání nové položky podle šablony řízení XAML do projektu](media/UWP-NewXAMLControl.png)

1. <span data-ttu-id="8bfed-120">Klikněte pravým tlačítkem na projekt v Průzkumníku řešení a vyberte **vlastnosti.**</span><span class="sxs-lookup"><span data-stu-id="8bfed-120">Right-click the project in Solution Explorer and select **Properties.**</span></span> <span data-ttu-id="8bfed-121">Na stránce vlastností rozbalte **vlastnosti konfigurace > C/C++** a klikněte na tlačítko **výstupní soubory**.</span><span class="sxs-lookup"><span data-stu-id="8bfed-121">In the Properties page, expand **Configuration Properties > C/C++** and click **Output Files**.</span></span> <span data-ttu-id="8bfed-122">V podokně na pravé straně, změňte hodnotu **generování souborů dokumentace XML** Ano:</span><span class="sxs-lookup"><span data-stu-id="8bfed-122">In the pane on the right, change the value for **Generate XML Documentation Files** to Yes:</span></span>

    ![Nastavení generování souborů dokumentace XML na Ano](media/UWP-GenerateXMLDocFiles.png)

1. <span data-ttu-id="8bfed-124">Klikněte pravým tlačítkem *řešení* nyní, vyberte **dávkové sestavení**, zaškrtněte tři políčka ladění v dialogovém okně, jak je uvedeno níže.</span><span class="sxs-lookup"><span data-stu-id="8bfed-124">Right click the *solution* now, select **Batch Build**, check the three Debug boxes in the dialog as shown below.</span></span> <span data-ttu-id="8bfed-125">Tím je zajištěno, že při sestavení, vygenerování kompletní artefaktů pro jednotlivé cílové systémy, které podporuje Windows.</span><span class="sxs-lookup"><span data-stu-id="8bfed-125">This makes sure that when you do a build, you generate a full set of artifacts for each of the target systems that Windows supports.</span></span>

    ![Batch sestavení](media/UWP-BatchBuild.png)

1. <span data-ttu-id="8bfed-127">V dávce sestavení dialogové okno a klikněte na tlačítko **sestavení** ověření projektu a vytvořit výstupní soubory, které potřebujete pro balíček NuGet.</span><span class="sxs-lookup"><span data-stu-id="8bfed-127">In the Batch Build dialog, and click **Build** to verify the project and create the output files that you need for the NuGet package.</span></span>

> [!Note]
> <span data-ttu-id="8bfed-128">V tomto názorném postupu použijete artefakty ladění pro balíček.</span><span class="sxs-lookup"><span data-stu-id="8bfed-128">In this walkthrough you use the Debug artifacts for the package.</span></span> <span data-ttu-id="8bfed-129">Pro balíček bez ladění místo toho zkontrolujte verzi možností v dialogovém okně dávkové sestavení a odkazovat na výsledný složky verze v krocích, které následují.</span><span class="sxs-lookup"><span data-stu-id="8bfed-129">For non-debug package, check the Release options in the Batch Build dialog instead, and refer to the resulting Release folders in the steps that follow.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="8bfed-130">Vytvářet a aktualizovat soubor s příponou .nuspec</span><span class="sxs-lookup"><span data-stu-id="8bfed-130">Create and update the .nuspec file</span></span>

<span data-ttu-id="8bfed-131">Chcete-li vytvořit počáteční `.nuspec` souboru, proveďte následující tři kroky.</span><span class="sxs-lookup"><span data-stu-id="8bfed-131">To create the initial `.nuspec` file, do the three steps below.</span></span> <span data-ttu-id="8bfed-132">V následujících pak provede další potřebné aktualizace.</span><span class="sxs-lookup"><span data-stu-id="8bfed-132">The sections that follow then guide you through other necessary updates.</span></span>

1. <span data-ttu-id="8bfed-133">Otevřete příkazový řádek a přejděte do složky obsahující `ImageEnhancer.vcxproj` (to se stane podsložky níže, kde je soubor řešení).</span><span class="sxs-lookup"><span data-stu-id="8bfed-133">Open a command prompt and navigate to the folder containing `ImageEnhancer.vcxproj` (this will be a subfolder below where the solution file is).</span></span>
1. <span data-ttu-id="8bfed-134">Spustit NuGet `spec` příkazu vygenerujte `ImageEnhancer.nuspec` (název souboru je převzat z názvu `.vcxproj` souborů):</span><span class="sxs-lookup"><span data-stu-id="8bfed-134">Run the NuGet `spec` command to generate `ImageEnhancer.nuspec` (the name of the file is taken from the name of the `.vcxproj` file):</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="8bfed-135">Otevřete `ImageEnhancer.nuspec` v editoru a aktualizovat ji tak, aby odpovídala následující, nahraďte vaše_jméno odpovídající hodnotu.</span><span class="sxs-lookup"><span data-stu-id="8bfed-135">Open `ImageEnhancer.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="8bfed-136">`<id>` Hodnotu, konkrétně musí být jedinečný v rámci nuget.org (viz zásady vytváření názvů, které jsou popsané v [vytváření balíčku](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="8bfed-136">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="8bfed-137">Všimněte si také, zda je nutné také aktualizovat autora a popis značky nebo dojde k chybě během kroku okolních.</span><span class="sxs-lookup"><span data-stu-id="8bfed-137">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
> <span data-ttu-id="8bfed-138">Pro balíčky vytvořené pro veřejné spotřeby, věnujte zvláštní pozornost `<tags>` elementu, jako jsou tyto značky ostatní najít váš balíček a co provádí.</span><span class="sxs-lookup"><span data-stu-id="8bfed-138">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

### <a name="adding-windows-metadata-to-the-package"></a><span data-ttu-id="8bfed-139">Přidávání metadat Windows do balíčku</span><span class="sxs-lookup"><span data-stu-id="8bfed-139">Adding Windows metadata to the package</span></span>

<span data-ttu-id="8bfed-140">Komponent prostředí Windows Runtime vyžaduje metadata, která popisuje všechny veřejně dostupné typy, které umožňuje jiným aplikacím a knihovny využívat komponentu.</span><span class="sxs-lookup"><span data-stu-id="8bfed-140">A Windows Runtime Component requires metadata that describes all of its publicly available types, which makes it possible for other apps and libraries to consume the component.</span></span> <span data-ttu-id="8bfed-141">Tato metadata je obsažený v souboru .winmd, který se vytvoří při kompilaci projektu a musí být součástí vašeho balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="8bfed-141">This metadata is contained in a .winmd file, which is created when you compile the project and must be included in your NuGet package.</span></span> <span data-ttu-id="8bfed-142">Soubor XML s daty IntelliSense vychází ve stejnou dobu a by měly být zahrnuty i.</span><span class="sxs-lookup"><span data-stu-id="8bfed-142">An XML file with IntelliSense data is also built at the same time, and should be included as well.</span></span>

<span data-ttu-id="8bfed-143">Přidejte následující `<files>` uzlu `.nuspec` souboru:</span><span class="sxs-lookup"><span data-stu-id="8bfed-143">Add the following `<files>` node to the `.nuspec` file:</span></span>

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

### <a name="adding-xaml-content"></a><span data-ttu-id="8bfed-144">Přidání součástí obsahu XAML</span><span class="sxs-lookup"><span data-stu-id="8bfed-144">Adding XAML content</span></span>

<span data-ttu-id="8bfed-145">Chcete-li zahrnout prvku XAML pomocí příslušné součásti, přidejte soubor XAML, který má výchozí šablonu pro ovládací prvek (generovaná šablony projektu).</span><span class="sxs-lookup"><span data-stu-id="8bfed-145">To include a XAML control with your component, you need to add the XAML file that has the default template for the control (as generated by the project template).</span></span> <span data-ttu-id="8bfed-146">To také ukládá `<files>` části:</span><span class="sxs-lookup"><span data-stu-id="8bfed-146">This also goes in the `<files>` section:</span></span>

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

### <a name="adding-the-native-implementation-libraries"></a><span data-ttu-id="8bfed-147">Přidání knihovny nativní implementaci</span><span class="sxs-lookup"><span data-stu-id="8bfed-147">Adding the native implementation libraries</span></span>

<span data-ttu-id="8bfed-148">V rámci vaší komponenty základní logika typu ImageEnhancer je v nativním kódu, který se nachází v různých `ImageEnhancer.dll` sestavení, které jsou generovány pro každý cílový modul runtime (x 86 a x64 ARM).</span><span class="sxs-lookup"><span data-stu-id="8bfed-148">Within your component, the core logic of the ImageEnhancer type is in native code, which is contained in the various `ImageEnhancer.dll` assemblies that are generated for each target runtime (ARM, x86, and x64).</span></span> <span data-ttu-id="8bfed-149">Zahrnout tyto v balíčku, odkazujte na ně v `<files>` části spolu s jejich přidružené .pri soubory prostředků:</span><span class="sxs-lookup"><span data-stu-id="8bfed-149">To include these in the package, reference them in the `<files>` section along with their associated .pri resource files:</span></span>

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

        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>

        <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    </files>
</package>
```

### <a name="adding-targets"></a><span data-ttu-id="8bfed-150">Přidání .targets</span><span class="sxs-lookup"><span data-stu-id="8bfed-150">Adding .targets</span></span>

<span data-ttu-id="8bfed-151">Projekty C++ a JavaScript, které může využívat vašeho balíčku NuGet v dalším kroku třeba souboru .targets pro identifikaci potřebné soubory sestavení a souboru winmd.</span><span class="sxs-lookup"><span data-stu-id="8bfed-151">Next, C++ and JavaScript projects that might consume your NuGet package need a .targets file to identify the necessary assembly and winmd files.</span></span> <span data-ttu-id="8bfed-152">(C# a Visual Basic projekty k tomu automaticky.) Tento soubor vytvořte tak, že zkopírujete následující text do `ImageEnhancer.targets` a uložte ho ve stejné složce jako `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="8bfed-152">(C# and Visual Basic projects do this automatically.) Create this file by copying the text below into `ImageEnhancer.targets` and save it in the same folder as the `.nuspec` file.</span></span> <span data-ttu-id="8bfed-153">_Poznámka:_: to `.targets` soubor musí být stejný název jako ID balíčku (například `<Id>` element v `.nupspec` souboru):</span><span class="sxs-lookup"><span data-stu-id="8bfed-153">_Note_: This `.targets` file needs to be the same name as the package ID (e.g. the `<Id>` element in the `.nupspec` file):</span></span>

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

<span data-ttu-id="8bfed-154">Potom se podívejte na `ImageEnhancer.targets` ve vaší `.nuspec` souboru:</span><span class="sxs-lookup"><span data-stu-id="8bfed-154">Then refer to `ImageEnhancer.targets` in your `.nuspec` file:</span></span>

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

### <a name="final-nuspec"></a><span data-ttu-id="8bfed-155">Poslední příponou .nuspec.</span><span class="sxs-lookup"><span data-stu-id="8bfed-155">Final .nuspec</span></span>

<span data-ttu-id="8bfed-156">Váš koncový `.nuspec` soubor by měl nyní vypadat jako následující, kde znovu vaše_jméno by měla být nahrazená příslušnou hodnotu:</span><span class="sxs-lookup"><span data-stu-id="8bfed-156">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    <!-- .targets -->
    <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

## <a name="package-the-component"></a><span data-ttu-id="8bfed-157">Balíček součásti</span><span class="sxs-lookup"><span data-stu-id="8bfed-157">Package the component</span></span>

<span data-ttu-id="8bfed-158">S dokončené `.nuspec` odkazující na všechny soubory, které je potřeba zahrnout do balíčku, jste připraveni ke spuštění `pack` příkaz:</span><span class="sxs-lookup"><span data-stu-id="8bfed-158">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack ImageEnhancer.nuspec
```

<span data-ttu-id="8bfed-159">Tím se vygeneruje `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="8bfed-159">This generates `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="8bfed-160">Otevření tohoto souboru v nástroje, jako [Explorer balíček NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) a rozšiřování všechny uzly, můžete zobrazit následující obsah:</span><span class="sxs-lookup"><span data-stu-id="8bfed-160">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![Průzkumník balíček NuGet zobrazující ImageEnhancer balíčku](media/UWP-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="8bfed-162">A `.nupkg` soubor je právě soubor ZIP s jiné rozšíření.</span><span class="sxs-lookup"><span data-stu-id="8bfed-162">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="8bfed-163">Můžete také zkontrolovat obsah balíčku, potom změnou `.nupkg` k `.zip`, ale nezapomeňte obnovit rozšíření před balíčku se nahrávají na nuget.org.</span><span class="sxs-lookup"><span data-stu-id="8bfed-163">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="8bfed-164">Pokud chcete zpřístupnit vašeho balíčku jinými vývojáři, postupujte podle pokynů [publikování balíčku](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="8bfed-164">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="8bfed-165">Související témata</span><span class="sxs-lookup"><span data-stu-id="8bfed-165">Related topics</span></span>

- [<span data-ttu-id="8bfed-166">referenční dokumentace příponou .nuspec</span><span class="sxs-lookup"><span data-stu-id="8bfed-166">.nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="8bfed-167">Balíčky symbolů</span><span class="sxs-lookup"><span data-stu-id="8bfed-167">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="8bfed-168">Správa verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="8bfed-168">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="8bfed-169">Podpora více verzí rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="8bfed-169">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="8bfed-170">Zahrnout do balíčku nástroje MSBuild props a cíle</span><span class="sxs-lookup"><span data-stu-id="8bfed-170">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="8bfed-171">Vytvoření lokalizovaných balíčků</span><span class="sxs-lookup"><span data-stu-id="8bfed-171">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
