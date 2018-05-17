---
title: Referenční informace prostředí PowerShell Get projektu NuGet
description: Referenční dokumentace pro příkaz prostředí GetProject PowerShell v konzole Správce balíčků NuGet v sadě Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a7b66cbf36095e31b5929596300018239749cb15
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="1e9fa-103">Get-Project (konzola Správce balíčků v sadě Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="1e9fa-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="1e9fa-104">*K dispozici pouze v rámci [Konzola správce balíčků NuGet](package-manager-console.md) v sadě Visual Studio v systému Windows.*</span><span class="sxs-lookup"><span data-stu-id="1e9fa-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="1e9fa-105">Zobrazí informace o výchozí nebo zadaného projektu.</span><span class="sxs-lookup"><span data-stu-id="1e9fa-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="1e9fa-106">`Get-Project` Vrátí konkrétně referenční objekt Visual Studio DTE (Development Tools Environment) pro projekt.</span><span class="sxs-lookup"><span data-stu-id="1e9fa-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="1e9fa-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="1e9fa-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="1e9fa-108">Parametry</span><span class="sxs-lookup"><span data-stu-id="1e9fa-108">Parameters</span></span>

| <span data-ttu-id="1e9fa-109">Parametr</span><span class="sxs-lookup"><span data-stu-id="1e9fa-109">Parameter</span></span> | <span data-ttu-id="1e9fa-110">Popis</span><span class="sxs-lookup"><span data-stu-id="1e9fa-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1e9fa-111">Název</span><span class="sxs-lookup"><span data-stu-id="1e9fa-111">Name</span></span> | <span data-ttu-id="1e9fa-112">Určuje projekt, pokud chcete zobrazit, jako výchozí bude použit výchozí projekt vybraný v konzoli správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="1e9fa-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="1e9fa-113">-Název přepínače je sám volitelné.</span><span class="sxs-lookup"><span data-stu-id="1e9fa-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="1e9fa-114">Všechny</span><span class="sxs-lookup"><span data-stu-id="1e9fa-114">All</span></span> | <span data-ttu-id="1e9fa-115">Zobrazí informace o všechny projekty v řešení; pořadí projektů není deterministické.</span><span class="sxs-lookup"><span data-stu-id="1e9fa-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="1e9fa-116">Žádná z těchto parametrů přijmout kanálu vstup nebo zástupné znaky.</span><span class="sxs-lookup"><span data-stu-id="1e9fa-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="1e9fa-117">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="1e9fa-117">Common Parameters</span></span>

<span data-ttu-id="1e9fa-118">`Get-Project` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, podrobná, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="1e9fa-118">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="1e9fa-119">Příklady</span><span class="sxs-lookup"><span data-stu-id="1e9fa-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```