---
title: Vytvoření balíčků NuGet pro Xamarin (pro iOS, Android a Windows) pomocí Visual Studia 2017 nebo 2019
description: Komplexní návod k vytváření balíčků NuGet pro Xamarin, které používají nativní api v systémech iOS, Android a Windows.
author: karann-msft
ms.author: karann
ms.date: 11/05/2019
ms.topic: tutorial
ms.openlocfilehash: 0cb653bad9e853d908039b3f7a94e1dd7eefdde5
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "78230899"
---
# <a name="create-packages-for-xamarin-with-visual-studio-2017-or-2019"></a><span data-ttu-id="be85a-103">Vytvoření balíčků pro Xamarin pomocí Visual Studia 2017 nebo 2019</span><span class="sxs-lookup"><span data-stu-id="be85a-103">Create packages for Xamarin with Visual Studio 2017 or 2019</span></span>

<span data-ttu-id="be85a-104">Balíček pro Xamarin obsahuje kód, který používá nativní API v systémech iOS, Android a Windows, v závislosti na operačním systému run-time.</span><span class="sxs-lookup"><span data-stu-id="be85a-104">A package for Xamarin contains code that uses native APIs on iOS, Android, and Windows, depending on the run-time operating system.</span></span> <span data-ttu-id="be85a-105">I když je to jednoduché, je vhodnější nechat vývojáři využívat balíček z knihovny PCL nebo .NET Standard prostřednictvím společné oblasti plochy rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="be85a-105">Although this is straightforward to do, it's preferable to let developers consume the package from a PCL or .NET Standard libraries through a common API surface area.</span></span>

<span data-ttu-id="be85a-106">V tomto návodu pomocí Visual Studia 2017 nebo 2019 vytvoříte balíček NuGet pro různé platformy, který lze použít v mobilních projektech v systémech iOS, Android a Windows.</span><span class="sxs-lookup"><span data-stu-id="be85a-106">In this walkthrough you use Visual Studio 2017 or 2019 to create a cross-platform NuGet package that can be used in mobile projects on iOS, Android, and Windows.</span></span>

1. [<span data-ttu-id="be85a-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="be85a-107">Prerequisites</span></span>](#prerequisites)
1. [<span data-ttu-id="be85a-108">Vytvoření struktury projektu a kódu abstrakce</span><span class="sxs-lookup"><span data-stu-id="be85a-108">Create the project structure and abstraction code</span></span>](#create-the-project-structure-and-abstraction-code)
1. [<span data-ttu-id="be85a-109">Napište kód specifický pro platformu</span><span class="sxs-lookup"><span data-stu-id="be85a-109">Write your platform-specific code</span></span>](#write-your-platform-specific-code)
1. [<span data-ttu-id="be85a-110">Vytvoření a aktualizace souboru Nuspec</span><span class="sxs-lookup"><span data-stu-id="be85a-110">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="be85a-111">Balení komponenty</span><span class="sxs-lookup"><span data-stu-id="be85a-111">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="be85a-112">Příbuzná témata</span><span class="sxs-lookup"><span data-stu-id="be85a-112">Related topics</span></span>](#related-topics)

## <a name="prerequisites"></a><span data-ttu-id="be85a-113">Požadavky</span><span class="sxs-lookup"><span data-stu-id="be85a-113">Prerequisites</span></span>

1. <span data-ttu-id="be85a-114">Visual Studio 2017 nebo 2019 s univerzální platformou Windows (UPW) a Xamarin.</span><span class="sxs-lookup"><span data-stu-id="be85a-114">Visual Studio 2017 or 2019 with Universal Windows Platform (UWP) and Xamarin.</span></span> <span data-ttu-id="be85a-115">Nainstalujte edici Společenství zdarma od [visualstudio.com](https://www.visualstudio.com/); můžete použít professional a enterprise edice, samozřejmě.</span><span class="sxs-lookup"><span data-stu-id="be85a-115">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span> <span data-ttu-id="be85a-116">Chcete-li zahrnout nástroje UPW a Xamarin, vyberte vlastní instalaci a zkontrolujte příslušné možnosti.</span><span class="sxs-lookup"><span data-stu-id="be85a-116">To include UWP and Xamarin tools, select a Custom install and check the appropriate options.</span></span>
1. <span data-ttu-id="be85a-117">NuGet CLI.</span><span class="sxs-lookup"><span data-stu-id="be85a-117">NuGet CLI.</span></span> <span data-ttu-id="be85a-118">Stáhněte si nejnovější verzi nuget.exe z [nuget.org/downloads](https://nuget.org/downloads)a uložte ji do zvoleného umístění.</span><span class="sxs-lookup"><span data-stu-id="be85a-118">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="be85a-119">Pak přidejte toto umístění do proměnné prostředí PATH, pokud ještě není.</span><span class="sxs-lookup"><span data-stu-id="be85a-119">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="be85a-120">nuget.exe je samotný nástroj rozhraní příkazového příkazu, nikoli instalátor, takže nezapomeňte uložit stažený soubor z prohlížeče namísto jeho spuštění.</span><span class="sxs-lookup"><span data-stu-id="be85a-120">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-project-structure-and-abstraction-code"></a><span data-ttu-id="be85a-121">Vytvoření struktury projektu a kódu abstrakce</span><span class="sxs-lookup"><span data-stu-id="be85a-121">Create the project structure and abstraction code</span></span>

1. <span data-ttu-id="be85a-122">Stáhněte a spusťte rozšíření šablony [standardních pluginů .NET](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) pro různé platformy pro Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="be85a-122">Download and run the [Cross-Platform .NET Standard Plugin Templates extension](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) for Visual Studio.</span></span> <span data-ttu-id="be85a-123">Tyto šablony usnadní vytvoření potřebné struktury projektu pro tento návod.</span><span class="sxs-lookup"><span data-stu-id="be85a-123">These templates will make it easy to create the necessary project structure for this walkthrough.</span></span>
1. <span data-ttu-id="be85a-124">V Sadě Visual Studio 2017 soubor > `Plugin`nový > **Project**, hledat , vyberte šablonu **modulu plug-in standardní knihovny napříč platformami .NET,** změňte název na LoggingLibrary a klikněte na OK.</span><span class="sxs-lookup"><span data-stu-id="be85a-124">In Visual Studio 2017, **File > New > Project**, search for `Plugin`, select the **Cross-Platform .NET Standard Library Plugin** template, change the name to LoggingLibrary, and click OK.</span></span>

    ![Nový projekt Aplikace Blank (Xamarin.Forms Portable) v VS 2017](media/CrossPlatform-NewProject.png)

    <span data-ttu-id="be85a-126">V Sadě Visual Studio 2019 soubor > `Plugin`nový > **Project**, hledat , vyberte šablonu **modulu plug-in standardní knihovny napříč platformami** a klikněte na Další.</span><span class="sxs-lookup"><span data-stu-id="be85a-126">In Visual Studio 2019, **File > New > Project**, search for `Plugin`, select the **Cross-Platform .NET Standard Library Plugin** template, and click Next.</span></span>

    ![Nový projekt Blank App (Xamarin.Forms Portable) v VS 2019](media/CrossPlatform-NewProject19-Part1.png)

    <span data-ttu-id="be85a-128">Změňte název na LoggingLibrary a klikněte na Vytvořit.</span><span class="sxs-lookup"><span data-stu-id="be85a-128">Change the name to LoggingLibrary, and click Create.</span></span>

    ![Nová konfigurace prázdné aplikace (Xamarin.Forms Portable) ve VS 2019](media/CrossPlatform-NewProject19-Part2.png)

<span data-ttu-id="be85a-130">Výsledné řešení obsahuje dva sdílené projekty spolu s řadou projektů specifických pro platformu:</span><span class="sxs-lookup"><span data-stu-id="be85a-130">The resulting solution contains two Shared projects, along with a variety of platform-specific projects:</span></span>

- <span data-ttu-id="be85a-131">Projekt, `ILoggingLibrary` který je obsažen `ILoggingLibrary.shared.cs` v souboru, definuje veřejné rozhraní (oblast povrchu rozhraní API) komponenty.</span><span class="sxs-lookup"><span data-stu-id="be85a-131">The `ILoggingLibrary` project, which is contained in the `ILoggingLibrary.shared.cs` file, defines the public interface (the API surface area) of the component.</span></span> <span data-ttu-id="be85a-132">Zde definujete rozhraní knihovny.</span><span class="sxs-lookup"><span data-stu-id="be85a-132">This is where you define the interface to your library.</span></span>
- <span data-ttu-id="be85a-133">Druhý sdílený projekt obsahuje `CrossLoggingLibrary.shared.cs` kód, který vyhledá implementaci abstraktního rozhraní specifické pro platformu za běhu.</span><span class="sxs-lookup"><span data-stu-id="be85a-133">The other Shared project contains code in `CrossLoggingLibrary.shared.cs` that will locate a platform-specific implementation of the abstract interface at run time.</span></span> <span data-ttu-id="be85a-134">Obvykle není nutné tento soubor upravovat.</span><span class="sxs-lookup"><span data-stu-id="be85a-134">You typically don't need to modify this file.</span></span>
- <span data-ttu-id="be85a-135">Projekty specifické pro platformu, jako je například `LoggingLibrary.android.cs`, `LoggingLibraryImplementation.cs` každý obsahuje nativní implementaci `LoggingLibrary.<PLATFORM>.cs` rozhraní v jejich příslušných (VS 2017) nebo (VS 2019) soubory.</span><span class="sxs-lookup"><span data-stu-id="be85a-135">The platform-specific projects, such as `LoggingLibrary.android.cs`, each contain a native implementation of the interface in their respective `LoggingLibraryImplementation.cs` (VS 2017) or `LoggingLibrary.<PLATFORM>.cs` (VS 2019) files.</span></span> <span data-ttu-id="be85a-136">Toje místo, kde můžete vytvořit kód knihovny.</span><span class="sxs-lookup"><span data-stu-id="be85a-136">This is where you build out your library's code.</span></span>

<span data-ttu-id="be85a-137">Ve výchozím nastavení ILoggingLibrary.shared.cs `ILoggingLibrary` soubor projektu obsahuje definici rozhraní, ale žádné metody.</span><span class="sxs-lookup"><span data-stu-id="be85a-137">By default, the ILoggingLibrary.shared.cs file of the `ILoggingLibrary` project contains an interface definition, but no methods.</span></span> <span data-ttu-id="be85a-138">Pro účely tohoto návodu přidejte následující metodu: `Log`</span><span class="sxs-lookup"><span data-stu-id="be85a-138">For the purposes of this walkthrough, add a `Log` method as follows:</span></span>

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

## <a name="write-your-platform-specific-code"></a><span data-ttu-id="be85a-139">Napište kód specifický pro platformu</span><span class="sxs-lookup"><span data-stu-id="be85a-139">Write your platform-specific code</span></span>

<span data-ttu-id="be85a-140">Chcete-li implementovat implementaci `ILoggingLibrary` rozhraní a jeho metod pro konkrétní platformu, postupujte takto:</span><span class="sxs-lookup"><span data-stu-id="be85a-140">To implement a platform-specific implementation of the `ILoggingLibrary` interface and its methods, do the following:</span></span>

1. <span data-ttu-id="be85a-141">Otevřete `LoggingLibraryImplementation.cs` soubor (VS 2017) nebo `LoggingLibrary.<PLATFORM>.cs` (VS 2019) každého projektu platformy a přidejte potřebný kód.</span><span class="sxs-lookup"><span data-stu-id="be85a-141">Open the `LoggingLibraryImplementation.cs` (VS 2017) or `LoggingLibrary.<PLATFORM>.cs` (VS 2019) file of each platform project and add the necessary code.</span></span> <span data-ttu-id="be85a-142">Například (pomocí `Android` projektu platformy):</span><span class="sxs-lookup"><span data-stu-id="be85a-142">For example (using the `Android` platform project):</span></span>

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

1. <span data-ttu-id="be85a-143">Opakujte tuto implementaci v projektech pro každou platformu, kterou chcete podporovat.</span><span class="sxs-lookup"><span data-stu-id="be85a-143">Repeat this implementation in the projects for each platform you want to support.</span></span>
1. <span data-ttu-id="be85a-144">Klikněte pravým tlačítkem myši na řešení a vyberte **sestavení řešení** zkontrolovat svou práci a vytvářet artefakty, které balíček další.</span><span class="sxs-lookup"><span data-stu-id="be85a-144">Right-click the solution and select **Build Solution** to check your work and produce the artifacts that you package next.</span></span> <span data-ttu-id="be85a-145">Pokud se zobrazí chyby týkající se chybějících odkazů, klepněte pravým tlačítkem myši na řešení, vyberte **obnovit balíčky NuGet** k instalaci závislostí a znovu sestavit.</span><span class="sxs-lookup"><span data-stu-id="be85a-145">If you get errors about missing references, right-click the solution, select **Restore NuGet Packages** to install dependencies, and rebuild.</span></span>

> [!Note]
> <span data-ttu-id="be85a-146">Pokud používáte Visual Studio 2019, před výběrem **obnovit nuget balíčky** a `MSBuild.Sdk.Extras` pokusu o opětovné sestavení, je třeba změnit verzi v `2.0.54` `LoggingLibrary.csproj`.</span><span class="sxs-lookup"><span data-stu-id="be85a-146">If you are using Visual Studio 2019, before selecting **Restore NuGet Packages** and trying to rebuild, you need to change the version of `MSBuild.Sdk.Extras` to `2.0.54` in `LoggingLibrary.csproj`.</span></span> <span data-ttu-id="be85a-147">K tomuto souboru lze přistupovat pouze prvním kliknutím pravým tlačítkem myši na projekt (pod řešením) a výběrem `Unload Project`, po kterém klepnete pravým tlačítkem myši na nezatížený projekt a vyberete . `Edit LoggingLibrary.csproj`</span><span class="sxs-lookup"><span data-stu-id="be85a-147">This file can only be accessed by first right-clicking the project (below the solution) and selecting `Unload Project`, after which you right-click on the unloaded project and select `Edit LoggingLibrary.csproj`.</span></span>

> [!Note]
> <span data-ttu-id="be85a-148">Chcete-li vytvořit pro iOS, potřebujete síťový Mac připojený k sadě Visual Studio, jak je popsáno v [úvodu k Xamarin.iOS pro Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span><span class="sxs-lookup"><span data-stu-id="be85a-148">To build for iOS you need a networked Mac connected to Visual Studio as described on [Introduction to Xamarin.iOS for Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span></span> <span data-ttu-id="be85a-149">Pokud mac nemáte k dispozici, zrušte výběr projektu iOS ve Správci konfigurace (krok 3 výše).</span><span class="sxs-lookup"><span data-stu-id="be85a-149">If you don't have a Mac available, clear the iOS project in the configuration manager (step 3 above).</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="be85a-150">Vytvoření a aktualizace souboru Nuspec</span><span class="sxs-lookup"><span data-stu-id="be85a-150">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="be85a-151">Otevřete příkazový řádek, `LoggingLibrary` přejděte do složky, `.sln` která je o jednu úroveň níže, kde je soubor, a spusťte příkaz NuGet `spec` a vytvořte počáteční `Package.nuspec` soubor:</span><span class="sxs-lookup"><span data-stu-id="be85a-151">Open a command prompt, navigate to the `LoggingLibrary` folder that's one level below where the `.sln` file is, and run the NuGet `spec` command to create the initial `Package.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="be85a-152">Přejmenujte tento `LoggingLibrary.nuspec` soubor na a otevřete jej v editoru.</span><span class="sxs-lookup"><span data-stu-id="be85a-152">Rename this file to `LoggingLibrary.nuspec` and open it in an editor.</span></span>
1. <span data-ttu-id="be85a-153">Aktualizujte soubor tak, aby odpovídal následujícímu, a nahrazte YOUR_NAME příslušnou hodnotou.</span><span class="sxs-lookup"><span data-stu-id="be85a-153">Update the file to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="be85a-154">Hodnota, `<id>` konkrétně musí být jedinečný napříč nuget.org (viz konvence pojmenování popsané v [vytvoření balíčku).](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)</span><span class="sxs-lookup"><span data-stu-id="be85a-154">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="be85a-155">Všimněte si také, že musíte také aktualizovat značky autora a popisu nebo se během kroku balení zobrazí chyba.</span><span class="sxs-lookup"><span data-stu-id="be85a-155">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
> <span data-ttu-id="be85a-156">Můžete příponu verze balíčku `-alpha` `-beta` s `-rc` aplikacemi , nebo označit balíček jako předběžnou verzi, zkontrolujte [předběžné verze](../create-packages/prerelease-packages.md) další informace o předběžných verzích.</span><span class="sxs-lookup"><span data-stu-id="be85a-156">You can suffix your package version with `-alpha`, `-beta` or `-rc` to mark your package as pre-release, check [Pre-release versions](../create-packages/prerelease-packages.md) for more information about pre-release versions.</span></span>

### <a name="add-reference-assemblies"></a><span data-ttu-id="be85a-157">Přidání referenčních sestavení</span><span class="sxs-lookup"><span data-stu-id="be85a-157">Add reference assemblies</span></span>

<span data-ttu-id="be85a-158">Chcete-li zahrnout referenční sestavení specifická pro `<files>` platformu, přidejte k prvku `LoggingLibrary.nuspec` podle potřeby pro podporované platformy následující:</span><span class="sxs-lookup"><span data-stu-id="be85a-158">To include platform-specific reference assemblies, add the following to the `<files>` element of `LoggingLibrary.nuspec` as appropriate for your supported platforms:</span></span>

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
> <span data-ttu-id="be85a-159">Chcete-li zkrátit názvy souborů DLL a XML, klepněte pravým tlačítkem myši na libovolný projekt, vyberte kartu **Knihovna** a změňte názvy sestavení.</span><span class="sxs-lookup"><span data-stu-id="be85a-159">To shorten the names of the DLL and XML files, right-click on any given project, select the **Library** tab, and change the assembly names.</span></span>

### <a name="add-dependencies"></a><span data-ttu-id="be85a-160">Přidání závislostí</span><span class="sxs-lookup"><span data-stu-id="be85a-160">Add dependencies</span></span>

<span data-ttu-id="be85a-161">Pokud máte specifické závislosti pro nativní `<dependencies>` implementace, `<group>` použijte element s prvky k jejich určení, například:</span><span class="sxs-lookup"><span data-stu-id="be85a-161">If you have specific dependencies for native implementations, use the `<dependencies>` element with `<group>` elements to specify them, for example:</span></span>

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

<span data-ttu-id="be85a-162">Například následující by nastavit iTextSharp jako závislost pro cíl UAP:</span><span class="sxs-lookup"><span data-stu-id="be85a-162">For example, the following would set iTextSharp as a dependency for the UAP target:</span></span>

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a><span data-ttu-id="be85a-163">Konečný .nuspec</span><span class="sxs-lookup"><span data-stu-id="be85a-163">Final .nuspec</span></span>

<span data-ttu-id="be85a-164">Konečný `.nuspec` soubor by nyní měl vypadat takto, kde by měl být opět nahrazen YOUR_NAME příslušnou hodnotou:</span><span class="sxs-lookup"><span data-stu-id="be85a-164">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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

## <a name="package-the-component"></a><span data-ttu-id="be85a-165">Balení komponenty</span><span class="sxs-lookup"><span data-stu-id="be85a-165">Package the component</span></span>

<span data-ttu-id="be85a-166">S dokončeným `.nuspec` odkazováním na všechny soubory, které potřebujete zahrnout do `pack` balíčku, jste připraveni spustit příkaz:</span><span class="sxs-lookup"><span data-stu-id="be85a-166">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack LoggingLibrary.nuspec
```

<span data-ttu-id="be85a-167">To bude `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`generovat .</span><span class="sxs-lookup"><span data-stu-id="be85a-167">This will generate `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="be85a-168">Otevření tohoto souboru v nástroji, jako je [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) a rozbalení všech uzlů, uvidíte následující obsah:</span><span class="sxs-lookup"><span data-stu-id="be85a-168">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![NuGet Package Explorer zobrazující balíček LoggingLibrary](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="be85a-170">Soubor `.nupkg` je pouze soubor ZIP s jinou příponou.</span><span class="sxs-lookup"><span data-stu-id="be85a-170">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="be85a-171">Můžete také prozkoumat obsah balíčku, `.nupkg` `.zip`pak změnou na , ale nezapomeňte obnovit rozšíření před odesláním balíček nuget.org.</span><span class="sxs-lookup"><span data-stu-id="be85a-171">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="be85a-172">Chcete-li balíček zpřístupnit ostatním [vývojářům,](../nuget-org/publish-a-package.md)postupujte podle pokynů k části Publikovat balíček .</span><span class="sxs-lookup"><span data-stu-id="be85a-172">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="be85a-173">Související témata</span><span class="sxs-lookup"><span data-stu-id="be85a-173">Related topics</span></span>

- [<span data-ttu-id="be85a-174">Odkaz na nuspec</span><span class="sxs-lookup"><span data-stu-id="be85a-174">Nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="be85a-175">Balíčky symbolů</span><span class="sxs-lookup"><span data-stu-id="be85a-175">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="be85a-176">Správa verzí balíčku</span><span class="sxs-lookup"><span data-stu-id="be85a-176">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="be85a-177">Podpora více verzí rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="be85a-177">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="be85a-178">Zahrnout rekvizity a cíle MSBuild do balíčku</span><span class="sxs-lookup"><span data-stu-id="be85a-178">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="be85a-179">Vytváření lokalizovaných balíčků</span><span class="sxs-lookup"><span data-stu-id="be85a-179">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
