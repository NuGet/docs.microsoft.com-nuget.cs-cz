---
title: Jak k ovládacím prvkům UWP balíček s NuGet
description: Postup vytvoření balíčků NuGet, které obsahují UWP řídí včetně nezbytné metadata a podpůrné soubory pro Visual Studio a nástroj Blend návrháře.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/14/2018
ms.topic: tutorial
ms.openlocfilehash: 963846e857c8757176e4fbe1cd60c92a7397ba01
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
---
# <a name="creating-uwp-controls-as-nuget-packages"></a>Vytváření ovládacích prvků UPW jako balíčků NuGet

Visual Studio 2017 můžete využít přidané možnosti pro ovládací prvky UWP přinášející balíčky NuGet. Tento průvodce vás provede tyto možnosti [ExtensionSDKasNuGetPackage ukázka](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage). 

## <a name="prerequisites"></a>Požadavky

1. Visual Studio 2017
1. Přehled o tom, jak [vytvořit balíčky UWP](create-uwp-packages.md)

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

Například Řekněme, že jste nastavili TPMinV pro ovládací prvky balíček Windows 10 Anniversary Edition (10.0; Sestavení 14393), takže chcete zajistit, že balíček je spotřebovávají pouze UWP projekty odpovídající dolní mez. Povolit vašeho balíčku pro projekty UWP, musí balíček vaše ovládací prvky s následující názvy složek:

    \lib\uap10.0\*
    \ref\uap10.0\*

K vynucení příslušné kontroly TPMinV, vytvořit [souboru cíle MSBuild](/visualstudio/msbuild/msbuild-targets) a balíček je v části `build\uap10.0" folder as `.targets < your_assembly_name >`, replacing `< your_assembly_name >' s názvem konkrétní sestavení.

Tady je příklad, jak by měla vypadat soubor cíle:

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

  <Target Name="TPMinVCheck" BeforeTargets="ResolveAssemblyReferences" Condition="'$(TargetPlatformMinVersion)' != ''">
    <PropertyGroup>
      <RequiredTPMinV>10.0.14393</RequiredTPMinV>
      <ActualTPMinV>$(TargetPlatformMinVersion)</ActualTPMinV>
    </PropertyGroup>
    <Error Condition=" '$([System.Version]::Parse($(ActualTPMinV)).CompareTo($([System.Version]::Parse($(RequiredTPMinV)))))' == '-1' "        Text = "The INSERT_PACKAGE_ID_HERE nuget package cannot be used in the $(MSBuildProjectName) project since the project's TargetPlatformMinVersion - $(ActualTPMinV) does not match the Minimum Version - $(RequiredTPMinV) supported by the package" />
  </Target>
</Project>
```

## <a name="add-design-time-support"></a>Přidání podpory návrhu

Konfigurace, kde vlastnosti ovládacích prvků zobrazí v inspector vlastnost, přidejte vlastní ozdobného prvku atd., umístěte vaše `design.dll` souboru uvnitř `lib\uap10.0\Design` složku v závislosti na cílové platformy. Také zajistit, aby **[upravit šablonu > Upravit kopii](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** funkce funguje, je nutné zahrnout `Generic.xaml` a všechny slovnících prostředků, které se sloučí v `<your_assembly_name>\Themes` složky (znovu s použitím název vašeho skutečné sestavení). (Tento soubor nemá žádný vliv na modul runtime chování ovládacího prvku.) Struktura složek by proto vypadat takto:

    \lib
      \uap10.0
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

## <a name="package-content-such-as-images"></a>Obsah balíčku, jako jsou bitové kopie

Do balíčku obsahu, například bitové kopie, které mohou být využívána vlastní ovládací prvek nebo využívání projektu UPW, umístěte těchto souborů v rámci `lib\uap10.0` složky.

Mohou také vytvářet [souboru cíle MSBuild](/visualstudio/msbuild/msbuild-targets) zajistit asset se zkopíruje do výstupní složky náročné projektu:

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Content Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0\contosoSampleImage.jpg">
            <CopyToOutputDirectory>Always</CopyToOutputDirectory>
        </Content>
    </ItemGroup>
</Project>
```

## <a name="see-also"></a>Viz také

- [Vytvoření balíčků UPW](create-uwp-packages.md)
- [Ukázka ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
