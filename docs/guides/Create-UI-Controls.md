---
title: Jak zabalit ovládací prvky uživatelského rozhraní pomocí NuGet
description: Vytvoření balíčků NuGet, které obsahují ovládací prvky UWP nebo WPF, včetně nezbytných metadat a podpůrných souborů pro návrháře sady Visual Studio a Blendu.
author: JonDouglas
ms.author: jodou
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: 317937b4d9d773d74384b8ebfcd2146062236ac1
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774325"
---
# <a name="creating-ui-controls-as-nuget-packages"></a><span data-ttu-id="adaad-103">Vytvoření ovládacích prvků uživatelského rozhraní jako balíčků NuGet</span><span class="sxs-lookup"><span data-stu-id="adaad-103">Creating UI controls as NuGet packages</span></span>

<span data-ttu-id="adaad-104">Počínaje sadou Visual Studio 2017 můžete využít výhod přidaných funkcí pro ovládací prvky UWP a WPF, které zadáváte do balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="adaad-104">Starting with Visual Studio 2017, you can take advantage of added capabilities for UWP and WPF controls that you deliver in NuGet packages.</span></span> <span data-ttu-id="adaad-105">Tato příručka vás provede následujícími možnostmi v kontextu ovládacích prvků UWP pomocí [ukázky ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span><span class="sxs-lookup"><span data-stu-id="adaad-105">This guide walks you through these capabilities in context of UWP controls using the [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span></span> <span data-ttu-id="adaad-106">Totéž platí pro ovládací prvky WPF, pokud není uvedeno jinak.</span><span class="sxs-lookup"><span data-stu-id="adaad-106">The same applies to WPF controls unless mentioned otherwise.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="adaad-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="adaad-107">Prerequisites</span></span>

1. <span data-ttu-id="adaad-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="adaad-108">Visual Studio 2017</span></span>
1. <span data-ttu-id="adaad-109">Informace o tom, jak [vytvářet balíčky UWP](create-uwp-packages.md)</span><span class="sxs-lookup"><span data-stu-id="adaad-109">Understanding of how to [Create UWP Packages](create-uwp-packages.md)</span></span>

## <a name="generate-library-layout"></a><span data-ttu-id="adaad-110">Generovat rozložení knihovny</span><span class="sxs-lookup"><span data-stu-id="adaad-110">Generate Library Layout</span></span>

> [!Note]
> <span data-ttu-id="adaad-111">To platí pouze pro ovládací prvky UWP.</span><span class="sxs-lookup"><span data-stu-id="adaad-111">This is applicable only to UWP controls.</span></span>

<span data-ttu-id="adaad-112">Nastavení `GenerateLibraryLayout` vlastnosti zajistí, že výstup sestavení projektu bude vygenerován v rozložení, které je připraveno k zabalení bez nutnosti jednotlivých položek souborů v nuspec.</span><span class="sxs-lookup"><span data-stu-id="adaad-112">Setting the `GenerateLibraryLayout` property ensures that the project build output is generated in a layout that is ready to be packaged without the need for individual file entries in the nuspec.</span></span>

<span data-ttu-id="adaad-113">Z vlastností projektu, přejít na kartu sestavení a zaškrtněte políčko Generovat rozložení knihovny.</span><span class="sxs-lookup"><span data-stu-id="adaad-113">From the project properties, go to the build tab and check the "Generate Library Layout" check box.</span></span> <span data-ttu-id="adaad-114">Tím se upraví soubor projektu a nastaví `GenerateLibraryLayout` příznak na hodnotu true pro aktuálně vybranou konfiguraci a platformu sestavení.</span><span class="sxs-lookup"><span data-stu-id="adaad-114">This will modify the project file and set the `GenerateLibraryLayout` flag to true for your currently selected build configuration and platform.</span></span>

<span data-ttu-id="adaad-115">Případně upravte soubor projektu tak, aby se přidal `<GenerateLibraryLayout>true</GenerateLibraryLayout>` do první nepodmíněné skupiny vlastností.</span><span class="sxs-lookup"><span data-stu-id="adaad-115">Alternately, edit the the project file to add `<GenerateLibraryLayout>true</GenerateLibraryLayout>` to the first unconditional property group.</span></span> <span data-ttu-id="adaad-116">Tato vlastnost by se použila bez ohledu na konfiguraci sestavení a platformu.</span><span class="sxs-lookup"><span data-stu-id="adaad-116">This would apply the property irrespective of the build configuration and platform.</span></span>

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a><span data-ttu-id="adaad-117">Přidání podpory nástrojů/panelu nástrojů pro ovládací prvky XAML</span><span class="sxs-lookup"><span data-stu-id="adaad-117">Add toolbox/assets pane support for XAML controls</span></span>

<span data-ttu-id="adaad-118">Chcete-li, aby se ovládací prvek XAML zobrazil v sadě nástrojů návrháře XAML v sadě Visual Studio a v podokně prostředky v Blendu, vytvořte `VisualStudioToolsManifest.xml` soubor v kořenovém adresáři `tools` složky projektu balíčku.</span><span class="sxs-lookup"><span data-stu-id="adaad-118">To have a XAML control appear in the XAML designer’s toolbox in Visual Studio and the Assets pane of Blend, create a `VisualStudioToolsManifest.xml` file in the root of the `tools` folder of your package project.</span></span> <span data-ttu-id="adaad-119">Tento soubor není povinný, pokud nepotřebujete, aby se ovládací prvek zobrazoval v podokně nástrojů nebo aktiv.</span><span class="sxs-lookup"><span data-stu-id="adaad-119">This file is not required if you don’t need the control to appear in the toolbox or Assets pane.</span></span>

```
\build
\lib
\tools
    VisualStudioToolsManifest.xml
```

<span data-ttu-id="adaad-120">Struktura souboru je následující:</span><span class="sxs-lookup"><span data-stu-id="adaad-120">The structure of the file is as follows:</span></span>

```xml
<FileList>
  <File Reference = "your_package_file">
    <ToolboxItems UIFramework="WPF" VSCategory="vs_category" BlendCategory="blend_category">
      <Item Type="type_full_name_1" />

      <!-- Any number of additional Items -->
      <Item Type="type_full_name_2" />
      <Item Type="type_full_name_3" />
    </ToolboxItems>
  </File>
</FileList>
```

<span data-ttu-id="adaad-121">kde:</span><span class="sxs-lookup"><span data-stu-id="adaad-121">where:</span></span>

- <span data-ttu-id="adaad-122">*your_package_file*: název řídicího souboru, například `ManagedPackage.winmd` ("ManagedPackage", je libovolný název, který se používá pro tento příklad a nemá žádný jiný význam).</span><span class="sxs-lookup"><span data-stu-id="adaad-122">*your_package_file*: the name of your control file, such as `ManagedPackage.winmd` ("ManagedPackage" is an arbitrary named used for this example and has no other meaning).</span></span>
- <span data-ttu-id="adaad-123">*vs_category*: popisek skupiny, ve které by se měl ovládací prvek zobrazit v sadě nástrojů Visual Studio designer.</span><span class="sxs-lookup"><span data-stu-id="adaad-123">*vs_category*: The label for the group in which the control should appear in the Visual Studio designer’s toolbox.</span></span> <span data-ttu-id="adaad-124">`VSCategory`Je nutné, aby se ovládací prvek zobrazil v sadě nástrojů.</span><span class="sxs-lookup"><span data-stu-id="adaad-124">A `VSCategory` is necessary for the control to appear in the toolbox.</span></span>
<span data-ttu-id="adaad-125">*ui_framework*: název rozhraní, například WPF, Upozorňujeme, že `UIFramework` atribut je vyžadován v uzlech ToolboxItems v sadě Visual Studio 16,7 Preview 3 nebo vyšší, aby se ovládací prvek zobrazil v sadě nástrojů.</span><span class="sxs-lookup"><span data-stu-id="adaad-125">*ui_framework*: The name of the Framework, such as 'WPF', note that `UIFramework` attribute is required on ToolboxItems nodes on Visual Studio 16.7 Preview 3 or above for the control to appear in toolbox.</span></span>
- <span data-ttu-id="adaad-126">*blend_category*: popisek skupiny, ve které by se měl ovládací prvek zobrazit v podokně assets návrháře Blendu.</span><span class="sxs-lookup"><span data-stu-id="adaad-126">*blend_category*: The label for the group in which the control should appear in the Blend designer’s Assets pane.</span></span> <span data-ttu-id="adaad-127">`BlendCategory`Je nutné, aby se ovládací prvek objevil v prostředcích.</span><span class="sxs-lookup"><span data-stu-id="adaad-127">A `BlendCategory` is necessary for the control to appear in Assets.</span></span>
- <span data-ttu-id="adaad-128">*type_full_name_n*: plně kvalifikovaný název pro každý ovládací prvek, včetně oboru názvů, jako je například `ManagedPackage.MyCustomControl` .</span><span class="sxs-lookup"><span data-stu-id="adaad-128">*type_full_name_n*: The fully-qualified name for each control, including the namespace, such as `ManagedPackage.MyCustomControl`.</span></span> <span data-ttu-id="adaad-129">Všimněte si, že formát tečky se používá pro spravované i nativní typy.</span><span class="sxs-lookup"><span data-stu-id="adaad-129">Note that the dot format is used for both managed and native types.</span></span>

<span data-ttu-id="adaad-130">V pokročilejších scénářích můžete také zahrnout více `<File>` prvků v případě, že `<FileList>` jeden balíček obsahuje více sestavení ovládacích prvků.</span><span class="sxs-lookup"><span data-stu-id="adaad-130">In more advanced scenarios, you can also include multiple `<File>` elements within `<FileList>` when a single package contains multiple control assemblies.</span></span> <span data-ttu-id="adaad-131">Můžete mít také více `<ToolboxItems>` uzlů v rámci jednoho `<File>` , pokud chcete uspořádat ovládací prvky do samostatných kategorií.</span><span class="sxs-lookup"><span data-stu-id="adaad-131">You can also have multiple `<ToolboxItems>` nodes within a single `<File>` if you want to organize your controls into separate categories.</span></span>

<span data-ttu-id="adaad-132">V následujícím příkladu se ovládací prvek implementovaný v nástroji `ManagedPackage.winmd` zobrazí v aplikaci Visual Studio a Blend ve skupině s názvem "Managed Package" a "MyCustomControl" se zobrazí v této skupině.</span><span class="sxs-lookup"><span data-stu-id="adaad-132">In the following example, the control implemented in `ManagedPackage.winmd` will appear in Visual Studio and Blend in a group named “Managed Package”, and “MyCustomControl” will appear in that group.</span></span> <span data-ttu-id="adaad-133">Všechny tyto názvy jsou libovolné.</span><span class="sxs-lookup"><span data-stu-id="adaad-133">All these names are arbitrary.</span></span>

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems UIFramework="WPF" VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![Příklad ovládacího prvku, který se zobrazí v aplikaci Visual Studio](media/UWP-control-vs-toolbox.png)

![Vzorový ovládací prvek, který se zobrazí v Blendu](media/UWP-control-blend-assets.png)

> [!Note]
> <span data-ttu-id="adaad-136">Každý ovládací prvek, který byste chtěli zobrazit v podokně Sada nástrojů/prostředky, musíte explicitně zadat.</span><span class="sxs-lookup"><span data-stu-id="adaad-136">You must explicitly specify every control that you would like to see in the toolbox/assets pane.</span></span> <span data-ttu-id="adaad-137">Ujistěte se, že je zadáte ve formátu `Namespace.ControlName` .</span><span class="sxs-lookup"><span data-stu-id="adaad-137">Ensure you specify them in the format `Namespace.ControlName`.</span></span>

## <a name="add-custom-icons-to-your-controls"></a><span data-ttu-id="adaad-138">Přidat vlastní ikony do ovládacích prvků</span><span class="sxs-lookup"><span data-stu-id="adaad-138">Add custom icons to your controls</span></span>

<span data-ttu-id="adaad-139">Chcete-li zobrazit vlastní ikonu v podokně Sada nástrojů/assets, přidejte do projektu obrázek nebo odpovídající `design.dll` projekt s názvem "obor názvů. Control. Extension" a nastavte akci sestavení na "Integrovaný prostředek".</span><span class="sxs-lookup"><span data-stu-id="adaad-139">To display a custom icon in the toolbox/assets pane, add an image to your project or the corresponding `design.dll` project with the name “Namespace.ControlName.extension” and set the build action to “Embedded Resource”.</span></span> <span data-ttu-id="adaad-140">Musíte také zajistit, aby vlastnost asociované `AssemblyInfo.cs` určovala atribut ProvideMetadata- `[assembly: ProvideMetadata(typeof(RegisterMetadata))]` .</span><span class="sxs-lookup"><span data-stu-id="adaad-140">You must also ensure that the associated `AssemblyInfo.cs` specifies the ProvideMetadata attribute - `[assembly: ProvideMetadata(typeof(RegisterMetadata))]`.</span></span> <span data-ttu-id="adaad-141">Podívejte se na tuto [ukázku](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20).</span><span class="sxs-lookup"><span data-stu-id="adaad-141">See this [sample](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20).</span></span>

<span data-ttu-id="adaad-142">Podporované formáty jsou `.png` , `.jpg` ,, a `.jpeg` `.gif` `.bmp` .</span><span class="sxs-lookup"><span data-stu-id="adaad-142">Supported formats are `.png`, `.jpg`, `.jpeg`, `.gif`, and `.bmp`.</span></span> <span data-ttu-id="adaad-143">Doporučený formát je BMP24 v rozmezí 16 × 16 pixelů.</span><span class="sxs-lookup"><span data-stu-id="adaad-143">The recommended format is BMP24 in 16 pixels by 16 pixels.</span></span>

![Ukázka ikony pole nástrojů](https://raw.githubusercontent.com/NuGet/docs.microsoft.com-nuget/live/docs/guides/media/ColorPicker_16x16x24.bmp)

<span data-ttu-id="adaad-145">Růžová pozadí je nahrazena za běhu.</span><span class="sxs-lookup"><span data-stu-id="adaad-145">The pink background is replaced at runtime.</span></span> <span data-ttu-id="adaad-146">Když se změní motiv sady Visual Studio a očekává se barva pozadí, jsou ikony Přebarvené.</span><span class="sxs-lookup"><span data-stu-id="adaad-146">The icons are recolored when the Visual Studio theme is changed and that background color is expected.</span></span> <span data-ttu-id="adaad-147">Další informace najdete v referenčních [obrázcích a ikonách pro Visual Studio](/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="adaad-147">For more information, please reference [Images and Icons for Visual Studio](/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio).</span></span>

<span data-ttu-id="adaad-148">V následujícím příkladu obsahuje projekt soubor s obrázkem s názvem "ManagedPackage.MyCustomControl.png".</span><span class="sxs-lookup"><span data-stu-id="adaad-148">In the example below, the project contains an image file named “ManagedPackage.MyCustomControl.png”.</span></span>

![Nastavení vlastní ikony v projektu](media/UWP-control-custom-icon.png)

> [!Note]
> <span data-ttu-id="adaad-150">Pro nativní ovládací prvky je nutné umístit ikonu jako prostředek v `design.dll` projektu.</span><span class="sxs-lookup"><span data-stu-id="adaad-150">For native controls, you must put the icon as a resource in the `design.dll` project.</span></span>

## <a name="support-specific-windows-platform-versions"></a><span data-ttu-id="adaad-151">Podporují konkrétní verze platformy Windows.</span><span class="sxs-lookup"><span data-stu-id="adaad-151">Support specific Windows platform versions</span></span>

<span data-ttu-id="adaad-152">Balíčky UWP mají TargetPlatformVersion (TPV) a TargetPlatformMinVersion (TPMinV), které definují horní a dolní meze verze operačního systému, kde se dá aplikace nainstalovat.</span><span class="sxs-lookup"><span data-stu-id="adaad-152">UWP packages have a TargetPlatformVersion (TPV) and TargetPlatformMinVersion (TPMinV) that define the upper and lower bounds of the OS version where the app can be installed.</span></span> <span data-ttu-id="adaad-153">TPV dále určuje verzi sady SDK, proti které je aplikace sestavena.</span><span class="sxs-lookup"><span data-stu-id="adaad-153">TPV further specifies the version of the SDK against which the app is built.</span></span> <span data-ttu-id="adaad-154">Nezapomeňte na tyto vlastnosti při vytváření balíčku UWP: použití rozhraní API mimo hranice verzí platforem definované v aplikaci způsobí selhání sestavení nebo selhání aplikace za běhu.</span><span class="sxs-lookup"><span data-stu-id="adaad-154">Be mindful of these properties when authoring a UWP package: using APIs outside the bounds of the platform versions defined in the app will cause either the build to fail or the app to fail at runtime.</span></span>

<span data-ttu-id="adaad-155">Řekněme například, že jste nastavili TPMinV pro balíček Controls na Windows 10 výročí Edition (10,0; Sestavení 14393), aby bylo zajištěno, že balíček je spotřebován pouze projekty UWP, které odpovídají danému dolnímu omezení.</span><span class="sxs-lookup"><span data-stu-id="adaad-155">For example, let’s say you’ve set the TPMinV for your controls package to Windows 10 Anniversary Edition (10.0; Build 14393), so you want to ensure that the package is consumed only by UWP projects that match that lower bound.</span></span> <span data-ttu-id="adaad-156">Chcete-li, aby bylo možné balíček využívat v projektech UWP, je nutné zabalit ovládací prvky s následujícími názvy složek:</span><span class="sxs-lookup"><span data-stu-id="adaad-156">To allow your package to be consumed by UWP projects, you must package your controls with the following folder names:</span></span>

```
\lib\uap10.0.14393\*
\ref\uap10.0.14393\*
```

<span data-ttu-id="adaad-157">NuGet bude automaticky kontrolovat TPMinV projektu, a pokud je nižší než Windows 10 výročí Edition (10,0;), instalace selže. Sestavení 14393)</span><span class="sxs-lookup"><span data-stu-id="adaad-157">NuGet will automatically check the TPMinV of the consuming project, and fail installation if it is lower than Windows 10 Anniversary Edition (10.0; Build 14393)</span></span>

<span data-ttu-id="adaad-158">V případě WPF řekněme, že chcete, aby váš balíček WPF Controls byly spotřebované projekty, které cílí na .NET Framework v 4.6.1 nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="adaad-158">In case of WPF, let's say you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher.</span></span> <span data-ttu-id="adaad-159">Aby bylo možné tento postup vyhovět, je nutné zabalit ovládací prvky s následujícími názvy složek:</span><span class="sxs-lookup"><span data-stu-id="adaad-159">To enforce that, you must package your controls with the following folder names:</span></span>

```
\lib\net461\*
\ref\net461\*
```

## <a name="add-design-time-support"></a><span data-ttu-id="adaad-160">Přidání podpory pro dobu návrhu</span><span class="sxs-lookup"><span data-stu-id="adaad-160">Add design-time support</span></span>

<span data-ttu-id="adaad-161">Chcete-li nakonfigurovat, kde se vlastnosti ovládacího prvku zobrazí v inspektoru vlastností, přidejte vlastní doplňky atd., umístěte `design.dll` soubor do `lib\uap10.0.14393\Design` složky tak, aby odpovídala cílové platformě.</span><span class="sxs-lookup"><span data-stu-id="adaad-161">To configure where the control properties show up in the property inspector, add custom adorners, etc., place your `design.dll` file inside the `lib\uap10.0.14393\Design` folder as appropriate to the target platform.</span></span> <span data-ttu-id="adaad-162">Aby bylo zajištěno, že funkce **[Upravit šablonu > upravit kopírování](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** funguje, je nutné zahrnout do `Generic.xaml` složky všechny slovníky prostředků, které se ve složce sloučí `<your_assembly_name>\Themes` (znovu pomocí vlastního názvu sestavení).</span><span class="sxs-lookup"><span data-stu-id="adaad-162">Also, to ensure that the **[Edit Template > Edit a Copy](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** feature works, you must include the `Generic.xaml` and any resource dictionaries that it merges in the `<your_assembly_name>\Themes` folder (again, using your actual assembly name).</span></span> <span data-ttu-id="adaad-163">(Tento soubor nemá žádný vliv na chování za běhu ovládacího prvku.) Struktura složek by tedy vypadala takto:</span><span class="sxs-lookup"><span data-stu-id="adaad-163">(This file has no impact on the runtime behavior of a control.) The folder structure would thus appear as follows:</span></span>

```
\lib
  \uap10.0.14393
    \Design
      \MyControl.design.dll
    \your_assembly_name
      \Themes
        Generic.xaml
```

<span data-ttu-id="adaad-164">V případě WPF pokračuje v příkladu, kde chcete, aby byl balíček WPF ovládací prvky spotřebován projekty cílené na .NET Framework v 4.6.1 nebo vyšší:</span><span class="sxs-lookup"><span data-stu-id="adaad-164">For WPF, continuing with the example where you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher:</span></span>

```
\lib
  \net461
    \Design
      \MyControl.design.dll
    \your_assembly_name
      \Themes
        Generic.xaml
```

> [!Note]
> <span data-ttu-id="adaad-165">Ve výchozím nastavení se vlastnosti ovládacího prvku zobrazí pod kategorií různé v inspektoru vlastností.</span><span class="sxs-lookup"><span data-stu-id="adaad-165">By default, control properties will show up under the Miscellaneous category in the property inspector.</span></span>

## <a name="use-strings-and-resources"></a><span data-ttu-id="adaad-166">Použití řetězců a prostředků</span><span class="sxs-lookup"><span data-stu-id="adaad-166">Use strings and resources</span></span>

<span data-ttu-id="adaad-167">Do balíčku můžete vložit řetězcové prostředky ( `.resw` ), které lze použít v ovládacím prvku nebo v projektu UWP, nastavte vlastnost souboru **Akce sestavení** `.resw` na **PRIResource**.</span><span class="sxs-lookup"><span data-stu-id="adaad-167">You can embed string resources (`.resw`) in your package that can be used by your control or the consuming UWP project, set the **Build Action** property of the `.resw` file to **PRIResource**.</span></span>

<span data-ttu-id="adaad-168">Příklad naleznete v tématu [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) v ukázce ExtensionSDKasNuGetPackage.</span><span class="sxs-lookup"><span data-stu-id="adaad-168">For an example, refer to [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) in the ExtensionSDKasNuGetPackage sample.</span></span>

> [!Note]
> <span data-ttu-id="adaad-169">To platí pouze pro ovládací prvky UWP.</span><span class="sxs-lookup"><span data-stu-id="adaad-169">This is applicable only to UWP controls.</span></span>

## <a name="see-also"></a><span data-ttu-id="adaad-170">Viz také</span><span class="sxs-lookup"><span data-stu-id="adaad-170">See also</span></span>

- [<span data-ttu-id="adaad-171">Vytváření balíčků UWP</span><span class="sxs-lookup"><span data-stu-id="adaad-171">Create UWP Packages</span></span>](create-uwp-packages.md)
- [<span data-ttu-id="adaad-172">Ukázka ExtensionSDKasNuGetPackage</span><span class="sxs-lookup"><span data-stu-id="adaad-172">ExtensionSDKasNuGetPackage sample</span></span>](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)