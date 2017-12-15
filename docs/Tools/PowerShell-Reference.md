---
title: "Referenční informace prostředí PowerShell NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/2/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: cd08b869-44c6-480e-90f7-494a6d08e6d0
description: "Úplný odkaz na příkazy prostředí PowerShell, které jsou k dispozici v konzoli správce balíčků NuGet v sadě Visual Studio."
keywords: "NuGet konzoly Správce balíčků, příkazy prostředí NuGet Powershell, referenční informace prostředí NuGet Powershell"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c0da5c88447784fdd49d824bbd03b11f73c22ebc
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="powershell-reference"></a><span data-ttu-id="464e3-104">Referenční informace prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="464e3-104">PowerShell reference</span></span>

<span data-ttu-id="464e3-105">Konzola správce balíčků poskytuje rozhraní PowerShell v sadě Visual Studio v systému Windows pro interakci s NuGet prostřednictvím určité příkazy uvedené níže.</span><span class="sxs-lookup"><span data-stu-id="464e3-105">The Package Manager Console provides a PowerShell interface within Visual Studio on Windows to interact with NuGet through the specific commands listed below.</span></span> <span data-ttu-id="464e3-106">(Konzole není v současné době k dispozici v sadě Visual Studio for Mac.) Průvodce pomocí konzoly, najdete v článku [Konzola správce balíčků](../tools/package-manager-console.md) tématu.</span><span class="sxs-lookup"><span data-stu-id="464e3-106">(The console is not presently available in Visual Studio for Mac.) For a guide to using the console, see the [Package Manager Console](../tools/package-manager-console.md) topic.</span></span>

> [!Tip]
> <span data-ttu-id="464e3-107">Všechny příkazy prostředí PowerShell se týkají pouze spotřeba balíčku.</span><span class="sxs-lookup"><span data-stu-id="464e3-107">All PowerShell commands relate only to package consumption.</span></span> <span data-ttu-id="464e3-108">Žádné příkazy prostředí PowerShell se vztahují k vytváření a publikování balíčků s výjimkou, pokud balíček může být také příjemce další balíčky.</span><span class="sxs-lookup"><span data-stu-id="464e3-108">No PowerShell commands relate to creating and publishing packages except to the extent that a package can also be a consumer of other packages.</span></span>

> [!Important]
> <span data-ttu-id="464e3-109">Zde uvedené příkazy jsou specifické pro konzolu Správce balíčků v sadě Visual Studio a liší od [příkazy modulu správy balíčků](https://msdn.microsoft.com/powershell/reference/6/packagemanagement/packagemanagement) které jsou k dispozici v obecné prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="464e3-109">The commands listed here are specific to the Package Manager Console in Visual Studio, and differ from the [Package Management module commands](https://msdn.microsoft.com/powershell/reference/6/packagemanagement/packagemanagement) that are available in a general PowerShell environment.</span></span> <span data-ttu-id="464e3-110">Konkrétně každé prostředí má příkazy, které nejsou k dispozici v dalších a příkazy se stejným názvem, může se také liší v jejich konkrétní argumenty.</span><span class="sxs-lookup"><span data-stu-id="464e3-110">Specifically, each environment has commands that are not available in the other, and commands with the same name may also differ in their specific arguments.</span></span> <span data-ttu-id="464e3-111">Pokud používáte konzolu pro správu balíčku v sadě Visual Studio, příkazy a argumenty, které jsou popsané v tomto tématu přítomen použít.</span><span class="sxs-lookup"><span data-stu-id="464e3-111">When using the Package Management Console in Visual Studio, the commands and arguments documented in this present topic apply.</span></span>

| <span data-ttu-id="464e3-112">Běžné příkazy</span><span class="sxs-lookup"><span data-stu-id="464e3-112">Common Commands</span></span> | <span data-ttu-id="464e3-113">Popis</span><span class="sxs-lookup"><span data-stu-id="464e3-113">Description</span></span> | <span data-ttu-id="464e3-114">Verze NuGet</span><span class="sxs-lookup"><span data-stu-id="464e3-114">NuGet Version</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="464e3-115">Instalace balíčku</span><span class="sxs-lookup"><span data-stu-id="464e3-115">Install-Package</span></span>](ps-ref-install-package.md) | <span data-ttu-id="464e3-116">Nainstaluje do projektu balíček a jeho závislé součásti.</span><span class="sxs-lookup"><span data-stu-id="464e3-116">Installs a package and its dependencies into the project.</span></span> | <span data-ttu-id="464e3-117">Všechny</span><span class="sxs-lookup"><span data-stu-id="464e3-117">All</span></span> |
| [<span data-ttu-id="464e3-118">Balíček aktualizace</span><span class="sxs-lookup"><span data-stu-id="464e3-118">Update-Package</span></span>](ps-ref-update-package.md) | <span data-ttu-id="464e3-119">Aktualizuje balíček a jeho závislosti nebo všechny balíčky v projektu.</span><span class="sxs-lookup"><span data-stu-id="464e3-119">Updates a package and its dependencies, or all packages in a project.</span></span> | <span data-ttu-id="464e3-120">Všechny</span><span class="sxs-lookup"><span data-stu-id="464e3-120">All</span></span> |
| [<span data-ttu-id="464e3-121">Najít balíček</span><span class="sxs-lookup"><span data-stu-id="464e3-121">Find-Package</span></span>](ps-ref-find-package.md) | <span data-ttu-id="464e3-122">Vyhledá zdroji balíčku pomocí ID balíčku nebo klíčová slova.</span><span class="sxs-lookup"><span data-stu-id="464e3-122">Searches a package source using a package ID or keywords.</span></span> | <span data-ttu-id="464e3-123">3.0+</span><span class="sxs-lookup"><span data-stu-id="464e3-123">3.0+</span></span> |
| [<span data-ttu-id="464e3-124">Get-Package</span><span class="sxs-lookup"><span data-stu-id="464e3-124">Get-Package</span></span>](ps-ref-get-package.md) | <span data-ttu-id="464e3-125">Načte seznam balíčků nainstalovaných v místním úložišti, nebo obsahuje seznam balíčků dostupných ze zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="464e3-125">Retrieves the list of packages installed in the local repository, or lists packages available from a package source.</span></span> | <span data-ttu-id="464e3-126">Všechny</span><span class="sxs-lookup"><span data-stu-id="464e3-126">All</span></span> |

| <span data-ttu-id="464e3-127">Sekundární příkazy</span><span class="sxs-lookup"><span data-stu-id="464e3-127">Secondary Commands</span></span> | <span data-ttu-id="464e3-128">Popis</span><span class="sxs-lookup"><span data-stu-id="464e3-128">Description</span></span> | <span data-ttu-id="464e3-129">Verze NuGet</span><span class="sxs-lookup"><span data-stu-id="464e3-129">NuGet Version</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="464e3-130">Přidat bindingRedirect –</span><span class="sxs-lookup"><span data-stu-id="464e3-130">Add-BindingRedirect</span></span>](ps-ref-add-bindingredirect.md) | <span data-ttu-id="464e3-131">Hledá ve všech sestaveních ve výstupní cestě pro projekt a přidá přesměrování vazby `app.config` nebo `web.config` potřeby.</span><span class="sxs-lookup"><span data-stu-id="464e3-131">Examines all assemblies within the output path for a project and adds binding redirects to the `app.config` or `web.config` where necessary.</span></span> | <span data-ttu-id="464e3-132">Všechny</span><span class="sxs-lookup"><span data-stu-id="464e3-132">All</span></span> |
| [<span data-ttu-id="464e3-133">Get projektu</span><span class="sxs-lookup"><span data-stu-id="464e3-133">Get-Project</span></span>](ps-ref-get-project.md) | <span data-ttu-id="464e3-134">Zobrazí informace o výchozí nebo zadaného projektu.</span><span class="sxs-lookup"><span data-stu-id="464e3-134">Displays information about the default or specified project.</span></span> | <span data-ttu-id="464e3-135">3.0+</span><span class="sxs-lookup"><span data-stu-id="464e3-135">3.0+</span></span> |
| [<span data-ttu-id="464e3-136">Otevřete PackagePage</span><span class="sxs-lookup"><span data-stu-id="464e3-136">Open-PackagePage</span></span>](ps-ref-open-packagepage.md) | <span data-ttu-id="464e3-137">Spuštění výchozího prohlížeče s projektu, licence nebo adresy URL sestav zneužití pro zadaný balíček.</span><span class="sxs-lookup"><span data-stu-id="464e3-137">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span> | <span data-ttu-id="464e3-138">Zastaralé v 3.0 +</span><span class="sxs-lookup"><span data-stu-id="464e3-138">Deprecated in 3.0+</span></span> |
| [<span data-ttu-id="464e3-139">Registrace TabExpansion</span><span class="sxs-lookup"><span data-stu-id="464e3-139">Register-TabExpansion</span></span>](ps-ref-register-tabexpansion.md) | <span data-ttu-id="464e3-140">Zaregistruje karta rozšíření pro parametry příkazu, umožňuje vytvářet vlastní rozšíření pro běžně používané parametr hodnoty.</span><span class="sxs-lookup"><span data-stu-id="464e3-140">Registers a tab expansion for the parameters of a command, allowing you to create customized expansions for commonly-used parameter values.</span></span> | <span data-ttu-id="464e3-141">Všechny</span><span class="sxs-lookup"><span data-stu-id="464e3-141">All</span></span> |
| [<span data-ttu-id="464e3-142">Synchronizace balíčku</span><span class="sxs-lookup"><span data-stu-id="464e3-142">Sync-Package</span></span>](ps-ref-sync-package.md) | <span data-ttu-id="464e3-143">Nainstalovaná verze balíčku z Get zadané projektu a synchronizuje ji s ostatními projekty v řešení.</span><span class="sxs-lookup"><span data-stu-id="464e3-143">Get the version of installed package from specified project and syncs the version to the rest of projects in the solution.</span></span> | <span data-ttu-id="464e3-144">3.0+</span><span class="sxs-lookup"><span data-stu-id="464e3-144">3.0+</span></span> |
| [<span data-ttu-id="464e3-145">Odinstalace balíčku</span><span class="sxs-lookup"><span data-stu-id="464e3-145">Uninstall-Package</span></span>](ps-ref-uninstall-package.md) | <span data-ttu-id="464e3-146">Odebere balíček z projektu, případně odebrání jeho závislé součásti.</span><span class="sxs-lookup"><span data-stu-id="464e3-146">Removes a package from a project, optionally removing its dependencies.</span></span> | <span data-ttu-id="464e3-147">Všechny</span><span class="sxs-lookup"><span data-stu-id="464e3-147">All</span></span> |

<span data-ttu-id="464e3-148">Pro dokončení, podrobné nápovědu k jakémukoli z těchto příkazů v rámci konzoly stačí spusťte následující s dotyčném název příkazu:</span><span class="sxs-lookup"><span data-stu-id="464e3-148">For complete, detailed help on any of these commands within the console, just run the following with the command name in question:</span></span>

```ps
Get-Help <command> -full
```

<span data-ttu-id="464e3-149">Všechny příkazy Konzola správce balíčků podporují následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216):</span><span class="sxs-lookup"><span data-stu-id="464e3-149">All Package Manager Console commands support the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216):</span></span>

- <span data-ttu-id="464e3-150">Ladit</span><span class="sxs-lookup"><span data-stu-id="464e3-150">Debug</span></span>
- <span data-ttu-id="464e3-151">ErrorAction</span><span class="sxs-lookup"><span data-stu-id="464e3-151">ErrorAction</span></span>
- <span data-ttu-id="464e3-152">ErrorVariable</span><span class="sxs-lookup"><span data-stu-id="464e3-152">ErrorVariable</span></span>
- <span data-ttu-id="464e3-153">OutBuffer</span><span class="sxs-lookup"><span data-stu-id="464e3-153">OutBuffer</span></span>
- <span data-ttu-id="464e3-154">OutVariable</span><span class="sxs-lookup"><span data-stu-id="464e3-154">OutVariable</span></span>
- <span data-ttu-id="464e3-155">PipelineVariable</span><span class="sxs-lookup"><span data-stu-id="464e3-155">PipelineVariable</span></span>
- <span data-ttu-id="464e3-156">Verbose</span><span class="sxs-lookup"><span data-stu-id="464e3-156">Verbose</span></span>
- <span data-ttu-id="464e3-157">WarningAction</span><span class="sxs-lookup"><span data-stu-id="464e3-157">WarningAction</span></span>
- <span data-ttu-id="464e3-158">WarningVariable</span><span class="sxs-lookup"><span data-stu-id="464e3-158">WarningVariable</span></span>

<span data-ttu-id="464e3-159">Podrobnosti najdete v části [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) v dokumentaci k prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="464e3-159">For details, refer to [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) in the PowerShell documentation.</span></span>
