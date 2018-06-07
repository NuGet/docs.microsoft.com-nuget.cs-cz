---
title: Příkaz help NuGet rozhraní příkazového řádku
description: Referenční dokumentace pro příkaz nuget.exe nápovědy
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d7112209a0a2a267343c3458ebacaf6b744786a9
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818253"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="79376-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="79376-103">help or ?</span></span> <span data-ttu-id="79376-104">Příkaz (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="79376-104">command (NuGet CLI)</span></span>

<span data-ttu-id="79376-105">**Platí pro:** všechny &bullet; **podporované verze**: všechny</span><span class="sxs-lookup"><span data-stu-id="79376-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="79376-106">Zobrazí obecné pomůže informace a informace o určité příkazy.</span><span class="sxs-lookup"><span data-stu-id="79376-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="79376-107">Použití</span><span class="sxs-lookup"><span data-stu-id="79376-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="79376-108">[příkaz] kde identifikuje konkrétní příkaz pro které chcete zobrazit nápovědu.</span><span class="sxs-lookup"><span data-stu-id="79376-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="79376-109">U některých příkazů, mějte na paměti k určení *pomoci* , jako první se `nuget help install`, protože je balíček s názvem "Nápověda" v nuget.org. Pokud zadáte název příkazu `nuget install help`, nebude získání nápovědy na příkaz instalace, ale místo toho nainstaluje balíček s názvem nápovědy.</span><span class="sxs-lookup"><span data-stu-id="79376-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="79376-110">Možnosti</span><span class="sxs-lookup"><span data-stu-id="79376-110">Options</span></span>

| <span data-ttu-id="79376-111">Možnost</span><span class="sxs-lookup"><span data-stu-id="79376-111">Option</span></span> | <span data-ttu-id="79376-112">Popis</span><span class="sxs-lookup"><span data-stu-id="79376-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="79376-113">Všechny</span><span class="sxs-lookup"><span data-stu-id="79376-113">All</span></span> | <span data-ttu-id="79376-114">Tisk podrobnou nápovědu pro všechny dostupné příkazy; Pokud je zadána konkrétní příkaz ignorována.</span><span class="sxs-lookup"><span data-stu-id="79376-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="79376-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="79376-115">ConfigFile</span></span> | <span data-ttu-id="79376-116">Konfigurační soubor NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="79376-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="79376-117">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.</span><span class="sxs-lookup"><span data-stu-id="79376-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="79376-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="79376-118">ForceEnglishOutput</span></span> | <span data-ttu-id="79376-119">*(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze.</span><span class="sxs-lookup"><span data-stu-id="79376-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="79376-120">Nápověda</span><span class="sxs-lookup"><span data-stu-id="79376-120">Help</span></span> | <span data-ttu-id="79376-121">Zobrazí nápovědu pro příkaz help sám sebe.</span><span class="sxs-lookup"><span data-stu-id="79376-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="79376-122">Markdownu</span><span class="sxs-lookup"><span data-stu-id="79376-122">Markdown</span></span> | <span data-ttu-id="79376-123">Tisk podrobnou nápovědu ve formátu markdown při použití s `-All`.</span><span class="sxs-lookup"><span data-stu-id="79376-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="79376-124">V opačném případě ignorovat.</span><span class="sxs-lookup"><span data-stu-id="79376-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="79376-125">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="79376-125">NonInteractive</span></span> | <span data-ttu-id="79376-126">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="79376-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="79376-127">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="79376-127">Verbosity</span></span> | <span data-ttu-id="79376-128">Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="79376-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="79376-129">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="79376-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="79376-130">Příklady</span><span class="sxs-lookup"><span data-stu-id="79376-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
