---
title: Balíčky symbolů nabízených oznámení, API NuGet | Microsoft Docs
author: cristinamanum
ms.author: cmanu
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Služba publikování umožňuje klientům publikovat nové balíčky symbolů.
keywords: Balíček symbolů nabízených oznámení rozhraní NuGet API
ms.reviewer: karann
ms.openlocfilehash: bd4a10cc976c9d0775a63cfe61c35327c196065c
ms.sourcegitcommit: e39e5a5ddf68bf41e816617e7f0339308523bbb3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/05/2020
ms.locfileid: "96738874"
---
# <a name="push-symbol-packages"></a>Balíčky symbolů nabízených oznámení

Balíčky symbolů ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) je možné vložit pomocí rozhraní NuGet V3 API.
Tyto operace jsou založeny na prostředku, který `SymbolPackagePublish` najdete v [indexu služby](service-index.md).

## <a name="versioning"></a>Správa verzí

Použije se následující `@type` hodnota:

@type osa                 | Poznámky
--------------------        | -----
SymbolPackagePublish/4.9.0  | Počáteční verze

## <a name="base-url"></a>Základní adresa URL

Základní adresa URL následujících rozhraní API je hodnota `@id` vlastnosti `SymbolPackagePublish/4.9.0` prostředku v [indexu služby](service-index.md)zdroje balíčku. Pro dokumentaci níže se používá adresa URL balíčku NuGet. org. Zvažte možnost `https://www.nuget.org/api/v2/symbolpackage` použít jako zástupný symbol pro `@id` hodnotu nalezenou v indexu služby.

## <a name="http-methods"></a>Metody HTTP

`PUT`Tento prostředek podporuje metodu HTTP. 

## <a name="push-a-symbol-package"></a>Vložení balíčku symbolů

nuget.org podporuje vložení nového formátu balíčků symbolů ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) pomocí následujícího rozhraní API. 

    PUT https://www.nuget.org/api/v2/symbolpackage

Balíčky symbolů se stejným ID a verzí je možné odeslat víckrát. Balíček symbolů bude odmítnut v následujících případech.
- Balíček se stejným ID a verzí neexistuje.
- Byl vložen balíček symbolů se stejným ID a verzí, ale ještě není publikovaný.
- Balíček symbolů ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) je neplatný (viz [omezení balíčku symbolů](../create-packages/Symbol-Packages-snupkg.md)).

### <a name="request-parameters"></a>Parametry žádosti

Název           | V     | Typ   | Vyžadováno | Poznámky
-------------- | ------ | ------ | -------- | -----
X-NuGet – ApiKey | Hlavička | řetězec | ano      | Například `X-NuGet-ApiKey: {USER_API_KEY}`.

Klíč rozhraní API je neprůhledný řetězec ze zdroje balíčku uživatelem a nakonfigurovaný do klienta. Není k dispozici žádný konkrétní formát řetězce, ale délka klíče rozhraní API by neměla překročit rozumnou velikost pro hodnoty hlaviček protokolu HTTP.

### <a name="request-body"></a>Text požadavku

Text žádosti o nabízení oznámení je stejný jako text žádosti o nabízenou žádost balíčku (viz [push a DELETE balíčku](package-publish-resource.md)). 

### <a name="response"></a>Odpověď

Stavový kód | Význam
----------- | -------
201         | Balíček symbolů byl úspěšně vložen.
400         | Poskytnutý balíček symbolů je neplatný.
401         | Uživatel nemá autorizaci k provedení této akce.
404         | Odpovídající balíček se zadaným ID a verzí neexistuje.
409         | Balíček symbolů se zadaným ID a verzí byl vložen, ale ještě není k dispozici.
413         | Balíček je moc velký.

