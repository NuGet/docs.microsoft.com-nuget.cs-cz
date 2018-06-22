---
title: Automatické dokončování, NuGet rozhraní API
description: Službu vyhledávání automatického dokončování podporuje interaktivní zjišťování ID balíčku a verze.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: d5e1936c6c5406a1a376c16b2bad5351320dfb4f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822133"
---
# <a name="autocomplete"></a><span data-ttu-id="4d3e1-103">Automatické dokončování</span><span class="sxs-lookup"><span data-stu-id="4d3e1-103">Autocomplete</span></span>

<span data-ttu-id="4d3e1-104">Je možné balíček ID a verzi automatického dokončování prostředí pomocí rozhraní API V3.</span><span class="sxs-lookup"><span data-stu-id="4d3e1-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="4d3e1-105">Prostředku používaného pro zadávání dotazů automatického dokončování je `SearchAutocompleteService` v nalezen prostředek [indexu služby](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="4d3e1-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="4d3e1-106">Správa verzí</span><span class="sxs-lookup"><span data-stu-id="4d3e1-106">Versioning</span></span>

<span data-ttu-id="4d3e1-107">Následující `@type` se používají hodnoty:</span><span class="sxs-lookup"><span data-stu-id="4d3e1-107">The following `@type` values are used:</span></span>

<span data-ttu-id="4d3e1-108">@type Hodnota</span><span class="sxs-lookup"><span data-stu-id="4d3e1-108">@type value</span></span>                          | <span data-ttu-id="4d3e1-109">Poznámky</span><span class="sxs-lookup"><span data-stu-id="4d3e1-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="4d3e1-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="4d3e1-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="4d3e1-111">Původní verze</span><span class="sxs-lookup"><span data-stu-id="4d3e1-111">The initial release</span></span>
<span data-ttu-id="4d3e1-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="4d3e1-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="4d3e1-113">Alias `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="4d3e1-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="4d3e1-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="4d3e1-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="4d3e1-115">Alias `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="4d3e1-115">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="4d3e1-116">Základní adresu URL</span><span class="sxs-lookup"><span data-stu-id="4d3e1-116">Base URL</span></span>

<span data-ttu-id="4d3e1-117">Základní adresu URL pro následující rozhraní API je hodnota `@id` vlastnost spojená s jedním z výše uvedených prostředků `@type` hodnoty.</span><span class="sxs-lookup"><span data-stu-id="4d3e1-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="4d3e1-118">V následujícím dokumentu zástupného textu základní adresa URL `{@id}` se použije.</span><span class="sxs-lookup"><span data-stu-id="4d3e1-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="4d3e1-119">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="4d3e1-119">HTTP Methods</span></span>

<span data-ttu-id="4d3e1-120">Všechny adresy URL v podpory registrace prostředků nalezen metody HTTP `GET` a `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="4d3e1-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="4d3e1-121">Vyhledávání pro balíček ID</span><span class="sxs-lookup"><span data-stu-id="4d3e1-121">Search for package IDs</span></span>

<span data-ttu-id="4d3e1-122">První autocomplete rozhraní API podporuje hledání část řetězce ID balíčku.</span><span class="sxs-lookup"><span data-stu-id="4d3e1-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="4d3e1-123">To je skvělé, pokud chcete poskytovat funkce typeahead balíčku v uživatelském rozhraní integrovat zdroje balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="4d3e1-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="4d3e1-124">Balíček se pouze neuvedené verzí se nezobrazí ve výsledcích.</span><span class="sxs-lookup"><span data-stu-id="4d3e1-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="4d3e1-125">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="4d3e1-125">Request parameters</span></span>

<span data-ttu-id="4d3e1-126">Název</span><span class="sxs-lookup"><span data-stu-id="4d3e1-126">Name</span></span>        | <span data-ttu-id="4d3e1-127">V</span><span class="sxs-lookup"><span data-stu-id="4d3e1-127">In</span></span>     | <span data-ttu-id="4d3e1-128">Typ</span><span class="sxs-lookup"><span data-stu-id="4d3e1-128">Type</span></span>    | <span data-ttu-id="4d3e1-129">Požadováno</span><span class="sxs-lookup"><span data-stu-id="4d3e1-129">Required</span></span> | <span data-ttu-id="4d3e1-130">Poznámky</span><span class="sxs-lookup"><span data-stu-id="4d3e1-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="4d3e1-131">q</span><span class="sxs-lookup"><span data-stu-id="4d3e1-131">q</span></span>           | <span data-ttu-id="4d3e1-132">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="4d3e1-132">URL</span></span>    | <span data-ttu-id="4d3e1-133">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="4d3e1-133">string</span></span>  | <span data-ttu-id="4d3e1-134">Ne</span><span class="sxs-lookup"><span data-stu-id="4d3e1-134">no</span></span>       | <span data-ttu-id="4d3e1-135">Řetězec, který má být porovnán balíček ID</span><span class="sxs-lookup"><span data-stu-id="4d3e1-135">The string to compare against package IDs</span></span>
<span data-ttu-id="4d3e1-136">Přeskočit</span><span class="sxs-lookup"><span data-stu-id="4d3e1-136">skip</span></span>        | <span data-ttu-id="4d3e1-137">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="4d3e1-137">URL</span></span>    | <span data-ttu-id="4d3e1-138">integer</span><span class="sxs-lookup"><span data-stu-id="4d3e1-138">integer</span></span> | <span data-ttu-id="4d3e1-139">Ne</span><span class="sxs-lookup"><span data-stu-id="4d3e1-139">no</span></span>       | <span data-ttu-id="4d3e1-140">Počet výsledků tak, aby přeskočil pro stránkování</span><span class="sxs-lookup"><span data-stu-id="4d3e1-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="4d3e1-141">proveďte</span><span class="sxs-lookup"><span data-stu-id="4d3e1-141">take</span></span>        | <span data-ttu-id="4d3e1-142">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="4d3e1-142">URL</span></span>    | <span data-ttu-id="4d3e1-143">integer</span><span class="sxs-lookup"><span data-stu-id="4d3e1-143">integer</span></span> | <span data-ttu-id="4d3e1-144">Ne</span><span class="sxs-lookup"><span data-stu-id="4d3e1-144">no</span></span>       | <span data-ttu-id="4d3e1-145">Počet výsledků, které má být vrácen pro stránkování</span><span class="sxs-lookup"><span data-stu-id="4d3e1-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="4d3e1-146">předběžné verze</span><span class="sxs-lookup"><span data-stu-id="4d3e1-146">prerelease</span></span>  | <span data-ttu-id="4d3e1-147">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="4d3e1-147">URL</span></span>    | <span data-ttu-id="4d3e1-148">Logická hodnota</span><span class="sxs-lookup"><span data-stu-id="4d3e1-148">boolean</span></span> | <span data-ttu-id="4d3e1-149">Ne</span><span class="sxs-lookup"><span data-stu-id="4d3e1-149">no</span></span>       | <span data-ttu-id="4d3e1-150">`true` nebo `false` určení, jestli se mají zahrnout [předběžné verze balíčků](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="4d3e1-150">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="4d3e1-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="4d3e1-151">semVerLevel</span></span> | <span data-ttu-id="4d3e1-152">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="4d3e1-152">URL</span></span>    | <span data-ttu-id="4d3e1-153">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="4d3e1-153">string</span></span>  | <span data-ttu-id="4d3e1-154">Ne</span><span class="sxs-lookup"><span data-stu-id="4d3e1-154">no</span></span>       | <span data-ttu-id="4d3e1-155">Řetězec verze o SemVer 1.0.0</span><span class="sxs-lookup"><span data-stu-id="4d3e1-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="4d3e1-156">Automatické dokončování dotazů `q` je analyzována způsobem, který je definován implementaci serveru.</span><span class="sxs-lookup"><span data-stu-id="4d3e1-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="4d3e1-157">nuget.org podporuje dotazování pro předponu tokenů ID balíčku, které jsou částí ID vyprodukované spliting původní formátu camelCase případ a symbol znaky.</span><span class="sxs-lookup"><span data-stu-id="4d3e1-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="4d3e1-158">`skip` Výchozí hodnoty parametrů na hodnotu 0.</span><span class="sxs-lookup"><span data-stu-id="4d3e1-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="4d3e1-159">`take` Parametr by měl být celé číslo větší než nula.</span><span class="sxs-lookup"><span data-stu-id="4d3e1-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="4d3e1-160">Implementaci serveru může uložit maximální hodnotu.</span><span class="sxs-lookup"><span data-stu-id="4d3e1-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="4d3e1-161">Pokud `prerelease` není zadána, jsou vyloučeny předběžné verze balíčků.</span><span class="sxs-lookup"><span data-stu-id="4d3e1-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="4d3e1-162">`semVerLevel` Parametr dotazu se používá k vyslovení souhlasu s [SemVer 2.0.0 balíčky](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span><span class="sxs-lookup"><span data-stu-id="4d3e1-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="4d3e1-163">Pokud tento parametr dotazu je vyloučená, bude vrácen pouze balíček ID s kompatibilní verze SemVer 1.0.0 (s [standardní verze NuGet](../reference/package-versioning.md) upozornění, jako jsou třeba řetězce verze se 4 kusy celé číslo).</span><span class="sxs-lookup"><span data-stu-id="4d3e1-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="4d3e1-164">Pokud `semVerLevel=2.0.0` je zadáno, bude vrácen SemVer 1.0.0 a SemVer 2.0.0 kompatibilní balíčky.</span><span class="sxs-lookup"><span data-stu-id="4d3e1-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="4d3e1-165">Najdete v článku [SemVer 2.0.0 podpora nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) Další informace.</span><span class="sxs-lookup"><span data-stu-id="4d3e1-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="4d3e1-166">Odpověď</span><span class="sxs-lookup"><span data-stu-id="4d3e1-166">Response</span></span>

<span data-ttu-id="4d3e1-167">Odpovědí je dokument JSON obsahující až `take` výsledky funkce automatického dokončování.</span><span class="sxs-lookup"><span data-stu-id="4d3e1-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="4d3e1-168">Kořenový objekt JSON má následující vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="4d3e1-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="4d3e1-169">Název</span><span class="sxs-lookup"><span data-stu-id="4d3e1-169">Name</span></span>      | <span data-ttu-id="4d3e1-170">Typ</span><span class="sxs-lookup"><span data-stu-id="4d3e1-170">Type</span></span>             | <span data-ttu-id="4d3e1-171">Požadováno</span><span class="sxs-lookup"><span data-stu-id="4d3e1-171">Required</span></span> | <span data-ttu-id="4d3e1-172">Poznámky</span><span class="sxs-lookup"><span data-stu-id="4d3e1-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="4d3e1-173">totalHits</span><span class="sxs-lookup"><span data-stu-id="4d3e1-173">totalHits</span></span> | <span data-ttu-id="4d3e1-174">integer</span><span class="sxs-lookup"><span data-stu-id="4d3e1-174">integer</span></span>          | <span data-ttu-id="4d3e1-175">Ano</span><span class="sxs-lookup"><span data-stu-id="4d3e1-175">yes</span></span>      | <span data-ttu-id="4d3e1-176">Celkový počet shod, bez ohledu na `skip` a `take`</span><span class="sxs-lookup"><span data-stu-id="4d3e1-176">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="4d3e1-177">data</span><span class="sxs-lookup"><span data-stu-id="4d3e1-177">data</span></span>      | <span data-ttu-id="4d3e1-178">Pole řetězců.</span><span class="sxs-lookup"><span data-stu-id="4d3e1-178">array of strings</span></span> | <span data-ttu-id="4d3e1-179">Ano</span><span class="sxs-lookup"><span data-stu-id="4d3e1-179">yes</span></span>      | <span data-ttu-id="4d3e1-180">ID balíčku odpovídala požadavku</span><span class="sxs-lookup"><span data-stu-id="4d3e1-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="4d3e1-181">Ukázková žádost</span><span class="sxs-lookup"><span data-stu-id="4d3e1-181">Sample request</span></span>

<span data-ttu-id="4d3e1-182">GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span><span class="sxs-lookup"><span data-stu-id="4d3e1-182">GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span></span>

### <a name="sample-response"></a><span data-ttu-id="4d3e1-183">Ukázková odpověď</span><span class="sxs-lookup"><span data-stu-id="4d3e1-183">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="4d3e1-184">Zobrazení výčtu verze balíčku</span><span class="sxs-lookup"><span data-stu-id="4d3e1-184">Enumerate package versions</span></span>

<span data-ttu-id="4d3e1-185">Po zjištění ID balíčku pomocí předchozího rozhraní API může klient používat automatické dokončování rozhraní API se vytvořit výčet verze balíčku pro ID zadaný balíček.</span><span class="sxs-lookup"><span data-stu-id="4d3e1-185">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="4d3e1-186">Verze balíčku, který neuvedené nezobrazí ve výsledcích.</span><span class="sxs-lookup"><span data-stu-id="4d3e1-186">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="4d3e1-187">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="4d3e1-187">Request parameters</span></span>

<span data-ttu-id="4d3e1-188">Název</span><span class="sxs-lookup"><span data-stu-id="4d3e1-188">Name</span></span>        | <span data-ttu-id="4d3e1-189">V</span><span class="sxs-lookup"><span data-stu-id="4d3e1-189">In</span></span>     | <span data-ttu-id="4d3e1-190">Typ</span><span class="sxs-lookup"><span data-stu-id="4d3e1-190">Type</span></span>    | <span data-ttu-id="4d3e1-191">Požadováno</span><span class="sxs-lookup"><span data-stu-id="4d3e1-191">Required</span></span> | <span data-ttu-id="4d3e1-192">Poznámky</span><span class="sxs-lookup"><span data-stu-id="4d3e1-192">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="4d3e1-193">id</span><span class="sxs-lookup"><span data-stu-id="4d3e1-193">id</span></span>          | <span data-ttu-id="4d3e1-194">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="4d3e1-194">URL</span></span>    | <span data-ttu-id="4d3e1-195">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="4d3e1-195">string</span></span>  | <span data-ttu-id="4d3e1-196">Ano</span><span class="sxs-lookup"><span data-stu-id="4d3e1-196">yes</span></span>      | <span data-ttu-id="4d3e1-197">ID balíčku se načíst verze pro</span><span class="sxs-lookup"><span data-stu-id="4d3e1-197">The package ID to fetch versions for</span></span>
<span data-ttu-id="4d3e1-198">předběžné verze</span><span class="sxs-lookup"><span data-stu-id="4d3e1-198">prerelease</span></span>  | <span data-ttu-id="4d3e1-199">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="4d3e1-199">URL</span></span>    | <span data-ttu-id="4d3e1-200">Logická hodnota</span><span class="sxs-lookup"><span data-stu-id="4d3e1-200">boolean</span></span> | <span data-ttu-id="4d3e1-201">Ne</span><span class="sxs-lookup"><span data-stu-id="4d3e1-201">no</span></span>       | <span data-ttu-id="4d3e1-202">`true` nebo `false` určení, jestli se mají zahrnout [předběžné verze balíčků](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="4d3e1-202">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="4d3e1-203">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="4d3e1-203">semVerLevel</span></span> | <span data-ttu-id="4d3e1-204">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="4d3e1-204">URL</span></span>    | <span data-ttu-id="4d3e1-205">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="4d3e1-205">string</span></span>  | <span data-ttu-id="4d3e1-206">Ne</span><span class="sxs-lookup"><span data-stu-id="4d3e1-206">no</span></span>       | <span data-ttu-id="4d3e1-207">Řetězec verze o SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="4d3e1-207">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="4d3e1-208">Pokud `prerelease` není zadána, jsou vyloučeny předběžné verze balíčků.</span><span class="sxs-lookup"><span data-stu-id="4d3e1-208">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="4d3e1-209">`semVerLevel` Parametr dotazu se používá k vyslovení souhlasu s SemVer 2.0.0 balíčky.</span><span class="sxs-lookup"><span data-stu-id="4d3e1-209">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="4d3e1-210">Pokud tento parametr dotazu je vyloučená, bude vrácen pouze SemVer 1.0.0 verze.</span><span class="sxs-lookup"><span data-stu-id="4d3e1-210">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="4d3e1-211">Pokud `semVerLevel=2.0.0` je zadáno, bude vrácen SemVer 1.0.0 a SemVer 2.0.0 verze.</span><span class="sxs-lookup"><span data-stu-id="4d3e1-211">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="4d3e1-212">Najdete v článku [SemVer 2.0.0 podpora nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) Další informace.</span><span class="sxs-lookup"><span data-stu-id="4d3e1-212">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="4d3e1-213">Odpověď</span><span class="sxs-lookup"><span data-stu-id="4d3e1-213">Response</span></span>

<span data-ttu-id="4d3e1-214">Odpověď je dokument JSON obsahující všechny verze balíčku zadaný balíček ID, filtrování podle parametrů daný dotaz.</span><span class="sxs-lookup"><span data-stu-id="4d3e1-214">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="4d3e1-215">Kořenový objekt JSON má následující vlastnost:</span><span class="sxs-lookup"><span data-stu-id="4d3e1-215">The root JSON object has the following property:</span></span>

<span data-ttu-id="4d3e1-216">Název</span><span class="sxs-lookup"><span data-stu-id="4d3e1-216">Name</span></span>      | <span data-ttu-id="4d3e1-217">Typ</span><span class="sxs-lookup"><span data-stu-id="4d3e1-217">Type</span></span>             | <span data-ttu-id="4d3e1-218">Požadováno</span><span class="sxs-lookup"><span data-stu-id="4d3e1-218">Required</span></span> | <span data-ttu-id="4d3e1-219">Poznámky</span><span class="sxs-lookup"><span data-stu-id="4d3e1-219">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="4d3e1-220">data</span><span class="sxs-lookup"><span data-stu-id="4d3e1-220">data</span></span>      | <span data-ttu-id="4d3e1-221">Pole řetězců.</span><span class="sxs-lookup"><span data-stu-id="4d3e1-221">array of strings</span></span> | <span data-ttu-id="4d3e1-222">Ano</span><span class="sxs-lookup"><span data-stu-id="4d3e1-222">yes</span></span>      | <span data-ttu-id="4d3e1-223">Verze balíčku odpovídala požadavku</span><span class="sxs-lookup"><span data-stu-id="4d3e1-223">The package versions matched by the request</span></span>

<span data-ttu-id="4d3e1-224">Verze v balíčku `data` pole může obsahovat metadata sestavení SemVer 2.0.0 (například `1.0.0+metadata`) Pokud `semVerLevel=2.0.0` zadaná v řetězci dotazu.</span><span class="sxs-lookup"><span data-stu-id="4d3e1-224">The package versions in the `data` array could contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` was provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="4d3e1-225">Ukázková žádost</span><span class="sxs-lookup"><span data-stu-id="4d3e1-225">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="4d3e1-226">Ukázková odpověď</span><span class="sxs-lookup"><span data-stu-id="4d3e1-226">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
