---
title: Reference k prostředí PowerShell pro instalaci balíčků NuGet
description: Reference k příkazu Install-Package PowerShell v konzole správce balíčků NuGet v aplikaci Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 1899662049735189ab4dcb728df5d56afdc5f7c5
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328204"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="13ce9-103">Install-Package (konzola Správce balíčků v sadě Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="13ce9-103">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="13ce9-104">*Toto téma popisuje příkaz v [konzole správce balíčků](../../consume-packages/install-use-packages-powershell.md) v sadě Visual Studio ve Windows. Obecný příkaz k instalaci balíčku PowerShellu najdete v referenčních [informacích k PowerShellu PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="13ce9-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="13ce9-105">Nainstaluje balíček a jeho závislosti do projektu.</span><span class="sxs-lookup"><span data-stu-id="13ce9-105">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="13ce9-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="13ce9-106">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="13ce9-107">V NuGet 2.8 + `Install-Package` může downgradovat existující balíček v projektu.</span><span class="sxs-lookup"><span data-stu-id="13ce9-107">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="13ce9-108">Například pokud máte nainstalovanou aplikaci Microsoft. AspNet. MVC 5.1.0-RC1, následující příkaz by ho měl downgradovat na 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="13ce9-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="13ce9-109">Parametry</span><span class="sxs-lookup"><span data-stu-id="13ce9-109">Parameters</span></span>

| <span data-ttu-id="13ce9-110">Parametr</span><span class="sxs-lookup"><span data-stu-id="13ce9-110">Parameter</span></span> | <span data-ttu-id="13ce9-111">Popis</span><span class="sxs-lookup"><span data-stu-id="13ce9-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="13ce9-112">Id</span><span class="sxs-lookup"><span data-stu-id="13ce9-112">Id</span></span> | <span data-ttu-id="13ce9-113">Požadovanou Identifikátor balíčku, který se má nainstalovat</span><span class="sxs-lookup"><span data-stu-id="13ce9-113">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="13ce9-114">(*3.0 +* ) Identifikátor může být cesta nebo adresa URL `packages.config` souboru `.nupkg` nebo souboru.</span><span class="sxs-lookup"><span data-stu-id="13ce9-114">(*3.0+*) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="13ce9-115">Samotný přepínač-ID je nepovinný.</span><span class="sxs-lookup"><span data-stu-id="13ce9-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="13ce9-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="13ce9-116">IgnoreDependencies</span></span> | <span data-ttu-id="13ce9-117">Nainstalujte jenom tento balíček a ne jeho závislosti.</span><span class="sxs-lookup"><span data-stu-id="13ce9-117">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="13ce9-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="13ce9-118">ProjectName</span></span> | <span data-ttu-id="13ce9-119">Projekt, do kterého má být balíček nainstalován, je nastaven výchozí projekt.</span><span class="sxs-lookup"><span data-stu-id="13ce9-119">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="13ce9-120">Source</span><span class="sxs-lookup"><span data-stu-id="13ce9-120">Source</span></span> | <span data-ttu-id="13ce9-121">Adresa URL nebo cesta ke složce pro zdroj balíčku, který má být prohledán.</span><span class="sxs-lookup"><span data-stu-id="13ce9-121">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="13ce9-122">Cesty k místní složce můžou být absolutní nebo relativní vzhledem k aktuální složce.</span><span class="sxs-lookup"><span data-stu-id="13ce9-122">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="13ce9-123">Pokud tento parametr vynecháte, `Install-Package` vyhledá aktuálně vybraný zdroj balíčku.</span><span class="sxs-lookup"><span data-stu-id="13ce9-123">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="13ce9-124">Version</span><span class="sxs-lookup"><span data-stu-id="13ce9-124">Version</span></span> | <span data-ttu-id="13ce9-125">Verze balíčku, který se má nainstalovat, ve výchozím nastavení na nejnovější verzi</span><span class="sxs-lookup"><span data-stu-id="13ce9-125">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="13ce9-126">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="13ce9-126">IncludePrerelease</span></span> | <span data-ttu-id="13ce9-127">Bere v úvahu předběžné verze balíčků pro instalaci.</span><span class="sxs-lookup"><span data-stu-id="13ce9-127">Considers prerelease packages for the install.</span></span> <span data-ttu-id="13ce9-128">Pokud tento parametr vynecháte, budou se brát v úvahu jenom stabilní balíčky.</span><span class="sxs-lookup"><span data-stu-id="13ce9-128">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="13ce9-129">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="13ce9-129">FileConflictAction</span></span> | <span data-ttu-id="13ce9-130">Akce, která se má provést, když se zobrazí výzva k přepsání nebo ignorování existujících souborů, na které se odkazuje v projektu</span><span class="sxs-lookup"><span data-stu-id="13ce9-130">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="13ce9-131">Možné hodnoty jsou *overwrite, ignore, None, OverwriteAll*a *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="13ce9-131">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="13ce9-132">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="13ce9-132">DependencyVersion</span></span> | <span data-ttu-id="13ce9-133">Verze balíčků závislostí, které se mají použít, což může být jedna z následujících:</span><span class="sxs-lookup"><span data-stu-id="13ce9-133">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="13ce9-134">*Nejnižší* (výchozí): nejnižší verze</span><span class="sxs-lookup"><span data-stu-id="13ce9-134">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="13ce9-135">*HighestPatch*: verze, která má nejnižší hlavní, nejnižší podverzi, nejvyšší opravu</span><span class="sxs-lookup"><span data-stu-id="13ce9-135">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="13ce9-136">*HighestMinor*: verze s nejnižší hlavní, nejvyšší podverze a nejvyšší opravou</span><span class="sxs-lookup"><span data-stu-id="13ce9-136">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="13ce9-137">*Nejvyšší úroveň* (výchozí pro balíček Update-Package bez parametrů): nejvyšší verze</span><span class="sxs-lookup"><span data-stu-id="13ce9-137">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="13ce9-138">Výchozí hodnotu můžete nastavit pomocí [`dependencyVersion`](../nuget-config-file.md#config-section) nastavení `Nuget.Config` v souboru.</span><span class="sxs-lookup"><span data-stu-id="13ce9-138">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="13ce9-139">WhatIf</span><span class="sxs-lookup"><span data-stu-id="13ce9-139">WhatIf</span></span> | <span data-ttu-id="13ce9-140">Ukazuje, co se stane při spuštění příkazu, aniž by bylo nutné instalaci skutečně provést.</span><span class="sxs-lookup"><span data-stu-id="13ce9-140">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="13ce9-141">Žádný z těchto parametrů nepřijímají vstupní ani zástupné znaky kanálu.</span><span class="sxs-lookup"><span data-stu-id="13ce9-141">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="13ce9-142">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="13ce9-142">Common Parameters</span></span>

<span data-ttu-id="13ce9-143">`Install-Package`podporuje následující [běžné parametry PowerShellu](http://go.microsoft.com/fwlink/?LinkID=113216): Ladit, Error Action, ErrorVariable, unbuffer, subvariable, PipelineVariable, verbose, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="13ce9-143">`Install-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="13ce9-144">Příklady</span><span class="sxs-lookup"><span data-stu-id="13ce9-144">Examples</span></span>

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
# Note: the URL must end with "packages.config"
Install-Package https://raw.githubusercontent.com/linked-data-dotnet/json-ld.net/master/.nuget/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-Package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
# Note: the URL must end with ".nupkg"
Install-Package https://globalcdn.nuget.org/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
