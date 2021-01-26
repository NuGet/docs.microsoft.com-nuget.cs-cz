---
title: Nabízení a odstraňování, rozhraní API NuGet
description: Služba publikování umožňuje klientům publikovat nové balíčky a odpisovat nebo odstraňovat existující balíčky.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 0a79266011433d5adc1341a8e250838988c84d13
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773926"
---
# <a name="push-and-delete"></a>Push a DELETE

Je možné předávat, odstraňovat (nebo odpisovat) v závislosti na implementaci serveru a přepisovat balíčky pomocí rozhraní NuGet V3 API. Tyto operace jsou založeny na prostředku, který `PackagePublish` najdete v [indexu služby](service-index.md).

## <a name="versioning"></a>Správa verzí

Použije se následující `@type` hodnota:

@type osa          | Poznámky
-------------------- | -----
PackagePublish/2.0.0 | Počáteční verze

## <a name="base-url"></a>Základní adresa URL

Základní adresa URL následujících rozhraní API je hodnota `@id` vlastnosti `PackagePublish/2.0.0` prostředku v [indexu služby](service-index.md)zdroje balíčku. Pro dokumentaci níže se používá adresa URL balíčku NuGet. org. Zvažte možnost `https://www.nuget.org/api/v2/package` použít jako zástupný symbol pro `@id` hodnotu nalezenou v indexu služby.

Všimněte si, že tato adresa URL odkazuje na stejné umístění jako starší verze V2 push Endpoint, protože protokol je stejný.

## <a name="http-methods"></a>Metody HTTP

`PUT`Metody, `POST` a `DELETE` http jsou podporovány tímto prostředkem. Které metody jsou podporovány u každého koncového bodu, viz níže.

## <a name="push-a-package"></a>Vložení balíčku

> [!Note]
> nuget.org má [Další požadavky](NuGet-Protocols.md) pro interakci s koncovým bodem push.

nuget.org podporuje vkládání nových balíčků pomocí následujícího rozhraní API. Pokud balíček se zadaným ID a verzí již existuje, nuget.org se zamítne. Další zdroje balíčků můžou podporovat nahrazení existujícího balíčku.

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a>Parametry žádosti

Name           | V     | Typ   | Vyžadováno | Poznámky
-------------- | ------ | ------ | -------- | -----
X-NuGet – ApiKey | Hlavička | řetězec | ano      | Například `X-NuGet-ApiKey: {USER_API_KEY}`.

Klíč rozhraní API je neprůhledný řetězec ze zdroje balíčku uživatelem a nakonfigurovaný do klienta. Není k dispozici žádný konkrétní formát řetězce, ale délka klíče rozhraní API by neměla překročit rozumnou velikost pro hodnoty hlaviček protokolu HTTP.

### <a name="request-body"></a>Text požadavku

Text žádosti musí být v následujícím tvaru:

#### <a name="multipart-form-data"></a>Data formuláře v částech

Hlavička požadavku `Content-Type` je `multipart/form-data` a první položkou v textu požadavku jsou nezpracované bajty vloženého. nupkg. Následné položky v těle části částmi jsou ignorovány. Název souboru nebo jiné hlavičky položek s více částmi jsou ignorovány.

### <a name="response"></a>Odpověď

Stavový kód | Význam
----------- | -------
201, 202    | Balíček se úspěšně odeslal.
400         | Zadaný balíček je neplatný.
409         | Balíček se zadaným ID a verzí již existuje.

Implementace serveru se liší v případě úspěšného vložení balíčku v případě, že se vrátí stavový kód úspěchu.

## <a name="delete-a-package"></a>Odstranění balíčku

nuget.org interpretuje požadavek na odstranění balíčku jako "unlist". To znamená, že balíček je stále k dispozici pro existující uživatele balíčku, ale balíček se již nezobrazuje ve výsledcích hledání nebo ve webovém rozhraní. Další informace o tomto postupu najdete v tématu [odstraněné zásady balíčků](../nuget-org/policies/deleting-packages.md) . Další implementace serveru jsou zdarma k interpretaci tohoto signálu jako pevného odstranění, obnovitelného odstranění nebo oddálení seznamu. Například [NuGet. Server](https://www.nuget.org/packages/NuGet.Server) (implementace serveru podporuje jenom starší verze V2 API) podporuje zpracování této žádosti jako buď oddálení, nebo pevné odstranění na základě možnosti konfigurace.

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a>Parametry žádosti

Name           | V     | Typ   | Vyžadováno | Poznámky
-------------- | ------ | ------ | -------- | -----
ID             | URL    | řetězec | ano      | ID balíčku, který se má odstranit
VERZE        | URL    | řetězec | ano      | Verze balíčku, který se má odstranit
X-NuGet – ApiKey | Hlavička | řetězec | ano      | Například `X-NuGet-ApiKey: {USER_API_KEY}`.

### <a name="response"></a>Odpověď

Stavový kód | Význam
----------- | -------
204         | Balíček se odstranil.
404         | Žádný balíček se zadaným `ID` a `VERSION` neexistuje.

## <a name="relist-a-package"></a>Přepsání balíčku

Pokud balíček není v seznamu, je možné ho znovu nastavit tak, aby se zobrazil ve výsledcích hledání pomocí koncového bodu "relist". Tento koncový bod má stejný tvar jako [koncový bod Delete (unlist)](#delete-a-package) , ale `POST` místo metody používá metodu http `DELETE` .

Pokud je tento balíček již uveden, požadavek bude stále úspěšný.

```
POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a>Parametry žádosti

Name           | V     | Typ   | Vyžadováno | Poznámky
-------------- | ------ | ------ | -------- | -----
ID             | URL    | řetězec | ano      | ID balíčku, který se má znovu zobrazit
VERZE        | URL    | řetězec | ano      | Verze balíčku, který se má znovu zobrazit
X-NuGet – ApiKey | Hlavička | řetězec | ano      | Například `X-NuGet-ApiKey: {USER_API_KEY}`.

### <a name="response"></a>Odpověď

Stavový kód | Význam
----------- | -------
200         | Balíček je nyní uveden
404         | Žádný balíček se zadaným `ID` a `VERSION` neexistuje.
