---
title: Postup vytvoření balíčků NuGet – symbol
description: Jak vytvořit balíčky NuGet, které obsahují pouze symboly pro podporu ladění dalších balíčcích NuGet v sadě Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: cf8761ac4c994d864cd49a8fb31b3be626d4c0a6
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/28/2018
---
# <a name="creating-symbol-packages"></a><span data-ttu-id="092eb-103">Vytváření balíčků – symbol</span><span class="sxs-lookup"><span data-stu-id="092eb-103">Creating symbol packages</span></span>

<span data-ttu-id="092eb-104">Kromě vytváření balíčků pro nuget.org nebo jiné zdroje NuGet také podporuje vytváření související symbol balíčky a publikováním do SymbolSource úložiště.</span><span class="sxs-lookup"><span data-stu-id="092eb-104">In addition to building packages for nuget.org or other sources, NuGet also supports creating associated symbol packages and publishing them to the SymbolSource repository.</span></span>

<span data-ttu-id="092eb-105">Poté můžete přidat balíček příjemci `https://nuget.smbsrc.net` k jejich symbol zdroje v sadě Visual Studio, což umožňuje zanoříte se do balíčku kódu v ladicím programu sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="092eb-105">Package consumers can then add `https://nuget.smbsrc.net` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="092eb-106">V tématu [zadejte symbolu (.pdb) a zdrojových souborů v ladicím programu sady Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) podrobnosti o tomto procesu.</span><span class="sxs-lookup"><span data-stu-id="092eb-106">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="092eb-107">Vytváření balíčku – symbol</span><span class="sxs-lookup"><span data-stu-id="092eb-107">Creating a symbol package</span></span>

<span data-ttu-id="092eb-108">Chcete-li vytvořit balíček symbol, postupujte podle těchto konvence:</span><span class="sxs-lookup"><span data-stu-id="092eb-108">To create a symbol package, follow these conventions:</span></span>

- <span data-ttu-id="092eb-109">Název primární balíček (pomocí kódu) `{identifier}.nupkg` a zahrnují všechny soubory kromě `.pdb` soubory.</span><span class="sxs-lookup"><span data-stu-id="092eb-109">Name the primary package (with your code) `{identifier}.nupkg` and include all your files except `.pdb` files.</span></span>
- <span data-ttu-id="092eb-110">Zadejte název balíčku symbol `{identifier}.symbols.nupkg` a obsahovat vaše sestavení knihoven DLL, `.pdb` soubory, soubory XMLDOC, zdrojové soubory (viz následující části).</span><span class="sxs-lookup"><span data-stu-id="092eb-110">Name the symbol package `{identifier}.symbols.nupkg` and include your assembly DLL, `.pdb` files, XMLDOC files, source files (see the sections that follow).</span></span>

<span data-ttu-id="092eb-111">Můžete vytvořit oba balíčky s `-Symbols` možnosti, buď z `.nuspec` soubor nebo soubor projektu:</span><span class="sxs-lookup"><span data-stu-id="092eb-111">You can create both packages with the `-Symbols` option, either from a `.nuspec` file or a project file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

<span data-ttu-id="092eb-112">Všimněte si, že `pack` vyžaduje Mono 4.4.2 na Mac OS X a nefunguje v systémech Linux.</span><span class="sxs-lookup"><span data-stu-id="092eb-112">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="092eb-113">V systému Mac, je nutné také převést Windows názvy cest v `.nuspec` souboru do cesty formátu UNIX.</span><span class="sxs-lookup"><span data-stu-id="092eb-113">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="092eb-114">Struktura balíček – symbol</span><span class="sxs-lookup"><span data-stu-id="092eb-114">Symbol package structure</span></span>

<span data-ttu-id="092eb-115">Symbol balíček, můžete vybrat více cílové rozhraní stejným způsobem, který nemá balíček knihovny, proto struktura `lib` složky by mělo obsahovat přesně stejný jako primární balíček jen včetně `.pdb` soubory spolu s knihovnou DLL.</span><span class="sxs-lookup"><span data-stu-id="092eb-115">A symbol package can target multiple target frameworks in the same way that a library package does, so the structure of the `lib` folder should be exactly the same as the primary package, only including `.pdb` files alongside the DLL.</span></span>

<span data-ttu-id="092eb-116">Toto rozložení mít například symbol balíček, který cílí rozhraní .NET 4.0 a Silverlight 4:</span><span class="sxs-lookup"><span data-stu-id="092eb-116">For example, a symbol package that targets .NET 4.0 and Silverlight 4 would have this layout:</span></span>

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

<span data-ttu-id="092eb-117">Zdrojové soubory jsou pak umístit do samostatné speciální složky s názvem `src`, které musí následovat relativní strukturu zdrojové úložiště.</span><span class="sxs-lookup"><span data-stu-id="092eb-117">Source files are then placed in a separate special folder named `src`, which must follow the relative structure of your source repository.</span></span> <span data-ttu-id="092eb-118">Je to proto, že soubory PDB obsahovat absolutní cesty na zdrojové soubory, které používá ke kompilaci odpovídající DLL a potřebují k nalezen během procesu publikování.</span><span class="sxs-lookup"><span data-stu-id="092eb-118">This is because PDBs contain absolute paths to source files used to compile the matching DLL, and they need to be found during the publishing process.</span></span> <span data-ttu-id="092eb-119">Základní cesta (běžné cesta předponu) může být vynechají. Představte si třeba knihovnu sestaven z těchto souborů:</span><span class="sxs-lookup"><span data-stu-id="092eb-119">A base path (common path prefix) can be stripped out. For example, consider a library built from these files:</span></span>

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

<span data-ttu-id="092eb-120">Kromě `lib` složky balíčku symbol by bylo potřeba obsahovat toto rozložení:</span><span class="sxs-lookup"><span data-stu-id="092eb-120">Apart from the `lib` folder, a symbol package would need to contain this layout:</span></span>

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

## <a name="referring-to-files-in-the-nuspec"></a><span data-ttu-id="092eb-121">Odkazy na soubory v soubor nuspec</span><span class="sxs-lookup"><span data-stu-id="092eb-121">Referring to files in the nuspec</span></span>

<span data-ttu-id="092eb-122">Symbol balíčku se dají vytvářet konvencemi z struktury složek, jak je popsáno v předchozí části, nebo zadáním jeho obsah v `files` oddílu manifest.</span><span class="sxs-lookup"><span data-stu-id="092eb-122">A symbol package can be built by conventions, from a folder structure as described in the previous section, or by specifying its contents in the `files` section of the manifest.</span></span> <span data-ttu-id="092eb-123">Například pokud chcete vytvořit balíček uvedené v předchozí části, použít následující `.nuspec` souboru:</span><span class="sxs-lookup"><span data-stu-id="092eb-123">For example, to build the package shown in the previous section, use the following in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="092eb-124">Publikování balíčku – symbol</span><span class="sxs-lookup"><span data-stu-id="092eb-124">Publishing a symbol package</span></span>

> [!Important]
> <span data-ttu-id="092eb-125">K nabízení balíčků nuget.org je nutné použít [nuget.exe v4.1.0 nebo vyšší](https://www.nuget.org/downloads), který implementuje požadovaná [NuGet protokoly](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="092eb-125">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="092eb-126">Pro větší pohodlí si nejprve uložit klíč rozhraní API s NuGet (viz [publikování balíčku](../create-packages/publish-a-package.md), které bude platit pro nuget.org a symbolsource.org, protože symbolsource.org zkontroluje s nuget.org ověřit, zda jste vlastníkem balíčku.</span><span class="sxs-lookup"><span data-stu-id="092eb-126">For convenience, first save your API key with NuGet (see [publish a package](../create-packages/publish-a-package.md), which will apply to both nuget.org and symbolsource.org, because symbolsource.org will check with nuget.org to verify that you are the package owner.</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. <span data-ttu-id="092eb-127">Po publikování primární balíček nuget.org, push balíček symbol následujícím způsobem, které budou automaticky používat symbolsource.org jako cíl z důvodu `.symbols` v názvu souboru:</span><span class="sxs-lookup"><span data-stu-id="092eb-127">After publishing your primary package to nuget.org, push the symbol package as follows, which will automatically use symbolsource.org as the target because of the `.symbols` in the filename:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

   > [!Note]
   > <span data-ttu-id="092eb-128">S nuget.exe 4.5.0 nebo vyšší symboly balíčky nejsou automaticky instaluje do symbolsource.org. Potřebovali byste tak, aby nabízel balíčky symboly samostatně, jak je popsáno v dalším kroku.</span><span class="sxs-lookup"><span data-stu-id="092eb-128">With nuget.exe 4.5.0 or above, the symbols packages are not automatically pushed to symbolsource.org. You would need to push the symbols packages separately as explained in the next step.</span></span>

3. <span data-ttu-id="092eb-129">K publikování do různých symbol úložiště, nebo tak, aby nabízel symbol balíček, který není postupujte podle zásad vytváření názvů, použít `-Source` možnost:</span><span class="sxs-lookup"><span data-stu-id="092eb-129">To publish to a different symbol repository, or to push a symbol package that doesn't follow the naming convention, use the `-Source` option:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. <span data-ttu-id="092eb-130">Můžete také push obě primární a symbolů balíčky do obou úložiště ve stejnou dobu pomocí tohoto vzorce:</span><span class="sxs-lookup"><span data-stu-id="092eb-130">You can also push both primary and symbol packages to both repositories at the same time using the following:</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="092eb-131">V takovém případě bude publikovat NuGet `MyPackage.symbols.nupkg`, pokud je k dispozici na https://nuget.smbsrc.net/ (nabízené URL pro symbolsource.org), po jeho publikuje primární balíček do nuget.org.</span><span class="sxs-lookup"><span data-stu-id="092eb-131">In this case, NuGet will publish `MyPackage.symbols.nupkg`, if present, to https://nuget.smbsrc.net/ (the push URL for symbolsource.org), after it publishes the primary package to nuget.org.</span></span>

## <a name="see-also"></a><span data-ttu-id="092eb-132">Viz také</span><span class="sxs-lookup"><span data-stu-id="092eb-132">See Also</span></span>

<span data-ttu-id="092eb-133">[Přesun do nového modulu SymbolSource](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span><span class="sxs-lookup"><span data-stu-id="092eb-133">[Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span></span>
