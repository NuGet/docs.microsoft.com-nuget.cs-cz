---
title: Reference k prostředí NuGet Add-BindingRedirect
description: Reference pro příkaz prostředí PowerShell Add-BindingRedirect v konzole správce balíčků NuGet v aplikaci Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: b1e88d32deb3ff34833ef22a9cbb8cad3f0d4354
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328240"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="6e3ad-103">Add-BindingRedirect (konzola Správce balíčků v sadě Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="6e3ad-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="6e3ad-104">*K dispozici pouze v rámci [konzoly Správce balíčků](../../consume-packages/install-use-packages-powershell.md) v sadě Visual Studio ve Windows.*</span><span class="sxs-lookup"><span data-stu-id="6e3ad-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="6e3ad-105">Prověřuje všechna sestavení v rámci výstupní cesty pro projekt a v případě potřeby přidá přesměrování vazby na konfigurační soubor aplikace nebo webu.</span><span class="sxs-lookup"><span data-stu-id="6e3ad-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="6e3ad-106">Tento příkaz se spustí automaticky při instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="6e3ad-106">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="6e3ad-107">Podrobnosti o přesměrování vazby a o tom, proč se používají, naleznete v tématu [Přesměrování verzí sestavení](/dotnet/framework/configure-apps/redirect-assembly-versions) v dokumentaci .NET.</span><span class="sxs-lookup"><span data-stu-id="6e3ad-107">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="6e3ad-108">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="6e3ad-108">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="6e3ad-109">Parametry</span><span class="sxs-lookup"><span data-stu-id="6e3ad-109">Parameters</span></span>

| <span data-ttu-id="6e3ad-110">Parametr</span><span class="sxs-lookup"><span data-stu-id="6e3ad-110">Parameter</span></span> | <span data-ttu-id="6e3ad-111">Popis</span><span class="sxs-lookup"><span data-stu-id="6e3ad-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6e3ad-112">ProjectName</span><span class="sxs-lookup"><span data-stu-id="6e3ad-112">ProjectName</span></span> | <span data-ttu-id="6e3ad-113">Požadovanou Projekt, ke kterému chcete přidat přesměrování vazby.</span><span class="sxs-lookup"><span data-stu-id="6e3ad-113">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="6e3ad-114">Samotný přepínač-ProjectName je nepovinný.</span><span class="sxs-lookup"><span data-stu-id="6e3ad-114">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="6e3ad-115">Žádný z těchto parametrů nepřijímají vstupní ani zástupné znaky kanálu.</span><span class="sxs-lookup"><span data-stu-id="6e3ad-115">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="6e3ad-116">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="6e3ad-116">Common Parameters</span></span>

<span data-ttu-id="6e3ad-117">`Add-BindingRedirect`podporuje následující [běžné parametry PowerShellu](http://go.microsoft.com/fwlink/?LinkID=113216): Ladit, Error Action, ErrorVariable, unbuffer, subvariable, PipelineVariable, verbose, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="6e3ad-117">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="6e3ad-118">Příklady</span><span class="sxs-lookup"><span data-stu-id="6e3ad-118">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```