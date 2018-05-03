---
title: Příkaz seznamu NuGet rozhraní příkazového řádku
description: Referenční dokumentace pro příkaz nuget.exe seznamu
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f4a44c70937e7cb49e472c53e9857e9f44d269f7
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="45019-103">příkaz seznamu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="45019-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="45019-104">**Platí pro:** spotřeba balíčku, publikování &bullet; **podporované verze:** všechny</span><span class="sxs-lookup"><span data-stu-id="45019-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="45019-105">Zobrazí seznam balíčků z daného zdroje.</span><span class="sxs-lookup"><span data-stu-id="45019-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="45019-106">Pokud nejsou zadány žádné zdroje, všechny zdroje definované v souboru globální konfiguraci `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config`, se používají.</span><span class="sxs-lookup"><span data-stu-id="45019-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="45019-107">Pokud `NuGet.Config` žádné zdroje, pak určuje `list` používá výchozí informačního kanálu (nuget.org).</span><span class="sxs-lookup"><span data-stu-id="45019-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="45019-108">Použití</span><span class="sxs-lookup"><span data-stu-id="45019-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="45019-109">volitelné hledané výrazy, kde bude filtr pro zobrazený seznam.</span><span class="sxs-lookup"><span data-stu-id="45019-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="45019-110">Hledaný text se použijí pro názvy balíčků, značky a popisy balíček stejně, jako jsou v případě, že jejich používání v nuget.org.</span><span class="sxs-lookup"><span data-stu-id="45019-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="45019-111">Možnosti</span><span class="sxs-lookup"><span data-stu-id="45019-111">Options</span></span>

| <span data-ttu-id="45019-112">Možnost</span><span class="sxs-lookup"><span data-stu-id="45019-112">Option</span></span> | <span data-ttu-id="45019-113">Popis</span><span class="sxs-lookup"><span data-stu-id="45019-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="45019-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="45019-114">AllVersions</span></span> | <span data-ttu-id="45019-115">Zobrazí seznam všech verze balíčku.</span><span class="sxs-lookup"><span data-stu-id="45019-115">List all versions of a package.</span></span> <span data-ttu-id="45019-116">Ve výchozím nastavení se zobrazí jenom nejnovější verzi balíčku.</span><span class="sxs-lookup"><span data-stu-id="45019-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="45019-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="45019-117">ConfigFile</span></span> | <span data-ttu-id="45019-118">Konfigurační soubor NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="45019-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="45019-119">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.</span><span class="sxs-lookup"><span data-stu-id="45019-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="45019-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="45019-120">ForceEnglishOutput</span></span> | <span data-ttu-id="45019-121">*(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze.</span><span class="sxs-lookup"><span data-stu-id="45019-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="45019-122">Nápověda</span><span class="sxs-lookup"><span data-stu-id="45019-122">Help</span></span> | <span data-ttu-id="45019-123">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="45019-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="45019-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="45019-124">IncludeDelisted</span></span> | <span data-ttu-id="45019-125">*(3.2 +)*  Zobrazovat neuvedené balíčky.</span><span class="sxs-lookup"><span data-stu-id="45019-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="45019-126">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="45019-126">NonInteractive</span></span> | <span data-ttu-id="45019-127">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="45019-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="45019-128">Předběžné verze</span><span class="sxs-lookup"><span data-stu-id="45019-128">PreRelease</span></span> | <span data-ttu-id="45019-129">Obsahuje předběžné verze balíčků v seznamu.</span><span class="sxs-lookup"><span data-stu-id="45019-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="45019-130">Zdroj</span><span class="sxs-lookup"><span data-stu-id="45019-130">Source</span></span> | <span data-ttu-id="45019-131">Určuje seznam balíčků zdroje pro vyhledávání.</span><span class="sxs-lookup"><span data-stu-id="45019-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="45019-132">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="45019-132">Verbosity</span></span> | <span data-ttu-id="45019-133">Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="45019-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="45019-134">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="45019-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="45019-135">Příklady</span><span class="sxs-lookup"><span data-stu-id="45019-135">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
