---
title: Index služby, NuGet rozhraní API | Microsoft Docs
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
ms.technology: ''
description: Index služby je vstupní bod rozhraní API HTTP NuGet a vytvoří výčet možností serveru.
keywords: Rozhraní API NuGet vstupní bod, NuGetA PI koncový bod zjišťování
ms.reviewer:
- karann
- unnir
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 1c1dea25067cc582a14a0dd22c2f3f7f70d40a02
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="service-index"></a><span data-ttu-id="bbdde-104">Index služby</span><span class="sxs-lookup"><span data-stu-id="bbdde-104">Service index</span></span>

<span data-ttu-id="bbdde-105">Index služby je dokument JSON, který je vstupní bod pro zdroje balíčku NuGet a umožňuje implementace klienta ke zjištění schopnosti zdroji balíčku.</span><span class="sxs-lookup"><span data-stu-id="bbdde-105">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="bbdde-106">Index služby je objekt JSON s dvěma požadované vlastnosti: `version` (verze schématu indexu služby) a `resources` (koncových bodů nebo možnosti zdrojových souborů balíčku).</span><span class="sxs-lookup"><span data-stu-id="bbdde-106">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="bbdde-107">index služby nuget.org je umístěn v `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="bbdde-107">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="bbdde-108">Správa verzí</span><span class="sxs-lookup"><span data-stu-id="bbdde-108">Versioning</span></span>

<span data-ttu-id="bbdde-109">`version` Hodnota je řetězec parseable verze SemVer 2.0.0, který označuje verzi schématu indexu služby.</span><span class="sxs-lookup"><span data-stu-id="bbdde-109">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span> <span data-ttu-id="bbdde-110">Rozhraní API vyžaduje, aby řetězec verze má hlavní verzi počet `3`.</span><span class="sxs-lookup"><span data-stu-id="bbdde-110">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="bbdde-111">Při provedení změn pevné na schéma indexu služby, zvýší se podverze řetězec verze.</span><span class="sxs-lookup"><span data-stu-id="bbdde-111">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="bbdde-112">Každý prostředek v indexu služby je verzí nezávisle na verzi schématu indexu služby.</span><span class="sxs-lookup"><span data-stu-id="bbdde-112">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="bbdde-113">Aktuální verze schématu `3.0.0`.</span><span class="sxs-lookup"><span data-stu-id="bbdde-113">The current schema version is `3.0.0`.</span></span> <span data-ttu-id="bbdde-114">`3.0.0` Je funkčně srovnatelný starší verze `3.0.0-beta.1` verze ale měl by být upřednostňované zřetelněji komunikuje stabilní, definované schéma.</span><span class="sxs-lookup"><span data-stu-id="bbdde-114">The `3.0.0` version is functionally equivalent to the older `3.0.0-beta.1` version but should be preferred as it more clearly communicates the stable, defined schema.</span></span>

## <a name="http-methods"></a><span data-ttu-id="bbdde-115">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="bbdde-115">HTTP methods</span></span>

<span data-ttu-id="bbdde-116">Index služba je přístupná pomocí metody HTTP `GET` a `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="bbdde-116">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="bbdde-117">Prostředky</span><span class="sxs-lookup"><span data-stu-id="bbdde-117">Resources</span></span>

<span data-ttu-id="bbdde-118">`resources` Vlastnost obsahuje pole prostředků nepodporuje tento zdroj balíčku.</span><span class="sxs-lookup"><span data-stu-id="bbdde-118">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="bbdde-119">Prostředek</span><span class="sxs-lookup"><span data-stu-id="bbdde-119">Resource</span></span>

<span data-ttu-id="bbdde-120">Prostředek je objektem ve `resources` pole.</span><span class="sxs-lookup"><span data-stu-id="bbdde-120">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="bbdde-121">Reprezentuje verzí schopností zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="bbdde-121">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="bbdde-122">Prostředek má následující vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="bbdde-122">A resource has the following properties:</span></span>

<span data-ttu-id="bbdde-123">Název</span><span class="sxs-lookup"><span data-stu-id="bbdde-123">Name</span></span>          | <span data-ttu-id="bbdde-124">Typ</span><span class="sxs-lookup"><span data-stu-id="bbdde-124">Type</span></span>   | <span data-ttu-id="bbdde-125">Požadováno</span><span class="sxs-lookup"><span data-stu-id="bbdde-125">Required</span></span> | <span data-ttu-id="bbdde-126">Poznámky</span><span class="sxs-lookup"><span data-stu-id="bbdde-126">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="bbdde-127">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="bbdde-127">string</span></span> | <span data-ttu-id="bbdde-128">Ano</span><span class="sxs-lookup"><span data-stu-id="bbdde-128">yes</span></span>      | <span data-ttu-id="bbdde-129">Adresa URL prostředku</span><span class="sxs-lookup"><span data-stu-id="bbdde-129">The URL to the resource</span></span>
@type         | <span data-ttu-id="bbdde-130">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="bbdde-130">string</span></span> | <span data-ttu-id="bbdde-131">Ano</span><span class="sxs-lookup"><span data-stu-id="bbdde-131">yes</span></span>      | <span data-ttu-id="bbdde-132">Řetězcová konstanta představující typ prostředku</span><span class="sxs-lookup"><span data-stu-id="bbdde-132">A string constant representing the resource type</span></span>
<span data-ttu-id="bbdde-133">comment</span><span class="sxs-lookup"><span data-stu-id="bbdde-133">comment</span></span>       | <span data-ttu-id="bbdde-134">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="bbdde-134">string</span></span> | <span data-ttu-id="bbdde-135">Ne</span><span class="sxs-lookup"><span data-stu-id="bbdde-135">no</span></span>       | <span data-ttu-id="bbdde-136">Lidské čitelný popis prostředku</span><span class="sxs-lookup"><span data-stu-id="bbdde-136">A human readable description of the resource</span></span>

<span data-ttu-id="bbdde-137">`@id` Je adresa URL, která musí být absolutní a buď musí mít schéma protokolu HTTP nebo HTTPS.</span><span class="sxs-lookup"><span data-stu-id="bbdde-137">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="bbdde-138">`@type` Slouží k identifikaci konkrétní protokol bude použit při interakci s prostředků.</span><span class="sxs-lookup"><span data-stu-id="bbdde-138">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="bbdde-139">Typ prostředku je neprůhledný řetězec, ale obvykle má formát:</span><span class="sxs-lookup"><span data-stu-id="bbdde-139">The type of the resource is an opaque string but generally has the format:</span></span>

    {RESOURCE_NAME}/{RESOURCE_VERSION}

<span data-ttu-id="bbdde-140">Klienti se očekává, pevné kódu `@type` hodnoty, pochopit a jejich vyhledat ve zdroji balíčku služby index.</span><span class="sxs-lookup"><span data-stu-id="bbdde-140">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="bbdde-141">Přesné `@type` hodnoty v současnosti jsou uvedené na dokumenty odkaz jednotlivých prostředků uvedené v [přehled rozhraní API](overview.md#resources-and-schema).</span><span class="sxs-lookup"><span data-stu-id="bbdde-141">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="bbdde-142">Z důvodu této dokumentace, bude v dokumentaci o různých prostředků v podstatě seskupené podle `{RESOURCE_NAME}` nachází v indexu služby, která je analogií seskupení podle scénáře.</span><span class="sxs-lookup"><span data-stu-id="bbdde-142">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="bbdde-143">Není potřeba, aby každý prostředek má jedinečnou `@id` nebo `@type`.</span><span class="sxs-lookup"><span data-stu-id="bbdde-143">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="bbdde-144">Je implementace klienta k určení, který prostředek se má přednost oproti jinému.</span><span class="sxs-lookup"><span data-stu-id="bbdde-144">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="bbdde-145">Jednou z možných implementací je, že prostředky na stejné nebo kompatibilní `@type` mohou být používány kruhového dotazování v případě selhání nebo serveru chyb připojení.</span><span class="sxs-lookup"><span data-stu-id="bbdde-145">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="bbdde-146">Ukázková žádost</span><span class="sxs-lookup"><span data-stu-id="bbdde-146">Sample request</span></span>

<span data-ttu-id="bbdde-147">GET https://api.nuget.org/v3/index.json</span><span class="sxs-lookup"><span data-stu-id="bbdde-147">GET https://api.nuget.org/v3/index.json</span></span>

### <a name="sample-response"></a><span data-ttu-id="bbdde-148">Ukázková odpověď</span><span class="sxs-lookup"><span data-stu-id="bbdde-148">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]
