---
title: Referenční informace prostředí PowerShell synchronizace balíček NuGet
description: Referenční dokumentace pro příkaz prostředí PowerShell synchronizace balíčku v konzole Správce balíčků NuGet v sadě Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 424c4fbe3ff4b61c665bf7353976d4fb09268185
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="22142-103">Sync-Package (konzola Správce balíčků v sadě Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="22142-103">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="22142-104">*Verze 3.0 +; k dispozici pouze v rámci [Konzola správce balíčků NuGet](package-manager-console.md) v sadě Visual Studio v systému Windows.*</span><span class="sxs-lookup"><span data-stu-id="22142-104">*Version 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="22142-105">Získá verzi instalovaného balíčku z zadané (nebo výchozí) projektu a synchronizuje ji s ostatními projekty v řešení.</span><span class="sxs-lookup"><span data-stu-id="22142-105">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="22142-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="22142-106">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="22142-107">Parametry</span><span class="sxs-lookup"><span data-stu-id="22142-107">Parameters</span></span>

| <span data-ttu-id="22142-108">Parametr</span><span class="sxs-lookup"><span data-stu-id="22142-108">Parameter</span></span> | <span data-ttu-id="22142-109">Popis</span><span class="sxs-lookup"><span data-stu-id="22142-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="22142-110">ID</span><span class="sxs-lookup"><span data-stu-id="22142-110">Id</span></span> | <span data-ttu-id="22142-111">(Povinné) Identifikátor balíček, který chcete synchronizovat. -Id je volitelný přepínač sám sebe.</span><span class="sxs-lookup"><span data-stu-id="22142-111">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="22142-112">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="22142-112">IgnoreDependencies</span></span> | <span data-ttu-id="22142-113">Nainstalujte pouze tento balíček a bez jeho závislých součástí.</span><span class="sxs-lookup"><span data-stu-id="22142-113">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="22142-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="22142-114">ProjectName</span></span> | <span data-ttu-id="22142-115">Projekt pro synchronizaci balíčku, jako výchozí bude použit výchozí projekt.</span><span class="sxs-lookup"><span data-stu-id="22142-115">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="22142-116">Version</span><span class="sxs-lookup"><span data-stu-id="22142-116">Version</span></span> | <span data-ttu-id="22142-117">Verze balíčku k synchronizaci, jako výchozí bude použit aktuálně nainstalované verze.</span><span class="sxs-lookup"><span data-stu-id="22142-117">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="22142-118">Zdroj</span><span class="sxs-lookup"><span data-stu-id="22142-118">Source</span></span> | <span data-ttu-id="22142-119">Cestu adresy URL nebo ke složce zdroji balíčků pro vyhledávání.</span><span class="sxs-lookup"><span data-stu-id="22142-119">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="22142-120">Cesty k místní složce může být absolutní, nebo relativně vzhledem k aktuální složce.</span><span class="sxs-lookup"><span data-stu-id="22142-120">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="22142-121">Pokud tento parametr vynechán, `Sync-Package` hledá aktuálně vybraném zdroji balíčku.</span><span class="sxs-lookup"><span data-stu-id="22142-121">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="22142-122">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="22142-122">IncludePrerelease</span></span> | <span data-ttu-id="22142-123">Obsahuje předběžné verze balíčků v synchronizace.</span><span class="sxs-lookup"><span data-stu-id="22142-123">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="22142-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="22142-124">FileConflictAction</span></span> | <span data-ttu-id="22142-125">Akce, který se má provést, když se zobrazí výzva k přepsání nebo ignorovat existující soubory, které se odkazuje na projekt.</span><span class="sxs-lookup"><span data-stu-id="22142-125">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="22142-126">Možné hodnoty jsou *přepsat, ignorovat, None, OverwriteAll*, a *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="22142-126">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="22142-127">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="22142-127">DependencyVersion</span></span> | <span data-ttu-id="22142-128">Verze závislosti balíčků chcete použít, které může být jedna z následujících akcí:</span><span class="sxs-lookup"><span data-stu-id="22142-128">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="22142-129">*Nejnižší* (výchozí): nejnižší verze</span><span class="sxs-lookup"><span data-stu-id="22142-129">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="22142-130">*HighestPatch*: oprava nejnižší hlavní, vedlejší nejnižší, nejvyšší verze</span><span class="sxs-lookup"><span data-stu-id="22142-130">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="22142-131">*HighestMinor*: verze se hlavní nejnižší, nejvyšší opravy menších, nejvyšší</span><span class="sxs-lookup"><span data-stu-id="22142-131">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="22142-132">*Nejvyšší* (výchozí nastavení pro balíček aktualizace bez parametrů): nejvyšší verze</span><span class="sxs-lookup"><span data-stu-id="22142-132">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="22142-133">Můžete nastavit výchozí hodnotu používanou [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) nastavení v `Nuget.Config` souboru.</span><span class="sxs-lookup"><span data-stu-id="22142-133">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="22142-134">WhatIf</span><span class="sxs-lookup"><span data-stu-id="22142-134">WhatIf</span></span> | <span data-ttu-id="22142-135">Zobrazuje, co by se stalo při spuštění příkazu bez ve skutečnosti provádí synchronizaci.</span><span class="sxs-lookup"><span data-stu-id="22142-135">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="22142-136">Žádná z těchto parametrů přijmout kanálu vstup nebo zástupné znaky.</span><span class="sxs-lookup"><span data-stu-id="22142-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="22142-137">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="22142-137">Common Parameters</span></span>

<span data-ttu-id="22142-138">`Sync-Package` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, podrobná, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="22142-138">`Sync-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="22142-139">Příklady</span><span class="sxs-lookup"><span data-stu-id="22142-139">Examples</span></span>

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
