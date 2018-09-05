---
title: Cílení na více platforem pro balíčky NuGet
description: Popis různých metod cílit na více verzí rozhraní .NET Framework z v rámci jednoho balíčku NuGet.
author: karann-msft
ms.author: karann
ms.date: 09/27/2017
ms.topic: conceptual
ms.openlocfilehash: 0b22d48b9151b903a5307beafa5ccef14e5fecf3
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551703"
---
# <a name="supporting-multiple-net-framework-versions"></a><span data-ttu-id="50629-103">Podpora více verzí rozhraní .NET framework</span><span class="sxs-lookup"><span data-stu-id="50629-103">Supporting multiple .NET framework versions</span></span>

<span data-ttu-id="50629-104">*Pro projekty .NET Core pomocí nástroje NuGet 4.0 +, naleznete v tématu [NuGet aktualizací Service pack a obnovení jako cílů MSBuild](../reference/msbuild-targets.md) podrobnosti o cílení na různé.*</span><span class="sxs-lookup"><span data-stu-id="50629-104">*For .NET Core projects using NuGet 4.0+, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md) for details on cross-targeting.*</span></span>

<span data-ttu-id="50629-105">Mnoho knihoven mířila na konkrétní verzi rozhraní .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="50629-105">Many libraries target a specific version of the .NET Framework.</span></span> <span data-ttu-id="50629-106">Například může mít jednu verzi knihovny, která je specifická pro UPW a jinou verzi, která využívá funkce sady rozhraní .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="50629-106">For example, you might have one version of your library that's specific to UWP, and another version that takes advantage of features in .NET Framework 4.6.</span></span>

<span data-ttu-id="50629-107">Aby se tomuto, podporuje NuGet uvedení více verzí stejného knihovny v jediném balíčku, při použití založené na konvenci pracovní adresář metody popsané v [vytvoření balíčku](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="50629-107">To accommodate this, NuGet supports putting multiple versions of the same library in a single package when using the convention-based working directory method described in [Creating a package](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span>

## <a name="framework-version-folder-structure"></a><span data-ttu-id="50629-108">Struktura složek verzi rozhraní Framework</span><span class="sxs-lookup"><span data-stu-id="50629-108">Framework version folder structure</span></span>

<span data-ttu-id="50629-109">Při vytváření balíčku, který obsahuje pouze jednu verzi knihovny nebo cílové více rozhraní, byste vždy měli vytvořit podsložky `lib` názvy jiné rozhraní malá a velká písmena pomocí následující konvence:</span><span class="sxs-lookup"><span data-stu-id="50629-109">When building a package that contains only one version of a library or target multiple frameworks, you always make subfolders under `lib` using different case-sensitive framework names with the following convention:</span></span>

    lib\{framework name}[{version}]

<span data-ttu-id="50629-110">Úplný seznam podporovaných názvy, najdete v článku [odkazovat na cílové rozhraní](../reference/target-frameworks.md#supported-frameworks).</span><span class="sxs-lookup"><span data-stu-id="50629-110">For a complete list of supported names, see the [Target Frameworks reference](../reference/target-frameworks.md#supported-frameworks).</span></span>

<span data-ttu-id="50629-111">Nikdy byste měli mít verzi knihovny, které nejsou specifické pro architekturu a umístěný přímo v kořenovém adresáři `lib` složky.</span><span class="sxs-lookup"><span data-stu-id="50629-111">You should never have a version of the library that is not specific to a framework and placed directly in the root `lib` folder.</span></span> <span data-ttu-id="50629-112">(Tato možnost je podporován pouze s `packages.config`).</span><span class="sxs-lookup"><span data-stu-id="50629-112">(This capability was supported only with `packages.config`).</span></span> <span data-ttu-id="50629-113">Mohlo by nastavit knihovnu jako kompatibilní s žádné cílové rozhraní framework a umožňují, aby byl nainstalován kdekoli, pravděpodobně výsledkem neočekávané běhové chyby.</span><span class="sxs-lookup"><span data-stu-id="50629-113">Doing so would make the library compatible with any target framework and allow it to be installed anywhere, likely resulting in unexpected runtime errors.</span></span> <span data-ttu-id="50629-114">Přidávání sestavení do kořenové složky (například `lib\abc.dll`) nebo v jejích podsložkách (například `lib\abc\abc.dll`) je zastaralá a je ignorován při použití formátu PackagesReference.</span><span class="sxs-lookup"><span data-stu-id="50629-114">Adding assemblies in the root folder (such as `lib\abc.dll`) or subfolders (such as `lib\abc\abc.dll`) has been deprecated and is ignored when using the PackagesReference format.</span></span>

<span data-ttu-id="50629-115">Například následující strukturu složek podporuje čtyři verze sestavení, které jsou specifické pro architekturu:</span><span class="sxs-lookup"><span data-stu-id="50629-115">For example, the following folder structure supports four versions of an assembly that are framework-specific:</span></span>

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

<span data-ttu-id="50629-116">Snadno zahrnout všechny tyto soubory při sestavování balíčku, použít k rekurzivnímu `**` zástupných znaků v `<files>` část vaší `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="50629-116">To easily include all these files when building the package, use a recursive `**` wildcard in the `<files>` section of your `.nuspec`:</span></span>

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a><span data-ttu-id="50629-117">Složky specifické pro architekturu</span><span class="sxs-lookup"><span data-stu-id="50629-117">Architecture-specific folders</span></span>

<span data-ttu-id="50629-118">Pokud máte specifické pro architekturu sestavení, to znamená, samostatné sestavení, které se zaměřují ARM, x 86 a x64, je nutné je umístit do složky s názvem `runtimes` do podsložky s názvem `{platform}-{architecture}\lib\{framework}` nebo `{platform}-{architecture}\native`.</span><span class="sxs-lookup"><span data-stu-id="50629-118">If you have architecture-specific assemblies, that is, separate assemblies that target ARM, x86, and x64, you must place them in a folder named `runtimes` within sub-folders named `{platform}-{architecture}\lib\{framework}` or `{platform}-{architecture}\native`.</span></span> <span data-ttu-id="50629-119">Například následující strukturu složek by odpovídala knihovny DLL nativního a spravovaného cílení na Windows 10 a `uap10.0` framework:</span><span class="sxs-lookup"><span data-stu-id="50629-119">For example, the following folder structure would accommodate both native and managed DLLs targeting Windows 10 and the `uap10.0` framework:</span></span>

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

<span data-ttu-id="50629-120">Naleznete v tématu [vytvoření balíčků UPW](../guides/create-uwp-packages.md) příklad odkazování na tyto soubory `.nuspec` manifestu.</span><span class="sxs-lookup"><span data-stu-id="50629-120">See [Create UWP Packages](../guides/create-uwp-packages.md) for an example of referencing these files in the `.nuspec` manifest.</span></span>

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a><span data-ttu-id="50629-121">Odpovídající verze sestavení a Cílová architektura, která v projektu</span><span class="sxs-lookup"><span data-stu-id="50629-121">Matching assembly versions and the target framework in a project</span></span>

<span data-ttu-id="50629-122">NuGet nainstaluje balíček, který má více verzí sestavení, pokusí se vyhledat název rozhraní sestavení s cílovou architekturu projektu.</span><span class="sxs-lookup"><span data-stu-id="50629-122">When NuGet installs a package that has multiple assembly versions, it tries to match the framework name of the assembly with the target framework of the project.</span></span>

<span data-ttu-id="50629-123">Pokud není nalezena shoda, zkopíruje NuGet sestavení nejvyšší verze, která je menší než nebo rovna cílové rozhraní projektu, pokud je k dispozici.</span><span class="sxs-lookup"><span data-stu-id="50629-123">If a match is not found, NuGet copies the assembly for the highest version that is less than or equal to the project's target framework, if available.</span></span> <span data-ttu-id="50629-124">Pokud se nenajde žádné kompatibilní sestavení, NuGet vrátí příslušnou chybovou zprávu.</span><span class="sxs-lookup"><span data-stu-id="50629-124">If no compatible assembly is found, NuGet returns an appropriate error message.</span></span>

<span data-ttu-id="50629-125">Zvažte například následující strukturu složky v balíčku:</span><span class="sxs-lookup"><span data-stu-id="50629-125">For example, consider the following folder structure in a package:</span></span>

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

<span data-ttu-id="50629-126">Při instalaci tohoto balíčku v projektu, který cílí na rozhraní .NET Framework 4.6, NuGet nainstaluje sestavení v `net45` složky, protože to je nejvyšší dostupná verze, která je menší než nebo rovna 4.6.</span><span class="sxs-lookup"><span data-stu-id="50629-126">When installing this package in a project that targets .NET Framework 4.6, NuGet installs the assembly in the `net45` folder, because that's the highest available version that's less than or equal to 4.6.</span></span>

<span data-ttu-id="50629-127">Pokud projekt cílí na rozhraní .NET Framework 4.6.1, na druhé straně NuGet nainstaluje sestavení v `net461` složky.</span><span class="sxs-lookup"><span data-stu-id="50629-127">If the project targets .NET Framework 4.6.1, on the other hand, NuGet installs the assembly in the `net461` folder.</span></span>

<span data-ttu-id="50629-128">Pokud projekt cílí na rozhraní .NET framework 4.0 a starší, vyvolá NuGet příslušnou chybovou zprávu pro nenašli kompatibilní sestavení.</span><span class="sxs-lookup"><span data-stu-id="50629-128">If the project targets .NET framework 4.0 and earlier, NuGet throws an appropriate error message for not finding the compatible assembly.</span></span>

## <a name="grouping-assemblies-by-framework-version"></a><span data-ttu-id="50629-129">Seskupení sestavení ve verzi rozhraní framework</span><span class="sxs-lookup"><span data-stu-id="50629-129">Grouping assemblies by framework version</span></span>

<span data-ttu-id="50629-130">NuGet zkopíruje sestavení ze složky v balíčku pouze jediná knihovna.</span><span class="sxs-lookup"><span data-stu-id="50629-130">NuGet copies assemblies from only a single library folder in the package.</span></span> <span data-ttu-id="50629-131">Předpokládejme například, že balíček má následující strukturu složek:</span><span class="sxs-lookup"><span data-stu-id="50629-131">For example, suppose a package has the following folder structure:</span></span>

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

<span data-ttu-id="50629-132">Při instalaci balíčku v projektu, který cílí na rozhraní .NET Framework 4.5, `MyAssembly.dll` (v2.0) je pouze sestavení nainstalována.</span><span class="sxs-lookup"><span data-stu-id="50629-132">When the package is installed in a project that targets .NET Framework 4.5, `MyAssembly.dll` (v2.0) is the only assembly installed.</span></span> <span data-ttu-id="50629-133">`MyAssembly.Core.dll` (verze 1.0) není nainstalována, protože není uveden v `net45` složky.</span><span class="sxs-lookup"><span data-stu-id="50629-133">`MyAssembly.Core.dll` (v1.0) is not installed because it's not listed in the `net45` folder.</span></span> <span data-ttu-id="50629-134">NuGet chová tímto způsobem, protože `MyAssembly.Core.dll` může mít sloučené do verze 2.0 `MyAssembly.dll`.</span><span class="sxs-lookup"><span data-stu-id="50629-134">NuGet behaves this way because `MyAssembly.Core.dll` might have merged into version 2.0 of `MyAssembly.dll`.</span></span>

<span data-ttu-id="50629-135">Chcete-li `MyAssembly.Core.dll` potřeba instalovat rozhraní .NET Framework 4.5, umístěte kopii `net45` složky.</span><span class="sxs-lookup"><span data-stu-id="50629-135">If you want `MyAssembly.Core.dll` to be installed for .NET Framework 4.5, place a copy in the `net45` folder.</span></span>

## <a name="grouping-assemblies-by-framework-profile"></a><span data-ttu-id="50629-136">Seskupení sestavení v rámci profilu</span><span class="sxs-lookup"><span data-stu-id="50629-136">Grouping assemblies by framework profile</span></span>

<span data-ttu-id="50629-137">NuGet také podporuje cílení na konkrétní verzi rozhraní framework profil přidáním spojovníkem a název profilu na konec složce.</span><span class="sxs-lookup"><span data-stu-id="50629-137">NuGet also supports targeting a specific framework profile by appending a dash and the profile name to the end of the folder.</span></span>

    lib\{framework name}-{profile}

<span data-ttu-id="50629-138">Podporované profily jsou následující:</span><span class="sxs-lookup"><span data-stu-id="50629-138">The supported profiles are as follows:</span></span>

- <span data-ttu-id="50629-139">`client`: Profil klienta</span><span class="sxs-lookup"><span data-stu-id="50629-139">`client`: Client Profile</span></span>
- <span data-ttu-id="50629-140">`full`: Full Profile</span><span class="sxs-lookup"><span data-stu-id="50629-140">`full`: Full Profile</span></span>
- <span data-ttu-id="50629-141">`wp`: Windows Phone</span><span class="sxs-lookup"><span data-stu-id="50629-141">`wp`: Windows Phone</span></span>
- <span data-ttu-id="50629-142">`cf`: Compact Framework</span><span class="sxs-lookup"><span data-stu-id="50629-142">`cf`: Compact Framework</span></span>

## <a name="determining-which-nuget-target-to-use"></a><span data-ttu-id="50629-143">Určení cíl NuGet</span><span class="sxs-lookup"><span data-stu-id="50629-143">Determining which NuGet target to use</span></span>

<span data-ttu-id="50629-144">Při balení knihovny, které cílí přenosné knihovny tříd může být složité určit, které se zaměřují NuGet, abyste používali v názvech složek a `.nuspec` souborů, zejména v případě cílení na pouze podmnožinu PCL.</span><span class="sxs-lookup"><span data-stu-id="50629-144">When packaging libraries targeting the Portable Class Library it can be tricky to determine which NuGet target you should use in your folder names and `.nuspec` file, especially if targeting only a subset of the PCL.</span></span> <span data-ttu-id="50629-145">Tyto externí prostředky vám pomůžou s tímto:</span><span class="sxs-lookup"><span data-stu-id="50629-145">The following external resources will help you with this:</span></span>

- <span data-ttu-id="50629-146">[Profily rozhraní v rozhraní .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)</span><span class="sxs-lookup"><span data-stu-id="50629-146">[Framework profiles in .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)</span></span>
- <span data-ttu-id="50629-147">[Přenosné knihovny tříd profily](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Tabulka výčet PCL profily a jejich odpovídající cíle NuGet</span><span class="sxs-lookup"><span data-stu-id="50629-147">[Portable Class Library profiles](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Table enumerating PCL profiles and their equivalent NuGet targets</span></span>
- <span data-ttu-id="50629-148">[Přenosné knihovny tříd profily nástroj](https://github.com/StephenCleary/PortableLibraryProfiles) (webu github.com): nástroj příkazového řádku pro určení PCL profily k dispozici v systému</span><span class="sxs-lookup"><span data-stu-id="50629-148">[Portable Class Library profiles tool](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): command line tool for determining PCL profiles available on your system</span></span>

## <a name="content-files-and-powershell-scripts"></a><span data-ttu-id="50629-149">Soubory obsahu a skripty prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="50629-149">Content files and PowerShell scripts</span></span>

> [!Warning]
> <span data-ttu-id="50629-150">Jsou k dispozici s měnitelnou soubory obsahu a spuštění skriptu `packages.config` formát pouze; se považují za zastaralé v jiném formátu by se neměl používat pro všechny nové balíčky.</span><span class="sxs-lookup"><span data-stu-id="50629-150">Mutable content files and script execution are available with the `packages.config` format only; they are deprecated with all other formats and should not be used for any new packages.</span></span>

<span data-ttu-id="50629-151">S `packages.config`, obsahu, soubory a skripty prostředí PowerShell můžete seskupit podle cílové rozhraní framework pomocí stejné konvence složky uvnitř `content` a `tools` složek.</span><span class="sxs-lookup"><span data-stu-id="50629-151">With `packages.config`, content files and PowerShell scripts can be grouped by target framework using the same folder convention inside the `content` and `tools` folders.</span></span> <span data-ttu-id="50629-152">Příklad:</span><span class="sxs-lookup"><span data-stu-id="50629-152">For example:</span></span>

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

<span data-ttu-id="50629-153">Pokud je prázdné složky framework, nebude NuGet přidat odkazy na sestavení nebo soubory obsahu nebo spouštění skriptů prostředí PowerShell pro dané rozhraní.</span><span class="sxs-lookup"><span data-stu-id="50629-153">If a framework folder is left empty, NuGet doesn't add assembly references or content files or run the PowerShell scripts for that framework.</span></span>

> [!Note]
> <span data-ttu-id="50629-154">Protože `init.ps1` provádí řešení úrovně a není závislá na projekt, musí být umístěné přímo pod `tools` složky.</span><span class="sxs-lookup"><span data-stu-id="50629-154">Because `init.ps1` is executed at the solution level and not dependent on project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="50629-155">Pokud je umístěn v rámci složky framework je ignorován.</span><span class="sxs-lookup"><span data-stu-id="50629-155">It's ignored if placed under a framework folder.</span></span>
