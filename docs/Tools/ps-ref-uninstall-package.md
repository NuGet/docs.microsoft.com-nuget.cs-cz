---
title: Referenční informace prostředí PowerShell odinstalujte balíček NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 06/01/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referenční dokumentace pro příkaz prostředí PowerShell odinstalace balíčku v konzole Správce balíčků NuGet v sadě Visual Studio.
keywords: NuGet konzoly Správce balíčků, příkazy prostředí NuGet Powershell, NuGet Powershell odkaz, odinstalační balíček
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: b53a36a6456522aa0d9d0d7cdf412de464ba9e08
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="b352b-104">Odinstalujte Package (konzola Správce balíčků v sadě Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="b352b-104">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="b352b-105">*Toto téma popisuje příkaz v rámci [Konzola správce balíčků NuGet](package-manager-console.md) v sadě Visual Studio v systému Windows. Příkaz Obecné odinstalace balíčků prostředí PowerShell najdete v článku [odkaz na prostředí PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="b352b-105">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="b352b-106">Odebere balíček z projektu, případně odebrání jeho závislé součásti.</span><span class="sxs-lookup"><span data-stu-id="b352b-106">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="b352b-107">Pokud jsou na tomto balíčku závislé jiné balíčky, příkaz se nezdaří, pokud není zadán parametr – Force.</span><span class="sxs-lookup"><span data-stu-id="b352b-107">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="b352b-108">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="b352b-108">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="b352b-109">Pokud jsou na tomto balíčku závislé jiné balíčky, příkaz se nezdaří, pokud není zadán parametr – Force.</span><span class="sxs-lookup"><span data-stu-id="b352b-109">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="b352b-110">Parametry</span><span class="sxs-lookup"><span data-stu-id="b352b-110">Parameters</span></span>

| <span data-ttu-id="b352b-111">Parametr</span><span class="sxs-lookup"><span data-stu-id="b352b-111">Parameter</span></span> | <span data-ttu-id="b352b-112">Popis</span><span class="sxs-lookup"><span data-stu-id="b352b-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b352b-113">ID</span><span class="sxs-lookup"><span data-stu-id="b352b-113">Id</span></span> | <span data-ttu-id="b352b-114">(Povinné) Identifikátor balíček, který chcete odinstalovat.</span><span class="sxs-lookup"><span data-stu-id="b352b-114">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="b352b-115">-Id je volitelný přepínač sám sebe.</span><span class="sxs-lookup"><span data-stu-id="b352b-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="b352b-116">Version</span><span class="sxs-lookup"><span data-stu-id="b352b-116">Version</span></span> | <span data-ttu-id="b352b-117">Verze balíčku, které chcete odinstalovat, jako výchozí bude použit aktuálně nainstalované verze.</span><span class="sxs-lookup"><span data-stu-id="b352b-117">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="b352b-118">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="b352b-118">RemoveDependencies</span></span> | <span data-ttu-id="b352b-119">Odinstalujte balíček a jeho nepoužité závislé součásti.</span><span class="sxs-lookup"><span data-stu-id="b352b-119">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="b352b-120">To znamená pokud některé závislé na něm závisí jiný balíček, se přeskočí.</span><span class="sxs-lookup"><span data-stu-id="b352b-120">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="b352b-121">ProjectName</span><span class="sxs-lookup"><span data-stu-id="b352b-121">ProjectName</span></span> | <span data-ttu-id="b352b-122">Projekt, ze kterého pro odinstalaci balíčku, jako výchozí bude použit výchozí projekt.</span><span class="sxs-lookup"><span data-stu-id="b352b-122">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="b352b-123">Platnost</span><span class="sxs-lookup"><span data-stu-id="b352b-123">Force</span></span> | <span data-ttu-id="b352b-124">Balíček, který se má odinstalovat, vynutí i v případě, že jsou na ní závislé jiné balíčky.</span><span class="sxs-lookup"><span data-stu-id="b352b-124">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="b352b-125">WhatIf</span><span class="sxs-lookup"><span data-stu-id="b352b-125">WhatIf</span></span> | <span data-ttu-id="b352b-126">Zobrazuje, co by se stalo při spuštění příkazu bez ve skutečnosti provádí odinstalaci.</span><span class="sxs-lookup"><span data-stu-id="b352b-126">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="b352b-127">Žádná z těchto parametrů přijmout kanálu vstup nebo zástupné znaky.</span><span class="sxs-lookup"><span data-stu-id="b352b-127">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="b352b-128">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="b352b-128">Common Parameters</span></span>

<span data-ttu-id="b352b-129">`Uninstall-Package` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, podrobná, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="b352b-129">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="b352b-130">Příklady</span><span class="sxs-lookup"><span data-stu-id="b352b-130">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
