---
title: Referenční informace prostředí PowerShell NuGet Open-PackagePage
description: Referenční informace pro příkaz Powershellu otevřít PackagePage v konzole Správce balíčků NuGet v sadě Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: fd738f15b461051c4e9413b3035456c687979b97
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842268"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="6f8f4-103">Open-PackagePage (konzola Správce balíčků v sadě Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="6f8f4-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="6f8f4-104">*Zastaralé v 3.0 +; k dispozici pouze v rámci [Konzola správce balíčků](package-manager-console.md) v sadě Visual Studio ve Windows.*</span><span class="sxs-lookup"><span data-stu-id="6f8f4-104">*Deprecated in 3.0+; available only within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="6f8f4-105">Spustí výchozí prohlížeč s projektem, licenci nebo adresa URL sestavy zneužití pro zadaný balíček.</span><span class="sxs-lookup"><span data-stu-id="6f8f4-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="6f8f4-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="6f8f4-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="6f8f4-107">Parametry</span><span class="sxs-lookup"><span data-stu-id="6f8f4-107">Parameters</span></span>

| <span data-ttu-id="6f8f4-108">Parametr</span><span class="sxs-lookup"><span data-stu-id="6f8f4-108">Parameter</span></span> | <span data-ttu-id="6f8f4-109">Popis</span><span class="sxs-lookup"><span data-stu-id="6f8f4-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6f8f4-110">Id</span><span class="sxs-lookup"><span data-stu-id="6f8f4-110">Id</span></span> | <span data-ttu-id="6f8f4-111">ID balíčku požadovaný balíček.</span><span class="sxs-lookup"><span data-stu-id="6f8f4-111">The package ID of the desired package.</span></span> <span data-ttu-id="6f8f4-112">-Id je volitelný přepínač samotný.</span><span class="sxs-lookup"><span data-stu-id="6f8f4-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="6f8f4-113">Version</span><span class="sxs-lookup"><span data-stu-id="6f8f4-113">Version</span></span> | <span data-ttu-id="6f8f4-114">Verze balíčku, jako výchozí se použije na nejnovější verzi.</span><span class="sxs-lookup"><span data-stu-id="6f8f4-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="6f8f4-115">Source</span><span class="sxs-lookup"><span data-stu-id="6f8f4-115">Source</span></span> | <span data-ttu-id="6f8f4-116">Zdroj balíčku jako výchozí se použije zdroj vybraný ve zdroji rozevíracího seznamu.</span><span class="sxs-lookup"><span data-stu-id="6f8f4-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="6f8f4-117">Licence</span><span class="sxs-lookup"><span data-stu-id="6f8f4-117">License</span></span> | <span data-ttu-id="6f8f4-118">Otevře prohlížeč na adresu URL licence balíčku.</span><span class="sxs-lookup"><span data-stu-id="6f8f4-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="6f8f4-119">Pokud není zadána - licence ani - ReportAbuse, prohlížeči otevře adresa URL projektu daného balíčku.</span><span class="sxs-lookup"><span data-stu-id="6f8f4-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="6f8f4-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="6f8f4-120">ReportAbuse</span></span> | <span data-ttu-id="6f8f4-121">Otevře se prohlížeč, aby adresa URL balíčku sestavy zneužití.</span><span class="sxs-lookup"><span data-stu-id="6f8f4-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="6f8f4-122">Pokud není zadána - licence ani - ReportAbuse, prohlížeči otevře adresa URL projektu daného balíčku.</span><span class="sxs-lookup"><span data-stu-id="6f8f4-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="6f8f4-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="6f8f4-123">PassThru</span></span> | <span data-ttu-id="6f8f4-124">Zobrazí adresu URL; pomocí - WhatIf potlačit, otevřete v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="6f8f4-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="6f8f4-125">Žádná z těchto parametrů přijímat kanálu vstup nebo zástupné znaky.</span><span class="sxs-lookup"><span data-stu-id="6f8f4-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="6f8f4-126">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="6f8f4-126">Common Parameters</span></span>

<span data-ttu-id="6f8f4-127">`Open-PackagePage` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="6f8f4-127">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="6f8f4-128">Příklady</span><span class="sxs-lookup"><span data-stu-id="6f8f4-128">Examples</span></span>

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