---
title: Metadata balíčků NuGet rozhraní API
description: Balíček registrace základní adresu URL umožňuje načítání metadat o balíčcích.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 50064e1450232e9cdedcc042a09c08860f802e76
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822220"
---
# <a name="package-metadata"></a>Metadata balíčků

Je možné načíst metadata o balíčků dostupných ve zdroji balíčku pomocí rozhraní API V3 NuGet. Tato metadata můžete načíst pomocí `RegistrationsBaseUrl` v nalezen prostředek [indexu služby](service-index.md).

Kolekce dokumentů v `RegistrationsBaseUrl` se často nazývají "registrace" nebo "registrace objekty BLOB". Sada dokumentů v rámci jedné `RegistrationsBaseUrl` se označuje jako "registrace hive". Registrace hive obsahuje všechny metadata o každého balíčku k dispozici ve zdroji balíčku.

## <a name="versioning"></a>Správa verzí

Následující `@type` se používají hodnoty:

@type Hodnota                     | Poznámky
------------------------------- | -----
RegistrationsBaseUrl            | Původní verze
RegistrationsBaseUrl/3.0.0-beta | Alias `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.0.0-rc   | Alias `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.4.0      | Algoritmem gzip odpovědí
RegistrationsBaseUrl/3.6.0      | Zahrnuje SemVer 2.0.0 balíčky

To představuje podregistrů tři odlišné registrace k dispozici pro různé verze klienta.

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

Tyto registrace nejsou komprimované (což znamená, používají předpokládané `Content-Encoding: identity`). SemVer 2.0.0 balíčky jsou **vyloučené** z tomuto podregistru.

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4.0

Tyto registrace jsou komprimována pomocí `Content-Encoding: gzip`. SemVer 2.0.0 balíčky jsou **vyloučené** z tomuto podregistru.

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6.0

Tyto registrace jsou komprimována pomocí `Content-Encoding: gzip`. SemVer 2.0.0 balíčky jsou **zahrnuté** v tomuto podregistru.
Další informace o SemVer 2.0.0, najdete v části [SemVer 2.0.0 podpora nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29).

## <a name="base-url"></a>Základní adresu URL

Základní adresu URL pro následující rozhraní API je hodnota `@id` vlastnost spojená s zmíněnými prostředků `@type` hodnoty. V následujícím dokumentu zástupného textu základní adresa URL `{@id}` se použije.

## <a name="http-methods"></a>Metody HTTP

Všechny adresy URL v podpory registrace prostředků nalezen metody HTTP `GET` a `HEAD`.

## <a name="registration-index"></a>Index registrace

Skupiny prostředků registrační balíček metadata podle ID balíčku. Není možné získat data o více než jeden ID balíčku najednou. Tento prostředek poskytuje způsob, jak zjistit ID balíčku. Místo toho klient předpokládá se, že již znáte ID požadované balíčku. K dispozici metadata o jednotlivých verzí balíčku se liší podle implementaci serveru. Objekty BLOB registrační balíček mají následující hierarchickou strukturu:

- **Index**: vstupní bod pro metadata balíčků, sdílí všechny balíčky ve zdroji se stejným ID balíčku.
- **Stránka**: seskupení verze balíčku. Číslo verze balíčku na stránce je definován implementaci serveru.
- **Listu**: specifické pro jeden balíček verze dokumentu.

Adresa URL registrace indexu je předvídatelný a klientem daného ID balíčku a registrace prostředku se dá určit `@id` hodnotu z indexu služby. Zjištění adresy URL pro registraci stránky a nechá zkontrolováním index registrace.

### <a name="registration-pages-and-leaves"></a>Registrace stránky a nechá

I když je to požadováno, nejedná striktně pro implementaci serveru pro ukládání, že registrace listy v samostatných registrací stránka dokumenty, je doporučený postup pro konzervaci paměti na straně klienta. Místo vložené všechny registrace ponechá v indexu nebo okamžitě ukládání nechá v dokumentech stránky, doporučuje se, že implementaci serveru definovat některé heuristiky si vybrat mezi dva přístupy, na základě počtu verze balíčku nebo Celková velikost všech balíček opustí.

Ukládání všechny verze balíčku (zůstanou) uloží index registrace na počet požadavků HTTP potřebné k načtení metadat balíčku ale znamená, že je nutné stáhnout větší dokumentu a musí být přidělena více paměti klienta. Na druhé straně Pokud implementaci serveru okamžitě ukládá nechá registrace v dokumentech zvláštní stránce, klient musíte provést další požadavky HTTP na získat informace, které potřebuje.

Heuristiky, který používá nuget.org je následujícím způsobem: Pokud je 128 nebo další verze balíčku, rozdělit na listech na stránky o velikosti 64. Pokud je kratší než 128 verze, vložené všechny ponechá do indexu registrace.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>Parametry žádosti

Název     | V     | Typ    | Požadováno | Poznámky
-------- | ------ | ------- | -------- | -----
LOWER_ID | Adresa URL    | odkazy řetězců  | Ano      | ID balíčku, psané malými písmeny

`LOWER_ID` Hodnota je psané malými písmeny pomocí pravidel implementovaných podle ID požadované balíčku. NET na [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) metoda.

### <a name="response"></a>Odpověď

Odpověď je dokument JSON, který má kořenový objekt s následujícími vlastnostmi:

Název  | Typ             | Požadováno | Poznámky
----- | ---------------- | -------- | -----
count | integer          | Ano      | Počet stránek registrace v indexu
Položky | Pole objektů | Ano      | Pole stránek registrace

Každá položka v objektu indexu `items` pole je objekt JSON představující na stránce registrace.

#### <a name="registration-page-object"></a>Registrace stránky objektu

Objekt stránku registrace nachází v indexu. registrace má následující vlastnosti:

Název   | Typ             | Požadováno | Poznámky
------ | ---------------- | -------- | -----
@id    | odkazy řetězců           | Ano      | Adresa URL k registrační stránce
count  | integer          | Ano      | Počet registrace ponechá na stránce
Položky  | Pole objektů | Ne       | Pole nechá registraci a jejich přidružení metadat
Nižší  | odkazy řetězců           | Ano      | Nejnižší verze SemVer 2.0.0 na stránce (včetně)
Nadřazené | odkazy řetězců           | Ne       | Adresa URL registrace indexu
horní  | odkazy řetězců           | Ano      | Nejvyšší verze SemVer 2.0.0 na stránce (včetně)

`lower` a `upper` hranice objektu page jsou užitečné v případě, kdy metadata pro konkrétní stránky verze.
Tyto hranice slouží k načtení jenom registrační stránce potřeby. Řetězce verze dodržovat [pravidla verze NuGet](../reference/package-versioning.md). Řetězce verze jsou normalized a nebudou obsahovat metadata sestavení. Jak se všemi verzemi v ekosystému NuGet, porovnání řetězců verzí je implementovaná pomocí [pravidla priorit verze SemVer 2.0.0's](http://semver.org/spec/v2.0.0.html#spec-item-11).

`parent` Vlastnost se zobrazí, pouze pokud má objekt stránku registrace `items` vlastnost.

Pokud `items` vlastnost není součástí objektu page registrace, zadat adresu URL v `@id` musíte použít k načtení metadat o verze jednotlivých balíčků. `items` Pole je někdy vyloučen z objektu stránky jako optimalizace. Pokud je velký počet verzí a ID jeden balíček, pak registraci u dokumentu indexu bude masivního a plýtvání procesu pro klienta, který záleží jenom na konkrétní verzi nebo malé oblast verze.

Všimněte si, že pokud `items` vlastnost nachází, `@id` vlastnost nemusíte použít, protože všechna data stránky je již v vloženou obslužnou `items` vlastnost.

Každá položka v objektu page `items` pole je objekt JSON představující listu registrace a je přiřazen metadat.

#### <a name="registration-leaf-object-in-a-page"></a>Registrace typu list objekt na stránce

Objekt typu list registrace najít na stránce registrace má následující vlastnosti:

Název           | Typ   | Požadováno | Poznámky
-------------- | ------ | -------- | -----
@id            | odkazy řetězců | Ano      | Adresu URL na listu registrace
catalogEntry   | odkazy objektů | Ano      | Položka katalogu obsahující metadata balíčků
packageContent | odkazy řetězců | Ano      | Adresa URL obsah balíčku (.nupkg)

Každý objekt typu list registrace představuje data související s verzí jednoho balíčku.

#### <a name="catalog-entry"></a>Položka katalogu

`catalogEntry` Vlastnost v objektu registrace typu list má následující vlastnosti:

Název                     | Typ                       | Požadováno | Poznámky
------------------------ | -------------------------- | -------- | -----
@id                      | odkazy řetězců                     | Ano      | Adresa URL dokumentu se používají k vytvoření tohoto objektu
Autoři                  | řetězec nebo pole řetězců. | Ne       | 
dependencyGroups         | Pole objektů           | Ne       | Závislosti balíčku, seskupené podle cílové rozhraní
description              | odkazy řetězců                     | Ne       | 
IconUrl                  | odkazy řetězců                     | Ne       | 
id                       | odkazy řetězců                     | Ano      | ID balíčku
Adresa LicenseUrl               | odkazy řetězců                     | Ne       | 
uvedené v seznamu                   | Logická hodnota                    | Ne       | By měly být považovány za uvedené Pokud chybí
MinClientVersion         | odkazy řetězců                     | Ne       | 
Adrese ProjectUrl               | odkazy řetězců                     | Ne       | 
Publikovat                | odkazy řetězců                     | Ne       | Řetězec obsahující časové razítko ISO 8601. Pokud byla publikována balíčku
RequireLicenseAcceptance | Logická hodnota                    | Ne       | 
souhrn                  | odkazy řetězců                     | Ne       | 
značky                     | řetězec nebo pole řetězců  | Ne       | 
Název                    | odkazy řetězců                     | Ne       | 
verze                  | odkazy řetězců                     | Ano      | Verze balíčku

`dependencyGroups` Vlastnost je pole objektů představující závislosti balíčku, seskupené podle cílové rozhraní. Pokud balíček nemá žádné závislosti `dependencyGroups` vlastnost chybí, prázdné pole, nebo `dependencies` vlastnosti všech skupin je prázdný nebo chybí.

#### <a name="package-dependency-group"></a>Skupina závislosti balíčku

Každý objekt skupiny závislosti má následující vlastnosti:

Název            | Typ             | Požadováno | Poznámky
--------------- | ---------------- | -------- | -----
targetFramework | odkazy řetězců           | Ne       | Cílové rozhraní, které se vztahují na tyto závislosti
závislosti    | Pole objektů | Ne       |

`targetFramework` Řetězec používá formát implementované knihovny .NET NuGet [NuGet.Frameworks](https://www.nuget.org/packages/NuGet.Frameworks/). Pokud žádné `targetFramework` není zadaný, skupina závislosti se vztahují na všechny cílové architektury.

`dependencies` Vlastnost je pole objektů, každý představující aktuální balíček závislost balíčku.

#### <a name="package-dependency"></a>Závislost balíčku

Každá závislost balíčku má následující vlastnosti:

Název         | Typ   | Požadováno | Poznámky
------------ | ------ | -------- | -----
id           | odkazy řetězců | Ano      | ID závislost balíčku
range        | odkazy objektů | Ne       | Povolené maximum [rozsahu verze](../reference/package-versioning.md#version-ranges-and-wildcards) závislosti
registrace | odkazy řetězců | Ne       | Adresa URL registrace indexu pro tuto závislost

Pokud `range` vlastnost je vyloučená nebo prázdný řetězec, klient by měl výchozí verze rozsahu `(, )`. To znamená je povolen, všechny verze závislosti.

### <a name="sample-request"></a>Ukázková žádost

    GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json

### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

V tomto konkrétním případě index registrace má vložená registrační stránce, takže k načíst metadata o verze jednotlivých balíčků nejsou potřeba žádné další požadavky.

## <a name="registration-page"></a>Registrační stránce

Registrační stránce obsahuje nechá registrace. Adresu URL k načtení stránky registrace je určen podle `@id` vlastnost [registrace stránky objektu](#registration-page-object) uvedených výše.

Když `items` pole není k dispozici v indexu registrace, z požadavku HTTP GET `@id` hodnota vrátí dokumentu JSON, který má objekt jako svůj kořen. Objekt má následující vlastnosti:

Název   | Typ             | Požadováno | Poznámky
------ | ---------------- | -------- | -----
@id    | odkazy řetězců           | Ano      | Adresa URL k registrační stránce
count  | integer          | Ano      | Počet registrace ponechá na stránce
Položky  | Pole objektů | Ano      | Pole nechá registraci a jejich přidružení metadat
Nižší  | odkazy řetězců           | Ano      | Nejnižší verze SemVer 2.0.0 na stránce (včetně)
Nadřazené | odkazy řetězců           | Ano      | Adresa URL registrace indexu
horní  | odkazy řetězců           | Ano      | Nejvyšší verze SemVer 2.0.0 na stránce (včetně)

Obrazec objekty listu registrace je stejný jako index registrace [výše](#registration-leaf-object-in-a-page).

## <a name="sample-request"></a>Ukázková žádost

    GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json

## <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>Registrace listu

Registrace typu list obsahuje informace o konkrétní balíček ID a verzi. Metadata o konkrétní verzi nemusí být k dispozici v tomto dokumentu. Je potřeba načíst metadata balíčků z [registrace index](#registration-index) nebo [registrační stránce](#registration-page) (což je zjištěno pomocí indexu registrace).

Adresa URL načíst listu registrace se získávají z `@id` vlastnost objektu typu list registrace v indexu registrace nebo registrační stránce.

Registrace listu je dokument JSON s kořenový objekt s následujícími vlastnostmi:

Název           | Typ    | Požadováno | Poznámky
-------------- | ------- | -------- | -----
@id            | odkazy řetězců  | Ano      | Adresu URL na listu registrace
catalogEntry   | odkazy řetězců  | Ne       | Adresu URL pro položky katalogu, která vytváří tyto listu
uvedené v seznamu         | Logická hodnota | Ne       | By měly být považovány za uvedené Pokud chybí
packageContent | odkazy řetězců  | Ne       | Adresa URL obsah balíčku (.nupkg)
Publikovat      | odkazy řetězců  | Ne       | Řetězec obsahující časové razítko ISO 8601. Pokud byla publikována balíčku
registrace   | odkazy řetězců  | Ne       | Adresa URL registrace indexu

> [!Note]
> V nuget.org `published` hodnota nastavena na rok 1900 po neuvedené balíčku.

### <a name="sample-request"></a>Ukázková žádost

    GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json

### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
