---
title: Rozhraní příkazového řádku NuGet místních hodnot
description: Referenční informace pro příkaz nuget.exe místních hodnot
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: 38d8b9366fb2749b77c987c950da3aa9e7f029fc
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/23/2018
ms.locfileid: "42794132"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="0462d-103">Příkaz local (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="0462d-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="0462d-104">**Platí pro:** balíček spotřeby &bullet; **podporované verze:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="0462d-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="0462d-105">Vymaže nebo vypíše místní prostředky NuGet, jako *http-cache*, *global-packages* složek a dočasné složky.</span><span class="sxs-lookup"><span data-stu-id="0462d-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="0462d-106">`locals` Příkaz lze také zobrazit seznam těchto umístěních.</span><span class="sxs-lookup"><span data-stu-id="0462d-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="0462d-107">Další informace najdete v tématu [Správa globálních balíčků a složek mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="0462d-107">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="0462d-108">Použití</span><span class="sxs-lookup"><span data-stu-id="0462d-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="0462d-109">kde `<folder>` je jedním z `all`, `http-cache`, `packages-cache` *(3.5 a starší)*, `global-packages`, `temp` *(3.4 +)*, a `plugins-cache` *(4.8 +)*.</span><span class="sxs-lookup"><span data-stu-id="0462d-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, `temp` *(3.4+)*, and `plugins-cache` *(4.8+)*.</span></span>

## <a name="options"></a><span data-ttu-id="0462d-110">Možnosti</span><span class="sxs-lookup"><span data-stu-id="0462d-110">Options</span></span>

| <span data-ttu-id="0462d-111">Možnost</span><span class="sxs-lookup"><span data-stu-id="0462d-111">Option</span></span> | <span data-ttu-id="0462d-112">Popis</span><span class="sxs-lookup"><span data-stu-id="0462d-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0462d-113">Vymazat</span><span class="sxs-lookup"><span data-stu-id="0462d-113">Clear</span></span> | <span data-ttu-id="0462d-114">Vymaže zadané složky.</span><span class="sxs-lookup"><span data-stu-id="0462d-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="0462d-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="0462d-115">ConfigFile</span></span> | <span data-ttu-id="0462d-116">Konfigurační soubor NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="0462d-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="0462d-117">Pokud není zadán, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.</span><span class="sxs-lookup"><span data-stu-id="0462d-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="0462d-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="0462d-118">ForceEnglishOutput</span></span> | <span data-ttu-id="0462d-119">*(3.5 +)*  Vynutí nuget.exe pro spuštění pomocí neutrální, základem je angličtina jazyková verze.</span><span class="sxs-lookup"><span data-stu-id="0462d-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="0462d-120">Nápověda</span><span class="sxs-lookup"><span data-stu-id="0462d-120">Help</span></span> | <span data-ttu-id="0462d-121">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="0462d-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="0462d-122">Seznam</span><span class="sxs-lookup"><span data-stu-id="0462d-122">List</span></span> | <span data-ttu-id="0462d-123">Zobrazí seznam umístění zadaná složka nebo umístění všech složek, při použití s *všechny*.</span><span class="sxs-lookup"><span data-stu-id="0462d-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="0462d-124">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="0462d-124">NonInteractive</span></span> | <span data-ttu-id="0462d-125">Potlačí vyzve k zadání uživatele o vstup ani potvrzení.</span><span class="sxs-lookup"><span data-stu-id="0462d-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="0462d-126">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="0462d-126">Verbosity</span></span> | <span data-ttu-id="0462d-127">Určuje množství podrobností, na které se zobrazí ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="0462d-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="0462d-128">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="0462d-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="0462d-129">Příklady</span><span class="sxs-lookup"><span data-stu-id="0462d-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="0462d-130">Další příklady najdete v tématu [Správa globálních balíčků a složek mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="0462d-130">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
