---
title: Rozhraní příkazového řádku NuGet místních hodnot
description: Referenční informace pro příkaz nuget.exe místních hodnot
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: ea216c4651ba9619bc3b6a7ab52546fd299b0bb6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545025"
---
# <a name="locals-command-nuget-cli"></a>Příkaz local (NuGet CLI)

**Platí pro:** balíček spotřeby &bullet; **podporované verze:** 3.3 +

Vymaže nebo vypíše místní prostředky NuGet, jako *http-cache*, *global-packages* složek a dočasné složky. `locals` Příkaz lze také zobrazit seznam těchto umístěních. Další informace najdete v tématu [Správa globálních balíčků a složek mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md).

## <a name="usage"></a>Použití

```cli
nuget locals <folder> [options]
```

kde `<folder>` je jedním z `all`, `http-cache`, `packages-cache` *(3.5 a starší)*, `global-packages`, `temp` *(3.4 +)*, a `plugins-cache` *(4.8 +)*.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| Vymazat | Vymaže zadané složky. |
| ConfigFile | Konfigurační soubor NuGet použít. Pokud není zadán, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.|
| ForceEnglishOutput | *(3.5 +)*  Vynutí nuget.exe pro spuštění pomocí neutrální, základem je angličtina jazyková verze. |
| Nápověda | Zobrazí nápovědu pro příkaz. |
| Seznam | Zobrazí seznam umístění zadaná složka nebo umístění všech složek, při použití s *všechny*. |
| Neinteraktivní | Potlačí vyzve k zadání uživatele o vstup ani potvrzení. |
| Podrobnosti | Určuje množství podrobností, na které se zobrazí ve výstupu: *normální*, *quiet*, *podrobné*. |

Viz také [proměnné prostředí](cli-ref-environment-variables.md)

## <a name="examples"></a>Příklady

```cli
nuget locals all -list
nuget locals http-cache -clear
```

Další příklady najdete v tématu [Správa globálních balíčků a složek mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md).
