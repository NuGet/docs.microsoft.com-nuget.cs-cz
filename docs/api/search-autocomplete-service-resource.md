---
title: Automatické dokončování, rozhraní API Nugetu
description: Vyhledávací služba Automatické dokončování podporuje interaktivní zjišťování balíčku ID a verze.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: fdc3ad8aa239a42d8a4c169a757715e856bdcb41
ms.sourcegitcommit: 9f94e00428d83aef4a7a87db679129eff7720c59
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/03/2019
ms.locfileid: "58911046"
---
# <a name="autocomplete"></a><span data-ttu-id="a3fd7-103">Automatické dokončování</span><span class="sxs-lookup"><span data-stu-id="a3fd7-103">Autocomplete</span></span>

<span data-ttu-id="a3fd7-104">Je možné vytvořit balíček ID a verzi automatického dokončování prostředí pomocí rozhraní API V3.</span><span class="sxs-lookup"><span data-stu-id="a3fd7-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="a3fd7-105">Je prostředek, který používá pro automatické dokončování dotazů `SearchAutocompleteService` prostředek se nenašel v [index služby](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="a3fd7-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="a3fd7-106">Správa verzí</span><span class="sxs-lookup"><span data-stu-id="a3fd7-106">Versioning</span></span>

<span data-ttu-id="a3fd7-107">Následující `@type` hodnoty:</span><span class="sxs-lookup"><span data-stu-id="a3fd7-107">The following `@type` values are used:</span></span>

<span data-ttu-id="a3fd7-108">@type Hodnota</span><span class="sxs-lookup"><span data-stu-id="a3fd7-108">@type value</span></span>                          | <span data-ttu-id="a3fd7-109">Poznámky</span><span class="sxs-lookup"><span data-stu-id="a3fd7-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="a3fd7-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="a3fd7-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="a3fd7-111">Počáteční verze</span><span class="sxs-lookup"><span data-stu-id="a3fd7-111">The initial release</span></span>
<span data-ttu-id="a3fd7-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="a3fd7-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="a3fd7-113">Alias of</span><span class="sxs-lookup"><span data-stu-id="a3fd7-113">Alias of</span></span> `SearchAutocompleteService`
<span data-ttu-id="a3fd7-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="a3fd7-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="a3fd7-115">Alias of</span><span class="sxs-lookup"><span data-stu-id="a3fd7-115">Alias of</span></span> `SearchAutocompleteService`

## <a name="base-url"></a><span data-ttu-id="a3fd7-116">Základní adresa URL</span><span class="sxs-lookup"><span data-stu-id="a3fd7-116">Base URL</span></span>

<span data-ttu-id="a3fd7-117">Základní adresa URL pro následující rozhraní API je hodnota `@id` vlastnost přiřazené k některému z výše uvedených prostředků `@type` hodnoty.</span><span class="sxs-lookup"><span data-stu-id="a3fd7-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="a3fd7-118">V následujícím dokumentu, zástupný symbol základní adresa URL `{@id}` se použije.</span><span class="sxs-lookup"><span data-stu-id="a3fd7-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="a3fd7-119">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="a3fd7-119">HTTP Methods</span></span>

<span data-ttu-id="a3fd7-120">Všechny adresy URL, které jsou součástí zdroje podpory registrace metody HTTP `GET` a `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="a3fd7-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="a3fd7-121">Vyhledejte balíček ID</span><span class="sxs-lookup"><span data-stu-id="a3fd7-121">Search for package IDs</span></span>

<span data-ttu-id="a3fd7-122">První funkce automatického dokončování rozhraní API podporuje vyhledávání část řetězce ID balíčku.</span><span class="sxs-lookup"><span data-stu-id="a3fd7-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="a3fd7-123">To je skvělé, pokud byste chtěli poskytnout funkce typeahead balíčku v uživatelském rozhraní, integrovaný s zdroj balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="a3fd7-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="a3fd7-124">Balíček se pouze neuvedené v seznamu verzí se nezobrazí ve výsledcích.</span><span class="sxs-lookup"><span data-stu-id="a3fd7-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="a3fd7-125">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="a3fd7-125">Request parameters</span></span>

<span data-ttu-id="a3fd7-126">Name</span><span class="sxs-lookup"><span data-stu-id="a3fd7-126">Name</span></span>        | <span data-ttu-id="a3fd7-127">V</span><span class="sxs-lookup"><span data-stu-id="a3fd7-127">In</span></span>     | <span data-ttu-id="a3fd7-128">Type</span><span class="sxs-lookup"><span data-stu-id="a3fd7-128">Type</span></span>    | <span data-ttu-id="a3fd7-129">Požadováno</span><span class="sxs-lookup"><span data-stu-id="a3fd7-129">Required</span></span> | <span data-ttu-id="a3fd7-130">Poznámky</span><span class="sxs-lookup"><span data-stu-id="a3fd7-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="a3fd7-131">q</span><span class="sxs-lookup"><span data-stu-id="a3fd7-131">q</span></span>           | <span data-ttu-id="a3fd7-132">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="a3fd7-132">URL</span></span>    | <span data-ttu-id="a3fd7-133">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="a3fd7-133">string</span></span>  | <span data-ttu-id="a3fd7-134">Ne</span><span class="sxs-lookup"><span data-stu-id="a3fd7-134">no</span></span>       | <span data-ttu-id="a3fd7-135">Řetězec určený k porovnání s ID balíčku</span><span class="sxs-lookup"><span data-stu-id="a3fd7-135">The string to compare against package IDs</span></span>
<span data-ttu-id="a3fd7-136">Přeskočit</span><span class="sxs-lookup"><span data-stu-id="a3fd7-136">skip</span></span>        | <span data-ttu-id="a3fd7-137">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="a3fd7-137">URL</span></span>    | <span data-ttu-id="a3fd7-138">integer</span><span class="sxs-lookup"><span data-stu-id="a3fd7-138">integer</span></span> | <span data-ttu-id="a3fd7-139">Ne</span><span class="sxs-lookup"><span data-stu-id="a3fd7-139">no</span></span>       | <span data-ttu-id="a3fd7-140">Počet výsledků, chcete-li přeskočit pro stránkování</span><span class="sxs-lookup"><span data-stu-id="a3fd7-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="a3fd7-141">Take</span><span class="sxs-lookup"><span data-stu-id="a3fd7-141">take</span></span>        | <span data-ttu-id="a3fd7-142">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="a3fd7-142">URL</span></span>    | <span data-ttu-id="a3fd7-143">integer</span><span class="sxs-lookup"><span data-stu-id="a3fd7-143">integer</span></span> | <span data-ttu-id="a3fd7-144">Ne</span><span class="sxs-lookup"><span data-stu-id="a3fd7-144">no</span></span>       | <span data-ttu-id="a3fd7-145">Počet výsledků, které má být vrácen pro stránkování</span><span class="sxs-lookup"><span data-stu-id="a3fd7-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="a3fd7-146">platnost předběžné verze</span><span class="sxs-lookup"><span data-stu-id="a3fd7-146">prerelease</span></span>  | <span data-ttu-id="a3fd7-147">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="a3fd7-147">URL</span></span>    | <span data-ttu-id="a3fd7-148">Logická hodnota</span><span class="sxs-lookup"><span data-stu-id="a3fd7-148">boolean</span></span> | <span data-ttu-id="a3fd7-149">Ne</span><span class="sxs-lookup"><span data-stu-id="a3fd7-149">no</span></span>       | `true` <span data-ttu-id="a3fd7-150">nebo `false` určující, jestli se mají zahrnout [balíčky v předběžné verzi](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="a3fd7-150">or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="a3fd7-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="a3fd7-151">semVerLevel</span></span> | <span data-ttu-id="a3fd7-152">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="a3fd7-152">URL</span></span>    | <span data-ttu-id="a3fd7-153">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="a3fd7-153">string</span></span>  | <span data-ttu-id="a3fd7-154">Ne</span><span class="sxs-lookup"><span data-stu-id="a3fd7-154">no</span></span>       | <span data-ttu-id="a3fd7-155">Řetězec verze SemVer 1.0.0</span><span class="sxs-lookup"><span data-stu-id="a3fd7-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="a3fd7-156">Automatické dokončování dotazů `q` je analyzován způsobem, který je definován implementací serveru.</span><span class="sxs-lookup"><span data-stu-id="a3fd7-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="a3fd7-157">nuget.org podporuje dotazování pro předponu tokeny typu ID balíčku, které jsou částí ID vytvářených spliting původní znaky stylem camel case a symbol.</span><span class="sxs-lookup"><span data-stu-id="a3fd7-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="a3fd7-158">`skip` Parametr má výchozí hodnotu 0.</span><span class="sxs-lookup"><span data-stu-id="a3fd7-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="a3fd7-159">`take` Parametr by měl být celé číslo větší než nula.</span><span class="sxs-lookup"><span data-stu-id="a3fd7-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="a3fd7-160">Implementace serveru může uložit maximální hodnotu.</span><span class="sxs-lookup"><span data-stu-id="a3fd7-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="a3fd7-161">Pokud `prerelease` není zadán, jsou vyloučeny balíčky v předběžné verzi.</span><span class="sxs-lookup"><span data-stu-id="a3fd7-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="a3fd7-162">`semVerLevel` Parametr dotazu se používá k přihlášení k [SemVer 2.0.0 balíčky](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span><span class="sxs-lookup"><span data-stu-id="a3fd7-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="a3fd7-163">Pokud tento parametr dotazu je vyloučený, vrátí se pouze balíček ID s SemVer 1.0.0 kompatibilní verze (s [standardní správy verzí NuGet](../reference/package-versioning.md) upozornění, jako jsou třeba řetězce verze 4 dali celé číslo).</span><span class="sxs-lookup"><span data-stu-id="a3fd7-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="a3fd7-164">Pokud `semVerLevel=2.0.0` je k dispozici, bude vrácen SemVer 1.0.0 a kompatibilní balíčky SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="a3fd7-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="a3fd7-165">Zobrazit [SemVer 2.0.0 podpora nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) Další informace.</span><span class="sxs-lookup"><span data-stu-id="a3fd7-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="a3fd7-166">Odpověď</span><span class="sxs-lookup"><span data-stu-id="a3fd7-166">Response</span></span>

<span data-ttu-id="a3fd7-167">Odpověď je dokument JSON obsahující až `take` výsledky automatického dokončování.</span><span class="sxs-lookup"><span data-stu-id="a3fd7-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="a3fd7-168">Kořenový objekt JSON má následující vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="a3fd7-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="a3fd7-169">Name</span><span class="sxs-lookup"><span data-stu-id="a3fd7-169">Name</span></span>      | <span data-ttu-id="a3fd7-170">Type</span><span class="sxs-lookup"><span data-stu-id="a3fd7-170">Type</span></span>             | <span data-ttu-id="a3fd7-171">Požadováno</span><span class="sxs-lookup"><span data-stu-id="a3fd7-171">Required</span></span> | <span data-ttu-id="a3fd7-172">Poznámky</span><span class="sxs-lookup"><span data-stu-id="a3fd7-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="a3fd7-173">totalHits</span><span class="sxs-lookup"><span data-stu-id="a3fd7-173">totalHits</span></span> | <span data-ttu-id="a3fd7-174">integer</span><span class="sxs-lookup"><span data-stu-id="a3fd7-174">integer</span></span>          | <span data-ttu-id="a3fd7-175">ano</span><span class="sxs-lookup"><span data-stu-id="a3fd7-175">yes</span></span>      | <span data-ttu-id="a3fd7-176">Celkový počet shod, bez ohledu na `skip` a</span><span class="sxs-lookup"><span data-stu-id="a3fd7-176">The total number of matches, disregarding `skip` and</span></span> `take`
<span data-ttu-id="a3fd7-177">data</span><span class="sxs-lookup"><span data-stu-id="a3fd7-177">data</span></span>      | <span data-ttu-id="a3fd7-178">pole řetězců</span><span class="sxs-lookup"><span data-stu-id="a3fd7-178">array of strings</span></span> | <span data-ttu-id="a3fd7-179">ano</span><span class="sxs-lookup"><span data-stu-id="a3fd7-179">yes</span></span>      | <span data-ttu-id="a3fd7-180">Balíček odpovídající ID požadavku</span><span class="sxs-lookup"><span data-stu-id="a3fd7-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="a3fd7-181">Ukázková žádost</span><span class="sxs-lookup"><span data-stu-id="a3fd7-181">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="a3fd7-182">Ukázková odpověď</span><span class="sxs-lookup"><span data-stu-id="a3fd7-182">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="a3fd7-183">Výčet verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="a3fd7-183">Enumerate package versions</span></span>

<span data-ttu-id="a3fd7-184">Po zjištění ID balíčku používat předchozí rozhraní API, může klient používat automatické dokončování rozhraní API k vytvoření výčtu verze balíčku pro ID zadaného balíčku.</span><span class="sxs-lookup"><span data-stu-id="a3fd7-184">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="a3fd7-185">Verze balíčku, který je neuvedené v seznamu se nezobrazí ve výsledcích.</span><span class="sxs-lookup"><span data-stu-id="a3fd7-185">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="a3fd7-186">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="a3fd7-186">Request parameters</span></span>

<span data-ttu-id="a3fd7-187">Name</span><span class="sxs-lookup"><span data-stu-id="a3fd7-187">Name</span></span>        | <span data-ttu-id="a3fd7-188">V</span><span class="sxs-lookup"><span data-stu-id="a3fd7-188">In</span></span>     | <span data-ttu-id="a3fd7-189">Type</span><span class="sxs-lookup"><span data-stu-id="a3fd7-189">Type</span></span>    | <span data-ttu-id="a3fd7-190">Požadováno</span><span class="sxs-lookup"><span data-stu-id="a3fd7-190">Required</span></span> | <span data-ttu-id="a3fd7-191">Poznámky</span><span class="sxs-lookup"><span data-stu-id="a3fd7-191">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="a3fd7-192">id</span><span class="sxs-lookup"><span data-stu-id="a3fd7-192">id</span></span>          | <span data-ttu-id="a3fd7-193">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="a3fd7-193">URL</span></span>    | <span data-ttu-id="a3fd7-194">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="a3fd7-194">string</span></span>  | <span data-ttu-id="a3fd7-195">ano</span><span class="sxs-lookup"><span data-stu-id="a3fd7-195">yes</span></span>      | <span data-ttu-id="a3fd7-196">ID balíčku k načtení verze pro</span><span class="sxs-lookup"><span data-stu-id="a3fd7-196">The package ID to fetch versions for</span></span>
<span data-ttu-id="a3fd7-197">platnost předběžné verze</span><span class="sxs-lookup"><span data-stu-id="a3fd7-197">prerelease</span></span>  | <span data-ttu-id="a3fd7-198">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="a3fd7-198">URL</span></span>    | <span data-ttu-id="a3fd7-199">Logická hodnota</span><span class="sxs-lookup"><span data-stu-id="a3fd7-199">boolean</span></span> | <span data-ttu-id="a3fd7-200">Ne</span><span class="sxs-lookup"><span data-stu-id="a3fd7-200">no</span></span>       | `true` <span data-ttu-id="a3fd7-201">nebo `false` určující, jestli se mají zahrnout [balíčky v předběžné verzi](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="a3fd7-201">or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="a3fd7-202">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="a3fd7-202">semVerLevel</span></span> | <span data-ttu-id="a3fd7-203">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="a3fd7-203">URL</span></span>    | <span data-ttu-id="a3fd7-204">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="a3fd7-204">string</span></span>  | <span data-ttu-id="a3fd7-205">Ne</span><span class="sxs-lookup"><span data-stu-id="a3fd7-205">no</span></span>       | <span data-ttu-id="a3fd7-206">Řetězec SemVer 2.0.0 verze</span><span class="sxs-lookup"><span data-stu-id="a3fd7-206">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="a3fd7-207">Pokud `prerelease` není zadán, jsou vyloučeny balíčky v předběžné verzi.</span><span class="sxs-lookup"><span data-stu-id="a3fd7-207">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="a3fd7-208">`semVerLevel` Parametr dotazu se používá k přihlášení k SemVer 2.0.0 balíčky.</span><span class="sxs-lookup"><span data-stu-id="a3fd7-208">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="a3fd7-209">Pokud tento parametr dotazu je vyloučený, vrátí se pouze verze SemVer 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="a3fd7-209">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="a3fd7-210">Pokud `semVerLevel=2.0.0` je k dispozici, bude vrácen SemVer 1.0.0 a verze SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="a3fd7-210">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="a3fd7-211">Zobrazit [SemVer 2.0.0 podpora nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) Další informace.</span><span class="sxs-lookup"><span data-stu-id="a3fd7-211">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="a3fd7-212">Odpověď</span><span class="sxs-lookup"><span data-stu-id="a3fd7-212">Response</span></span>

<span data-ttu-id="a3fd7-213">Odpověď je dokument JSON obsahující všechny verze balíčků poskytovaný balíček ID, daný dotaz s parametry filtrování.</span><span class="sxs-lookup"><span data-stu-id="a3fd7-213">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="a3fd7-214">Kořenový objekt JSON má následující vlastnost:</span><span class="sxs-lookup"><span data-stu-id="a3fd7-214">The root JSON object has the following property:</span></span>

<span data-ttu-id="a3fd7-215">Name</span><span class="sxs-lookup"><span data-stu-id="a3fd7-215">Name</span></span>      | <span data-ttu-id="a3fd7-216">Type</span><span class="sxs-lookup"><span data-stu-id="a3fd7-216">Type</span></span>             | <span data-ttu-id="a3fd7-217">Požadováno</span><span class="sxs-lookup"><span data-stu-id="a3fd7-217">Required</span></span> | <span data-ttu-id="a3fd7-218">Poznámky</span><span class="sxs-lookup"><span data-stu-id="a3fd7-218">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="a3fd7-219">data</span><span class="sxs-lookup"><span data-stu-id="a3fd7-219">data</span></span>      | <span data-ttu-id="a3fd7-220">pole řetězců</span><span class="sxs-lookup"><span data-stu-id="a3fd7-220">array of strings</span></span> | <span data-ttu-id="a3fd7-221">ano</span><span class="sxs-lookup"><span data-stu-id="a3fd7-221">yes</span></span>      | <span data-ttu-id="a3fd7-222">Verze balíčku, který odpovídá požadavku</span><span class="sxs-lookup"><span data-stu-id="a3fd7-222">The package versions matched by the request</span></span>

<span data-ttu-id="a3fd7-223">Verze balíčku v `data` pole může obsahovat metadata sestavení SemVer 2.0.0 (třeba `1.0.0+metadata`) Pokud `semVerLevel=2.0.0` je k dispozici v řetězci dotazu.</span><span class="sxs-lookup"><span data-stu-id="a3fd7-223">The package versions in the `data` array may contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` is provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="a3fd7-224">Ukázková žádost</span><span class="sxs-lookup"><span data-stu-id="a3fd7-224">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="a3fd7-225">Ukázková odpověď</span><span class="sxs-lookup"><span data-stu-id="a3fd7-225">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
