---
title: Příkaz seznamu NuGet rozhraní příkazového řádku
description: Referenční dokumentace pro příkaz nuget.exe seznamu
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b0f144d8abbba7388fe39cd113e4eeddccbca2c6
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818435"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="8920a-103">příkaz seznamu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="8920a-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="8920a-104">**Platí pro:** spotřeba balíčku, publikování &bullet; **podporované verze:** všechny</span><span class="sxs-lookup"><span data-stu-id="8920a-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="8920a-105">Zobrazí seznam balíčků z daného zdroje.</span><span class="sxs-lookup"><span data-stu-id="8920a-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="8920a-106">Pokud nejsou zadány žádné zdroje, všechny zdroje definované v souboru globální konfiguraci `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config`, se používají.</span><span class="sxs-lookup"><span data-stu-id="8920a-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="8920a-107">Pokud `NuGet.Config` žádné zdroje, pak určuje `list` používá výchozí informačního kanálu (nuget.org).</span><span class="sxs-lookup"><span data-stu-id="8920a-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="8920a-108">Použití</span><span class="sxs-lookup"><span data-stu-id="8920a-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="8920a-109">volitelné hledané výrazy, kde bude filtr pro zobrazený seznam.</span><span class="sxs-lookup"><span data-stu-id="8920a-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="8920a-110">Hledaný text se použijí pro názvy balíčků, značky a popisy balíček stejně, jako jsou v případě, že jejich používání v nuget.org.</span><span class="sxs-lookup"><span data-stu-id="8920a-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="8920a-111">Možnosti</span><span class="sxs-lookup"><span data-stu-id="8920a-111">Options</span></span>

| <span data-ttu-id="8920a-112">Možnost</span><span class="sxs-lookup"><span data-stu-id="8920a-112">Option</span></span> | <span data-ttu-id="8920a-113">Popis</span><span class="sxs-lookup"><span data-stu-id="8920a-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8920a-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="8920a-114">AllVersions</span></span> | <span data-ttu-id="8920a-115">Zobrazí seznam všech verze balíčku.</span><span class="sxs-lookup"><span data-stu-id="8920a-115">List all versions of a package.</span></span> <span data-ttu-id="8920a-116">Ve výchozím nastavení se zobrazí jenom nejnovější verzi balíčku.</span><span class="sxs-lookup"><span data-stu-id="8920a-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="8920a-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="8920a-117">ConfigFile</span></span> | <span data-ttu-id="8920a-118">Konfigurační soubor NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="8920a-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="8920a-119">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.</span><span class="sxs-lookup"><span data-stu-id="8920a-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="8920a-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="8920a-120">ForceEnglishOutput</span></span> | <span data-ttu-id="8920a-121">*(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze.</span><span class="sxs-lookup"><span data-stu-id="8920a-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="8920a-122">Nápověda</span><span class="sxs-lookup"><span data-stu-id="8920a-122">Help</span></span> | <span data-ttu-id="8920a-123">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="8920a-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="8920a-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="8920a-124">IncludeDelisted</span></span> | <span data-ttu-id="8920a-125">*(3.2 +)*  Zobrazovat neuvedené balíčky.</span><span class="sxs-lookup"><span data-stu-id="8920a-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="8920a-126">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="8920a-126">NonInteractive</span></span> | <span data-ttu-id="8920a-127">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="8920a-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="8920a-128">Předběžné verze</span><span class="sxs-lookup"><span data-stu-id="8920a-128">PreRelease</span></span> | <span data-ttu-id="8920a-129">Obsahuje předběžné verze balíčků v seznamu.</span><span class="sxs-lookup"><span data-stu-id="8920a-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="8920a-130">Zdroj</span><span class="sxs-lookup"><span data-stu-id="8920a-130">Source</span></span> | <span data-ttu-id="8920a-131">Určuje seznam balíčků zdroje pro vyhledávání.</span><span class="sxs-lookup"><span data-stu-id="8920a-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="8920a-132">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="8920a-132">Verbosity</span></span> | <span data-ttu-id="8920a-133">Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="8920a-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="8920a-134">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="8920a-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="8920a-135">Příklady</span><span class="sxs-lookup"><span data-stu-id="8920a-135">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
