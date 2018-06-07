---
title: Referenční informace prostředí PowerShell NuGet Open-PackagePage
description: Referenční dokumentace pro příkaz prostředí PowerShell PackagePage otevřete v konzole Správce balíčků NuGet v sadě Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: e64a83c01a7baac330c99fe40ba52f328a2133b8
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817717"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="ee281-103">Open-PackagePage (konzola Správce balíčků v sadě Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="ee281-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="ee281-104">*Zastaralé v 3.0 +; k dispozici pouze v rámci [Konzola správce balíčků NuGet](package-manager-console.md) v sadě Visual Studio v systému Windows.*</span><span class="sxs-lookup"><span data-stu-id="ee281-104">*Deprecated in 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="ee281-105">Spuštění výchozího prohlížeče s projektu, licence nebo adresy URL sestav zneužití pro zadaný balíček.</span><span class="sxs-lookup"><span data-stu-id="ee281-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="ee281-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="ee281-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="ee281-107">Parametry</span><span class="sxs-lookup"><span data-stu-id="ee281-107">Parameters</span></span>

| <span data-ttu-id="ee281-108">Parametr</span><span class="sxs-lookup"><span data-stu-id="ee281-108">Parameter</span></span> | <span data-ttu-id="ee281-109">Popis</span><span class="sxs-lookup"><span data-stu-id="ee281-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ee281-110">ID</span><span class="sxs-lookup"><span data-stu-id="ee281-110">Id</span></span> | <span data-ttu-id="ee281-111">ID balíčku požadované balíčku.</span><span class="sxs-lookup"><span data-stu-id="ee281-111">The package ID of the desired package.</span></span> <span data-ttu-id="ee281-112">-Id je volitelný přepínač sám sebe.</span><span class="sxs-lookup"><span data-stu-id="ee281-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="ee281-113">Version</span><span class="sxs-lookup"><span data-stu-id="ee281-113">Version</span></span> | <span data-ttu-id="ee281-114">Verze balíčku, jako výchozí bude použit na nejnovější verzi.</span><span class="sxs-lookup"><span data-stu-id="ee281-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="ee281-115">Zdroj</span><span class="sxs-lookup"><span data-stu-id="ee281-115">Source</span></span> | <span data-ttu-id="ee281-116">Zdroj balíčku jako výchozí bude použit zdroj vybraný v zdroji rozevíracího seznamu.</span><span class="sxs-lookup"><span data-stu-id="ee281-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="ee281-117">Licence</span><span class="sxs-lookup"><span data-stu-id="ee281-117">License</span></span> | <span data-ttu-id="ee281-118">Otevře prohlížeč na adrese URL licence balíčku.</span><span class="sxs-lookup"><span data-stu-id="ee281-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="ee281-119">Pokud je zadán - licence ani - ReportAbuse, prohlížeči se otevře adresa URL projektu balíčku.</span><span class="sxs-lookup"><span data-stu-id="ee281-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="ee281-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="ee281-120">ReportAbuse</span></span> | <span data-ttu-id="ee281-121">Otevře prohlížeč na adresu URL zneužití sestavy balíčku.</span><span class="sxs-lookup"><span data-stu-id="ee281-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="ee281-122">Pokud je zadán - licence ani - ReportAbuse, prohlížeči se otevře adresa URL projektu balíčku.</span><span class="sxs-lookup"><span data-stu-id="ee281-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="ee281-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="ee281-123">PassThru</span></span> | <span data-ttu-id="ee281-124">Zobrazí adresu URL; pomocí s - WhatIf potlačit, otevřete v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="ee281-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="ee281-125">Žádná z těchto parametrů přijmout kanálu vstup nebo zástupné znaky.</span><span class="sxs-lookup"><span data-stu-id="ee281-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="ee281-126">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="ee281-126">Common Parameters</span></span>

<span data-ttu-id="ee281-127">`Open-PackagePage` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, podrobná, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="ee281-127">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="ee281-128">Příklady</span><span class="sxs-lookup"><span data-stu-id="ee281-128">Examples</span></span>

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