---
title: Vytváření balíčků NuGet pro .NET Standard a .NET Framework pomocí sady Visual Studio 2015
description: Kompletní návod k vytváření .NET Standard a .NET Framework balíčků NuGet pomocí NuGet 3. x a Visual Studio 2015.
author: JonDouglas
ms.author: jodou
ms.date: 02/02/2018
ms.topic: tutorial
ms.openlocfilehash: d55228bbbd238d8930404ea52c5a80383bc9e0a3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774390"
---
# <a name="create-net-standard-and-net-framework-packages-with-visual-studio-2015"></a>Vytváření balíčků .NET Standard a .NET Framework pomocí sady Visual Studio 2015

**Poznámka:** Visual Studio 2017 se doporučuje pro vývoj .NET Standardch knihoven. Visual Studio 2015 může pracovat, ale nástroje .NET Core byly předáno pouze do stavu Preview. Podívejte se na téma [Vytvoření a publikování balíčku pomocí sady Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) pro práci s NuGet 4. x + a Visual Studio 2017.

[Knihovna .NET Standard](/dotnet/articles/standard/library) je formální specifikace rozhraní API .NET, která má být k dispozici ve všech modulech runtime .NET, což znamená větší jednotnost v ekosystému .NET. Knihovna .NET Standard definuje jednotnou sadu rozhraní API BCL (knihovny základních tříd) pro všechny platformy .NET, které mají být implementovány, nezávisle na zatížení. Umožňuje vývojářům vytvářet kód, který je použitelný napříč všemi moduly runtime technologie .NET, a snižuje, zda neeliminují direktivy podmíněné kompilace specifické pro platformu ve sdíleném kódu.

Tato příručka vás provede vytvořením balíčku NuGet, který cílí na .NET Standard knihovny 1,4 nebo zacílení balíčku .NET Framework 4,6. Knihovna .NET Standard 1,4 funguje napříč .NET Framework 4.6.1, Univerzální platforma Windows 10, .NET Core a mono/Xamarin. Podrobnosti najdete v [tabulce mapování .NET Standard](/dotnet/standard/net-standard#net-implementation-support) (dokumentace rozhraní .NET). Pokud chcete, můžete zvolit jinou verzi knihovny .NET Standard.

## <a name="prerequisites"></a>Požadavky

1. Visual Studio 2015 Update 3
1. (Jenom .NET Standard) [.NET Core SDK](https://www.microsoft.com/net/download/)
1. Rozhraní příkazového řádku NuGet Stáhněte si nejnovější verzi nuget.exe z [NuGet.org/downloads](https://nuget.org/downloads)a uložte ji do umístění dle vašeho výběru. Pak přidejte toto umístění do proměnné prostředí PATH, pokud ještě není.

    > [!Note]
    > nuget.exe je samotný nástroj rozhraní příkazového řádku, nikoli instalační program, proto je nutné stažený soubor uložit z prohlížeče místo jeho spuštění.

## <a name="create-the-class-library-project"></a>Vytvořit projekt knihovny tříd

1. V aplikaci Visual Studio, **soubor > nový > projektu**, rozbalte uzel **Visual C# > Windows** , vyberte možnost **Knihovna tříd (přenosná)**, změňte název na AppLogger a vyberte **OK**.

    ![Vytvořit nový projekt knihovny tříd](media/NetStandard-NewProject.png)

1. V dialogovém okně **Přidat přenosnou knihovnu tříd** , která se zobrazí, vyberte možnosti pro `.NET Framework 4.6` a `ASP.NET Core 1.0` . (Pokud cílíte .NET Framework, můžete vybrat, jaké možnosti jsou vhodné.)

1. Pokud cílíte .NET Standard, klikněte pravým tlačítkem na `AppLogger (Portable)` Průzkumník řešení, vyberte **vlastnosti**, vyberte kartu **Knihovna** a potom v části **cíle** vyberte **target .NET Platform Standard** . Tato akce vyzve k potvrzení, po kterém můžete `.NET Standard 1.4` z rozevírací nabídky vybrat (nebo jinou dostupnou verzi):

    ![Nastavení cíle na .NET Standard 1,4](media/NetStandard-ChangeTarget.png)

1. Klikněte na kartu **sestavení** , změňte **konfiguraci** na a `Release` zaškrtněte políčko **soubor dokumentace XML**.

1. Přidejte do komponenty kód, například:

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

1. Nastavte konfiguraci na vydanou verzi, sestavte projekt a ověřte, jestli se soubory DLL a XML vytvoří ve `bin\Release` složce.

## <a name="create-and-update-the-nuspec-file"></a>Vytvoření a aktualizace souboru. nuspec

1. Otevřete příkazový řádek, přejděte do složky obsahující `AppLogger.csproj` složku (jedna úroveň níže, kde `.sln` je soubor), a spuštěním `spec` příkazu NuGet vytvořte počáteční `AppLogger.nuspec` soubor:

    ```cli
    nuget spec
    ```

1. Otevřete `AppLogger.nuspec` v editoru a aktualizujte ho, aby odpovídal následujícímu, a nahraďte YOUR_NAME příslušnou hodnotou. `<id>`Hodnota konkrétně musí být jedinečná napříč NuGet.org (podívejte se na zásady vytváření názvů popsané v tématu [Vytvoření balíčku](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number). Všimněte si také, že je nutné také aktualizovat značky Autor a popis, jinak se zobrazí chyba v průběhu balení.

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

1. Přidejte do souboru referenční sestavení `.nuspec` , konkrétně knihovnu DLL knihovny a soubor XML IntelliSense:

    Pokud cílíte .NET Standard, zobrazí se podobné položky jako v následujícím příkladu:

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

    Pokud cílíte .NET Framework, zobrazí se podobné položky jako v následujícím příkladu:

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\net46\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\net46\AppLogger.xml" />
    </files>
    ```

1. Klikněte pravým tlačítkem na řešení a vyberte **Sestavit řešení** , aby se vygenerovaly všechny soubory balíčku.

### <a name="declaring-dependencies"></a>Deklarace závislostí

Pokud máte nějaké závislosti na jiných balíčcích NuGet, seznamte `<dependencies>` se s elementy v manifestu elementu `<group>` . Chcete-li například deklarovat závislost na NewtonSoft.Js8.0.3 nebo vyšší, přidejte následující:

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

Syntaxe atributu *Version* tady znamená, že je přijatelná verze 8.0.3 nebo vyšší. Pokud chcete zadat jiné rozsahy verzí, přečtěte si téma [Správa verzí balíčku](../concepts/package-versioning.md).

### <a name="adding-a-readme"></a>Přidání souboru Readme

Vytvořte `readme.txt` soubor, umístěte ho do kořenové složky projektu a pak na něj v `.nuspec` souboru použijte:

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

Sada Visual Studio `readme.txt` se zobrazí, když se balíček nainstaluje do projektu. Tento soubor se nezobrazuje při instalaci do projektů .NET Core nebo pro balíčky, které jsou nainstalované jako závislost.

## <a name="package-the-component"></a>Zabalení komponenty

Po dokončení `.nuspec` odkazů na všechny soubory, které potřebujete zahrnout do balíčku, jste připraveni spustit `pack` příkaz:

```cli
nuget pack AppLogger.nuspec
```

Tím vygenerujete `AppLogger.YOUR_NAME.1.0.0.nupkg` . Tento soubor otevřete v nástroji, jako je [Průzkumník balíčků NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) , a rozbalením všech uzlů se zobrazí následující obsah (zobrazený pro .NET Standard):

![Průzkumník balíčků NuGet zobrazující balíček AppLogger](media/NetStandard-PackageExplorer.png)

> [!Tip]
> `.nupkg`Soubor je pouze soubor zip s jinou příponou. Můžete také prošetřit obsah balíčku, potom změnou `.nupkg` na `.zip` , ale nezapomeňte obnovit rozšíření před nahráním balíčku do NuGet.org.

Pokud chcete balíček zpřístupnit ostatním vývojářům, postupujte podle pokynů v tématu [publikování balíčku](../nuget-org/publish-a-package.md).

Všimněte si, že `pack` vyžaduje mono 4.4.2 na Mac OS X a nefunguje v systémech Linux. Na Macu musíte také v souboru převést cesty Windows `.nuspec` na cesty ve stylu systému UNIX.

## <a name="related-topics"></a>Související témata

- [odkaz. nuspec](../reference/nuspec.md)
- [Podpora více verzí rozhraní .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Zahrnutí vlastností MSBuild a cílů do balíčku](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Vytvoření lokalizovaných balíčků](../create-packages/creating-localized-packages.md)
- [Balíčky symbolů](../create-packages/symbol-packages-snupkg.md)
- [Správa verzí balíčků](../concepts/package-versioning.md)
- [Dokumentace ke knihovně .NET Standard](/dotnet/articles/standard/library)
- [Přenos do .NET Core z .NET Framework](/dotnet/articles/core/porting/index)
