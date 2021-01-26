---
title: tools.jspro zjišťování verzí nuget.exe
description: Koncový bod pro
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: eb28ccbc4460663b0f149d2d08e9b47dd69847c7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773819"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a><span data-ttu-id="566c4-103">tools.jspro zjišťování verzí nuget.exe</span><span class="sxs-lookup"><span data-stu-id="566c4-103">tools.json for discovering nuget.exe versions</span></span>

<span data-ttu-id="566c4-104">V současné době existuje několik způsobů, jak na svém počítači získat nejnovější verzi nuget.exe pomocí skriptu.</span><span class="sxs-lookup"><span data-stu-id="566c4-104">Today, there are a few ways to get the latest version of nuget.exe on your machine in a scriptable fashion.</span></span> <span data-ttu-id="566c4-105">Balíček můžete například stáhnout a extrahovat [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) z NuGet.org. To má složitost, protože buď vyžaduje, abyste již měli nuget.exe (pro `nuget.exe install` ), nebo musíte rozbalit soubor. nupkg pomocí základního nástroje pro rozbalení a vyhledat binární soubor uvnitř.</span><span class="sxs-lookup"><span data-stu-id="566c4-105">For example, you can download and extract the [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package from nuget.org. This has some complexity since it either requires that you already have nuget.exe (for `nuget.exe install`) or you have to unzip the .nupkg using a basic unzip tool and find the binary inside.</span></span>

<span data-ttu-id="566c4-106">Pokud již máte nuget.exe, můžete také použít `nuget.exe update -self` existující kopii nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="566c4-106">If you already have nuget.exe, you can also use `nuget.exe update -self`, however this also requires having an existing copy of nuget.exe.</span></span> <span data-ttu-id="566c4-107">Tento přístup také aktualizuje na nejnovější verzi.</span><span class="sxs-lookup"><span data-stu-id="566c4-107">This approach also updates you to the latest version.</span></span> <span data-ttu-id="566c4-108">Neumožňuje použití konkrétní verze.</span><span class="sxs-lookup"><span data-stu-id="566c4-108">It does not allow the use of a specific version.</span></span>

<span data-ttu-id="566c4-109">`tools.json`Koncový bod je k dispozici pro řešení potíží s zaváděním a pro řízení verze nuget.exe, kterou stáhnete.</span><span class="sxs-lookup"><span data-stu-id="566c4-109">The `tools.json` endpoint is available to both solve the bootstrapping problem and to give control of the version of nuget.exe that you download.</span></span> <span data-ttu-id="566c4-110">Tato možnost se dá použít v prostředích CI/CD nebo ve vlastních skriptech ke zjišťování a stažení všech vydaných verzí nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="566c4-110">This can be used in CI/CD environments or in custom scripts to discover and download any released version of nuget.exe.</span></span>

<span data-ttu-id="566c4-111">`tools.json`Koncový bod se dá načíst pomocí neověřeného požadavku HTTP (třeba `Invoke-WebRequest` v PowerShellu nebo `wget` ).</span><span class="sxs-lookup"><span data-stu-id="566c4-111">The `tools.json` endpoint can be fetched using an unauthenticated HTTP request (e.g. `Invoke-WebRequest` in PowerShell or `wget`).</span></span> <span data-ttu-id="566c4-112">Dá se analyzovat pomocí deserializace JSON a následné nuget.exe adresy URL pro stahování je možné také načíst pomocí neověřených požadavků HTTP.</span><span class="sxs-lookup"><span data-stu-id="566c4-112">It can be parsed using a JSON deserializer and subsequent nuget.exe download URLs can also be fetched using unauthenticated HTTP requests.</span></span>

<span data-ttu-id="566c4-113">Koncový bod se dá načíst pomocí `GET` metody:</span><span class="sxs-lookup"><span data-stu-id="566c4-113">The endpoint can be fetched using the `GET` method:</span></span>

```
GET https://dist.nuget.org/tools.json
```

<span data-ttu-id="566c4-114">[Schéma JSON](https://json-schema.org/) pro koncový bod je k dispozici zde:</span><span class="sxs-lookup"><span data-stu-id="566c4-114">The [JSON schema](https://json-schema.org/) for the endpoint is available here:</span></span>

```
GET https://dist.nuget.org/tools.schema.json
```

## <a name="response"></a><span data-ttu-id="566c4-115">Odpověď</span><span class="sxs-lookup"><span data-stu-id="566c4-115">Response</span></span>

<span data-ttu-id="566c4-116">Odpověď je dokument JSON obsahující všechny dostupné verze nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="566c4-116">The response is a JSON document containing all of the available versions of nuget.exe.</span></span>

<span data-ttu-id="566c4-117">Kořenový objekt JSON má následující vlastnost:</span><span class="sxs-lookup"><span data-stu-id="566c4-117">The root JSON object has the following property:</span></span>

<span data-ttu-id="566c4-118">Název</span><span class="sxs-lookup"><span data-stu-id="566c4-118">Name</span></span>      | <span data-ttu-id="566c4-119">Typ</span><span class="sxs-lookup"><span data-stu-id="566c4-119">Type</span></span>             | <span data-ttu-id="566c4-120">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="566c4-120">Required</span></span>
--------- | ---------------- | --------
<span data-ttu-id="566c4-121">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="566c4-121">nuget.exe</span></span> | <span data-ttu-id="566c4-122">pole objektů</span><span class="sxs-lookup"><span data-stu-id="566c4-122">array of objects</span></span> | <span data-ttu-id="566c4-123">ano</span><span class="sxs-lookup"><span data-stu-id="566c4-123">yes</span></span>

<span data-ttu-id="566c4-124">Každý objekt v `nuget.exe` poli má následující vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="566c4-124">Each object in the `nuget.exe` array has the following properties:</span></span>

<span data-ttu-id="566c4-125">Název</span><span class="sxs-lookup"><span data-stu-id="566c4-125">Name</span></span>     | <span data-ttu-id="566c4-126">Typ</span><span class="sxs-lookup"><span data-stu-id="566c4-126">Type</span></span>   | <span data-ttu-id="566c4-127">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="566c4-127">Required</span></span> | <span data-ttu-id="566c4-128">Poznámky</span><span class="sxs-lookup"><span data-stu-id="566c4-128">Notes</span></span>
-------- | ------ | -------- | -----
<span data-ttu-id="566c4-129">verze</span><span class="sxs-lookup"><span data-stu-id="566c4-129">version</span></span>  | <span data-ttu-id="566c4-130">řetězec</span><span class="sxs-lookup"><span data-stu-id="566c4-130">string</span></span> | <span data-ttu-id="566c4-131">ano</span><span class="sxs-lookup"><span data-stu-id="566c4-131">yes</span></span>      | <span data-ttu-id="566c4-132">Řetězec SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="566c4-132">A SemVer 2.0.0 string</span></span>
<span data-ttu-id="566c4-133">url</span><span class="sxs-lookup"><span data-stu-id="566c4-133">url</span></span>      | <span data-ttu-id="566c4-134">řetězec</span><span class="sxs-lookup"><span data-stu-id="566c4-134">string</span></span> | <span data-ttu-id="566c4-135">ano</span><span class="sxs-lookup"><span data-stu-id="566c4-135">yes</span></span>      | <span data-ttu-id="566c4-136">Absolutní adresa URL pro stažení této verze nuget.exe</span><span class="sxs-lookup"><span data-stu-id="566c4-136">An absolute URL for downloading this version of nuget.exe</span></span>
<span data-ttu-id="566c4-137">skladiště</span><span class="sxs-lookup"><span data-stu-id="566c4-137">stage</span></span>    | <span data-ttu-id="566c4-138">řetězec</span><span class="sxs-lookup"><span data-stu-id="566c4-138">string</span></span> | <span data-ttu-id="566c4-139">ano</span><span class="sxs-lookup"><span data-stu-id="566c4-139">yes</span></span>      | <span data-ttu-id="566c4-140">Řetězec výčtu</span><span class="sxs-lookup"><span data-stu-id="566c4-140">An enum string</span></span>
<span data-ttu-id="566c4-141">nahrávaný</span><span class="sxs-lookup"><span data-stu-id="566c4-141">uploaded</span></span> | <span data-ttu-id="566c4-142">řetězec</span><span class="sxs-lookup"><span data-stu-id="566c4-142">string</span></span> | <span data-ttu-id="566c4-143">ano</span><span class="sxs-lookup"><span data-stu-id="566c4-143">yes</span></span>      | <span data-ttu-id="566c4-144">Přibližné časové razítko ISO 8601, kdy byla verze zpřístupněna</span><span class="sxs-lookup"><span data-stu-id="566c4-144">An approximate ISO 8601 timestamp of when the version was made available</span></span>

<span data-ttu-id="566c4-145">Položky v poli budou seřazeny sestupně, SemVer 2.0.0 objednávka.</span><span class="sxs-lookup"><span data-stu-id="566c4-145">The items in the array will be sorted in descending, SemVer 2.0.0 order.</span></span> <span data-ttu-id="566c4-146">Tato záruka má snížit zatížení klienta, který má zájem o nejvyšší číslo verze.</span><span class="sxs-lookup"><span data-stu-id="566c4-146">This guarantee is meant to reduce the burden of a client that is interested in highest version number.</span></span> <span data-ttu-id="566c4-147">To ale znamená, že seznam není seřazený v chronologickém pořadí.</span><span class="sxs-lookup"><span data-stu-id="566c4-147">However this does mean that the list is not sorted in chronological order.</span></span> <span data-ttu-id="566c4-148">Pokud je například nižší hlavní verze zavedená v pozdější době než vyšší hlavní verze, tato služba se v horní části seznamu nezobrazí.</span><span class="sxs-lookup"><span data-stu-id="566c4-148">For example, if a lower major version is serviced at a date later than a higher major version, this serviced version will not appear at the top of the list.</span></span> <span data-ttu-id="566c4-149">Pokud chcete nejnovější verzi vydanou pomocí *časového razítka*, jednoduše seřaďte pole podle `uploaded` řetězce.</span><span class="sxs-lookup"><span data-stu-id="566c4-149">If you want the latest version released by *timestamp*, simply sort the array by the `uploaded` string.</span></span> <span data-ttu-id="566c4-150">To funguje, protože `uploaded` časové razítko je ve formátu [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) , který lze seřadit chronologicky pomocí lexicographical řazení (tj. jednoduché řazení řetězců).</span><span class="sxs-lookup"><span data-stu-id="566c4-150">This works because the `uploaded` timestamp is in the [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format which can be sorted chronologically by using a lexicographical sort (i.e. a simple string sort).</span></span>

<span data-ttu-id="566c4-151">`stage`Vlastnost určuje, jak prověřené Tato verze nástroje.</span><span class="sxs-lookup"><span data-stu-id="566c4-151">The `stage` property indicates how vetted this version of the tool is.</span></span> 

<span data-ttu-id="566c4-152">Fáze</span><span class="sxs-lookup"><span data-stu-id="566c4-152">Stage</span></span>              | <span data-ttu-id="566c4-153">Význam</span><span class="sxs-lookup"><span data-stu-id="566c4-153">Meaning</span></span>
------------------ | ------
<span data-ttu-id="566c4-154">EarlyAccessPreview</span><span class="sxs-lookup"><span data-stu-id="566c4-154">EarlyAccessPreview</span></span> | <span data-ttu-id="566c4-155">Ještě není vidět na [webové stránce Stáhnout](https://www.nuget.org/downloads) a měly by je ověřit partneři.</span><span class="sxs-lookup"><span data-stu-id="566c4-155">Not yet visible on the [download web page](https://www.nuget.org/downloads) and should be validated by partners</span></span>
<span data-ttu-id="566c4-156">Vydáno</span><span class="sxs-lookup"><span data-stu-id="566c4-156">Released</span></span>           | <span data-ttu-id="566c4-157">K dispozici na webu pro stahování, ale ještě není doporučováno pro rozsáhlou spotřebu</span><span class="sxs-lookup"><span data-stu-id="566c4-157">Available on the download site but is not yet recommended for wide-spread consumption</span></span>
<span data-ttu-id="566c4-158">ReleasedAndBlessed</span><span class="sxs-lookup"><span data-stu-id="566c4-158">ReleasedAndBlessed</span></span> | <span data-ttu-id="566c4-159">K dispozici na webu pro stahování a doporučuje se pro spotřebu</span><span class="sxs-lookup"><span data-stu-id="566c4-159">Available on the download site and is recommended for consumption</span></span>

<span data-ttu-id="566c4-160">Jedním jednoduchým přístupem k nejnovějším a doporučeným verzím je první verze v seznamu, který má `stage` hodnotu `ReleasedAndBlessed` .</span><span class="sxs-lookup"><span data-stu-id="566c4-160">One simple approach for having the latest, recommended version is to take the first version in the list that has the `stage` value of `ReleasedAndBlessed`.</span></span> <span data-ttu-id="566c4-161">To funguje, protože verze jsou seřazené v SemVer 2.0.0 pořadí.</span><span class="sxs-lookup"><span data-stu-id="566c4-161">This works because the versions are sorted in SemVer 2.0.0 order.</span></span>

<span data-ttu-id="566c4-162">`NuGet.CommandLine`Balíček v NuGet.org je obvykle aktualizován pouze s `ReleasedAndBlessed` verzemi.</span><span class="sxs-lookup"><span data-stu-id="566c4-162">The `NuGet.CommandLine` package on nuget.org is typically only updated with `ReleasedAndBlessed` versions.</span></span>

### <a name="sample-request"></a><span data-ttu-id="566c4-163">Ukázková žádost</span><span class="sxs-lookup"><span data-stu-id="566c4-163">Sample request</span></span>

```
GET https://dist.nuget.org/tools.json
```

### <a name="sample-response"></a><span data-ttu-id="566c4-164">Ukázková odpověď</span><span class="sxs-lookup"><span data-stu-id="566c4-164">Sample response</span></span>

[!code-JSON [tools-json.json](./_data/tools-json.json)]
