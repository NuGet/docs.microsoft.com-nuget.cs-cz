---
title: Rozhraní příkazového řádku NuGet místní hodnoty – příkaz
description: Referenční dokumentace pro nuget.exe místní hodnoty – příkaz
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: 90e8c85e7a3e0e9520933e2ddd6dd84447475f2b
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818198"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="c14c6-103">Příkaz local (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="c14c6-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="c14c6-104">**Platí pro:** balíček spotřeba &bullet; **podporované verze:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="c14c6-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="c14c6-105">Vymaže nebo vypíše místní prostředky NuGet, jako *http mezipaměti*, *globální balíčky* složku a dočasnou složku.</span><span class="sxs-lookup"><span data-stu-id="c14c6-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="c14c6-106">`locals` Příkaz lze použít také zobrazíte seznam těchto umístěních.</span><span class="sxs-lookup"><span data-stu-id="c14c6-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="c14c6-107">Další informace najdete v tématu [správy globální balíčky a složky mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="c14c6-107">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="c14c6-108">Použití</span><span class="sxs-lookup"><span data-stu-id="c14c6-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="c14c6-109">kde `<folder>` je jedním z `all`, `http-cache`, `packages-cache` *(3.5 a starší)*, `global-packages`, a `temp` *(3.4 +)*.</span><span class="sxs-lookup"><span data-stu-id="c14c6-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="c14c6-110">Možnosti</span><span class="sxs-lookup"><span data-stu-id="c14c6-110">Options</span></span>

| <span data-ttu-id="c14c6-111">Možnost</span><span class="sxs-lookup"><span data-stu-id="c14c6-111">Option</span></span> | <span data-ttu-id="c14c6-112">Popis</span><span class="sxs-lookup"><span data-stu-id="c14c6-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c14c6-113">Zrušte zaškrtnutí</span><span class="sxs-lookup"><span data-stu-id="c14c6-113">Clear</span></span> | <span data-ttu-id="c14c6-114">Vymaže do zadané složky.</span><span class="sxs-lookup"><span data-stu-id="c14c6-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="c14c6-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="c14c6-115">ConfigFile</span></span> | <span data-ttu-id="c14c6-116">Konfigurační soubor NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="c14c6-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="c14c6-117">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.</span><span class="sxs-lookup"><span data-stu-id="c14c6-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="c14c6-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="c14c6-118">ForceEnglishOutput</span></span> | <span data-ttu-id="c14c6-119">*(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze.</span><span class="sxs-lookup"><span data-stu-id="c14c6-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="c14c6-120">Nápověda</span><span class="sxs-lookup"><span data-stu-id="c14c6-120">Help</span></span> | <span data-ttu-id="c14c6-121">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="c14c6-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="c14c6-122">Seznam</span><span class="sxs-lookup"><span data-stu-id="c14c6-122">List</span></span> | <span data-ttu-id="c14c6-123">Zobrazí seznam umístění do zadané složky nebo umístění všechny složky při použití s *všechny*.</span><span class="sxs-lookup"><span data-stu-id="c14c6-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="c14c6-124">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="c14c6-124">NonInteractive</span></span> | <span data-ttu-id="c14c6-125">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="c14c6-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="c14c6-126">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="c14c6-126">Verbosity</span></span> | <span data-ttu-id="c14c6-127">Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="c14c6-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="c14c6-128">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c14c6-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c14c6-129">Příklady</span><span class="sxs-lookup"><span data-stu-id="c14c6-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="c14c6-130">Další příklady najdete v tématu [správy globální balíčky a složky mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="c14c6-130">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
