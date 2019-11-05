---
title: Tools. JSON pro zjišťování verzí NuGet. exe
description: Koncový bod pro
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: a186db9727bdfd1b55bf73a1f29283352555dede
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/05/2019
ms.locfileid: "73611020"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a><span data-ttu-id="05b6d-103">Tools. JSON pro zjišťování verzí NuGet. exe</span><span class="sxs-lookup"><span data-stu-id="05b6d-103">tools.json for discovering nuget.exe versions</span></span>

<span data-ttu-id="05b6d-104">V současné době existuje několik způsobů, jak na svém počítači získat nejnovější verzi nástroje NuGet. exe, která umožňuje skriptovat.</span><span class="sxs-lookup"><span data-stu-id="05b6d-104">Today, there are a few ways to get the latest version of nuget.exe on your machine in a scriptable fashion.</span></span> <span data-ttu-id="05b6d-105">Balíček [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) můžete například stáhnout a extrahovat z NuGet.org. To má složitost, protože buď vyžaduje, abyste už měli nástroj NuGet. exe (pro `nuget.exe install`), nebo musíte rozbalit soubor. nupkg pomocí základního nástroje pro rozbalení a vyhledat binární soubor uvnitř.</span><span class="sxs-lookup"><span data-stu-id="05b6d-105">For example, you can download and extract the [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package from nuget.org. This has some complexity since it either requires that you already have nuget.exe (for `nuget.exe install`) or you have to unzip the .nupkg using a basic unzip tool and find the binary inside.</span></span>

<span data-ttu-id="05b6d-106">Pokud již máte NuGet. exe, můžete také použít `nuget.exe update -self`, ale to vyžaduje, abyste měli existující kopii NuGet. exe.</span><span class="sxs-lookup"><span data-stu-id="05b6d-106">If you already have nuget.exe, you can also use `nuget.exe update -self`, however this also requires having an existing copy of nuget.exe.</span></span> <span data-ttu-id="05b6d-107">Tento přístup také aktualizuje na nejnovější verzi.</span><span class="sxs-lookup"><span data-stu-id="05b6d-107">This approach also updates you to the latest version.</span></span> <span data-ttu-id="05b6d-108">Neumožňuje použití konkrétní verze.</span><span class="sxs-lookup"><span data-stu-id="05b6d-108">It does not allow the use of a specific version.</span></span>

<span data-ttu-id="05b6d-109">Koncový bod `tools.json` je k dispozici pro řešení potíží s zaváděním a pro řízení verze souboru NuGet. exe, který stáhnete.</span><span class="sxs-lookup"><span data-stu-id="05b6d-109">The `tools.json` endpoint is available to both solve the bootstrapping problem and to give control of the version of nuget.exe that you download.</span></span> <span data-ttu-id="05b6d-110">Tato možnost se dá použít v prostředích CI/CD nebo ve vlastních skriptech ke zjišťování a stažení všech vydaných verzí NuGet. exe.</span><span class="sxs-lookup"><span data-stu-id="05b6d-110">This can be used in CI/CD environments or in custom scripts to discover and download any released version of nuget.exe.</span></span>

<span data-ttu-id="05b6d-111">Koncový bod `tools.json` lze načíst pomocí neověřeného požadavku HTTP (např. `Invoke-WebRequest` v PowerShellu nebo `wget`).</span><span class="sxs-lookup"><span data-stu-id="05b6d-111">The `tools.json` endpoint can be fetched using an unauthenticated HTTP request (e.g. `Invoke-WebRequest` in PowerShell or `wget`).</span></span> <span data-ttu-id="05b6d-112">Dá se analyzovat pomocí deserializace JSON a následné adresy URL pro stahování NuGet. exe můžete také načíst pomocí neověřených požadavků HTTP.</span><span class="sxs-lookup"><span data-stu-id="05b6d-112">It can be parsed using a JSON deserializer and subsequent nuget.exe download URLs can also be fetched using unauthenticated HTTP requests.</span></span>

<span data-ttu-id="05b6d-113">Koncový bod se dá načíst pomocí metody `GET`:</span><span class="sxs-lookup"><span data-stu-id="05b6d-113">The endpoint can be fetched using the `GET` method:</span></span>

    GET https://dist.nuget.org/tools.json

<span data-ttu-id="05b6d-114">[Schéma JSON](https://json-schema.org/) pro koncový bod je k dispozici zde:</span><span class="sxs-lookup"><span data-stu-id="05b6d-114">The [JSON schema](https://json-schema.org/) for the endpoint is available here:</span></span>

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a><span data-ttu-id="05b6d-115">Základě</span><span class="sxs-lookup"><span data-stu-id="05b6d-115">Response</span></span>

<span data-ttu-id="05b6d-116">Odpověď je dokument JSON obsahující všechny dostupné verze nástroje NuGet. exe.</span><span class="sxs-lookup"><span data-stu-id="05b6d-116">The response is a JSON document containing all of the available versions of nuget.exe.</span></span>

<span data-ttu-id="05b6d-117">Kořenový objekt JSON má následující vlastnost:</span><span class="sxs-lookup"><span data-stu-id="05b6d-117">The root JSON object has the following property:</span></span>

<span data-ttu-id="05b6d-118">Name</span><span class="sxs-lookup"><span data-stu-id="05b6d-118">Name</span></span>      | <span data-ttu-id="05b6d-119">Typ</span><span class="sxs-lookup"><span data-stu-id="05b6d-119">Type</span></span>             | <span data-ttu-id="05b6d-120">Požadováno</span><span class="sxs-lookup"><span data-stu-id="05b6d-120">Required</span></span>
--------- | ---------------- | --------
<span data-ttu-id="05b6d-121">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="05b6d-121">nuget.exe</span></span> | <span data-ttu-id="05b6d-122">pole objektů</span><span class="sxs-lookup"><span data-stu-id="05b6d-122">array of objects</span></span> | <span data-ttu-id="05b6d-123">Ano</span><span class="sxs-lookup"><span data-stu-id="05b6d-123">yes</span></span>

<span data-ttu-id="05b6d-124">Každý objekt v poli `nuget.exe` má následující vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="05b6d-124">Each object in the `nuget.exe` array has the following properties:</span></span>

<span data-ttu-id="05b6d-125">Name</span><span class="sxs-lookup"><span data-stu-id="05b6d-125">Name</span></span>     | <span data-ttu-id="05b6d-126">Typ</span><span class="sxs-lookup"><span data-stu-id="05b6d-126">Type</span></span>   | <span data-ttu-id="05b6d-127">Požadováno</span><span class="sxs-lookup"><span data-stu-id="05b6d-127">Required</span></span> | <span data-ttu-id="05b6d-128">Poznámky</span><span class="sxs-lookup"><span data-stu-id="05b6d-128">Notes</span></span>
-------- | ------ | -------- | -----
<span data-ttu-id="05b6d-129">verze</span><span class="sxs-lookup"><span data-stu-id="05b6d-129">version</span></span>  | <span data-ttu-id="05b6d-130">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="05b6d-130">string</span></span> | <span data-ttu-id="05b6d-131">Ano</span><span class="sxs-lookup"><span data-stu-id="05b6d-131">yes</span></span>      | <span data-ttu-id="05b6d-132">Řetězec SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="05b6d-132">A SemVer 2.0.0 string</span></span>
<span data-ttu-id="05b6d-133">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="05b6d-133">url</span></span>      | <span data-ttu-id="05b6d-134">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="05b6d-134">string</span></span> | <span data-ttu-id="05b6d-135">Ano</span><span class="sxs-lookup"><span data-stu-id="05b6d-135">yes</span></span>      | <span data-ttu-id="05b6d-136">Absolutní adresa URL pro stažení této verze souboru NuGet. exe</span><span class="sxs-lookup"><span data-stu-id="05b6d-136">An absolute URL for downloading this version of nuget.exe</span></span>
<span data-ttu-id="05b6d-137">Skladiště</span><span class="sxs-lookup"><span data-stu-id="05b6d-137">stage</span></span>    | <span data-ttu-id="05b6d-138">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="05b6d-138">string</span></span> | <span data-ttu-id="05b6d-139">Ano</span><span class="sxs-lookup"><span data-stu-id="05b6d-139">yes</span></span>      | <span data-ttu-id="05b6d-140">Řetězec výčtu</span><span class="sxs-lookup"><span data-stu-id="05b6d-140">An enum string</span></span>
<span data-ttu-id="05b6d-141">nahrávaný</span><span class="sxs-lookup"><span data-stu-id="05b6d-141">uploaded</span></span> | <span data-ttu-id="05b6d-142">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="05b6d-142">string</span></span> | <span data-ttu-id="05b6d-143">Ano</span><span class="sxs-lookup"><span data-stu-id="05b6d-143">yes</span></span>      | <span data-ttu-id="05b6d-144">Přibližné časové razítko ISO 8601, kdy byla verze zpřístupněna</span><span class="sxs-lookup"><span data-stu-id="05b6d-144">An approximate ISO 8601 timestamp of when the version was made available</span></span>

<span data-ttu-id="05b6d-145">Položky v poli budou seřazeny sestupně, SemVer 2.0.0 objednávka.</span><span class="sxs-lookup"><span data-stu-id="05b6d-145">The items in the array will be sorted in descending, SemVer 2.0.0 order.</span></span> <span data-ttu-id="05b6d-146">Tato záruka má snížit zatížení klienta, který má zájem o nejvyšší číslo verze.</span><span class="sxs-lookup"><span data-stu-id="05b6d-146">This guarantee is meant to reduce the burden of a client that is interested in highest version number.</span></span> <span data-ttu-id="05b6d-147">To ale znamená, že seznam není seřazený v chronologickém pořadí.</span><span class="sxs-lookup"><span data-stu-id="05b6d-147">However this does mean that the list is not sorted in chronological order.</span></span> <span data-ttu-id="05b6d-148">Pokud je například nižší hlavní verze zavedená v pozdější době než vyšší hlavní verze, tato služba se v horní části seznamu nezobrazí.</span><span class="sxs-lookup"><span data-stu-id="05b6d-148">For example, if a lower major version is serviced at a date later than a higher major version, this serviced version will not appear at the top of the list.</span></span> <span data-ttu-id="05b6d-149">Pokud chcete nejnovější verzi vydanou *časovým razítkem*, jednoduše seřaďte pole pomocí `uploaded`ho řetězce.</span><span class="sxs-lookup"><span data-stu-id="05b6d-149">If you want the latest version released by *timestamp*, simply sort the array by the `uploaded` string.</span></span> <span data-ttu-id="05b6d-150">To funguje, protože časové razítko `uploaded` je ve formátu [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) , který lze seřadit chronologicky pomocí lexicographical řazení (tj. jednoduché řazení řetězců).</span><span class="sxs-lookup"><span data-stu-id="05b6d-150">This works because the `uploaded` timestamp is in the [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format which can be sorted chronologically by using a lexicographical sort (i.e. a simple string sort).</span></span>

<span data-ttu-id="05b6d-151">Vlastnost `stage` určuje, jak prověřené Tato verze nástroje.</span><span class="sxs-lookup"><span data-stu-id="05b6d-151">The `stage` property indicates how vetted this version of the tool is.</span></span> 

<span data-ttu-id="05b6d-152">Skladiště</span><span class="sxs-lookup"><span data-stu-id="05b6d-152">Stage</span></span>              | <span data-ttu-id="05b6d-153">Význam</span><span class="sxs-lookup"><span data-stu-id="05b6d-153">Meaning</span></span>
------------------ | ------
<span data-ttu-id="05b6d-154">EarlyAccessPreview</span><span class="sxs-lookup"><span data-stu-id="05b6d-154">EarlyAccessPreview</span></span> | <span data-ttu-id="05b6d-155">Ještě není vidět na [webové stránce Stáhnout](https://www.nuget.org/downloads) a měly by je ověřit partneři.</span><span class="sxs-lookup"><span data-stu-id="05b6d-155">Not yet visible on the [download web page](https://www.nuget.org/downloads) and should be validated by partners</span></span>
<span data-ttu-id="05b6d-156">Vydáno</span><span class="sxs-lookup"><span data-stu-id="05b6d-156">Released</span></span>           | <span data-ttu-id="05b6d-157">K dispozici na webu pro stahování, ale ještě není doporučováno pro rozsáhlou spotřebu</span><span class="sxs-lookup"><span data-stu-id="05b6d-157">Available on the download site but is not yet recommended for wide-spread consumption</span></span>
<span data-ttu-id="05b6d-158">ReleasedAndBlessed</span><span class="sxs-lookup"><span data-stu-id="05b6d-158">ReleasedAndBlessed</span></span> | <span data-ttu-id="05b6d-159">K dispozici na webu pro stahování a doporučuje se pro spotřebu</span><span class="sxs-lookup"><span data-stu-id="05b6d-159">Available on the download site and is recommended for consumption</span></span>

<span data-ttu-id="05b6d-160">Jedním jednoduchým přístupem k nejnovějším a doporučeným verzím je první verze v seznamu, která má `stage` hodnotu `ReleasedAndBlessed`.</span><span class="sxs-lookup"><span data-stu-id="05b6d-160">One simple approach for having the latest, recommended version is to take the first version in the list that has the `stage` value of `ReleasedAndBlessed`.</span></span> <span data-ttu-id="05b6d-161">To funguje, protože verze jsou seřazené v SemVer 2.0.0 pořadí.</span><span class="sxs-lookup"><span data-stu-id="05b6d-161">This works because the versions are sorted in SemVer 2.0.0 order.</span></span>

<span data-ttu-id="05b6d-162">Balíček `NuGet.CommandLine` v nuget.org se obvykle aktualizuje jenom pomocí `ReleasedAndBlessed` verzí.</span><span class="sxs-lookup"><span data-stu-id="05b6d-162">The `NuGet.CommandLine` package on nuget.org is typically only updated with `ReleasedAndBlessed` versions.</span></span>

### <a name="sample-request"></a><span data-ttu-id="05b6d-163">Ukázková žádost</span><span class="sxs-lookup"><span data-stu-id="05b6d-163">Sample request</span></span>

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a><span data-ttu-id="05b6d-164">Ukázková odpověď</span><span class="sxs-lookup"><span data-stu-id="05b6d-164">Sample response</span></span>

[!code-JSON [tools-json.json](./_data/tools-json.json)]
