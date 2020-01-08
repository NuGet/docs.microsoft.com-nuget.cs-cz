---
title: Reference k prostředí NuGet Add-BindingRedirect
description: Reference pro příkaz prostředí PowerShell Add-BindingRedirect v konzole správce balíčků NuGet v aplikaci Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d3d156cf882229260e8cf55f8ece2804aec36dc9
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384981"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="86593-103">Add-BindingRedirect (konzola Správce balíčků v sadě Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="86593-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="86593-104">*K dispozici pouze v rámci [konzoly Správce balíčků](../../consume-packages/install-use-packages-powershell.md) v sadě Visual Studio ve Windows.*</span><span class="sxs-lookup"><span data-stu-id="86593-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="86593-105">Prověřuje všechna sestavení v rámci výstupní cesty pro projekt a v případě potřeby přidá přesměrování vazby na konfigurační soubor aplikace nebo webu.</span><span class="sxs-lookup"><span data-stu-id="86593-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="86593-106">Tento příkaz se spustí automaticky při instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="86593-106">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="86593-107">Podrobnosti o přesměrování vazby a o tom, proč se používají, naleznete v tématu [Přesměrování verzí sestavení](/dotnet/framework/configure-apps/redirect-assembly-versions) v dokumentaci .NET.</span><span class="sxs-lookup"><span data-stu-id="86593-107">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="86593-108">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="86593-108">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="86593-109">Parametry</span><span class="sxs-lookup"><span data-stu-id="86593-109">Parameters</span></span>

| <span data-ttu-id="86593-110">Parametr</span><span class="sxs-lookup"><span data-stu-id="86593-110">Parameter</span></span> | <span data-ttu-id="86593-111">Popis</span><span class="sxs-lookup"><span data-stu-id="86593-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="86593-112">ProjectName</span><span class="sxs-lookup"><span data-stu-id="86593-112">ProjectName</span></span> | <span data-ttu-id="86593-113">Požadovanou Projekt, ke kterému chcete přidat přesměrování vazby.</span><span class="sxs-lookup"><span data-stu-id="86593-113">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="86593-114">Samotný přepínač-ProjectName je nepovinný.</span><span class="sxs-lookup"><span data-stu-id="86593-114">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="86593-115">Žádný z těchto parametrů nepřijímají vstupní ani zástupné znaky kanálu.</span><span class="sxs-lookup"><span data-stu-id="86593-115">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="86593-116">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="86593-116">Common Parameters</span></span>

<span data-ttu-id="86593-117">`Add-BindingRedirect` podporuje následující [běžné parametry PowerShellu](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, inbuffer, subvariable, PipelineVariable, verbose, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="86593-117">`Add-BindingRedirect` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="86593-118">Příklady</span><span class="sxs-lookup"><span data-stu-id="86593-118">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```