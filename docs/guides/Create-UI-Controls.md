---
title: Jak zabalit ovládací prvky ui s NuGet
description: Jak vytvořit balíčky NuGet, které obsahují ovládací prvky UPW nebo WPF, včetně nezbytných metadat a podpůrných souborů pro návrháře sady Visual Studio a Blend.
author: karann-msft
ms.author: karann
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: da8c5a05311c790bf6b873bc0f1a077d3ef1db87
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "73610619"
---
# <a name="creating-ui-controls-as-nuget-packages"></a>Vytvoření ovládacích prvků uživatelského rozhraní jako balíčků NuGet

Počínaje Visual Studio 2017, můžete využít přidané možnosti pro OVLÁDACÍ PRVKY UPW a WPF, které dodáváte v balíčcích NuGet. Tato příručka vás provede těmito funkcemi v kontextu ovládacích prvků UPW pomocí [ukázky ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage). Totéž platí pro ovládací prvky WPF, pokud není uvedeno jinak.

## <a name="prerequisites"></a>Požadavky

1. Visual Studio 2017
1. Pochopení toho, jak [vytvořit balíčky UPW](create-uwp-packages.md)

## <a name="generate-library-layout"></a>Generovat rozložení knihovny

> [!Note]
> To platí pouze pro ovládací prvky UPW.

Nastavení `GenerateLibraryLayout` vlastnosti zajišťuje, že výstup sestavení projektu je generován v rozložení, které je připraveno k balení bez nutnosti jednotlivých položek souboru v nuspec.

Ve vlastnostech projektu přejděte na kartu sestavení a zaškrtněte políčko Generovat rozložení knihovny. Tím se změní soubor projektu `GenerateLibraryLayout` a nastaví příznak na hodnotu true pro aktuálně vybranou konfiguraci sestavení a platformu.

Případně upravte soubor projektu, `<GenerateLibraryLayout>true</GenerateLibraryLayout>` který chcete přidat do první skupiny nepodmíněných vlastností. To by použít vlastnost bez ohledu na konfiguraci sestavení a platformu.

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a>Přidání podpory panelu nástrojů/datových zdrojů pro ovládací prvky XAML

Chcete-li, aby se ovládací prvek XAML zobrazil v panelu nástrojů návrháře `VisualStudioToolsManifest.xml` XAML v `tools` sadě Visual Studio a podokně Prostředků blendu, vytvořte soubor v kořenovém adresáři složky projektu balíčku. Tento soubor není vyžadován, pokud nepotřebujete ovládací prvek, který se zobrazí v panelu nástrojů nebo v podokně Datové zdroje.

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

- *your_package_file*: název řídicího souboru, například `ManagedPackage.winmd` ("ManagedPackage" je libovolně pojmenovaný pro tento příklad a nemá žádný jiný význam).
- *vs_category*: Popisek pro skupinu, ve kterém by měl být ovládací prvek zobrazen v panelu nástrojů návrháře sady Visual Studio. A `VSCategory` je nezbytné pro ovládací prvek se zobrazí v panelu nástrojů.
- *blend_category*: Popisek pro skupinu, ve které by se měl ovládací prvek zobrazit v podokně Datové zdroje návrháře prolnutí. A `BlendCategory` je nezbytné pro ovládací prvek se zobrazí v prostředky.
- *type_full_name_n*: Plně kvalifikovaný název pro každý ovládací prvek, `ManagedPackage.MyCustomControl`včetně oboru názvů, například . Všimněte si, že formát tečky se používá pro spravované i nativní typy.

V pokročilejších scénářích můžete také `<File>` zahrnout `<FileList>` více prvků v rámci, když jeden balíček obsahuje více sestavení ovládacího prvku. Můžete mít také `<ToolboxItems>` více uzlů `<File>` v rámci jednoho, pokud chcete uspořádat ovládací prvky do samostatných kategorií.

V následujícím příkladu ovládací `ManagedPackage.winmd` prvek implementovaný v aplikaci se zobrazí v sadě Visual Studio a Blend ve skupině s názvem "Spravovaný balíček" a "MyCustomControl" se zobrazí v této skupině. Všechna tato jména jsou libovolná.

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![Ukázkový ovládací prvek tak, jak se zobrazuje v sadě Visual Studio](media/UWP-control-vs-toolbox.png)

![Příklad ovládacího prvku, který se zobrazuje v prolnutí](media/UWP-control-blend-assets.png)

> [!Note]
> Je nutné explicitně zadat každý ovládací prvek, který chcete zobrazit v podokně nástrojů/datových zdrojů. Ujistěte se, že `Namespace.ControlName`je zadáte ve formátu .

## <a name="add-custom-icons-to-your-controls"></a>Přidání vlastních ikon k ovládacím prvkům

Chcete-li zobrazit vlastní ikonu v podokně panelu nástrojů nebo `design.dll` datových zdrojů, přidejte obrázek do projektu nebo odpovídajícího projektu s názvem Namespace.ControlName.extension a nastavte akci sestavení na Vložený zdroj. Musíte také zajistit, `AssemblyInfo.cs` že přidružený určuje ProvideMetadata atribut - `[assembly: ProvideMetadata(typeof(RegisterMetadata))]`. Viz tento [příklad](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20).

Podporované formáty `.png` `.jpg`jsou `.jpeg` `.gif`, `.bmp`, , a . Doporučený formát je BMP24 v 16 pixelech x 16 pixelů.

![Ukázka ikony rámečku nástrojů](https://raw.githubusercontent.com/NuGet/docs.microsoft.com-nuget/live/docs/guides/media/ColorPicker_16x16x24.bmp)

Růžové pozadí je nahrazeno za běhu. Ikony jsou přebarveny při změně motivu sady Visual Studio a očekává se barva pozadí. Další informace naleznete v [odkazech na obrázky a ikony sady Visual Studio](https://docs.microsoft.com/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio).

V níže uvedeném příkladu projekt obsahuje soubor obrázku s názvem "ManagedPackage.MyCustomControl.png".

![Nastavení vlastní ikony v projektu](media/UWP-control-custom-icon.png)

> [!Note]
> U nativních ovládacích prvků je nutné `design.dll` umístit ikonu jako zdroj do projektu.

## <a name="support-specific-windows-platform-versions"></a>Podpora konkrétních verzí platformy Windows

Balíčky UPW mají TargetPlatformVersion (TPV) a TargetPlatformMinVersion (TPMinV), které definují horní a dolní hranice verze operačního systému, kde lze nainstalovat aplikaci. TPV dále určuje verzi sady SDK, proti které je aplikace postavena. Mějte na paměti tyto vlastnosti při vytváření balíčku UPW: použití rozhraní API mimo hranice verze platformy definované v aplikaci způsobí, že sestavení nezdaří nebo aplikace nezdaří za běhu.

Řekněme například, že jste nastavili tpminv pro balíček ovládacích prvků na Windows 10 Anniversary Edition (10.0; Sestavení 14393), takže chcete zajistit, že balíček je spotřebována pouze projekty UPW, které odpovídají dolní mez. Chcete-li povolit, aby byl balíček spotřebován projekty UPW, je nutné zabalit ovládací prvky s následujícími názvy složek:

    \lib\uap10.0.14393\*
    \ref\uap10.0.14393\*

NuGet automaticky zkontroluje TPMinV náročného projektu a nezdaří instalaci, pokud je nižší než Windows 10 Anniversary Edition (10.0; Budova 14393)

V případě WPF řekněme, že chcete, aby váš balíček wpf ovládacích prvků spotřebovávat projekty cílení .NET Framework v4.6.1 nebo vyšší. Chcete-li vynutit, že je nutné zabalit ovládací prvky s následujícími názvy složek:

    \lib\net461\*
    \ref\net461\*

## <a name="add-design-time-support"></a>Přidání podpory návrhu

Chcete-li nakonfigurovat, kde se vlastnosti ovládacího prvku zobrazí v `design.dll` inspektoru `lib\uap10.0.14393\Design` vlastností, přidejte vlastní adorners atd., umístěte soubor do složky podle potřeby na cílovou platformu. Chcete-li zajistit, aby funkce **[Upravit šablonu > Upravit kopii](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** fungovala, musíte do složky zahrnout slovníky `Generic.xaml` prostředků a všechny slovníky prostředků, které slučuje `<your_assembly_name>\Themes` (opět pomocí skutečného názvu sestavení). (Tento soubor nemá žádný vliv na chování ovládacího prvku za běhu.) Struktura složek by se tedy jevila takto:

    \lib
      \uap10.0.14393
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml


Pro WPF, pokračování v příkladu, kde chcete, aby váš wpf ovládací prvky balíček spotřebovávat projekty cílení .NET Framework v4.6.1 nebo vyšší:

    \lib
      \net461
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> Ve výchozím nastavení se vlastnosti ovládacího prvku zobrazí v kategorii Různé v inspektoru vlastností.

## <a name="use-strings-and-resources"></a>Použití řetězců a prostředků

Můžete vložit prostředky řetězce`.resw`( ) do balíčku, který může být použit ovládacím prvkem nebo náročným projektem UPW, nastavit vlastnost **Build Action** souboru `.resw` na **PRIResource**.

Příklad naleznete [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) v ExtensionSDKasNuGetPackage vzorku.

> [!Note]
> To platí pouze pro ovládací prvky UPW.

## <a name="see-also"></a>Viz také

- [Vytvořit balíčky UPW](create-uwp-packages.md)
- [Ukázka rozšířeníSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
