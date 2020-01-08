---
title: Referenční dokumentace PowerShellu pro synchronizaci balíčků NuGet
description: Reference k příkazu Sync-Package PowerShell v konzole správce balíčků NuGet v aplikaci Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 12a3d5f32056539a75da9e17b15d67e72a8a42c2
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384900"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="b67ac-103">Sync-Package (konzola Správce balíčků v sadě Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="b67ac-103">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="b67ac-104">*Verze 3.0 +; k dispozici pouze v rámci [konzoly Správce balíčků](../../consume-packages/install-use-packages-powershell.md) v sadě Visual Studio ve Windows.*</span><span class="sxs-lookup"><span data-stu-id="b67ac-104">*Version 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="b67ac-105">Získá verzi nainstalovaného balíčku z určeného (nebo výchozího) projektu a synchronizuje verzi s ostatními projekty v řešení.</span><span class="sxs-lookup"><span data-stu-id="b67ac-105">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="b67ac-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="b67ac-106">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="b67ac-107">Parametry</span><span class="sxs-lookup"><span data-stu-id="b67ac-107">Parameters</span></span>

| <span data-ttu-id="b67ac-108">Parametr</span><span class="sxs-lookup"><span data-stu-id="b67ac-108">Parameter</span></span> | <span data-ttu-id="b67ac-109">Popis</span><span class="sxs-lookup"><span data-stu-id="b67ac-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b67ac-110">Id</span><span class="sxs-lookup"><span data-stu-id="b67ac-110">Id</span></span> | <span data-ttu-id="b67ac-111">Požadovanou Identifikátor balíčku, který se má synchronizovat Samotný přepínač-ID je nepovinný.</span><span class="sxs-lookup"><span data-stu-id="b67ac-111">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="b67ac-112">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="b67ac-112">IgnoreDependencies</span></span> | <span data-ttu-id="b67ac-113">Nainstalujte jenom tento balíček a ne jeho závislosti.</span><span class="sxs-lookup"><span data-stu-id="b67ac-113">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="b67ac-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="b67ac-114">ProjectName</span></span> | <span data-ttu-id="b67ac-115">Projekt, z něhož má být balíček synchronizován, výchozí nastavení projektu.</span><span class="sxs-lookup"><span data-stu-id="b67ac-115">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="b67ac-116">Version</span><span class="sxs-lookup"><span data-stu-id="b67ac-116">Version</span></span> | <span data-ttu-id="b67ac-117">Verze balíčku, který se má synchronizovat, je nastavená verze na aktuálně nainstalovanou verzi.</span><span class="sxs-lookup"><span data-stu-id="b67ac-117">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="b67ac-118">Zdroj</span><span class="sxs-lookup"><span data-stu-id="b67ac-118">Source</span></span> | <span data-ttu-id="b67ac-119">Adresa URL nebo cesta ke složce pro zdroj balíčku, který má být prohledán.</span><span class="sxs-lookup"><span data-stu-id="b67ac-119">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="b67ac-120">Cesty k místní složce můžou být absolutní nebo relativní vzhledem k aktuální složce.</span><span class="sxs-lookup"><span data-stu-id="b67ac-120">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="b67ac-121">Pokud tento parametr vynecháte, `Sync-Package` prohledá aktuálně vybraný zdroj balíčku.</span><span class="sxs-lookup"><span data-stu-id="b67ac-121">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="b67ac-122">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="b67ac-122">IncludePrerelease</span></span> | <span data-ttu-id="b67ac-123">Zahrnuje předprodejní balíčky v synchronizaci.</span><span class="sxs-lookup"><span data-stu-id="b67ac-123">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="b67ac-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="b67ac-124">FileConflictAction</span></span> | <span data-ttu-id="b67ac-125">Akce, která se má provést, když se zobrazí výzva k přepsání nebo ignorování existujících souborů, na které se odkazuje v projektu</span><span class="sxs-lookup"><span data-stu-id="b67ac-125">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="b67ac-126">Možné hodnoty jsou *overwrite, ignore, None, OverwriteAll*a *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="b67ac-126">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="b67ac-127">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="b67ac-127">DependencyVersion</span></span> | <span data-ttu-id="b67ac-128">Verze balíčků závislostí, které se mají použít, což může být jedna z následujících:</span><span class="sxs-lookup"><span data-stu-id="b67ac-128">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="b67ac-129">*Nejnižší* (výchozí): nejnižší verze</span><span class="sxs-lookup"><span data-stu-id="b67ac-129">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="b67ac-130">*HighestPatch*: verze, která má nejnižší hlavní, nejnižší podverzi, nejvyšší opravu</span><span class="sxs-lookup"><span data-stu-id="b67ac-130">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="b67ac-131">*HighestMinor*: verze s nejnižší hlavní, nejvyšší podverze a nejvyšší opravou</span><span class="sxs-lookup"><span data-stu-id="b67ac-131">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="b67ac-132">*Nejvyšší* (výchozí pro balíček Update-Package bez parametrů): nejvyšší verze</span><span class="sxs-lookup"><span data-stu-id="b67ac-132">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="b67ac-133">Výchozí hodnotu můžete nastavit pomocí nastavení [`dependencyVersion`](../nuget-config-file.md#config-section) v souboru `Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="b67ac-133">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="b67ac-134">WhatIf</span><span class="sxs-lookup"><span data-stu-id="b67ac-134">WhatIf</span></span> | <span data-ttu-id="b67ac-135">Ukazuje, co se stane při spuštění příkazu, aniž by došlo ke skutečnému provedení synchronizace.</span><span class="sxs-lookup"><span data-stu-id="b67ac-135">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="b67ac-136">Žádný z těchto parametrů nepřijímají vstupní ani zástupné znaky kanálu.</span><span class="sxs-lookup"><span data-stu-id="b67ac-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="b67ac-137">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="b67ac-137">Common Parameters</span></span>

<span data-ttu-id="b67ac-138">`Sync-Package` podporuje následující [běžné parametry PowerShellu](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, inbuffer, subvariable, PipelineVariable, verbose, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="b67ac-138">`Sync-Package` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="b67ac-139">Příklady</span><span class="sxs-lookup"><span data-stu-id="b67ac-139">Examples</span></span>

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
