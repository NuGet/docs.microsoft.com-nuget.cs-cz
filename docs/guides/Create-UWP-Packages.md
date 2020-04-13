---
title: Vytvoření balíčků NuGet pro univerzální platformu Windows
description: Komplexní návod k vytváření balíčků NuGet pomocí součásti prostředí Windows Runtime pro univerzální platformu Windows.
author: karann-msft
ms.author: karann
ms.date: 03/21/2017
ms.topic: tutorial
ms.openlocfilehash: 77aa186291122a8d05018ecacd1329da459badad
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "72380753"
---
# <a name="create-uwp-packages"></a>Vytvoření balíčků UPW

[Univerzální platforma Windows (UPW)](https://developer.microsoft.com/windows) poskytuje společnou platformu aplikací pro každé zařízení se systémem Windows 10. V rámci tohoto modelu mohou aplikace UPW volat rozhraní API WinRT, která jsou společná pro všechna zařízení, a také rozhraní API (včetně Win32 a .NET), která jsou specifická pro rodinu zařízení, na které je aplikace spuštěna.

V tomto návodu vytvoříte balíček NuGet s nativní komponentou UPW (včetně ovládacího prvku XAML), který lze použít v řízených i nativních projektech.

## <a name="prerequisites"></a>Požadavky

1. Visual Studio 2017 nebo Visual Studio 2015. Nainstalujte 2017 Community edition zdarma od [visualstudio.com](https://www.visualstudio.com/); můžete také použít edice Professional a Enterprise.

1. NuGet CLI. Stáhněte si `nuget.exe` nejnovější verzi z [nuget.org/downloads](https://nuget.org/downloads)a uložte ji na `.exe` místo podle vašeho výběru (stahování je přímo). Pak přidejte toto umístění do proměnné prostředí PATH, pokud ještě není.

## <a name="create-a-uwp-windows-runtime-component"></a>Vytvoření součásti runtime systému Windows v programu UPW

1. V sadě Visual Studio zvolte **Soubor > Nový > Project**, rozbalte uzel Visual **C++ > Windows > Universal,** vyberte šablonu **komponenty Prostředí Windows Runtime (Universal Windows),** změňte název na ImageEnhancer a klepněte na OK. Po zobrazení výzvy přijměte výchozí hodnoty pro cílovou a minimální verzi.

    ![Vytvoření nového projektu komponenty runtime systému Windows UWP](media/UWP-NewProject.png)

1. Klepněte pravým tlačítkem myši na projekt v Průzkumníku řešení, vyberte **Přidat > novou položku**, klepněte na uzel **XAML v jazyc >e Visual C++,** vyberte **položku Templated Control**, změňte název na AwesomeImageControl.cpp a klepněte na **přidat**:

    ![Přidání nové položky ovládacího prvku šablony XAML do projektu](media/UWP-NewXAMLControl.png)

1. Klikněte pravým tlačítkem myši na projekt v Průzkumníku řešení a vyberte **Vlastnosti.** Na stránce Vlastnosti **rozbalte položku Vlastnosti konfigurace > C/C++** a klepněte na **příkaz Výstupní soubory**. V podokně vpravo změňte hodnotu **pro Generovat soubory dokumentace XML** na Ano:

    ![Nastavení generování souborů dokumentace XML na ano](media/UWP-GenerateXMLDocFiles.png)

1. Klikněte pravým tlačítkem myši na *řešení,* vyberte **Dávkové sestavení**, zaškrtněte tři pole ladění v dialogovém okně, jak je znázorněno níže. Tím zajistíte, že při vytváření sestavení vygenerujete úplnou sadu artefaktů pro každý z cílových systémů, které systém Windows podporuje.

    ![Dávkové sestavení](media/UWP-BatchBuild.png)

1. V dialogovém okně Dávkové sestavení a klepněte na tlačítko **Sestavit,** chcete-li ověřit projekt a vytvořit výstupní soubory, které potřebujete pro balíček NuGet.

> [!Note]
> V tomto návodu použijete artefakty ladění pro balíček. U balíčku bez ladění zkontrolujte možnosti vydání v dialogovém okně Dávkové sestavení a v následujících krocích se podívejte na výsledné složky release.

## <a name="create-and-update-the-nuspec-file"></a>Vytvoření a aktualizace souboru Nuspec

Chcete-li `.nuspec` vytvořit počáteční soubor, proveďte následující tři kroky. Následující části vás pak provedou dalšími nezbytnými aktualizacemi.

1. Otevřete příkazový řádek a přejděte do složky obsahující `ImageEnhancer.vcxproj` (bude to podsložka pod místem, kde je soubor řešení).
1. Spusťte `spec` příkaz NuGet pro generování `ImageEnhancer.nuspec` (název souboru je `.vcxproj` převzat z názvu souboru):

    ```cli
    nuget spec
    ```

1. Otevřete `ImageEnhancer.nuspec` v editoru a aktualizujte jej tak, aby odpovídal následujícímu, a nahrazují YOUR_NAME příslušnou hodnotou. Hodnota, `<id>` konkrétně musí být jedinečný napříč nuget.org (viz konvence pojmenování popsané v [vytvoření balíčku).](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) Všimněte si také, že musíte také aktualizovat značky autora a popisu nebo se během kroku balení zobrazí chyba.

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
> U balíčků vytvořených pro veřejnou `<tags>` spotřebu věnujte tomuto prvku zvláštní pozornost, protože tyto značky pomáhají ostatním najít váš balíček a pochopit, co dělá.

### <a name="adding-windows-metadata-to-the-package"></a>Přidání metadat systému Windows do balíčku

Součást prostředí Windows Runtime vyžaduje metadata, která popisují všechny jeho veřejně dostupné typy, což umožňuje ostatním aplikacím a knihovnám využívat komponentu. Tato metadata jsou obsažena v souboru .winmd, který je vytvořen při kompilaci projektu a musí být zahrnuty do balíčku NuGet. Soubor XML s daty Technologie IntelliSense je také vytvořen současně a měl by být také zahrnut.

Přidejte `<files>` do souboru `.nuspec` následující uzel:

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

Chcete-li zahrnout ovládací prvek XAML s komponentou, je třeba přidat soubor XAML, který má výchozí šablonu pro ovládací prvek (jak je generováno šablonou projektu). To platí i `<files>` v sekci:

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

V rámci komponenty je základní logika typu ImageEnhancer v nativním `ImageEnhancer.dll` kódu, který je obsažen v různých sestaveních, které jsou generovány pro každý cílový runtime (ARM, x86 a x64). Chcete-li je zahrnout do balíčku, odkazujte na ně v `<files>` sekci spolu s přidruženými soubory prostředků .pri:

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

### <a name="adding-targets"></a>Přidání .targets

Dále c++ a JavaScript projekty, které mohou využívat váš balíček NuGet potřebovat soubor .targets k identifikaci potřebné sestavení a winmd soubory. (Projekty jazyka C# a Visual Basic to dělají automaticky.) Vytvořte tento soubor zkopírováním `ImageEnhancer.targets` níže uvedeného textu do `.nuspec` a uložte jej do stejné složky jako soubor. _Poznámka_: `.targets` Tento soubor musí mít stejný název jako ID `<Id>` balíčku (např. prvek v souboru): `.nupspec`

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

Pak se `ImageEnhancer.targets` podívejte `.nuspec` do souboru:

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

### <a name="final-nuspec"></a>Konečný .nuspec

Konečný `.nuspec` soubor by nyní měl vypadat takto, kde by měl být opět nahrazen YOUR_NAME příslušnou hodnotou:

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

## <a name="package-the-component"></a>Balení komponenty

S dokončeným `.nuspec` odkazováním na všechny soubory, které potřebujete zahrnout do `pack` balíčku, jste připraveni spustit příkaz:

```cli
nuget pack ImageEnhancer.nuspec
```

To generuje `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`. Otevření tohoto souboru v nástroji, jako je [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) a rozbalení všech uzlů, uvidíte následující obsah:

![NuGet Package Explorer zobrazující balíček ImageEnhancer](media/UWP-PackageExplorer.png)

> [!Tip]
> Soubor `.nupkg` je pouze soubor ZIP s jinou příponou. Můžete také prozkoumat obsah balíčku, `.nupkg` `.zip`pak změnou na , ale nezapomeňte obnovit rozšíření před odesláním balíček nuget.org.

Chcete-li balíček zpřístupnit ostatním [vývojářům,](../nuget-org/publish-a-package.md)postupujte podle pokynů k části Publikovat balíček .

## <a name="related-topics"></a>Související témata

- [Odkaz na odkaz .nuspec](../reference/nuspec.md)
- [Balíčky symbolů](../create-packages/symbol-packages-snupkg.md)
- [Správa verzí balíčku](../concepts/package-versioning.md)
- [Podpora více verzí rozhraní .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Zahrnout rekvizity a cíle MSBuild do balíčku](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Vytváření lokalizovaných balíčků](../create-packages/creating-localized-packages.md)
