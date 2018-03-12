---
title: "Vytvoření balíčků NuGet standardní .NET s Visual Studiem 2015 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/02/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Návod začátku do konce, vytváření balíčků NuGet pro rozhraní .NET standardní pomocí nástroje NuGet 3.x a Visual Studio 2015."
keywords: "Vytvoření balíčku, .NET Standard balíčky, .NET Standard mapování tabulky"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c15ffd709856fc9d5b9a9fb2fe87c0029b82650d
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/08/2018
---
# <a name="create-net-standard-packages-with-visual-studio-2015"></a>Vytvoření balíčků .NET Standard s Visual Studio 2015

*Platí pro NuGet 3.x. V tématu [vytvoření a publikování balíčku s Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) pro práci s NuGet 4.x+.*

[Standardní knihovny .NET](/dotnet/articles/standard/library) je formální specifikaci rozhraní API technologie .NET by měla být k dispozici pro všechny moduly runtime rozhraní .NET, tím větší jednotnost vytváří v ekosystému .NET. Standardní knihovny .NET definuje jednotnou sadu BCL (základní třída knihovna) rozhraní API pro všechny platformy .NET implementovat, nezávisle na zatížení. Umožňuje vývojářům vytvářet kód, který je použitelný přes všechny moduly runtime rozhraní .NET a snižuje není eliminuje direktivy specifické pro platformu Podmíněná kompilace v sdíleného kódu.

Tento průvodce vás provede procesem vytváření balíčku NuGet cílení .NET standardní knihovny 1.4. Tuto knihovnu funguje napříč rozhraní .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core a Mono nebo Xamarin. Podrobnosti najdete v tématu [.NET Standard mapovací tabulku](#net-standard-mapping-table) dál v tomto tématu.

## <a name="prerequisites"></a>Požadavky

1. Visual Studio 2015 Update 3
1. [.NET core SDK](https://www.microsoft.com/net/download/)
1. Rozhraní příkazového řádku NuGet. Stáhněte si nejnovější verzi nuget.exe z [nuget.org/downloads](https://nuget.org/downloads), ukládání do umístění podle vaší volby. Pak přidejte tohoto umístění do vaší proměnné prostředí PATH, pokud již není.

    > [!Note]
    > nuget.exe je že nástroj příkazového řádku, není instalační program, takže je nutné z prohlížeče namísto spuštění ho uložte stažený soubor.

## <a name="create-the-class-library-project"></a>Vytvoření projektu knihovny tříd

1. V sadě Visual Studio **soubor > Nový > projekt**, rozbalte **Visual C# > Windows** uzlu, vyberte **knihovny tříd (přenositelností)**, změňte název na AppLogger a klikněte na tlačítko OK.

    ![Vytvoření nového projektu knihovny tříd](media/NetStandard-NewProject.png)

1. V **přidat Přenosná knihovna tříd** dialog, který se zobrazí, vyberte `.NET Framework 4.6` a `ASP.NET Core 1.0` možnosti.

1. Klikněte pravým tlačítkem myši `AppLogger (Portable)` v Průzkumníku řešení, vyberte **vlastnosti**, vyberte **knihovny** a potom klikněte na tlačítko **Standard platformy cílové rozhraní .NET** v **Cílení** části. Zobrazí se výzva k potvrzení, po kterém můžete vybrat `.NET Standard 1.4` v rozevíracím seznamu:

    ![Nastavení cíl na standardní 1.4 rozhraní .NET](media/NetStandard-ChangeTarget.png)

1. Klikněte na **sestavení** změňte **konfigurace** k `Release`a zaškrtněte políčko pro **souborů dokumentace XML**.

1. Přidáte kód pro součásti, například:

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

1. Nastavte konfiguraci na verzi, sestavte projekt a zkontrolujte, že jsou v rámci vytváří soubory DLL a XML `bin\Release` složky.

## <a name="create-and-update-the-nuspec-file"></a>Vytvářet a aktualizovat soubor s příponou .nuspec

1. Otevřete příkazový řádek, přejděte do složky obsahující `AppLogger.csproj` složky (o jednu úroveň pod where `.sln` soubor), a spusťte NuGet `spec` příkaz pro vytvoření počáteční `AppLogger.nuspec` souboru:

```cli
nuget spec
```

1. Otevřete `AppLogger.nuspec` v editoru a aktualizovat ji tak, aby odpovídala následující, nahraďte vaše_jméno odpovídající hodnotu. `<id>` Hodnotu, konkrétně musí být jedinečný v rámci nuget.org (viz zásady vytváření názvů, které jsou popsané v [vytváření balíčku](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number). Všimněte si také, zda je nutné také aktualizovat autora a popis značky nebo dojde k chybě během kroku okolních.

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>AppLogger.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>AppLogger</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome application logging utility</description>
    <releaseNotes>First release</releaseNotes>
    <copyright>Copyright 2018 (c) Contoso Corporation. All rights reserved.</copyright>
    <tags>logger logging logs</tags>
    </metadata>
</package>
```

1. Přidat odkaz na sestavení, které chcete `.nuspec` souboru, a to knihovně DLL a soubor IntelliSense XML:

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

1. Klikněte pravým tlačítkem na řešení a vyberte **sestavit řešení** ke generování všechny soubory pro balíček.

### <a name="declaring-dependencies"></a>Deklarování závislosti

Pokud máte všechny závislosti na dalších balíčcích NuGet, seznamu těch, které do manifestu `<dependencies>` element s `<group>` elementy. Chcete-li například závislost na NewtonSoft.Json 8.0.3 deklarovat nebo vyšší, přidejte následující:

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

Syntaxe *verze* atribut zde označuje, že verze 8.0.3 nebo novější je přijatelná. Zadejte jinou verzi rozsahy, najdete v tématu [Správa verzí balíčku](../reference/package-versioning.md).

### <a name="adding-a-readme"></a>Přidání soubor readme

Vytvoření vaší `readme.txt` souboru, umístěte do kořenové složky projektu a najdete ji v `.nuspec` souboru:

```xml
<?xml version="1.0"?>
<package >
    <metadata>...
    </metadata>
    <files>
    <file src="readme.txt" target="" />
    </files>
</package>
```

Visual Studio zobrazení `readme.txt` při instalaci balíčku do projektu. Soubor se nezobrazí, pokud nainstalované do projektů .NET Core, nebo pro balíčky, které se instalují jako závislost.

## <a name="package-the-component"></a>Balíček součásti

S dokončené `.nuspec` odkazující na všechny soubory, které je potřeba zahrnout do balíčku, jste připraveni ke spuštění `pack` příkaz:

```cli
nuget pack AppLogger.nuspec
```

Tím se vygeneruje `AppLogger.YOUR_NAME.1.0.0.nupkg`. Otevření tohoto souboru v nástroje, jako [Explorer balíček NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) a rozšiřování všechny uzly, můžete zobrazit následující obsah:

![Průzkumník balíček NuGet zobrazující AppLogger balíčku](media/NetStandard-PackageExplorer.png)

> [!Tip]
> A `.nupkg` soubor je právě soubor ZIP s jiné rozšíření. Můžete také zkontrolovat obsah balíčku, potom změnou `.nupkg` k `.zip`, ale nezapomeňte obnovit rozšíření před balíčku se nahrávají na nuget.org.

Pokud chcete zpřístupnit vašeho balíčku jinými vývojáři, postupujte podle pokynů [publikování balíčku](../create-packages/publish-a-package.md).

Všimněte si, že `pack` vyžaduje Mono 4.4.2 na Mac OS X a nefunguje v systémech Linux. V systému Mac, je nutné také převést Windows názvy cest v `.nuspec` souboru do cesty formátu UNIX.

## <a name="net-standard-mapping-table"></a>.NET standard mapování tabulky

| Název platformy | Alias |
| --- | --- |
| Standardní rozhraní .NET | monikerů netstandard | 1.0 | 1.1 | 1.2 | 1.3 | 1.4 | 1.5 | 1.6 |
| .NET Core | netcoreapp | &#x2192; | &#x2192; | &#x2192; | &#x2192; | &#x2192; | &#x2192; | 1.0 |
| .NET Framework | NET | 4.5 | 4.5.1 | 4.6 | 4.6.1 | 4.6.2 | 4.6.3 |
| Mono/Xamarin Platforms | &#x2192; | &#x2192; | &#x2192; | &#x2192; | &#x2192; | &#x2192; |
| Univerzální platforma pro Windows | uap | &#x2192; | &#x2192; | &#x2192; | &#x2192; |10.0 |
| Windows | Win| &#x2192; | 8.0 | 8.1 |
| Windows Phone | wpa| &#x2192;| &#x2192; | 8.1 |
| Windows Phone Silverlight | wp | 8.0 |

## <a name="related-topics"></a>Související témata

- [referenční dokumentace příponou .nuspec](../reference/nuspec.md)
- [Podpora více verzí rozhraní .NET framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Zahrnout do balíčku nástroje MSBuild props a cíle](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [Vytvoření lokalizovaných balíčků](../create-packages/creating-localized-packages.md)
- [Balíčky symbolů](../create-packages/symbol-packages.md)
- [Správa verzí balíčků](../reference/package-versioning.md)
- [Standardní knihovny .NET dokumentaci](/dotnet/articles/standard/library)
- [Portování do .NET Core z rozhraní .NET Framework](/dotnet/articles/core/porting/index)
