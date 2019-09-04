---
title: Hledání, rozhraní API NuGet
description: Vyhledávací služba umožňuje klientům dotazovat se na balíčky podle klíčového slova a filtrovat výsledky u určitých polí balíčku.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: be25e9bf72b9115de8ae55f6296195fed3152f10
ms.sourcegitcommit: ac9a00ccaf90e539a381e92b650074910b21eb0d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/03/2019
ms.locfileid: "70235122"
---
# <a name="search"></a>Hledat

Je možné vyhledat balíčky dostupné ve zdroji balíčku pomocí rozhraní V3 API. Prostředek, který se používá pro hledání `SearchQueryService` , je prostředek, který se nachází v [indexu služby](service-index.md).

## <a name="versioning"></a>Správa verzí

Použijí se `@type` tyto hodnoty:

@typeosa                   | Poznámky
----------------------------- | -----
SearchQueryService            | Počáteční verze
SearchQueryService/3.0.0-beta | Alias pro`SearchQueryService`
SearchQueryService/3.0.0-rc   | Alias pro`SearchQueryService`

## <a name="base-url"></a>Základní adresa URL

Základní adresa URL následujícího rozhraní API je hodnota `@id` vlastnosti přidružené k jedné z výše uvedených hodnot prostředků. `@type` V následujícím dokumentu se použije zástupná základní `{@id}` adresa URL.

## <a name="http-methods"></a>Metody HTTP

Všechny adresy URL nalezené v registračním prostředku podporují metody `GET` http `HEAD`a.

## <a name="search-for-packages"></a>Vyhledat balíčky

Rozhraní API pro vyhledávání umožňuje klientovi dotaz na stránku balíčků, které odpovídají zadanému vyhledávacímu dotazu. Interpretace vyhledávacího dotazu (například tokenizace hledaného výrazu) je určena implementací serveru, ale obecným předpokladem je, že vyhledávací dotaz se používá pro odpovídající ID balíčku, názvy, popisy a značky. Je také možné zvážit další pole metadat balíčku.

Ve výsledcích hledání by se nikdy neměl zobrazovat neuvedený balíček.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>Parametry žádosti

Name        | V     | type    | Požadováno | Poznámky
----------- | ------ | ------- | -------- | -----
q           | Adresa URL    | odkazy řetězců  | Ne       | Hledané výrazy, které se mají použít k filtrování balíčků
Přeskočit        | Adresa URL    | integer | Ne       | Počet výsledků, které se mají přeskočit, pro stránkování
nezbytná        | Adresa URL    | integer | Ne       | Počet výsledků, které se mají vrátit, pro stránkování
předběžné verze  | Adresa URL    | Logická hodnota | Ne       | `true`nebo `false` určete, jestli se mají zahrnout [předběžné verze balíčků](../create-packages/prerelease-packages.md)
semVerLevel | Adresa URL    | odkazy řetězců  | Ne       | Řetězec verze SemVer 1.0.0 

Vyhledávací dotaz `q` je analyzován způsobem, který je definován implementací serveru. nuget.org podporuje základní filtrování na [nejrůznějších polích](../consume-packages/finding-and-choosing-packages.md#search-syntax). `q` Pokud není zadán, všechny balíčky by měly být vráceny v rámci hranic, které jsou zavedeny funkcí přeskočit a převzít. Tím povolíte kartu Procházet v prostředí sady NuGet sady Visual Studio.

`skip` Parametr má výchozí hodnotu 0.

`take` Parametr by měl být celé číslo větší než nula. Implementace serveru může poskytovat maximální hodnotu.

Pokud `prerelease` není zadaný, vyloučí se balíčky předběžných verzí.

Parametr dotazu se používá pro výslovný souhlas s [SemVer balíčky 2.0.0.](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages) `semVerLevel`
Pokud je tento parametr dotazu vyloučený, vrátí se jenom balíčky s SemVer verzemi kompatibilními s 1.0.0 (se [standardními](../concepts/package-versioning.md) upozorněními verzí NuGet, jako jsou například řetězce verze se 4 celými čísly).
Pokud `semVerLevel=2.0.0` je k dispozici, budou vráceny balíčky kompatibilní s SemVer 1.0.0 a SemVer 2.0.0. Další informace najdete v tématu [Podpora SemVer 2.0.0 pro NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .

### <a name="response"></a>Odpověď

Odpověď je dokument JSON obsahující až do `take` výsledků hledání. Výsledky hledání jsou seskupeny podle ID balíčku.

Kořenový objekt JSON má následující vlastnosti:

Name      | type             | Požadováno | Poznámky
--------- | ---------------- | -------- | -----
totalHits | integer          | ano      | Celkový počet shod, nesouvisející `skip` a`take`
data      | pole objektů | ano      | Výsledky hledání, které odpovídají žádosti

### <a name="search-result"></a>Výsledek hledání

Každá položka v `data` poli je objekt JSON, který se skládá ze skupiny verzí balíčku sdílejících stejné ID balíčku.
Objekt má následující vlastnosti:

Name           | type                       | Požadováno | Poznámky
-------------- | -------------------------- | -------- | -----
id             | odkazy řetězců                     | ano      | ID vyhovujícího balíčku
verze        | odkazy řetězců                     | ano      | Úplný řetězec verze SemVer 2.0.0 balíčku (může obsahovat metadata sestavení)
description    | odkazy řetězců                     | Ne       | 
verze       | pole objektů           | ano      | Všechny verze balíčku, které odpovídají `prerelease` parametru
Autoři        | řetězec nebo pole řetězců | Ne       | 
iconUrl        | odkazy řetězců                     | Ne       | 
licenseUrl     | odkazy řetězců                     | Ne       | 
vlastníka         | řetězec nebo pole řetězců | Ne       | 
projectUrl     | odkazy řetězců                     | Ne       | 
registrace   | odkazy řetězců                     | Ne       | Absolutní adresa URL k přidruženému [registračnímu indexu](registration-base-url-resource.md#registration-index)
souhrn        | odkazy řetězců                     | Ne       | 
značky           | řetězec nebo pole řetězců | Ne       | 
název          | odkazy řetězců                     | Ne       | 
totalDownloads | integer                    | Ne       | Tato hodnota se dá odvodit ze součtu souborů ke stažení v `versions` poli.
ověřují       | Logická hodnota                    | Ne       | Logická hodnota JSON, která označuje, jestli je balíček [ověřený](../nuget-org/id-prefix-reservation.md)

Na nuget.org je ověřený balíček jeden, který obsahuje ID balíčku, které odpovídá předponě rezervovaného ID a vlastněné jedním z vlastníků rezervované předpony. Další informace najdete v dokumentaci k [rezervaci předpony ID](../reference/id-prefix-reservation.md).

Metadata obsažená v objektu výsledků hledání jsou pořízena z nejnovější verze balíčku. Každá položka v `versions` poli je objekt JSON s následujícími vlastnostmi:

Name      | type    | Požadováno | Poznámky
--------- | ------- | -------- | -----
@id       | odkazy řetězců  | ano      | Absolutní adresa URL k přidruženému [registračnímu listu](registration-base-url-resource.md#registration-leaf)
verze   | odkazy řetězců  | ano      | Úplný řetězec verze SemVer 2.0.0 balíčku (může obsahovat metadata sestavení)
soubory | integer | ano      | Počet souborů ke stažení pro tuto konkrétní verzi balíčku

### <a name="sample-request"></a>Ukázková žádost

    GET https://azuresearch-usnc.nuget.org/query?q=NuGet.Versioning&prerelease=false&semVerLevel=2.0.0

### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [search-result.json](./_data/search-result.json)]
