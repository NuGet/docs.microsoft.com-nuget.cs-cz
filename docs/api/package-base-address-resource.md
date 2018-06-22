---
title: Obsah balíčku NuGet rozhraní API
description: Základní adresa balíčku je jednoduché rozhraní pro načítání balíčku sám sebe.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: a6ac40368f30d33f35d4ca0b6cc18ce4bd6efee5
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819174"
---
# <a name="package-content"></a><span data-ttu-id="892ae-103">Obsah balíčku</span><span class="sxs-lookup"><span data-stu-id="892ae-103">Package Content</span></span>

<span data-ttu-id="892ae-104">Je možné ke generování adresy URL se načíst obsah libovolného balíčku (souboru .nupkg v podadresáři) pomocí rozhraní API V3.</span><span class="sxs-lookup"><span data-stu-id="892ae-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="892ae-105">Je prostředku používaného pro načítání obsahu balíčku `PackageBaseAddress` v nalezen prostředek [indexu služby](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="892ae-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="892ae-106">Tento prostředek také umožňuje zjišťování všech verzí balíčku, uvedené nebo není uveden v seznamu.</span><span class="sxs-lookup"><span data-stu-id="892ae-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="892ae-107">Tento prostředek se obvykle označuje jako buď "balíček základní adresu" nebo "ploché container".</span><span class="sxs-lookup"><span data-stu-id="892ae-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="892ae-108">Správa verzí</span><span class="sxs-lookup"><span data-stu-id="892ae-108">Versioning</span></span>

<span data-ttu-id="892ae-109">Následující `@type` hodnota se používá:</span><span class="sxs-lookup"><span data-stu-id="892ae-109">The following `@type` value is used:</span></span>

<span data-ttu-id="892ae-110">@type Hodnota</span><span class="sxs-lookup"><span data-stu-id="892ae-110">@type value</span></span>              | <span data-ttu-id="892ae-111">Poznámky</span><span class="sxs-lookup"><span data-stu-id="892ae-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="892ae-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="892ae-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="892ae-113">Původní verze</span><span class="sxs-lookup"><span data-stu-id="892ae-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="892ae-114">Základní adresu URL</span><span class="sxs-lookup"><span data-stu-id="892ae-114">Base URL</span></span>

<span data-ttu-id="892ae-115">Základní adresu URL pro následující rozhraní API je hodnota `@id` vlastnost spojená s zmíněnými prostředků `@type` hodnotu.</span><span class="sxs-lookup"><span data-stu-id="892ae-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="892ae-116">V následujícím dokumentu zástupného textu základní adresa URL `{@id}` se použije.</span><span class="sxs-lookup"><span data-stu-id="892ae-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="892ae-117">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="892ae-117">HTTP methods</span></span>

<span data-ttu-id="892ae-118">Všechny adresy URL v podpory registrace prostředků nalezen metody HTTP `GET` a `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="892ae-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="892ae-119">Zobrazení výčtu verze balíčku</span><span class="sxs-lookup"><span data-stu-id="892ae-119">Enumerate package versions</span></span>

<span data-ttu-id="892ae-120">Když klient zná ID balíčku a chce zjistit, které balíčku verze balíčku zdroj má k dispozici, klient můžete vytvořit adresu URL předvídatelný výčet všechny verze balíčku.</span><span class="sxs-lookup"><span data-stu-id="892ae-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="892ae-121">Tento seznam je určené jako "adresářů" pro balíček obsahu API uvedených níže.</span><span class="sxs-lookup"><span data-stu-id="892ae-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="892ae-122">Tento seznam obsahuje obě verze uvedené a neuvedené balíček.</span><span class="sxs-lookup"><span data-stu-id="892ae-122">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="892ae-123">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="892ae-123">Request parameters</span></span>

<span data-ttu-id="892ae-124">Název</span><span class="sxs-lookup"><span data-stu-id="892ae-124">Name</span></span>     | <span data-ttu-id="892ae-125">V</span><span class="sxs-lookup"><span data-stu-id="892ae-125">In</span></span>     | <span data-ttu-id="892ae-126">Typ</span><span class="sxs-lookup"><span data-stu-id="892ae-126">Type</span></span>    | <span data-ttu-id="892ae-127">Požadováno</span><span class="sxs-lookup"><span data-stu-id="892ae-127">Required</span></span> | <span data-ttu-id="892ae-128">Poznámky</span><span class="sxs-lookup"><span data-stu-id="892ae-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="892ae-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="892ae-129">LOWER_ID</span></span> | <span data-ttu-id="892ae-130">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="892ae-130">URL</span></span>    | <span data-ttu-id="892ae-131">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="892ae-131">string</span></span>  | <span data-ttu-id="892ae-132">Ano</span><span class="sxs-lookup"><span data-stu-id="892ae-132">yes</span></span>      | <span data-ttu-id="892ae-133">ID balíčku, malá písmena</span><span class="sxs-lookup"><span data-stu-id="892ae-133">The package ID, lowercase</span></span>

<span data-ttu-id="892ae-134">`LOWER_ID` Hodnota je psané malými písmeny pomocí pravidel implementovaných podle ID požadované balíčku. NET na [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) metoda.</span><span class="sxs-lookup"><span data-stu-id="892ae-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="892ae-135">Odpověď</span><span class="sxs-lookup"><span data-stu-id="892ae-135">Response</span></span>

<span data-ttu-id="892ae-136">Pokud zdroj balíčku má žádné verzích ID zadaný balíček, je vrácen 404 stavový kód.</span><span class="sxs-lookup"><span data-stu-id="892ae-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="892ae-137">Pokud zdroj balíčku má jeden nebo více verzí, je vrácen 200 stavový kód.</span><span class="sxs-lookup"><span data-stu-id="892ae-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="892ae-138">Text odpovědi je objekt JSON s následující vlastnost:</span><span class="sxs-lookup"><span data-stu-id="892ae-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="892ae-139">Název</span><span class="sxs-lookup"><span data-stu-id="892ae-139">Name</span></span>     | <span data-ttu-id="892ae-140">Typ</span><span class="sxs-lookup"><span data-stu-id="892ae-140">Type</span></span>             | <span data-ttu-id="892ae-141">Požadováno</span><span class="sxs-lookup"><span data-stu-id="892ae-141">Required</span></span> | <span data-ttu-id="892ae-142">Poznámky</span><span class="sxs-lookup"><span data-stu-id="892ae-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="892ae-143">verze</span><span class="sxs-lookup"><span data-stu-id="892ae-143">versions</span></span> | <span data-ttu-id="892ae-144">Pole řetězců.</span><span class="sxs-lookup"><span data-stu-id="892ae-144">array of strings</span></span> | <span data-ttu-id="892ae-145">Ano</span><span class="sxs-lookup"><span data-stu-id="892ae-145">yes</span></span>      | <span data-ttu-id="892ae-146">Balíček ID, které jsou k dispozici</span><span class="sxs-lookup"><span data-stu-id="892ae-146">The package IDs available</span></span>

<span data-ttu-id="892ae-147">Řetězce v `versions` pole jsou všechny psané malými písmeny, [normalized řetězce verze NuGet](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="892ae-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="892ae-148">Řetězce verze neobsahují žádné SemVer 2.0.0 metadata sestavení.</span><span class="sxs-lookup"><span data-stu-id="892ae-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="892ae-149">Účelem je, že řetězce verze součástí toto pole lze použít doslovné pro `LOWER_VERSION` tokeny najít v následujících koncových bodů.</span><span class="sxs-lookup"><span data-stu-id="892ae-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="892ae-150">Ukázková žádost</span><span class="sxs-lookup"><span data-stu-id="892ae-150">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="892ae-151">Ukázková odpověď</span><span class="sxs-lookup"><span data-stu-id="892ae-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="892ae-152">Stažení obsahu balíčku (.nupkg)</span><span class="sxs-lookup"><span data-stu-id="892ae-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="892ae-153">Pokud klient zná ID balíčku a verze a chce stáhnout obsah balíčku, potřebují jenom vytvořit následující adresu URL:</span><span class="sxs-lookup"><span data-stu-id="892ae-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="892ae-154">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="892ae-154">Request parameters</span></span>

<span data-ttu-id="892ae-155">Název</span><span class="sxs-lookup"><span data-stu-id="892ae-155">Name</span></span>          | <span data-ttu-id="892ae-156">V</span><span class="sxs-lookup"><span data-stu-id="892ae-156">In</span></span>     | <span data-ttu-id="892ae-157">Typ</span><span class="sxs-lookup"><span data-stu-id="892ae-157">Type</span></span>   | <span data-ttu-id="892ae-158">Požadováno</span><span class="sxs-lookup"><span data-stu-id="892ae-158">Required</span></span> | <span data-ttu-id="892ae-159">Poznámky</span><span class="sxs-lookup"><span data-stu-id="892ae-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="892ae-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="892ae-160">LOWER_ID</span></span>      | <span data-ttu-id="892ae-161">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="892ae-161">URL</span></span>    | <span data-ttu-id="892ae-162">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="892ae-162">string</span></span> | <span data-ttu-id="892ae-163">Ano</span><span class="sxs-lookup"><span data-stu-id="892ae-163">yes</span></span>      | <span data-ttu-id="892ae-164">ID balíčku, malá písmena</span><span class="sxs-lookup"><span data-stu-id="892ae-164">The package ID, lowercase</span></span>
<span data-ttu-id="892ae-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="892ae-165">LOWER_VERSION</span></span> | <span data-ttu-id="892ae-166">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="892ae-166">URL</span></span>    | <span data-ttu-id="892ae-167">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="892ae-167">string</span></span> | <span data-ttu-id="892ae-168">Ano</span><span class="sxs-lookup"><span data-stu-id="892ae-168">yes</span></span>      | <span data-ttu-id="892ae-169">Verze balíčku normalized a psané malými písmeny</span><span class="sxs-lookup"><span data-stu-id="892ae-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="892ae-170">Obě `LOWER_ID` a `LOWER_VERSION` jsou psané malými písmeny pomocí pravidel implementované. NET na [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) metoda.</span><span class="sxs-lookup"><span data-stu-id="892ae-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="892ae-171">`LOWER_VERSION` Je verze balíčku požadované normalized pomocí verze NuGet [normalizaci pravidla](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="892ae-171">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="892ae-172">To znamená, že aby metadata sestavení, kterou specifikace SemVer 2.0.0 se musí v tomto případě vyloučit.</span><span class="sxs-lookup"><span data-stu-id="892ae-172">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="892ae-173">Text odpovědi</span><span class="sxs-lookup"><span data-stu-id="892ae-173">Response body</span></span>

<span data-ttu-id="892ae-174">Pokud balíček existuje ve zdroji balíčku, je vrácena 200 stavový kód.</span><span class="sxs-lookup"><span data-stu-id="892ae-174">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="892ae-175">Text odpovědi bude obsah balíčku sám sebe.</span><span class="sxs-lookup"><span data-stu-id="892ae-175">The response body will be the package content itself.</span></span>

<span data-ttu-id="892ae-176">Pokud balíček neexistuje ve zdroji balíčku, je vrácena 404 stavový kód.</span><span class="sxs-lookup"><span data-stu-id="892ae-176">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="892ae-177">Ukázková žádost</span><span class="sxs-lookup"><span data-stu-id="892ae-177">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="892ae-178">Ukázková odpověď</span><span class="sxs-lookup"><span data-stu-id="892ae-178">Sample response</span></span>

<span data-ttu-id="892ae-179">Binární datový proud, který je .nupkg pro Newtonsoft.Json 9.0.1.</span><span class="sxs-lookup"><span data-stu-id="892ae-179">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="892ae-180">Stáhněte manifest balíčku (s příponou .nuspec)</span><span class="sxs-lookup"><span data-stu-id="892ae-180">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="892ae-181">Pokud klient zná ID balíčku a verze a chce stáhnout manifest balíčku, potřebují jenom vytvořit následující adresu URL:</span><span class="sxs-lookup"><span data-stu-id="892ae-181">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="892ae-182">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="892ae-182">Request parameters</span></span>

<span data-ttu-id="892ae-183">Název</span><span class="sxs-lookup"><span data-stu-id="892ae-183">Name</span></span>          | <span data-ttu-id="892ae-184">V</span><span class="sxs-lookup"><span data-stu-id="892ae-184">In</span></span>     | <span data-ttu-id="892ae-185">Typ</span><span class="sxs-lookup"><span data-stu-id="892ae-185">Type</span></span>    | <span data-ttu-id="892ae-186">Požadováno</span><span class="sxs-lookup"><span data-stu-id="892ae-186">Required</span></span> | <span data-ttu-id="892ae-187">Poznámky</span><span class="sxs-lookup"><span data-stu-id="892ae-187">Notes</span></span>
------------- | ------ | ------- | -------- | -----
<span data-ttu-id="892ae-188">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="892ae-188">LOWER_ID</span></span>      | <span data-ttu-id="892ae-189">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="892ae-189">URL</span></span>    | <span data-ttu-id="892ae-190">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="892ae-190">string</span></span>  | <span data-ttu-id="892ae-191">Ano</span><span class="sxs-lookup"><span data-stu-id="892ae-191">yes</span></span>      | <span data-ttu-id="892ae-192">ID balíčku, malá písmena</span><span class="sxs-lookup"><span data-stu-id="892ae-192">The package ID, lowercase</span></span>
<span data-ttu-id="892ae-193">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="892ae-193">LOWER_VERSION</span></span> | <span data-ttu-id="892ae-194">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="892ae-194">URL</span></span>    | <span data-ttu-id="892ae-195">integer</span><span class="sxs-lookup"><span data-stu-id="892ae-195">integer</span></span> | <span data-ttu-id="892ae-196">Ano</span><span class="sxs-lookup"><span data-stu-id="892ae-196">yes</span></span>      | <span data-ttu-id="892ae-197">Verze balíčku normalized a psané malými písmeny</span><span class="sxs-lookup"><span data-stu-id="892ae-197">The package version, normalized and lowercased</span></span>

<span data-ttu-id="892ae-198">Obě `LOWER_ID` a `LOWER_VERSION` jsou psané malými písmeny pomocí pravidel implementované. NET na [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) metoda.</span><span class="sxs-lookup"><span data-stu-id="892ae-198">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="892ae-199">`LOWER_VERSION` Je verze balíčku požadované normalized pomocí verze NuGet [normalizaci pravidla](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="892ae-199">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="892ae-200">To znamená, že aby metadata sestavení, kterou specifikace SemVer 2.0.0 se musí v tomto případě vyloučit.</span><span class="sxs-lookup"><span data-stu-id="892ae-200">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="892ae-201">Text odpovědi</span><span class="sxs-lookup"><span data-stu-id="892ae-201">Response body</span></span>

<span data-ttu-id="892ae-202">Pokud balíček existuje ve zdroji balíčku, je vrácena 200 stavový kód.</span><span class="sxs-lookup"><span data-stu-id="892ae-202">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="892ae-203">Text odpovědi bude manifest balíčku, který je příponou .nuspec obsažené v odpovídající .nupkg.</span><span class="sxs-lookup"><span data-stu-id="892ae-203">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="892ae-204">Příponou .nuspec je dokument XML.</span><span class="sxs-lookup"><span data-stu-id="892ae-204">The .nuspec is an XML document.</span></span>

<span data-ttu-id="892ae-205">Pokud balíček neexistuje ve zdroji balíčku, je vrácena 404 stavový kód.</span><span class="sxs-lookup"><span data-stu-id="892ae-205">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="892ae-206">Ukázková žádost</span><span class="sxs-lookup"><span data-stu-id="892ae-206">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="892ae-207">Ukázková odpověď</span><span class="sxs-lookup"><span data-stu-id="892ae-207">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
