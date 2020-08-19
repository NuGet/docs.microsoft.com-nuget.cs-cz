---
title: NuGet CLI – příkaz odstranění
description: Odkaz na příkaz nuget.exe DELETE
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: bec1a778d4986a4cb7ee87e1ef8a98550c96ed57
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622860"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="787d9-103">DELETE – příkaz (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="787d9-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="787d9-104">**Platí pro:** publikování &bullet; **podporovaných verzí balíčku:** vše</span><span class="sxs-lookup"><span data-stu-id="787d9-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="787d9-105">Odstraní nebo zruší výpis balíčku ze zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="787d9-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="787d9-106">V případě nuget.org příkaz DELETE [odpíše balíček](../../nuget-org/policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="787d9-106">For nuget.org, the delete command [unlists the package](../../nuget-org/policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="787d9-107">Využití</span><span class="sxs-lookup"><span data-stu-id="787d9-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="787d9-108">kde `<packageID>` a `<packageVersion>` Identifikujte přesný balíček pro odstranění nebo odseznamování.</span><span class="sxs-lookup"><span data-stu-id="787d9-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="787d9-109">Přesné chování závisí na zdroji.</span><span class="sxs-lookup"><span data-stu-id="787d9-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="787d9-110">Pro místní složky se například odstraní balíček. pro nuget.org balíček není v seznamu.</span><span class="sxs-lookup"><span data-stu-id="787d9-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="787d9-111">Možnosti</span><span class="sxs-lookup"><span data-stu-id="787d9-111">Options</span></span>

- **`-ApiKey`**

  <span data-ttu-id="787d9-112">Klíč rozhraní API pro cílové úložiště</span><span class="sxs-lookup"><span data-stu-id="787d9-112">The API key for the target repository.</span></span> <span data-ttu-id="787d9-113">Pokud není k dispozici, použije se ten, který je zadaný v konfiguračním souboru.</span><span class="sxs-lookup"><span data-stu-id="787d9-113">If not present, the one specified in the config file is used.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="787d9-114">Konfigurační soubor NuGet, který se má použít</span><span class="sxs-lookup"><span data-stu-id="787d9-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="787d9-115">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows) nebo `~/.nuget/NuGet/NuGet.Config` nebo `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="787d9-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="787d9-116">*(3.5 +)* Vynutí spuštění nuget.exe s využitím neutrální jazykové verze založené na angličtině.</span><span class="sxs-lookup"><span data-stu-id="787d9-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="787d9-117">Zobrazí informace o nápovědě k příkazu.</span><span class="sxs-lookup"><span data-stu-id="787d9-117">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="787d9-118">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="787d9-118">Suppresses prompts for user input or confirmations.</span></span>

 - **`-np|-NoPrompt`**

   <span data-ttu-id="787d9-119">Nedotazovat se při odstraňování</span><span class="sxs-lookup"><span data-stu-id="787d9-119">Do not prompt when deleting.</span></span>

 - <span data-ttu-id="787d9-120">**`-NoServiceEndpoint`** Nepřipojí k zdrojové adrese URL rozhraní API/v2/Packages.</span><span class="sxs-lookup"><span data-stu-id="787d9-120">**`-NoServiceEndpoint`** Does not append "api/v2/packages" to the source URL.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="787d9-121">Určuje adresu URL serveru.</span><span class="sxs-lookup"><span data-stu-id="787d9-121">Specifies the server URL.</span></span> <span data-ttu-id="787d9-122">Adresa URL pro nuget.org je `https://api.nuget.org/v3/index.json` .</span><span class="sxs-lookup"><span data-stu-id="787d9-122">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="787d9-123">V případě privátních informačních kanálů nahraďte název hostitele, například *% hostname%/API/V3*.</span><span class="sxs-lookup"><span data-stu-id="787d9-123">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="787d9-124">Určuje množství podrobností zobrazených ve výstupu: `normal` (výchozí), `quiet` nebo `detailed` .</span><span class="sxs-lookup"><span data-stu-id="787d9-124">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="787d9-125">Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="787d9-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="787d9-126">Příklady</span><span class="sxs-lookup"><span data-stu-id="787d9-126">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
