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
# <a name="rate-limits"></a>Omezení přenosové rychlosti

Rozhraní NuGet.org API vynutilo omezení četnosti, aby se zabránilo zneužití. Žádosti, které překračují limit přenosové rychlosti, vrátí následující chybu: 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

Kromě omezení požadavků pomocí omezení přenosové rychlosti některá rozhraní API také vynutila kvótu. Žádosti, které překračují kvótu, vrátí následující chybu:

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

V následujících tabulkách jsou uvedeny omezení přenosové rychlosti pro rozhraní NuGet.org API.

## <a name="package-search"></a>Hledání balíčku

> [!Note]
> Doporučujeme používat [rozhraní API pro vyhledávání](search-query-service-resource.md) NuGet. org, protože neodpovídá aktuálně omezené rychlosti. Pro rozhraní API pro vyhledávání V1 a v2 platí následující omezení:

| API | Typ limitu | Hodnota limitu | UseCase API |
|:---|:---|:---|:---|
**GET** `/api/v1/Packages` | adresu klienta | 1000 minut | Dotazování metadat balíčku NuGet přes v1 OData `Packages` Collection |
**GET** `/api/v1/Search()` | adresu klienta | 3000 minut | Hledání balíčků NuGet prostřednictvím koncového bodu pro vyhledávání v1 | 
**GET** `/api/v2/Packages` | adresu klienta | 20000 minut | Dotazování metadat balíčku NuGet přes v2 OData `Packages` Collection | 
**GET** `/api/v2/Packages/$count` | adresu klienta | 100 minut | Dotazování na počet balíčků NuGet prostřednictvím kolekce `Packages` v2 OData | 

## <a name="package-push-and-unlist"></a>Vložení a odbalení balíčku

| API | Typ limitu | Hodnota limitu | UseCase API | 
|:---|:---|:---|:--- |
**Umístit** `/api/v2/package` | Klíč rozhraní API | 350 za hodinu | Nahrání nového balíčku NuGet (verze) prostřednictvím nabízeného koncového bodu v2 
**Odstranit** `/api/v2/package/{id}/{version}` | Klíč rozhraní API | 250 za hodinu | Odpisovat balíček NuGet (verze) prostřednictvím koncového bodu v2 
