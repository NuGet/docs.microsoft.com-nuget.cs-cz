---
title: Omezení přenosové rychlosti | Microsoft Docs
author:
- cmanu
- anangaur
ms.author:
- cmanu
manager: skofman
ms.date: 03/20/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Rozhraní API NuGet se vynucuje omezení přenosové rychlosti, aby se zabránilo zneužití.
keywords: Míra NuGet rozhraní API, omezení
ms.reviewer:
- skofman
- anangaur
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: f7891d5e4c008219d9f4808f223f3e5e7ae06ced
ms.sourcegitcommit: fa40be739d093a37d5f7072b62ebdb4f595f4110
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/30/2018
---
# <a name="rate-limits"></a><span data-ttu-id="38dba-104">Omezení přenosové rychlosti</span><span class="sxs-lookup"><span data-stu-id="38dba-104">Rate Limits</span></span>

<span data-ttu-id="38dba-105">Rozhraní API NuGet.org vynucuje, aby se zabránilo zneužití omezení rychlosti.</span><span class="sxs-lookup"><span data-stu-id="38dba-105">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="38dba-106">Požadavky, které překračují limit rychlosti vrátí následující chybu:</span><span class="sxs-lookup"><span data-stu-id="38dba-106">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="38dba-107">V následujících tabulkách najdete omezení přenosové rychlosti pro rozhraní API NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="38dba-107">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="38dba-108">Balíček vyhledávání</span><span class="sxs-lookup"><span data-stu-id="38dba-108">Package search</span></span>

> [!Note]
> <span data-ttu-id="38dba-109">Doporučujeme používat NuGet.org [rozhraní API V3](https://docs.microsoft.com/nuget/api/search-query-service-resource) aktuálně pro vyhledávání, které jsou původce a nemají žádné omezení.</span><span class="sxs-lookup"><span data-stu-id="38dba-109">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="38dba-110">V1 a V2 vyhledání rozhraní API, limity followins platí:</span><span class="sxs-lookup"><span data-stu-id="38dba-110">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="38dba-111">rozhraní API</span><span class="sxs-lookup"><span data-stu-id="38dba-111">API</span></span> | <span data-ttu-id="38dba-112">Omezení typu</span><span class="sxs-lookup"><span data-stu-id="38dba-112">Limit Type</span></span> | <span data-ttu-id="38dba-113">Mezní hodnota</span><span class="sxs-lookup"><span data-stu-id="38dba-113">Limit Value</span></span> | <span data-ttu-id="38dba-114">Rozhraní API usecase</span><span class="sxs-lookup"><span data-stu-id="38dba-114">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="38dba-115">**GET** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="38dba-115">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="38dba-116">IP</span><span class="sxs-lookup"><span data-stu-id="38dba-116">IP</span></span> | <span data-ttu-id="38dba-117">1000 za minutu</span><span class="sxs-lookup"><span data-stu-id="38dba-117">1000 / minute</span></span> | <span data-ttu-id="38dba-118">Dotaz na metadata balíčků NuGet prostřednictvím v1 OData `Packages` kolekce</span><span class="sxs-lookup"><span data-stu-id="38dba-118">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="38dba-119">**GET** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="38dba-119">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="38dba-120">IP</span><span class="sxs-lookup"><span data-stu-id="38dba-120">IP</span></span> | <span data-ttu-id="38dba-121">3000 za minutu</span><span class="sxs-lookup"><span data-stu-id="38dba-121">3000 / minute</span></span> | <span data-ttu-id="38dba-122">Hledání balíčků NuGet prostřednictvím koncového bodu hledání v1</span><span class="sxs-lookup"><span data-stu-id="38dba-122">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="38dba-123">**GET** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="38dba-123">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="38dba-124">IP</span><span class="sxs-lookup"><span data-stu-id="38dba-124">IP</span></span> | <span data-ttu-id="38dba-125">20000 za minutu</span><span class="sxs-lookup"><span data-stu-id="38dba-125">20000 / minute</span></span> | <span data-ttu-id="38dba-126">Dotaz na metadata balíčků NuGet prostřednictvím v2 OData `Packages` kolekce</span><span class="sxs-lookup"><span data-stu-id="38dba-126">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="38dba-127">**GET** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="38dba-127">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="38dba-128">IP</span><span class="sxs-lookup"><span data-stu-id="38dba-128">IP</span></span> | <span data-ttu-id="38dba-129">100 za minutu</span><span class="sxs-lookup"><span data-stu-id="38dba-129">100 / minute</span></span> | <span data-ttu-id="38dba-130">Dotaz na počet balíček NuGet prostřednictvím v2 OData `Packages` kolekce</span><span class="sxs-lookup"><span data-stu-id="38dba-130">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="38dba-131">Balíček Push a Unlist</span><span class="sxs-lookup"><span data-stu-id="38dba-131">Package Push and Unlist</span></span>

| <span data-ttu-id="38dba-132">rozhraní API</span><span class="sxs-lookup"><span data-stu-id="38dba-132">API</span></span> | <span data-ttu-id="38dba-133">Omezení typu</span><span class="sxs-lookup"><span data-stu-id="38dba-133">Limit Type</span></span> | <span data-ttu-id="38dba-134">Mezní hodnota</span><span class="sxs-lookup"><span data-stu-id="38dba-134">Limit Value</span></span> | <span data-ttu-id="38dba-135">Usecase pomocnou hnací jednotku</span><span class="sxs-lookup"><span data-stu-id="38dba-135">APU usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="38dba-136">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="38dba-136">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="38dba-137">Klíč rozhraní API</span><span class="sxs-lookup"><span data-stu-id="38dba-137">API Key</span></span> | <span data-ttu-id="38dba-138">100 za minutu</span><span class="sxs-lookup"><span data-stu-id="38dba-138">100 / minute</span></span> | <span data-ttu-id="38dba-139">Nahrát nový balíček NuGet (verze) prostřednictvím koncového bodu nabízené v2</span><span class="sxs-lookup"><span data-stu-id="38dba-139">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="38dba-140">**ODSTRANIT** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="38dba-140">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="38dba-141">Klíč rozhraní API</span><span class="sxs-lookup"><span data-stu-id="38dba-141">API Key</span></span> | <span data-ttu-id="38dba-142">100 za minutu</span><span class="sxs-lookup"><span data-stu-id="38dba-142">100 / minute</span></span> | <span data-ttu-id="38dba-143">Unlist balíček NuGet (verze) prostřednictvím koncového bodu v2</span><span class="sxs-lookup"><span data-stu-id="38dba-143">Unlist a NuGet package (version) via v2 endpoint</span></span> 
