---
title: Služba Index, rozhraní API Nugetu
description: Index služby je vstupní bod rozhraní API HTTP NuGet a vytváří výčet možností serveru.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1dcfb87690b728280b494d4434f9c1d7ee7a7e74
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324718"
---
# <a name="service-index"></a><span data-ttu-id="92e17-103">Index služby</span><span class="sxs-lookup"><span data-stu-id="92e17-103">Service index</span></span>

<span data-ttu-id="92e17-104">Index služby je dokument JSON, který je vstupním bodem pro zdroj balíčku NuGet a umožňuje implementace klienta ke zjištění schopnosti zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="92e17-104">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="92e17-105">Index služby je objekt JSON s dvěma požadované vlastnosti: `version` (verze schématu indexu služby) a `resources` (koncové body nebo možnosti zdroje balíčku).</span><span class="sxs-lookup"><span data-stu-id="92e17-105">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="92e17-106">index služby nuget.org se nachází na `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="92e17-106">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="92e17-107">Správa verzí</span><span class="sxs-lookup"><span data-stu-id="92e17-107">Versioning</span></span>

<span data-ttu-id="92e17-108">`version` Hodnota je řetězec SemVer 2.0.0 parseable verze, který označuje verzi schématu indexu služby.</span><span class="sxs-lookup"><span data-stu-id="92e17-108">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span> <span data-ttu-id="92e17-109">Rozhraní API Určuje, zda má řetězec verze číslo hlavní verze `3`.</span><span class="sxs-lookup"><span data-stu-id="92e17-109">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="92e17-110">Jak nevýznamných změn schématu indexu služby, zvýší se verze řetězec podverze.</span><span class="sxs-lookup"><span data-stu-id="92e17-110">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="92e17-111">Každý prostředek v indexu služby je označené verzí odděleně od verze schématu indexu služby.</span><span class="sxs-lookup"><span data-stu-id="92e17-111">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="92e17-112">Aktuální verze schématu `3.0.0`.</span><span class="sxs-lookup"><span data-stu-id="92e17-112">The current schema version is `3.0.0`.</span></span> <span data-ttu-id="92e17-113">`3.0.0` Je funkčně srovnatelný s starší verze `3.0.0-beta.1` verze, ale se bude upřednostňovat jako jasněji komunikuje stabilní, definice schématu.</span><span class="sxs-lookup"><span data-stu-id="92e17-113">The `3.0.0` version is functionally equivalent to the older `3.0.0-beta.1` version but should be preferred as it more clearly communicates the stable, defined schema.</span></span>

## <a name="http-methods"></a><span data-ttu-id="92e17-114">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="92e17-114">HTTP methods</span></span>

<span data-ttu-id="92e17-115">Index služby je přístupný pomocí metody HTTP `GET` a `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="92e17-115">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="92e17-116">Prostředky</span><span class="sxs-lookup"><span data-stu-id="92e17-116">Resources</span></span>

<span data-ttu-id="92e17-117">`resources` Vlastnost obsahuje celou řadu prostředků nepodporuje zdroje tohoto balíčku.</span><span class="sxs-lookup"><span data-stu-id="92e17-117">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="92e17-118">Prostředek</span><span class="sxs-lookup"><span data-stu-id="92e17-118">Resource</span></span>

<span data-ttu-id="92e17-119">Prostředek je objekt `resources` pole.</span><span class="sxs-lookup"><span data-stu-id="92e17-119">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="92e17-120">Představuje systémovou správou verzí možnost zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="92e17-120">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="92e17-121">Prostředek má následující vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="92e17-121">A resource has the following properties:</span></span>

<span data-ttu-id="92e17-122">Název</span><span class="sxs-lookup"><span data-stu-id="92e17-122">Name</span></span>          | <span data-ttu-id="92e17-123">Typ</span><span class="sxs-lookup"><span data-stu-id="92e17-123">Type</span></span>   | <span data-ttu-id="92e17-124">Požadováno</span><span class="sxs-lookup"><span data-stu-id="92e17-124">Required</span></span> | <span data-ttu-id="92e17-125">Poznámky</span><span class="sxs-lookup"><span data-stu-id="92e17-125">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="92e17-126">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="92e17-126">string</span></span> | <span data-ttu-id="92e17-127">ano</span><span class="sxs-lookup"><span data-stu-id="92e17-127">yes</span></span>      | <span data-ttu-id="92e17-128">Adresa URL k prostředku</span><span class="sxs-lookup"><span data-stu-id="92e17-128">The URL to the resource</span></span>
@type         | <span data-ttu-id="92e17-129">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="92e17-129">string</span></span> | <span data-ttu-id="92e17-130">ano</span><span class="sxs-lookup"><span data-stu-id="92e17-130">yes</span></span>      | <span data-ttu-id="92e17-131">Konstanta řetězec představující typ prostředku</span><span class="sxs-lookup"><span data-stu-id="92e17-131">A string constant representing the resource type</span></span>
<span data-ttu-id="92e17-132">comment</span><span class="sxs-lookup"><span data-stu-id="92e17-132">comment</span></span>       | <span data-ttu-id="92e17-133">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="92e17-133">string</span></span> | <span data-ttu-id="92e17-134">Ne</span><span class="sxs-lookup"><span data-stu-id="92e17-134">no</span></span>       | <span data-ttu-id="92e17-135">Lidské čitelný popis prostředku</span><span class="sxs-lookup"><span data-stu-id="92e17-135">A human readable description of the resource</span></span>

<span data-ttu-id="92e17-136">`@id` Je adresa URL, která musí být absolutní a musí mít schéma HTTP nebo HTTPS.</span><span class="sxs-lookup"><span data-stu-id="92e17-136">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="92e17-137">`@type` Slouží k identifikaci konkrétní protokol bude použit při interakci s prostředkem.</span><span class="sxs-lookup"><span data-stu-id="92e17-137">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="92e17-138">Typ prostředku je neprůhledný řetězec, ale obvykle má formát:</span><span class="sxs-lookup"><span data-stu-id="92e17-138">The type of the resource is an opaque string but generally has the format:</span></span>

    {RESOURCE_NAME}/{RESOURCE_VERSION}

<span data-ttu-id="92e17-139">Klienti se očekává pevný kód `@type` hodnoty mají přehled a je vyhledat v indexu služby zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="92e17-139">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="92e17-140">Přesné `@type` hodnoty v současnosti jsou uvedené na referenční dokumenty jednotlivé prostředky uvedené v [přehled rozhraní API](overview.md#resources-and-schema).</span><span class="sxs-lookup"><span data-stu-id="92e17-140">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="92e17-141">Pro účely této dokumentaci, se v dokumentaci k různým prostředkům v podstatě seskupené podle `{RESOURCE_NAME}` v indexu služby, která je analogií seskupení podle scénáře.</span><span class="sxs-lookup"><span data-stu-id="92e17-141">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="92e17-142">Neexistuje žádný požadavek, že každý prostředek má jedinečnou `@id` nebo `@type`.</span><span class="sxs-lookup"><span data-stu-id="92e17-142">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="92e17-143">Je implementace klienta, chcete-li určit, který prostředek se má přednost před jiným.</span><span class="sxs-lookup"><span data-stu-id="92e17-143">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="92e17-144">Jednu možnou implementaci je, že prostředky se stejným nebo kompatibilní `@type` lze použít v vždy střídat dokola v případě selhání nebo serveru chyb připojení.</span><span class="sxs-lookup"><span data-stu-id="92e17-144">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="92e17-145">Ukázková žádost</span><span class="sxs-lookup"><span data-stu-id="92e17-145">Sample request</span></span>

    GET https://api.nuget.org/v3/index.json

### <a name="sample-response"></a><span data-ttu-id="92e17-146">Ukázková odpověď</span><span class="sxs-lookup"><span data-stu-id="92e17-146">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]
