---
title: Metadata balíčku, API NuGet
description: Základní adresa URL pro registraci balíčku umožňuje načítat metadata o balíčcích.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1a2e98ab36c8dc08e5f14b19b57f5ea0d790524c
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488319"
---
# <a name="package-metadata"></a>Metadata balíčků

Je možné načíst metadata o balíčcích dostupných ve zdroji balíčku pomocí rozhraní NuGet V3 API. Tato metadata lze načíst pomocí prostředku, který `RegistrationsBaseUrl` najdete v [indexu služby](service-index.md).

Kolekce dokumentů, které se nacházejí v `RegistrationsBaseUrl` části, se často nazývají "registrace" nebo "objekty blob registrace". Sada dokumentů na jednom `RegistrationsBaseUrl` z nich se označuje jako registrační podregistr. Registrační podregistr obsahuje všechna metadata o každém balíčku, který je k dispozici ve zdroji balíčku.

## <a name="versioning"></a>Správa verzí

Použijí se `@type` tyto hodnoty:

@typeosa                     | Poznámky
------------------------------- | -----
RegistrationsBaseUrl            | Počáteční verze
RegistrationsBaseUrl/3.0.0 – beta | Alias pro`RegistrationsBaseUrl`
RegistrationsBaseUrl/3.0.0 – RC   | Alias pro`RegistrationsBaseUrl`
RegistrationsBaseUrl/3.4.0      | Komprimovaný jako gzip odpovědi
RegistrationsBaseUrl/3.6.0      | Zahrnuje balíčky 2.0.0 pro SemVer

To představuje tři samostatné registrační podregistry, které jsou k dispozici pro různé verze klienta.

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

Tyto registrace nejsou komprimovány (což znamená, že používají implicitní `Content-Encoding: identity`). Z tohoto podregistru jsou vyloučeny balíčky 2.0.0 SemVer.

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4.0

Tyto registrace se komprimují pomocí `Content-Encoding: gzip`. Z tohoto podregistru jsou vyloučeny balíčky 2.0.0 SemVer.

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6.0

Tyto registrace se komprimují pomocí `Content-Encoding: gzip`. V tomto podregistru jsou zahrnuté balíčky 2.0.0 SemVer.
Další informace o SemVer 2.0.0 najdete v tématu [Podpora SemVer 2.0.0 pro NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29).

## <a name="base-url"></a>Základní adresa URL

Základní adresa URL následujících rozhraní API je hodnota `@id` vlastnosti přidružené k výše uvedeným hodnotám prostředku. `@type` V následujícím dokumentu se použije zástupná základní `{@id}` adresa URL.

## <a name="http-methods"></a>Metody HTTP

Všechny adresy URL nalezené v registračním prostředku podporují metody `GET` http `HEAD`a.

## <a name="registration-index"></a>Registrační index

Prostředek registrace seskupuje metadata balíčku podle ID balíčku. Nemůžete najednou získat data o více než jednom ID balíčku. Tento prostředek neposkytuje žádný způsob, jak zjišťovat ID balíčků. Místo toho se předpokládá, že je u klienta již známo ID požadovaného balíčku. Dostupná metadata týkající se jednotlivých verzí balíčků se liší podle implementace serveru. Objekty blob pro registraci balíčků mají následující hierarchickou strukturu:

- **Index**: vstupní bod pro metadata balíčku, který sdílí všechny balíčky na zdroji se stejným ID balíčku.
- **Stránka**: seskupení verzí balíčku. Počet verzí balíčku na stránce je definován implementací serveru.
- **List**: dokument určený pro jednu verzi balíčku.

Adresa URL registračního indexu je předvídatelné a může být určena klientem pro ID balíčku a `@id` hodnotu prostředku registrace z indexu služby. Adresy URL registračních stránek a listů jsou zjištěny kontrolou registračního indexu.

### <a name="registration-pages-and-leaves"></a>Registrační stránky a listy

Ačkoli není bezpodmínečně nutné, aby implementace serveru ukládala registrační listy v samostatných dokumentech registrační stránky, je doporučený postup pro zachování paměti na straně klienta. Místo vložení všech registračních ponechá v indexu nebo okamžitě uloží listy do stránkovacích dokumentů, doporučuje se, aby implementace serveru definovala určitou heuristickou volbu mezi oběma přístupy na základě počtu verzí balíčku nebo vynechává se kumulativní velikost balíčku.

Uložení všech verzí balíčku (opustí) v registračním indexu šetří počet požadavků HTTP potřebných k načtení metadat balíčku, ale znamená, že je nutné stáhnout větší dokument a musí být přidělena více klientských paměti. Na druhé straně, pokud implementace serveru hned ukládá registraci v samostatných dokumentech stránky, klient musí provést další požadavky HTTP, aby získal informace, které potřebuje.

Tato heuristická metoda, kterou používá nuget.org, je následující: Pokud jsou k dispozici 128 nebo více verzí balíčku, přerušte listy na velikost 64. Pokud jsou k dispozici méně než 128 verzí, všechny zůstanou vloženy do registračního indexu.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>Parametry žádosti

Name     | V     | type    | Požadováno | Poznámky
-------- | ------ | ------- | -------- | -----
LOWER_ID | Adresa URL    | odkazy řetězců  | ano      | ID balíčku, malými písmeny

`LOWER_ID` Hodnota je ID požadovaného balíčku s malými písmeny pomocí pravidel implementovaných pomocí. [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) Metoda netto.

### <a name="response"></a>Odpověď

Odpověď je dokument JSON, který má kořenový objekt s následujícími vlastnostmi:

Name  | type             | Požadováno | Poznámky
----- | ---------------- | -------- | -----
count | integer          | ano      | Počet registračních stránek v indexu
items | pole objektů | ano      | Pole registračních stránek

Každá položka v `items` poli objektu index je objekt JSON, který představuje registrační stránku.

#### <a name="registration-page-object"></a>Registrační objekt stránky

Registrační objekt stránky, který se našel v registračním indexu, má tyto vlastnosti:

Name   | type             | Požadováno | Poznámky
------ | ---------------- | -------- | -----
@id    | odkazy řetězců           | ano      | Adresa URL stránky pro registraci
count  | integer          | ano      | Počet ponechání registrace na stránce
items  | pole objektů | Ne       | Pole registrace opustí a jejich přidružená metadata
malým  | odkazy řetězců           | ano      | Nejnižší verze SemVer 2.0.0 na stránce (včetně)
nadřazený | odkazy řetězců           | Ne       | Adresa URL indexu registrace
umístit  | odkazy řetězců           | ano      | Nejvyšší verze SemVer 2.0.0 na stránce (včetně)

Meze `lower` objektů `upper` stránky a jsou užitečné v případě, že je potřeba metadata pro konkrétní verzi stránky.
Tyto hranice lze použít k načtení jediné registrační stránky, kterou potřebujete. Řetězce verze vyhovují [pravidlům verzí NuGet](../concepts/package-versioning.md). Řetězce verze jsou normalizovány a neobsahují metadata sestavení. Stejně jako u všech verzí v ekosystému NuGet se porovnání řetězců verzí implementuje pomocí [pravidel priority verze SemVer 2.0.0](http://semver.org/spec/v2.0.0.html#spec-item-11).

Vlastnost se zobrazí pouze v případě, že objekt registrační stránky `items` má vlastnost. `parent`

Pokud vlastnost není k dispozici v objektu registrační stránky, adresa URL zadaná v rozhraní `@id` musí být použita k načtení metadat o jednotlivých verzích balíčků. `items` `items` Pole je někdy vyloučeno z objektu Page jako optimalizace. Pokud je počet verzí jednoho balíčku moc velký, pak bude dokument indexu registrace obrovský a wasteful se na zpracování pro klienta, který stojí jenom na konkrétní verzi nebo malý rozsah verzí.

Všimněte si, že `items` Pokud je vlastnost přítomna `@id` , není nutné použít vlastnost, protože všechna data stránky jsou již vložena do `items` vlastnosti.

Každá položka v `items` poli objektu stránky je objekt JSON, který představuje registrační list a má přidružená metadata.

#### <a name="registration-leaf-object-in-a-page"></a>Registrační listový objekt na stránce

Registrační objekt na listu, který se našel na registrační stránce, má tyto vlastnosti:

Name           | type   | Požadováno | Poznámky
-------------- | ------ | -------- | -----
@id            | odkazy řetězců | ano      | Adresa URL listu registrace
catalogEntry   | odkazy objektů | ano      | Záznam katalogu obsahující metadata balíčku
packageContent | odkazy řetězců | ano      | Adresa URL obsahu balíčku (. nupkg)

Každý registrační listový objekt představuje data přidružená k jedné verzi balíčku.

#### <a name="catalog-entry"></a>Záznam v katalogu

`catalogEntry` Vlastnost v objektu registračního listu má následující vlastnosti:

Name                     | type                       | Požadováno | Poznámky
------------------------ | -------------------------- | -------- | -----
@id                      | odkazy řetězců                     | ano      | Adresa URL dokumentu použitá k vyprodukování tohoto objektu
Autoři                  | řetězec nebo pole řetězců | Ne       | 
dependencyGroups         | pole objektů           | Ne       | Závislosti balíčku seskupené podle cílové architektury
vyřazení              | odkazy objektů                     | Ne       | Zastaralé přidružení k balíčku
description              | odkazy řetězců                     | Ne       | 
iconUrl                  | odkazy řetězců                     | Ne       | 
id                       | odkazy řetězců                     | ano      | ID balíčku
licenseUrl               | odkazy řetězců                     | Ne       |
licenseExpression        | odkazy řetězců                     | Ne       | 
uvedené v seznamu                   | Logická hodnota                    | Ne       | By mělo být považováno za uvedené, pokud chybí
minClientVersion         | odkazy řetězců                     | Ne       | 
projectUrl               | odkazy řetězců                     | Ne       | 
zveřejněna                | odkazy řetězců                     | Ne       | Řetězec obsahující časové razítko ISO 8601 při publikování balíčku
requireLicenseAcceptance | Logická hodnota                    | Ne       | 
souhrn                  | odkazy řetězců                     | Ne       | 
značky                     | řetězec nebo pole řetězce  | Ne       | 
název                    | odkazy řetězců                     | Ne       | 
verze                  | odkazy řetězců                     | ano      | Úplný řetězec verze po normalizaci

Vlastnost Package `version` je úplný řetězec verze po normalizaci. To znamená, že sem můžete zahrnout data sestavení SemVer 2.0.0.

`dependencyGroups` Vlastnost je pole objektů reprezentující závislosti balíčku seskupené podle cílové architektury. Pokud balíček nemá žádné závislosti, `dependencyGroups` vlastnost chybí, prázdné pole `dependencies` nebo vlastnost všech skupin jsou prázdné nebo chybí.

Hodnota `licenseExpression` vlastnosti je v souladu s [syntaxí multilicenčního výrazu NuGet](https://docs.microsoft.com/en-us/nuget/reference/nuspec#license).

#### <a name="package-dependency-group"></a>Skupina závislostí balíčku

Každý objekt skupiny závislostí má následující vlastnosti:

Name            | type             | Požadováno | Poznámky
--------------- | ---------------- | -------- | -----
targetFramework | odkazy řetězců           | Ne       | Cílové rozhraní .NET Framework, na které se tyto závislosti vztahují
závislosti    | pole objektů | Ne       |

Řetězec používá formát implementovaný rozhraním NuGet knihovny .NET pro NuGet [. architektury.](https://www.nuget.org/packages/NuGet.Frameworks/) `targetFramework` `targetFramework` Pokud není zadaný, použije se skupina závislostí na všechny cílové architektury.

`dependencies` Vlastnost je pole objektů, z nichž každý představuje závislost balíčku aktuálního balíčku.

#### <a name="package-dependency"></a>Závislost balíčku

Jednotlivé závislosti balíčků mají následující vlastnosti:

Name         | type   | Požadováno | Poznámky
------------ | ------ | -------- | -----
id           | odkazy řetězců | ano      | ID závislosti balíčku
range        | odkazy objektů | Ne       | Povolený [rozsah verzí](../concepts/package-versioning.md#version-ranges-and-wildcards) závislosti
registrace | odkazy řetězců | Ne       | Adresa URL indexu registrace pro tuto závislost

Pokud je `(, )`vlastnost vyloučená nebo je prázdným řetězcem, měl by být ve výchozím nastavení povolený rozsah verzí klienta. `range` To znamená, že je povolená jakákoli verze závislosti.

#### <a name="package-deprecation"></a>Zastaralé balíčky

Každý zastaralý balíček má následující vlastnosti:

Name             | type             | Požadováno | Poznámky
---------------- | ---------------- | -------- | -----
hlediska          | pole řetězců | ano      | Důvody, proč byl balíček zastaralý
zpráva          | odkazy řetězců           | Ne       | Další podrobnosti o této zastaralosti
alternatePackage | odkazy objektů           | Ne       | Závislost balíčku, která se má použít místo toho

`reasons` Vlastnost musí obsahovat alespoň jeden řetězec a měla by obsahovat pouze řetězce z následující tabulky:

Důvod       | Popis             
------------ | -----------
Starší verze       | Balíček se už neudržuje.
CriticalBugs | Balíček obsahuje chyby, které nejsou vhodné pro použití.
Ostatní        | Balíček je zastaralý z důvodu, že tento seznam není v tomto seznamu.

`reasons` Pokud vlastnost obsahuje řetězce, které nejsou ze známé sady, měly by být ignorovány. V řetězcích nejsou rozlišována velká a malá `legacy` písmena, proto by měla být `Legacy`zpracována stejně jako. V poli není žádné omezení řazení, takže řetězce mohou být uspořádány do libovolného pořadí. Kromě toho, pokud vlastnost obsahuje pouze řetězce, které nejsou ze známé sady, měla by být zpracována, jako by obsahovala pouze řetězec "other".

### <a name="sample-request"></a>Ukázková žádost

    GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json

### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

V tomto konkrétním případě registrační index má registrační stránku vloženě, takže nepotřebujete žádné další požadavky k načtení metadat pro jednotlivé verze balíčků.

## <a name="registration-page"></a>Registrační stránka

Registrační stránka obsahuje ponechání registračních stránek. Adresa URL pro načtení registrační stránky je určena `@id` vlastností ve výše uvedeném [objektu registrační stránky](#registration-page-object) .

Pokud pole není v registračním indexu k dispozici, vrátí požadavek HTTP GET na `@id` hodnotu dokument JSON, který má objekt jako svůj kořenový adresář. `items` Objekt má následující vlastnosti:

Name   | type             | Požadováno | Poznámky
------ | ---------------- | -------- | -----
@id    | odkazy řetězců           | ano      | Adresa URL stránky pro registraci
count  | integer          | ano      | Počet ponechání registrace na stránce
items  | pole objektů | ano      | Pole registrace opustí a jejich přidružená metadata
malým  | odkazy řetězců           | ano      | Nejnižší verze SemVer 2.0.0 na stránce (včetně)
nadřazený | odkazy řetězců           | ano      | Adresa URL indexu registrace
umístit  | odkazy řetězců           | ano      | Nejvyšší verze SemVer 2.0.0 na stránce (včetně)

Tvar listů registračních objektů je stejný jako v indexu registrace [výše](#registration-leaf-object-in-a-page).

## <a name="sample-request"></a>Ukázková žádost

    GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json

## <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>Registrační list

Registrační list obsahuje informace o konkrétním ID a verzi balíčku. Metadata týkající se konkrétní verze nemusí být v tomto dokumentu k dispozici. Metadata balíčku by se měla načíst z registračního [indexu](#registration-index) nebo [registrační stránky](#registration-page) (která se zjistila pomocí registračního indexu).

Adresa URL pro načtení registračního listu je získána z `@id` vlastnosti registračního objektu listu v registračním indexu nebo na registrační stránce.

Registrační list je dokument JSON s kořenovým objektem s následujícími vlastnostmi:

Name           | type    | Požadováno | Poznámky
-------------- | ------- | -------- | -----
@id            | odkazy řetězců  | ano      | Adresa URL listu registrace
catalogEntry   | odkazy řetězců  | Ne       | Adresa URL položky katalogu, která vytvořila tento list
uvedené v seznamu         | Logická hodnota | Ne       | By mělo být považováno za uvedené, pokud chybí
packageContent | odkazy řetězců  | Ne       | Adresa URL obsahu balíčku (. nupkg)
zveřejněna      | odkazy řetězců  | Ne       | Řetězec obsahující časové razítko ISO 8601 při publikování balíčku
registrace   | odkazy řetězců  | Ne       | Adresa URL indexu registrace

> [!Note]
> V NuGet.org je `published` hodnota nastavena na rok 1900, pokud je balíček neuvedený.

### <a name="sample-request"></a>Ukázková žádost

    GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json

### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
