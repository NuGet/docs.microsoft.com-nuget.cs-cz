---
title: "Příkaz seznamu NuGet rozhraní příkazového řádku | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 728c8452-0457-4bb8-bfdc-de77fe1570bd
description: "Referenční dokumentace pro příkaz nuget.exe seznamu"
keywords: "odkaz na seznam nuget, seznam balíčků příkaz"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 62a7077e7adac1e4d8cf305fd6e66a6ce5ebfb76
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="list-command-nuget-cli"></a>příkaz seznamu (NuGet CLI)

**Platí pro:** spotřeba balíčku, publikování &bullet; **podporované verze:** všechny

Zobrazí seznam balíčků z daného zdroje. Pokud nejsou zadány žádné zdroje, všechny zdroje definované v souboru globální konfiguraci `%AppData%\NuGet\NuGet.Config`, se používají. Pokud `NuGet.Config` žádné zdroje, pak určuje `list` používá výchozí informačního kanálu (nuget.org).

## <a name="usage"></a>Použití

```
nuget list [search terms] [options]
```

volitelné hledané výrazy, kde bude filtr pro zobrazený seznam. Hledaný text se použijí pro názvy balíčků, značky a Popis balíčku.

## <a name="options"></a>Možnosti
| Možnost | Popis |
| --- | --- |
| AllVersions | Zobrazí seznam všech verze balíčku. Ve výchozím nastavení se zobrazí jenom nejnovější verzi balíčku. |
| ConfigFile | *(2.5 +)*  NuGet konfiguračním souboru použít. Pokud není zadaný, *%AppData%\NuGet\NuGet.Config* se používá. |
| ForceEnglishOutput | *(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze. |
| Nápověda | Zobrazí nápovědu pro příkaz. |
| IncludeDelisted | *(3.2 +)*  Zobrazovat neuvedené balíčky. |
| Neinteraktivní | Potlačí výzvy pro vstup uživatele nebo potvrzení. |
| Předběžné verze | Obsahuje předběžné verze balíčků v seznamu. |
| Zdroj | Určuje seznam balíčků zdroje pro vyhledávání. |
| Podrobnosti | Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné (2.5 +)*. |

Viz také [proměnné prostředí](cli-ref-environment-variables.md)

## <a name="examples"></a>Příklady

```
nuget list

nuget list -Verbosity detailed -AllVersions
```
