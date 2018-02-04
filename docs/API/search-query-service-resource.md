---
title: "Vyhledávání, NuGet rozhraní API | Microsoft Docs"
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
description: "Služba vyhledávání umožňuje klientům dotazu pro balíčků – klíčové slovo a výsledky filtru na určitá pole balíčku."
keywords: "Rozhraní API search NuGet, NuGet zjistit balíčky, rozhraní API pro balíčky NuGet dotazu, rozhraní API procházet balíčky NuGet"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 612ce0f46b654335a29bb36a64b27525994162ed
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/02/2018
---
# <a name="search"></a>Hledat

Je možné vyhledat balíčků dostupných ve zdroji balíčku pomocí rozhraní API V3. Prostředek používá pro vyhledávání `SearchQueryService` v nalezen prostředek [indexu služby](service-index.md).

## <a name="versioning"></a>Správa verzí

Následující `@type` se používají hodnoty:

@typeHodnota                   | Poznámky
----------------------------- | -----
SearchQueryService            | Původní verze
SearchQueryService/3.0.0-beta | Alias`SearchQueryService`
SearchQueryService/3.0.0-rc   | Alias`SearchQueryService`

## <a name="base-url"></a>Základní adresu URL

Základní adresu URL pro následující rozhraní API je hodnota `@id` vlastnost spojená s jedním z výše uvedených prostředků `@type` hodnoty. V následujícím dokumentu zástupného textu základní adresa URL `{@id}` se použije.

## <a name="http-methods"></a>Metody HTTP

Všechny adresy URL v podpory registrace prostředků nalezen metody HTTP `GET` a `HEAD`.

## <a name="search-for-packages"></a>Vyhledejte balíčky

Hledání rozhraní API umožňuje klientovi dotazu pro stránku balíčků odpovídající zadaná vyhledávací dotaz. Výklad vyhledávací dotaz (například Tokenizace hledaným výrazům) je dáno implementaci serveru ale obecné očekává se, že vyhledávací dotaz se používá pro odpovídající ID balíčku, nadpisy, popisy a značky. Další pole metadat balíčku může také zvážit.

Balíček není uveden v seznamu by se nikdy zobrazit ve výsledcích hledání.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parametry žádosti

Název        | V     | Typ    | Požadováno | Poznámky
----------- | ------ | ------- | -------- | -----
q           | Adresa URL    | odkazy řetězců  | Ne       | Hledané termíny a slouží jako filtr balíčky
Přeskočit        | Adresa URL    | integer | Ne       | Počet výsledků tak, aby přeskočil pro stránkování
proveďte        | Adresa URL    | integer | Ne       | Počet výsledků, které má být vrácen pro stránkování
předběžné verze  | Adresa URL    | Logická hodnota | Ne       | `true`nebo `false` určení, jestli se mají zahrnout [předběžné verze balíčků](../create-packages/prerelease-packages.md)
semVerLevel | Adresa URL    | odkazy řetězců  | Ne       | Řetězec verze o SemVer 1.0.0 

Vyhledávací dotaz `q` je analyzována způsobem, který je definován implementaci serveru. nuget.org podporuje základní filtrování [různých polí](../consume-packages/finding-and-choosing-packages.md#search-syntax). Pokud žádné `q` je zadáno, má být vrácen všechny balíčky v hranicích způsobené přeskočit a proveďte. To umožňuje kartě "Browse" v prostředí NuGet sady Visual Studio.

`skip` Výchozí hodnoty parametrů na hodnotu 0.

`take` Parametr by měl být celé číslo větší než nula. Implementaci serveru může uložit maximální hodnotu.

Pokud `prerelease` není zadána, jsou vyloučeny předběžné verze balíčků.

`semVerLevel` Parametr dotazu se používá k vyslovení souhlasu s [SemVer 2.0.0 balíčky](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Pokud tento parametr dotazu je vyloučená, bude vrácen pouze balíčky s kompatibilní verze SemVer 1.0.0 (s [standardní verze NuGet](../reference/package-versioning.md) upozornění, jako jsou třeba řetězce verze se 4 kusy celé číslo).
Pokud `semVerLevel=2.0.0` je zadáno, bude vrácen SemVer 1.0.0 a SemVer 2.0.0 kompatibilní balíčky. Najdete v článku [SemVer 2.0.0 podpora nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) Další informace.

### <a name="response"></a>Odpověď

Odpovědí je dokument JSON obsahující až `take` výsledky hledání. Výsledky hledání jsou seskupené podle ID balíčku.

Kořenový objekt JSON má následující vlastnosti:

Název      | Typ             | Požadováno | Poznámky
--------- | ---------------- | -------- | -----
totalHits | integer          | Ano      | Celkový počet shod, bez ohledu na `skip` a`take`
data      | Pole objektů | Ano      | Výsledky hledání odpovídala požadavku

### <a name="search-result"></a>výsledek hledání

Jednotlivé položky `data` pole je objekt JSON, které se skládá z skupinu verze balíčku sdílení stejné ID balíčku.
Objekt má následující vlastnosti:

Název           | Typ                       | Požadováno | Poznámky
-------------- | -------------------------- | -------- | -----
id             | odkazy řetězců                     | Ano      | ID odpovídající balíčku
verze        | odkazy řetězců                     | Ano      | Úplný řetězec SemVer 2.0.0 verze balíčku (může obsahovat metadata sestavení)
description    | odkazy řetězců                     | Ne       | 
verze       | Pole objektů           | Ano      | Všechny verze balíčku odpovídajících `prerelease` parametr
Autoři        | řetězec nebo pole řetězců. | Ne       | 
IconUrl        | odkazy řetězců                     | Ne       | 
licenseUrl     | odkazy řetězců                     | Ne       | 
Vlastníci         | řetězec nebo pole řetězců. | Ne       | 
projectUrl     | odkazy řetězců                     | Ne       | 
registrace   | odkazy řetězců                     | Ne       | Absolutní adresa URL s příslušnými [index registrace](registration-base-url-resource.md#registration-index)
souhrn        | odkazy řetězců                     | Ne       | 
značky           | řetězec nebo pole řetězců. | Ne       | 
Název          | odkazy řetězců                     | Ne       | 
totalDownloads | integer                    | Ne       | Tato hodnota se nedá odvodit součtem probíhající stahování `versions` pole
Ověření       | Logická hodnota                    | Ne       | JSON logickou hodnotu udávající, zda tento balíček je [ověření](../reference/id-prefix-reservation.md)

V nuget.org je ověřené balíček takovou, která má odpovídající vyhrazenou předponu ID ID balíčku a vlastní jeden vyhrazený obor názvů vlastníků. Další informace najdete v tématu [dokumentaci o rezervaci předpona ID](../reference/id-prefix-reservation.md).

Metadat obsažených v objektu výsledků hledání je založena na nejnovější verzi balíčku. Jednotlivé položky `versions` pole je objekt JSON s následujícími vlastnostmi:

Název      | Typ    | Požadováno | Poznámky
--------- | ------- | -------- | -----
@id       | odkazy řetězců  | Ano      | Absolutní adresa URL s příslušnými [listu registrace](registration-base-url-resource.md#registration-leaf)
verze   | odkazy řetězců  | Ano      | Úplný řetězec SemVer 2.0.0 verze balíčku (může obsahovat metadata sestavení)
Soubory ke stažení | integer | Ano      | Počet souborů ke stažení pro tuto verzi konkrétním balíčku

### <a name="sample-request"></a>Ukázková žádost

    GET https://api-v2v3search-0.nuget.org/query?q=NuGet.Versioning&prerelease=false

### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [search-result.json](./_data/search-result.json)]
