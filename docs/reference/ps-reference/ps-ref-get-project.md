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
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="2eec5-103">Get-Project (konzola Správce balíčků v sadě Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="2eec5-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="2eec5-104">*K dispozici pouze v rámci [konzoly Správce balíčků](../../consume-packages/install-use-packages-powershell.md) v sadě Visual Studio ve Windows.*</span><span class="sxs-lookup"><span data-stu-id="2eec5-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="2eec5-105">Zobrazí informace o výchozím nebo zadaném projektu.</span><span class="sxs-lookup"><span data-stu-id="2eec5-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="2eec5-106">`Get-Project`konkrétně vrátí referenční do objektu aplikace Visual Studio DTE (vývojové nástroje) pro projekt.</span><span class="sxs-lookup"><span data-stu-id="2eec5-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="2eec5-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="2eec5-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="2eec5-108">Parametry</span><span class="sxs-lookup"><span data-stu-id="2eec5-108">Parameters</span></span>

| <span data-ttu-id="2eec5-109">Parametr</span><span class="sxs-lookup"><span data-stu-id="2eec5-109">Parameter</span></span> | <span data-ttu-id="2eec5-110">Popis</span><span class="sxs-lookup"><span data-stu-id="2eec5-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2eec5-111">Name</span><span class="sxs-lookup"><span data-stu-id="2eec5-111">Name</span></span> | <span data-ttu-id="2eec5-112">Určuje projekt, který se má zobrazit, výchozí nastavení výchozího projektu, který je vybraný v konzole správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="2eec5-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="2eec5-113">Přepínač-Name je sám nepovinný.</span><span class="sxs-lookup"><span data-stu-id="2eec5-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="2eec5-114">Všechny</span><span class="sxs-lookup"><span data-stu-id="2eec5-114">All</span></span> | <span data-ttu-id="2eec5-115">Zobrazí informace pro každý projekt v řešení; pořadí projektů není deterministické.</span><span class="sxs-lookup"><span data-stu-id="2eec5-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="2eec5-116">Žádný z těchto parametrů nepřijímají vstupní ani zástupné znaky kanálu.</span><span class="sxs-lookup"><span data-stu-id="2eec5-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="2eec5-117">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="2eec5-117">Common Parameters</span></span>

<span data-ttu-id="2eec5-118">`Get-Project`podporuje následující [běžné parametry PowerShellu](http://go.microsoft.com/fwlink/?LinkID=113216): Ladit, Error Action, ErrorVariable, unbuffer, subvariable, PipelineVariable, verbose, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="2eec5-118">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="2eec5-119">Příklady</span><span class="sxs-lookup"><span data-stu-id="2eec5-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```