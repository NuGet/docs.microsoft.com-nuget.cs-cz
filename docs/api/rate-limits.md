---
title: Omezení rozhraní API Nugetu přenosové rychlosti
description: Rozhraní API pro NuGet se vynucovat omezení přenosové rychlosti, aby se zabránilo zneužití.
author: cmanu
ms.author: cmanu
manager: skofman
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: a55eb49318b766028d1579a4d33618617bbd8801
ms.sourcegitcommit: 4d139cb54a46616ae48d1768fa108ae3bf450d5b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/03/2018
ms.locfileid: "39508124"
---
# <a name="rate-limits"></a><span data-ttu-id="c6f9c-103">Omezení přenosové rychlosti</span><span class="sxs-lookup"><span data-stu-id="c6f9c-103">Rate Limits</span></span>

<span data-ttu-id="c6f9c-104">Rozhraní API NuGet.org vynucuje omezení rychlosti, aby se zabránilo zneužití.</span><span class="sxs-lookup"><span data-stu-id="c6f9c-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="c6f9c-105">Požadavky, které překračují omezení četnosti se vrátí následující chybu:</span><span class="sxs-lookup"><span data-stu-id="c6f9c-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="c6f9c-106">Kromě omezení pomocí omezení přenosové rychlosti požadavků některá rozhraní API taky vynutit kvóty.</span><span class="sxs-lookup"><span data-stu-id="c6f9c-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="c6f9c-107">Žádosti, které překročí kvótu vrátí následující chybu:</span><span class="sxs-lookup"><span data-stu-id="c6f9c-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="c6f9c-108">Omezení přenosové rychlosti pro rozhraní API NuGet.org v následujících tabulkách.</span><span class="sxs-lookup"><span data-stu-id="c6f9c-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="c6f9c-109">Vyhledávání balíčků</span><span class="sxs-lookup"><span data-stu-id="c6f9c-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="c6f9c-110">Doporučujeme používat NuGet.org [rozhraní API V3](https://docs.microsoft.com/nuget/api/search-query-service-resource) aktuálně pro hledání, které jsou výkonné a nemá žádné omezení.</span><span class="sxs-lookup"><span data-stu-id="c6f9c-110">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="c6f9c-111">V1 a V2 vyhledejte rozhraní API, followins omezení platí:</span><span class="sxs-lookup"><span data-stu-id="c6f9c-111">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="c6f9c-112">rozhraní API</span><span class="sxs-lookup"><span data-stu-id="c6f9c-112">API</span></span> | <span data-ttu-id="c6f9c-113">Typ limitu</span><span class="sxs-lookup"><span data-stu-id="c6f9c-113">Limit Type</span></span> | <span data-ttu-id="c6f9c-114">Mezní hodnota</span><span class="sxs-lookup"><span data-stu-id="c6f9c-114">Limit Value</span></span> | <span data-ttu-id="c6f9c-115">Rozhraní API usecase</span><span class="sxs-lookup"><span data-stu-id="c6f9c-115">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="c6f9c-116">**GET** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="c6f9c-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="c6f9c-117">IP</span><span class="sxs-lookup"><span data-stu-id="c6f9c-117">IP</span></span> | <span data-ttu-id="c6f9c-118">1 000 / min</span><span class="sxs-lookup"><span data-stu-id="c6f9c-118">1000 / minute</span></span> | <span data-ttu-id="c6f9c-119">Dotazu na metadata balíčku NuGet přes v1 OData `Packages` kolekce</span><span class="sxs-lookup"><span data-stu-id="c6f9c-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="c6f9c-120">**GET** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="c6f9c-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="c6f9c-121">IP</span><span class="sxs-lookup"><span data-stu-id="c6f9c-121">IP</span></span> | <span data-ttu-id="c6f9c-122">3000 / min</span><span class="sxs-lookup"><span data-stu-id="c6f9c-122">3000 / minute</span></span> | <span data-ttu-id="c6f9c-123">Hledat balíčky NuGet prostřednictvím koncového bodu v1 vyhledávání</span><span class="sxs-lookup"><span data-stu-id="c6f9c-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="c6f9c-124">**GET** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="c6f9c-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="c6f9c-125">IP</span><span class="sxs-lookup"><span data-stu-id="c6f9c-125">IP</span></span> | <span data-ttu-id="c6f9c-126">20000 / min</span><span class="sxs-lookup"><span data-stu-id="c6f9c-126">20000 / minute</span></span> | <span data-ttu-id="c6f9c-127">Dotazu na metadata balíčku NuGet přes v2 OData `Packages` kolekce</span><span class="sxs-lookup"><span data-stu-id="c6f9c-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="c6f9c-128">**GET** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="c6f9c-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="c6f9c-129">IP</span><span class="sxs-lookup"><span data-stu-id="c6f9c-129">IP</span></span> | <span data-ttu-id="c6f9c-130">100 / min</span><span class="sxs-lookup"><span data-stu-id="c6f9c-130">100 / minute</span></span> | <span data-ttu-id="c6f9c-131">Počet balíčků NuGet přes v2 OData dotazů `Packages` kolekce</span><span class="sxs-lookup"><span data-stu-id="c6f9c-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="c6f9c-132">Balíček se službami Push a vyjmutí ze seznamu</span><span class="sxs-lookup"><span data-stu-id="c6f9c-132">Package Push and Unlist</span></span>

| <span data-ttu-id="c6f9c-133">rozhraní API</span><span class="sxs-lookup"><span data-stu-id="c6f9c-133">API</span></span> | <span data-ttu-id="c6f9c-134">Typ limitu</span><span class="sxs-lookup"><span data-stu-id="c6f9c-134">Limit Type</span></span> | <span data-ttu-id="c6f9c-135">Mezní hodnota</span><span class="sxs-lookup"><span data-stu-id="c6f9c-135">Limit Value</span></span> | <span data-ttu-id="c6f9c-136">Rozhraní API usecase</span><span class="sxs-lookup"><span data-stu-id="c6f9c-136">API usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="c6f9c-137">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="c6f9c-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="c6f9c-138">Klíč rozhraní API</span><span class="sxs-lookup"><span data-stu-id="c6f9c-138">API Key</span></span> | <span data-ttu-id="c6f9c-139">250 / hodina</span><span class="sxs-lookup"><span data-stu-id="c6f9c-139">250 / hour</span></span> | <span data-ttu-id="c6f9c-140">Nahrání nového balíčku NuGet (verze) prostřednictvím koncového bodu v2 nabízených oznámení</span><span class="sxs-lookup"><span data-stu-id="c6f9c-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="c6f9c-141">**ODSTRANIT** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="c6f9c-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="c6f9c-142">Klíč rozhraní API</span><span class="sxs-lookup"><span data-stu-id="c6f9c-142">API Key</span></span> | <span data-ttu-id="c6f9c-143">250 / hodina</span><span class="sxs-lookup"><span data-stu-id="c6f9c-143">250 / hour</span></span> | <span data-ttu-id="c6f9c-144">Vyjmutí ze seznamu balíčku NuGet (verze) prostřednictvím koncového bodu v2</span><span class="sxs-lookup"><span data-stu-id="c6f9c-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 
