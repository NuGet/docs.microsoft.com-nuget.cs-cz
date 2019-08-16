---
title: Vytváření balíčků NuGet pro Xamarin (pro iOS, Android a Windows) pomocí sady Visual Studio 2015
description: Ucelený návod k vytváření balíčků NuGet pro Xamarin, který používá nativní rozhraní API pro iOS, Android a Windows.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: tutorial
ms.openlocfilehash: 927991429d8d4ce54aa35be3e450475a38141b11
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488916"
---
# <a name="create-packages-for-xamarin-with-visual-studio-2015"></a><span data-ttu-id="6c5ac-103">Vytváření balíčků pro Xamarin pomocí sady Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="6c5ac-103">Create packages for Xamarin with Visual Studio 2015</span></span>

<span data-ttu-id="6c5ac-104">Balíček pro Xamarin obsahuje kód, který používá nativní rozhraní API v systémech iOS, Android a Windows v závislosti na operačním systému za běhu.</span><span class="sxs-lookup"><span data-stu-id="6c5ac-104">A package for Xamarin contains code that uses native APIs on iOS, Android, and Windows, depending on the run-time operating system.</span></span> <span data-ttu-id="6c5ac-105">I když je to jednoduché, je vhodnější dát vývojářům využívání tohoto balíčku z knihovny PCL nebo .NET Standard pomocí běžné oblasti rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="6c5ac-105">Although this is straightforward to do, it's preferable to let developers consume the package from a PCL or .NET Standard libraries through a common API surface area.</span></span>

<span data-ttu-id="6c5ac-106">V tomto návodu použijete Visual Studio 2015 vytvořit balíček NuGet pro různé platformy, který se dá použít v mobilních projektech pro iOS, Android a Windows.</span><span class="sxs-lookup"><span data-stu-id="6c5ac-106">In this walkthrough you use Visual Studio 2015 create a cross-platform NuGet package that can be used in mobile projects on iOS, Android, and Windows.</span></span>

1. [<span data-ttu-id="6c5ac-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="6c5ac-107">Prerequisites</span></span>](#prerequisites)
1. [<span data-ttu-id="6c5ac-108">Vytvoření struktury projektu a kódu abstrakce</span><span class="sxs-lookup"><span data-stu-id="6c5ac-108">Create the project structure and abstraction code</span></span>](#create-the-project-structure-and-abstraction-code)
1. [<span data-ttu-id="6c5ac-109">Psaní kódu specifického pro platformu</span><span class="sxs-lookup"><span data-stu-id="6c5ac-109">Write your platform-specific code</span></span>](#write-your-platform-specific-code)
1. [<span data-ttu-id="6c5ac-110">Vytvoření a aktualizace souboru. nuspec</span><span class="sxs-lookup"><span data-stu-id="6c5ac-110">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="6c5ac-111">Zabalení komponenty</span><span class="sxs-lookup"><span data-stu-id="6c5ac-111">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="6c5ac-112">Příbuzná témata</span><span class="sxs-lookup"><span data-stu-id="6c5ac-112">Related topics</span></span>](#related-topics)

## <a name="prerequisites"></a><span data-ttu-id="6c5ac-113">Požadavky</span><span class="sxs-lookup"><span data-stu-id="6c5ac-113">Prerequisites</span></span>

1. <span data-ttu-id="6c5ac-114">Visual Studio 2015 with Univerzální platforma Windows (UWP) a Xamarin.</span><span class="sxs-lookup"><span data-stu-id="6c5ac-114">Visual Studio 2015 with Universal Windows Platform (UWP) and Xamarin.</span></span> <span data-ttu-id="6c5ac-115">Nainstalujte si od verze Community Edition zdarma od [VisualStudio.com](https://www.visualstudio.com/); Samozřejmě můžete používat i edice Professional a Enterprise.</span><span class="sxs-lookup"><span data-stu-id="6c5ac-115">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span> <span data-ttu-id="6c5ac-116">Chcete-li zahrnout nástroje UWP a Xamarin, vyberte vlastní instalaci a ověřte příslušné možnosti.</span><span class="sxs-lookup"><span data-stu-id="6c5ac-116">To include UWP and Xamarin tools, select a Custom install and check the appropriate options.</span></span>
1. <span data-ttu-id="6c5ac-117">Rozhraní příkazového řádku NuGet</span><span class="sxs-lookup"><span data-stu-id="6c5ac-117">NuGet CLI.</span></span> <span data-ttu-id="6c5ac-118">Stáhněte si nejnovější verzi nástroje NuGet. exe z [NuGet.org/downloads](https://nuget.org/downloads)a uložte ji do umístění podle vašeho výběru.</span><span class="sxs-lookup"><span data-stu-id="6c5ac-118">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="6c5ac-119">Pak přidejte toto umístění do proměnné prostředí PATH, pokud ještě není.</span><span class="sxs-lookup"><span data-stu-id="6c5ac-119">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="6c5ac-120">NuGet. exe je samotný nástroj rozhraní příkazového řádku, nikoli instalační program, proto uložte stažený soubor z prohlížeče namísto jeho spuštění.</span><span class="sxs-lookup"><span data-stu-id="6c5ac-120">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-project-structure-and-abstraction-code"></a><span data-ttu-id="6c5ac-121">Vytvoření struktury projektu a kódu abstrakce</span><span class="sxs-lookup"><span data-stu-id="6c5ac-121">Create the project structure and abstraction code</span></span>

1. <span data-ttu-id="6c5ac-122">Stáhněte a spusťte [modul plug-in pro rozšíření šablon Xamarin](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) pro Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6c5ac-122">Download and run the [Plugin for Xamarin Templates extension](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) for Visual Studio.</span></span> <span data-ttu-id="6c5ac-123">Tyto šablony usnadňují vytváření potřebných struktur projektu pro tento návod.</span><span class="sxs-lookup"><span data-stu-id="6c5ac-123">These templates will make it easy to create the necessary project structure for this walkthrough.</span></span>
1. <span data-ttu-id="6c5ac-124">V aplikaci Visual Studio **soubor > Nový > projekt**, vyhledejte `Plugin`, vyberte **modul plug-in pro Xamarin** , změňte název na LoggingLibrary a klikněte na OK.</span><span class="sxs-lookup"><span data-stu-id="6c5ac-124">In Visual Studio, **File > New > Project**, search for `Plugin`, select the **Plugin for Xamarin** template, change the name to LoggingLibrary, and click OK.</span></span>

    ![Nová prázdná aplikace (Xamarin. Forms Portable) projekt v aplikaci Visual Studio](media/CrossPlatform-NewProject.png)

<span data-ttu-id="6c5ac-126">Výsledné řešení obsahuje dva projekty PCL společně s nejrůznějšími projekty pro konkrétní platformy:</span><span class="sxs-lookup"><span data-stu-id="6c5ac-126">The resulting solution contains two PCL projects, along with a variety of platform-specific projects:</span></span>

- <span data-ttu-id="6c5ac-127">PCL s názvem `Plugin.LoggingLibrary.Abstractions (Portable)`definuje veřejné rozhraní (oblast rozhraní API) komponenty, v tomto `ILoggingLibrary` případě rozhraní obsažené v souboru ILoggingLibrary.cs.</span><span class="sxs-lookup"><span data-stu-id="6c5ac-127">The PCL named `Plugin.LoggingLibrary.Abstractions (Portable)`, defines the public interface (the API surface area) of the component, in this case the `ILoggingLibrary` interface contained in the ILoggingLibrary.cs file.</span></span> <span data-ttu-id="6c5ac-128">Toto je místo, kde definujete rozhraní do knihovny.</span><span class="sxs-lookup"><span data-stu-id="6c5ac-128">This is where you define the interface to your library.</span></span>
- <span data-ttu-id="6c5ac-129">Ostatní PCL, `Plugin.LoggingLibrary (Portable)`obsahuje kód v CrossLoggingLibrary.cs, který v době běhu najde implementaci abstraktního rozhraní specifickou pro konkrétní platformu.</span><span class="sxs-lookup"><span data-stu-id="6c5ac-129">The other PCL, `Plugin.LoggingLibrary (Portable)`, contains code in CrossLoggingLibrary.cs that will locate a platform-specific implementation of the abstract interface at run time.</span></span> <span data-ttu-id="6c5ac-130">Tento soubor obvykle nemusíte měnit.</span><span class="sxs-lookup"><span data-stu-id="6c5ac-130">You typically don't need to modify this file.</span></span>
- <span data-ttu-id="6c5ac-131">Projekty specifické pro platformu, například `Plugin.LoggingLibrary.Android`, obsahují, obsahují nativní implementaci rozhraní v příslušných souborech LoggingLibraryImplementation.cs.</span><span class="sxs-lookup"><span data-stu-id="6c5ac-131">The platform-specific projects, such as `Plugin.LoggingLibrary.Android`, each contain contain a native implementation of the interface in their respective LoggingLibraryImplementation.cs files.</span></span> <span data-ttu-id="6c5ac-132">Tady můžete sestavit kód vaší knihovny.</span><span class="sxs-lookup"><span data-stu-id="6c5ac-132">This is where you build out your library's code.</span></span>

<span data-ttu-id="6c5ac-133">Ve výchozím nastavení soubor ILoggingLibrary.cs projektu abstrakce obsahuje definici rozhraní, ale žádné metody.</span><span class="sxs-lookup"><span data-stu-id="6c5ac-133">By default, the ILoggingLibrary.cs file of the Abstractions project contains an interface definition, but no methods.</span></span> <span data-ttu-id="6c5ac-134">Pro účely tohoto návodu přidejte `Log` metodu následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="6c5ac-134">For the purposes of this walkthrough, add a `Log` method as follows:</span></span>

```cs
using System;

namespace Plugin.LoggingLibrary.Abstractions
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

## <a name="write-your-platform-specific-code"></a><span data-ttu-id="6c5ac-135">Psaní kódu specifického pro platformu</span><span class="sxs-lookup"><span data-stu-id="6c5ac-135">Write your platform-specific code</span></span>

<span data-ttu-id="6c5ac-136">Chcete-li implementovat implementaci `ILoggingLibrary` rozhraní a jeho metod specifickou pro konkrétní platformu, udělejte toto:</span><span class="sxs-lookup"><span data-stu-id="6c5ac-136">To implement a platform-specific implementation of the `ILoggingLibrary` interface and its methods, do the following:</span></span>

1. <span data-ttu-id="6c5ac-137">`LoggingLibraryImplementation.cs` Otevřete soubor pro každý projekt platformy a přidejte potřebný kód.</span><span class="sxs-lookup"><span data-stu-id="6c5ac-137">Open the `LoggingLibraryImplementation.cs` file of each platform project and add the necessary code.</span></span> <span data-ttu-id="6c5ac-138">Například (použití `Plugin.LoggingLibrary.Android` projektu):</span><span class="sxs-lookup"><span data-stu-id="6c5ac-138">For example (using the `Plugin.LoggingLibrary.Android` project):</span></span>

    ```cs
    using Plugin.LoggingLibrary.Abstractions;
    using System;

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

1. <span data-ttu-id="6c5ac-139">Tuto implementaci opakujte v projektech pro každou platformu, kterou chcete podporovat.</span><span class="sxs-lookup"><span data-stu-id="6c5ac-139">Repeat this implementation in the projects for each platform you want to support.</span></span>
1. <span data-ttu-id="6c5ac-140">Klikněte pravým tlačítkem na projekt pro iOS, vyberte **vlastnosti**, klikněte na kartu **sestavení** a odeberte "\iPhone" z **výstupní cesty** a nastavení **souboru dokumentace XML** .</span><span class="sxs-lookup"><span data-stu-id="6c5ac-140">Right-click the iOS project, select **Properties**, click the **Build** tab, and remove "\iPhone" from the **Output path** and **XML documentation file** settings.</span></span> <span data-ttu-id="6c5ac-141">To je jenom pro pozdější pohodlí v tomto návodu.</span><span class="sxs-lookup"><span data-stu-id="6c5ac-141">This is just for later convenience in this walkthrough.</span></span> <span data-ttu-id="6c5ac-142">Po dokončení soubor uložte.</span><span class="sxs-lookup"><span data-stu-id="6c5ac-142">Save the file when done.</span></span>
1. <span data-ttu-id="6c5ac-143">Klikněte pravým tlačítkem na řešení, vyberte **Configuration Manager...** a zaškrtněte políčka **sestavení** pro PCLS a každou platformu, kterou podporujete.</span><span class="sxs-lookup"><span data-stu-id="6c5ac-143">Right-click the solution, select **Configuration Manager...**, and check the **Build** boxes for the PCLs and each platform you're supporting.</span></span>
1. <span data-ttu-id="6c5ac-144">Klikněte pravým tlačítkem na řešení a vyberte **Sestavit řešení** , abyste zkontrolovali práci a vytvořili artefakty, které zabalíte jako další.</span><span class="sxs-lookup"><span data-stu-id="6c5ac-144">Right-click the solution and select **Build Solution** to check your work and produce the artifacts that you package next.</span></span> <span data-ttu-id="6c5ac-145">Pokud se zobrazí chybové zprávy o chybějících odkazech, klikněte pravým tlačítkem na řešení, vyberte možnost **obnovit balíčky NuGet** a nainstalujte závislosti a znovu sestavte.</span><span class="sxs-lookup"><span data-stu-id="6c5ac-145">If you get errors about missing references, right-click the solution, select **Restore NuGet Packages** to install dependencies, and rebuild.</span></span>

> [!Note]
> <span data-ttu-id="6c5ac-146">Pro sestavení pro iOS budete potřebovat síťovou adresu MAC připojenou k Visual Studiu, jak je popsáno v tématu [Úvod do Xamarin. iOS pro Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span><span class="sxs-lookup"><span data-stu-id="6c5ac-146">To build for iOS you need a networked Mac connected to Visual Studio as described on [Introduction to Xamarin.iOS for Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span></span> <span data-ttu-id="6c5ac-147">Pokud nemáte k dispozici počítač Mac, vymažte projekt iOS v nástroji Configuration Manager (krok 3 výše).</span><span class="sxs-lookup"><span data-stu-id="6c5ac-147">If you don't have a Mac available, clear the iOS project in the configuration manager (step 3 above).</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="6c5ac-148">Vytvoření a aktualizace souboru. nuspec</span><span class="sxs-lookup"><span data-stu-id="6c5ac-148">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="6c5ac-149">Otevřete příkazový `LoggingLibrary` řádek, přejděte do složky, která je na jednu úroveň níže, `.sln` kde je soubor, a spuštěním příkazu NuGet `spec` vytvořte počáteční `Package.nuspec` soubor:</span><span class="sxs-lookup"><span data-stu-id="6c5ac-149">Open a command prompt, navigate to the `LoggingLibrary` folder that's one level below where the `.sln` file is, and run the NuGet `spec` command to create the initial `Package.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="6c5ac-150">Přejmenujte tento `LoggingLibrary.nuspec` soubor na a otevřete ho v editoru.</span><span class="sxs-lookup"><span data-stu-id="6c5ac-150">Rename this file to `LoggingLibrary.nuspec` and open it in an editor.</span></span>
1. <span data-ttu-id="6c5ac-151">Aktualizujte soubor tak, aby odpovídal následujícímu, nahraďte YOUR_NAME příslušnou hodnotou.</span><span class="sxs-lookup"><span data-stu-id="6c5ac-151">Update the file to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="6c5ac-152">Hodnota konkrétně musí být jedinečná napříč NuGet.org (podívejte se na zásady vytváření názvů popsané v tématu [Vytvoření balíčku).](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) `<id>`</span><span class="sxs-lookup"><span data-stu-id="6c5ac-152">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="6c5ac-153">Všimněte si také, že je nutné také aktualizovat značky Autor a popis, jinak se zobrazí chyba v průběhu balení.</span><span class="sxs-lookup"><span data-stu-id="6c5ac-153">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
        <copyright>Copyright 2016</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Tip]
> <span data-ttu-id="6c5ac-154">Verzi `-alpha`balíčku můžete příponou, `-beta` nebo `-rc` Chcete-li označit balíček jako předběžnou verzi, Projděte si předběžné verze [verzí](../create-packages/prerelease-packages.md) , kde najdete další informace o předběžných verzích.</span><span class="sxs-lookup"><span data-stu-id="6c5ac-154">You can suffix your package version with `-alpha`, `-beta` or `-rc` to mark your package as pre-release, check [Pre-release versions](../create-packages/prerelease-packages.md) for more information about pre-release versions.</span></span>

### <a name="add-reference-assemblies"></a><span data-ttu-id="6c5ac-155">Přidat referenční sestavení</span><span class="sxs-lookup"><span data-stu-id="6c5ac-155">Add reference assemblies</span></span>

<span data-ttu-id="6c5ac-156">Chcete-li zahrnout referenční sestavení specifická pro platformu, přidejte následující `<files>` `LoggingLibrary.nuspec` prvky, které jsou vhodné pro podporované platformy:</span><span class="sxs-lookup"><span data-stu-id="6c5ac-156">To include platform-specific reference assemblies, add the following to the `<files>` element of `LoggingLibrary.nuspec` as appropriate for your supported platforms:</span></span>

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
> <span data-ttu-id="6c5ac-157">Chcete-li zkrátit názvy knihoven DLL a souborů XML, klikněte pravým tlačítkem na libovolný daný projekt, vyberte kartu **Knihovna** a změňte názvy sestavení.</span><span class="sxs-lookup"><span data-stu-id="6c5ac-157">To shorten the names of the DLL and XML files, right-click on any given project, select the **Library** tab, and change the assembly names.</span></span>

### <a name="add-dependencies"></a><span data-ttu-id="6c5ac-158">Přidat závislosti</span><span class="sxs-lookup"><span data-stu-id="6c5ac-158">Add dependencies</span></span>

<span data-ttu-id="6c5ac-159">Máte-li specifické závislosti pro nativní implementace, použijte `<dependencies>` element s `<group>` prvky pro jejich určení, například:</span><span class="sxs-lookup"><span data-stu-id="6c5ac-159">If you have specific dependencies for native implementations, use the `<dependencies>` element with `<group>` elements to specify them, for example:</span></span>

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

<span data-ttu-id="6c5ac-160">Následující příklad by nastavil iTextSharp jako závislost pro cíl UAP:</span><span class="sxs-lookup"><span data-stu-id="6c5ac-160">For example, the following would set iTextSharp as a dependency for the UAP target:</span></span>

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a><span data-ttu-id="6c5ac-161">Finální. nuspec</span><span class="sxs-lookup"><span data-stu-id="6c5ac-161">Final .nuspec</span></span>

<span data-ttu-id="6c5ac-162">Konečný `.nuspec` soubor by teď měl vypadat nějak takto, kde znovu YOUR_NAME by mělo být nahrazeno příslušnou hodnotou:</span><span class="sxs-lookup"><span data-stu-id="6c5ac-162">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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
    <copyright>Copyright 2016</copyright>
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

## <a name="package-the-component"></a><span data-ttu-id="6c5ac-163">Zabalení komponenty</span><span class="sxs-lookup"><span data-stu-id="6c5ac-163">Package the component</span></span>

<span data-ttu-id="6c5ac-164">Po dokončení `.nuspec` odkazů na všechny soubory, které potřebujete zahrnout do balíčku, jste připraveni `pack` spustit příkaz:</span><span class="sxs-lookup"><span data-stu-id="6c5ac-164">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack LoggingLibrary.nuspec
```

<span data-ttu-id="6c5ac-165">Tím se vygeneruje `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="6c5ac-165">This will generate `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="6c5ac-166">Tento soubor otevřete v nástroji jako [Průzkumník balíčků NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) a rozbalíte všechny uzly. zobrazí se následující obsah:</span><span class="sxs-lookup"><span data-stu-id="6c5ac-166">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![Průzkumník balíčků NuGet zobrazující balíček LoggingLibrary](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="6c5ac-168">`.nupkg` Soubor je pouze soubor zip s jinou příponou.</span><span class="sxs-lookup"><span data-stu-id="6c5ac-168">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="6c5ac-169">Můžete také prošetřit obsah balíčku, potom změnou `.nupkg` na `.zip`, ale nezapomeňte obnovit rozšíření před nahráním balíčku do NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="6c5ac-169">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="6c5ac-170">Pokud chcete balíček zpřístupnit ostatním vývojářům, postupujte podle pokynů v tématu [publikování balíčku](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="6c5ac-170">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="6c5ac-171">Související témata</span><span class="sxs-lookup"><span data-stu-id="6c5ac-171">Related topics</span></span>

- [<span data-ttu-id="6c5ac-172">Odkaz na nuspec</span><span class="sxs-lookup"><span data-stu-id="6c5ac-172">Nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="6c5ac-173">Balíčky symbolů</span><span class="sxs-lookup"><span data-stu-id="6c5ac-173">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="6c5ac-174">Správa verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="6c5ac-174">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="6c5ac-175">Podpora více verzí .NET Framework</span><span class="sxs-lookup"><span data-stu-id="6c5ac-175">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="6c5ac-176">Zahrnutí vlastností MSBuild a cílů do balíčku</span><span class="sxs-lookup"><span data-stu-id="6c5ac-176">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="6c5ac-177">Vytvoření lokalizovaných balíčků</span><span class="sxs-lookup"><span data-stu-id="6c5ac-177">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)