---
title: Referenční informace prostředí PowerShell NuGet Register-TabExpansion
description: Referenční dokumentace pro příkaz prostředí PowerShell Register-TabExpansion v konzole Správce balíčků NuGet v sadě Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8011c0e6aa951a32114d460803c493810964a7e0
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818410"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="63568-103">Register-TabExpansion (konzola Správce balíčků v sadě Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="63568-103">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="63568-104">*K dispozici pouze v rámci [Konzola správce balíčků NuGet](package-manager-console.md) v sadě Visual Studio v systému Windows.*</span><span class="sxs-lookup"><span data-stu-id="63568-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="63568-105">Zaregistruje karta rozšíření pro parametry zadaný příkaz tak, aby při karta se používá, když zadáte příkaz, rozšířená hodnoty se zobrazí jako dostupné možnosti pro parametr nejistá.</span><span class="sxs-lookup"><span data-stu-id="63568-105">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="63568-106">Všechny předchozí rozšíření pro příkaz se přepíší.</span><span class="sxs-lookup"><span data-stu-id="63568-106">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="63568-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="63568-107">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="63568-108">Parametry</span><span class="sxs-lookup"><span data-stu-id="63568-108">Parameters</span></span>

| <span data-ttu-id="63568-109">Parametr</span><span class="sxs-lookup"><span data-stu-id="63568-109">Parameter</span></span> | <span data-ttu-id="63568-110">Popis</span><span class="sxs-lookup"><span data-stu-id="63568-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="63568-111">Název</span><span class="sxs-lookup"><span data-stu-id="63568-111">Name</span></span> | <span data-ttu-id="63568-112">(Povinné) Příkaz, do které chcete zaregistrovat rozšíření.</span><span class="sxs-lookup"><span data-stu-id="63568-112">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="63568-113">-Název je volitelný přepínač sám sebe.</span><span class="sxs-lookup"><span data-stu-id="63568-113">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="63568-114">Definice</span><span class="sxs-lookup"><span data-stu-id="63568-114">Definition</span></span> | <span data-ttu-id="63568-115">(Povinné) Objekt popisující argumentem v syntaxi `@{'<parameter>' = {'<value1>', '<value2>', ...}}` kde `<parameter>` je název parametru upravit a každý `<value>` poskytuje konkrétní rozšíření.</span><span class="sxs-lookup"><span data-stu-id="63568-115">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="63568-116">Jednoduché i dvojité uvozovky, jsou přijaty.</span><span class="sxs-lookup"><span data-stu-id="63568-116">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="63568-117">Žádná z těchto parametrů přijmout kanálu vstup nebo zástupné znaky.</span><span class="sxs-lookup"><span data-stu-id="63568-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="63568-118">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="63568-118">Common Parameters</span></span>

<span data-ttu-id="63568-119">`Register-TabExpansion` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, podrobná, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="63568-119">`Register-TabExpansion` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="63568-120">Příklady</span><span class="sxs-lookup"><span data-stu-id="63568-120">Examples</span></span>

<span data-ttu-id="63568-121">Vezměte v úvahu řešení, které obsahuje tři názvy projektů EventManager, nástrojů a SpecialParser.</span><span class="sxs-lookup"><span data-stu-id="63568-121">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="63568-122">Vývojář se často používá `Update-Package` příkazu v různých časech s každou z těchto projekty.</span><span class="sxs-lookup"><span data-stu-id="63568-122">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="63568-123">Jana vyhledá vhodné používat `Update-Package` příkaz zadejte automatické dokončování rozšíření pro `-ProjectName` argument, takže se nemusí na název projektu zadejte pokaždé, když.</span><span class="sxs-lookup"><span data-stu-id="63568-123">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="63568-124">Následující příkaz, pak zaregistruje názvy těchto tří projektů jako rozšíření pro `-ProjectName` parametr:</span><span class="sxs-lookup"><span data-stu-id="63568-124">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="63568-125">Vývojář může zadejte `Update-Package -ProjectName `, stiskněte klávesu Tab a rozšíření nabízeny jako možnosti automatického dokončování v tématu:</span><span class="sxs-lookup"><span data-stu-id="63568-125">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Příklad použití Register-TabExpansion](media/Register-TabExpansion-Example.png)
