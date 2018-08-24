---
title: Podpisy úložiště, rozhraní API Nugetu | Dokumentace Microsoftu
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 3/2/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Prostředek podpisy úložiště umožňuje klientům zdroje balíčků oznamujeme jejich úložiště podpis funkce.
keywords: Podpisy úložiště NuGet rozhraní API, nuget.org podpisové certifikáty, podepisování balíčků nuget.org
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 32dd2ee19261488a2b1b92724095a11ced69ae68
ms.sourcegitcommit: c643dd2c44e085601551ff7079d696bcc3ad2b49
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/21/2018
ms.locfileid: "42793608"
---
# <a name="repository-signatures"></a><span data-ttu-id="dcbe3-104">Podpisy úložiště</span><span class="sxs-lookup"><span data-stu-id="dcbe3-104">Repository signatures</span></span>

<span data-ttu-id="dcbe3-105">Pokud zdroj balíčku podporuje přidávání podpisy úložiště publikovaných balíčků, je možné pro klienta k určení podpisové certifikáty, které jsou používány zdroji balíčku.</span><span class="sxs-lookup"><span data-stu-id="dcbe3-105">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="dcbe3-106">Tento prostředek umožňuje klientům zjišťovat, zda úložiště podepsaný balíček byla změněna nebo má neočekávaný podpisový certifikát.</span><span class="sxs-lookup"><span data-stu-id="dcbe3-106">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="dcbe3-107">Prostředek, který používá pro načtení těchto informací podpisu úložiště je `RepositorySignatures` prostředek se nenašel v [index služby](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="dcbe3-107">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

> [!Note]
> <span data-ttu-id="dcbe3-108">NuGet.org se spustí oznámení `RepositorySignatures` prostředků v blízké budoucnosti.</span><span class="sxs-lookup"><span data-stu-id="dcbe3-108">NuGet.org will start announcing the `RepositorySignatures` resource in the near future.</span></span>

## <a name="versioning"></a><span data-ttu-id="dcbe3-109">Správa verzí</span><span class="sxs-lookup"><span data-stu-id="dcbe3-109">Versioning</span></span>

<span data-ttu-id="dcbe3-110">Následující `@type` hodnota se používá:</span><span class="sxs-lookup"><span data-stu-id="dcbe3-110">The following `@type` value is used:</span></span>

<span data-ttu-id="dcbe3-111">@type Hodnota</span><span class="sxs-lookup"><span data-stu-id="dcbe3-111">@type value</span></span>                | <span data-ttu-id="dcbe3-112">Poznámky</span><span class="sxs-lookup"><span data-stu-id="dcbe3-112">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="dcbe3-113">RepositorySignatures/4.7.0</span><span class="sxs-lookup"><span data-stu-id="dcbe3-113">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="dcbe3-114">Počáteční verze</span><span class="sxs-lookup"><span data-stu-id="dcbe3-114">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="dcbe3-115">Základní adresa URL</span><span class="sxs-lookup"><span data-stu-id="dcbe3-115">Base URL</span></span>

<span data-ttu-id="dcbe3-116">Adresa URL vstupního bodu pro následující rozhraní API je hodnota `@id` vlastnost přidružená k výše uvedených prostředků `@type` hodnotu.</span><span class="sxs-lookup"><span data-stu-id="dcbe3-116">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="dcbe3-117">Toto téma používá zástupné adresy URL `{@id}`.</span><span class="sxs-lookup"><span data-stu-id="dcbe3-117">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="dcbe3-118">Všimněte si, že na rozdíl od jiných prostředků `{@id}` adresa URL je potřeba zpracovat v přes protokol HTTPS.</span><span class="sxs-lookup"><span data-stu-id="dcbe3-118">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="dcbe3-119">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="dcbe3-119">HTTP methods</span></span>

<span data-ttu-id="dcbe3-120">Všechny adresy URL v metod podpory jenom HTTP prostředku podpisy úložiště `GET` a `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="dcbe3-120">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="dcbe3-121">Index podpisy úložiště</span><span class="sxs-lookup"><span data-stu-id="dcbe3-121">Repository signatures index</span></span>

<span data-ttu-id="dcbe3-122">Index podpisy úložiště obsahuje dva druhy údajů:</span><span class="sxs-lookup"><span data-stu-id="dcbe3-122">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="dcbe3-123">Jestli na zdroj nenašel všechny balíčky jsou úložiště, které jsou podepsány zdroje tohoto balíčku.</span><span class="sxs-lookup"><span data-stu-id="dcbe3-123">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="dcbe3-124">Seznam certifikátů používaného zdroje balíčku k podepisování balíčků.</span><span class="sxs-lookup"><span data-stu-id="dcbe3-124">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="dcbe3-125">Ve většině případů bude seznam certifikátů vždy jen připojeno k.</span><span class="sxs-lookup"><span data-stu-id="dcbe3-125">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="dcbe3-126">Nové certifikáty byly přidány do seznamu, pokud předchozí podpisový certifikát vypršela platnost a zdroj balíčku je potřeba začít používat nový podpisový certifikát.</span><span class="sxs-lookup"><span data-stu-id="dcbe3-126">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="dcbe3-127">Pokud je certifikát je odebrán ze seznamu, to znamená, že všechny podpisů balíčků, které jsou vytvořené pomocí odebrané podpisového certifikátu by už být uznán platnou klienta.</span><span class="sxs-lookup"><span data-stu-id="dcbe3-127">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="dcbe3-128">V takovém případě je neplatný podpis balíčku (ale ne nutně balíček).</span><span class="sxs-lookup"><span data-stu-id="dcbe3-128">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="dcbe3-129">Zásady klienta může povolit instalaci balíčku jako bez znaménka.</span><span class="sxs-lookup"><span data-stu-id="dcbe3-129">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="dcbe3-130">V případě zrušení certifikátů (třeba klíče ohrožení zabezpečení) zdroj balíčku by měl znovu podepsat všechny balíčky, které jsou podepsané certifikátem pro ovlivněné.</span><span class="sxs-lookup"><span data-stu-id="dcbe3-130">In the case of certificate revocation (e.g. key compromise), the package source is expected to re-sign all packages signed by the affected certificate.</span></span> <span data-ttu-id="dcbe3-131">Kromě toho by měl zdroj balíčku ovlivněné certifikát odebrat ze seznamu podpisový certifikát.</span><span class="sxs-lookup"><span data-stu-id="dcbe3-131">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="dcbe3-132">Následující požadavek načte index podpisy úložiště.</span><span class="sxs-lookup"><span data-stu-id="dcbe3-132">The following request fetches the repository signatures index.</span></span>

    GET {@id}

<span data-ttu-id="dcbe3-133">Signatura indexu úložiště je dokument JSON, který obsahuje objekt s následujícími vlastnostmi:</span><span class="sxs-lookup"><span data-stu-id="dcbe3-133">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="dcbe3-134">Název</span><span class="sxs-lookup"><span data-stu-id="dcbe3-134">Name</span></span>                | <span data-ttu-id="dcbe3-135">Typ</span><span class="sxs-lookup"><span data-stu-id="dcbe3-135">Type</span></span>             | <span data-ttu-id="dcbe3-136">Požadováno</span><span class="sxs-lookup"><span data-stu-id="dcbe3-136">Required</span></span>
------------------- | ---------------- | --------
<span data-ttu-id="dcbe3-137">allRepositorySigned</span><span class="sxs-lookup"><span data-stu-id="dcbe3-137">allRepositorySigned</span></span> | <span data-ttu-id="dcbe3-138">Logická hodnota</span><span class="sxs-lookup"><span data-stu-id="dcbe3-138">boolean</span></span>          | <span data-ttu-id="dcbe3-139">Ano</span><span class="sxs-lookup"><span data-stu-id="dcbe3-139">yes</span></span>
<span data-ttu-id="dcbe3-140">signingCertificates</span><span class="sxs-lookup"><span data-stu-id="dcbe3-140">signingCertificates</span></span> | <span data-ttu-id="dcbe3-141">Pole objektů</span><span class="sxs-lookup"><span data-stu-id="dcbe3-141">array of objects</span></span> | <span data-ttu-id="dcbe3-142">Ano</span><span class="sxs-lookup"><span data-stu-id="dcbe3-142">yes</span></span>

<span data-ttu-id="dcbe3-143">`allRepositorySigned` Logická hodnota je nastavena na hodnotu false, pokud zdroj balíčku má některé balíčky, které mají žádný podpis úložiště.</span><span class="sxs-lookup"><span data-stu-id="dcbe3-143">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="dcbe3-144">Pokud je nastavená hodnota true, všechny balíčky, které jsou k dispozici na datový typ boolean zdroje musí mít podpis úložiště vytvořeného pomocí jedné z podpisové certifikáty podle `signingCertificates`.</span><span class="sxs-lookup"><span data-stu-id="dcbe3-144">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

<span data-ttu-id="dcbe3-145">Měla by existovat jeden nebo více podpisové certifikáty v `signingCertificates` pole, pokud `allRepositorySigned` logická hodnota je nastavena na hodnotu true.</span><span class="sxs-lookup"><span data-stu-id="dcbe3-145">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="dcbe3-146">Pokud je pole prázdné a `allRepositorySigned` je nastavena na hodnotu true, všechny balíčky ze zdroje by měl být neplatná, i když se zásady klienta může stále povolit spotřebu balíčků.</span><span class="sxs-lookup"><span data-stu-id="dcbe3-146">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="dcbe3-147">Každý prvek v tomto poli je objekt JSON s následujícími vlastnostmi.</span><span class="sxs-lookup"><span data-stu-id="dcbe3-147">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="dcbe3-148">Název</span><span class="sxs-lookup"><span data-stu-id="dcbe3-148">Name</span></span>         | <span data-ttu-id="dcbe3-149">Typ</span><span class="sxs-lookup"><span data-stu-id="dcbe3-149">Type</span></span>   | <span data-ttu-id="dcbe3-150">Požadováno</span><span class="sxs-lookup"><span data-stu-id="dcbe3-150">Required</span></span> | <span data-ttu-id="dcbe3-151">Poznámky</span><span class="sxs-lookup"><span data-stu-id="dcbe3-151">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="dcbe3-152">contentUrl</span><span class="sxs-lookup"><span data-stu-id="dcbe3-152">contentUrl</span></span>   | <span data-ttu-id="dcbe3-153">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="dcbe3-153">string</span></span> | <span data-ttu-id="dcbe3-154">Ano</span><span class="sxs-lookup"><span data-stu-id="dcbe3-154">yes</span></span>      | <span data-ttu-id="dcbe3-155">Absolutní adresa URL pro kódování DER veřejný certifikát</span><span class="sxs-lookup"><span data-stu-id="dcbe3-155">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="dcbe3-156">otisky prstů</span><span class="sxs-lookup"><span data-stu-id="dcbe3-156">fingerprints</span></span> | <span data-ttu-id="dcbe3-157">odkazy objektů</span><span class="sxs-lookup"><span data-stu-id="dcbe3-157">object</span></span> | <span data-ttu-id="dcbe3-158">Ano</span><span class="sxs-lookup"><span data-stu-id="dcbe3-158">yes</span></span>      |
<span data-ttu-id="dcbe3-159">Předmět</span><span class="sxs-lookup"><span data-stu-id="dcbe3-159">subject</span></span>      | <span data-ttu-id="dcbe3-160">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="dcbe3-160">string</span></span> | <span data-ttu-id="dcbe3-161">Ano</span><span class="sxs-lookup"><span data-stu-id="dcbe3-161">yes</span></span>      | <span data-ttu-id="dcbe3-162">Rozlišující název subjektu z certifikátu</span><span class="sxs-lookup"><span data-stu-id="dcbe3-162">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="dcbe3-163">issuer</span><span class="sxs-lookup"><span data-stu-id="dcbe3-163">issuer</span></span>       | <span data-ttu-id="dcbe3-164">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="dcbe3-164">string</span></span> | <span data-ttu-id="dcbe3-165">Ano</span><span class="sxs-lookup"><span data-stu-id="dcbe3-165">yes</span></span>      | <span data-ttu-id="dcbe3-166">Rozlišující název vystavitele certifikátu</span><span class="sxs-lookup"><span data-stu-id="dcbe3-166">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="dcbe3-167">neplatí před</span><span class="sxs-lookup"><span data-stu-id="dcbe3-167">notBefore</span></span>    | <span data-ttu-id="dcbe3-168">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="dcbe3-168">string</span></span> | <span data-ttu-id="dcbe3-169">Ano</span><span class="sxs-lookup"><span data-stu-id="dcbe3-169">yes</span></span>      | <span data-ttu-id="dcbe3-170">Výchozí časové razítko období platnosti certifikátu</span><span class="sxs-lookup"><span data-stu-id="dcbe3-170">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="dcbe3-171">neplatí po</span><span class="sxs-lookup"><span data-stu-id="dcbe3-171">notAfter</span></span>     | <span data-ttu-id="dcbe3-172">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="dcbe3-172">string</span></span> | <span data-ttu-id="dcbe3-173">Ano</span><span class="sxs-lookup"><span data-stu-id="dcbe3-173">yes</span></span>      | <span data-ttu-id="dcbe3-174">Časové razítko koncové období platnosti certifikátu</span><span class="sxs-lookup"><span data-stu-id="dcbe3-174">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="dcbe3-175">Všimněte si, `contentUrl` je potřeba zpracovat v přes protokol HTTPS.</span><span class="sxs-lookup"><span data-stu-id="dcbe3-175">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="dcbe3-176">Tato adresa URL nemá žádné konkrétnímu vzor adresy URL a musí být zjištěny dynamicky, pomocí tohoto dokumentu indexu podpisy úložiště.</span><span class="sxs-lookup"><span data-stu-id="dcbe3-176">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="dcbe3-177">Všechny vlastnosti v tomto objektu (ze aside `contentUrl`) musí být derivable z certifikátu na `contentUrl`.</span><span class="sxs-lookup"><span data-stu-id="dcbe3-177">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="dcbe3-178">Tyto vlastnosti derivable jsou k dispozici jako usnadnění a minimalizovat výměny zpráv.</span><span class="sxs-lookup"><span data-stu-id="dcbe3-178">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="dcbe3-179">`fingerprints` Objektu má následující vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="dcbe3-179">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="dcbe3-180">Název</span><span class="sxs-lookup"><span data-stu-id="dcbe3-180">Name</span></span>                   | <span data-ttu-id="dcbe3-181">Typ</span><span class="sxs-lookup"><span data-stu-id="dcbe3-181">Type</span></span>   | <span data-ttu-id="dcbe3-182">Požadováno</span><span class="sxs-lookup"><span data-stu-id="dcbe3-182">Required</span></span> | <span data-ttu-id="dcbe3-183">Poznámky</span><span class="sxs-lookup"><span data-stu-id="dcbe3-183">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="dcbe3-184">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="dcbe3-184">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="dcbe3-185">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="dcbe3-185">string</span></span> | <span data-ttu-id="dcbe3-186">Ano</span><span class="sxs-lookup"><span data-stu-id="dcbe3-186">yes</span></span>      | <span data-ttu-id="dcbe3-187">Otisk SHA-256</span><span class="sxs-lookup"><span data-stu-id="dcbe3-187">The SHA-256 fingerprint</span></span>

<span data-ttu-id="dcbe3-188">Název klíče `2.16.840.1.101.3.4.2.1` je OID hashovací algoritmus SHA-256.</span><span class="sxs-lookup"><span data-stu-id="dcbe3-188">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="dcbe3-189">Všechny hodnoty hash musí být malými písmeny, šestnáctkově zakódovaného řetězcové reprezentace hodnoty hash výtahu.</span><span class="sxs-lookup"><span data-stu-id="dcbe3-189">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="dcbe3-190">Ukázková žádost</span><span class="sxs-lookup"><span data-stu-id="dcbe3-190">Sample request</span></span>

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a><span data-ttu-id="dcbe3-191">Ukázková odpověď</span><span class="sxs-lookup"><span data-stu-id="dcbe3-191">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
