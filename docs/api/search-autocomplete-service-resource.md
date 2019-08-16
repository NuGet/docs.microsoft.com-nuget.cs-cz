---
title: Automatické dokončování, rozhraní API NuGet
description: Služba Automatické dokončování hledání podporuje interaktivní zjišťování ID a verzí balíčků.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1179ad649da560766f28c18ab6fa670fd8fa6d8b
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488296"
---
# <a name="autocomplete"></a><span data-ttu-id="06d0e-103">Automatické dokončování</span><span class="sxs-lookup"><span data-stu-id="06d0e-103">Autocomplete</span></span>

<span data-ttu-id="06d0e-104">Pomocí rozhraní V3 API je možné vytvořit ID balíčku a verzi prostředí pro automatické dokončování.</span><span class="sxs-lookup"><span data-stu-id="06d0e-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="06d0e-105">Prostředek, který se používá k provedení dotazů automatického `SearchAutocompleteService` dokončování, je prostředek, který se nachází v [indexu služby](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="06d0e-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="06d0e-106">Správa verzí</span><span class="sxs-lookup"><span data-stu-id="06d0e-106">Versioning</span></span>

<span data-ttu-id="06d0e-107">Použijí se `@type` tyto hodnoty:</span><span class="sxs-lookup"><span data-stu-id="06d0e-107">The following `@type` values are used:</span></span>

<span data-ttu-id="06d0e-108">@typeosa</span><span class="sxs-lookup"><span data-stu-id="06d0e-108">@type value</span></span>                          | <span data-ttu-id="06d0e-109">Poznámky</span><span class="sxs-lookup"><span data-stu-id="06d0e-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="06d0e-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="06d0e-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="06d0e-111">Počáteční verze</span><span class="sxs-lookup"><span data-stu-id="06d0e-111">The initial release</span></span>
<span data-ttu-id="06d0e-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="06d0e-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="06d0e-113">Alias pro`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="06d0e-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="06d0e-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="06d0e-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="06d0e-115">Alias pro`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="06d0e-115">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="06d0e-116">Základní adresa URL</span><span class="sxs-lookup"><span data-stu-id="06d0e-116">Base URL</span></span>

<span data-ttu-id="06d0e-117">Základní adresa URL následujících rozhraní API je hodnota `@id` vlastnosti přidružené k jedné z výše uvedených hodnot prostředků. `@type`</span><span class="sxs-lookup"><span data-stu-id="06d0e-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="06d0e-118">V následujícím dokumentu se použije zástupná základní `{@id}` adresa URL.</span><span class="sxs-lookup"><span data-stu-id="06d0e-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="06d0e-119">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="06d0e-119">HTTP Methods</span></span>

<span data-ttu-id="06d0e-120">Všechny adresy URL nalezené v registračním prostředku podporují metody `GET` http `HEAD`a.</span><span class="sxs-lookup"><span data-stu-id="06d0e-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="06d0e-121">Vyhledat ID balíčků</span><span class="sxs-lookup"><span data-stu-id="06d0e-121">Search for package IDs</span></span>

<span data-ttu-id="06d0e-122">První rozhraní API pro automatické dokončování podporuje hledání částí řetězce ID balíčku.</span><span class="sxs-lookup"><span data-stu-id="06d0e-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="06d0e-123">To je skvělé, když chcete poskytnout funkci balíčku typeahead v uživatelském rozhraní integrovaném se zdrojem balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="06d0e-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="06d0e-124">Ve výsledcích se nezobrazí balíček s pouze neuvedenými verzemi.</span><span class="sxs-lookup"><span data-stu-id="06d0e-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="06d0e-125">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="06d0e-125">Request parameters</span></span>

<span data-ttu-id="06d0e-126">Name</span><span class="sxs-lookup"><span data-stu-id="06d0e-126">Name</span></span>        | <span data-ttu-id="06d0e-127">V</span><span class="sxs-lookup"><span data-stu-id="06d0e-127">In</span></span>     | <span data-ttu-id="06d0e-128">type</span><span class="sxs-lookup"><span data-stu-id="06d0e-128">Type</span></span>    | <span data-ttu-id="06d0e-129">Požadováno</span><span class="sxs-lookup"><span data-stu-id="06d0e-129">Required</span></span> | <span data-ttu-id="06d0e-130">Poznámky</span><span class="sxs-lookup"><span data-stu-id="06d0e-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="06d0e-131">q</span><span class="sxs-lookup"><span data-stu-id="06d0e-131">q</span></span>           | <span data-ttu-id="06d0e-132">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="06d0e-132">URL</span></span>    | <span data-ttu-id="06d0e-133">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="06d0e-133">string</span></span>  | <span data-ttu-id="06d0e-134">Ne</span><span class="sxs-lookup"><span data-stu-id="06d0e-134">no</span></span>       | <span data-ttu-id="06d0e-135">Řetězec, který se má porovnat s ID balíčků</span><span class="sxs-lookup"><span data-stu-id="06d0e-135">The string to compare against package IDs</span></span>
<span data-ttu-id="06d0e-136">Přeskočit</span><span class="sxs-lookup"><span data-stu-id="06d0e-136">skip</span></span>        | <span data-ttu-id="06d0e-137">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="06d0e-137">URL</span></span>    | <span data-ttu-id="06d0e-138">integer</span><span class="sxs-lookup"><span data-stu-id="06d0e-138">integer</span></span> | <span data-ttu-id="06d0e-139">Ne</span><span class="sxs-lookup"><span data-stu-id="06d0e-139">no</span></span>       | <span data-ttu-id="06d0e-140">Počet výsledků, které se mají přeskočit, pro stránkování</span><span class="sxs-lookup"><span data-stu-id="06d0e-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="06d0e-141">nezbytná</span><span class="sxs-lookup"><span data-stu-id="06d0e-141">take</span></span>        | <span data-ttu-id="06d0e-142">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="06d0e-142">URL</span></span>    | <span data-ttu-id="06d0e-143">integer</span><span class="sxs-lookup"><span data-stu-id="06d0e-143">integer</span></span> | <span data-ttu-id="06d0e-144">Ne</span><span class="sxs-lookup"><span data-stu-id="06d0e-144">no</span></span>       | <span data-ttu-id="06d0e-145">Počet výsledků, které se mají vrátit, pro stránkování</span><span class="sxs-lookup"><span data-stu-id="06d0e-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="06d0e-146">předběžné verze</span><span class="sxs-lookup"><span data-stu-id="06d0e-146">prerelease</span></span>  | <span data-ttu-id="06d0e-147">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="06d0e-147">URL</span></span>    | <span data-ttu-id="06d0e-148">Logická hodnota</span><span class="sxs-lookup"><span data-stu-id="06d0e-148">boolean</span></span> | <span data-ttu-id="06d0e-149">Ne</span><span class="sxs-lookup"><span data-stu-id="06d0e-149">no</span></span>       | <span data-ttu-id="06d0e-150">`true`nebo `false` určete, jestli se mají zahrnout [předběžné verze balíčků](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="06d0e-150">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="06d0e-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="06d0e-151">semVerLevel</span></span> | <span data-ttu-id="06d0e-152">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="06d0e-152">URL</span></span>    | <span data-ttu-id="06d0e-153">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="06d0e-153">string</span></span>  | <span data-ttu-id="06d0e-154">Ne</span><span class="sxs-lookup"><span data-stu-id="06d0e-154">no</span></span>       | <span data-ttu-id="06d0e-155">Řetězec verze SemVer 1.0.0</span><span class="sxs-lookup"><span data-stu-id="06d0e-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="06d0e-156">Dotaz `q` na automatické dokončování je analyzován způsobem, který je definován implementací serveru.</span><span class="sxs-lookup"><span data-stu-id="06d0e-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="06d0e-157">nuget.org podporuje dotazování na předponu tokenů ID balíčku, které jsou částmi ID vytvořenými rozdělením originálu pomocí znaků písmen a symbolů ve stylu CamelCase.</span><span class="sxs-lookup"><span data-stu-id="06d0e-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="06d0e-158">`skip` Parametr má výchozí hodnotu 0.</span><span class="sxs-lookup"><span data-stu-id="06d0e-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="06d0e-159">`take` Parametr by měl být celé číslo větší než nula.</span><span class="sxs-lookup"><span data-stu-id="06d0e-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="06d0e-160">Implementace serveru může poskytovat maximální hodnotu.</span><span class="sxs-lookup"><span data-stu-id="06d0e-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="06d0e-161">Pokud `prerelease` není zadaný, vyloučí se balíčky předběžných verzí.</span><span class="sxs-lookup"><span data-stu-id="06d0e-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="06d0e-162">Parametr dotazu se používá pro výslovný souhlas s [SemVer balíčky 2.0.0.](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages) `semVerLevel`</span><span class="sxs-lookup"><span data-stu-id="06d0e-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="06d0e-163">Pokud je tento parametr dotazu vyloučený, vrátí se jenom ID balíčků se kompatibilními verzemi SemVer 1.0.0 (se standardními omezeními [verzí NuGet](../concepts/package-versioning.md) , jako jsou například řetězce verze se 4 celými čísly).</span><span class="sxs-lookup"><span data-stu-id="06d0e-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../concepts/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="06d0e-164">Pokud `semVerLevel=2.0.0` je k dispozici, budou vráceny balíčky kompatibilní s SemVer 1.0.0 a SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="06d0e-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="06d0e-165">Další informace najdete v tématu [Podpora SemVer 2.0.0 pro NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .</span><span class="sxs-lookup"><span data-stu-id="06d0e-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="06d0e-166">Odpověď</span><span class="sxs-lookup"><span data-stu-id="06d0e-166">Response</span></span>

<span data-ttu-id="06d0e-167">Odpověď je dokument JSON, který obsahuje `take` výsledky automatického dokončování.</span><span class="sxs-lookup"><span data-stu-id="06d0e-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="06d0e-168">Kořenový objekt JSON má následující vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="06d0e-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="06d0e-169">Name</span><span class="sxs-lookup"><span data-stu-id="06d0e-169">Name</span></span>      | <span data-ttu-id="06d0e-170">type</span><span class="sxs-lookup"><span data-stu-id="06d0e-170">Type</span></span>             | <span data-ttu-id="06d0e-171">Požadováno</span><span class="sxs-lookup"><span data-stu-id="06d0e-171">Required</span></span> | <span data-ttu-id="06d0e-172">Poznámky</span><span class="sxs-lookup"><span data-stu-id="06d0e-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="06d0e-173">totalHits</span><span class="sxs-lookup"><span data-stu-id="06d0e-173">totalHits</span></span> | <span data-ttu-id="06d0e-174">integer</span><span class="sxs-lookup"><span data-stu-id="06d0e-174">integer</span></span>          | <span data-ttu-id="06d0e-175">ano</span><span class="sxs-lookup"><span data-stu-id="06d0e-175">yes</span></span>      | <span data-ttu-id="06d0e-176">Celkový počet shod, nesouvisející `skip` a`take`</span><span class="sxs-lookup"><span data-stu-id="06d0e-176">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="06d0e-177">data</span><span class="sxs-lookup"><span data-stu-id="06d0e-177">data</span></span>      | <span data-ttu-id="06d0e-178">pole řetězců</span><span class="sxs-lookup"><span data-stu-id="06d0e-178">array of strings</span></span> | <span data-ttu-id="06d0e-179">ano</span><span class="sxs-lookup"><span data-stu-id="06d0e-179">yes</span></span>      | <span data-ttu-id="06d0e-180">ID balíčků, které odpovídá požadavek</span><span class="sxs-lookup"><span data-stu-id="06d0e-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="06d0e-181">Ukázková žádost</span><span class="sxs-lookup"><span data-stu-id="06d0e-181">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="06d0e-182">Ukázková odpověď</span><span class="sxs-lookup"><span data-stu-id="06d0e-182">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="06d0e-183">Zobrazení výčtu verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="06d0e-183">Enumerate package versions</span></span>

<span data-ttu-id="06d0e-184">Po zjištění ID balíčku pomocí předchozího rozhraní API může klient použít rozhraní API pro automatické dokončování k zobrazení výčtu verzí balíčků pro zadané ID balíčku.</span><span class="sxs-lookup"><span data-stu-id="06d0e-184">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="06d0e-185">Ve výsledcích se nezobrazí verze balíčku, který není uveden v seznamu.</span><span class="sxs-lookup"><span data-stu-id="06d0e-185">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="06d0e-186">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="06d0e-186">Request parameters</span></span>

<span data-ttu-id="06d0e-187">Name</span><span class="sxs-lookup"><span data-stu-id="06d0e-187">Name</span></span>        | <span data-ttu-id="06d0e-188">V</span><span class="sxs-lookup"><span data-stu-id="06d0e-188">In</span></span>     | <span data-ttu-id="06d0e-189">type</span><span class="sxs-lookup"><span data-stu-id="06d0e-189">Type</span></span>    | <span data-ttu-id="06d0e-190">Požadováno</span><span class="sxs-lookup"><span data-stu-id="06d0e-190">Required</span></span> | <span data-ttu-id="06d0e-191">Poznámky</span><span class="sxs-lookup"><span data-stu-id="06d0e-191">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="06d0e-192">id</span><span class="sxs-lookup"><span data-stu-id="06d0e-192">id</span></span>          | <span data-ttu-id="06d0e-193">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="06d0e-193">URL</span></span>    | <span data-ttu-id="06d0e-194">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="06d0e-194">string</span></span>  | <span data-ttu-id="06d0e-195">ano</span><span class="sxs-lookup"><span data-stu-id="06d0e-195">yes</span></span>      | <span data-ttu-id="06d0e-196">ID balíčku, pro který se mají načíst verze</span><span class="sxs-lookup"><span data-stu-id="06d0e-196">The package ID to fetch versions for</span></span>
<span data-ttu-id="06d0e-197">předběžné verze</span><span class="sxs-lookup"><span data-stu-id="06d0e-197">prerelease</span></span>  | <span data-ttu-id="06d0e-198">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="06d0e-198">URL</span></span>    | <span data-ttu-id="06d0e-199">Logická hodnota</span><span class="sxs-lookup"><span data-stu-id="06d0e-199">boolean</span></span> | <span data-ttu-id="06d0e-200">Ne</span><span class="sxs-lookup"><span data-stu-id="06d0e-200">no</span></span>       | <span data-ttu-id="06d0e-201">`true`nebo `false` určete, jestli se mají zahrnout [předběžné verze balíčků](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="06d0e-201">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="06d0e-202">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="06d0e-202">semVerLevel</span></span> | <span data-ttu-id="06d0e-203">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="06d0e-203">URL</span></span>    | <span data-ttu-id="06d0e-204">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="06d0e-204">string</span></span>  | <span data-ttu-id="06d0e-205">Ne</span><span class="sxs-lookup"><span data-stu-id="06d0e-205">no</span></span>       | <span data-ttu-id="06d0e-206">Řetězec verze SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="06d0e-206">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="06d0e-207">Pokud `prerelease` není zadaný, vyloučí se balíčky předběžných verzí.</span><span class="sxs-lookup"><span data-stu-id="06d0e-207">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="06d0e-208">Parametr `semVerLevel` dotazu se používá pro výslovný souhlas s SemVer balíčky 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="06d0e-208">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="06d0e-209">Pokud je tento parametr dotazu vyloučený, vrátí se pouze verze SemVer 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="06d0e-209">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="06d0e-210">Pokud `semVerLevel=2.0.0` je k dispozici, vrátí se obě verze SemVer 1.0.0 a SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="06d0e-210">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="06d0e-211">Další informace najdete v tématu [Podpora SemVer 2.0.0 pro NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) .</span><span class="sxs-lookup"><span data-stu-id="06d0e-211">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="06d0e-212">Odpověď</span><span class="sxs-lookup"><span data-stu-id="06d0e-212">Response</span></span>

<span data-ttu-id="06d0e-213">Odpověď je dokument JSON obsahující všechny verze balíčků zadaného ID balíčku, které filtrují podle daných parametrů dotazu.</span><span class="sxs-lookup"><span data-stu-id="06d0e-213">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="06d0e-214">Kořenový objekt JSON má následující vlastnost:</span><span class="sxs-lookup"><span data-stu-id="06d0e-214">The root JSON object has the following property:</span></span>

<span data-ttu-id="06d0e-215">Name</span><span class="sxs-lookup"><span data-stu-id="06d0e-215">Name</span></span>      | <span data-ttu-id="06d0e-216">type</span><span class="sxs-lookup"><span data-stu-id="06d0e-216">Type</span></span>             | <span data-ttu-id="06d0e-217">Požadováno</span><span class="sxs-lookup"><span data-stu-id="06d0e-217">Required</span></span> | <span data-ttu-id="06d0e-218">Poznámky</span><span class="sxs-lookup"><span data-stu-id="06d0e-218">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="06d0e-219">data</span><span class="sxs-lookup"><span data-stu-id="06d0e-219">data</span></span>      | <span data-ttu-id="06d0e-220">pole řetězců</span><span class="sxs-lookup"><span data-stu-id="06d0e-220">array of strings</span></span> | <span data-ttu-id="06d0e-221">ano</span><span class="sxs-lookup"><span data-stu-id="06d0e-221">yes</span></span>      | <span data-ttu-id="06d0e-222">Verze balíčku, které odpovídají danému požadavku</span><span class="sxs-lookup"><span data-stu-id="06d0e-222">The package versions matched by the request</span></span>

<span data-ttu-id="06d0e-223">Verze balíčku v `data` poli mohou obsahovat metadata sestavení SemVer 2.0.0 ( `1.0.0+metadata`například), `semVerLevel=2.0.0` Pokud je v řetězci dotazu uvedena.</span><span class="sxs-lookup"><span data-stu-id="06d0e-223">The package versions in the `data` array may contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` is provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="06d0e-224">Ukázková žádost</span><span class="sxs-lookup"><span data-stu-id="06d0e-224">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="06d0e-225">Ukázková odpověď</span><span class="sxs-lookup"><span data-stu-id="06d0e-225">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
