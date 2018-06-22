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
ms.openlocfilehash: c5d3cf68ac6a96a6c14eb5e652bcf72698b6a8e8
ms.sourcegitcommit: 8f0bb8bb9cb91d27d660963ed9b0f32642f420fe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
ms.locfileid: "34225941"
---
# <a name="rate-limits"></a>Omezení přenosové rychlosti

Rozhraní API NuGet.org vynucuje, aby se zabránilo zneužití omezení rychlosti. Požadavky, které překračují limit rychlosti vrátí následující chybu: 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

V následujících tabulkách najdete omezení přenosové rychlosti pro rozhraní API NuGet.org.

## <a name="package-search"></a>Balíček vyhledávání

> [!Note]
> Doporučujeme používat NuGet.org [rozhraní API V3](https://docs.microsoft.com/nuget/api/search-query-service-resource) aktuálně pro vyhledávání, které jsou původce a nemají žádné omezení. V1 a V2 vyhledání rozhraní API, limity followins platí:


| rozhraní API | Omezení typu | Mezní hodnota | Rozhraní API usecase |
|:---|:---|:---|:---|
**GET** `/api/v1/Packages` | IP | 1000 za minutu | Dotaz na metadata balíčků NuGet prostřednictvím v1 OData `Packages` kolekce |
**GET** `/api/v1/Search()` | IP | 3000 za minutu | Hledání balíčků NuGet prostřednictvím koncového bodu hledání v1 | 
**GET** `/api/v2/Packages` | IP | 20000 za minutu | Dotaz na metadata balíčků NuGet prostřednictvím v2 OData `Packages` kolekce | 
**GET** `/api/v2/Packages/$count` | IP | 100 za minutu | Dotaz na počet balíček NuGet prostřednictvím v2 OData `Packages` kolekce | 

## <a name="package-push-and-unlist"></a>Balíček Push a Unlist

| rozhraní API | Omezení typu | Mezní hodnota | Rozhraní API usecase | 
|:---|:---|:---|:--- |
**PUT** `/api/v2/package` | Klíč rozhraní API | 250 / hodinu | Nahrát nový balíček NuGet (verze) prostřednictvím koncového bodu nabízené v2 
**ODSTRANIT** `/api/v2/package/{id}/{version}` | Klíč rozhraní API | 250 / hodinu | Unlist balíček NuGet (verze) prostřednictvím koncového bodu v2 
