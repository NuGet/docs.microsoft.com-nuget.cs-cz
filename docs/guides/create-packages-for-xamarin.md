---
title: Vytváření balíčků NuGet pro Xamarin (pro iOS, Android a Windows) pomocí sady Visual Studio 2017 nebo 2019
description: Ucelený návod k vytváření balíčků NuGet pro Xamarin, který používá nativní rozhraní API pro iOS, Android a Windows.
author: karann-msft
ms.author: karann
ms.date: 11/05/2019
ms.topic: tutorial
ms.openlocfilehash: 0cb653bad9e853d908039b3f7a94e1dd7eefdde5
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230899"
---
# <a name="create-packages-for-xamarin-with-visual-studio-2017-or-2019"></a><span data-ttu-id="65d06-103">Vytváření balíčků pro Xamarin pomocí sady Visual Studio 2017 nebo 2019</span><span class="sxs-lookup"><span data-stu-id="65d06-103">Create packages for Xamarin with Visual Studio 2017 or 2019</span></span>

<span data-ttu-id="65d06-104">Balíček pro Xamarin obsahuje kód, který používá nativní rozhraní API v systémech iOS, Android a Windows v závislosti na operačním systému za běhu.</span><span class="sxs-lookup"><span data-stu-id="65d06-104">A package for Xamarin contains code that uses native APIs on iOS, Android, and Windows, depending on the run-time operating system.</span></span> <span data-ttu-id="65d06-105">I když je to jednoduché, je vhodnější dát vývojářům využívání tohoto balíčku z knihovny PCL nebo .NET Standard pomocí běžné oblasti rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="65d06-105">Although this is straightforward to do, it's preferable to let developers consume the package from a PCL or .NET Standard libraries through a common API surface area.</span></span>

<span data-ttu-id="65d06-106">V tomto návodu použijete Visual Studio 2017 nebo 2019 k vytvoření balíčku NuGet pro různé platformy, který se dá použít v mobilních projektech pro iOS, Android a Windows.</span><span class="sxs-lookup"><span data-stu-id="65d06-106">In this walkthrough you use Visual Studio 2017 or 2019 to create a cross-platform NuGet package that can be used in mobile projects on iOS, Android, and Windows.</span></span>

1. [<span data-ttu-id="65d06-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="65d06-107">Prerequisites</span></span>](#prerequisites)
1. [<span data-ttu-id="65d06-108">Vytvoření struktury projektu a kódu abstrakce</span><span class="sxs-lookup"><span data-stu-id="65d06-108">Create the project structure and abstraction code</span></span>](#create-the-project-structure-and-abstraction-code)
1. [<span data-ttu-id="65d06-109">Psaní kódu specifického pro platformu</span><span class="sxs-lookup"><span data-stu-id="65d06-109">Write your platform-specific code</span></span>](#write-your-platform-specific-code)
1. [<span data-ttu-id="65d06-110">Vytvoření a aktualizace souboru. nuspec</span><span class="sxs-lookup"><span data-stu-id="65d06-110">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="65d06-111">Zabalení komponenty</span><span class="sxs-lookup"><span data-stu-id="65d06-111">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="65d06-112">Příbuzná témata</span><span class="sxs-lookup"><span data-stu-id="65d06-112">Related topics</span></span>](#related-topics)

## <a name="prerequisites"></a><span data-ttu-id="65d06-113">Požadavky</span><span class="sxs-lookup"><span data-stu-id="65d06-113">Prerequisites</span></span>

1. <span data-ttu-id="65d06-114">Visual Studio 2017 nebo 2019 s Univerzální platforma Windows (UWP) a Xamarin.</span><span class="sxs-lookup"><span data-stu-id="65d06-114">Visual Studio 2017 or 2019 with Universal Windows Platform (UWP) and Xamarin.</span></span> <span data-ttu-id="65d06-115">Nainstalujte si od verze Community Edition zdarma od [VisualStudio.com](https://www.visualstudio.com/); Samozřejmě můžete používat i edice Professional a Enterprise.</span><span class="sxs-lookup"><span data-stu-id="65d06-115">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span> <span data-ttu-id="65d06-116">Chcete-li zahrnout nástroje UWP a Xamarin, vyberte vlastní instalaci a ověřte příslušné možnosti.</span><span class="sxs-lookup"><span data-stu-id="65d06-116">To include UWP and Xamarin tools, select a Custom install and check the appropriate options.</span></span>
1. <span data-ttu-id="65d06-117">Rozhraní příkazového řádku NuGet</span><span class="sxs-lookup"><span data-stu-id="65d06-117">NuGet CLI.</span></span> <span data-ttu-id="65d06-118">Stáhněte si nejnovější verzi nástroje NuGet. exe z [NuGet.org/downloads](https://nuget.org/downloads)a uložte ji do umístění podle vašeho výběru.</span><span class="sxs-lookup"><span data-stu-id="65d06-118">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="65d06-119">Pak přidejte toto umístění do proměnné prostředí PATH, pokud ještě není.</span><span class="sxs-lookup"><span data-stu-id="65d06-119">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="65d06-120">NuGet. exe je samotný nástroj rozhraní příkazového řádku, nikoli instalační program, proto uložte stažený soubor z prohlížeče namísto jeho spuštění.</span><span class="sxs-lookup"><span data-stu-id="65d06-120">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-project-structure-and-abstraction-code"></a><span data-ttu-id="65d06-121">Vytvoření struktury projektu a kódu abstrakce</span><span class="sxs-lookup"><span data-stu-id="65d06-121">Create the project structure and abstraction code</span></span>

1. <span data-ttu-id="65d06-122">Stáhněte a spusťte [rozšíření šablon modulu plug-in .NET Standard pro různé platformy](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) pro Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="65d06-122">Download and run the [Cross-Platform .NET Standard Plugin Templates extension](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) for Visual Studio.</span></span> <span data-ttu-id="65d06-123">Tyto šablony usnadňují vytváření potřebných struktur projektu pro tento návod.</span><span class="sxs-lookup"><span data-stu-id="65d06-123">These templates will make it easy to create the necessary project structure for this walkthrough.</span></span>
1. <span data-ttu-id="65d06-124">V aplikaci Visual Studio 2017, **soubor > nový > projektu**, vyhledejte `Plugin`, vyberte šablonu **modulu plug-in knihovny .NET Standard pro různé platformy** , změňte název na LoggingLibrary a klikněte na OK.</span><span class="sxs-lookup"><span data-stu-id="65d06-124">In Visual Studio 2017, **File > New > Project**, search for `Plugin`, select the **Cross-Platform .NET Standard Library Plugin** template, change the name to LoggingLibrary, and click OK.</span></span>

    ![Nový prázdný projekt aplikace (Xamarin. Forms Portable) v sadě VS 2017](media/CrossPlatform-NewProject.png)

    <span data-ttu-id="65d06-126">V aplikaci Visual Studio 2019, **soubor > nový > projektu**, vyhledejte `Plugin`, vyberte šablonu **modulu plug-in knihovny .NET Standard pro různé platformy** a klikněte na další.</span><span class="sxs-lookup"><span data-stu-id="65d06-126">In Visual Studio 2019, **File > New > Project**, search for `Plugin`, select the **Cross-Platform .NET Standard Library Plugin** template, and click Next.</span></span>

    ![Nový prázdný projekt aplikace (Xamarin. Forms Portable) v sadě VS 2019](media/CrossPlatform-NewProject19-Part1.png)

    <span data-ttu-id="65d06-128">Změňte název na LoggingLibrary a klikněte na vytvořit.</span><span class="sxs-lookup"><span data-stu-id="65d06-128">Change the name to LoggingLibrary, and click Create.</span></span>

    ![Nová prázdná konfigurace aplikace (Xamarin. Forms Portable) ve VS 2019](media/CrossPlatform-NewProject19-Part2.png)

<span data-ttu-id="65d06-130">Výsledné řešení obsahuje dva sdílené projekty společně s nejrůznějšími projekty pro konkrétní platformy:</span><span class="sxs-lookup"><span data-stu-id="65d06-130">The resulting solution contains two Shared projects, along with a variety of platform-specific projects:</span></span>

- <span data-ttu-id="65d06-131">`ILoggingLibrary` projekt, který je obsažen v souboru `ILoggingLibrary.shared.cs`, definuje veřejné rozhraní (oblast rozhraní API) komponenty.</span><span class="sxs-lookup"><span data-stu-id="65d06-131">The `ILoggingLibrary` project, which is contained in the `ILoggingLibrary.shared.cs` file, defines the public interface (the API surface area) of the component.</span></span> <span data-ttu-id="65d06-132">Toto je místo, kde definujete rozhraní do knihovny.</span><span class="sxs-lookup"><span data-stu-id="65d06-132">This is where you define the interface to your library.</span></span>
- <span data-ttu-id="65d06-133">Druhý sdílený projekt obsahuje kód v `CrossLoggingLibrary.shared.cs`, který v době běhu najde implementaci abstraktního rozhraní specifickou pro konkrétní platformu.</span><span class="sxs-lookup"><span data-stu-id="65d06-133">The other Shared project contains code in `CrossLoggingLibrary.shared.cs` that will locate a platform-specific implementation of the abstract interface at run time.</span></span> <span data-ttu-id="65d06-134">Tento soubor obvykle nemusíte měnit.</span><span class="sxs-lookup"><span data-stu-id="65d06-134">You typically don't need to modify this file.</span></span>
- <span data-ttu-id="65d06-135">Projekty specifické pro platformu, například `LoggingLibrary.android.cs`, obsahují nativní implementaci rozhraní v příslušných `LoggingLibraryImplementation.cs` (VS 2017) nebo `LoggingLibrary.<PLATFORM>.cs` (VS 2019) soubory.</span><span class="sxs-lookup"><span data-stu-id="65d06-135">The platform-specific projects, such as `LoggingLibrary.android.cs`, each contain a native implementation of the interface in their respective `LoggingLibraryImplementation.cs` (VS 2017) or `LoggingLibrary.<PLATFORM>.cs` (VS 2019) files.</span></span> <span data-ttu-id="65d06-136">Tady můžete sestavit kód vaší knihovny.</span><span class="sxs-lookup"><span data-stu-id="65d06-136">This is where you build out your library's code.</span></span>

<span data-ttu-id="65d06-137">Ve výchozím nastavení soubor ILoggingLibrary.shared.cs projektu `ILoggingLibrary` obsahuje definici rozhraní, ale žádné metody.</span><span class="sxs-lookup"><span data-stu-id="65d06-137">By default, the ILoggingLibrary.shared.cs file of the `ILoggingLibrary` project contains an interface definition, but no methods.</span></span> <span data-ttu-id="65d06-138">Pro účely tohoto návodu přidejte `Log` metodu následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="65d06-138">For the purposes of this walkthrough, add a `Log` method as follows:</span></span>

```cs
using System;
using System.Collections.Generic;
using System.Text;

namespace Plugin.LoggingLibrary
{
    /// <summary>
    /// Interface for LoggingLibrary
    /// </summary>
    public interface ILoggingLibrary
    {
        /// <summary>
        /// Log a message
        /// </summary>
        void Log(string text);
    }
}
```

## <a name="write-your-platform-specific-code"></a><span data-ttu-id="65d06-139">Psaní kódu specifického pro platformu</span><span class="sxs-lookup"><span data-stu-id="65d06-139">Write your platform-specific code</span></span>

<span data-ttu-id="65d06-140">Chcete-li implementovat implementaci rozhraní `ILoggingLibrary` specifického pro platformu a jeho metody, postupujte následovně:</span><span class="sxs-lookup"><span data-stu-id="65d06-140">To implement a platform-specific implementation of the `ILoggingLibrary` interface and its methods, do the following:</span></span>

1. <span data-ttu-id="65d06-141">Otevřete soubor `LoggingLibraryImplementation.cs` (VS 2017) nebo `LoggingLibrary.<PLATFORM>.cs` (VS 2019) pro každý projekt platformy a přidejte potřebný kód.</span><span class="sxs-lookup"><span data-stu-id="65d06-141">Open the `LoggingLibraryImplementation.cs` (VS 2017) or `LoggingLibrary.<PLATFORM>.cs` (VS 2019) file of each platform project and add the necessary code.</span></span> <span data-ttu-id="65d06-142">Například (použití projektu platformy `Android`):</span><span class="sxs-lookup"><span data-stu-id="65d06-142">For example (using the `Android` platform project):</span></span>

    ```cs
    using System;
    using System.Collections.Generic;
    using System.Text;

    namespace Plugin.LoggingLibrary
    {
        /// <summary>
        /// Implementation for Feature
        /// </summary>
        public class LoggingLibraryImplementation : ILoggingLibrary
        {
            /// <summary>
            /// Log a message
            /// </summary>
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log on Android");
            }
        }
    }
    ```

1. <span data-ttu-id="65d06-143">Tuto implementaci opakujte v projektech pro každou platformu, kterou chcete podporovat.</span><span class="sxs-lookup"><span data-stu-id="65d06-143">Repeat this implementation in the projects for each platform you want to support.</span></span>
1. <span data-ttu-id="65d06-144">Klikněte pravým tlačítkem na řešení a vyberte **Sestavit řešení** , abyste zkontrolovali práci a vytvořili artefakty, které zabalíte jako další.</span><span class="sxs-lookup"><span data-stu-id="65d06-144">Right-click the solution and select **Build Solution** to check your work and produce the artifacts that you package next.</span></span> <span data-ttu-id="65d06-145">Pokud se zobrazí chybové zprávy o chybějících odkazech, klikněte pravým tlačítkem na řešení, vyberte možnost **obnovit balíčky NuGet** a nainstalujte závislosti a znovu sestavte.</span><span class="sxs-lookup"><span data-stu-id="65d06-145">If you get errors about missing references, right-click the solution, select **Restore NuGet Packages** to install dependencies, and rebuild.</span></span>

> [!Note]
> <span data-ttu-id="65d06-146">Pokud používáte sadu Visual Studio 2019, před výběrem možnosti **obnovit balíčky NuGet** a pokusem o opětovné sestavení je třeba změnit verzi `MSBuild.Sdk.Extras` na `2.0.54` v `LoggingLibrary.csproj`.</span><span class="sxs-lookup"><span data-stu-id="65d06-146">If you are using Visual Studio 2019, before selecting **Restore NuGet Packages** and trying to rebuild, you need to change the version of `MSBuild.Sdk.Extras` to `2.0.54` in `LoggingLibrary.csproj`.</span></span> <span data-ttu-id="65d06-147">K tomuto souboru se dá dostat jenom tak, že nejdřív kliknete pravým tlačítkem myši na projekt (pod řešením) a vyberete `Unload Project`, po kterém kliknete pravým tlačítkem na nenačtený projekt a vyberete `Edit LoggingLibrary.csproj`.</span><span class="sxs-lookup"><span data-stu-id="65d06-147">This file can only be accessed by first right-clicking the project (below the solution) and selecting `Unload Project`, after which you right-click on the unloaded project and select `Edit LoggingLibrary.csproj`.</span></span>

> [!Note]
> <span data-ttu-id="65d06-148">Pro sestavení pro iOS budete potřebovat síťovou adresu MAC připojenou k Visual Studiu, jak je popsáno v tématu [Úvod do Xamarin. iOS pro Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span><span class="sxs-lookup"><span data-stu-id="65d06-148">To build for iOS you need a networked Mac connected to Visual Studio as described on [Introduction to Xamarin.iOS for Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span></span> <span data-ttu-id="65d06-149">Pokud nemáte k dispozici počítač Mac, vymažte projekt iOS v nástroji Configuration Manager (krok 3 výše).</span><span class="sxs-lookup"><span data-stu-id="65d06-149">If you don't have a Mac available, clear the iOS project in the configuration manager (step 3 above).</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="65d06-150">Vytvoření a aktualizace souboru. nuspec</span><span class="sxs-lookup"><span data-stu-id="65d06-150">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="65d06-151">Otevřete příkazový řádek, přejděte do složky `LoggingLibrary`, která představuje jednu úroveň níže, kde je `.sln` soubor, a spuštěním příkazu NuGet `spec` vytvořte počáteční soubor `Package.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="65d06-151">Open a command prompt, navigate to the `LoggingLibrary` folder that's one level below where the `.sln` file is, and run the NuGet `spec` command to create the initial `Package.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="65d06-152">Přejmenujte tento soubor na `LoggingLibrary.nuspec` a otevřete ho v editoru.</span><span class="sxs-lookup"><span data-stu-id="65d06-152">Rename this file to `LoggingLibrary.nuspec` and open it in an editor.</span></span>
1. <span data-ttu-id="65d06-153">Aktualizujte soubor tak, aby odpovídal následujícímu, nahraďte YOUR_NAME příslušnou hodnotou.</span><span class="sxs-lookup"><span data-stu-id="65d06-153">Update the file to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="65d06-154">Hodnota `<id>`, konkrétně, musí být jedinečná napříč nuget.org (podívejte se na zásady vytváření názvů popsané v tématu [Vytvoření balíčku](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="65d06-154">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="65d06-155">Všimněte si také, že je nutné také aktualizovat značky Autor a popis, jinak se zobrazí chyba v průběhu balení.</span><span class="sxs-lookup"><span data-stu-id="65d06-155">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>LoggingLibrary.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>LoggingLibrary</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2018</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Tip]
> <span data-ttu-id="65d06-156">Verzi balíčku můžete příponou `-alpha`, `-beta` nebo `-rc` Pokud chcete balíček označit jako předběžnou verzi, Projděte si [předběžné verze verzí](../create-packages/prerelease-packages.md) , kde najdete další informace o předběžných verzích.</span><span class="sxs-lookup"><span data-stu-id="65d06-156">You can suffix your package version with `-alpha`, `-beta` or `-rc` to mark your package as pre-release, check [Pre-release versions](../create-packages/prerelease-packages.md) for more information about pre-release versions.</span></span>

### <a name="add-reference-assemblies"></a><span data-ttu-id="65d06-157">Přidat referenční sestavení</span><span class="sxs-lookup"><span data-stu-id="65d06-157">Add reference assemblies</span></span>

<span data-ttu-id="65d06-158">Chcete-li zahrnout referenční sestavení specifická pro platformu, přidejte následující prvky do `<files>`ho prvku `LoggingLibrary.nuspec` podle potřeby pro podporované platformy:</span><span class="sxs-lookup"><span data-stu-id="65d06-158">To include platform-specific reference assemblies, add the following to the `<files>` element of `LoggingLibrary.nuspec` as appropriate for your supported platforms:</span></span>

```xml
<!-- Insert below <metadata> element -->
<files>
    <!-- Cross-platform reference assemblies -->
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

    <!-- iOS reference assemblies -->
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

    <!-- Android reference assemblies -->
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

    <!-- UWP reference assemblies -->
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
</files>
```

> [!Note]
> <span data-ttu-id="65d06-159">Chcete-li zkrátit názvy knihoven DLL a souborů XML, klikněte pravým tlačítkem na libovolný daný projekt, vyberte kartu **Knihovna** a změňte názvy sestavení.</span><span class="sxs-lookup"><span data-stu-id="65d06-159">To shorten the names of the DLL and XML files, right-click on any given project, select the **Library** tab, and change the assembly names.</span></span>

### <a name="add-dependencies"></a><span data-ttu-id="65d06-160">Přidat závislosti</span><span class="sxs-lookup"><span data-stu-id="65d06-160">Add dependencies</span></span>

<span data-ttu-id="65d06-161">Máte-li specifické závislosti pro nativní implementace, použijte prvek `<dependencies>` s `<group>` prvky pro jejich určení, například:</span><span class="sxs-lookup"><span data-stu-id="65d06-161">If you have specific dependencies for native implementations, use the `<dependencies>` element with `<group>` elements to specify them, for example:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="MonoAndroid">
        <!--MonoAndroid dependencies go here-->
    </group>
    <group targetFramework="Xamarin.iOS10">
        <!--Xamarin.iOS10 dependencies go here-->
    </group>
    <group targetFramework="uap">
        <!--uap dependencies go here-->
    </group>
</dependencies>
```

<span data-ttu-id="65d06-162">Následující příklad by nastavil iTextSharp jako závislost pro cíl UAP:</span><span class="sxs-lookup"><span data-stu-id="65d06-162">For example, the following would set iTextSharp as a dependency for the UAP target:</span></span>

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a><span data-ttu-id="65d06-163">Finální. nuspec</span><span class="sxs-lookup"><span data-stu-id="65d06-163">Final .nuspec</span></span>

<span data-ttu-id="65d06-164">Konečný `.nuspec` soubor by teď měl vypadat nějak takto, kde se znovu YOUR_NAME by se měla nahradit příslušnou hodnotou:</span><span class="sxs-lookup"><span data-stu-id="65d06-164">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>LoggingLibrary.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>LoggingLibrary</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome application logging utility</description>
    <releaseNotes>First release</releaseNotes>
    <copyright>Copyright 2018</copyright>
    <tags>logger logging logs</tags>
        <dependencies>
        <group targetFramework="MonoAndroid">
            <!--MonoAndroid dependencies go here-->
        </group>
        <group targetFramework="Xamarin.iOS10">
            <!--Xamarin.iOS10 dependencies go here-->
        </group>
        <group targetFramework="uap">
            <dependency id="iTextSharp" version="5.5.9" />
        </group>
    </dependencies>
    </metadata>
    <files>
        <!-- Cross-platform reference assemblies -->
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

        <!-- iOS reference assemblies -->
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

        <!-- Android reference assemblies -->
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

        <!-- UWP reference assemblies -->
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
    </files>
</package>
```

## <a name="package-the-component"></a><span data-ttu-id="65d06-165">Zabalení komponenty</span><span class="sxs-lookup"><span data-stu-id="65d06-165">Package the component</span></span>

<span data-ttu-id="65d06-166">Po dokončení `.nuspec` odkazování na všechny soubory, které potřebujete zahrnout do balíčku, jste připraveni ke spuštění příkazu `pack`:</span><span class="sxs-lookup"><span data-stu-id="65d06-166">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack LoggingLibrary.nuspec
```

<span data-ttu-id="65d06-167">Tím se vygeneruje `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="65d06-167">This will generate `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="65d06-168">Tento soubor otevřete v nástroji jako [Průzkumník balíčků NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) a rozbalíte všechny uzly. zobrazí se následující obsah:</span><span class="sxs-lookup"><span data-stu-id="65d06-168">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![Průzkumník balíčků NuGet zobrazující balíček LoggingLibrary](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="65d06-170">Soubor `.nupkg` je pouze soubor ZIP s jinou příponou.</span><span class="sxs-lookup"><span data-stu-id="65d06-170">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="65d06-171">Můžete také prošetřit obsah balíčku, potom změnou `.nupkg` na `.zip`, ale nezapomeňte obnovit rozšíření před nahráním balíčku do nuget.org.</span><span class="sxs-lookup"><span data-stu-id="65d06-171">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="65d06-172">Pokud chcete balíček zpřístupnit ostatním vývojářům, postupujte podle pokynů v tématu [publikování balíčku](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="65d06-172">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="65d06-173">Příbuzná témata</span><span class="sxs-lookup"><span data-stu-id="65d06-173">Related topics</span></span>

- [<span data-ttu-id="65d06-174">Odkaz na nuspec</span><span class="sxs-lookup"><span data-stu-id="65d06-174">Nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="65d06-175">Balíčky symbolů</span><span class="sxs-lookup"><span data-stu-id="65d06-175">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="65d06-176">Správa verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="65d06-176">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="65d06-177">Podpora více verzí .NET Framework</span><span class="sxs-lookup"><span data-stu-id="65d06-177">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="65d06-178">Zahrnutí vlastností MSBuild a cílů do balíčku</span><span class="sxs-lookup"><span data-stu-id="65d06-178">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="65d06-179">Vytvoření lokalizovaných balíčků</span><span class="sxs-lookup"><span data-stu-id="65d06-179">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
