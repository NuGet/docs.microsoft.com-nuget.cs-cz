---
title: Publikování symbolů balíčky NuGet pomocí nového formátu balíčku symbol ".snupkg. | Dokumentace Microsoftu
author:
- cristinamanu
- kraigb
ms.author:
- cristinamanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Postup vytvoření symbolu balíčky NuGet (snupkg).
keywords: Symbol balíčky NuGet, balíček NuGet ladění, podpora, balíček symboly ladění, symbol vytváření balíčku NuGet
ms.reviewer:
- anangaur
- karann
ms.openlocfilehash: 43f346dc64ebbc59d02b9c7875b04205d8c5d83a
ms.sourcegitcommit: b6efd4b210d92bf163c67e412ca9a5a018d117f0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/26/2019
ms.locfileid: "56852439"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="6b3c5-104">Vytváření balíčků symbolů (.snupkg)</span><span class="sxs-lookup"><span data-stu-id="6b3c5-104">Creating symbol packages (.snupkg)</span></span>

<span data-ttu-id="6b3c5-105">Balíčky symbolů umožňují ladění vylepšit vaše balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="6b3c5-105">Symbol packages allow you to improve the debugging experience of your NuGet packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6b3c5-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="6b3c5-106">Prerequisites</span></span>

<span data-ttu-id="6b3c5-107">[nuget.exe v4.9.0 nebo vyšší](https://www.nuget.org/downloads) nebo [dotnet.exe v2.2.0 nebo vyšší](https://www.microsoft.com/net/download/dotnet-core/2.2), které implementují požadované [NuGet protokoly](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="6b3c5-107">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet.exe v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="6b3c5-108">Vytváří se balíček symbolů</span><span class="sxs-lookup"><span data-stu-id="6b3c5-108">Creating a symbol package</span></span>

<span data-ttu-id="6b3c5-109">Můžete vytvořit balíček symbolů snupkg pomocí dotnet.exe, NuGet.exe nebo MSBuild.</span><span class="sxs-lookup"><span data-stu-id="6b3c5-109">You can create a snupkg symbol package using dotnet.exe, NuGet.exe, or MSBuild.</span></span> <span data-ttu-id="6b3c5-110">Pokud používáte NuGet.exe, můžete použít následující příkazy k vytvoření souboru .snupkg kromě .nupkg souboru:</span><span class="sxs-lookup"><span data-stu-id="6b3c5-110">If you're using NuGet.exe, you can use the following commands to create a .snupkg file in addition to the .nupkg file:</span></span>

```
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

<span data-ttu-id="6b3c5-111">Pokud používáte dotnet.exe nebo MSBuild, použijte následující kroky k vytvoření souboru .snupkg kromě .nupkg souboru:</span><span class="sxs-lookup"><span data-stu-id="6b3c5-111">If you're using dotnet.exe or MSBuild, use the following steps to create a .snupkg file in addition to the .nupkg file:</span></span>

1. <span data-ttu-id="6b3c5-112">Do souboru .csproj přidejte následující vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="6b3c5-112">Add the following properties to your .csproj file:</span></span>

    ```xml
    <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
    </PropertyGroup>
    ```

1. <span data-ttu-id="6b3c5-113">Váš projekt s aktualizací Service Pack `dotnet pack MyPackage.csproj` nebo `msbuild -t:pack MyPackage.csproj`.</span><span class="sxs-lookup"><span data-stu-id="6b3c5-113">Pack your project with `dotnet pack MyPackage.csproj` or `msbuild -t:pack MyPackage.csproj`.</span></span>

<span data-ttu-id="6b3c5-114">`SymbolPackageFormat` Vlastnost může mít jednu ze dvou hodnot: `symbols.nupkg` (výchozí) nebo `snupkg`.</span><span class="sxs-lookup"><span data-stu-id="6b3c5-114">The `SymbolPackageFormat` property can have one of the two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="6b3c5-115">Pokud `SymbolPackageFormat` vlastnost není zadaný, použije se výchozí `symbols.nupkg` a vytvoří se balíček symbolů starší verze.</span><span class="sxs-lookup"><span data-stu-id="6b3c5-115">If the `SymbolPackageFormat` property is not specified, it defaults to `symbols.nupkg` and a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="6b3c5-116">Starší verze formátu `.symbols.nupkg` je ale pouze z důvodů kompatibility stále podporována (viz [starších verzí balíčků symbolů](Symbol-Packages.md)).</span><span class="sxs-lookup"><span data-stu-id="6b3c5-116">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="6b3c5-117">Server symbolů NuGet.org přijímá pouze nový formát balíček symbolů - `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="6b3c5-117">NuGet.org symbols server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="6b3c5-118">Publikování balíčku symbolů</span><span class="sxs-lookup"><span data-stu-id="6b3c5-118">Publishing a symbol package</span></span>

1. <span data-ttu-id="6b3c5-119">Pro usnadnění práce, uložte svůj klíč rozhraní API s NuGet (viz [publikování balíčku](../create-packages/publish-a-package.md)).</span><span class="sxs-lookup"><span data-stu-id="6b3c5-119">For convenience, first save your API key with NuGet (see [publish a package](../create-packages/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="6b3c5-120">Po publikování vaší primární balíčků na nuget.org, push balíček symbolů následujícím způsobem.</span><span class="sxs-lookup"><span data-stu-id="6b3c5-120">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="6b3c5-121">Můžete také vložit obě primární a symbol balíčky na pomocí následující příkaz.</span><span class="sxs-lookup"><span data-stu-id="6b3c5-121">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="6b3c5-122">.Nupkg a .snupkg soubory musí mít k dispozici v aktuální složce.</span><span class="sxs-lookup"><span data-stu-id="6b3c5-122">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="6b3c5-123">NuGet se publikovat oba balíčky nuget.org. `MyPackage.nupkg` se nejprve publikovat, za nímž následuje `MyPackage.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="6b3c5-123">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="6b3c5-124">NuGet.org symbol server</span><span class="sxs-lookup"><span data-stu-id="6b3c5-124">NuGet.org symbol server</span></span>

<span data-ttu-id="6b3c5-125">NuGet.org podporuje své vlastní úložiště serveru symbolů a přijímá pouze nový formát balíček symbolů - `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="6b3c5-125">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="6b3c5-126">Příjemci balíčku můžete použít symboly publikované na nuget.org symbol server tak, že přidáte `https://symbols.nuget.org/download/symbols` k jejich symbol zdroje v sadě Visual Studio, který umožňuje krokování s vnořením do kódu balíček v ladicím programu sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6b3c5-126">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="6b3c5-127">Zobrazit [zadání symbolu (.pdb) a zdrojových souborů v ladicím programu sady Visual Studio](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017) podrobnosti o tomto procesu.</span><span class="sxs-lookup"><span data-stu-id="6b3c5-127">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="6b3c5-128">Omezení balíček symbolů Nuget.org</span><span class="sxs-lookup"><span data-stu-id="6b3c5-128">Nuget.org symbol package constraints</span></span>

<span data-ttu-id="6b3c5-129">Balíčky symbolů, které jsou podporovány na nuget.org mají následující omezení</span><span class="sxs-lookup"><span data-stu-id="6b3c5-129">The symbol packages supported on nuget.org have the following contraints</span></span>

- <span data-ttu-id="6b3c5-130">Následující přípony souborů můžou přidat do balíčků symbolů.</span><span class="sxs-lookup"><span data-stu-id="6b3c5-130">Only the following file extensions are allowed to be added to a symbol package.</span></span> ```.pdb,.nuspec,.xml,.psmdcp,.rels,.p7s```
- <span data-ttu-id="6b3c5-131">Pouze spravované [souborům Portable PDB](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) jsou aktuálně podporovány na serveru symbolů nuget.</span><span class="sxs-lookup"><span data-stu-id="6b3c5-131">Only managed [Portable pdbs](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are currently supported on nuget symbol server.</span></span>
- <span data-ttu-id="6b3c5-132">Soubory PDB a DLL přidružené nupkg musela být vytvořená s kompilátorem v sadě Visual Studio verzi 15.9 nebo vyšší (viz [kryptografické hodnoty hash souboru pdb](https://github.com/dotnet/roslyn/issues/24429))</span><span class="sxs-lookup"><span data-stu-id="6b3c5-132">The pdbs and associated nupkg dlls need to be built with the compiler in Visual Studio version 15.9 or above (see [pdb crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="6b3c5-133">Publikovat balíček symbolů na nuget.org se nezdaří, pokud jiné typy souborů jsou součástí .snupkg.</span><span class="sxs-lookup"><span data-stu-id="6b3c5-133">The symbol package publish on nuget.org will fail if any other file types are included in the .snupkg.</span></span>

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="6b3c5-134">Ověření balíčku symbolů a indexování</span><span class="sxs-lookup"><span data-stu-id="6b3c5-134">Symbol package validation and indexing</span></span>

<span data-ttu-id="6b3c5-135">Symbol balíčky, které jsou publikovány na [NuGet.org](https://www.nuget.org/) projít několik ověření, jako jsou antivirové kontroly.</span><span class="sxs-lookup"><span data-stu-id="6b3c5-135">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, such as virus checks.</span></span>

<span data-ttu-id="6b3c5-136">Když tento balíček prošel všechny ověřovací kontroly, může trvat nějakou dobu symboly pro indexování a být k dispozici pro použití ze serverů symbolů NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="6b3c5-136">When the package has passed all validation checks, it might take a while for the symbols to index and be available for consumption from the NuGet.org symbol servers.</span></span> <span data-ttu-id="6b3c5-137">Pokud balíček selhání kontroly ověřování, na stránce podrobností balíčku pro .nupkg se aktualizuje a zobrazí související chyby a také obdržíte e-mail s upozorněním můžete o něm.</span><span class="sxs-lookup"><span data-stu-id="6b3c5-137">If the package fails a validation check, the package details page for the .nupkg will update to display the associated error and you will also receive an email notifying you about it.</span></span>

<span data-ttu-id="6b3c5-138">Ověření balíčku a indexování obvykle trvá méně než 15 minut.</span><span class="sxs-lookup"><span data-stu-id="6b3c5-138">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="6b3c5-139">Pokud o publikování balíčku trvá déle, než se očekávalo, navštivte [status.nuget.org](https://status.nuget.org/) ke kontrole, pokud nuget.org dochází k žádné přerušení.</span><span class="sxs-lookup"><span data-stu-id="6b3c5-139">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if nuget.org is experiencing any interruptions.</span></span> <span data-ttu-id="6b3c5-140">Pokud jsou všechny systémy provozní a balíčku nebyla úspěšně publikována do jedné hodiny, přihlaste se prosím na nuget.org a kontaktujte nás přes odkaz na podporu se obraťte se na stránce s podrobnostmi balíčku.</span><span class="sxs-lookup"><span data-stu-id="6b3c5-140">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="6b3c5-141">Struktura balíčku symbolů</span><span class="sxs-lookup"><span data-stu-id="6b3c5-141">Symbol package structure</span></span>

<span data-ttu-id="6b3c5-142">Soubor .nupkg budou naprosto stejné jako dnes je ale soubor .snupkg by mít následující vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="6b3c5-142">The .nupkg file would be exactly the same as it is today, but the .snupkg file would have the following characteristics:</span></span>

1) <span data-ttu-id="6b3c5-143">.snupkg, bude mít jako odpovídající .nupkg stejné id a verzi.</span><span class="sxs-lookup"><span data-stu-id="6b3c5-143">The .snupkg will have the same id and version as the corresponding .nupkg.</span></span>
2) <span data-ttu-id="6b3c5-144">.snupkg bude mít strukturu složek přesné jako soubor nupkg pro soubory DLL nebo EXE s rozlišovat, že namísto knihovny DLL/exe, jejich odpovídající soubory PDB budou zahrnuty ve stejné hierarchii složek.</span><span class="sxs-lookup"><span data-stu-id="6b3c5-144">The .snupkg will have the exact folder structure as the nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="6b3c5-145">Mimo snupkg by zůstaly souborů a složek s příponou než PDB.</span><span class="sxs-lookup"><span data-stu-id="6b3c5-145">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="6b3c5-146">Soubor souboru .nuspec v .snupkg zadejte také nové PackageType jak je uvedeno níže.</span><span class="sxs-lookup"><span data-stu-id="6b3c5-146">The .nuspec file in the .snupkg will also specify a new PackageType as below.</span></span> <span data-ttu-id="6b3c5-147">To by měl pouze jeden PackageType zadán.</span><span class="sxs-lookup"><span data-stu-id="6b3c5-147">This should the only one PackageType specified.</span></span> 
``` 
<packageTypes>
  <packageType name="SymbolsPackage"/>
</packageTypes>
```
4) <span data-ttu-id="6b3c5-148">Pokud autor rozhodne použít vlastní soubor nuspec vytvářet jejich nupkg a snupkg, snupkg by měl mít stejné hierarchii složek a souborů, které jsou podrobně popsané v 2).</span><span class="sxs-lookup"><span data-stu-id="6b3c5-148">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="6b3c5-149">```authors``` a ```owners``` pole budou vyloučeny z snupkg nuspec.</span><span class="sxs-lookup"><span data-stu-id="6b3c5-149">```authors``` and ```owners``` field will be excluded from the snupkg's nuspec.</span></span>

## <a name="see-also"></a><span data-ttu-id="6b3c5-150">Viz také</span><span class="sxs-lookup"><span data-stu-id="6b3c5-150">See Also</span></span>

[<span data-ttu-id="6b3c5-151">NuGet-Package-Debugging-&-Symbols-Improvements</span><span class="sxs-lookup"><span data-stu-id="6b3c5-151">NuGet-Package-Debugging-&-Symbols-Improvements</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)
