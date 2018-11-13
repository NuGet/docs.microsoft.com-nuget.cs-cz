---
title: Vytváření balíčků NuGet symbol
description: Jak vytvořit balíčky NuGet, které obsahují pouze symboly v zájmu podpory ladění jiných balíčků NuGet v sadě Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 3321cba9082eb35b53ba693e246db18e5d8e187b
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580256"
---
# <a name="creating-symbol-packages-legacy"></a>Vytváření balíčků symbolů (starší verze)

> [!Important]
> Nové doporučený formát pro balíčky symbolů je .snupkg. Zobrazit [vytváření balíčků symbolů (.snupkg)](Symbol-Packages-snupkg.md). </br>
> . symbols.nupkg je stále podporovány, ale pouze z důvodu kompatibility.

Kromě vytváření balíčků pro nuget.org nebo jiné zdroje NuGet také podporuje vytváření přidružené balíčky symbolů a publikujete je do úložiště SymbolSource.

Poté můžete přidat balíček příjemci `https://nuget.smbsrc.net` k jejich symbol zdroje v sadě Visual Studio, který umožňuje krokování s vnořením do kódu balíček v ladicím programu sady Visual Studio. Zobrazit [zadání symbolu (.pdb) a zdrojových souborů v ladicím programu sady Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) podrobnosti o tomto procesu.

## <a name="creating-a-symbol-package"></a>Vytváří se balíček symbolů

Vytvořte balíček symbolů, postupujte podle těchto konvence:

- Zadejte název primárního balíčku (s vaším kódem) `{identifier}.nupkg` a zahrnout všechny soubory s výjimkou `.pdb` soubory.
- Zadejte název balíčku symbolů `{identifier}.symbols.nupkg` a zahrnout sestavení knihovny DLL, `.pdb` soubory, soubory XMLDOC, zdrojové soubory (viz následující části).

Můžete vytvořit oba balíčky s `-Symbols` možnosti, buď z `.nuspec` soubor nebo soubor projektu:

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

Všimněte si, že `pack` vyžaduje Mono 4.4.2 v Mac OS X a nebude fungovat v systémech Linux. Na počítači Mac, je také nutné převést Windows cest v `.nuspec` soubor do cesty k systému UNIX.

## <a name="symbol-package-structure"></a>Struktura balíčku symbolů

Balíček symbolů můžete cílit na více cílových platforem stejným způsobem, který nemá balíček knihovny, proto struktury `lib` složka by měla být přesně stejný jako primární balíček jen včetně `.pdb` soubory společně s knihovny DLL.

Toto rozložení mít například balíček symbolů, který cílí na rozhraní .NET 4.0 a Silverlight 4:

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

Zdrojové soubory jsou pak umístěné v samostatné speciální složky s názvem `src`, které musí následovat relativní struktury zdrojového úložiště. Je to proto, že soubory PDB obsahovat absolutní cesty ke zdrojovým souborům používá ke kompilaci odpovídající knihovny DLL, a potřebují najít během procesu publikování. Základní cesta (běžnou předponu cesty) může být vynechají. Představte si třeba knihovnu sestaven z těchto souborů:

    C:\Projects
        \MyProject
            \Common
                \MyClass.cs
            \Full
                \Properties
                    \AssemblyInfo.cs
                \MyAssembly.csproj (producing \lib\net40\MyAssembly.dll)
            \Silverlight
                \Properties
                    \AssemblyInfo.cs
                \MySilverlightExtensions.cs
                \MyAssembly.csproj (producing \lib\sl4\MyAssembly.dll)

Kromě `lib` složce balíček symbolů by bylo potřeba obsahovat toto rozložení:

    \src
        \Common
            \MyClass.cs
        \Full
            \Properties
                \AssemblyInfo.cs
        \Silverlight
            \Properties
                \AssemblyInfo.cs
            \MySilverlightExtensions.cs

## <a name="referring-to-files-in-the-nuspec"></a>Odkazování na soubory v souboru nuspec

Balíček symbolů se dají podle konvence z strukturu složek, jak je popsáno v předchozí části, nebo tak, že zadáte jeho obsah `files` manifestu. Například provést sestavení balíčku je znázorněno v předchozí části, pomocí následujících postupů v `.nuspec` souboru:

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-symbol-package"></a>Publikování balíčku symbolů

> [!Important]
> Push balíčků na nuget.org je nutné použít [nuget.exe verze 4.1.0 nebo vyšší](https://www.nuget.org/downloads), který implementuje požadované [NuGet protokoly](../api/nuget-protocols.md).

1. Pro usnadnění práce, uložte svůj klíč rozhraní API s NuGet (viz [publikování balíčku](../create-packages/publish-a-package.md), které bude platit na webech nuget.org a symbolsource.org, protože symbolsource.org zkontroluje s nuget.org a ověřte, zda jste vlastníkem balíčku.

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. Po publikování primární balíčků na nuget.org, push balíček symbolů následujícím způsobem, které budou automaticky používat symbolsource.org jako cíl z důvodu `.symbols` v názvu souboru:

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. Chcete publikovat do úložiště symbolů různých, nebo tak, aby nabízel symbol balíček, který není postupujte z zásady vytváření názvů, použijte `-Source` možnost:

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. Můžete také vložit obě primární a symbol balíčky do obou úložišť ve stejnou dobu následujícím způsobem:

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > S nuget.exe 4.5.0 nebo vyšší, symboly balíčky nejsou automaticky nahrány do symbolsource.org. Je třeba tak, aby nabízel balíčky symboly samostatně, jak je vysvětleno v dalším kroku.
   
V takovém případě budete publikovat NuGet `MyPackage.symbols.nupkg`, pokud jsou k dispozici na https://nuget.smbsrc.net/ (URL nabízených oznámení pro symbolsource.org), po publikuje primární balíčků na nuget.org.

## <a name="see-also"></a>Viz také

[Přechod na nový stroj SymbolSource](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)
