---
title: "Vytvoření balíčků NuGet standardní .NET s Visual Studiem 2015 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 29b3bceb-0f35-4cdd-bbc3-a04eb823164c
description: "Návod začátku do konce, vytváření balíčků NuGet pro rozhraní .NET standardní pomocí nástroje NuGet 3.x a Visual Studio 2015."
keywords: "Vytvoření balíčku, .NET Standard balíčky, .NET Standard mapování tabulky"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e02888bf552997afe25e967f13e021e78e40d48d
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/05/2018
---
# <a name="create-net-standard-packages-with-visual-studio-2015"></a><span data-ttu-id="df900-104">Vytvoření balíčků .NET Standard s Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="df900-104">Create .NET Standard packages with Visual Studio 2015</span></span>

<span data-ttu-id="df900-105">*Platí pro NuGet 3.x. V tématu [vytvořit .NET standardní balíčky s Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) pro práci s NuGet 4.x+.*</span><span class="sxs-lookup"><span data-stu-id="df900-105">*Applies to NuGet 3.x. See [Create .NET Standard Packages with Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) for working with NuGet 4.x+.*</span></span>

<span data-ttu-id="df900-106">[Standardní knihovny .NET](/dotnet/articles/standard/library) je formální specifikaci rozhraní API technologie .NET by měla být k dispozici pro všechny moduly runtime rozhraní .NET, tím větší jednotnost vytváří v ekosystému .NET.</span><span class="sxs-lookup"><span data-stu-id="df900-106">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="df900-107">Standardní knihovny .NET definuje jednotnou sadu BCL (základní třída knihovna) rozhraní API pro všechny platformy .NET implementovat, nezávisle na zatížení.</span><span class="sxs-lookup"><span data-stu-id="df900-107">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="df900-108">Ji umožňuje vývojářům vytvářet PCLs, které jsou použitelné pro všechny moduly runtime rozhraní .NET, a snižuje, pokud není eliminuje direktivy specifické pro platformu Podmíněná kompilace v sdíleného kódu.</span><span class="sxs-lookup"><span data-stu-id="df900-108">It enables developers to produce PCLs that are usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="df900-109">Tato příručka vás provede procesem vytvoření balíčku nuget cílení na rozhraní .NET standardní knihovně 1,4.</span><span class="sxs-lookup"><span data-stu-id="df900-109">This guide will walk you through creating a nuget package targeting .NET Standard Library 1.4.</span></span> <span data-ttu-id="df900-110">To bude fungovat přes rozhraní .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core a Mono nebo Xamarin.</span><span class="sxs-lookup"><span data-stu-id="df900-110">This will work across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="df900-111">Podrobnosti najdete v tématu [.NET Standard mapovací tabulku](#net-standard-mapping-table) dál v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="df900-111">For details, see the [.NET Standard mapping table](#net-standard-mapping-table) later in this topic.</span></span>

1. [<span data-ttu-id="df900-112">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="df900-112">Pre-requisites</span></span>](#pre-requisites)
1. [<span data-ttu-id="df900-113">Vytvoření projektu knihovny tříd</span><span class="sxs-lookup"><span data-stu-id="df900-113">Create the class library project</span></span>](#create-the-class-library-project)
1. [<span data-ttu-id="df900-114">Vytvářet a aktualizovat soubor s příponou .nuspec</span><span class="sxs-lookup"><span data-stu-id="df900-114">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="df900-115">Balíček součásti</span><span class="sxs-lookup"><span data-stu-id="df900-115">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="df900-116">Další možnosti</span><span class="sxs-lookup"><span data-stu-id="df900-116">Additional options</span></span>](#additional-options)
1. [<span data-ttu-id="df900-117">.NET standard mapování tabulky</span><span class="sxs-lookup"><span data-stu-id="df900-117">.NET Standard mapping table</span></span>](#net-standard-mapping-table)
1. [<span data-ttu-id="df900-118">Související témata</span><span class="sxs-lookup"><span data-stu-id="df900-118">Related topics</span></span>](#related-topics)


## <a name="pre-requisites"></a><span data-ttu-id="df900-119">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="df900-119">Pre-requisites</span></span>

1. <span data-ttu-id="df900-120">Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="df900-120">Visual Studio 2015.</span></span> <span data-ttu-id="df900-121">Instalaci edice Community zdarma z [visualstudio.com](https://www.visualstudio.com/); samozřejmě můžete taky edice Professional a Enterprise.</span><span class="sxs-lookup"><span data-stu-id="df900-121">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span>
1. <span data-ttu-id="df900-122">.NET core: Instalace .NET Core společně s šablony a dalších nástrojů pro Visual Studio 2015 z [https://go.microsoft.com/fwlink/?LinkId=824849](https://go.microsoft.com/fwlink/?LinkId=824849).</span><span class="sxs-lookup"><span data-stu-id="df900-122">.NET Core: Install .NET Core along with templates and other tools for Visual Studio 2015 from [https://go.microsoft.com/fwlink/?LinkId=824849](https://go.microsoft.com/fwlink/?LinkId=824849).</span></span>
1. <span data-ttu-id="df900-123">Rozhraní příkazového řádku NuGet.</span><span class="sxs-lookup"><span data-stu-id="df900-123">NuGet CLI.</span></span> <span data-ttu-id="df900-124">Stáhněte si nejnovější verzi nuget.exe z [nuget.org/downloads](https://nuget.org/downloads), ukládání do umístění podle vaší volby.</span><span class="sxs-lookup"><span data-stu-id="df900-124">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="df900-125">Pak přidejte tohoto umístění do vaší proměnné prostředí PATH, pokud již není.</span><span class="sxs-lookup"><span data-stu-id="df900-125">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="df900-126">nuget.exe je že nástroj příkazového řádku, není instalační program, takže je nutné z prohlížeče namísto spuštění ho uložte stažený soubor.</span><span class="sxs-lookup"><span data-stu-id="df900-126">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>



## <a name="create-the-class-library-project"></a><span data-ttu-id="df900-127">Vytvoření projektu knihovny tříd</span><span class="sxs-lookup"><span data-stu-id="df900-127">Create the class library project</span></span>

1. <span data-ttu-id="df900-128">V sadě Visual Studio **soubor > Nový > projekt**, rozbalte **Visual C# > Windows** uzlu, vyberte **knihovny tříd (přenositelností)**, změňte název na AppLogger a klikněte na tlačítko OK.</span><span class="sxs-lookup"><span data-stu-id="df900-128">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and click OK.</span></span>

    ![Vytvoření nového projektu knihovny tříd](media/NetStandard-NewProject.png)

1. <span data-ttu-id="df900-130">V **přidat Přenosná knihovna tříd** dialog, který se zobrazí, vyberte `.NET Framework 4.6` a `ASP.NET Core 1.0` možnosti.</span><span class="sxs-lookup"><span data-stu-id="df900-130">In the **Add Portable Class Library** dialog that appears, select the `.NET Framework 4.6` and `ASP.NET Core 1.0` options.</span></span>
1. <span data-ttu-id="df900-131">Klikněte pravým tlačítkem myši `AppLogger (Portable)` v Průzkumníku řešení, vyberte **vlastnosti**, vyberte **knihovny** a potom klikněte na tlačítko **Standard platformy cílové rozhraní .NET** v **Cílení** části.</span><span class="sxs-lookup"><span data-stu-id="df900-131">Right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then click **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="df900-132">Zobrazí se výzva k potvrzení, po kterém můžete vybrat `.NET Standard 1.4` v rozevíracím seznamu:</span><span class="sxs-lookup"><span data-stu-id="df900-132">This will prompt for confirmation, after which you can select `.NET Standard 1.4` from the drop down:</span></span>

    ![Nastavení cíl na standardní 1.4 rozhraní .NET](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="df900-134">Klikněte na **sestavení** změňte **konfigurace** k `Release`a zaškrtněte políčko pro **souborů dokumentace XML**.</span><span class="sxs-lookup"><span data-stu-id="df900-134">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>
1. <span data-ttu-id="df900-135">Přidáte kód pro součásti, například:</span><span class="sxs-lookup"><span data-stu-id="df900-135">Add your code to the component, for example:</span></span>

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log");
            }
        }
    }
    ```

1. <span data-ttu-id="df900-136">Sestavení projektu (s konfigurací verzi) a zkontrolujte, že jsou ve složce bin\Release vytváří soubory DLL a XML.</span><span class="sxs-lookup"><span data-stu-id="df900-136">Build the project (with the Release configuration) and check that DLL and XML files are produced within the bin\Release folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="df900-137">Vytvářet a aktualizovat soubor s příponou .nuspec</span><span class="sxs-lookup"><span data-stu-id="df900-137">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="df900-138">Otevřete příkazový řádek, přejděte do složky obsahující `AppLogg.csproj` složky (o jednu úroveň pod where `.sln` soubor), a spusťte NuGet `spec` příkaz pro vytvoření počáteční `AppLogger.nuspec` souboru:</span><span class="sxs-lookup"><span data-stu-id="df900-138">Open a command prompt, navigate to the folder containing `AppLogg.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

```
nuget spec
```

1. <span data-ttu-id="df900-139">Otevřete `AppLogger.nuspec` v editoru a aktualizovat ji tak, aby odpovídala následující, nahraďte vaše_jméno odpovídající hodnotu.</span><span class="sxs-lookup"><span data-stu-id="df900-139">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="df900-140">`<id>` Hodnotu, konkrétně musí být jedinečný v rámci nuget.org (viz zásady vytváření názvů, které jsou popsané v [vytváření balíčku](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="df900-140">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="df900-141">Všimněte si také, zda je nutné také aktualizovat autora a popis značky nebo budete dojde k chybě během kroku okolních.</span><span class="sxs-lookup"><span data-stu-id="df900-141">Also note that you must also update the author and description tags or you'll get an error during the packing step.</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>AppLogger.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>AppLogger</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome application logging utility</description>
    <releaseNotes>First release</releaseNotes>
    <copyright>Copyright 2016 (c) Contoso Corporation. All rights reserved.</copyright>
    <tags>logger logging logs</tags>
    </metadata>
</package>
```

1. <span data-ttu-id="df900-142">Přidat odkaz na sestavení, které chcete `.nuspec` souboru, a to knihovně DLL a soubor IntelliSense XML:</span><span class="sxs-lookup"><span data-stu-id="df900-142">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="df900-143">Klikněte pravým tlačítkem na řešení a vyberte **sestavit řešení** ke generování všechny soubory pro balíček.</span><span class="sxs-lookup"><span data-stu-id="df900-143">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>


## <a name="package-the-component"></a><span data-ttu-id="df900-144">Balíček součásti</span><span class="sxs-lookup"><span data-stu-id="df900-144">Package the component</span></span>

<span data-ttu-id="df900-145">S dokončené `.nuspec` odkazující na všechny soubory, které je potřeba zahrnout do balíčku, jste připraveni ke spuštění `pack` příkaz:</span><span class="sxs-lookup"><span data-stu-id="df900-145">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```
nuget pack AppLogger.nuspec
```

<span data-ttu-id="df900-146">Tím se vygeneruje `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="df900-146">This will generate `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="df900-147">Otevření tohoto souboru v nástroje, jako [Explorer balíček NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) a rozšiřování všechny uzly, zobrazí se následující obsah:</span><span class="sxs-lookup"><span data-stu-id="df900-147">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you'll see the following contents:</span></span>

![Průzkumník balíček NuGet zobrazující AppLogger balíčku](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="df900-149">A `.nupkg` soubor je právě soubor ZIP s jiné rozšíření.</span><span class="sxs-lookup"><span data-stu-id="df900-149">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="df900-150">Můžete také zkontrolovat obsah balíčku, potom změnou `.nupkg` k `.zip`, ale nezapomeňte obnovit rozšíření před balíčku se nahrávají na nuget.org.</span><span class="sxs-lookup"><span data-stu-id="df900-150">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="df900-151">Pokud chcete zpřístupnit vašeho balíčku jinými vývojáři, postupujte podle pokynů [publikování balíčku](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="df900-151">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="df900-152">Všimněte si, že `pack` vyžaduje Mono 4.4.2 na Mac OS X a nefunguje v systémech Linux.</span><span class="sxs-lookup"><span data-stu-id="df900-152">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="df900-153">V systému Mac, je nutné také převést Windows názvy cest v `.nuspec` souboru do cesty formátu UNIX.</span><span class="sxs-lookup"><span data-stu-id="df900-153">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="additional-options"></a><span data-ttu-id="df900-154">Další možnosti</span><span class="sxs-lookup"><span data-stu-id="df900-154">Additional options</span></span>

<span data-ttu-id="df900-155">V následujících částech přejít do další možnosti pro vytvoření balíčku NuGet:</span><span class="sxs-lookup"><span data-stu-id="df900-155">The following sections go into additional options for NuGet package creation:</span></span>

- [<span data-ttu-id="df900-156">Deklarování závislosti</span><span class="sxs-lookup"><span data-stu-id="df900-156">Declaring dependencies</span></span>](#declaring-dependencies)
- [<span data-ttu-id="df900-157">Podpora více cílové rozhraní</span><span class="sxs-lookup"><span data-stu-id="df900-157">Supporting multiple target frameworks</span></span>](#supporting-multiple-target-frameworks)
- [<span data-ttu-id="df900-158">Přidání cíle a props pro nástroje MSBuild</span><span class="sxs-lookup"><span data-stu-id="df900-158">Adding targets and props for MSBuild</span></span>](#adding-targets-and-props-for-msbuild)
- [<span data-ttu-id="df900-159">Vytvoření lokalizovaných balíčků</span><span class="sxs-lookup"><span data-stu-id="df900-159">Creating localized packages</span></span>](#creating-localized-packages)
- [<span data-ttu-id="df900-160">Přidání soubor readme</span><span class="sxs-lookup"><span data-stu-id="df900-160">Adding a readme</span></span>](#adding-a-readme)

### <a name="declaring-dependencies"></a><span data-ttu-id="df900-161">Deklarování závislosti</span><span class="sxs-lookup"><span data-stu-id="df900-161">Declaring dependencies</span></span>

<span data-ttu-id="df900-162">Pokud máte všechny závislosti na dalších balíčcích NuGet, programů v seznamu `<dependencies>` element s `<group>` elementy.</span><span class="sxs-lookup"><span data-stu-id="df900-162">If you have any dependencies on other NuGet packages, list those in the `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="df900-163">Chcete-li například závislost na NewtonSoft.Json 8.0.3 deklarovat nebo vyšší, přidejte následující:</span><span class="sxs-lookup"><span data-stu-id="df900-163">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="df900-164">Syntaxe *verze* atribut zde označuje, že verze 8.0.3 nebo novější je přijatelná.</span><span class="sxs-lookup"><span data-stu-id="df900-164">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="df900-165">Zadejte jinou verzi rozsahy, najdete v tématu [Správa verzí balíčku](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="df900-165">To specify different version ranges, refer to [Package versioning](../reference/package-versioning.md).</span></span>

### <a name="supporting-multiple-target-frameworks"></a><span data-ttu-id="df900-166">Podpora více cílové rozhraní</span><span class="sxs-lookup"><span data-stu-id="df900-166">Supporting multiple target frameworks</span></span>

<span data-ttu-id="df900-167">Předpokládejme, že chcete využít výhod rozhraní API v rozhraní .NET Framework 4.6.2, který není k dispozici v rozhraní .NET standardní 1.4.</span><span class="sxs-lookup"><span data-stu-id="df900-167">Suppose you'd like to take advantage of an API in .NET Framework 4.6.2 that is not available in .NET Standard 1.4.</span></span> <span data-ttu-id="df900-168">K tomuto účelu, budete nejprve muset Ujistěte se, že knihovny zkompiluje pro .NET 4.6.2 pomocí Podmíněná kompilace nebo sdílených projektů.</span><span class="sxs-lookup"><span data-stu-id="df900-168">To do this, you'll first need to make sure the library compiles for .NET 4.6.2 by using conditional compilation or shared projects.</span></span> <span data-ttu-id="df900-169">(V sadě Visual Studio, můžete vytvořit projekt NetCore, přidejte rozhraní výběru oddílu více framework a následně vytvořit.) Pak vytvoříte balíček použití jednoduchého postupu založené na konvenci directory pracovní následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="df900-169">(In Visual Studio, you can create a NetCore project, add the framework of choice to the multiple framework section, and then build.) Then you create the package using the simple convention-based working directory technique as follows:</span></span>

1. <span data-ttu-id="df900-170">V projektu kořenovou složku obsahující vaše `.nuspec` souboru, vytvořte složku s názvem `lib`.</span><span class="sxs-lookup"><span data-stu-id="df900-170">In the project's root folder containing your `.nuspec` file, create a folder named `lib`.</span></span>
1. <span data-ttu-id="df900-171">Uvnitř `lib`, vytvořte složky pro každou platformu, které chcete podporovat:</span><span class="sxs-lookup"><span data-stu-id="df900-171">Inside `lib`, create folders for each platform you want to support:</span></span>

        \lib
            \netstandard1.4
                \AppLogger.dll
            \net462
                \AppLogger.dll

1. <span data-ttu-id="df900-172">V `.nuspec` soubor, přidejte `files` pod uzlem `package` uzlu a odkazovat na soubory v `lib` pomocí zástupných znaků.</span><span class="sxs-lookup"><span data-stu-id="df900-172">In the `.nuspec` file, add a `files` node under the `package` node and refer to the files in `lib` using wildcards.</span></span> <span data-ttu-id="df900-173">**Poznámka:** Token náhrady nejsou podporovány s přístupem založené na konvenci pracovní adresář, takže je nahradit literálových hodnot:</span><span class="sxs-lookup"><span data-stu-id="df900-173">**Note:** Token replacements are not supported with the convention-based working directory approach, so replace them with literal values:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>AppLogger.YOUR_NAME</id>
        <version>1.0.0.0</version>
        <title>AppLogger</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release.</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>logger logging logs</tags>
        </metadata>
        <files>
            <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. <span data-ttu-id="df900-174">Vytvořit balíček znovu s použitím `nuget pack AppLogger.spec`.</span><span class="sxs-lookup"><span data-stu-id="df900-174">Create the package again using `nuget pack AppLogger.spec`.</span></span>

<span data-ttu-id="df900-175">Další podrobnosti o použití Tato technika, najdete v části [podpora více verzí rozhraní .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)</span><span class="sxs-lookup"><span data-stu-id="df900-175">For more details on using this technique, see [Supporting Multiple .NET Framework Versions](../create-packages/supporting-multiple-target-frameworks.md)</span></span>

### <a name="adding-targets-and-props-for-msbuild"></a><span data-ttu-id="df900-176">Přidání cíle a props pro nástroje MSBuild</span><span class="sxs-lookup"><span data-stu-id="df900-176">Adding targets and props for MSBuild</span></span>

<span data-ttu-id="df900-177">V některých případech můžete chtít přidat vlastní sestavovací cíle nebo vlastnosti v projektech, které využívají vašeho balíčku, jako je například spuštění vlastního nástroje nebo procesu během vytváření sestavení.</span><span class="sxs-lookup"><span data-stu-id="df900-177">In some cases you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="df900-178">To uděláte tak, že přidáte soubory v `\build` složky, jak je popsáno v následujících krocích.</span><span class="sxs-lookup"><span data-stu-id="df900-178">You do this by adding files in a `\build` folder as described in the steps below.</span></span> <span data-ttu-id="df900-179">Při instalaci balíčku NuGet se soubory \build přidá MSBuild element v souboru projektu odkazující na soubory .targets a props.</span><span class="sxs-lookup"><span data-stu-id="df900-179">When NuGet installs a package with \build files, it adds an MSBuild element in the project file pointing to the .targets and .props files.</span></span>

> [!Note]
> <span data-ttu-id="df900-180">Při použití `project.json`, cíle nejsou přidány do projektu, ale jsou k dispozici prostřednictvím `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="df900-180">When using `project.json`, targets are not added to the project but are made available through the `project.lock.json`.</span></span>


1. <span data-ttu-id="df900-181">V projektu složku obsahující vaše `.nuspec` souboru, vytvořte složku s názvem `build`.</span><span class="sxs-lookup"><span data-stu-id="df900-181">In the project folder containing the your `.nuspec` file, create a folder named `build`.</span></span>
1. <span data-ttu-id="df900-182">Uvnitř `build`, vytváření složek pro všechny podporované a v rámci ty umístit vaše `.targets` a `.props` soubory:</span><span class="sxs-lookup"><span data-stu-id="df900-182">Inside `build`, create folders for each supported, and within those place your `.targets` and `.props` files:</span></span>

        \build
            \netstandard1.4
                \AppLogger.props
                \AppLogger.targets
            \net462
                \AppLogger.props
                \AppLogger.targets

1. <span data-ttu-id="df900-183">V `.nuspec` soubor, přidejte `files` pod uzlem `package` uzlu a odkazovat na soubory v `build` pomocí zástupných znaků.</span><span class="sxs-lookup"><span data-stu-id="df900-183">In the `.nuspec` file, add a `files` node under the `package` node and refer to the files in `build` using wildcards.</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>...
        </metadata>
        <files>
            <file src="build\**" target="build" />
        </files>
    </package>
    ```

1. <span data-ttu-id="df900-184">Vytvořit balíček znovu s použitím `nuget pack AppLogger.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="df900-184">Create the package again using `nuget pack AppLogger.nuspec`.</span></span>

<span data-ttu-id="df900-185">Další podrobnosti najdete v části [zahrnují MSBuild props a cíle v balíčku](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package).</span><span class="sxs-lookup"><span data-stu-id="df900-185">For additional details, refer to [Include MSBuild props and targets in a package](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package).</span></span>


### <a name="creating-localized-packages"></a><span data-ttu-id="df900-186">Vytvoření lokalizovaných balíčků</span><span class="sxs-lookup"><span data-stu-id="df900-186">Creating localized packages</span></span>

<span data-ttu-id="df900-187">Pokud chcete vytvořit lokalizované verze knihovny, můžete vytvořit samostatné balíčky pro různá národní prostředí nebo zahrnout lokalizovaný prostředek sestavení v rámci jednoho balíčku.</span><span class="sxs-lookup"><span data-stu-id="df900-187">To create localized versions of your library, you can either create separate packages for different locales, or include localized resource assemblies within a single package.</span></span> <span data-ttu-id="df900-188">Tady je postup pozdější přístup, němčiny a Italština:</span><span class="sxs-lookup"><span data-stu-id="df900-188">Here's how to do the latter approach for German and Italian:</span></span>

1. <span data-ttu-id="df900-189">V rámci každé cílové složce framework pod `lib`, vytvořte složky pro každý podporovaný jazyk jiné než anglické výchozí.</span><span class="sxs-lookup"><span data-stu-id="df900-189">Within each target framework folder under `lib`, create folders for each supported language other than the English default.</span></span> <span data-ttu-id="df900-190">V uvedených složkách můžete umístit prostředek sestavení a lokalizované soubory IntelliSense XML.</span><span class="sxs-lookup"><span data-stu-id="df900-190">In these folders you can place resource assemblies  and localized IntelliSense XML files.</span></span> <span data-ttu-id="df900-191">Příklad:</span><span class="sxs-lookup"><span data-stu-id="df900-191">For example:</span></span>

        lib
        ├───netstandard1.4
        │   │   AppLogger.dll
        │   │   AppLogger.xml
        │   │
        │   ├───de
        │   │       AppLogger.resources.dll
        │   │       AppLogger.xml
        │   │
        │   └───it
        │           AppLogger.resources.dll
        │           AppLogger.xml
        └───net462
            │   AppLogger.dll
            │   AppLogger.xml
            │
            ├───de
            │       AppLogger.resources.dll
            │       AppLogger.xml
            │
            └───it
                    AppLogger.resources.dll
                    AppLogger.xml

1. <span data-ttu-id="df900-192">V `.nuspec` souboru, odkazují tyto soubory v `<files>` uzlu:</span><span class="sxs-lookup"><span data-stu-id="df900-192">In the `.nuspec` file, reference these files in the `<files>` node:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>...
        </metadata>
        <files>
        <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. <span data-ttu-id="df900-193">Vytvořit balíček znovu s použitím `nuget pack AppLogger.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="df900-193">Create the package again using `nuget pack AppLogger.nuspec`.</span></span>


### <a name="adding-a-readme"></a><span data-ttu-id="df900-194">Přidání soubor readme</span><span class="sxs-lookup"><span data-stu-id="df900-194">Adding a readme</span></span>

<span data-ttu-id="df900-195">Pokud zahrnete `readme.txt` souboru v kořenu balíčku, Visual Studio se zobrazí se při instalaci balíčku přímo.</span><span class="sxs-lookup"><span data-stu-id="df900-195">When you include a `readme.txt` file in the root of the package, Visual Studio will display it when the package is installed directly.</span></span>

> [!Note]
> <span data-ttu-id="df900-196">Soubory Readme nejsou zobrazeny pro balíčky, které se instalují jako závislost, nebo pro projekty .NET Core.</span><span class="sxs-lookup"><span data-stu-id="df900-196">Readme files are not shown for packages that are installed as a dependency, or for .NET Core projects.</span></span>


<span data-ttu-id="df900-197">Chcete-li to provést, vytvořte vaše `readme.txt` souboru, umístěte do kořenové složky projektu a najdete ji v `.nuspec` souboru:</span><span class="sxs-lookup"><span data-stu-id="df900-197">To do this, create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>...
    </metadata>
    <files>
    <file src="readme.txt" target="" />
    </files>
</package>
```


## <a name="net-standard-mapping-table"></a><span data-ttu-id="df900-198">.NET standard mapování tabulky</span><span class="sxs-lookup"><span data-stu-id="df900-198">.NET Standard mapping table</span></span>

|<span data-ttu-id="df900-199">Název platformy</span><span class="sxs-lookup"><span data-stu-id="df900-199">Platform Name</span></span> |<span data-ttu-id="df900-200">Alias</span><span class="sxs-lookup"><span data-stu-id="df900-200">Alias</span></span>|
|--------------|-----|
|<span data-ttu-id="df900-201">Standardní rozhraní .NET</span><span class="sxs-lookup"><span data-stu-id="df900-201">.NET Standard</span></span> | <span data-ttu-id="df900-202">monikerů netstandard</span><span class="sxs-lookup"><span data-stu-id="df900-202">netstandard</span></span>| <span data-ttu-id="df900-203">1.0</span><span class="sxs-lookup"><span data-stu-id="df900-203">1.0</span></span>| <span data-ttu-id="df900-204">1.1</span><span class="sxs-lookup"><span data-stu-id="df900-204">1.1</span></span>| <span data-ttu-id="df900-205">1.2</span><span class="sxs-lookup"><span data-stu-id="df900-205">1.2</span></span>| <span data-ttu-id="df900-206">1.3</span><span class="sxs-lookup"><span data-stu-id="df900-206">1.3</span></span>| <span data-ttu-id="df900-207">1.4</span><span class="sxs-lookup"><span data-stu-id="df900-207">1.4</span></span>| <span data-ttu-id="df900-208">1.5</span><span class="sxs-lookup"><span data-stu-id="df900-208">1.5</span></span>| <span data-ttu-id="df900-209">1.6</span><span class="sxs-lookup"><span data-stu-id="df900-209">1.6</span></span>|
|<span data-ttu-id="df900-210">.NET Core</span><span class="sxs-lookup"><span data-stu-id="df900-210">.NET Core</span></span> | <span data-ttu-id="df900-211">netcoreapp</span><span class="sxs-lookup"><span data-stu-id="df900-211">netcoreapp</span></span>| <span data-ttu-id="df900-212">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="df900-212">&#x2192;</span></span>| <span data-ttu-id="df900-213">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="df900-213">&#x2192;</span></span>| <span data-ttu-id="df900-214">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="df900-214">&#x2192;</span></span>| <span data-ttu-id="df900-215">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="df900-215">&#x2192;</span></span>| <span data-ttu-id="df900-216">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="df900-216">&#x2192;</span></span>| <span data-ttu-id="df900-217">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="df900-217">&#x2192;</span></span>| <span data-ttu-id="df900-218">1.0</span><span class="sxs-lookup"><span data-stu-id="df900-218">1.0</span></span>|
|<span data-ttu-id="df900-219">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="df900-219">.NET Framework</span></span>| <span data-ttu-id="df900-220">NET</span><span class="sxs-lookup"><span data-stu-id="df900-220">net</span></span>| <span data-ttu-id="df900-221">4.5</span><span class="sxs-lookup"><span data-stu-id="df900-221">4.5</span></span>| <span data-ttu-id="df900-222">4.5.1</span><span class="sxs-lookup"><span data-stu-id="df900-222">4.5.1</span></span>| <span data-ttu-id="df900-223">4.6</span><span class="sxs-lookup"><span data-stu-id="df900-223">4.6</span></span>| <span data-ttu-id="df900-224">4.6.1</span><span class="sxs-lookup"><span data-stu-id="df900-224">4.6.1</span></span>| <span data-ttu-id="df900-225">4.6.2</span><span class="sxs-lookup"><span data-stu-id="df900-225">4.6.2</span></span>| <span data-ttu-id="df900-226">4.6.3</span><span class="sxs-lookup"><span data-stu-id="df900-226">4.6.3</span></span>|
|<span data-ttu-id="df900-227">Platformy mono nebo Xamarin</span><span class="sxs-lookup"><span data-stu-id="df900-227">Mono/Xamarin Platforms</span></span>| <span data-ttu-id="df900-228">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="df900-228">&#x2192;</span></span>| <span data-ttu-id="df900-229">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="df900-229">&#x2192;</span></span>| <span data-ttu-id="df900-230">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="df900-230">&#x2192;</span></span>| <span data-ttu-id="df900-231">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="df900-231">&#x2192;</span></span>| <span data-ttu-id="df900-232">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="df900-232">&#x2192;</span></span>| <span data-ttu-id="df900-233">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="df900-233">&#x2192;</span></span>|
|<span data-ttu-id="df900-234">Univerzální platforma pro Windows</span><span class="sxs-lookup"><span data-stu-id="df900-234">Universal Windows Platform</span></span>| <span data-ttu-id="df900-235">uap</span><span class="sxs-lookup"><span data-stu-id="df900-235">uap</span></span>| <span data-ttu-id="df900-236">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="df900-236">&#x2192;</span></span>| <span data-ttu-id="df900-237">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="df900-237">&#x2192;</span></span>| <span data-ttu-id="df900-238">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="df900-238">&#x2192;</span></span>| <span data-ttu-id="df900-239">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="df900-239">&#x2192;</span></span>|<span data-ttu-id="df900-240">10.0</span><span class="sxs-lookup"><span data-stu-id="df900-240">10.0</span></span>|
|<span data-ttu-id="df900-241">Windows</span><span class="sxs-lookup"><span data-stu-id="df900-241">Windows</span></span>| <span data-ttu-id="df900-242">Win</span><span class="sxs-lookup"><span data-stu-id="df900-242">win</span></span>| <span data-ttu-id="df900-243">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="df900-243">&#x2192;</span></span>| <span data-ttu-id="df900-244">8.0</span><span class="sxs-lookup"><span data-stu-id="df900-244">8.0</span></span>| <span data-ttu-id="df900-245">8.1</span><span class="sxs-lookup"><span data-stu-id="df900-245">8.1</span></span>|
|<span data-ttu-id="df900-246">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="df900-246">Windows Phone</span></span>| <span data-ttu-id="df900-247">WPA</span><span class="sxs-lookup"><span data-stu-id="df900-247">wpa</span></span>| <span data-ttu-id="df900-248">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="df900-248">&#x2192;</span></span>| <span data-ttu-id="df900-249">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="df900-249">&#x2192;</span></span>|<span data-ttu-id="df900-250">8.1</span><span class="sxs-lookup"><span data-stu-id="df900-250">8.1</span></span>|
|<span data-ttu-id="df900-251">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="df900-251">Windows Phone Silverlight</span></span>| <span data-ttu-id="df900-252">webové části</span><span class="sxs-lookup"><span data-stu-id="df900-252">wp</span></span>| <span data-ttu-id="df900-253">8.0</span><span class="sxs-lookup"><span data-stu-id="df900-253">8.0</span></span>|



## <a name="related-topics"></a><span data-ttu-id="df900-254">Související témata</span><span class="sxs-lookup"><span data-stu-id="df900-254">Related topics</span></span>

- [<span data-ttu-id="df900-255">Odkaz na soubor Nuspec</span><span class="sxs-lookup"><span data-stu-id="df900-255">Nuspec Reference</span></span>](../schema/nuspec.md)
- [<span data-ttu-id="df900-256">Symbol balíčky</span><span class="sxs-lookup"><span data-stu-id="df900-256">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="df900-257">Správa verzí balíčku</span><span class="sxs-lookup"><span data-stu-id="df900-257">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="df900-258">Podpora více verzí rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="df900-258">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="df900-259">Zahrnout do balíčku nástroje MSBuild props a cíle</span><span class="sxs-lookup"><span data-stu-id="df900-259">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="df900-260">Vytvoření lokalizovaných balíčků</span><span class="sxs-lookup"><span data-stu-id="df900-260">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="df900-261">Standardní knihovny .NET dokumentaci</span><span class="sxs-lookup"><span data-stu-id="df900-261">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="df900-262">Portování do .NET Core z rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="df900-262">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
