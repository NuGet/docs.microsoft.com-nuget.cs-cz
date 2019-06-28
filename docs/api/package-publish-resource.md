---
title: Nasdílení změn a odstranění rozhraní API Nugetu
description: Služba publikování umožňuje klientům publikovat nové balíčky a vyjmutí ze seznamu nebo odstranit existující balíčky.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 6e81055796e20186c5769d2ec39849e6c551ff87
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426727"
---
# <a name="push-and-delete"></a>Nasdílení změn a odstranění

Je možné vložit, odstranit (nebo vyjmutí ze seznamu, v závislosti na implementaci serveru) a relist balíčky pomocí rozhraní API V3 NuGet. Tyto operace jsou odhlásit z založené `PackagePublish` prostředek se nenašel v [index služby](service-index.md).

## <a name="versioning"></a>Správa verzí

Následující `@type` hodnota se používá:

@type Hodnota          | Poznámky
-------------------- | -----
PackagePublish/2.0.0 | Počáteční verze

## <a name="base-url"></a>Základní adresa URL

Základní adresa URL pro následující rozhraní API je hodnota `@id` vlastnost `PackagePublish/2.0.0` prostředků ve zdroji balíčku [index služby](service-index.md). Pro níže uvedenou dokumentaci se používá adresu URL nuget.org. Vezměte v úvahu `https://www.nuget.org/api/v2/package` jako zástupný symbol pro `@id` hodnota nalezena v indexu služby.

Všimněte si, že tato adresa URL odkazuje do stejného umístění jako starší verze koncového bodu V2 nabízených oznámení, protože protokol je stejný.

## <a name="http-methods"></a>Metody HTTP

`PUT`, `POST` a `DELETE` tento prostředek podporovaných metod HTTP. Které metody jsou podporovány na každém koncovém bodu najdete níže.

## <a name="push-a-package"></a>Push balíčku

> [!Note]
> má nuget.org [další požadavky](NuGet-Protocols.md) pro komunikaci s koncovým bodem nabízených oznámení.

nuget.org podporuje vkládání nové balíčky pomocí následující rozhraní API. Pokud balíček s zadané ID a verzí již existuje, bude taková nuget.org nasdílení změn. Další zdroje balíčků můžou podporovat nahrazení existujícího balíčku.

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a>Parametry žádosti

Name           | V     | type   | Požadováno | Poznámky
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | Záhlaví | odkazy řetězců | ano      | Třeba `X-NuGet-ApiKey: {USER_API_KEY}`.

Klíč rozhraní API je neprůhledný řetězec získali ze zdroje balíčku uživatelem a konfiguraci do klienta. Je vyžadováno žádné konkrétní řetězec formátu, ale délka klíče rozhraní API by neměl být delší než rozumnou velikost pro hodnoty hlavičky protokolu HTTP.

### <a name="request-body"></a>Text požadavku

Text požadavku musí být v následujícím tvaru:

#### <a name="multipart-form-data"></a>Dat vícedílného formuláře

Hlavička požadavku `Content-Type` je `multipart/form-data` a nezpracované bajtů .nupkg stisknuté je první položka v textu požadavku. Následující položky v textu vícedílné zprávy jsou ignorovány. Název souboru nebo jiné záhlaví položek s více částmi. jsou ignorovány.

### <a name="response"></a>Odpověď

Stavový kód | Význam
----------- | -------
201, 202    | Balíček byl úspěšně odeslal.
400         | Zadaný balíček je neplatný
409         | Balíček se zadané ID a verze již existuje.

Implementace serveru lišit na stavový kód úspěchu vrátí, když se úspěšně odeslal balíček.

## <a name="delete-a-package"></a>Odstranění balíčku

nuget.org interpretuje požadavku na odstranění balíčku jako příslušný "vyjmutí ze seznamu". To znamená, že balíček je stále k dispozici pro stávající zákazníky balíček, ale balíček už se zobrazí ve výsledcích hledání nebo ve webovém rozhraní. Další informace o tento postup najdete v článku [odstranit balíčky](../nuget-org/policies/deleting-packages.md) zásad. Jiné implementace serveru je zdarma jak interpretovat jako pevný odstranit tento signál, obnovitelné odstranění nebo vyjmutí ze seznamu. Například [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (na serveru implementace podporuje pouze rozhraní API pro starší verze 2) podporuje tato žádost zpracovává jako unlist nebo pevné delete založené na možnosti konfigurace.

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a>Parametry žádosti

Name           | V     | type   | Požadováno | Poznámky
-------------- | ------ | ------ | -------- | -----
ID             | Adresa URL    | odkazy řetězců | ano      | ID balíčku, který se má odstranit
VERZE        | Adresa URL    | odkazy řetězců | ano      | Verze balíčku k odstranění
X-NuGet-ApiKey | Záhlaví | odkazy řetězců | ano      | Třeba `X-NuGet-ApiKey: {USER_API_KEY}`.

### <a name="response"></a>Odpověď

Stavový kód | Význam
----------- | -------
204         | Balíček byl odstraněn.
404         | Žádný balíček pomocí zadaných `ID` a `VERSION` existuje

## <a name="relist-a-package"></a>Relist balíčku

Pokud balíček je neuvedené v seznamu, je možné vytvořit balíček znovu viditelné ve výsledcích vyhledávání pomocí koncového bodu "relist". Tento koncový bod má stejný tvar jako [odstranit (vyjmutí ze seznamu) koncového bodu](#delete-a-package) , ale používá `POST` metoda protokolu HTTP místo `DELETE` metody.

Pokud už je balíček uvedený, stále neproběhne.

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a>Parametry žádosti

Name           | V     | type   | Požadováno | Poznámky
-------------- | ------ | ------ | -------- | -----
ID             | Adresa URL    | odkazy řetězců | ano      | ID balíčku, který se má relist
VERZE        | Adresa URL    | odkazy řetězců | ano      | Verze balíčku, který se relist
X-NuGet-ApiKey | Záhlaví | odkazy řetězců | ano      | Třeba `X-NuGet-ApiKey: {USER_API_KEY}`.

### <a name="response"></a>Odpověď

Stavový kód | Význam
----------- | -------
200         | Balíček je nyní uveden.
404         | Žádný balíček pomocí zadaných `ID` a `VERSION` existuje
