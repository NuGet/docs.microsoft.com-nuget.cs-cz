---
title: Příkaz NuGet CLI Update
description: Referenční informace k příkazu NuGet. exe Update
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: b5da09c3dd6ffa0ce1b7b44731ed67ddd0336c58
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328255"
---
# <a name="update-command-nuget-cli"></a>Příkaz update (NuGet CLI)

**Platí pro:** &bullet; **podporované verze balíčku:** vše

Aktualizuje všechny balíčky v projektu (pomocí `packages.config`) na nejnovější dostupné verze. Před spuštěním `update` [nástroje](cli-ref-restore.md) se doporučuje spustit příkaz Restore. (Pokud chcete aktualizovat jednotlivý balíček, [`nuget install`](cli-ref-install.md) použijte bez zadání čísla verze. v takovém případě NuGet nainstaluje nejnovější verzi.)

Poznámka: `update` nefunguje s rozhraním příkazového řádku spuštěným v mono (Mac OSX nebo Linux) nebo při použití formátu PackageReference.

`update` Příkaz také aktualizuje odkazy na sestavení v souboru projektu za předpokladu, že tyto odkazy již existují. Pokud aktualizovaný balíček obsahuje přidané sestavení, nový odkaz se *nepřidá.* Nové závislosti balíčků také nemají přidané odkazy na sestavení. Chcete-li zahrnout tyto operace jako součást aktualizace, aktualizujte balíček v aplikaci Visual Studio pomocí uživatelského rozhraní Správce balíčků nebo konzoly Správce balíčků.

Tento příkaz lze také použít k aktualizaci souboru NuGet. exe pomocí příznaku *-vlastní* .

## <a name="usage"></a>Použití

```cli
nuget update <configPath> [options]
```

kde `<configPath>` identifikuje`packages.config` buď soubor řešení nebo, který obsahuje seznam závislostí projektu.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| ConfigFile | Konfigurační soubor NuGet, který se má použít Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows `~/.nuget/NuGet/NuGet.Config` ) nebo (Mac/Linux).|
| FileConflictAction | Určuje akci, která se má provést, když se zobrazí výzva k přepsání nebo ignorování existujících souborů, na které se odkazuje v projektu. Hodnoty jsou *přepisované, ignore, None*. |
| ForceEnglishOutput | *(3.5 +)* Vynutí, aby soubor NuGet. exe běžel pomocí neutrální jazykové verze určené pro angličtinu. |
| Help | Zobrazí informace o nápovědě k příkazu. |
| Id | Určuje seznam ID balíčků, které se mají aktualizovat. |
| MSBuildPath | *(4.0 +)* Určuje cestu nástroje MSBuild, který má být použit s příkazem, přičemž přednost `-MSBuildVersion`využije. |
| MSBuildVersion | *(3.2 +)* Určuje verzi nástroje MSBuild, která má být použita s tímto příkazem. Podporované hodnoty jsou 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. Ve výchozím nastavení je nástroj MSBuild v cestě vybrán, jinak má výchozí nejvyšší nainstalovanou verzi nástroje MSBuild. |
| NonInteractive | Potlačí výzvy pro vstup uživatele nebo potvrzení. |
| Předběžné verze | Umožňuje aktualizaci předprodejních verzí. Tento příznak není požadován při aktualizaci předprodejních balíčků, které jsou již nainstalovány. |
| RepositoryPath | Určuje místní složku, ve které jsou balíčky nainstalované. |
| Odvod | Určuje, že se budou instalovat jenom aktualizace s nejvyšší verzí dostupnou v rámci stejné hlavní a dílčí verze, jako je nainstalovaný balíček. |
| Samorozbalující | Aktualizuje NuGet. exe na nejnovější verzi. všechny ostatní argumenty jsou ignorovány. |
| Source | Určuje seznam zdrojů balíčků (jako adresy URL), které se mají použít pro aktualizace. Pokud je tato hodnota vynechána, příkaz použije zdroje zadané v konfiguračních souborech, viz [běžné konfigurace NuGet](../../consume-packages/configuring-nuget-behavior.md). |
| Verbosity | Určuje množství podrobností zobrazených ve výstupu: *normální*, tiché a *podrobné*. |
| Version | Při použití s jedním ID balíčku určuje verzi balíčku, který se má aktualizovat. |

Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .

## <a name="examples"></a>Příklady

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
