---
title: Příkaz aktualizace NuGet rozhraní příkazového řádku
description: Referenční dokumentace pro příkaz nuget.exe aktualizace
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 39e269b10a0cf144d5971d2af9f82a606e0b6904
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817704"
---
# <a name="update-command-nuget-cli"></a>Příkaz update (NuGet CLI)

**Platí pro:** balíček spotřeba &bullet; **podporované verze:** všechny

Aktualizuje všechny balíčky v projektu (pomocí `packages.config`) na jejich nejnovější verze, k dispozici. Doporučuje se spouštět ['Obnovení'](cli-ref-restore.md) dřív, než spustíte `update`. (Chcete-li aktualizovat jednotlivých balíčků, použijte [ `nuget install` ](cli-ref-install.md) bez zadání číslem verze, ve kterém případu NuGet nainstaluje nejnovější verzi.)

Poznámka: `update` pomocí rozhraní příkazového řádku při použití formátu PackageReference spuštěna pod Mono (Mac OSX nebo Linux) nebo nefunguje.

`update` Příkaz aktualizuje také odkazy na sestavení v souboru projektu, zadaný těch, které odkazuje již existuje. Pokud aktualizovaný balíček přidané sestavení, nový odkaz je *není* přidat. Nové závislosti balíčků také nemají jejich odkazy na sestavení, který je přidán. Chcete-li zahrnout tyto operace aktualizace, aktualizujte balíček v sadě Visual Studio pomocí uživatelského rozhraní Správce balíčků nebo konzole Správce balíčků.

Tento příkaz lze použít také k aktualizaci nuget.exe samotné pomocí *-self* příznak.

## <a name="usage"></a>Použití

```cli
nuget update <configPath> [options]
```

kde `<configPath>` identifikuje buď `packages.config` nebo soubor řešení, která uvádí závislosti projektu.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| ConfigFile | Konfigurační soubor NuGet použít. Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.|
| FileConflictAction | Určuje akci, kterou provést, pokud se zobrazí výzva k přepsání nebo ignorovat existující soubory, které se odkazuje na projekt. Hodnoty jsou *přepsat, ignorovat, none*. |
| ForceEnglishOutput | *(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze. |
| Nápověda | Zobrazí nápovědu pro příkaz. |
| ID | Určuje seznam balíčku ID aktualizovat. |
| MSBuildPath | *(4.0 +)*  Určuje cestu MSBuild používat pomocí příkazu, přednost před `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)*  Určuje verzi nástroje MSBuild k použití se tento příkaz. Podporované hodnoty jsou 4, 12, 14, 15. Ve výchozím nastavení je zachyceny MSBuild ve své cestě jinak bude výchozí nejvyšší nainstalovanou verzi nástroje MSBuild. |
| Neinteraktivní | Potlačí výzvy pro vstup uživatele nebo potvrzení. |
| Předběžné verze | Umožňuje aktualizaci na předprodejní verze. Tento příznak se nevyžaduje při aktualizaci předběžné verze balíčků, které jsou již nainstalovány. |
| RepositoryPath | Určuje místní složku, ve kterém jsou nainstalované balíčky. |
| Bezpečné | Určuje, který aktualizuje pouze s nejvyšší verzi k dispozici v rámci stejnou hlavní a vedlejší verzi jako nainstaluje s nainstalovaným balíčkem. |
| Vlastní | Nuget.exe aktualizace na nejnovější verzi; všechny další argumenty se ignorují. |
| Zdroj | Určuje seznam zdrojů balíčku (jako adresy URL) pro aktualizace. Pokud tento parametr vynechán, příkaz používá zdrojů, součástí konfigurační soubory, najdete v části [konfigurace NuGet chování](../consume-packages/configuring-nuget-behavior.md). |
| Podrobnosti | Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*. |
| Version | Při použití s jedno ID balíčku, určuje verzi balíčku aktualizace. |

Viz také [proměnné prostředí](cli-ref-environment-variables.md)

## <a name="examples"></a>Příklady

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
