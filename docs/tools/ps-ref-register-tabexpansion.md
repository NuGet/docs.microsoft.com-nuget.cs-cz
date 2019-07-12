---
title: Referenční informace prostředí PowerShell NuGet Register-TabExpansion
description: Referenční informace pro příkaz Powershellu zaregistrujte TabExpansion v konzole Správce balíčků NuGet v sadě Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8adb80af85e2e32fa8c35e5272cf90ff0c0ddcbb
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842486"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="9cd74-103">Register-TabExpansion (konzola Správce balíčků v sadě Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="9cd74-103">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="9cd74-104">*K dispozici pouze v rámci [Konzola správce balíčků](package-manager-console.md) v sadě Visual Studio ve Windows.*</span><span class="sxs-lookup"><span data-stu-id="9cd74-104">*Available only within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="9cd74-105">Zaregistruje rozšíření tab pro parametry zadaný příkaz tak, aby při karta se používá při zadání příkazu, rozšířené hodnoty se zobrazí jako dostupné možnosti pro parametr nejistá.</span><span class="sxs-lookup"><span data-stu-id="9cd74-105">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="9cd74-106">Všechny předchozí rozšíření příkazu jsou přepsány.</span><span class="sxs-lookup"><span data-stu-id="9cd74-106">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="9cd74-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="9cd74-107">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="9cd74-108">Parametry</span><span class="sxs-lookup"><span data-stu-id="9cd74-108">Parameters</span></span>

| <span data-ttu-id="9cd74-109">Parametr</span><span class="sxs-lookup"><span data-stu-id="9cd74-109">Parameter</span></span> | <span data-ttu-id="9cd74-110">Popis</span><span class="sxs-lookup"><span data-stu-id="9cd74-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9cd74-111">Name</span><span class="sxs-lookup"><span data-stu-id="9cd74-111">Name</span></span> | <span data-ttu-id="9cd74-112">(Povinné) Příkaz pro registraci rozšíření.</span><span class="sxs-lookup"><span data-stu-id="9cd74-112">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="9cd74-113">-Název je volitelný přepínač samotný.</span><span class="sxs-lookup"><span data-stu-id="9cd74-113">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="9cd74-114">Definice</span><span class="sxs-lookup"><span data-stu-id="9cd74-114">Definition</span></span> | <span data-ttu-id="9cd74-115">(Povinné) Objekt popisující argument v syntaxi `@{'<parameter>' = {'<value1>', '<value2>', ...}}` kde `<parameter>` je název parametru k úpravě a každý `<value>` poskytuje konkrétní rozšíření.</span><span class="sxs-lookup"><span data-stu-id="9cd74-115">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="9cd74-116">Jednoduché i dvojité uvozovky jsou přijaty.</span><span class="sxs-lookup"><span data-stu-id="9cd74-116">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="9cd74-117">Žádná z těchto parametrů přijímat kanálu vstup nebo zástupné znaky.</span><span class="sxs-lookup"><span data-stu-id="9cd74-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="9cd74-118">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="9cd74-118">Common Parameters</span></span>

<span data-ttu-id="9cd74-119">`Register-TabExpansion` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="9cd74-119">`Register-TabExpansion` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="9cd74-120">Příklady</span><span class="sxs-lookup"><span data-stu-id="9cd74-120">Examples</span></span>

<span data-ttu-id="9cd74-121">Vezměte v úvahu řešení, které obsahuje tři projekty názvy EventManager, nástroje a SpecialParser.</span><span class="sxs-lookup"><span data-stu-id="9cd74-121">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="9cd74-122">Vývojář se často používá `Update-Package` příkaz v různých časech s každým z těchto projektech.</span><span class="sxs-lookup"><span data-stu-id="9cd74-122">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="9cd74-123">Vyhledá je výhodné mít `Update-Package` příkaz poskytují rozšíření automatické dokončování pro `-ProjectName` argument, takže nepotřebuje zadejte název projektu pokaždé, když.</span><span class="sxs-lookup"><span data-stu-id="9cd74-123">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="9cd74-124">Následující příkaz, pak zaregistruje jako rozšíření pro názvy těchto tří projektů `-ProjectName` parametr:</span><span class="sxs-lookup"><span data-stu-id="9cd74-124">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="9cd74-125">Vývojář potom můžete zadat `Update-Package -ProjectName `, stiskněte klávesu Tab a zobrazit rozšíření nabízeny jako možnosti automatického dokončování:</span><span class="sxs-lookup"><span data-stu-id="9cd74-125">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Příklad použití TabExpansion registru](media/Register-TabExpansion-Example.png)
