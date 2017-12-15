---
title: "Příkaz help NuGet rozhraní příkazového řádku | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 780d7f52-d6c6-45cd-8a62-218ff8c0b270
description: "Referenční dokumentace pro příkaz nuget.exe nápovědy"
keywords: "odkaz na nápovědu nuget, příkazu nápovědy"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 55dc263fedd7ed5a3e48b76dbc9a3ccc220655cf
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="help-or--command-nuget-cli"></a>Nápověda nebo? příkaz (NuGet CLI)

**Platí pro:** všechny &bullet; **podporované verze**: všechny

Zobrazí obecné pomůže informace a informace o určité příkazy.

## <a name="usage"></a>Použití

```
nuget help [command] [options]
nuget ? [command] [options]
```

[příkaz] kde identifikuje konkrétní příkaz pro které chcete zobrazit nápovědu.

> [!Warning]
> U některých příkazů, mějte na paměti k určení *pomoci* , jako první se `nuget help install`, protože je balíček s názvem "Nápověda" v nuget.org. Pokud zadáte název příkazu `nuget install help`, není získání nápovědy na příkaz instalace, ale místo toho nainstaluje balíček s názvem nápovědy.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| Všechny | Tisk podrobnou nápovědu pro všechny dostupné příkazy; Pokud je zadána konkrétní příkaz ignorována. |
| ConfigFile | *(2.5 +)*  NuGet konfiguračním souboru použít. Pokud není zadaný, *%AppData%\NuGet\NuGet.Config* se používá. |
| ForceEnglishOutput | *(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze. |
| Nápověda | Zobrazí nápovědu pro příkaz help sám sebe. |
| Markdownu | Tisk podrobnou nápovědu ve formátu markdown při použití s `-All`. V opačném případě ignorovat. |
| Neinteraktivní | Potlačí výzvy pro vstup uživatele nebo potvrzení. |
| Podrobnosti | Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné (2.5 +)*. |

Viz také [proměnné prostředí](cli-ref-environment-variables.md)

## <a name="examples"></a>Příklady

```
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
