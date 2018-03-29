---
title: Příkaz help NuGet rozhraní příkazového řádku | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referenční dokumentace pro příkaz nuget.exe nápovědy
keywords: odkaz na nápovědu nuget, příkazu nápovědy
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 440861e53b4a9ff73a9d3e8a2a3dad7dbddc9584
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="ff84d-104">Nápověda nebo?</span><span class="sxs-lookup"><span data-stu-id="ff84d-104">help or ?</span></span> <span data-ttu-id="ff84d-105">příkaz (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="ff84d-105">command (NuGet CLI)</span></span>

<span data-ttu-id="ff84d-106">**Platí pro:** všechny &bullet; **podporované verze**: všechny</span><span class="sxs-lookup"><span data-stu-id="ff84d-106">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="ff84d-107">Zobrazí obecné pomůže informace a informace o určité příkazy.</span><span class="sxs-lookup"><span data-stu-id="ff84d-107">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="ff84d-108">Použití</span><span class="sxs-lookup"><span data-stu-id="ff84d-108">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="ff84d-109">[příkaz] kde identifikuje konkrétní příkaz pro které chcete zobrazit nápovědu.</span><span class="sxs-lookup"><span data-stu-id="ff84d-109">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="ff84d-110">U některých příkazů, mějte na paměti k určení *pomoci* , jako první se `nuget help install`, protože je balíček s názvem "Nápověda" v nuget.org. Pokud zadáte název příkazu `nuget install help`, nebude získání nápovědy na příkaz instalace, ale místo toho nainstaluje balíček s názvem nápovědy.</span><span class="sxs-lookup"><span data-stu-id="ff84d-110">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="ff84d-111">Možnosti</span><span class="sxs-lookup"><span data-stu-id="ff84d-111">Options</span></span>

| <span data-ttu-id="ff84d-112">Možnost</span><span class="sxs-lookup"><span data-stu-id="ff84d-112">Option</span></span> | <span data-ttu-id="ff84d-113">Popis</span><span class="sxs-lookup"><span data-stu-id="ff84d-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ff84d-114">Všechny</span><span class="sxs-lookup"><span data-stu-id="ff84d-114">All</span></span> | <span data-ttu-id="ff84d-115">Tisk podrobnou nápovědu pro všechny dostupné příkazy; Pokud je zadána konkrétní příkaz ignorována.</span><span class="sxs-lookup"><span data-stu-id="ff84d-115">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="ff84d-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="ff84d-116">ConfigFile</span></span> | <span data-ttu-id="ff84d-117">Konfigurační soubor NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="ff84d-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ff84d-118">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.</span><span class="sxs-lookup"><span data-stu-id="ff84d-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="ff84d-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="ff84d-119">ForceEnglishOutput</span></span> | <span data-ttu-id="ff84d-120">*(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze.</span><span class="sxs-lookup"><span data-stu-id="ff84d-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="ff84d-121">Nápověda</span><span class="sxs-lookup"><span data-stu-id="ff84d-121">Help</span></span> | <span data-ttu-id="ff84d-122">Zobrazí nápovědu pro příkaz help sám sebe.</span><span class="sxs-lookup"><span data-stu-id="ff84d-122">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="ff84d-123">Markdownu</span><span class="sxs-lookup"><span data-stu-id="ff84d-123">Markdown</span></span> | <span data-ttu-id="ff84d-124">Tisk podrobnou nápovědu ve formátu markdown při použití s `-All`.</span><span class="sxs-lookup"><span data-stu-id="ff84d-124">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="ff84d-125">V opačném případě ignorovat.</span><span class="sxs-lookup"><span data-stu-id="ff84d-125">Ignored otherwise.</span></span> |
| <span data-ttu-id="ff84d-126">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="ff84d-126">NonInteractive</span></span> | <span data-ttu-id="ff84d-127">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="ff84d-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="ff84d-128">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="ff84d-128">Verbosity</span></span> | <span data-ttu-id="ff84d-129">Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="ff84d-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="ff84d-130">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ff84d-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ff84d-131">Příklady</span><span class="sxs-lookup"><span data-stu-id="ff84d-131">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
