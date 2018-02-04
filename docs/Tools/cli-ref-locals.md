---
title: "Příkaz místní hodnoty – NuGet rozhraní příkazového řádku | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenční dokumentace pro nuget.exe místní hodnoty – příkaz"
keywords: "místní hodnoty – odkaz nuget, místní hodnoty – příkaz"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b2f62a9ab5699bfb486eee146ab7046f5240aa50
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/02/2018
---
# <a name="locals-command-nuget-cli"></a>místní hodnoty – příkaz (NuGet CLI)

**Platí pro:** balíček spotřeba &bullet; **podporované verze:** 3.3 +

Vymaže nebo vypíše místní prostředky NuGet například mezipaměti požadavek http, mezipaměti balíčky a složka globální balíčky celého systému. `locals` Příkaz lze použít také zobrazíte seznam těchto umístěních. Další informace najdete v tématu [Správa mezipaměti NuGet](../consume-packages/managing-the-nuget-cache.md).

## <a name="usage"></a>Použití

```cli
nuget locals <cache> [options]
```

kde `<cache>` je jedním z `all`, `http-cache`, `packages-cache`, `global-packages`, a `temp` *(3.4 +)*.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| Zrušte zaškrtnutí | Zadaný mezipaměť nevymaže. |
| ConfigFile | Konfigurační soubor NuGet použít. Pokud není zadaný, *%AppData%\NuGet\NuGet.Config* se používá. |
| ForceEnglishOutput | *(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze. |
| Nápověda | Zobrazí nápovědu pro příkaz. |
| Seznam | Zobrazí seznam umístění zadaná mezipaměti nebo umístění všechny mezipaměti při použití s *všechny*. |
| Neinteraktivní | Potlačí výzvy pro vstup uživatele nebo potvrzení. |
| Podrobnosti | Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*. |

Viz také [proměnné prostředí](cli-ref-environment-variables.md)

## <a name="examples"></a>Příklady

```cli
nuget locals all -list
nuget locals http-cache -clear
```
