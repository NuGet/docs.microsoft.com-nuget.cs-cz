---
title: Vytvoření balíčků Rozhraní .NET Standard a .NET Framework NuGet pomocí sady Visual Studio 2015
description: Komplexní návod k vytváření balíčků .NET Standard a .NET Framework NuGet pomocí nuget3.x a Visual Studio 2015.
author: karann-msft
ms.author: karann
ms.date: 02/02/2018
ms.topic: tutorial
ms.openlocfilehash: b16bf422e2627be3b8516a875d749639734064a9
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "72380726"
---
# <a name="create-net-standard-and-net-framework-packages-with-visual-studio-2015"></a>Vytvoření balíčků rozhraní .NET Standard a .NET Framework pomocí sady Visual Studio 2015

**Poznámka:** Visual Studio 2017 se doporučuje pro vývoj knihoven .NET Standard. Visual Studio 2015 může fungovat, ale nástroje .NET Core byly přeneseny pouze do stavu Náhled. Viz [Vytvoření a publikování balíčku s Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) pro práci s NuGet 4.x+ a Visual Studio 2017.

[Standardní knihovna .NET](/dotnet/articles/standard/library) je formální specifikace rozhraní .NET API, která má být k dispozici ve všech runčasech .NET, čímž vytváří větší jednotnost v ekosystému .NET. Standardní knihovna .NET definuje jednotnou sadu rozhraní API BCL (Base Class Library) pro všechny platformy .NET k implementaci, nezávisle na zatížení. Umožňuje vývojářům vytvářet kód, který je použitelný ve všech runčasech .NET, a snižuje, pokud neeliminuje direktivy podmíněné kompilace specifické pro platformu ve sdíleném kódu.

Tato příručka vás provede vytvořením balíčku NuGet, který cílí na .NET Standard Library 1.4 nebo balíček zaměřený na rozhraní .NET Framework 4.6. Knihovna .NET Standard 1.4 funguje napříč rozhraním .NET Framework 4.6.1, Univerzální platformou Windows 10, .NET Core a Mono/Xamarin. Podrobnosti naleznete v [tabulce mapování standardu .NET](/dotnet/standard/net-standard#net-implementation-support) (dokumentace k rozhraní.NET). Pokud chcete, můžete zvolit jinou verzi knihovny .NET Standard.

## <a name="prerequisites"></a>Požadavky

1. Visual Studio 2015 Update 3
1. (Pouze standard.NET) [Sada SDK jádra .NET](https://www.microsoft.com/net/download/)
1. NuGet CLI. Stáhněte si nejnovější verzi nuget.exe z [nuget.org/downloads](https://nuget.org/downloads)a uložte ji do zvoleného umístění. Pak přidejte toto umístění do proměnné prostředí PATH, pokud ještě není.

    > [!Note]
    > nuget.exe je samotný nástroj rozhraní příkazového příkazu, nikoli instalátor, takže nezapomeňte uložit stažený soubor z prohlížeče namísto jeho spuštění.

## <a name="create-the-class-library-project"></a>Vytvoření projektu knihovny tříd

1. V sadě Visual Studio rozbal **> >te**uzel **Visual C# > Windows** , vyberte **Knihovnu tříd (Portable),** změňte název na AppLogger a vyberte **OK**.

    ![Vytvořit nový projekt knihovny tříd](media/NetStandard-NewProject.png)

1. V zobrazeném dialogovém okně **Přidat knihovnu přenosných tříd** vyberte volby pro `.NET Framework 4.6` a `ASP.NET Core 1.0`. (Pokud cílení .NET Framework, můžete vybrat podle toho, které možnosti jsou vhodné.)

1. Pokud cílíte na standard `AppLogger (Portable)` .NET, klikněte pravým tlačítkem myši na položku Průzkumník řešení a vyberte **vlastnosti**, vyberte kartu **Knihovna** a v části **Cílení** vyberte **možnost Cílová platforma .NET Standard.** Tato akce vyzve k potvrzení, po `.NET Standard 1.4` kterém můžete vybrat (nebo jinou dostupnou verzi) z rozbalovacího programu:

    ![Nastavení cíle na standard .NET 1.4](media/NetStandard-ChangeTarget.png)

1. Klikněte na kartu **Sestavení,** `Release`změňte **konfiguraci** na a zaškrtněte **políčko soubor dokumentace XML**.

1. Přidejte kód do komponenty, například:

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

1. Nastavte konfiguraci na Release, vytvořte projekt a zkontrolujte, zda `bin\Release` jsou soubory DLL a XML vytvořeny ve složce.

## <a name="create-and-update-the-nuspec-file"></a>Vytvoření a aktualizace souboru Nuspec

1. Otevřete příkazový řádek, přejděte `AppLogger.csproj` do složky obsahující `.sln` složku (o jednu `spec` úroveň níže, `AppLogger.nuspec` kde je soubor) a spusťte příkaz NuGet a vytvořte počáteční soubor:

    ```cli
    nuget spec
    ```

1. Otevřete `AppLogger.nuspec` v editoru a aktualizujte jej tak, aby odpovídal následujícímu, a nahrazují YOUR_NAME příslušnou hodnotou. Hodnota, `<id>` konkrétně musí být jedinečný v celé nuget.org (viz konvence pojmenování popsané v [vytvoření balíčku](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number). Všimněte si také, že musíte také aktualizovat značky autora a popisu nebo se během kroku balení zobrazí chyba.

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

1. Přidejte do souboru `.nuspec` referenční sestavení, konkrétně knihovnu DLL knihovny a soubor XML technologie IntelliSense:

    Pokud cílení .NET Standard, položky se zobrazí podobně jako následující:

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

    Pokud cílení .NET Framework, položky se zobrazí podobně jako následující:

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\net46\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\net46\AppLogger.xml" />
    </files>
    ```

1. Klikněte pravým tlačítkem myši na řešení a vyberte **sestavit řešení** generovat všechny soubory pro balíček.

### <a name="declaring-dependencies"></a>Deklarování závislostí

Pokud máte nějaké závislosti na jiných balíčcích NuGet, `<dependencies>` uveďte `<group>` je v elementu manifestu s prvky. Chcete-li například deklarovat závislost na souboru NewtonSoft.Json 8.0.3 nebo vyšší, přidejte následující:

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

Syntaxe atributu *version* zde označuje, že verze 8.0.3 nebo vyšší je přijatelná. Chcete-li určit různé rozsahy verzí, podívejte se na [správa verzí balíčků](../concepts/package-versioning.md).

### <a name="adding-a-readme"></a>Přidání readme

Vytvořte `readme.txt` soubor, umístěte jej do kořenové složky `.nuspec` projektu a podívejte se na něj v souboru:

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

Visual Studio `readme.txt` zobrazit při instalaci balíčku do projektu. Soubor není zobrazen při instalaci do projektů .NET Core nebo pro balíčky, které jsou nainstalovány jako závislost.

## <a name="package-the-component"></a>Balení komponenty

S dokončeným `.nuspec` odkazováním na všechny soubory, které potřebujete zahrnout do `pack` balíčku, jste připraveni spustit příkaz:

```cli
nuget pack AppLogger.nuspec
```

To generuje `AppLogger.YOUR_NAME.1.0.0.nupkg`. Otevření tohoto souboru v nástroji, jako je [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) a rozbalení všech uzlů, uvidíte následující obsah (zobrazeno pro .NET Standard):

![NuGet Package Explorer zobrazující balíček AppLogger](media/NetStandard-PackageExplorer.png)

> [!Tip]
> Soubor `.nupkg` je pouze soubor ZIP s jinou příponou. Můžete také prozkoumat obsah balíčku, `.nupkg` `.zip`pak změnou na , ale nezapomeňte obnovit rozšíření před odesláním balíček nuget.org.

Chcete-li balíček zpřístupnit ostatním [vývojářům,](../nuget-org/publish-a-package.md)postupujte podle pokynů k části Publikovat balíček .

Všimněte `pack` si, že vyžaduje Mono 4.4.2 na Mac OS X a nefunguje na systémech Linux. Na Macu musíte také převést názvy cest Windows v souboru `.nuspec` na cesty ve stylu Unixu.

## <a name="related-topics"></a>Související témata

- [Odkaz .nuspec](../reference/nuspec.md)
- [Podpora více verzí rozhraní .NET framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Zahrnout rekvizity a cíle MSBuild do balíčku](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Vytvoření lokalizovaných balíčků](../create-packages/creating-localized-packages.md)
- [Balíčky symbolů](../create-packages/symbol-packages-snupkg.md)
- [Správa verzí balíčku](../concepts/package-versioning.md)
- [Dokumentace standardní knihovny .NET](/dotnet/articles/standard/library)
- [Přenesení na jádro .NET z rozhraní .NET Framework](/dotnet/articles/core/porting/index)
