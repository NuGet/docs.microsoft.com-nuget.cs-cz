---
title: Cílové architektury referenční dokumentace pro NuGet
description: Odkazy na rozhraní target NuGet identifikovat a izolovat závisí na architektuře součásti balíčku.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/11/2017
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: c9267945b8055b536cf35911c36a066981ef67b6
ms.sourcegitcommit: c643dd2c44e085601551ff7079d696bcc3ad2b49
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/21/2018
ms.locfileid: "42793556"
---
# <a name="target-frameworks"></a>Cílové architektury

NuGet používá odkazy na cílové rozhraní v různých místech konkrétně identifikovat a izolovat komponenty závisí na architektuře balíčku:

- [manifest souboru .nuspec](../reference/nuspec.md): balíček můžete určit různé balíčky, které mají být zahrnuty v projektu v závislosti na cílové rozhraní projektu.
- [název složky .nupkg](../create-packages/creating-a-package.md#from-a-convention-based-working-directory): složky uvnitř balíčku `lib` složka může mít název podle cílové rozhraní, z nichž každý obsahuje knihovny DLL a další obsah, který je vhodný pro dané rozhraní.
- [soubor Packages.config](../reference/packages-config.md): `targetframework` atribut závislosti určuje variantu balíček pro instalaci.

> [!Note]
> NuGet zdrojový kód klienta, který vypočítá níže uvedených tabulkách se nachází v následujících umístěních:
> - Nepodporuje názvy framework: [FrameworkConstants.cs](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Frameworks/FrameworkConstants.cs)
> - Priorita rozhraní Framework a mapování: [DefaultFrameworkMappings.cs](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Frameworks/DefaultFrameworkMappings.cs)

## <a name="supported-frameworks"></a>Podporované architektury

Architektura je obvykle odkazuje na moniker krátký cílového rozhraní nebo TFM. V .NET Standard to je taky je zobecněný k *TxM* umožňující jeden odkaz na více platforem.

Klienti NuGet podporují rozhraní v následující tabulce. Ekvivalenty jsou uvedeny v hranatých závorkách []. Všimněte si, že některé nástroje, jako například `dotnet`, může být v některé soubory používají variace procesu canonical Tfm. Například `dotnet pack` používá `.NETCoreApp2.0` v `.nuspec` souboru spíše než `netcoreapp2.0`. Různé klientské nástroje Nugetu správně zpracovat tyto varianty, ale vždy používejte canonical Tfm při úpravách souborů přímo.

| Název | Zkratka | Tfm/TxMs |
| ------------- | ------------ | --------- |
|.NET Framework | NET | net11 |
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
|Microsoft Store (Windows Store) | netcore | netcore [netcore45] |
| | | netcore45 [vyhrajte, win8] |
| | | netcore451 [win81] |
| | | netcore50 |
|.NET MicroFramework | netmf | netmf |
|Windows | Windows | Windows [win8, netcore45] |
| | | win8 [netcore45, vyhrajte] |
| | | win81 [netcore451] |
| | | win10 (není podporováno platformou Windows 10) |
Silverlight | SL | sl4 |
| | | sl5 |
Windows Phone (SL) | webové části | wp [wp7] |
| | | wp7 |
| | | wp75 |
| | | wp8 |
| | | wp81 |
Windows Phone (UPW) | | wpa81 |
Univerzální platforma pro Windows | uap | uap [uap10.0] |
| | | uap10.0 |
.NET standard | netstandard | netstandard1.0 |
| | | netstandard1.1 |
| | | netstandard1.2 |
| | | netstandard1.3 |
| | | netstandard1.4 |
| | | netstandard1.5 |
| | | netstandard1.6 |
| | | netstandard2.0 |
Aplikace .NET core | netcoreapp | netcoreapp1.0 |
| | | netcoreapp1.1 |
| | | netcoreapp2.0 |
| | | netcoreapp2.1 |
Tizen | Tizen | tizen3 |
| | | tizen4 |

## <a name="deprecated-frameworks"></a>Zastaralá rozhraní

Následující architektury jsou zastaralé. Balíčky, které cílí na tyto architektury byste migrovat na uvedené nahrazení.

| Zastaralá architektura | Nahrazení
| --- | ---
| aspnet50 | netcoreapp |
| aspnetcore50 |
| dnxcore50 |
| dnx |
| dnx45 |
| dnx451 |
| dnx452 |
| DotNet | netstandard |
| dotnet50 | |
| dotnet51 | |
| dotnet52 | |
| dotnet53 | |
| dotnet54 | |
| dotnet55 | |
| dotnet56 | |
| winrt | Windows |

## <a name="precedence"></a>Priorita

Počet rozhraní jsou související s a kompatibilní mezi sebou, ale není nutně ekvivalentní:

| Rozhraní .NET Framework | Můžete použít |
| -- | --- |
| uap (Universal Windows Platform) | win81 |
| | wpa81 |
| | netcore50 |
| Vyhrajte (Microsoft Store) | winrt |
| | |

## <a name="net-platform-standard"></a>Platforma NET Standard

[Standard platformy .NET](https://github.com/dotnet/corefx/blob/master/Documentation/architecture/net-platform-standard.md) zjednodušuje odkazy mezi binárně kompatibilní rozhraní, což rámec jediný cíl, který odkazují jiné kombinace. (Na pozadí, najdete v článku [Úvod do .NET](/dotnet/articles/standard/index).)

[NuGet získáte nejbližší nástroje Framework](https://aka.ms/s2m3th) simuluje NuGet používá k výběru jedno rozhraní z mnoha dostupných rozhraní prostředků v balíček založený na rozhraní .NET framework projektu.

`dotnet` Řadu monikery by měla sloužit NuGet 3.3 a dříve; `netstandard` moniker syntaxe by měla sloužit verzi 3.4 a vyšší.

## <a name="portable-class-libraries"></a>Přenosné knihovny tříd

> [!Warning]
> **Nedoporučujeme používat PCLs**. I když jsou podporovaná PCLs, autory balíčku by měl podporovat netstandard místo. Na Standard platformy .NET jsou výsledkem vývoje PCLs a představuje binární přenositelnost napříč platformami využijte jeden moniker, které se vázalo na statickou knihovnu jako *portable-a + b + c* monikery.

Chcete-li definovat cílovou architekturu, která odkazuje na více podřízených cílových – rozhraní `portable` použití klíčového slova používat jako předpona seznam odkazovaných rozhraní. Vyhněte se uměle další rozhraní, které nejsou přímo zkompilovali, protože by mohlo způsobit nežádoucí vedlejší účinky v těchto rozhraní.

Další architektury definované třetími stranami zajištění kompatibility se další prostředí, které jsou k dispozici tímto způsobem. Kromě toho existuje Zkrácený tvar vlastností profilu čísla, která jsou k dispozici tyto kombinace související rozhraní uvedená ve formě odkazovat `Profile#`, ale nejedná se nedoporučuje používat tato čísla podle snižuje čitelnost složek a `.nuspec`.

| Profil # | Rozhraní | Jméno a příjmení | .NET standard |
 --- | --- | --- | ---
 Profile2 | . NETFramework 4.0 | portable-net40+win8+sl4+wp7 |
 | | Windows 8.0 | |
 | | Silverlight 4.0 |
 | | WindowsPhone 7.0|
 Profile3 | . NETFramework 4.0 | Přenosná net40 + sl4
 | | Silverlight 4.0 |
 Profile4 | . NETFramework 4.5 | portable-net45+sl4+win8+wp7
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.0 |
 Profile5 | . NETFramework 4.0 | Přenosná net40 + win8
 | | Windows 8.0 |
 Profile6 | .NETFramework 4.0.3 | Přenosná net403 + win8
 | | Windows 8.0 |
 Profile7 | . NETFramework 4.5 | Portable-net45 + win8 | netstandard1.1
 | | Windows 8.0 |
 Profile14 | . NETFramework 4.0 | Přenosná net40 + sl5
 | | Silverlight 5.0 |
 Profile18 | .NETFramework 4.0.3 | portable-net403+sl4
 | | Silverlight 4.0 |
 Profile19 | .NETFramework 4.0.3 | portable-net403+sl5
 | | Silverlight 5.0 |
 Profile23 | . NETFramework 4.5 | Portable-net45 + sl4
 | | Silverlight 4.0 |
 Profile24 | . NETFramework 4.5 | portable-net45+sl5
 | | Silverlight 5.0 |
 Profile31 | Windows 8.1 | Přenosná win81 + wp81 | netstandard1.0
 | | WindowsPhone 8.1 (SL) |
 Profile32 | Windows 8.1 | Přenosná win81 + wpa81 | netstandard1.2
 | | WindowsPhone 8.1 (UPW) |
 Profile36 | . NETFramework 4.0 | portable-net40+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile37 | . NETFramework 4.0 | Přenosná net40 sl5 + win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile41 | .NETFramework 4.0.3 | portable-net403+sl4+win8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 Profile42 | .NETFramework 4.0.3 | portable-net403+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile44 | . NETFramework 4.5.1 | Přenosná net451 + win81 | netstandard1.2
 | | Windows 8.1 |
 Profile46 | . NETFramework 4.5 | portable-net45+sl4+win8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 Profile47 | . NETFramework 4.5 | sl5 Portable-net45 + win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile49 | . NETFramework 4.5 | Portable-net45 + wp8 | netstandard1.0
 | | WindowsPhone 8.0 (SL) |
 Profile78 | . NETFramework 4.5 | Portable-net45 + win8 wp8 | netstandard1.0
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile84 | WindowsPhone 8.1 | Přenosná wp81 + wpa81 | netstandard1.0
 | | WindowsPhone 8.1 (UPW) |
 Profile88 | . NETFramework 4.0 | portable-net40+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile92 | . NETFramework 4.0 | Přenosná net40 + win8 wpa81
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UPW) |
 Profile95 | .NETFramework 4.0.3 | portable-net403+sl4+win8+wp7
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.0 |
 Profile96 | .NETFramework 4.0.3 | portable-net403+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile102 | .NETFramework 4.0.3 | portable-net403+win8+wpa81
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UPW) |
 Profile104 | . NETFramework 4.5 | portable-net45+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile111 | . NETFramework 4.5 | Portable-net45 + win8 wpa81 | netstandard1.1
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UPW) |
 Profile136 | . NETFramework 4.0 | Přenosná net40 sl5 + win8 + wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile143 | .NETFramework 4.0.3 | portable-net403+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile147 | .NETFramework 4.0.3 | portable-net403+sl5+win8+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile151 | NETFramework 4.5.1 | Přenosná net451 win81 + wpa81 | netstandard1.2
 | | Windows 8.1 |
 | | WindowsPhone 8.1 (UPW) |
 Profile154 | . NETFramework 4.5 | portable-net45+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile157 | Windows 8.1 | Přenosná win81 wp81 + wpa81 | netstandard1.0
 | | WindowsPhone 8.1 (SL) |
 | | WindowsPhone 8.1 (UPW) |
 Profile158 | . NETFramework 4.5 | portable-net45+sl5+win8+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile225 | . NETFramework 4.0 | Přenosná net40 sl5 + win8 + wpa81
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UPW) |
 Profile240 | .NETFramework 4.0.3 | portable-net403+sl5+win8+wpa8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UPW) |
 Profile255 | . NETFramework 4.5 | portable-net45+sl5+win8+wpa81
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UPW) |
 Profile259 | . NETFramework 4.5 | Portable-net45 + win8 + wpa81 + wp8 | netstandard1.0
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UPW) |
 | | WindowsPhone 8.0 (SL) |
 Profile328 | . NETFramework 4.0 | portable-net40+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UPW) |
 | | WindowsPhone 8.0 (SL) |
 Profile336 | .NETFramework 4.0.3 | portable-net403+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UPW) |
 | | WindowsPhone 8.0 (SL) |
 Profile344 | . NETFramework 4.5 | portable-net45+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UPW) |
 | | WindowsPhone 8.0 (SL) |

Balíčky NuGet, které cílí na Xamarin kromě toho můžete použít další architektury definované Xamarin. Zobrazit [NuGet vytváření balíčků pro Xamarin](https://developer.xamarin.com/guides/cross-platform/advanced/nuget/).

| Název | Popis | .NET standard |
| --- | --- | ---
| monoandroid | Mono podporu operačního systému Android | netstandard1.4 |
| monotouch | Mono – podpora pro iOS | netstandard1.4 |
| monomac | Mono podpory pro OS x | netstandard1.4 |
| xamarinios | Podpora pro Xamarin pro iOS | netstandard1.4 |
| xamarinmac | Podporuje pro Xamarin pro Mac | netstandard1.4 |
| xamarinpsthree | Podpora pro Xamarin v Playstation 3 | netstandard1.4 |
| xamarinpsfour | Podpora pro Xamarin v Playstation 4 | netstandard1.4 |
| xamarinpsvita | Podpora pro Xamarin v PS Vita | netstandard1.4 |
| xamarinwatchos | Xamarin pro Watch OS | netstandard1.4 |
| xamarintvos | Xamarin pro TV OS | netstandard1.4 |
| xamarinxboxthreesixty | Xamarin pro XBox 360 | netstandard1.4 |
| xamarinxboxone | Xamarin pro XBox One | netstandard1.4 |

> [!Note]
> Stephen Cleary vytvořil nástroj, který obsahuje seznam podporovaných PCLs, které můžete najít na jeho příspěvku, [Framework profily v prostředí .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html).
