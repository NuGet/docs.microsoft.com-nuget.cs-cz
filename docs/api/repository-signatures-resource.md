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
# <a name="repository-signatures"></a><span data-ttu-id="e4a5c-103">Podpisy úložiště</span><span class="sxs-lookup"><span data-stu-id="e4a5c-103">Repository signatures</span></span>

<span data-ttu-id="e4a5c-104">Pokud zdroj balíčku podporuje přidávání podpisů úložiště do publikovaných balíčků, může klient určit podpisové certifikáty používané zdrojem balíčku.</span><span class="sxs-lookup"><span data-stu-id="e4a5c-104">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="e4a5c-105">Tento prostředek umožňuje klientům zjistit, zda byl balíček podepsaný úložištěm zfalšován nebo má neočekávaný podpisový certifikát.</span><span class="sxs-lookup"><span data-stu-id="e4a5c-105">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="e4a5c-106">Prostředek, který se používá pro načtení informací o podpisu tohoto úložiště, je prostředek, který se `RepositorySignatures` našel v [indexu služby](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="e4a5c-106">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="e4a5c-107">Správa verzí</span><span class="sxs-lookup"><span data-stu-id="e4a5c-107">Versioning</span></span>

<span data-ttu-id="e4a5c-108">Použije se následující `@type` hodnota:</span><span class="sxs-lookup"><span data-stu-id="e4a5c-108">The following `@type` value is used:</span></span>

<span data-ttu-id="e4a5c-109">@type osa</span><span class="sxs-lookup"><span data-stu-id="e4a5c-109">@type value</span></span>                | <span data-ttu-id="e4a5c-110">Poznámky</span><span class="sxs-lookup"><span data-stu-id="e4a5c-110">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="e4a5c-111">RepositorySignatures/4.7.0</span><span class="sxs-lookup"><span data-stu-id="e4a5c-111">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="e4a5c-112">Počáteční verze</span><span class="sxs-lookup"><span data-stu-id="e4a5c-112">The initial release</span></span>
<span data-ttu-id="e4a5c-113">RepositorySignatures/4.9.0</span><span class="sxs-lookup"><span data-stu-id="e4a5c-113">RepositorySignatures/4.9.0</span></span> | <span data-ttu-id="e4a5c-114">Podporováno NuGet v 4.9 a klienty</span><span class="sxs-lookup"><span data-stu-id="e4a5c-114">Supported by NuGet v4.9+ clients</span></span>
<span data-ttu-id="e4a5c-115">RepositorySignatures/5.0.0</span><span class="sxs-lookup"><span data-stu-id="e4a5c-115">RepositorySignatures/5.0.0</span></span> | <span data-ttu-id="e4a5c-116">Povoluje povolení `allRepositorySigned` .</span><span class="sxs-lookup"><span data-stu-id="e4a5c-116">Allows enabling `allRepositorySigned`.</span></span> <span data-ttu-id="e4a5c-117">Podporováno klienty NuGet v 5.0 +</span><span class="sxs-lookup"><span data-stu-id="e4a5c-117">Supported by NuGet v5.0+ clients</span></span>

## <a name="base-url"></a><span data-ttu-id="e4a5c-118">Základní adresa URL</span><span class="sxs-lookup"><span data-stu-id="e4a5c-118">Base URL</span></span>

<span data-ttu-id="e4a5c-119">Adresa URL vstupního bodu pro následující rozhraní API je hodnota `@id` vlastnosti přidružené k uvedené `@type` hodnotě prostředku.</span><span class="sxs-lookup"><span data-stu-id="e4a5c-119">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="e4a5c-120">Toto téma používá zástupnou adresu URL `{@id}` .</span><span class="sxs-lookup"><span data-stu-id="e4a5c-120">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="e4a5c-121">Všimněte si, že na rozdíl od jiných prostředků musí `{@id}` být adresa URL obsluhována přes protokol HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e4a5c-121">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="e4a5c-122">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="e4a5c-122">HTTP methods</span></span>

<span data-ttu-id="e4a5c-123">Všechny adresy URL nalezené v prostředku signatury úložiště podporují pouze metody HTTP `GET` a `HEAD` .</span><span class="sxs-lookup"><span data-stu-id="e4a5c-123">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="e4a5c-124">Index podpisů úložiště</span><span class="sxs-lookup"><span data-stu-id="e4a5c-124">Repository signatures index</span></span>

<span data-ttu-id="e4a5c-125">Rejstřík podpisů úložiště obsahuje dvě části informací:</span><span class="sxs-lookup"><span data-stu-id="e4a5c-125">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="e4a5c-126">Bez ohledu na to, jestli jsou všechny balíčky nalezené ve zdroji úložiště podepsané tímto zdrojem balíčku</span><span class="sxs-lookup"><span data-stu-id="e4a5c-126">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="e4a5c-127">Seznam certifikátů používaných zdrojem balíčku k podepisování balíčků</span><span class="sxs-lookup"><span data-stu-id="e4a5c-127">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="e4a5c-128">Ve většině případů se seznam certifikátů připojí jenom k.</span><span class="sxs-lookup"><span data-stu-id="e4a5c-128">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="e4a5c-129">Do seznamu by se přidaly nové certifikáty, pokud vypršela platnost předchozího podpisového certifikátu a zdroj balíčku musí začít používat nový podpisový certifikát.</span><span class="sxs-lookup"><span data-stu-id="e4a5c-129">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="e4a5c-130">Pokud je certifikát ze seznamu odebraný, znamená to, že klient nebude moci považovat všechny signatury balíčků vytvořené s odebraným podpisovým certifikátem za platné.</span><span class="sxs-lookup"><span data-stu-id="e4a5c-130">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="e4a5c-131">V tomto případě je podpis balíčku (ale ne nutně balíček) neplatný.</span><span class="sxs-lookup"><span data-stu-id="e4a5c-131">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="e4a5c-132">Zásady klienta mohou umožňovat instalaci balíčku jako nepodepsaný.</span><span class="sxs-lookup"><span data-stu-id="e4a5c-132">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="e4a5c-133">V případě odvolání certifikátu (například ohrožení bezpečnosti klíče) se očekává, že zdroj balíčku znovu podepíše všechny balíčky podepsané ovlivněným certifikátem.</span><span class="sxs-lookup"><span data-stu-id="e4a5c-133">In the case of certificate revocation (e.g. key compromise), the package source is expected to re-sign all packages signed by the affected certificate.</span></span> <span data-ttu-id="e4a5c-134">Kromě toho by měl zdroj balíčku odebrat ovlivněný certifikát ze seznamu podpisového certifikátu.</span><span class="sxs-lookup"><span data-stu-id="e4a5c-134">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="e4a5c-135">Následující požadavek Načte index signatury úložiště.</span><span class="sxs-lookup"><span data-stu-id="e4a5c-135">The following request fetches the repository signatures index.</span></span>

```
GET {@id}
```

<span data-ttu-id="e4a5c-136">Index podpisu úložiště je dokument JSON, který obsahuje objekt s následujícími vlastnostmi:</span><span class="sxs-lookup"><span data-stu-id="e4a5c-136">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="e4a5c-137">Název</span><span class="sxs-lookup"><span data-stu-id="e4a5c-137">Name</span></span>                | <span data-ttu-id="e4a5c-138">Typ</span><span class="sxs-lookup"><span data-stu-id="e4a5c-138">Type</span></span>             | <span data-ttu-id="e4a5c-139">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="e4a5c-139">Required</span></span> | <span data-ttu-id="e4a5c-140">Poznámky</span><span class="sxs-lookup"><span data-stu-id="e4a5c-140">Notes</span></span>
------------------- | ---------------- | -------- | -----
<span data-ttu-id="e4a5c-141">allRepositorySigned</span><span class="sxs-lookup"><span data-stu-id="e4a5c-141">allRepositorySigned</span></span> | <span data-ttu-id="e4a5c-142">boolean</span><span class="sxs-lookup"><span data-stu-id="e4a5c-142">boolean</span></span>          | <span data-ttu-id="e4a5c-143">ano</span><span class="sxs-lookup"><span data-stu-id="e4a5c-143">yes</span></span>      | <span data-ttu-id="e4a5c-144">Musí se nacházet `false` v prostředcích 4.7.0 a 4.9.0.</span><span class="sxs-lookup"><span data-stu-id="e4a5c-144">Must be `false` on 4.7.0 and 4.9.0 resources</span></span>
<span data-ttu-id="e4a5c-145">signingCertificates</span><span class="sxs-lookup"><span data-stu-id="e4a5c-145">signingCertificates</span></span> | <span data-ttu-id="e4a5c-146">pole objektů</span><span class="sxs-lookup"><span data-stu-id="e4a5c-146">array of objects</span></span> | <span data-ttu-id="e4a5c-147">ano</span><span class="sxs-lookup"><span data-stu-id="e4a5c-147">yes</span></span>      | 

<span data-ttu-id="e4a5c-148">`allRepositorySigned`Logická hodnota je nastavená na false, pokud má zdroj balíčku nějaké balíčky, které nemají žádný podpis úložiště.</span><span class="sxs-lookup"><span data-stu-id="e4a5c-148">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="e4a5c-149">Pokud je logická hodnota nastavená na true, všechny balíčky, které jsou k dispozici ve zdroji, musí mít podpis úložiště vytvořený jedním z podpisových certifikátů uvedených v části `signingCertificates` .</span><span class="sxs-lookup"><span data-stu-id="e4a5c-149">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

> [!Warning]
> <span data-ttu-id="e4a5c-150">`allRepositorySigned`Logická hodnota musí mít hodnotu false u prostředků 4.7.0 a 4.9.0.</span><span class="sxs-lookup"><span data-stu-id="e4a5c-150">The `allRepositorySigned` boolean must be false on the 4.7.0 and 4.9.0 resources.</span></span> <span data-ttu-id="e4a5c-151">Klienti NuGet v 4.7, v 4.8 a v 4.9 nemůžou instalovat balíčky ze zdrojů, které mají `allRepositorySigned` nastavené na true.</span><span class="sxs-lookup"><span data-stu-id="e4a5c-151">NuGet v4.7, v4.8, and v4.9 clients cannot install packages from sources that have `allRepositorySigned` set to true.</span></span>

<span data-ttu-id="e4a5c-152">V poli musí být jeden nebo více podpisových certifikátů, `signingCertificates` Pokud `allRepositorySigned` je logická hodnota nastavena na true.</span><span class="sxs-lookup"><span data-stu-id="e4a5c-152">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="e4a5c-153">Pokud je pole prázdné a `allRepositorySigned` je nastaveno na hodnotu true, všechny balíčky ze zdroje by měly být považovány za neplatné, i když zásady klienta přesto mohou umožňovat spotřebu balíčků.</span><span class="sxs-lookup"><span data-stu-id="e4a5c-153">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="e4a5c-154">Každý prvek v tomto poli je objekt JSON s následujícími vlastnostmi.</span><span class="sxs-lookup"><span data-stu-id="e4a5c-154">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="e4a5c-155">Název</span><span class="sxs-lookup"><span data-stu-id="e4a5c-155">Name</span></span>         | <span data-ttu-id="e4a5c-156">Typ</span><span class="sxs-lookup"><span data-stu-id="e4a5c-156">Type</span></span>   | <span data-ttu-id="e4a5c-157">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="e4a5c-157">Required</span></span> | <span data-ttu-id="e4a5c-158">Poznámky</span><span class="sxs-lookup"><span data-stu-id="e4a5c-158">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="e4a5c-159">contentUrl</span><span class="sxs-lookup"><span data-stu-id="e4a5c-159">contentUrl</span></span>   | <span data-ttu-id="e4a5c-160">řetězec</span><span class="sxs-lookup"><span data-stu-id="e4a5c-160">string</span></span> | <span data-ttu-id="e4a5c-161">ano</span><span class="sxs-lookup"><span data-stu-id="e4a5c-161">yes</span></span>      | <span data-ttu-id="e4a5c-162">Absolutní adresa URL veřejného certifikátu kódovaného pomocí DER</span><span class="sxs-lookup"><span data-stu-id="e4a5c-162">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="e4a5c-163">otisky prstů</span><span class="sxs-lookup"><span data-stu-id="e4a5c-163">fingerprints</span></span> | <span data-ttu-id="e4a5c-164">object</span><span class="sxs-lookup"><span data-stu-id="e4a5c-164">object</span></span> | <span data-ttu-id="e4a5c-165">ano</span><span class="sxs-lookup"><span data-stu-id="e4a5c-165">yes</span></span>      |
<span data-ttu-id="e4a5c-166">subject</span><span class="sxs-lookup"><span data-stu-id="e4a5c-166">subject</span></span>      | <span data-ttu-id="e4a5c-167">řetězec</span><span class="sxs-lookup"><span data-stu-id="e4a5c-167">string</span></span> | <span data-ttu-id="e4a5c-168">ano</span><span class="sxs-lookup"><span data-stu-id="e4a5c-168">yes</span></span>      | <span data-ttu-id="e4a5c-169">Rozlišující název subjektu z certifikátu</span><span class="sxs-lookup"><span data-stu-id="e4a5c-169">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="e4a5c-170">issuer</span><span class="sxs-lookup"><span data-stu-id="e4a5c-170">issuer</span></span>       | <span data-ttu-id="e4a5c-171">řetězec</span><span class="sxs-lookup"><span data-stu-id="e4a5c-171">string</span></span> | <span data-ttu-id="e4a5c-172">ano</span><span class="sxs-lookup"><span data-stu-id="e4a5c-172">yes</span></span>      | <span data-ttu-id="e4a5c-173">Rozlišující název vystavitele certifikátu</span><span class="sxs-lookup"><span data-stu-id="e4a5c-173">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="e4a5c-174">notBefore</span><span class="sxs-lookup"><span data-stu-id="e4a5c-174">notBefore</span></span>    | <span data-ttu-id="e4a5c-175">řetězec</span><span class="sxs-lookup"><span data-stu-id="e4a5c-175">string</span></span> | <span data-ttu-id="e4a5c-176">ano</span><span class="sxs-lookup"><span data-stu-id="e4a5c-176">yes</span></span>      | <span data-ttu-id="e4a5c-177">Počáteční časové razítko období platnosti certifikátu</span><span class="sxs-lookup"><span data-stu-id="e4a5c-177">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="e4a5c-178">notAfter</span><span class="sxs-lookup"><span data-stu-id="e4a5c-178">notAfter</span></span>     | <span data-ttu-id="e4a5c-179">řetězec</span><span class="sxs-lookup"><span data-stu-id="e4a5c-179">string</span></span> | <span data-ttu-id="e4a5c-180">ano</span><span class="sxs-lookup"><span data-stu-id="e4a5c-180">yes</span></span>      | <span data-ttu-id="e4a5c-181">Koncové časové razítko období platnosti certifikátu</span><span class="sxs-lookup"><span data-stu-id="e4a5c-181">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="e4a5c-182">Všimněte si, že musí `contentUrl` být obsluhován přes protokol HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e4a5c-182">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="e4a5c-183">Tato adresa URL nemá žádný konkrétní vzor adresy URL a je nutné ji dynamicky zjistit pomocí tohoto dokumentu indexu podpisů úložiště.</span><span class="sxs-lookup"><span data-stu-id="e4a5c-183">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="e4a5c-184">Všechny vlastnosti v tomto objektu (kromě z `contentUrl` ) musí být odvozené z certifikátu, který najdete na adrese `contentUrl` .</span><span class="sxs-lookup"><span data-stu-id="e4a5c-184">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="e4a5c-185">Tyto odvozené vlastnosti jsou k dispozici jako pohodlí pro minimalizaci zpáteční cesty.</span><span class="sxs-lookup"><span data-stu-id="e4a5c-185">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="e4a5c-186">`fingerprints`Objekt má následující vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="e4a5c-186">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="e4a5c-187">Název</span><span class="sxs-lookup"><span data-stu-id="e4a5c-187">Name</span></span>                   | <span data-ttu-id="e4a5c-188">Typ</span><span class="sxs-lookup"><span data-stu-id="e4a5c-188">Type</span></span>   | <span data-ttu-id="e4a5c-189">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="e4a5c-189">Required</span></span> | <span data-ttu-id="e4a5c-190">Poznámky</span><span class="sxs-lookup"><span data-stu-id="e4a5c-190">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="e4a5c-191">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="e4a5c-191">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="e4a5c-192">řetězec</span><span class="sxs-lookup"><span data-stu-id="e4a5c-192">string</span></span> | <span data-ttu-id="e4a5c-193">ano</span><span class="sxs-lookup"><span data-stu-id="e4a5c-193">yes</span></span>      | <span data-ttu-id="e4a5c-194">Otisk SHA-256</span><span class="sxs-lookup"><span data-stu-id="e4a5c-194">The SHA-256 fingerprint</span></span>

<span data-ttu-id="e4a5c-195">Název klíče `2.16.840.1.101.3.4.2.1` je identifikátor OID algoritmu hash SHA-256.</span><span class="sxs-lookup"><span data-stu-id="e4a5c-195">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="e4a5c-196">Všechny hodnoty hash musí být malé, šestnáctkově zakódované řetězcové reprezentace algoritmu hash.</span><span class="sxs-lookup"><span data-stu-id="e4a5c-196">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="e4a5c-197">Ukázková žádost</span><span class="sxs-lookup"><span data-stu-id="e4a5c-197">Sample request</span></span>

```
GET https://api.nuget.org/v3-index/repository-signatures/index.json
```

### <a name="sample-response"></a><span data-ttu-id="e4a5c-198">Ukázková odpověď</span><span class="sxs-lookup"><span data-stu-id="e4a5c-198">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
