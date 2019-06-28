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
# <a name="select-assemblies-referenced-by-projects"></a>Vyberte sestavení odkazovaných projektů

Odkazy na explicitní sestavení umožňuje podmnožinu sestavení má být použit pro technologii IntelliSense a kompilace, všechna sestavení jsou k dispozici v době běhu. `PackageReference` a `packages.config` fungují jinak a díky tomu potřeba starat vytvořit balíček, který má být kompatibilní s oběma typy projektů autory balíčku.

> [!Note]
> Odkazy na explicitní sestavení se vztahují na sestavení .NET. Není metoda distribuovat nativní sestavení, které jsou P/vyvolaná ve spravované sestavení.

## <a name="packagereference-support"></a>`PackageReference` Podpora

Když projekt používá balíček s `PackageReference` a balíček obsahuje `ref\<tfm>\` adresáře, bude klasifikovat NuGet ty sestaví jako prostředky v době kompilace, zatímco `lib\<tfm>\` sestavení jsou klasifikovány jako za běhu. Sestavení v `ref\<tfm>\` nejsou používány za běhu. To znamená, že je nutné pro libovolné sestavení v `ref\<tfm>\` mít odpovídající sestavení v jednom `lib\<tfm>\` nebo relevantní `runtime\` adresář, v opačném případě modul runtime pravděpodobně dojde k chybám. Od sestavení v `ref\<tfm>\` nejsou používány za běhu, může být [sestavení obsahující jenom metadata](https://github.com/dotnet/roslyn/blob/master/docs/features/refout.md) snížit velikost balíčku.

> [!Important]
> Pokud balíček obsahuje soubor nuspec `<references>` – element (používané `packages.config`, viz níže) a neobsahuje sestavení v `ref\<tfm>\`, NuGet budou prezentovat sestavení, které jsou uvedeny v souboru nuspec `<references>` prvek jako prostředky kompilace i prostředí runtime. To znamená, že bude existovat výjimky modulu CLR při muset načíst další sestavení v odkazovaných sestaveních `lib\<tfm>\` adresáře.

> [!Note]
> Pokud balíček obsahuje `runtime\` adresáři NuGet nemusejí podporovat použití prostředků v `lib\` adresáře.

## <a name="packagesconfig-support"></a>`packages.config` Podpora

Projekty pomocí `packages.config` ke správě NuGet balíčky obvykle přidá odkazy na všechna sestavení v `lib\<tfm>\` adresáře. `ref\` Adresář byl přidán k podpoře `PackageReference` , není proto při použití `packages.config`. Explicitně nastavit, která sestavení jsou odkazovány pro projekty používající `packages.config`, musíte použít balíček [ `<references>` prvku v souboru nuspec](../reference/nuspec.md#explicit-assembly-references). Příklad:

```xml
<references>
    <group targetFramework="net45">
        <reference file="MyLibrary.dll" />
    </group>
</references>
```

> [!Note]
> `packages.config` použití projektu proces volá [resolveassemblyreference –](https://github.com/Microsoft/msbuild/blob/master/documentation/wiki/ResolveAssemblyReference.md) zkopírujte sestavení do `bin\<configuration>\` výstupní adresář. Sestavení vašeho projektu je zkopírován, pak systém sestavení vypadá v manifestu sestavení pro odkazované sestavení a pak zkopíruje tato sestavení a rekurzivně opakuje pro všechna sestavení. To znamená, že pokud žádná sestavení v vaše `lib\<tfm>\` adresáře nejsou uvedené v jakékoli jiné manifest sestavení jako závislost (Pokud je sestavení načtených v modulu runtime pomocí `Assembly.Load`, MEF nebo jiné rozhraní framework injektáž závislostí), nemusí být zkopírovat do svého projektu `bin\<configuration>\` výstupní adresář navzdory tomu, že v `bin\<tfm>\`.

## <a name="example"></a>Příklad

Tento balíček bude obsahovat tři sestavení `MyLib.dll`, `MyHelpers.dll` a `MyUtilities.dll`, který cílí na rozhraní .NET Framework 4.7.2. `MyUtilities.dll` obsahuje třídy, které mají být používány pouze další dvě sestavení, takže nechci zpřístupnit tyto třídy v technologii IntelliSense nebo v době kompilace projektů s použitím balíčku. Moje `nuspec` soubor musí obsahovat následující prvky XML:

```xml
<references>
    <group targetFramework="net472">
        <reference file="MyLib.dll" />
        <reference file="MyHelpers.dll" />
    </group>
</references>
```

a budou soubory v balíčku:

```text
lib\net472\MyLib.dll
lib\net472\MyHelpers.dll
lib\net472\MyUtilities.dll
ref\net472\MyLib.dll
ref\net472\MyHelpers.dll
```
