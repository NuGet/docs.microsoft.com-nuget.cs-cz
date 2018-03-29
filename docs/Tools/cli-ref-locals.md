---
title: Příkaz místní hodnoty – NuGet rozhraní příkazového řádku | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/19/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referenční dokumentace pro nuget.exe místní hodnoty – příkaz
keywords: místní hodnoty – odkaz nuget, místní hodnoty – příkaz
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 0122c79e55b12838bd123cf91bfcbc5dbbd2a65c
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="97cc0-104">místní hodnoty – příkaz (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="97cc0-104">locals command (NuGet CLI)</span></span>

<span data-ttu-id="97cc0-105">**Platí pro:** balíček spotřeba &bullet; **podporované verze:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="97cc0-105">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="97cc0-106">Vymaže nebo vypíše místní prostředky NuGet, jako *http mezipaměti*, *globální balíčky* složku a dočasnou složku.</span><span class="sxs-lookup"><span data-stu-id="97cc0-106">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="97cc0-107">`locals` Příkaz lze použít také zobrazíte seznam těchto umístěních.</span><span class="sxs-lookup"><span data-stu-id="97cc0-107">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="97cc0-108">Další informace najdete v tématu [správy globální balíčky a složky mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="97cc0-108">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="97cc0-109">Použití</span><span class="sxs-lookup"><span data-stu-id="97cc0-109">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="97cc0-110">kde `<folder>` je jedním z `all`, `http-cache`, `packages-cache` *(3.5 a starší)*, `global-packages`, a `temp` *(3.4 +)*.</span><span class="sxs-lookup"><span data-stu-id="97cc0-110">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="97cc0-111">Možnosti</span><span class="sxs-lookup"><span data-stu-id="97cc0-111">Options</span></span>

| <span data-ttu-id="97cc0-112">Možnost</span><span class="sxs-lookup"><span data-stu-id="97cc0-112">Option</span></span> | <span data-ttu-id="97cc0-113">Popis</span><span class="sxs-lookup"><span data-stu-id="97cc0-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="97cc0-114">Zrušte zaškrtnutí</span><span class="sxs-lookup"><span data-stu-id="97cc0-114">Clear</span></span> | <span data-ttu-id="97cc0-115">Vymaže do zadané složky.</span><span class="sxs-lookup"><span data-stu-id="97cc0-115">Clears the specified folder.</span></span> |
| <span data-ttu-id="97cc0-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="97cc0-116">ConfigFile</span></span> | <span data-ttu-id="97cc0-117">Konfigurační soubor NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="97cc0-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="97cc0-118">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.</span><span class="sxs-lookup"><span data-stu-id="97cc0-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="97cc0-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="97cc0-119">ForceEnglishOutput</span></span> | <span data-ttu-id="97cc0-120">*(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze.</span><span class="sxs-lookup"><span data-stu-id="97cc0-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="97cc0-121">Nápověda</span><span class="sxs-lookup"><span data-stu-id="97cc0-121">Help</span></span> | <span data-ttu-id="97cc0-122">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="97cc0-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="97cc0-123">Seznam</span><span class="sxs-lookup"><span data-stu-id="97cc0-123">List</span></span> | <span data-ttu-id="97cc0-124">Zobrazí seznam umístění do zadané složky nebo umístění všechny složky při použití s *všechny*.</span><span class="sxs-lookup"><span data-stu-id="97cc0-124">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="97cc0-125">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="97cc0-125">NonInteractive</span></span> | <span data-ttu-id="97cc0-126">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="97cc0-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="97cc0-127">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="97cc0-127">Verbosity</span></span> | <span data-ttu-id="97cc0-128">Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="97cc0-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="97cc0-129">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="97cc0-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="97cc0-130">Příklady</span><span class="sxs-lookup"><span data-stu-id="97cc0-130">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="97cc0-131">Další příklady najdete v tématu [správy globální balíčky a složky mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="97cc0-131">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
