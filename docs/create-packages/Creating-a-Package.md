---
title: Jak vytvořit balíček NuGet
description: Podrobné pokyny k procesu návrhu a vytvoření balíčku NuGet, včetně klíčových rozhodovací body, jako jsou soubory a správy verzí.
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: f0d9667b752caf7831278ac3fd63cfd67f7d34a4
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610584"
---
# <a name="creating-nuget-packages"></a><span data-ttu-id="571a6-103">Vytváření balíčků NuGet</span><span class="sxs-lookup"><span data-stu-id="571a6-103">Creating NuGet packages</span></span>

<span data-ttu-id="571a6-104">Bez ohledu na to co dělá váš balíček nebo co kódu obsahuje, použít `nuget.exe` do balíčku, které tuto funkci do komponenty, které můžete sdílet s a používat libovolný počet dalších vývojářů.</span><span class="sxs-lookup"><span data-stu-id="571a6-104">No matter what your package does or what code it contains, you use `nuget.exe` to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="571a6-105">Chcete-li nainstalovat `nuget.exe`, naleznete v tématu [nainstalovat rozhraní příkazového řádku NuGet](../install-nuget-client-tools.md#nugetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="571a6-105">To install `nuget.exe`, see [Install NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli).</span></span> <span data-ttu-id="571a6-106">Všimněte si, že Visual Studio automaticky nezahrnuje `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="571a6-106">Note that Visual Studio does not automatically include `nuget.exe`.</span></span>

<span data-ttu-id="571a6-107">Technicky vzato balíček NuGet je jenom soubor ZIP, který je byl přejmenován s `.nupkg` rozšíření a jehož obsah odpovídat určité konvence.</span><span class="sxs-lookup"><span data-stu-id="571a6-107">Technically speaking, a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension and whose contents match certain conventions.</span></span> <span data-ttu-id="571a6-108">Toto téma popisuje podrobný postup vytvoření balíčku, který splňuje tyto konvence.</span><span class="sxs-lookup"><span data-stu-id="571a6-108">This topic describes the detailed process of creating a package that meets those conventions.</span></span> <span data-ttu-id="571a6-109">Podrobný návod najdete v tématu [rychlý start: vytvoření a publikování balíčku](../quickstart/create-and-publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="571a6-109">For a focused walkthrough, refer to [Quickstart: create and publish a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="571a6-110">Balení začíná zkompilovaného kódu (sestavení), symboly a/nebo jiné soubory, které má být dodána jako balíček (viz [přehled a pracovní postup](overview-and-workflow.md)).</span><span class="sxs-lookup"><span data-stu-id="571a6-110">Packaging begins with the compiled code (assemblies), symbols, and/or other files that you want to deliver as a package (see [Overview and workflow](overview-and-workflow.md)).</span></span> <span data-ttu-id="571a6-111">Tento proces je nezávislý na kompilace nebo jinak generování souborů, které patří do balíčku, i když můžete nakreslit z informací v souboru projektu pro synchronizaci kompilované sestavení a balíčky.</span><span class="sxs-lookup"><span data-stu-id="571a6-111">This process is independent from compiling or otherwise generating the files that go into the package, although you can draw from information in a project file to keep the compiled assemblies and packages in sync.</span></span>

> [!Note]
> <span data-ttu-id="571a6-112">Toto téma platí pro typy projektů než projekty .NET Core pomocí sady Visual Studio 2017 a NuGet 4.0 +.</span><span class="sxs-lookup"><span data-stu-id="571a6-112">This topic applies to project types other than .NET Core projects using Visual Studio 2017 and NuGet 4.0+.</span></span> <span data-ttu-id="571a6-113">V těchto projektech .NET Core NuGet používá informace v souboru projektu přímo.</span><span class="sxs-lookup"><span data-stu-id="571a6-113">In those .NET Core projects, NuGet uses information in the project file directly.</span></span> <span data-ttu-id="571a6-114">Podrobnosti najdete v tématu [vytvořit standardní balíčky .NET se sadou Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) a [NuGet aktualizací Service pack a obnovení jako cílů MSBuild](../reference/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="571a6-114">For details, see [Create .NET Standard Packages with Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) and [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).</span></span>

## <a name="deciding-which-assemblies-to-package"></a><span data-ttu-id="571a6-115">Rozhodování o tom, která sestavení do balíčku</span><span class="sxs-lookup"><span data-stu-id="571a6-115">Deciding which assemblies to package</span></span>

<span data-ttu-id="571a6-116">Většina pro obecné účely balíčky obsahují jeden nebo více sestavení, které ostatní vývojáři mohou použít ve své vlastní projekty.</span><span class="sxs-lookup"><span data-stu-id="571a6-116">Most general-purpose packages contain one or more assemblies that other developers can use in their own projects.</span></span>

- <span data-ttu-id="571a6-117">Obecně je vhodné mít jedno sestavení na balíček NuGet, za předpokladu, že každé sestavení je nezávisle na sobě užitečné.</span><span class="sxs-lookup"><span data-stu-id="571a6-117">In general, it's best to have one assembly per NuGet package, provided that each assembly is independently useful.</span></span> <span data-ttu-id="571a6-118">Například, pokud máte `Utilities.dll` , který závisí na `Parser.dll`, a `Parser.dll` je užitečné sama o sobě a pak vytvořte jeden balíček pro každého.</span><span class="sxs-lookup"><span data-stu-id="571a6-118">For example, if you have a `Utilities.dll` that depends on `Parser.dll`, and `Parser.dll` is useful on its own, then create one package for each.</span></span> <span data-ttu-id="571a6-119">To umožňuje vývojářům využít `Parser.dll` nezávisle na `Utilities.dll`.</span><span class="sxs-lookup"><span data-stu-id="571a6-119">Doing so allows developers to use `Parser.dll` independently of `Utilities.dll`.</span></span>

- <span data-ttu-id="571a6-120">Pokud vaše knihovna se skládá z více sestavení, které nejsou nezávisle na sobě užitečné, pak je v pořádku je zkombinovat do jednoho balíčku.</span><span class="sxs-lookup"><span data-stu-id="571a6-120">If your library is composed of multiple assemblies that aren't independently useful, then it's fine to combine them into one package.</span></span> <span data-ttu-id="571a6-121">Použijeme předchozí příklad, pokud `Parser.dll` obsahuje kód, který je používán pouze `Utilities.dll`, pak můžete zachovat `Parser.dll` ve stejném balíku.</span><span class="sxs-lookup"><span data-stu-id="571a6-121">Using the previous example, if `Parser.dll` contains code that's used only by `Utilities.dll`, then it's fine to keep `Parser.dll` in the same package.</span></span>

- <span data-ttu-id="571a6-122">Podobně pokud `Utilities.dll` závisí na `Utilities.resources.dll`, je-li znovu odkazující aktivita není užitečná sama o sobě, potom se spojí i ve stejném balíku.</span><span class="sxs-lookup"><span data-stu-id="571a6-122">Similarly, if `Utilities.dll` depends on `Utilities.resources.dll`, where again the latter is not useful on its own, then put both in the same package.</span></span>

<span data-ttu-id="571a6-123">Prostředky ve skutečnosti představují zvláštní případ.</span><span class="sxs-lookup"><span data-stu-id="571a6-123">Resources are, in fact, a special case.</span></span> <span data-ttu-id="571a6-124">Při instalaci do projektu balíček NuGet automaticky přidá odkazy na sestavení knihovny DLL balíčku, *s výjimkou* ty, které jsou pojmenovány `.resources.dll` vzhledem k tomu, že se budou považovat za lokalizovaná satelitní sestavení (viz [ Vytvoření lokalizovaných balíčků](creating-localized-packages.md)).</span><span class="sxs-lookup"><span data-stu-id="571a6-124">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies (see [Creating localized packages](creating-localized-packages.md)).</span></span> <span data-ttu-id="571a6-125">Z tohoto důvodu se vyhněte se použití `.resources.dll` pro soubory, které jinak obsahují základní balíček kódu.</span><span class="sxs-lookup"><span data-stu-id="571a6-125">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="571a6-126">Pokud vaše knihovna obsahuje sestavení vzájemné spolupráce COM, postupujte podle dalších pokynů v [vytváření balíčků pomocí sestavení vzájemné spolupráce COM](#authoring-packages-with-com-interop-assemblies).</span><span class="sxs-lookup"><span data-stu-id="571a6-126">If your library contains COM interop assemblies, follow additional the guidelines in [Authoring packages with COM interop assemblies](#authoring-packages-with-com-interop-assemblies).</span></span>

## <a name="the-role-and-structure-of-the-nuspec-file"></a><span data-ttu-id="571a6-127">Role a struktura souboru .nuspec souboru</span><span class="sxs-lookup"><span data-stu-id="571a6-127">The role and structure of the .nuspec file</span></span>

<span data-ttu-id="571a6-128">Když víte, jaké soubory, které chcete balíček, dalším krokem je vytvoření manifestu balíčku v `.nuspec` souboru XML.</span><span class="sxs-lookup"><span data-stu-id="571a6-128">Once you know what files you want to package, the next step is creating a package manifest in a `.nuspec` XML file.</span></span>

<span data-ttu-id="571a6-129">Manifest:</span><span class="sxs-lookup"><span data-stu-id="571a6-129">The manifest:</span></span>

1. <span data-ttu-id="571a6-130">Popisuje obsah balíčku a je součástí balíčku.</span><span class="sxs-lookup"><span data-stu-id="571a6-130">Describes the package's contents and is itself included in the package.</span></span>
1. <span data-ttu-id="571a6-131">Vytvoření balíčku a nastaví na tom, jak nainstalovat do projektu balíček NuGet.</span><span class="sxs-lookup"><span data-stu-id="571a6-131">Drives both the creation of the package and instructs NuGet on how to install the package into a project.</span></span> <span data-ttu-id="571a6-132">Například manifest identifikuje další závislosti balíčků tak, aby NuGet můžete nainstalovat také těchto závislostí při instalaci hlavního balíčku.</span><span class="sxs-lookup"><span data-stu-id="571a6-132">For example, the manifest identifies other package dependencies such that NuGet can also install those dependencies when the main package is installed.</span></span>
1. <span data-ttu-id="571a6-133">Obsahuje vlastnosti požadované a volitelné, jak je popsáno níže.</span><span class="sxs-lookup"><span data-stu-id="571a6-133">Contains both required and optional properties as described below.</span></span> <span data-ttu-id="571a6-134">Naleznete v části najdete přesné informace, včetně dalších vlastností, zde nejsou uvedeny [souboru .nuspec odkaz](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="571a6-134">For exact details, including other properties not mentioned here, see  the [.nuspec reference](../reference/nuspec.md).</span></span>

<span data-ttu-id="571a6-135">Požadované vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="571a6-135">Required properties:</span></span>

- <span data-ttu-id="571a6-136">Identifikátor balíčku musí být jedinečný ve galerii, který je hostitelem balíčku.</span><span class="sxs-lookup"><span data-stu-id="571a6-136">The package identifier, which must be unique across the gallery that hosts the package.</span></span>
- <span data-ttu-id="571a6-137">Konkrétní verzi číslo ve tvaru *Hlavníverze.podverze.oprava [-přípona]* kde *– přípona* identifikuje [předběžných verzí](prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="571a6-137">A specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md)</span></span>
- <span data-ttu-id="571a6-138">Název balíčku jak by se měla objevit na hostiteli (jako je nuget.org)</span><span class="sxs-lookup"><span data-stu-id="571a6-138">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="571a6-139">Informace o Autor a vlastník.</span><span class="sxs-lookup"><span data-stu-id="571a6-139">Author and owner information.</span></span>
- <span data-ttu-id="571a6-140">Dlouhý popis balíčku.</span><span class="sxs-lookup"><span data-stu-id="571a6-140">A long description of the package.</span></span>

<span data-ttu-id="571a6-141">Společné vlastnosti volitelné:</span><span class="sxs-lookup"><span data-stu-id="571a6-141">Common optional properties:</span></span>

- <span data-ttu-id="571a6-142">Zpráva k vydání verze</span><span class="sxs-lookup"><span data-stu-id="571a6-142">Release notes</span></span>
- <span data-ttu-id="571a6-143">Informace o autorských právech</span><span class="sxs-lookup"><span data-stu-id="571a6-143">Copyright information</span></span>
- <span data-ttu-id="571a6-144">Krátký popis [uživatelského rozhraní Správce balíčků v sadě Visual Studio](../tools/package-manager-ui.md)</span><span class="sxs-lookup"><span data-stu-id="571a6-144">A short description for the [Package Manager UI in Visual Studio](../tools/package-manager-ui.md)</span></span>
- <span data-ttu-id="571a6-145">ID národního prostředí</span><span class="sxs-lookup"><span data-stu-id="571a6-145">A locale ID</span></span>
- <span data-ttu-id="571a6-146">Adresa URL projektu</span><span class="sxs-lookup"><span data-stu-id="571a6-146">Project URL</span></span>
- <span data-ttu-id="571a6-147">Licence jako výraz nebo souboru (`licenseUrl` je zastaralé, použijte [ `license` prvek metadat souboru nuspec](../reference/nuspec.md#license))</span><span class="sxs-lookup"><span data-stu-id="571a6-147">License as an expression or file (`licenseUrl` is being deprecated, use the [`license` nuspec metadata element](../reference/nuspec.md#license))</span></span>
- <span data-ttu-id="571a6-148">Adresa URL ikony</span><span class="sxs-lookup"><span data-stu-id="571a6-148">An icon URL</span></span>
- <span data-ttu-id="571a6-149">Seznam závislosti a odkazy</span><span class="sxs-lookup"><span data-stu-id="571a6-149">Lists of dependencies and references</span></span>
- <span data-ttu-id="571a6-150">Značky, které pomáhají při hledání v galerii</span><span class="sxs-lookup"><span data-stu-id="571a6-150">Tags that assist in gallery searches</span></span>

<span data-ttu-id="571a6-151">Tady je typické (ale fiktivní) `.nuspec` soubor s komentáři popisující vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="571a6-151">The following is a typical (but fictitious) `.nuspec` file, with comments describing the properties:</span></span>

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

        <!-- 
            Owners are typically nuget.org identities that allow gallery
            users to easily find other packages by the same owners.  
        -->
        <owners>dejanatc, rjdey</owners>
        
         <!-- Project URL provides a link for the gallery -->
        <projectUrl>http://github.com/contoso/UsefulStuff</projectUrl>

         <!-- License information is displayed on the gallery -->
        <license type="expression">Apache-2.0</license>
        

        <!-- The icon is used in Visual Studio's package manager UI -->
        <iconUrl>http://github.com/contoso/UsefulStuff/nuget_icon.png</iconUrl>

        <!-- 
            If true, this value prompts the user to accept the license when
            installing the package. 
        -->
        <requireLicenseAcceptance>false</requireLicenseAcceptance>

        <!-- Any details about this particular release -->
        <releaseNotes>Bug fixes and performance improvements</releaseNotes>

        <!-- 
            The description can be used in package manager UI. Note that the
            nuget.org gallery uses information you add in the portal. 
        -->
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

<span data-ttu-id="571a6-152">Podrobnosti o deklarace závislostí a zadání čísla verzí, naleznete v tématu [Správa verzí balíčků](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="571a6-152">For details on declaring dependencies and specifying version numbers, see [Package versioning](../reference/package-versioning.md).</span></span> <span data-ttu-id="571a6-153">Je také možné na povrchu prostředky od závislostí přímo v balíčku pomocí `include` a `exclude` atributy na `dependency` elementu.</span><span class="sxs-lookup"><span data-stu-id="571a6-153">It is also possible to surface assets from dependencies directly in the package by using the `include` and `exclude` attributes on the `dependency` element.</span></span> <span data-ttu-id="571a6-154">Zobrazit [souboru .nuspec Reference - závislosti](../reference/nuspec.md#dependencies).</span><span class="sxs-lookup"><span data-stu-id="571a6-154">See [.nuspec Reference - Dependencies](../reference/nuspec.md#dependencies).</span></span>

<span data-ttu-id="571a6-155">Protože manifest je součástí balíčku vytvořených z ní, najdete prozkoumáním existující balíčky libovolný počet dalších příkladů.</span><span class="sxs-lookup"><span data-stu-id="571a6-155">Because the manifest is included in the package created from it, you can find any number of additional examples by examining existing packages.</span></span> <span data-ttu-id="571a6-156">Dobrým zdrojem je *global-packages* složky v počítači, umístění se vrátí následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="571a6-156">A good source is the *global-packages* folder on your computer, the location of which is returned by the following command:</span></span>

```cli
nuget locals -list global-packages
```

<span data-ttu-id="571a6-157">Přejděte do libovolného *package\version* složka, Kopírovat `.nupkg` do souboru `.zip` souboru a pak otevřete, který `.zip` souboru a zkoumat `.nuspec` v něm.</span><span class="sxs-lookup"><span data-stu-id="571a6-157">Go into any *package\version* folder, copy the `.nupkg` file to a `.zip` file, then open that `.zip` file and examine the `.nuspec` within it.</span></span>

> [!Note]
> <span data-ttu-id="571a6-158">Při vytváření `.nuspec` z projektu sady Visual Studio obsahuje manifest tokeny, které jsou nahrazeny informacemi z projektu při vytváření balíčku.</span><span class="sxs-lookup"><span data-stu-id="571a6-158">When creating a `.nuspec` from a Visual Studio project, the manifest contains tokens that are replaced with information from the project when the package is built.</span></span> <span data-ttu-id="571a6-159">Zobrazit [vytváření souboru .nuspec z projektu sady Visual Studio](#from-a-visual-studio-project).</span><span class="sxs-lookup"><span data-stu-id="571a6-159">See [Creating the .nuspec from a Visual Studio project](#from-a-visual-studio-project).</span></span>

## <a name="creating-the-nuspec-file"></a><span data-ttu-id="571a6-160">Vytvoření souboru .nuspec souboru</span><span class="sxs-lookup"><span data-stu-id="571a6-160">Creating the .nuspec file</span></span>

<span data-ttu-id="571a6-161">Vytvoření kompletní manifestu obvykle začíná základní `.nuspec` soubor generovaný prostřednictvím jednoho z následujících metod:</span><span class="sxs-lookup"><span data-stu-id="571a6-161">Creating a complete manifest typically begins with a basic `.nuspec` file generated through one of the following methods:</span></span>

- [<span data-ttu-id="571a6-162">Podle úmluvy pracovní adresář</span><span class="sxs-lookup"><span data-stu-id="571a6-162">A convention-based working directory</span></span>](#from-a-convention-based-working-directory)
- [<span data-ttu-id="571a6-163">Sestavení knihovny DLL</span><span class="sxs-lookup"><span data-stu-id="571a6-163">An assembly DLL</span></span>](#from-an-assembly-dll)
- [<span data-ttu-id="571a6-164">A Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="571a6-164">A Visual Studio project</span></span>](#from-a-visual-studio-project)    
- [<span data-ttu-id="571a6-165">Nový soubor s výchozími hodnotami.</span><span class="sxs-lookup"><span data-stu-id="571a6-165">New file with default values</span></span>](#new-file-with-default-values)

<span data-ttu-id="571a6-166">Pak upravíte soubor ručně tak, aby popisuje přesný obsah, který chcete ve finálním balíčku.</span><span class="sxs-lookup"><span data-stu-id="571a6-166">You then edit the file by hand so that it describes the exact content you want in the final package.</span></span>

> [!Important]
> <span data-ttu-id="571a6-167">Vygeneruje `.nuspec` soubory obsahují zástupné symboly, které musí být upravena před vytvořením balíčku s `nuget pack` příkazu.</span><span class="sxs-lookup"><span data-stu-id="571a6-167">Generated `.nuspec` files contain placeholders that must be modified before creating the package with the `nuget pack` command.</span></span> <span data-ttu-id="571a6-168">Příkaz selže, pokud `.nuspec` obsahuje zástupné symboly.</span><span class="sxs-lookup"><span data-stu-id="571a6-168">That command fails if the `.nuspec` contains any placeholders.</span></span>

### <a name="from-a-convention-based-working-directory"></a><span data-ttu-id="571a6-169">Z pracovního adresáře podle úmluvy</span><span class="sxs-lookup"><span data-stu-id="571a6-169">From a convention-based working directory</span></span>

<span data-ttu-id="571a6-170">Vzhledem k tomu, že balíček NuGet je jenom soubor ZIP, který je byl přejmenován s `.nupkg` rozšíření, často je nejjednodušší vytvořit strukturu složky na vašem místním systému souborů a pak se vytvořit `.nuspec` souboru přímo z této struktury.</span><span class="sxs-lookup"><span data-stu-id="571a6-170">Because a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension, it's often easiest to create the folder structure you want on your local file system, then create the `.nuspec` file directly from that structure.</span></span> <span data-ttu-id="571a6-171">`nuget pack` Příkaz automaticky přidá všechny soubory v danou strukturu složek (s výjimkou některou ze složek, které začínají `.`, díky tomu můžete zachovat soukromé soubory ve stejné struktuře).</span><span class="sxs-lookup"><span data-stu-id="571a6-171">The `nuget pack` command then automatically adds all files in that folder structure (excluding any folders that begin with `.`, allowing you to keep private files in the same structure).</span></span>

<span data-ttu-id="571a6-172">Výhodou tohoto přístupu je, že nemusíte určit v manifestu soubory, které chcete zahrnout do balíčku (jak je popsáno dále v tomto tématu).</span><span class="sxs-lookup"><span data-stu-id="571a6-172">The advantage to this approach is that you don't need to specify in the manifest which files you want to include in the package (as explained later in this topic).</span></span> <span data-ttu-id="571a6-173">Můžete jednoduše použít proces sestavení vytvořit strukturu přesně složka, která přejdou do balíčku a snadno můžete zahrnout další soubory, které nemusí být součástí projektu jinak:</span><span class="sxs-lookup"><span data-stu-id="571a6-173">You can simply have your build process produce the exact folder structure that goes into the package, and you can easily include other files that might not be part of a project otherwise:</span></span>

- <span data-ttu-id="571a6-174">Obsah a zdrojový kód, který by měl být vloženy do cílový projekt.</span><span class="sxs-lookup"><span data-stu-id="571a6-174">Content and source code that should be injected into the target project.</span></span>
- <span data-ttu-id="571a6-175">Skripty prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="571a6-175">PowerShell scripts</span></span>
- <span data-ttu-id="571a6-176">Transformací do existující konfigurace a soubory zdrojového kódu v projektu.</span><span class="sxs-lookup"><span data-stu-id="571a6-176">Transformations to existing configuration and source code files in a project.</span></span>

<span data-ttu-id="571a6-177">Vytváření složky jsou následující:</span><span class="sxs-lookup"><span data-stu-id="571a6-177">The folder conventions are as follows:</span></span>

| <span data-ttu-id="571a6-178">Folder</span><span class="sxs-lookup"><span data-stu-id="571a6-178">Folder</span></span> | <span data-ttu-id="571a6-179">Popis</span><span class="sxs-lookup"><span data-stu-id="571a6-179">Description</span></span> | <span data-ttu-id="571a6-180">Akce při instalaci balíčku</span><span class="sxs-lookup"><span data-stu-id="571a6-180">Action upon package install</span></span> |
| --- | --- | --- |
| <span data-ttu-id="571a6-181">(uživatel root)</span><span class="sxs-lookup"><span data-stu-id="571a6-181">(root)</span></span> | <span data-ttu-id="571a6-182">Umístění pro soubor readme.txt</span><span class="sxs-lookup"><span data-stu-id="571a6-182">Location for readme.txt</span></span> | <span data-ttu-id="571a6-183">Při instalaci balíčku sady Visual Studio zobrazí soubor readme.txt v kořenovém adresáři balíčku.</span><span class="sxs-lookup"><span data-stu-id="571a6-183">Visual Studio displays a readme.txt file in the package root when the package is installed.</span></span> |
| <span data-ttu-id="571a6-184">lib/{tfm}</span><span class="sxs-lookup"><span data-stu-id="571a6-184">lib/{tfm}</span></span> | <span data-ttu-id="571a6-185">Sestavení (`.dll`), dokumentace ke službě (`.xml`) a symbol (`.pdb`) soubory pro dané cílové rozhraní Framework Moniker (TFM)</span><span class="sxs-lookup"><span data-stu-id="571a6-185">Assembly (`.dll`), documentation (`.xml`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="571a6-186">Sestavení jsou přidány jako odkazy pro kompilaci, jakož i modul runtime; `.xml` a `.pdb` zkopírovány do složky projektu.</span><span class="sxs-lookup"><span data-stu-id="571a6-186">Assemblies are added as references for compile as well as runtime; `.xml` and `.pdb` copied into project folders.</span></span> <span data-ttu-id="571a6-187">Zobrazit [podpora více cílových platforem](supporting-multiple-target-frameworks.md) pro vytvoření dílčí složky specifické pro cílové rozhraní framework.</span><span class="sxs-lookup"><span data-stu-id="571a6-187">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md) for creating framework target-specific sub-folders.</span></span> |
| <span data-ttu-id="571a6-188">REF / {tfm}</span><span class="sxs-lookup"><span data-stu-id="571a6-188">ref/{tfm}</span></span> | <span data-ttu-id="571a6-189">Sestavení (`.dll`) a symbol (`.pdb`) soubory pro dané cílové rozhraní Framework Moniker (TFM)</span><span class="sxs-lookup"><span data-stu-id="571a6-189">Assembly (`.dll`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="571a6-190">Sestavení jsou přidány jako odkazy pouze pro kompilaci; Proto nic budou zkopírovány do složky bin projektu.</span><span class="sxs-lookup"><span data-stu-id="571a6-190">Assemblies are added as references only for compile time; So nothing will be copied into project bin folder.</span></span> |
| <span data-ttu-id="571a6-191">Moduly runtime</span><span class="sxs-lookup"><span data-stu-id="571a6-191">runtimes</span></span> | <span data-ttu-id="571a6-192">Sestavení specifické pro architekturu (`.dll`), symbol (`.pdb`) a nativní prostředky (`.pri`) soubory</span><span class="sxs-lookup"><span data-stu-id="571a6-192">Architecture-specific assembly (`.dll`), symbol (`.pdb`), and native resource (`.pri`) files</span></span> | <span data-ttu-id="571a6-193">Sestavení jsou přidány jako odkazy pouze na modul runtime; Další soubory jsou zkopírovány do složky projektu.</span><span class="sxs-lookup"><span data-stu-id="571a6-193">Assemblies are added as references only for runtime; other files are copied into project folders.</span></span> <span data-ttu-id="571a6-194">By měl vždy být odpovídající (TFM) `AnyCPU` konkrétní sestavení v rámci `/ref/{tfm}` složky zadejte odpovídající sestavení v době kompilace.</span><span class="sxs-lookup"><span data-stu-id="571a6-194">There should always be a corresponding (TFM) `AnyCPU` specific assembly under `/ref/{tfm}` folder to provide corresponding compile time assembly.</span></span> <span data-ttu-id="571a6-195">Zobrazit [podpora více cílových platforem](supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="571a6-195">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md).</span></span> |
| <span data-ttu-id="571a6-196">obsah</span><span class="sxs-lookup"><span data-stu-id="571a6-196">content</span></span> | <span data-ttu-id="571a6-197">Různé soubory</span><span class="sxs-lookup"><span data-stu-id="571a6-197">Arbitrary files</span></span> | <span data-ttu-id="571a6-198">Obsah je zkopírován do kořenového adresáře projektu.</span><span class="sxs-lookup"><span data-stu-id="571a6-198">Contents are copied to the project root.</span></span> <span data-ttu-id="571a6-199">Představte si, že **obsah** složky jako kořen cílové aplikace, takže v konečném důsledku využívajícího balíček.</span><span class="sxs-lookup"><span data-stu-id="571a6-199">Think of the **content** folder as the root of the target application that ultimately consumes the package.</span></span> <span data-ttu-id="571a6-200">Balíček v aplikaci prvku přidat obrázek */obrázky* složku, umístěte ho do balíčku *obsah nebo imagí* složky.</span><span class="sxs-lookup"><span data-stu-id="571a6-200">To have the package add an image in the application's */images* folder, place it in the package's *content/images* folder.</span></span> |
| <span data-ttu-id="571a6-201">sestavení</span><span class="sxs-lookup"><span data-stu-id="571a6-201">build</span></span> | <span data-ttu-id="571a6-202">Nástroj MSBuild `.targets` a `.props` soubory</span><span class="sxs-lookup"><span data-stu-id="571a6-202">MSBuild `.targets` and `.props` files</span></span> | <span data-ttu-id="571a6-203">Automaticky vložit do souboru projektu nebo `project.lock.json` (NuGet 3.x+).</span><span class="sxs-lookup"><span data-stu-id="571a6-203">Automatically inserted into the project file or `project.lock.json` (NuGet 3.x+).</span></span> |
| <span data-ttu-id="571a6-204">nástroje</span><span class="sxs-lookup"><span data-stu-id="571a6-204">tools</span></span> | <span data-ttu-id="571a6-205">Skripty prostředí PowerShell a programy, které jsou přístupné z konzole Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="571a6-205">Powershell scripts and programs accessible from the Package Manager Console</span></span> | <span data-ttu-id="571a6-206">`tools` Složka je přidána do `PATH` proměnné prostředí pro konzolu Správce balíčků (konkrétně *není* k `PATH` jako sada pro nástroje MSBuild při sestavování projektu).</span><span class="sxs-lookup"><span data-stu-id="571a6-206">The `tools` folder is added to the `PATH` environment variable for the Package Manager Console only (Specifically, *not* to the `PATH` as set for MSBuild when building the project).</span></span> |

<span data-ttu-id="571a6-207">Protože vaše struktura složky může obsahovat libovolný počet sestavení pro libovolný počet cílových platforem, tato metoda je nezbytná, při vytváření balíčků, které podporují více platforem.</span><span class="sxs-lookup"><span data-stu-id="571a6-207">Because your folder structure can contain any number of assemblies for any number of target frameworks, this method is necessary when creating packages that support multiple frameworks.</span></span>

<span data-ttu-id="571a6-208">V každém případě až budete mít struktuře požadované složky na místě, spusťte následující příkaz v této složce vytvořte `.nuspec` souboru:</span><span class="sxs-lookup"><span data-stu-id="571a6-208">In any case, once you have the desired folder structure in place, run the following command in that folder to create the `.nuspec` file:</span></span>

```cli
nuget spec
```

<span data-ttu-id="571a6-209">Znovu, vygenerované `.nuspec` neobsahuje žádné explicitní odkazy na soubory v této struktuře.</span><span class="sxs-lookup"><span data-stu-id="571a6-209">Again, the generated `.nuspec` contains no explicit references to files in the folder structure.</span></span> <span data-ttu-id="571a6-210">NuGet automaticky obsahuje všechny soubory, když se balíček vytvoří.</span><span class="sxs-lookup"><span data-stu-id="571a6-210">NuGet automatically includes all files when the package is created.</span></span> <span data-ttu-id="571a6-211">Nevyhnete se ale upravit zástupné hodnoty v ostatních částech v manifestu.</span><span class="sxs-lookup"><span data-stu-id="571a6-211">You still need to edit placeholder values in other parts of the manifest, however.</span></span>

### <a name="from-an-assembly-dll"></a><span data-ttu-id="571a6-212">Ze sestavení knihovny DLL</span><span class="sxs-lookup"><span data-stu-id="571a6-212">From an assembly DLL</span></span>

<span data-ttu-id="571a6-213">V jednoduchém případě vytvoření balíčku ze sestavení, můžete vygenerovat `.nuspec` soubor z metadat sestavení pomocí následujícího příkazu:</span><span class="sxs-lookup"><span data-stu-id="571a6-213">In the simple case of creating a package from an assembly, you can generate a `.nuspec` file from the metadata in the assembly using the following command:</span></span>

```cli
nuget spec <assembly-name>.dll
```

<span data-ttu-id="571a6-214">Použití této formy nahradí několik zástupných symbolů v manifestu konkrétní hodnoty ze sestavení.</span><span class="sxs-lookup"><span data-stu-id="571a6-214">Using this form replaces a few placeholders in the manifest with specific values from the assembly.</span></span> <span data-ttu-id="571a6-215">Například `<id>` je nastavena na název sestavení, a `<version>` je nastavené na verzi sestavení.</span><span class="sxs-lookup"><span data-stu-id="571a6-215">For example, the `<id>` property is set to the assembly name, and `<version>` is set to the assembly version.</span></span> <span data-ttu-id="571a6-216">Další vlastnosti v manifestu, ale nepoužíváte porovnání hodnot v sestavení a stále tedy obsahovaly zástupné symboly.</span><span class="sxs-lookup"><span data-stu-id="571a6-216">Other properties in the manifest, however, don't have matching values in the assembly and thus still contain placeholders.</span></span>

### <a name="from-a-visual-studio-project"></a><span data-ttu-id="571a6-217">Z projektu sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="571a6-217">From a Visual Studio project</span></span>

<span data-ttu-id="571a6-218">Vytváření `.nuspec` z `.csproj` nebo `.vbproj` souboru je pohodlné, protože další balíčky, které byly nainstalovány do těchto projektu jsou automaticky odkazována jako závislosti.</span><span class="sxs-lookup"><span data-stu-id="571a6-218">Creating a `.nuspec` from a `.csproj` or `.vbproj` file is convenient because other packages that have been installed into those project are automatically referenced as dependencies.</span></span> <span data-ttu-id="571a6-219">Jednoduše použijte následující příkaz ve stejné složce jako soubor projektu:</span><span class="sxs-lookup"><span data-stu-id="571a6-219">Simply use the following command in the same folder as the project file:</span></span>

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

<span data-ttu-id="571a6-220">Výsledná `<project-name>.nuspec` soubor obsahuje *tokeny* , která se nahradí v době vytváření balíčků hodnotami z projektu, včetně odkazů na další balíčky, které jsou již nainstalovány.</span><span class="sxs-lookup"><span data-stu-id="571a6-220">The resulting `<project-name>.nuspec` file contains *tokens* that are replaced at packaging time with values from the project, including references to any other packages that have already been installed.</span></span>

<span data-ttu-id="571a6-221">Token je oddělen složenými `$` symboly na obou stranách vlastnosti projektu.</span><span class="sxs-lookup"><span data-stu-id="571a6-221">A token is delimited by `$` symbols on both sides of the project property.</span></span> <span data-ttu-id="571a6-222">Například `<id>` hodnota v manifestu generované v tomto stejně, jako obvykle se zobrazí takto:</span><span class="sxs-lookup"><span data-stu-id="571a6-222">For example, the `<id>` value in a manifest generated in this way typically appears as follows:</span></span>

```xml
<id>$id$</id>
```

<span data-ttu-id="571a6-223">Tento token nahrazen `AssemblyName` hodnotu ze souboru projektu v balení čas.</span><span class="sxs-lookup"><span data-stu-id="571a6-223">This token is replaced with the `AssemblyName` value from the project file at packing time.</span></span> <span data-ttu-id="571a6-224">Pro přesné mapování hodnot projektu k `.nuspec` tokeny, najdete v článku [odkazovat na náhradní tokeny](../reference/nuspec.md#replacement-tokens).</span><span class="sxs-lookup"><span data-stu-id="571a6-224">For the exact mapping of project values to `.nuspec` tokens, see the [Replacement Tokens reference](../reference/nuspec.md#replacement-tokens).</span></span>

<span data-ttu-id="571a6-225">Tokeny můžete snížit z by bylo potřeba aktualizovat klíčové hodnoty jako číslo verze v `.nuspec` při aktualizaci projektu.</span><span class="sxs-lookup"><span data-stu-id="571a6-225">Tokens relieve you from needing to update crucial values like the version number in the `.nuspec` as you update the project.</span></span> <span data-ttu-id="571a6-226">(Můžete vždy nahradit tokeny literálových hodnot v případě potřeby).</span><span class="sxs-lookup"><span data-stu-id="571a6-226">(You can always replace the tokens with literal values, if desired).</span></span> 

<span data-ttu-id="571a6-227">Všimněte si, že existuje několik dalších balení možností k dispozici při práci v projektu sady Visual Studio, jak je popsáno v [spuštění balíčku nuget pro generování souboru .nupkg](#running-nuget-pack-to-generate-the-nupkg-file) později.</span><span class="sxs-lookup"><span data-stu-id="571a6-227">Note that there are several additional packaging options available when working from a Visual Studio project, as described in [Running nuget pack to generate the .nupkg file](#running-nuget-pack-to-generate-the-nupkg-file) later on.</span></span>

#### <a name="solution-level-packages"></a><span data-ttu-id="571a6-228">Balíčky na úrovni řešení</span><span class="sxs-lookup"><span data-stu-id="571a6-228">Solution-level packages</span></span>

<span data-ttu-id="571a6-229">*NuGet 2.x pouze. Ve Správci NuGet 3.0 není k dispozici.*</span><span class="sxs-lookup"><span data-stu-id="571a6-229">*NuGet 2.x only. Not available in NuGet 3.0+.*</span></span>

<span data-ttu-id="571a6-230">NuGet 2.x nepodporuje rozeznávání úrovni řešení balíček, který nainstaluje nástroje nebo další příkazy pro konzolu Správce balíčků (obsah `tools` složky), ale přidejte odkazy na obsah, nebo vlastní nastavení pro všechny projekty v sestavení řešení.</span><span class="sxs-lookup"><span data-stu-id="571a6-230">NuGet 2.x supported the notion of a solution-level package that installs tools or additional commands for the Package Manager Console (the contents of the `tools` folder), but does not add references, content, or build customizations to any projects in the solution.</span></span> <span data-ttu-id="571a6-231">Tyto balíčky obsahují žádné soubory v její přímé `lib`, `content`, nebo `build` složky a žádný z jejích závislostí mít soubory v jejich `lib`, `content`, nebo `build` složky.</span><span class="sxs-lookup"><span data-stu-id="571a6-231">Such packages contain no files in its direct `lib`, `content`, or `build` folders, and none of its dependencies have files in their respective `lib`, `content`, or `build` folders.</span></span>

<span data-ttu-id="571a6-232">Sleduje NuGet, nainstalované balíčky úrovni řešení v `packages.config` ve `.nuget` složky, nikoli projektu `packages.config` souboru.</span><span class="sxs-lookup"><span data-stu-id="571a6-232">NuGet tracks installed solution-level packages in a `packages.config` file in the `.nuget` folder, rather than the project's `packages.config` file.</span></span>

### <a name="new-file-with-default-values"></a><span data-ttu-id="571a6-233">Nový soubor s výchozími hodnotami.</span><span class="sxs-lookup"><span data-stu-id="571a6-233">New file with default values</span></span>

<span data-ttu-id="571a6-234">Následující příkaz vytvoří výchozí manifest se zástupnými symboly, které zajistí, že začnete s správná struktura:</span><span class="sxs-lookup"><span data-stu-id="571a6-234">The following command creates a default manifest with placeholders, which ensures you start with the proper file structure:</span></span>

```cli
nuget spec [<package-name>]
```

<span data-ttu-id="571a6-235">Vynecháte-li \<název balíčku\>, je výsledný soubor `Package.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="571a6-235">If you omit \<package-name\>, the resulting file is `Package.nuspec`.</span></span> <span data-ttu-id="571a6-236">Pokud je třeba zadat název `Contoso.Utility.UsefulStuff`, soubor je `Contoso.Utility.UsefulStuff.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="571a6-236">If you provide a name such as `Contoso.Utility.UsefulStuff`, the file is `Contoso.Utility.UsefulStuff.nuspec`.</span></span>

<span data-ttu-id="571a6-237">Výsledná `.nuspec` obsahuje zástupné symboly pro hodnoty, jako jsou `projectUrl`.</span><span class="sxs-lookup"><span data-stu-id="571a6-237">The resulting `.nuspec` contains placeholders for values like the `projectUrl`.</span></span> <span data-ttu-id="571a6-238">Ujistěte se, než je použijete k vytvoření poslední úpravy souboru `.nupkg` souboru.</span><span class="sxs-lookup"><span data-stu-id="571a6-238">Be sure to edit the file before using it to create the final `.nupkg` file.</span></span>

## <a name="choosing-a-unique-package-identifier-and-setting-the-version-number"></a><span data-ttu-id="571a6-239">Výběr balíčku jedinečný identifikátor a nastaví číslo verze</span><span class="sxs-lookup"><span data-stu-id="571a6-239">Choosing a unique package identifier and setting the version number</span></span>

<span data-ttu-id="571a6-240">Identifikátor balíčku (`<id>` element) a číslo verze (`<version>` element) jsou dvě nejdůležitější hodnoty v manifestu, protože jednoznačně identifikují přesný kód, který je součástí balíčku.</span><span class="sxs-lookup"><span data-stu-id="571a6-240">The package identifier (`<id>` element) and the version number (`<version>` element) are the two most important values in the manifest because they uniquely identify the exact code that's contained in the package.</span></span>

<span data-ttu-id="571a6-241">**Osvědčené postupy pro identifikátor balíčku:**</span><span class="sxs-lookup"><span data-stu-id="571a6-241">**Best practices for the package identifier:**</span></span>

- <span data-ttu-id="571a6-242">**Jedinečnost**: Identifikátor musí být jedinečný mezi nuget.org nebo libovolné galerii hostitelem balíčku.</span><span class="sxs-lookup"><span data-stu-id="571a6-242">**Uniqueness**: The identifier must be unique across nuget.org or whatever gallery hosts the package.</span></span> <span data-ttu-id="571a6-243">Než se rozhodnete u identifikátoru Prohledat galerii použít ke kontrole, zda název je již používán.</span><span class="sxs-lookup"><span data-stu-id="571a6-243">Before deciding on an identifier, search the applicable gallery to check if the name is already in use.</span></span> <span data-ttu-id="571a6-244">Aby nedocházelo ke konfliktům, je použít název vaší společnosti jako první část identifikátoru, jako dobrý vzorek `Contoso.`.</span><span class="sxs-lookup"><span data-stu-id="571a6-244">To avoid conflicts, a good pattern is to use your company name as the first part of the identifier, such as `Contoso.`.</span></span>
- <span data-ttu-id="571a6-245">**Namespace jako názvy**: Postupujte podle vzoru podobný obory názvů v rozhraní .NET, pomocí zápisu s tečkou místo pomlčky.</span><span class="sxs-lookup"><span data-stu-id="571a6-245">**Namespace-like names**: Follow a pattern similar to namespaces in .NET, using dot notation instead of hyphens.</span></span> <span data-ttu-id="571a6-246">Například použít `Contoso.Utility.UsefulStuff` spíše než `Contoso-Utility-UsefulStuff` nebo `Contoso_Utility_UsefulStuff`.</span><span class="sxs-lookup"><span data-stu-id="571a6-246">For example, use `Contoso.Utility.UsefulStuff` rather than `Contoso-Utility-UsefulStuff` or `Contoso_Utility_UsefulStuff`.</span></span> <span data-ttu-id="571a6-247">Příjemci také užitečné, když identifikátor balíčku shoduje s obory názvů používané v kódu.</span><span class="sxs-lookup"><span data-stu-id="571a6-247">Consumers also find it helpful when the package identifier matches the namespaces used in the code.</span></span>
- <span data-ttu-id="571a6-248">**Ukázkové balíčky**: Pokud možno vytvořit balíček ukázek kódu, který ukazuje, jak použít jiný balíček, připojit `.Sample` jako příponu k identifikátoru, jako v `Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="571a6-248">**Sample Packages**: If you produce a package of sample code that demonstrates how to use another package, attach `.Sample` as a suffix to the identifier, as in `Contoso.Utility.UsefulStuff.Sample`.</span></span> <span data-ttu-id="571a6-249">(Ukázkového balíčku by samozřejmě mít závislost na jiný balíček.) Při vytváření balíčku vzorku, použijte podle úmluvy pracovní adresář metody popsané dříve.</span><span class="sxs-lookup"><span data-stu-id="571a6-249">(The sample package would of course have a dependency on the other package.) When creating a sample package, use the convention-based working directory method described earlier.</span></span> <span data-ttu-id="571a6-250">V `content` složky, uspořádat ukázkový kód do složky s názvem `\Samples\<identifier>` stejně jako v `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="571a6-250">In the `content` folder, arrange the sample code in a folder called `\Samples\<identifier>` as in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span></span>

<span data-ttu-id="571a6-251">**Osvědčené postupy pro verze balíčku:**</span><span class="sxs-lookup"><span data-stu-id="571a6-251">**Best practices for the package version:**</span></span>

- <span data-ttu-id="571a6-252">Obecně platí nastavte verzi balíčku tak, aby odpovídaly knihovny, i když to není nezbytně nutné.</span><span class="sxs-lookup"><span data-stu-id="571a6-252">In general, set the version of the package to match the library, though this is not strictly required.</span></span> <span data-ttu-id="571a6-253">Toto je jednoduché když omezíte balíčku do jednoho sestavení, jak je popsáno výše v [rozhodování o tom, která sestavení do balíčku](#deciding-which-assemblies-to-package).</span><span class="sxs-lookup"><span data-stu-id="571a6-253">This is a simple matter when you limit a package to a single assembly, as described earlier in [Deciding which assemblies to package](#deciding-which-assemblies-to-package).</span></span> <span data-ttu-id="571a6-254">Celkově nezapomeňte, že NuGet, samotné se zabývá verze balíčků při řešení závislostí, nikoli verze sestavení.</span><span class="sxs-lookup"><span data-stu-id="571a6-254">Overall, remember that NuGet itself deals with package versions when resolving dependencies, not assembly versions.</span></span>
- <span data-ttu-id="571a6-255">Při použití schématu nestandardní verze, být potřeba vzít v úvahu pravidla NuGet správy verzí, jak je vysvětleno v [Správa verzí balíčků](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="571a6-255">When using a non-standard version scheme, be sure to consider the NuGet versioning rules as explained in [Package versioning](../reference/package-versioning.md).</span></span>

> <span data-ttu-id="571a6-256">Následující řadu stručný blogové příspěvky jsou také užitečné k pochopení správy verzí:</span><span class="sxs-lookup"><span data-stu-id="571a6-256">The following series of brief blog posts are also helpful to understand versioning:</span></span>
>
> - [<span data-ttu-id="571a6-257">Část 1: S ohledem na knihoven DLL</span><span class="sxs-lookup"><span data-stu-id="571a6-257">Part 1: Taking on DLL Hell</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [<span data-ttu-id="571a6-258">Část 2: Základní algoritmus</span><span class="sxs-lookup"><span data-stu-id="571a6-258">Part 2: The core algorithm</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [<span data-ttu-id="571a6-259">3. část: Sjednocení prostřednictvím přesměrování vazeb</span><span class="sxs-lookup"><span data-stu-id="571a6-259">Part 3: Unification via Binding Redirects</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="setting-a-package-type"></a><span data-ttu-id="571a6-260">Nastavení typ balíčku</span><span class="sxs-lookup"><span data-stu-id="571a6-260">Setting a package type</span></span>

<span data-ttu-id="571a6-261">Nuget 3.5 +, může být označený balíčky s konkrétním *typ balíčku* označující jeho zamýšlené použití.</span><span class="sxs-lookup"><span data-stu-id="571a6-261">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="571a6-262">Balíčky není označena jako s typem, včetně všech balíčků, které jsou vytvořené pomocí starší verze balíčku nuget, ve výchozím nastavení `Dependency` typu.</span><span class="sxs-lookup"><span data-stu-id="571a6-262">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="571a6-263">`Dependency` balíčky typ sestavení nebo runtime prostředky přidat do knihovny a aplikace a může být nainstalován v libovolným typem projektu (za předpokladu, že jsou kompatibilní).</span><span class="sxs-lookup"><span data-stu-id="571a6-263">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="571a6-264">`DotnetCliTool` Typ balíčky jsou rozšíření [.NET CLI](/dotnet/articles/core/tools/index) a jsou vyvolány z příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="571a6-264">`DotnetCliTool` type packages are extensions to the [.NET CLI](/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="571a6-265">Tyto balíčky můžete nainstalovat jenom v projektech .NET Core a nemají žádný vliv na operace obnovení.</span><span class="sxs-lookup"><span data-stu-id="571a6-265">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="571a6-266">Další podrobnosti o těchto rozšířeních jednotlivých projektů jsou dostupné v [rozšiřitelnost .NET Core](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) dokumentaci.</span><span class="sxs-lookup"><span data-stu-id="571a6-266">More details about these per-project extensions are available in the  [.NET Core extensibility](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

- <span data-ttu-id="571a6-267">Vlastní typ balíčky pomocí libovolného typu identifikátor, který odpovídá stejná pravidla formát jako ID balíčku.</span><span class="sxs-lookup"><span data-stu-id="571a6-267">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="571a6-268">Jakýkoli typ jiný než `Dependency` a `DotnetCliTool`, ale nejsou rozpoznány v aplikaci Správce balíčků NuGet v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="571a6-268">Any type other than `Dependency` and `DotnetCliTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="571a6-269">Typy balíčků jsou nastaveny `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="571a6-269">Package types are set in the `.nuspec` file.</span></span> <span data-ttu-id="571a6-270">Je nejvhodnější pro zpětnou kompatibilitu s *není* explicitně nastaveno `Dependency` zadejte a místo toho přináší setrvávání u NuGet tohoto typu, pokud žádný typ za předpokladu, že je zadán.</span><span class="sxs-lookup"><span data-stu-id="571a6-270">It's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="571a6-271">`.nuspec`: Označuje typ balíčku v rámci `packageTypes\packageType` pod uzlem `<metadata>` element:</span><span class="sxs-lookup"><span data-stu-id="571a6-271">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

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

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="571a6-272">Přidání souboru readme a další soubory</span><span class="sxs-lookup"><span data-stu-id="571a6-272">Adding a readme and other files</span></span>

<span data-ttu-id="571a6-273">Pokud chcete přímo zadat soubory, které chcete zahrnout do balíčku, použijte `<files>` uzlu v `.nuspec` souboru, který *následuje* `<metadata>` značky:</span><span class="sxs-lookup"><span data-stu-id="571a6-273">To directly specify files to include in the package, use the `<files>` node in the `.nuspec` file, which *follows* the `<metadata>` tag:</span></span>

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
> <span data-ttu-id="571a6-274">Při použití přístup podle úmluvy pracovní adresář, můžete umístit readme.txt ve svém kořenu a další obsah `content` složky.</span><span class="sxs-lookup"><span data-stu-id="571a6-274">When using the convention-based working directory approach, you can place the readme.txt in the package root and other content in the `content` folder.</span></span> <span data-ttu-id="571a6-275">Ne `<file>` prvky jsou nezbytné v manifestu.</span><span class="sxs-lookup"><span data-stu-id="571a6-275">No `<file>` elements are necessary in the manifest.</span></span>

<span data-ttu-id="571a6-276">Pokud zahrnete soubor s názvem `readme.txt` v kořenovém adresáři balíčku sady Visual Studio zobrazí obsah tohoto souboru jako prostý text okamžitě po instalaci balíčku přímo.</span><span class="sxs-lookup"><span data-stu-id="571a6-276">When you include a file named `readme.txt` in the package root, Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="571a6-277">(Soubory Readme nejsou zobrazeny pro balíčky nainstalované jako závislosti).</span><span class="sxs-lookup"><span data-stu-id="571a6-277">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="571a6-278">Tady je například jak se zobrazí v souboru readme HtmlAgilityPack balíčku:</span><span class="sxs-lookup"><span data-stu-id="571a6-278">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Zobrazit soubor readme pro balíček NuGet při instalaci](media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="571a6-280">Zadáte-li prázdné `<files>` uzlu `.nuspec` souboru NuGet neobsahuje žádný jiný obsah v balíčku, než co je v `lib` složky.</span><span class="sxs-lookup"><span data-stu-id="571a6-280">If you include an empty `<files>` node in the `.nuspec` file, NuGet doesn't include any other content in the package other than what's in the `lib` folder.</span></span>

## <a name="including-msbuild-props-and-targets-in-a-package"></a><span data-ttu-id="571a6-281">Včetně cíle a vlastnosti nástroje MSBuild v balíčku</span><span class="sxs-lookup"><span data-stu-id="571a6-281">Including MSBuild props and targets in a package</span></span>

<span data-ttu-id="571a6-282">V některých případech můžete chtít přidat vlastní sestavení cíle nebo vlastnosti v projektech, které využívají vašeho balíčku, například spuštěním vlastní nástroje nebo procesu během sestavování.</span><span class="sxs-lookup"><span data-stu-id="571a6-282">In some cases, you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="571a6-283">To provedete tak, že soubory ve formě `<package_id>.targets` nebo `<package_id>.props` (například `Contoso.Utility.UsefulStuff.targets`) v rámci `\build` složky projektu.</span><span class="sxs-lookup"><span data-stu-id="571a6-283">You do this by placing files in the form `<package_id>.targets` or `<package_id>.props` (such as `Contoso.Utility.UsefulStuff.targets`) within the `\build` folder of the project.</span></span>

<span data-ttu-id="571a6-284">Soubory v kořenové složce `\build` složky jsou považovány za vhodný pro všechny cílové architektury.</span><span class="sxs-lookup"><span data-stu-id="571a6-284">Files in the root `\build` folder are considered suitable for all target frameworks.</span></span> <span data-ttu-id="571a6-285">Pro poskytování souborů specifické pro architekturu, nejprve umístíte do příslušné podsložky, jako je následující:</span><span class="sxs-lookup"><span data-stu-id="571a6-285">To provide framework-specific files, first place them within appropriate subfolders, such as the following:</span></span>

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

<span data-ttu-id="571a6-286">Potom v `.nuspec` souboru, je nutné k odkazování na tyto soubory `<files>` uzlu:</span><span class="sxs-lookup"><span data-stu-id="571a6-286">Then in the `.nuspec` file, be sure to refer to these files in the `<files>` node:</span></span>

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

<span data-ttu-id="571a6-287">Včetně cíle a vlastnosti nástroje MSBuild v balíčku byl [představeny s nástrojem NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), proto se doporučuje přidat `minClientVersion="2.5"` atribut `metadata` element označující minimální verzi klienta NuGet potřeba využívat balíček.</span><span class="sxs-lookup"><span data-stu-id="571a6-287">Including MSBuild props and targets in a package was [introduced with NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), therefore it is recommended to add the `minClientVersion="2.5"` attribute to the `metadata` element, to indicate the minimum NuGet client version required to consume the package.</span></span>

<span data-ttu-id="571a6-288">Po instalaci balíček NuGet `\build` soubory, přidá MSBuild `<Import>` elementy v souboru projektu, přejdete `.targets` a `.props` soubory.</span><span class="sxs-lookup"><span data-stu-id="571a6-288">When NuGet installs a package with `\build` files, it adds MSBuild `<Import>` elements in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="571a6-289">(`.props` je přidán v horní části souboru projektu. `.targets` je přidán v dolní části.) Samostatné podmíněné MSBuild `<Import>` prvek přidán pro každou cílovou architekturu.</span><span class="sxs-lookup"><span data-stu-id="571a6-289">(`.props` is added at the top of the project file; `.targets` is added at the bottom.) A separate conditional MSBuild `<Import>` element is added for each target framework.</span></span>

<span data-ttu-id="571a6-290">Nástroj MSBuild `.props` a `.targets` soubory pro cílení na různé architektury je možné umístit `\buildMultiTargeting` složky.</span><span class="sxs-lookup"><span data-stu-id="571a6-290">MSBuild `.props` and `.targets` files for cross-framework targeting can be placed in the `\buildMultiTargeting` folder.</span></span> <span data-ttu-id="571a6-291">Během instalace balíčku NuGet přidá odpovídající `<Import>` prvků, které se soubor projektu s podmínkou, která Cílová architektura, která není nastavena (vlastnost MSBuild `$(TargetFramework)` musí být prázdný).</span><span class="sxs-lookup"><span data-stu-id="571a6-291">During package installation, NuGet adds the corresponding `<Import>` elements to the project file with the condition, that the target framework is not set (the MSBuild property `$(TargetFramework)` must be empty).</span></span>

<span data-ttu-id="571a6-292">Nuget 3.x cíle nebyly přidány do projektu, ale místo toho jsou k dispozici prostřednictvím `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="571a6-292">With NuGet 3.x, targets are not added to the project but are instead made available through the `project.lock.json`.</span></span>

## <a name="authoring-packages-with-com-interop-assemblies"></a><span data-ttu-id="571a6-293">Vytváření balíčků pomocí sestavení vzájemné spolupráce COM</span><span class="sxs-lookup"><span data-stu-id="571a6-293">Authoring packages with COM interop assemblies</span></span>

<span data-ttu-id="571a6-294">Balíčky, které obsahují sestavení vzájemné spolupráce COM musí obsahovat odpovídající [soubor cílů](#including-msbuild-props-and-targets-in-a-package) tak, aby správné `EmbedInteropTypes` do projektů s použitím formátu PackageReference se přidají metadata.</span><span class="sxs-lookup"><span data-stu-id="571a6-294">Packages that contain COM interop assemblies must include an appropriate [targets file](#including-msbuild-props-and-targets-in-a-package) so that the correct `EmbedInteropTypes` metadata is added to projects using the PackageReference format.</span></span> <span data-ttu-id="571a6-295">Ve výchozím nastavení `EmbedInteropTypes` metadat má vždy hodnotu false pro všechna sestavení zadáním PackageReference tak soubor cílů přidá tato metadata explicitně.</span><span class="sxs-lookup"><span data-stu-id="571a6-295">By default, the `EmbedInteropTypes` metadata is always false for all assemblies when PackageReference is used, so the targets file adds this metadata explicitly.</span></span> <span data-ttu-id="571a6-296">Aby nedocházelo ke konfliktům, cílový název by měl být jedinečný; v ideálním případě by použít kombinaci váš název balíčku a sestavení jsou vložené a nahraďte `{InteropAssemblyName}` v níže uvedeném příkladu s danou hodnotou.</span><span class="sxs-lookup"><span data-stu-id="571a6-296">To avoid conflicts, the target name should be unique; ideally, use a combination of your package name and the assembly being embedded, replacing the `{InteropAssemblyName}` in the example below with that value.</span></span> <span data-ttu-id="571a6-297">(Viz také [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) příklad.)</span><span class="sxs-lookup"><span data-stu-id="571a6-297">(Also see [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) for an example.)</span></span>

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

<span data-ttu-id="571a6-298">Všimněte si, že při použití `packages.config` formátu správy přidávání odkazů na sestavení z balíčků způsobí, že NuGet a sady Visual Studio vyhledat sestavení vzájemné spolupráce COM a nastavit `EmbedInteropTypes` na hodnotu true v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="571a6-298">Note that when using the `packages.config` management format, adding references to the assemblies from the packages causes NuGet and Visual Studio to check for COM interop assemblies and set the `EmbedInteropTypes` to true in the project file.</span></span> <span data-ttu-id="571a6-299">V tomto případě cíle, které jsou přepsaný.</span><span class="sxs-lookup"><span data-stu-id="571a6-299">In this case the targets are overriden.</span></span>

<span data-ttu-id="571a6-300">Kromě toho ve výchozím nastavení [tok prostředky sestavení není přechodně](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="571a6-300">Additionally, by default the [build assets do not flow transitively](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span> <span data-ttu-id="571a6-301">Balíčky vytvořené podle postupu popsaného tady pracovní odlišně při se berou jako přechodné závislosti z odkazu typu projekt na projekt.</span><span class="sxs-lookup"><span data-stu-id="571a6-301">Packages authored as described here work differently when they are pulled as a transitive dependency from a project to project reference.</span></span> <span data-ttu-id="571a6-302">Příjemce balíčku můžete zajistí, aby tok tak, že upravíte výchozí hodnotu PrivateAssets tak, aby nezahrnovala sestavení.</span><span class="sxs-lookup"><span data-stu-id="571a6-302">The package consumer can allow them to flow by modifying the PrivateAssets default value to not include build.</span></span>

<a name="creating-the-package"></a>

## <a name="running-nuget-pack-to-generate-the-nupkg-file"></a><span data-ttu-id="571a6-303">Spuštění balíčku nuget pro generování souboru .nupkg</span><span class="sxs-lookup"><span data-stu-id="571a6-303">Running nuget pack to generate the .nupkg file</span></span>

<span data-ttu-id="571a6-304">Při použití sestavení nebo pracovního adresáře založené na konvenci, vytvořit balíček spuštěním `nuget pack` s vaší `.nuspec` souboru, nahradí `<project-name>` s vaší konkrétní název souboru:</span><span class="sxs-lookup"><span data-stu-id="571a6-304">When using an assembly or the convention-based working directory, create a package by running `nuget pack` with your `.nuspec` file, replacing `<project-name>` with your specific filename:</span></span>

```cli
nuget pack <project-name>.nuspec
```

<span data-ttu-id="571a6-305">Při použití projektu sady Visual Studio, spusťte `nuget pack` pomocí souboru projektu, který automaticky načte projektu `.nuspec` souboru a nahradí všechny tokeny pomocí hodnot v souboru projektu:</span><span class="sxs-lookup"><span data-stu-id="571a6-305">When using a Visual Studio project, run `nuget pack` with your project file, which automatically loads the project's `.nuspec` file and replaces any tokens within it using values in the project file:</span></span>

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> <span data-ttu-id="571a6-306">Přímo pomocí souboru projektu je nezbytné pro nahrazování tokenů, protože projekt je zdrojové hodnoty tokenu.</span><span class="sxs-lookup"><span data-stu-id="571a6-306">Using the project file directly is necessary for token replacement because the project is the source of the token values.</span></span> <span data-ttu-id="571a6-307">Nahrazování tokenů neodehrává používáte `nuget pack` s `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="571a6-307">Token replacement does not happen if you use `nuget pack` with a `.nuspec` file.</span></span>

<span data-ttu-id="571a6-308">Ve všech případech `nuget pack` vyloučí složek, které začínají tečkou, jako například `.git` nebo `.hg`.</span><span class="sxs-lookup"><span data-stu-id="571a6-308">In all cases, `nuget pack` excludes folders that start with a period, such as `.git` or `.hg`.</span></span>

<span data-ttu-id="571a6-309">NuGet uvádí, jestli jsou všechny chyby `.nuspec` soubor, který vyžadují opravu, jako je například zapomínání Chcete-li změnit hodnoty zástupných symbolů v manifestu.</span><span class="sxs-lookup"><span data-stu-id="571a6-309">NuGet indicates if there are any errors in the `.nuspec` file that need correcting, such as forgetting to change placeholder values in the manifest.</span></span>

<span data-ttu-id="571a6-310">Jednou `nuget pack` proběhne úspěšně, je nutné `.nupkg` souborů, které můžete publikovat do vhodný galerie, jak je popsáno v [publikování balíčku](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="571a6-310">Once `nuget pack` succeeds, you have a `.nupkg` file that you can publish to a suitable gallery as described in [Publishing a Package](../create-packages/publish-a-package.md).</span></span>

> [!Tip]
> <span data-ttu-id="571a6-311">Užitečný způsob, jak prozkoumat balíčku po jeho vytvoření je otevřít v [Průzkumníku balíčků](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) nástroj.</span><span class="sxs-lookup"><span data-stu-id="571a6-311">A helpful way to examine a package after creating it is to open it in the [Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) tool.</span></span> <span data-ttu-id="571a6-312">To poskytuje grafické zobrazení obsahu balíčku a jeho manifestu.</span><span class="sxs-lookup"><span data-stu-id="571a6-312">This gives you a graphical view of the package contents and its manifest.</span></span> <span data-ttu-id="571a6-313">Můžete také přejmenovat, výsledná `.nupkg` do souboru `.zip` soubor a seznamte se s jeho obsahem přímo.</span><span class="sxs-lookup"><span data-stu-id="571a6-313">You can also rename the resulting `.nupkg` file to a `.zip` file and explore its contents directly.</span></span>

### <a name="additional-options"></a><span data-ttu-id="571a6-314">Další možnosti</span><span class="sxs-lookup"><span data-stu-id="571a6-314">Additional options</span></span>

<span data-ttu-id="571a6-315">Můžete použít různé přepínače příkazového řádku s `nuget pack` vyloučit soubory, přepíše číslo verze v manifestu a změňte výstupní složky, kromě jiných funkcí.</span><span class="sxs-lookup"><span data-stu-id="571a6-315">You can use various command-line switches with `nuget pack` to exclude files, override the version number in the manifest, and change the output folder, among other features.</span></span> <span data-ttu-id="571a6-316">Úplný seznam najdete [pack informace o příkazech](../tools/cli-ref-pack.md).</span><span class="sxs-lookup"><span data-stu-id="571a6-316">For a complete list, refer to the [pack command reference](../tools/cli-ref-pack.md).</span></span>

<span data-ttu-id="571a6-317">Několik, která jsou běžné u projektů sady Visual Studio jsou následující možnosti:</span><span class="sxs-lookup"><span data-stu-id="571a6-317">The following options are a few that are common with Visual Studio projects:</span></span>

- <span data-ttu-id="571a6-318">**Odkazované projekty**: Pokud projekt odkazuje na jiné projekty, můžete přidat odkazované projekty v rámci balíčku, nebo jako závislosti, s použitím `-IncludeReferencedProjects` možnost:</span><span class="sxs-lookup"><span data-stu-id="571a6-318">**Referenced projects**: If the project references other projects, you can add the referenced projects as part of the package, or as dependencies, by using the `-IncludeReferencedProjects` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    <span data-ttu-id="571a6-319">Tento proces zařazení je rekurzivní, pokud tedy `MyProject.csproj` odkazy na projekty B a C a projekty odkazovat D, E a F a soubory z B, C, D, E a F jsou součástí balíčku.</span><span class="sxs-lookup"><span data-stu-id="571a6-319">This inclusion process is recursive, so if `MyProject.csproj` references projects B and C, and those projects reference D, E, and F, then files from B, C, D, E, and F are included in the package.</span></span>

    <span data-ttu-id="571a6-320">Pokud obsahuje odkazovaný projekt `.nuspec` soubor sama, pak NuGet přidá tento Odkazovaný projekt jako závislost místo.</span><span class="sxs-lookup"><span data-stu-id="571a6-320">If a referenced project includes a `.nuspec` file of its own, then NuGet adds that referenced project as a dependency instead.</span></span>  <span data-ttu-id="571a6-321">Budete muset balíček a publikujte tento projekt samostatně.</span><span class="sxs-lookup"><span data-stu-id="571a6-321">You need to package and publish that project separately.</span></span>

- <span data-ttu-id="571a6-322">**Konfigurace sestavení**: Standardně používá NuGet výchozí konfigurace sestavení, nastavte v souboru projektu, obvykle *ladění*.</span><span class="sxs-lookup"><span data-stu-id="571a6-322">**Build configuration**: By default, NuGet uses the default build configuration set in the project file, typically *Debug*.</span></span> <span data-ttu-id="571a6-323">Aby zabalil soubory z jiné sestavení konfigurace, jako například *verze*, použijte `-properties` možnost s konfigurací:</span><span class="sxs-lookup"><span data-stu-id="571a6-323">To pack files from a different build configuration, such as *Release*, use the `-properties` option with the configuration:</span></span>

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- <span data-ttu-id="571a6-324">**Symboly**: Chcete-li zahrnout symboly, které umožňují uživatelům procházet kódem balíčku v ladicím programu, použijte `-Symbols` možnost:</span><span class="sxs-lookup"><span data-stu-id="571a6-324">**Symbols**: to include symbols that allow consumers to step through your package code in the debugger, use the `-Symbols` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="testing-package-installation"></a><span data-ttu-id="571a6-325">Testování instalace balíčku</span><span class="sxs-lookup"><span data-stu-id="571a6-325">Testing package installation</span></span>

<span data-ttu-id="571a6-326">Před publikováním balíčku se obvykle chcete otestovat proces instalace balíčku do projektu.</span><span class="sxs-lookup"><span data-stu-id="571a6-326">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="571a6-327">Testy, zkontrolujte, zda nutně soubory všechny ukládaly do jejich správné umístění v projektu.</span><span class="sxs-lookup"><span data-stu-id="571a6-327">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="571a6-328">Můžete testovat zařízení ručně v sadě Visual Studio nebo na příkazovém řádku pomocí běžných [balíček instalační postup, který](../consume-packages/ways-to-install-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="571a6-328">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/ways-to-install-a-package.md).</span></span>

<span data-ttu-id="571a6-329">Pro automatizované testování základní proces je následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="571a6-329">For automated testing, the basic process is as follows:</span></span>

1. <span data-ttu-id="571a6-330">Kopírovat `.nupkg` soubor do místní složky.</span><span class="sxs-lookup"><span data-stu-id="571a6-330">Copy the `.nupkg` file to a local folder.</span></span>
1. <span data-ttu-id="571a6-331">Přidat složku do vašeho zdroje balíčků pomocí `nuget sources add -name <name> -source <path>` příkazu (naleznete v tématu [zdroje nuget](../tools/cli-ref-sources.md)).</span><span class="sxs-lookup"><span data-stu-id="571a6-331">Add the folder to your package sources using the `nuget sources add -name <name> -source <path>` command (see [nuget sources](../tools/cli-ref-sources.md)).</span></span> <span data-ttu-id="571a6-332">Všimněte si, že budete potřebovat pouze nastavit tento místní zdroj jednou na jakémkoli daném počítači.</span><span class="sxs-lookup"><span data-stu-id="571a6-332">Note that you need only set this local source once on any given computer.</span></span>
1. <span data-ttu-id="571a6-333">Nainstalovat balíček z tohoto zdroje pomocí `nuget install <packageID> -source <name>` kde `<name>` odpovídá názvu zdroje uvedeným `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="571a6-333">Install the package from that source using `nuget install <packageID> -source <name>` where `<name>` matches the name of your source as given to `nuget sources`.</span></span> <span data-ttu-id="571a6-334">Zadání zdrojové zajišťuje, že je balíček nainstalován z tohoto zdroje samostatně.</span><span class="sxs-lookup"><span data-stu-id="571a6-334">Specifying the source ensures that the package is installed from that source alone.</span></span>
1. <span data-ttu-id="571a6-335">Prozkoumání systému souborů ke kontrole, zda jsou správně nainstalovány soubory.</span><span class="sxs-lookup"><span data-stu-id="571a6-335">Examine your file system to check that files are installed correctly.</span></span>

## <a name="next-steps"></a><span data-ttu-id="571a6-336">Další kroky</span><span class="sxs-lookup"><span data-stu-id="571a6-336">Next Steps</span></span>

<span data-ttu-id="571a6-337">Jakmile vytvoříte balíček, který je `.nupkg` souboru ji také publikovat podle vašeho výběru v galerii podle popisu v [publikování balíčku](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="571a6-337">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="571a6-338">Můžete také chtít rozšířit možnosti vašeho balíčku nebo jinak podporovala jiné scénáře, jak je popsáno v následujících tématech:</span><span class="sxs-lookup"><span data-stu-id="571a6-338">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="571a6-339">Správa verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="571a6-339">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="571a6-340">Podpora více cílových verzí rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="571a6-340">Supporting multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="571a6-341">Transformace zdrojového a konfiguračních souborů</span><span class="sxs-lookup"><span data-stu-id="571a6-341">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="571a6-342">Lokalizace</span><span class="sxs-lookup"><span data-stu-id="571a6-342">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="571a6-343">Předběžné verze</span><span class="sxs-lookup"><span data-stu-id="571a6-343">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)

<span data-ttu-id="571a6-344">Dostupné jsou i další balíčky typů je potřeba vědět:</span><span class="sxs-lookup"><span data-stu-id="571a6-344">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="571a6-345">Nativní balíčky</span><span class="sxs-lookup"><span data-stu-id="571a6-345">Native Packages</span></span>](../create-packages/native-packages.md)
- [<span data-ttu-id="571a6-346">Balíčky symbolů</span><span class="sxs-lookup"><span data-stu-id="571a6-346">Symbol Packages</span></span>](../create-packages/symbol-packages.md)
