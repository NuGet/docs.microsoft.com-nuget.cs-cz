---
title: Vytvoření balíčků NuGet pro Xamarin (pro iOS, Android a Windows) s Visual Studiem 2015 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: tutorial
ms.prod: nuget
ms.technology: ''
description: Návod začátku do konce vytváření balíčků NuGet pro Xamarin pomocí nativních rozhraní API pro iOS, Android a Windows.
keywords: Vytvoření balíčku, balíčky pro Xamarin, balíčky a platformy
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: e101ca2d124a19d2cf758776717b3680aa5bbdd8
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="create-packages-for-xamarin-with-visual-studio-2015"></a><span data-ttu-id="a3557-104">Vytvoření balíčků pro Xamarin s Visual Studiem 2015</span><span class="sxs-lookup"><span data-stu-id="a3557-104">Create packages for Xamarin with Visual Studio 2015</span></span>

<span data-ttu-id="a3557-105">Balíček pro Xamarin obsahuje kód, který používá nativních rozhraní API pro iOS, Android a Windows, v závislosti na spuštění operačního systému.</span><span class="sxs-lookup"><span data-stu-id="a3557-105">A package for Xamarin contains code that uses native APIs on iOS, Android, and Windows, depending on the run-time operating system.</span></span> <span data-ttu-id="a3557-106">Přestože je toto přehledné udělat, je vhodnější, aby mohli vývojáři využívat balíček PCL nebo .NET Standard knihovny prostřednictvím společné rozhraní API surface oblasti.</span><span class="sxs-lookup"><span data-stu-id="a3557-106">Although this is straightforward to do, it's preferable to let developers consume the package from a PCL or .NET Standard libraries through a common API surface area.</span></span>

<span data-ttu-id="a3557-107">V tomto návodu, které můžete použít Visual Studio 2015 vytvoření balíčku NuGet a platformy, který lze použít v mobilních projekty pro iOS, Android a Windows.</span><span class="sxs-lookup"><span data-stu-id="a3557-107">In this walkthrough you use Visual Studio 2015 create a cross-platform NuGet package that can be used in mobile projects on iOS, Android, and Windows.</span></span>

1. [<span data-ttu-id="a3557-108">Požadavky</span><span class="sxs-lookup"><span data-stu-id="a3557-108">Prerequisites</span></span>](#prerequisites)
1. [<span data-ttu-id="a3557-109">Vytvoření projektu strukturu a abstrakce kód</span><span class="sxs-lookup"><span data-stu-id="a3557-109">Create the project structure and abstraction code</span></span>](#create-the-project-structure-and-abstraction-code)
1. [<span data-ttu-id="a3557-110">Zadejte kód, podle platformy</span><span class="sxs-lookup"><span data-stu-id="a3557-110">Write your platform-specific code</span></span>](#write-your-platform-specific-code)
1. [<span data-ttu-id="a3557-111">Vytvářet a aktualizovat soubor s příponou .nuspec</span><span class="sxs-lookup"><span data-stu-id="a3557-111">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="a3557-112">Balíček součásti</span><span class="sxs-lookup"><span data-stu-id="a3557-112">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="a3557-113">Související témata</span><span class="sxs-lookup"><span data-stu-id="a3557-113">Related topics</span></span>](#related-topics)

## <a name="prerequisites"></a><span data-ttu-id="a3557-114">Požadavky</span><span class="sxs-lookup"><span data-stu-id="a3557-114">Prerequisites</span></span>

1. <span data-ttu-id="a3557-115">Visual Studio 2015 se univerzální platformu Windows (UWP) a Xamarin.</span><span class="sxs-lookup"><span data-stu-id="a3557-115">Visual Studio 2015 with Universal Windows Platform (UWP) and Xamarin.</span></span> <span data-ttu-id="a3557-116">Instalaci edice Community zdarma z [visualstudio.com](https://www.visualstudio.com/); samozřejmě můžete taky edice Professional a Enterprise.</span><span class="sxs-lookup"><span data-stu-id="a3557-116">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span> <span data-ttu-id="a3557-117">Zahrnout nástroje pro UPW a Xamarin, vyberte vlastní instalaci a zkontrolujte příslušné možnosti.</span><span class="sxs-lookup"><span data-stu-id="a3557-117">To include UWP and Xamarin tools, select a Custom install and check the appropriate options.</span></span>
1. <span data-ttu-id="a3557-118">Rozhraní příkazového řádku NuGet.</span><span class="sxs-lookup"><span data-stu-id="a3557-118">NuGet CLI.</span></span> <span data-ttu-id="a3557-119">Stáhněte si nejnovější verzi nuget.exe z [nuget.org/downloads](https://nuget.org/downloads), ukládání do umístění podle vaší volby.</span><span class="sxs-lookup"><span data-stu-id="a3557-119">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="a3557-120">Pak přidejte tohoto umístění do vaší proměnné prostředí PATH, pokud již není.</span><span class="sxs-lookup"><span data-stu-id="a3557-120">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="a3557-121">nuget.exe je že nástroj příkazového řádku, není instalační program, takže je nutné z prohlížeče namísto spuštění ho uložte stažený soubor.</span><span class="sxs-lookup"><span data-stu-id="a3557-121">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-project-structure-and-abstraction-code"></a><span data-ttu-id="a3557-122">Vytvoření projektu strukturu a abstrakce kód</span><span class="sxs-lookup"><span data-stu-id="a3557-122">Create the project structure and abstraction code</span></span>

1. <span data-ttu-id="a3557-123">Stažení a spuštění [modul plug-in pro Xamarin šablony rozšíření](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) pro sadu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a3557-123">Download and run the [Plugin for Xamarin Templates extension](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) for Visual Studio.</span></span> <span data-ttu-id="a3557-124">Tyto šablony snadno vytvořit strukturu nezbytné projektu pro účely tohoto postupu.</span><span class="sxs-lookup"><span data-stu-id="a3557-124">These templates will make it easy to create the necessary project structure for this walkthrough.</span></span>
1. <span data-ttu-id="a3557-125">V sadě Visual Studio **soubor > Nový > projekt**, vyhledejte `Plugin`, vyberte **modul plug-in pro Xamarin** šablony, změňte název na LoggingLibrary a klikněte na tlačítko OK.</span><span class="sxs-lookup"><span data-stu-id="a3557-125">In Visual Studio, **File > New > Project**, search for `Plugin`, select the **Plugin for Xamarin** template, change the name to LoggingLibrary, and click OK.</span></span>

    ![Nový projekt prázdná aplikace (Xamarin.Forms přenositelností) v sadě Visual Studio](media/CrossPlatform-NewProject.png)

<span data-ttu-id="a3557-127">Výsledný řešení obsahuje dva projekty PCL, společně s celou řadu specifických pro platformy projekty:</span><span class="sxs-lookup"><span data-stu-id="a3557-127">The resulting solution contains two PCL projects, along with a variety of platform-specific projects:</span></span>

- <span data-ttu-id="a3557-128">PCL s názvem `Plugin.LoggingLibrary.Abstractions (Portable)`, definuje veřejné rozhraní (prostor oblast rozhraní API) komponenty, v takovém případě `ILoggingLibrary` rozhraní obsažené v souboru ILoggingLibrary.cs.</span><span class="sxs-lookup"><span data-stu-id="a3557-128">The PCL named `Plugin.LoggingLibrary.Abstractions (Portable)`, defines the public interface (the API surface area) of the component, in this case the `ILoggingLibrary` interface contained in the ILoggingLibrary.cs file.</span></span> <span data-ttu-id="a3557-129">Toto je, kde můžete definovat rozhraní do knihovny.</span><span class="sxs-lookup"><span data-stu-id="a3557-129">This is where you define the interface to your library.</span></span>
- <span data-ttu-id="a3557-130">Další PCL `Plugin.LoggingLibrary (Portable)`, obsahuje kód v CrossLoggingLibrary.cs, který vyhledá specifické pro platformu implementaci abstraktní rozhraní za běhu.</span><span class="sxs-lookup"><span data-stu-id="a3557-130">The other PCL, `Plugin.LoggingLibrary (Portable)`, contains code in CrossLoggingLibrary.cs that will locate a platform-specific implementation of the abstract interface at run time.</span></span> <span data-ttu-id="a3557-131">Obvykle nepotřebujete pro úpravu tohoto souboru.</span><span class="sxs-lookup"><span data-stu-id="a3557-131">You typically don't need to modify this file.</span></span>
- <span data-ttu-id="a3557-132">Specifické platformy projekty, například `Plugin.LoggingLibrary.Android`, každý obsahovat obsahovat nativní implementaci rozhraní ve svých příslušných LoggingLibraryImplementation.cs souborů.</span><span class="sxs-lookup"><span data-stu-id="a3557-132">The platform-specific projects, such as `Plugin.LoggingLibrary.Android`, each contain contain a native implementation of the interface in their respective LoggingLibraryImplementation.cs files.</span></span> <span data-ttu-id="a3557-133">Toto je, kde vytvoříte na vaše knihovna kódu.</span><span class="sxs-lookup"><span data-stu-id="a3557-133">This is where you build out your library's code.</span></span>

<span data-ttu-id="a3557-134">Ve výchozím nastavení soubor ILoggingLibrary.cs projektu abstrakce obsahuje definici rozhraní, ale žádné metody.</span><span class="sxs-lookup"><span data-stu-id="a3557-134">By default, the ILoggingLibrary.cs file of the Abstractions project contains an interface definition, but no methods.</span></span> <span data-ttu-id="a3557-135">Pro účely tohoto návodu, přidejte `Log` metoda následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="a3557-135">For the purposes of this walkthrough, add a `Log` method as follows:</span></span>

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

## <a name="write-your-platform-specific-code"></a><span data-ttu-id="a3557-136">Zadejte kód, podle platformy</span><span class="sxs-lookup"><span data-stu-id="a3557-136">Write your platform-specific code</span></span>

<span data-ttu-id="a3557-137">K implementaci specifické pro platformu provádění `ILoggingLibrary` rozhraní a její metody, postupujte takto:</span><span class="sxs-lookup"><span data-stu-id="a3557-137">To implement a platform-specific implementation of the `ILoggingLibrary` interface and its methods, do the following:</span></span>

1. <span data-ttu-id="a3557-138">Otevřete `LoggingLibraryImplementation.cs` soubor pro každou platformu projektu a přidání nezbytného kódu.</span><span class="sxs-lookup"><span data-stu-id="a3557-138">Open the `LoggingLibraryImplementation.cs` file of each platform project and add the necessary code.</span></span> <span data-ttu-id="a3557-139">Například (pomocí `Plugin.LoggingLibrary.Android` projekt):</span><span class="sxs-lookup"><span data-stu-id="a3557-139">For example (using the `Plugin.LoggingLibrary.Android` project):</span></span>

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

1. <span data-ttu-id="a3557-140">Tato implementace v projektech opakujte pro každou platformu, kterou chcete podporovat.</span><span class="sxs-lookup"><span data-stu-id="a3557-140">Repeat this implementation in the projects for each platform you want to support.</span></span>
1. <span data-ttu-id="a3557-141">Klikněte pravým tlačítkem na projekt pro iOS, vyberte **vlastnosti**, klikněte na tlačítko **sestavení** a odeberte "\iPhone" z **výstupní cesta** a **souborů dokumentace XML**  nastavení.</span><span class="sxs-lookup"><span data-stu-id="a3557-141">Right-click the iOS project, select **Properties**, click the **Build** tab, and remove "\iPhone" from the **Output path** and **XML documentation file** settings.</span></span> <span data-ttu-id="a3557-142">Toto platí jenom pro novější usnadnění práce v tomto návodu.</span><span class="sxs-lookup"><span data-stu-id="a3557-142">This is just for later convenience in this walkthrough.</span></span> <span data-ttu-id="a3557-143">Uložte soubor po dokončení.</span><span class="sxs-lookup"><span data-stu-id="a3557-143">Save the file when done.</span></span>
1. <span data-ttu-id="a3557-144">Klikněte pravým tlačítkem na řešení, vyberte **nástroje Configuration Manager...** a zkontrolujte **sestavení** políček u PCLs a jednotlivé platformy, které podporujete.</span><span class="sxs-lookup"><span data-stu-id="a3557-144">Right-click the solution, select **Configuration Manager...**, and check the **Build** boxes for the PCLs and each platform you're supporting.</span></span>
1. <span data-ttu-id="a3557-145">Klikněte pravým tlačítkem na řešení a vyberte **sestavit řešení** ke kontrole práci a vytvoří artefakty, které další balíček.</span><span class="sxs-lookup"><span data-stu-id="a3557-145">Right-click the solution and select **Build Solution** to check your work and produce the artifacts that you package next.</span></span> <span data-ttu-id="a3557-146">Pokud dojde k chybám o chybějícím odkazům, klikněte pravým tlačítkem na řešení, vyberte **obnovení balíčků NuGet** k instalaci závislosti a sestavte znovu.</span><span class="sxs-lookup"><span data-stu-id="a3557-146">If you get errors about missing references, right-click the solution, select **Restore NuGet Packages** to install dependencies, and rebuild.</span></span>

> [!Note]
> <span data-ttu-id="a3557-147">K vytvoření pro iOS potřebujete síťově připojeného počítače Mac připojené k sadě Visual Studio, jak je popsáno na [Úvod do Xamarin.iOS pro sadu Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span><span class="sxs-lookup"><span data-stu-id="a3557-147">To build for iOS you need a networked Mac connected to Visual Studio as described on [Introduction to Xamarin.iOS for Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span></span> <span data-ttu-id="a3557-148">Pokud nemáte k dispozici Mac, zrušte projekt pro iOS v configuration Manageru (krok 3 výše).</span><span class="sxs-lookup"><span data-stu-id="a3557-148">If you don't have a Mac available, clear the iOS project in the configuration manager (step 3 above).</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="a3557-149">Vytvářet a aktualizovat soubor s příponou .nuspec</span><span class="sxs-lookup"><span data-stu-id="a3557-149">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="a3557-150">Otevřete příkazový řádek, přejděte na `LoggingLibrary` složky, která je jednu úroveň pod where `.sln` souboru a spusťte NuGet `spec` příkaz pro vytvoření počáteční `Package.nuspec` souboru:</span><span class="sxs-lookup"><span data-stu-id="a3557-150">Open a command prompt, navigate to the `LoggingLibrary` folder that's one level below where the `.sln` file is, and run the NuGet `spec` command to create the initial `Package.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="a3557-151">Přejmenujte tento soubor do `LoggingLibrary.nuspec` a otevře ji v editoru.</span><span class="sxs-lookup"><span data-stu-id="a3557-151">Rename this file to `LoggingLibrary.nuspec` and open it in an editor.</span></span>
1. <span data-ttu-id="a3557-152">Aktualizujte, aby se shodoval s následujícím, nahraďte vaše_jméno odpovídající hodnotu.</span><span class="sxs-lookup"><span data-stu-id="a3557-152">Update the file to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="a3557-153">`<id>` Hodnotu, konkrétně musí být jedinečný v rámci nuget.org (viz zásady vytváření názvů, které jsou popsané v [vytváření balíčku](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="a3557-153">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="a3557-154">Všimněte si také, zda je nutné také aktualizovat autora a popis značky nebo dojde k chybě během kroku okolních.</span><span class="sxs-lookup"><span data-stu-id="a3557-154">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
> <span data-ttu-id="a3557-155">Můžete přípona vaší verzí balíčku `-alpha`, `-beta` nebo `-rc` označit jako předběžné verze vašeho balíčku, zkontrolujte [předprodejní verze](../create-packages/prerelease-packages.md) Další informace o předběžné verze.</span><span class="sxs-lookup"><span data-stu-id="a3557-155">You can suffix your package version with `-alpha`, `-beta` or `-rc` to mark your package as pre-release, check [Pre-release versions](../create-packages/prerelease-packages.md) for more information about pre-release versions.</span></span>

### <a name="add-reference-assemblies"></a><span data-ttu-id="a3557-156">Přidat odkaz na sestavení</span><span class="sxs-lookup"><span data-stu-id="a3557-156">Add reference assemblies</span></span>

<span data-ttu-id="a3557-157">Pokud chcete specifické pro platformu referenční sestavení, přidejte následující příkaz a `<files>` element `LoggingLibrary.nuspec` podle potřeby podporovaných platforem:</span><span class="sxs-lookup"><span data-stu-id="a3557-157">To include platform-specific reference assemblies, add the following to the `<files>` element of `LoggingLibrary.nuspec` as appropriate for your supported platforms:</span></span>

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
> <span data-ttu-id="a3557-158">Tak, aby zkrátil názvy souborů DLL a XML, klikněte pravým tlačítkem na jakékoli dané projekt, vyberte **knihovny** kartě a změnit názvy sestavení.</span><span class="sxs-lookup"><span data-stu-id="a3557-158">To shorten the names of the DLL and XML files, right-click on any given project, select the **Library** tab, and change the assembly names.</span></span>

### <a name="add-dependencies"></a><span data-ttu-id="a3557-159">Přidat závislosti</span><span class="sxs-lookup"><span data-stu-id="a3557-159">Add dependencies</span></span>

<span data-ttu-id="a3557-160">Pokud máte konkrétní závislosti pro nativní implementace, použijte `<dependencies>` element s `<group>` elementy, je třeba zadat:</span><span class="sxs-lookup"><span data-stu-id="a3557-160">If you have specific dependencies for native implementations, use the `<dependencies>` element with `<group>` elements to specify them, for example:</span></span>

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

<span data-ttu-id="a3557-161">Například následující by nastavit iTextSharp jako závislost pro cíl UAP:</span><span class="sxs-lookup"><span data-stu-id="a3557-161">For example, the following would set iTextSharp as a dependency for the UAP target:</span></span>

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a><span data-ttu-id="a3557-162">Poslední příponou .nuspec.</span><span class="sxs-lookup"><span data-stu-id="a3557-162">Final .nuspec</span></span>

<span data-ttu-id="a3557-163">Váš koncový `.nuspec` soubor by měl nyní vypadat jako následující, kde znovu vaše_jméno by měla být nahrazená příslušnou hodnotu:</span><span class="sxs-lookup"><span data-stu-id="a3557-163">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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

## <a name="package-the-component"></a><span data-ttu-id="a3557-164">Balíček součásti</span><span class="sxs-lookup"><span data-stu-id="a3557-164">Package the component</span></span>

<span data-ttu-id="a3557-165">S dokončené `.nuspec` odkazující na všechny soubory, které je potřeba zahrnout do balíčku, jste připraveni ke spuštění `pack` příkaz:</span><span class="sxs-lookup"><span data-stu-id="a3557-165">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack LoggingLibrary.nuspec
```

<span data-ttu-id="a3557-166">Tím se vygeneruje `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="a3557-166">This will generate `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="a3557-167">Otevření tohoto souboru v nástroje, jako [Explorer balíček NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) a rozšiřování všechny uzly, můžete zobrazit následující obsah:</span><span class="sxs-lookup"><span data-stu-id="a3557-167">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![Průzkumník balíček NuGet zobrazující LoggingLibrary balíčku](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="a3557-169">A `.nupkg` soubor je právě soubor ZIP s jiné rozšíření.</span><span class="sxs-lookup"><span data-stu-id="a3557-169">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="a3557-170">Můžete také zkontrolovat obsah balíčku, potom změnou `.nupkg` k `.zip`, ale nezapomeňte obnovit rozšíření před balíčku se nahrávají na nuget.org.</span><span class="sxs-lookup"><span data-stu-id="a3557-170">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="a3557-171">Pokud chcete zpřístupnit vašeho balíčku jinými vývojáři, postupujte podle pokynů [publikování balíčku](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="a3557-171">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="a3557-172">Související témata</span><span class="sxs-lookup"><span data-stu-id="a3557-172">Related topics</span></span>

- [<span data-ttu-id="a3557-173">Odkaz na soubor Nuspec</span><span class="sxs-lookup"><span data-stu-id="a3557-173">Nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="a3557-174">Balíčky symbolů</span><span class="sxs-lookup"><span data-stu-id="a3557-174">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="a3557-175">Správa verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="a3557-175">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="a3557-176">Podpora více verzí rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="a3557-176">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="a3557-177">Včetně MSBuild props a cíle v balíčku</span><span class="sxs-lookup"><span data-stu-id="a3557-177">Including MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="a3557-178">Vytvoření lokalizovaných balíčků</span><span class="sxs-lookup"><span data-stu-id="a3557-178">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)