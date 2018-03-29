---
title: Příkaz setapikey NuGet rozhraní příkazového řádku | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referenční dokumentace pro příkaz setapikey nuget.exe
keywords: referenční dokumentace setapikey nuget, setapikey příkaz
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 696ccf9df5af487d3bf75925c1c1e0d1d1bf7f7b
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="6308a-104">příkaz setapikey (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="6308a-104">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="6308a-105">**Platí pro:** spotřeba balíčku, publikování &bullet; **podporované verze:** všechny</span><span class="sxs-lookup"><span data-stu-id="6308a-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="6308a-106">Uloží klíč rozhraní API pro adresu URL daného serveru do `NuGet.Config` tak, aby nemusí být zadaný pro následné příkazy.</span><span class="sxs-lookup"><span data-stu-id="6308a-106">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="6308a-107">Použití</span><span class="sxs-lookup"><span data-stu-id="6308a-107">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="6308a-108">kde `<source>` identifikuje server a `<key>` je klíč nebo heslo, abyste uložili.</span><span class="sxs-lookup"><span data-stu-id="6308a-108">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="6308a-109">Pokud `<source>` je tento parametr vynechán, předpokládá se nuget.org.</span><span class="sxs-lookup"><span data-stu-id="6308a-109">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="6308a-110">Možnosti</span><span class="sxs-lookup"><span data-stu-id="6308a-110">Options</span></span>

| <span data-ttu-id="6308a-111">Možnost</span><span class="sxs-lookup"><span data-stu-id="6308a-111">Option</span></span> | <span data-ttu-id="6308a-112">Popis</span><span class="sxs-lookup"><span data-stu-id="6308a-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6308a-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="6308a-113">ConfigFile</span></span> | <span data-ttu-id="6308a-114">Konfigurační soubor NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="6308a-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="6308a-115">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.</span><span class="sxs-lookup"><span data-stu-id="6308a-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="6308a-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="6308a-116">ForceEnglishOutput</span></span> | <span data-ttu-id="6308a-117">*(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze.</span><span class="sxs-lookup"><span data-stu-id="6308a-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="6308a-118">Nápověda</span><span class="sxs-lookup"><span data-stu-id="6308a-118">Help</span></span> | <span data-ttu-id="6308a-119">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="6308a-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="6308a-120">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="6308a-120">NonInteractive</span></span> | <span data-ttu-id="6308a-121">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="6308a-121">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="6308a-122">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="6308a-122">Verbosity</span></span> | <span data-ttu-id="6308a-123">Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="6308a-123">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="6308a-124">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="6308a-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="6308a-125">Příklady</span><span class="sxs-lookup"><span data-stu-id="6308a-125">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
