---
title: Referenční dokumentace k prostředí NuGet Get-Project PowerShell
description: Reference k příkazu getproject PowerShell v konzole správce balíčků NuGet v aplikaci Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 830746f032bb4eb916508ef320c5b3d0486b89a4
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328210"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Get-Project (konzola Správce balíčků v sadě Visual Studio)

*K dispozici pouze v rámci [konzoly Správce balíčků](../../consume-packages/install-use-packages-powershell.md) v sadě Visual Studio ve Windows.*

Zobrazí informace o výchozím nebo zadaném projektu. `Get-Project`konkrétně vrátí referenční do objektu aplikace Visual Studio DTE (vývojové nástroje) pro projekt.

## <a name="syntax"></a>Syntaxe

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>Parametry

| Parametr | Popis |
| --- | --- |
| Name | Určuje projekt, který se má zobrazit, výchozí nastavení výchozího projektu, který je vybraný v konzole správce balíčků. Přepínač-Name je sám nepovinný. |
| Všechny | Zobrazí informace pro každý projekt v řešení; pořadí projektů není deterministické. |

Žádný z těchto parametrů nepřijímají vstupní ani zástupné znaky kanálu.

## <a name="common-parameters"></a>Společné parametry

`Get-Project`podporuje následující [běžné parametry PowerShellu](http://go.microsoft.com/fwlink/?LinkID=113216): Ladit, Error Action, ErrorVariable, unbuffer, subvariable, PipelineVariable, verbose, WarningAction a WarningVariable.

## <a name="examples"></a>Příklady

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```