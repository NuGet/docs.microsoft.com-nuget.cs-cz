---
title: Vytvoření balíčků NuGet pro Xamarin (pro iOS, Android a Windows) pomocí Visual Studia 2017 nebo 2019
description: Komplexní návod k vytváření balíčků NuGet pro Xamarin, které používají nativní api v systémech iOS, Android a Windows.
author: karann-msft
ms.author: karann
ms.date: 11/05/2019
ms.topic: tutorial
ms.openlocfilehash: 0cb653bad9e853d908039b3f7a94e1dd7eefdde5
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "78230899"
---
# <a name="create-packages-for-xamarin-with-visual-studio-2017-or-2019"></a>Vytvoření balíčků pro Xamarin pomocí Visual Studia 2017 nebo 2019

Balíček pro Xamarin obsahuje kód, který používá nativní API v systémech iOS, Android a Windows, v závislosti na operačním systému run-time. I když je to jednoduché, je vhodnější nechat vývojáři využívat balíček z knihovny PCL nebo .NET Standard prostřednictvím společné oblasti plochy rozhraní API.

V tomto návodu pomocí Visual Studia 2017 nebo 2019 vytvoříte balíček NuGet pro různé platformy, který lze použít v mobilních projektech v systémech iOS, Android a Windows.

1. [Požadavky](#prerequisites)
1. [Vytvoření struktury projektu a kódu abstrakce](#create-the-project-structure-and-abstraction-code)
1. [Napište kód specifický pro platformu](#write-your-platform-specific-code)
1. [Vytvoření a aktualizace souboru Nuspec](#create-and-update-the-nuspec-file)
1. [Balení komponenty](#package-the-component)
1. [Příbuzná témata](#related-topics)

## <a name="prerequisites"></a>Požadavky

1. Visual Studio 2017 nebo 2019 s univerzální platformou Windows (UPW) a Xamarin. Nainstalujte edici Společenství zdarma od [visualstudio.com](https://www.visualstudio.com/); můžete použít professional a enterprise edice, samozřejmě. Chcete-li zahrnout nástroje UPW a Xamarin, vyberte vlastní instalaci a zkontrolujte příslušné možnosti.
1. NuGet CLI. Stáhněte si nejnovější verzi nuget.exe z [nuget.org/downloads](https://nuget.org/downloads)a uložte ji do zvoleného umístění. Pak přidejte toto umístění do proměnné prostředí PATH, pokud ještě není.

> [!Note]
> nuget.exe je samotný nástroj rozhraní příkazového příkazu, nikoli instalátor, takže nezapomeňte uložit stažený soubor z prohlížeče namísto jeho spuštění.

## <a name="create-the-project-structure-and-abstraction-code"></a>Vytvoření struktury projektu a kódu abstrakce

1. Stáhněte a spusťte rozšíření šablony [standardních pluginů .NET](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) pro různé platformy pro Visual Studio. Tyto šablony usnadní vytvoření potřebné struktury projektu pro tento návod.
1. V Sadě Visual Studio 2017 soubor > `Plugin`nový > **Project**, hledat , vyberte šablonu **modulu plug-in standardní knihovny napříč platformami .NET,** změňte název na LoggingLibrary a klikněte na OK.

    ![Nový projekt Aplikace Blank (Xamarin.Forms Portable) v VS 2017](media/CrossPlatform-NewProject.png)

    V Sadě Visual Studio 2019 soubor > `Plugin`nový > **Project**, hledat , vyberte šablonu **modulu plug-in standardní knihovny napříč platformami** a klikněte na Další.

    ![Nový projekt Blank App (Xamarin.Forms Portable) v VS 2019](media/CrossPlatform-NewProject19-Part1.png)

    Změňte název na LoggingLibrary a klikněte na Vytvořit.

    ![Nová konfigurace prázdné aplikace (Xamarin.Forms Portable) ve VS 2019](media/CrossPlatform-NewProject19-Part2.png)

Výsledné řešení obsahuje dva sdílené projekty spolu s řadou projektů specifických pro platformu:

- Projekt, `ILoggingLibrary` který je obsažen `ILoggingLibrary.shared.cs` v souboru, definuje veřejné rozhraní (oblast povrchu rozhraní API) komponenty. Zde definujete rozhraní knihovny.
- Druhý sdílený projekt obsahuje `CrossLoggingLibrary.shared.cs` kód, který vyhledá implementaci abstraktního rozhraní specifické pro platformu za běhu. Obvykle není nutné tento soubor upravovat.
- Projekty specifické pro platformu, jako je například `LoggingLibrary.android.cs`, `LoggingLibraryImplementation.cs` každý obsahuje nativní implementaci `LoggingLibrary.<PLATFORM>.cs` rozhraní v jejich příslušných (VS 2017) nebo (VS 2019) soubory. Toje místo, kde můžete vytvořit kód knihovny.

Ve výchozím nastavení ILoggingLibrary.shared.cs `ILoggingLibrary` soubor projektu obsahuje definici rozhraní, ale žádné metody. Pro účely tohoto návodu přidejte následující metodu: `Log`

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

## <a name="write-your-platform-specific-code"></a>Napište kód specifický pro platformu

Chcete-li implementovat implementaci `ILoggingLibrary` rozhraní a jeho metod pro konkrétní platformu, postupujte takto:

1. Otevřete `LoggingLibraryImplementation.cs` soubor (VS 2017) nebo `LoggingLibrary.<PLATFORM>.cs` (VS 2019) každého projektu platformy a přidejte potřebný kód. Například (pomocí `Android` projektu platformy):

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

1. Opakujte tuto implementaci v projektech pro každou platformu, kterou chcete podporovat.
1. Klikněte pravým tlačítkem myši na řešení a vyberte **sestavení řešení** zkontrolovat svou práci a vytvářet artefakty, které balíček další. Pokud se zobrazí chyby týkající se chybějících odkazů, klepněte pravým tlačítkem myši na řešení, vyberte **obnovit balíčky NuGet** k instalaci závislostí a znovu sestavit.

> [!Note]
> Pokud používáte Visual Studio 2019, před výběrem **obnovit nuget balíčky** a `MSBuild.Sdk.Extras` pokusu o opětovné sestavení, je třeba změnit verzi v `2.0.54` `LoggingLibrary.csproj`. K tomuto souboru lze přistupovat pouze prvním kliknutím pravým tlačítkem myši na projekt (pod řešením) a výběrem `Unload Project`, po kterém klepnete pravým tlačítkem myši na nezatížený projekt a vyberete . `Edit LoggingLibrary.csproj`

> [!Note]
> Chcete-li vytvořit pro iOS, potřebujete síťový Mac připojený k sadě Visual Studio, jak je popsáno v [úvodu k Xamarin.iOS pro Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/). Pokud mac nemáte k dispozici, zrušte výběr projektu iOS ve Správci konfigurace (krok 3 výše).

## <a name="create-and-update-the-nuspec-file"></a>Vytvoření a aktualizace souboru Nuspec

1. Otevřete příkazový řádek, `LoggingLibrary` přejděte do složky, `.sln` která je o jednu úroveň níže, kde je soubor, a spusťte příkaz NuGet `spec` a vytvořte počáteční `Package.nuspec` soubor:

    ```cli
    nuget spec
    ```

1. Přejmenujte tento `LoggingLibrary.nuspec` soubor na a otevřete jej v editoru.
1. Aktualizujte soubor tak, aby odpovídal následujícímu, a nahrazte YOUR_NAME příslušnou hodnotou. Hodnota, `<id>` konkrétně musí být jedinečný napříč nuget.org (viz konvence pojmenování popsané v [vytvoření balíčku).](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) Všimněte si také, že musíte také aktualizovat značky autora a popisu nebo se během kroku balení zobrazí chyba.

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
> Můžete příponu verze balíčku `-alpha` `-beta` s `-rc` aplikacemi , nebo označit balíček jako předběžnou verzi, zkontrolujte [předběžné verze](../create-packages/prerelease-packages.md) další informace o předběžných verzích.

### <a name="add-reference-assemblies"></a>Přidání referenčních sestavení

Chcete-li zahrnout referenční sestavení specifická pro `<files>` platformu, přidejte k prvku `LoggingLibrary.nuspec` podle potřeby pro podporované platformy následující:

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
> Chcete-li zkrátit názvy souborů DLL a XML, klepněte pravým tlačítkem myši na libovolný projekt, vyberte kartu **Knihovna** a změňte názvy sestavení.

### <a name="add-dependencies"></a>Přidání závislostí

Pokud máte specifické závislosti pro nativní `<dependencies>` implementace, `<group>` použijte element s prvky k jejich určení, například:

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

Například následující by nastavit iTextSharp jako závislost pro cíl UAP:

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a>Konečný .nuspec

Konečný `.nuspec` soubor by nyní měl vypadat takto, kde by měl být opět nahrazen YOUR_NAME příslušnou hodnotou:

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

## <a name="package-the-component"></a>Balení komponenty

S dokončeným `.nuspec` odkazováním na všechny soubory, které potřebujete zahrnout do `pack` balíčku, jste připraveni spustit příkaz:

```cli
nuget pack LoggingLibrary.nuspec
```

To bude `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`generovat . Otevření tohoto souboru v nástroji, jako je [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) a rozbalení všech uzlů, uvidíte následující obsah:

![NuGet Package Explorer zobrazující balíček LoggingLibrary](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> Soubor `.nupkg` je pouze soubor ZIP s jinou příponou. Můžete také prozkoumat obsah balíčku, `.nupkg` `.zip`pak změnou na , ale nezapomeňte obnovit rozšíření před odesláním balíček nuget.org.

Chcete-li balíček zpřístupnit ostatním [vývojářům,](../nuget-org/publish-a-package.md)postupujte podle pokynů k části Publikovat balíček .

## <a name="related-topics"></a>Související témata

- [Odkaz na nuspec](../reference/nuspec.md)
- [Balíčky symbolů](../create-packages/symbol-packages.md)
- [Správa verzí balíčku](../concepts/package-versioning.md)
- [Podpora více verzí rozhraní .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Zahrnout rekvizity a cíle MSBuild do balíčku](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Vytváření lokalizovaných balíčků](../create-packages/creating-localized-packages.md)
