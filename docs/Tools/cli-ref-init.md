---
title: Rozhraní příkazového řádku NuGet init – příkaz
description: Referenční dokumentace pro nuget.exe init – příkaz
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f5e819d014637d1ebb0403d9d838f9362efb20f0
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="43361-103">Init – příkaz (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="43361-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="43361-104">**Platí pro:** balíček vytvoření &bullet; **podporované verze:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="43361-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="43361-105">Zkopíruje všechny balíčky z plochých složku do cílové složky pomocí hierarchickém rozložení, jak je popsáno [přidat příkaz](cli-ref-add.md).</span><span class="sxs-lookup"><span data-stu-id="43361-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="43361-106">To znamená, pomocí `init` je ekvivalentní k použití `add` na každý balíček ve složce.</span><span class="sxs-lookup"><span data-stu-id="43361-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="43361-107">Stejně jako u `add`, cíl musí být místní složku nebo cesty UNC. Úložiště balíčku HTTP například nuget.org nebo privátní servery nejsou podporovány.</span><span class="sxs-lookup"><span data-stu-id="43361-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="43361-108">Použití</span><span class="sxs-lookup"><span data-stu-id="43361-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="43361-109">kde `<source>` je složka, která obsahuje balíčky a `<destination>` je místní složka nebo cesta UNC ke kterému se zkopírují balíčky.</span><span class="sxs-lookup"><span data-stu-id="43361-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="43361-110">Možnosti</span><span class="sxs-lookup"><span data-stu-id="43361-110">Options</span></span>

| <span data-ttu-id="43361-111">Možnost</span><span class="sxs-lookup"><span data-stu-id="43361-111">Option</span></span> | <span data-ttu-id="43361-112">Popis</span><span class="sxs-lookup"><span data-stu-id="43361-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="43361-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="43361-113">ConfigFile</span></span> | <span data-ttu-id="43361-114">Konfigurační soubor NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="43361-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="43361-115">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.</span><span class="sxs-lookup"><span data-stu-id="43361-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="43361-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="43361-116">ForceEnglishOutput</span></span> | <span data-ttu-id="43361-117">*(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze.</span><span class="sxs-lookup"><span data-stu-id="43361-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="43361-118">Rozbalte položku</span><span class="sxs-lookup"><span data-stu-id="43361-118">Expand</span></span> | <span data-ttu-id="43361-119">Přidá všechny soubory v každý balíček, který je přidán ke zdroji balíčku; stejné jako `-Expand` s `add` příkaz.</span><span class="sxs-lookup"><span data-stu-id="43361-119">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="43361-120">Nápověda</span><span class="sxs-lookup"><span data-stu-id="43361-120">Help</span></span> | <span data-ttu-id="43361-121">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="43361-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="43361-122">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="43361-122">NonInteractive</span></span> | <span data-ttu-id="43361-123">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="43361-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="43361-124">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="43361-124">Verbosity</span></span> | <span data-ttu-id="43361-125">Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="43361-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="43361-126">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="43361-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="43361-127">Příklady</span><span class="sxs-lookup"><span data-stu-id="43361-127">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
