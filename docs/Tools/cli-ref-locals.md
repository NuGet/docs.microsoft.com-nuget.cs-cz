---
title: "Příkaz místní hodnoty – NuGet rozhraní příkazového řádku | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenční dokumentace pro nuget.exe místní hodnoty – příkaz"
keywords: "místní hodnoty – odkaz nuget, místní hodnoty – příkaz"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b2f62a9ab5699bfb486eee146ab7046f5240aa50
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="73b8f-104">místní hodnoty – příkaz (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="73b8f-104">locals command (NuGet CLI)</span></span>

<span data-ttu-id="73b8f-105">**Platí pro:** balíček spotřeba &bullet; **podporované verze:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="73b8f-105">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="73b8f-106">Vymaže nebo vypíše místní prostředky NuGet například mezipaměti požadavek http, mezipaměti balíčky a složka globální balíčky celého systému.</span><span class="sxs-lookup"><span data-stu-id="73b8f-106">Clears or lists local NuGet resources such as the http-request cache, packages cache, and the machine-wide global packages folder.</span></span> <span data-ttu-id="73b8f-107">`locals` Příkaz lze použít také zobrazíte seznam těchto umístěních.</span><span class="sxs-lookup"><span data-stu-id="73b8f-107">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="73b8f-108">Další informace najdete v tématu [Správa mezipaměti NuGet](../consume-packages/managing-the-nuget-cache.md).</span><span class="sxs-lookup"><span data-stu-id="73b8f-108">For more information, see [Managing the NuGet Cache](../consume-packages/managing-the-nuget-cache.md).</span></span>

## <a name="usage"></a><span data-ttu-id="73b8f-109">Použití</span><span class="sxs-lookup"><span data-stu-id="73b8f-109">Usage</span></span>

```cli
nuget locals <cache> [options]
```

<span data-ttu-id="73b8f-110">kde `<cache>` je jedním z `all`, `http-cache`, `packages-cache`, `global-packages`, a `temp` *(3.4 +)*.</span><span class="sxs-lookup"><span data-stu-id="73b8f-110">where `<cache>` is one of `all`, `http-cache`, `packages-cache`, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="73b8f-111">Možnosti</span><span class="sxs-lookup"><span data-stu-id="73b8f-111">Options</span></span>

| <span data-ttu-id="73b8f-112">Možnost</span><span class="sxs-lookup"><span data-stu-id="73b8f-112">Option</span></span> | <span data-ttu-id="73b8f-113">Popis</span><span class="sxs-lookup"><span data-stu-id="73b8f-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="73b8f-114">Zrušte zaškrtnutí</span><span class="sxs-lookup"><span data-stu-id="73b8f-114">Clear</span></span> | <span data-ttu-id="73b8f-115">Zadaný mezipaměť nevymaže.</span><span class="sxs-lookup"><span data-stu-id="73b8f-115">Clears the specified cache.</span></span> |
| <span data-ttu-id="73b8f-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="73b8f-116">ConfigFile</span></span> | <span data-ttu-id="73b8f-117">Konfigurační soubor NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="73b8f-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="73b8f-118">Pokud není zadaný, *%AppData%\NuGet\NuGet.Config* se používá.</span><span class="sxs-lookup"><span data-stu-id="73b8f-118">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="73b8f-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="73b8f-119">ForceEnglishOutput</span></span> | <span data-ttu-id="73b8f-120">*(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze.</span><span class="sxs-lookup"><span data-stu-id="73b8f-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="73b8f-121">Nápověda</span><span class="sxs-lookup"><span data-stu-id="73b8f-121">Help</span></span> | <span data-ttu-id="73b8f-122">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="73b8f-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="73b8f-123">Seznam</span><span class="sxs-lookup"><span data-stu-id="73b8f-123">List</span></span> | <span data-ttu-id="73b8f-124">Zobrazí seznam umístění zadaná mezipaměti nebo umístění všechny mezipaměti při použití s *všechny*.</span><span class="sxs-lookup"><span data-stu-id="73b8f-124">Lists the location of the specified cache, or the locations of all caches when used with *all*.</span></span> |
| <span data-ttu-id="73b8f-125">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="73b8f-125">NonInteractive</span></span> | <span data-ttu-id="73b8f-126">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="73b8f-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="73b8f-127">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="73b8f-127">Verbosity</span></span> | <span data-ttu-id="73b8f-128">Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="73b8f-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="73b8f-129">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="73b8f-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="73b8f-130">Příklady</span><span class="sxs-lookup"><span data-stu-id="73b8f-130">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```
