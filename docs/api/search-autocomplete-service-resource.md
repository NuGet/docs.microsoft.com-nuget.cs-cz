---
title: Automatické dokončování, rozhraní API Nugetu
description: Vyhledávací služba Automatické dokončování podporuje interaktivní zjišťování balíčku ID a verze.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 2d2b20c1ea439ec0a3225cf983d9a4d2eedb0333
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324757"
---
# <a name="autocomplete"></a><span data-ttu-id="4e9f5-103">Automatické dokončování</span><span class="sxs-lookup"><span data-stu-id="4e9f5-103">Autocomplete</span></span>

<span data-ttu-id="4e9f5-104">Je možné vytvořit balíček ID a verzi automatického dokončování prostředí pomocí rozhraní API V3.</span><span class="sxs-lookup"><span data-stu-id="4e9f5-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="4e9f5-105">Je prostředek, který používá pro automatické dokončování dotazů `SearchAutocompleteService` prostředek se nenašel v [index služby](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="4e9f5-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="4e9f5-106">Správa verzí</span><span class="sxs-lookup"><span data-stu-id="4e9f5-106">Versioning</span></span>

<span data-ttu-id="4e9f5-107">Následující `@type` hodnoty:</span><span class="sxs-lookup"><span data-stu-id="4e9f5-107">The following `@type` values are used:</span></span>

<span data-ttu-id="4e9f5-108">@type Hodnota</span><span class="sxs-lookup"><span data-stu-id="4e9f5-108">@type value</span></span>                          | <span data-ttu-id="4e9f5-109">Poznámky</span><span class="sxs-lookup"><span data-stu-id="4e9f5-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="4e9f5-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="4e9f5-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="4e9f5-111">Počáteční verze</span><span class="sxs-lookup"><span data-stu-id="4e9f5-111">The initial release</span></span>
<span data-ttu-id="4e9f5-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="4e9f5-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="4e9f5-113">Alias of `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="4e9f5-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="4e9f5-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="4e9f5-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="4e9f5-115">Alias of `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="4e9f5-115">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="4e9f5-116">Základní adresa URL</span><span class="sxs-lookup"><span data-stu-id="4e9f5-116">Base URL</span></span>

<span data-ttu-id="4e9f5-117">Základní adresa URL pro následující rozhraní API je hodnota `@id` vlastnost přiřazené k některému z výše uvedených prostředků `@type` hodnoty.</span><span class="sxs-lookup"><span data-stu-id="4e9f5-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="4e9f5-118">V následujícím dokumentu, zástupný symbol základní adresa URL `{@id}` se použije.</span><span class="sxs-lookup"><span data-stu-id="4e9f5-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="4e9f5-119">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="4e9f5-119">HTTP Methods</span></span>

<span data-ttu-id="4e9f5-120">Všechny adresy URL, které jsou součástí zdroje podpory registrace metody HTTP `GET` a `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="4e9f5-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="4e9f5-121">Vyhledejte balíček ID</span><span class="sxs-lookup"><span data-stu-id="4e9f5-121">Search for package IDs</span></span>

<span data-ttu-id="4e9f5-122">První funkce automatického dokončování rozhraní API podporuje vyhledávání část řetězce ID balíčku.</span><span class="sxs-lookup"><span data-stu-id="4e9f5-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="4e9f5-123">To je skvělé, pokud byste chtěli poskytnout funkce typeahead balíčku v uživatelském rozhraní, integrovaný s zdroj balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="4e9f5-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="4e9f5-124">Balíček se pouze neuvedené v seznamu verzí se nezobrazí ve výsledcích.</span><span class="sxs-lookup"><span data-stu-id="4e9f5-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="4e9f5-125">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="4e9f5-125">Request parameters</span></span>

<span data-ttu-id="4e9f5-126">Název</span><span class="sxs-lookup"><span data-stu-id="4e9f5-126">Name</span></span>        | <span data-ttu-id="4e9f5-127">V</span><span class="sxs-lookup"><span data-stu-id="4e9f5-127">In</span></span>     | <span data-ttu-id="4e9f5-128">Typ</span><span class="sxs-lookup"><span data-stu-id="4e9f5-128">Type</span></span>    | <span data-ttu-id="4e9f5-129">Požadováno</span><span class="sxs-lookup"><span data-stu-id="4e9f5-129">Required</span></span> | <span data-ttu-id="4e9f5-130">Poznámky</span><span class="sxs-lookup"><span data-stu-id="4e9f5-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="4e9f5-131">q</span><span class="sxs-lookup"><span data-stu-id="4e9f5-131">q</span></span>           | <span data-ttu-id="4e9f5-132">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="4e9f5-132">URL</span></span>    | <span data-ttu-id="4e9f5-133">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="4e9f5-133">string</span></span>  | <span data-ttu-id="4e9f5-134">Ne</span><span class="sxs-lookup"><span data-stu-id="4e9f5-134">no</span></span>       | <span data-ttu-id="4e9f5-135">Řetězec určený k porovnání s ID balíčku</span><span class="sxs-lookup"><span data-stu-id="4e9f5-135">The string to compare against package IDs</span></span>
<span data-ttu-id="4e9f5-136">Přeskočit</span><span class="sxs-lookup"><span data-stu-id="4e9f5-136">skip</span></span>        | <span data-ttu-id="4e9f5-137">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="4e9f5-137">URL</span></span>    | <span data-ttu-id="4e9f5-138">integer</span><span class="sxs-lookup"><span data-stu-id="4e9f5-138">integer</span></span> | <span data-ttu-id="4e9f5-139">Ne</span><span class="sxs-lookup"><span data-stu-id="4e9f5-139">no</span></span>       | <span data-ttu-id="4e9f5-140">Počet výsledků, chcete-li přeskočit pro stránkování</span><span class="sxs-lookup"><span data-stu-id="4e9f5-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="4e9f5-141">Take</span><span class="sxs-lookup"><span data-stu-id="4e9f5-141">take</span></span>        | <span data-ttu-id="4e9f5-142">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="4e9f5-142">URL</span></span>    | <span data-ttu-id="4e9f5-143">integer</span><span class="sxs-lookup"><span data-stu-id="4e9f5-143">integer</span></span> | <span data-ttu-id="4e9f5-144">Ne</span><span class="sxs-lookup"><span data-stu-id="4e9f5-144">no</span></span>       | <span data-ttu-id="4e9f5-145">Počet výsledků, které má být vrácen pro stránkování</span><span class="sxs-lookup"><span data-stu-id="4e9f5-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="4e9f5-146">platnost předběžné verze</span><span class="sxs-lookup"><span data-stu-id="4e9f5-146">prerelease</span></span>  | <span data-ttu-id="4e9f5-147">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="4e9f5-147">URL</span></span>    | <span data-ttu-id="4e9f5-148">Logická hodnota</span><span class="sxs-lookup"><span data-stu-id="4e9f5-148">boolean</span></span> | <span data-ttu-id="4e9f5-149">Ne</span><span class="sxs-lookup"><span data-stu-id="4e9f5-149">no</span></span>       | <span data-ttu-id="4e9f5-150">`true` nebo `false` určující, jestli se mají zahrnout [balíčky v předběžné verzi](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="4e9f5-150">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="4e9f5-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="4e9f5-151">semVerLevel</span></span> | <span data-ttu-id="4e9f5-152">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="4e9f5-152">URL</span></span>    | <span data-ttu-id="4e9f5-153">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="4e9f5-153">string</span></span>  | <span data-ttu-id="4e9f5-154">Ne</span><span class="sxs-lookup"><span data-stu-id="4e9f5-154">no</span></span>       | <span data-ttu-id="4e9f5-155">Řetězec verze SemVer 1.0.0</span><span class="sxs-lookup"><span data-stu-id="4e9f5-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="4e9f5-156">Automatické dokončování dotazů `q` je analyzován způsobem, který je definován implementací serveru.</span><span class="sxs-lookup"><span data-stu-id="4e9f5-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="4e9f5-157">nuget.org podporuje dotazování pro předponu tokeny typu ID balíčku, které jsou částí ID vytvářených spliting původní znaky stylem camel case a symbol.</span><span class="sxs-lookup"><span data-stu-id="4e9f5-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="4e9f5-158">`skip` Parametr má výchozí hodnotu 0.</span><span class="sxs-lookup"><span data-stu-id="4e9f5-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="4e9f5-159">`take` Parametr by měl být celé číslo větší než nula.</span><span class="sxs-lookup"><span data-stu-id="4e9f5-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="4e9f5-160">Implementace serveru může uložit maximální hodnotu.</span><span class="sxs-lookup"><span data-stu-id="4e9f5-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="4e9f5-161">Pokud `prerelease` není zadán, jsou vyloučeny balíčky v předběžné verzi.</span><span class="sxs-lookup"><span data-stu-id="4e9f5-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="4e9f5-162">`semVerLevel` Parametr dotazu se používá k přihlášení k [SemVer 2.0.0 balíčky](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span><span class="sxs-lookup"><span data-stu-id="4e9f5-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="4e9f5-163">Pokud tento parametr dotazu je vyloučený, vrátí se pouze balíček ID s SemVer 1.0.0 kompatibilní verze (s [standardní správy verzí NuGet](../reference/package-versioning.md) upozornění, jako jsou třeba řetězce verze 4 dali celé číslo).</span><span class="sxs-lookup"><span data-stu-id="4e9f5-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="4e9f5-164">Pokud `semVerLevel=2.0.0` je k dispozici, bude vrácen SemVer 1.0.0 a kompatibilní balíčky SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="4e9f5-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="4e9f5-165">Zobrazit [SemVer 2.0.0 podpora nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) Další informace.</span><span class="sxs-lookup"><span data-stu-id="4e9f5-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="4e9f5-166">Odpověď</span><span class="sxs-lookup"><span data-stu-id="4e9f5-166">Response</span></span>

<span data-ttu-id="4e9f5-167">Odpověď je dokument JSON obsahující až `take` výsledky automatického dokončování.</span><span class="sxs-lookup"><span data-stu-id="4e9f5-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="4e9f5-168">Kořenový objekt JSON má následující vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="4e9f5-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="4e9f5-169">Název</span><span class="sxs-lookup"><span data-stu-id="4e9f5-169">Name</span></span>      | <span data-ttu-id="4e9f5-170">Typ</span><span class="sxs-lookup"><span data-stu-id="4e9f5-170">Type</span></span>             | <span data-ttu-id="4e9f5-171">Požadováno</span><span class="sxs-lookup"><span data-stu-id="4e9f5-171">Required</span></span> | <span data-ttu-id="4e9f5-172">Poznámky</span><span class="sxs-lookup"><span data-stu-id="4e9f5-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="4e9f5-173">totalHits</span><span class="sxs-lookup"><span data-stu-id="4e9f5-173">totalHits</span></span> | <span data-ttu-id="4e9f5-174">integer</span><span class="sxs-lookup"><span data-stu-id="4e9f5-174">integer</span></span>          | <span data-ttu-id="4e9f5-175">ano</span><span class="sxs-lookup"><span data-stu-id="4e9f5-175">yes</span></span>      | <span data-ttu-id="4e9f5-176">Celkový počet shod, bez ohledu na `skip` a `take`</span><span class="sxs-lookup"><span data-stu-id="4e9f5-176">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="4e9f5-177">data</span><span class="sxs-lookup"><span data-stu-id="4e9f5-177">data</span></span>      | <span data-ttu-id="4e9f5-178">pole řetězců</span><span class="sxs-lookup"><span data-stu-id="4e9f5-178">array of strings</span></span> | <span data-ttu-id="4e9f5-179">ano</span><span class="sxs-lookup"><span data-stu-id="4e9f5-179">yes</span></span>      | <span data-ttu-id="4e9f5-180">Balíček odpovídající ID požadavku</span><span class="sxs-lookup"><span data-stu-id="4e9f5-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="4e9f5-181">Ukázková žádost</span><span class="sxs-lookup"><span data-stu-id="4e9f5-181">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="4e9f5-182">Ukázková odpověď</span><span class="sxs-lookup"><span data-stu-id="4e9f5-182">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="4e9f5-183">Výčet verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="4e9f5-183">Enumerate package versions</span></span>

<span data-ttu-id="4e9f5-184">Po zjištění ID balíčku používat předchozí rozhraní API, může klient používat automatické dokončování rozhraní API k vytvoření výčtu verze balíčku pro ID zadaného balíčku.</span><span class="sxs-lookup"><span data-stu-id="4e9f5-184">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="4e9f5-185">Verze balíčku, který je neuvedené v seznamu se nezobrazí ve výsledcích.</span><span class="sxs-lookup"><span data-stu-id="4e9f5-185">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="4e9f5-186">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="4e9f5-186">Request parameters</span></span>

<span data-ttu-id="4e9f5-187">Název</span><span class="sxs-lookup"><span data-stu-id="4e9f5-187">Name</span></span>        | <span data-ttu-id="4e9f5-188">V</span><span class="sxs-lookup"><span data-stu-id="4e9f5-188">In</span></span>     | <span data-ttu-id="4e9f5-189">Typ</span><span class="sxs-lookup"><span data-stu-id="4e9f5-189">Type</span></span>    | <span data-ttu-id="4e9f5-190">Požadováno</span><span class="sxs-lookup"><span data-stu-id="4e9f5-190">Required</span></span> | <span data-ttu-id="4e9f5-191">Poznámky</span><span class="sxs-lookup"><span data-stu-id="4e9f5-191">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="4e9f5-192">id</span><span class="sxs-lookup"><span data-stu-id="4e9f5-192">id</span></span>          | <span data-ttu-id="4e9f5-193">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="4e9f5-193">URL</span></span>    | <span data-ttu-id="4e9f5-194">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="4e9f5-194">string</span></span>  | <span data-ttu-id="4e9f5-195">ano</span><span class="sxs-lookup"><span data-stu-id="4e9f5-195">yes</span></span>      | <span data-ttu-id="4e9f5-196">ID balíčku k načtení verze pro</span><span class="sxs-lookup"><span data-stu-id="4e9f5-196">The package ID to fetch versions for</span></span>
<span data-ttu-id="4e9f5-197">platnost předběžné verze</span><span class="sxs-lookup"><span data-stu-id="4e9f5-197">prerelease</span></span>  | <span data-ttu-id="4e9f5-198">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="4e9f5-198">URL</span></span>    | <span data-ttu-id="4e9f5-199">Logická hodnota</span><span class="sxs-lookup"><span data-stu-id="4e9f5-199">boolean</span></span> | <span data-ttu-id="4e9f5-200">Ne</span><span class="sxs-lookup"><span data-stu-id="4e9f5-200">no</span></span>       | <span data-ttu-id="4e9f5-201">`true` nebo `false` určující, jestli se mají zahrnout [balíčky v předběžné verzi](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="4e9f5-201">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="4e9f5-202">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="4e9f5-202">semVerLevel</span></span> | <span data-ttu-id="4e9f5-203">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="4e9f5-203">URL</span></span>    | <span data-ttu-id="4e9f5-204">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="4e9f5-204">string</span></span>  | <span data-ttu-id="4e9f5-205">Ne</span><span class="sxs-lookup"><span data-stu-id="4e9f5-205">no</span></span>       | <span data-ttu-id="4e9f5-206">Řetězec SemVer 2.0.0 verze</span><span class="sxs-lookup"><span data-stu-id="4e9f5-206">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="4e9f5-207">Pokud `prerelease` není zadán, jsou vyloučeny balíčky v předběžné verzi.</span><span class="sxs-lookup"><span data-stu-id="4e9f5-207">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="4e9f5-208">`semVerLevel` Parametr dotazu se používá k přihlášení k SemVer 2.0.0 balíčky.</span><span class="sxs-lookup"><span data-stu-id="4e9f5-208">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="4e9f5-209">Pokud tento parametr dotazu je vyloučený, vrátí se pouze verze SemVer 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="4e9f5-209">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="4e9f5-210">Pokud `semVerLevel=2.0.0` je k dispozici, bude vrácen SemVer 1.0.0 a verze SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="4e9f5-210">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="4e9f5-211">Zobrazit [SemVer 2.0.0 podpora nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) Další informace.</span><span class="sxs-lookup"><span data-stu-id="4e9f5-211">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="4e9f5-212">Odpověď</span><span class="sxs-lookup"><span data-stu-id="4e9f5-212">Response</span></span>

<span data-ttu-id="4e9f5-213">Odpověď je dokument JSON obsahující všechny verze balíčků poskytovaný balíček ID, daný dotaz s parametry filtrování.</span><span class="sxs-lookup"><span data-stu-id="4e9f5-213">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="4e9f5-214">Kořenový objekt JSON má následující vlastnost:</span><span class="sxs-lookup"><span data-stu-id="4e9f5-214">The root JSON object has the following property:</span></span>

<span data-ttu-id="4e9f5-215">Název</span><span class="sxs-lookup"><span data-stu-id="4e9f5-215">Name</span></span>      | <span data-ttu-id="4e9f5-216">Typ</span><span class="sxs-lookup"><span data-stu-id="4e9f5-216">Type</span></span>             | <span data-ttu-id="4e9f5-217">Požadováno</span><span class="sxs-lookup"><span data-stu-id="4e9f5-217">Required</span></span> | <span data-ttu-id="4e9f5-218">Poznámky</span><span class="sxs-lookup"><span data-stu-id="4e9f5-218">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="4e9f5-219">data</span><span class="sxs-lookup"><span data-stu-id="4e9f5-219">data</span></span>      | <span data-ttu-id="4e9f5-220">pole řetězců</span><span class="sxs-lookup"><span data-stu-id="4e9f5-220">array of strings</span></span> | <span data-ttu-id="4e9f5-221">ano</span><span class="sxs-lookup"><span data-stu-id="4e9f5-221">yes</span></span>      | <span data-ttu-id="4e9f5-222">Verze balíčku, který odpovídá požadavku</span><span class="sxs-lookup"><span data-stu-id="4e9f5-222">The package versions matched by the request</span></span>

<span data-ttu-id="4e9f5-223">Verze balíčku v `data` pole může obsahovat metadata sestavení SemVer 2.0.0 (třeba `1.0.0+metadata`) Pokud `semVerLevel=2.0.0` byla zadaná v řetězci dotazu.</span><span class="sxs-lookup"><span data-stu-id="4e9f5-223">The package versions in the `data` array could contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` was provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="4e9f5-224">Ukázková žádost</span><span class="sxs-lookup"><span data-stu-id="4e9f5-224">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="4e9f5-225">Ukázková odpověď</span><span class="sxs-lookup"><span data-stu-id="4e9f5-225">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
