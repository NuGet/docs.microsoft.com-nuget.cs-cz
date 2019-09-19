---
title: Jak publikovat balíčky symbolů NuGet pomocí nového formátu balíčku symbolů '. snupkg ' | Microsoft Docs
author: cristinamanu
ms.author: cristinamanu
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Jak vytvořit balíčky symbolů NuGet (snupkg).
keywords: Balíčky symbolů NuGet, ladění balíčku NuGet, podpora ladění NuGet, symboly balíčků, konvence balíčků symbolů
ms.reviewer:
- anangaur
- karann
ms.openlocfilehash: 5546881dbf7577eb289a28b35bc2c0e7dc5cac40
ms.sourcegitcommit: 1eda83ab537c86cc27316e7bc67f95a358766e63
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/18/2019
ms.locfileid: "71094113"
---
# <a name="creating-symbol-packages-snupkg"></a>Vytváření balíčků symbolů (. snupkg)

Balíčky symbolů umožňují zlepšit možnosti ladění balíčků NuGet.

## <a name="prerequisites"></a>Požadavky

[NuGet. exe v 4.9.0 nebo novější](https://www.nuget.org/downloads) nebo [dotnet. exe v 2.2.0 nebo vyšší](https://www.microsoft.com/net/download/dotnet-core/2.2), které implementují požadované [protokoly NuGet](../api/nuget-protocols.md).

## <a name="creating-a-symbol-package"></a>Vytvoření balíčku symbolů

Pokud používáte dotnet. exe nebo MSBuild, je třeba nastavit `IncludeSymbols` vlastnosti a a `SymbolPackageFormat` vytvořit soubor. snupkg společně se souborem. nupkg.

* Přidejte do souboru. csproj následující vlastnosti:

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols> 
      <SymbolPackageFormat>snupkg</SymbolPackageFormat> 
   </PropertyGroup>
   ```

* Nebo zadejte tyto vlastnosti na příkazovém řádku:

     ```cli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  or

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

Pokud používáte NuGet. exe, můžete k vytvoření souboru. snupkg spolu s souborem. nupkg použít následující příkazy:

```
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

Vlastnost může mít jednu ze dvou hodnot: `symbols.nupkg` (výchozí) nebo `snupkg`. [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) Pokud tato vlastnost není zadána, bude vytvořen starší balíček symbolů.

> [!Note]
> Starší verze formátu `.symbols.nupkg` jsou stále podporovány, ale pouze z důvodů kompatibility (viz [starší balíčky symbolů](Symbol-Packages.md)). Server symbolů NuGet. org přijímá pouze nový formát balíčku symbolů – `.snupkg`.

## <a name="publishing-a-symbol-package"></a>Publikování balíčku symbolů

1. Pro usnadnění práce nejdřív uložte klíč rozhraní API pomocí NuGet (viz [publikování balíčku](../nuget-org/publish-a-package.md)).

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. Po publikování primárního balíčku na nuget.org vložte balíček symbolů následujícím způsobem.

    ```cli
    nuget push MyPackage.snupkg
    ```

1. Pomocí níže uvedeného příkazu můžete zároveň současně nabízet jak primární, tak i balíčky symbolů. V aktuální složce musí být přítomné soubory. nupkg a. snupkg.

    ```cli
    nuget push MyPackage.nupkg
    ```

NuGet bude publikovat oba balíčky do nuget.org. bude Publikováno jako první, `MyPackage.snupkg`následované. `MyPackage.nupkg`

> [!Note]
> Pokud se balíček symbolů nepublikuje, ověřte, že jste nakonfigurovali zdroj NuGet.org `https://api.nuget.org/v3/index.json`jako. Publikování balíčku symbolů je podporované jenom [rozhraním API NuGet V3](../api/overview.md#versioning).

## <a name="nugetorg-symbol-server"></a>NuGet.org symbol server

NuGet.org podporuje vlastní úložiště symbolů serveru a přijímá pouze nový formát balíčku symbolů – `.snupkg`. Příjemci balíčku můžou použít symboly publikované do serveru symbolů NuGet.org přidáním `https://symbols.nuget.org/download/symbols` do jejich zdrojů symbolů v aplikaci Visual Studio, které umožňují krokování kódu balíčku v ladicím programu sady Visual Studio. Podrobnosti o tomto procesu najdete v tématu [určení symbolu (PDB) a zdrojových souborů v ladicím programu sady Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md) .

### <a name="nugetorg-symbol-package-constraints"></a>Omezení balíčku symbolů NuGet.org

NuGet.org má následující omezení pro balíčky symbolů:

- V balíčcích symbolů jsou povoleny pouze následující přípony souborů: `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`,`.p7s`
- Na serveru se symbolem NuGet. org jsou podporované jenom spravované [přenosné soubory PDB](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) .
- Soubory PDB a jejich přidružené knihovny DLL nupkg musí být sestaveny s kompilátorem v aplikaci Visual Studio verze 15,9 nebo vyšší (viz [PDB kryptografický otisk](https://github.com/dotnet/roslyn/issues/24429)).

Balíčky symbolů publikované do NuGet.org selžou, pokud tato omezení nebudou splněna. 

### <a name="symbol-package-validation-and-indexing"></a>Ověřování a indexování balíčku symbolů

Balíčky symbolů publikované do [NuGet.org](https://www.nuget.org/) prošly několika ověřeními, včetně kontroly malwaru. Pokud balíček selže, zobrazí se na stránce Podrobnosti o jeho balíčku chybová zpráva. Kromě toho vlastníci balíčku obdrží e-mail s pokyny, jak opravit zjištěné problémy.

Když balíček symbolů předává všechna ověření, symboly budou indexovány pomocí serverů se symboly NuGet. org. Po indexování bude symbol dostupný pro spotřebu ze serverů symbolů NuGet.org.

Ověření a indexování balíčku obvykle trvá 15 minut. Pokud publikování balíčku trvá déle, než se čekalo, navštivte [status.NuGet.org](https://status.nuget.org/) a ověřte, jestli NuGet.org má nějaké přerušení. Pokud jsou všechny systémy funkční a balíček ještě není po celou hodinu publikovaný, přihlaste se k nuget.org a na stránce s podrobnostmi balíčku kontaktujte nás pomocí odkazu podpora kontaktů.

## <a name="symbol-package-structure"></a>Struktura balíčku symbolů

Soubor. nupkg by byl přesně stejný, jako v současné době, ale soubor. snupkg má následující vlastnosti:

1) Přípona. snupkg bude mít stejné ID a verzi jako odpovídající. nupkg.
2) Soubor. snupkg bude mít přesnou strukturu složek jako nupkg pro všechny soubory DLL nebo EXE s rozlišením, které místo knihoven DLL/exe, jejich odpovídající soubory PDB bude zahrnuta do stejné hierarchie složek. Soubory a složky s rozšířeními jinými než PDB budou ponechány mimo snupkg.
3) Soubor. nuspec v souboru. snupkg také určí nové PackageType, jak je uvedeno níže. Mělo by se zadat jenom jeden PackageType.

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) Pokud se autor rozhodne použít vlastní nuspec k sestavení nupkg a snupkg, měl by mít snupkg stejnou hierarchii složek a souborů, které jsou popsány v 2).
5) ```authors```a ```owners``` pole bude vyloučeno z nuspecu snupkg.
6) Nepoužívejte ```<license>``` element. A. snupkg se zabývá stejnou licencí jako odpovídající. nupkg.

## <a name="see-also"></a>Viz také

Zvažte použití odkazu na zdroj pro povolení ladění zdrojového kódu v sestaveních .NET. Další informace najdete v [pokynech ke zdrojovému propojení](/dotnet/standard/library-guidance/sourcelink.md).

Další informace o balíčcích symbolů najdete v tématu [Ladění balíčků NuGet &ch symbolů vylepšení](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) návrhu.
