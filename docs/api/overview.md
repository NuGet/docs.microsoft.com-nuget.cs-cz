---
title: Přehled rozhraní API Nugetu
description: NuGet rozhraní API je sada koncových bodů HTTP, které je možné stáhnout balíčky, načíst metadata, publikovat nové balíčky atd.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: fe843a121e2f1aae376f3e30a7b911792057688f
ms.sourcegitcommit: e9c58dbfc1af2876337dcc37b1b070e8ddec0388
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/09/2018
ms.locfileid: "40020528"
---
# <a name="nuget-api"></a>Rozhraní API Nugetu

NuGet rozhraní API je sada koncových bodů HTTP, které je možné stáhnout balíčky, načíst metadata, publikovat nové balíčky a provádějí většinu dalších operací k dispozici v oficiální klienty NuGet.

Toto rozhraní API používá klienta NuGet v sadě Visual Studio, nuget.exe a rozhraní příkazového řádku .NET k provádění operací NuGet, jako [ `dotnet restore` ](/dotnet/articles/core/preview3/tools/dotnet-restore), vyhledávání v Uživatelském rozhraní služby Visual Studio a [ `nuget.exe push` ](../tools/cli-ref-push.md).

Všimněte si, v některých případech nuget.org má další požadavky, které nejsou vynucené z jiných zdrojů balíčků. Tyto rozdíly jsou popsány pomocí [protokoly nuget.org](nuget-protocols.md).

## <a name="service-index"></a>Index služby

Vstupní bod pro rozhraní API je dokument JSON v dobře známé umístění. Tento dokument je volána **index služby**. Umístění index služby pro nuget.org je `https://api.nuget.org/v3/index.json`.

Tento dokument JSON obsahuje seznam *prostředky* která poskytují různé funkce a splnit různé případy použití.

Klienti podporující rozhraní API by měl přijmout jednu nebo více tyto adresy URL indexu služby jako způsob připojení ke zdrojům odpovídající balíček.

Další informace o index služby najdete v tématu [reference k rozhraní API](service-index.md).

## <a name="versioning"></a>Správa verzí

Rozhraní API je verze 3 protokolu HTTP Nugetu. Tento protokol se někdy označuje jako "V3 API." Tyto referenční dokumenty bude odkazovat na tuto verzi protokolu jednoduše jako "rozhraní API."

Verze schématu indexu služby je indikován `version` vlastnost index služby. Rozhraní API Určuje, zda má řetězec verze číslo hlavní verze `3`. Jak nevýznamných změn schématu indexu služby, zvýší se verze řetězec podverze.

Starší klienti (jako je například nuget.exe 2.x) nepodporují rozhraní API V3 a podporují pouze starší API V2, které není zdokumentované tady.

Rozhraní API V3 NuGet jmenuje jako takové, protože jedná se o nástupce rozhraní API V2, která byla protokolu založených na protokolu OData implementované verze 2.x oficiální klienta NuGet. Rozhraní API V3 je nejprve podporován ve verzi 3.0 oficiální klienta NuGet a stále verze nejnovější hlavní protokol není podporovaný od klienta NuGet 4.0 a. 

Bez konce protokolu změnám rozhraní API od jeho prvním vydání.

## <a name="resources-and-schema"></a>Prostředky a schématu

**Index služby** popisuje různé druhy prostředků. Aktuální sadu prostředků podporované jsou následující:

Název prostředku                                                          | Požadováno | Popis
---------------------------------------------------------------------- | -------- | -----------
[`PackagePublish`](package-publish-resource.md)                        | Ano      | Push a delete (nebo vyjmutí ze seznamu) balíčky.
[`SearchQueryService`](search-query-service-resource.md)               | Ano      | Můžete filtrovat a hledat balíčky – klíčové slovo.
[`RegistrationsBaseUrl`](registration-base-url-resource.md)            | Ano      | Získáte metadata balíčku.
[`PackageBaseAddress`](package-base-address-resource.md)               | Ano      | Získáte balíček obsahu (.nupkg).
[`SearchAutocompleteService`](search-autocomplete-service-resource.md) | Ne       | Zjistíte ID balíčku a verze pomocí dílčí řetězec.
[`ReportAbuseUriTemplate`](report-abuse-resource.md)                   | Ne       | Vytvořte adresu URL pro přístup k webové stránky "ohlásit nevhodné chování".
[`RepositorySignatures`](repository-signatures-resource.md)            | Ne       | Získání certifikátů pro podpis úložiště.
[`Catalog`](catalog-resource.md)                                       | Ne       | Celý záznam všech událostí balíčku.

Obecně platí všechny NEBINÁRNÍ data vrácená rozhraním API prostředku se serializují pomocí formátu JSON. Schéma odpovědi vrácené každého prostředku v indexu služby je samostatně definované pro daný prostředek. Další informace o jednotlivých prostředcích najdete v tématech uvedených výše.

> [!Note]
> Když zdroj neimplementuje `SearchAutocompleteService` všechna chování automatického dokončování by mělo být zakázáno bez výpadku. Když `ReportAbuseUriTemplate` neimplementována oficiální spadá klienta NuGet zpět na nuget.org ohlásit nevhodné chování adresy URL (sledované podle [Domů NuGet #4924](https://github.com/NuGet/Home/issues/4924)). Jiní klienti mohou zvolit, aby jednoduše adresa URL pro sestavu zneužití nezobrazovat uživateli.

## <a name="timestamps"></a>Časová razítka

Všechny časová razítka vrácená rozhraním API jsou UTC nebo jinak zvoleny pomocí [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) reprezentace. 

## <a name="http-methods"></a>Metody HTTP

Příkaz   | Použití
------ | -----------
ZÍSKAT    | Provádí operaci jen pro čtení, obvykle načítají se data.
HLAVNÍ   | Načte hlavičky odpovědi pro odpovídající `GET` požadavku.
PUT    | Vytvoří prostředek, který neexistuje, nebo pokud existuje, aktualizuje ji. Některé prostředky nemusí podporovat aktualizaci.
DELETE | Odstraní nebo unlists prostředku.

## <a name="http-status-codes"></a>Stavové kódy HTTP

Kód | Popis
---- | -----
200  | Úspěch, a je text odpovědi.
201  | Úspěch a prostředek byl vytvořen.
202  | Úspěch požadavku byla přijata ale úkony mohou být nekompletní a dokončených asynchronně.
204  | Úspěch, ale neexistuje žádný text odpovědi.
301  | Trvalé přesměrování.
302  | Dočasné přesměrování.
400  | Parametry v adrese URL nebo v textu žádosti nejsou platné.
401  | Zadaná pověření jsou neplatná.
403  | Akce není povolen zadaný zadaných přihlašovacích údajů.
404  | Požadovaný prostředek neexistuje.
409  | V požadavku je v konfliktu s existující prostředek.
500  | Služby došlo k neočekávané chybě.
503  | Služba je dočasně nedostupná.

Žádné `GET` požadavku na koncový bod rozhraní API může vrátit přesměrování HTTP (301 nebo 302). Klienti měli bez výpadku zpracovávat takové přesměrování pozorováním `Location` záhlaví a vydání následných `GET`. Dokumentace týkající se konkrétní koncové body nebude volat explicitně, kde mohou být použity přesměrování.

V případě úrovni 500 stavový kód klienta můžete implementovat mechanismus přiměřené opakování. Oficiální NuGet klienta opakované pokusy třikrát při zjištění libovolné úrovni 500 stavový kód nebo došlo k chybě TCP/DNS.

## <a name="http-request-headers"></a>Hlavičky žádosti HTTP

Název                     | Popis
------------------------ | -----------
X-NuGet-ApiKey           | Vyžadováno pro push a delete, naleznete v tématu [ `PackagePublish` prostředků](package-publish-resource.md)
X-NuGet klienta Version   | **Zastaralé** a nahradit `X-NuGet-Protocol-Version`
X-NuGet-Protocol-Version | Vyžaduje se v některých případech pouze na nuget.org, naleznete v tématu [protokoly nuget.org](NuGet-Protocols.md)
X-NuGet-Session-Id       | *Volitelné*. NuGet klientů v4.7 + identifikovat požadavky HTTP, které jsou součástí stejné relace klienta NuGet. Pro `PackageReference` existuje operace obnovení je jedno id relace, pro jiné scénáře, jako je automatické dokončování, a `packages.config` obnovení může být několik různých id relace z důvodu jak dostaneme kód.

## <a name="authentication"></a>Ověřování

Ověřování zůstane až po implementaci zdroje balíčku k definování. Pro nuget.org, pouze `PackagePublish` prostředek vyžaduje ověření prostřednictvím speciální záhlaví klíče rozhraní API. Zobrazit [ `PackagePublish` prostředků](package-publish-resource.md) podrobnosti.
