---
title: Metadata balíčku NuGet rozhraní API
description: V balíčku základní adresa URL pro registraci umožňuje načítání metadat o balíčcích.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 0b35e2bbdde63f7f7a5298bd035c180389cd345d
ms.sourcegitcommit: 2a9d149bc6f5ff76b0b657324820bd0429cddeef
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/01/2019
ms.locfileid: "67496502"
---
# <a name="package-metadata"></a>Metadata balíčků

Je možné načíst metadata balíčků dostupných ve zdroji balíčků pomocí NuGet rozhraní API V3. Tato metadata můžete načíst pomocí `RegistrationsBaseUrl` prostředek se nenašel v [index služby](service-index.md).

Kolekce dokumentů nalezené pod `RegistrationsBaseUrl` jsou často nazývány "registrace" nebo "objekty BLOB registrace". Sadu dokumentů v rámci jediného `RegistrationsBaseUrl` se označuje jako "hive registrace". Registrace hive obsahuje všechny metadata o všech balíčků dostupných ve zdroji balíčku.

## <a name="versioning"></a>Správa verzí

Následující `@type` hodnoty:

@type Hodnota                     | Poznámky
------------------------------- | -----
RegistrationsBaseUrl            | Počáteční verze
RegistrationsBaseUrl/3.0.0-beta | Alias of `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.0.0-rc   | Alias of `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.4.0      | Komprimovaný jako GZIP odpovědi
RegistrationsBaseUrl/3.6.0      | Obsahuje balíčky SemVer 2.0.0

Reprezentuje podregistry tři odlišné registrace k dispozici pro různé verze klienta.

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

Tyto registrace nejsou komprimované (to znamená, že používají k předpokládanému `Content-Encoding: identity`). SemVer 2.0.0 balíčky jsou **vyloučené** z této hive.

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4.0

Tyto registrace jsou komprimované pomocí `Content-Encoding: gzip`. SemVer 2.0.0 balíčky jsou **vyloučené** z této hive.

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6.0

Tyto registrace jsou komprimované pomocí `Content-Encoding: gzip`. SemVer 2.0.0 balíčky jsou **zahrnuté** v tomto hive.
Další informace o SemVer 2.0.0 najdete v tématu [SemVer 2.0.0 podpora nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29).

## <a name="base-url"></a>Základní adresa URL

Základní adresa URL pro následující rozhraní API je hodnota `@id` vlastnost přidružená k výše uvedených prostředků `@type` hodnoty. V následujícím dokumentu, zástupný symbol základní adresa URL `{@id}` se použije.

## <a name="http-methods"></a>Metody HTTP

Všechny adresy URL, které jsou součástí zdroje podpory registrace metody HTTP `GET` a `HEAD`.

## <a name="registration-index"></a>Registrace indexu

Skupiny prostředků registrační balíček metadata podle ID balíčku. Není možné současně zobrazit údaje o více než jeden ID balíčku. Tento prostředek poskytuje žádný způsob, jak zjistit ID balíčku. Místo toho klienta předpokládá, že je už znáte ID požadované balíčku. K dispozici metadata o jednotlivých verzí balíčků se liší podle implementaci serveru. Objekty BLOB registrační balíček mají následující hierarchickou strukturu:

- **Index**: vstupní bod pro metadata balíčků, sdílí všech balíčků ve zdroji se stejným ID balíčku.
- **Stránka**: seskupení verze balíčku. Číslo verze balíčku na stránce je definován implementací serveru.
- **Listu**: dokument specifické pro verzi jednoho balíčku.

Adresa URL registrace indexu je předvídatelný a se dají určit pomocí klienta, ID balíčku a registrace prostředků `@id` hodnotu z indexu služby. Zjištění adresy URL stránky registrace a nechá zkontrolováním index registrace.

### <a name="registration-pages-and-leaves"></a>Registrační stránky a ponechá

I když ho má není nezbytně nutné pro implementaci serveru pro ukládání, že registrace listy v samostatných registrací stránky dokumentů, je doporučený postup pro konzervaci paměti na straně klienta. Místo vkládání všechny registrace ponechá v indexu nebo okamžitě ukládání listy v dokumentech stránky, doporučuje se, že implementaci serveru definovat některé heuristiku k výběru mezi dva přístupy na základě čísla verze balíčku nebo Celková velikost balíčku opustí.

Ukládání všech verzí balíčku (listy) v indexu uloží registrace na počet požadavků HTTP potřebné k načtení metadat balíčku, ale znamená, že větší dokumentu je nutné stáhnout a větší množství paměti klienta se musí přidělovat. Na druhé straně pokud registrace ponechá implementaci serveru okamžitě ukládá v dokumentech zvláštní stránce, klient musí provést další požadavky HTTP, chcete-li získat informace, které potřebuje.

Heuristiky, který používá nuget.org je následující: Pokud je 128 nebo více verzí balíčku, rozdělit listy na stránky o velikosti 64. Pokud jsou menší než 128 verze, ponechá všechny vložené do indexu registrace.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>Parametry žádosti

Name     | V     | type    | Požadováno | Poznámky
-------- | ------ | ------- | -------- | -----
LOWER_ID | Adresa URL    | odkazy řetězců  | ano      | ID balíčku, psané malými písmeny

`LOWER_ID` Hodnotu ID požadovaný balíček psané malými písmeny pomocí pravidel implementované. NET společnosti [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) metody.

### <a name="response"></a>Odpověď

Odpověď je dokument JSON, který má kořenový objekt s následujícími vlastnostmi:

Name  | type             | Požadováno | Poznámky
----- | ---------------- | -------- | -----
count | integer          | ano      | Počet stránek registrace v indexu
items | Pole objektů | ano      | Pole registrační stránky

Každou položku v indexu objektu `items` pole je objekt JSON představující registrační stránku.

#### <a name="registration-page-object"></a>Registrace objektu page

Registrace objektu stránku v indexu registrace má následující vlastnosti:

Name   | type             | Požadováno | Poznámky
------ | ---------------- | -------- | -----
@id    | odkazy řetězců           | ano      | Adresa URL na registrační stránku
count  | integer          | ano      | Číslo registrace ponechá na stránce
items  | Pole objektů | Ne       | Pole registrace ponechá a jejich přidružených metadat
Nižší  | odkazy řetězců           | ano      | Nejnižší verze SemVer 2.0.0 na stránce (včetně)
Nadřazené | odkazy řetězců           | Ne       | Adresa URL pro registraci indexu
horní  | odkazy řetězců           | ano      | Nejvyšší verze SemVer 2.0.0 na stránce (včetně)

`lower` a `upper` hranice objektu page jsou užitečné v případě potřeby metadata pro konkrétní stránka verze.
Tyto hranice je možné načíst pouze registrační stránku potřeby. Řetězce verze dodržovat [pravidla verze Nugetu](../reference/package-versioning.md). Řetězce verze jsou normalizovány a nemusí obsahovat metadata sestavení. Jak se všemi verzemi v ekosystému NuGet porovnání řetězce verze je implementováno pomocí [pravidla priorit verze SemVer 2.0.0's](http://semver.org/spec/v2.0.0.html#spec-item-11).

`parent` Vlastnost se zobrazí, pouze pokud má objekt stránky registrace `items` vlastnost.

Pokud `items` vlastnost není k dispozici v objektu page registrace, adresa URL zadaná v `@id` musí slouží k načtení metadat o nějakém balíčku verze. `items` Pole je někdy vyloučen z objektu page rámci optimalizace. Pokud je velmi velký počet verzí a ID jeden balíček, registrace dokumentu indexu budou obrovskými a plýtvání proces pro klienta, který pouze dbá na konkrétní verzi, nebo malých rozsah verzí.

Všimněte si, že pokud `items` vlastnost je k dispozici, `@id` vlastnost nemusí použít, protože všechna data stránky, která je již vložená v `items` vlastnost.

Každá položka v objektu page `items` pole je objekt JSON představující typu registrace a její přidružené metadat.

#### <a name="registration-leaf-object-in-a-page"></a>Registrace listové objekty na stránce

Registrace objektu typu list najít na stránce registrace má následující vlastnosti:

Name           | type   | Požadováno | Poznámky
-------------- | ------ | -------- | -----
@id            | odkazy řetězců | ano      | Adresa URL pro registraci typu list
catalogEntry   | odkazy objektů | ano      | Položka katalogu obsahující metadata balíčků
packageContent | odkazy řetězců | ano      | Adresa URL pro obsah balíčku (.nupkg)

Každý registrace typu list objekt představuje data související s verzí jednoho balíčku.

#### <a name="catalog-entry"></a>Položka katalogu

`catalogEntry` Vlastnost v objektu typu list registrace má následující vlastnosti:

Name                     | type                       | Požadováno | Poznámky
------------------------ | -------------------------- | -------- | -----
@id                      | odkazy řetězců                     | ano      | Adresa URL pro dokument použitý k vytvoření tohoto objektu
Autoři                  | řetězec nebo pole řetězců | Ne       | 
dependencyGroups         | Pole objektů           | Ne       | Závislosti balíčků, seskupených podle cílové rozhraní framework
Vyřazení              | odkazy objektů                     | Ne       | Vyřazení přidružené k balíčku
description              | odkazy řetězců                     | Ne       | 
iconUrl                  | odkazy řetězců                     | Ne       | 
id                       | odkazy řetězců                     | ano      | ID balíčku
licenseUrl               | odkazy řetězců                     | Ne       |
licenseExpression        | odkazy řetězců                     | Ne       | 
uvedené v seznamu                   | Logická hodnota                    | Ne       | By měly být považovány za uvedené if chybí
minClientVersion         | odkazy řetězců                     | Ne       | 
projectUrl               | odkazy řetězců                     | Ne       | 
Publikování                | odkazy řetězců                     | Ne       | Řetězec obsahující časové razítko ISO 8601 z při publikování balíčku
requireLicenseAcceptance | Logická hodnota                    | Ne       | 
souhrn                  | odkazy řetězců                     | Ne       | 
značky                     | řetězec nebo pole řetězců  | Ne       | 
název                    | odkazy řetězců                     | Ne       | 
verze                  | odkazy řetězců                     | ano      | Plná verze řetězce po normalizace

Balíček `version` vlastnost po normalizace řetězce plnou verzi. To znamená, že data SemVer 2.0.0 sestavení může být součástí tady.

`dependencyGroups` Vlastnost je pole objektů představujících závislosti balíčků, seskupených podle cílové rozhraní. Pokud balíček nemá žádné závislosti `dependencyGroups` vlastnost chybí, prázdné pole, nebo `dependencies` vlastnosti všech skupin je prázdná nebo chybí.

Hodnota `licenseExpression` vlastnost v souladu s [syntaxe výrazu licence NuGet](https://docs.microsoft.com/en-us/nuget/reference/nuspec#license).

#### <a name="package-dependency-group"></a>Skupina závislostí balíčku

Každý objekt skupiny závislosti má následující vlastnosti:

Name            | type             | Požadováno | Poznámky
--------------- | ---------------- | -------- | -----
targetFramework | odkazy řetězců           | Ne       | Cílová architektura, která se vztahují na tyto závislosti
závislosti    | Pole objektů | Ne       |

`targetFramework` Řetězec ve formátu implementované knihovny .NET NuGet [NuGet.Frameworks](https://www.nuget.org/packages/NuGet.Frameworks/). Pokud ne `targetFramework` určena skupina závislostí se vztahuje na všechny cílové architektury.

`dependencies` Vlastnost je pole objektů, z nichž každý představuje závislost balíčku aktuálního balíčku.

#### <a name="package-dependency"></a>Závislost balíčku

Každá závislost balíčku má následující vlastnosti:

Name         | type   | Požadováno | Poznámky
------------ | ------ | -------- | -----
id           | odkazy řetězců | ano      | ID závislosti balíčků
range        | odkazy objektů | Ne       | Povolených [rozsah verzí](../reference/package-versioning.md#version-ranges-and-wildcards) závislosti
registrace | odkazy řetězců | Ne       | Adresa URL pro registraci index pro tuto závislost

Pokud `range` vyloučené vlastnost nebo prázdný řetězec, klient by měl jako výchozí rozsah verzí `(, )`. To znamená je povolené všechny verze závislosti.

#### <a name="package-deprecation"></a>Odstranění balíčku

Vyřazení každý balíček má následující vlastnosti:

Name             | type             | Požadováno | Poznámky
---------------- | ---------------- | -------- | -----
důvody          | pole řetězců | ano      | Z důvodů, proč se přestala nabízet balíčku
zpráva          | odkazy řetězců           | Ne       | Další podrobnosti o tomto vyřazení
alternatePackage | odkazy objektů           | Ne       | Závislost balíčku, který se má použít místo toho

`reasons` Vlastností musí obsahovat alespoň jeden řetězec a by měl obsahovat pouze řetězce z následující tabulky:

Důvod       | Popis             
------------ | -----------
Starší verze       | Balíček se již neudržuje
CriticalBugs | Balíček obsahuje chyby, které vhodný pro použití
Ostatní        | Balíček je zastaralý z důvodu není v tomto seznamu

Pokud `reasons` vlastnost obsahuje řetězce, které nejsou ze sady známá, mají se ignorovat. Řetězce jsou malá a velká písmena, takže `legacy` by měl být stejné považován `Legacy`. Neexistuje žádné pořadí omezení pole, tak řetězce můžete uspořádat v libovolném libovolného pořadí. Kromě toho pokud vlastnost obsahuje pouze řetězce, které nejsou ze sady známé, ji by měl být zpracován jako obsahoval pouze "Other" řetězec.

### <a name="sample-request"></a>Ukázková žádost

    GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json

### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

V tomto konkrétním případě registrace indexu je vložená registrační stránku tak k načtení metadat o nějakém balíčku verze nejsou potřeba žádné další požadavky.

## <a name="registration-page"></a>Stránka pro registraci do

Na registrační stránku obsahuje listy registrace. Adresu URL pro načtení stránky registrace závisí `@id` vlastnost v [objektu page registrace](#registration-page-object) uvedených výše.

Když `items` pole není k dispozici v indexu registrace, požadavek HTTP GET ze `@id` hodnotu vrátí dokument JSON, který má jako jeho kořenový objekt. Objekt má následující vlastnosti:

Name   | type             | Požadováno | Poznámky
------ | ---------------- | -------- | -----
@id    | odkazy řetězců           | ano      | Adresa URL na registrační stránku
count  | integer          | ano      | Číslo registrace ponechá na stránce
items  | Pole objektů | ano      | Pole registrace ponechá a jejich přidružených metadat
Nižší  | odkazy řetězců           | ano      | Nejnižší verze SemVer 2.0.0 na stránce (včetně)
Nadřazené | odkazy řetězců           | ano      | Adresa URL pro registraci indexu
horní  | odkazy řetězců           | ano      | Nejvyšší verze SemVer 2.0.0 na stránce (včetně)

Tvar listové objekty registrace je stejné jako index registrace [nad](#registration-leaf-object-in-a-page).

## <a name="sample-request"></a>Ukázková žádost

    GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json

## <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>Registrace typu list

Registrace typu list obsahuje informace o konkrétní ID a verzi. Metadata o konkrétní verzi nemusí být k dispozici v tomto dokumentu. Metadata balíčku by měla být získána z [registrace index](#registration-index) nebo [registrační stránku](#registration-page) (což je zjištěným pomocí indexu registrace).

Adresa URL pro načtení typu registrace se získávají z `@id` vlastnosti objektu typu list registrace v registraci index nebo stránce pro registraci.

Registrace typu list je dokument JSON s kořenovým objektem s následujícími vlastnostmi:

Name           | type    | Požadováno | Poznámky
-------------- | ------- | -------- | -----
@id            | odkazy řetězců  | ano      | Adresa URL pro registraci typu list
catalogEntry   | odkazy řetězců  | Ne       | Adresa URL položek katalogu, který vytvořil tyto typu list
uvedené v seznamu         | Logická hodnota | Ne       | By měly být považovány za uvedené if chybí
packageContent | odkazy řetězců  | Ne       | Adresa URL pro obsah balíčku (.nupkg)
Publikování      | odkazy řetězců  | Ne       | Řetězec obsahující časové razítko ISO 8601 z při publikování balíčku
registrace   | odkazy řetězců  | Ne       | Adresa URL pro registraci indexu

> [!Note]
> Na nuget.org `published` hodnotu roku 1900, pokud je balíček neuvedené v seznamu.

### <a name="sample-request"></a>Ukázková žádost

    GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json

### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
