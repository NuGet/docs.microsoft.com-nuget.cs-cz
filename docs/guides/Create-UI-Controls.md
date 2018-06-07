---
title: Jak zabalit ovládacích prvků uživatelského rozhraní s NuGet
description: Postup vytvoření balíčků NuGet, které obsahují UWP nebo WPF ovládací prvky, včetně potřeby metadata a podpůrné soubory pro Visual Studio a nástroj Blend návrháře.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: ab7499c415f63319fd314f33607f74d400b5f957
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818654"
---
# <a name="creating-ui-controls-as-nuget-packages"></a>Vytváření ovládacích prvků uživatelského rozhraní jako balíčků NuGet

Visual Studio 2017 můžete využít přidaných funkcí pro UPW a WPF ovládacích prvků, které doručit do balíčků NuGet. Tento průvodce vás provede tyto funkce v kontextu UWP ovládacích prvků pomocí [ExtensionSDKasNuGetPackage ukázka](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage). Totéž platí i pro ovládacích prvků WPF Jestliže není uvedeno jinak.

## <a name="prerequisites"></a>Požadavky

1. Visual Studio 2017
1. Přehled o tom, jak [vytvořit balíčky UWP](create-uwp-packages.md)

## <a name="generate-library-layout"></a>Generovat knihovny rozložení

> [!Note]
> To se vztahuje pouze na UWP ovládací prvky.

Nastavení `GenerateLibraryLayout` vlastnost zajistí, že je v rozložení, který je připraven k zabalené bez nutnosti položky jednotlivých souborů v soubor nuspec vygenerováno výstupu sestavení projektu.

Z vlastností projektu přejděte na kartu sestavení a zaškrtnutím políčka "Generovat knihovny rozložení". Tato akce upravit soubor projektu a nastavit `GenerateLibraryLayout` příznak na hodnotu true pro aktuálně vybrané konfigurace sestavení a platformu.

Můžete také upravit souboru projektu přidejte `<GenerateLibraryLayout>true</GenerateLibraryLayout>` ke skupině první nepodmíněné vlastnost. To platí vlastnost bez ohledu na platformu a konfigurace sestavení.

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a>Přidání podpory podokna nástrojů nebo prostředky pro ovládací prvky jazyka XAML

Pokud chcete, aby ovládacího prvku XAML, zobrazí v sadě nástrojů Návrhář XAML v sadě Visual Studio a podokně prostředky Blend, vytvořte `VisualStudioToolsManifest.xml` soubor v kořenovém `tools` složky balíčku projektu. Tento soubor se nevyžaduje, pokud nepotřebujete, než se objeví v soupravy nástrojů nebo prostředky podokně ovládacího prvku.

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

- *your_package_file*: soubor název vlastního ovládacího prvku, třeba `ManagedPackage.winmd` ("ManagedPackage" je libovolnou s názvem používá v tomto příkladu a nemá žádný další význam).
- *vs_category*: štítek pro skupinu, ve kterém by se měla objevit ovládací prvek v sadě nástrojů Visual Studio designer. A `VSCategory` je nezbytné pro ovládací prvek se objeví v panelu nástrojů.
- *blend_category*: štítek pro skupinu, ve kterém by se měla objevit ovládacího prvku v podokně prostředky návrháře Blend. A `BlendCategory` je nezbytné pro ovládací prvek zobrazí v prostředky.
- *type_full_name_n*: plně kvalifikovaný název pro každý ovládací prvek, včetně oboru názvů, jako například `ManagedPackage.MyCustomControl`. Všimněte si, že formát tečkou se používá pro spravovaná a nativní typy.

V pokročilejších scénářích, můžete použít také více `<File>` elementů v rámci `<FileList>` když jeden balíček obsahuje více sestavení ovládacího prvku. Také můžete mít více `<ToolboxItems>` uzly v rámci jednoho `<File>` Pokud budete chtít uspořádání ovládacích prvků do samostatných kategorií.

V následujícím příkladu ovládacího prvku implementované v `ManagedPackage.winmd` se zobrazí v sadě Visual Studio a přizpůsobte ve skupině s názvem "Spravované balíček" a "MyCustomControl" se zobrazí v této skupině. Všechny tyto názvy jsou libovolný.

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![Ovládací prvek příklad, jak se objeví v sadě Visual Studio](media/UWP-control-vs-toolbox.png)

![Ovládací prvek příklad, jak se zobrazují v programu Blend](media/UWP-control-blend-assets.png)

> [!Note]
> Je třeba explicitně zadat každý ovládací prvek, který chcete zobrazit v podokně nástrojů nebo prostředky. Ujistěte se, zadejte ve formátu `Namespace.ControlName`.

## <a name="add-custom-icons-to-your-controls"></a>Přidat vlastní ikony pro vaše ovládací prvky

Vlastní ikonu na panelu nástrojů nebo prostředky zobrazíte přidat bitovou kopii do projektu nebo odpovídající `design.dll` projektu s názvem "Namespace.ControlName.extension" a nastavte akce sestavení "Vložený prostředek". Podporované formáty jsou `.png`, `.jpg`, `.jpeg`, `.gif`, a `.bmp`. Doporučené obrázek je 64 × 64 pixelů.

V následujícím příkladu projekt obsahuje soubor bitové kopie s názvem "ManagedPackage.MyCustomControl.png".

![Nastavení vlastní ikonou v projektu](media/UWP-control-custom-icon.png)

> [!Note]
> Pro nativní ovládací prvky, musíte umístit na ikonu jako prostředek v `design.dll` projektu.

## <a name="support-specific-windows-platform-versions"></a>Podporují konkrétní verze platformy Windows

Balíčky UWP mít TargetPlatformVersion (TPV) a TargetPlatformMinVersion (TPMinV), které definují horní a dolní meze verze operačního systému nainstalovanou aplikaci. Další TPV Určuje verzi sady SDK, pro kterou je integrovaná aplikace. Mějte na paměti tyto vlastnosti při vytváření balíčku UWP: použití rozhraní API mimo hranice verze platforem, které jsou definované v aplikaci způsobí selhání sestavení nebo aplikaci k selhání za běhu.

Například Řekněme, že jste nastavili TPMinV pro vaše ovládací prvky balíček do Windows 10 Anniversary Edition (10.0; Sestavení 14393), takže chcete zajistit, že balíček je spotřebovávají pouze UWP projekty odpovídající dolní mez. Povolit vašeho balíčku pro projekty UWP, musí balíček vaše ovládací prvky s následující názvy složek:

    \lib\uap10.0.14393\*
    \ref\uap10.0.14393\*

NuGet automaticky zkontroluje TPMinV náročné projektu a pokud je nižší než Windows 10 Anniversary Edition (10.0; selhat instalace Sestavení 14393)

V případě WPF Řekněme, že byste chtěli vašeho balíčku ovládacích prvků WPF spotřebované projekty cílení na rozhraní .NET Framework v4.6.1 nebo vyšší. Pokud chcete vynutit, který, musí balíček vaše ovládací prvky s následující názvy složek:

    \lib\net461\*
    \ref\net461\*

## <a name="add-design-time-support"></a>Přidání podpory návrhu

Konfigurace, kde vlastnosti ovládacích prvků zobrazí v inspector vlastnost, přidejte vlastní ozdobného prvku atd., umístěte vaše `design.dll` souboru uvnitř `lib\uap10.0.14393\Design` složku v závislosti na cílové platformy. Také zajistit, aby **[upravit šablonu > Upravit kopii](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** funkce funguje, je nutné zahrnout `Generic.xaml` a všechny slovnících prostředků, které se sloučí v `<your_assembly_name>\Themes` složky (znovu s použitím název vašeho skutečné sestavení). (Tento soubor nemá žádný vliv na modul runtime chování ovládacího prvku.) Struktura složek by proto vypadat takto:

    \lib
      \uap10.0.14393
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml


Pro grafický subsystém WPF pokračování příkladu s, kam chcete vaší WPF prvky balíček spotřebované projekty cílení na rozhraní .NET Framework v4.6.1 nebo vyšší:

    \lib
      \net461
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> Ve výchozím nastavení vlastností ovládacího prvku se zobrazí na různé kategorie v inspector vlastnost.

## <a name="use-strings-and-resources"></a>Použití řetězců a prostředky

Můžete vložit řetězcové prostředky (`.resw`) do balíčku, který můžete použít vlastní ovládací prvek nebo využívání projektu UPW, nastavte **akce sestavení** vlastnost `.resw` do souboru **PRIResource**.

Příklad najdete v části [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) v ukázce ExtensionSDKasNuGetPackage.

> [!Note]
> To se vztahuje pouze na UWP ovládací prvky.

## <a name="see-also"></a>Viz také:

- [Vytvoření balíčků UPW](create-uwp-packages.md)
- [Ukázka ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
