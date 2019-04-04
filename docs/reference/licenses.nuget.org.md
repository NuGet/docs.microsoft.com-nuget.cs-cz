---
title: licenses.nuget.org
author: agr
ms.date: 02/22/2019
ms.openlocfilehash: 4a40cc1f7d333e8d35a721f3eed2e6b9365faf7b
ms.sourcegitcommit: 8793f528a11bd8e8fb229cd12e9abba50d61e104
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/04/2019
ms.locfileid: "58921556"
---
# <a name="licensesnugetorg"></a>licenses.nuget.org

## <a name="rationale"></a>Důvody

Se zavedením [licence výrazy](nuspec.md#license), požadavek se umístila mít spolehlivé služby, které by pro identifikátory jednotlivých licencí, identifikátory výjimky nebo licence výrazy poskytnout odkaz na text.
Další požadavky pro tuto službu je mají stabilní schéma adresy URL, který není napadnutelná propojit rot, takže jsme může bezpečně použít pro zajištění zpětné kompatibility pro starší klienty.

Licenses.nuget.org splňuje tuto roli. Nuget.org se použije k poskytnutí text odkazu licence pro balíčky, které určují svoji licenci pro použití výrazu licence. `nuget pack` nebo s jinými balení [klientských nástrojů](https://docs.microsoft.com/en-us/nuget/install-nuget-client-tools) nastavit [ `licenseUrl` ](nuspec.md#licenseurl) element tak, aby odkazoval na licenses.nuget.org k zajištění zpětné kompatibility se starší klienty, kteří nepodporují `license` element.

## <a name="protocol"></a>Protocol (Protokol)

Licenses.nuget.org má zobrazit uživateli ve svém prohlížeči, jsou uvedeny žádné odpovědi. který je strojově čitelný.
Protokol HTTPS a musí být vytvořen určitým způsobem žádosti se očekává. Ladicí program podporuje pouze `GET` požadavky.
Výrazy licence nebo licence výjimka identifikátorů přijímá jako vstup způsobem níže uvedené. Mějte prosím na paměti, že všechny prvky výrazů licence jsou malá a velká písmena a veškerý vstup do licenses.nuget.org tedy malá a velká písmena i.

### <a name="license-expressions"></a>Výrazy licence

#### <a name="request"></a>Request

Výrazy licence (včetně triviální případech, pokud výraz se skládá z jednu licenci) musí být [kódovaná adresou URL](https://tools.ietf.org/html/rfc3986#section-2.1) a použít jako cesta požadavku, aby licenses.nuget.org.

| Výraz licence | Adresa URL pro použití |
|:---|:---|
| MIT                                                | <https://licenses.nuget.org/MIT> |
| (MIT)                                              | <https://licenses.nuget.org/(MIT)> |
| (LGPL 2.0 – jen s Apache FLTK výjimky nebo-2.0+) | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

Služby podporuje pouze identifikátory licencí a licencí výjimka identifikátory, které jsou přijaty nuget.org. Všechny licence výrazy, které obsahují identifikátory nepodporované licence nebo licence výjimka identifikátory nebo, který není v souladu s syntaxe výrazu licence jsou považovány za neplatné.

#### <a name="response"></a>Odpověď

Licenses.nuget.org reaguje na požadavky obsahující výrazy platnou licenci se stavovým kódem HTTP 200 a webová stránka obsahující popis výrazu licence:

* Pokud se zadaný výraz licence obsahuje identifikátor jednu licenci na webové stránce je vrácen, která obsahuje odkaz na text licenční;
* Pokud se zadaný výraz licence je výraz složeného licence, webové stránky, je vrácena, který obsahuje výraz licence s odkazy na jednotlivé licence nebo licence výjimka odkazy.

Všechny žádosti, které obsahují výraz neplatná licence za následek odpověď HTTP 404.

### <a name="license-exceptions"></a>Licence výjimky

#### <a name="request"></a>Request

Licence výjimka identifikátory musí být kódovaná adresou URL a slouží jako cestu požadavku, aby licenses.nuget.org. Pouze identifikátor jednu licenci výjimky, lze je zadat v jedné žádosti. Žádné další znaky kromě licence výjimka identifikátor může představovat v část cesty adresy URL.

| Identifikátor výjimky licence | Adresa URL pro použití |
|:---|:---|
|FLTK-exception            | <https://licenses.nuget.org/FLTK-exception> |
|openvpn-openssl-exception | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a>Odpověď

Licenses.nuget.org odpoví na žádost s identifikátorem výjimka známé licence se odpověď HTTP 200 a webové stránky obsahující text odkazu pro výjimku příslušnými licenčními.

Jakoukoli žádost obsahující identifikátor výjimky nepodporované licence výsledků v odpovědi HTTP 404.