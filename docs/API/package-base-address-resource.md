---
title: "Balíček obsahu, NuGet rozhraní API | Microsoft Docs"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Základní adresa balíčku je jednoduché rozhraní pro načítání balíčku sám sebe."
keywords: "NuGet s plochou kontejneru, základní adresa balíčku NuGet, NuGet nupkg rozhraní API, verze balíčku NuGet rozhraní API, rozhraní API NuGet neuvedené balíčky, rozhraní API NuGet stahování nuspec"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: c2e631dc0bba95ac849430d77142f27ef591f741
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
---
# <a name="package-content"></a><span data-ttu-id="7542c-104">Obsah balíčku</span><span class="sxs-lookup"><span data-stu-id="7542c-104">Package Content</span></span>

<span data-ttu-id="7542c-105">Je možné ke generování adresy URL se načíst obsah libovolného balíčku (souboru .nupkg v podadresáři) pomocí rozhraní API V3.</span><span class="sxs-lookup"><span data-stu-id="7542c-105">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="7542c-106">Je prostředku používaného pro načítání obsahu balíčku `PackageBaseAddress` v nalezen prostředek [indexu služby](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="7542c-106">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="7542c-107">Tento prostředek také umožňuje zjišťování všech verzí balíčku, uvedené nebo není uveden v seznamu.</span><span class="sxs-lookup"><span data-stu-id="7542c-107">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="7542c-108">Tento prostředek se obvykle označuje jako buď "balíček základní adresu" nebo "ploché container".</span><span class="sxs-lookup"><span data-stu-id="7542c-108">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="7542c-109">Správa verzí</span><span class="sxs-lookup"><span data-stu-id="7542c-109">Versioning</span></span>

<span data-ttu-id="7542c-110">Následující `@type` hodnota se používá:</span><span class="sxs-lookup"><span data-stu-id="7542c-110">The following `@type` value is used:</span></span>

<span data-ttu-id="7542c-111">@typeHodnota</span><span class="sxs-lookup"><span data-stu-id="7542c-111">@type value</span></span>              | <span data-ttu-id="7542c-112">Poznámky</span><span class="sxs-lookup"><span data-stu-id="7542c-112">Notes</span></span>
------------------------ | -----
<span data-ttu-id="7542c-113">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="7542c-113">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="7542c-114">Původní verze</span><span class="sxs-lookup"><span data-stu-id="7542c-114">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="7542c-115">Základní adresu URL</span><span class="sxs-lookup"><span data-stu-id="7542c-115">Base URL</span></span>

<span data-ttu-id="7542c-116">Základní adresu URL pro následující rozhraní API je hodnota `@id` vlastnost spojená s zmíněnými prostředků `@type` hodnotu.</span><span class="sxs-lookup"><span data-stu-id="7542c-116">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="7542c-117">V následujícím dokumentu zástupného textu základní adresa URL `{@id}` se použije.</span><span class="sxs-lookup"><span data-stu-id="7542c-117">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="7542c-118">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="7542c-118">HTTP methods</span></span>

<span data-ttu-id="7542c-119">Všechny adresy URL v podpory registrace prostředků nalezen metody HTTP `GET` a `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="7542c-119">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="7542c-120">Zobrazení výčtu verze balíčku</span><span class="sxs-lookup"><span data-stu-id="7542c-120">Enumerate package versions</span></span>

<span data-ttu-id="7542c-121">Když klient zná ID balíčku a chce zjistit, které balíčku verze balíčku zdroj má k dispozici, klient můžete vytvořit adresu URL předvídatelný výčet všechny verze balíčku.</span><span class="sxs-lookup"><span data-stu-id="7542c-121">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="7542c-122">Tento seznam je určené jako "adresářů" pro balíček obsahu API uvedených níže.</span><span class="sxs-lookup"><span data-stu-id="7542c-122">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="7542c-123">Tento seznam obsahuje obě verze uvedené a neuvedené balíček.</span><span class="sxs-lookup"><span data-stu-id="7542c-123">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="7542c-124">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="7542c-124">Request parameters</span></span>

<span data-ttu-id="7542c-125">Název</span><span class="sxs-lookup"><span data-stu-id="7542c-125">Name</span></span>     | <span data-ttu-id="7542c-126">V</span><span class="sxs-lookup"><span data-stu-id="7542c-126">In</span></span>     | <span data-ttu-id="7542c-127">Typ</span><span class="sxs-lookup"><span data-stu-id="7542c-127">Type</span></span>    | <span data-ttu-id="7542c-128">Požadováno</span><span class="sxs-lookup"><span data-stu-id="7542c-128">Required</span></span> | <span data-ttu-id="7542c-129">Poznámky</span><span class="sxs-lookup"><span data-stu-id="7542c-129">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="7542c-130">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="7542c-130">LOWER_ID</span></span> | <span data-ttu-id="7542c-131">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="7542c-131">URL</span></span>    | <span data-ttu-id="7542c-132">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="7542c-132">string</span></span>  | <span data-ttu-id="7542c-133">Ano</span><span class="sxs-lookup"><span data-stu-id="7542c-133">yes</span></span>      | <span data-ttu-id="7542c-134">ID balíčku, malá písmena</span><span class="sxs-lookup"><span data-stu-id="7542c-134">The package ID, lowercase</span></span>

<span data-ttu-id="7542c-135">`LOWER_ID` Hodnota je psané malými písmeny pomocí pravidel implementovaných podle ID požadované balíčku. NET na [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) metoda.</span><span class="sxs-lookup"><span data-stu-id="7542c-135">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="7542c-136">Odpověď</span><span class="sxs-lookup"><span data-stu-id="7542c-136">Response</span></span>

<span data-ttu-id="7542c-137">Pokud zdroj balíčku má žádné verzích ID zadaný balíček, je vrácen 404 stavový kód.</span><span class="sxs-lookup"><span data-stu-id="7542c-137">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="7542c-138">Pokud zdroj balíčku má jeden nebo více verzí, je vrácen 200 stavový kód.</span><span class="sxs-lookup"><span data-stu-id="7542c-138">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="7542c-139">Text odpovědi je objekt JSON s následující vlastnost:</span><span class="sxs-lookup"><span data-stu-id="7542c-139">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="7542c-140">Název</span><span class="sxs-lookup"><span data-stu-id="7542c-140">Name</span></span>     | <span data-ttu-id="7542c-141">Typ</span><span class="sxs-lookup"><span data-stu-id="7542c-141">Type</span></span>             | <span data-ttu-id="7542c-142">Požadováno</span><span class="sxs-lookup"><span data-stu-id="7542c-142">Required</span></span> | <span data-ttu-id="7542c-143">Poznámky</span><span class="sxs-lookup"><span data-stu-id="7542c-143">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="7542c-144">verze</span><span class="sxs-lookup"><span data-stu-id="7542c-144">versions</span></span> | <span data-ttu-id="7542c-145">Pole řetězců.</span><span class="sxs-lookup"><span data-stu-id="7542c-145">array of strings</span></span> | <span data-ttu-id="7542c-146">Ano</span><span class="sxs-lookup"><span data-stu-id="7542c-146">yes</span></span>      | <span data-ttu-id="7542c-147">Balíček ID, které jsou k dispozici</span><span class="sxs-lookup"><span data-stu-id="7542c-147">The package IDs available</span></span>

<span data-ttu-id="7542c-148">Řetězce v `versions` pole jsou všechny psané malými písmeny, [normalized řetězce verze NuGet](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="7542c-148">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="7542c-149">Řetězce verze neobsahují žádné SemVer 2.0.0 metadata sestavení.</span><span class="sxs-lookup"><span data-stu-id="7542c-149">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="7542c-150">Účelem je, že řetězce verze součástí toto pole lze použít doslovné pro `LOWER_VERSION` tokeny najít v následujících koncových bodů.</span><span class="sxs-lookup"><span data-stu-id="7542c-150">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="7542c-151">Ukázková žádost</span><span class="sxs-lookup"><span data-stu-id="7542c-151">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="7542c-152">Ukázková odpověď</span><span class="sxs-lookup"><span data-stu-id="7542c-152">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="7542c-153">Stažení obsahu balíčku (.nupkg)</span><span class="sxs-lookup"><span data-stu-id="7542c-153">Download package content (.nupkg)</span></span>

<span data-ttu-id="7542c-154">Pokud klient zná ID balíčku a verze a chce stáhnout obsah balíčku, potřebují jenom vytvořit následující adresu URL:</span><span class="sxs-lookup"><span data-stu-id="7542c-154">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="7542c-155">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="7542c-155">Request parameters</span></span>

<span data-ttu-id="7542c-156">Název</span><span class="sxs-lookup"><span data-stu-id="7542c-156">Name</span></span>          | <span data-ttu-id="7542c-157">V</span><span class="sxs-lookup"><span data-stu-id="7542c-157">In</span></span>     | <span data-ttu-id="7542c-158">Typ</span><span class="sxs-lookup"><span data-stu-id="7542c-158">Type</span></span>   | <span data-ttu-id="7542c-159">Požadováno</span><span class="sxs-lookup"><span data-stu-id="7542c-159">Required</span></span> | <span data-ttu-id="7542c-160">Poznámky</span><span class="sxs-lookup"><span data-stu-id="7542c-160">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="7542c-161">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="7542c-161">LOWER_ID</span></span>      | <span data-ttu-id="7542c-162">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="7542c-162">URL</span></span>    | <span data-ttu-id="7542c-163">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="7542c-163">string</span></span> | <span data-ttu-id="7542c-164">Ano</span><span class="sxs-lookup"><span data-stu-id="7542c-164">yes</span></span>      | <span data-ttu-id="7542c-165">ID balíčku, malá písmena</span><span class="sxs-lookup"><span data-stu-id="7542c-165">The package ID, lowercase</span></span>
<span data-ttu-id="7542c-166">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="7542c-166">LOWER_VERSION</span></span> | <span data-ttu-id="7542c-167">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="7542c-167">URL</span></span>    | <span data-ttu-id="7542c-168">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="7542c-168">string</span></span> | <span data-ttu-id="7542c-169">Ano</span><span class="sxs-lookup"><span data-stu-id="7542c-169">yes</span></span>      | <span data-ttu-id="7542c-170">Verze balíčku normalized a psané malými písmeny</span><span class="sxs-lookup"><span data-stu-id="7542c-170">The package version, normalized and lowercased</span></span>

<span data-ttu-id="7542c-171">Obě `LOWER_ID` a `LOWER_VERSION` jsou psané malými písmeny pomocí pravidel implementované. NET na [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) metoda.</span><span class="sxs-lookup"><span data-stu-id="7542c-171">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="7542c-172">`LOWER_VERSION` Je verze balíčku požadované normalized pomocí verze NuGet [normalizaci pravidla](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="7542c-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="7542c-173">To znamená, že aby metadata sestavení, kterou specifikace SemVer 2.0.0 se musí v tomto případě vyloučit.</span><span class="sxs-lookup"><span data-stu-id="7542c-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="7542c-174">Text odpovědi</span><span class="sxs-lookup"><span data-stu-id="7542c-174">Response body</span></span>

<span data-ttu-id="7542c-175">Pokud balíček existuje ve zdroji balíčku, je vrácena 200 stavový kód.</span><span class="sxs-lookup"><span data-stu-id="7542c-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="7542c-176">Text odpovědi bude obsah balíčku sám sebe.</span><span class="sxs-lookup"><span data-stu-id="7542c-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="7542c-177">Pokud balíček neexistuje ve zdroji balíčku, je vrácena 404 stavový kód.</span><span class="sxs-lookup"><span data-stu-id="7542c-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="7542c-178">Ukázková žádost</span><span class="sxs-lookup"><span data-stu-id="7542c-178">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="7542c-179">Ukázková odpověď</span><span class="sxs-lookup"><span data-stu-id="7542c-179">Sample response</span></span>

<span data-ttu-id="7542c-180">Binární datový proud, který je .nupkg pro Newtonsoft.Json 9.0.1.</span><span class="sxs-lookup"><span data-stu-id="7542c-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="7542c-181">Stáhněte manifest balíčku (s příponou .nuspec)</span><span class="sxs-lookup"><span data-stu-id="7542c-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="7542c-182">Pokud klient zná ID balíčku a verze a chce stáhnout manifest balíčku, potřebují jenom vytvořit následující adresu URL:</span><span class="sxs-lookup"><span data-stu-id="7542c-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="7542c-183">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="7542c-183">Request parameters</span></span>

<span data-ttu-id="7542c-184">Název</span><span class="sxs-lookup"><span data-stu-id="7542c-184">Name</span></span>          | <span data-ttu-id="7542c-185">V</span><span class="sxs-lookup"><span data-stu-id="7542c-185">In</span></span>     | <span data-ttu-id="7542c-186">Typ</span><span class="sxs-lookup"><span data-stu-id="7542c-186">Type</span></span>    | <span data-ttu-id="7542c-187">Požadováno</span><span class="sxs-lookup"><span data-stu-id="7542c-187">Required</span></span> | <span data-ttu-id="7542c-188">Poznámky</span><span class="sxs-lookup"><span data-stu-id="7542c-188">Notes</span></span>
------------- | ------ | ------- | -------- | -----
<span data-ttu-id="7542c-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="7542c-189">LOWER_ID</span></span>      | <span data-ttu-id="7542c-190">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="7542c-190">URL</span></span>    | <span data-ttu-id="7542c-191">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="7542c-191">string</span></span>  | <span data-ttu-id="7542c-192">Ano</span><span class="sxs-lookup"><span data-stu-id="7542c-192">yes</span></span>      | <span data-ttu-id="7542c-193">ID balíčku, malá písmena</span><span class="sxs-lookup"><span data-stu-id="7542c-193">The package ID, lowercase</span></span>
<span data-ttu-id="7542c-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="7542c-194">LOWER_VERSION</span></span> | <span data-ttu-id="7542c-195">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="7542c-195">URL</span></span>    | <span data-ttu-id="7542c-196">integer</span><span class="sxs-lookup"><span data-stu-id="7542c-196">integer</span></span> | <span data-ttu-id="7542c-197">Ano</span><span class="sxs-lookup"><span data-stu-id="7542c-197">yes</span></span>      | <span data-ttu-id="7542c-198">Verze balíčku normalized a psané malými písmeny</span><span class="sxs-lookup"><span data-stu-id="7542c-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="7542c-199">Obě `LOWER_ID` a `LOWER_VERSION` jsou psané malými písmeny pomocí pravidel implementované. NET na [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) metoda.</span><span class="sxs-lookup"><span data-stu-id="7542c-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="7542c-200">`LOWER_VERSION` Je verze balíčku požadované normalized pomocí verze NuGet [normalizaci pravidla](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="7542c-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="7542c-201">To znamená, že aby metadata sestavení, kterou specifikace SemVer 2.0.0 se musí v tomto případě vyloučit.</span><span class="sxs-lookup"><span data-stu-id="7542c-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="7542c-202">Text odpovědi</span><span class="sxs-lookup"><span data-stu-id="7542c-202">Response body</span></span>

<span data-ttu-id="7542c-203">Pokud balíček existuje ve zdroji balíčku, je vrácena 200 stavový kód.</span><span class="sxs-lookup"><span data-stu-id="7542c-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="7542c-204">Text odpovědi bude manifest balíčku, který je příponou .nuspec obsažené v odpovídající .nupkg.</span><span class="sxs-lookup"><span data-stu-id="7542c-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="7542c-205">Příponou .nuspec je dokument XML.</span><span class="sxs-lookup"><span data-stu-id="7542c-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="7542c-206">Pokud balíček neexistuje ve zdroji balíčku, je vrácena 404 stavový kód.</span><span class="sxs-lookup"><span data-stu-id="7542c-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="7542c-207">Ukázková žádost</span><span class="sxs-lookup"><span data-stu-id="7542c-207">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="7542c-208">Ukázková odpověď</span><span class="sxs-lookup"><span data-stu-id="7542c-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
