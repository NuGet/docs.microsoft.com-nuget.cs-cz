---
title: Vytvoření balíčků NuGet pro univerzální platformu Windows
description: Komplexní návod k vytváření balíčků NuGet pomocí součásti prostředí Windows Runtime pro univerzální platformu Windows v systému C#.
author: rrelyea
ms.author: rrelyea
ms.date: 02/28/2020
ms.topic: tutorial
ms.openlocfilehash: 61f46f2623769927f881877cfe3f96132211b442
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231803"
---
# <a name="create-uwp-packages-c"></a>Vytvořit balíčky UPW (C#)

[Univerzální platforma Windows (UPW)](/windows/uwp) poskytuje společnou platformu aplikací pro každé zařízení se systémem Windows 10. V rámci tohoto modelu mohou aplikace UPW volat rozhraní API WinRT, která jsou společná pro všechna zařízení, a také rozhraní API (včetně Win32 a .NET), která jsou specifická pro rodinu zařízení, na které je aplikace spuštěna.

V tomto návodu vytvoříte balíček NuGet s komponentou C# UWP (včetně ovládacího prvku XAML), který lze použít v řízených i nativních projektech.

## <a name="prerequisites"></a>Požadavky

1. Visual Studio 2019. Nainstalujte verzi Community 2019 zdarma od [visualstudio.com](https://www.visualstudio.com/); můžete také použít edice Professional a Enterprise.

1. NuGet CLI. Stáhněte si `nuget.exe` nejnovější verzi z [nuget.org/downloads](https://nuget.org/downloads)a uložte ji na `.exe` místo podle vašeho výběru (stahování je přímo). Pak přidejte toto umístění do proměnné prostředí PATH, pokud ještě není. [Další podrobnosti](/nuget/reference/nuget-exe-cli-reference#windows).

## <a name="create-a-uwp-windows-runtime-component"></a>Vytvoření součásti runtime systému Windows v programu UPW

1. V sadě Visual Studio zvolte **Soubor > Nový > Project**, vyhledejte položku "uwp c#", vyberte šablonu **komponenty Prostředí Windows Runtime (Universal Windows),** klepněte na tlačítko Další, změňte název na ImageEnhancer a klepněte na tlačítko Vytvořit. Po zobrazení výzvy přijměte výchozí hodnoty pro cílovou a minimální verzi.

    ![Vytvoření nového projektu komponenty runtime systému Windows UWP](media/UWP-NewProject-CS.png)

1. Klepněte pravým tlačítkem myši na projekt v Průzkumníku řešení, vyberte **Přidat > novou položku**, vyberte **Šablonový ovládací prvek**, změňte název, AwesomeImageControl.cs, a klepněte na **Přidat**:

    ![Přidání nové položky ovládacího prvku šablony XAML do projektu](media/UWP-NewXAMLControl-CS.png)

1. Klikněte pravým tlačítkem myši na projekt v Průzkumníku řešení a vyberte **Vlastnosti.** Na stránce Vlastnosti zvolte **Vytvořit** kartu a povolte **soubor dokumentace XML**:

    ![Nastavení generování souborů dokumentace XML na ano](media/UWP-GenerateXMLDocFiles-CS.png)

1. Klikněte pravým tlačítkem myši na *řešení,* vyberte **Dávkové sestavení**, zaškrtněte pět sestavení v dialogovém okně, jak je znázorněno níže. Tím zajistíte, že při vytváření sestavení vygenerujete úplnou sadu artefaktů pro každý z cílových systémů, které systém Windows podporuje.

    ![Dávkové sestavení](media/UWP-BatchBuild-CS.png)

1. V dialogovém okně Dávkové sestavení a klepněte na tlačítko **Sestavit,** chcete-li ověřit projekt a vytvořit výstupní soubory, které potřebujete pro balíček NuGet.

> [!Note]
> V tomto návodu použijete artefakty ladění pro balíček. U balíčku bez ladění zkontrolujte možnosti vydání v dialogovém okně Dávkové sestavení a v následujících krocích se podívejte na výsledné složky release.

## <a name="create-and-update-the-nuspec-file"></a>Vytvoření a aktualizace souboru Nuspec

Chcete-li `.nuspec` vytvořit počáteční soubor, proveďte následující tři kroky. Následující části vás pak provedou dalšími nezbytnými aktualizacemi.

1. Otevřete příkazový řádek a přejděte do složky obsahující `ImageEnhancer.csproj` (bude to podsložka pod místem, kde je soubor řešení).
1. Spusťte příkaz, [`NuGet spec`](/nuget/reference/cli-reference/cli-ref-spec) který chcete vygenerovat `ImageEnhancer.nuspec` (název `.csroj` souboru je převzat z názvu souboru):

    ```cli
    nuget spec
    ```

1. Otevřete `ImageEnhancer.nuspec` v editoru a aktualizujte jej tak, aby odpovídal následujícímu, a nahrazují YOUR_NAME příslušnou hodnotou. Nenechávejte žádné hodnoty $propertyName$. Hodnota, `<id>` konkrétně musí být jedinečný napříč nuget.org (viz konvence pojmenování popsané v [vytvoření balíčku).](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) Všimněte si také, že musíte také aktualizovat značky autora a popisu nebo se během kroku balení zobrazí chyba.

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
      <file src="bin\Debug\ImageEnhancer.winmd" target="lib\uap10.0"/>
      <file src="bin\Debug\ImageEnhancer.xml" target="lib\uap10.0"/>
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

V rámci komponenty je základní logika typu ImageEnhancer v nativním `ImageEnhancer.winmd` kódu, který je obsažen v různých sestaveních, které jsou generovány pro každý cílový runtime (ARM, ARM64, x86 a x64). Chcete-li je zahrnout do balíčku, odkazujte na ně v `<files>` sekci spolu s přidruženými soubory prostředků .pri:

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

## <a name="package-the-component"></a>Balení komponenty

S dokončeným `.nuspec` odkazováním na všechny soubory, které potřebujete zahrnout do [`nuget pack`](/nuget/reference/cli-reference/cli-ref-pack) balíčku, jste připraveni spustit příkaz:

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
