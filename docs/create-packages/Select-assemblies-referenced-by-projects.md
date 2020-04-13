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
# <a name="select-assemblies-referenced-by-projects"></a>Vybrat sestavení odkazovaná projekty

Explicitní odkazy na sestavení umožňují použití podmnožiny sestavení pro službu IntelliSense a kompilaci, zatímco všechna sestavení jsou k dispozici za běhu. `PackageReference`a `packages.config` pracovat odlišně, a jako výsledek balíček autoři musí dbát na vytvoření balíčku, které mají být kompatibilní s oběma typy projektu.

> [!Note]
> Explicitní odkazy na sestavení se vztahují k sestavením .NET. Není metoda k distribuci nativní sestavení, které jsou P/Vzbuzované spravované sestavení.

## <a name="packagereference-support"></a>`PackageReference`Podporu

Pokud projekt používá balíček s `PackageReference` a `ref\<tfm>\` balíček obsahuje adresář, NuGet klasifikuje tyto `lib\<tfm>\` sestavení jako prostředky v době kompilace, zatímco sestavení jsou klasifikovány jako datové zdroje runtime. Sestavení v `ref\<tfm>\` se nepoužívají za běhu. To znamená, že je `ref\<tfm>\` nezbytné pro všechny sestavení `lib\<tfm>\` v `runtime\` mít odpovídající sestavení v jednom nebo příslušném adresáři, jinak dojde k chybám za běhu. Vzhledem k `ref\<tfm>\` tomu, že sestavení v nejsou používány za běhu, mohou být [sestavení pouze metadata](https://github.com/dotnet/roslyn/blob/master/docs/features/refout.md) ke snížení velikosti balíčku.

> [!Important]
> Pokud balíček obsahuje `<references>` nuspec element `packages.config`(používá , viz níže) `ref\<tfm>\`a neobsahuje sestavení v , NuGet `<references>` bude inzerovat sestavení uvedená v nuspec element jako kompilování a runtime prostředky. To znamená, že budou existovat výjimky za běhu, když odkazovaná `lib\<tfm>\` sestavení potřebují načíst jakékoli jiné sestavení v adresáři.

> [!Note]
> Pokud balíček `runtime\` obsahuje adresář, NuGet nesmí používat `lib\` prostředky v adresáři.

## <a name="packagesconfig-support"></a>`packages.config`Podporu

Projekty, které používají `packages.config` ke správě balíčků NuGet, obvykle přidávají odkazy na všechna sestavení v adresáři. `lib\<tfm>\` Adresář `ref\` byl přidán `PackageReference` do podpory, a proto `packages.config`není považován za použití . Chcete-li explicitně nastavit, která `packages.config`sestavení jsou odkazována pro projekty pomocí , balíček musí použít [ `<references>` prvek v souboru nuspec](../reference/nuspec.md#explicit-assembly-references). Příklad:

```xml
<references>
    <group targetFramework="net45">
        <reference file="MyLibrary.dll" />
    </group>
</references>
```

> [!Note]
> `packages.config`projekt použít proces s názvem [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/master/documentation/wiki/ResolveAssemblyReference.md) `bin\<configuration>\` ke kopírování sestavení do výstupního adresáře. Sestavení projektu je zkopírováno, pak systém sestavení vyhledá manifest sestavení pro odkazovaná sestavení, pak zkopíruje tato sestavení a rekurzivně se opakuje pro všechna sestavení. To znamená, že pokud některé `lib\<tfm>\` sestavení v adresáři nejsou uvedeny v manifestu jiného sestavení jako závislost `Assembly.Load`(pokud je sestavení načteno za běhu pomocí , MEF `bin\<configuration>\` nebo jiného `bin\<tfm>\`rámce vkládání závislostí), nemusí být zkopírováno do výstupního adresáře projektu, přestože je v .

## <a name="example"></a>Příklad

Můj balíček bude obsahovat `MyHelpers.dll` `MyUtilities.dll`tři sestavení , `MyLib.dll`a , které jsou zaměřené na rozhraní .NET Framework 4.7.2. `MyUtilities.dll`obsahuje třídy určené k použití pouze další dvě sestavení, takže nechci, aby tyto třídy k dispozici v IntelliSense nebo v době kompilace na projekty pomocí balíčku. Soubor `nuspec` musí obsahovat následující prvky XML:

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
