---
title: "Postup vytvoření balíčků NuGet symbol | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 09/12/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Jak vytvořit balíčky NuGet, které obsahují pouze symboly pro podporu ladění dalších balíčcích NuGet v sadě Visual Studio."
keywords: "Symbol balíčky NuGet, balíček NuGet ladění, podpora ladění, balíček symboly, konvence symbol balíček NuGet"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: e25c34442861c36e9002120afc03cb39ea396f54
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
---
# <a name="creating-symbol-packages"></a><span data-ttu-id="639c0-104">Vytváření balíčků – symbol</span><span class="sxs-lookup"><span data-stu-id="639c0-104">Creating symbol packages</span></span>

<span data-ttu-id="639c0-105">Kromě vytváření balíčků pro nuget.org nebo jiné zdroje NuGet také podporuje vytváření balíčků přidružených symbol a jejich publikování [SymbolSource úložiště](http://www.symbolsource.org/Public).</span><span class="sxs-lookup"><span data-stu-id="639c0-105">In addition to building packages for nuget.org or other sources, NuGet also supports creating associated symbol packages and publishing them to the [SymbolSource repository](http://www.symbolsource.org/Public).</span></span>

<span data-ttu-id="639c0-106">Poté můžete přidat balíček příjemci `http://srv.symbolsource.org/pdb/Public` k jejich symbol zdroje v sadě Visual Studio, což umožňuje zanoříte se do balíčku kódu v ladicím programu sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="639c0-106">Package consumers can then add `http://srv.symbolsource.org/pdb/Public` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="639c0-107">V tématu [zadejte symbolu (.pdb) a zdrojových souborů v ladicím programu sady Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) podrobnosti o tomto procesu.</span><span class="sxs-lookup"><span data-stu-id="639c0-107">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="639c0-108">Vytváření balíčku – symbol</span><span class="sxs-lookup"><span data-stu-id="639c0-108">Creating a symbol package</span></span>

<span data-ttu-id="639c0-109">Chcete-li vytvořit balíček symbol, postupujte podle těchto konvence:</span><span class="sxs-lookup"><span data-stu-id="639c0-109">To create a symbol package, follow these conventions:</span></span>

- <span data-ttu-id="639c0-110">Název primární balíček (pomocí kódu) `{identifier}.nupkg` a zahrnují všechny soubory kromě `.pdb` soubory.</span><span class="sxs-lookup"><span data-stu-id="639c0-110">Name the primary package (with your code) `{identifier}.nupkg` and include all your files except `.pdb` files.</span></span>
- <span data-ttu-id="639c0-111">Zadejte název balíčku symbol `{identifier}.symbols.nupkg` a obsahovat vaše sestavení knihoven DLL, `.pdb` soubory, soubory XMLDOC, zdrojové soubory (viz následující části).</span><span class="sxs-lookup"><span data-stu-id="639c0-111">Name the symbol package `{identifier}.symbols.nupkg` and include your assembly DLL, `.pdb` files, XMLDOC files, source files (see the sections that follow).</span></span>

<span data-ttu-id="639c0-112">Můžete vytvořit oba balíčky s `-Symbols` možnosti, buď z `.nuspec` soubor nebo soubor projektu:</span><span class="sxs-lookup"><span data-stu-id="639c0-112">You can create both packages with the `-Symbols` option, either from a `.nuspec` file or a project file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

<span data-ttu-id="639c0-113">Všimněte si, že `pack` vyžaduje Mono 4.4.2 na Mac OS X a nefunguje v systémech Linux.</span><span class="sxs-lookup"><span data-stu-id="639c0-113">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="639c0-114">V systému Mac, je nutné také převést Windows názvy cest v `.nuspec` souboru do cesty formátu UNIX.</span><span class="sxs-lookup"><span data-stu-id="639c0-114">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="639c0-115">Struktura balíček – symbol</span><span class="sxs-lookup"><span data-stu-id="639c0-115">Symbol package structure</span></span>

<span data-ttu-id="639c0-116">Symbol balíček, můžete vybrat více cílové rozhraní stejným způsobem, který nemá balíček knihovny, proto struktura `lib` složky by mělo obsahovat přesně stejný jako primární balíček jen včetně `.pdb` soubory spolu s knihovnou DLL.</span><span class="sxs-lookup"><span data-stu-id="639c0-116">A symbol package can target multiple target frameworks in the same way that a library package does, so the structure of the `lib` folder should be exactly the same as the primary package, only including `.pdb` files alongside the DLL.</span></span>

<span data-ttu-id="639c0-117">Toto rozložení mít například symbol balíček, který cílí rozhraní .NET 4.0 a Silverlight 4:</span><span class="sxs-lookup"><span data-stu-id="639c0-117">For example, a symbol package that targets .NET 4.0 and Silverlight 4 would have this layout:</span></span>

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

<span data-ttu-id="639c0-118">Zdrojové soubory jsou pak umístit do samostatné speciální složky s názvem `src`, které musí následovat relativní strukturu zdrojové úložiště.</span><span class="sxs-lookup"><span data-stu-id="639c0-118">Source files are then placed in a separate special folder named `src`, which must follow the relative structure of your source repository.</span></span> <span data-ttu-id="639c0-119">Je to proto, že soubory PDB obsahovat absolutní cesty na zdrojové soubory, které používá ke kompilaci odpovídající DLL a potřebují k nalezen během procesu publikování.</span><span class="sxs-lookup"><span data-stu-id="639c0-119">This is because PDBs contain absolute paths to source files used to compile the matching DLL, and they need to be found during the publishing process.</span></span> <span data-ttu-id="639c0-120">Základní cesta (běžné cesta předponu) může být vynechají. Představte si třeba knihovnu sestaven z těchto souborů:</span><span class="sxs-lookup"><span data-stu-id="639c0-120">A base path (common path prefix) can be stripped out. For example, consider a library built from these files:</span></span>

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

<span data-ttu-id="639c0-121">Kromě `lib` složky balíčku symbol by bylo potřeba obsahovat toto rozložení:</span><span class="sxs-lookup"><span data-stu-id="639c0-121">Apart from the `lib` folder, a symbol package would need to contain this layout:</span></span>

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

## <a name="referring-to-files-in-the-nuspec"></a><span data-ttu-id="639c0-122">Odkazy na soubory v soubor nuspec</span><span class="sxs-lookup"><span data-stu-id="639c0-122">Referring to files in the nuspec</span></span>

<span data-ttu-id="639c0-123">Symbol balíčku se dají vytvářet konvencemi z struktury složek, jak je popsáno v předchozí části, nebo zadáním jeho obsah v `files` oddílu manifest.</span><span class="sxs-lookup"><span data-stu-id="639c0-123">A symbol package can be built by conventions, from a folder structure as described in the previous section, or by specifying its contents in the `files` section of the manifest.</span></span> <span data-ttu-id="639c0-124">Například pokud chcete vytvořit balíček uvedené v předchozí části, použít následující `.nuspec` souboru:</span><span class="sxs-lookup"><span data-stu-id="639c0-124">For example, to build the package shown in the previous section, use the following in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="639c0-125">Publikování balíčku – symbol</span><span class="sxs-lookup"><span data-stu-id="639c0-125">Publishing a symbol package</span></span>

> [!Important]
> <span data-ttu-id="639c0-126">K nabízení balíčků nuget.org je nutné použít [nuget.exe v4.1.0 nebo vyšší](https://www.nuget.org/downloads), který implementuje požadovaná [NuGet protokoly](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="639c0-126">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="639c0-127">Pro větší pohodlí si nejprve uložit klíč rozhraní API s NuGet (viz [publikování balíčku](../create-packages/publish-a-package.md), které bude platit pro nuget.org a symbolsource.org, protože symbolsource.org zkontroluje s nuget.org ověřit, zda jste vlastníkem balíčku.</span><span class="sxs-lookup"><span data-stu-id="639c0-127">For convenience, first save your API key with NuGet (see [publish a package](../create-packages/publish-a-package.md), which will apply to both nuget.org and symbolsource.org, because symbolsource.org will check with nuget.org to verify that you are the package owner.</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="639c0-128">Po publikování primární balíček nuget.org, push balíček symbol následujícím způsobem, které budou automaticky používat symbolsource.org jako cíl z důvodu `.symbols` v názvu souboru:</span><span class="sxs-lookup"><span data-stu-id="639c0-128">After publishing your primary package to nuget.org, push the symbol package as follows, which will automatically use symbolsource.org as the target because of the `.symbols` in the filename:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```
> [!Note]
> <span data-ttu-id="639c0-129">S nuget.exe 4.5.0 nebo vyšší symboly balíčky nejsou automaticky instaluje do symbolsource.org. Potřebovali byste tak, aby nabízel balíčky symboly samostatně, jak je popsáno v dalším kroku.</span><span class="sxs-lookup"><span data-stu-id="639c0-129">With nuget.exe 4.5.0 or above, the symbols packages are not automatically pushed to symbolsource.org. You would need to push the symbols packages separately as explained in the next step.</span></span>

1. <span data-ttu-id="639c0-130">K publikování do různých symbol úložiště, nebo tak, aby nabízel symbol balíček, který není postupujte podle zásad vytváření názvů, použít `-Source` možnost:</span><span class="sxs-lookup"><span data-stu-id="639c0-130">To publish to a different symbol repository, or to push a symbol package that doesn't follow the naming convention, use the `-Source` option:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

1. <span data-ttu-id="639c0-131">Můžete také push obě primární a symbolů balíčky do obou úložiště ve stejnou dobu pomocí tohoto vzorce:</span><span class="sxs-lookup"><span data-stu-id="639c0-131">You can also push both primary and symbol packages to both repositories at the same time using the following:</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="639c0-132">V takovém případě bude publikovat NuGet `MyPackage.symbols.nupkg`, pokud je k dispozici, k https://nuget.smbsrc.net/ (nabízené URL pro symbolsource.org), po jeho publikuje primární balíček do nuget.org.</span><span class="sxs-lookup"><span data-stu-id="639c0-132">In this case, NuGet will publish `MyPackage.symbols.nupkg`, if present, to https://nuget.smbsrc.net/ (the push URL for symbolsource.org), after it publishes the primary package to nuget.org.</span></span>

## <a name="see-also"></a><span data-ttu-id="639c0-133">Viz také</span><span class="sxs-lookup"><span data-stu-id="639c0-133">See Also</span></span>

<span data-ttu-id="639c0-134">[Pomocí SymbolSource](https://www.symbolsource.org/Public/Wiki/Using) (symbolsource.org)</span><span class="sxs-lookup"><span data-stu-id="639c0-134">[Using SymbolSource](https://www.symbolsource.org/Public/Wiki/Using) (symbolsource.org)</span></span>
