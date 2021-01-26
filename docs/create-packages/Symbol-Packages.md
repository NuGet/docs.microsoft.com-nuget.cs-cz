---
title: Vytváření starších balíčků symbolů (. Symbols. nupkg)
description: Vytvoření balíčků NuGet, které obsahují pouze symboly pro podporu ladění dalších balíčků NuGet v aplikaci Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: d9a96986bf80aa15423d7dcee6ea3fe59255252b
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774552"
---
# <a name="creating-legacy-symbol-packages-symbolsnupkg"></a>Vytváření starších balíčků symbolů (. Symbols. nupkg)

> [!Important]
> Nový doporučený formát pro balíčky symbolů je. snupkg. Viz [vytváření balíčků symbolů (. snupkg)](Symbol-Packages-snupkg.md). </br>
> . Symbols. nupkg je stále podporován, ale pouze z důvodu kompatibility.

Kromě vytváření balíčků pro nuget.org nebo jiných zdrojů NuGet podporuje také vytváření přidružených balíčků symbolů, které mohou být publikovány na servery symbolů. Formát balíčku symbolů starší verze,. Symbols. nupkg, lze vložit do úložiště SymbolSource.

Příjemci balíčku pak mohou přidat `https://nuget.smbsrc.net` do svých zdrojů symbolů v aplikaci Visual Studio, které umožňují krokování kódu balíčku v ladicím programu sady Visual Studio. Podrobnosti o tomto procesu najdete v tématu [určení symbolu (PDB) a zdrojových souborů v ladicím programu sady Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) .

## <a name="creating-a-legacy-symbol-package"></a>Vytváření starší verze balíčku symbolů

Chcete-li vytvořit starší verzi balíčku symbolů, postupujte podle těchto konvencí:

- Pojmenujte primární balíček (s vaším kódem) `{identifier}.nupkg` a zahrňte všechny soubory s výjimkou `.pdb` souborů.
- Pojmenujte balíček staršího symbolu `{identifier}.symbols.nupkg` a zahrňte vaše sestavení DLL, `.pdb` soubory, soubory xmldoc a zdrojové soubory (viz následující části).

Oba balíčky lze vytvořit pomocí `-Symbols` Možnosti buď ze `.nuspec` souboru, nebo souboru projektu:

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

Všimněte si, že `pack` vyžaduje mono 4.4.2 na Mac OS X a nefunguje v systémech Linux. Na Macu musíte také v souboru převést cesty Windows `.nuspec` na cesty ve stylu systému UNIX.

## <a name="legacy-symbol-package-structure"></a>Struktura balíčku symbolů starší verze

Balíček starší verze může cílit na více cílových rozhraní stejným způsobem jako balíček knihovny, takže struktura `lib` složky by měla být přesně stejná jako u primárního balíčku, včetně `.pdb` souborů společně s knihovnou DLL.

Například starší balíček symbolů, který cílí na rozhraní .NET 4,0 a Silverlight 4, by měl toto rozložení:

```
\lib
    \net40
        \MyAssembly.dll
        \MyAssembly.pdb
    \sl40
        \MyAssembly.dll
        \MyAssembly.pdb
```

Zdrojové soubory se pak umístí do samostatné speciální složky s názvem `src` , která musí následovat po relativní struktuře zdrojového úložiště. Důvodem je, že soubory PDB obsahuje absolutní cesty ke zdrojovým souborům používaným ke kompilaci vyhovující knihovny DLL a musí být nalezeny během procesu publikování. Základní cestu (předpona společné cesty) lze odložit. Zvažte například knihovnu vytvořenou z těchto souborů:

```
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
```

Kromě ze `lib` složky by starší verze balíčku symbolů musela obsahovat toto rozložení:

```
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
```

## <a name="referring-to-files-in-the-nuspec"></a>Odkazy na soubory v nuspec

Starší verze balíčku symbolů lze vytvořit podle konvencí, ze struktury složek, jak je popsáno v předchozí části, nebo zadáním jejího obsahu v `files` části manifestu. Chcete-li například sestavit balíček uvedený v předchozí části, použijte následující `.nuspec` soubor:

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-legacy-symbol-package"></a>Publikování staršího balíčku symbolů

> [!Important]
> Pokud chcete nabízet balíčky do nuget.org, musíte použít [nuget.exe v 4.9.1 nebo vyšší](https://www.nuget.org/downloads), která implementuje požadované [protokoly NuGet](../api/nuget-protocols.md).

1. Pro usnadnění práce nejdřív uložte klíč rozhraní API pomocí NuGet (viz [publikování balíčku](../nuget-org/publish-a-package.md), který bude platit jak pro NuGet.org, tak pro symbolsource.org, protože symbolsource.org se ověří pomocí NuGet.org a ověří, že jste vlastníkem balíčku.

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. Po publikování primárního balíčku do nuget.org nahrajte starší verzi balíčku symbolů následujícím způsobem, který automaticky použije symbolsource.org jako cíl z důvodu `.symbols` v názvu souboru:

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. Chcete-li publikovat v jiném úložišti symbolů nebo odeslat starší balíček symbolů, který nedodržuje konvence pojmenování, použijte `-Source` možnost:

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. Současně můžete do obou úložišť současně nabízet i balíčky s primárním i symbolem, a to pomocí následujících:

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > Když nuget.exe 4.5.0 nebo novější, balíčky symbolů se automaticky nevloží do symbolsource.org. Balíčky symbolů byste museli nabízet samostatně, jak je vysvětleno v předchozích krocích.
   
V tomto případě bude NuGet publikovat `MyPackage.symbols.nupkg` , pokud je k dispozici, do https://nuget.smbsrc.net/ (adresa URL push pro symbolsource.org) po publikování primárního balíčku do NuGet.org.

## <a name="see-also"></a>Viz také

* [Vytváření balíčků symbolů (. snupkg)](Symbol-Packages-snupkg.md) – nový doporučený formát pro balíčky symbolů
* [Přechod na nový modul SymbolSource](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)
