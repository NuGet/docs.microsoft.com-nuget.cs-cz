---
title: Vytváření starších balíčků symbolů (.symbols.nupkg)
description: Jak vytvořit Balíčky NuGet, které obsahují pouze symboly pro podporu ladění jiných balíčků NuGet v sadě Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 374e9ccfc01cd06508e76529765db3f849342222
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "77476266"
---
# <a name="creating-legacy-symbol-packages-symbolsnupkg"></a>Vytváření starších balíčků symbolů (.symbols.nupkg)

> [!Important]
> Nový doporučený formát pro balíčky symbolů je .snupkg. Viz [Vytváření balíčků symbolů (.snupkg)](Symbol-Packages-snupkg.md). </br>
> .symbols.nupkg je stále podporován, ale pouze z důvodů kompatibility.

Kromě vytváření balíčků pro nuget.org nebo jiných zdrojů, NuGet také podporuje vytváření přidružené symbol balíčky, které mohou být publikovány na servery symbolů. Formát balíčku starších symbolů,.symbols.nupkg, lze zasunout do úložiště SymbolSource.

Příjemci balíčků `https://nuget.smbsrc.net` pak můžete přidat do svých zdrojů symbolů v sadě Visual Studio, což umožňuje krokování do kódu balíčku v ladicím programu Sady Visual Studio. Podrobnosti o tomto [procesu naleznete v tématu Určení symbolu (.pdb) a zdrojových souborů v ladicím programu sady Visual Studio.](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger)

## <a name="creating-a-legacy-symbol-package"></a>Vytvoření balíčku starších symbolů

Chcete-li vytvořit balíček starších symbolů, postupujte podle těchto konvencí:

- Pojmenujte primární balíček `{identifier}.nupkg` (s kódem) `.pdb` a zahrňte všechny soubory kromě souborů.
- Pojmenujte balíček starších `{identifier}.symbols.nupkg` symbolů `.pdb` a zahrňte knihovnu DLL sestavení, soubory, soubory XMLDOC, zdrojové soubory (viz následující části).

Oba balíčky můžete `-Symbols` vytvořit s možností, a to buď ze souboru, `.nuspec` nebo ze souboru projektu:

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

Všimněte `pack` si, že vyžaduje Mono 4.4.2 na Mac OS X a nefunguje na systémech Linux. Na Macu musíte také převést názvy cest Windows v souboru `.nuspec` na cesty ve stylu Unixu.

## <a name="legacy-symbol-package-structure"></a>Struktura balíčku starších symbolů

Balíček starších symbolů může cílit na více cílových architektur stejným `lib` způsobem jako balíček knihovny, takže `.pdb` struktura složky by měla být přesně stejná jako primární balíček, včetně souborů vedle knihovny DLL.

Například balíček starších symbolů, který cílí na rozhraní .NET 4.0 a Silverlight 4, by měl toto rozložení:

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

Zdrojové soubory jsou pak umístěny `src`do samostatné speciální složky s názvem , která musí sledovat relativní strukturu zdrojového úložiště. Důvodem je, že pdbs obsahují absolutní cesty ke zdrojovým souborům používaným ke kompilaci odpovídající dll a je třeba je nalézt během procesu publikování. Základní cestu (společnou předponu cesty) lze odebrat. Zvažte například knihovnu vytvořenou z těchto souborů:

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

Kromě `lib` složky by balíček starších symbolů musel obsahovat toto rozložení:

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

## <a name="referring-to-files-in-the-nuspec"></a>Odkazující na soubory v nuspec

Balíček starší symbol může být sestaven konvencemi, ze struktury složek, jak je popsáno `files` v předchozí části, nebo zadáním jeho obsahu v části manifestu. Chcete-li například vytvořit balíček zobrazený v předchozí `.nuspec` části, použijte v souboru následující:

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-legacy-symbol-package"></a>Publikování balíčku starších symbolů

> [!Important]
> Chcete-li vysunout balíčky nuget.org musíte použít [nuget.exe v4.9.1 nebo vyšší](https://www.nuget.org/downloads), který implementuje požadované [protokoly NuGet](../api/nuget-protocols.md).

1. Pro větší pohodlí nejprve uložte klíč rozhraní API s NuGet (viz [publikování balíčku](../nuget-org/publish-a-package.md), který se bude vztahovat na nuget.org i symbolsource.org, protože symbolsource.org bude kontrolovat u nuget.org ověřit, zda jste vlastníkem balíčku.

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. Po publikování primární balíček nuget.org, push starší symbol balíček takto, který bude `.symbols` automaticky používat symbolsource.org jako cíl z důvodu v názvu souboru:

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. Chcete-li publikovat do jiného úložiště symbolů nebo vysunout balíček starších symbolů, který nedodržuje konvence pojmenování, použijte `-Source` tuto možnost:

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. Balíčky primárních i symbolů můžete také do obou úložišť současně tlačit pomocí následujících položek:

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > U nuget.exe 4.5.0 nebo vyšší, symboly balíčky nejsou automaticky posunuty do symbolsource.org. Balíčky symbolů byste museli stlačovat samostatně, jak je vysvětleno v předchozích krocích.
   
V tomto případě NuGet `MyPackage.symbols.nupkg`publikuje , https://nuget.smbsrc.net/ pokud je k dispozici, do (nabízená adresa URL pro symbolsource.org) poté, co publikuje primární balíček nuget.org.

## <a name="see-also"></a>Viz také

* [Vytváření balíčků symbolů (.snupkg)](Symbol-Packages-snupkg.md) - Nový doporučený formát pro balíčky symbolů
* [Přechod na nový modul SymbolSource](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)
