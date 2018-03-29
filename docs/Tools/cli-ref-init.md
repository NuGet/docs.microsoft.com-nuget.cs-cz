---
title: Příkaz init NuGet rozhraní příkazového řádku | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referenční dokumentace pro nuget.exe init – příkaz
keywords: Init – odkaz nuget, Init – příkaz
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 01a3553622020b5868e33ece09cd7555cb712fd3
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="init-command-nuget-cli"></a>Init – příkaz (NuGet CLI)

**Platí pro:** balíček vytvoření &bullet; **podporované verze:** 3.3 +

Zkopíruje všechny balíčky z plochých složku do cílové složky pomocí hierarchickém rozložení, jak je popsáno [přidat příkaz](cli-ref-add.md). To znamená, pomocí `init` je ekvivalentní k použití `add` na každý balíček ve složce.

Stejně jako u `add`, cíl musí být místní složku nebo cesty UNC. Úložiště balíčku HTTP například nuget.org nebo privátní servery nejsou podporovány.

## <a name="usage"></a>Použití

```cli
nuget init <source> <destination> [options]
```

kde `<source>` je složka, která obsahuje balíčky a `<destination>` je místní složka nebo cesta UNC ke kterému se zkopírují balíčky.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| ConfigFile | Konfigurační soubor NuGet použít. Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.|
| ForceEnglishOutput | *(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze. |
| Rozbalte položku | Přidá všechny soubory v každý balíček, který je přidán ke zdroji balíčku; stejné jako `-Expand` s `add` příkaz. |
| Nápověda | Zobrazí nápovědu pro příkaz. |
| Neinteraktivní | Potlačí výzvy pro vstup uživatele nebo potvrzení. |
| Podrobnosti | Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*. |

Viz také [proměnné prostředí](cli-ref-environment-variables.md)

## <a name="examples"></a>Příklady

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
