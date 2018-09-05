---
title: Rozhraní příkazového řádku NuGet init
description: Referenční informace pro příkaz init nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551407"
---
# <a name="init-command-nuget-cli"></a>příkaz init (rozhraní příkazového řádku NuGet)

**Platí pro:** vytvoření balíčku &bullet; **podporované verze:** 3.3 +

Zkopíruje všechny balíčky z plochého složky do cílové složky pomocí hierarchickém rozložení, jak je popsáno [přidat příkaz](cli-ref-add.md). To znamená, že použití `init` je ekvivalentní k použití `add` příkaz na každý balíček ve složce.

Stejně jako u `add`, cíl musí být místní složku nebo cesty UNC. Úložiště balíčku HTTP jako je nuget.org nebo privátní servery nejsou podporovány.

## <a name="usage"></a>Použití

```cli
nuget init <source> <destination> [options]
```

kde `<source>` je složku, která obsahuje balíčky a `<destination>` je místní složka nebo cesta UNC, do které se zkopírují balíčky.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| ConfigFile | Konfigurační soubor NuGet použít. Pokud není zadán, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.|
| ForceEnglishOutput | *(3.5 +)*  Vynutí nuget.exe pro spuštění pomocí neutrální, základem je angličtina jazyková verze. |
| Rozbalte položku | Přidá všechny soubory v každý balíček, který je přidán ke zdroji balíčku; stejné jako `-Expand` s `add` příkazu. |
| Nápověda | Zobrazí nápovědu pro příkaz. |
| Neinteraktivní | Potlačí vyzve k zadání uživatele o vstup ani potvrzení. |
| Podrobnosti | Určuje množství podrobností, na které se zobrazí ve výstupu: *normální*, *quiet*, *podrobné*. |

Viz také [proměnné prostředí](cli-ref-environment-variables.md)

## <a name="examples"></a>Příklady

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
