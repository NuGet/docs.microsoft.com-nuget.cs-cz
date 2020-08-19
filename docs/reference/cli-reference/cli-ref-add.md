---
title: NuGet CLI – příkaz Add
description: Referenční informace o příkazu nuget.exe Add
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 89d268946243e8eae07e482db48e809a15260c38
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622899"
---
# <a name="add-command-nuget-cli"></a>Add – příkaz (NuGet CLI)

**Platí pro**: publikování &bullet; **podporovaných verzí**balíčku: 3.3 +

Přidá zadaný balíček do zdroje nepřipojeného balíčku protokolu HTTP (složka nebo cesta UNC) v hierarchickém rozložení, kde jsou vytvářeny složky pro ID a číslo verze balíčku. Příklad:

```
\\myserver\packages
  └─<packageID>
    └─<version>
      ├─<packageID>.<version>.nupkg
      ├─<packageID>.<version>.nupkg.sha512
      └─<packageID>.nuspec
```

Při obnovení nebo aktualizaci zdroje balíčku poskytuje hierarchické rozložení významně lepší výkon.

K rozbalení všech souborů v balíčku do cílového zdroje balíčků použijte `-Expand` přepínač. To obvykle vede k tomu, že se v cíli objeví další podsložky, například `tools` a `lib` .

## <a name="usage"></a>Využití

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

kde `<packagePath>` je cesta k balíčku, který se má přidat, a `<sourcePath>` Určuje zdroj balíčku na bázi složky, do kterého se balíček přidá. Zdroje HTTP nejsou podporovány.

## <a name="options"></a>Možnosti

- **`-ConfigFile`**

  Konfigurační soubor NuGet, který se má použít Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows) nebo `~/.nuget/NuGet/NuGet.Config` nebo `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-Expand`**

  Přidá všechny soubory v balíčku do zdroje balíčku.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Vynutí spuštění nuget.exe s využitím neutrální jazykové verze založené na angličtině.
Vynutí spuštění nuget.exe s využitím neutrální jazykové verze založené na angličtině.

- **`-?|-help`**

  Zobrazí informace o nápovědě k příkazu.

- **`-NonInteractive`**

  Potlačí výzvy pro vstup uživatele nebo potvrzení.

- **`-src|-Source`**

   Určuje zdroj balíčku, což je složka nebo sdílená složka UNC, do které se nupkg přidá. Zdroje http nejsou podporovány.

- **`-Verbosity [normal|quiet|detailed]`**

  Určuje množství podrobností zobrazených ve výstupu: `normal` (výchozí), `quiet` nebo `detailed` .

Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .

## <a name="examples"></a>Příklady

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
