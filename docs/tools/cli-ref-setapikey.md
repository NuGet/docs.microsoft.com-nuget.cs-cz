---
title: Příkaz setapikey NuGet rozhraní příkazového řádku
description: Referenční dokumentace pro příkaz setapikey nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 66fc62074b4e7c39ff2ed6b515eee9f821530536
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817681"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="66f74-103">příkaz setapikey (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="66f74-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="66f74-104">**Platí pro:** spotřeba balíčku, publikování &bullet; **podporované verze:** všechny</span><span class="sxs-lookup"><span data-stu-id="66f74-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="66f74-105">Uloží klíč rozhraní API pro adresu URL daného serveru do `NuGet.Config` tak, aby nemusí být zadaný pro následné příkazy.</span><span class="sxs-lookup"><span data-stu-id="66f74-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="66f74-106">Použití</span><span class="sxs-lookup"><span data-stu-id="66f74-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="66f74-107">kde `<source>` identifikuje server a `<key>` je klíč nebo heslo, abyste uložili.</span><span class="sxs-lookup"><span data-stu-id="66f74-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="66f74-108">Pokud `<source>` je tento parametr vynechán, předpokládá se nuget.org.</span><span class="sxs-lookup"><span data-stu-id="66f74-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="66f74-109">Možnosti</span><span class="sxs-lookup"><span data-stu-id="66f74-109">Options</span></span>

| <span data-ttu-id="66f74-110">Možnost</span><span class="sxs-lookup"><span data-stu-id="66f74-110">Option</span></span> | <span data-ttu-id="66f74-111">Popis</span><span class="sxs-lookup"><span data-stu-id="66f74-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="66f74-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="66f74-112">ConfigFile</span></span> | <span data-ttu-id="66f74-113">Konfigurační soubor NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="66f74-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="66f74-114">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.</span><span class="sxs-lookup"><span data-stu-id="66f74-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="66f74-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="66f74-115">ForceEnglishOutput</span></span> | <span data-ttu-id="66f74-116">*(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze.</span><span class="sxs-lookup"><span data-stu-id="66f74-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="66f74-117">Nápověda</span><span class="sxs-lookup"><span data-stu-id="66f74-117">Help</span></span> | <span data-ttu-id="66f74-118">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="66f74-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="66f74-119">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="66f74-119">NonInteractive</span></span> | <span data-ttu-id="66f74-120">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="66f74-120">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="66f74-121">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="66f74-121">Verbosity</span></span> | <span data-ttu-id="66f74-122">Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="66f74-122">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="66f74-123">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="66f74-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="66f74-124">Příklady</span><span class="sxs-lookup"><span data-stu-id="66f74-124">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
