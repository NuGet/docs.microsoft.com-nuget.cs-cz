---
title: NuGet CLI – příkaz místních hodnot
description: Referenční informace o příkazu NuGet. exe Locals
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: b02360c38ad66c95bbe3c7d403ef4a959112c91a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328345"
---
# <a name="locals-command-nuget-cli"></a>Příkaz local (NuGet CLI)

**Platí pro:** &bullet; **podporované verze balíčku:** 3.3+

Vymaže nebo vypíše místní prostředky NuGet, například složku *HTTP-cache*, *Global-Packages* a Temp. `locals` Příkaz lze také použít k zobrazení seznamu těchto umístění. Další informace najdete v tématu [Správa globálních balíčků a složek mezipaměti](../../consume-packages/managing-the-global-packages-and-cache-folders.md).

## <a name="usage"></a>Použití

```cli
nuget locals <folder> [options]
```

kde `<folder>` je jedna z `all`, `http-cache` `global-packages` `temp` `plugins-cache` , `packages-cache` *(3,5 a starší)* ,, *(3.4 +)* a *(4.8 +)* .

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| Vymazat | Vymaže určenou složku. |
| ConfigFile | Konfigurační soubor NuGet, který se má použít Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows `~/.nuget/NuGet/NuGet.Config` ) nebo (Mac/Linux).|
| ForceEnglishOutput | *(3.5 +)* Vynutí, aby soubor NuGet. exe běžel pomocí neutrální jazykové verze určené pro angličtinu. |
| Help | Zobrazí informace o nápovědě k příkazu. |
| Seznam | Vypíše umístění zadané složky nebo umístění všech složek při použití se *všemi*. |
| NonInteractive | Potlačí výzvy pro vstup uživatele nebo potvrzení. |
| Verbosity | Určuje množství podrobností zobrazených ve výstupu: *normální*, tiché a *podrobné*. |

Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .

## <a name="examples"></a>Příklady

```cli
nuget locals all -list
nuget locals http-cache -clear
```

Další příklady najdete v tématu [Správa globálních balíčků a složek mezipaměti](../../consume-packages/managing-the-global-packages-and-cache-folders.md).
