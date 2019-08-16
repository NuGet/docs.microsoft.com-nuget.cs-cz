---
title: Automatické dokončování, rozhraní API NuGet
description: Služba Automatické dokončování hledání podporuje interaktivní zjišťování ID a verzí balíčků.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1179ad649da560766f28c18ab6fa670fd8fa6d8b
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488296"
---
# <a name="autocomplete"></a>Automatické dokončování

Pomocí rozhraní V3 API je možné vytvořit ID balíčku a verzi prostředí pro automatické dokončování. Prostředek, který se používá k provedení dotazů automatického `SearchAutocompleteService` dokončování, je prostředek, který se nachází v [indexu služby](service-index.md).

## <a name="versioning"></a>Správa verzí

Použijí se `@type` tyto hodnoty:

@typeosa                          | Poznámky
------------------------------------ | -----
SearchAutocompleteService            | Počáteční verze
SearchAutocompleteService/3.0.0-beta | Alias pro`SearchAutocompleteService`
SearchAutocompleteService/3.0.0-rc   | Alias pro`SearchAutocompleteService`

## <a name="base-url"></a>Základní adresa URL

Základní adresa URL následujících rozhraní API je hodnota `@id` vlastnosti přidružené k jedné z výše uvedených hodnot prostředků. `@type` V následujícím dokumentu se použije zástupná základní `{@id}` adresa URL.

## <a name="http-methods"></a>Metody HTTP

Všechny adresy URL nalezené v registračním prostředku podporují metody `GET` http `HEAD`a.

## <a name="search-for-package-ids"></a>Vyhledat ID balíčků

První rozhraní API pro automatické dokončování podporuje hledání částí řetězce ID balíčku. To je skvělé, když chcete poskytnout funkci balíčku typeahead v uživatelském rozhraní integrovaném se zdrojem balíčku NuGet.

Ve výsledcích se nezobrazí balíček s pouze neuvedenými verzemi.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parametry žádosti

Name        | V     | type    | Požadováno | Poznámky
----------- | ------ | ------- | -------- | -----
q           | Adresa URL    | odkazy řetězců  | Ne       | Řetězec, který se má porovnat s ID balíčků
Přeskočit        | Adresa URL    | integer | Ne       | Počet výsledků, které se mají přeskočit, pro stránkování
nezbytná        | Adresa URL    | integer | Ne       | Počet výsledků, které se mají vrátit, pro stránkování
předběžné verze  | Adresa URL    | Logická hodnota | Ne       | `true`nebo `false` určete, jestli se mají zahrnout [předběžné verze balíčků](../create-packages/prerelease-packages.md)
semVerLevel | Adresa URL    | odkazy řetězců  | Ne       | Řetězec verze SemVer 1.0.0 

Dotaz `q` na automatické dokončování je analyzován způsobem, který je definován implementací serveru. nuget.org podporuje dotazování na předponu tokenů ID balíčku, které jsou částmi ID vytvořenými rozdělením originálu pomocí znaků písmen a symbolů ve stylu CamelCase.

`skip` Parametr má výchozí hodnotu 0.

`take` Parametr by měl být celé číslo větší než nula. Implementace serveru může poskytovat maximální hodnotu.

Pokud `prerelease` není zadaný, vyloučí se balíčky předběžných verzí.

Parametr dotazu se používá pro výslovný souhlas s [SemVer balíčky 2.0.0.](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages) `semVerLevel`
Pokud je tento parametr dotazu vyloučený, vrátí se jenom ID balíčků se kompatibilními verzemi SemVer 1.0.0 (se standardními omezeními [verzí NuGet](../concepts/package-versioning.md) , jako jsou například řetězce verze se 4 celými čísly).
Pokud `semVerLevel=2.0.0` je k dispozici, budou vráceny balíčky kompatibilní s SemVer 1.0.0 a SemVer 2.0.0. Další informace najdete v tématu [Podpora SemVer 2.0.0 pro NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .

### <a name="response"></a>Odpověď

Odpověď je dokument JSON, který obsahuje `take` výsledky automatického dokončování.

Kořenový objekt JSON má následující vlastnosti:

Name      | type             | Požadováno | Poznámky
--------- | ---------------- | -------- | -----
totalHits | integer          | ano      | Celkový počet shod, nesouvisející `skip` a`take`
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

Name        | V     | type    | Požadováno | Poznámky
----------- | ------ | ------- | -------- | -----
id          | Adresa URL    | odkazy řetězců  | ano      | ID balíčku, pro který se mají načíst verze
předběžné verze  | Adresa URL    | Logická hodnota | Ne       | `true`nebo `false` určete, jestli se mají zahrnout [předběžné verze balíčků](../create-packages/prerelease-packages.md)
semVerLevel | Adresa URL    | odkazy řetězců  | Ne       | Řetězec verze SemVer 2.0.0 

Pokud `prerelease` není zadaný, vyloučí se balíčky předběžných verzí.

Parametr `semVerLevel` dotazu se používá pro výslovný souhlas s SemVer balíčky 2.0.0. Pokud je tento parametr dotazu vyloučený, vrátí se pouze verze SemVer 1.0.0. Pokud `semVerLevel=2.0.0` je k dispozici, vrátí se obě verze SemVer 1.0.0 a SemVer 2.0.0. Další informace najdete v tématu [Podpora SemVer 2.0.0 pro NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .

### <a name="response"></a>Odpověď

Odpověď je dokument JSON obsahující všechny verze balíčků zadaného ID balíčku, které filtrují podle daných parametrů dotazu.

Kořenový objekt JSON má následující vlastnost:

Name      | type             | Požadováno | Poznámky
--------- | ---------------- | -------- | -----
data      | pole řetězců | ano      | Verze balíčku, které odpovídají danému požadavku

Verze balíčku v `data` poli mohou obsahovat metadata sestavení SemVer 2.0.0 ( `1.0.0+metadata`například), `semVerLevel=2.0.0` Pokud je v řetězci dotazu uvedena.

### <a name="sample-request"></a>Ukázková žádost

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
