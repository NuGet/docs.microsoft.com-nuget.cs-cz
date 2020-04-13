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
# <a name="licensesnugetorg"></a><span data-ttu-id="e40eb-102">licenses.nuget.org</span><span class="sxs-lookup"><span data-stu-id="e40eb-102">licenses.nuget.org</span></span>

## <a name="rationale"></a><span data-ttu-id="e40eb-103">Odůvodnění</span><span class="sxs-lookup"><span data-stu-id="e40eb-103">Rationale</span></span>

<span data-ttu-id="e40eb-104">Se zavedením [licenčních výrazů](../reference/nuspec.md#license)se objevil požadavek na spolehlivou službu, která by poskytovala referenční text pro jednotlivé identifikátory licencí, identifikátory výjimek nebo licenční výrazy.</span><span class="sxs-lookup"><span data-stu-id="e40eb-104">With the introduction of the [license expressions](../reference/nuspec.md#license), a requirement emerged to have a reliable service that would provide a reference text for individual license identifiers, exception identifiers or license expressions.</span></span>
<span data-ttu-id="e40eb-105">Dalším požadavkem pro tuto službu je mít stabilní schéma URL, které není náchylné k propojení hnilobě, takže můžeme bezpečně použít k zajištění zpětné kompatibility pro starší klienty.</span><span class="sxs-lookup"><span data-stu-id="e40eb-105">An additional requirement for this service is to have a stable URL schema, that is not susceptible to link rot, so that we can safely use it to provide backwards compatibility for older clients.</span></span>

<span data-ttu-id="e40eb-106">Licenses.nuget.org tuto roli plní.</span><span class="sxs-lookup"><span data-stu-id="e40eb-106">Licenses.nuget.org fulfills that role.</span></span> <span data-ttu-id="e40eb-107">Nuget.org jej používá k poskytnutí textového odkazu licence pro balíčky, které určují svou licenci pomocí licenčního výrazu.</span><span class="sxs-lookup"><span data-stu-id="e40eb-107">Nuget.org uses it to provide the license text reference for packages that specify their license using a license expression.</span></span> <span data-ttu-id="e40eb-108">`nuget pack`nebo balení s [jinými klientskými nástroji](../install-nuget-client-tools.md) nastavte [`licenseUrl`](../reference/nuspec.md#licenseurl) prvek tak, aby ukazoval na `license` licenses.nuget.org aby poskytoval zpětnou kompatibilitu se staršími klienty, kteří tento prvek nepodporují.</span><span class="sxs-lookup"><span data-stu-id="e40eb-108">`nuget pack` or packing with other [client tools](../install-nuget-client-tools.md) set the [`licenseUrl`](../reference/nuspec.md#licenseurl) element to point to licenses.nuget.org to provide backwards compatibility with older clients that don't support the `license` element.</span></span>

## <a name="protocol"></a><span data-ttu-id="e40eb-109">Protocol (Protokol)</span><span class="sxs-lookup"><span data-stu-id="e40eb-109">Protocol</span></span>

<span data-ttu-id="e40eb-110">Licenses.nuget.org je určen k zobrazení lidmi ve svých prohlížečích, nejsou k dispozici žádné strojově čitelné odpovědi.</span><span class="sxs-lookup"><span data-stu-id="e40eb-110">Licenses.nuget.org is intended to be viewed by people in their browsers, no machine-readable responses are provided.</span></span>
<span data-ttu-id="e40eb-111">Protokol HTTPS musí být použit a očekává se, že požadavky budou vytvořeny určitým způsobem.</span><span class="sxs-lookup"><span data-stu-id="e40eb-111">HTTPS protocol must be used and requests are expected to be constructed in a certain way.</span></span> <span data-ttu-id="e40eb-112">Podporuje `GET` pouze požadavky.</span><span class="sxs-lookup"><span data-stu-id="e40eb-112">It only supports `GET` requests.</span></span>
<span data-ttu-id="e40eb-113">Přijímá licenční výrazy nebo identifikátory výjimek licence jako vstup způsobem uvedeným níže.</span><span class="sxs-lookup"><span data-stu-id="e40eb-113">It accepts license expressions or license exception identifiers as an input in a way specified below.</span></span> <span data-ttu-id="e40eb-114">Vezměte prosím na vědomí, že všechny prvky licenční výrazy jsou rozlišování velkých a malých písmen, a proto všechny vstupy do licenses.nuget.org je rozlišování velkých a malých písmen.</span><span class="sxs-lookup"><span data-stu-id="e40eb-114">Please note, that all elements of license expressions are case sensitive, and therefore all input to licenses.nuget.org is case sensitive as well.</span></span>

### <a name="license-expressions"></a><span data-ttu-id="e40eb-115">Licenční výrazy</span><span class="sxs-lookup"><span data-stu-id="e40eb-115">License expressions</span></span>

#### <a name="request"></a><span data-ttu-id="e40eb-116">Žádost</span><span class="sxs-lookup"><span data-stu-id="e40eb-116">Request</span></span>

<span data-ttu-id="e40eb-117">Licenční výrazy (včetně triviálních případů, kdy se výraz skládá z jedné licence) musí být [kódovány adresou URL](https://tools.ietf.org/html/rfc3986#section-2.1) a použity jako cesta v požadavku na licenses.nuget.org.</span><span class="sxs-lookup"><span data-stu-id="e40eb-117">License expressions (including the trivial cases when expression consists of a single license) have to be [URL-encoded](https://tools.ietf.org/html/rfc3986#section-2.1) and used as a path in the request to licenses.nuget.org.</span></span>

| <span data-ttu-id="e40eb-118">Výraz licence</span><span class="sxs-lookup"><span data-stu-id="e40eb-118">License expression</span></span> | <span data-ttu-id="e40eb-119">Adresa URL, která má být</span><span class="sxs-lookup"><span data-stu-id="e40eb-119">URL to use</span></span> |
|:---|:---|
| <span data-ttu-id="e40eb-120">MIT</span><span class="sxs-lookup"><span data-stu-id="e40eb-120">MIT</span></span>                                                | <https://licenses.nuget.org/MIT> |
| <span data-ttu-id="e40eb-121">(MIT)</span><span class="sxs-lookup"><span data-stu-id="e40eb-121">(MIT)</span></span>                                              | <https://licenses.nuget.org/(MIT)> |
| <span data-ttu-id="e40eb-122">(POUZE LGPL-2.0-s výjimkou FLTK NEBO Apache-2.0+)</span><span class="sxs-lookup"><span data-stu-id="e40eb-122">(LGPL-2.0-only WITH FLTK-exception OR Apache-2.0+)</span></span> | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

<span data-ttu-id="e40eb-123">Služba podporuje pouze identifikátory licencí a identifikátory výjimek licencí, které jsou akceptovány nuget.org. Všechny licenční výrazy, které obsahují nepodporované identifikátory licencí nebo identifikátory výjimek licencí nebo které neodpovídají syntaxi licenčního výrazu, jsou považovány za neplatné.</span><span class="sxs-lookup"><span data-stu-id="e40eb-123">The service supports only license identifiers and license exception identifiers that are accepted by nuget.org. All license expressions that contain unsupported license identifiers or license exception identifiers or that does not conform to license expression syntax are considered invalid.</span></span>

#### <a name="response"></a><span data-ttu-id="e40eb-124">Odpověď</span><span class="sxs-lookup"><span data-stu-id="e40eb-124">Response</span></span>

<span data-ttu-id="e40eb-125">Licenses.nuget.org reaguje na požadavky obsahující platné licenční výrazy se stavovým kódem HTTP 200 a webovou stránkou obsahující popis licenčního výrazu:</span><span class="sxs-lookup"><span data-stu-id="e40eb-125">Licenses.nuget.org responds to requests containing valid license expressions with an HTTP 200 status code and a web page containing a description of the license expression:</span></span>

* <span data-ttu-id="e40eb-126">pokud zadaný licenční výraz obsahuje jeden identifikátor licence, je vrácena webová stránka, která obsahuje tento referenční text licence;</span><span class="sxs-lookup"><span data-stu-id="e40eb-126">if supplied license expression contains a single license identifier a web page is returned that contains that license reference text;</span></span>
* <span data-ttu-id="e40eb-127">Pokud je zadaný licenční výraz složeným licenčním výrazem, je vrácena webová stránka obsahující licenční výraz s odkazy na jednotlivé licence nebo licence výjimky.</span><span class="sxs-lookup"><span data-stu-id="e40eb-127">if supplied license expression is a composite license expression, a web page is returned that contains the license expression with links to individual license or license exception references.</span></span>

<span data-ttu-id="e40eb-128">Všechny požadavky, které obsahují neplatný licenční výraz, mají za následek odpověď HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="e40eb-128">Any requests that contain an invalid license expression result in an HTTP 404 response.</span></span>

### <a name="license-exceptions"></a><span data-ttu-id="e40eb-129">Výjimky licencí</span><span class="sxs-lookup"><span data-stu-id="e40eb-129">License exceptions</span></span>

#### <a name="request"></a><span data-ttu-id="e40eb-130">Žádost</span><span class="sxs-lookup"><span data-stu-id="e40eb-130">Request</span></span>

<span data-ttu-id="e40eb-131">Identifikátory výjimek licence musí být kódovány adresou URL a použity jako cesta v žádosti o licenses.nuget.org. V jednom požadavku lze poskytnout pouze jeden identifikátor výjimky licence.</span><span class="sxs-lookup"><span data-stu-id="e40eb-131">License exception identifiers must be URL-encoded and used as a path in the request to licenses.nuget.org. Only a single license exception identifier can be supplied in a single request.</span></span> <span data-ttu-id="e40eb-132">V části cesty adresy URL se nesmí v části cesty k adrese URL nenasytit žádné další znaky kromě identifikátoru výjimky licence.</span><span class="sxs-lookup"><span data-stu-id="e40eb-132">No additional characters besides license exception identifier may present in the path portion of the URL.</span></span>

| <span data-ttu-id="e40eb-133">Identifikátor výjimky licence</span><span class="sxs-lookup"><span data-stu-id="e40eb-133">License exception identifier</span></span> | <span data-ttu-id="e40eb-134">Adresa URL, která má být</span><span class="sxs-lookup"><span data-stu-id="e40eb-134">URL to use</span></span> |
|:---|:---|
|<span data-ttu-id="e40eb-135">Výjimka FLTK</span><span class="sxs-lookup"><span data-stu-id="e40eb-135">FLTK-exception</span></span>            | <https://licenses.nuget.org/FLTK-exception> |
|<span data-ttu-id="e40eb-136">openvpn-openssl-výjimka</span><span class="sxs-lookup"><span data-stu-id="e40eb-136">openvpn-openssl-exception</span></span> | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a><span data-ttu-id="e40eb-137">Odpověď</span><span class="sxs-lookup"><span data-stu-id="e40eb-137">Response</span></span>

<span data-ttu-id="e40eb-138">Licenses.nuget.org odpoví na požadavek se známým identifikátorem výjimky licence s odpovědí HTTP 200 a webovou stránkou obsahující referenční text pro zadanou výjimku licence.</span><span class="sxs-lookup"><span data-stu-id="e40eb-138">Licenses.nuget.org responds to a request with a known license exception identifier with a HTTP 200 response and a web page containing the reference text for the specified license exception.</span></span>

<span data-ttu-id="e40eb-139">Jakýkoli požadavek obsahující nepodporovaný identifikátor výjimky licence má za následek odpověď HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="e40eb-139">Any request containing an unsupported license exception identifier results in an HTTP 404 response.</span></span>