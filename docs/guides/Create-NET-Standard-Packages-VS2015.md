---
title: Vytvořte standardní rozhraní .NET a balíčky NuGet rozhraní .NET Framework s Visual Studiem 2015
description: Návod začátku do konce, vytváření balíčků NuGet pro rozhraní .NET Framework a .NET Standard pomocí nástroje NuGet 3.x a Visual Studio 2015.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 02/02/2018
ms.topic: tutorial
ms.openlocfilehash: c66e782ea5d4e9e2a9585d8301dc2a1b2e8c72b9
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818724"
---
# <a name="create-net-standard-and-net-framework-packages-with-visual-studio-2015"></a><span data-ttu-id="9bdea-103">Vytvoření balíčků .NET Standard a rozhraní .NET Framework s Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="9bdea-103">Create .NET Standard and .NET Framework packages with Visual Studio 2015</span></span>

<span data-ttu-id="9bdea-104">**Poznámka:** Visual Studio 2017 se doporučuje pro vývoj .NET standardní knihovny.</span><span class="sxs-lookup"><span data-stu-id="9bdea-104">**Note:** Visual Studio 2017 is recommended for developing .NET Standard libraries.</span></span> <span data-ttu-id="9bdea-105">Visual Studio 2015 můžete pracovat, ale nástrojů .NET Core byla uvedena do režimu pouze pro náhled stavu.</span><span class="sxs-lookup"><span data-stu-id="9bdea-105">Visual Studio 2015 can work but the .NET Core tooling was brought only to Preview state.</span></span> <span data-ttu-id="9bdea-106">V tématu [vytvoření a publikování balíčku s Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) pro práci s NuGet 4.x+ a Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="9bdea-106">See [Create and publish a package with Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) for working with NuGet 4.x+ and Visual Studio 2017.</span></span>

<span data-ttu-id="9bdea-107">[Standardní knihovny .NET](/dotnet/articles/standard/library) je formální specifikaci rozhraní API technologie .NET by měla být k dispozici pro všechny moduly runtime rozhraní .NET, tím větší jednotnost vytváří v ekosystému .NET.</span><span class="sxs-lookup"><span data-stu-id="9bdea-107">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="9bdea-108">Standardní knihovny .NET definuje jednotnou sadu BCL (základní třída knihovna) rozhraní API pro všechny platformy .NET implementovat, nezávisle na zatížení.</span><span class="sxs-lookup"><span data-stu-id="9bdea-108">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="9bdea-109">Umožňuje vývojářům vytvářet kód, který je použitelný přes všechny moduly runtime rozhraní .NET a snižuje není eliminuje direktivy specifické pro platformu Podmíněná kompilace v sdíleného kódu.</span><span class="sxs-lookup"><span data-stu-id="9bdea-109">It enables developers to produce code that is usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="9bdea-110">Tento průvodce vás provede procesem vytváření balíčku NuGet cílení na rozhraní .NET standardní knihovně 1,4 nebo balíček cílení na rozhraní .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="9bdea-110">This guide walks you through creating a NuGet package targeting .NET Standard Library 1.4 or a package targeting .NET Framework 4.6.</span></span> <span data-ttu-id="9bdea-111">Knihovna .NET standardní 1.4 funguje napříč rozhraní .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core a Mono nebo Xamarin.</span><span class="sxs-lookup"><span data-stu-id="9bdea-111">A .NET Standard 1.4 library works across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="9bdea-112">Podrobnosti najdete v tématu [.NET Standard mapovací tabulku](/dotnet/standard/net-standard#net-implementation-support) (.NET dokumentaci).</span><span class="sxs-lookup"><span data-stu-id="9bdea-112">For details, see the [.NET Standard mapping table](/dotnet/standard/net-standard#net-implementation-support) (.NET documentation).</span></span> <span data-ttu-id="9bdea-113">Pokud chcete, můžete druhou verzi standardní knihovny .NET.</span><span class="sxs-lookup"><span data-stu-id="9bdea-113">You can choose other version of the .NET Standard Library if you want.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9bdea-114">Požadavky</span><span class="sxs-lookup"><span data-stu-id="9bdea-114">Prerequisites</span></span>

1. <span data-ttu-id="9bdea-115">Visual Studio 2015 Update 3</span><span class="sxs-lookup"><span data-stu-id="9bdea-115">Visual Studio 2015 Update 3</span></span>
1. <span data-ttu-id="9bdea-116">(Jenom .NET standard) [.NET core SDK](https://www.microsoft.com/net/download/)</span><span class="sxs-lookup"><span data-stu-id="9bdea-116">(.NET Standard only) [.NET Core SDK](https://www.microsoft.com/net/download/)</span></span>
1. <span data-ttu-id="9bdea-117">Rozhraní příkazového řádku NuGet.</span><span class="sxs-lookup"><span data-stu-id="9bdea-117">NuGet CLI.</span></span> <span data-ttu-id="9bdea-118">Stáhněte si nejnovější verzi nuget.exe z [nuget.org/downloads](https://nuget.org/downloads), ukládání do umístění podle vaší volby.</span><span class="sxs-lookup"><span data-stu-id="9bdea-118">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="9bdea-119">Pak přidejte tohoto umístění do vaší proměnné prostředí PATH, pokud již není.</span><span class="sxs-lookup"><span data-stu-id="9bdea-119">Then add that location to your PATH environment variable if it isn't already.</span></span>

    > [!Note]
    > <span data-ttu-id="9bdea-120">nuget.exe je že nástroj příkazového řádku, není instalační program, takže je nutné z prohlížeče namísto spuštění ho uložte stažený soubor.</span><span class="sxs-lookup"><span data-stu-id="9bdea-120">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-class-library-project"></a><span data-ttu-id="9bdea-121">Vytvoření projektu knihovny tříd</span><span class="sxs-lookup"><span data-stu-id="9bdea-121">Create the class library project</span></span>

1. <span data-ttu-id="9bdea-122">V sadě Visual Studio **soubor > Nový > projekt**, rozbalte **Visual C# > Windows** uzlu, vyberte **knihovny tříd (přenositelností)**, změňte název na AppLogger a vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="9bdea-122">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and select **OK**.</span></span>

    ![Vytvoření nového projektu knihovny tříd](media/NetStandard-NewProject.png)

1. <span data-ttu-id="9bdea-124">V **přidat Přenosná knihovna tříd** dialog, který se zobrazí, vyberte možnosti pro `.NET Framework 4.6` a `ASP.NET Core 1.0`.</span><span class="sxs-lookup"><span data-stu-id="9bdea-124">In the **Add Portable Class Library** dialog that appears, select the options for `.NET Framework 4.6` and `ASP.NET Core 1.0`.</span></span> <span data-ttu-id="9bdea-125">(Pokud cílení na rozhraní .NET Framework, můžete vybrat kteroukoli možnosti jsou vhodné.)</span><span class="sxs-lookup"><span data-stu-id="9bdea-125">(If targeting .NET Framework, you can select whichever options are appropriate.)</span></span>

1. <span data-ttu-id="9bdea-126">Pokud cílení na rozhraní .NET standardní, klikněte pravým tlačítkem `AppLogger (Portable)` v Průzkumníku řešení, vyberte **vlastnosti**, vyberte **knihovny** a potom vyberte **cíl Standard platformy .NET** v **cílení na** oddílu.</span><span class="sxs-lookup"><span data-stu-id="9bdea-126">If targeting .NET Standard, right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then select  **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="9bdea-127">Tato akce zobrazí výzvu k potvrzení, po kterém můžete vybrat `.NET Standard 1.4` (nebo jinou verzi k dispozici) z rozevíracího seznamu:</span><span class="sxs-lookup"><span data-stu-id="9bdea-127">This action prompts for confirmation, after which you can select `.NET Standard 1.4` (or another available version) from the drop down:</span></span>

    ![Nastavení cíl na standardní 1.4 rozhraní .NET](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="9bdea-129">Klikněte na **sestavení** změňte **konfigurace** k `Release`a zaškrtněte políčko pro **souborů dokumentace XML**.</span><span class="sxs-lookup"><span data-stu-id="9bdea-129">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>

1. <span data-ttu-id="9bdea-130">Přidáte kód pro součásti, například:</span><span class="sxs-lookup"><span data-stu-id="9bdea-130">Add your code to the component, for example:</span></span>

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

1. <span data-ttu-id="9bdea-131">Nastavte konfiguraci na verzi, sestavte projekt a zkontrolujte, že jsou v rámci vytváří soubory DLL a XML `bin\Release` složky.</span><span class="sxs-lookup"><span data-stu-id="9bdea-131">Set the configuration to Release, build the project, and check that DLL and XML files are produced within the `bin\Release` folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="9bdea-132">Vytvářet a aktualizovat soubor s příponou .nuspec</span><span class="sxs-lookup"><span data-stu-id="9bdea-132">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="9bdea-133">Otevřete příkazový řádek, přejděte do složky obsahující `AppLogger.csproj` složky (o jednu úroveň pod where `.sln` soubor), a spusťte NuGet `spec` příkaz pro vytvoření počáteční `AppLogger.nuspec` souboru:</span><span class="sxs-lookup"><span data-stu-id="9bdea-133">Open a command prompt, navigate to the folder containing `AppLogger.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="9bdea-134">Otevřete `AppLogger.nuspec` v editoru a aktualizovat ji tak, aby odpovídala následující, nahraďte vaše_jméno odpovídající hodnotu.</span><span class="sxs-lookup"><span data-stu-id="9bdea-134">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="9bdea-135">`<id>` Hodnotu, konkrétně musí být jedinečný v rámci nuget.org (viz zásady vytváření názvů, které jsou popsané v [vytváření balíčku](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="9bdea-135">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="9bdea-136">Všimněte si také, zda je nutné také aktualizovat autora a popis značky nebo dojde k chybě během kroku okolních.</span><span class="sxs-lookup"><span data-stu-id="9bdea-136">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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

1. <span data-ttu-id="9bdea-137">Přidat odkaz na sestavení, které chcete `.nuspec` souboru, a to knihovně DLL a soubor IntelliSense XML:</span><span class="sxs-lookup"><span data-stu-id="9bdea-137">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    <span data-ttu-id="9bdea-138">Cílení na rozhraní .NET standardní, položky se zobrazí podobná této:</span><span class="sxs-lookup"><span data-stu-id="9bdea-138">If targeting .NET Standard, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

    <span data-ttu-id="9bdea-139">Pokud cílení na rozhraní .NET Framework, se objeví položky podobné následujícímu:</span><span class="sxs-lookup"><span data-stu-id="9bdea-139">If targeting .NET Framework, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\net46\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\net46\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="9bdea-140">Klikněte pravým tlačítkem na řešení a vyberte **sestavit řešení** ke generování všechny soubory pro balíček.</span><span class="sxs-lookup"><span data-stu-id="9bdea-140">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>

### <a name="declaring-dependencies"></a><span data-ttu-id="9bdea-141">Deklarování závislosti</span><span class="sxs-lookup"><span data-stu-id="9bdea-141">Declaring dependencies</span></span>

<span data-ttu-id="9bdea-142">Pokud máte všechny závislosti na dalších balíčcích NuGet, seznamu těch, které do manifestu `<dependencies>` element s `<group>` elementy.</span><span class="sxs-lookup"><span data-stu-id="9bdea-142">If you have any dependencies on other NuGet packages, list those in the manifest's `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="9bdea-143">Chcete-li například závislost na NewtonSoft.Json 8.0.3 deklarovat nebo vyšší, přidejte následující:</span><span class="sxs-lookup"><span data-stu-id="9bdea-143">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="9bdea-144">Syntaxe *verze* atribut zde označuje, že verze 8.0.3 nebo novější je přijatelná.</span><span class="sxs-lookup"><span data-stu-id="9bdea-144">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="9bdea-145">Zadejte jinou verzi rozsahy, najdete v tématu [Správa verzí balíčku](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="9bdea-145">To specify different version ranges, refer to [Package versioning](../reference/package-versioning.md).</span></span>

### <a name="adding-a-readme"></a><span data-ttu-id="9bdea-146">Přidání soubor readme</span><span class="sxs-lookup"><span data-stu-id="9bdea-146">Adding a readme</span></span>

<span data-ttu-id="9bdea-147">Vytvoření vaší `readme.txt` souboru, umístěte do kořenové složky projektu a najdete ji v `.nuspec` souboru:</span><span class="sxs-lookup"><span data-stu-id="9bdea-147">Create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

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

<span data-ttu-id="9bdea-148">Visual Studio zobrazení `readme.txt` při instalaci balíčku do projektu.</span><span class="sxs-lookup"><span data-stu-id="9bdea-148">Visual Studio display `readme.txt` when the package is installed into a project.</span></span> <span data-ttu-id="9bdea-149">Soubor se nezobrazí, pokud nainstalované do projektů .NET Core, nebo pro balíčky, které se instalují jako závislost.</span><span class="sxs-lookup"><span data-stu-id="9bdea-149">The file is not shown when installed into .NET Core projects, or for packages that are installed as a dependency.</span></span>

## <a name="package-the-component"></a><span data-ttu-id="9bdea-150">Balíček součásti</span><span class="sxs-lookup"><span data-stu-id="9bdea-150">Package the component</span></span>

<span data-ttu-id="9bdea-151">S dokončené `.nuspec` odkazující na všechny soubory, které je potřeba zahrnout do balíčku, jste připraveni ke spuštění `pack` příkaz:</span><span class="sxs-lookup"><span data-stu-id="9bdea-151">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack AppLogger.nuspec
```

<span data-ttu-id="9bdea-152">Tím se vygeneruje `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="9bdea-152">This generates `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="9bdea-153">Otevření tohoto souboru v nástroje, jako [Explorer balíček NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) a rozšiřování všechny uzly, můžete zobrazit následující obsah (zobrazené pro .NET Standard):</span><span class="sxs-lookup"><span data-stu-id="9bdea-153">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents (shown for .NET Standard):</span></span>

![Průzkumník balíček NuGet zobrazující AppLogger balíčku](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="9bdea-155">A `.nupkg` soubor je právě soubor ZIP s jiné rozšíření.</span><span class="sxs-lookup"><span data-stu-id="9bdea-155">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="9bdea-156">Můžete také zkontrolovat obsah balíčku, potom změnou `.nupkg` k `.zip`, ale nezapomeňte obnovit rozšíření před balíčku se nahrávají na nuget.org.</span><span class="sxs-lookup"><span data-stu-id="9bdea-156">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="9bdea-157">Pokud chcete zpřístupnit vašeho balíčku jinými vývojáři, postupujte podle pokynů [publikování balíčku](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="9bdea-157">To make your package available to other developers, follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="9bdea-158">Všimněte si, že `pack` vyžaduje Mono 4.4.2 na Mac OS X a nefunguje v systémech Linux.</span><span class="sxs-lookup"><span data-stu-id="9bdea-158">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="9bdea-159">V systému Mac, je nutné také převést Windows názvy cest v `.nuspec` souboru do cesty formátu UNIX.</span><span class="sxs-lookup"><span data-stu-id="9bdea-159">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="related-topics"></a><span data-ttu-id="9bdea-160">Související témata</span><span class="sxs-lookup"><span data-stu-id="9bdea-160">Related topics</span></span>

- [<span data-ttu-id="9bdea-161">referenční dokumentace příponou .nuspec</span><span class="sxs-lookup"><span data-stu-id="9bdea-161">.nuspec reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="9bdea-162">Podpora více verzí rozhraní .NET framework</span><span class="sxs-lookup"><span data-stu-id="9bdea-162">Supporting multiple .NET framework versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="9bdea-163">Zahrnout do balíčku nástroje MSBuild props a cíle</span><span class="sxs-lookup"><span data-stu-id="9bdea-163">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="9bdea-164">Vytvoření lokalizovaných balíčků</span><span class="sxs-lookup"><span data-stu-id="9bdea-164">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="9bdea-165">Balíčky symbolů</span><span class="sxs-lookup"><span data-stu-id="9bdea-165">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="9bdea-166">Správa verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="9bdea-166">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="9bdea-167">Standardní knihovny .NET dokumentaci</span><span class="sxs-lookup"><span data-stu-id="9bdea-167">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="9bdea-168">Portování do .NET Core z rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="9bdea-168">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)