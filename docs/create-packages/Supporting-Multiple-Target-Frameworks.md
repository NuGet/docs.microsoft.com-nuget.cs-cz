---
title: Cílení na více platforem pro balíčky NuGet
description: Popis různých metod, které cílí na více .NET Framework verzí z jednoho balíčku NuGet.
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: 14483264030dd3bb32c7295886f2d37d52e735cc
ms.sourcegitcommit: fc1b716afda999148eb06d62beedb350643eb346
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/14/2019
ms.locfileid: "69020037"
---
# <a name="support-multiple-net-versions"></a><span data-ttu-id="fcda2-103">Podpora více verzí rozhraní .NET</span><span class="sxs-lookup"><span data-stu-id="fcda2-103">Support multiple .NET versions</span></span>

<span data-ttu-id="fcda2-104">Mnoho knihoven cílí na konkrétní verzi .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="fcda2-104">Many libraries target a specific version of the .NET Framework.</span></span> <span data-ttu-id="fcda2-105">Například můžete mít jednu verzi knihovny, která je specifická pro UWP, a další verzi, která využívá funkce v .NET Framework 4,6.</span><span class="sxs-lookup"><span data-stu-id="fcda2-105">For example, you might have one version of your library that's specific to UWP, and another version that takes advantage of features in .NET Framework 4.6.</span></span> <span data-ttu-id="fcda2-106">Aby to bylo možné, NuGet podporuje vložení více verzí stejné knihovny do jednoho balíčku.</span><span class="sxs-lookup"><span data-stu-id="fcda2-106">To accommodate this, NuGet supports putting multiple versions of the same library in a single package.</span></span>

<span data-ttu-id="fcda2-107">Tento článek popisuje rozložení balíčku NuGet bez ohledu na to, jak je balíček nebo sestavení sestaveno (to znamená, že rozložení je stejné, ať už používáte více souborů *. csproj* , které nejsou typu SDK, a vlastní soubor *. nuspec* nebo jeden targetecd. Sada SDK – Style *. csproj*).</span><span class="sxs-lookup"><span data-stu-id="fcda2-107">This article describes the layout of a NuGet package, regardless of how the package or assemblies are built (that is, the layout is the same whether using multiple non-SDK-style *.csproj* files and a custom *.nuspec* file, or a single multi-targetecd SDK-style *.csproj*).</span></span> <span data-ttu-id="fcda2-108">Pro projekt ve stylu sady SDK zná [cíle sady](../reference/msbuild-targets.md) NuGet, jak musí být balíček layed a automatizuje vložení sestavení do správných složek lib a vytváření skupin závislostí pro každou cílovou architekturu (TFM).</span><span class="sxs-lookup"><span data-stu-id="fcda2-108">For an SDK-style project, NuGet [pack targets](../reference/msbuild-targets.md) knows how the package must be layed out and automates putting the assemblies in the correct lib folders and creating dependency groups for each target framework (TFM).</span></span> <span data-ttu-id="fcda2-109">Podrobné pokyny najdete v tématu [Podpora více .NET Frameworkch verzí v souboru projektu](multiple-target-frameworks-project-file.md).</span><span class="sxs-lookup"><span data-stu-id="fcda2-109">For detailed instructions, see [Support multiple .NET Framework versions in your project file](multiple-target-frameworks-project-file.md).</span></span>

<span data-ttu-id="fcda2-110">Pokud používáte metodu pracovního adresáře založenou na konvenci, která je popsaná v tématu [Vytvoření balíčku](../create-packages/creating-a-package.md#from-a-convention-based-working-directory), musíte balíček ručně rozložit podle pokynů v tomto článku.</span><span class="sxs-lookup"><span data-stu-id="fcda2-110">You must manually lay out the package as described in this article when using the convention-based working directory method described in [Creating a package](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> <span data-ttu-id="fcda2-111">Pro projekt ve stylu sady SDK se doporučuje automatizovaná metoda, ale můžete také zvolit ruční rozložení balíčku, jak je popsáno v tomto článku.</span><span class="sxs-lookup"><span data-stu-id="fcda2-111">For an SDK-style project, the automated method is recommended, but you may also choose to manually lay out the package as described in this article.</span></span>

## <a name="framework-version-folder-structure"></a><span data-ttu-id="fcda2-112">Struktura složek verze rozhraní</span><span class="sxs-lookup"><span data-stu-id="fcda2-112">Framework version folder structure</span></span>

<span data-ttu-id="fcda2-113">Při sestavování balíčku, který obsahuje pouze jednu verzi knihovny nebo cílení na více platforem, je vždy nutné vytvořit `lib` podsložky v rámci používání různých názvů architektury s rozlišováním velkých a malých písmen s následující konvencí:</span><span class="sxs-lookup"><span data-stu-id="fcda2-113">When building a package that contains only one version of a library or target multiple frameworks, you always make subfolders under `lib` using different case-sensitive framework names with the following convention:</span></span>

    lib\{framework name}[{version}]

<span data-ttu-id="fcda2-114">Úplný seznam podporovaných názvů najdete v referenčních informacích o [cílových rozhraních](../reference/target-frameworks.md#supported-frameworks).</span><span class="sxs-lookup"><span data-stu-id="fcda2-114">For a complete list of supported names, see the [Target Frameworks reference](../reference/target-frameworks.md#supported-frameworks).</span></span>

<span data-ttu-id="fcda2-115">Nikdy byste neměli mít verzi knihovny, která není specifická pro rozhraní a umístěna přímo do kořenové `lib` složky.</span><span class="sxs-lookup"><span data-stu-id="fcda2-115">You should never have a version of the library that is not specific to a framework and placed directly in the root `lib` folder.</span></span> <span data-ttu-id="fcda2-116">(Tato schopnost byla podporovaná jenom `packages.config`s.)</span><span class="sxs-lookup"><span data-stu-id="fcda2-116">(This capability was supported only with `packages.config`).</span></span> <span data-ttu-id="fcda2-117">Díky tomu by knihovna byla kompatibilní s libovolným cílovou architekturou a povolila se její instalace kdekoli, což pravděpodobně způsobí neočekávané chyby za běhu.</span><span class="sxs-lookup"><span data-stu-id="fcda2-117">Doing so would make the library compatible with any target framework and allow it to be installed anywhere, likely resulting in unexpected runtime errors.</span></span> <span data-ttu-id="fcda2-118">Přidání sestavení do kořenové složky (například `lib\abc.dll`) nebo podsložek ( `lib\abc\abc.dll`například) se už nepoužívá a při použití formátu PackagesReference se ignoruje.</span><span class="sxs-lookup"><span data-stu-id="fcda2-118">Adding assemblies in the root folder (such as `lib\abc.dll`) or subfolders (such as `lib\abc\abc.dll`) has been deprecated and is ignored when using the PackagesReference format.</span></span>

<span data-ttu-id="fcda2-119">Například následující struktura složek podporuje čtyři verze sestavení, které jsou specifické pro rozhraní:</span><span class="sxs-lookup"><span data-stu-id="fcda2-119">For example, the following folder structure supports four versions of an assembly that are framework-specific:</span></span>

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

<span data-ttu-id="fcda2-120">Pro snadné zahrnutí všech těchto souborů při sestavování balíčku použijte rekurzivní `**` zástupné znaky `<files>` v části svého: `.nuspec`</span><span class="sxs-lookup"><span data-stu-id="fcda2-120">To easily include all these files when building the package, use a recursive `**` wildcard in the `<files>` section of your `.nuspec`:</span></span>

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a><span data-ttu-id="fcda2-121">Složky specifické pro architekturu</span><span class="sxs-lookup"><span data-stu-id="fcda2-121">Architecture-specific folders</span></span>

<span data-ttu-id="fcda2-122">Pokud máte sestavení pro konkrétní architekturu, tj. samostatná sestavení, která cílí na ARM, x86 a x64, je nutné umístit je do složky s názvem `runtimes` v podsložkách s názvem `{platform}-{architecture}\lib\{framework}` nebo `{platform}-{architecture}\native`.</span><span class="sxs-lookup"><span data-stu-id="fcda2-122">If you have architecture-specific assemblies, that is, separate assemblies that target ARM, x86, and x64, you must place them in a folder named `runtimes` within sub-folders named `{platform}-{architecture}\lib\{framework}` or `{platform}-{architecture}\native`.</span></span> <span data-ttu-id="fcda2-123">Například následující struktura složky by pokryla nativní i spravované knihovny DLL cílící na `uap10.0` Windows 10 a rozhraní:</span><span class="sxs-lookup"><span data-stu-id="fcda2-123">For example, the following folder structure would accommodate both native and managed DLLs targeting Windows 10 and the `uap10.0` framework:</span></span>

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

<span data-ttu-id="fcda2-124">Tato sestavení budou k dispozici pouze za běhu, takže pokud chcete zadat odpovídající sestavení pro čas kompilace a pak mít `AnyCPU` sestavení ve `/ref{tfm}` složce.</span><span class="sxs-lookup"><span data-stu-id="fcda2-124">These assemblies will only be available at runtime, so if you want to provide the corresponding compile time assembly as well then have `AnyCPU` assembly in `/ref{tfm}` folder.</span></span> 

<span data-ttu-id="fcda2-125">Počítejte s tím, že NuGet vždy vybere tyto kompilační nebo běhové prostředky z jedné složky, takže pokud existují některé `/ref` kompatibilní `/lib` prostředky, ze kterých bude možné přidat sestavení v době kompilace, bude ignorováno.</span><span class="sxs-lookup"><span data-stu-id="fcda2-125">Please note, NuGet always picks these compile or runtime assets from one folder so if there are some compatible assets from `/ref` then `/lib` will be ignored to add compile-time assemblies.</span></span> <span data-ttu-id="fcda2-126">Podobně platí, že pokud existují některé prostředky compatbile `/runtime` , ze `/lib` kterých se pak bude pro modul runtime ignorovat také.</span><span class="sxs-lookup"><span data-stu-id="fcda2-126">Similarly, if there are some compatbile assets from `/runtime` then also `/lib` will be ignored for runtime.</span></span>

<span data-ttu-id="fcda2-127">Příklady odkazů na tyto soubory v `.nuspec` manifestu najdete v tématu věnovaném [Vytvoření balíčků UWP](../guides/create-uwp-packages.md) .</span><span class="sxs-lookup"><span data-stu-id="fcda2-127">See [Create UWP Packages](../guides/create-uwp-packages.md) for an example of referencing these files in the `.nuspec` manifest.</span></span>

<span data-ttu-id="fcda2-128">Viz také [balení komponenty aplikace pro Windows Store pomocí nástroje NuGet](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2)</span><span class="sxs-lookup"><span data-stu-id="fcda2-128">Also, see [Packing a Windows store app component with NuGet](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2)</span></span>

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a><span data-ttu-id="fcda2-129">Vyhovující verze sestavení a cílová architektura v projektu</span><span class="sxs-lookup"><span data-stu-id="fcda2-129">Matching assembly versions and the target framework in a project</span></span>

<span data-ttu-id="fcda2-130">Když NuGet nainstaluje balíček s více verzemi sestavení, pokusí se porovnat název rozhraní sestavení s cílovou architekturou projektu.</span><span class="sxs-lookup"><span data-stu-id="fcda2-130">When NuGet installs a package that has multiple assembly versions, it tries to match the framework name of the assembly with the target framework of the project.</span></span>

<span data-ttu-id="fcda2-131">Pokud není nalezena shoda, NuGet zkopíruje sestavení pro nejvyšší verzi, která je menší než nebo rovna cílové verzi rozhraní .NET Framework projektu, je-li k dispozici.</span><span class="sxs-lookup"><span data-stu-id="fcda2-131">If a match is not found, NuGet copies the assembly for the highest version that is less than or equal to the project's target framework, if available.</span></span> <span data-ttu-id="fcda2-132">Pokud není nalezeno žádné kompatibilní sestavení, NuGet vrátí příslušnou chybovou zprávu.</span><span class="sxs-lookup"><span data-stu-id="fcda2-132">If no compatible assembly is found, NuGet returns an appropriate error message.</span></span>

<span data-ttu-id="fcda2-133">Zvažte například následující strukturu složek v balíčku:</span><span class="sxs-lookup"><span data-stu-id="fcda2-133">For example, consider the following folder structure in a package:</span></span>

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

<span data-ttu-id="fcda2-134">Při instalaci tohoto balíčku do projektu, který se zaměřuje na .NET Framework 4,6, NuGet nainstaluje sestavení do `net45` složky, protože to je nejvyšší dostupná verze, která je menší nebo rovna 4,6.</span><span class="sxs-lookup"><span data-stu-id="fcda2-134">When installing this package in a project that targets .NET Framework 4.6, NuGet installs the assembly in the `net45` folder, because that's the highest available version that's less than or equal to 4.6.</span></span>

<span data-ttu-id="fcda2-135">Pokud cílíte na projekt .NET Framework 4.6.1, nainstaluje NuGet do `net461` složky sestavení.</span><span class="sxs-lookup"><span data-stu-id="fcda2-135">If the project targets .NET Framework 4.6.1, on the other hand, NuGet installs the assembly in the `net461` folder.</span></span>

<span data-ttu-id="fcda2-136">Pokud je projekt cílen na rozhraní .NET Framework 4,0 a starší, NuGet vyvolá příslušnou chybovou zprávu pro nalezení kompatibilního sestavení.</span><span class="sxs-lookup"><span data-stu-id="fcda2-136">If the project targets .NET framework 4.0 and earlier, NuGet throws an appropriate error message for not finding the compatible assembly.</span></span>

## <a name="grouping-assemblies-by-framework-version"></a><span data-ttu-id="fcda2-137">Seskupení sestavení podle verze architektury</span><span class="sxs-lookup"><span data-stu-id="fcda2-137">Grouping assemblies by framework version</span></span>

<span data-ttu-id="fcda2-138">NuGet kopíruje sestavení z jediné složky knihovny v balíčku.</span><span class="sxs-lookup"><span data-stu-id="fcda2-138">NuGet copies assemblies from only a single library folder in the package.</span></span> <span data-ttu-id="fcda2-139">Předpokládejme například, že balíček má následující strukturu složek:</span><span class="sxs-lookup"><span data-stu-id="fcda2-139">For example, suppose a package has the following folder structure:</span></span>

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

<span data-ttu-id="fcda2-140">Když je balíček nainstalován v projektu, který cílí na .NET Framework 4,5, `MyAssembly.dll` (v 2.0) je jediné nainstalovaná sestavení.</span><span class="sxs-lookup"><span data-stu-id="fcda2-140">When the package is installed in a project that targets .NET Framework 4.5, `MyAssembly.dll` (v2.0) is the only assembly installed.</span></span> <span data-ttu-id="fcda2-141">`MyAssembly.Core.dll`(v 1.0) není nainstalováno, protože není uvedeno ve `net45` složce.</span><span class="sxs-lookup"><span data-stu-id="fcda2-141">`MyAssembly.Core.dll` (v1.0) is not installed because it's not listed in the `net45` folder.</span></span> <span data-ttu-id="fcda2-142">NuGet se chová tímto způsobem, `MyAssembly.Core.dll` protože se mohl sloučit do verze 2,0 `MyAssembly.dll`systému.</span><span class="sxs-lookup"><span data-stu-id="fcda2-142">NuGet behaves this way because `MyAssembly.Core.dll` might have merged into version 2.0 of `MyAssembly.dll`.</span></span>

<span data-ttu-id="fcda2-143">Pokud chcete nainstalovat .NET Framework 4,5, umístěte kopii `net45` do složky. `MyAssembly.Core.dll`</span><span class="sxs-lookup"><span data-stu-id="fcda2-143">If you want `MyAssembly.Core.dll` to be installed for .NET Framework 4.5, place a copy in the `net45` folder.</span></span>

## <a name="grouping-assemblies-by-framework-profile"></a><span data-ttu-id="fcda2-144">Seskupení sestavení podle profilu architektury</span><span class="sxs-lookup"><span data-stu-id="fcda2-144">Grouping assemblies by framework profile</span></span>

<span data-ttu-id="fcda2-145">NuGet také podporuje cílení na konkrétní profil architektury připojením pomlčky a názvu profilu na konec složky.</span><span class="sxs-lookup"><span data-stu-id="fcda2-145">NuGet also supports targeting a specific framework profile by appending a dash and the profile name to the end of the folder.</span></span>

    lib\{framework name}-{profile}

<span data-ttu-id="fcda2-146">Podporované profily jsou následující:</span><span class="sxs-lookup"><span data-stu-id="fcda2-146">The supported profiles are as follows:</span></span>

- <span data-ttu-id="fcda2-147">`client`: Profil klienta</span><span class="sxs-lookup"><span data-stu-id="fcda2-147">`client`: Client Profile</span></span>
- <span data-ttu-id="fcda2-148">`full`: Úplný profil</span><span class="sxs-lookup"><span data-stu-id="fcda2-148">`full`: Full Profile</span></span>
- <span data-ttu-id="fcda2-149">`wp`: Windows Phone</span><span class="sxs-lookup"><span data-stu-id="fcda2-149">`wp`: Windows Phone</span></span>
- <span data-ttu-id="fcda2-150">`cf`: Kompaktní rozhraní</span><span class="sxs-lookup"><span data-stu-id="fcda2-150">`cf`: Compact Framework</span></span>

## <a name="declaring-dependencies-advanced"></a><span data-ttu-id="fcda2-151">Deklarace závislostí (rozšířené)</span><span class="sxs-lookup"><span data-stu-id="fcda2-151">Declaring dependencies (Advanced)</span></span>

<span data-ttu-id="fcda2-152">Při balení souboru projektu se NuGet pokusí automaticky generovat závislosti z projektu.</span><span class="sxs-lookup"><span data-stu-id="fcda2-152">When packing a project file, NuGet tries to automatically generate the dependencies from the project.</span></span> <span data-ttu-id="fcda2-153">Informace v této části o použití souboru *. nuspec* k deklaraci závislostí jsou obvykle nezbytné jenom pro pokročilé scénáře.</span><span class="sxs-lookup"><span data-stu-id="fcda2-153">The information in this section about using a *.nuspec* file to declare dependencies is typically necessary for advanced scenarios only.</span></span>

<span data-ttu-id="fcda2-154">*(Verze 2.0 +)* Můžete deklarovat závislosti balíčků v *. nuspec* odpovídající cílové architektuře cílového projektu pomocí `<group>` prvků v rámci `<dependencies>` elementu.</span><span class="sxs-lookup"><span data-stu-id="fcda2-154">*(Version 2.0+)* You can declare package dependencies in the *.nuspec* corresponding to the target framework of the target project using `<group>` elements within the `<dependencies>` element.</span></span> <span data-ttu-id="fcda2-155">Další informace naleznete v tématu [závislosti elementu](../reference/nuspec.md#dependencies-element).</span><span class="sxs-lookup"><span data-stu-id="fcda2-155">For more information, see [dependencies element](../reference/nuspec.md#dependencies-element).</span></span>

<span data-ttu-id="fcda2-156">Každá skupina má atribut s názvem `targetFramework` a obsahuje nula nebo více `<dependency>` prvků.</span><span class="sxs-lookup"><span data-stu-id="fcda2-156">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="fcda2-157">Tyto závislosti jsou nainstalovány společně, pokud je cílový rámec kompatibilní s profilem rozhraní projektu.</span><span class="sxs-lookup"><span data-stu-id="fcda2-157">Those dependencies are installed together when the target framework is compatible with the project's framework profile.</span></span> <span data-ttu-id="fcda2-158">Přesné identifikátory rozhraní naleznete v tématu [cílová rozhraní](../reference/target-frameworks.md) .</span><span class="sxs-lookup"><span data-stu-id="fcda2-158">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

<span data-ttu-id="fcda2-159">Pro soubory v *lib/* a *ref/* Folders doporučujeme použít jednu skupinu na moniker (TFM).</span><span class="sxs-lookup"><span data-stu-id="fcda2-159">We recommend using one group per Target Framework Moniker (TFM) for files in the *lib/* and *ref/* folders.</span></span>

<span data-ttu-id="fcda2-160">Následující příklad ukazuje různé varianty `<group>` elementu:</span><span class="sxs-lookup"><span data-stu-id="fcda2-160">The following example shows different variations of the `<group>` element:</span></span>

```xml
<dependencies>

    <group targetFramework="net472">
        <dependency id="jQuery" version="1.10.2" />
        <dependency id="WebActivatorEx" version="2.2.0" />
    </group>

    <group targetFramework="net20">
    </group>

</dependencies>
```

## <a name="determining-which-nuget-target-to-use"></a><span data-ttu-id="fcda2-161">Určení, který cíl NuGet použít</span><span class="sxs-lookup"><span data-stu-id="fcda2-161">Determining which NuGet target to use</span></span>

<span data-ttu-id="fcda2-162">Při vytváření balíčků knihoven cílících na knihovnu přenosných tříd může být obtížné určit, který cíl NuGet byste měli použít ve svých názvech `.nuspec` a souborech složek, zejména pokud cílíte jenom na podmnožinu PCL.</span><span class="sxs-lookup"><span data-stu-id="fcda2-162">When packaging libraries targeting the Portable Class Library it can be tricky to determine which NuGet target you should use in your folder names and `.nuspec` file, especially if targeting only a subset of the PCL.</span></span> <span data-ttu-id="fcda2-163">Následující externí prostředky vám pomůžou s tímto:</span><span class="sxs-lookup"><span data-stu-id="fcda2-163">The following external resources will help you with this:</span></span>

- <span data-ttu-id="fcda2-164">[Profily architektury v .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephencleary.com)</span><span class="sxs-lookup"><span data-stu-id="fcda2-164">[Framework profiles in .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephencleary.com)</span></span>
- <span data-ttu-id="fcda2-165">[Přenositelné profily knihovny tříd](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Tabulka s výčtem profilů PCL a jejich ekvivalentních cílů NuGet</span><span class="sxs-lookup"><span data-stu-id="fcda2-165">[Portable Class Library profiles](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Table enumerating PCL profiles and their equivalent NuGet targets</span></span>
- <span data-ttu-id="fcda2-166">[Nástroj pro profily přenosných knihoven tříd](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): nástroj příkazového řádku pro určení profilů PCL dostupných v systému</span><span class="sxs-lookup"><span data-stu-id="fcda2-166">[Portable Class Library profiles tool](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): command line tool for determining PCL profiles available on your system</span></span>

## <a name="content-files-and-powershell-scripts"></a><span data-ttu-id="fcda2-167">Soubory obsahu a skripty PowerShellu</span><span class="sxs-lookup"><span data-stu-id="fcda2-167">Content files and PowerShell scripts</span></span>

> [!Warning]
> <span data-ttu-id="fcda2-168">Soubory s `packages.config` proměnlivým obsahem a provádění skriptu jsou k dispozici pouze ve formátu; jsou zastaralé pro všechny ostatní formáty a neměly by být použity pro žádné nové balíčky.</span><span class="sxs-lookup"><span data-stu-id="fcda2-168">Mutable content files and script execution are available with the `packages.config` format only; they are deprecated with all other formats and should not be used for any new packages.</span></span>

<span data-ttu-id="fcda2-169">Se `packages.config`soubory obsahu a skripty PowerShellu se dají seskupovat podle cílové architektury pomocí stejné konvence `content` složky ve složkách `tools` a.</span><span class="sxs-lookup"><span data-stu-id="fcda2-169">With `packages.config`, content files and PowerShell scripts can be grouped by target framework using the same folder convention inside the `content` and `tools` folders.</span></span> <span data-ttu-id="fcda2-170">Příklad:</span><span class="sxs-lookup"><span data-stu-id="fcda2-170">For example:</span></span>

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

<span data-ttu-id="fcda2-171">Pokud je složka rozhraní ponechána prázdná, NuGet nepřidá odkazy na sestavení ani soubory obsahu nebo spustí skripty prostředí PowerShell pro tuto architekturu.</span><span class="sxs-lookup"><span data-stu-id="fcda2-171">If a framework folder is left empty, NuGet doesn't add assembly references or content files or run the PowerShell scripts for that framework.</span></span>

> [!Note]
> <span data-ttu-id="fcda2-172">Vzhledem `init.ps1` k tomu, že je spuštěn na úrovni řešení a není závislý na projektu, je nutné jej umístit `tools` přímo do složky.</span><span class="sxs-lookup"><span data-stu-id="fcda2-172">Because `init.ps1` is executed at the solution level and not dependent on project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="fcda2-173">Ignoruje se, pokud je umístěn do složky rozhraní.</span><span class="sxs-lookup"><span data-stu-id="fcda2-173">It's ignored if placed under a framework folder.</span></span>
