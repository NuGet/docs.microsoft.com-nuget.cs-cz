---
title: Referenční informace prostředí PowerShell NuGet
description: Úplný odkaz na příkazy prostředí PowerShell, které jsou k dispozici v konzoli správce balíčků NuGet v sadě Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: ba9f5dc2b570298d9011f62a081631ec31623701
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34816987"
---
# <a name="powershell-reference"></a><span data-ttu-id="a090a-103">Referenční informace prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="a090a-103">PowerShell reference</span></span>

<span data-ttu-id="a090a-104">Konzola správce balíčků poskytuje rozhraní PowerShell v sadě Visual Studio v systému Windows pro interakci s NuGet prostřednictvím určité příkazy uvedené níže.</span><span class="sxs-lookup"><span data-stu-id="a090a-104">The Package Manager Console provides a PowerShell interface within Visual Studio on Windows to interact with NuGet through the specific commands listed below.</span></span> <span data-ttu-id="a090a-105">(Konzole není v současné době k dispozici v sadě Visual Studio for Mac.) Průvodce pomocí konzoly, najdete v článku [Konzola správce balíčků](../tools/package-manager-console.md) tématu.</span><span class="sxs-lookup"><span data-stu-id="a090a-105">(The console is not presently available in Visual Studio for Mac.) For a guide to using the console, see the [Package Manager Console](../tools/package-manager-console.md) topic.</span></span>

> [!Tip]
> <span data-ttu-id="a090a-106">Všechny příkazy prostředí PowerShell se týkají pouze spotřeba balíčku.</span><span class="sxs-lookup"><span data-stu-id="a090a-106">All PowerShell commands relate only to package consumption.</span></span> <span data-ttu-id="a090a-107">Žádné příkazy prostředí PowerShell se vztahují k vytváření a publikování balíčků s výjimkou, pokud balíček může být také příjemce další balíčky.</span><span class="sxs-lookup"><span data-stu-id="a090a-107">No PowerShell commands relate to creating and publishing packages except to the extent that a package can also be a consumer of other packages.</span></span>

> [!Important]
> <span data-ttu-id="a090a-108">Zde uvedené příkazy jsou specifické pro konzolu Správce balíčků v sadě Visual Studio a liší od [příkazy modulu správy balíčků](/powershell/module/packagemanagement/?view=powershell-6) které jsou k dispozici v obecné prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a090a-108">The commands listed here are specific to the Package Manager Console in Visual Studio, and differ from the [Package Management module commands](/powershell/module/packagemanagement/?view=powershell-6) that are available in a general PowerShell environment.</span></span> <span data-ttu-id="a090a-109">Konkrétně každé prostředí má příkazy, které nejsou k dispozici v dalších a příkazy se stejným názvem, může se také liší v jejich konkrétní argumenty.</span><span class="sxs-lookup"><span data-stu-id="a090a-109">Specifically, each environment has commands that are not available in the other, and commands with the same name may also differ in their specific arguments.</span></span> <span data-ttu-id="a090a-110">Pokud používáte konzolu pro správu balíčku v sadě Visual Studio, příkazy a argumenty, které jsou popsané v tomto tématu přítomen použít.</span><span class="sxs-lookup"><span data-stu-id="a090a-110">When using the Package Management Console in Visual Studio, the commands and arguments documented in this present topic apply.</span></span>

| <span data-ttu-id="a090a-111">Běžné příkazy</span><span class="sxs-lookup"><span data-stu-id="a090a-111">Common Commands</span></span> | <span data-ttu-id="a090a-112">Popis</span><span class="sxs-lookup"><span data-stu-id="a090a-112">Description</span></span> | <span data-ttu-id="a090a-113">Verze NuGet</span><span class="sxs-lookup"><span data-stu-id="a090a-113">NuGet Version</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="a090a-114">Install-Package</span><span class="sxs-lookup"><span data-stu-id="a090a-114">Install-Package</span></span>](ps-ref-install-package.md) | <span data-ttu-id="a090a-115">Nainstaluje do projektu balíček a jeho závislé součásti.</span><span class="sxs-lookup"><span data-stu-id="a090a-115">Installs a package and its dependencies into the project.</span></span> | <span data-ttu-id="a090a-116">Všechny</span><span class="sxs-lookup"><span data-stu-id="a090a-116">All</span></span> |
| [<span data-ttu-id="a090a-117">Update-Package</span><span class="sxs-lookup"><span data-stu-id="a090a-117">Update-Package</span></span>](ps-ref-update-package.md) | <span data-ttu-id="a090a-118">Aktualizuje balíček a jeho závislosti nebo všechny balíčky v projektu.</span><span class="sxs-lookup"><span data-stu-id="a090a-118">Updates a package and its dependencies, or all packages in a project.</span></span> | <span data-ttu-id="a090a-119">Všechny</span><span class="sxs-lookup"><span data-stu-id="a090a-119">All</span></span> |
| [<span data-ttu-id="a090a-120">Find-Package</span><span class="sxs-lookup"><span data-stu-id="a090a-120">Find-Package</span></span>](ps-ref-find-package.md) | <span data-ttu-id="a090a-121">Vyhledá zdroji balíčku pomocí ID balíčku nebo klíčová slova.</span><span class="sxs-lookup"><span data-stu-id="a090a-121">Searches a package source using a package ID or keywords.</span></span> | <span data-ttu-id="a090a-122">3.0+</span><span class="sxs-lookup"><span data-stu-id="a090a-122">3.0+</span></span> |
| [<span data-ttu-id="a090a-123">Get-Package</span><span class="sxs-lookup"><span data-stu-id="a090a-123">Get-Package</span></span>](ps-ref-get-package.md) | <span data-ttu-id="a090a-124">Načte seznam balíčků nainstalovaných v místním úložišti, nebo obsahuje seznam balíčků dostupných ze zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="a090a-124">Retrieves the list of packages installed in the local repository, or lists packages available from a package source.</span></span> | <span data-ttu-id="a090a-125">Všechny</span><span class="sxs-lookup"><span data-stu-id="a090a-125">All</span></span> |

| <span data-ttu-id="a090a-126">Sekundární příkazy</span><span class="sxs-lookup"><span data-stu-id="a090a-126">Secondary Commands</span></span> | <span data-ttu-id="a090a-127">Popis</span><span class="sxs-lookup"><span data-stu-id="a090a-127">Description</span></span> | <span data-ttu-id="a090a-128">Verze NuGet</span><span class="sxs-lookup"><span data-stu-id="a090a-128">NuGet Version</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="a090a-129">Add-BindingRedirect</span><span class="sxs-lookup"><span data-stu-id="a090a-129">Add-BindingRedirect</span></span>](ps-ref-add-bindingredirect.md) | <span data-ttu-id="a090a-130">Hledá ve všech sestaveních ve výstupní cestě pro projekt a přidá přesměrování vazby `app.config` nebo `web.config` potřeby.</span><span class="sxs-lookup"><span data-stu-id="a090a-130">Examines all assemblies within the output path for a project and adds binding redirects to the `app.config` or `web.config` where necessary.</span></span> | <span data-ttu-id="a090a-131">Všechny</span><span class="sxs-lookup"><span data-stu-id="a090a-131">All</span></span> |
| [<span data-ttu-id="a090a-132">Get-Project</span><span class="sxs-lookup"><span data-stu-id="a090a-132">Get-Project</span></span>](ps-ref-get-project.md) | <span data-ttu-id="a090a-133">Zobrazí informace o výchozí nebo zadaného projektu.</span><span class="sxs-lookup"><span data-stu-id="a090a-133">Displays information about the default or specified project.</span></span> | <span data-ttu-id="a090a-134">3.0+</span><span class="sxs-lookup"><span data-stu-id="a090a-134">3.0+</span></span> |
| [<span data-ttu-id="a090a-135">Open-PackagePage</span><span class="sxs-lookup"><span data-stu-id="a090a-135">Open-PackagePage</span></span>](ps-ref-open-packagepage.md) | <span data-ttu-id="a090a-136">Spuštění výchozího prohlížeče s projektu, licence nebo adresy URL sestav zneužití pro zadaný balíček.</span><span class="sxs-lookup"><span data-stu-id="a090a-136">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span> | <span data-ttu-id="a090a-137">Zastaralé v 3.0 +</span><span class="sxs-lookup"><span data-stu-id="a090a-137">Deprecated in 3.0+</span></span> |
| [<span data-ttu-id="a090a-138">Registrace TabExpansion</span><span class="sxs-lookup"><span data-stu-id="a090a-138">Register-TabExpansion</span></span>](ps-ref-register-tabexpansion.md) | <span data-ttu-id="a090a-139">Zaregistruje karta rozšíření pro parametry příkazu, umožňuje vytvářet vlastní rozšíření pro běžně používané parametr hodnoty.</span><span class="sxs-lookup"><span data-stu-id="a090a-139">Registers a tab expansion for the parameters of a command, allowing you to create customized expansions for commonly-used parameter values.</span></span> | <span data-ttu-id="a090a-140">Všechny</span><span class="sxs-lookup"><span data-stu-id="a090a-140">All</span></span> |
| [<span data-ttu-id="a090a-141">Sync-Package</span><span class="sxs-lookup"><span data-stu-id="a090a-141">Sync-Package</span></span>](ps-ref-sync-package.md) | <span data-ttu-id="a090a-142">Nainstalovaná verze balíčku z Get zadané projektu a synchronizuje ji s ostatními projekty v řešení.</span><span class="sxs-lookup"><span data-stu-id="a090a-142">Get the version of installed package from specified project and syncs the version to the rest of projects in the solution.</span></span> | <span data-ttu-id="a090a-143">3.0+</span><span class="sxs-lookup"><span data-stu-id="a090a-143">3.0+</span></span> |
| [<span data-ttu-id="a090a-144">Uninstall-Package</span><span class="sxs-lookup"><span data-stu-id="a090a-144">Uninstall-Package</span></span>](ps-ref-uninstall-package.md) | <span data-ttu-id="a090a-145">Odebere balíček z projektu, případně odebrání jeho závislé součásti.</span><span class="sxs-lookup"><span data-stu-id="a090a-145">Removes a package from a project, optionally removing its dependencies.</span></span> | <span data-ttu-id="a090a-146">Všechny</span><span class="sxs-lookup"><span data-stu-id="a090a-146">All</span></span> |

<span data-ttu-id="a090a-147">Pro dokončení, podrobné nápovědu k jakémukoli z těchto příkazů v rámci konzoly stačí spusťte následující s dotyčném název příkazu:</span><span class="sxs-lookup"><span data-stu-id="a090a-147">For complete, detailed help on any of these commands within the console, just run the following with the command name in question:</span></span>

```ps
Get-Help <command> -full
```

<span data-ttu-id="a090a-148">Všechny příkazy Konzola správce balíčků podporují následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216):</span><span class="sxs-lookup"><span data-stu-id="a090a-148">All Package Manager Console commands support the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216):</span></span>

- <span data-ttu-id="a090a-149">Ladit</span><span class="sxs-lookup"><span data-stu-id="a090a-149">Debug</span></span>
- <span data-ttu-id="a090a-150">ErrorAction</span><span class="sxs-lookup"><span data-stu-id="a090a-150">ErrorAction</span></span>
- <span data-ttu-id="a090a-151">ErrorVariable</span><span class="sxs-lookup"><span data-stu-id="a090a-151">ErrorVariable</span></span>
- <span data-ttu-id="a090a-152">OutBuffer</span><span class="sxs-lookup"><span data-stu-id="a090a-152">OutBuffer</span></span>
- <span data-ttu-id="a090a-153">OutVariable</span><span class="sxs-lookup"><span data-stu-id="a090a-153">OutVariable</span></span>
- <span data-ttu-id="a090a-154">PipelineVariable</span><span class="sxs-lookup"><span data-stu-id="a090a-154">PipelineVariable</span></span>
- <span data-ttu-id="a090a-155">Verbose</span><span class="sxs-lookup"><span data-stu-id="a090a-155">Verbose</span></span>
- <span data-ttu-id="a090a-156">WarningAction</span><span class="sxs-lookup"><span data-stu-id="a090a-156">WarningAction</span></span>
- <span data-ttu-id="a090a-157">WarningVariable</span><span class="sxs-lookup"><span data-stu-id="a090a-157">WarningVariable</span></span>

<span data-ttu-id="a090a-158">Podrobnosti najdete v části [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) v dokumentaci k prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a090a-158">For details, refer to [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) in the PowerShell documentation.</span></span>