---
title: Vytváření starších balíčků symbolů (. Symbols. nupkg)
description: Vytvoření balíčků NuGet, které obsahují pouze symboly pro podporu ladění dalších balíčků NuGet v aplikaci Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 374e9ccfc01cd06508e76529765db3f849342222
ms.sourcegitcommit: 1799d4ac23c8aacee7498fdc72c40dd1646d267b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/20/2020
ms.locfileid: "77476266"
---
# <a name="creating-legacy-symbol-packages-symbolsnupkg"></a><span data-ttu-id="9739b-103">Vytváření starších balíčků symbolů (. Symbols. nupkg)</span><span class="sxs-lookup"><span data-stu-id="9739b-103">Creating legacy symbol packages (.symbols.nupkg)</span></span>

> [!Important]
> <span data-ttu-id="9739b-104">Nový doporučený formát pro balíčky symbolů je. snupkg.</span><span class="sxs-lookup"><span data-stu-id="9739b-104">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="9739b-105">Viz [vytváření balíčků symbolů (. snupkg)](Symbol-Packages-snupkg.md).</span><span class="sxs-lookup"><span data-stu-id="9739b-105">See [Creating symbol packages (.snupkg)](Symbol-Packages-snupkg.md).</span></span> </br>
> <span data-ttu-id="9739b-106">. Symbols. nupkg je stále podporován, ale pouze z důvodu kompatibility.</span><span class="sxs-lookup"><span data-stu-id="9739b-106">.symbols.nupkg is still supported but only for compatibility reasons.</span></span>

<span data-ttu-id="9739b-107">Kromě vytváření balíčků pro nuget.org nebo jiných zdrojů NuGet podporuje také vytváření přidružených balíčků symbolů, které mohou být publikovány na servery symbolů.</span><span class="sxs-lookup"><span data-stu-id="9739b-107">In addition to building packages for nuget.org or other sources, NuGet also supports creating associated symbol packages that can be published to symbol servers.</span></span> <span data-ttu-id="9739b-108">Formát balíčku symbolů starší verze,. Symbols. nupkg, lze vložit do úložiště SymbolSource.</span><span class="sxs-lookup"><span data-stu-id="9739b-108">The legacy symbol package format, .symbols.nupkg, can be pushed to the SymbolSource repository.</span></span>

<span data-ttu-id="9739b-109">Příjemci balíčku pak mohou přidat `https://nuget.smbsrc.net` do svých zdrojů symbolů v aplikaci Visual Studio, které umožňují krokování kódu balíčku v ladicím programu sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9739b-109">Package consumers can then add `https://nuget.smbsrc.net` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="9739b-110">Podrobnosti o tomto procesu najdete v tématu [určení symbolu (PDB) a zdrojových souborů v ladicím programu sady Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) .</span><span class="sxs-lookup"><span data-stu-id="9739b-110">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

## <a name="creating-a-legacy-symbol-package"></a><span data-ttu-id="9739b-111">Vytváření starší verze balíčku symbolů</span><span class="sxs-lookup"><span data-stu-id="9739b-111">Creating a legacy symbol package</span></span>

<span data-ttu-id="9739b-112">Chcete-li vytvořit starší verzi balíčku symbolů, postupujte podle těchto konvencí:</span><span class="sxs-lookup"><span data-stu-id="9739b-112">To create a legacy symbol package, follow these conventions:</span></span>

- <span data-ttu-id="9739b-113">Pojmenujte primární balíček (s kódem) `{identifier}.nupkg` a zahrňte všechny soubory s výjimkou souborů `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="9739b-113">Name the primary package (with your code) `{identifier}.nupkg` and include all your files except `.pdb` files.</span></span>
- <span data-ttu-id="9739b-114">Zadejte název starší verze balíčku symbolů `{identifier}.symbols.nupkg` a do souboru DLL sestavení, soubory `.pdb`, soubory XMLDOC a zdrojové soubory (viz následující části).</span><span class="sxs-lookup"><span data-stu-id="9739b-114">Name the legacy symbol package `{identifier}.symbols.nupkg` and include your assembly DLL, `.pdb` files, XMLDOC files, source files (see the sections that follow).</span></span>

<span data-ttu-id="9739b-115">Oba balíčky lze vytvořit pomocí možnosti `-Symbols`, buď ze souboru `.nuspec` nebo souboru projektu:</span><span class="sxs-lookup"><span data-stu-id="9739b-115">You can create both packages with the `-Symbols` option, either from a `.nuspec` file or a project file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

<span data-ttu-id="9739b-116">Všimněte si, že `pack` vyžaduje mono 4.4.2 v Mac OS X a nefunguje v systémech Linux.</span><span class="sxs-lookup"><span data-stu-id="9739b-116">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="9739b-117">V počítači Mac je nutné také převést cesty systému Windows v souboru `.nuspec` na cesty ve stylu systému UNIX.</span><span class="sxs-lookup"><span data-stu-id="9739b-117">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="legacy-symbol-package-structure"></a><span data-ttu-id="9739b-118">Struktura balíčku symbolů starší verze</span><span class="sxs-lookup"><span data-stu-id="9739b-118">Legacy symbol package structure</span></span>

<span data-ttu-id="9739b-119">Balíček starší verze se může zaměřit na více cílových rozhraní stejným způsobem jako balíček knihovny, takže struktura `lib` složky by měla být přesně stejná jako primární balíček, včetně souborů `.pdb` společně s knihovnou DLL.</span><span class="sxs-lookup"><span data-stu-id="9739b-119">A legacy symbol package can target multiple target frameworks in the same way that a library package does, so the structure of the `lib` folder should be exactly the same as the primary package, only including `.pdb` files alongside the DLL.</span></span>

<span data-ttu-id="9739b-120">Například starší balíček symbolů, který cílí na rozhraní .NET 4,0 a Silverlight 4, by měl toto rozložení:</span><span class="sxs-lookup"><span data-stu-id="9739b-120">For example, a legacy symbol package that targets .NET 4.0 and Silverlight 4 would have this layout:</span></span>

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

<span data-ttu-id="9739b-121">Zdrojové soubory se pak umístí do samostatné speciální složky s názvem `src`, která musí následovat po relativní struktuře zdrojového úložiště.</span><span class="sxs-lookup"><span data-stu-id="9739b-121">Source files are then placed in a separate special folder named `src`, which must follow the relative structure of your source repository.</span></span> <span data-ttu-id="9739b-122">Důvodem je, že soubory PDB obsahuje absolutní cesty ke zdrojovým souborům používaným ke kompilaci vyhovující knihovny DLL a musí být nalezeny během procesu publikování.</span><span class="sxs-lookup"><span data-stu-id="9739b-122">This is because PDBs contain absolute paths to source files used to compile the matching DLL, and they need to be found during the publishing process.</span></span> <span data-ttu-id="9739b-123">Základní cestu (předpona společné cesty) lze odložit. Zvažte například knihovnu vytvořenou z těchto souborů:</span><span class="sxs-lookup"><span data-stu-id="9739b-123">A base path (common path prefix) can be stripped out. For example, consider a library built from these files:</span></span>

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

<span data-ttu-id="9739b-124">Kromě `lib` složky by měl starší balíček symbolů obsahovat toto rozložení:</span><span class="sxs-lookup"><span data-stu-id="9739b-124">Apart from the `lib` folder, a legacy symbol package would need to contain this layout:</span></span>

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

## <a name="referring-to-files-in-the-nuspec"></a><span data-ttu-id="9739b-125">Odkazy na soubory v nuspec</span><span class="sxs-lookup"><span data-stu-id="9739b-125">Referring to files in the nuspec</span></span>

<span data-ttu-id="9739b-126">Starší verze balíčku symbolů lze vytvořit podle konvencí, ze struktury složek, jak je popsáno v předchozí části, nebo zadáním jejího obsahu v části `files` manifestu.</span><span class="sxs-lookup"><span data-stu-id="9739b-126">A legacy symbol package can be built by conventions, from a folder structure as described in the previous section, or by specifying its contents in the `files` section of the manifest.</span></span> <span data-ttu-id="9739b-127">Chcete-li například sestavit balíček uvedený v předchozí části, použijte následující příkaz v souboru `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="9739b-127">For example, to build the package shown in the previous section, use the following in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-legacy-symbol-package"></a><span data-ttu-id="9739b-128">Publikování staršího balíčku symbolů</span><span class="sxs-lookup"><span data-stu-id="9739b-128">Publishing a legacy symbol package</span></span>

> [!Important]
> <span data-ttu-id="9739b-129">Pokud chcete nabízet balíčky do nuget.org, musíte použít [NuGet. exe v 4.9.1 nebo vyšší](https://www.nuget.org/downloads), který implementuje požadované [protokoly NuGet](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="9739b-129">To push packages to nuget.org you must use [nuget.exe v4.9.1 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="9739b-130">Pro usnadnění práce nejdřív uložte klíč rozhraní API pomocí NuGet (viz [publikování balíčku](../nuget-org/publish-a-package.md), který bude platit jak pro NuGet.org, tak pro symbolsource.org, protože symbolsource.org se ověří pomocí NuGet.org a ověří, že jste vlastníkem balíčku.</span><span class="sxs-lookup"><span data-stu-id="9739b-130">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md), which will apply to both nuget.org and symbolsource.org, because symbolsource.org will check with nuget.org to verify that you are the package owner.</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. <span data-ttu-id="9739b-131">Po publikování primárního balíčku do nuget.org nahrajte starší verzi balíčku symbolů následujícím způsobem, který automaticky použije symbolsource.org jako cíl z důvodu `.symbols` v názvu souboru:</span><span class="sxs-lookup"><span data-stu-id="9739b-131">After publishing your primary package to nuget.org, push the legacy symbol package as follows, which will automatically use symbolsource.org as the target because of the `.symbols` in the filename:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. <span data-ttu-id="9739b-132">Chcete-li publikovat do jiného úložiště symbolů nebo odeslat starší balíček symbolů, který nedodržuje zásady vytváření názvů, použijte možnost `-Source`:</span><span class="sxs-lookup"><span data-stu-id="9739b-132">To publish to a different symbol repository, or to push a legacy symbol package that doesn't follow the naming convention, use the `-Source` option:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. <span data-ttu-id="9739b-133">Současně můžete do obou úložišť současně nabízet i balíčky s primárním i symbolem, a to pomocí následujících:</span><span class="sxs-lookup"><span data-stu-id="9739b-133">You can also push both primary and symbol packages to both repositories at the same time using the following:</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > <span data-ttu-id="9739b-134">Pomocí nástroje NuGet. exe 4.5.0 nebo vyšší nejsou balíčky symbolů automaticky vloženy do symbolsource.org. Balíčky symbolů byste museli nabízet samostatně, jak je vysvětleno v předchozích krocích.</span><span class="sxs-lookup"><span data-stu-id="9739b-134">With nuget.exe 4.5.0 or above, the symbols packages are not automatically pushed to symbolsource.org. You would need to push the symbols packages separately as explained in the earlier steps.</span></span>
   
<span data-ttu-id="9739b-135">V tomto případě bude NuGet publikovat `MyPackage.symbols.nupkg`, pokud je k dispozici, aby https://nuget.smbsrc.net/ (adresa URL pro nabízení oznámení pro symbolsource.org) po publikování primárního balíčku do nuget.org.</span><span class="sxs-lookup"><span data-stu-id="9739b-135">In this case, NuGet will publish `MyPackage.symbols.nupkg`, if present, to https://nuget.smbsrc.net/ (the push URL for symbolsource.org), after it publishes the primary package to nuget.org.</span></span>

## <a name="see-also"></a><span data-ttu-id="9739b-136">Viz také</span><span class="sxs-lookup"><span data-stu-id="9739b-136">See also</span></span>

* <span data-ttu-id="9739b-137">[Vytváření balíčků symbolů (. snupkg)](Symbol-Packages-snupkg.md) – nový doporučený formát pro balíčky symbolů</span><span class="sxs-lookup"><span data-stu-id="9739b-137">[Creating symbol packages (.snupkg)](Symbol-Packages-snupkg.md) - The new recommended format for symbol packages</span></span>
* <span data-ttu-id="9739b-138">[Přechod na nový modul SymbolSource](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span><span class="sxs-lookup"><span data-stu-id="9739b-138">[Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span></span>
