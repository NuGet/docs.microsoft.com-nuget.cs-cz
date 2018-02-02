---
title: "Katalog, rozhraní API NuGet V3 | Microsoft Docs"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/30/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Katalog je index všech balíčků, vytvoření a na nuget.org odstraněn."
keywords: "Rozhraní API V3 NuGet katalogu, nuget.org transakčního protokolu, replikaci NuGet.org, klonování NuGet.org připojovacího záznam NuGet.org"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: d1a24be68a60085a40361c374ffb34dc221f09c4
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
---
# <a name="catalog"></a>Catalog

**Katalogu** je na prostředek, který zaznamenává všechny operace balíček ve zdroji balíčku, například vytváření a odstranění. Katalog prostředků má `Catalog` zadejte [indexu služby](service-index.md).

> [!Note]
> Protože katalogu není používán oficiální klienta NuGet, ne všechny zdroje balíčků implementovat katalogu.

> [!Note]
> V současné době není k dispozici v Číně nuget.org katalogu. Další podrobnosti najdete v tématu [NuGet/NuGetGallery #4949](https://github.com/NuGet/NuGetGallery/issues/4949).

## <a name="versioning"></a>Správa verzí

Následující `@type` hodnota se používá:

@typeHodnota   | Poznámky
------------- | -----
CATALOG/3.0.0 | Původní verze

## <a name="base-url"></a>Základní adresu URL

Adresa URL vstupní bod pro následující rozhraní API je hodnota `@id` vlastnost spojená s zmíněnými prostředků `@type` hodnoty. Toto téma používá adresu URL zástupný symbol `{@id}`.

## <a name="http-methods"></a>Metody HTTP

Všechny adresy URL v podpoře prostředků katalogu nalezen jenom metody HTTP `GET` a `HEAD`.

## <a name="catalog-index"></a>Index katalogu

Index katalogu je dokument v dobře známé umístění, které obsahuje seznam položek katalogu, uspořádány cronologically. Je vstupní bod katalogu prostředku.

Index se skládá z katalogu stránky. Každé stránce katalogu obsahuje položky katalogu. Každá položka katalogu představuje události týkající se jeden balíček v určitém bodě v čase. Položka katalogu, kterou může představovat balíček, který byl vytvořen, neuvedené, relisted nebo odstraněn ze zdroje balíčků. Zpracováním položek katalogu v chronologickém pořadí, můžete vytvořit klienta aktuální přehled o každý balíček, který existuje ve zdroji balíčku V3.

Stručně řečeno objekty BLOB katalogu mají následující hierarchickou strukturu:

- **Index**: vstupní bod pro katalog.
- **Stránka**: seskupení položek katalogu.
- **Listu**: dokument představující položka katalogu, což je snímek stavu jeden balíček.

Každý objekt katalogu má vlastnost s názvem `commitTimeStamp` udávající, kdy byla položka přidána do katalogu. Položky katalogu budou přidány do katalogu stránky v dávkách názvem potvrzení. Všechny položky katalogu ve stejné potvrzení mají stejné časové razítko potvrzení (`commitTimeStamp`) a ID potvrzení (`commitId`). Položky katalogu, které jsou umístěny ve stejné potvrzení představují události, ke kterým došlo okolo stejného bodu v čase ve zdroji balíčku. Není žádný řazení v rámci katalogu potvrzení.

Protože každý ID a verzi balíčku je jedinečný, nikdy bude více než jedna položka katalogu v potvrzení. Tím se zajistí, že položky katalogu pro jeden balíček může vždy jednoznačně seřadit s ohledem na časové razítko potvrzení.

Je nikdy nemůže mít více než jeden potvrzení do katalogu za `commitTimeStamp`. Jinými slovy `commitId` je redundantní s `commitTimeStamp`.

Rozdíl k [balíček prostředek metadat](registration-base-url-resource.md), který je indexovaný podle ID balíčku, katalogu je indexované (a dotazovatelné) pouze podle času.

Položky katalogu jsou vždy přidaných do katalogu v monotónně se zvyšující, chronologickém pořadí. To znamená, že pokud potvrzení katalogu je přidaný v době X pak žádné potvrzení katalogu nebude nikdy přidán s časem menší než nebo rovna X.

Následující požadavek načte index katalogu.

    GET {@id}

Index katalogu je dokument JSON, který obsahuje objekt s následujícími vlastnostmi:

Název            | Typ             | Požadováno | Poznámky
--------------- | ---------------- | -------- | -----
commitId        | odkazy řetězců           | Ano      | Jedinečné ID přidružené k nejnovější potvrzení
commitTimeStamp | odkazy řetězců           | Ano      | Časové razítko poslední zápisu
count           | integer          | Ano      | Počet stránek v indexu
Položky           | Pole objektů | Ano      | Pole objektů, každý objekt reprezentující stránky

Každý prvek v `items` pole je objekt s některé minimální podrobnosti o každé stránce. Tyto objekty stránky neobsahují nechá katalogu (položky). Pořadí prvků v toto pole není definováno. Stránky lze provést řazení podle klienta v paměti pomocí jejich `commitTimeStamp` vlastnost.

Zavedeném nové stránky `count` se zvýší a zobrazí se v nové objekty `items` pole.

Jako položky budou přidány do katalogu, index `commitId` změní a `commitTimeStamp` zvýší. Tyto dvě vlastnosti jsou v podstatě souhrn přes všechny stránky `commitId` a `commitTimeStamp` hodnoty ve `items` pole.

### <a name="catalog-page-object-in-the-index"></a>Katalog stránky objekt v indexu

Objekty, na stránce katalogu najít v katalogu indexu `items` vlastnost mít následující vlastnosti:

Název            | Typ    | Požadováno | Poznámky
--------------- | ------- | -------- | -----
@id             | odkazy řetězců  | Ano      | Adresu URL stránky načtení katalogu
commitId        | odkazy řetězců  | Ano      | Jedinečné ID přidružené k nejnovější potvrzení na této stránce
commitTimeStamp | odkazy řetězců  | Ano      | Časové razítko poslední potvrzení na této stránce
count           | integer | Ano      | Počet položek na stránce katalogu

Rozdíl k [balíček prostředek metadat](registration-base-url-resource.md) což v některých případech inlines opustí do indexu, se nikdy vložená do indexu nechá katalogu a musí být vždy získána pomocí stránky `@id` adresy URL.

### <a name="sample-request"></a>Ukázková žádost

    GET https://api.nuget.org/v3/catalog0/index.json

### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [catalog-index.json](./_data/catalog-index.json)]

## <a name="catalog-page"></a>Stránka katalogu

Stránka katalogu je kolekce položek katalogu. Je to dokument načtených pomocí jedné z `@id` hodnoty najdete v indexu katalogu. Adresu URL stránky katalogu není určen jako předvídatelný a by měly být zjištěny pomocí pouze index katalogu.

Přidání nových položek katalogu na stránku v indexu katalogu pouze s nejvyšší časové razítko potvrzení nebo na novou stránku. Jakmile se zobrazí stránka s vyšší časové razítko potvrzení přidaných do katalogu, se nikdy starší stránky přidají do nebo změnit.

Dokument stránky katalogu je objekt JSON s následujícími vlastnostmi:

Název            | Typ             | Požadováno | Poznámky
--------------- | ---------------- | -------- | -----
commitId        | odkazy řetězců           | Ano      | Jedinečné ID přidružené k nejnovější potvrzení na této stránce
commitTimeStamp | odkazy řetězců           | Ano      | Časové razítko poslední potvrzení na této stránce
count           | integer          | Ano      | Počet položek na stránce
Položky           | Pole objektů | Ano      | Položky katalogu na této stránce
Nadřazené          | odkazy řetězců           | Ano      | Adresu URL katalogu indexu

Každý prvek v `items` pole je objekt s některé minimální podrobnosti o položka katalogu. Tyto položky objekty nebudou obsahovat všechna data položka katalogu. Pořadí položek na stránce `items` pole není definováno. Položky lze provést řazení podle klienta v paměti pomocí jejich `commitTimeStamp` vlastnost.

Počet položek katalogu na stránce je definován implementaci serveru. Pro nuget.org je maximálně 550 položek v každé stránce, ale skutečný počet může být menší pro některé dependong stránky na velikosti další dávku potvrzení v bodě v čase.

Zavedeném nové položky `count` je katalog zvýšena a nové položky objekty se zobrazí v `items` pole.

Při přidání položek na stránku, `commitId` změny a `commitTimeStamp` zvyšuje. Tyto dvě vlastnosti jsou v podstatě souhrn přes všechny `commitId` a `commitTimeStamp` hodnoty ve `items` pole.

### <a name="catalog-item-object-in-a-page"></a>Objekt položky na stránce v katalogu

Objekty, na položky katalogu najít na stránce katalogu `items` vlastnost mít následující vlastnosti:

Název            | Typ    | Požadováno | Poznámky
--------------- | ------- | -------- | -----
@id             | odkazy řetězců  | Ano      | Adresa URL načíst položka katalogu
@type           | odkazy řetězců  | Ano      | Typ položky katalogu
commitId        | odkazy řetězců  | Ano      | ID potvrzení spojené s touto položkou katalogu
commitTimeStamp | odkazy řetězců  | Ano      | Časové razítko potvrzení této položky katalogu
nuget:ID        | odkazy řetězců  | Ano      | Tato listu související s ID balíčku
nuget:Version   | odkazy řetězců  | Ano      | Verze balíčku, tento listu související s

`@type` Hodnota bude mít jednu z následujících dvou hodnot:

1. `nuget:PackageDetails`: to odpovídá `PackageDetails` typu v dokumentu listu katalogu.
1. `nuget:PackageDelete`: to odpovídá `PackageDelete` typu v dokumentu listu katalogu.

Další podrobnosti o jaké každý typ znamená, najdete v článku [odpovídající položky typu](#item-types) níže.

### <a name="sample-request"></a>Ukázková žádost

    GET https://api.nuget.org/v3/catalog0/page2926.json

### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [catalog-page.json](./_data/catalog-page.json)]

## <a name="catalog-leaf"></a>Katalog listu

Katalog listu obsahuje metadata o konkrétní ID a verzi balíčku v určitém okamžiku v čase. Je to dokument načtena pomocí `@id` nalezena hodnota na stránce katalogu. Adresu URL katalogu listu neměla být predictedable a by měly být zjištěny pomocí pouze na stránce katalogu.

Dokument listu katalogu je objekt JSON s následujícími vlastnostmi:

Název                    | Typ                       | Požadováno | Poznámky
----------------------- | -------------------------- | -------- | -----
@type                   | řetězec nebo pole řetězců. | Ano      | Typy položek katalogu
catalog:commitId        | odkazy řetězců                     | Ano      | Potvrzení ID spojené s této položky katalogu
catalog:commitTimeStamp | odkazy řetězců                     | Ano      | Časové razítko potvrzení této položky katalogu
id                      | odkazy řetězců                     | Ano      | ID balíčku položky katalogu
Publikovat               | odkazy řetězců                     | Ano      | Datum publikování balíčku položka katalogu
verze                 | odkazy řetězců                     | Ano      | Verze balíčku položky katalogu

### <a name="item-types"></a>Typy položek

`@type` Vlastnost je řetězec nebo pole řetězců. Pro usnadnění práce Pokud `@type` hodnota je řetězec, by měl být považovány za žádné pole s velikostí, jeden. Ne všechny možné hodnoty pro `@type` popsané. Každá položka katalogu má však přesně jednu ze dvou hodnot pro typ následující řetězec:

1. `PackageDetails`: představuje snímek metadata balíčků
1. `PackageDelete`: představuje balíček, který byl odstraněn

### <a name="package-details-catalog-items"></a>Položky katalogu podrobnosti balíčku

Položky s typem katalogu `PackageDetails` obsahovat snímek metadata balíčků pro konkrétní balíček (kombinaci ID a verzi). Položku katalogu podrobnosti balíčku se vytvářejí, když zdroj balíčku dojde kterýkoli z následujících scénářů:

1. Balíček je **nabídnutých**.
1. Balíček je **uvedené**.
1. Balíček je **neuvedené**.
1. Balíček je **přeformátování**.

Balíček přeformátování je správce gesta, která v podstatě generuje falešných push existujícího balíčku se žádné změny k balíčku sám sebe. V nuget.org se používá přeformátování po opravě chyby v jednom z pozadí úlohy, které využívají katalogu.

K určení, které z těchto scénářů vytváří položka katalogu, kterou neměli klienti využívání položky katalogu. Místo toho klienta by měl jednoduše aktualizovat všechny zachována zobrazení nebo index s metadat obsažených v položka katalogu. Kromě toho by měla řádně zpracovávat položky katalogu duplicitní nebo redundantní (idempotently).

Položky katalogu podrobnosti balíčku mít následující vlastnosti kromě těch, které [obsahovat všechny katalogu nechá](#catalog-leaf).

Název                    | Typ                       | Požadováno | Poznámky
----------------------- | -------------------------- | -------- | -----
Autoři                 | odkazy řetězců                     | Ne       |
Vytvořit                 | odkazy řetězců                     | Ano      | Při prvním vytvoření balíčku časové razítko
dependencyGroups        | Pole objektů           | Ne       | Stejný formát jako [balíček prostředek metadat](registration-base-url-resource.md#package-dependency-group)
description             | odkazy řetězců                     | Ne       |
IconUrl                 | odkazy řetězců                     | Ne       |
isPrerelease            | Logická hodnota                    | Ano      | Zda je předprodejní verze balíčku
jazyk                | odkazy řetězců                     | Ne       |
licenseUrl              | odkazy řetězců                     | Ne       |
uvedené v seznamu                  | Logická hodnota                    | Ne       | Zda je balíček uvedený
MinClientVersion        | odkazy řetězců                     | Ne       |
packageHash             | odkazy řetězců                     | Ano      | Hodnota hash balíčku, kódování pomocí [standardní base 64](https://tools.ietf.org/html/rfc4648#section-4)
packageHashAlgorithm    | odkazy řetězců                     | Ano      |
packageSize             | integer                    | Ano      | Velikost balíčku .nupkg v bajtech
projectUrl              | odkazy řetězců                     | Ne       |
ReleaseNotes            | odkazy řetězců                     | Ne       |
requireLicenseAgreement | Logická hodnota                    | Ne       | Předpokládejme `false` li vyloučit
souhrn                 | odkazy řetězců                     | Ne       |
značky                    | Pole řetězců.           | Ne       |
Název                   | odkazy řetězců                     | Ne       |
verbatimVersion         | odkazy řetězců                     | Ne       | Řetězec verze jako ho původně najde v příponou .nuspec

Balíček `version` vlastnost je řetězec úplné, normalizované verze. To znamená, že SemVer 2.0.0 sestavení data mohou být zahrnuté v tomto poli.

`created` Časové razítko je, když balíček je napřed přijata sadou zdroj balíčku, který je obvykle po krátkou dobu před časové razítko potvrzení položka katalogu.

`packageHashAlgorithm` Se, řetězce definované represeting implementace serveru používají k vytvoření algoritmu hash `packageHash`. nuget.org vždycky použijí `packageHashAlgorithm` hodnotu `SHA512`.

`published` Časové razítko je čas, pokud byl poslední uvedený balíček.

> [!Note]
> V nuget.org `published` hodnota nastavena na rok 1900 po neuvedené balíčku.

#### <a name="sample-request"></a>Ukázková žádost

GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

#### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [catalog-package-details.json](./_data/catalog-package-details.json)]

### <a name="package-delete-catalog-items"></a>Položky katalogu odstranění balíčku

Položky s typem katalogu `PackageDelete` obsahovat minimální sadu informace o tom klientům katalogu, že balíček se odstranil z balíčku zdroje a již není k dispozici pro všechny operace balíčku (například obnovení).

> [!Note]
> Je možné balíčku k odstranění a později znovu publikovat pomocí stejné ID balíčku a verzi. V nuget.org je velmi výjimečných případech, protože to naruší oficiální klient předpokládá, že ID balíčku a verzi implikují určitý balíček obsahu. Další informace o odstranění balíčku na nuget.org najdete v tématu [naše zásady](../policies/deleting-packages.md).

Položky katalogu odstranit balíček mít žádné další vlastnosti kromě těch, které [obsahovat všechny katalogu nechá](#catalog-leaf).

`version` Vlastnost je původní řetězec verze v balíčku příponou .nuspec nalezen.

`published` Vlastnost je čas, když balíček byl odstraněn, což je většinou jako krátkou dobu před časové razítko potvrzení položka katalogu.

#### <a name="sample-request"></a>Ukázková žádost

GET https://api.nuget.org/v3/catalog0/data/2017.11.02.00.40.00/netstandard1.4_lib.1.0.0-test.json

#### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [catalog-package-delete.json](./_data/catalog-package-delete.json)]

## <a name="cursor"></a>Kurzor

### <a name="overview"></a>Přehled

Tato část popisuje koncept klienta, který, i když není vyžadováno nutně protokolem, musí být součástí žádnou implementaci klienta praktické katalogu.

Protože katalogu je strukturu dat připojovacím indexované podle času, klient měli uložit **kurzor** místně, představující až co bodu v čase klienta zpracovala položky katalogu. Všimněte si, že tato hodnota kurzoru nikdy se má vygenerovat pomocí hodiny počítače klienta. Místo toho by měla být dřívější hodnota z objektu katalogu `commitTimestamp` hodnotu.

Pokaždé, když klient chce zpracovat nové události ve zdroji balíčku, je nutné pouze dotaz katalogu pro všechny položky katalogu s časovým razítkem potvrzení větší než jeho uložené kurzoru. Jakmile klient úspěšně zpracuje všechny nové položky katalogu, zaznamenává nejnovější časové razítko potvrzení položky katalogu, které jsou právě zpracovávány jako jeho nová hodnota kurzoru.

Tento přístup může být klient nezapomeňte nikdy neproběhly žádné události balíčku, které došlo k chybě ve zdroji balíčku.
Kromě toho klient nikdy opětovné zpracování staré události před časové razítko potvrzení zaznamenaná na pozici kurzoru.

Tato účinný koncept kurzory se používá pro řadu úloh na pozadí nuget.org a slouží k zachování aktualizovaného stavu rozhraní API V3, sám sebe. 

### <a name="initial-value"></a>Počáteční hodnota

Když klient katalogu zahajuje velmi první (a proto nemá žádnou hodnotu kurzoru), měla by používat výchozí hodnotu kurzoru. NET na `System.DateTimeOffset.MinValue` nebo určitou takové podobá představu o minimální reprezentovat časové razítko.

### <a name="iterating-over-catalog-items"></a>Iterování přes položky katalogu

Dotaz pro další sadu položek katalogu pro zpracování, klient proveďte následující kroky:

1. Načtení kurzoru zaznamenaná hodnota z místního úložiště.
1. Stáhněte si a deserializovat index katalogu.
1. Najít všechny stránky s časovým razítkem potvrzení katalogu *větší než* kurzor.
1. Deklarujte prázdný seznam položek katalogu ke zpracování.
1. Pro každou stránku katalogu shodná v kroku 3:
   1. Stáhněte si a deserializovat stránce katalogu.
   1. Najít všechny položky s časovým razítkem potvrzení katalogu *větší než* kurzor.
   1. Přidejte všechny odpovídající položky katalogu do seznamu deklarované v kroku 4.
1. Seřadíte seznam položek katalogu časové razítko potvrzení.
1. Zpracování jednotlivých položek katalogu v pořadí:
   1. Stáhněte si a deserializovat položka katalogu.
   1. Náležitě reagovat na typ položky katalogu.
   1. Proces dokumentu položky katalogu způsobem specifické pro klienta.
1. Zaznamenejte časové razítko poslední položky katalogu potvrzení jako nová hodnota kurzoru.

Pomocí základního algoritmu můžete vytvořit implementace klienta kompletní zobrazení všech balíčků dostupných ve zdroji balíčku. Klient musí provést pouze tento algoritmus pravidelně vždy informováni o nejnovějších změn ke zdroji balíčku.

> [!Note]
> To je algoritmus, který používá tento nuget.org zachovat [Metadata balíčků](registration-base-url-resource.md), [obsah balíčku](package-base-address-resource.md), [vyhledávání](search-query-service-resource.md) a [automatického dokončování](search-autocomplete-service-resource.md) Aktuální prostředky.

### <a name="dependent-cursors"></a>Závislé kurzory

Předpokládejme, že existují dvě katalogu klienti, kteří mají inherant závislostí, kde výstup jednoho klienta závisí na výstupu jiného klienta. 

#### <a name="example"></a>Příklad

Například v nuget.org přehled nově publikovaných balíček neměla by se zobrazit v prostředku hledání se zobrazí v prostředek metadat balíčku. Je to proto, že operace "obnovení" prováděných klientem oficiální NuGet používá prostředek metadat balíčku. Pokud zákazník zjistí balíčku pomocí vyhledávací službu, že byste měli mít úspěšně obnovit tento balíček pomocí prostředek metadat balíčku. Vyhledávání prostředků, jinými slovy, závisí na prostředek metadat balíčku. Každý prostředek má úloha katalogu klienta pozadí aktualizace prostředku. Každý klient má svou vlastní kurzoru.

Vzhledem k tomu, že oba prostředky jsou vytvořené z katalogu, kurzor katalogu klienta, která aktualizuje prostředek vyhledávání *nesmí přesahovat* kurzor klienta katalogu metadat balíčku.

#### <a name="algorithm"></a>Algoritmus

Pokud chcete implementovat toto omezení, upravte jednoduchý algoritmus výše uvedené jako:

1. Načtení kurzoru zaznamenaná hodnota z místního úložiště.
1. Stáhněte si a deserializovat index katalogu.
1. Najít všechny stránky s časovým razítkem potvrzení katalogu *větší než* kurzor **menší než nebo rovna této závislosti kurzoru.**
1. Deklarujte prázdný seznam položek katalogu ke zpracování.
1. Pro každou stránku katalogu shodná v kroku 3:
   1. Stáhněte si a deserializovat stránce katalogu.
   1. Najít všechny položky s časovým razítkem potvrzení katalogu *větší než* kurzor **menší než nebo rovna této závislosti kurzoru.**
   1. Přidejte všechny odpovídající položky katalogu do seznamu deklarované v kroku 4.
1. Seřadíte seznam položek katalogu časové razítko potvrzení.
1. Zpracování jednotlivých položek katalogu v pořadí:
   1. Stáhněte si a deserializovat položka katalogu.
   1. Náležitě reagovat na typ položky katalogu.
   1. Proces dokumentu položky katalogu způsobem specifické pro klienta.
1. Zaznamenejte časové razítko poslední položky katalogu potvrzení jako nová hodnota kurzoru.

Pomocí této změny algoritmu, můžete vytvořit systému závislé katalogu klientů všechny vytváření vlastních konkrétními indexy, artefakty atd.
