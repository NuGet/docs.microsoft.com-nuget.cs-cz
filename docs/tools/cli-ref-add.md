---
title: Rozhraní příkazového řádku NuGet přidat – příkaz
description: Příkaz Přidat odkaz nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545831"
---
# <a name="add-command-nuget-cli"></a>Příkaz add (NuGet CLI)

**Platí pro**: balíček publikování &bullet; **podporované verze**: 3.3 +

Přidá zadaný balíček ke zdroji balíčku jiným protokolem než HTTP (složka nebo cesta UNC) v hierarchickém rozložení, ve které jsou vytvořeny složky pro číslo ID a verzi balíčku. Příklad:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

Při obnovení nebo aktualizaci na zdroji balíčku, hierarchickém rozložení poskytuje výrazně vyšší výkon.

Chcete-li rozbalit všechny soubory v balíčku pro cílový zdroj balíčků, použijte `-Expand` přepnout. To obvykle za následek další podsložky, které jsou uvedené v cíli, jako například `tools` a `lib`.

## <a name="usage"></a>Použití

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

kde `<packagePath>` je cesta k balíčku, který chcete přidat, a `<sourcePath>` Určuje zdroj balíčků založená na složku, do kterého se přidá balíček. Zdroje HTTP nejsou podporovány.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| ConfigFile | Konfigurační soubor NuGet použít. Pokud není zadán, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.|
| Expand | Přidá všechny soubory v balíčku ke zdroji balíčku. |
| ForceEnglishOutput | *(3.5 +)*  Vynutí nuget.exe pro spuštění pomocí neutrální, základem je angličtina jazyková verze. |
| Help | Zobrazí nápovědu pro příkaz. |
| NonInteractive | Potlačí vyzve k zadání uživatele o vstup ani potvrzení. |
| Verbosity | Určuje množství podrobností, na které se zobrazí ve výstupu: *normální*, *quiet*, *podrobné*. |

Viz také [proměnné prostředí](cli-ref-environment-variables.md)

## <a name="examples"></a>Příklady

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
