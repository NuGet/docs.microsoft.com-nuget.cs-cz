---
title: Vícenásobné cílení pro balíčky NuGet
description: Popis různých metod, které mají cílit na více verzí rozhraní .NET Framework z jednoho balíčku NuGet.
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: 34f7c6132ba6050e20114642932ccf29a5ec088d
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "79429008"
---
# <a name="support-multiple-net-versions"></a><span data-ttu-id="cee9b-103">Podpora více verzí rozhraní .NET</span><span class="sxs-lookup"><span data-stu-id="cee9b-103">Support multiple .NET versions</span></span>

<span data-ttu-id="cee9b-104">Mnoho knihoven cílí na konkrétní verzi rozhraní .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="cee9b-104">Many libraries target a specific version of the .NET Framework.</span></span> <span data-ttu-id="cee9b-105">Můžete mít například jednu verzi knihovny, která je specifická pro UPW, a jinou verzi, která využívá výhod funkcí v rozhraní .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="cee9b-105">For example, you might have one version of your library that's specific to UWP, and another version that takes advantage of features in .NET Framework 4.6.</span></span> <span data-ttu-id="cee9b-106">Chcete-li přizpůsobit toto, NuGet podporuje uvedení více verzí stejné knihovny v jednom balíčku.</span><span class="sxs-lookup"><span data-stu-id="cee9b-106">To accommodate this, NuGet supports putting multiple versions of the same library in a single package.</span></span>

<span data-ttu-id="cee9b-107">Tento článek popisuje rozložení balíčku NuGet, bez ohledu na to, jak jsou vytvořeny balíček nebo sestavení (to znamená, že rozložení je stejné, ať už pomocí více souborů *csproj* ve stylu s dsad a vlastní soubor *.nuspec* nebo jeden víceúčelový *soubor SDK .csproj*).</span><span class="sxs-lookup"><span data-stu-id="cee9b-107">This article describes the layout of a NuGet package, regardless of how the package or assemblies are built (that is, the layout is the same whether using multiple non-SDK-style *.csproj* files and a custom *.nuspec* file, or a single multi-targeted SDK-style *.csproj*).</span></span> <span data-ttu-id="cee9b-108">Pro projekt ve stylu Sady SDK cíle sady NuGet [pack](../reference/msbuild-targets.md) ví, jak musí být balíček rozložen a automatizuje umístění sestavení do správných složek lib a vytváření skupin závislostí pro každý cílový rámec (TFM).</span><span class="sxs-lookup"><span data-stu-id="cee9b-108">For an SDK-style project, NuGet [pack targets](../reference/msbuild-targets.md) knows how the package must be layed out and automates putting the assemblies in the correct lib folders and creating dependency groups for each target framework (TFM).</span></span> <span data-ttu-id="cee9b-109">Podrobné pokyny naleznete v [tématu Podpora více verzí rozhraní .NET Framework v souboru projektu](multiple-target-frameworks-project-file.md).</span><span class="sxs-lookup"><span data-stu-id="cee9b-109">For detailed instructions, see [Support multiple .NET Framework versions in your project file](multiple-target-frameworks-project-file.md).</span></span>

<span data-ttu-id="cee9b-110">Při použití metody pracovního adresáře založené na konvencích popsané v [článku Vytvoření balíčku](../create-packages/creating-a-package.md#from-a-convention-based-working-directory)je nutné ručně rozložit balíček.</span><span class="sxs-lookup"><span data-stu-id="cee9b-110">You must manually lay out the package as described in this article when using the convention-based working directory method described in [Creating a package](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> <span data-ttu-id="cee9b-111">Pro projekt ve stylu sady SDK je doporučena automatizovaná metoda, ale můžete také ručně rozložit balíček, jak je popsáno v tomto článku.</span><span class="sxs-lookup"><span data-stu-id="cee9b-111">For an SDK-style project, the automated method is recommended, but you may also choose to manually lay out the package as described in this article.</span></span>

## <a name="framework-version-folder-structure"></a><span data-ttu-id="cee9b-112">Struktura složek verzí architektury</span><span class="sxs-lookup"><span data-stu-id="cee9b-112">Framework version folder structure</span></span>

<span data-ttu-id="cee9b-113">Při vytváření balíčku, který obsahuje pouze jednu verzi knihovny nebo cíl `lib` více architektur, vždy vytvořit podsložky pod pomocí různých názvů rozhraní rozlišující malá a velká písmena s následující konvencí:</span><span class="sxs-lookup"><span data-stu-id="cee9b-113">When building a package that contains only one version of a library or target multiple frameworks, you always make subfolders under `lib` using different case-sensitive framework names with the following convention:</span></span>

    lib\{framework name}[{version}]

<span data-ttu-id="cee9b-114">Úplný seznam podporovaných názvů naleznete v [odkazu Cílové architektury](../reference/target-frameworks.md#supported-frameworks).</span><span class="sxs-lookup"><span data-stu-id="cee9b-114">For a complete list of supported names, see the [Target Frameworks reference](../reference/target-frameworks.md#supported-frameworks).</span></span>

<span data-ttu-id="cee9b-115">Nikdy byste neměli mít verzi knihovny, která není specifická `lib` pro rozhraní a umístěna přímo do kořenové složky.</span><span class="sxs-lookup"><span data-stu-id="cee9b-115">You should never have a version of the library that is not specific to a framework and placed directly in the root `lib` folder.</span></span> <span data-ttu-id="cee9b-116">(Tato funkce byla `packages.config`podporována pouze s ).</span><span class="sxs-lookup"><span data-stu-id="cee9b-116">(This capability was supported only with `packages.config`).</span></span> <span data-ttu-id="cee9b-117">Pokud by bylo možné knihovnu kompatibilní s libovolným cílovým rozhraním a umožnit její instalaci kdekoli, což by pravděpodobně vedlo k neočekávaným chybám za běhu.</span><span class="sxs-lookup"><span data-stu-id="cee9b-117">Doing so would make the library compatible with any target framework and allow it to be installed anywhere, likely resulting in unexpected runtime errors.</span></span> <span data-ttu-id="cee9b-118">Přidání sestavení do kořenové složky (například) `lib\abc.dll` `lib\abc\abc.dll`nebo podsložek (například ) bylo zastaralé a při použití formátu PackagesReference je ignorováno.</span><span class="sxs-lookup"><span data-stu-id="cee9b-118">Adding assemblies in the root folder (such as `lib\abc.dll`) or subfolders (such as `lib\abc\abc.dll`) has been deprecated and is ignored when using the PackagesReference format.</span></span>

<span data-ttu-id="cee9b-119">Například následující struktura složek podporuje čtyři verze sestavení, které jsou specifické pro architekturu:</span><span class="sxs-lookup"><span data-stu-id="cee9b-119">For example, the following folder structure supports four versions of an assembly that are framework-specific:</span></span>

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

<span data-ttu-id="cee9b-120">Chcete-li při vytváření balíčku snadno zahrnout všechny tyto `**` soubory, `<files>` použijte v `.nuspec`části :</span><span class="sxs-lookup"><span data-stu-id="cee9b-120">To easily include all these files when building the package, use a recursive `**` wildcard in the `<files>` section of your `.nuspec`:</span></span>

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a><span data-ttu-id="cee9b-121">Složky specifické pro architekturu</span><span class="sxs-lookup"><span data-stu-id="cee9b-121">Architecture-specific folders</span></span>

<span data-ttu-id="cee9b-122">Pokud máte sestavení specifická pro architekturu, to znamená samostatná sestavení, která cílí na ARM, x86 a x64, musíte je umístit do složky s názvem `runtimes` v podsložkách s názvem `{platform}-{architecture}\lib\{framework}` nebo `{platform}-{architecture}\native`.</span><span class="sxs-lookup"><span data-stu-id="cee9b-122">If you have architecture-specific assemblies, that is, separate assemblies that target ARM, x86, and x64, you must place them in a folder named `runtimes` within sub-folders named `{platform}-{architecture}\lib\{framework}` or `{platform}-{architecture}\native`.</span></span> <span data-ttu-id="cee9b-123">Například následující struktura složek by vyhovovala nativním i spravovaným knihovnám DLL zaměřeným na systém Windows 10 a `uap10.0` rámci:</span><span class="sxs-lookup"><span data-stu-id="cee9b-123">For example, the following folder structure would accommodate both native and managed DLLs targeting Windows 10 and the `uap10.0` framework:</span></span>

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

<span data-ttu-id="cee9b-124">Tato sestavení budou k dispozici pouze za běhu, takže pokud chcete poskytnout odpovídající `AnyCPU` sestavení `/ref/{tfm}` čas kompilace také pak mít sestavení ve složce.</span><span class="sxs-lookup"><span data-stu-id="cee9b-124">These assemblies will only be available at runtime, so if you want to provide the corresponding compile time assembly as well then have `AnyCPU` assembly in `/ref/{tfm}` folder.</span></span> 

<span data-ttu-id="cee9b-125">Upozorňujeme, nuget vždy vybere tyto kompilovat nebo runtime prostředky z `/ref` `/lib` jedné složky, takže pokud existují některé kompatibilní prostředky z té doby budou ignorovány přidat sestavení v době kompilace.</span><span class="sxs-lookup"><span data-stu-id="cee9b-125">Please note, NuGet always picks these compile or runtime assets from one folder so if there are some compatible assets from `/ref` then `/lib` will be ignored to add compile-time assemblies.</span></span> <span data-ttu-id="cee9b-126">Podobně, pokud existují některé kompatibilní `/runtimes` prostředky `/lib` z pak také budou ignorovány pro běh.</span><span class="sxs-lookup"><span data-stu-id="cee9b-126">Similarly, if there are some compatible assets from `/runtimes` then also `/lib` will be ignored for runtime.</span></span>

<span data-ttu-id="cee9b-127">Viz [Vytvoření balíčků UPW](../guides/create-uwp-packages.md) pro příklad odkazování `.nuspec` na tyto soubory v manifestu.</span><span class="sxs-lookup"><span data-stu-id="cee9b-127">See [Create UWP Packages](../guides/create-uwp-packages.md) for an example of referencing these files in the `.nuspec` manifest.</span></span>

<span data-ttu-id="cee9b-128">Taky si přečtěte [část Balení součásti aplikace pro Windows Store pomocí NuGetu.](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2)</span><span class="sxs-lookup"><span data-stu-id="cee9b-128">Also, see [Packing a Windows store app component with NuGet](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2)</span></span>

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a><span data-ttu-id="cee9b-129">Odpovídající verze sestavení a cílové rozhraní v projektu</span><span class="sxs-lookup"><span data-stu-id="cee9b-129">Matching assembly versions and the target framework in a project</span></span>

<span data-ttu-id="cee9b-130">Když NuGet nainstaluje balíček, který má více verzí sestavení, pokusí se shodovat název rámce sestavení s cílovým rámcem projektu.</span><span class="sxs-lookup"><span data-stu-id="cee9b-130">When NuGet installs a package that has multiple assembly versions, it tries to match the framework name of the assembly with the target framework of the project.</span></span>

<span data-ttu-id="cee9b-131">Pokud není nalezena shoda, NuGet zkopíruje sestavení pro nejvyšší verzi, která je menší nebo rovna cílové rozhraní projektu, pokud je k dispozici.</span><span class="sxs-lookup"><span data-stu-id="cee9b-131">If a match is not found, NuGet copies the assembly for the highest version that is less than or equal to the project's target framework, if available.</span></span> <span data-ttu-id="cee9b-132">Pokud není nalezeno žádné kompatibilní sestavení, NuGet vrátí příslušnou chybovou zprávu.</span><span class="sxs-lookup"><span data-stu-id="cee9b-132">If no compatible assembly is found, NuGet returns an appropriate error message.</span></span>

<span data-ttu-id="cee9b-133">Zvažte například následující strukturu složek v balíčku:</span><span class="sxs-lookup"><span data-stu-id="cee9b-133">For example, consider the following folder structure in a package:</span></span>

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

<span data-ttu-id="cee9b-134">Při instalaci tohoto balíčku v projektu, který se zaměřuje na rozhraní .NET Framework 4.6, NuGet nainstaluje sestavení ve `net45` složce, protože to je nejvyšší dostupná verze, která je menší nebo rovna 4.6.</span><span class="sxs-lookup"><span data-stu-id="cee9b-134">When installing this package in a project that targets .NET Framework 4.6, NuGet installs the assembly in the `net45` folder, because that's the highest available version that's less than or equal to 4.6.</span></span>

<span data-ttu-id="cee9b-135">Pokud projekt cíle .NET Framework 4.6.1, na druhé straně NuGet `net461` nainstaluje sestavení ve složce.</span><span class="sxs-lookup"><span data-stu-id="cee9b-135">If the project targets .NET Framework 4.6.1, on the other hand, NuGet installs the assembly in the `net461` folder.</span></span>

<span data-ttu-id="cee9b-136">Pokud se projekt zaměřuje na rozhraní .NET Framework 4.0 a starší, NuGet vyvolá příslušnou chybovou zprávu pro nenalezení kompatibilního sestavení.</span><span class="sxs-lookup"><span data-stu-id="cee9b-136">If the project targets .NET framework 4.0 and earlier, NuGet throws an appropriate error message for not finding the compatible assembly.</span></span>

## <a name="grouping-assemblies-by-framework-version"></a><span data-ttu-id="cee9b-137">Seskupení sestavení podle verze architektury</span><span class="sxs-lookup"><span data-stu-id="cee9b-137">Grouping assemblies by framework version</span></span>

<span data-ttu-id="cee9b-138">NuGet zkopíruje sestavení pouze z jedné složky knihovny v balíčku.</span><span class="sxs-lookup"><span data-stu-id="cee9b-138">NuGet copies assemblies from only a single library folder in the package.</span></span> <span data-ttu-id="cee9b-139">Předpokládejme například, že balíček má následující strukturu složek:</span><span class="sxs-lookup"><span data-stu-id="cee9b-139">For example, suppose a package has the following folder structure:</span></span>

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

<span data-ttu-id="cee9b-140">Při instalaci balíčku v projektu, který se zaměřuje `MyAssembly.dll` na rozhraní .NET Framework 4.5 (v2.0) je pouze nainstalované sestavení.</span><span class="sxs-lookup"><span data-stu-id="cee9b-140">When the package is installed in a project that targets .NET Framework 4.5, `MyAssembly.dll` (v2.0) is the only assembly installed.</span></span> <span data-ttu-id="cee9b-141">`MyAssembly.Core.dll`(v1.0) není nainstalován, protože není uveden `net45` ve složce.</span><span class="sxs-lookup"><span data-stu-id="cee9b-141">`MyAssembly.Core.dll` (v1.0) is not installed because it's not listed in the `net45` folder.</span></span> <span data-ttu-id="cee9b-142">NuGet se chová tímto způsobem, protože `MyAssembly.Core.dll` pravděpodobně `MyAssembly.dll`byly sloučeny do verze 2.0 .</span><span class="sxs-lookup"><span data-stu-id="cee9b-142">NuGet behaves this way because `MyAssembly.Core.dll` might have merged into version 2.0 of `MyAssembly.dll`.</span></span>

<span data-ttu-id="cee9b-143">Pokud chcete `MyAssembly.Core.dll` být nainstalovánpro rozhraní .NET Framework 4.5, umístěte kopii do `net45` složky.</span><span class="sxs-lookup"><span data-stu-id="cee9b-143">If you want `MyAssembly.Core.dll` to be installed for .NET Framework 4.5, place a copy in the `net45` folder.</span></span>

## <a name="grouping-assemblies-by-framework-profile"></a><span data-ttu-id="cee9b-144">Seskupení sestavení podle profilu rámce</span><span class="sxs-lookup"><span data-stu-id="cee9b-144">Grouping assemblies by framework profile</span></span>

<span data-ttu-id="cee9b-145">NuGet také podporuje cílení na konkrétní profil architektury připojením pomlčka a název profilu na konec složky.</span><span class="sxs-lookup"><span data-stu-id="cee9b-145">NuGet also supports targeting a specific framework profile by appending a dash and the profile name to the end of the folder.</span></span>

    lib\{framework name}-{profile}

<span data-ttu-id="cee9b-146">Podporované profily jsou následující:</span><span class="sxs-lookup"><span data-stu-id="cee9b-146">The supported profiles are as follows:</span></span>

- <span data-ttu-id="cee9b-147">`client`: Profil klienta</span><span class="sxs-lookup"><span data-stu-id="cee9b-147">`client`: Client Profile</span></span>
- <span data-ttu-id="cee9b-148">`full`: Úplný profil</span><span class="sxs-lookup"><span data-stu-id="cee9b-148">`full`: Full Profile</span></span>
- <span data-ttu-id="cee9b-149">`wp`: Windows Phone</span><span class="sxs-lookup"><span data-stu-id="cee9b-149">`wp`: Windows Phone</span></span>
- <span data-ttu-id="cee9b-150">`cf`: Kompaktní rámec</span><span class="sxs-lookup"><span data-stu-id="cee9b-150">`cf`: Compact Framework</span></span>

## <a name="declaring-dependencies-advanced"></a><span data-ttu-id="cee9b-151">Deklarování závislostí (Upřesnit)</span><span class="sxs-lookup"><span data-stu-id="cee9b-151">Declaring dependencies (Advanced)</span></span>

<span data-ttu-id="cee9b-152">Při balení souboru projektu NuGet pokusí automaticky generovat závislosti z projektu.</span><span class="sxs-lookup"><span data-stu-id="cee9b-152">When packing a project file, NuGet tries to automatically generate the dependencies from the project.</span></span> <span data-ttu-id="cee9b-153">Informace v této části o použití souboru *.nuspec* k deklarování závislostí jsou obvykle nezbytné pouze pro pokročilé scénáře.</span><span class="sxs-lookup"><span data-stu-id="cee9b-153">The information in this section about using a *.nuspec* file to declare dependencies is typically necessary for advanced scenarios only.</span></span>

<span data-ttu-id="cee9b-154">*(verze 2.0+)* Můžete deklarovat závislosti balíčku v *.nuspec* odpovídající cílovému `<group>` rámci `<dependencies>` cílového projektu pomocí prvků v rámci prvku.</span><span class="sxs-lookup"><span data-stu-id="cee9b-154">*(Version 2.0+)* You can declare package dependencies in the *.nuspec* corresponding to the target framework of the target project using `<group>` elements within the `<dependencies>` element.</span></span> <span data-ttu-id="cee9b-155">Další informace naleznete v tématu [element závislosti .](../reference/nuspec.md#dependencies-element)</span><span class="sxs-lookup"><span data-stu-id="cee9b-155">For more information, see [dependencies element](../reference/nuspec.md#dependencies-element).</span></span>

<span data-ttu-id="cee9b-156">Každá skupina má `targetFramework` atribut s názvem `<dependency>` a obsahuje nula nebo více prvků.</span><span class="sxs-lookup"><span data-stu-id="cee9b-156">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="cee9b-157">Tyto závislosti jsou nainstalovány společně, když je cílový rámec kompatibilní s profilem architektury projektu.</span><span class="sxs-lookup"><span data-stu-id="cee9b-157">Those dependencies are installed together when the target framework is compatible with the project's framework profile.</span></span> <span data-ttu-id="cee9b-158">Viz [Cílové architektury](../reference/target-frameworks.md) pro přesné identifikátory rozhraní.</span><span class="sxs-lookup"><span data-stu-id="cee9b-158">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

<span data-ttu-id="cee9b-159">Doporučujeme použít jednu skupinu na cílový rámec zástupný název (TFM) pro soubory v *lib/* a *ref/* složky.</span><span class="sxs-lookup"><span data-stu-id="cee9b-159">We recommend using one group per Target Framework Moniker (TFM) for files in the *lib/* and *ref/* folders.</span></span>

<span data-ttu-id="cee9b-160">Následující příklad ukazuje různé varianty `<group>` prvku:</span><span class="sxs-lookup"><span data-stu-id="cee9b-160">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="determining-which-nuget-target-to-use"></a><span data-ttu-id="cee9b-161">Určení, který cíl NuGet použít</span><span class="sxs-lookup"><span data-stu-id="cee9b-161">Determining which NuGet target to use</span></span>

<span data-ttu-id="cee9b-162">Při balení knihoven zaměřených na knihovnu přenosných tříd může být obtížné určit, který cíl NuGet byste měli použít v názvech a `.nuspec` souboru složek, zejména pokud cílíte pouze na podmnožinu pcl.</span><span class="sxs-lookup"><span data-stu-id="cee9b-162">When packaging libraries targeting the Portable Class Library it can be tricky to determine which NuGet target you should use in your folder names and `.nuspec` file, especially if targeting only a subset of the PCL.</span></span> <span data-ttu-id="cee9b-163">S tím vám pomohou následující externí zdroje:</span><span class="sxs-lookup"><span data-stu-id="cee9b-163">The following external resources will help you with this:</span></span>

- <span data-ttu-id="cee9b-164">[Profily architektury v rozhraní .NET](https://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephencleary.com)</span><span class="sxs-lookup"><span data-stu-id="cee9b-164">[Framework profiles in .NET](https://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephencleary.com)</span></span>
- <span data-ttu-id="cee9b-165">[Profily knihovny přenosných tříd](https://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Tabulka s výčetem profilů PCL a jejich ekvivalentních cílů NuGet</span><span class="sxs-lookup"><span data-stu-id="cee9b-165">[Portable Class Library profiles](https://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Table enumerating PCL profiles and their equivalent NuGet targets</span></span>
- <span data-ttu-id="cee9b-166">[Nástroj profily knihovny přenosných tříd](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): nástroj příkazového řádku pro určení profilů PCL dostupných ve vašem systému</span><span class="sxs-lookup"><span data-stu-id="cee9b-166">[Portable Class Library profiles tool](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): command line tool for determining PCL profiles available on your system</span></span>

## <a name="content-files-and-powershell-scripts"></a><span data-ttu-id="cee9b-167">Soubory obsahu a skripty prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="cee9b-167">Content files and PowerShell scripts</span></span>

> [!Warning]
> <span data-ttu-id="cee9b-168">Mutable soubory obsahu a spuštění `packages.config` skriptu jsou k dispozici pouze ve formátu; jsou zastaralé se všemi ostatními formáty a neměly by být používány pro žádné nové balíčky.</span><span class="sxs-lookup"><span data-stu-id="cee9b-168">Mutable content files and script execution are available with the `packages.config` format only; they are deprecated with all other formats and should not be used for any new packages.</span></span>

<span data-ttu-id="cee9b-169">Pomocí `packages.config`souborů obsahu a skriptů prostředí PowerShell lze seskupit `content` `tools` podle cílového rozhraní pomocí stejné konvence složek uvnitř složek a.</span><span class="sxs-lookup"><span data-stu-id="cee9b-169">With `packages.config`, content files and PowerShell scripts can be grouped by target framework using the same folder convention inside the `content` and `tools` folders.</span></span> <span data-ttu-id="cee9b-170">Příklad:</span><span class="sxs-lookup"><span data-stu-id="cee9b-170">For example:</span></span>

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

<span data-ttu-id="cee9b-171">Pokud je složka architektury ponechána prázdná, NuGet nepřidá odkazy na sestavení nebo soubory obsahu ani nespustí skripty prostředí PowerShell pro tento rámec.</span><span class="sxs-lookup"><span data-stu-id="cee9b-171">If a framework folder is left empty, NuGet doesn't add assembly references or content files or run the PowerShell scripts for that framework.</span></span>

> [!Note]
> <span data-ttu-id="cee9b-172">Protože `init.ps1` je spuštěn na úrovni řešení a není závislá na projektu, musí být umístěnpřímo do `tools` složky.</span><span class="sxs-lookup"><span data-stu-id="cee9b-172">Because `init.ps1` is executed at the solution level and not dependent on project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="cee9b-173">Je ignorována, pokud je umístěna pod rámcovou složkou.</span><span class="sxs-lookup"><span data-stu-id="cee9b-173">It's ignored if placed under a framework folder.</span></span>
