---
title: Reference k NuGet Find-Package PowerShellu
description: Referenční informace k příkazu Find-Package PowerShellu v konzole správce balíčků NuGet v aplikaci Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 263835da64340a13737b32ab54ab057cb640a080
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901756"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="4a7f8-103">Find-Package (konzola správce balíčků v aplikaci Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="4a7f8-103">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="4a7f8-104">*Verze 3.0 +; Toto téma popisuje příkaz v [konzole správce balíčků](../../consume-packages/install-use-packages-powershell.md) v sadě Visual Studio ve Windows. Obecný příkaz Find-Package PowerShellu najdete v [referenčních informacích k PowerShellu PackageManagement](/powershell/module/packagemanagement).*</span><span class="sxs-lookup"><span data-stu-id="4a7f8-104">*Version 3.0+; this topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement).*</span></span>

<span data-ttu-id="4a7f8-105">Získá sadu vzdálených balíčků se zadaným ID nebo klíčovými slovy ze zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="4a7f8-105">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="4a7f8-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="4a7f8-106">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="4a7f8-107">Parametry</span><span class="sxs-lookup"><span data-stu-id="4a7f8-107">Parameters</span></span>

| <span data-ttu-id="4a7f8-108">Parametr</span><span class="sxs-lookup"><span data-stu-id="4a7f8-108">Parameter</span></span> | <span data-ttu-id="4a7f8-109">Popis</span><span class="sxs-lookup"><span data-stu-id="4a7f8-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4a7f8-110">&lt;Klíčová slova ID&gt;</span><span class="sxs-lookup"><span data-stu-id="4a7f8-110">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="4a7f8-111">Požadovanou Klíčová slova, která se mají použít při vyhledávání zdroje balíčku</span><span class="sxs-lookup"><span data-stu-id="4a7f8-111">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="4a7f8-112">Pomocí parametru-ExactMatch můžete vracet pouze ty balíčky, jejichž ID balíčku odpovídá klíčovým slovům.</span><span class="sxs-lookup"><span data-stu-id="4a7f8-112">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="4a7f8-113">Pokud nejsou zadána žádná klíčová slova, `Find-Package` vrátí seznam prvních 20 balíčků ke stažení nebo číslo určené parametrem-First.</span><span class="sxs-lookup"><span data-stu-id="4a7f8-113">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="4a7f8-114">Všimněte si, že-ID je volitelné a no-op.</span><span class="sxs-lookup"><span data-stu-id="4a7f8-114">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="4a7f8-115">Zdroj</span><span class="sxs-lookup"><span data-stu-id="4a7f8-115">Source</span></span> | <span data-ttu-id="4a7f8-116">Adresa URL nebo cesta ke složce pro zdroj balíčku, který má být prohledán.</span><span class="sxs-lookup"><span data-stu-id="4a7f8-116">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="4a7f8-117">Cesty k místní složce můžou být absolutní nebo relativní vzhledem k aktuální složce.</span><span class="sxs-lookup"><span data-stu-id="4a7f8-117">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="4a7f8-118">Pokud tento parametr vynecháte, `Find-Package` vyhledá aktuálně vybraný zdroj balíčku.</span><span class="sxs-lookup"><span data-stu-id="4a7f8-118">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="4a7f8-119">AllVersions</span><span class="sxs-lookup"><span data-stu-id="4a7f8-119">AllVersions</span></span> | <span data-ttu-id="4a7f8-120">Zobrazí všechny dostupné verze jednotlivých balíčků, nikoli jenom nejnovější verzi.</span><span class="sxs-lookup"><span data-stu-id="4a7f8-120">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="4a7f8-121">První</span><span class="sxs-lookup"><span data-stu-id="4a7f8-121">First</span></span> | <span data-ttu-id="4a7f8-122">Počet balíčků, které mají být vráceny od začátku seznamu; Výchozí hodnota je 20.</span><span class="sxs-lookup"><span data-stu-id="4a7f8-122">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="4a7f8-123">Přeskočit</span><span class="sxs-lookup"><span data-stu-id="4a7f8-123">Skip</span></span> | <span data-ttu-id="4a7f8-124">Vynechává první celočíselné &lt; &gt; balíčky ze zobrazeného seznamu.</span><span class="sxs-lookup"><span data-stu-id="4a7f8-124">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="4a7f8-125">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="4a7f8-125">IncludePrerelease</span></span> | <span data-ttu-id="4a7f8-126">Zahrnuje předběžné verze balíčků ve výsledcích.</span><span class="sxs-lookup"><span data-stu-id="4a7f8-126">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="4a7f8-127">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="4a7f8-127">ExactMatch</span></span> | <span data-ttu-id="4a7f8-128">Určili jste použití &lt; klíčových slov &gt; jako ID balíčku s rozlišováním velkých a malých písmen.</span><span class="sxs-lookup"><span data-stu-id="4a7f8-128">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="4a7f8-129">StartWith</span><span class="sxs-lookup"><span data-stu-id="4a7f8-129">StartWith</span></span> | <span data-ttu-id="4a7f8-130">Vrátí balíčky, jejichž ID balíčku začíná &lt; klíčovými slovy &gt; .</span><span class="sxs-lookup"><span data-stu-id="4a7f8-130">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="4a7f8-131">Žádný z těchto parametrů nepřijímají vstupní ani zástupné znaky kanálu.</span><span class="sxs-lookup"><span data-stu-id="4a7f8-131">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="4a7f8-132">Společné parametry</span><span class="sxs-lookup"><span data-stu-id="4a7f8-132">Common Parameters</span></span>

<span data-ttu-id="4a7f8-133">`Find-Package` podporuje následující [běžné parametry PowerShellu](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, inbuffer, subvariable, PipelineVariable, verbose, WarningAction a WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="4a7f8-133">`Find-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="4a7f8-134">Příklady</span><span class="sxs-lookup"><span data-stu-id="4a7f8-134">Examples</span></span>

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```