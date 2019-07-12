---
title: Referenční informace prostředí PowerShell odinstalujte NuGet-Package
description: Referenční informace pro příkaz Powershellu Uninstall-Package v konzole Správce balíčků NuGet v sadě Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: c95479103be2cba3b4eb6964ea761870477863bd
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842477"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="e4a7f-103">Uninstall-Package (konzola Správce balíčků v sadě Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="e4a7f-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="e4a7f-104">*Toto téma popisuje příkaz v rámci [Konzola správce balíčků](package-manager-console.md) v sadě Visual Studio ve Windows. Obecný příkaz Powershellu Uninstall-Package, najdete v článku [odkazu modulu Powershellu PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="e4a7f-104">*This topic describes the command within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="e4a7f-105">Odebere balíček z projektu, případně odebrání jeho závislostí.</span><span class="sxs-lookup"><span data-stu-id="e4a7f-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="e4a7f-106">Pokud na tento balíček jsou závislé jiné balíčky, příkaz se nezdaří, pokud – Force je zadána možnost.</span><span class="sxs-lookup"><span data-stu-id="e4a7f-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="e4a7f-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="e4a7f-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="e4a7f-108">Pokud na tento balíček jsou závislé jiné balíčky, příkaz se nezdaří, pokud – Force je zadána možnost.</span><span class="sxs-lookup"><span data-stu-id="e4a7f-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="e4a7f-109">Parametry</span><span class="sxs-lookup"><span data-stu-id="e4a7f-109">Parameters</span></span>

| <span data-ttu-id="e4a7f-110">Parametr</span><span class="sxs-lookup"><span data-stu-id="e4a7f-110">Parameter</span></span> | <span data-ttu-id="e4a7f-111">Popis</span><span class="sxs-lookup"><span data-stu-id="e4a7f-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e4a7f-112">Id</span><span class="sxs-lookup"><span data-stu-id="e4a7f-112">Id</span></span> | <span data-ttu-id="e4a7f-113">(Povinné) Identifikátor balíčku, který se odinstalovat.</span><span class="sxs-lookup"><span data-stu-id="e4a7f-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="e4a7f-114">-Id je volitelný přepínač samotný.</span><span class="sxs-lookup"><span data-stu-id="e4a7f-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="e4a7f-115">Version</span><span class="sxs-lookup"><span data-stu-id="e4a7f-115">Version</span></span> | <span data-ttu-id="e4a7f-116">Verze balíčku k odinstalaci, jako výchozí se použije aktuálně nainstalovanou verzi.</span><span class="sxs-lookup"><span data-stu-id="e4a7f-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="e4a7f-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="e4a7f-117">RemoveDependencies</span></span> | <span data-ttu-id="e4a7f-118">Odinstalujte balíček a jeho nepoužité závislé součásti.</span><span class="sxs-lookup"><span data-stu-id="e4a7f-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="e4a7f-119">To znamená pokud má závislost na něm závisí jiný balíček, se přeskočí.</span><span class="sxs-lookup"><span data-stu-id="e4a7f-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="e4a7f-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="e4a7f-120">ProjectName</span></span> | <span data-ttu-id="e4a7f-121">Projekt, ze kterého chcete odinstalovat balíček, jako výchozí se použije výchozí projekt.</span><span class="sxs-lookup"><span data-stu-id="e4a7f-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="e4a7f-122">Platnost</span><span class="sxs-lookup"><span data-stu-id="e4a7f-122">Force</span></span> | <span data-ttu-id="e4a7f-123">Vynutí balíčku tak, že se odinstalují, i v případě, že jsou na ní závislé jiné balíčky.</span><span class="sxs-lookup"><span data-stu-id="e4a7f-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="e4a7f-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="e4a7f-124">WhatIf</span></span> | <span data-ttu-id="e4a7f-125">Ukazuje, co by se stalo při spuštění příkazu bez ve skutečnosti provádí odinstalaci.</span><span class="sxs-lookup"><span data-stu-id="e4a7f-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="e4a7f-126">Žádná z těchto parametrů přijímat kanálu vstup nebo zástupné znaky.</span><span class="sxs-lookup"><span data-stu-id="e4a7f-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="e4a7f-127">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="e4a7f-127">Common Parameters</span></span>

<span data-ttu-id="e4a7f-128">`Uninstall-Package` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="e4a7f-128">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="e4a7f-129">Příklady</span><span class="sxs-lookup"><span data-stu-id="e4a7f-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
