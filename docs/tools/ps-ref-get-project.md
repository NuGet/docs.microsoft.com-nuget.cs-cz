---
title: Referenční informace prostředí PowerShell Get projektu NuGet
description: Referenční dokumentace pro příkaz prostředí GetProject PowerShell v konzole Správce balíčků NuGet v sadě Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: afdf9f762bbd34531f9d9093238a2fed27e3f4d3
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817753"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="9ecdd-103">Get-Project (konzola Správce balíčků v sadě Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="9ecdd-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="9ecdd-104">*K dispozici pouze v rámci [Konzola správce balíčků NuGet](package-manager-console.md) v sadě Visual Studio v systému Windows.*</span><span class="sxs-lookup"><span data-stu-id="9ecdd-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="9ecdd-105">Zobrazí informace o výchozí nebo zadaného projektu.</span><span class="sxs-lookup"><span data-stu-id="9ecdd-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="9ecdd-106">`Get-Project` Vrátí konkrétně referenční objekt Visual Studio DTE (Development Tools Environment) pro projekt.</span><span class="sxs-lookup"><span data-stu-id="9ecdd-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="9ecdd-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="9ecdd-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="9ecdd-108">Parametry</span><span class="sxs-lookup"><span data-stu-id="9ecdd-108">Parameters</span></span>

| <span data-ttu-id="9ecdd-109">Parametr</span><span class="sxs-lookup"><span data-stu-id="9ecdd-109">Parameter</span></span> | <span data-ttu-id="9ecdd-110">Popis</span><span class="sxs-lookup"><span data-stu-id="9ecdd-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9ecdd-111">Název</span><span class="sxs-lookup"><span data-stu-id="9ecdd-111">Name</span></span> | <span data-ttu-id="9ecdd-112">Určuje projekt, pokud chcete zobrazit, jako výchozí bude použit výchozí projekt vybraný v konzoli správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="9ecdd-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="9ecdd-113">-Název přepínače je sám volitelné.</span><span class="sxs-lookup"><span data-stu-id="9ecdd-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="9ecdd-114">Všechny</span><span class="sxs-lookup"><span data-stu-id="9ecdd-114">All</span></span> | <span data-ttu-id="9ecdd-115">Zobrazí informace o všechny projekty v řešení; pořadí projektů není deterministické.</span><span class="sxs-lookup"><span data-stu-id="9ecdd-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="9ecdd-116">Žádná z těchto parametrů přijmout kanálu vstup nebo zástupné znaky.</span><span class="sxs-lookup"><span data-stu-id="9ecdd-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="9ecdd-117">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="9ecdd-117">Common Parameters</span></span>

<span data-ttu-id="9ecdd-118">`Get-Project` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, podrobná, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="9ecdd-118">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="9ecdd-119">Příklady</span><span class="sxs-lookup"><span data-stu-id="9ecdd-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```