---
title: NuGet – příkaz init CLI
description: Referenční informace o příkazu NuGet. exe init
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328336"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="9709e-103">init – příkaz (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="9709e-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="9709e-104">**Platí pro:** vytváření &bullet; balíčků **podporuje verze:** 3.3+</span><span class="sxs-lookup"><span data-stu-id="9709e-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="9709e-105">Zkopíruje všechny balíčky z ploché složky do cílové složky pomocí hierarchického rozložení, jak je popsáno v [příkazu přidat](cli-ref-add.md).</span><span class="sxs-lookup"><span data-stu-id="9709e-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="9709e-106">To znamená, že `init` použití je ekvivalentní s `add` použitím příkazu na každém balíčku ve složce.</span><span class="sxs-lookup"><span data-stu-id="9709e-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="9709e-107">Stejně jako `add`v nástroji musí být cílem buď místní složka, nebo cesta UNC; Úložiště balíčků HTTP, jako je nuget.org nebo privátní servery, nejsou podporovaná.</span><span class="sxs-lookup"><span data-stu-id="9709e-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="9709e-108">Použití</span><span class="sxs-lookup"><span data-stu-id="9709e-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="9709e-109">kde `<source>` je složka obsahující balíčky a `<destination>` je místní složkou nebo cestou UNC, na kterou jsou balíčky zkopírovány.</span><span class="sxs-lookup"><span data-stu-id="9709e-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="9709e-110">Možnosti</span><span class="sxs-lookup"><span data-stu-id="9709e-110">Options</span></span>

| <span data-ttu-id="9709e-111">Možnost</span><span class="sxs-lookup"><span data-stu-id="9709e-111">Option</span></span> | <span data-ttu-id="9709e-112">Popis</span><span class="sxs-lookup"><span data-stu-id="9709e-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9709e-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="9709e-113">ConfigFile</span></span> | <span data-ttu-id="9709e-114">Konfigurační soubor NuGet, který se má použít</span><span class="sxs-lookup"><span data-stu-id="9709e-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="9709e-115">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows `~/.nuget/NuGet/NuGet.Config` ) nebo (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="9709e-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="9709e-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="9709e-116">ForceEnglishOutput</span></span> | <span data-ttu-id="9709e-117">*(3.5 +)* Vynutí, aby soubor NuGet. exe běžel pomocí neutrální jazykové verze určené pro angličtinu.</span><span class="sxs-lookup"><span data-stu-id="9709e-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="9709e-118">Expand</span><span class="sxs-lookup"><span data-stu-id="9709e-118">Expand</span></span> | <span data-ttu-id="9709e-119">Přidá všechny soubory v každém balíčku, který je přidán do zdroje balíčku. totéž jako `-Expand` `add` u příkazu.</span><span class="sxs-lookup"><span data-stu-id="9709e-119">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="9709e-120">Help</span><span class="sxs-lookup"><span data-stu-id="9709e-120">Help</span></span> | <span data-ttu-id="9709e-121">Zobrazí informace o nápovědě k příkazu.</span><span class="sxs-lookup"><span data-stu-id="9709e-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="9709e-122">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="9709e-122">NonInteractive</span></span> | <span data-ttu-id="9709e-123">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="9709e-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="9709e-124">Verbosity</span><span class="sxs-lookup"><span data-stu-id="9709e-124">Verbosity</span></span> | <span data-ttu-id="9709e-125">Určuje množství podrobností zobrazených ve výstupu: *normální*, tiché a *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="9709e-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="9709e-126">Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="9709e-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="9709e-127">Příklady</span><span class="sxs-lookup"><span data-stu-id="9709e-127">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
