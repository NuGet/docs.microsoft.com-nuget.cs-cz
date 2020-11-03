---
title: Vytvoření balíčků NuGet pro Univerzální platforma Windows
description: Ucelený návod k vytváření balíčků NuGet pomocí prostředí Windows Runtime komponenty pro Univerzální platforma Windows v jazyce C#.
author: rrelyea
ms.author: rrelyea
ms.date: 02/28/2020
ms.topic: tutorial
ms.openlocfilehash: 6f8037f439d627af158b6d5b7746a633b053e514
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238007"
---
# <a name="create-uwp-packages-c"></a><span data-ttu-id="d21b4-103">Vytváření balíčků UWP (C#)</span><span class="sxs-lookup"><span data-stu-id="d21b4-103">Create UWP packages (C#)</span></span>

<span data-ttu-id="d21b4-104">[Univerzální platforma Windows (UWP)](/windows/uwp) poskytuje běžnou aplikační platformu pro každé zařízení s Windows 10.</span><span class="sxs-lookup"><span data-stu-id="d21b4-104">The [Universal Windows Platform (UWP)](/windows/uwp) provides a common app platform for every device that runs Windows 10.</span></span> <span data-ttu-id="d21b4-105">V rámci tohoto modelu můžou aplikace pro UWP volat rozhraní API WinRT, která jsou společná pro všechna zařízení, a taky rozhraní API (včetně Win32 a .NET), která jsou specifická pro řadu zařízení, ve které je aplikace spuštěná.</span><span class="sxs-lookup"><span data-stu-id="d21b4-105">Within this model, UWP apps can call both the WinRT APIs that are common to all devices, and also APIs (including Win32 and .NET) that are specific to the device family on which the app is running.</span></span>

<span data-ttu-id="d21b4-106">V tomto návodu vytvoříte balíček NuGet pomocí komponenty pro platformu UWP v jazyce C# (včetně ovládacího prvku XAML), který lze použít v spravovaných i nativních projektech.</span><span class="sxs-lookup"><span data-stu-id="d21b4-106">In this walkthrough you create a NuGet package with a C# UWP component (including a XAML control) that can be used in both Managed and Native projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d21b4-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="d21b4-107">Prerequisites</span></span>

1. <span data-ttu-id="d21b4-108">Visual Studio 2019.</span><span class="sxs-lookup"><span data-stu-id="d21b4-108">Visual Studio 2019.</span></span> <span data-ttu-id="d21b4-109">Nainstalujte si bezplatnou edici 2019 Community Edition od [VisualStudio.com](https://www.visualstudio.com/); můžete použít i edice Professional a Enterprise.</span><span class="sxs-lookup"><span data-stu-id="d21b4-109">Install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well.</span></span>

1. <span data-ttu-id="d21b4-110">Rozhraní příkazového řádku NuGet</span><span class="sxs-lookup"><span data-stu-id="d21b4-110">NuGet CLI.</span></span> <span data-ttu-id="d21b4-111">Stáhněte si nejnovější verzi `nuget.exe` z [NuGet.org/downloads](https://nuget.org/downloads)a uložte ji do umístění dle vašeho výběru (stažení je `.exe` přímo).</span><span class="sxs-lookup"><span data-stu-id="d21b4-111">Download the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice (the download is the `.exe` directly).</span></span> <span data-ttu-id="d21b4-112">Pak přidejte toto umístění do proměnné prostředí PATH, pokud ještě není.</span><span class="sxs-lookup"><span data-stu-id="d21b4-112">Then add that location to your PATH environment variable if it isn't already.</span></span> <span data-ttu-id="d21b4-113">[Další podrobnosti](../reference/nuget-exe-cli-reference.md#windows).</span><span class="sxs-lookup"><span data-stu-id="d21b4-113">[More details](../reference/nuget-exe-cli-reference.md#windows).</span></span>

## <a name="create-a-uwp-windows-runtime-component"></a><span data-ttu-id="d21b4-114">Vytvoření komponenty prostředí Windows Runtime UWP</span><span class="sxs-lookup"><span data-stu-id="d21b4-114">Create a UWP Windows Runtime component</span></span>

1. <span data-ttu-id="d21b4-115">V aplikaci Visual Studio zvolte **soubor > nový > projekt** , vyhledejte "UWP c#", vyberte šablonu **prostředí Windows Runtime komponenty (Universal Windows)** , klikněte na další, změňte název na ImageEnhancer a klikněte na vytvořit.</span><span class="sxs-lookup"><span data-stu-id="d21b4-115">In Visual Studio, choose **File > New > Project** , search for "uwp c#", select the **Windows Runtime Component (Universal Windows)** template, click next, change the name to ImageEnhancer, and click Create.</span></span> <span data-ttu-id="d21b4-116">Po zobrazení výzvy přijměte výchozí hodnoty pro cílovou verzi a minimální verzi.</span><span class="sxs-lookup"><span data-stu-id="d21b4-116">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

    ![Vytváření nového projektu součásti prostředí Windows Runtime pro UWP](media/UWP-NewProject-CS.png)

1. <span data-ttu-id="d21b4-118">Klikněte pravým tlačítkem na projekt v Průzkumník řešení, vyberte **přidat > novou položku** , vyberte **ovládací prvek s šablonou** , změňte název na AwesomeImageControl.cs a klikněte na **Přidat** :</span><span class="sxs-lookup"><span data-stu-id="d21b4-118">Right click the project in Solution Explorer, select **Add > New Item** , select **Templated Control** , change the name to AwesomeImageControl.cs, and click **Add** :</span></span>

    ![Přidání nové položky ovládacího prvku v šabloně XAML do projektu](media/UWP-NewXAMLControl-CS.png)

1. <span data-ttu-id="d21b4-120">Klikněte pravým tlačítkem na projekt v Průzkumník řešení a vyberte **Vlastnosti.**</span><span class="sxs-lookup"><span data-stu-id="d21b4-120">Right-click the project in Solution Explorer and select **Properties.**</span></span> <span data-ttu-id="d21b4-121">Na stránce Vlastnosti klikněte na kartu **sestavení** a povolte **soubor dokumentace XML** :</span><span class="sxs-lookup"><span data-stu-id="d21b4-121">In the Properties page, choose **Build** tab and enable **XML Documentation File** :</span></span>

    ![Nastavení generovat soubory dokumentace XML na Ano](media/UWP-GenerateXMLDocFiles-CS.png)

1. <span data-ttu-id="d21b4-123">Klikněte pravým tlačítkem na *řešení* , vyberte **dávkové sestavení** , zaškrtněte pět polí sestavení v dialogovém okně, jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="d21b4-123">Right click the *solution* now, select **Batch Build** , check the five build boxes in the dialog as shown below.</span></span> <span data-ttu-id="d21b4-124">Tím je zajištěno, že při sestavení vygenerujete úplnou sadu artefaktů pro každý cílový systém, který systém Windows podporuje.</span><span class="sxs-lookup"><span data-stu-id="d21b4-124">This makes sure that when you do a build, you generate a full set of artifacts for each of the target systems that Windows supports.</span></span>

    ![Dávkové sestavení](media/UWP-BatchBuild-CS.png)

1. <span data-ttu-id="d21b4-126">V dialogovém okně dávkové sestavení a kliknutím na **sestavení** ověřte projekt a vytvořte výstupní soubory, které potřebujete pro balíček NuGet.</span><span class="sxs-lookup"><span data-stu-id="d21b4-126">In the Batch Build dialog, and click **Build** to verify the project and create the output files that you need for the NuGet package.</span></span>

> [!Note]
> <span data-ttu-id="d21b4-127">V tomto návodu použijete pro balíček artefakty ladění.</span><span class="sxs-lookup"><span data-stu-id="d21b4-127">In this walkthrough you use the Debug artifacts for the package.</span></span> <span data-ttu-id="d21b4-128">V případě neladicího balíčku si místo toho v dialogovém okně dávkové sestavení vyhledejte možnosti vydání a podívejte se na výsledné složky verze v následujících krocích.</span><span class="sxs-lookup"><span data-stu-id="d21b4-128">For non-debug package, check the Release options in the Batch Build dialog instead, and refer to the resulting Release folders in the steps that follow.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="d21b4-129">Vytvoření a aktualizace souboru. nuspec</span><span class="sxs-lookup"><span data-stu-id="d21b4-129">Create and update the .nuspec file</span></span>

<span data-ttu-id="d21b4-130">Chcete-li vytvořit počáteční `.nuspec` soubor, proveďte následující tři kroky.</span><span class="sxs-lookup"><span data-stu-id="d21b4-130">To create the initial `.nuspec` file, do the three steps below.</span></span> <span data-ttu-id="d21b4-131">Následující části vás pak provede dalšími potřebnými aktualizacemi.</span><span class="sxs-lookup"><span data-stu-id="d21b4-131">The sections that follow then guide you through other necessary updates.</span></span>

1. <span data-ttu-id="d21b4-132">Otevřete příkazový řádek a přejděte do složky, která obsahuje `ImageEnhancer.csproj` (Toto je podsložka, ve které je soubor řešení).</span><span class="sxs-lookup"><span data-stu-id="d21b4-132">Open a command prompt and navigate to the folder containing `ImageEnhancer.csproj` (this will be a subfolder below where the solution file is).</span></span>
1. <span data-ttu-id="d21b4-133">Spusťte [`NuGet spec`](../reference/cli-reference/cli-ref-spec.md) příkaz, který se má vygenerovat `ImageEnhancer.nuspec` (název souboru se povede z názvu `.csroj` souboru):</span><span class="sxs-lookup"><span data-stu-id="d21b4-133">Run the [`NuGet spec`](../reference/cli-reference/cli-ref-spec.md) command to generate `ImageEnhancer.nuspec` (the name of the file is taken from the name of the `.csroj` file):</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="d21b4-134">Otevřete `ImageEnhancer.nuspec` v editoru a aktualizujte ho, aby odpovídal následujícímu, a nahraďte YOUR_NAME příslušnou hodnotou.</span><span class="sxs-lookup"><span data-stu-id="d21b4-134">Open `ImageEnhancer.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="d21b4-135">Nenechávejte žádné z hodnot $propertyName $.</span><span class="sxs-lookup"><span data-stu-id="d21b4-135">Do not leave any of the $propertyName$ values.</span></span> <span data-ttu-id="d21b4-136">`<id>`Hodnota konkrétně musí být jedinečná napříč NuGet.org (podívejte se na zásady vytváření názvů popsané v tématu [Vytvoření balíčku](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="d21b4-136">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="d21b4-137">Všimněte si také, že je nutné také aktualizovat značky Autor a popis, jinak se zobrazí chyba v průběhu balení.</span><span class="sxs-lookup"><span data-stu-id="d21b4-137">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
        <copyright>Copyright 2020</copyright>
        <tags>image enhancer imageenhancer</tags>
        </metadata>
    </package>
    ```

> [!Note]
> <span data-ttu-id="d21b4-138">Pro balíčky sestavené pro veřejnou spotřebu věnujte zvláštní pozornost `<tags>` prvku, protože tyto značky můžou ostatním uživatelům najít váš balíček a pochopit, co to dělá.</span><span class="sxs-lookup"><span data-stu-id="d21b4-138">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

### <a name="adding-windows-metadata-to-the-package"></a><span data-ttu-id="d21b4-139">Přidávají se metadata Windows do balíčku.</span><span class="sxs-lookup"><span data-stu-id="d21b4-139">Adding Windows metadata to the package</span></span>

<span data-ttu-id="d21b4-140">Komponenta prostředí Windows Runtime vyžaduje metadata, která popisují všechny veřejně dostupné typy, což umožňuje ostatním aplikacím a knihovnám využívat součást.</span><span class="sxs-lookup"><span data-stu-id="d21b4-140">A Windows Runtime Component requires metadata that describes all of its publicly available types, which makes it possible for other apps and libraries to consume the component.</span></span> <span data-ttu-id="d21b4-141">Tato metadata jsou obsažena v souboru WinMD, který je vytvořen při kompilování projektu a musí být součástí balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="d21b4-141">This metadata is contained in a .winmd file, which is created when you compile the project and must be included in your NuGet package.</span></span> <span data-ttu-id="d21b4-142">Soubor XML s daty technologie IntelliSense je také sestaven současně a měl by být zahrnut také.</span><span class="sxs-lookup"><span data-stu-id="d21b4-142">An XML file with IntelliSense data is also built at the same time, and should be included as well.</span></span>

<span data-ttu-id="d21b4-143">Přidejte `<files>` do souboru následující uzel `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="d21b4-143">Add the following `<files>` node to the `.nuspec` file:</span></span>

```xml
<package>
    <metadata>
        ...
    </metadata>

    <files>
        <!-- WinMd and IntelliSense files -->
      <file src="bin\Debug\ImageEnhancer.winmd" target="lib\uap10.0"/>
      <file src="bin\Debug\ImageEnhancer.xml" target="lib\uap10.0"/>
    </files>
</package>
```

### <a name="adding-xaml-content"></a><span data-ttu-id="d21b4-144">Přidání obsahu XAML</span><span class="sxs-lookup"><span data-stu-id="d21b4-144">Adding XAML content</span></span>

<span data-ttu-id="d21b4-145">Chcete-li zahrnout ovládací prvek XAML do komponenty, je nutné přidat soubor XAML, který má výchozí šablonu pro ovládací prvek (jak je vygenerována šablonou projektu).</span><span class="sxs-lookup"><span data-stu-id="d21b4-145">To include a XAML control with your component, you need to add the XAML file that has the default template for the control (as generated by the project template).</span></span> <span data-ttu-id="d21b4-146">To se taky doplní v `<files>` části:</span><span class="sxs-lookup"><span data-stu-id="d21b4-146">This also goes in the `<files>` section:</span></span>

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

### <a name="adding-the-native-implementation-libraries"></a><span data-ttu-id="d21b4-147">Přidání nativních implementačních knihoven</span><span class="sxs-lookup"><span data-stu-id="d21b4-147">Adding the native implementation libraries</span></span>

<span data-ttu-id="d21b4-148">V rámci vaší komponenty je základní logika typu ImageEnhancer v nativním kódu, který je obsažen v různých `ImageEnhancer.winmd` sestaveních, která jsou generována pro každý cílový modul runtime (ARM, ARM64, x86 a x64).</span><span class="sxs-lookup"><span data-stu-id="d21b4-148">Within your component, the core logic of the ImageEnhancer type is in native code, which is contained in the various `ImageEnhancer.winmd` assemblies that are generated for each target runtime (ARM, ARM64, x86, and x64).</span></span> <span data-ttu-id="d21b4-149">Pokud je chcete zahrnout do balíčku, odkázat je v `<files>` části spolu s jejich přidruženými zdrojovými soubory. pri:</span><span class="sxs-lookup"><span data-stu-id="d21b4-149">To include these in the package, reference them in the `<files>` section along with their associated .pri resource files:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- WINMDs and resources -->
      <file src="bin\ARM\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm"/>
      <file src="bin\ARM\Debug\ImageEnhancer.pri" target="runtimes\win10-arm"/>

      <file src="bin\ARM64\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm64"/>
      <file src="bin\ARM64\Debug\ImageEnhancer.pri" target="runtimes\win10-arm64"/>

      <file src="bin\x64\Debug\ImageEnhancer.winmd" target="runtimes\win10-x64"/>
      <file src="bin\x64\Debug\ImageEnhancer.pri" target="runtimes\win10-x64"/>

      <file src="bin\x86\Debug\ImageEnhancer.winmd" target="runtimes\win10-x86"/>
      <file src="bin\x86\Debug\ImageEnhancer.pri" target="runtimes\win10-x86"/>

    </files>
</package>
```

### <a name="final-nuspec"></a><span data-ttu-id="d21b4-150">Finální. nuspec</span><span class="sxs-lookup"><span data-stu-id="d21b4-150">Final .nuspec</span></span>

<span data-ttu-id="d21b4-151">Konečný `.nuspec` soubor by teď měl vypadat nějak takto, kde se znovu YOUR_NAME třeba nahradit příslušnou hodnotou:</span><span class="sxs-lookup"><span data-stu-id="d21b4-151">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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
    <copyright>Copyright 2020</copyright>
    <tags>image enhancer imageenhancer</tags>
    </metadata>
    <files>
    <!-- WinMd and IntelliSense -->
      <file src="bin\Debug\ImageEnhancer.winmd" target="lib\uap10.0"/>
      <file src="bin\Debug\ImageEnhancer.xml" target="lib\uap10.0"/>

    <!-- XAML controls -->
    <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    <!-- WINMDs and resources -->
      <file src="bin\ARM\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm"/>
      <file src="bin\ARM\Debug\ImageEnhancer.pri" target="runtimes\win10-arm"/>

      <file src="bin\ARM64\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm64"/>
      <file src="bin\ARM64\Debug\ImageEnhancer.pri" target="runtimes\win10-arm64"/>

      <file src="bin\x64\Debug\ImageEnhancer.winmd" target="runtimes\win10-x64"/>
      <file src="bin\x64\Debug\ImageEnhancer.pri" target="runtimes\win10-x64"/>

      <file src="bin\x86\Debug\ImageEnhancer.winmd" target="runtimes\win10-x86"/>
      <file src="bin\x86\Debug\ImageEnhancer.pri" target="runtimes\win10-x86"/>

    </files>
</package>
```

## <a name="package-the-component"></a><span data-ttu-id="d21b4-152">Zabalení komponenty</span><span class="sxs-lookup"><span data-stu-id="d21b4-152">Package the component</span></span>

<span data-ttu-id="d21b4-153">Po dokončení `.nuspec` odkazů na všechny soubory, které potřebujete zahrnout do balíčku, jste připraveni spustit [`nuget pack`](../reference/cli-reference/cli-ref-pack.md) příkaz:</span><span class="sxs-lookup"><span data-stu-id="d21b4-153">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the [`nuget pack`](../reference/cli-reference/cli-ref-pack.md) command:</span></span>

```cli
nuget pack ImageEnhancer.nuspec
```

<span data-ttu-id="d21b4-154">Tím vygenerujete `ImageEnhancer.YOUR_NAME.1.0.0.nupkg` .</span><span class="sxs-lookup"><span data-stu-id="d21b4-154">This generates `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="d21b4-155">Tento soubor otevřete v nástroji jako [Průzkumník balíčků NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) a rozbalíte všechny uzly. zobrazí se následující obsah:</span><span class="sxs-lookup"><span data-stu-id="d21b4-155">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![Průzkumník balíčků NuGet zobrazující balíček ImageEnhancer](media/UWP-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="d21b4-157">`.nupkg`Soubor je pouze soubor zip s jinou příponou.</span><span class="sxs-lookup"><span data-stu-id="d21b4-157">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="d21b4-158">Můžete také prošetřit obsah balíčku, potom změnou `.nupkg` na `.zip` , ale nezapomeňte obnovit rozšíření před nahráním balíčku do NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="d21b4-158">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="d21b4-159">Pokud chcete balíček zpřístupnit ostatním vývojářům, postupujte podle pokynů v tématu [publikování balíčku](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="d21b4-159">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="d21b4-160">Související témata</span><span class="sxs-lookup"><span data-stu-id="d21b4-160">Related topics</span></span>

- [<span data-ttu-id="d21b4-161">Odkaz. nuspec</span><span class="sxs-lookup"><span data-stu-id="d21b4-161">.nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="d21b4-162">Balíčky symbolů</span><span class="sxs-lookup"><span data-stu-id="d21b4-162">Symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="d21b4-163">Správa verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="d21b4-163">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="d21b4-164">Podpora více verzí .NET Framework</span><span class="sxs-lookup"><span data-stu-id="d21b4-164">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="d21b4-165">Zahrnutí vlastností MSBuild a cílů do balíčku</span><span class="sxs-lookup"><span data-stu-id="d21b4-165">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="d21b4-166">Vytváření lokalizovaných balíčků</span><span class="sxs-lookup"><span data-stu-id="d21b4-166">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)