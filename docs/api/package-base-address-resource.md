---
title: Obsah balíčku, rozhraní API NuGet
description: Základní adresa balíčku je jednoduché rozhraní pro načtení samotného balíčku.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 8ea03ece635aa06e22032c4fb43ce932dbdf717c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773937"
---
# <a name="package-content"></a><span data-ttu-id="45025-103">Obsah balíčku</span><span class="sxs-lookup"><span data-stu-id="45025-103">Package Content</span></span>

<span data-ttu-id="45025-104">Je možné vygenerovat adresu URL pro načtení obsahu libovolného balíčku (soubor. nupkg) pomocí rozhraní V3 API.</span><span class="sxs-lookup"><span data-stu-id="45025-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="45025-105">Prostředek, který se používá pro načítání obsahu balíčku, je prostředek, který se `PackageBaseAddress` našel v [indexu služby](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="45025-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="45025-106">Tento prostředek také umožňuje zjišťování všech verzí balíčku uvedených v seznamu nebo bez jeho uvedení na seznamu.</span><span class="sxs-lookup"><span data-stu-id="45025-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="45025-107">Tento prostředek se běžně označuje jako základní adresa balíčku nebo jako "plochý kontejner".</span><span class="sxs-lookup"><span data-stu-id="45025-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="45025-108">Správa verzí</span><span class="sxs-lookup"><span data-stu-id="45025-108">Versioning</span></span>

<span data-ttu-id="45025-109">Použije se následující `@type` hodnota:</span><span class="sxs-lookup"><span data-stu-id="45025-109">The following `@type` value is used:</span></span>

<span data-ttu-id="45025-110">@type osa</span><span class="sxs-lookup"><span data-stu-id="45025-110">@type value</span></span>              | <span data-ttu-id="45025-111">Poznámky</span><span class="sxs-lookup"><span data-stu-id="45025-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="45025-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="45025-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="45025-113">Počáteční verze</span><span class="sxs-lookup"><span data-stu-id="45025-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="45025-114">Základní adresa URL</span><span class="sxs-lookup"><span data-stu-id="45025-114">Base URL</span></span>

<span data-ttu-id="45025-115">Základní adresa URL následujících rozhraní API je hodnota `@id` vlastnosti přidružené k uvedené `@type` hodnotě prostředku.</span><span class="sxs-lookup"><span data-stu-id="45025-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="45025-116">V následujícím dokumentu se použije zástupná základní adresa URL `{@id}` .</span><span class="sxs-lookup"><span data-stu-id="45025-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="45025-117">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="45025-117">HTTP methods</span></span>

<span data-ttu-id="45025-118">Všechny adresy URL nalezené v registračním prostředku podporují metody HTTP `GET` a `HEAD` .</span><span class="sxs-lookup"><span data-stu-id="45025-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="45025-119">Zobrazení výčtu verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="45025-119">Enumerate package versions</span></span>

<span data-ttu-id="45025-120">Pokud klient zná ID balíčku a chce zjistit, které verze balíčků má zdroj balíčku k dispozici, může klient sestavit předvídatelné adresy URL pro zobrazení výčtu všech verzí balíčků.</span><span class="sxs-lookup"><span data-stu-id="45025-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="45025-121">Tento seznam má být "výpis adresáře" pro rozhraní API obsahu balíčku, který je uveden níže.</span><span class="sxs-lookup"><span data-stu-id="45025-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="45025-122">Tento seznam obsahuje uvedené i neuvedené verze balíčků.</span><span class="sxs-lookup"><span data-stu-id="45025-122">This list contains both listed and unlisted package versions.</span></span>

```
GET {@id}/{LOWER_ID}/index.json
```

### <a name="request-parameters"></a><span data-ttu-id="45025-123">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="45025-123">Request parameters</span></span>

<span data-ttu-id="45025-124">Name</span><span class="sxs-lookup"><span data-stu-id="45025-124">Name</span></span>     | <span data-ttu-id="45025-125">V</span><span class="sxs-lookup"><span data-stu-id="45025-125">In</span></span>     | <span data-ttu-id="45025-126">Typ</span><span class="sxs-lookup"><span data-stu-id="45025-126">Type</span></span>    | <span data-ttu-id="45025-127">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="45025-127">Required</span></span> | <span data-ttu-id="45025-128">Poznámky</span><span class="sxs-lookup"><span data-stu-id="45025-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="45025-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="45025-129">LOWER_ID</span></span> | <span data-ttu-id="45025-130">URL</span><span class="sxs-lookup"><span data-stu-id="45025-130">URL</span></span>    | <span data-ttu-id="45025-131">řetězec</span><span class="sxs-lookup"><span data-stu-id="45025-131">string</span></span>  | <span data-ttu-id="45025-132">ano</span><span class="sxs-lookup"><span data-stu-id="45025-132">yes</span></span>      | <span data-ttu-id="45025-133">ID balíčku, malými písmeny</span><span class="sxs-lookup"><span data-stu-id="45025-133">The package ID, lowercased</span></span>

<span data-ttu-id="45025-134">`LOWER_ID`Hodnota je ID požadovaného balíčku s malými písmeny pomocí pravidel implementovaných pomocí. Metoda netto [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true) .</span><span class="sxs-lookup"><span data-stu-id="45025-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true) method.</span></span>

### <a name="response"></a><span data-ttu-id="45025-135">Odpověď</span><span class="sxs-lookup"><span data-stu-id="45025-135">Response</span></span>

<span data-ttu-id="45025-136">Pokud zdroj balíčku nemá žádné verze zadaného ID balíčku, vrátí se stavový kód 404.</span><span class="sxs-lookup"><span data-stu-id="45025-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="45025-137">Pokud má zdroj balíčku jednu nebo více verzí, vrátí se stavový kód 200.</span><span class="sxs-lookup"><span data-stu-id="45025-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="45025-138">Tělo odpovědi je objekt JSON s následující vlastností:</span><span class="sxs-lookup"><span data-stu-id="45025-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="45025-139">Název</span><span class="sxs-lookup"><span data-stu-id="45025-139">Name</span></span>     | <span data-ttu-id="45025-140">Typ</span><span class="sxs-lookup"><span data-stu-id="45025-140">Type</span></span>             | <span data-ttu-id="45025-141">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="45025-141">Required</span></span> | <span data-ttu-id="45025-142">Poznámky</span><span class="sxs-lookup"><span data-stu-id="45025-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="45025-143">verze</span><span class="sxs-lookup"><span data-stu-id="45025-143">versions</span></span> | <span data-ttu-id="45025-144">pole řetězců</span><span class="sxs-lookup"><span data-stu-id="45025-144">array of strings</span></span> | <span data-ttu-id="45025-145">ano</span><span class="sxs-lookup"><span data-stu-id="45025-145">yes</span></span>      | <span data-ttu-id="45025-146">Dostupné verze</span><span class="sxs-lookup"><span data-stu-id="45025-146">The versions available</span></span>

<span data-ttu-id="45025-147">Řetězce v `versions` poli jsou všechny s malými písmeny, [normalizované řetězce verze NuGet](../concepts/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="45025-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="45025-148">Řetězce verze neobsahují žádná metadata buildu SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="45025-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="45025-149">Záměrem je, aby se pro tokeny, které se `LOWER_VERSION` nacházejí v následujících koncových bodech, používaly doslovné řetězce verze v tomto poli.</span><span class="sxs-lookup"><span data-stu-id="45025-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="45025-150">Ukázková žádost</span><span class="sxs-lookup"><span data-stu-id="45025-150">Sample request</span></span>

```
GET https://api.nuget.org/v3-flatcontainer/owin/index.json
```

### <a name="sample-response"></a><span data-ttu-id="45025-151">Ukázková odpověď</span><span class="sxs-lookup"><span data-stu-id="45025-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="45025-152">Stáhnout obsah balíčku (. nupkg)</span><span class="sxs-lookup"><span data-stu-id="45025-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="45025-153">Pokud klient zná ID a verzi balíčku a chce stáhnout obsah balíčku, stačí vytvořit následující adresu URL:</span><span class="sxs-lookup"><span data-stu-id="45025-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

```
GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg
```

### <a name="request-parameters"></a><span data-ttu-id="45025-154">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="45025-154">Request parameters</span></span>

<span data-ttu-id="45025-155">Name</span><span class="sxs-lookup"><span data-stu-id="45025-155">Name</span></span>          | <span data-ttu-id="45025-156">V</span><span class="sxs-lookup"><span data-stu-id="45025-156">In</span></span>     | <span data-ttu-id="45025-157">Typ</span><span class="sxs-lookup"><span data-stu-id="45025-157">Type</span></span>   | <span data-ttu-id="45025-158">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="45025-158">Required</span></span> | <span data-ttu-id="45025-159">Poznámky</span><span class="sxs-lookup"><span data-stu-id="45025-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="45025-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="45025-160">LOWER_ID</span></span>      | <span data-ttu-id="45025-161">URL</span><span class="sxs-lookup"><span data-stu-id="45025-161">URL</span></span>    | <span data-ttu-id="45025-162">řetězec</span><span class="sxs-lookup"><span data-stu-id="45025-162">string</span></span> | <span data-ttu-id="45025-163">ano</span><span class="sxs-lookup"><span data-stu-id="45025-163">yes</span></span>      | <span data-ttu-id="45025-164">ID balíčku, malá písmena</span><span class="sxs-lookup"><span data-stu-id="45025-164">The package ID, lowercase</span></span>
<span data-ttu-id="45025-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="45025-165">LOWER_VERSION</span></span> | <span data-ttu-id="45025-166">URL</span><span class="sxs-lookup"><span data-stu-id="45025-166">URL</span></span>    | <span data-ttu-id="45025-167">řetězec</span><span class="sxs-lookup"><span data-stu-id="45025-167">string</span></span> | <span data-ttu-id="45025-168">ano</span><span class="sxs-lookup"><span data-stu-id="45025-168">yes</span></span>      | <span data-ttu-id="45025-169">Verze balíčku, normalizovaná a malá</span><span class="sxs-lookup"><span data-stu-id="45025-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="45025-170">`LOWER_ID`A `LOWER_VERSION` jsou malá pomocí pravidel implementovaných pomocí. SÍŤ[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="45025-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true)</span></span>
<span data-ttu-id="45025-171">Metoda.</span><span class="sxs-lookup"><span data-stu-id="45025-171">method.</span></span>

<span data-ttu-id="45025-172">`LOWER_VERSION`Je požadovaná verze balíčku normalizovaná pomocí [pravidel normalizace](../concepts/package-versioning.md#normalized-version-numbers)verzí NuGet.</span><span class="sxs-lookup"><span data-stu-id="45025-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="45025-173">To znamená, že v tomto případě musí být vyloučena metadata sestavení, která jsou povolena specifikací SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="45025-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="45025-174">Text odpovědi</span><span class="sxs-lookup"><span data-stu-id="45025-174">Response body</span></span>

<span data-ttu-id="45025-175">Pokud balíček existuje ve zdroji balíčku, vrátí se stavový kód 200.</span><span class="sxs-lookup"><span data-stu-id="45025-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="45025-176">Tělo odpovědi bude samotný obsah balíčku.</span><span class="sxs-lookup"><span data-stu-id="45025-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="45025-177">Pokud balíček ve zdroji balíčku neexistuje, vrátí se stavový kód 404.</span><span class="sxs-lookup"><span data-stu-id="45025-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="45025-178">Ukázková žádost</span><span class="sxs-lookup"><span data-stu-id="45025-178">Sample request</span></span>

```
GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg
```

### <a name="sample-response"></a><span data-ttu-id="45025-179">Ukázková odpověď</span><span class="sxs-lookup"><span data-stu-id="45025-179">Sample response</span></span>

<span data-ttu-id="45025-180">Binární datový proud, který je souborem. nupkg pro Newtonsoft.Jsv 9.0.1.</span><span class="sxs-lookup"><span data-stu-id="45025-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="45025-181">Stáhnout manifest balíčku (. nuspec)</span><span class="sxs-lookup"><span data-stu-id="45025-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="45025-182">Pokud klient zná ID a verzi balíčku a chce stáhnout manifest balíčku, stačí vytvořit následující adresu URL:</span><span class="sxs-lookup"><span data-stu-id="45025-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

```
GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec
```

### <a name="request-parameters"></a><span data-ttu-id="45025-183">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="45025-183">Request parameters</span></span>

<span data-ttu-id="45025-184">Name</span><span class="sxs-lookup"><span data-stu-id="45025-184">Name</span></span>          | <span data-ttu-id="45025-185">V</span><span class="sxs-lookup"><span data-stu-id="45025-185">In</span></span>     | <span data-ttu-id="45025-186">Typ</span><span class="sxs-lookup"><span data-stu-id="45025-186">Type</span></span>   | <span data-ttu-id="45025-187">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="45025-187">Required</span></span> | <span data-ttu-id="45025-188">Poznámky</span><span class="sxs-lookup"><span data-stu-id="45025-188">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="45025-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="45025-189">LOWER_ID</span></span>      | <span data-ttu-id="45025-190">URL</span><span class="sxs-lookup"><span data-stu-id="45025-190">URL</span></span>    | <span data-ttu-id="45025-191">řetězec</span><span class="sxs-lookup"><span data-stu-id="45025-191">string</span></span> | <span data-ttu-id="45025-192">ano</span><span class="sxs-lookup"><span data-stu-id="45025-192">yes</span></span>      | <span data-ttu-id="45025-193">ID balíčku, malá písmena</span><span class="sxs-lookup"><span data-stu-id="45025-193">The package ID, lowercase</span></span>
<span data-ttu-id="45025-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="45025-194">LOWER_VERSION</span></span> | <span data-ttu-id="45025-195">URL</span><span class="sxs-lookup"><span data-stu-id="45025-195">URL</span></span>    | <span data-ttu-id="45025-196">řetězec</span><span class="sxs-lookup"><span data-stu-id="45025-196">string</span></span> | <span data-ttu-id="45025-197">ano</span><span class="sxs-lookup"><span data-stu-id="45025-197">yes</span></span>      | <span data-ttu-id="45025-198">Verze balíčku, normalizovaná a malá</span><span class="sxs-lookup"><span data-stu-id="45025-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="45025-199">`LOWER_ID`A `LOWER_VERSION` jsou malá pomocí pravidel implementovaných pomocí. Metoda netto [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true) .</span><span class="sxs-lookup"><span data-stu-id="45025-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true) method.</span></span>

<span data-ttu-id="45025-200">`LOWER_VERSION`Je požadovaná verze balíčku normalizovaná pomocí [pravidel normalizace](../concepts/package-versioning.md#normalized-version-numbers)verzí NuGet.</span><span class="sxs-lookup"><span data-stu-id="45025-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="45025-201">To znamená, že v tomto případě musí být vyloučena metadata sestavení, která jsou povolena specifikací SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="45025-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="45025-202">Text odpovědi</span><span class="sxs-lookup"><span data-stu-id="45025-202">Response body</span></span>

<span data-ttu-id="45025-203">Pokud balíček existuje ve zdroji balíčku, vrátí se stavový kód 200.</span><span class="sxs-lookup"><span data-stu-id="45025-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="45025-204">Tělo odpovědi bude manifest balíčku, který je soubor. nuspec obsažený v odpovídajícím nupkg.</span><span class="sxs-lookup"><span data-stu-id="45025-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="45025-205">Soubor. nuspec je dokument XML.</span><span class="sxs-lookup"><span data-stu-id="45025-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="45025-206">Pokud balíček ve zdroji balíčku neexistuje, vrátí se stavový kód 404.</span><span class="sxs-lookup"><span data-stu-id="45025-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="45025-207">Ukázková žádost</span><span class="sxs-lookup"><span data-stu-id="45025-207">Sample request</span></span>

```
GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec
```

### <a name="sample-response"></a><span data-ttu-id="45025-208">Ukázková odpověď</span><span class="sxs-lookup"><span data-stu-id="45025-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
