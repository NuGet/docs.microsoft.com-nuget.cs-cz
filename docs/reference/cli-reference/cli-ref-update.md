---
title: Příkaz NuGet CLI Update
description: Referenční informace k příkazu nuget.exe Update
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: cfa7fdcc6af46fd5f4030ba424754291f697bc43
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779133"
---
# <a name="update-command-nuget-cli"></a>Update – příkaz (NuGet CLI)

**Platí pro:** &bullet; **podporované verze balíčku:** vše

Aktualizuje všechny balíčky v projektu (pomocí `packages.config` ) na nejnovější dostupné verze. Před spuštěním nástroje se doporučuje spustit příkaz [Restore](cli-ref-restore.md) `update` . (Pokud chcete aktualizovat jednotlivý balíček, použijte [`nuget install`](cli-ref-install.md) bez zadání čísla verze. v takovém případě NuGet nainstaluje nejnovější verzi.)

Poznámka: `update` nefunguje s rozhraním příkazového řádku spuštěným v mono (Mac OSX nebo Linux) nebo při použití formátu PackageReference.

`update`Příkaz také aktualizuje odkazy na sestavení v souboru projektu za předpokladu, že tyto odkazy již existují. Pokud aktualizovaný balíček obsahuje přidané sestavení, nový *odkaz se nepřidá.* Nové závislosti balíčků také nemají přidané odkazy na sestavení. Chcete-li zahrnout tyto operace jako součást aktualizace, aktualizujte balíček v aplikaci Visual Studio pomocí uživatelského rozhraní Správce balíčků nebo konzoly Správce balíčků.

Tento příkaz lze také použít k aktualizaci nuget.exe sebe sama pomocí příznaku *-vlastní* .

## <a name="usage"></a>Využití

```cli
nuget update <configPath> [options]
```

kde `<configPath>` identifikuje buď `packages.config` soubor řešení nebo, který obsahuje seznam závislostí projektu.

## <a name="options"></a>Možnosti

- **`-ConfigFile`**

  Konfigurační soubor NuGet, který se má použít Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows) nebo `~/.nuget/NuGet/NuGet.Config` nebo `~/.config/NuGet/NuGet.Config` (Mac/Linux).
  
- **`-DependencyVersion [Lowest, HighestPatch, HighestMinor, Highest, Ignore]`**

  Určuje verzi balíčků závislostí, které se mají použít, což může být jedna z následujících:<br/><ul><li>*Nejnižší* (výchozí): nejnižší verze</li><li>*HighestPatch*: verze, která má nejnižší hlavní, nejnižší podverzi, nejvyšší opravu</li><li>*HighestMinor*: verze s nejnižší hlavní, nejvyšší podverze a nejvyšší opravou</li><li>*Nejvyšší*: nejvyšší verze</li><li>*Ignorovat*: nebudou použity žádné balíčky závislostí.</li></ul>

- **`-FileConflictAction [PromptUser, Overwrite, Ignore]`**

  Určuje výchozí akci, pokud soubor z balíčku již v cílovém projektu existuje. Nastavte na `Overwrite` vždycky přepsat soubory. Nastavte na `Ignore` Přeskočit soubory.

  Tato `PromptUser` akce, ve výchozím nastavení, zobrazí výzvu k zadání všech konfliktních souborů `OverwriteAll` , pokud ani `IgnoreAll` není zadáno, který bude platit pro všechny zbývající soubory.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Vynutí spuštění nuget.exe s využitím neutrální jazykové verze založené na angličtině.

- **`-?|-help`**

  Zobrazí informace o nápovědě k příkazu.

- **`-Id`**

  Určuje seznam ID balíčků, které se mají aktualizovat.

- **`-MSBuildPath`**

  *(4.0 +)* Určuje cestu nástroje MSBuild, který má být použit s příkazem, přičemž přednost využije `-MSBuildVersion` .

- **`-MSBuildVersion`**

  *(3.2 +)* Určuje verzi nástroje MSBuild, která má být použita s tímto příkazem. Podporované hodnoty jsou 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. Ve výchozím nastavení je nástroj MSBuild v cestě vybrán, jinak má výchozí nejvyšší nainstalovanou verzi nástroje MSBuild.

- **`-NonInteractive`**

  Potlačí výzvy pro vstup uživatele nebo potvrzení.

- **`-PreRelease`**

  Umožňuje aktualizaci předprodejních verzí. Tento příznak není požadován při aktualizaci předprodejních balíčků, které jsou již nainstalovány.

- **`-RepositoryPath`**

  Určuje místní složku, ve které jsou balíčky nainstalované.

- **`-Safe`**

  Určuje, že se budou instalovat jenom aktualizace s nejvyšší verzí dostupnou v rámci stejné hlavní a dílčí verze, jako je nainstalovaný balíček.

- **`-Self`**

  Aktualizuje nuget.exe na nejnovější verzi. všechny ostatní argumenty jsou ignorovány.

- **`-Source`**

  Určuje seznam zdrojů balíčků (jako adresy URL), které se mají použít pro aktualizace. Pokud je tato hodnota vynechána, příkaz použije zdroje zadané v konfiguračních souborech, viz [běžné konfigurace NuGet](../../consume-packages/configuring-nuget-behavior.md).

- **`-Verbosity [normal|quiet|detailed]`**

  Určuje množství podrobností zobrazených ve výstupu: `normal` (výchozí), `quiet` nebo `detailed` .

- **`-Version`**

  Při použití s jedním ID balíčku určuje verzi balíčku, který se má aktualizovat.

Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .

## <a name="examples"></a>Příklady

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
