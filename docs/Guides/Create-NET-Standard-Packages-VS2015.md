---
title: "Vytvoření balíčků NuGet standardní .NET s Visual Studiem 2015 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/02/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Návod začátku do konce, vytváření balíčků NuGet pro rozhraní .NET standardní pomocí nástroje NuGet 3.x a Visual Studio 2015."
keywords: "Vytvoření balíčku, .NET Standard balíčky, .NET Standard mapování tabulky"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: abf6a56cbc84bdd066e31e77c7883825a8456144
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2018
---
# <a name="create-net-standard-packages-with-visual-studio-2015"></a><span data-ttu-id="56f12-104">Vytvoření balíčků .NET Standard s Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="56f12-104">Create .NET Standard packages with Visual Studio 2015</span></span>

<span data-ttu-id="56f12-105">*Platí pro NuGet 3.x. V tématu [vytvoření a publikování balíčku s Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) pro práci s NuGet 4.x+.*</span><span class="sxs-lookup"><span data-stu-id="56f12-105">*Applies to NuGet 3.x. See [Create and publish a package with Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) for working with NuGet 4.x+.*</span></span>

<span data-ttu-id="56f12-106">[Standardní knihovny .NET](/dotnet/articles/standard/library) je formální specifikaci rozhraní API technologie .NET by měla být k dispozici pro všechny moduly runtime rozhraní .NET, tím větší jednotnost vytváří v ekosystému .NET.</span><span class="sxs-lookup"><span data-stu-id="56f12-106">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="56f12-107">Standardní knihovny .NET definuje jednotnou sadu BCL (základní třída knihovna) rozhraní API pro všechny platformy .NET implementovat, nezávisle na zatížení.</span><span class="sxs-lookup"><span data-stu-id="56f12-107">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="56f12-108">Umožňuje vývojářům vytvářet kód, který je použitelný přes všechny moduly runtime rozhraní .NET a snižuje není eliminuje direktivy specifické pro platformu Podmíněná kompilace v sdíleného kódu.</span><span class="sxs-lookup"><span data-stu-id="56f12-108">It enables developers to produce code that is usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="56f12-109">Tento průvodce vás provede procesem vytváření balíčku NuGet cílení .NET standardní knihovny 1.4.</span><span class="sxs-lookup"><span data-stu-id="56f12-109">This guide walks you through creating a NuGet package targeting .NET Standard Library 1.4.</span></span> <span data-ttu-id="56f12-110">Tuto knihovnu funguje napříč rozhraní .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core a Mono nebo Xamarin.</span><span class="sxs-lookup"><span data-stu-id="56f12-110">Such a library works across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="56f12-111">Podrobnosti najdete v tématu [.NET Standard mapovací tabulku](#net-standard-mapping-table) dál v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="56f12-111">For details, see the [.NET Standard mapping table](#net-standard-mapping-table) later in this topic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="56f12-112">Požadavky</span><span class="sxs-lookup"><span data-stu-id="56f12-112">Prerequisites</span></span>

1. <span data-ttu-id="56f12-113">Visual Studio 2015 Update 3</span><span class="sxs-lookup"><span data-stu-id="56f12-113">Visual Studio 2015 Update 3</span></span>
1. [<span data-ttu-id="56f12-114">.NET core SDK</span><span class="sxs-lookup"><span data-stu-id="56f12-114">.NET Core SDK</span></span>](https://www.microsoft.com/net/download/)
1. <span data-ttu-id="56f12-115">Rozhraní příkazového řádku NuGet.</span><span class="sxs-lookup"><span data-stu-id="56f12-115">NuGet CLI.</span></span> <span data-ttu-id="56f12-116">Stáhněte si nejnovější verzi nuget.exe z [nuget.org/downloads](https://nuget.org/downloads), ukládání do umístění podle vaší volby.</span><span class="sxs-lookup"><span data-stu-id="56f12-116">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="56f12-117">Pak přidejte tohoto umístění do vaší proměnné prostředí PATH, pokud již není.</span><span class="sxs-lookup"><span data-stu-id="56f12-117">Then add that location to your PATH environment variable if it isn't already.</span></span>

    > [!Note]
    > <span data-ttu-id="56f12-118">nuget.exe je že nástroj příkazového řádku, není instalační program, takže je nutné z prohlížeče namísto spuštění ho uložte stažený soubor.</span><span class="sxs-lookup"><span data-stu-id="56f12-118">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-class-library-project"></a><span data-ttu-id="56f12-119">Vytvoření projektu knihovny tříd</span><span class="sxs-lookup"><span data-stu-id="56f12-119">Create the class library project</span></span>

1. <span data-ttu-id="56f12-120">V sadě Visual Studio **soubor > Nový > projekt**, rozbalte **Visual C# > Windows** uzlu, vyberte **knihovny tříd (přenositelností)**, změňte název na AppLogger a klikněte na tlačítko OK.</span><span class="sxs-lookup"><span data-stu-id="56f12-120">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and click OK.</span></span>

    ![Vytvoření nového projektu knihovny tříd](media/NetStandard-NewProject.png)

1. <span data-ttu-id="56f12-122">V **přidat Přenosná knihovna tříd** dialog, který se zobrazí, vyberte `.NET Framework 4.6` a `ASP.NET Core 1.0` možnosti.</span><span class="sxs-lookup"><span data-stu-id="56f12-122">In the **Add Portable Class Library** dialog that appears, select the `.NET Framework 4.6` and `ASP.NET Core 1.0` options.</span></span>

1. <span data-ttu-id="56f12-123">Klikněte pravým tlačítkem myši `AppLogger (Portable)` v Průzkumníku řešení, vyberte **vlastnosti**, vyberte **knihovny** a potom klikněte na tlačítko **Standard platformy cílové rozhraní .NET** v **Cílení** části.</span><span class="sxs-lookup"><span data-stu-id="56f12-123">Right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then click **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="56f12-124">Zobrazí se výzva k potvrzení, po kterém můžete vybrat `.NET Standard 1.4` v rozevíracím seznamu:</span><span class="sxs-lookup"><span data-stu-id="56f12-124">This will prompt for confirmation, after which you can select `.NET Standard 1.4` from the drop down:</span></span>

    ![Nastavení cíl na standardní 1.4 rozhraní .NET](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="56f12-126">Klikněte na **sestavení** změňte **konfigurace** k `Release`a zaškrtněte políčko pro **souborů dokumentace XML**.</span><span class="sxs-lookup"><span data-stu-id="56f12-126">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>

1. <span data-ttu-id="56f12-127">Přidáte kód pro součásti, například:</span><span class="sxs-lookup"><span data-stu-id="56f12-127">Add your code to the component, for example:</span></span>

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

1. <span data-ttu-id="56f12-128">Nastavte konfiguraci na verzi, sestavte projekt a zkontrolujte, že jsou v rámci vytváří soubory DLL a XML `bin\Release` složky.</span><span class="sxs-lookup"><span data-stu-id="56f12-128">Set the configuration to Release, build the project, and check that DLL and XML files are produced within the `bin\Release` folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="56f12-129">Vytvářet a aktualizovat soubor s příponou .nuspec</span><span class="sxs-lookup"><span data-stu-id="56f12-129">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="56f12-130">Otevřete příkazový řádek, přejděte do složky obsahující `AppLogger.csproj` složky (o jednu úroveň pod where `.sln` soubor), a spusťte NuGet `spec` příkaz pro vytvoření počáteční `AppLogger.nuspec` souboru:</span><span class="sxs-lookup"><span data-stu-id="56f12-130">Open a command prompt, navigate to the folder containing `AppLogger.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="56f12-131">Otevřete `AppLogger.nuspec` v editoru a aktualizovat ji tak, aby odpovídala následující, nahraďte vaše_jméno odpovídající hodnotu.</span><span class="sxs-lookup"><span data-stu-id="56f12-131">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="56f12-132">`<id>` Hodnotu, konkrétně musí být jedinečný v rámci nuget.org (viz zásady vytváření názvů, které jsou popsané v [vytváření balíčku](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="56f12-132">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="56f12-133">Všimněte si také, zda je nutné také aktualizovat autora a popis značky nebo dojde k chybě během kroku okolních.</span><span class="sxs-lookup"><span data-stu-id="56f12-133">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
        <copyright>Copyright 2018 (c) Contoso Corporation. All rights reserved.</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

1. <span data-ttu-id="56f12-134">Přidat odkaz na sestavení, které chcete `.nuspec` souboru, a to knihovně DLL a soubor IntelliSense XML:</span><span class="sxs-lookup"><span data-stu-id="56f12-134">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="56f12-135">Klikněte pravým tlačítkem na řešení a vyberte **sestavit řešení** ke generování všechny soubory pro balíček.</span><span class="sxs-lookup"><span data-stu-id="56f12-135">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>

### <a name="declaring-dependencies"></a><span data-ttu-id="56f12-136">Deklarování závislosti</span><span class="sxs-lookup"><span data-stu-id="56f12-136">Declaring dependencies</span></span>

<span data-ttu-id="56f12-137">Pokud máte všechny závislosti na dalších balíčcích NuGet, seznamu těch, které do manifestu `<dependencies>` element s `<group>` elementy.</span><span class="sxs-lookup"><span data-stu-id="56f12-137">If you have any dependencies on other NuGet packages, list those in the manifest's `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="56f12-138">Chcete-li například závislost na NewtonSoft.Json 8.0.3 deklarovat nebo vyšší, přidejte následující:</span><span class="sxs-lookup"><span data-stu-id="56f12-138">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="56f12-139">Syntaxe *verze* atribut zde označuje, že verze 8.0.3 nebo novější je přijatelná.</span><span class="sxs-lookup"><span data-stu-id="56f12-139">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="56f12-140">Zadejte jinou verzi rozsahy, najdete v tématu [Správa verzí balíčku](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="56f12-140">To specify different version ranges, refer to [Package versioning](../reference/package-versioning.md).</span></span>

### <a name="adding-a-readme"></a><span data-ttu-id="56f12-141">Přidání soubor readme</span><span class="sxs-lookup"><span data-stu-id="56f12-141">Adding a readme</span></span>

<span data-ttu-id="56f12-142">Vytvoření vaší `readme.txt` souboru, umístěte do kořenové složky projektu a najdete ji v `.nuspec` souboru:</span><span class="sxs-lookup"><span data-stu-id="56f12-142">Create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

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

<span data-ttu-id="56f12-143">Visual Studio zobrazení `readme.txt` při instalaci balíčku do projektu.</span><span class="sxs-lookup"><span data-stu-id="56f12-143">Visual Studio display `readme.txt` when the package is installed into a project.</span></span> <span data-ttu-id="56f12-144">Soubor se nezobrazí, pokud nainstalované do projektů .NET Core, nebo pro balíčky, které se instalují jako závislost.</span><span class="sxs-lookup"><span data-stu-id="56f12-144">The file is not shown when installed into .NET Core projects, or for packages that are installed as a dependency.</span></span>

## <a name="package-the-component"></a><span data-ttu-id="56f12-145">Balíček součásti</span><span class="sxs-lookup"><span data-stu-id="56f12-145">Package the component</span></span>

<span data-ttu-id="56f12-146">S dokončené `.nuspec` odkazující na všechny soubory, které je potřeba zahrnout do balíčku, jste připraveni ke spuštění `pack` příkaz:</span><span class="sxs-lookup"><span data-stu-id="56f12-146">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack AppLogger.nuspec
```

<span data-ttu-id="56f12-147">Tím se vygeneruje `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="56f12-147">This will generate `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="56f12-148">Otevření tohoto souboru v nástroje, jako [Explorer balíček NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) a rozšiřování všechny uzly, můžete zobrazit následující obsah:</span><span class="sxs-lookup"><span data-stu-id="56f12-148">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![Průzkumník balíček NuGet zobrazující AppLogger balíčku](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="56f12-150">A `.nupkg` soubor je právě soubor ZIP s jiné rozšíření.</span><span class="sxs-lookup"><span data-stu-id="56f12-150">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="56f12-151">Můžete také zkontrolovat obsah balíčku, potom změnou `.nupkg` k `.zip`, ale nezapomeňte obnovit rozšíření před balíčku se nahrávají na nuget.org.</span><span class="sxs-lookup"><span data-stu-id="56f12-151">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="56f12-152">Pokud chcete zpřístupnit vašeho balíčku jinými vývojáři, postupujte podle pokynů [publikování balíčku](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="56f12-152">To make your package available to other developers, follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="56f12-153">Všimněte si, že `pack` vyžaduje Mono 4.4.2 na Mac OS X a nefunguje v systémech Linux.</span><span class="sxs-lookup"><span data-stu-id="56f12-153">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="56f12-154">V systému Mac, je nutné také převést Windows názvy cest v `.nuspec` souboru do cesty formátu UNIX.</span><span class="sxs-lookup"><span data-stu-id="56f12-154">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="net-standard-mapping-table"></a><span data-ttu-id="56f12-155">.NET standard mapování tabulky</span><span class="sxs-lookup"><span data-stu-id="56f12-155">.NET Standard mapping table</span></span>

| <span data-ttu-id="56f12-156">Název platformy</span><span class="sxs-lookup"><span data-stu-id="56f12-156">Platform Name</span></span> | <span data-ttu-id="56f12-157">Alias</span><span class="sxs-lookup"><span data-stu-id="56f12-157">Alias</span></span> |
| --- | --- |
| <span data-ttu-id="56f12-158">Standardní rozhraní .NET</span><span class="sxs-lookup"><span data-stu-id="56f12-158">.NET Standard</span></span> | <span data-ttu-id="56f12-159">monikerů netstandard</span><span class="sxs-lookup"><span data-stu-id="56f12-159">netstandard</span></span> | <span data-ttu-id="56f12-160">1.0</span><span class="sxs-lookup"><span data-stu-id="56f12-160">1.0</span></span> | <span data-ttu-id="56f12-161">1.1</span><span class="sxs-lookup"><span data-stu-id="56f12-161">1.1</span></span> | <span data-ttu-id="56f12-162">1.2</span><span class="sxs-lookup"><span data-stu-id="56f12-162">1.2</span></span> | <span data-ttu-id="56f12-163">1.3</span><span class="sxs-lookup"><span data-stu-id="56f12-163">1.3</span></span> | <span data-ttu-id="56f12-164">1.4</span><span class="sxs-lookup"><span data-stu-id="56f12-164">1.4</span></span> | <span data-ttu-id="56f12-165">1.5</span><span class="sxs-lookup"><span data-stu-id="56f12-165">1.5</span></span> | <span data-ttu-id="56f12-166">1.6</span><span class="sxs-lookup"><span data-stu-id="56f12-166">1.6</span></span> |
| <span data-ttu-id="56f12-167">.NET Core</span><span class="sxs-lookup"><span data-stu-id="56f12-167">.NET Core</span></span> | <span data-ttu-id="56f12-168">netcoreapp</span><span class="sxs-lookup"><span data-stu-id="56f12-168">netcoreapp</span></span> | <span data-ttu-id="56f12-169">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="56f12-169">&#x2192;</span></span> | <span data-ttu-id="56f12-170">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="56f12-170">&#x2192;</span></span> | <span data-ttu-id="56f12-171">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="56f12-171">&#x2192;</span></span> | <span data-ttu-id="56f12-172">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="56f12-172">&#x2192;</span></span> | <span data-ttu-id="56f12-173">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="56f12-173">&#x2192;</span></span> | <span data-ttu-id="56f12-174">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="56f12-174">&#x2192;</span></span> | <span data-ttu-id="56f12-175">1.0</span><span class="sxs-lookup"><span data-stu-id="56f12-175">1.0</span></span> |
| <span data-ttu-id="56f12-176">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="56f12-176">.NET Framework</span></span> | <span data-ttu-id="56f12-177">NET</span><span class="sxs-lookup"><span data-stu-id="56f12-177">net</span></span> | <span data-ttu-id="56f12-178">4.5</span><span class="sxs-lookup"><span data-stu-id="56f12-178">4.5</span></span> | <span data-ttu-id="56f12-179">4.5.1</span><span class="sxs-lookup"><span data-stu-id="56f12-179">4.5.1</span></span> | <span data-ttu-id="56f12-180">4.6</span><span class="sxs-lookup"><span data-stu-id="56f12-180">4.6</span></span> | <span data-ttu-id="56f12-181">4.6.1</span><span class="sxs-lookup"><span data-stu-id="56f12-181">4.6.1</span></span> | <span data-ttu-id="56f12-182">4.6.2</span><span class="sxs-lookup"><span data-stu-id="56f12-182">4.6.2</span></span> | <span data-ttu-id="56f12-183">4.6.3</span><span class="sxs-lookup"><span data-stu-id="56f12-183">4.6.3</span></span> |
| <span data-ttu-id="56f12-184">Mono/Xamarin Platforms</span><span class="sxs-lookup"><span data-stu-id="56f12-184">Mono/Xamarin Platforms</span></span> | <span data-ttu-id="56f12-185">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="56f12-185">&#x2192;</span></span> | <span data-ttu-id="56f12-186">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="56f12-186">&#x2192;</span></span> | <span data-ttu-id="56f12-187">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="56f12-187">&#x2192;</span></span> | <span data-ttu-id="56f12-188">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="56f12-188">&#x2192;</span></span> | <span data-ttu-id="56f12-189">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="56f12-189">&#x2192;</span></span> | <span data-ttu-id="56f12-190">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="56f12-190">&#x2192;</span></span> |
| <span data-ttu-id="56f12-191">Univerzální platforma pro Windows</span><span class="sxs-lookup"><span data-stu-id="56f12-191">Universal Windows Platform</span></span> | <span data-ttu-id="56f12-192">uap</span><span class="sxs-lookup"><span data-stu-id="56f12-192">uap</span></span> | <span data-ttu-id="56f12-193">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="56f12-193">&#x2192;</span></span> | <span data-ttu-id="56f12-194">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="56f12-194">&#x2192;</span></span> | <span data-ttu-id="56f12-195">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="56f12-195">&#x2192;</span></span> | <span data-ttu-id="56f12-196">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="56f12-196">&#x2192;</span></span> |<span data-ttu-id="56f12-197">10.0</span><span class="sxs-lookup"><span data-stu-id="56f12-197">10.0</span></span> |
| <span data-ttu-id="56f12-198">Windows</span><span class="sxs-lookup"><span data-stu-id="56f12-198">Windows</span></span> | <span data-ttu-id="56f12-199">Win</span><span class="sxs-lookup"><span data-stu-id="56f12-199">win</span></span>| <span data-ttu-id="56f12-200">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="56f12-200">&#x2192;</span></span> | <span data-ttu-id="56f12-201">8.0</span><span class="sxs-lookup"><span data-stu-id="56f12-201">8.0</span></span> | <span data-ttu-id="56f12-202">8.1</span><span class="sxs-lookup"><span data-stu-id="56f12-202">8.1</span></span> |
| <span data-ttu-id="56f12-203">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="56f12-203">Windows Phone</span></span> | <span data-ttu-id="56f12-204">wpa</span><span class="sxs-lookup"><span data-stu-id="56f12-204">wpa</span></span>| <span data-ttu-id="56f12-205">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="56f12-205">&#x2192;</span></span>| <span data-ttu-id="56f12-206">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="56f12-206">&#x2192;</span></span> | <span data-ttu-id="56f12-207">8.1</span><span class="sxs-lookup"><span data-stu-id="56f12-207">8.1</span></span> |
| <span data-ttu-id="56f12-208">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="56f12-208">Windows Phone Silverlight</span></span> | <span data-ttu-id="56f12-209">wp</span><span class="sxs-lookup"><span data-stu-id="56f12-209">wp</span></span> | <span data-ttu-id="56f12-210">8.0</span><span class="sxs-lookup"><span data-stu-id="56f12-210">8.0</span></span> |

## <a name="related-topics"></a><span data-ttu-id="56f12-211">Související témata</span><span class="sxs-lookup"><span data-stu-id="56f12-211">Related topics</span></span>

- [<span data-ttu-id="56f12-212">referenční dokumentace příponou .nuspec</span><span class="sxs-lookup"><span data-stu-id="56f12-212">.nuspec reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="56f12-213">Podpora více verzí rozhraní .NET framework</span><span class="sxs-lookup"><span data-stu-id="56f12-213">Supporting multiple .NET framework versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="56f12-214">Zahrnout do balíčku nástroje MSBuild props a cíle</span><span class="sxs-lookup"><span data-stu-id="56f12-214">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="56f12-215">Vytvoření lokalizovaných balíčků</span><span class="sxs-lookup"><span data-stu-id="56f12-215">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="56f12-216">Balíčky symbolů</span><span class="sxs-lookup"><span data-stu-id="56f12-216">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="56f12-217">Správa verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="56f12-217">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="56f12-218">Standardní knihovny .NET dokumentaci</span><span class="sxs-lookup"><span data-stu-id="56f12-218">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="56f12-219">Portování do .NET Core z rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="56f12-219">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
