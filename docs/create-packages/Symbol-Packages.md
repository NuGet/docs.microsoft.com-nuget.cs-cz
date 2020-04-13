---
title: Vytváření starších balíčků symbolů (.symbols.nupkg)
description: Jak vytvořit Balíčky NuGet, které obsahují pouze symboly pro podporu ladění jiných balíčků NuGet v sadě Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 374e9ccfc01cd06508e76529765db3f849342222
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "77476266"
---
# <a name="creating-legacy-symbol-packages-symbolsnupkg"></a><span data-ttu-id="e6f8a-103">Vytváření starších balíčků symbolů (.symbols.nupkg)</span><span class="sxs-lookup"><span data-stu-id="e6f8a-103">Creating legacy symbol packages (.symbols.nupkg)</span></span>

> [!Important]
> <span data-ttu-id="e6f8a-104">Nový doporučený formát pro balíčky symbolů je .snupkg.</span><span class="sxs-lookup"><span data-stu-id="e6f8a-104">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="e6f8a-105">Viz [Vytváření balíčků symbolů (.snupkg)](Symbol-Packages-snupkg.md).</span><span class="sxs-lookup"><span data-stu-id="e6f8a-105">See [Creating symbol packages (.snupkg)](Symbol-Packages-snupkg.md).</span></span> </br>
> <span data-ttu-id="e6f8a-106">.symbols.nupkg je stále podporován, ale pouze z důvodů kompatibility.</span><span class="sxs-lookup"><span data-stu-id="e6f8a-106">.symbols.nupkg is still supported but only for compatibility reasons.</span></span>

<span data-ttu-id="e6f8a-107">Kromě vytváření balíčků pro nuget.org nebo jiných zdrojů, NuGet také podporuje vytváření přidružené symbol balíčky, které mohou být publikovány na servery symbolů.</span><span class="sxs-lookup"><span data-stu-id="e6f8a-107">In addition to building packages for nuget.org or other sources, NuGet also supports creating associated symbol packages that can be published to symbol servers.</span></span> <span data-ttu-id="e6f8a-108">Formát balíčku starších symbolů,.symbols.nupkg, lze zasunout do úložiště SymbolSource.</span><span class="sxs-lookup"><span data-stu-id="e6f8a-108">The legacy symbol package format, .symbols.nupkg, can be pushed to the SymbolSource repository.</span></span>

<span data-ttu-id="e6f8a-109">Příjemci balíčků `https://nuget.smbsrc.net` pak můžete přidat do svých zdrojů symbolů v sadě Visual Studio, což umožňuje krokování do kódu balíčku v ladicím programu Sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e6f8a-109">Package consumers can then add `https://nuget.smbsrc.net` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="e6f8a-110">Podrobnosti o tomto [procesu naleznete v tématu Určení symbolu (.pdb) a zdrojových souborů v ladicím programu sady Visual Studio.](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger)</span><span class="sxs-lookup"><span data-stu-id="e6f8a-110">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

## <a name="creating-a-legacy-symbol-package"></a><span data-ttu-id="e6f8a-111">Vytvoření balíčku starších symbolů</span><span class="sxs-lookup"><span data-stu-id="e6f8a-111">Creating a legacy symbol package</span></span>

<span data-ttu-id="e6f8a-112">Chcete-li vytvořit balíček starších symbolů, postupujte podle těchto konvencí:</span><span class="sxs-lookup"><span data-stu-id="e6f8a-112">To create a legacy symbol package, follow these conventions:</span></span>

- <span data-ttu-id="e6f8a-113">Pojmenujte primární balíček `{identifier}.nupkg` (s kódem) `.pdb` a zahrňte všechny soubory kromě souborů.</span><span class="sxs-lookup"><span data-stu-id="e6f8a-113">Name the primary package (with your code) `{identifier}.nupkg` and include all your files except `.pdb` files.</span></span>
- <span data-ttu-id="e6f8a-114">Pojmenujte balíček starších `{identifier}.symbols.nupkg` symbolů `.pdb` a zahrňte knihovnu DLL sestavení, soubory, soubory XMLDOC, zdrojové soubory (viz následující části).</span><span class="sxs-lookup"><span data-stu-id="e6f8a-114">Name the legacy symbol package `{identifier}.symbols.nupkg` and include your assembly DLL, `.pdb` files, XMLDOC files, source files (see the sections that follow).</span></span>

<span data-ttu-id="e6f8a-115">Oba balíčky můžete `-Symbols` vytvořit s možností, a to buď ze souboru, `.nuspec` nebo ze souboru projektu:</span><span class="sxs-lookup"><span data-stu-id="e6f8a-115">You can create both packages with the `-Symbols` option, either from a `.nuspec` file or a project file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

<span data-ttu-id="e6f8a-116">Všimněte `pack` si, že vyžaduje Mono 4.4.2 na Mac OS X a nefunguje na systémech Linux.</span><span class="sxs-lookup"><span data-stu-id="e6f8a-116">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="e6f8a-117">Na Macu musíte také převést názvy cest Windows v souboru `.nuspec` na cesty ve stylu Unixu.</span><span class="sxs-lookup"><span data-stu-id="e6f8a-117">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="legacy-symbol-package-structure"></a><span data-ttu-id="e6f8a-118">Struktura balíčku starších symbolů</span><span class="sxs-lookup"><span data-stu-id="e6f8a-118">Legacy symbol package structure</span></span>

<span data-ttu-id="e6f8a-119">Balíček starších symbolů může cílit na více cílových architektur stejným `lib` způsobem jako balíček knihovny, takže `.pdb` struktura složky by měla být přesně stejná jako primární balíček, včetně souborů vedle knihovny DLL.</span><span class="sxs-lookup"><span data-stu-id="e6f8a-119">A legacy symbol package can target multiple target frameworks in the same way that a library package does, so the structure of the `lib` folder should be exactly the same as the primary package, only including `.pdb` files alongside the DLL.</span></span>

<span data-ttu-id="e6f8a-120">Například balíček starších symbolů, který cílí na rozhraní .NET 4.0 a Silverlight 4, by měl toto rozložení:</span><span class="sxs-lookup"><span data-stu-id="e6f8a-120">For example, a legacy symbol package that targets .NET 4.0 and Silverlight 4 would have this layout:</span></span>

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

<span data-ttu-id="e6f8a-121">Zdrojové soubory jsou pak umístěny `src`do samostatné speciální složky s názvem , která musí sledovat relativní strukturu zdrojového úložiště.</span><span class="sxs-lookup"><span data-stu-id="e6f8a-121">Source files are then placed in a separate special folder named `src`, which must follow the relative structure of your source repository.</span></span> <span data-ttu-id="e6f8a-122">Důvodem je, že pdbs obsahují absolutní cesty ke zdrojovým souborům používaným ke kompilaci odpovídající dll a je třeba je nalézt během procesu publikování.</span><span class="sxs-lookup"><span data-stu-id="e6f8a-122">This is because PDBs contain absolute paths to source files used to compile the matching DLL, and they need to be found during the publishing process.</span></span> <span data-ttu-id="e6f8a-123">Základní cestu (společnou předponu cesty) lze odebrat. Zvažte například knihovnu vytvořenou z těchto souborů:</span><span class="sxs-lookup"><span data-stu-id="e6f8a-123">A base path (common path prefix) can be stripped out. For example, consider a library built from these files:</span></span>

    C:\Projects
        \MyProject
            \Common
                \MyClass.cs
            \Full
                \Properties
                    \AssemblyInfo.cs
                \MyAssembly.csproj (producing \lib\net40\MyAssembly.dll)
            \Silverlight
                \Properties
                    \AssemblyInfo.cs
                \MySilverlightExtensions.cs
                \MyAssembly.csproj (producing \lib\sl4\MyAssembly.dll)

<span data-ttu-id="e6f8a-124">Kromě `lib` složky by balíček starších symbolů musel obsahovat toto rozložení:</span><span class="sxs-lookup"><span data-stu-id="e6f8a-124">Apart from the `lib` folder, a legacy symbol package would need to contain this layout:</span></span>

    \src
        \Common
            \MyClass.cs
        \Full
            \Properties
                \AssemblyInfo.cs
        \Silverlight
            \Properties
                \AssemblyInfo.cs
            \MySilverlightExtensions.cs

## <a name="referring-to-files-in-the-nuspec"></a><span data-ttu-id="e6f8a-125">Odkazující na soubory v nuspec</span><span class="sxs-lookup"><span data-stu-id="e6f8a-125">Referring to files in the nuspec</span></span>

<span data-ttu-id="e6f8a-126">Balíček starší symbol může být sestaven konvencemi, ze struktury složek, jak je popsáno `files` v předchozí části, nebo zadáním jeho obsahu v části manifestu.</span><span class="sxs-lookup"><span data-stu-id="e6f8a-126">A legacy symbol package can be built by conventions, from a folder structure as described in the previous section, or by specifying its contents in the `files` section of the manifest.</span></span> <span data-ttu-id="e6f8a-127">Chcete-li například vytvořit balíček zobrazený v předchozí `.nuspec` části, použijte v souboru následující:</span><span class="sxs-lookup"><span data-stu-id="e6f8a-127">For example, to build the package shown in the previous section, use the following in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-legacy-symbol-package"></a><span data-ttu-id="e6f8a-128">Publikování balíčku starších symbolů</span><span class="sxs-lookup"><span data-stu-id="e6f8a-128">Publishing a legacy symbol package</span></span>

> [!Important]
> <span data-ttu-id="e6f8a-129">Chcete-li vysunout balíčky nuget.org musíte použít [nuget.exe v4.9.1 nebo vyšší](https://www.nuget.org/downloads), který implementuje požadované [protokoly NuGet](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="e6f8a-129">To push packages to nuget.org you must use [nuget.exe v4.9.1 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="e6f8a-130">Pro větší pohodlí nejprve uložte klíč rozhraní API s NuGet (viz [publikování balíčku](../nuget-org/publish-a-package.md), který se bude vztahovat na nuget.org i symbolsource.org, protože symbolsource.org bude kontrolovat u nuget.org ověřit, zda jste vlastníkem balíčku.</span><span class="sxs-lookup"><span data-stu-id="e6f8a-130">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md), which will apply to both nuget.org and symbolsource.org, because symbolsource.org will check with nuget.org to verify that you are the package owner.</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. <span data-ttu-id="e6f8a-131">Po publikování primární balíček nuget.org, push starší symbol balíček takto, který bude `.symbols` automaticky používat symbolsource.org jako cíl z důvodu v názvu souboru:</span><span class="sxs-lookup"><span data-stu-id="e6f8a-131">After publishing your primary package to nuget.org, push the legacy symbol package as follows, which will automatically use symbolsource.org as the target because of the `.symbols` in the filename:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. <span data-ttu-id="e6f8a-132">Chcete-li publikovat do jiného úložiště symbolů nebo vysunout balíček starších symbolů, který nedodržuje konvence pojmenování, použijte `-Source` tuto možnost:</span><span class="sxs-lookup"><span data-stu-id="e6f8a-132">To publish to a different symbol repository, or to push a legacy symbol package that doesn't follow the naming convention, use the `-Source` option:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. <span data-ttu-id="e6f8a-133">Balíčky primárních i symbolů můžete také do obou úložišť současně tlačit pomocí následujících položek:</span><span class="sxs-lookup"><span data-stu-id="e6f8a-133">You can also push both primary and symbol packages to both repositories at the same time using the following:</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > <span data-ttu-id="e6f8a-134">U nuget.exe 4.5.0 nebo vyšší, symboly balíčky nejsou automaticky posunuty do symbolsource.org. Balíčky symbolů byste museli stlačovat samostatně, jak je vysvětleno v předchozích krocích.</span><span class="sxs-lookup"><span data-stu-id="e6f8a-134">With nuget.exe 4.5.0 or above, the symbols packages are not automatically pushed to symbolsource.org. You would need to push the symbols packages separately as explained in the earlier steps.</span></span>
   
<span data-ttu-id="e6f8a-135">V tomto případě NuGet `MyPackage.symbols.nupkg`publikuje , https://nuget.smbsrc.net/ pokud je k dispozici, do (nabízená adresa URL pro symbolsource.org) poté, co publikuje primární balíček nuget.org.</span><span class="sxs-lookup"><span data-stu-id="e6f8a-135">In this case, NuGet will publish `MyPackage.symbols.nupkg`, if present, to https://nuget.smbsrc.net/ (the push URL for symbolsource.org), after it publishes the primary package to nuget.org.</span></span>

## <a name="see-also"></a><span data-ttu-id="e6f8a-136">Viz také</span><span class="sxs-lookup"><span data-stu-id="e6f8a-136">See also</span></span>

* <span data-ttu-id="e6f8a-137">[Vytváření balíčků symbolů (.snupkg)](Symbol-Packages-snupkg.md) - Nový doporučený formát pro balíčky symbolů</span><span class="sxs-lookup"><span data-stu-id="e6f8a-137">[Creating symbol packages (.snupkg)](Symbol-Packages-snupkg.md) - The new recommended format for symbol packages</span></span>
* <span data-ttu-id="e6f8a-138">[Přechod na nový modul SymbolSource](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span><span class="sxs-lookup"><span data-stu-id="e6f8a-138">[Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span></span>
