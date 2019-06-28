---
title: Vytváření balíčků NuGet pro Xamarin pomocí sady Visual Studio 2015 (pro iOS, Android a Windows)
description: Návod začátku do konce vytváření balíčků NuGet pro Xamarin pomocí nativních rozhraní API v iOS, Android a Windows.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: tutorial
ms.openlocfilehash: d737b70febd1e18aa8a39cc73a9a9cf333f758c6
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426844"
---
# <a name="create-packages-for-xamarin-with-visual-studio-2015"></a><span data-ttu-id="03766-103">Vytváření balíčků pro Xamarin pomocí sady Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="03766-103">Create packages for Xamarin with Visual Studio 2015</span></span>

<span data-ttu-id="03766-104">Balíček pro Xamarin obsahuje kód, který používá nativní rozhraní API v iOS, Android a Windows, v závislosti na operačním systému za běhu.</span><span class="sxs-lookup"><span data-stu-id="03766-104">A package for Xamarin contains code that uses native APIs on iOS, Android, and Windows, depending on the run-time operating system.</span></span> <span data-ttu-id="03766-105">I když je to jednoduchý postup, je vhodnější umožňují vývojářům využívat balíček z PCL nebo plocha knihovny .NET Standard prostřednictvím společného rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="03766-105">Although this is straightforward to do, it's preferable to let developers consume the package from a PCL or .NET Standard libraries through a common API surface area.</span></span>

<span data-ttu-id="03766-106">V tomto názorném postupu, který používáte Visual Studio 2015 vytvořte balíček NuGet napříč platformami, která lze použít v mobilních projektů na iOS, Android a Windows.</span><span class="sxs-lookup"><span data-stu-id="03766-106">In this walkthrough you use Visual Studio 2015 create a cross-platform NuGet package that can be used in mobile projects on iOS, Android, and Windows.</span></span>

1. [<span data-ttu-id="03766-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="03766-107">Prerequisites</span></span>](#prerequisites)
1. [<span data-ttu-id="03766-108">Vytvoření projektu strukturu a abstrakce kódu</span><span class="sxs-lookup"><span data-stu-id="03766-108">Create the project structure and abstraction code</span></span>](#create-the-project-structure-and-abstraction-code)
1. [<span data-ttu-id="03766-109">Napište svůj kód specifický pro platformu</span><span class="sxs-lookup"><span data-stu-id="03766-109">Write your platform-specific code</span></span>](#write-your-platform-specific-code)
1. [<span data-ttu-id="03766-110">Vytvoření a aktualizaci souboru .nuspec souboru</span><span class="sxs-lookup"><span data-stu-id="03766-110">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="03766-111">Balíček komponenty</span><span class="sxs-lookup"><span data-stu-id="03766-111">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="03766-112">Související témata</span><span class="sxs-lookup"><span data-stu-id="03766-112">Related topics</span></span>](#related-topics)

## <a name="prerequisites"></a><span data-ttu-id="03766-113">Požadavky</span><span class="sxs-lookup"><span data-stu-id="03766-113">Prerequisites</span></span>

1. <span data-ttu-id="03766-114">Visual Studio 2015 s platformou Universal Windows (UPW) a Xamarin.</span><span class="sxs-lookup"><span data-stu-id="03766-114">Visual Studio 2015 with Universal Windows Platform (UWP) and Xamarin.</span></span> <span data-ttu-id="03766-115">Instalace edice Community zdarma z [visualstudio.com](https://www.visualstudio.com/); samozřejmě můžete také, edice Professional a Enterprise.</span><span class="sxs-lookup"><span data-stu-id="03766-115">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span> <span data-ttu-id="03766-116">Aby byly nástroje pro UPW a Xamarin, vyberte vlastní instalaci a zkontrolujte příslušné možnosti.</span><span class="sxs-lookup"><span data-stu-id="03766-116">To include UWP and Xamarin tools, select a Custom install and check the appropriate options.</span></span>
1. <span data-ttu-id="03766-117">Rozhraní příkazového řádku NuGet.</span><span class="sxs-lookup"><span data-stu-id="03766-117">NuGet CLI.</span></span> <span data-ttu-id="03766-118">Stažení nejnovější verze programu nuget.exe z [nuget.org/downloads](https://nuget.org/downloads), ukládání do umístění podle vašeho výběru.</span><span class="sxs-lookup"><span data-stu-id="03766-118">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="03766-119">Pak přidejte toto umístění do proměnné prostředí PATH, pokud ještě není.</span><span class="sxs-lookup"><span data-stu-id="03766-119">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="03766-120">nuget.exe je že nástroj příkazového řádku, není instalační program, proto ji nezapomeňte Uložte stažený soubor ve svém prohlížeči místo jeho spuštění.</span><span class="sxs-lookup"><span data-stu-id="03766-120">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-project-structure-and-abstraction-code"></a><span data-ttu-id="03766-121">Vytvoření projektu strukturu a abstrakce kódu</span><span class="sxs-lookup"><span data-stu-id="03766-121">Create the project structure and abstraction code</span></span>

1. <span data-ttu-id="03766-122">Stáhněte a spusťte [modul plug-in pro rozšíření Xamarin šablony](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) pro sadu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="03766-122">Download and run the [Plugin for Xamarin Templates extension](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) for Visual Studio.</span></span> <span data-ttu-id="03766-123">Tyto šablony se usnadňují vytváření struktury projektu potřebné pro tento návod.</span><span class="sxs-lookup"><span data-stu-id="03766-123">These templates will make it easy to create the necessary project structure for this walkthrough.</span></span>
1. <span data-ttu-id="03766-124">V sadě Visual Studio **soubor > Nový > projekt**, vyhledejte `Plugin`, vyberte **modul plug-in pro Xamarin** šablony, změňte název na LoggingLibrary a klikněte na tlačítko OK.</span><span class="sxs-lookup"><span data-stu-id="03766-124">In Visual Studio, **File > New > Project**, search for `Plugin`, select the **Plugin for Xamarin** template, change the name to LoggingLibrary, and click OK.</span></span>

    ![Nový projekt prázdná aplikace (Xamarin.Forms přenosná) v sadě Visual Studio](media/CrossPlatform-NewProject.png)

<span data-ttu-id="03766-126">Výsledný řešení obsahuje dva projekty PCL, spolu s celou řadu projektů specifické pro platformu:</span><span class="sxs-lookup"><span data-stu-id="03766-126">The resulting solution contains two PCL projects, along with a variety of platform-specific projects:</span></span>

- <span data-ttu-id="03766-127">PCL s názvem `Plugin.LoggingLibrary.Abstractions (Portable)`, definuje veřejné rozhraní (svrchní oblasti rozhraní API) komponenty, v tomto případě `ILoggingLibrary` obsažené v souboru ILoggingLibrary.cs rozhraní.</span><span class="sxs-lookup"><span data-stu-id="03766-127">The PCL named `Plugin.LoggingLibrary.Abstractions (Portable)`, defines the public interface (the API surface area) of the component, in this case the `ILoggingLibrary` interface contained in the ILoggingLibrary.cs file.</span></span> <span data-ttu-id="03766-128">Toto je tady můžete definovat rozhraní do knihovny.</span><span class="sxs-lookup"><span data-stu-id="03766-128">This is where you define the interface to your library.</span></span>
- <span data-ttu-id="03766-129">Další PCL `Plugin.LoggingLibrary (Portable)`, obsahuje kód v CrossLoggingLibrary.cs, který bude vyhledávat konkrétní platformy implementaci abstraktní rozhraní v době běhu.</span><span class="sxs-lookup"><span data-stu-id="03766-129">The other PCL, `Plugin.LoggingLibrary (Portable)`, contains code in CrossLoggingLibrary.cs that will locate a platform-specific implementation of the abstract interface at run time.</span></span> <span data-ttu-id="03766-130">Obvykle není nutné k úpravě tohoto souboru.</span><span class="sxs-lookup"><span data-stu-id="03766-130">You typically don't need to modify this file.</span></span>
- <span data-ttu-id="03766-131">Projekty konkrétní platformy, jako například `Plugin.LoggingLibrary.Android`každá obsahovat obsahovat nativní implementace rozhraní v jejich příslušných LoggingLibraryImplementation.cs soubory.</span><span class="sxs-lookup"><span data-stu-id="03766-131">The platform-specific projects, such as `Plugin.LoggingLibrary.Android`, each contain contain a native implementation of the interface in their respective LoggingLibraryImplementation.cs files.</span></span> <span data-ttu-id="03766-132">To je, ve kterém sestavujete své knihovny kódu.</span><span class="sxs-lookup"><span data-stu-id="03766-132">This is where you build out your library's code.</span></span>

<span data-ttu-id="03766-133">Ve výchozím souboru ILoggingLibrary.cs abstrakce projektu obsahuje definice rozhraní, ale žádné metody.</span><span class="sxs-lookup"><span data-stu-id="03766-133">By default, the ILoggingLibrary.cs file of the Abstractions project contains an interface definition, but no methods.</span></span> <span data-ttu-id="03766-134">Pro účely tohoto návodu, přidejte `Log` metodu následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="03766-134">For the purposes of this walkthrough, add a `Log` method as follows:</span></span>

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

## <a name="write-your-platform-specific-code"></a><span data-ttu-id="03766-135">Napište svůj kód specifický pro platformu</span><span class="sxs-lookup"><span data-stu-id="03766-135">Write your platform-specific code</span></span>

<span data-ttu-id="03766-136">K implementaci specifické pro platformu provádění `ILoggingLibrary` rozhraní a jeho metody, postupujte takto:</span><span class="sxs-lookup"><span data-stu-id="03766-136">To implement a platform-specific implementation of the `ILoggingLibrary` interface and its methods, do the following:</span></span>

1. <span data-ttu-id="03766-137">Otevřít `LoggingLibraryImplementation.cs` souboru pro každou platformu projektu a přidání nezbytného kódu.</span><span class="sxs-lookup"><span data-stu-id="03766-137">Open the `LoggingLibraryImplementation.cs` file of each platform project and add the necessary code.</span></span> <span data-ttu-id="03766-138">Příklad (použití `Plugin.LoggingLibrary.Android` projektu):</span><span class="sxs-lookup"><span data-stu-id="03766-138">For example (using the `Plugin.LoggingLibrary.Android` project):</span></span>

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

1. <span data-ttu-id="03766-139">Tato implementace v projektech opakujte pro každou platformu, kterou chcete podporovat.</span><span class="sxs-lookup"><span data-stu-id="03766-139">Repeat this implementation in the projects for each platform you want to support.</span></span>
1. <span data-ttu-id="03766-140">Klikněte pravým tlačítkem na projekt pro iOS, vyberte **vlastnosti**, klikněte na tlačítko **sestavení** kartu a odebrání "\iPhone" **výstupní cesta** a **soubor dokumentace XML**  nastavení.</span><span class="sxs-lookup"><span data-stu-id="03766-140">Right-click the iOS project, select **Properties**, click the **Build** tab, and remove "\iPhone" from the **Output path** and **XML documentation file** settings.</span></span> <span data-ttu-id="03766-141">Toto platí jenom pro pohodlí dále v tomto názorném postupu.</span><span class="sxs-lookup"><span data-stu-id="03766-141">This is just for later convenience in this walkthrough.</span></span> <span data-ttu-id="03766-142">Po dokončení soubor uložte.</span><span class="sxs-lookup"><span data-stu-id="03766-142">Save the file when done.</span></span>
1. <span data-ttu-id="03766-143">Klikněte pravým tlačítkem na řešení, vyberte **nástroje Configuration Manager...** a zkontrolujte **sestavení** polí PCLs a jednotlivé platformy, které podporujete.</span><span class="sxs-lookup"><span data-stu-id="03766-143">Right-click the solution, select **Configuration Manager...**, and check the **Build** boxes for the PCLs and each platform you're supporting.</span></span>
1. <span data-ttu-id="03766-144">Klikněte pravým tlačítkem na řešení a vyberte **sestavit řešení** zkontrolujte svou práci a vytvoří artefakty, které můžete dále balíček.</span><span class="sxs-lookup"><span data-stu-id="03766-144">Right-click the solution and select **Build Solution** to check your work and produce the artifacts that you package next.</span></span> <span data-ttu-id="03766-145">Pokud se zobrazí chyby týkající se chybějící odkazy, klikněte pravým tlačítkem na řešení, vyberte **obnovit balíčky NuGet** instalace závislosti a sestavte znovu.</span><span class="sxs-lookup"><span data-stu-id="03766-145">If you get errors about missing references, right-click the solution, select **Restore NuGet Packages** to install dependencies, and rebuild.</span></span>

> [!Note]
> <span data-ttu-id="03766-146">K vývoji pro iOS budete potřebovat síťově připojeného počítače Mac připojené k sadě Visual Studio, jak je popsáno v [Úvod k Xamarin.iosu pro Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span><span class="sxs-lookup"><span data-stu-id="03766-146">To build for iOS you need a networked Mac connected to Visual Studio as described on [Introduction to Xamarin.iOS for Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span></span> <span data-ttu-id="03766-147">Pokud nemáte k dispozici na Macu, zrušte zaškrtnutí políčka projektu pro iOS v configuration Manageru (krok 3 výše).</span><span class="sxs-lookup"><span data-stu-id="03766-147">If you don't have a Mac available, clear the iOS project in the configuration manager (step 3 above).</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="03766-148">Vytvoření a aktualizaci souboru .nuspec souboru</span><span class="sxs-lookup"><span data-stu-id="03766-148">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="03766-149">Otevřete příkazový řádek, přejděte na `LoggingLibrary` složku, která je jednu úroveň pod where `.sln` soubor a spusťte NuGet `spec` příkaz pro vytvoření počáteční `Package.nuspec` souboru:</span><span class="sxs-lookup"><span data-stu-id="03766-149">Open a command prompt, navigate to the `LoggingLibrary` folder that's one level below where the `.sln` file is, and run the NuGet `spec` command to create the initial `Package.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="03766-150">Přejmenujte tento soubor na `LoggingLibrary.nuspec` a otevřít ji v editoru.</span><span class="sxs-lookup"><span data-stu-id="03766-150">Rename this file to `LoggingLibrary.nuspec` and open it in an editor.</span></span>
1. <span data-ttu-id="03766-151">Aktualizace souboru tak, aby odpovídala následující příkaz, nahradíte vaše_jméno odpovídající hodnotu.</span><span class="sxs-lookup"><span data-stu-id="03766-151">Update the file to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="03766-152">`<id>` , Konkrétně musí být hodnota jedinečná napříč nuget.org (naleznete v tématu Zásady vytváření názvů je popsáno v [vytvoření balíčku](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="03766-152">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="03766-153">Všimněte si také, že budete muset taky aktualizovat Autor a popis značky nebo dojde k chybě během kroku balení.</span><span class="sxs-lookup"><span data-stu-id="03766-153">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
> <span data-ttu-id="03766-154">Můžete příponu verzi balíčku `-alpha`, `-beta` nebo `-rc` označit jako předběžné verze balíčku, zkontrolujte [předběžných verzí](../create-packages/prerelease-packages.md) Další informace o předběžných verzích.</span><span class="sxs-lookup"><span data-stu-id="03766-154">You can suffix your package version with `-alpha`, `-beta` or `-rc` to mark your package as pre-release, check [Pre-release versions](../create-packages/prerelease-packages.md) for more information about pre-release versions.</span></span>

### <a name="add-reference-assemblies"></a><span data-ttu-id="03766-155">Přidat odkaz na sestavení</span><span class="sxs-lookup"><span data-stu-id="03766-155">Add reference assemblies</span></span>

<span data-ttu-id="03766-156">Chcete-li zahrnout odkaz na konkrétní platformu sestavení, přidejte následující text do `<files>` prvek `LoggingLibrary.nuspec` odpovídajícím způsobem pro podporované platformy:</span><span class="sxs-lookup"><span data-stu-id="03766-156">To include platform-specific reference assemblies, add the following to the `<files>` element of `LoggingLibrary.nuspec` as appropriate for your supported platforms:</span></span>

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
> <span data-ttu-id="03766-157">Zkraťte názvy souborů knihovny DLL a XML, klikněte pravým tlačítkem na každého projektu, vyberte **knihovny** kartu a změnit názvy sestavení.</span><span class="sxs-lookup"><span data-stu-id="03766-157">To shorten the names of the DLL and XML files, right-click on any given project, select the **Library** tab, and change the assembly names.</span></span>

### <a name="add-dependencies"></a><span data-ttu-id="03766-158">Přidat závislosti</span><span class="sxs-lookup"><span data-stu-id="03766-158">Add dependencies</span></span>

<span data-ttu-id="03766-159">Pokud máte konkrétní závislosti pro nativní implementace, použijte `<dependencies>` element s `<group>` prvků, které mají být zadány, například:</span><span class="sxs-lookup"><span data-stu-id="03766-159">If you have specific dependencies for native implementations, use the `<dependencies>` element with `<group>` elements to specify them, for example:</span></span>

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

<span data-ttu-id="03766-160">Například následující byste nastavili iTextSharp jako závislost pro cíl UAP:</span><span class="sxs-lookup"><span data-stu-id="03766-160">For example, the following would set iTextSharp as a dependency for the UAP target:</span></span>

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a><span data-ttu-id="03766-161">Poslední souboru .nuspec</span><span class="sxs-lookup"><span data-stu-id="03766-161">Final .nuspec</span></span>

<span data-ttu-id="03766-162">Výsledná `.nuspec` soubor by teď měl vypadat jako následující, kde znovu vaše_jméno by měla být nahrazena odpovídající hodnotu:</span><span class="sxs-lookup"><span data-stu-id="03766-162">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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

## <a name="package-the-component"></a><span data-ttu-id="03766-163">Balíček komponenty</span><span class="sxs-lookup"><span data-stu-id="03766-163">Package the component</span></span>

<span data-ttu-id="03766-164">S dokončenou `.nuspec` odkazující na všechny soubory, které je potřeba zahrnout do balíčku, jste připraveni spustit `pack` příkaz:</span><span class="sxs-lookup"><span data-stu-id="03766-164">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack LoggingLibrary.nuspec
```

<span data-ttu-id="03766-165">Tím se vygeneruje `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="03766-165">This will generate `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="03766-166">Tento soubor otevřete v nástroje, jako je [NuGet – Průzkumník balíčků](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) a rozšiřuje všechny uzly, viz následující obsah:</span><span class="sxs-lookup"><span data-stu-id="03766-166">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![Zobrazuje LoggingLibrary balíčku NuGet – Průzkumník balíčků](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="03766-168">A `.nupkg` soubor je jenom soubor ZIP s jinou příponou.</span><span class="sxs-lookup"><span data-stu-id="03766-168">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="03766-169">Můžete také prozkoumat obsah balíčku, potom změnou `.nupkg` k `.zip`, ale nezapomeňte k obnovení rozšíření před nahráním balíčků na nuget.org.</span><span class="sxs-lookup"><span data-stu-id="03766-169">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="03766-170">Aby váš balíček k dispozici s ostatními vývojáři, postupujte podle pokynů [publikování balíčku](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="03766-170">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="03766-171">Související témata</span><span class="sxs-lookup"><span data-stu-id="03766-171">Related topics</span></span>

- [<span data-ttu-id="03766-172">Odkaz na soubor Nuspec</span><span class="sxs-lookup"><span data-stu-id="03766-172">Nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="03766-173">Balíčky symbolů</span><span class="sxs-lookup"><span data-stu-id="03766-173">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="03766-174">Správa verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="03766-174">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="03766-175">Podpora více verzí rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="03766-175">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="03766-176">Včetně cíle a vlastnosti nástroje MSBuild v balíčku</span><span class="sxs-lookup"><span data-stu-id="03766-176">Including MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="03766-177">Vytvoření lokalizovaných balíčků</span><span class="sxs-lookup"><span data-stu-id="03766-177">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)