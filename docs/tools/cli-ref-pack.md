---
title: Příkaz balíčku NuGet rozhraní příkazového řádku
description: Referenční informace pro příkaz pack nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 826316bdbce881836836f2a667cfa5297996d14f
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580308"
---
# <a name="pack-command-nuget-cli"></a>Příkaz Pack (NuGet CLI)

**Platí pro:** vytvoření balíčku &bullet; **podporované verze:** 2.7 +

Vytvoří balíček NuGet stanoveného `.nuspec` nebo soubor projektu. `dotnet pack` Příkazu (naleznete v tématu [příkazy dotnet](dotnet-Commands.md)) a `msbuild /t:pack` (naleznete v tématu [cíle nástroje MSBuild](../reference/msbuild-targets.md)) mohou být použity jako alternativní úložiště.

> [!Important]
> Mono se nepodporuje vytváření balíčku ze souboru projektu. Budete také muset upravit jiné než místní cesty v `.nuspec` sdílené cesty stylu systému Unix, jak nuget.exe nepřevádí Windows cesty, samotného.

## <a name="usage"></a>Použití

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

kde `<nuspecPath>` a `<projectPath>` zadejte `.nuspec` nebo souboru, resp. projektu.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| BasePath | Nastaví základní cestu k souborům definovaným v `.nuspec` souboru. |
| Sestavení | Určuje, zda by měly být sestaveny projektu před vytvořením balíčku. |
| Vyloučení | Určuje nejméně jeden vzor zástupných znaků pro vyloučení při vytváření balíčku. Chcete-li zadat více než jeden vzor, opakujte příznak - vyloučení. Viz následující příklad. |
| ExcludeEmptyDirectories | Zabraňuje zahrnovaly prázdné adresáře při sestavování balíčku. |
| ForceEnglishOutput | *(3.5 +)*  Vynutí nuget.exe pro spuštění pomocí neutrální, základem je angličtina jazyková verze. |
| ConfigFile | Zadejte konfigurační soubor pro příkaz pack. |
| Nápověda | Zobrazí nápovědu pro příkaz. |
| IncludeReferencedProjects | Označuje, že sestavení balíčku by měl zahrnovat odkazované projekty buď jako závislosti, nebo jako součást balíčku. Pokud odkazovaný projekt má odpovídající `.nuspec` soubor, který má stejný název jako projekt, pak tento Odkazovaný projekt je přidán jako závislost. V opačném případě Odkazovaný projekt je přidán jako součást balíčku. |
| MinClientVersion | Nastavte *minClientVersion* atribut pro vytvořený balíček. Tato hodnota se přepíše stávající hodnotu *minClientVersion* atribut (pokud existuje) `.nuspec` souboru. |
| MSBuildPath | *(4.0 +)*  Určuje cestu k používání pomocí příkazu, přednost `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)*  Určuje verzi Msbuildu, který se má použít tento příkaz. Podporované hodnoty jsou 4, 12, 14, 15. Ve výchozím nastavení se vybere MSBuild na vaší cestě jinak je výchozí hodnotou nejvyšší nainstalovaná verze Msbuildu. |
| NoDefaultExcludes | Zabraňuje standardně vylučovaly NuGet balíček soubory a soubory a složky, které začínají tečkou, jako například `.svn` a `.gitignore`. |
| NoPackageAnalysis | Určuje, že balíček by neměl balíčku spustit jeho analýzu po sestavení. |
| OutputDirectory | Určuje složku, ve kterém je uložený vytvořený balíček. Pokud není zadána žádná složka, použije se aktuální složce. |
| Vlastnosti | By se zobrazit poslední na příkazovém řádku po další možnosti. Určuje seznam vlastností, které přepisují hodnoty v souboru projektu. Zobrazit [obecné vlastnosti projektu nástroje MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) pro názvy vlastností. Vlastnosti argumentu tady je seznam token = dvojice hodnot oddělených středníkem, ve kterém každý výskyt `$token$` v `.nuspec` soubor se nahradí zadanou hodnotu. Hodnoty mohou být řetězce v uvozovkách. Všimněte si, že pro vlastnost "Konfigurace" Výchozí hodnota je "Debug". Chcete-li změnit konfiguraci vydané verze, použijte `-Properties Configuration=Release`. |
| Přípona | *(3.4.4+)*  Připojí přípona interně vygenerovanému číslu verze, obvykle se používá pro připojování sestavení nebo jiné předběžné verze identifikátory. Například použití `-suffix nightly` vytvoří balíček s lajk číslo verze `1.2.3-nightly`. Přípony musí začínat písmenem, aby se zabránilo upozornění a chyby, kde najdete potenciální nekompatibility s různými verzemi nástroje NuGet a Správce balíčků NuGet. |
| Symboly | Určuje, zda balíček obsahuje zdroje a symbolů. Při použití s `.nuspec` soubor, vytvoří běžný soubor balíčku NuGet a odpovídající balíček symbolů. Ve výchozím nastavení vytvoří [symbol starší verze balíčku](../create-packages/Symbol-Packages.md). Nové doporučený formát pro balíčky symbolů je .snupkg. Zobrazit [vytváření balíčků symbolů (.snupkg)](../create-packages/Symbol-Packages-snupkg.md). |
| Nástroj | Určuje, že výstupní soubory projektu musí být umístěné ve `tool` složky. |
| Podrobnosti | Určuje množství podrobností, na které se zobrazí ve výstupu: *normální*, *quiet*, *podrobné*. |
| Version | Přepíše číslo verze z `.nuspec` souboru. |

Viz také [proměnné prostředí](cli-ref-environment-variables.md)

## <a name="excluding-development-dependencies"></a>Kromě závislosti vývoj

Některé balíčky NuGet jsou užitečné jako vývoj závislosti, které umožňují vytvářet vlastní knihovny, ale nutně nevyžadují jako závislosti skutečného balíčku.

`pack` Ignoruje příkaz `package` položky v `packages.config` , které mají `developmentDependency` atribut nastaven na `true`. Tyto položky nesmí obsahovat jako závislosti v vytvořený balíček.

Představte si třeba následující `packages.config` soubor zdrojového projektu:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

Pro tento projekt vytvořil balíček `nuget pack` bude mít závislost na `jQuery` a `microsoft-web-helpers` , ale ne `netfx-Guard`.

## <a name="examples"></a>Příklady

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -MSBuildVersion 12 -Properties owners=janedoe,xiaop;version="1.0.5

# Create a package from project foo.nuspec and the corresponding symbol package using the new recommended format .snupkg
nuget pack foo.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
