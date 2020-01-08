---
title: Aktualizace NuGet – Reference k balíčku PowerShell
description: Reference k příkazu Update-Package PowerShell v konzole správce balíčků NuGet v aplikaci Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: e1bff9d4b7391d8be87afa4b8f2fbd51ae922140
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384853"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="18104-103">Update-Package (konzola Správce balíčků v sadě Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="18104-103">Update-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="18104-104">*K dispozici pouze v rámci [konzoly Správce balíčků NuGet](../../consume-packages/install-use-packages-powershell.md) v sadě Visual Studio ve Windows.*</span><span class="sxs-lookup"><span data-stu-id="18104-104">*Available only within the [NuGet Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="18104-105">Aktualizuje balíček a jeho závislosti nebo všechny balíčky v projektu na novější verzi.</span><span class="sxs-lookup"><span data-stu-id="18104-105">Updates a package and its dependencies, or all packages in a project, to a newer version.</span></span>

## <a name="syntax"></a><span data-ttu-id="18104-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="18104-106">Syntax</span></span>

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="18104-107">V NuGet 2.8 + můžete `Update-Package` použít k downgradování existujícího balíčku v projektu.</span><span class="sxs-lookup"><span data-stu-id="18104-107">In NuGet 2.8+, `Update-Package` can be used to downgrade an existing package in your project.</span></span> <span data-ttu-id="18104-108">Například pokud máte nainstalovanou aplikaci Microsoft. AspNet. MVC 5.1.0-RC1, následující příkaz by ho měl downgradovat na 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="18104-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="18104-109">Parametry</span><span class="sxs-lookup"><span data-stu-id="18104-109">Parameters</span></span>

|  <span data-ttu-id="18104-110">Parametr</span><span class="sxs-lookup"><span data-stu-id="18104-110">Parameter</span></span> | <span data-ttu-id="18104-111">Popis</span><span class="sxs-lookup"><span data-stu-id="18104-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="18104-112">Id</span><span class="sxs-lookup"><span data-stu-id="18104-112">Id</span></span> | <span data-ttu-id="18104-113">Identifikátor balíčku, který se má aktualizovat</span><span class="sxs-lookup"><span data-stu-id="18104-113">The identifier of the package to update.</span></span> <span data-ttu-id="18104-114">Pokud tento parametr vynecháte, aktualizuje všechny balíčky.</span><span class="sxs-lookup"><span data-stu-id="18104-114">If omitted, updates all packages.</span></span> <span data-ttu-id="18104-115">Samotný přepínač-ID je nepovinný.</span><span class="sxs-lookup"><span data-stu-id="18104-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="18104-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="18104-116">IgnoreDependencies</span></span> | <span data-ttu-id="18104-117">Přeskočí aktualizaci závislostí balíčku.</span><span class="sxs-lookup"><span data-stu-id="18104-117">Skips updating the package's dependencies.</span></span> |
| <span data-ttu-id="18104-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="18104-118">ProjectName</span></span> | <span data-ttu-id="18104-119">Název projektu obsahujícího balíčky, které se mají aktualizovat – výchozí nastavení pro všechny projekty</span><span class="sxs-lookup"><span data-stu-id="18104-119">The name of the project containing the packages to update, defaulting to all projects.</span></span> |
| <span data-ttu-id="18104-120">Version</span><span class="sxs-lookup"><span data-stu-id="18104-120">Version</span></span> | <span data-ttu-id="18104-121">Verze, která se má použít pro upgrade, ve výchozím nastavení na nejnovější verzi.</span><span class="sxs-lookup"><span data-stu-id="18104-121">The version to use for the upgrade, defaulting to the latest version.</span></span> <span data-ttu-id="18104-122">V NuGet 3.0 + musí být hodnota verze jedna z *nejnižší, nejvyšší, HighestMinor*nebo *HighestPatch* (ekvivalentní k bezpečnému).</span><span class="sxs-lookup"><span data-stu-id="18104-122">In NuGet 3.0+, the version value must be one of *Lowest, Highest, HighestMinor*, or *HighestPatch* (equivalent to -Safe).</span></span> |
| <span data-ttu-id="18104-123">Odvod</span><span class="sxs-lookup"><span data-stu-id="18104-123">Safe</span></span> | <span data-ttu-id="18104-124">Omezuje upgrady jenom na verze se stejnou hlavní a dílčí verzí jako aktuálně nainstalovaný balíček.</span><span class="sxs-lookup"><span data-stu-id="18104-124">Constrains upgrades to only versions with the same Major and Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="18104-125">Zdroj</span><span class="sxs-lookup"><span data-stu-id="18104-125">Source</span></span> | <span data-ttu-id="18104-126">Adresa URL nebo cesta ke složce pro zdroj balíčku, který má být prohledán.</span><span class="sxs-lookup"><span data-stu-id="18104-126">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="18104-127">Cesty k místní složce můžou být absolutní nebo relativní vzhledem k aktuální složce.</span><span class="sxs-lookup"><span data-stu-id="18104-127">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="18104-128">Pokud tento parametr vynecháte, `Update-Package` prohledá aktuálně vybraný zdroj balíčku.</span><span class="sxs-lookup"><span data-stu-id="18104-128">If omitted, `Update-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="18104-129">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="18104-129">IncludePrerelease</span></span> | <span data-ttu-id="18104-130">Zahrnuje předběžné verze balíčků pro aktualizace.</span><span class="sxs-lookup"><span data-stu-id="18104-130">Includes prerelease packages for updates.</span></span> |
| <span data-ttu-id="18104-131">Přeinstalace</span><span class="sxs-lookup"><span data-stu-id="18104-131">Reinstall</span></span> | <span data-ttu-id="18104-132">Resintalls balíčky pomocí jejich aktuálně nainstalovaných verzí.</span><span class="sxs-lookup"><span data-stu-id="18104-132">Resintalls packages using their currently installed versions.</span></span> <span data-ttu-id="18104-133">Viz [Přeinstalace a aktualizace balíčků](../../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="18104-133">See [Reinstalling and updating packages](../../consume-packages/reinstalling-and-updating-packages.md).</span></span> |
| <span data-ttu-id="18104-134">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="18104-134">FileConflictAction</span></span> | <span data-ttu-id="18104-135">Akce, která se má provést, když se zobrazí výzva k přepsání nebo ignorování existujících souborů, na které se odkazuje v projektu</span><span class="sxs-lookup"><span data-stu-id="18104-135">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="18104-136">Možné hodnoty jsou *overwrite, ignore, None, OverwriteAll*a *IgnoreAll* (3.0 +).</span><span class="sxs-lookup"><span data-stu-id="18104-136">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *IgnoreAll* (3.0+).</span></span> |
| <span data-ttu-id="18104-137">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="18104-137">DependencyVersion</span></span> | <span data-ttu-id="18104-138">Verze balíčků závislostí, které se mají použít, což může být jedna z následujících:</span><span class="sxs-lookup"><span data-stu-id="18104-138">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="18104-139">*Nejnižší* (výchozí): nejnižší verze</span><span class="sxs-lookup"><span data-stu-id="18104-139">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="18104-140">*HighestPatch*: verze, která má nejnižší hlavní, nejnižší podverzi, nejvyšší opravu</span><span class="sxs-lookup"><span data-stu-id="18104-140">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="18104-141">*HighestMinor*: verze s nejnižší hlavní, nejvyšší podverze a nejvyšší opravou</span><span class="sxs-lookup"><span data-stu-id="18104-141">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="18104-142">*Nejvyšší* (výchozí pro balíček Update-Package bez parametrů): nejvyšší verze</span><span class="sxs-lookup"><span data-stu-id="18104-142">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="18104-143">Výchozí hodnotu můžete nastavit pomocí nastavení [`dependencyVersion`](../nuget-config-file.md#config-section) v souboru `Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="18104-143">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="18104-144">ToHighestPatch</span><span class="sxs-lookup"><span data-stu-id="18104-144">ToHighestPatch</span></span> | <span data-ttu-id="18104-145">ekvivalent – Safe.</span><span class="sxs-lookup"><span data-stu-id="18104-145">equivalent to -Safe.</span></span> |
| <span data-ttu-id="18104-146">ToHighestMinor</span><span class="sxs-lookup"><span data-stu-id="18104-146">ToHighestMinor</span></span> | <span data-ttu-id="18104-147">Omezuje upgrady jenom na verze se stejnou hlavní verzí jako aktuálně nainstalovaný balíček.</span><span class="sxs-lookup"><span data-stu-id="18104-147">Constrains upgrades to only versions with the same Major version as the currently installed package.</span></span> |
| <span data-ttu-id="18104-148">WhatIf</span><span class="sxs-lookup"><span data-stu-id="18104-148">WhatIf</span></span> | <span data-ttu-id="18104-149">Ukazuje, co se stane při spuštění příkazu bez toho, aby se aktualizace skutečně prováděla.</span><span class="sxs-lookup"><span data-stu-id="18104-149">Shows what would happen when running the command without actually performing the update.</span></span> |

<span data-ttu-id="18104-150">Žádný z těchto parametrů nepřijímají vstupní ani zástupné znaky kanálu.</span><span class="sxs-lookup"><span data-stu-id="18104-150">None of these parameters accept pipeline input or wildcard characters.</span></span>

### <a name="common-parameters"></a><span data-ttu-id="18104-151">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="18104-151">Common Parameters</span></span>

<span data-ttu-id="18104-152">`Update-Package` podporuje následující [běžné parametry PowerShellu](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, inbuffer, subvariable, PipelineVariable, verbose, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="18104-152">`Update-Package` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

### <a name="examples"></a><span data-ttu-id="18104-153">Příklady</span><span class="sxs-lookup"><span data-stu-id="18104-153">Examples</span></span>

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
