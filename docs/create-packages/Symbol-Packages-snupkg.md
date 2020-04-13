---
title: Jak publikovat balíčky symbolů NuGet pomocí nového formátu balíčku symbolů '.snupkg'| Dokumenty společnosti Microsoft
author: cristinamanu
ms.author: cristinamanu
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Jak vytvořit balíčky symbolů NuGet (snupkg).
keywords: Balíčky symbolů NuGet, ladění balíčku NuGet, podpora ladění NuGet, symboly balíčků balíčků, konvence balíčků symbolů
ms.reviewer:
- anangaur
- karann
ms.openlocfilehash: c42032f1869f4be0af44ffa8fbd5ad522f73c459
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "80380415"
---
# <a name="creating-symbol-packages-snupkg"></a>Vytváření balíčků symbolů (.snupkg)

Dobré ladění prostředí závisí na přítomnost ladicí symboly, protože poskytují důležité informace, jako je přidružení mezi zkompilované a zdrojový kód, názvy místních proměnných, trasování zásobníku a další. Balíčky symbolů (.snupkg) můžete distribuovat tyto symboly a zlepšit ladění prostředí balíčků NuGet.

## <a name="prerequisites"></a>Požadavky

[nuget.exe v4.9.0 nebo vyšší](https://www.nuget.org/downloads) nebo [dotnet CLI v2.2.0 nebo vyšší](https://www.microsoft.com/net/download/dotnet-core/2.2), které implementují požadované [protokoly NuGet](../api/nuget-protocols.md).

## <a name="creating-a-symbol-package"></a>Vytvoření balíčku symbolů

Pokud používáte dotnet CLI nebo MSBuild, je `IncludeSymbols` `SymbolPackageFormat` třeba nastavit vlastnosti a k vytvoření souboru .snupkg kromě souboru .nupkg.

* Do souboru .csproj přidejte následující vlastnosti:

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

  – nebo –

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

Pokud používáte soubor NuGet.exe, můžete kromě souboru .nupkg použít následující příkazy k vytvoření souboru Snupkg:

```cli
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

Vlastnost [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) může mít jednu `symbols.nupkg` ze dvou hodnot: (výchozí) nebo `snupkg`. Pokud tato vlastnost není zadána, bude vytvořen balíček starší symbol.

> [!Note]
> Starší formát `.symbols.nupkg` je stále podporován, ale pouze z důvodů kompatibility (viz [Starší balíčky symbolů).](Symbol-Packages.md) Server symbolů NuGet.org přijímá pouze nový formát `.snupkg`balíčku symbolů - .

## <a name="publishing-a-symbol-package"></a>Publikování balíčku symbolů

1. Pro větší pohodlí nejprve uložte klíč rozhraní API s NuGet (viz [publikování balíčku](../nuget-org/publish-a-package.md)).

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. Po publikování primární balíček nuget.org, stiskněte balíček symbol takto.

    ```cli
    nuget push MyPackage.snupkg
    ```

1. Balíčky primárních i symbolů můžete také tlačit současně pomocí příkazu níže. V aktuální složce musí být k dispozici soubory .nupkg i .snupkg.

    ```cli
    nuget push MyPackage.nupkg
    ```

NuGet publikuje oba balíčky do nuget.org. `MyPackage.nupkg` budou zveřejněny jako první, následované `MyPackage.snupkg`.

> [!Note]
> Pokud balíček symbolů není publikován, zkontrolujte, zda jste `https://api.nuget.org/v3/index.json`nakonfigurovali NuGet.org zdroj jako . Publikování balíčku symbolů je podporováno pouze [rozhraním API NuGet V3](../api/overview.md#versioning).

## <a name="nugetorg-symbol-server"></a>NuGet.org symbolový server

NuGet.org podporuje vlastní úložiště serverů symbolů a přijímá pouze `.snupkg`nový formát balíčku symbolů - . Příjemci balíčků mohou použít symboly publikované `https://symbols.nuget.org/download/symbols` na nuget.org serveru symbolů přidáním zdrojů symbolů v sadě Visual Studio, což umožňuje krokování do kódu balíčku v ladicím programu sady Visual Studio. Podrobnosti o tomto [procesu naleznete v tématu Určení symbolu (.pdb) a zdrojových souborů v ladicím programu sady Visual Studio.](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger)

### <a name="nugetorg-symbol-package-constraints"></a>omezení balíčku NuGet.org symbolů

NuGet.org má následující omezení pro balíčky symbolů:

- V balíčcích symbolů jsou povoleny `.pdb` `.nuspec`pouze `.xml` `.psmdcp`následující `.rels`přípony souborů: , , , , , ,`.p7s`
- Na serveru se symboly NuGet.org jsou podporovány pouze spravované [přenosné objekty PDB.](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md)
- Disky DLL a přidružené knihovny DLL .nupkg musí být vytvořeny pomocí kompilátoru ve visual taště verze 15.9 nebo vyšší (viz [pdb kryptografický hash)](https://github.com/dotnet/roslyn/issues/24429)

Balíčky symbolů publikované do NuGet.org se nezdaří ověření, pokud tato omezení nejsou splněna. 

### <a name="symbol-package-validation-and-indexing"></a>Ověření a indexování balíčku symbolů

Balíčky symbolů publikované [NuGet.org](https://www.nuget.org/) podrobeny několika ověřením, včetně skenování malwaru. Pokud balíček neprojde kontrolou ověření, zobrazí se na stránce podrobností o balíčku chybová zpráva. Kromě toho majitelé balíčku obdrží e-mail s pokyny, jak opravit zjištěné problémy.

Pokud balíček symbolprošel všechna ověření, symboly budou indexovány servery symbol NuGet.org a bude k dispozici pro spotřebu.

Ověření a indexování balíčku obvykle trvá méně než 15 minut. Pokud publikování balíčku trvá déle, než bylo očekáváno, navštivte [status.nuget.org](https://status.nuget.org/) a zkontrolujte, zda NuGet.org dochází k přerušení. Pokud jsou všechny systémy funkční a balíček nebyl úspěšně publikován do hodiny, přihlaste se do nuget.org a kontaktujte nás pomocí odkazu Kontaktujte podporu na stránce podrobností o balíčku.

## <a name="symbol-package-structure"></a>Struktura balíčku symbolů

Symbol balíček (.snupkg) má následující vlastnosti:

1) .snupkg má stejné id a verzi jako jeho odpovídající Balíček NuGet (.nupkg).
2) .snupkg má stejnou strukturu složek jako jeho odpovídající .nupkg pro všechny soubory DLL nebo EXE s rozdílem, že místo DLL/EXEs budou jejich odpovídající objekty PDB zahrnuty do hierarchie stejných složek. Soubory a složky s jinými příponami než PDB budou ponechány mimo snupkg.
3) Soubor .nuspec balíčku symbolů `SymbolsPackage` má typ balíčku:

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) Pokud se autor rozhodne použít vlastní nuspec k sestavení jejich nupkg a snupkg, snupkg by měl mít stejnou hierarchii složek a soubory podrobně popsané v 2).
5) Následující pole budou vyloučena z nuspec ```authors```snupkg: ```owners``` ```requireLicenseAcceptance```, ```license type``` ```licenseUrl```, ```icon```, , , a .
6) Nepoužívejte ```<license>``` prvek. A .snupkg je zahrnuta ve stejné licenci jako odpovídající .nupkg.

## <a name="see-also"></a>Viz také

Zvažte použití zdrojového odkazu k povolení ladění zdrojového kódu sestavení .NET. Další informace naleznete v [pokynech pro zdrojový odkaz](/dotnet/standard/library-guidance/sourcelink).

Další informace o balíčcích symbolů naleznete v specifikaci návrhu [ladění balíčků NuGet & symboly.](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)
