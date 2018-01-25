---
title: "Cílové rozhraní odkazy pro NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/11/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "NuGet cílový framework odkazy identifikovat a izolovat framework závislé součásti balíčku."
keywords: "Balíček NuGet cílem, cíle rozhraní .NET framework, verze rozhraní .NET framework"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: c69ff6efca2dcc4a5c1242277f537012e9f4610f
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
---
# <a name="target-frameworks"></a>Cílové rozhraní

NuGet používá cílový framework odkazy v různých místech konkrétně identifikovat a izolovat framework závislé součásti balíčku:

- [manifest příponou .nuspec](../schema/nuspec.md): balíček může naznačovat jedinečné balíčky, které mají být zahrnuty v projektu v závislosti na cílový framework projektu na.
- [název složky .nupkg](../create-packages/creating-a-package.md#from-a-convention-based-working-directory): složky uvnitř balíček `lib` může mít název složky podle cílové rozhraní, z nichž každý obsahuje knihoven DLL a další obsah, které jsou vhodné pro dané platformy.
- [soubor Packages.config](../schema/packages-config.md): `targetframework` atribut závislost určuje variantu balíček pro instalaci.

> [!Note]
> Zdrojový kód klienta NuGet, který vypočítá následující tabulky se nachází v následujících umístěních:
> - Podporované názvy framework: [FrameworkConstants.cs](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Frameworks/FrameworkConstants.cs)
> - Framework přednost a mapování: [DefaultFrameworkMappings.cs](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Frameworks/DefaultFrameworkMappings.cs)

## <a name="supported-frameworks"></a>Podporované architektury

Rozhraní je obvykle odkazuje na krátké cílový framework přezdívka nebo TFM. V rozhraní .NET standardní Toto je také je zobecněny, aby *TxM* umožňující jeden odkaz na více rozhraní.

Klienti NuGet podporují rozhraní v následující tabulce. Ekvivalenty se zobrazí v závorkách []. Všimněte si, že některé nástroje, jako například `dotnet`, může použít variace kanonický TFMs v některé soubory. Například `dotnet pack` používá `.NETCoreApp2.0` v `.nuspec` souboru místo `netcoreapp2.0`. Různé nástroje klienta NuGet zpracování těchto variant správně, ale byste měli vždycky používat kanonický TFMs při úpravě soubory přímo.

| Název           | Zkratka | TFMs/TxMs |
| -------------  | ------------ | --------- |
|.NET Framework  | NET          | net11     |
|                |              | net20     |
|                |              | Net35     |
|                |              | net40     |
|                |              | net403    |
|                |              | net45      |
|                |              | net451     |
|                |              | net452     |
|                |              | net46      |
|                |              | net461     |
|                |              | net462     |
|Microsoft Storu (pro Windows Store) | netcore      | netcore [netcore45] |
|                |              | netcore45 [win, win8] |
|                |              | netcore451 [win81] |
|                |              | netcore50 |
|MicroFramework rozhraní .NET | netmf    | netmf |
|Windows         | Win          | win [win8, netcore45] |
| | | win8 [netcore45, win] |
| | | win81 [netcore451] |
| | | win10 (nepodporuje platformu Windows 10) |
Silverlight | sl | sl4 |
| | | sl5 |
Windows Phone (SL) | wp | wp [wp7] |
| | | wp7 |
| | | wp75 |
| | | wp8 |
| | | wp81 |
Windows Phone (UWP) | | wpa81 |
Univerzální platforma pro Windows | uap | uap [uap10.0] |
| | | uap10.0 |
Standardní rozhraní .NET | monikerů netstandard | netstandard1.0 |
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
tizen | tizen | tizen3 |
| | | tizen4 |

## <a name="deprecated-frameworks"></a>Zastaralá rozhraní
Tyto architektury jsou zastaralé. Balíčky cílené na tyto architektury měli migrovat na uvedené nahrazení.

| Nepoužívané framework | Nahrazení
| --- | ---
| aspnet50 | netcoreapp |
| aspnetcore50 |
| dnxcore50 |
| dnx |
| dnx45 |
| dnx451 |
| dnx452 |
| dotnet | monikerů netstandard |
| dotnet50 | |
| dotnet51 | |
| dotnet52 | |
| dotnet53 | |
| dotnet54 | |
| dotnet55 | |
| dotnet56 | |
| winrt | Win |

## <a name="precedence"></a>Priorita

Je několik rozhraní související s a kompatibilní s sebou, ale není nutně ekvivalentní:

| Rozhraní .NET Framework | Můžete použít |
| --- | --- |
| uap (Universal Windows Platform) | win81 |
| | wpa81 |
| | netcore50 |
| Win (Microsoft Store) | winrt |
| | | winrt45 |

## <a name="net-platform-standard"></a>Standardní NET platformy

[Standard platformy .NET](https://github.com/dotnet/corefx/blob/master/Documentation/architecture/net-platform-standard.md) zjednodušuje odkazy mezi rozhraní kompatibilní s binární, povolení jedné cílové rozhraní tak, aby odkazovaly kombinaci jiných. (Pro informace viz [Úvod do rozhraní .NET](/dotnet/articles/standard/index).)

[NuGet získat nejbližší Framework nástroj](https://aka.ms/s2m3th) simuluje NuGet používá k výběru jedné framework z mnoha prostředky k dispozici framework v balíčku na rozhraní .NET framework projektu na základě.

`dotnet` Řadu zástupných názvů by měl používat v NuGet 3.3 a dříve; `netstandard` Přezdívka syntaxe by měla být použita v3.4 a novější.

## <a name="portable-class-libraries"></a>Knihovny přenosných tříd

> [!Warning]
> **Nedoporučuje se PCLs**. I když jsou podporované PCLs, balíček autoři by měly podporovat monikerů netstandard místo. Na Standard platformy .NET je PCLs a představuje binární přenositelnost napříč platformami pomocí jednoho přezdívka, který není vázaný na static, jako jsou třeba *přenosné-+ b + c* zástupných názvů.

K definování cílové rozhraní, které odkazuje na více podřízených target – rozhraní, `portable` – klíčové slovo použití používat jako předpona seznam odkazované architektury. Vyhněte se uměle navíc rozhraní, které nejsou přímo kompilovány proti protože může vést k neočekávaným vedlejší efekty při tyto architektury.

Další rozhraní definované třetím stranám zajišťují kompatibilitu s další prostředí, které jsou dostupné tímto způsobem. Kromě toho existují sdružená profil čísla, které jsou k dispozici, chcete-li tyto kombinace související rozhraní jako `Profile#`, ale toto není doporučený postup pro tato čísla použít, protože snižuje čitelnost složek a `.nuspec`.

| Profil # | rozhraní | Úplný název | Standardní rozhraní .NET |
 --- | --- | --- | ---
 Profile2 | .NETFramework 4.0 | portable-net40+win8+sl4+wp7 |
 | | Windows 8.0 | |
 | | Silverlight 4.0 |
 | | WindowsPhone 7.0|
 Profile3 | .NETFramework 4.0 | portable-net40+sl4
 | | Silverlight 4.0 |
 Profile4 | .NETFramework 4.5 | portable-net45+sl4+win8+wp7
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.0 |
 Profile5 | .NETFramework 4.0 | portable-net40+win8
 | | Windows 8.0 |
 Profile6 | .NETFramework 4.0.3 | portable-net403+win8
 | | Windows 8.0 |
 Profile7 | .NETFramework 4.5 | přenositelností net45 + win8 | netstandard1.1
 | | Windows 8.0 |
 Profile14 | .NETFramework 4.0 | portable-net40+sl5
 | | Silverlight 5.0 |
 Profile18 | .NETFramework 4.0.3 | portable-net403+sl4
 | | Silverlight 4.0 |
 Profile19 | .NETFramework 4.0.3 | portable-net403+sl5
 | | Silverlight 5.0 |
 Profile23 | .NETFramework 4.5 | portable-net45+sl4
 | | Silverlight 4.0 |
 Profile24 | .NETFramework 4.5 | portable-net45+sl5
 | | Silverlight 5.0 |
 Profile31 | Windows 8.1 | portable-win81+wp81 | netstandard1.0
 | | WindowsPhone 8.1 (SL) |
 Profile32 | Windows 8.1 | portable-win81+wpa81 | netstandard1.2
 | | WindowsPhone 8.1 (UWP) |
 Profile36 | .NETFramework 4.0 | portable-net40+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile37 | .NETFramework 4.0 | portable-net40+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile41 | .NETFramework 4.0.3 | portable-net403+sl4+win8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 Profile42 | .NETFramework 4.0.3 | portable-net403+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile44 | .NETFramework 4.5.1 | portable-net451+win81 | netstandard1.2
 | | Windows 8.1 |
 Profile46 | .NETFramework 4.5 | portable-net45+sl4+win8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 Profile47 | .NETFramework 4.5 | portable-net45+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile49 | .NETFramework 4.5 | portable-net45+wp8 | netstandard1.0
 | | WindowsPhone 8.0 (SL) |
 Profile78 | .NETFramework 4.5 | portable-net45+win8+wp8 | netstandard1.0
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile84 | WindowsPhone 8.1 | portable-wp81+wpa81 | netstandard1.0
 | | WindowsPhone 8.1 (UWP) |
 Profile88 | .NETFramework 4.0 | portable-net40+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile92 | .NETFramework 4.0 | portable-net40+win8+wpa81
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
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
 | | WindowsPhone 8.1 (UWP) |
 Profile104 | .NETFramework 4.5 | portable-net45+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile111 | .NETFramework 4.5 | portable-net45+win8+wpa81 | netstandard1.1
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile136 | .NETFramework 4.0 | portable-net40+sl5+win8+wp8
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
 Profile151 | NETFramework 4.5.1 | portable-net451+win81+wpa81 | netstandard1.2
 | | Windows 8.1 |
 | | WindowsPhone 8.1 (UWP) |
 Profile154 | .NETFramework 4.5 | portable-net45+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile157 | Windows 8.1 | portable-win81+wp81+wpa81 | netstandard1.0
 | | WindowsPhone 8.1 (SL) |
 | | WindowsPhone 8.1 (UWP) |
 Profile158 | .NETFramework 4.5 | portable-net45+sl5+win8+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile225 | .NETFramework 4.0 | portable-net40+sl5+win8+wpa81
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile240 | .NETFramework 4.0.3 | portable-net403+sl5+win8+wpa8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile255 | .NETFramework 4.5 | portable-net45+sl5+win8+wpa81
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile259 | .NETFramework 4.5 | portable-net45+win8+wpa81+wp8 | netstandard1.0
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |
 Profile328 | .NETFramework 4.0 | portable-net40+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |
 Profile336 | .NETFramework 4.0.3 | portable-net403+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |
 Profile344 | .NETFramework 4.5 | portable-net45+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |

Balíčky NuGet cílení Xamarin můžou navíc použít další rozhraní definované Xamarin. V tématu [balíčky NuGet vytváření pro Xamarin](https://developer.xamarin.com/guides/cross-platform/advanced/nuget/).

| Název | Popis | Standardní rozhraní .NET |
| --- | --- | ---
| monoandroid | Monofonní podporu pro operační systém Android | netstandard1.4 |
| monotouch | Monofonní podpora pro iOS | netstandard1.4 |
| monomac | Monofonní podpora OSX | netstandard1.4 |
| xamarinios | Podpora pro Xamarin pro iOS | netstandard1.4 |
| xamarinmac | Podporuje pro Xamarin pro Mac | netstandard1.4 |
| xamarinpsthree | Podpora pro Xamarin na Playstation 3 | netstandard1.4 |
| xamarinpsfour | Podpora pro Xamarin na Playstation 4 | netstandard1.4 |
| xamarinpsvita | Podpora pro Xamarin na PS Vita | netstandard1.4 |
| xamarinwatchos | Xamarin pro sledování operačního systému | netstandard1.4 |
| xamarintvos | Xamarin pro TV operačního systému | netstandard1.4 |
| xamarinxboxthreesixty | Xamarin pro XBox 360 | netstandard1.4 |
| xamarinxboxone | Xamarin pro XBox jeden | netstandard1.4 |

> [!Note]
> Stephen Cleary vytvořil nástroj, který obsahuje seznam podporovaných PCLs, které můžete najít na jeho post, [Framework profily v rozhraní .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html).
