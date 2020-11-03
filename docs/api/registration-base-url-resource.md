---
title: Metadata balíčku, API NuGet
description: Základní adresa URL pro registraci balíčku umožňuje načítat metadata o balíčcích.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 852dca8c70b09d941e844b1f7cd03b38e2192481
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237520"
---
# <a name="package-metadata"></a>Metadata balíčků

Je možné načíst metadata o balíčcích dostupných ve zdroji balíčku pomocí rozhraní NuGet V3 API. Tato metadata lze načíst pomocí prostředku, který `RegistrationsBaseUrl` najdete v [indexu služby](service-index.md).

Kolekce dokumentů, které se nacházejí v části `RegistrationsBaseUrl` , se často nazývají "registrace" nebo "objekty blob registrace". Sada dokumentů na jednom z nich `RegistrationsBaseUrl` se označuje jako registrační podregistr. Registrační podregistr obsahuje všechna metadata o každém balíčku, který je k dispozici ve zdroji balíčku.

## <a name="versioning"></a>Správa verzí

Použijí se tyto `@type` hodnoty:

@type osa                     | Poznámky
------------------------------- | -----
RegistrationsBaseUrl            | Počáteční verze
RegistrationsBaseUrl/3.0.0 – beta | Alias pro `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.0.0 – RC   | Alias pro `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.4.0      | Komprimovaný jako gzip odpovědi
RegistrationsBaseUrl/3.6.0      | Zahrnuje balíčky 2.0.0 pro SemVer

To představuje tři samostatné registrační podregistry, které jsou k dispozici pro různé verze klienta.

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

Tyto registrace nejsou komprimovány (což znamená, že používají implicitní `Content-Encoding: identity` ). Z tohoto podregistru jsou **vyloučeny** balíčky 2.0.0 SemVer.

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4.0

Tyto registrace se komprimují pomocí `Content-Encoding: gzip` . Z tohoto podregistru jsou **vyloučeny** balíčky 2.0.0 SemVer.

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6.0

Tyto registrace se komprimují pomocí `Content-Encoding: gzip` . V tomto podregistru jsou **zahrnuté** balíčky 2.0.0 SemVer.
Další informace o SemVer 2.0.0 najdete v tématu [Podpora SemVer 2.0.0 pro NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29).

## <a name="base-url"></a>Základní adresa URL

Základní adresa URL následujících rozhraní API je hodnota `@id` vlastnosti přidružené k výše uvedeným `@type` hodnotám prostředku. V následujícím dokumentu se použije zástupná základní adresa URL `{@id}` .

## <a name="http-methods"></a>Metody HTTP

Všechny adresy URL nalezené v registračním prostředku podporují metody HTTP `GET` a `HEAD` .

## <a name="registration-index"></a>Registrační index

Prostředek registrace seskupuje metadata balíčku podle ID balíčku. Nemůžete najednou získat data o více než jednom ID balíčku. Tento prostředek neposkytuje žádný způsob, jak zjišťovat ID balíčků. Místo toho se předpokládá, že je u klienta již známo ID požadovaného balíčku. Dostupná metadata týkající se jednotlivých verzí balíčků se liší podle implementace serveru. Objekty blob pro registraci balíčků mají následující hierarchickou strukturu:

- **Index** : vstupní bod pro metadata balíčku, který sdílí všechny balíčky na zdroji se stejným ID balíčku.
- **Stránka** : seskupení verzí balíčku. Počet verzí balíčku na stránce je definován implementací serveru.
- **List** : dokument určený pro jednu verzi balíčku.

Adresa URL registračního indexu je předvídatelné a může být určena klientem pro ID balíčku a hodnotu prostředku registrace `@id` z indexu služby. Adresy URL registračních stránek a listů jsou zjištěny kontrolou registračního indexu.

### <a name="registration-pages-and-leaves"></a>Registrační stránky a listy

Ačkoli není bezpodmínečně nutné, aby implementace serveru ukládala registrační listy v samostatných dokumentech registrační stránky, je doporučený postup pro zachování paměti na straně klienta. Místo zaznamenání veškeré registrace opustí index nebo okamžitě uloží listy do stránkovacích dokumentů. doporučuje se, aby implementace serveru definovala určitou heuristickou dobu, kterou si můžete vybrat mezi dvěma přístupy na základě počtu verzí balíčků nebo vynechání kumulativní velikosti balíčku.

Uložení všech verzí balíčku (opustí) v registračním indexu šetří počet požadavků HTTP potřebných k načtení metadat balíčku, ale znamená, že je nutné stáhnout větší dokument a musí být přidělena více klientských paměti. Na druhé straně, pokud implementace serveru hned ukládá registraci v samostatných dokumentech stránky, klient musí provést další požadavky HTTP, aby získal informace, které potřebuje.

Tato heuristická metoda, kterou používá nuget.org, je následující: Pokud jsou k dispozici 128 nebo více verzí balíčku, přerušte listy na velikost 64. Pokud jsou k dispozici méně než 128 verzí, všechny zůstanou vloženy do registračního indexu. To znamená, že balíčky s 65 až 127 verze budou mít dvě stránky v indexu, ale obě stránky budou vloženy.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>Parametry žádosti

Název     | V     | Typ    | Vyžadováno | Poznámky
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | řetězec  | ano      | ID balíčku, malými písmeny

`LOWER_ID`Hodnota je ID požadovaného balíčku s malými písmeny pomocí pravidel implementovaných pomocí. Metoda netto [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) .

### <a name="response"></a>Odpověď

Odpověď je dokument JSON, který má kořenový objekt s následujícími vlastnostmi:

Název  | Typ             | Vyžadováno | Poznámky
----- | ---------------- | -------- | -----
count | integer          | ano      | Počet registračních stránek v indexu
položek | pole objektů | ano      | Pole registračních stránek

Každá položka v poli objektu index `items` je objekt JSON, který představuje registrační stránku.

#### <a name="registration-page-object"></a>Registrační objekt stránky

Registrační objekt stránky, který se našel v registračním indexu, má tyto vlastnosti:

Název   | Typ             | Vyžadováno | Poznámky
------ | ---------------- | -------- | -----
@id    | řetězec           | ano      | Adresa URL stránky pro registraci
count  | integer          | ano      | Počet ponechání registrace na stránce
položek  | pole objektů | ne       | Pole registrace opustí a jejich přidružená metadata
malým  | řetězec           | ano      | Nejnižší verze SemVer 2.0.0 na stránce (včetně)
nadřazený | řetězec           | ne       | Adresa URL indexu registrace
umístit  | řetězec           | ano      | Nejvyšší verze SemVer 2.0.0 na stránce (včetně)

`lower` `upper` Meze objektů stránky a jsou užitečné v případě, že je potřeba metadata pro konkrétní verzi stránky.
Tyto hranice lze použít k načtení jediné registrační stránky, kterou potřebujete. Řetězce verze vyhovují [pravidlům verzí NuGet](../concepts/package-versioning.md). Řetězce verze jsou normalizovány a neobsahují metadata sestavení. Stejně jako u všech verzí v ekosystému NuGet se porovnání řetězců verzí implementuje pomocí [pravidel priority verze SemVer 2.0.0](https://semver.org/spec/v2.0.0.html#spec-item-11).

`parent`Vlastnost se zobrazí pouze v případě, že objekt registrační stránky má `items` vlastnost.

Pokud vlastnost není k `items` dispozici v objektu registrační stránky, adresa URL zadaná v rozhraní `@id` musí být použita k načtení metadat o jednotlivých verzích balíčků. `items`Pole je někdy vyloučeno z objektu Page jako optimalizace. Pokud je počet verzí jednoho balíčku moc velký, pak bude dokument indexu registrace obrovský a wasteful se na zpracování pro klienta, který stojí jenom na konkrétní verzi nebo malý rozsah verzí.

Všimněte si, že pokud `items` je vlastnost přítomna, `@id` není nutné použít vlastnost, protože všechna data stránky jsou již vložena do `items` Vlastnosti.

Každá položka v poli objektu stránky `items` je objekt JSON, který představuje registrační list a má přidružená metadata.

#### <a name="registration-leaf-object-in-a-page"></a>Registrační listový objekt na stránce

Registrační objekt na listu, který se našel na registrační stránce, má tyto vlastnosti:

Název           | Typ   | Vyžadováno | Poznámky
-------------- | ------ | -------- | -----
@id            | řetězec | ano      | Adresa URL listu registrace
catalogEntry   | object | ano      | Záznam katalogu obsahující metadata balíčku
packageContent | řetězec | ano      | Adresa URL obsahu balíčku (. nupkg)

Každý registrační listový objekt představuje data přidružená k jedné verzi balíčku.

#### <a name="catalog-entry"></a>Záznam v katalogu

`catalogEntry`Vlastnost v objektu registračního listu má následující vlastnosti:

Název                     | Typ                       | Vyžadováno | Poznámky
------------------------ | -------------------------- | -------- | -----
@id                      | řetězec                     | ano      | Adresa URL dokumentu použitého k vyprodukování tohoto objektu
Autoři                  | řetězec nebo pole řetězců | ne       | 
dependencyGroups         | pole objektů           | ne       | Závislosti balíčku seskupené podle cílové architektury
vyřazení              | object                     | ne       | Zastaralé přidružení k balíčku
description              | řetězec                     | ne       | 
iconUrl                  | řetězec                     | ne       | 
id                       | řetězec                     | ano      | ID balíčku
licenseUrl               | řetězec                     | ne       |
licenseExpression        | řetězec                     | ne       | 
uvedené v seznamu                   | boolean                    | ne       | By mělo být považováno za uvedené, pokud chybí
minClientVersion         | řetězec                     | ne       | 
projectUrl               | řetězec                     | ne       | 
zveřejněna                | řetězec                     | ne       | Řetězec obsahující časové razítko ISO 8601 při publikování balíčku
requireLicenseAcceptance | boolean                    | ne       | 
shrnutí                  | řetězec                     | ne       | 
tags                     | řetězec nebo pole řetězce  | ne       | 
title                    | řetězec                     | ne       | 
verze                  | řetězec                     | ano      | Úplný řetězec verze po normalizaci

Vlastnost Package `version` je úplný řetězec verze po normalizaci. To znamená, že sem můžete zahrnout data sestavení SemVer 2.0.0.

`dependencyGroups`Vlastnost je pole objektů reprezentující závislosti balíčku seskupené podle cílové architektury. Pokud balíček nemá žádné závislosti, `dependencyGroups` vlastnost chybí, prázdné pole nebo `dependencies` vlastnost všech skupin jsou prázdné nebo chybí.

Hodnota vlastnosti je v `licenseExpression` souladu s [syntaxí multilicenčního výrazu NuGet](../reference/nuspec.md#license).

> [!Note]
> V nuget.org `published` je hodnota nastavena na rok 1900, pokud je balíček neuvedený.

#### <a name="package-dependency-group"></a>Skupina závislostí balíčku

Každý objekt skupiny závislostí má následující vlastnosti:

Název            | Typ             | Vyžadováno | Poznámky
--------------- | ---------------- | -------- | -----
targetFramework | řetězec           | ne       | Cílové rozhraní .NET Framework, na které se tyto závislosti vztahují
závislosti    | pole objektů | ne       |

`targetFramework`Řetězec používá formát implementovaný rozhraním NuGet knihovny .NET pro NuGet [. architektury](https://www.nuget.org/packages/NuGet.Frameworks/). Pokud `targetFramework` není zadaný, použije se skupina závislostí na všechny cílové architektury.

`dependencies`Vlastnost je pole objektů, z nichž každý představuje závislost balíčku aktuálního balíčku.

#### <a name="package-dependency"></a>Závislost balíčku

Jednotlivé závislosti balíčků mají následující vlastnosti:

Název         | Typ   | Vyžadováno | Poznámky
------------ | ------ | -------- | -----
id           | řetězec | ano      | ID závislosti balíčku
range        | object | ne       | Povolený [rozsah verzí](../concepts/package-versioning.md#version-ranges) závislosti
registrace | řetězec | ne       | Adresa URL indexu registrace pro tuto závislost

Pokud `range` je vlastnost vyloučená nebo je prázdným řetězcem, měl by být ve výchozím nastavení povolený rozsah verzí klienta `(, )` . To znamená, že je povolená jakákoli verze závislosti. Hodnota `*` není pro `range` vlastnost povolena.

#### <a name="package-deprecation"></a>Vyřazení balíčku

Každý zastaralý balíček má následující vlastnosti:

Název             | Typ             | Vyžadováno | Poznámky
---------------- | ---------------- | -------- | -----
hlediska          | pole řetězců | ano      | Důvody, proč byl balíček zastaralý
zpráva          | řetězec           | ne       | Další podrobnosti o této zastaralosti
alternatePackage | object           | ne       | Alternativní balíček, který se má použít místo toho

`reasons`Vlastnost musí obsahovat alespoň jeden řetězec a měla by obsahovat pouze řetězce z následující tabulky:

Důvod       | Popis             
------------ | -----------
Starší verze       | Balíček se už neudržuje.
CriticalBugs | Balíček obsahuje chyby, které nejsou vhodné pro použití.
Ostatní        | Balíček je zastaralý z důvodu, že tento seznam není v tomto seznamu.

Pokud `reasons` vlastnost obsahuje řetězce, které nejsou ze známé sady, měly by být ignorovány. V řetězcích nejsou rozlišována velká a malá písmena, proto `legacy` by měla být zpracována stejně jako `Legacy` . V poli není žádné omezení řazení, takže řetězce mohou být uspořádány do libovolného pořadí. Kromě toho, pokud vlastnost obsahuje pouze řetězce, které nejsou ze známé sady, měla by být zpracována, jako by obsahovala pouze řetězec "other".

#### <a name="alternate-package"></a>Alternativní balíček

Objekt alternativního balíčku má následující vlastnosti:

Název         | Typ   | Vyžadováno | Poznámky
------------ | ------ | -------- | -----
id           | řetězec | ano      | ID alternativního balíčku
range        | object | ne       | Povolený [rozsah verzí](../concepts/package-versioning.md#version-ranges), nebo `*` Pokud je povolená nějaká verze

### <a name="sample-request"></a>Ukázková žádost

    GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json

### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

V tomto konkrétním případě registrační index má registrační stránku vloženě, takže nepotřebujete žádné další požadavky k načtení metadat pro jednotlivé verze balíčků.

## <a name="registration-page"></a>Registrační stránka

Registrační stránka obsahuje ponechání registračních stránek. Adresa URL pro načtení registrační stránky je určena `@id` vlastností ve výše uvedeném [objektu registrační stránky](#registration-page-object) . Adresa URL nemá být předvídatelná a měla by být vždy zjištěna prostřednictvím dokumentu indexu.

> [!Warning]
> V nuget.org Adresa URL dokumentu registrační stránky obsahuje dolní a horní mez stránky. Tento předpoklad by však neměl být klientem nikdy proveden, protože implementace serveru jsou volné, aby bylo možné změnit tvar adresy URL, pokud má dokument indexu platný odkaz.

Pokud `items` pole není v registračním indexu k dispozici, vrátí požadavek HTTP GET na `@id` hodnotu dokument JSON, který má objekt jako svůj kořenový adresář. Objekt má následující vlastnosti:

Název   | Typ             | Vyžadováno | Poznámky
------ | ---------------- | -------- | -----
@id    | řetězec           | ano      | Adresa URL stránky pro registraci
count  | integer          | ano      | Počet ponechání registrace na stránce
položek  | pole objektů | ano      | Pole registrace opustí a jejich přidružená metadata
malým  | řetězec           | ano      | Nejnižší verze SemVer 2.0.0 na stránce (včetně)
nadřazený | řetězec           | ano      | Adresa URL indexu registrace
umístit  | řetězec           | ano      | Nejvyšší verze SemVer 2.0.0 na stránce (včetně)

Tvar listů registračních objektů je stejný jako v indexu registrace [výše](#registration-leaf-object-in-a-page).

## <a name="sample-request"></a>Ukázková žádost

    GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json

## <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>Registrační list

Registrační list obsahuje informace o konkrétním ID a verzi balíčku. Metadata týkající se konkrétní verze nemusí být v tomto dokumentu k dispozici. Metadata balíčku by se měla načíst z registračního [indexu](#registration-index) nebo [registrační stránky](#registration-page) (která se zjistila pomocí registračního indexu).

Adresa URL pro načtení registračního listu je získána z `@id` vlastnosti registračního objektu listu v registračním indexu nebo na registrační stránce. Stejně jako u dokumentu stránky. Adresa URL nemá být předvídatelná a měla by být vždy zjištěna prostřednictvím objektu registrační stránky.

> [!Warning]
> V nuget.org Adresa URL pro tento dokument registračního listu obsahuje verzi balíčku. Tento předpoklad by však neměl být klientem nikdy proveden, protože implementace serveru jsou volné, aby bylo možné změnit tvar adresy URL, pokud má nadřazený dokument platný odkaz. 

Registrační list je dokument JSON s kořenovým objektem s následujícími vlastnostmi:

Název           | Typ    | Vyžadováno | Poznámky
-------------- | ------- | -------- | -----
@id            | řetězec  | ano      | Adresa URL listu registrace
catalogEntry   | řetězec  | ne       | Adresa URL položky katalogu, která vytvořila tento list
uvedené v seznamu         | boolean | ne       | By mělo být považováno za uvedené, pokud chybí
packageContent | řetězec  | ne       | Adresa URL obsahu balíčku (. nupkg)
zveřejněna      | řetězec  | ne       | Řetězec obsahující časové razítko ISO 8601 při publikování balíčku
registrace   | řetězec  | ne       | Adresa URL indexu registrace

> [!Note]
> V nuget.org `published` je hodnota nastavena na rok 1900, pokud je balíček neuvedený.

### <a name="sample-request"></a>Ukázková žádost

    GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json

### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
