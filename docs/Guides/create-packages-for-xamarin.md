---
title: "Vytvoření balíčků NuGet a platformy (pro iOS, Android a Windows) | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Návod začátku do konce vytváření balíčků NuGet pro Xamarin pomocí nativních rozhraní API pro iOS, Android a Windows."
keywords: "Vytvoření balíčku, balíčky pro Xamarin, balíčky a platformy"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 185a0e1e424d1ceb2d8bacbcc1502b38412c4c41
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/08/2018
---
# <a name="create-cross-platform-packages"></a>Vytváření balíčků a platformy

Napříč platformami balíček obsahuje kód, který používá nativních rozhraní API pro iOS, Android a Windows, v závislosti na spuštění operačního systému. Přestože je toto přehledné udělat, je vhodnější, aby mohli vývojáři využívat balíček PCL nebo .NET Standard knihovny prostřednictvím společné rozhraní API surface oblasti.

V tomto návodu vytvoříte balíček NuGet a platformy, který lze použít v mobilních projekty pro iOS, Android a Windows.

1. [Požadavky](#prerequisites)
1. [Vytvoření projektu strukturu a abstrakce kód](#create-the-project-structure-and-abstraction-code)
1. [Zadejte kód, podle platformy](#write-your-platform-specific-code)
1. [Vytvářet a aktualizovat soubor s příponou .nuspec](#create-and-update-the-nuspec-file)
1. [Balíček součásti](#package-the-component)
1. [Související témata](#related-topics)

## <a name="prerequisites"></a>Požadavky

1. Visual Studio 2015 se univerzální platformu Windows (UWP) a Xamarin. Instalaci edice Community zdarma z [visualstudio.com](https://www.visualstudio.com/); samozřejmě můžete taky edice Professional a Enterprise. Zahrnout nástroje pro UPW a Xamarin, vyberte vlastní instalaci a zkontrolujte příslušné možnosti.
1. Rozhraní příkazového řádku NuGet. Stáhněte si nejnovější verzi nuget.exe z [nuget.org/downloads](https://nuget.org/downloads), ukládání do umístění podle vaší volby. Pak přidejte tohoto umístění do vaší proměnné prostředí PATH, pokud již není.

> [!Note]
> nuget.exe je že nástroj příkazového řádku, není instalační program, takže je nutné z prohlížeče namísto spuštění ho uložte stažený soubor.

## <a name="create-the-project-structure-and-abstraction-code"></a>Vytvoření projektu strukturu a abstrakce kód

1. Stažení a spuštění [modul plug-in pro Xamarin šablony rozšíření](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) pro sadu Visual Studio. Tyto šablony snadno vytvořit strukturu nezbytné projektu pro účely tohoto postupu.
1. V sadě Visual Studio **soubor > Nový > projekt**, vyhledejte `Plugin`, vyberte **modul plug-in pro Xamarin** šablony, změňte název na LoggingLibrary a klikněte na tlačítko OK.

    ![Nový projekt prázdná aplikace (Xamarin.Forms přenositelností) v sadě Visual Studio](media/CrossPlatform-NewProject.png)

Výsledný řešení obsahuje dva projekty PCL, společně s celou řadu specifických pro platformy projekty:

- PCL s názvem `Plugin.LoggingLibrary.Abstractions (Portable)`, definuje veřejné rozhraní (prostor oblast rozhraní API) komponenty, v takovém případě `ILoggingLibrary` rozhraní obsažené v souboru ILoggingLibrary.cs. Toto je, kde můžete definovat rozhraní do knihovny.
- Další PCL `Plugin.LoggingLibrary (Portable)`, obsahuje kód v CrossLoggingLibrary.cs, který vyhledá specifické pro platformu implementaci abstraktní rozhraní za běhu. Obvykle nepotřebujete pro úpravu tohoto souboru.
- Specifické platformy projekty, například `Plugin.LoggingLibrary.Android`, každý obsahovat obsahovat nativní implementaci rozhraní ve svých příslušných LoggingLibraryImplementation.cs souborů. Toto je, kde vytvoříte na vaše knihovna kódu.

Ve výchozím nastavení soubor ILoggingLibrary.cs projektu abstrakce obsahuje definici rozhraní, ale žádné metody. Pro účely tohoto návodu, přidejte `Log` metoda následujícím způsobem:

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

## <a name="write-your-platform-specific-code"></a>Zadejte kód, podle platformy

K implementaci specifické pro platformu provádění `ILoggingLibrary` rozhraní a její metody, postupujte takto:

1. Otevřete `LoggingLibraryImplementation.cs` soubor pro každou platformu projektu a přidání nezbytného kódu. Například (pomocí `Plugin.LoggingLibrary.Android` projekt):

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
1. Klikněte pravým tlačítkem na projekt pro iOS, vyberte **vlastnosti**, klikněte na tlačítko **sestavení** a odeberte "\iPhone" z **výstupní cesta** a **souborů dokumentace XML**  nastavení. Toto platí jenom pro novější usnadnění práce v tomto návodu. Uložte soubor po dokončení.
1. Klikněte pravým tlačítkem na řešení, vyberte **nástroje Configuration Manager...** a zkontrolujte **sestavení** políček u PCLs a jednotlivé platformy, které podporujete.
1. Klikněte pravým tlačítkem na řešení a vyberte **sestavit řešení** ke kontrole práci a vytvoří artefakty, které další balíček. Pokud dojde k chybám o chybějícím odkazům, klikněte pravým tlačítkem na řešení, vyberte **obnovení balíčků NuGet** k instalaci závislosti a sestavte znovu.

> [!Note]
> K vytvoření pro iOS potřebujete síťově připojeného počítače Mac připojené k sadě Visual Studio, jak je popsáno na [Úvod do Xamarin.iOS pro sadu Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/). Pokud nemáte k dispozici Mac, zrušte projekt pro iOS v configuration Manageru (krok 3 výše).

## <a name="create-and-update-the-nuspec-file"></a>Vytvářet a aktualizovat soubor s příponou .nuspec

1. Otevřete příkazový řádek, přejděte na `LoggingLibrary` složky, která je jednu úroveň pod where `.sln` souboru a spusťte NuGet `spec` příkaz pro vytvoření počáteční `Package.nuspec` souboru:

```cli
nuget spec
```

1. Přejmenujte tento soubor do `LoggingLibrary.nuspec` a otevře ji v editoru.
1. Aktualizujte, aby se shodoval s následujícím, nahraďte vaše_jméno odpovídající hodnotu. `<id>` Hodnotu, konkrétně musí být jedinečný v rámci nuget.org (viz zásady vytváření názvů, které jsou popsané v [vytváření balíčku](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)). Všimněte si také, zda je nutné také aktualizovat autora a popis značky nebo dojde k chybě během kroku okolních.

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
> Můžete přípona vaší verzí balíčku `-alpha`, `-beta` nebo `-rc` označit jako předběžné verze vašeho balíčku, zkontrolujte [předprodejní verze](../create-packages/prerelease-packages.md) Další informace o předběžné verze.

### <a name="add-reference-assemblies"></a>Přidat odkaz na sestavení

Pokud chcete specifické pro platformu referenční sestavení, přidejte následující příkaz a `<files>` element `LoggingLibrary.nuspec` podle potřeby podporovaných platforem:

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
> Tak, aby zkrátil názvy souborů DLL a XML, klikněte pravým tlačítkem na jakékoli dané projekt, vyberte **knihovny** kartě a změnit názvy sestavení.

### <a name="add-dependencies"></a>Přidat závislosti

Pokud máte konkrétní závislosti pro nativní implementace, použijte `<dependencies>` element s `<group>` elementy, je třeba zadat:

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

### <a name="final-nuspec"></a>Poslední příponou .nuspec.

Váš koncový `.nuspec` soubor by měl nyní vypadat jako následující, kde znovu vaše_jméno by měla být nahrazená příslušnou hodnotu:

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

## <a name="package-the-component"></a>Balíček součásti

S dokončené `.nuspec` odkazující na všechny soubory, které je potřeba zahrnout do balíčku, jste připraveni ke spuštění `pack` příkaz:

```cli
nuget pack LoggingLibrary.nuspec
```

Tím se vygeneruje `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`. Otevření tohoto souboru v nástroje, jako [Explorer balíček NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) a rozšiřování všechny uzly, můžete zobrazit následující obsah:

![Průzkumník balíček NuGet zobrazující LoggingLibrary balíčku](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> A `.nupkg` soubor je právě soubor ZIP s jiné rozšíření. Můžete také zkontrolovat obsah balíčku, potom změnou `.nupkg` k `.zip`, ale nezapomeňte obnovit rozšíření před balíčku se nahrávají na nuget.org.

Pokud chcete zpřístupnit vašeho balíčku jinými vývojáři, postupujte podle pokynů [publikování balíčku](../create-packages/publish-a-package.md).

## <a name="related-topics"></a>Související témata

- [Odkaz na soubor Nuspec](../reference/nuspec.md)
- [Balíčky symbolů](../create-packages/symbol-packages.md)
- [Správa verzí balíčků](../reference/package-versioning.md)
- [Podpora více verzí rozhraní .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Včetně MSBuild props a cíle v balíčku](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [Vytvoření lokalizovaných balíčků](../create-packages/creating-localized-packages.md)