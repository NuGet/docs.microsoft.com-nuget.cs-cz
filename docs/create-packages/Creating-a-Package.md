---
title: Vytvoření balíčku NuGet pomocí cli nuget.exe
description: Podrobný průvodce procesem navrhování a vytváření balíčku NuGet, včetně klíčových rozhodovacích bodů, jako jsou soubory a správa verzí.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: b3e6f0efc9e2e12de186ffd4ce29d496d07d5fc4
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428945"
---
# <a name="create-a-package-using-the-nugetexe-cli"></a><span data-ttu-id="ea690-103">Vytvoření balíčku pomocí cli nuget.exe</span><span class="sxs-lookup"><span data-stu-id="ea690-103">Create a package using the nuget.exe CLI</span></span>

<span data-ttu-id="ea690-104">Bez ohledu na to, co váš balíček dělá nebo jaký `nuget.exe` kód `dotnet.exe`obsahuje, použijete jeden z nástrojů rozhraní rozhraní rozhraní cli, nebo , k balení této funkce do součásti, která může být sdílena s libovolným počtem jiných vývojářů.</span><span class="sxs-lookup"><span data-stu-id="ea690-104">No matter what your package does or what code it contains, you use one of the CLI tools, either `nuget.exe` or `dotnet.exe`, to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="ea690-105">Informace o instalaci nástrojů ClI nuget, naleznete [v tématu Instalace klientských nástrojů NuGet](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="ea690-105">To install NuGet CLI tools, see [Install NuGet client tools](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="ea690-106">Všimněte si, že Visual Studio neobsahuje automaticky nástroj cli.</span><span class="sxs-lookup"><span data-stu-id="ea690-106">Note that Visual Studio does not automatically include a CLI tool.</span></span>

- <span data-ttu-id="ea690-107">U projektů, které nejsou ve stylu sady SDK, obvykle projekty rozhraní .NET Framework, vytvořte balíček podle kroků popsaných v tomto článku.</span><span class="sxs-lookup"><span data-stu-id="ea690-107">For non-SDK-style projects, typically .NET Framework projects, follow the steps described in this article to create a package.</span></span> <span data-ttu-id="ea690-108">Podrobné pokyny pomocí sady Visual Studio `nuget.exe` a rozhraní příkazového příkazu naleznete v [tématu Vytvoření a publikování balíčku rozhraní .NET Framework](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md).</span><span class="sxs-lookup"><span data-stu-id="ea690-108">For step-by-step instructions using Visual Studio and the `nuget.exe` CLI, see [Create and publish a .NET Framework package](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md).</span></span>

- <span data-ttu-id="ea690-109">Pro projekty .NET Core a .NET Standard, které používají [formát ve stylu sady SDK,](../resources/check-project-format.md)a všechny ostatní projekty ve stylu sady SDK naleznete v [tématu Vytvoření balíčku NuGet pomocí rozhraní příkazového příkazu dotnet .](creating-a-package-dotnet-cli.md)</span><span class="sxs-lookup"><span data-stu-id="ea690-109">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, see [Create a NuGet package using the dotnet CLI](creating-a-package-dotnet-cli.md).</span></span>

- <span data-ttu-id="ea690-110">Pro projekty `packages.config` migrované z [PackageReference](../consume-packages/package-references-in-project-files.md)použijte [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span><span class="sxs-lookup"><span data-stu-id="ea690-110">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

<span data-ttu-id="ea690-111">Technicky vzato, balíček NuGet je pouze soubor ZIP, `.nupkg` který byl přejmenován s příponou a jehož obsah odpovídá určitým konvencím.</span><span class="sxs-lookup"><span data-stu-id="ea690-111">Technically speaking, a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension and whose contents match certain conventions.</span></span> <span data-ttu-id="ea690-112">Toto téma popisuje podrobný proces vytváření balíčku, který splňuje tyto konvence.</span><span class="sxs-lookup"><span data-stu-id="ea690-112">This topic describes the detailed process of creating a package that meets those conventions.</span></span>

<span data-ttu-id="ea690-113">Balení začíná kompilovaným kódem (sestaveními), symboly a/nebo jinými soubory, které chcete doručit jako balíček (viz [Přehled a pracovní postup).](overview-and-workflow.md)</span><span class="sxs-lookup"><span data-stu-id="ea690-113">Packaging begins with the compiled code (assemblies), symbols, and/or other files that you want to deliver as a package (see [Overview and workflow](overview-and-workflow.md)).</span></span> <span data-ttu-id="ea690-114">Tento proces je nezávislý na kompilaci nebo jiné generování souborů, které přejdou do balíčku, i když můžete čerpat z informací v souboru projektu, aby zkompilovaná sestavení a balíčky v synchronizaci.</span><span class="sxs-lookup"><span data-stu-id="ea690-114">This process is independent from compiling or otherwise generating the files that go into the package, although you can draw from information in a project file to keep the compiled assemblies and packages in sync.</span></span>

> [!Important]
> <span data-ttu-id="ea690-115">Toto téma se týká projektů, které nejsou ve stylu sady SDK, obvykle projekty než .NET Core a .NET Standard projekty pomocí Visual Studio 2017 a vyšší verze a NuGet 4.0 +.</span><span class="sxs-lookup"><span data-stu-id="ea690-115">This topic applies to non-SDK-style projects, typically projects other than .NET Core and .NET Standard projects using Visual Studio 2017 and higher versions and NuGet 4.0+.</span></span>

## <a name="decide-which-assemblies-to-package"></a><span data-ttu-id="ea690-116">Rozhodněte se, která sestavení mají být zabalena</span><span class="sxs-lookup"><span data-stu-id="ea690-116">Decide which assemblies to package</span></span>

<span data-ttu-id="ea690-117">Většina balíčků pro obecné účely obsahuje jedno nebo více sestavení, které mohou ostatní vývojáři použít ve svých vlastních projektech.</span><span class="sxs-lookup"><span data-stu-id="ea690-117">Most general-purpose packages contain one or more assemblies that other developers can use in their own projects.</span></span>

- <span data-ttu-id="ea690-118">Obecně je nejlepší mít jedno sestavení na balíček NuGet, za předpokladu, že každé sestavení je nezávisle užitečné.</span><span class="sxs-lookup"><span data-stu-id="ea690-118">In general, it's best to have one assembly per NuGet package, provided that each assembly is independently useful.</span></span> <span data-ttu-id="ea690-119">Například pokud máte, `Utilities.dll` který `Parser.dll`závisí `Parser.dll` na , a je užitečné samostatně, pak vytvořte jeden balíček pro každý.</span><span class="sxs-lookup"><span data-stu-id="ea690-119">For example, if you have a `Utilities.dll` that depends on `Parser.dll`, and `Parser.dll` is useful on its own, then create one package for each.</span></span> <span data-ttu-id="ea690-120">To umožňuje vývojářům `Parser.dll` používat `Utilities.dll`nezávisle na .</span><span class="sxs-lookup"><span data-stu-id="ea690-120">Doing so allows developers to use `Parser.dll` independently of `Utilities.dll`.</span></span>

- <span data-ttu-id="ea690-121">Pokud se vaše knihovna skládá z více sestavení, která nejsou nezávisle užitečná, je v pořádku je kombinovat do jednoho balíčku.</span><span class="sxs-lookup"><span data-stu-id="ea690-121">If your library is composed of multiple assemblies that aren't independently useful, then it's fine to combine them into one package.</span></span> <span data-ttu-id="ea690-122">Použití předchozího příkladu, pokud `Parser.dll` obsahuje kód, který se používá pouze `Utilities.dll`v , pak je v pořádku zachovat `Parser.dll` ve stejném balíčku.</span><span class="sxs-lookup"><span data-stu-id="ea690-122">Using the previous example, if `Parser.dll` contains code that's used only by `Utilities.dll`, then it's fine to keep `Parser.dll` in the same package.</span></span>

- <span data-ttu-id="ea690-123">Podobně, pokud `Utilities.dll` závisí `Utilities.resources.dll`na , kde opět není užitečné samo o sobě, pak dát oba ve stejném balíčku.</span><span class="sxs-lookup"><span data-stu-id="ea690-123">Similarly, if `Utilities.dll` depends on `Utilities.resources.dll`, where again the latter is not useful on its own, then put both in the same package.</span></span>

<span data-ttu-id="ea690-124">Zdroje jsou ve skutečnosti zvláštní případ.</span><span class="sxs-lookup"><span data-stu-id="ea690-124">Resources are, in fact, a special case.</span></span> <span data-ttu-id="ea690-125">Při instalaci balíčku do projektu NuGet automaticky přidá odkazy na sestavení knihovny DLL balíčku, *s výjimkou* těch, které jsou pojmenovány, `.resources.dll` protože jsou považovány za lokalizované satelitní sestavení (viz [Vytváření lokalizovaných balíčků](creating-localized-packages.md)).</span><span class="sxs-lookup"><span data-stu-id="ea690-125">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies (see [Creating localized packages](creating-localized-packages.md)).</span></span> <span data-ttu-id="ea690-126">Z tohoto důvodu `.resources.dll` se vyhněte použití pro soubory, které jinak obsahují základní kód balíčku.</span><span class="sxs-lookup"><span data-stu-id="ea690-126">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="ea690-127">Pokud vaše knihovna obsahuje sestavení interop com, postupujte podle dalších pokynů v [části Vytvořit balíčky s meziop sestaveními com](author-packages-with-com-interop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="ea690-127">If your library contains COM interop assemblies, follow additional the guidelines in [Create packages with COM interop assemblies](author-packages-with-com-interop-assemblies.md).</span></span>

## <a name="the-role-and-structure-of-the-nuspec-file"></a><span data-ttu-id="ea690-128">Role a struktura souboru .nuspec</span><span class="sxs-lookup"><span data-stu-id="ea690-128">The role and structure of the .nuspec file</span></span>

<span data-ttu-id="ea690-129">Jakmile budete vědět, jaké soubory chcete zabalit, dalším krokem `.nuspec` je vytvoření manifestu balíčku v souboru XML.</span><span class="sxs-lookup"><span data-stu-id="ea690-129">Once you know what files you want to package, the next step is creating a package manifest in a `.nuspec` XML file.</span></span>

<span data-ttu-id="ea690-130">Manifest:</span><span class="sxs-lookup"><span data-stu-id="ea690-130">The manifest:</span></span>

1. <span data-ttu-id="ea690-131">Popisuje obsah balíčku a je sám součástí balíčku.</span><span class="sxs-lookup"><span data-stu-id="ea690-131">Describes the package's contents and is itself included in the package.</span></span>
1. <span data-ttu-id="ea690-132">Řídí vytvoření balíčku a instruuje NuGet o tom, jak nainstalovat balíček do projektu.</span><span class="sxs-lookup"><span data-stu-id="ea690-132">Drives both the creation of the package and instructs NuGet on how to install the package into a project.</span></span> <span data-ttu-id="ea690-133">Například manifest identifikuje jiné závislosti balíčků tak, aby NuGet můžete také nainstalovat tyto závislosti při instalaci hlavního balíčku.</span><span class="sxs-lookup"><span data-stu-id="ea690-133">For example, the manifest identifies other package dependencies such that NuGet can also install those dependencies when the main package is installed.</span></span>
1. <span data-ttu-id="ea690-134">Obsahuje požadované i volitelné vlastnosti, jak je popsáno níže.</span><span class="sxs-lookup"><span data-stu-id="ea690-134">Contains both required and optional properties as described below.</span></span> <span data-ttu-id="ea690-135">Přesné podrobnosti, včetně dalších vlastností, které zde nejsou uvedeny, naleznete v [odkazu .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="ea690-135">For exact details, including other properties not mentioned here, see  the [.nuspec reference](../reference/nuspec.md).</span></span>

<span data-ttu-id="ea690-136">Požadované vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="ea690-136">Required properties:</span></span>

- <span data-ttu-id="ea690-137">Identifikátor balíčku, který musí být jedinečný v celé galerii, která je hostitelem balíčku.</span><span class="sxs-lookup"><span data-stu-id="ea690-137">The package identifier, which must be unique across the gallery that hosts the package.</span></span>
- <span data-ttu-id="ea690-138">Konkrétní číslo verze ve formuláři *Major.Minor.Patch[-Přípona],* kde *přípona* identifikuje [předběžné verze](prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="ea690-138">A specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md)</span></span>
- <span data-ttu-id="ea690-139">Název balíčku, jak by se měl objevit na hostiteli (jako nuget.org)</span><span class="sxs-lookup"><span data-stu-id="ea690-139">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="ea690-140">Informace o autorovi a majiteli.</span><span class="sxs-lookup"><span data-stu-id="ea690-140">Author and owner information.</span></span>
- <span data-ttu-id="ea690-141">Dlouhý popis balíčku.</span><span class="sxs-lookup"><span data-stu-id="ea690-141">A long description of the package.</span></span>

<span data-ttu-id="ea690-142">Běžné volitelné vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="ea690-142">Common optional properties:</span></span>

- <span data-ttu-id="ea690-143">Poznámky k verzi</span><span class="sxs-lookup"><span data-stu-id="ea690-143">Release notes</span></span>
- <span data-ttu-id="ea690-144">Informace o autorských právech</span><span class="sxs-lookup"><span data-stu-id="ea690-144">Copyright information</span></span>
- <span data-ttu-id="ea690-145">Stručný popis [ui Správce balíčků v sadě Visual Studio](../consume-packages/install-use-packages-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="ea690-145">A short description for the [Package Manager UI in Visual Studio](../consume-packages/install-use-packages-visual-studio.md)</span></span>
- <span data-ttu-id="ea690-146">ID národního prostředí</span><span class="sxs-lookup"><span data-stu-id="ea690-146">A locale ID</span></span>
- <span data-ttu-id="ea690-147">Adresa URL projektu</span><span class="sxs-lookup"><span data-stu-id="ea690-147">Project URL</span></span>
- <span data-ttu-id="ea690-148">Licence jako výraz nebo`licenseUrl` soubor ( je zastaralá, použijte [ `license` prvek metadat nuspec](../reference/nuspec.md#license))</span><span class="sxs-lookup"><span data-stu-id="ea690-148">License as an expression or file (`licenseUrl` is being deprecated, use the [`license` nuspec metadata element](../reference/nuspec.md#license))</span></span>
- <span data-ttu-id="ea690-149">Adresa URL ikony</span><span class="sxs-lookup"><span data-stu-id="ea690-149">An icon URL</span></span>
- <span data-ttu-id="ea690-150">Seznamy závislostí a odkazů</span><span class="sxs-lookup"><span data-stu-id="ea690-150">Lists of dependencies and references</span></span>
- <span data-ttu-id="ea690-151">Značky, které pomáhají při vyhledávání v galerii</span><span class="sxs-lookup"><span data-stu-id="ea690-151">Tags that assist in gallery searches</span></span>

<span data-ttu-id="ea690-152">Následuje typický (ale fiktivní) `.nuspec` soubor s komentáři popisujícími vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="ea690-152">The following is a typical (but fictitious) `.nuspec` file, with comments describing the properties:</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
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

<span data-ttu-id="ea690-153">Podrobnosti o deklarování závislostí a určení čísel verzí naleznete v tématech [packages.config](../reference/packages-config.md) a [Package versioning](../concepts/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="ea690-153">For details on declaring dependencies and specifying version numbers, see [packages.config](../reference/packages-config.md) and [Package versioning](../concepts/package-versioning.md).</span></span> <span data-ttu-id="ea690-154">Je také možné povrchové prostředky ze závislostí přímo `include` `exclude` v balíčku `dependency` pomocí atributy a na prvek.</span><span class="sxs-lookup"><span data-stu-id="ea690-154">It is also possible to surface assets from dependencies directly in the package by using the `include` and `exclude` attributes on the `dependency` element.</span></span> <span data-ttu-id="ea690-155">Viz [odkaz .nuspec - závislosti](../reference/nuspec.md#dependencies).</span><span class="sxs-lookup"><span data-stu-id="ea690-155">See [.nuspec Reference - Dependencies](../reference/nuspec.md#dependencies).</span></span>

<span data-ttu-id="ea690-156">Vzhledem k tomu, že manifest je součástí balíčku vytvořeného z něj, můžete najít libovolný počet dalších příkladů zkoumáním existující balíčky.</span><span class="sxs-lookup"><span data-stu-id="ea690-156">Because the manifest is included in the package created from it, you can find any number of additional examples by examining existing packages.</span></span> <span data-ttu-id="ea690-157">Dobrým zdrojem je složka *globálních balíčků* v počítači, jejíž umístění je vráceno následujícím příkazem:</span><span class="sxs-lookup"><span data-stu-id="ea690-157">A good source is the *global-packages* folder on your computer, the location of which is returned by the following command:</span></span>

```cli
nuget locals -list global-packages
```

<span data-ttu-id="ea690-158">Přejděte do libovolné složky `.nupkg` *package\version,* zkopírujte `.zip` soubor do `.nuspec` souboru, `.zip` otevřete jej a zkontrolujte v něm.</span><span class="sxs-lookup"><span data-stu-id="ea690-158">Go into any *package\version* folder, copy the `.nupkg` file to a `.zip` file, then open that `.zip` file and examine the `.nuspec` within it.</span></span>

> [!Note]
> <span data-ttu-id="ea690-159">Při vytváření `.nuspec` z projektu sady Visual Studio manifest obsahuje tokeny, které jsou nahrazeny informacemi z projektu při sestavení balíčku.</span><span class="sxs-lookup"><span data-stu-id="ea690-159">When creating a `.nuspec` from a Visual Studio project, the manifest contains tokens that are replaced with information from the project when the package is built.</span></span> <span data-ttu-id="ea690-160">Viz [Vytvoření .nuspec z projektu sady Visual Studio](#from-a-visual-studio-project).</span><span class="sxs-lookup"><span data-stu-id="ea690-160">See [Creating the .nuspec from a Visual Studio project](#from-a-visual-studio-project).</span></span>

## <a name="create-the-nuspec-file"></a><span data-ttu-id="ea690-161">Vytvoření souboru Nuspec</span><span class="sxs-lookup"><span data-stu-id="ea690-161">Create the .nuspec file</span></span>

<span data-ttu-id="ea690-162">Vytvoření úplného manifestu obvykle začíná `.nuspec` základním souborem generovaným jednou z následujících metod:</span><span class="sxs-lookup"><span data-stu-id="ea690-162">Creating a complete manifest typically begins with a basic `.nuspec` file generated through one of the following methods:</span></span>

- [<span data-ttu-id="ea690-163">Pracovní adresář založený na konvencích</span><span class="sxs-lookup"><span data-stu-id="ea690-163">A convention-based working directory</span></span>](#from-a-convention-based-working-directory)
- [<span data-ttu-id="ea690-164">DLL sestavy</span><span class="sxs-lookup"><span data-stu-id="ea690-164">An assembly DLL</span></span>](#from-an-assembly-dll)
- [<span data-ttu-id="ea690-165">Projekt sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ea690-165">A Visual Studio project</span></span>](#from-a-visual-studio-project)    
- [<span data-ttu-id="ea690-166">Nový soubor s výchozími hodnotami</span><span class="sxs-lookup"><span data-stu-id="ea690-166">New file with default values</span></span>](#new-file-with-default-values)

<span data-ttu-id="ea690-167">Potom upravit soubor ručně tak, aby popis přesně obsah, který chcete v konečném balíčku.</span><span class="sxs-lookup"><span data-stu-id="ea690-167">You then edit the file by hand so that it describes the exact content you want in the final package.</span></span>

> [!Important]
> <span data-ttu-id="ea690-168">Generované `.nuspec` soubory obsahují zástupné symboly, které musí `nuget pack` být změněny před vytvořením balíčku pomocí příkazu.</span><span class="sxs-lookup"><span data-stu-id="ea690-168">Generated `.nuspec` files contain placeholders that must be modified before creating the package with the `nuget pack` command.</span></span> <span data-ttu-id="ea690-169">Tento příkaz se `.nuspec` nezdaří, pokud obsahuje všechny zástupné symboly.</span><span class="sxs-lookup"><span data-stu-id="ea690-169">That command fails if the `.nuspec` contains any placeholders.</span></span>

### <a name="from-a-convention-based-working-directory"></a><span data-ttu-id="ea690-170">Z pracovního adresáře založeného na konvencích</span><span class="sxs-lookup"><span data-stu-id="ea690-170">From a convention-based working directory</span></span>

<span data-ttu-id="ea690-171">Vzhledem k tomu, že balíček NuGet je `.nupkg` pouze soubor ZIP, který byl přejmenován s příponou, je často `.nuspec` nejjednodušší vytvořit strukturu složek, kterou chcete v místním systému souborů, a pak soubor vytvořit přímo z této struktury.</span><span class="sxs-lookup"><span data-stu-id="ea690-171">Because a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension, it's often easiest to create the folder structure you want on your local file system, then create the `.nuspec` file directly from that structure.</span></span> <span data-ttu-id="ea690-172">Příkaz `nuget pack` pak automaticky přidá všechny soubory ve struktuře složek (s výjimkou všech složek, které začínají `.`, což umožňuje zachovat soukromé soubory ve stejné struktuře).</span><span class="sxs-lookup"><span data-stu-id="ea690-172">The `nuget pack` command then automatically adds all files in that folder structure (excluding any folders that begin with `.`, allowing you to keep private files in the same structure).</span></span>

<span data-ttu-id="ea690-173">Výhodou tohoto přístupu je, že není nutné zadat v manifestu, které soubory chcete zahrnout do balíčku (jak je vysvětleno dále v tomto tématu).</span><span class="sxs-lookup"><span data-stu-id="ea690-173">The advantage to this approach is that you don't need to specify in the manifest which files you want to include in the package (as explained later in this topic).</span></span> <span data-ttu-id="ea690-174">Můžete jednoduše mít proces sestavení vytvořit přesnou strukturu složek, která jde do balíčku a můžete snadno zahrnout další soubory, které nemusí být součástí projektu jinak:</span><span class="sxs-lookup"><span data-stu-id="ea690-174">You can simply have your build process produce the exact folder structure that goes into the package, and you can easily include other files that might not be part of a project otherwise:</span></span>

- <span data-ttu-id="ea690-175">Obsah a zdrojový kód, který by měl být vložen do cílového projektu.</span><span class="sxs-lookup"><span data-stu-id="ea690-175">Content and source code that should be injected into the target project.</span></span>
- <span data-ttu-id="ea690-176">Skripty prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="ea690-176">PowerShell scripts</span></span>
- <span data-ttu-id="ea690-177">Transformace na existující konfigurace a soubory zdrojového kódu v projektu.</span><span class="sxs-lookup"><span data-stu-id="ea690-177">Transformations to existing configuration and source code files in a project.</span></span>

<span data-ttu-id="ea690-178">Konvence složek jsou následující:</span><span class="sxs-lookup"><span data-stu-id="ea690-178">The folder conventions are as follows:</span></span>

| <span data-ttu-id="ea690-179">Složka</span><span class="sxs-lookup"><span data-stu-id="ea690-179">Folder</span></span> | <span data-ttu-id="ea690-180">Popis</span><span class="sxs-lookup"><span data-stu-id="ea690-180">Description</span></span> | <span data-ttu-id="ea690-181">Akce při instalaci balíčku</span><span class="sxs-lookup"><span data-stu-id="ea690-181">Action upon package install</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ea690-182">(kořen)</span><span class="sxs-lookup"><span data-stu-id="ea690-182">(root)</span></span> | <span data-ttu-id="ea690-183">Umístění souboru readme.txt</span><span class="sxs-lookup"><span data-stu-id="ea690-183">Location for readme.txt</span></span> | <span data-ttu-id="ea690-184">Visual Studio zobrazí soubor readme.txt v kořenovém adresáři balíčku při instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="ea690-184">Visual Studio displays a readme.txt file in the package root when the package is installed.</span></span> |
| <span data-ttu-id="ea690-185">lib/{tfm}</span><span class="sxs-lookup"><span data-stu-id="ea690-185">lib/{tfm}</span></span> | <span data-ttu-id="ea690-186">Assembly`.dll`( ),`.xml`dokumentace (`.pdb`) a symbol ( ) soubory pro daný cílový rámec moniker (TFM)</span><span class="sxs-lookup"><span data-stu-id="ea690-186">Assembly (`.dll`), documentation (`.xml`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="ea690-187">Sestavení jsou přidány jako odkazy pro kompilování i runtime; `.xml` a `.pdb` zkopírovány do složek projektu.</span><span class="sxs-lookup"><span data-stu-id="ea690-187">Assemblies are added as references for compile as well as runtime; `.xml` and `.pdb` copied into project folders.</span></span> <span data-ttu-id="ea690-188">Viz [Podpora více cílových rozhraní](supporting-multiple-target-frameworks.md) pro vytváření podsložek specifických pro cíl rámce.</span><span class="sxs-lookup"><span data-stu-id="ea690-188">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md) for creating framework target-specific sub-folders.</span></span> |
| <span data-ttu-id="ea690-189">ref/{tfm}</span><span class="sxs-lookup"><span data-stu-id="ea690-189">ref/{tfm}</span></span> | <span data-ttu-id="ea690-190">Assembly`.dll`( )`.pdb`a symbol ( ) soubory pro daný cílový rámec zástupný název (TFM)</span><span class="sxs-lookup"><span data-stu-id="ea690-190">Assembly (`.dll`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="ea690-191">Sestavení jsou přidány jako odkazy pouze pro čas kompilace; Takže nic nebude zkopírováno do složky přihrádky projektu.</span><span class="sxs-lookup"><span data-stu-id="ea690-191">Assemblies are added as references only for compile time; So nothing will be copied into project bin folder.</span></span> |
| <span data-ttu-id="ea690-192">Runtime</span><span class="sxs-lookup"><span data-stu-id="ea690-192">runtimes</span></span> | <span data-ttu-id="ea690-193">Sestavení specifické pro`.dll`architekturu`.pdb`( ),`.pri`symbol ( ) a nativní soubory prostředků ( )</span><span class="sxs-lookup"><span data-stu-id="ea690-193">Architecture-specific assembly (`.dll`), symbol (`.pdb`), and native resource (`.pri`) files</span></span> | <span data-ttu-id="ea690-194">Sestavení jsou přidány jako odkazy pouze pro běh. ostatní soubory jsou zkopírovány do složek projektu.</span><span class="sxs-lookup"><span data-stu-id="ea690-194">Assemblies are added as references only for runtime; other files are copied into project folders.</span></span> <span data-ttu-id="ea690-195">Ve `/ref/{tfm}` složce by mělo být `AnyCPU` vždy odpovídající sestavení specifické pro (TFM), které poskytuje odpovídající sestavení času kompilace.</span><span class="sxs-lookup"><span data-stu-id="ea690-195">There should always be a corresponding (TFM) `AnyCPU` specific assembly under `/ref/{tfm}` folder to provide corresponding compile time assembly.</span></span> <span data-ttu-id="ea690-196">Viz [Podpora více cílových architektur](supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="ea690-196">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md).</span></span> |
| <span data-ttu-id="ea690-197">content</span><span class="sxs-lookup"><span data-stu-id="ea690-197">content</span></span> | <span data-ttu-id="ea690-198">Libovolné soubory</span><span class="sxs-lookup"><span data-stu-id="ea690-198">Arbitrary files</span></span> | <span data-ttu-id="ea690-199">Obsah se zkopíruje do kořenového adresáře projektu.</span><span class="sxs-lookup"><span data-stu-id="ea690-199">Contents are copied to the project root.</span></span> <span data-ttu-id="ea690-200">Představte si složku **obsahu** jako kořen cílové aplikace, která nakonec spotřebovává balíček.</span><span class="sxs-lookup"><span data-stu-id="ea690-200">Think of the **content** folder as the root of the target application that ultimately consumes the package.</span></span> <span data-ttu-id="ea690-201">Chcete-li, aby balíček přidal obrázek do složky */images* aplikace, umístěte jej do složky *obsahu/obrázků* balíčku.</span><span class="sxs-lookup"><span data-stu-id="ea690-201">To have the package add an image in the application's */images* folder, place it in the package's *content/images* folder.</span></span> |
| <span data-ttu-id="ea690-202">sestavení</span><span class="sxs-lookup"><span data-stu-id="ea690-202">build</span></span> | <span data-ttu-id="ea690-203">*(3.x+)* MSBuild `.targets` `.props` a soubory</span><span class="sxs-lookup"><span data-stu-id="ea690-203">*(3.x+)* MSBuild `.targets` and `.props` files</span></span> | <span data-ttu-id="ea690-204">Automaticky vložendo projektu.</span><span class="sxs-lookup"><span data-stu-id="ea690-204">Automatically inserted into the project.</span></span> |
| <span data-ttu-id="ea690-205">buildMultiTargeting</span><span class="sxs-lookup"><span data-stu-id="ea690-205">buildMultiTargeting</span></span> | <span data-ttu-id="ea690-206">*(4.0+)* MSBuild `.targets` `.props` a soubory pro cílení napříč rámci</span><span class="sxs-lookup"><span data-stu-id="ea690-206">*(4.0+)* MSBuild `.targets` and `.props` files for cross-framework targeting</span></span> | <span data-ttu-id="ea690-207">Automaticky vložendo projektu.</span><span class="sxs-lookup"><span data-stu-id="ea690-207">Automatically inserted into the project.</span></span> |
| <span data-ttu-id="ea690-208">buildTransitive</span><span class="sxs-lookup"><span data-stu-id="ea690-208">buildTransitive</span></span> | <span data-ttu-id="ea690-209">*(5.0+)* MSBuild `.targets` `.props` a soubory, které toku přechodně na všechny náročné projektu.</span><span class="sxs-lookup"><span data-stu-id="ea690-209">*(5.0+)* MSBuild `.targets` and `.props` files that flow transitively to any consuming project.</span></span> <span data-ttu-id="ea690-210">Podívejte se na stránku [funkcí.](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior)</span><span class="sxs-lookup"><span data-stu-id="ea690-210">See the [feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) page.</span></span> | <span data-ttu-id="ea690-211">Automaticky vložendo projektu.</span><span class="sxs-lookup"><span data-stu-id="ea690-211">Automatically inserted into the project.</span></span> |
| <span data-ttu-id="ea690-212">nástroje</span><span class="sxs-lookup"><span data-stu-id="ea690-212">tools</span></span> | <span data-ttu-id="ea690-213">Skripty a programy prostředí Powershell přístupné z konzoly Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="ea690-213">Powershell scripts and programs accessible from the Package Manager Console</span></span> | <span data-ttu-id="ea690-214">Složka `tools` je přidána `PATH` do proměnné prostředí pouze pro konzolu `PATH` Správce balíčků (konkrétně *ne* na sadu msbuild při vytváření projektu).</span><span class="sxs-lookup"><span data-stu-id="ea690-214">The `tools` folder is added to the `PATH` environment variable for the Package Manager Console only (Specifically, *not* to the `PATH` as set for MSBuild when building the project).</span></span> |

<span data-ttu-id="ea690-215">Vzhledem k tomu, že struktura složek může obsahovat libovolný počet sestavení pro libovolný počet cílových architektur, je tato metoda nezbytná při vytváření balíčků, které podporují více architektur.</span><span class="sxs-lookup"><span data-stu-id="ea690-215">Because your folder structure can contain any number of assemblies for any number of target frameworks, this method is necessary when creating packages that support multiple frameworks.</span></span>

<span data-ttu-id="ea690-216">V každém případě, jakmile budete mít požadovanou strukturu složek na místě, spusťte následující příkaz v této složce k vytvoření souboru: `.nuspec`</span><span class="sxs-lookup"><span data-stu-id="ea690-216">In any case, once you have the desired folder structure in place, run the following command in that folder to create the `.nuspec` file:</span></span>

```cli
nuget spec
```

<span data-ttu-id="ea690-217">Znovu `.nuspec` generované neobsahuje žádné explicitní odkazy na soubory ve struktuře složek.</span><span class="sxs-lookup"><span data-stu-id="ea690-217">Again, the generated `.nuspec` contains no explicit references to files in the folder structure.</span></span> <span data-ttu-id="ea690-218">NuGet automaticky zahrnuje všechny soubory při vytvoření balíčku.</span><span class="sxs-lookup"><span data-stu-id="ea690-218">NuGet automatically includes all files when the package is created.</span></span> <span data-ttu-id="ea690-219">Stále je však nutné upravit zástupné hodnoty v jiných částech manifestu.</span><span class="sxs-lookup"><span data-stu-id="ea690-219">You still need to edit placeholder values in other parts of the manifest, however.</span></span>

### <a name="from-an-assembly-dll"></a><span data-ttu-id="ea690-220">Z dll sestavy</span><span class="sxs-lookup"><span data-stu-id="ea690-220">From an assembly DLL</span></span>

<span data-ttu-id="ea690-221">V jednoduchém případě vytvoření balíčku z sestavení můžete `.nuspec` vygenerovat soubor z metadat v sestavení pomocí následujícího příkazu:</span><span class="sxs-lookup"><span data-stu-id="ea690-221">In the simple case of creating a package from an assembly, you can generate a `.nuspec` file from the metadata in the assembly using the following command:</span></span>

```cli
nuget spec <assembly-name>.dll
```

<span data-ttu-id="ea690-222">Pomocí tohoto formuláře nahradí několik zástupných symbolů v manifestu se specifickými hodnotami ze sestavy.</span><span class="sxs-lookup"><span data-stu-id="ea690-222">Using this form replaces a few placeholders in the manifest with specific values from the assembly.</span></span> <span data-ttu-id="ea690-223">Například `<id>` vlastnost je nastavena na název `<version>` sestavení a je nastavena na verzi sestavení.</span><span class="sxs-lookup"><span data-stu-id="ea690-223">For example, the `<id>` property is set to the assembly name, and `<version>` is set to the assembly version.</span></span> <span data-ttu-id="ea690-224">Ostatní vlastnosti v manifestu však nemají odpovídající hodnoty v sestavení a proto stále obsahují zástupné symboly.</span><span class="sxs-lookup"><span data-stu-id="ea690-224">Other properties in the manifest, however, don't have matching values in the assembly and thus still contain placeholders.</span></span>

### <a name="from-a-visual-studio-project"></a><span data-ttu-id="ea690-225">Z projektu sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ea690-225">From a Visual Studio project</span></span>

<span data-ttu-id="ea690-226">Vytvoření `.nuspec` ze `.csproj` souboru nebo `.vbproj` je vhodné, protože ostatní balíčky, které byly nainstalovány do tohoto projektu jsou automaticky odkazovány jako závislosti.</span><span class="sxs-lookup"><span data-stu-id="ea690-226">Creating a `.nuspec` from a `.csproj` or `.vbproj` file is convenient because other packages that have been installed into those project are automatically referenced as dependencies.</span></span> <span data-ttu-id="ea690-227">Jednoduše použijte následující příkaz ve stejné složce jako soubor projektu:</span><span class="sxs-lookup"><span data-stu-id="ea690-227">Simply use the following command in the same folder as the project file:</span></span>

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

<span data-ttu-id="ea690-228">Výsledný `<project-name>.nuspec` soubor obsahuje *tokeny,* které jsou nahrazeny v době balení s hodnotami z projektu, včetně odkazů na všechny ostatní balíčky, které již byly nainstalovány.</span><span class="sxs-lookup"><span data-stu-id="ea690-228">The resulting `<project-name>.nuspec` file contains *tokens* that are replaced at packaging time with values from the project, including references to any other packages that have already been installed.</span></span>

<span data-ttu-id="ea690-229">Pokud máte balíčky závislostí zahrnout do *.nuspec*, místo toho použít `nuget pack`a získat soubor *.nuspec* z v rámci generovaného souboru *.nupkg.*</span><span class="sxs-lookup"><span data-stu-id="ea690-229">If you have package dependencies to include in the *.nuspec*, instead use `nuget pack`, and get the *.nuspec* file from within the generated *.nupkg* file.</span></span> <span data-ttu-id="ea690-230">Použijte například následující příkaz.</span><span class="sxs-lookup"><span data-stu-id="ea690-230">For example, use the following command.</span></span>

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget pack myproject.csproj
```

<span data-ttu-id="ea690-231">Token je oddělen `$` symboly na obou stranách vlastnosti projektu.</span><span class="sxs-lookup"><span data-stu-id="ea690-231">A token is delimited by `$` symbols on both sides of the project property.</span></span> <span data-ttu-id="ea690-232">Například `<id>` hodnota v manifestu generované tímto způsobem se obvykle zobrazí takto:</span><span class="sxs-lookup"><span data-stu-id="ea690-232">For example, the `<id>` value in a manifest generated in this way typically appears as follows:</span></span>

```xml
<id>$id$</id>
```

<span data-ttu-id="ea690-233">Tento token je nahrazen `AssemblyName` hodnotou ze souboru projektu v době balení.</span><span class="sxs-lookup"><span data-stu-id="ea690-233">This token is replaced with the `AssemblyName` value from the project file at packing time.</span></span> <span data-ttu-id="ea690-234">Přesné mapování hodnot projektu `.nuspec` na tokeny naleznete v [odkazu na tokeny nahrazení tokenů](../reference/nuspec.md#replacement-tokens).</span><span class="sxs-lookup"><span data-stu-id="ea690-234">For the exact mapping of project values to `.nuspec` tokens, see the [Replacement Tokens reference](../reference/nuspec.md#replacement-tokens).</span></span>

<span data-ttu-id="ea690-235">Tokeny vás zbaví nutnosti aktualizovat klíčové hodnoty, `.nuspec` jako je číslo verze při aktualizaci projektu.</span><span class="sxs-lookup"><span data-stu-id="ea690-235">Tokens relieve you from needing to update crucial values like the version number in the `.nuspec` as you update the project.</span></span> <span data-ttu-id="ea690-236">(Tokeny můžete vždy v případě potřeby nahradit literálovými hodnotami).</span><span class="sxs-lookup"><span data-stu-id="ea690-236">(You can always replace the tokens with literal values, if desired).</span></span> 

<span data-ttu-id="ea690-237">Všimněte si, že existuje několik dalších možností balení k dispozici při práci z projektu sady Visual Studio, jak je popsáno v [spuštění nuget pack pro generování souboru .nupkg](#run-nuget-pack-to-generate-the-nupkg-file) později.</span><span class="sxs-lookup"><span data-stu-id="ea690-237">Note that there are several additional packaging options available when working from a Visual Studio project, as described in [Running nuget pack to generate the .nupkg file](#run-nuget-pack-to-generate-the-nupkg-file) later on.</span></span>

#### <a name="solution-level-packages"></a><span data-ttu-id="ea690-238">Balíčky na úrovni řešení</span><span class="sxs-lookup"><span data-stu-id="ea690-238">Solution-level packages</span></span>

<span data-ttu-id="ea690-239">*Pouze NuGet 2.x. Není k dispozici v NuGet 3.0+.*</span><span class="sxs-lookup"><span data-stu-id="ea690-239">*NuGet 2.x only. Not available in NuGet 3.0+.*</span></span>

<span data-ttu-id="ea690-240">NuGet 2.x podporuje pojem balíček na úrovni řešení, který nainstaluje nástroje nebo `tools` další příkazy pro konzolu Správce balíčků (obsah složky), ale nepřidává odkazy, obsah nebo sestavení vlastního nastavení pro všechny projekty v řešení.</span><span class="sxs-lookup"><span data-stu-id="ea690-240">NuGet 2.x supported the notion of a solution-level package that installs tools or additional commands for the Package Manager Console (the contents of the `tools` folder), but does not add references, content, or build customizations to any projects in the solution.</span></span> <span data-ttu-id="ea690-241">Tyto balíčky neobsahují `lib`žádné `content`soubory `build` v jeho přímé , nebo složky `lib` `content`a `build` žádný z jeho závislostí mají soubory v jejich příslušné , , nebo složky.</span><span class="sxs-lookup"><span data-stu-id="ea690-241">Such packages contain no files in its direct `lib`, `content`, or `build` folders, and none of its dependencies have files in their respective `lib`, `content`, or `build` folders.</span></span>

<span data-ttu-id="ea690-242">NuGet sleduje nainstalované balíčky `packages.config` na `.nuget` úrovni řešení v souboru `packages.config` ve složce, nikoli soubor projektu.</span><span class="sxs-lookup"><span data-stu-id="ea690-242">NuGet tracks installed solution-level packages in a `packages.config` file in the `.nuget` folder, rather than the project's `packages.config` file.</span></span>

### <a name="new-file-with-default-values"></a><span data-ttu-id="ea690-243">Nový soubor s výchozími hodnotami</span><span class="sxs-lookup"><span data-stu-id="ea690-243">New file with default values</span></span>

<span data-ttu-id="ea690-244">Následující příkaz vytvoří výchozí manifest se zástupnými symboly, který zajistí, že začnete se správnou strukturou souboru:</span><span class="sxs-lookup"><span data-stu-id="ea690-244">The following command creates a default manifest with placeholders, which ensures you start with the proper file structure:</span></span>

```cli
nuget spec [<package-name>]
```

<span data-ttu-id="ea690-245">Pokud vyneche \<\>název balíčku , `Package.nuspec`výsledný soubor je .</span><span class="sxs-lookup"><span data-stu-id="ea690-245">If you omit \<package-name\>, the resulting file is `Package.nuspec`.</span></span> <span data-ttu-id="ea690-246">Pokud zadáte název, `Contoso.Utility.UsefulStuff`například , `Contoso.Utility.UsefulStuff.nuspec`soubor je .</span><span class="sxs-lookup"><span data-stu-id="ea690-246">If you provide a name such as `Contoso.Utility.UsefulStuff`, the file is `Contoso.Utility.UsefulStuff.nuspec`.</span></span>

<span data-ttu-id="ea690-247">Výsledek `.nuspec` obsahuje zástupné symboly `projectUrl`pro hodnoty, jako je .</span><span class="sxs-lookup"><span data-stu-id="ea690-247">The resulting `.nuspec` contains placeholders for values like the `projectUrl`.</span></span> <span data-ttu-id="ea690-248">Nezapomeňte soubor upravit, než soubor použijete `.nupkg` k vytvoření konečného souboru.</span><span class="sxs-lookup"><span data-stu-id="ea690-248">Be sure to edit the file before using it to create the final `.nupkg` file.</span></span>

## <a name="choose-a-unique-package-identifier-and-setting-the-version-number"></a><span data-ttu-id="ea690-249">Zvolte jedinečný identifikátor balíčku a nastavení čísla verze</span><span class="sxs-lookup"><span data-stu-id="ea690-249">Choose a unique package identifier and setting the version number</span></span>

<span data-ttu-id="ea690-250">Identifikátor balíčku`<id>` (element) a číslo`<version>` verze ( element) jsou dvě nejdůležitější hodnoty v manifestu, protože jednoznačně identifikují přesný kód, který je obsažen v balíčku.</span><span class="sxs-lookup"><span data-stu-id="ea690-250">The package identifier (`<id>` element) and the version number (`<version>` element) are the two most important values in the manifest because they uniquely identify the exact code that's contained in the package.</span></span>

<span data-ttu-id="ea690-251">**Doporučené postupy pro identifikátor balíčku:**</span><span class="sxs-lookup"><span data-stu-id="ea690-251">**Best practices for the package identifier:**</span></span>

- <span data-ttu-id="ea690-252">**Jedinečnost**: Identifikátor musí být jedinečný v celé nuget.org nebo v jakékoli galerii, která balíček hostuje.</span><span class="sxs-lookup"><span data-stu-id="ea690-252">**Uniqueness**: The identifier must be unique across nuget.org or whatever gallery hosts the package.</span></span> <span data-ttu-id="ea690-253">Než se rozhodnete pro identifikátor, vyhledejte v příslušné galerii, zda je název již používán.</span><span class="sxs-lookup"><span data-stu-id="ea690-253">Before deciding on an identifier, search the applicable gallery to check if the name is already in use.</span></span> <span data-ttu-id="ea690-254">Chcete-li se vyhnout konfliktům, je dobrým vzorem použití názvu společnosti `Contoso.`jako první části identifikátoru, například .</span><span class="sxs-lookup"><span data-stu-id="ea690-254">To avoid conflicts, a good pattern is to use your company name as the first part of the identifier, such as `Contoso.`.</span></span>
- <span data-ttu-id="ea690-255">**Názvy podobné oboru názvů**: Postupujte podle vzoru podobného oborům názvů v rozhraní .NET pomocí tečkového zápisu místo spojovníků.</span><span class="sxs-lookup"><span data-stu-id="ea690-255">**Namespace-like names**: Follow a pattern similar to namespaces in .NET, using dot notation instead of hyphens.</span></span> <span data-ttu-id="ea690-256">Například použijte `Contoso.Utility.UsefulStuff` spíše `Contoso-Utility-UsefulStuff` `Contoso_Utility_UsefulStuff`než nebo .</span><span class="sxs-lookup"><span data-stu-id="ea690-256">For example, use `Contoso.Utility.UsefulStuff` rather than `Contoso-Utility-UsefulStuff` or `Contoso_Utility_UsefulStuff`.</span></span> <span data-ttu-id="ea690-257">Spotřebitelé také najít užitečné, když identifikátor balíčku odpovídá obory názvů používané v kódu.</span><span class="sxs-lookup"><span data-stu-id="ea690-257">Consumers also find it helpful when the package identifier matches the namespaces used in the code.</span></span>
- <span data-ttu-id="ea690-258">**Ukázkové balíčky**: Pokud vytvoříte balíček ukázkový kód, `.Sample` který ukazuje, jak používat jiný `Contoso.Utility.UsefulStuff.Sample`balíček, připojte jako příponu k identifikátoru, jako v .</span><span class="sxs-lookup"><span data-stu-id="ea690-258">**Sample Packages**: If you produce a package of sample code that demonstrates how to use another package, attach `.Sample` as a suffix to the identifier, as in `Contoso.Utility.UsefulStuff.Sample`.</span></span> <span data-ttu-id="ea690-259">(Ukázkový balíček by samozřejmě měl závislost na druhém balíčku.) Při vytváření ukázkového balíčku použijte metodu pracovního adresáře založenou na konvencích, která byla popsána výše.</span><span class="sxs-lookup"><span data-stu-id="ea690-259">(The sample package would of course have a dependency on the other package.) When creating a sample package, use the convention-based working directory method described earlier.</span></span> <span data-ttu-id="ea690-260">Ve `content` složce uspořádejte ukázkový `\Samples\<identifier>` kód `\Samples\Contoso.Utility.UsefulStuff.Sample`do složky volané jako v .</span><span class="sxs-lookup"><span data-stu-id="ea690-260">In the `content` folder, arrange the sample code in a folder called `\Samples\<identifier>` as in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span></span>

<span data-ttu-id="ea690-261">**Doporučené postupy pro verzi balíčku:**</span><span class="sxs-lookup"><span data-stu-id="ea690-261">**Best practices for the package version:**</span></span>

- <span data-ttu-id="ea690-262">Obecně platí, že nastavte verzi balíčku tak, aby odpovídala knihovně, i když to není nezbytně nutné.</span><span class="sxs-lookup"><span data-stu-id="ea690-262">In general, set the version of the package to match the library, though this is not strictly required.</span></span> <span data-ttu-id="ea690-263">Toto je jednoduchá záležitost, když omezíte balíček na jedno sestavení, jak je popsáno výše v [rozhodnutí, která sestavení balíček](#decide-which-assemblies-to-package).</span><span class="sxs-lookup"><span data-stu-id="ea690-263">This is a simple matter when you limit a package to a single assembly, as described earlier in [Deciding which assemblies to package](#decide-which-assemblies-to-package).</span></span> <span data-ttu-id="ea690-264">Celkově nezapomeňte, že NuGet sám se zabývá verze balíčků při řešení závislostí, nikoli verze sestavení.</span><span class="sxs-lookup"><span data-stu-id="ea690-264">Overall, remember that NuGet itself deals with package versions when resolving dependencies, not assembly versions.</span></span>
- <span data-ttu-id="ea690-265">Při použití nestandardní verze schématu, nezapomeňte zvážit NuGet pravidla správy verzí, jak je vysvětleno v [package versioning](../concepts/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="ea690-265">When using a non-standard version scheme, be sure to consider the NuGet versioning rules as explained in [Package versioning](../concepts/package-versioning.md).</span></span>

> <span data-ttu-id="ea690-266">Následující série krátkých blogových příspěvků je také užitečná pro pochopení správy verzí:</span><span class="sxs-lookup"><span data-stu-id="ea690-266">The following series of brief blog posts are also helpful to understand versioning:</span></span>
>
> - [<span data-ttu-id="ea690-267">Část 1: Převzetí DLL Hell</span><span class="sxs-lookup"><span data-stu-id="ea690-267">Part 1: Taking on DLL Hell</span></span>](https://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [<span data-ttu-id="ea690-268">Část 2: Základní algoritmus</span><span class="sxs-lookup"><span data-stu-id="ea690-268">Part 2: The core algorithm</span></span>](https://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [<span data-ttu-id="ea690-269">Část 3: Sjednocení prostřednictvím závazných přesměrování</span><span class="sxs-lookup"><span data-stu-id="ea690-269">Part 3: Unification via Binding Redirects</span></span>](https://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="add-a-readme-and-other-files"></a><span data-ttu-id="ea690-270">Přidání souboru readme a dalších souborů</span><span class="sxs-lookup"><span data-stu-id="ea690-270">Add a readme and other files</span></span>

<span data-ttu-id="ea690-271">Chcete-li přímo určit soubory, které `<files>` mají být `.nuspec` zahrnuty do `<metadata>` balíčku, použijte uzel v souboru, který následuje *za* značkou:</span><span class="sxs-lookup"><span data-stu-id="ea690-271">To directly specify files to include in the package, use the `<files>` node in the `.nuspec` file, which *follows* the `<metadata>` tag:</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
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
> <span data-ttu-id="ea690-272">Při použití přístupu pracovního adresáře založeného na konvencích můžete soubor readme.txt umístit do kořenového adresáře balíčku a dalšího obsahu ve `content` složce.</span><span class="sxs-lookup"><span data-stu-id="ea690-272">When using the convention-based working directory approach, you can place the readme.txt in the package root and other content in the `content` folder.</span></span> <span data-ttu-id="ea690-273">V `<file>` manifestu nejsou nutné žádné prvky.</span><span class="sxs-lookup"><span data-stu-id="ea690-273">No `<file>` elements are necessary in the manifest.</span></span>

<span data-ttu-id="ea690-274">Když zahrnete `readme.txt` soubor pojmenovaný do kořenového adresáře balíčku, Visual Studio zobrazí obsah tohoto souboru jako prostý text ihned po instalaci balíčku přímo.</span><span class="sxs-lookup"><span data-stu-id="ea690-274">When you include a file named `readme.txt` in the package root, Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="ea690-275">(Soubory Readme se nezobrazují pro balíčky nainstalované jako závislosti).</span><span class="sxs-lookup"><span data-stu-id="ea690-275">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="ea690-276">Například zde je návod, jak se zobrazí readme pro balíček HtmlAgilityPack:</span><span class="sxs-lookup"><span data-stu-id="ea690-276">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Zobrazení souboru readme pro balíček NuGet při instalaci](media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="ea690-278">Pokud do `<files>` `.nuspec` souboru zahrnete prázdný uzel, NuGet nezahrne do balíčku žádný `lib` jiný obsah než co je ve složce.</span><span class="sxs-lookup"><span data-stu-id="ea690-278">If you include an empty `<files>` node in the `.nuspec` file, NuGet doesn't include any other content in the package other than what's in the `lib` folder.</span></span>

## <a name="include-msbuild-props-and-targets-in-a-package"></a><span data-ttu-id="ea690-279">Zahrnout rekvizity a cíle MSBuild do balíčku</span><span class="sxs-lookup"><span data-stu-id="ea690-279">Include MSBuild props and targets in a package</span></span>

<span data-ttu-id="ea690-280">V některých případech můžete chtít přidat vlastní cíle sestavení nebo vlastnosti v projektech, které spotřebovávají váš balíček, jako je například spuštění vlastního nástroje nebo procesu během sestavení.</span><span class="sxs-lookup"><span data-stu-id="ea690-280">In some cases, you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="ea690-281">To provést umístěním souborů `<package_id>.targets` ve `<package_id>.props` formuláři `Contoso.Utility.UsefulStuff.targets`nebo `\build` (například ) do složky projektu.</span><span class="sxs-lookup"><span data-stu-id="ea690-281">You do this by placing files in the form `<package_id>.targets` or `<package_id>.props` (such as `Contoso.Utility.UsefulStuff.targets`) within the `\build` folder of the project.</span></span>

<span data-ttu-id="ea690-282">Soubory v `\build` kořenové složce jsou považovány za vhodné pro všechny cílové architektury.</span><span class="sxs-lookup"><span data-stu-id="ea690-282">Files in the root `\build` folder are considered suitable for all target frameworks.</span></span> <span data-ttu-id="ea690-283">Chcete-li poskytnout soubory specifické pro architekturu, umístěte je nejprve do příslušných podsložek, například následující:</span><span class="sxs-lookup"><span data-stu-id="ea690-283">To provide framework-specific files, first place them within appropriate subfolders, such as the following:</span></span>

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

<span data-ttu-id="ea690-284">Pak v `.nuspec` souboru, ujistěte se, `<files>` že odkazovat na tyto soubory v uzlu:</span><span class="sxs-lookup"><span data-stu-id="ea690-284">Then in the `.nuspec` file, be sure to refer to these files in the `<files>` node:</span></span>

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

<span data-ttu-id="ea690-285">Včetně MSBuild rekvizity a cíle v balíčku byla [zavedena s NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), proto se doporučuje přidat `minClientVersion="2.5"` atribut do `metadata` prvku, k označení minimální verze klienta NuGet potřebné ke spotřebě balíčku.</span><span class="sxs-lookup"><span data-stu-id="ea690-285">Including MSBuild props and targets in a package was [introduced with NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), therefore it is recommended to add the `minClientVersion="2.5"` attribute to the `metadata` element, to indicate the minimum NuGet client version required to consume the package.</span></span>

<span data-ttu-id="ea690-286">Když NuGet nainstaluje `\build` balíček se soubory, `<Import>` přidá prvky MSBuild v souboru projektu směřující na soubory `.targets` a. `.props`</span><span class="sxs-lookup"><span data-stu-id="ea690-286">When NuGet installs a package with `\build` files, it adds MSBuild `<Import>` elements in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="ea690-287">(`.props` je přidán v horní části souboru projektu; `.targets` je přidán v dolní části.) Pro každý cílový `<Import>` rámec je přidán samostatný podmíněný prvek MSBuild.</span><span class="sxs-lookup"><span data-stu-id="ea690-287">(`.props` is added at the top of the project file; `.targets` is added at the bottom.) A separate conditional MSBuild `<Import>` element is added for each target framework.</span></span>

<span data-ttu-id="ea690-288">MSBuild `.props` `.targets` a soubory pro cílení mezi rámci `\buildMultiTargeting` lze umístit do složky.</span><span class="sxs-lookup"><span data-stu-id="ea690-288">MSBuild `.props` and `.targets` files for cross-framework targeting can be placed in the `\buildMultiTargeting` folder.</span></span> <span data-ttu-id="ea690-289">Během instalace balíčku NuGet `<Import>` přidá odpovídající prvky do souboru projektu s podmínkou, že `$(TargetFramework)` cílová architektura není nastavena (MSBuild vlastnost musí být prázdný).</span><span class="sxs-lookup"><span data-stu-id="ea690-289">During package installation, NuGet adds the corresponding `<Import>` elements to the project file with the condition, that the target framework is not set (the MSBuild property `$(TargetFramework)` must be empty).</span></span>

<span data-ttu-id="ea690-290">S NuGet 3.x cíle nejsou přidány do projektu, `{projectName}.nuget.g.targets` ale `{projectName}.nuget.g.props`jsou k dispozici prostřednictvím a .</span><span class="sxs-lookup"><span data-stu-id="ea690-290">With NuGet 3.x, targets are not added to the project but are instead made available through `{projectName}.nuget.g.targets` and `{projectName}.nuget.g.props`.</span></span>

## <a name="run-nuget-pack-to-generate-the-nupkg-file"></a><span data-ttu-id="ea690-291">Spuštěním balíčku nuget pro generování souboru .nupkg</span><span class="sxs-lookup"><span data-stu-id="ea690-291">Run nuget pack to generate the .nupkg file</span></span>

<span data-ttu-id="ea690-292">Při použití sestavení nebo pracovního adresáře založeného `nuget pack` na `.nuspec` konventu `<project-name>` vytvořte balíček spuštěním se souborem a nahrazením určitým názvem souboru:</span><span class="sxs-lookup"><span data-stu-id="ea690-292">When using an assembly or the convention-based working directory, create a package by running `nuget pack` with your `.nuspec` file, replacing `<project-name>` with your specific filename:</span></span>

```cli
nuget pack <project-name>.nuspec
```

<span data-ttu-id="ea690-293">Při použití projektu sady `nuget pack` Visual Studio spusťte s souborem `.nuspec` projektu, který automaticky načte soubor projektu a nahradí všechny tokeny v něm pomocí hodnot v souboru projektu:</span><span class="sxs-lookup"><span data-stu-id="ea690-293">When using a Visual Studio project, run `nuget pack` with your project file, which automatically loads the project's `.nuspec` file and replaces any tokens within it using values in the project file:</span></span>

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> <span data-ttu-id="ea690-294">Použití souboru projektu přímo je nezbytné pro nahrazení tokenu, protože projekt je zdrojem hodnot tokenu.</span><span class="sxs-lookup"><span data-stu-id="ea690-294">Using the project file directly is necessary for token replacement because the project is the source of the token values.</span></span> <span data-ttu-id="ea690-295">Nahrazení tokenu se nestane, pokud používáte `nuget pack` se souborem. `.nuspec`</span><span class="sxs-lookup"><span data-stu-id="ea690-295">Token replacement does not happen if you use `nuget pack` with a `.nuspec` file.</span></span>

<span data-ttu-id="ea690-296">Ve všech `nuget pack` případech nezahrnuje složky začínající tečkou, například `.git` nebo `.hg`.</span><span class="sxs-lookup"><span data-stu-id="ea690-296">In all cases, `nuget pack` excludes folders that start with a period, such as `.git` or `.hg`.</span></span>

<span data-ttu-id="ea690-297">NuGet označuje, pokud jsou `.nuspec` nějaké chyby v souboru, které je třeba opravit, například zapomínání změnit zástupné hodnoty v manifestu.</span><span class="sxs-lookup"><span data-stu-id="ea690-297">NuGet indicates if there are any errors in the `.nuspec` file that need correcting, such as forgetting to change placeholder values in the manifest.</span></span>

<span data-ttu-id="ea690-298">Jakmile `nuget pack` uspějete, máte `.nupkg` soubor, který můžete publikovat do vhodné galerie, jak je popsáno v publikování [balíčku](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="ea690-298">Once `nuget pack` succeeds, you have a `.nupkg` file that you can publish to a suitable gallery as described in [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

> [!Tip]
> <span data-ttu-id="ea690-299">Užitečným způsobem, jak zkontrolovat balíček po jeho vytvoření, je otevřít jej v nástroji [Průzkumník balíčků.](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)</span><span class="sxs-lookup"><span data-stu-id="ea690-299">A helpful way to examine a package after creating it is to open it in the [Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) tool.</span></span> <span data-ttu-id="ea690-300">To vám dává grafické zobrazení obsahu balíčku a jeho manifestu.</span><span class="sxs-lookup"><span data-stu-id="ea690-300">This gives you a graphical view of the package contents and its manifest.</span></span> <span data-ttu-id="ea690-301">Výsledný `.nupkg` soubor můžete také přejmenovat `.zip` na soubor a přímo prozkoumat jeho obsah.</span><span class="sxs-lookup"><span data-stu-id="ea690-301">You can also rename the resulting `.nupkg` file to a `.zip` file and explore its contents directly.</span></span>

### <a name="additional-options"></a><span data-ttu-id="ea690-302">Další možnosti</span><span class="sxs-lookup"><span data-stu-id="ea690-302">Additional options</span></span>

<span data-ttu-id="ea690-303">Můžete použít různé přepínače `nuget pack` příkazového řádku s vyloučit soubory, přepsat číslo verze v manifestu a změnit výstupní složku, mimo jiné funkce.</span><span class="sxs-lookup"><span data-stu-id="ea690-303">You can use various command-line switches with `nuget pack` to exclude files, override the version number in the manifest, and change the output folder, among other features.</span></span> <span data-ttu-id="ea690-304">Úplný seznam naleznete v [odkazu na příkaz balení](../reference/cli-reference/cli-ref-pack.md).</span><span class="sxs-lookup"><span data-stu-id="ea690-304">For a complete list, refer to the [pack command reference](../reference/cli-reference/cli-ref-pack.md).</span></span>

<span data-ttu-id="ea690-305">Následující možnosti jsou některé, které jsou společné s projekty sady Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="ea690-305">The following options are a few that are common with Visual Studio projects:</span></span>

- <span data-ttu-id="ea690-306">**Odkazované projekty**: Pokud projekt odkazuje na jiné projekty, můžete přidat odkazované projekty jako `-IncludeReferencedProjects` součást balíčku nebo jako závislosti pomocí možnosti:</span><span class="sxs-lookup"><span data-stu-id="ea690-306">**Referenced projects**: If the project references other projects, you can add the referenced projects as part of the package, or as dependencies, by using the `-IncludeReferencedProjects` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    <span data-ttu-id="ea690-307">Tento proces zahrnutí je rekurzivní, takže pokud `MyProject.csproj` odkazuje na projekty B a C a tyto projekty odkazují na D, E a F, pak jsou do balíčku zahrnuty soubory z B, C, D, E a F.</span><span class="sxs-lookup"><span data-stu-id="ea690-307">This inclusion process is recursive, so if `MyProject.csproj` references projects B and C, and those projects reference D, E, and F, then files from B, C, D, E, and F are included in the package.</span></span>

    <span data-ttu-id="ea690-308">Pokud odkazovaný projekt `.nuspec` obsahuje vlastní soubor, pak NuGet přidá tento odkazovaný projekt jako závislost místo.</span><span class="sxs-lookup"><span data-stu-id="ea690-308">If a referenced project includes a `.nuspec` file of its own, then NuGet adds that referenced project as a dependency instead.</span></span>  <span data-ttu-id="ea690-309">Je třeba balíček a publikovat tento projekt samostatně.</span><span class="sxs-lookup"><span data-stu-id="ea690-309">You need to package and publish that project separately.</span></span>

- <span data-ttu-id="ea690-310">**Konfigurace sestavení**: Ve výchozím nastavení používá nuget výchozí konfigurační sadu sestavení v souboru projektu, obvykle *ladění*.</span><span class="sxs-lookup"><span data-stu-id="ea690-310">**Build configuration**: By default, NuGet uses the default build configuration set in the project file, typically *Debug*.</span></span> <span data-ttu-id="ea690-311">Chcete-li zabalit soubory z jiné konfigurace `-properties` sestavení, jako je *například release*, použijte tuto možnost s konfigurací:</span><span class="sxs-lookup"><span data-stu-id="ea690-311">To pack files from a different build configuration, such as *Release*, use the `-properties` option with the configuration:</span></span>

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- <span data-ttu-id="ea690-312">**Symboly**: chcete-li zahrnout symboly, které umožňují spotřebitelům `-Symbols` krokovat kód balíčku v ladicím programu, použijte možnost:</span><span class="sxs-lookup"><span data-stu-id="ea690-312">**Symbols**: to include symbols that allow consumers to step through your package code in the debugger, use the `-Symbols` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="test-package-installation"></a><span data-ttu-id="ea690-313">Instalace testovacího balíčku</span><span class="sxs-lookup"><span data-stu-id="ea690-313">Test package installation</span></span>

<span data-ttu-id="ea690-314">Před publikováním balíčku obvykle chcete otestovat proces instalace balíčku do projektu.</span><span class="sxs-lookup"><span data-stu-id="ea690-314">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="ea690-315">Testy ujistěte se, že nutně soubory všechny skončí na jejich správných místech v projektu.</span><span class="sxs-lookup"><span data-stu-id="ea690-315">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="ea690-316">Instalace můžete testovat ručně v sadě Visual Studio nebo na příkazovém řádku pomocí běžných [kroků instalace balíčku](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span><span class="sxs-lookup"><span data-stu-id="ea690-316">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

<span data-ttu-id="ea690-317">Pro automatizované testování je základní proces následující:</span><span class="sxs-lookup"><span data-stu-id="ea690-317">For automated testing, the basic process is as follows:</span></span>

1. <span data-ttu-id="ea690-318">Zkopírujte `.nupkg` soubor do místní složky.</span><span class="sxs-lookup"><span data-stu-id="ea690-318">Copy the `.nupkg` file to a local folder.</span></span>
1. <span data-ttu-id="ea690-319">Přidejte složku do zdrojů `nuget sources add -name <name> -source <path>` balíčku pomocí příkazu (viz [nuget zdroje](../reference/cli-reference/cli-ref-sources.md)).</span><span class="sxs-lookup"><span data-stu-id="ea690-319">Add the folder to your package sources using the `nuget sources add -name <name> -source <path>` command (see [nuget sources](../reference/cli-reference/cli-ref-sources.md)).</span></span> <span data-ttu-id="ea690-320">Všimněte si, že stačí nastavit tento místní zdroj pouze jednou v daném počítači.</span><span class="sxs-lookup"><span data-stu-id="ea690-320">Note that you need only set this local source once on any given computer.</span></span>
1. <span data-ttu-id="ea690-321">Nainstalujte balíček z `nuget install <packageID> -source <name>` `<name>` tohoto zdroje pomocí místa, `nuget sources`kde odpovídá názvu zdroje, jak je uvedeno na .</span><span class="sxs-lookup"><span data-stu-id="ea690-321">Install the package from that source using `nuget install <packageID> -source <name>` where `<name>` matches the name of your source as given to `nuget sources`.</span></span> <span data-ttu-id="ea690-322">Zadání zdroje zajišťuje, že balíček je nainstalován z tohoto zdroje sám.</span><span class="sxs-lookup"><span data-stu-id="ea690-322">Specifying the source ensures that the package is installed from that source alone.</span></span>
1. <span data-ttu-id="ea690-323">Zkontrolujte systém souborů a zkontrolujte, zda jsou soubory nainstalovány správně.</span><span class="sxs-lookup"><span data-stu-id="ea690-323">Examine your file system to check that files are installed correctly.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea690-324">Další kroky</span><span class="sxs-lookup"><span data-stu-id="ea690-324">Next Steps</span></span>

<span data-ttu-id="ea690-325">Po vytvoření balíčku, což je `.nupkg` soubor, můžete jej publikovat do galerie podle vašeho výběru, jak je popsáno na [publikování balíčku](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="ea690-325">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="ea690-326">Můžete také rozšířit možnosti balíčku nebo jinak podporovat jiné scénáře, jak je popsáno v následujících tématech:</span><span class="sxs-lookup"><span data-stu-id="ea690-326">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="ea690-327">Správa verzí balíčku</span><span class="sxs-lookup"><span data-stu-id="ea690-327">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="ea690-328">Podpora více cílových architektur</span><span class="sxs-lookup"><span data-stu-id="ea690-328">Supporting multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="ea690-329">Transformace zdrojových a konfiguračních souborů</span><span class="sxs-lookup"><span data-stu-id="ea690-329">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="ea690-330">Lokalizace</span><span class="sxs-lookup"><span data-stu-id="ea690-330">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="ea690-331">Předběžné verze</span><span class="sxs-lookup"><span data-stu-id="ea690-331">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="ea690-332">Nastavení typu balíčku</span><span class="sxs-lookup"><span data-stu-id="ea690-332">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="ea690-333">Vytváření balíčků pomocí meziop sestavení COM</span><span class="sxs-lookup"><span data-stu-id="ea690-333">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="ea690-334">Nakonec existují další typy balíčků, které mají být vědomi:</span><span class="sxs-lookup"><span data-stu-id="ea690-334">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="ea690-335">Nativní balíčky</span><span class="sxs-lookup"><span data-stu-id="ea690-335">Native Packages</span></span>](../guides/native-packages.md)
- [<span data-ttu-id="ea690-336">Balíčky symbolů</span><span class="sxs-lookup"><span data-stu-id="ea690-336">Symbol Packages</span></span>](../create-packages/symbol-packages-snupkg.md)
