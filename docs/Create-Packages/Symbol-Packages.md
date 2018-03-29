---
title: Postup vytvoření balíčků NuGet symbol | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 09/12/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Jak vytvořit balíčky NuGet, které obsahují pouze symboly pro podporu ladění dalších balíčcích NuGet v sadě Visual Studio.
keywords: Symbol balíčky NuGet, balíček NuGet ladění, podpora ladění, balíček symboly, konvence symbol balíček NuGet
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 6b6ddb0ca8ac5d7589dc5cb6de66ee3aa5faf8b6
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="creating-symbol-packages"></a>Vytváření balíčků – symbol

Kromě vytváření balíčků pro nuget.org nebo jiné zdroje NuGet také podporuje vytváření související symbol balíčky a publikováním do SymbolSource úložiště.

Poté můžete přidat balíček příjemci `https://nuget.smbsrc.net` k jejich symbol zdroje v sadě Visual Studio, což umožňuje zanoříte se do balíčku kódu v ladicím programu sady Visual Studio. V tématu [zadejte symbolu (.pdb) a zdrojových souborů v ladicím programu sady Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) podrobnosti o tomto procesu.

## <a name="creating-a-symbol-package"></a>Vytváření balíčku – symbol

Chcete-li vytvořit balíček symbol, postupujte podle těchto konvence:

- Název primární balíček (pomocí kódu) `{identifier}.nupkg` a zahrnují všechny soubory kromě `.pdb` soubory.
- Zadejte název balíčku symbol `{identifier}.symbols.nupkg` a obsahovat vaše sestavení knihoven DLL, `.pdb` soubory, soubory XMLDOC, zdrojové soubory (viz následující části).

Můžete vytvořit oba balíčky s `-Symbols` možnosti, buď z `.nuspec` soubor nebo soubor projektu:

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

Všimněte si, že `pack` vyžaduje Mono 4.4.2 na Mac OS X a nefunguje v systémech Linux. V systému Mac, je nutné také převést Windows názvy cest v `.nuspec` souboru do cesty formátu UNIX.

## <a name="symbol-package-structure"></a>Struktura balíček – symbol

Symbol balíček, můžete vybrat více cílové rozhraní stejným způsobem, který nemá balíček knihovny, proto struktura `lib` složky by mělo obsahovat přesně stejný jako primární balíček jen včetně `.pdb` soubory spolu s knihovnou DLL.

Toto rozložení mít například symbol balíček, který cílí rozhraní .NET 4.0 a Silverlight 4:

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

Zdrojové soubory jsou pak umístit do samostatné speciální složky s názvem `src`, které musí následovat relativní strukturu zdrojové úložiště. Je to proto, že soubory PDB obsahovat absolutní cesty na zdrojové soubory, které používá ke kompilaci odpovídající DLL a potřebují k nalezen během procesu publikování. Základní cesta (běžné cesta předponu) může být vynechají. Představte si třeba knihovnu sestaven z těchto souborů:

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

Kromě `lib` složky balíčku symbol by bylo potřeba obsahovat toto rozložení:

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

## <a name="referring-to-files-in-the-nuspec"></a>Odkazy na soubory v soubor nuspec

Symbol balíčku se dají vytvářet konvencemi z struktury složek, jak je popsáno v předchozí části, nebo zadáním jeho obsah v `files` oddílu manifest. Například pokud chcete vytvořit balíček uvedené v předchozí části, použít následující `.nuspec` souboru:

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-symbol-package"></a>Publikování balíčku – symbol

> [!Important]
> K nabízení balíčků nuget.org je nutné použít [nuget.exe v4.1.0 nebo vyšší](https://www.nuget.org/downloads), který implementuje požadovaná [NuGet protokoly](../api/nuget-protocols.md).

1. Pro větší pohodlí si nejprve uložit klíč rozhraní API s NuGet (viz [publikování balíčku](../create-packages/publish-a-package.md), které bude platit pro nuget.org a symbolsource.org, protože symbolsource.org zkontroluje s nuget.org ověřit, zda jste vlastníkem balíčku.

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. Po publikování primární balíček nuget.org, push balíček symbol následujícím způsobem, které budou automaticky používat symbolsource.org jako cíl z důvodu `.symbols` v názvu souboru:

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```
> [!Note]
> S nuget.exe 4.5.0 nebo vyšší symboly balíčky nejsou automaticky instaluje do symbolsource.org. Potřebovali byste tak, aby nabízel balíčky symboly samostatně, jak je popsáno v dalším kroku.

1. K publikování do různých symbol úložiště, nebo tak, aby nabízel symbol balíček, který není postupujte podle zásad vytváření názvů, použít `-Source` možnost:

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

1. Můžete také push obě primární a symbolů balíčky do obou úložiště ve stejnou dobu pomocí tohoto vzorce:

    ```cli
    nuget push MyPackage.nupkg
    ```

V takovém případě bude publikovat NuGet `MyPackage.symbols.nupkg`, pokud je k dispozici na https://nuget.smbsrc.net/ (nabízené URL pro symbolsource.org), po jeho publikuje primární balíček do nuget.org.

## <a name="see-also"></a>Viz také

[Přesun do nového modulu SymbolSource](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)
