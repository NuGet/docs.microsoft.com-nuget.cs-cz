---
title: Referenční informace prostředí PowerShell NuGet Open-PackagePage | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referenční dokumentace pro příkaz prostředí PowerShell PackagePage otevřete v konzole Správce balíčků NuGet v sadě Visual Studio.
keywords: NuGet konzoly Správce balíčků, příkazy prostředí NuGet Powershell, odkaz NuGet Powershell, otevřete PackagePage
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 5e0955e58daacf381666c676c8fcf22c698e9db6
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="7a00f-104">Otevřete PackagePage (konzola Správce balíčků v sadě Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="7a00f-104">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="7a00f-105">*Zastaralé v 3.0 +; k dispozici pouze v rámci [Konzola správce balíčků NuGet](package-manager-console.md) v sadě Visual Studio v systému Windows.*</span><span class="sxs-lookup"><span data-stu-id="7a00f-105">*Deprecated in 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="7a00f-106">Spuštění výchozího prohlížeče s projektu, licence nebo adresy URL sestav zneužití pro zadaný balíček.</span><span class="sxs-lookup"><span data-stu-id="7a00f-106">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="7a00f-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="7a00f-107">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="7a00f-108">Parametry</span><span class="sxs-lookup"><span data-stu-id="7a00f-108">Parameters</span></span>

| <span data-ttu-id="7a00f-109">Parametr</span><span class="sxs-lookup"><span data-stu-id="7a00f-109">Parameter</span></span> | <span data-ttu-id="7a00f-110">Popis</span><span class="sxs-lookup"><span data-stu-id="7a00f-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7a00f-111">ID</span><span class="sxs-lookup"><span data-stu-id="7a00f-111">Id</span></span> | <span data-ttu-id="7a00f-112">ID balíčku požadované balíčku.</span><span class="sxs-lookup"><span data-stu-id="7a00f-112">The package ID of the desired package.</span></span> <span data-ttu-id="7a00f-113">-Id je volitelný přepínač sám sebe.</span><span class="sxs-lookup"><span data-stu-id="7a00f-113">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="7a00f-114">Version</span><span class="sxs-lookup"><span data-stu-id="7a00f-114">Version</span></span> | <span data-ttu-id="7a00f-115">Verze balíčku, jako výchozí bude použit na nejnovější verzi.</span><span class="sxs-lookup"><span data-stu-id="7a00f-115">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="7a00f-116">Zdroj</span><span class="sxs-lookup"><span data-stu-id="7a00f-116">Source</span></span> | <span data-ttu-id="7a00f-117">Zdroj balíčku jako výchozí bude použit zdroj vybraný v zdroji rozevíracího seznamu.</span><span class="sxs-lookup"><span data-stu-id="7a00f-117">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="7a00f-118">License</span><span class="sxs-lookup"><span data-stu-id="7a00f-118">License</span></span> | <span data-ttu-id="7a00f-119">Otevře prohlížeč na adrese URL licence balíčku.</span><span class="sxs-lookup"><span data-stu-id="7a00f-119">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="7a00f-120">Pokud je zadán - licence ani - ReportAbuse, prohlížeči se otevře adresa URL projektu balíčku.</span><span class="sxs-lookup"><span data-stu-id="7a00f-120">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="7a00f-121">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="7a00f-121">ReportAbuse</span></span> | <span data-ttu-id="7a00f-122">Otevře prohlížeč na adresu URL zneužití sestavy balíčku.</span><span class="sxs-lookup"><span data-stu-id="7a00f-122">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="7a00f-123">Pokud je zadán - licence ani - ReportAbuse, prohlížeči se otevře adresa URL projektu balíčku.</span><span class="sxs-lookup"><span data-stu-id="7a00f-123">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="7a00f-124">PassThru</span><span class="sxs-lookup"><span data-stu-id="7a00f-124">PassThru</span></span> | <span data-ttu-id="7a00f-125">Zobrazí adresu URL; pomocí s - WhatIf potlačit, otevřete v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="7a00f-125">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="7a00f-126">Žádná z těchto parametrů přijmout kanálu vstup nebo zástupné znaky.</span><span class="sxs-lookup"><span data-stu-id="7a00f-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="7a00f-127">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="7a00f-127">Common Parameters</span></span>

<span data-ttu-id="7a00f-128">`Open-PackagePage` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, podrobná, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="7a00f-128">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="7a00f-129">Příklady</span><span class="sxs-lookup"><span data-stu-id="7a00f-129">Examples</span></span>

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