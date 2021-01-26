---
title: Automatické dokončování, rozhraní API NuGet
description: Služba Automatické dokončování hledání podporuje interaktivní zjišťování ID a verzí balíčků.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 2893e13ff7b070844a2bdd5722da3aa1f123538d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773964"
---
# <a name="autocomplete"></a><span data-ttu-id="d2de6-103">Automatické dokončování</span><span class="sxs-lookup"><span data-stu-id="d2de6-103">Autocomplete</span></span>

<span data-ttu-id="d2de6-104">Pomocí rozhraní V3 API je možné vytvořit ID balíčku a verzi prostředí pro automatické dokončování.</span><span class="sxs-lookup"><span data-stu-id="d2de6-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="d2de6-105">Prostředek, který se používá k provedení dotazů automatického dokončování, je prostředek, který se `SearchAutocompleteService` nachází v [indexu služby](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="d2de6-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="d2de6-106">Správa verzí</span><span class="sxs-lookup"><span data-stu-id="d2de6-106">Versioning</span></span>

<span data-ttu-id="d2de6-107">Použijí se tyto `@type` hodnoty:</span><span class="sxs-lookup"><span data-stu-id="d2de6-107">The following `@type` values are used:</span></span>

<span data-ttu-id="d2de6-108">@type osa</span><span class="sxs-lookup"><span data-stu-id="d2de6-108">@type value</span></span>                          | <span data-ttu-id="d2de6-109">Poznámky</span><span class="sxs-lookup"><span data-stu-id="d2de6-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="d2de6-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="d2de6-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="d2de6-111">Počáteční verze</span><span class="sxs-lookup"><span data-stu-id="d2de6-111">The initial release</span></span>
<span data-ttu-id="d2de6-112">SearchAutocompleteService/3.0.0 – beta</span><span class="sxs-lookup"><span data-stu-id="d2de6-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="d2de6-113">Alias pro `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="d2de6-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="d2de6-114">SearchAutocompleteService/3.0.0 – RC</span><span class="sxs-lookup"><span data-stu-id="d2de6-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="d2de6-115">Alias pro `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="d2de6-115">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="d2de6-116">SearchAutocompleteService/3.5.0</span><span class="sxs-lookup"><span data-stu-id="d2de6-116">SearchAutocompleteService/3.5.0</span></span>      | <span data-ttu-id="d2de6-117">Zahrnuje podporu pro `packageType` parametr dotazu.</span><span class="sxs-lookup"><span data-stu-id="d2de6-117">Includes support for `packageType` query parameter</span></span>

### <a name="searchautocompleteservice350"></a><span data-ttu-id="d2de6-118">SearchAutocompleteService/3.5.0</span><span class="sxs-lookup"><span data-stu-id="d2de6-118">SearchAutocompleteService/3.5.0</span></span>
<span data-ttu-id="d2de6-119">Tato verze zavádí podporu `packageType` parametru dotazu, který umožňuje filtrování podle typu balíčků definovaných autory.</span><span class="sxs-lookup"><span data-stu-id="d2de6-119">This version introduces support for the `packageType` query parameter, allowing filtering by author defined package types.</span></span> <span data-ttu-id="d2de6-120">Je plně zpětně kompatibilní s dotazy na `SearchAutocompleteService` .</span><span class="sxs-lookup"><span data-stu-id="d2de6-120">It is fully backwards compatible with queries to `SearchAutocompleteService`.</span></span>

## <a name="base-url"></a><span data-ttu-id="d2de6-121">Základní adresa URL</span><span class="sxs-lookup"><span data-stu-id="d2de6-121">Base URL</span></span>

<span data-ttu-id="d2de6-122">Základní adresa URL následujících rozhraní API je hodnota `@id` vlastnosti přidružené k jedné z výše uvedených `@type` hodnot prostředků.</span><span class="sxs-lookup"><span data-stu-id="d2de6-122">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="d2de6-123">V následujícím dokumentu se použije zástupná základní adresa URL `{@id}` .</span><span class="sxs-lookup"><span data-stu-id="d2de6-123">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="d2de6-124">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="d2de6-124">HTTP Methods</span></span>

<span data-ttu-id="d2de6-125">Všechny adresy URL nalezené v registračním prostředku podporují metody HTTP `GET` a `HEAD` .</span><span class="sxs-lookup"><span data-stu-id="d2de6-125">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="d2de6-126">Vyhledat ID balíčků</span><span class="sxs-lookup"><span data-stu-id="d2de6-126">Search for package IDs</span></span>

<span data-ttu-id="d2de6-127">První rozhraní API pro automatické dokončování podporuje hledání částí řetězce ID balíčku.</span><span class="sxs-lookup"><span data-stu-id="d2de6-127">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="d2de6-128">To je skvělé, když chcete poskytnout funkci balíčku typeahead v uživatelském rozhraní integrovaném se zdrojem balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="d2de6-128">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="d2de6-129">Ve výsledcích se nezobrazí balíček s pouze neuvedenými verzemi.</span><span class="sxs-lookup"><span data-stu-id="d2de6-129">A package with only unlisted versions will not appear in the results.</span></span>

```
GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}&packageType={PACKAGETYPE}
```

### <a name="request-parameters"></a><span data-ttu-id="d2de6-130">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="d2de6-130">Request parameters</span></span>

<span data-ttu-id="d2de6-131">Name</span><span class="sxs-lookup"><span data-stu-id="d2de6-131">Name</span></span>        | <span data-ttu-id="d2de6-132">V</span><span class="sxs-lookup"><span data-stu-id="d2de6-132">In</span></span>     | <span data-ttu-id="d2de6-133">Typ</span><span class="sxs-lookup"><span data-stu-id="d2de6-133">Type</span></span>    | <span data-ttu-id="d2de6-134">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="d2de6-134">Required</span></span> | <span data-ttu-id="d2de6-135">Poznámky</span><span class="sxs-lookup"><span data-stu-id="d2de6-135">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="d2de6-136">q</span><span class="sxs-lookup"><span data-stu-id="d2de6-136">q</span></span>           | <span data-ttu-id="d2de6-137">URL</span><span class="sxs-lookup"><span data-stu-id="d2de6-137">URL</span></span>    | <span data-ttu-id="d2de6-138">řetězec</span><span class="sxs-lookup"><span data-stu-id="d2de6-138">string</span></span>  | <span data-ttu-id="d2de6-139">ne</span><span class="sxs-lookup"><span data-stu-id="d2de6-139">no</span></span>       | <span data-ttu-id="d2de6-140">Řetězec, který se má porovnat s ID balíčků</span><span class="sxs-lookup"><span data-stu-id="d2de6-140">The string to compare against package IDs</span></span>
<span data-ttu-id="d2de6-141">Přeskočit</span><span class="sxs-lookup"><span data-stu-id="d2de6-141">skip</span></span>        | <span data-ttu-id="d2de6-142">URL</span><span class="sxs-lookup"><span data-stu-id="d2de6-142">URL</span></span>    | <span data-ttu-id="d2de6-143">integer</span><span class="sxs-lookup"><span data-stu-id="d2de6-143">integer</span></span> | <span data-ttu-id="d2de6-144">ne</span><span class="sxs-lookup"><span data-stu-id="d2de6-144">no</span></span>       | <span data-ttu-id="d2de6-145">Počet výsledků, které se mají přeskočit, pro stránkování</span><span class="sxs-lookup"><span data-stu-id="d2de6-145">The number of results to skip, for pagination</span></span>
<span data-ttu-id="d2de6-146">take</span><span class="sxs-lookup"><span data-stu-id="d2de6-146">take</span></span>        | <span data-ttu-id="d2de6-147">URL</span><span class="sxs-lookup"><span data-stu-id="d2de6-147">URL</span></span>    | <span data-ttu-id="d2de6-148">integer</span><span class="sxs-lookup"><span data-stu-id="d2de6-148">integer</span></span> | <span data-ttu-id="d2de6-149">ne</span><span class="sxs-lookup"><span data-stu-id="d2de6-149">no</span></span>       | <span data-ttu-id="d2de6-150">Počet výsledků, které se mají vrátit, pro stránkování</span><span class="sxs-lookup"><span data-stu-id="d2de6-150">The number of results to return, for pagination</span></span>
<span data-ttu-id="d2de6-151">předběžné verze</span><span class="sxs-lookup"><span data-stu-id="d2de6-151">prerelease</span></span>  | <span data-ttu-id="d2de6-152">URL</span><span class="sxs-lookup"><span data-stu-id="d2de6-152">URL</span></span>    | <span data-ttu-id="d2de6-153">boolean</span><span class="sxs-lookup"><span data-stu-id="d2de6-153">boolean</span></span> | <span data-ttu-id="d2de6-154">ne</span><span class="sxs-lookup"><span data-stu-id="d2de6-154">no</span></span>       | <span data-ttu-id="d2de6-155">`true` nebo `false` Určete, jestli se mají zahrnout [předběžné verze balíčků](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="d2de6-155">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="d2de6-156">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="d2de6-156">semVerLevel</span></span> | <span data-ttu-id="d2de6-157">URL</span><span class="sxs-lookup"><span data-stu-id="d2de6-157">URL</span></span>    | <span data-ttu-id="d2de6-158">řetězec</span><span class="sxs-lookup"><span data-stu-id="d2de6-158">string</span></span>  | <span data-ttu-id="d2de6-159">ne</span><span class="sxs-lookup"><span data-stu-id="d2de6-159">no</span></span>       | <span data-ttu-id="d2de6-160">Řetězec verze SemVer 1.0.0</span><span class="sxs-lookup"><span data-stu-id="d2de6-160">A SemVer 1.0.0 version string</span></span> 
<span data-ttu-id="d2de6-161">packageType</span><span class="sxs-lookup"><span data-stu-id="d2de6-161">packageType</span></span> | <span data-ttu-id="d2de6-162">URL</span><span class="sxs-lookup"><span data-stu-id="d2de6-162">URL</span></span>    | <span data-ttu-id="d2de6-163">řetězec</span><span class="sxs-lookup"><span data-stu-id="d2de6-163">string</span></span>  | <span data-ttu-id="d2de6-164">ne</span><span class="sxs-lookup"><span data-stu-id="d2de6-164">no</span></span>       | <span data-ttu-id="d2de6-165">Typ balíčku, který se má použít k filtrování balíčků (přidaných v `SearchAutocompleteService/3.5.0` )</span><span class="sxs-lookup"><span data-stu-id="d2de6-165">The package type to use to filter packages (added in `SearchAutocompleteService/3.5.0`)</span></span>

<span data-ttu-id="d2de6-166">Dotaz na automatické dokončování `q` je analyzován způsobem, který je definován implementací serveru.</span><span class="sxs-lookup"><span data-stu-id="d2de6-166">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="d2de6-167">nuget.org podporuje dotazování na předponu tokenů ID balíčku, které jsou částmi ID vytvořenými rozdělením originálu pomocí znaků písmen a symbolů ve stylu CamelCase.</span><span class="sxs-lookup"><span data-stu-id="d2de6-167">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="d2de6-168">`skip`Parametr má výchozí hodnotu 0.</span><span class="sxs-lookup"><span data-stu-id="d2de6-168">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="d2de6-169">`take`Parametr by měl být celé číslo větší než nula.</span><span class="sxs-lookup"><span data-stu-id="d2de6-169">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="d2de6-170">Implementace serveru může poskytovat maximální hodnotu.</span><span class="sxs-lookup"><span data-stu-id="d2de6-170">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="d2de6-171">Pokud není `prerelease` zadaný, vyloučí se balíčky předběžných verzí.</span><span class="sxs-lookup"><span data-stu-id="d2de6-171">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="d2de6-172">`semVerLevel`Parametr dotazu se používá pro výslovný souhlas s [SemVer balíčky 2.0.0](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span><span class="sxs-lookup"><span data-stu-id="d2de6-172">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="d2de6-173">Pokud je tento parametr dotazu vyloučený, vrátí se jenom ID balíčků se kompatibilními verzemi SemVer 1.0.0 (se [standardními omezeními verzí NuGet](../concepts/package-versioning.md) , jako jsou například řetězce verze se 4 celými čísly).</span><span class="sxs-lookup"><span data-stu-id="d2de6-173">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../concepts/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="d2de6-174">Pokud `semVerLevel=2.0.0` je k dispozici, budou vráceny balíčky kompatibilní s SemVer 1.0.0 a SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="d2de6-174">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="d2de6-175">Další informace najdete v tématu [Podpora SemVer 2.0.0 pro NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .</span><span class="sxs-lookup"><span data-stu-id="d2de6-175">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

<span data-ttu-id="d2de6-176">`packageType`Parametr se používá k dalšímu filtrování výsledků automatického dokončování do pouze balíčků, které mají alespoň jeden typ balíčku, který odpovídá názvu typu balíčku.</span><span class="sxs-lookup"><span data-stu-id="d2de6-176">The `packageType` parameter is used to further filter the autocomplete results to only packages that have at least one package type matching the package type name.</span></span>
<span data-ttu-id="d2de6-177">Pokud zadaný typ balíčku není platný typ balíčku definovaný [dokumentem typu balíčku](https://github.com/NuGet/Home/wiki/Package-Type-%5BPacking%5D), vrátí se prázdný výsledek.</span><span class="sxs-lookup"><span data-stu-id="d2de6-177">If the provided package type is not a valid package type as defined by the [Package Type document](https://github.com/NuGet/Home/wiki/Package-Type-%5BPacking%5D), an empty result will returned.</span></span>
<span data-ttu-id="d2de6-178">Pokud je zadaný typ balíčku prázdný, nebude použit žádný filtr.</span><span class="sxs-lookup"><span data-stu-id="d2de6-178">If the provided package type is empty, no filter will be applied.</span></span> <span data-ttu-id="d2de6-179">Jinými slovy, nepředání hodnoty do `packageType` parametru se bude chovat, jako by nebyl předán parametr.</span><span class="sxs-lookup"><span data-stu-id="d2de6-179">In other words, passing no value to the `packageType` parameter will behave as if the parameter was not passed.</span></span>

### <a name="response"></a><span data-ttu-id="d2de6-180">Odpověď</span><span class="sxs-lookup"><span data-stu-id="d2de6-180">Response</span></span>

<span data-ttu-id="d2de6-181">Odpověď je dokument JSON, který obsahuje `take` Výsledky automatického dokončování.</span><span class="sxs-lookup"><span data-stu-id="d2de6-181">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="d2de6-182">Kořenový objekt JSON má následující vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="d2de6-182">The root JSON object has the following properties:</span></span>

<span data-ttu-id="d2de6-183">Název</span><span class="sxs-lookup"><span data-stu-id="d2de6-183">Name</span></span>      | <span data-ttu-id="d2de6-184">Typ</span><span class="sxs-lookup"><span data-stu-id="d2de6-184">Type</span></span>             | <span data-ttu-id="d2de6-185">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="d2de6-185">Required</span></span> | <span data-ttu-id="d2de6-186">Poznámky</span><span class="sxs-lookup"><span data-stu-id="d2de6-186">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="d2de6-187">totalHits</span><span class="sxs-lookup"><span data-stu-id="d2de6-187">totalHits</span></span> | <span data-ttu-id="d2de6-188">integer</span><span class="sxs-lookup"><span data-stu-id="d2de6-188">integer</span></span>          | <span data-ttu-id="d2de6-189">ano</span><span class="sxs-lookup"><span data-stu-id="d2de6-189">yes</span></span>      | <span data-ttu-id="d2de6-190">Celkový počet shod, nesouvisející `skip` a `take`</span><span class="sxs-lookup"><span data-stu-id="d2de6-190">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="d2de6-191">data</span><span class="sxs-lookup"><span data-stu-id="d2de6-191">data</span></span>      | <span data-ttu-id="d2de6-192">pole řetězců</span><span class="sxs-lookup"><span data-stu-id="d2de6-192">array of strings</span></span> | <span data-ttu-id="d2de6-193">ano</span><span class="sxs-lookup"><span data-stu-id="d2de6-193">yes</span></span>      | <span data-ttu-id="d2de6-194">ID balíčků, které odpovídá požadavek</span><span class="sxs-lookup"><span data-stu-id="d2de6-194">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="d2de6-195">Ukázková žádost</span><span class="sxs-lookup"><span data-stu-id="d2de6-195">Sample request</span></span>

```
GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true
```

### <a name="sample-response"></a><span data-ttu-id="d2de6-196">Ukázková odpověď</span><span class="sxs-lookup"><span data-stu-id="d2de6-196">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="d2de6-197">Zobrazení výčtu verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="d2de6-197">Enumerate package versions</span></span>

<span data-ttu-id="d2de6-198">Po zjištění ID balíčku pomocí předchozího rozhraní API může klient použít rozhraní API pro automatické dokončování k zobrazení výčtu verzí balíčků pro zadané ID balíčku.</span><span class="sxs-lookup"><span data-stu-id="d2de6-198">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="d2de6-199">Ve výsledcích se nezobrazí verze balíčku, který není uveden v seznamu.</span><span class="sxs-lookup"><span data-stu-id="d2de6-199">A package version that is unlisted will not appear in the results.</span></span>

```
GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}
```

### <a name="request-parameters"></a><span data-ttu-id="d2de6-200">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="d2de6-200">Request parameters</span></span>

<span data-ttu-id="d2de6-201">Name</span><span class="sxs-lookup"><span data-stu-id="d2de6-201">Name</span></span>        | <span data-ttu-id="d2de6-202">V</span><span class="sxs-lookup"><span data-stu-id="d2de6-202">In</span></span>     | <span data-ttu-id="d2de6-203">Typ</span><span class="sxs-lookup"><span data-stu-id="d2de6-203">Type</span></span>    | <span data-ttu-id="d2de6-204">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="d2de6-204">Required</span></span> | <span data-ttu-id="d2de6-205">Poznámky</span><span class="sxs-lookup"><span data-stu-id="d2de6-205">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="d2de6-206">id</span><span class="sxs-lookup"><span data-stu-id="d2de6-206">id</span></span>          | <span data-ttu-id="d2de6-207">URL</span><span class="sxs-lookup"><span data-stu-id="d2de6-207">URL</span></span>    | <span data-ttu-id="d2de6-208">řetězec</span><span class="sxs-lookup"><span data-stu-id="d2de6-208">string</span></span>  | <span data-ttu-id="d2de6-209">ano</span><span class="sxs-lookup"><span data-stu-id="d2de6-209">yes</span></span>      | <span data-ttu-id="d2de6-210">ID balíčku, pro který se mají načíst verze</span><span class="sxs-lookup"><span data-stu-id="d2de6-210">The package ID to fetch versions for</span></span>
<span data-ttu-id="d2de6-211">předběžné verze</span><span class="sxs-lookup"><span data-stu-id="d2de6-211">prerelease</span></span>  | <span data-ttu-id="d2de6-212">URL</span><span class="sxs-lookup"><span data-stu-id="d2de6-212">URL</span></span>    | <span data-ttu-id="d2de6-213">boolean</span><span class="sxs-lookup"><span data-stu-id="d2de6-213">boolean</span></span> | <span data-ttu-id="d2de6-214">ne</span><span class="sxs-lookup"><span data-stu-id="d2de6-214">no</span></span>       | <span data-ttu-id="d2de6-215">`true` nebo `false` Určete, jestli se mají zahrnout [předběžné verze balíčků](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="d2de6-215">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="d2de6-216">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="d2de6-216">semVerLevel</span></span> | <span data-ttu-id="d2de6-217">URL</span><span class="sxs-lookup"><span data-stu-id="d2de6-217">URL</span></span>    | <span data-ttu-id="d2de6-218">řetězec</span><span class="sxs-lookup"><span data-stu-id="d2de6-218">string</span></span>  | <span data-ttu-id="d2de6-219">ne</span><span class="sxs-lookup"><span data-stu-id="d2de6-219">no</span></span>       | <span data-ttu-id="d2de6-220">Řetězec verze SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="d2de6-220">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="d2de6-221">Pokud není `prerelease` zadaný, vyloučí se balíčky předběžných verzí.</span><span class="sxs-lookup"><span data-stu-id="d2de6-221">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="d2de6-222">`semVerLevel`Parametr dotazu se používá pro výslovný souhlas s SemVer balíčky 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="d2de6-222">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="d2de6-223">Pokud je tento parametr dotazu vyloučený, vrátí se pouze verze SemVer 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="d2de6-223">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="d2de6-224">Pokud `semVerLevel=2.0.0` je k dispozici, vrátí se obě verze SemVer 1.0.0 a SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="d2de6-224">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="d2de6-225">Další informace najdete v tématu [Podpora SemVer 2.0.0 pro NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .</span><span class="sxs-lookup"><span data-stu-id="d2de6-225">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="d2de6-226">Odpověď</span><span class="sxs-lookup"><span data-stu-id="d2de6-226">Response</span></span>

<span data-ttu-id="d2de6-227">Odpověď je dokument JSON obsahující všechny verze balíčků zadaného ID balíčku, které filtrují podle daných parametrů dotazu.</span><span class="sxs-lookup"><span data-stu-id="d2de6-227">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="d2de6-228">Kořenový objekt JSON má následující vlastnost:</span><span class="sxs-lookup"><span data-stu-id="d2de6-228">The root JSON object has the following property:</span></span>

<span data-ttu-id="d2de6-229">Název</span><span class="sxs-lookup"><span data-stu-id="d2de6-229">Name</span></span>      | <span data-ttu-id="d2de6-230">Typ</span><span class="sxs-lookup"><span data-stu-id="d2de6-230">Type</span></span>             | <span data-ttu-id="d2de6-231">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="d2de6-231">Required</span></span> | <span data-ttu-id="d2de6-232">Poznámky</span><span class="sxs-lookup"><span data-stu-id="d2de6-232">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="d2de6-233">data</span><span class="sxs-lookup"><span data-stu-id="d2de6-233">data</span></span>      | <span data-ttu-id="d2de6-234">pole řetězců</span><span class="sxs-lookup"><span data-stu-id="d2de6-234">array of strings</span></span> | <span data-ttu-id="d2de6-235">ano</span><span class="sxs-lookup"><span data-stu-id="d2de6-235">yes</span></span>      | <span data-ttu-id="d2de6-236">Verze balíčku, které odpovídají danému požadavku</span><span class="sxs-lookup"><span data-stu-id="d2de6-236">The package versions matched by the request</span></span>

<span data-ttu-id="d2de6-237">Verze balíčku v `data` poli mohou obsahovat metadata sestavení SemVer 2.0.0 (například `1.0.0+metadata` ), pokud `semVerLevel=2.0.0` je v řetězci dotazu uvedena.</span><span class="sxs-lookup"><span data-stu-id="d2de6-237">The package versions in the `data` array may contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` is provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="d2de6-238">Ukázková žádost</span><span class="sxs-lookup"><span data-stu-id="d2de6-238">Sample request</span></span>

```
GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true
```

### <a name="sample-response"></a><span data-ttu-id="d2de6-239">Ukázková odpověď</span><span class="sxs-lookup"><span data-stu-id="d2de6-239">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
