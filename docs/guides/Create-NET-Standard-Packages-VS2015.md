---
title: Vytváření balíčků NuGet pro .NET Standard a .NET Framework pomocí sady Visual Studio 2015
description: Kompletní návod k vytváření .NET Standard a .NET Framework balíčků NuGet pomocí NuGet 3. x a Visual Studio 2015.
author: karann-msft
ms.author: karann
ms.date: 02/02/2018
ms.topic: tutorial
ms.openlocfilehash: 11dce27b93c3d09a2d27dc79f8d4fed86df879ba
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488978"
---
# <a name="create-net-standard-and-net-framework-packages-with-visual-studio-2015"></a><span data-ttu-id="dd24d-103">Vytváření balíčků .NET Standard a .NET Framework pomocí sady Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="dd24d-103">Create .NET Standard and .NET Framework packages with Visual Studio 2015</span></span>

<span data-ttu-id="dd24d-104">**Poznámka:** Visual Studio 2017 se doporučuje pro vývoj .NET Standardch knihoven.</span><span class="sxs-lookup"><span data-stu-id="dd24d-104">**Note:** Visual Studio 2017 is recommended for developing .NET Standard libraries.</span></span> <span data-ttu-id="dd24d-105">Visual Studio 2015 může pracovat, ale nástroje .NET Core byly předáno pouze do stavu Preview.</span><span class="sxs-lookup"><span data-stu-id="dd24d-105">Visual Studio 2015 can work but the .NET Core tooling was brought only to Preview state.</span></span> <span data-ttu-id="dd24d-106">Podívejte se na téma [Vytvoření a publikování balíčku pomocí sady Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) pro práci s NuGet 4. x + a Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="dd24d-106">See [Create and publish a package with Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) for working with NuGet 4.x+ and Visual Studio 2017.</span></span>

<span data-ttu-id="dd24d-107">[Knihovna .NET Standard](/dotnet/articles/standard/library) je formální specifikace rozhraní API .NET, která má být k dispozici ve všech modulech runtime .NET, což znamená větší jednotnost v ekosystému .NET.</span><span class="sxs-lookup"><span data-stu-id="dd24d-107">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="dd24d-108">Knihovna .NET Standard definuje jednotnou sadu rozhraní API BCL (knihovny základních tříd) pro všechny platformy .NET, které mají být implementovány, nezávisle na zatížení.</span><span class="sxs-lookup"><span data-stu-id="dd24d-108">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="dd24d-109">Umožňuje vývojářům vytvářet kód, který je použitelný napříč všemi moduly runtime technologie .NET, a snižuje, zda neeliminují direktivy podmíněné kompilace specifické pro platformu ve sdíleném kódu.</span><span class="sxs-lookup"><span data-stu-id="dd24d-109">It enables developers to produce code that is usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="dd24d-110">Tato příručka vás provede vytvořením balíčku NuGet, který cílí na .NET Standard knihovny 1,4 nebo zacílení balíčku .NET Framework 4,6.</span><span class="sxs-lookup"><span data-stu-id="dd24d-110">This guide walks you through creating a NuGet package targeting .NET Standard Library 1.4 or a package targeting .NET Framework 4.6.</span></span> <span data-ttu-id="dd24d-111">Knihovna .NET Standard 1,4 funguje napříč .NET Framework 4.6.1, Univerzální platforma Windows 10, .NET Core a mono/Xamarin.</span><span class="sxs-lookup"><span data-stu-id="dd24d-111">A .NET Standard 1.4 library works across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="dd24d-112">Podrobnosti najdete v [tabulce mapování .NET Standard](/dotnet/standard/net-standard#net-implementation-support) (dokumentace rozhraní .NET).</span><span class="sxs-lookup"><span data-stu-id="dd24d-112">For details, see the [.NET Standard mapping table](/dotnet/standard/net-standard#net-implementation-support) (.NET documentation).</span></span> <span data-ttu-id="dd24d-113">Pokud chcete, můžete zvolit jinou verzi knihovny .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="dd24d-113">You can choose other version of the .NET Standard Library if you want.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dd24d-114">Požadavky</span><span class="sxs-lookup"><span data-stu-id="dd24d-114">Prerequisites</span></span>

1. <span data-ttu-id="dd24d-115">Visual Studio 2015 Update 3</span><span class="sxs-lookup"><span data-stu-id="dd24d-115">Visual Studio 2015 Update 3</span></span>
1. <span data-ttu-id="dd24d-116">(Jenom .NET Standard) [.NET Core SDK](https://www.microsoft.com/net/download/)</span><span class="sxs-lookup"><span data-stu-id="dd24d-116">(.NET Standard only) [.NET Core SDK](https://www.microsoft.com/net/download/)</span></span>
1. <span data-ttu-id="dd24d-117">Rozhraní příkazového řádku NuGet</span><span class="sxs-lookup"><span data-stu-id="dd24d-117">NuGet CLI.</span></span> <span data-ttu-id="dd24d-118">Stáhněte si nejnovější verzi nástroje NuGet. exe z [NuGet.org/downloads](https://nuget.org/downloads)a uložte ji do umístění podle vašeho výběru.</span><span class="sxs-lookup"><span data-stu-id="dd24d-118">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="dd24d-119">Pak přidejte toto umístění do proměnné prostředí PATH, pokud ještě není.</span><span class="sxs-lookup"><span data-stu-id="dd24d-119">Then add that location to your PATH environment variable if it isn't already.</span></span>

    > [!Note]
    > <span data-ttu-id="dd24d-120">NuGet. exe je samotný nástroj rozhraní příkazového řádku, nikoli instalační program, proto uložte stažený soubor z prohlížeče namísto jeho spuštění.</span><span class="sxs-lookup"><span data-stu-id="dd24d-120">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-class-library-project"></a><span data-ttu-id="dd24d-121">Vytvořit projekt knihovny tříd</span><span class="sxs-lookup"><span data-stu-id="dd24d-121">Create the class library project</span></span>

1. <span data-ttu-id="dd24d-122">V aplikaci Visual Studio, **soubor > nový > projektu**, rozbalte **uzel C# Visual > Windows** , vyberte možnost **Knihovna tříd (přenosná)** , změňte název na AppLogger a vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="dd24d-122">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and select **OK**.</span></span>

    ![Vytvořit nový projekt knihovny tříd](media/NetStandard-NewProject.png)

1. <span data-ttu-id="dd24d-124">V dialogovém okně **Přidat přenosnou knihovnu tříd** , která se zobrazí, vyberte `.NET Framework 4.6` možnosti `ASP.NET Core 1.0`pro a.</span><span class="sxs-lookup"><span data-stu-id="dd24d-124">In the **Add Portable Class Library** dialog that appears, select the options for `.NET Framework 4.6` and `ASP.NET Core 1.0`.</span></span> <span data-ttu-id="dd24d-125">(Pokud cílíte .NET Framework, můžete vybrat, jaké možnosti jsou vhodné.)</span><span class="sxs-lookup"><span data-stu-id="dd24d-125">(If targeting .NET Framework, you can select whichever options are appropriate.)</span></span>

1. <span data-ttu-id="dd24d-126">Pokud cílíte .NET Standard, klikněte pravým `AppLogger (Portable)` tlačítkem na Průzkumník řešení, vyberte **vlastnosti**, vyberte kartu **Knihovna** a potom v části **cíle** vyberte **target .NET Platform Standard** .</span><span class="sxs-lookup"><span data-stu-id="dd24d-126">If targeting .NET Standard, right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then select  **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="dd24d-127">Tato akce vyzve k potvrzení, po kterém můžete z rozevírací `.NET Standard 1.4` nabídky vybrat (nebo jinou dostupnou verzi):</span><span class="sxs-lookup"><span data-stu-id="dd24d-127">This action prompts for confirmation, after which you can select `.NET Standard 1.4` (or another available version) from the drop down:</span></span>

    ![Nastavení cíle na .NET Standard 1,4](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="dd24d-129">Klikněte na kartu **sestavení** , změňte **konfiguraci** na `Release`a zaškrtněte políčko **soubor dokumentace XML**.</span><span class="sxs-lookup"><span data-stu-id="dd24d-129">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>

1. <span data-ttu-id="dd24d-130">Přidejte do komponenty kód, například:</span><span class="sxs-lookup"><span data-stu-id="dd24d-130">Add your code to the component, for example:</span></span>

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

1. <span data-ttu-id="dd24d-131">Nastavte konfiguraci na vydanou verzi, sestavte projekt a ověřte, jestli se soubory DLL a XML vytvoří `bin\Release` ve složce.</span><span class="sxs-lookup"><span data-stu-id="dd24d-131">Set the configuration to Release, build the project, and check that DLL and XML files are produced within the `bin\Release` folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="dd24d-132">Vytvoření a aktualizace souboru. nuspec</span><span class="sxs-lookup"><span data-stu-id="dd24d-132">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="dd24d-133">Otevřete příkazový řádek, `AppLogger.csproj` přejděte do složky obsahující složku (jedna úroveň níže, `.sln` kde je soubor), a spuštěním příkazu NuGet `spec` vytvořte počáteční `AppLogger.nuspec` soubor:</span><span class="sxs-lookup"><span data-stu-id="dd24d-133">Open a command prompt, navigate to the folder containing `AppLogger.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="dd24d-134">Otevřete `AppLogger.nuspec` v editoru a aktualizujte ho, aby odpovídal následujícímu, a nahraďte YOUR_NAME příslušnou hodnotou.</span><span class="sxs-lookup"><span data-stu-id="dd24d-134">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="dd24d-135">Hodnota konkrétně musí být jedinečná napříč NuGet.org (podívejte se na zásady vytváření názvů popsané v tématu [Vytvoření balíčku.](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) `<id>`</span><span class="sxs-lookup"><span data-stu-id="dd24d-135">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="dd24d-136">Všimněte si také, že je nutné také aktualizovat značky Autor a popis, jinak se zobrazí chyba v průběhu balení.</span><span class="sxs-lookup"><span data-stu-id="dd24d-136">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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

1. <span data-ttu-id="dd24d-137">Přidejte do `.nuspec` souboru referenční sestavení, konkrétně knihovnu DLL knihovny a soubor XML IntelliSense:</span><span class="sxs-lookup"><span data-stu-id="dd24d-137">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    <span data-ttu-id="dd24d-138">Pokud cílíte .NET Standard, zobrazí se podobné položky jako v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="dd24d-138">If targeting .NET Standard, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

    <span data-ttu-id="dd24d-139">Pokud cílíte .NET Framework, zobrazí se podobné položky jako v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="dd24d-139">If targeting .NET Framework, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\net46\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\net46\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="dd24d-140">Klikněte pravým tlačítkem na řešení a vyberte **Sestavit řešení** , aby se vygenerovaly všechny soubory balíčku.</span><span class="sxs-lookup"><span data-stu-id="dd24d-140">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>

### <a name="declaring-dependencies"></a><span data-ttu-id="dd24d-141">Deklarace závislostí</span><span class="sxs-lookup"><span data-stu-id="dd24d-141">Declaring dependencies</span></span>

<span data-ttu-id="dd24d-142">Pokud máte nějaké závislosti na jiných balíčcích NuGet, Seznamte se s `<dependencies>` `<group>` elementy v manifestu elementu.</span><span class="sxs-lookup"><span data-stu-id="dd24d-142">If you have any dependencies on other NuGet packages, list those in the manifest's `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="dd24d-143">Chcete-li například deklarovat závislost na NewtonSoft. JSON 8.0.3 nebo vyšší, přidejte následující:</span><span class="sxs-lookup"><span data-stu-id="dd24d-143">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="dd24d-144">Syntaxe atributu *Version* tady znamená, že je přijatelná verze 8.0.3 nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="dd24d-144">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="dd24d-145">Pokud chcete zadat jiné rozsahy verzí, přečtěte si téma [Správa verzí balíčku](../concepts/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="dd24d-145">To specify different version ranges, refer to [Package versioning](../concepts/package-versioning.md).</span></span>

### <a name="adding-a-readme"></a><span data-ttu-id="dd24d-146">Přidání souboru Readme</span><span class="sxs-lookup"><span data-stu-id="dd24d-146">Adding a readme</span></span>

<span data-ttu-id="dd24d-147">Vytvořte soubor, umístěte ho do kořenové složky projektu a pak na něj `.nuspec` v souboru použijte: `readme.txt`</span><span class="sxs-lookup"><span data-stu-id="dd24d-147">Create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

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

<span data-ttu-id="dd24d-148">Sada Visual Studio `readme.txt` se zobrazí, když se balíček nainstaluje do projektu.</span><span class="sxs-lookup"><span data-stu-id="dd24d-148">Visual Studio display `readme.txt` when the package is installed into a project.</span></span> <span data-ttu-id="dd24d-149">Tento soubor se nezobrazuje při instalaci do projektů .NET Core nebo pro balíčky, které jsou nainstalované jako závislost.</span><span class="sxs-lookup"><span data-stu-id="dd24d-149">The file is not shown when installed into .NET Core projects, or for packages that are installed as a dependency.</span></span>

## <a name="package-the-component"></a><span data-ttu-id="dd24d-150">Zabalení komponenty</span><span class="sxs-lookup"><span data-stu-id="dd24d-150">Package the component</span></span>

<span data-ttu-id="dd24d-151">Po dokončení `.nuspec` odkazů na všechny soubory, které potřebujete zahrnout do balíčku, jste připraveni `pack` spustit příkaz:</span><span class="sxs-lookup"><span data-stu-id="dd24d-151">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack AppLogger.nuspec
```

<span data-ttu-id="dd24d-152">Tím vygenerujete `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="dd24d-152">This generates `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="dd24d-153">Tento soubor otevřete v nástroji, jako je [Průzkumník balíčků NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) , a rozbalením všech uzlů se zobrazí následující obsah (zobrazený pro .NET Standard):</span><span class="sxs-lookup"><span data-stu-id="dd24d-153">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents (shown for .NET Standard):</span></span>

![Průzkumník balíčků NuGet zobrazující balíček AppLogger](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="dd24d-155">`.nupkg` Soubor je pouze soubor zip s jinou příponou.</span><span class="sxs-lookup"><span data-stu-id="dd24d-155">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="dd24d-156">Můžete také prošetřit obsah balíčku, potom změnou `.nupkg` na `.zip`, ale nezapomeňte obnovit rozšíření před nahráním balíčku do NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="dd24d-156">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="dd24d-157">Pokud chcete balíček zpřístupnit ostatním vývojářům, postupujte podle pokynů v tématu [publikování balíčku](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="dd24d-157">To make your package available to other developers, follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="dd24d-158">Všimněte si `pack` , že vyžaduje mono 4.4.2 na Mac OS X a nefunguje v systémech Linux.</span><span class="sxs-lookup"><span data-stu-id="dd24d-158">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="dd24d-159">Na Macu musíte také v `.nuspec` souboru převést cesty Windows na cesty ve stylu systému UNIX.</span><span class="sxs-lookup"><span data-stu-id="dd24d-159">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="related-topics"></a><span data-ttu-id="dd24d-160">Související témata</span><span class="sxs-lookup"><span data-stu-id="dd24d-160">Related topics</span></span>

- [<span data-ttu-id="dd24d-161">odkaz. nuspec</span><span class="sxs-lookup"><span data-stu-id="dd24d-161">.nuspec reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="dd24d-162">Podpora více verzí rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="dd24d-162">Supporting multiple .NET framework versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="dd24d-163">Zahrnutí vlastností MSBuild a cílů do balíčku</span><span class="sxs-lookup"><span data-stu-id="dd24d-163">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="dd24d-164">Vytvoření lokalizovaných balíčků</span><span class="sxs-lookup"><span data-stu-id="dd24d-164">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="dd24d-165">Balíčky symbolů</span><span class="sxs-lookup"><span data-stu-id="dd24d-165">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="dd24d-166">Správa verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="dd24d-166">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="dd24d-167">Dokumentace ke knihovně .NET Standard</span><span class="sxs-lookup"><span data-stu-id="dd24d-167">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="dd24d-168">Přenos do .NET Core z .NET Framework</span><span class="sxs-lookup"><span data-stu-id="dd24d-168">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
