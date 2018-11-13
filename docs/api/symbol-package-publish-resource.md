---
title: Vložit Symbol balíčky NuGet rozhraní API | Dokumentace Microsoftu
author:
- cristinamanum
- kraigb
ms.author:
- cmanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Služba publikování umožňuje klientům publikovat nové balíčky pro symbol.
keywords: Balíček NuGet rozhraní API nabízených symbolů
ms.reviewer: karann
ms.openlocfilehash: 514ab3683db81da5b2220b005b8b39f1fec8300d
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580452"
---
# <a name="push-symbol-packages"></a><span data-ttu-id="c818c-104">Balíčky symbolů nabízených oznámení</span><span class="sxs-lookup"><span data-stu-id="c818c-104">Push Symbol Packages</span></span>

<span data-ttu-id="c818c-105">Je možné do balíčků symbolů nabízených oznámení ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) pomocí rozhraní API V3 NuGet.</span><span class="sxs-lookup"><span data-stu-id="c818c-105">It is possible to push symbols packages ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the NuGet V3 API.</span></span>
<span data-ttu-id="c818c-106">Tyto operace jsou odhlásit z založené `SymbolPackagePublish` prostředek se nenašel v [index služby](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="c818c-106">These operations are based off of the `SymbolPackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="c818c-107">Správa verzí</span><span class="sxs-lookup"><span data-stu-id="c818c-107">Versioning</span></span>

<span data-ttu-id="c818c-108">Následující `@type` hodnota se používá:</span><span class="sxs-lookup"><span data-stu-id="c818c-108">The following `@type` value is used:</span></span>

<span data-ttu-id="c818c-109">@type Hodnota</span><span class="sxs-lookup"><span data-stu-id="c818c-109">@type value</span></span>                 | <span data-ttu-id="c818c-110">Poznámky</span><span class="sxs-lookup"><span data-stu-id="c818c-110">Notes</span></span>
--------------------        | -----
<span data-ttu-id="c818c-111">SymbolPackagePublish/4.9.0</span><span class="sxs-lookup"><span data-stu-id="c818c-111">SymbolPackagePublish/4.9.0</span></span>  | <span data-ttu-id="c818c-112">Počáteční verze</span><span class="sxs-lookup"><span data-stu-id="c818c-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="c818c-113">Základní adresa URL</span><span class="sxs-lookup"><span data-stu-id="c818c-113">Base URL</span></span>

<span data-ttu-id="c818c-114">Základní adresa URL pro následující rozhraní API je hodnota `@id` vlastnost `SymbolPackagePublish/4.9.0` prostředků ve zdroji balíčku [index služby](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="c818c-114">The base URL for the following APIs is the value of the `@id` property of the `SymbolPackagePublish/4.9.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="c818c-115">Pro níže uvedenou dokumentaci se používá adresu URL nuget.org.</span><span class="sxs-lookup"><span data-stu-id="c818c-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="c818c-116">Vezměte v úvahu `https://www.nuget.org/api/v2/symbolpackage` jako zástupný symbol pro `@id` hodnota nalezena v indexu služby.</span><span class="sxs-lookup"><span data-stu-id="c818c-116">Consider `https://www.nuget.org/api/v2/symbolpackage` as a placeholder for the `@id` value found in the service index.</span></span>

## <a name="http-methods"></a><span data-ttu-id="c818c-117">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="c818c-117">HTTP methods</span></span>

<span data-ttu-id="c818c-118">`PUT` Tento prostředek podporuje metodu protokolu HTTP.</span><span class="sxs-lookup"><span data-stu-id="c818c-118">The `PUT` HTTP method is supported by this resource.</span></span> 

## <a name="push-a-symbol-package"></a><span data-ttu-id="c818c-119">Push balíček symbolů</span><span class="sxs-lookup"><span data-stu-id="c818c-119">Push a symbol package</span></span>

<span data-ttu-id="c818c-120">podporuje vložit nový formát symbol balíčky nuget.org ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) pomocí následujících rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="c818c-120">nuget.org supports pushing new symbol packages format ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the following API.</span></span> 

    PUT https://www.nuget.org/api/v2/symbolpackage

<span data-ttu-id="c818c-121">Balíčky symbolů se stejným ID a verzi lze odeslat více než jednou.</span><span class="sxs-lookup"><span data-stu-id="c818c-121">Symbol packages with the same ID and version can be submitted multiple times.</span></span> <span data-ttu-id="c818c-122">V následujících případech budou odmítnuty balíček symbolů.</span><span class="sxs-lookup"><span data-stu-id="c818c-122">A symbol package will be rejected in the following cases.</span></span>
- <span data-ttu-id="c818c-123">Balíček se stejným ID a verze neexistuje.</span><span class="sxs-lookup"><span data-stu-id="c818c-123">A package with the same ID and version does not exist.</span></span>
- <span data-ttu-id="c818c-124">Balíček symbolů se stejným ID a verze se vložil, ale ještě nebyla publikována.</span><span class="sxs-lookup"><span data-stu-id="c818c-124">A symbol package with the same ID and version was pushed but is not yet published.</span></span>
- <span data-ttu-id="c818c-125">Balíček symbolů ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) je neplatný (naleznete v tématu [symbol balíček omezení](../create-packages/Symbol-Packages-snupkg.md)).</span><span class="sxs-lookup"><span data-stu-id="c818c-125">The symbol package ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) is invalid (see [symbol package constraints](../create-packages/Symbol-Packages-snupkg.md)).</span></span>

### <a name="request-parameters"></a><span data-ttu-id="c818c-126">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="c818c-126">Request parameters</span></span>

<span data-ttu-id="c818c-127">Název</span><span class="sxs-lookup"><span data-stu-id="c818c-127">Name</span></span>           | <span data-ttu-id="c818c-128">V</span><span class="sxs-lookup"><span data-stu-id="c818c-128">In</span></span>     | <span data-ttu-id="c818c-129">Typ</span><span class="sxs-lookup"><span data-stu-id="c818c-129">Type</span></span>   | <span data-ttu-id="c818c-130">Požadováno</span><span class="sxs-lookup"><span data-stu-id="c818c-130">Required</span></span> | <span data-ttu-id="c818c-131">Poznámky</span><span class="sxs-lookup"><span data-stu-id="c818c-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="c818c-132">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="c818c-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="c818c-133">Záhlaví</span><span class="sxs-lookup"><span data-stu-id="c818c-133">Header</span></span> | <span data-ttu-id="c818c-134">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="c818c-134">string</span></span> | <span data-ttu-id="c818c-135">Ano</span><span class="sxs-lookup"><span data-stu-id="c818c-135">yes</span></span>      | <span data-ttu-id="c818c-136">Třeba `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="c818c-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="c818c-137">Klíč rozhraní API je neprůhledný řetězec získali ze zdroje balíčku uživatelem a konfiguraci do klienta.</span><span class="sxs-lookup"><span data-stu-id="c818c-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="c818c-138">Je vyžadováno žádné konkrétní řetězec formátu, ale délka klíče rozhraní API by neměl být delší než rozumnou velikost pro hodnoty hlavičky protokolu HTTP.</span><span class="sxs-lookup"><span data-stu-id="c818c-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="c818c-139">Text žádosti</span><span class="sxs-lookup"><span data-stu-id="c818c-139">Request body</span></span>

<span data-ttu-id="c818c-140">Text žádosti o nasdílení změn symbol je stejná jako žádost subjektu, který požadavek nabízených oznámení balíčku (viz [balíček nabízených oznámení a odstranit](package-publish-resource.md)).</span><span class="sxs-lookup"><span data-stu-id="c818c-140">The request body for the symbol push is same as with the request body of a package push request (see [package push and delete](package-publish-resource.md)).</span></span> 

### <a name="response"></a><span data-ttu-id="c818c-141">Odpověď</span><span class="sxs-lookup"><span data-stu-id="c818c-141">Response</span></span>

<span data-ttu-id="c818c-142">Stavový kód</span><span class="sxs-lookup"><span data-stu-id="c818c-142">Status Code</span></span> | <span data-ttu-id="c818c-143">Význam</span><span class="sxs-lookup"><span data-stu-id="c818c-143">Meaning</span></span>
----------- | -------
<span data-ttu-id="c818c-144">201</span><span class="sxs-lookup"><span data-stu-id="c818c-144">201</span></span>         | <span data-ttu-id="c818c-145">Balíček symbolů se úspěšně odeslal.</span><span class="sxs-lookup"><span data-stu-id="c818c-145">The symbol package was successfully pushed.</span></span>
<span data-ttu-id="c818c-146">400</span><span class="sxs-lookup"><span data-stu-id="c818c-146">400</span></span>         | <span data-ttu-id="c818c-147">Zadaný symbol balíček je neplatný.</span><span class="sxs-lookup"><span data-stu-id="c818c-147">The provided symbol package is invalid.</span></span>
<span data-ttu-id="c818c-148">401</span><span class="sxs-lookup"><span data-stu-id="c818c-148">401</span></span>         | <span data-ttu-id="c818c-149">Uživatel nemá oprávnění k provedení této akce.</span><span class="sxs-lookup"><span data-stu-id="c818c-149">The user is not authorized to perform this action.</span></span>
<span data-ttu-id="c818c-150">404</span><span class="sxs-lookup"><span data-stu-id="c818c-150">404</span></span>         | <span data-ttu-id="c818c-151">Neexistuje odpovídající balíček se zadané ID a verzi.</span><span class="sxs-lookup"><span data-stu-id="c818c-151">A corresponding package with the provided ID and version does not exist.</span></span>
<span data-ttu-id="c818c-152">409</span><span class="sxs-lookup"><span data-stu-id="c818c-152">409</span></span>         | <span data-ttu-id="c818c-153">Balíček symbolů pomocí zadaného ID a verze se vložil, ale je ještě není k dispozici.</span><span class="sxs-lookup"><span data-stu-id="c818c-153">A symbol package with the provided ID and version was pushed but it is not available yet.</span></span>
<span data-ttu-id="c818c-154">413</span><span class="sxs-lookup"><span data-stu-id="c818c-154">413</span></span>         | <span data-ttu-id="c818c-155">Balíček je příliš velký.</span><span class="sxs-lookup"><span data-stu-id="c818c-155">The package is too large.</span></span>

