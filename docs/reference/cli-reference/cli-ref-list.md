---
title: Seznam CLI NuGet – příkaz
description: Reference k příkazu NuGet. exe list
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328324"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="2bbb0-103">list – příkaz (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="2bbb0-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="2bbb0-104">**Platí pro:** spotřeba balíčku, publikování &bullet; **podporovaných verzí:** vše</span><span class="sxs-lookup"><span data-stu-id="2bbb0-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="2bbb0-105">Zobrazí seznam balíčků z daného zdroje.</span><span class="sxs-lookup"><span data-stu-id="2bbb0-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="2bbb0-106">Pokud nejsou zadány žádné zdroje, budou použity všechny zdroje definované v globálním konfiguračním `%AppData%\NuGet\NuGet.Config` souboru (Windows) `~/.nuget/NuGet/NuGet.Config`nebo.</span><span class="sxs-lookup"><span data-stu-id="2bbb0-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="2bbb0-107">Pokud `NuGet.Config` neurčuje žádné zdroje `list` , použije výchozí kanál (NuGet.org).</span><span class="sxs-lookup"><span data-stu-id="2bbb0-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="2bbb0-108">Použití</span><span class="sxs-lookup"><span data-stu-id="2bbb0-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="2bbb0-109">kde volitelné hledané výrazy budou filtrovat zobrazený seznam.</span><span class="sxs-lookup"><span data-stu-id="2bbb0-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="2bbb0-110">Hledané výrazy se aplikují na názvy balíčků, značek a popisů balíčků stejně jako při jejich použití v nuget.org.</span><span class="sxs-lookup"><span data-stu-id="2bbb0-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="2bbb0-111">Možnosti</span><span class="sxs-lookup"><span data-stu-id="2bbb0-111">Options</span></span>

| <span data-ttu-id="2bbb0-112">Možnost</span><span class="sxs-lookup"><span data-stu-id="2bbb0-112">Option</span></span> | <span data-ttu-id="2bbb0-113">Popis</span><span class="sxs-lookup"><span data-stu-id="2bbb0-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2bbb0-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="2bbb0-114">AllVersions</span></span> | <span data-ttu-id="2bbb0-115">Zobrazí seznam všech verzí balíčku.</span><span class="sxs-lookup"><span data-stu-id="2bbb0-115">List all versions of a package.</span></span> <span data-ttu-id="2bbb0-116">Ve výchozím nastavení se zobrazí pouze nejnovější verze balíčku.</span><span class="sxs-lookup"><span data-stu-id="2bbb0-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="2bbb0-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="2bbb0-117">ConfigFile</span></span> | <span data-ttu-id="2bbb0-118">Konfigurační soubor NuGet, který se má použít</span><span class="sxs-lookup"><span data-stu-id="2bbb0-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="2bbb0-119">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows `~/.nuget/NuGet/NuGet.Config` ) nebo (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="2bbb0-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="2bbb0-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="2bbb0-120">ForceEnglishOutput</span></span> | <span data-ttu-id="2bbb0-121">*(3.5 +)* Vynutí, aby soubor NuGet. exe běžel pomocí neutrální jazykové verze určené pro angličtinu.</span><span class="sxs-lookup"><span data-stu-id="2bbb0-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="2bbb0-122">Help</span><span class="sxs-lookup"><span data-stu-id="2bbb0-122">Help</span></span> | <span data-ttu-id="2bbb0-123">Zobrazí informace o nápovědě k příkazu.</span><span class="sxs-lookup"><span data-stu-id="2bbb0-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="2bbb0-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="2bbb0-124">IncludeDelisted</span></span> | <span data-ttu-id="2bbb0-125">*(3.2 +)* Zobrazí neuvedené balíčky.</span><span class="sxs-lookup"><span data-stu-id="2bbb0-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="2bbb0-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="2bbb0-126">NonInteractive</span></span> | <span data-ttu-id="2bbb0-127">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="2bbb0-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="2bbb0-128">Předběžné verze</span><span class="sxs-lookup"><span data-stu-id="2bbb0-128">PreRelease</span></span> | <span data-ttu-id="2bbb0-129">Obsahuje předběžné verze balíčků v seznamu.</span><span class="sxs-lookup"><span data-stu-id="2bbb0-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="2bbb0-130">Source</span><span class="sxs-lookup"><span data-stu-id="2bbb0-130">Source</span></span> | <span data-ttu-id="2bbb0-131">Určuje seznam zdrojů balíčků, které se mají hledat.</span><span class="sxs-lookup"><span data-stu-id="2bbb0-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="2bbb0-132">Verbosity</span><span class="sxs-lookup"><span data-stu-id="2bbb0-132">Verbosity</span></span> | <span data-ttu-id="2bbb0-133">Určuje množství podrobností zobrazených ve výstupu: *normální*, tiché a *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="2bbb0-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="2bbb0-134">Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="2bbb0-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="2bbb0-135">Příklady</span><span class="sxs-lookup"><span data-stu-id="2bbb0-135">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
