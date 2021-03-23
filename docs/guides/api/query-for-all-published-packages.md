---
title: Dotaz na všechny balíčky publikované do nuget.org
description: Pomocí rozhraní API NuGet se můžete dotazovat na všechny balíčky publikované na nuget.org a v průběhu času zůstat v aktuálním stavu.
author: joelverhagen
ms.author: jver
ms.date: 11/02/2017
ms.topic: tutorial
ms.reviewer: kraigb
ms.openlocfilehash: 8f21aad93eb952035683314c10cd964f265ec4fd
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859340"
---
# <a name="query-for-all-packages-published-to-nugetorg"></a><span data-ttu-id="7a65c-103">Dotaz na všechny balíčky publikované do nuget.org</span><span class="sxs-lookup"><span data-stu-id="7a65c-103">Query for all packages published to nuget.org</span></span>

<span data-ttu-id="7a65c-104">Jeden společný vzor dotazu na starší verzi rozhraní OData v2 API vytvořil výčet všech balíčků publikovaných do nuget.org, seřazené podle toho, kdy byl balíček publikovaný.</span><span class="sxs-lookup"><span data-stu-id="7a65c-104">One common query pattern on the legacy OData V2 API was enumerating all packages published to nuget.org, ordered by when the package was published.</span></span> <span data-ttu-id="7a65c-105">Scénáře, které vyžadují tento druh dotazů na nuget.org, se výrazně liší:</span><span class="sxs-lookup"><span data-stu-id="7a65c-105">Scenarios requiring this kind of query against nuget.org vary widely:</span></span>

- <span data-ttu-id="7a65c-106">Úplné replikace nuget.org</span><span class="sxs-lookup"><span data-stu-id="7a65c-106">Replicating nuget.org entirely</span></span>
- <span data-ttu-id="7a65c-107">Zjišťování, kdy byly vydány nové verze balíčků</span><span class="sxs-lookup"><span data-stu-id="7a65c-107">Detecting when packages have new versions released</span></span>
- <span data-ttu-id="7a65c-108">Hledání balíčků, které jsou závislé na vašem balíčku</span><span class="sxs-lookup"><span data-stu-id="7a65c-108">Finding packages that depend on your package</span></span>

<span data-ttu-id="7a65c-109">Starší způsob, jak to provést, je obvykle závislý na řazení entity balíčku OData pomocí časového razítka a stránkování napříč velkou sadou výsledků dotazu `skip` pomocí `top` parametrů a (velikost stránky).</span><span class="sxs-lookup"><span data-stu-id="7a65c-109">The legacy way of doing this typically depended on sorting the OData package entity by a timestamp and paging across the massive result set using `skip` and `top` (page size) parameters.</span></span> <span data-ttu-id="7a65c-110">Tento přístup bohužel má několik nevýhod:</span><span class="sxs-lookup"><span data-stu-id="7a65c-110">Unfortunately, this approach has some drawbacks:</span></span>

- <span data-ttu-id="7a65c-111">Možnost chybějících balíčků, protože se provádějí dotazy na data, která často mění pořadí</span><span class="sxs-lookup"><span data-stu-id="7a65c-111">Possibility of missing packages, because the queries are being made on data that is often changing order</span></span>
- <span data-ttu-id="7a65c-112">Pomalá odezva na dotaz, protože dotazy nejsou optimalizované (nejvíc optimalizované dotazy jsou ty, které podporují scénář hlavní pro oficiálního klienta NuGet)</span><span class="sxs-lookup"><span data-stu-id="7a65c-112">Slow query response time, because the queries are not optimized (the most optimized queries are ones that support a mainline scenario for the official NuGet client)</span></span>
- <span data-ttu-id="7a65c-113">Použití zastaralých a nedokumentovaných rozhraní API, což znamená, že podpora takových dotazů v budoucnu není zaručená</span><span class="sxs-lookup"><span data-stu-id="7a65c-113">Use of deprecated and undocumented API, meaning the support of such queries in the future is not guaranteed</span></span>
- <span data-ttu-id="7a65c-114">Neschopnost přehrát historii v přesném pořadí, v jakém se ukázalo</span><span class="sxs-lookup"><span data-stu-id="7a65c-114">Inability to replay history in the exact order that it transpired</span></span>

<span data-ttu-id="7a65c-115">Z tohoto důvodu je možné za tímto účelem vyřešit výše uvedené scénáře a spolehlivě a budoucím způsobem kontrolovat.</span><span class="sxs-lookup"><span data-stu-id="7a65c-115">For this reason, the following guide can be followed to address the aforementioned scenarios in a more reliable and future-proof way.</span></span>

## <a name="overview"></a><span data-ttu-id="7a65c-116">Přehled</span><span class="sxs-lookup"><span data-stu-id="7a65c-116">Overview</span></span>

<span data-ttu-id="7a65c-117">Uprostřed tohoto průvodce je prostředek v [rozhraní NuGet API](../../api/overview.md) , který se nazývá **katalog**.</span><span class="sxs-lookup"><span data-stu-id="7a65c-117">At the center of this guide is resource in the [NuGet API](../../api/overview.md) called the **catalog**.</span></span> <span data-ttu-id="7a65c-118">Katalog je rozhraní API pro připojení, které umožňuje volajícímu zobrazit úplnou historii balíčků přidaných, upravených a odstraněných z nuget.org. Pokud vás zajímá všechny nebo dokonce podmnožiny balíčků publikovaných na nuget.org, je katalog skvělým způsobem, jak si udržet aktuální sadu aktuálně dostupných balíčků jako času.</span><span class="sxs-lookup"><span data-stu-id="7a65c-118">The catalog is an append-only API that allows the caller to see a full history of packages added to, modified, and deleted from nuget.org. If you are interested in all or even a subset of packages published to nuget.org, the catalog is a great way to stay up-to-date with the set of currently available packages as time goes on.</span></span>

<span data-ttu-id="7a65c-119">Tento průvodce je určený jako podrobný návod, ale pokud vás zajímá podrobné informace o katalogu, podívejte se na jeho [referenční dokument k rozhraní API](../../api/catalog-resource.md).</span><span class="sxs-lookup"><span data-stu-id="7a65c-119">This guide is intended to be a high-level walk-through but if you are interested in the fine-grain details of the catalog, see its [API reference document](../../api/catalog-resource.md).</span></span>

<span data-ttu-id="7a65c-120">Následující kroky lze implementovat v libovolném programovacím jazyce podle vašeho výběru.</span><span class="sxs-lookup"><span data-stu-id="7a65c-120">The following steps can be implemented in any programming language of your choice.</span></span> <span data-ttu-id="7a65c-121">Pokud chcete spustit úplnou ukázku, podívejte se na [ukázku C#](#c-sample-code) uvedenou níže.</span><span class="sxs-lookup"><span data-stu-id="7a65c-121">If you want a full running sample, take a look at the [C# sample](#c-sample-code) mentioned below.</span></span>

<span data-ttu-id="7a65c-122">Jinak postupujte podle příručky níže a vytvořte si spolehlivého čtečky katalogu.</span><span class="sxs-lookup"><span data-stu-id="7a65c-122">Otherwise, follow the guide below to build a reliable catalog reader.</span></span>

## <a name="initialize-a-cursor"></a><span data-ttu-id="7a65c-123">Inicializovat kurzor</span><span class="sxs-lookup"><span data-stu-id="7a65c-123">Initialize a cursor</span></span>

<span data-ttu-id="7a65c-124">Prvním krokem při sestavování spolehlivého čtečky katalogu je implementace kurzoru.</span><span class="sxs-lookup"><span data-stu-id="7a65c-124">The first step in building a reliable catalog reader is implementing a cursor.</span></span> <span data-ttu-id="7a65c-125">Úplné podrobnosti o návrhu kurzoru katalogu najdete v [referenčním dokumentu katalogu](../../api/catalog-resource.md#cursor).</span><span class="sxs-lookup"><span data-stu-id="7a65c-125">For full details about the design of a catalog cursor, see the [catalog reference document](../../api/catalog-resource.md#cursor).</span></span> <span data-ttu-id="7a65c-126">V krátké době je kurzor v čase, ke kterému jste v katalogu zpracovali události.</span><span class="sxs-lookup"><span data-stu-id="7a65c-126">In short, cursor is a point in time up to which you have processed events in the catalog.</span></span> <span data-ttu-id="7a65c-127">Události v katalogu reprezentují balíčky Publisher a další změny balíčků.</span><span class="sxs-lookup"><span data-stu-id="7a65c-127">Events in the catalog represent package publishes and other package changes.</span></span> <span data-ttu-id="7a65c-128">Pokud se zajímáte o všechny balíčky, které byly v minulosti publikovány do NuGet (od začátku času), měli byste ukazatel inicializovat na časové razítko "minimální hodnota" (např. `DateTime.MinValue` v rozhraní .NET).</span><span class="sxs-lookup"><span data-stu-id="7a65c-128">If you care about all packages ever published to NuGet (since the beginning of time), you would initialize your cursor to a "minimum value" timestamp (e.g. `DateTime.MinValue` in .NET).</span></span> <span data-ttu-id="7a65c-129">Pokud se budete zajímat jenom o balíčcích publikovaných od tohoto okamžiku, použije se aktuální časové razítko jako počáteční hodnota kurzoru.</span><span class="sxs-lookup"><span data-stu-id="7a65c-129">If you care only about packages published starting now, you would use the current timestamp as your initial cursor value.</span></span>

<span data-ttu-id="7a65c-130">V tomto průvodci inicializujeme kurzor na časové razítko před hodinovou známkou.</span><span class="sxs-lookup"><span data-stu-id="7a65c-130">For this guide, we'll initialize our cursor to a timestamp one hour ago.</span></span> <span data-ttu-id="7a65c-131">Prozatím stačí toto časové razítko uložit v paměti.</span><span class="sxs-lookup"><span data-stu-id="7a65c-131">For now, just save that timestamp in memory.</span></span>

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a><span data-ttu-id="7a65c-132">Určení adresy URL indexu katalogu</span><span class="sxs-lookup"><span data-stu-id="7a65c-132">Determine catalog index URL</span></span>

<span data-ttu-id="7a65c-133">Umístění každého prostředku (koncového bodu) v rozhraní NuGet API by mělo být zjištěno pomocí [indexu služby](../../api/service-index.md).</span><span class="sxs-lookup"><span data-stu-id="7a65c-133">The location of every resource (endpoint) in the NuGet API should be discovered using the [service index](../../api/service-index.md).</span></span> <span data-ttu-id="7a65c-134">Vzhledem k tomu, že se tato příručka zaměřuje na nuget.org, budeme používat index služby NuGet. org.</span><span class="sxs-lookup"><span data-stu-id="7a65c-134">Because this guide focuses on nuget.org, we'll be using nuget.org's service index.</span></span>

```
GET https://api.nuget.org/v3/index.json
```

<span data-ttu-id="7a65c-135">Dokument služby je dokument JSON obsahující všechny prostředky na nuget.org. Vyhledejte prostředek s `@type` hodnotou vlastnosti `Catalog/3.0.0` .</span><span class="sxs-lookup"><span data-stu-id="7a65c-135">The service document is JSON document containing all of the resources on nuget.org. Look for the resource having the `@type` property value of `Catalog/3.0.0`.</span></span> <span data-ttu-id="7a65c-136">Přidružená `@id` hodnota vlastnosti je adresa URL samotného indexu katalogu.</span><span class="sxs-lookup"><span data-stu-id="7a65c-136">The associated `@id` property value is the URL to the catalog index itself.</span></span> 

## <a name="find-new-catalog-leaves"></a><span data-ttu-id="7a65c-137">Najít nový katalog – listy</span><span class="sxs-lookup"><span data-stu-id="7a65c-137">Find new catalog leaves</span></span>

<span data-ttu-id="7a65c-138">Pomocí `@id` hodnoty vlastnosti nalezené v předchozím kroku Stáhněte rejstřík katalogu:</span><span class="sxs-lookup"><span data-stu-id="7a65c-138">Using the `@id` property value found in the previous step, download the catalog index:</span></span>

```
GET https://api.nuget.org/v3/catalog0/index.json
```

<span data-ttu-id="7a65c-139">Deserializace [indexu katalogu](../../api/catalog-resource.md#catalog-index).</span><span class="sxs-lookup"><span data-stu-id="7a65c-139">Deserialize the [catalog index](../../api/catalog-resource.md#catalog-index).</span></span> <span data-ttu-id="7a65c-140">Vyfiltrujte všechny [objekty stránky katalogu](../../api/catalog-resource.md#catalog-page-object-in-the-index) s `commitTimeStamp` menší nebo rovnou aktuální hodnotě kurzoru.</span><span class="sxs-lookup"><span data-stu-id="7a65c-140">Filter out all [catalog page objects](../../api/catalog-resource.md#catalog-page-object-in-the-index) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="7a65c-141">Pro každou zbývající stránku katalogu Stáhněte celý dokument pomocí `@id` Vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="7a65c-141">For each remaining catalog page, download the full document using the `@id` property.</span></span>

```
GET https://api.nuget.org/v3/catalog0/page2926.json
```

<span data-ttu-id="7a65c-142">Deserializace [stránky katalogu](../../api/catalog-resource.md#catalog-page).</span><span class="sxs-lookup"><span data-stu-id="7a65c-142">Deserialize the [catalog page](../../api/catalog-resource.md#catalog-page).</span></span> <span data-ttu-id="7a65c-143">Vyfiltrujte všechny [objekty listu katalogu](../../api/catalog-resource.md#catalog-item-object-in-a-page) s `commitTimeStamp` menší nebo rovnou aktuální hodnotě kurzoru.</span><span class="sxs-lookup"><span data-stu-id="7a65c-143">Filter out all [catalog leaf objects](../../api/catalog-resource.md#catalog-item-object-in-a-page) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="7a65c-144">Po stažení všech stránek katalogu, které nejsou odfiltrovány, máte sadu listů katalogu, která představuje balíčky, které byly publikovány, nejsou v seznamu, uvedeny nebo odstraněny v čase mezi časovým razítkem kurzoru a nyní.</span><span class="sxs-lookup"><span data-stu-id="7a65c-144">After you have downloaded all of the catalog pages not filtered out, you have a set of catalog leaf objects representing packages that have been published, unlisted, listed, or deleted in the time between your cursor timestamp and now.</span></span>

## <a name="process-catalog-leaves"></a><span data-ttu-id="7a65c-145">Ponechá katalog procesů</span><span class="sxs-lookup"><span data-stu-id="7a65c-145">Process catalog leaves</span></span>

<span data-ttu-id="7a65c-146">V tomto okamžiku můžete provádět libovolné vlastní zpracování, které byste chtěli v položkách katalogu.</span><span class="sxs-lookup"><span data-stu-id="7a65c-146">At this point, you can perform any custom processing you'd like on the catalog items.</span></span> <span data-ttu-id="7a65c-147">Pokud potřebujete jenom ID a verzi balíčku, můžete zkontrolovat `nuget:id` `nuget:version` vlastnosti a v objektech položky katalogu, které se nacházejí na stránkách.</span><span class="sxs-lookup"><span data-stu-id="7a65c-147">If all you need is the ID and version of the package, you can inspect the `nuget:id` and `nuget:version` properties on the catalog item objects found in the pages.</span></span> <span data-ttu-id="7a65c-148">Nezapomeňte se podívat na `@type` vlastnost a zjistit, zda se položka katalogu týká existujícího balíčku nebo odstraněného balíčku.</span><span class="sxs-lookup"><span data-stu-id="7a65c-148">Make sure to look at the `@type` property to know if the catalog item concerns an existing package or a deleted package.</span></span>

<span data-ttu-id="7a65c-149">Pokud vás zajímá metadata o balíčku (například popis, závislosti, velikost nupkg atd.), můžete načíst [dokument listu katalogu](../../api/catalog-resource.md#catalog-leaf) pomocí `@id` Vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="7a65c-149">If you are interested in the metadata about the package (such at the description, dependencies, .nupkg size, etc), you can fetch the [catalog leaf document](../../api/catalog-resource.md#catalog-leaf) using the `@id` property.</span></span>

```
GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json
```

<span data-ttu-id="7a65c-150">Tento dokument obsahuje všechna metadata zahrnutá v [prostředku metadat balíčku](../../api/registration-base-url-resource.md)a další.</span><span class="sxs-lookup"><span data-stu-id="7a65c-150">This document has all of the metadata included in the [package metadata resource](../../api/registration-base-url-resource.md), and more!</span></span>

<span data-ttu-id="7a65c-151">Tento krok je místo, kde implementujete vlastní logiku.</span><span class="sxs-lookup"><span data-stu-id="7a65c-151">This step is where you implement your custom logic.</span></span> <span data-ttu-id="7a65c-152">Ostatní kroky v této příručce jsou implementovány v podstatě stejně, jako bez ohledu na to, co v katalogu děláte.</span><span class="sxs-lookup"><span data-stu-id="7a65c-152">The other steps in this guide are implemented in pretty much the same way not matter what you are doing with the catalog leaves.</span></span>

### <a name="downloading-the-nupkg"></a><span data-ttu-id="7a65c-153">Stahuje se. nupkg.</span><span class="sxs-lookup"><span data-stu-id="7a65c-153">Downloading the .nupkg</span></span>

<span data-ttu-id="7a65c-154">Pokud vás zajímá stahování souborů. nupkg pro balíčky nalezené v katalogu, můžete použít [prostředek obsahu balíčku](../../api/package-base-address-resource.md).</span><span class="sxs-lookup"><span data-stu-id="7a65c-154">If you are interested in downloading the .nupkg's for packages found in the catalog, you can use the [package content resource](../../api/package-base-address-resource.md).</span></span> <span data-ttu-id="7a65c-155">Upozorňujeme ale, že mezi tím, kdy se balíček v katalogu nachází, existuje krátké zpoždění a když je dostupný v prostředku obsahu balíčku.</span><span class="sxs-lookup"><span data-stu-id="7a65c-155">However, note that there is a short delay between when a package is found in catalog and when it's available in the package content resource.</span></span> <span data-ttu-id="7a65c-156">Proto pokud při `404 Not Found` pokusu o stažení balíčku. nupkg pro balíček, který jste našli v katalogu, narazíte na soubor., zkuste to znovu později.</span><span class="sxs-lookup"><span data-stu-id="7a65c-156">Therefore, if you encounter `404 Not Found` when attempting to download a .nupkg for a package that you found in the catalog, simply retry a short time later.</span></span> <span data-ttu-id="7a65c-157">Oprava této prodlevy se sleduje podle problému GitHubu [NuGet/NuGetGallery # 3455](https://github.com/NuGet/NuGetGallery/issues/3455).</span><span class="sxs-lookup"><span data-stu-id="7a65c-157">Fixing this delay is tracked by GitHub issue [NuGet/NuGetGallery#3455](https://github.com/NuGet/NuGetGallery/issues/3455).</span></span>

## <a name="move-the-cursor-forward"></a><span data-ttu-id="7a65c-158">Přesunout kurzor vpřed</span><span class="sxs-lookup"><span data-stu-id="7a65c-158">Move the cursor forward</span></span>

<span data-ttu-id="7a65c-159">Po úspěšném zpracování položek katalogu je nutné určit novou hodnotu kurzoru, kterou chcete uložit.</span><span class="sxs-lookup"><span data-stu-id="7a65c-159">Once you have successfully processed the catalog items, you need to determine the new cursor value to save.</span></span> <span data-ttu-id="7a65c-160">To provedete tak, že vyhledáte maximum (nejnovější chronologicky) `commitTimeStamp` všech zpracovaných položek katalogu.</span><span class="sxs-lookup"><span data-stu-id="7a65c-160">To do this, find the maximum (latest chronologically) `commitTimeStamp` of all catalog items that you processed.</span></span> <span data-ttu-id="7a65c-161">Toto je nová hodnota kurzoru.</span><span class="sxs-lookup"><span data-stu-id="7a65c-161">This is your new cursor value.</span></span> <span data-ttu-id="7a65c-162">Uložte ho do některého trvalého úložiště, jako je databáze, systém souborů nebo úložiště objektů BLOB.</span><span class="sxs-lookup"><span data-stu-id="7a65c-162">Save it to some persistent store, like a database, file system, or blob storage.</span></span> <span data-ttu-id="7a65c-163">Pokud chcete získat další položky katalogu, stačí začít od [prvního kroku](#initialize-a-cursor) inicializací hodnoty kurzoru z tohoto trvalého úložiště.</span><span class="sxs-lookup"><span data-stu-id="7a65c-163">When you want to get more catalog items, simply start from the [first step](#initialize-a-cursor) by initializing your cursor value from this persistent store.</span></span>

<span data-ttu-id="7a65c-164">Pokud vaše aplikace vyvolá výjimku nebo chyby, nepřesunete kurzor vpřed.</span><span class="sxs-lookup"><span data-stu-id="7a65c-164">If your application throws an exception or faults, don't move the cursor forward.</span></span> <span data-ttu-id="7a65c-165">Přesunutí kurzoru má za to, že nikdy nemusíte před kurzorem znovu zpracovávat položky katalogu.</span><span class="sxs-lookup"><span data-stu-id="7a65c-165">Moving the cursor forward has the meaning that you never again need to process catalog items before your cursor.</span></span>

<span data-ttu-id="7a65c-166">Pokud z nějakého důvodu máte chybu ve způsobu zpracování katalogu, můžete jednoduše přesunout kurzor zpět v čase a nechat svůj kód znovu zpracovat staré položky katalogu.</span><span class="sxs-lookup"><span data-stu-id="7a65c-166">If, for some reason, you have a bug in how you process catalog leaves, you can simply move your cursor backward in time and allow your code to reprocess the old catalog items.</span></span>

## <a name="c-sample-code"></a><span data-ttu-id="7a65c-167">Ukázkový kód C#</span><span class="sxs-lookup"><span data-stu-id="7a65c-167">C# sample code</span></span>

<span data-ttu-id="7a65c-168">Vzhledem k tomu, že se jedná o sadu dokumentů JSON, které jsou dostupné přes protokol HTTP, může se jednat o použití libovolného programovacího jazyka, který má klienta HTTP a deserializaci JSON.</span><span class="sxs-lookup"><span data-stu-id="7a65c-168">Because the catalog is a set of JSON documents available over HTTP, it can be interacted with using any programming language that has an HTTP client and JSON deserializer.</span></span>

<span data-ttu-id="7a65c-169">Ukázky v jazyce C# jsou k dispozici v [úložišti NuGet/Samples](https://github.com/NuGet/Samples/tree/main/CatalogReaderExample).</span><span class="sxs-lookup"><span data-stu-id="7a65c-169">C# samples are available in the [NuGet/Samples repository](https://github.com/NuGet/Samples/tree/main/CatalogReaderExample).</span></span>

```cli
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a><span data-ttu-id="7a65c-170">Katalogová sada SDK</span><span class="sxs-lookup"><span data-stu-id="7a65c-170">Catalog SDK</span></span>

<span data-ttu-id="7a65c-171">Nejjednodušší způsob, jak využít katalog, je použít předběžnou verzi balíčku sady SDK katalogu .NET `NuGet.Protocol.Catalog` , která je k dispozici na Azure Artifacts pomocí následující zdrojové adresy URL balíčku NuGet: `https://pkgs.dev.azure.com/dnceng/public/_packaging/nuget-build/nuget/v3/index.json` .</span><span class="sxs-lookup"><span data-stu-id="7a65c-171">The easiest way to consume the catalog is to use the pre-release .NET catalog SDK package `NuGet.Protocol.Catalog`, which is available on Azure Artifacts using the following NuGet package source URL: `https://pkgs.dev.azure.com/dnceng/public/_packaging/nuget-build/nuget/v3/index.json`.</span></span>

<span data-ttu-id="7a65c-172">Tento balíček můžete nainstalovat do projektu kompatibilního se systémem `netstandard1.3` nebo vyšším (například .NET Framework 4,6).</span><span class="sxs-lookup"><span data-stu-id="7a65c-172">You can install this package to a project compatible with `netstandard1.3` or greater (such as .NET Framework 4.6).</span></span>

<span data-ttu-id="7a65c-173">Ukázka použití tohoto balíčku je k dispozici na GitHubu v [projektu NuGet. Protocol. Catalog. Sample](https://github.com/NuGet/Samples/tree/main/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).</span><span class="sxs-lookup"><span data-stu-id="7a65c-173">A sample using this package is available on GitHub in the [NuGet.Protocol.Catalog.Sample project](https://github.com/NuGet/Samples/tree/main/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="7a65c-174">Ukázkový výstup</span><span class="sxs-lookup"><span data-stu-id="7a65c-174">Sample output</span></span>

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

### <a name="minimal-sample"></a><span data-ttu-id="7a65c-175">Minimální vzorek</span><span class="sxs-lookup"><span data-stu-id="7a65c-175">Minimal sample</span></span>

<span data-ttu-id="7a65c-176">Příklad s menším počtem závislostí, které ilustrují interakci s katalogem, naleznete v tématu [CatalogReaderExample Sample Project](https://github.com/NuGet/Samples/tree/main/CatalogReaderExample/CatalogReaderExample).</span><span class="sxs-lookup"><span data-stu-id="7a65c-176">For an example with fewer dependencies that illustrates the interaction with the catalog in more detail, see the [CatalogReaderExample sample project](https://github.com/NuGet/Samples/tree/main/CatalogReaderExample/CatalogReaderExample).</span></span> <span data-ttu-id="7a65c-177">Projekt cílí na `netcoreapp2.0` a závisí na [4.4.0 NuGet. Protocol](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (pro překlad indexu služby) a [Newtonsoft.Jsv 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (pro deserializaci JSON).</span><span class="sxs-lookup"><span data-stu-id="7a65c-177">The project targets `netcoreapp2.0` and depends on the [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (for resolving the service index) and [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (for JSON deserialization).</span></span>

<span data-ttu-id="7a65c-178">Hlavní logika kódu je viditelná v [souboru program. cs](https://github.com/NuGet/Samples/blob/main/CatalogReaderExample/CatalogReaderExample/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="7a65c-178">The main logic of the code is visible in the [Program.cs file](https://github.com/NuGet/Samples/blob/main/CatalogReaderExample/CatalogReaderExample/Program.cs).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="7a65c-179">Ukázkový výstup</span><span class="sxs-lookup"><span data-stu-id="7a65c-179">Sample output</span></span>

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
