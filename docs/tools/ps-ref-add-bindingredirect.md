---
title: Referenční informace prostředí PowerShell NuGet BindingRedirect
description: Referenční informace pro příkaz prostředí PowerShell Add-BindingRedirect v konzole Správce balíčků NuGet v sadě Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a5f318ddfb2bb8498ab3e608f8036be05dcb0706
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842541"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="6c9af-103">Add-BindingRedirect (konzola Správce balíčků v sadě Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="6c9af-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="6c9af-104">*K dispozici pouze v rámci [Konzola správce balíčků](package-manager-console.md) v sadě Visual Studio ve Windows.*</span><span class="sxs-lookup"><span data-stu-id="6c9af-104">*Available only within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="6c9af-105">Zkontroluje ve všech sestaveních ve výstupní cesta pro projekt a v případě potřeby přidá přesměrování vazby do konfiguračního souboru aplikace nebo web.</span><span class="sxs-lookup"><span data-stu-id="6c9af-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="6c9af-106">Tento příkaz spustí automaticky při instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="6c9af-106">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="6c9af-107">Podrobnosti o vazby přesměrování a proč se používají, najdete v části [přesměrování verze sestavení](/dotnet/framework/configure-apps/redirect-assembly-versions) v dokumentaci k rozhraní .NET.</span><span class="sxs-lookup"><span data-stu-id="6c9af-107">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="6c9af-108">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="6c9af-108">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="6c9af-109">Parametry</span><span class="sxs-lookup"><span data-stu-id="6c9af-109">Parameters</span></span>

| <span data-ttu-id="6c9af-110">Parametr</span><span class="sxs-lookup"><span data-stu-id="6c9af-110">Parameter</span></span> | <span data-ttu-id="6c9af-111">Popis</span><span class="sxs-lookup"><span data-stu-id="6c9af-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6c9af-112">ProjectName</span><span class="sxs-lookup"><span data-stu-id="6c9af-112">ProjectName</span></span> | <span data-ttu-id="6c9af-113">(Povinné) Projekt, do které chcete přidat přesměrování vazby.</span><span class="sxs-lookup"><span data-stu-id="6c9af-113">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="6c9af-114">Je volitelný přepínač - ProjectName samotný.</span><span class="sxs-lookup"><span data-stu-id="6c9af-114">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="6c9af-115">Žádná z těchto parametrů přijímat kanálu vstup nebo zástupné znaky.</span><span class="sxs-lookup"><span data-stu-id="6c9af-115">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="6c9af-116">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="6c9af-116">Common Parameters</span></span>

<span data-ttu-id="6c9af-117">`Add-BindingRedirect` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="6c9af-117">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="6c9af-118">Příklady</span><span class="sxs-lookup"><span data-stu-id="6c9af-118">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```