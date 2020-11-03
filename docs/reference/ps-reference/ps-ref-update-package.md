---
title: Reference k NuGet Update-Package PowerShellu
description: Referenční informace k příkazu Update-Package PowerShellu v konzole správce balíčků NuGet v aplikaci Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: af918d11e8f976be962d52084c5eda4d53e382c6
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238033"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="402ca-103">Update-Package (konzola správce balíčků v aplikaci Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="402ca-103">Update-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="402ca-104">*K dispozici pouze v rámci [konzoly Správce balíčků NuGet](../../consume-packages/install-use-packages-powershell.md) v sadě Visual Studio ve Windows.*</span><span class="sxs-lookup"><span data-stu-id="402ca-104">*Available only within the [NuGet Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="402ca-105">Aktualizuje balíček a jeho závislosti nebo všechny balíčky v projektu na novější verzi.</span><span class="sxs-lookup"><span data-stu-id="402ca-105">Updates a package and its dependencies, or all packages in a project, to a newer version.</span></span>

## <a name="syntax"></a><span data-ttu-id="402ca-106">Syntax</span><span class="sxs-lookup"><span data-stu-id="402ca-106">Syntax</span></span>

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="402ca-107">V NuGet 2.8 + `Update-Package` lze použít k downgradování existujícího balíčku v projektu.</span><span class="sxs-lookup"><span data-stu-id="402ca-107">In NuGet 2.8+, `Update-Package` can be used to downgrade an existing package in your project.</span></span> <span data-ttu-id="402ca-108">Například pokud máte nainstalovanou aplikaci Microsoft. AspNet. MVC 5.1.0-RC1, následující příkaz by ho měl downgradovat na 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="402ca-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="402ca-109">Parametry</span><span class="sxs-lookup"><span data-stu-id="402ca-109">Parameters</span></span>

|  <span data-ttu-id="402ca-110">Parametr</span><span class="sxs-lookup"><span data-stu-id="402ca-110">Parameter</span></span> | <span data-ttu-id="402ca-111">Popis</span><span class="sxs-lookup"><span data-stu-id="402ca-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="402ca-112">Id</span><span class="sxs-lookup"><span data-stu-id="402ca-112">Id</span></span> | <span data-ttu-id="402ca-113">Identifikátor balíčku, který se má aktualizovat</span><span class="sxs-lookup"><span data-stu-id="402ca-113">The identifier of the package to update.</span></span> <span data-ttu-id="402ca-114">Pokud tento parametr vynecháte, aktualizuje všechny balíčky.</span><span class="sxs-lookup"><span data-stu-id="402ca-114">If omitted, updates all packages.</span></span> <span data-ttu-id="402ca-115">Samotný přepínač-ID je nepovinný.</span><span class="sxs-lookup"><span data-stu-id="402ca-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="402ca-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="402ca-116">IgnoreDependencies</span></span> | <span data-ttu-id="402ca-117">Přeskočí aktualizaci závislostí balíčku.</span><span class="sxs-lookup"><span data-stu-id="402ca-117">Skips updating the package's dependencies.</span></span> |
| <span data-ttu-id="402ca-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="402ca-118">ProjectName</span></span> | <span data-ttu-id="402ca-119">Název projektu obsahujícího balíčky, které se mají aktualizovat – výchozí nastavení pro všechny projekty</span><span class="sxs-lookup"><span data-stu-id="402ca-119">The name of the project containing the packages to update, defaulting to all projects.</span></span> |
| <span data-ttu-id="402ca-120">Verze</span><span class="sxs-lookup"><span data-stu-id="402ca-120">Version</span></span> | <span data-ttu-id="402ca-121">Verze, která se má použít pro upgrade, ve výchozím nastavení na nejnovější verzi.</span><span class="sxs-lookup"><span data-stu-id="402ca-121">The version to use for the upgrade, defaulting to the latest version.</span></span> <span data-ttu-id="402ca-122">V NuGet 3.0 + musí být hodnota verze jedna z *nejnižší, nejvyšší, HighestMinor* nebo *HighestPatch* (ekvivalentní k bezpečnému).</span><span class="sxs-lookup"><span data-stu-id="402ca-122">In NuGet 3.0+, the version value must be one of *Lowest, Highest, HighestMinor* , or *HighestPatch* (equivalent to -Safe).</span></span> |
| <span data-ttu-id="402ca-123">Odvod</span><span class="sxs-lookup"><span data-stu-id="402ca-123">Safe</span></span> | <span data-ttu-id="402ca-124">Omezuje upgrady jenom na verze se stejnou hlavní a dílčí verzí jako aktuálně nainstalovaný balíček.</span><span class="sxs-lookup"><span data-stu-id="402ca-124">Constrains upgrades to only versions with the same Major and Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="402ca-125">Zdroj</span><span class="sxs-lookup"><span data-stu-id="402ca-125">Source</span></span> | <span data-ttu-id="402ca-126">Adresa URL nebo cesta ke složce pro zdroj balíčku, který má být prohledán.</span><span class="sxs-lookup"><span data-stu-id="402ca-126">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="402ca-127">Cesty k místní složce můžou být absolutní nebo relativní vzhledem k aktuální složce.</span><span class="sxs-lookup"><span data-stu-id="402ca-127">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="402ca-128">Pokud tento parametr vynecháte, `Update-Package` vyhledá aktuálně vybraný zdroj balíčku.</span><span class="sxs-lookup"><span data-stu-id="402ca-128">If omitted, `Update-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="402ca-129">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="402ca-129">IncludePrerelease</span></span> | <span data-ttu-id="402ca-130">Zahrnuje předběžné verze balíčků pro aktualizace.</span><span class="sxs-lookup"><span data-stu-id="402ca-130">Includes prerelease packages for updates.</span></span> |
| <span data-ttu-id="402ca-131">Instaluje</span><span class="sxs-lookup"><span data-stu-id="402ca-131">Reinstall</span></span> | <span data-ttu-id="402ca-132">Resintalls balíčky pomocí jejich aktuálně nainstalovaných verzí.</span><span class="sxs-lookup"><span data-stu-id="402ca-132">Resintalls packages using their currently installed versions.</span></span> <span data-ttu-id="402ca-133">Viz [Přeinstalace a aktualizace balíčků](../../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="402ca-133">See [Reinstalling and updating packages](../../consume-packages/reinstalling-and-updating-packages.md).</span></span> |
| <span data-ttu-id="402ca-134">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="402ca-134">FileConflictAction</span></span> | <span data-ttu-id="402ca-135">Akce, která se má provést, když se zobrazí výzva k přepsání nebo ignorování existujících souborů, na které se odkazuje v projektu</span><span class="sxs-lookup"><span data-stu-id="402ca-135">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="402ca-136">Možné hodnoty jsou *overwrite, ignore, None, OverwriteAll* a *IgnoreAll* (3.0 +).</span><span class="sxs-lookup"><span data-stu-id="402ca-136">Possible values are *Overwrite, Ignore, None, OverwriteAll* , and *IgnoreAll* (3.0+).</span></span> |
| <span data-ttu-id="402ca-137">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="402ca-137">DependencyVersion</span></span> | <span data-ttu-id="402ca-138">Verze balíčků závislostí, které se mají použít, což může být jedna z následujících:</span><span class="sxs-lookup"><span data-stu-id="402ca-138">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="402ca-139">*Nejnižší* (výchozí): nejnižší verze</span><span class="sxs-lookup"><span data-stu-id="402ca-139">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="402ca-140">*HighestPatch* : verze, která má nejnižší hlavní, nejnižší podverzi, nejvyšší opravu</span><span class="sxs-lookup"><span data-stu-id="402ca-140">*HighestPatch* : the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="402ca-141">*HighestMinor* : verze s nejnižší hlavní, nejvyšší podverze a nejvyšší opravou</span><span class="sxs-lookup"><span data-stu-id="402ca-141">*HighestMinor* : the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="402ca-142">*Nejvyšší* (výchozí pro Update-Package bez parametrů): nejvyšší verze</span><span class="sxs-lookup"><span data-stu-id="402ca-142">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="402ca-143">Výchozí hodnotu můžete nastavit pomocí [`dependencyVersion`](../nuget-config-file.md#config-section) nastavení v `Nuget.Config` souboru.</span><span class="sxs-lookup"><span data-stu-id="402ca-143">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="402ca-144">ToHighestPatch</span><span class="sxs-lookup"><span data-stu-id="402ca-144">ToHighestPatch</span></span> | <span data-ttu-id="402ca-145">ekvivalent – Safe.</span><span class="sxs-lookup"><span data-stu-id="402ca-145">equivalent to -Safe.</span></span> |
| <span data-ttu-id="402ca-146">ToHighestMinor</span><span class="sxs-lookup"><span data-stu-id="402ca-146">ToHighestMinor</span></span> | <span data-ttu-id="402ca-147">Omezuje upgrady jenom na verze se stejnou hlavní verzí jako aktuálně nainstalovaný balíček.</span><span class="sxs-lookup"><span data-stu-id="402ca-147">Constrains upgrades to only versions with the same Major version as the currently installed package.</span></span> |
| <span data-ttu-id="402ca-148">WhatIf</span><span class="sxs-lookup"><span data-stu-id="402ca-148">WhatIf</span></span> | <span data-ttu-id="402ca-149">Ukazuje, co se stane při spuštění příkazu bez toho, aby se aktualizace skutečně prováděla.</span><span class="sxs-lookup"><span data-stu-id="402ca-149">Shows what would happen when running the command without actually performing the update.</span></span> |

<span data-ttu-id="402ca-150">Žádný z těchto parametrů nepřijímají vstupní ani zástupné znaky kanálu.</span><span class="sxs-lookup"><span data-stu-id="402ca-150">None of these parameters accept pipeline input or wildcard characters.</span></span>

### <a name="common-parameters"></a><span data-ttu-id="402ca-151">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="402ca-151">Common Parameters</span></span>

<span data-ttu-id="402ca-152">`Update-Package` podporuje následující [běžné parametry PowerShellu](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, inbuffer, subvariable, PipelineVariable, verbose, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="402ca-152">`Update-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

### <a name="examples"></a><span data-ttu-id="402ca-153">Příklady</span><span class="sxs-lookup"><span data-stu-id="402ca-153">Examples</span></span>

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
Update-Package Elmah –reinstall 

# Reinstall the Elmah package in just MyProject
Update-Package Elmah -ProjectName MyProject -reinstall

# Reinstall the same version of the original package without touching dependencies.
Update-Package Elmah –reinstall -ignoreDependencies
```
