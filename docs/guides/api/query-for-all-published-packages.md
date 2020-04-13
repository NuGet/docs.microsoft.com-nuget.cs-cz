---
title: Dotaz na všechny balíčky publikované do nuget.org
description: Pomocí nugetového rozhraní API můžete dotazovat na všechny balíčky publikované do nuget.org a zůstat aktuální v průběhu času.
author: joelverhagen
ms.author: jver
ms.date: 11/02/2017
ms.topic: tutorial
ms.reviewer: kraigb
ms.openlocfilehash: 0bd21c427b5b89ae9e5f1500d75e1bf63a96e828
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "64498224"
---
# <a name="query-for-all-packages-published-to-nugetorg"></a><span data-ttu-id="b761c-103">Dotaz na všechny balíčky publikované do nuget.org</span><span class="sxs-lookup"><span data-stu-id="b761c-103">Query for all packages published to nuget.org</span></span>

<span data-ttu-id="b761c-104">Jeden společný vzor dotazu na starší rozhraní API OData V2 byl výčet všech balíčků publikovaných do nuget.org, seřazené při publikování balíčku.</span><span class="sxs-lookup"><span data-stu-id="b761c-104">One common query pattern on the legacy OData V2 API was enumerating all packages published to nuget.org, ordered by when the package was published.</span></span> <span data-ttu-id="b761c-105">Scénáře, které vyžadují tento druh dotazu proti nuget.org se značně liší:</span><span class="sxs-lookup"><span data-stu-id="b761c-105">Scenarios requiring this kind of query against nuget.org vary widely:</span></span>

- <span data-ttu-id="b761c-106">Replikace nuget.org úplně</span><span class="sxs-lookup"><span data-stu-id="b761c-106">Replicating nuget.org entirely</span></span>
- <span data-ttu-id="b761c-107">Zjišťování, kdy jsou vydány nové verze</span><span class="sxs-lookup"><span data-stu-id="b761c-107">Detecting when packages have new versions released</span></span>
- <span data-ttu-id="b761c-108">Hledání balíčků, které závisí na vašem balíčku</span><span class="sxs-lookup"><span data-stu-id="b761c-108">Finding packages that depend on your package</span></span>

<span data-ttu-id="b761c-109">Starší způsob, jak to udělat, obvykle závisí na řazení entity balíčku OData podle časového `skip` razítka a stránkování přes masivní sadu výsledků pomocí a `top` (velikost stránky) parametry.</span><span class="sxs-lookup"><span data-stu-id="b761c-109">The legacy way of doing this typically depended on sorting the OData package entity by a timestamp and paging across the massive result set using `skip` and `top` (page size) parameters.</span></span> <span data-ttu-id="b761c-110">Bohužel, tento přístup má některé nevýhody:</span><span class="sxs-lookup"><span data-stu-id="b761c-110">Unfortunately, this approach has some drawbacks:</span></span>

- <span data-ttu-id="b761c-111">Možnost chybějících balíčků, protože dotazy jsou prováděny na data, která se často mění pořadí</span><span class="sxs-lookup"><span data-stu-id="b761c-111">Possibility of missing packages, because the queries are being made on data that is often changing order</span></span>
- <span data-ttu-id="b761c-112">Pomalá doba odezvy dotazu, protože dotazy nejsou optimalizovány (nejvíce optimalizované dotazy jsou ty, které podporují hlavní scénář pro oficiální klientnu NuGet)</span><span class="sxs-lookup"><span data-stu-id="b761c-112">Slow query response time, because the queries are not optimized (the most optimized queries are ones that support a mainline scenario for the official NuGet client)</span></span>
- <span data-ttu-id="b761c-113">Použití zastaralého a nedokumentovaného ROZHRANÍ API, což znamená, že podpora takových dotazů v budoucnu není zaručena</span><span class="sxs-lookup"><span data-stu-id="b761c-113">Use of deprecated and undocumented API, meaning the support of such queries in the future is not guaranteed</span></span>
- <span data-ttu-id="b761c-114">Neschopnost přehrát historii v přesném pořadí, v jakém se objevila</span><span class="sxs-lookup"><span data-stu-id="b761c-114">Inability to replay history in the exact order that it transpired</span></span>

<span data-ttu-id="b761c-115">Z tohoto důvodu lze sledovat následující příručku k řešení výše uvedených scénářů spolehlivějším způsobem, který obnaží budoucnost.</span><span class="sxs-lookup"><span data-stu-id="b761c-115">For this reason, the following guide can be followed to address the aforementioned scenarios in a more reliable and future-proof way.</span></span>

## <a name="overview"></a><span data-ttu-id="b761c-116">Přehled</span><span class="sxs-lookup"><span data-stu-id="b761c-116">Overview</span></span>

<span data-ttu-id="b761c-117">V centru této příručky je prostředek v [nuget api](../../api/overview.md) s názvem **katalogu**.</span><span class="sxs-lookup"><span data-stu-id="b761c-117">At the center of this guide is resource in the [NuGet API](../../api/overview.md) called the **catalog**.</span></span> <span data-ttu-id="b761c-118">Katalog je pouze připojit rozhraní API, které umožňuje volajícímu zobrazit úplnou historii balíčků přidaných, upravených a odstraněných z nuget.org. Máte-li zájem o všechny nebo dokonce podmnožinu balíčků publikovaných do nuget.org, katalog je skvělý způsob, jak zůstat up-to-date se sadou aktuálně dostupných balíčků, jak čas pokračuje.</span><span class="sxs-lookup"><span data-stu-id="b761c-118">The catalog is an append-only API that allows the caller to see a full history of packages added to, modified, and deleted from nuget.org. If you are interested in all or even a subset of packages published to nuget.org, the catalog is a great way to stay up-to-date with the set of currently available packages as time goes on.</span></span>

<span data-ttu-id="b761c-119">Tato příručka má být na vysoké úrovni walk-through, ale pokud máte zájem o jemné zrnitosti podrobnosti katalogu, naleznete v jeho [referenčním dokumentu rozhraní API](../../api/catalog-resource.md).</span><span class="sxs-lookup"><span data-stu-id="b761c-119">This guide is intended to be a high-level walk-through but if you are interested in the fine-grain details of the catalog, see its [API reference document](../../api/catalog-resource.md).</span></span>

<span data-ttu-id="b761c-120">Následující kroky mohou být implementovány v libovolném programovacím jazyce podle vašeho výběru.</span><span class="sxs-lookup"><span data-stu-id="b761c-120">The following steps can be implemented in any programming language of your choice.</span></span> <span data-ttu-id="b761c-121">Pokud chcete úplné spuštění ukázky, podívejte se na [c# ukázku](#c-sample-code) uvedenou níže.</span><span class="sxs-lookup"><span data-stu-id="b761c-121">If you want a full running sample, take a look at the [C# sample](#c-sample-code) mentioned below.</span></span>

<span data-ttu-id="b761c-122">V opačném případě postupujte podle níže uvedeného průvodce a vytvořte spolehlivou čtečku katalogů.</span><span class="sxs-lookup"><span data-stu-id="b761c-122">Otherwise, follow the guide below to build a reliable catalog reader.</span></span>

## <a name="initialize-a-cursor"></a><span data-ttu-id="b761c-123">Inicializovat kurzor</span><span class="sxs-lookup"><span data-stu-id="b761c-123">Initialize a cursor</span></span>

<span data-ttu-id="b761c-124">Prvním krokem při vytváření spolehlivé čtečky katalogů je implementace kurzoru.</span><span class="sxs-lookup"><span data-stu-id="b761c-124">The first step in building a reliable catalog reader is implementing a cursor.</span></span> <span data-ttu-id="b761c-125">Podrobné informace o návrhu kurzoru katalogu naleznete v [referenčním dokumentu katalogu](../../api/catalog-resource.md#cursor).</span><span class="sxs-lookup"><span data-stu-id="b761c-125">For full details about the design of a catalog cursor, see the [catalog reference document](../../api/catalog-resource.md#cursor).</span></span> <span data-ttu-id="b761c-126">Stručně řečeno, kurzor je bod v čase, do kterého jste zpracovali události v katalogu.</span><span class="sxs-lookup"><span data-stu-id="b761c-126">In short, cursor is a point in time up to which you have processed events in the catalog.</span></span> <span data-ttu-id="b761c-127">Události v katalogu představují publikování balíčků a další změny balíčků.</span><span class="sxs-lookup"><span data-stu-id="b761c-127">Events in the catalog represent package publishes and other package changes.</span></span> <span data-ttu-id="b761c-128">Pokud vám záleží na všech balíčcích, které byly někdy publikovány na NuGet (od počátku času), inicializovali byste kurzor na časové razítko "minimální hodnoty" (např. `DateTime.MinValue` v .NET).</span><span class="sxs-lookup"><span data-stu-id="b761c-128">If you care about all packages ever published to NuGet (since the beginning of time), you would initialize your cursor to a "minimum value" timestamp (e.g. `DateTime.MinValue` in .NET).</span></span> <span data-ttu-id="b761c-129">Pokud vám záleží pouze na balíčcích publikovaných od nynějška, použijete aktuální časové razítko jako počáteční hodnotu kurzoru.</span><span class="sxs-lookup"><span data-stu-id="b761c-129">If you care only about packages published starting now, you would use the current timestamp as your initial cursor value.</span></span>

<span data-ttu-id="b761c-130">Pro tuto příručku budeme inicializovat náš kurzor na časové razítko před hodinou.</span><span class="sxs-lookup"><span data-stu-id="b761c-130">For this guide, we'll initialize our cursor to a timestamp one hour ago.</span></span> <span data-ttu-id="b761c-131">Prozatím uložte to časové razítko do paměti.</span><span class="sxs-lookup"><span data-stu-id="b761c-131">For now, just save that timestamp in memory.</span></span>

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a><span data-ttu-id="b761c-132">Určení adresy URL indexu katalogu</span><span class="sxs-lookup"><span data-stu-id="b761c-132">Determine catalog index URL</span></span>

<span data-ttu-id="b761c-133">Umístění každého prostředku (koncového bodu) v rozhraní API NuGet by měla být zjištěna pomocí [indexu služby](../../api/service-index.md).</span><span class="sxs-lookup"><span data-stu-id="b761c-133">The location of every resource (endpoint) in the NuGet API should be discovered using the [service index](../../api/service-index.md).</span></span> <span data-ttu-id="b761c-134">Vzhledem k tomu, že tato příručka se zaměřuje na nuget.org, budeme používat nuget.org index služeb.</span><span class="sxs-lookup"><span data-stu-id="b761c-134">Because this guide focuses on nuget.org, we'll be using nuget.org's service index.</span></span>

    GET https://api.nuget.org/v3/index.json

<span data-ttu-id="b761c-135">Servisní doklad je dokument JSON obsahující všechny prostředky na nuget.org. Vyhledejte prostředek s `@type` hodnotou `Catalog/3.0.0`vlastnosti .</span><span class="sxs-lookup"><span data-stu-id="b761c-135">The service document is JSON document containing all of the resources on nuget.org. Look for the resource having the `@type` property value of `Catalog/3.0.0`.</span></span> <span data-ttu-id="b761c-136">Přidružená `@id` hodnota vlastnosti je adresa URL samotného indexu katalogu.</span><span class="sxs-lookup"><span data-stu-id="b761c-136">The associated `@id` property value is the URL to the catalog index itself.</span></span> 

## <a name="find-new-catalog-leaves"></a><span data-ttu-id="b761c-137">Najít nové katalogové listy</span><span class="sxs-lookup"><span data-stu-id="b761c-137">Find new catalog leaves</span></span>

<span data-ttu-id="b761c-138">Pomocí `@id` hodnoty vlastnosti nalezené v předchozím kroku stáhněte index katalogu:</span><span class="sxs-lookup"><span data-stu-id="b761c-138">Using the `@id` property value found in the previous step, download the catalog index:</span></span>

    GET https://api.nuget.org/v3/catalog0/index.json

<span data-ttu-id="b761c-139">Dekontujte [index katalogu](../../api/catalog-resource.md#catalog-index).</span><span class="sxs-lookup"><span data-stu-id="b761c-139">Deserialize the [catalog index](../../api/catalog-resource.md#catalog-index).</span></span> <span data-ttu-id="b761c-140">Odfiltrujte všechny [objekty stránky katalogu](../../api/catalog-resource.md#catalog-page-object-in-the-index) s `commitTimeStamp` hodnotou aktuální kurzoru menší nebo rovnou.</span><span class="sxs-lookup"><span data-stu-id="b761c-140">Filter out all [catalog page objects](../../api/catalog-resource.md#catalog-page-object-in-the-index) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="b761c-141">Pro každou zbývající stránku katalogu stáhněte celý dokument pomocí vlastnosti. `@id`</span><span class="sxs-lookup"><span data-stu-id="b761c-141">For each remaining catalog page, download the full document using the `@id` property.</span></span>

    GET https://api.nuget.org/v3/catalog0/page2926.json

<span data-ttu-id="b761c-142">Dekontujte [stránku katalogu](../../api/catalog-resource.md#catalog-page).</span><span class="sxs-lookup"><span data-stu-id="b761c-142">Deserialize the [catalog page](../../api/catalog-resource.md#catalog-page).</span></span> <span data-ttu-id="b761c-143">Odfiltrovat všechny [objekty listu katalogu](../../api/catalog-resource.md#catalog-item-object-in-a-page) s `commitTimeStamp` menší nebo rovna aktuální hodnotu kurzoru.</span><span class="sxs-lookup"><span data-stu-id="b761c-143">Filter out all [catalog leaf objects](../../api/catalog-resource.md#catalog-item-object-in-a-page) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="b761c-144">Po stažení všech stránek katalogu, které nejsou odfiltrovány, máte sadu objektů listu katalogu představující balíčky, které byly publikovány, neuvedeny, uvedeny nebo odstraněny v čase mezi časovým razítkem kurzoru a nyní.</span><span class="sxs-lookup"><span data-stu-id="b761c-144">After you have downloaded all of the catalog pages not filtered out, you have a set of catalog leaf objects representing packages that have been published, unlisted, listed, or deleted in the time between your cursor timestamp and now.</span></span>

## <a name="process-catalog-leaves"></a><span data-ttu-id="b761c-145">Listy katalogu procesů</span><span class="sxs-lookup"><span data-stu-id="b761c-145">Process catalog leaves</span></span>

<span data-ttu-id="b761c-146">V tomto okamžiku můžete provádět jakékoli vlastní zpracování, které chcete na položky katalogu.</span><span class="sxs-lookup"><span data-stu-id="b761c-146">At this point, you can perform any custom processing you'd like on the catalog items.</span></span> <span data-ttu-id="b761c-147">Pokud vše, co potřebujete, je ID a verze `nuget:id` `nuget:version` balíčku, můžete zkontrolovat vlastnosti a na objekty položky katalogu nalezené na stránkách.</span><span class="sxs-lookup"><span data-stu-id="b761c-147">If all you need is the ID and version of the package, you can inspect the `nuget:id` and `nuget:version` properties on the catalog item objects found in the pages.</span></span> <span data-ttu-id="b761c-148">Nezapomeňte se podívat `@type` na vlastnost, abyste zjistili, zda se položka katalogu týká existujícího balíčku nebo odstraněného balíčku.</span><span class="sxs-lookup"><span data-stu-id="b761c-148">Make sure to look at the `@type` property to know if the catalog item concerns an existing package or a deleted package.</span></span>

<span data-ttu-id="b761c-149">Pokud vás zajímají metadata o balíčku (například v popisu, závislosti, .nupkg velikost, atd),můžete `@id` načíst katalog list [dokumentu](../../api/catalog-resource.md#catalog-leaf) pomocí vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="b761c-149">If you are interested in the metadata about the package (such at the description, dependencies, .nupkg size, etc), you can fetch the [catalog leaf document](../../api/catalog-resource.md#catalog-leaf) using the `@id` property.</span></span>

    GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

<span data-ttu-id="b761c-150">Tento dokument obsahuje všechna metadata obsažená v [prostředku metadat balíčku](../../api/registration-base-url-resource.md)a další!</span><span class="sxs-lookup"><span data-stu-id="b761c-150">This document has all of the metadata included in the [package metadata resource](../../api/registration-base-url-resource.md), and more!</span></span>

<span data-ttu-id="b761c-151">Tento krok je, kde implementovat vlastní logiku.</span><span class="sxs-lookup"><span data-stu-id="b761c-151">This step is where you implement your custom logic.</span></span> <span data-ttu-id="b761c-152">Další kroky v této příručce jsou implementovány v podstatě stejným způsobem bez ohledu na to, co děláte s katalogu listy.</span><span class="sxs-lookup"><span data-stu-id="b761c-152">The other steps in this guide are implemented in pretty much the same way not matter what you are doing with the catalog leaves.</span></span>

### <a name="downloading-the-nupkg"></a><span data-ttu-id="b761c-153">Stahování .nupkg</span><span class="sxs-lookup"><span data-stu-id="b761c-153">Downloading the .nupkg</span></span>

<span data-ttu-id="b761c-154">Máte-li zájem o stažení .nupkg pro balíčky nalezené v katalogu, můžete použít [zdroj obsahu balíčku](../../api/package-base-address-resource.md).</span><span class="sxs-lookup"><span data-stu-id="b761c-154">If you are interested in downloading the .nupkg's for packages found in the catalog, you can use the [package content resource](../../api/package-base-address-resource.md).</span></span> <span data-ttu-id="b761c-155">Všimněte si však, že je krátká prodleva mezi při nalezení balíčku v katalogu a kdy je k dispozici v prostředku obsahu balíčku.</span><span class="sxs-lookup"><span data-stu-id="b761c-155">However, note that there is a short delay between when a package is found in catalog and when it's available in the package content resource.</span></span> <span data-ttu-id="b761c-156">Proto pokud narazíte `404 Not Found` při pokusu o stažení .nupkg pro balíček, který jste našli v katalogu, jednoduše opakujte krátce později.</span><span class="sxs-lookup"><span data-stu-id="b761c-156">Therefore, if you encounter `404 Not Found` when attempting to download a .nupkg for a package that you found in the catalog, simply retry a short time later.</span></span> <span data-ttu-id="b761c-157">Oprava tohoto zpoždění je sledována problémgithub [nuget/nugetgallery #3455](https://github.com/NuGet/NuGetGallery/issues/3455).</span><span class="sxs-lookup"><span data-stu-id="b761c-157">Fixing this delay is tracked by GitHub issue [NuGet/NuGetGallery#3455](https://github.com/NuGet/NuGetGallery/issues/3455).</span></span>

## <a name="move-the-cursor-forward"></a><span data-ttu-id="b761c-158">Přesunutí kurzoru dopředu</span><span class="sxs-lookup"><span data-stu-id="b761c-158">Move the cursor forward</span></span>

<span data-ttu-id="b761c-159">Po úspěšném zpracování položek katalogu je třeba určit novou hodnotu kurzoru, kterou chcete uložit.</span><span class="sxs-lookup"><span data-stu-id="b761c-159">Once you have successfully processed the catalog items, you need to determine the new cursor value to save.</span></span> <span data-ttu-id="b761c-160">Chcete-li to provést, najděte maximum `commitTimeStamp` (nejnovější chronologicky) všech položek katalogu, které jste zpracovali.</span><span class="sxs-lookup"><span data-stu-id="b761c-160">To do this, find the maximum (latest chronologically) `commitTimeStamp` of all catalog items that you processed.</span></span> <span data-ttu-id="b761c-161">Toto je vaše nová hodnota kurzoru.</span><span class="sxs-lookup"><span data-stu-id="b761c-161">This is your new cursor value.</span></span> <span data-ttu-id="b761c-162">Uložte ji do některé ho trvaléúložiště, jako je databáze, systém souborů nebo úložiště objektů blob.</span><span class="sxs-lookup"><span data-stu-id="b761c-162">Save it to some persistent store, like a database, file system, or blob storage.</span></span> <span data-ttu-id="b761c-163">Pokud chcete získat více položek katalogu, jednoduše začněte od [prvního kroku](#initialize-a-cursor) inicializací hodnoty kurzoru z tohoto trvalého úložiště.</span><span class="sxs-lookup"><span data-stu-id="b761c-163">When you want to get more catalog items, simply start from the [first step](#initialize-a-cursor) by initializing your cursor value from this persistent store.</span></span>

<span data-ttu-id="b761c-164">Pokud vaše aplikace vyvolá výjimku nebo chyby, nepohybujte kurzorem dopředu.</span><span class="sxs-lookup"><span data-stu-id="b761c-164">If your application throws an exception or faults, don't move the cursor forward.</span></span> <span data-ttu-id="b761c-165">Přesunutí kurzoru dopředu má význam, že už nikdy nebudete muset zpracovávat položky katalogu před kurzorem.</span><span class="sxs-lookup"><span data-stu-id="b761c-165">Moving the cursor forward has the meaning that you never again need to process catalog items before your cursor.</span></span>

<span data-ttu-id="b761c-166">Pokud z nějakého důvodu máte chybu v tom, jak zpracováváte listy katalogu, můžete jednoduše přesunout kurzor zpět v čase a povolit kódu znovu zpracovat staré položky katalogu.</span><span class="sxs-lookup"><span data-stu-id="b761c-166">If, for some reason, you have a bug in how you process catalog leaves, you can simply move your cursor backward in time and allow your code to reprocess the old catalog items.</span></span>

## <a name="c-sample-code"></a><span data-ttu-id="b761c-167">Ukázkový kód jazyka C#</span><span class="sxs-lookup"><span data-stu-id="b761c-167">C# sample code</span></span>

<span data-ttu-id="b761c-168">Vzhledem k tomu, že katalog je sada dokumentů JSON k dispozici přes HTTP, může být v interakci s pomocí libovolného programovacího jazyka, který má klienta HTTP a JSON deserializer.</span><span class="sxs-lookup"><span data-stu-id="b761c-168">Because the catalog is a set of JSON documents available over HTTP, it can be interacted with using any programming language that has an HTTP client and JSON deserializer.</span></span>

<span data-ttu-id="b761c-169">Ukázky jazyka C# jsou k dispozici v [úložišti NuGet/Samples](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).</span><span class="sxs-lookup"><span data-stu-id="b761c-169">C# samples are available in the [NuGet/Samples repository](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).</span></span>

```cli
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a><span data-ttu-id="b761c-170">Sada SDK katalogu</span><span class="sxs-lookup"><span data-stu-id="b761c-170">Catalog SDK</span></span>

<span data-ttu-id="b761c-171">Nejjednodušší způsob, jak využít katalog, je použít balíček sady SDK katalogu [.NET.](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog)</span><span class="sxs-lookup"><span data-stu-id="b761c-171">The easiest way to consume the catalog is to use the pre-release .NET catalog SDK package: [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog).</span></span> <span data-ttu-id="b761c-172">Tento balíček je `nuget-build` k dispozici na myget kanálu, pro `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`které používáte nuget balíček zdroj URL .</span><span class="sxs-lookup"><span data-stu-id="b761c-172">This package is available on the `nuget-build` MyGet feed, for which you use the NuGet package source URL `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`.</span></span>

<span data-ttu-id="b761c-173">Tento balíček můžete nainstalovat do `netstandard1.3` projektu kompatibilního s nebo vyšší (například rozhraní .NET Framework 4.6).</span><span class="sxs-lookup"><span data-stu-id="b761c-173">You can install this package to a project compatible with `netstandard1.3` or greater (such as .NET Framework 4.6).</span></span>

<span data-ttu-id="b761c-174">Ukázka pomocí tohoto balíčku je k dispozici na GitHubu v [projektu NuGet.Protocol.Catalog.Sample](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).</span><span class="sxs-lookup"><span data-stu-id="b761c-174">A sample using this package is available on GitHub in the [NuGet.Protocol.Catalog.Sample project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="b761c-175">Ukázkový výstup</span><span class="sxs-lookup"><span data-stu-id="b761c-175">Sample output</span></span>

```output
2017-11-10T22:16:44.8689025+00:00: Found package details leaf for xSkrape.APIWrapper.REST 1.0.2.
2017-11-10T22:16:54.6972769+00:00: Found package details leaf for xSkrape.APIWrapper.REST 1.0.1.
2017-11-10T22:19:20.6385542+00:00: Found package details leaf for Platform.EnUnity 1.0.8.
...
2017-11-10T23:05:04.9695890+00:00: Found package details leaf for xSkrape.APIWrapper.Base 1.0.1.
2017-11-10T23:05:04.9695890+00:00: Found package details leaf for xSkrape.APIWrapper.Base 1.0.2.
2017-11-10T23:07:23.1303569+00:00: Found package details leaf for VeiculoX.Model 0.0.15.
Processing the catalog leafs failed. Retrying.
fail: NuGet.Protocol.Catalog.LoggerCatalogLeafProcessor[0]
      10 catalog commits have been processed. We will now simulate a failure.
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      Failed to process leaf https://api.nuget.org/v3/catalog0/data/2017.11.10.23.07.23/veiculox.model.0.0.15.json (VeiculoX.Model 0.0.15, PackageDetails).
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      13 out of 59 leaves were left incomplete due to a processing failure.
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      1 out of 1 pages were left incomplete due to a processing failure.
2017-11-10T23:07:23.1303569+00:00: Found package details leaf for VeiculoX.Model 0.0.15.
2017-11-10T23:07:33.0212446+00:00: Found package details leaf for VeiculoX.Model 0.0.14.
2017-11-10T23:07:41.6621837+00:00: Found package details leaf for VeiculoX.Model 0.0.13.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for CreaSoft.Composition.Web.Extensions 1.1.0.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for DarkXaHTeP.Extensions.Configuration.Consul 0.0.4.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.3.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Imaging 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Imaging.Interop.14.0.DesignTime 14.3.25407.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Language.Intellisense 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Language.StandardClassification 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.ManagedInterfaces 8.0.50727.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.2.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.3.
```

### <a name="minimal-sample"></a><span data-ttu-id="b761c-176">Minimální vzorek</span><span class="sxs-lookup"><span data-stu-id="b761c-176">Minimal sample</span></span>

<span data-ttu-id="b761c-177">Příklad s menším počtem závislostí, který podrobněji ilustruje interakci s katalogem, naleznete v [ukázkovém projektu CatalogReaderExample](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample).</span><span class="sxs-lookup"><span data-stu-id="b761c-177">For an example with fewer dependencies that illustrates the interaction with the catalog in more detail, see the [CatalogReaderExample sample project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample).</span></span> <span data-ttu-id="b761c-178">Projekt se `netcoreapp2.0` zaměřuje a závisí na [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (pro řešení indexu služeb) a [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (pro deserializaci JSON).</span><span class="sxs-lookup"><span data-stu-id="b761c-178">The project targets `netcoreapp2.0` and depends on the [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (for resolving the service index) and [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (for JSON deserialization).</span></span>

<span data-ttu-id="b761c-179">Hlavní logika kódu je viditelná v [souboru Program.cs](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="b761c-179">The main logic of the code is visible in the [Program.cs file](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="b761c-180">Ukázkový výstup</span><span class="sxs-lookup"><span data-stu-id="b761c-180">Sample output</span></span>

```output
No cursor found. Defaulting to 11/2/2017 9:41:28 PM.
Fetched catalog index https://api.nuget.org/v3/catalog0/index.json.
Fetched catalog page https://api.nuget.org/v3/catalog0/page2935.json.
Processing 69 catalog leaves.
11/2/2017 9:32:35 PM: DotVVM.Compiler.Light 1.1.7 (type is nuget:PackageDetails)
11/2/2017 9:32:35 PM: Momentum.Pm.Api 5.12.181-beta (type is nuget:PackageDetails)
11/2/2017 9:32:44 PM: Momentum.Pm.PortalApi 5.12.181-beta (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Genesys.Extensions.Standard 3.17.11.40 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Genesys.Extensions.Core 3.17.11.40 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.Serialization.Bond 1.0.4 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.AmazonS3 1.0.4 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.DocumentStores.DocumentDb 1.0.6 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.BlobStorage 1.0.5 (type is nuget:PackageDetails)
...
11/2/2017 10:23:54 PM: Cake.GitPackager 0.1.2 (type is nuget:PackageDetails)
11/2/2017 10:23:54 PM: UtilPack.NuGet 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:23:54 PM: UtilPack.NuGet.AssemblyLoading 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:26 PM: UtilPack.NuGet.Deployment 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:26 PM: UtilPack.NuGet.Common.MSBuild 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:36 PM: InstaClient 1.0.2 (type is nuget:PackageDetails)
11/2/2017 10:26:36 PM: SecureStrConvertor.VARUN_RUSIYA 1.0.0.5 (type is nuget:PackageDetails)
Writing cursor value: 11/2/2017 10:26:36 PM.
```
