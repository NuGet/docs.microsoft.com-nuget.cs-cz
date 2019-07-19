---
title: Referenční dokumentace prostředí NuGet Open-PackagePage
description: Reference pro příkaz Open-PackagePage PowerShell v konzole správce balíčků NuGet v aplikaci Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 0237c23d81000a1d58264cc0ab48c73d819d0e5a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328216"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="4e1bc-103">Open-PackagePage (konzola Správce balíčků v sadě Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="4e1bc-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="4e1bc-104">*Zastaralé v 3.0 +; k dispozici pouze v rámci [konzoly Správce balíčků](../../consume-packages/install-use-packages-powershell.md) v sadě Visual Studio ve Windows.*</span><span class="sxs-lookup"><span data-stu-id="4e1bc-104">*Deprecated in 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="4e1bc-105">Spustí výchozí prohlížeč s adresou URL projektu, licence nebo sestavy pro zneužití zadaného balíčku.</span><span class="sxs-lookup"><span data-stu-id="4e1bc-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="4e1bc-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="4e1bc-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="4e1bc-107">Parametry</span><span class="sxs-lookup"><span data-stu-id="4e1bc-107">Parameters</span></span>

| <span data-ttu-id="4e1bc-108">Parametr</span><span class="sxs-lookup"><span data-stu-id="4e1bc-108">Parameter</span></span> | <span data-ttu-id="4e1bc-109">Popis</span><span class="sxs-lookup"><span data-stu-id="4e1bc-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4e1bc-110">Id</span><span class="sxs-lookup"><span data-stu-id="4e1bc-110">Id</span></span> | <span data-ttu-id="4e1bc-111">ID balíčku požadovaného balíčku.</span><span class="sxs-lookup"><span data-stu-id="4e1bc-111">The package ID of the desired package.</span></span> <span data-ttu-id="4e1bc-112">Samotný přepínač-ID je nepovinný.</span><span class="sxs-lookup"><span data-stu-id="4e1bc-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="4e1bc-113">Version</span><span class="sxs-lookup"><span data-stu-id="4e1bc-113">Version</span></span> | <span data-ttu-id="4e1bc-114">Verze balíčku, výchozí nastavení na nejnovější verzi.</span><span class="sxs-lookup"><span data-stu-id="4e1bc-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="4e1bc-115">Source</span><span class="sxs-lookup"><span data-stu-id="4e1bc-115">Source</span></span> | <span data-ttu-id="4e1bc-116">Zdroj balíčku, výchozí nastavení pro vybraný zdroj v rozevíracím seznamu zdroje</span><span class="sxs-lookup"><span data-stu-id="4e1bc-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="4e1bc-117">Licence</span><span class="sxs-lookup"><span data-stu-id="4e1bc-117">License</span></span> | <span data-ttu-id="4e1bc-118">Otevře prohlížeč na adresu URL licence balíčku.</span><span class="sxs-lookup"><span data-stu-id="4e1bc-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="4e1bc-119">Pokud není zadána žádná licence ani parametr-ReportAbuse, prohlížeč otevře adresu URL projektu balíčku.</span><span class="sxs-lookup"><span data-stu-id="4e1bc-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="4e1bc-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="4e1bc-120">ReportAbuse</span></span> | <span data-ttu-id="4e1bc-121">Otevře prohlížeč na adrese URL pro zneužití sestavy balíčku.</span><span class="sxs-lookup"><span data-stu-id="4e1bc-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="4e1bc-122">Pokud není zadána žádná licence ani parametr-ReportAbuse, prohlížeč otevře adresu URL projektu balíčku.</span><span class="sxs-lookup"><span data-stu-id="4e1bc-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="4e1bc-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="4e1bc-123">PassThru</span></span> | <span data-ttu-id="4e1bc-124">Zobrazí adresu URL. pro potlačení otevírání prohlížeče použijte příkaz with-WhatIf.</span><span class="sxs-lookup"><span data-stu-id="4e1bc-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="4e1bc-125">Žádný z těchto parametrů nepřijímají vstupní ani zástupné znaky kanálu.</span><span class="sxs-lookup"><span data-stu-id="4e1bc-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="4e1bc-126">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="4e1bc-126">Common Parameters</span></span>

<span data-ttu-id="4e1bc-127">`Open-PackagePage`podporuje následující [běžné parametry PowerShellu](http://go.microsoft.com/fwlink/?LinkID=113216): Ladit, Error Action, ErrorVariable, unbuffer, subvariable, PipelineVariable, verbose, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="4e1bc-127">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="4e1bc-128">Příklady</span><span class="sxs-lookup"><span data-stu-id="4e1bc-128">Examples</span></span>

```ps
# Opens a browser with the Ninject package's project page
Open-PackagePage Ninject

# Opens a browser with the Ninject package's license page
Open-PackagePage Ninject -License

# Opens a browser with the Ninject package's report abuse page  
Open-PackagePage Ninject -ReportAbuse

# Assigns the license URL to the variable, $url, without launching the browser
$url = Open-PackagePage Ninject -License -PassThru -WhatIf
```