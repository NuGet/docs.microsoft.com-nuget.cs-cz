---
title: Referenční dokumentace cílových rozhraní pro NuGet
description: Rozhraní NuGet pro cílovou architekturu odkazuje na identifikaci a izolaci komponent balíčku závislých na rozhraní.
author: JonDouglas
ms.author: jodou
ms.date: 12/11/2017
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 7671b50b84bf1447fe94e02896786d1f309425dd
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777316"
---
# <a name="target-frameworks"></a>Cílové architektury

NuGet používá cílové rozhraní odkazy na celou řadu míst pro specifickou identifikaci a izolaci komponent balíčku závislých na rozhraní:

- [soubor projektu](../create-packages/multiple-target-frameworks-project-file.md): pro projekty ve stylu sady SDK obsahuje soubor *. csproj* odkazy na cílové rozhraní .NET Framework.
- [. nuspec manifest](../reference/nuspec.md): balíček může označovat samostatné balíčky, které se mají zahrnout do projektu v závislosti na cílové platformě projektu.
- [. nupkg název složky](../create-packages/creating-a-package.md#from-a-convention-based-working-directory): složky uvnitř `lib` složky balíčku mohou být pojmenovány podle cílové architektury, z nichž každá obsahuje knihovny DLL a další obsah odpovídající danému rozhraní.
- [packages.config](../reference/packages-config.md): `targetframework` atribut závislosti určuje variantu balíčku, který se má nainstalovat.

> [!Note]
> Zdrojový kód klienta NuGet, který počítá tabulky uvedené níže, najdete v následujících umístěních:
> - Podporované názvy rozhraní: [FrameworkConstants.cs](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Frameworks/FrameworkConstants.cs)
> - Priorita architektury a mapování: [DefaultFrameworkMappings.cs](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Frameworks/DefaultFrameworkMappings.cs)

## <a name="supported-frameworks"></a>Podporované architektury

Rozhraní je obvykle odkazováno krátkým monikerem cílového rozhraní Framework nebo TFM. V .NET Standard to je také generalizované na *TxM* , aby bylo možné použít jediný odkaz na více rozhraní.

Klienti NuGet podporují rozhraní v následující tabulce. Ekvivalenty jsou uvedeny v závorkách []. Všimněte si, že některé nástroje, například `dotnet` , mohou v některých souborech používat variace kanonické TFM. Například `dotnet pack` používá  `.NETCoreApp2.0` v `.nuspec` souboru místo `netcoreapp2.0` . Různé nástroje klienta NuGet tyto variace zpracovávají správně, ale při přímém upravování souborů byste měli vždycky používat kanonickou TFM.

| Name | Zkratka | TFM/TxMs |
| ------------- | ------------ | --------- |
|.NET Framework | net | net11 |
| | | net20 |
| | | net35 |
| | | net40 |
| | | net403 |
| | | net45 |
| | | net451 |
| | | net452 |
| | | net46 |
| | | net461 |
| | | net462 |
| | | net47 |
| | | net471 |
| | | net472 |
| | | net48 |
|Microsoft Store (Windows Store) | Netcore | Netcore [netcore45] |
| | | netcore45 [Win, Win8] |
| | | netcore451 [win81] |
| | | netcore50 |
|Architektura .NET – mikrorozhraní | netmf | netmf |
|Windows | výher | Win [Win8, netcore45] |
| | | Win8 [netcore45, Win] |
| | | win81 [netcore451] |
| | | Win10 (platforma Windows 10 nepodporuje) |
Silverlight | SSL | sl4 |
| | | sl5 |
Windows Phone (SL) | požadavku | WP [WP7] |
| | | wp7 |
| | | wp75 |
| | | WP8 |
| | | wp81 |
Windows Phone (UWP) | | wpa81 |
Univerzální platforma Windows | UAP | UAP [UAP 10.0] |
| | | UAP 10.0 |
| | | UAP 10.0. xxxxx (kde 10.0. xxxxx je minimální verze aplikace náročné na cílovou platformu) |
.NET Standard | netstandard | netstandard 1.0 |
| | | netstandard 1.1 |
| | | netstandard 1.2 |
| | | netstandard 1.3 |
| | | netstandard 1.4 |
| | | netstandard 1.5 |
| | | netstandard 1.6 |
| | | netstandard 2.0 |
| | | netstandard 2.1 |
Aplikace .NET Core | netcoreapp | netcoreapp 1.0 |
| | | netcoreapp 1.1 |
| | | netcoreapp2.0 |
| | | netcoreapp 2.1 |
| | | netcoreapp 2.2 |
| | | netcoreapp 3.0 |
| | | netcoreapp 3.1 |
Tizen | tizen | tizen3 |
| | | tizen4 |

## <a name="deprecated-frameworks"></a>Zastaralá rozhraní

Následující rozhraní jsou zastaralá. Balíčky, které cílí na tyto architektury, by se měly migrovat na zmíněné náhrady.

| Zastaralé rozhraní | Náhrada
| --- | ---
| aspnet50 | netcoreapp |
| aspnetcore50 |
| dnxcore50 |
| DNX |
| dnx45 |
| dnx451 |
| dnx452 |
| dotnet | netstandard |
| dotnet50 | |
| dotnet51 | |
| dotnet52 | |
| dotnet53 | |
| dotnet54 | |
| dotnet55 | |
| dotnet56 | |
| WinRT | výher |

## <a name="precedence"></a>Priorita

Řada architektur souvisí s a je kompatibilní s jednou, ale ne nutně rovnocenná:

| Rozhraní .NET Framework | Dá se použít |
| -- | --- |
| UAP (Univerzální platforma Windows) | win81 |
| | wpa81 |
| | netcore50 |
| Win (Microsoft Store) | WinRT |
| | |

## <a name="net-standard"></a>NET Standard

[.NET Standard](/dotnet/standard/net-standard) zjednodušuje odkazy mezi binárními kompatibilními rozhraními, což umožňuje, aby jedna cílová architektura odkazovala na kombinaci dalších. (Pro pozadí si přečtěte část [Úvod do .NET](/dotnet/articles/standard/index).)

[Nástroj NuGet získat nejbližší rozhraní](https://aka.ms/s2m3th) simuluje, co nástroj NuGet používá k výběru jedné architektury z mnoha dostupných prostředků rozhraní v balíčku v závislosti na architektuře projektu.

`dotnet`Řada monikerů by měla být použita v NuGet 3,3 a starších verzích. `netstandard` syntaxe monikeru by měla být použita v 3.4 a novějších verzích.

## <a name="portable-class-libraries"></a>Přenosné knihovny tříd

> [!Warning]
> **PCLS se nedoporučují**. I když je podpora PCLs podporovaná, autoři balíčků by měli místo toho podporovat netstandard. Standard platformy .NET je vývoj PCLs a představuje binární přenositelnost napříč platformami pomocí jednoho monikeru, který není svázán se statickou knihovnou jako přenosné monikery *a + b + c* .

Chcete-li definovat cílovou verzi rozhraní .NET Framework, která odkazuje na více podřízených rozhraní, `portable` klíčové slovo používá k vytvoření předpony seznamu odkazovaných rozhraní. Vyhněte se uměle včetně dalších rozhraní, která nejsou přímo zkompilována proti tomu, protože mohou vést k nežádoucím vedlejším účinkům v těchto rozhraních.

Další architektury definované třetími stranami poskytují kompatibilitu s jinými prostředími, která jsou tímto způsobem přístupná. Kromě toho existují zkrácená čísla profilů, která jsou k dispozici pro odkazování na tyto kombinace souvisejících platforem, jako je `Profile#` , ale toto není doporučený postup pro použití těchto čísel, protože snižuje čitelnost složek a `.nuspec` .

| Profilu # | Rozhraní | Jméno a příjmení | .NET Standard |
 --- | --- | --- | ---
 Profile2 | . NETFramework 4,0 | Přenosné – net40 + Win8 + sl4 + WP7 |
 | | Windows 8.0 | |
 | | Silverlight 4,0 |
 | | WindowsPhone 7,0|
 Profile3 | . NETFramework 4,0 | Přenosné – net40 + sl4
 | | Silverlight 4,0 |
 Profile4 | . NETFramework 4,5 | Přenosné – Net45 + sl4 + Win8 + WP7
 | | Silverlight 4,0 |
 | | Windows 8.0 |
 | | WindowsPhone 7,0 |
 Profile5 | . NETFramework 4,0 | Přenosné – net40 + Win8
 | | Windows 8.0 |
 Profile6 | . NETFramework 4.0.3 | Přenosné – net403 + Win8
 | | Windows 8.0 |
 Profile7 | . NETFramework 4,5 | Přenosné – Net45 + Win8 | netstandard 1.1
 | | Windows 8.0 |
 Profile14 | . NETFramework 4,0 | Přenosné – net40 + SL5
 | | Silverlight 5,0 |
 Profile18 | . NETFramework 4.0.3 | Přenosné – net403 + sl4
 | | Silverlight 4,0 |
 Profile19 | . NETFramework 4.0.3 | Přenosné – net403 + SL5
 | | Silverlight 5,0 |
 Profile23 | . NETFramework 4,5 | Přenosné – Net45 + sl4
 | | Silverlight 4,0 |
 Profile24 | . NETFramework 4,5 | Přenosné – Net45 + SL5
 | | Silverlight 5,0 |
 Profile31 | Windows 8.1 | Přenosné – win81 + wp81 | netstandard 1.0
 | | WindowsPhone 8,1 (SL) |
 Profile32 | Windows 8.1 | Přenosné – win81 + wpa81 | netstandard 1.2
 | | WindowsPhone 8,1 (UWP) |
 Profile36 | . NETFramework 4,0 | Přenosné – net40 + sl4 + Win8 + WP8
 | | Silverlight 4,0 |
 | | Windows 8.0 |
 | | WindowsPhone 8,0 (SL) |
 Profile37 | . NETFramework 4,0 | Přenosné – net40 + SL5 + Win8
 | | Silverlight 5,0 |
 | | Windows 8.0 |
 Profile41 | . NETFramework 4.0.3 | Přenosné – net403 + sl4 + Win8
 | | Silverlight 4,0 |
 | | Windows 8.0 |
 Profile42 | . NETFramework 4.0.3 | Přenosné – net403 + SL5 + Win8
 | | Silverlight 5,0 |
 | | Windows 8.0 |
 Profile44 | . NETFramework 4.5.1 | Přenosné – net451 + win81 | netstandard 1.2
 | | Windows 8.1 |
 Profile46 | . NETFramework 4,5 | Přenosné – Net45 + sl4 + Win8
 | | Silverlight 4,0 |
 | | Windows 8.0 |
 Profile47 | . NETFramework 4,5 | Přenosné – Net45 + SL5 + Win8
 | | Silverlight 5,0 |
 | | Windows 8.0 |
 Profile49 | . NETFramework 4,5 | Přenosné – Net45 + WP8 | netstandard 1.0
 | | WindowsPhone 8,0 (SL) |
 Profile78 | . NETFramework 4,5 | Přenosné – Net45 + Win8 + WP8 | netstandard 1.0
 | | Windows 8.0 |
 | | WindowsPhone 8,0 (SL) |
 Profile84 | WindowsPhone 8,1 | Přenosné – wp81 + wpa81 | netstandard 1.0
 | | WindowsPhone 8,1 (UWP) |
 Profile88 | . NETFramework 4,0 | Přenosné – net40 + sl4 + Win8 + wp75
 | | Silverlight 4,0 |
 | | Windows 8.0 |
 | | WindowsPhone 7,5 |
 Profile92 | . NETFramework 4,0 | Přenosné – net40 + Win8 + wpa81
 | | Windows 8.0 |
 | | WindowsPhone 8,1 (UWP) |
 Profile95 | . NETFramework 4.0.3 | Přenosné – net403 + sl4 + Win8 + WP7
 | | Silverlight 4,0 |
 | | Windows 8.0 |
 | | WindowsPhone 7,0 |
 Profile96 | . NETFramework 4.0.3 | Přenosné – net403 + sl4 + Win8 + wp75
 | | Silverlight 4,0 |
 | | Windows 8.0 |
 | | WindowsPhone 7,5 |
 Profile102 | . NETFramework 4.0.3 | Přenosné – net403 + Win8 + wpa81
 | | Windows 8.0 |
 | | WindowsPhone 8,1 (UWP) |
 Profile104 | . NETFramework 4,5 | Přenosné – Net45 + sl4 + Win8 + wp75
 | | Silverlight 4,0 |
 | | Windows 8.0 |
 | | WindowsPhone 7,5 |
 Profile111 | . NETFramework 4,5 | Přenosné – Net45 + Win8 + wpa81 | netstandard 1.1
 | | Windows 8.0 |
 | | WindowsPhone 8,1 (UWP) |
 Profile136 | . NETFramework 4,0 | Přenosné – net40 + SL5 + Win8 + WP8
 | | Silverlight 5,0 |
 | | Windows 8.0 |
 | | WindowsPhone 8,0 (SL) |
 Profile143 | . NETFramework 4.0.3 | Přenosné – net403 + sl4 + Win8 + WP8
 | | Silverlight 4,0 |
 | | Windows 8.0 |
 | | WindowsPhone 8,0 (SL) |
 Profile147 | . NETFramework 4.0.3 | Přenosné – net403 + SL5 + Win8 + WP8
 | | Silverlight 5,0 |
 | | Windows 8.0 |
 | | WindowsPhone 8,0 (SL) |
 Profile151 | NETFramework 4.5.1 | Přenosné – net451 + win81 + wpa81 | netstandard 1.2
 | | Windows 8.1 |
 | | WindowsPhone 8,1 (UWP) |
 Profile154 | . NETFramework 4,5 | Přenosné – Net45 + sl4 + Win8 + WP8
 | | Silverlight 4,0 |
 | | Windows 8.0 |
 | | WindowsPhone 8,0 (SL) |
 Profile157 | Windows 8.1 | Přenosné – win81 + wp81 + wpa81 | netstandard 1.0
 | | WindowsPhone 8,1 (SL) |
 | | WindowsPhone 8,1 (UWP) |
 Profile158 | . NETFramework 4,5 | Přenosné – Net45 + SL5 + Win8 + WP8
 | | Silverlight 5,0 |
 | | Windows 8.0 |
 | | WindowsPhone 8,0 (SL) |
 Profile225 | . NETFramework 4,0 | Přenosné – net40 + SL5 + Win8 + wpa81
 | | Silverlight 5,0 |
 | | Windows 8.0 |
 | | WindowsPhone 8,1 (UWP) |
 Profile240 | . NETFramework 4.0.3 | Přenosné – net403 + SL5 + Win8 + wpa8
 | | Silverlight 5,0 |
 | | Windows 8.0 |
 | | WindowsPhone 8,1 (UWP) |
 Profile255 | . NETFramework 4,5 | Přenosné – Net45 + SL5 + Win8 + wpa81
 | | Silverlight 5,0 |
 | | Windows 8.0 |
 | | WindowsPhone 8,1 (UWP) |
 Profile259 | . NETFramework 4,5 | Přenosné – Net45 + Win8 + wpa81 + WP8 | netstandard 1.0
 | | Windows 8.0 |
 | | WindowsPhone 8,1 (UWP) |
 | | WindowsPhone 8,0 (SL) |
 Profile328 | . NETFramework 4,0 | Přenosné – net40 + SL5 + Win8 + wpa81 + WP8
 | | Silverlight 5,0 |
 | | Windows 8.0 |
 | | WindowsPhone 8,1 (UWP) |
 | | WindowsPhone 8,0 (SL) |
 Profile336 | . NETFramework 4.0.3 | Přenosné – net403 + SL5 + Win8 + wpa81 + WP8
 | | Silverlight 5,0 |
 | | Windows 8.0 |
 | | WindowsPhone 8,1 (UWP) |
 | | WindowsPhone 8,0 (SL) |
 Profile344 | . NETFramework 4,5 | Přenosné – Net45 + SL5 + Win8 + wpa81 + WP8
 | | Silverlight 5,0 |
 | | Windows 8.0 |
 | | WindowsPhone 8,1 (UWP) |
 | | WindowsPhone 8,0 (SL) |

Balíčky NuGet cílené na Xamarin můžou navíc používat další architektury definované pro Xamarin. Viz [vytváření balíčků NuGet pro Xamarin](https://developer.xamarin.com/guides/cross-platform/advanced/nuget/).

| Název | Popis | .NET Standard |
| --- | --- | ---
| monoandroid | Podpora mono pro operační systém Android | netstandard 1.4 |
| MonoTouch | Podpora mono pro iOS | netstandard 1.4 |
| monomac | Podpora mono pro OSX | netstandard 1.4 |
| xamarinios | Podpora pro Xamarin pro iOS | netstandard 1.4 |
| xamarinmac | Podporuje se pro Xamarin for Mac. | netstandard 1.4 |
| xamarinpsthree | Podpora pro Xamarin na PlayStation 3 | netstandard 1.4 |
| xamarinpsfour | Podpora pro Xamarin na PlayStation 4 | netstandard 1.4 |
| xamarinpsvita | Podpora Xamarin na PS | netstandard 1.4 |
| xamarinwatchos | Xamarin for Watch – operační systém | netstandard 1.4 |
| xamarintvos | Xamarin pro TV OS | netstandard 1.4 |
| xamarinxboxthreesixty | Xamarin pro XBox 360 | netstandard 1.4 |
| xamarinxboxone | Xamarin pro XBox One | netstandard 1.4 |

> [!Note]
> Stephenal vytvořil nástroj, který obsahuje seznam podporovaných PCLs, které najdete v části [profily architektury rozhraní .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html).
