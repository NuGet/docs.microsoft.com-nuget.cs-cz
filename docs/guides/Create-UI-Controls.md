---
title: Jak ovládacích prvků uživatelského rozhraní balíčku nuget
description: Jak vytvořit balíčky NuGet, které obsahují UPW nebo WPF ovládací prvky, včetně potřebná metadata a podpůrné soubory pro návrháře Visual Studio a Blend.
author: karann-msft
ms.author: karann
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: 522dbbb2a39eb1cb6f0d23f39a48158b07c9076d
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426857"
---
# <a name="creating-ui-controls-as-nuget-packages"></a>Vytvoření ovládacích prvků uživatelského rozhraní jako balíčků NuGet

Od verze Visual Studio 2017, můžete využít výhod přidané možnosti pro UPW a WPF ovládací prvky, které jsou užitečné v balíčcích NuGet. Tento průvodce vás provede tyto možnosti v souvislosti s použitím ovládacích prvků UPW [ExtensionSDKasNuGetPackage ukázka](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage). Totéž platí pro ovládací prvky WPF, pokud není uvedeno jinak.

## <a name="prerequisites"></a>Požadavky

1. Visual Studio 2017
1. Přehled o tom, jak [vytvoření balíčků UPW](create-uwp-packages.md)

## <a name="generate-library-layout"></a>Generovat rozložení knihovny

> [!Note]
> To se vztahuje pouze na ovládacích prvků UPW.

Nastavení `GenerateLibraryLayout` vlastnost zajistí, že se výstupní sestavení projektu vygeneruje v rozložení, který je připraven k zabalit, bez nutnosti položky jednotlivých souborů v souboru nuspec.

Z vlastnosti projektu přejděte na kartu sestavení a zaškrtnutím políčka "Generovat rozložení knihovny". To bude úpravu souboru projektu a nastavte `GenerateLibraryLayout` příznak na hodnotu true pro aktuálně vybraná konfigurace sestavení a platformu.

Můžete také upravit soubor projektu a přidejte `<GenerateLibraryLayout>true</GenerateLibraryLayout>` do první skupiny vlastností Nepodmíněný. To platí bez ohledu na konfiguraci sestavení a platformu vlastnost.

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a>Přidání podpory podokna nástrojů a prostředků pro ovládací prvky XAML

Pokud chcete, aby se zobrazí v panelu nástrojů návrháře XAML v sadě Visual Studio a v podokně prostředků aplikace Blend ovládacího prvku XAML, vytvořte `VisualStudioToolsManifest.xml` soubor v kořenové složce `tools` složce balíčku projektu. Tento soubor není povinný, pokud už nepotřebujete ovládací prvek se zobrazí v okně nástrojů nebo prostředky.

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

Struktura souboru je následující:

```xml
<FileList>
  <File Reference = "your_package_file">
    <ToolboxItems VSCategory="vs_category" BlendCategory="blend_category">
      <Item Type="type_full_name_1" />

      <!-- Any number of additional Items -->
      <Item Type="type_full_name_2" />
      <Item Type="type_full_name_3" />
    </ToolboxItems>
  </File>
</FileList>
```

kde:

- *your_package_file*: soubor název vašeho ovládacího prvku, třeba `ManagedPackage.winmd` ("ManagedPackage" je libovolnou s názvem používá pro účely tohoto příkladu a nemá žádný význam).
- *vs_category*: Popisek skupiny, ve kterém by se měla zobrazit ovládací prvek v panelu nástrojů návrháře aplikace Visual Studio. A `VSCategory` je nezbytné pro ovládací prvek se zobrazí na panelu nástrojů.
- *blend_category*: Popisek skupiny, ve kterém ovládací prvek by se měla zobrazit v podokně návrháře Blendu prostředky. A `BlendCategory` je nezbytné pro ovládací prvek se zobrazí v majetku.
- *type_full_name_n*: Plně kvalifikovaný název pro každý ovládací prvek, včetně oboru názvů, jako například `ManagedPackage.MyCustomControl`. Všimněte si, že formát tečka se používá pro spravovaný i nativní typy.

V pokročilejších scénářích, může také obsahovat více `<File>` elementů v rámci `<FileList>` Pokud jeden balíček obsahuje více sestavení ovládacího prvku. Můžete mít také více `<ToolboxItems>` uzly v jednom `<File>` Pokud budete chtít uspořádání ovládacích prvků do samostatných kategorií.

V následujícím příkladu, ovládací prvek implementované v `ManagedPackage.winmd` se zobrazí v sadě Visual Studio a Vmísil skupina s názvem "Spravované balíček" a "MyCustomControl" se zobrazí v této skupině. Tyto názvy jsou libovolného.

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![Ovládací prvek příklad, jak se zobrazí v sadě Visual Studio](media/UWP-control-vs-toolbox.png)

![Ovládací prvek příklad, jak se zobrazí v Blendu](media/UWP-control-blend-assets.png)

> [!Note]
> Je nutné explicitně zadat každý ovládací prvek, který chcete zobrazit na panelu nástrojů a prostředků. Ujistěte se, zadejte ve formátu `Namespace.ControlName`.

## <a name="add-custom-icons-to-your-controls"></a>Přidat vlastní ikony k ovládacím prvkům

K zobrazení vlastní ikony na panelu nástrojů a prostředků, přidat bitovou kopii do projektu nebo odpovídající `design.dll` projektu s názvem "Namespace.ControlName.extension" a nastavte akci sestavení na "Integrovaný prostředek". Musíte také zajistit, aby přidružené `AssemblyInfo.cs` Určuje atribut ProvideMetadata - `[assembly: ProvideMetadata(typeof(RegisterMetadata))]`. Najdete v tomto [ukázka](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20).

Podporované formáty jsou `.png`, `.jpg`, `.jpeg`, `.gif`, a `.bmp`. Doporučený formát je BMP24 v 16 × 16 pixelů.

![Ukázkový nástroj pro ikonu pole](https://raw.githubusercontent.com/NuGet/docs.microsoft.com-nuget/live/docs/guides/media/ColorPicker_16x16x24.bmp)

Růžový na pozadí nahrazuje za běhu. Ikony jsou obarveny při změně motivu sady Visual Studio a očekává se, že barvu pozadí. Další informace, použijte odkaz [obrázky a ikony pro sadu Visual Studio](https://docs.microsoft.com/en-us/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio).

V následujícím příkladu projektu obsahuje soubor image s názvem "ManagedPackage.MyCustomControl.png".

![Nastavení vlastní ikony v projektu](media/UWP-control-custom-icon.png)

> [!Note]
> Pro nativní ovládací prvky, je nutné umístit na ikonu jako prostředek v `design.dll` projektu.

## <a name="support-specific-windows-platform-versions"></a>Podporují konkrétní verze platformy Windows

Balíčků UPW mít TargetPlatformVersion (TPV) a prvkem TargetPlatformMinVersion (TPMinV), které definují horní a dolní meze zápisu verze operačního systému nainstalovanou aplikaci. Další TPV Určuje verzi sady SDK, proti kterému byla sestavena. Mějte na paměti tyto vlastnosti při vytváření balíčků UPW: pomocí rozhraní API mimo hranice verze platformy, které jsou definovány v aplikaci způsobí, že aby sestavení selhalo, nebo aplikaci, aby v době běhu selhat.

Například Řekněme, že jste nastavili TPMinV pro balíček sady ovládacích prvků Windows 10 Anniversary Edition (10.0; Sestavení 14393), tak, že chcete mít jistotu, že balíček je využívá jenom UPW projekty, které odpovídají, který dolní mez. Aby váš balíček pro projekty UWP, musíte sestavit balíček své ovládací prvky s následující názvy složek:

    \lib\uap10.0.14393\*
    \ref\uap10.0.14393\*

NuGet automaticky zkontroluje TPMinV náročné projektu a instalace selhat, pokud je nižší než Windows 10 Anniversary Edition (10.0; Sestavení 14393)

V případě WPF Řekněme, že byste chtěli balíčku ovládacích prvků WPF spotřebované podle projekty cílené na rozhraní .NET Framework v4.6.1 nebo vyšší. K vynucení, který, musíte sestavit balíček své ovládací prvky s následující názvy složek:

    \lib\net461\*
    \ref\net461\*

## <a name="add-design-time-support"></a>Přidání podpory během návrhu

Ke konfiguraci, kde vlastnosti ovládacího prvku zobrazí v okně Inspektor. vlastnosti, přidejte vlastní doplňky apod., umístěte vaše `design.dll` soubor uvnitř `lib\uap10.0.14393\Design` složky v závislosti na cílové platformě. Také zajistit, aby **[upravit šablonu > Upravit kopii](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** funkce funguje, je nutné uvést `Generic.xaml` a sloučení v slovníky prostředků `<your_assembly_name>\Themes` složky (znovu s použitím název vašeho sestavení skutečné). (Tento soubor nemá žádný vliv na chování modulu runtime ovládacího prvku.) Struktura složek by tak vypadat následovně:

    \lib
      \uap10.0.14393
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml


Pro WPF pokračování příkladu s, kde chcete vaše WPF – ovládací prvky balíček spotřebované podle projekty cílené na rozhraní .NET Framework v4.6.1 nebo vyšší:

    \lib
      \net461
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> Ve výchozím nastavení vlastností ovládacích prvků se zobrazí v rámci různé kategorie v inspektoru.

## <a name="use-strings-and-resources"></a>Použití řetězců a prostředků

Můžete vložit řetězcové prostředky (`.resw`) v balíčku, který lze použít ovládací prvek nebo náročné projektu UPW, nastavte **akce sestavení** vlastnost `.resw` do souboru **PRIResource**.

Příklad najdete v tématu [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) v ukázce ExtensionSDKasNuGetPackage.

> [!Note]
> To se vztahuje pouze na ovládacích prvků UPW.

## <a name="see-also"></a>Viz také:

- [Vytvoření balíčků UPW](create-uwp-packages.md)
- [Ukázka ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
