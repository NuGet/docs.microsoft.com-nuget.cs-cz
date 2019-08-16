---
title: Vytvoření balíčků NuGet pro Univerzální platforma Windows
description: Kompletní návod k vytváření balíčků NuGet pomocí prostředí Windows Runtime komponenty pro Univerzální platforma Windows.
author: karann-msft
ms.author: karann
ms.date: 03/21/2017
ms.topic: tutorial
ms.openlocfilehash: 1683349faacdf5ad47baafeef3457bbb3bb1baa9
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488990"
---
# <a name="create-uwp-packages"></a>Vytvoření balíčků UPW

[Univerzální platforma Windows (UWP)](https://developer.microsoft.com/windows) poskytuje běžnou aplikační platformu pro každé zařízení s Windows 10. V rámci tohoto modelu můžou aplikace pro UWP volat rozhraní API WinRT, která jsou společná pro všechna zařízení, a taky rozhraní API (včetně Win32 a .NET), která jsou specifická pro řadu zařízení, ve které je aplikace spuštěná.

V tomto návodu vytvoříte balíček NuGet s nativní komponentou UWP (včetně ovládacího prvku XAML), který lze použít v spravovaných i nativních projektech.

## <a name="prerequisites"></a>Požadavky

1. Visual Studio 2017 nebo Visual Studio 2015. Nainstalujte si bezplatnou edici 2017 Community Edition od [VisualStudio.com](https://www.visualstudio.com/); můžete použít i edice Professional a Enterprise.

1. Rozhraní příkazového řádku NuGet Stáhněte si nejnovější verzi `nuget.exe` z [NuGet.org/downloads](https://nuget.org/downloads)a uložte ji do umístění dle vašeho výběru (stažení je `.exe` přímo). Pak přidejte toto umístění do proměnné prostředí PATH, pokud ještě není.

## <a name="create-a-uwp-windows-runtime-component"></a>Vytvoření komponenty prostředí Windows Runtime UWP

1. V aplikaci Visual Studio zvolte **soubor > nový > projekt**, rozbalte položku **Visual C++ > Windows > univerzální** uzel, vyberte šablonu **prostředí Windows Runtime součásti (Universal Windows)** , změňte název na ImageEnhancer a klikněte na OK. Po zobrazení výzvy přijměte výchozí hodnoty pro cílovou verzi a minimální verzi.

    ![Vytváření nového projektu součásti prostředí Windows Runtime pro UWP](media/UWP-NewProject.png)

1. Klikněte pravým tlačítkem na projekt v Průzkumník řešení, vyberte **přidat > novou položku**, klikněte na uzel **Visual C++ > XAML** , vyberte **ovládací prvek**s šablonou, změňte název na AwesomeImageControl. cpp a klikněte na tlačítko **Přidat**:

    ![Přidání nové položky ovládacího prvku v šabloně XAML do projektu](media/UWP-NewXAMLControl.png)

1. Klikněte pravým tlačítkem na projekt v Průzkumník řešení a vyberte **Vlastnosti.** Na stránce Vlastnosti rozbalte položku **Vlastnosti konfigurace > CC++ /** a klikněte na možnost **výstupní soubory**. V pravém podokně změňte hodnotu pro **Generovat soubory dokumentace XML** na Ano:

    ![Nastavení generovat soubory dokumentace XML na Ano](media/UWP-GenerateXMLDocFiles.png)

1. Klikněte pravým tlačítkem na *řešení* , vyberte **dávkové sestavení**a zaškrtněte tři pole pro ladění v dialogovém okně, jak je znázorněno níže. Tím je zajištěno, že při sestavení vygenerujete úplnou sadu artefaktů pro každý cílový systém, který systém Windows podporuje.

    ![Dávkové sestavení](media/UWP-BatchBuild.png)

1. V dialogovém okně dávkové sestavení a kliknutím na **sestavení** ověřte projekt a vytvořte výstupní soubory, které potřebujete pro balíček NuGet.

> [!Note]
> V tomto návodu použijete pro balíček artefakty ladění. V případě neladicího balíčku si místo toho v dialogovém okně dávkové sestavení vyhledejte možnosti vydání a podívejte se na výsledné složky verze v následujících krocích.

## <a name="create-and-update-the-nuspec-file"></a>Vytvoření a aktualizace souboru. nuspec

Chcete-li vytvořit `.nuspec` počáteční soubor, proveďte následující tři kroky. Následující části vás pak provede dalšími potřebnými aktualizacemi.

1. Otevřete příkazový řádek a přejděte do složky, která obsahuje `ImageEnhancer.vcxproj` (Toto je podsložka, ve které je soubor řešení).
1. Spusťte příkaz NuGet `spec` , který se `ImageEnhancer.nuspec` má vygenerovat (název souboru se povede `.vcxproj` z názvu souboru):

    ```cli
    nuget spec
    ```

1. Otevřete `ImageEnhancer.nuspec` v editoru a aktualizujte ho, aby odpovídal následujícímu, a nahraďte YOUR_NAME příslušnou hodnotou. Hodnota konkrétně musí být jedinečná napříč NuGet.org (podívejte se na zásady vytváření názvů popsané v tématu [Vytvoření balíčku).](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) `<id>` Všimněte si také, že je nutné také aktualizovat značky Autor a popis, jinak se zobrazí chyba v průběhu balení.

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
        <copyright>Copyright 2016</copyright>
        <tags>image enhancer imageenhancer</tags>
        </metadata>
    </package>
    ```

> [!Note]
> Pro balíčky sestavené pro veřejnou spotřebu věnujte zvláštní pozornost `<tags>` prvku, protože tyto značky můžou ostatním uživatelům najít váš balíček a pochopit, co to dělá.

### <a name="adding-windows-metadata-to-the-package"></a>Přidávají se metadata Windows do balíčku.

Komponenta prostředí Windows Runtime vyžaduje metadata, která popisují všechny veřejně dostupné typy, což umožňuje ostatním aplikacím a knihovnám využívat součást. Tato metadata jsou obsažena v souboru WinMD, který je vytvořen při kompilování projektu a musí být součástí balíčku NuGet. Soubor XML s daty technologie IntelliSense je také sestaven současně a měl by být zahrnut také.

`<files>` Přidejte`.nuspec` do souboru následující uzel:

```xml
<package>
    <metadata>
        ...
    </metadata>

    <files>
        <!-- WinMd and IntelliSense files -->
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.winmd" target="lib\uap10.0"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.xml" target="lib\uap10.0"/>
    </files>
</package>
```

### <a name="adding-xaml-content"></a>Přidání obsahu XAML

Chcete-li zahrnout ovládací prvek XAML do komponenty, je nutné přidat soubor XAML, který má výchozí šablonu pro ovládací prvek (jak je vygenerována šablonou projektu). To se `<files>` taky doplní v části:

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

V rámci vaší komponenty je základní logika typu ImageEnhancer v nativním kódu, který je obsažen v různých `ImageEnhancer.dll` sestaveních, která jsou generována pro každý cílový modul runtime (ARM, x86 a x64). Pokud je chcete zahrnout do balíčku, odkázat je v `<files>` části spolu s jejich přidruženými zdrojovými soubory. pri:

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- DLLs and resources -->
        <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm\native"/>
        <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm\native"/>

        <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm64\native"/>
        <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm64\native"/>

        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>

        <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    </files>
</package>
```

### <a name="adding-targets"></a>Přidávání cílů

V dalších C++ a v projektech JavaScriptu, které mohou spotřebovat váš balíček NuGet, potřebuje soubor. targets k identifikaci potřebných sestavení a souborů winmd. (C# a Visual Basic projekty automaticky.) Vytvořte tento soubor zkopírováním textu níže do `ImageEnhancer.targets` a uložte ho do stejné složky, ve které je `.nuspec` soubor. _Poznámka:_ Tento `.targets` soubor musí mít stejný název jako ID balíčku (např `<Id>` . element v `.nupspec` souboru):

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <PropertyGroup>
        <ImageEnhancer-Platform Condition="'$(Platform)' == 'Win32'">x86</ImageEnhancer-Platform>
        <ImageEnhancer-Platform Condition="'$(Platform)' != 'Win32'">$(Platform)</ImageEnhancer-Platform>
    </PropertyGroup>
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Reference Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0\ImageEnhancer.winmd">
            <Implementation>ImageEnhancer.dll</Implementation>
        </Reference>
    <ReferenceCopyLocalPaths Include="$(MSBuildThisFileDirectory)..\..\runtimes\win10-$(ImageEnhancer-Platform)\native\ImageEnhancer.dll" />
    </ItemGroup>
</Project>
```

Pak se podívejte `ImageEnhancer.targets` na téma `.nuspec` v souboru:

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- .targets -->
        <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

### <a name="final-nuspec"></a>Finální. nuspec

Konečný `.nuspec` soubor by teď měl vypadat nějak takto, kde znovu YOUR_NAME by mělo být nahrazeno příslušnou hodnotou:

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
    <copyright>Copyright 2016</copyright>
    <tags>image enhancer imageenhancer</tags>
    </metadata>
    <files>
    <!-- WinMd and IntelliSense -->
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.winmd" target="lib\uap10.0"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.xml" target="lib\uap10.0"/>

    <!-- XAML controls -->
    <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    <!-- DLLs and resources -->
    <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm\native"/>
    <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm\native"/>
    <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm64\native"/>
    <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm64\native"/>     
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    <!-- .targets -->
    <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

## <a name="package-the-component"></a>Zabalení komponenty

Po dokončení `.nuspec` odkazů na všechny soubory, které potřebujete zahrnout do balíčku, jste připraveni `pack` spustit příkaz:

```cli
nuget pack ImageEnhancer.nuspec
```

Tím vygenerujete `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`. Tento soubor otevřete v nástroji jako [Průzkumník balíčků NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) a rozbalíte všechny uzly. zobrazí se následující obsah:

![Průzkumník balíčků NuGet zobrazující balíček ImageEnhancer](media/UWP-PackageExplorer.png)

> [!Tip]
> `.nupkg` Soubor je pouze soubor zip s jinou příponou. Můžete také prošetřit obsah balíčku, potom změnou `.nupkg` na `.zip`, ale nezapomeňte obnovit rozšíření před nahráním balíčku do NuGet.org.

Pokud chcete balíček zpřístupnit ostatním vývojářům, postupujte podle pokynů v tématu [publikování balíčku](../nuget-org/publish-a-package.md).

## <a name="related-topics"></a>Související témata

- [Odkaz. nuspec](../reference/nuspec.md)
- [Balíčky symbolů](../create-packages/symbol-packages.md)
- [Správa verzí balíčků](../concepts/package-versioning.md)
- [Podpora více verzí .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Zahrnutí vlastností MSBuild a cílů do balíčku](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Vytvoření lokalizovaných balíčků](../create-packages/creating-localized-packages.md)
