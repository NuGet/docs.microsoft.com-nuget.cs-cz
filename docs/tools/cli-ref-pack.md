---
title: Příkaz pack NuGet rozhraní příkazového řádku
description: Referenční dokumentace pro příkaz nuget.exe pack
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: a2468b099a822e69298ea78c80cfd1d5d5c09938
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
---
# <a name="pack-command-nuget-cli"></a>Příkaz Pack (NuGet CLI)

**Platí pro:** balíček vytvoření &bullet; **podporované verze:** 2.7 +

Vytvoří balíček NuGet založený na zadaný `.nuspec` nebo soubor projektu. `dotnet pack` Příkazu (najdete v části [dotnet příkazy](dotnet-Commands.md)) a `msbuild /t:pack` (najdete v části [cíle MSBuild](../reference/msbuild-targets.md)) může být použita jako alternativ.

> [!Important]
> V části Mono není podporováno vytváření balíčku ze souboru projektu. Také budete muset upravit jiné než místní cesty v `.nuspec` souborů na formátu UNIX cesty, jako jsou třeba nuget.exe nepřevádí názvy cest Windows sám sebe.

## <a name="usage"></a>Použití

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

kde `<nuspecPath>` a `<projectPath>` zadejte `.nuspec` nebo projektu soubor, v uvedeném pořadí.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| BasePath | Nastaví základní cesta soubory definované v `.nuspec` souboru. |
| Sestavení | Určuje, že projekt by měly být vytvořeny před vytvořením balíčku. |
| Vyloučení | Určuje jeden nebo více vzory zástupných znaků, které chcete vyloučit při vytváření balíčku. Chcete-li zadat více než jeden vzorek, opakujte příznak - vyloučení. Viz následující příklad. |
| ExcludeEmptyDirectories | Při vytváření balíčku, zabraňuje zahrnutí prázdných adresářů. |
| ForceEnglishOutput | *(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze. |
| Nápověda | Zobrazí nápovědu pro příkaz. |
| IncludeReferencedProjects | Označuje, že balíček integrovaný by měla zahrnovat odkazované projekty jako závislosti nebo jako součást balíčku. Pokud odkazované projekt má odpovídající `.nuspec` soubor, který má stejný název jako projekt, pak tento odkazovaný projektu se přidal jako závislost. Odkazovaný projekt, jinak se přidá jako součást balíčku. |
| MinClientVersion | Nastavte *minClientVersion* atribut pro vytvoření balíčku. Tato hodnota se přepíše stávající hodnotu *minClientVersion* atribut (pokud existuje) `.nuspec` souboru. |
| MSBuildPath | *(4.0 +)*  Určuje cestu MSBuild používat pomocí příkazu, přednost před `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)*  Určuje verzi nástroje MSBuild k použití se tento příkaz. Podporované hodnoty jsou 4, 12, 14, 15. Ve výchozím nastavení je zachyceny MSBuild ve své cestě jinak bude výchozí nejvyšší nainstalovanou verzi nástroje MSBuild. |
| NoDefaultExcludes | Zabraňuje výchozí vyloučení NuGet balíček soubory a soubory a složky začínající tečkou, jako například `.svn` a `.gitignore`. |
| NoPackageAnalysis | Určuje, že sada by neměl spustit analysis balíčku po vytvoření balíčku. |
| Výstupnísložka | Určuje složku, ve kterém je uložen balíček vytvořený. Pokud není zadaný žádný složky, se používá aktuální složky. |
| Vlastnosti | By se zobrazit poslední na příkazovém řádku po další možnosti. Určuje seznam vlastností, které potlačí hodnoty v souboru projektu; v tématu [běžné vlastnosti projektu nástroje MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) pro názvy vlastností. Argument vlastnosti tady je seznam token = hodnota páry, oddělené středníky, kde každý výskyt `$token$` v `.nuspec` souboru se nahradí s danou hodnotou. Hodnoty mohou být řetězce v uvozovkách. Všimněte si, že pro vlastnost "Konfigurace" Výchozí hodnota je "Debug". Můžete změnit konfiguraci verze `-Properties Configuration=Release`. |
| Přípona | *(3.4.4+)*  Připojí příponu k číslo verze generované interně, obvykle se používá pro připojování sestavení nebo dalších identifikátorů předběžné verze. Například pomocí `-suffix nightly` vytvoří balíček s jako číslo verze `1.2.3-nightly`. Přípony musí začínat písmenem, aby se zabránilo upozornění, chyby a potenciální nekompatibilitu s různými verzemi nástroje NuGet a Správce balíčků NuGet. |
| Symboly | Určuje, zda balíček obsahuje zdroje a symboly. Při použití s `.nuspec` souboru, tím se vytvoří soubor regulární balíčku NuGet a odpovídající balíčku symbolů. |
| Nástroj | Určuje, že výstupních souborů projektu mají být umístěny v `tool` složky. |
| Podrobnosti | Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*. |
| Version | Přepsání číslo verze z `.nuspec` souboru. |

Viz také [proměnné prostředí](cli-ref-environment-variables.md)

## <a name="excluding-development-dependencies"></a>S výjimkou vývoj závislosti

Některé balíčky NuGet jsou užitečné jako vývoj závislosti, které umožňují vytvářet vlastní knihovny, ale nejsou nezbytně potřebné jako závislosti skutečné balíčků.

`pack` Příkaz bude ignorovat `package` položek v `packages.config` mají `developmentDependency` atribut nastaven na `true`. Tyto položky nebudou obsahovat jako závislosti v vytvořený balíčku.

Například vezměte v úvahu následující `packages.config` v projektu zdroje:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

Pro tento projekt balíček vytvořený `nuget pack` bude mít závislost na `jQuery` a `microsoft-web-helpers` ale ne `netfx-Guard`.

## <a name="examples"></a>Příklady

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -MSBuildVersion 12 -Properties owners=janedoe,xiaop;version="1.0.5

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
