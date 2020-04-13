---
title: Vytvoření balíčků NuGet pro univerzální platformu Windows
description: Komplexní návod k vytváření balíčků NuGet pomocí součásti prostředí Windows Runtime pro univerzální platformu Windows.
author: karann-msft
ms.author: karann
ms.date: 03/21/2017
ms.topic: tutorial
ms.openlocfilehash: 77aa186291122a8d05018ecacd1329da459badad
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "72380753"
---
# <a name="create-uwp-packages"></a><span data-ttu-id="03560-103">Vytvoření balíčků UPW</span><span class="sxs-lookup"><span data-stu-id="03560-103">Create UWP packages</span></span>

<span data-ttu-id="03560-104">[Univerzální platforma Windows (UPW)](https://developer.microsoft.com/windows) poskytuje společnou platformu aplikací pro každé zařízení se systémem Windows 10.</span><span class="sxs-lookup"><span data-stu-id="03560-104">The [Universal Windows Platform (UWP)](https://developer.microsoft.com/windows) provides a common app platform for every device that runs Windows 10.</span></span> <span data-ttu-id="03560-105">V rámci tohoto modelu mohou aplikace UPW volat rozhraní API WinRT, která jsou společná pro všechna zařízení, a také rozhraní API (včetně Win32 a .NET), která jsou specifická pro rodinu zařízení, na které je aplikace spuštěna.</span><span class="sxs-lookup"><span data-stu-id="03560-105">Within this model, UWP apps can call both the WinRT APIs that are common to all devices, and also APIs (including Win32 and .NET) that are specific to the device family on which the app is running.</span></span>

<span data-ttu-id="03560-106">V tomto návodu vytvoříte balíček NuGet s nativní komponentou UPW (včetně ovládacího prvku XAML), který lze použít v řízených i nativních projektech.</span><span class="sxs-lookup"><span data-stu-id="03560-106">In this walkthrough you create a NuGet package with a native UWP component (including a XAML control) that can be used in both Managed and Native projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="03560-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="03560-107">Prerequisites</span></span>

1. <span data-ttu-id="03560-108">Visual Studio 2017 nebo Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="03560-108">Visual Studio 2017 or Visual Studio 2015.</span></span> <span data-ttu-id="03560-109">Nainstalujte 2017 Community edition zdarma od [visualstudio.com](https://www.visualstudio.com/); můžete také použít edice Professional a Enterprise.</span><span class="sxs-lookup"><span data-stu-id="03560-109">Install the 2017 Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well.</span></span>

1. <span data-ttu-id="03560-110">NuGet CLI.</span><span class="sxs-lookup"><span data-stu-id="03560-110">NuGet CLI.</span></span> <span data-ttu-id="03560-111">Stáhněte si `nuget.exe` nejnovější verzi z [nuget.org/downloads](https://nuget.org/downloads)a uložte ji na `.exe` místo podle vašeho výběru (stahování je přímo).</span><span class="sxs-lookup"><span data-stu-id="03560-111">Download the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice (the download is the `.exe` directly).</span></span> <span data-ttu-id="03560-112">Pak přidejte toto umístění do proměnné prostředí PATH, pokud ještě není.</span><span class="sxs-lookup"><span data-stu-id="03560-112">Then add that location to your PATH environment variable if it isn't already.</span></span>

## <a name="create-a-uwp-windows-runtime-component"></a><span data-ttu-id="03560-113">Vytvoření součásti runtime systému Windows v programu UPW</span><span class="sxs-lookup"><span data-stu-id="03560-113">Create a UWP Windows Runtime component</span></span>

1. <span data-ttu-id="03560-114">V sadě Visual Studio zvolte **Soubor > Nový > Project**, rozbalte uzel Visual **C++ > Windows > Universal,** vyberte šablonu **komponenty Prostředí Windows Runtime (Universal Windows),** změňte název na ImageEnhancer a klepněte na OK.</span><span class="sxs-lookup"><span data-stu-id="03560-114">In Visual Studio, choose **File > New > Project**, expand the **Visual C++ > Windows > Universal** node, select the **Windows Runtime Component (Universal Windows)** template, change the name to ImageEnhancer, and click OK.</span></span> <span data-ttu-id="03560-115">Po zobrazení výzvy přijměte výchozí hodnoty pro cílovou a minimální verzi.</span><span class="sxs-lookup"><span data-stu-id="03560-115">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

    ![Vytvoření nového projektu komponenty runtime systému Windows UWP](media/UWP-NewProject.png)

1. <span data-ttu-id="03560-117">Klepněte pravým tlačítkem myši na projekt v Průzkumníku řešení, vyberte **Přidat > novou položku**, klepněte na uzel **XAML v jazyc >e Visual C++,** vyberte **položku Templated Control**, změňte název na AwesomeImageControl.cpp a klepněte na **přidat**:</span><span class="sxs-lookup"><span data-stu-id="03560-117">Right click the project in Solution Explorer, select **Add > New Item**, click the **Visual C++ > XAML** node, select **Templated Control**, change the name to AwesomeImageControl.cpp, and click **Add**:</span></span>

    ![Přidání nové položky ovládacího prvku šablony XAML do projektu](media/UWP-NewXAMLControl.png)

1. <span data-ttu-id="03560-119">Klikněte pravým tlačítkem myši na projekt v Průzkumníku řešení a vyberte **Vlastnosti.**</span><span class="sxs-lookup"><span data-stu-id="03560-119">Right-click the project in Solution Explorer and select **Properties.**</span></span> <span data-ttu-id="03560-120">Na stránce Vlastnosti **rozbalte položku Vlastnosti konfigurace > C/C++** a klepněte na **příkaz Výstupní soubory**.</span><span class="sxs-lookup"><span data-stu-id="03560-120">In the Properties page, expand **Configuration Properties > C/C++** and click **Output Files**.</span></span> <span data-ttu-id="03560-121">V podokně vpravo změňte hodnotu **pro Generovat soubory dokumentace XML** na Ano:</span><span class="sxs-lookup"><span data-stu-id="03560-121">In the pane on the right, change the value for **Generate XML Documentation Files** to Yes:</span></span>

    ![Nastavení generování souborů dokumentace XML na ano](media/UWP-GenerateXMLDocFiles.png)

1. <span data-ttu-id="03560-123">Klikněte pravým tlačítkem myši na *řešení,* vyberte **Dávkové sestavení**, zaškrtněte tři pole ladění v dialogovém okně, jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="03560-123">Right click the *solution* now, select **Batch Build**, check the three Debug boxes in the dialog as shown below.</span></span> <span data-ttu-id="03560-124">Tím zajistíte, že při vytváření sestavení vygenerujete úplnou sadu artefaktů pro každý z cílových systémů, které systém Windows podporuje.</span><span class="sxs-lookup"><span data-stu-id="03560-124">This makes sure that when you do a build, you generate a full set of artifacts for each of the target systems that Windows supports.</span></span>

    ![Dávkové sestavení](media/UWP-BatchBuild.png)

1. <span data-ttu-id="03560-126">V dialogovém okně Dávkové sestavení a klepněte na tlačítko **Sestavit,** chcete-li ověřit projekt a vytvořit výstupní soubory, které potřebujete pro balíček NuGet.</span><span class="sxs-lookup"><span data-stu-id="03560-126">In the Batch Build dialog, and click **Build** to verify the project and create the output files that you need for the NuGet package.</span></span>

> [!Note]
> <span data-ttu-id="03560-127">V tomto návodu použijete artefakty ladění pro balíček.</span><span class="sxs-lookup"><span data-stu-id="03560-127">In this walkthrough you use the Debug artifacts for the package.</span></span> <span data-ttu-id="03560-128">U balíčku bez ladění zkontrolujte možnosti vydání v dialogovém okně Dávkové sestavení a v následujících krocích se podívejte na výsledné složky release.</span><span class="sxs-lookup"><span data-stu-id="03560-128">For non-debug package, check the Release options in the Batch Build dialog instead, and refer to the resulting Release folders in the steps that follow.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="03560-129">Vytvoření a aktualizace souboru Nuspec</span><span class="sxs-lookup"><span data-stu-id="03560-129">Create and update the .nuspec file</span></span>

<span data-ttu-id="03560-130">Chcete-li `.nuspec` vytvořit počáteční soubor, proveďte následující tři kroky.</span><span class="sxs-lookup"><span data-stu-id="03560-130">To create the initial `.nuspec` file, do the three steps below.</span></span> <span data-ttu-id="03560-131">Následující části vás pak provedou dalšími nezbytnými aktualizacemi.</span><span class="sxs-lookup"><span data-stu-id="03560-131">The sections that follow then guide you through other necessary updates.</span></span>

1. <span data-ttu-id="03560-132">Otevřete příkazový řádek a přejděte do složky obsahující `ImageEnhancer.vcxproj` (bude to podsložka pod místem, kde je soubor řešení).</span><span class="sxs-lookup"><span data-stu-id="03560-132">Open a command prompt and navigate to the folder containing `ImageEnhancer.vcxproj` (this will be a subfolder below where the solution file is).</span></span>
1. <span data-ttu-id="03560-133">Spusťte `spec` příkaz NuGet pro generování `ImageEnhancer.nuspec` (název souboru je `.vcxproj` převzat z názvu souboru):</span><span class="sxs-lookup"><span data-stu-id="03560-133">Run the NuGet `spec` command to generate `ImageEnhancer.nuspec` (the name of the file is taken from the name of the `.vcxproj` file):</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="03560-134">Otevřete `ImageEnhancer.nuspec` v editoru a aktualizujte jej tak, aby odpovídal následujícímu, a nahrazují YOUR_NAME příslušnou hodnotou.</span><span class="sxs-lookup"><span data-stu-id="03560-134">Open `ImageEnhancer.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="03560-135">Hodnota, `<id>` konkrétně musí být jedinečný napříč nuget.org (viz konvence pojmenování popsané v [vytvoření balíčku).](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)</span><span class="sxs-lookup"><span data-stu-id="03560-135">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="03560-136">Všimněte si také, že musíte také aktualizovat značky autora a popisu nebo se během kroku balení zobrazí chyba.</span><span class="sxs-lookup"><span data-stu-id="03560-136">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
> <span data-ttu-id="03560-137">U balíčků vytvořených pro veřejnou `<tags>` spotřebu věnujte tomuto prvku zvláštní pozornost, protože tyto značky pomáhají ostatním najít váš balíček a pochopit, co dělá.</span><span class="sxs-lookup"><span data-stu-id="03560-137">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

### <a name="adding-windows-metadata-to-the-package"></a><span data-ttu-id="03560-138">Přidání metadat systému Windows do balíčku</span><span class="sxs-lookup"><span data-stu-id="03560-138">Adding Windows metadata to the package</span></span>

<span data-ttu-id="03560-139">Součást prostředí Windows Runtime vyžaduje metadata, která popisují všechny jeho veřejně dostupné typy, což umožňuje ostatním aplikacím a knihovnám využívat komponentu.</span><span class="sxs-lookup"><span data-stu-id="03560-139">A Windows Runtime Component requires metadata that describes all of its publicly available types, which makes it possible for other apps and libraries to consume the component.</span></span> <span data-ttu-id="03560-140">Tato metadata jsou obsažena v souboru .winmd, který je vytvořen při kompilaci projektu a musí být zahrnuty do balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="03560-140">This metadata is contained in a .winmd file, which is created when you compile the project and must be included in your NuGet package.</span></span> <span data-ttu-id="03560-141">Soubor XML s daty Technologie IntelliSense je také vytvořen současně a měl by být také zahrnut.</span><span class="sxs-lookup"><span data-stu-id="03560-141">An XML file with IntelliSense data is also built at the same time, and should be included as well.</span></span>

<span data-ttu-id="03560-142">Přidejte `<files>` do souboru `.nuspec` následující uzel:</span><span class="sxs-lookup"><span data-stu-id="03560-142">Add the following `<files>` node to the `.nuspec` file:</span></span>

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

### <a name="adding-xaml-content"></a><span data-ttu-id="03560-143">Přidání obsahu XAML</span><span class="sxs-lookup"><span data-stu-id="03560-143">Adding XAML content</span></span>

<span data-ttu-id="03560-144">Chcete-li zahrnout ovládací prvek XAML s komponentou, je třeba přidat soubor XAML, který má výchozí šablonu pro ovládací prvek (jak je generováno šablonou projektu).</span><span class="sxs-lookup"><span data-stu-id="03560-144">To include a XAML control with your component, you need to add the XAML file that has the default template for the control (as generated by the project template).</span></span> <span data-ttu-id="03560-145">To platí i `<files>` v sekci:</span><span class="sxs-lookup"><span data-stu-id="03560-145">This also goes in the `<files>` section:</span></span>

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

### <a name="adding-the-native-implementation-libraries"></a><span data-ttu-id="03560-146">Přidání nativních implementačních knihoven</span><span class="sxs-lookup"><span data-stu-id="03560-146">Adding the native implementation libraries</span></span>

<span data-ttu-id="03560-147">V rámci komponenty je základní logika typu ImageEnhancer v nativním `ImageEnhancer.dll` kódu, který je obsažen v různých sestaveních, které jsou generovány pro každý cílový runtime (ARM, x86 a x64).</span><span class="sxs-lookup"><span data-stu-id="03560-147">Within your component, the core logic of the ImageEnhancer type is in native code, which is contained in the various `ImageEnhancer.dll` assemblies that are generated for each target runtime (ARM, x86, and x64).</span></span> <span data-ttu-id="03560-148">Chcete-li je zahrnout do balíčku, odkazujte na ně v `<files>` sekci spolu s přidruženými soubory prostředků .pri:</span><span class="sxs-lookup"><span data-stu-id="03560-148">To include these in the package, reference them in the `<files>` section along with their associated .pri resource files:</span></span>

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

### <a name="adding-targets"></a><span data-ttu-id="03560-149">Přidání .targets</span><span class="sxs-lookup"><span data-stu-id="03560-149">Adding .targets</span></span>

<span data-ttu-id="03560-150">Dále c++ a JavaScript projekty, které mohou využívat váš balíček NuGet potřebovat soubor .targets k identifikaci potřebné sestavení a winmd soubory.</span><span class="sxs-lookup"><span data-stu-id="03560-150">Next, C++ and JavaScript projects that might consume your NuGet package need a .targets file to identify the necessary assembly and winmd files.</span></span> <span data-ttu-id="03560-151">(Projekty jazyka C# a Visual Basic to dělají automaticky.) Vytvořte tento soubor zkopírováním `ImageEnhancer.targets` níže uvedeného textu do `.nuspec` a uložte jej do stejné složky jako soubor.</span><span class="sxs-lookup"><span data-stu-id="03560-151">(C# and Visual Basic projects do this automatically.) Create this file by copying the text below into `ImageEnhancer.targets` and save it in the same folder as the `.nuspec` file.</span></span> <span data-ttu-id="03560-152">_Poznámka_: `.targets` Tento soubor musí mít stejný název jako ID `<Id>` balíčku (např. prvek v souboru): `.nupspec`</span><span class="sxs-lookup"><span data-stu-id="03560-152">_Note_: This `.targets` file needs to be the same name as the package ID (e.g. the `<Id>` element in the `.nupspec` file):</span></span>

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

<span data-ttu-id="03560-153">Pak se `ImageEnhancer.targets` podívejte `.nuspec` do souboru:</span><span class="sxs-lookup"><span data-stu-id="03560-153">Then refer to `ImageEnhancer.targets` in your `.nuspec` file:</span></span>

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

### <a name="final-nuspec"></a><span data-ttu-id="03560-154">Konečný .nuspec</span><span class="sxs-lookup"><span data-stu-id="03560-154">Final .nuspec</span></span>

<span data-ttu-id="03560-155">Konečný `.nuspec` soubor by nyní měl vypadat takto, kde by měl být opět nahrazen YOUR_NAME příslušnou hodnotou:</span><span class="sxs-lookup"><span data-stu-id="03560-155">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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

## <a name="package-the-component"></a><span data-ttu-id="03560-156">Balení komponenty</span><span class="sxs-lookup"><span data-stu-id="03560-156">Package the component</span></span>

<span data-ttu-id="03560-157">S dokončeným `.nuspec` odkazováním na všechny soubory, které potřebujete zahrnout do `pack` balíčku, jste připraveni spustit příkaz:</span><span class="sxs-lookup"><span data-stu-id="03560-157">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack ImageEnhancer.nuspec
```

<span data-ttu-id="03560-158">To generuje `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="03560-158">This generates `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="03560-159">Otevření tohoto souboru v nástroji, jako je [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) a rozbalení všech uzlů, uvidíte následující obsah:</span><span class="sxs-lookup"><span data-stu-id="03560-159">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![NuGet Package Explorer zobrazující balíček ImageEnhancer](media/UWP-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="03560-161">Soubor `.nupkg` je pouze soubor ZIP s jinou příponou.</span><span class="sxs-lookup"><span data-stu-id="03560-161">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="03560-162">Můžete také prozkoumat obsah balíčku, `.nupkg` `.zip`pak změnou na , ale nezapomeňte obnovit rozšíření před odesláním balíček nuget.org.</span><span class="sxs-lookup"><span data-stu-id="03560-162">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="03560-163">Chcete-li balíček zpřístupnit ostatním [vývojářům,](../nuget-org/publish-a-package.md)postupujte podle pokynů k části Publikovat balíček .</span><span class="sxs-lookup"><span data-stu-id="03560-163">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="03560-164">Související témata</span><span class="sxs-lookup"><span data-stu-id="03560-164">Related topics</span></span>

- [<span data-ttu-id="03560-165">Odkaz na odkaz .nuspec</span><span class="sxs-lookup"><span data-stu-id="03560-165">.nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="03560-166">Balíčky symbolů</span><span class="sxs-lookup"><span data-stu-id="03560-166">Symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="03560-167">Správa verzí balíčku</span><span class="sxs-lookup"><span data-stu-id="03560-167">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="03560-168">Podpora více verzí rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="03560-168">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="03560-169">Zahrnout rekvizity a cíle MSBuild do balíčku</span><span class="sxs-lookup"><span data-stu-id="03560-169">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="03560-170">Vytváření lokalizovaných balíčků</span><span class="sxs-lookup"><span data-stu-id="03560-170">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
