---
title: Omezení přenosové rychlosti, rozhraní API NuGet
description: Rozhraní API NuGet budou vyžadovat omezení přenosové rychlosti, aby se zabránilo zneužití.
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 372304255bf8849693947b22539e012ccdd48966
ms.sourcegitcommit: 0a63956bf12aaf1b1b45e680bc8e90f97347988c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/13/2020
ms.locfileid: "83367931"
---
# <a name="rate-limits"></a><span data-ttu-id="6440b-103">Omezení přenosové rychlosti</span><span class="sxs-lookup"><span data-stu-id="6440b-103">Rate Limits</span></span>

<span data-ttu-id="6440b-104">Rozhraní NuGet.org API vynutilo omezení četnosti, aby se zabránilo zneužití.</span><span class="sxs-lookup"><span data-stu-id="6440b-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="6440b-105">Žádosti, které překračují limit přenosové rychlosti, vrátí následující chybu:</span><span class="sxs-lookup"><span data-stu-id="6440b-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="6440b-106">Kromě omezení požadavků pomocí omezení přenosové rychlosti některá rozhraní API také vynutila kvótu.</span><span class="sxs-lookup"><span data-stu-id="6440b-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="6440b-107">Žádosti, které překračují kvótu, vrátí následující chybu:</span><span class="sxs-lookup"><span data-stu-id="6440b-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="6440b-108">V následujících tabulkách jsou uvedeny omezení přenosové rychlosti pro rozhraní NuGet.org API.</span><span class="sxs-lookup"><span data-stu-id="6440b-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="6440b-109">Hledání balíčku</span><span class="sxs-lookup"><span data-stu-id="6440b-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="6440b-110">Doporučujeme používat [rozhraní API pro vyhledávání](search-query-service-resource.md) NuGet. org, protože neodpovídá aktuálně omezené rychlosti.</span><span class="sxs-lookup"><span data-stu-id="6440b-110">We recommend using NuGet.org's [V3 search APIs](search-query-service-resource.md) as it is not rate limited currently.</span></span> <span data-ttu-id="6440b-111">Pro rozhraní API pro vyhledávání V1 a v2 platí následující omezení:</span><span class="sxs-lookup"><span data-stu-id="6440b-111">For V1 and V2 search APIs, the following limits apply:</span></span>

| <span data-ttu-id="6440b-112">Rozhraní API</span><span class="sxs-lookup"><span data-stu-id="6440b-112">API</span></span> | <span data-ttu-id="6440b-113">Typ limitu</span><span class="sxs-lookup"><span data-stu-id="6440b-113">Limit Type</span></span> | <span data-ttu-id="6440b-114">Hodnota limitu</span><span class="sxs-lookup"><span data-stu-id="6440b-114">Limit Value</span></span> | <span data-ttu-id="6440b-115">Případ použití rozhraní API</span><span class="sxs-lookup"><span data-stu-id="6440b-115">API Use Case</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="6440b-116">**Získat**`/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="6440b-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="6440b-117">IP adresa</span><span class="sxs-lookup"><span data-stu-id="6440b-117">IP</span></span> | <span data-ttu-id="6440b-118">1000 minut</span><span class="sxs-lookup"><span data-stu-id="6440b-118">1000 / minute</span></span> | <span data-ttu-id="6440b-119">Dotazování metadat balíčku NuGet prostřednictvím kolekce OData v1 `Packages`</span><span class="sxs-lookup"><span data-stu-id="6440b-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="6440b-120">**Získat**`/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="6440b-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="6440b-121">IP adresa</span><span class="sxs-lookup"><span data-stu-id="6440b-121">IP</span></span> | <span data-ttu-id="6440b-122">3000 minut</span><span class="sxs-lookup"><span data-stu-id="6440b-122">3000 / minute</span></span> | <span data-ttu-id="6440b-123">Hledání balíčků NuGet prostřednictvím koncového bodu pro vyhledávání v1</span><span class="sxs-lookup"><span data-stu-id="6440b-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="6440b-124">**Získat**`/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="6440b-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="6440b-125">IP adresa</span><span class="sxs-lookup"><span data-stu-id="6440b-125">IP</span></span> | <span data-ttu-id="6440b-126">20000 minut</span><span class="sxs-lookup"><span data-stu-id="6440b-126">20000 / minute</span></span> | <span data-ttu-id="6440b-127">Dotaz na metadata balíčku NuGet přes kolekci OData v2 `Packages`</span><span class="sxs-lookup"><span data-stu-id="6440b-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="6440b-128">**Získat**`/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="6440b-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="6440b-129">IP adresa</span><span class="sxs-lookup"><span data-stu-id="6440b-129">IP</span></span> | <span data-ttu-id="6440b-130">100 minut</span><span class="sxs-lookup"><span data-stu-id="6440b-130">100 / minute</span></span> | <span data-ttu-id="6440b-131">Dotaz na počet balíčků NuGet přes v2 `Packages` shromažďování dat OData</span><span class="sxs-lookup"><span data-stu-id="6440b-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="6440b-132">Vložení a odbalení balíčku</span><span class="sxs-lookup"><span data-stu-id="6440b-132">Package Push and Unlist</span></span>

| <span data-ttu-id="6440b-133">Rozhraní API</span><span class="sxs-lookup"><span data-stu-id="6440b-133">API</span></span> | <span data-ttu-id="6440b-134">Typ limitu</span><span class="sxs-lookup"><span data-stu-id="6440b-134">Limit Type</span></span> | <span data-ttu-id="6440b-135">Hodnota limitu</span><span class="sxs-lookup"><span data-stu-id="6440b-135">Limit Value</span></span> | <span data-ttu-id="6440b-136">Případ použití rozhraní API</span><span class="sxs-lookup"><span data-stu-id="6440b-136">API Use Case</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="6440b-137">**Vložit**`/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="6440b-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="6440b-138">Klíč rozhraní API</span><span class="sxs-lookup"><span data-stu-id="6440b-138">API Key</span></span> | <span data-ttu-id="6440b-139">350 za hodinu</span><span class="sxs-lookup"><span data-stu-id="6440b-139">350 / hour</span></span> | <span data-ttu-id="6440b-140">Nahrání nového balíčku NuGet (verze) prostřednictvím nabízeného koncového bodu v2</span><span class="sxs-lookup"><span data-stu-id="6440b-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="6440b-141">**Odstranit**`/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="6440b-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="6440b-142">Klíč rozhraní API</span><span class="sxs-lookup"><span data-stu-id="6440b-142">API Key</span></span> | <span data-ttu-id="6440b-143">250 za hodinu</span><span class="sxs-lookup"><span data-stu-id="6440b-143">250 / hour</span></span> | <span data-ttu-id="6440b-144">Odpisovat balíček NuGet (verze) prostřednictvím koncového bodu v2</span><span class="sxs-lookup"><span data-stu-id="6440b-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 

## <a name="nugetorg-website-page-views"></a><span data-ttu-id="6440b-145">nuget.org zobrazení stránek webu</span><span class="sxs-lookup"><span data-stu-id="6440b-145">nuget.org website page views</span></span>

<span data-ttu-id="6440b-146">Pokud přistupujete k webovým stránkám nuget.org programově, zvažte zkoumání našich dokumentovaných [rozhraní API V3](overview.md).</span><span class="sxs-lookup"><span data-stu-id="6440b-146">If you are accessing the nuget.org web pages programmatically, consider investigating our documented [V3 APIs](overview.md).</span></span> <span data-ttu-id="6440b-147">Tyto koncové body umožňují jednodušší přístup k metadatům a obsahu balíčků.</span><span class="sxs-lookup"><span data-stu-id="6440b-147">These endpoints allow for simpler access to package metadata and content.</span></span> <span data-ttu-id="6440b-148">Rozhraní V3 API má lepší dostupnost a má vyšší výkon než přístup k webovým stránkám galerie NuGet, které jsou určeny pro interakci webového prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="6440b-148">The V3 API has better availability and has higher performance than accessing the NuGet Gallery web pages, which are designed for web browser interaction.</span></span>

| <span data-ttu-id="6440b-149">Rozhraní API</span><span class="sxs-lookup"><span data-stu-id="6440b-149">API</span></span> | <span data-ttu-id="6440b-150">Typ limitu</span><span class="sxs-lookup"><span data-stu-id="6440b-150">Limit Type</span></span> | <span data-ttu-id="6440b-151">Hodnota limitu</span><span class="sxs-lookup"><span data-stu-id="6440b-151">Limit Value</span></span> | <span data-ttu-id="6440b-152">Případ použití rozhraní API</span><span class="sxs-lookup"><span data-stu-id="6440b-152">API Use Case</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="6440b-153">**Získat**`/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="6440b-153">**GET** `/package/{id}/{version}`</span></span> | <span data-ttu-id="6440b-154">IP adresa</span><span class="sxs-lookup"><span data-stu-id="6440b-154">IP</span></span> | <span data-ttu-id="6440b-155">50 minut</span><span class="sxs-lookup"><span data-stu-id="6440b-155">50 / minute</span></span> | <span data-ttu-id="6440b-156">Zobrazit stránku s podrobnostmi balíčku (verze)</span><span class="sxs-lookup"><span data-stu-id="6440b-156">Display package (version) details page.</span></span> 
