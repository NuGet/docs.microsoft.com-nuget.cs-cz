---
title: Protokoly nuget.org | Microsoft Docs
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 10/30/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: ba1d9742-9f1c-42ff-8c30-8e953e23c501
description: "Měnící nuget.org protokoly pro interakci s klienty NuGet."
ms.reviewer:
- kraigb
- karann-msft
ms.openlocfilehash: 0bc71795d120256b9eb14ca64141f0b69f01e620
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/05/2018
---
# <a name="nugetorg-protocols"></a>Protokoly nuget.org

Pro interakci s nuget.org, klienti musí postupovat podle určité protokoly. Protože tyto protokoly uchovávat vyvíjejí, klienti musí identifikovat verzi protokolu, které používají při volání metody konkrétní nuget.org rozhraní API. To umožňuje nuget.org zavádět změny způsobem pevné pro původní klienty.

> [!Note]
> Rozhraní API popsané na této stránce jsou specifické pro nuget.org a neexistuje žádný očekávání pro jiné implementace NuGet serveru zavádět tato rozhraní API. 

Informace o rozhraní API NuGet široce implementována v ekosystému NuGet najdete v tématu [přehled rozhraní API](overview.md).

Toto téma uvádí různé protokoly jako a pokud by byly předány existence.

## <a name="nuget-protocol-version-410"></a>Verze protokolu NuGet 4.1.0

4.1.0 protokol Určuje použití klíče ověření rozsahu pro interakci s služby než nuget.org se ověřit balíček proti nuget.org účtu. Všimněte si, že `4.1.0` verze číslo je neprůhledný řetězec, ale se stane, se shoduje s první verzi oficiální klienta NuGet podporovaným tento protokol.

Ověření zajistí, že rozhraní API klíče vytvořené uživatelem se používají pouze s nuget.org a tímto ověřování nebo ověřování z službu třetí strany se zpracovává prostřednictvím jednorázové použití klíče ověření rozsahu. Tyto klíče ověřte oboru slouží k ověření, že balíček patří do určitého uživatele (účet) v nuget.org.

### <a name="client-requirement"></a>Požadavek klienta

Klienti jsou potřeba předat následující hlavičku při provádění volání rozhraní API **nabízené** balíčků nuget.org:

```
X-NuGet-Protocol-Version: 4.1.0
```

Všimněte si, že `X-NuGet-Client-Version` záhlaví má podobnou sémantiku, ale je vyhrazen pouze používat oficiální klienta NuGet. Třetí strany klienti měli používat `X-NuGet-Protocol-Version` hlavičku a hodnotu.

**Nabízené** samotný protokol je popsána v dokumentaci k [ `PackagePublish` prostředků](package-publish-resource.md).

Pokud klient komunikuje s externích služeb a potřebuje k ověření, zda balíček patří do určitého uživatele (účet), měl by se používat protokol následující a používat klíče ověřte oboru a není klíče rozhraní API z nuget.org.

### <a name="api-to-request-a-verify-scope-key"></a>Žádost o oboru ověřte klíč rozhraní API

Toto rozhraní API slouží k získání klíče ověřte oboru pro autora nuget.org se ověřit balíček vlastníkem mu.

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a>Parametry žádosti

Název           | V     | Typ   | Požadováno | Poznámky
-------------- | ------ | ------ | -------- | -----
ID             | Adresa URL    | odkazy řetězců | Ano      | Balíček identidier, pro které je požadováno ověřte, zda klíč oboru
VERZE        | Adresa URL    | odkazy řetězců | Ne       | Verze balíčku
X-NuGet-ApiKey | Záhlaví | odkazy řetězců | Ano      | Třeba `X-NuGet-ApiKey: {USER_API_KEY}`.

#### <a name="response"></a>Odpověď

```
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a>Rozhraní API a ověřte klíč oboru ověřte

Toto rozhraní API slouží k ověření oboru ověřte, zda klíč pro vlastníkem nuget.org autora balíčku.

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a>Parametry žádosti

Název           | V     | Typ   | Požadováno | Poznámky
-------------  | ------ | ------ | -------- | -----
ID             | Adresa URL    | odkazy řetězců | Ano      | Identifikátor balíčku, jehož klíč oboru ověřte, zda je požadováno
VERZE        | Adresa URL    | odkazy řetězců | Ne       | Verze balíčku
X-NuGet-ApiKey | Záhlaví | odkazy řetězců | Ano      | Třeba `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`.

> [!Note]
> Tento klíč oboru rozhraní API ověřte platnost vyprší v čase za den nebo při prvním použití, cokoliv nastane dříve.

#### <a name="response"></a>Odpověď

Stavový kód | Význam
----------- | -------
200         | Klíč rozhraní API je platný
403         | Klíč rozhraní API je neplatný nebo není autorizovaný k nabízení pro balíček
404         | Balíček odkazuje `ID` a `VERSION` (volitelné) neexistuje
