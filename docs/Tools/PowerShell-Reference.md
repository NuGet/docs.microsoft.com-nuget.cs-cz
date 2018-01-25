---
title: "Referenční informace prostředí PowerShell NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/02/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Úplný odkaz na příkazy prostředí PowerShell, které jsou k dispozici v konzoli správce balíčků NuGet v sadě Visual Studio."
keywords: "NuGet konzoly Správce balíčků, příkazy prostředí NuGet Powershell, referenční informace prostředí NuGet Powershell"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0cbd9b13b34bd93fea6c6684c03bca9cff5d9e5e
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
---
# <a name="powershell-reference"></a><span data-ttu-id="49b14-104">Referenční informace prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="49b14-104">PowerShell reference</span></span>

<span data-ttu-id="49b14-105">Konzola správce balíčků poskytuje rozhraní PowerShell v sadě Visual Studio v systému Windows pro interakci s NuGet prostřednictvím určité příkazy uvedené níže.</span><span class="sxs-lookup"><span data-stu-id="49b14-105">The Package Manager Console provides a PowerShell interface within Visual Studio on Windows to interact with NuGet through the specific commands listed below.</span></span> <span data-ttu-id="49b14-106">(Konzole není v současné době k dispozici v sadě Visual Studio for Mac.) Průvodce pomocí konzoly, najdete v článku [Konzola správce balíčků](../tools/package-manager-console.md) tématu.</span><span class="sxs-lookup"><span data-stu-id="49b14-106">(The console is not presently available in Visual Studio for Mac.) For a guide to using the console, see the [Package Manager Console](../tools/package-manager-console.md) topic.</span></span>

> [!Tip]
> <span data-ttu-id="49b14-107">Všechny příkazy prostředí PowerShell se týkají pouze spotřeba balíčku.</span><span class="sxs-lookup"><span data-stu-id="49b14-107">All PowerShell commands relate only to package consumption.</span></span> <span data-ttu-id="49b14-108">Žádné příkazy prostředí PowerShell se vztahují k vytváření a publikování balíčků s výjimkou, pokud balíček může být také příjemce další balíčky.</span><span class="sxs-lookup"><span data-stu-id="49b14-108">No PowerShell commands relate to creating and publishing packages except to the extent that a package can also be a consumer of other packages.</span></span>

> [!Important]
> <span data-ttu-id="49b14-109">Zde uvedené příkazy jsou specifické pro konzolu Správce balíčků v sadě Visual Studio a liší od [příkazy modulu správy balíčků](/powershell/module/packagemanagement/?view=powershell-6) které jsou k dispozici v obecné prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="49b14-109">The commands listed here are specific to the Package Manager Console in Visual Studio, and differ from the [Package Management module commands](/powershell/module/packagemanagement/?view=powershell-6) that are available in a general PowerShell environment.</span></span> <span data-ttu-id="49b14-110">Konkrétně každé prostředí má příkazy, které nejsou k dispozici v dalších a příkazy se stejným názvem, může se také liší v jejich konkrétní argumenty.</span><span class="sxs-lookup"><span data-stu-id="49b14-110">Specifically, each environment has commands that are not available in the other, and commands with the same name may also differ in their specific arguments.</span></span> <span data-ttu-id="49b14-111">Pokud používáte konzolu pro správu balíčku v sadě Visual Studio, příkazy a argumenty, které jsou popsané v tomto tématu přítomen použít.</span><span class="sxs-lookup"><span data-stu-id="49b14-111">When using the Package Management Console in Visual Studio, the commands and arguments documented in this present topic apply.</span></span>

| <span data-ttu-id="49b14-112">Běžné příkazy</span><span class="sxs-lookup"><span data-stu-id="49b14-112">Common Commands</span></span> | <span data-ttu-id="49b14-113">Popis</span><span class="sxs-lookup"><span data-stu-id="49b14-113">Description</span></span> | <span data-ttu-id="49b14-114">Verze NuGet</span><span class="sxs-lookup"><span data-stu-id="49b14-114">NuGet Version</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="49b14-115">Install-Package</span><span class="sxs-lookup"><span data-stu-id="49b14-115">Install-Package</span></span>](ps-ref-install-package.md) | <span data-ttu-id="49b14-116">Nainstaluje do projektu balíček a jeho závislé součásti.</span><span class="sxs-lookup"><span data-stu-id="49b14-116">Installs a package and its dependencies into the project.</span></span> | <span data-ttu-id="49b14-117">Všechny</span><span class="sxs-lookup"><span data-stu-id="49b14-117">All</span></span> |
| [<span data-ttu-id="49b14-118">Update-Package</span><span class="sxs-lookup"><span data-stu-id="49b14-118">Update-Package</span></span>](ps-ref-update-package.md) | <span data-ttu-id="49b14-119">Aktualizuje balíček a jeho závislosti nebo všechny balíčky v projektu.</span><span class="sxs-lookup"><span data-stu-id="49b14-119">Updates a package and its dependencies, or all packages in a project.</span></span> | <span data-ttu-id="49b14-120">Všechny</span><span class="sxs-lookup"><span data-stu-id="49b14-120">All</span></span> |
| [<span data-ttu-id="49b14-121">Find-Package</span><span class="sxs-lookup"><span data-stu-id="49b14-121">Find-Package</span></span>](ps-ref-find-package.md) | <span data-ttu-id="49b14-122">Vyhledá zdroji balíčku pomocí ID balíčku nebo klíčová slova.</span><span class="sxs-lookup"><span data-stu-id="49b14-122">Searches a package source using a package ID or keywords.</span></span> | <span data-ttu-id="49b14-123">3.0+</span><span class="sxs-lookup"><span data-stu-id="49b14-123">3.0+</span></span> |
| [<span data-ttu-id="49b14-124">Get-Package</span><span class="sxs-lookup"><span data-stu-id="49b14-124">Get-Package</span></span>](ps-ref-get-package.md) | <span data-ttu-id="49b14-125">Načte seznam balíčků nainstalovaných v místním úložišti, nebo obsahuje seznam balíčků dostupných ze zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="49b14-125">Retrieves the list of packages installed in the local repository, or lists packages available from a package source.</span></span> | <span data-ttu-id="49b14-126">Všechny</span><span class="sxs-lookup"><span data-stu-id="49b14-126">All</span></span> |

| <span data-ttu-id="49b14-127">Sekundární příkazy</span><span class="sxs-lookup"><span data-stu-id="49b14-127">Secondary Commands</span></span> | <span data-ttu-id="49b14-128">Popis</span><span class="sxs-lookup"><span data-stu-id="49b14-128">Description</span></span> | <span data-ttu-id="49b14-129">Verze NuGet</span><span class="sxs-lookup"><span data-stu-id="49b14-129">NuGet Version</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="49b14-130">Add-BindingRedirect</span><span class="sxs-lookup"><span data-stu-id="49b14-130">Add-BindingRedirect</span></span>](ps-ref-add-bindingredirect.md) | <span data-ttu-id="49b14-131">Hledá ve všech sestaveních ve výstupní cestě pro projekt a přidá přesměrování vazby `app.config` nebo `web.config` potřeby.</span><span class="sxs-lookup"><span data-stu-id="49b14-131">Examines all assemblies within the output path for a project and adds binding redirects to the `app.config` or `web.config` where necessary.</span></span> | <span data-ttu-id="49b14-132">Všechny</span><span class="sxs-lookup"><span data-stu-id="49b14-132">All</span></span> |
| [<span data-ttu-id="49b14-133">Get-Project</span><span class="sxs-lookup"><span data-stu-id="49b14-133">Get-Project</span></span>](ps-ref-get-project.md) | <span data-ttu-id="49b14-134">Zobrazí informace o výchozí nebo zadaného projektu.</span><span class="sxs-lookup"><span data-stu-id="49b14-134">Displays information about the default or specified project.</span></span> | <span data-ttu-id="49b14-135">3.0+</span><span class="sxs-lookup"><span data-stu-id="49b14-135">3.0+</span></span> |
| [<span data-ttu-id="49b14-136">Open-PackagePage</span><span class="sxs-lookup"><span data-stu-id="49b14-136">Open-PackagePage</span></span>](ps-ref-open-packagepage.md) | <span data-ttu-id="49b14-137">Spuštění výchozího prohlížeče s projektu, licence nebo adresy URL sestav zneužití pro zadaný balíček.</span><span class="sxs-lookup"><span data-stu-id="49b14-137">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span> | <span data-ttu-id="49b14-138">Zastaralé v 3.0 +</span><span class="sxs-lookup"><span data-stu-id="49b14-138">Deprecated in 3.0+</span></span> |
| [<span data-ttu-id="49b14-139">Register-TabExpansion</span><span class="sxs-lookup"><span data-stu-id="49b14-139">Register-TabExpansion</span></span>](ps-ref-register-tabexpansion.md) | <span data-ttu-id="49b14-140">Zaregistruje karta rozšíření pro parametry příkazu, umožňuje vytvářet vlastní rozšíření pro běžně používané parametr hodnoty.</span><span class="sxs-lookup"><span data-stu-id="49b14-140">Registers a tab expansion for the parameters of a command, allowing you to create customized expansions for commonly-used parameter values.</span></span> | <span data-ttu-id="49b14-141">Všechny</span><span class="sxs-lookup"><span data-stu-id="49b14-141">All</span></span> |
| [<span data-ttu-id="49b14-142">Sync-Package</span><span class="sxs-lookup"><span data-stu-id="49b14-142">Sync-Package</span></span>](ps-ref-sync-package.md) | <span data-ttu-id="49b14-143">Nainstalovaná verze balíčku z Get zadané projektu a synchronizuje ji s ostatními projekty v řešení.</span><span class="sxs-lookup"><span data-stu-id="49b14-143">Get the version of installed package from specified project and syncs the version to the rest of projects in the solution.</span></span> | <span data-ttu-id="49b14-144">3.0+</span><span class="sxs-lookup"><span data-stu-id="49b14-144">3.0+</span></span> |
| [<span data-ttu-id="49b14-145">Uninstall-Package</span><span class="sxs-lookup"><span data-stu-id="49b14-145">Uninstall-Package</span></span>](ps-ref-uninstall-package.md) | <span data-ttu-id="49b14-146">Odebere balíček z projektu, případně odebrání jeho závislé součásti.</span><span class="sxs-lookup"><span data-stu-id="49b14-146">Removes a package from a project, optionally removing its dependencies.</span></span> | <span data-ttu-id="49b14-147">Všechny</span><span class="sxs-lookup"><span data-stu-id="49b14-147">All</span></span> |

<span data-ttu-id="49b14-148">Pro dokončení, podrobné nápovědu k jakémukoli z těchto příkazů v rámci konzoly stačí spusťte následující s dotyčném název příkazu:</span><span class="sxs-lookup"><span data-stu-id="49b14-148">For complete, detailed help on any of these commands within the console, just run the following with the command name in question:</span></span>

```ps
Get-Help <command> -full
```

<span data-ttu-id="49b14-149">Všechny příkazy Konzola správce balíčků podporují následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216):</span><span class="sxs-lookup"><span data-stu-id="49b14-149">All Package Manager Console commands support the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216):</span></span>

- <span data-ttu-id="49b14-150">Ladit</span><span class="sxs-lookup"><span data-stu-id="49b14-150">Debug</span></span>
- <span data-ttu-id="49b14-151">ErrorAction</span><span class="sxs-lookup"><span data-stu-id="49b14-151">ErrorAction</span></span>
- <span data-ttu-id="49b14-152">ErrorVariable</span><span class="sxs-lookup"><span data-stu-id="49b14-152">ErrorVariable</span></span>
- <span data-ttu-id="49b14-153">OutBuffer</span><span class="sxs-lookup"><span data-stu-id="49b14-153">OutBuffer</span></span>
- <span data-ttu-id="49b14-154">OutVariable</span><span class="sxs-lookup"><span data-stu-id="49b14-154">OutVariable</span></span>
- <span data-ttu-id="49b14-155">PipelineVariable</span><span class="sxs-lookup"><span data-stu-id="49b14-155">PipelineVariable</span></span>
- <span data-ttu-id="49b14-156">Verbose</span><span class="sxs-lookup"><span data-stu-id="49b14-156">Verbose</span></span>
- <span data-ttu-id="49b14-157">WarningAction</span><span class="sxs-lookup"><span data-stu-id="49b14-157">WarningAction</span></span>
- <span data-ttu-id="49b14-158">WarningVariable</span><span class="sxs-lookup"><span data-stu-id="49b14-158">WarningVariable</span></span>

<span data-ttu-id="49b14-159">Podrobnosti najdete v části [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) v dokumentaci k prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="49b14-159">For details, refer to [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) in the PowerShell documentation.</span></span>
