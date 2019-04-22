---
title: licenses.nuget.org
author: agr
ms.date: 02/22/2019
ms.openlocfilehash: 4a40cc1f7d333e8d35a721f3eed2e6b9365faf7b
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/18/2019
ms.locfileid: "58921556"
---
# <a name="licensesnugetorg"></a><span data-ttu-id="ecea5-102">licenses.nuget.org</span><span class="sxs-lookup"><span data-stu-id="ecea5-102">licenses.nuget.org</span></span>

## <a name="rationale"></a><span data-ttu-id="ecea5-103">Důvody</span><span class="sxs-lookup"><span data-stu-id="ecea5-103">Rationale</span></span>

<span data-ttu-id="ecea5-104">Se zavedením [licence výrazy](nuspec.md#license), požadavek se umístila mít spolehlivé služby, které by pro identifikátory jednotlivých licencí, identifikátory výjimky nebo licence výrazy poskytnout odkaz na text.</span><span class="sxs-lookup"><span data-stu-id="ecea5-104">With the introduction of the [license expressions](nuspec.md#license), a requirement emerged to have a reliable service that would provide a reference text for individual license identifiers, exception identifiers or license expressions.</span></span>
<span data-ttu-id="ecea5-105">Další požadavky pro tuto službu je mají stabilní schéma adresy URL, který není napadnutelná propojit rot, takže jsme může bezpečně použít pro zajištění zpětné kompatibility pro starší klienty.</span><span class="sxs-lookup"><span data-stu-id="ecea5-105">An additional requirement for this service is to have a stable URL schema, that is not susceptible to link rot, so that we can safely use it to provide backwards compatibility for older clients.</span></span>

<span data-ttu-id="ecea5-106">Licenses.nuget.org splňuje tuto roli.</span><span class="sxs-lookup"><span data-stu-id="ecea5-106">Licenses.nuget.org fulfills that role.</span></span> <span data-ttu-id="ecea5-107">Nuget.org se použije k poskytnutí text odkazu licence pro balíčky, které určují svoji licenci pro použití výrazu licence.</span><span class="sxs-lookup"><span data-stu-id="ecea5-107">Nuget.org uses it to provide the license text reference for packages that specify their license using a license expression.</span></span> <span data-ttu-id="ecea5-108">`nuget pack` nebo s jinými balení [klientských nástrojů](https://docs.microsoft.com/en-us/nuget/install-nuget-client-tools) nastavit [ `licenseUrl` ](nuspec.md#licenseurl) element tak, aby odkazoval na licenses.nuget.org k zajištění zpětné kompatibility se starší klienty, kteří nepodporují `license` element.</span><span class="sxs-lookup"><span data-stu-id="ecea5-108">`nuget pack` or packing with other [client tools](https://docs.microsoft.com/en-us/nuget/install-nuget-client-tools) set the [`licenseUrl`](nuspec.md#licenseurl) element to point to licenses.nuget.org to provide backwards compatibility with older clients that don't support the `license` element.</span></span>

## <a name="protocol"></a><span data-ttu-id="ecea5-109">Protocol (Protokol)</span><span class="sxs-lookup"><span data-stu-id="ecea5-109">Protocol</span></span>

<span data-ttu-id="ecea5-110">Licenses.nuget.org má zobrazit uživateli ve svém prohlížeči, jsou uvedeny žádné odpovědi. který je strojově čitelný.</span><span class="sxs-lookup"><span data-stu-id="ecea5-110">Licenses.nuget.org is intended to be viewed by people in their browsers, no machine-readable responses are provided.</span></span>
<span data-ttu-id="ecea5-111">Protokol HTTPS a musí být vytvořen určitým způsobem žádosti se očekává.</span><span class="sxs-lookup"><span data-stu-id="ecea5-111">HTTPS protocol must be used and requests are expected to be constructed in a certain way.</span></span> <span data-ttu-id="ecea5-112">Ladicí program podporuje pouze `GET` požadavky.</span><span class="sxs-lookup"><span data-stu-id="ecea5-112">It only supports `GET` requests.</span></span>
<span data-ttu-id="ecea5-113">Výrazy licence nebo licence výjimka identifikátorů přijímá jako vstup způsobem níže uvedené.</span><span class="sxs-lookup"><span data-stu-id="ecea5-113">It accepts license expressions or license exception identifiers as an input in a way specified below.</span></span> <span data-ttu-id="ecea5-114">Mějte prosím na paměti, že všechny prvky výrazů licence jsou malá a velká písmena a veškerý vstup do licenses.nuget.org tedy malá a velká písmena i.</span><span class="sxs-lookup"><span data-stu-id="ecea5-114">Please note, that all elements of license expressions are case sensitive, and therefore all input to licenses.nuget.org is case sensitive as well.</span></span>

### <a name="license-expressions"></a><span data-ttu-id="ecea5-115">Výrazy licence</span><span class="sxs-lookup"><span data-stu-id="ecea5-115">License expressions</span></span>

#### <a name="request"></a><span data-ttu-id="ecea5-116">Request</span><span class="sxs-lookup"><span data-stu-id="ecea5-116">Request</span></span>

<span data-ttu-id="ecea5-117">Výrazy licence (včetně triviální případech, pokud výraz se skládá z jednu licenci) musí být [kódovaná adresou URL](https://tools.ietf.org/html/rfc3986#section-2.1) a použít jako cesta požadavku, aby licenses.nuget.org.</span><span class="sxs-lookup"><span data-stu-id="ecea5-117">License expressions (including the trivial cases when expression consists of a single license) have to be [URL-encoded](https://tools.ietf.org/html/rfc3986#section-2.1) and used as a path in the request to licenses.nuget.org.</span></span>

| <span data-ttu-id="ecea5-118">Výraz licence</span><span class="sxs-lookup"><span data-stu-id="ecea5-118">License expression</span></span> | <span data-ttu-id="ecea5-119">Adresa URL pro použití</span><span class="sxs-lookup"><span data-stu-id="ecea5-119">URL to use</span></span> |
|:---|:---|
| <span data-ttu-id="ecea5-120">MIT</span><span class="sxs-lookup"><span data-stu-id="ecea5-120">MIT</span></span>                                                | <https://licenses.nuget.org/MIT> |
| <span data-ttu-id="ecea5-121">(MIT)</span><span class="sxs-lookup"><span data-stu-id="ecea5-121">(MIT)</span></span>                                              | <https://licenses.nuget.org/(MIT)> |
| <span data-ttu-id="ecea5-122">(LGPL 2.0 – jen s Apache FLTK výjimky nebo-2.0+)</span><span class="sxs-lookup"><span data-stu-id="ecea5-122">(LGPL-2.0-only WITH FLTK-exception OR Apache-2.0+)</span></span> | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

<span data-ttu-id="ecea5-123">Služby podporuje pouze identifikátory licencí a licencí výjimka identifikátory, které jsou přijaty nuget.org. Všechny licence výrazy, které obsahují identifikátory nepodporované licence nebo licence výjimka identifikátory nebo, který není v souladu s syntaxe výrazu licence jsou považovány za neplatné.</span><span class="sxs-lookup"><span data-stu-id="ecea5-123">The service supports only license identifiers and license exception identifiers that are accepted by nuget.org. All license expressions that contain unsupported license identifiers or license exception identifiers or that does not conform to license expression syntax are considered invalid.</span></span>

#### <a name="response"></a><span data-ttu-id="ecea5-124">Odpověď</span><span class="sxs-lookup"><span data-stu-id="ecea5-124">Response</span></span>

<span data-ttu-id="ecea5-125">Licenses.nuget.org reaguje na požadavky obsahující výrazy platnou licenci se stavovým kódem HTTP 200 a webová stránka obsahující popis výrazu licence:</span><span class="sxs-lookup"><span data-stu-id="ecea5-125">Licenses.nuget.org responds to requests containing valid license expressions with an HTTP 200 status code and a web page containing a description of the license expression:</span></span>

* <span data-ttu-id="ecea5-126">Pokud se zadaný výraz licence obsahuje identifikátor jednu licenci na webové stránce je vrácen, která obsahuje odkaz na text licenční;</span><span class="sxs-lookup"><span data-stu-id="ecea5-126">if supplied license expression contains a single license identifier a web page is returned that contains that license reference text;</span></span>
* <span data-ttu-id="ecea5-127">Pokud se zadaný výraz licence je výraz složeného licence, webové stránky, je vrácena, který obsahuje výraz licence s odkazy na jednotlivé licence nebo licence výjimka odkazy.</span><span class="sxs-lookup"><span data-stu-id="ecea5-127">if supplied license expression is a composite license expression, a web page is returned that contains the license expression with links to individual license or license exception references.</span></span>

<span data-ttu-id="ecea5-128">Všechny žádosti, které obsahují výraz neplatná licence za následek odpověď HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="ecea5-128">Any requests that contain an invalid license expression result in an HTTP 404 response.</span></span>

### <a name="license-exceptions"></a><span data-ttu-id="ecea5-129">Licence výjimky</span><span class="sxs-lookup"><span data-stu-id="ecea5-129">License exceptions</span></span>

#### <a name="request"></a><span data-ttu-id="ecea5-130">Request</span><span class="sxs-lookup"><span data-stu-id="ecea5-130">Request</span></span>

<span data-ttu-id="ecea5-131">Licence výjimka identifikátory musí být kódovaná adresou URL a slouží jako cestu požadavku, aby licenses.nuget.org. Pouze identifikátor jednu licenci výjimky, lze je zadat v jedné žádosti.</span><span class="sxs-lookup"><span data-stu-id="ecea5-131">License exception identifiers must be URL-encoded and used as a path in the request to licenses.nuget.org. Only a single license exception identifier can be supplied in a single request.</span></span> <span data-ttu-id="ecea5-132">Žádné další znaky kromě licence výjimka identifikátor může představovat v část cesty adresy URL.</span><span class="sxs-lookup"><span data-stu-id="ecea5-132">No additional characters besides license exception identifier may present in the path portion of the URL.</span></span>

| <span data-ttu-id="ecea5-133">Identifikátor výjimky licence</span><span class="sxs-lookup"><span data-stu-id="ecea5-133">License exception identifier</span></span> | <span data-ttu-id="ecea5-134">Adresa URL pro použití</span><span class="sxs-lookup"><span data-stu-id="ecea5-134">URL to use</span></span> |
|:---|:---|
|<span data-ttu-id="ecea5-135">FLTK-exception</span><span class="sxs-lookup"><span data-stu-id="ecea5-135">FLTK-exception</span></span>            | <https://licenses.nuget.org/FLTK-exception> |
|<span data-ttu-id="ecea5-136">openvpn-openssl-exception</span><span class="sxs-lookup"><span data-stu-id="ecea5-136">openvpn-openssl-exception</span></span> | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a><span data-ttu-id="ecea5-137">Odpověď</span><span class="sxs-lookup"><span data-stu-id="ecea5-137">Response</span></span>

<span data-ttu-id="ecea5-138">Licenses.nuget.org odpoví na žádost s identifikátorem výjimka známé licence se odpověď HTTP 200 a webové stránky obsahující text odkazu pro výjimku příslušnými licenčními.</span><span class="sxs-lookup"><span data-stu-id="ecea5-138">Licenses.nuget.org responds to a request with a known license exception identifier with a HTTP 200 response and a web page containing the reference text for the specified license exception.</span></span>

<span data-ttu-id="ecea5-139">Jakoukoli žádost obsahující identifikátor výjimky nepodporované licence výsledků v odpovědi HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="ecea5-139">Any request containing an unsupported license exception identifier results in an HTTP 404 response.</span></span>