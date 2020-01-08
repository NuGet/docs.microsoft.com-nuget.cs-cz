---
title: Referenční dokumentace prostředí PowerShell pro odinstalaci NuGet
description: Reference k příkazu Uninstall-Package PowerShell v konzole správce balíčků NuGet v aplikaci Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 05b7bf0e8abad0904b9e851ea6b7a5317e74229d
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384412"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="c1bbc-103">Uninstall-Package (konzola Správce balíčků v sadě Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="c1bbc-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="c1bbc-104">*Toto téma popisuje příkaz v [konzole správce balíčků](../../consume-packages/install-use-packages-powershell.md) v sadě Visual Studio ve Windows. Obecný příkaz pro odinstalaci do PowerShellu najdete v tématu [referenční informace k PowerShellu pro PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="c1bbc-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="c1bbc-105">Odebere balíček z projektu, volitelně odebere jeho závislosti.</span><span class="sxs-lookup"><span data-stu-id="c1bbc-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="c1bbc-106">Pokud jsou na tomto balíčku závislé jiné balíčky a není zadán parametr –Force, příkaz se nezdaří.</span><span class="sxs-lookup"><span data-stu-id="c1bbc-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="c1bbc-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="c1bbc-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="c1bbc-108">Pokud jsou na tomto balíčku závislé jiné balíčky a není zadán parametr –Force, příkaz se nezdaří.</span><span class="sxs-lookup"><span data-stu-id="c1bbc-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="c1bbc-109">Parametry</span><span class="sxs-lookup"><span data-stu-id="c1bbc-109">Parameters</span></span>

| <span data-ttu-id="c1bbc-110">Parametr</span><span class="sxs-lookup"><span data-stu-id="c1bbc-110">Parameter</span></span> | <span data-ttu-id="c1bbc-111">Popis</span><span class="sxs-lookup"><span data-stu-id="c1bbc-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c1bbc-112">Id</span><span class="sxs-lookup"><span data-stu-id="c1bbc-112">Id</span></span> | <span data-ttu-id="c1bbc-113">Požadovanou Identifikátor balíčku, který se má odinstalovat</span><span class="sxs-lookup"><span data-stu-id="c1bbc-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="c1bbc-114">Samotný přepínač-ID je nepovinný.</span><span class="sxs-lookup"><span data-stu-id="c1bbc-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="c1bbc-115">Version</span><span class="sxs-lookup"><span data-stu-id="c1bbc-115">Version</span></span> | <span data-ttu-id="c1bbc-116">Verze balíčku, který se má odinstalovat, se zastaví jako aktuálně nainstalovaná verze.</span><span class="sxs-lookup"><span data-stu-id="c1bbc-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="c1bbc-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="c1bbc-117">RemoveDependencies</span></span> | <span data-ttu-id="c1bbc-118">Odinstalujte balíček a jeho nepoužívané závislosti.</span><span class="sxs-lookup"><span data-stu-id="c1bbc-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="c1bbc-119">To znamená, že pokud má nějaká závislost jiný balíček, který na něm závisí, přeskočí se.</span><span class="sxs-lookup"><span data-stu-id="c1bbc-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="c1bbc-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="c1bbc-120">ProjectName</span></span> | <span data-ttu-id="c1bbc-121">Projekt, ze kterého má být balíček odinstalován, výchozí nastavení projektu.</span><span class="sxs-lookup"><span data-stu-id="c1bbc-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="c1bbc-122">Force</span><span class="sxs-lookup"><span data-stu-id="c1bbc-122">Force</span></span> | <span data-ttu-id="c1bbc-123">Vynutí odinstalaci balíčku, a to i v případě, že na něm závisí jiné balíčky.</span><span class="sxs-lookup"><span data-stu-id="c1bbc-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="c1bbc-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="c1bbc-124">WhatIf</span></span> | <span data-ttu-id="c1bbc-125">Ukazuje, co se stane při spuštění příkazu, aniž by se skutečně prováděla odinstalace.</span><span class="sxs-lookup"><span data-stu-id="c1bbc-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="c1bbc-126">Žádný z těchto parametrů nepřijímají vstupní ani zástupné znaky kanálu.</span><span class="sxs-lookup"><span data-stu-id="c1bbc-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="c1bbc-127">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="c1bbc-127">Common Parameters</span></span>

<span data-ttu-id="c1bbc-128">`Uninstall-Package` podporuje následující [běžné parametry PowerShellu](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, inbuffer, subvariable, PipelineVariable, verbose, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="c1bbc-128">`Uninstall-Package` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="c1bbc-129">Příklady</span><span class="sxs-lookup"><span data-stu-id="c1bbc-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
