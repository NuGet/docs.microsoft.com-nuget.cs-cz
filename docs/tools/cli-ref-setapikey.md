---
title: Příkaz setapikey NuGet rozhraní příkazového řádku
description: Referenční informace pro příkaz nuget.exe setapikey
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b00e8b1f7a6fda9c1a0c079069fa8ee08a45b419
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549217"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="e93b4-103">příkaz setapikey (rozhraní příkazového řádku NuGet)</span><span class="sxs-lookup"><span data-stu-id="e93b4-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="e93b4-104">**Platí pro:** využití balíčků, publikováním &bullet; **podporované verze:** všechny</span><span class="sxs-lookup"><span data-stu-id="e93b4-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="e93b4-105">Uloží klíč rozhraní API pro adresu URL daného serveru do `NuGet.Config` tak, že není nutné zadat pro následné příkazy.</span><span class="sxs-lookup"><span data-stu-id="e93b4-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="e93b4-106">Použití</span><span class="sxs-lookup"><span data-stu-id="e93b4-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="e93b4-107">kde `<source>` identifikuje server a `<key>` je klíč nebo heslo uložte.</span><span class="sxs-lookup"><span data-stu-id="e93b4-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="e93b4-108">Pokud `<source>` je vynechána, předpokládá se nuget.org.</span><span class="sxs-lookup"><span data-stu-id="e93b4-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="e93b4-109">Možnosti</span><span class="sxs-lookup"><span data-stu-id="e93b4-109">Options</span></span>

| <span data-ttu-id="e93b4-110">Možnost</span><span class="sxs-lookup"><span data-stu-id="e93b4-110">Option</span></span> | <span data-ttu-id="e93b4-111">Popis</span><span class="sxs-lookup"><span data-stu-id="e93b4-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e93b4-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="e93b4-112">ConfigFile</span></span> | <span data-ttu-id="e93b4-113">Konfigurační soubor NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="e93b4-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="e93b4-114">Pokud není zadán, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.</span><span class="sxs-lookup"><span data-stu-id="e93b4-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="e93b4-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="e93b4-115">ForceEnglishOutput</span></span> | <span data-ttu-id="e93b4-116">*(3.5 +)*  Vynutí nuget.exe pro spuštění pomocí neutrální, základem je angličtina jazyková verze.</span><span class="sxs-lookup"><span data-stu-id="e93b4-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="e93b4-117">Nápověda</span><span class="sxs-lookup"><span data-stu-id="e93b4-117">Help</span></span> | <span data-ttu-id="e93b4-118">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="e93b4-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="e93b4-119">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="e93b4-119">NonInteractive</span></span> | <span data-ttu-id="e93b4-120">Potlačí vyzve k zadání uživatele o vstup ani potvrzení.</span><span class="sxs-lookup"><span data-stu-id="e93b4-120">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="e93b4-121">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="e93b4-121">Verbosity</span></span> | <span data-ttu-id="e93b4-122">Určuje množství podrobností, na které se zobrazí ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="e93b4-122">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="e93b4-123">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="e93b4-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="e93b4-124">Příklady</span><span class="sxs-lookup"><span data-stu-id="e93b4-124">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
