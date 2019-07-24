---
title: NuGet CLI – příkaz odstranění
description: Referenční informace o příkazu NuGet. exe DELETE
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5185bc8b89f645a0a0f4d3241b5fa04e09560ede
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328354"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="365da-103">DELETE – příkaz (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="365da-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="365da-104">**Platí pro:** publikování &bullet; **podporovaných verzí balíčku:** vše</span><span class="sxs-lookup"><span data-stu-id="365da-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="365da-105">Odstraní nebo zruší výpis balíčku ze zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="365da-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="365da-106">V případě nuget.org příkaz DELETE [odpíše balíček](../../nuget-org/policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="365da-106">For nuget.org, the delete command [unlists the package](../../nuget-org/policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="365da-107">Použití</span><span class="sxs-lookup"><span data-stu-id="365da-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="365da-108">kde `<packageID>` a`<packageVersion>` Identifikujte přesný balíček pro odstranění nebo odseznamování.</span><span class="sxs-lookup"><span data-stu-id="365da-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="365da-109">Přesné chování závisí na zdroji.</span><span class="sxs-lookup"><span data-stu-id="365da-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="365da-110">Pro místní složky se například odstraní balíček. pro nuget.org balíček není v seznamu.</span><span class="sxs-lookup"><span data-stu-id="365da-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="365da-111">Možnosti</span><span class="sxs-lookup"><span data-stu-id="365da-111">Options</span></span>

| <span data-ttu-id="365da-112">Možnost</span><span class="sxs-lookup"><span data-stu-id="365da-112">Option</span></span> | <span data-ttu-id="365da-113">Popis</span><span class="sxs-lookup"><span data-stu-id="365da-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="365da-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="365da-114">ApiKey</span></span> | <span data-ttu-id="365da-115">Klíč rozhraní API pro cílové úložiště</span><span class="sxs-lookup"><span data-stu-id="365da-115">The API key for the target repository.</span></span> <span data-ttu-id="365da-116">Pokud není k dispozici, použije se ten, který je zadaný v konfiguračním souboru.</span><span class="sxs-lookup"><span data-stu-id="365da-116">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="365da-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="365da-117">ConfigFile</span></span> | <span data-ttu-id="365da-118">Konfigurační soubor NuGet, který se má použít</span><span class="sxs-lookup"><span data-stu-id="365da-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="365da-119">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows `~/.nuget/NuGet/NuGet.Config` ) nebo (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="365da-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="365da-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="365da-120">ForceEnglishOutput</span></span> | <span data-ttu-id="365da-121">*(3.5 +)* Vynutí, aby soubor NuGet. exe běžel pomocí neutrální jazykové verze určené pro angličtinu.</span><span class="sxs-lookup"><span data-stu-id="365da-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="365da-122">Help</span><span class="sxs-lookup"><span data-stu-id="365da-122">Help</span></span> | <span data-ttu-id="365da-123">Zobrazí informace o nápovědě k příkazu.</span><span class="sxs-lookup"><span data-stu-id="365da-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="365da-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="365da-124">NonInteractive</span></span> | <span data-ttu-id="365da-125">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="365da-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="365da-126">Source</span><span class="sxs-lookup"><span data-stu-id="365da-126">Source</span></span> | <span data-ttu-id="365da-127">Určuje adresu URL serveru.</span><span class="sxs-lookup"><span data-stu-id="365da-127">Specifies the server URL.</span></span> <span data-ttu-id="365da-128">Adresa URL pro nuget.org je `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="365da-128">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="365da-129">V případě privátních informačních kanálů nahraďte název hostitele, například *% hostname%/API/V3*.</span><span class="sxs-lookup"><span data-stu-id="365da-129">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="365da-130">Verbosity</span><span class="sxs-lookup"><span data-stu-id="365da-130">Verbosity</span></span> | <span data-ttu-id="365da-131">Určuje množství podrobností zobrazených ve výstupu: *normální*, tiché a *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="365da-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="365da-132">Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="365da-132">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="365da-133">Příklady</span><span class="sxs-lookup"><span data-stu-id="365da-133">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
