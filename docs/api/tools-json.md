---
title: Tools.JSON pro zjišťování nuget.exe verze
description: Koncový bod pro
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: 003139abac7808dbdaef4aa66119e09772db2b4f
ms.sourcegitcommit: b6efd4b210d92bf163c67e412ca9a5a018d117f0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/26/2019
ms.locfileid: "56852530"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a><span data-ttu-id="d8058-103">Tools.JSON pro zjišťování nuget.exe verze</span><span class="sxs-lookup"><span data-stu-id="d8058-103">tools.json for discovering nuget.exe versions</span></span>

<span data-ttu-id="d8058-104">V současné době existuje několik způsobů, jak získat nejnovější verzi programu nuget.exe na svém počítači skriptovatelný způsobem.</span><span class="sxs-lookup"><span data-stu-id="d8058-104">Today, there are a few ways to get the latest version of nuget.exe on your machine in a scriptable fashion.</span></span> <span data-ttu-id="d8058-105">Například můžete stáhnout a extrahovat [ `NuGet.CommandLine` ](https://www.nuget.org/packages/NuGet.CommandLine/) balíček z webu nuget.org. To má některé složitost, protože se buď vyžaduje, že už máte nuget.exe (pro `nuget.exe install`) nebo máte rozbalit .nupkg nástrojem základní unzip a vyhledejte binární vnitřní.</span><span class="sxs-lookup"><span data-stu-id="d8058-105">For example, you can download and extract the [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package from nuget.org. This has some complexity since it either requires that you already have nuget.exe (for `nuget.exe install`) or you have to unzip the .nupkg using a basic unzip tool and find the binary inside.</span></span>

<span data-ttu-id="d8058-106">Pokud už máte nuget.exe, můžete také použít `nuget.exe update -self`, ale tento proces také vyžaduje s existující kopie nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="d8058-106">If you already have nuget.exe, you can also use `nuget.exe update -self`, however this also requires having an existing copy of nuget.exe.</span></span> <span data-ttu-id="d8058-107">Tento přístup můžete rovněž aktualizuje na nejnovější verzi.</span><span class="sxs-lookup"><span data-stu-id="d8058-107">This approach also updates you to the latest version.</span></span> <span data-ttu-id="d8058-108">Neumožňuje použít konkrétní verzi.</span><span class="sxs-lookup"><span data-stu-id="d8058-108">It does not allow the use of a specific version.</span></span>

<span data-ttu-id="d8058-109">`tools.json` Koncový bod je k dispozici pro obě samozaváděcí problém vyřešit a poskytnout kontrolu verze programu nuget.exe, který můžete stáhnout.</span><span class="sxs-lookup"><span data-stu-id="d8058-109">The `tools.json` endpoint is available to both solve the bootstrapping problem and to give control of the version of nuget.exe that you download.</span></span> <span data-ttu-id="d8058-110">To lze vyhledat a stáhnout všechny vydané verze programu nuget.exe použít v prostředích CI/CD nebo vlastní skripty.</span><span class="sxs-lookup"><span data-stu-id="d8058-110">This can be used in CI/CD environments or in custom scripts to discover and download any released version of nuget.exe.</span></span>

<span data-ttu-id="d8058-111">`tools.json` Koncového bodu můžete načíst pomocí neověřené žádosti protokolu HTTP (například `Invoke-WebRequest` v prostředí PowerShell nebo `wget`).</span><span class="sxs-lookup"><span data-stu-id="d8058-111">The `tools.json` endpoint can be fetched using an unauthenticated HTTP request (e.g. `Invoke-WebRequest` in PowerShell or `wget`).</span></span> <span data-ttu-id="d8058-112">Může být analyzován pomocí deserializátor JSON a následné nuget.exe pro stažení adresy URL můžete načíst taky pomocí neověřené požadavky HTTP.</span><span class="sxs-lookup"><span data-stu-id="d8058-112">It can be parsed using a JSON deserializer and subsequent nuget.exe download URLs can also be fetched using unauthenticated HTTP requests.</span></span>

<span data-ttu-id="d8058-113">Koncový bod můžete načíst pomocí `GET` metody:</span><span class="sxs-lookup"><span data-stu-id="d8058-113">The endpoint can be fetched using the `GET` method:</span></span>

    GET https://dist.nuget.org/tools.json

<span data-ttu-id="d8058-114">[Schématu JSON](http://json-schema.org/) pro koncový bod je k dispozici zde:</span><span class="sxs-lookup"><span data-stu-id="d8058-114">The [JSON schema](http://json-schema.org/) for the endpoint is available here:</span></span>

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a><span data-ttu-id="d8058-115">Odpověď</span><span class="sxs-lookup"><span data-stu-id="d8058-115">Response</span></span>

<span data-ttu-id="d8058-116">Odpověď je dokument JSON obsahující všechny dostupné verze programu nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="d8058-116">The response is a JSON document containing all of the available versions of nuget.exe.</span></span>

<span data-ttu-id="d8058-117">Kořenový objekt JSON má následující vlastnost:</span><span class="sxs-lookup"><span data-stu-id="d8058-117">The root JSON object has the following property:</span></span>

<span data-ttu-id="d8058-118">Název</span><span class="sxs-lookup"><span data-stu-id="d8058-118">Name</span></span>      | <span data-ttu-id="d8058-119">Typ</span><span class="sxs-lookup"><span data-stu-id="d8058-119">Type</span></span>             | <span data-ttu-id="d8058-120">Požadováno</span><span class="sxs-lookup"><span data-stu-id="d8058-120">Required</span></span>
--------- | ---------------- | --------
<span data-ttu-id="d8058-121">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="d8058-121">nuget.exe</span></span> | <span data-ttu-id="d8058-122">Pole objektů</span><span class="sxs-lookup"><span data-stu-id="d8058-122">array of objects</span></span> | <span data-ttu-id="d8058-123">ano</span><span class="sxs-lookup"><span data-stu-id="d8058-123">yes</span></span>

<span data-ttu-id="d8058-124">Každý objekt v `nuget.exe` pole má následující vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="d8058-124">Each object in the `nuget.exe` array has the following properties:</span></span>

<span data-ttu-id="d8058-125">Název</span><span class="sxs-lookup"><span data-stu-id="d8058-125">Name</span></span>     | <span data-ttu-id="d8058-126">Typ</span><span class="sxs-lookup"><span data-stu-id="d8058-126">Type</span></span>   | <span data-ttu-id="d8058-127">Požadováno</span><span class="sxs-lookup"><span data-stu-id="d8058-127">Required</span></span> | <span data-ttu-id="d8058-128">Poznámky</span><span class="sxs-lookup"><span data-stu-id="d8058-128">Notes</span></span>
-------- | ------ | -------- | -----
<span data-ttu-id="d8058-129">verze</span><span class="sxs-lookup"><span data-stu-id="d8058-129">version</span></span>  | <span data-ttu-id="d8058-130">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="d8058-130">string</span></span> | <span data-ttu-id="d8058-131">ano</span><span class="sxs-lookup"><span data-stu-id="d8058-131">yes</span></span>      | <span data-ttu-id="d8058-132">Řetězec SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="d8058-132">A SemVer 2.0.0 string</span></span>
<span data-ttu-id="d8058-133">url</span><span class="sxs-lookup"><span data-stu-id="d8058-133">url</span></span>      | <span data-ttu-id="d8058-134">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="d8058-134">string</span></span> | <span data-ttu-id="d8058-135">ano</span><span class="sxs-lookup"><span data-stu-id="d8058-135">yes</span></span>      | <span data-ttu-id="d8058-136">Absolutní adresa URL pro stahování tato verze programu nuget.exe</span><span class="sxs-lookup"><span data-stu-id="d8058-136">An absolute URL for downloading this version of nuget.exe</span></span>
<span data-ttu-id="d8058-137">fáze</span><span class="sxs-lookup"><span data-stu-id="d8058-137">stage</span></span>    | <span data-ttu-id="d8058-138">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="d8058-138">string</span></span> | <span data-ttu-id="d8058-139">ano</span><span class="sxs-lookup"><span data-stu-id="d8058-139">yes</span></span>      | <span data-ttu-id="d8058-140">Řetězec výčtu</span><span class="sxs-lookup"><span data-stu-id="d8058-140">An enum string</span></span>
<span data-ttu-id="d8058-141">Nahrání</span><span class="sxs-lookup"><span data-stu-id="d8058-141">uploaded</span></span> | <span data-ttu-id="d8058-142">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="d8058-142">string</span></span> | <span data-ttu-id="d8058-143">ano</span><span class="sxs-lookup"><span data-stu-id="d8058-143">yes</span></span>      | <span data-ttu-id="d8058-144">Přibližné časové razítko ISO 8601 z verze kdy byl k dispozici</span><span class="sxs-lookup"><span data-stu-id="d8058-144">An approximate ISO 8601 timestamp of when the version was made available</span></span>

<span data-ttu-id="d8058-145">Položky v poli budou seřazeny v sestupném pořadí SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="d8058-145">The items in the array will be sorted in descending, SemVer 2.0.0 order.</span></span> <span data-ttu-id="d8058-146">Aby se snížila zátěž klienta, který je uvažujete o nejvyšší číslo verze je určená této záruky.</span><span class="sxs-lookup"><span data-stu-id="d8058-146">This guarantee is meant to reduce the burden of a client that is interested in highest version number.</span></span> <span data-ttu-id="d8058-147">Ale to znamená, že seznam není seřazen v chronologickém pořadí.</span><span class="sxs-lookup"><span data-stu-id="d8058-147">However this does mean that the list is not sorted in chronological order.</span></span> <span data-ttu-id="d8058-148">Například pokud nižší hlavní verze se obsluhují na datum pozdější než vyšší hlavní verze, tuto upravenou verzí se nezobrazí v horní části seznamu.</span><span class="sxs-lookup"><span data-stu-id="d8058-148">For example, if a lower major version is serviced at a date later than a higher major version, this serviced version will not appear at the top of the list.</span></span> <span data-ttu-id="d8058-149">Pokud chcete na nejnovější verzi vydal *časové razítko*, jednoduše seřadit pole pomocí `uploaded` řetězec.</span><span class="sxs-lookup"><span data-stu-id="d8058-149">If you want the latest version released by *timestamp*, simply sort the array by the `uploaded` string.</span></span> <span data-ttu-id="d8058-150">Tento postup funguje, protože `uploaded` časové razítko není v [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) formát, který lze seřadit chronologicky pomocí lexicographical řazení (to znamená jednoduchým řetězcem řazení).</span><span class="sxs-lookup"><span data-stu-id="d8058-150">This works because the `uploaded` timestamp is in the [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format which can be sorted chronologically by using a lexicographical sort (i.e. a simple string sort).</span></span>

<span data-ttu-id="d8058-151">`stage` Vlastnost určuje, jak prověřené je tato verze nástroje.</span><span class="sxs-lookup"><span data-stu-id="d8058-151">The `stage` property indicates how vetted this version of the tool is.</span></span> 

<span data-ttu-id="d8058-152">Fáze</span><span class="sxs-lookup"><span data-stu-id="d8058-152">Stage</span></span>              | <span data-ttu-id="d8058-153">Význam</span><span class="sxs-lookup"><span data-stu-id="d8058-153">Meaning</span></span>
------------------ | ------
<span data-ttu-id="d8058-154">EarlyAccessPreview</span><span class="sxs-lookup"><span data-stu-id="d8058-154">EarlyAccessPreview</span></span> | <span data-ttu-id="d8058-155">Nejsou ještě viditelné na [webové stránce pro stažení](https://www.nuget.org/downloads) a by měl být ověřen od partnerů</span><span class="sxs-lookup"><span data-stu-id="d8058-155">Not yet visible on the [download web page](https://www.nuget.org/downloads) and should be validated by partners</span></span>
<span data-ttu-id="d8058-156">Všeobecně dostupné</span><span class="sxs-lookup"><span data-stu-id="d8058-156">Released</span></span>           | <span data-ttu-id="d8058-157">K dispozici na webu Stažení ale ještě není doporučeno pro šíření celou spotřebu</span><span class="sxs-lookup"><span data-stu-id="d8058-157">Available on the download site but is not yet recommended for wide-spread consumption</span></span>
<span data-ttu-id="d8058-158">ReleasedAndBlessed</span><span class="sxs-lookup"><span data-stu-id="d8058-158">ReleasedAndBlessed</span></span> | <span data-ttu-id="d8058-159">K dispozici na serveru pro stahování a je doporučena pro využití</span><span class="sxs-lookup"><span data-stu-id="d8058-159">Available on the download site and is recommended for consumption</span></span>

<span data-ttu-id="d8058-160">Jeden jednoduchým přístupem k nutnosti na nejnovější verzi, doporučená verze je v seznamu, který se má provést první verze `stage` hodnotu `ReleasedAndBlessed`.</span><span class="sxs-lookup"><span data-stu-id="d8058-160">One simple approach for having the latest, recommended version is to take the first version in the list that has the `stage` value of `ReleasedAndBlessed`.</span></span> <span data-ttu-id="d8058-161">Tento postup funguje, protože verze jsou seřazeny podle SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="d8058-161">This works because the versions are sorted in SemVer 2.0.0 order.</span></span>

<span data-ttu-id="d8058-162">`NuGet.CommandLine` Balíčků na nuget.org je obvykle pouze aktualizován `ReleasedAndBlessed` verze.</span><span class="sxs-lookup"><span data-stu-id="d8058-162">The `NuGet.CommandLine` package on nuget.org is typically only updated with `ReleasedAndBlessed` versions.</span></span>

### <a name="sample-request"></a><span data-ttu-id="d8058-163">Ukázková žádost</span><span class="sxs-lookup"><span data-stu-id="d8058-163">Sample request</span></span>

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a><span data-ttu-id="d8058-164">Ukázková odpověď</span><span class="sxs-lookup"><span data-stu-id="d8058-164">Sample response</span></span>

[!code-JSON [tools-json.json](./_data/tools-json.json)]
