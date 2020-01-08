---
title: Reference k prostředí NuGet Get-Package PowerShell
description: Reference k příkazu Get-Package PowerShell v konzole správce balíčků NuGet v aplikaci Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 1c39fea2131b8f4b8a91314347a19366d5a582c2
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/25/2019
ms.locfileid: "75385190"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="d985e-103">Get-Package (konzola Správce balíčků v sadě Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="d985e-103">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="d985e-104">*Toto téma popisuje příkaz v [konzole správce balíčků](../../consume-packages/install-use-packages-powershell.md) v sadě Visual Studio ve Windows. Obecný příkaz prostředí PowerShell Get-Package najdete v [referenčních informacích k PowerShellu PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="d985e-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="d985e-105">Načte seznam balíčků nainstalovaných v místním úložišti, vypíše balíčky dostupné ze zdroje balíčku při použití s přepínačem-ListAvailable nebo zobrazí seznam dostupných aktualizací, pokud se používá s přepínačem-Update.</span><span class="sxs-lookup"><span data-stu-id="d985e-105">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="d985e-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="d985e-106">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="d985e-107">Bez parametrů `Get-Package` zobrazí seznam balíčků nainstalovaných ve výchozím projektu.</span><span class="sxs-lookup"><span data-stu-id="d985e-107">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="d985e-108">Parametry</span><span class="sxs-lookup"><span data-stu-id="d985e-108">Parameters</span></span>

| <span data-ttu-id="d985e-109">Parametr</span><span class="sxs-lookup"><span data-stu-id="d985e-109">Parameter</span></span> | <span data-ttu-id="d985e-110">Popis</span><span class="sxs-lookup"><span data-stu-id="d985e-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d985e-111">Zdroj</span><span class="sxs-lookup"><span data-stu-id="d985e-111">Source</span></span> | <span data-ttu-id="d985e-112">Adresa URL nebo cesta ke složce pro balíček</span><span class="sxs-lookup"><span data-stu-id="d985e-112">The URL or folder path for the package .</span></span> <span data-ttu-id="d985e-113">Cesty k místní složce můžou být absolutní nebo relativní vzhledem k aktuální složce.</span><span class="sxs-lookup"><span data-stu-id="d985e-113">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="d985e-114">Pokud tento parametr vynecháte, `Get-Package` prohledá aktuálně vybraný zdroj balíčku.</span><span class="sxs-lookup"><span data-stu-id="d985e-114">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="d985e-115">Při použití s-ListAvailable se výchozí hodnoty nuget.org.</span><span class="sxs-lookup"><span data-stu-id="d985e-115">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="d985e-116">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="d985e-116">ListAvailable</span></span> | <span data-ttu-id="d985e-117">Vypíše balíčky dostupné ze zdroje balíčku, přičemž se jako výchozí nuget.org. Zobrazuje výchozí 50 balíčků, pokud nejsou zadány hodnoty-PageSize a/nebo-First.</span><span class="sxs-lookup"><span data-stu-id="d985e-117">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="d985e-118">Aktualizace</span><span class="sxs-lookup"><span data-stu-id="d985e-118">Updates</span></span> | <span data-ttu-id="d985e-119">Vypíše balíčky, které mají k dispozici aktualizaci ze zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="d985e-119">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="d985e-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="d985e-120">ProjectName</span></span> | <span data-ttu-id="d985e-121">Projekt, ze kterého se mají získat nainstalované balíčky</span><span class="sxs-lookup"><span data-stu-id="d985e-121">The project from which to get installed packages.</span></span> <span data-ttu-id="d985e-122">Je-li tento parametr vynechán, vrátí instalované projekty pro celé řešení.</span><span class="sxs-lookup"><span data-stu-id="d985e-122">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="d985e-123">Filtrovat</span><span class="sxs-lookup"><span data-stu-id="d985e-123">Filter</span></span> | <span data-ttu-id="d985e-124">Řetězec filtru, který slouží k zúžení seznamu balíčků jeho použitím na ID, popis a značky balíčku.</span><span class="sxs-lookup"><span data-stu-id="d985e-124">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="d985e-125">První</span><span class="sxs-lookup"><span data-stu-id="d985e-125">First</span></span> | <span data-ttu-id="d985e-126">Počet balíčků, které mají být vráceny od začátku seznamu.</span><span class="sxs-lookup"><span data-stu-id="d985e-126">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="d985e-127">Pokud není zadaný, použije se výchozí hodnota 50.</span><span class="sxs-lookup"><span data-stu-id="d985e-127">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="d985e-128">Skip</span><span class="sxs-lookup"><span data-stu-id="d985e-128">Skip</span></span> | <span data-ttu-id="d985e-129">Vynechává první &lt;int&gt; Packages ze zobrazeného seznamu.</span><span class="sxs-lookup"><span data-stu-id="d985e-129">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="d985e-130">AllVersions</span><span class="sxs-lookup"><span data-stu-id="d985e-130">AllVersions</span></span> | <span data-ttu-id="d985e-131">Zobrazí všechny dostupné verze jednotlivých balíčků, nikoli jenom nejnovější verzi.</span><span class="sxs-lookup"><span data-stu-id="d985e-131">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="d985e-132">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="d985e-132">IncludePrerelease</span></span> | <span data-ttu-id="d985e-133">Zahrnuje předběžné verze balíčků ve výsledcích.</span><span class="sxs-lookup"><span data-stu-id="d985e-133">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="d985e-134">PageSize</span><span class="sxs-lookup"><span data-stu-id="d985e-134">PageSize</span></span> | <span data-ttu-id="d985e-135">*(3.0 +)* Pokud se při použití s-ListAvailable (povinné), počet balíčků, které se mají zobrazit, před tím, než se zobrazí výzva k pokračování.</span><span class="sxs-lookup"><span data-stu-id="d985e-135">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="d985e-136">Žádný z těchto parametrů nepřijímají vstupní ani zástupné znaky kanálu.</span><span class="sxs-lookup"><span data-stu-id="d985e-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="d985e-137">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="d985e-137">Common Parameters</span></span>

<span data-ttu-id="d985e-138">`Get-Package` podporuje následující [běžné parametry PowerShellu](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, inbuffer, subvariable, PipelineVariable, verbose, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="d985e-138">`Get-Package` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="d985e-139">Příklady</span><span class="sxs-lookup"><span data-stu-id="d985e-139">Examples</span></span>

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
