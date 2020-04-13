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
# <a name="query-for-all-packages-published-to-nugetorg"></a>Dotaz na všechny balíčky publikované do nuget.org

Jeden společný vzor dotazu na starší rozhraní API OData V2 byl výčet všech balíčků publikovaných do nuget.org, seřazené při publikování balíčku. Scénáře, které vyžadují tento druh dotazu proti nuget.org se značně liší:

- Replikace nuget.org úplně
- Zjišťování, kdy jsou vydány nové verze
- Hledání balíčků, které závisí na vašem balíčku

Starší způsob, jak to udělat, obvykle závisí na řazení entity balíčku OData podle časového `skip` razítka a stránkování přes masivní sadu výsledků pomocí a `top` (velikost stránky) parametry. Bohužel, tento přístup má některé nevýhody:

- Možnost chybějících balíčků, protože dotazy jsou prováděny na data, která se často mění pořadí
- Pomalá doba odezvy dotazu, protože dotazy nejsou optimalizovány (nejvíce optimalizované dotazy jsou ty, které podporují hlavní scénář pro oficiální klientnu NuGet)
- Použití zastaralého a nedokumentovaného ROZHRANÍ API, což znamená, že podpora takových dotazů v budoucnu není zaručena
- Neschopnost přehrát historii v přesném pořadí, v jakém se objevila

Z tohoto důvodu lze sledovat následující příručku k řešení výše uvedených scénářů spolehlivějším způsobem, který obnaží budoucnost.

## <a name="overview"></a>Přehled

V centru této příručky je prostředek v [nuget api](../../api/overview.md) s názvem **katalogu**. Katalog je pouze připojit rozhraní API, které umožňuje volajícímu zobrazit úplnou historii balíčků přidaných, upravených a odstraněných z nuget.org. Máte-li zájem o všechny nebo dokonce podmnožinu balíčků publikovaných do nuget.org, katalog je skvělý způsob, jak zůstat up-to-date se sadou aktuálně dostupných balíčků, jak čas pokračuje.

Tato příručka má být na vysoké úrovni walk-through, ale pokud máte zájem o jemné zrnitosti podrobnosti katalogu, naleznete v jeho [referenčním dokumentu rozhraní API](../../api/catalog-resource.md).

Následující kroky mohou být implementovány v libovolném programovacím jazyce podle vašeho výběru. Pokud chcete úplné spuštění ukázky, podívejte se na [c# ukázku](#c-sample-code) uvedenou níže.

V opačném případě postupujte podle níže uvedeného průvodce a vytvořte spolehlivou čtečku katalogů.

## <a name="initialize-a-cursor"></a>Inicializovat kurzor

Prvním krokem při vytváření spolehlivé čtečky katalogů je implementace kurzoru. Podrobné informace o návrhu kurzoru katalogu naleznete v [referenčním dokumentu katalogu](../../api/catalog-resource.md#cursor). Stručně řečeno, kurzor je bod v čase, do kterého jste zpracovali události v katalogu. Události v katalogu představují publikování balíčků a další změny balíčků. Pokud vám záleží na všech balíčcích, které byly někdy publikovány na NuGet (od počátku času), inicializovali byste kurzor na časové razítko "minimální hodnoty" (např. `DateTime.MinValue` v .NET). Pokud vám záleží pouze na balíčcích publikovaných od nynějška, použijete aktuální časové razítko jako počáteční hodnotu kurzoru.

Pro tuto příručku budeme inicializovat náš kurzor na časové razítko před hodinou. Prozatím uložte to časové razítko do paměti.

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a>Určení adresy URL indexu katalogu

Umístění každého prostředku (koncového bodu) v rozhraní API NuGet by měla být zjištěna pomocí [indexu služby](../../api/service-index.md). Vzhledem k tomu, že tato příručka se zaměřuje na nuget.org, budeme používat nuget.org index služeb.

    GET https://api.nuget.org/v3/index.json

Servisní doklad je dokument JSON obsahující všechny prostředky na nuget.org. Vyhledejte prostředek s `@type` hodnotou `Catalog/3.0.0`vlastnosti . Přidružená `@id` hodnota vlastnosti je adresa URL samotného indexu katalogu. 

## <a name="find-new-catalog-leaves"></a>Najít nové katalogové listy

Pomocí `@id` hodnoty vlastnosti nalezené v předchozím kroku stáhněte index katalogu:

    GET https://api.nuget.org/v3/catalog0/index.json

Dekontujte [index katalogu](../../api/catalog-resource.md#catalog-index). Odfiltrujte všechny [objekty stránky katalogu](../../api/catalog-resource.md#catalog-page-object-in-the-index) s `commitTimeStamp` hodnotou aktuální kurzoru menší nebo rovnou.

Pro každou zbývající stránku katalogu stáhněte celý dokument pomocí vlastnosti. `@id`

    GET https://api.nuget.org/v3/catalog0/page2926.json

Dekontujte [stránku katalogu](../../api/catalog-resource.md#catalog-page). Odfiltrovat všechny [objekty listu katalogu](../../api/catalog-resource.md#catalog-item-object-in-a-page) s `commitTimeStamp` menší nebo rovna aktuální hodnotu kurzoru.

Po stažení všech stránek katalogu, které nejsou odfiltrovány, máte sadu objektů listu katalogu představující balíčky, které byly publikovány, neuvedeny, uvedeny nebo odstraněny v čase mezi časovým razítkem kurzoru a nyní.

## <a name="process-catalog-leaves"></a>Listy katalogu procesů

V tomto okamžiku můžete provádět jakékoli vlastní zpracování, které chcete na položky katalogu. Pokud vše, co potřebujete, je ID a verze `nuget:id` `nuget:version` balíčku, můžete zkontrolovat vlastnosti a na objekty položky katalogu nalezené na stránkách. Nezapomeňte se podívat `@type` na vlastnost, abyste zjistili, zda se položka katalogu týká existujícího balíčku nebo odstraněného balíčku.

Pokud vás zajímají metadata o balíčku (například v popisu, závislosti, .nupkg velikost, atd),můžete `@id` načíst katalog list [dokumentu](../../api/catalog-resource.md#catalog-leaf) pomocí vlastnosti.

    GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

Tento dokument obsahuje všechna metadata obsažená v [prostředku metadat balíčku](../../api/registration-base-url-resource.md)a další!

Tento krok je, kde implementovat vlastní logiku. Další kroky v této příručce jsou implementovány v podstatě stejným způsobem bez ohledu na to, co děláte s katalogu listy.

### <a name="downloading-the-nupkg"></a>Stahování .nupkg

Máte-li zájem o stažení .nupkg pro balíčky nalezené v katalogu, můžete použít [zdroj obsahu balíčku](../../api/package-base-address-resource.md). Všimněte si však, že je krátká prodleva mezi při nalezení balíčku v katalogu a kdy je k dispozici v prostředku obsahu balíčku. Proto pokud narazíte `404 Not Found` při pokusu o stažení .nupkg pro balíček, který jste našli v katalogu, jednoduše opakujte krátce později. Oprava tohoto zpoždění je sledována problémgithub [nuget/nugetgallery #3455](https://github.com/NuGet/NuGetGallery/issues/3455).

## <a name="move-the-cursor-forward"></a>Přesunutí kurzoru dopředu

Po úspěšném zpracování položek katalogu je třeba určit novou hodnotu kurzoru, kterou chcete uložit. Chcete-li to provést, najděte maximum `commitTimeStamp` (nejnovější chronologicky) všech položek katalogu, které jste zpracovali. Toto je vaše nová hodnota kurzoru. Uložte ji do některé ho trvaléúložiště, jako je databáze, systém souborů nebo úložiště objektů blob. Pokud chcete získat více položek katalogu, jednoduše začněte od [prvního kroku](#initialize-a-cursor) inicializací hodnoty kurzoru z tohoto trvalého úložiště.

Pokud vaše aplikace vyvolá výjimku nebo chyby, nepohybujte kurzorem dopředu. Přesunutí kurzoru dopředu má význam, že už nikdy nebudete muset zpracovávat položky katalogu před kurzorem.

Pokud z nějakého důvodu máte chybu v tom, jak zpracováváte listy katalogu, můžete jednoduše přesunout kurzor zpět v čase a povolit kódu znovu zpracovat staré položky katalogu.

## <a name="c-sample-code"></a>Ukázkový kód jazyka C#

Vzhledem k tomu, že katalog je sada dokumentů JSON k dispozici přes HTTP, může být v interakci s pomocí libovolného programovacího jazyka, který má klienta HTTP a JSON deserializer.

Ukázky jazyka C# jsou k dispozici v [úložišti NuGet/Samples](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).

```cli
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a>Sada SDK katalogu

Nejjednodušší způsob, jak využít katalog, je použít balíček sady SDK katalogu [.NET.](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog) Tento balíček je `nuget-build` k dispozici na myget kanálu, pro `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`které používáte nuget balíček zdroj URL .

Tento balíček můžete nainstalovat do `netstandard1.3` projektu kompatibilního s nebo vyšší (například rozhraní .NET Framework 4.6).

Ukázka pomocí tohoto balíčku je k dispozici na GitHubu v [projektu NuGet.Protocol.Catalog.Sample](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).

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

Příklad s menším počtem závislostí, který podrobněji ilustruje interakci s katalogem, naleznete v [ukázkovém projektu CatalogReaderExample](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample). Projekt se `netcoreapp2.0` zaměřuje a závisí na [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (pro řešení indexu služeb) a [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (pro deserializaci JSON).

Hlavní logika kódu je viditelná v [souboru Program.cs](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).

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
