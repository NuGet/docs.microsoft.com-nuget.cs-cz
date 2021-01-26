---
title: NuGet CLI – příkaz setapikey
description: Odkaz na příkaz nuget.exe setapikey
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3e0c2f84e336e0a642b1b5e815e74a1fb0878467
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780014"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="7074e-103">setapikey – příkaz (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="7074e-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="7074e-104">**Platí pro:** spotřeba balíčku, publikování &bullet; **podporovaných verzí:** vše</span><span class="sxs-lookup"><span data-stu-id="7074e-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="7074e-105">Uloží klíč rozhraní API pro danou adresu URL serveru `NuGet.Config` tak, aby se nemusel zadat pro následné příkazy.</span><span class="sxs-lookup"><span data-stu-id="7074e-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="7074e-106">Využití</span><span class="sxs-lookup"><span data-stu-id="7074e-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="7074e-107">kde `<source>` identifikuje server a `<key>` je klíč, který se má uložit.</span><span class="sxs-lookup"><span data-stu-id="7074e-107">where `<source>` identifies the server and `<key>` is the key to save.</span></span> <span data-ttu-id="7074e-108">Pokud `<source>` je hodnota vynechána, předpokládá se NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="7074e-108">If `<source>` is omitted, nuget.org is assumed.</span></span> 

> [!NOTE]
> <span data-ttu-id="7074e-109">Klíč rozhraní API se nepoužívá pro ověřování pomocí privátního informačního kanálu.</span><span class="sxs-lookup"><span data-stu-id="7074e-109">API key is not used for authenticating with the private feed.</span></span> <span data-ttu-id="7074e-110">Pro správu přihlašovacích údajů pro ověřování ve zdroji použijte [ `nuget sources` příkaz](../cli-reference/cli-ref-sources.md) .</span><span class="sxs-lookup"><span data-stu-id="7074e-110">Refer to [`nuget sources` command](../cli-reference/cli-ref-sources.md) to manage credentials for authenticating with the source.</span></span>
> <span data-ttu-id="7074e-111">Klíče rozhraní API lze získat z jednotlivých serverů NuGet.</span><span class="sxs-lookup"><span data-stu-id="7074e-111">API keys can be obtained from the individual NuGet servers.</span></span> <span data-ttu-id="7074e-112">Pokud chcete vytvořit a spravovat APIKeys pro nuget.org, přečtěte si téma [získání-a-API-Key](../../nuget-org/scoped-api-keys.md#acquire-an-api-key) .</span><span class="sxs-lookup"><span data-stu-id="7074e-112">To create and manage APIKeys for nuget.org refer to [acquire-an-api-key](../../nuget-org/scoped-api-keys.md#acquire-an-api-key)</span></span>

## <a name="options"></a><span data-ttu-id="7074e-113">Možnosti</span><span class="sxs-lookup"><span data-stu-id="7074e-113">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="7074e-114">Konfigurační soubor NuGet, který se má použít</span><span class="sxs-lookup"><span data-stu-id="7074e-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="7074e-115">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows) nebo `~/.nuget/NuGet/NuGet.Config` nebo `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="7074e-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="7074e-116">*(3.5 +)* Vynutí spuštění nuget.exe s využitím neutrální jazykové verze založené na angličtině.</span><span class="sxs-lookup"><span data-stu-id="7074e-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="7074e-117">Zobrazí informace o nápovědě k příkazu.</span><span class="sxs-lookup"><span data-stu-id="7074e-117">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="7074e-118">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="7074e-118">Suppresses prompts for user input or confirmations.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="7074e-119">Adresa URL serveru, kde je klíč rozhraní API platný</span><span class="sxs-lookup"><span data-stu-id="7074e-119">Server URL where the API key is valid.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="7074e-120">Určuje množství podrobností zobrazených ve výstupu: `normal` (výchozí), `quiet` nebo `detailed` .</span><span class="sxs-lookup"><span data-stu-id="7074e-120">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="7074e-121">Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="7074e-121">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="7074e-122">Příklady</span><span class="sxs-lookup"><span data-stu-id="7074e-122">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
