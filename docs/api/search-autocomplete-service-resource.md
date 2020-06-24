---
title: Automatické dokončování, rozhraní API NuGet
description: Služba Automatické dokončování hledání podporuje interaktivní zjišťování ID a verzí balíčků.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: f574849bf99cd4da4eefd55c3dd5a0648042f0c1
ms.sourcegitcommit: 7e9c0630335ef9ec1e200e2ee9065f702e52a8ec
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/24/2020
ms.locfileid: "85292290"
---
# <a name="autocomplete"></a>Automatické dokončování

Pomocí rozhraní V3 API je možné vytvořit ID balíčku a verzi prostředí pro automatické dokončování. Prostředek, který se používá k provedení dotazů automatického dokončování, je prostředek, který se `SearchAutocompleteService` nachází v [indexu služby](service-index.md).

## <a name="versioning"></a>Správa verzí

Použijí se tyto `@type` hodnoty:

@typeosa                          | Poznámky
------------------------------------ | -----
SearchAutocompleteService            | Počáteční verze
SearchAutocompleteService/3.0.0 – beta | Alias pro`SearchAutocompleteService`
SearchAutocompleteService/3.0.0 – RC   | Alias pro`SearchAutocompleteService`
SearchAutocompleteService/3.5.0      | Zahrnuje podporu pro `packageType` parametr dotazu.

### <a name="searchautocompleteservice350"></a>SearchAutocompleteService/3.5.0
Tato verze zavádí podporu `packageType` parametru dotazu, který umožňuje filtrování podle typu balíčků definovaných autory. Je plně zpětně kompatibilní s dotazy na `SearchAutocompleteService` .

## <a name="base-url"></a>Základní adresa URL

Základní adresa URL následujících rozhraní API je hodnota `@id` vlastnosti přidružené k jedné z výše uvedených `@type` hodnot prostředků. V následujícím dokumentu se použije zástupná základní adresa URL `{@id}` .

## <a name="http-methods"></a>Metody HTTP

Všechny adresy URL nalezené v registračním prostředku podporují metody HTTP `GET` a `HEAD` .

## <a name="search-for-package-ids"></a>Vyhledat ID balíčků

První rozhraní API pro automatické dokončování podporuje hledání částí řetězce ID balíčku. To je skvělé, když chcete poskytnout funkci balíčku typeahead v uživatelském rozhraní integrovaném se zdrojem balíčku NuGet.

Ve výsledcích se nezobrazí balíček s pouze neuvedenými verzemi.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}&packageType={PACKAGETYPE}

### <a name="request-parameters"></a>Parametry žádosti

Name        | V     | Typ    | Vyžadováno | Poznámky
----------- | ------ | ------- | -------- | -----
q           | URL    | řetězec  | ne       | Řetězec, který se má porovnat s ID balíčků
Přeskočit        | URL    | celé číslo | ne       | Počet výsledků, které se mají přeskočit, pro stránkování
nezbytná        | URL    | celé číslo | ne       | Počet výsledků, které se mají vrátit, pro stránkování
předběžné verze  | URL    | Boolean | ne       | `true`nebo `false` Určete, jestli se mají zahrnout [předběžné verze balíčků](../create-packages/prerelease-packages.md)
semVerLevel | URL    | řetězec  | ne       | Řetězec verze SemVer 1.0.0 
packageType | URL    | řetězec  | ne       | Typ balíčku, který se má použít k filtrování balíčků (přidaných v `SearchAutocompleteService/3.5.0` )

Dotaz na automatické dokončování `q` je analyzován způsobem, který je definován implementací serveru. nuget.org podporuje dotazování na předponu tokenů ID balíčku, které jsou částmi ID vytvořenými rozdělením originálu pomocí znaků písmen a symbolů ve stylu CamelCase.

`skip`Parametr má výchozí hodnotu 0.

`take`Parametr by měl být celé číslo větší než nula. Implementace serveru může poskytovat maximální hodnotu.

Pokud není `prerelease` zadaný, vyloučí se balíčky předběžných verzí.

`semVerLevel`Parametr dotazu se používá pro výslovný souhlas s [SemVer balíčky 2.0.0](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Pokud je tento parametr dotazu vyloučený, vrátí se jenom ID balíčků se kompatibilními verzemi SemVer 1.0.0 (se [standardními omezeními verzí NuGet](../concepts/package-versioning.md) , jako jsou například řetězce verze se 4 celými čísly).
Pokud `semVerLevel=2.0.0` je k dispozici, budou vráceny balíčky kompatibilní s SemVer 1.0.0 a SemVer 2.0.0. Další informace najdete v tématu [Podpora SemVer 2.0.0 pro NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .

`packageType`Parametr se používá k dalšímu filtrování výsledků automatického dokončování do pouze balíčků, které mají alespoň jeden typ balíčku, který odpovídá názvu typu balíčku.
Pokud zadaný typ balíčku není platný typ balíčku definovaný [dokumentem typu balíčku](https://github.com/NuGet/Home/wiki/Package-Type-%5BPacking%5D), vrátí se prázdný výsledek.
Pokud je zadaný typ balíčku prázdný, nebude použit žádný filtr. Jinými slovy, nepředání hodnoty do `packageType` parametru se bude chovat, jako by nebyl předán parametr.

### <a name="response"></a>Odpověď

Odpověď je dokument JSON, který obsahuje `take` Výsledky automatického dokončování.

Kořenový objekt JSON má následující vlastnosti:

Name      | Typ             | Vyžadováno | Poznámky
--------- | ---------------- | -------- | -----
totalHits | celé číslo          | ano      | Celkový počet shod, nesouvisející `skip` a`take`
data      | pole řetězců | ano      | ID balíčků, které odpovídá požadavek

### <a name="sample-request"></a>Ukázková žádost

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>Zobrazení výčtu verzí balíčků

Po zjištění ID balíčku pomocí předchozího rozhraní API může klient použít rozhraní API pro automatické dokončování k zobrazení výčtu verzí balíčků pro zadané ID balíčku.

Ve výsledcích se nezobrazí verze balíčku, který není uveden v seznamu.

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parametry žádosti

Name        | V     | Typ    | Vyžadováno | Poznámky
----------- | ------ | ------- | -------- | -----
id          | URL    | řetězec  | ano      | ID balíčku, pro který se mají načíst verze
předběžné verze  | URL    | Boolean | ne       | `true`nebo `false` Určete, jestli se mají zahrnout [předběžné verze balíčků](../create-packages/prerelease-packages.md)
semVerLevel | URL    | řetězec  | ne       | Řetězec verze SemVer 2.0.0 

Pokud není `prerelease` zadaný, vyloučí se balíčky předběžných verzí.

`semVerLevel`Parametr dotazu se používá pro výslovný souhlas s SemVer balíčky 2.0.0. Pokud je tento parametr dotazu vyloučený, vrátí se pouze verze SemVer 1.0.0. Pokud `semVerLevel=2.0.0` je k dispozici, vrátí se obě verze SemVer 1.0.0 a SemVer 2.0.0. Další informace najdete v tématu [Podpora SemVer 2.0.0 pro NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .

### <a name="response"></a>Odpověď

Odpověď je dokument JSON obsahující všechny verze balíčků zadaného ID balíčku, které filtrují podle daných parametrů dotazu.

Kořenový objekt JSON má následující vlastnost:

Name      | Typ             | Vyžadováno | Poznámky
--------- | ---------------- | -------- | -----
data      | pole řetězců | ano      | Verze balíčku, které odpovídají danému požadavku

Verze balíčku v `data` poli mohou obsahovat metadata sestavení SemVer 2.0.0 (například `1.0.0+metadata` ), pokud `semVerLevel=2.0.0` je v řetězci dotazu uvedena.

### <a name="sample-request"></a>Ukázková žádost

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
