---
title: "Automatické dokončování, NuGet rozhraní API | Microsoft Docs"
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
description: "Službu vyhledávání automatického dokončování podporuje interaktivní zjišťování ID balíčku a verze."
keywords: "Rozhraní API funkce automatického dokončování NuGet, ID balíčku NuGet vyhledávání, ID balíčku dílčí řetězec"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 7c984ca61799293d7832851b80cf3fefc4734288
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/02/2018
---
# <a name="autocomplete"></a><span data-ttu-id="e03a3-104">Automatické dokončování</span><span class="sxs-lookup"><span data-stu-id="e03a3-104">Autocomplete</span></span>

<span data-ttu-id="e03a3-105">Je možné balíček ID a verzi automatického dokončování prostředí pomocí rozhraní API V3.</span><span class="sxs-lookup"><span data-stu-id="e03a3-105">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="e03a3-106">Prostředku používaného pro zadávání dotazů automatického dokončování je `SearchAutocompleteService` v nalezen prostředek [indexu služby](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="e03a3-106">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="e03a3-107">Správa verzí</span><span class="sxs-lookup"><span data-stu-id="e03a3-107">Versioning</span></span>

<span data-ttu-id="e03a3-108">Následující `@type` se používají hodnoty:</span><span class="sxs-lookup"><span data-stu-id="e03a3-108">The following `@type` values are used:</span></span>

<span data-ttu-id="e03a3-109">@typeHodnota</span><span class="sxs-lookup"><span data-stu-id="e03a3-109">@type value</span></span>                          | <span data-ttu-id="e03a3-110">Poznámky</span><span class="sxs-lookup"><span data-stu-id="e03a3-110">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="e03a3-111">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="e03a3-111">SearchAutocompleteService</span></span>            | <span data-ttu-id="e03a3-112">Původní verze</span><span class="sxs-lookup"><span data-stu-id="e03a3-112">The initial release</span></span>
<span data-ttu-id="e03a3-113">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="e03a3-113">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="e03a3-114">Alias`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="e03a3-114">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="e03a3-115">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="e03a3-115">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="e03a3-116">Alias`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="e03a3-116">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="e03a3-117">Základní adresu URL</span><span class="sxs-lookup"><span data-stu-id="e03a3-117">Base URL</span></span>

<span data-ttu-id="e03a3-118">Základní adresu URL pro následující rozhraní API je hodnota `@id` vlastnost spojená s jedním z výše uvedených prostředků `@type` hodnoty.</span><span class="sxs-lookup"><span data-stu-id="e03a3-118">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="e03a3-119">V následujícím dokumentu zástupného textu základní adresa URL `{@id}` se použije.</span><span class="sxs-lookup"><span data-stu-id="e03a3-119">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="e03a3-120">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="e03a3-120">HTTP Methods</span></span>

<span data-ttu-id="e03a3-121">Všechny adresy URL v podpory registrace prostředků nalezen metody HTTP `GET` a `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="e03a3-121">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="e03a3-122">Vyhledávání pro balíček ID</span><span class="sxs-lookup"><span data-stu-id="e03a3-122">Search for package IDs</span></span>

<span data-ttu-id="e03a3-123">První autocomplete rozhraní API podporuje hledání část řetězce ID balíčku.</span><span class="sxs-lookup"><span data-stu-id="e03a3-123">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="e03a3-124">To je skvělé, pokud chcete poskytovat funkce typeahead balíčku v uživatelském rozhraní integrovat zdroje balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="e03a3-124">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="e03a3-125">Balíček se pouze neuvedené verzí se nezobrazí ve výsledcích.</span><span class="sxs-lookup"><span data-stu-id="e03a3-125">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="e03a3-126">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="e03a3-126">Request parameters</span></span>

<span data-ttu-id="e03a3-127">Název</span><span class="sxs-lookup"><span data-stu-id="e03a3-127">Name</span></span>        | <span data-ttu-id="e03a3-128">V</span><span class="sxs-lookup"><span data-stu-id="e03a3-128">In</span></span>     | <span data-ttu-id="e03a3-129">Typ</span><span class="sxs-lookup"><span data-stu-id="e03a3-129">Type</span></span>    | <span data-ttu-id="e03a3-130">Požadováno</span><span class="sxs-lookup"><span data-stu-id="e03a3-130">Required</span></span> | <span data-ttu-id="e03a3-131">Poznámky</span><span class="sxs-lookup"><span data-stu-id="e03a3-131">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="e03a3-132">q</span><span class="sxs-lookup"><span data-stu-id="e03a3-132">q</span></span>           | <span data-ttu-id="e03a3-133">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="e03a3-133">URL</span></span>    | <span data-ttu-id="e03a3-134">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="e03a3-134">string</span></span>  | <span data-ttu-id="e03a3-135">Ne</span><span class="sxs-lookup"><span data-stu-id="e03a3-135">no</span></span>       | <span data-ttu-id="e03a3-136">Řetězec, který má být porovnán balíček ID</span><span class="sxs-lookup"><span data-stu-id="e03a3-136">The string to compare against package IDs</span></span>
<span data-ttu-id="e03a3-137">Přeskočit</span><span class="sxs-lookup"><span data-stu-id="e03a3-137">skip</span></span>        | <span data-ttu-id="e03a3-138">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="e03a3-138">URL</span></span>    | <span data-ttu-id="e03a3-139">integer</span><span class="sxs-lookup"><span data-stu-id="e03a3-139">integer</span></span> | <span data-ttu-id="e03a3-140">Ne</span><span class="sxs-lookup"><span data-stu-id="e03a3-140">no</span></span>       | <span data-ttu-id="e03a3-141">Počet výsledků tak, aby přeskočil pro stránkování</span><span class="sxs-lookup"><span data-stu-id="e03a3-141">The number of results to skip, for pagination</span></span>
<span data-ttu-id="e03a3-142">proveďte</span><span class="sxs-lookup"><span data-stu-id="e03a3-142">take</span></span>        | <span data-ttu-id="e03a3-143">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="e03a3-143">URL</span></span>    | <span data-ttu-id="e03a3-144">integer</span><span class="sxs-lookup"><span data-stu-id="e03a3-144">integer</span></span> | <span data-ttu-id="e03a3-145">Ne</span><span class="sxs-lookup"><span data-stu-id="e03a3-145">no</span></span>       | <span data-ttu-id="e03a3-146">Počet výsledků, které má být vrácen pro stránkování</span><span class="sxs-lookup"><span data-stu-id="e03a3-146">The number of results to return, for pagination</span></span>
<span data-ttu-id="e03a3-147">předběžné verze</span><span class="sxs-lookup"><span data-stu-id="e03a3-147">prerelease</span></span>  | <span data-ttu-id="e03a3-148">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="e03a3-148">URL</span></span>    | <span data-ttu-id="e03a3-149">Logická hodnota</span><span class="sxs-lookup"><span data-stu-id="e03a3-149">boolean</span></span> | <span data-ttu-id="e03a3-150">Ne</span><span class="sxs-lookup"><span data-stu-id="e03a3-150">no</span></span>       | <span data-ttu-id="e03a3-151">`true`nebo `false` určení, jestli se mají zahrnout [předběžné verze balíčků](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="e03a3-151">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="e03a3-152">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="e03a3-152">semVerLevel</span></span> | <span data-ttu-id="e03a3-153">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="e03a3-153">URL</span></span>    | <span data-ttu-id="e03a3-154">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="e03a3-154">string</span></span>  | <span data-ttu-id="e03a3-155">Ne</span><span class="sxs-lookup"><span data-stu-id="e03a3-155">no</span></span>       | <span data-ttu-id="e03a3-156">Řetězec verze o SemVer 1.0.0</span><span class="sxs-lookup"><span data-stu-id="e03a3-156">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="e03a3-157">Automatické dokončování dotazů `q` je analyzována způsobem, který je definován implementaci serveru.</span><span class="sxs-lookup"><span data-stu-id="e03a3-157">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="e03a3-158">nuget.org podporuje dotazování pro předponu tokenů ID balíčku, které jsou částí ID vyprodukované spliting původní formátu camelCase případ a symbol znaky.</span><span class="sxs-lookup"><span data-stu-id="e03a3-158">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="e03a3-159">`skip` Výchozí hodnoty parametrů na hodnotu 0.</span><span class="sxs-lookup"><span data-stu-id="e03a3-159">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="e03a3-160">`take` Parametr by měl být celé číslo větší než nula.</span><span class="sxs-lookup"><span data-stu-id="e03a3-160">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="e03a3-161">Implementaci serveru může uložit maximální hodnotu.</span><span class="sxs-lookup"><span data-stu-id="e03a3-161">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="e03a3-162">Pokud `prerelease` není zadána, jsou vyloučeny předběžné verze balíčků.</span><span class="sxs-lookup"><span data-stu-id="e03a3-162">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="e03a3-163">`semVerLevel` Parametr dotazu se používá k vyslovení souhlasu s [SemVer 2.0.0 balíčky](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span><span class="sxs-lookup"><span data-stu-id="e03a3-163">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="e03a3-164">Pokud tento parametr dotazu je vyloučená, bude vrácen pouze balíček ID s kompatibilní verze SemVer 1.0.0 (s [standardní verze NuGet](../reference/package-versioning.md) upozornění, jako jsou třeba řetězce verze se 4 kusy celé číslo).</span><span class="sxs-lookup"><span data-stu-id="e03a3-164">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="e03a3-165">Pokud `semVerLevel=2.0.0` je zadáno, bude vrácen SemVer 1.0.0 a SemVer 2.0.0 kompatibilní balíčky.</span><span class="sxs-lookup"><span data-stu-id="e03a3-165">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="e03a3-166">Najdete v článku [SemVer 2.0.0 podpora nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) Další informace.</span><span class="sxs-lookup"><span data-stu-id="e03a3-166">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="e03a3-167">Odpověď</span><span class="sxs-lookup"><span data-stu-id="e03a3-167">Response</span></span>

<span data-ttu-id="e03a3-168">Odpovědí je dokument JSON obsahující až `take` výsledky funkce automatického dokončování.</span><span class="sxs-lookup"><span data-stu-id="e03a3-168">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="e03a3-169">Kořenový objekt JSON má následující vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="e03a3-169">The root JSON object has the following properties:</span></span>

<span data-ttu-id="e03a3-170">Název</span><span class="sxs-lookup"><span data-stu-id="e03a3-170">Name</span></span>      | <span data-ttu-id="e03a3-171">Typ</span><span class="sxs-lookup"><span data-stu-id="e03a3-171">Type</span></span>             | <span data-ttu-id="e03a3-172">Požadováno</span><span class="sxs-lookup"><span data-stu-id="e03a3-172">Required</span></span> | <span data-ttu-id="e03a3-173">Poznámky</span><span class="sxs-lookup"><span data-stu-id="e03a3-173">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="e03a3-174">totalHits</span><span class="sxs-lookup"><span data-stu-id="e03a3-174">totalHits</span></span> | <span data-ttu-id="e03a3-175">integer</span><span class="sxs-lookup"><span data-stu-id="e03a3-175">integer</span></span>          | <span data-ttu-id="e03a3-176">Ano</span><span class="sxs-lookup"><span data-stu-id="e03a3-176">yes</span></span>      | <span data-ttu-id="e03a3-177">Celkový počet shod, bez ohledu na `skip` a`take`</span><span class="sxs-lookup"><span data-stu-id="e03a3-177">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="e03a3-178">data</span><span class="sxs-lookup"><span data-stu-id="e03a3-178">data</span></span>      | <span data-ttu-id="e03a3-179">Pole řetězců.</span><span class="sxs-lookup"><span data-stu-id="e03a3-179">array of strings</span></span> | <span data-ttu-id="e03a3-180">Ano</span><span class="sxs-lookup"><span data-stu-id="e03a3-180">yes</span></span>      | <span data-ttu-id="e03a3-181">ID balíčku odpovídala požadavku</span><span class="sxs-lookup"><span data-stu-id="e03a3-181">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="e03a3-182">Ukázková žádost</span><span class="sxs-lookup"><span data-stu-id="e03a3-182">Sample request</span></span>

<span data-ttu-id="e03a3-183">GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span><span class="sxs-lookup"><span data-stu-id="e03a3-183">GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span></span>

### <a name="sample-response"></a><span data-ttu-id="e03a3-184">Ukázková odpověď</span><span class="sxs-lookup"><span data-stu-id="e03a3-184">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="e03a3-185">Zobrazení výčtu verze balíčku</span><span class="sxs-lookup"><span data-stu-id="e03a3-185">Enumerate package versions</span></span>

<span data-ttu-id="e03a3-186">Po zjištění ID balíčku pomocí předchozího rozhraní API může klient používat automatické dokončování rozhraní API se vytvořit výčet verze balíčku pro ID zadaný balíček.</span><span class="sxs-lookup"><span data-stu-id="e03a3-186">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="e03a3-187">Verze balíčku, který neuvedené nezobrazí ve výsledcích.</span><span class="sxs-lookup"><span data-stu-id="e03a3-187">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="e03a3-188">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="e03a3-188">Request parameters</span></span>

<span data-ttu-id="e03a3-189">Název</span><span class="sxs-lookup"><span data-stu-id="e03a3-189">Name</span></span>        | <span data-ttu-id="e03a3-190">V</span><span class="sxs-lookup"><span data-stu-id="e03a3-190">In</span></span>     | <span data-ttu-id="e03a3-191">Typ</span><span class="sxs-lookup"><span data-stu-id="e03a3-191">Type</span></span>    | <span data-ttu-id="e03a3-192">Požadováno</span><span class="sxs-lookup"><span data-stu-id="e03a3-192">Required</span></span> | <span data-ttu-id="e03a3-193">Poznámky</span><span class="sxs-lookup"><span data-stu-id="e03a3-193">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="e03a3-194">id</span><span class="sxs-lookup"><span data-stu-id="e03a3-194">id</span></span>          | <span data-ttu-id="e03a3-195">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="e03a3-195">URL</span></span>    | <span data-ttu-id="e03a3-196">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="e03a3-196">string</span></span>  | <span data-ttu-id="e03a3-197">Ano</span><span class="sxs-lookup"><span data-stu-id="e03a3-197">yes</span></span>      | <span data-ttu-id="e03a3-198">ID balíčku se načíst verze pro</span><span class="sxs-lookup"><span data-stu-id="e03a3-198">The package ID to fetch versions for</span></span>
<span data-ttu-id="e03a3-199">předběžné verze</span><span class="sxs-lookup"><span data-stu-id="e03a3-199">prerelease</span></span>  | <span data-ttu-id="e03a3-200">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="e03a3-200">URL</span></span>    | <span data-ttu-id="e03a3-201">Logická hodnota</span><span class="sxs-lookup"><span data-stu-id="e03a3-201">boolean</span></span> | <span data-ttu-id="e03a3-202">Ne</span><span class="sxs-lookup"><span data-stu-id="e03a3-202">no</span></span>       | <span data-ttu-id="e03a3-203">`true`nebo `false` určení, jestli se mají zahrnout [předběžné verze balíčků](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="e03a3-203">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="e03a3-204">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="e03a3-204">semVerLevel</span></span> | <span data-ttu-id="e03a3-205">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="e03a3-205">URL</span></span>    | <span data-ttu-id="e03a3-206">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="e03a3-206">string</span></span>  | <span data-ttu-id="e03a3-207">Ne</span><span class="sxs-lookup"><span data-stu-id="e03a3-207">no</span></span>       | <span data-ttu-id="e03a3-208">Řetězec verze o SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="e03a3-208">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="e03a3-209">Pokud `prerelease` není zadána, jsou vyloučeny předběžné verze balíčků.</span><span class="sxs-lookup"><span data-stu-id="e03a3-209">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="e03a3-210">`semVerLevel` Parametr dotazu se používá k vyslovení souhlasu s SemVer 2.0.0 balíčky.</span><span class="sxs-lookup"><span data-stu-id="e03a3-210">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="e03a3-211">Pokud tento parametr dotazu je vyloučená, bude vrácen pouze SemVer 1.0.0 verze.</span><span class="sxs-lookup"><span data-stu-id="e03a3-211">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="e03a3-212">Pokud `semVerLevel=2.0.0` je zadáno, bude vrácen SemVer 1.0.0 a SemVer 2.0.0 verze.</span><span class="sxs-lookup"><span data-stu-id="e03a3-212">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="e03a3-213">Najdete v článku [SemVer 2.0.0 podpora nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) Další informace.</span><span class="sxs-lookup"><span data-stu-id="e03a3-213">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="e03a3-214">Odpověď</span><span class="sxs-lookup"><span data-stu-id="e03a3-214">Response</span></span>

<span data-ttu-id="e03a3-215">Odpověď je dokument JSON obsahující všechny verze balíčku zadaný balíček ID, filtrování podle parametrů daný dotaz.</span><span class="sxs-lookup"><span data-stu-id="e03a3-215">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="e03a3-216">Kořenový objekt JSON má následující vlastnost:</span><span class="sxs-lookup"><span data-stu-id="e03a3-216">The root JSON object has the following property:</span></span>

<span data-ttu-id="e03a3-217">Název</span><span class="sxs-lookup"><span data-stu-id="e03a3-217">Name</span></span>      | <span data-ttu-id="e03a3-218">Typ</span><span class="sxs-lookup"><span data-stu-id="e03a3-218">Type</span></span>             | <span data-ttu-id="e03a3-219">Požadováno</span><span class="sxs-lookup"><span data-stu-id="e03a3-219">Required</span></span> | <span data-ttu-id="e03a3-220">Poznámky</span><span class="sxs-lookup"><span data-stu-id="e03a3-220">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="e03a3-221">data</span><span class="sxs-lookup"><span data-stu-id="e03a3-221">data</span></span>      | <span data-ttu-id="e03a3-222">Pole řetězců.</span><span class="sxs-lookup"><span data-stu-id="e03a3-222">array of strings</span></span> | <span data-ttu-id="e03a3-223">Ano</span><span class="sxs-lookup"><span data-stu-id="e03a3-223">yes</span></span>      | <span data-ttu-id="e03a3-224">Verze balíčku odpovídala požadavku</span><span class="sxs-lookup"><span data-stu-id="e03a3-224">The package versions matched by the request</span></span>

<span data-ttu-id="e03a3-225">Verze v balíčku `data` pole může obsahovat metadata sestavení SemVer 2.0.0 (například `1.0.0+metadata`) Pokud `semVerLevel=2.0.0` zadaná v řetězci dotazu.</span><span class="sxs-lookup"><span data-stu-id="e03a3-225">The package versions in the `data` array could contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` was provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="e03a3-226">Ukázková žádost</span><span class="sxs-lookup"><span data-stu-id="e03a3-226">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="e03a3-227">Ukázková odpověď</span><span class="sxs-lookup"><span data-stu-id="e03a3-227">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
