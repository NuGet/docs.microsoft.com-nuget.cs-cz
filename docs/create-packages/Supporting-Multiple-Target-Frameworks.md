---
title: Cílení na více verzí pro balíčky NuGet
description: Popis různých metod k cílení na více verzí rozhraní .NET Framework z v rámci jednoho balíčku NuGet.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 09/27/2017
ms.topic: conceptual
ms.openlocfilehash: 9bdcff8210c192a695a5645f28ef88087469ec52
ms.sourcegitcommit: f0b31af805183cf3a98eabb504e16d9b05223cfe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/22/2018
---
# <a name="supporting-multiple-net-framework-versions"></a><span data-ttu-id="9885d-103">Podpora více verzí rozhraní .NET framework</span><span class="sxs-lookup"><span data-stu-id="9885d-103">Supporting multiple .NET framework versions</span></span>

<span data-ttu-id="9885d-104">*Projekty .NET Core pomocí nástroje NuGet 4.0 +, najdete v části [NuGet pack a obnovit jako cíle MSBuild](../reference/msbuild-targets.md) podrobnosti o cílení na více verzí.*</span><span class="sxs-lookup"><span data-stu-id="9885d-104">*For .NET Core projects using NuGet 4.0+, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md) for details on cross-targeting.*</span></span>

<span data-ttu-id="9885d-105">Mnoho knihovny cílení na konkrétní verzi rozhraní .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="9885d-105">Many libraries target a specific version of the .NET Framework.</span></span> <span data-ttu-id="9885d-106">Například můžete mít jednu verzi knihovnu, která je specifická pro UPW a jinou verzi, která využívá funkce v rozhraní .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="9885d-106">For example, you might have one version of your library that's specific to UWP, and another version that takes advantage of features in .NET Framework 4.6.</span></span>

<span data-ttu-id="9885d-107">Pro přizpůsobení, podporuje NuGet uvedení více verzí stejnou knihovnu v jeden balíček, při použití založené na konvenci pracovní adresář metoda popsaná v [vytváření balíčku](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="9885d-107">To accommodate this, NuGet supports putting multiple versions of the same library in a single package when using the convention-based working directory method described in [Creating a package](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span>

## <a name="framework-version-folder-structure"></a><span data-ttu-id="9885d-108">Struktura složek Framework verze</span><span class="sxs-lookup"><span data-stu-id="9885d-108">Framework version folder structure</span></span>

<span data-ttu-id="9885d-109">Při vytváření balíčku, který obsahuje pouze jednu verzi knihovny nebo cílové více rozhraní, je vytvořit podsložky `lib` pomocí různých malá a velká písmena framework názvy následující konvence:</span><span class="sxs-lookup"><span data-stu-id="9885d-109">When building a package that contains only one version of a library or target multiple frameworks, you always make subfolders under `lib` using different case-sensitive framework names with the following convention:</span></span>

    lib\{framework name}[{version}]

<span data-ttu-id="9885d-110">Úplný seznam podporovaných názvy, najdete v článku [odkazovat na cílové rozhraní](../reference/target-frameworks.md#supported-frameworks).</span><span class="sxs-lookup"><span data-stu-id="9885d-110">For a complete list of supported names, see the [Target Frameworks reference](../reference/target-frameworks.md#supported-frameworks).</span></span>

<span data-ttu-id="9885d-111">Nikdy byste měli mít verzi knihovny, které nejsou specifické pro rozhraní a umístěný přímo v kořenu `lib` složky.</span><span class="sxs-lookup"><span data-stu-id="9885d-111">You should never have a version of the library that is not specific to a framework and placed directly in the root `lib` folder.</span></span> <span data-ttu-id="9885d-112">(Tato možnost se podporuje jenom s `packages.config`).</span><span class="sxs-lookup"><span data-stu-id="9885d-112">(This capability was supported only with `packages.config`).</span></span> <span data-ttu-id="9885d-113">To by upravit knihovny kompatibilní se žádné cílové rozhraní a povolit, aby byl nainstalován odkudkoli, pravděpodobně vést k chybám za běhu neočekávané.</span><span class="sxs-lookup"><span data-stu-id="9885d-113">Doing so would make the library compatible with any target framework and allow it to be installed anywhere, likely resulting in unexpected runtime errors.</span></span> <span data-ttu-id="9885d-114">Přidání sestavení v kořenové složce (například `lib\abc.dll`) nebo v jejich podsložkách (například `lib\abc\abc.dll`) se už nepoužívá a je ignorována, pokud v PackagesReference formátu.</span><span class="sxs-lookup"><span data-stu-id="9885d-114">Adding assemblies in the root folder (such as `lib\abc.dll`) or subfolders (such as `lib\abc\abc.dll`) has been deprecated and is ignored when using the PackagesReference format.</span></span>

<span data-ttu-id="9885d-115">Například následující strukturu složek podporuje čtyři verze sestavení, které jsou specifické pro framework:</span><span class="sxs-lookup"><span data-stu-id="9885d-115">For example, the following folder structure supports four versions of an assembly that are framework-specific:</span></span>

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

<span data-ttu-id="9885d-116">Při vytváření balíčku snadno zahrnout všechny tyto soubory, použijte rekurzivního `**` zástupný znak v `<files>` část vaší `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="9885d-116">To easily include all these files when building the package, use a recursive `**` wildcard in the `<files>` section of your `.nuspec`:</span></span>

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a><span data-ttu-id="9885d-117">Architektura konkrétní složky</span><span class="sxs-lookup"><span data-stu-id="9885d-117">Architecture-specific folders</span></span>

<span data-ttu-id="9885d-118">Pokud máte specifické pro architekturu sestavení, to znamená, samostatné sestavení, které cílí ARM, x 86 a x64, můžete je nutné umístit do složky s názvem `runtimes` v rámci dílčí složky s názvem `{platform}-{architecture}\lib\{framework}` nebo `{platform}-{architecture}\native`.</span><span class="sxs-lookup"><span data-stu-id="9885d-118">If you have architecture-specific assemblies, that is, separate assemblies that target ARM, x86, and x64, you must place them in a folder named `runtimes` within sub-folders named `{platform}-{architecture}\lib\{framework}` or `{platform}-{architecture}\native`.</span></span> <span data-ttu-id="9885d-119">Například následující strukturu složek by zohlednit nativní a spravovaná knihovny DLL cílení na Windows 10 a `uap10.0` framework:</span><span class="sxs-lookup"><span data-stu-id="9885d-119">For example, the following folder structure would accommodate both native and managed DLLs targeting Windows 10 and the `uap10.0` framework:</span></span>

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

<span data-ttu-id="9885d-120">V tématu [vytvořit balíčky UWP](../guides/create-uwp-packages.md) příklad odkazující na tyto soubory v `.nuspec` manifest.</span><span class="sxs-lookup"><span data-stu-id="9885d-120">See [Create UWP Packages](../guides/create-uwp-packages.md) for an example of referencing these files in the `.nuspec` manifest.</span></span>

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a><span data-ttu-id="9885d-121">Odpovídající verze sestavení a cílové rozhraní v projektu</span><span class="sxs-lookup"><span data-stu-id="9885d-121">Matching assembly versions and the target framework in a project</span></span>

<span data-ttu-id="9885d-122">Když NuGet nainstaluje balíček, který má více verzí sestavení, pokusí se shodovat s názvem framework sestavení s cílový framework projektu.</span><span class="sxs-lookup"><span data-stu-id="9885d-122">When NuGet installs a package that has multiple assembly versions, it tries to match the framework name of the assembly with the target framework of the project.</span></span>

<span data-ttu-id="9885d-123">Pokud není nalezena shoda, zkopíruje NuGet sestavení pro nejvyšší verzi, která je menší než nebo rovno cílový framework projektu na, pokud je k dispozici.</span><span class="sxs-lookup"><span data-stu-id="9885d-123">If a match is not found, NuGet copies the assembly for the highest version that is less than or equal to the project's target framework, if available.</span></span> <span data-ttu-id="9885d-124">Pokud se nenajde žádné kompatibilní sestavení, vrátí NuGet příslušná chybová zpráva.</span><span class="sxs-lookup"><span data-stu-id="9885d-124">If no compatible assembly is found, NuGet returns an appropriate error message.</span></span>

<span data-ttu-id="9885d-125">Zvažte například následující strukturu složek v balíčku:</span><span class="sxs-lookup"><span data-stu-id="9885d-125">For example, consider the following folder structure in a package:</span></span>

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

<span data-ttu-id="9885d-126">Pokud při instalaci tohoto balíčku do projektu, jehož cílem rozhraní .NET Framework 4.6, NuGet nainstaluje sestavení v `net45` složky, protože se jedná o nejvyšší verzi k dispozici, která je menší než nebo rovna 4.6.</span><span class="sxs-lookup"><span data-stu-id="9885d-126">When installing this package in a project that targets .NET Framework 4.6, NuGet installs the assembly in the `net45` folder, because that's the highest available version that's less than or equal to 4.6.</span></span>

<span data-ttu-id="9885d-127">Pokud projekt cílem rozhraní .NET Framework 4.6.1, na druhé straně NuGet nainstaluje sestavení v `net461` složky.</span><span class="sxs-lookup"><span data-stu-id="9885d-127">If the project targets .NET Framework 4.6.1, on the other hand, NuGet installs the assembly in the `net461` folder.</span></span>

<span data-ttu-id="9885d-128">Pokud projekt cílem rozhraní .NET framework 4.0 a starší, vyvolá NuGet příslušná chybová zpráva pro nemůžete najít kompatibilní sestavení.</span><span class="sxs-lookup"><span data-stu-id="9885d-128">If the project targets .NET framework 4.0 and earlier, NuGet throws an appropriate error message for not finding the compatible assembly.</span></span>

## <a name="grouping-assemblies-by-framework-version"></a><span data-ttu-id="9885d-129">Seskupování podle framework, verze sestavení</span><span class="sxs-lookup"><span data-stu-id="9885d-129">Grouping assemblies by framework version</span></span>

<span data-ttu-id="9885d-130">NuGet zkopíruje sestavení ze pouze jediná knihovna složky v balíčku.</span><span class="sxs-lookup"><span data-stu-id="9885d-130">NuGet copies assemblies from only a single library folder in the package.</span></span> <span data-ttu-id="9885d-131">Předpokládejme například, že balíček má následující strukturu složek:</span><span class="sxs-lookup"><span data-stu-id="9885d-131">For example, suppose a package has the following folder structure:</span></span>

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

<span data-ttu-id="9885d-132">Při instalaci balíčku v projektu, jehož cílem rozhraní .NET Framework 4.5, `MyAssembly.dll` (v2.0) je nainstalována pouze sestavení.</span><span class="sxs-lookup"><span data-stu-id="9885d-132">When the package is installed in a project that targets .NET Framework 4.5, `MyAssembly.dll` (v2.0) is the only assembly installed.</span></span> <span data-ttu-id="9885d-133">`MyAssembly.Core.dll` (verze 1.0) není nainstalována, protože není uveden ve `net45` složky.</span><span class="sxs-lookup"><span data-stu-id="9885d-133">`MyAssembly.Core.dll` (v1.0) is not installed because it's not listed in the `net45` folder.</span></span> <span data-ttu-id="9885d-134">NuGet chová tímto způsobem, protože `MyAssembly.Core.dll` může mít sloučené do verze 2.0 `MyAssembly.dll`.</span><span class="sxs-lookup"><span data-stu-id="9885d-134">NuGet behaves this way because `MyAssembly.Core.dll` might have merged into version 2.0 of `MyAssembly.dll`.</span></span>

<span data-ttu-id="9885d-135">Chcete-li `MyAssembly.Core.dll` k instalaci pro rozhraní .NET Framework 4.5, umístěte kopii v `net45` složky.</span><span class="sxs-lookup"><span data-stu-id="9885d-135">If you want `MyAssembly.Core.dll` to be installed for .NET Framework 4.5, place a copy in the `net45` folder.</span></span>

## <a name="grouping-assemblies-by-framework-profile"></a><span data-ttu-id="9885d-136">Seskupení sestavení profilem framework</span><span class="sxs-lookup"><span data-stu-id="9885d-136">Grouping assemblies by framework profile</span></span>

<span data-ttu-id="9885d-137">Cílení na konkrétní framework profil připojením pomlčkou a název profilu na konec složce podporuje také NuGet.</span><span class="sxs-lookup"><span data-stu-id="9885d-137">NuGet also supports targeting a specific framework profile by appending a dash and the profile name to the end of the folder.</span></span>

    lib\{framework name}-{profile}

<span data-ttu-id="9885d-138">Podporované profily jsou následující:</span><span class="sxs-lookup"><span data-stu-id="9885d-138">The supported profiles are as follows:</span></span>

- <span data-ttu-id="9885d-139">`client`: Profil klienta</span><span class="sxs-lookup"><span data-stu-id="9885d-139">`client`: Client Profile</span></span>
- <span data-ttu-id="9885d-140">`full`: Full Profile</span><span class="sxs-lookup"><span data-stu-id="9885d-140">`full`: Full Profile</span></span>
- <span data-ttu-id="9885d-141">`wp`: Windows Phone</span><span class="sxs-lookup"><span data-stu-id="9885d-141">`wp`: Windows Phone</span></span>
- <span data-ttu-id="9885d-142">`cf`: Compact Framework</span><span class="sxs-lookup"><span data-stu-id="9885d-142">`cf`: Compact Framework</span></span>

## <a name="determining-which-nuget-target-to-use"></a><span data-ttu-id="9885d-143">Určení, který NuGet cíle použít</span><span class="sxs-lookup"><span data-stu-id="9885d-143">Determining which NuGet target to use</span></span>

<span data-ttu-id="9885d-144">Při vytváření balíčků knihovny cílení na přenosné knihovny tříd může být složité určit, který NuGet cílový ve složce názvy byste měli používat a `.nuspec` souboru, zvlášť pokud cílení jenom podmnožinu PCL.</span><span class="sxs-lookup"><span data-stu-id="9885d-144">When packaging libraries targeting the Portable Class Library it can be tricky to determine which NuGet target you should use in your folder names and `.nuspec` file, especially if targeting only a subset of the PCL.</span></span> <span data-ttu-id="9885d-145">Následující externí prostředky vám pomůže s tímto:</span><span class="sxs-lookup"><span data-stu-id="9885d-145">The following external resources will help you with this:</span></span>

- <span data-ttu-id="9885d-146">[Profily Framework v rozhraní .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)</span><span class="sxs-lookup"><span data-stu-id="9885d-146">[Framework profiles in .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)</span></span>
- <span data-ttu-id="9885d-147">[Přenosná knihovna tříd profily](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): tabulka výčtu PCL profily a jejich ekvivalent cíle NuGet</span><span class="sxs-lookup"><span data-stu-id="9885d-147">[Portable Class Library profiles](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Table enumerating PCL profiles and their equivalent NuGet targets</span></span>
- <span data-ttu-id="9885d-148">[Přenosná knihovna tříd profily nástroj](https://github.com/StephenCleary/PortableLibraryProfiles) (webu github.com): nástroj příkazového řádku pro určení PCL profilů dostupných v systému</span><span class="sxs-lookup"><span data-stu-id="9885d-148">[Portable Class Library profiles tool](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): command line tool for determining PCL profiles available on your system</span></span>

## <a name="content-files-and-powershell-scripts"></a><span data-ttu-id="9885d-149">Soubory obsahu a skriptů prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="9885d-149">Content files and PowerShell scripts</span></span>

> [!Warning]
> <span data-ttu-id="9885d-150">Měnitelný soubory obsahu a spouštění skriptů jsou k dispozici `packages.config` formát pouze; se nepoužívají v jiném formátu a by nemělo být použito pro všechny nové balíčky.</span><span class="sxs-lookup"><span data-stu-id="9885d-150">Mutable content files and script execution are available with the `packages.config` format only; they are deprecated with all other formats and should not be used for any new packages.</span></span>

<span data-ttu-id="9885d-151">S `packages.config`, obsahu, soubory a skripty prostředí PowerShell lze seskupovat podle cílové rozhraní, pomocí stejné konvence složky uvnitř `content` a `tools` složek.</span><span class="sxs-lookup"><span data-stu-id="9885d-151">With `packages.config`, content files and PowerShell scripts can be grouped by target framework using the same folder convention inside the `content` and `tools` folders.</span></span> <span data-ttu-id="9885d-152">Příklad:</span><span class="sxs-lookup"><span data-stu-id="9885d-152">For example:</span></span>

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

<span data-ttu-id="9885d-153">Pokud složku rozhraní je prázdné, není NuGet přidejte odkazy na sestavení nebo soubory obsahu nebo spuštění skriptů prostředí PowerShell dané platformy.</span><span class="sxs-lookup"><span data-stu-id="9885d-153">If a framework folder is left empty, NuGet doesn't add assembly references or content files or run the PowerShell scripts for that framework.</span></span>

> [!Note]
> <span data-ttu-id="9885d-154">Protože `init.ps1` se spustí v řešení úrovně a není závislá na projekt, je nutné ji umístit přímo pod `tools` složky.</span><span class="sxs-lookup"><span data-stu-id="9885d-154">Because `init.ps1` is executed at the solution level and not dependent on project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="9885d-155">Pokud se umístit pod složku rozhraní je ignorován.</span><span class="sxs-lookup"><span data-stu-id="9885d-155">It's ignored if placed under a framework folder.</span></span>