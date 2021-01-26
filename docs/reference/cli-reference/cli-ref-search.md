---
title: Příkaz pro vyhledávání NuGet CLI
description: Referenční informace pro příkaz nuget.exe Search
author: JonDouglas
ms.author: jodou
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 6f4adcdf3981e5ec0e5e88337a8c3bcdd9158ca3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779165"
---
# <a name="search-command-nuget-cli"></a><span data-ttu-id="d8657-103">Search – příkaz (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="d8657-103">search command (NuGet CLI)</span></span>

<span data-ttu-id="d8657-104">**Platí pro:** &bullet; **podporované verze balíčku:** 5,8 +</span><span class="sxs-lookup"><span data-stu-id="d8657-104">**Applies to:** package consumption &bullet; **Supported versions:** 5.8+</span></span>

<span data-ttu-id="d8657-105">Vyhledá zadaný zdroj pomocí zadaného řetězce dotazu.</span><span class="sxs-lookup"><span data-stu-id="d8657-105">Searches a given source using the query string provided.</span></span> <span data-ttu-id="d8657-106">Pokud nejsou zadány žádné zdroje, budou použity všechny zdroje definované v% data% \NuGet\NuGet.config.</span><span class="sxs-lookup"><span data-stu-id="d8657-106">If no sources are specified, all sources defined in %AppData%\NuGet\NuGet.config are used.</span></span>

## <a name="usage"></a><span data-ttu-id="d8657-107">Využití</span><span class="sxs-lookup"><span data-stu-id="d8657-107">Usage</span></span>

```cli
nuget search [search terms] [options]
```

<span data-ttu-id="d8657-108">kde jsou použity hledané výrazy pro názvy balíčků, značek a popisů balíčků stejně jako při jejich použití v nuget.org.</span><span class="sxs-lookup"><span data-stu-id="d8657-108">where the search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="d8657-109">Možnosti</span><span class="sxs-lookup"><span data-stu-id="d8657-109">Options</span></span>

| <span data-ttu-id="d8657-110">Název</span><span class="sxs-lookup"><span data-stu-id="d8657-110">Name</span></span> | <span data-ttu-id="d8657-111">Popis</span><span class="sxs-lookup"><span data-stu-id="d8657-111">Description</span></span> | <span data-ttu-id="d8657-112">Využití</span><span class="sxs-lookup"><span data-stu-id="d8657-112">Usage</span></span> |
| ---  |     ---     |  :-:  |
| <span data-ttu-id="d8657-113">Předběžné verze</span><span class="sxs-lookup"><span data-stu-id="d8657-113">PreRelease</span></span> | <span data-ttu-id="d8657-114">Balíčky předběžného vydání nejsou ve výchozím nastavení zahrnuty, ale mohou být zahrnuty pomocí tohoto argumentu.</span><span class="sxs-lookup"><span data-stu-id="d8657-114">Pre-release packages are not included by default, but can be included by using this argument</span></span> | <span data-ttu-id="d8657-115">– Předběžná verze</span><span class="sxs-lookup"><span data-stu-id="d8657-115">-PreRelease</span></span> |
| <span data-ttu-id="d8657-116">Zdroj</span><span class="sxs-lookup"><span data-stu-id="d8657-116">Source</span></span> | <span data-ttu-id="d8657-117">Konkrétní zdroje balíčků pro vyhledávání místo dotazování na výchozí zdroje v __nuget.config__</span><span class="sxs-lookup"><span data-stu-id="d8657-117">Specific package source(s) to search instead of querying the default sources in __nuget.config__</span></span> | <span data-ttu-id="d8657-118">-Source `<Source URL>`</span><span class="sxs-lookup"><span data-stu-id="d8657-118">-Source `<Source URL>`</span></span>|
| <span data-ttu-id="d8657-119">Take</span><span class="sxs-lookup"><span data-stu-id="d8657-119">Take</span></span> | <span data-ttu-id="d8657-120">Počet výsledků, které se mají vrátit.</span><span class="sxs-lookup"><span data-stu-id="d8657-120">The number of results to return.</span></span> <span data-ttu-id="d8657-121">Výchozí hodnota je 20.</span><span class="sxs-lookup"><span data-stu-id="d8657-121">The default value is 20.</span></span> | <span data-ttu-id="d8657-122">– Převzít `<positive integer>`</span><span class="sxs-lookup"><span data-stu-id="d8657-122">-Take `<positive integer>`</span></span> |
| <span data-ttu-id="d8657-123">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="d8657-123">Verbosity</span></span> | <span data-ttu-id="d8657-124">Úroveň podrobností, která se má zobrazit ve výstupu</span><span class="sxs-lookup"><span data-stu-id="d8657-124">The level of detail to display in the output.</span></span> <span data-ttu-id="d8657-125">Výchozí hodnota je _Normal_.</span><span class="sxs-lookup"><span data-stu-id="d8657-125">The default is _normal_.</span></span> <span data-ttu-id="d8657-126">(Viz poznámka níže)</span><span class="sxs-lookup"><span data-stu-id="d8657-126">(See the note below)</span></span>  | <span data-ttu-id="d8657-127">– Podrobnosti `<quiet|normal|detailed>`</span><span class="sxs-lookup"><span data-stu-id="d8657-127">-Verbosity `<quiet|normal|detailed>`</span></span> |
| <span data-ttu-id="d8657-128">Nápověda</span><span class="sxs-lookup"><span data-stu-id="d8657-128">Help</span></span> | <span data-ttu-id="d8657-129">Zobrazí informace o nápovědě k příkazu.</span><span class="sxs-lookup"><span data-stu-id="d8657-129">Displays help information for the command</span></span> | <span data-ttu-id="d8657-130">-Help</span><span class="sxs-lookup"><span data-stu-id="d8657-130">-Help</span></span> |

<span data-ttu-id="d8657-131">Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="d8657-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

> [!NOTE] 
> <span data-ttu-id="d8657-132">Úrovně podrobností:</span><span class="sxs-lookup"><span data-stu-id="d8657-132">Verbosity Levels:</span></span>
> * <span data-ttu-id="d8657-133">_quiet_ – ID balíčku, verze</span><span class="sxs-lookup"><span data-stu-id="d8657-133">_quiet_ - Package ID, Version</span></span>
> * <span data-ttu-id="d8657-134">_Normal_ – ID balíčku, verze, soubory ke stažení, náhled popisu</span><span class="sxs-lookup"><span data-stu-id="d8657-134">_normal_ - Package ID, Version, Downloads, Preview of Description</span></span>
> * <span data-ttu-id="d8657-135">_podrobné_ – ID balíčku, verze, soubory ke stažení, úplný popis, další informace, jako je například adresa URL dotazu</span><span class="sxs-lookup"><span data-stu-id="d8657-135">_detailed_ - Package ID, Version, Downloads, Full Description, Other information such as the query URL</span></span>

## <a name="examples"></a><span data-ttu-id="d8657-136">Příklady</span><span class="sxs-lookup"><span data-stu-id="d8657-136">Examples</span></span>

<span data-ttu-id="d8657-137">Vyhledat balíčky související s *protokolováním* z výchozích zdrojů:</span><span class="sxs-lookup"><span data-stu-id="d8657-137">Search for *logging*-related packages from default sources:</span></span>
```
nuget search logging
```
<span data-ttu-id="d8657-138">Vyhledejte balíčky související s *protokolováním* s podrobnostmi:</span><span class="sxs-lookup"><span data-stu-id="d8657-138">Search for *logging*-related packages with detailed verbosity:</span></span>
```
nuget search logging -Verbosity detailed
```
<span data-ttu-id="d8657-139">Vyhledejte balíčky související s *protokolováním* a zobrazte pouze prvních 5 výsledků:</span><span class="sxs-lookup"><span data-stu-id="d8657-139">Search for *logging*-related packages, and only show the top 5 results:</span></span>
```
nuget search logging -Take 5
```
<span data-ttu-id="d8657-140">Vyhledat balíčky související s *JSON*, včetně předběžných verzí, ze zadaného zdroje/informačního kanálu:</span><span class="sxs-lookup"><span data-stu-id="d8657-140">Search for *JSON*-related packages, including pre-release versions, from specified source/feed:</span></span>
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
<span data-ttu-id="d8657-141">Hledat balíčky související s *JSON* z několika zdrojů nebo kanálů:</span><span class="sxs-lookup"><span data-stu-id="d8657-141">Search for *JSON*-related packages from multiple sources/feeds:</span></span>
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
