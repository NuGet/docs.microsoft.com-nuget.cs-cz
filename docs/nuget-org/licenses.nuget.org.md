---
title: licenses.nuget.org
author: agr
ms.date: 02/22/2019
ms.openlocfilehash: 717cf8c47335c620410be71300b07de82799e1d3
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427551"
---
# <a name="licensesnugetorg"></a>licenses.nuget.org

## <a name="rationale"></a>Odůvodnění

Se zavedením [licenčních výrazů](../reference/nuspec.md#license)se objevil požadavek na spolehlivou službu, která by poskytovala referenční text pro jednotlivé identifikátory licencí, identifikátory výjimek nebo licenční výrazy.
Dalším požadavkem pro tuto službu je mít stabilní schéma URL, které není náchylné k propojení hnilobě, takže můžeme bezpečně použít k zajištění zpětné kompatibility pro starší klienty.

Licenses.nuget.org tuto roli plní. Nuget.org jej používá k poskytnutí textového odkazu licence pro balíčky, které určují svou licenci pomocí licenčního výrazu. `nuget pack`nebo balení s [jinými klientskými nástroji](../install-nuget-client-tools.md) nastavte [`licenseUrl`](../reference/nuspec.md#licenseurl) prvek tak, aby ukazoval na `license` licenses.nuget.org aby poskytoval zpětnou kompatibilitu se staršími klienty, kteří tento prvek nepodporují.

## <a name="protocol"></a>Protocol (Protokol)

Licenses.nuget.org je určen k zobrazení lidmi ve svých prohlížečích, nejsou k dispozici žádné strojově čitelné odpovědi.
Protokol HTTPS musí být použit a očekává se, že požadavky budou vytvořeny určitým způsobem. Podporuje `GET` pouze požadavky.
Přijímá licenční výrazy nebo identifikátory výjimek licence jako vstup způsobem uvedeným níže. Vezměte prosím na vědomí, že všechny prvky licenční výrazy jsou rozlišování velkých a malých písmen, a proto všechny vstupy do licenses.nuget.org je rozlišování velkých a malých písmen.

### <a name="license-expressions"></a>Licenční výrazy

#### <a name="request"></a>Žádost

Licenční výrazy (včetně triviálních případů, kdy se výraz skládá z jedné licence) musí být [kódovány adresou URL](https://tools.ietf.org/html/rfc3986#section-2.1) a použity jako cesta v požadavku na licenses.nuget.org.

| Výraz licence | Adresa URL, která má být |
|:---|:---|
| MIT                                                | <https://licenses.nuget.org/MIT> |
| (MIT)                                              | <https://licenses.nuget.org/(MIT)> |
| (POUZE LGPL-2.0-s výjimkou FLTK NEBO Apache-2.0+) | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

Služba podporuje pouze identifikátory licencí a identifikátory výjimek licencí, které jsou akceptovány nuget.org. Všechny licenční výrazy, které obsahují nepodporované identifikátory licencí nebo identifikátory výjimek licencí nebo které neodpovídají syntaxi licenčního výrazu, jsou považovány za neplatné.

#### <a name="response"></a>Odpověď

Licenses.nuget.org reaguje na požadavky obsahující platné licenční výrazy se stavovým kódem HTTP 200 a webovou stránkou obsahující popis licenčního výrazu:

* pokud zadaný licenční výraz obsahuje jeden identifikátor licence, je vrácena webová stránka, která obsahuje tento referenční text licence;
* Pokud je zadaný licenční výraz složeným licenčním výrazem, je vrácena webová stránka obsahující licenční výraz s odkazy na jednotlivé licence nebo licence výjimky.

Všechny požadavky, které obsahují neplatný licenční výraz, mají za následek odpověď HTTP 404.

### <a name="license-exceptions"></a>Výjimky licencí

#### <a name="request"></a>Žádost

Identifikátory výjimek licence musí být kódovány adresou URL a použity jako cesta v žádosti o licenses.nuget.org. V jednom požadavku lze poskytnout pouze jeden identifikátor výjimky licence. V části cesty adresy URL se nesmí v části cesty k adrese URL nenasytit žádné další znaky kromě identifikátoru výjimky licence.

| Identifikátor výjimky licence | Adresa URL, která má být |
|:---|:---|
|Výjimka FLTK            | <https://licenses.nuget.org/FLTK-exception> |
|openvpn-openssl-výjimka | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a>Odpověď

Licenses.nuget.org odpoví na požadavek se známým identifikátorem výjimky licence s odpovědí HTTP 200 a webovou stránkou obsahující referenční text pro zadanou výjimku licence.

Jakýkoli požadavek obsahující nepodporovaný identifikátor výjimky licence má za následek odpověď HTTP 404.