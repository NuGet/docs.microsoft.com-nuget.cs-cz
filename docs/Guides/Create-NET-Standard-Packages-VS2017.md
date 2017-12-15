---
title: "Vytvoření balíčků NuGet standardní 2.0 .NET s Visual Studio 2017 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 5/23/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 2c1de334-fdc9-4e1e-8ef6-a90b3e77ff0f
description: "Návod začátku do konce, vytváření balíčků NuGet pro standardní 2.0 rozhraní .NET pomocí nástroje NuGet 4.x a Visual Studio 2017."
keywords: "Vytvoření balíčku, .NET Standard balíčky .NET Core"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 82e413119b12503336becd6019e4fa3e4ac0b1f3
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="create-net-standard-20-packages-with-visual-studio-2017"></a>Vytvoření balíčků standardní rozhraní .NET 2.0 s Visual Studio 2017

*Platí pro NuGet 4.x+ a MSBuild 15.3 + v souladu s Visual Studio 2017 Update 3. U starších verzí Visual Studio 2017, tyto pokyny platí pro standardní 1.4 .NET 1.6 změnou \<TargetFramework\> vlastnost. Viz také [vytvořit .NET standardní balíčky s Visual Studiem 2015](../guides/create-net-standard-packages-vs2015.md) pro práci s NuGet 3.x+.*

[Standardní knihovny .NET](https://docs.microsoft.com/dotnet/articles/standard/library) je formální specifikaci rozhraní API technologie .NET by měla být k dispozici pro všechny moduly runtime rozhraní .NET, tím větší jednotnost vytváří v ekosystému .NET. Standardní knihovny .NET definuje jednotnou sadu BCL (základní třída knihovna) rozhraní API pro všechny platformy .NET implementovat, nezávisle na zatížení. Ji umožňuje vývojářům vytvářet PCLs, které jsou použitelné pro všechny moduly runtime rozhraní .NET, a snižuje, pokud není eliminuje direktivy specifické pro platformu Podmíněná kompilace v sdíleného kódu.

Tato příručka vás provede procesem vytvoření balíčku nuget cílení na rozhraní .NET standardní knihovny 2.0 s Visual Studio 2017 Update 3 a NuGet 4.0.

1. [Předpoklady](#pre-requisites)
1. [Vytvoření projektu knihovny tříd](#create-the-netstandard-class-library-project)
1. [Upravit metadata v souboru .csproj](#edit-metadata-in-the-csproj-file)
1. [Balíček součásti](#package-the-component)
1. [Související témata](#related-topics)

## <a name="pre-requisites"></a>Předpoklady

Tento postup vyžaduje Visual Studio 2017 Update 3 se **vývoj pro různé platformy .NET Core** zatížení. Edice Community můžete nainstalovat zdarma z [visualstudio.com](https://www.visualstudio.com/), nebo použijte edice Professional a Enterprise.

Vyžadují pracovního vytížení, zobrazí se následující v instalačním programu sady Visual Studio:

![Vývoj pro různé platformy zatížení .NET core v instalačním programu Visual Studio](media/NuGet4-01-Workload.png)

## <a name="create-the-net-standard-class-library-project"></a>Vytvořte standardní rozhraní .NET projektu knihovny tříd

1. V sadě Visual Studio **soubor > Nový > projekt**, rozbalte **Visual C# > .NET Standard** uzlu, vyberte **knihovny tříd (Net Standard)**, změňte název na AppLogger, a Klikněte na tlačítko OK.

    ![Vytvoření nového projektu knihovny tříd](media/NuGet4-02-NewProject.png)

1. Změnit konfiguraci sestavení na **verze**.
1. Klikněte pravým tlačítkem myši `AppLogger` projekt v Průzkumníku řešení, vyberte **vlastnosti**, vyberte **sestavení** kartě, zaškrtněte políčko pro **souborů dokumentace XML**a nastavte Název souboru k právě `AppLogger.xml`. Potom uložte projekt.

1. Přidat kód pro součásti, například následující (který jasně právě výstupy zpráv do konzoly):

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                Console.WriteLine(text);
            }
        }
    }
    ```

1. Sestavení projektu (s konfigurací verzi) a zkontrolujte, že jsou v rámci vytváří soubory DLL a XML `bin\Release\netstandard2.0` složky.

## <a name="edit-metadata-in-the-csproj-file"></a>Upravit metadata v souboru .csproj

S projekty NuGet 4.0 a .NET Core, metadata balíčků je obsažena přímo v `.csproj` souboru místo externích souborů, jako `.nuspec`. Úplný popis této metadat se nachází v [NuGet pack a obnovit jako cíle MSBuild](../schema/msbuild-targets.md#pack-target).

1. Klikněte pravým tlačítkem na projekt v Průzkumníku řešení, vyberte **upravit AppLogger.csproj**a pak upravte první skupinu vlastnost k přidání informací balíčku, například následující:

    ```xml
    <PropertyGroup>
        <TargetFramework>netstandard2.0</TargetFramework>
        <PackageId>AppLogger.YOUR_NAME</PackageId>
        <PackageVersion>1.0.0</PackageVersion>
        <Authors>YOUR_NAME</Authors>
        <Description>Awesome application logging utility</Description>
        <PackageRequireLicenseAcceptance>false</PackageRequireLicenseAcceptance>
        <PackageReleaseNotes>First release</PackageReleaseNotes>
        <Copyright>Copyright 2017 (c) Contoso Corporation. All rights reserved.</Copyright>
        <PackageTags>logger logging logs</PackageTags>
    </PropertyGroup>
    ```

1. Uložte projekt, pak pravým tlačítkem na řešení a vyberte **sestavit řešení** znovu vygenerovat všechny soubory pro balíček, tentokrát s metadaty správné.


## <a name="package-the-component"></a>Balíček součásti

NuGet 4.0 podporuje cíl pack pomocí nástroje MSBuild verze 15.1 + (včetně nástroje MSBuild 15.3 jako součást Visual Studio 2017 Update 3) Pokud projekt obsahuje metadata potřebný balíček, jak byl přidán v předchozí části. K vyvolání MSBuild tímto způsobem, jednoduše zadejte cíl pack na příkazovém řádku ve stejné složce jako `.csproj` souboru:

    msbuild /t:pack /p:Configuration=Release

Další možnosti s `msbuild /t:pack`, soubory obsahu, symboly, například včetně a zdrojový kód, najdete v části [NuGet pack a obnovit jako cíle MSBuild](../schema/msbuild-targets.md#pack-target).

V každém případě výše uvedeného příkazu generuje `AppLogger.YOUR_NAME.1.0.0.nupkg` v `bin\Release` složky ve výchozím nastavení, jako je sestavení pro tuto konfiguraci. V případě vynechání `/p` přepínače, bude výchozí konfigurace `Debug`. 

Otevření tohoto souboru v nástroje, jako [Explorer balíček NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) a rozšiřování všechny uzly, zobrazí se následující obsah:

![Průzkumník balíček NuGet zobrazující AppLogger balíčku](media/NuGet4-03-PackageExplorer.png)

> [!Tip]
> A `.nupkg` soubor je právě soubor ZIP s jiné rozšíření. Můžete také zkontrolovat obsah balíčku, potom změnou `.nupkg` k `.zip`, ale nezapomeňte obnovit rozšíření před balíčku se nahrávají na nuget.org.

Pokud chcete zpřístupnit vašeho balíčku jinými vývojáři, postupujte podle pokynů [publikování balíčku](../create-packages/publish-a-package.md).

## <a name="related-topics"></a>Související témata

- [Balíček odkazy v souborech projektu](../consume-packages/package-references-in-project-files.md) popisuje všechny podrobnosti o popisující vašeho balíčku přímo v souboru projektu.
- [NuGet pack a obnovit jako cíle MSBuild](../schema/msbuild-targets.md) popisuje všechny možnosti použití `msbuild /t:pack` k vytvoření balíčku.
- [Standardní knihovny .NET dokumentaci](https://docs.microsoft.com/dotnet/articles/standard/library)
- [Portování do .NET Core z rozhraní .NET Framework](https://docs.microsoft.com/dotnet/articles/core/porting/index)
