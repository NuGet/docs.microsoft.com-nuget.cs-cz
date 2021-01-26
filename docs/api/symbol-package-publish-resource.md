---
title: Balíčky symbolů nabízených oznámení, API NuGet | Microsoft Docs
author: cristinamanum
ms.author: cmanu
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Služba publikování umožňuje klientům publikovat nové balíčky symbolů.
keywords: Balíček symbolů nabízených oznámení rozhraní NuGet API
ms.reviewer: karann
ms.openlocfilehash: 91bb4c9ca77fd7f1ff35831e02eb4f9d65d641c5
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773892"
---
# <a name="push-symbol-packages"></a><span data-ttu-id="661f6-104">Balíčky symbolů nabízených oznámení</span><span class="sxs-lookup"><span data-stu-id="661f6-104">Push Symbol Packages</span></span>

<span data-ttu-id="661f6-105">Balíčky symbolů ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) je možné vložit pomocí rozhraní NuGet V3 API.</span><span class="sxs-lookup"><span data-stu-id="661f6-105">It is possible to push symbols packages ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the NuGet V3 API.</span></span>
<span data-ttu-id="661f6-106">Tyto operace jsou založeny na prostředku, který `SymbolPackagePublish` najdete v [indexu služby](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="661f6-106">These operations are based off of the `SymbolPackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="661f6-107">Správa verzí</span><span class="sxs-lookup"><span data-stu-id="661f6-107">Versioning</span></span>

<span data-ttu-id="661f6-108">Použije se následující `@type` hodnota:</span><span class="sxs-lookup"><span data-stu-id="661f6-108">The following `@type` value is used:</span></span>

<span data-ttu-id="661f6-109">@type osa</span><span class="sxs-lookup"><span data-stu-id="661f6-109">@type value</span></span>                 | <span data-ttu-id="661f6-110">Poznámky</span><span class="sxs-lookup"><span data-stu-id="661f6-110">Notes</span></span>
--------------------        | -----
<span data-ttu-id="661f6-111">SymbolPackagePublish/4.9.0</span><span class="sxs-lookup"><span data-stu-id="661f6-111">SymbolPackagePublish/4.9.0</span></span>  | <span data-ttu-id="661f6-112">Počáteční verze</span><span class="sxs-lookup"><span data-stu-id="661f6-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="661f6-113">Základní adresa URL</span><span class="sxs-lookup"><span data-stu-id="661f6-113">Base URL</span></span>

<span data-ttu-id="661f6-114">Základní adresa URL následujících rozhraní API je hodnota `@id` vlastnosti `SymbolPackagePublish/4.9.0` prostředku v [indexu služby](service-index.md)zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="661f6-114">The base URL for the following APIs is the value of the `@id` property of the `SymbolPackagePublish/4.9.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="661f6-115">Pro dokumentaci níže se používá adresa URL balíčku NuGet. org.</span><span class="sxs-lookup"><span data-stu-id="661f6-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="661f6-116">Zvažte možnost `https://www.nuget.org/api/v2/symbolpackage` použít jako zástupný symbol pro `@id` hodnotu nalezenou v indexu služby.</span><span class="sxs-lookup"><span data-stu-id="661f6-116">Consider `https://www.nuget.org/api/v2/symbolpackage` as a placeholder for the `@id` value found in the service index.</span></span>

## <a name="http-methods"></a><span data-ttu-id="661f6-117">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="661f6-117">HTTP methods</span></span>

<span data-ttu-id="661f6-118">`PUT`Tento prostředek podporuje metodu HTTP.</span><span class="sxs-lookup"><span data-stu-id="661f6-118">The `PUT` HTTP method is supported by this resource.</span></span> 

## <a name="push-a-symbol-package"></a><span data-ttu-id="661f6-119">Vložení balíčku symbolů</span><span class="sxs-lookup"><span data-stu-id="661f6-119">Push a symbol package</span></span>

<span data-ttu-id="661f6-120">nuget.org podporuje vložení nového formátu balíčků symbolů ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) pomocí následujícího rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="661f6-120">nuget.org supports pushing new symbol packages format ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the following API.</span></span> 

```
PUT https://www.nuget.org/api/v2/symbolpackage
```

<span data-ttu-id="661f6-121">Balíčky symbolů se stejným ID a verzí je možné odeslat víckrát.</span><span class="sxs-lookup"><span data-stu-id="661f6-121">Symbol packages with the same ID and version can be submitted multiple times.</span></span> <span data-ttu-id="661f6-122">Balíček symbolů bude odmítnut v následujících případech.</span><span class="sxs-lookup"><span data-stu-id="661f6-122">A symbol package will be rejected in the following cases.</span></span>
- <span data-ttu-id="661f6-123">Balíček se stejným ID a verzí neexistuje.</span><span class="sxs-lookup"><span data-stu-id="661f6-123">A package with the same ID and version does not exist.</span></span>
- <span data-ttu-id="661f6-124">Byl vložen balíček symbolů se stejným ID a verzí, ale ještě není publikovaný.</span><span class="sxs-lookup"><span data-stu-id="661f6-124">A symbol package with the same ID and version was pushed but is not yet published.</span></span>
- <span data-ttu-id="661f6-125">Balíček symbolů ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) je neplatný (viz [omezení balíčku symbolů](../create-packages/Symbol-Packages-snupkg.md)).</span><span class="sxs-lookup"><span data-stu-id="661f6-125">The symbol package ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) is invalid (see [symbol package constraints](../create-packages/Symbol-Packages-snupkg.md)).</span></span>

### <a name="request-parameters"></a><span data-ttu-id="661f6-126">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="661f6-126">Request parameters</span></span>

<span data-ttu-id="661f6-127">Name</span><span class="sxs-lookup"><span data-stu-id="661f6-127">Name</span></span>           | <span data-ttu-id="661f6-128">V</span><span class="sxs-lookup"><span data-stu-id="661f6-128">In</span></span>     | <span data-ttu-id="661f6-129">Typ</span><span class="sxs-lookup"><span data-stu-id="661f6-129">Type</span></span>   | <span data-ttu-id="661f6-130">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="661f6-130">Required</span></span> | <span data-ttu-id="661f6-131">Poznámky</span><span class="sxs-lookup"><span data-stu-id="661f6-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="661f6-132">X-NuGet – ApiKey</span><span class="sxs-lookup"><span data-stu-id="661f6-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="661f6-133">Hlavička</span><span class="sxs-lookup"><span data-stu-id="661f6-133">Header</span></span> | <span data-ttu-id="661f6-134">řetězec</span><span class="sxs-lookup"><span data-stu-id="661f6-134">string</span></span> | <span data-ttu-id="661f6-135">ano</span><span class="sxs-lookup"><span data-stu-id="661f6-135">yes</span></span>      | <span data-ttu-id="661f6-136">Například `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="661f6-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="661f6-137">Klíč rozhraní API je neprůhledný řetězec ze zdroje balíčku uživatelem a nakonfigurovaný do klienta.</span><span class="sxs-lookup"><span data-stu-id="661f6-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="661f6-138">Není k dispozici žádný konkrétní formát řetězce, ale délka klíče rozhraní API by neměla překročit rozumnou velikost pro hodnoty hlaviček protokolu HTTP.</span><span class="sxs-lookup"><span data-stu-id="661f6-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="661f6-139">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="661f6-139">Request body</span></span>

<span data-ttu-id="661f6-140">Text žádosti o nabízení oznámení je stejný jako text žádosti o nabízenou žádost balíčku (viz [push a DELETE balíčku](package-publish-resource.md)).</span><span class="sxs-lookup"><span data-stu-id="661f6-140">The request body for the symbol push is same as with the request body of a package push request (see [package push and delete](package-publish-resource.md)).</span></span> 

### <a name="response"></a><span data-ttu-id="661f6-141">Odpověď</span><span class="sxs-lookup"><span data-stu-id="661f6-141">Response</span></span>

<span data-ttu-id="661f6-142">Stavový kód</span><span class="sxs-lookup"><span data-stu-id="661f6-142">Status Code</span></span> | <span data-ttu-id="661f6-143">Význam</span><span class="sxs-lookup"><span data-stu-id="661f6-143">Meaning</span></span>
----------- | -------
<span data-ttu-id="661f6-144">201</span><span class="sxs-lookup"><span data-stu-id="661f6-144">201</span></span>         | <span data-ttu-id="661f6-145">Balíček symbolů byl úspěšně vložen.</span><span class="sxs-lookup"><span data-stu-id="661f6-145">The symbol package was successfully pushed.</span></span>
<span data-ttu-id="661f6-146">400</span><span class="sxs-lookup"><span data-stu-id="661f6-146">400</span></span>         | <span data-ttu-id="661f6-147">Poskytnutý balíček symbolů je neplatný.</span><span class="sxs-lookup"><span data-stu-id="661f6-147">The provided symbol package is invalid.</span></span>
<span data-ttu-id="661f6-148">401</span><span class="sxs-lookup"><span data-stu-id="661f6-148">401</span></span>         | <span data-ttu-id="661f6-149">Uživatel nemá autorizaci k provedení této akce.</span><span class="sxs-lookup"><span data-stu-id="661f6-149">The user is not authorized to perform this action.</span></span>
<span data-ttu-id="661f6-150">404</span><span class="sxs-lookup"><span data-stu-id="661f6-150">404</span></span>         | <span data-ttu-id="661f6-151">Odpovídající balíček se zadaným ID a verzí neexistuje.</span><span class="sxs-lookup"><span data-stu-id="661f6-151">A corresponding package with the provided ID and version does not exist.</span></span>
<span data-ttu-id="661f6-152">409</span><span class="sxs-lookup"><span data-stu-id="661f6-152">409</span></span>         | <span data-ttu-id="661f6-153">Balíček symbolů se zadaným ID a verzí byl vložen, ale ještě není k dispozici.</span><span class="sxs-lookup"><span data-stu-id="661f6-153">A symbol package with the provided ID and version was pushed but it is not available yet.</span></span>
<span data-ttu-id="661f6-154">413</span><span class="sxs-lookup"><span data-stu-id="661f6-154">413</span></span>         | <span data-ttu-id="661f6-155">Balíček je moc velký.</span><span class="sxs-lookup"><span data-stu-id="661f6-155">The package is too large.</span></span>

