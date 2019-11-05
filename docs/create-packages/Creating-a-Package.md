---
title: Vytvoření balíčku NuGet pomocí NuGet. exe CLI
description: Podrobný průvodce procesem navrhování a vytváření balíčku NuGet, včetně klíčových bodů rozhodování, jako jsou soubory a správa verzí.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 12ecfb8374c43a04d57d32575556adebc991d053
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610693"
---
# <a name="create-a-package-using-the-nugetexe-cli"></a><span data-ttu-id="5d4a8-103">Vytvoření balíčku pomocí rozhraní příkazového řádku NuGet. exe</span><span class="sxs-lookup"><span data-stu-id="5d4a8-103">Create a package using the nuget.exe CLI</span></span>

<span data-ttu-id="5d4a8-104">Bez ohledu na to, co váš balíček obsahuje, nebo jaký kód obsahuje, použijte jeden z nástrojů rozhraní příkazového řádku `nuget.exe` nebo `dotnet.exe` a zabalit tuto funkci do komponenty, kterou lze sdílet s a používat v jakémkoli počtu jiných vývojářů.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-104">No matter what your package does or what code it contains, you use one of the CLI tools, either `nuget.exe` or `dotnet.exe`, to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="5d4a8-105">Pokud chcete nainstalovat nástroje NuGet CLI, přečtěte si téma [Instalace nástrojů klienta NuGet](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="5d4a8-105">To install NuGet CLI tools, see [Install NuGet client tools](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="5d4a8-106">Všimněte si, že Visual Studio nezahrnuje automaticky nástroj CLI.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-106">Note that Visual Studio does not automatically include a CLI tool.</span></span>

- <span data-ttu-id="5d4a8-107">Pro projekty, které nejsou ve stylu sady SDK, obvykle .NET Framework projekty, postupujte podle kroků popsaných v tomto článku a vytvořte balíček.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-107">For non-SDK-style projects, typically .NET Framework projects, follow the steps described in this article to create a package.</span></span> <span data-ttu-id="5d4a8-108">Podrobné pokyny k používání sady Visual Studio a `nuget.exe` CLI najdete v tématu [Vytvoření a publikování .NET Framework balíčku](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md).</span><span class="sxs-lookup"><span data-stu-id="5d4a8-108">For step-by-step instructions using Visual Studio and the `nuget.exe` CLI, see [Create and publish a .NET Framework package](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md).</span></span>

- <span data-ttu-id="5d4a8-109">Pro projekty .NET Core a .NET Standard, které používají [Formát ve stylu sady SDK](../resources/check-project-format.md), a všechny další projekty ve stylu sady SDK, přečtěte si téma [Vytvoření balíčku NuGet pomocí rozhraní příkazového řádku dotnet](creating-a-package-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="5d4a8-109">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, see [Create a NuGet package using the dotnet CLI](creating-a-package-dotnet-cli.md).</span></span>

- <span data-ttu-id="5d4a8-110">Pro projekty migrované z `packages.config` do [PackageReference](../consume-packages/package-references-in-project-files.md)použijte [MSBuild-t:Pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span><span class="sxs-lookup"><span data-stu-id="5d4a8-110">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

<span data-ttu-id="5d4a8-111">Technicky řečeno, balíček NuGet je jenom soubor ZIP, který se přejmenoval s příponou `.nupkg` a jehož obsah se shoduje s některými úmluvami.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-111">Technically speaking, a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension and whose contents match certain conventions.</span></span> <span data-ttu-id="5d4a8-112">Toto téma popisuje podrobný proces vytváření balíčku, který splňuje tyto konvence.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-112">This topic describes the detailed process of creating a package that meets those conventions.</span></span>

<span data-ttu-id="5d4a8-113">Balení začíná kompilovaným kódem (sestavení), symboly a/nebo dalšími soubory, které chcete doručit jako balíček (viz [Přehled a pracovní postup](overview-and-workflow.md)).</span><span class="sxs-lookup"><span data-stu-id="5d4a8-113">Packaging begins with the compiled code (assemblies), symbols, and/or other files that you want to deliver as a package (see [Overview and workflow](overview-and-workflow.md)).</span></span> <span data-ttu-id="5d4a8-114">Tento proces je nezávislý na kompilování nebo jinak generují soubory, které se nacházejí v balíčku, i když můžete kreslit z informací v souboru projektu, aby se zkompilované sestavení a balíčky udržovaly synchronizované.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-114">This process is independent from compiling or otherwise generating the files that go into the package, although you can draw from information in a project file to keep the compiled assemblies and packages in sync.</span></span>

> [!Important]
> <span data-ttu-id="5d4a8-115">Toto téma se vztahuje na projekty nevyužívající sadu SDK, obvykle v jiných projektech než .NET Core a .NET Standard projekty pomocí sady Visual Studio 2017 a novějších verzí a NuGet 4.0 +.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-115">This topic applies to non-SDK-style projects, typically projects other than .NET Core and .NET Standard projects using Visual Studio 2017 and higher versions and NuGet 4.0+.</span></span>

## <a name="decide-which-assemblies-to-package"></a><span data-ttu-id="5d4a8-116">Rozhodněte, která sestavení se mají zabalit</span><span class="sxs-lookup"><span data-stu-id="5d4a8-116">Decide which assemblies to package</span></span>

<span data-ttu-id="5d4a8-117">Většina balíčků pro obecné účely obsahuje jedno nebo více sestavení, která mohou používat jiní vývojáři ve svých vlastních projektech.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-117">Most general-purpose packages contain one or more assemblies that other developers can use in their own projects.</span></span>

- <span data-ttu-id="5d4a8-118">Obecně je vhodné mít jedno sestavení pro každý balíček NuGet za předpokladu, že každé sestavení je nezávisle užitečné.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-118">In general, it's best to have one assembly per NuGet package, provided that each assembly is independently useful.</span></span> <span data-ttu-id="5d4a8-119">Například pokud máte `Utilities.dll`, který závisí na `Parser.dll`, a `Parser.dll` je užitečné na vlastní a pak pro každou z nich vytvořit jeden balíček.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-119">For example, if you have a `Utilities.dll` that depends on `Parser.dll`, and `Parser.dll` is useful on its own, then create one package for each.</span></span> <span data-ttu-id="5d4a8-120">To umožňuje vývojářům použít `Parser.dll` nezávisle na `Utilities.dll`.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-120">Doing so allows developers to use `Parser.dll` independently of `Utilities.dll`.</span></span>

- <span data-ttu-id="5d4a8-121">Pokud se knihovna skládá z více sestavení, která nejsou nezávislá na sobě, je vhodné je kombinovat do jednoho balíčku.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-121">If your library is composed of multiple assemblies that aren't independently useful, then it's fine to combine them into one package.</span></span> <span data-ttu-id="5d4a8-122">V předchozím příkladu, pokud `Parser.dll` obsahuje kód, který se používá pouze `Utilities.dll`, je to v pořádku, pokud chcete ve stejném balíčku zachovat `Parser.dll`.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-122">Using the previous example, if `Parser.dll` contains code that's used only by `Utilities.dll`, then it's fine to keep `Parser.dll` in the same package.</span></span>

- <span data-ttu-id="5d4a8-123">Podobně platí, že pokud `Utilities.dll` závisí na `Utilities.resources.dll`, kde se to znovu nehodí, pak do stejného balíčku vložte obojí.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-123">Similarly, if `Utilities.dll` depends on `Utilities.resources.dll`, where again the latter is not useful on its own, then put both in the same package.</span></span>

<span data-ttu-id="5d4a8-124">Prostředky jsou ve skutečnosti zvláštním případem.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-124">Resources are, in fact, a special case.</span></span> <span data-ttu-id="5d4a8-125">Když je balíček nainstalován do projektu, NuGet automaticky přidá odkazy na sestavení do knihoven DLL balíčku, *kromě* těch, které jsou pojmenovány `.resources.dll`, protože se předpokládá, že jsou lokalizovaná satelitní sestavení (viz téma [vytváření lokalizovaných balíčků ](creating-localized-packages.md)).</span><span class="sxs-lookup"><span data-stu-id="5d4a8-125">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies (see [Creating localized packages](creating-localized-packages.md)).</span></span> <span data-ttu-id="5d4a8-126">Z tohoto důvodu Vyhněte použití `.resources.dll` u souborů, které jinak obsahují základní kód balíčku.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-126">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="5d4a8-127">Pokud vaše knihovna obsahuje sestavení zprostředkovatele komunikace s objekty COM, postupujte podle dalších pokynů v části [Vytvoření balíčků se sestaveními zprostředkovatele komunikace s objekty COM](author-packages-with-com-interop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="5d4a8-127">If your library contains COM interop assemblies, follow additional the guidelines in [Create packages with COM interop assemblies](author-packages-with-com-interop-assemblies.md).</span></span>

## <a name="the-role-and-structure-of-the-nuspec-file"></a><span data-ttu-id="5d4a8-128">Role a struktura souboru. nuspec</span><span class="sxs-lookup"><span data-stu-id="5d4a8-128">The role and structure of the .nuspec file</span></span>

<span data-ttu-id="5d4a8-129">Jakmile víte, které soubory chcete zabalit, je dalším krokem vytvoření manifestu balíčku v souboru XML `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-129">Once you know what files you want to package, the next step is creating a package manifest in a `.nuspec` XML file.</span></span>

<span data-ttu-id="5d4a8-130">Manifest:</span><span class="sxs-lookup"><span data-stu-id="5d4a8-130">The manifest:</span></span>

1. <span data-ttu-id="5d4a8-131">Popisuje obsah balíčku a je sám součástí balíčku.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-131">Describes the package's contents and is itself included in the package.</span></span>
1. <span data-ttu-id="5d4a8-132">Vydělí jak vytvoření balíčku, tak instruuje nástroj NuGet o tom, jak balíček nainstalovat do projektu.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-132">Drives both the creation of the package and instructs NuGet on how to install the package into a project.</span></span> <span data-ttu-id="5d4a8-133">Například manifest identifikuje jiné závislosti balíčků, takže může NuGet nainstalovat i tyto závislosti při instalaci hlavního balíčku.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-133">For example, the manifest identifies other package dependencies such that NuGet can also install those dependencies when the main package is installed.</span></span>
1. <span data-ttu-id="5d4a8-134">Obsahuje požadované i volitelné vlastnosti, jak je popsáno níže.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-134">Contains both required and optional properties as described below.</span></span> <span data-ttu-id="5d4a8-135">Přesné podrobnosti, včetně dalších vlastností, které zde nejsou uvedeny, naleznete v tématu [. nuspec reference](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="5d4a8-135">For exact details, including other properties not mentioned here, see  the [.nuspec reference](../reference/nuspec.md).</span></span>

<span data-ttu-id="5d4a8-136">Požadované vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="5d4a8-136">Required properties:</span></span>

- <span data-ttu-id="5d4a8-137">Identifikátor balíčku, který musí být jedinečný v rámci Galerie, která hostuje balíček.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-137">The package identifier, which must be unique across the gallery that hosts the package.</span></span>
- <span data-ttu-id="5d4a8-138">Konkrétní číslo verze ve formátu *hlavní. podverze. Oprava [-přípona]* , kde *-přípona* identifikuje [předběžné verze verzí](prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="5d4a8-138">A specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md)</span></span>
- <span data-ttu-id="5d4a8-139">Název balíčku, jak by měl být zobrazen na hostiteli (například nuget.org)</span><span class="sxs-lookup"><span data-stu-id="5d4a8-139">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="5d4a8-140">Informace o autorovi a vlastníka.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-140">Author and owner information.</span></span>
- <span data-ttu-id="5d4a8-141">Dlouhý popis balíčku.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-141">A long description of the package.</span></span>

<span data-ttu-id="5d4a8-142">Běžné volitelné vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="5d4a8-142">Common optional properties:</span></span>

- <span data-ttu-id="5d4a8-143">Zpráva k vydání verze</span><span class="sxs-lookup"><span data-stu-id="5d4a8-143">Release notes</span></span>
- <span data-ttu-id="5d4a8-144">Informace o autorských právech</span><span class="sxs-lookup"><span data-stu-id="5d4a8-144">Copyright information</span></span>
- <span data-ttu-id="5d4a8-145">Krátký popis [uživatelského rozhraní Správce balíčků v aplikaci Visual Studio](../consume-packages/install-use-packages-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="5d4a8-145">A short description for the [Package Manager UI in Visual Studio](../consume-packages/install-use-packages-visual-studio.md)</span></span>
- <span data-ttu-id="5d4a8-146">ID národního prostředí</span><span class="sxs-lookup"><span data-stu-id="5d4a8-146">A locale ID</span></span>
- <span data-ttu-id="5d4a8-147">Adresa URL projektu</span><span class="sxs-lookup"><span data-stu-id="5d4a8-147">Project URL</span></span>
- <span data-ttu-id="5d4a8-148">Licence jako výraz nebo soubor (`licenseUrl` je zastaralá, použijte [element metadat `license` nuspec](../reference/nuspec.md#license))</span><span class="sxs-lookup"><span data-stu-id="5d4a8-148">License as an expression or file (`licenseUrl` is being deprecated, use the [`license` nuspec metadata element](../reference/nuspec.md#license))</span></span>
- <span data-ttu-id="5d4a8-149">Adresa URL ikony</span><span class="sxs-lookup"><span data-stu-id="5d4a8-149">An icon URL</span></span>
- <span data-ttu-id="5d4a8-150">Seznam závislostí a odkazů</span><span class="sxs-lookup"><span data-stu-id="5d4a8-150">Lists of dependencies and references</span></span>
- <span data-ttu-id="5d4a8-151">Značky, které pomáhají při hledání v galerii</span><span class="sxs-lookup"><span data-stu-id="5d4a8-151">Tags that assist in gallery searches</span></span>

<span data-ttu-id="5d4a8-152">Následuje typický (ale fiktivní) soubor `.nuspec` s komentáři popisujícím vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="5d4a8-152">The following is a typical (but fictitious) `.nuspec` file, with comments describing the properties:</span></span>

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

<span data-ttu-id="5d4a8-153">Podrobnosti o deklarování závislostí a zadání čísel verzí najdete v tématu [Packages. config](../reference/packages-config.md) a [Správa verzí balíčků](../concepts/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="5d4a8-153">For details on declaring dependencies and specifying version numbers, see [packages.config](../reference/packages-config.md) and [Package versioning](../concepts/package-versioning.md).</span></span> <span data-ttu-id="5d4a8-154">Je také možné Surface prostředků ze závislostí přímo v balíčku pomocí atributů `include` a `exclude` na elementu `dependency`.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-154">It is also possible to surface assets from dependencies directly in the package by using the `include` and `exclude` attributes on the `dependency` element.</span></span> <span data-ttu-id="5d4a8-155">Viz [referenční závislosti. nuspec](../reference/nuspec.md#dependencies).</span><span class="sxs-lookup"><span data-stu-id="5d4a8-155">See [.nuspec Reference - Dependencies](../reference/nuspec.md#dependencies).</span></span>

<span data-ttu-id="5d4a8-156">Vzhledem k tomu, že je manifest součástí balíčku, který byl vytvořen z něj, můžete najít libovolný počet dalších příkladů zkoumáním existujících balíčků.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-156">Because the manifest is included in the package created from it, you can find any number of additional examples by examining existing packages.</span></span> <span data-ttu-id="5d4a8-157">Dobrým zdrojem je složka *globálního balíčku* v počítači, umístění, které je vráceno následujícím příkazem:</span><span class="sxs-lookup"><span data-stu-id="5d4a8-157">A good source is the *global-packages* folder on your computer, the location of which is returned by the following command:</span></span>

```cli
nuget locals -list global-packages
```

<span data-ttu-id="5d4a8-158">Do libovolné složky *package\version* zkopírujte soubor `.nupkg` do souboru `.zip`, pak otevřete tento soubor `.zip` a prověřte `.nuspec` v něm.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-158">Go into any *package\version* folder, copy the `.nupkg` file to a `.zip` file, then open that `.zip` file and examine the `.nuspec` within it.</span></span>

> [!Note]
> <span data-ttu-id="5d4a8-159">Při vytváření `.nuspec` z projektu sady Visual Studio obsahuje manifest tokeny, které jsou nahrazeny informacemi z projektu při sestavení balíčku.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-159">When creating a `.nuspec` from a Visual Studio project, the manifest contains tokens that are replaced with information from the project when the package is built.</span></span> <span data-ttu-id="5d4a8-160">Viz [vytvoření. nuspec z projektu sady Visual Studio](#from-a-visual-studio-project).</span><span class="sxs-lookup"><span data-stu-id="5d4a8-160">See [Creating the .nuspec from a Visual Studio project](#from-a-visual-studio-project).</span></span>

## <a name="create-the-nuspec-file"></a><span data-ttu-id="5d4a8-161">Vytvoření souboru. nuspec</span><span class="sxs-lookup"><span data-stu-id="5d4a8-161">Create the .nuspec file</span></span>

<span data-ttu-id="5d4a8-162">Vytvoření kompletního manifestu obvykle začíná základním souborem `.nuspec` vygenerovaným pomocí jedné z následujících metod:</span><span class="sxs-lookup"><span data-stu-id="5d4a8-162">Creating a complete manifest typically begins with a basic `.nuspec` file generated through one of the following methods:</span></span>

- [<span data-ttu-id="5d4a8-163">Pracovní adresář na základě konvence</span><span class="sxs-lookup"><span data-stu-id="5d4a8-163">A convention-based working directory</span></span>](#from-a-convention-based-working-directory)
- [<span data-ttu-id="5d4a8-164">Knihovna DLL sestavení</span><span class="sxs-lookup"><span data-stu-id="5d4a8-164">An assembly DLL</span></span>](#from-an-assembly-dll)
- [<span data-ttu-id="5d4a8-165">Projekt sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5d4a8-165">A Visual Studio project</span></span>](#from-a-visual-studio-project)    
- [<span data-ttu-id="5d4a8-166">Nový soubor s výchozími hodnotami</span><span class="sxs-lookup"><span data-stu-id="5d4a8-166">New file with default values</span></span>](#new-file-with-default-values)

<span data-ttu-id="5d4a8-167">Soubor pak upravíte ručně, aby pomohly v konečném balíčku popsaný přesný obsah.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-167">You then edit the file by hand so that it describes the exact content you want in the final package.</span></span>

> [!Important]
> <span data-ttu-id="5d4a8-168">Vygenerované soubory `.nuspec` obsahují zástupné symboly, které je třeba upravit před vytvořením balíčku pomocí příkazu `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-168">Generated `.nuspec` files contain placeholders that must be modified before creating the package with the `nuget pack` command.</span></span> <span data-ttu-id="5d4a8-169">Tento příkaz se nezdařil, pokud `.nuspec` obsahuje zástupné symboly.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-169">That command fails if the `.nuspec` contains any placeholders.</span></span>

### <a name="from-a-convention-based-working-directory"></a><span data-ttu-id="5d4a8-170">Z pracovního adresáře založeného na konvencích</span><span class="sxs-lookup"><span data-stu-id="5d4a8-170">From a convention-based working directory</span></span>

<span data-ttu-id="5d4a8-171">Vzhledem k tomu, že balíček NuGet je jenom soubor ZIP, který je přejmenovaný pomocí rozšíření `.nupkg`, často je nejjednodušší vytvořit strukturu složek, kterou chcete v místním systému souborů, a pak vytvořit soubor `.nuspec` přímo z této struktury.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-171">Because a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension, it's often easiest to create the folder structure you want on your local file system, then create the `.nuspec` file directly from that structure.</span></span> <span data-ttu-id="5d4a8-172">Příkaz `nuget pack` pak automaticky přidá všechny soubory v této struktuře složek (kromě všech složek, které začínají na `.`, což vám umožní zachovat soukromé soubory ve stejné struktuře).</span><span class="sxs-lookup"><span data-stu-id="5d4a8-172">The `nuget pack` command then automatically adds all files in that folder structure (excluding any folders that begin with `.`, allowing you to keep private files in the same structure).</span></span>

<span data-ttu-id="5d4a8-173">Výhodou tohoto přístupu je, že nemusíte určovat v manifestu, které soubory chcete zahrnout do balíčku (jak je popsáno dále v tomto tématu).</span><span class="sxs-lookup"><span data-stu-id="5d4a8-173">The advantage to this approach is that you don't need to specify in the manifest which files you want to include in the package (as explained later in this topic).</span></span> <span data-ttu-id="5d4a8-174">Proces sestavení může jednoduše vytvořit přesnou strukturu složky, která je součástí balíčku, a můžete snadno zahrnout další soubory, které nemusí být součástí projektu, jinak:</span><span class="sxs-lookup"><span data-stu-id="5d4a8-174">You can simply have your build process produce the exact folder structure that goes into the package, and you can easily include other files that might not be part of a project otherwise:</span></span>

- <span data-ttu-id="5d4a8-175">Obsah a zdrojový kód, které by měly být vloženy do cílového projektu.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-175">Content and source code that should be injected into the target project.</span></span>
- <span data-ttu-id="5d4a8-176">PowerShellové skripty</span><span class="sxs-lookup"><span data-stu-id="5d4a8-176">PowerShell scripts</span></span>
- <span data-ttu-id="5d4a8-177">Transformace na existující soubory konfigurace a zdrojového kódu v projektu.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-177">Transformations to existing configuration and source code files in a project.</span></span>

<span data-ttu-id="5d4a8-178">Konvence složek jsou následující:</span><span class="sxs-lookup"><span data-stu-id="5d4a8-178">The folder conventions are as follows:</span></span>

| <span data-ttu-id="5d4a8-179">Folder</span><span class="sxs-lookup"><span data-stu-id="5d4a8-179">Folder</span></span> | <span data-ttu-id="5d4a8-180">Popis</span><span class="sxs-lookup"><span data-stu-id="5d4a8-180">Description</span></span> | <span data-ttu-id="5d4a8-181">Akce při instalaci balíčku</span><span class="sxs-lookup"><span data-stu-id="5d4a8-181">Action upon package install</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5d4a8-182">zobrazuje</span><span class="sxs-lookup"><span data-stu-id="5d4a8-182">(root)</span></span> | <span data-ttu-id="5d4a8-183">Umístění souboru Readme. txt</span><span class="sxs-lookup"><span data-stu-id="5d4a8-183">Location for readme.txt</span></span> | <span data-ttu-id="5d4a8-184">Sada Visual Studio při instalaci balíčku zobrazí v kořenovém adresáři balíčku soubor Readme. txt.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-184">Visual Studio displays a readme.txt file in the package root when the package is installed.</span></span> |
| <span data-ttu-id="5d4a8-185">lib/{TFM}</span><span class="sxs-lookup"><span data-stu-id="5d4a8-185">lib/{tfm}</span></span> | <span data-ttu-id="5d4a8-186">Assembly (`.dll`), dokumentace (`.xml`) a soubory symbolů (`.pdb`) pro daný moniker cílového rozhraní (TFM)</span><span class="sxs-lookup"><span data-stu-id="5d4a8-186">Assembly (`.dll`), documentation (`.xml`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="5d4a8-187">Sestavení jsou přidána jako reference pro kompilaci a také za běhu; `.xml` a `.pdb` zkopírovány do složek projektu.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-187">Assemblies are added as references for compile as well as runtime; `.xml` and `.pdb` copied into project folders.</span></span> <span data-ttu-id="5d4a8-188">Viz [Podpora více cílových rozhraní](supporting-multiple-target-frameworks.md) pro vytváření podadresářů specifických pro cíl rozhraní.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-188">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md) for creating framework target-specific sub-folders.</span></span> |
| <span data-ttu-id="5d4a8-189">ref/{TFM}</span><span class="sxs-lookup"><span data-stu-id="5d4a8-189">ref/{tfm}</span></span> | <span data-ttu-id="5d4a8-190">Assembly (`.dll`) a symbol (`.pdb`) soubory pro daný moniker cílového rozhraní (TFM)</span><span class="sxs-lookup"><span data-stu-id="5d4a8-190">Assembly (`.dll`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="5d4a8-191">Sestavení jsou přidána jako odkazy pouze pro dobu kompilace; Takže se nic nezkopíruje do složky Bin projektu.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-191">Assemblies are added as references only for compile time; So nothing will be copied into project bin folder.</span></span> |
| <span data-ttu-id="5d4a8-192">moduly runtime</span><span class="sxs-lookup"><span data-stu-id="5d4a8-192">runtimes</span></span> | <span data-ttu-id="5d4a8-193">Sestavení pro konkrétní architekturu (`.dll`), symbol (`.pdb`) a soubory nativního prostředku (`.pri`)</span><span class="sxs-lookup"><span data-stu-id="5d4a8-193">Architecture-specific assembly (`.dll`), symbol (`.pdb`), and native resource (`.pri`) files</span></span> | <span data-ttu-id="5d4a8-194">Sestavení jsou přidána jako odkazy pouze pro modul runtime; jiné soubory jsou zkopírovány do složek projektu.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-194">Assemblies are added as references only for runtime; other files are copied into project folders.</span></span> <span data-ttu-id="5d4a8-195">V rámci `/ref/{tfm}` složky by mělo vždy být odpovídající (TFM) `AnyCPU` konkrétní sestavení, které poskytne odpovídající sestavení času kompilace.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-195">There should always be a corresponding (TFM) `AnyCPU` specific assembly under `/ref/{tfm}` folder to provide corresponding compile time assembly.</span></span> <span data-ttu-id="5d4a8-196">Viz [Podpora více cílových rozhraní](supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="5d4a8-196">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md).</span></span> |
| <span data-ttu-id="5d4a8-197">obsah</span><span class="sxs-lookup"><span data-stu-id="5d4a8-197">content</span></span> | <span data-ttu-id="5d4a8-198">Libovolné soubory</span><span class="sxs-lookup"><span data-stu-id="5d4a8-198">Arbitrary files</span></span> | <span data-ttu-id="5d4a8-199">Obsah je zkopírován do kořenového adresáře projektu.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-199">Contents are copied to the project root.</span></span> <span data-ttu-id="5d4a8-200">Složku **obsahu** si můžete představit jako kořen cílové aplikace, která nakonec balíček spotřebovává.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-200">Think of the **content** folder as the root of the target application that ultimately consumes the package.</span></span> <span data-ttu-id="5d4a8-201">Pokud chcete, aby balíček přidal obrázek do složky */images* aplikace, umístěte ho do složky *obsah/image* balíčku.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-201">To have the package add an image in the application's */images* folder, place it in the package's *content/images* folder.</span></span> |
| <span data-ttu-id="5d4a8-202">sestavení</span><span class="sxs-lookup"><span data-stu-id="5d4a8-202">build</span></span> | <span data-ttu-id="5d4a8-203">*(3. x +)* Soubory MSBuild `.targets` a `.props`</span><span class="sxs-lookup"><span data-stu-id="5d4a8-203">*(3.x+)* MSBuild `.targets` and `.props` files</span></span> | <span data-ttu-id="5d4a8-204">Automaticky vložen do projektu.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-204">Automatically inserted into the project.</span></span> |
| <span data-ttu-id="5d4a8-205">buildMultiTargeting</span><span class="sxs-lookup"><span data-stu-id="5d4a8-205">buildMultiTargeting</span></span> | <span data-ttu-id="5d4a8-206">*(4.0 +)* Soubory MSBuild `.targets` a `.props` pro cílení na různé architektury</span><span class="sxs-lookup"><span data-stu-id="5d4a8-206">*(4.0+)* MSBuild `.targets` and `.props` files for cross-framework targeting</span></span> | <span data-ttu-id="5d4a8-207">Automaticky vložen do projektu.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-207">Automatically inserted into the project.</span></span> |
| <span data-ttu-id="5d4a8-208">buildTransitive</span><span class="sxs-lookup"><span data-stu-id="5d4a8-208">buildTransitive</span></span> | <span data-ttu-id="5d4a8-209">*(5.0 +)* Nástroj MSBuild `.targets` a `.props` soubory, které přenášejí přenos do libovolného náročného projektu.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-209">*(5.0+)* MSBuild `.targets` and `.props` files that flow transitively to any consuming project.</span></span> <span data-ttu-id="5d4a8-210">Podívejte se na stránku [funkce](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) .</span><span class="sxs-lookup"><span data-stu-id="5d4a8-210">See the [feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) page.</span></span> | <span data-ttu-id="5d4a8-211">Automaticky vložen do projektu.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-211">Automatically inserted into the project.</span></span> |
| <span data-ttu-id="5d4a8-212">nástroje</span><span class="sxs-lookup"><span data-stu-id="5d4a8-212">tools</span></span> | <span data-ttu-id="5d4a8-213">Skripty a programy PowerShellu dostupné z konzoly Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="5d4a8-213">Powershell scripts and programs accessible from the Package Manager Console</span></span> | <span data-ttu-id="5d4a8-214">Složka `tools` se přidá do proměnné prostředí `PATH` pouze pro konzolu Správce balíčků (konkrétně *ne* do `PATH` jako nastavená pro MSBuild při sestavování projektu).</span><span class="sxs-lookup"><span data-stu-id="5d4a8-214">The `tools` folder is added to the `PATH` environment variable for the Package Manager Console only (Specifically, *not* to the `PATH` as set for MSBuild when building the project).</span></span> |

<span data-ttu-id="5d4a8-215">Vzhledem k tomu, že struktura složky může obsahovat libovolný počet sestavení pro libovolný počet cílových rozhraní, tato metoda je nezbytná při vytváření balíčků, které podporují více rozhraní.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-215">Because your folder structure can contain any number of assemblies for any number of target frameworks, this method is necessary when creating packages that support multiple frameworks.</span></span>

<span data-ttu-id="5d4a8-216">Pokud je v každém případě požadovaná struktura složky, spusťte v této složce následující příkaz pro vytvoření souboru `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="5d4a8-216">In any case, once you have the desired folder structure in place, run the following command in that folder to create the `.nuspec` file:</span></span>

```cli
nuget spec
```

<span data-ttu-id="5d4a8-217">Znovu vygenerovaná `.nuspec` neobsahuje žádné explicitní odkazy na soubory ve struktuře složek.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-217">Again, the generated `.nuspec` contains no explicit references to files in the folder structure.</span></span> <span data-ttu-id="5d4a8-218">NuGet automaticky zahrnuje všechny soubory při vytvoření balíčku.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-218">NuGet automatically includes all files when the package is created.</span></span> <span data-ttu-id="5d4a8-219">Je však stále nutné upravovat zástupné hodnoty v jiných částech manifestu.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-219">You still need to edit placeholder values in other parts of the manifest, however.</span></span>

### <a name="from-an-assembly-dll"></a><span data-ttu-id="5d4a8-220">Z knihovny DLL sestavení</span><span class="sxs-lookup"><span data-stu-id="5d4a8-220">From an assembly DLL</span></span>

<span data-ttu-id="5d4a8-221">V jednoduchém případě vytvoření balíčku ze sestavení můžete vygenerovat soubor `.nuspec` z metadat v sestavení pomocí následujícího příkazu:</span><span class="sxs-lookup"><span data-stu-id="5d4a8-221">In the simple case of creating a package from an assembly, you can generate a `.nuspec` file from the metadata in the assembly using the following command:</span></span>

```cli
nuget spec <assembly-name>.dll
```

<span data-ttu-id="5d4a8-222">Použití tohoto formuláře nahrazuje několik zástupných symbolů v manifestu s konkrétními hodnotami ze sestavení.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-222">Using this form replaces a few placeholders in the manifest with specific values from the assembly.</span></span> <span data-ttu-id="5d4a8-223">Například vlastnost `<id>` je nastavena na název sestavení a `<version>` je nastavena na verzi sestavení.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-223">For example, the `<id>` property is set to the assembly name, and `<version>` is set to the assembly version.</span></span> <span data-ttu-id="5d4a8-224">Jiné vlastnosti v manifestu však nemají v sestavení shodné hodnoty, takže stále obsahují zástupné symboly.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-224">Other properties in the manifest, however, don't have matching values in the assembly and thus still contain placeholders.</span></span>

### <a name="from-a-visual-studio-project"></a><span data-ttu-id="5d4a8-225">Z projektu sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5d4a8-225">From a Visual Studio project</span></span>

<span data-ttu-id="5d4a8-226">Vytvoření `.nuspec` ze souboru `.csproj` nebo `.vbproj` je pohodlné, protože další balíčky, které byly do těchto projektů nainstalovány, jsou automaticky odkazovány jako závislosti.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-226">Creating a `.nuspec` from a `.csproj` or `.vbproj` file is convenient because other packages that have been installed into those project are automatically referenced as dependencies.</span></span> <span data-ttu-id="5d4a8-227">Jednoduše použijte následující příkaz ve stejné složce jako soubor projektu:</span><span class="sxs-lookup"><span data-stu-id="5d4a8-227">Simply use the following command in the same folder as the project file:</span></span>

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

<span data-ttu-id="5d4a8-228">Výsledný soubor `<project-name>.nuspec` obsahuje *tokeny* , které jsou nahrazeny v době balení s hodnotami z projektu, včetně odkazů na všechny ostatní balíčky, které již byly nainstalovány.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-228">The resulting `<project-name>.nuspec` file contains *tokens* that are replaced at packaging time with values from the project, including references to any other packages that have already been installed.</span></span>

<span data-ttu-id="5d4a8-229">Pokud máte závislosti balíčků, které chcete zahrnout do souboru *. nuspec*, místo toho použijte `nuget pack` a získejte soubor *. nuspec* z generovaného souboru *. nupkg* .</span><span class="sxs-lookup"><span data-stu-id="5d4a8-229">If you have package dependencies to include in the *.nuspec*, instead use `nuget pack`, and get the *.nuspec* file from within the generated *.nupkg* file.</span></span> <span data-ttu-id="5d4a8-230">Použijte například následující příkaz.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-230">For example, use the following command.</span></span>

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget pack myproject.csproj
```

<span data-ttu-id="5d4a8-231">Token je oddělený `$` symboly na obou stranách vlastnosti projektu.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-231">A token is delimited by `$` symbols on both sides of the project property.</span></span> <span data-ttu-id="5d4a8-232">Například hodnota `<id>` v manifestu generované tímto způsobem obvykle vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="5d4a8-232">For example, the `<id>` value in a manifest generated in this way typically appears as follows:</span></span>

```xml
<id>$id$</id>
```

<span data-ttu-id="5d4a8-233">Tento token je nahrazen hodnotou `AssemblyName` ze souboru projektu v době balení.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-233">This token is replaced with the `AssemblyName` value from the project file at packing time.</span></span> <span data-ttu-id="5d4a8-234">Přesné mapování hodnot projektu na tokeny `.nuspec` naleznete v [referenčních informacích k náhradním tokenům](../reference/nuspec.md#replacement-tokens).</span><span class="sxs-lookup"><span data-stu-id="5d4a8-234">For the exact mapping of project values to `.nuspec` tokens, see the [Replacement Tokens reference](../reference/nuspec.md#replacement-tokens).</span></span>

<span data-ttu-id="5d4a8-235">Tokeny zbavují nutnost aktualizace důležitých hodnot, jako je číslo verze v `.nuspec` při aktualizaci projektu.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-235">Tokens relieve you from needing to update crucial values like the version number in the `.nuspec` as you update the project.</span></span> <span data-ttu-id="5d4a8-236">(V případě potřeby můžete tokeny vždy nahradit hodnotami literálů).</span><span class="sxs-lookup"><span data-stu-id="5d4a8-236">(You can always replace the tokens with literal values, if desired).</span></span> 

<span data-ttu-id="5d4a8-237">Všimněte si, že při práci z projektu sady Visual Studio je k dispozici několik dalších možností balení, jak je popsáno v tématu [spuštění sady NuGet Pack pro vygenerování souboru. nupkg](#run-nuget-pack-to-generate-the-nupkg-file) později.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-237">Note that there are several additional packaging options available when working from a Visual Studio project, as described in [Running nuget pack to generate the .nupkg file](#run-nuget-pack-to-generate-the-nupkg-file) later on.</span></span>

#### <a name="solution-level-packages"></a><span data-ttu-id="5d4a8-238">Balíčky na úrovni řešení</span><span class="sxs-lookup"><span data-stu-id="5d4a8-238">Solution-level packages</span></span>

<span data-ttu-id="5d4a8-239">*Pouze NuGet 2. x. Není k dispozici v NuGet 3.0 + +.*</span><span class="sxs-lookup"><span data-stu-id="5d4a8-239">*NuGet 2.x only. Not available in NuGet 3.0+.*</span></span>

<span data-ttu-id="5d4a8-240">NuGet 2. x podporuje pojem balíčku na úrovni řešení, který nainstaluje nástroje nebo další příkazy pro konzolu Správce balíčků (obsah složky `tools`), ale nepřidá odkazy, obsah ani přizpůsobení sestavení do žádného projektu v řešení.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-240">NuGet 2.x supported the notion of a solution-level package that installs tools or additional commands for the Package Manager Console (the contents of the `tools` folder), but does not add references, content, or build customizations to any projects in the solution.</span></span> <span data-ttu-id="5d4a8-241">Takové balíčky neobsahují ve svých přímých složkách `lib`, `content` nebo `build` žádné soubory a žádná z jejích závislostí nemá soubory v příslušných `lib`, `content` nebo `build` složkách.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-241">Such packages contain no files in its direct `lib`, `content`, or `build` folders, and none of its dependencies have files in their respective `lib`, `content`, or `build` folders.</span></span>

<span data-ttu-id="5d4a8-242">NuGet sleduje nainstalované balíčky na úrovni řešení v souboru `packages.config` ve složce `.nuget`, nikoli v souboru `packages.config` projektu.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-242">NuGet tracks installed solution-level packages in a `packages.config` file in the `.nuget` folder, rather than the project's `packages.config` file.</span></span>

### <a name="new-file-with-default-values"></a><span data-ttu-id="5d4a8-243">Nový soubor s výchozími hodnotami</span><span class="sxs-lookup"><span data-stu-id="5d4a8-243">New file with default values</span></span>

<span data-ttu-id="5d4a8-244">Následující příkaz vytvoří výchozí manifest se zástupnými symboly, který vám zajistí začátek správné struktury souborů:</span><span class="sxs-lookup"><span data-stu-id="5d4a8-244">The following command creates a default manifest with placeholders, which ensures you start with the proper file structure:</span></span>

```cli
nuget spec [<package-name>]
```

<span data-ttu-id="5d4a8-245">Pokud \<\>název balíčku vynecháte, je výsledný soubor `Package.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-245">If you omit \<package-name\>, the resulting file is `Package.nuspec`.</span></span> <span data-ttu-id="5d4a8-246">Pokud zadáte název, například `Contoso.Utility.UsefulStuff`, soubor je `Contoso.Utility.UsefulStuff.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-246">If you provide a name such as `Contoso.Utility.UsefulStuff`, the file is `Contoso.Utility.UsefulStuff.nuspec`.</span></span>

<span data-ttu-id="5d4a8-247">Výsledný `.nuspec` obsahuje zástupné symboly pro hodnoty, jako je `projectUrl`.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-247">The resulting `.nuspec` contains placeholders for values like the `projectUrl`.</span></span> <span data-ttu-id="5d4a8-248">Nezapomeňte soubor před použitím upravit, aby se vytvořil finální soubor `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-248">Be sure to edit the file before using it to create the final `.nupkg` file.</span></span>

## <a name="choose-a-unique-package-identifier-and-setting-the-version-number"></a><span data-ttu-id="5d4a8-249">Vyberte jedinečný identifikátor balíčku a nastavte číslo verze.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-249">Choose a unique package identifier and setting the version number</span></span>

<span data-ttu-id="5d4a8-250">Identifikátor balíčku (`<id>` element) a číslo verze (element `<version>`) jsou dvě nejdůležitější hodnoty v manifestu, protože jednoznačně identifikují přesný kód, který je obsažen v balíčku.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-250">The package identifier (`<id>` element) and the version number (`<version>` element) are the two most important values in the manifest because they uniquely identify the exact code that's contained in the package.</span></span>

<span data-ttu-id="5d4a8-251">**Osvědčené postupy pro identifikátor balíčku:**</span><span class="sxs-lookup"><span data-stu-id="5d4a8-251">**Best practices for the package identifier:**</span></span>

- <span data-ttu-id="5d4a8-252">**Jedinečnost**: identifikátor musí být jedinečný v rámci NuGet.org nebo bez ohledu na to, jakou galerii hostují balíček.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-252">**Uniqueness**: The identifier must be unique across nuget.org or whatever gallery hosts the package.</span></span> <span data-ttu-id="5d4a8-253">Než se rozhodnete pro identifikátor, vyhledejte příslušnou galerii a ověřte, jestli se tento název už používá.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-253">Before deciding on an identifier, search the applicable gallery to check if the name is already in use.</span></span> <span data-ttu-id="5d4a8-254">Aby nedocházelo ke konfliktům, dobrým vzorem je použít název vaší společnosti jako první část identifikátoru, například `Contoso.`.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-254">To avoid conflicts, a good pattern is to use your company name as the first part of the identifier, such as `Contoso.`.</span></span>
- <span data-ttu-id="5d4a8-255">**Obor názvů jako názvy**: Sledujte vzor podobný oborům názvů v rozhraní .NET pomocí notace tečky namísto spojovníků.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-255">**Namespace-like names**: Follow a pattern similar to namespaces in .NET, using dot notation instead of hyphens.</span></span> <span data-ttu-id="5d4a8-256">Použijte například `Contoso.Utility.UsefulStuff` místo `Contoso-Utility-UsefulStuff` nebo `Contoso_Utility_UsefulStuff`.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-256">For example, use `Contoso.Utility.UsefulStuff` rather than `Contoso-Utility-UsefulStuff` or `Contoso_Utility_UsefulStuff`.</span></span> <span data-ttu-id="5d4a8-257">Příjemci také naleznou užitečné, pokud se identifikátor balíčku shoduje s obory názvů použitými v kódu.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-257">Consumers also find it helpful when the package identifier matches the namespaces used in the code.</span></span>
- <span data-ttu-id="5d4a8-258">**Ukázkové balíčky**: Pokud vytváříte balíček ukázkového kódu, který ukazuje, jak použít jiný balíček, připojte `.Sample` jako příponu k identifikátoru, jako v `Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-258">**Sample Packages**: If you produce a package of sample code that demonstrates how to use another package, attach `.Sample` as a suffix to the identifier, as in `Contoso.Utility.UsefulStuff.Sample`.</span></span> <span data-ttu-id="5d4a8-259">(Vzorový balíček samozřejmě má závislost na druhém balíčku.) Při vytváření ukázkového balíčku použijte metodu pracovní adresáře založenou na konvenci, která je popsaná výše.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-259">(The sample package would of course have a dependency on the other package.) When creating a sample package, use the convention-based working directory method described earlier.</span></span> <span data-ttu-id="5d4a8-260">Ve složce `content` uspořádejte vzorový kód do složky s názvem `\Samples\<identifier>` jako v `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-260">In the `content` folder, arrange the sample code in a folder called `\Samples\<identifier>` as in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span></span>

<span data-ttu-id="5d4a8-261">**Osvědčené postupy pro verzi balíčku:**</span><span class="sxs-lookup"><span data-stu-id="5d4a8-261">**Best practices for the package version:**</span></span>

- <span data-ttu-id="5d4a8-262">Obecně platí, že nastavte verzi balíčku tak, aby odpovídala knihovně, i když to není nezbytně nutné.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-262">In general, set the version of the package to match the library, though this is not strictly required.</span></span> <span data-ttu-id="5d4a8-263">Toto je jednoduchá skutečnost při omezení balíčku na jedno sestavení, jak je popsáno výše v tématu [určení sestavení, která chcete zabalit](#decide-which-assemblies-to-package).</span><span class="sxs-lookup"><span data-stu-id="5d4a8-263">This is a simple matter when you limit a package to a single assembly, as described earlier in [Deciding which assemblies to package](#decide-which-assemblies-to-package).</span></span> <span data-ttu-id="5d4a8-264">Celkově mějte na paměti, že aplikace NuGet pracuje s verzemi balíčku při řešení závislostí, nikoli ve verzích sestavení.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-264">Overall, remember that NuGet itself deals with package versions when resolving dependencies, not assembly versions.</span></span>
- <span data-ttu-id="5d4a8-265">Při použití nestandardního schématu verzí nezapomeňte zvážit pravidla správy verzí NuGet, jak je vysvětleno v tématu [Správa verzí balíčků](../concepts/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="5d4a8-265">When using a non-standard version scheme, be sure to consider the NuGet versioning rules as explained in [Package versioning](../concepts/package-versioning.md).</span></span>

> <span data-ttu-id="5d4a8-266">Následující řada stručných příspěvků na blogu je také užitečná pro pochopení správy verzí:</span><span class="sxs-lookup"><span data-stu-id="5d4a8-266">The following series of brief blog posts are also helpful to understand versioning:</span></span>
>
> - [<span data-ttu-id="5d4a8-267">Část 1: pořízení Hell knihovny DLL</span><span class="sxs-lookup"><span data-stu-id="5d4a8-267">Part 1: Taking on DLL Hell</span></span>](https://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [<span data-ttu-id="5d4a8-268">Část 2: základní algoritmus</span><span class="sxs-lookup"><span data-stu-id="5d4a8-268">Part 2: The core algorithm</span></span>](https://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [<span data-ttu-id="5d4a8-269">Část 3: sjednocení pomocí přesměrování vazeb</span><span class="sxs-lookup"><span data-stu-id="5d4a8-269">Part 3: Unification via Binding Redirects</span></span>](https://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="add-a-readme-and-other-files"></a><span data-ttu-id="5d4a8-270">Přidání souboru Readme a dalších souborů</span><span class="sxs-lookup"><span data-stu-id="5d4a8-270">Add a readme and other files</span></span>

<span data-ttu-id="5d4a8-271">Pokud chcete přímo určit soubory, které se mají zahrnout do balíčku, použijte v souboru `.nuspec` uzel `<files>`, který *následuje* označení `<metadata>`:</span><span class="sxs-lookup"><span data-stu-id="5d4a8-271">To directly specify files to include in the package, use the `<files>` node in the `.nuspec` file, which *follows* the `<metadata>` tag:</span></span>

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
> <span data-ttu-id="5d4a8-272">Pokud používáte přístup k pracovnímu adresáři založenému na konvencích, můžete soubor Readme. txt umístit do kořenového adresáře balíčku a dalšího obsahu ve složce `content`.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-272">When using the convention-based working directory approach, you can place the readme.txt in the package root and other content in the `content` folder.</span></span> <span data-ttu-id="5d4a8-273">V manifestu nejsou potřebné žádné prvky `<file>`.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-273">No `<file>` elements are necessary in the manifest.</span></span>

<span data-ttu-id="5d4a8-274">Pokud zahrnete soubor s názvem `readme.txt` do kořenového adresáře balíčku, sada Visual Studio zobrazí obsah tohoto souboru jako prostý text ihned po instalaci balíčku přímo.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-274">When you include a file named `readme.txt` in the package root, Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="5d4a8-275">(Soubory Readme se nezobrazí pro balíčky nainstalované jako závislosti).</span><span class="sxs-lookup"><span data-stu-id="5d4a8-275">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="5d4a8-276">Tady je příklad, jak se zobrazí soubor Readme pro balíček HtmlAgilityPack:</span><span class="sxs-lookup"><span data-stu-id="5d4a8-276">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Zobrazení souboru Readme pro balíček NuGet při instalaci](media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="5d4a8-278">Pokud do souboru `.nuspec` zahrnete prázdný uzel `<files>`, NuGet v balíčku neobsahuje žádný jiný obsah, než kolik je ve složce `lib`.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-278">If you include an empty `<files>` node in the `.nuspec` file, NuGet doesn't include any other content in the package other than what's in the `lib` folder.</span></span>

## <a name="include-msbuild-props-and-targets-in-a-package"></a><span data-ttu-id="5d4a8-279">Zahrnutí vlastností MSBuild a cílů do balíčku</span><span class="sxs-lookup"><span data-stu-id="5d4a8-279">Include MSBuild props and targets in a package</span></span>

<span data-ttu-id="5d4a8-280">V některých případech můžete chtít přidat vlastní cíle sestavení nebo vlastnosti v projektech, které používají váš balíček, jako je například spuštění vlastního nástroje nebo procesu během sestavování.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-280">In some cases, you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="5d4a8-281">To provedete tak, že umístíte soubory do formuláře `<package_id>.targets` nebo `<package_id>.props` (například `Contoso.Utility.UsefulStuff.targets`) do složky `\build` projektu.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-281">You do this by placing files in the form `<package_id>.targets` or `<package_id>.props` (such as `Contoso.Utility.UsefulStuff.targets`) within the `\build` folder of the project.</span></span>

<span data-ttu-id="5d4a8-282">Soubory v kořenové složce `\build` jsou považovány za vhodné pro všechny cílové platformy.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-282">Files in the root `\build` folder are considered suitable for all target frameworks.</span></span> <span data-ttu-id="5d4a8-283">Chcete-li poskytnout soubory specifické pro rozhraní, umístěte je nejprve do příslušných podsložek, například následující:</span><span class="sxs-lookup"><span data-stu-id="5d4a8-283">To provide framework-specific files, first place them within appropriate subfolders, such as the following:</span></span>

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

<span data-ttu-id="5d4a8-284">Pak v souboru `.nuspec` nezapomeňte na tyto soubory odkazovat v uzlu `<files>`:</span><span class="sxs-lookup"><span data-stu-id="5d4a8-284">Then in the `.nuspec` file, be sure to refer to these files in the `<files>` node:</span></span>

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

<span data-ttu-id="5d4a8-285">Zahrnutí a cíle nástroje MSBuild do balíčku bylo [zavedeno s NuGet 2,5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), proto je vhodné přidat atribut `minClientVersion="2.5"` do prvku `metadata`, aby označovala minimální verzi klienta NuGet nutnou ke spotřebování balíčku.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-285">Including MSBuild props and targets in a package was [introduced with NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), therefore it is recommended to add the `minClientVersion="2.5"` attribute to the `metadata` element, to indicate the minimum NuGet client version required to consume the package.</span></span>

<span data-ttu-id="5d4a8-286">Když nástroj NuGet nainstaluje balíček se soubory `\build`, přidá prvky MSBuild `<Import>` v souboru projektu, které odkazují na soubory `.targets` a `.props`.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-286">When NuGet installs a package with `\build` files, it adds MSBuild `<Import>` elements in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="5d4a8-287">(`.props` se přidá v horní části souboru projektu; v dolní části se přidá `.targets`.) Pro každé cílové rozhraní se přidá samostatný podmíněný prvek `<Import>` nástroje MSBuild.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-287">(`.props` is added at the top of the project file; `.targets` is added at the bottom.) A separate conditional MSBuild `<Import>` element is added for each target framework.</span></span>

<span data-ttu-id="5d4a8-288">Soubory MSBuild `.props` a `.targets` pro cílení na více architektur lze umístit do složky `\buildMultiTargeting`.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-288">MSBuild `.props` and `.targets` files for cross-framework targeting can be placed in the `\buildMultiTargeting` folder.</span></span> <span data-ttu-id="5d4a8-289">V průběhu instalace balíčku NuGet přidá odpovídající prvky `<Import>` do souboru projektu s podmínkou, že cílové rozhraní není nastavené (vlastnost MSBuild `$(TargetFramework)` musí být prázdná).</span><span class="sxs-lookup"><span data-stu-id="5d4a8-289">During package installation, NuGet adds the corresponding `<Import>` elements to the project file with the condition, that the target framework is not set (the MSBuild property `$(TargetFramework)` must be empty).</span></span>

<span data-ttu-id="5d4a8-290">S NuGet 3. x se cíle do projektu nepřidaly, ale místo toho jsou k dispozici prostřednictvím `{projectName}.nuget.g.targets` a `{projectName}.nuget.g.props`.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-290">With NuGet 3.x, targets are not added to the project but are instead made available through `{projectName}.nuget.g.targets` and `{projectName}.nuget.g.props`.</span></span>

## <a name="run-nuget-pack-to-generate-the-nupkg-file"></a><span data-ttu-id="5d4a8-291">Spustit balíček NuGet pro vygenerování souboru. nupkg</span><span class="sxs-lookup"><span data-stu-id="5d4a8-291">Run nuget pack to generate the .nupkg file</span></span>

<span data-ttu-id="5d4a8-292">Při použití sestavení nebo pracovního adresáře založeného na konvenci vytvořte balíček spuštěním `nuget pack` se souborem `.nuspec` a nahrazením `<project-name>` konkrétním názvem souboru:</span><span class="sxs-lookup"><span data-stu-id="5d4a8-292">When using an assembly or the convention-based working directory, create a package by running `nuget pack` with your `.nuspec` file, replacing `<project-name>` with your specific filename:</span></span>

```cli
nuget pack <project-name>.nuspec
```

<span data-ttu-id="5d4a8-293">Při použití projektu sady Visual Studio spusťte `nuget pack` se souborem projektu, který automaticky načte soubor `.nuspec` projektu a nahradí všechny tokeny v rámci něj pomocí hodnot v souboru projektu:</span><span class="sxs-lookup"><span data-stu-id="5d4a8-293">When using a Visual Studio project, run `nuget pack` with your project file, which automatically loads the project's `.nuspec` file and replaces any tokens within it using values in the project file:</span></span>

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> <span data-ttu-id="5d4a8-294">Použití souboru projektu přímo je nezbytné pro nahrazení tokenu, protože projekt je zdrojem hodnot tokenu.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-294">Using the project file directly is necessary for token replacement because the project is the source of the token values.</span></span> <span data-ttu-id="5d4a8-295">Nahrazení tokenu se nestane, pokud použijete `nuget pack` se souborem `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-295">Token replacement does not happen if you use `nuget pack` with a `.nuspec` file.</span></span>

<span data-ttu-id="5d4a8-296">Ve všech případech `nuget pack` vylučuje složky, které začínají tečkou, například `.git` nebo `.hg`.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-296">In all cases, `nuget pack` excludes folders that start with a period, such as `.git` or `.hg`.</span></span>

<span data-ttu-id="5d4a8-297">NuGet označuje, zda se v souboru `.nuspec` vyskytnou nějaké chyby, které vyžadují opravu, jako je například forgetting ke změně zástupných hodnot v manifestu.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-297">NuGet indicates if there are any errors in the `.nuspec` file that need correcting, such as forgetting to change placeholder values in the manifest.</span></span>

<span data-ttu-id="5d4a8-298">Po úspěšném `nuget pack` máte soubor `.nupkg`, který můžete publikovat do vhodné galerie, jak je popsáno v tématu [publikování balíčku](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="5d4a8-298">Once `nuget pack` succeeds, you have a `.nupkg` file that you can publish to a suitable gallery as described in [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

> [!Tip]
> <span data-ttu-id="5d4a8-299">Užitečný způsob, jak prostudovat balíček po jeho vytvoření, je otevřít v nástroji [Průzkumník balíčků](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) .</span><span class="sxs-lookup"><span data-stu-id="5d4a8-299">A helpful way to examine a package after creating it is to open it in the [Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) tool.</span></span> <span data-ttu-id="5d4a8-300">Získáte tak grafické zobrazení obsahu balíčku a jeho manifestu.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-300">This gives you a graphical view of the package contents and its manifest.</span></span> <span data-ttu-id="5d4a8-301">Výsledný soubor `.nupkg` můžete také přejmenovat na soubor `.zip` a prozkoumat jeho obsah přímo.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-301">You can also rename the resulting `.nupkg` file to a `.zip` file and explore its contents directly.</span></span>

### <a name="additional-options"></a><span data-ttu-id="5d4a8-302">Další možnosti</span><span class="sxs-lookup"><span data-stu-id="5d4a8-302">Additional options</span></span>

<span data-ttu-id="5d4a8-303">K vyloučení souborů můžete použít různé přepínače příkazového řádku s `nuget pack`, přepsat číslo verze v manifestu a změnit výstupní složku mezi další funkce.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-303">You can use various command-line switches with `nuget pack` to exclude files, override the version number in the manifest, and change the output folder, among other features.</span></span> <span data-ttu-id="5d4a8-304">Úplný seznam najdete v [referenčních informacích k příkazu Pack](../reference/cli-reference/cli-ref-pack.md).</span><span class="sxs-lookup"><span data-stu-id="5d4a8-304">For a complete list, refer to the [pack command reference](../reference/cli-reference/cli-ref-pack.md).</span></span>

<span data-ttu-id="5d4a8-305">Následující možnosti jsou běžné v projektech sady Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="5d4a8-305">The following options are a few that are common with Visual Studio projects:</span></span>

- <span data-ttu-id="5d4a8-306">**Odkazované projekty**: Pokud projekt odkazuje na jiné projekty, můžete přidat odkazované projekty jako součást balíčku nebo jako závislosti pomocí možnosti `-IncludeReferencedProjects`:</span><span class="sxs-lookup"><span data-stu-id="5d4a8-306">**Referenced projects**: If the project references other projects, you can add the referenced projects as part of the package, or as dependencies, by using the `-IncludeReferencedProjects` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    <span data-ttu-id="5d4a8-307">Tento proces zahrnutí je rekurzivní, takže pokud `MyProject.csproj` odkazuje na projekty B a C a tyto projekty odkazují D, E a F, jsou do balíčku zahrnuty soubory z B, C, D, E a F.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-307">This inclusion process is recursive, so if `MyProject.csproj` references projects B and C, and those projects reference D, E, and F, then files from B, C, D, E, and F are included in the package.</span></span>

    <span data-ttu-id="5d4a8-308">Pokud odkazovaný projekt obsahuje vlastní soubor `.nuspec`, pak NuGet místo toho přidá tento odkazovaný projekt jako závislost.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-308">If a referenced project includes a `.nuspec` file of its own, then NuGet adds that referenced project as a dependency instead.</span></span>  <span data-ttu-id="5d4a8-309">Tento projekt je nutné zabalit a publikovat samostatně.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-309">You need to package and publish that project separately.</span></span>

- <span data-ttu-id="5d4a8-310">**Konfigurace sestavení**: ve výchozím nastavení NuGet používá výchozí konfigurační sadu sestavení v souboru projektu, obvykle *ladění*.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-310">**Build configuration**: By default, NuGet uses the default build configuration set in the project file, typically *Debug*.</span></span> <span data-ttu-id="5d4a8-311">Chcete-li zabalit soubory z jiné konfigurace sestavení, jako je *verze*, použijte možnost `-properties` s konfigurací:</span><span class="sxs-lookup"><span data-stu-id="5d4a8-311">To pack files from a different build configuration, such as *Release*, use the `-properties` option with the configuration:</span></span>

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- <span data-ttu-id="5d4a8-312">**Symboly**: Pokud chcete zahrnout symboly, které uživatelům umožňují procházet kód balíčku v ladicím programu, použijte možnost `-Symbols`:</span><span class="sxs-lookup"><span data-stu-id="5d4a8-312">**Symbols**: to include symbols that allow consumers to step through your package code in the debugger, use the `-Symbols` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="test-package-installation"></a><span data-ttu-id="5d4a8-313">Instalace testovacího balíčku</span><span class="sxs-lookup"><span data-stu-id="5d4a8-313">Test package installation</span></span>

<span data-ttu-id="5d4a8-314">Před publikováním balíčku obvykle budete chtít otestovat proces instalace balíčku do projektu.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-314">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="5d4a8-315">Testy zajistí, že všechny soubory v projektu budou mít všechny na správném místě.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-315">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="5d4a8-316">Instalaci můžete v aplikaci Visual Studio nebo na příkazovém řádku otestovat ručně pomocí [kroků normální instalace balíčku](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span><span class="sxs-lookup"><span data-stu-id="5d4a8-316">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

<span data-ttu-id="5d4a8-317">Pro automatizované testování je základní proces následující:</span><span class="sxs-lookup"><span data-stu-id="5d4a8-317">For automated testing, the basic process is as follows:</span></span>

1. <span data-ttu-id="5d4a8-318">Zkopírujte soubor `.nupkg` do místní složky.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-318">Copy the `.nupkg` file to a local folder.</span></span>
1. <span data-ttu-id="5d4a8-319">Přidejte složku do zdrojů balíčku pomocí příkazu `nuget sources add -name <name> -source <path>` (viz [zdroje NuGet](../reference/cli-reference/cli-ref-sources.md)).</span><span class="sxs-lookup"><span data-stu-id="5d4a8-319">Add the folder to your package sources using the `nuget sources add -name <name> -source <path>` command (see [nuget sources](../reference/cli-reference/cli-ref-sources.md)).</span></span> <span data-ttu-id="5d4a8-320">Všimněte si, že tento místní zdroj je potřeba nastavit jenom jednou na daném počítači.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-320">Note that you need only set this local source once on any given computer.</span></span>
1. <span data-ttu-id="5d4a8-321">Nainstalujte balíček z tohoto zdroje pomocí `nuget install <packageID> -source <name>`, kde `<name>` odpovídá názvu vašeho zdroje, jak je uvedeno `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-321">Install the package from that source using `nuget install <packageID> -source <name>` where `<name>` matches the name of your source as given to `nuget sources`.</span></span> <span data-ttu-id="5d4a8-322">Zadání zdroje zajistí, že se balíček nainstaluje jenom z tohoto zdroje.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-322">Specifying the source ensures that the package is installed from that source alone.</span></span>
1. <span data-ttu-id="5d4a8-323">Kontrolou systému souborů ověřte, zda jsou soubory správně nainstalovány.</span><span class="sxs-lookup"><span data-stu-id="5d4a8-323">Examine your file system to check that files are installed correctly.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5d4a8-324">Další kroky</span><span class="sxs-lookup"><span data-stu-id="5d4a8-324">Next Steps</span></span>

<span data-ttu-id="5d4a8-325">Po vytvoření balíčku, který je soubor `.nupkg`, ho můžete publikovat do Galerie podle svého výběru, jak je popsáno v tématu [publikování balíčku](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="5d4a8-325">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="5d4a8-326">Můžete také chtít zvětšit možnosti vašeho balíčku nebo jinak podporovat jiné scénáře, jak je popsáno v následujících tématech:</span><span class="sxs-lookup"><span data-stu-id="5d4a8-326">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="5d4a8-327">Správa verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="5d4a8-327">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="5d4a8-328">Podpora více cílových architektur</span><span class="sxs-lookup"><span data-stu-id="5d4a8-328">Supporting multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="5d4a8-329">Transformace zdrojových a konfiguračních souborů</span><span class="sxs-lookup"><span data-stu-id="5d4a8-329">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="5d4a8-330">Lokalizace</span><span class="sxs-lookup"><span data-stu-id="5d4a8-330">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="5d4a8-331">Předběžné verze verzí</span><span class="sxs-lookup"><span data-stu-id="5d4a8-331">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="5d4a8-332">Nastavení typu balíčku</span><span class="sxs-lookup"><span data-stu-id="5d4a8-332">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="5d4a8-333">Vytváření balíčků pomocí sestavení zprostředkovatele komunikace s objekty COM</span><span class="sxs-lookup"><span data-stu-id="5d4a8-333">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="5d4a8-334">Nakonec existují další typy balíčků, o kterých byste měli vědět:</span><span class="sxs-lookup"><span data-stu-id="5d4a8-334">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="5d4a8-335">Nativní balíčky</span><span class="sxs-lookup"><span data-stu-id="5d4a8-335">Native Packages</span></span>](../guides/native-packages.md)
- [<span data-ttu-id="5d4a8-336">Balíčky symbolů</span><span class="sxs-lookup"><span data-stu-id="5d4a8-336">Symbol Packages</span></span>](../create-packages/symbol-packages-snupkg.md)
