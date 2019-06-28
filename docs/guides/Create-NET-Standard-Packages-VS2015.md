---
title: Vytvoření .NET Standard a balíčky NuGet rozhraní .NET Framework pomocí sady Visual Studio 2015
description: Začátku do konce postup vytváření balíčků NuGet pro rozhraní .NET Framework a .NET Standard s využitím NuGet 3.x a Visual Studio 2015.
author: karann-msft
ms.author: karann
ms.date: 02/02/2018
ms.topic: tutorial
ms.openlocfilehash: af0c42853a9e407557a010ff2793406499b4b2ef
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426883"
---
# <a name="create-net-standard-and-net-framework-packages-with-visual-studio-2015"></a><span data-ttu-id="83e70-103">Vytváření balíčků pro .NET Standard a .NET Framework pomocí sady Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="83e70-103">Create .NET Standard and .NET Framework packages with Visual Studio 2015</span></span>

<span data-ttu-id="83e70-104">**Poznámka:** Visual Studio 2017 se doporučuje pro vývoj knihoven .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="83e70-104">**Note:** Visual Studio 2017 is recommended for developing .NET Standard libraries.</span></span> <span data-ttu-id="83e70-105">Visual Studio 2015 můžete pracovat, ale nástroje pro .NET Core se přepne do režimu jenom pro verzi Preview.</span><span class="sxs-lookup"><span data-stu-id="83e70-105">Visual Studio 2015 can work but the .NET Core tooling was brought only to Preview state.</span></span> <span data-ttu-id="83e70-106">Zobrazit [vytvoření a publikování balíčku sady Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) pro práci s NuGet 4.x+ a sady Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="83e70-106">See [Create and publish a package with Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) for working with NuGet 4.x+ and Visual Studio 2017.</span></span>

<span data-ttu-id="83e70-107">[Knihovna .NET Standard](/dotnet/articles/standard/library) je formální specifikaci rozhraní .NET API by měla být k dispozici pro všechny moduly runtime .NET, tedy vytvoření většího sjednocení v ekosystému .NET.</span><span class="sxs-lookup"><span data-stu-id="83e70-107">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="83e70-108">Knihovna .NET Standard definuje jednotnou sadu BCL (knihovna tříd Base) rozhraní API pro všechny platformy .NET pro implementaci, nezávisle na úloze.</span><span class="sxs-lookup"><span data-stu-id="83e70-108">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="83e70-109">Umožňuje vývojářům vytvářet kód, který je použitelný přes všechny moduly runtime .NET a snižuje, pokud nebude eliminuje direktivy podmíněné kompilace specifické pro platformu v sdílený kód.</span><span class="sxs-lookup"><span data-stu-id="83e70-109">It enables developers to produce code that is usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="83e70-110">Tento průvodce vás provede vytvořením cílí na .NET Standard knihovny 1.4 balíček NuGet nebo pomocí balíčku cílení na rozhraní .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="83e70-110">This guide walks you through creating a NuGet package targeting .NET Standard Library 1.4 or a package targeting .NET Framework 4.6.</span></span> <span data-ttu-id="83e70-111">Knihovna .NET Standard 1.4 funguje i rozhraní .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, Mono/Xamarin.</span><span class="sxs-lookup"><span data-stu-id="83e70-111">A .NET Standard 1.4 library works across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="83e70-112">Podrobnosti najdete v tématu [.NET Standard mapování tabulky](/dotnet/standard/net-standard#net-implementation-support) (dokumentace k .NET).</span><span class="sxs-lookup"><span data-stu-id="83e70-112">For details, see the [.NET Standard mapping table](/dotnet/standard/net-standard#net-implementation-support) (.NET documentation).</span></span> <span data-ttu-id="83e70-113">Chcete-li, můžete zvolit jinou verzi knihovny .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="83e70-113">You can choose other version of the .NET Standard Library if you want.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83e70-114">Požadavky</span><span class="sxs-lookup"><span data-stu-id="83e70-114">Prerequisites</span></span>

1. <span data-ttu-id="83e70-115">Visual Studio 2015 Update 3</span><span class="sxs-lookup"><span data-stu-id="83e70-115">Visual Studio 2015 Update 3</span></span>
1. <span data-ttu-id="83e70-116">(Pouze .NET standard) [.NET core SDK](https://www.microsoft.com/net/download/)</span><span class="sxs-lookup"><span data-stu-id="83e70-116">(.NET Standard only) [.NET Core SDK](https://www.microsoft.com/net/download/)</span></span>
1. <span data-ttu-id="83e70-117">Rozhraní příkazového řádku NuGet.</span><span class="sxs-lookup"><span data-stu-id="83e70-117">NuGet CLI.</span></span> <span data-ttu-id="83e70-118">Stažení nejnovější verze programu nuget.exe z [nuget.org/downloads](https://nuget.org/downloads), ukládání do umístění podle vašeho výběru.</span><span class="sxs-lookup"><span data-stu-id="83e70-118">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="83e70-119">Pak přidejte toto umístění do proměnné prostředí PATH, pokud ještě není.</span><span class="sxs-lookup"><span data-stu-id="83e70-119">Then add that location to your PATH environment variable if it isn't already.</span></span>

    > [!Note]
    > <span data-ttu-id="83e70-120">nuget.exe je že nástroj příkazového řádku, není instalační program, proto ji nezapomeňte Uložte stažený soubor ve svém prohlížeči místo jeho spuštění.</span><span class="sxs-lookup"><span data-stu-id="83e70-120">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-class-library-project"></a><span data-ttu-id="83e70-121">Vytvořte projekt knihovny tříd</span><span class="sxs-lookup"><span data-stu-id="83e70-121">Create the class library project</span></span>

1. <span data-ttu-id="83e70-122">V sadě Visual Studio **soubor > Nový > projekt**, rozbalte **Visual C# > Windows** uzlu, vyberte **knihovna tříd (přenosná)** , změňte název na AppLogger a vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="83e70-122">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and select **OK**.</span></span>

    ![Vytvořit nový projekt knihovny tříd](media/NetStandard-NewProject.png)

1. <span data-ttu-id="83e70-124">V **přidat přenosnou knihovnu tříd** dialogové okno, které se zobrazí, vyberte požadované možnosti pro `.NET Framework 4.6` a `ASP.NET Core 1.0`.</span><span class="sxs-lookup"><span data-stu-id="83e70-124">In the **Add Portable Class Library** dialog that appears, select the options for `.NET Framework 4.6` and `ASP.NET Core 1.0`.</span></span> <span data-ttu-id="83e70-125">(Pokud je zaměřen na rozhraní .NET Framework, můžete vybrat toho možnosti je vhodné.)</span><span class="sxs-lookup"><span data-stu-id="83e70-125">(If targeting .NET Framework, you can select whichever options are appropriate.)</span></span>

1. <span data-ttu-id="83e70-126">Cílení na .NET Standard, klikněte pravým tlačítkem `AppLogger (Portable)` v Průzkumníku řešení vyberte **vlastnosti**, vyberte **knihovny** kartu a potom vyberte **cílové Standard platformy .NET** v **cílení** oddílu.</span><span class="sxs-lookup"><span data-stu-id="83e70-126">If targeting .NET Standard, right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then select  **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="83e70-127">Tato akce zobrazí výzvu k potvrzení, po kterém můžete vybrat `.NET Standard 1.4` (nebo jinou verzi k dispozici) z rozevíracího seznamu:</span><span class="sxs-lookup"><span data-stu-id="83e70-127">This action prompts for confirmation, after which you can select `.NET Standard 1.4` (or another available version) from the drop down:</span></span>

    ![Nastavení cíl na .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="83e70-129">Klikněte na **sestavení** kartu, změnit **konfigurace** k `Release`a zaškrtněte políčko u **soubor dokumentace XML**.</span><span class="sxs-lookup"><span data-stu-id="83e70-129">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>

1. <span data-ttu-id="83e70-130">Přidejte svůj kód na součást, například:</span><span class="sxs-lookup"><span data-stu-id="83e70-130">Add your code to the component, for example:</span></span>

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

1. <span data-ttu-id="83e70-131">Nastavení konfigurace pro vydání, sestavte projekt a zkontrolujte, že jsou soubory DLL a XML vytvořený v rámci `bin\Release` složky.</span><span class="sxs-lookup"><span data-stu-id="83e70-131">Set the configuration to Release, build the project, and check that DLL and XML files are produced within the `bin\Release` folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="83e70-132">Vytvoření a aktualizaci souboru .nuspec souboru</span><span class="sxs-lookup"><span data-stu-id="83e70-132">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="83e70-133">Otevřete příkazový řádek, přejděte na složku obsahující `AppLogger.csproj` složky (o jednu úroveň pod where `.sln` soubor), a spusťte NuGet `spec` příkaz pro vytvoření počáteční `AppLogger.nuspec` souboru:</span><span class="sxs-lookup"><span data-stu-id="83e70-133">Open a command prompt, navigate to the folder containing `AppLogger.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="83e70-134">Otevřít `AppLogger.nuspec` v editoru a aktualizujte ji, aby se shodoval s následujícím, nahradíte vaše_jméno odpovídající hodnotu.</span><span class="sxs-lookup"><span data-stu-id="83e70-134">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="83e70-135">`<id>` , Konkrétně musí být hodnota jedinečná napříč nuget.org (naleznete v tématu Zásady vytváření názvů je popsáno v [vytvoření balíčku](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="83e70-135">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="83e70-136">Všimněte si také, že budete muset taky aktualizovat Autor a popis značky nebo dojde k chybě během kroku balení.</span><span class="sxs-lookup"><span data-stu-id="83e70-136">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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

1. <span data-ttu-id="83e70-137">Přidejte referenční sestavení pro `.nuspec` souboru, a to knihovny DLL a soubor IntelliSense XML:</span><span class="sxs-lookup"><span data-stu-id="83e70-137">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    <span data-ttu-id="83e70-138">Cílení na .NET Standard, položky se zobrazí podobný následujícímu:</span><span class="sxs-lookup"><span data-stu-id="83e70-138">If targeting .NET Standard, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

    <span data-ttu-id="83e70-139">Pokud se zaměřujete na rozhraní .NET Framework, vypadat podobně jako následující položky:</span><span class="sxs-lookup"><span data-stu-id="83e70-139">If targeting .NET Framework, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\net46\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\net46\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="83e70-140">Klikněte pravým tlačítkem na řešení a vyberte **sestavit řešení** vygenerujte tyto soubory pro balíček.</span><span class="sxs-lookup"><span data-stu-id="83e70-140">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>

### <a name="declaring-dependencies"></a><span data-ttu-id="83e70-141">Deklarace závislostí</span><span class="sxs-lookup"><span data-stu-id="83e70-141">Declaring dependencies</span></span>

<span data-ttu-id="83e70-142">Pokud máte všechny závislosti na dalších balíčcích NuGet, seznamu programů v manifestu `<dependencies>` element s `<group>` elementy.</span><span class="sxs-lookup"><span data-stu-id="83e70-142">If you have any dependencies on other NuGet packages, list those in the manifest's `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="83e70-143">Chcete-li například deklaruje závislost na NewtonSoft.Json 8.0.3 nebo novější, přidejte následující:</span><span class="sxs-lookup"><span data-stu-id="83e70-143">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="83e70-144">Syntaxe *verze* atribut tady označuje tuto verzi 8.0.3 nebo vyšší je přijatelné.</span><span class="sxs-lookup"><span data-stu-id="83e70-144">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="83e70-145">Zadejte rozsahy jinou verzi, najdete v tématu [Správa verzí balíčků](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="83e70-145">To specify different version ranges, refer to [Package versioning](../reference/package-versioning.md).</span></span>

### <a name="adding-a-readme"></a><span data-ttu-id="83e70-146">Přidání souboru readme</span><span class="sxs-lookup"><span data-stu-id="83e70-146">Adding a readme</span></span>

<span data-ttu-id="83e70-147">Vytvoření vašeho `readme.txt` souboru, umístěte ho do kořenové složky projektu a najdete ji v `.nuspec` souboru:</span><span class="sxs-lookup"><span data-stu-id="83e70-147">Create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

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

<span data-ttu-id="83e70-148">Visual Studio zobrazení `readme.txt` při instalaci balíčku do projektu.</span><span class="sxs-lookup"><span data-stu-id="83e70-148">Visual Studio display `readme.txt` when the package is installed into a project.</span></span> <span data-ttu-id="83e70-149">Soubor se nezobrazí při instalaci do projektů .NET Core nebo pro balíčky, které se instalují jako závislost.</span><span class="sxs-lookup"><span data-stu-id="83e70-149">The file is not shown when installed into .NET Core projects, or for packages that are installed as a dependency.</span></span>

## <a name="package-the-component"></a><span data-ttu-id="83e70-150">Balíček komponenty</span><span class="sxs-lookup"><span data-stu-id="83e70-150">Package the component</span></span>

<span data-ttu-id="83e70-151">S dokončenou `.nuspec` odkazující na všechny soubory, které je potřeba zahrnout do balíčku, jste připraveni spustit `pack` příkaz:</span><span class="sxs-lookup"><span data-stu-id="83e70-151">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack AppLogger.nuspec
```

<span data-ttu-id="83e70-152">Tím se vygeneruje `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="83e70-152">This generates `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="83e70-153">Tento soubor otevřete v nástroje, jako je [NuGet – Průzkumník balíčků](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) a rozšiřuje všechny uzly, viz následující obsah (viz obrázek pro .NET Standard):</span><span class="sxs-lookup"><span data-stu-id="83e70-153">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents (shown for .NET Standard):</span></span>

![Zobrazuje AppLogger balíčku NuGet – Průzkumník balíčků](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="83e70-155">A `.nupkg` soubor je jenom soubor ZIP s jinou příponou.</span><span class="sxs-lookup"><span data-stu-id="83e70-155">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="83e70-156">Můžete také prozkoumat obsah balíčku, potom změnou `.nupkg` k `.zip`, ale nezapomeňte k obnovení rozšíření před nahráním balíčků na nuget.org.</span><span class="sxs-lookup"><span data-stu-id="83e70-156">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="83e70-157">Aby váš balíček k dispozici s ostatními vývojáři, postupujte podle pokynů [publikování balíčku](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="83e70-157">To make your package available to other developers, follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="83e70-158">Všimněte si, že `pack` vyžaduje Mono 4.4.2 v Mac OS X a nebude fungovat v systémech Linux.</span><span class="sxs-lookup"><span data-stu-id="83e70-158">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="83e70-159">Na počítači Mac, je také nutné převést Windows cest v `.nuspec` soubor do cesty k systému UNIX.</span><span class="sxs-lookup"><span data-stu-id="83e70-159">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="related-topics"></a><span data-ttu-id="83e70-160">Související témata</span><span class="sxs-lookup"><span data-stu-id="83e70-160">Related topics</span></span>

- [<span data-ttu-id="83e70-161">odkaz na souboru .nuspec</span><span class="sxs-lookup"><span data-stu-id="83e70-161">.nuspec reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="83e70-162">Podpora více verzí rozhraní .NET framework</span><span class="sxs-lookup"><span data-stu-id="83e70-162">Supporting multiple .NET framework versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="83e70-163">Zahrnout do balíčku cíle a vlastnosti nástroje MSBuild</span><span class="sxs-lookup"><span data-stu-id="83e70-163">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="83e70-164">Vytvoření lokalizovaných balíčků</span><span class="sxs-lookup"><span data-stu-id="83e70-164">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="83e70-165">Balíčky symbolů</span><span class="sxs-lookup"><span data-stu-id="83e70-165">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="83e70-166">Správa verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="83e70-166">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="83e70-167">Dokumentace ke službě knihovna .NET standard</span><span class="sxs-lookup"><span data-stu-id="83e70-167">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="83e70-168">Portování do .NET Core v rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="83e70-168">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
