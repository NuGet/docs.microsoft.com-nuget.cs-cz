---
title: Instalační příkaz NuGet CLI
description: Referenční informace k příkazu nuget.exe Install
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 23856728d07d07183b5aedcd6218a56a444c410b
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623094"
---
# <a name="install-command-nuget-cli"></a>Install – příkaz (NuGet CLI)

**Platí pro:** &bullet; **podporované verze balíčku:** vše

Stáhne a nainstaluje balíček do projektu, přičemž se použije jako výchozí pro aktuální složku pomocí zadaných zdrojů balíčků.

> [!Tip]
> Chcete-li stáhnout balíček přímo mimo kontext projektu, navštivte stránku balíčku na [NuGet.org](https://www.nuget.org) a vyberte odkaz **ke stažení** .

Pokud nejsou zadány žádné zdroje, budou použity hodnoty uvedené v globálním konfiguračním souboru `%appdata%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux). Další podrobnosti najdete v tématu [běžné konfigurace NuGet](../../consume-packages/configuring-nuget-behavior.md) .

Pokud nejsou zadány žádné konkrétní balíčky, aplikace `install` nainstaluje všechny balíčky uvedené v `packages.config` souboru projektu a bude tak vypadat podobně jako [`restore`](cli-ref-restore.md) .

`install`Příkaz neupraví soubor projektu nebo `packages.config` ; tímto způsobem je podobný jako `restore` v tom, že přidá pouze balíčky na disk, ale nemění závislosti projektu.

Chcete-li přidat závislost, buď přidejte balíček prostřednictvím uživatelského rozhraní nebo konzoly Správce balíčků v aplikaci Visual Studio, nebo upravte `packages.config` a potom spusťte buď `install` nebo `restore` .

## <a name="usage"></a>Využití

```cli
nuget install <packageID | configFilePath> [options]
```

kde `<packageID>` pojmenuje balíček k instalaci (pomocí nejnovější verze) nebo `<configFilePath>` identifikuje `packages.config` soubor, který obsahuje seznam balíčků, které se mají nainstalovat. Můžete určit konkrétní verzi s `-Version` možností.

## <a name="options"></a>Možnosti

- **`-ConfigFile`**

  Konfigurační soubor NuGet, který se má použít Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows) nebo `~/.nuget/NuGet/NuGet.Config` nebo `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-DependencyVersion`**

  *(4.4 +)* Verze balíčků závislostí, které se mají použít, což může být jedna z následujících:<br/><ul><li>*Nejnižší* (výchozí): nejnižší verze</li><li>*HighestPatch*: verze, která má nejnižší hlavní, nejnižší podverzi, nejvyšší opravu</li><li>*HighestMinor*: verze s nejnižší hlavní, nejvyšší podverze a nejvyšší opravou</li><li>*Nejvyšší*: nejvyšší verze</li><li>*Ignorovat*: nebudou použity žádné balíčky závislostí.</li></ul>

- **`-DirectDownload`**

  Přímo si stáhněte bez naplnění jakýchkoli mezipamětí s metadaty nebo binárními soubory.

- **`-DisableParallelProcessing`**

  Zakáže instalaci více balíčků paralelně.

- **`-x|-ExcludeVersion`**

  Nainstaluje balíček do složky s názvem pouze s názvem balíčku a číslem verze.

- **`-FallbackSource`**

  *(3.2 +)* Seznam zdrojů balíčků, které se použijí jako záložní pro případ, že se balíček nenajde v primárním nebo výchozím zdroji.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Vynutí spuštění nuget.exe s využitím neutrální jazykové verze založené na angličtině.

- **`-Framework`**

  *(4.4 +)* Cílové rozhraní, které se používá pro výběr závislostí. Pokud není zadaný, použije se výchozí hodnota any.

- **`-?|-help`**

  Zobrazí informace o nápovědě k příkazu.

- **`-NoCache`**

  Zabraňuje balíčku NuGet v použití balíčků v mezipaměti. Viz [Správa globálních balíčků a složek mezipaměti](../../consume-packages/managing-the-global-packages-and-cache-folders.md).

- **`-NonInteractive`**

  Potlačí výzvy pro vstup uživatele nebo potvrzení.

- **`-OutputDirectory`**

  Určuje složku, ve které jsou balíčky nainstalované. Pokud není zadána žádná složka, je použita aktuální složka.

- **`-PackageSaveMode`**

  Určuje typy souborů, které se uloží po instalaci balíčku: jedna z hodnot `nuspec` , `nupkg` nebo `nuspec;nupkg` .

- **`-PreRelease`**

  Umožňuje instalaci předprodejních balíčků. Tento příznak není požadován při obnovování balíčků pomocí `packages.config` .

- **`-RequireConsent`**

  Ověřuje, jestli je před stažením a instalací balíčků povolený obnovování balíčků. Podrobnosti najdete v tématu věnovaném [obnovení balíčků](../../consume-packages/package-restore.md).

- **`-SolutionDirectory`**

  Určuje kořenovou složku řešení, pro kterou mají být balíčky obnoveny.

- **`-Source`**

   Určuje seznam zdrojů balíčků (jako adresy URL), které se mají použít. Pokud je tato hodnota vynechána, příkaz použije zdroje zadané v konfiguračních souborech, viz [běžné konfigurace NuGet](../../consume-packages/configuring-nuget-behavior.md).

- **`-Verbosity [normal|quiet|detailed]`**

  Určuje množství podrobností zobrazených ve výstupu: `normal` (výchozí), `quiet` nebo `detailed` .

- **`-Version`**

  Určuje verzi balíčku, který se má nainstalovat.

Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .

## <a name="examples"></a>Příklady

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
