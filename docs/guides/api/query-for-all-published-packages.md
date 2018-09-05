---
title: Dotaz pro všechny balíčky, které jsou publikovány na nuget.org
description: Pomocí rozhraní API pro NuGet, se můžete dotazovat na všechny balíčky, které jsou publikovány na nuget.org a přehled o aktuálním dění v čase.
author: joelverhagen
ms.author: jver
ms.date: 11/02/2017
ms.topic: tutorial
ms.reviewer: kraigb
ms.openlocfilehash: 0bd21c427b5b89ae9e5f1500d75e1bf63a96e828
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551075"
---
# <a name="query-for-all-packages-published-to-nugetorg"></a><span data-ttu-id="75590-103">Dotaz pro všechny balíčky, které jsou publikovány na nuget.org</span><span class="sxs-lookup"><span data-stu-id="75590-103">Query for all packages published to nuget.org</span></span>

<span data-ttu-id="75590-104">Jeden běžný vzor dotazu na starší verze OData V2 API se výčet všech balíčků, které jsou publikovány na nuget.org, seřazené podle při publikování balíčku.</span><span class="sxs-lookup"><span data-stu-id="75590-104">One common query pattern on the legacy OData V2 API was enumerating all packages published to nuget.org, ordered by when the package was published.</span></span> <span data-ttu-id="75590-105">Scénáře, které vyžadují tento druh dotazu na nuget.org se velmi liší:</span><span class="sxs-lookup"><span data-stu-id="75590-105">Scenarios requiring this kind of query against nuget.org vary widely:</span></span>

- <span data-ttu-id="75590-106">Zcela replikaci nuget.org</span><span class="sxs-lookup"><span data-stu-id="75590-106">Replicating nuget.org entirely</span></span>
- <span data-ttu-id="75590-107">Zjištění, kdy balíčky obsahují nové vydané verze</span><span class="sxs-lookup"><span data-stu-id="75590-107">Detecting when packages have new versions released</span></span>
- <span data-ttu-id="75590-108">Hledání balíčky, které závisí na balíčku</span><span class="sxs-lookup"><span data-stu-id="75590-108">Finding packages that depend on your package</span></span>

<span data-ttu-id="75590-109">Starším způsobem udělat to obvykle závisí na balíčku entity OData řazení podle časového razítka a stránkování ve výsledku obrovské sady s použitím `skip` a `top` parametry (velikost stránky).</span><span class="sxs-lookup"><span data-stu-id="75590-109">The legacy way of doing this typically depended on sorting the OData package entity by a timestamp and paging across the massive result set using `skip` and `top` (page size) parameters.</span></span> <span data-ttu-id="75590-110">Bohužel tento přístup má určité nevýhody:</span><span class="sxs-lookup"><span data-stu-id="75590-110">Unfortunately, this approach has some drawbacks:</span></span>

- <span data-ttu-id="75590-111">Možnost chybějící balíčky, protože se provádějí dotazy na data, která se často mění pořadí</span><span class="sxs-lookup"><span data-stu-id="75590-111">Possibility of missing packages, because the queries are being made on data that is often changing order</span></span>
- <span data-ttu-id="75590-112">Dlouhá doba odezvy dotazů, protože nejsou optimalizované dotazy (nejvíce optimalizované dotazy jsou ty, které podporují hlavní scénáře pro oficiální klienta NuGet)</span><span class="sxs-lookup"><span data-stu-id="75590-112">Slow query response time, because the queries are not optimized (the most optimized queries are ones that support a mainline scenario for the official NuGet client)</span></span>
- <span data-ttu-id="75590-113">Není zaručeno, že použití zastaralé a nedokumentované rozhraní API, to znamená podpora takové dotazy v budoucnu</span><span class="sxs-lookup"><span data-stu-id="75590-113">Use of deprecated and undocumented API, meaning the support of such queries in the future is not guaranteed</span></span>
- <span data-ttu-id="75590-114">Neschopnost přehrát historie v uvedeném pořadí, ukázalo</span><span class="sxs-lookup"><span data-stu-id="75590-114">Inability to replay history in the exact order that it transpired</span></span>

<span data-ttu-id="75590-115">Z tohoto důvodu platí následující pokyny k řešení výše uvedených scénářů spolehlivější a budoucnosti způsobem.</span><span class="sxs-lookup"><span data-stu-id="75590-115">For this reason, the following guide can be followed to address the aforementioned scenarios in a more reliable and future-proof way.</span></span>

## <a name="overview"></a><span data-ttu-id="75590-116">Přehled</span><span class="sxs-lookup"><span data-stu-id="75590-116">Overview</span></span>

<span data-ttu-id="75590-117">Uprostřed tohoto průvodce je prostředek [NuGet rozhraní API](../../api/overview.md) volána **katalogu**.</span><span class="sxs-lookup"><span data-stu-id="75590-117">At the center of this guide is resource in the [NuGet API](../../api/overview.md) called the **catalog**.</span></span> <span data-ttu-id="75590-118">Katalog je rozhraní API nabízí jen možnost připojovat, které umožňuje volajícímu zobrazit úplnou historii balíčky se přidaly, upravit a odstranit z webu nuget.org. Pokud vás zajímají všechny nebo dokonce podmnožinu balíčky, které jsou publikovány na nuget.org, katalog je skvělý způsob, jak udržovat aktuální stav pomocí sadu aktuálně k dispozici balíčky odehrává.</span><span class="sxs-lookup"><span data-stu-id="75590-118">The catalog is an append-only API that allows the caller to see a full history of packages added to, modified, and deleted from nuget.org. If you are interested in all or even a subset of packages published to nuget.org, the catalog is a great way to stay up-to-date with the set of currently available packages as time goes on.</span></span>

<span data-ttu-id="75590-119">Tato příručka je určená podrobný návod, jak, ale pokud vás zajímají podrobnější informace katalogu, přečtěte si téma jeho [API referenční dokument](../../api/catalog-resource.md).</span><span class="sxs-lookup"><span data-stu-id="75590-119">This guide is intended to be a high-level walk-through but if you are interested in the fine-grain details of the catalog, see its [API reference document](../../api/catalog-resource.md).</span></span>

<span data-ttu-id="75590-120">Následující kroky je možné implementovat v libovolném programovacím jazyce podle vašeho výběru.</span><span class="sxs-lookup"><span data-stu-id="75590-120">The following steps can be implemented in any programming language of your choice.</span></span> <span data-ttu-id="75590-121">Pokud chcete úplnou ukázku spuštěné, podívejte se na [ukázka v jazyce C#](#c-sample-code) uvedených níže.</span><span class="sxs-lookup"><span data-stu-id="75590-121">If you want a full running sample, take a look at the [C# sample](#c-sample-code) mentioned below.</span></span>

<span data-ttu-id="75590-122">Jinak postupujte podle níže průvodce k vytvoření čtečky spolehlivé katalogu.</span><span class="sxs-lookup"><span data-stu-id="75590-122">Otherwise, follow the guide below to build a reliable catalog reader.</span></span>

## <a name="initialize-a-cursor"></a><span data-ttu-id="75590-123">Inicializovat kurzoru</span><span class="sxs-lookup"><span data-stu-id="75590-123">Initialize a cursor</span></span>

<span data-ttu-id="75590-124">Prvním krokem při sestavování spolehlivých katalogu čtečky implementuje kurzoru.</span><span class="sxs-lookup"><span data-stu-id="75590-124">The first step in building a reliable catalog reader is implementing a cursor.</span></span> <span data-ttu-id="75590-125">Úplné podrobnosti o návrhu kurzoru katalogu, najdete v článku [katalogu referenční dokument](../../api/catalog-resource.md#cursor).</span><span class="sxs-lookup"><span data-stu-id="75590-125">For full details about the design of a catalog cursor, see the [catalog reference document](../../api/catalog-resource.md#cursor).</span></span> <span data-ttu-id="75590-126">Stručně řečeno kurzor je bod v čase, které byly zpracovány události v katalogu.</span><span class="sxs-lookup"><span data-stu-id="75590-126">In short, cursor is a point in time up to which you have processed events in the catalog.</span></span> <span data-ttu-id="75590-127">Publikuje události v balíčku představují katalogu a změní jiný balíček.</span><span class="sxs-lookup"><span data-stu-id="75590-127">Events in the catalog represent package publishes and other package changes.</span></span> <span data-ttu-id="75590-128">Pokud vás zajímají všechny balíčky publikovanou NuGet (od počátku času), by se inicializovat kurzor do časového razítka "minimální hodnota" (například `DateTime.MinValue` v rozhraní .NET).</span><span class="sxs-lookup"><span data-stu-id="75590-128">If you care about all packages ever published to NuGet (since the beginning of time), you would initialize your cursor to a "minimum value" timestamp (e.g. `DateTime.MinValue` in .NET).</span></span> <span data-ttu-id="75590-129">Pokud vám záleží jenom publikované balíčky teď spouští, použijete aktuální časové razítko jako hodnota počáteční kurzoru.</span><span class="sxs-lookup"><span data-stu-id="75590-129">If you care only about packages published starting now, you would use the current timestamp as your initial cursor value.</span></span>

<span data-ttu-id="75590-130">Pro tohoto průvodce budete inicializujeme naše kurzor do časového razítka jednu hodinu před.</span><span class="sxs-lookup"><span data-stu-id="75590-130">For this guide, we'll initialize our cursor to a timestamp one hour ago.</span></span> <span data-ttu-id="75590-131">Teď stačí uložte tohoto časového razítka v paměti.</span><span class="sxs-lookup"><span data-stu-id="75590-131">For now, just save that timestamp in memory.</span></span>

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a><span data-ttu-id="75590-132">Určit adresu URL katalogu indexu</span><span class="sxs-lookup"><span data-stu-id="75590-132">Determine catalog index URL</span></span>

<span data-ttu-id="75590-133">Umístění všech prostředků (koncový bod) v rozhraní API NuGet by měly být zjištěny pomocí [index služby](../../api/service-index.md).</span><span class="sxs-lookup"><span data-stu-id="75590-133">The location of every resource (endpoint) in the NuGet API should be discovered using the [service index](../../api/service-index.md).</span></span> <span data-ttu-id="75590-134">Protože tento průvodce se zaměřuje na nuget.org, budeme používat index služby nuget.org.</span><span class="sxs-lookup"><span data-stu-id="75590-134">Because this guide focuses on nuget.org, we'll be using nuget.org's service index.</span></span>

    GET https://api.nuget.org/v3/index.json

<span data-ttu-id="75590-135">Dokument služby je dokument JSON obsahující všechny prostředky na nuget.org. Vyhledejte prostředek s `@type` hodnotou vlastnosti `Catalog/3.0.0`.</span><span class="sxs-lookup"><span data-stu-id="75590-135">The service document is JSON document containing all of the resources on nuget.org. Look for the resource having the `@type` property value of `Catalog/3.0.0`.</span></span> <span data-ttu-id="75590-136">Přidružené `@id` hodnota vlastnosti je adresa URL samotného index katalogu.</span><span class="sxs-lookup"><span data-stu-id="75590-136">The associated `@id` property value is the URL to the catalog index itself.</span></span> 

## <a name="find-new-catalog-leaves"></a><span data-ttu-id="75590-137">Najít nové ponechá katalogu</span><span class="sxs-lookup"><span data-stu-id="75590-137">Find new catalog leaves</span></span>

<span data-ttu-id="75590-138">Použití `@id` vlastnost hodnotu nalezenou v předchozím kroku, stáhněte si index katalogu:</span><span class="sxs-lookup"><span data-stu-id="75590-138">Using the `@id` property value found in the previous step, download the catalog index:</span></span>

    GET https://api.nuget.org/v3/catalog0/index.json

<span data-ttu-id="75590-139">Deserializaci [index katalogu](../../api/catalog-resource.md#catalog-index).</span><span class="sxs-lookup"><span data-stu-id="75590-139">Deserialize the [catalog index](../../api/catalog-resource.md#catalog-index).</span></span> <span data-ttu-id="75590-140">Filtrování všeho [stránky objektů katalogu](../../api/catalog-resource.md#catalog-page-object-in-the-index) s `commitTimeStamp` menší nebo rovna hodnotě aktuální kurzor.</span><span class="sxs-lookup"><span data-stu-id="75590-140">Filter out all [catalog page objects](../../api/catalog-resource.md#catalog-page-object-in-the-index) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="75590-141">Pro každý zbývající stránky katalogu stáhnout pomocí celého dokumentu `@id` vlastnost.</span><span class="sxs-lookup"><span data-stu-id="75590-141">For each remaining catalog page, download the full document using the `@id` property.</span></span>

    GET https://api.nuget.org/v3/catalog0/page2926.json

<span data-ttu-id="75590-142">Deserializaci [stránky Katalog](../../api/catalog-resource.md#catalog-page).</span><span class="sxs-lookup"><span data-stu-id="75590-142">Deserialize the [catalog page](../../api/catalog-resource.md#catalog-page).</span></span> <span data-ttu-id="75590-143">Filtrování všeho [katalogu listové objekty](../../api/catalog-resource.md#catalog-item-object-in-a-page) s `commitTimeStamp` menší nebo rovna hodnotě aktuální kurzor.</span><span class="sxs-lookup"><span data-stu-id="75590-143">Filter out all [catalog leaf objects](../../api/catalog-resource.md#catalog-item-object-in-a-page) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="75590-144">Po stažení všechny stránky katalogu není odfiltrovat, máte sadu katalogu objekty typu list představují balíčky, které byly publikované, neuvedené v seznamu, uvedené nebo odstraněné v době mezi vaše časové razítko kurzoru a nyní.</span><span class="sxs-lookup"><span data-stu-id="75590-144">After you have downloaded all of the catalog pages not filtered out, you have a set of catalog leaf objects representing packages that have been published, unlisted, listed, or deleted in the time between your cursor timestamp and now.</span></span>

## <a name="process-catalog-leaves"></a><span data-ttu-id="75590-145">Opustí proces katalogu</span><span class="sxs-lookup"><span data-stu-id="75590-145">Process catalog leaves</span></span>

<span data-ttu-id="75590-146">V tomto okamžiku můžete provést vlastní zpracování, které chcete na položky katalogu.</span><span class="sxs-lookup"><span data-stu-id="75590-146">At this point, you can perform any custom processing you'd like on the catalog items.</span></span> <span data-ttu-id="75590-147">Pokud je všechno, co potřebujete ID a verzi balíčku, si můžete prohlédnout `nuget:id` a `nuget:version` položky objekty nalezené na stránkách vlastností v katalogu.</span><span class="sxs-lookup"><span data-stu-id="75590-147">If all you need is the ID and version of the package, you can inspect the `nuget:id` and `nuget:version` properties on the catalog item objects found in the pages.</span></span> <span data-ttu-id="75590-148">Ujistěte se, že se podívat `@type` vlastnost vědět, pokud položka katalogu se týká existující balíček nebo odstranil balíček.</span><span class="sxs-lookup"><span data-stu-id="75590-148">Make sure to look at the `@type` property to know if the catalog item concerns an existing package or a deleted package.</span></span>

<span data-ttu-id="75590-149">Pokud vás zajímají metadata o balíčku (například na popis, závislosti, velikost .nupkg atd), můžete načíst [katalogu listu dokumentu](../../api/catalog-resource.md#catalog-leaf) pomocí `@id` vlastnost.</span><span class="sxs-lookup"><span data-stu-id="75590-149">If you are interested in the metadata about the package (such at the description, dependencies, .nupkg size, etc), you can fetch the [catalog leaf document](../../api/catalog-resource.md#catalog-leaf) using the `@id` property.</span></span>

    GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

<span data-ttu-id="75590-150">Tento dokument obsahuje všechna metadata součástí [balíček metadata resource](../../api/registration-base-url-resource.md)a další!</span><span class="sxs-lookup"><span data-stu-id="75590-150">This document has all of the metadata included in the [package metadata resource](../../api/registration-base-url-resource.md), and more!</span></span>

<span data-ttu-id="75590-151">Tento krok je, kde můžete implementovat vlastní logiku.</span><span class="sxs-lookup"><span data-stu-id="75590-151">This step is where you implement your custom logic.</span></span> <span data-ttu-id="75590-152">Další kroky v této příručce jsou implementovány v pretty skoro stejné způsobem není důležité, co právě děláte s listy katalogu.</span><span class="sxs-lookup"><span data-stu-id="75590-152">The other steps in this guide are implemented in pretty much the same way not matter what you are doing with the catalog leaves.</span></span>

### <a name="downloading-the-nupkg"></a><span data-ttu-id="75590-153">Stahuje .nupkg</span><span class="sxs-lookup"><span data-stu-id="75590-153">Downloading the .nupkg</span></span>

<span data-ttu-id="75590-154">Pokud vás zajímá při stahování balíčků .nupkg v katalogu nalezen, můžete použít [balíček obsahu prostředku](../../api/package-base-address-resource.md).</span><span class="sxs-lookup"><span data-stu-id="75590-154">If you are interested in downloading the .nupkg's for packages found in the catalog, you can use the [package content resource](../../api/package-base-address-resource.md).</span></span> <span data-ttu-id="75590-155">Mějte však na paměti, že je prodleva mezi při balíčku se nachází v katalogu a když je k dispozici v balíčku obsahu prostředku.</span><span class="sxs-lookup"><span data-stu-id="75590-155">However, note that there is a short delay between when a package is found in catalog and when it's available in the package content resource.</span></span> <span data-ttu-id="75590-156">Proto pokud narazíte na `404 Not Found` při pokusu o stažení .nupkg pro balíček, který jste našli v katalogu, jednoduše opakujte krátkého formátu času později.</span><span class="sxs-lookup"><span data-stu-id="75590-156">Therefore, if you encounter `404 Not Found` when attempting to download a .nupkg for a package that you found in the catalog, simply retry a short time later.</span></span> <span data-ttu-id="75590-157">Oprava toto zpoždění je sledován pomocí funkce problém Githubu [NuGet/NuGetGallery #3455](https://github.com/NuGet/NuGetGallery/issues/3455).</span><span class="sxs-lookup"><span data-stu-id="75590-157">Fixing this delay is tracked by GitHub issue [NuGet/NuGetGallery#3455](https://github.com/NuGet/NuGetGallery/issues/3455).</span></span>

## <a name="move-the-cursor-forward"></a><span data-ttu-id="75590-158">Přesunutí kurzoru vpřed</span><span class="sxs-lookup"><span data-stu-id="75590-158">Move the cursor forward</span></span>

<span data-ttu-id="75590-159">Po úspěšném zpracování položek katalogu, je nutné určit nová hodnota kurzor uložte.</span><span class="sxs-lookup"><span data-stu-id="75590-159">Once you have successfully processed the catalog items, you need to determine the new cursor value to save.</span></span> <span data-ttu-id="75590-160">Chcete-li to provést, vyhledejte maximální (nejnovější chronologicky) `commitTimeStamp` všech položek katalogu, které můžete zpracovat.</span><span class="sxs-lookup"><span data-stu-id="75590-160">To do this, find the maximum (latest chronologically) `commitTimeStamp` of all catalog items that you processed.</span></span> <span data-ttu-id="75590-161">Toto je nová hodnota kurzoru.</span><span class="sxs-lookup"><span data-stu-id="75590-161">This is your new cursor value.</span></span> <span data-ttu-id="75590-162">Uložte ho do nějaké trvalého úložiště, jako jsou databáze, systém souborů nebo úložiště objektů blob.</span><span class="sxs-lookup"><span data-stu-id="75590-162">Save it to some persistent store, like a database, file system, or blob storage.</span></span> <span data-ttu-id="75590-163">Pokud chcete získat více položek katalogu, stačí spustit z [první krok](#initialize-a-cursor) podle inicializace kurzor hodnotu z této trvalého úložiště.</span><span class="sxs-lookup"><span data-stu-id="75590-163">When you want to get more catalog items, simply start from the [first step](#initialize-a-cursor) by initializing your cursor value from this persistent store.</span></span>

<span data-ttu-id="75590-164">Pokud vaše aplikace vyvolá výjimku nebo chyby, Nepřesouvat kurzor vpřed.</span><span class="sxs-lookup"><span data-stu-id="75590-164">If your application throws an exception or faults, don't move the cursor forward.</span></span> <span data-ttu-id="75590-165">V budoucnu kurzor má význam, který nikdy znovu potřebujete ke zpracování položek katalogu před kurzor.</span><span class="sxs-lookup"><span data-stu-id="75590-165">Moving the cursor forward has the meaning that you never again need to process catalog items before your cursor.</span></span>

<span data-ttu-id="75590-166">Pokud z nějakého důvodu máte chybu v o procesu katalogu opustí, stačí posunout kurzorem zpět v čase a umožňují váš kód za účelem opětovného zpracování staré položky katalogu.</span><span class="sxs-lookup"><span data-stu-id="75590-166">If, for some reason, you have a bug in how you process catalog leaves, you can simply move your cursor backward in time and allow your code to reprocess the old catalog items.</span></span>

## <a name="c-sample-code"></a><span data-ttu-id="75590-167">Vzorový kód jazyka C#</span><span class="sxs-lookup"><span data-stu-id="75590-167">C# sample code</span></span>

<span data-ttu-id="75590-168">Protože katalogu je sada dokumentů JSON, které jsou k dispozici prostřednictvím protokolu HTTP, může být interakci s použitím libovolného programovacího jazyka, který má klienta HTTP a JSON deserializátor.</span><span class="sxs-lookup"><span data-stu-id="75590-168">Because the catalog is a set of JSON documents available over HTTP, it can be interacted with using any programming language that has an HTTP client and JSON deserializer.</span></span>

<span data-ttu-id="75590-169">Jsou k dispozici v jazyce C# – ukázky [úložiště NuGet/Samples](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).</span><span class="sxs-lookup"><span data-stu-id="75590-169">C# samples are available in the [NuGet/Samples repository](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).</span></span>

```cli
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a><span data-ttu-id="75590-170">Katalog SDK</span><span class="sxs-lookup"><span data-stu-id="75590-170">Catalog SDK</span></span>

<span data-ttu-id="75590-171">Nejjednodušší způsob, jak využívat katalogu je použít balíček předběžné verze katalogu .NET SDK: [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog).</span><span class="sxs-lookup"><span data-stu-id="75590-171">The easiest way to consume the catalog is to use the pre-release .NET catalog SDK package: [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog).</span></span> <span data-ttu-id="75590-172">Tento balíček je k dispozici na `nuget-build` MyGet informační kanál, pro který použijete adresu URL zdroje balíčku NuGet `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="75590-172">This package is available on the `nuget-build` MyGet feed, for which you use the NuGet package source URL `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`.</span></span>

<span data-ttu-id="75590-173">Instalací tohoto balíčku do projektu, který je kompatibilní s `netstandard1.3` nebo větší (například rozhraní .NET Framework 4.6).</span><span class="sxs-lookup"><span data-stu-id="75590-173">You can install this package to a project compatible with `netstandard1.3` or greater (such as .NET Framework 4.6).</span></span>

<span data-ttu-id="75590-174">Pomocí tohoto balíčku ukázka je k dispozici na Githubu v [NuGet.Protocol.Catalog.Sample projektu](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).</span><span class="sxs-lookup"><span data-stu-id="75590-174">A sample using this package is available on GitHub in the [NuGet.Protocol.Catalog.Sample project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="75590-175">Ukázkový výstup</span><span class="sxs-lookup"><span data-stu-id="75590-175">Sample output</span></span>

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

### <a name="minimal-sample"></a><span data-ttu-id="75590-176">Minimální vzorek</span><span class="sxs-lookup"><span data-stu-id="75590-176">Minimal sample</span></span>

<span data-ttu-id="75590-177">Příklad s menším počtem závislosti, který znázorňuje interakci s katalogem podrobněji, najdete v článku [CatalogReaderExample ukázkový projekt](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample).</span><span class="sxs-lookup"><span data-stu-id="75590-177">For an example with fewer dependencies that illustrates the interaction with the catalog in more detail, see the [CatalogReaderExample sample project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample).</span></span> <span data-ttu-id="75590-178">Cíle projektu `netcoreapp2.0` a závisí [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (pro řešení index služby) a [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (pro deserializaci JSON).</span><span class="sxs-lookup"><span data-stu-id="75590-178">The project targets `netcoreapp2.0` and depends on the [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (for resolving the service index) and [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (for JSON deserialization).</span></span>

<span data-ttu-id="75590-179">Hlavní logika kód je viditelný [souboru Program.cs](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="75590-179">The main logic of the code is visible in the [Program.cs file](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="75590-180">Ukázkový výstup</span><span class="sxs-lookup"><span data-stu-id="75590-180">Sample output</span></span>

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
