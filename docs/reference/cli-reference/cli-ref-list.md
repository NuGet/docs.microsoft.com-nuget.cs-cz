---
title: Seznam CLI NuGet – příkaz
description: Reference k příkazu NuGet. exe list
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94228521b3be85277990bca2da69518b7070bbdf
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813335"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="6eb83-103">list – příkaz (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="6eb83-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="6eb83-104">**Platí pro:** spotřeba balíčku, publikování &bullet; **podporovaných verzích:** vše</span><span class="sxs-lookup"><span data-stu-id="6eb83-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="6eb83-105">Zobrazí seznam balíčků z daného zdroje.</span><span class="sxs-lookup"><span data-stu-id="6eb83-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="6eb83-106">Pokud nejsou zadány žádné zdroje, budou použity všechny zdroje definované v globálním konfiguračním souboru `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config`.</span><span class="sxs-lookup"><span data-stu-id="6eb83-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="6eb83-107">Pokud `NuGet.Config` neurčuje žádné zdroje, `list` použije výchozí kanál (nuget.org).</span><span class="sxs-lookup"><span data-stu-id="6eb83-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="6eb83-108">Použití</span><span class="sxs-lookup"><span data-stu-id="6eb83-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="6eb83-109">kde volitelné hledané výrazy budou filtrovat zobrazený seznam.</span><span class="sxs-lookup"><span data-stu-id="6eb83-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="6eb83-110">Hledané výrazy se aplikují na názvy balíčků, značek a popisů balíčků stejně jako při jejich použití v nuget.org.</span><span class="sxs-lookup"><span data-stu-id="6eb83-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="6eb83-111">Možnosti</span><span class="sxs-lookup"><span data-stu-id="6eb83-111">Options</span></span>

| <span data-ttu-id="6eb83-112">Možnost</span><span class="sxs-lookup"><span data-stu-id="6eb83-112">Option</span></span> | <span data-ttu-id="6eb83-113">Popis</span><span class="sxs-lookup"><span data-stu-id="6eb83-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6eb83-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="6eb83-114">AllVersions</span></span> | <span data-ttu-id="6eb83-115">Zobrazí seznam všech verzí balíčku.</span><span class="sxs-lookup"><span data-stu-id="6eb83-115">List all versions of a package.</span></span> <span data-ttu-id="6eb83-116">Ve výchozím nastavení se zobrazí pouze nejnovější verze balíčku.</span><span class="sxs-lookup"><span data-stu-id="6eb83-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="6eb83-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="6eb83-117">ConfigFile</span></span> | <span data-ttu-id="6eb83-118">Konfigurační soubor NuGet, který se má použít</span><span class="sxs-lookup"><span data-stu-id="6eb83-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="6eb83-119">Pokud není zadaný, použije se `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="6eb83-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="6eb83-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="6eb83-120">ForceEnglishOutput</span></span> | <span data-ttu-id="6eb83-121">*(3.5 +)* Vynutí, aby soubor NuGet. exe běžel pomocí neutrální jazykové verze určené pro angličtinu.</span><span class="sxs-lookup"><span data-stu-id="6eb83-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="6eb83-122">Nápověda</span><span class="sxs-lookup"><span data-stu-id="6eb83-122">Help</span></span> | <span data-ttu-id="6eb83-123">Zobrazí informace o nápovědě k příkazu.</span><span class="sxs-lookup"><span data-stu-id="6eb83-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="6eb83-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="6eb83-124">IncludeDelisted</span></span> | <span data-ttu-id="6eb83-125">*(3.2 +)* Zobrazí neuvedené balíčky.</span><span class="sxs-lookup"><span data-stu-id="6eb83-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="6eb83-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="6eb83-126">NonInteractive</span></span> | <span data-ttu-id="6eb83-127">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="6eb83-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="6eb83-128">PreRelease</span><span class="sxs-lookup"><span data-stu-id="6eb83-128">PreRelease</span></span> | <span data-ttu-id="6eb83-129">Obsahuje předběžné verze balíčků v seznamu.</span><span class="sxs-lookup"><span data-stu-id="6eb83-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="6eb83-130">Zdroj</span><span class="sxs-lookup"><span data-stu-id="6eb83-130">Source</span></span> | <span data-ttu-id="6eb83-131">Určuje seznam zdrojů balíčků, které se mají hledat.</span><span class="sxs-lookup"><span data-stu-id="6eb83-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="6eb83-132">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="6eb83-132">Verbosity</span></span> | <span data-ttu-id="6eb83-133">Určuje množství podrobností zobrazených ve výstupu: *normální*, *tiché*a *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="6eb83-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="6eb83-134">Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="6eb83-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="6eb83-135">Příklady</span><span class="sxs-lookup"><span data-stu-id="6eb83-135">Examples</span></span>

<span data-ttu-id="6eb83-136">Vypsat všechny balíčky z nakonfigurovaných informačních kanálů:</span><span class="sxs-lookup"><span data-stu-id="6eb83-136">List all packages from configured feeds:</span></span>
```
nuget list
```
<span data-ttu-id="6eb83-137">Seznamte se s podrobnými podrobnostmi pro balíčky související s Azure:</span><span class="sxs-lookup"><span data-stu-id="6eb83-137">List Azure-related packages with detailed verbosity:</span></span>
```
nuget list Azure -Verbosity detailed
```
<span data-ttu-id="6eb83-138">Vypíše všechny verze balíčků souvisejících s Azure z nakonfigurovaných informačních kanálů:</span><span class="sxs-lookup"><span data-stu-id="6eb83-138">List all versions of Azure-related packages from configured feeds:</span></span>
```
nuget list Azure -AllVersions
```
<span data-ttu-id="6eb83-139">Vypíše všechny verze balíčků souvisejících s JSON ze zadaného zdroje nebo kanálu:</span><span class="sxs-lookup"><span data-stu-id="6eb83-139">List all versions of JSON-related packages from specified source/feed:</span></span>
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
<span data-ttu-id="6eb83-140">Vypíše balíčky související s JSON z několika zdrojů nebo kanálů:</span><span class="sxs-lookup"><span data-stu-id="6eb83-140">List JSON-related packages from multiple sources/feeds:</span></span>
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```

