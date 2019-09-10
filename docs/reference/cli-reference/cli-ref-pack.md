---
title: NuGet – příkaz packu CLI
description: Reference k příkazu NuGet. exe Pack
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 76829d45ea9821da3b7fdaa2f88d30dbb104fea1
ms.sourcegitcommit: 5a741f025e816b684ffe44a81ef7d3fbd2800039
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/09/2019
ms.locfileid: "70815358"
---
# <a name="pack-command-nuget-cli"></a>Příkaz Pack (NuGet CLI)

**Platí pro:** vytváření &bullet; balíčků **podporuje verze:** 2.7+

Vytvoří balíček NuGet založený na zadaném souboru [. nuspec](../nuspec.md) nebo projektu. Příkaz (viz [příkazy dotnet](../dotnet-Commands.md)) a `msbuild -t:pack` (viz [cíle nástroje MSBuild](../msbuild-targets.md)) lze použít jako alternativy. `dotnet pack`

> [!Important]
> V rámci mono není podporováno vytváření balíčku ze souboru projektu. Také je nutné upravit jiné než místní cesty v `.nuspec` souboru na cesty ve stylu systému UNIX, protože NuGet. exe nepřevádí samotné cesty systému Windows.

## <a name="usage"></a>Použití

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

kde `<nuspecPath>` a `<projectPath>` Zadejte`.nuspec` soubor projektu, v uvedeném pořadí.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| BasePath | Nastaví základní cestu souborů definovaných v souboru [. nuspec](../nuspec.md) . |
| Sestavení | Určuje, že projekt by měl být sestaven před sestavením balíčku. |
| Deterministický | Určete, zda má příkaz vytvořit deterministický balíček. Vícenásobné vyvolání příkazu Pack vygeneruje přesně stejný balíček Byte-to-Byte. Výstup příkazu Pack není ovlivněn okolním stavem počítače. Konkrétně položky zip budou časové razítko jako 1980-01-01. Aby bylo možné dosáhnout úplných determinismem, sestavení by měla být sestavena s odpovídající možností kompilátoru [– deterministické](/dotnet/csharp/language-reference/compiler-options/deterministic-compiler-option). |
| Slevy | Určuje jeden nebo více vzorových zástupných znaků, které se mají vyloučit při vytváření balíčku. Chcete-li zadat více než jeden vzor, opakujte příznak-Exclude. Viz následující příklad. |
| ExcludeEmptyDirectories | Zabrání zahrnutí prázdných adresářů při sestavování balíčku. |
| ForceEnglishOutput | *(3.5 +)* Vynutí, aby soubor NuGet. exe běžel pomocí neutrální jazykové verze určené pro angličtinu. |
| ConfigFile | Zadejte konfigurační soubor pro příkaz Pack. |
| Help | Zobrazí informace o nápovědě k příkazu. |
| IncludeReferencedProjects | Označuje, že sestavený balíček by měl zahrnovat odkazované projekty buď jako závislosti, nebo jako součást balíčku. Pokud má odkazovaný projekt odpovídající `.nuspec` soubor, který má stejný název jako projekt, pak je odkaz na projekt přidán jako závislost. V opačném případě se odkazovaný projekt přidá jako součást balíčku. |
| MinClientVersion | Nastavte atribut *minClientVersion* pro vytvořený balíček. Tato hodnota přepíše hodnotu existujícího atributu *minClientVersion* (pokud existuje) v `.nuspec` souboru. |
| MSBuildPath | *(4.0 +)* Určuje cestu nástroje MSBuild, který má být použit s příkazem, přičemž přednost `-MSBuildVersion`využije. |
| MSBuildVersion | *(3.2 +)* Určuje verzi nástroje MSBuild, která má být použita s tímto příkazem. Podporované hodnoty jsou 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. Ve výchozím nastavení je nástroj MSBuild v cestě vybrán, jinak má výchozí nejvyšší nainstalovanou verzi nástroje MSBuild. |
| NoDefaultExcludes | Zabraňuje výchozímu vyloučení souborů a souborů balíčku NuGet počínaje tečkou, například `.svn` a. `.gitignore` |
| NoPackageAnalysis | Určuje, že sada by neměla po sestavení balíčku spustit analýzu balíčku. |
| OutputDirectory | Určuje složku, ve které je vytvořený balíček uložený. Pokud není zadána žádná složka, je použita aktuální složka. |
| Vlastnosti | By měl být na příkazovém řádku zobrazen na konci dalších možností. Určuje seznam vlastností, které přepíší hodnoty v souboru projektu. názvy vlastností najdete v tématu [běžné vlastnosti projektu nástroje MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) . Argument vlastnosti tady je seznam párů token = hodnota oddělený středníky, kde každý výskyt `$token$` `.nuspec` v souboru bude nahrazen danou hodnotou. Hodnoty mohou být řetězce v uvozovkách. Všimněte si, že pro vlastnost "konfigurace" je výchozí hodnota "ladit". Chcete-li přejít na konfiguraci vydané verze `-Properties Configuration=Release`, použijte. |
| Auditování | *(3.4.4 +)* Připojí příponu k interně vygenerovanému číslu verze, které se obvykle používá pro připojení buildu nebo jiné identifikátory předběžného vydání. Například pomocí `-suffix nightly` vytvoříte balíček s číslem verze, jako `1.2.3-nightly`je. Přípony musí začínat písmenem, aby se předešlo varováním, chybám a potenciálním nekompatibilitám s různými verzemi NuGet a správcem balíčků NuGet. |
| Symboly | Určuje, že balíček obsahuje zdroje a symboly. Při použití se `.nuspec` souborem se vytvoří pravidelný soubor balíčku NuGet a odpovídající balíček symbolů. Ve výchozím nastavení vytvoří [starší verzi balíčku symbolů](../../create-packages/Symbol-Packages.md). Nový doporučený formát pro balíčky symbolů je. snupkg. Viz [vytváření balíčků symbolů (. snupkg)](../../create-packages/Symbol-Packages-snupkg.md). |
| Nástroj | Určuje, že výstupní soubory projektu by měly být umístěny do `tool` složky. |
| Verbosity | Určuje množství podrobností zobrazených ve výstupu: *normální*, *tiché*a *podrobné*. |
| Version | Přepíše číslo verze ze `.nuspec` souboru. |

Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .

## <a name="excluding-development-dependencies"></a>Vyloučení závislostí vývoje

Některé balíčky NuGet jsou užitečné jako závislosti na vývoji, které vám pomůžou vytvářet vlastní knihovny, ale nutně se nevyžadují jako skutečné závislosti balíčků.

`package` Příkazbude`packages.config` ignorovat položkyv`true`, které mají atributnastavennahodnotu.`developmentDependency` `pack` Tyto položky nebudou do vytvořeného balíčku zahrnovat jako závislosti.

Zvažte například následující `packages.config` soubor ve zdrojovém projektu:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

Pro tento projekt bude mít balíček vytvořen pomocí `nuget pack` závislost na `jQuery` , `microsoft-web-helpers` ale ne `netfx-Guard`.

## <a name="examples"></a>Příklady

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -MSBuildVersion 12 -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.nuspec and the corresponding symbol package using the new recommended format .snupkg
nuget pack foo.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
