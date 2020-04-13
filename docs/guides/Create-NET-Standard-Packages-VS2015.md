---
title: Vytvoření balíčků Rozhraní .NET Standard a .NET Framework NuGet pomocí sady Visual Studio 2015
description: Komplexní návod k vytváření balíčků .NET Standard a .NET Framework NuGet pomocí nuget3.x a Visual Studio 2015.
author: karann-msft
ms.author: karann
ms.date: 02/02/2018
ms.topic: tutorial
ms.openlocfilehash: b16bf422e2627be3b8516a875d749639734064a9
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "72380726"
---
# <a name="create-net-standard-and-net-framework-packages-with-visual-studio-2015"></a><span data-ttu-id="e90b6-103">Vytvoření balíčků rozhraní .NET Standard a .NET Framework pomocí sady Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="e90b6-103">Create .NET Standard and .NET Framework packages with Visual Studio 2015</span></span>

<span data-ttu-id="e90b6-104">**Poznámka:** Visual Studio 2017 se doporučuje pro vývoj knihoven .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="e90b6-104">**Note:** Visual Studio 2017 is recommended for developing .NET Standard libraries.</span></span> <span data-ttu-id="e90b6-105">Visual Studio 2015 může fungovat, ale nástroje .NET Core byly přeneseny pouze do stavu Náhled.</span><span class="sxs-lookup"><span data-stu-id="e90b6-105">Visual Studio 2015 can work but the .NET Core tooling was brought only to Preview state.</span></span> <span data-ttu-id="e90b6-106">Viz [Vytvoření a publikování balíčku s Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) pro práci s NuGet 4.x+ a Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="e90b6-106">See [Create and publish a package with Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) for working with NuGet 4.x+ and Visual Studio 2017.</span></span>

<span data-ttu-id="e90b6-107">[Standardní knihovna .NET](/dotnet/articles/standard/library) je formální specifikace rozhraní .NET API, která má být k dispozici ve všech runčasech .NET, čímž vytváří větší jednotnost v ekosystému .NET.</span><span class="sxs-lookup"><span data-stu-id="e90b6-107">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="e90b6-108">Standardní knihovna .NET definuje jednotnou sadu rozhraní API BCL (Base Class Library) pro všechny platformy .NET k implementaci, nezávisle na zatížení.</span><span class="sxs-lookup"><span data-stu-id="e90b6-108">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="e90b6-109">Umožňuje vývojářům vytvářet kód, který je použitelný ve všech runčasech .NET, a snižuje, pokud neeliminuje direktivy podmíněné kompilace specifické pro platformu ve sdíleném kódu.</span><span class="sxs-lookup"><span data-stu-id="e90b6-109">It enables developers to produce code that is usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="e90b6-110">Tato příručka vás provede vytvořením balíčku NuGet, který cílí na .NET Standard Library 1.4 nebo balíček zaměřený na rozhraní .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="e90b6-110">This guide walks you through creating a NuGet package targeting .NET Standard Library 1.4 or a package targeting .NET Framework 4.6.</span></span> <span data-ttu-id="e90b6-111">Knihovna .NET Standard 1.4 funguje napříč rozhraním .NET Framework 4.6.1, Univerzální platformou Windows 10, .NET Core a Mono/Xamarin.</span><span class="sxs-lookup"><span data-stu-id="e90b6-111">A .NET Standard 1.4 library works across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="e90b6-112">Podrobnosti naleznete v [tabulce mapování standardu .NET](/dotnet/standard/net-standard#net-implementation-support) (dokumentace k rozhraní.NET).</span><span class="sxs-lookup"><span data-stu-id="e90b6-112">For details, see the [.NET Standard mapping table](/dotnet/standard/net-standard#net-implementation-support) (.NET documentation).</span></span> <span data-ttu-id="e90b6-113">Pokud chcete, můžete zvolit jinou verzi knihovny .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="e90b6-113">You can choose other version of the .NET Standard Library if you want.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e90b6-114">Požadavky</span><span class="sxs-lookup"><span data-stu-id="e90b6-114">Prerequisites</span></span>

1. <span data-ttu-id="e90b6-115">Visual Studio 2015 Update 3</span><span class="sxs-lookup"><span data-stu-id="e90b6-115">Visual Studio 2015 Update 3</span></span>
1. <span data-ttu-id="e90b6-116">(Pouze standard.NET) [Sada SDK jádra .NET](https://www.microsoft.com/net/download/)</span><span class="sxs-lookup"><span data-stu-id="e90b6-116">(.NET Standard only) [.NET Core SDK](https://www.microsoft.com/net/download/)</span></span>
1. <span data-ttu-id="e90b6-117">NuGet CLI.</span><span class="sxs-lookup"><span data-stu-id="e90b6-117">NuGet CLI.</span></span> <span data-ttu-id="e90b6-118">Stáhněte si nejnovější verzi nuget.exe z [nuget.org/downloads](https://nuget.org/downloads)a uložte ji do zvoleného umístění.</span><span class="sxs-lookup"><span data-stu-id="e90b6-118">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="e90b6-119">Pak přidejte toto umístění do proměnné prostředí PATH, pokud ještě není.</span><span class="sxs-lookup"><span data-stu-id="e90b6-119">Then add that location to your PATH environment variable if it isn't already.</span></span>

    > [!Note]
    > <span data-ttu-id="e90b6-120">nuget.exe je samotný nástroj rozhraní příkazového příkazu, nikoli instalátor, takže nezapomeňte uložit stažený soubor z prohlížeče namísto jeho spuštění.</span><span class="sxs-lookup"><span data-stu-id="e90b6-120">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-class-library-project"></a><span data-ttu-id="e90b6-121">Vytvoření projektu knihovny tříd</span><span class="sxs-lookup"><span data-stu-id="e90b6-121">Create the class library project</span></span>

1. <span data-ttu-id="e90b6-122">V sadě Visual Studio rozbal **> >te**uzel **Visual C# > Windows** , vyberte **Knihovnu tříd (Portable),** změňte název na AppLogger a vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="e90b6-122">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and select **OK**.</span></span>

    ![Vytvořit nový projekt knihovny tříd](media/NetStandard-NewProject.png)

1. <span data-ttu-id="e90b6-124">V zobrazeném dialogovém okně **Přidat knihovnu přenosných tříd** vyberte volby pro `.NET Framework 4.6` a `ASP.NET Core 1.0`.</span><span class="sxs-lookup"><span data-stu-id="e90b6-124">In the **Add Portable Class Library** dialog that appears, select the options for `.NET Framework 4.6` and `ASP.NET Core 1.0`.</span></span> <span data-ttu-id="e90b6-125">(Pokud cílení .NET Framework, můžete vybrat podle toho, které možnosti jsou vhodné.)</span><span class="sxs-lookup"><span data-stu-id="e90b6-125">(If targeting .NET Framework, you can select whichever options are appropriate.)</span></span>

1. <span data-ttu-id="e90b6-126">Pokud cílíte na standard `AppLogger (Portable)` .NET, klikněte pravým tlačítkem myši na položku Průzkumník řešení a vyberte **vlastnosti**, vyberte kartu **Knihovna** a v části **Cílení** vyberte **možnost Cílová platforma .NET Standard.**</span><span class="sxs-lookup"><span data-stu-id="e90b6-126">If targeting .NET Standard, right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then select  **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="e90b6-127">Tato akce vyzve k potvrzení, po `.NET Standard 1.4` kterém můžete vybrat (nebo jinou dostupnou verzi) z rozbalovacího programu:</span><span class="sxs-lookup"><span data-stu-id="e90b6-127">This action prompts for confirmation, after which you can select `.NET Standard 1.4` (or another available version) from the drop down:</span></span>

    ![Nastavení cíle na standard .NET 1.4](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="e90b6-129">Klikněte na kartu **Sestavení,** `Release`změňte **konfiguraci** na a zaškrtněte **políčko soubor dokumentace XML**.</span><span class="sxs-lookup"><span data-stu-id="e90b6-129">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>

1. <span data-ttu-id="e90b6-130">Přidejte kód do komponenty, například:</span><span class="sxs-lookup"><span data-stu-id="e90b6-130">Add your code to the component, for example:</span></span>

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

1. <span data-ttu-id="e90b6-131">Nastavte konfiguraci na Release, vytvořte projekt a zkontrolujte, zda `bin\Release` jsou soubory DLL a XML vytvořeny ve složce.</span><span class="sxs-lookup"><span data-stu-id="e90b6-131">Set the configuration to Release, build the project, and check that DLL and XML files are produced within the `bin\Release` folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="e90b6-132">Vytvoření a aktualizace souboru Nuspec</span><span class="sxs-lookup"><span data-stu-id="e90b6-132">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="e90b6-133">Otevřete příkazový řádek, přejděte `AppLogger.csproj` do složky obsahující `.sln` složku (o jednu `spec` úroveň níže, `AppLogger.nuspec` kde je soubor) a spusťte příkaz NuGet a vytvořte počáteční soubor:</span><span class="sxs-lookup"><span data-stu-id="e90b6-133">Open a command prompt, navigate to the folder containing `AppLogger.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="e90b6-134">Otevřete `AppLogger.nuspec` v editoru a aktualizujte jej tak, aby odpovídal následujícímu, a nahrazují YOUR_NAME příslušnou hodnotou.</span><span class="sxs-lookup"><span data-stu-id="e90b6-134">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="e90b6-135">Hodnota, `<id>` konkrétně musí být jedinečný v celé nuget.org (viz konvence pojmenování popsané v [vytvoření balíčku](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="e90b6-135">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="e90b6-136">Všimněte si také, že musíte také aktualizovat značky autora a popisu nebo se během kroku balení zobrazí chyba.</span><span class="sxs-lookup"><span data-stu-id="e90b6-136">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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

1. <span data-ttu-id="e90b6-137">Přidejte do souboru `.nuspec` referenční sestavení, konkrétně knihovnu DLL knihovny a soubor XML technologie IntelliSense:</span><span class="sxs-lookup"><span data-stu-id="e90b6-137">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    <span data-ttu-id="e90b6-138">Pokud cílení .NET Standard, položky se zobrazí podobně jako následující:</span><span class="sxs-lookup"><span data-stu-id="e90b6-138">If targeting .NET Standard, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

    <span data-ttu-id="e90b6-139">Pokud cílení .NET Framework, položky se zobrazí podobně jako následující:</span><span class="sxs-lookup"><span data-stu-id="e90b6-139">If targeting .NET Framework, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\net46\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\net46\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="e90b6-140">Klikněte pravým tlačítkem myši na řešení a vyberte **sestavit řešení** generovat všechny soubory pro balíček.</span><span class="sxs-lookup"><span data-stu-id="e90b6-140">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>

### <a name="declaring-dependencies"></a><span data-ttu-id="e90b6-141">Deklarování závislostí</span><span class="sxs-lookup"><span data-stu-id="e90b6-141">Declaring dependencies</span></span>

<span data-ttu-id="e90b6-142">Pokud máte nějaké závislosti na jiných balíčcích NuGet, `<dependencies>` uveďte `<group>` je v elementu manifestu s prvky.</span><span class="sxs-lookup"><span data-stu-id="e90b6-142">If you have any dependencies on other NuGet packages, list those in the manifest's `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="e90b6-143">Chcete-li například deklarovat závislost na souboru NewtonSoft.Json 8.0.3 nebo vyšší, přidejte následující:</span><span class="sxs-lookup"><span data-stu-id="e90b6-143">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="e90b6-144">Syntaxe atributu *version* zde označuje, že verze 8.0.3 nebo vyšší je přijatelná.</span><span class="sxs-lookup"><span data-stu-id="e90b6-144">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="e90b6-145">Chcete-li určit různé rozsahy verzí, podívejte se na [správa verzí balíčků](../concepts/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="e90b6-145">To specify different version ranges, refer to [Package versioning](../concepts/package-versioning.md).</span></span>

### <a name="adding-a-readme"></a><span data-ttu-id="e90b6-146">Přidání readme</span><span class="sxs-lookup"><span data-stu-id="e90b6-146">Adding a readme</span></span>

<span data-ttu-id="e90b6-147">Vytvořte `readme.txt` soubor, umístěte jej do kořenové složky `.nuspec` projektu a podívejte se na něj v souboru:</span><span class="sxs-lookup"><span data-stu-id="e90b6-147">Create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

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

<span data-ttu-id="e90b6-148">Visual Studio `readme.txt` zobrazit při instalaci balíčku do projektu.</span><span class="sxs-lookup"><span data-stu-id="e90b6-148">Visual Studio display `readme.txt` when the package is installed into a project.</span></span> <span data-ttu-id="e90b6-149">Soubor není zobrazen při instalaci do projektů .NET Core nebo pro balíčky, které jsou nainstalovány jako závislost.</span><span class="sxs-lookup"><span data-stu-id="e90b6-149">The file is not shown when installed into .NET Core projects, or for packages that are installed as a dependency.</span></span>

## <a name="package-the-component"></a><span data-ttu-id="e90b6-150">Balení komponenty</span><span class="sxs-lookup"><span data-stu-id="e90b6-150">Package the component</span></span>

<span data-ttu-id="e90b6-151">S dokončeným `.nuspec` odkazováním na všechny soubory, které potřebujete zahrnout do `pack` balíčku, jste připraveni spustit příkaz:</span><span class="sxs-lookup"><span data-stu-id="e90b6-151">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack AppLogger.nuspec
```

<span data-ttu-id="e90b6-152">To generuje `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="e90b6-152">This generates `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="e90b6-153">Otevření tohoto souboru v nástroji, jako je [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) a rozbalení všech uzlů, uvidíte následující obsah (zobrazeno pro .NET Standard):</span><span class="sxs-lookup"><span data-stu-id="e90b6-153">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents (shown for .NET Standard):</span></span>

![NuGet Package Explorer zobrazující balíček AppLogger](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="e90b6-155">Soubor `.nupkg` je pouze soubor ZIP s jinou příponou.</span><span class="sxs-lookup"><span data-stu-id="e90b6-155">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="e90b6-156">Můžete také prozkoumat obsah balíčku, `.nupkg` `.zip`pak změnou na , ale nezapomeňte obnovit rozšíření před odesláním balíček nuget.org.</span><span class="sxs-lookup"><span data-stu-id="e90b6-156">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="e90b6-157">Chcete-li balíček zpřístupnit ostatním [vývojářům,](../nuget-org/publish-a-package.md)postupujte podle pokynů k části Publikovat balíček .</span><span class="sxs-lookup"><span data-stu-id="e90b6-157">To make your package available to other developers, follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="e90b6-158">Všimněte `pack` si, že vyžaduje Mono 4.4.2 na Mac OS X a nefunguje na systémech Linux.</span><span class="sxs-lookup"><span data-stu-id="e90b6-158">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="e90b6-159">Na Macu musíte také převést názvy cest Windows v souboru `.nuspec` na cesty ve stylu Unixu.</span><span class="sxs-lookup"><span data-stu-id="e90b6-159">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="related-topics"></a><span data-ttu-id="e90b6-160">Související témata</span><span class="sxs-lookup"><span data-stu-id="e90b6-160">Related topics</span></span>

- [<span data-ttu-id="e90b6-161">Odkaz .nuspec</span><span class="sxs-lookup"><span data-stu-id="e90b6-161">.nuspec reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="e90b6-162">Podpora více verzí rozhraní .NET framework</span><span class="sxs-lookup"><span data-stu-id="e90b6-162">Supporting multiple .NET framework versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="e90b6-163">Zahrnout rekvizity a cíle MSBuild do balíčku</span><span class="sxs-lookup"><span data-stu-id="e90b6-163">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="e90b6-164">Vytvoření lokalizovaných balíčků</span><span class="sxs-lookup"><span data-stu-id="e90b6-164">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="e90b6-165">Balíčky symbolů</span><span class="sxs-lookup"><span data-stu-id="e90b6-165">Symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="e90b6-166">Správa verzí balíčku</span><span class="sxs-lookup"><span data-stu-id="e90b6-166">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="e90b6-167">Dokumentace standardní knihovny .NET</span><span class="sxs-lookup"><span data-stu-id="e90b6-167">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="e90b6-168">Přenesení na jádro .NET z rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="e90b6-168">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
