---
title: Push a odstranit, NuGet rozhraní API
description: Služba publikování umožňuje klientům publikování nové balíčky a unlist nebo odstranit existující balíčky.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 911c8238624f806b1fbb5c7938d02b6bdfbd8614
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
---
# <a name="push-and-delete"></a><span data-ttu-id="522f4-103">Push a odstranění</span><span class="sxs-lookup"><span data-stu-id="522f4-103">Push and Delete</span></span>

<span data-ttu-id="522f4-104">Je možné push, odstraníte (nebo unlist, v závislosti na implementaci serveru) a relist balíčky pomocí rozhraní API V3 NuGet.</span><span class="sxs-lookup"><span data-stu-id="522f4-104">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="522f4-105">Tyto operace jsou na základě odhlásit z `PackagePublish` v nalezen prostředek [indexu služby](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="522f4-105">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="522f4-106">Správa verzí</span><span class="sxs-lookup"><span data-stu-id="522f4-106">Versioning</span></span>

<span data-ttu-id="522f4-107">Následující `@type` hodnota se používá:</span><span class="sxs-lookup"><span data-stu-id="522f4-107">The following `@type` value is used:</span></span>

<span data-ttu-id="522f4-108">@type Hodnota</span><span class="sxs-lookup"><span data-stu-id="522f4-108">@type value</span></span>          | <span data-ttu-id="522f4-109">Poznámky</span><span class="sxs-lookup"><span data-stu-id="522f4-109">Notes</span></span>
-------------------- | -----
<span data-ttu-id="522f4-110">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="522f4-110">PackagePublish/2.0.0</span></span> | <span data-ttu-id="522f4-111">Původní verze</span><span class="sxs-lookup"><span data-stu-id="522f4-111">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="522f4-112">Základní adresu URL</span><span class="sxs-lookup"><span data-stu-id="522f4-112">Base URL</span></span>

<span data-ttu-id="522f4-113">Základní adresu URL pro následující rozhraní API je hodnota `@id` vlastnost `PackagePublish/2.0.0` prostředků ve zdroji balíčků [indexu služby](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="522f4-113">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="522f4-114">Adresa URL nuget.org v dokumentaci je použita.</span><span class="sxs-lookup"><span data-stu-id="522f4-114">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="522f4-115">Vezměte v úvahu `https://www.nuget.org/api/v2/package` jako zástupný symbol pro `@id` nalezena hodnota v indexu služby.</span><span class="sxs-lookup"><span data-stu-id="522f4-115">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="522f4-116">Všimněte si, že tato adresa URL odkazuje do stejného umístění jako starší verze koncový bod nabízené V2 vzhledem k tomu, že protokol je stejný.</span><span class="sxs-lookup"><span data-stu-id="522f4-116">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="522f4-117">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="522f4-117">HTTP methods</span></span>

<span data-ttu-id="522f4-118">`PUT`, `POST` a `DELETE` metody HTTP podporuje tento prostředek.</span><span class="sxs-lookup"><span data-stu-id="522f4-118">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="522f4-119">Které metody jsou podporovány na každém koncovém bodu najdete níže.</span><span class="sxs-lookup"><span data-stu-id="522f4-119">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="522f4-120">Push balíčku</span><span class="sxs-lookup"><span data-stu-id="522f4-120">Push a package</span></span>

> [!Note]
> <span data-ttu-id="522f4-121">má nuget.org [další požadavky](NuGet-Protocols.md) pro interakci s koncovým bodem push.</span><span class="sxs-lookup"><span data-stu-id="522f4-121">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="522f4-122">nuget.org podporuje vkládání nové balíčky pomocí následující rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="522f4-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="522f4-123">Pokud balíček s zadané ID a verzí již existuje, odmítnou nuget.org nabízeného oznámení.</span><span class="sxs-lookup"><span data-stu-id="522f4-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="522f4-124">Další zdroje balíčku může podporovat nahrazování existujícího balíčku.</span><span class="sxs-lookup"><span data-stu-id="522f4-124">Other package sources may support replacing an existing package.</span></span>

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a><span data-ttu-id="522f4-125">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="522f4-125">Request parameters</span></span>

<span data-ttu-id="522f4-126">Název</span><span class="sxs-lookup"><span data-stu-id="522f4-126">Name</span></span>           | <span data-ttu-id="522f4-127">V</span><span class="sxs-lookup"><span data-stu-id="522f4-127">In</span></span>     | <span data-ttu-id="522f4-128">Typ</span><span class="sxs-lookup"><span data-stu-id="522f4-128">Type</span></span>   | <span data-ttu-id="522f4-129">Požadováno</span><span class="sxs-lookup"><span data-stu-id="522f4-129">Required</span></span> | <span data-ttu-id="522f4-130">Poznámky</span><span class="sxs-lookup"><span data-stu-id="522f4-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="522f4-131">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="522f4-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="522f4-132">Záhlaví</span><span class="sxs-lookup"><span data-stu-id="522f4-132">Header</span></span> | <span data-ttu-id="522f4-133">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="522f4-133">string</span></span> | <span data-ttu-id="522f4-134">Ano</span><span class="sxs-lookup"><span data-stu-id="522f4-134">yes</span></span>      | <span data-ttu-id="522f4-135">Třeba `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="522f4-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="522f4-136">Klíč rozhraní API je neprůhledný řetězec, že podmínky ze zdroje balíčků uživatelem a nakonfigurované do klienta.</span><span class="sxs-lookup"><span data-stu-id="522f4-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="522f4-137">Je vyžadováno žádné konkrétní řetězec formátu, ale nesmí překročit délka klíč rozhraní API přiměřené velikosti pro hodnoty hlavičky protokolu HTTP.</span><span class="sxs-lookup"><span data-stu-id="522f4-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="522f4-138">Text žádosti</span><span class="sxs-lookup"><span data-stu-id="522f4-138">Request body</span></span>

<span data-ttu-id="522f4-139">Textu požadavku musí pocházet v následující podobě:</span><span class="sxs-lookup"><span data-stu-id="522f4-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="522f4-140">Dat vícedílného formuláře</span><span class="sxs-lookup"><span data-stu-id="522f4-140">Multipart form data</span></span>

<span data-ttu-id="522f4-141">Hlavička požadavku `Content-Type` je `multipart/form-data` a první položky v těle žádosti je nezpracované bajtů .nupkg se instaluje.</span><span class="sxs-lookup"><span data-stu-id="522f4-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="522f4-142">Následující položky v textu vícedílné zprávy se ignorují.</span><span class="sxs-lookup"><span data-stu-id="522f4-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="522f4-143">Název souboru nebo jiné záhlaví položek s více částmi se ignorují.</span><span class="sxs-lookup"><span data-stu-id="522f4-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="522f4-144">Odpověď</span><span class="sxs-lookup"><span data-stu-id="522f4-144">Response</span></span>

<span data-ttu-id="522f4-145">Stavový kód</span><span class="sxs-lookup"><span data-stu-id="522f4-145">Status Code</span></span> | <span data-ttu-id="522f4-146">Význam</span><span class="sxs-lookup"><span data-stu-id="522f4-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="522f4-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="522f4-147">201, 202</span></span>    | <span data-ttu-id="522f4-148">Balíček byl úspěšně poslat.</span><span class="sxs-lookup"><span data-stu-id="522f4-148">The package was successfully pushed</span></span>
<span data-ttu-id="522f4-149">400</span><span class="sxs-lookup"><span data-stu-id="522f4-149">400</span></span>         | <span data-ttu-id="522f4-150">Zadaný balíček je neplatná</span><span class="sxs-lookup"><span data-stu-id="522f4-150">The provided package is invalid</span></span>
<span data-ttu-id="522f4-151">409</span><span class="sxs-lookup"><span data-stu-id="522f4-151">409</span></span>         | <span data-ttu-id="522f4-152">Balíček s zadané ID a verzí již existuje.</span><span class="sxs-lookup"><span data-stu-id="522f4-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="522f4-153">Implementace serveru lišit vráceny v případě, že balíček je úspěšně nabídnutých úspěch stavový kód.</span><span class="sxs-lookup"><span data-stu-id="522f4-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="522f4-154">Odstranění balíčku</span><span class="sxs-lookup"><span data-stu-id="522f4-154">Delete a package</span></span>

<span data-ttu-id="522f4-155">nuget.org interpretuje požadavku na odstranění balíčku jako na "unlist".</span><span class="sxs-lookup"><span data-stu-id="522f4-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="522f4-156">To znamená, že balíček je stále k dispozici pro existující příjemce balíčku, ale balíček už se zobrazí ve výsledcích hledání nebo webové rozhraní.</span><span class="sxs-lookup"><span data-stu-id="522f4-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="522f4-157">Další informace o tento postup najdete v tématu [odstranit balíčky](../policies/deleting-packages.md) zásad.</span><span class="sxs-lookup"><span data-stu-id="522f4-157">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="522f4-158">Jiných implementacích serveru jsou volně interpretovat jako pevný odstranění tohoto signálu, soft odstranit nebo unlist.</span><span class="sxs-lookup"><span data-stu-id="522f4-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="522f4-159">Například [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (implementaci serveru pouze podpora starší API V2) podporuje zpracování této žádosti jako unlist nebo pevné odstranění podle možnosti konfigurace.</span><span class="sxs-lookup"><span data-stu-id="522f4-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="522f4-160">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="522f4-160">Request parameters</span></span>

<span data-ttu-id="522f4-161">Název</span><span class="sxs-lookup"><span data-stu-id="522f4-161">Name</span></span>           | <span data-ttu-id="522f4-162">V</span><span class="sxs-lookup"><span data-stu-id="522f4-162">In</span></span>     | <span data-ttu-id="522f4-163">Typ</span><span class="sxs-lookup"><span data-stu-id="522f4-163">Type</span></span>   | <span data-ttu-id="522f4-164">Požadováno</span><span class="sxs-lookup"><span data-stu-id="522f4-164">Required</span></span> | <span data-ttu-id="522f4-165">Poznámky</span><span class="sxs-lookup"><span data-stu-id="522f4-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="522f4-166">ID</span><span class="sxs-lookup"><span data-stu-id="522f4-166">ID</span></span>             | <span data-ttu-id="522f4-167">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="522f4-167">URL</span></span>    | <span data-ttu-id="522f4-168">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="522f4-168">string</span></span> | <span data-ttu-id="522f4-169">Ano</span><span class="sxs-lookup"><span data-stu-id="522f4-169">yes</span></span>      | <span data-ttu-id="522f4-170">ID balíčku se má odstranit</span><span class="sxs-lookup"><span data-stu-id="522f4-170">The ID of the package to delete</span></span>
<span data-ttu-id="522f4-171">VERZE</span><span class="sxs-lookup"><span data-stu-id="522f4-171">VERSION</span></span>        | <span data-ttu-id="522f4-172">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="522f4-172">URL</span></span>    | <span data-ttu-id="522f4-173">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="522f4-173">string</span></span> | <span data-ttu-id="522f4-174">Ano</span><span class="sxs-lookup"><span data-stu-id="522f4-174">yes</span></span>      | <span data-ttu-id="522f4-175">Verze balíčku odstranit</span><span class="sxs-lookup"><span data-stu-id="522f4-175">The version of the package to delete</span></span>
<span data-ttu-id="522f4-176">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="522f4-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="522f4-177">Záhlaví</span><span class="sxs-lookup"><span data-stu-id="522f4-177">Header</span></span> | <span data-ttu-id="522f4-178">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="522f4-178">string</span></span> | <span data-ttu-id="522f4-179">Ano</span><span class="sxs-lookup"><span data-stu-id="522f4-179">yes</span></span>      | <span data-ttu-id="522f4-180">Třeba `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="522f4-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="522f4-181">Odpověď</span><span class="sxs-lookup"><span data-stu-id="522f4-181">Response</span></span>

<span data-ttu-id="522f4-182">Stavový kód</span><span class="sxs-lookup"><span data-stu-id="522f4-182">Status Code</span></span> | <span data-ttu-id="522f4-183">Význam</span><span class="sxs-lookup"><span data-stu-id="522f4-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="522f4-184">204</span><span class="sxs-lookup"><span data-stu-id="522f4-184">204</span></span>         | <span data-ttu-id="522f4-185">Balíček byl odstraněn.</span><span class="sxs-lookup"><span data-stu-id="522f4-185">The package was deleted</span></span>
<span data-ttu-id="522f4-186">404</span><span class="sxs-lookup"><span data-stu-id="522f4-186">404</span></span>         | <span data-ttu-id="522f4-187">Žádný balíček poskytnutým `ID` a `VERSION` existuje</span><span class="sxs-lookup"><span data-stu-id="522f4-187">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="522f4-188">Relist balíčku</span><span class="sxs-lookup"><span data-stu-id="522f4-188">Relist a package</span></span>

<span data-ttu-id="522f4-189">Pokud je balíček neuvedené, je možné vytvořit tento balíček opět viditelné ve výsledcích hledání používá koncový bod "relist".</span><span class="sxs-lookup"><span data-stu-id="522f4-189">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="522f4-190">Tento koncový bod má stejné tvar jako [odstranit (unlist) koncový bod](#delete-a-package) ale používá `POST` metoda HTTP místo `DELETE` metoda.</span><span class="sxs-lookup"><span data-stu-id="522f4-190">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="522f4-191">Pokud už je balíček uvedený, stále neproběhne.</span><span class="sxs-lookup"><span data-stu-id="522f4-191">If the package is already listed, the request still succeeds.</span></span>

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="522f4-192">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="522f4-192">Request parameters</span></span>

<span data-ttu-id="522f4-193">Název</span><span class="sxs-lookup"><span data-stu-id="522f4-193">Name</span></span>           | <span data-ttu-id="522f4-194">V</span><span class="sxs-lookup"><span data-stu-id="522f4-194">In</span></span>     | <span data-ttu-id="522f4-195">Typ</span><span class="sxs-lookup"><span data-stu-id="522f4-195">Type</span></span>   | <span data-ttu-id="522f4-196">Požadováno</span><span class="sxs-lookup"><span data-stu-id="522f4-196">Required</span></span> | <span data-ttu-id="522f4-197">Poznámky</span><span class="sxs-lookup"><span data-stu-id="522f4-197">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="522f4-198">ID</span><span class="sxs-lookup"><span data-stu-id="522f4-198">ID</span></span>             | <span data-ttu-id="522f4-199">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="522f4-199">URL</span></span>    | <span data-ttu-id="522f4-200">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="522f4-200">string</span></span> | <span data-ttu-id="522f4-201">Ano</span><span class="sxs-lookup"><span data-stu-id="522f4-201">yes</span></span>      | <span data-ttu-id="522f4-202">ID balíčku má relist</span><span class="sxs-lookup"><span data-stu-id="522f4-202">The ID of the package to relist</span></span>
<span data-ttu-id="522f4-203">VERZE</span><span class="sxs-lookup"><span data-stu-id="522f4-203">VERSION</span></span>        | <span data-ttu-id="522f4-204">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="522f4-204">URL</span></span>    | <span data-ttu-id="522f4-205">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="522f4-205">string</span></span> | <span data-ttu-id="522f4-206">Ano</span><span class="sxs-lookup"><span data-stu-id="522f4-206">yes</span></span>      | <span data-ttu-id="522f4-207">Verze balíčku, který má relist</span><span class="sxs-lookup"><span data-stu-id="522f4-207">The version of the package to relist</span></span>
<span data-ttu-id="522f4-208">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="522f4-208">X-NuGet-ApiKey</span></span> | <span data-ttu-id="522f4-209">Záhlaví</span><span class="sxs-lookup"><span data-stu-id="522f4-209">Header</span></span> | <span data-ttu-id="522f4-210">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="522f4-210">string</span></span> | <span data-ttu-id="522f4-211">Ano</span><span class="sxs-lookup"><span data-stu-id="522f4-211">yes</span></span>      | <span data-ttu-id="522f4-212">Třeba `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="522f4-212">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="522f4-213">Odpověď</span><span class="sxs-lookup"><span data-stu-id="522f4-213">Response</span></span>

<span data-ttu-id="522f4-214">Stavový kód</span><span class="sxs-lookup"><span data-stu-id="522f4-214">Status Code</span></span> | <span data-ttu-id="522f4-215">Význam</span><span class="sxs-lookup"><span data-stu-id="522f4-215">Meaning</span></span>
----------- | -------
<span data-ttu-id="522f4-216">200</span><span class="sxs-lookup"><span data-stu-id="522f4-216">200</span></span>         | <span data-ttu-id="522f4-217">Balíček je nyní obsažena.</span><span class="sxs-lookup"><span data-stu-id="522f4-217">The package is now listed</span></span>
<span data-ttu-id="522f4-218">404</span><span class="sxs-lookup"><span data-stu-id="522f4-218">404</span></span>         | <span data-ttu-id="522f4-219">Žádný balíček poskytnutým `ID` a `VERSION` existuje</span><span class="sxs-lookup"><span data-stu-id="522f4-219">No package with the provided `ID` and `VERSION` exists</span></span>
