---
title: "Příkaz setapikey NuGet rozhraní příkazového řádku | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenční dokumentace pro příkaz setapikey nuget.exe"
keywords: "referenční dokumentace setapikey nuget, setapikey příkaz"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ca6caddbf1404bcaa1ca068c9556f7cf0c651947
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="2e961-104">příkaz setapikey (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="2e961-104">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="2e961-105">**Platí pro:** spotřeba balíčku, publikování &bullet; **podporované verze:** všechny</span><span class="sxs-lookup"><span data-stu-id="2e961-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="2e961-106">Uloží klíč rozhraní API pro adresu URL daného serveru do `NuGet.Config` tak, aby nemusí být zadaný pro následné příkazy.</span><span class="sxs-lookup"><span data-stu-id="2e961-106">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="2e961-107">Použití</span><span class="sxs-lookup"><span data-stu-id="2e961-107">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="2e961-108">kde `<source>` identifikuje server a `<key>` je klíč nebo heslo, abyste uložili.</span><span class="sxs-lookup"><span data-stu-id="2e961-108">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="2e961-109">Pokud `<source>` je tento parametr vynechán, předpokládá se nuget.org.</span><span class="sxs-lookup"><span data-stu-id="2e961-109">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="2e961-110">Možnosti</span><span class="sxs-lookup"><span data-stu-id="2e961-110">Options</span></span>

| <span data-ttu-id="2e961-111">Možnost</span><span class="sxs-lookup"><span data-stu-id="2e961-111">Option</span></span> | <span data-ttu-id="2e961-112">Popis</span><span class="sxs-lookup"><span data-stu-id="2e961-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2e961-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="2e961-113">ConfigFile</span></span> | <span data-ttu-id="2e961-114">Konfigurační soubor NuGet chcete upravit.</span><span class="sxs-lookup"><span data-stu-id="2e961-114">The NuGet configuration file to modify.</span></span> <span data-ttu-id="2e961-115">Pokud není zadaný, *%AppData%\NuGet\NuGet.Config* se používá.</span><span class="sxs-lookup"><span data-stu-id="2e961-115">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="2e961-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="2e961-116">ForceEnglishOutput</span></span> | <span data-ttu-id="2e961-117">*(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze.</span><span class="sxs-lookup"><span data-stu-id="2e961-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="2e961-118">Nápověda</span><span class="sxs-lookup"><span data-stu-id="2e961-118">Help</span></span> | <span data-ttu-id="2e961-119">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="2e961-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="2e961-120">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="2e961-120">NonInteractive</span></span> | <span data-ttu-id="2e961-121">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="2e961-121">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="2e961-122">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="2e961-122">Verbosity</span></span> | <span data-ttu-id="2e961-123">Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="2e961-123">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="2e961-124">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="2e961-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="2e961-125">Příklady</span><span class="sxs-lookup"><span data-stu-id="2e961-125">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
