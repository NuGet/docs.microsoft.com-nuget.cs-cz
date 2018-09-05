---
title: Automatické dokončování, rozhraní API Nugetu
description: Vyhledávací služba Automatické dokončování podporuje interaktivní zjišťování balíčku ID a verze.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 01f919dc3bbfb6752c8f8e055a3cd473ad194e75
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549080"
---
# <a name="autocomplete"></a>Automatické dokončování

Je možné vytvořit balíček ID a verzi automatického dokončování prostředí pomocí rozhraní API V3. Je prostředek, který používá pro automatické dokončování dotazů `SearchAutocompleteService` prostředek se nenašel v [index služby](service-index.md).

## <a name="versioning"></a>Správa verzí

Následující `@type` hodnoty:

@type Hodnota                          | Poznámky
------------------------------------ | -----
SearchAutocompleteService            | Počáteční verze
SearchAutocompleteService/3.0.0-beta | Alias `SearchAutocompleteService`
SearchAutocompleteService/3.0.0-rc   | Alias `SearchAutocompleteService`

## <a name="base-url"></a>Základní adresa URL

Základní adresa URL pro následující rozhraní API je hodnota `@id` vlastnost přiřazené k některému z výše uvedených prostředků `@type` hodnoty. V následujícím dokumentu, zástupný symbol základní adresa URL `{@id}` se použije.

## <a name="http-methods"></a>Metody HTTP

Všechny adresy URL, které jsou součástí zdroje podpory registrace metody HTTP `GET` a `HEAD`.

## <a name="search-for-package-ids"></a>Vyhledejte balíček ID

První funkce automatického dokončování rozhraní API podporuje vyhledávání část řetězce ID balíčku. To je skvělé, pokud byste chtěli poskytnout funkce typeahead balíčku v uživatelském rozhraní, integrovaný s zdroj balíčku NuGet.

Balíček se pouze neuvedené v seznamu verzí se nezobrazí ve výsledcích.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parametry žádosti

Název        | V     | Typ    | Požadováno | Poznámky
----------- | ------ | ------- | -------- | -----
q           | Adresa URL    | odkazy řetězců  | Ne       | Řetězec určený k porovnání s ID balíčku
Přeskočit        | Adresa URL    | integer | Ne       | Počet výsledků, chcete-li přeskočit pro stránkování
Take        | Adresa URL    | integer | Ne       | Počet výsledků, které má být vrácen pro stránkování
platnost předběžné verze  | Adresa URL    | Logická hodnota | Ne       | `true` nebo `false` určující, jestli se mají zahrnout [balíčky v předběžné verzi](../create-packages/prerelease-packages.md)
semVerLevel | Adresa URL    | odkazy řetězců  | Ne       | Řetězec verze SemVer 1.0.0 

Automatické dokončování dotazů `q` je analyzován způsobem, který je definován implementací serveru. nuget.org podporuje dotazování pro předponu tokeny typu ID balíčku, které jsou částí ID vytvářených spliting původní znaky stylem camel case a symbol.

`skip` Parametr má výchozí hodnotu 0.

`take` Parametr by měl být celé číslo větší než nula. Implementace serveru může uložit maximální hodnotu.

Pokud `prerelease` není zadán, jsou vyloučeny balíčky v předběžné verzi.

`semVerLevel` Parametr dotazu se používá k přihlášení k [SemVer 2.0.0 balíčky](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Pokud tento parametr dotazu je vyloučený, vrátí se pouze balíček ID s SemVer 1.0.0 kompatibilní verze (s [standardní správy verzí NuGet](../reference/package-versioning.md) upozornění, jako jsou třeba řetězce verze 4 dali celé číslo).
Pokud `semVerLevel=2.0.0` je k dispozici, bude vrácen SemVer 1.0.0 a kompatibilní balíčky SemVer 2.0.0. Zobrazit [SemVer 2.0.0 podpora nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) Další informace.

### <a name="response"></a>Odpověď

Odpověď je dokument JSON obsahující až `take` výsledky automatického dokončování.

Kořenový objekt JSON má následující vlastnosti:

Název      | Typ             | Požadováno | Poznámky
--------- | ---------------- | -------- | -----
totalHits | integer          | Ano      | Celkový počet shod, bez ohledu na `skip` a `take`
data      | pole řetězců | Ano      | Balíček odpovídající ID požadavku

### <a name="sample-request"></a>Ukázková žádost

ZÍSKAT https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>Výčet verzí balíčků

Po zjištění ID balíčku používat předchozí rozhraní API, může klient používat automatické dokončování rozhraní API k vytvoření výčtu verze balíčku pro ID zadaného balíčku.

Verze balíčku, který je neuvedené v seznamu se nezobrazí ve výsledcích.

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parametry žádosti

Název        | V     | Typ    | Požadováno | Poznámky
----------- | ------ | ------- | -------- | -----
id          | Adresa URL    | odkazy řetězců  | Ano      | ID balíčku k načtení verze pro
platnost předběžné verze  | Adresa URL    | Logická hodnota | Ne       | `true` nebo `false` určující, jestli se mají zahrnout [balíčky v předběžné verzi](../create-packages/prerelease-packages.md)
semVerLevel | Adresa URL    | odkazy řetězců  | Ne       | Řetězec SemVer 2.0.0 verze 

Pokud `prerelease` není zadán, jsou vyloučeny balíčky v předběžné verzi.

`semVerLevel` Parametr dotazu se používá k přihlášení k SemVer 2.0.0 balíčky. Pokud tento parametr dotazu je vyloučený, vrátí se pouze verze SemVer 1.0.0. Pokud `semVerLevel=2.0.0` je k dispozici, bude vrácen SemVer 1.0.0 a verze SemVer 2.0.0. Zobrazit [SemVer 2.0.0 podpora nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) Další informace.

### <a name="response"></a>Odpověď

Odpověď je dokument JSON obsahující všechny verze balíčků poskytovaný balíček ID, daný dotaz s parametry filtrování.

Kořenový objekt JSON má následující vlastnost:

Název      | Typ             | Požadováno | Poznámky
--------- | ---------------- | -------- | -----
data      | pole řetězců | Ano      | Verze balíčku, který odpovídá požadavku

Verze balíčku v `data` pole může obsahovat metadata sestavení SemVer 2.0.0 (třeba `1.0.0+metadata`) Pokud `semVerLevel=2.0.0` byla zadaná v řetězci dotazu.

### <a name="sample-request"></a>Ukázková žádost

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
