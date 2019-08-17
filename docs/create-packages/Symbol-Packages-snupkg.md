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
ms.openlocfilehash: 992b3ddd04a1bb34e7aca25dfaa6f7df5485907b
ms.sourcegitcommit: 80cf99f40759911324468be1ec815c96aebf376d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/17/2019
ms.locfileid: "69564542"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="b13d9-104">Vytváření balíčků symbolů (. snupkg)</span><span class="sxs-lookup"><span data-stu-id="b13d9-104">Creating symbol packages (.snupkg)</span></span>

<span data-ttu-id="b13d9-105">Balíčky symbolů umožňují zlepšit možnosti ladění balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="b13d9-105">Symbol packages allow you to improve the debugging experience of your NuGet packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b13d9-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="b13d9-106">Prerequisites</span></span>

<span data-ttu-id="b13d9-107">[NuGet. exe v 4.9.0 nebo novější](https://www.nuget.org/downloads) nebo [dotnet. exe v 2.2.0 nebo vyšší](https://www.microsoft.com/net/download/dotnet-core/2.2), které implementují požadované [protokoly NuGet](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="b13d9-107">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet.exe v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="b13d9-108">Vytvoření balíčku symbolů</span><span class="sxs-lookup"><span data-stu-id="b13d9-108">Creating a symbol package</span></span>

<span data-ttu-id="b13d9-109">Balíček snupkg symbol můžete vytvořit pomocí příkazu dotnet. exe, NuGet. exe nebo MSBuild.</span><span class="sxs-lookup"><span data-stu-id="b13d9-109">You can create a snupkg symbol package using dotnet.exe, NuGet.exe, or MSBuild.</span></span> <span data-ttu-id="b13d9-110">Pokud používáte NuGet. exe, můžete k vytvoření souboru. snupkg spolu s souborem. nupkg použít následující příkazy:</span><span class="sxs-lookup"><span data-stu-id="b13d9-110">If you're using NuGet.exe, you can use the following commands to create a .snupkg file in addition to the .nupkg file:</span></span>

```
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

<span data-ttu-id="b13d9-111">Pokud používáte dotnet. exe nebo MSBuild, použijte následující postup k vytvoření souboru. snupkg společně se souborem. nupkg:</span><span class="sxs-lookup"><span data-stu-id="b13d9-111">If you're using dotnet.exe or MSBuild, use the following steps to create a .snupkg file in addition to the .nupkg file:</span></span>

1. <span data-ttu-id="b13d9-112">Do souboru. csproj přidejte následující vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="b13d9-112">Add the following properties to your .csproj file:</span></span>

    ```xml
    <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
    </PropertyGroup>
    ```

1. <span data-ttu-id="b13d9-113">Sbalení projektu pomocí `dotnet pack MyPackage.csproj` nebo `msbuild -t:pack MyPackage.csproj`.</span><span class="sxs-lookup"><span data-stu-id="b13d9-113">Pack your project with `dotnet pack MyPackage.csproj` or `msbuild -t:pack MyPackage.csproj`.</span></span>

<span data-ttu-id="b13d9-114">Vlastnost může mít jednu ze dvou hodnot: `symbols.nupkg` (výchozí) nebo `snupkg`. [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat)</span><span class="sxs-lookup"><span data-stu-id="b13d9-114">The [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) property can have one of two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="b13d9-115">[`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) Pokud vlastnost není zadána, bude vytvořen starší balíček symbolů.</span><span class="sxs-lookup"><span data-stu-id="b13d9-115">If the [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) property is not specified, a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="b13d9-116">Starší verze formátu `.symbols.nupkg` jsou stále podporovány, ale pouze z důvodů kompatibility (viz [starší balíčky symbolů](Symbol-Packages.md)).</span><span class="sxs-lookup"><span data-stu-id="b13d9-116">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="b13d9-117">Server symbolů NuGet. org přijímá pouze nový formát balíčku symbolů – `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="b13d9-117">NuGet.org's symbol server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="b13d9-118">Publikování balíčku symbolů</span><span class="sxs-lookup"><span data-stu-id="b13d9-118">Publishing a symbol package</span></span>

1. <span data-ttu-id="b13d9-119">Pro usnadnění práce nejdřív uložte klíč rozhraní API pomocí NuGet (viz [publikování balíčku](../nuget-org/publish-a-package.md)).</span><span class="sxs-lookup"><span data-stu-id="b13d9-119">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="b13d9-120">Po publikování primárního balíčku na nuget.org vložte balíček symbolů následujícím způsobem.</span><span class="sxs-lookup"><span data-stu-id="b13d9-120">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="b13d9-121">Pomocí níže uvedeného příkazu můžete zároveň současně nabízet jak primární, tak i balíčky symbolů.</span><span class="sxs-lookup"><span data-stu-id="b13d9-121">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="b13d9-122">V aktuální složce musí být přítomné soubory. nupkg a. snupkg.</span><span class="sxs-lookup"><span data-stu-id="b13d9-122">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="b13d9-123">NuGet bude publikovat oba balíčky do nuget.org. bude Publikováno jako první, `MyPackage.snupkg`následované. `MyPackage.nupkg`</span><span class="sxs-lookup"><span data-stu-id="b13d9-123">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

> [!Note]
> <span data-ttu-id="b13d9-124">Pokud se balíček symbolů nepublikuje, ověřte, že jste nakonfigurovali zdroj NuGet.org `https://api.nuget.org/v3/index.json`jako.</span><span class="sxs-lookup"><span data-stu-id="b13d9-124">If the symbol package isn't published, check that you've configured the NuGet.org source as `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="b13d9-125">Publikování balíčku symbolů je podporované jenom [rozhraním API NuGet V3](../api/overview.md#versioning).</span><span class="sxs-lookup"><span data-stu-id="b13d9-125">Symbol package publishing is only supported by [the NuGet V3 API](../api/overview.md#versioning).</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="b13d9-126">NuGet.org symbol server</span><span class="sxs-lookup"><span data-stu-id="b13d9-126">NuGet.org symbol server</span></span>

<span data-ttu-id="b13d9-127">NuGet.org podporuje vlastní úložiště symbolů serveru a přijímá pouze nový formát balíčku symbolů – `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="b13d9-127">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="b13d9-128">Příjemci balíčku můžou použít symboly publikované do serveru symbolů NuGet.org přidáním `https://symbols.nuget.org/download/symbols` do jejich zdrojů symbolů v aplikaci Visual Studio, které umožňují krokování kódu balíčku v ladicím programu sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b13d9-128">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="b13d9-129">Podrobnosti o tomto procesu najdete v tématu [určení symbolu (PDB) a zdrojových souborů v ladicím programu sady Visual Studio](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017) .</span><span class="sxs-lookup"><span data-stu-id="b13d9-129">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="b13d9-130">Omezení balíčku symbolů Nuget.org</span><span class="sxs-lookup"><span data-stu-id="b13d9-130">Nuget.org symbol package constraints</span></span>

<span data-ttu-id="b13d9-131">Balíčky symbolů podporované v nuget.org mají následující contraints</span><span class="sxs-lookup"><span data-stu-id="b13d9-131">The symbol packages supported on nuget.org have the following contraints</span></span>

- <span data-ttu-id="b13d9-132">Do balíčku symbolů smí být přidána pouze následující přípony souborů.</span><span class="sxs-lookup"><span data-stu-id="b13d9-132">Only the following file extensions are allowed to be added to a symbol package.</span></span> ```.pdb,.nuspec,.xml,.psmdcp,.rels,.p7s```
- <span data-ttu-id="b13d9-133">Na serveru symbolů NuGet se aktuálně podporují jenom spravované [přenosné soubory PDB](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) .</span><span class="sxs-lookup"><span data-stu-id="b13d9-133">Only managed [Portable pdbs](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are currently supported on nuget symbol server.</span></span>
- <span data-ttu-id="b13d9-134">Soubory PDB a přidružené knihovny DLL nupkg musí být sestaveny s kompilátorem v aplikaci Visual Studio verze 15,9 nebo vyšší (viz soubor [PDB kryptografický otisk](https://github.com/dotnet/roslyn/issues/24429)).</span><span class="sxs-lookup"><span data-stu-id="b13d9-134">The pdbs and associated nupkg dlls need to be built with the compiler in Visual Studio version 15.9 or above (see [pdb crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="b13d9-135">Pokud jsou všechny ostatní typy souborů zahrnuté v souboru. snupkg, nebude balíček symbolů Publish on nuget.org úspěšný.</span><span class="sxs-lookup"><span data-stu-id="b13d9-135">The symbol package publish on nuget.org will fail if any other file types are included in the .snupkg.</span></span>

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="b13d9-136">Ověřování a indexování balíčku symbolů</span><span class="sxs-lookup"><span data-stu-id="b13d9-136">Symbol package validation and indexing</span></span>

<span data-ttu-id="b13d9-137">Balíčky symbolů publikované do [NuGet.org](https://www.nuget.org/) prošly několika ověřeními, jako jsou třeba kontroly virů.</span><span class="sxs-lookup"><span data-stu-id="b13d9-137">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, such as virus checks.</span></span>

<span data-ttu-id="b13d9-138">Když balíček úspěšně prošel všemi ověřovacími kontrolami, může chvíli trvat, než se symboly indexují a budou dostupné pro využití ze serverů symbolů NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="b13d9-138">When the package has passed all validation checks, it might take a while for the symbols to index and be available for consumption from the NuGet.org symbol servers.</span></span> <span data-ttu-id="b13d9-139">Pokud balíček neuspěje při ověřování, aktualizuje se stránka s podrobnostmi balíčku pro. nupkg, aby se zobrazila přidružená chyba, a obdržíte také e-mail s upozorněním.</span><span class="sxs-lookup"><span data-stu-id="b13d9-139">If the package fails a validation check, the package details page for the .nupkg will update to display the associated error and you will also receive an email notifying you about it.</span></span>

<span data-ttu-id="b13d9-140">Ověření a indexování balíčku obvykle trvá 15 minut.</span><span class="sxs-lookup"><span data-stu-id="b13d9-140">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="b13d9-141">Pokud publikování balíčku trvá déle, než se čekalo, navštivte [status.NuGet.org](https://status.nuget.org/) a ověřte, jestli NuGet.org má nějaké přerušení.</span><span class="sxs-lookup"><span data-stu-id="b13d9-141">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if nuget.org is experiencing any interruptions.</span></span> <span data-ttu-id="b13d9-142">Pokud jsou všechny systémy funkční a balíček ještě není po celou hodinu publikovaný, přihlaste se k nuget.org a na stránce s podrobnostmi balíčku kontaktujte nás pomocí odkazu podpora kontaktů.</span><span class="sxs-lookup"><span data-stu-id="b13d9-142">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="b13d9-143">Struktura balíčku symbolů</span><span class="sxs-lookup"><span data-stu-id="b13d9-143">Symbol package structure</span></span>

<span data-ttu-id="b13d9-144">Soubor. nupkg by byl přesně stejný, jako v současné době, ale soubor. snupkg má následující vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="b13d9-144">The .nupkg file would be exactly the same as it is today, but the .snupkg file would have the following characteristics:</span></span>

1) <span data-ttu-id="b13d9-145">Přípona. snupkg bude mít stejné ID a verzi jako odpovídající. nupkg.</span><span class="sxs-lookup"><span data-stu-id="b13d9-145">The .snupkg will have the same id and version as the corresponding .nupkg.</span></span>
2) <span data-ttu-id="b13d9-146">Soubor. snupkg bude mít přesnou strukturu složek jako nupkg pro všechny soubory DLL nebo EXE s rozlišením, které místo knihoven DLL/exe, jejich odpovídající soubory PDB bude zahrnuta do stejné hierarchie složek.</span><span class="sxs-lookup"><span data-stu-id="b13d9-146">The .snupkg will have the exact folder structure as the nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="b13d9-147">Soubory a složky s rozšířeními jinými než PDB budou ponechány mimo snupkg.</span><span class="sxs-lookup"><span data-stu-id="b13d9-147">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="b13d9-148">Soubor. nuspec v souboru. snupkg také určí nové PackageType, jak je uvedeno níže.</span><span class="sxs-lookup"><span data-stu-id="b13d9-148">The .nuspec file in the .snupkg will also specify a new PackageType as below.</span></span> <span data-ttu-id="b13d9-149">Mělo by se zadat jenom jeden PackageType.</span><span class="sxs-lookup"><span data-stu-id="b13d9-149">This should the only one PackageType specified.</span></span>

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) <span data-ttu-id="b13d9-150">Pokud se autor rozhodne použít vlastní nuspec k sestavení nupkg a snupkg, měl by mít snupkg stejnou hierarchii složek a souborů, které jsou popsány v 2).</span><span class="sxs-lookup"><span data-stu-id="b13d9-150">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="b13d9-151">```authors```a ```owners``` pole bude vyloučeno z nuspecu snupkg.</span><span class="sxs-lookup"><span data-stu-id="b13d9-151">```authors``` and ```owners``` field will be excluded from the snupkg's nuspec.</span></span>
6) <span data-ttu-id="b13d9-152">Nepoužívejte <license> element.</span><span class="sxs-lookup"><span data-stu-id="b13d9-152">Do not use the <license> element.</span></span> <span data-ttu-id="b13d9-153">A. snupkg se zabývá stejnou licencí jako odpovídající. nupkg.</span><span class="sxs-lookup"><span data-stu-id="b13d9-153">A .snupkg is covered under the same license as the corresponding .nupkg.</span></span>

## <a name="see-also"></a><span data-ttu-id="b13d9-154">Viz také</span><span class="sxs-lookup"><span data-stu-id="b13d9-154">See Also</span></span>

[<span data-ttu-id="b13d9-155">NuGet-Package-Debugging-&-Symbols-Improvements</span><span class="sxs-lookup"><span data-stu-id="b13d9-155">NuGet-Package-Debugging-&-Symbols-Improvements</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)
