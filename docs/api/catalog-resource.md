---
title: Prostředek katalogu, rozhraní NuGet V3 API
description: Katalog je index všech balíčků vytvořených a odstraněných v nuget.org.
author: joelverhagen
ms.author: jver
ms.date: 10/30/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 11485f583d6993919f6bb8acabcc87d9e4261975
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774159"
---
# <a name="catalog"></a>Katalog

**Katalog** je prostředek, který zaznamenává všechny operace balíčku ve zdroji balíčku, například vytvoření a odstranění. Prostředek katalogu má `Catalog` typ v [indexu služby](service-index.md). Tento prostředek můžete použít k [dotazování na všechny publikované balíčky](../guides/api/query-for-all-published-packages.md).

> [!Note]
> Protože katalog nepoužívá oficiální klient NuGet, neimplementuje katalog všechny zdroje balíčků.

> [!Note]
> V současné době není katalog nuget.org k dispozici v Číně. Další podrobnosti najdete v tématu [NuGet/NuGetGallery # 4949](https://github.com/NuGet/NuGetGallery/issues/4949).

## <a name="versioning"></a>Správa verzí

Použije se následující `@type` hodnota:

@type osa   | Poznámky
------------- | -----
Katalog/3.0.0 | Počáteční verze

## <a name="base-url"></a>Základní adresa URL

Adresa URL vstupního bodu pro následující rozhraní API je hodnota `@id` vlastnosti přidružené k výše uvedeným `@type` hodnotám prostředku. Toto téma používá zástupnou adresu URL `{@id}` .

## <a name="http-methods"></a>Metody HTTP

Všechny adresy URL nalezené v prostředku katalogu podporují pouze metody HTTP `GET` a `HEAD` .

## <a name="catalog-index"></a>Index katalogu

Rejstřík katalogu je dokument v dobře známém umístění, které obsahuje seznam položek katalogu, seřazené chronologicky. Je to vstupní bod prostředku katalogu.

Index se skládá ze stránek katalogu. Každá stránka katalogu obsahuje položky katalogu. Každá položka katalogu představuje událost týkající se jednoho balíčku v určitém časovém bodě. Položka katalogu může představovat balíček, který byl vytvořen, není v seznamu, přepsán nebo odstraněn ze zdroje balíčku. Po zpracování položek katalogu v chronologickém pořadí může klient sestavit aktuální pohled na každý balíček, který existuje ve zdroji balíčku v3.

V krátkých objektech blob katalogu mají následující hierarchickou strukturu:

- **Index**: vstupní bod katalogu.
- **Stránka**: seskupení položek katalogu.
- **List**: dokument reprezentující položku katalogu, který je snímkem stavu jednoho balíčku.

Každý objekt katalogu má vlastnost s názvem, která `commitTimeStamp` představuje, když byla položka přidána do katalogu. Položky katalogu jsou přidány do stránky katalogu v dávkách s názvem potvrzení. Všechny položky katalogu ve stejném potvrzení mají stejné časové razítko potvrzení ( `commitTimeStamp` ) a ID potvrzení ( `commitId` ). Katalogové položky umístěné ve stejném potvrzení reprezentují události, ke kterým došlo přibližně ke stejnému bodu v čase ve zdroji balíčku. V rámci potvrzení katalogu není žádné řazení.

Vzhledem k tomu, že každé ID a verzi balíčku je jedinečné, v potvrzení nikdy nebude více než jedna položka katalogu. Tím se zajistí, že položky katalogu pro jeden balíček se můžou vždycky jednoznačně seřadit s ohledem na časové razítko potvrzení.

V katalogu není nikdy více než jedno potvrzení na `commitTimeStamp` . Jinými slovy, `commitId` je redundantní s `commitTimeStamp` .

Na rozdíl od [prostředku metadat balíčku](registration-base-url-resource.md), který je indexován identifikátorem ID balíčku, je katalog indexován (a Queryable) pouze podle času.

Položky katalogu se vždycky přidávají do katalogu ve rovnoměrně zvětšující zvýšeném chronologickém pořadí. To znamená, že pokud se přidají potvrzení katalogu v čase X, nepřidá se žádné potvrzení katalogu za čas menší nebo rovno X.

Následující požadavek Načte index katalogu.

```
GET {@id}
```

Index katalogu je dokument JSON, který obsahuje objekt s následujícími vlastnostmi:

Název            | Typ             | Vyžadováno | Poznámky
--------------- | ---------------- | -------- | -----
commitId        | řetězec           | ano      | Jedinečné ID přidružené k nejnovějšímu potvrzení změn
commitTimeStamp | řetězec           | ano      | Časové razítko posledního potvrzení změn
count           | integer          | ano      | Počet stránek v indexu
položek           | pole objektů | ano      | Pole objektů, každý objekt, který představuje stránku

Každý prvek v `items` poli je objekt s minimálními podrobnostmi o každé stránce. Tyto objekty stránky neobsahují katalog (položky). Pořadí prvků v tomto poli není definováno. Stránky lze seřadit podle klienta v paměti pomocí jejich `commitTimeStamp` Vlastnosti.

Při zavedení nových stránek se `count` zvýší a v poli se zobrazí nové objekty `items` .

Když se do katalogu přidají položky, index se `commitId` změní a `commitTimeStamp` narůstá. Tyto dvě vlastnosti jsou v podstatě souhrnem všech stránek `commitId` a `commitTimeStamp` hodnot v poli `items` .

### <a name="catalog-page-object-in-the-index"></a>Objekt stránky katalogu v indexu

Objekty stránky katalogu nalezené ve vlastnosti index katalogu `items` mají následující vlastnosti:

Název            | Typ    | Vyžadováno | Poznámky
--------------- | ------- | -------- | -----
@id             | řetězec  | ano      | Adresa URL pro načtení stránky katalogu
commitId        | řetězec  | ano      | Jedinečné ID přidružené k nejnovějšímu potvrzení na této stránce
commitTimeStamp | řetězec  | ano      | Časové razítko posledního potvrzení na této stránce
count           | integer | ano      | Počet položek na stránce katalogu

Na rozdíl od [prostředku metadat balíčku](registration-base-url-resource.md) , který v některých případech zanechá v indexu, zůstanou listy v katalogu nikdy vložené do indexu a musí se vždy načíst pomocí `@id` adresy URL stránky.

### <a name="sample-request"></a>Ukázková žádost

```
GET https://api.nuget.org/v3/catalog0/index.json
```

### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [catalog-index.json](./_data/catalog-index.json)]

## <a name="catalog-page"></a>Stránka katalogu

Stránka katalogu je kolekce položek katalogu. Je to dokument načtený pomocí jedné z `@id` hodnot nalezených v indexu katalogu. Adresa URL stránky katalogu není zamýšlena jako předvídatelná a měla by být zjištěna pouze pomocí indexu katalogu.

Nové položky katalogu jsou přidány na stránku v indexu katalogu pouze s nejvyšším časovým razítkem potvrzení nebo na novou stránku. Po přidání stránky s vyšším časovým razítkem potvrzení do katalogu se starší stránky nikdy nepřidaly nebo nezměnily.

Dokument stránky katalogu je objekt JSON s následujícími vlastnostmi:

Název            | Typ             | Vyžadováno | Poznámky
--------------- | ---------------- | -------- | -----
commitId        | řetězec           | ano      | Jedinečné ID přidružené k nejnovějšímu potvrzení na této stránce
commitTimeStamp | řetězec           | ano      | Časové razítko posledního potvrzení na této stránce
count           | integer          | ano      | Počet položek na stránce
položek           | pole objektů | ano      | Položky katalogu na této stránce
nadřazený          | řetězec           | ano      | Adresa URL indexu katalogu

Každý prvek v `items` poli je objekt s některými minimálními podrobnostmi o položce katalogu. Tyto objekty položek neobsahují všechna data položky katalogu. Pořadí položek v poli stránky není `items` definováno. Položky lze seřadit podle klienta v paměti pomocí jejich `commitTimeStamp` Vlastnosti.

Počet položek katalogu na stránce je definován implementací serveru. Pro nuget.org se na každé stránce nachází maximálně 550 položek, i když může být pro některé stránky menší počet položek v závislosti na velikosti další dávky potvrzení v daném časovém okamžiku.

Při zavedení nových položek se `count` zvýší a nové objekty položky katalogu se zobrazí v poli `items` .

Když jsou položky přidány na stránku, `commitId` změny a `commitTimeStamp` zvýšení. Tyto dvě vlastnosti jsou v podstatě souhrnem všech `commitId` hodnot a `commitTimeStamp` v poli `items` .

### <a name="catalog-item-object-in-a-page"></a>Objekt položky katalogu na stránce

Objekty položky katalogu, které byly nalezeny ve vlastnosti stránky katalogu, `items` mají následující vlastnosti:

Název            | Typ    | Vyžadováno | Poznámky
--------------- | ------- | -------- | -----
@id             | řetězec  | ano      | Adresa URL pro načtení položky katalogu
@type           | řetězec  | ano      | Typ položky katalogu
commitId        | řetězec  | ano      | ID potvrzení přidružené k této položce katalogu
commitTimeStamp | řetězec  | ano      | Časové razítko potvrzení této položky katalogu
NuGet: ID        | řetězec  | ano      | ID balíčku, se kterým tento list souvisí
NuGet: verze   | řetězec  | ano      | Verze balíčku, se kterou tento list souvisí

`@type`Hodnota bude jedna z následujících dvou hodnot:

1. `nuget:PackageDetails`: to odpovídá `PackageDetails` typu v dokumentu listu katalogu.
1. `nuget:PackageDelete`: odpovídá `PackageDelete` typu v dokumentu listu katalogu.

Další podrobnosti o tom, co každý typ znamená, naleznete níže v [odpovídajících typech položek](#item-types) .

### <a name="sample-request"></a>Ukázková žádost

```
GET https://api.nuget.org/v3/catalog0/page2926.json
```

### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [catalog-page.json](./_data/catalog-page.json)]

## <a name="catalog-leaf"></a>List katalogu

List katalogu obsahuje metadata týkající se konkrétního ID a verze balíčku v určitém časovém okamžiku. Je to dokument načtený pomocí hodnoty, která se `@id` nachází na stránce katalogu. Adresa URL listu katalogu není zamýšlena jako předvídatelná a měla by být zjištěna pouze pomocí stránky katalogu.

Dokument listu katalogu je objekt JSON s následujícími vlastnostmi:

Název                    | Typ                       | Vyžadováno | Poznámky
----------------------- | -------------------------- | -------- | -----
@type                   | řetězec nebo pole řetězců | ano      | Typ (y) položky katalogu
Katalog: commitId        | řetězec                     | ano      | ID potvrzení přidružené k této položce katalogu
Katalog: commitTimeStamp | řetězec                     | ano      | Časové razítko potvrzení této položky katalogu
id                      | řetězec                     | ano      | ID balíčku položky katalogu
zveřejněna               | řetězec                     | ano      | Datum publikování položky katalogu balíčku
verze                 | řetězec                     | ano      | Verze balíčku položky katalogu

### <a name="item-types"></a>Typy položek

`@type`Vlastnost je řetězec nebo pole řetězců. Pro usnadnění, pokud `@type` je hodnota řetězec, by měla být zpracována jako libovolná pole s velikostí jedna. Ne všechny možné hodnoty pro `@type` jsou zdokumentovány. Každá položka katalogu však obsahuje přesně jednu z následujících dvou hodnot řetězcového typu:

1. `PackageDetails`: představuje snímek metadat balíčku.
1. `PackageDelete`: představuje balíček, který se odstranil.

### <a name="package-details-catalog-items"></a>Podrobnosti balíčku – položky katalogu

Položky katalogu s typem `PackageDetails` obsahují snímek metadat balíčku pro konkrétní balíček (kombinaci ID a verze). Položka katalogu podrobností balíčku se vytvoří, když zdroj balíčku nalezne některý z následujících scénářů:

1. Balíček je **vložen**.
1. **Zobrazí se balíček.**
1. Balíček není v **seznamu**.
1. Dojde k **přetečení** balíčku.

Přetékání balíčku je gesto správce, které v podstatě generuje falešné vložení stávajícího balíčku bez jakýchkoli změn samotného balíčku. V nuget.org se po opravě chyby v jedné z úloh na pozadí, které využívají katalog, používá přesměrování.

Klienti, kteří mají položky katalogu, by se neměli pokoušet určit, který z těchto scénářů vytvořil položku katalogu. Místo toho by klient měl jednoduše aktualizovat jakékoli udržované zobrazení nebo index s metadaty obsaženými v položce katalogu. Kromě toho by se měly duplicitní a redundantní položky katalogu zpracovat řádným (idempotently).

Položky katalogu podrobností katalogu obsahují kromě těch, které jsou [zahrnuté ve všech pochodech katalogu](#catalog-leaf), následující vlastnosti.

Název                    | Typ                       | Vyžadováno | Poznámky
----------------------- | -------------------------- | -------- | -----
Autoři                 | řetězec                     | ne       |
vytvářejí                 | řetězec                     | ne       | Časové razítko při prvním vytvoření balíčku. Záložní vlastnost: `published` .
dependencyGroups        | pole objektů           | ne       | Závislosti balíčku seskupené podle cílového rozhraní ([stejný formát jako prostředek metadat balíčku](registration-base-url-resource.md#package-dependency-group))
vyřazení             | object                     | ne       | Vyřazení přidružení k balíčku ([stejný formát jako prostředek metadat balíčku](registration-base-url-resource.md#package-deprecation))
description             | řetězec                     | ne       |
iconUrl                 | řetězec                     | ne       |
isPrerelease            | boolean                    | ne       | Bez ohledu na to, jestli je verze balíčku předběžná. Lze zjistit z `version` .
language                | řetězec                     | ne       |
licenseUrl              | řetězec                     | ne       |
uvedené v seznamu                  | boolean                    | ne       | Bez ohledu na to, jestli je tento balíček uvedený
minClientVersion        | řetězec                     | ne       |
packageHash             | řetězec                     | ano      | Hodnota hash balíčku, kódování pomocí [standardu base 64](https://tools.ietf.org/html/rfc4648#section-4)
packageHashAlgorithm    | řetězec                     | ano      |
packageSize             | integer                    | ano      | Velikost balíčku. nupkg v bajtech
packageTypes            | pole objektů           | ne       | Typy balíčků určené autorem.
projectUrl              | řetězec                     | ne       |
releaseNotes            | řetězec                     | ne       |
requireLicenseAgreement | boolean                    | ne       | Předpokládat, `false` Pokud vyloučeno
shrnutí                 | řetězec                     | ne       |
tags                    | pole řetězců           | ne       |
title                   | řetězec                     | ne       |
verbatimVersion         | řetězec                     | ne       | Řetězec verze, který je původně nalezen v. nuspec

Vlastnost Package `version` je úplný řetězec verze po normalizaci. To znamená, že sem můžete zahrnout data sestavení SemVer 2.0.0.

`created`Časové razítko je při prvním přijetí balíčku zdrojem balíčku, což je obvykle krátká doba před potvrzením časového razítka položky katalogu.

`packageHashAlgorithm`Je řetězec definovaný implementací serveru představující algoritmus hash použitý k vytvoření `packageHash` . nuget.org vždycky používá `packageHashAlgorithm` hodnotu `SHA512` .

`packageTypes`Vlastnost bude přítomna pouze v případě, že autor zadal typ balíčku. Pokud je k dispozici, bude mít vždy alespoň jednu (1) položku. Každá položka v `packageTypes` poli je objekt JSON s následujícími vlastnostmi:

Název      | Typ    | Vyžadováno | Poznámky
--------- | ------- | -------- | -----
name      | řetězec  | ano      | Název typu balíčku.
verze    | řetězec  | ne       | Verze typu balíčku. K dispozici pouze v případě, že autor výslovně zadal verzi v nuspec.

`published`Časové razítko je čas posledního uvedení balíčku.

> [!Note]
> V nuget.org `published` je hodnota nastavena na rok 1900, pokud je balíček neuvedený.

#### <a name="sample-request"></a>Ukázková žádost

```
GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json
```

#### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [catalog-package-details.json](./_data/catalog-package-details.json)]

### <a name="package-delete-catalog-items"></a>Zabalení odstranění položek katalogu

Položky katalogu s typem `PackageDelete` obsahují minimální sadu informací, které označují, že klienti odstranili balíček ze zdroje balíčku a že už není dostupný pro žádnou operaci balíčku (například obnovení).

> [!NOTE]
> Balíček je možné odstranit a později znovu publikovat pomocí stejného ID a verze balíčku. V nuget.org se jedná o velmi vzácná velká písmena, protože by to znamenalo, že oficiální předpoklad klienta předpokládá, že ID a verze balíčku implikují určitý obsah balíčku. Další informace o odstraňování balíčků v nuget.org najdete v [naší zásadě](../nuget-org/policies/deleting-packages.md).

Neexistují žádné další vlastnosti kromě těch, které jsou [zahrnuté ve všech pochodech v katalogu](#catalog-leaf), a odstranit tak položky katalogu.

`version`Vlastnost je původní řetězec verze, který najdete v balíčku. nuspec.

`published`Vlastnost je čas, kdy byl balíček odstraněn, což je obvykle krátký čas před potvrzením časového razítka položky katalogu.

#### <a name="sample-request"></a>Ukázková žádost

```
GET https://api.nuget.org/v3/catalog0/data/2017.11.02.00.40.00/netstandard1.4_lib.1.0.0-test.json
```

#### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [catalog-package-delete.json](./_data/catalog-package-delete.json)]

## <a name="cursor"></a>Kurzor

### <a name="overview"></a>Přehled

Tato část popisuje koncept klienta, který není nutně nezbytný protokolem, by měl být součástí jakékoli praktické implementace klienta katalogu.

Vzhledem k tomu, že je katalog datovou strukturou, která je jenom pro připojení indexovanou časem, by měl klient uložit **kurzor** místně, který představuje bod v čase, který klient zpracoval položky katalogu. Všimněte si, že tato hodnota kurzoru by nikdy neměla být vygenerovaná pomocí hodin počítače klienta. Místo toho by měla hodnota pocházet z hodnoty objektu katalogu `commitTimestamp` .

Pokaždé, když chce klient zpracovat nové události ve zdroji balíčku, bude potřebovat pouze dotaz katalogu pro všechny položky katalogu s časovým razítkem potvrzení větším, než je uložený kurzor. Jakmile klient úspěšně zpracuje všechny nové položky katalogu, zaznamená nejnovější časové razítko potvrzení položek katalogu, které se právě zpracovaly jako nová hodnota kurzoru.

Pomocí tohoto přístupu může klient mít jistotu, že nikdy nechybíš žádné události balíčku, ke kterým došlo ve zdroji balíčku.
Kromě toho klient nikdy nemusí znovu zpracovávat staré události před zaznamenaným časovým razítkem potvrzení kurzoru.

Tento výkonný koncept ukazatelů se používá pro spoustu úloh na pozadí nuget.org a používá se k udržení aktuálního stavu rozhraní API v3. 

### <a name="initial-value"></a>Počáteční hodnota

Když se klient katalogu spouští poprvé (a proto nemá žádnou hodnotu kurzoru), měl by použít výchozí hodnotu kurzoru. NETTO `System.DateTimeOffset.MinValue` nebo nějaký podobný pojem minimálního reprezentovatelné časové razítko.

### <a name="iterating-over-catalog-items"></a>Iterace položek katalogu

Chcete-li se dotázat na další sadu položek katalogu ke zpracování, klient by měl:

1. Načte hodnotu zaznamenaného kurzoru z místního úložiště.
1. Stáhněte a deserializovat index katalogu.
1. Vyhledá všechny stránky katalogu s časovým razítkem potvrzení *větším než* kurzor.
1. Deklarujte prázdný seznam položek katalogu, které se mají zpracovat.
1. Pro každou stránku katalogu, která se shoduje v kroku 3:
   1. Stáhněte a deserializovat stránku katalogu.
   1. Najde všechny položky katalogu s časovým razítkem potvrzení *větším, než* je kurzor.
   1. Do seznamu deklarovaného v kroku 4 přidejte všechny položky odpovídajícího katalogu.
1. Seřaďte seznam položek katalogu podle časového razítka potvrzení.
1. Zpracovat každou položku katalogu v sekvenci:
   1. Stáhněte a deserializovat položku katalogu.
   1. Vhodně reagují na typ položky katalogu.
   1. Zpracování dokumentu položky katalogu v rámci konkrétního klienta.
1. Zaznamenejte poslední časové razítko potvrzení položky katalogu jako novou hodnotu kurzoru.

U tohoto základního algoritmu může implementace klienta sestavit kompletní zobrazení všech balíčků dostupných ve zdroji balíčku. Klient potřebuje spustit tento algoritmus jenom pravidelně, aby vždycky věděli o nejnovějších změnách ve zdroji balíčku.

> [!Note]
> Toto je algoritmus, který nuget.org používá k uchování [metadat balíčku](registration-base-url-resource.md), [obsahu balíčku](package-base-address-resource.md), [hledání](search-query-service-resource.md) a [dokončování](search-autocomplete-service-resource.md) prostředků v aktuálním stavu.

### <a name="dependent-cursors"></a>Závislé kurzory

Předpokládejme, že existují dva klienty katalogu, kteří mají základní závislost v případě, že výstup jednoho klienta závisí na výstupu jiného klienta. 

#### <a name="example"></a>Příklad

Například v nuget.org se v prostředku vyhledávání nesmí zobrazit nově publikovaný balíček, než se objeví v prostředku metadata balíčku. Důvodem je, že operace obnovení prováděná oficiálním klientem NuGet používá prostředek metadat balíčku. Pokud zákazník zjistí balíček pomocí vyhledávací služby, musí být schopný úspěšně obnovit tento balíček pomocí prostředku metadat balíčku. Jinými slovy, prostředek vyhledávání závisí na prostředku metadat balíčku. Každý prostředek má úlohu na pozadí klienta katalogu, která tento prostředek aktualizuje. Každý klient má svůj vlastní kurzor.

Vzhledem k tomu, že oba prostředky jsou vytvořeny z katalogu, kurzor klienta katalogu, který aktualizuje prostředek vyhledávání, *nesmí jít nad* kurzorem klienta katalogu metadat balíčku.

#### <a name="algorithm"></a>Algoritmus

Pokud chcete toto omezení implementovat, stačí upravit výše uvedený algoritmus:

1. Načte hodnotu zaznamenaného kurzoru z místního úložiště.
1. Stáhněte a deserializovat index katalogu.
1. Vyhledá všechny stránky katalogu s časovým razítkem potvrzení *větším, než* je ukazatel, který je **menší nebo roven kurzoru závislosti.**
1. Deklarujte prázdný seznam položek katalogu, které se mají zpracovat.
1. Pro každou stránku katalogu, která se shoduje v kroku 3:
   1. Stáhněte a deserializovat stránku katalogu.
   1. Najde všechny položky katalogu s časovým razítkem potvrzení *větším než* ukazatel, který je **menší nebo roven ukazateli na závislost.**
   1. Do seznamu deklarovaného v kroku 4 přidejte všechny položky odpovídajícího katalogu.
1. Seřaďte seznam položek katalogu podle časového razítka potvrzení.
1. Zpracovat každou položku katalogu v sekvenci:
   1. Stáhněte a deserializovat položku katalogu.
   1. Vhodně reagují na typ položky katalogu.
   1. Zpracování dokumentu položky katalogu v rámci konkrétního klienta.
1. Zaznamenejte poslední časové razítko potvrzení položky katalogu jako novou hodnotu kurzoru.

Pomocí tohoto upraveného algoritmu můžete vytvořit systém závislých klientů katalogu, kteří budou vytvářet své vlastní konkrétní indexy, artefakty atd.
