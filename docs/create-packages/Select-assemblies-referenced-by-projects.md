---
title: Vybrat sestavení, na která odkazují projekty
description: Vytvořte podmnožinu sestavení v balíčku k dispozici pro kompilátor, zatímco všechna sestavení jsou k dispozici za běhu.
author: zivkan
ms.author: zivkan
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: b2202946d0060e09828250d240f931044d1bf485
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859028"
---
# <a name="select-assemblies-referenced-by-projects"></a><span data-ttu-id="97b83-103">Vybrat sestavení, na která odkazují projekty</span><span class="sxs-lookup"><span data-stu-id="97b83-103">Select Assemblies Referenced By Projects</span></span>

<span data-ttu-id="97b83-104">Explicitní odkazy na sestavení umožňují použít podmnožinu sestavení pro technologii IntelliSense a kompilaci, zatímco všechna sestavení jsou k dispozici v době běhu.</span><span class="sxs-lookup"><span data-stu-id="97b83-104">Explicit assembly references allows a subset of assemblies to be used for IntelliSense and compiling, while all assemblies are available at run-time.</span></span> <span data-ttu-id="97b83-105">`PackageReference` a `packages.config` fungují jinak a jako tvůrci balíčku výsledků se musí postarat o vytvoření balíčku tak, aby byl kompatibilní s oběma typy projektů.</span><span class="sxs-lookup"><span data-stu-id="97b83-105">`PackageReference` and `packages.config` work differently, and as a result package authors need to take care to create the package to be compatible with both project types.</span></span>

> [!Note]
> <span data-ttu-id="97b83-106">Explicitní odkazy na sestavení souvisejí s sestaveními .NET.</span><span class="sxs-lookup"><span data-stu-id="97b83-106">Explicit assembly references are related to .NET assemblies.</span></span> <span data-ttu-id="97b83-107">Nejedná se o metodu pro distribuci nativních sestavení, která jsou volána ve spravovaném sestavení.</span><span class="sxs-lookup"><span data-stu-id="97b83-107">It is not a method to distribute native assemblies that are P/Invoked by a managed assembly.</span></span>

## <a name="packagereference-support"></a><span data-ttu-id="97b83-108">`PackageReference` pracovníky</span><span class="sxs-lookup"><span data-stu-id="97b83-108">`PackageReference` support</span></span>

<span data-ttu-id="97b83-109">Když projekt používá balíček s `PackageReference` a balíček obsahuje `ref\<tfm>\` adresář, nástroj NuGet tyto sestavení klasifikuje jako prostředky v době kompilace, zatímco `lib\<tfm>\` sestavení jsou klasifikována jako prostředky modulu runtime.</span><span class="sxs-lookup"><span data-stu-id="97b83-109">When a project uses a package with `PackageReference` and the package contains a `ref\<tfm>\` directory, NuGet will classify those assembles as compile-time assets, while the `lib\<tfm>\` assemblies are classified as runtime assets.</span></span> <span data-ttu-id="97b83-110">Sestavení v `ref\<tfm>\` se nepoužívají v době běhu.</span><span class="sxs-lookup"><span data-stu-id="97b83-110">Assemblies in `ref\<tfm>\` are not used at runtime.</span></span> <span data-ttu-id="97b83-111">To znamená, že pro každé sestavení v `ref\<tfm>\` musí mít odpovídající sestavení v buď nebo v `lib\<tfm>\` příslušném `runtime\` adresáři, jinak dojde k chybám za běhu.</span><span class="sxs-lookup"><span data-stu-id="97b83-111">This means it is necessary for any assembly in `ref\<tfm>\` to have a matching assembly in either `lib\<tfm>\` or a relevant `runtime\` directory, otherwise runtime errors will likely occur.</span></span> <span data-ttu-id="97b83-112">Vzhledem k tomu, že sestavení v nástroji `ref\<tfm>\` nejsou použita za běhu, mohou být [sestavení pouze metadat](https://github.com/dotnet/roslyn/blob/main/docs/features/refout.md) pro snížení velikosti balíčku.</span><span class="sxs-lookup"><span data-stu-id="97b83-112">Since assemblies in `ref\<tfm>\` are not used at runtime, they may be [metadata-only assemblies](https://github.com/dotnet/roslyn/blob/main/docs/features/refout.md) to reduce package size.</span></span>

> [!Important]
> <span data-ttu-id="97b83-113">Pokud balíček obsahuje `<references>` element nuspec (používaný v `packages.config` , viz níže) a neobsahuje sestavení v nástroji `ref\<tfm>\` , NuGet bude inzerovat sestavení uvedená v `<references>` elementu nuspec jako prostředky kompilace a modulu runtime.</span><span class="sxs-lookup"><span data-stu-id="97b83-113">If a package contains the nuspec `<references>` element (used by `packages.config`, see below) and does not contain assemblies in `ref\<tfm>\`, NuGet will advertise the assemblies listed in the nuspec `<references>` element as both the compile and runtime assets.</span></span> <span data-ttu-id="97b83-114">To znamená, že dojde k výjimkám za běhu v případě, že odkazovaná sestavení potřebují načíst jakékoliv jiné sestavení v `lib\<tfm>\` adresáři.</span><span class="sxs-lookup"><span data-stu-id="97b83-114">This means there will be runtime exceptions when the referenced assemblies need to load any other assembly in the `lib\<tfm>\` directory.</span></span>

> [!Note]
> <span data-ttu-id="97b83-115">Pokud balíček obsahuje `runtime\` adresář, NuGet nemusí použít prostředky v `lib\` adresáři.</span><span class="sxs-lookup"><span data-stu-id="97b83-115">If the package contains a `runtime\` directory, NuGet may not use the assets in the `lib\` directory.</span></span>

## <a name="packagesconfig-support"></a><span data-ttu-id="97b83-116">`packages.config` pracovníky</span><span class="sxs-lookup"><span data-stu-id="97b83-116">`packages.config` support</span></span>

<span data-ttu-id="97b83-117">Projekty `packages.config` , které používají ke správě balíčků NuGet, obvykle přidávají odkazy na všechna sestavení v `lib\<tfm>\` adresáři.</span><span class="sxs-lookup"><span data-stu-id="97b83-117">Projects using `packages.config` to manage NuGet packages normally add references to all assemblies in the `lib\<tfm>\` directory.</span></span> <span data-ttu-id="97b83-118">`ref\`Adresář se přidal do podpory `PackageReference` , a proto se při použití nebere v úvahu `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="97b83-118">The `ref\` directory was added to support `PackageReference` and therefore isn't considered when using `packages.config`.</span></span> <span data-ttu-id="97b83-119">Chcete-li explicitně nastavit, která sestavení jsou odkazována na projekty pomocí `packages.config` , balíček musí použít [ `<references>` prvek v souboru nuspec](../reference/nuspec.md#explicit-assembly-references).</span><span class="sxs-lookup"><span data-stu-id="97b83-119">To explicitly set which assemblies are referenced for projects using `packages.config`, the package must use the [`<references>` element in the nuspec file](../reference/nuspec.md#explicit-assembly-references).</span></span> <span data-ttu-id="97b83-120">Například:</span><span class="sxs-lookup"><span data-stu-id="97b83-120">For example:</span></span>

```xml
<references>
    <group targetFramework="net45">
        <reference file="MyLibrary.dll" />
    </group>
</references>
```

> [!Note]
> <span data-ttu-id="97b83-121">`packages.config` projekt kopíruje sestavení do výstupního adresáře pomocí procesu s názvem [ResolveAssemblyReference –](https://github.com/Microsoft/msbuild/blob/main/documentation/wiki/ResolveAssemblyReference.md) `bin\<configuration>\` .</span><span class="sxs-lookup"><span data-stu-id="97b83-121">`packages.config` project use a process called [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/main/documentation/wiki/ResolveAssemblyReference.md) to copy assemblies to the `bin\<configuration>\` output directory.</span></span> <span data-ttu-id="97b83-122">Sestavení projektu je zkopírováno, pak systém sestavení vyhledá manifest sestavení pro odkazovaná sestavení a poté zkopíruje tato sestavení a rekurzivně opakuje pro všechna sestavení.</span><span class="sxs-lookup"><span data-stu-id="97b83-122">Your project's assembly is copied, then the build system looks at the assembly manifest for referenced assemblies, then copies those assemblies and recursively repeats for all assemblies.</span></span> <span data-ttu-id="97b83-123">To znamená, že pokud některé sestavení v adresáři nejsou `lib\<tfm>\` uvedena v manifestu žádného jiného sestavení jako závislost (Pokud je sestavení načteno za běhu pomocí `Assembly.Load` rozhraní MEF nebo jiné rozhraní pro vkládání závislostí), pak nemusí být zkopírováno do `bin\<configuration>\` výstupního adresáře projektu, i když se nachází v `bin\<tfm>\` .</span><span class="sxs-lookup"><span data-stu-id="97b83-123">This means that if any of the assemblies in your `lib\<tfm>\` directory are not listed in any other assembly's manifest as a dependency (if the assembly is loaded at runtime using `Assembly.Load`, MEF or another dependency injection framework), then it may not be copied to your project's `bin\<configuration>\` output directory despite being in `bin\<tfm>\`.</span></span>

## <a name="example"></a><span data-ttu-id="97b83-124">Příklad</span><span class="sxs-lookup"><span data-stu-id="97b83-124">Example</span></span>

<span data-ttu-id="97b83-125">Balíček bude obsahovat tři sestavení, `MyLib.dll` `MyHelpers.dll` a `MyUtilities.dll` , které cílí na .NET Framework 4.7.2.</span><span class="sxs-lookup"><span data-stu-id="97b83-125">My package will contain three assemblies, `MyLib.dll`, `MyHelpers.dll` and `MyUtilities.dll`, which are targeting the .NET Framework 4.7.2.</span></span> <span data-ttu-id="97b83-126">`MyUtilities.dll` obsahuje třídy, které mají být použity pouze ostatními dvěma sestaveními, takže nechci tyto třídy zpřístupnit v technologii IntelliSense nebo v době kompilace do projektů pomocí balíčku.</span><span class="sxs-lookup"><span data-stu-id="97b83-126">`MyUtilities.dll` contains classes intended to be used only by the other two assemblies, so I don't want to make those classes available in IntelliSense or at compile time to projects using my package.</span></span> <span data-ttu-id="97b83-127">`nuspec`Soubor musí obsahovat následující prvky XML:</span><span class="sxs-lookup"><span data-stu-id="97b83-127">My `nuspec` file needs to contain the following XML elements:</span></span>

```xml
<references>
    <group targetFramework="net472">
        <reference file="MyLib.dll" />
        <reference file="MyHelpers.dll" />
    </group>
</references>
```

<span data-ttu-id="97b83-128">a soubory v balíčku budou:</span><span class="sxs-lookup"><span data-stu-id="97b83-128">and the files in the package will be:</span></span>

```text
lib\net472\MyLib.dll
lib\net472\MyHelpers.dll
lib\net472\MyUtilities.dll
ref\net472\MyLib.dll
ref\net472\MyHelpers.dll
```
