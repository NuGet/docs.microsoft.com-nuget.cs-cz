---
title: Vytváření balíčků NuGet pro Xamarin pomocí sady Visual Studio 2015 (pro iOS, Android a Windows)
description: Návod začátku do konce vytváření balíčků NuGet pro Xamarin pomocí nativních rozhraní API v iOS, Android a Windows.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: tutorial
ms.openlocfilehash: d737b70febd1e18aa8a39cc73a9a9cf333f758c6
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426844"
---
# <a name="create-packages-for-xamarin-with-visual-studio-2015"></a>Vytváření balíčků pro Xamarin pomocí sady Visual Studio 2015

Balíček pro Xamarin obsahuje kód, který používá nativní rozhraní API v iOS, Android a Windows, v závislosti na operačním systému za běhu. I když je to jednoduchý postup, je vhodnější umožňují vývojářům využívat balíček z PCL nebo plocha knihovny .NET Standard prostřednictvím společného rozhraní API.

V tomto názorném postupu, který používáte Visual Studio 2015 vytvořte balíček NuGet napříč platformami, která lze použít v mobilních projektů na iOS, Android a Windows.

1. [Požadavky](#prerequisites)
1. [Vytvoření projektu strukturu a abstrakce kódu](#create-the-project-structure-and-abstraction-code)
1. [Napište svůj kód specifický pro platformu](#write-your-platform-specific-code)
1. [Vytvoření a aktualizaci souboru .nuspec souboru](#create-and-update-the-nuspec-file)
1. [Balíček komponenty](#package-the-component)
1. [Související témata](#related-topics)

## <a name="prerequisites"></a>Požadavky

1. Visual Studio 2015 s platformou Universal Windows (UPW) a Xamarin. Instalace edice Community zdarma z [visualstudio.com](https://www.visualstudio.com/); samozřejmě můžete také, edice Professional a Enterprise. Aby byly nástroje pro UPW a Xamarin, vyberte vlastní instalaci a zkontrolujte příslušné možnosti.
1. Rozhraní příkazového řádku NuGet. Stažení nejnovější verze programu nuget.exe z [nuget.org/downloads](https://nuget.org/downloads), ukládání do umístění podle vašeho výběru. Pak přidejte toto umístění do proměnné prostředí PATH, pokud ještě není.

> [!Note]
> nuget.exe je že nástroj příkazového řádku, není instalační program, proto ji nezapomeňte Uložte stažený soubor ve svém prohlížeči místo jeho spuštění.

## <a name="create-the-project-structure-and-abstraction-code"></a>Vytvoření projektu strukturu a abstrakce kódu

1. Stáhněte a spusťte [modul plug-in pro rozšíření Xamarin šablony](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) pro sadu Visual Studio. Tyto šablony se usnadňují vytváření struktury projektu potřebné pro tento návod.
1. V sadě Visual Studio **soubor > Nový > projekt**, vyhledejte `Plugin`, vyberte **modul plug-in pro Xamarin** šablony, změňte název na LoggingLibrary a klikněte na tlačítko OK.

    ![Nový projekt prázdná aplikace (Xamarin.Forms přenosná) v sadě Visual Studio](media/CrossPlatform-NewProject.png)

Výsledný řešení obsahuje dva projekty PCL, spolu s celou řadu projektů specifické pro platformu:

- PCL s názvem `Plugin.LoggingLibrary.Abstractions (Portable)`, definuje veřejné rozhraní (svrchní oblasti rozhraní API) komponenty, v tomto případě `ILoggingLibrary` obsažené v souboru ILoggingLibrary.cs rozhraní. Toto je tady můžete definovat rozhraní do knihovny.
- Další PCL `Plugin.LoggingLibrary (Portable)`, obsahuje kód v CrossLoggingLibrary.cs, který bude vyhledávat konkrétní platformy implementaci abstraktní rozhraní v době běhu. Obvykle není nutné k úpravě tohoto souboru.
- Projekty konkrétní platformy, jako například `Plugin.LoggingLibrary.Android`každá obsahovat obsahovat nativní implementace rozhraní v jejich příslušných LoggingLibraryImplementation.cs soubory. To je, ve kterém sestavujete své knihovny kódu.

Ve výchozím souboru ILoggingLibrary.cs abstrakce projektu obsahuje definice rozhraní, ale žádné metody. Pro účely tohoto návodu, přidejte `Log` metodu následujícím způsobem:

```cs
using System;

namespace Plugin.LoggingLibrary.Abstractions
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

## <a name="write-your-platform-specific-code"></a>Napište svůj kód specifický pro platformu

K implementaci specifické pro platformu provádění `ILoggingLibrary` rozhraní a jeho metody, postupujte takto:

1. Otevřít `LoggingLibraryImplementation.cs` souboru pro každou platformu projektu a přidání nezbytného kódu. Příklad (použití `Plugin.LoggingLibrary.Android` projektu):

    ```cs
    using Plugin.LoggingLibrary.Abstractions;
    using System;

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

1. Tato implementace v projektech opakujte pro každou platformu, kterou chcete podporovat.
1. Klikněte pravým tlačítkem na projekt pro iOS, vyberte **vlastnosti**, klikněte na tlačítko **sestavení** kartu a odebrání "\iPhone" **výstupní cesta** a **soubor dokumentace XML**  nastavení. Toto platí jenom pro pohodlí dále v tomto názorném postupu. Po dokončení soubor uložte.
1. Klikněte pravým tlačítkem na řešení, vyberte **nástroje Configuration Manager...** a zkontrolujte **sestavení** polí PCLs a jednotlivé platformy, které podporujete.
1. Klikněte pravým tlačítkem na řešení a vyberte **sestavit řešení** zkontrolujte svou práci a vytvoří artefakty, které můžete dále balíček. Pokud se zobrazí chyby týkající se chybějící odkazy, klikněte pravým tlačítkem na řešení, vyberte **obnovit balíčky NuGet** instalace závislosti a sestavte znovu.

> [!Note]
> K vývoji pro iOS budete potřebovat síťově připojeného počítače Mac připojené k sadě Visual Studio, jak je popsáno v [Úvod k Xamarin.iosu pro Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/). Pokud nemáte k dispozici na Macu, zrušte zaškrtnutí políčka projektu pro iOS v configuration Manageru (krok 3 výše).

## <a name="create-and-update-the-nuspec-file"></a>Vytvoření a aktualizaci souboru .nuspec souboru

1. Otevřete příkazový řádek, přejděte na `LoggingLibrary` složku, která je jednu úroveň pod where `.sln` soubor a spusťte NuGet `spec` příkaz pro vytvoření počáteční `Package.nuspec` souboru:

    ```cli
    nuget spec
    ```

1. Přejmenujte tento soubor na `LoggingLibrary.nuspec` a otevřít ji v editoru.
1. Aktualizace souboru tak, aby odpovídala následující příkaz, nahradíte vaše_jméno odpovídající hodnotu. `<id>` , Konkrétně musí být hodnota jedinečná napříč nuget.org (naleznete v tématu Zásady vytváření názvů je popsáno v [vytvoření balíčku](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)). Všimněte si také, že budete muset taky aktualizovat Autor a popis značky nebo dojde k chybě během kroku balení.

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
        <copyright>Copyright 2016</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Tip]
> Můžete příponu verzi balíčku `-alpha`, `-beta` nebo `-rc` označit jako předběžné verze balíčku, zkontrolujte [předběžných verzí](../create-packages/prerelease-packages.md) Další informace o předběžných verzích.

### <a name="add-reference-assemblies"></a>Přidat odkaz na sestavení

Chcete-li zahrnout odkaz na konkrétní platformu sestavení, přidejte následující text do `<files>` prvek `LoggingLibrary.nuspec` odpovídajícím způsobem pro podporované platformy:

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
> Zkraťte názvy souborů knihovny DLL a XML, klikněte pravým tlačítkem na každého projektu, vyberte **knihovny** kartu a změnit názvy sestavení.

### <a name="add-dependencies"></a>Přidat závislosti

Pokud máte konkrétní závislosti pro nativní implementace, použijte `<dependencies>` element s `<group>` prvků, které mají být zadány, například:

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

Například následující byste nastavili iTextSharp jako závislost pro cíl UAP:

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a>Poslední souboru .nuspec

Výsledná `.nuspec` soubor by teď měl vypadat jako následující, kde znovu vaše_jméno by měla být nahrazena odpovídající hodnotu:

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
    <copyright>Copyright 2016</copyright>
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

## <a name="package-the-component"></a>Balíček komponenty

S dokončenou `.nuspec` odkazující na všechny soubory, které je potřeba zahrnout do balíčku, jste připraveni spustit `pack` příkaz:

```cli
nuget pack LoggingLibrary.nuspec
```

Tím se vygeneruje `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`. Tento soubor otevřete v nástroje, jako je [NuGet – Průzkumník balíčků](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) a rozšiřuje všechny uzly, viz následující obsah:

![Zobrazuje LoggingLibrary balíčku NuGet – Průzkumník balíčků](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> A `.nupkg` soubor je jenom soubor ZIP s jinou příponou. Můžete také prozkoumat obsah balíčku, potom změnou `.nupkg` k `.zip`, ale nezapomeňte k obnovení rozšíření před nahráním balíčků na nuget.org.

Aby váš balíček k dispozici s ostatními vývojáři, postupujte podle pokynů [publikování balíčku](../nuget-org/publish-a-package.md).

## <a name="related-topics"></a>Související témata

- [Odkaz na soubor Nuspec](../reference/nuspec.md)
- [Balíčky symbolů](../create-packages/symbol-packages.md)
- [Správa verzí balíčků](../reference/package-versioning.md)
- [Podpora více verzí rozhraní .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Včetně cíle a vlastnosti nástroje MSBuild v balíčku](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [Vytvoření lokalizovaných balíčků](../create-packages/creating-localized-packages.md)