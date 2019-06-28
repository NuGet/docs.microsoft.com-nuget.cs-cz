---
title: Obsah balíčku NuGet rozhraní API
description: Základní adresa balíček je jednoduché rozhraní pro načítání samotném balíčku.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 2f0f93e0cee78ea03cbd53194cdc2a10871fd7e1
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426755"
---
# <a name="package-content"></a><span data-ttu-id="43687-103">Balíček obsahu</span><span class="sxs-lookup"><span data-stu-id="43687-103">Package Content</span></span>

<span data-ttu-id="43687-104">Je možné ke generování adresy URL načíst obsah libovolného balíčku (souboru .nupkg) pomocí rozhraní API V3.</span><span class="sxs-lookup"><span data-stu-id="43687-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="43687-105">Prostředek, který používá pro načtení balíčku obsahu je `PackageBaseAddress` prostředek se nenašel v [index služby](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="43687-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="43687-106">Tento prostředek také umožňuje zjišťování všech verzí balíčku uvedené nebo neuvedené v seznamu.</span><span class="sxs-lookup"><span data-stu-id="43687-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="43687-107">Tento prostředek se obvykle označuje jako buď "balíček základní adresa" nebo "ploché kontejneru".</span><span class="sxs-lookup"><span data-stu-id="43687-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="43687-108">Správa verzí</span><span class="sxs-lookup"><span data-stu-id="43687-108">Versioning</span></span>

<span data-ttu-id="43687-109">Následující `@type` hodnota se používá:</span><span class="sxs-lookup"><span data-stu-id="43687-109">The following `@type` value is used:</span></span>

<span data-ttu-id="43687-110">@type Hodnota</span><span class="sxs-lookup"><span data-stu-id="43687-110">@type value</span></span>              | <span data-ttu-id="43687-111">Poznámky</span><span class="sxs-lookup"><span data-stu-id="43687-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="43687-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="43687-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="43687-113">Počáteční verze</span><span class="sxs-lookup"><span data-stu-id="43687-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="43687-114">Základní adresa URL</span><span class="sxs-lookup"><span data-stu-id="43687-114">Base URL</span></span>

<span data-ttu-id="43687-115">Základní adresa URL pro následující rozhraní API je hodnota `@id` vlastnost přidružená k výše uvedených prostředků `@type` hodnotu.</span><span class="sxs-lookup"><span data-stu-id="43687-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="43687-116">V následujícím dokumentu, zástupný symbol základní adresa URL `{@id}` se použije.</span><span class="sxs-lookup"><span data-stu-id="43687-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="43687-117">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="43687-117">HTTP methods</span></span>

<span data-ttu-id="43687-118">Všechny adresy URL, které jsou součástí zdroje podpory registrace metody HTTP `GET` a `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="43687-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="43687-119">Výčet verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="43687-119">Enumerate package versions</span></span>

<span data-ttu-id="43687-120">Pokud klient zná ID balíčku a chcete zjistit, které balíček verze balíčku zdroj nemá k dispozici, klient může vytvořit předvídatelné adresu URL se vytvořit výčet všech verzí balíčků.</span><span class="sxs-lookup"><span data-stu-id="43687-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="43687-121">Tento seznam je určena být "výpis adresáře" pro balíček obsahu API, které jsou uvedené níže.</span><span class="sxs-lookup"><span data-stu-id="43687-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="43687-122">Tento seznam obsahuje obě verze uvedené a neuvedené v seznamu balíčků.</span><span class="sxs-lookup"><span data-stu-id="43687-122">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="43687-123">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="43687-123">Request parameters</span></span>

<span data-ttu-id="43687-124">Name</span><span class="sxs-lookup"><span data-stu-id="43687-124">Name</span></span>     | <span data-ttu-id="43687-125">V</span><span class="sxs-lookup"><span data-stu-id="43687-125">In</span></span>     | <span data-ttu-id="43687-126">type</span><span class="sxs-lookup"><span data-stu-id="43687-126">Type</span></span>    | <span data-ttu-id="43687-127">Požadováno</span><span class="sxs-lookup"><span data-stu-id="43687-127">Required</span></span> | <span data-ttu-id="43687-128">Poznámky</span><span class="sxs-lookup"><span data-stu-id="43687-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="43687-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="43687-129">LOWER_ID</span></span> | <span data-ttu-id="43687-130">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="43687-130">URL</span></span>    | <span data-ttu-id="43687-131">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="43687-131">string</span></span>  | <span data-ttu-id="43687-132">ano</span><span class="sxs-lookup"><span data-stu-id="43687-132">yes</span></span>      | <span data-ttu-id="43687-133">ID balíčku, malá písmena</span><span class="sxs-lookup"><span data-stu-id="43687-133">The package ID, lowercase</span></span>

<span data-ttu-id="43687-134">`LOWER_ID` Hodnotu ID požadovaný balíček psané malými písmeny pomocí pravidel implementované. NET společnosti [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) metody.</span><span class="sxs-lookup"><span data-stu-id="43687-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="43687-135">Odpověď</span><span class="sxs-lookup"><span data-stu-id="43687-135">Response</span></span>

<span data-ttu-id="43687-136">Pokud zdroj balíčku má žádné verze ID zadaného balíčku, je vrácen stavový kód 404.</span><span class="sxs-lookup"><span data-stu-id="43687-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="43687-137">Pokud zdroj balíčku má jednu nebo více verzí, vrátí se kód stavový kód 200.</span><span class="sxs-lookup"><span data-stu-id="43687-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="43687-138">Text odpovědi je objekt JSON s následující vlastnost:</span><span class="sxs-lookup"><span data-stu-id="43687-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="43687-139">Name</span><span class="sxs-lookup"><span data-stu-id="43687-139">Name</span></span>     | <span data-ttu-id="43687-140">type</span><span class="sxs-lookup"><span data-stu-id="43687-140">Type</span></span>             | <span data-ttu-id="43687-141">Požadováno</span><span class="sxs-lookup"><span data-stu-id="43687-141">Required</span></span> | <span data-ttu-id="43687-142">Poznámky</span><span class="sxs-lookup"><span data-stu-id="43687-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="43687-143">verze</span><span class="sxs-lookup"><span data-stu-id="43687-143">versions</span></span> | <span data-ttu-id="43687-144">pole řetězců</span><span class="sxs-lookup"><span data-stu-id="43687-144">array of strings</span></span> | <span data-ttu-id="43687-145">ano</span><span class="sxs-lookup"><span data-stu-id="43687-145">yes</span></span>      | <span data-ttu-id="43687-146">Balíček ID, které jsou k dispozici</span><span class="sxs-lookup"><span data-stu-id="43687-146">The package IDs available</span></span>

<span data-ttu-id="43687-147">Řetězce ve `versions` pole jsou všechny psané malými písmeny, [normalizovat řetězce verze NuGet](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="43687-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="43687-148">Řetězce verze neobsahuje žádné SemVer 2.0.0 metadat sestavení.</span><span class="sxs-lookup"><span data-stu-id="43687-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="43687-149">Cílem je, že verze řetězce nalezen v tomto poli je možné verbatim pro `LOWER_VERSION` tokenů najdete v následujících koncových bodů.</span><span class="sxs-lookup"><span data-stu-id="43687-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="43687-150">Ukázková žádost</span><span class="sxs-lookup"><span data-stu-id="43687-150">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="43687-151">Ukázková odpověď</span><span class="sxs-lookup"><span data-stu-id="43687-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="43687-152">Stáhnout obsah balíčku (.nupkg)</span><span class="sxs-lookup"><span data-stu-id="43687-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="43687-153">Pokud klient zná ID balíčku a verzi a chce stáhnout obsah balíčku, potřebují jenom vytvořit následující adresu URL:</span><span class="sxs-lookup"><span data-stu-id="43687-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="43687-154">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="43687-154">Request parameters</span></span>

<span data-ttu-id="43687-155">Name</span><span class="sxs-lookup"><span data-stu-id="43687-155">Name</span></span>          | <span data-ttu-id="43687-156">V</span><span class="sxs-lookup"><span data-stu-id="43687-156">In</span></span>     | <span data-ttu-id="43687-157">type</span><span class="sxs-lookup"><span data-stu-id="43687-157">Type</span></span>   | <span data-ttu-id="43687-158">Požadováno</span><span class="sxs-lookup"><span data-stu-id="43687-158">Required</span></span> | <span data-ttu-id="43687-159">Poznámky</span><span class="sxs-lookup"><span data-stu-id="43687-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="43687-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="43687-160">LOWER_ID</span></span>      | <span data-ttu-id="43687-161">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="43687-161">URL</span></span>    | <span data-ttu-id="43687-162">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="43687-162">string</span></span> | <span data-ttu-id="43687-163">ano</span><span class="sxs-lookup"><span data-stu-id="43687-163">yes</span></span>      | <span data-ttu-id="43687-164">ID balíčku, malá písmena</span><span class="sxs-lookup"><span data-stu-id="43687-164">The package ID, lowercase</span></span>
<span data-ttu-id="43687-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="43687-165">LOWER_VERSION</span></span> | <span data-ttu-id="43687-166">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="43687-166">URL</span></span>    | <span data-ttu-id="43687-167">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="43687-167">string</span></span> | <span data-ttu-id="43687-168">ano</span><span class="sxs-lookup"><span data-stu-id="43687-168">yes</span></span>      | <span data-ttu-id="43687-169">Verze balíčku, normalizovaná a psané malými písmeny</span><span class="sxs-lookup"><span data-stu-id="43687-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="43687-170">Obě `LOWER_ID` a `LOWER_VERSION` jsou psané malými písmeny pomocí pravidel implementované. NET. [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span><span class="sxs-lookup"><span data-stu-id="43687-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span></span>
<span data-ttu-id="43687-171">Metoda.</span><span class="sxs-lookup"><span data-stu-id="43687-171">method.</span></span>

<span data-ttu-id="43687-172">`LOWER_VERSION` Se verze balíčku požadovaného normalizuje pomocí verze Nugetu [normalizace pravidla](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="43687-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="43687-173">To znamená, že v tomto případě je třeba vyloučit tato sestavení metadata, která je povolena ve specifikaci SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="43687-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="43687-174">Text odpovědi</span><span class="sxs-lookup"><span data-stu-id="43687-174">Response body</span></span>

<span data-ttu-id="43687-175">Pokud balíček existuje ve zdroji balíčku, vrátí se kód stavový kód 200.</span><span class="sxs-lookup"><span data-stu-id="43687-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="43687-176">Text odpovědi bude samotného obsahu balíčku.</span><span class="sxs-lookup"><span data-stu-id="43687-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="43687-177">Pokud balíček na zdroj balíčku neexistuje, vrátí se stavový kód 404.</span><span class="sxs-lookup"><span data-stu-id="43687-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="43687-178">Ukázková žádost</span><span class="sxs-lookup"><span data-stu-id="43687-178">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="43687-179">Ukázková odpověď</span><span class="sxs-lookup"><span data-stu-id="43687-179">Sample response</span></span>

<span data-ttu-id="43687-180">Binární datový proud, který je .nupkg pro Newtonsoft.Json 9.0.1.</span><span class="sxs-lookup"><span data-stu-id="43687-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="43687-181">Stáhnout manifest balíčku (souboru .nuspec)</span><span class="sxs-lookup"><span data-stu-id="43687-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="43687-182">Pokud klient zná ID balíčku a verzi a chce, aby se stáhnout manifest balíčku, potřebují jenom vytvořit následující adresu URL:</span><span class="sxs-lookup"><span data-stu-id="43687-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="43687-183">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="43687-183">Request parameters</span></span>

<span data-ttu-id="43687-184">Name</span><span class="sxs-lookup"><span data-stu-id="43687-184">Name</span></span>          | <span data-ttu-id="43687-185">V</span><span class="sxs-lookup"><span data-stu-id="43687-185">In</span></span>     | <span data-ttu-id="43687-186">type</span><span class="sxs-lookup"><span data-stu-id="43687-186">Type</span></span>   | <span data-ttu-id="43687-187">Požadováno</span><span class="sxs-lookup"><span data-stu-id="43687-187">Required</span></span> | <span data-ttu-id="43687-188">Poznámky</span><span class="sxs-lookup"><span data-stu-id="43687-188">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="43687-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="43687-189">LOWER_ID</span></span>      | <span data-ttu-id="43687-190">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="43687-190">URL</span></span>    | <span data-ttu-id="43687-191">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="43687-191">string</span></span> | <span data-ttu-id="43687-192">ano</span><span class="sxs-lookup"><span data-stu-id="43687-192">yes</span></span>      | <span data-ttu-id="43687-193">ID balíčku, malá písmena</span><span class="sxs-lookup"><span data-stu-id="43687-193">The package ID, lowercase</span></span>
<span data-ttu-id="43687-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="43687-194">LOWER_VERSION</span></span> | <span data-ttu-id="43687-195">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="43687-195">URL</span></span>    | <span data-ttu-id="43687-196">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="43687-196">string</span></span> | <span data-ttu-id="43687-197">ano</span><span class="sxs-lookup"><span data-stu-id="43687-197">yes</span></span>      | <span data-ttu-id="43687-198">Verze balíčku, normalizovaná a psané malými písmeny</span><span class="sxs-lookup"><span data-stu-id="43687-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="43687-199">Obě `LOWER_ID` a `LOWER_VERSION` jsou psané malými písmeny pomocí pravidel implementované. NET společnosti [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) metody.</span><span class="sxs-lookup"><span data-stu-id="43687-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="43687-200">`LOWER_VERSION` Se verze balíčku požadovaného normalizuje pomocí verze Nugetu [normalizace pravidla](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="43687-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="43687-201">To znamená, že v tomto případě je třeba vyloučit tato sestavení metadata, která je povolena ve specifikaci SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="43687-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="43687-202">Text odpovědi</span><span class="sxs-lookup"><span data-stu-id="43687-202">Response body</span></span>

<span data-ttu-id="43687-203">Pokud balíček existuje ve zdroji balíčku, vrátí se kód stavový kód 200.</span><span class="sxs-lookup"><span data-stu-id="43687-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="43687-204">Text odpovědi bude manifest balíčku, který je souboru .nuspec obsažené v odpovídající .nupkg.</span><span class="sxs-lookup"><span data-stu-id="43687-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="43687-205">Souboru .nuspec je dokument XML.</span><span class="sxs-lookup"><span data-stu-id="43687-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="43687-206">Pokud balíček na zdroj balíčku neexistuje, vrátí se stavový kód 404.</span><span class="sxs-lookup"><span data-stu-id="43687-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="43687-207">Ukázková žádost</span><span class="sxs-lookup"><span data-stu-id="43687-207">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="43687-208">Ukázková odpověď</span><span class="sxs-lookup"><span data-stu-id="43687-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
