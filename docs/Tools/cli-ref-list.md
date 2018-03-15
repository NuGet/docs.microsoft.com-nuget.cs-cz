---
title: "Příkaz seznamu NuGet rozhraní příkazového řádku | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenční dokumentace pro příkaz nuget.exe seznamu"
keywords: "odkaz na seznam nuget, seznam balíčků příkaz"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7e0945b9e64a15a839f62bde0a0ef8f3d83335d4
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2018
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="fdb49-104">příkaz seznamu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="fdb49-104">list command (NuGet CLI)</span></span>

<span data-ttu-id="fdb49-105">**Platí pro:** spotřeba balíčku, publikování &bullet; **podporované verze:** všechny</span><span class="sxs-lookup"><span data-stu-id="fdb49-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="fdb49-106">Zobrazí seznam balíčků z daného zdroje.</span><span class="sxs-lookup"><span data-stu-id="fdb49-106">Displays a list of packages from a given source.</span></span> <span data-ttu-id="fdb49-107">Pokud nejsou zadány žádné zdroje, všechny zdroje definované v souboru globální konfiguraci `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config`, se používají.</span><span class="sxs-lookup"><span data-stu-id="fdb49-107">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="fdb49-108">Pokud `NuGet.Config` žádné zdroje, pak určuje `list` používá výchozí informačního kanálu (nuget.org).</span><span class="sxs-lookup"><span data-stu-id="fdb49-108">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="fdb49-109">Použití</span><span class="sxs-lookup"><span data-stu-id="fdb49-109">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="fdb49-110">volitelné hledané výrazy, kde bude filtr pro zobrazený seznam.</span><span class="sxs-lookup"><span data-stu-id="fdb49-110">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="fdb49-111">Hledaný text se použijí pro názvy balíčků, značky a popisy balíček stejně, jako jsou v případě, že jejich používání v nuget.org.</span><span class="sxs-lookup"><span data-stu-id="fdb49-111">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="fdb49-112">Možnosti</span><span class="sxs-lookup"><span data-stu-id="fdb49-112">Options</span></span>

| <span data-ttu-id="fdb49-113">Možnost</span><span class="sxs-lookup"><span data-stu-id="fdb49-113">Option</span></span> | <span data-ttu-id="fdb49-114">Popis</span><span class="sxs-lookup"><span data-stu-id="fdb49-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fdb49-115">AllVersions</span><span class="sxs-lookup"><span data-stu-id="fdb49-115">AllVersions</span></span> | <span data-ttu-id="fdb49-116">Zobrazí seznam všech verze balíčku.</span><span class="sxs-lookup"><span data-stu-id="fdb49-116">List all versions of a package.</span></span> <span data-ttu-id="fdb49-117">Ve výchozím nastavení se zobrazí jenom nejnovější verzi balíčku.</span><span class="sxs-lookup"><span data-stu-id="fdb49-117">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="fdb49-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="fdb49-118">ConfigFile</span></span> | <span data-ttu-id="fdb49-119">Konfigurační soubor NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="fdb49-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="fdb49-120">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.</span><span class="sxs-lookup"><span data-stu-id="fdb49-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="fdb49-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="fdb49-121">ForceEnglishOutput</span></span> | <span data-ttu-id="fdb49-122">*(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze.</span><span class="sxs-lookup"><span data-stu-id="fdb49-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="fdb49-123">Nápověda</span><span class="sxs-lookup"><span data-stu-id="fdb49-123">Help</span></span> | <span data-ttu-id="fdb49-124">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="fdb49-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="fdb49-125">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="fdb49-125">IncludeDelisted</span></span> | <span data-ttu-id="fdb49-126">*(3.2 +)*  Zobrazovat neuvedené balíčky.</span><span class="sxs-lookup"><span data-stu-id="fdb49-126">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="fdb49-127">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="fdb49-127">NonInteractive</span></span> | <span data-ttu-id="fdb49-128">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="fdb49-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="fdb49-129">Předběžné verze</span><span class="sxs-lookup"><span data-stu-id="fdb49-129">PreRelease</span></span> | <span data-ttu-id="fdb49-130">Obsahuje předběžné verze balíčků v seznamu.</span><span class="sxs-lookup"><span data-stu-id="fdb49-130">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="fdb49-131">Zdroj</span><span class="sxs-lookup"><span data-stu-id="fdb49-131">Source</span></span> | <span data-ttu-id="fdb49-132">Určuje seznam balíčků zdroje pro vyhledávání.</span><span class="sxs-lookup"><span data-stu-id="fdb49-132">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="fdb49-133">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="fdb49-133">Verbosity</span></span> | <span data-ttu-id="fdb49-134">Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="fdb49-134">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="fdb49-135">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="fdb49-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="fdb49-136">Příklady</span><span class="sxs-lookup"><span data-stu-id="fdb49-136">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
