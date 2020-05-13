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

| Rozhraní API | Typ limitu | Hodnota limitu | Případ použití rozhraní API |
|:---|:---|:---|:---|
**Získat**`/api/v1/Packages` | IP adresa | 1000 minut | Dotazování metadat balíčku NuGet prostřednictvím kolekce OData v1 `Packages` |
**Získat**`/api/v1/Search()` | IP adresa | 3000 minut | Hledání balíčků NuGet prostřednictvím koncového bodu pro vyhledávání v1 | 
**Získat**`/api/v2/Packages` | IP adresa | 20000 minut | Dotaz na metadata balíčku NuGet přes kolekci OData v2 `Packages` | 
**Získat**`/api/v2/Packages/$count` | IP adresa | 100 minut | Dotaz na počet balíčků NuGet přes v2 `Packages` shromažďování dat OData | 

## <a name="package-push-and-unlist"></a>Vložení a odbalení balíčku

| Rozhraní API | Typ limitu | Hodnota limitu | Případ použití rozhraní API | 
|:---|:---|:---|:--- |
**Vložit**`/api/v2/package` | Klíč rozhraní API | 350 za hodinu | Nahrání nového balíčku NuGet (verze) prostřednictvím nabízeného koncového bodu v2 
**Odstranit**`/api/v2/package/{id}/{version}` | Klíč rozhraní API | 250 za hodinu | Odpisovat balíček NuGet (verze) prostřednictvím koncového bodu v2 

## <a name="nugetorg-website-page-views"></a>nuget.org zobrazení stránek webu

Pokud přistupujete k webovým stránkám nuget.org programově, zvažte zkoumání našich dokumentovaných [rozhraní API V3](overview.md). Tyto koncové body umožňují jednodušší přístup k metadatům a obsahu balíčků. Rozhraní V3 API má lepší dostupnost a má vyšší výkon než přístup k webovým stránkám galerie NuGet, které jsou určeny pro interakci webového prohlížeče.

| Rozhraní API | Typ limitu | Hodnota limitu | Případ použití rozhraní API | 
|:---|:---|:---|:--- |
**Získat**`/package/{id}/{version}` | IP adresa | 50 minut | Zobrazit stránku s podrobnostmi balíčku (verze) 
