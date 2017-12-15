---
title: "Referenční informace prostředí PowerShell Get projektu NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 09c10ea3-ba26-4bfa-999e-de5350e6e920
description: "Referenční dokumentace pro příkaz prostředí GetProject PowerShell v konzole Správce balíčků NuGet v sadě Visual Studio."
keywords: "NuGet konzoly Správce balíčků, příkazy prostředí NuGet Powershell, NuGet Powershell odkaz, Get-projektu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 40c986164c3f6bd6a02877e15827541aae77d8ad
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="b0b07-104">Get projektu (konzola Správce balíčků v sadě Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="b0b07-104">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="b0b07-105">*K dispozici pouze v rámci [Konzola správce balíčků NuGet](Package-Manager-Console.md) v sadě Visual Studio v systému Windows.*</span><span class="sxs-lookup"><span data-stu-id="b0b07-105">*Available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="b0b07-106">Zobrazí informace o výchozí nebo zadaného projektu.</span><span class="sxs-lookup"><span data-stu-id="b0b07-106">Displays information about the default or specified project.</span></span> <span data-ttu-id="b0b07-107">`Get-Project`Vrátí konkrétně referenční objekt Visual Studio DTE (Development Tools Environment) pro projekt.</span><span class="sxs-lookup"><span data-stu-id="b0b07-107">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="b0b07-108">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="b0b07-108">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="b0b07-109">Parametry</span><span class="sxs-lookup"><span data-stu-id="b0b07-109">Parameters</span></span>

| <span data-ttu-id="b0b07-110">Parametr</span><span class="sxs-lookup"><span data-stu-id="b0b07-110">Parameter</span></span> | <span data-ttu-id="b0b07-111">Popis</span><span class="sxs-lookup"><span data-stu-id="b0b07-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b0b07-112">Název</span><span class="sxs-lookup"><span data-stu-id="b0b07-112">Name</span></span> | <span data-ttu-id="b0b07-113">Určuje projekt, pokud chcete zobrazit, jako výchozí bude použit výchozí projekt vybraný v konzoli správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="b0b07-113">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="b0b07-114">-Název přepínače je sám volitelné.</span><span class="sxs-lookup"><span data-stu-id="b0b07-114">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="b0b07-115">Všechny</span><span class="sxs-lookup"><span data-stu-id="b0b07-115">All</span></span> | <span data-ttu-id="b0b07-116">Zobrazí informace o všechny projekty v řešení; pořadí projektů není deterministické.</span><span class="sxs-lookup"><span data-stu-id="b0b07-116">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="b0b07-117">Žádná z těchto parametrů přijmout kanálu vstup nebo zástupné znaky.</span><span class="sxs-lookup"><span data-stu-id="b0b07-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="b0b07-118">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="b0b07-118">Common Parameters</span></span>

<span data-ttu-id="b0b07-119">`Get-Project`podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, podrobná, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="b0b07-119">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="b0b07-120">Příklady</span><span class="sxs-lookup"><span data-stu-id="b0b07-120">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```