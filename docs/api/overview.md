---
title: Přehled rozhraní API serveru NuGet
description: Rozhraní API serveru NuGet je sada koncových bodů HTTP, které je možné použít ke stažení balíčků, načítání metadat, publikování nových balíčků atd.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: aacf56a5dc5af9abf6f60d42bc7fd530a128d0d8
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428707"
---
# <a name="nuget-server-api"></a>Serverové rozhraní API pro NuGet

Rozhraní API serveru NuGet je sada koncových bodů HTTP, které je možné použít ke stažení balíčků, načítání metadat, publikování nových balíčků a provádění většiny dalších operací, které jsou k dispozici v oficiálních klientech NuGet.

Toto rozhraní API používá klient NuGet v aplikaci Visual Studio, NuGet. exe a rozhraní .NET CLI k provádění operací NuGet, jako je [`dotnet restore`](/dotnet/core/tools/dotnet-restore?tabs=netcore2x), hledání v uživatelském rozhraní sady Visual studio a [`nuget.exe push`](../reference/cli-reference/cli-ref-push.md).

Všimněte si, že v některých případech má nuget.org další požadavky, které nejsou vynutily jinými zdroji balíčků. Tyto rozdíly jsou popsány v [protokolech NuGet.org](nuget-protocols.md).

Jednoduchý výčet a stažení dostupných verzí NuGet. exe najdete v tématu koncový bod [Tools. JSON](tools-json.md) .

## <a name="service-index"></a>Index služby

Vstupním bodem pro rozhraní API je dokument JSON ve známém umístění. Tento dokument se nazývá **index služby**. Umístění indexu služby pro nuget.org je `https://api.nuget.org/v3/index.json`.

Tento dokument JSON obsahuje seznam *prostředků* , které poskytují různé funkce a splňují různé případy použití.

Klienti, kteří podporují rozhraní API, by měli přijmout jednu nebo více těchto adres URL indexu služby jako způsob připojení k příslušným zdrojům balíčků.

Další informace o indexu služby najdete v referenčních informacích k [rozhraní API](service-index.md).

## <a name="versioning"></a>Správa verzí

Rozhraní API je verze 3 protokolu HTTP NuGet. Tento protokol se někdy označuje jako "rozhraní V3 API". Tyto referenční dokumenty budou odkazovat na tuto verzi protokolu jednoduše jako rozhraní API.

Verze schématu indexu služby je označena vlastností `version` v indexu služby. Rozhraní API vyžaduje, aby měl řetězec verze hlavní číslo verze `3`. V rámci schématu indexu služby budou provedeny nepodstatné změny, ale zvýší se vedlejší verze řetězce verze.

Starší klienti (například NuGet. exe 2. x) nepodporují rozhraní V3 API a podporují jenom starší rozhraní API v2, které tady není popsané.

Rozhraní API NuGet v3 je pojmenované, protože se jedná o následníka rozhraní API v2, což byl protokol založený na OData, který implementuje verze 2. x oficiálního klienta NuGet. Verze v3 API byla poprvé podporovaná verzí 3,0 oficiálního klienta NuGet a stále je to nejnovější verze hlavního protokolu podporovaná klientem NuGet, 4,0 a na. 

V rozhraní API byly provedeny neprůlomové změny protokolu, protože byly nejprve vydány.

## <a name="resources-and-schema"></a>Prostředky a schéma

**Index služby** popisuje nejrůznější prostředky. Aktuální sada podporovaných prostředků je následující:

Název prostředku                                                        | Požaduje se | Popis
-------------------------------------------------------------------- | -------- | -----------
[Katalog](catalog-resource.md)                                       | ne       | Úplný záznam všech událostí balíčku.
[PackageBaseAddress](package-base-address-resource.md)               | ano      | Získat obsah balíčku (. nupkg)
[PackageDetailsUriTemplate](package-details-template-resource.md)    | ne       | Vytvořte adresu URL pro přístup k webové stránce s podrobnostmi o balíčku.
[PackagePublish](package-publish-resource.md)                        | ano      | Doručovat a odstraňovat (nebo odpisovat) balíčky.
[RegistrationsBaseUrl](registration-base-url-resource.md)            | ano      | Získá metadata balíčku.
[ReportAbuseUriTemplate](report-abuse-resource.md)                   | ne       | Vytvořte adresu URL pro přístup k webové stránce zneužití sestavy.
[RepositorySignatures](repository-signatures-resource.md)            | ne       | Získejte certifikáty používané k podepisování úložiště.
[SearchAutocompleteService](search-autocomplete-service-resource.md) | ne       | Vyhledat ID a verze balíčků podle podřetězce.
[SearchQueryService](search-query-service-resource.md)               | ano      | Vyfiltruje a vyhledá balíčky podle klíčového slova.
[SymbolPackagePublish](symbol-package-publish-resource.md)           | ne       | Nabízet balíčky symbolů.

Obecně platí, že všechna nebinární data vrácená prostředkem rozhraní API jsou serializovaná pomocí formátu JSON. Schéma odpovědi vrácené každým prostředkem v indexu služby je definováno individuálně pro daný prostředek. Další informace o jednotlivých prostředcích najdete v tématech uvedených výše.

V budoucnu mohou být při vývojovém protokolu přidány do odpovědí JSON nové vlastnosti. Aby klient mohl být v budoucnu, implementace by neměl předpokládat, že schéma odpovědi je finální a nemůže zahrnovat další data. Všechny vlastnosti, které implementace nerozumí, by měly být ignorovány.

> [!Note]
> Pokud zdroj neimplementuje `SearchAutocompleteService` jakékoli chování automatického dokončování by mělo být řádně zakázané. Když se `ReportAbuseUriTemplate` neimplementuje, oficiální klient NuGet se vrátí do balíčku NuGet. adresa URL pro zneužití zprávy organizace (sledována nástrojem [NuGet/Home # 4924](https://github.com/NuGet/Home/issues/4924)). Jiní klienti mohou vyjádřit výslovný neodkazování na adresu URL zneužití zprávy uživateli.

### <a name="undocumented-resources-on-nugetorg"></a>Nedokumentované prostředky v nuget.org

Index služby V3 v nuget.org obsahuje některé prostředky, které nejsou popsané výše. Existuje několik důvodů, proč nezdokumentovat prostředek.

Nejdříve nezdokumentujte prostředky použité jako podrobnosti implementace nuget.org. `SearchGalleryQueryService` spadají do této kategorie. [NuGetGallery](https://github.com/NuGet/NuGetGallery) tento prostředek používá k delegování některých dotazů v2 (OData) na náš index vyhledávání namísto použití databáze. Tento prostředek se představil z důvodu škálovatelnosti a není určený pro externí použití.

Za druhé nezdokumentujte prostředky, které se nikdy nedodaly ve verzi RTM oficiálního klienta.
do této kategorie patří `PackageDisplayMetadataUriTemplate` a `PackageVersionDisplayMetadataUriTemplate`.

V ostatních případech neuvádíme prostředky, které jsou úzce spojeny s protokolem v2, který je záměrně nedokumentovaný. Prostředek `LegacyGallery` spadá do této kategorie. Tento prostředek umožňuje, aby index služby V3 odkazoval na odpovídající zdrojovou adresu URL v2. Tento prostředek podporuje `nuget.exe list`.

Pokud zde prostředek není dokumentován, *důrazně* doporučujeme, abyste na ně nemuseli zabírat žádné závislosti. Může dojít k odstranění nebo změně chování těchto nedokumentovaných prostředků, které by mohly poškodit vaši implementaci neočekávaným způsobem.

## <a name="timestamps"></a>Časová razítka

Všechna časová razítka vrácená rozhraním API jsou UTC nebo jinak zadaná pomocí reprezentace [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) . 

## <a name="http-methods"></a>Metody HTTP

Příkaz   | Použití
------ | -----------
GET    | Provede operaci určenou jen pro čtení, která obvykle načítá data.
ZÁHLAVÍ   | Načte hlavičky odpovědi pro odpovídající požadavek `GET`.
PUT    | Vytvoří prostředek, který neexistuje, nebo (pokud existuje) ho aktualizuje. Některé prostředky nemusí podporovat aktualizaci.
DELETE | Odstraní nebo zruší výpis prostředku.

## <a name="http-status-codes"></a>Stavové kódy HTTP

Kód | Popis
---- | -----
200  | Úspěch a text odpovědi.
201  | Úspěch a prostředek byl vytvořen.
202  | Úspěch, požadavek byl přijat, ale některé práce mohou být neúplné a dokončeny asynchronně.
204  | Úspěch, ale neexistuje žádné tělo odpovědi.
301  | Trvalé přesměrování.
302  | Dočasné přesměrování.
400  | Parametry v adrese URL nebo textu žádosti nejsou platné.
401  | Zadané přihlašovací údaje jsou neplatné.
403  | Pro zadané přihlašovací údaje se akce nepovoluje.
404  | Požadovaný prostředek neexistuje.
409  | Požadavek je v konfliktu s existujícím prostředkem.
500  | Služba zjistila neočekávanou chybu.
503  | Služba je dočasně nedostupná.

Jakýkoli `GET` požadavek provedený na koncový bod rozhraní API může vrátit přesměrování HTTP (301 nebo 302). Klienti by měli bez problémů zvládnout taková přesměrování tím, že projednávají hlavičku `Location` a vydávají následné `GET`. Dokumentace týkající se konkrétních koncových bodů explicitně nevolá, kde je možné použít přesměrování.

V případě stavového kódu 500 na úrovni může klient implementovat přiměřený mechanismus opakování. Oficiální klient NuGet opakuje opakované pokusy při zjištění chyby stavového kódu na úrovni 500 nebo chyby protokolu TCP/DNS.

## <a name="http-request-headers"></a>Hlavičky požadavku HTTP

Název                     | Popis
------------------------ | -----------
X-NuGet-ApiKey           | Vyžadování pro vložení a odstranění, viz [`PackagePublish` prostředek](package-publish-resource.md)
X-NuGet-Client-Version   | **Zastaralé** a nahrazeno `X-NuGet-Protocol-Version`
X-NuGet-Protocol-Version | Vyžadováno v určitých případech pouze v nuget.org, viz [protokoly NuGet.org](NuGet-Protocols.md)
X-NuGet-Session-Id       | *Volitelné*. Klienti NuGet v 4.7 a identifikují požadavky HTTP, které jsou součástí stejné klientské relace NuGet.

`X-NuGet-Session-Id` má jednu hodnotu pro všechny operace související s jedním obnovením v `PackageReference`. Pro jiné scénáře, jako je například automatické dokončování a `packages.config` obnovení, může být v důsledku způsobu faktoringu kódu několik různých ID relace.

## <a name="authentication"></a>Ověřování

Ověřování je ponecháno až do zdrojové implementace balíčku pro definování. Pro nuget.org vyžaduje ověření pouze prostředek `PackagePublish`, a to prostřednictvím zvláštního záhlaví klíče rozhraní API. Podrobnosti najdete v tématu [`PackagePublish` prostředku](package-publish-resource.md) .
