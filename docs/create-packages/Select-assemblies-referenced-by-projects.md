---
title: Vyberte sestavení odkazovaných projektů
description: Zpřístupníte podmnožinu sestavení v balíčku kompilátoru, všechna sestavení jsou k dispozici za běhu.
author: zivkan
ms.author: zivkan
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: b32075c3f2c06c15c07d36602bdabdaee8b9405a
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427659"
---
# <a name="select-assemblies-referenced-by-projects"></a><span data-ttu-id="dda30-103">Vyberte sestavení odkazovaných projektů</span><span class="sxs-lookup"><span data-stu-id="dda30-103">Select Assemblies Referenced By Projects</span></span>

<span data-ttu-id="dda30-104">Odkazy na explicitní sestavení umožňuje podmnožinu sestavení má být použit pro technologii IntelliSense a kompilace, všechna sestavení jsou k dispozici v době běhu.</span><span class="sxs-lookup"><span data-stu-id="dda30-104">Explicit assembly references allows a subset of assemblies to be used for IntelliSense and compiling, while all assemblies are available at run-time.</span></span> <span data-ttu-id="dda30-105">`PackageReference` a `packages.config` fungují jinak a díky tomu potřeba starat vytvořit balíček, který má být kompatibilní s oběma typy projektů autory balíčku.</span><span class="sxs-lookup"><span data-stu-id="dda30-105">`PackageReference` and `packages.config` work differently, and as a result package authors need to take care to create the package to be compatible with both project types.</span></span>

> [!Note]
> <span data-ttu-id="dda30-106">Odkazy na explicitní sestavení se vztahují na sestavení .NET.</span><span class="sxs-lookup"><span data-stu-id="dda30-106">Explicit assembly references are related to .NET assemblies.</span></span> <span data-ttu-id="dda30-107">Není metoda distribuovat nativní sestavení, které jsou P/vyvolaná ve spravované sestavení.</span><span class="sxs-lookup"><span data-stu-id="dda30-107">It is not a method to distribute native assemblies that are P/Invoked by a managed assembly.</span></span>

## <a name="packagereference-support"></a><span data-ttu-id="dda30-108">`PackageReference` Podpora</span><span class="sxs-lookup"><span data-stu-id="dda30-108">`PackageReference` support</span></span>

<span data-ttu-id="dda30-109">Když projekt používá balíček s `PackageReference` a balíček obsahuje `ref\<tfm>\` adresáře, bude klasifikovat NuGet ty sestaví jako prostředky v době kompilace, zatímco `lib\<tfm>\` sestavení jsou klasifikovány jako za běhu.</span><span class="sxs-lookup"><span data-stu-id="dda30-109">When a project uses a package with `PackageReference` and the package contains a `ref\<tfm>\` directory, NuGet will classify those assembles as compile-time assets, while the `lib\<tfm>\` assemblies are classified as runtime assets.</span></span> <span data-ttu-id="dda30-110">Sestavení v `ref\<tfm>\` nejsou používány za běhu.</span><span class="sxs-lookup"><span data-stu-id="dda30-110">Assemblies in `ref\<tfm>\` are not used at runtime.</span></span> <span data-ttu-id="dda30-111">To znamená, že je nutné pro libovolné sestavení v `ref\<tfm>\` mít odpovídající sestavení v jednom `lib\<tfm>\` nebo relevantní `runtime\` adresář, v opačném případě modul runtime pravděpodobně dojde k chybám.</span><span class="sxs-lookup"><span data-stu-id="dda30-111">This means it is necessary for any assembly in `ref\<tfm>\` to have a matching assembly in either `lib\<tfm>\` or a relevant `runtime\` directory, otherwise runtime errors will likely occur.</span></span> <span data-ttu-id="dda30-112">Od sestavení v `ref\<tfm>\` nejsou používány za běhu, může být [sestavení obsahující jenom metadata](https://github.com/dotnet/roslyn/blob/master/docs/features/refout.md) snížit velikost balíčku.</span><span class="sxs-lookup"><span data-stu-id="dda30-112">Since assemblies in `ref\<tfm>\` are not used at runtime, they may be [metadata-only assemblies](https://github.com/dotnet/roslyn/blob/master/docs/features/refout.md) to reduce package size.</span></span>

> [!Important]
> <span data-ttu-id="dda30-113">Pokud balíček obsahuje soubor nuspec `<references>` – element (používané `packages.config`, viz níže) a neobsahuje sestavení v `ref\<tfm>\`, NuGet budou prezentovat sestavení, které jsou uvedeny v souboru nuspec `<references>` prvek jako prostředky kompilace i prostředí runtime.</span><span class="sxs-lookup"><span data-stu-id="dda30-113">If a package contains the nuspec `<references>` element (used by `packages.config`, see below) and does not contain assemblies in `ref\<tfm>\`, NuGet will advertise the assemblies listed in the nuspec `<references>` element as both the compile and runtime assets.</span></span> <span data-ttu-id="dda30-114">To znamená, že bude existovat výjimky modulu CLR při muset načíst další sestavení v odkazovaných sestaveních `lib\<tfm>\` adresáře.</span><span class="sxs-lookup"><span data-stu-id="dda30-114">This means there will be runtime exceptions when the referenced assemblies need to load any other assembly in the `lib\<tfm>\` directory.</span></span>

> [!Note]
> <span data-ttu-id="dda30-115">Pokud balíček obsahuje `runtime\` adresáři NuGet nemusejí podporovat použití prostředků v `lib\` adresáře.</span><span class="sxs-lookup"><span data-stu-id="dda30-115">If the package contains a `runtime\` directory, NuGet may not use the assets in the `lib\` directory.</span></span>

## <a name="packagesconfig-support"></a><span data-ttu-id="dda30-116">`packages.config` Podpora</span><span class="sxs-lookup"><span data-stu-id="dda30-116">`packages.config` support</span></span>

<span data-ttu-id="dda30-117">Projekty pomocí `packages.config` ke správě NuGet balíčky obvykle přidá odkazy na všechna sestavení v `lib\<tfm>\` adresáře.</span><span class="sxs-lookup"><span data-stu-id="dda30-117">Projects using `packages.config` to manage NuGet packages normally add references to all assemblies in the `lib\<tfm>\` directory.</span></span> <span data-ttu-id="dda30-118">`ref\` Adresář byl přidán k podpoře `PackageReference` , není proto při použití `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="dda30-118">The `ref\` directory was added to support `PackageReference` and therefore isn't considered when using `packages.config`.</span></span> <span data-ttu-id="dda30-119">Explicitně nastavit, která sestavení jsou odkazovány pro projekty používající `packages.config`, musíte použít balíček [ `<references>` prvku v souboru nuspec](../reference/nuspec.md#explicit-assembly-references).</span><span class="sxs-lookup"><span data-stu-id="dda30-119">To explicitly set which assemblies are referenced for projects using `packages.config`, the package must use the [`<references>` element in the nuspec file](../reference/nuspec.md#explicit-assembly-references).</span></span> <span data-ttu-id="dda30-120">Příklad:</span><span class="sxs-lookup"><span data-stu-id="dda30-120">For example:</span></span>

```xml
<references>
    <group targetFramework="net45">
        <reference file="MyLibrary.dll" />
    </group>
</references>
```

> [!Note]
> <span data-ttu-id="dda30-121">`packages.config` použití projektu proces volá [resolveassemblyreference –](https://github.com/Microsoft/msbuild/blob/master/documentation/wiki/ResolveAssemblyReference.md) zkopírujte sestavení do `bin\<configuration>\` výstupní adresář.</span><span class="sxs-lookup"><span data-stu-id="dda30-121">`packages.config` project use a process called [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/master/documentation/wiki/ResolveAssemblyReference.md) to copy assemblies to the `bin\<configuration>\` output directory.</span></span> <span data-ttu-id="dda30-122">Sestavení vašeho projektu je zkopírován, pak systém sestavení vypadá v manifestu sestavení pro odkazované sestavení a pak zkopíruje tato sestavení a rekurzivně opakuje pro všechna sestavení.</span><span class="sxs-lookup"><span data-stu-id="dda30-122">Your project's assembly is copied, then the build system looks at the assembly manifest for referenced assemblies, then copies those assemblies and recursively repeats for all assemblies.</span></span> <span data-ttu-id="dda30-123">To znamená, že pokud žádná sestavení v vaše `lib\<tfm>\` adresáře nejsou uvedené v jakékoli jiné manifest sestavení jako závislost (Pokud je sestavení načtených v modulu runtime pomocí `Assembly.Load`, MEF nebo jiné rozhraní framework injektáž závislostí), nemusí být zkopírovat do svého projektu `bin\<configuration>\` výstupní adresář navzdory tomu, že v `bin\<tfm>\`.</span><span class="sxs-lookup"><span data-stu-id="dda30-123">This means that if any of the assemblies in your `lib\<tfm>\` directory are not listed in any other assembly's manifest as a dependency (if the assembly is loaded at runtime using `Assembly.Load`, MEF or another dependency injection framework), then it may not be copied to your project's `bin\<configuration>\` output directory despite being in `bin\<tfm>\`.</span></span>

## <a name="example"></a><span data-ttu-id="dda30-124">Příklad</span><span class="sxs-lookup"><span data-stu-id="dda30-124">Example</span></span>

<span data-ttu-id="dda30-125">Tento balíček bude obsahovat tři sestavení `MyLib.dll`, `MyHelpers.dll` a `MyUtilities.dll`, který cílí na rozhraní .NET Framework 4.7.2.</span><span class="sxs-lookup"><span data-stu-id="dda30-125">My package will contain three assemblies, `MyLib.dll`, `MyHelpers.dll` and `MyUtilities.dll`, which are targeting the .NET Framework 4.7.2.</span></span> <span data-ttu-id="dda30-126">`MyUtilities.dll` obsahuje třídy, které mají být používány pouze další dvě sestavení, takže nechci zpřístupnit tyto třídy v technologii IntelliSense nebo v době kompilace projektů s použitím balíčku.</span><span class="sxs-lookup"><span data-stu-id="dda30-126">`MyUtilities.dll` contains classes intended to be used only by the other two assemblies, so I don't want to make those classes available in IntelliSense or at compile time to projects using my package.</span></span> <span data-ttu-id="dda30-127">Moje `nuspec` soubor musí obsahovat následující prvky XML:</span><span class="sxs-lookup"><span data-stu-id="dda30-127">My `nuspec` file needs to contain the following XML elements:</span></span>

```xml
<references>
    <group targetFramework="net472">
        <reference file="MyLib.dll" />
        <reference file="MyHelpers.dll" />
    </group>
</references>
```

<span data-ttu-id="dda30-128">a budou soubory v balíčku:</span><span class="sxs-lookup"><span data-stu-id="dda30-128">and the files in the package will be:</span></span>

```text
lib\net472\MyLib.dll
lib\net472\MyHelpers.dll
lib\net472\MyUtilities.dll
ref\net472\MyLib.dll
ref\net472\MyHelpers.dll
```
