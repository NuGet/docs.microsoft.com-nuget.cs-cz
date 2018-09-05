---
title: Nasdílení změn a odstranění rozhraní API Nugetu
description: Služba publikování umožňuje klientům publikovat nové balíčky a vyjmutí ze seznamu nebo odstranit existující balíčky.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: ad66d8e0ffda13aaef744104c213863b0e111e0e
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547518"
---
# <a name="push-and-delete"></a><span data-ttu-id="52832-103">Nasdílení změn a odstranění</span><span class="sxs-lookup"><span data-stu-id="52832-103">Push and Delete</span></span>

<span data-ttu-id="52832-104">Je možné vložit, odstranit (nebo vyjmutí ze seznamu, v závislosti na implementaci serveru) a relist balíčky pomocí rozhraní API V3 NuGet.</span><span class="sxs-lookup"><span data-stu-id="52832-104">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="52832-105">Tyto operace jsou odhlásit z založené `PackagePublish` prostředek se nenašel v [index služby](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="52832-105">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="52832-106">Správa verzí</span><span class="sxs-lookup"><span data-stu-id="52832-106">Versioning</span></span>

<span data-ttu-id="52832-107">Následující `@type` hodnota se používá:</span><span class="sxs-lookup"><span data-stu-id="52832-107">The following `@type` value is used:</span></span>

<span data-ttu-id="52832-108">@type Hodnota</span><span class="sxs-lookup"><span data-stu-id="52832-108">@type value</span></span>          | <span data-ttu-id="52832-109">Poznámky</span><span class="sxs-lookup"><span data-stu-id="52832-109">Notes</span></span>
-------------------- | -----
<span data-ttu-id="52832-110">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="52832-110">PackagePublish/2.0.0</span></span> | <span data-ttu-id="52832-111">Počáteční verze</span><span class="sxs-lookup"><span data-stu-id="52832-111">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="52832-112">Základní adresa URL</span><span class="sxs-lookup"><span data-stu-id="52832-112">Base URL</span></span>

<span data-ttu-id="52832-113">Základní adresa URL pro následující rozhraní API je hodnota `@id` vlastnost `PackagePublish/2.0.0` prostředků ve zdroji balíčku [index služby](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="52832-113">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="52832-114">Pro níže uvedenou dokumentaci se používá adresu URL nuget.org.</span><span class="sxs-lookup"><span data-stu-id="52832-114">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="52832-115">Vezměte v úvahu `https://www.nuget.org/api/v2/package` jako zástupný symbol pro `@id` hodnota nalezena v indexu služby.</span><span class="sxs-lookup"><span data-stu-id="52832-115">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="52832-116">Všimněte si, že tato adresa URL odkazuje do stejného umístění jako starší verze koncového bodu V2 nabízených oznámení, protože protokol je stejný.</span><span class="sxs-lookup"><span data-stu-id="52832-116">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="52832-117">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="52832-117">HTTP methods</span></span>

<span data-ttu-id="52832-118">`PUT`, `POST` a `DELETE` tento prostředek podporovaných metod HTTP.</span><span class="sxs-lookup"><span data-stu-id="52832-118">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="52832-119">Které metody jsou podporovány na každém koncovém bodu najdete níže.</span><span class="sxs-lookup"><span data-stu-id="52832-119">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="52832-120">Push balíčku</span><span class="sxs-lookup"><span data-stu-id="52832-120">Push a package</span></span>

> [!Note]
> <span data-ttu-id="52832-121">má nuget.org [další požadavky](NuGet-Protocols.md) pro komunikaci s koncovým bodem nabízených oznámení.</span><span class="sxs-lookup"><span data-stu-id="52832-121">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="52832-122">nuget.org podporuje vkládání nové balíčky pomocí následující rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="52832-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="52832-123">Pokud balíček s zadané ID a verzí již existuje, bude taková nuget.org nasdílení změn.</span><span class="sxs-lookup"><span data-stu-id="52832-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="52832-124">Další zdroje balíčků můžou podporovat nahrazení existujícího balíčku.</span><span class="sxs-lookup"><span data-stu-id="52832-124">Other package sources may support replacing an existing package.</span></span>

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a><span data-ttu-id="52832-125">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="52832-125">Request parameters</span></span>

<span data-ttu-id="52832-126">Název</span><span class="sxs-lookup"><span data-stu-id="52832-126">Name</span></span>           | <span data-ttu-id="52832-127">V</span><span class="sxs-lookup"><span data-stu-id="52832-127">In</span></span>     | <span data-ttu-id="52832-128">Typ</span><span class="sxs-lookup"><span data-stu-id="52832-128">Type</span></span>   | <span data-ttu-id="52832-129">Požadováno</span><span class="sxs-lookup"><span data-stu-id="52832-129">Required</span></span> | <span data-ttu-id="52832-130">Poznámky</span><span class="sxs-lookup"><span data-stu-id="52832-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="52832-131">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="52832-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="52832-132">Záhlaví</span><span class="sxs-lookup"><span data-stu-id="52832-132">Header</span></span> | <span data-ttu-id="52832-133">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="52832-133">string</span></span> | <span data-ttu-id="52832-134">Ano</span><span class="sxs-lookup"><span data-stu-id="52832-134">yes</span></span>      | <span data-ttu-id="52832-135">Třeba `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="52832-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="52832-136">Klíč rozhraní API je neprůhledný řetězec získali ze zdroje balíčku uživatelem a konfiguraci do klienta.</span><span class="sxs-lookup"><span data-stu-id="52832-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="52832-137">Je vyžadováno žádné konkrétní řetězec formátu, ale délka klíče rozhraní API by neměl být delší než rozumnou velikost pro hodnoty hlavičky protokolu HTTP.</span><span class="sxs-lookup"><span data-stu-id="52832-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="52832-138">Text žádosti</span><span class="sxs-lookup"><span data-stu-id="52832-138">Request body</span></span>

<span data-ttu-id="52832-139">Text požadavku musí být v následujícím tvaru:</span><span class="sxs-lookup"><span data-stu-id="52832-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="52832-140">Dat vícedílného formuláře</span><span class="sxs-lookup"><span data-stu-id="52832-140">Multipart form data</span></span>

<span data-ttu-id="52832-141">Hlavička požadavku `Content-Type` je `multipart/form-data` a nezpracované bajtů .nupkg stisknuté je první položka v textu požadavku.</span><span class="sxs-lookup"><span data-stu-id="52832-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="52832-142">Následující položky v textu vícedílné zprávy jsou ignorovány.</span><span class="sxs-lookup"><span data-stu-id="52832-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="52832-143">Název souboru nebo jiné záhlaví položek s více částmi. jsou ignorovány.</span><span class="sxs-lookup"><span data-stu-id="52832-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="52832-144">Odpověď</span><span class="sxs-lookup"><span data-stu-id="52832-144">Response</span></span>

<span data-ttu-id="52832-145">Stavový kód</span><span class="sxs-lookup"><span data-stu-id="52832-145">Status Code</span></span> | <span data-ttu-id="52832-146">Význam</span><span class="sxs-lookup"><span data-stu-id="52832-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="52832-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="52832-147">201, 202</span></span>    | <span data-ttu-id="52832-148">Balíček byl úspěšně odeslal.</span><span class="sxs-lookup"><span data-stu-id="52832-148">The package was successfully pushed</span></span>
<span data-ttu-id="52832-149">400</span><span class="sxs-lookup"><span data-stu-id="52832-149">400</span></span>         | <span data-ttu-id="52832-150">Zadaný balíček je neplatný</span><span class="sxs-lookup"><span data-stu-id="52832-150">The provided package is invalid</span></span>
<span data-ttu-id="52832-151">409</span><span class="sxs-lookup"><span data-stu-id="52832-151">409</span></span>         | <span data-ttu-id="52832-152">Balíček se zadané ID a verze již existuje.</span><span class="sxs-lookup"><span data-stu-id="52832-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="52832-153">Implementace serveru lišit na stavový kód úspěchu vrátí, když se úspěšně odeslal balíček.</span><span class="sxs-lookup"><span data-stu-id="52832-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="52832-154">Odstranění balíčku</span><span class="sxs-lookup"><span data-stu-id="52832-154">Delete a package</span></span>

<span data-ttu-id="52832-155">nuget.org interpretuje požadavku na odstranění balíčku jako příslušný "vyjmutí ze seznamu".</span><span class="sxs-lookup"><span data-stu-id="52832-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="52832-156">To znamená, že balíček je stále k dispozici pro stávající zákazníky balíček, ale balíček už se zobrazí ve výsledcích hledání nebo ve webovém rozhraní.</span><span class="sxs-lookup"><span data-stu-id="52832-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="52832-157">Další informace o tento postup najdete v článku [odstranit balíčky](../policies/deleting-packages.md) zásad.</span><span class="sxs-lookup"><span data-stu-id="52832-157">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="52832-158">Jiné implementace serveru je zdarma jak interpretovat jako pevný odstranit tento signál, obnovitelné odstranění nebo vyjmutí ze seznamu.</span><span class="sxs-lookup"><span data-stu-id="52832-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="52832-159">Například [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (na serveru implementace podporuje pouze rozhraní API pro starší verze 2) podporuje tato žádost zpracovává jako unlist nebo pevné delete založené na možnosti konfigurace.</span><span class="sxs-lookup"><span data-stu-id="52832-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="52832-160">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="52832-160">Request parameters</span></span>

<span data-ttu-id="52832-161">Název</span><span class="sxs-lookup"><span data-stu-id="52832-161">Name</span></span>           | <span data-ttu-id="52832-162">V</span><span class="sxs-lookup"><span data-stu-id="52832-162">In</span></span>     | <span data-ttu-id="52832-163">Typ</span><span class="sxs-lookup"><span data-stu-id="52832-163">Type</span></span>   | <span data-ttu-id="52832-164">Požadováno</span><span class="sxs-lookup"><span data-stu-id="52832-164">Required</span></span> | <span data-ttu-id="52832-165">Poznámky</span><span class="sxs-lookup"><span data-stu-id="52832-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="52832-166">ID</span><span class="sxs-lookup"><span data-stu-id="52832-166">ID</span></span>             | <span data-ttu-id="52832-167">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="52832-167">URL</span></span>    | <span data-ttu-id="52832-168">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="52832-168">string</span></span> | <span data-ttu-id="52832-169">Ano</span><span class="sxs-lookup"><span data-stu-id="52832-169">yes</span></span>      | <span data-ttu-id="52832-170">ID balíčku, který se má odstranit</span><span class="sxs-lookup"><span data-stu-id="52832-170">The ID of the package to delete</span></span>
<span data-ttu-id="52832-171">VERZE</span><span class="sxs-lookup"><span data-stu-id="52832-171">VERSION</span></span>        | <span data-ttu-id="52832-172">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="52832-172">URL</span></span>    | <span data-ttu-id="52832-173">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="52832-173">string</span></span> | <span data-ttu-id="52832-174">Ano</span><span class="sxs-lookup"><span data-stu-id="52832-174">yes</span></span>      | <span data-ttu-id="52832-175">Verze balíčku k odstranění</span><span class="sxs-lookup"><span data-stu-id="52832-175">The version of the package to delete</span></span>
<span data-ttu-id="52832-176">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="52832-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="52832-177">Záhlaví</span><span class="sxs-lookup"><span data-stu-id="52832-177">Header</span></span> | <span data-ttu-id="52832-178">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="52832-178">string</span></span> | <span data-ttu-id="52832-179">Ano</span><span class="sxs-lookup"><span data-stu-id="52832-179">yes</span></span>      | <span data-ttu-id="52832-180">Třeba `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="52832-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="52832-181">Odpověď</span><span class="sxs-lookup"><span data-stu-id="52832-181">Response</span></span>

<span data-ttu-id="52832-182">Stavový kód</span><span class="sxs-lookup"><span data-stu-id="52832-182">Status Code</span></span> | <span data-ttu-id="52832-183">Význam</span><span class="sxs-lookup"><span data-stu-id="52832-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="52832-184">204</span><span class="sxs-lookup"><span data-stu-id="52832-184">204</span></span>         | <span data-ttu-id="52832-185">Balíček byl odstraněn.</span><span class="sxs-lookup"><span data-stu-id="52832-185">The package was deleted</span></span>
<span data-ttu-id="52832-186">404</span><span class="sxs-lookup"><span data-stu-id="52832-186">404</span></span>         | <span data-ttu-id="52832-187">Žádný balíček pomocí zadaných `ID` a `VERSION` existuje</span><span class="sxs-lookup"><span data-stu-id="52832-187">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="52832-188">Relist balíčku</span><span class="sxs-lookup"><span data-stu-id="52832-188">Relist a package</span></span>

<span data-ttu-id="52832-189">Pokud balíček je neuvedené v seznamu, je možné vytvořit balíček znovu viditelné ve výsledcích vyhledávání pomocí koncového bodu "relist".</span><span class="sxs-lookup"><span data-stu-id="52832-189">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="52832-190">Tento koncový bod má stejný tvar jako [odstranit (vyjmutí ze seznamu) koncového bodu](#delete-a-package) , ale používá `POST` metoda protokolu HTTP místo `DELETE` metody.</span><span class="sxs-lookup"><span data-stu-id="52832-190">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="52832-191">Pokud už je balíček uvedený, stále neproběhne.</span><span class="sxs-lookup"><span data-stu-id="52832-191">If the package is already listed, the request still succeeds.</span></span>

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="52832-192">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="52832-192">Request parameters</span></span>

<span data-ttu-id="52832-193">Název</span><span class="sxs-lookup"><span data-stu-id="52832-193">Name</span></span>           | <span data-ttu-id="52832-194">V</span><span class="sxs-lookup"><span data-stu-id="52832-194">In</span></span>     | <span data-ttu-id="52832-195">Typ</span><span class="sxs-lookup"><span data-stu-id="52832-195">Type</span></span>   | <span data-ttu-id="52832-196">Požadováno</span><span class="sxs-lookup"><span data-stu-id="52832-196">Required</span></span> | <span data-ttu-id="52832-197">Poznámky</span><span class="sxs-lookup"><span data-stu-id="52832-197">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="52832-198">ID</span><span class="sxs-lookup"><span data-stu-id="52832-198">ID</span></span>             | <span data-ttu-id="52832-199">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="52832-199">URL</span></span>    | <span data-ttu-id="52832-200">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="52832-200">string</span></span> | <span data-ttu-id="52832-201">Ano</span><span class="sxs-lookup"><span data-stu-id="52832-201">yes</span></span>      | <span data-ttu-id="52832-202">ID balíčku, který se má relist</span><span class="sxs-lookup"><span data-stu-id="52832-202">The ID of the package to relist</span></span>
<span data-ttu-id="52832-203">VERZE</span><span class="sxs-lookup"><span data-stu-id="52832-203">VERSION</span></span>        | <span data-ttu-id="52832-204">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="52832-204">URL</span></span>    | <span data-ttu-id="52832-205">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="52832-205">string</span></span> | <span data-ttu-id="52832-206">Ano</span><span class="sxs-lookup"><span data-stu-id="52832-206">yes</span></span>      | <span data-ttu-id="52832-207">Verze balíčku, který se relist</span><span class="sxs-lookup"><span data-stu-id="52832-207">The version of the package to relist</span></span>
<span data-ttu-id="52832-208">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="52832-208">X-NuGet-ApiKey</span></span> | <span data-ttu-id="52832-209">Záhlaví</span><span class="sxs-lookup"><span data-stu-id="52832-209">Header</span></span> | <span data-ttu-id="52832-210">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="52832-210">string</span></span> | <span data-ttu-id="52832-211">Ano</span><span class="sxs-lookup"><span data-stu-id="52832-211">yes</span></span>      | <span data-ttu-id="52832-212">Třeba `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="52832-212">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="52832-213">Odpověď</span><span class="sxs-lookup"><span data-stu-id="52832-213">Response</span></span>

<span data-ttu-id="52832-214">Stavový kód</span><span class="sxs-lookup"><span data-stu-id="52832-214">Status Code</span></span> | <span data-ttu-id="52832-215">Význam</span><span class="sxs-lookup"><span data-stu-id="52832-215">Meaning</span></span>
----------- | -------
<span data-ttu-id="52832-216">200</span><span class="sxs-lookup"><span data-stu-id="52832-216">200</span></span>         | <span data-ttu-id="52832-217">Balíček je nyní uveden.</span><span class="sxs-lookup"><span data-stu-id="52832-217">The package is now listed</span></span>
<span data-ttu-id="52832-218">404</span><span class="sxs-lookup"><span data-stu-id="52832-218">404</span></span>         | <span data-ttu-id="52832-219">Žádný balíček pomocí zadaných `ID` a `VERSION` existuje</span><span class="sxs-lookup"><span data-stu-id="52832-219">No package with the provided `ID` and `VERSION` exists</span></span>
