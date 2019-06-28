---
title: Vytváření balíčků NuGet symbol
description: Jak vytvořit balíčky NuGet, které obsahují pouze symboly v zájmu podpory ladění jiných balíčků NuGet v sadě Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 40f934f3c3fcea62acae66639c22108a93363b8b
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426770"
---
# <a name="creating-symbol-packages-legacy"></a><span data-ttu-id="98e15-103">Vytváření balíčků symbolů (starší verze)</span><span class="sxs-lookup"><span data-stu-id="98e15-103">Creating symbol packages (legacy)</span></span>

> [!Important]
> <span data-ttu-id="98e15-104">Nové doporučený formát pro balíčky symbolů je .snupkg.</span><span class="sxs-lookup"><span data-stu-id="98e15-104">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="98e15-105">Zobrazit [vytváření balíčků symbolů (.snupkg)](Symbol-Packages-snupkg.md).</span><span class="sxs-lookup"><span data-stu-id="98e15-105">See [Creating symbol packages (.snupkg)](Symbol-Packages-snupkg.md).</span></span> </br>
> <span data-ttu-id="98e15-106">. symbols.nupkg je stále podporovány, ale pouze z důvodu kompatibility.</span><span class="sxs-lookup"><span data-stu-id="98e15-106">.symbols.nupkg is still supported but only for compatibility reasons.</span></span>

<span data-ttu-id="98e15-107">Kromě vytváření balíčků pro nuget.org nebo jiné zdroje NuGet také podporuje vytváření přidružené balíčky symbolů a publikujete je do úložiště SymbolSource.</span><span class="sxs-lookup"><span data-stu-id="98e15-107">In addition to building packages for nuget.org or other sources, NuGet also supports creating associated symbol packages and publishing them to the SymbolSource repository.</span></span>

<span data-ttu-id="98e15-108">Poté můžete přidat balíček příjemci `https://nuget.smbsrc.net` k jejich symbol zdroje v sadě Visual Studio, který umožňuje krokování s vnořením do kódu balíček v ladicím programu sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="98e15-108">Package consumers can then add `https://nuget.smbsrc.net` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="98e15-109">Zobrazit [zadání symbolu (.pdb) a zdrojových souborů v ladicím programu sady Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) podrobnosti o tomto procesu.</span><span class="sxs-lookup"><span data-stu-id="98e15-109">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="98e15-110">Vytváří se balíček symbolů</span><span class="sxs-lookup"><span data-stu-id="98e15-110">Creating a symbol package</span></span>

<span data-ttu-id="98e15-111">Vytvořte balíček symbolů, postupujte podle těchto konvence:</span><span class="sxs-lookup"><span data-stu-id="98e15-111">To create a symbol package, follow these conventions:</span></span>

- <span data-ttu-id="98e15-112">Zadejte název primárního balíčku (s vaším kódem) `{identifier}.nupkg` a zahrnout všechny soubory s výjimkou `.pdb` soubory.</span><span class="sxs-lookup"><span data-stu-id="98e15-112">Name the primary package (with your code) `{identifier}.nupkg` and include all your files except `.pdb` files.</span></span>
- <span data-ttu-id="98e15-113">Zadejte název balíčku symbolů `{identifier}.symbols.nupkg` a zahrnout sestavení knihovny DLL, `.pdb` soubory, soubory XMLDOC, zdrojové soubory (viz následující části).</span><span class="sxs-lookup"><span data-stu-id="98e15-113">Name the symbol package `{identifier}.symbols.nupkg` and include your assembly DLL, `.pdb` files, XMLDOC files, source files (see the sections that follow).</span></span>

<span data-ttu-id="98e15-114">Můžete vytvořit oba balíčky s `-Symbols` možnosti, buď z `.nuspec` soubor nebo soubor projektu:</span><span class="sxs-lookup"><span data-stu-id="98e15-114">You can create both packages with the `-Symbols` option, either from a `.nuspec` file or a project file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

<span data-ttu-id="98e15-115">Všimněte si, že `pack` vyžaduje Mono 4.4.2 v Mac OS X a nebude fungovat v systémech Linux.</span><span class="sxs-lookup"><span data-stu-id="98e15-115">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="98e15-116">Na počítači Mac, je také nutné převést Windows cest v `.nuspec` soubor do cesty k systému UNIX.</span><span class="sxs-lookup"><span data-stu-id="98e15-116">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="98e15-117">Struktura balíčku symbolů</span><span class="sxs-lookup"><span data-stu-id="98e15-117">Symbol package structure</span></span>

<span data-ttu-id="98e15-118">Balíček symbolů můžete cílit na více cílových platforem stejným způsobem, který nemá balíček knihovny, proto struktury `lib` složka by měla být přesně stejný jako primární balíček jen včetně `.pdb` soubory společně s knihovny DLL.</span><span class="sxs-lookup"><span data-stu-id="98e15-118">A symbol package can target multiple target frameworks in the same way that a library package does, so the structure of the `lib` folder should be exactly the same as the primary package, only including `.pdb` files alongside the DLL.</span></span>

<span data-ttu-id="98e15-119">Toto rozložení mít například balíček symbolů, který cílí na rozhraní .NET 4.0 a Silverlight 4:</span><span class="sxs-lookup"><span data-stu-id="98e15-119">For example, a symbol package that targets .NET 4.0 and Silverlight 4 would have this layout:</span></span>

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

<span data-ttu-id="98e15-120">Zdrojové soubory jsou pak umístěné v samostatné speciální složky s názvem `src`, které musí následovat relativní struktury zdrojového úložiště.</span><span class="sxs-lookup"><span data-stu-id="98e15-120">Source files are then placed in a separate special folder named `src`, which must follow the relative structure of your source repository.</span></span> <span data-ttu-id="98e15-121">Je to proto, že soubory PDB obsahovat absolutní cesty ke zdrojovým souborům používá ke kompilaci odpovídající knihovny DLL, a potřebují najít během procesu publikování.</span><span class="sxs-lookup"><span data-stu-id="98e15-121">This is because PDBs contain absolute paths to source files used to compile the matching DLL, and they need to be found during the publishing process.</span></span> <span data-ttu-id="98e15-122">Základní cesta (běžnou předponu cesty) může být vynechají. Představte si třeba knihovnu sestaven z těchto souborů:</span><span class="sxs-lookup"><span data-stu-id="98e15-122">A base path (common path prefix) can be stripped out. For example, consider a library built from these files:</span></span>

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

<span data-ttu-id="98e15-123">Kromě `lib` složce balíček symbolů by bylo potřeba obsahovat toto rozložení:</span><span class="sxs-lookup"><span data-stu-id="98e15-123">Apart from the `lib` folder, a symbol package would need to contain this layout:</span></span>

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

## <a name="referring-to-files-in-the-nuspec"></a><span data-ttu-id="98e15-124">Odkazování na soubory v souboru nuspec</span><span class="sxs-lookup"><span data-stu-id="98e15-124">Referring to files in the nuspec</span></span>

<span data-ttu-id="98e15-125">Balíček symbolů se dají podle konvence z strukturu složek, jak je popsáno v předchozí části, nebo tak, že zadáte jeho obsah `files` manifestu.</span><span class="sxs-lookup"><span data-stu-id="98e15-125">A symbol package can be built by conventions, from a folder structure as described in the previous section, or by specifying its contents in the `files` section of the manifest.</span></span> <span data-ttu-id="98e15-126">Například provést sestavení balíčku je znázorněno v předchozí části, pomocí následujících postupů v `.nuspec` souboru:</span><span class="sxs-lookup"><span data-stu-id="98e15-126">For example, to build the package shown in the previous section, use the following in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="98e15-127">Publikování balíčku symbolů</span><span class="sxs-lookup"><span data-stu-id="98e15-127">Publishing a symbol package</span></span>

> [!Important]
> <span data-ttu-id="98e15-128">Push balíčků na nuget.org je nutné použít [nuget.exe v4.9.1 nebo vyšší](https://www.nuget.org/downloads), který implementuje požadované [NuGet protokoly](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="98e15-128">To push packages to nuget.org you must use [nuget.exe v4.9.1 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="98e15-129">Pro usnadnění práce, uložte svůj klíč rozhraní API s NuGet (viz [publikování balíčku](../nuget-org/publish-a-package.md), které bude platit na webech nuget.org a symbolsource.org, protože symbolsource.org zkontroluje s nuget.org a ověřte, zda jste vlastníkem balíčku.</span><span class="sxs-lookup"><span data-stu-id="98e15-129">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md), which will apply to both nuget.org and symbolsource.org, because symbolsource.org will check with nuget.org to verify that you are the package owner.</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. <span data-ttu-id="98e15-130">Po publikování primární balíčků na nuget.org, push balíček symbolů následujícím způsobem, které budou automaticky používat symbolsource.org jako cíl z důvodu `.symbols` v názvu souboru:</span><span class="sxs-lookup"><span data-stu-id="98e15-130">After publishing your primary package to nuget.org, push the symbol package as follows, which will automatically use symbolsource.org as the target because of the `.symbols` in the filename:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. <span data-ttu-id="98e15-131">Chcete publikovat do úložiště symbolů různých, nebo tak, aby nabízel symbol balíček, který není postupujte z zásady vytváření názvů, použijte `-Source` možnost:</span><span class="sxs-lookup"><span data-stu-id="98e15-131">To publish to a different symbol repository, or to push a symbol package that doesn't follow the naming convention, use the `-Source` option:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. <span data-ttu-id="98e15-132">Můžete také vložit obě primární a symbol balíčky do obou úložišť ve stejnou dobu následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="98e15-132">You can also push both primary and symbol packages to both repositories at the same time using the following:</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > <span data-ttu-id="98e15-133">S nuget.exe 4.5.0 nebo vyšší, symboly balíčky nejsou automaticky nahrány do symbolsource.org. Je třeba tak, aby nabízel balíčky symboly samostatně, jak je vysvětleno v dalším kroku.</span><span class="sxs-lookup"><span data-stu-id="98e15-133">With nuget.exe 4.5.0 or above, the symbols packages are not automatically pushed to symbolsource.org. You would need to push the symbols packages separately as explained in the next step.</span></span>
   
<span data-ttu-id="98e15-134">V takovém případě budete publikovat NuGet `MyPackage.symbols.nupkg`, pokud jsou k dispozici na https://nuget.smbsrc.net/ (URL nabízených oznámení pro symbolsource.org), po publikuje primární balíčků na nuget.org.</span><span class="sxs-lookup"><span data-stu-id="98e15-134">In this case, NuGet will publish `MyPackage.symbols.nupkg`, if present, to https://nuget.smbsrc.net/ (the push URL for symbolsource.org), after it publishes the primary package to nuget.org.</span></span>

## <a name="see-also"></a><span data-ttu-id="98e15-135">Viz také</span><span class="sxs-lookup"><span data-stu-id="98e15-135">See Also</span></span>

<span data-ttu-id="98e15-136">[Přechod na nový stroj SymbolSource](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span><span class="sxs-lookup"><span data-stu-id="98e15-136">[Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span></span>
