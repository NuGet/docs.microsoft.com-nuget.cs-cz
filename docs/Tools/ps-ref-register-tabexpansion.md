---
title: Referenční informace prostředí PowerShell NuGet Register-TabExpansion | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referenční dokumentace pro příkaz prostředí PowerShell Register-TabExpansion v konzole Správce balíčků NuGet v sadě Visual Studio.
keywords: NuGet konzoly Správce balíčků, příkazy prostředí NuGet Powershell, NuGet Powershell odkaz, Register-TabExpansion
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: c7b95c46c55b95a8d743f9661ef9c63433b0192d
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="6ab33-104">Register-TabExpansion (konzola Správce balíčků v sadě Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="6ab33-104">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="6ab33-105">*K dispozici pouze v rámci [Konzola správce balíčků NuGet](package-manager-console.md) v sadě Visual Studio v systému Windows.*</span><span class="sxs-lookup"><span data-stu-id="6ab33-105">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="6ab33-106">Zaregistruje karta rozšíření pro parametry zadaný příkaz tak, aby při karta se používá, když zadáte příkaz, rozšířená hodnoty se zobrazí jako dostupné možnosti pro parametr nejistá.</span><span class="sxs-lookup"><span data-stu-id="6ab33-106">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="6ab33-107">Všechny předchozí rozšíření pro příkaz se přepíší.</span><span class="sxs-lookup"><span data-stu-id="6ab33-107">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="6ab33-108">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="6ab33-108">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="6ab33-109">Parametry</span><span class="sxs-lookup"><span data-stu-id="6ab33-109">Parameters</span></span>

| <span data-ttu-id="6ab33-110">Parametr</span><span class="sxs-lookup"><span data-stu-id="6ab33-110">Parameter</span></span> | <span data-ttu-id="6ab33-111">Popis</span><span class="sxs-lookup"><span data-stu-id="6ab33-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6ab33-112">Název</span><span class="sxs-lookup"><span data-stu-id="6ab33-112">Name</span></span> | <span data-ttu-id="6ab33-113">(Povinné) Příkaz, do které chcete zaregistrovat rozšíření.</span><span class="sxs-lookup"><span data-stu-id="6ab33-113">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="6ab33-114">-Název je volitelný přepínač sám sebe.</span><span class="sxs-lookup"><span data-stu-id="6ab33-114">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="6ab33-115">Definice</span><span class="sxs-lookup"><span data-stu-id="6ab33-115">Definition</span></span> | <span data-ttu-id="6ab33-116">(Povinné) Objekt popisující argumentem v syntaxi `@{'<parameter>' = {'<value1>', '<value2>', ...}}` kde `<parameter>` je název parametru upravit a každý `<value>` poskytuje konkrétní rozšíření.</span><span class="sxs-lookup"><span data-stu-id="6ab33-116">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="6ab33-117">Jednoduché i dvojité uvozovky, jsou přijaty.</span><span class="sxs-lookup"><span data-stu-id="6ab33-117">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="6ab33-118">Žádná z těchto parametrů přijmout kanálu vstup nebo zástupné znaky.</span><span class="sxs-lookup"><span data-stu-id="6ab33-118">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="6ab33-119">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="6ab33-119">Common Parameters</span></span>

<span data-ttu-id="6ab33-120">`Register-TabExpansion` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, podrobná, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="6ab33-120">`Register-TabExpansion` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="6ab33-121">Příklady</span><span class="sxs-lookup"><span data-stu-id="6ab33-121">Examples</span></span>

<span data-ttu-id="6ab33-122">Vezměte v úvahu řešení, které obsahuje tři názvy projektů EventManager, nástrojů a SpecialParser.</span><span class="sxs-lookup"><span data-stu-id="6ab33-122">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="6ab33-123">Vývojář se často používá `Update-Package` příkazu v různých časech s každou z těchto projekty.</span><span class="sxs-lookup"><span data-stu-id="6ab33-123">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="6ab33-124">Jana vyhledá vhodné používat `Update-Package` příkaz zadejte automatické dokončování rozšíření pro `-ProjectName` argument, takže se nemusí na název projektu zadejte pokaždé, když.</span><span class="sxs-lookup"><span data-stu-id="6ab33-124">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="6ab33-125">Následující příkaz, pak zaregistruje názvy těchto tří projektů jako rozšíření pro `-ProjectName` parametr:</span><span class="sxs-lookup"><span data-stu-id="6ab33-125">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="6ab33-126">Vývojář může zadejte `Update-Package -ProjectName `, stiskněte klávesu Tab a rozšíření nabízeny jako možnosti automatického dokončování v tématu:</span><span class="sxs-lookup"><span data-stu-id="6ab33-126">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Příklad použití Register-TabExpansion](media/Register-TabExpansion-Example.png)
