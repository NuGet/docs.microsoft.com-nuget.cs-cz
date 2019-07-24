---
title: Instalační příkaz NuGet CLI
description: Reference k instalačnímu příkazu NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f39bcc67c5f659f05ef02f2579bcf07b4481bb27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328339"
---
# <a name="install-command-nuget-cli"></a>Příkaz install (NuGet CLI)

**Platí pro:** &bullet; **podporované verze balíčku:** vše

Stáhne a nainstaluje balíček do projektu, přičemž se použije jako výchozí pro aktuální složku pomocí zadaných zdrojů balíčků.

> [!Tip]
> Chcete-li stáhnout balíček přímo mimo kontext projektu, navštivte stránku balíčku na [NuGet.org](https://www.nuget.org) a vyberte odkaz **ke stažení** .

Pokud nejsou zadány žádné zdroje, budou použity hodnoty uvedené v globálním konfiguračním `%appdata%\NuGet\NuGet.Config` souboru (Windows) `~/.nuget/NuGet/NuGet.Config` nebo (Mac/Linux). Další podrobnosti najdete v tématu [běžné konfigurace NuGet](../../consume-packages/configuring-nuget-behavior.md) .

Pokud nejsou zadány žádné konkrétní balíčky `install` , aplikace nainstaluje všechny balíčky uvedené v `packages.config` souboru projektu a bude tak [`restore`](cli-ref-restore.md)vypadat podobně jako.

Příkaz neupraví soubor projektu nebo `packages.config`; tímto `restore` způsobem je podobný jako v tom, že přidá pouze balíčky na disk, ale nemění závislosti projektu. `install`

Chcete-li přidat závislost, buď přidejte balíček prostřednictvím uživatelského rozhraní nebo konzoly Správce balíčků v aplikaci Visual Studio, nebo `packages.config` upravte a potom spusťte `install` buď `restore`nebo.

## <a name="usage"></a>Použití

```cli
nuget install <packageID | configFilePath> [options]
```

kde `<packageID>` pojmenuje balíček k instalaci (pomocí nejnovější verze) nebo `<configFilePath>` identifikuje `packages.config` soubor, který obsahuje seznam balíčků, které se mají nainstalovat. Můžete určit konkrétní verzi s `-Version` možností.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| ConfigFile | Konfigurační soubor NuGet, který se má použít Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows `~/.nuget/NuGet/NuGet.Config` ) nebo (Mac/Linux).|
| DependencyVersion | *(4.4 +)* Verze balíčků závislostí, které se mají použít, což může být jedna z následujících:<br/><ul><li>*Nejnižší* (výchozí): nejnižší verze</li><li>*HighestPatch*: verze, která má nejnižší hlavní, nejnižší podverzi, nejvyšší opravu</li><li>*HighestMinor*: verze s nejnižší hlavní, nejvyšší podverze a nejvyšší opravou</li><li>*Nejvyšší*: nejvyšší verze</li></ul> |
| DisableParallelProcessing | Zakáže instalaci více balíčků paralelně. |
| ExcludeVersion | Nainstaluje balíček do složky s názvem pouze s názvem balíčku a číslem verze. |
| FallbackSource | *(3.2 +)* Seznam zdrojů balíčků, které se použijí jako záložní pro případ, že se balíček nenajde v primárním nebo výchozím zdroji. |
| ForceEnglishOutput | *(3.5 +)* Vynutí, aby soubor NuGet. exe běžel pomocí neutrální jazykové verze určené pro angličtinu. |
| Rozhraní .NET Framework | *(4.4 +)* Cílové rozhraní, které se používá pro výběr závislostí. Pokud není zadaný, použije se výchozí hodnota any. |
| Help | Zobrazí informace o nápovědě k příkazu. |
| NoCache | Zabraňuje balíčku NuGet v použití balíčků v mezipaměti. Viz [Správa globálních balíčků a složek mezipaměti](../../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NonInteractive | Potlačí výzvy pro vstup uživatele nebo potvrzení. |
| OutputDirectory | Určuje složku, ve které jsou balíčky nainstalované. Pokud není zadána žádná složka, je použita aktuální složka. |
| PackageSaveMode | Určuje typy souborů, které se uloží po instalaci balíčku: jedna z `nuspec`hodnot `nupkg`, nebo `nuspec;nupkg`. |
| Předběžné verze | Umožňuje instalaci předprodejních balíčků. Tento příznak není požadován při obnovování balíčků pomocí `packages.config`. |
| RequireConsent | Ověřuje, jestli je před stažením a instalací balíčků povolený obnovování balíčků. Podrobnosti najdete v tématu věnovaném [obnovení balíčků](../../consume-packages/package-restore.md). |
| SolutionDirectory | Určuje kořenovou složku řešení, pro kterou mají být balíčky obnoveny. |
| Source | Určuje seznam zdrojů balíčků (jako adresy URL), které se mají použít. Pokud je tato hodnota vynechána, příkaz použije zdroje zadané v konfiguračních souborech, viz [běžné konfigurace NuGet](../../consume-packages/configuring-nuget-behavior.md). |
| Verbosity | Určuje množství podrobností zobrazených ve výstupu: *normální*, tiché a *podrobné*. |
| Version | Určuje verzi balíčku, který se má nainstalovat. |

Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .

## <a name="examples"></a>Příklady

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
