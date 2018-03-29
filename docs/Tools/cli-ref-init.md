---
title: Příkaz init NuGet rozhraní příkazového řádku | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referenční dokumentace pro nuget.exe init – příkaz
keywords: Init – odkaz nuget, Init – příkaz
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 01a3553622020b5868e33ece09cd7555cb712fd3
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="c54e0-104">Init – příkaz (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="c54e0-104">init command (NuGet CLI)</span></span>

<span data-ttu-id="c54e0-105">**Platí pro:** balíček vytvoření &bullet; **podporované verze:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="c54e0-105">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="c54e0-106">Zkopíruje všechny balíčky z plochých složku do cílové složky pomocí hierarchickém rozložení, jak je popsáno [přidat příkaz](cli-ref-add.md).</span><span class="sxs-lookup"><span data-stu-id="c54e0-106">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="c54e0-107">To znamená, pomocí `init` je ekvivalentní k použití `add` na každý balíček ve složce.</span><span class="sxs-lookup"><span data-stu-id="c54e0-107">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="c54e0-108">Stejně jako u `add`, cíl musí být místní složku nebo cesty UNC. Úložiště balíčku HTTP například nuget.org nebo privátní servery nejsou podporovány.</span><span class="sxs-lookup"><span data-stu-id="c54e0-108">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="c54e0-109">Použití</span><span class="sxs-lookup"><span data-stu-id="c54e0-109">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="c54e0-110">kde `<source>` je složka, která obsahuje balíčky a `<destination>` je místní složka nebo cesta UNC ke kterému se zkopírují balíčky.</span><span class="sxs-lookup"><span data-stu-id="c54e0-110">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="c54e0-111">Možnosti</span><span class="sxs-lookup"><span data-stu-id="c54e0-111">Options</span></span>

| <span data-ttu-id="c54e0-112">Možnost</span><span class="sxs-lookup"><span data-stu-id="c54e0-112">Option</span></span> | <span data-ttu-id="c54e0-113">Popis</span><span class="sxs-lookup"><span data-stu-id="c54e0-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c54e0-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="c54e0-114">ConfigFile</span></span> | <span data-ttu-id="c54e0-115">Konfigurační soubor NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="c54e0-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="c54e0-116">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.</span><span class="sxs-lookup"><span data-stu-id="c54e0-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="c54e0-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="c54e0-117">ForceEnglishOutput</span></span> | <span data-ttu-id="c54e0-118">*(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze.</span><span class="sxs-lookup"><span data-stu-id="c54e0-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="c54e0-119">Rozbalte položku</span><span class="sxs-lookup"><span data-stu-id="c54e0-119">Expand</span></span> | <span data-ttu-id="c54e0-120">Přidá všechny soubory v každý balíček, který je přidán ke zdroji balíčku; stejné jako `-Expand` s `add` příkaz.</span><span class="sxs-lookup"><span data-stu-id="c54e0-120">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="c54e0-121">Nápověda</span><span class="sxs-lookup"><span data-stu-id="c54e0-121">Help</span></span> | <span data-ttu-id="c54e0-122">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="c54e0-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="c54e0-123">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="c54e0-123">NonInteractive</span></span> | <span data-ttu-id="c54e0-124">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="c54e0-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="c54e0-125">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="c54e0-125">Verbosity</span></span> | <span data-ttu-id="c54e0-126">Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="c54e0-126">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="c54e0-127">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c54e0-127">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c54e0-128">Příklady</span><span class="sxs-lookup"><span data-stu-id="c54e0-128">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
