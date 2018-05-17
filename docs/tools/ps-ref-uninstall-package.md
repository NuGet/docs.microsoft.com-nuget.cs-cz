---
title: Referenční informace prostředí PowerShell odinstalujte balíček NuGet
description: Referenční dokumentace pro příkaz prostředí PowerShell odinstalace balíčku v konzole Správce balíčků NuGet v sadě Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 5969526a12cb6e06f23f35a2481d0385bb9780ab
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="94e41-103">Uninstall-Package (konzola Správce balíčků v sadě Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="94e41-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="94e41-104">*Toto téma popisuje příkaz v rámci [Konzola správce balíčků NuGet](package-manager-console.md) v sadě Visual Studio v systému Windows. Příkaz Obecné odinstalace balíčků prostředí PowerShell najdete v článku [odkaz na prostředí PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="94e41-104">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="94e41-105">Odebere balíček z projektu, případně odebrání jeho závislé součásti.</span><span class="sxs-lookup"><span data-stu-id="94e41-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="94e41-106">Pokud jsou na tomto balíčku závislé jiné balíčky, příkaz se nezdaří, pokud není zadán parametr – Force.</span><span class="sxs-lookup"><span data-stu-id="94e41-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="94e41-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="94e41-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="94e41-108">Pokud jsou na tomto balíčku závislé jiné balíčky, příkaz se nezdaří, pokud není zadán parametr – Force.</span><span class="sxs-lookup"><span data-stu-id="94e41-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="94e41-109">Parametry</span><span class="sxs-lookup"><span data-stu-id="94e41-109">Parameters</span></span>

| <span data-ttu-id="94e41-110">Parametr</span><span class="sxs-lookup"><span data-stu-id="94e41-110">Parameter</span></span> | <span data-ttu-id="94e41-111">Popis</span><span class="sxs-lookup"><span data-stu-id="94e41-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="94e41-112">ID</span><span class="sxs-lookup"><span data-stu-id="94e41-112">Id</span></span> | <span data-ttu-id="94e41-113">(Povinné) Identifikátor balíček, který chcete odinstalovat.</span><span class="sxs-lookup"><span data-stu-id="94e41-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="94e41-114">-Id je volitelný přepínač sám sebe.</span><span class="sxs-lookup"><span data-stu-id="94e41-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="94e41-115">Version</span><span class="sxs-lookup"><span data-stu-id="94e41-115">Version</span></span> | <span data-ttu-id="94e41-116">Verze balíčku, které chcete odinstalovat, jako výchozí bude použit aktuálně nainstalované verze.</span><span class="sxs-lookup"><span data-stu-id="94e41-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="94e41-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="94e41-117">RemoveDependencies</span></span> | <span data-ttu-id="94e41-118">Odinstalujte balíček a jeho nepoužité závislé součásti.</span><span class="sxs-lookup"><span data-stu-id="94e41-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="94e41-119">To znamená pokud některé závislé na něm závisí jiný balíček, se přeskočí.</span><span class="sxs-lookup"><span data-stu-id="94e41-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="94e41-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="94e41-120">ProjectName</span></span> | <span data-ttu-id="94e41-121">Projekt, ze kterého pro odinstalaci balíčku, jako výchozí bude použit výchozí projekt.</span><span class="sxs-lookup"><span data-stu-id="94e41-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="94e41-122">Platnost</span><span class="sxs-lookup"><span data-stu-id="94e41-122">Force</span></span> | <span data-ttu-id="94e41-123">Balíček, který se má odinstalovat, vynutí i v případě, že jsou na ní závislé jiné balíčky.</span><span class="sxs-lookup"><span data-stu-id="94e41-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="94e41-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="94e41-124">WhatIf</span></span> | <span data-ttu-id="94e41-125">Zobrazuje, co by se stalo při spuštění příkazu bez ve skutečnosti provádí odinstalaci.</span><span class="sxs-lookup"><span data-stu-id="94e41-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="94e41-126">Žádná z těchto parametrů přijmout kanálu vstup nebo zástupné znaky.</span><span class="sxs-lookup"><span data-stu-id="94e41-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="94e41-127">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="94e41-127">Common Parameters</span></span>

<span data-ttu-id="94e41-128">`Uninstall-Package` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, podrobná, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="94e41-128">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="94e41-129">Příklady</span><span class="sxs-lookup"><span data-stu-id="94e41-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
