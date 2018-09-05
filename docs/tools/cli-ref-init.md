---
title: Rozhraní příkazového řádku NuGet init
description: Referenční informace pro příkaz init nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551407"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="57590-103">příkaz init (rozhraní příkazového řádku NuGet)</span><span class="sxs-lookup"><span data-stu-id="57590-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="57590-104">**Platí pro:** vytvoření balíčku &bullet; **podporované verze:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="57590-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="57590-105">Zkopíruje všechny balíčky z plochého složky do cílové složky pomocí hierarchickém rozložení, jak je popsáno [přidat příkaz](cli-ref-add.md).</span><span class="sxs-lookup"><span data-stu-id="57590-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="57590-106">To znamená, že použití `init` je ekvivalentní k použití `add` příkaz na každý balíček ve složce.</span><span class="sxs-lookup"><span data-stu-id="57590-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="57590-107">Stejně jako u `add`, cíl musí být místní složku nebo cesty UNC. Úložiště balíčku HTTP jako je nuget.org nebo privátní servery nejsou podporovány.</span><span class="sxs-lookup"><span data-stu-id="57590-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="57590-108">Použití</span><span class="sxs-lookup"><span data-stu-id="57590-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="57590-109">kde `<source>` je složku, která obsahuje balíčky a `<destination>` je místní složka nebo cesta UNC, do které se zkopírují balíčky.</span><span class="sxs-lookup"><span data-stu-id="57590-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="57590-110">Možnosti</span><span class="sxs-lookup"><span data-stu-id="57590-110">Options</span></span>

| <span data-ttu-id="57590-111">Možnost</span><span class="sxs-lookup"><span data-stu-id="57590-111">Option</span></span> | <span data-ttu-id="57590-112">Popis</span><span class="sxs-lookup"><span data-stu-id="57590-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="57590-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="57590-113">ConfigFile</span></span> | <span data-ttu-id="57590-114">Konfigurační soubor NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="57590-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="57590-115">Pokud není zadán, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.</span><span class="sxs-lookup"><span data-stu-id="57590-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="57590-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="57590-116">ForceEnglishOutput</span></span> | <span data-ttu-id="57590-117">*(3.5 +)*  Vynutí nuget.exe pro spuštění pomocí neutrální, základem je angličtina jazyková verze.</span><span class="sxs-lookup"><span data-stu-id="57590-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="57590-118">Rozbalte položku</span><span class="sxs-lookup"><span data-stu-id="57590-118">Expand</span></span> | <span data-ttu-id="57590-119">Přidá všechny soubory v každý balíček, který je přidán ke zdroji balíčku; stejné jako `-Expand` s `add` příkazu.</span><span class="sxs-lookup"><span data-stu-id="57590-119">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="57590-120">Nápověda</span><span class="sxs-lookup"><span data-stu-id="57590-120">Help</span></span> | <span data-ttu-id="57590-121">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="57590-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="57590-122">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="57590-122">NonInteractive</span></span> | <span data-ttu-id="57590-123">Potlačí vyzve k zadání uživatele o vstup ani potvrzení.</span><span class="sxs-lookup"><span data-stu-id="57590-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="57590-124">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="57590-124">Verbosity</span></span> | <span data-ttu-id="57590-125">Určuje množství podrobností, na které se zobrazí ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="57590-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="57590-126">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="57590-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="57590-127">Příklady</span><span class="sxs-lookup"><span data-stu-id="57590-127">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
