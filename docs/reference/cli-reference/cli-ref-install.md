---
title: Instalační příkaz NuGet CLI
description: Reference k instalačnímu příkazu NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 6c49b2406462eae6ce45c65dfd8b3a9eb1077e73
ms.sourcegitcommit: 415c70d7014545c1f65271a2debf8c3c1c5eb688
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/06/2020
ms.locfileid: "77036939"
---
# <a name="install-command-nuget-cli"></a>Příkaz install (NuGet CLI)

**Platí pro:** spotřeba balíčku &bullet; **podporovaných verzích:** vše

Stáhne a nainstaluje balíček do projektu, přičemž se použije jako výchozí pro aktuální složku pomocí zadaných zdrojů balíčků.

> [!Tip]
> Chcete-li stáhnout balíček přímo mimo kontext projektu, navštivte stránku balíčku na [NuGet.org](https://www.nuget.org) a vyberte odkaz **ke stažení** .

Pokud nejsou zadány žádné zdroje, budou použity hodnoty uvedené v globálním konfiguračním souboru `%appdata%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux). Další podrobnosti najdete v tématu [běžné konfigurace NuGet](../../consume-packages/configuring-nuget-behavior.md) .

Pokud nejsou zadány žádné konkrétní balíčky, `install` nainstaluje všechny balíčky uvedené v souboru `packages.config` projektu, takže se podobá [`restore`](cli-ref-restore.md).

Příkaz `install` neupraví soubor projektu ani `packages.config`; tímto způsobem je podobný `restore` v tom, že přidává jenom balíčky na disk, ale nemění závislosti projektu.

Chcete-li přidat závislost, buď přidejte balíček prostřednictvím uživatelského rozhraní nebo konzoly Správce balíčků v aplikaci Visual Studio, nebo upravte `packages.config` a potom spusťte buď `install` nebo `restore`.

## <a name="usage"></a>Využití

```cli
nuget install <packageID | configFilePath> [options]
```

kde `<packageID>` pojmenuje balíček k instalaci (pomocí nejnovější verze), nebo `<configFilePath>` identifikuje soubor `packages.config`, který obsahuje seznam balíčků pro instalaci. Konkrétní verzi můžete označit možností `-Version`.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| ConfigFile | Konfigurační soubor NuGet, který se má použít Pokud není zadaný, použije se `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).|
| DependencyVersion | *(4.4 +)* Verze balíčků závislostí, které se mají použít, což může být jedna z následujících:<br/><ul><li>*Nejnižší* (výchozí): nejnižší verze</li><li>*HighestPatch*: verze, která má nejnižší hlavní, nejnižší podverzi, nejvyšší opravu</li><li>*HighestMinor*: verze s nejnižší hlavní, nejvyšší podverze a nejvyšší opravou</li><li>*Nejvyšší*: nejvyšší verze</li><li>*Ignorovat*: nebudou použity žádné balíčky závislostí.</li></ul> |
| DisableParallelProcessing | Zakáže instalaci více balíčků paralelně. |
| ExcludeVersion | Nainstaluje balíček do složky s názvem pouze s názvem balíčku a číslem verze. |
| FallbackSource | *(3.2 +)* Seznam zdrojů balíčků, které se použijí jako záložní pro případ, že se balíček nenajde v primárním nebo výchozím zdroji. |
| ForceEnglishOutput | *(3.5 +)* Vynutí, aby soubor NuGet. exe běžel pomocí neutrální jazykové verze určené pro angličtinu. |
| Rozhraní .NET Framework | *(4.4 +)* Cílové rozhraní, které se používá pro výběr závislostí. Pokud není zadaný, použije se výchozí hodnota any. |
| Nápověda | Zobrazí informace o nápovědě k příkazu. |
| NoCache | Zabraňuje balíčku NuGet v použití balíčků v mezipaměti. Viz [Správa globálních balíčků a složek mezipaměti](../../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NonInteractive | Potlačí výzvy pro vstup uživatele nebo potvrzení. |
| OutputDirectory | Určuje složku, ve které jsou balíčky nainstalované. Pokud není zadána žádná složka, je použita aktuální složka. |
| PackageSaveMode | Určuje typy souborů, které se uloží po instalaci balíčku: jedna z `nuspec`, `nupkg`nebo `nuspec;nupkg`. |
| PreRelease | Umožňuje instalaci předprodejních balíčků. Tento příznak není při obnovování balíčků s `packages.config`požadován. |
| RequireConsent | Ověřuje, jestli je před stažením a instalací balíčků povolený obnovování balíčků. Podrobnosti najdete v tématu věnovaném [obnovení balíčků](../../consume-packages/package-restore.md). |
| SolutionDirectory | Určuje kořenovou složku řešení, pro kterou mají být balíčky obnoveny. |
| Zdroj | Určuje seznam zdrojů balíčků (jako adresy URL), které se mají použít. Pokud je tato hodnota vynechána, příkaz použije zdroje zadané v konfiguračních souborech, viz [běžné konfigurace NuGet](../../consume-packages/configuring-nuget-behavior.md). |
| Podrobnosti | Určuje množství podrobností zobrazených ve výstupu: *normální*, *tiché*a *podrobné*. |
| Version | Určuje verzi balíčku, která se má nainstalovat. |

Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .

## <a name="examples"></a>Příklady

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
