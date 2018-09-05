---
title: Omezení rozhraní API Nugetu přenosové rychlosti
description: Rozhraní API pro NuGet se vynucovat omezení přenosové rychlosti, aby se zabránilo zneužití.
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 70b478ae17cd10b17f9d6ecb0f5776c1effcea58
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548674"
---
# <a name="rate-limits"></a><span data-ttu-id="c981d-103">Omezení přenosové rychlosti</span><span class="sxs-lookup"><span data-stu-id="c981d-103">Rate Limits</span></span>

<span data-ttu-id="c981d-104">Rozhraní API NuGet.org vynucuje omezení rychlosti, aby se zabránilo zneužití.</span><span class="sxs-lookup"><span data-stu-id="c981d-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="c981d-105">Požadavky, které překračují omezení četnosti se vrátí následující chybu:</span><span class="sxs-lookup"><span data-stu-id="c981d-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="c981d-106">Kromě omezení pomocí omezení přenosové rychlosti požadavků některá rozhraní API taky vynutit kvóty.</span><span class="sxs-lookup"><span data-stu-id="c981d-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="c981d-107">Žádosti, které překročí kvótu vrátí následující chybu:</span><span class="sxs-lookup"><span data-stu-id="c981d-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="c981d-108">Omezení přenosové rychlosti pro rozhraní API NuGet.org v následujících tabulkách.</span><span class="sxs-lookup"><span data-stu-id="c981d-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="c981d-109">Vyhledávání balíčků</span><span class="sxs-lookup"><span data-stu-id="c981d-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="c981d-110">Doporučujeme používat NuGet.org [rozhraní API V3](https://docs.microsoft.com/nuget/api/search-query-service-resource) aktuálně pro hledání, které jsou výkonné a nemá žádné omezení.</span><span class="sxs-lookup"><span data-stu-id="c981d-110">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="c981d-111">V1 a V2 vyhledejte rozhraní API, followins omezení platí:</span><span class="sxs-lookup"><span data-stu-id="c981d-111">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="c981d-112">rozhraní API</span><span class="sxs-lookup"><span data-stu-id="c981d-112">API</span></span> | <span data-ttu-id="c981d-113">Typ limitu</span><span class="sxs-lookup"><span data-stu-id="c981d-113">Limit Type</span></span> | <span data-ttu-id="c981d-114">Mezní hodnota</span><span class="sxs-lookup"><span data-stu-id="c981d-114">Limit Value</span></span> | <span data-ttu-id="c981d-115">Rozhraní API usecase</span><span class="sxs-lookup"><span data-stu-id="c981d-115">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="c981d-116">**GET** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="c981d-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="c981d-117">IP</span><span class="sxs-lookup"><span data-stu-id="c981d-117">IP</span></span> | <span data-ttu-id="c981d-118">1 000 / min</span><span class="sxs-lookup"><span data-stu-id="c981d-118">1000 / minute</span></span> | <span data-ttu-id="c981d-119">Dotazu na metadata balíčku NuGet přes v1 OData `Packages` kolekce</span><span class="sxs-lookup"><span data-stu-id="c981d-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="c981d-120">**GET** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="c981d-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="c981d-121">IP</span><span class="sxs-lookup"><span data-stu-id="c981d-121">IP</span></span> | <span data-ttu-id="c981d-122">3000 / min</span><span class="sxs-lookup"><span data-stu-id="c981d-122">3000 / minute</span></span> | <span data-ttu-id="c981d-123">Hledat balíčky NuGet prostřednictvím koncového bodu v1 vyhledávání</span><span class="sxs-lookup"><span data-stu-id="c981d-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="c981d-124">**GET** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="c981d-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="c981d-125">IP</span><span class="sxs-lookup"><span data-stu-id="c981d-125">IP</span></span> | <span data-ttu-id="c981d-126">20000 / min</span><span class="sxs-lookup"><span data-stu-id="c981d-126">20000 / minute</span></span> | <span data-ttu-id="c981d-127">Dotazu na metadata balíčku NuGet přes v2 OData `Packages` kolekce</span><span class="sxs-lookup"><span data-stu-id="c981d-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="c981d-128">**GET** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="c981d-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="c981d-129">IP</span><span class="sxs-lookup"><span data-stu-id="c981d-129">IP</span></span> | <span data-ttu-id="c981d-130">100 / min</span><span class="sxs-lookup"><span data-stu-id="c981d-130">100 / minute</span></span> | <span data-ttu-id="c981d-131">Počet balíčků NuGet přes v2 OData dotazů `Packages` kolekce</span><span class="sxs-lookup"><span data-stu-id="c981d-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="c981d-132">Balíček se službami Push a vyjmutí ze seznamu</span><span class="sxs-lookup"><span data-stu-id="c981d-132">Package Push and Unlist</span></span>

| <span data-ttu-id="c981d-133">rozhraní API</span><span class="sxs-lookup"><span data-stu-id="c981d-133">API</span></span> | <span data-ttu-id="c981d-134">Typ limitu</span><span class="sxs-lookup"><span data-stu-id="c981d-134">Limit Type</span></span> | <span data-ttu-id="c981d-135">Mezní hodnota</span><span class="sxs-lookup"><span data-stu-id="c981d-135">Limit Value</span></span> | <span data-ttu-id="c981d-136">Rozhraní API usecase</span><span class="sxs-lookup"><span data-stu-id="c981d-136">API usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="c981d-137">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="c981d-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="c981d-138">Klíč rozhraní API</span><span class="sxs-lookup"><span data-stu-id="c981d-138">API Key</span></span> | <span data-ttu-id="c981d-139">250 / hodina</span><span class="sxs-lookup"><span data-stu-id="c981d-139">250 / hour</span></span> | <span data-ttu-id="c981d-140">Nahrání nového balíčku NuGet (verze) prostřednictvím koncového bodu v2 nabízených oznámení</span><span class="sxs-lookup"><span data-stu-id="c981d-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="c981d-141">**ODSTRANIT** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="c981d-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="c981d-142">Klíč rozhraní API</span><span class="sxs-lookup"><span data-stu-id="c981d-142">API Key</span></span> | <span data-ttu-id="c981d-143">250 / hodina</span><span class="sxs-lookup"><span data-stu-id="c981d-143">250 / hour</span></span> | <span data-ttu-id="c981d-144">Vyjmutí ze seznamu balíčku NuGet (verze) prostřednictvím koncového bodu v2</span><span class="sxs-lookup"><span data-stu-id="c981d-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 
