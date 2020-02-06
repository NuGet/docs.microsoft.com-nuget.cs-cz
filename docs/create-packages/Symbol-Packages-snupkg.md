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
ms.openlocfilehash: 839c38ec165372bab9b93dec25e5c8e8e9439bfa
ms.sourcegitcommit: 415c70d7014545c1f65271a2debf8c3c1c5eb688
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/06/2020
ms.locfileid: "77036887"
---
# <a name="creating-symbol-packages-snupkg"></a>Vytváření balíčků symbolů (. snupkg)

Dobré prostředí ladění spoléhá na přítomnost symbolů ladění, protože poskytují kritické informace, jako je například přidružení mezi zkompilovaným a zdrojovým kódem, názvy místních proměnných, trasování zásobníku a další. Balíčky symbolů (. snupkg) můžete použít k distribuci těchto symbolů a zlepšení možností ladění balíčků NuGet.

## <a name="prerequisites"></a>Předpoklady

[NuGet. exe v 4.9.0 nebo vyšší](https://www.nuget.org/downloads) nebo [dotnet CLI v 2.2.0 nebo vyšší](https://www.microsoft.com/net/download/dotnet-core/2.2), které implementují požadované [protokoly NuGet](../api/nuget-protocols.md).

## <a name="creating-a-symbol-package"></a>Vytvoření balíčku symbolů

Pokud používáte dotnet CLI nebo MSBuild, musíte nastavit `IncludeSymbols` a vlastnosti `SymbolPackageFormat` a vytvořit soubor. snupkg společně s souborem. nupkg.

* Přidejte do souboru. csproj následující vlastnosti:

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
   </PropertyGroup>
   ```

* Nebo zadejte tyto vlastnosti na příkazovém řádku:

     ```dotnetcli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  nebo

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

Pokud používáte NuGet. exe, můžete k vytvoření souboru. snupkg spolu s souborem. nupkg použít následující příkazy:

```cli
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

Vlastnost [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) může mít jednu ze dvou hodnot: `symbols.nupkg` (výchozí) nebo `snupkg`. Pokud tato vlastnost není zadána, bude vytvořen starší balíček symbolů.

> [!Note]
> Starší verze formátu `.symbols.nupkg` jsou stále podporovány, ale pouze z důvodů kompatibility (viz [starší balíčky symbolů](Symbol-Packages.md)). Server symbolů NuGet. org přijímá jenom nový formát balíčku symbolů – `.snupkg`.

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

NuGet bude publikovat oba balíčky do nuget.org. Nejprve se publikuje `MyPackage.nupkg` a potom `MyPackage.snupkg`.

> [!Note]
> Pokud se balíček symbolů nepublikuje, ověřte, že jste nakonfigurovali zdroj NuGet.org jako `https://api.nuget.org/v3/index.json`. Publikování balíčku symbolů je podporované jenom [rozhraním API NuGet V3](../api/overview.md#versioning).

## <a name="nugetorg-symbol-server"></a>NuGet.org symbol server

NuGet.org podporuje vlastní úložiště symbolů serveru a přijímá pouze nový formát balíčku symbolů – `.snupkg`. Příjemci balíčku můžou používat symboly publikované na serveru symbolů nuget.org přidáním `https://symbols.nuget.org/download/symbols` do jejich zdrojů symbolů v aplikaci Visual Studio, které umožňují krokování kódu balíčku v ladicím programu sady Visual Studio. Podrobnosti o tomto procesu najdete v tématu [určení symbolu (PDB) a zdrojových souborů v ladicím programu sady Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) .

### <a name="nugetorg-symbol-package-constraints"></a>Omezení balíčku symbolů NuGet.org

NuGet.org má následující omezení pro balíčky symbolů:

- V balíčcích symbolů jsou povoleny pouze následující přípony souborů: `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`, `.p7s`
- Na serveru se symbolem NuGet. org jsou podporované jenom spravované [přenosné soubory PDB](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) .
- Soubory PDB a jejich přidružené knihovny DLL nupkg musí být sestaveny s kompilátorem v aplikaci Visual Studio verze 15,9 nebo vyšší (viz [PDB kryptografický otisk](https://github.com/dotnet/roslyn/issues/24429)).

Balíčky symbolů publikované do NuGet.org selžou, pokud tato omezení nebudou splněna. 

### <a name="symbol-package-validation-and-indexing"></a>Ověřování a indexování balíčku symbolů

Balíčky symbolů publikované do [NuGet.org](https://www.nuget.org/) prošly několika ověřeními, včetně kontroly malwaru. Pokud balíček selže, zobrazí se na stránce Podrobnosti o jeho balíčku chybová zpráva. Kromě toho vlastníci balíčku obdrží e-mail s pokyny, jak opravit zjištěné problémy.

Když balíček symbolů předává všechna ověření, symboly budou indexovány na servery se symboly NuGet. org a budou k dispozici pro spotřebu.

Ověření a indexování balíčku obvykle trvá 15 minut. Pokud bude publikování balíčku trvat déle, než se čekalo, navštivte [status.NuGet.org](https://status.nuget.org/) a ověřte, jestli NuGet.org má nějaké přerušení. Pokud jsou všechny systémy funkční a balíček ještě není po celou hodinu publikovaný, přihlaste se k nuget.org a na stránce s podrobnostmi balíčku kontaktujte nás pomocí odkazu podpora kontaktů.

## <a name="symbol-package-structure"></a>Struktura balíčku symbolů

Balíček symbolů (. snupkg) má následující vlastnosti:

1) Soubor. snupkg má stejné ID a verzi jako odpovídající balíček NuGet (. nupkg).
2) Přípona. snupkg má stejnou strukturu složek jako odpovídající. nupkg pro jakékoli soubory DLL nebo EXE s rozlišením, které místo knihoven DLL/exe, jejich odpovídající soubory PDB bude zahrnuta do stejné hierarchie složek. Soubory a složky s rozšířeními jinými než PDB budou ponechány mimo snupkg.
3) Soubor. nuspec balíčku symbolů má typ balíčku `SymbolsPackage`:

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) Pokud se autor rozhodne použít vlastní nuspec k sestavení nupkg a snupkg, měl by mít snupkg stejnou hierarchii složek a souborů, které jsou popsány v 2).
5) Následující pole se vyloučí z nuspec snupkg: ```authors```, ```owners```, ```requireLicenseAcceptance```, ```license type```, ```licenseUrl```a ```icon```.
6) Nepoužívejte element ```<license>```. A. snupkg se zabývá stejnou licencí jako odpovídající. nupkg.

## <a name="see-also"></a>Viz také

Zvažte použití odkazu na zdroj pro povolení ladění zdrojového kódu v sestaveních .NET. Další informace najdete v [pokynech ke zdrojovému propojení](/dotnet/standard/library-guidance/sourcelink).

Další informace o balíčcích symbolů najdete v tématu [Ladění balíčků NuGet &ch symbolů vylepšení](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) návrhu.
