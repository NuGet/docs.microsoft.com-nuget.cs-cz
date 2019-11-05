---
title: Jak zabalit ovládací prvky uživatelského rozhraní pomocí NuGet
description: Vytvoření balíčků NuGet, které obsahují ovládací prvky UWP nebo WPF, včetně nezbytných metadat a podpůrných souborů pro návrháře sady Visual Studio a Blendu.
author: karann-msft
ms.author: karann
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: da8c5a05311c790bf6b873bc0f1a077d3ef1db87
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610619"
---
# <a name="creating-ui-controls-as-nuget-packages"></a>Vytvoření ovládacích prvků uživatelského rozhraní jako balíčků NuGet

Počínaje sadou Visual Studio 2017 můžete využít výhod přidaných funkcí pro ovládací prvky UWP a WPF, které zadáváte do balíčků NuGet. Tato příručka vás provede následujícími možnostmi v kontextu ovládacích prvků UWP pomocí [ukázky ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage). Totéž platí pro ovládací prvky WPF, pokud není uvedeno jinak.

## <a name="prerequisites"></a>Požadavky

1. Visual Studio 2017
1. Informace o tom, jak [vytvářet balíčky UWP](create-uwp-packages.md)

## <a name="generate-library-layout"></a>Generovat rozložení knihovny

> [!Note]
> To platí pouze pro ovládací prvky UWP.

Nastavení vlastnosti `GenerateLibraryLayout` zajistí, že výstup sestavení projektu bude vygenerován v rozložení, které je připraveno k zabalení bez nutnosti jednotlivých položek souborů v nuspec.

Z vlastností projektu, přejít na kartu sestavení a zaškrtněte políčko Generovat rozložení knihovny. Tím se upraví soubor projektu a nastaví se příznak `GenerateLibraryLayout` pro aktuálně vybranou konfiguraci a platformu sestavení na hodnotu true.

Případně upravte soubor projektu pro přidání `<GenerateLibraryLayout>true</GenerateLibraryLayout>` do první nepodmíněné skupiny vlastností. Tato vlastnost by se použila bez ohledu na konfiguraci sestavení a platformu.

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a>Přidání podpory nástrojů/panelu nástrojů pro ovládací prvky XAML

Chcete-li, aby se ovládací prvek XAML zobrazil v sadě nástrojů návrháře XAML v sadě Visual Studio a v podokně assets (prostředky), vytvořte soubor `VisualStudioToolsManifest.xml` v kořenu složky `tools` projektu balíčku. Tento soubor není povinný, pokud nepotřebujete, aby se ovládací prvek zobrazoval v podokně nástrojů nebo aktiv.

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

- *your_package_file*: název řídicího souboru, například `ManagedPackage.winmd` ("ManagedPackage" je libovolný název, který se používá pro tento příklad a nemá žádný jiný význam).
- *vs_category*: popisek skupiny, ve které by se měl ovládací prvek zobrazit v sadě nástrojů Visual Studio designer. `VSCategory` je nutné, aby se ovládací prvek zobrazoval v sadě nástrojů.
- *blend_category*: popisek skupiny, ve které by se měl ovládací prvek zobrazit v podokně assets návrháře Blendu. `BlendCategory` je nutné, aby se ovládací prvek objevil v prostředcích.
- *type_full_name_n*: plně kvalifikovaný název pro každý ovládací prvek, včetně oboru názvů, jako je například `ManagedPackage.MyCustomControl`. Všimněte si, že formát tečky se používá pro spravované i nativní typy.

V pokročilejších scénářích můžete také zahrnout více `<File>` prvků v rámci `<FileList>`, pokud jeden balíček obsahuje více sestavení ovládacích prvků. Můžete mít také více `<ToolboxItems>` uzlů v rámci jednoho `<File>`, pokud chcete uspořádat ovládací prvky do samostatných kategorií.

V následujícím příkladu se ovládací prvek implementovaný v `ManagedPackage.winmd` zobrazí v aplikaci Visual Studio a Blend ve skupině s názvem "Managed Package" a "MyCustomControl" se zobrazí v této skupině. Všechny tyto názvy jsou libovolné.

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![Příklad ovládacího prvku, který se zobrazí v aplikaci Visual Studio](media/UWP-control-vs-toolbox.png)

![Vzorový ovládací prvek, který se zobrazí v Blendu](media/UWP-control-blend-assets.png)

> [!Note]
> Každý ovládací prvek, který byste chtěli zobrazit v podokně Sada nástrojů/prostředky, musíte explicitně zadat. Ujistěte se, že je zadáte ve formátu `Namespace.ControlName`.

## <a name="add-custom-icons-to-your-controls"></a>Přidat vlastní ikony do ovládacích prvků

Chcete-li zobrazit vlastní ikonu v podokně Sada nástrojů/assets, přidejte do projektu obrázek nebo odpovídající projekt `design.dll` s názvem "obor názvů. Control. Extension" a nastavte akci sestavení na "Integrovaný prostředek". Musíte také zajistit, aby související `AssemblyInfo.cs` určovala `[assembly: ProvideMetadata(typeof(RegisterMetadata))]`atributu ProvideMetadata. Podívejte se na tuto [ukázku](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20).

Podporované formáty jsou `.png`, `.jpg`, `.jpeg`, `.gif`a `.bmp`. Doporučený formát je BMP24 v rozmezí 16 × 16 pixelů.

![Ukázka ikony pole nástrojů](https://raw.githubusercontent.com/NuGet/docs.microsoft.com-nuget/live/docs/guides/media/ColorPicker_16x16x24.bmp)

Růžová pozadí je nahrazena za běhu. Když se změní motiv sady Visual Studio a očekává se barva pozadí, jsou ikony Přebarvené. Další informace najdete v referenčních [obrázcích a ikonách pro Visual Studio](https://docs.microsoft.com/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio).

V následujícím příkladu obsahuje projekt soubor s obrázkem s názvem "ManagedPackage. MyCustomControl. png".

![Nastavení vlastní ikony v projektu](media/UWP-control-custom-icon.png)

> [!Note]
> Pro nativní ovládací prvky je nutné umístit ikonu jako prostředek v projektu `design.dll`.

## <a name="support-specific-windows-platform-versions"></a>Podporují konkrétní verze platformy Windows.

Balíčky UWP mají TargetPlatformVersion (TPV) a TargetPlatformMinVersion (TPMinV), které definují horní a dolní meze verze operačního systému, kde se dá aplikace nainstalovat. TPV dále určuje verzi sady SDK, proti které je aplikace sestavena. Nezapomeňte na tyto vlastnosti při vytváření balíčku UWP: použití rozhraní API mimo hranice verzí platforem definované v aplikaci způsobí selhání sestavení nebo selhání aplikace za běhu.

Řekněme například, že jste nastavili TPMinV pro balíček Controls na Windows 10 výročí Edition (10,0; Sestavení 14393), aby bylo zajištěno, že balíček je spotřebován pouze projekty UWP, které odpovídají danému dolnímu omezení. Chcete-li, aby bylo možné balíček využívat v projektech UWP, je nutné zabalit ovládací prvky s následujícími názvy složek:

    \lib\uap10.0.14393\*
    \ref\uap10.0.14393\*

NuGet bude automaticky kontrolovat TPMinV projektu, a pokud je nižší než Windows 10 výročí Edition (10,0;), instalace selže. Sestavení 14393)

V případě WPF řekněme, že chcete, aby váš balíček WPF Controls byly spotřebované projekty, které cílí na .NET Framework v 4.6.1 nebo vyšší. Aby bylo možné tento postup vyhovět, je nutné zabalit ovládací prvky s následujícími názvy složek:

    \lib\net461\*
    \ref\net461\*

## <a name="add-design-time-support"></a>Přidání podpory pro dobu návrhu

Chcete-li nakonfigurovat, kde se vlastnosti ovládacího prvku zobrazí v inspektoru vlastností, přidejte vlastní doplňky atd., umístěte soubor `design.dll` do složky `lib\uap10.0.14393\Design` tak, aby odpovídala cílové platformě. Aby bylo zajištěno, že funkce **[Upravit šablonu > upravit kopírování](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** funguje, je nutné zahrnout `Generic.xaml` a všechny slovníky prostředků, které se sloučí do složky `<your_assembly_name>\Themes` (znovu pomocí vlastního názvu sestavení). (Tento soubor nemá žádný vliv na chování za běhu ovládacího prvku.) Struktura složek by tedy vypadala takto:

    \lib
      \uap10.0.14393
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml


V případě WPF pokračuje v příkladu, kde chcete, aby byl balíček WPF ovládací prvky spotřebován projekty cílené na .NET Framework v 4.6.1 nebo vyšší:

    \lib
      \net461
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> Ve výchozím nastavení se vlastnosti ovládacího prvku zobrazí pod kategorií různé v inspektoru vlastností.

## <a name="use-strings-and-resources"></a>Použití řetězců a prostředků

Do balíčku můžete vkládat řetězcové prostředky (`.resw`), které lze použít pro ovládací prvek nebo zpracování projektu UWP, nastavením vlastnosti **Akce sestavení** `.resw` souboru na **PRIResource**.

Příklad naleznete v tématu [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) v ukázce ExtensionSDKasNuGetPackage.

> [!Note]
> To platí pouze pro ovládací prvky UWP.

## <a name="see-also"></a>Viz také:

- [Vytvoření balíčků UPW](create-uwp-packages.md)
- [Ukázka ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
