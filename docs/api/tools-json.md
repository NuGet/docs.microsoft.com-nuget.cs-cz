---
title: Tools.JSON pro zjišťování nuget.exe verze
description: Koncový bod pro
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: 6184fe8e987e0637cb912999f2e3fa3a3dc9b4ba
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546932"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a><span data-ttu-id="88ae5-103">Tools.JSON pro zjišťování nuget.exe verze</span><span class="sxs-lookup"><span data-stu-id="88ae5-103">tools.json for discovering nuget.exe versions</span></span>

<span data-ttu-id="88ae5-104">V současné době existuje několik způsobů, jak získat nejnovější verzi programu nuget.exe na svém počítači skriptovatelný způsobem.</span><span class="sxs-lookup"><span data-stu-id="88ae5-104">Today, there are a few ways to get the latest version of nuget.exe on your machine in a scriptable fashion.</span></span> <span data-ttu-id="88ae5-105">Například můžete stáhnout a extrahovat [ `NuGet.CommandLine` ](https://www.nuget.org/packages/NuGet.CommandLine/) balíček z webu nuget.org. To má některé složitost, protože se buď vyžaduje, že už máte nuget.exe (pro `nuget.exe install`) nebo máte rozbalit .nupkg nástrojem základní unzip a vyhledejte binární vnitřní.</span><span class="sxs-lookup"><span data-stu-id="88ae5-105">For example, you can download and extract the [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package from nuget.org. This has some complexity since it either requires that you already have nuget.exe (for `nuget.exe install`) or you have to unzip the .nupkg using a basic unzip tool and find the binary inside.</span></span>

<span data-ttu-id="88ae5-106">Pokud už máte nuget.exe, můžete také použít `nuget.exe update -self`, ale tento proces také vyžaduje s existující kopie nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="88ae5-106">If you already have nuget.exe, you can also use `nuget.exe update -self`, however this also requires having an existing copy of nuget.exe.</span></span> <span data-ttu-id="88ae5-107">Tento přístup můžete rovněž aktualizuje na nejnovější verzi.</span><span class="sxs-lookup"><span data-stu-id="88ae5-107">This approach also updates you to the latest version.</span></span> <span data-ttu-id="88ae5-108">Neumožňuje použít konkrétní verzi.</span><span class="sxs-lookup"><span data-stu-id="88ae5-108">It does not allow the use of a specific version.</span></span>

<span data-ttu-id="88ae5-109">`tools.json` Koncový bod je k dispozici pro obě samozaváděcí problém vyřešit a poskytnout kontrolu verze programu nuget.exe, který můžete stáhnout.</span><span class="sxs-lookup"><span data-stu-id="88ae5-109">The `tools.json` endpoint is available to both solve the bootstrapping problem and to give control of the version of nuget.exe that you download.</span></span> <span data-ttu-id="88ae5-110">To lze vyhledat a stáhnout všechny vydané verze programu nuget.exe použít v prostředích CI/CD nebo vlastní skripty.</span><span class="sxs-lookup"><span data-stu-id="88ae5-110">This can be used in CI/CD environments or in custom scripts to discover and download any released version of nuget.exe.</span></span>

<span data-ttu-id="88ae5-111">`tools.json` Koncového bodu můžete načíst pomocí neověřené žádosti protokolu HTTP (například `Invoke-WebRequest` v prostředí PowerShell nebo `wget`).</span><span class="sxs-lookup"><span data-stu-id="88ae5-111">The `tools.json` endpoint can be fetched using an unauthenticated HTTP request (e.g. `Invoke-WebRequest` in PowerShell or `wget`).</span></span> <span data-ttu-id="88ae5-112">Může být analyzován pomocí deserializátor JSON a následné nuget.exe pro stažení adresy URL můžete načíst taky pomocí neověřené požadavky HTTP.</span><span class="sxs-lookup"><span data-stu-id="88ae5-112">It can be parsed using a JSON deserializer and subsequent nuget.exe download URLs can also be fetched using unauthenticated HTTP requests.</span></span>

<span data-ttu-id="88ae5-113">Koncový bod můžete načíst pomocí `GET` metody:</span><span class="sxs-lookup"><span data-stu-id="88ae5-113">The endpoint can be fetched using the `GET` method:</span></span>

    GET https://dist.nuget.org/tools.json

<span data-ttu-id="88ae5-114">[Schématu JSON](http://json-schema.org/) pro koncový bod je k dispozici zde:</span><span class="sxs-lookup"><span data-stu-id="88ae5-114">The [JSON schema](http://json-schema.org/) for the endpoint is available here:</span></span>

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a><span data-ttu-id="88ae5-115">Odpověď</span><span class="sxs-lookup"><span data-stu-id="88ae5-115">Response</span></span>

<span data-ttu-id="88ae5-116">Odpověď je dokument JSON obsahující všechny dostupné verze programu nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="88ae5-116">The response is a JSON document containing all of the available versions of nuget.exe.</span></span>

<span data-ttu-id="88ae5-117">Kořenový objekt JSON má následující vlastnost:</span><span class="sxs-lookup"><span data-stu-id="88ae5-117">The root JSON object has the following property:</span></span>

<span data-ttu-id="88ae5-118">Název</span><span class="sxs-lookup"><span data-stu-id="88ae5-118">Name</span></span>      | <span data-ttu-id="88ae5-119">Typ</span><span class="sxs-lookup"><span data-stu-id="88ae5-119">Type</span></span>             | <span data-ttu-id="88ae5-120">Požadováno</span><span class="sxs-lookup"><span data-stu-id="88ae5-120">Required</span></span>
--------- | ---------------- | --------
<span data-ttu-id="88ae5-121">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="88ae5-121">nuget.exe</span></span> | <span data-ttu-id="88ae5-122">Pole objektů</span><span class="sxs-lookup"><span data-stu-id="88ae5-122">array of objects</span></span> | <span data-ttu-id="88ae5-123">Ano</span><span class="sxs-lookup"><span data-stu-id="88ae5-123">yes</span></span>

<span data-ttu-id="88ae5-124">Každý objekt v `nuget.exe` pole má následující vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="88ae5-124">Each object in the `nuget.exe` array has the following properties:</span></span>

<span data-ttu-id="88ae5-125">Název</span><span class="sxs-lookup"><span data-stu-id="88ae5-125">Name</span></span>     | <span data-ttu-id="88ae5-126">Typ</span><span class="sxs-lookup"><span data-stu-id="88ae5-126">Type</span></span>   | <span data-ttu-id="88ae5-127">Požadováno</span><span class="sxs-lookup"><span data-stu-id="88ae5-127">Required</span></span> | <span data-ttu-id="88ae5-128">Poznámky</span><span class="sxs-lookup"><span data-stu-id="88ae5-128">Notes</span></span>
-------- | ------ | -------- | -----
<span data-ttu-id="88ae5-129">verze</span><span class="sxs-lookup"><span data-stu-id="88ae5-129">version</span></span>  | <span data-ttu-id="88ae5-130">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="88ae5-130">string</span></span> | <span data-ttu-id="88ae5-131">Ano</span><span class="sxs-lookup"><span data-stu-id="88ae5-131">yes</span></span>      | <span data-ttu-id="88ae5-132">Řetězec SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="88ae5-132">A SemVer 2.0.0 string</span></span>
<span data-ttu-id="88ae5-133">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="88ae5-133">url</span></span>      | <span data-ttu-id="88ae5-134">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="88ae5-134">string</span></span> | <span data-ttu-id="88ae5-135">Ano</span><span class="sxs-lookup"><span data-stu-id="88ae5-135">yes</span></span>      | <span data-ttu-id="88ae5-136">Absolutní adresa URL pro stahování tato verze programu nuget.exe</span><span class="sxs-lookup"><span data-stu-id="88ae5-136">An absolute URL for downloading this version of nuget.exe</span></span>
<span data-ttu-id="88ae5-137">fáze</span><span class="sxs-lookup"><span data-stu-id="88ae5-137">stage</span></span>    | <span data-ttu-id="88ae5-138">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="88ae5-138">string</span></span> | <span data-ttu-id="88ae5-139">Ano</span><span class="sxs-lookup"><span data-stu-id="88ae5-139">yes</span></span>      | <span data-ttu-id="88ae5-140">Řetězec výčtu</span><span class="sxs-lookup"><span data-stu-id="88ae5-140">An enum string</span></span>
<span data-ttu-id="88ae5-141">Nahrání</span><span class="sxs-lookup"><span data-stu-id="88ae5-141">uploaded</span></span> | <span data-ttu-id="88ae5-142">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="88ae5-142">string</span></span> | <span data-ttu-id="88ae5-143">Ano</span><span class="sxs-lookup"><span data-stu-id="88ae5-143">yes</span></span>      | <span data-ttu-id="88ae5-144">Přibližné časové razítko z verze kdy byl k dispozici</span><span class="sxs-lookup"><span data-stu-id="88ae5-144">An approximate timestamp of when the version was made available</span></span>

<span data-ttu-id="88ae5-145">Položky v poli budou seřazeny v sestupném pořadí SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="88ae5-145">The items in the array will be sorted in descending, SemVer 2.0.0 order.</span></span> <span data-ttu-id="88ae5-146">Tuto záruku je určená pro usnadnění zatížení na klientovi hledáte nejnovější verzi.</span><span class="sxs-lookup"><span data-stu-id="88ae5-146">This guarantee is meant to ease the burden on a client looking for the latest version.</span></span> 

<span data-ttu-id="88ae5-147">`stage` Vlastnost určuje, jak vettect tato verze nástroje je.</span><span class="sxs-lookup"><span data-stu-id="88ae5-147">The `stage` property indicates how vettect this version of the tool is.</span></span> 

<span data-ttu-id="88ae5-148">fáze</span><span class="sxs-lookup"><span data-stu-id="88ae5-148">Stage</span></span>              | <span data-ttu-id="88ae5-149">Význam</span><span class="sxs-lookup"><span data-stu-id="88ae5-149">Meaning</span></span>
------------------ | ------
<span data-ttu-id="88ae5-150">EarlyAccessPreview</span><span class="sxs-lookup"><span data-stu-id="88ae5-150">EarlyAccessPreview</span></span> | <span data-ttu-id="88ae5-151">Nejsou ještě viditelné na [webové stránce pro stažení](https://www.nuget.org/downloads) a by měl být ověřen od partnerů</span><span class="sxs-lookup"><span data-stu-id="88ae5-151">Not yet visible on the [download web page](https://www.nuget.org/downloads) and should be validated by partners</span></span>
<span data-ttu-id="88ae5-152">Všeobecně dostupné</span><span class="sxs-lookup"><span data-stu-id="88ae5-152">Released</span></span>           | <span data-ttu-id="88ae5-153">K dispozici na webu Stažení ale ještě není doporučeno pro šíření celou spotřebu</span><span class="sxs-lookup"><span data-stu-id="88ae5-153">Available on the download site but is not yet recommended for wide-spread consumption</span></span>
<span data-ttu-id="88ae5-154">ReleasedAndBlessed</span><span class="sxs-lookup"><span data-stu-id="88ae5-154">ReleasedAndBlessed</span></span> | <span data-ttu-id="88ae5-155">K dispozici na serveru pro stahování a je doporučena pro využití</span><span class="sxs-lookup"><span data-stu-id="88ae5-155">Available on the download site and is recommended for consumption</span></span>

<span data-ttu-id="88ae5-156">Jeden jednoduchým přístupem k nutnosti na nejnovější verzi, doporučená verze je v seznamu, který se má provést první verze `stage` hodnotu `ReleasedAndBlessed`.</span><span class="sxs-lookup"><span data-stu-id="88ae5-156">One simple approach for having the latest, recommended version is to take the first version in the list that has the `stage` value of `ReleasedAndBlessed`.</span></span>

<span data-ttu-id="88ae5-157">`NuGet.CommandLine` Balíčků na nuget.org je obvykle pouze aktualizován `ReleasedAndBlessed` verze.</span><span class="sxs-lookup"><span data-stu-id="88ae5-157">The `NuGet.CommandLine` package on nuget.org is typically only updated with `ReleasedAndBlessed` versions.</span></span>

### <a name="sample-request"></a><span data-ttu-id="88ae5-158">Ukázková žádost</span><span class="sxs-lookup"><span data-stu-id="88ae5-158">Sample request</span></span>

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a><span data-ttu-id="88ae5-159">Ukázková odpověď</span><span class="sxs-lookup"><span data-stu-id="88ae5-159">Sample response</span></span>

[!code-JSON [tools-json.json](./_data/tools-json.json)]
