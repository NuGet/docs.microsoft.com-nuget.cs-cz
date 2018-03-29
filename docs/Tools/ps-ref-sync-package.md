---
title: Referenční informace prostředí PowerShell synchronizace balíček NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referenční dokumentace pro příkaz prostředí PowerShell synchronizace balíčku v konzole Správce balíčků NuGet v sadě Visual Studio.
keywords: NuGet konzoly Správce balíčků, příkazy prostředí NuGet Powershell, NuGet Powershell odkaz, synchronizace balíčku
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 0297015c3f1b8a8aced2545b4c4c3e6ccb1c7146
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="27bfe-104">Synchronizace Package (konzola Správce balíčků v sadě Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="27bfe-104">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="27bfe-105">*Verze 3.0 +; k dispozici pouze v rámci [Konzola správce balíčků NuGet](package-manager-console.md) v sadě Visual Studio v systému Windows.*</span><span class="sxs-lookup"><span data-stu-id="27bfe-105">*Version 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="27bfe-106">Získá verzi instalovaného balíčku z zadané (nebo výchozí) projektu a synchronizuje ji s ostatními projekty v řešení.</span><span class="sxs-lookup"><span data-stu-id="27bfe-106">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="27bfe-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="27bfe-107">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="27bfe-108">Parametry</span><span class="sxs-lookup"><span data-stu-id="27bfe-108">Parameters</span></span>

| <span data-ttu-id="27bfe-109">Parametr</span><span class="sxs-lookup"><span data-stu-id="27bfe-109">Parameter</span></span> | <span data-ttu-id="27bfe-110">Popis</span><span class="sxs-lookup"><span data-stu-id="27bfe-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="27bfe-111">ID</span><span class="sxs-lookup"><span data-stu-id="27bfe-111">Id</span></span> | <span data-ttu-id="27bfe-112">(Povinné) Identifikátor balíček, který chcete synchronizovat. -Id je volitelný přepínač sám sebe.</span><span class="sxs-lookup"><span data-stu-id="27bfe-112">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="27bfe-113">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="27bfe-113">IgnoreDependencies</span></span> | <span data-ttu-id="27bfe-114">Nainstalujte pouze tento balíček a bez jeho závislých součástí.</span><span class="sxs-lookup"><span data-stu-id="27bfe-114">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="27bfe-115">ProjectName</span><span class="sxs-lookup"><span data-stu-id="27bfe-115">ProjectName</span></span> | <span data-ttu-id="27bfe-116">Projekt pro synchronizaci balíčku, jako výchozí bude použit výchozí projekt.</span><span class="sxs-lookup"><span data-stu-id="27bfe-116">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="27bfe-117">Version</span><span class="sxs-lookup"><span data-stu-id="27bfe-117">Version</span></span> | <span data-ttu-id="27bfe-118">Verze balíčku k synchronizaci, jako výchozí bude použit aktuálně nainstalované verze.</span><span class="sxs-lookup"><span data-stu-id="27bfe-118">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="27bfe-119">Zdroj</span><span class="sxs-lookup"><span data-stu-id="27bfe-119">Source</span></span> | <span data-ttu-id="27bfe-120">Cestu adresy URL nebo ke složce zdroji balíčků pro vyhledávání.</span><span class="sxs-lookup"><span data-stu-id="27bfe-120">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="27bfe-121">Cesty k místní složce může být absolutní, nebo relativně vzhledem k aktuální složce.</span><span class="sxs-lookup"><span data-stu-id="27bfe-121">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="27bfe-122">Pokud tento parametr vynechán, `Sync-Package` hledá aktuálně vybraném zdroji balíčku.</span><span class="sxs-lookup"><span data-stu-id="27bfe-122">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="27bfe-123">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="27bfe-123">IncludePrerelease</span></span> | <span data-ttu-id="27bfe-124">Obsahuje předběžné verze balíčků v synchronizace.</span><span class="sxs-lookup"><span data-stu-id="27bfe-124">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="27bfe-125">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="27bfe-125">FileConflictAction</span></span> | <span data-ttu-id="27bfe-126">Akce, který se má provést, když se zobrazí výzva k přepsání nebo ignorovat existující soubory, které se odkazuje na projekt.</span><span class="sxs-lookup"><span data-stu-id="27bfe-126">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="27bfe-127">Možné hodnoty jsou *přepsat, ignorovat, None, OverwriteAll*, a *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="27bfe-127">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="27bfe-128">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="27bfe-128">DependencyVersion</span></span> | <span data-ttu-id="27bfe-129">Verze závislosti balíčků chcete použít, které může být jedna z následujících akcí:</span><span class="sxs-lookup"><span data-stu-id="27bfe-129">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="27bfe-130">*Nejnižší* (výchozí): nejnižší verze</span><span class="sxs-lookup"><span data-stu-id="27bfe-130">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="27bfe-131">*HighestPatch*: oprava nejnižší hlavní, vedlejší nejnižší, nejvyšší verze</span><span class="sxs-lookup"><span data-stu-id="27bfe-131">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="27bfe-132">*HighestMinor*: verze se hlavní nejnižší, nejvyšší opravy menších, nejvyšší</span><span class="sxs-lookup"><span data-stu-id="27bfe-132">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="27bfe-133">*Nejvyšší* (výchozí nastavení pro balíček aktualizace bez parametrů): nejvyšší verze</span><span class="sxs-lookup"><span data-stu-id="27bfe-133">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="27bfe-134">Můžete nastavit výchozí hodnotu používanou [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) nastavení v `Nuget.Config` souboru.</span><span class="sxs-lookup"><span data-stu-id="27bfe-134">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="27bfe-135">WhatIf</span><span class="sxs-lookup"><span data-stu-id="27bfe-135">WhatIf</span></span> | <span data-ttu-id="27bfe-136">Zobrazuje, co by se stalo při spuštění příkazu bez ve skutečnosti provádí synchronizaci.</span><span class="sxs-lookup"><span data-stu-id="27bfe-136">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="27bfe-137">Žádná z těchto parametrů přijmout kanálu vstup nebo zástupné znaky.</span><span class="sxs-lookup"><span data-stu-id="27bfe-137">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="27bfe-138">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="27bfe-138">Common Parameters</span></span>

<span data-ttu-id="27bfe-139">`Sync-Package` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, podrobná, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="27bfe-139">`Sync-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="27bfe-140">Příklady</span><span class="sxs-lookup"><span data-stu-id="27bfe-140">Examples</span></span>

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
