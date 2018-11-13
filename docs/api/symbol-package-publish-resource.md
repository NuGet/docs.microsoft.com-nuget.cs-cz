---
title: Vložit Symbol balíčky NuGet rozhraní API | Dokumentace Microsoftu
author:
- cristinamanum
- kraigb
ms.author:
- cmanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Služba publikování umožňuje klientům publikovat nové balíčky pro symbol.
keywords: Balíček NuGet rozhraní API nabízených symbolů
ms.reviewer: karann
ms.openlocfilehash: 514ab3683db81da5b2220b005b8b39f1fec8300d
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580452"
---
# <a name="push-symbol-packages"></a>Balíčky symbolů nabízených oznámení

Je možné do balíčků symbolů nabízených oznámení ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) pomocí rozhraní API V3 NuGet.
Tyto operace jsou odhlásit z založené `SymbolPackagePublish` prostředek se nenašel v [index služby](service-index.md).

## <a name="versioning"></a>Správa verzí

Následující `@type` hodnota se používá:

@type Hodnota                 | Poznámky
--------------------        | -----
SymbolPackagePublish/4.9.0  | Počáteční verze

## <a name="base-url"></a>Základní adresa URL

Základní adresa URL pro následující rozhraní API je hodnota `@id` vlastnost `SymbolPackagePublish/4.9.0` prostředků ve zdroji balíčku [index služby](service-index.md). Pro níže uvedenou dokumentaci se používá adresu URL nuget.org. Vezměte v úvahu `https://www.nuget.org/api/v2/symbolpackage` jako zástupný symbol pro `@id` hodnota nalezena v indexu služby.

## <a name="http-methods"></a>Metody HTTP

`PUT` Tento prostředek podporuje metodu protokolu HTTP. 

## <a name="push-a-symbol-package"></a>Push balíček symbolů

podporuje vložit nový formát symbol balíčky nuget.org ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) pomocí následujících rozhraní API. 

    PUT https://www.nuget.org/api/v2/symbolpackage

Balíčky symbolů se stejným ID a verzi lze odeslat více než jednou. V následujících případech budou odmítnuty balíček symbolů.
- Balíček se stejným ID a verze neexistuje.
- Balíček symbolů se stejným ID a verze se vložil, ale ještě nebyla publikována.
- Balíček symbolů ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) je neplatný (naleznete v tématu [symbol balíček omezení](../create-packages/Symbol-Packages-snupkg.md)).

### <a name="request-parameters"></a>Parametry žádosti

Název           | V     | Typ   | Požadováno | Poznámky
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | Záhlaví | odkazy řetězců | Ano      | Třeba `X-NuGet-ApiKey: {USER_API_KEY}`.

Klíč rozhraní API je neprůhledný řetězec získali ze zdroje balíčku uživatelem a konfiguraci do klienta. Je vyžadováno žádné konkrétní řetězec formátu, ale délka klíče rozhraní API by neměl být delší než rozumnou velikost pro hodnoty hlavičky protokolu HTTP.

### <a name="request-body"></a>Text žádosti

Text žádosti o nasdílení změn symbol je stejná jako žádost subjektu, který požadavek nabízených oznámení balíčku (viz [balíček nabízených oznámení a odstranit](package-publish-resource.md)). 

### <a name="response"></a>Odpověď

Stavový kód | Význam
----------- | -------
201         | Balíček symbolů se úspěšně odeslal.
400         | Zadaný symbol balíček je neplatný.
401         | Uživatel nemá oprávnění k provedení této akce.
404         | Neexistuje odpovídající balíček se zadané ID a verzi.
409         | Balíček symbolů pomocí zadaného ID a verze se vložil, ale je ještě není k dispozici.
413         | Balíček je příliš velký.

