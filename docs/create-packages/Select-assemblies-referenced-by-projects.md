---
title: Vybrat sestavení odkazovaná projekty
description: Zpřístupnit kompilátoru podmnožinu sestavení v balíčku, zatímco všechna sestavení jsou k dispozici za běhu.
author: zivkan
ms.author: zivkan
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: b32075c3f2c06c15c07d36602bdabdaee8b9405a
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427659"
---
# <a name="select-assemblies-referenced-by-projects"></a><span data-ttu-id="14aef-103">Vybrat sestavení odkazovaná projekty</span><span class="sxs-lookup"><span data-stu-id="14aef-103">Select Assemblies Referenced By Projects</span></span>

<span data-ttu-id="14aef-104">Explicitní odkazy na sestavení umožňují použití podmnožiny sestavení pro službu IntelliSense a kompilaci, zatímco všechna sestavení jsou k dispozici za běhu.</span><span class="sxs-lookup"><span data-stu-id="14aef-104">Explicit assembly references allows a subset of assemblies to be used for IntelliSense and compiling, while all assemblies are available at run-time.</span></span> <span data-ttu-id="14aef-105">`PackageReference`a `packages.config` pracovat odlišně, a jako výsledek balíček autoři musí dbát na vytvoření balíčku, které mají být kompatibilní s oběma typy projektu.</span><span class="sxs-lookup"><span data-stu-id="14aef-105">`PackageReference` and `packages.config` work differently, and as a result package authors need to take care to create the package to be compatible with both project types.</span></span>

> [!Note]
> <span data-ttu-id="14aef-106">Explicitní odkazy na sestavení se vztahují k sestavením .NET.</span><span class="sxs-lookup"><span data-stu-id="14aef-106">Explicit assembly references are related to .NET assemblies.</span></span> <span data-ttu-id="14aef-107">Není metoda k distribuci nativní sestavení, které jsou P/Vzbuzované spravované sestavení.</span><span class="sxs-lookup"><span data-stu-id="14aef-107">It is not a method to distribute native assemblies that are P/Invoked by a managed assembly.</span></span>

## <a name="packagereference-support"></a><span data-ttu-id="14aef-108">`PackageReference`Podporu</span><span class="sxs-lookup"><span data-stu-id="14aef-108">`PackageReference` support</span></span>

<span data-ttu-id="14aef-109">Pokud projekt používá balíček s `PackageReference` a `ref\<tfm>\` balíček obsahuje adresář, NuGet klasifikuje tyto `lib\<tfm>\` sestavení jako prostředky v době kompilace, zatímco sestavení jsou klasifikovány jako datové zdroje runtime.</span><span class="sxs-lookup"><span data-stu-id="14aef-109">When a project uses a package with `PackageReference` and the package contains a `ref\<tfm>\` directory, NuGet will classify those assembles as compile-time assets, while the `lib\<tfm>\` assemblies are classified as runtime assets.</span></span> <span data-ttu-id="14aef-110">Sestavení v `ref\<tfm>\` se nepoužívají za běhu.</span><span class="sxs-lookup"><span data-stu-id="14aef-110">Assemblies in `ref\<tfm>\` are not used at runtime.</span></span> <span data-ttu-id="14aef-111">To znamená, že je `ref\<tfm>\` nezbytné pro všechny sestavení `lib\<tfm>\` v `runtime\` mít odpovídající sestavení v jednom nebo příslušném adresáři, jinak dojde k chybám za běhu.</span><span class="sxs-lookup"><span data-stu-id="14aef-111">This means it is necessary for any assembly in `ref\<tfm>\` to have a matching assembly in either `lib\<tfm>\` or a relevant `runtime\` directory, otherwise runtime errors will likely occur.</span></span> <span data-ttu-id="14aef-112">Vzhledem k `ref\<tfm>\` tomu, že sestavení v nejsou používány za běhu, mohou být [sestavení pouze metadata](https://github.com/dotnet/roslyn/blob/master/docs/features/refout.md) ke snížení velikosti balíčku.</span><span class="sxs-lookup"><span data-stu-id="14aef-112">Since assemblies in `ref\<tfm>\` are not used at runtime, they may be [metadata-only assemblies](https://github.com/dotnet/roslyn/blob/master/docs/features/refout.md) to reduce package size.</span></span>

> [!Important]
> <span data-ttu-id="14aef-113">Pokud balíček obsahuje `<references>` nuspec element `packages.config`(používá , viz níže) `ref\<tfm>\`a neobsahuje sestavení v , NuGet `<references>` bude inzerovat sestavení uvedená v nuspec element jako kompilování a runtime prostředky.</span><span class="sxs-lookup"><span data-stu-id="14aef-113">If a package contains the nuspec `<references>` element (used by `packages.config`, see below) and does not contain assemblies in `ref\<tfm>\`, NuGet will advertise the assemblies listed in the nuspec `<references>` element as both the compile and runtime assets.</span></span> <span data-ttu-id="14aef-114">To znamená, že budou existovat výjimky za běhu, když odkazovaná `lib\<tfm>\` sestavení potřebují načíst jakékoli jiné sestavení v adresáři.</span><span class="sxs-lookup"><span data-stu-id="14aef-114">This means there will be runtime exceptions when the referenced assemblies need to load any other assembly in the `lib\<tfm>\` directory.</span></span>

> [!Note]
> <span data-ttu-id="14aef-115">Pokud balíček `runtime\` obsahuje adresář, NuGet nesmí používat `lib\` prostředky v adresáři.</span><span class="sxs-lookup"><span data-stu-id="14aef-115">If the package contains a `runtime\` directory, NuGet may not use the assets in the `lib\` directory.</span></span>

## <a name="packagesconfig-support"></a><span data-ttu-id="14aef-116">`packages.config`Podporu</span><span class="sxs-lookup"><span data-stu-id="14aef-116">`packages.config` support</span></span>

<span data-ttu-id="14aef-117">Projekty, které používají `packages.config` ke správě balíčků NuGet, obvykle přidávají odkazy na všechna sestavení v adresáři. `lib\<tfm>\`</span><span class="sxs-lookup"><span data-stu-id="14aef-117">Projects using `packages.config` to manage NuGet packages normally add references to all assemblies in the `lib\<tfm>\` directory.</span></span> <span data-ttu-id="14aef-118">Adresář `ref\` byl přidán `PackageReference` do podpory, a proto `packages.config`není považován za použití .</span><span class="sxs-lookup"><span data-stu-id="14aef-118">The `ref\` directory was added to support `PackageReference` and therefore isn't considered when using `packages.config`.</span></span> <span data-ttu-id="14aef-119">Chcete-li explicitně nastavit, která `packages.config`sestavení jsou odkazována pro projekty pomocí , balíček musí použít [ `<references>` prvek v souboru nuspec](../reference/nuspec.md#explicit-assembly-references).</span><span class="sxs-lookup"><span data-stu-id="14aef-119">To explicitly set which assemblies are referenced for projects using `packages.config`, the package must use the [`<references>` element in the nuspec file](../reference/nuspec.md#explicit-assembly-references).</span></span> <span data-ttu-id="14aef-120">Příklad:</span><span class="sxs-lookup"><span data-stu-id="14aef-120">For example:</span></span>

```xml
<references>
    <group targetFramework="net45">
        <reference file="MyLibrary.dll" />
    </group>
</references>
```

> [!Note]
> <span data-ttu-id="14aef-121">`packages.config`projekt použít proces s názvem [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/master/documentation/wiki/ResolveAssemblyReference.md) `bin\<configuration>\` ke kopírování sestavení do výstupního adresáře.</span><span class="sxs-lookup"><span data-stu-id="14aef-121">`packages.config` project use a process called [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/master/documentation/wiki/ResolveAssemblyReference.md) to copy assemblies to the `bin\<configuration>\` output directory.</span></span> <span data-ttu-id="14aef-122">Sestavení projektu je zkopírováno, pak systém sestavení vyhledá manifest sestavení pro odkazovaná sestavení, pak zkopíruje tato sestavení a rekurzivně se opakuje pro všechna sestavení.</span><span class="sxs-lookup"><span data-stu-id="14aef-122">Your project's assembly is copied, then the build system looks at the assembly manifest for referenced assemblies, then copies those assemblies and recursively repeats for all assemblies.</span></span> <span data-ttu-id="14aef-123">To znamená, že pokud některé `lib\<tfm>\` sestavení v adresáři nejsou uvedeny v manifestu jiného sestavení jako závislost `Assembly.Load`(pokud je sestavení načteno za běhu pomocí , MEF `bin\<configuration>\` nebo jiného `bin\<tfm>\`rámce vkládání závislostí), nemusí být zkopírováno do výstupního adresáře projektu, přestože je v .</span><span class="sxs-lookup"><span data-stu-id="14aef-123">This means that if any of the assemblies in your `lib\<tfm>\` directory are not listed in any other assembly's manifest as a dependency (if the assembly is loaded at runtime using `Assembly.Load`, MEF or another dependency injection framework), then it may not be copied to your project's `bin\<configuration>\` output directory despite being in `bin\<tfm>\`.</span></span>

## <a name="example"></a><span data-ttu-id="14aef-124">Příklad</span><span class="sxs-lookup"><span data-stu-id="14aef-124">Example</span></span>

<span data-ttu-id="14aef-125">Můj balíček bude obsahovat `MyHelpers.dll` `MyUtilities.dll`tři sestavení , `MyLib.dll`a , které jsou zaměřené na rozhraní .NET Framework 4.7.2.</span><span class="sxs-lookup"><span data-stu-id="14aef-125">My package will contain three assemblies, `MyLib.dll`, `MyHelpers.dll` and `MyUtilities.dll`, which are targeting the .NET Framework 4.7.2.</span></span> <span data-ttu-id="14aef-126">`MyUtilities.dll`obsahuje třídy určené k použití pouze další dvě sestavení, takže nechci, aby tyto třídy k dispozici v IntelliSense nebo v době kompilace na projekty pomocí balíčku.</span><span class="sxs-lookup"><span data-stu-id="14aef-126">`MyUtilities.dll` contains classes intended to be used only by the other two assemblies, so I don't want to make those classes available in IntelliSense or at compile time to projects using my package.</span></span> <span data-ttu-id="14aef-127">Soubor `nuspec` musí obsahovat následující prvky XML:</span><span class="sxs-lookup"><span data-stu-id="14aef-127">My `nuspec` file needs to contain the following XML elements:</span></span>

```xml
<references>
    <group targetFramework="net472">
        <reference file="MyLib.dll" />
        <reference file="MyHelpers.dll" />
    </group>
</references>
```

<span data-ttu-id="14aef-128">a soubory v balíčku budou:</span><span class="sxs-lookup"><span data-stu-id="14aef-128">and the files in the package will be:</span></span>

```text
lib\net472\MyLib.dll
lib\net472\MyHelpers.dll
lib\net472\MyUtilities.dll
ref\net472\MyLib.dll
ref\net472\MyHelpers.dll
```
