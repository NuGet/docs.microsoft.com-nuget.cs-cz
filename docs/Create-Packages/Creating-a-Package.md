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
ms.openlocfilehash: 613e3eb9d08a0da96340f32b13c486508fa32439
ms.sourcegitcommit: df21fe770900644d476d51622a999597a6f20ef8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/12/2018
---
# <a name="creating-nuget-packages"></a><span data-ttu-id="87364-104">Vytváření balíčků NuGet</span><span class="sxs-lookup"><span data-stu-id="87364-104">Creating NuGet packages</span></span>

<span data-ttu-id="87364-105">Bez ohledu na jaké vašeho balíčku nebo co code je obsahuje, můžete použít `nuget.exe` do balíčku, které tuto funkci do komponenty, které je možné sdílet s a používat libovolný počet dalších vývojáři.</span><span class="sxs-lookup"><span data-stu-id="87364-105">No matter what your package does or what code it contains, you use `nuget.exe` to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="87364-106">Chcete-li nainstalovat `nuget.exe`, najdete v části [nainstalovat rozhraní příkazového řádku NuGet](../install-nuget-client-tools.md#nugetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="87364-106">To install `nuget.exe`, see [Install NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli).</span></span> <span data-ttu-id="87364-107">Všimněte si, že Visual Studio automaticky nezahrnuje `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="87364-107">Note that Visual Studio does not automatically include `nuget.exe`.</span></span>

<span data-ttu-id="87364-108">Technicky platí, že balíček NuGet je právě soubor ZIP, který byl přejmenován s `.nupkg` rozšíření, jejichž obsah odpovídají určité konvence.</span><span class="sxs-lookup"><span data-stu-id="87364-108">Technically speaking, a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension and whose contents match certain conventions.</span></span> <span data-ttu-id="87364-109">Toto téma popisuje podrobný proces vytvoření balíčku, který splňuje tyto konvence.</span><span class="sxs-lookup"><span data-stu-id="87364-109">This topic describes the detailed process of creating a package that meets those conventions.</span></span> <span data-ttu-id="87364-110">Podrobný návod, najdete v části [rychlý start: vytvoření a publikování balíčku](../quickstart/create-and-publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="87364-110">For a focused walkthrough, refer to [Quickstart: create and publish a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="87364-111">Balení začíná zkompilovaný kód (sestavení), symboly a další soubory, které chcete doručit jako balíček (viz [přehled a pracovní postup](overview-and-workflow.md)).</span><span class="sxs-lookup"><span data-stu-id="87364-111">Packaging begins with the compiled code (assemblies), symbols, and/or other files that you want to deliver as a package (see [Overview and workflow](overview-and-workflow.md)).</span></span> <span data-ttu-id="87364-112">Tento proces je nezávislé na kompilování nebo jinak generování souborů, které patří do balíčku, i když můžete použít kreslení z informací v souboru projektu pro synchronizaci kompilované sestavení a balíčky.</span><span class="sxs-lookup"><span data-stu-id="87364-112">This process is independent from compiling or otherwise generating the files that go into the package, although you can use draw from information in a project file to keep the compiled assemblies and packages in sync.</span></span>

> [!Note]
> <span data-ttu-id="87364-113">Toto téma se vztahuje na typy projektů než projektů .NET Core pomocí Visual Studio 2017 a NuGet 4.0 +.</span><span class="sxs-lookup"><span data-stu-id="87364-113">This topic applies to project types other than .NET Core projects using Visual Studio 2017 and NuGet 4.0+.</span></span> <span data-ttu-id="87364-114">V těchto projektech .NET Core NuGet používá informace v souboru projektu přímo.</span><span class="sxs-lookup"><span data-stu-id="87364-114">In those .NET Core projects, NuGet uses information in the project file directly.</span></span> <span data-ttu-id="87364-115">Podrobnosti najdete v tématu [vytvořit .NET standardní balíčky s Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) a [NuGet pack a obnovit jako cíle MSBuild](../reference/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="87364-115">For details, see [Create .NET Standard Packages with Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) and [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).</span></span>

## <a name="deciding-which-assemblies-to-package"></a><span data-ttu-id="87364-116">Rozhodnutí, která sestavení do balíčku</span><span class="sxs-lookup"><span data-stu-id="87364-116">Deciding which assemblies to package</span></span>

<span data-ttu-id="87364-117">Většina pro obecné účely balíčky obsahují jeden nebo více sestavení, které ostatní vývojáři mohou použít ve svých vlastních projektů.</span><span class="sxs-lookup"><span data-stu-id="87364-117">Most general-purpose packages contain one or more assemblies that other developers can use in their own projects.</span></span>

- <span data-ttu-id="87364-118">Obecně platí je nejlepší mít jedno sestavení na balíček NuGet předpokladu, že každé sestavení je nezávisle užitečné.</span><span class="sxs-lookup"><span data-stu-id="87364-118">In general, it's best to have one assembly per NuGet package, provided that each assembly is independently useful.</span></span> <span data-ttu-id="87364-119">Pokud máte například `Utilities.dll` , závisí na `Parser.dll`, a `Parser.dll` je užitečné sama o sobě, a pak vytvořte jeden balíček pro každý.</span><span class="sxs-lookup"><span data-stu-id="87364-119">For example, if you have a `Utilities.dll` that depends on `Parser.dll`, and `Parser.dll` is useful on its own, then create one package for each.</span></span> <span data-ttu-id="87364-120">Díky tomu mohou vývojáři použít `Parser.dll` nezávisle na `Utilities.dll`.</span><span class="sxs-lookup"><span data-stu-id="87364-120">Doing so allows developers to use `Parser.dll` independently of `Utilities.dll`.</span></span>

- <span data-ttu-id="87364-121">Pokud vaše knihovna se skládá z více sestavení, které nejsou nezávisle užitečné, je vhodná pro jejich zkombinovat do jednoho balíčku.</span><span class="sxs-lookup"><span data-stu-id="87364-121">If your library is composed of multiple assemblies that aren't independently useful, then it's fine to combine them into one package.</span></span> <span data-ttu-id="87364-122">Použijeme předchozí příklad, pokud `Parser.dll` obsahuje kód, který se používá pouze systémem `Utilities.dll`, pak je v pořádku zachovat `Parser.dll` ve stejném balíčku.</span><span class="sxs-lookup"><span data-stu-id="87364-122">Using the previous example, if `Parser.dll` contains code that's used only by `Utilities.dll`, then it's fine to keep `Parser.dll` in the same package.</span></span>

- <span data-ttu-id="87364-123">Podobně pokud `Utilities.dll` závisí na `Utilities.resources.dll`, je-li znovu tento není užitečné sama o sobě, pak přesuňte i ve stejném balíčku.</span><span class="sxs-lookup"><span data-stu-id="87364-123">Similarly, if `Utilities.dll` depends on `Utilities.resources.dll`, where again the latter is not useful on its own, then put both in the same package.</span></span>

<span data-ttu-id="87364-124">Prostředky jsou ve skutečnosti ve speciálním případě.</span><span class="sxs-lookup"><span data-stu-id="87364-124">Resources are, in fact, a special case.</span></span> <span data-ttu-id="87364-125">Při instalaci balíčku do projektu NuGet automaticky přidá odkazy na sestavení pro knihovny DLL balíčku, *s výjimkou* ty, které jsou s názvem `.resources.dll` vzhledem k tomu, že se předpokládá, že lokalizované satelitní sestavení (viz [ Vytvoření lokalizovaných balíčků](creating-localized-packages.md)).</span><span class="sxs-lookup"><span data-stu-id="87364-125">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies (see [Creating localized packages](creating-localized-packages.md)).</span></span> <span data-ttu-id="87364-126">Z tohoto důvodu vyhýbat se používání `.resources.dll` pro soubory, které jinak obsahují nezbytné balíček kódu.</span><span class="sxs-lookup"><span data-stu-id="87364-126">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="87364-127">Pokud vaše knihovna obsahuje sestavení zprostředkovatele komunikace s objekty COM, postupujte podle dalších pokynů v [vytváření balíčků s sestavení vzájemné spolupráce COM](#authoring-packages-with-com-interop-assemblies).</span><span class="sxs-lookup"><span data-stu-id="87364-127">If your library contains COM interop assemblies, follow additional the guidelines in [Authoring packages with COM interop assemblies](#authoring-packages-with-com-interop-assemblies).</span></span>

## <a name="the-role-and-structure-of-the-nuspec-file"></a><span data-ttu-id="87364-128">Role a struktura souboru s příponou .nuspec</span><span class="sxs-lookup"><span data-stu-id="87364-128">The role and structure of the .nuspec file</span></span>

<span data-ttu-id="87364-129">Jakmile již víte, jaké soubory, které chcete balíček a dalším krokem je vytvoření manifestu balíčku v `.nuspec` souboru XML.</span><span class="sxs-lookup"><span data-stu-id="87364-129">Once you know what files you want to package, the next step is creating a package manifest in a `.nuspec` XML file.</span></span>

<span data-ttu-id="87364-130">V manifestu:</span><span class="sxs-lookup"><span data-stu-id="87364-130">The manifest:</span></span>

1. <span data-ttu-id="87364-131">Popisuje obsah balíčku a je sám součástí balíčku.</span><span class="sxs-lookup"><span data-stu-id="87364-131">Describes the package's contents and is itself included in the package.</span></span>
1. <span data-ttu-id="87364-132">Jednotky vytvoření balíčku a dá pokyn NuGet k instalaci balíčku do projektu.</span><span class="sxs-lookup"><span data-stu-id="87364-132">Drives both the creation of the package and instructs NuGet on how to install the package into a project.</span></span> <span data-ttu-id="87364-133">Například manifest identifikuje další závislosti balíčků tak, aby NuGet můžete také nainstalovat těchto závislostí při instalaci hlavní balíčku.</span><span class="sxs-lookup"><span data-stu-id="87364-133">For example, the manifest identifies other package dependencies such that NuGet can also install those dependencies when the main package is installed.</span></span>
1. <span data-ttu-id="87364-134">Požadované a volitelné vlastnosti obsahuje, jak je popsáno níže.</span><span class="sxs-lookup"><span data-stu-id="87364-134">Contains both required and optional properties as described below.</span></span> <span data-ttu-id="87364-135">Přesné podrobnosti, včetně dalších vlastností, zde nejsou uvedeny najdete v tématu [příponou .nuspec odkaz](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="87364-135">For exact details, including other properties not mentioned here, see  the [.nuspec reference](../reference/nuspec.md).</span></span>

<span data-ttu-id="87364-136">Požadované vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="87364-136">Required properties:</span></span>

- <span data-ttu-id="87364-137">Identifikátor balíčku, který musí být jedinečný v rámci galerie, který je hostitelem balíčku.</span><span class="sxs-lookup"><span data-stu-id="87364-137">The package identifier, which must be unique across the gallery that hosts the package.</span></span>
- <span data-ttu-id="87364-138">Konkrétní verzi číslo ve tvaru *Major.Minor.Patch [-přípona]* kde *-přípona* identifikuje [předprodejní verze](prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="87364-138">A specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md)</span></span>
- <span data-ttu-id="87364-139">Název balíčku, jako by měl se v hostitelském (např. nuget.org)</span><span class="sxs-lookup"><span data-stu-id="87364-139">The package title as it should appears on the host (like nuget.org)</span></span>
- <span data-ttu-id="87364-140">Informace o vytváření a vlastníka.</span><span class="sxs-lookup"><span data-stu-id="87364-140">Author and owner information.</span></span>
- <span data-ttu-id="87364-141">Dlouhý popis balíčku.</span><span class="sxs-lookup"><span data-stu-id="87364-141">A long description of the package.</span></span>

<span data-ttu-id="87364-142">Běžné volitelné vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="87364-142">Common optional properties:</span></span>

- <span data-ttu-id="87364-143">Zpráva k vydání verze</span><span class="sxs-lookup"><span data-stu-id="87364-143">Release notes</span></span>
- <span data-ttu-id="87364-144">Informace o autorských právech</span><span class="sxs-lookup"><span data-stu-id="87364-144">Copyright information</span></span>
- <span data-ttu-id="87364-145">Krátký popis [uživatelského rozhraní Správce balíčků v sadě Visual Studio](../tools/package-manager-ui.md)</span><span class="sxs-lookup"><span data-stu-id="87364-145">A short description for the [Package Manager UI in Visual Studio](../tools/package-manager-ui.md)</span></span>
- <span data-ttu-id="87364-146">ID národního prostředí</span><span class="sxs-lookup"><span data-stu-id="87364-146">A locale ID</span></span>
- <span data-ttu-id="87364-147">Domovská stránka a adresy URL licence</span><span class="sxs-lookup"><span data-stu-id="87364-147">Home page and license URLs</span></span>
- <span data-ttu-id="87364-148">Adresu URL ikony</span><span class="sxs-lookup"><span data-stu-id="87364-148">An icon URL</span></span>
- <span data-ttu-id="87364-149">Seznam závislosti a odkazy</span><span class="sxs-lookup"><span data-stu-id="87364-149">Lists of dependencies and references</span></span>
- <span data-ttu-id="87364-150">Značky, které pomáhají při hledání Galerie</span><span class="sxs-lookup"><span data-stu-id="87364-150">Tags that assist in gallery searches</span></span>

<span data-ttu-id="87364-151">Toto je typické (ale fiktivní) `.nuspec` soubor s komentáři popisující vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="87364-151">The following is a typical (but fictitious) `.nuspec` file, with comments describing the properties:</span></span>

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

<span data-ttu-id="87364-152">Podrobnosti o deklarace závislosti a zadání čísla verzí, naleznete v části [Správa verzí balíčku](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="87364-152">For details on declaring dependencies and specifying version numbers, see [Package versioning](../reference/package-versioning.md).</span></span> <span data-ttu-id="87364-153">Je také možné do prostor prostředky z závislosti přímo v balíčku pomocí `include` a `exclude` atributy na `dependency` elementu.</span><span class="sxs-lookup"><span data-stu-id="87364-153">It is also possible to surface assets from dependencies directly in the package by using the `include` and `exclude` attributes on the `dependency` element.</span></span> <span data-ttu-id="87364-154">V tématu [příponou .nuspec odkaz - závislosti](../reference/nuspec.md#dependencies).</span><span class="sxs-lookup"><span data-stu-id="87364-154">See [.nuspec Reference - Dependencies](../reference/nuspec.md#dependencies).</span></span>

<span data-ttu-id="87364-155">Manifest je zahrnutý v balíčku vytvořit z něj, proto vyhledejte libovolný počet Další příklady tak, že prověří existující balíčky.</span><span class="sxs-lookup"><span data-stu-id="87364-155">Because the manifest is included in the package created from it, you can find any number of additional examples by examining existing packages.</span></span> <span data-ttu-id="87364-156">Je dobré zdroj mezipaměti globální balíčku na počítači, umístění, které vrátí následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="87364-156">A good source is the global package cache on your machine, the location of which is returned by the following command:</span></span>

```cli
nuget locals -list global-packages
```

<span data-ttu-id="87364-157">Přejděte do jakéhokoli *package\version* složce, kopie `.nupkg` do souboru `.zip` souboru a pak otevřete, `.zip` soubor a zkontrolujte `.nuspec` v něm.</span><span class="sxs-lookup"><span data-stu-id="87364-157">Go into any *package\version* folder, copy the `.nupkg` file to a `.zip` file, then open that `.zip` file and examine the `.nuspec` within it.</span></span>

> [!Note]
> <span data-ttu-id="87364-158">Při vytváření `.nuspec` z projektu sady Visual Studio manifest obsahuje tokenů, které jsou nahrazeny informace z projektu, když je balíček vytvořen.</span><span class="sxs-lookup"><span data-stu-id="87364-158">When creating a `.nuspec` from a Visual Studio project, the manifest contains tokens that are replaced with information from the project when the package is built.</span></span> <span data-ttu-id="87364-159">V tématu [vytváření příponou .nuspec z projektu sady Visual Studio](#from-a-visual-studio-project).</span><span class="sxs-lookup"><span data-stu-id="87364-159">See [Creating the .nuspec from a Visual Studio project](#from-a-visual-studio-project).</span></span>

## <a name="creating-the-nuspec-file"></a><span data-ttu-id="87364-160">Vytvoření souboru s příponou .nuspec</span><span class="sxs-lookup"><span data-stu-id="87364-160">Creating the .nuspec file</span></span>

<span data-ttu-id="87364-161">Vytváření dokončení manifestu obvykle začíná základní `.nuspec` souboru vygenerovaného prostřednictvím jednoho z následujících metod:</span><span class="sxs-lookup"><span data-stu-id="87364-161">Creating a complete manifest typically begins with a basic `.nuspec` file generated through one of the following methods:</span></span>

- [<span data-ttu-id="87364-162">Založené na konvenci pracovní adresář</span><span class="sxs-lookup"><span data-stu-id="87364-162">A convention-based working directory</span></span>](#from-a-convention-based-working-directory)
- [<span data-ttu-id="87364-163">Sestavení knihovny DLL</span><span class="sxs-lookup"><span data-stu-id="87364-163">An assembly DLL</span></span>](#from-an-assembly-dll)
- [<span data-ttu-id="87364-164">A Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="87364-164">A Visual Studio project</span></span>](#from-a-visual-studio-project)    
- [<span data-ttu-id="87364-165">Nový soubor s výchozími hodnotami</span><span class="sxs-lookup"><span data-stu-id="87364-165">New file with default values</span></span>](#new-file-with-default-values)

<span data-ttu-id="87364-166">Pak upravíte soubor ručně tak, aby popisuje přesný obsah, který chcete v posledním balíčku.</span><span class="sxs-lookup"><span data-stu-id="87364-166">You then edit the file by hand so that it describes the exact content you want in the final package.</span></span>

> [!Important]
> <span data-ttu-id="87364-167">Generované `.nuspec` soubory obsahují zástupné symboly, které je třeba upravit před vytvořením balíčku s `nuget pack` příkaz.</span><span class="sxs-lookup"><span data-stu-id="87364-167">Generated `.nuspec` files contain placeholders that must be modified before creating the package with the `nuget pack` command.</span></span> <span data-ttu-id="87364-168">Příkaz selže, pokud `.nuspec` obsahuje zástupné symboly.</span><span class="sxs-lookup"><span data-stu-id="87364-168">That command fails if the `.nuspec` contains any placeholders.</span></span>

### <a name="from-a-convention-based-working-directory"></a><span data-ttu-id="87364-169">Z založené na konvenci pracovní adresář</span><span class="sxs-lookup"><span data-stu-id="87364-169">From a convention-based working directory</span></span>

<span data-ttu-id="87364-170">Protože balíčku NuGet je právě soubor ZIP, který byl přejmenován s `.nupkg` rozšíření, jeho často nejjednodušší vytvořit strukturu složek, které chcete v systému souborů, pak vytvořte `.nuspec` soubor přímo z této struktury.</span><span class="sxs-lookup"><span data-stu-id="87364-170">Because a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension, its often easiest to create the folder structure you want on the file system, then create the `.nuspec` file directly from that structure.</span></span> <span data-ttu-id="87364-171">`nuget pack` Příkaz automaticky přidá všechny soubory v této struktuře složek (s výjimkou všechny složky, které začínají `.`, umožňuje zachovat soubory soukromých ve stejné struktuře).</span><span class="sxs-lookup"><span data-stu-id="87364-171">The `nuget pack` command then automatically adds all files in that folder structure (excluding any folders that begin with `.`, allowing you keep private files in the same structure).</span></span>

<span data-ttu-id="87364-172">Výhoda tohoto přístupu je, že nemusíte v manifestu zadejte soubory, které chcete zahrnout do balíčku (jak je popsáno dále v tomto tématu).</span><span class="sxs-lookup"><span data-stu-id="87364-172">The advantage to this approach is that you don't need to specify in the manifest which files you want to include in the package (as explained later in this topic).</span></span> <span data-ttu-id="87364-173">Jednoduše může mít vaše procesu sestavení vytvořit strukturu přesnou složku, která přejde do balíčku a snadno můžete zahrnout další soubory, které nemusí být součástí projektu jinak:</span><span class="sxs-lookup"><span data-stu-id="87364-173">You can simply have your build process produce the exact folder structure that goes into the package, and you can easily include other files that might not be part of a project otherwise:</span></span>

- <span data-ttu-id="87364-174">Obsah a zdrojový kód, který by měl být vloženy do cílový projekt.</span><span class="sxs-lookup"><span data-stu-id="87364-174">Content and source code that should be injected into the target project.</span></span>
- <span data-ttu-id="87364-175">Skripty prostředí PowerShell (balíčky použité v NuGet 2.x může zahrnovat taky skriptů instalace, což není podporováno v NuGet 3.x a novější).</span><span class="sxs-lookup"><span data-stu-id="87364-175">PowerShell scripts (packages used in NuGet 2.x can include installation scripts as well, which is not supported in NuGet 3.x and later).</span></span>
- <span data-ttu-id="87364-176">Transformace na existující konfiguraci a zdrojové soubory kódu v projektu.</span><span class="sxs-lookup"><span data-stu-id="87364-176">Transformations to existing configuration and source code files in a project.</span></span>

<span data-ttu-id="87364-177">Konvence složky jsou následující:</span><span class="sxs-lookup"><span data-stu-id="87364-177">The folder conventions are as follows:</span></span>

| <span data-ttu-id="87364-178">Folder</span><span class="sxs-lookup"><span data-stu-id="87364-178">Folder</span></span> | <span data-ttu-id="87364-179">Popis</span><span class="sxs-lookup"><span data-stu-id="87364-179">Description</span></span> | <span data-ttu-id="87364-180">Akce při instalaci balíčku</span><span class="sxs-lookup"><span data-stu-id="87364-180">Action upon package install</span></span> |
| --- | --- | --- |
| <span data-ttu-id="87364-181">(uživatel root)</span><span class="sxs-lookup"><span data-stu-id="87364-181">(root)</span></span> | <span data-ttu-id="87364-182">Umístění souboru readme.txt</span><span class="sxs-lookup"><span data-stu-id="87364-182">Location for readme.txt</span></span> | <span data-ttu-id="87364-183">Při instalaci balíčku Visual Studio zobrazí souboru readme.txt v kořenu balíčku.</span><span class="sxs-lookup"><span data-stu-id="87364-183">Visual Studio displays a readme.txt file in the package root when the package is installed.</span></span> |
| <span data-ttu-id="87364-184">lib / {tfm}</span><span class="sxs-lookup"><span data-stu-id="87364-184">lib/{tfm}</span></span> | <span data-ttu-id="87364-185">Sestavení (`.dll`), dokumentace (`.xml`) a symbol (`.pdb`) soubory pro danou cílový Framework Přezdívka (TFM)</span><span class="sxs-lookup"><span data-stu-id="87364-185">Assembly (`.dll`), documentation (`.xml`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="87364-186">Sestavení jsou přidány jako odkazy; `.xml` a `.pdb` zkopírovány do složky projektu.</span><span class="sxs-lookup"><span data-stu-id="87364-186">Assemblies are added as references; `.xml` and `.pdb` copied into project folders.</span></span> <span data-ttu-id="87364-187">V tématu [podpora více cílové rozhraní](supporting-multiple-target-frameworks.md) pro vytvoření framework specifické pro cílové podsložky.</span><span class="sxs-lookup"><span data-stu-id="87364-187">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md) for creating framework target-specific sub-folders.</span></span> |
| <span data-ttu-id="87364-188">Moduly runtime</span><span class="sxs-lookup"><span data-stu-id="87364-188">runtimes</span></span> | <span data-ttu-id="87364-189">Architektura konkrétní sestavení (`.dll`), symbol (`.pdb`) a nativní prostředků (`.pri`) souborů</span><span class="sxs-lookup"><span data-stu-id="87364-189">Architecture-specific assembly (`.dll`), symbol (`.pdb`), and native resource (`.pri`) files</span></span> | <span data-ttu-id="87364-190">Sestavení jsou přidány jako odkazy; ostatní soubory se zkopírují do složky projektu.</span><span class="sxs-lookup"><span data-stu-id="87364-190">Assemblies are added as references; other files are copied into project folders.</span></span> <span data-ttu-id="87364-191">V tématu [podpora více cílové rozhraní](supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="87364-191">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md).</span></span> |
| <span data-ttu-id="87364-192">obsah</span><span class="sxs-lookup"><span data-stu-id="87364-192">content</span></span> | <span data-ttu-id="87364-193">Různé soubory</span><span class="sxs-lookup"><span data-stu-id="87364-193">Arbitrary files</span></span> | <span data-ttu-id="87364-194">Obsah je zkopírován do kořenového adresáře projektu.</span><span class="sxs-lookup"><span data-stu-id="87364-194">Contents are copied to the project root.</span></span> <span data-ttu-id="87364-195">Představte si, že **obsah** složky jako kořen cílová aplikace, který nakonec využívá balíčku.</span><span class="sxs-lookup"><span data-stu-id="87364-195">Think of the **content** folder as the root of the target application that ultimately consumes the package.</span></span> <span data-ttu-id="87364-196">Do mají balíček přidat bitovou kopii do aplikace */image* složku, umístěte ji do balíčku *obsah nebo obrázky* složky.</span><span class="sxs-lookup"><span data-stu-id="87364-196">To have the package add an image in the application's */images* folder, place it in the package's *content/images* folder.</span></span> |
| <span data-ttu-id="87364-197">sestavení</span><span class="sxs-lookup"><span data-stu-id="87364-197">build</span></span> | <span data-ttu-id="87364-198">MSBuild `.targets` a `.props` soubory</span><span class="sxs-lookup"><span data-stu-id="87364-198">MSBuild `.targets` and `.props` files</span></span> | <span data-ttu-id="87364-199">Automaticky vloží do souboru projektu nebo `project.lock.json` (NuGet 3.x+).</span><span class="sxs-lookup"><span data-stu-id="87364-199">Automatically inserted into the project file or `project.lock.json` (NuGet 3.x+).</span></span> |
| <span data-ttu-id="87364-200">nástroje</span><span class="sxs-lookup"><span data-stu-id="87364-200">tools</span></span> | <span data-ttu-id="87364-201">Skripty prostředí PowerShell a programy, které jsou přístupné z konzoly Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="87364-201">Powershell scripts and programs accessible from the Package Manager Console</span></span> | <span data-ttu-id="87364-202">`tools` Se přidá složka `PATH` proměnnou prostředí pro konzolu Správce balíčků (konkrétně *není* k `PATH` jako sada pro MSBuild při sestavování projektu).</span><span class="sxs-lookup"><span data-stu-id="87364-202">The `tools` folder is added to the `PATH` environment variable for the Package Manager Console only (Specifically, *not* to the `PATH` as set for MSBuild when building the project).</span></span> |

<span data-ttu-id="87364-203">Protože struktury složky může obsahovat libovolný počet sestavení pro libovolný počet cílové rozhraní, tato metoda je nutné při vytváření balíčků, které podporují více rozhraní</span><span class="sxs-lookup"><span data-stu-id="87364-203">Because your folder structure can contain any number of assemblies for any number of target frameworks, this method is necessary when creating packages that support multiple frameworks</span></span> 

<span data-ttu-id="87364-204">V každém případě až budete mít struktuře požadované složky na místě, spusťte následující příkaz v této složce vytvořit `.nuspec` souboru:</span><span class="sxs-lookup"><span data-stu-id="87364-204">In any case, once you have the desired folder structure in place, run the following command in that folder to create the `.nuspec` file:</span></span>

```cli
nuget spec
```

<span data-ttu-id="87364-205">Znovu vygenerovaný `.nuspec` neobsahuje žádné explicitní odkazy na soubory v této struktuře.</span><span class="sxs-lookup"><span data-stu-id="87364-205">Again, the generated `.nuspec` contains no explicit references to files in the folder structure.</span></span> <span data-ttu-id="87364-206">NuGet automaticky zahrne všechny soubory, když je balíček vytvořen.</span><span class="sxs-lookup"><span data-stu-id="87364-206">NuGet automatically includes all files when the package is created.</span></span> <span data-ttu-id="87364-207">Stále je třeba upravit zástupné hodnoty v dalších částech tohoto manifest, ale.</span><span class="sxs-lookup"><span data-stu-id="87364-207">You still need to edit placeholder values in other parts of the manifest, however.</span></span>

### <a name="from-an-assembly-dll"></a><span data-ttu-id="87364-208">Ze sestavení knihoven DLL</span><span class="sxs-lookup"><span data-stu-id="87364-208">From an assembly DLL</span></span>

<span data-ttu-id="87364-209">V případě jednoduchého vytváření balíčku ze sestavení může generovat `.nuspec` souboru z metadat v sestavení pomocí následujícího příkazu:</span><span class="sxs-lookup"><span data-stu-id="87364-209">In the simple case of creating a package from an assembly, you can generate a `.nuspec` file from the metadata in the assembly using the following command:</span></span>

```cli
nuget spec <assembly-name>.dll
```

<span data-ttu-id="87364-210">Pomocí tohoto formuláře nahradí konkrétní hodnoty od sestavení, několik zástupné symboly v manifestu.</span><span class="sxs-lookup"><span data-stu-id="87364-210">Using this form replaces a few placeholders in the manifest with specific values from the assembly.</span></span> <span data-ttu-id="87364-211">Například `<id>` je nastavena na název sestavení a `<version>` je nastaven na verzi sestavení.</span><span class="sxs-lookup"><span data-stu-id="87364-211">For example, the `<id>` property is set to the assembly name, and `<version>` is set to the assembly version.</span></span> <span data-ttu-id="87364-212">Ostatní vlastnosti v manifestu, ale nemáte mít odpovídající hodnoty v sestavení a stále proto obsahují zástupné symboly.</span><span class="sxs-lookup"><span data-stu-id="87364-212">Other properties in the manifest, however, don't have matching values in the assembly and thus still contain placeholders.</span></span>

### <a name="from-a-visual-studio-project"></a><span data-ttu-id="87364-213">Z projektu sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="87364-213">From a Visual Studio project</span></span>

<span data-ttu-id="87364-214">Vytváření `.nuspec` z `.csproj` nebo `.vbproj` souboru je vhodné, protože jiné balíčky, které byly nainstalovány do těchto projektu se automaticky odkazuje jako závislosti.</span><span class="sxs-lookup"><span data-stu-id="87364-214">Creating a `.nuspec` from a `.csproj` or `.vbproj` file is convenient because other packages that have been installed into those project are automatically referenced as dependencies.</span></span> <span data-ttu-id="87364-215">Ve stejné složce jako soubor projektu jednoduše použijte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="87364-215">Simply use the following command in the same folder as the project file:</span></span>

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

<span data-ttu-id="87364-216">Výsledná `<project-name>.nuspec` soubor obsahuje *tokeny* , se nahrazují během balení hodnoty z projektu, včetně odkazů na další balíčky, které již jsou nainstalovány.</span><span class="sxs-lookup"><span data-stu-id="87364-216">The resulting `<project-name>.nuspec` file contains *tokens* that are replaced at packaging time with values from the project, including references to any other packages that have already been installed.</span></span>

<span data-ttu-id="87364-217">Token je oddělená `$` symboly na obou stranách vlastnosti projektu.</span><span class="sxs-lookup"><span data-stu-id="87364-217">A token is delimited by `$` symbols on both sides of the project property.</span></span> <span data-ttu-id="87364-218">Například `<id>` hodnota v manifestu vygenerované v tomto způsobem obvykle vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="87364-218">For example, the `<id>` value in a manifest generated in this way typically appears as follows:</span></span>

```xml
<id>$id$</id>
```

<span data-ttu-id="87364-219">Tento token nahrazen `AssemblyName` hodnotu ze souboru projektu v balení čas.</span><span class="sxs-lookup"><span data-stu-id="87364-219">This token is replaced with the `AssemblyName` value from the project file at packing time.</span></span> <span data-ttu-id="87364-220">Pro přesné mapování projektu hodnot na `.nuspec` tokeny, najdete v článku [odkazovat nahrazení tokeny](../reference/nuspec.md#replacement-tokens).</span><span class="sxs-lookup"><span data-stu-id="87364-220">For the exact mapping of project values to `.nuspec` tokens, see the [Replacement Tokens reference](../reference/nuspec.md#replacement-tokens).</span></span>

<span data-ttu-id="87364-221">Tokeny můžete snížit z museli klíčové hodnoty jako číslo verze v aktualizovat `.nuspec` jako aktualizace projektu.</span><span class="sxs-lookup"><span data-stu-id="87364-221">Tokens relieve you from needing to update crucial values like the version number in the `.nuspec` as you update the project.</span></span> <span data-ttu-id="87364-222">(Můžete vždy nahradit tokeny literálových hodnot v případě potřeby).</span><span class="sxs-lookup"><span data-stu-id="87364-222">(You can always replace the tokens with literal values, if desired).</span></span> 

<span data-ttu-id="87364-223">Všimněte si, že existuje několik další balení možností při práci z projektu sady Visual Studio, jak je popsáno v [systémem nuget aktualizací Service pack ke generování souboru .nupkg v podadresáři](#running-nuget-pack-to-generate-the-nupkg-file) později.</span><span class="sxs-lookup"><span data-stu-id="87364-223">Note that there are several additional packaging options available when working from a Visual Studio project, as described in [Running nuget pack to generate the .nupkg file](#running-nuget-pack-to-generate-the-nupkg-file) later on.</span></span>

#### <a name="solution-level-packages"></a><span data-ttu-id="87364-224">Balíčky úrovni řešení</span><span class="sxs-lookup"><span data-stu-id="87364-224">Solution-level packages</span></span>

<span data-ttu-id="87364-225">*NuGet pouze 2.x. Není k dispozici v NuGet 3.0 +.*</span><span class="sxs-lookup"><span data-stu-id="87364-225">*NuGet 2.x only. Not available in NuGet 3.0+.*</span></span>

<span data-ttu-id="87364-226">NuGet 2.x podporované představu o úrovni řešení balíček, který nainstaluje nástroje nebo další příkazy pro konzolu Správce balíčků (obsah `tools` složky), ale nemá přidejte odkazy na obsah, nebo vytvořit vlastní nastavení na všechny projekty v řešení.</span><span class="sxs-lookup"><span data-stu-id="87364-226">NuGet 2.x supported the notion of a solution-level package that installs tools or additional commands for the Package Manager Console (the contents of the `tools` folder), but does not add references, content, or build customizations to any projects in the solution.</span></span> <span data-ttu-id="87364-227">Tyto balíčky obsahovat žádné soubory v jeho přímo `lib`, `content`, nebo `build` složek a jeden z jejich závislých mít soubory v jejich odpovídajících `lib`, `content`, nebo `build` složek.</span><span class="sxs-lookup"><span data-stu-id="87364-227">Such packages contain no files in its direct `lib`, `content`, or `build` folders, and none of its dependencies have files in their respective `lib`, `content`, or `build` folders.</span></span>

<span data-ttu-id="87364-228">Sleduje NuGet nainstalované balíky úrovni řešení v `packages.config` v soubor `.nuget` složky, nikoli projektu `packages.config` souboru.</span><span class="sxs-lookup"><span data-stu-id="87364-228">NuGet tracks installed solution-level packages in a `packages.config` file in the `.nuget` folder, rather than the project's `packages.config` file.</span></span>

### <a name="new-file-with-default-values"></a><span data-ttu-id="87364-229">Nový soubor s výchozími hodnotami</span><span class="sxs-lookup"><span data-stu-id="87364-229">New file with default values</span></span>

<span data-ttu-id="87364-230">Následující příkaz vytvoří výchozí manifest se zástupnými symboly, což zajistí, že začínáte s strukturu správný soubor:</span><span class="sxs-lookup"><span data-stu-id="87364-230">The following command creates a default manifest with placeholders, which ensures you start with the proper file structure:</span></span>

```cli
nuget spec [<package-name>]
```

<span data-ttu-id="87364-231">Pokud vynecháte \<název balíčku\>, bude výsledný soubor je `Package.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="87364-231">If you omit \<package-name\>, the resulting file is `Package.nuspec`.</span></span> <span data-ttu-id="87364-232">Pokud je třeba zadat název `Contoso.Utility.UsefulStuff`, je soubor `Contoso.Utility.UsefulStuff.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="87364-232">If you provide a name such as `Contoso.Utility.UsefulStuff`, the file is `Contoso.Utility.UsefulStuff.nuspec`.</span></span>

<span data-ttu-id="87364-233">Výsledná `.nuspec` obsahuje zástupné symboly pro hodnot, jako `projectUrl`.</span><span class="sxs-lookup"><span data-stu-id="87364-233">The resulting `.nuspec` contains placeholders for values like the `projectUrl`.</span></span> <span data-ttu-id="87364-234">Nezapomeňte upravit soubor než jej použijete k vytvoření konečné `.nupkg` souboru.</span><span class="sxs-lookup"><span data-stu-id="87364-234">Be sure to edit the file before using it to create the final `.nupkg` file.</span></span>

## <a name="choosing-a-unique-package-identifier-and-setting-the-version-number"></a><span data-ttu-id="87364-235">Výběr balíčku jedinečný identifikátor a nastavení číslo verze</span><span class="sxs-lookup"><span data-stu-id="87364-235">Choosing a unique package identifier and setting the version number</span></span>

<span data-ttu-id="87364-236">Identifikátor balíčku (`<id>` element) a číslo verze (`<version>` element) jsou dvě nejdůležitější hodnoty v manifestu, protože jednoznačně identifikují přesný kód, který je součástí balíčku.</span><span class="sxs-lookup"><span data-stu-id="87364-236">The package identifier (`<id>` element) and the version number (`<version>` element) are the two most important values in the manifest because they uniquely identify the exact code that's contained in the package.</span></span>

<span data-ttu-id="87364-237">**Osvědčené postupy pro identifikátor balíčku:**</span><span class="sxs-lookup"><span data-stu-id="87364-237">**Best practices for the package identifier:**</span></span>

- <span data-ttu-id="87364-238">**Jedinečnost**: identifikátor musí být jedinečný v rámci nuget.org nebo jakoukoli Galerie hostitelem balíčku.</span><span class="sxs-lookup"><span data-stu-id="87364-238">**Uniqueness**: The identifier must be unique across nuget.org or whatever gallery hosts the package.</span></span> <span data-ttu-id="87364-239">Než se rozhodnete, že na identifikátor, vyhledejte galerii použít ke kontrole, pokud název je již používán.</span><span class="sxs-lookup"><span data-stu-id="87364-239">Before deciding on an identifier, search the applicable gallery to check if the name is already in use.</span></span> <span data-ttu-id="87364-240">Aby nedocházelo ke konfliktům, dobrým způsobem je použít název vaší společnosti jako první část identifikátor, jako například `Contoso.`.</span><span class="sxs-lookup"><span data-stu-id="87364-240">To avoid conflicts, a good pattern is to use your company name as the first part of the identifier, such as `Contoso.`.</span></span>
- <span data-ttu-id="87364-241">**Namespace jako názvy**: postupujte podle vzor podobná obory názvů v rozhraní .NET, pomocí zápisu s tečkou místo pomlčky.</span><span class="sxs-lookup"><span data-stu-id="87364-241">**Namespace-like names**: Follow a pattern similar to namespaces in .NET, using dot notation instead of hyphens.</span></span> <span data-ttu-id="87364-242">Například použít `Contoso.Utility.UsefulStuff` místo `Contoso-Utility-UsefulStuff` nebo `Contoso_Utility_UsefulStuff`.</span><span class="sxs-lookup"><span data-stu-id="87364-242">For example, use `Contoso.Utility.UsefulStuff` rather than `Contoso-Utility-UsefulStuff` or `Contoso_Utility_UsefulStuff`.</span></span> <span data-ttu-id="87364-243">Příjemci knihovny také užitečné, když se identifikátor balíčku shoduje s obory názvů používá v kódu.</span><span class="sxs-lookup"><span data-stu-id="87364-243">Consumers also find it helpful when the package identifier matches the namespaces used in the code.</span></span>
- <span data-ttu-id="87364-244">**Ukázkové balíčky**: Pokud vytvořit balíček ukázkový kód, který ukazuje, jak chcete použít jiný balíček, připojit `.Sample` jako příponu k identifikátoru, jako v `Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="87364-244">**Sample Packages**: If you produce a package of sample code that demonstrates how to use another package, attach `.Sample` as a suffix to the identifier, as in `Contoso.Utility.UsefulStuff.Sample`.</span></span> <span data-ttu-id="87364-245">(Balíček ukázkové by samozřejmě jsou závislé na jiný balíček.) Při vytváření balíčku ukázka, použijte založené na konvenci pracovní adresář metody popsané výše.</span><span class="sxs-lookup"><span data-stu-id="87364-245">(The sample package would of course have a dependency on the other package.) When creating a sample package, use the convention-based working directory method described earlier.</span></span> <span data-ttu-id="87364-246">V `content` složce uspořádat ukázkový kód ve složce s názvem `\Samples\<identifier>` jako v `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="87364-246">In the `content` folder, arrange the sample code in a folder called `\Samples\<identifier>` as in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span></span>

<span data-ttu-id="87364-247">**Osvědčené postupy pro verze balíčku:**</span><span class="sxs-lookup"><span data-stu-id="87364-247">**Best practices for the package version:**</span></span>

- <span data-ttu-id="87364-248">Obecně platí nastavte verze balíčku tak, aby odpovídaly knihovny, i když to není nezbytně nutné.</span><span class="sxs-lookup"><span data-stu-id="87364-248">In general, set the version of the package to match the library, though this is not strictly required.</span></span> <span data-ttu-id="87364-249">Toto je představuje jednoduché při omezit balíčku do jednoho sestavení, jak je popsáno výše v [rozhodnutí, která sestavení balíčku](#deciding-which-assemblies-to-package).</span><span class="sxs-lookup"><span data-stu-id="87364-249">This is a simple matter when you limit a package to a single assembly, as described earlier in [Deciding which assemblies to package](#deciding-which-assemblies-to-package).</span></span> <span data-ttu-id="87364-250">Celkově platí nezapomeňte, že NuGet samotné se zabývá verze balíčku při rozpoznávání závislostem není verzí sestavení.</span><span class="sxs-lookup"><span data-stu-id="87364-250">Overall, remember that NuGet itself deals with package versions when resolving dependencies, not assembly versions.</span></span>
- <span data-ttu-id="87364-251">Při použití nestandardní verzi schématu, nezapomeňte pravidla verzí NuGet zvažte, jak je popsáno v [Správa verzí balíčku](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="87364-251">When using a non-standard version scheme, be sure to consider the NuGet versioning rules as explained in [Package versioning](../reference/package-versioning.md).</span></span>

> <span data-ttu-id="87364-252">Následující řadu příspěvcích na blogu stručný jsou také užitečné rozumět Správa verzí:</span><span class="sxs-lookup"><span data-stu-id="87364-252">The following series of brief blog posts are also helpful to understand versioning:</span></span>
>
> - [<span data-ttu-id="87364-253">Část 1: Pořízení na knihoven DLL</span><span class="sxs-lookup"><span data-stu-id="87364-253">Part 1: Taking on DLL Hell</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [<span data-ttu-id="87364-254">Část 2: Algoritmus jádra</span><span class="sxs-lookup"><span data-stu-id="87364-254">Part 2: The core algorithm</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [<span data-ttu-id="87364-255">Část 3: Sjednocení prostřednictvím přesměrování vazby</span><span class="sxs-lookup"><span data-stu-id="87364-255">Part 3: Unification via Binding Redirects</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="setting-a-package-type"></a><span data-ttu-id="87364-256">Balíček typ nastavení</span><span class="sxs-lookup"><span data-stu-id="87364-256">Setting a package type</span></span>

<span data-ttu-id="87364-257">U balíčku NuGet 3.5 +, může být označen balíčky konkrétní *typ balíčku* indikující její zamýšlené použití.</span><span class="sxs-lookup"><span data-stu-id="87364-257">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="87364-258">Balíčky s typem, včetně všech balíčky vytvořené pomocí dřívějších verzích systému NuGet, nebyl označen jako výchozí `Dependency` typu.</span><span class="sxs-lookup"><span data-stu-id="87364-258">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="87364-259">`Dependency` Typ balíčky sestavení nebo běhu prostředky přidat do knihovny a aplikace a lze nainstalovat do libovolného typu projektu (za předpokladu, že jsou kompatibilní).</span><span class="sxs-lookup"><span data-stu-id="87364-259">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="87364-260">`DotnetCliTool` Typ balíčky jsou rozšíření [rozhraní příkazového řádku .NET](/dotnet/articles/core/tools/index) a jsou vyvolány z příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="87364-260">`DotnetCliTool` type packages are extensions to the [.NET CLI](/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="87364-261">Tyto balíčky lze nainstalovat pouze v projektech .NET Core a mít žádný vliv na operace obnovení.</span><span class="sxs-lookup"><span data-stu-id="87364-261">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="87364-262">Další podrobnosti o těchto – projekt rozšíření jsou k dispozici v [rozšiřitelnost .NET Core](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) dokumentaci.</span><span class="sxs-lookup"><span data-stu-id="87364-262">More details about these per-project extensions are available in the  [.NET Core extensibility](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

- <span data-ttu-id="87364-263">Vlastní typ balíčků, použijte identifikátor libovolný typ, který vyhovuje pravidlům stejný formát jako ID balíčku.</span><span class="sxs-lookup"><span data-stu-id="87364-263">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="87364-264">Jakýkoli typ jinými než `Dependency` a `DotnetCliTool`, ale nejsou rozpoznány pomocí Správce balíčků NuGet v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="87364-264">Any type other than `Dependency` and `DotnetCliTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="87364-265">Typy balíčků jsou nastavené `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="87364-265">Package types are set in the `.nuspec` file.</span></span> <span data-ttu-id="87364-266">Je nejvhodnější pro zpětnou kompatibilitu pro *není* explicitně nastaven `Dependency` zadejte a místo toho spoléhají na NuGet za předpokladu, že tento typ, pokud žádný typ zadaný.</span><span class="sxs-lookup"><span data-stu-id="87364-266">It's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="87364-267">`.nuspec`: Označuje typ balíčku v rámci `packageTypes\packageType` pod uzlem `<metadata>` element:</span><span class="sxs-lookup"><span data-stu-id="87364-267">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

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

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="87364-268">Přidání soubor readme a další soubory</span><span class="sxs-lookup"><span data-stu-id="87364-268">Adding a readme and other files</span></span>

<span data-ttu-id="87364-269">Pokud chcete přímo zadat soubory, které chcete zahrnout do balíčku, použijte `<files>` uzel v `.nuspec` souboru, který *následuje* `<metadata>` značky:</span><span class="sxs-lookup"><span data-stu-id="87364-269">To directly specify files to include in the package, use the `<files>` node in the `.nuspec` file, which *follows* the `<metadata>` tag:</span></span>

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
> <span data-ttu-id="87364-270">Při použití přístup založené na konvenci pracovní adresář, můžete umístit souboru readme.txt kořenového adresáře balíčku a další obsah `content` složky.</span><span class="sxs-lookup"><span data-stu-id="87364-270">When using the convention-based working directory approach, you can place the readme.txt in the package root and other content in the `content` folder.</span></span> <span data-ttu-id="87364-271">Ne `<file>` prvky jsou nezbytné v manifestu.</span><span class="sxs-lookup"><span data-stu-id="87364-271">No `<file>` elements are necessary in the manifest.</span></span>

<span data-ttu-id="87364-272">Pokud zahrnete soubor s názvem `readme.txt` v kořenu balíčku sady Visual Studio zobrazí obsah tohoto souboru jako prostý text okamžitě po instalaci balíčku přímo.</span><span class="sxs-lookup"><span data-stu-id="87364-272">When you include a file named `readme.txt` in the package root, Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="87364-273">(Soubory Readme nejsou zobrazeny pro balíčky nainstalované jako závislosti).</span><span class="sxs-lookup"><span data-stu-id="87364-273">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="87364-274">Můžete zde je ukázka, jak se zobrazí v souboru readme pro balíček HtmlAgilityPack:</span><span class="sxs-lookup"><span data-stu-id="87364-274">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Zobrazení soubor readme pro balíček NuGet po instalaci](media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="87364-276">Pokud zahrnete prázdnou `<files>` uzel v `.nuspec` souboru NuGet neobsahuje žádný jiný obsah v balíčku než co je v `lib` složky.</span><span class="sxs-lookup"><span data-stu-id="87364-276">If you include an empty `<files>` node in the `.nuspec` file, NuGet doesn't include any other content in the package other than what's in the `lib` folder.</span></span>

## <a name="including-msbuild-props-and-targets-in-a-package"></a><span data-ttu-id="87364-277">Včetně MSBuild props a cíle v balíčku</span><span class="sxs-lookup"><span data-stu-id="87364-277">Including MSBuild props and targets in a package</span></span>

<span data-ttu-id="87364-278">V některých případech můžete chtít přidat vlastní sestavovací cíle nebo vlastnosti v projektech, které využívají vašeho balíčku, jako je například spuštění vlastního nástroje nebo procesu během vytváření sestavení.</span><span class="sxs-lookup"><span data-stu-id="87364-278">In some cases, you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="87364-279">To uděláte tak, že soubory ve formátu `<package_id>.targets` nebo `<package_id>.props` (například `Contoso.Utility.UsefulStuff.targets`) v rámci `\build` složce projektu.</span><span class="sxs-lookup"><span data-stu-id="87364-279">You do this by placing files in the form `<package_id>.targets` or `<package_id>.props` (such as `Contoso.Utility.UsefulStuff.targets`) within the `\build` folder of the project.</span></span>

<span data-ttu-id="87364-280">Soubory v kořenovém `\build` složky jsou považovány za vhodné pro všechny cílové architektury.</span><span class="sxs-lookup"><span data-stu-id="87364-280">Files in the root `\build` folder are considered suitable for all target frameworks.</span></span> <span data-ttu-id="87364-281">Pokud chcete zadat konkrétní rozhraní soubory, nejprve umístíte těch v rámci příslušných podsložek, například následující:</span><span class="sxs-lookup"><span data-stu-id="87364-281">To provide framework-specific files, first place those within appropriate subfolders, such as the following:</span></span>

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

<span data-ttu-id="87364-282">Potom v `.nuspec` souboru, ujistěte se, který bude odkazovat na těchto souborů v `<files>` uzlu:</span><span class="sxs-lookup"><span data-stu-id="87364-282">Then in the `.nuspec` file, be sure to refer to these files in the `<files>` node:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata minClientVersion="2.5">
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

<span data-ttu-id="87364-283">Včetně MSBuild props a cíle v balíčku byla [zavedené NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), proto se doporučuje přidat `minClientVersion="2.5"` atribut `metadata` element udávajících minimální verzi klienta NuGet potřeba využívat balíčku.</span><span class="sxs-lookup"><span data-stu-id="87364-283">Including MSBuild props and targets in a package was [introduced with NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), therefore it is recommended to add the `minClientVersion="2.5"` attribute to the `metadata` element, to indicate the minimum NuGet client version required to consume the package.</span></span>

<span data-ttu-id="87364-284">Když NuGet nainstaluje balíček s `\build` soubory, přidá MSBuild `<Import>` elementy v souboru projektu odkazující na `.targets` a `.props` soubory.</span><span class="sxs-lookup"><span data-stu-id="87364-284">When NuGet installs a package with `\build` files, it adds an MSBuild `<Import>` elements in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="87364-285">(`.props` se přidá na začátek souboru projektu; `.targets` se přidá na dolní.)</span><span class="sxs-lookup"><span data-stu-id="87364-285">(`.props` is added at the top of the project file; `.targets` is added at the bottom.)</span></span>

<span data-ttu-id="87364-286">U balíčku NuGet 3.x, cíle nejsou přidány do projektu, ale místo toho jsou k dispozici prostřednictvím `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="87364-286">With NuGet 3.x, targets are not added to the project but are instead made available through the `project.lock.json`.</span></span>

## <a name="authoring-packages-with-com-interop-assemblies"></a><span data-ttu-id="87364-287">Vytváření balíčků s sestavení vzájemné spolupráce COM</span><span class="sxs-lookup"><span data-stu-id="87364-287">Authoring packages with COM interop assemblies</span></span>

<span data-ttu-id="87364-288">Balíčky, které obsahují sestavení vzájemné spolupráce COM musí obsahovat odpovídající [cíle souboru](#including-msbuild-props-and-targets-in-a-package) tak, aby správný `EmbedInteropTypes` metadata jsou přidány do projektů pomocí formátu PackageReference.</span><span class="sxs-lookup"><span data-stu-id="87364-288">Packages that contain COM interop assemblies must include an appropriate [targets file](#including-msbuild-props-and-targets-in-a-package) so that the correct `EmbedInteropTypes` metadata is added to projects using the PackageReference format.</span></span> <span data-ttu-id="87364-289">Ve výchozím nastavení `EmbedInteropTypes` metadata je vždy hodnotu false pro všechna sestavení při PackageReference se používá, takže soubor cíle přidá tato metadata explicitně.</span><span class="sxs-lookup"><span data-stu-id="87364-289">By default, the `EmbedInteropTypes` metadata is always false for all assemblies when PackageReference is used, so the targets file adds this metadata explicitly.</span></span> <span data-ttu-id="87364-290">Aby nedocházelo ke konfliktům, musí být cílový název jedinečné; v ideálním případě použít kombinaci váš název balíčku a sestavení se embedded, ve které nahradíte `{InteropAssemblyName}` v níže uvedeném příkladu s danou hodnotou.</span><span class="sxs-lookup"><span data-stu-id="87364-290">To avoid conflicts, the target name should be unique; ideally, use a combination of your package name and the assembly being embedded, replacing the `{InteropAssemblyName}` in the example below with that value.</span></span> <span data-ttu-id="87364-291">(Viz také [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) příklad.)</span><span class="sxs-lookup"><span data-stu-id="87364-291">(Also see [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) for an example.)</span></span>

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

<span data-ttu-id="87364-292">Všimněte si, že při použití `packages.config` NuGet a sady Visual Studio pro kontrolu sestavení vzájemné spolupráce COM a nastavit přidávání odkazů na sestavení z balíčků způsobí, že formát reference `EmbedInteropTypes` na hodnotu true v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="87364-292">Note that when using the `packages.config` reference format, adding references to the assemblies from the packages causes NuGet and Visual Studio to check for COM interop assemblies and set the `EmbedInteropTypes` to true in the project file.</span></span> <span data-ttu-id="87364-293">V tomto případě jsou cíle elementem.</span><span class="sxs-lookup"><span data-stu-id="87364-293">In this case the targets are overriden.</span></span>

<span data-ttu-id="87364-294">Kromě toho ve výchozím nastavení [toku prostředky sestavení není přechodně](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="87364-294">Additionally, by default the [build assets do not flow transitively](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span> <span data-ttu-id="87364-295">Balíčky vytvořené podle postupu popsaného tady pracovní jinak po jejich vyjmutí jako přenositelné závislost z odkaz na projekt na projekt.</span><span class="sxs-lookup"><span data-stu-id="87364-295">Packages authored as described here work differently when they are pulled as a transitive dependency from a project to project reference.</span></span> <span data-ttu-id="87364-296">Příjemce balíček můžete jim toku změnou výchozí hodnota PrivateAssets tak, aby neobsahoval sestavení povolit.</span><span class="sxs-lookup"><span data-stu-id="87364-296">The package consumer can allow them to flow by modifying the PrivateAssets default value to not include build.</span></span>

<a name="creating-the-package"></a>

## <a name="running-nuget-pack-to-generate-the-nupkg-file"></a><span data-ttu-id="87364-297">S aktualizací Service pack nuget ke generování souboru .nupkg v podadresáři</span><span class="sxs-lookup"><span data-stu-id="87364-297">Running nuget pack to generate the .nupkg file</span></span>

<span data-ttu-id="87364-298">Pokud používáte sestavení nebo pracovní adresář založené na konvenci, vytvořit balíček spuštěním `nuget pack` s vaší `.nuspec` souboru, nahraďte `<manifest-name>` s vaší konkrétní název souboru:</span><span class="sxs-lookup"><span data-stu-id="87364-298">When using an assembly or the convention-based working directory, create a package by running `nuget pack` with your `.nuspec` file, replacing `<manifest-name>` with your specific filename:</span></span>

```cli
nuget pack <project-name>.nuspec
```

<span data-ttu-id="87364-299">Při použití projektu sady Visual Studio, spusťte `nuget pack` s soubor projektu, který automaticky načte projektu `.nuspec` souboru a nahradí všechny tokeny v něm pomocí hodnot v souboru projektu:</span><span class="sxs-lookup"><span data-stu-id="87364-299">When using a Visual Studio project, run `nuget pack` with your project file, which automatically loads the project's `.nuspec` file and replaces any tokens within it using values in the project file:</span></span>

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> <span data-ttu-id="87364-300">Přímo pomocí souboru projektu je nezbytné pro token nahrazení, protože projekt je zdrojem hodnoty tokenu.</span><span class="sxs-lookup"><span data-stu-id="87364-300">Using the project file directly is necessary for token replacement because the project is the source of the token values.</span></span> <span data-ttu-id="87364-301">Nahrazení tokenu není dojít, pokud používáte `nuget pack` s `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="87364-301">Token replacement does not happen if you use `nuget pack` with a `.nuspec` file.</span></span>

<span data-ttu-id="87364-302">Ve všech případech `nuget pack` vyloučí složek, které začínají s dobou, jako například `.git` nebo `.hg`.</span><span class="sxs-lookup"><span data-stu-id="87364-302">In all cases, `nuget pack` excludes folders that start with a period, such as `.git` or `.hg`.</span></span>

<span data-ttu-id="87364-303">NuGet označuje, pokud jsou všechny chyby `.nuspec` soubor, který vyžadují opravu, jako je například, že zapomenete změnit zástupné hodnoty v manifestu.</span><span class="sxs-lookup"><span data-stu-id="87364-303">NuGet indicates if there are any errors in the `.nuspec` file that need correcting, such as forgetting to change placeholder values in the manifest.</span></span>

<span data-ttu-id="87364-304">Jednou `nuget pack` úspěšné, máte `.nupkg` souborů, které můžete publikovat do Galerie vhodný, jak je popsáno v [publikování balíčku](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="87364-304">Once `nuget pack` succeeds, you have a `.nupkg` file that you can publish to a suitable gallery as described in [Publishing a Package](../create-packages/publish-a-package.md).</span></span>

> [!Tip]
> <span data-ttu-id="87364-305">Užitečné způsob, jak zkontrolovat balíček po vytvoření ho otevřít v [balíček Průzkumníka](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) nástroj.</span><span class="sxs-lookup"><span data-stu-id="87364-305">A helpful way to examine a package after creating it is to open it in the [Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) tool.</span></span> <span data-ttu-id="87364-306">To vám dává grafické zobrazení obsah balíčku a jeho manifestu.</span><span class="sxs-lookup"><span data-stu-id="87364-306">This gives you a graphical view of the package contents and its manifest.</span></span> <span data-ttu-id="87364-307">Můžete také přejmenovat, výsledná `.nupkg` do souboru `.zip` souboru a seznamte se s jeho obsahem přímo.</span><span class="sxs-lookup"><span data-stu-id="87364-307">You can also rename the resulting `.nupkg` file to a `.zip` file and explore its contents directly.</span></span>

### <a name="additional-options"></a><span data-ttu-id="87364-308">Další možnosti</span><span class="sxs-lookup"><span data-stu-id="87364-308">Additional options</span></span>

<span data-ttu-id="87364-309">Můžete použít různé přepínače příkazového řádku s `nuget pack` vyloučit soubory, přepsat číslo verze v manifestu a změnit do výstupní složky mezi dalších funkcí.</span><span class="sxs-lookup"><span data-stu-id="87364-309">You can use various command-line switches with `nuget pack` to exclude files, override the version number in the manifest, and change the output folder, among other features.</span></span> <span data-ttu-id="87364-310">Úplný seznam najdete v článku [pack reference k příkazům](../tools/cli-ref-pack.md).</span><span class="sxs-lookup"><span data-stu-id="87364-310">For a complete list, refer to the [pack command reference](../tools/cli-ref-pack.md).</span></span>

<span data-ttu-id="87364-311">Pár jsou běžné u projektů sady Visual Studio jsou následující možnosti:</span><span class="sxs-lookup"><span data-stu-id="87364-311">The following options are a few that are common with Visual Studio projects:</span></span>

- <span data-ttu-id="87364-312">**Odkazovaný projekty**: Pokud projekt odkazuje na jiné projekty, můžete přidat odkazované projekty jako součást balíčku, nebo jako závislosti, s použitím `-IncludeReferencedProjects` možnost:</span><span class="sxs-lookup"><span data-stu-id="87364-312">**Referenced projects**: If the project references other projects, you can add the referenced projects as part of the package, or as dependencies, by using the `-IncludeReferencedProjects` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    <span data-ttu-id="87364-313">Tento proces zahrnutí je rekurzivní, takže když `MyProject.csproj` odkazy na projekty B a C a tyto projekty odkazovat D, E a F a potom soubory z B, C, D, E a F jsou součástí balíčku.</span><span class="sxs-lookup"><span data-stu-id="87364-313">This inclusion process is recursive, so if `MyProject.csproj` references projects B and C, and those projects reference D, E, and F, then files from B, C, D, E, and F are included in the package.</span></span>

    <span data-ttu-id="87364-314">Pokud obsahuje odkazovaný projektu `.nuspec` souboru svůj vlastní, pak NuGet přidá tento Odkazovaný projekt jako závislost místo.</span><span class="sxs-lookup"><span data-stu-id="87364-314">If a referenced project includes a `.nuspec` file of its own, then NuGet adds that referenced project as a dependency instead.</span></span>  <span data-ttu-id="87364-315">Budete muset balíčku a publikování tohoto projektu v samostatně.</span><span class="sxs-lookup"><span data-stu-id="87364-315">You need to package and publish that project separately.</span></span>

- <span data-ttu-id="87364-316">**Konfigurace sestavení**: ve výchozím nastavení používá NuGet je konfigurace sestavení výchozí nastavená v souboru projektu, obvykle *ladění*.</span><span class="sxs-lookup"><span data-stu-id="87364-316">**Build configuration**: By default, NuGet uses the default build configuration set in the project file, typically *Debug*.</span></span> <span data-ttu-id="87364-317">K pack soubory z různých sestavení konfigurace, jako například *verze*, použijte `-properties` možnost s konfigurací:</span><span class="sxs-lookup"><span data-stu-id="87364-317">To pack files from a different build configuration, such as *Release*, use the `-properties` option with the configuration:</span></span>

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- <span data-ttu-id="87364-318">**Symboly**: Chcete-li například symboly, které umožňují příjemcům krokovat kód balíčku v ladicím programu, použijte `-Symbols` možnost:</span><span class="sxs-lookup"><span data-stu-id="87364-318">**Symbols**: to include symbols that allow consumers to step through your package code in the debugger, use the `-Symbols` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="testing-package-installation"></a><span data-ttu-id="87364-319">Testování instalace balíčku</span><span class="sxs-lookup"><span data-stu-id="87364-319">Testing package installation</span></span>

<span data-ttu-id="87364-320">Před publikováním balíček, chcete obvykle testovat proces instalace balíčku do projektu.</span><span class="sxs-lookup"><span data-stu-id="87364-320">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="87364-321">Testy, zkontrolujte, zda nutně soubory všechny skončili na jejich správné místech v projektu.</span><span class="sxs-lookup"><span data-stu-id="87364-321">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="87364-322">Můžete otestovat instalace ručně v sadě Visual Studio nebo na příkazovém řádku pomocí normální [balíček kroky instalace](../consume-packages/ways-to-install-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="87364-322">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/ways-to-install-a-package.md).</span></span>

<span data-ttu-id="87364-323">Pro automatizované testování základní proces je následující:</span><span class="sxs-lookup"><span data-stu-id="87364-323">For automated testing, the basic process is as follows:</span></span>

1. <span data-ttu-id="87364-324">Kopírování `.nupkg` soubor do místní složky.</span><span class="sxs-lookup"><span data-stu-id="87364-324">Copy the `.nupkg` file to a local folder.</span></span>
1. <span data-ttu-id="87364-325">Přidat složku do vaší zdroje balíčku pomocí `nuget sources add -name <name> -source <path>` příkazu (najdete v části [zdroje nuget](../tools/cli-ref-sources.md)).</span><span class="sxs-lookup"><span data-stu-id="87364-325">Add the folder to your package sources using the `nuget sources add -name <name> -source <path>` command (see [nuget sources](../tools/cli-ref-sources.md)).</span></span> <span data-ttu-id="87364-326">Všimněte si, že budete potřebovat pouze jednou nastavit tento místní zdroj libovolného daného počítače.</span><span class="sxs-lookup"><span data-stu-id="87364-326">Note that you need only set this local source once on any given computer.</span></span>
1. <span data-ttu-id="87364-327">Nainstalujte balíček z tohoto zdroje pomocí `nuget install <packageID> -source <name>` kde `<name>` odpovídá názvu zdrojového přidělený `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="87364-327">Install the package from that source using `nuget install <packageID> -source <name>` where `<name>` matches the name of your source as given to `nuget sources`.</span></span> <span data-ttu-id="87364-328">Zadání zdrojové zajistí, že balíček je nainstalovat z tohoto zdroje samostatně.</span><span class="sxs-lookup"><span data-stu-id="87364-328">Specifying the source ensures that the package is installed from that source alone.</span></span>
1. <span data-ttu-id="87364-329">Zkontrolujte a zkontrolujte, zda jsou soubory správně nainstalovány v systému souborů.</span><span class="sxs-lookup"><span data-stu-id="87364-329">Examine the file system to check that files are installed correctly.</span></span>

## <a name="next-steps"></a><span data-ttu-id="87364-330">Další kroky</span><span class="sxs-lookup"><span data-stu-id="87364-330">Next Steps</span></span>

<span data-ttu-id="87364-331">Po vytvoření balíčku, který je `.nupkg` souboru, můžete ji publikujete do Galerie zvoleného jak je popsáno na [publikování balíčku](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="87364-331">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="87364-332">Můžete také chtít rozšiřují možnosti vašeho balíčku nebo jinak podporovala jiné scénáře, jak je popsáno v následujících tématech:</span><span class="sxs-lookup"><span data-stu-id="87364-332">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="87364-333">Správa verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="87364-333">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="87364-334">Podpora více cílových verzí rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="87364-334">Supporting multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="87364-335">Transformace zdroje a konfiguračních souborů</span><span class="sxs-lookup"><span data-stu-id="87364-335">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="87364-336">Lokalizace</span><span class="sxs-lookup"><span data-stu-id="87364-336">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="87364-337">Předběžné verze</span><span class="sxs-lookup"><span data-stu-id="87364-337">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)

<span data-ttu-id="87364-338">Nakonec existují další balíčky typy zajímat:</span><span class="sxs-lookup"><span data-stu-id="87364-338">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="87364-339">Nativní balíčky</span><span class="sxs-lookup"><span data-stu-id="87364-339">Native Packages</span></span>](../create-packages/native-packages.md)
- [<span data-ttu-id="87364-340">Balíčky symbolů</span><span class="sxs-lookup"><span data-stu-id="87364-340">Symbol Packages</span></span>](../create-packages/symbol-packages.md)
