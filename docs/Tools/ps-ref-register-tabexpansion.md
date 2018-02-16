---
title: "Referenční informace prostředí PowerShell NuGet Register-TabExpansion | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenční dokumentace pro příkaz prostředí PowerShell Register-TabExpansion v konzole Správce balíčků NuGet v sadě Visual Studio."
keywords: "NuGet konzoly Správce balíčků, příkazy prostředí NuGet Powershell, NuGet Powershell odkaz, Register-TabExpansion"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9e363b8a7fa7e25d24331eb3e4eb87141e6a3b97
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/14/2018
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="0a2fb-104">Register-TabExpansion (konzola Správce balíčků v sadě Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="0a2fb-104">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="0a2fb-105">*K dispozici pouze v rámci [Konzola správce balíčků NuGet](package-manager-console.md) v sadě Visual Studio v systému Windows.*</span><span class="sxs-lookup"><span data-stu-id="0a2fb-105">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="0a2fb-106">Zaregistruje karta rozšíření pro parametry zadaný příkaz tak, aby při karta se používá, když zadáte příkaz, rozšířená hodnoty se zobrazí jako dostupné možnosti pro parametr nejistá.</span><span class="sxs-lookup"><span data-stu-id="0a2fb-106">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="0a2fb-107">Všechny předchozí rozšíření pro příkaz se přepíší.</span><span class="sxs-lookup"><span data-stu-id="0a2fb-107">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="0a2fb-108">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="0a2fb-108">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="0a2fb-109">Parametry</span><span class="sxs-lookup"><span data-stu-id="0a2fb-109">Parameters</span></span>

| <span data-ttu-id="0a2fb-110">Parametr</span><span class="sxs-lookup"><span data-stu-id="0a2fb-110">Parameter</span></span> | <span data-ttu-id="0a2fb-111">Popis</span><span class="sxs-lookup"><span data-stu-id="0a2fb-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0a2fb-112">Název</span><span class="sxs-lookup"><span data-stu-id="0a2fb-112">Name</span></span> | <span data-ttu-id="0a2fb-113">(Povinné) Příkaz, do které chcete zaregistrovat rozšíření.</span><span class="sxs-lookup"><span data-stu-id="0a2fb-113">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="0a2fb-114">-Název je volitelný přepínač sám sebe.</span><span class="sxs-lookup"><span data-stu-id="0a2fb-114">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="0a2fb-115">Definice</span><span class="sxs-lookup"><span data-stu-id="0a2fb-115">Definition</span></span> | <span data-ttu-id="0a2fb-116">(Povinné) Objekt popisující argumentem v syntaxi `@{'<parameter>' = {'<value1>', '<value2>', ...}}` kde `<parameter>` je název parametru upravit a každý `<value>` poskytuje konkrétní rozšíření.</span><span class="sxs-lookup"><span data-stu-id="0a2fb-116">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="0a2fb-117">Jednoduché i dvojité uvozovky, jsou přijaty.</span><span class="sxs-lookup"><span data-stu-id="0a2fb-117">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="0a2fb-118">Žádná z těchto parametrů přijmout kanálu vstup nebo zástupné znaky.</span><span class="sxs-lookup"><span data-stu-id="0a2fb-118">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="0a2fb-119">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="0a2fb-119">Common Parameters</span></span>

<span data-ttu-id="0a2fb-120">`Register-TabExpansion` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, podrobná, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="0a2fb-120">`Register-TabExpansion` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="0a2fb-121">Příklady</span><span class="sxs-lookup"><span data-stu-id="0a2fb-121">Examples</span></span>

<span data-ttu-id="0a2fb-122">Vezměte v úvahu řešení, které obsahuje tři názvy projektů EventManager, nástrojů a SpecialParser.</span><span class="sxs-lookup"><span data-stu-id="0a2fb-122">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="0a2fb-123">Vývojář se často používá `Update-Package` příkazu v různých časech s každou z těchto projekty.</span><span class="sxs-lookup"><span data-stu-id="0a2fb-123">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="0a2fb-124">Jana vyhledá vhodné používat `Update-Package` příkaz zadejte automatické dokončování rozšíření pro `-ProjectName` argument, takže se nemusí na název projektu zadejte pokaždé, když.</span><span class="sxs-lookup"><span data-stu-id="0a2fb-124">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="0a2fb-125">Následující příkaz, pak zaregistruje názvy těchto tří projektů jako rozšíření pro `-ProjectName` parametr:</span><span class="sxs-lookup"><span data-stu-id="0a2fb-125">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="0a2fb-126">Vývojář může zadejte `Update-Package -ProjectName `, stiskněte klávesu Tab a rozšíření nabízeny jako možnosti automatického dokončování v tématu:</span><span class="sxs-lookup"><span data-stu-id="0a2fb-126">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Příklad použití Register-TabExpansion](media/Register-TabExpansion-Example.png)
