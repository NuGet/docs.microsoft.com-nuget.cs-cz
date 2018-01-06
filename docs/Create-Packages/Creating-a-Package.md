---
title: "Postup vytvoření balíčku NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/12/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 456797cb-e3e4-4b88-9b01-8b5153cee802
description: "Podrobný průvodce do procesu návrhu a vytvoření balíčku NuGet, včetně klíče rozhodovací body, jako jsou soubory a správu verzí."
keywords: "Vytvoření balíčku NuGet, vytváření balíčku, nuspec manifest, konvence balíčku NuGet, verze balíčku NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 50bc9e79f95f901477208f638b0965c82fd98356
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/05/2018
---
# <a name="creating-nuget-packages"></a><span data-ttu-id="81a60-104">Vytváření balíčků NuGet</span><span class="sxs-lookup"><span data-stu-id="81a60-104">Creating NuGet packages</span></span>

<span data-ttu-id="81a60-105">Bez ohledu na jaké vašeho balíčku nebo co code je obsahuje, můžete použít `nuget.exe` do balíčku, které tuto funkci do komponenty, které je možné sdílet s a používat libovolný počet dalších vývojáři.</span><span class="sxs-lookup"><span data-stu-id="81a60-105">No matter what your package does or what code it contains, you use `nuget.exe` to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="81a60-106">Chcete-li nainstalovat `nuget.exe`, najdete v části [nainstalovat rozhraní příkazového řádku NuGet](../guides/Install-NuGet.md#nuget-cli).</span><span class="sxs-lookup"><span data-stu-id="81a60-106">To install `nuget.exe`, see [Install NuGet CLI](../guides/Install-NuGet.md#nuget-cli).</span></span> <span data-ttu-id="81a60-107">Všimněte si, že Visual Studio automaticky nezahrnuje `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="81a60-107">Note that Visual Studio does not automatically include `nuget.exe`.</span></span>

<span data-ttu-id="81a60-108">Technicky platí, že balíček NuGet je právě soubor ZIP, který byl přejmenován s `.nupkg` rozšíření, jejichž obsah odpovídají určité konvence.</span><span class="sxs-lookup"><span data-stu-id="81a60-108">Technically speaking, a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension and whose contents match certain conventions.</span></span> <span data-ttu-id="81a60-109">Toto téma popisuje podrobný proces vytvoření balíčku, který splňuje tyto konvence.</span><span class="sxs-lookup"><span data-stu-id="81a60-109">This topic describes the detailed process of creating a package that meets those conventions.</span></span> <span data-ttu-id="81a60-110">Podrobný návod, najdete v části [vytvoření a publikování rychlé spuštění balíčku](../quickstart/create-and-publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="81a60-110">For a focused walkthrough, refer to [Create and Publish a Package Quickstart](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="81a60-111">Balení začíná zkompilovaný kód (sestavení), symboly a další soubory, které chcete doručit jako balíček (viz [přehled a pracovní postup](Overview-and-Workflow.md)).</span><span class="sxs-lookup"><span data-stu-id="81a60-111">Packaging begins with the compiled code (assemblies), symbols, and/or other files that you want to deliver as a package (see [Overview and workflow](Overview-and-Workflow.md)).</span></span> <span data-ttu-id="81a60-112">Tento proces je nezávislé na kompilování nebo jinak generování souborů, které patří do balíčku, i když můžete použít kreslení z informací v souboru projektu pro synchronizaci kompilované assemblines a balíčky.</span><span class="sxs-lookup"><span data-stu-id="81a60-112">This process is independent from compiling or otherwise generating the files that go into the package, although you can use draw from information in a project file to keep the compiled assemblines and packages in sync.</span></span>

<span data-ttu-id="81a60-113">V tomto tématu:</span><span class="sxs-lookup"><span data-stu-id="81a60-113">In this topic:</span></span>

- [<span data-ttu-id="81a60-114">Rozhodnutí, která sestavení do balíčku</span><span class="sxs-lookup"><span data-stu-id="81a60-114">Deciding which assemblies to package</span></span>](#deciding-which-assemblies-to-package)
- [<span data-ttu-id="81a60-115">Role a struktura `.nuspec` souboru</span><span class="sxs-lookup"><span data-stu-id="81a60-115">The role and structure of the `.nuspec` file</span></span>](#the-role-and-structure-of-the-nuspec-file)
- <span data-ttu-id="81a60-116">[Vytváření `.nuspec` soubor](#creating-the-nuspec-file) z:</span><span class="sxs-lookup"><span data-stu-id="81a60-116">[Creating the `.nuspec` file](#creating-the-nuspec-file) from:</span></span>
    - [<span data-ttu-id="81a60-117">Založené na konvenci pracovní adresář</span><span class="sxs-lookup"><span data-stu-id="81a60-117">A convention-based working directory</span></span>](#from-a-convention-based-working-directory)
    - [<span data-ttu-id="81a60-118">Sestavení knihovny DLL</span><span class="sxs-lookup"><span data-stu-id="81a60-118">An assembly DLL</span></span>](#from-an-assembly-dll)
    - [<span data-ttu-id="81a60-119">Projekt sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="81a60-119">A Visual Studio project</span></span>](#from-a-visual-studio-project)
    - [<span data-ttu-id="81a60-120">Nový soubor s výchozími hodnotami</span><span class="sxs-lookup"><span data-stu-id="81a60-120">New file with default values</span></span>](#new-file-with-default-values)    
- [<span data-ttu-id="81a60-121">Výběr balíčku jedinečný identifikátor a nastavení číslo verze</span><span class="sxs-lookup"><span data-stu-id="81a60-121">Choosing a unique package identifier and setting the version number</span></span>](#choosing-a-unique-package-identifier-and-setting-the-version-number)
- <span data-ttu-id="81a60-122">[Typ balíčku nastavení](#setting-a-package-type) (NuGet 3.5 a novější)</span><span class="sxs-lookup"><span data-stu-id="81a60-122">[Setting a package type](#setting-a-package-type) (NuGet 3.5 and later)</span></span>
- [<span data-ttu-id="81a60-123">Přidání soubor readme a další soubory</span><span class="sxs-lookup"><span data-stu-id="81a60-123">Adding a readme and other files</span></span>](#adding-a-readme-and-other-files)
- [<span data-ttu-id="81a60-124">Včetně MSBuild props a cíle v balíčku</span><span class="sxs-lookup"><span data-stu-id="81a60-124">Including MSBuild props and targets in a package</span></span>](#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="81a60-125">Vytváření balíčků, které obsahují sestavení vzájemné spolupráce COM</span><span class="sxs-lookup"><span data-stu-id="81a60-125">Authoring packages that contain COM interop assemblies</span></span>](#authoring-packages-with-com-interop-assemblies)
- [<span data-ttu-id="81a60-126">S aktualizací Service pack nuget ke generování souboru .nupkg v podadresáři</span><span class="sxs-lookup"><span data-stu-id="81a60-126">Running nuget pack to generate the .nupkg file</span></span>](#running-nuget-pack-to-generate-the-nupkg-file)

<span data-ttu-id="81a60-127">Po tyto základní kroky, jak je popsáno jinde v této dokumentaci můžete začlenit celou řadu dalších funkcí.</span><span class="sxs-lookup"><span data-stu-id="81a60-127">After these core steps, you can incorporate a variety of other features as described elsewhere in this documentation.</span></span> <span data-ttu-id="81a60-128">V tématu [další kroky](#next-steps) níže.</span><span class="sxs-lookup"><span data-stu-id="81a60-128">See [Next steps](#next-steps) below.</span></span>

> [!Note]
> <span data-ttu-id="81a60-129">Toto téma se vztahuje na typy projektů než projektů .NET Core pomocí Visual Studio 2017 a NuGet 4.0 +.</span><span class="sxs-lookup"><span data-stu-id="81a60-129">This topic applies to project types other than .NET Core projects using Visual Studio 2017 and NuGet 4.0+.</span></span> <span data-ttu-id="81a60-130">V těchto projektech .NET Core NuGet používá informace v `.csproj` souboru přímo.</span><span class="sxs-lookup"><span data-stu-id="81a60-130">In those .NET Core projects, NuGet uses information in the `.csproj` file directly.</span></span> <span data-ttu-id="81a60-131">Podrobnosti najdete v tématu [vytvořit .NET standardní balíčky s Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) a [NuGet pack a obnovit jako cíle MSBuild](../schema/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="81a60-131">For details, see [Create .NET Standard Packages with Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) and [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md).</span></span>

## <a name="deciding-which-assemblies-to-package"></a><span data-ttu-id="81a60-132">Rozhodnutí, která sestavení do balíčku</span><span class="sxs-lookup"><span data-stu-id="81a60-132">Deciding which assemblies to package</span></span>

<span data-ttu-id="81a60-133">Většina pro obecné účely balíčky obsahují jeden nebo více sestavení, které ostatní vývojáři mohou použít ve svých vlastních projektů.</span><span class="sxs-lookup"><span data-stu-id="81a60-133">Most general-purpose packages contain one or more assemblies that other developers can use in their own projects.</span></span>

- <span data-ttu-id="81a60-134">Obecně platí je nejlepší mít jedno sestavení na balíček NuGet předpokladu, že každé sestavení je nezávisle užitečné.</span><span class="sxs-lookup"><span data-stu-id="81a60-134">In general, it's best to have one assembly per NuGet package, provided that each assembly is independently useful.</span></span> <span data-ttu-id="81a60-135">Pokud máte například `Utilities.dll` , závisí na `Parser.dll`, a `Parser.dll` je užitečné sama o sobě, a pak vytvořte jeden balíček pro každý.</span><span class="sxs-lookup"><span data-stu-id="81a60-135">For example, if you have a `Utilities.dll` that depends on `Parser.dll`, and `Parser.dll` is useful on its own, then create one package for each.</span></span> <span data-ttu-id="81a60-136">Díky tomu mohou vývojáři použít `Parser.dll` nezávisle na `Utilities.dll`.</span><span class="sxs-lookup"><span data-stu-id="81a60-136">Doing so allows developers to use `Parser.dll` independently of `Utilities.dll`.</span></span>

- <span data-ttu-id="81a60-137">Pokud vaše knihovna se skládá z více sestavení, které nejsou nezávisle užitečné, je vhodná pro jejich zkombinovat do jednoho balíčku.</span><span class="sxs-lookup"><span data-stu-id="81a60-137">If your library is composed of multiple assemblies that aren't independently useful, then it's fine to combine them into one package.</span></span> <span data-ttu-id="81a60-138">Použijeme předchozí příklad, pokud `Parser.dll` obsahuje kód, který se používá pouze systémem `Utilities.dll`, pak je v pořádku zachovat `Parser.dll` ve stejném balíčku.</span><span class="sxs-lookup"><span data-stu-id="81a60-138">Using the previous example, if `Parser.dll` contains code that's used only by `Utilities.dll`, then it's fine to keep `Parser.dll` in the same package.</span></span>
    - <span data-ttu-id="81a60-139">Podobně pokud `Utilities.dll` závisí na `Utilities.resources.dll`, je-li znovu tento není užitečné sama o sobě, pak přesuňte i ve stejném balíčku.</span><span class="sxs-lookup"><span data-stu-id="81a60-139">Similarly, if `Utilities.dll` depends on `Utilities.resources.dll`, where again the latter is not useful on its own, then put both in the same package.</span></span>

<span data-ttu-id="81a60-140">Prostředky jsou ve skutečnosti ve speciálním případě.</span><span class="sxs-lookup"><span data-stu-id="81a60-140">Resources are, in fact, a special case.</span></span> <span data-ttu-id="81a60-141">Při instalaci balíčku do projektu NuGet automaticky přidá odkazy na sestavení pro knihovny DLL balíčku, *s výjimkou* ty, které jsou s názvem `.resources.dll` vzhledem k tomu, že se předpokládá, že lokalizované satelitní sestavení (viz [ Vytvoření lokalizovaných balíčků](creating-localized-packages.md)).</span><span class="sxs-lookup"><span data-stu-id="81a60-141">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies (see [Creating localized packages](creating-localized-packages.md)).</span></span> <span data-ttu-id="81a60-142">Z tohoto důvodu vyhýbat se používání `.resources.dll` pro soubory, které jinak obsahují nezbytné balíček kódu.</span><span class="sxs-lookup"><span data-stu-id="81a60-142">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="81a60-143">Pokud vaše knihovna obsahuje sestavení zprostředkovatele komunikace s objekty COM, postupujte podle dalších pokynů v [vytváření balíčků s sestavení vzájemné spolupráce COM](#authoring-packages-with-com-interop-assemblies).</span><span class="sxs-lookup"><span data-stu-id="81a60-143">If your library contains COM interop assemblies, follow additional the guidelines in [Authoring packages with COM interop assemblies](#authoring-packages-with-com-interop-assemblies).</span></span>

## <a name="the-role-and-structure-of-the-nuspec-file"></a><span data-ttu-id="81a60-144">Role a struktura souboru s příponou .nuspec</span><span class="sxs-lookup"><span data-stu-id="81a60-144">The role and structure of the .nuspec file</span></span>

<span data-ttu-id="81a60-145">Jakmile již víte, jaké soubory, které chcete balíček a dalším krokem je vytvoření manifestu balíčku v `.nuspec` souboru XML.</span><span class="sxs-lookup"><span data-stu-id="81a60-145">Once you know what files you want to package, the next step is creating a package manifest in a `.nuspec` XML file.</span></span>

<span data-ttu-id="81a60-146">V manifestu:</span><span class="sxs-lookup"><span data-stu-id="81a60-146">The manifest:</span></span>

1. <span data-ttu-id="81a60-147">Popisuje obsah balíčku a je sám součástí balíčku.</span><span class="sxs-lookup"><span data-stu-id="81a60-147">Describes the package's contents and is itself included in the package.</span></span>
1. <span data-ttu-id="81a60-148">Jednotky vytvoření balíčku a dá pokyn NuGet k instalaci balíčku do projektu.</span><span class="sxs-lookup"><span data-stu-id="81a60-148">Drives both the creation of the package and instructs NuGet on how to install the package into a project.</span></span> <span data-ttu-id="81a60-149">Například manifest identifikuje další závislosti balíčků tak, aby NuGet můžete také nainstalovat těchto závislostí při instalaci hlavní balíčku.</span><span class="sxs-lookup"><span data-stu-id="81a60-149">For example, the manifest identifies other package dependencies such that NuGet can also install those dependencies when the main package is installed.</span></span>
1. <span data-ttu-id="81a60-150">Požadované a volitelné vlastnosti obsahuje, jak je popsáno níže.</span><span class="sxs-lookup"><span data-stu-id="81a60-150">Contains both required and optional properties as described below.</span></span> <span data-ttu-id="81a60-151">Přesné podrobnosti, včetně dalších vlastností, zde nejsou uvedeny najdete v tématu [příponou .nuspec odkaz](../schema/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="81a60-151">For exact details, including other properties not mentioned here, see  the [.nuspec reference](../schema/nuspec.md).</span></span>

<span data-ttu-id="81a60-152">Požadované vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="81a60-152">Required properties:</span></span>

- <span data-ttu-id="81a60-153">Identifikátor balíčku, který musí být jedinečný v rámci galerie, který je hostitelem balíčku.</span><span class="sxs-lookup"><span data-stu-id="81a60-153">The package identifier, which must be unique across the gallery that hosts the package.</span></span>
- <span data-ttu-id="81a60-154">Konkrétní verzi číslo ve tvaru *Major.Minor.Patch [-přípona]* kde *-přípona* identifikuje [předprodejní verze](Prerelease-Packages.md)</span><span class="sxs-lookup"><span data-stu-id="81a60-154">A specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](Prerelease-Packages.md)</span></span>
- <span data-ttu-id="81a60-155">Název balíčku, jako by měl se v hostitelském (např. nuget.org)</span><span class="sxs-lookup"><span data-stu-id="81a60-155">The package title as it should appears on the host (like nuget.org)</span></span>
- <span data-ttu-id="81a60-156">Informace o vytváření a vlastníka.</span><span class="sxs-lookup"><span data-stu-id="81a60-156">Author and owner information.</span></span>
- <span data-ttu-id="81a60-157">Dlouhý popis balíčku.</span><span class="sxs-lookup"><span data-stu-id="81a60-157">A long description of the package.</span></span>

<span data-ttu-id="81a60-158">Běžné volitelné vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="81a60-158">Common optional properties:</span></span>

- <span data-ttu-id="81a60-159">Poznámky k verzi</span><span class="sxs-lookup"><span data-stu-id="81a60-159">Release notes</span></span>
- <span data-ttu-id="81a60-160">Informace o autorských právech</span><span class="sxs-lookup"><span data-stu-id="81a60-160">Copyright information</span></span>
- <span data-ttu-id="81a60-161">Krátký popis [uživatelského rozhraní Správce balíčků v sadě Visual Studio](../Tools/Package-Manager-UI.md)</span><span class="sxs-lookup"><span data-stu-id="81a60-161">A short description for the [Package Manager UI in Visual Studio](../Tools/Package-Manager-UI.md)</span></span>
- <span data-ttu-id="81a60-162">ID národního prostředí</span><span class="sxs-lookup"><span data-stu-id="81a60-162">A locale ID</span></span>
- <span data-ttu-id="81a60-163">Domovská stránka a adresy URL licence</span><span class="sxs-lookup"><span data-stu-id="81a60-163">Home page and license URLs</span></span>
- <span data-ttu-id="81a60-164">Adresu URL ikony</span><span class="sxs-lookup"><span data-stu-id="81a60-164">An icon URL</span></span>
- <span data-ttu-id="81a60-165">Seznam závislosti a odkazy</span><span class="sxs-lookup"><span data-stu-id="81a60-165">Lists of dependencies and references</span></span>
- <span data-ttu-id="81a60-166">Značky, které pomáhají při hledání Galerie</span><span class="sxs-lookup"><span data-stu-id="81a60-166">Tags that assist in gallery searches</span></span>

<span data-ttu-id="81a60-167">Toto je typické (ale fiktivní) `.nuspec` soubor s komentáři popisující vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="81a60-167">The following is a typical (but fictitious) `.nuspec` file, with comments describing the properties:</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
    <!-- The identifier that must be unique within the hosting gallery -->
    <id>Contoso.Utility.UsefulStuff</id>

    <!-- The package version number that is used when resolving dependencies -->
    <version>1.8.3-beta</version>

    <!-- Authors contain text that appears directly on the gallery -->
    <authors>Dejana Tesic, Rajeev Dey</authors>

    <!-- Owners are typically nuget.org identities that allow gallery
            users to easily find other packages by the same owners.  -->
    <owners>dejanatc, rjdey</owners>

    <!-- License and project URLs provide links for the gallery -->
    <licenseUrl>http://opensource.org/licenses/MS-PL</licenseUrl>
    <projectUrl>http://github.com/contoso/UsefulStuff</projectUrl>

    <!-- The icon is used in Visual Studio's package manager UI -->
    <iconUrl>http://github.com/contoso/UsefulStuff/nuget_icon.png</iconUrl>

    <!-- If true, this value prompts the user to accept the license when
            installing the package. -->
    <requireLicenseAcceptance>false</requireLicenseAcceptance>

    <!-- Any details about this particular release -->
    <releaseNotes>Bug fixes and performance improvements</releaseNotes>

    <!-- The description can be used in package manager UI. Note that the
            nuget.org gallery uses information you add in the portal. -->
    <description>Core utility functions for web applications</description>

    <!-- Copyright information -->
    <copyright>Copyright ©2016 Contoso Corporation</copyright>

    <!-- Tags appear in the gallery and can be used for tag searches -->
    <tags>web utility http json url parsing</tags>

    <!-- Dependencies are automatically installed when the package is installed -->
    <dependencies>
        <dependency id="Newtonsoft.Json" version="9.0" />
    </dependencies>
    </metadata>

    <!-- A readme.txt to display when the package is installed -->
    <files>
        <file src="readme.txt" target="" />
    </files>
</package>
```

<span data-ttu-id="81a60-168">Podrobnosti o deklarace závislosti a zadání čísla verzí, naleznete v části [Správa verzí balíčku](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="81a60-168">For details on declaring dependencies and specifying version numbers, see [Package versioning](../reference/package-versioning.md).</span></span> <span data-ttu-id="81a60-169">Je také možné do prostor prostředky z závislosti přímo v balíčku pomocí `include` a `exclude` atributy na `dependency` elementu.</span><span class="sxs-lookup"><span data-stu-id="81a60-169">It is also possible to surface assets from dependencies directly in the package by using the `include` and `exclude` attributes on the `dependency` element.</span></span> <span data-ttu-id="81a60-170">V tématu [příponou .nuspec odkaz - závislosti](../Schema/nuspec.md#dependencies).</span><span class="sxs-lookup"><span data-stu-id="81a60-170">See [.nuspec Reference - Dependencies](../Schema/nuspec.md#dependencies).</span></span>

<span data-ttu-id="81a60-171">Manifest je zahrnutý v balíčku vytvořit z něj, proto vyhledejte libovolný počet Další příklady tak, že prověří existující balíčky.</span><span class="sxs-lookup"><span data-stu-id="81a60-171">Because the manifest is included in the package created from it, you can find any number of additional examples by examining existing packages.</span></span> <span data-ttu-id="81a60-172">Je dobré zdroj mezipaměti globální balíčku na počítači, umístění, které vrátí následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="81a60-172">A good source is the global package cache on your machine, the location of which is returned by the following command:</span></span>

```
nuget locals -list global-packages
```

<span data-ttu-id="81a60-173">Přejděte do jakéhokoli *package\version* složce, kopie `.nupkg` do souboru `.zip` souboru a pak otevřete, `.zip` soubor a zkontrolujte `.nuspec` v něm.</span><span class="sxs-lookup"><span data-stu-id="81a60-173">Go into any *package\version* folder, copy the `.nupkg` file to a `.zip` file, then open that `.zip` file and examine the `.nuspec` within it.</span></span>

> [!Note]
> <span data-ttu-id="81a60-174">Při vytváření `.nuspec` z projektu sady Visual Studio manifest obsahuje tokenů, které jsou nahrazeny informace z projektu při vytváření balíčku.</span><span class="sxs-lookup"><span data-stu-id="81a60-174">When creating a `.nuspec` from a Visual Studio project, the manifest contains tokens that are be replaced with information from the project when the package is built.</span></span> <span data-ttu-id="81a60-175">V tématu [vytváření příponou .nuspec z projektu sady Visual Studio](#from-a-visual-studio-project).</span><span class="sxs-lookup"><span data-stu-id="81a60-175">See [Creating the .nuspec from a Visual Studio project](#from-a-visual-studio-project).</span></span>

## <a name="creating-the-nuspec-file"></a><span data-ttu-id="81a60-176">Vytvoření souboru s příponou .nuspec</span><span class="sxs-lookup"><span data-stu-id="81a60-176">Creating the .nuspec file</span></span>

<span data-ttu-id="81a60-177">Vytváření dokončení manifestu obvykle začíná základní `.nuspec` souboru vygenerovaného prostřednictvím jednoho z následujících metod:</span><span class="sxs-lookup"><span data-stu-id="81a60-177">Creating a complete manifest typically begins with a basic `.nuspec` file generated through one of the following methods:</span></span>

- [<span data-ttu-id="81a60-178">Založené na konvenci pracovní adresář</span><span class="sxs-lookup"><span data-stu-id="81a60-178">A convention-based working directory</span></span>](#from-a-convention-based-working-directory)
- [<span data-ttu-id="81a60-179">Sestavení knihovny DLL</span><span class="sxs-lookup"><span data-stu-id="81a60-179">An assembly DLL</span></span>](#from-an-assembly-dll)
- [<span data-ttu-id="81a60-180">Projekt sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="81a60-180">A Visual Studio project</span></span>](#from-a-visual-studio-project)    
- [<span data-ttu-id="81a60-181">Nový soubor s výchozími hodnotami</span><span class="sxs-lookup"><span data-stu-id="81a60-181">New file with default values</span></span>](#new-file-with-default-values)

<span data-ttu-id="81a60-182">Pak upravíte soubor ručně tak, aby popisuje přesný obsah, který chcete v posledním balíčku.</span><span class="sxs-lookup"><span data-stu-id="81a60-182">You then edit the file by hand so that it describes the exact content you want in the final package.</span></span>

> [!Important]
> <span data-ttu-id="81a60-183">Generované `.nuspec` soubory obsahují zástupné symboly, které je třeba upravit před vytvořením balíčku s `nuget pack` příkaz.</span><span class="sxs-lookup"><span data-stu-id="81a60-183">Generated `.nuspec` files contain placeholders that must be modified before creating the package with the `nuget pack` command.</span></span> <span data-ttu-id="81a60-184">Příkaz selže, pokud `.nuspec` obsahuje zástupné symboly.</span><span class="sxs-lookup"><span data-stu-id="81a60-184">That command fails if the `.nuspec` contains any placeholders.</span></span>

### <a name="from-a-convention-based-working-directory"></a><span data-ttu-id="81a60-185">Z založené na konvenci pracovní adresář</span><span class="sxs-lookup"><span data-stu-id="81a60-185">From a convention-based working directory</span></span>

<span data-ttu-id="81a60-186">Protože balíčku NuGet je právě soubor ZIP, který byl přejmenován s `.nupkg` rozšíření, jeho často nejjednodušší vytvořit strukturu složek, které chcete v systému souborů, pak vytvořte `.nuspec` soubor přímo z této struktury.</span><span class="sxs-lookup"><span data-stu-id="81a60-186">Because a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension, its often easiest to create the folder structure you want on the file system, then create the `.nuspec` file directly from that structure.</span></span> <span data-ttu-id="81a60-187">`nuget pack` Příkaz automaticky přidá všechny soubory v této struktuře složek (s výjimkou všechny složky, které začínají `.`, umožňuje zachovat soubory soukromých ve stejné struktuře).</span><span class="sxs-lookup"><span data-stu-id="81a60-187">The `nuget pack` command then automatically adds all files in that folder structure (excluding any folders that begin with `.`, allowing you keep private files in the same structure).</span></span>

<span data-ttu-id="81a60-188">Výhoda tohoto přístupu je, že nemusíte v manifestu zadejte soubory, které chcete zahrnout do balíčku (jak je popsáno dále v tomto tématu).</span><span class="sxs-lookup"><span data-stu-id="81a60-188">The advantage to this approach is that you don't need to specify in the manifest which files you want to include in the package (as explained later in this topic).</span></span> <span data-ttu-id="81a60-189">Jednoduše může mít vaše procesu sestavení vytvořit strukturu přesnou složku, která přejde do balíčku a snadno můžete zahrnout další soubory, které nemusí být součástí projektu jinak:</span><span class="sxs-lookup"><span data-stu-id="81a60-189">You can simply have your build process produce the exact folder structure that goes into the package, and you can easily include other files that might not be part of a project otherwise:</span></span>

- <span data-ttu-id="81a60-190">Obsah a zdrojový kód, který by měl být vloženy do cílový projekt.</span><span class="sxs-lookup"><span data-stu-id="81a60-190">Content and source code that should be injected into the target project.</span></span>
- <span data-ttu-id="81a60-191">Skripty prostředí PowerShell (balíčky použité v NuGet 2.x může zahrnovat taky skriptů instalace, což není podporováno v NuGet 3.x a novější).</span><span class="sxs-lookup"><span data-stu-id="81a60-191">PowerShell scripts (packages used in NuGet 2.x can include installation scripts as well, which is not supported in NuGet 3.x and later).</span></span>
- <span data-ttu-id="81a60-192">Transformace na existující konfiguraci a zdrojové soubory kódu v projektu.</span><span class="sxs-lookup"><span data-stu-id="81a60-192">Transformations to existing configuration and source code files in a project.</span></span>

<span data-ttu-id="81a60-193">Konvence složky jsou následující:</span><span class="sxs-lookup"><span data-stu-id="81a60-193">The folder conventions are as follows:</span></span>

| <span data-ttu-id="81a60-194">Folder</span><span class="sxs-lookup"><span data-stu-id="81a60-194">Folder</span></span> | <span data-ttu-id="81a60-195">Popis</span><span class="sxs-lookup"><span data-stu-id="81a60-195">Description</span></span> | <span data-ttu-id="81a60-196">Akce při instalaci balíčku</span><span class="sxs-lookup"><span data-stu-id="81a60-196">Action upon package install</span></span> |
| --- | --- | --- |
| <span data-ttu-id="81a60-197">(uživatel root)</span><span class="sxs-lookup"><span data-stu-id="81a60-197">(root)</span></span> | <span data-ttu-id="81a60-198">Umístění souboru readme.txt</span><span class="sxs-lookup"><span data-stu-id="81a60-198">Location for readme.txt</span></span> | <span data-ttu-id="81a60-199">Při instalaci balíčku Visual Studio zobrazí souboru readme.txt v kořenu balíčku.</span><span class="sxs-lookup"><span data-stu-id="81a60-199">Visual Studio displays a readme.txt file in the package root when the package is installed.</span></span> |
| <span data-ttu-id="81a60-200">lib / {tfm}</span><span class="sxs-lookup"><span data-stu-id="81a60-200">lib/{tfm}</span></span> | <span data-ttu-id="81a60-201">Sestavení (`.dll`), dokumentace (`.xml`) a symbol (`.pdb`) soubory pro danou cílový Framework Přezdívka (TFM)</span><span class="sxs-lookup"><span data-stu-id="81a60-201">Assembly (`.dll`), documentation (`.xml`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="81a60-202">Sestavení jsou přidány jako odkazy; `.xml` a `.pdb` zkopírovány do složky projektu.</span><span class="sxs-lookup"><span data-stu-id="81a60-202">Assemblies are added as references; `.xml` and `.pdb` copied into project folders.</span></span> <span data-ttu-id="81a60-203">V tématu [podpora více cílové rozhraní](Supporting-Multiple-Target-Frameworks.md) pro vytvoření framework specifické pro cílové podsložky.</span><span class="sxs-lookup"><span data-stu-id="81a60-203">See [Supporting multiple target frameworks](Supporting-Multiple-Target-Frameworks.md) for creating framework target-specific sub-folders.</span></span> |
| <span data-ttu-id="81a60-204">Moduly runtime</span><span class="sxs-lookup"><span data-stu-id="81a60-204">runtimes</span></span> | <span data-ttu-id="81a60-205">Architektura konkrétní sestavení (`.dll`), symbol (`.pdb`) a nativní prostředků (`.pri`) souborů</span><span class="sxs-lookup"><span data-stu-id="81a60-205">Architecture-specific assembly (`.dll`), symbol (`.pdb`), and native resource (`.pri`) files</span></span> | <span data-ttu-id="81a60-206">Sestavení jsou přidány jako odkazy; ostatní soubory se zkopírují do složky projektu.</span><span class="sxs-lookup"><span data-stu-id="81a60-206">Assemblies are added as references; other files are copied into project folders.</span></span> <span data-ttu-id="81a60-207">V tématu [podpora více cílové rozhraní](Supporting-Multiple-Target-Frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="81a60-207">See [Supporting multiple target frameworks](Supporting-Multiple-Target-Frameworks.md).</span></span> |
| <span data-ttu-id="81a60-208">obsah</span><span class="sxs-lookup"><span data-stu-id="81a60-208">content</span></span> | <span data-ttu-id="81a60-209">Různé soubory</span><span class="sxs-lookup"><span data-stu-id="81a60-209">Arbitrary files</span></span> | <span data-ttu-id="81a60-210">Obsah je zkopírován do kořenového adresáře projektu.</span><span class="sxs-lookup"><span data-stu-id="81a60-210">Contents are copied to the project root.</span></span> <span data-ttu-id="81a60-211">Představte si, že **obsah** složky jako kořen cílová aplikace, který nakonec využívá balíčku.</span><span class="sxs-lookup"><span data-stu-id="81a60-211">Think of the **content** folder as the root of the target application that ultimately consumes the package.</span></span> <span data-ttu-id="81a60-212">Do mají balíček přidat bitovou kopii do aplikace */image* složku, umístěte ji do balíčku *obsah nebo obrázky* složky.</span><span class="sxs-lookup"><span data-stu-id="81a60-212">To have the package add an image in the application's */images* folder, place it in the package's *content/images* folder.</span></span> |
| <span data-ttu-id="81a60-213">sestavení</span><span class="sxs-lookup"><span data-stu-id="81a60-213">build</span></span> | <span data-ttu-id="81a60-214">MSBuild `.targets` a `.props` soubory</span><span class="sxs-lookup"><span data-stu-id="81a60-214">MSBuild `.targets` and `.props` files</span></span> | <span data-ttu-id="81a60-215">Automaticky vloží do souboru projektu (NuGet 2.x) nebo `project.lock.json` (NuGet 3.x+).</span><span class="sxs-lookup"><span data-stu-id="81a60-215">Automatically inserted into the project file (NuGet 2.x) or `project.lock.json` (NuGet 3.x+).</span></span> |
| <span data-ttu-id="81a60-216">nástroje</span><span class="sxs-lookup"><span data-stu-id="81a60-216">tools</span></span> | <span data-ttu-id="81a60-217">Skripty prostředí PowerShell a programy, které jsou přístupné z konzoly Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="81a60-217">Powershell scripts and programs accessible from the Package Manager Console</span></span> | <span data-ttu-id="81a60-218">`tools` Se přidá složka `PATH` proměnnou prostředí pro konzolu Správce balíčků (konkrétně *není* k `PATH` jako sada pro MSBuild při sestavování projektu).</span><span class="sxs-lookup"><span data-stu-id="81a60-218">The `tools` folder is added to the `PATH` environment variable for the Package Manager Console only (Specifically, *not* to the `PATH` as set for MSBuild when building the project).</span></span> |

<span data-ttu-id="81a60-219">Protože struktury složky může obsahovat libovolný počet sestavení pro libovolný počet cílové rozhraní, tato metoda je nutné při vytváření balíčků, které podporují více rozhraní</span><span class="sxs-lookup"><span data-stu-id="81a60-219">Because your folder structure can contain any number of assemblies for any number of target frameworks, this method is necessary when creating packages that support multiple frameworks</span></span> 

<span data-ttu-id="81a60-220">V každém případě až budete mít struktuře požadované složky na místě, spusťte následující příkaz v této složce vytvořit `.nuspec` souboru:</span><span class="sxs-lookup"><span data-stu-id="81a60-220">In any case, once you have the desired folder structure in place, run the following command in that folder to create the `.nuspec` file:</span></span>

```
nuget spec
```

<span data-ttu-id="81a60-221">Znovu vygenerovaný `.nuspec` neobsahuje žádné explicitní odkazy na soubory v této struktuře.</span><span class="sxs-lookup"><span data-stu-id="81a60-221">Again, the generated `.nuspec` contains no explicit references to files in the folder structure.</span></span> <span data-ttu-id="81a60-222">NuGet automaticky zahrne všechny soubory, když je balíček vytvořen.</span><span class="sxs-lookup"><span data-stu-id="81a60-222">NuGet automatically includes all files when the package is created.</span></span> <span data-ttu-id="81a60-223">Stále je třeba upravit zástupné hodnoty v dalších částech tohoto manifest, ale.</span><span class="sxs-lookup"><span data-stu-id="81a60-223">You still need to edit placeholder values in other parts of the manifest, however.</span></span>

### <a name="from-an-assembly-dll"></a><span data-ttu-id="81a60-224">Ze sestavení knihoven DLL</span><span class="sxs-lookup"><span data-stu-id="81a60-224">From an assembly DLL</span></span>

<span data-ttu-id="81a60-225">V případě jednoduchého vytváření balíčku ze sestavení může generovat `.nuspec` souboru z metadat v sestavení pomocí následujícího příkazu:</span><span class="sxs-lookup"><span data-stu-id="81a60-225">In the simple case of creating a package from an assembly, you can generate a `.nuspec` file from the metadata in the assembly using the following command:</span></span>

```
nuget spec <assembly-name>.dll
```

<span data-ttu-id="81a60-226">Pomocí tohoto formuláře nahradí konkrétní hodnoty od sestavení, několik zástupné symboly v manifestu.</span><span class="sxs-lookup"><span data-stu-id="81a60-226">Using this form replaces a few placeholders in the manifest with specific values from the assembly.</span></span> <span data-ttu-id="81a60-227">Například `<id>` je nastavena na název sestavení a `<version>` je nastaven na verzi sestavení.</span><span class="sxs-lookup"><span data-stu-id="81a60-227">For example, the `<id>` property is set to the assembly name, and `<version>` is set to the assembly version.</span></span> <span data-ttu-id="81a60-228">Ostatní vlastnosti v manifestu, ale nemáte mít odpovídající hodnoty v sestavení a stále proto obsahují zástupné symboly.</span><span class="sxs-lookup"><span data-stu-id="81a60-228">Other properties in the manifest, however, don't have matching values in the assembly and thus still contain placeholders.</span></span>

### <a name="from-a-visual-studio-project"></a><span data-ttu-id="81a60-229">Z projektu sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="81a60-229">From a Visual Studio project</span></span>

<span data-ttu-id="81a60-230">Vytváření `.nuspec` z `.csproj` nebo `.vbproj` souboru je vhodné, protože jiné balíčky, které byly nainstalovány do těchto projektu se automaticky odkazuje jako závislosti.</span><span class="sxs-lookup"><span data-stu-id="81a60-230">Creating a `.nuspec` from a `.csproj` or `.vbproj` file is convenient because other packages that have been installed into those project are automatically referenced as dependencies.</span></span> <span data-ttu-id="81a60-231">Ve stejné složce jako soubor projektu jednoduše použijte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="81a60-231">Simply use the following command in the same folder as the project file:</span></span>

```
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

<span data-ttu-id="81a60-232">Výsledná `<project-name>.nuspec` soubor obsahuje *tokeny* , se nahrazují během balení hodnoty z projektu, včetně odkazů na další balíčky, které již jsou nainstalovány.</span><span class="sxs-lookup"><span data-stu-id="81a60-232">The resulting `<project-name>.nuspec` file contains *tokens* that are replaced at packaging time with values from the project, including references to any other packages that have already been installed.</span></span>

<span data-ttu-id="81a60-233">Token je oddělená `$` symboly na obou stranách vlastnosti projektu.</span><span class="sxs-lookup"><span data-stu-id="81a60-233">A token is delimited by `$` symbols on both sides of the project property.</span></span> <span data-ttu-id="81a60-234">Například `<id>` hodnota v manifestu vygenerované v tomto způsobem obvykle vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="81a60-234">For example, the `<id>` value in a manifest generated in this way typically appears as follows:</span></span>

```xml
<id>$id$</id>
```

<span data-ttu-id="81a60-235">Tento token nahrazen `AssemblyName` hodnotu ze souboru projektu v balení čas.</span><span class="sxs-lookup"><span data-stu-id="81a60-235">This token is replaced with the `AssemblyName` value from the project file at packing time.</span></span> <span data-ttu-id="81a60-236">Pro přesné mapování projektu hodnot na `.nuspec` tokeny, najdete v článku [odkazovat nahrazení tokeny](../schema/nuspec.md#replacement-tokens).</span><span class="sxs-lookup"><span data-stu-id="81a60-236">For the exact mapping of project values to `.nuspec` tokens, see the [Replacement Tokens reference](../schema/nuspec.md#replacement-tokens).</span></span>

<span data-ttu-id="81a60-237">Tokeny můžete snížit z museli klíčové hodnoty jako číslo verze v aktualizovat `.nuspec` jako aktualizace projektu.</span><span class="sxs-lookup"><span data-stu-id="81a60-237">Tokens relieve you from needing to update crucial values like the version number in the `.nuspec` as you update the project.</span></span> <span data-ttu-id="81a60-238">(Můžete vždy nahradit tokeny literálových hodnot v případě potřeby).</span><span class="sxs-lookup"><span data-stu-id="81a60-238">(You can always replace the tokens with literal values, if desired).</span></span> 

<span data-ttu-id="81a60-239">Všimněte si, že existuje několik další balení možností při práci z projektu sady Visual Studio, jak je popsáno v [systémem nuget aktualizací Service pack ke generování souboru .nupkg v podadresáři](#running-nuget-pack-to-generate-the-nupkg-file) později.</span><span class="sxs-lookup"><span data-stu-id="81a60-239">Note that there are several additional packaging options available when working from a Visual Studio project, as described in [Running nuget pack to generate the .nupkg file](#running-nuget-pack-to-generate-the-nupkg-file) later on.</span></span>

#### <a name="solution-level-packages"></a><span data-ttu-id="81a60-240">Balíčky úrovni řešení</span><span class="sxs-lookup"><span data-stu-id="81a60-240">Solution-level packages</span></span>

<span data-ttu-id="81a60-241">*NuGet pouze 2.x. Není k dispozici v NuGet 3.0 +.*</span><span class="sxs-lookup"><span data-stu-id="81a60-241">*NuGet 2.x only. Not available in NuGet 3.0+.*</span></span>

<span data-ttu-id="81a60-242">NuGet 2.x podporované představu o úrovni řešení balíček, který nainstaluje nástroje nebo další příkazy pro konzolu Správce balíčků (obsah `tools` složky), ale nemá přidejte odkazy na obsah, nebo vytvořit vlastní nastavení na všechny projekty v řešení.</span><span class="sxs-lookup"><span data-stu-id="81a60-242">NuGet 2.x supported the notion of a solution-level package that installs tools or additional commands for the Package Manager Console (the contents of the `tools` folder), but does not add references, content, or build customizations to any projects in the solution.</span></span> <span data-ttu-id="81a60-243">Tyto balíčky obsahovat žádné soubory v jeho přímo `lib`, `content`, nebo `build` složek a jeden z jejich závislých mít soubory v jejich odpovídajících `lib`, `content`, nebo `build` složek.</span><span class="sxs-lookup"><span data-stu-id="81a60-243">Such packages contain no files in its direct `lib`, `content`, or `build` folders, and none of its dependencies have files in their respective `lib`, `content`, or `build` folders.</span></span> 

<span data-ttu-id="81a60-244">Sleduje NuGet nainstalované balíky úrovni řešení v `packages.config` v soubor `.nuget` složky, nikoli projektu `packages.config` souboru.</span><span class="sxs-lookup"><span data-stu-id="81a60-244">NuGet tracks installed solution-level packages in a `packages.config` file in the `.nuget` folder, rather than the project's `packages.config` file.</span></span>

### <a name="new-file-with-default-values"></a><span data-ttu-id="81a60-245">Nový soubor s výchozími hodnotami</span><span class="sxs-lookup"><span data-stu-id="81a60-245">New file with default values</span></span>

<span data-ttu-id="81a60-246">Následující příkaz vytvoří výchozí manifest se zástupnými symboly, což zajistí, že začínáte s strukturu správný soubor:</span><span class="sxs-lookup"><span data-stu-id="81a60-246">The following command creates a default manifest with placeholders, which ensures you start with the proper file structure:</span></span>

```
nuget spec [<package-name>]
```

<span data-ttu-id="81a60-247">Pokud vynecháte \<název balíčku\>, bude výsledný soubor je `Package.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="81a60-247">If you omit \<package-name\>, the resulting file is `Package.nuspec`.</span></span> <span data-ttu-id="81a60-248">Pokud je třeba zadat název `Contoso.Utility.UsefulStuff`, je soubor `Contoso.Utility.UsefulStuff.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="81a60-248">If you provide a name such as `Contoso.Utility.UsefulStuff`, the file is `Contoso.Utility.UsefulStuff.nuspec`.</span></span>

<span data-ttu-id="81a60-249">Výsledná `.nuspec` obsahuje zástupné symboly pro hodnot, jako `projectUrl`.</span><span class="sxs-lookup"><span data-stu-id="81a60-249">The resulting `.nuspec` contains placeholders for values like the `projectUrl`.</span></span> <span data-ttu-id="81a60-250">Nezapomeňte upravit soubor než jej použijete k vytvoření konečné `.nupkg` souboru.</span><span class="sxs-lookup"><span data-stu-id="81a60-250">Be sure to edit the file before using it to create the final `.nupkg` file.</span></span>

## <a name="choosing-a-unique-package-identifier-and-setting-the-version-number"></a><span data-ttu-id="81a60-251">Výběr balíčku jedinečný identifikátor a nastavení číslo verze</span><span class="sxs-lookup"><span data-stu-id="81a60-251">Choosing a unique package identifier and setting the version number</span></span>

<span data-ttu-id="81a60-252">Identifikátor balíčku (`<id>` element) a číslo verze (`<version>` element) jsou dvě nejdůležitější hodnoty v manifestu, protože jednoznačně identifikují přesný kód, který je součástí balíčku.</span><span class="sxs-lookup"><span data-stu-id="81a60-252">The package identifier (`<id>` element) and the version number (`<version>` element) are the two most important values in the manifest because they uniquely identify the exact code that's contained in the package.</span></span>

<span data-ttu-id="81a60-253">**Osvědčené postupy pro identifikátor balíčku:**</span><span class="sxs-lookup"><span data-stu-id="81a60-253">**Best practices for the package identifier:**</span></span>

- <span data-ttu-id="81a60-254">**Jedinečnost**: identifikátor musí být jedinečný v rámci nuget.org nebo jakoukoli Galerie hostitelem balíčku.</span><span class="sxs-lookup"><span data-stu-id="81a60-254">**Uniqueness**: The identifier must be unique across nuget.org or whatever gallery hosts the package.</span></span> <span data-ttu-id="81a60-255">Než se rozhodnete, že na identifikátor, vyhledejte galerii použít ke kontrole, pokud název je již používán.</span><span class="sxs-lookup"><span data-stu-id="81a60-255">Before deciding on an identifier, search the applicable gallery to check if the name is already in use.</span></span> <span data-ttu-id="81a60-256">Aby nedocházelo ke konfliktům, dobrým způsobem je použít název vaší společnosti jako první část identifikátor, jako například `Contoso.`.</span><span class="sxs-lookup"><span data-stu-id="81a60-256">To avoid conflicts, a good pattern is to use your company name as the first part of the identifier, such as `Contoso.`.</span></span>
- <span data-ttu-id="81a60-257">**Namespace jako názvy**: postupujte podle vzor podobná obory názvů v rozhraní .NET, pomocí zápisu s tečkou místo pomlčky.</span><span class="sxs-lookup"><span data-stu-id="81a60-257">**Namespace-like names**: Follow a pattern similar to namespaces in .NET, using dot notation instead of hyphens.</span></span> <span data-ttu-id="81a60-258">Například použít `Contoso.Utility.UsefulStuff` místo `Contoso-Utility-UsefulStuff` nebo `Contoso_Utility_UsefulStuff`.</span><span class="sxs-lookup"><span data-stu-id="81a60-258">For example, use `Contoso.Utility.UsefulStuff` rather than `Contoso-Utility-UsefulStuff` or `Contoso_Utility_UsefulStuff`.</span></span> <span data-ttu-id="81a60-259">Příjemci knihovny také užitečné, když se identifikátor balíčku shoduje s obory názvů používá v kódu.</span><span class="sxs-lookup"><span data-stu-id="81a60-259">Consumers also find it helpful when the package identifier matches the namespaces used in the code.</span></span>
- <span data-ttu-id="81a60-260">**Ukázkové balíčky**: Pokud vytvořit balíček ukázkový kód, který ukazuje, jak chcete použít jiný balíček, připojit `.Sample` jako příponu k identifikátoru, jako v `Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="81a60-260">**Sample Packages**: If you produce a package of sample code that demonstrates how to use another package, attach `.Sample` as a suffix to the identifier, as in `Contoso.Utility.UsefulStuff.Sample`.</span></span> <span data-ttu-id="81a60-261">(Balíček ukázkové by samozřejmě jsou závislé na jiný balíček.) Při vytváření balíčku ukázka, použijte založené na konvenci pracovní adresář metody popsané výše.</span><span class="sxs-lookup"><span data-stu-id="81a60-261">(The sample package would of course have a dependency on the other package.) When creating a sample package, use the convention-based working directory method described earlier.</span></span> <span data-ttu-id="81a60-262">V `content` složce uspořádat ukázkový kód ve složce s názvem `\Samples\<identifier>` jako v `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="81a60-262">In the `content` folder, arrange the sample code in a folder called `\Samples\<identifier>` as in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span></span>

<span data-ttu-id="81a60-263">**Osvědčené postupy pro verze balíčku:**</span><span class="sxs-lookup"><span data-stu-id="81a60-263">**Best practices for the package version:**</span></span>

- <span data-ttu-id="81a60-264">Obecně platí nastavte verze balíčku tak, aby odpovídaly knihovny, i když to není nezbytně nutné.</span><span class="sxs-lookup"><span data-stu-id="81a60-264">In general, set the version of the package to match the library, though this is not strictly required.</span></span> <span data-ttu-id="81a60-265">Toto je představuje jednoduché při omezit balíčku do jednoho sestavení, jak je popsáno výše v [rozhodnutí, která sestavení balíčku](#deciding-which-assemblies-to-package).</span><span class="sxs-lookup"><span data-stu-id="81a60-265">This is a simple matter when you limit a package to a single assembly, as described earlier in [Deciding which assemblies to package](#deciding-which-assemblies-to-package).</span></span> <span data-ttu-id="81a60-266">Celkově platí nezapomeňte, že NuGet samotné se zabývá verze balíčku při rozpoznávání závislostem není verzí sestavení.</span><span class="sxs-lookup"><span data-stu-id="81a60-266">Overall, remember that NuGet itself deals with package versions when resolving dependencies, not assembly versions.</span></span>
- <span data-ttu-id="81a60-267">Při použití nestandardní verzi schématu, nezapomeňte pravidla verzí NuGet zvažte, jak je popsáno v [Správa verzí balíčku](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="81a60-267">When using a non-standard version scheme, be sure to consider the NuGet versioning rules as explained in [Package versioning](../reference/package-versioning.md).</span></span>

> <span data-ttu-id="81a60-268">Následující řadu příspěvcích na blogu stručný jsou také užitečné rozumět Správa verzí:</span><span class="sxs-lookup"><span data-stu-id="81a60-268">The following series of brief blog posts are also helpful to understand versioning:</span></span>
>
> - [<span data-ttu-id="81a60-269">Část 1: Pořízení na knihoven DLL</span><span class="sxs-lookup"><span data-stu-id="81a60-269">Part 1: Taking on DLL Hell</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [<span data-ttu-id="81a60-270">Část 2: Algoritmus jádra</span><span class="sxs-lookup"><span data-stu-id="81a60-270">Part 2: The core algorithm</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [<span data-ttu-id="81a60-271">Část 3: Sjednocení prostřednictvím přesměrování vazby</span><span class="sxs-lookup"><span data-stu-id="81a60-271">Part 3: Unification via Binding Redirects</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="setting-a-package-type"></a><span data-ttu-id="81a60-272">Balíček typ nastavení</span><span class="sxs-lookup"><span data-stu-id="81a60-272">Setting a package type</span></span>

<span data-ttu-id="81a60-273">U balíčku NuGet 3.5 +, může být označen balíčky konkrétní *typ balíčku* indikující její zamýšlené použití.</span><span class="sxs-lookup"><span data-stu-id="81a60-273">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="81a60-274">Balíčky s typem, včetně všech balíčky vytvořené pomocí dřívějších verzích systému NuGet, nebyl označen jako výchozí `Dependency` typu.</span><span class="sxs-lookup"><span data-stu-id="81a60-274">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="81a60-275">`Dependency`Typ balíčky sestavení nebo běhu prostředky přidat do knihovny a aplikace a lze nainstalovat do libovolného typu projektu (za předpokladu, že jsou kompatibilní).</span><span class="sxs-lookup"><span data-stu-id="81a60-275">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="81a60-276">`DotnetCliTool`Typ balíčky jsou rozšíření [rozhraní příkazového řádku .NET](/dotnet/articles/core/tools/index) a jsou vyvolány z příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="81a60-276">`DotnetCliTool` type packages are extensions to the [.NET CLI](/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="81a60-277">Tyto balíčky lze nainstalovat pouze v projektech .NET Core a mít žádný vliv na operace obnovení.</span><span class="sxs-lookup"><span data-stu-id="81a60-277">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="81a60-278">Další podrobnosti o těchto – projekt rozšíření jsou k dispozici v [rozšiřitelnost .NET Core](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) dokumentaci.</span><span class="sxs-lookup"><span data-stu-id="81a60-278">More details about these per-project extensions are available in the  [.NET Core extensibility](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

    <span data-ttu-id="81a60-279">Pokud je nainstalován balíček DotnetCliTool, Visual Studio umístí balíček v `project.json` `tools` uzlu místo `dependencies` uzlu.</span><span class="sxs-lookup"><span data-stu-id="81a60-279">When a DotnetCliTool package is installed, Visual Studio places the package in the `project.json` `tools` node instead of the `dependencies` node.</span></span>

- <span data-ttu-id="81a60-280">Vlastní typ balíčků, použijte identifikátor libovolný typ, který vyhovuje pravidlům stejný formát jako ID balíčku.</span><span class="sxs-lookup"><span data-stu-id="81a60-280">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="81a60-281">Jakýkoli typ jinými než `Dependency` a `DotnetCliTool`, ale nejsou rozpoznány pomocí Správce balíčků NuGet v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="81a60-281">Any type other than `Dependency` and `DotnetCliTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="81a60-282">Typy balíčků jsou nastavené buď `.nuspec` souboru nebo v `project.json`.</span><span class="sxs-lookup"><span data-stu-id="81a60-282">Package types are set either in the `.nuspec` file or in `project.json`.</span></span> <span data-ttu-id="81a60-283">V obou případech je nejvhodnější pro zpětné kompatibility na *není* explicitně nastaven `Dependency` zadejte a místo toho spoléhají na NuGet tohoto typu, pokud žádný typ za předpokladu, že je zadán.</span><span class="sxs-lookup"><span data-stu-id="81a60-283">In both cases, it's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="81a60-284">`.nuspec`: Označuje typ balíčku v rámci `packageTypes\packageType` pod uzlem `<metadata>` element:</span><span class="sxs-lookup"><span data-stu-id="81a60-284">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetCliTool" />
        </packageTypes>
        </metadata>
    </package>
    ```

- <span data-ttu-id="81a60-285">`project.json`: Označuje typ balíčku v rámci `packOptions.packageType` vlastnosti json:</span><span class="sxs-lookup"><span data-stu-id="81a60-285">`project.json`: Indicate the package type within a `packOptions.packageType` property json:</span></span>

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="81a60-286">Přidání soubor readme a další soubory</span><span class="sxs-lookup"><span data-stu-id="81a60-286">Adding a readme and other files</span></span>

<span data-ttu-id="81a60-287">Pokud chcete přímo zadat soubory, které chcete zahrnout do balíčku, použijte `<files>` uzel v `.nuspec` souboru, který *následuje* `<metadata>` značky:</span><span class="sxs-lookup"><span data-stu-id="81a60-287">To directly specify files to include in the package, use the `<files>` node in the `.nuspec` file, which *follows* the `<metadata>` tag:</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
    <!-- ... -->
    </metadata>
    <files>
    <!-- Add a readme -->
    <file src="readme.txt" target="" />

    <!-- Add files from an arbitrary folder that's not necessarily in the project -->
    <file src="..\..\SomeRoot\**\*.*" target="" />
    </files>
</package>
```

> [!Tip]
> <span data-ttu-id="81a60-288">Při použití přístup založené na konvenci pracovní adresář, můžete umístit souboru readme.txt kořenového adresáře balíčku a další obsah `content` složky.</span><span class="sxs-lookup"><span data-stu-id="81a60-288">When using the convention-based working directory approach, you can place the readme.txt in the package root and other content in the `content` folder.</span></span> <span data-ttu-id="81a60-289">Ne `<file>` prvky jsou nezbytné v manifestu.</span><span class="sxs-lookup"><span data-stu-id="81a60-289">No `<file>` elements are necessary in the manifest.</span></span>

<span data-ttu-id="81a60-290">Pokud zahrnete soubor s názvem `readme.txt` v kořenu balíčku sady Visual Studio zobrazí obsah tohoto souboru jako prostý text okamžitě po instalaci balíčku přímo.</span><span class="sxs-lookup"><span data-stu-id="81a60-290">When you include a file named `readme.txt` in the package root, Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="81a60-291">(Soubory Readme nejsou zobrazeny pro balíčky nainstalované jako závislosti).</span><span class="sxs-lookup"><span data-stu-id="81a60-291">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="81a60-292">Můžete zde je ukázka, jak se zobrazí v souboru readme pro balíček HtmlAgilityPack:</span><span class="sxs-lookup"><span data-stu-id="81a60-292">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Zobrazení soubor readme pro balíček NuGet po instalaci](media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="81a60-294">Pokud zahrnete prázdnou `<files>` uzel v `.nuspec` souboru NuGet neobsahuje žádný jiný obsah v balíčku než co je v `lib` složky.</span><span class="sxs-lookup"><span data-stu-id="81a60-294">If you include an empty `<files>` node in the `.nuspec` file, NuGet doesn't include any other content in the package other than what's in the `lib` folder.</span></span>

## <a name="including-msbuild-props-and-targets-in-a-package"></a><span data-ttu-id="81a60-295">Včetně MSBuild props a cíle v balíčku</span><span class="sxs-lookup"><span data-stu-id="81a60-295">Including MSBuild props and targets in a package</span></span>

<span data-ttu-id="81a60-296">V některých případech můžete chtít přidat vlastní sestavovací cíle nebo vlastnosti v projektech, které využívají vašeho balíčku, jako je například spuštění vlastního nástroje nebo procesu během vytváření sestavení.</span><span class="sxs-lookup"><span data-stu-id="81a60-296">In some cases, you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="81a60-297">To uděláte tak, že soubory ve formátu `<package_id>.targets` nebo `<package_id>.props` (například `Contoso.Utility.UsefulStuff.targets`) v rámci `\build` složce projektu.</span><span class="sxs-lookup"><span data-stu-id="81a60-297">You do this by placing files in the form `<package_id>.targets` or `<package_id>.props` (such as `Contoso.Utility.UsefulStuff.targets`) within the `\build` folder of the project.</span></span>

<span data-ttu-id="81a60-298">Soubory v kořenovém `\build` složky jsou považovány za vhodné pro všechny cílové architektury.</span><span class="sxs-lookup"><span data-stu-id="81a60-298">Files in the root `\build` folder are considered suitable for all target frameworks.</span></span> <span data-ttu-id="81a60-299">Pokud chcete zadat konkrétní rozhraní soubory, nejprve umístíte těch v rámci příslušných podsložek, například následující:</span><span class="sxs-lookup"><span data-stu-id="81a60-299">To provide framework-specific files, first place those within appropriate subfolders, such as the following:</span></span>

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

<span data-ttu-id="81a60-300">Potom v `.nuspec` souboru, ujistěte se, který bude odkazovat na těchto souborů v `<files>` uzlu:</span><span class="sxs-lookup"><span data-stu-id="81a60-300">Then in the `.nuspec` file, be sure to refer to these files in the `<files>` node:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <!-- ... -->
    </metadata>
    <files>
    <!-- Include everything in \build -->
    <file src="build\**" target="build" />

    <!-- Other files -->
    <!-- ... -->
    </files>
</package>
```

<span data-ttu-id="81a60-301">Když NuGet 2.x nainstaluje balíček s `\build` soubory, přidá MSBuild `<Import>` elementy v souboru projektu odkazující na `.targets` a `.props` soubory.</span><span class="sxs-lookup"><span data-stu-id="81a60-301">When NuGet 2.x installs a package with `\build` files, it adds an MSBuild `<Import>` elements in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="81a60-302">(`.props` se přidá na začátek souboru projektu; `.targets` se přidá na dolní.)</span><span class="sxs-lookup"><span data-stu-id="81a60-302">(`.props` is added at the top of the project file; `.targets` is added at the bottom.)</span></span>

<span data-ttu-id="81a60-303">U balíčku NuGet 3.x, cíle nejsou přidány do projektu, ale místo toho jsou k dispozici prostřednictvím `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="81a60-303">With NuGet 3.x, targets are not added to the project but are instead made available through the `project.lock.json`.</span></span>

## <a name="authoring-packages-with-com-interop-assemblies"></a><span data-ttu-id="81a60-304">Vytváření balíčků s sestavení vzájemné spolupráce COM</span><span class="sxs-lookup"><span data-stu-id="81a60-304">Authoring packages with COM interop assemblies</span></span>

<span data-ttu-id="81a60-305">Balíčky, které obsahují sestavení vzájemné spolupráce COM musí obsahovat odpovídající [cíle souboru](#including-msbuild-props-and-targets-in-a-package) tak, aby správný `EmbedInteropTypes` metadata jsou přidány do projektů pomocí formátu PackageReference.</span><span class="sxs-lookup"><span data-stu-id="81a60-305">Packages that contain COM interop assemblies must include an appropriate [targets file](#including-msbuild-props-and-targets-in-a-package) so that the correct `EmbedInteropTypes` metadata is added to projects using the PackageReference format.</span></span> <span data-ttu-id="81a60-306">Ve výchozím nastavení `EmbedInteropTypes` metadata je vždy hodnotu false pro všechna sestavení při PackageReference se používá, takže soubor cíle přidá tato metadata explicitně.</span><span class="sxs-lookup"><span data-stu-id="81a60-306">By default, the `EmbedInteropTypes` metadata is always false for all assemblies when PackageReference is used, so the targets file adds this metadata explicitly.</span></span> <span data-ttu-id="81a60-307">Aby nedocházelo ke konfliktům, musí být cílový název jedinečné; v ideálním případě použít kombinaci váš název balíčku a sestavení se embedded, ve které nahradíte `{InteropAssemblyName}` v níže uvedeném příkladu s danou hodnotou.</span><span class="sxs-lookup"><span data-stu-id="81a60-307">To avoid conflicts, the target name should be unique; ideally, use a combination of your package name and the assembly being embedded, replacing the `{InteropAssemblyName}` in the example below with that value.</span></span> <span data-ttu-id="81a60-308">(Viz také [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) příklad.)</span><span class="sxs-lookup"><span data-stu-id="81a60-308">(Also see [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) for an example.)</span></span>

```xml      
<Target Name="EmbeddingAssemblyNameFromPackageId" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <PropertyGroup>
    <_InteropAssemblyFileName>{InteropAssemblyName}</_InteropAssemblyFileName>
  </PropertyGroup>
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '$(_InteropAssemblyFileName)' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

<span data-ttu-id="81a60-309">Všimněte si, že při použití `packages.config` NuGet a sady Visual Studio pro kontrolu sestavení vzájemné spolupráce COM a nastavit přidávání odkazů na sestavení z balíčků způsobí, že formát reference `EmbedInteropTypes` na hodnotu true v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="81a60-309">Note that when using the `packages.config` reference format, adding references to the assemblies from the packages causes NuGet and Visual Studio to check for COM interop assemblies and set the `EmbedInteropTypes` to true in the project file.</span></span> <span data-ttu-id="81a60-310">V tomto případě jsou cíle elementem.</span><span class="sxs-lookup"><span data-stu-id="81a60-310">In this case the targets are overriden.</span></span>

<span data-ttu-id="81a60-311">Kromě toho ve výchozím nastavení [toku prostředky sestavení není přechodně](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="81a60-311">Additionally, by default the [build assets do not flow transitively](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span> <span data-ttu-id="81a60-312">Balíčky vytvořené podle postupu popsaného tady pracovní jinak po jejich vyjmutí jako přenositelné závislost z odkaz na projekt na projekt.</span><span class="sxs-lookup"><span data-stu-id="81a60-312">Packages authored as described here work differently when they are pulled as a transitive dependency from a project to project reference.</span></span> <span data-ttu-id="81a60-313">Příjemce balíček můžete jim toku změnou výchozí hodnota PrivateAssets tak, aby neobsahoval sestavení povolit.</span><span class="sxs-lookup"><span data-stu-id="81a60-313">The package consumer can allow them to flow by modifying the PrivateAssets default value to not include build.</span></span>  

<a name="creating-the-package"></a>

## <a name="running-nuget-pack-to-generate-the-nupkg-file"></a><span data-ttu-id="81a60-314">S aktualizací Service pack nuget ke generování souboru .nupkg v podadresáři</span><span class="sxs-lookup"><span data-stu-id="81a60-314">Running nuget pack to generate the .nupkg file</span></span>

<span data-ttu-id="81a60-315">Pokud používáte sestavení nebo pracovní adresář založené na konvenci, vytvořit balíček spuštěním `nuget pack` s vaší `.nuspec` souboru, nahraďte `<manifest-name>` s vaší konkrétní název souboru:</span><span class="sxs-lookup"><span data-stu-id="81a60-315">When using an assembly or the convention-based working directory, create a package by running `nuget pack` with your `.nuspec` file, replacing `<manifest-name>` with your specific filename:</span></span>

```
nuget pack <project-name>.nuspec
```

<span data-ttu-id="81a60-316">Při použití projektu sady Visual Studio, spusťte `nuget pack` s soubor projektu, který automaticky načte projektu `.nuspec` souboru a nahradí všechny tokeny v něm pomocí hodnot v souboru projektu:</span><span class="sxs-lookup"><span data-stu-id="81a60-316">When using a Visual Studio project, run `nuget pack` with your project file, which automatically loads the project's `.nuspec` file and replaces any tokens within it using values in the project file:</span></span>

```
nuget pack <project-name>.csproj
```

> [!Note]
> <span data-ttu-id="81a60-317">Přímo pomocí souboru projektu je nezbytné pro token nahrazení, protože projekt je zdrojem hodnoty tokenu.</span><span class="sxs-lookup"><span data-stu-id="81a60-317">Using the project file directly is necessary for token replacement because the project is the source of the token values.</span></span> <span data-ttu-id="81a60-318">Nahrazení tokenu není dojít, pokud používáte `nuget pack` s `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="81a60-318">Token replacement does not happen if you use `nuget pack` with a `.nuspec` file.</span></span>

<span data-ttu-id="81a60-319">Ve všech případech `nuget pack` vyloučí složek, které začínají s dobou, jako například `.git` nebo `.hg`.</span><span class="sxs-lookup"><span data-stu-id="81a60-319">In all cases, `nuget pack` excludes folders that start with a period, such as `.git` or `.hg`.</span></span>

<span data-ttu-id="81a60-320">NuGet označuje, pokud jsou všechny chyby `.nuspec` soubor, který vyžadují opravu, jako je například, že zapomenete změnit zástupné hodnoty v manifestu.</span><span class="sxs-lookup"><span data-stu-id="81a60-320">NuGet indicates if there are any errors in the `.nuspec` file that need correcting, such as forgetting to change placeholder values in the manifest.</span></span>

<span data-ttu-id="81a60-321">Jednou `nuget pack` úspěšné, máte `.nupkg` souborů, které můžete publikovat do Galerie vhodný, jak je popsáno v [publikování balíčku](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="81a60-321">Once `nuget pack` succeeds, you have a `.nupkg` file that you can publish to a suitable gallery as described in [Publishing a Package](../create-packages/publish-a-package.md).</span></span>

> [!Tip]
> <span data-ttu-id="81a60-322">Užitečné způsob, jak zkontrolovat balíček po vytvoření ho otevřít v [balíček Průzkumníka](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) nástroj.</span><span class="sxs-lookup"><span data-stu-id="81a60-322">A helpful way to examine a package after creating it is to open it in the [Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) tool.</span></span> <span data-ttu-id="81a60-323">To vám dává grafické zobrazení obsah balíčku a jeho manifestu.</span><span class="sxs-lookup"><span data-stu-id="81a60-323">This gives you a graphical view of the package contents and its manifest.</span></span> <span data-ttu-id="81a60-324">Můžete také přejmenovat, výsledná `.nupkg` do souboru `.zip` souboru a seznamte se s jeho obsahem přímo.</span><span class="sxs-lookup"><span data-stu-id="81a60-324">You can also rename the resulting `.nupkg` file to a `.zip` file and explore its contents directly.</span></span>

### <a name="additional-options"></a><span data-ttu-id="81a60-325">Další možnosti</span><span class="sxs-lookup"><span data-stu-id="81a60-325">Additional options</span></span>

<span data-ttu-id="81a60-326">Můžete použít různé přepínače příkazového řádku s `nuget pack` vyloučit soubory, přepsat číslo verze v manifestu a změnit do výstupní složky mezi dalších funkcí.</span><span class="sxs-lookup"><span data-stu-id="81a60-326">You can use various command-line switches with `nuget pack` to exclude files, override the version number in the manifest, and change the output folder, among other features.</span></span> <span data-ttu-id="81a60-327">Úplný seznam najdete v článku [pack reference k příkazům](../tools/cli-ref-pack.md).</span><span class="sxs-lookup"><span data-stu-id="81a60-327">For a complete list, refer to the [pack command reference](../tools/cli-ref-pack.md).</span></span>

<span data-ttu-id="81a60-328">Pár jsou běžné u projektů sady Visual Studio jsou následující možnosti:</span><span class="sxs-lookup"><span data-stu-id="81a60-328">The following options are a few that are common with Visual Studio projects:</span></span>

- <span data-ttu-id="81a60-329">**Odkazovaný projekty**: Pokud projekt odkazuje na jiné projekty, můžete přidat odkazované projekty jako součást balíčku, nebo jako závislosti, s použitím `-IncludeReferencedProjects` možnost:</span><span class="sxs-lookup"><span data-stu-id="81a60-329">**Referenced projects**: If the project references other projects, you can add the referenced projects as part of the package, or as dependencies, by using the `-IncludeReferencedProjects` option:</span></span>

    ```
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    <span data-ttu-id="81a60-330">Tento proces zahrnutí je rekurzivní, takže když `MyProject.csproj` odkazy na projekty B a C a tyto projekty odkazovat D, E a F a potom soubory z B, C, D, E a F jsou součástí balíčku.</span><span class="sxs-lookup"><span data-stu-id="81a60-330">This inclusion process is recursive, so if `MyProject.csproj` references projects B and C, and those projects reference D, E, and F, then files from B, C, D, E, and F are included in the package.</span></span>

    <span data-ttu-id="81a60-331">Pokud obsahuje odkazovaný projektu `.nuspec` souboru svůj vlastní, pak NuGet přidá tento Odkazovaný projekt jako závislost místo.</span><span class="sxs-lookup"><span data-stu-id="81a60-331">If a referenced project includes a `.nuspec` file of its own, then NuGet adds that referenced project as a dependency instead.</span></span>  <span data-ttu-id="81a60-332">Budete muset balíčku a publikování tohoto projektu v samostatně.</span><span class="sxs-lookup"><span data-stu-id="81a60-332">You need to package and publish that project separately.</span></span>

- <span data-ttu-id="81a60-333">**Konfigurace sestavení**: ve výchozím nastavení používá NuGet je konfigurace sestavení výchozí nastavená v souboru projektu, obvykle *ladění*.</span><span class="sxs-lookup"><span data-stu-id="81a60-333">**Build configuration**: By default, NuGet uses the default build configuration set in the project file, typically *Debug*.</span></span> <span data-ttu-id="81a60-334">K pack soubory z různých sestavení konfigurace, jako například *verze*, použijte `-properties` možnost s konfigurací:</span><span class="sxs-lookup"><span data-stu-id="81a60-334">To pack files from a different build configuration, such as *Release*, use the `-properties` option with the configuration:</span></span>

    ```
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- <span data-ttu-id="81a60-335">**Symboly**: Chcete-li například symboly, které umožňují příjemcům krokovat kód balíčku v ladicím programu, použijte `-Symbols` možnost:</span><span class="sxs-lookup"><span data-stu-id="81a60-335">**Symbols**: to include symbols that allow consumers to step through your package code in the debugger, use the `-Symbols` option:</span></span>

    ```
    nuget pack MyProject.csproj -symbols
    ```

### <a name="testing-package-installation"></a><span data-ttu-id="81a60-336">Testování instalace balíčku</span><span class="sxs-lookup"><span data-stu-id="81a60-336">Testing package installation</span></span>

<span data-ttu-id="81a60-337">Před publikováním balíček, chcete obvykle testovat proces instalace balíčku do projektu.</span><span class="sxs-lookup"><span data-stu-id="81a60-337">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="81a60-338">Testy, zkontrolujte, zda nutně soubory všechny skončili na jejich správné místech v projektu.</span><span class="sxs-lookup"><span data-stu-id="81a60-338">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="81a60-339">Můžete otestovat instalace ručně v sadě Visual Studio nebo na příkazovém řádku pomocí normální [balíček kroky instalace](../Quickstart/Use-a-Package.md).</span><span class="sxs-lookup"><span data-stu-id="81a60-339">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../Quickstart/Use-a-Package.md).</span></span>

<span data-ttu-id="81a60-340">Pro automatizované testování základní proces je následující:</span><span class="sxs-lookup"><span data-stu-id="81a60-340">For automated testing, the basic process is as follows:</span></span>

1. <span data-ttu-id="81a60-341">Kopírování `.nupkg` soubor do místní složky.</span><span class="sxs-lookup"><span data-stu-id="81a60-341">Copy the `.nupkg` file to a local folder.</span></span>
1. <span data-ttu-id="81a60-342">Přidat složku do vaší zdroje balíčku pomocí `nuget sources -name <name> -source <path>` příkazu (najdete v části [zdroje nuget](../tools/cli-ref-sources.md)).</span><span class="sxs-lookup"><span data-stu-id="81a60-342">Add the folder to your package sources using the `nuget sources -name <name> -source <path>` command (see [nuget sources](../tools/cli-ref-sources.md)).</span></span> <span data-ttu-id="81a60-343">Všimněte si, že budete potřebovat pouze jednou nastavit tento místní zdroj libovolného daného počítače.</span><span class="sxs-lookup"><span data-stu-id="81a60-343">Note that you need only set this local source once on any given computer.</span></span>
1. <span data-ttu-id="81a60-344">Nainstalujte balíček z tohoto zdroje pomocí `nuget install <packageID> -source <name>` kde `<name>` odpovídá názvu zdrojového přidělený `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="81a60-344">Install the package from that source using `nuget install <packageID> -source <name>` where `<name>` matches the name of your source as given to `nuget sources`.</span></span> <span data-ttu-id="81a60-345">Zadání zdrojové zajistí, že balíček je nainstalovat z tohoto zdroje samostatně.</span><span class="sxs-lookup"><span data-stu-id="81a60-345">Specifying the source ensures that the package is installed from that source alone.</span></span>
1. <span data-ttu-id="81a60-346">Zkontrolujte a zkontrolujte, zda jsou soubory správně nainstalovány v systému souborů.</span><span class="sxs-lookup"><span data-stu-id="81a60-346">Examine the file system to check that files are installed correctly.</span></span>

## <a name="next-steps"></a><span data-ttu-id="81a60-347">Další kroky</span><span class="sxs-lookup"><span data-stu-id="81a60-347">Next Steps</span></span>

<span data-ttu-id="81a60-348">Po vytvoření balíčku, který je `.nupkg` souboru, můžete ji publikujete do Galerie zvoleného jak je popsáno na [publikování balíčku](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="81a60-348">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="81a60-349">Můžete také chtít rozšiřují možnosti vašeho balíčku nebo jinak podporovala jiné scénáře, jak je popsáno v následujících tématech:</span><span class="sxs-lookup"><span data-stu-id="81a60-349">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="81a60-350">Správa verzí balíčku</span><span class="sxs-lookup"><span data-stu-id="81a60-350">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="81a60-351">Podpora více cílové rozhraní</span><span class="sxs-lookup"><span data-stu-id="81a60-351">Supporting multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="81a60-352">Transformace zdroje a konfiguračních souborů</span><span class="sxs-lookup"><span data-stu-id="81a60-352">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="81a60-353">Lokalizace</span><span class="sxs-lookup"><span data-stu-id="81a60-353">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="81a60-354">Předběžné verze</span><span class="sxs-lookup"><span data-stu-id="81a60-354">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)

<span data-ttu-id="81a60-355">Nakonec existují další balíčky typy zajímat:</span><span class="sxs-lookup"><span data-stu-id="81a60-355">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="81a60-356">Nativní balíčky</span><span class="sxs-lookup"><span data-stu-id="81a60-356">Native Packages</span></span>](../create-packages/native-packages.md)
- [<span data-ttu-id="81a60-357">Balíčky symbolů</span><span class="sxs-lookup"><span data-stu-id="81a60-357">Symbol Packages</span></span>](../create-packages/symbol-packages.md)
