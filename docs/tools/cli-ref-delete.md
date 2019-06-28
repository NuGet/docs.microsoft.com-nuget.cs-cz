---
title: Příkaz rozhraní příkazového řádku NuGet delete
description: Referenční informace pro příkaz delete nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3ea2dc3e87d0a626704fe5623d39eaf5bd3f3446
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426112"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="42d5e-103">Odstranit příkazu (rozhraní příkazového řádku NuGet)</span><span class="sxs-lookup"><span data-stu-id="42d5e-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="42d5e-104">**Platí pro:** balíček publikování &bullet; **podporované verze:** všechny</span><span class="sxs-lookup"><span data-stu-id="42d5e-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="42d5e-105">Odstraní nebo unlists balíčku ze zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="42d5e-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="42d5e-106">Pro nuget.org, příkazem k odstranění [unlists balíček](../nuget-org/policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="42d5e-106">For nuget.org, the delete command [unlists the package](../nuget-org/policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="42d5e-107">Použití</span><span class="sxs-lookup"><span data-stu-id="42d5e-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="42d5e-108">kde `<packageID>` a `<packageVersion>` určit přesné balíček odstranit nebo vyjmutí ze seznamu.</span><span class="sxs-lookup"><span data-stu-id="42d5e-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="42d5e-109">Přesné chování závisí na zdroji.</span><span class="sxs-lookup"><span data-stu-id="42d5e-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="42d5e-110">Pro místní složky například balíček se odstraní; Tento balíček představuje pro nuget.org neuvedené v seznamu.</span><span class="sxs-lookup"><span data-stu-id="42d5e-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="42d5e-111">Možnosti</span><span class="sxs-lookup"><span data-stu-id="42d5e-111">Options</span></span>

| <span data-ttu-id="42d5e-112">Možnost</span><span class="sxs-lookup"><span data-stu-id="42d5e-112">Option</span></span> | <span data-ttu-id="42d5e-113">Popis</span><span class="sxs-lookup"><span data-stu-id="42d5e-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="42d5e-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="42d5e-114">ApiKey</span></span> | <span data-ttu-id="42d5e-115">Klíč rozhraní API pro cílového úložiště.</span><span class="sxs-lookup"><span data-stu-id="42d5e-115">The API key for the target repository.</span></span> <span data-ttu-id="42d5e-116">Pokud není k dispozici, použije se verze zadaná v konfiguračním souboru.</span><span class="sxs-lookup"><span data-stu-id="42d5e-116">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="42d5e-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="42d5e-117">ConfigFile</span></span> | <span data-ttu-id="42d5e-118">Konfigurační soubor NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="42d5e-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="42d5e-119">Pokud není zadán, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.</span><span class="sxs-lookup"><span data-stu-id="42d5e-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="42d5e-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="42d5e-120">ForceEnglishOutput</span></span> | <span data-ttu-id="42d5e-121">*(3.5 +)*  Vynutí nuget.exe pro spuštění pomocí neutrální, základem je angličtina jazyková verze.</span><span class="sxs-lookup"><span data-stu-id="42d5e-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="42d5e-122">Help</span><span class="sxs-lookup"><span data-stu-id="42d5e-122">Help</span></span> | <span data-ttu-id="42d5e-123">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="42d5e-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="42d5e-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="42d5e-124">NonInteractive</span></span> | <span data-ttu-id="42d5e-125">Potlačí vyzve k zadání uživatele o vstup ani potvrzení.</span><span class="sxs-lookup"><span data-stu-id="42d5e-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="42d5e-126">Source</span><span class="sxs-lookup"><span data-stu-id="42d5e-126">Source</span></span> | <span data-ttu-id="42d5e-127">Určuje adresu URL serveru.</span><span class="sxs-lookup"><span data-stu-id="42d5e-127">Specifies the server URL.</span></span> <span data-ttu-id="42d5e-128">Adresa URL nuget.org `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="42d5e-128">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="42d5e-129">Pro privátní kanály, nahraďte název hostitele, například *%hostname%/api/v3*.</span><span class="sxs-lookup"><span data-stu-id="42d5e-129">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="42d5e-130">Verbosity</span><span class="sxs-lookup"><span data-stu-id="42d5e-130">Verbosity</span></span> | <span data-ttu-id="42d5e-131">Určuje množství podrobností, na které se zobrazí ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="42d5e-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="42d5e-132">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="42d5e-132">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="42d5e-133">Příklady</span><span class="sxs-lookup"><span data-stu-id="42d5e-133">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
