---
title: Příkaz delete NuGet rozhraní příkazového řádku
description: Referenční dokumentace pro příkaz delete nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 1db00a32d777f1c0247f855bf57a0dcf1c6734ae
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="b815f-103">Odstranit příkazu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="b815f-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="b815f-104">**Platí pro:** balíček publikování &bullet; **podporované verze:** všechny</span><span class="sxs-lookup"><span data-stu-id="b815f-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="b815f-105">Odstraní nebo unlists balíčku ze zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="b815f-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="b815f-106">Pro nuget.org, příkaz delete [unlists balíček](../policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="b815f-106">For nuget.org, the delete command [unlists the package](../policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="b815f-107">Použití</span><span class="sxs-lookup"><span data-stu-id="b815f-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="b815f-108">kde `<packageID>` a `<packageVersion>` přesný balíček odstranit nebo unlist identifikovat.</span><span class="sxs-lookup"><span data-stu-id="b815f-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="b815f-109">Přesný postup závisí na zdroji.</span><span class="sxs-lookup"><span data-stu-id="b815f-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="b815f-110">Pro místní složky, například daný balíček byl odstraněn; balíček není pro nuget.org neuvedené.</span><span class="sxs-lookup"><span data-stu-id="b815f-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="b815f-111">Možnosti</span><span class="sxs-lookup"><span data-stu-id="b815f-111">Options</span></span>

| <span data-ttu-id="b815f-112">Možnost</span><span class="sxs-lookup"><span data-stu-id="b815f-112">Option</span></span> | <span data-ttu-id="b815f-113">Popis</span><span class="sxs-lookup"><span data-stu-id="b815f-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b815f-114">apiKey</span><span class="sxs-lookup"><span data-stu-id="b815f-114">ApiKey</span></span> | <span data-ttu-id="b815f-115">Klíč rozhraní API pro cílové úložiště.</span><span class="sxs-lookup"><span data-stu-id="b815f-115">The API key for the target repository.</span></span> <span data-ttu-id="b815f-116">Pokud není přítomný, použije se verze zadaná v konfiguračním souboru.</span><span class="sxs-lookup"><span data-stu-id="b815f-116">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="b815f-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="b815f-117">ConfigFile</span></span> | <span data-ttu-id="b815f-118">Konfigurační soubor NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="b815f-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b815f-119">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.</span><span class="sxs-lookup"><span data-stu-id="b815f-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="b815f-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="b815f-120">ForceEnglishOutput</span></span> | <span data-ttu-id="b815f-121">*(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze.</span><span class="sxs-lookup"><span data-stu-id="b815f-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="b815f-122">Nápověda</span><span class="sxs-lookup"><span data-stu-id="b815f-122">Help</span></span> | <span data-ttu-id="b815f-123">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="b815f-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="b815f-124">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="b815f-124">NonInteractive</span></span> | <span data-ttu-id="b815f-125">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="b815f-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="b815f-126">Zdroj</span><span class="sxs-lookup"><span data-stu-id="b815f-126">Source</span></span> | <span data-ttu-id="b815f-127">Určuje adresu URL serveru.</span><span class="sxs-lookup"><span data-stu-id="b815f-127">Specifies the server URL.</span></span> <span data-ttu-id="b815f-128">Adresa URL nuget.org je `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="b815f-128">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="b815f-129">Pro privátní informační kanály, nahraďte název hostitele, například *%hostname%/api/v3*.</span><span class="sxs-lookup"><span data-stu-id="b815f-129">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="b815f-130">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="b815f-130">Verbosity</span></span> | <span data-ttu-id="b815f-131">Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="b815f-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="b815f-132">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b815f-132">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="b815f-133">Příklady</span><span class="sxs-lookup"><span data-stu-id="b815f-133">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
