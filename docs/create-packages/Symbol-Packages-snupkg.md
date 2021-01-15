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
ms.openlocfilehash: fbcc035a6b800617f995d3bcebd7e1764aa467b0
ms.sourcegitcommit: 323a107c345c7cb4e344a6e6d8de42c63c5188b7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/15/2021
ms.locfileid: "98235721"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="d4b6d-104">Vytváření balíčků symbolů (. snupkg)</span><span class="sxs-lookup"><span data-stu-id="d4b6d-104">Creating symbol packages (.snupkg)</span></span>

<span data-ttu-id="d4b6d-105">Dobré prostředí ladění spoléhá na přítomnost symbolů ladění, protože poskytují kritické informace, jako je například přidružení mezi zkompilovaným a zdrojovým kódem, názvy místních proměnných, trasování zásobníku a další.</span><span class="sxs-lookup"><span data-stu-id="d4b6d-105">A good debugging experience relies on the presence of debug symbols as they provide critical information like the association between the compiled and the source code, names of local variables, stack traces, and more.</span></span> <span data-ttu-id="d4b6d-106">Balíčky symbolů (. snupkg) můžete použít k distribuci těchto symbolů a zlepšení možností ladění balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="d4b6d-106">You can use symbol packages (.snupkg) to distribute these symbols and improve the debugging experience of your NuGet packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d4b6d-107">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="d4b6d-107">Prerequisites</span></span>

<span data-ttu-id="d4b6d-108">[nuget.exe v 4.9.0 nebo vyšší](https://www.nuget.org/downloads) nebo [dotnet CLI v 2.2.0 nebo vyšší](https://www.microsoft.com/net/download/dotnet-core/2.2), které implementují požadované [protokoly NuGet](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="d4b6d-108">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet CLI v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="d4b6d-109">Vytvoření balíčku symbolů</span><span class="sxs-lookup"><span data-stu-id="d4b6d-109">Creating a symbol package</span></span>

<span data-ttu-id="d4b6d-110">Pokud používáte dotnet CLI nebo MSBuild, musíte nastavit `IncludeSymbols` vlastnosti a a `SymbolPackageFormat` vytvořit soubor. snupkg společně s souborem. nupkg.</span><span class="sxs-lookup"><span data-stu-id="d4b6d-110">If you're using dotnet CLI or MSBuild, you need to set the `IncludeSymbols` and `SymbolPackageFormat` properties to create a .snupkg file in addition to the .nupkg file.</span></span>

* <span data-ttu-id="d4b6d-111">Přidejte do souboru. csproj následující vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="d4b6d-111">Either add the following properties to your .csproj file:</span></span>

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
   </PropertyGroup>
   ```

* <span data-ttu-id="d4b6d-112">Nebo zadejte tyto vlastnosti na příkazovém řádku:</span><span class="sxs-lookup"><span data-stu-id="d4b6d-112">Or specify these properties on the command-line:</span></span>

     ```dotnetcli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  <span data-ttu-id="d4b6d-113">nebo</span><span class="sxs-lookup"><span data-stu-id="d4b6d-113">or</span></span>

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

<span data-ttu-id="d4b6d-114">Pokud používáte NuGet.exe, můžete k vytvoření souboru. snupkg spolu s souborem. nupkg použít následující příkazy:</span><span class="sxs-lookup"><span data-stu-id="d4b6d-114">If you're using NuGet.exe, you can use the following commands to create a .snupkg file in addition to the .nupkg file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

<span data-ttu-id="d4b6d-115">[`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat)Vlastnost může mít jednu ze dvou hodnot: `symbols.nupkg` (výchozí) nebo `snupkg` .</span><span class="sxs-lookup"><span data-stu-id="d4b6d-115">The [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) property can have one of two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="d4b6d-116">Pokud tato vlastnost není zadána, bude vytvořen starší balíček symbolů.</span><span class="sxs-lookup"><span data-stu-id="d4b6d-116">If this property is not specified, a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="d4b6d-117">Starší verze formátu `.symbols.nupkg` jsou stále podporovány, ale pouze z důvodů kompatibility, jako jsou nativní balíčky (viz [starší balíčky symbolů](Symbol-Packages.md)).</span><span class="sxs-lookup"><span data-stu-id="d4b6d-117">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons like native packages (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="d4b6d-118">Server symbolů NuGet. org přijímá pouze nový formát balíčku symbolů – `.snupkg` .</span><span class="sxs-lookup"><span data-stu-id="d4b6d-118">NuGet.org's symbol server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="d4b6d-119">Publikování balíčku symbolů</span><span class="sxs-lookup"><span data-stu-id="d4b6d-119">Publishing a symbol package</span></span>

1. <span data-ttu-id="d4b6d-120">Pro usnadnění práce nejdřív uložte klíč rozhraní API pomocí NuGet (viz [publikování balíčku](../nuget-org/publish-a-package.md)).</span><span class="sxs-lookup"><span data-stu-id="d4b6d-120">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="d4b6d-121">Po publikování primárního balíčku na nuget.org vložte balíček symbolů následujícím způsobem.</span><span class="sxs-lookup"><span data-stu-id="d4b6d-121">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="d4b6d-122">Pomocí níže uvedeného příkazu můžete zároveň současně nabízet jak primární, tak i balíčky symbolů.</span><span class="sxs-lookup"><span data-stu-id="d4b6d-122">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="d4b6d-123">V aktuální složce musí být přítomné soubory. nupkg a. snupkg.</span><span class="sxs-lookup"><span data-stu-id="d4b6d-123">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="d4b6d-124">NuGet bude publikovat oba balíčky do nuget.org. `MyPackage.nupkg` bude Publikováno jako první, následované `MyPackage.snupkg` .</span><span class="sxs-lookup"><span data-stu-id="d4b6d-124">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

> [!Note]
> <span data-ttu-id="d4b6d-125">Pokud se balíček symbolů nepublikuje, ověřte, že jste nakonfigurovali zdroj NuGet.org jako `https://api.nuget.org/v3/index.json` .</span><span class="sxs-lookup"><span data-stu-id="d4b6d-125">If the symbol package isn't published, check that you've configured the NuGet.org source as `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="d4b6d-126">Publikování balíčku symbolů je podporované jenom [rozhraním API NuGet V3](../api/overview.md#versioning).</span><span class="sxs-lookup"><span data-stu-id="d4b6d-126">Symbol package publishing is only supported by [the NuGet V3 API](../api/overview.md#versioning).</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="d4b6d-127">Server symbolů NuGet.org</span><span class="sxs-lookup"><span data-stu-id="d4b6d-127">NuGet.org symbol server</span></span>

<span data-ttu-id="d4b6d-128">NuGet.org podporuje vlastní úložiště symbolů serveru a přijímá pouze nový formát balíčku symbolů – `.snupkg` .</span><span class="sxs-lookup"><span data-stu-id="d4b6d-128">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="d4b6d-129">Příjemci balíčku můžou použít symboly publikované do serveru symbolů nuget.org přidáním `https://symbols.nuget.org/download/symbols` do jejich zdrojů symbolů v aplikaci Visual Studio, které umožňují krokování kódu balíčku v ladicím programu sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d4b6d-129">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="d4b6d-130">Podrobnosti o tomto procesu najdete v tématu [určení symbolu (PDB) a zdrojových souborů v ladicím programu sady Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) .</span><span class="sxs-lookup"><span data-stu-id="d4b6d-130">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="d4b6d-131">Omezení balíčku symbolů NuGet.org</span><span class="sxs-lookup"><span data-stu-id="d4b6d-131">NuGet.org symbol package constraints</span></span>

<span data-ttu-id="d4b6d-132">NuGet.org má následující omezení pro balíčky symbolů:</span><span class="sxs-lookup"><span data-stu-id="d4b6d-132">NuGet.org has the following constraints for symbol packages:</span></span>

- <span data-ttu-id="d4b6d-133">V balíčcích symbolů jsou povoleny pouze následující přípony souborů: `.pdb` , `.nuspec` , `.xml` , `.psmdcp` , `.rels` , `.p7s`</span><span class="sxs-lookup"><span data-stu-id="d4b6d-133">Only the following file extensions are allowed in symbol packages: `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`, `.p7s`</span></span>
- <span data-ttu-id="d4b6d-134">Na serveru se symbolem NuGet. org jsou podporované jenom spravované [přenosné soubory PDB](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) .</span><span class="sxs-lookup"><span data-stu-id="d4b6d-134">Only managed [Portable PDBs](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are supported on NuGet.org's symbol server.</span></span>
- <span data-ttu-id="d4b6d-135">Soubory PDB a jejich přidružené knihovny DLL nupkg musí být sestaveny s kompilátorem v aplikaci Visual Studio verze 15,9 nebo vyšší (viz [PDB kryptografický otisk](https://github.com/dotnet/roslyn/issues/24429)).</span><span class="sxs-lookup"><span data-stu-id="d4b6d-135">The PDBs and their associated .nupkg DLLs need to be built with the compiler in Visual Studio version 15.9 or above (see [PDB crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="d4b6d-136">Balíčky symbolů publikované do NuGet.org selžou, pokud tato omezení nebudou splněna.</span><span class="sxs-lookup"><span data-stu-id="d4b6d-136">Symbol packages published to NuGet.org will fail validation if these constraints aren't met.</span></span> 

> [!NOTE]
> <span data-ttu-id="d4b6d-137">Nativní projekty, jako jsou projekty C++, vytváří Windows soubory PDB místo přenosných soubory PDB.</span><span class="sxs-lookup"><span data-stu-id="d4b6d-137">Native projects, such as C++ projects, produce Windows PDBs instead of Portable PDBs.</span></span> <span data-ttu-id="d4b6d-138">Ty nejsou podporovány serverem symbolů NuGet. org.</span><span class="sxs-lookup"><span data-stu-id="d4b6d-138">These are not supported by NuGet.org's symbol server.</span></span> <span data-ttu-id="d4b6d-139">Místo toho prosím použijte [starší balíčky symbolů](Symbol-Packages.md) .</span><span class="sxs-lookup"><span data-stu-id="d4b6d-139">Please use [Legacy Symbol Packages](Symbol-Packages.md) instead.</span></span>

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="d4b6d-140">Ověřování a indexování balíčku symbolů</span><span class="sxs-lookup"><span data-stu-id="d4b6d-140">Symbol package validation and indexing</span></span>

<span data-ttu-id="d4b6d-141">Balíčky symbolů publikované do [NuGet.org](https://www.nuget.org/) prošly několika ověřeními, včetně kontroly malwaru.</span><span class="sxs-lookup"><span data-stu-id="d4b6d-141">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, including malware scanning.</span></span> <span data-ttu-id="d4b6d-142">Pokud balíček selže, zobrazí se na stránce Podrobnosti o jeho balíčku chybová zpráva.</span><span class="sxs-lookup"><span data-stu-id="d4b6d-142">If a package fails a validation check, its package details page will display an error message.</span></span> <span data-ttu-id="d4b6d-143">Kromě toho vlastníci balíčku obdrží e-mail s pokyny, jak opravit zjištěné problémy.</span><span class="sxs-lookup"><span data-stu-id="d4b6d-143">In addition, the package's owners will receive an email with instructions on how to fix the identified issues.</span></span>

<span data-ttu-id="d4b6d-144">Když balíček symbolů předává všechna ověření, symboly budou indexovány na servery se symboly NuGet. org a budou k dispozici pro spotřebu.</span><span class="sxs-lookup"><span data-stu-id="d4b6d-144">When the symbol package has passed all validations, the symbols will be indexed by NuGet.org's symbol servers and will be available for consumption.</span></span>

<span data-ttu-id="d4b6d-145">Ověření a indexování balíčku obvykle trvá 15 minut.</span><span class="sxs-lookup"><span data-stu-id="d4b6d-145">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="d4b6d-146">Pokud bude publikování balíčku trvat déle, než se čekalo, navštivte [status.NuGet.org](https://status.nuget.org/) a ověřte, jestli NuGet.org má nějaké přerušení.</span><span class="sxs-lookup"><span data-stu-id="d4b6d-146">If the package publishing takes longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if NuGet.org is experiencing any interruptions.</span></span> <span data-ttu-id="d4b6d-147">Pokud jsou všechny systémy funkční a balíček ještě není po celou hodinu publikovaný, přihlaste se k nuget.org a na stránce s podrobnostmi balíčku kontaktujte nás pomocí odkazu podpora kontaktů.</span><span class="sxs-lookup"><span data-stu-id="d4b6d-147">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="d4b6d-148">Struktura balíčku symbolů</span><span class="sxs-lookup"><span data-stu-id="d4b6d-148">Symbol package structure</span></span>

<span data-ttu-id="d4b6d-149">Balíček symbolů (. snupkg) má následující vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="d4b6d-149">The symbol package (.snupkg) has the following characteristics:</span></span>

1) <span data-ttu-id="d4b6d-150">Soubor. snupkg má stejné ID a verzi jako odpovídající balíček NuGet (. nupkg).</span><span class="sxs-lookup"><span data-stu-id="d4b6d-150">The .snupkg has the same id and version as its corresponding NuGet package (.nupkg).</span></span>
2) <span data-ttu-id="d4b6d-151">Přípona. snupkg má stejnou strukturu složek jako odpovídající. nupkg pro jakékoli soubory DLL nebo EXE s rozlišením, které místo knihoven DLL/exe, jejich odpovídající soubory PDB bude zahrnuta do stejné hierarchie složek.</span><span class="sxs-lookup"><span data-stu-id="d4b6d-151">The .snupkg has the same folder structure as its corresponding .nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="d4b6d-152">Soubory a složky s rozšířeními jinými než PDB budou ponechány mimo snupkg.</span><span class="sxs-lookup"><span data-stu-id="d4b6d-152">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="d4b6d-153">Soubor. nuspec balíčku symbolů má `SymbolsPackage` Typ balíčku:</span><span class="sxs-lookup"><span data-stu-id="d4b6d-153">The symbol package's .nuspec file has the `SymbolsPackage` package type:</span></span>

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) <span data-ttu-id="d4b6d-154">Pokud se autor rozhodne použít vlastní nuspec k sestavení nupkg a snupkg, měl by mít snupkg stejnou hierarchii složek a souborů, které jsou popsány v 2).</span><span class="sxs-lookup"><span data-stu-id="d4b6d-154">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="d4b6d-155">Následující pole budou vyloučena z nuspec snupkg: ```authors``` , ```owners``` , ```requireLicenseAcceptance``` , ```license type``` , ```licenseUrl``` a  ```icon``` .</span><span class="sxs-lookup"><span data-stu-id="d4b6d-155">The following fields will be excluded from the snupkg's nuspec: ```authors```, ```owners```, ```requireLicenseAcceptance```, ```license type```, ```licenseUrl```, and  ```icon```.</span></span>
6) <span data-ttu-id="d4b6d-156">Nepoužívejte ```<license>``` element.</span><span class="sxs-lookup"><span data-stu-id="d4b6d-156">Do not use the ```<license>``` element.</span></span> <span data-ttu-id="d4b6d-157">A. snupkg se zabývá stejnou licencí jako odpovídající. nupkg.</span><span class="sxs-lookup"><span data-stu-id="d4b6d-157">A .snupkg is covered under the same license as the corresponding .nupkg.</span></span>

## <a name="see-also"></a><span data-ttu-id="d4b6d-158">Viz také:</span><span class="sxs-lookup"><span data-stu-id="d4b6d-158">See also</span></span>

<span data-ttu-id="d4b6d-159">Zvažte použití odkazu na zdroj pro povolení ladění zdrojového kódu v sestaveních .NET.</span><span class="sxs-lookup"><span data-stu-id="d4b6d-159">Consider using Source Link to enable source code debugging of .NET assemblies.</span></span> <span data-ttu-id="d4b6d-160">Další informace najdete v [pokynech ke zdrojovému propojení](/dotnet/standard/library-guidance/sourcelink).</span><span class="sxs-lookup"><span data-stu-id="d4b6d-160">For more information, please refer to the [Source Link guidance](/dotnet/standard/library-guidance/sourcelink).</span></span>

<span data-ttu-id="d4b6d-161">Další informace o balíčcích symbolů najdete v tématu [Ladění balíčků NuGet &ch symbolů vylepšení](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) návrhu.</span><span class="sxs-lookup"><span data-stu-id="d4b6d-161">For more information on symbol packages, please refer to the [NuGet Package Debugging & Symbols Improvements](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) design spec.</span></span>
