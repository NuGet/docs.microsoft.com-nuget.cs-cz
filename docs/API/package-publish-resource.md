---
title: "Push a odstranit, NuGet rozhraní API | Microsoft Docs"
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
ms.assetid: 1eaa403a-5c13-4c05-9352-2f791b98aa7e
description: "Služba publikování umožňuje klientům publikování nové balíčky a unlist nebo odstranit existující balíčky."
keywords: "Nabízené balíček NuGet rozhraní API, rozhraní API NuGet odstranit balíček NuGet API unlist balíčku, nahrajte balíček NuGet rozhraní API, rozhraní API NuGet vytvořit balíček"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 87970a701c63bce2b74c619069ec1d231ea77ab5
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/05/2018
---
# <a name="push-and-delete"></a><span data-ttu-id="6e030-104">Push a odstranění</span><span class="sxs-lookup"><span data-stu-id="6e030-104">Push and Delete</span></span>

<span data-ttu-id="6e030-105">Je možné push, odstraníte (nebo unlist, v závislosti na implementaci serveru) a relist balíčky pomocí rozhraní API V3 NuGet.</span><span class="sxs-lookup"><span data-stu-id="6e030-105">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="6e030-106">Tyto operace jsou na základě odhlásit z `PackagePublish` v nalezen prostředek [indexu služby](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="6e030-106">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="6e030-107">Správa verzí</span><span class="sxs-lookup"><span data-stu-id="6e030-107">Versioning</span></span>

<span data-ttu-id="6e030-108">Následující `@type` hodnota se používá:</span><span class="sxs-lookup"><span data-stu-id="6e030-108">The following `@type` value is used:</span></span>

<span data-ttu-id="6e030-109">@typeHodnota</span><span class="sxs-lookup"><span data-stu-id="6e030-109">@type value</span></span>          | <span data-ttu-id="6e030-110">Poznámky</span><span class="sxs-lookup"><span data-stu-id="6e030-110">Notes</span></span>
-------------------- | -----
<span data-ttu-id="6e030-111">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="6e030-111">PackagePublish/2.0.0</span></span> | <span data-ttu-id="6e030-112">Původní verze</span><span class="sxs-lookup"><span data-stu-id="6e030-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="6e030-113">Základní adresu URL</span><span class="sxs-lookup"><span data-stu-id="6e030-113">Base URL</span></span>

<span data-ttu-id="6e030-114">Základní adresu URL pro následující rozhraní API je hodnota `@id` vlastnost `PackagePublish/2.0.0` prostředků ve zdroji balíčků [indexu služby](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="6e030-114">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="6e030-115">Adresa URL nuget.org v dokumentaci je použita.</span><span class="sxs-lookup"><span data-stu-id="6e030-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="6e030-116">Vezměte v úvahu `https://www.nuget.org/api/v2/package` jako zástupný symbol pro `@id` nalezena hodnota v indexu služby.</span><span class="sxs-lookup"><span data-stu-id="6e030-116">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="6e030-117">Všimněte si, že tato adresa URL odkazuje do stejného umístění jako starší verze koncový bod nabízené V2 vzhledem k tomu, že protokol je stejný.</span><span class="sxs-lookup"><span data-stu-id="6e030-117">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="6e030-118">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="6e030-118">HTTP methods</span></span>

<span data-ttu-id="6e030-119">`PUT`, `POST` a `DELETE` metody HTTP podporuje tento prostředek.</span><span class="sxs-lookup"><span data-stu-id="6e030-119">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="6e030-120">Které metody jsou podporovány na každém koncovém bodu najdete níže.</span><span class="sxs-lookup"><span data-stu-id="6e030-120">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="6e030-121">Push balíčku</span><span class="sxs-lookup"><span data-stu-id="6e030-121">Push a package</span></span>

> [!Note]
> <span data-ttu-id="6e030-122">má nuget.org [další požadavky](NuGet-Protocols.md) pro interakci s koncovým bodem push.</span><span class="sxs-lookup"><span data-stu-id="6e030-122">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="6e030-123">nuget.org podporuje vkládání nové balíčky pomocí následující rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="6e030-123">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="6e030-124">Pokud balíček s zadané ID a verzí již existuje, odmítnou nuget.org nabízeného oznámení.</span><span class="sxs-lookup"><span data-stu-id="6e030-124">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="6e030-125">Další zdroje balíčku může podporovat nahrazování existujícího balíčku.</span><span class="sxs-lookup"><span data-stu-id="6e030-125">Other package sources may support replacing an existing package.</span></span>

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a><span data-ttu-id="6e030-126">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="6e030-126">Request parameters</span></span>

<span data-ttu-id="6e030-127">Název</span><span class="sxs-lookup"><span data-stu-id="6e030-127">Name</span></span>           | <span data-ttu-id="6e030-128">V</span><span class="sxs-lookup"><span data-stu-id="6e030-128">In</span></span>     | <span data-ttu-id="6e030-129">Typ</span><span class="sxs-lookup"><span data-stu-id="6e030-129">Type</span></span>   | <span data-ttu-id="6e030-130">Požadováno</span><span class="sxs-lookup"><span data-stu-id="6e030-130">Required</span></span> | <span data-ttu-id="6e030-131">Poznámky</span><span class="sxs-lookup"><span data-stu-id="6e030-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="6e030-132">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="6e030-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="6e030-133">Záhlaví</span><span class="sxs-lookup"><span data-stu-id="6e030-133">Header</span></span> | <span data-ttu-id="6e030-134">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="6e030-134">string</span></span> | <span data-ttu-id="6e030-135">Ano</span><span class="sxs-lookup"><span data-stu-id="6e030-135">yes</span></span>      | <span data-ttu-id="6e030-136">Třeba `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="6e030-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="6e030-137">Klíč rozhraní API je neprůhledný řetězec, že podmínky ze zdroje balíčků uživatelem a nakonfigurované do klienta.</span><span class="sxs-lookup"><span data-stu-id="6e030-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="6e030-138">Je vyžadováno žádné konkrétní řetězec formátu, ale nesmí překročit délka klíč rozhraní API přiměřené velikosti pro hodnoty hlavičky protokolu HTTP.</span><span class="sxs-lookup"><span data-stu-id="6e030-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="6e030-139">Text žádosti</span><span class="sxs-lookup"><span data-stu-id="6e030-139">Request body</span></span>

<span data-ttu-id="6e030-140">Textu požadavku musí pocházet v následující podobě:</span><span class="sxs-lookup"><span data-stu-id="6e030-140">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="6e030-141">Dat vícedílného formuláře</span><span class="sxs-lookup"><span data-stu-id="6e030-141">Multipart form data</span></span>

<span data-ttu-id="6e030-142">Hlavička požadavku `Content-Type` je `multipart/form-data` a první položky v těle žádosti je nezpracované bajtů .nupkg se instaluje.</span><span class="sxs-lookup"><span data-stu-id="6e030-142">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="6e030-143">Následující položky v textu vícedílné zprávy se ignorují.</span><span class="sxs-lookup"><span data-stu-id="6e030-143">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="6e030-144">Název souboru nebo jiné záhlaví položek s více částmi se ignorují.</span><span class="sxs-lookup"><span data-stu-id="6e030-144">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="6e030-145">Odpověď</span><span class="sxs-lookup"><span data-stu-id="6e030-145">Response</span></span>

<span data-ttu-id="6e030-146">Stavový kód</span><span class="sxs-lookup"><span data-stu-id="6e030-146">Status Code</span></span> | <span data-ttu-id="6e030-147">Význam</span><span class="sxs-lookup"><span data-stu-id="6e030-147">Meaning</span></span>
----------- | -------
<span data-ttu-id="6e030-148">201, 202</span><span class="sxs-lookup"><span data-stu-id="6e030-148">201, 202</span></span>    | <span data-ttu-id="6e030-149">Balíček byl úspěšně poslat.</span><span class="sxs-lookup"><span data-stu-id="6e030-149">The package was successfully pushed</span></span>
<span data-ttu-id="6e030-150">400</span><span class="sxs-lookup"><span data-stu-id="6e030-150">400</span></span>         | <span data-ttu-id="6e030-151">Zadaný balíček je neplatná</span><span class="sxs-lookup"><span data-stu-id="6e030-151">The provided package is invalid</span></span>
<span data-ttu-id="6e030-152">409</span><span class="sxs-lookup"><span data-stu-id="6e030-152">409</span></span>         | <span data-ttu-id="6e030-153">Balíček s zadané ID a verzí již existuje.</span><span class="sxs-lookup"><span data-stu-id="6e030-153">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="6e030-154">Implementace serveru lišit vráceny v případě, že balíček je úspěšně nabídnutých úspěch stavový kód.</span><span class="sxs-lookup"><span data-stu-id="6e030-154">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="6e030-155">Odstranění balíčku</span><span class="sxs-lookup"><span data-stu-id="6e030-155">Delete a package</span></span>

<span data-ttu-id="6e030-156">nuget.org interpretuje požadavku na odstranění balíčku jako na "unlist".</span><span class="sxs-lookup"><span data-stu-id="6e030-156">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="6e030-157">To znamená, že balíček je stále k dispozici pro existující příjemce balíčku, ale balíček už se zobrazí ve výsledcích hledání nebo webové rozhraní.</span><span class="sxs-lookup"><span data-stu-id="6e030-157">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="6e030-158">Další informace o tento postup najdete v tématu [odstranit balíčky](../policies/deleting-packages.md) zásad.</span><span class="sxs-lookup"><span data-stu-id="6e030-158">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="6e030-159">Jiných implementacích serveru jsou volně interpretovat jako pevný odstranění tohoto signálu, soft odstranit nebo unlist.</span><span class="sxs-lookup"><span data-stu-id="6e030-159">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="6e030-160">Například [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (implementaci serveru pouze podpora starší API V2) podporuje zpracování této žádosti jako unlist nebo pevné odstranění podle možnosti konfigurace.</span><span class="sxs-lookup"><span data-stu-id="6e030-160">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="6e030-161">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="6e030-161">Request parameters</span></span>

<span data-ttu-id="6e030-162">Název</span><span class="sxs-lookup"><span data-stu-id="6e030-162">Name</span></span>           | <span data-ttu-id="6e030-163">V</span><span class="sxs-lookup"><span data-stu-id="6e030-163">In</span></span>     | <span data-ttu-id="6e030-164">Typ</span><span class="sxs-lookup"><span data-stu-id="6e030-164">Type</span></span>   | <span data-ttu-id="6e030-165">Požadováno</span><span class="sxs-lookup"><span data-stu-id="6e030-165">Required</span></span> | <span data-ttu-id="6e030-166">Poznámky</span><span class="sxs-lookup"><span data-stu-id="6e030-166">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="6e030-167">ID</span><span class="sxs-lookup"><span data-stu-id="6e030-167">ID</span></span>             | <span data-ttu-id="6e030-168">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="6e030-168">URL</span></span>    | <span data-ttu-id="6e030-169">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="6e030-169">string</span></span> | <span data-ttu-id="6e030-170">Ano</span><span class="sxs-lookup"><span data-stu-id="6e030-170">yes</span></span>      | <span data-ttu-id="6e030-171">ID balíčku se má odstranit</span><span class="sxs-lookup"><span data-stu-id="6e030-171">The ID of the package to delete</span></span>
<span data-ttu-id="6e030-172">VERZE</span><span class="sxs-lookup"><span data-stu-id="6e030-172">VERSION</span></span>        | <span data-ttu-id="6e030-173">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="6e030-173">URL</span></span>    | <span data-ttu-id="6e030-174">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="6e030-174">string</span></span> | <span data-ttu-id="6e030-175">Ano</span><span class="sxs-lookup"><span data-stu-id="6e030-175">yes</span></span>      | <span data-ttu-id="6e030-176">Verze balíčku odstranit</span><span class="sxs-lookup"><span data-stu-id="6e030-176">The version of the package to delete</span></span>
<span data-ttu-id="6e030-177">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="6e030-177">X-NuGet-ApiKey</span></span> | <span data-ttu-id="6e030-178">Záhlaví</span><span class="sxs-lookup"><span data-stu-id="6e030-178">Header</span></span> | <span data-ttu-id="6e030-179">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="6e030-179">string</span></span> | <span data-ttu-id="6e030-180">Ano</span><span class="sxs-lookup"><span data-stu-id="6e030-180">yes</span></span>      | <span data-ttu-id="6e030-181">Třeba `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="6e030-181">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="6e030-182">Odpověď</span><span class="sxs-lookup"><span data-stu-id="6e030-182">Response</span></span>

<span data-ttu-id="6e030-183">Stavový kód</span><span class="sxs-lookup"><span data-stu-id="6e030-183">Status Code</span></span> | <span data-ttu-id="6e030-184">Význam</span><span class="sxs-lookup"><span data-stu-id="6e030-184">Meaning</span></span>
----------- | -------
<span data-ttu-id="6e030-185">204</span><span class="sxs-lookup"><span data-stu-id="6e030-185">204</span></span>         | <span data-ttu-id="6e030-186">Balíček byl odstraněn.</span><span class="sxs-lookup"><span data-stu-id="6e030-186">The package was deleted</span></span>
<span data-ttu-id="6e030-187">404</span><span class="sxs-lookup"><span data-stu-id="6e030-187">404</span></span>         | <span data-ttu-id="6e030-188">Žádný balíček poskytnutým `ID` a `VERSION` existuje</span><span class="sxs-lookup"><span data-stu-id="6e030-188">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="6e030-189">Relist balíčku</span><span class="sxs-lookup"><span data-stu-id="6e030-189">Relist a package</span></span>

<span data-ttu-id="6e030-190">Pokud je balíček neuvedené, je možné vytvořit tento balíček opět viditelné ve výsledcích hledání používá koncový bod "relist".</span><span class="sxs-lookup"><span data-stu-id="6e030-190">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="6e030-191">Tento koncový bod má stejné tvar jako [odstranit (unlist) koncový bod](#delete-a-package) ale používá `POST` metoda HTTP místo `DELETE` metoda.</span><span class="sxs-lookup"><span data-stu-id="6e030-191">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="6e030-192">Pokud už je balíček uvedený, stále neproběhne.</span><span class="sxs-lookup"><span data-stu-id="6e030-192">If the package is already listed, the request still succeeds.</span></span>

```
POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="6e030-193">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="6e030-193">Request parameters</span></span>

<span data-ttu-id="6e030-194">Název</span><span class="sxs-lookup"><span data-stu-id="6e030-194">Name</span></span>           | <span data-ttu-id="6e030-195">V</span><span class="sxs-lookup"><span data-stu-id="6e030-195">In</span></span>     | <span data-ttu-id="6e030-196">Typ</span><span class="sxs-lookup"><span data-stu-id="6e030-196">Type</span></span>   | <span data-ttu-id="6e030-197">Požadováno</span><span class="sxs-lookup"><span data-stu-id="6e030-197">Required</span></span> | <span data-ttu-id="6e030-198">Poznámky</span><span class="sxs-lookup"><span data-stu-id="6e030-198">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="6e030-199">ID</span><span class="sxs-lookup"><span data-stu-id="6e030-199">ID</span></span>             | <span data-ttu-id="6e030-200">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="6e030-200">URL</span></span>    | <span data-ttu-id="6e030-201">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="6e030-201">string</span></span> | <span data-ttu-id="6e030-202">Ano</span><span class="sxs-lookup"><span data-stu-id="6e030-202">yes</span></span>      | <span data-ttu-id="6e030-203">ID balíčku má relist</span><span class="sxs-lookup"><span data-stu-id="6e030-203">The ID of the package to relist</span></span>
<span data-ttu-id="6e030-204">VERZE</span><span class="sxs-lookup"><span data-stu-id="6e030-204">VERSION</span></span>        | <span data-ttu-id="6e030-205">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="6e030-205">URL</span></span>    | <span data-ttu-id="6e030-206">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="6e030-206">string</span></span> | <span data-ttu-id="6e030-207">Ano</span><span class="sxs-lookup"><span data-stu-id="6e030-207">yes</span></span>      | <span data-ttu-id="6e030-208">Verze balíčku, který má relist</span><span class="sxs-lookup"><span data-stu-id="6e030-208">The version of the package to relist</span></span>
<span data-ttu-id="6e030-209">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="6e030-209">X-NuGet-ApiKey</span></span> | <span data-ttu-id="6e030-210">Záhlaví</span><span class="sxs-lookup"><span data-stu-id="6e030-210">Header</span></span> | <span data-ttu-id="6e030-211">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="6e030-211">string</span></span> | <span data-ttu-id="6e030-212">Ano</span><span class="sxs-lookup"><span data-stu-id="6e030-212">yes</span></span>      | <span data-ttu-id="6e030-213">Třeba `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="6e030-213">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="6e030-214">Odpověď</span><span class="sxs-lookup"><span data-stu-id="6e030-214">Response</span></span>

<span data-ttu-id="6e030-215">Stavový kód</span><span class="sxs-lookup"><span data-stu-id="6e030-215">Status Code</span></span> | <span data-ttu-id="6e030-216">Význam</span><span class="sxs-lookup"><span data-stu-id="6e030-216">Meaning</span></span>
----------- | -------
<span data-ttu-id="6e030-217">204</span><span class="sxs-lookup"><span data-stu-id="6e030-217">204</span></span>         | <span data-ttu-id="6e030-218">Balíček je nyní obsažena.</span><span class="sxs-lookup"><span data-stu-id="6e030-218">The package is now listed</span></span>
<span data-ttu-id="6e030-219">404</span><span class="sxs-lookup"><span data-stu-id="6e030-219">404</span></span>         | <span data-ttu-id="6e030-220">Žádný balíček poskytnutým `ID` a `VERSION` existuje</span><span class="sxs-lookup"><span data-stu-id="6e030-220">No package with the provided `ID` and `VERSION` exists</span></span>
