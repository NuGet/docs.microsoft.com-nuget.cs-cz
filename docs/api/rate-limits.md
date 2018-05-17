---
title: Omezení přenosové rychlosti, NuGet rozhraní API
description: Rozhraní API NuGet se vynucuje omezení přenosové rychlosti, aby se zabránilo zneužití.
author: cmanu
ms.author: cmanu
manager: skofman
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: e236d685a700d0f47480336cece8edfd44c28863
ms.sourcegitcommit: 68c8a494a11c892ac671fec3170ba7be97fb044d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/04/2018
---
# <a name="rate-limits"></a><span data-ttu-id="3c428-103">Omezení přenosové rychlosti</span><span class="sxs-lookup"><span data-stu-id="3c428-103">Rate Limits</span></span>

<span data-ttu-id="3c428-104">Rozhraní API NuGet.org vynucuje, aby se zabránilo zneužití omezení rychlosti.</span><span class="sxs-lookup"><span data-stu-id="3c428-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="3c428-105">Požadavky, které překračují limit rychlosti vrátí následující chybu:</span><span class="sxs-lookup"><span data-stu-id="3c428-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="3c428-106">V následujících tabulkách najdete omezení přenosové rychlosti pro rozhraní API NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="3c428-106">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="3c428-107">Balíček vyhledávání</span><span class="sxs-lookup"><span data-stu-id="3c428-107">Package search</span></span>

> [!Note]
> <span data-ttu-id="3c428-108">Doporučujeme používat NuGet.org [rozhraní API V3](https://docs.microsoft.com/nuget/api/search-query-service-resource) aktuálně pro vyhledávání, které jsou původce a nemají žádné omezení.</span><span class="sxs-lookup"><span data-stu-id="3c428-108">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="3c428-109">V1 a V2 vyhledání rozhraní API, limity followins platí:</span><span class="sxs-lookup"><span data-stu-id="3c428-109">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="3c428-110">rozhraní API</span><span class="sxs-lookup"><span data-stu-id="3c428-110">API</span></span> | <span data-ttu-id="3c428-111">Omezení typu</span><span class="sxs-lookup"><span data-stu-id="3c428-111">Limit Type</span></span> | <span data-ttu-id="3c428-112">Mezní hodnota</span><span class="sxs-lookup"><span data-stu-id="3c428-112">Limit Value</span></span> | <span data-ttu-id="3c428-113">Rozhraní API usecase</span><span class="sxs-lookup"><span data-stu-id="3c428-113">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="3c428-114">**GET** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="3c428-114">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="3c428-115">IP</span><span class="sxs-lookup"><span data-stu-id="3c428-115">IP</span></span> | <span data-ttu-id="3c428-116">1000 za minutu</span><span class="sxs-lookup"><span data-stu-id="3c428-116">1000 / minute</span></span> | <span data-ttu-id="3c428-117">Dotaz na metadata balíčků NuGet prostřednictvím v1 OData `Packages` kolekce</span><span class="sxs-lookup"><span data-stu-id="3c428-117">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="3c428-118">**GET** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="3c428-118">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="3c428-119">IP</span><span class="sxs-lookup"><span data-stu-id="3c428-119">IP</span></span> | <span data-ttu-id="3c428-120">3000 za minutu</span><span class="sxs-lookup"><span data-stu-id="3c428-120">3000 / minute</span></span> | <span data-ttu-id="3c428-121">Hledání balíčků NuGet prostřednictvím koncového bodu hledání v1</span><span class="sxs-lookup"><span data-stu-id="3c428-121">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="3c428-122">**GET** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="3c428-122">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="3c428-123">IP</span><span class="sxs-lookup"><span data-stu-id="3c428-123">IP</span></span> | <span data-ttu-id="3c428-124">20000 za minutu</span><span class="sxs-lookup"><span data-stu-id="3c428-124">20000 / minute</span></span> | <span data-ttu-id="3c428-125">Dotaz na metadata balíčků NuGet prostřednictvím v2 OData `Packages` kolekce</span><span class="sxs-lookup"><span data-stu-id="3c428-125">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="3c428-126">**GET** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="3c428-126">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="3c428-127">IP</span><span class="sxs-lookup"><span data-stu-id="3c428-127">IP</span></span> | <span data-ttu-id="3c428-128">100 za minutu</span><span class="sxs-lookup"><span data-stu-id="3c428-128">100 / minute</span></span> | <span data-ttu-id="3c428-129">Dotaz na počet balíček NuGet prostřednictvím v2 OData `Packages` kolekce</span><span class="sxs-lookup"><span data-stu-id="3c428-129">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="3c428-130">Balíček Push a Unlist</span><span class="sxs-lookup"><span data-stu-id="3c428-130">Package Push and Unlist</span></span>

| <span data-ttu-id="3c428-131">rozhraní API</span><span class="sxs-lookup"><span data-stu-id="3c428-131">API</span></span> | <span data-ttu-id="3c428-132">Omezení typu</span><span class="sxs-lookup"><span data-stu-id="3c428-132">Limit Type</span></span> | <span data-ttu-id="3c428-133">Mezní hodnota</span><span class="sxs-lookup"><span data-stu-id="3c428-133">Limit Value</span></span> | <span data-ttu-id="3c428-134">Rozhraní API usecase</span><span class="sxs-lookup"><span data-stu-id="3c428-134">API usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="3c428-135">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="3c428-135">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="3c428-136">Klíč rozhraní API</span><span class="sxs-lookup"><span data-stu-id="3c428-136">API Key</span></span> | <span data-ttu-id="3c428-137">100 za minutu</span><span class="sxs-lookup"><span data-stu-id="3c428-137">100 / minute</span></span> | <span data-ttu-id="3c428-138">Nahrát nový balíček NuGet (verze) prostřednictvím koncového bodu nabízené v2</span><span class="sxs-lookup"><span data-stu-id="3c428-138">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="3c428-139">**ODSTRANIT** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="3c428-139">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="3c428-140">Klíč rozhraní API</span><span class="sxs-lookup"><span data-stu-id="3c428-140">API Key</span></span> | <span data-ttu-id="3c428-141">100 za minutu</span><span class="sxs-lookup"><span data-stu-id="3c428-141">100 / minute</span></span> | <span data-ttu-id="3c428-142">Unlist balíček NuGet (verze) prostřednictvím koncového bodu v2</span><span class="sxs-lookup"><span data-stu-id="3c428-142">Unlist a NuGet package (version) via v2 endpoint</span></span> 
