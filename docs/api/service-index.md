---
title: Index služby, rozhraní API NuGet
description: Index služby je vstupním bodem rozhraní NuGet HTTP API a vytvoří výčet schopností serveru.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: c2d4d23313c80c24b537b1df227a9cea6784ef6e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775352"
---
# <a name="service-index"></a><span data-ttu-id="c0217-103">Index služby</span><span class="sxs-lookup"><span data-stu-id="c0217-103">Service index</span></span>

<span data-ttu-id="c0217-104">Index služby je dokument JSON, který je vstupním bodem pro zdroj balíčku NuGet a umožňuje implementaci klienta zjistit možnosti zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="c0217-104">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="c0217-105">Index služby je objekt JSON se dvěma požadovanými vlastnostmi: `version` (verze schématu indexu služby) a `resources`  (koncové body nebo funkce zdroje balíčku).</span><span class="sxs-lookup"><span data-stu-id="c0217-105">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="c0217-106">index služby NuGet. org je umístěný na adrese `https://api.nuget.org/v3/index.json` .</span><span class="sxs-lookup"><span data-stu-id="c0217-106">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="c0217-107">Správa verzí</span><span class="sxs-lookup"><span data-stu-id="c0217-107">Versioning</span></span>

<span data-ttu-id="c0217-108">`version`Hodnota je řetězec SemVer 2.0.0 s analýzou verze, který označuje verzi schématu indexu služby.</span><span class="sxs-lookup"><span data-stu-id="c0217-108">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span> <span data-ttu-id="c0217-109">Rozhraní API vyžaduje, aby řetězec verze měl hlavní číslo verze `3` .</span><span class="sxs-lookup"><span data-stu-id="c0217-109">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="c0217-110">V rámci schématu indexu služby budou provedeny nepodstatné změny, ale zvýší se vedlejší verze řetězce verze.</span><span class="sxs-lookup"><span data-stu-id="c0217-110">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="c0217-111">Každý prostředek v indexu služby je nezávisle na verzi schématu indexu služby.</span><span class="sxs-lookup"><span data-stu-id="c0217-111">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="c0217-112">Aktuální verze schématu je `3.0.0` .</span><span class="sxs-lookup"><span data-stu-id="c0217-112">The current schema version is `3.0.0`.</span></span> <span data-ttu-id="c0217-113">`3.0.0`Verze je funkčně ekvivalentní starší `3.0.0-beta.1` verzi, ale měla by být preferována, protože lépe komunikuje stabilní, definované schéma.</span><span class="sxs-lookup"><span data-stu-id="c0217-113">The `3.0.0` version is functionally equivalent to the older `3.0.0-beta.1` version but should be preferred as it more clearly communicates the stable, defined schema.</span></span>

## <a name="http-methods"></a><span data-ttu-id="c0217-114">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="c0217-114">HTTP methods</span></span>

<span data-ttu-id="c0217-115">Index služby je přístupný pomocí metod HTTP `GET` a `HEAD` .</span><span class="sxs-lookup"><span data-stu-id="c0217-115">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="c0217-116">Zdroje</span><span class="sxs-lookup"><span data-stu-id="c0217-116">Resources</span></span>

<span data-ttu-id="c0217-117">`resources`Vlastnost obsahuje pole prostředků podporované tímto zdrojem balíčku.</span><span class="sxs-lookup"><span data-stu-id="c0217-117">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="c0217-118">Prostředek</span><span class="sxs-lookup"><span data-stu-id="c0217-118">Resource</span></span>

<span data-ttu-id="c0217-119">Prostředek je objekt v poli `resources` .</span><span class="sxs-lookup"><span data-stu-id="c0217-119">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="c0217-120">Představuje možnost verze zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="c0217-120">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="c0217-121">Prostředek má následující vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="c0217-121">A resource has the following properties:</span></span>

<span data-ttu-id="c0217-122">Název</span><span class="sxs-lookup"><span data-stu-id="c0217-122">Name</span></span>          | <span data-ttu-id="c0217-123">Typ</span><span class="sxs-lookup"><span data-stu-id="c0217-123">Type</span></span>   | <span data-ttu-id="c0217-124">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="c0217-124">Required</span></span> | <span data-ttu-id="c0217-125">Poznámky</span><span class="sxs-lookup"><span data-stu-id="c0217-125">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="c0217-126">řetězec</span><span class="sxs-lookup"><span data-stu-id="c0217-126">string</span></span> | <span data-ttu-id="c0217-127">ano</span><span class="sxs-lookup"><span data-stu-id="c0217-127">yes</span></span>      | <span data-ttu-id="c0217-128">Adresa URL prostředku</span><span class="sxs-lookup"><span data-stu-id="c0217-128">The URL to the resource</span></span>
@type         | <span data-ttu-id="c0217-129">řetězec</span><span class="sxs-lookup"><span data-stu-id="c0217-129">string</span></span> | <span data-ttu-id="c0217-130">ano</span><span class="sxs-lookup"><span data-stu-id="c0217-130">yes</span></span>      | <span data-ttu-id="c0217-131">Řetězcová konstanta představující typ prostředku</span><span class="sxs-lookup"><span data-stu-id="c0217-131">A string constant representing the resource type</span></span>
<span data-ttu-id="c0217-132">comment</span><span class="sxs-lookup"><span data-stu-id="c0217-132">comment</span></span>       | <span data-ttu-id="c0217-133">řetězec</span><span class="sxs-lookup"><span data-stu-id="c0217-133">string</span></span> | <span data-ttu-id="c0217-134">ne</span><span class="sxs-lookup"><span data-stu-id="c0217-134">no</span></span>       | <span data-ttu-id="c0217-135">Lidský čitelný popis prostředku</span><span class="sxs-lookup"><span data-stu-id="c0217-135">A human readable description of the resource</span></span>

<span data-ttu-id="c0217-136">`@id`Je adresa URL, která musí být absolutní a musí mít buď schéma HTTP, nebo HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c0217-136">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="c0217-137">`@type`Slouží k identifikaci konkrétního protokolu, který se má použít při interakci s prostředkem.</span><span class="sxs-lookup"><span data-stu-id="c0217-137">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="c0217-138">Typ prostředku je neprůhledný řetězec, ale obecně má formát:</span><span class="sxs-lookup"><span data-stu-id="c0217-138">The type of the resource is an opaque string but generally has the format:</span></span>

```
{RESOURCE_NAME}/{RESOURCE_VERSION}
```

<span data-ttu-id="c0217-139">U klientů se očekává, že budou zakódovat `@type` hodnoty, které znají, a vyhledají je v indexu služby zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="c0217-139">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="c0217-140">Přesné `@type` hodnoty používané v současnosti jsou vyhodnoceny na základě dokumentů odkazů na jednotlivé prostředky, které jsou uvedeny v [přehledu rozhraní API](overview.md#resources-and-schema).</span><span class="sxs-lookup"><span data-stu-id="c0217-140">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="c0217-141">V této dokumentaci se dokumentace k různým prostředkům v podstatě seskupí podle toho, jak se `{RESOURCE_NAME}` nachází v indexu služby, což je analogické seskupení podle scénáře.</span><span class="sxs-lookup"><span data-stu-id="c0217-141">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="c0217-142">Neexistuje žádný požadavek, aby každý prostředek měl jedinečný `@id` nebo `@type` .</span><span class="sxs-lookup"><span data-stu-id="c0217-142">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="c0217-143">Je k tomu implementace klienta, aby bylo možné určit, který prostředek se má preferovat jiným.</span><span class="sxs-lookup"><span data-stu-id="c0217-143">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="c0217-144">Jednou z možných implementací je, že prostředky stejného nebo kompatibilního typu se `@type` dají použít v kruhovém dotazování v případě selhání připojení nebo chyby serveru.</span><span class="sxs-lookup"><span data-stu-id="c0217-144">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="c0217-145">Ukázková žádost</span><span class="sxs-lookup"><span data-stu-id="c0217-145">Sample request</span></span>

```
GET https://api.nuget.org/v3/index.json
```

### <a name="sample-response"></a><span data-ttu-id="c0217-146">Ukázková odpověď</span><span class="sxs-lookup"><span data-stu-id="c0217-146">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]
