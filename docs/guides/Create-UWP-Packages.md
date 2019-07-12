---
title: Vytváření balíčků NuGet pro Universal Windows Platform
description: Začátku do konce postup vytváření balíčků NuGet pro univerzální platformu Windows pomocí komponenty Windows Runtime.
author: karann-msft
ms.author: karann
ms.date: 03/21/2017
ms.topic: tutorial
ms.openlocfilehash: 344c8d764180d0f33c1bce77b721e3657297e74e
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842123"
---
# <a name="create-uwp-packages"></a>Vytvoření balíčků UPW

[Univerzální platformu Windows (UPW)](https://developer.microsoft.com/windows) poskytuje společnou platformu aplikace pro každé zařízení, na kterém běží Windows 10. V rámci tohoto modelu aplikací pro UWP můžete volat rozhraní API WinRT, která jsou společná pro všechna zařízení i také rozhraní API (včetně Win32 a .NET), které jsou specifické na řadě zařízení, na kterém je aplikace spuštěna.

V tomto návodu vytvoříte balíček NuGet s nativní UWP součásti (včetně ovládacího prvku XAML), který lze použít v spravovaný a nativní projekty.

## <a name="prerequisites"></a>Požadavky

1. Visual Studio 2017 nebo Visual Studio 2015. Instalace edice Community 2017 zdarma z [visualstudio.com](https://www.visualstudio.com/); můžete použít také edice Professional a Enterprise.

1. Rozhraní příkazového řádku NuGet. Stáhněte si nejnovější verzi `nuget.exe` z [nuget.org/downloads](https://nuget.org/downloads), ukládání do umístění podle vašeho výběru (soubor ke stažení je `.exe` přímo). Pak přidejte toto umístění do proměnné prostředí PATH, pokud ještě není.

## <a name="create-a-uwp-windows-runtime-component"></a>Vytvoření součásti UPW Windows Runtime

1. V sadě Visual Studio, zvolte **soubor > Nový > projekt**, rozbalte **Visual C++ > Windows > univerzální** uzlu, vyberte **součást prostředí Windows Runtime (Universal Windows)** šablony, změňte název na ImageEnhancer a klikněte na tlačítko OK. Přijměte výchozí hodnoty pro cílovou verzi a minimální verzi po zobrazení výzvy.

    ![Vytvoření nového projektu UPW součást prostředí Windows Runtime](media/UWP-NewProject.png)

1. Klikněte pravým tlačítkem myši na projekt v Průzkumníku řešení, vyberte **Přidat > Nová položka**, klikněte na tlačítko **Visual C++ > XAML** uzlu, vyberte **prvku bez vizuálního vzhledu**, změňte název na AwesomeImageControl.cpp a klikněte na tlačítko **přidat**:

    ![Přidání nové položky bez vizuálního vzhledu ovládacího prvku XAML do projektu](media/UWP-NewXAMLControl.png)

1. Klikněte pravým tlačítkem na projekt v Průzkumníku řešení a vyberte **vlastnosti.** Na stránce vlastností rozbalte **vlastnosti konfigurace > C/C++** a klikněte na tlačítko **výstupní soubory**. V podokně na pravé straně, změňte hodnotu **Generovat soubory dokumentace XML** na Ano:

    ![Nastavení Generovat soubory dokumentace XML na hodnotu Ano](media/UWP-GenerateXMLDocFiles.png)

1. Klikněte pravým tlačítkem myši *řešení* teď vyberte **dávkové sestavení**, zkontrolujte tři ladění pole v dialogovém okně, jak je znázorněno níže. Tím je zajištěno, že když použijete sestavení, vygenerujete kompletní sadu artefaktů pro každé cílové systémy, které podporuje Windows.

    ![Dávkové sestavení](media/UWP-BatchBuild.png)

1. V dávce sestavit dialogové okno a klikněte na tlačítko **sestavení** ověření projektu a vytvoření výstupních souborů, které potřebujete pro balíček NuGet.

> [!Note]
> V tomto názorném postupu použijete artefakty ladění pro balíček. Bez ladění balíčku zkontrolujte verzi možnosti v dialogovém okně dávkové sestavení místo toho a odkazovat na výsledný verzi složky v následujících kroků.

## <a name="create-and-update-the-nuspec-file"></a>Vytvoření a aktualizaci souboru .nuspec souboru

Chcete-li vytvořit počáteční `.nuspec` soubor, proveďte následující tři kroky. Následující části pak vás provede další potřebné aktualizace.

1. Otevřete příkazový řádek a přejděte do složky obsahující `ImageEnhancer.vcxproj` (bude to podsložka níže kde je soubor řešení).
1. Spuštění balíčku NuGet `spec` příkazu vygenerujte `ImageEnhancer.nuspec` (název souboru je převzat z názvu `.vcxproj` souboru):

    ```cli
    nuget spec
    ```

1. Otevřít `ImageEnhancer.nuspec` v editoru a aktualizujte ji, aby se shodoval s následujícím, nahradíte vaše_jméno odpovídající hodnotu. `<id>` , Konkrétně musí být hodnota jedinečná napříč nuget.org (naleznete v tématu Zásady vytváření názvů je popsáno v [vytvoření balíčku](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)). Všimněte si také, že budete muset taky aktualizovat Autor a popis značky nebo dojde k chybě během kroku balení.

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
> Pro balíčky sestavené ke zveřejnění, věnujte zvláštní pozornost `<tags>` element, protože tyto značky pomoci ostatním najít váš balíček a pochopit jeho význam.

### <a name="adding-windows-metadata-to-the-package"></a>Přidání metadat Windows do balíčku

Komponenta Windows Runtime vyžaduje metadata, která popisuje všechny veřejně dostupné typy, které umožňují další aplikace a knihovny, které chcete využívat komponentu. Tato metadata je obsažen v souboru winmd, který je vytvořen při kompilaci projektu a musí být součástí balíčku NuGet. Soubor XML s daty technologie IntelliSense je také integrované ve stejnou dobu a by měly být zahrnuty i.

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

### <a name="adding-xaml-content"></a>Přidání obsahu XAML

Zahrnout ovládacího prvku XAML pomocí vaší komponentě, budete muset přidat soubor XAML, který má výchozí šablony pro ovládací prvek (vygenerovaný pomocí šablony projektu). To také ukládá `<files>` části:

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

### <a name="adding-the-native-implementation-libraries"></a>Přidat nativní implementace knihovny

V rámci vaší komponenty základní logiky ImageEnhancer typ je v nativním kódu, který je obsažen v různých `ImageEnhancer.dll` sestavení, které jsou generovány pro každý cílový modul runtime (x 86 a x64 ARM). Pokud chcete zahrnout do balíčku, na ně odkazovat v `<files>` části spolu s jejich soubory prostředků přidružené .pri:

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

Projekty C++ a JavaScript, které může využívat svůj balíček NuGet dále, třeba souboru .targets pro identifikaci potřebné soubory sestavení a soubor winmd. (Projekty jazyka C# a Visual Basic udělat automaticky.) Tento soubor vytvořit zkopírováním níže uvedený text do `ImageEnhancer.targets` a uložte ho do stejné složky jako `.nuspec` souboru. _Poznámka:_ To `.targets` soubor musí být stejný název jako ID balíčku (například `<Id>` element v `.nupspec` souboru):

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

Potom použijte `ImageEnhancer.targets` ve vašich `.nuspec` souboru:

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

### <a name="final-nuspec"></a>Poslední souboru .nuspec

Výsledná `.nuspec` soubor by teď měl vypadat jako následující, kde znovu vaše_jméno by měla být nahrazena odpovídající hodnotu:

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

## <a name="package-the-component"></a>Balíček komponenty

S dokončenou `.nuspec` odkazující na všechny soubory, které je potřeba zahrnout do balíčku, jste připraveni spustit `pack` příkaz:

```cli
nuget pack ImageEnhancer.nuspec
```

Tím se vygeneruje `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`. Tento soubor otevřete v nástroje, jako je [NuGet – Průzkumník balíčků](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) a rozšiřuje všechny uzly, viz následující obsah:

![Zobrazuje ImageEnhancer balíčku NuGet – Průzkumník balíčků](media/UWP-PackageExplorer.png)

> [!Tip]
> A `.nupkg` soubor je jenom soubor ZIP s jinou příponou. Můžete také prozkoumat obsah balíčku, potom změnou `.nupkg` k `.zip`, ale nezapomeňte k obnovení rozšíření před nahráním balíčků na nuget.org.

Aby váš balíček k dispozici s ostatními vývojáři, postupujte podle pokynů [publikování balíčku](../nuget-org/publish-a-package.md).

## <a name="related-topics"></a>Související témata

- [odkaz na souboru .nuspec](../reference/nuspec.md)
- [Balíčky symbolů](../create-packages/symbol-packages.md)
- [Správa verzí balíčků](../reference/package-versioning.md)
- [Podpora více verzí rozhraní .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Zahrnout do balíčku cíle a vlastnosti nástroje MSBuild](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Vytvoření lokalizovaných balíčků](../create-packages/creating-localized-packages.md)
