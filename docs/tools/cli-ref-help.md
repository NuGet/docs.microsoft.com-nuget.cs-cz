---
title: Příkaz help NuGet rozhraní příkazového řádku
description: Referenční informace pro příkaz help nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546560"
---
# <a name="help-or--command-nuget-cli"></a>help or ? Příkaz (NuGet CLI)

**Platí pro:** všechny &bullet; **podporované verze**: všechny

Zobrazí obecné pomůže informace a informace o konkrétní příkazy.

## <a name="usage"></a>Použití

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

kde [příkaz] označuje ke konkrétnímu příkazu, pro které chcete zobrazit nápovědu.

> [!Warning]
> U některých příkazů, mějte k určení *pomáhají* , jako první se `nuget help install`, protože je balíček s názvem "Nápověda" na nuget.org. Pokud dáte příkaz `nuget install help`, nebude získat pomoc na instalačního příkazu, ale místo toho nainstaluje balíček s názvem nápovědy.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| Všechny | Tisk podrobnou nápovědu pro všechny dostupné příkazy. ignoruje, pokud je zadána ke konkrétnímu příkazu. |
| ConfigFile | Konfigurační soubor NuGet použít. Pokud není zadán, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.|
| ForceEnglishOutput | *(3.5 +)*  Vynutí nuget.exe pro spuštění pomocí neutrální, základem je angličtina jazyková verze. |
| Nápověda | Zobrazí nápovědu pro příkaz help, samotného. |
| Markdown | Tisk podrobnou nápovědu ve formátu markdown zadáním `-All`. Jinak ignorována. |
| Neinteraktivní | Potlačí vyzve k zadání uživatele o vstup ani potvrzení. |
| Podrobnosti | Určuje množství podrobností, na které se zobrazí ve výstupu: *normální*, *quiet*, *podrobné*. |

Viz také [proměnné prostředí](cli-ref-environment-variables.md)

## <a name="examples"></a>Příklady

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
