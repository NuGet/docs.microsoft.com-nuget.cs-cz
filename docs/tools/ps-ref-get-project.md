---
title: Referenční informace prostředí PowerShell Get projektu NuGet
description: Referenční informace pro příkaz prostředí GetProject PowerShell v konzole Správce balíčků NuGet v sadě Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 849261711fafcadbab38bf6fe99340c4b79e1e21
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550434"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Get-Project (konzola Správce balíčků v sadě Visual Studio)

*K dispozici pouze v rámci [Konzola správce balíčků NuGet](package-manager-console.md) v sadě Visual Studio ve Windows.*

Zobrazí informace o výchozích nebo zadaný projekt. `Get-Project` Konkrétně vrací referenční objekt Visual Studio DTE (Development Tools Environment) pro projekt.

## <a name="syntax"></a>Syntaxe

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>Parametry

| Parametr | Popis |
| --- | --- |
| Název | Určuje projekt k zobrazení, jako výchozí se použije výchozí projekt vybraný v konzole Správce balíčků. – Název přepínače je volitelné. |
| Všechny | Zobrazí informace pro každý projekt v řešení; pořadí projekty není deterministický. |

Žádná z těchto parametrů přijímat kanálu vstup nebo zástupné znaky.

## <a name="common-parameters"></a>Společné parametry

`Get-Project` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction a WarningVariable.

## <a name="examples"></a>Příklady

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```