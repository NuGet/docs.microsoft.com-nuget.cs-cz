---
title: Příkaz listovat NuGet rozhraní příkazového řádku
description: Referenční informace pro příkaz seznamu nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549798"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="ecbff-103">příkaz listovat (rozhraní příkazového řádku NuGet)</span><span class="sxs-lookup"><span data-stu-id="ecbff-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="ecbff-104">**Platí pro:** využití balíčků, publikováním &bullet; **podporované verze:** všechny</span><span class="sxs-lookup"><span data-stu-id="ecbff-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="ecbff-105">Zobrazí seznam balíčků z daného zdroje.</span><span class="sxs-lookup"><span data-stu-id="ecbff-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="ecbff-106">Pokud nejsou zadány žádné zdroje, všechny zdroje definované v souboru globální konfiguraci `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config`, se používají.</span><span class="sxs-lookup"><span data-stu-id="ecbff-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="ecbff-107">Pokud `NuGet.Config` žádné zdroje, pak určuje `list` používá výchozí kanál (nuget.org).</span><span class="sxs-lookup"><span data-stu-id="ecbff-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="ecbff-108">Použití</span><span class="sxs-lookup"><span data-stu-id="ecbff-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="ecbff-109">volitelné hledané výrazy ve kterém se filtr pro zobrazený seznam.</span><span class="sxs-lookup"><span data-stu-id="ecbff-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="ecbff-110">Hledané termíny se použijí na názvy balíčků, značky a Popis balíčku, stejně jako při použití na nuget.org.</span><span class="sxs-lookup"><span data-stu-id="ecbff-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="ecbff-111">Možnosti</span><span class="sxs-lookup"><span data-stu-id="ecbff-111">Options</span></span>

| <span data-ttu-id="ecbff-112">Možnost</span><span class="sxs-lookup"><span data-stu-id="ecbff-112">Option</span></span> | <span data-ttu-id="ecbff-113">Popis</span><span class="sxs-lookup"><span data-stu-id="ecbff-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ecbff-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="ecbff-114">AllVersions</span></span> | <span data-ttu-id="ecbff-115">Zobrazí seznam všech verzí balíčku.</span><span class="sxs-lookup"><span data-stu-id="ecbff-115">List all versions of a package.</span></span> <span data-ttu-id="ecbff-116">Ve výchozím nastavení zobrazí se pouze nejnovější verze balíčku.</span><span class="sxs-lookup"><span data-stu-id="ecbff-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="ecbff-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="ecbff-117">ConfigFile</span></span> | <span data-ttu-id="ecbff-118">Konfigurační soubor NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="ecbff-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ecbff-119">Pokud není zadán, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.</span><span class="sxs-lookup"><span data-stu-id="ecbff-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="ecbff-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="ecbff-120">ForceEnglishOutput</span></span> | <span data-ttu-id="ecbff-121">*(3.5 +)*  Vynutí nuget.exe pro spuštění pomocí neutrální, základem je angličtina jazyková verze.</span><span class="sxs-lookup"><span data-stu-id="ecbff-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="ecbff-122">Nápověda</span><span class="sxs-lookup"><span data-stu-id="ecbff-122">Help</span></span> | <span data-ttu-id="ecbff-123">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="ecbff-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="ecbff-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="ecbff-124">IncludeDelisted</span></span> | <span data-ttu-id="ecbff-125">*(3.2 +)*  Zobrazit neuvedené v seznamu balíčků.</span><span class="sxs-lookup"><span data-stu-id="ecbff-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="ecbff-126">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="ecbff-126">NonInteractive</span></span> | <span data-ttu-id="ecbff-127">Potlačí vyzve k zadání uživatele o vstup ani potvrzení.</span><span class="sxs-lookup"><span data-stu-id="ecbff-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="ecbff-128">Platnost předběžné verze</span><span class="sxs-lookup"><span data-stu-id="ecbff-128">PreRelease</span></span> | <span data-ttu-id="ecbff-129">Obsahuje předběžné verze balíčků v seznamu.</span><span class="sxs-lookup"><span data-stu-id="ecbff-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="ecbff-130">Zdroj</span><span class="sxs-lookup"><span data-stu-id="ecbff-130">Source</span></span> | <span data-ttu-id="ecbff-131">Určuje seznam zdrojů balíčků pro hledání.</span><span class="sxs-lookup"><span data-stu-id="ecbff-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="ecbff-132">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="ecbff-132">Verbosity</span></span> | <span data-ttu-id="ecbff-133">Určuje množství podrobností, na které se zobrazí ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="ecbff-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="ecbff-134">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ecbff-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ecbff-135">Příklady</span><span class="sxs-lookup"><span data-stu-id="ecbff-135">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
