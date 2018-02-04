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
ms.openlocfilehash: 5a1f68aaffd26a0f903aa3a7a4a450a0121191c3
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/02/2018
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="f0f5b-104">příkaz seznamu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="f0f5b-104">list command (NuGet CLI)</span></span>

<span data-ttu-id="f0f5b-105">**Platí pro:** spotřeba balíčku, publikování &bullet; **podporované verze:** všechny</span><span class="sxs-lookup"><span data-stu-id="f0f5b-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="f0f5b-106">Zobrazí seznam balíčků z daného zdroje.</span><span class="sxs-lookup"><span data-stu-id="f0f5b-106">Displays a list of packages from a given source.</span></span> <span data-ttu-id="f0f5b-107">Pokud nejsou zadány žádné zdroje, všechny zdroje definované v souboru globální konfiguraci `%AppData%\NuGet\NuGet.Config`, se používají.</span><span class="sxs-lookup"><span data-stu-id="f0f5b-107">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config`, are used.</span></span> <span data-ttu-id="f0f5b-108">Pokud `NuGet.Config` žádné zdroje, pak určuje `list` používá výchozí informačního kanálu (nuget.org).</span><span class="sxs-lookup"><span data-stu-id="f0f5b-108">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="f0f5b-109">Použití</span><span class="sxs-lookup"><span data-stu-id="f0f5b-109">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="f0f5b-110">volitelné hledané výrazy, kde bude filtr pro zobrazený seznam.</span><span class="sxs-lookup"><span data-stu-id="f0f5b-110">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="f0f5b-111">Hledaný text se použijí pro názvy balíčků, značky a Popis balíčku.</span><span class="sxs-lookup"><span data-stu-id="f0f5b-111">Search terms are applied to the names of packages, tags, and package descriptions.</span></span>

## <a name="options"></a><span data-ttu-id="f0f5b-112">Možnosti</span><span class="sxs-lookup"><span data-stu-id="f0f5b-112">Options</span></span>

| <span data-ttu-id="f0f5b-113">Možnost</span><span class="sxs-lookup"><span data-stu-id="f0f5b-113">Option</span></span> | <span data-ttu-id="f0f5b-114">Popis</span><span class="sxs-lookup"><span data-stu-id="f0f5b-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f0f5b-115">AllVersions</span><span class="sxs-lookup"><span data-stu-id="f0f5b-115">AllVersions</span></span> | <span data-ttu-id="f0f5b-116">Zobrazí seznam všech verze balíčku.</span><span class="sxs-lookup"><span data-stu-id="f0f5b-116">List all versions of a package.</span></span> <span data-ttu-id="f0f5b-117">Ve výchozím nastavení se zobrazí jenom nejnovější verzi balíčku.</span><span class="sxs-lookup"><span data-stu-id="f0f5b-117">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="f0f5b-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f0f5b-118">ConfigFile</span></span> | <span data-ttu-id="f0f5b-119">Konfigurační soubor NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="f0f5b-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="f0f5b-120">Pokud není zadaný, *%AppData%\NuGet\NuGet.Config* se používá.</span><span class="sxs-lookup"><span data-stu-id="f0f5b-120">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="f0f5b-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f0f5b-121">ForceEnglishOutput</span></span> | <span data-ttu-id="f0f5b-122">*(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze.</span><span class="sxs-lookup"><span data-stu-id="f0f5b-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f0f5b-123">Nápověda</span><span class="sxs-lookup"><span data-stu-id="f0f5b-123">Help</span></span> | <span data-ttu-id="f0f5b-124">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="f0f5b-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="f0f5b-125">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="f0f5b-125">IncludeDelisted</span></span> | <span data-ttu-id="f0f5b-126">*(3.2 +)*  Zobrazovat neuvedené balíčky.</span><span class="sxs-lookup"><span data-stu-id="f0f5b-126">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="f0f5b-127">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="f0f5b-127">NonInteractive</span></span> | <span data-ttu-id="f0f5b-128">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="f0f5b-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="f0f5b-129">Předběžné verze</span><span class="sxs-lookup"><span data-stu-id="f0f5b-129">PreRelease</span></span> | <span data-ttu-id="f0f5b-130">Obsahuje předběžné verze balíčků v seznamu.</span><span class="sxs-lookup"><span data-stu-id="f0f5b-130">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="f0f5b-131">Zdroj</span><span class="sxs-lookup"><span data-stu-id="f0f5b-131">Source</span></span> | <span data-ttu-id="f0f5b-132">Určuje seznam balíčků zdroje pro vyhledávání.</span><span class="sxs-lookup"><span data-stu-id="f0f5b-132">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="f0f5b-133">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="f0f5b-133">Verbosity</span></span> | <span data-ttu-id="f0f5b-134">Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="f0f5b-134">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="f0f5b-135">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="f0f5b-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="f0f5b-136">Příklady</span><span class="sxs-lookup"><span data-stu-id="f0f5b-136">Examples</span></span>

```cli
nuget list

nuget list -Verbosity detailed -AllVersions
```
