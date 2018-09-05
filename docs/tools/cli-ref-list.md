---
title: Příkaz listovat NuGet rozhraní příkazového řádku
description: Referenční informace pro příkaz seznamu nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549798"
---
# <a name="list-command-nuget-cli"></a>příkaz listovat (rozhraní příkazového řádku NuGet)

**Platí pro:** využití balíčků, publikováním &bullet; **podporované verze:** všechny

Zobrazí seznam balíčků z daného zdroje. Pokud nejsou zadány žádné zdroje, všechny zdroje definované v souboru globální konfiguraci `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config`, se používají. Pokud `NuGet.Config` žádné zdroje, pak určuje `list` používá výchozí kanál (nuget.org).

## <a name="usage"></a>Použití

```cli
nuget list [search terms] [options]
```

volitelné hledané výrazy ve kterém se filtr pro zobrazený seznam. Hledané termíny se použijí na názvy balíčků, značky a Popis balíčku, stejně jako při použití na nuget.org.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| AllVersions | Zobrazí seznam všech verzí balíčku. Ve výchozím nastavení zobrazí se pouze nejnovější verze balíčku. |
| ConfigFile | Konfigurační soubor NuGet použít. Pokud není zadán, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.|
| ForceEnglishOutput | *(3.5 +)*  Vynutí nuget.exe pro spuštění pomocí neutrální, základem je angličtina jazyková verze. |
| Nápověda | Zobrazí nápovědu pro příkaz. |
| IncludeDelisted | *(3.2 +)*  Zobrazit neuvedené v seznamu balíčků. |
| Neinteraktivní | Potlačí vyzve k zadání uživatele o vstup ani potvrzení. |
| Platnost předběžné verze | Obsahuje předběžné verze balíčků v seznamu. |
| Zdroj | Určuje seznam zdrojů balíčků pro hledání. |
| Podrobnosti | Určuje množství podrobností, na které se zobrazí ve výstupu: *normální*, *quiet*, *podrobné*. |

Viz také [proměnné prostředí](cli-ref-environment-variables.md)

## <a name="examples"></a>Příklady

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
