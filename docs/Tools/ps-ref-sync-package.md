---
title: "Referenční informace prostředí PowerShell synchronizace balíček NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 1b980b93-fa58-430c-b663-78ce069b1603
description: "Referenční dokumentace pro příkaz prostředí PowerShell synchronizace balíčku v konzole Správce balíčků NuGet v sadě Visual Studio."
keywords: "NuGet konzoly Správce balíčků, příkazy prostředí NuGet Powershell, NuGet Powershell odkaz, synchronizace balíčku"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4dc542714f14f0e6d3e827292f8fce06561fe270
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="16da3-104">Synchronizace Package (konzola Správce balíčků v sadě Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="16da3-104">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="16da3-105">*Verze 3.0 +; k dispozici pouze v rámci [Konzola správce balíčků NuGet](Package-Manager-Console.md) v sadě Visual Studio v systému Windows.*</span><span class="sxs-lookup"><span data-stu-id="16da3-105">*Version 3.0+; available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="16da3-106">Získá verzi instalovaného balíčku z zadané (nebo výchozí) projektu a synchronizuje ji s ostatními projekty v řešení.</span><span class="sxs-lookup"><span data-stu-id="16da3-106">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="16da3-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="16da3-107">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="16da3-108">Parametry</span><span class="sxs-lookup"><span data-stu-id="16da3-108">Parameters</span></span>

| <span data-ttu-id="16da3-109">Parametr</span><span class="sxs-lookup"><span data-stu-id="16da3-109">Parameter</span></span> | <span data-ttu-id="16da3-110">Popis</span><span class="sxs-lookup"><span data-stu-id="16da3-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="16da3-111">ID</span><span class="sxs-lookup"><span data-stu-id="16da3-111">Id</span></span> | <span data-ttu-id="16da3-112">(Povinné) Identifikátor balíček, který chcete synchronizovat. -Id je volitelný přepínač sám sebe.</span><span class="sxs-lookup"><span data-stu-id="16da3-112">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="16da3-113">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="16da3-113">IgnoreDependencies</span></span> | <span data-ttu-id="16da3-114">Nainstalujte pouze tento balíček a bez jeho závislých součástí.</span><span class="sxs-lookup"><span data-stu-id="16da3-114">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="16da3-115">ProjectName</span><span class="sxs-lookup"><span data-stu-id="16da3-115">ProjectName</span></span> | <span data-ttu-id="16da3-116">Projekt pro synchronizaci balíčku, jako výchozí bude použit výchozí projekt.</span><span class="sxs-lookup"><span data-stu-id="16da3-116">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="16da3-117">Version</span><span class="sxs-lookup"><span data-stu-id="16da3-117">Version</span></span> | <span data-ttu-id="16da3-118">Verze balíčku k synchronizaci, jako výchozí bude použit aktuálně nainstalované verze.</span><span class="sxs-lookup"><span data-stu-id="16da3-118">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="16da3-119">Zdroj</span><span class="sxs-lookup"><span data-stu-id="16da3-119">Source</span></span> | <span data-ttu-id="16da3-120">Cestu adresy URL nebo ke složce zdroji balíčků pro vyhledávání.</span><span class="sxs-lookup"><span data-stu-id="16da3-120">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="16da3-121">Cesty k místní složce může být absolutní, nebo relativně vzhledem k aktuální složce.</span><span class="sxs-lookup"><span data-stu-id="16da3-121">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="16da3-122">Pokud tento parametr vynechán, `Sync-Package` hledá aktuálně vybraném zdroji balíčku.</span><span class="sxs-lookup"><span data-stu-id="16da3-122">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="16da3-123">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="16da3-123">IncludePrerelease</span></span> | <span data-ttu-id="16da3-124">Obsahuje předběžné verze balíčků v synchronizace.</span><span class="sxs-lookup"><span data-stu-id="16da3-124">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="16da3-125">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="16da3-125">FileConflictAction</span></span> | <span data-ttu-id="16da3-126">Akce, který se má provést, když se zobrazí výzva k přepsání nebo ignorovat existující soubory, které se odkazuje na projekt.</span><span class="sxs-lookup"><span data-stu-id="16da3-126">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="16da3-127">Možné hodnoty jsou *přepsat, ignorovat, None, OverwriteAll*, a *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="16da3-127">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="16da3-128">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="16da3-128">DependencyVersion</span></span> | <span data-ttu-id="16da3-129">Verze závislosti balíčků chcete použít, které může být jedna z následujících akcí:</span><span class="sxs-lookup"><span data-stu-id="16da3-129">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="16da3-130">*Nejnižší* (výchozí): nejnižší verze</span><span class="sxs-lookup"><span data-stu-id="16da3-130">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="16da3-131">*HighestPatch*: oprava nejnižší hlavní, vedlejší nejnižší, nejvyšší verze</span><span class="sxs-lookup"><span data-stu-id="16da3-131">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="16da3-132">*HighestMinor*: verze se hlavní nejnižší, nejvyšší opravy menších, nejvyšší</span><span class="sxs-lookup"><span data-stu-id="16da3-132">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="16da3-133">*Nejvyšší* (výchozí nastavení pro balíček aktualizace bez parametrů): nejvyšší verze</span><span class="sxs-lookup"><span data-stu-id="16da3-133">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="16da3-134">Můžete nastavit výchozí hodnotu používanou [ `dependencyVersion` ](../Schema/nuget-config-file.md#config-section) nastavení v `Nuget.Config` souboru.</span><span class="sxs-lookup"><span data-stu-id="16da3-134">You can set the default value using the [`dependencyVersion`](../Schema/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="16da3-135">WhatIf</span><span class="sxs-lookup"><span data-stu-id="16da3-135">WhatIf</span></span> | <span data-ttu-id="16da3-136">Zobrazuje, co by se stalo při spuštění příkazu bez ve skutečnosti provádí synchronizaci.</span><span class="sxs-lookup"><span data-stu-id="16da3-136">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="16da3-137">Žádná z těchto parametrů přijmout kanálu vstup nebo zástupné znaky.</span><span class="sxs-lookup"><span data-stu-id="16da3-137">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="16da3-138">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="16da3-138">Common Parameters</span></span>

<span data-ttu-id="16da3-139">`Sync-Package`podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, podrobná, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="16da3-139">`Sync-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="16da3-140">Příklady</span><span class="sxs-lookup"><span data-stu-id="16da3-140">Examples</span></span>

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
