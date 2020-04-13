---
title: Jak publikovat balíčky symbolů NuGet pomocí nového formátu balíčku symbolů '.snupkg'| Dokumenty společnosti Microsoft
author: cristinamanu
ms.author: cristinamanu
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Jak vytvořit balíčky symbolů NuGet (snupkg).
keywords: Balíčky symbolů NuGet, ladění balíčku NuGet, podpora ladění NuGet, symboly balíčků balíčků, konvence balíčků symbolů
ms.reviewer:
- anangaur
- karann
ms.openlocfilehash: c42032f1869f4be0af44ffa8fbd5ad522f73c459
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "80380415"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="792e4-104">Vytváření balíčků symbolů (.snupkg)</span><span class="sxs-lookup"><span data-stu-id="792e4-104">Creating symbol packages (.snupkg)</span></span>

<span data-ttu-id="792e4-105">Dobré ladění prostředí závisí na přítomnost ladicí symboly, protože poskytují důležité informace, jako je přidružení mezi zkompilované a zdrojový kód, názvy místních proměnných, trasování zásobníku a další.</span><span class="sxs-lookup"><span data-stu-id="792e4-105">A good debugging experience relies on the presence of debug symbols as they provide critical information like the association between the compiled and the source code, names of local variables, stack traces, and more.</span></span> <span data-ttu-id="792e4-106">Balíčky symbolů (.snupkg) můžete distribuovat tyto symboly a zlepšit ladění prostředí balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="792e4-106">You can use symbol packages (.snupkg) to distribute these symbols and improve the debugging experience of your NuGet packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="792e4-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="792e4-107">Prerequisites</span></span>

<span data-ttu-id="792e4-108">[nuget.exe v4.9.0 nebo vyšší](https://www.nuget.org/downloads) nebo [dotnet CLI v2.2.0 nebo vyšší](https://www.microsoft.com/net/download/dotnet-core/2.2), které implementují požadované [protokoly NuGet](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="792e4-108">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet CLI v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="792e4-109">Vytvoření balíčku symbolů</span><span class="sxs-lookup"><span data-stu-id="792e4-109">Creating a symbol package</span></span>

<span data-ttu-id="792e4-110">Pokud používáte dotnet CLI nebo MSBuild, je `IncludeSymbols` `SymbolPackageFormat` třeba nastavit vlastnosti a k vytvoření souboru .snupkg kromě souboru .nupkg.</span><span class="sxs-lookup"><span data-stu-id="792e4-110">If you're using dotnet CLI or MSBuild, you need to set the `IncludeSymbols` and `SymbolPackageFormat` properties to create a .snupkg file in addition to the .nupkg file.</span></span>

* <span data-ttu-id="792e4-111">Do souboru .csproj přidejte následující vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="792e4-111">Either add the following properties to your .csproj file:</span></span>

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
   </PropertyGroup>
   ```

* <span data-ttu-id="792e4-112">Nebo zadejte tyto vlastnosti na příkazovém řádku:</span><span class="sxs-lookup"><span data-stu-id="792e4-112">Or specify these properties on the command-line:</span></span>

     ```dotnetcli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  <span data-ttu-id="792e4-113">– nebo –</span><span class="sxs-lookup"><span data-stu-id="792e4-113">or</span></span>

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

<span data-ttu-id="792e4-114">Pokud používáte soubor NuGet.exe, můžete kromě souboru .nupkg použít následující příkazy k vytvoření souboru Snupkg:</span><span class="sxs-lookup"><span data-stu-id="792e4-114">If you're using NuGet.exe, you can use the following commands to create a .snupkg file in addition to the .nupkg file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

<span data-ttu-id="792e4-115">Vlastnost [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) může mít jednu `symbols.nupkg` ze dvou hodnot: (výchozí) nebo `snupkg`.</span><span class="sxs-lookup"><span data-stu-id="792e4-115">The [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) property can have one of two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="792e4-116">Pokud tato vlastnost není zadána, bude vytvořen balíček starší symbol.</span><span class="sxs-lookup"><span data-stu-id="792e4-116">If this property is not specified, a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="792e4-117">Starší formát `.symbols.nupkg` je stále podporován, ale pouze z důvodů kompatibility (viz [Starší balíčky symbolů).](Symbol-Packages.md)</span><span class="sxs-lookup"><span data-stu-id="792e4-117">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="792e4-118">Server symbolů NuGet.org přijímá pouze nový formát `.snupkg`balíčku symbolů - .</span><span class="sxs-lookup"><span data-stu-id="792e4-118">NuGet.org's symbol server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="792e4-119">Publikování balíčku symbolů</span><span class="sxs-lookup"><span data-stu-id="792e4-119">Publishing a symbol package</span></span>

1. <span data-ttu-id="792e4-120">Pro větší pohodlí nejprve uložte klíč rozhraní API s NuGet (viz [publikování balíčku](../nuget-org/publish-a-package.md)).</span><span class="sxs-lookup"><span data-stu-id="792e4-120">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="792e4-121">Po publikování primární balíček nuget.org, stiskněte balíček symbol takto.</span><span class="sxs-lookup"><span data-stu-id="792e4-121">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="792e4-122">Balíčky primárních i symbolů můžete také tlačit současně pomocí příkazu níže.</span><span class="sxs-lookup"><span data-stu-id="792e4-122">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="792e4-123">V aktuální složce musí být k dispozici soubory .nupkg i .snupkg.</span><span class="sxs-lookup"><span data-stu-id="792e4-123">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="792e4-124">NuGet publikuje oba balíčky do nuget.org. `MyPackage.nupkg` budou zveřejněny jako první, následované `MyPackage.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="792e4-124">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

> [!Note]
> <span data-ttu-id="792e4-125">Pokud balíček symbolů není publikován, zkontrolujte, zda jste `https://api.nuget.org/v3/index.json`nakonfigurovali NuGet.org zdroj jako .</span><span class="sxs-lookup"><span data-stu-id="792e4-125">If the symbol package isn't published, check that you've configured the NuGet.org source as `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="792e4-126">Publikování balíčku symbolů je podporováno pouze [rozhraním API NuGet V3](../api/overview.md#versioning).</span><span class="sxs-lookup"><span data-stu-id="792e4-126">Symbol package publishing is only supported by [the NuGet V3 API](../api/overview.md#versioning).</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="792e4-127">NuGet.org symbolový server</span><span class="sxs-lookup"><span data-stu-id="792e4-127">NuGet.org symbol server</span></span>

<span data-ttu-id="792e4-128">NuGet.org podporuje vlastní úložiště serverů symbolů a přijímá pouze `.snupkg`nový formát balíčku symbolů - .</span><span class="sxs-lookup"><span data-stu-id="792e4-128">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="792e4-129">Příjemci balíčků mohou použít symboly publikované `https://symbols.nuget.org/download/symbols` na nuget.org serveru symbolů přidáním zdrojů symbolů v sadě Visual Studio, což umožňuje krokování do kódu balíčku v ladicím programu sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="792e4-129">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="792e4-130">Podrobnosti o tomto [procesu naleznete v tématu Určení symbolu (.pdb) a zdrojových souborů v ladicím programu sady Visual Studio.](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger)</span><span class="sxs-lookup"><span data-stu-id="792e4-130">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="792e4-131">omezení balíčku NuGet.org symbolů</span><span class="sxs-lookup"><span data-stu-id="792e4-131">NuGet.org symbol package constraints</span></span>

<span data-ttu-id="792e4-132">NuGet.org má následující omezení pro balíčky symbolů:</span><span class="sxs-lookup"><span data-stu-id="792e4-132">NuGet.org has the following constraints for symbol packages:</span></span>

- <span data-ttu-id="792e4-133">V balíčcích symbolů jsou povoleny `.pdb` `.nuspec`pouze `.xml` `.psmdcp`následující `.rels`přípony souborů: , , , , , ,`.p7s`</span><span class="sxs-lookup"><span data-stu-id="792e4-133">Only the following file extensions are allowed in symbol packages: `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`, `.p7s`</span></span>
- <span data-ttu-id="792e4-134">Na serveru se symboly NuGet.org jsou podporovány pouze spravované [přenosné objekty PDB.](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md)</span><span class="sxs-lookup"><span data-stu-id="792e4-134">Only managed [Portable PDBs](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are supported on NuGet.org's symbol server.</span></span>
- <span data-ttu-id="792e4-135">Disky DLL a přidružené knihovny DLL .nupkg musí být vytvořeny pomocí kompilátoru ve visual taště verze 15.9 nebo vyšší (viz [pdb kryptografický hash)](https://github.com/dotnet/roslyn/issues/24429)</span><span class="sxs-lookup"><span data-stu-id="792e4-135">The PDBs and their associated .nupkg DLLs need to be built with the compiler in Visual Studio version 15.9 or above (see [PDB crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="792e4-136">Balíčky symbolů publikované do NuGet.org se nezdaří ověření, pokud tato omezení nejsou splněna.</span><span class="sxs-lookup"><span data-stu-id="792e4-136">Symbol packages published to NuGet.org will fail validation if these constraints aren't met.</span></span> 

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="792e4-137">Ověření a indexování balíčku symbolů</span><span class="sxs-lookup"><span data-stu-id="792e4-137">Symbol package validation and indexing</span></span>

<span data-ttu-id="792e4-138">Balíčky symbolů publikované [NuGet.org](https://www.nuget.org/) podrobeny několika ověřením, včetně skenování malwaru.</span><span class="sxs-lookup"><span data-stu-id="792e4-138">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, including malware scanning.</span></span> <span data-ttu-id="792e4-139">Pokud balíček neprojde kontrolou ověření, zobrazí se na stránce podrobností o balíčku chybová zpráva.</span><span class="sxs-lookup"><span data-stu-id="792e4-139">If a package fails a validation check, its package details page will display an error message.</span></span> <span data-ttu-id="792e4-140">Kromě toho majitelé balíčku obdrží e-mail s pokyny, jak opravit zjištěné problémy.</span><span class="sxs-lookup"><span data-stu-id="792e4-140">In addition, the package's owners will receive an email with instructions on how to fix the identified issues.</span></span>

<span data-ttu-id="792e4-141">Pokud balíček symbolprošel všechna ověření, symboly budou indexovány servery symbol NuGet.org a bude k dispozici pro spotřebu.</span><span class="sxs-lookup"><span data-stu-id="792e4-141">When the symbol package has passed all validations, the symbols will be indexed by NuGet.org's symbol servers and will be available for consumption.</span></span>

<span data-ttu-id="792e4-142">Ověření a indexování balíčku obvykle trvá méně než 15 minut.</span><span class="sxs-lookup"><span data-stu-id="792e4-142">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="792e4-143">Pokud publikování balíčku trvá déle, než bylo očekáváno, navštivte [status.nuget.org](https://status.nuget.org/) a zkontrolujte, zda NuGet.org dochází k přerušení.</span><span class="sxs-lookup"><span data-stu-id="792e4-143">If the package publishing takes longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if NuGet.org is experiencing any interruptions.</span></span> <span data-ttu-id="792e4-144">Pokud jsou všechny systémy funkční a balíček nebyl úspěšně publikován do hodiny, přihlaste se do nuget.org a kontaktujte nás pomocí odkazu Kontaktujte podporu na stránce podrobností o balíčku.</span><span class="sxs-lookup"><span data-stu-id="792e4-144">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="792e4-145">Struktura balíčku symbolů</span><span class="sxs-lookup"><span data-stu-id="792e4-145">Symbol package structure</span></span>

<span data-ttu-id="792e4-146">Symbol balíček (.snupkg) má následující vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="792e4-146">The symbol package (.snupkg) has the following characteristics:</span></span>

1) <span data-ttu-id="792e4-147">.snupkg má stejné id a verzi jako jeho odpovídající Balíček NuGet (.nupkg).</span><span class="sxs-lookup"><span data-stu-id="792e4-147">The .snupkg has the same id and version as its corresponding NuGet package (.nupkg).</span></span>
2) <span data-ttu-id="792e4-148">.snupkg má stejnou strukturu složek jako jeho odpovídající .nupkg pro všechny soubory DLL nebo EXE s rozdílem, že místo DLL/EXEs budou jejich odpovídající objekty PDB zahrnuty do hierarchie stejných složek.</span><span class="sxs-lookup"><span data-stu-id="792e4-148">The .snupkg has the same folder structure as its corresponding .nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="792e4-149">Soubory a složky s jinými příponami než PDB budou ponechány mimo snupkg.</span><span class="sxs-lookup"><span data-stu-id="792e4-149">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="792e4-150">Soubor .nuspec balíčku symbolů `SymbolsPackage` má typ balíčku:</span><span class="sxs-lookup"><span data-stu-id="792e4-150">The symbol package's .nuspec file has the `SymbolsPackage` package type:</span></span>

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) <span data-ttu-id="792e4-151">Pokud se autor rozhodne použít vlastní nuspec k sestavení jejich nupkg a snupkg, snupkg by měl mít stejnou hierarchii složek a soubory podrobně popsané v 2).</span><span class="sxs-lookup"><span data-stu-id="792e4-151">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="792e4-152">Následující pole budou vyloučena z nuspec ```authors```snupkg: ```owners``` ```requireLicenseAcceptance```, ```license type``` ```licenseUrl```, ```icon```, , , a .</span><span class="sxs-lookup"><span data-stu-id="792e4-152">The following fields will be excluded from the snupkg's nuspec: ```authors```, ```owners```, ```requireLicenseAcceptance```, ```license type```, ```licenseUrl```, and  ```icon```.</span></span>
6) <span data-ttu-id="792e4-153">Nepoužívejte ```<license>``` prvek.</span><span class="sxs-lookup"><span data-stu-id="792e4-153">Do not use the ```<license>``` element.</span></span> <span data-ttu-id="792e4-154">A .snupkg je zahrnuta ve stejné licenci jako odpovídající .nupkg.</span><span class="sxs-lookup"><span data-stu-id="792e4-154">A .snupkg is covered under the same license as the corresponding .nupkg.</span></span>

## <a name="see-also"></a><span data-ttu-id="792e4-155">Viz také</span><span class="sxs-lookup"><span data-stu-id="792e4-155">See also</span></span>

<span data-ttu-id="792e4-156">Zvažte použití zdrojového odkazu k povolení ladění zdrojového kódu sestavení .NET.</span><span class="sxs-lookup"><span data-stu-id="792e4-156">Consider using Source Link to enable source code debugging of .NET assemblies.</span></span> <span data-ttu-id="792e4-157">Další informace naleznete v [pokynech pro zdrojový odkaz](/dotnet/standard/library-guidance/sourcelink).</span><span class="sxs-lookup"><span data-stu-id="792e4-157">For more information, please refer to the [Source Link guidance](/dotnet/standard/library-guidance/sourcelink).</span></span>

<span data-ttu-id="792e4-158">Další informace o balíčcích symbolů naleznete v specifikaci návrhu [ladění balíčků NuGet & symboly.](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)</span><span class="sxs-lookup"><span data-stu-id="792e4-158">For more information on symbol packages, please refer to the [NuGet Package Debugging & Symbols Improvements](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) design spec.</span></span>
