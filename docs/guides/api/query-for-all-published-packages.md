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
# <a name="query-for-all-packages-published-to-nugetorg"></a>Dotaz pro všechny balíčky, které jsou publikovány na nuget.org

Jeden běžný vzor dotazu na starší verze OData V2 API se výčet všech balíčků, které jsou publikovány na nuget.org, seřazené podle při publikování balíčku. Scénáře, které vyžadují tento druh dotazu na nuget.org se velmi liší:

- Zcela replikaci nuget.org
- Zjištění, kdy balíčky obsahují nové vydané verze
- Hledání balíčky, které závisí na balíčku

Starším způsobem udělat to obvykle závisí na balíčku entity OData řazení podle časového razítka a stránkování ve výsledku obrovské sady s použitím `skip` a `top` parametry (velikost stránky). Bohužel tento přístup má určité nevýhody:

- Možnost chybějící balíčky, protože se provádějí dotazy na data, která se často mění pořadí
- Dlouhá doba odezvy dotazů, protože nejsou optimalizované dotazy (nejvíce optimalizované dotazy jsou ty, které podporují hlavní scénáře pro oficiální klienta NuGet)
- Není zaručeno, že použití zastaralé a nedokumentované rozhraní API, to znamená podpora takové dotazy v budoucnu
- Neschopnost přehrát historie v uvedeném pořadí, ukázalo

Z tohoto důvodu platí následující pokyny k řešení výše uvedených scénářů spolehlivější a budoucnosti způsobem.

## <a name="overview"></a>Přehled

Uprostřed tohoto průvodce je prostředek [NuGet rozhraní API](../../api/overview.md) volána **katalogu**. Katalog je rozhraní API nabízí jen možnost připojovat, které umožňuje volajícímu zobrazit úplnou historii balíčky se přidaly, upravit a odstranit z webu nuget.org. Pokud vás zajímají všechny nebo dokonce podmnožinu balíčky, které jsou publikovány na nuget.org, katalog je skvělý způsob, jak udržovat aktuální stav pomocí sadu aktuálně k dispozici balíčky odehrává.

Tato příručka je určená podrobný návod, jak, ale pokud vás zajímají podrobnější informace katalogu, přečtěte si téma jeho [API referenční dokument](../../api/catalog-resource.md).

Následující kroky je možné implementovat v libovolném programovacím jazyce podle vašeho výběru. Pokud chcete úplnou ukázku spuštěné, podívejte se na [ukázka v jazyce C#](#c-sample-code) uvedených níže.

Jinak postupujte podle níže průvodce k vytvoření čtečky spolehlivé katalogu.

## <a name="initialize-a-cursor"></a>Inicializovat kurzoru

Prvním krokem při sestavování spolehlivých katalogu čtečky implementuje kurzoru. Úplné podrobnosti o návrhu kurzoru katalogu, najdete v článku [katalogu referenční dokument](../../api/catalog-resource.md#cursor). Stručně řečeno kurzor je bod v čase, které byly zpracovány události v katalogu. Publikuje události v balíčku představují katalogu a změní jiný balíček. Pokud vás zajímají všechny balíčky publikovanou NuGet (od počátku času), by se inicializovat kurzor do časového razítka "minimální hodnota" (například `DateTime.MinValue` v rozhraní .NET). Pokud vám záleží jenom publikované balíčky teď spouští, použijete aktuální časové razítko jako hodnota počáteční kurzoru.

Pro tohoto průvodce budete inicializujeme naše kurzor do časového razítka jednu hodinu před. Teď stačí uložte tohoto časového razítka v paměti.

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a>Určit adresu URL katalogu indexu

Umístění všech prostředků (koncový bod) v rozhraní API NuGet by měly být zjištěny pomocí [index služby](../../api/service-index.md). Protože tento průvodce se zaměřuje na nuget.org, budeme používat index služby nuget.org.

    GET https://api.nuget.org/v3/index.json

Dokument služby je dokument JSON obsahující všechny prostředky na nuget.org. Vyhledejte prostředek s `@type` hodnotou vlastnosti `Catalog/3.0.0`. Přidružené `@id` hodnota vlastnosti je adresa URL samotného index katalogu. 

## <a name="find-new-catalog-leaves"></a>Najít nové ponechá katalogu

Použití `@id` vlastnost hodnotu nalezenou v předchozím kroku, stáhněte si index katalogu:

    GET https://api.nuget.org/v3/catalog0/index.json

Deserializaci [index katalogu](../../api/catalog-resource.md#catalog-index). Filtrování všeho [stránky objektů katalogu](../../api/catalog-resource.md#catalog-page-object-in-the-index) s `commitTimeStamp` menší nebo rovna hodnotě aktuální kurzor.

Pro každý zbývající stránky katalogu stáhnout pomocí celého dokumentu `@id` vlastnost.

    GET https://api.nuget.org/v3/catalog0/page2926.json

Deserializaci [stránky Katalog](../../api/catalog-resource.md#catalog-page). Filtrování všeho [katalogu listové objekty](../../api/catalog-resource.md#catalog-item-object-in-a-page) s `commitTimeStamp` menší nebo rovna hodnotě aktuální kurzor.

Po stažení všechny stránky katalogu není odfiltrovat, máte sadu katalogu objekty typu list představují balíčky, které byly publikované, neuvedené v seznamu, uvedené nebo odstraněné v době mezi vaše časové razítko kurzoru a nyní.

## <a name="process-catalog-leaves"></a>Opustí proces katalogu

V tomto okamžiku můžete provést vlastní zpracování, které chcete na položky katalogu. Pokud je všechno, co potřebujete ID a verzi balíčku, si můžete prohlédnout `nuget:id` a `nuget:version` položky objekty nalezené na stránkách vlastností v katalogu. Ujistěte se, že se podívat `@type` vlastnost vědět, pokud položka katalogu se týká existující balíček nebo odstranil balíček.

Pokud vás zajímají metadata o balíčku (například na popis, závislosti, velikost .nupkg atd), můžete načíst [katalogu listu dokumentu](../../api/catalog-resource.md#catalog-leaf) pomocí `@id` vlastnost.

    GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

Tento dokument obsahuje všechna metadata součástí [balíček metadata resource](../../api/registration-base-url-resource.md)a další!

Tento krok je, kde můžete implementovat vlastní logiku. Další kroky v této příručce jsou implementovány v pretty skoro stejné způsobem není důležité, co právě děláte s listy katalogu.

### <a name="downloading-the-nupkg"></a>Stahuje .nupkg

Pokud vás zajímá při stahování balíčků .nupkg v katalogu nalezen, můžete použít [balíček obsahu prostředku](../../api/package-base-address-resource.md). Mějte však na paměti, že je prodleva mezi při balíčku se nachází v katalogu a když je k dispozici v balíčku obsahu prostředku. Proto pokud narazíte na `404 Not Found` při pokusu o stažení .nupkg pro balíček, který jste našli v katalogu, jednoduše opakujte krátkého formátu času později. Oprava toto zpoždění je sledován pomocí funkce problém Githubu [NuGet/NuGetGallery #3455](https://github.com/NuGet/NuGetGallery/issues/3455).

## <a name="move-the-cursor-forward"></a>Přesunutí kurzoru vpřed

Po úspěšném zpracování položek katalogu, je nutné určit nová hodnota kurzor uložte. Chcete-li to provést, vyhledejte maximální (nejnovější chronologicky) `commitTimeStamp` všech položek katalogu, které můžete zpracovat. Toto je nová hodnota kurzoru. Uložte ho do nějaké trvalého úložiště, jako jsou databáze, systém souborů nebo úložiště objektů blob. Pokud chcete získat více položek katalogu, stačí spustit z [první krok](#initialize-a-cursor) podle inicializace kurzor hodnotu z této trvalého úložiště.

Pokud vaše aplikace vyvolá výjimku nebo chyby, Nepřesouvat kurzor vpřed. V budoucnu kurzor má význam, který nikdy znovu potřebujete ke zpracování položek katalogu před kurzor.

Pokud z nějakého důvodu máte chybu v o procesu katalogu opustí, stačí posunout kurzorem zpět v čase a umožňují váš kód za účelem opětovného zpracování staré položky katalogu.

## <a name="c-sample-code"></a>Vzorový kód jazyka C#

Protože katalogu je sada dokumentů JSON, které jsou k dispozici prostřednictvím protokolu HTTP, může být interakci s použitím libovolného programovacího jazyka, který má klienta HTTP a JSON deserializátor.

Jsou k dispozici v jazyce C# – ukázky [úložiště NuGet/Samples](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).

```cli
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a>Katalog SDK

Nejjednodušší způsob, jak využívat katalogu je použít balíček předběžné verze katalogu .NET SDK: [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog). Tento balíček je k dispozici na `nuget-build` MyGet informační kanál, pro který použijete adresu URL zdroje balíčku NuGet `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`.

Instalací tohoto balíčku do projektu, který je kompatibilní s `netstandard1.3` nebo větší (například rozhraní .NET Framework 4.6).

Pomocí tohoto balíčku ukázka je k dispozici na Githubu v [NuGet.Protocol.Catalog.Sample projektu](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).

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

Příklad s menším počtem závislosti, který znázorňuje interakci s katalogem podrobněji, najdete v článku [CatalogReaderExample ukázkový projekt](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample). Cíle projektu `netcoreapp2.0` a závisí [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (pro řešení index služby) a [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (pro deserializaci JSON).

Hlavní logika kód je viditelný [souboru Program.cs](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).

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
