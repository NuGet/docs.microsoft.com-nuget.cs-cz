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
# <a name="rate-limits"></a>Omezení přenosové rychlosti

Rozhraní API NuGet.org vynucuje omezení rychlosti, aby se zabránilo zneužití. Požadavky, které překračují omezení četnosti se vrátí následující chybu: 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

Kromě omezení pomocí omezení přenosové rychlosti požadavků některá rozhraní API taky vynutit kvóty. Žádosti, které překročí kvótu vrátí následující chybu:

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

Omezení přenosové rychlosti pro rozhraní API NuGet.org v následujících tabulkách.

## <a name="package-search"></a>Vyhledávání balíčků

> [!Note]
> Doporučujeme používat NuGet.org [rozhraní API V3](https://docs.microsoft.com/nuget/api/search-query-service-resource) aktuálně pro hledání, které jsou výkonné a nemá žádné omezení. V1 a V2 vyhledejte rozhraní API, followins omezení platí:


| rozhraní API | Typ limitu | Mezní hodnota | Rozhraní API usecase |
|:---|:---|:---|:---|
**GET** `/api/v1/Packages` | IP | 1 000 / min | Dotazu na metadata balíčku NuGet přes v1 OData `Packages` kolekce |
**GET** `/api/v1/Search()` | IP | 3000 / min | Hledat balíčky NuGet prostřednictvím koncového bodu v1 vyhledávání | 
**GET** `/api/v2/Packages` | IP | 20000 / min | Dotazu na metadata balíčku NuGet přes v2 OData `Packages` kolekce | 
**GET** `/api/v2/Packages/$count` | IP | 100 / min | Počet balíčků NuGet přes v2 OData dotazů `Packages` kolekce | 

## <a name="package-push-and-unlist"></a>Balíček se službami Push a vyjmutí ze seznamu

| rozhraní API | Typ limitu | Mezní hodnota | Rozhraní API usecase | 
|:---|:---|:---|:--- |
**PUT** `/api/v2/package` | Klíč rozhraní API | 250 / hodina | Nahrání nového balíčku NuGet (verze) prostřednictvím koncového bodu v2 nabízených oznámení 
**ODSTRANIT** `/api/v2/package/{id}/{version}` | Klíč rozhraní API | 250 / hodina | Vyjmutí ze seznamu balíčku NuGet (verze) prostřednictvím koncového bodu v2 
