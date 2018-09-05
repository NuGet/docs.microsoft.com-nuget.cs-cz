---
title: Automatické dokončování, rozhraní API Nugetu
description: Vyhledávací služba Automatické dokončování podporuje interaktivní zjišťování balíčku ID a verze.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 01f919dc3bbfb6752c8f8e055a3cd473ad194e75
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549080"
---
# <a name="autocomplete"></a><span data-ttu-id="c9d56-103">Automatické dokončování</span><span class="sxs-lookup"><span data-stu-id="c9d56-103">Autocomplete</span></span>

<span data-ttu-id="c9d56-104">Je možné vytvořit balíček ID a verzi automatického dokončování prostředí pomocí rozhraní API V3.</span><span class="sxs-lookup"><span data-stu-id="c9d56-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="c9d56-105">Je prostředek, který používá pro automatické dokončování dotazů `SearchAutocompleteService` prostředek se nenašel v [index služby](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="c9d56-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="c9d56-106">Správa verzí</span><span class="sxs-lookup"><span data-stu-id="c9d56-106">Versioning</span></span>

<span data-ttu-id="c9d56-107">Následující `@type` hodnoty:</span><span class="sxs-lookup"><span data-stu-id="c9d56-107">The following `@type` values are used:</span></span>

<span data-ttu-id="c9d56-108">@type Hodnota</span><span class="sxs-lookup"><span data-stu-id="c9d56-108">@type value</span></span>                          | <span data-ttu-id="c9d56-109">Poznámky</span><span class="sxs-lookup"><span data-stu-id="c9d56-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="c9d56-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="c9d56-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="c9d56-111">Počáteční verze</span><span class="sxs-lookup"><span data-stu-id="c9d56-111">The initial release</span></span>
<span data-ttu-id="c9d56-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="c9d56-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="c9d56-113">Alias `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="c9d56-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="c9d56-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="c9d56-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="c9d56-115">Alias `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="c9d56-115">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="c9d56-116">Základní adresa URL</span><span class="sxs-lookup"><span data-stu-id="c9d56-116">Base URL</span></span>

<span data-ttu-id="c9d56-117">Základní adresa URL pro následující rozhraní API je hodnota `@id` vlastnost přiřazené k některému z výše uvedených prostředků `@type` hodnoty.</span><span class="sxs-lookup"><span data-stu-id="c9d56-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="c9d56-118">V následujícím dokumentu, zástupný symbol základní adresa URL `{@id}` se použije.</span><span class="sxs-lookup"><span data-stu-id="c9d56-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="c9d56-119">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="c9d56-119">HTTP Methods</span></span>

<span data-ttu-id="c9d56-120">Všechny adresy URL, které jsou součástí zdroje podpory registrace metody HTTP `GET` a `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="c9d56-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="c9d56-121">Vyhledejte balíček ID</span><span class="sxs-lookup"><span data-stu-id="c9d56-121">Search for package IDs</span></span>

<span data-ttu-id="c9d56-122">První funkce automatického dokončování rozhraní API podporuje vyhledávání část řetězce ID balíčku.</span><span class="sxs-lookup"><span data-stu-id="c9d56-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="c9d56-123">To je skvělé, pokud byste chtěli poskytnout funkce typeahead balíčku v uživatelském rozhraní, integrovaný s zdroj balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="c9d56-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="c9d56-124">Balíček se pouze neuvedené v seznamu verzí se nezobrazí ve výsledcích.</span><span class="sxs-lookup"><span data-stu-id="c9d56-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="c9d56-125">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="c9d56-125">Request parameters</span></span>

<span data-ttu-id="c9d56-126">Název</span><span class="sxs-lookup"><span data-stu-id="c9d56-126">Name</span></span>        | <span data-ttu-id="c9d56-127">V</span><span class="sxs-lookup"><span data-stu-id="c9d56-127">In</span></span>     | <span data-ttu-id="c9d56-128">Typ</span><span class="sxs-lookup"><span data-stu-id="c9d56-128">Type</span></span>    | <span data-ttu-id="c9d56-129">Požadováno</span><span class="sxs-lookup"><span data-stu-id="c9d56-129">Required</span></span> | <span data-ttu-id="c9d56-130">Poznámky</span><span class="sxs-lookup"><span data-stu-id="c9d56-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="c9d56-131">q</span><span class="sxs-lookup"><span data-stu-id="c9d56-131">q</span></span>           | <span data-ttu-id="c9d56-132">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="c9d56-132">URL</span></span>    | <span data-ttu-id="c9d56-133">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="c9d56-133">string</span></span>  | <span data-ttu-id="c9d56-134">Ne</span><span class="sxs-lookup"><span data-stu-id="c9d56-134">no</span></span>       | <span data-ttu-id="c9d56-135">Řetězec určený k porovnání s ID balíčku</span><span class="sxs-lookup"><span data-stu-id="c9d56-135">The string to compare against package IDs</span></span>
<span data-ttu-id="c9d56-136">Přeskočit</span><span class="sxs-lookup"><span data-stu-id="c9d56-136">skip</span></span>        | <span data-ttu-id="c9d56-137">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="c9d56-137">URL</span></span>    | <span data-ttu-id="c9d56-138">integer</span><span class="sxs-lookup"><span data-stu-id="c9d56-138">integer</span></span> | <span data-ttu-id="c9d56-139">Ne</span><span class="sxs-lookup"><span data-stu-id="c9d56-139">no</span></span>       | <span data-ttu-id="c9d56-140">Počet výsledků, chcete-li přeskočit pro stránkování</span><span class="sxs-lookup"><span data-stu-id="c9d56-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="c9d56-141">Take</span><span class="sxs-lookup"><span data-stu-id="c9d56-141">take</span></span>        | <span data-ttu-id="c9d56-142">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="c9d56-142">URL</span></span>    | <span data-ttu-id="c9d56-143">integer</span><span class="sxs-lookup"><span data-stu-id="c9d56-143">integer</span></span> | <span data-ttu-id="c9d56-144">Ne</span><span class="sxs-lookup"><span data-stu-id="c9d56-144">no</span></span>       | <span data-ttu-id="c9d56-145">Počet výsledků, které má být vrácen pro stránkování</span><span class="sxs-lookup"><span data-stu-id="c9d56-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="c9d56-146">platnost předběžné verze</span><span class="sxs-lookup"><span data-stu-id="c9d56-146">prerelease</span></span>  | <span data-ttu-id="c9d56-147">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="c9d56-147">URL</span></span>    | <span data-ttu-id="c9d56-148">Logická hodnota</span><span class="sxs-lookup"><span data-stu-id="c9d56-148">boolean</span></span> | <span data-ttu-id="c9d56-149">Ne</span><span class="sxs-lookup"><span data-stu-id="c9d56-149">no</span></span>       | <span data-ttu-id="c9d56-150">`true` nebo `false` určující, jestli se mají zahrnout [balíčky v předběžné verzi](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="c9d56-150">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="c9d56-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="c9d56-151">semVerLevel</span></span> | <span data-ttu-id="c9d56-152">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="c9d56-152">URL</span></span>    | <span data-ttu-id="c9d56-153">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="c9d56-153">string</span></span>  | <span data-ttu-id="c9d56-154">Ne</span><span class="sxs-lookup"><span data-stu-id="c9d56-154">no</span></span>       | <span data-ttu-id="c9d56-155">Řetězec verze SemVer 1.0.0</span><span class="sxs-lookup"><span data-stu-id="c9d56-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="c9d56-156">Automatické dokončování dotazů `q` je analyzován způsobem, který je definován implementací serveru.</span><span class="sxs-lookup"><span data-stu-id="c9d56-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="c9d56-157">nuget.org podporuje dotazování pro předponu tokeny typu ID balíčku, které jsou částí ID vytvářených spliting původní znaky stylem camel case a symbol.</span><span class="sxs-lookup"><span data-stu-id="c9d56-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="c9d56-158">`skip` Parametr má výchozí hodnotu 0.</span><span class="sxs-lookup"><span data-stu-id="c9d56-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="c9d56-159">`take` Parametr by měl být celé číslo větší než nula.</span><span class="sxs-lookup"><span data-stu-id="c9d56-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="c9d56-160">Implementace serveru může uložit maximální hodnotu.</span><span class="sxs-lookup"><span data-stu-id="c9d56-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="c9d56-161">Pokud `prerelease` není zadán, jsou vyloučeny balíčky v předběžné verzi.</span><span class="sxs-lookup"><span data-stu-id="c9d56-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="c9d56-162">`semVerLevel` Parametr dotazu se používá k přihlášení k [SemVer 2.0.0 balíčky](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span><span class="sxs-lookup"><span data-stu-id="c9d56-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="c9d56-163">Pokud tento parametr dotazu je vyloučený, vrátí se pouze balíček ID s SemVer 1.0.0 kompatibilní verze (s [standardní správy verzí NuGet](../reference/package-versioning.md) upozornění, jako jsou třeba řetězce verze 4 dali celé číslo).</span><span class="sxs-lookup"><span data-stu-id="c9d56-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="c9d56-164">Pokud `semVerLevel=2.0.0` je k dispozici, bude vrácen SemVer 1.0.0 a kompatibilní balíčky SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="c9d56-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="c9d56-165">Zobrazit [SemVer 2.0.0 podpora nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) Další informace.</span><span class="sxs-lookup"><span data-stu-id="c9d56-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="c9d56-166">Odpověď</span><span class="sxs-lookup"><span data-stu-id="c9d56-166">Response</span></span>

<span data-ttu-id="c9d56-167">Odpověď je dokument JSON obsahující až `take` výsledky automatického dokončování.</span><span class="sxs-lookup"><span data-stu-id="c9d56-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="c9d56-168">Kořenový objekt JSON má následující vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="c9d56-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="c9d56-169">Název</span><span class="sxs-lookup"><span data-stu-id="c9d56-169">Name</span></span>      | <span data-ttu-id="c9d56-170">Typ</span><span class="sxs-lookup"><span data-stu-id="c9d56-170">Type</span></span>             | <span data-ttu-id="c9d56-171">Požadováno</span><span class="sxs-lookup"><span data-stu-id="c9d56-171">Required</span></span> | <span data-ttu-id="c9d56-172">Poznámky</span><span class="sxs-lookup"><span data-stu-id="c9d56-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="c9d56-173">totalHits</span><span class="sxs-lookup"><span data-stu-id="c9d56-173">totalHits</span></span> | <span data-ttu-id="c9d56-174">integer</span><span class="sxs-lookup"><span data-stu-id="c9d56-174">integer</span></span>          | <span data-ttu-id="c9d56-175">Ano</span><span class="sxs-lookup"><span data-stu-id="c9d56-175">yes</span></span>      | <span data-ttu-id="c9d56-176">Celkový počet shod, bez ohledu na `skip` a `take`</span><span class="sxs-lookup"><span data-stu-id="c9d56-176">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="c9d56-177">data</span><span class="sxs-lookup"><span data-stu-id="c9d56-177">data</span></span>      | <span data-ttu-id="c9d56-178">pole řetězců</span><span class="sxs-lookup"><span data-stu-id="c9d56-178">array of strings</span></span> | <span data-ttu-id="c9d56-179">Ano</span><span class="sxs-lookup"><span data-stu-id="c9d56-179">yes</span></span>      | <span data-ttu-id="c9d56-180">Balíček odpovídající ID požadavku</span><span class="sxs-lookup"><span data-stu-id="c9d56-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="c9d56-181">Ukázková žádost</span><span class="sxs-lookup"><span data-stu-id="c9d56-181">Sample request</span></span>

<span data-ttu-id="c9d56-182">ZÍSKAT https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span><span class="sxs-lookup"><span data-stu-id="c9d56-182">GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span></span>

### <a name="sample-response"></a><span data-ttu-id="c9d56-183">Ukázková odpověď</span><span class="sxs-lookup"><span data-stu-id="c9d56-183">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="c9d56-184">Výčet verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="c9d56-184">Enumerate package versions</span></span>

<span data-ttu-id="c9d56-185">Po zjištění ID balíčku používat předchozí rozhraní API, může klient používat automatické dokončování rozhraní API k vytvoření výčtu verze balíčku pro ID zadaného balíčku.</span><span class="sxs-lookup"><span data-stu-id="c9d56-185">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="c9d56-186">Verze balíčku, který je neuvedené v seznamu se nezobrazí ve výsledcích.</span><span class="sxs-lookup"><span data-stu-id="c9d56-186">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="c9d56-187">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="c9d56-187">Request parameters</span></span>

<span data-ttu-id="c9d56-188">Název</span><span class="sxs-lookup"><span data-stu-id="c9d56-188">Name</span></span>        | <span data-ttu-id="c9d56-189">V</span><span class="sxs-lookup"><span data-stu-id="c9d56-189">In</span></span>     | <span data-ttu-id="c9d56-190">Typ</span><span class="sxs-lookup"><span data-stu-id="c9d56-190">Type</span></span>    | <span data-ttu-id="c9d56-191">Požadováno</span><span class="sxs-lookup"><span data-stu-id="c9d56-191">Required</span></span> | <span data-ttu-id="c9d56-192">Poznámky</span><span class="sxs-lookup"><span data-stu-id="c9d56-192">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="c9d56-193">id</span><span class="sxs-lookup"><span data-stu-id="c9d56-193">id</span></span>          | <span data-ttu-id="c9d56-194">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="c9d56-194">URL</span></span>    | <span data-ttu-id="c9d56-195">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="c9d56-195">string</span></span>  | <span data-ttu-id="c9d56-196">Ano</span><span class="sxs-lookup"><span data-stu-id="c9d56-196">yes</span></span>      | <span data-ttu-id="c9d56-197">ID balíčku k načtení verze pro</span><span class="sxs-lookup"><span data-stu-id="c9d56-197">The package ID to fetch versions for</span></span>
<span data-ttu-id="c9d56-198">platnost předběžné verze</span><span class="sxs-lookup"><span data-stu-id="c9d56-198">prerelease</span></span>  | <span data-ttu-id="c9d56-199">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="c9d56-199">URL</span></span>    | <span data-ttu-id="c9d56-200">Logická hodnota</span><span class="sxs-lookup"><span data-stu-id="c9d56-200">boolean</span></span> | <span data-ttu-id="c9d56-201">Ne</span><span class="sxs-lookup"><span data-stu-id="c9d56-201">no</span></span>       | <span data-ttu-id="c9d56-202">`true` nebo `false` určující, jestli se mají zahrnout [balíčky v předběžné verzi](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="c9d56-202">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="c9d56-203">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="c9d56-203">semVerLevel</span></span> | <span data-ttu-id="c9d56-204">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="c9d56-204">URL</span></span>    | <span data-ttu-id="c9d56-205">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="c9d56-205">string</span></span>  | <span data-ttu-id="c9d56-206">Ne</span><span class="sxs-lookup"><span data-stu-id="c9d56-206">no</span></span>       | <span data-ttu-id="c9d56-207">Řetězec SemVer 2.0.0 verze</span><span class="sxs-lookup"><span data-stu-id="c9d56-207">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="c9d56-208">Pokud `prerelease` není zadán, jsou vyloučeny balíčky v předběžné verzi.</span><span class="sxs-lookup"><span data-stu-id="c9d56-208">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="c9d56-209">`semVerLevel` Parametr dotazu se používá k přihlášení k SemVer 2.0.0 balíčky.</span><span class="sxs-lookup"><span data-stu-id="c9d56-209">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="c9d56-210">Pokud tento parametr dotazu je vyloučený, vrátí se pouze verze SemVer 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="c9d56-210">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="c9d56-211">Pokud `semVerLevel=2.0.0` je k dispozici, bude vrácen SemVer 1.0.0 a verze SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="c9d56-211">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="c9d56-212">Zobrazit [SemVer 2.0.0 podpora nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) Další informace.</span><span class="sxs-lookup"><span data-stu-id="c9d56-212">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="c9d56-213">Odpověď</span><span class="sxs-lookup"><span data-stu-id="c9d56-213">Response</span></span>

<span data-ttu-id="c9d56-214">Odpověď je dokument JSON obsahující všechny verze balíčků poskytovaný balíček ID, daný dotaz s parametry filtrování.</span><span class="sxs-lookup"><span data-stu-id="c9d56-214">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="c9d56-215">Kořenový objekt JSON má následující vlastnost:</span><span class="sxs-lookup"><span data-stu-id="c9d56-215">The root JSON object has the following property:</span></span>

<span data-ttu-id="c9d56-216">Název</span><span class="sxs-lookup"><span data-stu-id="c9d56-216">Name</span></span>      | <span data-ttu-id="c9d56-217">Typ</span><span class="sxs-lookup"><span data-stu-id="c9d56-217">Type</span></span>             | <span data-ttu-id="c9d56-218">Požadováno</span><span class="sxs-lookup"><span data-stu-id="c9d56-218">Required</span></span> | <span data-ttu-id="c9d56-219">Poznámky</span><span class="sxs-lookup"><span data-stu-id="c9d56-219">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="c9d56-220">data</span><span class="sxs-lookup"><span data-stu-id="c9d56-220">data</span></span>      | <span data-ttu-id="c9d56-221">pole řetězců</span><span class="sxs-lookup"><span data-stu-id="c9d56-221">array of strings</span></span> | <span data-ttu-id="c9d56-222">Ano</span><span class="sxs-lookup"><span data-stu-id="c9d56-222">yes</span></span>      | <span data-ttu-id="c9d56-223">Verze balíčku, který odpovídá požadavku</span><span class="sxs-lookup"><span data-stu-id="c9d56-223">The package versions matched by the request</span></span>

<span data-ttu-id="c9d56-224">Verze balíčku v `data` pole může obsahovat metadata sestavení SemVer 2.0.0 (třeba `1.0.0+metadata`) Pokud `semVerLevel=2.0.0` byla zadaná v řetězci dotazu.</span><span class="sxs-lookup"><span data-stu-id="c9d56-224">The package versions in the `data` array could contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` was provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="c9d56-225">Ukázková žádost</span><span class="sxs-lookup"><span data-stu-id="c9d56-225">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="c9d56-226">Ukázková odpověď</span><span class="sxs-lookup"><span data-stu-id="c9d56-226">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
