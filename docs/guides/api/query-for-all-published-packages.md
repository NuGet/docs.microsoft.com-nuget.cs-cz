---
title: Dotaz na všechny balíčky publikované do nuget.org
description: Pomocí rozhraní API NuGet se můžete dotazovat na všechny balíčky publikované na nuget.org a v průběhu času zůstat v aktuálním stavu.
author: joelverhagen
ms.author: jver
ms.date: 11/02/2017
ms.topic: tutorial
ms.reviewer: kraigb
ms.openlocfilehash: 7e611b568538e0acfcbad2e5d986a0f9382ac8fd
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774118"
---
# <a name="query-for-all-packages-published-to-nugetorg"></a>Dotaz na všechny balíčky publikované do nuget.org

Jeden společný vzor dotazu na starší verzi rozhraní OData v2 API vytvořil výčet všech balíčků publikovaných do nuget.org, seřazené podle toho, kdy byl balíček publikovaný. Scénáře, které vyžadují tento druh dotazů na nuget.org, se výrazně liší:

- Úplné replikace nuget.org
- Zjišťování, kdy byly vydány nové verze balíčků
- Hledání balíčků, které jsou závislé na vašem balíčku

Starší způsob, jak to provést, je obvykle závislý na řazení entity balíčku OData pomocí časového razítka a stránkování napříč velkou sadou výsledků dotazu `skip` pomocí `top` parametrů a (velikost stránky). Tento přístup bohužel má několik nevýhod:

- Možnost chybějících balíčků, protože se provádějí dotazy na data, která často mění pořadí
- Pomalá odezva na dotaz, protože dotazy nejsou optimalizované (nejvíc optimalizované dotazy jsou ty, které podporují scénář hlavní pro oficiálního klienta NuGet)
- Použití zastaralých a nedokumentovaných rozhraní API, což znamená, že podpora takových dotazů v budoucnu není zaručená
- Neschopnost přehrát historii v přesném pořadí, v jakém se ukázalo

Z tohoto důvodu je možné za tímto účelem vyřešit výše uvedené scénáře a spolehlivě a budoucím způsobem kontrolovat.

## <a name="overview"></a>Přehled

Uprostřed tohoto průvodce je prostředek v [rozhraní NuGet API](../../api/overview.md) , který se nazývá **katalog**. Katalog je rozhraní API pro připojení, které umožňuje volajícímu zobrazit úplnou historii balíčků přidaných, upravených a odstraněných z nuget.org. Pokud vás zajímá všechny nebo dokonce podmnožiny balíčků publikovaných na nuget.org, je katalog skvělým způsobem, jak si udržet aktuální sadu aktuálně dostupných balíčků jako času.

Tento průvodce je určený jako podrobný návod, ale pokud vás zajímá podrobné informace o katalogu, podívejte se na jeho [referenční dokument k rozhraní API](../../api/catalog-resource.md).

Následující kroky lze implementovat v libovolném programovacím jazyce podle vašeho výběru. Pokud chcete spustit úplnou ukázku, podívejte se na [ukázku C#](#c-sample-code) uvedenou níže.

Jinak postupujte podle příručky níže a vytvořte si spolehlivého čtečky katalogu.

## <a name="initialize-a-cursor"></a>Inicializovat kurzor

Prvním krokem při sestavování spolehlivého čtečky katalogu je implementace kurzoru. Úplné podrobnosti o návrhu kurzoru katalogu najdete v [referenčním dokumentu katalogu](../../api/catalog-resource.md#cursor). V krátké době je kurzor v čase, ke kterému jste v katalogu zpracovali události. Události v katalogu reprezentují balíčky Publisher a další změny balíčků. Pokud se zajímáte o všechny balíčky, které byly v minulosti publikovány do NuGet (od začátku času), měli byste ukazatel inicializovat na časové razítko "minimální hodnota" (např. `DateTime.MinValue` v rozhraní .NET). Pokud se budete zajímat jenom o balíčcích publikovaných od tohoto okamžiku, použije se aktuální časové razítko jako počáteční hodnota kurzoru.

V tomto průvodci inicializujeme kurzor na časové razítko před hodinovou známkou. Prozatím stačí toto časové razítko uložit v paměti.

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a>Určení adresy URL indexu katalogu

Umístění každého prostředku (koncového bodu) v rozhraní NuGet API by mělo být zjištěno pomocí [indexu služby](../../api/service-index.md). Vzhledem k tomu, že se tato příručka zaměřuje na nuget.org, budeme používat index služby NuGet. org.

```
GET https://api.nuget.org/v3/index.json
```

Dokument služby je dokument JSON obsahující všechny prostředky na nuget.org. Vyhledejte prostředek s `@type` hodnotou vlastnosti `Catalog/3.0.0` . Přidružená `@id` hodnota vlastnosti je adresa URL samotného indexu katalogu. 

## <a name="find-new-catalog-leaves"></a>Najít nový katalog – listy

Pomocí `@id` hodnoty vlastnosti nalezené v předchozím kroku Stáhněte rejstřík katalogu:

```
GET https://api.nuget.org/v3/catalog0/index.json
```

Deserializace [indexu katalogu](../../api/catalog-resource.md#catalog-index). Vyfiltrujte všechny [objekty stránky katalogu](../../api/catalog-resource.md#catalog-page-object-in-the-index) s `commitTimeStamp` menší nebo rovnou aktuální hodnotě kurzoru.

Pro každou zbývající stránku katalogu Stáhněte celý dokument pomocí `@id` Vlastnosti.

```
GET https://api.nuget.org/v3/catalog0/page2926.json
```

Deserializace [stránky katalogu](../../api/catalog-resource.md#catalog-page). Vyfiltrujte všechny [objekty listu katalogu](../../api/catalog-resource.md#catalog-item-object-in-a-page) s `commitTimeStamp` menší nebo rovnou aktuální hodnotě kurzoru.

Po stažení všech stránek katalogu, které nejsou odfiltrovány, máte sadu listů katalogu, která představuje balíčky, které byly publikovány, nejsou v seznamu, uvedeny nebo odstraněny v čase mezi časovým razítkem kurzoru a nyní.

## <a name="process-catalog-leaves"></a>Ponechá katalog procesů

V tomto okamžiku můžete provádět libovolné vlastní zpracování, které byste chtěli v položkách katalogu. Pokud potřebujete jenom ID a verzi balíčku, můžete zkontrolovat `nuget:id` `nuget:version` vlastnosti a v objektech položky katalogu, které se nacházejí na stránkách. Nezapomeňte se podívat na `@type` vlastnost a zjistit, zda se položka katalogu týká existujícího balíčku nebo odstraněného balíčku.

Pokud vás zajímá metadata o balíčku (například popis, závislosti, velikost nupkg atd.), můžete načíst [dokument listu katalogu](../../api/catalog-resource.md#catalog-leaf) pomocí `@id` Vlastnosti.

```
GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json
```

Tento dokument obsahuje všechna metadata zahrnutá v [prostředku metadat balíčku](../../api/registration-base-url-resource.md)a další.

Tento krok je místo, kde implementujete vlastní logiku. Ostatní kroky v této příručce jsou implementovány v podstatě stejně, jako bez ohledu na to, co v katalogu děláte.

### <a name="downloading-the-nupkg"></a>Stahuje se. nupkg.

Pokud vás zajímá stahování souborů. nupkg pro balíčky nalezené v katalogu, můžete použít [prostředek obsahu balíčku](../../api/package-base-address-resource.md). Upozorňujeme ale, že mezi tím, kdy se balíček v katalogu nachází, existuje krátké zpoždění a když je dostupný v prostředku obsahu balíčku. Proto pokud při `404 Not Found` pokusu o stažení balíčku. nupkg pro balíček, který jste našli v katalogu, narazíte na soubor., zkuste to znovu později. Oprava této prodlevy se sleduje podle problému GitHubu [NuGet/NuGetGallery # 3455](https://github.com/NuGet/NuGetGallery/issues/3455).

## <a name="move-the-cursor-forward"></a>Přesunout kurzor vpřed

Po úspěšném zpracování položek katalogu je nutné určit novou hodnotu kurzoru, kterou chcete uložit. To provedete tak, že vyhledáte maximum (nejnovější chronologicky) `commitTimeStamp` všech zpracovaných položek katalogu. Toto je nová hodnota kurzoru. Uložte ho do některého trvalého úložiště, jako je databáze, systém souborů nebo úložiště objektů BLOB. Pokud chcete získat další položky katalogu, stačí začít od [prvního kroku](#initialize-a-cursor) inicializací hodnoty kurzoru z tohoto trvalého úložiště.

Pokud vaše aplikace vyvolá výjimku nebo chyby, nepřesunete kurzor vpřed. Přesunutí kurzoru má za to, že nikdy nemusíte před kurzorem znovu zpracovávat položky katalogu.

Pokud z nějakého důvodu máte chybu ve způsobu zpracování katalogu, můžete jednoduše přesunout kurzor zpět v čase a nechat svůj kód znovu zpracovat staré položky katalogu.

## <a name="c-sample-code"></a>Ukázkový kód C#

Vzhledem k tomu, že se jedná o sadu dokumentů JSON, které jsou dostupné přes protokol HTTP, může se jednat o použití libovolného programovacího jazyka, který má klienta HTTP a deserializaci JSON.

Ukázky v jazyce C# jsou k dispozici v [úložišti NuGet/Samples](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).

```cli
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a>Katalogová sada SDK

Nejjednodušší způsob, jak využít katalog, je použít předběžnou verzi balíčku sady SDK katalogu .NET `NuGet.Protocol.Catalog` , která je k dispozici na Azure Artifacts pomocí následující zdrojové adresy URL balíčku NuGet: `https://pkgs.dev.azure.com/dnceng/public/_packaging/nuget-build/nuget/v3/index.json` .

Tento balíček můžete nainstalovat do projektu kompatibilního se systémem `netstandard1.3` nebo vyšším (například .NET Framework 4,6).

Ukázka použití tohoto balíčku je k dispozici na GitHubu v [projektu NuGet. Protocol. Catalog. Sample](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).

#### <a name="sample-output"></a>Ukázkový výstup

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

### <a name="minimal-sample"></a>Minimální vzorek

Příklad s menším počtem závislostí, které ilustrují interakci s katalogem, naleznete v tématu [CatalogReaderExample Sample Project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample). Projekt cílí na `netcoreapp2.0` a závisí na [4.4.0 NuGet. Protocol](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (pro překlad indexu služby) a [Newtonsoft.Jsv 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (pro deserializaci JSON).

Hlavní logika kódu je viditelná v [souboru program.cs](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).

#### <a name="sample-output"></a>Ukázkový výstup

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
