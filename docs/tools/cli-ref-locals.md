---
title: Rozhraní příkazového řádku NuGet místní hodnoty – příkaz
description: Referenční dokumentace pro nuget.exe místní hodnoty – příkaz
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: 90e8c85e7a3e0e9520933e2ddd6dd84447475f2b
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818198"
---
# <a name="locals-command-nuget-cli"></a>Příkaz local (NuGet CLI)

**Platí pro:** balíček spotřeba &bullet; **podporované verze:** 3.3 +

Vymaže nebo vypíše místní prostředky NuGet, jako *http mezipaměti*, *globální balíčky* složku a dočasnou složku. `locals` Příkaz lze použít také zobrazíte seznam těchto umístěních. Další informace najdete v tématu [správy globální balíčky a složky mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md).

## <a name="usage"></a>Použití

```cli
nuget locals <folder> [options]
```

kde `<folder>` je jedním z `all`, `http-cache`, `packages-cache` *(3.5 a starší)*, `global-packages`, a `temp` *(3.4 +)*.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| Zrušte zaškrtnutí | Vymaže do zadané složky. |
| ConfigFile | Konfigurační soubor NuGet použít. Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.|
| ForceEnglishOutput | *(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze. |
| Nápověda | Zobrazí nápovědu pro příkaz. |
| Seznam | Zobrazí seznam umístění do zadané složky nebo umístění všechny složky při použití s *všechny*. |
| Neinteraktivní | Potlačí výzvy pro vstup uživatele nebo potvrzení. |
| Podrobnosti | Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*. |

Viz také [proměnné prostředí](cli-ref-environment-variables.md)

## <a name="examples"></a>Příklady

```cli
nuget locals all -list
nuget locals http-cache -clear
```

Další příklady najdete v tématu [správy globální balíčky a složky mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md).
