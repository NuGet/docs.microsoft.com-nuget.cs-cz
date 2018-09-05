---
title: Referenční informace prostředí PowerShell pro aktualizaci balíčku NuGet
description: Referenční informace pro příkaz Powershellu Update-Package v konzole Správce balíčků NuGet v sadě Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d47e1978ab7d827e0b8b97cd4e7237019185b50f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546073"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="afb50-103">Update-Package (konzola Správce balíčků v sadě Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="afb50-103">Update-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="afb50-104">*K dispozici pouze v rámci [Konzola správce balíčků NuGet](package-manager-console.md) v sadě Visual Studio ve Windows.*</span><span class="sxs-lookup"><span data-stu-id="afb50-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="afb50-105">Aktualizuje balíček a jeho závislosti nebo všechny balíčky v projektu, na novější verzi.</span><span class="sxs-lookup"><span data-stu-id="afb50-105">Updates a package and its dependencies, or all packages in a project, to a newer version.</span></span>

## <a name="syntax"></a><span data-ttu-id="afb50-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="afb50-106">Syntax</span></span>

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="afb50-107">Ve Správci NuGet 2.8 + `Update-Package` je možné přejít na nižší verzi existujícího balíčku ve vašem projektu.</span><span class="sxs-lookup"><span data-stu-id="afb50-107">In NuGet 2.8+, `Update-Package` can be used to downgrade an existing package in your project.</span></span> <span data-ttu-id="afb50-108">Například pokud máte nainstalovaný 5.1.0-rc1 Microsoft.AspNet.MVC následujícího příkazu by downgradovat ho 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="afb50-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="afb50-109">Parametry</span><span class="sxs-lookup"><span data-stu-id="afb50-109">Parameters</span></span>

|  <span data-ttu-id="afb50-110">Parametr</span><span class="sxs-lookup"><span data-stu-id="afb50-110">Parameter</span></span> | <span data-ttu-id="afb50-111">Popis</span><span class="sxs-lookup"><span data-stu-id="afb50-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="afb50-112">ID</span><span class="sxs-lookup"><span data-stu-id="afb50-112">Id</span></span> | <span data-ttu-id="afb50-113">Identifikátor balíčku aktualizace.</span><span class="sxs-lookup"><span data-stu-id="afb50-113">The identifier of the package to update.</span></span> <span data-ttu-id="afb50-114">Pokud tento parametr vynechán, aktualizuje všechny balíčky.</span><span class="sxs-lookup"><span data-stu-id="afb50-114">If omitted, updates all packages.</span></span> <span data-ttu-id="afb50-115">-Id je volitelný přepínač samotný.</span><span class="sxs-lookup"><span data-stu-id="afb50-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="afb50-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="afb50-116">IgnoreDependencies</span></span> | <span data-ttu-id="afb50-117">Přeskočí aktualizace závislosti balíčku.</span><span class="sxs-lookup"><span data-stu-id="afb50-117">Skips updating the package's dependencies.</span></span> |
| <span data-ttu-id="afb50-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="afb50-118">ProjectName</span></span> | <span data-ttu-id="afb50-119">Název projektu, který obsahuje balíčky pro, jako výchozí se použije na všechny projekty.</span><span class="sxs-lookup"><span data-stu-id="afb50-119">The name of the project containing the packages to update, defaulting to all projects.</span></span> |
| <span data-ttu-id="afb50-120">Version</span><span class="sxs-lookup"><span data-stu-id="afb50-120">Version</span></span> | <span data-ttu-id="afb50-121">Verze, který se má použít k upgradu, jako výchozí se použije na nejnovější verzi.</span><span class="sxs-lookup"><span data-stu-id="afb50-121">The version to use for the upgrade, defaulting to the latest version.</span></span> <span data-ttu-id="afb50-122">Ve Správci NuGet 3.0, hodnota verze musí být jeden z *nejnižší, nejvyšší, HighestMinor*, nebo *HighestPatch* (ekvivalentní – bezpečné).</span><span class="sxs-lookup"><span data-stu-id="afb50-122">In NuGet 3.0+, the version value must be one of *Lowest, Highest, HighestMinor*, or *HighestPatch* (equivalent to -Safe).</span></span> |
| <span data-ttu-id="afb50-123">Bezpečné</span><span class="sxs-lookup"><span data-stu-id="afb50-123">Safe</span></span> | <span data-ttu-id="afb50-124">Omezí upgrade na pouze verze se stejnou verzí hlavní a podverze jako nainstalovaný balíček.</span><span class="sxs-lookup"><span data-stu-id="afb50-124">Constrains upgrades to only versions with the same Major and Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="afb50-125">Zdroj</span><span class="sxs-lookup"><span data-stu-id="afb50-125">Source</span></span> | <span data-ttu-id="afb50-126">Cesta URL nebo složku zdroje balíčku. Chcete-li hledat.</span><span class="sxs-lookup"><span data-stu-id="afb50-126">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="afb50-127">Cesty k místní složce může být absolutní nebo relativní vzhledem k aktuální složky.</span><span class="sxs-lookup"><span data-stu-id="afb50-127">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="afb50-128">Pokud tento parametr vynechán, `Update-Package` hledá aktuálně vybraném zdroji balíčku.</span><span class="sxs-lookup"><span data-stu-id="afb50-128">If omitted, `Update-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="afb50-129">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="afb50-129">IncludePrerelease</span></span> | <span data-ttu-id="afb50-130">Obsahuje předběžné verze balíčků aktualizace.</span><span class="sxs-lookup"><span data-stu-id="afb50-130">Includes prerelease packages for updates.</span></span> |
| <span data-ttu-id="afb50-131">Znovu nainstalujte</span><span class="sxs-lookup"><span data-stu-id="afb50-131">Reinstall</span></span> | <span data-ttu-id="afb50-132">Resintalls balíčků pomocí jejich aktuálně nainstalované verze.</span><span class="sxs-lookup"><span data-stu-id="afb50-132">Resintalls packages using their currently installed versions.</span></span> <span data-ttu-id="afb50-133">Zobrazit [Reinstalling a aktualizace balíčků](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="afb50-133">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span> |
| <span data-ttu-id="afb50-134">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="afb50-134">FileConflictAction</span></span> | <span data-ttu-id="afb50-135">Akce, který se má provést, když se zobrazí výzva k přepsání nebo ignorovat existující soubory, které jsou odkazované projektem.</span><span class="sxs-lookup"><span data-stu-id="afb50-135">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="afb50-136">Možné hodnoty jsou *přepsat, ignorovat, None, OverwriteAll*, a *IgnoreAll* (3.0 +).</span><span class="sxs-lookup"><span data-stu-id="afb50-136">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *IgnoreAll* (3.0+).</span></span> |
| <span data-ttu-id="afb50-137">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="afb50-137">DependencyVersion</span></span> | <span data-ttu-id="afb50-138">Verze závislé balíčky použití, které může být jedna z následujících akcí:</span><span class="sxs-lookup"><span data-stu-id="afb50-138">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="afb50-139">*Nejnižší* (výchozí): nejnižší verze</span><span class="sxs-lookup"><span data-stu-id="afb50-139">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="afb50-140">*HighestPatch*: verze s nejnižší hlavní, vedlejší nejnižší, nejvyšší oprava</span><span class="sxs-lookup"><span data-stu-id="afb50-140">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="afb50-141">*HighestMinor*: verze s hlavní nejnižší, nejvyšší podverze, nejvyšší oprava</span><span class="sxs-lookup"><span data-stu-id="afb50-141">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="afb50-142">*Nejvyšší* (výchozí pro Update-Package bez parametrů): nejvyšší verze</span><span class="sxs-lookup"><span data-stu-id="afb50-142">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="afb50-143">Můžete nastavit výchozí hodnotu používanou [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) nastavení `Nuget.Config` souboru.</span><span class="sxs-lookup"><span data-stu-id="afb50-143">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="afb50-144">ToHighestPatch</span><span class="sxs-lookup"><span data-stu-id="afb50-144">ToHighestPatch</span></span> | <span data-ttu-id="afb50-145">Omezí upgrade na pouze verze s využitím stejné podverze jako nainstalovaný balíček.</span><span class="sxs-lookup"><span data-stu-id="afb50-145">Constrains upgrades to only versions with the same Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="afb50-146">ToHighestMinor</span><span class="sxs-lookup"><span data-stu-id="afb50-146">ToHighestMinor</span></span> | <span data-ttu-id="afb50-147">Omezí upgrade na pouze verze se stejnou hlavní verzí jako nainstalovaný balíček.</span><span class="sxs-lookup"><span data-stu-id="afb50-147">Constrains upgrades to only versions with the same Major version as the currently installed package.</span></span> |
| <span data-ttu-id="afb50-148">WhatIf</span><span class="sxs-lookup"><span data-stu-id="afb50-148">WhatIf</span></span> | <span data-ttu-id="afb50-149">Ukazuje, co by se stalo při spuštění příkazu bez samotnému provedení aktualizace.</span><span class="sxs-lookup"><span data-stu-id="afb50-149">Shows what would happen when running the command without actually performing the update.</span></span> |

<span data-ttu-id="afb50-150">Žádná z těchto parametrů přijímat kanálu vstup nebo zástupné znaky.</span><span class="sxs-lookup"><span data-stu-id="afb50-150">None of these parameters accept pipeline input or wildcard characters.</span></span>

### <a name="common-parameters"></a><span data-ttu-id="afb50-151">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="afb50-151">Common Parameters</span></span>

<span data-ttu-id="afb50-152">`Update-Package` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="afb50-152">`Update-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

### <a name="examples"></a><span data-ttu-id="afb50-153">Příklady</span><span class="sxs-lookup"><span data-stu-id="afb50-153">Examples</span></span>

```ps
# Updates all packages in every project of the solution
Update-Package

# Updates every package in the MvcApplication1 project
Update-Package -ProjectName MvcApplication1

# Updates the Elmah package in every project to the latest version
Update-Package Elmah

# Updates the Elmah package to version 1.1.0 in every project showing optional -Id usage
Update-Package -Id Elmah -Version 1.1.0

# Updates the Elmah package within the MvcApplication1 project to the highest "safe" version.
# For example, if Elmah version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2,
# and 1.1 are available in the feed, the -Safe parameter updates the package to 1.0.2 instead
# of 1.1 as it would otherwise.
Update-Package Elmah -ProjectName MvcApplication1 -Safe

# Reinstall the same version of the original package, but with the latest version of dependencies
# (subject to version constraints). If this command rolls a dependency back to an earlier version,
# use Update-Package <dependency_name> to reinstall that one dependency without affecting the
# dependent package.
Update-Package ELmah –reinstall 

# Reinstall the Elmah package in just MyProject
Update-Package Elmah -ProjectName MyProject -reinstall

# Reinstall the same version of the original package without touching dependencies.
Update-Package ELmah –reinstall -ignoreDependencies
```
