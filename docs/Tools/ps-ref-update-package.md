---
title: Referenční informace prostředí PowerShell aktualizace balíčku NuGet
description: Referenční dokumentace pro příkaz prostředí PowerShell balíček aktualizace v konzole Správce balíčků NuGet v sadě Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 621e59633117a29c58fe643860ee7e2b40a4fbe2
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
---
# <a name="update-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="f84d0-103">Balíček aktualizace (konzola Správce balíčků v sadě Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="f84d0-103">Update-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="f84d0-104">*K dispozici pouze v rámci [Konzola správce balíčků NuGet](package-manager-console.md) v sadě Visual Studio v systému Windows.*</span><span class="sxs-lookup"><span data-stu-id="f84d0-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="f84d0-105">Aktualizuje balíček a jeho závislosti nebo všechny balíčky v projektu, na novější verzi.</span><span class="sxs-lookup"><span data-stu-id="f84d0-105">Updates a package and its dependencies, or all packages in a project, to a newer version.</span></span>

## <a name="syntax"></a><span data-ttu-id="f84d0-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="f84d0-106">Syntax</span></span>

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="f84d0-107">V NuGet 2.8 + `Update-Package` lze použít na starší verzi existující balíček v projektu.</span><span class="sxs-lookup"><span data-stu-id="f84d0-107">In NuGet 2.8+, `Update-Package` can be used to downgrade an existing package in your project.</span></span> <span data-ttu-id="f84d0-108">Například pokud máte nainstalovaný 5.1.0-rc1 Microsoft.AspNet.MVC, následující příkaz by přejděte na starší 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="f84d0-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="f84d0-109">Parametry</span><span class="sxs-lookup"><span data-stu-id="f84d0-109">Parameters</span></span>

|  <span data-ttu-id="f84d0-110">Parametr</span><span class="sxs-lookup"><span data-stu-id="f84d0-110">Parameter</span></span> | <span data-ttu-id="f84d0-111">Popis</span><span class="sxs-lookup"><span data-stu-id="f84d0-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f84d0-112">ID</span><span class="sxs-lookup"><span data-stu-id="f84d0-112">Id</span></span> | <span data-ttu-id="f84d0-113">Identifikátor balíčku aktualizace.</span><span class="sxs-lookup"><span data-stu-id="f84d0-113">The identifier of the package to update.</span></span> <span data-ttu-id="f84d0-114">Pokud tento parametr vynechán, aktualizuje všechny balíčky.</span><span class="sxs-lookup"><span data-stu-id="f84d0-114">If omitted, updates all packages.</span></span> <span data-ttu-id="f84d0-115">-Id je volitelný přepínač sám sebe.</span><span class="sxs-lookup"><span data-stu-id="f84d0-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="f84d0-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="f84d0-116">IgnoreDependencies</span></span> | <span data-ttu-id="f84d0-117">Přeskočí aktualizace balíčku závislosti.</span><span class="sxs-lookup"><span data-stu-id="f84d0-117">Skips updating the package's dependencies.</span></span> |
| <span data-ttu-id="f84d0-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="f84d0-118">ProjectName</span></span> | <span data-ttu-id="f84d0-119">Název projektu obsahující balíčky aktualizace, jako výchozí bude použit na všechny projekty.</span><span class="sxs-lookup"><span data-stu-id="f84d0-119">The name of the project containing the packages to update, defaulting to all projects.</span></span> |
| <span data-ttu-id="f84d0-120">Version</span><span class="sxs-lookup"><span data-stu-id="f84d0-120">Version</span></span> | <span data-ttu-id="f84d0-121">Verze se má použít k upgradu, jako výchozí bude použit na nejnovější verzi.</span><span class="sxs-lookup"><span data-stu-id="f84d0-121">The version to use for the upgrade, defaulting to the latest version.</span></span> <span data-ttu-id="f84d0-122">V NuGet 3.0 a pozdější verze hodnota musí být jeden z *nejnižší, nejvyšší, HighestMinor*, nebo *HighestPatch* (ekvivalentní - bezpečné).</span><span class="sxs-lookup"><span data-stu-id="f84d0-122">In NuGet 3.0+, the version value must be one of *Lowest, Highest, HighestMinor*, or *HighestPatch* (equivalent to -Safe).</span></span> |
| <span data-ttu-id="f84d0-123">Bezpečné</span><span class="sxs-lookup"><span data-stu-id="f84d0-123">Safe</span></span> | <span data-ttu-id="f84d0-124">Omezí upgrade na pouze verze se stejnou hlavní a vedlejší verzi jako s aktuálně nainstalovaným balíčkem.</span><span class="sxs-lookup"><span data-stu-id="f84d0-124">Constrains upgrades to only versions with the same Major and Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="f84d0-125">Zdroj</span><span class="sxs-lookup"><span data-stu-id="f84d0-125">Source</span></span> | <span data-ttu-id="f84d0-126">Cestu adresy URL nebo ke složce zdroji balíčků pro vyhledávání.</span><span class="sxs-lookup"><span data-stu-id="f84d0-126">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="f84d0-127">Cesty k místní složce může být absolutní, nebo relativně vzhledem k aktuální složce.</span><span class="sxs-lookup"><span data-stu-id="f84d0-127">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="f84d0-128">Pokud tento parametr vynechán, `Update-Package` hledá aktuálně vybraném zdroji balíčku.</span><span class="sxs-lookup"><span data-stu-id="f84d0-128">If omitted, `Update-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="f84d0-129">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="f84d0-129">IncludePrerelease</span></span> | <span data-ttu-id="f84d0-130">Obsahuje předběžné verze balíčků aktualizací.</span><span class="sxs-lookup"><span data-stu-id="f84d0-130">Includes prerelease packages for updates.</span></span> |
| <span data-ttu-id="f84d0-131">Přeinstalujte</span><span class="sxs-lookup"><span data-stu-id="f84d0-131">Reinstall</span></span> | <span data-ttu-id="f84d0-132">Balíčky Resintalls pomocí jejich aktuálně nainstalované verze.</span><span class="sxs-lookup"><span data-stu-id="f84d0-132">Resintalls packages using their currently installed versions.</span></span> <span data-ttu-id="f84d0-133">V tématu [Reinstalling a aktualizaci balíčků](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="f84d0-133">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span> |
| <span data-ttu-id="f84d0-134">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="f84d0-134">FileConflictAction</span></span> | <span data-ttu-id="f84d0-135">Akce, který se má provést, když se zobrazí výzva k přepsání nebo ignorovat existující soubory, které se odkazuje na projekt.</span><span class="sxs-lookup"><span data-stu-id="f84d0-135">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="f84d0-136">Možné hodnoty jsou *přepsat, ignorovat, None, OverwriteAll*, a *IgnoreAll* (3.0 +).</span><span class="sxs-lookup"><span data-stu-id="f84d0-136">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *IgnoreAll* (3.0+).</span></span> |
| <span data-ttu-id="f84d0-137">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="f84d0-137">DependencyVersion</span></span> | <span data-ttu-id="f84d0-138">Verze závislosti balíčků chcete použít, které může být jedna z následujících akcí:</span><span class="sxs-lookup"><span data-stu-id="f84d0-138">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="f84d0-139">*Nejnižší* (výchozí): nejnižší verze</span><span class="sxs-lookup"><span data-stu-id="f84d0-139">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="f84d0-140">*HighestPatch*: oprava nejnižší hlavní, vedlejší nejnižší, nejvyšší verze</span><span class="sxs-lookup"><span data-stu-id="f84d0-140">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="f84d0-141">*HighestMinor*: verze se hlavní nejnižší, nejvyšší opravy menších, nejvyšší</span><span class="sxs-lookup"><span data-stu-id="f84d0-141">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="f84d0-142">*Nejvyšší* (výchozí nastavení pro balíček aktualizace bez parametrů): nejvyšší verze</span><span class="sxs-lookup"><span data-stu-id="f84d0-142">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="f84d0-143">Můžete nastavit výchozí hodnotu používanou [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) nastavení v `Nuget.Config` souboru.</span><span class="sxs-lookup"><span data-stu-id="f84d0-143">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="f84d0-144">ToHighestPatch</span><span class="sxs-lookup"><span data-stu-id="f84d0-144">ToHighestPatch</span></span> | <span data-ttu-id="f84d0-145">Omezí upgrade na pouze verze vedlejší verzi shodnou s aktuálně nainstalovaným balíčkem.</span><span class="sxs-lookup"><span data-stu-id="f84d0-145">Constrains upgrades to only versions with the same Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="f84d0-146">ToHighestMinor</span><span class="sxs-lookup"><span data-stu-id="f84d0-146">ToHighestMinor</span></span> | <span data-ttu-id="f84d0-147">Omezí upgrade na pouze verze se stejnou hlavní verzí jako s aktuálně nainstalovaným balíčkem.</span><span class="sxs-lookup"><span data-stu-id="f84d0-147">Constrains upgrades to only versions with the same Major version as the currently installed package.</span></span> |
| <span data-ttu-id="f84d0-148">WhatIf</span><span class="sxs-lookup"><span data-stu-id="f84d0-148">WhatIf</span></span> | <span data-ttu-id="f84d0-149">Zobrazuje, co by se stalo při spuštění příkazu bez ve skutečnosti provádí aktualizace.</span><span class="sxs-lookup"><span data-stu-id="f84d0-149">Shows what would happen when running the command without actually performing the update.</span></span> |

<span data-ttu-id="f84d0-150">Žádná z těchto parametrů přijmout kanálu vstup nebo zástupné znaky.</span><span class="sxs-lookup"><span data-stu-id="f84d0-150">None of these parameters accept pipeline input or wildcard characters.</span></span>

### <a name="common-parameters"></a><span data-ttu-id="f84d0-151">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="f84d0-151">Common Parameters</span></span>

<span data-ttu-id="f84d0-152">`Update-Package` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, podrobná, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="f84d0-152">`Update-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

### <a name="examples"></a><span data-ttu-id="f84d0-153">Příklady</span><span class="sxs-lookup"><span data-stu-id="f84d0-153">Examples</span></span>

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
