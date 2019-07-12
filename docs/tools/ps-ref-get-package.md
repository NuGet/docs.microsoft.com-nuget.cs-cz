---
title: Referenční informace prostředí PowerShell Get balíček NuGet
description: Referenční informace pro příkaz prostředí PowerShell Get-Package v konzole Správce balíčků NuGet v sadě Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d0d25cb6e21f6d0d42389e08340b6f1e1baf8a64
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842506"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="14206-103">Get-Package (konzola Správce balíčků v sadě Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="14206-103">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="14206-104">*Toto téma popisuje příkaz v rámci [Konzola správce balíčků](package-manager-console.md) v sadě Visual Studio ve Windows. Obecný příkaz prostředí PowerShell Get-Package, najdete v článku [odkazu modulu Powershellu PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="14206-104">*This topic describes the command within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="14206-105">Načte seznam balíčků nainstalovaných v místním úložišti, zobrazí seznam dostupných balíčků z balíčku zdroje při použití s přepínačem - ListAvailable nebo vypíše dostupné aktualizace při použití s přepínačem - Update.</span><span class="sxs-lookup"><span data-stu-id="14206-105">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="14206-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="14206-106">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="14206-107">Bez parametrů `Get-Package` zobrazí seznam balíčků nainstalovaných ve výchozím nastavení projektu.</span><span class="sxs-lookup"><span data-stu-id="14206-107">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="14206-108">Parametry</span><span class="sxs-lookup"><span data-stu-id="14206-108">Parameters</span></span>

| <span data-ttu-id="14206-109">Parametr</span><span class="sxs-lookup"><span data-stu-id="14206-109">Parameter</span></span> | <span data-ttu-id="14206-110">Popis</span><span class="sxs-lookup"><span data-stu-id="14206-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="14206-111">Source</span><span class="sxs-lookup"><span data-stu-id="14206-111">Source</span></span> | <span data-ttu-id="14206-112">Cesta adresy URL nebo složka balíčku.</span><span class="sxs-lookup"><span data-stu-id="14206-112">The URL or folder path for the package .</span></span> <span data-ttu-id="14206-113">Cesty k místní složce může být absolutní nebo relativní vzhledem k aktuální složky.</span><span class="sxs-lookup"><span data-stu-id="14206-113">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="14206-114">Pokud tento parametr vynechán, `Get-Package` hledá aktuálně vybraném zdroji balíčku.</span><span class="sxs-lookup"><span data-stu-id="14206-114">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="14206-115">Při použití s - ListAvailable, výchozí hodnota je nuget.org.</span><span class="sxs-lookup"><span data-stu-id="14206-115">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="14206-116">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="14206-116">ListAvailable</span></span> | <span data-ttu-id="14206-117">Zobrazí seznam balíčků z balíčku zdroje, jako výchozí se použije na nuget.org. Ukazuje na výchozí hodnotu 50 balíčky jsou určena - PageSize nebo - první.</span><span class="sxs-lookup"><span data-stu-id="14206-117">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="14206-118">Aktualizace</span><span class="sxs-lookup"><span data-stu-id="14206-118">Updates</span></span> | <span data-ttu-id="14206-119">Zobrazí seznam balíčků, které mají k dispozici aktualizace ze zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="14206-119">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="14206-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="14206-120">ProjectName</span></span> | <span data-ttu-id="14206-121">Projekt, ze kterého se mají balíčky nainstalovat.</span><span class="sxs-lookup"><span data-stu-id="14206-121">The project from which to get installed packages.</span></span> <span data-ttu-id="14206-122">Pokud tento parametr vynechán, vrátí nainstalované projekty pro celé řešení.</span><span class="sxs-lookup"><span data-stu-id="14206-122">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="14206-123">Filtr</span><span class="sxs-lookup"><span data-stu-id="14206-123">Filter</span></span> | <span data-ttu-id="14206-124">Řetězec filtru sloužící k zúžení seznamu balíčků použitím na ID balíčku, popisu a značkách.</span><span class="sxs-lookup"><span data-stu-id="14206-124">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="14206-125">první</span><span class="sxs-lookup"><span data-stu-id="14206-125">First</span></span> | <span data-ttu-id="14206-126">Počet balíčků vrátit od začátku seznamu.</span><span class="sxs-lookup"><span data-stu-id="14206-126">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="14206-127">Pokud není zadán, výchozí hodnota je 50.</span><span class="sxs-lookup"><span data-stu-id="14206-127">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="14206-128">Skip</span><span class="sxs-lookup"><span data-stu-id="14206-128">Skip</span></span> | <span data-ttu-id="14206-129">Vynechá první &lt;int&gt; balíčky ze zobrazeného seznamu.</span><span class="sxs-lookup"><span data-stu-id="14206-129">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="14206-130">AllVersions</span><span class="sxs-lookup"><span data-stu-id="14206-130">AllVersions</span></span> | <span data-ttu-id="14206-131">Zobrazí všechny dostupné verze každého balíčku namísto pouze nejnovější verze.</span><span class="sxs-lookup"><span data-stu-id="14206-131">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="14206-132">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="14206-132">IncludePrerelease</span></span> | <span data-ttu-id="14206-133">Obsahuje předběžné verze balíčků ve výsledcích.</span><span class="sxs-lookup"><span data-stu-id="14206-133">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="14206-134">PageSize</span><span class="sxs-lookup"><span data-stu-id="14206-134">PageSize</span></span> | <span data-ttu-id="14206-135">*(3.0 +)*  Při použití s - ListAvailable (povinné), počet balíčků do seznamu předtím, než poskytne výzvy a pokračujte.</span><span class="sxs-lookup"><span data-stu-id="14206-135">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="14206-136">Žádná z těchto parametrů přijímat kanálu vstup nebo zástupné znaky.</span><span class="sxs-lookup"><span data-stu-id="14206-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="14206-137">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="14206-137">Common Parameters</span></span>

<span data-ttu-id="14206-138">`Get-Package` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="14206-138">`Get-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="14206-139">Příklady</span><span class="sxs-lookup"><span data-stu-id="14206-139">Examples</span></span>

```ps
# Lists the packages installed in the current solution
Get-Package

# Lists the packages installed in a project
Get-Package -ProjectName MyProject

# Lists packages available in the current package source
Get-Package -ListAvailable

# Lists 30 packages at a time from the current source, and prompts to continue if more are available
Get-Package -ListAvailable -PageSize 30

# Lists packages with the Ninject keyword in the current source, up to 50
Get-Package -ListAvailable -Filter Ninject

# List all versions of packages matching the filter "jquery"
Get-Package -ListAvailable -Filter jquery -AllVersions

# Lists packages installed in the solution that have available updates
Get-Package -Updates

# Lists packages installed in a specific project that have available updates
Get-Package -Updates -ProjectName MyProject
```
