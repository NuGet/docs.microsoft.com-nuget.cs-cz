---
title: Protokoly nuget.org
description: Rozvíjející protokoly nuget.org k interakci s klienty NuGet.
author: anangaur
ms.author: anangaur
ms.date: 10/30/2017
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: d0add777040dbb8bcde6d8e385a4feab568e5cdd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547270"
---
# <a name="nugetorg-protocols"></a>protokoly nuget.org

K interakci s nuget.org, klienti musí použít některé protokoly. Protože tyto protokoly umožní mít vznikající, musí klienti určují verzi protokolu, které používají při volání konkrétní nuget.org rozhraní API. To umožňuje nuget.org zavedení změn způsobem pevné pro staré klienty.

> [!Note]
> Rozhraní API popsané na této stránce jsou specifické pro nuget.org a neexistuje žádná očekávání pro jiné implementace NuGet server k zavedení těchto rozhraní API. 

Informace o rozhraní API NuGet široce implementované v ekosystému NuGet, najdete v článku [přehled rozhraní API](overview.md).

Toto téma obsahuje seznam různých protokolů jako a pokud by byly předány existence.

## <a name="nuget-protocol-version-410"></a>NuGet protocol verze 4.1.0

4.1.0 protokol Určuje použití klíče ověření rozsahu pro interakci s jinými službami než nuget.org se ověřit balíček proti účtu nuget.org. Všimněte si, že `4.1.0` verze číslo, které je neprůhledný řetězec, ale se stane se shoduje s první verzi oficiální klienta NuGet, který nepodporuje tento protokol.

Ověření zajistí, že klíče rozhraní API vytvořené uživatelem se používají pouze s nuget.org a tohoto ověření nebo ověřovací služby třetích stran probíhá prostřednictvím funkce klíče ověření oboru jedno použití. Tyto klíče ověření oboru slouží k ověření, že balíček patří do určitého uživatele (účet) na nuget.org.

### <a name="client-requirement"></a>Požadavek klienta

Klientů je potřeba předat následující záhlaví při provádění volání rozhraní API **nabízených** balíčků na nuget.org:

    X-NuGet-Protocol-Version: 4.1.0

Všimněte si, `X-NuGet-Client-Version` má podobnou sémantiku jako záhlaví, ale je vyhrazen pouze použije oficiální klienta NuGet. Třetí strany klienti měli používat `X-NuGet-Protocol-Version` hlavičku a hodnotu.

**Nabízených** samotný protokol je popsán v dokumentaci k [ `PackagePublish` prostředků](package-publish-resource.md).

Pokud klient komunikuje s externími službami a je potřeba ověřit, jestli balíček patří do určitého uživatele (účet), měl by používat následující protokol a ověřte, zda rozsah klíčů a ne klíče rozhraní API z webu nuget.org.

### <a name="api-to-request-a-verify-scope-key"></a>Rozhraní API pro požádat o klíč ověřte, zda rozsah

Toto rozhraní API slouží k získání klíče ověřte obor autora nuget.org se ověřit balíček vlastněné neúčtuje.

    POST api/v2/package/create-verification-key/{ID}/{VERSION}

#### <a name="request-parameters"></a>Parametry žádosti

Název           | V     | Typ   | Požadováno | Poznámky
-------------- | ------ | ------ | -------- | -----
ID             | Adresa URL    | odkazy řetězců | Ano      | Balíček identidier, pro kterou je požadována klíč oboru ověřte
VERZE        | Adresa URL    | odkazy řetězců | Ne       | Verze balíčku
X-NuGet-ApiKey | Záhlaví | odkazy řetězců | Ano      | Třeba `X-NuGet-ApiKey: {USER_API_KEY}`.

#### <a name="response"></a>Odpověď

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a>Rozhraní API pro ověření klíče ověřte, zda rozsah

Toto rozhraní API slouží k ověření ověřte, zda rozsah klíč pro vlastní nuget.org Autor balíčku.

    GET api/v2/verifykey/{ID}/{VERSION}

#### <a name="request-parameters"></a>Parametry žádosti

Název           | V     | Typ   | Požadováno | Poznámky
-------------  | ------ | ------ | -------- | -----
ID             | Adresa URL    | odkazy řetězců | Ano      | Identifikátor balíčku, pro kterou je požadována klíč oboru ověřte
VERZE        | Adresa URL    | odkazy řetězců | Ne       | Verze balíčku
X-NuGet-ApiKey | Záhlaví | odkazy řetězců | Ano      | Třeba `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`.

> [!Note]
> Tento klíč rozhraní API oboru ověřte, zda vypršení platnosti v čase za den nebo při prvním použití podle toho, co nastane dříve.

#### <a name="response"></a>Odpověď

Stavový kód | Význam
----------- | -------
200         | Klíč rozhraní API je platný
403         | Klíč rozhraní API je neplatný nebo není povoleno push pro balíček
404         | Balíček odkazuje `ID` a `VERSION` (volitelné) neexistuje
