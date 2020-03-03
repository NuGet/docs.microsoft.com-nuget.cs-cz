---
title: Vytváření balíčků NuGet pro Xamarin (pro iOS, Android a Windows) pomocí sady Visual Studio 2017 nebo 2019
description: Ucelený návod k vytváření balíčků NuGet pro Xamarin, který používá nativní rozhraní API pro iOS, Android a Windows.
author: karann-msft
ms.author: karann
ms.date: 11/05/2019
ms.topic: tutorial
ms.openlocfilehash: 0cb653bad9e853d908039b3f7a94e1dd7eefdde5
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230899"
---
# <a name="create-packages-for-xamarin-with-visual-studio-2017-or-2019"></a>Vytváření balíčků pro Xamarin pomocí sady Visual Studio 2017 nebo 2019

Balíček pro Xamarin obsahuje kód, který používá nativní rozhraní API v systémech iOS, Android a Windows v závislosti na operačním systému za běhu. I když je to jednoduché, je vhodnější dát vývojářům využívání tohoto balíčku z knihovny PCL nebo .NET Standard pomocí běžné oblasti rozhraní API.

V tomto návodu použijete Visual Studio 2017 nebo 2019 k vytvoření balíčku NuGet pro různé platformy, který se dá použít v mobilních projektech pro iOS, Android a Windows.

1. [Požadavky](#prerequisites)
1. [Vytvoření struktury projektu a kódu abstrakce](#create-the-project-structure-and-abstraction-code)
1. [Psaní kódu specifického pro platformu](#write-your-platform-specific-code)
1. [Vytvoření a aktualizace souboru. nuspec](#create-and-update-the-nuspec-file)
1. [Zabalení komponenty](#package-the-component)
1. [Příbuzná témata](#related-topics)

## <a name="prerequisites"></a>Požadavky

1. Visual Studio 2017 nebo 2019 s Univerzální platforma Windows (UWP) a Xamarin. Nainstalujte si od verze Community Edition zdarma od [VisualStudio.com](https://www.visualstudio.com/); Samozřejmě můžete používat i edice Professional a Enterprise. Chcete-li zahrnout nástroje UWP a Xamarin, vyberte vlastní instalaci a ověřte příslušné možnosti.
1. Rozhraní příkazového řádku NuGet Stáhněte si nejnovější verzi nástroje NuGet. exe z [NuGet.org/downloads](https://nuget.org/downloads)a uložte ji do umístění podle vašeho výběru. Pak přidejte toto umístění do proměnné prostředí PATH, pokud ještě není.

> [!Note]
> NuGet. exe je samotný nástroj rozhraní příkazového řádku, nikoli instalační program, proto uložte stažený soubor z prohlížeče namísto jeho spuštění.

## <a name="create-the-project-structure-and-abstraction-code"></a>Vytvoření struktury projektu a kódu abstrakce

1. Stáhněte a spusťte [rozšíření šablon modulu plug-in .NET Standard pro různé platformy](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) pro Visual Studio. Tyto šablony usnadňují vytváření potřebných struktur projektu pro tento návod.
1. V aplikaci Visual Studio 2017, **soubor > nový > projektu**, vyhledejte `Plugin`, vyberte šablonu **modulu plug-in knihovny .NET Standard pro různé platformy** , změňte název na LoggingLibrary a klikněte na OK.

    ![Nový prázdný projekt aplikace (Xamarin. Forms Portable) v sadě VS 2017](media/CrossPlatform-NewProject.png)

    V aplikaci Visual Studio 2019, **soubor > nový > projektu**, vyhledejte `Plugin`, vyberte šablonu **modulu plug-in knihovny .NET Standard pro různé platformy** a klikněte na další.

    ![Nový prázdný projekt aplikace (Xamarin. Forms Portable) v sadě VS 2019](media/CrossPlatform-NewProject19-Part1.png)

    Změňte název na LoggingLibrary a klikněte na vytvořit.

    ![Nová prázdná konfigurace aplikace (Xamarin. Forms Portable) ve VS 2019](media/CrossPlatform-NewProject19-Part2.png)

Výsledné řešení obsahuje dva sdílené projekty společně s nejrůznějšími projekty pro konkrétní platformy:

- `ILoggingLibrary` projekt, který je obsažen v souboru `ILoggingLibrary.shared.cs`, definuje veřejné rozhraní (oblast rozhraní API) komponenty. Toto je místo, kde definujete rozhraní do knihovny.
- Druhý sdílený projekt obsahuje kód v `CrossLoggingLibrary.shared.cs`, který v době běhu najde implementaci abstraktního rozhraní specifickou pro konkrétní platformu. Tento soubor obvykle nemusíte měnit.
- Projekty specifické pro platformu, například `LoggingLibrary.android.cs`, obsahují nativní implementaci rozhraní v příslušných `LoggingLibraryImplementation.cs` (VS 2017) nebo `LoggingLibrary.<PLATFORM>.cs` (VS 2019) soubory. Tady můžete sestavit kód vaší knihovny.

Ve výchozím nastavení soubor ILoggingLibrary.shared.cs projektu `ILoggingLibrary` obsahuje definici rozhraní, ale žádné metody. Pro účely tohoto návodu přidejte `Log` metodu následujícím způsobem:

```cs
using System;
using System.Collections.Generic;
using System.Text;

namespace Plugin.LoggingLibrary
{
    /// <summary>
    /// Interface for LoggingLibrary
    /// </summary>
    public interface ILoggingLibrary
    {
        /// <summary>
        /// Log a message
        /// </summary>
        void Log(string text);
    }
}
```

## <a name="write-your-platform-specific-code"></a>Psaní kódu specifického pro platformu

Chcete-li implementovat implementaci rozhraní `ILoggingLibrary` specifického pro platformu a jeho metody, postupujte následovně:

1. Otevřete soubor `LoggingLibraryImplementation.cs` (VS 2017) nebo `LoggingLibrary.<PLATFORM>.cs` (VS 2019) pro každý projekt platformy a přidejte potřebný kód. Například (použití projektu platformy `Android`):

    ```cs
    using System;
    using System.Collections.Generic;
    using System.Text;

    namespace Plugin.LoggingLibrary
    {
        /// <summary>
        /// Implementation for Feature
        /// </summary>
        public class LoggingLibraryImplementation : ILoggingLibrary
        {
            /// <summary>
            /// Log a message
            /// </summary>
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log on Android");
            }
        }
    }
    ```

1. Tuto implementaci opakujte v projektech pro každou platformu, kterou chcete podporovat.
1. Klikněte pravým tlačítkem na řešení a vyberte **Sestavit řešení** , abyste zkontrolovali práci a vytvořili artefakty, které zabalíte jako další. Pokud se zobrazí chybové zprávy o chybějících odkazech, klikněte pravým tlačítkem na řešení, vyberte možnost **obnovit balíčky NuGet** a nainstalujte závislosti a znovu sestavte.

> [!Note]
> Pokud používáte sadu Visual Studio 2019, před výběrem možnosti **obnovit balíčky NuGet** a pokusem o opětovné sestavení je třeba změnit verzi `MSBuild.Sdk.Extras` na `2.0.54` v `LoggingLibrary.csproj`. K tomuto souboru se dá dostat jenom tak, že nejdřív kliknete pravým tlačítkem myši na projekt (pod řešením) a vyberete `Unload Project`, po kterém kliknete pravým tlačítkem na nenačtený projekt a vyberete `Edit LoggingLibrary.csproj`.

> [!Note]
> Pro sestavení pro iOS budete potřebovat síťovou adresu MAC připojenou k Visual Studiu, jak je popsáno v tématu [Úvod do Xamarin. iOS pro Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/). Pokud nemáte k dispozici počítač Mac, vymažte projekt iOS v nástroji Configuration Manager (krok 3 výše).

## <a name="create-and-update-the-nuspec-file"></a>Vytvoření a aktualizace souboru. nuspec

1. Otevřete příkazový řádek, přejděte do složky `LoggingLibrary`, která představuje jednu úroveň níže, kde je `.sln` soubor, a spuštěním příkazu NuGet `spec` vytvořte počáteční soubor `Package.nuspec`:

    ```cli
    nuget spec
    ```

1. Přejmenujte tento soubor na `LoggingLibrary.nuspec` a otevřete ho v editoru.
1. Aktualizujte soubor tak, aby odpovídal následujícímu, nahraďte YOUR_NAME příslušnou hodnotou. Hodnota `<id>`, konkrétně, musí být jedinečná napříč nuget.org (podívejte se na zásady vytváření názvů popsané v tématu [Vytvoření balíčku](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)). Všimněte si také, že je nutné také aktualizovat značky Autor a popis, jinak se zobrazí chyba v průběhu balení.

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>LoggingLibrary.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>LoggingLibrary</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2018</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Tip]
> Verzi balíčku můžete příponou `-alpha`, `-beta` nebo `-rc` Pokud chcete balíček označit jako předběžnou verzi, Projděte si [předběžné verze verzí](../create-packages/prerelease-packages.md) , kde najdete další informace o předběžných verzích.

### <a name="add-reference-assemblies"></a>Přidat referenční sestavení

Chcete-li zahrnout referenční sestavení specifická pro platformu, přidejte následující prvky do `<files>`ho prvku `LoggingLibrary.nuspec` podle potřeby pro podporované platformy:

```xml
<!-- Insert below <metadata> element -->
<files>
    <!-- Cross-platform reference assemblies -->
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

    <!-- iOS reference assemblies -->
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

    <!-- Android reference assemblies -->
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

    <!-- UWP reference assemblies -->
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
</files>
```

> [!Note]
> Chcete-li zkrátit názvy knihoven DLL a souborů XML, klikněte pravým tlačítkem na libovolný daný projekt, vyberte kartu **Knihovna** a změňte názvy sestavení.

### <a name="add-dependencies"></a>Přidat závislosti

Máte-li specifické závislosti pro nativní implementace, použijte prvek `<dependencies>` s `<group>` prvky pro jejich určení, například:

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="MonoAndroid">
        <!--MonoAndroid dependencies go here-->
    </group>
    <group targetFramework="Xamarin.iOS10">
        <!--Xamarin.iOS10 dependencies go here-->
    </group>
    <group targetFramework="uap">
        <!--uap dependencies go here-->
    </group>
</dependencies>
```

Následující příklad by nastavil iTextSharp jako závislost pro cíl UAP:

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a>Finální. nuspec

Konečný `.nuspec` soubor by teď měl vypadat nějak takto, kde se znovu YOUR_NAME by se měla nahradit příslušnou hodnotou:

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>LoggingLibrary.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>LoggingLibrary</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome application logging utility</description>
    <releaseNotes>First release</releaseNotes>
    <copyright>Copyright 2018</copyright>
    <tags>logger logging logs</tags>
        <dependencies>
        <group targetFramework="MonoAndroid">
            <!--MonoAndroid dependencies go here-->
        </group>
        <group targetFramework="Xamarin.iOS10">
            <!--Xamarin.iOS10 dependencies go here-->
        </group>
        <group targetFramework="uap">
            <dependency id="iTextSharp" version="5.5.9" />
        </group>
    </dependencies>
    </metadata>
    <files>
        <!-- Cross-platform reference assemblies -->
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

        <!-- iOS reference assemblies -->
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

        <!-- Android reference assemblies -->
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

        <!-- UWP reference assemblies -->
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
    </files>
</package>
```

## <a name="package-the-component"></a>Zabalení komponenty

Po dokončení `.nuspec` odkazování na všechny soubory, které potřebujete zahrnout do balíčku, jste připraveni ke spuštění příkazu `pack`:

```cli
nuget pack LoggingLibrary.nuspec
```

Tím se vygeneruje `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`. Tento soubor otevřete v nástroji jako [Průzkumník balíčků NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) a rozbalíte všechny uzly. zobrazí se následující obsah:

![Průzkumník balíčků NuGet zobrazující balíček LoggingLibrary](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> Soubor `.nupkg` je pouze soubor ZIP s jinou příponou. Můžete také prošetřit obsah balíčku, potom změnou `.nupkg` na `.zip`, ale nezapomeňte obnovit rozšíření před nahráním balíčku do nuget.org.

Pokud chcete balíček zpřístupnit ostatním vývojářům, postupujte podle pokynů v tématu [publikování balíčku](../nuget-org/publish-a-package.md).

## <a name="related-topics"></a>Příbuzná témata

- [Odkaz na nuspec](../reference/nuspec.md)
- [Balíčky symbolů](../create-packages/symbol-packages.md)
- [Správa verzí balíčků](../concepts/package-versioning.md)
- [Podpora více verzí .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Zahrnutí vlastností MSBuild a cílů do balíčku](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Vytvoření lokalizovaných balíčků](../create-packages/creating-localized-packages.md)
