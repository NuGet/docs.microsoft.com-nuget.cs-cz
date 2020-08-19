---
title: Seznam CLI NuGet – příkaz
description: Referenční informace pro příkaz nuget.exe list
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 91886dbbdcdb24648289d6f6efbe1f87e4099fff
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623068"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="43567-103">list – příkaz (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="43567-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="43567-104">**Platí pro:** spotřeba balíčku, publikování &bullet; **podporovaných verzí:** vše</span><span class="sxs-lookup"><span data-stu-id="43567-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="43567-105">Zobrazí seznam balíčků z daného zdroje.</span><span class="sxs-lookup"><span data-stu-id="43567-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="43567-106">Pokud nejsou zadány žádné zdroje, budou použity všechny zdroje definované v globálním konfiguračním souboru `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` .</span><span class="sxs-lookup"><span data-stu-id="43567-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="43567-107">Pokud `NuGet.Config` neurčuje žádné zdroje, `list` použije výchozí kanál (NuGet.org).</span><span class="sxs-lookup"><span data-stu-id="43567-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="43567-108">Využití</span><span class="sxs-lookup"><span data-stu-id="43567-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="43567-109">kde volitelné hledané výrazy budou filtrovat zobrazený seznam.</span><span class="sxs-lookup"><span data-stu-id="43567-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="43567-110">[Hledané výrazy](/nuget/consume-packages/finding-and-choosing-packages#search-syntax) se aplikují na názvy balíčků, značek a popisů balíčků stejně jako při jejich použití v NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="43567-110">[Search terms](/nuget/consume-packages/finding-and-choosing-packages#search-syntax) are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span> 

## <a name="options"></a><span data-ttu-id="43567-111">Možnosti</span><span class="sxs-lookup"><span data-stu-id="43567-111">Options</span></span>

- **`-AllVersions`**

  <span data-ttu-id="43567-112">Zobrazí seznam všech verzí balíčku.</span><span class="sxs-lookup"><span data-stu-id="43567-112">List all versions of a package.</span></span> <span data-ttu-id="43567-113">Ve výchozím nastavení se zobrazí pouze nejnovější verze balíčku.</span><span class="sxs-lookup"><span data-stu-id="43567-113">By default, only the latest package version is displayed.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="43567-114">Konfigurační soubor NuGet, který se má použít</span><span class="sxs-lookup"><span data-stu-id="43567-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="43567-115">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows) nebo `~/.nuget/NuGet/NuGet.Config` nebo `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="43567-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="43567-116">*(3.5 +)* Vynutí spuštění nuget.exe s využitím neutrální jazykové verze založené na angličtině.</span><span class="sxs-lookup"><span data-stu-id="43567-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="43567-117">Zobrazí informace o nápovědě k příkazu.</span><span class="sxs-lookup"><span data-stu-id="43567-117">Displays help information for the command.</span></span>

- **`-IncludeDelisted`**

  <span data-ttu-id="43567-118">*(3.2 +)* Zobrazí neuvedené balíčky.</span><span class="sxs-lookup"><span data-stu-id="43567-118">*(3.2+)* Display unlisted packages.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="43567-119">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="43567-119">Suppresses prompts for user input or confirmations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="43567-120">Obsahuje předběžné verze balíčků v seznamu.</span><span class="sxs-lookup"><span data-stu-id="43567-120">Includes prerelease packages in the list.</span></span>

- **`-Source`**

  <span data-ttu-id="43567-121">Určuje seznam zdrojů balíčků, které se mají hledat.</span><span class="sxs-lookup"><span data-stu-id="43567-121">Specifies a list of packages sources to search.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="43567-122">Určuje množství podrobností zobrazených ve výstupu: `normal` (výchozí), `quiet` nebo `detailed` .</span><span class="sxs-lookup"><span data-stu-id="43567-122">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="43567-123">Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="43567-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="43567-124">Příklady</span><span class="sxs-lookup"><span data-stu-id="43567-124">Examples</span></span>

<span data-ttu-id="43567-125">Vypsat všechny balíčky z nakonfigurovaných informačních kanálů:</span><span class="sxs-lookup"><span data-stu-id="43567-125">List all packages from configured feeds:</span></span>
```
nuget list
```
<span data-ttu-id="43567-126">Seznamte se s podrobnými podrobnostmi pro balíčky související s Azure:</span><span class="sxs-lookup"><span data-stu-id="43567-126">List Azure-related packages with detailed verbosity:</span></span>
```
nuget list Azure -Verbosity detailed
```
<span data-ttu-id="43567-127">Vypíše všechny verze balíčků souvisejících s Azure z nakonfigurovaných informačních kanálů:</span><span class="sxs-lookup"><span data-stu-id="43567-127">List all versions of Azure-related packages from configured feeds:</span></span>
```
nuget list Azure -AllVersions
```
<span data-ttu-id="43567-128">Vypíše všechny verze balíčků souvisejících s JSON ze zadaného zdroje nebo kanálu:</span><span class="sxs-lookup"><span data-stu-id="43567-128">List all versions of JSON-related packages from specified source/feed:</span></span>
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
<span data-ttu-id="43567-129">Vypíše balíčky související s JSON z několika zdrojů nebo kanálů:</span><span class="sxs-lookup"><span data-stu-id="43567-129">List JSON-related packages from multiple sources/feeds:</span></span>
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```
