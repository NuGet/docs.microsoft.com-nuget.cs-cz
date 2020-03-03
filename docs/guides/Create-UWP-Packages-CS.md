---
title: Vytvoření balíčků NuGet pro Univerzální platforma Windows
description: Ucelený návod k vytváření balíčků NuGet pomocí prostředí Windows Runtime komponenty pro Univerzální platforma Windows v C#.
author: rrelyea
ms.author: rrelyea
ms.date: 02/28/2020
ms.topic: tutorial
ms.openlocfilehash: 61f46f2623769927f881877cfe3f96132211b442
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231803"
---
# <a name="create-uwp-packages-c"></a>Vytvořit balíčky UWP (C#)

[Univerzální platforma Windows (UWP)](/windows/uwp) poskytuje běžnou aplikační platformu pro každé zařízení s Windows 10. V rámci tohoto modelu můžou aplikace pro UWP volat rozhraní API WinRT, která jsou společná pro všechna zařízení, a taky rozhraní API (včetně Win32 a .NET), která jsou specifická pro řadu zařízení, ve které je aplikace spuštěná.

V tomto návodu vytvoříte balíček NuGet s komponentou C# UWP (včetně ovládacího prvku XAML), který lze použít v spravovaných i nativních projektech.

## <a name="prerequisites"></a>Požadavky

1. Visual Studio 2019. Nainstalujte si bezplatnou edici 2019 Community Edition od [VisualStudio.com](https://www.visualstudio.com/); můžete použít i edice Professional a Enterprise.

1. Rozhraní příkazového řádku NuGet Stáhněte si nejnovější verzi `nuget.exe` z [NuGet.org/downloads](https://nuget.org/downloads)a uložte ji do umístění dle vašeho výběru (stažení je `.exe` přímo). Pak přidejte toto umístění do proměnné prostředí PATH, pokud ještě není. [Další podrobnosti](/nuget/reference/nuget-exe-cli-reference#windows).

## <a name="create-a-uwp-windows-runtime-component"></a>Vytvoření komponenty prostředí Windows Runtime UWP

1. V aplikaci Visual Studio zvolte **soubor > nový > projekt**, vyhledejte "UWP c#", vyberte šablonu **prostředí Windows Runtime komponenty (Universal Windows)** , klikněte na další, změňte název na ImageEnhancer a klikněte na vytvořit. Po zobrazení výzvy přijměte výchozí hodnoty pro cílovou verzi a minimální verzi.

    ![Vytváření nového projektu součásti prostředí Windows Runtime pro UWP](media/UWP-NewProject-CS.png)

1. Klikněte pravým tlačítkem na projekt v Průzkumník řešení, vyberte **přidat > novou položku**, vyberte **ovládací prvek s šablonou**, změňte název na AwesomeImageControl.cs a klikněte na **Přidat**:

    ![Přidání nové položky ovládacího prvku v šabloně XAML do projektu](media/UWP-NewXAMLControl-CS.png)

1. Klikněte pravým tlačítkem na projekt v Průzkumník řešení a vyberte **Vlastnosti.** Na stránce Vlastnosti klikněte na kartu **sestavení** a povolte **soubor dokumentace XML**:

    ![Nastavení generovat soubory dokumentace XML na Ano](media/UWP-GenerateXMLDocFiles-CS.png)

1. Klikněte pravým tlačítkem na *řešení* , vyberte **dávkové sestavení**, zaškrtněte pět polí sestavení v dialogovém okně, jak je znázorněno níže. Tím je zajištěno, že při sestavení vygenerujete úplnou sadu artefaktů pro každý cílový systém, který systém Windows podporuje.

    ![Dávkové sestavení](media/UWP-BatchBuild-CS.png)

1. V dialogovém okně dávkové sestavení a kliknutím na **sestavení** ověřte projekt a vytvořte výstupní soubory, které potřebujete pro balíček NuGet.

> [!Note]
> V tomto návodu použijete pro balíček artefakty ladění. V případě neladicího balíčku si místo toho v dialogovém okně dávkové sestavení vyhledejte možnosti vydání a podívejte se na výsledné složky verze v následujících krocích.

## <a name="create-and-update-the-nuspec-file"></a>Vytvoření a aktualizace souboru. nuspec

Chcete-li vytvořit počáteční soubor `.nuspec`, proveďte následující tři kroky. Následující části vás pak provede dalšími potřebnými aktualizacemi.

1. Otevřete příkazový řádek a přejděte do složky, která obsahuje `ImageEnhancer.csproj` (Toto je podsložka, ve které je soubor řešení).
1. Spusťte příkaz [`NuGet spec`](/nuget/reference/cli-reference/cli-ref-spec) , který vygeneruje `ImageEnhancer.nuspec` (název souboru se povede z názvu souboru `.csroj`):

    ```cli
    nuget spec
    ```

1. Otevřete `ImageEnhancer.nuspec` v editoru a aktualizujte ho tak, aby odpovídalo následujícímu, a nahraďte YOUR_NAME odpovídající hodnotou. Nenechávejte žádné z hodnot $propertyName $. Hodnota `<id>`, konkrétně, musí být jedinečná napříč nuget.org (podívejte se na zásady vytváření názvů popsané v tématu [Vytvoření balíčku](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)). Všimněte si také, že je nutné také aktualizovat značky Autor a popis, jinak se zobrazí chyba v průběhu balení.

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>ImageEnhancer.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>ImageEnhancer</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome Image Enhancer</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2020</copyright>
        <tags>image enhancer imageenhancer</tags>
        </metadata>
    </package>
    ```

> [!Note]
> Pro balíčky sestavené pro veřejnou spotřebu věnujte zvláštní pozornost prvku `<tags>`, protože tyto značky můžou ostatním najít váš balíček a pochopit, co dělá.

### <a name="adding-windows-metadata-to-the-package"></a>Přidávají se metadata Windows do balíčku.

Komponenta prostředí Windows Runtime vyžaduje metadata, která popisují všechny veřejně dostupné typy, což umožňuje ostatním aplikacím a knihovnám využívat součást. Tato metadata jsou obsažena v souboru WinMD, který je vytvořen při kompilování projektu a musí být součástí balíčku NuGet. Soubor XML s daty technologie IntelliSense je také sestaven současně a měl by být zahrnut také.

Přidejte následující `<files>` uzel do souboru `.nuspec`:

```xml
<package>
    <metadata>
        ...
    </metadata>

    <files>
        <!-- WinMd and IntelliSense files -->
      <file src="bin\Debug\ImageEnhancer.winmd" target="lib\uap10.0"/>
      <file src="bin\Debug\ImageEnhancer.xml" target="lib\uap10.0"/>
    </files>
</package>
```

### <a name="adding-xaml-content"></a>Přidání obsahu XAML

Chcete-li zahrnout ovládací prvek XAML do komponenty, je nutné přidat soubor XAML, který má výchozí šablonu pro ovládací prvek (jak je vygenerována šablonou projektu). To se taky doplní v části `<files>`:

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- XAML controls -->
        <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    </files>
</package>
```

### <a name="adding-the-native-implementation-libraries"></a>Přidání nativních implementačních knihoven

Základní logika typu ImageEnhancer je v rámci vaší komponenty v nativním kódu, který je obsažen v různých `ImageEnhancer.winmd` sestaveních, která jsou generována pro každý cílový modul runtime (ARM, ARM64, x86 a x64). Pokud je chcete zahrnout do balíčku, odkázat je v části `<files>` společně s přidruženými soubory prostředků. pri:

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- WINMDs and resources -->
      <file src="bin\ARM\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm"/>
      <file src="bin\ARM\Debug\ImageEnhancer.pri" target="runtimes\win10-arm"/>

      <file src="bin\ARM64\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm64"/>
      <file src="bin\ARM64\Debug\ImageEnhancer.pri" target="runtimes\win10-arm64"/>

      <file src="bin\x64\Debug\ImageEnhancer.winmd" target="runtimes\win10-x64"/>
      <file src="bin\x64\Debug\ImageEnhancer.pri" target="runtimes\win10-x64"/>

      <file src="bin\x86\Debug\ImageEnhancer.winmd" target="runtimes\win10-x86"/>
      <file src="bin\x86\Debug\ImageEnhancer.pri" target="runtimes\win10-x86"/>

    </files>
</package>
```

### <a name="final-nuspec"></a>Finální. nuspec

Konečný `.nuspec` soubor by teď měl vypadat nějak takto, kde se znovu YOUR_NAME by se měla nahradit příslušnou hodnotou:

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>ImageEnhancer.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>ImageEnhancer</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome Image Enhancer</description>
    <releaseNotes>First Release</releaseNotes>
    <copyright>Copyright 2020</copyright>
    <tags>image enhancer imageenhancer</tags>
    </metadata>
    <files>
    <!-- WinMd and IntelliSense -->
      <file src="bin\Debug\ImageEnhancer.winmd" target="lib\uap10.0"/>
      <file src="bin\Debug\ImageEnhancer.xml" target="lib\uap10.0"/>

    <!-- XAML controls -->
    <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    <!-- WINMDs and resources -->
      <file src="bin\ARM\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm"/>
      <file src="bin\ARM\Debug\ImageEnhancer.pri" target="runtimes\win10-arm"/>

      <file src="bin\ARM64\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm64"/>
      <file src="bin\ARM64\Debug\ImageEnhancer.pri" target="runtimes\win10-arm64"/>

      <file src="bin\x64\Debug\ImageEnhancer.winmd" target="runtimes\win10-x64"/>
      <file src="bin\x64\Debug\ImageEnhancer.pri" target="runtimes\win10-x64"/>

      <file src="bin\x86\Debug\ImageEnhancer.winmd" target="runtimes\win10-x86"/>
      <file src="bin\x86\Debug\ImageEnhancer.pri" target="runtimes\win10-x86"/>

    </files>
</package>
```

## <a name="package-the-component"></a>Zabalení komponenty

Po dokončení `.nuspec` odkazování na všechny soubory, které potřebujete zahrnout do balíčku, jste připraveni ke spuštění příkazu [`nuget pack`](/nuget/reference/cli-reference/cli-ref-pack) :

```cli
nuget pack ImageEnhancer.nuspec
```

Tím vygenerujete `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`. Tento soubor otevřete v nástroji jako [Průzkumník balíčků NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) a rozbalíte všechny uzly. zobrazí se následující obsah:

![Průzkumník balíčků NuGet zobrazující balíček ImageEnhancer](media/UWP-PackageExplorer.png)

> [!Tip]
> Soubor `.nupkg` je pouze soubor ZIP s jinou příponou. Můžete také prošetřit obsah balíčku, potom změnou `.nupkg` na `.zip`, ale nezapomeňte obnovit rozšíření před nahráním balíčku do nuget.org.

Pokud chcete balíček zpřístupnit ostatním vývojářům, postupujte podle pokynů v tématu [publikování balíčku](../nuget-org/publish-a-package.md).

## <a name="related-topics"></a>Příbuzná témata

- [Odkaz. nuspec](../reference/nuspec.md)
- [Balíčky symbolů](../create-packages/symbol-packages-snupkg.md)
- [Správa verzí balíčků](../concepts/package-versioning.md)
- [Podpora více verzí .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Zahrnutí vlastností MSBuild a cílů do balíčku](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Vytvoření lokalizovaných balíčků](../create-packages/creating-localized-packages.md)
