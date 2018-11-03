---
title: Hledání rozhraní API Nugetu
description: Vyhledávací služba umožňuje klientům k vytvoření dotazu na balíčky pomocí klíčového slova a k filtrování výsledků na určitá pole balíčku.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: cfcb52ba7689f1b392c782b4ad42ba820a76c8bf
ms.sourcegitcommit: 09107c5092050f44a0c6abdfb21db73878f78bd0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/03/2018
ms.locfileid: "50981129"
---
# <a name="search"></a>Hledat

Je možné vyhledat balíčky k dispozici ve zdroji balíčku pomocí rozhraní API V3. Je prostředek, který používá pro vyhledávání `SearchQueryService` prostředek se nenašel v [index služby](service-index.md).

## <a name="versioning"></a>Správa verzí

Následující `@type` hodnoty:

@type Hodnota                   | Poznámky
----------------------------- | -----
SearchQueryService            | Počáteční verze
SearchQueryService/3.0.0-beta | Alias `SearchQueryService`
SearchQueryService/3.0.0-rc   | Alias `SearchQueryService`

## <a name="base-url"></a>Základní adresa URL

Základní adresa URL pro následující rozhraní API je hodnota `@id` vlastnost přiřazené k některému z výše uvedených prostředků `@type` hodnoty. V následujícím dokumentu, zástupný symbol základní adresa URL `{@id}` se použije.

## <a name="http-methods"></a>Metody HTTP

Všechny adresy URL, které jsou součástí zdroje podpory registrace metody HTTP `GET` a `HEAD`.

## <a name="search-for-packages"></a>Vyhledat balíčky

Rozhraní API pro vyhledávání umožňuje klientovi do dotazu pro stránku balíčků odpovídající zadanému vyhledávacímu dotazu. Výklad vyhledávací dotaz (například Tokenizace hledané termíny) je určeno implementaci serveru ale obecné očekává se, že vyhledávací dotaz se použije k porovnání s ID balíčku, názvy, popisy a značky. Mohou také zvážit další pole metadat balíčku.

Neuvedené v seznamu balíčků by nikdy nezobrazí ve výsledcích hledání.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parametry žádosti

Název        | V     | Typ    | Požadováno | Poznámky
----------- | ------ | ------- | -------- | -----
q           | Adresa URL    | odkazy řetězců  | Ne       | Hledané termíny a slouží k filtrování balíčky
Přeskočit        | Adresa URL    | integer | Ne       | Počet výsledků, chcete-li přeskočit pro stránkování
Take        | Adresa URL    | integer | Ne       | Počet výsledků, které má být vrácen pro stránkování
platnost předběžné verze  | Adresa URL    | Logická hodnota | Ne       | `true` nebo `false` určující, jestli se mají zahrnout [balíčky v předběžné verzi](../create-packages/prerelease-packages.md)
semVerLevel | Adresa URL    | odkazy řetězců  | Ne       | Řetězec verze SemVer 1.0.0 

Vyhledávací dotaz `q` je analyzován způsobem, který je definován implementací serveru. nuget.org podporuje základní filtrování [různých polí](../consume-packages/finding-and-choosing-packages.md#search-syntax). Pokud ne `q` je k dispozici, má být vrácen všechny balíčky, v rámci hranice stanovené skip a take. To umožňuje na kartě "Procházení" v prostředí sady Visual Studio NuGet.

`skip` Parametr má výchozí hodnotu 0.

`take` Parametr by měl být celé číslo větší než nula. Implementace serveru může uložit maximální hodnotu.

Pokud `prerelease` není zadán, jsou vyloučeny balíčky v předběžné verzi.

`semVerLevel` Parametr dotazu se používá k přihlášení k [SemVer 2.0.0 balíčky](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Pokud tento parametr dotazu je vyloučený, vrátí se pouze balíčky s SemVer 1.0.0 kompatibilní verze (s [standardní správy verzí NuGet](../reference/package-versioning.md) upozornění, jako jsou třeba řetězce verze 4 dali celé číslo).
Pokud `semVerLevel=2.0.0` je k dispozici, bude vrácen SemVer 1.0.0 a kompatibilní balíčky SemVer 2.0.0. Zobrazit [SemVer 2.0.0 podpora nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) Další informace.

### <a name="response"></a>Odpověď

Odpověď je dokument JSON obsahující až `take` výsledky hledání. Výsledky hledání jsou seskupené podle ID balíčku.

Kořenový objekt JSON má následující vlastnosti:

Název      | Typ             | Požadováno | Poznámky
--------- | ---------------- | -------- | -----
totalHits | integer          | Ano      | Celkový počet shod, bez ohledu na `skip` a `take`
data      | Pole objektů | Ano      | Výsledky hledání odpovídající požadavek

### <a name="search-result"></a>Výsledek vyhledávání

Každá položka v `data` pole je objekt JSON, které se skládá ze skupiny verze balíčku sdílení stejné ID balíčku.
Objekt má následující vlastnosti:

Název           | Typ                       | Požadováno | Poznámky
-------------- | -------------------------- | -------- | -----
id             | odkazy řetězců                     | Ano      | ID odpovídající balíček
verze        | odkazy řetězců                     | Ano      | Úplný řetězec SemVer 2.0.0 verze balíčku (může obsahovat metadata sestavení)
description    | odkazy řetězců                     | Ne       | 
verze       | Pole objektů           | Ano      | Všechny verze odpovídající balíček `prerelease` parametr
Autoři        | řetězec nebo pole řetězců | Ne       | 
IconUrl        | odkazy řetězců                     | Ne       | 
LicenseUrl     | odkazy řetězců                     | Ne       | 
Vlastníci         | řetězec nebo pole řetězců | Ne       | 
ProjectUrl     | odkazy řetězců                     | Ne       | 
registrace   | odkazy řetězců                     | Ne       | Absolutní adresa URL s příslušnými [registrace indexu](registration-base-url-resource.md#registration-index)
souhrn        | odkazy řetězců                     | Ne       | 
značky           | řetězec nebo pole řetězců | Ne       | 
Název          | odkazy řetězců                     | Ne       | 
totalDownloads | integer                    | Ne       | Vynásobí součtem soubory ke stažení v jde odvodit tuto hodnotu `versions` pole
ověření       | Logická hodnota                    | Ne       | JSON logická hodnota označující, jestli tento balíček představuje [ověření](../reference/id-prefix-reservation.md)

Ověřené balíček na nuget.org, je znak, který se má ID balíčku odpovídající vyhrazenou předponu ID a vlastní pomocí jedné z vlastníků vyhrazenou předponou. Další informace najdete v tématu [dokumentaci ke službě rezervace předpony ID](../reference/id-prefix-reservation.md).

Metadat obsažených v objektu výsledků hledání je převzata z nejnovější verze balíčku. Každá položka v `versions` pole je objekt JSON s následujícími vlastnostmi:

Název      | Typ    | Požadováno | Poznámky
--------- | ------- | -------- | -----
@id       | odkazy řetězců  | Ano      | Absolutní adresa URL s příslušnými [registrace typu list](registration-base-url-resource.md#registration-leaf)
verze   | odkazy řetězců  | Ano      | Úplný řetězec SemVer 2.0.0 verze balíčku (může obsahovat metadata sestavení)
Soubory ke stažení | integer | Ano      | Počet souborů ke stažení pro tento konkrétní balíček verze

### <a name="sample-request"></a>Ukázková žádost

    GET https://api-v2v3search-0.nuget.org/query?q=NuGet.Versioning&prerelease=false

### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [search-result.json](./_data/search-result.json)]
