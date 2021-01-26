---
title: nuget.org protokoly
description: Vývoj nuget.orgch protokolů pro interakci s klienty NuGet.
author: anangaur
ms.author: anangaur
ms.date: 01/21/2021
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: ea072484c896c4862e47b2c03a1b177f196b0aad
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773968"
---
# <a name="nugetorg-protocols"></a>Protokoly nuget.org

Aby mohli klienti pracovat s nuget.org, musí dodržovat určité protokoly. Vzhledem k tomu, že tyto protokoly neustále vyvíjejí vývoj, musí klienti určit verzi protokolu, kterou používají při volání specifických rozhraní nuget.org API. To umožňuje nuget.org začlenit změny nevhodným způsobem pro staré klienty.

> [!Note]
> Rozhraní API dokumentované na této stránce jsou specifická pro nuget.org a neočekávají se pro zavedení těchto rozhraní API jinými implementacemi serveru NuGet. 

Informace o rozhraní NuGet API implementovaném v celém ekosystému NuGet najdete v tématu [Přehled rozhraní API](overview.md).

V tomto tématu je uveden seznam různých protokolů, které jsou a kdy existují.

## <a name="nuget-protocol-version-410"></a>Verze protokolu NuGet 4.1.0

Protokol 4.1.0 určuje použití klíčů ověření a rozsahu pro interakci s jinými službami, než je nuget.org, k ověření balíčku proti účtu nuget.org. Všimněte si, že `4.1.0` číslo verze je neprůhledný řetězec, ale v případě, že se shoduje s první verzí oficiálního klienta NuGet, který tento protokol podporuje.

Ověřování zajišťuje, aby se uživatelsky vytvořené klíče rozhraní API používaly jenom s nuget.org a aby se jiné ověřování nebo ověřování od služby třetí strany zpracovalo pomocí klíčů pro ověření platnosti. Tyto klíče ověření a rozsahu se dají použít k ověření, že balíček patří ke konkrétnímu uživateli (účtu) v nuget.org.

### <a name="client-requirement"></a>Požadavek klienta

Při volání rozhraní API k **nabízení** balíčků do NuGet.org musí klienti předat následující hlavičku:

```
X-NuGet-Protocol-Version: 4.1.0
```

Všimněte si, že `X-NuGet-Client-Version` Hlavička má podobnou sémantiku, ale je vyhrazena jenom pro oficiálního klienta NuGet. Klienti třetích stran by měli používat `X-NuGet-Protocol-Version` hlavičku a hodnotu.

Samotný protokol **push** je popsaný v dokumentaci k [ `PackagePublish` prostředku](package-publish-resource.md).

Pokud klient komunikuje s externími službami a potřebuje ověřit, jestli balíček patří konkrétnímu uživateli (účtu), měl by použít následující protokol a použít klíče rozhraní API pro ověření a nikoli klíče rozhraní API z nuget.org.

### <a name="api-to-request-a-verify-scope-key"></a>Rozhraní API pro vyžádání klíče pro kontrolu rozsahu

Toto rozhraní API slouží k získání klíče ověřovacího oboru pro autora nuget.org k ověření balíčku, jehož vlastníkem je.

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a>Parametry žádosti

Name           | V     | Typ   | Vyžadováno | Poznámky
-------------- | ------ | ------ | -------- | -----
ID             | URL    | řetězec | ano      | Identidier balíčku, pro který se požaduje klíč ověření
VERZE        | URL    | řetězec | ne       | Verze balíčku
X-NuGet – ApiKey | Hlavička | řetězec | ano      | Například `X-NuGet-ApiKey: {USER_API_KEY}`.

#### <a name="response"></a>Odpověď

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a>Rozhraní API pro ověření klíče oboru ověřování

Toto rozhraní API se používá k ověření klíče ověřovacího oboru pro balíček vlastněné autorem nuget.org.

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a>Parametry žádosti

Name           | V     | Typ   | Vyžadováno | Poznámky
-------------  | ------ | ------ | -------- | -----
ID             | URL    | řetězec | ano      | Identifikátor balíčku, pro který se požaduje klíč ověření
VERZE        | URL    | řetězec | ne       | Verze balíčku
X-NuGet – ApiKey | Hlavička | řetězec | ano      | Například `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`.

> [!Note]
> Tento klíč rozhraní API oboru rozhraní API vyprší během dne nebo při prvním použití, podle toho, co nastane dřív.

#### <a name="response"></a>Odpověď

Stavový kód | Význam
----------- | -------
200         | Klíč rozhraní API je platný.
403         | Klíč rozhraní API je neplatný nebo nemá oprávnění k vložení do balíčku.
404         | Balíček, na který odkazuje `ID` a `VERSION` (volitelné), neexistuje.
