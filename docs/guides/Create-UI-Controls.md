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
# <a name="creating-ui-controls-as-nuget-packages"></a><span data-ttu-id="58f49-103">Vytvoření ovládacích prvků uživatelského rozhraní jako balíčků NuGet</span><span class="sxs-lookup"><span data-stu-id="58f49-103">Creating UI controls as NuGet packages</span></span>

<span data-ttu-id="58f49-104">Počínaje Visual Studio 2017, můžete využít přidané možnosti pro OVLÁDACÍ PRVKY UPW a WPF, které dodáváte v balíčcích NuGet.</span><span class="sxs-lookup"><span data-stu-id="58f49-104">Starting with Visual Studio 2017, you can take advantage of added capabilities for UWP and WPF controls that you deliver in NuGet packages.</span></span> <span data-ttu-id="58f49-105">Tato příručka vás provede těmito funkcemi v kontextu ovládacích prvků UPW pomocí [ukázky ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span><span class="sxs-lookup"><span data-stu-id="58f49-105">This guide walks you through these capabilities in context of UWP controls using the [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span></span> <span data-ttu-id="58f49-106">Totéž platí pro ovládací prvky WPF, pokud není uvedeno jinak.</span><span class="sxs-lookup"><span data-stu-id="58f49-106">The same applies to WPF controls unless mentioned otherwise.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58f49-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="58f49-107">Prerequisites</span></span>

1. <span data-ttu-id="58f49-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="58f49-108">Visual Studio 2017</span></span>
1. <span data-ttu-id="58f49-109">Pochopení toho, jak [vytvořit balíčky UPW](create-uwp-packages.md)</span><span class="sxs-lookup"><span data-stu-id="58f49-109">Understanding of how to [Create UWP Packages](create-uwp-packages.md)</span></span>

## <a name="generate-library-layout"></a><span data-ttu-id="58f49-110">Generovat rozložení knihovny</span><span class="sxs-lookup"><span data-stu-id="58f49-110">Generate Library Layout</span></span>

> [!Note]
> <span data-ttu-id="58f49-111">To platí pouze pro ovládací prvky UPW.</span><span class="sxs-lookup"><span data-stu-id="58f49-111">This is applicable only to UWP controls.</span></span>

<span data-ttu-id="58f49-112">Nastavení `GenerateLibraryLayout` vlastnosti zajišťuje, že výstup sestavení projektu je generován v rozložení, které je připraveno k balení bez nutnosti jednotlivých položek souboru v nuspec.</span><span class="sxs-lookup"><span data-stu-id="58f49-112">Setting the `GenerateLibraryLayout` property ensures that the project build output is generated in a layout that is ready to be packaged without the need for individual file entries in the nuspec.</span></span>

<span data-ttu-id="58f49-113">Ve vlastnostech projektu přejděte na kartu sestavení a zaškrtněte políčko Generovat rozložení knihovny.</span><span class="sxs-lookup"><span data-stu-id="58f49-113">From the project properties, go to the build tab and check the "Generate Library Layout" check box.</span></span> <span data-ttu-id="58f49-114">Tím se změní soubor projektu `GenerateLibraryLayout` a nastaví příznak na hodnotu true pro aktuálně vybranou konfiguraci sestavení a platformu.</span><span class="sxs-lookup"><span data-stu-id="58f49-114">This will modify the project file and set the `GenerateLibraryLayout` flag to true for your currently selected build configuration and platform.</span></span>

<span data-ttu-id="58f49-115">Případně upravte soubor projektu, `<GenerateLibraryLayout>true</GenerateLibraryLayout>` který chcete přidat do první skupiny nepodmíněných vlastností.</span><span class="sxs-lookup"><span data-stu-id="58f49-115">Alternately, edit the the project file to add `<GenerateLibraryLayout>true</GenerateLibraryLayout>` to the first unconditional property group.</span></span> <span data-ttu-id="58f49-116">To by použít vlastnost bez ohledu na konfiguraci sestavení a platformu.</span><span class="sxs-lookup"><span data-stu-id="58f49-116">This would apply the property irrespective of the build configuration and platform.</span></span>

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a><span data-ttu-id="58f49-117">Přidání podpory panelu nástrojů/datových zdrojů pro ovládací prvky XAML</span><span class="sxs-lookup"><span data-stu-id="58f49-117">Add toolbox/assets pane support for XAML controls</span></span>

<span data-ttu-id="58f49-118">Chcete-li, aby se ovládací prvek XAML zobrazil v panelu nástrojů návrháře `VisualStudioToolsManifest.xml` XAML v `tools` sadě Visual Studio a podokně Prostředků blendu, vytvořte soubor v kořenovém adresáři složky projektu balíčku.</span><span class="sxs-lookup"><span data-stu-id="58f49-118">To have a XAML control appear in the XAML designer’s toolbox in Visual Studio and the Assets pane of Blend, create a `VisualStudioToolsManifest.xml` file in the root of the `tools` folder of your package project.</span></span> <span data-ttu-id="58f49-119">Tento soubor není vyžadován, pokud nepotřebujete ovládací prvek, který se zobrazí v panelu nástrojů nebo v podokně Datové zdroje.</span><span class="sxs-lookup"><span data-stu-id="58f49-119">This file is not required if you don’t need the control to appear in the toolbox or Assets pane.</span></span>

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

<span data-ttu-id="58f49-120">Struktura souboru je následující:</span><span class="sxs-lookup"><span data-stu-id="58f49-120">The structure of the file is as follows:</span></span>

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

<span data-ttu-id="58f49-121">kde:</span><span class="sxs-lookup"><span data-stu-id="58f49-121">where:</span></span>

- <span data-ttu-id="58f49-122">*your_package_file*: název řídicího souboru, například `ManagedPackage.winmd` ("ManagedPackage" je libovolně pojmenovaný pro tento příklad a nemá žádný jiný význam).</span><span class="sxs-lookup"><span data-stu-id="58f49-122">*your_package_file*: the name of your control file, such as `ManagedPackage.winmd` ("ManagedPackage" is an arbitrary named used for this example and has no other meaning).</span></span>
- <span data-ttu-id="58f49-123">*vs_category*: Popisek pro skupinu, ve kterém by měl být ovládací prvek zobrazen v panelu nástrojů návrháře sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="58f49-123">*vs_category*: The label for the group in which the control should appear in the Visual Studio designer’s toolbox.</span></span> <span data-ttu-id="58f49-124">A `VSCategory` je nezbytné pro ovládací prvek se zobrazí v panelu nástrojů.</span><span class="sxs-lookup"><span data-stu-id="58f49-124">A `VSCategory` is necessary for the control to appear in the toolbox.</span></span>
- <span data-ttu-id="58f49-125">*blend_category*: Popisek pro skupinu, ve které by se měl ovládací prvek zobrazit v podokně Datové zdroje návrháře prolnutí.</span><span class="sxs-lookup"><span data-stu-id="58f49-125">*blend_category*: The label for the group in which the control should appear in the Blend designer’s Assets pane.</span></span> <span data-ttu-id="58f49-126">A `BlendCategory` je nezbytné pro ovládací prvek se zobrazí v prostředky.</span><span class="sxs-lookup"><span data-stu-id="58f49-126">A `BlendCategory` is necessary for the control to appear in Assets.</span></span>
- <span data-ttu-id="58f49-127">*type_full_name_n*: Plně kvalifikovaný název pro každý ovládací prvek, `ManagedPackage.MyCustomControl`včetně oboru názvů, například .</span><span class="sxs-lookup"><span data-stu-id="58f49-127">*type_full_name_n*: The fully-qualified name for each control, including the namespace, such as `ManagedPackage.MyCustomControl`.</span></span> <span data-ttu-id="58f49-128">Všimněte si, že formát tečky se používá pro spravované i nativní typy.</span><span class="sxs-lookup"><span data-stu-id="58f49-128">Note that the dot format is used for both managed and native types.</span></span>

<span data-ttu-id="58f49-129">V pokročilejších scénářích můžete také `<File>` zahrnout `<FileList>` více prvků v rámci, když jeden balíček obsahuje více sestavení ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="58f49-129">In more advanced scenarios, you can also include multiple `<File>` elements within `<FileList>` when a single package contains multiple control assemblies.</span></span> <span data-ttu-id="58f49-130">Můžete mít také `<ToolboxItems>` více uzlů `<File>` v rámci jednoho, pokud chcete uspořádat ovládací prvky do samostatných kategorií.</span><span class="sxs-lookup"><span data-stu-id="58f49-130">You can also have multiple `<ToolboxItems>` nodes within a single `<File>` if you want to organize your controls into separate categories.</span></span>

<span data-ttu-id="58f49-131">V následujícím příkladu ovládací `ManagedPackage.winmd` prvek implementovaný v aplikaci se zobrazí v sadě Visual Studio a Blend ve skupině s názvem "Spravovaný balíček" a "MyCustomControl" se zobrazí v této skupině.</span><span class="sxs-lookup"><span data-stu-id="58f49-131">In the following example, the control implemented in `ManagedPackage.winmd` will appear in Visual Studio and Blend in a group named “Managed Package”, and “MyCustomControl” will appear in that group.</span></span> <span data-ttu-id="58f49-132">Všechna tato jména jsou libovolná.</span><span class="sxs-lookup"><span data-stu-id="58f49-132">All these names are arbitrary.</span></span>

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
> <span data-ttu-id="58f49-135">Je nutné explicitně zadat každý ovládací prvek, který chcete zobrazit v podokně nástrojů/datových zdrojů.</span><span class="sxs-lookup"><span data-stu-id="58f49-135">You must explicitly specify every control that you would like to see in the toolbox/assets pane.</span></span> <span data-ttu-id="58f49-136">Ujistěte se, že `Namespace.ControlName`je zadáte ve formátu .</span><span class="sxs-lookup"><span data-stu-id="58f49-136">Ensure you specify them in the format `Namespace.ControlName`.</span></span>

## <a name="add-custom-icons-to-your-controls"></a><span data-ttu-id="58f49-137">Přidání vlastních ikon k ovládacím prvkům</span><span class="sxs-lookup"><span data-stu-id="58f49-137">Add custom icons to your controls</span></span>

<span data-ttu-id="58f49-138">Chcete-li zobrazit vlastní ikonu v podokně panelu nástrojů nebo `design.dll` datových zdrojů, přidejte obrázek do projektu nebo odpovídajícího projektu s názvem Namespace.ControlName.extension a nastavte akci sestavení na Vložený zdroj.</span><span class="sxs-lookup"><span data-stu-id="58f49-138">To display a custom icon in the toolbox/assets pane, add an image to your project or the corresponding `design.dll` project with the name “Namespace.ControlName.extension” and set the build action to “Embedded Resource”.</span></span> <span data-ttu-id="58f49-139">Musíte také zajistit, `AssemblyInfo.cs` že přidružený určuje ProvideMetadata atribut - `[assembly: ProvideMetadata(typeof(RegisterMetadata))]`.</span><span class="sxs-lookup"><span data-stu-id="58f49-139">You must also ensure that the associated `AssemblyInfo.cs` specifies the ProvideMetadata attribute - `[assembly: ProvideMetadata(typeof(RegisterMetadata))]`.</span></span> <span data-ttu-id="58f49-140">Viz tento [příklad](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20).</span><span class="sxs-lookup"><span data-stu-id="58f49-140">See this [sample](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20).</span></span>

<span data-ttu-id="58f49-141">Podporované formáty `.png` `.jpg`jsou `.jpeg` `.gif`, `.bmp`, , a .</span><span class="sxs-lookup"><span data-stu-id="58f49-141">Supported formats are `.png`, `.jpg`, `.jpeg`, `.gif`, and `.bmp`.</span></span> <span data-ttu-id="58f49-142">Doporučený formát je BMP24 v 16 pixelech x 16 pixelů.</span><span class="sxs-lookup"><span data-stu-id="58f49-142">The recommended format is BMP24 in 16 pixels by 16 pixels.</span></span>

![Ukázka ikony rámečku nástrojů](https://raw.githubusercontent.com/NuGet/docs.microsoft.com-nuget/live/docs/guides/media/ColorPicker_16x16x24.bmp)

<span data-ttu-id="58f49-144">Růžové pozadí je nahrazeno za běhu.</span><span class="sxs-lookup"><span data-stu-id="58f49-144">The pink background is replaced at runtime.</span></span> <span data-ttu-id="58f49-145">Ikony jsou přebarveny při změně motivu sady Visual Studio a očekává se barva pozadí.</span><span class="sxs-lookup"><span data-stu-id="58f49-145">The icons are recolored when the Visual Studio theme is changed and that background color is expected.</span></span> <span data-ttu-id="58f49-146">Další informace naleznete v [odkazech na obrázky a ikony sady Visual Studio](https://docs.microsoft.com/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="58f49-146">For more information, please reference [Images and Icons for Visual Studio](https://docs.microsoft.com/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio).</span></span>

<span data-ttu-id="58f49-147">V níže uvedeném příkladu projekt obsahuje soubor obrázku s názvem "ManagedPackage.MyCustomControl.png".</span><span class="sxs-lookup"><span data-stu-id="58f49-147">In the example below, the project contains an image file named “ManagedPackage.MyCustomControl.png”.</span></span>

![Nastavení vlastní ikony v projektu](media/UWP-control-custom-icon.png)

> [!Note]
> <span data-ttu-id="58f49-149">U nativních ovládacích prvků je nutné `design.dll` umístit ikonu jako zdroj do projektu.</span><span class="sxs-lookup"><span data-stu-id="58f49-149">For native controls, you must put the icon as a resource in the `design.dll` project.</span></span>

## <a name="support-specific-windows-platform-versions"></a><span data-ttu-id="58f49-150">Podpora konkrétních verzí platformy Windows</span><span class="sxs-lookup"><span data-stu-id="58f49-150">Support specific Windows platform versions</span></span>

<span data-ttu-id="58f49-151">Balíčky UPW mají TargetPlatformVersion (TPV) a TargetPlatformMinVersion (TPMinV), které definují horní a dolní hranice verze operačního systému, kde lze nainstalovat aplikaci.</span><span class="sxs-lookup"><span data-stu-id="58f49-151">UWP packages have a TargetPlatformVersion (TPV) and TargetPlatformMinVersion (TPMinV) that define the upper and lower bounds of the OS version where the app can be installed.</span></span> <span data-ttu-id="58f49-152">TPV dále určuje verzi sady SDK, proti které je aplikace postavena.</span><span class="sxs-lookup"><span data-stu-id="58f49-152">TPV further specifies the version of the SDK against which the app is built.</span></span> <span data-ttu-id="58f49-153">Mějte na paměti tyto vlastnosti při vytváření balíčku UPW: použití rozhraní API mimo hranice verze platformy definované v aplikaci způsobí, že sestavení nezdaří nebo aplikace nezdaří za běhu.</span><span class="sxs-lookup"><span data-stu-id="58f49-153">Be mindful of these properties when authoring a UWP package: using APIs outside the bounds of the platform versions defined in the app will cause either the build to fail or the app to fail at runtime.</span></span>

<span data-ttu-id="58f49-154">Řekněme například, že jste nastavili tpminv pro balíček ovládacích prvků na Windows 10 Anniversary Edition (10.0; Sestavení 14393), takže chcete zajistit, že balíček je spotřebována pouze projekty UPW, které odpovídají dolní mez.</span><span class="sxs-lookup"><span data-stu-id="58f49-154">For example, let’s say you’ve set the TPMinV for your controls package to Windows 10 Anniversary Edition (10.0; Build 14393), so you want to ensure that the package is consumed only by UWP projects that match that lower bound.</span></span> <span data-ttu-id="58f49-155">Chcete-li povolit, aby byl balíček spotřebován projekty UPW, je nutné zabalit ovládací prvky s následujícími názvy složek:</span><span class="sxs-lookup"><span data-stu-id="58f49-155">To allow your package to be consumed by UWP projects, you must package your controls with the following folder names:</span></span>

    \lib\uap10.0.14393\*
    \ref\uap10.0.14393\*

<span data-ttu-id="58f49-156">NuGet automaticky zkontroluje TPMinV náročného projektu a nezdaří instalaci, pokud je nižší než Windows 10 Anniversary Edition (10.0; Budova 14393)</span><span class="sxs-lookup"><span data-stu-id="58f49-156">NuGet will automatically check the TPMinV of the consuming project, and fail installation if it is lower than Windows 10 Anniversary Edition (10.0; Build 14393)</span></span>

<span data-ttu-id="58f49-157">V případě WPF řekněme, že chcete, aby váš balíček wpf ovládacích prvků spotřebovávat projekty cílení .NET Framework v4.6.1 nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="58f49-157">In case of WPF, let's say you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher.</span></span> <span data-ttu-id="58f49-158">Chcete-li vynutit, že je nutné zabalit ovládací prvky s následujícími názvy složek:</span><span class="sxs-lookup"><span data-stu-id="58f49-158">To enforce that, you must package your controls with the following folder names:</span></span>

    \lib\net461\*
    \ref\net461\*

## <a name="add-design-time-support"></a><span data-ttu-id="58f49-159">Přidání podpory návrhu</span><span class="sxs-lookup"><span data-stu-id="58f49-159">Add design-time support</span></span>

<span data-ttu-id="58f49-160">Chcete-li nakonfigurovat, kde se vlastnosti ovládacího prvku zobrazí v `design.dll` inspektoru `lib\uap10.0.14393\Design` vlastností, přidejte vlastní adorners atd., umístěte soubor do složky podle potřeby na cílovou platformu.</span><span class="sxs-lookup"><span data-stu-id="58f49-160">To configure where the control properties show up in the property inspector, add custom adorners, etc., place your `design.dll` file inside the `lib\uap10.0.14393\Design` folder as appropriate to the target platform.</span></span> <span data-ttu-id="58f49-161">Chcete-li zajistit, aby funkce **[Upravit šablonu > Upravit kopii](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** fungovala, musíte do složky zahrnout slovníky `Generic.xaml` prostředků a všechny slovníky prostředků, které slučuje `<your_assembly_name>\Themes` (opět pomocí skutečného názvu sestavení).</span><span class="sxs-lookup"><span data-stu-id="58f49-161">Also, to ensure that the **[Edit Template > Edit a Copy](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** feature works, you must include the `Generic.xaml` and any resource dictionaries that it merges in the `<your_assembly_name>\Themes` folder (again, using your actual assembly name).</span></span> <span data-ttu-id="58f49-162">(Tento soubor nemá žádný vliv na chování ovládacího prvku za běhu.) Struktura složek by se tedy jevila takto:</span><span class="sxs-lookup"><span data-stu-id="58f49-162">(This file has no impact on the runtime behavior of a control.) The folder structure would thus appear as follows:</span></span>

    \lib
      \uap10.0.14393
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml


<span data-ttu-id="58f49-163">Pro WPF, pokračování v příkladu, kde chcete, aby váš wpf ovládací prvky balíček spotřebovávat projekty cílení .NET Framework v4.6.1 nebo vyšší:</span><span class="sxs-lookup"><span data-stu-id="58f49-163">For WPF, continuing with the example where you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher:</span></span>

    \lib
      \net461
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> <span data-ttu-id="58f49-164">Ve výchozím nastavení se vlastnosti ovládacího prvku zobrazí v kategorii Různé v inspektoru vlastností.</span><span class="sxs-lookup"><span data-stu-id="58f49-164">By default, control properties will show up under the Miscellaneous category in the property inspector.</span></span>

## <a name="use-strings-and-resources"></a><span data-ttu-id="58f49-165">Použití řetězců a prostředků</span><span class="sxs-lookup"><span data-stu-id="58f49-165">Use strings and resources</span></span>

<span data-ttu-id="58f49-166">Můžete vložit prostředky řetězce`.resw`( ) do balíčku, který může být použit ovládacím prvkem nebo náročným projektem UPW, nastavit vlastnost **Build Action** souboru `.resw` na **PRIResource**.</span><span class="sxs-lookup"><span data-stu-id="58f49-166">You can embed string resources (`.resw`) in your package that can be used by your control or the consuming UWP project, set the **Build Action** property of the `.resw` file to **PRIResource**.</span></span>

<span data-ttu-id="58f49-167">Příklad naleznete [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) v ExtensionSDKasNuGetPackage vzorku.</span><span class="sxs-lookup"><span data-stu-id="58f49-167">For an example, refer to [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) in the ExtensionSDKasNuGetPackage sample.</span></span>

> [!Note]
> <span data-ttu-id="58f49-168">To platí pouze pro ovládací prvky UPW.</span><span class="sxs-lookup"><span data-stu-id="58f49-168">This is applicable only to UWP controls.</span></span>

## <a name="see-also"></a><span data-ttu-id="58f49-169">Viz také</span><span class="sxs-lookup"><span data-stu-id="58f49-169">See also</span></span>

- [<span data-ttu-id="58f49-170">Vytvořit balíčky UPW</span><span class="sxs-lookup"><span data-stu-id="58f49-170">Create UWP Packages</span></span>](create-uwp-packages.md)
- [<span data-ttu-id="58f49-171">Ukázka rozšířeníSDKasNuGetPackage</span><span class="sxs-lookup"><span data-stu-id="58f49-171">ExtensionSDKasNuGetPackage sample</span></span>](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
