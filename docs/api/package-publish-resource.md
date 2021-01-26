---
title: Nabízení a odstraňování, rozhraní API NuGet
description: Služba publikování umožňuje klientům publikovat nové balíčky a odpisovat nebo odstraňovat existující balíčky.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 0a79266011433d5adc1341a8e250838988c84d13
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773926"
---
# <a name="push-and-delete"></a><span data-ttu-id="1240a-103">Push a DELETE</span><span class="sxs-lookup"><span data-stu-id="1240a-103">Push and Delete</span></span>

<span data-ttu-id="1240a-104">Je možné předávat, odstraňovat (nebo odpisovat) v závislosti na implementaci serveru a přepisovat balíčky pomocí rozhraní NuGet V3 API.</span><span class="sxs-lookup"><span data-stu-id="1240a-104">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="1240a-105">Tyto operace jsou založeny na prostředku, který `PackagePublish` najdete v [indexu služby](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="1240a-105">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="1240a-106">Správa verzí</span><span class="sxs-lookup"><span data-stu-id="1240a-106">Versioning</span></span>

<span data-ttu-id="1240a-107">Použije se následující `@type` hodnota:</span><span class="sxs-lookup"><span data-stu-id="1240a-107">The following `@type` value is used:</span></span>

<span data-ttu-id="1240a-108">@type osa</span><span class="sxs-lookup"><span data-stu-id="1240a-108">@type value</span></span>          | <span data-ttu-id="1240a-109">Poznámky</span><span class="sxs-lookup"><span data-stu-id="1240a-109">Notes</span></span>
-------------------- | -----
<span data-ttu-id="1240a-110">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="1240a-110">PackagePublish/2.0.0</span></span> | <span data-ttu-id="1240a-111">Počáteční verze</span><span class="sxs-lookup"><span data-stu-id="1240a-111">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="1240a-112">Základní adresa URL</span><span class="sxs-lookup"><span data-stu-id="1240a-112">Base URL</span></span>

<span data-ttu-id="1240a-113">Základní adresa URL následujících rozhraní API je hodnota `@id` vlastnosti `PackagePublish/2.0.0` prostředku v [indexu služby](service-index.md)zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="1240a-113">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="1240a-114">Pro dokumentaci níže se používá adresa URL balíčku NuGet. org.</span><span class="sxs-lookup"><span data-stu-id="1240a-114">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="1240a-115">Zvažte možnost `https://www.nuget.org/api/v2/package` použít jako zástupný symbol pro `@id` hodnotu nalezenou v indexu služby.</span><span class="sxs-lookup"><span data-stu-id="1240a-115">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="1240a-116">Všimněte si, že tato adresa URL odkazuje na stejné umístění jako starší verze V2 push Endpoint, protože protokol je stejný.</span><span class="sxs-lookup"><span data-stu-id="1240a-116">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="1240a-117">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="1240a-117">HTTP methods</span></span>

<span data-ttu-id="1240a-118">`PUT`Metody, `POST` a `DELETE` http jsou podporovány tímto prostředkem.</span><span class="sxs-lookup"><span data-stu-id="1240a-118">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="1240a-119">Které metody jsou podporovány u každého koncového bodu, viz níže.</span><span class="sxs-lookup"><span data-stu-id="1240a-119">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="1240a-120">Vložení balíčku</span><span class="sxs-lookup"><span data-stu-id="1240a-120">Push a package</span></span>

> [!Note]
> <span data-ttu-id="1240a-121">nuget.org má [Další požadavky](NuGet-Protocols.md) pro interakci s koncovým bodem push.</span><span class="sxs-lookup"><span data-stu-id="1240a-121">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="1240a-122">nuget.org podporuje vkládání nových balíčků pomocí následujícího rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="1240a-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="1240a-123">Pokud balíček se zadaným ID a verzí již existuje, nuget.org se zamítne.</span><span class="sxs-lookup"><span data-stu-id="1240a-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="1240a-124">Další zdroje balíčků můžou podporovat nahrazení existujícího balíčku.</span><span class="sxs-lookup"><span data-stu-id="1240a-124">Other package sources may support replacing an existing package.</span></span>

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a><span data-ttu-id="1240a-125">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="1240a-125">Request parameters</span></span>

<span data-ttu-id="1240a-126">Name</span><span class="sxs-lookup"><span data-stu-id="1240a-126">Name</span></span>           | <span data-ttu-id="1240a-127">V</span><span class="sxs-lookup"><span data-stu-id="1240a-127">In</span></span>     | <span data-ttu-id="1240a-128">Typ</span><span class="sxs-lookup"><span data-stu-id="1240a-128">Type</span></span>   | <span data-ttu-id="1240a-129">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="1240a-129">Required</span></span> | <span data-ttu-id="1240a-130">Poznámky</span><span class="sxs-lookup"><span data-stu-id="1240a-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="1240a-131">X-NuGet – ApiKey</span><span class="sxs-lookup"><span data-stu-id="1240a-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="1240a-132">Hlavička</span><span class="sxs-lookup"><span data-stu-id="1240a-132">Header</span></span> | <span data-ttu-id="1240a-133">řetězec</span><span class="sxs-lookup"><span data-stu-id="1240a-133">string</span></span> | <span data-ttu-id="1240a-134">ano</span><span class="sxs-lookup"><span data-stu-id="1240a-134">yes</span></span>      | <span data-ttu-id="1240a-135">Například `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="1240a-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="1240a-136">Klíč rozhraní API je neprůhledný řetězec ze zdroje balíčku uživatelem a nakonfigurovaný do klienta.</span><span class="sxs-lookup"><span data-stu-id="1240a-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="1240a-137">Není k dispozici žádný konkrétní formát řetězce, ale délka klíče rozhraní API by neměla překročit rozumnou velikost pro hodnoty hlaviček protokolu HTTP.</span><span class="sxs-lookup"><span data-stu-id="1240a-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="1240a-138">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="1240a-138">Request body</span></span>

<span data-ttu-id="1240a-139">Text žádosti musí být v následujícím tvaru:</span><span class="sxs-lookup"><span data-stu-id="1240a-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="1240a-140">Data formuláře v částech</span><span class="sxs-lookup"><span data-stu-id="1240a-140">Multipart form data</span></span>

<span data-ttu-id="1240a-141">Hlavička požadavku `Content-Type` je `multipart/form-data` a první položkou v textu požadavku jsou nezpracované bajty vloženého. nupkg.</span><span class="sxs-lookup"><span data-stu-id="1240a-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="1240a-142">Následné položky v těle části částmi jsou ignorovány.</span><span class="sxs-lookup"><span data-stu-id="1240a-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="1240a-143">Název souboru nebo jiné hlavičky položek s více částmi jsou ignorovány.</span><span class="sxs-lookup"><span data-stu-id="1240a-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="1240a-144">Odpověď</span><span class="sxs-lookup"><span data-stu-id="1240a-144">Response</span></span>

<span data-ttu-id="1240a-145">Stavový kód</span><span class="sxs-lookup"><span data-stu-id="1240a-145">Status Code</span></span> | <span data-ttu-id="1240a-146">Význam</span><span class="sxs-lookup"><span data-stu-id="1240a-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="1240a-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="1240a-147">201, 202</span></span>    | <span data-ttu-id="1240a-148">Balíček se úspěšně odeslal.</span><span class="sxs-lookup"><span data-stu-id="1240a-148">The package was successfully pushed</span></span>
<span data-ttu-id="1240a-149">400</span><span class="sxs-lookup"><span data-stu-id="1240a-149">400</span></span>         | <span data-ttu-id="1240a-150">Zadaný balíček je neplatný.</span><span class="sxs-lookup"><span data-stu-id="1240a-150">The provided package is invalid</span></span>
<span data-ttu-id="1240a-151">409</span><span class="sxs-lookup"><span data-stu-id="1240a-151">409</span></span>         | <span data-ttu-id="1240a-152">Balíček se zadaným ID a verzí již existuje.</span><span class="sxs-lookup"><span data-stu-id="1240a-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="1240a-153">Implementace serveru se liší v případě úspěšného vložení balíčku v případě, že se vrátí stavový kód úspěchu.</span><span class="sxs-lookup"><span data-stu-id="1240a-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="1240a-154">Odstranění balíčku</span><span class="sxs-lookup"><span data-stu-id="1240a-154">Delete a package</span></span>

<span data-ttu-id="1240a-155">nuget.org interpretuje požadavek na odstranění balíčku jako "unlist".</span><span class="sxs-lookup"><span data-stu-id="1240a-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="1240a-156">To znamená, že balíček je stále k dispozici pro existující uživatele balíčku, ale balíček se již nezobrazuje ve výsledcích hledání nebo ve webovém rozhraní.</span><span class="sxs-lookup"><span data-stu-id="1240a-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="1240a-157">Další informace o tomto postupu najdete v tématu [odstraněné zásady balíčků](../nuget-org/policies/deleting-packages.md) .</span><span class="sxs-lookup"><span data-stu-id="1240a-157">For more information about this practice, see the [Deleted Packages](../nuget-org/policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="1240a-158">Další implementace serveru jsou zdarma k interpretaci tohoto signálu jako pevného odstranění, obnovitelného odstranění nebo oddálení seznamu.</span><span class="sxs-lookup"><span data-stu-id="1240a-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="1240a-159">Například [NuGet. Server](https://www.nuget.org/packages/NuGet.Server) (implementace serveru podporuje jenom starší verze V2 API) podporuje zpracování této žádosti jako buď oddálení, nebo pevné odstranění na základě možnosti konfigurace.</span><span class="sxs-lookup"><span data-stu-id="1240a-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="1240a-160">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="1240a-160">Request parameters</span></span>

<span data-ttu-id="1240a-161">Name</span><span class="sxs-lookup"><span data-stu-id="1240a-161">Name</span></span>           | <span data-ttu-id="1240a-162">V</span><span class="sxs-lookup"><span data-stu-id="1240a-162">In</span></span>     | <span data-ttu-id="1240a-163">Typ</span><span class="sxs-lookup"><span data-stu-id="1240a-163">Type</span></span>   | <span data-ttu-id="1240a-164">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="1240a-164">Required</span></span> | <span data-ttu-id="1240a-165">Poznámky</span><span class="sxs-lookup"><span data-stu-id="1240a-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="1240a-166">ID</span><span class="sxs-lookup"><span data-stu-id="1240a-166">ID</span></span>             | <span data-ttu-id="1240a-167">URL</span><span class="sxs-lookup"><span data-stu-id="1240a-167">URL</span></span>    | <span data-ttu-id="1240a-168">řetězec</span><span class="sxs-lookup"><span data-stu-id="1240a-168">string</span></span> | <span data-ttu-id="1240a-169">ano</span><span class="sxs-lookup"><span data-stu-id="1240a-169">yes</span></span>      | <span data-ttu-id="1240a-170">ID balíčku, který se má odstranit</span><span class="sxs-lookup"><span data-stu-id="1240a-170">The ID of the package to delete</span></span>
<span data-ttu-id="1240a-171">VERZE</span><span class="sxs-lookup"><span data-stu-id="1240a-171">VERSION</span></span>        | <span data-ttu-id="1240a-172">URL</span><span class="sxs-lookup"><span data-stu-id="1240a-172">URL</span></span>    | <span data-ttu-id="1240a-173">řetězec</span><span class="sxs-lookup"><span data-stu-id="1240a-173">string</span></span> | <span data-ttu-id="1240a-174">ano</span><span class="sxs-lookup"><span data-stu-id="1240a-174">yes</span></span>      | <span data-ttu-id="1240a-175">Verze balíčku, který se má odstranit</span><span class="sxs-lookup"><span data-stu-id="1240a-175">The version of the package to delete</span></span>
<span data-ttu-id="1240a-176">X-NuGet – ApiKey</span><span class="sxs-lookup"><span data-stu-id="1240a-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="1240a-177">Hlavička</span><span class="sxs-lookup"><span data-stu-id="1240a-177">Header</span></span> | <span data-ttu-id="1240a-178">řetězec</span><span class="sxs-lookup"><span data-stu-id="1240a-178">string</span></span> | <span data-ttu-id="1240a-179">ano</span><span class="sxs-lookup"><span data-stu-id="1240a-179">yes</span></span>      | <span data-ttu-id="1240a-180">Například `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="1240a-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="1240a-181">Odpověď</span><span class="sxs-lookup"><span data-stu-id="1240a-181">Response</span></span>

<span data-ttu-id="1240a-182">Stavový kód</span><span class="sxs-lookup"><span data-stu-id="1240a-182">Status Code</span></span> | <span data-ttu-id="1240a-183">Význam</span><span class="sxs-lookup"><span data-stu-id="1240a-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="1240a-184">204</span><span class="sxs-lookup"><span data-stu-id="1240a-184">204</span></span>         | <span data-ttu-id="1240a-185">Balíček se odstranil.</span><span class="sxs-lookup"><span data-stu-id="1240a-185">The package was deleted</span></span>
<span data-ttu-id="1240a-186">404</span><span class="sxs-lookup"><span data-stu-id="1240a-186">404</span></span>         | <span data-ttu-id="1240a-187">Žádný balíček se zadaným `ID` a `VERSION` neexistuje.</span><span class="sxs-lookup"><span data-stu-id="1240a-187">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="1240a-188">Přepsání balíčku</span><span class="sxs-lookup"><span data-stu-id="1240a-188">Relist a package</span></span>

<span data-ttu-id="1240a-189">Pokud balíček není v seznamu, je možné ho znovu nastavit tak, aby se zobrazil ve výsledcích hledání pomocí koncového bodu "relist".</span><span class="sxs-lookup"><span data-stu-id="1240a-189">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="1240a-190">Tento koncový bod má stejný tvar jako [koncový bod Delete (unlist)](#delete-a-package) , ale `POST` místo metody používá metodu http `DELETE` .</span><span class="sxs-lookup"><span data-stu-id="1240a-190">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="1240a-191">Pokud je tento balíček již uveden, požadavek bude stále úspěšný.</span><span class="sxs-lookup"><span data-stu-id="1240a-191">If the package is already listed, the request still succeeds.</span></span>

```
POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="1240a-192">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="1240a-192">Request parameters</span></span>

<span data-ttu-id="1240a-193">Name</span><span class="sxs-lookup"><span data-stu-id="1240a-193">Name</span></span>           | <span data-ttu-id="1240a-194">V</span><span class="sxs-lookup"><span data-stu-id="1240a-194">In</span></span>     | <span data-ttu-id="1240a-195">Typ</span><span class="sxs-lookup"><span data-stu-id="1240a-195">Type</span></span>   | <span data-ttu-id="1240a-196">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="1240a-196">Required</span></span> | <span data-ttu-id="1240a-197">Poznámky</span><span class="sxs-lookup"><span data-stu-id="1240a-197">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="1240a-198">ID</span><span class="sxs-lookup"><span data-stu-id="1240a-198">ID</span></span>             | <span data-ttu-id="1240a-199">URL</span><span class="sxs-lookup"><span data-stu-id="1240a-199">URL</span></span>    | <span data-ttu-id="1240a-200">řetězec</span><span class="sxs-lookup"><span data-stu-id="1240a-200">string</span></span> | <span data-ttu-id="1240a-201">ano</span><span class="sxs-lookup"><span data-stu-id="1240a-201">yes</span></span>      | <span data-ttu-id="1240a-202">ID balíčku, který se má znovu zobrazit</span><span class="sxs-lookup"><span data-stu-id="1240a-202">The ID of the package to relist</span></span>
<span data-ttu-id="1240a-203">VERZE</span><span class="sxs-lookup"><span data-stu-id="1240a-203">VERSION</span></span>        | <span data-ttu-id="1240a-204">URL</span><span class="sxs-lookup"><span data-stu-id="1240a-204">URL</span></span>    | <span data-ttu-id="1240a-205">řetězec</span><span class="sxs-lookup"><span data-stu-id="1240a-205">string</span></span> | <span data-ttu-id="1240a-206">ano</span><span class="sxs-lookup"><span data-stu-id="1240a-206">yes</span></span>      | <span data-ttu-id="1240a-207">Verze balíčku, který se má znovu zobrazit</span><span class="sxs-lookup"><span data-stu-id="1240a-207">The version of the package to relist</span></span>
<span data-ttu-id="1240a-208">X-NuGet – ApiKey</span><span class="sxs-lookup"><span data-stu-id="1240a-208">X-NuGet-ApiKey</span></span> | <span data-ttu-id="1240a-209">Hlavička</span><span class="sxs-lookup"><span data-stu-id="1240a-209">Header</span></span> | <span data-ttu-id="1240a-210">řetězec</span><span class="sxs-lookup"><span data-stu-id="1240a-210">string</span></span> | <span data-ttu-id="1240a-211">ano</span><span class="sxs-lookup"><span data-stu-id="1240a-211">yes</span></span>      | <span data-ttu-id="1240a-212">Například `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="1240a-212">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="1240a-213">Odpověď</span><span class="sxs-lookup"><span data-stu-id="1240a-213">Response</span></span>

<span data-ttu-id="1240a-214">Stavový kód</span><span class="sxs-lookup"><span data-stu-id="1240a-214">Status Code</span></span> | <span data-ttu-id="1240a-215">Význam</span><span class="sxs-lookup"><span data-stu-id="1240a-215">Meaning</span></span>
----------- | -------
<span data-ttu-id="1240a-216">200</span><span class="sxs-lookup"><span data-stu-id="1240a-216">200</span></span>         | <span data-ttu-id="1240a-217">Balíček je nyní uveden</span><span class="sxs-lookup"><span data-stu-id="1240a-217">The package is now listed</span></span>
<span data-ttu-id="1240a-218">404</span><span class="sxs-lookup"><span data-stu-id="1240a-218">404</span></span>         | <span data-ttu-id="1240a-219">Žádný balíček se zadaným `ID` a `VERSION` neexistuje.</span><span class="sxs-lookup"><span data-stu-id="1240a-219">No package with the provided `ID` and `VERSION` exists</span></span>
