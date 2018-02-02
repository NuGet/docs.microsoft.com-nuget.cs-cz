---
title: "Přehled, NuGet rozhraní API | Microsoft Docs"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Rozhraní API NuGet je sada koncových bodů protokolu HTTP, které je možné stáhnout balíčky, načíst metadata, publikujte nové balíčky atd."
keywords: "Rozhraní API V3 NuGet, rozhraní API NuGet V2, NuGet JSON, rozhraní API registrace NuGet NuGet API ploché kontejner, NuGet nupkg rozhraní API, NuGet metadat rozhraní API, hledání NuGet rozhraní API a NuGet nabízené rozhraní API, NuGe publikovat rozhraní API, NuGet odstranit rozhraní API, rozhraní API, protokol NuGet unlist NuGet"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: c28b0912be6dbccab06078100cb71821c3658e08
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-api"></a>NuGet rozhraní API

Rozhraní API NuGet je sada koncových bodů protokolu HTTP, které lze použít pro stáhnout balíčky, načtení metadat, publikování nové balíčky a provádět většinu dalších operací k dispozici v oficiální klienty NuGet.

Toto rozhraní API slouží klientem NuGet v sadě Visual Studio, nuget.exe a rozhraní příkazového řádku .NET k provádění operací NuGet, jako [ `dotnet restore` ](/dotnet/articles/core/preview3/tools/dotnet-restore), vyhledávání v uživatelském rozhraní Visual Studio a [ `nuget.exe push` ](../tools/cli-ref-push.md).

Poznámka: v některých případech nuget.org má další požadavky, které nejsou vynucené jinými zdroji balíčku. Tyto rozdíly jsou popsány pomocí [nuget.org protokoly](nuget-protocols.md).

## <a name="service-index"></a>Index služby

Vstupní bod pro rozhraní API je dokument JSON v dobře známé umístění. Tento dokument je volána **indexu služby**.
Umístění indexu služby pro nuget.org je `https://api.nuget.org/v3/index.json`.

Tento dokument JSON obsahuje seznam *prostředky* který poskytují různé funkce a splnění použití v odlišných situacích.

Klienti, které podporují rozhraní API by měl přijmout jednu nebo více tyto adresy URL služby indexu jako způsobu připojení ke zdrojům příslušných balíčku.

Další informace o indexu služby najdete v tématu [jeho referenční dokumentace rozhraní API](service-index.md).

## <a name="versioning"></a>Správa verzí

Rozhraní API je verze 3 NuGet protokolu HTTP. Tento protokol se někdy označuje jako "V3 API." Tyto dokumenty odkaz bude odkazovat na tuto verzi protokolu jednoduše jako "rozhraní API."

Verze schématu indexu služby je indikován `version` vlastnost v indexu služby. Rozhraní API vyžaduje, aby řetězec verze má hlavní verzi počet `3`. Při provedení změn pevné na schéma indexu služby, zvýší se podverze řetězec verze.

Starší klienty (například nuget.exe 2.x) nepodporují rozhraní API V3 a podporují pouze starší API V2, který není zde popsán.

Rozhraní API V3 NuGet je jako takový název, protože je nástupcem V2 rozhraní API, která byla protokol OData na základě implementované verze 2.x oficiální klienta NuGet. Rozhraní API V3 byl nejprve nepodporuje verzi 3.0 oficiální klienta NuGet a je stále nejnovější hlavní protokol verze podporována klientem nástroje NuGet 4.0 a na. 

Byly provedeny non nejnovější protokol změn do rozhraní API od prvního vydání.

## <a name="resources-and-schema"></a>Prostředky a schématu

**Indexu služby** popisuje různé druhy prostředků. Aktuální sadu prostředků podporované jsou následující:

Název prostředku                                                          | Požadováno | Popis
---------------------------------------------------------------------- | -------- | -----------
[`PackagePublish`](package-publish-resource.md)                        | Ano      | Push a odstraňte (nebo unlist) balíčky.
[`SearchQueryService`](search-query-service-resource.md)               | Ano      | Filtr a vyhledejte balíčků – klíčové slovo.
[`RegistrationsBaseUrl`](registration-base-url-resource.md)            | Ano      | Získáte metadata balíčků.
[`PackageBaseAddress`](package-base-address-resource.md)               | Ano      | Získáte obsah balíčku (.nupkg).
[`SearchAutocompleteService`](search-autocomplete-service-resource.md) | Ne       | Zjišťování ID balíčku a verze dílčí řetězec.
[`ReportAbuseUriTemplate`](report-abuse-resource.md)                   | Ne       | Vytvořte adresu URL pro přístup k webové stránky "oznámení zneužití".
[`Catalog`](catalog-resource.md)                                       | Ne       | Úplný záznam všechny události balíčku.

Obecně platí všechny NEBINÁRNÍ data vrácená prostředkem rozhraní API se serializují pomocí JSON. Schéma odpovědi vrácené každého prostředku v indexu služby je jednotlivě definované pro tento prostředek. Další informace o jednotlivých prostředcích najdete v tématech uvedených výše.

> [!Note]
> Pokud zdroj neimplementuje `SearchAutocompleteService` žádné chování automatického dokončování by mělo být zakázáno řádně. Když `ReportAbuseUriTemplate` není implementována oficiální vrátí klienta NuGet k nuget.org sestavy zneužití URL (sledovaných pomocí [NuGet Domů #4924](https://github.com/NuGet/Home/issues/4924)). Ostatní klienti mohou zvolit, aby jednoduše adresu URL sestavy zneužití nezobrazovat uživateli.

## <a name="timestamps"></a>Časová razítka

Všechny časová razítka vrácený rozhraní API jsou UTC nebo zadávají jinak pomocí [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) reprezentace. 

## <a name="http-methods"></a>Metody HTTP

Verb   | Použití
------ | -----------
GET    | Provede operaci jen pro čtení, obvykle načítání dat.
HEAD   | Načte hlavičky odpovědi pro příslušné `GET` požadavku.
PUT    | Vytvoří prostředek, který neexistuje, nebo pokud neexistuje, aktualizuje. Některé prostředky, nemusí podporovat aktualizace.
DELETE | Odstraní nebo unlists prostředku.

## <a name="http-status-codes"></a>Stavové kódy HTTP

Kód | Popis
---- | -----
200  | Úspěch, a že je text odpovědi.
201  | Úspěch a prostředek byl vytvořen.
202  | Úspěch, požadavek byl přijat, ale některé pracovní stále může být neúplné a dokončených asynchronně.
204  | Úspěch, ale neexistuje žádný text odpovědi.
301  | Trvalé přesměrování.
302  | Dočasné přesměrování.
400  | Parametry v adrese URL nebo v textu žádosti nejsou platné.
401  | Zadané přihlašovací údaje jsou neplatné.
403  | Akce není povolena, danou zadané přihlašovací údaje.
404  | Požadovaný prostředek neexistuje.
409  | Pro žádosti v konfliktu s existující prostředek.
500  | Služby došlo k neočekávané chybě.
503  | Služba je dočasně nedostupná.

Všechny `GET` požadavek na koncový bod rozhraní API může vrátit přesměrování HTTP (301 nebo 302). Klienti měli pohodlné zpracování takové přesměrování pomocí sledování `Location` záhlaví a vydávání následné `GET`. Dokumentace týkající se specifické koncové body nebude vyvolávající explicitně kde mohou být použity přesměrování.

V případě úrovni 500 stavový kód klienta můžete implementovat mechanismus přiměřené opakování. Oficiální NuGet klienta opakované pokusy třikrát při zjištění žádné úrovni 500 stavový kód nebo chyba TCP a DNS.

## <a name="http-request-headers"></a>Hlavičky požadavku HTTP

Název                     | Popis
------------------------ | -----------
X-NuGet-ApiKey           | Požadované pro nabízené a odstranění, najdete v části [ `PackagePublish` prostředků](package-publish-resource.md)
X-NuGet-Client-Version   | **Zastaralé** a nahradit`X-NuGet-Protocol-Version`
X-NuGet-Protocol-Version | V některých případech pouze v nuget.org potřeba, najdete v části [nuget.org protokoly](NuGet-Protocols.md)

## <a name="authentication"></a>Ověřování

Ověřování je ponecháno implementace zdroje balíčku definovat. Pro nuget.org pouze `PackagePublish` prostředek vyžaduje ověření prostřednictvím speciální záhlaví klíče rozhraní API. V tématu [ `PackagePublish` prostředků](package-publish-resource.md) podrobnosti.
