---
title: NuGet CLI – příkaz místních hodnot
description: Reference pro příkaz nuget.exe Locals
author: JonDouglas
ms.author: jodou
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: 25feb29c7b96c47681cedd8208b8595952d3ca49
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779199"
---
# <a name="locals-command-nuget-cli"></a>Locals – příkaz (NuGet CLI)

**Platí pro:** &bullet; **podporované verze balíčku:** 3.3 +

Vymaže nebo vypíše místní prostředky NuGet, například složku *HTTP-cache*, *Global-Packages* a Temp. `locals`Příkaz lze také použít k zobrazení seznamu těchto umístění. Další informace najdete v tématu [Správa globálních balíčků a složek mezipaměti](../../consume-packages/managing-the-global-packages-and-cache-folders.md).

## <a name="usage"></a>Využití

```cli
nuget locals <folder> [options]
```

kde `<folder>` je jedna z `all` , `http-cache` , `packages-cache` *(3,5 a starší)*, `global-packages` , `temp` *(3.4 +)* a `plugins-cache` *(4.8 +)*.

## <a name="options"></a>Možnosti

- **`-Clear`**

  Vymaže určenou složku.

- **`-ConfigFile`**

  Konfigurační soubor NuGet, který se má použít Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows) nebo `~/.nuget/NuGet/NuGet.Config` nebo `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-ForceEnglishOutput`**

  *(3.5 +)* Vynutí spuštění nuget.exe s využitím neutrální jazykové verze založené na angličtině.

- **`-?|-help`**

  Zobrazí informace o nápovědě k příkazu.

- **`-List`**

  Vypíše umístění zadané složky nebo umístění všech složek při použití se *všemi*.

- **`-NonInteractive`**

  Potlačí výzvy pro vstup uživatele nebo potvrzení.

- **`-Verbosity [normal|quiet|detailed]`**

  Určuje množství podrobností zobrazených ve výstupu: `normal` (výchozí), `quiet` nebo `detailed` .

Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .

## <a name="examples"></a>Příklady

```cli
nuget locals all -list
nuget locals http-cache -clear
```

Další příklady najdete v tématu [Správa globálních balíčků a složek mezipaměti](../../consume-packages/managing-the-global-packages-and-cache-folders.md).
