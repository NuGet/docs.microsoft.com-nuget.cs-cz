---
title: Rozhraní příkazového řádku NuGet přidat – příkaz
description: Referenční dokumentace pro nuget.exe přidat – příkaz
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f229ca100463c556f9c4cefc49f52724a9c4ba77
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817607"
---
# <a name="add-command-nuget-cli"></a>Příkaz add (NuGet CLI)

**Platí pro**: balíček publikování &bullet; **podporované verze**: 3.3 +

Přidá zadaný balíček zdroj balíčku jiným protokolem než HTTP (složka nebo cesta UNC) v hierarchickém rozložení, ve kterém se vytvoří složky pro číslo ID a verzi balíčku. Příklad:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

Při obnovení nebo aktualizaci na zdroji balíčku, hierarchickém rozložení poskytuje výrazně lepší výkon.

Všechny soubory v balíčku rozšířit do cílového zdroje balíčku, použít `-Expand` přepínače. To obvykle vede k další podsložky zobrazovaných v cílovém umístění, jako například `tools` a `lib`.

## <a name="usage"></a>Použití

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

kde `<packagePath>` je název cesty k balíčku, který chcete přidat, a `<sourcePath>` určuje zdroji na základě složky balíčku, do které budou přidány balíčku. Zdroje protokolu HTTP nejsou podporovány.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| ConfigFile | Konfigurační soubor NuGet použít. Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.|
| Rozbalte položku | Přidá všechny soubory v balíčku ke zdroji balíčku. |
| ForceEnglishOutput | *(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze. |
| Nápověda | Zobrazí nápovědu pro příkaz. |
| Neinteraktivní | Potlačí výzvy pro vstup uživatele nebo potvrzení. |
| Podrobnosti | Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*. |

Viz také [proměnné prostředí](cli-ref-environment-variables.md)

## <a name="examples"></a>Příklady

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
