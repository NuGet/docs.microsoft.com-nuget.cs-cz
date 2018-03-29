---
title: Aktualizace balíčku NuGet referenční informace prostředí PowerShell | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referenční dokumentace pro příkaz prostředí PowerShell balíček aktualizace v konzole Správce balíčků NuGet v sadě Visual Studio.
keywords: NuGet konzoly Správce balíčků, příkazy prostředí NuGet Powershell, NuGet Powershell odkaz, balíček aktualizace
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 05772159d62f73e7d25f71ad36809f5ae8ef6aae
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="update-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="98be6-104">Balíček aktualizace (konzola Správce balíčků v sadě Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="98be6-104">Update-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="98be6-105">*K dispozici pouze v rámci [Konzola správce balíčků NuGet](package-manager-console.md) v sadě Visual Studio v systému Windows.*</span><span class="sxs-lookup"><span data-stu-id="98be6-105">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="98be6-106">Aktualizuje balíček a jeho závislosti nebo všechny balíčky v projektu, na novější verzi.</span><span class="sxs-lookup"><span data-stu-id="98be6-106">Updates a package and its dependencies, or all packages in a project, to a newer version.</span></span>

## <a name="syntax"></a><span data-ttu-id="98be6-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="98be6-107">Syntax</span></span>

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="98be6-108">V NuGet 2.8 + `Update-Package` lze použít na starší verzi existující balíček v projektu.</span><span class="sxs-lookup"><span data-stu-id="98be6-108">In NuGet 2.8+, `Update-Package` can be used to downgrade an existing package in your project.</span></span> <span data-ttu-id="98be6-109">Například pokud máte nainstalovaný 5.1.0-rc1 Microsoft.AspNet.MVC, následující příkaz by přejděte na starší 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="98be6-109">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="98be6-110">Parametry</span><span class="sxs-lookup"><span data-stu-id="98be6-110">Parameters</span></span>

|  <span data-ttu-id="98be6-111">Parametr</span><span class="sxs-lookup"><span data-stu-id="98be6-111">Parameter</span></span> | <span data-ttu-id="98be6-112">Popis</span><span class="sxs-lookup"><span data-stu-id="98be6-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="98be6-113">ID</span><span class="sxs-lookup"><span data-stu-id="98be6-113">Id</span></span> | <span data-ttu-id="98be6-114">Identifikátor balíčku aktualizace.</span><span class="sxs-lookup"><span data-stu-id="98be6-114">The identifier of the package to update.</span></span> <span data-ttu-id="98be6-115">Pokud tento parametr vynechán, aktualizuje všechny balíčky.</span><span class="sxs-lookup"><span data-stu-id="98be6-115">If omitted, updates all packages.</span></span> <span data-ttu-id="98be6-116">-Id je volitelný přepínač sám sebe.</span><span class="sxs-lookup"><span data-stu-id="98be6-116">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="98be6-117">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="98be6-117">IgnoreDependencies</span></span> | <span data-ttu-id="98be6-118">Přeskočí aktualizace balíčku závislosti.</span><span class="sxs-lookup"><span data-stu-id="98be6-118">Skips updating the package's dependencies.</span></span> |
| <span data-ttu-id="98be6-119">ProjectName</span><span class="sxs-lookup"><span data-stu-id="98be6-119">ProjectName</span></span> | <span data-ttu-id="98be6-120">Název projektu obsahující balíčky aktualizace, jako výchozí bude použit na všechny projekty.</span><span class="sxs-lookup"><span data-stu-id="98be6-120">The name of the project containing the packages to update, defaulting to all projects.</span></span> |
| <span data-ttu-id="98be6-121">Version</span><span class="sxs-lookup"><span data-stu-id="98be6-121">Version</span></span> | <span data-ttu-id="98be6-122">Verze se má použít k upgradu, jako výchozí bude použit na nejnovější verzi.</span><span class="sxs-lookup"><span data-stu-id="98be6-122">The version to use for the upgrade, defaulting to the latest version.</span></span> <span data-ttu-id="98be6-123">V NuGet 3.0 a pozdější verze hodnota musí být jeden z *nejnižší, nejvyšší, HighestMinor*, nebo *HighestPatch* (ekvivalentní - bezpečné).</span><span class="sxs-lookup"><span data-stu-id="98be6-123">In NuGet 3.0+, the version value must be one of *Lowest, Highest, HighestMinor*, or *HighestPatch* (equivalent to -Safe).</span></span> |
| <span data-ttu-id="98be6-124">Bezpečné</span><span class="sxs-lookup"><span data-stu-id="98be6-124">Safe</span></span> | <span data-ttu-id="98be6-125">Omezí upgrade na pouze verze se stejnou hlavní a vedlejší verzi jako s aktuálně nainstalovaným balíčkem.</span><span class="sxs-lookup"><span data-stu-id="98be6-125">Constrains upgrades to only versions with the same Major and Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="98be6-126">Zdroj</span><span class="sxs-lookup"><span data-stu-id="98be6-126">Source</span></span> | <span data-ttu-id="98be6-127">Cestu adresy URL nebo ke složce zdroji balíčků pro vyhledávání.</span><span class="sxs-lookup"><span data-stu-id="98be6-127">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="98be6-128">Cesty k místní složce může být absolutní, nebo relativně vzhledem k aktuální složce.</span><span class="sxs-lookup"><span data-stu-id="98be6-128">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="98be6-129">Pokud tento parametr vynechán, `Update-Package` hledá aktuálně vybraném zdroji balíčku.</span><span class="sxs-lookup"><span data-stu-id="98be6-129">If omitted, `Update-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="98be6-130">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="98be6-130">IncludePrerelease</span></span> | <span data-ttu-id="98be6-131">Obsahuje předběžné verze balíčků aktualizací.</span><span class="sxs-lookup"><span data-stu-id="98be6-131">Includes prerelease packages for updates.</span></span> |
| <span data-ttu-id="98be6-132">Přeinstalujte</span><span class="sxs-lookup"><span data-stu-id="98be6-132">Reinstall</span></span> | <span data-ttu-id="98be6-133">Balíčky Resintalls pomocí jejich aktuálně nainstalované verze.</span><span class="sxs-lookup"><span data-stu-id="98be6-133">Resintalls packages using their currently installed versions.</span></span> <span data-ttu-id="98be6-134">V tématu [Reinstalling a aktualizaci balíčků](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="98be6-134">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span> |
| <span data-ttu-id="98be6-135">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="98be6-135">FileConflictAction</span></span> | <span data-ttu-id="98be6-136">Akce, který se má provést, když se zobrazí výzva k přepsání nebo ignorovat existující soubory, které se odkazuje na projekt.</span><span class="sxs-lookup"><span data-stu-id="98be6-136">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="98be6-137">Možné hodnoty jsou *přepsat, ignorovat, None, OverwriteAll*, a *IgnoreAll* (3.0 +).</span><span class="sxs-lookup"><span data-stu-id="98be6-137">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *IgnoreAll* (3.0+).</span></span> |
| <span data-ttu-id="98be6-138">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="98be6-138">DependencyVersion</span></span> | <span data-ttu-id="98be6-139">Verze závislosti balíčků chcete použít, které může být jedna z následujících akcí:</span><span class="sxs-lookup"><span data-stu-id="98be6-139">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="98be6-140">*Nejnižší* (výchozí): nejnižší verze</span><span class="sxs-lookup"><span data-stu-id="98be6-140">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="98be6-141">*HighestPatch*: oprava nejnižší hlavní, vedlejší nejnižší, nejvyšší verze</span><span class="sxs-lookup"><span data-stu-id="98be6-141">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="98be6-142">*HighestMinor*: verze se hlavní nejnižší, nejvyšší opravy menších, nejvyšší</span><span class="sxs-lookup"><span data-stu-id="98be6-142">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="98be6-143">*Nejvyšší* (výchozí nastavení pro balíček aktualizace bez parametrů): nejvyšší verze</span><span class="sxs-lookup"><span data-stu-id="98be6-143">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="98be6-144">Můžete nastavit výchozí hodnotu používanou [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) nastavení v `Nuget.Config` souboru.</span><span class="sxs-lookup"><span data-stu-id="98be6-144">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="98be6-145">ToHighestPatch</span><span class="sxs-lookup"><span data-stu-id="98be6-145">ToHighestPatch</span></span> | <span data-ttu-id="98be6-146">Omezí upgrade na pouze verze vedlejší verzi shodnou s aktuálně nainstalovaným balíčkem.</span><span class="sxs-lookup"><span data-stu-id="98be6-146">Constrains upgrades to only versions with the same Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="98be6-147">ToHighestMinor</span><span class="sxs-lookup"><span data-stu-id="98be6-147">ToHighestMinor</span></span> | <span data-ttu-id="98be6-148">Omezí upgrade na pouze verze se stejnou hlavní verzí jako s aktuálně nainstalovaným balíčkem.</span><span class="sxs-lookup"><span data-stu-id="98be6-148">Constrains upgrades to only versions with the same Major version as the currently installed package.</span></span> |
| <span data-ttu-id="98be6-149">WhatIf</span><span class="sxs-lookup"><span data-stu-id="98be6-149">WhatIf</span></span> | <span data-ttu-id="98be6-150">Zobrazuje, co by se stalo při spuštění příkazu bez ve skutečnosti provádí aktualizace.</span><span class="sxs-lookup"><span data-stu-id="98be6-150">Shows what would happen when running the command without actually performing the update.</span></span> |

<span data-ttu-id="98be6-151">Žádná z těchto parametrů přijmout kanálu vstup nebo zástupné znaky.</span><span class="sxs-lookup"><span data-stu-id="98be6-151">None of these parameters accept pipeline input or wildcard characters.</span></span>

### <a name="common-parameters"></a><span data-ttu-id="98be6-152">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="98be6-152">Common Parameters</span></span>

<span data-ttu-id="98be6-153">`Update-Package` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, podrobná, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="98be6-153">`Update-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

### <a name="examples"></a><span data-ttu-id="98be6-154">Příklady</span><span class="sxs-lookup"><span data-stu-id="98be6-154">Examples</span></span>

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
