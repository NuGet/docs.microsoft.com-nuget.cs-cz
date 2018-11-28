---
title: Publikování symbolů balíčky NuGet pomocí nového formátu balíčku symbol ".snupkg. | Dokumentace Microsoftu
author:
- cristinamanu
- kraigb
ms.author:
- cristinamanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Postup vytvoření symbolu balíčky NuGet (snupkg).
keywords: Symbol balíčky NuGet, balíček NuGet ladění, podpora, balíček symboly ladění, symbol vytváření balíčku NuGet
ms.reviewer:
- anangaur
- karann
ms.openlocfilehash: 48ca4b62e722988b3dfe69306565d7f159805962
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453452"
---
# <a name="creating-symbol-packages-snupkg"></a>Vytváření balíčků symbolů (.snupkg)

## <a name="prerequisites"></a>Požadavky

[nuget.exe v4.9.0 nebo vyšší](https://www.nuget.org/downloads) nebo [dotnet.exe v2.2.0 nebo vyšší](https://www.microsoft.com/net/download/dotnet-core/2.2), které implementují požadované [NuGet protokoly](../api/nuget-protocols.md).

## <a name="creating-a-symbol-package"></a>Vytváří se balíček symbolů

Balíček symbolů snupkg lze vytvořit ze souboru .nuspec souboru nebo ze souboru csproj. NuGet.exe a dotnet.exe jsou podporované. Když možnosti ```-Symbols -SymbolPackageFormat snupkg``` se používají k příkazu pack nuget.exe .snupkg soubor vytvoří v dále .nupkg souboru.

Příklady příkazů pro vytvoření .snupkg souborů
```
dotnet pack MyPackage.csproj --include-symbols -p:SymbolPackageFormat=snupkg

nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg

msbuild -t:pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
```

`.snupkgs` nejsou vytvořené ve výchozím nastavení. Je nutné předat `SymbolPackageFormat` vlastnost spolu s `-Symbols` v případě nuget.exe, `--include-symbols` v případě dotnet.exe, nebo `-p:IncludeSymbols` v případě nástroje msbuild.

Vlastnost SymbolPackageFormat může mít jednu ze dvou hodnot: `symbols.nupkg` (výchozí) nebo `snupkg`. Pokud SymbolPackageFormat není zadán, použije se výchozí `symbols.nupkg` a vytvoří se balíček symbolů starší verze.

> [!Note]
> Starší verze formátu `.symbols.nupkg` je ale pouze z důvodů kompatibility stále podporována (viz [starších verzí balíčků symbolů](Symbol-Packages.md)). Server symbolů NuGet.org přijímá pouze nový formát balíček symbolů - `.snupkg`.

## <a name="publishing-a-symbol-package"></a>Publikování balíčku symbolů

1. Pro usnadnění práce, uložte svůj klíč rozhraní API s NuGet (viz [publikování balíčku](../create-packages/publish-a-package.md)).

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. Po publikování vaší primární balíčků na nuget.org, push balíček symbolů následujícím způsobem.

    ```cli
    nuget push MyPackage.snupkg
    ```

1. Můžete také vložit obě primární a symbol balíčky na pomocí následující příkaz. .Nupkg a .snupkg soubory musí mít k dispozici v aktuální složce.

    ```cli
    nuget push MyPackage.nupkg
    ```

NuGet se publikovat oba balíčky nuget.org. `MyPackage.nupkg` se nejprve publikovat, za nímž následuje `MyPackage.snupkg`.

## <a name="nugetorg-symbol-server"></a>Server symbolů NuGet.org

NuGet.org podporuje své vlastní úložiště serveru symbolů a přijímá pouze nový formát balíček symbolů - `.snupkg`. Příjemci balíčku můžete použít symboly publikované na nuget.org symbol server tak, že přidáte `https://symbols.nuget.org/download/symbols` k jejich symbol zdroje v sadě Visual Studio, který umožňuje krokování s vnořením do kódu balíček v ladicím programu sady Visual Studio. Zobrazit [zadání symbolu (.pdb) a zdrojových souborů v ladicím programu sady Visual Studio](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017) podrobnosti o tomto procesu.

### <a name="nugetorg-symbol-package-constraints"></a>Omezení balíček symbolů Nuget.org

Balíčky symbolů, které jsou podporovány na nuget.org mají následující omezení

- Následující přípony souborů můžou přidat do balíčků symbolů. ```.pdb,.nuspec,.xml,.psmdcp,.rels,.p7s```
- Pouze spravované [souborům Portable PDB](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) jsou aktuálně podporovány na serveru symbolů nuget.
- Soubory PDB a DLL přidružené nupkg musela být vytvořená s kompilátorem v sadě Visual Studio verzi 15.9 nebo vyšší (viz [kryptografické hodnoty hash souboru pdb](https://github.com/dotnet/roslyn/issues/24429))

Publikovat balíček symbolů na nuget.org se nezdaří, pokud jiné typy souborů jsou součástí .snupkg.

### <a name="symbol-package-validation-and-indexing"></a>Ověření balíčku symbolů a indexování

Symbol balíčky, které jsou publikovány na [NuGet.org](https://www.nuget.org/) projít několik ověření, jako jsou antivirové kontroly.

Když tento balíček prošel všechny ověřovací kontroly, může trvat nějakou dobu symboly pro indexování a být k dispozici pro použití ze serverů symbolů NuGet.org. Pokud balíček selhání kontroly ověřování, na stránce podrobností balíčku pro .nupkg se aktualizuje a zobrazí související chyby a také obdržíte e-mail s upozorněním můžete o něm.

Ověření balíčku a indexování obvykle trvá méně než 15 minut. Pokud o publikování balíčku trvá déle, než se očekávalo, navštivte [status.nuget.org](https://status.nuget.org/) ke kontrole, pokud nuget.org dochází k žádné přerušení. Pokud jsou všechny systémy provozní a balíčku nebyla úspěšně publikována do jedné hodiny, přihlaste se prosím na nuget.org a kontaktujte nás přes odkaz na podporu se obraťte se na stránce s podrobnostmi balíčku.

## <a name="symbol-package-structure"></a>Struktura balíčku symbolů

Soubor .nupkg budou naprosto stejné jako dnes je ale soubor .snupkg by mít následující vlastnosti:

1) .snupkg, bude mít jako odpovídající .nupkg stejné id a verzi.
2) .snupkg bude mít strukturu složek přesné jako soubor nupkg pro soubory DLL nebo EXE s rozlišovat, že namísto knihovny DLL/exe, jejich odpovídající soubory PDB budou zahrnuty ve stejné hierarchii složek. Mimo snupkg by zůstaly souborů a složek s příponou než PDB.
3) Soubor souboru .nuspec v .snupkg zadejte také nové PackageType jak je uvedeno níže. To by měl pouze jeden PackageType zadán. 
``` 
<packageTypes>
  <packageType name="SymbolsPackage"/>
</packageTypes>
```
4) Pokud autor rozhodne použít vlastní soubor nuspec vytvářet jejich nupkg a snupkg, snupkg by měl mít stejné hierarchii složek a souborů, které jsou podrobně popsané v 2).
5) ```authors``` a ```owners``` pole budou vyloučeny z snupkg nuspec.

## <a name="see-also"></a>Viz také

[NuGet – balíček – ladění – & - symboly – vylepšení](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)
