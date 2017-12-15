---
title: "Příkaz help NuGet rozhraní příkazového řádku | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 780d7f52-d6c6-45cd-8a62-218ff8c0b270
description: "Referenční dokumentace pro příkaz nuget.exe nápovědy"
keywords: "odkaz na nápovědu nuget, příkazu nápovědy"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 55dc263fedd7ed5a3e48b76dbc9a3ccc220655cf
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="74f03-104">Nápověda nebo?</span><span class="sxs-lookup"><span data-stu-id="74f03-104">help or ?</span></span> <span data-ttu-id="74f03-105">příkaz (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="74f03-105">command (NuGet CLI)</span></span>

<span data-ttu-id="74f03-106">**Platí pro:** všechny &bullet; **podporované verze**: všechny</span><span class="sxs-lookup"><span data-stu-id="74f03-106">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="74f03-107">Zobrazí obecné pomůže informace a informace o určité příkazy.</span><span class="sxs-lookup"><span data-stu-id="74f03-107">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="74f03-108">Použití</span><span class="sxs-lookup"><span data-stu-id="74f03-108">Usage</span></span>

```
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="74f03-109">[příkaz] kde identifikuje konkrétní příkaz pro které chcete zobrazit nápovědu.</span><span class="sxs-lookup"><span data-stu-id="74f03-109">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="74f03-110">U některých příkazů, mějte na paměti k určení *pomoci* , jako první se `nuget help install`, protože je balíček s názvem "Nápověda" v nuget.org. Pokud zadáte název příkazu `nuget install help`, není získání nápovědy na příkaz instalace, ale místo toho nainstaluje balíček s názvem nápovědy.</span><span class="sxs-lookup"><span data-stu-id="74f03-110">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you'll not get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="74f03-111">Možnosti</span><span class="sxs-lookup"><span data-stu-id="74f03-111">Options</span></span>

| <span data-ttu-id="74f03-112">Možnost</span><span class="sxs-lookup"><span data-stu-id="74f03-112">Option</span></span> | <span data-ttu-id="74f03-113">Popis</span><span class="sxs-lookup"><span data-stu-id="74f03-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="74f03-114">Všechny</span><span class="sxs-lookup"><span data-stu-id="74f03-114">All</span></span> | <span data-ttu-id="74f03-115">Tisk podrobnou nápovědu pro všechny dostupné příkazy; Pokud je zadána konkrétní příkaz ignorována.</span><span class="sxs-lookup"><span data-stu-id="74f03-115">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="74f03-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="74f03-116">ConfigFile</span></span> | <span data-ttu-id="74f03-117">*(2.5 +)*  NuGet konfiguračním souboru použít.</span><span class="sxs-lookup"><span data-stu-id="74f03-117">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="74f03-118">Pokud není zadaný, *%AppData%\NuGet\NuGet.Config* se používá.</span><span class="sxs-lookup"><span data-stu-id="74f03-118">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="74f03-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="74f03-119">ForceEnglishOutput</span></span> | <span data-ttu-id="74f03-120">*(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze.</span><span class="sxs-lookup"><span data-stu-id="74f03-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="74f03-121">Nápověda</span><span class="sxs-lookup"><span data-stu-id="74f03-121">Help</span></span> | <span data-ttu-id="74f03-122">Zobrazí nápovědu pro příkaz help sám sebe.</span><span class="sxs-lookup"><span data-stu-id="74f03-122">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="74f03-123">Markdownu</span><span class="sxs-lookup"><span data-stu-id="74f03-123">Markdown</span></span> | <span data-ttu-id="74f03-124">Tisk podrobnou nápovědu ve formátu markdown při použití s `-All`.</span><span class="sxs-lookup"><span data-stu-id="74f03-124">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="74f03-125">V opačném případě ignorovat.</span><span class="sxs-lookup"><span data-stu-id="74f03-125">Ignored otherwise.</span></span> |
| <span data-ttu-id="74f03-126">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="74f03-126">NonInteractive</span></span> | <span data-ttu-id="74f03-127">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="74f03-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="74f03-128">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="74f03-128">Verbosity</span></span> | <span data-ttu-id="74f03-129">Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="74f03-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="74f03-130">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="74f03-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="74f03-131">Příklady</span><span class="sxs-lookup"><span data-stu-id="74f03-131">Examples</span></span>

```
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
