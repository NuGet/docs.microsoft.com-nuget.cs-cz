---
title: Jak publikovat balíčky symbolů NuGet pomocí nového formátu balíčku symbolů '. snupkg ' | Microsoft Docs
author: cristinamanu
ms.author: cristinamanu
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Jak vytvořit balíčky symbolů NuGet (snupkg).
keywords: Balíčky symbolů NuGet, ladění balíčku NuGet, podpora ladění NuGet, symboly balíčků, konvence balíčků symbolů
ms.reviewer:
- anangaur
- karann
ms.openlocfilehash: 0197902e4dbc18893d68833fbcfe4263f185a594
ms.sourcegitcommit: e4b0ff4460865db6dc7bc9f20e9f644d98493011
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/26/2019
ms.locfileid: "71307188"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="47c74-104">Vytváření balíčků symbolů (. snupkg)</span><span class="sxs-lookup"><span data-stu-id="47c74-104">Creating symbol packages (.snupkg)</span></span>

<span data-ttu-id="47c74-105">Balíčky symbolů umožňují zlepšit možnosti ladění balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="47c74-105">Symbol packages allow you to improve the debugging experience of your NuGet packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47c74-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="47c74-106">Prerequisites</span></span>

<span data-ttu-id="47c74-107">[NuGet. exe v 4.9.0 nebo novější](https://www.nuget.org/downloads) nebo [dotnet. exe v 2.2.0 nebo vyšší](https://www.microsoft.com/net/download/dotnet-core/2.2), které implementují požadované [protokoly NuGet](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="47c74-107">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet.exe v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="47c74-108">Vytvoření balíčku symbolů</span><span class="sxs-lookup"><span data-stu-id="47c74-108">Creating a symbol package</span></span>

<span data-ttu-id="47c74-109">Pokud používáte dotnet. exe nebo MSBuild, je třeba nastavit `IncludeSymbols` vlastnosti a a `SymbolPackageFormat` vytvořit soubor. snupkg společně se souborem. nupkg.</span><span class="sxs-lookup"><span data-stu-id="47c74-109">If you're using dotnet.exe or MSBuild, you need to set the `IncludeSymbols` and `SymbolPackageFormat` properties to create a .snupkg file in addition to the .nupkg file.</span></span>

* <span data-ttu-id="47c74-110">Přidejte do souboru. csproj následující vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="47c74-110">Either add the following properties to your .csproj file:</span></span>

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols> 
      <SymbolPackageFormat>snupkg</SymbolPackageFormat> 
   </PropertyGroup>
   ```

* <span data-ttu-id="47c74-111">Nebo zadejte tyto vlastnosti na příkazovém řádku:</span><span class="sxs-lookup"><span data-stu-id="47c74-111">Or specify these properties on the command-line:</span></span>

     ```cli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  <span data-ttu-id="47c74-112">or</span><span class="sxs-lookup"><span data-stu-id="47c74-112">or</span></span>

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

<span data-ttu-id="47c74-113">Pokud používáte NuGet. exe, můžete k vytvoření souboru. snupkg spolu s souborem. nupkg použít následující příkazy:</span><span class="sxs-lookup"><span data-stu-id="47c74-113">If you're using NuGet.exe, you can use the following commands to create a .snupkg file in addition to the .nupkg file:</span></span>

```
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

<span data-ttu-id="47c74-114">Vlastnost může mít jednu ze dvou hodnot: `symbols.nupkg` (výchozí) nebo `snupkg`. [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat)</span><span class="sxs-lookup"><span data-stu-id="47c74-114">The [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) property can have one of two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="47c74-115">Pokud tato vlastnost není zadána, bude vytvořen starší balíček symbolů.</span><span class="sxs-lookup"><span data-stu-id="47c74-115">If this property is not specified, a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="47c74-116">Starší verze formátu `.symbols.nupkg` jsou stále podporovány, ale pouze z důvodů kompatibility (viz [starší balíčky symbolů](Symbol-Packages.md)).</span><span class="sxs-lookup"><span data-stu-id="47c74-116">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="47c74-117">Server symbolů NuGet. org přijímá pouze nový formát balíčku symbolů – `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="47c74-117">NuGet.org's symbol server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="47c74-118">Publikování balíčku symbolů</span><span class="sxs-lookup"><span data-stu-id="47c74-118">Publishing a symbol package</span></span>

1. <span data-ttu-id="47c74-119">Pro usnadnění práce nejdřív uložte klíč rozhraní API pomocí NuGet (viz [publikování balíčku](../nuget-org/publish-a-package.md)).</span><span class="sxs-lookup"><span data-stu-id="47c74-119">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="47c74-120">Po publikování primárního balíčku na nuget.org vložte balíček symbolů následujícím způsobem.</span><span class="sxs-lookup"><span data-stu-id="47c74-120">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="47c74-121">Pomocí níže uvedeného příkazu můžete zároveň současně nabízet jak primární, tak i balíčky symbolů.</span><span class="sxs-lookup"><span data-stu-id="47c74-121">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="47c74-122">V aktuální složce musí být přítomné soubory. nupkg a. snupkg.</span><span class="sxs-lookup"><span data-stu-id="47c74-122">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="47c74-123">NuGet bude publikovat oba balíčky do nuget.org. bude Publikováno jako první, `MyPackage.snupkg`následované. `MyPackage.nupkg`</span><span class="sxs-lookup"><span data-stu-id="47c74-123">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

> [!Note]
> <span data-ttu-id="47c74-124">Pokud se balíček symbolů nepublikuje, ověřte, že jste nakonfigurovali zdroj NuGet.org `https://api.nuget.org/v3/index.json`jako.</span><span class="sxs-lookup"><span data-stu-id="47c74-124">If the symbol package isn't published, check that you've configured the NuGet.org source as `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="47c74-125">Publikování balíčku symbolů je podporované jenom [rozhraním API NuGet V3](../api/overview.md#versioning).</span><span class="sxs-lookup"><span data-stu-id="47c74-125">Symbol package publishing is only supported by [the NuGet V3 API](../api/overview.md#versioning).</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="47c74-126">NuGet.org symbol server</span><span class="sxs-lookup"><span data-stu-id="47c74-126">NuGet.org symbol server</span></span>

<span data-ttu-id="47c74-127">NuGet.org podporuje vlastní úložiště symbolů serveru a přijímá pouze nový formát balíčku symbolů – `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="47c74-127">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="47c74-128">Příjemci balíčku můžou použít symboly publikované do serveru symbolů NuGet.org přidáním `https://symbols.nuget.org/download/symbols` do jejich zdrojů symbolů v aplikaci Visual Studio, které umožňují krokování kódu balíčku v ladicím programu sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="47c74-128">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="47c74-129">Podrobnosti o tomto procesu najdete v tématu [určení symbolu (PDB) a zdrojových souborů v ladicím programu sady Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) .</span><span class="sxs-lookup"><span data-stu-id="47c74-129">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="47c74-130">Omezení balíčku symbolů NuGet.org</span><span class="sxs-lookup"><span data-stu-id="47c74-130">NuGet.org symbol package constraints</span></span>

<span data-ttu-id="47c74-131">NuGet.org má následující omezení pro balíčky symbolů:</span><span class="sxs-lookup"><span data-stu-id="47c74-131">NuGet.org has the following constraints for symbol packages:</span></span>

- <span data-ttu-id="47c74-132">V balíčcích symbolů jsou povoleny pouze následující přípony souborů: `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`,`.p7s`</span><span class="sxs-lookup"><span data-stu-id="47c74-132">Only the following file extensions are allowed in symbol packages: `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`, `.p7s`</span></span>
- <span data-ttu-id="47c74-133">Na serveru se symbolem NuGet. org jsou podporované jenom spravované [přenosné soubory PDB](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) .</span><span class="sxs-lookup"><span data-stu-id="47c74-133">Only managed [Portable PDBs](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are supported on NuGet.org's symbol server.</span></span>
- <span data-ttu-id="47c74-134">Soubory PDB a jejich přidružené knihovny DLL nupkg musí být sestaveny s kompilátorem v aplikaci Visual Studio verze 15,9 nebo vyšší (viz [PDB kryptografický otisk](https://github.com/dotnet/roslyn/issues/24429)).</span><span class="sxs-lookup"><span data-stu-id="47c74-134">The PDBs and their associated .nupkg DLLs need to be built with the compiler in Visual Studio version 15.9 or above (see [PDB crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="47c74-135">Balíčky symbolů publikované do NuGet.org selžou, pokud tato omezení nebudou splněna.</span><span class="sxs-lookup"><span data-stu-id="47c74-135">Symbol packages published to NuGet.org will fail validation if these constraints aren't met.</span></span> 

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="47c74-136">Ověřování a indexování balíčku symbolů</span><span class="sxs-lookup"><span data-stu-id="47c74-136">Symbol package validation and indexing</span></span>

<span data-ttu-id="47c74-137">Balíčky symbolů publikované do [NuGet.org](https://www.nuget.org/) prošly několika ověřeními, včetně kontroly malwaru.</span><span class="sxs-lookup"><span data-stu-id="47c74-137">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, including malware scanning.</span></span> <span data-ttu-id="47c74-138">Pokud balíček selže, zobrazí se na stránce Podrobnosti o jeho balíčku chybová zpráva.</span><span class="sxs-lookup"><span data-stu-id="47c74-138">If a package fails a validation check, its package details page will display an error message.</span></span> <span data-ttu-id="47c74-139">Kromě toho vlastníci balíčku obdrží e-mail s pokyny, jak opravit zjištěné problémy.</span><span class="sxs-lookup"><span data-stu-id="47c74-139">In addition, the package's owners will receive an email with instructions on how to fix the identified issues.</span></span>

<span data-ttu-id="47c74-140">Když balíček symbolů předává všechna ověření, symboly budou indexovány pomocí serverů se symboly NuGet. org.</span><span class="sxs-lookup"><span data-stu-id="47c74-140">When the symbol package has passed all validations, the symbols will be indexed by NuGet.org's symbol servers.</span></span> <span data-ttu-id="47c74-141">Po indexování bude symbol dostupný pro spotřebu ze serverů symbolů NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="47c74-141">Once indexed, the symbol will be available for consumption from the NuGet.org symbol servers.</span></span>

<span data-ttu-id="47c74-142">Ověření a indexování balíčku obvykle trvá 15 minut.</span><span class="sxs-lookup"><span data-stu-id="47c74-142">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="47c74-143">Pokud publikování balíčku trvá déle, než se čekalo, navštivte [status.NuGet.org](https://status.nuget.org/) a ověřte, jestli NuGet.org má nějaké přerušení.</span><span class="sxs-lookup"><span data-stu-id="47c74-143">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if NuGet.org is experiencing any interruptions.</span></span> <span data-ttu-id="47c74-144">Pokud jsou všechny systémy funkční a balíček ještě není po celou hodinu publikovaný, přihlaste se k nuget.org a na stránce s podrobnostmi balíčku kontaktujte nás pomocí odkazu podpora kontaktů.</span><span class="sxs-lookup"><span data-stu-id="47c74-144">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="47c74-145">Struktura balíčku symbolů</span><span class="sxs-lookup"><span data-stu-id="47c74-145">Symbol package structure</span></span>

<span data-ttu-id="47c74-146">Soubor. nupkg by byl přesně stejný, jako v současné době, ale soubor. snupkg má následující vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="47c74-146">The .nupkg file would be exactly the same as it is today, but the .snupkg file would have the following characteristics:</span></span>

1) <span data-ttu-id="47c74-147">Přípona. snupkg bude mít stejné ID a verzi jako odpovídající. nupkg.</span><span class="sxs-lookup"><span data-stu-id="47c74-147">The .snupkg will have the same id and version as the corresponding .nupkg.</span></span>
2) <span data-ttu-id="47c74-148">Soubor. snupkg bude mít přesnou strukturu složek jako nupkg pro všechny soubory DLL nebo EXE s rozlišením, které místo knihoven DLL/exe, jejich odpovídající soubory PDB bude zahrnuta do stejné hierarchie složek.</span><span class="sxs-lookup"><span data-stu-id="47c74-148">The .snupkg will have the exact folder structure as the nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="47c74-149">Soubory a složky s rozšířeními jinými než PDB budou ponechány mimo snupkg.</span><span class="sxs-lookup"><span data-stu-id="47c74-149">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="47c74-150">Soubor. nuspec v souboru. snupkg také určí nové PackageType, jak je uvedeno níže.</span><span class="sxs-lookup"><span data-stu-id="47c74-150">The .nuspec file in the .snupkg will also specify a new PackageType as below.</span></span> <span data-ttu-id="47c74-151">Mělo by se zadat jenom jeden PackageType.</span><span class="sxs-lookup"><span data-stu-id="47c74-151">This should the only one PackageType specified.</span></span>

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) <span data-ttu-id="47c74-152">Pokud se autor rozhodne použít vlastní nuspec k sestavení nupkg a snupkg, měl by mít snupkg stejnou hierarchii složek a souborů, které jsou popsány v 2).</span><span class="sxs-lookup"><span data-stu-id="47c74-152">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="47c74-153">```authors```a ```owners``` pole bude vyloučeno z nuspecu snupkg.</span><span class="sxs-lookup"><span data-stu-id="47c74-153">```authors``` and ```owners``` field will be excluded from the snupkg's nuspec.</span></span>
6) <span data-ttu-id="47c74-154">Nepoužívejte ```<license>``` element.</span><span class="sxs-lookup"><span data-stu-id="47c74-154">Do not use the ```<license>``` element.</span></span> <span data-ttu-id="47c74-155">A. snupkg se zabývá stejnou licencí jako odpovídající. nupkg.</span><span class="sxs-lookup"><span data-stu-id="47c74-155">A .snupkg is covered under the same license as the corresponding .nupkg.</span></span>

## <a name="see-also"></a><span data-ttu-id="47c74-156">Viz také</span><span class="sxs-lookup"><span data-stu-id="47c74-156">See Also</span></span>

<span data-ttu-id="47c74-157">Zvažte použití odkazu na zdroj pro povolení ladění zdrojového kódu v sestaveních .NET.</span><span class="sxs-lookup"><span data-stu-id="47c74-157">Consider using Source Link to enable source code debugging of .NET assemblies.</span></span> <span data-ttu-id="47c74-158">Další informace najdete v [pokynech ke zdrojovému propojení](/dotnet/standard/library-guidance/sourcelink).</span><span class="sxs-lookup"><span data-stu-id="47c74-158">For more information, please refer to the [Source Link guidance](/dotnet/standard/library-guidance/sourcelink).</span></span>

<span data-ttu-id="47c74-159">Další informace o balíčcích symbolů najdete v tématu [Ladění balíčků NuGet &ch symbolů vylepšení](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) návrhu.</span><span class="sxs-lookup"><span data-stu-id="47c74-159">For more information on symbol packages, please refer to the [NuGet Package Debugging & Symbols Improvements](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) design spec.</span></span>
