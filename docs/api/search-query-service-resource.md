---
title: Hledání, rozhraní API NuGet
description: Vyhledávací služba umožňuje klientům dotazovat se na balíčky podle klíčového slova a filtrovat výsledky u určitých polí balíčku.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: aed591ceba00f1820a573eacf312112db0a1c69e
ms.sourcegitcommit: 7e9c0630335ef9ec1e200e2ee9065f702e52a8ec
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/24/2020
ms.locfileid: "85292268"
---
# <a name="search"></a>Search

Je možné vyhledat balíčky dostupné ve zdroji balíčku pomocí rozhraní V3 API. Prostředek, který se používá pro hledání, je prostředek, který se `SearchQueryService` nachází v [indexu služby](service-index.md).

## <a name="versioning"></a>Správa verzí

Použijí se tyto `@type` hodnoty:

@typeosa                   | Poznámky
----------------------------- | -----
SearchQueryService            | Počáteční verze
SearchQueryService/3.0.0 – beta | Alias pro`SearchQueryService`
SearchQueryService/3.0.0 – RC   | Alias pro`SearchQueryService`
SearchQueryService/3.5.0      | Zahrnuje podporu pro `packageType` parametr dotazu.

### <a name="searchqueryservice350"></a>SearchQueryService/3.5.0
Tato verze zavádí podporu pro `packageType` parametr dotazu a `packageTypes` vlastnost Response, což umožňuje filtrování podle typu balíčků definovaných autory. Je plně zpětně kompatibilní s dotazy na `SearchQueryService` .

## <a name="base-url"></a>Základní adresa URL

Základní adresa URL následujícího rozhraní API je hodnota `@id` vlastnosti přidružené k jedné z výše uvedených `@type` hodnot prostředků. V následujícím dokumentu se použije zástupná základní adresa URL `{@id}` .

## <a name="http-methods"></a>Metody HTTP

Všechny adresy URL nalezené v registračním prostředku podporují metody HTTP `GET` a `HEAD` .

## <a name="search-for-packages"></a>Vyhledat balíčky

Rozhraní API pro vyhledávání umožňuje klientovi dotaz na stránku balíčků, které odpovídají zadanému vyhledávacímu dotazu. Interpretace vyhledávacího dotazu (například tokenizace hledaného výrazu) je určena implementací serveru, ale obecným předpokladem je, že vyhledávací dotaz se používá pro odpovídající ID balíčku, názvy, popisy a značky. Je také možné zvážit další pole metadat balíčku.

Ve výsledcích hledání by se nikdy neměl zobrazovat neuvedený balíček.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}&packageType={PACKAGETYPE}

### <a name="request-parameters"></a>Parametry žádosti

Name        | V     | Typ    | Vyžadováno | Poznámky
----------- | ------ | ------- | -------- | -----
q           | URL    | řetězec  | ne       | Hledané výrazy, které se mají použít k filtrování balíčků
Přeskočit        | URL    | celé číslo | ne       | Počet výsledků, které se mají přeskočit, pro stránkování
nezbytná        | URL    | celé číslo | ne       | Počet výsledků, které se mají vrátit, pro stránkování
předběžné verze  | URL    | Boolean | ne       | `true`nebo `false` Určete, jestli se mají zahrnout [předběžné verze balíčků](../create-packages/prerelease-packages.md)
semVerLevel | URL    | řetězec  | ne       | Řetězec verze SemVer 1.0.0 
packageType | URL    | řetězec  | ne       | Typ balíčku, který se má použít k filtrování balíčků (přidaných v `SearchQueryService/3.5.0` )

Vyhledávací dotaz `q` je analyzován způsobem, který je definován implementací serveru. nuget.org podporuje základní filtrování na [nejrůznějších polích](../consume-packages/finding-and-choosing-packages.md#search-syntax). Pokud `q` není zadán, všechny balíčky by měly být vráceny v rámci hranic, které jsou zavedeny funkcí přeskočit a převzít. Tím povolíte kartu Procházet v prostředí sady NuGet sady Visual Studio.

`skip`Parametr má výchozí hodnotu 0.

`take`Parametr by měl být celé číslo větší než nula. Implementace serveru může poskytovat maximální hodnotu.

Pokud není `prerelease` zadaný, vyloučí se balíčky předběžných verzí.

`semVerLevel`Parametr dotazu se používá pro výslovný souhlas s [SemVer balíčky 2.0.0](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).
Pokud je tento parametr dotazu vyloučený, vrátí se jenom balíčky s SemVer verzemi kompatibilními s 1.0.0 (se [standardními](../concepts/package-versioning.md) upozorněními verzí NuGet, jako jsou například řetězce verze se 4 celými čísly).
Pokud `semVerLevel=2.0.0` je k dispozici, budou vráceny balíčky kompatibilní s SemVer 1.0.0 a SemVer 2.0.0. Další informace najdete v tématu [Podpora SemVer 2.0.0 pro NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .

`packageType`Parametr se používá k dalšímu filtrování výsledků hledání pouze na balíčky, které mají alespoň jeden typ balíčku, který odpovídá názvu typu balíčku.
Pokud zadaný typ balíčku není platný typ balíčku definovaný [dokumentem typu balíčku](https://github.com/NuGet/Home/wiki/Package-Type-%5BPacking%5D), vrátí se prázdný výsledek.
Pokud je zadaný typ balíčku prázdný, nebude použit žádný filtr. Jinými slovy, pokud parametr packageType nepředáte žádnou hodnotu, bude se chovat, jako by nebyl předán parametr.

### <a name="response"></a>Odpověď

Odpověď je dokument JSON obsahující až do `take` výsledků hledání. Výsledky hledání jsou seskupeny podle ID balíčku.

Kořenový objekt JSON má následující vlastnosti:

Name      | Typ             | Vyžadováno | Poznámky
--------- | ---------------- | -------- | -----
totalHits | celé číslo          | ano      | Celkový počet shod, nesouvisející `skip` a`take`
data      | pole objektů | ano      | Výsledky hledání, které odpovídají žádosti

### <a name="search-result"></a>Výsledek hledání

Každá položka v `data` poli je objekt JSON, který se skládá ze skupiny verzí balíčku sdílejících stejné ID balíčku.
Objekt má následující vlastnosti:

Name           | Typ                       | Vyžadováno | Poznámky
-------------- | -------------------------- | -------- | -----
id             | řetězec                     | ano      | ID vyhovujícího balíčku
verze        | řetězec                     | ano      | Úplný řetězec verze SemVer 2.0.0 balíčku (může obsahovat metadata sestavení)
description    | řetězec                     | ne       | 
verze       | pole objektů           | ano      | Všechny verze balíčku, které odpovídají `prerelease` parametru
Autoři        | řetězec nebo pole řetězců | ne       | 
iconUrl        | řetězec                     | ne       | 
licenseUrl     | řetězec                     | ne       | 
vlastníka         | řetězec nebo pole řetězců | ne       | 
projectUrl     | řetězec                     | ne       | 
registrace   | řetězec                     | ne       | Absolutní adresa URL k přidruženému [registračnímu indexu](registration-base-url-resource.md#registration-index)
summary        | řetězec                     | ne       | 
tags           | řetězec nebo pole řetězců | ne       | 
title          | řetězec                     | ne       | 
totalDownloads | celé číslo                    | ne       | Tato hodnota se dá odvodit ze součtu souborů ke stažení v `versions` poli.
ověřují       | Boolean                    | ne       | Logická hodnota JSON, která označuje, jestli je balíček [ověřený](../nuget-org/id-prefix-reservation.md)
packageTypes   | pole objektů           | ano      | Typy balíčků definované autorem balíčku (přidáno v `SearchQueryService/3.5.0` )

Na nuget.org je ověřený balíček jeden, který obsahuje ID balíčku, které odpovídá předponě rezervovaného ID a vlastněné jedním z vlastníků rezervované předpony. Další informace najdete v dokumentaci k [rezervaci předpony ID](../reference/id-prefix-reservation.md).

Metadata obsažená v objektu výsledků hledání jsou pořízena z nejnovější verze balíčku. Každá položka v `versions` poli je objekt JSON s následujícími vlastnostmi:

Name      | Typ    | Vyžadováno | Poznámky
--------- | ------- | -------- | -----
@id       | řetězec  | ano      | Absolutní adresa URL k přidruženému [registračnímu listu](registration-base-url-resource.md#registration-leaf)
verze   | řetězec  | ano      | Úplný řetězec verze SemVer 2.0.0 balíčku (může obsahovat metadata sestavení)
soubory | celé číslo | ano      | Počet souborů ke stažení pro tuto konkrétní verzi balíčku

`packageTypes`Pole se vždy skládá z nejméně jedné (1) položky. Typ balíčku pro dané ID balíčku se považuje za typy balíčků definované nejnovější verzí balíčku s ohledem na ostatní parametry vyhledávání. Každá položka v `packageTypes` poli je objekt JSON s následujícími vlastnostmi:

Name      | Typ    | Vyžadováno | Poznámky
--------- | ------- | -------- | -----
name      | řetězec  | ano      | Název typu balíčku.

### <a name="sample-request"></a>Ukázková žádost

    GET https://azuresearch-usnc.nuget.org/query?q=NuGet.Versioning&prerelease=false&semVerLevel=2.0.0

### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [search-result.json](./_data/search-result.json)]
