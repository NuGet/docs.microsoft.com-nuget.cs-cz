---
title: Podpisy úložiště, rozhraní API Nugetu | Dokumentace Microsoftu
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: Prostředek podpisy úložiště umožňuje klientům zdroje balíčků oznamujeme jejich úložiště podpis funkce.
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: ea318446c41a0d85d3fbf959dd38c929a0d0e9a1
ms.sourcegitcommit: 6b71926f062ecddb8729ef8567baf67fd269642a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/22/2019
ms.locfileid: "59931849"
---
# <a name="repository-signatures"></a>Podpisy úložiště

Pokud zdroj balíčku podporuje přidávání podpisy úložiště publikovaných balíčků, je možné pro klienta k určení podpisové certifikáty, které jsou používány zdroji balíčku. Tento prostředek umožňuje klientům zjišťovat, zda úložiště podepsaný balíček byla změněna nebo má neočekávaný podpisový certifikát.

Prostředek, který používá pro načtení těchto informací podpisu úložiště je `RepositorySignatures` prostředek se nenašel v [index služby](service-index.md).

## <a name="versioning"></a>Správa verzí

Následující `@type` hodnota se používá:

@type Hodnota                | Poznámky
-------------------------- | -----
RepositorySignatures/4.7.0 | Počáteční verze
RepositorySignatures/4.9.0 | Podporuje NuGet v4.9 + klientů
RepositorySignatures/5.0.0 | Umožňuje povolení `allRepositorySigned`. Podporuje NuGet 5.0 + klientů

## <a name="base-url"></a>Základní adresa URL

Adresa URL vstupního bodu pro následující rozhraní API je hodnota `@id` vlastnost přidružená k výše uvedených prostředků `@type` hodnotu. Toto téma používá zástupné adresy URL `{@id}`.

Všimněte si, že na rozdíl od jiných prostředků `{@id}` adresa URL je potřeba zpracovat v přes protokol HTTPS.

## <a name="http-methods"></a>Metody HTTP

Všechny adresy URL v metod podpory jenom HTTP prostředku podpisy úložiště `GET` a `HEAD`.

## <a name="repository-signatures-index"></a>Index podpisy úložiště

Index podpisy úložiště obsahuje dva druhy údajů:

1. Jestli na zdroj nenašel všechny balíčky jsou úložiště, které jsou podepsány zdroje tohoto balíčku.
1. Seznam certifikátů používaného zdroje balíčku k podepisování balíčků.

Ve většině případů bude seznam certifikátů vždy jen připojeno k. Nové certifikáty byly přidány do seznamu, pokud předchozí podpisový certifikát vypršela platnost a zdroj balíčku je potřeba začít používat nový podpisový certifikát. Pokud je certifikát je odebrán ze seznamu, to znamená, že všechny podpisů balíčků, které jsou vytvořené pomocí odebrané podpisového certifikátu by už být uznán platnou klienta. V takovém případě je neplatný podpis balíčku (ale ne nutně balíček). Zásady klienta může povolit instalaci balíčku jako bez znaménka.

V případě zrušení certifikátů (třeba klíče ohrožení zabezpečení) zdroj balíčku by měl znovu podepsat všechny balíčky, které jsou podepsané certifikátem pro ovlivněné. Kromě toho by měl zdroj balíčku ovlivněné certifikát odebrat ze seznamu podpisový certifikát.

Následující požadavek načte index podpisy úložiště.

    GET {@id}

Signatura indexu úložiště je dokument JSON, který obsahuje objekt s následujícími vlastnostmi:

Název                | Type             | Požadováno | Poznámky
------------------- | ---------------- | -------- | -----
allRepositorySigned | Logická hodnota          | ano      | Musí být `false` 4.7.0 a 4.9.0 prostředků
signingCertificates | Pole objektů | ano      | 

`allRepositorySigned` Logická hodnota je nastavena na hodnotu false, pokud zdroj balíčku má některé balíčky, které mají žádný podpis úložiště. Pokud je nastavená hodnota true, všechny balíčky, které jsou k dispozici na datový typ boolean zdroje musí mít podpis úložiště vytvořeného pomocí jedné z podpisové certifikáty podle `signingCertificates`.

> [!Warning]
> `allRepositorySigned` Boolean musí mít hodnotu false u 4.7.0 a 4.9.0 prostředků. Klienti NuGet v4.7, v4.8 a v4.9 nelze nainstalovat balíčky ze zdrojů, které mají `allRepositorySigned` nastavenou na hodnotu true.

Měla by existovat jeden nebo více podpisové certifikáty v `signingCertificates` pole, pokud `allRepositorySigned` logická hodnota je nastavena na hodnotu true. Pokud je pole prázdné a `allRepositorySigned` je nastavena na hodnotu true, všechny balíčky ze zdroje by měl být neplatná, i když se zásady klienta může stále povolit spotřebu balíčků. Každý prvek v tomto poli je objekt JSON s následujícími vlastnostmi.

Název         | Type   | Požadováno | Poznámky
------------ | ------ | -------- | -----
contentUrl   | odkazy řetězců | ano      | Absolutní adresa URL pro kódování DER veřejný certifikát
otisky prstů | odkazy objektů | ano      |
Předmět      | odkazy řetězců | ano      | Rozlišující název subjektu z certifikátu
issuer       | odkazy řetězců | ano      | Rozlišující název vystavitele certifikátu
neplatí před    | odkazy řetězců | ano      | Výchozí časové razítko období platnosti certifikátu
neplatí po     | odkazy řetězců | ano      | Časové razítko koncové období platnosti certifikátu

Všimněte si, `contentUrl` je potřeba zpracovat v přes protokol HTTPS. Tato adresa URL nemá žádné konkrétnímu vzor adresy URL a musí být zjištěny dynamicky, pomocí tohoto dokumentu indexu podpisy úložiště. 

Všechny vlastnosti v tomto objektu (ze aside `contentUrl`) musí být derivable z certifikátu na `contentUrl`.
Tyto vlastnosti derivable jsou k dispozici jako usnadnění a minimalizovat výměny zpráv.

`fingerprints` Objektu má následující vlastnosti:

Název                   | Type   | Požadováno | Poznámky
---------------------- | ------ | -------- | -----
2.16.840.1.101.3.4.2.1 | odkazy řetězců | ano      | Otisk SHA-256

Název klíče `2.16.840.1.101.3.4.2.1` je OID hashovací algoritmus SHA-256.

Všechny hodnoty hash musí být malými písmeny, šestnáctkově zakódovaného řetězcové reprezentace hodnoty hash výtahu.

### <a name="sample-request"></a>Ukázková žádost

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a>Ukázková odpověď

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
