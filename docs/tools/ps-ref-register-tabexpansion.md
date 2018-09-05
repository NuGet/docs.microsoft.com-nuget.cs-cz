---
title: Referenční informace prostředí PowerShell NuGet Register-TabExpansion
description: Referenční informace pro příkaz Powershellu zaregistrujte TabExpansion v konzole Správce balíčků NuGet v sadě Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 98171c598bd4a3468bd23e2d6060e267c38021b4
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546602"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="18cf8-103">Register-TabExpansion (konzola Správce balíčků v sadě Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="18cf8-103">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="18cf8-104">*K dispozici pouze v rámci [Konzola správce balíčků NuGet](package-manager-console.md) v sadě Visual Studio ve Windows.*</span><span class="sxs-lookup"><span data-stu-id="18cf8-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="18cf8-105">Zaregistruje rozšíření tab pro parametry zadaný příkaz tak, aby při karta se používá při zadání příkazu, rozšířené hodnoty se zobrazí jako dostupné možnosti pro parametr nejistá.</span><span class="sxs-lookup"><span data-stu-id="18cf8-105">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="18cf8-106">Všechny předchozí rozšíření příkazu jsou přepsány.</span><span class="sxs-lookup"><span data-stu-id="18cf8-106">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="18cf8-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="18cf8-107">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="18cf8-108">Parametry</span><span class="sxs-lookup"><span data-stu-id="18cf8-108">Parameters</span></span>

| <span data-ttu-id="18cf8-109">Parametr</span><span class="sxs-lookup"><span data-stu-id="18cf8-109">Parameter</span></span> | <span data-ttu-id="18cf8-110">Popis</span><span class="sxs-lookup"><span data-stu-id="18cf8-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="18cf8-111">Název</span><span class="sxs-lookup"><span data-stu-id="18cf8-111">Name</span></span> | <span data-ttu-id="18cf8-112">(Povinné) Příkaz pro registraci rozšíření.</span><span class="sxs-lookup"><span data-stu-id="18cf8-112">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="18cf8-113">-Název je volitelný přepínač samotný.</span><span class="sxs-lookup"><span data-stu-id="18cf8-113">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="18cf8-114">Definice</span><span class="sxs-lookup"><span data-stu-id="18cf8-114">Definition</span></span> | <span data-ttu-id="18cf8-115">(Povinné) Objekt popisující argument v syntaxi `@{'<parameter>' = {'<value1>', '<value2>', ...}}` kde `<parameter>` je název parametru k úpravě a každý `<value>` poskytuje konkrétní rozšíření.</span><span class="sxs-lookup"><span data-stu-id="18cf8-115">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="18cf8-116">Jednoduché i dvojité uvozovky jsou přijaty.</span><span class="sxs-lookup"><span data-stu-id="18cf8-116">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="18cf8-117">Žádná z těchto parametrů přijímat kanálu vstup nebo zástupné znaky.</span><span class="sxs-lookup"><span data-stu-id="18cf8-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="18cf8-118">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="18cf8-118">Common Parameters</span></span>

<span data-ttu-id="18cf8-119">`Register-TabExpansion` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="18cf8-119">`Register-TabExpansion` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="18cf8-120">Příklady</span><span class="sxs-lookup"><span data-stu-id="18cf8-120">Examples</span></span>

<span data-ttu-id="18cf8-121">Vezměte v úvahu řešení, které obsahuje tři projekty názvy EventManager, nástroje a SpecialParser.</span><span class="sxs-lookup"><span data-stu-id="18cf8-121">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="18cf8-122">Vývojář se často používá `Update-Package` příkaz v různých časech s každým z těchto projektech.</span><span class="sxs-lookup"><span data-stu-id="18cf8-122">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="18cf8-123">Vyhledá je výhodné mít `Update-Package` příkaz poskytují rozšíření automatické dokončování pro `-ProjectName` argument, takže nepotřebuje zadejte název projektu pokaždé, když.</span><span class="sxs-lookup"><span data-stu-id="18cf8-123">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="18cf8-124">Následující příkaz, pak zaregistruje jako rozšíření pro názvy těchto tří projektů `-ProjectName` parametr:</span><span class="sxs-lookup"><span data-stu-id="18cf8-124">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="18cf8-125">Vývojář potom můžete zadat `Update-Package -ProjectName `, stiskněte klávesu Tab a zobrazit rozšíření nabízeny jako možnosti automatického dokončování:</span><span class="sxs-lookup"><span data-stu-id="18cf8-125">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Příklad použití TabExpansion registru](media/Register-TabExpansion-Example.png)
