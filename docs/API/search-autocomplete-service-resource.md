---
title: "Automatické dokončování, NuGet rozhraní API | Microsoft Docs"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Službu vyhledávání automatického dokončování podporuje interaktivní zjišťování ID balíčku a verze."
keywords: "Rozhraní API funkce automatického dokončování NuGet, ID balíčku NuGet vyhledávání, ID balíčku dílčí řetězec"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 7c984ca61799293d7832851b80cf3fefc4734288
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/02/2018
---
# <a name="autocomplete"></a>Automatické dokončování

Je možné balíček ID a verzi automatického dokončování prostředí pomocí rozhraní API V3. Prostředku používaného pro zadávání dotazů automatického dokončování je `SearchAutocompleteService` v nalezen prostředek [indexu služby](service-index.md).

## <a name="versioning"></a>Správa verzí

Následující `@type` se používají hodnoty:

@typeHodnota                          | Poznámky
------------------------------------ | -----
SearchAutocompleteService            | Původní verze
SearchAutocompleteService/3.0.0-beta | Alias`SearchAutocompleteService`
SearchAutocompleteService/3.0.0-rc   | Alias`SearchAutocompleteService`

## <a name="base-url"></a>Základní adresu URL

Základní adresu URL pro následující rozhraní API je hodnota `@id` vlastnost spojená s jedním z výše uvedených prostředků `@type` hodnoty. V následujícím dokumentu zástupného textu základní adresa URL `{@id}` se použije.

## <a name="http-methods"></a>Metody HTTP

Všechny adresy URL v podpory registrace prostředků nalezen metody HTTP `GET` a `HEAD`.

## <a name="search-for-package-ids"></a>Vyhledávání pro balíček ID

První autocomplete rozhraní API podporuje hledání část řetězce ID balíčku. To je skvělé, pokud chcete poskytovat funkce typeahead balíčku v uživatelském rozhraní integrovat zdroje balíčku NuGet.

Balíček se pouze neuvedené verzí se nezobrazí ve výsledcích.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parametry žádosti

Název        | V     | Typ    | Požadováno | Poznámky
----------- | ------ | ------- | -------- | -----
q           | Adresa URL    | odkazy řetězců  | Ne       | Řetězec, který má být porovnán balíček ID
Přeskočit        | Adresa URL    | integer | Ne       | Počet výsledků tak, aby přeskočil pro stránkování
proveďte        | Adresa URL    | integer | Ne       | Počet výsledků, které má být vrácen pro stránkování
předběžné verze  | Adresa URL    | Logická hodnota | Ne       | `true`nebo `false` určení, jestli se mají zahrnout [předběžné verze balíčků](../create-packages/prerelease-packages.md)
semVerLevel | Adresa URL    | odkazy řetězců  | Ne       | Řetězec verze o SemVer 1.0.0 

Automatické dokončování dotazů `q` je analyzována způsobem, který je definován implementaci serveru. nuget.org podporuje dotazování pro předponu tokenů ID balíčku, které jsou částí ID vyprodukované spliting původní formátu camelCase případ a symbol znaky.

`skip` Výchozí hodnoty parametrů na hodnotu 0.

`take` Parametr by měl být celé číslo větší než nula. Implementaci serveru může uložit maximální hodnotu.

Pokud `prerelease` není zadána, jsou vyloučeny předběžné verze balíčků.

`semVerLevel` Parametr dotazu se používá k vyslovení souhlasu s [SemVer 2.0.0 balíčky](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Pokud tento parametr dotazu je vyloučená, bude vrácen pouze balíček ID s kompatibilní verze SemVer 1.0.0 (s [standardní verze NuGet](../reference/package-versioning.md) upozornění, jako jsou třeba řetězce verze se 4 kusy celé číslo).
Pokud `semVerLevel=2.0.0` je zadáno, bude vrácen SemVer 1.0.0 a SemVer 2.0.0 kompatibilní balíčky. Najdete v článku [SemVer 2.0.0 podpora nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) Další informace.

### <a name="response"></a>Odpověď

Odpovědí je dokument JSON obsahující až `take` výsledky funkce automatického dokončování.

Kořenový objekt JSON má následující vlastnosti:

Název      | Typ             | Požadováno | Poznámky
--------- | ---------------- | -------- | -----
totalHits | integer          | Ano      | Celkový počet shod, bez ohledu na `skip` a`take`
data      | Pole řetězců. | Ano      | ID balíčku odpovídala požadavku

### <a name="sample-request"></a>Ukázková žádost

GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>Zobrazení výčtu verze balíčku

Po zjištění ID balíčku pomocí předchozího rozhraní API může klient používat automatické dokončování rozhraní API se vytvořit výčet verze balíčku pro ID zadaný balíček.

Verze balíčku, který neuvedené nezobrazí ve výsledcích.

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parametry žádosti

Název        | V     | Typ    | Požadováno | Poznámky
----------- | ------ | ------- | -------- | -----
id          | Adresa URL    | odkazy řetězců  | Ano      | ID balíčku se načíst verze pro
předběžné verze  | Adresa URL    | Logická hodnota | Ne       | `true`nebo `false` určení, jestli se mají zahrnout [předběžné verze balíčků](../create-packages/prerelease-packages.md)
semVerLevel | Adresa URL    | odkazy řetězců  | Ne       | Řetězec verze o SemVer 2.0.0 

Pokud `prerelease` není zadána, jsou vyloučeny předběžné verze balíčků.

`semVerLevel` Parametr dotazu se používá k vyslovení souhlasu s SemVer 2.0.0 balíčky. Pokud tento parametr dotazu je vyloučená, bude vrácen pouze SemVer 1.0.0 verze. Pokud `semVerLevel=2.0.0` je zadáno, bude vrácen SemVer 1.0.0 a SemVer 2.0.0 verze. Najdete v článku [SemVer 2.0.0 podpora nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) Další informace.

### <a name="response"></a>Odpověď

Odpověď je dokument JSON obsahující všechny verze balíčku zadaný balíček ID, filtrování podle parametrů daný dotaz.

Kořenový objekt JSON má následující vlastnost:

Název      | Typ             | Požadováno | Poznámky
--------- | ---------------- | -------- | -----
data      | Pole řetězců. | Ano      | Verze balíčku odpovídala požadavku

Verze v balíčku `data` pole může obsahovat metadata sestavení SemVer 2.0.0 (například `1.0.0+metadata`) Pokud `semVerLevel=2.0.0` zadaná v řetězci dotazu.

### <a name="sample-request"></a>Ukázková žádost

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
