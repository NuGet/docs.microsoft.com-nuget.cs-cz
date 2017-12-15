---
title: "Příkaz init NuGet rozhraní příkazového řádku | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: d413e4f3-1b41-4a92-8df8-87d21b542bd3
description: "Referenční dokumentace pro nuget.exe init – příkaz"
keywords: "Init – odkaz nuget, Init – příkaz"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f63a3cbcca1aeff02995f23afd217c76e534b3be
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="init-command-nuget-cli"></a>Init – příkaz (NuGet CLI)

**Platí pro:** balíček vytvoření &bullet; **podporované verze:** 3.3 +

Zkopíruje všechny balíčky z plochých složku do cílové složky pomocí hierarchickém rozložení, jak je popsáno [přidat příkaz](#add) výše. To znamená, pomocí `init` je ekvivalentní k použití `add` na každý balíček ve složce.

Stejně jako u `add`, cíl musí být místní složku nebo cesty UNC. Úložiště balíčku HTTP například nuget.org nebo privátní servery nejsou podporovány.

## <a name="usage"></a>Použití

```
nuget init <source> <destination> [options]
```

kde `<source>` je složka, která obsahuje balíčky a `<destination>` je místní složka nebo cesta UNC ke kterému se zkopírují balíčky.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| ConfigFile | Konfigurační soubor NuGet použít. Pokud není zadaný, *%AppData%\NuGet\NuGet.Config* se používá. |
| ForceEnglishOutput | *(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze. |
| Rozbalte položku | Přidá všechny soubory v každý balíček, který je přidán ke zdroji balíčku; stejné jako `-Expand` s `add` příkaz. |
| Nápověda | Zobrazí nápovědu pro příkaz. |
| Neinteraktivní | Potlačí výzvy pro vstup uživatele nebo potvrzení. |
| Podrobnosti | Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné (2.5 +)*. |

Viz také [proměnné prostředí](cli-ref-environment-variables.md)

## <a name="examples"></a>Příklady

```
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
