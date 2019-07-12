---
title: Referenční informace prostředí PowerShell Get projektu NuGet
description: Referenční informace pro příkaz prostředí GetProject PowerShell v konzole Správce balíčků NuGet v sadě Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 2ceb1557eafd213c148d3ab870925ef5bbbee145
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842284"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="b97fc-103">Get-Project (konzola Správce balíčků v sadě Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="b97fc-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="b97fc-104">*K dispozici pouze v rámci [Konzola správce balíčků](package-manager-console.md) v sadě Visual Studio ve Windows.*</span><span class="sxs-lookup"><span data-stu-id="b97fc-104">*Available only within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="b97fc-105">Zobrazí informace o výchozích nebo zadaný projekt.</span><span class="sxs-lookup"><span data-stu-id="b97fc-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="b97fc-106">`Get-Project` Konkrétně vrací referenční objekt Visual Studio DTE (Development Tools Environment) pro projekt.</span><span class="sxs-lookup"><span data-stu-id="b97fc-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="b97fc-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="b97fc-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="b97fc-108">Parametry</span><span class="sxs-lookup"><span data-stu-id="b97fc-108">Parameters</span></span>

| <span data-ttu-id="b97fc-109">Parametr</span><span class="sxs-lookup"><span data-stu-id="b97fc-109">Parameter</span></span> | <span data-ttu-id="b97fc-110">Popis</span><span class="sxs-lookup"><span data-stu-id="b97fc-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b97fc-111">Name</span><span class="sxs-lookup"><span data-stu-id="b97fc-111">Name</span></span> | <span data-ttu-id="b97fc-112">Určuje projekt k zobrazení, jako výchozí se použije výchozí projekt vybraný v konzole Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="b97fc-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="b97fc-113">– Název přepínače je volitelné.</span><span class="sxs-lookup"><span data-stu-id="b97fc-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="b97fc-114">Všechny</span><span class="sxs-lookup"><span data-stu-id="b97fc-114">All</span></span> | <span data-ttu-id="b97fc-115">Zobrazí informace pro každý projekt v řešení; pořadí projekty není deterministický.</span><span class="sxs-lookup"><span data-stu-id="b97fc-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="b97fc-116">Žádná z těchto parametrů přijímat kanálu vstup nebo zástupné znaky.</span><span class="sxs-lookup"><span data-stu-id="b97fc-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="b97fc-117">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="b97fc-117">Common Parameters</span></span>

<span data-ttu-id="b97fc-118">`Get-Project` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="b97fc-118">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="b97fc-119">Příklady</span><span class="sxs-lookup"><span data-stu-id="b97fc-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```