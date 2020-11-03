---
title: Reference k NuGet Register-TabExpansion PowerShellu
description: Referenční informace k příkazu Register-TabExpansion PowerShellu v konzole správce balíčků NuGet v aplikaci Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 9d5bae2878cb6bf0848bca9a5ed9af0fee61bb85
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237150"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="7a7d0-103">Register-TabExpansion (konzola správce balíčků v aplikaci Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="7a7d0-103">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="7a7d0-104">*K dispozici pouze v rámci [konzoly Správce balíčků](../../consume-packages/install-use-packages-powershell.md) v sadě Visual Studio ve Windows.*</span><span class="sxs-lookup"><span data-stu-id="7a7d0-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="7a7d0-105">Zaregistruje rozšíření pro parametry zadaného příkazu, například když se při zadání příkazu použije karta, rozšíří se hodnoty jako dostupné možnosti pro daný parametr.</span><span class="sxs-lookup"><span data-stu-id="7a7d0-105">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="7a7d0-106">Všechna předchozí rozšíření pro příkaz jsou přepsána.</span><span class="sxs-lookup"><span data-stu-id="7a7d0-106">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="7a7d0-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="7a7d0-107">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="7a7d0-108">Parametry</span><span class="sxs-lookup"><span data-stu-id="7a7d0-108">Parameters</span></span>

| <span data-ttu-id="7a7d0-109">Parametr</span><span class="sxs-lookup"><span data-stu-id="7a7d0-109">Parameter</span></span> | <span data-ttu-id="7a7d0-110">Popis</span><span class="sxs-lookup"><span data-stu-id="7a7d0-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7a7d0-111">Název</span><span class="sxs-lookup"><span data-stu-id="7a7d0-111">Name</span></span> | <span data-ttu-id="7a7d0-112">Požadovanou Příkaz, pro který mají být zaregistrována rozšíření.</span><span class="sxs-lookup"><span data-stu-id="7a7d0-112">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="7a7d0-113">Samotný přepínač-Name je nepovinný.</span><span class="sxs-lookup"><span data-stu-id="7a7d0-113">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="7a7d0-114">Definice</span><span class="sxs-lookup"><span data-stu-id="7a7d0-114">Definition</span></span> | <span data-ttu-id="7a7d0-115">Požadovanou Objekt popisující argument v syntaxi, `@{'<parameter>' = {'<value1>', '<value2>', ...}}` kde `<parameter>` je název parametru, který má být upraven, a každý `<value>` z nich poskytuje konkrétní rozšíření.</span><span class="sxs-lookup"><span data-stu-id="7a7d0-115">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="7a7d0-116">Jsou přijímány jednoduché i dvojité uvozovky.</span><span class="sxs-lookup"><span data-stu-id="7a7d0-116">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="7a7d0-117">Žádný z těchto parametrů nepřijímají vstupní ani zástupné znaky kanálu.</span><span class="sxs-lookup"><span data-stu-id="7a7d0-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="7a7d0-118">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="7a7d0-118">Common Parameters</span></span>

<span data-ttu-id="7a7d0-119">`Register-TabExpansion` podporuje následující [běžné parametry PowerShellu](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, inbuffer, subvariable, PipelineVariable, verbose, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="7a7d0-119">`Register-TabExpansion` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="7a7d0-120">Příklady</span><span class="sxs-lookup"><span data-stu-id="7a7d0-120">Examples</span></span>

<span data-ttu-id="7a7d0-121">Vezměte v úvahu řešení, které obsahuje tři projekty s názvy EventManager, nástroje a SpecialParser.</span><span class="sxs-lookup"><span data-stu-id="7a7d0-121">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="7a7d0-122">Vývojář často používá `Update-Package` příkaz v různých časech s každým z těchto projektů.</span><span class="sxs-lookup"><span data-stu-id="7a7d0-122">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="7a7d0-123">Zjistí, že má `Update-Package` příkaz k dispozici rozšíření automatického dokončování pro `-ProjectName` argument, takže nemusí pokaždé zadávat název projektu.</span><span class="sxs-lookup"><span data-stu-id="7a7d0-123">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="7a7d0-124">Následující příkaz zaregistruje tyto tři názvy projektů jako rozšíření pro `-ProjectName` parametr:</span><span class="sxs-lookup"><span data-stu-id="7a7d0-124">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="7a7d0-125">Vývojář pak může zadat `Update-Package -ProjectName ` , stisknout klávesu TAB a zobrazit rozšíření nabízená jako možnosti automatického dokončování:</span><span class="sxs-lookup"><span data-stu-id="7a7d0-125">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Příklad použití Register-TabExpansion](media/Register-TabExpansion-Example.png)