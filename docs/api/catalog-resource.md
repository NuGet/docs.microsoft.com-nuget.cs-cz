---
title: Prostředek katalogu, rozhraní API NuGet V3
description: Katalog je index všechny balíčky, které se vytvoří a odstraní na nuget.org.
author: joelverhagen
ms.author: jver
ms.date: 10/30/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 4884de71151ee1ae3c0a78b803c9222f9c1d86ec
ms.sourcegitcommit: ef08f376688f0191a8d3d873b6a4386afd799373
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/28/2019
ms.locfileid: "66266360"
---
# <a name="catalog"></a>Katalog

**Katalogu** je prostředek, který zaznamenává všechny operace balíčků ve zdroji balíčku, jako je například vytvoření a odstranění. Prostředek katalogu má `Catalog` zadejte [index služby](service-index.md). Můžete použít tento prostředek k [dotazů pro všechny publikované balíčky](../guides/api/query-for-all-published-packages.md).

> [!Note]
> Vzhledem k tomu, že katalog není používán oficiální klienta NuGet, ne všechny zdroje balíčků implementovat v katalogu.

> [!Note]
> Katalog nuget.org v současné době není k dispozici v Číně. Další podrobnosti najdete v tématu [NuGet/NuGetGallery #4949](https://github.com/NuGet/NuGetGallery/issues/4949).

## <a name="versioning"></a>Správa verzí

Následující `@type` hodnota se používá:

@type Hodnota   | Poznámky
------------- | -----
CATALOG/3.0.0 | Počáteční verze

## <a name="base-url"></a>Základní adresa URL

Adresa URL vstupního bodu pro následující rozhraní API je hodnota `@id` vlastnost přidružená k výše uvedených prostředků `@type` hodnoty. Toto téma používá zástupné adresy URL `{@id}`.

## <a name="http-methods"></a>Metody HTTP

Všechny adresy URL, které jsou součástí podporu katalogu prostředků pouze metody HTTP `GET` a `HEAD`.

## <a name="catalog-index"></a>Index katalogu

Index katalogu je dokument v dobře známé umístění, které obsahuje seznam položek katalogu, seřazené chronologicky. Je vstupním bodem prostředek katalogu.

Index se skládá z stránky katalogu. Každá stránka katalogu obsahuje položky katalogu. Každá položka katalogu představuje události týkající se jeden balíček v bodě v čase. Položka katalogu mohou představovat balíček, který byl vytvořen, neuvedené v seznamu, relisted nebo odstraněné ze zdroje balíčku. Zpracováním položek katalogu v chronologickém pořadí, můžete sestavit klienta aktuální přehled o všech balíčků, který existuje ve zdroji balíčku V3.

Stručně řečeno objekty BLOB katalogu mají následující hierarchickou strukturu:

- **Index**: vstupní bod pro katalog.
- **Stránka**: seskupení položek katalogu.
- **Listu**: dokument představující položka katalogu, což je snímek stavu jednoho balíčku.

Každý objekt katalogu má vlastnost s názvem `commitTimeStamp` udávající, kdy byla položka přidána do katalogu. Položky katalogu budou přidány na stránku katalogu v dávkách nazývá potvrzení. Všechny položky katalogu v rámci stejného potvrzení mají stejné časové razítko potvrzení (`commitTimeStamp`) a ID potvrzení změn (`commitId`). Položky katalogu, které jsou umístěny v rámci stejného potvrzení představují události, k nimž došlo přibližně stejný bod v čase ve zdroji balíčku. Neexistuje žádné řazení v rámci katalogu potvrzení.

Protože každý ID balíčku a verzi je jedinečný, nikdy nebude více než jedna položka katalogu v potvrzení. Tím se zajistí, že položky katalogu pro jeden balíček může vždy být jednoznačně uspořádány ve vztahu časové razítko potvrzení.

Existuje více potvrzení do katalogu za za žádných `commitTimeStamp`. Jinými slovy `commitId` je redundantní. s `commitTimeStamp`.

Rozdíl od [balíček metadata resource](registration-base-url-resource.md), což je indexované podle ID balíčku, katalog je indexované (a dotazovatelného) pouze podle času.

Položky katalogu jsou vždy přidány do katalogu v monotónně se zvyšující chronologickém pořadí. To znamená, že pokud potvrzení katalogu se přidá v okamžiku X potom bez potvrzení katalogu nebude nikdy přidán s časem nižším než nebo rovna X.

Následující požadavek načte index katalogu.

    GET {@id}

Index katalogu je dokument JSON, který obsahuje objekt s následujícími vlastnostmi:

Name            | Type             | Požadováno | Poznámky
--------------- | ---------------- | -------- | -----
commitId        | odkazy řetězců           | ano      | Jedinečné ID přidružené k nejnovějším potvrzení
commitTimeStamp | odkazy řetězců           | ano      | Časové razítko poslední potvrzení změn
count           | integer          | ano      | Počet stránek v indexu
items           | Pole objektů | ano      | Pole objektů, každý objekt představující stránku

Každý prvek `items` pole je objekt s minimální podrobnosti o jednotlivých stránkách. Tyto objekty stránky neobsahují ponechá katalogu (položky). Pořadí prvků v tomto poli není definován. Stránky lze provést řazení podle klienta v paměti pomocí jejich `commitTimeStamp` vlastnost.

Jak jsou zavedeny nové stránky, `count` se zvýší a zobrazí se v nové objekty `items` pole.

Přidávání položek do katalogu, index `commitId` se změní a `commitTimeStamp` zvýší. Tyto dvě vlastnosti jsou v podstatě souhrn přes všechny stránky `commitId` a `commitTimeStamp` hodnoty v `items` pole.

### <a name="catalog-page-object-in-the-index"></a>Objekt katalogu stránku v indexu

Objekty stránky katalogu nalezena v katalogu indexu `items` vlastnosti mají následující vlastnosti:

Name            | Type    | Požadováno | Poznámky
--------------- | ------- | -------- | -----
@id             | odkazy řetězců  | ano      | Adresa URL stránky načtení katalogu
commitId        | odkazy řetězců  | ano      | Jedinečné ID přidružené k nejnovějším potvrzení na této stránce
commitTimeStamp | odkazy řetězců  | ano      | Časové razítko poslední potvrzení změn na této stránce
count           | integer | ano      | Počet položek na stránce katalog

Rozdíl od [balíček metadata resource](registration-base-url-resource.md) což v některých případech inlines opustí do indexu, nechá katalogu nikdy jsou vloženy do indexu a musí být vždy získána pomocí stránky `@id` adresy URL.

### <a name="sample-request"></a>Ukázková žádost

    GET https://api.nuget.org/v3/catalog0/index.json

### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [catalog-index.json](./_data/catalog-index.json)]

## <a name="catalog-page"></a>Katalog stránky

Na stránce katalogu je kolekce položek katalogu. Je načíst pomocí jedné z dokumentu `@id` nalezeny hodnoty v katalogu indexu. Adresa URL stránky katalogu tudíž předvídatelný a by měly být zjištěny pomocí pouze index katalogu.

Přidání nových položek katalogu se na stránku v katalogu index pouze s nejvyšší časové razítko potvrzení nebo na novou stránku. Po přidání na stránku s vyšší časové razítko potvrzení do katalogu starší stránky nikdy k přidání nebo změně.

Katalog stránky dokumentu je objekt JSON s následujícími vlastnostmi:

Name            | Type             | Požadováno | Poznámky
--------------- | ---------------- | -------- | -----
commitId        | odkazy řetězců           | ano      | Jedinečné ID přidružené k nejnovějším potvrzení na této stránce
commitTimeStamp | odkazy řetězců           | ano      | Časové razítko poslední potvrzení změn na této stránce
count           | integer          | ano      | Počet položek na stránce
items           | Pole objektů | ano      | Položky katalogu na této stránce
Nadřazené          | odkazy řetězců           | ano      | Adresa URL indexu katalogu

Každý prvek `items` pole je objekt s minimální podrobnosti o položky katalogu. Tyto objekty položky neobsahují všechna data položky katalogu. Pořadí položek na stránce `items` pole není definován. Položky lze provést řazení podle klienta v paměti pomocí jejich `commitTimeStamp` vlastnost.

Počet položek katalogu na stránce je definován implementací serveru. Pro nuget.org je maximálně 550 položek na každé stránce, ale skutečný počet může být menší pro některé stránky v závislosti na velikosti další dávku potvrzení v bodě v čase.

Zavedeném nových položek `count` je objektům katalogu přičítání a nové položky se zobrazí v `items` pole.

Při přidání položky na stránku `commitId` změny a `commitTimeStamp` zvyšuje. Tyto dvě vlastnosti jsou v podstatě přehled napříč všemi `commitId` a `commitTimeStamp` hodnoty v `items` pole.

### <a name="catalog-item-object-in-a-page"></a>Objekt položky na stránce katalogu

Najít objekty položky katalogu na stránce katalog `items` vlastnosti mají následující vlastnosti:

Name            | Type    | Požadováno | Poznámky
--------------- | ------- | -------- | -----
@id             | odkazy řetězců  | ano      | Adresa URL pro načtení položky katalogu
@type           | odkazy řetězců  | ano      | Typ položky katalogu
commitId        | odkazy řetězců  | ano      | ID potvrzení změn, které jsou přidružené k této položky katalogu
commitTimeStamp | odkazy řetězců  | ano      | Časové razítko potvrzení této položky katalogu
nuget:ID        | odkazy řetězců  | ano      | ID balíčku, týkající se tohoto listu
nuget:Version   | odkazy řetězců  | ano      | Verze balíčku, týkající se tohoto listu

`@type` Hodnota bude jeden z následujících dvou hodnot:

1. `nuget:PackageDetails`: to odpovídá `PackageDetails` typu v dokumentu katalogu typu list.
1. `nuget:PackageDelete`: to odpovídá `PackageDelete` typu v dokumentu katalogu typu list.

Další informace o tom, co každý typ znamená, najdete v článku [odpovídající položky typu](#item-types) níže.

### <a name="sample-request"></a>Ukázková žádost

    GET https://api.nuget.org/v3/catalog0/page2926.json

### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [catalog-page.json](./_data/catalog-page.json)]

## <a name="catalog-leaf"></a>Katalog listu

Katalog typu list obsahuje metadata o konkrétní ID a verzi v určitém okamžiku v čase. Je načtena pomocí dokumentu `@id` hodnota nalezena v katalogu stránky. Adresa URL na list katalogu považovat předvídatelný a by měly být zjištěny pomocí pouze stránky katalogu.

Dokument listu katalogu je objekt JSON s následujícími vlastnostmi:

Name                    | Type                       | Požadováno | Poznámky
----------------------- | -------------------------- | -------- | -----
@type                   | řetězec nebo pole řetězců | ano      | Typy položek katalogu
catalog:commitId        | odkazy řetězců                     | ano      | ID potvrzení změn přidružené k této položky katalogu
catalog:commitTimeStamp | odkazy řetězců                     | ano      | Časové razítko potvrzení této položky katalogu
id                      | odkazy řetězců                     | ano      | ID balíčku položky katalogu
Publikování               | odkazy řetězců                     | ano      | Položka katalogu datum publikování balíčku
verze                 | odkazy řetězců                     | ano      | Verze balíčku položky katalogu

### <a name="item-types"></a>Typy položek

`@type` Vlastnosti je string nebo pole řetězců. Pro usnadnění práce Pokud `@type` hodnota je řetězec, mají být považována za jakékoli pole o velikosti jednoho. Ne všechny možné hodnoty pro `@type` jsou popsány. Každá položka katalogu má ale přesně jednu ze dvou následujících hodnot typu řetězec:

1. `PackageDetails`: představuje snímek metadata balíčků
1. `PackageDelete`: představuje balíček, který byl odstraněn

### <a name="package-details-catalog-items"></a>Podrobnosti balíčku položek katalogu

Položky s typem katalogu `PackageDetails` obsahují snímek metadat balíčku pro určitý balíček (kombinaci ID a verzi). Katalogové položky podrobnosti balíčku je vytvořen, pokud zdroj balíčku, zaznamená některý z následujících scénářů:

1. Balíček je **vloženo**.
1. Balíček je **uvedené**.
1. Balíček je **neuvedené**.
1. Balíček je **přeformátování**.

Přeformátování balíčku je pro správu gesta, která v podstatě generuje falešné oznámení o existující balíček bez jediné změny na samotném balíčku. Na nuget.org se používá přeformátování po opravě chyby v jednom z úlohy na pozadí, které využívají katalogu.

Klienti využívání položky katalogu by se neměly pokoušet zjistit, které z těchto scénářů vytvořené položky katalogu. Místo toho by měl jednoduše aktualizaci klienta udržována zobrazení ani index pomocí metadat obsažených v položky katalogu. Kromě toho by měla řádně zpracovat duplicitní nebo nadbytečné katalogových položek (idempotently).

Položky katalogu podrobnosti balíčku mají následující vlastnosti kromě těch [na všechny listy katalogu](#catalog-leaf).

Name                    | Type                       | Požadováno | Poznámky
----------------------- | -------------------------- | -------- | -----
Autoři                 | odkazy řetězců                     | Ne       |
Vytvoření                 | odkazy řetězců                     | Ne       | Časové razítko z při prvním vytvoření balíčku. Základní vlastnosti: `published`.
dependencyGroups        | Pole objektů           | Ne       | Stejný formát jako [balíček metadata resource](registration-base-url-resource.md#package-dependency-group)
description             | odkazy řetězců                     | Ne       |
iconUrl                 | odkazy řetězců                     | Ne       |
isPrerelease            | Logická hodnota                    | Ne       | Určuje, jestli je předběžná verze balíčku. Můžete zjistit z `version`.
jazyk                | odkazy řetězců                     | Ne       |
licenseUrl              | odkazy řetězců                     | Ne       |
uvedené v seznamu                  | Logická hodnota                    | Ne       | Určuje, jestli je balíček uvedený
minClientVersion        | odkazy řetězců                     | Ne       |
packageHash             | odkazy řetězců                     | ano      | Hodnota hash balíčku kódování pomocí [standardní base-64](https://tools.ietf.org/html/rfc4648#section-4)
packageHashAlgorithm    | odkazy řetězců                     | ano      |
packageSize             | integer                    | ano      | Velikost balíčku .nupkg v bajtech
projectUrl              | odkazy řetězců                     | Ne       |
ReleaseNotes            | odkazy řetězců                     | Ne       |
requireLicenseAgreement | Logická hodnota                    | Ne       | Předpokládejme `false` -li vyloučit
souhrn                 | odkazy řetězců                     | Ne       |
značky                    | pole řetězců           | Ne       |
název                   | odkazy řetězců                     | Ne       |
verbatimVersion         | odkazy řetězců                     | Ne       | Řetězec verze, protože původně součástí souboru .nuspec

Balíček `version` vlastnost po normalizace řetězce plnou verzi. To znamená, že data SemVer 2.0.0 sestavení může být součástí tady.

`created` Časové razítko je při podle zdroje balíčku, který je obvykle krátkou dobu před časové razítko potvrzení položka katalogu byla prvním přijetí balíček.

`packageHashAlgorithm` Je definován implementací serveru představující hashovací algoritmus používaný k vytvoření řetězce `packageHash`. vždy používá nuget.org `packageHashAlgorithm` hodnotu `SHA512`.

`published` Časové razítko je čas, kdy byl balíček poslední uveden.

> [!Note]
> Na nuget.org `published` hodnotu roku 1900, pokud je balíček neuvedené v seznamu.

#### <a name="sample-request"></a>Ukázková žádost

ZÍSKAT https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

#### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [catalog-package-details.json](./_data/catalog-package-details.json)]

### <a name="package-delete-catalog-items"></a>Položky katalogu odstranění balíčku

Položky s typem katalogu `PackageDelete` obsahují minimální sadu informaci o katalogu klientům, že balíček se odstranil z balíčku zdroje a není už k dispozici pro libovolnou operaci balíčku (například obnovení).

> [!Note]
> Je možné pro balíček, který chcete odstranit a později znovu publikovat pomocí stejné ID balíčku a verzi. Na nuget.org to je velmi vzácný případ, protože to naruší oficiální klienta z předpokladu, že ID balíčku a verzi implikují určitý balíček obsahu. Další informace o odstranění balíčků na nuget.org, naleznete v tématu [naše zásady](../policies/deleting-packages.md).

Položky katalogu odstranit balíček mají žádné další vlastnosti, kromě těch [na všechny listy katalogu](#catalog-leaf).

`version` Vlastnost je původní řetězec verze v souboru .nuspec balíčku.

`published` Čas při balíčku byl odstraněn, což je obvykle jako krátkou dobu před časové razítko potvrzení položka katalogu je vlastnost.

#### <a name="sample-request"></a>Ukázková žádost

ZÍSKAT https://api.nuget.org/v3/catalog0/data/2017.11.02.00.40.00/netstandard1.4_lib.1.0.0-test.json

#### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [catalog-package-delete.json](./_data/catalog-package-delete.json)]

## <a name="cursor"></a>Kurzor

### <a name="overview"></a>Přehled

Tato část popisuje koncept klienta, který, i když není nutně zákonného protokol, musí být součástí žádné implementace klienta praktické katalogu.

Protože katalogu je struktury nabízí jen možnost Připojovat data indexované podle času, klient by měla být uložena **kurzor** místně, až bodu v čase klienta zpracovala položky katalogu. Všimněte si, že tato hodnota kurzor by měl nebudou nikdy generována formátu, klientské počítače. Místo toho hodnotu musí pocházet z objektu katalogu `commitTimestamp` hodnotu.

Pokaždé, když klient požaduje zpracovávat nové události ve zdroji balíčku, nemusí pouze dotazu v katalogu pro všechny položky katalogu s časovým razítkem potvrzení větší než jeho uložené kurzoru. Jakmile klient úspěšně zpracuje všechny nové položky katalogu, zaznamenává nejnovější potvrzení změn časové razítko položky katalogu právě zpracovat jako novou hodnotu kurzoru.

Tento přístup může být klient nezapomeňte Nezmeškejte žádné balíček události, ke kterým došlo ve zdroji balíčku.
Kromě toho klient se nikdy má za účelem opětovného zpracování staré události před časové razítko zaznamenané potvrzení kurzoru.

Tento výkonný koncept kurzory se používá pro řadu úloh na pozadí nuget.org a slouží k udržování stavu samotné rozhraní API V3. 

### <a name="initial-value"></a>Počáteční hodnota

Když klient katalogu je pro úplně první čas spuštění (a tedy nemá žádnou hodnotu kurzoru), měla by použít výchozí hodnotu kurzoru. NET společnosti `System.DateTimeOffset.MinValue` nebo určitou takové obdobná představu o minimální reprezentovatelné časové razítko.

### <a name="iterating-over-catalog-items"></a>Iterování položek katalogu

Pro dotazy, další sadu položek katalogu pro zpracování, by měl klient:

1. Načtěte hodnotu zaznamenané kurzor z místního úložiště.
1. Stáhněte si a deserializovat index katalogu.
1. Najít všechny stránky s časovým razítkem potvrzení katalogu *větší než* kurzor.
1. Deklarujte prázdný seznam položek katalogu pro zpracování.
1. Pro každou stránku katalogu se shodou v kroku 3:
   1. Stáhněte si a deserializovat stránky katalogu.
   1. Najít všechny položky s časovým razítkem potvrzení katalogu *větší než* kurzor.
   1. Všechny odpovídající položky katalogu přidáte do seznamu deklarované v kroku 4.
1. Seřaďte seznam položek katalogu podle časové razítko potvrzení.
1. Zpracování každé položky katalogu v pořadí:
   1. Stáhněte si a deserializovat položky katalogu.
   1. Typ položky katalogu reagují odpovídajícím způsobem.
   1. Proces dokumentu položky katalogu v podobě specifické pro klienta.
1. Zaznamenejte časové razítko poslední položka katalogu potvrzení jako novou hodnotu kurzoru.

Pomocí tohoto algoritmu základní implementace klienta lze sestavit úplný přehled všech balíčků dostupných ve zdroji balíčku. Klient potřebují pouze spustit tento algoritmus se vždy přehled o nejnovějších změn ke zdroji balíčku.

> [!Note]
> To je algoritmus používá tento nuget.org zachovat [Metadata balíčků](registration-base-url-resource.md), [obsah balíčku](package-base-address-resource.md), [hledání](search-query-service-resource.md) a [automatické dokončování](search-autocomplete-service-resource.md) Aktuální prostředky.

### <a name="dependent-cursors"></a>Závislé kurzory

Předpokládejme, že existují dva klienti katalogu, které mají vlastní závislost, pokud jeden klient výstup závisí na výstupu jiného klienta. 

#### <a name="example"></a>Příklad

Například na nuget.org přehled nově publikovaných balíček by se neměl zobrazit v hledání prostředků předtím, než se zobrazí v resource metadata balíčku. Toto je vzhledem k tomu používá resource metadata balíčku "obnovit" operace prováděné oficiální pro klienta NuGet. Pokud zákazník zjistí balíček se službou search, měly by být možné úspěšně obnovit tento balíček pomocí resource metadata balíčku. Jinými slovy hledání prostředků závisí na resource metadata balíčku. Každý prostředek má katalog klienta úloha na pozadí aktualizuje tento prostředek. Každý klient má své vlastní kurzoru.

Vzhledem k tomu, že oba prostředky jsou sestaveny z katalogu kurzor katalogu klienta, která aktualizuje prostředek hledání *nesmí jít nad rámec* kurzor klienta katalog metadat balíčku.

#### <a name="algorithm"></a>algoritmus

K implementaci tohoto omezení, stačí upravte výše, aby se algoritmus:

1. Načtěte hodnotu zaznamenané kurzor z místního úložiště.
1. Stáhněte si a deserializovat index katalogu.
1. Najít všechny stránky s časovým razítkem potvrzení katalogu *větší než* kurzor **menší nebo rovna kurzor na závislost.**
1. Deklarujte prázdný seznam položek katalogu pro zpracování.
1. Pro každou stránku katalogu se shodou v kroku 3:
   1. Stáhněte si a deserializovat stránky katalogu.
   1. Najít všechny položky s časovým razítkem potvrzení katalogu *větší než* kurzor **menší nebo rovna kurzor na závislost.**
   1. Všechny odpovídající položky katalogu přidáte do seznamu deklarované v kroku 4.
1. Seřaďte seznam položek katalogu podle časové razítko potvrzení.
1. Zpracování každé položky katalogu v pořadí:
   1. Stáhněte si a deserializovat položky katalogu.
   1. Typ položky katalogu reagují odpovídajícím způsobem.
   1. Proces dokumentu položky katalogu v podobě specifické pro klienta.
1. Zaznamenejte časové razítko poslední položka katalogu potvrzení jako novou hodnotu kurzoru.

Pomocí tohoto algoritmu upravené, můžete vytvořit systém katalogu závislé klienty vytváří všechny své vlastní specifickými indexy, artefakty, atd.
