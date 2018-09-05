---
title: Rozhraní příkazového řádku NuGet místních hodnot
description: Referenční informace pro příkaz nuget.exe místních hodnot
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: ea216c4651ba9619bc3b6a7ab52546fd299b0bb6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545025"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="c4f05-103">Příkaz local (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="c4f05-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="c4f05-104">**Platí pro:** balíček spotřeby &bullet; **podporované verze:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="c4f05-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="c4f05-105">Vymaže nebo vypíše místní prostředky NuGet, jako *http-cache*, *global-packages* složek a dočasné složky.</span><span class="sxs-lookup"><span data-stu-id="c4f05-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="c4f05-106">`locals` Příkaz lze také zobrazit seznam těchto umístěních.</span><span class="sxs-lookup"><span data-stu-id="c4f05-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="c4f05-107">Další informace najdete v tématu [Správa globálních balíčků a složek mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="c4f05-107">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="c4f05-108">Použití</span><span class="sxs-lookup"><span data-stu-id="c4f05-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="c4f05-109">kde `<folder>` je jedním z `all`, `http-cache`, `packages-cache` *(3.5 a starší)*, `global-packages`, `temp` *(3.4 +)*, a `plugins-cache` *(4.8 +)*.</span><span class="sxs-lookup"><span data-stu-id="c4f05-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, `temp` *(3.4+)*, and `plugins-cache` *(4.8+)*.</span></span>

## <a name="options"></a><span data-ttu-id="c4f05-110">Možnosti</span><span class="sxs-lookup"><span data-stu-id="c4f05-110">Options</span></span>

| <span data-ttu-id="c4f05-111">Možnost</span><span class="sxs-lookup"><span data-stu-id="c4f05-111">Option</span></span> | <span data-ttu-id="c4f05-112">Popis</span><span class="sxs-lookup"><span data-stu-id="c4f05-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c4f05-113">Vymazat</span><span class="sxs-lookup"><span data-stu-id="c4f05-113">Clear</span></span> | <span data-ttu-id="c4f05-114">Vymaže zadané složky.</span><span class="sxs-lookup"><span data-stu-id="c4f05-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="c4f05-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="c4f05-115">ConfigFile</span></span> | <span data-ttu-id="c4f05-116">Konfigurační soubor NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="c4f05-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="c4f05-117">Pokud není zadán, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.</span><span class="sxs-lookup"><span data-stu-id="c4f05-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="c4f05-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="c4f05-118">ForceEnglishOutput</span></span> | <span data-ttu-id="c4f05-119">*(3.5 +)*  Vynutí nuget.exe pro spuštění pomocí neutrální, základem je angličtina jazyková verze.</span><span class="sxs-lookup"><span data-stu-id="c4f05-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="c4f05-120">Nápověda</span><span class="sxs-lookup"><span data-stu-id="c4f05-120">Help</span></span> | <span data-ttu-id="c4f05-121">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="c4f05-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="c4f05-122">Seznam</span><span class="sxs-lookup"><span data-stu-id="c4f05-122">List</span></span> | <span data-ttu-id="c4f05-123">Zobrazí seznam umístění zadaná složka nebo umístění všech složek, při použití s *všechny*.</span><span class="sxs-lookup"><span data-stu-id="c4f05-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="c4f05-124">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="c4f05-124">NonInteractive</span></span> | <span data-ttu-id="c4f05-125">Potlačí vyzve k zadání uživatele o vstup ani potvrzení.</span><span class="sxs-lookup"><span data-stu-id="c4f05-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="c4f05-126">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="c4f05-126">Verbosity</span></span> | <span data-ttu-id="c4f05-127">Určuje množství podrobností, na které se zobrazí ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="c4f05-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="c4f05-128">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c4f05-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c4f05-129">Příklady</span><span class="sxs-lookup"><span data-stu-id="c4f05-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="c4f05-130">Další příklady najdete v tématu [Správa globálních balíčků a složek mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="c4f05-130">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
