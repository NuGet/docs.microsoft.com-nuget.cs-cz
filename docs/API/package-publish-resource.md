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
ms.openlocfilehash: 1fa3c0e1698a11208d9ef29fdf26a4980cb60cf5
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="push-and-delete"></a><span data-ttu-id="3763a-104">Push a odstranění</span><span class="sxs-lookup"><span data-stu-id="3763a-104">Push and Delete</span></span>

<span data-ttu-id="3763a-105">Je možné nabízené a odstranit (nebo unlist, v závislosti na implementaci serveru) balíčky, pomocí rozhraní API V3 NuGet.</span><span class="sxs-lookup"><span data-stu-id="3763a-105">It is possible to push and delete (or unlist, depending on the server implementation) packages using the NuGet V3 API.</span></span>
<span data-ttu-id="3763a-106">Obě tyto operace jsou na základě odhlásit z `PackagePublish` v nalezen prostředek [indexu služby](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="3763a-106">Both operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="3763a-107">Správa verzí</span><span class="sxs-lookup"><span data-stu-id="3763a-107">Versioning</span></span>

<span data-ttu-id="3763a-108">Následující `@type` hodnota se používá:</span><span class="sxs-lookup"><span data-stu-id="3763a-108">The following `@type` value is used:</span></span>

<span data-ttu-id="3763a-109">@typeHodnota</span><span class="sxs-lookup"><span data-stu-id="3763a-109">@type value</span></span>          | <span data-ttu-id="3763a-110">Poznámky</span><span class="sxs-lookup"><span data-stu-id="3763a-110">Notes</span></span>
-------------------- | -----
<span data-ttu-id="3763a-111">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="3763a-111">PackagePublish/2.0.0</span></span> | <span data-ttu-id="3763a-112">Původní verze</span><span class="sxs-lookup"><span data-stu-id="3763a-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="3763a-113">Základní adresu URL</span><span class="sxs-lookup"><span data-stu-id="3763a-113">Base URL</span></span>

<span data-ttu-id="3763a-114">Základní adresu URL pro následující rozhraní API je hodnota `@id` vlastnost `PackagePublish/2.0.0` prostředků ve zdroji balíčků [indexu služby](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="3763a-114">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="3763a-115">Adresa URL nuget.org v dokumentaci je použita.</span><span class="sxs-lookup"><span data-stu-id="3763a-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="3763a-116">Vezměte v úvahu `https://www.nuget.org/api/v2/package` jako zástupný symbol pro `@id` nalezena hodnota v indexu služby.</span><span class="sxs-lookup"><span data-stu-id="3763a-116">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="3763a-117">Všimněte si, že tato adresa URL odkazuje do stejného umístění jako starší verze koncový bod nabízené V2 vzhledem k tomu, že protokol je stejný.</span><span class="sxs-lookup"><span data-stu-id="3763a-117">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="3763a-118">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="3763a-118">HTTP methods</span></span>

<span data-ttu-id="3763a-119">`PUT` a `DELETE` metody HTTP podporuje tento prostředek.</span><span class="sxs-lookup"><span data-stu-id="3763a-119">The `PUT` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="3763a-120">Které metody jsou podporovány na každém koncovém bodu najdete níže.</span><span class="sxs-lookup"><span data-stu-id="3763a-120">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="3763a-121">Push balíčku</span><span class="sxs-lookup"><span data-stu-id="3763a-121">Push a package</span></span>

<span data-ttu-id="3763a-122">nuget.org podporuje vkládání nové balíčky pomocí následující rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="3763a-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="3763a-123">Pokud balíček s zadané ID a verzí již existuje, odmítnou nuget.org nabízeného oznámení.</span><span class="sxs-lookup"><span data-stu-id="3763a-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="3763a-124">Další zdroje balíčku může podporovat nahrazování existujícího balíčku.</span><span class="sxs-lookup"><span data-stu-id="3763a-124">Other package sources may support replacing an existing package.</span></span>

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a><span data-ttu-id="3763a-125">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="3763a-125">Request parameters</span></span>

<span data-ttu-id="3763a-126">Název</span><span class="sxs-lookup"><span data-stu-id="3763a-126">Name</span></span>           | <span data-ttu-id="3763a-127">V</span><span class="sxs-lookup"><span data-stu-id="3763a-127">In</span></span>     | <span data-ttu-id="3763a-128">Typ</span><span class="sxs-lookup"><span data-stu-id="3763a-128">Type</span></span>   | <span data-ttu-id="3763a-129">Požadováno</span><span class="sxs-lookup"><span data-stu-id="3763a-129">Required</span></span> | <span data-ttu-id="3763a-130">Poznámky</span><span class="sxs-lookup"><span data-stu-id="3763a-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="3763a-131">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="3763a-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="3763a-132">Záhlaví</span><span class="sxs-lookup"><span data-stu-id="3763a-132">Header</span></span> | <span data-ttu-id="3763a-133">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="3763a-133">string</span></span> | <span data-ttu-id="3763a-134">Ano</span><span class="sxs-lookup"><span data-stu-id="3763a-134">yes</span></span>      | <span data-ttu-id="3763a-135">Třeba `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="3763a-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="3763a-136">Klíč rozhraní API je neprůhledný řetězec, že podmínky ze zdroje balíčků uživatelem a nakonfigurované do klienta.</span><span class="sxs-lookup"><span data-stu-id="3763a-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="3763a-137">Je vyžadováno žádné konkrétní řetězec formátu, ale nesmí překročit délka klíč rozhraní API přiměřené velikosti pro hodnoty hlavičky protokolu HTTP.</span><span class="sxs-lookup"><span data-stu-id="3763a-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="3763a-138">Text žádosti</span><span class="sxs-lookup"><span data-stu-id="3763a-138">Request body</span></span>

<span data-ttu-id="3763a-139">Textu požadavku musí pocházet v následující podobě:</span><span class="sxs-lookup"><span data-stu-id="3763a-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="3763a-140">Dat vícedílného formuláře</span><span class="sxs-lookup"><span data-stu-id="3763a-140">Multipart form data</span></span>

<span data-ttu-id="3763a-141">Hlavička požadavku `Content-Type` je `multipart/form-data` a první položky v těle žádosti je nezpracované bajtů .nupkg se instaluje.</span><span class="sxs-lookup"><span data-stu-id="3763a-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="3763a-142">Následující položky v textu vícedílné zprávy se ignorují.</span><span class="sxs-lookup"><span data-stu-id="3763a-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="3763a-143">Název souboru nebo jiné záhlaví položek s více částmi se ignorují.</span><span class="sxs-lookup"><span data-stu-id="3763a-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="3763a-144">Odpověď</span><span class="sxs-lookup"><span data-stu-id="3763a-144">Response</span></span>

<span data-ttu-id="3763a-145">Stavový kód</span><span class="sxs-lookup"><span data-stu-id="3763a-145">Status Code</span></span> | <span data-ttu-id="3763a-146">Význam</span><span class="sxs-lookup"><span data-stu-id="3763a-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="3763a-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="3763a-147">201, 202</span></span>    | <span data-ttu-id="3763a-148">Balíček byl úspěšně poslat.</span><span class="sxs-lookup"><span data-stu-id="3763a-148">The package was successfully pushed</span></span>
<span data-ttu-id="3763a-149">400</span><span class="sxs-lookup"><span data-stu-id="3763a-149">400</span></span>         | <span data-ttu-id="3763a-150">Zadaný balíček je neplatná</span><span class="sxs-lookup"><span data-stu-id="3763a-150">The provided package is invalid</span></span>
<span data-ttu-id="3763a-151">409</span><span class="sxs-lookup"><span data-stu-id="3763a-151">409</span></span>         | <span data-ttu-id="3763a-152">Balíček s zadané ID a verzí již existuje.</span><span class="sxs-lookup"><span data-stu-id="3763a-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="3763a-153">Implementace serveru lišit vráceny v případě, že balíček je úspěšně nabídnutých úspěch stavový kód.</span><span class="sxs-lookup"><span data-stu-id="3763a-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="3763a-154">Odstranění balíčku</span><span class="sxs-lookup"><span data-stu-id="3763a-154">Delete a package</span></span>

<span data-ttu-id="3763a-155">nuget.org interpretuje požadavku na odstranění balíčku jako na "unlist".</span><span class="sxs-lookup"><span data-stu-id="3763a-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="3763a-156">To znamená, že balíček je stále k dispozici pro existující příjemce balíčku, ale balíček už se zobrazí ve výsledcích hledání nebo webové rozhraní.</span><span class="sxs-lookup"><span data-stu-id="3763a-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="3763a-157">Další informace o tento postup najdete v tématu [odstranit balíčky](../policies/deleting-packages.md) zásad.</span><span class="sxs-lookup"><span data-stu-id="3763a-157">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="3763a-158">Jiných implementacích serveru jsou volně interpretovat jako pevný odstranění tohoto signálu, soft odstranit nebo unlist.</span><span class="sxs-lookup"><span data-stu-id="3763a-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="3763a-159">Například [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (implementaci serveru pouze podpora starší API V2) podporuje zpracování této žádosti jako unlist nebo pevné odstranění podle možnosti konfigurace.</span><span class="sxs-lookup"><span data-stu-id="3763a-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="3763a-160">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="3763a-160">Request parameters</span></span>

<span data-ttu-id="3763a-161">Název</span><span class="sxs-lookup"><span data-stu-id="3763a-161">Name</span></span>           | <span data-ttu-id="3763a-162">V</span><span class="sxs-lookup"><span data-stu-id="3763a-162">In</span></span>     | <span data-ttu-id="3763a-163">Typ</span><span class="sxs-lookup"><span data-stu-id="3763a-163">Type</span></span>   | <span data-ttu-id="3763a-164">Požadováno</span><span class="sxs-lookup"><span data-stu-id="3763a-164">Required</span></span> | <span data-ttu-id="3763a-165">Poznámky</span><span class="sxs-lookup"><span data-stu-id="3763a-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="3763a-166">ID</span><span class="sxs-lookup"><span data-stu-id="3763a-166">ID</span></span>             | <span data-ttu-id="3763a-167">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="3763a-167">URL</span></span>    | <span data-ttu-id="3763a-168">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="3763a-168">string</span></span> | <span data-ttu-id="3763a-169">Ano</span><span class="sxs-lookup"><span data-stu-id="3763a-169">yes</span></span>      | <span data-ttu-id="3763a-170">ID balíčku se má odstranit</span><span class="sxs-lookup"><span data-stu-id="3763a-170">The ID of the package to delete</span></span>
<span data-ttu-id="3763a-171">VERZE</span><span class="sxs-lookup"><span data-stu-id="3763a-171">VERSION</span></span>        | <span data-ttu-id="3763a-172">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="3763a-172">URL</span></span>    | <span data-ttu-id="3763a-173">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="3763a-173">string</span></span> | <span data-ttu-id="3763a-174">Ano</span><span class="sxs-lookup"><span data-stu-id="3763a-174">yes</span></span>      | <span data-ttu-id="3763a-175">Verze balíčku odstranit</span><span class="sxs-lookup"><span data-stu-id="3763a-175">The version of the package to delete</span></span>
<span data-ttu-id="3763a-176">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="3763a-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="3763a-177">Záhlaví</span><span class="sxs-lookup"><span data-stu-id="3763a-177">Header</span></span> | <span data-ttu-id="3763a-178">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="3763a-178">string</span></span> | <span data-ttu-id="3763a-179">Ano</span><span class="sxs-lookup"><span data-stu-id="3763a-179">yes</span></span>      | <span data-ttu-id="3763a-180">Třeba `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="3763a-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="3763a-181">Odpověď</span><span class="sxs-lookup"><span data-stu-id="3763a-181">Response</span></span>

<span data-ttu-id="3763a-182">Stavový kód</span><span class="sxs-lookup"><span data-stu-id="3763a-182">Status Code</span></span> | <span data-ttu-id="3763a-183">Význam</span><span class="sxs-lookup"><span data-stu-id="3763a-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="3763a-184">204</span><span class="sxs-lookup"><span data-stu-id="3763a-184">204</span></span>         | <span data-ttu-id="3763a-185">Balíček byl odstraněn.</span><span class="sxs-lookup"><span data-stu-id="3763a-185">The package was deleted</span></span>
<span data-ttu-id="3763a-186">404</span><span class="sxs-lookup"><span data-stu-id="3763a-186">404</span></span>         | <span data-ttu-id="3763a-187">Žádný balíček poskytnutým `ID` a `VERSION` existuje</span><span class="sxs-lookup"><span data-stu-id="3763a-187">No package with the provided `ID` and `VERSION` exists</span></span>
