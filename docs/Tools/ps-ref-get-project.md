---
title: Referenční informace prostředí PowerShell Get projektu NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referenční dokumentace pro příkaz prostředí GetProject PowerShell v konzole Správce balíčků NuGet v sadě Visual Studio.
keywords: NuGet konzoly Správce balíčků, příkazy prostředí NuGet Powershell, NuGet Powershell odkaz, Get-projektu
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 9fcdcf7c550408cd7dfd73787ee14821c46a1df9
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="25fa6-104">Get projektu (konzola Správce balíčků v sadě Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="25fa6-104">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="25fa6-105">*K dispozici pouze v rámci [Konzola správce balíčků NuGet](package-manager-console.md) v sadě Visual Studio v systému Windows.*</span><span class="sxs-lookup"><span data-stu-id="25fa6-105">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="25fa6-106">Zobrazí informace o výchozí nebo zadaného projektu.</span><span class="sxs-lookup"><span data-stu-id="25fa6-106">Displays information about the default or specified project.</span></span> <span data-ttu-id="25fa6-107">`Get-Project` Vrátí konkrétně referenční objekt Visual Studio DTE (Development Tools Environment) pro projekt.</span><span class="sxs-lookup"><span data-stu-id="25fa6-107">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="25fa6-108">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="25fa6-108">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="25fa6-109">Parametry</span><span class="sxs-lookup"><span data-stu-id="25fa6-109">Parameters</span></span>

| <span data-ttu-id="25fa6-110">Parametr</span><span class="sxs-lookup"><span data-stu-id="25fa6-110">Parameter</span></span> | <span data-ttu-id="25fa6-111">Popis</span><span class="sxs-lookup"><span data-stu-id="25fa6-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="25fa6-112">Název</span><span class="sxs-lookup"><span data-stu-id="25fa6-112">Name</span></span> | <span data-ttu-id="25fa6-113">Určuje projekt, pokud chcete zobrazit, jako výchozí bude použit výchozí projekt vybraný v konzoli správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="25fa6-113">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="25fa6-114">-Název přepínače je sám volitelné.</span><span class="sxs-lookup"><span data-stu-id="25fa6-114">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="25fa6-115">Všechny</span><span class="sxs-lookup"><span data-stu-id="25fa6-115">All</span></span> | <span data-ttu-id="25fa6-116">Zobrazí informace o všechny projekty v řešení; pořadí projektů není deterministické.</span><span class="sxs-lookup"><span data-stu-id="25fa6-116">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="25fa6-117">Žádná z těchto parametrů přijmout kanálu vstup nebo zástupné znaky.</span><span class="sxs-lookup"><span data-stu-id="25fa6-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="25fa6-118">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="25fa6-118">Common Parameters</span></span>

<span data-ttu-id="25fa6-119">`Get-Project` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, podrobná, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="25fa6-119">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="25fa6-120">Příklady</span><span class="sxs-lookup"><span data-stu-id="25fa6-120">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```