---
title: Služba Index, NuGet rozhraní API
description: Index služby je vstupní bod rozhraní API HTTP NuGet a vytvoří výčet možností serveru.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 84e623e8480e4d17edad2ec3b2da6dcb6e53d21b
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822091"
---
# <a name="service-index"></a><span data-ttu-id="d62ed-103">Index služby</span><span class="sxs-lookup"><span data-stu-id="d62ed-103">Service index</span></span>

<span data-ttu-id="d62ed-104">Index služby je dokument JSON, který je vstupní bod pro zdroje balíčku NuGet a umožňuje implementace klienta ke zjištění schopnosti zdroji balíčku.</span><span class="sxs-lookup"><span data-stu-id="d62ed-104">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="d62ed-105">Index služby je objekt JSON s dvěma požadované vlastnosti: `version` (verze schématu indexu služby) a `resources` (koncových bodů nebo možnosti zdrojových souborů balíčku).</span><span class="sxs-lookup"><span data-stu-id="d62ed-105">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="d62ed-106">index služby nuget.org je umístěn v `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="d62ed-106">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="d62ed-107">Správa verzí</span><span class="sxs-lookup"><span data-stu-id="d62ed-107">Versioning</span></span>

<span data-ttu-id="d62ed-108">`version` Hodnota je řetězec parseable verze SemVer 2.0.0, který označuje verzi schématu indexu služby.</span><span class="sxs-lookup"><span data-stu-id="d62ed-108">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span> <span data-ttu-id="d62ed-109">Rozhraní API vyžaduje, aby řetězec verze má hlavní verzi počet `3`.</span><span class="sxs-lookup"><span data-stu-id="d62ed-109">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="d62ed-110">Při provedení změn pevné na schéma indexu služby, zvýší se podverze řetězec verze.</span><span class="sxs-lookup"><span data-stu-id="d62ed-110">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="d62ed-111">Každý prostředek v indexu služby je verzí nezávisle na verzi schématu indexu služby.</span><span class="sxs-lookup"><span data-stu-id="d62ed-111">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="d62ed-112">Aktuální verze schématu `3.0.0`.</span><span class="sxs-lookup"><span data-stu-id="d62ed-112">The current schema version is `3.0.0`.</span></span> <span data-ttu-id="d62ed-113">`3.0.0` Je funkčně srovnatelný starší verze `3.0.0-beta.1` verze ale měl by být upřednostňované zřetelněji komunikuje stabilní, definované schéma.</span><span class="sxs-lookup"><span data-stu-id="d62ed-113">The `3.0.0` version is functionally equivalent to the older `3.0.0-beta.1` version but should be preferred as it more clearly communicates the stable, defined schema.</span></span>

## <a name="http-methods"></a><span data-ttu-id="d62ed-114">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="d62ed-114">HTTP methods</span></span>

<span data-ttu-id="d62ed-115">Index služba je přístupná pomocí metody HTTP `GET` a `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="d62ed-115">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="d62ed-116">Prostředky</span><span class="sxs-lookup"><span data-stu-id="d62ed-116">Resources</span></span>

<span data-ttu-id="d62ed-117">`resources` Vlastnost obsahuje pole prostředků nepodporuje tento zdroj balíčku.</span><span class="sxs-lookup"><span data-stu-id="d62ed-117">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="d62ed-118">Prostředek</span><span class="sxs-lookup"><span data-stu-id="d62ed-118">Resource</span></span>

<span data-ttu-id="d62ed-119">Prostředek je objektem ve `resources` pole.</span><span class="sxs-lookup"><span data-stu-id="d62ed-119">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="d62ed-120">Reprezentuje verzí schopností zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="d62ed-120">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="d62ed-121">Prostředek má následující vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="d62ed-121">A resource has the following properties:</span></span>

<span data-ttu-id="d62ed-122">Název</span><span class="sxs-lookup"><span data-stu-id="d62ed-122">Name</span></span>          | <span data-ttu-id="d62ed-123">Typ</span><span class="sxs-lookup"><span data-stu-id="d62ed-123">Type</span></span>   | <span data-ttu-id="d62ed-124">Požadováno</span><span class="sxs-lookup"><span data-stu-id="d62ed-124">Required</span></span> | <span data-ttu-id="d62ed-125">Poznámky</span><span class="sxs-lookup"><span data-stu-id="d62ed-125">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="d62ed-126">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="d62ed-126">string</span></span> | <span data-ttu-id="d62ed-127">Ano</span><span class="sxs-lookup"><span data-stu-id="d62ed-127">yes</span></span>      | <span data-ttu-id="d62ed-128">Adresa URL prostředku</span><span class="sxs-lookup"><span data-stu-id="d62ed-128">The URL to the resource</span></span>
@type         | <span data-ttu-id="d62ed-129">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="d62ed-129">string</span></span> | <span data-ttu-id="d62ed-130">Ano</span><span class="sxs-lookup"><span data-stu-id="d62ed-130">yes</span></span>      | <span data-ttu-id="d62ed-131">Řetězcová konstanta představující typ prostředku</span><span class="sxs-lookup"><span data-stu-id="d62ed-131">A string constant representing the resource type</span></span>
<span data-ttu-id="d62ed-132">comment</span><span class="sxs-lookup"><span data-stu-id="d62ed-132">comment</span></span>       | <span data-ttu-id="d62ed-133">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="d62ed-133">string</span></span> | <span data-ttu-id="d62ed-134">Ne</span><span class="sxs-lookup"><span data-stu-id="d62ed-134">no</span></span>       | <span data-ttu-id="d62ed-135">Lidské čitelný popis prostředku</span><span class="sxs-lookup"><span data-stu-id="d62ed-135">A human readable description of the resource</span></span>

<span data-ttu-id="d62ed-136">`@id` Je adresa URL, která musí být absolutní a buď musí mít schéma protokolu HTTP nebo HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d62ed-136">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="d62ed-137">`@type` Slouží k identifikaci konkrétní protokol bude použit při interakci s prostředků.</span><span class="sxs-lookup"><span data-stu-id="d62ed-137">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="d62ed-138">Typ prostředku je neprůhledný řetězec, ale obvykle má formát:</span><span class="sxs-lookup"><span data-stu-id="d62ed-138">The type of the resource is an opaque string but generally has the format:</span></span>

    {RESOURCE_NAME}/{RESOURCE_VERSION}

<span data-ttu-id="d62ed-139">Klienti se očekává, pevné kódu `@type` hodnoty, pochopit a jejich vyhledat ve zdroji balíčku služby index.</span><span class="sxs-lookup"><span data-stu-id="d62ed-139">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="d62ed-140">Přesné `@type` hodnoty v současnosti jsou uvedené na dokumenty odkaz jednotlivých prostředků uvedené v [přehled rozhraní API](overview.md#resources-and-schema).</span><span class="sxs-lookup"><span data-stu-id="d62ed-140">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="d62ed-141">Z důvodu této dokumentace, bude v dokumentaci o různých prostředků v podstatě seskupené podle `{RESOURCE_NAME}` nachází v indexu služby, která je analogií seskupení podle scénáře.</span><span class="sxs-lookup"><span data-stu-id="d62ed-141">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="d62ed-142">Není potřeba, aby každý prostředek má jedinečnou `@id` nebo `@type`.</span><span class="sxs-lookup"><span data-stu-id="d62ed-142">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="d62ed-143">Je implementace klienta k určení, který prostředek se má přednost oproti jinému.</span><span class="sxs-lookup"><span data-stu-id="d62ed-143">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="d62ed-144">Jednou z možných implementací je, že prostředky na stejné nebo kompatibilní `@type` mohou být používány kruhového dotazování v případě selhání nebo serveru chyb připojení.</span><span class="sxs-lookup"><span data-stu-id="d62ed-144">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="d62ed-145">Ukázková žádost</span><span class="sxs-lookup"><span data-stu-id="d62ed-145">Sample request</span></span>

<span data-ttu-id="d62ed-146">GET https://api.nuget.org/v3/index.json</span><span class="sxs-lookup"><span data-stu-id="d62ed-146">GET https://api.nuget.org/v3/index.json</span></span>

### <a name="sample-response"></a><span data-ttu-id="d62ed-147">Ukázková odpověď</span><span class="sxs-lookup"><span data-stu-id="d62ed-147">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]