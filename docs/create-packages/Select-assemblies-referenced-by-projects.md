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
# <a name="select-assemblies-referenced-by-projects"></a>Vybrat sestavení, na která odkazují projekty

Explicitní odkazy na sestavení umožňují použít podmnožinu sestavení pro technologii IntelliSense a kompilaci, zatímco všechna sestavení jsou k dispozici v době běhu. `PackageReference` a `packages.config` fungují jinak a jako tvůrci balíčku výsledků se musí postarat o vytvoření balíčku tak, aby byl kompatibilní s oběma typy projektů.

> [!Note]
> Explicitní odkazy na sestavení souvisejí s sestaveními .NET. Nejedná se o metodu pro distribuci nativních sestavení, která jsou volána ve spravovaném sestavení.

## <a name="packagereference-support"></a>`PackageReference` pracovníky

Když projekt používá balíček s `PackageReference` a balíček obsahuje `ref\<tfm>\` adresář, nástroj NuGet tyto sestavení klasifikuje jako prostředky v době kompilace, zatímco `lib\<tfm>\` sestavení jsou klasifikována jako prostředky modulu runtime. Sestavení v `ref\<tfm>\` se nepoužívají v době běhu. To znamená, že pro každé sestavení v `ref\<tfm>\` musí mít odpovídající sestavení v buď nebo v `lib\<tfm>\` příslušném `runtime\` adresáři, jinak dojde k chybám za běhu. Vzhledem k tomu, že sestavení v nástroji `ref\<tfm>\` nejsou použita za běhu, mohou být [sestavení pouze metadat](https://github.com/dotnet/roslyn/blob/main/docs/features/refout.md) pro snížení velikosti balíčku.

> [!Important]
> Pokud balíček obsahuje `<references>` element nuspec (používaný v `packages.config` , viz níže) a neobsahuje sestavení v nástroji `ref\<tfm>\` , NuGet bude inzerovat sestavení uvedená v `<references>` elementu nuspec jako prostředky kompilace a modulu runtime. To znamená, že dojde k výjimkám za běhu v případě, že odkazovaná sestavení potřebují načíst jakékoliv jiné sestavení v `lib\<tfm>\` adresáři.

> [!Note]
> Pokud balíček obsahuje `runtime\` adresář, NuGet nemusí použít prostředky v `lib\` adresáři.

## <a name="packagesconfig-support"></a>`packages.config` pracovníky

Projekty `packages.config` , které používají ke správě balíčků NuGet, obvykle přidávají odkazy na všechna sestavení v `lib\<tfm>\` adresáři. `ref\`Adresář se přidal do podpory `PackageReference` , a proto se při použití nebere v úvahu `packages.config` . Chcete-li explicitně nastavit, která sestavení jsou odkazována na projekty pomocí `packages.config` , balíček musí použít [ `<references>` prvek v souboru nuspec](../reference/nuspec.md#explicit-assembly-references). Například:

```xml
<references>
    <group targetFramework="net45">
        <reference file="MyLibrary.dll" />
    </group>
</references>
```

> [!Note]
> `packages.config` projekt kopíruje sestavení do výstupního adresáře pomocí procesu s názvem [ResolveAssemblyReference –](https://github.com/Microsoft/msbuild/blob/main/documentation/wiki/ResolveAssemblyReference.md) `bin\<configuration>\` . Sestavení projektu je zkopírováno, pak systém sestavení vyhledá manifest sestavení pro odkazovaná sestavení a poté zkopíruje tato sestavení a rekurzivně opakuje pro všechna sestavení. To znamená, že pokud některé sestavení v adresáři nejsou `lib\<tfm>\` uvedena v manifestu žádného jiného sestavení jako závislost (Pokud je sestavení načteno za běhu pomocí `Assembly.Load` rozhraní MEF nebo jiné rozhraní pro vkládání závislostí), pak nemusí být zkopírováno do `bin\<configuration>\` výstupního adresáře projektu, i když se nachází v `bin\<tfm>\` .

## <a name="example"></a>Příklad

Balíček bude obsahovat tři sestavení, `MyLib.dll` `MyHelpers.dll` a `MyUtilities.dll` , které cílí na .NET Framework 4.7.2. `MyUtilities.dll` obsahuje třídy, které mají být použity pouze ostatními dvěma sestaveními, takže nechci tyto třídy zpřístupnit v technologii IntelliSense nebo v době kompilace do projektů pomocí balíčku. `nuspec`Soubor musí obsahovat následující prvky XML:

```xml
<references>
    <group targetFramework="net472">
        <reference file="MyLib.dll" />
        <reference file="MyHelpers.dll" />
    </group>
</references>
```

a soubory v balíčku budou:

```text
lib\net472\MyLib.dll
lib\net472\MyHelpers.dll
lib\net472\MyUtilities.dll
ref\net472\MyLib.dll
ref\net472\MyHelpers.dll
```
