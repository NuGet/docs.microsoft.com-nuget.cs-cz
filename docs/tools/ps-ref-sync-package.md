---
title: Referenční informace prostředí PowerShell synchronizace balíček NuGet
description: Referenční informace pro příkaz Powershellu synchronizace-Package v konzole Správce balíčků NuGet v sadě Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8119664b1bafe9238b12b1819cc46dc1ee7bdd00
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547991"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="a4b74-103">Sync-Package (konzola Správce balíčků v sadě Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="a4b74-103">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="a4b74-104">*Verze 3.0 a; k dispozici pouze v rámci [Konzola správce balíčků NuGet](package-manager-console.md) v sadě Visual Studio ve Windows.*</span><span class="sxs-lookup"><span data-stu-id="a4b74-104">*Version 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="a4b74-105">Získá verzi nainstalovaného balíčku ze zadané (nebo výchozí) projektu a synchronizuje na verzi, aby Zbývající projekty v řešení.</span><span class="sxs-lookup"><span data-stu-id="a4b74-105">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="a4b74-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="a4b74-106">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="a4b74-107">Parametry</span><span class="sxs-lookup"><span data-stu-id="a4b74-107">Parameters</span></span>

| <span data-ttu-id="a4b74-108">Parametr</span><span class="sxs-lookup"><span data-stu-id="a4b74-108">Parameter</span></span> | <span data-ttu-id="a4b74-109">Popis</span><span class="sxs-lookup"><span data-stu-id="a4b74-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a4b74-110">ID</span><span class="sxs-lookup"><span data-stu-id="a4b74-110">Id</span></span> | <span data-ttu-id="a4b74-111">(Povinné) Identifikátor balíčku, který se synchronizuje. -Id je volitelný přepínač samotný.</span><span class="sxs-lookup"><span data-stu-id="a4b74-111">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="a4b74-112">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="a4b74-112">IgnoreDependencies</span></span> | <span data-ttu-id="a4b74-113">Nainstalujte pouze tento balíček a nikoli jeho závislé.</span><span class="sxs-lookup"><span data-stu-id="a4b74-113">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="a4b74-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="a4b74-114">ProjectName</span></span> | <span data-ttu-id="a4b74-115">Projekt pro synchronizaci balíčku, jako výchozí se použije výchozí projekt.</span><span class="sxs-lookup"><span data-stu-id="a4b74-115">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="a4b74-116">Version</span><span class="sxs-lookup"><span data-stu-id="a4b74-116">Version</span></span> | <span data-ttu-id="a4b74-117">Verze balíčku k synchronizaci, jako výchozí se použije aktuálně nainstalovanou verzi.</span><span class="sxs-lookup"><span data-stu-id="a4b74-117">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="a4b74-118">Zdroj</span><span class="sxs-lookup"><span data-stu-id="a4b74-118">Source</span></span> | <span data-ttu-id="a4b74-119">Cesta URL nebo složku zdroje balíčku. Chcete-li hledat.</span><span class="sxs-lookup"><span data-stu-id="a4b74-119">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="a4b74-120">Cesty k místní složce může být absolutní nebo relativní vzhledem k aktuální složky.</span><span class="sxs-lookup"><span data-stu-id="a4b74-120">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="a4b74-121">Pokud tento parametr vynechán, `Sync-Package` hledá aktuálně vybraném zdroji balíčku.</span><span class="sxs-lookup"><span data-stu-id="a4b74-121">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="a4b74-122">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="a4b74-122">IncludePrerelease</span></span> | <span data-ttu-id="a4b74-123">Obsahuje předběžné verze balíčků v synchronizace.</span><span class="sxs-lookup"><span data-stu-id="a4b74-123">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="a4b74-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="a4b74-124">FileConflictAction</span></span> | <span data-ttu-id="a4b74-125">Akce, který se má provést, když se zobrazí výzva k přepsání nebo ignorovat existující soubory, které jsou odkazované projektem.</span><span class="sxs-lookup"><span data-stu-id="a4b74-125">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="a4b74-126">Možné hodnoty jsou *přepsat, ignorovat, None, OverwriteAll*, a *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="a4b74-126">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="a4b74-127">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="a4b74-127">DependencyVersion</span></span> | <span data-ttu-id="a4b74-128">Verze závislé balíčky použití, které může být jedna z následujících akcí:</span><span class="sxs-lookup"><span data-stu-id="a4b74-128">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="a4b74-129">*Nejnižší* (výchozí): nejnižší verze</span><span class="sxs-lookup"><span data-stu-id="a4b74-129">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="a4b74-130">*HighestPatch*: verze s nejnižší hlavní, vedlejší nejnižší, nejvyšší oprava</span><span class="sxs-lookup"><span data-stu-id="a4b74-130">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="a4b74-131">*HighestMinor*: verze s hlavní nejnižší, nejvyšší podverze, nejvyšší oprava</span><span class="sxs-lookup"><span data-stu-id="a4b74-131">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="a4b74-132">*Nejvyšší* (výchozí pro Update-Package bez parametrů): nejvyšší verze</span><span class="sxs-lookup"><span data-stu-id="a4b74-132">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="a4b74-133">Můžete nastavit výchozí hodnotu používanou [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) nastavení `Nuget.Config` souboru.</span><span class="sxs-lookup"><span data-stu-id="a4b74-133">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="a4b74-134">WhatIf</span><span class="sxs-lookup"><span data-stu-id="a4b74-134">WhatIf</span></span> | <span data-ttu-id="a4b74-135">Ukazuje, co by se stalo při spuštění příkazu bez samotnému provedení synchronizace.</span><span class="sxs-lookup"><span data-stu-id="a4b74-135">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="a4b74-136">Žádná z těchto parametrů přijímat kanálu vstup nebo zástupné znaky.</span><span class="sxs-lookup"><span data-stu-id="a4b74-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="a4b74-137">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="a4b74-137">Common Parameters</span></span>

<span data-ttu-id="a4b74-138">`Sync-Package` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="a4b74-138">`Sync-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="a4b74-139">Příklady</span><span class="sxs-lookup"><span data-stu-id="a4b74-139">Examples</span></span>

```ps
# Sync the Elmah package installed in the default project into the other projects in the solution
Sync-Package Elmah

# Sync the Elmah package installed in the ClassLibrary1 project into other projects in the solution
Sync-Package Elmah -ProjectName ClassLibrary1

# Sync Microsoft.Aspnet.package but not its dependencies into the other projects in the solution
Sync-Package Microsoft.Aspnet.Mvc -IgnoreDependencies

# Sync jQuery.Validation and install the highest version of jQuery (a dependency) from the package source    
Sync-Package jQuery.Validation -DependencyVersion highest
```
