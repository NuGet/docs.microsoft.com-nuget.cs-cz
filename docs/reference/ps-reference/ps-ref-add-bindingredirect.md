---
title: Reference k NuGet Add-BindingRedirect PowerShellu
description: Referenční informace k příkazu Add-BindingRedirect PowerShellu v konzole správce balíčků NuGet v aplikaci Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 62edf1bf8995a4e1ffb83acc7a7621a786cc53e4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777617"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="289b4-103">Add-BindingRedirect (konzola správce balíčků v aplikaci Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="289b4-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="289b4-104">*K dispozici pouze v rámci [konzoly Správce balíčků](../../consume-packages/install-use-packages-powershell.md) v sadě Visual Studio ve Windows.*</span><span class="sxs-lookup"><span data-stu-id="289b4-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="289b4-105">Prověřuje všechna sestavení v rámci výstupní cesty pro projekt a v případě potřeby přidá přesměrování vazby na konfigurační soubor aplikace nebo webu.</span><span class="sxs-lookup"><span data-stu-id="289b4-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="289b4-106">Tento příkaz se spustí automaticky při instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="289b4-106">This command is run automatically when installing a package.</span></span>

> [!NOTE]
> <span data-ttu-id="289b4-107">To se týká jenom scénářů, které používají soubor packages.config.</span><span class="sxs-lookup"><span data-stu-id="289b4-107">This only applies to scenarios using a packages.config file.</span></span> <span data-ttu-id="289b4-108">Další informace najdete v dokumentaci k [souboru NuGet packages.config](~/reference/packages-config.md).</span><span class="sxs-lookup"><span data-stu-id="289b4-108">For more information, see [NuGet packages.config file reference](~/reference/packages-config.md).</span></span>

<span data-ttu-id="289b4-109">Podrobnosti o přesměrování vazby a o tom, proč se používají, naleznete v tématu [Přesměrování verzí sestavení](/dotnet/framework/configure-apps/redirect-assembly-versions) v dokumentaci .NET.</span><span class="sxs-lookup"><span data-stu-id="289b4-109">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="289b4-110">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="289b4-110">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="289b4-111">Parametry</span><span class="sxs-lookup"><span data-stu-id="289b4-111">Parameters</span></span>

| <span data-ttu-id="289b4-112">Parametr</span><span class="sxs-lookup"><span data-stu-id="289b4-112">Parameter</span></span> | <span data-ttu-id="289b4-113">Popis</span><span class="sxs-lookup"><span data-stu-id="289b4-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="289b4-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="289b4-114">ProjectName</span></span> | <span data-ttu-id="289b4-115">Požadovanou Projekt, ke kterému chcete přidat přesměrování vazby.</span><span class="sxs-lookup"><span data-stu-id="289b4-115">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="289b4-116">Samotný přepínač-ProjectName je nepovinný.</span><span class="sxs-lookup"><span data-stu-id="289b4-116">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="289b4-117">Žádný z těchto parametrů nepřijímají vstupní ani zástupné znaky kanálu.</span><span class="sxs-lookup"><span data-stu-id="289b4-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="289b4-118">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="289b4-118">Common Parameters</span></span>

<span data-ttu-id="289b4-119">`Add-BindingRedirect` podporuje následující [běžné parametry PowerShellu](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, inbuffer, subvariable, PipelineVariable, verbose, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="289b4-119">`Add-BindingRedirect` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="289b4-120">Příklady</span><span class="sxs-lookup"><span data-stu-id="289b4-120">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```