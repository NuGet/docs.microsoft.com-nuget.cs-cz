---
title: Aktualizace příkazu rozhraní příkazového řádku NuGet
description: Referenční informace pro příkaz update nuget.exe
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a242d02a54fd86899cbe274ab63538b53307c1bb
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67425922"
---
# <a name="update-command-nuget-cli"></a>Příkaz update (NuGet CLI)

**Platí pro:** balíček spotřeby &bullet; **podporované verze:** všechny

Aktualizuje všechny balíčky v projektu (pomocí `packages.config`) jejich nejnovější dostupné verze. Doporučuje se spouštět ["obnovit"](cli-ref-restore.md) dřív, než spustíte `update`. (K aktualizaci jednotlivých balíčků, použijte [ `nuget install` ](cli-ref-install.md) bez zadání číslo verze, ve kterém případu NuGet nainstaluje nejnovější verzi.)

Poznámka: `update` nefunguje pro rozhraní příkazového řádku s mono (Mac OS x nebo Linux) nebo při použití formátu PackageReference.

`update` Příkaz aktualizuje také odkazy na sestavení v souboru projektu, pokud jsou již odkazuje existovat. Pokud aktualizovaný balíček má přidání sestavení, je nový odkaz *není* přidán. Nové závislosti balíčků také nemají přidání jejich odkazů na sestavení. Chcete-li zahrnout tyto operace aktualizace, aktualizujte balíček v sadě Visual Studio pomocí uživatelského rozhraní Správce balíčků nebo konzole Správce balíčků.

Tento příkaz slouží také k aktualizaci nuget.exe samotný pomocí *-self* příznak.

## <a name="usage"></a>Použití

```cli
nuget update <configPath> [options]
```

kde `<configPath>` identifikuje buď `packages.config` nebo soubor řešení, která obsahuje seznam závislostí projektu.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| ConfigFile | Konfigurační soubor NuGet použít. Pokud není zadán, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.|
| FileConflictAction | Určuje akce má být provedena, když se zobrazí výzva k přepsání nebo ignorovat existující soubory, které jsou odkazované projektem. Hodnoty jsou *přepsat, ignorovat, none*. |
| ForceEnglishOutput | *(3.5 +)*  Vynutí nuget.exe pro spuštění pomocí neutrální, základem je angličtina jazyková verze. |
| Help | Zobrazí nápovědu pro příkaz. |
| Id | Určuje seznam ID k aktualizaci balíčku. |
| MSBuildPath | *(4.0 +)*  Určuje cestu k používání pomocí příkazu, přednost `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)*  Určuje verzi Msbuildu, který se má použít tento příkaz. Podporované hodnoty jsou 4, 12, 14, 15.1, 15.3, 15.4, 15.5, verzi 15.6, 15.7, 15.8, 15.9. Ve výchozím nastavení se vybere MSBuild na vaší cestě jinak je výchozí hodnotou nejvyšší nainstalovaná verze Msbuildu. |
| NonInteractive | Potlačí vyzve k zadání uživatele o vstup ani potvrzení. |
| Platnost předběžné verze | Umožňuje aktualizaci pro předběžné verze. Tento příznak není potřeba při aktualizaci předběžné verze balíčků, které jsou již nainstalovány. |
| RepositoryPath | Určuje místní složku, ve kterém jsou nainstalované balíčky. |
| Bezpečné | Určuje, která aktualizuje pouze s nejvyšší verze k dispozici v rámci stejné hlavní a dílčí verze jako nainstalovaného balíčku se nainstaluje. |
| Vlastní | Aktualizuje na nejnovější verzi; nuget.exe Další argumenty jsou ignorovány. |
| Source | Určuje seznam zdrojů balíčků (jako adresy URL) použít pro aktualizace. Pokud tento parametr vynechán, příkaz používá zdroje k dispozici v konfiguračních souborech naleznete v tématu [konfigurace běžných NuGet](../consume-packages/configuring-nuget-behavior.md). |
| Verbosity | Určuje množství podrobností, na které se zobrazí ve výstupu: *normální*, *quiet*, *podrobné*. |
| Version | Zadáním jednoho ID balíčku, určuje verzi balíčku aktualizace. |

Viz také [proměnné prostředí](cli-ref-environment-variables.md)

## <a name="examples"></a>Příklady

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
