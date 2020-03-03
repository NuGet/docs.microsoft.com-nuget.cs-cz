---
title: NuGet CLI – příkaz setapikey
description: Referenční informace o příkazu NuGet. exe setapikey
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: e06cfb5b355dfae8104090db7babdecdf9e9fec1
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231224"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="1917c-103">setapikey – příkaz (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="1917c-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="1917c-104">**Platí pro:** spotřeba balíčku, publikování &bullet; **podporovaných verzích:** vše</span><span class="sxs-lookup"><span data-stu-id="1917c-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="1917c-105">Uloží klíč rozhraní API pro danou adresu URL serveru do `NuGet.Config`, aby se nemusel zadat pro následné příkazy.</span><span class="sxs-lookup"><span data-stu-id="1917c-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="1917c-106">Využití</span><span class="sxs-lookup"><span data-stu-id="1917c-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="1917c-107">kde `<source>` identifikuje server a `<key>` je klíč, který se má uložit.</span><span class="sxs-lookup"><span data-stu-id="1917c-107">where `<source>` identifies the server and `<key>` is the key to save.</span></span> <span data-ttu-id="1917c-108">Pokud je hodnota `<source>` vynechána, předpokládá se nuget.org.</span><span class="sxs-lookup"><span data-stu-id="1917c-108">If `<source>` is omitted, nuget.org is assumed.</span></span> 

> [!NOTE]
> <span data-ttu-id="1917c-109">Klíč rozhraní API se nepoužívá pro ověřování pomocí privátního informačního kanálu.</span><span class="sxs-lookup"><span data-stu-id="1917c-109">API key is not used for authenticating with the private feed.</span></span> <span data-ttu-id="1917c-110">Pokud chcete spravovat přihlašovací údaje pro ověřování ve zdroji, přečtěte si [`nuget sources` příkaz](../cli-reference/cli-ref-sources.md) .</span><span class="sxs-lookup"><span data-stu-id="1917c-110">Refer to [`nuget sources` command](../cli-reference/cli-ref-sources.md) to manage credentials for authenticating with the source.</span></span>
> <span data-ttu-id="1917c-111">Klíče rozhraní API lze získat z jednotlivých serverů NuGet.</span><span class="sxs-lookup"><span data-stu-id="1917c-111">API keys can be obtained from the individual NuGet servers.</span></span> <span data-ttu-id="1917c-112">Pokud chcete vytvořit a spravovat APIKeys pro nuget.org, přečtěte si téma [Publishing-API-Key](../../quickstart/includes/publish-api-key.md) .</span><span class="sxs-lookup"><span data-stu-id="1917c-112">To create and manage APIKeys for nuget.org refer to [publish-api-key](../../quickstart/includes/publish-api-key.md)</span></span>

## <a name="options"></a><span data-ttu-id="1917c-113">Možnosti</span><span class="sxs-lookup"><span data-stu-id="1917c-113">Options</span></span>

| <span data-ttu-id="1917c-114">Možnost</span><span class="sxs-lookup"><span data-stu-id="1917c-114">Option</span></span> | <span data-ttu-id="1917c-115">Popis</span><span class="sxs-lookup"><span data-stu-id="1917c-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1917c-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="1917c-116">ConfigFile</span></span> | <span data-ttu-id="1917c-117">Konfigurační soubor NuGet, který se má použít</span><span class="sxs-lookup"><span data-stu-id="1917c-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="1917c-118">Pokud není zadaný, použije se `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="1917c-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="1917c-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="1917c-119">ForceEnglishOutput</span></span> | <span data-ttu-id="1917c-120">*(3.5 +)* Vynutí, aby soubor NuGet. exe běžel pomocí neutrální jazykové verze určené pro angličtinu.</span><span class="sxs-lookup"><span data-stu-id="1917c-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="1917c-121">Nápověda</span><span class="sxs-lookup"><span data-stu-id="1917c-121">Help</span></span> | <span data-ttu-id="1917c-122">Zobrazí informace o nápovědě k příkazu.</span><span class="sxs-lookup"><span data-stu-id="1917c-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="1917c-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="1917c-123">NonInteractive</span></span> | <span data-ttu-id="1917c-124">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="1917c-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="1917c-125">Verbosity</span><span class="sxs-lookup"><span data-stu-id="1917c-125">Verbosity</span></span> | <span data-ttu-id="1917c-126">Určuje množství podrobností zobrazených ve výstupu: *normální*, *tiché*a *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="1917c-126">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="1917c-127">Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="1917c-127">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="1917c-128">Příklady</span><span class="sxs-lookup"><span data-stu-id="1917c-128">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
