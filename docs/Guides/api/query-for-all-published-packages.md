---
title: Dotaz pro všechny balíčky publikovaná nuget.org | Microsoft Docs
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 11/02/2017
ms.topic: tutorial
ms.prod: nuget
ms.technology: ''
description: Pomocí rozhraní API NuGet, se můžete dotazovat pro všechny balíčky, které jsou publikovány do nuget.org a vždy aktuální v průběhu času.
keywords: Rozhraní API NuGet výčet všechny balíčky, replikace balíčky NuGet rozhraní API, publikovat nejnovější balíčky do nuget.org
ms.reviewer:
- karann
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 5ea11e1b4edd87b6d30d3838986ca60aaa77870f
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="query-for-all-packages-published-to-nugetorg"></a>Dotaz pro všechny balíčky, které jsou publikovány do nuget.org

Jeden běžný vzor dotazu na starší verze rozhraní API V2 OData se vytváření výčtů pro všechny balíčky, které jsou publikovány do nuget.org, seřazené podle při publikování balíčku. Scénářům, které vyžadují tento druh dotazu vůči nuget.org se velmi liší:

- Zcela replikace nuget.org
- Zjištění, kdy balíčky obsahují vydání nové verze
- Hledání balíčky, které jsou závislé na váš balíček

Starší verze způsob to to obvykle závisí na balíček entity OData řazení podle časového razítka a stránkování napříč masivní výsledek nastavit pomocí `skip` a `top` parametry (velikost stránky). Bohužel se tento přístup má některé nevýhody:

- Možnost chybějících balíčků, protože dotazy jsou určené pro data, která se často mění pořadí
- Dlouhá doba odezvy dotazu, protože nejsou optimalizované dotazy (většina optimalizované dotazy jsou ty, které podporují nejdůležitějších scénář pro oficiální klienta NuGet)
- Použití zastaralé a nedokumentovanými rozhraní API v budoucnu znamená podpoře takové dotazy není zaručena.
- Neschopnost přehráním historie v uvedeném pořadí, které ukázalo

Z tohoto důvodu lze vyřešit výše uvedené scénáře způsobem spolehlivější a osvědčení do budoucna postupovat následovně.

## <a name="overview"></a>Přehled

V centru této příručky je prostředek [NuGet API](../../api/overview.md) názvem **katalogu**. Katalog je rozhraní API připojovacím, které umožňuje volajícímu najdete v části úplnou historii balíčky přidat, upravit a odstranit z nuget.org. Pokud vás zajímá všechny nebo i podmnožinu balíčky, které jsou publikovány do nuget.org, katalog je skvělým způsobem, jak zůstat odehrává aktuální sadu aktuálně dostupné balíčky.

Tato příručka je určena podrobný návod, ale pokud vás zajímají podrobnosti důkladnou katalogu, přečtěte si téma jeho [dokumentu Referenční dokumentace rozhraní API](../../api/catalog-resource.md).

Tyto kroky můžou se implementovat v jakékoli programovací jazyk podle vašeho výběru. Pokud chcete Úplná ukázka spuštěné, prohlédněte si [C# ukázka](#c-sample-code) uvedených níže.

Jinak postupujte podle níže průvodce k vytvoření čtečky spolehlivé katalogu.

## <a name="initialize-a-cursor"></a>Inicializace kurzoru

Prvním krokem při vytváření spolehlivé katalogu čtečky je implementace kurzoru. Úplné podrobnosti o návrhu kurzoru katalogu najdete v tématu [katalogu referenčním dokumentu](../../api/catalog-resource.md#cursor). Stručně řečeno kurzor je bod v čase, ke kterému mají zpracování událostí v katalogu. Publikuje události v balíčku představují katalogu a změní jiný balíček. Pokud se zajímáte o všech balíčků NuGet někdy publikovány (od začátku čas), můžete se inicializuje kurzor na časové razítko "minimální hodnota" (například `DateTime.MinValue` v rozhraní .NET). Pokud vám záleží jenom balíčky publikovaná od nyní, využije aktuální časové razítko jako hodnota počáteční kurzoru.

Tato příručka jsme budete inicializovat naše kurzoru časovým razítkem jednu hodinu před. Prozatím se právě uložte tento časové razítko v paměti.

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a>Určení adresy URL katalogu indexu

Umístění všech prostředků (koncový bod) v rozhraní API NuGet by měly být zjištěny pomocí [indexu služby](../../api/service-index.md). Protože tato příručka se zaměřuje na nuget.org, budeme používat nuget.org služby index.

    GET https://api.nuget.org/v3/index.json

Dokument služby je dokument JSON obsahující všechny prostředky v nuget.org. Vyhledejte prostředek s `@type` hodnota vlastnosti `Catalog/3.0.0`. Přidruženého `@id` hodnota vlastnosti je adresu URL katalogu index sám sebe. 

## <a name="find-new-catalog-leaves"></a>Najít nové nechá katalogu

Pomocí `@id` stáhnout index katalogu nalezena v předchozím kroku, hodnota vlastnosti:

    GET https://api.nuget.org/v3/catalog0/index.json

Deserializovat [katalogu index](../../api/catalog-resource.md#catalog-index). Filtrovat všechny [katalogu objekty stránky](../../api/catalog-resource.md#catalog-page-object-in-the-index) s `commitTimeStamp` menší než nebo rovna hodnotě aktuální kurzor.

Pro každý zbývající stránku katalogu stahování celého dokumentu pomocí `@id` vlastnost.

    GET https://api.nuget.org/v3/catalog0/page2926.json

Deserializovat [katalogu stránky](../../api/catalog-resource.md#catalog-page). Filtrovat všechny [katalogu objekty listu](../../api/catalog-resource.md#catalog-item-object-in-a-page) s `commitTimeStamp` menší než nebo rovna hodnotě aktuální kurzor.

Poté, co jste si stáhli všechny stránky katalogu není odfiltrovat, máte také sadu objektů typu list katalogu představující balíčky, které byly publikované, neuvedené, seznamu nebo odstraněných v době mezi vaší kurzoru časové razítko a teď.

## <a name="process-catalog-leaves"></a>Opustí proces katalogu

V tomto okamžiku můžete provést všechny vlastní zpracování, které si přejete na položky katalogu. Pokud potřebujete ID a verzi balíčku, si můžete prohlédnout `nuget:id` a `nuget:version` položky objekty najít na stránkách vlastností v katalogu. Zajistěte, aby se podívat na `@type` vlastnost vědět, pokud položka katalogu, kterou se vztahuje na existující balíček nebo odstraněné balíčku.

Pokud vás zajímá metadata o balíčku (například na popis, závislostí, velikost .nupkg atd), může načíst [katalogu listu dokumentu](../../api/catalog-resource.md#catalog-leaf) pomocí `@id` vlastnost.

    GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

Tento dokument obsahuje všechny metadat, které jsou součástí [balíček prostředek metadat](../../api/registration-base-url-resource.md)a další!

Tento krok je, kde můžete implementovat vlastní logiky. Další kroky v této příručce jsou implementované v pretty podobné způsobem není důležité, co dělají s listy katalogu.

### <a name="downloading-the-nupkg"></a>Stahování .nupkg

Pokud vás zajímá stahování pro balíčky .nupkg v katalogu nalezen, můžete použít [zdrojového obsahu balíčku](../../api/package-base-address-resource.md). Upozorňujeme však, že se prodleva mezi při je v katalogu nalezen balíček a pokud je k dispozici v zdrojového obsahu balíčku. Proto pokud dojde k `404 Not Found` při pokusu o stažení .nupkg pro balíček, který jste získali v katalogu, jednoduše znovu po krátkou dobu později. Oprava Tato prodleva sledován problém Githubu [NuGet/NuGetGallery #3455](https://github.com/NuGet/NuGetGallery/issues/3455).

## <a name="move-the-cursor-forward"></a>Přesunutí kurzoru předat dál

Jakmile byl úspěšně zpracován položky katalogu, je nutné určit nová hodnota kurzoru uložit. K tomuto účelu najít maximální (nejnovější časovém pořadí) `commitTimeStamp` položek katalogu, které je zpracovat. Toto je vaše nová hodnota kurzoru. Uložte na některé trvalého úložiště, jako jsou databáze, systém souborů nebo úložiště objektů blob. Pokud chcete získat další položky katalogu, jednoduše spustíte z [první krok](#initialize-a-cursor) podle inicializace kurzoru hodnota z této trvalého úložiště.

Pokud vaše aplikace vyvolá výjimku nebo chyb, nemusíte přesuňte se ukazatelem dál. Postoupíte kurzor má význam, které nikdy znovu potřebujete ke zpracování položky katalogu před kurzor.

Pokud z nějakého důvodu, máte opustí chyby v tom, jak zpracovat katalogu, můžete jednoduše přesuňte kurzor zpětné v čase a povolit kódu opětovné zpracování staré položky katalogu.

## <a name="c-sample-code"></a>Ukázkový kód C#

Protože katalogu je sada dokumentů JSON, které jsou k dispozici prostřednictvím protokolu HTTP, může být zpracoval s použitím žádný programovací jazyk, který má klienta HTTP a deserializátor JSON.

Jsou k dispozici v C# – ukázky [úložiště NuGet/Samples](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).

```cli
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a>Katalogu SDK

Nejjednodušší způsob, jak využívat katalogu je použití balíčku SDK Předběžná verze rozhraní .NET katalogu: [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog). Tento balíček je k dispozici na `nuget-build` MyGet kanálu, pro které použijete adresu URL zdroje balíčku NuGet `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`.

Instalaci tohoto balíčku do projektu kompatibilní s `netstandard1.3` nebo větší (například rozhraní .NET Framework 4.6).

Ukázka použití tento balíček je dostupná na Githubu v [NuGet.Protocol.Catalog.Sample projektu](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).

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

### <a name="minimal-sample"></a>Minimální ukázka

Příklad s méně závislosti který znázorňuje interakci s katalogem podrobněji, naleznete v části [CatalogReaderExample ukázkový projekt](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample). Cíle projektu `netcoreapp2.0` a závisí na [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (pro řešení služby index) a [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (pro deserializaci JSON).

Hlavní logika kódu se zobrazí na [souboru Program.cs](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).

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
