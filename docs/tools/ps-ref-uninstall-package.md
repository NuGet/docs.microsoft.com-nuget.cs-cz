---
title: Referenční informace prostředí PowerShell odinstalujte balíček NuGet
description: Referenční dokumentace pro příkaz prostředí PowerShell odinstalace balíčku v konzole Správce balíčků NuGet v sadě Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 860a58c359c9b723564a70f83aee4eee5cebf16d
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818864"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="5eff3-103">Uninstall-Package (konzola Správce balíčků v sadě Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="5eff3-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="5eff3-104">*Toto téma popisuje příkaz v rámci [Konzola správce balíčků NuGet](package-manager-console.md) v sadě Visual Studio v systému Windows. Příkaz Obecné odinstalace balíčků prostředí PowerShell najdete v článku [odkaz na prostředí PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="5eff3-104">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="5eff3-105">Odebere balíček z projektu, případně odebrání jeho závislé součásti.</span><span class="sxs-lookup"><span data-stu-id="5eff3-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="5eff3-106">Pokud jsou na tomto balíčku závislé jiné balíčky, příkaz se nezdaří, pokud není zadán parametr – Force.</span><span class="sxs-lookup"><span data-stu-id="5eff3-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="5eff3-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="5eff3-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="5eff3-108">Pokud jsou na tomto balíčku závislé jiné balíčky, příkaz se nezdaří, pokud není zadán parametr – Force.</span><span class="sxs-lookup"><span data-stu-id="5eff3-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="5eff3-109">Parametry</span><span class="sxs-lookup"><span data-stu-id="5eff3-109">Parameters</span></span>

| <span data-ttu-id="5eff3-110">Parametr</span><span class="sxs-lookup"><span data-stu-id="5eff3-110">Parameter</span></span> | <span data-ttu-id="5eff3-111">Popis</span><span class="sxs-lookup"><span data-stu-id="5eff3-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5eff3-112">ID</span><span class="sxs-lookup"><span data-stu-id="5eff3-112">Id</span></span> | <span data-ttu-id="5eff3-113">(Povinné) Identifikátor balíček, který chcete odinstalovat.</span><span class="sxs-lookup"><span data-stu-id="5eff3-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="5eff3-114">-Id je volitelný přepínač sám sebe.</span><span class="sxs-lookup"><span data-stu-id="5eff3-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="5eff3-115">Version</span><span class="sxs-lookup"><span data-stu-id="5eff3-115">Version</span></span> | <span data-ttu-id="5eff3-116">Verze balíčku, které chcete odinstalovat, jako výchozí bude použit aktuálně nainstalované verze.</span><span class="sxs-lookup"><span data-stu-id="5eff3-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="5eff3-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="5eff3-117">RemoveDependencies</span></span> | <span data-ttu-id="5eff3-118">Odinstalujte balíček a jeho nepoužité závislé součásti.</span><span class="sxs-lookup"><span data-stu-id="5eff3-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="5eff3-119">To znamená pokud některé závislé na něm závisí jiný balíček, se přeskočí.</span><span class="sxs-lookup"><span data-stu-id="5eff3-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="5eff3-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="5eff3-120">ProjectName</span></span> | <span data-ttu-id="5eff3-121">Projekt, ze kterého pro odinstalaci balíčku, jako výchozí bude použit výchozí projekt.</span><span class="sxs-lookup"><span data-stu-id="5eff3-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="5eff3-122">Platnost</span><span class="sxs-lookup"><span data-stu-id="5eff3-122">Force</span></span> | <span data-ttu-id="5eff3-123">Balíček, který se má odinstalovat, vynutí i v případě, že jsou na ní závislé jiné balíčky.</span><span class="sxs-lookup"><span data-stu-id="5eff3-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="5eff3-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="5eff3-124">WhatIf</span></span> | <span data-ttu-id="5eff3-125">Zobrazuje, co by se stalo při spuštění příkazu bez ve skutečnosti provádí odinstalaci.</span><span class="sxs-lookup"><span data-stu-id="5eff3-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="5eff3-126">Žádná z těchto parametrů přijmout kanálu vstup nebo zástupné znaky.</span><span class="sxs-lookup"><span data-stu-id="5eff3-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="5eff3-127">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="5eff3-127">Common Parameters</span></span>

<span data-ttu-id="5eff3-128">`Uninstall-Package` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, podrobná, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="5eff3-128">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="5eff3-129">Příklady</span><span class="sxs-lookup"><span data-stu-id="5eff3-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
