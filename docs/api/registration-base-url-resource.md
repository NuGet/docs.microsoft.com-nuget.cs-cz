---
title: Metadata balíčku, API NuGet
description: Základní adresa URL pro registraci balíčku umožňuje načítat metadata o balíčcích.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 852dca8c70b09d941e844b1f7cd03b38e2192481
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230877"
---
# <a name="package-metadata"></a>Metadata balíčků

Je možné načíst metadata o balíčcích dostupných ve zdroji balíčku pomocí rozhraní NuGet V3 API. Tato metadata lze načíst pomocí `RegistrationsBaseUrl` prostředku, který najdete v [indexu služby](service-index.md).

Kolekce dokumentů nalezených v rámci `RegistrationsBaseUrl` se často nazývají "registrace" nebo "objekty blob registrace". Sada dokumentů v rámci jednoho `RegistrationsBaseUrl` je označována jako "registrační podregistr". Registrační podregistr obsahuje všechna metadata o každém balíčku, který je k dispozici ve zdroji balíčku.

## <a name="versioning"></a>Správa verzí

Použijí se následující hodnoty `@type`:

hodnota @type                     | Poznámky:
------------------------------- | -----
RegistrationsBaseUrl            | Počáteční verze
RegistrationsBaseUrl/3.0.0 – beta | Alias `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.0.0 – RC   | Alias `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.4.0      | Komprimovaný jako gzip odpovědi
RegistrationsBaseUrl/3.6.0      | Zahrnuje balíčky 2.0.0 pro SemVer

To představuje tři samostatné registrační podregistry, které jsou k dispozici pro různé verze klienta.

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

Tyto registrace nejsou komprimovány (což znamená, že používají implicitní `Content-Encoding: identity`). Z tohoto podregistru jsou **vyloučeny** balíčky 2.0.0 SemVer.

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4.0

Tyto registrace se komprimují pomocí `Content-Encoding: gzip`. Z tohoto podregistru jsou **vyloučeny** balíčky 2.0.0 SemVer.

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6.0

Tyto registrace se komprimují pomocí `Content-Encoding: gzip`. V tomto podregistru jsou **zahrnuté** balíčky 2.0.0 SemVer.
Další informace o SemVer 2.0.0 najdete v tématu [Podpora SemVer 2.0.0 pro NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29).

## <a name="base-url"></a>Základní adresa URL

Základní adresa URL následujících rozhraní API je hodnota vlastnosti `@id` přidružená k výše uvedeným `@type`m hodnotám prostředku. V následujícím dokumentu se použije základní adresa URL pro zástupné znaky `{@id}`.

## <a name="http-methods"></a>Metody HTTP

Všechny adresy URL nalezené v registračním prostředku podporují metody HTTP `GET` a `HEAD`.

## <a name="registration-index"></a>Registrační index

Prostředek registrace seskupuje metadata balíčku podle ID balíčku. Nemůžete najednou získat data o více než jednom ID balíčku. Tento prostředek neposkytuje žádný způsob, jak zjišťovat ID balíčků. Místo toho se předpokládá, že je u klienta již známo ID požadovaného balíčku. Dostupná metadata týkající se jednotlivých verzí balíčků se liší podle implementace serveru. Objekty blob pro registraci balíčků mají následující hierarchickou strukturu:

- **Index**: vstupní bod pro metadata balíčku, který sdílí všechny balíčky na zdroji se stejným ID balíčku.
- **Stránka**: seskupení verzí balíčku. Počet verzí balíčku na stránce je definován implementací serveru.
- **List**: dokument určený pro jednu verzi balíčku.

Adresa URL registračního indexu je předvídatelné a může být určena klientem pro ID balíčku a hodnotu `@id` prostředku registrace z indexu služby. Adresy URL registračních stránek a listů jsou zjištěny kontrolou registračního indexu.

### <a name="registration-pages-and-leaves"></a>Registrační stránky a listy

Ačkoli není bezpodmínečně nutné, aby implementace serveru ukládala registrační listy v samostatných dokumentech registrační stránky, je doporučený postup pro zachování paměti na straně klienta. Místo vložení všech registračních ponechá v indexu nebo okamžitě uloží listy do stránkovacích dokumentů, doporučuje se, aby implementace serveru definovala určitou heuristickou volbu mezi oběma přístupy na základě počtu verzí balíčku nebo vynechává se kumulativní velikost balíčku.

Uložení všech verzí balíčku (opustí) v registračním indexu šetří počet požadavků HTTP potřebných k načtení metadat balíčku, ale znamená, že je nutné stáhnout větší dokument a musí být přidělena více klientských paměti. Na druhé straně, pokud implementace serveru hned ukládá registraci v samostatných dokumentech stránky, klient musí provést další požadavky HTTP, aby získal informace, které potřebuje.

Tato heuristická metoda, kterou používá nuget.org, je následující: Pokud jsou k dispozici 128 nebo více verzí balíčku, přerušte listy na velikost 64. Pokud jsou k dispozici méně než 128 verzí, všechny zůstanou vloženy do registračního indexu. To znamená, že balíčky s 65 až 127 verze budou mít dvě stránky v indexu, ale obě stránky budou vloženy.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>Parametry žádosti

Název     | V     | Typ    | Požadováno | Poznámky:
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | string  | ano      | ID balíčku, malými písmeny

Hodnota `LOWER_ID` je ID požadovaného balíčku s malými písmeny pomocí pravidel implementovaných nástrojem. Metoda [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) sítě

### <a name="response"></a>Odpověď

Odpověď je dokument JSON, který má kořenový objekt s následujícími vlastnostmi:

Název  | Typ             | Požadováno | Poznámky:
----- | ---------------- | -------- | -----
count | celé číslo          | ano      | Počet registračních stránek v indexu
položky | pole objektů | ano      | Pole registračních stránek

Každá položka v `items` poli objektu index je objekt JSON, který představuje registrační stránku.

#### <a name="registration-page-object"></a>Registrační objekt stránky

Registrační objekt stránky, který se našel v registračním indexu, má tyto vlastnosti:

Název   | Typ             | Požadováno | Poznámky:
------ | ---------------- | -------- | -----
@id    | string           | ano      | Adresa URL stránky pro registraci
count  | celé číslo          | ano      | Počet ponechání registrace na stránce
položky  | pole objektů | ne       | Pole registrace opustí a jejich přidružená metadata
Malým  | string           | ano      | Nejnižší verze SemVer 2.0.0 na stránce (včetně)
nadřazený | string           | ne       | Adresa URL indexu registrace
umístit  | string           | ano      | Nejvyšší verze SemVer 2.0.0 na stránce (včetně)

Hranice `lower` a `upper` objektu Page jsou užitečné v případě, že jsou požadována metadata pro konkrétní verzi stránky.
Tyto hranice lze použít k načtení jediné registrační stránky, kterou potřebujete. Řetězce verze vyhovují [pravidlům verzí NuGet](../concepts/package-versioning.md). Řetězce verze jsou normalizovány a neobsahují metadata sestavení. Stejně jako u všech verzí v ekosystému NuGet se porovnání řetězců verzí implementuje pomocí [pravidel priority verze SemVer 2.0.0](https://semver.org/spec/v2.0.0.html#spec-item-11).

Vlastnost `parent` se zobrazí pouze v případě, že objekt registrační stránky má vlastnost `items`.

Pokud není v objektu registrační stránky k dispozici vlastnost `items`, adresa URL zadaná v `@id` musí být použita k načtení metadat o jednotlivých verzích balíčků. Pole `items` je někdy vyloučeno z objektu Page jako optimalizace. Pokud je počet verzí jednoho balíčku moc velký, pak bude dokument indexu registrace obrovský a wasteful se na zpracování pro klienta, který stojí jenom na konkrétní verzi nebo malý rozsah verzí.

Všimněte si, že pokud je vlastnost `items` k dispozici, není nutné použít vlastnost `@id`, protože všechna data stránky jsou již vložena do vlastnosti `items`.

Každá položka v poli `items` objektu stránky je objekt JSON, který představuje registrační list a přidružená metadata.

#### <a name="registration-leaf-object-in-a-page"></a>Registrační listový objekt na stránce

Registrační objekt na listu, který se našel na registrační stránce, má tyto vlastnosti:

Název           | Typ   | Požadováno | Poznámky:
-------------- | ------ | -------- | -----
@id            | string | ano      | Adresa URL listu registrace
catalogEntry   | objekt | ano      | Záznam katalogu obsahující metadata balíčku
packageContent | string | ano      | Adresa URL obsahu balíčku (. nupkg)

Každý registrační listový objekt představuje data přidružená k jedné verzi balíčku.

#### <a name="catalog-entry"></a>Záznam v katalogu

Vlastnost `catalogEntry` v objektu registračního listu má následující vlastnosti:

Název                     | Typ                       | Požadováno | Poznámky:
------------------------ | -------------------------- | -------- | -----
@id                      | string                     | ano      | Adresa URL dokumentu použitého k vyprodukování tohoto objektu
Autoři                  | řetězec nebo pole řetězců | ne       | 
dependencyGroups         | pole objektů           | ne       | Závislosti balíčku seskupené podle cílové architektury
vyřazení              | objekt                     | ne       | Zastaralé přidružení k balíčku
description              | string                     | ne       | 
iconUrl                  | string                     | ne       | 
id                       | string                     | ano      | ID balíčku
licenseUrl               | string                     | ne       |
licenseExpression        | string                     | ne       | 
uvedené v seznamu                   | Boolean                    | ne       | By mělo být považováno za uvedené, pokud chybí
minClientVersion         | string                     | ne       | 
projectUrl               | string                     | ne       | 
zveřejněna                | string                     | ne       | Řetězec obsahující časové razítko ISO 8601 při publikování balíčku
requireLicenseAcceptance | Boolean                    | ne       | 
summary                  | string                     | ne       | 
značek                     | řetězec nebo pole řetězce  | ne       | 
Název                    | string                     | ne       | 
Verze nástroje                   | string                     | ano      | Úplný řetězec verze po normalizaci

Vlastnost `version` balíčku je úplný řetězec verze po normalizaci. To znamená, že sem můžete zahrnout data sestavení SemVer 2.0.0.

Vlastnost `dependencyGroups` je pole objektů reprezentující závislosti balíčku seskupené podle cílové architektury. Pokud balíček nemá žádné závislosti, chybí vlastnost `dependencyGroups`, prázdné pole nebo vlastnost `dependencies` všech skupin je prázdná nebo chybí.

Hodnota vlastnosti `licenseExpression` v souladu s [syntaxí multilicenčního výrazu NuGet](../reference/nuspec.md#license).

> [!Note]
> V nuget.org je hodnota `published` nastavena na rok 1900, pokud je balíček neuvedený.

#### <a name="package-dependency-group"></a>Skupina závislostí balíčku

Každý objekt skupiny závislostí má následující vlastnosti:

Název            | Typ             | Požadováno | Poznámky:
--------------- | ---------------- | -------- | -----
targetFramework | string           | ne       | Cílové rozhraní .NET Framework, na které se tyto závislosti vztahují
dependencies    | pole objektů | ne       |

Řetězec `targetFramework` používá formát implementovaný rozhraním NuGet knihovny .NET pro NuGet. [architektury](https://www.nuget.org/packages/NuGet.Frameworks/). Pokud není zadán žádný `targetFramework`, vztahuje se skupina závislostí na všechny cílové architektury.

Vlastnost `dependencies` je pole objektů, z nichž každý představuje závislost balíčku aktuálního balíčku.

#### <a name="package-dependency"></a>Závislost balíčku

Jednotlivé závislosti balíčků mají následující vlastnosti:

Název         | Typ   | Požadováno | Poznámky:
------------ | ------ | -------- | -----
id           | string | ano      | ID závislosti balíčku
range        | objekt | ne       | Povolený [rozsah verzí](../concepts/package-versioning.md#version-ranges) závislosti
registrace | string | ne       | Adresa URL indexu registrace pro tuto závislost

Pokud je vlastnost `range` vyloučená nebo je to prázdný řetězec, měl by být ve výchozím nastavení `(, )`rozsahu verze. To znamená, že je povolená jakákoli verze závislosti. Hodnota `*` není pro vlastnost `range` povolena.

#### <a name="package-deprecation"></a>Zastaralé balíčky

Každý zastaralý balíček má následující vlastnosti:

Název             | Typ             | Požadováno | Poznámky:
---------------- | ---------------- | -------- | -----
hlediska          | pole řetězců | ano      | Důvody, proč byl balíček zastaralý
zpráva          | string           | ne       | Další podrobnosti o této zastaralosti
alternatePackage | objekt           | ne       | Alternativní balíček, který se má použít místo toho

Vlastnost `reasons` musí obsahovat alespoň jeden řetězec a měla by obsahovat pouze řetězce z následující tabulky:

Důvod       | Popis             
------------ | -----------
Starší verze       | Balíček se už neudržuje.
CriticalBugs | Balíček obsahuje chyby, které nejsou vhodné pro použití.
Další        | Balíček je zastaralý z důvodu, že tento seznam není v tomto seznamu.

Pokud vlastnost `reasons` obsahuje řetězce, které nejsou ze známé sady, měly by být ignorovány. V řetězcích nejsou rozlišována velká a malá písmena, proto by `legacy` měla být zpracována stejně jako `Legacy`. V poli není žádné omezení řazení, takže řetězce mohou být uspořádány do libovolného pořadí. Kromě toho, pokud vlastnost obsahuje pouze řetězce, které nejsou ze známé sady, měla by být zpracována, jako by obsahovala pouze řetězec "other".

#### <a name="alternate-package"></a>Alternativní balíček

Objekt alternativního balíčku má následující vlastnosti:

Název         | Typ   | Požadováno | Poznámky:
------------ | ------ | -------- | -----
id           | string | ano      | ID alternativního balíčku
range        | objekt | ne       | Povolený [rozsah verzí](../concepts/package-versioning.md#version-ranges), nebo `*`, pokud je povolená nějaká verze

### <a name="sample-request"></a>Ukázková žádost

    GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json

### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

V tomto konkrétním případě registrační index má registrační stránku vloženě, takže nepotřebujete žádné další požadavky k načtení metadat pro jednotlivé verze balíčků.

## <a name="registration-page"></a>Registrační stránka

Registrační stránka obsahuje ponechání registračních stránek. Adresa URL pro načtení registrační stránky je určena vlastností `@id` v [objektu registrační stránky](#registration-page-object) , který je uveden výše. Adresa URL nemá být předvídatelná a měla by být vždy zjištěna prostřednictvím dokumentu indexu.

> [!Warning]
> V nuget.org Adresa URL dokumentu registrační stránky obsahuje dolní a horní mez stránky. Tento předpoklad by však neměl být klientem nikdy proveden, protože implementace serveru jsou volné, aby bylo možné změnit tvar adresy URL, pokud má dokument indexu platný odkaz.

Pokud pole `items` není v registračním indexu k dispozici, požadavek HTTP GET hodnoty `@id` vrátí dokument JSON, který má objekt jako svůj kořen. Objekt má následující vlastnosti:

Název   | Typ             | Požadováno | Poznámky:
------ | ---------------- | -------- | -----
@id    | string           | ano      | Adresa URL stránky pro registraci
count  | celé číslo          | ano      | Počet ponechání registrace na stránce
položky  | pole objektů | ano      | Pole registrace opustí a jejich přidružená metadata
Malým  | string           | ano      | Nejnižší verze SemVer 2.0.0 na stránce (včetně)
nadřazený | string           | ano      | Adresa URL indexu registrace
umístit  | string           | ano      | Nejvyšší verze SemVer 2.0.0 na stránce (včetně)

Tvar listů registračních objektů je stejný jako v indexu registrace [výše](#registration-leaf-object-in-a-page).

## <a name="sample-request"></a>Ukázková žádost

    GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json

## <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>Registrační list

Registrační list obsahuje informace o konkrétním ID a verzi balíčku. Metadata týkající se konkrétní verze nemusí být v tomto dokumentu k dispozici. Metadata balíčku by se měla načíst z registračního [indexu](#registration-index) nebo [registrační stránky](#registration-page) (která se zjistila pomocí registračního indexu).

Adresa URL pro načtení registračního listu je získána z vlastnosti `@id` registračního objektu listu v registračním indexu nebo na registrační stránce. Stejně jako u dokumentu stránky. Adresa URL nemá být předvídatelná a měla by být vždy zjištěna prostřednictvím objektu registrační stránky.

> [!Warning]
> V nuget.org Adresa URL pro tento dokument registračního listu obsahuje verzi balíčku. Tento předpoklad by však neměl být klientem nikdy proveden, protože implementace serveru jsou volné, aby bylo možné změnit tvar adresy URL, pokud má nadřazený dokument platný odkaz. 

Registrační list je dokument JSON s kořenovým objektem s následujícími vlastnostmi:

Název           | Typ    | Požadováno | Poznámky:
-------------- | ------- | -------- | -----
@id            | string  | ano      | Adresa URL listu registrace
catalogEntry   | string  | ne       | Adresa URL položky katalogu, která vytvořila tento list
uvedené v seznamu         | Boolean | ne       | By mělo být považováno za uvedené, pokud chybí
packageContent | string  | ne       | Adresa URL obsahu balíčku (. nupkg)
zveřejněna      | string  | ne       | Řetězec obsahující časové razítko ISO 8601 při publikování balíčku
registrace   | string  | ne       | Adresa URL indexu registrace

> [!Note]
> V nuget.org je hodnota `published` nastavena na rok 1900, pokud je balíček neuvedený.

### <a name="sample-request"></a>Ukázková žádost

    GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json

### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
