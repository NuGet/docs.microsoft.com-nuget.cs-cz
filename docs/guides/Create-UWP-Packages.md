---
title: Vytváření balíčků NuGet pro Universal Windows Platform
description: Začátku do konce postup vytváření balíčků NuGet pro univerzální platformu Windows pomocí komponenty Windows Runtime.
author: karann-msft
ms.author: karann
ms.date: 03/21/2017
ms.topic: tutorial
ms.openlocfilehash: 344c8d764180d0f33c1bce77b721e3657297e74e
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842123"
---
# <a name="create-uwp-packages"></a><span data-ttu-id="3eac6-103">Vytvoření balíčků UPW</span><span class="sxs-lookup"><span data-stu-id="3eac6-103">Create UWP packages</span></span>

<span data-ttu-id="3eac6-104">[Univerzální platformu Windows (UPW)](https://developer.microsoft.com/windows) poskytuje společnou platformu aplikace pro každé zařízení, na kterém běží Windows 10.</span><span class="sxs-lookup"><span data-stu-id="3eac6-104">The [Universal Windows Platform (UWP)](https://developer.microsoft.com/windows) provides a common app platform for every device that runs Windows 10.</span></span> <span data-ttu-id="3eac6-105">V rámci tohoto modelu aplikací pro UWP můžete volat rozhraní API WinRT, která jsou společná pro všechna zařízení i také rozhraní API (včetně Win32 a .NET), které jsou specifické na řadě zařízení, na kterém je aplikace spuštěna.</span><span class="sxs-lookup"><span data-stu-id="3eac6-105">Within this model, UWP apps can call both the WinRT APIs that are common to all devices, and also APIs (including Win32 and .NET) that are specific to the device family on which the app is running.</span></span>

<span data-ttu-id="3eac6-106">V tomto návodu vytvoříte balíček NuGet s nativní UWP součásti (včetně ovládacího prvku XAML), který lze použít v spravovaný a nativní projekty.</span><span class="sxs-lookup"><span data-stu-id="3eac6-106">In this walkthrough you create a NuGet package with a native UWP component (including a XAML control) that can be used in both Managed and Native projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3eac6-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="3eac6-107">Prerequisites</span></span>

1. <span data-ttu-id="3eac6-108">Visual Studio 2017 nebo Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="3eac6-108">Visual Studio 2017 or Visual Studio 2015.</span></span> <span data-ttu-id="3eac6-109">Instalace edice Community 2017 zdarma z [visualstudio.com](https://www.visualstudio.com/); můžete použít také edice Professional a Enterprise.</span><span class="sxs-lookup"><span data-stu-id="3eac6-109">Install the 2017 Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well.</span></span>

1. <span data-ttu-id="3eac6-110">Rozhraní příkazového řádku NuGet.</span><span class="sxs-lookup"><span data-stu-id="3eac6-110">NuGet CLI.</span></span> <span data-ttu-id="3eac6-111">Stáhněte si nejnovější verzi `nuget.exe` z [nuget.org/downloads](https://nuget.org/downloads), ukládání do umístění podle vašeho výběru (soubor ke stažení je `.exe` přímo).</span><span class="sxs-lookup"><span data-stu-id="3eac6-111">Download the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice (the download is the `.exe` directly).</span></span> <span data-ttu-id="3eac6-112">Pak přidejte toto umístění do proměnné prostředí PATH, pokud ještě není.</span><span class="sxs-lookup"><span data-stu-id="3eac6-112">Then add that location to your PATH environment variable if it isn't already.</span></span>

## <a name="create-a-uwp-windows-runtime-component"></a><span data-ttu-id="3eac6-113">Vytvoření součásti UPW Windows Runtime</span><span class="sxs-lookup"><span data-stu-id="3eac6-113">Create a UWP Windows Runtime component</span></span>

1. <span data-ttu-id="3eac6-114">V sadě Visual Studio, zvolte **soubor > Nový > projekt**, rozbalte **Visual C++ > Windows > univerzální** uzlu, vyberte **součást prostředí Windows Runtime (Universal Windows)** šablony, změňte název na ImageEnhancer a klikněte na tlačítko OK.</span><span class="sxs-lookup"><span data-stu-id="3eac6-114">In Visual Studio, choose **File > New > Project**, expand the **Visual C++ > Windows > Universal** node, select the **Windows Runtime Component (Universal Windows)** template, change the name to ImageEnhancer, and click OK.</span></span> <span data-ttu-id="3eac6-115">Přijměte výchozí hodnoty pro cílovou verzi a minimální verzi po zobrazení výzvy.</span><span class="sxs-lookup"><span data-stu-id="3eac6-115">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

    ![Vytvoření nového projektu UPW součást prostředí Windows Runtime](media/UWP-NewProject.png)

1. <span data-ttu-id="3eac6-117">Klikněte pravým tlačítkem myši na projekt v Průzkumníku řešení, vyberte **Přidat > Nová položka**, klikněte na tlačítko **Visual C++ > XAML** uzlu, vyberte **prvku bez vizuálního vzhledu**, změňte název na AwesomeImageControl.cpp a klikněte na tlačítko **přidat**:</span><span class="sxs-lookup"><span data-stu-id="3eac6-117">Right click the project in Solution Explorer, select **Add > New Item**, click the **Visual C++ > XAML** node, select **Templated Control**, change the name to AwesomeImageControl.cpp, and click **Add**:</span></span>

    ![Přidání nové položky bez vizuálního vzhledu ovládacího prvku XAML do projektu](media/UWP-NewXAMLControl.png)

1. <span data-ttu-id="3eac6-119">Klikněte pravým tlačítkem na projekt v Průzkumníku řešení a vyberte **vlastnosti.**</span><span class="sxs-lookup"><span data-stu-id="3eac6-119">Right-click the project in Solution Explorer and select **Properties.**</span></span> <span data-ttu-id="3eac6-120">Na stránce vlastností rozbalte **vlastnosti konfigurace > C/C++** a klikněte na tlačítko **výstupní soubory**.</span><span class="sxs-lookup"><span data-stu-id="3eac6-120">In the Properties page, expand **Configuration Properties > C/C++** and click **Output Files**.</span></span> <span data-ttu-id="3eac6-121">V podokně na pravé straně, změňte hodnotu **Generovat soubory dokumentace XML** na Ano:</span><span class="sxs-lookup"><span data-stu-id="3eac6-121">In the pane on the right, change the value for **Generate XML Documentation Files** to Yes:</span></span>

    ![Nastavení Generovat soubory dokumentace XML na hodnotu Ano](media/UWP-GenerateXMLDocFiles.png)

1. <span data-ttu-id="3eac6-123">Klikněte pravým tlačítkem myši *řešení* teď vyberte **dávkové sestavení**, zkontrolujte tři ladění pole v dialogovém okně, jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="3eac6-123">Right click the *solution* now, select **Batch Build**, check the three Debug boxes in the dialog as shown below.</span></span> <span data-ttu-id="3eac6-124">Tím je zajištěno, že když použijete sestavení, vygenerujete kompletní sadu artefaktů pro každé cílové systémy, které podporuje Windows.</span><span class="sxs-lookup"><span data-stu-id="3eac6-124">This makes sure that when you do a build, you generate a full set of artifacts for each of the target systems that Windows supports.</span></span>

    ![Dávkové sestavení](media/UWP-BatchBuild.png)

1. <span data-ttu-id="3eac6-126">V dávce sestavit dialogové okno a klikněte na tlačítko **sestavení** ověření projektu a vytvoření výstupních souborů, které potřebujete pro balíček NuGet.</span><span class="sxs-lookup"><span data-stu-id="3eac6-126">In the Batch Build dialog, and click **Build** to verify the project and create the output files that you need for the NuGet package.</span></span>

> [!Note]
> <span data-ttu-id="3eac6-127">V tomto názorném postupu použijete artefakty ladění pro balíček.</span><span class="sxs-lookup"><span data-stu-id="3eac6-127">In this walkthrough you use the Debug artifacts for the package.</span></span> <span data-ttu-id="3eac6-128">Bez ladění balíčku zkontrolujte verzi možnosti v dialogovém okně dávkové sestavení místo toho a odkazovat na výsledný verzi složky v následujících kroků.</span><span class="sxs-lookup"><span data-stu-id="3eac6-128">For non-debug package, check the Release options in the Batch Build dialog instead, and refer to the resulting Release folders in the steps that follow.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="3eac6-129">Vytvoření a aktualizaci souboru .nuspec souboru</span><span class="sxs-lookup"><span data-stu-id="3eac6-129">Create and update the .nuspec file</span></span>

<span data-ttu-id="3eac6-130">Chcete-li vytvořit počáteční `.nuspec` soubor, proveďte následující tři kroky.</span><span class="sxs-lookup"><span data-stu-id="3eac6-130">To create the initial `.nuspec` file, do the three steps below.</span></span> <span data-ttu-id="3eac6-131">Následující části pak vás provede další potřebné aktualizace.</span><span class="sxs-lookup"><span data-stu-id="3eac6-131">The sections that follow then guide you through other necessary updates.</span></span>

1. <span data-ttu-id="3eac6-132">Otevřete příkazový řádek a přejděte do složky obsahující `ImageEnhancer.vcxproj` (bude to podsložka níže kde je soubor řešení).</span><span class="sxs-lookup"><span data-stu-id="3eac6-132">Open a command prompt and navigate to the folder containing `ImageEnhancer.vcxproj` (this will be a subfolder below where the solution file is).</span></span>
1. <span data-ttu-id="3eac6-133">Spuštění balíčku NuGet `spec` příkazu vygenerujte `ImageEnhancer.nuspec` (název souboru je převzat z názvu `.vcxproj` souboru):</span><span class="sxs-lookup"><span data-stu-id="3eac6-133">Run the NuGet `spec` command to generate `ImageEnhancer.nuspec` (the name of the file is taken from the name of the `.vcxproj` file):</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="3eac6-134">Otevřít `ImageEnhancer.nuspec` v editoru a aktualizujte ji, aby se shodoval s následujícím, nahradíte vaše_jméno odpovídající hodnotu.</span><span class="sxs-lookup"><span data-stu-id="3eac6-134">Open `ImageEnhancer.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="3eac6-135">`<id>` , Konkrétně musí být hodnota jedinečná napříč nuget.org (naleznete v tématu Zásady vytváření názvů je popsáno v [vytvoření balíčku](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="3eac6-135">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="3eac6-136">Všimněte si také, že budete muset taky aktualizovat Autor a popis značky nebo dojde k chybě během kroku balení.</span><span class="sxs-lookup"><span data-stu-id="3eac6-136">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
> <span data-ttu-id="3eac6-137">Pro balíčky sestavené ke zveřejnění, věnujte zvláštní pozornost `<tags>` element, protože tyto značky pomoci ostatním najít váš balíček a pochopit jeho význam.</span><span class="sxs-lookup"><span data-stu-id="3eac6-137">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

### <a name="adding-windows-metadata-to-the-package"></a><span data-ttu-id="3eac6-138">Přidání metadat Windows do balíčku</span><span class="sxs-lookup"><span data-stu-id="3eac6-138">Adding Windows metadata to the package</span></span>

<span data-ttu-id="3eac6-139">Komponenta Windows Runtime vyžaduje metadata, která popisuje všechny veřejně dostupné typy, které umožňují další aplikace a knihovny, které chcete využívat komponentu.</span><span class="sxs-lookup"><span data-stu-id="3eac6-139">A Windows Runtime Component requires metadata that describes all of its publicly available types, which makes it possible for other apps and libraries to consume the component.</span></span> <span data-ttu-id="3eac6-140">Tato metadata je obsažen v souboru winmd, který je vytvořen při kompilaci projektu a musí být součástí balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="3eac6-140">This metadata is contained in a .winmd file, which is created when you compile the project and must be included in your NuGet package.</span></span> <span data-ttu-id="3eac6-141">Soubor XML s daty technologie IntelliSense je také integrované ve stejnou dobu a by měly být zahrnuty i.</span><span class="sxs-lookup"><span data-stu-id="3eac6-141">An XML file with IntelliSense data is also built at the same time, and should be included as well.</span></span>

<span data-ttu-id="3eac6-142">Přidejte následující `<files>` uzlu `.nuspec` souboru:</span><span class="sxs-lookup"><span data-stu-id="3eac6-142">Add the following `<files>` node to the `.nuspec` file:</span></span>

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

### <a name="adding-xaml-content"></a><span data-ttu-id="3eac6-143">Přidání obsahu XAML</span><span class="sxs-lookup"><span data-stu-id="3eac6-143">Adding XAML content</span></span>

<span data-ttu-id="3eac6-144">Zahrnout ovládacího prvku XAML pomocí vaší komponentě, budete muset přidat soubor XAML, který má výchozí šablony pro ovládací prvek (vygenerovaný pomocí šablony projektu).</span><span class="sxs-lookup"><span data-stu-id="3eac6-144">To include a XAML control with your component, you need to add the XAML file that has the default template for the control (as generated by the project template).</span></span> <span data-ttu-id="3eac6-145">To také ukládá `<files>` části:</span><span class="sxs-lookup"><span data-stu-id="3eac6-145">This also goes in the `<files>` section:</span></span>

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

### <a name="adding-the-native-implementation-libraries"></a><span data-ttu-id="3eac6-146">Přidat nativní implementace knihovny</span><span class="sxs-lookup"><span data-stu-id="3eac6-146">Adding the native implementation libraries</span></span>

<span data-ttu-id="3eac6-147">V rámci vaší komponenty základní logiky ImageEnhancer typ je v nativním kódu, který je obsažen v různých `ImageEnhancer.dll` sestavení, které jsou generovány pro každý cílový modul runtime (x 86 a x64 ARM).</span><span class="sxs-lookup"><span data-stu-id="3eac6-147">Within your component, the core logic of the ImageEnhancer type is in native code, which is contained in the various `ImageEnhancer.dll` assemblies that are generated for each target runtime (ARM, x86, and x64).</span></span> <span data-ttu-id="3eac6-148">Pokud chcete zahrnout do balíčku, na ně odkazovat v `<files>` části spolu s jejich soubory prostředků přidružené .pri:</span><span class="sxs-lookup"><span data-stu-id="3eac6-148">To include these in the package, reference them in the `<files>` section along with their associated .pri resource files:</span></span>

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

### <a name="adding-targets"></a><span data-ttu-id="3eac6-149">Přidání .targets</span><span class="sxs-lookup"><span data-stu-id="3eac6-149">Adding .targets</span></span>

<span data-ttu-id="3eac6-150">Projekty C++ a JavaScript, které může využívat svůj balíček NuGet dále, třeba souboru .targets pro identifikaci potřebné soubory sestavení a soubor winmd.</span><span class="sxs-lookup"><span data-stu-id="3eac6-150">Next, C++ and JavaScript projects that might consume your NuGet package need a .targets file to identify the necessary assembly and winmd files.</span></span> <span data-ttu-id="3eac6-151">(Projekty jazyka C# a Visual Basic udělat automaticky.) Tento soubor vytvořit zkopírováním níže uvedený text do `ImageEnhancer.targets` a uložte ho do stejné složky jako `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="3eac6-151">(C# and Visual Basic projects do this automatically.) Create this file by copying the text below into `ImageEnhancer.targets` and save it in the same folder as the `.nuspec` file.</span></span> <span data-ttu-id="3eac6-152">_Poznámka:_ To `.targets` soubor musí být stejný název jako ID balíčku (například `<Id>` element v `.nupspec` souboru):</span><span class="sxs-lookup"><span data-stu-id="3eac6-152">_Note_: This `.targets` file needs to be the same name as the package ID (e.g. the `<Id>` element in the `.nupspec` file):</span></span>

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

<span data-ttu-id="3eac6-153">Potom použijte `ImageEnhancer.targets` ve vašich `.nuspec` souboru:</span><span class="sxs-lookup"><span data-stu-id="3eac6-153">Then refer to `ImageEnhancer.targets` in your `.nuspec` file:</span></span>

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

### <a name="final-nuspec"></a><span data-ttu-id="3eac6-154">Poslední souboru .nuspec</span><span class="sxs-lookup"><span data-stu-id="3eac6-154">Final .nuspec</span></span>

<span data-ttu-id="3eac6-155">Výsledná `.nuspec` soubor by teď měl vypadat jako následující, kde znovu vaše_jméno by měla být nahrazena odpovídající hodnotu:</span><span class="sxs-lookup"><span data-stu-id="3eac6-155">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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

## <a name="package-the-component"></a><span data-ttu-id="3eac6-156">Balíček komponenty</span><span class="sxs-lookup"><span data-stu-id="3eac6-156">Package the component</span></span>

<span data-ttu-id="3eac6-157">S dokončenou `.nuspec` odkazující na všechny soubory, které je potřeba zahrnout do balíčku, jste připraveni spustit `pack` příkaz:</span><span class="sxs-lookup"><span data-stu-id="3eac6-157">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack ImageEnhancer.nuspec
```

<span data-ttu-id="3eac6-158">Tím se vygeneruje `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="3eac6-158">This generates `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="3eac6-159">Tento soubor otevřete v nástroje, jako je [NuGet – Průzkumník balíčků](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) a rozšiřuje všechny uzly, viz následující obsah:</span><span class="sxs-lookup"><span data-stu-id="3eac6-159">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![Zobrazuje ImageEnhancer balíčku NuGet – Průzkumník balíčků](media/UWP-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="3eac6-161">A `.nupkg` soubor je jenom soubor ZIP s jinou příponou.</span><span class="sxs-lookup"><span data-stu-id="3eac6-161">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="3eac6-162">Můžete také prozkoumat obsah balíčku, potom změnou `.nupkg` k `.zip`, ale nezapomeňte k obnovení rozšíření před nahráním balíčků na nuget.org.</span><span class="sxs-lookup"><span data-stu-id="3eac6-162">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="3eac6-163">Aby váš balíček k dispozici s ostatními vývojáři, postupujte podle pokynů [publikování balíčku](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="3eac6-163">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="3eac6-164">Související témata</span><span class="sxs-lookup"><span data-stu-id="3eac6-164">Related topics</span></span>

- [<span data-ttu-id="3eac6-165">odkaz na souboru .nuspec</span><span class="sxs-lookup"><span data-stu-id="3eac6-165">.nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="3eac6-166">Balíčky symbolů</span><span class="sxs-lookup"><span data-stu-id="3eac6-166">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="3eac6-167">Správa verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="3eac6-167">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="3eac6-168">Podpora více verzí rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="3eac6-168">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="3eac6-169">Zahrnout do balíčku cíle a vlastnosti nástroje MSBuild</span><span class="sxs-lookup"><span data-stu-id="3eac6-169">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="3eac6-170">Vytvoření lokalizovaných balíčků</span><span class="sxs-lookup"><span data-stu-id="3eac6-170">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
