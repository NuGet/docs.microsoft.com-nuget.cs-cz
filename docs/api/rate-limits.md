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
ms.openlocfilehash: 9e60c0236bd4e6f1374b50a236447faf80dddb38
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813192"
---
# <a name="rate-limits"></a><span data-ttu-id="65225-103">Omezení přenosové rychlosti</span><span class="sxs-lookup"><span data-stu-id="65225-103">Rate Limits</span></span>

<span data-ttu-id="65225-104">Rozhraní NuGet.org API vynutilo omezení četnosti, aby se zabránilo zneužití.</span><span class="sxs-lookup"><span data-stu-id="65225-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="65225-105">Žádosti, které překračují limit přenosové rychlosti, vrátí následující chybu:</span><span class="sxs-lookup"><span data-stu-id="65225-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="65225-106">Kromě omezení požadavků pomocí omezení přenosové rychlosti některá rozhraní API také vynutila kvótu.</span><span class="sxs-lookup"><span data-stu-id="65225-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="65225-107">Žádosti, které překračují kvótu, vrátí následující chybu:</span><span class="sxs-lookup"><span data-stu-id="65225-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="65225-108">V následujících tabulkách jsou uvedeny omezení přenosové rychlosti pro rozhraní NuGet.org API.</span><span class="sxs-lookup"><span data-stu-id="65225-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="65225-109">Hledání balíčku</span><span class="sxs-lookup"><span data-stu-id="65225-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="65225-110">Doporučujeme používat [rozhraní API pro vyhledávání](search-query-service-resource.md) NuGet. org, protože neodpovídá aktuálně omezené rychlosti.</span><span class="sxs-lookup"><span data-stu-id="65225-110">We recommend using NuGet.org's [V3 search APIs](search-query-service-resource.md) as it is not rate limited currently.</span></span> <span data-ttu-id="65225-111">Pro rozhraní API pro vyhledávání V1 a v2 platí následující omezení:</span><span class="sxs-lookup"><span data-stu-id="65225-111">For V1 and V2 search APIs, the following limits apply:</span></span>

| <span data-ttu-id="65225-112">API</span><span class="sxs-lookup"><span data-stu-id="65225-112">API</span></span> | <span data-ttu-id="65225-113">Typ limitu</span><span class="sxs-lookup"><span data-stu-id="65225-113">Limit Type</span></span> | <span data-ttu-id="65225-114">Hodnota limitu</span><span class="sxs-lookup"><span data-stu-id="65225-114">Limit Value</span></span> | <span data-ttu-id="65225-115">UseCase API</span><span class="sxs-lookup"><span data-stu-id="65225-115">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="65225-116">**GET** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="65225-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="65225-117">adresu klienta</span><span class="sxs-lookup"><span data-stu-id="65225-117">IP</span></span> | <span data-ttu-id="65225-118">1000 minut</span><span class="sxs-lookup"><span data-stu-id="65225-118">1000 / minute</span></span> | <span data-ttu-id="65225-119">Dotazování metadat balíčku NuGet přes v1 OData `Packages` Collection</span><span class="sxs-lookup"><span data-stu-id="65225-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="65225-120">**GET** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="65225-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="65225-121">adresu klienta</span><span class="sxs-lookup"><span data-stu-id="65225-121">IP</span></span> | <span data-ttu-id="65225-122">3000 minut</span><span class="sxs-lookup"><span data-stu-id="65225-122">3000 / minute</span></span> | <span data-ttu-id="65225-123">Hledání balíčků NuGet prostřednictvím koncového bodu pro vyhledávání v1</span><span class="sxs-lookup"><span data-stu-id="65225-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="65225-124">**GET** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="65225-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="65225-125">adresu klienta</span><span class="sxs-lookup"><span data-stu-id="65225-125">IP</span></span> | <span data-ttu-id="65225-126">20000 minut</span><span class="sxs-lookup"><span data-stu-id="65225-126">20000 / minute</span></span> | <span data-ttu-id="65225-127">Dotazování metadat balíčku NuGet přes v2 OData `Packages` Collection</span><span class="sxs-lookup"><span data-stu-id="65225-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="65225-128">**GET** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="65225-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="65225-129">adresu klienta</span><span class="sxs-lookup"><span data-stu-id="65225-129">IP</span></span> | <span data-ttu-id="65225-130">100 minut</span><span class="sxs-lookup"><span data-stu-id="65225-130">100 / minute</span></span> | <span data-ttu-id="65225-131">Dotazování na počet balíčků NuGet prostřednictvím kolekce `Packages` v2 OData</span><span class="sxs-lookup"><span data-stu-id="65225-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="65225-132">Vložení a odbalení balíčku</span><span class="sxs-lookup"><span data-stu-id="65225-132">Package Push and Unlist</span></span>

| <span data-ttu-id="65225-133">API</span><span class="sxs-lookup"><span data-stu-id="65225-133">API</span></span> | <span data-ttu-id="65225-134">Typ limitu</span><span class="sxs-lookup"><span data-stu-id="65225-134">Limit Type</span></span> | <span data-ttu-id="65225-135">Hodnota limitu</span><span class="sxs-lookup"><span data-stu-id="65225-135">Limit Value</span></span> | <span data-ttu-id="65225-136">UseCase API</span><span class="sxs-lookup"><span data-stu-id="65225-136">API usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="65225-137">**Umístit** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="65225-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="65225-138">Klíč rozhraní API</span><span class="sxs-lookup"><span data-stu-id="65225-138">API Key</span></span> | <span data-ttu-id="65225-139">350 za hodinu</span><span class="sxs-lookup"><span data-stu-id="65225-139">350 / hour</span></span> | <span data-ttu-id="65225-140">Nahrání nového balíčku NuGet (verze) prostřednictvím nabízeného koncového bodu v2</span><span class="sxs-lookup"><span data-stu-id="65225-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="65225-141">**Odstranit** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="65225-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="65225-142">Klíč rozhraní API</span><span class="sxs-lookup"><span data-stu-id="65225-142">API Key</span></span> | <span data-ttu-id="65225-143">250 za hodinu</span><span class="sxs-lookup"><span data-stu-id="65225-143">250 / hour</span></span> | <span data-ttu-id="65225-144">Odpisovat balíček NuGet (verze) prostřednictvím koncového bodu v2</span><span class="sxs-lookup"><span data-stu-id="65225-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 
