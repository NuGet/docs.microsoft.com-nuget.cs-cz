---
title: NuGet CLI – příkaz setapikey
description: Referenční informace o příkazu NuGet. exe setapikey
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b00e8b1f7a6fda9c1a0c079069fa8ee08a45b419
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328285"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="09f8a-103">setapikey – příkaz (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="09f8a-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="09f8a-104">**Platí pro:** spotřeba balíčku, publikování &bullet; **podporovaných verzí:** vše</span><span class="sxs-lookup"><span data-stu-id="09f8a-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="09f8a-105">Uloží klíč rozhraní API pro danou adresu URL `NuGet.Config` serveru tak, aby se nemusel zadat pro následné příkazy.</span><span class="sxs-lookup"><span data-stu-id="09f8a-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="09f8a-106">Použití</span><span class="sxs-lookup"><span data-stu-id="09f8a-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="09f8a-107">kde `<source>` identifikuje server a `<key>` je klíč nebo heslo, které se má uložit.</span><span class="sxs-lookup"><span data-stu-id="09f8a-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="09f8a-108">Pokud `<source>` je hodnota vynechána, předpokládá se NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="09f8a-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="09f8a-109">Možnosti</span><span class="sxs-lookup"><span data-stu-id="09f8a-109">Options</span></span>

| <span data-ttu-id="09f8a-110">Možnost</span><span class="sxs-lookup"><span data-stu-id="09f8a-110">Option</span></span> | <span data-ttu-id="09f8a-111">Popis</span><span class="sxs-lookup"><span data-stu-id="09f8a-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="09f8a-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="09f8a-112">ConfigFile</span></span> | <span data-ttu-id="09f8a-113">Konfigurační soubor NuGet, který se má použít</span><span class="sxs-lookup"><span data-stu-id="09f8a-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="09f8a-114">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows `~/.nuget/NuGet/NuGet.Config` ) nebo (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="09f8a-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="09f8a-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="09f8a-115">ForceEnglishOutput</span></span> | <span data-ttu-id="09f8a-116">*(3.5 +)* Vynutí, aby soubor NuGet. exe běžel pomocí neutrální jazykové verze určené pro angličtinu.</span><span class="sxs-lookup"><span data-stu-id="09f8a-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="09f8a-117">Help</span><span class="sxs-lookup"><span data-stu-id="09f8a-117">Help</span></span> | <span data-ttu-id="09f8a-118">Zobrazí informace o nápovědě k příkazu.</span><span class="sxs-lookup"><span data-stu-id="09f8a-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="09f8a-119">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="09f8a-119">NonInteractive</span></span> | <span data-ttu-id="09f8a-120">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="09f8a-120">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="09f8a-121">Verbosity</span><span class="sxs-lookup"><span data-stu-id="09f8a-121">Verbosity</span></span> | <span data-ttu-id="09f8a-122">Určuje množství podrobností zobrazených ve výstupu: *normální*, tiché a *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="09f8a-122">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="09f8a-123">Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="09f8a-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="09f8a-124">Příklady</span><span class="sxs-lookup"><span data-stu-id="09f8a-124">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
