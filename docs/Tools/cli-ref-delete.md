---
title: "Příkaz delete NuGet rozhraní příkazového řádku | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: c213a07a-711d-47e0-9ee6-1d582e6cdb69
description: "Referenční dokumentace pro příkaz delete nuget.exe"
keywords: "nuget odstranit odkaz, odstraňte příkaz balíčku"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 92af9dc356f3932347864976496e0ba1216496c9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="61f50-104">Odstranit příkazu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="61f50-104">delete command (NuGet CLI)</span></span>

<span data-ttu-id="61f50-105">**Platí pro:** balíček publikování &bullet; **podporované verze:** všechny</span><span class="sxs-lookup"><span data-stu-id="61f50-105">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="61f50-106">Odstraní nebo unlists balíčku ze zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="61f50-106">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="61f50-107">Pro nuget.org, příkaz delete [unlists balíček](../policies/Deleting-Packages.md).</span><span class="sxs-lookup"><span data-stu-id="61f50-107">For nuget.org, the delete command [unlists the package](../policies/Deleting-Packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="61f50-108">Použití</span><span class="sxs-lookup"><span data-stu-id="61f50-108">Usage</span></span>

```
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="61f50-109">kde `<packageID>` a `<packageVersion>` přesný balíček odstranit nebo unlist identifikovat.</span><span class="sxs-lookup"><span data-stu-id="61f50-109">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="61f50-110">Přesný postup závisí na zdroji.</span><span class="sxs-lookup"><span data-stu-id="61f50-110">The exact behavior depends on the source.</span></span> <span data-ttu-id="61f50-111">Pro místní složky, například daný balíček byl odstraněn; balíček není pro nuget.org neuvedené.</span><span class="sxs-lookup"><span data-stu-id="61f50-111">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="61f50-112">Možnosti</span><span class="sxs-lookup"><span data-stu-id="61f50-112">Options</span></span>

| <span data-ttu-id="61f50-113">Možnost</span><span class="sxs-lookup"><span data-stu-id="61f50-113">Option</span></span> | <span data-ttu-id="61f50-114">Popis</span><span class="sxs-lookup"><span data-stu-id="61f50-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="61f50-115">apiKey</span><span class="sxs-lookup"><span data-stu-id="61f50-115">ApiKey</span></span> | <span data-ttu-id="61f50-116">Klíč rozhraní API pro cílové úložiště.</span><span class="sxs-lookup"><span data-stu-id="61f50-116">The API key for the target repository.</span></span> <span data-ttu-id="61f50-117">Pokud není přítomný, ten zadat *%AppData%\NuGet\NuGet.Config* se používá.</span><span class="sxs-lookup"><span data-stu-id="61f50-117">If not present, the one specified in *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="61f50-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="61f50-118">ConfigFile</span></span> | <span data-ttu-id="61f50-119">*(2.5 +)*  NuGet konfiguračním souboru použít.</span><span class="sxs-lookup"><span data-stu-id="61f50-119">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="61f50-120">Pokud není zadaný, *%AppData%\NuGet\NuGet.Config* se používá.</span><span class="sxs-lookup"><span data-stu-id="61f50-120">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="61f50-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="61f50-121">ForceEnglishOutput</span></span> | <span data-ttu-id="61f50-122">*(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze.</span><span class="sxs-lookup"><span data-stu-id="61f50-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="61f50-123">Nápověda</span><span class="sxs-lookup"><span data-stu-id="61f50-123">Help</span></span> | <span data-ttu-id="61f50-124">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="61f50-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="61f50-125">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="61f50-125">NonInteractive</span></span> | <span data-ttu-id="61f50-126">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="61f50-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="61f50-127">Zdroj</span><span class="sxs-lookup"><span data-stu-id="61f50-127">Source</span></span> | <span data-ttu-id="61f50-128">Určuje adresu URL serveru.</span><span class="sxs-lookup"><span data-stu-id="61f50-128">Specifies the server URL.</span></span> <span data-ttu-id="61f50-129">Adresa URL nuget.org je `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="61f50-129">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="61f50-130">Pro privátní informační kanály, nahraďte název hostitele, například *%hostname%/api/v3*.</span><span class="sxs-lookup"><span data-stu-id="61f50-130">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="61f50-131">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="61f50-131">Verbosity</span></span> | <span data-ttu-id="61f50-132">Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="61f50-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="61f50-133">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="61f50-133">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="61f50-134">Příklady</span><span class="sxs-lookup"><span data-stu-id="61f50-134">Examples</span></span>

```
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
