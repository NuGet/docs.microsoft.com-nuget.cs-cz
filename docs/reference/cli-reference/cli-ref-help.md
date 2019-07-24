---
title: NuGet – příkaz help CLI
description: Referenční informace o příkazu NuGet. exe help
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328342"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="5644a-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="5644a-103">help or ?</span></span> <span data-ttu-id="5644a-104">Příkaz (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="5644a-104">command (NuGet CLI)</span></span>

<span data-ttu-id="5644a-105">**Platí pro:** všechny &bullet; **podporované verze**: vše</span><span class="sxs-lookup"><span data-stu-id="5644a-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="5644a-106">Zobrazí obecné informace o nápovědě a nápovědu k určitým příkazům.</span><span class="sxs-lookup"><span data-stu-id="5644a-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="5644a-107">Použití</span><span class="sxs-lookup"><span data-stu-id="5644a-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="5644a-108">WHERE [příkaz] identifikuje konkrétní příkaz, pro který chcete zobrazit nápovědu.</span><span class="sxs-lookup"><span data-stu-id="5644a-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="5644a-109">U některých příkazů Nezapomeňte zadat nejprve *help* , jako `nuget help install`je například, protože v NuGet.org je balíček s názvem "Help". Pokud příkaz `nuget install help`přiřadíte, nebudete mít k příkazu install nápovědu, ale místo toho se nainstaluje balíček s názvem Nápověda.</span><span class="sxs-lookup"><span data-stu-id="5644a-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="5644a-110">Možnosti</span><span class="sxs-lookup"><span data-stu-id="5644a-110">Options</span></span>

| <span data-ttu-id="5644a-111">Možnost</span><span class="sxs-lookup"><span data-stu-id="5644a-111">Option</span></span> | <span data-ttu-id="5644a-112">Popis</span><span class="sxs-lookup"><span data-stu-id="5644a-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5644a-113">Všechny</span><span class="sxs-lookup"><span data-stu-id="5644a-113">All</span></span> | <span data-ttu-id="5644a-114">Vytiskne podrobnou nápovědu pro všechny dostupné příkazy. ignoruje se, pokud je zadaný konkrétní příkaz.</span><span class="sxs-lookup"><span data-stu-id="5644a-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="5644a-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="5644a-115">ConfigFile</span></span> | <span data-ttu-id="5644a-116">Konfigurační soubor NuGet, který se má použít</span><span class="sxs-lookup"><span data-stu-id="5644a-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="5644a-117">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows `~/.nuget/NuGet/NuGet.Config` ) nebo (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="5644a-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="5644a-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="5644a-118">ForceEnglishOutput</span></span> | <span data-ttu-id="5644a-119">*(3.5 +)* Vynutí, aby soubor NuGet. exe běžel pomocí neutrální jazykové verze určené pro angličtinu.</span><span class="sxs-lookup"><span data-stu-id="5644a-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="5644a-120">Help</span><span class="sxs-lookup"><span data-stu-id="5644a-120">Help</span></span> | <span data-ttu-id="5644a-121">Zobrazí informace o nápovědě k samotnému příkazu help.</span><span class="sxs-lookup"><span data-stu-id="5644a-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="5644a-122">Markdown</span><span class="sxs-lookup"><span data-stu-id="5644a-122">Markdown</span></span> | <span data-ttu-id="5644a-123">Při použití s nástrojem `-All`tisknout podrobnou podporu ve formátu Markdownu</span><span class="sxs-lookup"><span data-stu-id="5644a-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="5644a-124">V opačném případě ignorována.</span><span class="sxs-lookup"><span data-stu-id="5644a-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="5644a-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="5644a-125">NonInteractive</span></span> | <span data-ttu-id="5644a-126">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="5644a-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="5644a-127">Verbosity</span><span class="sxs-lookup"><span data-stu-id="5644a-127">Verbosity</span></span> | <span data-ttu-id="5644a-128">Určuje množství podrobností zobrazených ve výstupu: *normální*, tiché a *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="5644a-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="5644a-129">Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="5644a-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="5644a-130">Příklady</span><span class="sxs-lookup"><span data-stu-id="5644a-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
