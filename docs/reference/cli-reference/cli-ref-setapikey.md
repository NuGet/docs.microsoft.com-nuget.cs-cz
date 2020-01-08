---
title: NuGet CLI – příkaz setapikey
description: Referenční informace o příkazu NuGet. exe setapikey
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0e2119953e6d07cd3571f156fa0b2665de49f963
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383966"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="46df8-103">setapikey – příkaz (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="46df8-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="46df8-104">**Platí pro:** spotřeba balíčku, publikování &bullet; **podporovaných verzích:** vše</span><span class="sxs-lookup"><span data-stu-id="46df8-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="46df8-105">Uloží klíč rozhraní API pro danou adresu URL serveru do `NuGet.Config`, aby se nemusel zadat pro následné příkazy.</span><span class="sxs-lookup"><span data-stu-id="46df8-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="46df8-106">Použití</span><span class="sxs-lookup"><span data-stu-id="46df8-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="46df8-107">kde `<source>` identifikuje server a `<key>` je klíč nebo heslo, které se má uložit.</span><span class="sxs-lookup"><span data-stu-id="46df8-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="46df8-108">Pokud je hodnota `<source>` vynechána, předpokládá se nuget.org.</span><span class="sxs-lookup"><span data-stu-id="46df8-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

> [!NOTE]
> <span data-ttu-id="46df8-109">Klíč rozhraní API se nepoužívá pro ověřování pomocí privátního informačního kanálu.</span><span class="sxs-lookup"><span data-stu-id="46df8-109">API key is not used for authenticating with the private feed.</span></span> <span data-ttu-id="46df8-110">Pokud chcete spravovat přihlašovací údaje pro ověřování ve zdroji, přečtěte si [`nuget sources` příkaz](../cli-reference/cli-ref-sources.md) .</span><span class="sxs-lookup"><span data-stu-id="46df8-110">Refer to [`nuget sources` command](../cli-reference/cli-ref-sources.md) to manage credentials for authenticating with the source.</span></span>

## <a name="options"></a><span data-ttu-id="46df8-111">Možnosti</span><span class="sxs-lookup"><span data-stu-id="46df8-111">Options</span></span>

| <span data-ttu-id="46df8-112">Možnost</span><span class="sxs-lookup"><span data-stu-id="46df8-112">Option</span></span> | <span data-ttu-id="46df8-113">Popis</span><span class="sxs-lookup"><span data-stu-id="46df8-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="46df8-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="46df8-114">ConfigFile</span></span> | <span data-ttu-id="46df8-115">Konfigurační soubor NuGet, který se má použít</span><span class="sxs-lookup"><span data-stu-id="46df8-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="46df8-116">Pokud není zadaný, použije se `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="46df8-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="46df8-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="46df8-117">ForceEnglishOutput</span></span> | <span data-ttu-id="46df8-118">*(3.5 +)* Vynutí, aby soubor NuGet. exe běžel pomocí neutrální jazykové verze určené pro angličtinu.</span><span class="sxs-lookup"><span data-stu-id="46df8-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="46df8-119">Nápověda</span><span class="sxs-lookup"><span data-stu-id="46df8-119">Help</span></span> | <span data-ttu-id="46df8-120">Zobrazí informace o nápovědě k příkazu.</span><span class="sxs-lookup"><span data-stu-id="46df8-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="46df8-121">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="46df8-121">NonInteractive</span></span> | <span data-ttu-id="46df8-122">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="46df8-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="46df8-123">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="46df8-123">Verbosity</span></span> | <span data-ttu-id="46df8-124">Určuje množství podrobností zobrazených ve výstupu: *normální*, *tiché*a *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="46df8-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="46df8-125">Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="46df8-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="46df8-126">Příklady</span><span class="sxs-lookup"><span data-stu-id="46df8-126">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
