---
title: Vytvoření .NET Standard a balíčky NuGet rozhraní .NET Framework pomocí sady Visual Studio 2015
description: Začátku do konce postup vytváření balíčků NuGet pro rozhraní .NET Framework a .NET Standard s využitím NuGet 3.x a Visual Studio 2015.
author: karann-msft
ms.author: karann
ms.date: 02/02/2018
ms.topic: tutorial
ms.openlocfilehash: 1198a781543e581f55740cc0ae5a212d3f8a8b61
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842446"
---
# <a name="create-net-standard-and-net-framework-packages-with-visual-studio-2015"></a>Vytváření balíčků pro .NET Standard a .NET Framework pomocí sady Visual Studio 2015

**Poznámka:** Visual Studio 2017 se doporučuje pro vývoj knihoven .NET Standard. Visual Studio 2015 můžete pracovat, ale nástroje pro .NET Core se přepne do režimu jenom pro verzi Preview. Zobrazit [vytvoření a publikování balíčku sady Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) pro práci s NuGet 4.x+ a sady Visual Studio 2017.

[Knihovna .NET Standard](/dotnet/articles/standard/library) je formální specifikaci rozhraní .NET API by měla být k dispozici pro všechny moduly runtime .NET, tedy vytvoření většího sjednocení v ekosystému .NET. Knihovna .NET Standard definuje jednotnou sadu BCL (knihovna tříd Base) rozhraní API pro všechny platformy .NET pro implementaci, nezávisle na úloze. Umožňuje vývojářům vytvářet kód, který je použitelný přes všechny moduly runtime .NET a snižuje, pokud nebude eliminuje direktivy podmíněné kompilace specifické pro platformu v sdílený kód.

Tento průvodce vás provede vytvořením cílí na .NET Standard knihovny 1.4 balíček NuGet nebo pomocí balíčku cílení na rozhraní .NET Framework 4.6. Knihovna .NET Standard 1.4 funguje i rozhraní .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, Mono/Xamarin. Podrobnosti najdete v tématu [.NET Standard mapování tabulky](/dotnet/standard/net-standard#net-implementation-support) (dokumentace k .NET). Chcete-li, můžete zvolit jinou verzi knihovny .NET Standard.

## <a name="prerequisites"></a>Požadavky

1. Visual Studio 2015 Update 3
1. (Pouze .NET standard) [.NET core SDK](https://www.microsoft.com/net/download/)
1. Rozhraní příkazového řádku NuGet. Stažení nejnovější verze programu nuget.exe z [nuget.org/downloads](https://nuget.org/downloads), ukládání do umístění podle vašeho výběru. Pak přidejte toto umístění do proměnné prostředí PATH, pokud ještě není.

    > [!Note]
    > nuget.exe je že nástroj příkazového řádku, není instalační program, proto ji nezapomeňte Uložte stažený soubor ve svém prohlížeči místo jeho spuštění.

## <a name="create-the-class-library-project"></a>Vytvořte projekt knihovny tříd

1. V sadě Visual Studio **soubor > Nový > projekt**, rozbalte **Visual C# > Windows** uzlu, vyberte **knihovna tříd (přenosná)** , změňte název na AppLogger a vyberte **OK**.

    ![Vytvořit nový projekt knihovny tříd](media/NetStandard-NewProject.png)

1. V **přidat přenosnou knihovnu tříd** dialogové okno, které se zobrazí, vyberte požadované možnosti pro `.NET Framework 4.6` a `ASP.NET Core 1.0`. (Pokud je zaměřen na rozhraní .NET Framework, můžete vybrat toho možnosti je vhodné.)

1. Cílení na .NET Standard, klikněte pravým tlačítkem `AppLogger (Portable)` v Průzkumníku řešení vyberte **vlastnosti**, vyberte **knihovny** kartu a potom vyberte **cílové Standard platformy .NET** v **cílení** oddílu. Tato akce zobrazí výzvu k potvrzení, po kterém můžete vybrat `.NET Standard 1.4` (nebo jinou verzi k dispozici) z rozevíracího seznamu:

    ![Nastavení cíl na .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. Klikněte na **sestavení** kartu, změnit **konfigurace** k `Release`a zaškrtněte políčko u **soubor dokumentace XML**.

1. Přidejte svůj kód na součást, například:

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

1. Nastavení konfigurace pro vydání, sestavte projekt a zkontrolujte, že jsou soubory DLL a XML vytvořený v rámci `bin\Release` složky.

## <a name="create-and-update-the-nuspec-file"></a>Vytvoření a aktualizaci souboru .nuspec souboru

1. Otevřete příkazový řádek, přejděte na složku obsahující `AppLogger.csproj` složky (o jednu úroveň pod where `.sln` soubor), a spusťte NuGet `spec` příkaz pro vytvoření počáteční `AppLogger.nuspec` souboru:

    ```cli
    nuget spec
    ```

1. Otevřít `AppLogger.nuspec` v editoru a aktualizujte ji, aby se shodoval s následujícím, nahradíte vaše_jméno odpovídající hodnotu. `<id>` , Konkrétně musí být hodnota jedinečná napříč nuget.org (naleznete v tématu Zásady vytváření názvů je popsáno v [vytvoření balíčku](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number). Všimněte si také, že budete muset taky aktualizovat Autor a popis značky nebo dojde k chybě během kroku balení.

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

1. Přidejte referenční sestavení pro `.nuspec` souboru, a to knihovny DLL a soubor IntelliSense XML:

    Cílení na .NET Standard, položky se zobrazí podobný následujícímu:

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

    Pokud se zaměřujete na rozhraní .NET Framework, vypadat podobně jako následující položky:

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\net46\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\net46\AppLogger.xml" />
    </files>
    ```

1. Klikněte pravým tlačítkem na řešení a vyberte **sestavit řešení** vygenerujte tyto soubory pro balíček.

### <a name="declaring-dependencies"></a>Deklarace závislostí

Pokud máte všechny závislosti na dalších balíčcích NuGet, seznamu programů v manifestu `<dependencies>` element s `<group>` elementy. Chcete-li například deklaruje závislost na NewtonSoft.Json 8.0.3 nebo novější, přidejte následující:

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

Syntaxe *verze* atribut tady označuje tuto verzi 8.0.3 nebo vyšší je přijatelné. Zadejte rozsahy jinou verzi, najdete v tématu [Správa verzí balíčků](../reference/package-versioning.md).

### <a name="adding-a-readme"></a>Přidání souboru readme

Vytvoření vašeho `readme.txt` souboru, umístěte ho do kořenové složky projektu a najdete ji v `.nuspec` souboru:

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

Visual Studio zobrazení `readme.txt` při instalaci balíčku do projektu. Soubor se nezobrazí při instalaci do projektů .NET Core nebo pro balíčky, které se instalují jako závislost.

## <a name="package-the-component"></a>Balíček komponenty

S dokončenou `.nuspec` odkazující na všechny soubory, které je potřeba zahrnout do balíčku, jste připraveni spustit `pack` příkaz:

```cli
nuget pack AppLogger.nuspec
```

Tím se vygeneruje `AppLogger.YOUR_NAME.1.0.0.nupkg`. Tento soubor otevřete v nástroje, jako je [NuGet – Průzkumník balíčků](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) a rozšiřuje všechny uzly, viz následující obsah (viz obrázek pro .NET Standard):

![Zobrazuje AppLogger balíčku NuGet – Průzkumník balíčků](media/NetStandard-PackageExplorer.png)

> [!Tip]
> A `.nupkg` soubor je jenom soubor ZIP s jinou příponou. Můžete také prozkoumat obsah balíčku, potom změnou `.nupkg` k `.zip`, ale nezapomeňte k obnovení rozšíření před nahráním balíčků na nuget.org.

Aby váš balíček k dispozici s ostatními vývojáři, postupujte podle pokynů [publikování balíčku](../nuget-org/publish-a-package.md).

Všimněte si, že `pack` vyžaduje Mono 4.4.2 v Mac OS X a nebude fungovat v systémech Linux. Na počítači Mac, je také nutné převést Windows cest v `.nuspec` soubor do cesty k systému UNIX.

## <a name="related-topics"></a>Související témata

- [odkaz na souboru .nuspec](../reference/nuspec.md)
- [Podpora více verzí rozhraní .NET framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Zahrnout do balíčku cíle a vlastnosti nástroje MSBuild](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Vytvoření lokalizovaných balíčků](../create-packages/creating-localized-packages.md)
- [Balíčky symbolů](../create-packages/symbol-packages.md)
- [Správa verzí balíčků](../reference/package-versioning.md)
- [Dokumentace ke službě knihovna .NET standard](/dotnet/articles/standard/library)
- [Portování do .NET Core v rozhraní .NET Framework](/dotnet/articles/core/porting/index)
