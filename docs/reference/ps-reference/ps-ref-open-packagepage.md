---
title: Reference k NuGet Open-PackagePage PowerShellu
description: Referenční informace k příkazu Open-PackagePage PowerShellu v konzole správce balíčků NuGet v aplikaci Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d34a91007197f8004e4923deedb1cdb26d662d53
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780404"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="0ec80-103">Open-PackagePage (konzola správce balíčků v aplikaci Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="0ec80-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="0ec80-104">*Zastaralé v 3.0 +; k dispozici pouze v rámci [konzoly Správce balíčků](../../consume-packages/install-use-packages-powershell.md) v sadě Visual Studio ve Windows.*</span><span class="sxs-lookup"><span data-stu-id="0ec80-104">*Deprecated in 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="0ec80-105">Spustí výchozí prohlížeč s adresou URL projektu, licence nebo sestavy pro zneužití zadaného balíčku.</span><span class="sxs-lookup"><span data-stu-id="0ec80-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="0ec80-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="0ec80-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="0ec80-107">Parametry</span><span class="sxs-lookup"><span data-stu-id="0ec80-107">Parameters</span></span>

| <span data-ttu-id="0ec80-108">Parametr</span><span class="sxs-lookup"><span data-stu-id="0ec80-108">Parameter</span></span> | <span data-ttu-id="0ec80-109">Popis</span><span class="sxs-lookup"><span data-stu-id="0ec80-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0ec80-110">Id</span><span class="sxs-lookup"><span data-stu-id="0ec80-110">Id</span></span> | <span data-ttu-id="0ec80-111">ID balíčku požadovaného balíčku.</span><span class="sxs-lookup"><span data-stu-id="0ec80-111">The package ID of the desired package.</span></span> <span data-ttu-id="0ec80-112">Samotný přepínač-ID je nepovinný.</span><span class="sxs-lookup"><span data-stu-id="0ec80-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="0ec80-113">Verze</span><span class="sxs-lookup"><span data-stu-id="0ec80-113">Version</span></span> | <span data-ttu-id="0ec80-114">Verze balíčku, výchozí nastavení na nejnovější verzi.</span><span class="sxs-lookup"><span data-stu-id="0ec80-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="0ec80-115">Zdroj</span><span class="sxs-lookup"><span data-stu-id="0ec80-115">Source</span></span> | <span data-ttu-id="0ec80-116">Zdroj balíčku, výchozí nastavení pro vybraný zdroj v rozevíracím seznamu zdroje</span><span class="sxs-lookup"><span data-stu-id="0ec80-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="0ec80-117">Licence</span><span class="sxs-lookup"><span data-stu-id="0ec80-117">License</span></span> | <span data-ttu-id="0ec80-118">Otevře prohlížeč na adresu URL licence balíčku.</span><span class="sxs-lookup"><span data-stu-id="0ec80-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="0ec80-119">Pokud není zadána žádná licence ani parametr-ReportAbuse, prohlížeč otevře adresu URL projektu balíčku.</span><span class="sxs-lookup"><span data-stu-id="0ec80-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="0ec80-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="0ec80-120">ReportAbuse</span></span> | <span data-ttu-id="0ec80-121">Otevře prohlížeč na adrese URL pro zneužití sestavy balíčku.</span><span class="sxs-lookup"><span data-stu-id="0ec80-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="0ec80-122">Pokud není zadána žádná licence ani parametr-ReportAbuse, prohlížeč otevře adresu URL projektu balíčku.</span><span class="sxs-lookup"><span data-stu-id="0ec80-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="0ec80-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="0ec80-123">PassThru</span></span> | <span data-ttu-id="0ec80-124">Zobrazí adresu URL. pro potlačení otevírání prohlížeče použijte příkaz with-WhatIf.</span><span class="sxs-lookup"><span data-stu-id="0ec80-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="0ec80-125">Žádný z těchto parametrů nepřijímají vstupní ani zástupné znaky kanálu.</span><span class="sxs-lookup"><span data-stu-id="0ec80-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="0ec80-126">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="0ec80-126">Common Parameters</span></span>

<span data-ttu-id="0ec80-127">`Open-PackagePage` podporuje následující [běžné parametry PowerShellu](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, inbuffer, subvariable, PipelineVariable, verbose, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="0ec80-127">`Open-PackagePage` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="0ec80-128">Příklady</span><span class="sxs-lookup"><span data-stu-id="0ec80-128">Examples</span></span>

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