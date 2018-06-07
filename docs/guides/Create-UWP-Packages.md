---
title: Vytvoření balíčků NuGet pro univerzální platformu Windows
description: Začátku do konce návod, jak vytvořit balíčky NuGet používání komponent prostředí Windows Runtime pro univerzální platformu Windows.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/21/2017
ms.topic: tutorial
ms.openlocfilehash: c5d5bf72b99f6c2fe1b0a708ddb314d5711bc73d
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818279"
---
# <a name="create-uwp-packages"></a>Vytvořit balíčky UWP

[Univerzální platformu Windows (UWP)](https://developer.microsoft.com/windows) poskytuje společné platformě aplikace pro každé zařízení se systémem Windows 10. V rámci tohoto modelu aplikace UWP můžete volat rozhraní API WinRT, které jsou společné pro všechna zařízení i taky rozhraní API (včetně Win32 a rozhraní .NET), které jsou specifické pro dané řadě zařízení, na kterém aplikace běží.

V tomto návodu vytvoříte balíček NuGet s nativní UWP komponentou (včetně ovládacího prvku XAML) mohou být používány spravované a nativní projekty.

## <a name="prerequisites"></a>Požadavky

1. Visual Studio 2017 nebo Visual Studio 2015. Instalaci edice Community 2017 zdarma z [visualstudio.com](https://www.visualstudio.com/); můžete použít také edice Professional a Enterprise.

1. Rozhraní příkazového řádku NuGet. Stáhněte si nejnovější verzi `nuget.exe` z [nuget.org/downloads](https://nuget.org/downloads), ukládání do umístění podle vaší volby (ke stažení je `.exe` přímo). Pak přidejte tohoto umístění do vaší proměnné prostředí PATH, pokud již není.

## <a name="create-a-uwp-windows-runtime-component"></a>Vytvoření komponenty prostředí Windows Runtime UWP

1. V sadě Visual Studio, vyberte **soubor > Nový > projekt**, rozbalte **Visual C++ > Windows > Universal** uzlu, vyberte **komponenty prostředí Windows Runtime (Universal Windows)** šablony, změňte název na ImageEnhancer a klikněte na tlačítko OK. Přijměte výchozí hodnoty pro cílovou verzi a minimální verzi po zobrazení výzvy.

    ![Vytvoření nového projektu UPW komponenty prostředí Windows Runtime](media/UWP-NewProject.png)

1. Klikněte pravým tlačítkem na projekt v Průzkumníku řešení, vyberte **Přidat > Nová položka**, klikněte na tlačítko **Visual C++ > XAML** uzlu, vyberte **Šablonované řízení**, změňte název souboru na AwesomeImageControl.cpp a klikněte na tlačítko **přidat**:

    ![Přidání nové položky podle šablony řízení XAML do projektu](media/UWP-NewXAMLControl.png)

1. Klikněte pravým tlačítkem na projekt v Průzkumníku řešení a vyberte **vlastnosti.** Na stránce vlastností rozbalte **vlastnosti konfigurace > C/C++** a klikněte na tlačítko **výstupní soubory**. V podokně na pravé straně, změňte hodnotu **generování souborů dokumentace XML** Ano:

    ![Nastavení generování souborů dokumentace XML na Ano](media/UWP-GenerateXMLDocFiles.png)

1. Klikněte pravým tlačítkem *řešení* nyní, vyberte **dávkové sestavení**, zaškrtněte tři políčka ladění v dialogovém okně, jak je uvedeno níže. Tím je zajištěno, že při sestavení, vygenerování kompletní artefaktů pro jednotlivé cílové systémy, které podporuje Windows.

    ![Batch sestavení](media/UWP-BatchBuild.png)

1. V dávce sestavení dialogové okno a klikněte na tlačítko **sestavení** ověření projektu a vytvořit výstupní soubory, které potřebujete pro balíček NuGet.

> [!Note]
> V tomto názorném postupu použijete artefakty ladění pro balíček. Pro balíček bez ladění místo toho zkontrolujte verzi možností v dialogovém okně dávkové sestavení a odkazovat na výsledný složky verze v krocích, které následují.

## <a name="create-and-update-the-nuspec-file"></a>Vytvářet a aktualizovat soubor s příponou .nuspec

Chcete-li vytvořit počáteční `.nuspec` souboru, proveďte následující tři kroky. V následujících pak provede další potřebné aktualizace.

1. Otevřete příkazový řádek a přejděte do složky obsahující `ImageEnhancer.vcxproj` (to se stane podsložky níže, kde je soubor řešení).
1. Spustit NuGet `spec` příkazu vygenerujte `ImageEnhancer.nuspec` (název souboru je převzat z názvu `.vcxproj` souborů):

    ```cli
    nuget spec
    ```

1. Otevřete `ImageEnhancer.nuspec` v editoru a aktualizovat ji tak, aby odpovídala následující, nahraďte vaše_jméno odpovídající hodnotu. `<id>` Hodnotu, konkrétně musí být jedinečný v rámci nuget.org (viz zásady vytváření názvů, které jsou popsané v [vytváření balíčku](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)). Všimněte si také, zda je nutné také aktualizovat autora a popis značky nebo dojde k chybě během kroku okolních.

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
> Pro balíčky vytvořené pro veřejné spotřeby, věnujte zvláštní pozornost `<tags>` elementu, jako jsou tyto značky ostatní najít váš balíček a co provádí.

### <a name="adding-windows-metadata-to-the-package"></a>Přidávání metadat Windows do balíčku

Komponent prostředí Windows Runtime vyžaduje metadata, která popisuje všechny veřejně dostupné typy, které umožňuje jiným aplikacím a knihovny využívat komponentu. Tato metadata je obsažený v souboru .winmd, který se vytvoří při kompilaci projektu a musí být součástí vašeho balíčku NuGet. Soubor XML s daty IntelliSense vychází ve stejnou dobu a by měly být zahrnuty i.

Přidejte následující `<files>` uzlu `.nuspec` souboru:

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

### <a name="adding-xaml-content"></a>Přidání součástí obsahu XAML

Chcete-li zahrnout prvku XAML pomocí příslušné součásti, přidejte soubor XAML, který má výchozí šablonu pro ovládací prvek (generovaná šablony projektu). To také ukládá `<files>` části:

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

### <a name="adding-the-native-implementation-libraries"></a>Přidání knihovny nativní implementaci

V rámci vaší komponenty základní logika typu ImageEnhancer je v nativním kódu, který se nachází v různých `ImageEnhancer.dll` sestavení, které jsou generovány pro každý cílový modul runtime (x 86 a x64 ARM). Zahrnout tyto v balíčku, odkazujte na ně v `<files>` části spolu s jejich přidružené .pri soubory prostředků:

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

        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>

        <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    </files>
</package>
```

### <a name="adding-targets"></a>Přidání .targets

Projekty C++ a JavaScript, které může využívat vašeho balíčku NuGet v dalším kroku třeba souboru .targets pro identifikaci potřebné soubory sestavení a souboru winmd. (C# a Visual Basic projekty k tomu automaticky.) Tento soubor vytvořte tak, že zkopírujete následující text do `ImageEnhancer.targets` a uložte ho ve stejné složce jako `.nuspec` souboru. _Poznámka:_: to `.targets` soubor musí být stejný název jako ID balíčku (například `<Id>` element v `.nupspec` souboru):

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

Potom se podívejte na `ImageEnhancer.targets` ve vaší `.nuspec` souboru:

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

### <a name="final-nuspec"></a>Poslední příponou .nuspec.

Váš koncový `.nuspec` soubor by měl nyní vypadat jako následující, kde znovu vaše_jméno by měla být nahrazená příslušnou hodnotu:

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
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    <!-- .targets -->
    <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

## <a name="package-the-component"></a>Balíček součásti

S dokončené `.nuspec` odkazující na všechny soubory, které je potřeba zahrnout do balíčku, jste připraveni ke spuštění `pack` příkaz:

```cli
nuget pack ImageEnhancer.nuspec
```

Tím se vygeneruje `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`. Otevření tohoto souboru v nástroje, jako [Explorer balíček NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) a rozšiřování všechny uzly, můžete zobrazit následující obsah:

![Průzkumník balíček NuGet zobrazující ImageEnhancer balíčku](media/UWP-PackageExplorer.png)

> [!Tip]
> A `.nupkg` soubor je právě soubor ZIP s jiné rozšíření. Můžete také zkontrolovat obsah balíčku, potom změnou `.nupkg` k `.zip`, ale nezapomeňte obnovit rozšíření před balíčku se nahrávají na nuget.org.

Pokud chcete zpřístupnit vašeho balíčku jinými vývojáři, postupujte podle pokynů [publikování balíčku](../create-packages/publish-a-package.md).

## <a name="related-topics"></a>Související témata

- [referenční dokumentace příponou .nuspec](../reference/nuspec.md)
- [Balíčky symbolů](../create-packages/symbol-packages.md)
- [Správa verzí balíčků](../reference/package-versioning.md)
- [Podpora více verzí rozhraní .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Zahrnout do balíčku nástroje MSBuild props a cíle](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [Vytvoření lokalizovaných balíčků](../create-packages/creating-localized-packages.md)
