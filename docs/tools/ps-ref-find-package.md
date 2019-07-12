---
title: Referenční informace prostředí PowerShell najít balíček NuGet
description: Referenční informace pro příkaz Powershellu Find-Package v konzole Správce balíčků NuGet v sadě Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: fee0ad0496f27d0796eddf177edc235bcb10da70
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842524"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="f5dd0-103">Find-Package (konzola Správce balíčků v sadě Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="f5dd0-103">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="f5dd0-104">*Verze 3.0 a; Toto téma popisuje příkaz v rámci [Konzola správce balíčků](package-manager-console.md) v sadě Visual Studio ve Windows. Obecný příkaz Find-balíčků v Powershellu najdete v článku [odkazu modulu Powershellu PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="f5dd0-104">*Version 3.0+; this topic describes the command within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="f5dd0-105">Získá sadu vzdálené balíčky pomocí zadaného ID nebo klíčová slova ze zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="f5dd0-105">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="f5dd0-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="f5dd0-106">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="f5dd0-107">Parametry</span><span class="sxs-lookup"><span data-stu-id="f5dd0-107">Parameters</span></span>

| <span data-ttu-id="f5dd0-108">Parametr</span><span class="sxs-lookup"><span data-stu-id="f5dd0-108">Parameter</span></span> | <span data-ttu-id="f5dd0-109">Popis</span><span class="sxs-lookup"><span data-stu-id="f5dd0-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f5dd0-110">ID &lt;klíčová slova&gt;</span><span class="sxs-lookup"><span data-stu-id="f5dd0-110">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="f5dd0-111">(Povinné) Klíčová slova pro vyhledávání ve zdroji balíčku.</span><span class="sxs-lookup"><span data-stu-id="f5dd0-111">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="f5dd0-112">Pomocí - ExactMatch vrátit pouze balíčky, jejichž ID balíčku shoduje s klíčovými slovy.</span><span class="sxs-lookup"><span data-stu-id="f5dd0-112">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="f5dd0-113">Žádná klíčová slova směru, je-li `Find-Package` vrátí seznam balíčků prvních 20 soubory ke stažení nebo číslo zadané parametrem - první.</span><span class="sxs-lookup"><span data-stu-id="f5dd0-113">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="f5dd0-114">Všimněte si, že – Id je volitelné a no-op.</span><span class="sxs-lookup"><span data-stu-id="f5dd0-114">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="f5dd0-115">Source</span><span class="sxs-lookup"><span data-stu-id="f5dd0-115">Source</span></span> | <span data-ttu-id="f5dd0-116">Cesta URL nebo složku zdroje balíčku. Chcete-li hledat.</span><span class="sxs-lookup"><span data-stu-id="f5dd0-116">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="f5dd0-117">Cesty k místní složce může být absolutní nebo relativní vzhledem k aktuální složky.</span><span class="sxs-lookup"><span data-stu-id="f5dd0-117">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="f5dd0-118">Pokud tento parametr vynechán, `Find-Package` hledá aktuálně vybraném zdroji balíčku.</span><span class="sxs-lookup"><span data-stu-id="f5dd0-118">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="f5dd0-119">AllVersions</span><span class="sxs-lookup"><span data-stu-id="f5dd0-119">AllVersions</span></span> | <span data-ttu-id="f5dd0-120">Zobrazí všechny dostupné verze každého balíčku namísto pouze nejnovější verze.</span><span class="sxs-lookup"><span data-stu-id="f5dd0-120">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="f5dd0-121">první</span><span class="sxs-lookup"><span data-stu-id="f5dd0-121">First</span></span> | <span data-ttu-id="f5dd0-122">Počet balíčků vrátit od začátku seznamu. Výchozí hodnota je 20.</span><span class="sxs-lookup"><span data-stu-id="f5dd0-122">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="f5dd0-123">Skip</span><span class="sxs-lookup"><span data-stu-id="f5dd0-123">Skip</span></span> | <span data-ttu-id="f5dd0-124">Vynechá první &lt;int&gt; balíčky ze zobrazeného seznamu.</span><span class="sxs-lookup"><span data-stu-id="f5dd0-124">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="f5dd0-125">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="f5dd0-125">IncludePrerelease</span></span> | <span data-ttu-id="f5dd0-126">Obsahuje předběžné verze balíčků ve výsledcích.</span><span class="sxs-lookup"><span data-stu-id="f5dd0-126">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="f5dd0-127">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="f5dd0-127">ExactMatch</span></span> | <span data-ttu-id="f5dd0-128">Zadané použití &lt;klíčová slova&gt; jako ID balíčku velká a malá písmena.</span><span class="sxs-lookup"><span data-stu-id="f5dd0-128">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="f5dd0-129">StartWith</span><span class="sxs-lookup"><span data-stu-id="f5dd0-129">StartWith</span></span> | <span data-ttu-id="f5dd0-130">Vrátí balíčky balíčku, jejichž ID začíná &lt;klíčová slova&gt;.</span><span class="sxs-lookup"><span data-stu-id="f5dd0-130">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="f5dd0-131">Žádná z těchto parametrů přijímat kanálu vstup nebo zástupné znaky.</span><span class="sxs-lookup"><span data-stu-id="f5dd0-131">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="f5dd0-132">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="f5dd0-132">Common Parameters</span></span>

<span data-ttu-id="f5dd0-133">`Find-Package` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="f5dd0-133">`Find-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="f5dd0-134">Příklady</span><span class="sxs-lookup"><span data-stu-id="f5dd0-134">Examples</span></span>

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```
