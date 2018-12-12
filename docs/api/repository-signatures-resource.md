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
ms.openlocfilehash: 81d32a7011268e45136e00cdb7345a95070aae06
ms.sourcegitcommit: be9c51b4b095aea40ef41bbea7e12ef0a194ee74
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/11/2018
ms.locfileid: "53248439"
---
# <a name="repository-signatures"></a><span data-ttu-id="cb475-103">Podpisy úložiště</span><span class="sxs-lookup"><span data-stu-id="cb475-103">Repository signatures</span></span>

<span data-ttu-id="cb475-104">Pokud zdroj balíčku podporuje přidávání podpisy úložiště publikovaných balíčků, je možné pro klienta k určení podpisové certifikáty, které jsou používány zdroji balíčku.</span><span class="sxs-lookup"><span data-stu-id="cb475-104">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="cb475-105">Tento prostředek umožňuje klientům zjišťovat, zda úložiště podepsaný balíček byla změněna nebo má neočekávaný podpisový certifikát.</span><span class="sxs-lookup"><span data-stu-id="cb475-105">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="cb475-106">Prostředek, který používá pro načtení těchto informací podpisu úložiště je `RepositorySignatures` prostředek se nenašel v [index služby](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="cb475-106">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="cb475-107">Správa verzí</span><span class="sxs-lookup"><span data-stu-id="cb475-107">Versioning</span></span>

<span data-ttu-id="cb475-108">Následující `@type` hodnota se používá:</span><span class="sxs-lookup"><span data-stu-id="cb475-108">The following `@type` value is used:</span></span>

<span data-ttu-id="cb475-109">@type Hodnota</span><span class="sxs-lookup"><span data-stu-id="cb475-109">@type value</span></span>                | <span data-ttu-id="cb475-110">Poznámky</span><span class="sxs-lookup"><span data-stu-id="cb475-110">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="cb475-111">RepositorySignatures/4.7.0</span><span class="sxs-lookup"><span data-stu-id="cb475-111">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="cb475-112">Počáteční verze</span><span class="sxs-lookup"><span data-stu-id="cb475-112">The initial release</span></span>
<span data-ttu-id="cb475-113">RepositorySignatures/4.9.0</span><span class="sxs-lookup"><span data-stu-id="cb475-113">RepositorySignatures/4.9.0</span></span> | <span data-ttu-id="cb475-114">Umožňuje povolení `allRepositorySigned`</span><span class="sxs-lookup"><span data-stu-id="cb475-114">Allows enabling `allRepositorySigned`</span></span>

## <a name="base-url"></a><span data-ttu-id="cb475-115">Základní adresa URL</span><span class="sxs-lookup"><span data-stu-id="cb475-115">Base URL</span></span>

<span data-ttu-id="cb475-116">Adresa URL vstupního bodu pro následující rozhraní API je hodnota `@id` vlastnost přidružená k výše uvedených prostředků `@type` hodnotu.</span><span class="sxs-lookup"><span data-stu-id="cb475-116">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="cb475-117">Toto téma používá zástupné adresy URL `{@id}`.</span><span class="sxs-lookup"><span data-stu-id="cb475-117">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="cb475-118">Všimněte si, že na rozdíl od jiných prostředků `{@id}` adresa URL je potřeba zpracovat v přes protokol HTTPS.</span><span class="sxs-lookup"><span data-stu-id="cb475-118">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="cb475-119">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="cb475-119">HTTP methods</span></span>

<span data-ttu-id="cb475-120">Všechny adresy URL v metod podpory jenom HTTP prostředku podpisy úložiště `GET` a `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="cb475-120">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="cb475-121">Index podpisy úložiště</span><span class="sxs-lookup"><span data-stu-id="cb475-121">Repository signatures index</span></span>

<span data-ttu-id="cb475-122">Index podpisy úložiště obsahuje dva druhy údajů:</span><span class="sxs-lookup"><span data-stu-id="cb475-122">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="cb475-123">Jestli na zdroj nenašel všechny balíčky jsou úložiště, které jsou podepsány zdroje tohoto balíčku.</span><span class="sxs-lookup"><span data-stu-id="cb475-123">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="cb475-124">Seznam certifikátů používaného zdroje balíčku k podepisování balíčků.</span><span class="sxs-lookup"><span data-stu-id="cb475-124">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="cb475-125">Ve většině případů bude seznam certifikátů vždy jen připojeno k.</span><span class="sxs-lookup"><span data-stu-id="cb475-125">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="cb475-126">Nové certifikáty byly přidány do seznamu, pokud předchozí podpisový certifikát vypršela platnost a zdroj balíčku je potřeba začít používat nový podpisový certifikát.</span><span class="sxs-lookup"><span data-stu-id="cb475-126">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="cb475-127">Pokud je certifikát je odebrán ze seznamu, to znamená, že všechny podpisů balíčků, které jsou vytvořené pomocí odebrané podpisového certifikátu by už být uznán platnou klienta.</span><span class="sxs-lookup"><span data-stu-id="cb475-127">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="cb475-128">V takovém případě je neplatný podpis balíčku (ale ne nutně balíček).</span><span class="sxs-lookup"><span data-stu-id="cb475-128">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="cb475-129">Zásady klienta může povolit instalaci balíčku jako bez znaménka.</span><span class="sxs-lookup"><span data-stu-id="cb475-129">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="cb475-130">V případě zrušení certifikátů (třeba klíče ohrožení zabezpečení) zdroj balíčku by měl znovu podepsat všechny balíčky, které jsou podepsané certifikátem pro ovlivněné.</span><span class="sxs-lookup"><span data-stu-id="cb475-130">In the case of certificate revocation (e.g. key compromise), the package source is expected to re-sign all packages signed by the affected certificate.</span></span> <span data-ttu-id="cb475-131">Kromě toho by měl zdroj balíčku ovlivněné certifikát odebrat ze seznamu podpisový certifikát.</span><span class="sxs-lookup"><span data-stu-id="cb475-131">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="cb475-132">Následující požadavek načte index podpisy úložiště.</span><span class="sxs-lookup"><span data-stu-id="cb475-132">The following request fetches the repository signatures index.</span></span>

    GET {@id}

<span data-ttu-id="cb475-133">Signatura indexu úložiště je dokument JSON, který obsahuje objekt s následujícími vlastnostmi:</span><span class="sxs-lookup"><span data-stu-id="cb475-133">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="cb475-134">Název</span><span class="sxs-lookup"><span data-stu-id="cb475-134">Name</span></span>                | <span data-ttu-id="cb475-135">Typ</span><span class="sxs-lookup"><span data-stu-id="cb475-135">Type</span></span>             | <span data-ttu-id="cb475-136">Požadováno</span><span class="sxs-lookup"><span data-stu-id="cb475-136">Required</span></span> | <span data-ttu-id="cb475-137">Poznámky</span><span class="sxs-lookup"><span data-stu-id="cb475-137">Notes</span></span>
------------------- | ---------------- | -------- | -----
<span data-ttu-id="cb475-138">allRepositorySigned</span><span class="sxs-lookup"><span data-stu-id="cb475-138">allRepositorySigned</span></span> | <span data-ttu-id="cb475-139">Logická hodnota</span><span class="sxs-lookup"><span data-stu-id="cb475-139">boolean</span></span>          | <span data-ttu-id="cb475-140">ano</span><span class="sxs-lookup"><span data-stu-id="cb475-140">yes</span></span>      | <span data-ttu-id="cb475-141">Musí být `false` na 4.7.0 prostředků</span><span class="sxs-lookup"><span data-stu-id="cb475-141">Must be `false` on 4.7.0 resource</span></span>
<span data-ttu-id="cb475-142">signingCertificates</span><span class="sxs-lookup"><span data-stu-id="cb475-142">signingCertificates</span></span> | <span data-ttu-id="cb475-143">Pole objektů</span><span class="sxs-lookup"><span data-stu-id="cb475-143">array of objects</span></span> | <span data-ttu-id="cb475-144">ano</span><span class="sxs-lookup"><span data-stu-id="cb475-144">yes</span></span>      | 

<span data-ttu-id="cb475-145">`allRepositorySigned` Logická hodnota je nastavena na hodnotu false, pokud zdroj balíčku má některé balíčky, které mají žádný podpis úložiště.</span><span class="sxs-lookup"><span data-stu-id="cb475-145">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="cb475-146">Pokud je nastavená hodnota true, všechny balíčky, které jsou k dispozici na datový typ boolean zdroje musí mít podpis úložiště vytvořeného pomocí jedné z podpisové certifikáty podle `signingCertificates`.</span><span class="sxs-lookup"><span data-stu-id="cb475-146">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

> [!Warning]
> <span data-ttu-id="cb475-147">`allRepositorySigned` Boolean musí mít hodnotu false na 4.7.0 prostředků.</span><span class="sxs-lookup"><span data-stu-id="cb475-147">The `allRepositorySigned` boolean must be false on the 4.7.0 resource.</span></span> <span data-ttu-id="cb475-148">Klienti NuGet v4.7 a v4.8 nelze nainstalovat balíčky ze zdrojů, které mají `allRepositorySigned` nastavenou na hodnotu true.</span><span class="sxs-lookup"><span data-stu-id="cb475-148">NuGet v4.7 and v4.8 clients cannot install packages from sources that have `allRepositorySigned` set to true.</span></span>

<span data-ttu-id="cb475-149">Měla by existovat jeden nebo více podpisové certifikáty v `signingCertificates` pole, pokud `allRepositorySigned` logická hodnota je nastavena na hodnotu true.</span><span class="sxs-lookup"><span data-stu-id="cb475-149">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="cb475-150">Pokud je pole prázdné a `allRepositorySigned` je nastavena na hodnotu true, všechny balíčky ze zdroje by měl být neplatná, i když se zásady klienta může stále povolit spotřebu balíčků.</span><span class="sxs-lookup"><span data-stu-id="cb475-150">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="cb475-151">Každý prvek v tomto poli je objekt JSON s následujícími vlastnostmi.</span><span class="sxs-lookup"><span data-stu-id="cb475-151">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="cb475-152">Název</span><span class="sxs-lookup"><span data-stu-id="cb475-152">Name</span></span>         | <span data-ttu-id="cb475-153">Typ</span><span class="sxs-lookup"><span data-stu-id="cb475-153">Type</span></span>   | <span data-ttu-id="cb475-154">Požadováno</span><span class="sxs-lookup"><span data-stu-id="cb475-154">Required</span></span> | <span data-ttu-id="cb475-155">Poznámky</span><span class="sxs-lookup"><span data-stu-id="cb475-155">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="cb475-156">contentUrl</span><span class="sxs-lookup"><span data-stu-id="cb475-156">contentUrl</span></span>   | <span data-ttu-id="cb475-157">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="cb475-157">string</span></span> | <span data-ttu-id="cb475-158">ano</span><span class="sxs-lookup"><span data-stu-id="cb475-158">yes</span></span>      | <span data-ttu-id="cb475-159">Absolutní adresa URL pro kódování DER veřejný certifikát</span><span class="sxs-lookup"><span data-stu-id="cb475-159">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="cb475-160">otisky prstů</span><span class="sxs-lookup"><span data-stu-id="cb475-160">fingerprints</span></span> | <span data-ttu-id="cb475-161">odkazy objektů</span><span class="sxs-lookup"><span data-stu-id="cb475-161">object</span></span> | <span data-ttu-id="cb475-162">ano</span><span class="sxs-lookup"><span data-stu-id="cb475-162">yes</span></span>      |
<span data-ttu-id="cb475-163">Předmět</span><span class="sxs-lookup"><span data-stu-id="cb475-163">subject</span></span>      | <span data-ttu-id="cb475-164">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="cb475-164">string</span></span> | <span data-ttu-id="cb475-165">ano</span><span class="sxs-lookup"><span data-stu-id="cb475-165">yes</span></span>      | <span data-ttu-id="cb475-166">Rozlišující název subjektu z certifikátu</span><span class="sxs-lookup"><span data-stu-id="cb475-166">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="cb475-167">issuer</span><span class="sxs-lookup"><span data-stu-id="cb475-167">issuer</span></span>       | <span data-ttu-id="cb475-168">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="cb475-168">string</span></span> | <span data-ttu-id="cb475-169">ano</span><span class="sxs-lookup"><span data-stu-id="cb475-169">yes</span></span>      | <span data-ttu-id="cb475-170">Rozlišující název vystavitele certifikátu</span><span class="sxs-lookup"><span data-stu-id="cb475-170">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="cb475-171">neplatí před</span><span class="sxs-lookup"><span data-stu-id="cb475-171">notBefore</span></span>    | <span data-ttu-id="cb475-172">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="cb475-172">string</span></span> | <span data-ttu-id="cb475-173">ano</span><span class="sxs-lookup"><span data-stu-id="cb475-173">yes</span></span>      | <span data-ttu-id="cb475-174">Výchozí časové razítko období platnosti certifikátu</span><span class="sxs-lookup"><span data-stu-id="cb475-174">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="cb475-175">neplatí po</span><span class="sxs-lookup"><span data-stu-id="cb475-175">notAfter</span></span>     | <span data-ttu-id="cb475-176">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="cb475-176">string</span></span> | <span data-ttu-id="cb475-177">ano</span><span class="sxs-lookup"><span data-stu-id="cb475-177">yes</span></span>      | <span data-ttu-id="cb475-178">Časové razítko koncové období platnosti certifikátu</span><span class="sxs-lookup"><span data-stu-id="cb475-178">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="cb475-179">Všimněte si, `contentUrl` je potřeba zpracovat v přes protokol HTTPS.</span><span class="sxs-lookup"><span data-stu-id="cb475-179">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="cb475-180">Tato adresa URL nemá žádné konkrétnímu vzor adresy URL a musí být zjištěny dynamicky, pomocí tohoto dokumentu indexu podpisy úložiště.</span><span class="sxs-lookup"><span data-stu-id="cb475-180">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="cb475-181">Všechny vlastnosti v tomto objektu (ze aside `contentUrl`) musí být derivable z certifikátu na `contentUrl`.</span><span class="sxs-lookup"><span data-stu-id="cb475-181">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="cb475-182">Tyto vlastnosti derivable jsou k dispozici jako usnadnění a minimalizovat výměny zpráv.</span><span class="sxs-lookup"><span data-stu-id="cb475-182">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="cb475-183">`fingerprints` Objektu má následující vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="cb475-183">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="cb475-184">Název</span><span class="sxs-lookup"><span data-stu-id="cb475-184">Name</span></span>                   | <span data-ttu-id="cb475-185">Typ</span><span class="sxs-lookup"><span data-stu-id="cb475-185">Type</span></span>   | <span data-ttu-id="cb475-186">Požadováno</span><span class="sxs-lookup"><span data-stu-id="cb475-186">Required</span></span> | <span data-ttu-id="cb475-187">Poznámky</span><span class="sxs-lookup"><span data-stu-id="cb475-187">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="cb475-188">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="cb475-188">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="cb475-189">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="cb475-189">string</span></span> | <span data-ttu-id="cb475-190">ano</span><span class="sxs-lookup"><span data-stu-id="cb475-190">yes</span></span>      | <span data-ttu-id="cb475-191">Otisk SHA-256</span><span class="sxs-lookup"><span data-stu-id="cb475-191">The SHA-256 fingerprint</span></span>

<span data-ttu-id="cb475-192">Název klíče `2.16.840.1.101.3.4.2.1` je OID hashovací algoritmus SHA-256.</span><span class="sxs-lookup"><span data-stu-id="cb475-192">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="cb475-193">Všechny hodnoty hash musí být malými písmeny, šestnáctkově zakódovaného řetězcové reprezentace hodnoty hash výtahu.</span><span class="sxs-lookup"><span data-stu-id="cb475-193">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="cb475-194">Ukázková žádost</span><span class="sxs-lookup"><span data-stu-id="cb475-194">Sample request</span></span>

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a><span data-ttu-id="cb475-195">Ukázková odpověď</span><span class="sxs-lookup"><span data-stu-id="cb475-195">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
