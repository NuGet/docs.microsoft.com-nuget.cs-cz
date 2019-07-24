---
title: NuGet CLI – příkaz místních hodnot
description: Referenční informace o příkazu NuGet. exe Locals
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: b02360c38ad66c95bbe3c7d403ef4a959112c91a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328345"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="fa0a4-103">Příkaz local (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="fa0a4-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="fa0a4-104">**Platí pro:** &bullet; **podporované verze balíčku:** 3.3+</span><span class="sxs-lookup"><span data-stu-id="fa0a4-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="fa0a4-105">Vymaže nebo vypíše místní prostředky NuGet, například složku *HTTP-cache*, *Global-Packages* a Temp.</span><span class="sxs-lookup"><span data-stu-id="fa0a4-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="fa0a4-106">`locals` Příkaz lze také použít k zobrazení seznamu těchto umístění.</span><span class="sxs-lookup"><span data-stu-id="fa0a4-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="fa0a4-107">Další informace najdete v tématu [Správa globálních balíčků a složek mezipaměti](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="fa0a4-107">For more information, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="fa0a4-108">Použití</span><span class="sxs-lookup"><span data-stu-id="fa0a4-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="fa0a4-109">kde `<folder>` je jedna z `all`, `http-cache` `global-packages` `temp` `plugins-cache` , `packages-cache` *(3,5 a starší)* ,, *(3.4 +)* a *(4.8 +)* .</span><span class="sxs-lookup"><span data-stu-id="fa0a4-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, `temp` *(3.4+)*, and `plugins-cache` *(4.8+)*.</span></span>

## <a name="options"></a><span data-ttu-id="fa0a4-110">Možnosti</span><span class="sxs-lookup"><span data-stu-id="fa0a4-110">Options</span></span>

| <span data-ttu-id="fa0a4-111">Možnost</span><span class="sxs-lookup"><span data-stu-id="fa0a4-111">Option</span></span> | <span data-ttu-id="fa0a4-112">Popis</span><span class="sxs-lookup"><span data-stu-id="fa0a4-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fa0a4-113">Vymazat</span><span class="sxs-lookup"><span data-stu-id="fa0a4-113">Clear</span></span> | <span data-ttu-id="fa0a4-114">Vymaže určenou složku.</span><span class="sxs-lookup"><span data-stu-id="fa0a4-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="fa0a4-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="fa0a4-115">ConfigFile</span></span> | <span data-ttu-id="fa0a4-116">Konfigurační soubor NuGet, který se má použít</span><span class="sxs-lookup"><span data-stu-id="fa0a4-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="fa0a4-117">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows `~/.nuget/NuGet/NuGet.Config` ) nebo (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="fa0a4-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="fa0a4-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="fa0a4-118">ForceEnglishOutput</span></span> | <span data-ttu-id="fa0a4-119">*(3.5 +)* Vynutí, aby soubor NuGet. exe běžel pomocí neutrální jazykové verze určené pro angličtinu.</span><span class="sxs-lookup"><span data-stu-id="fa0a4-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="fa0a4-120">Help</span><span class="sxs-lookup"><span data-stu-id="fa0a4-120">Help</span></span> | <span data-ttu-id="fa0a4-121">Zobrazí informace o nápovědě k příkazu.</span><span class="sxs-lookup"><span data-stu-id="fa0a4-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="fa0a4-122">Seznam</span><span class="sxs-lookup"><span data-stu-id="fa0a4-122">List</span></span> | <span data-ttu-id="fa0a4-123">Vypíše umístění zadané složky nebo umístění všech složek při použití se *všemi*.</span><span class="sxs-lookup"><span data-stu-id="fa0a4-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="fa0a4-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="fa0a4-124">NonInteractive</span></span> | <span data-ttu-id="fa0a4-125">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="fa0a4-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="fa0a4-126">Verbosity</span><span class="sxs-lookup"><span data-stu-id="fa0a4-126">Verbosity</span></span> | <span data-ttu-id="fa0a4-127">Určuje množství podrobností zobrazených ve výstupu: *normální*, tiché a *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="fa0a4-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="fa0a4-128">Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="fa0a4-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="fa0a4-129">Příklady</span><span class="sxs-lookup"><span data-stu-id="fa0a4-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="fa0a4-130">Další příklady najdete v tématu [Správa globálních balíčků a složek mezipaměti](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="fa0a4-130">For additional examples, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
