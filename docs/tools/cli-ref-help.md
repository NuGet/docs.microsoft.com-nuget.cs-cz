---
title: Příkaz help NuGet rozhraní příkazového řádku
description: Referenční informace pro příkaz help nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546560"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="83dda-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="83dda-103">help or ?</span></span> <span data-ttu-id="83dda-104">Příkaz (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="83dda-104">command (NuGet CLI)</span></span>

<span data-ttu-id="83dda-105">**Platí pro:** všechny &bullet; **podporované verze**: všechny</span><span class="sxs-lookup"><span data-stu-id="83dda-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="83dda-106">Zobrazí obecné pomůže informace a informace o konkrétní příkazy.</span><span class="sxs-lookup"><span data-stu-id="83dda-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="83dda-107">Použití</span><span class="sxs-lookup"><span data-stu-id="83dda-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="83dda-108">kde [příkaz] označuje ke konkrétnímu příkazu, pro které chcete zobrazit nápovědu.</span><span class="sxs-lookup"><span data-stu-id="83dda-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="83dda-109">U některých příkazů, mějte k určení *pomáhají* , jako první se `nuget help install`, protože je balíček s názvem "Nápověda" na nuget.org. Pokud dáte příkaz `nuget install help`, nebude získat pomoc na instalačního příkazu, ale místo toho nainstaluje balíček s názvem nápovědy.</span><span class="sxs-lookup"><span data-stu-id="83dda-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="83dda-110">Možnosti</span><span class="sxs-lookup"><span data-stu-id="83dda-110">Options</span></span>

| <span data-ttu-id="83dda-111">Možnost</span><span class="sxs-lookup"><span data-stu-id="83dda-111">Option</span></span> | <span data-ttu-id="83dda-112">Popis</span><span class="sxs-lookup"><span data-stu-id="83dda-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="83dda-113">Všechny</span><span class="sxs-lookup"><span data-stu-id="83dda-113">All</span></span> | <span data-ttu-id="83dda-114">Tisk podrobnou nápovědu pro všechny dostupné příkazy. ignoruje, pokud je zadána ke konkrétnímu příkazu.</span><span class="sxs-lookup"><span data-stu-id="83dda-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="83dda-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="83dda-115">ConfigFile</span></span> | <span data-ttu-id="83dda-116">Konfigurační soubor NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="83dda-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="83dda-117">Pokud není zadán, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.</span><span class="sxs-lookup"><span data-stu-id="83dda-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="83dda-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="83dda-118">ForceEnglishOutput</span></span> | <span data-ttu-id="83dda-119">*(3.5 +)*  Vynutí nuget.exe pro spuštění pomocí neutrální, základem je angličtina jazyková verze.</span><span class="sxs-lookup"><span data-stu-id="83dda-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="83dda-120">Nápověda</span><span class="sxs-lookup"><span data-stu-id="83dda-120">Help</span></span> | <span data-ttu-id="83dda-121">Zobrazí nápovědu pro příkaz help, samotného.</span><span class="sxs-lookup"><span data-stu-id="83dda-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="83dda-122">Markdown</span><span class="sxs-lookup"><span data-stu-id="83dda-122">Markdown</span></span> | <span data-ttu-id="83dda-123">Tisk podrobnou nápovědu ve formátu markdown zadáním `-All`.</span><span class="sxs-lookup"><span data-stu-id="83dda-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="83dda-124">Jinak ignorována.</span><span class="sxs-lookup"><span data-stu-id="83dda-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="83dda-125">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="83dda-125">NonInteractive</span></span> | <span data-ttu-id="83dda-126">Potlačí vyzve k zadání uživatele o vstup ani potvrzení.</span><span class="sxs-lookup"><span data-stu-id="83dda-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="83dda-127">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="83dda-127">Verbosity</span></span> | <span data-ttu-id="83dda-128">Určuje množství podrobností, na které se zobrazí ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="83dda-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="83dda-129">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="83dda-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="83dda-130">Příklady</span><span class="sxs-lookup"><span data-stu-id="83dda-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
