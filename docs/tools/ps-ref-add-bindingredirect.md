---
title: Referenční informace prostředí PowerShell NuGet BindingRedirect
description: Referenční dokumentace pro příkaz prostředí PowerShell přidat BindingRedirect v konzole Správce balíčků NuGet v sadě Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: f3addd95b64d78eac201deeb2c64915ea935cd71
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817620"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="55d97-103">Add-BindingRedirect (konzola Správce balíčků v sadě Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="55d97-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="55d97-104">*K dispozici pouze v rámci [Konzola správce balíčků NuGet](package-manager-console.md) v sadě Visual Studio v systému Windows.*</span><span class="sxs-lookup"><span data-stu-id="55d97-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="55d97-105">Hledá ve všech sestaveních ve výstupní cestě pro projekt a potřeby přidá přesměrování vazby do konfiguračního souboru aplikace nebo webu.</span><span class="sxs-lookup"><span data-stu-id="55d97-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="55d97-106">Tento příkaz spustí automaticky při instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="55d97-106">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="55d97-107">Podrobnosti o vazby přesměrování a proč se používají, najdete v části [přesměrování verzí sestavení](/dotnet/framework/configure-apps/redirect-assembly-versions) v dokumentaci k rozhraní .NET.</span><span class="sxs-lookup"><span data-stu-id="55d97-107">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="55d97-108">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="55d97-108">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="55d97-109">Parametry</span><span class="sxs-lookup"><span data-stu-id="55d97-109">Parameters</span></span>

| <span data-ttu-id="55d97-110">Parametr</span><span class="sxs-lookup"><span data-stu-id="55d97-110">Parameter</span></span> | <span data-ttu-id="55d97-111">Popis</span><span class="sxs-lookup"><span data-stu-id="55d97-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="55d97-112">ProjectName</span><span class="sxs-lookup"><span data-stu-id="55d97-112">ProjectName</span></span> | <span data-ttu-id="55d97-113">(Povinné) Projekt, pro které má být přidána přesměrování vazby.</span><span class="sxs-lookup"><span data-stu-id="55d97-113">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="55d97-114">Je volitelný přepínač - ProjectName sám sebe.</span><span class="sxs-lookup"><span data-stu-id="55d97-114">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="55d97-115">Žádná z těchto parametrů přijmout kanálu vstup nebo zástupné znaky.</span><span class="sxs-lookup"><span data-stu-id="55d97-115">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="55d97-116">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="55d97-116">Common Parameters</span></span>

<span data-ttu-id="55d97-117">`Add-BindingRedirect` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, podrobná, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="55d97-117">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="55d97-118">Příklady</span><span class="sxs-lookup"><span data-stu-id="55d97-118">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```