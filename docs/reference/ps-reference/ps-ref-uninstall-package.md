---
title: Reference k NuGet Uninstall-Package PowerShellu
description: Referenční informace k příkazu Uninstall-Package PowerShellu v konzole správce balíčků NuGet v aplikaci Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 371e95c341efbce1c4a15facefc15cd51b266141
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901782"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="34902-103">Uninstall-Package (konzola správce balíčků v aplikaci Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="34902-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="34902-104">*Toto téma popisuje příkaz v [konzole správce balíčků](../../consume-packages/install-use-packages-powershell.md) v sadě Visual Studio ve Windows. Obecný příkaz Uninstall-Package PowerShellu najdete v [referenčních informacích k PowerShellu PackageManagement](/powershell/module/packagemanagement).*</span><span class="sxs-lookup"><span data-stu-id="34902-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement).*</span></span>

<span data-ttu-id="34902-105">Odebere balíček z projektu, volitelně odebere jeho závislosti.</span><span class="sxs-lookup"><span data-stu-id="34902-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="34902-106">Pokud jsou na tomto balíčku závislé jiné balíčky, příkaz se nezdaří, pokud není zadána možnost – Force.</span><span class="sxs-lookup"><span data-stu-id="34902-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="34902-107">Syntax</span><span class="sxs-lookup"><span data-stu-id="34902-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="34902-108">Pokud jsou na tomto balíčku závislé jiné balíčky, příkaz se nezdaří, pokud není zadána možnost – Force.</span><span class="sxs-lookup"><span data-stu-id="34902-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="34902-109">Parametry</span><span class="sxs-lookup"><span data-stu-id="34902-109">Parameters</span></span>

| <span data-ttu-id="34902-110">Parametr</span><span class="sxs-lookup"><span data-stu-id="34902-110">Parameter</span></span> | <span data-ttu-id="34902-111">Popis</span><span class="sxs-lookup"><span data-stu-id="34902-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="34902-112">Id</span><span class="sxs-lookup"><span data-stu-id="34902-112">Id</span></span> | <span data-ttu-id="34902-113">Požadovanou Identifikátor balíčku, který se má odinstalovat</span><span class="sxs-lookup"><span data-stu-id="34902-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="34902-114">Samotný přepínač-ID je nepovinný.</span><span class="sxs-lookup"><span data-stu-id="34902-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="34902-115">Verze</span><span class="sxs-lookup"><span data-stu-id="34902-115">Version</span></span> | <span data-ttu-id="34902-116">Verze balíčku, který se má odinstalovat, se zastaví jako aktuálně nainstalovaná verze.</span><span class="sxs-lookup"><span data-stu-id="34902-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="34902-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="34902-117">RemoveDependencies</span></span> | <span data-ttu-id="34902-118">Odinstalujte balíček a jeho nepoužívané závislosti.</span><span class="sxs-lookup"><span data-stu-id="34902-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="34902-119">To znamená, že pokud má nějaká závislost jiný balíček, který na něm závisí, přeskočí se.</span><span class="sxs-lookup"><span data-stu-id="34902-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="34902-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="34902-120">ProjectName</span></span> | <span data-ttu-id="34902-121">Projekt, ze kterého má být balíček odinstalován, výchozí nastavení projektu.</span><span class="sxs-lookup"><span data-stu-id="34902-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="34902-122">Force</span><span class="sxs-lookup"><span data-stu-id="34902-122">Force</span></span> | <span data-ttu-id="34902-123">Vynutí odinstalaci balíčku, a to i v případě, že na něm závisí jiné balíčky.</span><span class="sxs-lookup"><span data-stu-id="34902-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="34902-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="34902-124">WhatIf</span></span> | <span data-ttu-id="34902-125">Ukazuje, co se stane při spuštění příkazu, aniž by se skutečně prováděla odinstalace.</span><span class="sxs-lookup"><span data-stu-id="34902-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="34902-126">Žádný z těchto parametrů nepřijímají vstupní ani zástupné znaky kanálu.</span><span class="sxs-lookup"><span data-stu-id="34902-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="34902-127">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="34902-127">Common Parameters</span></span>

<span data-ttu-id="34902-128">`Uninstall-Package` podporuje následující [běžné parametry PowerShellu](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, inbuffer, subvariable, PipelineVariable, verbose, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="34902-128">`Uninstall-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="34902-129">Příklady</span><span class="sxs-lookup"><span data-stu-id="34902-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```