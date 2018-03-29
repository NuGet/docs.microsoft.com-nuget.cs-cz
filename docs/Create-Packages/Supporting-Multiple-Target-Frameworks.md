---
title: Cílení na více verzí pro balíčky NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 09/27/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Popis různých metod k cílení na více verzí rozhraní .NET Framework z v rámci jednoho balíčku NuGet.
keywords: Balíček NuGet cílení na rozhraní .NET Framework verze, NuGet a rozhraní .NET, cílení na více rozhraní, vytvoření balíčku NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 4349fed276b1a1f46845c990718f9202b356072c
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="supporting-multiple-net-framework-versions"></a><span data-ttu-id="a9220-104">Podpora více verzí rozhraní .NET framework</span><span class="sxs-lookup"><span data-stu-id="a9220-104">Supporting multiple .NET framework versions</span></span>

<span data-ttu-id="a9220-105">*Projekty .NET Core pomocí nástroje NuGet 4.0 +, najdete v části [NuGet pack a obnovit jako cíle MSBuild](../reference/msbuild-targets.md) podrobnosti o cílení na více verzí.*</span><span class="sxs-lookup"><span data-stu-id="a9220-105">*For .NET Core projects using NuGet 4.0+, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md) for details on cross-targeting.*</span></span>

<span data-ttu-id="a9220-106">Mnoho knihovny cílení na konkrétní verzi rozhraní .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="a9220-106">Many libraries target a specific version of the .NET Framework.</span></span> <span data-ttu-id="a9220-107">Například můžete mít jednu verzi knihovnu, která je specifická pro UPW a jinou verzi, která využívá funkce v rozhraní .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="a9220-107">For example, you might have one version of your library that's specific to UWP, and another version that takes advantage of features in .NET Framework 4.6.</span></span>

<span data-ttu-id="a9220-108">Pro přizpůsobení, podporuje NuGet uvedení více verzí stejnou knihovnu v jeden balíček, při použití založené na konvenci pracovní adresář metoda popsaná v [vytváření balíčku](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="a9220-108">To accommodate this, NuGet supports putting multiple versions of the same library in a single package when using the convention-based working directory method described in [Creating a package](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span>

## <a name="framework-version-folder-structure"></a><span data-ttu-id="a9220-109">Struktura složek Framework verze</span><span class="sxs-lookup"><span data-stu-id="a9220-109">Framework version folder structure</span></span>

<span data-ttu-id="a9220-110">Při vytváření balíčku, který obsahuje pouze jednu verzi knihovny nebo cílové více rozhraní, je vytvořit podsložky `lib` pomocí různých malá a velká písmena framework názvy následující konvence:</span><span class="sxs-lookup"><span data-stu-id="a9220-110">When building a package that contains only one version of a library or target multiple frameworks, you always make subfolders under `lib` using different case-sensitive framework names with the following convention:</span></span>

    lib\{framework name}[{version}]

<span data-ttu-id="a9220-111">Úplný seznam podporovaných názvy, najdete v článku [odkazovat na cílové rozhraní](../reference/target-frameworks.md#supported-frameworks).</span><span class="sxs-lookup"><span data-stu-id="a9220-111">For a complete list of supported names, see the [Target Frameworks reference](../reference/target-frameworks.md#supported-frameworks).</span></span>

<span data-ttu-id="a9220-112">Nikdy byste měli mít verzi knihovny, které nejsou specifické pro rozhraní a umístěný přímo v kořenu `lib` složky.</span><span class="sxs-lookup"><span data-stu-id="a9220-112">You should never have a version of the library that is not specific to a framework and placed directly in the root `lib` folder.</span></span> <span data-ttu-id="a9220-113">(Tato možnost se podporuje jenom s `packages.config`).</span><span class="sxs-lookup"><span data-stu-id="a9220-113">(This capability was supported only with `packages.config`).</span></span> <span data-ttu-id="a9220-114">To tak, aby se ujistěte se, kompatibilní s žádné cílové rozhraní a aby ji bylo možné nainstalovat odkudkoli pravděpodobně výsledkem runtime neočekávané chyby.</span><span class="sxs-lookup"><span data-stu-id="a9220-114">Doing so would make the compatible with any target framework and allow it to be installed anywhere, likely resulting in unexpected runtime errors.</span></span> <span data-ttu-id="a9220-115">Přidání sestavení v kořenové složce (například `lib\abc.dll`) nebo v jejich podsložkách (například `lib\abc\abc.dll`) se už nepoužívá a je ignorována, pokud v PackagesReference formátu.</span><span class="sxs-lookup"><span data-stu-id="a9220-115">Adding assemblies in the root folder (such as `lib\abc.dll`) or subfolders (such as `lib\abc\abc.dll`) has been deprecated and is ignored when using the PackagesReference format.</span></span>

<span data-ttu-id="a9220-116">Například následující strukturu složek podporuje čtyři verze sestavení, které jsou specifické pro framework:</span><span class="sxs-lookup"><span data-stu-id="a9220-116">For example, the following folder structure supports four versions of an assembly that are framework-specific:</span></span>

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

<span data-ttu-id="a9220-117">Při vytváření balíčku snadno zahrnout všechny tyto soubory, použijte rekurzivního `**` zástupný znak v `<files>` část vaší `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="a9220-117">To easily include all these files when building the package, use a recursive `**` wildcard in the `<files>` section of your `.nuspec`:</span></span>

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a><span data-ttu-id="a9220-118">Architektura konkrétní složky</span><span class="sxs-lookup"><span data-stu-id="a9220-118">Architecture-specific folders</span></span>

<span data-ttu-id="a9220-119">Pokud máte specifické pro architekturu sestavení, to znamená, samostatné sestavení, které cílí ARM, x 86 a x64, můžete je nutné umístit do složky s názvem `runtimes` v rámci dílčí složky s názvem `{platform}-{architecture}\lib\{framework}` nebo `{platform}-{architecture}\native`.</span><span class="sxs-lookup"><span data-stu-id="a9220-119">If you have architecture-specific assemblies, that is, separate assemblies that target ARM, x86, and x64, you must place them in a folder named `runtimes` within sub-folders named `{platform}-{architecture}\lib\{framework}` or `{platform}-{architecture}\native`.</span></span> <span data-ttu-id="a9220-120">Například následující strukturu složek by zohlednit nativní a spravovaná knihovny DLL cílení na Windows 10 a `uap10.0` framework:</span><span class="sxs-lookup"><span data-stu-id="a9220-120">For example, the following folder structure would accommodate both native and managed DLLs targeting Windows 10 and the `uap10.0` framework:</span></span>

    \runtimes
        \win10-arm
            \native
            \lib\uap10.0
        \win10-x86
            \native
            \lib\uap10.0
        \win10-x64
            \native
            \lib\uap10.0

<span data-ttu-id="a9220-121">V tématu [vytvořit balíčky UWP](../guides/create-uwp-packages.md) příklad odkazující na tyto soubory v `.nuspec` manifest.</span><span class="sxs-lookup"><span data-stu-id="a9220-121">See [Create UWP Packages](../guides/create-uwp-packages.md) for an example of referencing these files in the `.nuspec` manifest.</span></span>

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a><span data-ttu-id="a9220-122">Odpovídající verze sestavení a cílové rozhraní v projektu</span><span class="sxs-lookup"><span data-stu-id="a9220-122">Matching assembly versions and the target framework in a project</span></span>

<span data-ttu-id="a9220-123">Když NuGet nainstaluje balíček, který má více verzí sestavení, pokusí se shodovat s názvem framework sestavení s cílový framework projektu.</span><span class="sxs-lookup"><span data-stu-id="a9220-123">When NuGet installs a package that has multiple assembly versions, it tries to match the framework name of the assembly with the target framework of the project.</span></span>

<span data-ttu-id="a9220-124">Pokud není nalezena shoda, zkopíruje NuGet sestavení pro nejvyšší verzi, která je menší než nebo rovno cílový framework projektu na, pokud je k dispozici.</span><span class="sxs-lookup"><span data-stu-id="a9220-124">If a match is not found, NuGet copies the assembly for the highest version that is less than or equal to the project's target framework, if available.</span></span> <span data-ttu-id="a9220-125">Pokud se nenajde žádné kompatibilní sestavení, vrátí NuGet příslušná chybová zpráva.</span><span class="sxs-lookup"><span data-stu-id="a9220-125">If no compatible assembly is found, NuGet returns an appropriate error message.</span></span>

<span data-ttu-id="a9220-126">Zvažte například následující strukturu složek v balíčku:</span><span class="sxs-lookup"><span data-stu-id="a9220-126">For example, consider the following folder structure in a package:</span></span>

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

<span data-ttu-id="a9220-127">Pokud při instalaci tohoto balíčku do projektu, jehož cílem rozhraní .NET Framework 4.6, NuGet nainstaluje sestavení v `net45` složky, protože se jedná o nejvyšší verzi k dispozici, která je menší než nebo rovna 4.6.</span><span class="sxs-lookup"><span data-stu-id="a9220-127">When installing this package in a project that targets .NET Framework 4.6, NuGet installs the assembly in the `net45` folder, because that's the highest available version that's less than or equal to 4.6.</span></span>

<span data-ttu-id="a9220-128">Pokud projekt cílem rozhraní .NET Framework 4.6.1, na druhé straně NuGet nainstaluje sestavení v `net461` složky.</span><span class="sxs-lookup"><span data-stu-id="a9220-128">If the project targets .NET Framework 4.6.1, on the other hand, NuGet installs the assembly in the `net461` folder.</span></span>

<span data-ttu-id="a9220-129">Pokud projekt cílem rozhraní .NET framework 4.0 a starší, vyvolá NuGet příslušná chybová zpráva pro nemůžete najít kompatibilní sestavení.</span><span class="sxs-lookup"><span data-stu-id="a9220-129">If the project targets .NET framework 4.0 and earlier, NuGet throws an appropriate error message for not finding the compatible assembly.</span></span>

## <a name="grouping-assemblies-by-framework-version"></a><span data-ttu-id="a9220-130">Seskupování podle framework, verze sestavení</span><span class="sxs-lookup"><span data-stu-id="a9220-130">Grouping assemblies by framework version</span></span>

<span data-ttu-id="a9220-131">NuGet zkopíruje sestavení ze pouze jediná knihovna složky v balíčku.</span><span class="sxs-lookup"><span data-stu-id="a9220-131">NuGet copies assemblies from only a single library folder in the package.</span></span> <span data-ttu-id="a9220-132">Předpokládejme například, že balíček má následující strukturu složek:</span><span class="sxs-lookup"><span data-stu-id="a9220-132">For example, suppose a package has the following folder structure:</span></span>

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

<span data-ttu-id="a9220-133">Při instalaci balíčku v projektu, jehož cílem rozhraní .NET Framework 4.5, `MyAssembly.dll` (v2.0) je nainstalována pouze sestavení.</span><span class="sxs-lookup"><span data-stu-id="a9220-133">When the package is installed in a project that targets .NET Framework 4.5, `MyAssembly.dll` (v2.0) is the only assembly installed.</span></span> <span data-ttu-id="a9220-134">`MyAssembly.Core.dll` (verze 1.0) není nainstalována, protože není uveden ve `net45` složky.</span><span class="sxs-lookup"><span data-stu-id="a9220-134">`MyAssembly.Core.dll` (v1.0) is not installed because it's not listed in the `net45` folder.</span></span> <span data-ttu-id="a9220-135">NuGet chová tímto způsobem, protože `MyAssembly.Core.dll` může mít sloučené do verze 2.0 `MyAssembly.dll`.</span><span class="sxs-lookup"><span data-stu-id="a9220-135">NuGet behaves this way because `MyAssembly.Core.dll` might have merged into version 2.0 of `MyAssembly.dll`.</span></span>

<span data-ttu-id="a9220-136">Chcete-li `MyAssembly.Core.dll` k instalaci pro rozhraní .NET Framework 4.5, umístěte kopii v `net45` složky.</span><span class="sxs-lookup"><span data-stu-id="a9220-136">If you want `MyAssembly.Core.dll` to be installed for .NET Framework 4.5, place a copy in the `net45` folder.</span></span>

## <a name="grouping-assemblies-by-framework-profile"></a><span data-ttu-id="a9220-137">Seskupení sestavení profilem framework</span><span class="sxs-lookup"><span data-stu-id="a9220-137">Grouping assemblies by framework profile</span></span>

<span data-ttu-id="a9220-138">Cílení na konkrétní framework profil připojením pomlčkou a název profilu na konec složce podporuje také NuGet.</span><span class="sxs-lookup"><span data-stu-id="a9220-138">NuGet also supports targeting a specific framework profile by appending a dash and the profile name to the end of the folder.</span></span>

    lib\{framework name}-{profile}

<span data-ttu-id="a9220-139">Podporované profily jsou následující:</span><span class="sxs-lookup"><span data-stu-id="a9220-139">The supported profiles are as follows:</span></span>

- <span data-ttu-id="a9220-140">`client`: Profil klienta</span><span class="sxs-lookup"><span data-stu-id="a9220-140">`client`: Client Profile</span></span>
- <span data-ttu-id="a9220-141">`full`: Full Profile</span><span class="sxs-lookup"><span data-stu-id="a9220-141">`full`: Full Profile</span></span>
- <span data-ttu-id="a9220-142">`wp`: Windows Phone</span><span class="sxs-lookup"><span data-stu-id="a9220-142">`wp`: Windows Phone</span></span>
- <span data-ttu-id="a9220-143">`cf`: Compact Framework</span><span class="sxs-lookup"><span data-stu-id="a9220-143">`cf`: Compact Framework</span></span>

## <a name="determining-which-nuget-target-to-use"></a><span data-ttu-id="a9220-144">Určení, který NuGet cíle použít</span><span class="sxs-lookup"><span data-stu-id="a9220-144">Determining which NuGet target to use</span></span>

<span data-ttu-id="a9220-145">Při vytváření balíčků knihovny cílení na přenosné knihovny tříd může být složité určit, který NuGet cílový ve složce názvy byste měli používat a `.nuspec` souboru, zvlášť pokud cílení jenom podmnožinu PCL.</span><span class="sxs-lookup"><span data-stu-id="a9220-145">When packaging libraries targeting the Portable Class Library it can be tricky to determine which NuGet target you should use in your folder names and `.nuspec` file, especially if targeting only a subset of the PCL.</span></span> <span data-ttu-id="a9220-146">Následující externí prostředky vám pomůže s tímto:</span><span class="sxs-lookup"><span data-stu-id="a9220-146">The following external resources will help you with this:</span></span>

- <span data-ttu-id="a9220-147">[Profily Framework v rozhraní .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)</span><span class="sxs-lookup"><span data-stu-id="a9220-147">[Framework profiles in .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)</span></span>
- <span data-ttu-id="a9220-148">[Přenosná knihovna tříd profily](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): tabulka výčtu PCL profily a jejich ekvivalent cíle NuGet</span><span class="sxs-lookup"><span data-stu-id="a9220-148">[Portable Class Library profiles](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Table enumerating PCL profiles and their equivalent NuGet targets</span></span>
- <span data-ttu-id="a9220-149">[Přenosná knihovna tříd profily nástroj](https://github.com/StephenCleary/PortableLibraryProfiles) (webu github.com): nástroj příkazového řádku pro určení PCL profilů dostupných v systému</span><span class="sxs-lookup"><span data-stu-id="a9220-149">[Portable Class Library profiles tool](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): command line tool for determining PCL profiles available on your system</span></span>

## <a name="content-files-and-powershell-scripts"></a><span data-ttu-id="a9220-150">Soubory obsahu a skriptů prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9220-150">Content files and PowerShell scripts</span></span>

> [!Warning]
> <span data-ttu-id="a9220-151">Měnitelný soubory obsahu a spouštění skriptů jsou k dispozici `packages.config` formát pouze; se nepoužívají v jiném formátu a by nemělo být použito pro všechny nové balíčky.</span><span class="sxs-lookup"><span data-stu-id="a9220-151">Mutable content files and script execution are available with the `packages.config` format only; they are deprecated with all other formats and should not be used for any new packages.</span></span>

<span data-ttu-id="a9220-152">S `packages.config`, obsahu, soubory a skripty prostředí PowerShell lze seskupovat podle cílové rozhraní, pomocí stejné konvence složky uvnitř `content` a `tools` složek.</span><span class="sxs-lookup"><span data-stu-id="a9220-152">With `packages.config`, content files and PowerShell scripts can be grouped by target framework using the same folder convention inside the `content` and `tools` folders.</span></span> <span data-ttu-id="a9220-153">Příklad:</span><span class="sxs-lookup"><span data-stu-id="a9220-153">For example:</span></span>

    \content
        \net46
            \MyContent.txt
        \net461
            \MyContent461.txt
        \uap
            \MyUWPContent.html
        \netcore
    \tools
        init.ps1
        \net46
            install.ps1
            uninstall.ps1
        \uap
            install.ps1
            uninstall.ps1

<span data-ttu-id="a9220-154">Pokud složku rozhraní je prázdné, není NuGet přidejte odkazy na sestavení nebo soubory obsahu nebo spuštění skriptů prostředí PowerShell dané platformy.</span><span class="sxs-lookup"><span data-stu-id="a9220-154">If a framework folder is left empty, NuGet doesn't add assembly references or content files or run the PowerShell scripts for that framework.</span></span>

> [!Note]
> <span data-ttu-id="a9220-155">Protože `init.ps1` se spustí v řešení úrovně a není závislá na projekt, je nutné ji umístit přímo pod `tools` složky.</span><span class="sxs-lookup"><span data-stu-id="a9220-155">Because `init.ps1` is executed at the solution level and not dependent on project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="a9220-156">Pokud se umístit pod složku rozhraní je ignorován.</span><span class="sxs-lookup"><span data-stu-id="a9220-156">It's ignored if placed under a framework folder.</span></span>
