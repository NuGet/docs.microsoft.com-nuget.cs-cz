---
title: Podpisy úložiště, API NuGet | Microsoft Docs
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: Prostředek podpisy úložiště umožňuje klientům balíčky balíčků informovat své možnosti podepisování úložiště.
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: bfdbbb3a11de3be3f2258a3a289c0188740cdfce
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775333"
---
# <a name="repository-signatures"></a>Podpisy úložiště

Pokud zdroj balíčku podporuje přidávání podpisů úložiště do publikovaných balíčků, může klient určit podpisové certifikáty používané zdrojem balíčku. Tento prostředek umožňuje klientům zjistit, zda byl balíček podepsaný úložištěm zfalšován nebo má neočekávaný podpisový certifikát.

Prostředek, který se používá pro načtení informací o podpisu tohoto úložiště, je prostředek, který se `RepositorySignatures` našel v [indexu služby](service-index.md).

## <a name="versioning"></a>Správa verzí

Použije se následující `@type` hodnota:

@type osa                | Poznámky
-------------------------- | -----
RepositorySignatures/4.7.0 | Počáteční verze
RepositorySignatures/4.9.0 | Podporováno NuGet v 4.9 a klienty
RepositorySignatures/5.0.0 | Povoluje povolení `allRepositorySigned` . Podporováno klienty NuGet v 5.0 +

## <a name="base-url"></a>Základní adresa URL

Adresa URL vstupního bodu pro následující rozhraní API je hodnota `@id` vlastnosti přidružené k uvedené `@type` hodnotě prostředku. Toto téma používá zástupnou adresu URL `{@id}` .

Všimněte si, že na rozdíl od jiných prostředků musí `{@id}` být adresa URL obsluhována přes protokol HTTPS.

## <a name="http-methods"></a>Metody HTTP

Všechny adresy URL nalezené v prostředku signatury úložiště podporují pouze metody HTTP `GET` a `HEAD` .

## <a name="repository-signatures-index"></a>Index podpisů úložiště

Rejstřík podpisů úložiště obsahuje dvě části informací:

1. Bez ohledu na to, jestli jsou všechny balíčky nalezené ve zdroji úložiště podepsané tímto zdrojem balíčku
1. Seznam certifikátů používaných zdrojem balíčku k podepisování balíčků

Ve většině případů se seznam certifikátů připojí jenom k. Do seznamu by se přidaly nové certifikáty, pokud vypršela platnost předchozího podpisového certifikátu a zdroj balíčku musí začít používat nový podpisový certifikát. Pokud je certifikát ze seznamu odebraný, znamená to, že klient nebude moci považovat všechny signatury balíčků vytvořené s odebraným podpisovým certifikátem za platné. V tomto případě je podpis balíčku (ale ne nutně balíček) neplatný. Zásady klienta mohou umožňovat instalaci balíčku jako nepodepsaný.

V případě odvolání certifikátu (například ohrožení bezpečnosti klíče) se očekává, že zdroj balíčku znovu podepíše všechny balíčky podepsané ovlivněným certifikátem. Kromě toho by měl zdroj balíčku odebrat ovlivněný certifikát ze seznamu podpisového certifikátu.

Následující požadavek Načte index signatury úložiště.

```
GET {@id}
```

Index podpisu úložiště je dokument JSON, který obsahuje objekt s následujícími vlastnostmi:

Název                | Typ             | Vyžadováno | Poznámky
------------------- | ---------------- | -------- | -----
allRepositorySigned | boolean          | ano      | Musí se nacházet `false` v prostředcích 4.7.0 a 4.9.0.
signingCertificates | pole objektů | ano      | 

`allRepositorySigned`Logická hodnota je nastavená na false, pokud má zdroj balíčku nějaké balíčky, které nemají žádný podpis úložiště. Pokud je logická hodnota nastavená na true, všechny balíčky, které jsou k dispozici ve zdroji, musí mít podpis úložiště vytvořený jedním z podpisových certifikátů uvedených v části `signingCertificates` .

> [!Warning]
> `allRepositorySigned`Logická hodnota musí mít hodnotu false u prostředků 4.7.0 a 4.9.0. Klienti NuGet v 4.7, v 4.8 a v 4.9 nemůžou instalovat balíčky ze zdrojů, které mají `allRepositorySigned` nastavené na true.

V poli musí být jeden nebo více podpisových certifikátů, `signingCertificates` Pokud `allRepositorySigned` je logická hodnota nastavena na true. Pokud je pole prázdné a `allRepositorySigned` je nastaveno na hodnotu true, všechny balíčky ze zdroje by měly být považovány za neplatné, i když zásady klienta přesto mohou umožňovat spotřebu balíčků. Každý prvek v tomto poli je objekt JSON s následujícími vlastnostmi.

Název         | Typ   | Vyžadováno | Poznámky
------------ | ------ | -------- | -----
contentUrl   | řetězec | ano      | Absolutní adresa URL veřejného certifikátu kódovaného pomocí DER
otisky prstů | object | ano      |
subject      | řetězec | ano      | Rozlišující název subjektu z certifikátu
issuer       | řetězec | ano      | Rozlišující název vystavitele certifikátu
notBefore    | řetězec | ano      | Počáteční časové razítko období platnosti certifikátu
notAfter     | řetězec | ano      | Koncové časové razítko období platnosti certifikátu

Všimněte si, že musí `contentUrl` být obsluhován přes protokol HTTPS. Tato adresa URL nemá žádný konkrétní vzor adresy URL a je nutné ji dynamicky zjistit pomocí tohoto dokumentu indexu podpisů úložiště. 

Všechny vlastnosti v tomto objektu (kromě z `contentUrl` ) musí být odvozené z certifikátu, který najdete na adrese `contentUrl` .
Tyto odvozené vlastnosti jsou k dispozici jako pohodlí pro minimalizaci zpáteční cesty.

`fingerprints`Objekt má následující vlastnosti:

Název                   | Typ   | Vyžadováno | Poznámky
---------------------- | ------ | -------- | -----
2.16.840.1.101.3.4.2.1 | řetězec | ano      | Otisk SHA-256

Název klíče `2.16.840.1.101.3.4.2.1` je identifikátor OID algoritmu hash SHA-256.

Všechny hodnoty hash musí být malé, šestnáctkově zakódované řetězcové reprezentace algoritmu hash.

### <a name="sample-request"></a>Ukázková žádost

```
GET https://api.nuget.org/v3-index/repository-signatures/index.json
```

### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
