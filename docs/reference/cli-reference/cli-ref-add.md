---
title: NuGet CLI – příkaz Add
description: Referenční informace o příkazu NuGet. exe Add
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328360"
---
# <a name="add-command-nuget-cli"></a>Příkaz add (NuGet CLI)

**Platí pro**: publikování &bullet; **podporovaných verzí**balíčku: 3.3+

Přidá zadaný balíček do zdroje nepřipojeného balíčku protokolu HTTP (složka nebo cesta UNC) v hierarchickém rozložení, kde jsou vytvářeny složky pro ID a číslo verze balíčku. Příklad:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

Při obnovení nebo aktualizaci zdroje balíčku poskytuje hierarchické rozložení významně lepší výkon.

K rozbalení všech souborů v balíčku do cílového zdroje balíčků použijte `-Expand` přepínač. To obvykle vede k tomu, že se v cíli objeví další podsložky `tools` , `lib`například a.

## <a name="usage"></a>Použití

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

kde `<packagePath>` je cesta k balíčku, který se má přidat, `<sourcePath>` a určuje zdroj balíčku na bázi složky, do kterého se balíček přidá. Zdroje HTTP nejsou podporovány.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| ConfigFile | Konfigurační soubor NuGet, který se má použít Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows `~/.nuget/NuGet/NuGet.Config` ) nebo (Mac/Linux).|
| Expand | Přidá všechny soubory v balíčku do zdroje balíčku. |
| ForceEnglishOutput | *(3.5 +)* Vynutí, aby soubor NuGet. exe běžel pomocí neutrální jazykové verze určené pro angličtinu. |
| Help | Zobrazí informace o nápovědě k příkazu. |
| NonInteractive | Potlačí výzvy pro vstup uživatele nebo potvrzení. |
| Verbosity | Určuje množství podrobností zobrazených ve výstupu: *normální*, tiché a *podrobné*. |

Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .

## <a name="examples"></a>Příklady

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
