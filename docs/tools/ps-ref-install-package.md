---
title: Referenční informace k Powershellu nainstalujte balíček NuGet
description: Referenční informace pro příkaz Powershellu Install-Package v konzole Správce balíčků NuGet v sadě Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 755c87bbc68d3b688c81e16edbc1faabdc9e0520
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842502"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="8ba28-103">Install-Package (konzola Správce balíčků v sadě Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="8ba28-103">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="8ba28-104">*Toto téma popisuje příkaz v rámci [Konzola správce balíčků](package-manager-console.md) v sadě Visual Studio ve Windows. Obecný příkaz prostředí PowerShell Install-Package, najdete v článku [odkazu modulu Powershellu PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="8ba28-104">*This topic describes the command within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="8ba28-105">Nainstaluje do projektu balíček a jeho závislosti.</span><span class="sxs-lookup"><span data-stu-id="8ba28-105">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="8ba28-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="8ba28-106">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="8ba28-107">Ve Správci NuGet 2.8 + `Install-Package` můžou provést downgrade existující balíček ve vašem projektu.</span><span class="sxs-lookup"><span data-stu-id="8ba28-107">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="8ba28-108">Například pokud máte nainstalovaný 5.1.0-rc1 Microsoft.AspNet.MVC následujícího příkazu by downgradovat ho 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="8ba28-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="8ba28-109">Parametry</span><span class="sxs-lookup"><span data-stu-id="8ba28-109">Parameters</span></span>

| <span data-ttu-id="8ba28-110">Parametr</span><span class="sxs-lookup"><span data-stu-id="8ba28-110">Parameter</span></span> | <span data-ttu-id="8ba28-111">Popis</span><span class="sxs-lookup"><span data-stu-id="8ba28-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8ba28-112">Id</span><span class="sxs-lookup"><span data-stu-id="8ba28-112">Id</span></span> | <span data-ttu-id="8ba28-113">(Povinné) Identifikátor balíčku pro instalaci.</span><span class="sxs-lookup"><span data-stu-id="8ba28-113">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="8ba28-114">(*3.0 +* ) identifikátor může být cesta nebo adresa URL `packages.config` souboru nebo `.nupkg` souboru.</span><span class="sxs-lookup"><span data-stu-id="8ba28-114">(*3.0+*) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="8ba28-115">-Id je volitelný přepínač samotný.</span><span class="sxs-lookup"><span data-stu-id="8ba28-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="8ba28-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="8ba28-116">IgnoreDependencies</span></span> | <span data-ttu-id="8ba28-117">Nainstalujte pouze tento balíček a nikoli jeho závislé.</span><span class="sxs-lookup"><span data-stu-id="8ba28-117">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="8ba28-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="8ba28-118">ProjectName</span></span> | <span data-ttu-id="8ba28-119">Projekt, do kterého chcete balíček nainstalovat, jako výchozí se použije výchozí projekt.</span><span class="sxs-lookup"><span data-stu-id="8ba28-119">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="8ba28-120">Source</span><span class="sxs-lookup"><span data-stu-id="8ba28-120">Source</span></span> | <span data-ttu-id="8ba28-121">Cesta URL nebo složku zdroje balíčku. Chcete-li hledat.</span><span class="sxs-lookup"><span data-stu-id="8ba28-121">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="8ba28-122">Cesty k místní složce může být absolutní nebo relativní vzhledem k aktuální složky.</span><span class="sxs-lookup"><span data-stu-id="8ba28-122">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="8ba28-123">Pokud tento parametr vynechán, `Install-Package` hledá aktuálně vybraném zdroji balíčku.</span><span class="sxs-lookup"><span data-stu-id="8ba28-123">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="8ba28-124">Version</span><span class="sxs-lookup"><span data-stu-id="8ba28-124">Version</span></span> | <span data-ttu-id="8ba28-125">Verze balíčku k instalaci, jako výchozí se použije na nejnovější verzi.</span><span class="sxs-lookup"><span data-stu-id="8ba28-125">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="8ba28-126">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="8ba28-126">IncludePrerelease</span></span> | <span data-ttu-id="8ba28-127">Bere v úvahu předběžné verze balíčků pro instalaci.</span><span class="sxs-lookup"><span data-stu-id="8ba28-127">Considers prerelease packages for the install.</span></span> <span data-ttu-id="8ba28-128">Pokud tento parametr vynechán, jsou považovány za pouze stabilní balíčky.</span><span class="sxs-lookup"><span data-stu-id="8ba28-128">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="8ba28-129">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="8ba28-129">FileConflictAction</span></span> | <span data-ttu-id="8ba28-130">Akce, který se má provést, když se zobrazí výzva k přepsání nebo ignorovat existující soubory, které jsou odkazované projektem.</span><span class="sxs-lookup"><span data-stu-id="8ba28-130">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="8ba28-131">Možné hodnoty jsou *přepsat, ignorovat, None, OverwriteAll*, a *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="8ba28-131">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="8ba28-132">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="8ba28-132">DependencyVersion</span></span> | <span data-ttu-id="8ba28-133">Verze závislé balíčky použití, které může být jedna z následujících akcí:</span><span class="sxs-lookup"><span data-stu-id="8ba28-133">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="8ba28-134">*Nejnižší* (výchozí): nejnižší verze</span><span class="sxs-lookup"><span data-stu-id="8ba28-134">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="8ba28-135">*HighestPatch*: verze s nejnižší hlavní, vedlejší nejnižší, nejvyšší oprava</span><span class="sxs-lookup"><span data-stu-id="8ba28-135">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="8ba28-136">*HighestMinor*: verze s hlavní nejnižší, nejvyšší podverze, nejvyšší oprava</span><span class="sxs-lookup"><span data-stu-id="8ba28-136">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="8ba28-137">*Nejvyšší* (výchozí pro Update-Package bez parametrů): nejvyšší verze</span><span class="sxs-lookup"><span data-stu-id="8ba28-137">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="8ba28-138">Můžete nastavit výchozí hodnotu používanou [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) nastavení `Nuget.Config` souboru.</span><span class="sxs-lookup"><span data-stu-id="8ba28-138">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="8ba28-139">WhatIf</span><span class="sxs-lookup"><span data-stu-id="8ba28-139">WhatIf</span></span> | <span data-ttu-id="8ba28-140">Ukazuje, co by se stalo při spuštění příkazu bez samotnému provedení instalace.</span><span class="sxs-lookup"><span data-stu-id="8ba28-140">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="8ba28-141">Žádná z těchto parametrů přijímat kanálu vstup nebo zástupné znaky.</span><span class="sxs-lookup"><span data-stu-id="8ba28-141">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="8ba28-142">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="8ba28-142">Common Parameters</span></span>

<span data-ttu-id="8ba28-143">`Install-Package` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="8ba28-143">`Install-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="8ba28-144">Příklady</span><span class="sxs-lookup"><span data-stu-id="8ba28-144">Examples</span></span>

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
Install-package https://raw.githubusercontent.com/json-ld.net/master/src/JsonLD/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
Install-package https://az320820.vo.msecnd.net/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
