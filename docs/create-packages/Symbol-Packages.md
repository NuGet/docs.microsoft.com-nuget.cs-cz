---
title: Vytváření balíčků NuGet symbol
description: Jak vytvořit balíčky NuGet, které obsahují pouze symboly v zájmu podpory ladění jiných balíčků NuGet v sadě Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: e917895d0fa6ed6dc4bc24b72afc7fa0770f2dd0
ms.sourcegitcommit: 8e3546ab630a24cde8725610b6a68f8eb87afa47
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/05/2018
ms.locfileid: "37843365"
---
# <a name="creating-symbol-packages"></a><span data-ttu-id="87cf8-103">Vytváření balíčků symbolů</span><span class="sxs-lookup"><span data-stu-id="87cf8-103">Creating symbol packages</span></span>

<span data-ttu-id="87cf8-104">Kromě vytváření balíčků pro nuget.org nebo jiné zdroje NuGet také podporuje vytváření přidružené balíčky symbolů a publikujete je do úložiště SymbolSource.</span><span class="sxs-lookup"><span data-stu-id="87cf8-104">In addition to building packages for nuget.org or other sources, NuGet also supports creating associated symbol packages and publishing them to the SymbolSource repository.</span></span>

<span data-ttu-id="87cf8-105">Poté můžete přidat balíček příjemci `https://nuget.smbsrc.net` k jejich symbol zdroje v sadě Visual Studio, který umožňuje krokování s vnořením do kódu balíček v ladicím programu sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="87cf8-105">Package consumers can then add `https://nuget.smbsrc.net` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="87cf8-106">Zobrazit [zadání symbolu (.pdb) a zdrojových souborů v ladicím programu sady Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) podrobnosti o tomto procesu.</span><span class="sxs-lookup"><span data-stu-id="87cf8-106">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="87cf8-107">Vytváří se balíček symbolů</span><span class="sxs-lookup"><span data-stu-id="87cf8-107">Creating a symbol package</span></span>

<span data-ttu-id="87cf8-108">Vytvořte balíček symbolů, postupujte podle těchto konvence:</span><span class="sxs-lookup"><span data-stu-id="87cf8-108">To create a symbol package, follow these conventions:</span></span>

- <span data-ttu-id="87cf8-109">Zadejte název primárního balíčku (s vaším kódem) `{identifier}.nupkg` a zahrnout všechny soubory s výjimkou `.pdb` soubory.</span><span class="sxs-lookup"><span data-stu-id="87cf8-109">Name the primary package (with your code) `{identifier}.nupkg` and include all your files except `.pdb` files.</span></span>
- <span data-ttu-id="87cf8-110">Zadejte název balíčku symbolů `{identifier}.symbols.nupkg` a zahrnout sestavení knihovny DLL, `.pdb` soubory, soubory XMLDOC, zdrojové soubory (viz následující části).</span><span class="sxs-lookup"><span data-stu-id="87cf8-110">Name the symbol package `{identifier}.symbols.nupkg` and include your assembly DLL, `.pdb` files, XMLDOC files, source files (see the sections that follow).</span></span>

<span data-ttu-id="87cf8-111">Můžete vytvořit oba balíčky s `-Symbols` možnosti, buď z `.nuspec` soubor nebo soubor projektu:</span><span class="sxs-lookup"><span data-stu-id="87cf8-111">You can create both packages with the `-Symbols` option, either from a `.nuspec` file or a project file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

<span data-ttu-id="87cf8-112">Všimněte si, že `pack` vyžaduje Mono 4.4.2 v Mac OS X a nebude fungovat v systémech Linux.</span><span class="sxs-lookup"><span data-stu-id="87cf8-112">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="87cf8-113">Na počítači Mac, je také nutné převést Windows cest v `.nuspec` soubor do cesty k systému UNIX.</span><span class="sxs-lookup"><span data-stu-id="87cf8-113">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="87cf8-114">Struktura balíčku symbolů</span><span class="sxs-lookup"><span data-stu-id="87cf8-114">Symbol package structure</span></span>

<span data-ttu-id="87cf8-115">Balíček symbolů můžete cílit na více cílových platforem stejným způsobem, který nemá balíček knihovny, proto struktury `lib` složka by měla být přesně stejný jako primární balíček jen včetně `.pdb` soubory společně s knihovny DLL.</span><span class="sxs-lookup"><span data-stu-id="87cf8-115">A symbol package can target multiple target frameworks in the same way that a library package does, so the structure of the `lib` folder should be exactly the same as the primary package, only including `.pdb` files alongside the DLL.</span></span>

<span data-ttu-id="87cf8-116">Toto rozložení mít například balíček symbolů, který cílí na rozhraní .NET 4.0 a Silverlight 4:</span><span class="sxs-lookup"><span data-stu-id="87cf8-116">For example, a symbol package that targets .NET 4.0 and Silverlight 4 would have this layout:</span></span>

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

<span data-ttu-id="87cf8-117">Zdrojové soubory jsou pak umístěné v samostatné speciální složky s názvem `src`, které musí následovat relativní struktury zdrojového úložiště.</span><span class="sxs-lookup"><span data-stu-id="87cf8-117">Source files are then placed in a separate special folder named `src`, which must follow the relative structure of your source repository.</span></span> <span data-ttu-id="87cf8-118">Je to proto, že soubory PDB obsahovat absolutní cesty ke zdrojovým souborům používá ke kompilaci odpovídající knihovny DLL, a potřebují najít během procesu publikování.</span><span class="sxs-lookup"><span data-stu-id="87cf8-118">This is because PDBs contain absolute paths to source files used to compile the matching DLL, and they need to be found during the publishing process.</span></span> <span data-ttu-id="87cf8-119">Základní cesta (běžnou předponu cesty) může být vynechají. Představte si třeba knihovnu sestaven z těchto souborů:</span><span class="sxs-lookup"><span data-stu-id="87cf8-119">A base path (common path prefix) can be stripped out. For example, consider a library built from these files:</span></span>

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

<span data-ttu-id="87cf8-120">Kromě `lib` složce balíček symbolů by bylo potřeba obsahovat toto rozložení:</span><span class="sxs-lookup"><span data-stu-id="87cf8-120">Apart from the `lib` folder, a symbol package would need to contain this layout:</span></span>

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

## <a name="referring-to-files-in-the-nuspec"></a><span data-ttu-id="87cf8-121">Odkazování na soubory v souboru nuspec</span><span class="sxs-lookup"><span data-stu-id="87cf8-121">Referring to files in the nuspec</span></span>

<span data-ttu-id="87cf8-122">Balíček symbolů se dají podle konvence z strukturu složek, jak je popsáno v předchozí části, nebo tak, že zadáte jeho obsah `files` manifestu.</span><span class="sxs-lookup"><span data-stu-id="87cf8-122">A symbol package can be built by conventions, from a folder structure as described in the previous section, or by specifying its contents in the `files` section of the manifest.</span></span> <span data-ttu-id="87cf8-123">Například provést sestavení balíčku je znázorněno v předchozí části, pomocí následujících postupů v `.nuspec` souboru:</span><span class="sxs-lookup"><span data-stu-id="87cf8-123">For example, to build the package shown in the previous section, use the following in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="87cf8-124">Publikování balíčku symbolů</span><span class="sxs-lookup"><span data-stu-id="87cf8-124">Publishing a symbol package</span></span>

> [!Important]
> <span data-ttu-id="87cf8-125">Push balíčků na nuget.org je nutné použít [nuget.exe verze 4.1.0 nebo vyšší](https://www.nuget.org/downloads), který implementuje požadované [NuGet protokoly](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="87cf8-125">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="87cf8-126">Pro usnadnění práce, uložte svůj klíč rozhraní API s NuGet (viz [publikování balíčku](../create-packages/publish-a-package.md), které bude platit na webech nuget.org a symbolsource.org, protože symbolsource.org zkontroluje s nuget.org a ověřte, zda jste vlastníkem balíčku.</span><span class="sxs-lookup"><span data-stu-id="87cf8-126">For convenience, first save your API key with NuGet (see [publish a package](../create-packages/publish-a-package.md), which will apply to both nuget.org and symbolsource.org, because symbolsource.org will check with nuget.org to verify that you are the package owner.</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. <span data-ttu-id="87cf8-127">Po publikování primární balíčků na nuget.org, push balíček symbolů následujícím způsobem, které budou automaticky používat symbolsource.org jako cíl z důvodu `.symbols` v názvu souboru:</span><span class="sxs-lookup"><span data-stu-id="87cf8-127">After publishing your primary package to nuget.org, push the symbol package as follows, which will automatically use symbolsource.org as the target because of the `.symbols` in the filename:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. <span data-ttu-id="87cf8-128">Chcete publikovat do úložiště symbolů různých, nebo tak, aby nabízel symbol balíček, který není postupujte z zásady vytváření názvů, použijte `-Source` možnost:</span><span class="sxs-lookup"><span data-stu-id="87cf8-128">To publish to a different symbol repository, or to push a symbol package that doesn't follow the naming convention, use the `-Source` option:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. <span data-ttu-id="87cf8-129">Můžete také vložit obě primární a symbol balíčky do obou úložišť ve stejnou dobu následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="87cf8-129">You can also push both primary and symbol packages to both repositories at the same time using the following:</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > <span data-ttu-id="87cf8-130">S nuget.exe 4.5.0 nebo vyšší, symboly balíčky nejsou automaticky nahrány do symbolsource.org. Je třeba tak, aby nabízel balíčky symboly samostatně, jak je vysvětleno v dalším kroku.</span><span class="sxs-lookup"><span data-stu-id="87cf8-130">With nuget.exe 4.5.0 or above, the symbols packages are not automatically pushed to symbolsource.org. You would need to push the symbols packages separately as explained in the next step.</span></span>
   
<span data-ttu-id="87cf8-131">V takovém případě budete publikovat NuGet `MyPackage.symbols.nupkg`, pokud jsou k dispozici na https://nuget.smbsrc.net/ (URL nabízených oznámení pro symbolsource.org), po publikuje primární balíčků na nuget.org.</span><span class="sxs-lookup"><span data-stu-id="87cf8-131">In this case, NuGet will publish `MyPackage.symbols.nupkg`, if present, to https://nuget.smbsrc.net/ (the push URL for symbolsource.org), after it publishes the primary package to nuget.org.</span></span>

## <a name="see-also"></a><span data-ttu-id="87cf8-132">Viz také</span><span class="sxs-lookup"><span data-stu-id="87cf8-132">See Also</span></span>

<span data-ttu-id="87cf8-133">[Přechod na nový stroj SymbolSource](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span><span class="sxs-lookup"><span data-stu-id="87cf8-133">[Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span></span>
