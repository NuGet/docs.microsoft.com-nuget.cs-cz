---
title: "Vytvoření balíčků NuGet standardní .NET s Visual Studiem 2015 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 29b3bceb-0f35-4cdd-bbc3-a04eb823164c
description: "Návod začátku do konce, vytváření balíčků NuGet pro rozhraní .NET standardní pomocí nástroje NuGet 3.x a Visual Studio 2015."
keywords: "Vytvoření balíčku, .NET Standard balíčky, .NET Standard mapování tabulky"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a912c27e1873d60426f2147995f69e2dcc433ca9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="create-net-standard-packages-with-visual-studio-2015"></a>Vytvoření balíčků .NET Standard s Visual Studio 2015

*Platí pro NuGet 3.x. V tématu [vytvořit .NET standardní balíčky s Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) pro práci s NuGet 4.x+.*

[Standardní knihovny .NET](https://docs.microsoft.com/dotnet/articles/standard/library) je formální specifikaci rozhraní API technologie .NET by měla být k dispozici pro všechny moduly runtime rozhraní .NET, tím větší jednotnost vytváří v ekosystému .NET. Standardní knihovny .NET definuje jednotnou sadu BCL (základní třída knihovna) rozhraní API pro všechny platformy .NET implementovat, nezávisle na zatížení. Ji umožňuje vývojářům vytvářet PCLs, které jsou použitelné pro všechny moduly runtime rozhraní .NET, a snižuje, pokud není eliminuje direktivy specifické pro platformu Podmíněná kompilace v sdíleného kódu.

Tato příručka vás provede procesem vytvoření balíčku nuget cílení na rozhraní .NET standardní knihovně 1,4. To bude fungovat přes rozhraní .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core a Mono nebo Xamarin. Podrobnosti najdete v tématu [.NET Standard mapovací tabulku](#net-standard-mapping-table) dál v tomto tématu.

1. [Předpoklady](#pre-requisites)
1. [Vytvoření projektu knihovny tříd](#create-the-class-library-project)
1. [Vytvářet a aktualizovat soubor s příponou .nuspec](#create-and-update-the-nuspec-file)
1. [Balíček součásti](#package-the-component)
1. [Další možnosti](#additional-options)
1. [.NET standard mapování tabulky](#net-standard-mapping-table)
1. [Související témata](#related-topics)


## <a name="pre-requisites"></a>Předpoklady

1. Visual Studio 2015. Instalaci edice Community zdarma z [visualstudio.com](https://www.visualstudio.com/); samozřejmě můžete taky edice Professional a Enterprise.
1. .NET core: Instalace .NET Core společně s šablony a dalších nástrojů pro Visual Studio 2015 z [https://go.microsoft.com/fwlink/?LinkId=824849](https://go.microsoft.com/fwlink/?LinkId=824849).
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
                throw new NotImplementedException("Called Log");
            }
        }
    }
    ```

1. Sestavení projektu (s konfigurací verzi) a zkontrolujte, že jsou ve složce bin\Release vytváří soubory DLL a XML.

## <a name="create-and-update-the-nuspec-file"></a>Vytvářet a aktualizovat soubor s příponou .nuspec

1. Otevřete příkazový řádek, přejděte do složky obsahující `AppLogg.csproj` složky (o jednu úroveň pod where `.sln` soubor), a spusťte NuGet `spec` příkaz pro vytvoření počáteční `AppLogger.nuspec` souboru:

```
nuget spec
```

1. Otevřete `AppLogger.nuspec` v editoru a aktualizovat ji tak, aby odpovídala následující, nahraďte vaše_jméno odpovídající hodnotu. `<id>` Hodnotu, konkrétně musí být jedinečný v rámci nuget.org (viz zásady vytváření názvů, které jsou popsané v [vytváření balíčku](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number). Všimněte si také, zda je nutné také aktualizovat autora a popis značky nebo budete dojde k chybě během kroku okolních.

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
    <copyright>Copyright 2016 (c) Contoso Corporation. All rights reserved.</copyright>
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


## <a name="package-the-component"></a>Balíček součásti

S dokončené `.nuspec` odkazující na všechny soubory, které je potřeba zahrnout do balíčku, jste připraveni ke spuštění `pack` příkaz:

```
nuget pack AppLogger.nuspec
```

Tím se vygeneruje `AppLogger.YOUR_NAME.1.0.0.nupkg`. Otevření tohoto souboru v nástroje, jako [Explorer balíček NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) a rozšiřování všechny uzly, zobrazí se následující obsah:

![Průzkumník balíček NuGet zobrazující AppLogger balíčku](media/NetStandard-PackageExplorer.png)

> [!Tip]
> A `.nupkg` soubor je právě soubor ZIP s jiné rozšíření. Můžete také zkontrolovat obsah balíčku, potom změnou `.nupkg` k `.zip`, ale nezapomeňte obnovit rozšíření před balíčku se nahrávají na nuget.org.

Pokud chcete zpřístupnit vašeho balíčku jinými vývojáři, postupujte podle pokynů [publikování balíčku](../create-packages/publish-a-package.md).

Všimněte si, že `pack` vyžaduje Mono 4.4.2 na Mac OS X a nefunguje v systémech Linux. V systému Mac, je nutné také převést Windows názvy cest v `.nuspec` souboru do cesty formátu UNIX.

## <a name="additional-options"></a>Další možnosti

V následujících částech přejít do další možnosti pro vytvoření balíčku NuGet:

- [Deklarování závislosti](#declaring-dependencies)
- [Podpora více cílové rozhraní](#supporting-multiple-target-frameworks)
- [Přidání cíle a props pro nástroje MSBuild](#adding-targets-and-props-for-msbuild)
- [Vytvoření lokalizovaných balíčků](#creating-localized-packages)
- [Přidání soubor readme](#adding-a-readme)

### <a name="declaring-dependencies"></a>Deklarování závislosti

Pokud máte všechny závislosti na dalších balíčcích NuGet, programů v seznamu `<dependencies>` element s `<group>` elementy. Chcete-li například závislost na NewtonSoft.Json 8.0.3 deklarovat nebo vyšší, přidejte následující:

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

Syntaxe *verze* atribut zde označuje, že verze 8.0.3 nebo novější je přijatelná. Zadejte jinou verzi rozsahy, najdete v tématu [Správa verzí balíčku](../reference/package-versioning.md).

### <a name="supporting-multiple-target-frameworks"></a>Podpora více cílové rozhraní

Předpokládejme, že chcete využít výhod rozhraní API v rozhraní .NET Framework 4.6.2, který není k dispozici v rozhraní .NET standardní 1.4. K tomuto účelu, budete nejprve muset Ujistěte se, že knihovny zkompiluje pro .NET 4.6.2 pomocí Podmíněná kompilace nebo sdílených projektů. (V sadě Visual Studio, můžete vytvořit projekt NetCore, přidejte rozhraní výběru oddílu více framework a následně vytvořit.) Pak vytvoříte balíček použití jednoduchého postupu založené na konvenci directory pracovní následujícím způsobem:

1. V projektu kořenovou složku obsahující vaše `.nuspec` souboru, vytvořte složku s názvem `lib`.
1. Uvnitř `lib`, vytvořte složky pro každou platformu, které chcete podporovat:

        \lib
            \netstandard1.4
                \AppLogger.dll
            \net462
                \AppLogger.dll

1. V `.nuspec` soubor, přidejte `files` pod uzlem `package` uzlu a odkazovat na soubory v `lib` pomocí zástupných znaků. **Poznámka:** Token náhrady nejsou podporovány s přístupem založené na konvenci pracovní adresář, takže je nahradit literálových hodnot:

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>AppLogger.YOUR_NAME</id>
        <version>1.0.0.0</version>
        <title>AppLogger</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release.</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>logger logging logs</tags>
        </metadata>
        <files>
            <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. Vytvořit balíček znovu s použitím `nuget pack AppLogger.spec`.

Další podrobnosti o použití Tato technika, najdete v části [podpora více verzí rozhraní .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)

### <a name="adding-targets-and-props-for-msbuild"></a>Přidání cíle a props pro nástroje MSBuild

V některých případech můžete chtít přidat vlastní sestavovací cíle nebo vlastnosti v projektech, které využívají vašeho balíčku, jako je například spuštění vlastního nástroje nebo procesu během vytváření sestavení. To uděláte tak, že přidáte soubory v `\build` složky, jak je popsáno v následujících krocích. Při instalaci balíčku NuGet se soubory \build přidá MSBuild element v souboru projektu odkazující na soubory .targets a props.

> [!Note]
> Při použití `project.json`, cíle nejsou přidány do projektu, ale jsou k dispozici prostřednictvím `project.lock.json`.


1. V projektu složku obsahující vaše `.nuspec` souboru, vytvořte složku s názvem `build`.
1. Uvnitř `build`, vytváření složek pro všechny podporované a v rámci ty umístit vaše `.targets` a `.props` soubory:

        \build
            \netstandard1.4
                \AppLogger.props
                \AppLogger.targets
            \net462
                \AppLogger.props
                \AppLogger.targets

1. V `.nuspec` soubor, přidejte `files` pod uzlem `package` uzlu a odkazovat na soubory v `build` pomocí zástupných znaků.

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>...
        </metadata>
        <files>
            <file src="build\**" target="build" />
        </files>
    </package>
    ```

1. Vytvořit balíček znovu s použitím `nuget pack AppLogger.nuspec`.

Další podrobnosti najdete v části [zahrnují MSBuild props a cíle v balíčku](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package).


### <a name="creating-localized-packages"></a>Vytvoření lokalizovaných balíčků

Pokud chcete vytvořit lokalizované verze knihovny, můžete vytvořit samostatné balíčky pro různá národní prostředí nebo zahrnout lokalizovaný prostředek sestavení v rámci jednoho balíčku. Tady je postup pozdější přístup, němčiny a Italština:

1. V rámci každé cílové složce framework pod `lib`, vytvořte složky pro každý podporovaný jazyk jiné než anglické výchozí. V uvedených složkách můžete umístit prostředek sestavení a lokalizované soubory IntelliSense XML. Příklad:

        lib
        ├───netstandard1.4
        │   │   AppLogger.dll
        │   │   AppLogger.xml
        │   │
        │   ├───de
        │   │       AppLogger.resources.dll
        │   │       AppLogger.xml
        │   │
        │   └───it
        │           AppLogger.resources.dll
        │           AppLogger.xml
        └───net462
            │   AppLogger.dll
            │   AppLogger.xml
            │
            ├───de
            │       AppLogger.resources.dll
            │       AppLogger.xml
            │
            └───it
                    AppLogger.resources.dll
                    AppLogger.xml

1. V `.nuspec` souboru, odkazují tyto soubory v `<files>` uzlu:

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>...
        </metadata>
        <files>
        <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. Vytvořit balíček znovu s použitím `nuget pack AppLogger.nuspec`.


### <a name="adding-a-readme"></a>Přidání soubor readme

Pokud zahrnete `readme.txt` souboru v kořenu balíčku, Visual Studio se zobrazí se při instalaci balíčku přímo.

> [!Note]
> Soubory Readme nejsou zobrazeny pro balíčky, které se instalují jako závislost, nebo pro projekty .NET Core.


Chcete-li to provést, vytvořte vaše `readme.txt` souboru, umístěte do kořenové složky projektu a najdete ji v `.nuspec` souboru:

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


## <a name="net-standard-mapping-table"></a>.NET standard mapování tabulky

|Název platformy |Alias|
|--------------|-----|
|Standardní rozhraní .NET | monikerů netstandard| 1.0| 1.1| 1.2| 1.3| 1.4| 1.5| 1.6|
|.NET Core | netcoreapp| & #x 2192;| & #x 2192;| & #x 2192;| & #x 2192;| & #x 2192;| & #x 2192;| 1.0|
|.NET Framework| NET| 4.5| 4.5.1| 4.6| 4.6.1| 4.6.2| 4.6.3|
|Platformy mono nebo Xamarin| & #x 2192;| & #x 2192;| & #x 2192;| & #x 2192;| & #x 2192;| & #x 2192;|
|Univerzální platforma pro Windows| uap| & #x 2192;| & #x 2192;| & #x 2192;| & #x 2192;|10.0|
|Windows| Win| & #x 2192;| 8.0| 8.1|
|Windows Phone| WPA| & #x 2192;| & #x 2192;|8.1|
|Windows Phone Silverlight| webové části| 8.0|



## <a name="related-topics"></a>Související témata

- [Odkaz na soubor Nuspec](../schema/nuspec.md)
- [Symbol balíčky](../create-packages/symbol-packages.md)
- [Správa verzí balíčku](../reference/package-versioning.md)
- [Podpora více verzí rozhraní .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Zahrnout do balíčku nástroje MSBuild props a cíle](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [Vytvoření lokalizovaných balíčků](../create-packages/creating-localized-packages.md)
- [Standardní knihovny .NET dokumentaci](https://docs.microsoft.com/dotnet/articles/standard/library)
- [Portování do .NET Core z rozhraní .NET Framework](https://docs.microsoft.com/dotnet/articles/core/porting/index)
