---
title: Balíčky symbolů nabízených oznámení, API NuGet | Microsoft Docs
author: cristinamanum
ms.author:
- cmanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Služba publikování umožňuje klientům publikovat nové balíčky symbolů.
keywords: Balíček symbolů nabízených oznámení rozhraní NuGet API
ms.reviewer: karann
ms.openlocfilehash: 27e557bf15ce31152243a409eddc4112eeb6c38b
ms.sourcegitcommit: ac9a00ccaf90e539a381e92b650074910b21eb0d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/03/2019
ms.locfileid: "70235105"
---
# <a name="push-symbol-packages"></a><span data-ttu-id="6fb45-104">Balíčky symbolů nabízených oznámení</span><span class="sxs-lookup"><span data-stu-id="6fb45-104">Push Symbol Packages</span></span>

<span data-ttu-id="6fb45-105">Balíčky symbolů ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) je možné vložit pomocí rozhraní NuGet V3 API.</span><span class="sxs-lookup"><span data-stu-id="6fb45-105">It is possible to push symbols packages ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the NuGet V3 API.</span></span>
<span data-ttu-id="6fb45-106">Tyto operace jsou založeny na `SymbolPackagePublish` prostředku, který najdete v [indexu služby](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="6fb45-106">These operations are based off of the `SymbolPackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="6fb45-107">Správa verzí</span><span class="sxs-lookup"><span data-stu-id="6fb45-107">Versioning</span></span>

<span data-ttu-id="6fb45-108">Použije se `@type` následující hodnota:</span><span class="sxs-lookup"><span data-stu-id="6fb45-108">The following `@type` value is used:</span></span>

<span data-ttu-id="6fb45-109">@typeosa</span><span class="sxs-lookup"><span data-stu-id="6fb45-109">@type value</span></span>                 | <span data-ttu-id="6fb45-110">Poznámky</span><span class="sxs-lookup"><span data-stu-id="6fb45-110">Notes</span></span>
--------------------        | -----
<span data-ttu-id="6fb45-111">SymbolPackagePublish/4.9.0</span><span class="sxs-lookup"><span data-stu-id="6fb45-111">SymbolPackagePublish/4.9.0</span></span>  | <span data-ttu-id="6fb45-112">Počáteční verze</span><span class="sxs-lookup"><span data-stu-id="6fb45-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="6fb45-113">Základní adresa URL</span><span class="sxs-lookup"><span data-stu-id="6fb45-113">Base URL</span></span>

<span data-ttu-id="6fb45-114">Základní adresa URL následujících rozhraní API je hodnota `@id` vlastnosti `SymbolPackagePublish/4.9.0` prostředku v [indexu služby](service-index.md)zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="6fb45-114">The base URL for the following APIs is the value of the `@id` property of the `SymbolPackagePublish/4.9.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="6fb45-115">Pro dokumentaci níže se používá adresa URL balíčku NuGet. org.</span><span class="sxs-lookup"><span data-stu-id="6fb45-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="6fb45-116">Zvažte `https://www.nuget.org/api/v2/symbolpackage` možnost použít jako zástupný symbol `@id` pro hodnotu nalezenou v indexu služby.</span><span class="sxs-lookup"><span data-stu-id="6fb45-116">Consider `https://www.nuget.org/api/v2/symbolpackage` as a placeholder for the `@id` value found in the service index.</span></span>

## <a name="http-methods"></a><span data-ttu-id="6fb45-117">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="6fb45-117">HTTP methods</span></span>

<span data-ttu-id="6fb45-118">Tento prostředek podporuje metodu http.`PUT`</span><span class="sxs-lookup"><span data-stu-id="6fb45-118">The `PUT` HTTP method is supported by this resource.</span></span> 

## <a name="push-a-symbol-package"></a><span data-ttu-id="6fb45-119">Vložení balíčku symbolů</span><span class="sxs-lookup"><span data-stu-id="6fb45-119">Push a symbol package</span></span>

<span data-ttu-id="6fb45-120">nuget.org podporuje vložení nového formátu balíčků symbolů ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) pomocí následujícího rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="6fb45-120">nuget.org supports pushing new symbol packages format ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the following API.</span></span> 

    PUT https://www.nuget.org/api/v2/symbolpackage

<span data-ttu-id="6fb45-121">Balíčky symbolů se stejným ID a verzí je možné odeslat víckrát.</span><span class="sxs-lookup"><span data-stu-id="6fb45-121">Symbol packages with the same ID and version can be submitted multiple times.</span></span> <span data-ttu-id="6fb45-122">Balíček symbolů bude odmítnut v následujících případech.</span><span class="sxs-lookup"><span data-stu-id="6fb45-122">A symbol package will be rejected in the following cases.</span></span>
- <span data-ttu-id="6fb45-123">Balíček se stejným ID a verzí neexistuje.</span><span class="sxs-lookup"><span data-stu-id="6fb45-123">A package with the same ID and version does not exist.</span></span>
- <span data-ttu-id="6fb45-124">Byl vložen balíček symbolů se stejným ID a verzí, ale ještě není publikovaný.</span><span class="sxs-lookup"><span data-stu-id="6fb45-124">A symbol package with the same ID and version was pushed but is not yet published.</span></span>
- <span data-ttu-id="6fb45-125">Balíček symbolů ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) je neplatný (viz [omezení balíčku symbolů](../create-packages/Symbol-Packages-snupkg.md)).</span><span class="sxs-lookup"><span data-stu-id="6fb45-125">The symbol package ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) is invalid (see [symbol package constraints](../create-packages/Symbol-Packages-snupkg.md)).</span></span>

### <a name="request-parameters"></a><span data-ttu-id="6fb45-126">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="6fb45-126">Request parameters</span></span>

<span data-ttu-id="6fb45-127">Name</span><span class="sxs-lookup"><span data-stu-id="6fb45-127">Name</span></span>           | <span data-ttu-id="6fb45-128">V</span><span class="sxs-lookup"><span data-stu-id="6fb45-128">In</span></span>     | <span data-ttu-id="6fb45-129">type</span><span class="sxs-lookup"><span data-stu-id="6fb45-129">Type</span></span>   | <span data-ttu-id="6fb45-130">Požadováno</span><span class="sxs-lookup"><span data-stu-id="6fb45-130">Required</span></span> | <span data-ttu-id="6fb45-131">Poznámky</span><span class="sxs-lookup"><span data-stu-id="6fb45-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="6fb45-132">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="6fb45-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="6fb45-133">Záhlaví</span><span class="sxs-lookup"><span data-stu-id="6fb45-133">Header</span></span> | <span data-ttu-id="6fb45-134">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="6fb45-134">string</span></span> | <span data-ttu-id="6fb45-135">ano</span><span class="sxs-lookup"><span data-stu-id="6fb45-135">yes</span></span>      | <span data-ttu-id="6fb45-136">Třeba `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="6fb45-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="6fb45-137">Klíč rozhraní API je neprůhledný řetězec ze zdroje balíčku uživatelem a nakonfigurovaný do klienta.</span><span class="sxs-lookup"><span data-stu-id="6fb45-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="6fb45-138">Není k dispozici žádný konkrétní formát řetězce, ale délka klíče rozhraní API by neměla překročit rozumnou velikost pro hodnoty hlaviček protokolu HTTP.</span><span class="sxs-lookup"><span data-stu-id="6fb45-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="6fb45-139">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="6fb45-139">Request body</span></span>

<span data-ttu-id="6fb45-140">Text žádosti o nabízení oznámení je stejný jako text žádosti o nabízenou žádost balíčku (viz [push a DELETE balíčku](package-publish-resource.md)).</span><span class="sxs-lookup"><span data-stu-id="6fb45-140">The request body for the symbol push is same as with the request body of a package push request (see [package push and delete](package-publish-resource.md)).</span></span> 

### <a name="response"></a><span data-ttu-id="6fb45-141">Odpověď</span><span class="sxs-lookup"><span data-stu-id="6fb45-141">Response</span></span>

<span data-ttu-id="6fb45-142">Stavový kód</span><span class="sxs-lookup"><span data-stu-id="6fb45-142">Status Code</span></span> | <span data-ttu-id="6fb45-143">Význam</span><span class="sxs-lookup"><span data-stu-id="6fb45-143">Meaning</span></span>
----------- | -------
<span data-ttu-id="6fb45-144">201</span><span class="sxs-lookup"><span data-stu-id="6fb45-144">201</span></span>         | <span data-ttu-id="6fb45-145">Balíček symbolů byl úspěšně vložen.</span><span class="sxs-lookup"><span data-stu-id="6fb45-145">The symbol package was successfully pushed.</span></span>
<span data-ttu-id="6fb45-146">400</span><span class="sxs-lookup"><span data-stu-id="6fb45-146">400</span></span>         | <span data-ttu-id="6fb45-147">Poskytnutý balíček symbolů je neplatný.</span><span class="sxs-lookup"><span data-stu-id="6fb45-147">The provided symbol package is invalid.</span></span>
<span data-ttu-id="6fb45-148">401</span><span class="sxs-lookup"><span data-stu-id="6fb45-148">401</span></span>         | <span data-ttu-id="6fb45-149">Uživatel nemá autorizaci k provedení této akce.</span><span class="sxs-lookup"><span data-stu-id="6fb45-149">The user is not authorized to perform this action.</span></span>
<span data-ttu-id="6fb45-150">404</span><span class="sxs-lookup"><span data-stu-id="6fb45-150">404</span></span>         | <span data-ttu-id="6fb45-151">Odpovídající balíček se zadaným ID a verzí neexistuje.</span><span class="sxs-lookup"><span data-stu-id="6fb45-151">A corresponding package with the provided ID and version does not exist.</span></span>
<span data-ttu-id="6fb45-152">409</span><span class="sxs-lookup"><span data-stu-id="6fb45-152">409</span></span>         | <span data-ttu-id="6fb45-153">Balíček symbolů se zadaným ID a verzí byl vložen, ale ještě není k dispozici.</span><span class="sxs-lookup"><span data-stu-id="6fb45-153">A symbol package with the provided ID and version was pushed but it is not available yet.</span></span>
<span data-ttu-id="6fb45-154">413</span><span class="sxs-lookup"><span data-stu-id="6fb45-154">413</span></span>         | <span data-ttu-id="6fb45-155">Balíček je moc velký.</span><span class="sxs-lookup"><span data-stu-id="6fb45-155">The package is too large.</span></span>

