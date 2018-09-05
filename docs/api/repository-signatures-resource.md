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
ms.openlocfilehash: 50f309b99d4bf59e14f3e29b6b0421d8c3e8aa5a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547978"
---
# <a name="repository-signatures"></a><span data-ttu-id="f8c42-103">Podpisy úložiště</span><span class="sxs-lookup"><span data-stu-id="f8c42-103">Repository signatures</span></span>

<span data-ttu-id="f8c42-104">Pokud zdroj balíčku podporuje přidávání podpisy úložiště publikovaných balíčků, je možné pro klienta k určení podpisové certifikáty, které jsou používány zdroji balíčku.</span><span class="sxs-lookup"><span data-stu-id="f8c42-104">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="f8c42-105">Tento prostředek umožňuje klientům zjišťovat, zda úložiště podepsaný balíček byla změněna nebo má neočekávaný podpisový certifikát.</span><span class="sxs-lookup"><span data-stu-id="f8c42-105">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="f8c42-106">Prostředek, který používá pro načtení těchto informací podpisu úložiště je `RepositorySignatures` prostředek se nenašel v [index služby](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="f8c42-106">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

> [!Note]
> <span data-ttu-id="f8c42-107">NuGet.org se spustí oznámení `RepositorySignatures` prostředků v blízké budoucnosti.</span><span class="sxs-lookup"><span data-stu-id="f8c42-107">NuGet.org will start announcing the `RepositorySignatures` resource in the near future.</span></span>

## <a name="versioning"></a><span data-ttu-id="f8c42-108">Správa verzí</span><span class="sxs-lookup"><span data-stu-id="f8c42-108">Versioning</span></span>

<span data-ttu-id="f8c42-109">Následující `@type` hodnota se používá:</span><span class="sxs-lookup"><span data-stu-id="f8c42-109">The following `@type` value is used:</span></span>

<span data-ttu-id="f8c42-110">@type Hodnota</span><span class="sxs-lookup"><span data-stu-id="f8c42-110">@type value</span></span>                | <span data-ttu-id="f8c42-111">Poznámky</span><span class="sxs-lookup"><span data-stu-id="f8c42-111">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="f8c42-112">RepositorySignatures/4.7.0</span><span class="sxs-lookup"><span data-stu-id="f8c42-112">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="f8c42-113">Počáteční verze</span><span class="sxs-lookup"><span data-stu-id="f8c42-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="f8c42-114">Základní adresa URL</span><span class="sxs-lookup"><span data-stu-id="f8c42-114">Base URL</span></span>

<span data-ttu-id="f8c42-115">Adresa URL vstupního bodu pro následující rozhraní API je hodnota `@id` vlastnost přidružená k výše uvedených prostředků `@type` hodnotu.</span><span class="sxs-lookup"><span data-stu-id="f8c42-115">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="f8c42-116">Toto téma používá zástupné adresy URL `{@id}`.</span><span class="sxs-lookup"><span data-stu-id="f8c42-116">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="f8c42-117">Všimněte si, že na rozdíl od jiných prostředků `{@id}` adresa URL je potřeba zpracovat v přes protokol HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f8c42-117">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="f8c42-118">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="f8c42-118">HTTP methods</span></span>

<span data-ttu-id="f8c42-119">Všechny adresy URL v metod podpory jenom HTTP prostředku podpisy úložiště `GET` a `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="f8c42-119">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="f8c42-120">Index podpisy úložiště</span><span class="sxs-lookup"><span data-stu-id="f8c42-120">Repository signatures index</span></span>

<span data-ttu-id="f8c42-121">Index podpisy úložiště obsahuje dva druhy údajů:</span><span class="sxs-lookup"><span data-stu-id="f8c42-121">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="f8c42-122">Jestli na zdroj nenašel všechny balíčky jsou úložiště, které jsou podepsány zdroje tohoto balíčku.</span><span class="sxs-lookup"><span data-stu-id="f8c42-122">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="f8c42-123">Seznam certifikátů používaného zdroje balíčku k podepisování balíčků.</span><span class="sxs-lookup"><span data-stu-id="f8c42-123">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="f8c42-124">Ve většině případů bude seznam certifikátů vždy jen připojeno k.</span><span class="sxs-lookup"><span data-stu-id="f8c42-124">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="f8c42-125">Nové certifikáty byly přidány do seznamu, pokud předchozí podpisový certifikát vypršela platnost a zdroj balíčku je potřeba začít používat nový podpisový certifikát.</span><span class="sxs-lookup"><span data-stu-id="f8c42-125">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="f8c42-126">Pokud je certifikát je odebrán ze seznamu, to znamená, že všechny podpisů balíčků, které jsou vytvořené pomocí odebrané podpisového certifikátu by už být uznán platnou klienta.</span><span class="sxs-lookup"><span data-stu-id="f8c42-126">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="f8c42-127">V takovém případě je neplatný podpis balíčku (ale ne nutně balíček).</span><span class="sxs-lookup"><span data-stu-id="f8c42-127">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="f8c42-128">Zásady klienta může povolit instalaci balíčku jako bez znaménka.</span><span class="sxs-lookup"><span data-stu-id="f8c42-128">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="f8c42-129">V případě zrušení certifikátů (třeba klíče ohrožení zabezpečení) zdroj balíčku by měl znovu podepsat všechny balíčky, které jsou podepsané certifikátem pro ovlivněné.</span><span class="sxs-lookup"><span data-stu-id="f8c42-129">In the case of certificate revocation (e.g. key compromise), the package source is expected to re-sign all packages signed by the affected certificate.</span></span> <span data-ttu-id="f8c42-130">Kromě toho by měl zdroj balíčku ovlivněné certifikát odebrat ze seznamu podpisový certifikát.</span><span class="sxs-lookup"><span data-stu-id="f8c42-130">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="f8c42-131">Následující požadavek načte index podpisy úložiště.</span><span class="sxs-lookup"><span data-stu-id="f8c42-131">The following request fetches the repository signatures index.</span></span>

    GET {@id}

<span data-ttu-id="f8c42-132">Signatura indexu úložiště je dokument JSON, který obsahuje objekt s následujícími vlastnostmi:</span><span class="sxs-lookup"><span data-stu-id="f8c42-132">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="f8c42-133">Název</span><span class="sxs-lookup"><span data-stu-id="f8c42-133">Name</span></span>                | <span data-ttu-id="f8c42-134">Typ</span><span class="sxs-lookup"><span data-stu-id="f8c42-134">Type</span></span>             | <span data-ttu-id="f8c42-135">Požadováno</span><span class="sxs-lookup"><span data-stu-id="f8c42-135">Required</span></span>
------------------- | ---------------- | --------
<span data-ttu-id="f8c42-136">allRepositorySigned</span><span class="sxs-lookup"><span data-stu-id="f8c42-136">allRepositorySigned</span></span> | <span data-ttu-id="f8c42-137">Logická hodnota</span><span class="sxs-lookup"><span data-stu-id="f8c42-137">boolean</span></span>          | <span data-ttu-id="f8c42-138">Ano</span><span class="sxs-lookup"><span data-stu-id="f8c42-138">yes</span></span>
<span data-ttu-id="f8c42-139">signingCertificates</span><span class="sxs-lookup"><span data-stu-id="f8c42-139">signingCertificates</span></span> | <span data-ttu-id="f8c42-140">Pole objektů</span><span class="sxs-lookup"><span data-stu-id="f8c42-140">array of objects</span></span> | <span data-ttu-id="f8c42-141">Ano</span><span class="sxs-lookup"><span data-stu-id="f8c42-141">yes</span></span>

<span data-ttu-id="f8c42-142">`allRepositorySigned` Logická hodnota je nastavena na hodnotu false, pokud zdroj balíčku má některé balíčky, které mají žádný podpis úložiště.</span><span class="sxs-lookup"><span data-stu-id="f8c42-142">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="f8c42-143">Pokud je nastavená hodnota true, všechny balíčky, které jsou k dispozici na datový typ boolean zdroje musí mít podpis úložiště vytvořeného pomocí jedné z podpisové certifikáty podle `signingCertificates`.</span><span class="sxs-lookup"><span data-stu-id="f8c42-143">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

<span data-ttu-id="f8c42-144">Měla by existovat jeden nebo více podpisové certifikáty v `signingCertificates` pole, pokud `allRepositorySigned` logická hodnota je nastavena na hodnotu true.</span><span class="sxs-lookup"><span data-stu-id="f8c42-144">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="f8c42-145">Pokud je pole prázdné a `allRepositorySigned` je nastavena na hodnotu true, všechny balíčky ze zdroje by měl být neplatná, i když se zásady klienta může stále povolit spotřebu balíčků.</span><span class="sxs-lookup"><span data-stu-id="f8c42-145">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="f8c42-146">Každý prvek v tomto poli je objekt JSON s následujícími vlastnostmi.</span><span class="sxs-lookup"><span data-stu-id="f8c42-146">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="f8c42-147">Název</span><span class="sxs-lookup"><span data-stu-id="f8c42-147">Name</span></span>         | <span data-ttu-id="f8c42-148">Typ</span><span class="sxs-lookup"><span data-stu-id="f8c42-148">Type</span></span>   | <span data-ttu-id="f8c42-149">Požadováno</span><span class="sxs-lookup"><span data-stu-id="f8c42-149">Required</span></span> | <span data-ttu-id="f8c42-150">Poznámky</span><span class="sxs-lookup"><span data-stu-id="f8c42-150">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="f8c42-151">contentUrl</span><span class="sxs-lookup"><span data-stu-id="f8c42-151">contentUrl</span></span>   | <span data-ttu-id="f8c42-152">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="f8c42-152">string</span></span> | <span data-ttu-id="f8c42-153">Ano</span><span class="sxs-lookup"><span data-stu-id="f8c42-153">yes</span></span>      | <span data-ttu-id="f8c42-154">Absolutní adresa URL pro kódování DER veřejný certifikát</span><span class="sxs-lookup"><span data-stu-id="f8c42-154">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="f8c42-155">otisky prstů</span><span class="sxs-lookup"><span data-stu-id="f8c42-155">fingerprints</span></span> | <span data-ttu-id="f8c42-156">odkazy objektů</span><span class="sxs-lookup"><span data-stu-id="f8c42-156">object</span></span> | <span data-ttu-id="f8c42-157">Ano</span><span class="sxs-lookup"><span data-stu-id="f8c42-157">yes</span></span>      |
<span data-ttu-id="f8c42-158">Předmět</span><span class="sxs-lookup"><span data-stu-id="f8c42-158">subject</span></span>      | <span data-ttu-id="f8c42-159">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="f8c42-159">string</span></span> | <span data-ttu-id="f8c42-160">Ano</span><span class="sxs-lookup"><span data-stu-id="f8c42-160">yes</span></span>      | <span data-ttu-id="f8c42-161">Rozlišující název subjektu z certifikátu</span><span class="sxs-lookup"><span data-stu-id="f8c42-161">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="f8c42-162">issuer</span><span class="sxs-lookup"><span data-stu-id="f8c42-162">issuer</span></span>       | <span data-ttu-id="f8c42-163">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="f8c42-163">string</span></span> | <span data-ttu-id="f8c42-164">Ano</span><span class="sxs-lookup"><span data-stu-id="f8c42-164">yes</span></span>      | <span data-ttu-id="f8c42-165">Rozlišující název vystavitele certifikátu</span><span class="sxs-lookup"><span data-stu-id="f8c42-165">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="f8c42-166">neplatí před</span><span class="sxs-lookup"><span data-stu-id="f8c42-166">notBefore</span></span>    | <span data-ttu-id="f8c42-167">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="f8c42-167">string</span></span> | <span data-ttu-id="f8c42-168">Ano</span><span class="sxs-lookup"><span data-stu-id="f8c42-168">yes</span></span>      | <span data-ttu-id="f8c42-169">Výchozí časové razítko období platnosti certifikátu</span><span class="sxs-lookup"><span data-stu-id="f8c42-169">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="f8c42-170">neplatí po</span><span class="sxs-lookup"><span data-stu-id="f8c42-170">notAfter</span></span>     | <span data-ttu-id="f8c42-171">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="f8c42-171">string</span></span> | <span data-ttu-id="f8c42-172">Ano</span><span class="sxs-lookup"><span data-stu-id="f8c42-172">yes</span></span>      | <span data-ttu-id="f8c42-173">Časové razítko koncové období platnosti certifikátu</span><span class="sxs-lookup"><span data-stu-id="f8c42-173">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="f8c42-174">Všimněte si, `contentUrl` je potřeba zpracovat v přes protokol HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f8c42-174">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="f8c42-175">Tato adresa URL nemá žádné konkrétnímu vzor adresy URL a musí být zjištěny dynamicky, pomocí tohoto dokumentu indexu podpisy úložiště.</span><span class="sxs-lookup"><span data-stu-id="f8c42-175">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="f8c42-176">Všechny vlastnosti v tomto objektu (ze aside `contentUrl`) musí být derivable z certifikátu na `contentUrl`.</span><span class="sxs-lookup"><span data-stu-id="f8c42-176">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="f8c42-177">Tyto vlastnosti derivable jsou k dispozici jako usnadnění a minimalizovat výměny zpráv.</span><span class="sxs-lookup"><span data-stu-id="f8c42-177">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="f8c42-178">`fingerprints` Objektu má následující vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="f8c42-178">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="f8c42-179">Název</span><span class="sxs-lookup"><span data-stu-id="f8c42-179">Name</span></span>                   | <span data-ttu-id="f8c42-180">Typ</span><span class="sxs-lookup"><span data-stu-id="f8c42-180">Type</span></span>   | <span data-ttu-id="f8c42-181">Požadováno</span><span class="sxs-lookup"><span data-stu-id="f8c42-181">Required</span></span> | <span data-ttu-id="f8c42-182">Poznámky</span><span class="sxs-lookup"><span data-stu-id="f8c42-182">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="f8c42-183">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="f8c42-183">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="f8c42-184">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="f8c42-184">string</span></span> | <span data-ttu-id="f8c42-185">Ano</span><span class="sxs-lookup"><span data-stu-id="f8c42-185">yes</span></span>      | <span data-ttu-id="f8c42-186">Otisk SHA-256</span><span class="sxs-lookup"><span data-stu-id="f8c42-186">The SHA-256 fingerprint</span></span>

<span data-ttu-id="f8c42-187">Název klíče `2.16.840.1.101.3.4.2.1` je OID hashovací algoritmus SHA-256.</span><span class="sxs-lookup"><span data-stu-id="f8c42-187">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="f8c42-188">Všechny hodnoty hash musí být malými písmeny, šestnáctkově zakódovaného řetězcové reprezentace hodnoty hash výtahu.</span><span class="sxs-lookup"><span data-stu-id="f8c42-188">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="f8c42-189">Ukázková žádost</span><span class="sxs-lookup"><span data-stu-id="f8c42-189">Sample request</span></span>

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a><span data-ttu-id="f8c42-190">Ukázková odpověď</span><span class="sxs-lookup"><span data-stu-id="f8c42-190">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
