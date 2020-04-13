---
title: Vytvoření balíčků NuGet pro univerzální platformu Windows
description: Komplexní návod k vytváření balíčků NuGet pomocí součásti prostředí Windows Runtime pro univerzální platformu Windows v systému C#.
author: rrelyea
ms.author: rrelyea
ms.date: 02/28/2020
ms.topic: tutorial
ms.openlocfilehash: 61f46f2623769927f881877cfe3f96132211b442
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231803"
---
# <a name="create-uwp-packages-c"></a><span data-ttu-id="35866-103">Vytvořit balíčky UPW (C#)</span><span class="sxs-lookup"><span data-stu-id="35866-103">Create UWP packages (C#)</span></span>

<span data-ttu-id="35866-104">[Univerzální platforma Windows (UPW)](/windows/uwp) poskytuje společnou platformu aplikací pro každé zařízení se systémem Windows 10.</span><span class="sxs-lookup"><span data-stu-id="35866-104">The [Universal Windows Platform (UWP)](/windows/uwp) provides a common app platform for every device that runs Windows 10.</span></span> <span data-ttu-id="35866-105">V rámci tohoto modelu mohou aplikace UPW volat rozhraní API WinRT, která jsou společná pro všechna zařízení, a také rozhraní API (včetně Win32 a .NET), která jsou specifická pro rodinu zařízení, na které je aplikace spuštěna.</span><span class="sxs-lookup"><span data-stu-id="35866-105">Within this model, UWP apps can call both the WinRT APIs that are common to all devices, and also APIs (including Win32 and .NET) that are specific to the device family on which the app is running.</span></span>

<span data-ttu-id="35866-106">V tomto návodu vytvoříte balíček NuGet s komponentou C# UWP (včetně ovládacího prvku XAML), který lze použít v řízených i nativních projektech.</span><span class="sxs-lookup"><span data-stu-id="35866-106">In this walkthrough you create a NuGet package with a C# UWP component (including a XAML control) that can be used in both Managed and Native projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="35866-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="35866-107">Prerequisites</span></span>

1. <span data-ttu-id="35866-108">Visual Studio 2019.</span><span class="sxs-lookup"><span data-stu-id="35866-108">Visual Studio 2019.</span></span> <span data-ttu-id="35866-109">Nainstalujte verzi Community 2019 zdarma od [visualstudio.com](https://www.visualstudio.com/); můžete také použít edice Professional a Enterprise.</span><span class="sxs-lookup"><span data-stu-id="35866-109">Install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well.</span></span>

1. <span data-ttu-id="35866-110">NuGet CLI.</span><span class="sxs-lookup"><span data-stu-id="35866-110">NuGet CLI.</span></span> <span data-ttu-id="35866-111">Stáhněte si `nuget.exe` nejnovější verzi z [nuget.org/downloads](https://nuget.org/downloads)a uložte ji na `.exe` místo podle vašeho výběru (stahování je přímo).</span><span class="sxs-lookup"><span data-stu-id="35866-111">Download the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice (the download is the `.exe` directly).</span></span> <span data-ttu-id="35866-112">Pak přidejte toto umístění do proměnné prostředí PATH, pokud ještě není.</span><span class="sxs-lookup"><span data-stu-id="35866-112">Then add that location to your PATH environment variable if it isn't already.</span></span> <span data-ttu-id="35866-113">[Další podrobnosti](/nuget/reference/nuget-exe-cli-reference#windows).</span><span class="sxs-lookup"><span data-stu-id="35866-113">[More details](/nuget/reference/nuget-exe-cli-reference#windows).</span></span>

## <a name="create-a-uwp-windows-runtime-component"></a><span data-ttu-id="35866-114">Vytvoření součásti runtime systému Windows v programu UPW</span><span class="sxs-lookup"><span data-stu-id="35866-114">Create a UWP Windows Runtime component</span></span>

1. <span data-ttu-id="35866-115">V sadě Visual Studio zvolte **Soubor > Nový > Project**, vyhledejte položku "uwp c#", vyberte šablonu **komponenty Prostředí Windows Runtime (Universal Windows),** klepněte na tlačítko Další, změňte název na ImageEnhancer a klepněte na tlačítko Vytvořit.</span><span class="sxs-lookup"><span data-stu-id="35866-115">In Visual Studio, choose **File > New > Project**, search for "uwp c#", select the **Windows Runtime Component (Universal Windows)** template, click next, change the name to ImageEnhancer, and click Create.</span></span> <span data-ttu-id="35866-116">Po zobrazení výzvy přijměte výchozí hodnoty pro cílovou a minimální verzi.</span><span class="sxs-lookup"><span data-stu-id="35866-116">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

    ![Vytvoření nového projektu komponenty runtime systému Windows UWP](media/UWP-NewProject-CS.png)

1. <span data-ttu-id="35866-118">Klepněte pravým tlačítkem myši na projekt v Průzkumníku řešení, vyberte **Přidat > novou položku**, vyberte **Šablonový ovládací prvek**, změňte název, AwesomeImageControl.cs, a klepněte na **Přidat**:</span><span class="sxs-lookup"><span data-stu-id="35866-118">Right click the project in Solution Explorer, select **Add > New Item**, select **Templated Control**, change the name to AwesomeImageControl.cs, and click **Add**:</span></span>

    ![Přidání nové položky ovládacího prvku šablony XAML do projektu](media/UWP-NewXAMLControl-CS.png)

1. <span data-ttu-id="35866-120">Klikněte pravým tlačítkem myši na projekt v Průzkumníku řešení a vyberte **Vlastnosti.**</span><span class="sxs-lookup"><span data-stu-id="35866-120">Right-click the project in Solution Explorer and select **Properties.**</span></span> <span data-ttu-id="35866-121">Na stránce Vlastnosti zvolte **Vytvořit** kartu a povolte **soubor dokumentace XML**:</span><span class="sxs-lookup"><span data-stu-id="35866-121">In the Properties page, choose **Build** tab and enable **XML Documentation File**:</span></span>

    ![Nastavení generování souborů dokumentace XML na ano](media/UWP-GenerateXMLDocFiles-CS.png)

1. <span data-ttu-id="35866-123">Klikněte pravým tlačítkem myši na *řešení,* vyberte **Dávkové sestavení**, zaškrtněte pět sestavení v dialogovém okně, jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="35866-123">Right click the *solution* now, select **Batch Build**, check the five build boxes in the dialog as shown below.</span></span> <span data-ttu-id="35866-124">Tím zajistíte, že při vytváření sestavení vygenerujete úplnou sadu artefaktů pro každý z cílových systémů, které systém Windows podporuje.</span><span class="sxs-lookup"><span data-stu-id="35866-124">This makes sure that when you do a build, you generate a full set of artifacts for each of the target systems that Windows supports.</span></span>

    ![Dávkové sestavení](media/UWP-BatchBuild-CS.png)

1. <span data-ttu-id="35866-126">V dialogovém okně Dávkové sestavení a klepněte na tlačítko **Sestavit,** chcete-li ověřit projekt a vytvořit výstupní soubory, které potřebujete pro balíček NuGet.</span><span class="sxs-lookup"><span data-stu-id="35866-126">In the Batch Build dialog, and click **Build** to verify the project and create the output files that you need for the NuGet package.</span></span>

> [!Note]
> <span data-ttu-id="35866-127">V tomto návodu použijete artefakty ladění pro balíček.</span><span class="sxs-lookup"><span data-stu-id="35866-127">In this walkthrough you use the Debug artifacts for the package.</span></span> <span data-ttu-id="35866-128">U balíčku bez ladění zkontrolujte možnosti vydání v dialogovém okně Dávkové sestavení a v následujících krocích se podívejte na výsledné složky release.</span><span class="sxs-lookup"><span data-stu-id="35866-128">For non-debug package, check the Release options in the Batch Build dialog instead, and refer to the resulting Release folders in the steps that follow.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="35866-129">Vytvoření a aktualizace souboru Nuspec</span><span class="sxs-lookup"><span data-stu-id="35866-129">Create and update the .nuspec file</span></span>

<span data-ttu-id="35866-130">Chcete-li `.nuspec` vytvořit počáteční soubor, proveďte následující tři kroky.</span><span class="sxs-lookup"><span data-stu-id="35866-130">To create the initial `.nuspec` file, do the three steps below.</span></span> <span data-ttu-id="35866-131">Následující části vás pak provedou dalšími nezbytnými aktualizacemi.</span><span class="sxs-lookup"><span data-stu-id="35866-131">The sections that follow then guide you through other necessary updates.</span></span>

1. <span data-ttu-id="35866-132">Otevřete příkazový řádek a přejděte do složky obsahující `ImageEnhancer.csproj` (bude to podsložka pod místem, kde je soubor řešení).</span><span class="sxs-lookup"><span data-stu-id="35866-132">Open a command prompt and navigate to the folder containing `ImageEnhancer.csproj` (this will be a subfolder below where the solution file is).</span></span>
1. <span data-ttu-id="35866-133">Spusťte příkaz, [`NuGet spec`](/nuget/reference/cli-reference/cli-ref-spec) který chcete vygenerovat `ImageEnhancer.nuspec` (název `.csroj` souboru je převzat z názvu souboru):</span><span class="sxs-lookup"><span data-stu-id="35866-133">Run the [`NuGet spec`](/nuget/reference/cli-reference/cli-ref-spec) command to generate `ImageEnhancer.nuspec` (the name of the file is taken from the name of the `.csroj` file):</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="35866-134">Otevřete `ImageEnhancer.nuspec` v editoru a aktualizujte jej tak, aby odpovídal následujícímu, a nahrazují YOUR_NAME příslušnou hodnotou.</span><span class="sxs-lookup"><span data-stu-id="35866-134">Open `ImageEnhancer.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="35866-135">Nenechávejte žádné hodnoty $propertyName$.</span><span class="sxs-lookup"><span data-stu-id="35866-135">Do not leave any of the $propertyName$ values.</span></span> <span data-ttu-id="35866-136">Hodnota, `<id>` konkrétně musí být jedinečný napříč nuget.org (viz konvence pojmenování popsané v [vytvoření balíčku).](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)</span><span class="sxs-lookup"><span data-stu-id="35866-136">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="35866-137">Všimněte si také, že musíte také aktualizovat značky autora a popisu nebo se během kroku balení zobrazí chyba.</span><span class="sxs-lookup"><span data-stu-id="35866-137">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
> <span data-ttu-id="35866-138">U balíčků vytvořených pro veřejnou `<tags>` spotřebu věnujte tomuto prvku zvláštní pozornost, protože tyto značky pomáhají ostatním najít váš balíček a pochopit, co dělá.</span><span class="sxs-lookup"><span data-stu-id="35866-138">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

### <a name="adding-windows-metadata-to-the-package"></a><span data-ttu-id="35866-139">Přidání metadat systému Windows do balíčku</span><span class="sxs-lookup"><span data-stu-id="35866-139">Adding Windows metadata to the package</span></span>

<span data-ttu-id="35866-140">Součást prostředí Windows Runtime vyžaduje metadata, která popisují všechny jeho veřejně dostupné typy, což umožňuje ostatním aplikacím a knihovnám využívat komponentu.</span><span class="sxs-lookup"><span data-stu-id="35866-140">A Windows Runtime Component requires metadata that describes all of its publicly available types, which makes it possible for other apps and libraries to consume the component.</span></span> <span data-ttu-id="35866-141">Tato metadata jsou obsažena v souboru .winmd, který je vytvořen při kompilaci projektu a musí být zahrnuty do balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="35866-141">This metadata is contained in a .winmd file, which is created when you compile the project and must be included in your NuGet package.</span></span> <span data-ttu-id="35866-142">Soubor XML s daty Technologie IntelliSense je také vytvořen současně a měl by být také zahrnut.</span><span class="sxs-lookup"><span data-stu-id="35866-142">An XML file with IntelliSense data is also built at the same time, and should be included as well.</span></span>

<span data-ttu-id="35866-143">Přidejte `<files>` do souboru `.nuspec` následující uzel:</span><span class="sxs-lookup"><span data-stu-id="35866-143">Add the following `<files>` node to the `.nuspec` file:</span></span>

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

### <a name="adding-xaml-content"></a><span data-ttu-id="35866-144">Přidání obsahu XAML</span><span class="sxs-lookup"><span data-stu-id="35866-144">Adding XAML content</span></span>

<span data-ttu-id="35866-145">Chcete-li zahrnout ovládací prvek XAML s komponentou, je třeba přidat soubor XAML, který má výchozí šablonu pro ovládací prvek (jak je generováno šablonou projektu).</span><span class="sxs-lookup"><span data-stu-id="35866-145">To include a XAML control with your component, you need to add the XAML file that has the default template for the control (as generated by the project template).</span></span> <span data-ttu-id="35866-146">To platí i `<files>` v sekci:</span><span class="sxs-lookup"><span data-stu-id="35866-146">This also goes in the `<files>` section:</span></span>

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

### <a name="adding-the-native-implementation-libraries"></a><span data-ttu-id="35866-147">Přidání nativních implementačních knihoven</span><span class="sxs-lookup"><span data-stu-id="35866-147">Adding the native implementation libraries</span></span>

<span data-ttu-id="35866-148">V rámci komponenty je základní logika typu ImageEnhancer v nativním `ImageEnhancer.winmd` kódu, který je obsažen v různých sestaveních, které jsou generovány pro každý cílový runtime (ARM, ARM64, x86 a x64).</span><span class="sxs-lookup"><span data-stu-id="35866-148">Within your component, the core logic of the ImageEnhancer type is in native code, which is contained in the various `ImageEnhancer.winmd` assemblies that are generated for each target runtime (ARM, ARM64, x86, and x64).</span></span> <span data-ttu-id="35866-149">Chcete-li je zahrnout do balíčku, odkazujte na ně v `<files>` sekci spolu s přidruženými soubory prostředků .pri:</span><span class="sxs-lookup"><span data-stu-id="35866-149">To include these in the package, reference them in the `<files>` section along with their associated .pri resource files:</span></span>

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

### <a name="final-nuspec"></a><span data-ttu-id="35866-150">Konečný .nuspec</span><span class="sxs-lookup"><span data-stu-id="35866-150">Final .nuspec</span></span>

<span data-ttu-id="35866-151">Konečný `.nuspec` soubor by nyní měl vypadat takto, kde by měl být opět nahrazen YOUR_NAME příslušnou hodnotou:</span><span class="sxs-lookup"><span data-stu-id="35866-151">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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

## <a name="package-the-component"></a><span data-ttu-id="35866-152">Balení komponenty</span><span class="sxs-lookup"><span data-stu-id="35866-152">Package the component</span></span>

<span data-ttu-id="35866-153">S dokončeným `.nuspec` odkazováním na všechny soubory, které potřebujete zahrnout do [`nuget pack`](/nuget/reference/cli-reference/cli-ref-pack) balíčku, jste připraveni spustit příkaz:</span><span class="sxs-lookup"><span data-stu-id="35866-153">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the [`nuget pack`](/nuget/reference/cli-reference/cli-ref-pack) command:</span></span>

```cli
nuget pack ImageEnhancer.nuspec
```

<span data-ttu-id="35866-154">To generuje `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="35866-154">This generates `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="35866-155">Otevření tohoto souboru v nástroji, jako je [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) a rozbalení všech uzlů, uvidíte následující obsah:</span><span class="sxs-lookup"><span data-stu-id="35866-155">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![NuGet Package Explorer zobrazující balíček ImageEnhancer](media/UWP-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="35866-157">Soubor `.nupkg` je pouze soubor ZIP s jinou příponou.</span><span class="sxs-lookup"><span data-stu-id="35866-157">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="35866-158">Můžete také prozkoumat obsah balíčku, `.nupkg` `.zip`pak změnou na , ale nezapomeňte obnovit rozšíření před odesláním balíček nuget.org.</span><span class="sxs-lookup"><span data-stu-id="35866-158">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="35866-159">Chcete-li balíček zpřístupnit ostatním [vývojářům,](../nuget-org/publish-a-package.md)postupujte podle pokynů k části Publikovat balíček .</span><span class="sxs-lookup"><span data-stu-id="35866-159">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="35866-160">Související témata</span><span class="sxs-lookup"><span data-stu-id="35866-160">Related topics</span></span>

- [<span data-ttu-id="35866-161">Odkaz na odkaz .nuspec</span><span class="sxs-lookup"><span data-stu-id="35866-161">.nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="35866-162">Balíčky symbolů</span><span class="sxs-lookup"><span data-stu-id="35866-162">Symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="35866-163">Správa verzí balíčku</span><span class="sxs-lookup"><span data-stu-id="35866-163">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="35866-164">Podpora více verzí rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="35866-164">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="35866-165">Zahrnout rekvizity a cíle MSBuild do balíčku</span><span class="sxs-lookup"><span data-stu-id="35866-165">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="35866-166">Vytváření lokalizovaných balíčků</span><span class="sxs-lookup"><span data-stu-id="35866-166">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
