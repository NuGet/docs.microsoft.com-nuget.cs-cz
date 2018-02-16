---
title: "Příkaz help NuGet rozhraní příkazového řádku | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenční dokumentace pro příkaz nuget.exe nápovědy"
keywords: "odkaz na nápovědu nuget, příkazu nápovědy"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b4255c353e412cf1d1a59590ee816b7887c90653
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/14/2018
---
# <a name="help-or--command-nuget-cli"></a>Nápověda nebo? příkaz (NuGet CLI)

**Platí pro:** všechny &bullet; **podporované verze**: všechny

Zobrazí obecné pomůže informace a informace o určité příkazy.

## <a name="usage"></a>Použití

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

[příkaz] kde identifikuje konkrétní příkaz pro které chcete zobrazit nápovědu.

> [!Warning]
> U některých příkazů, mějte na paměti k určení *pomoci* , jako první se `nuget help install`, protože je balíček s názvem "Nápověda" v nuget.org. Pokud zadáte název příkazu `nuget install help`, nebude získání nápovědy na příkaz instalace, ale místo toho nainstaluje balíček s názvem nápovědy.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| Všechny | Tisk podrobnou nápovědu pro všechny dostupné příkazy; Pokud je zadána konkrétní příkaz ignorována. |
| ConfigFile | Konfigurační soubor NuGet použít. Pokud není zadaný, *%AppData%\NuGet\NuGet.Config* se používá. |
| ForceEnglishOutput | *(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze. |
| Nápověda | Zobrazí nápovědu pro příkaz help sám sebe. |
| Markdownu | Tisk podrobnou nápovědu ve formátu markdown při použití s `-All`. V opačném případě ignorovat. |
| Neinteraktivní | Potlačí výzvy pro vstup uživatele nebo potvrzení. |
| Podrobnosti | Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*. |

Viz také [proměnné prostředí](cli-ref-environment-variables.md)

## <a name="examples"></a>Příklady

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
