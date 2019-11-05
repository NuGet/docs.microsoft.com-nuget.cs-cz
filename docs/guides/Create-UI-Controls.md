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
# <a name="creating-ui-controls-as-nuget-packages"></a><span data-ttu-id="236f4-103">Vytvoření ovládacích prvků uživatelského rozhraní jako balíčků NuGet</span><span class="sxs-lookup"><span data-stu-id="236f4-103">Creating UI controls as NuGet packages</span></span>

<span data-ttu-id="236f4-104">Počínaje sadou Visual Studio 2017 můžete využít výhod přidaných funkcí pro ovládací prvky UWP a WPF, které zadáváte do balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="236f4-104">Starting with Visual Studio 2017, you can take advantage of added capabilities for UWP and WPF controls that you deliver in NuGet packages.</span></span> <span data-ttu-id="236f4-105">Tato příručka vás provede následujícími možnostmi v kontextu ovládacích prvků UWP pomocí [ukázky ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span><span class="sxs-lookup"><span data-stu-id="236f4-105">This guide walks you through these capabilities in context of UWP controls using the [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span></span> <span data-ttu-id="236f4-106">Totéž platí pro ovládací prvky WPF, pokud není uvedeno jinak.</span><span class="sxs-lookup"><span data-stu-id="236f4-106">The same applies to WPF controls unless mentioned otherwise.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="236f4-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="236f4-107">Prerequisites</span></span>

1. <span data-ttu-id="236f4-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="236f4-108">Visual Studio 2017</span></span>
1. <span data-ttu-id="236f4-109">Informace o tom, jak [vytvářet balíčky UWP](create-uwp-packages.md)</span><span class="sxs-lookup"><span data-stu-id="236f4-109">Understanding of how to [Create UWP Packages](create-uwp-packages.md)</span></span>

## <a name="generate-library-layout"></a><span data-ttu-id="236f4-110">Generovat rozložení knihovny</span><span class="sxs-lookup"><span data-stu-id="236f4-110">Generate Library Layout</span></span>

> [!Note]
> <span data-ttu-id="236f4-111">To platí pouze pro ovládací prvky UWP.</span><span class="sxs-lookup"><span data-stu-id="236f4-111">This is applicable only to UWP controls.</span></span>

<span data-ttu-id="236f4-112">Nastavení vlastnosti `GenerateLibraryLayout` zajistí, že výstup sestavení projektu bude vygenerován v rozložení, které je připraveno k zabalení bez nutnosti jednotlivých položek souborů v nuspec.</span><span class="sxs-lookup"><span data-stu-id="236f4-112">Setting the `GenerateLibraryLayout` property ensures that the project build output is generated in a layout that is ready to be packaged without the need for individual file entries in the nuspec.</span></span>

<span data-ttu-id="236f4-113">Z vlastností projektu, přejít na kartu sestavení a zaškrtněte políčko Generovat rozložení knihovny.</span><span class="sxs-lookup"><span data-stu-id="236f4-113">From the project properties, go to the build tab and check the "Generate Library Layout" check box.</span></span> <span data-ttu-id="236f4-114">Tím se upraví soubor projektu a nastaví se příznak `GenerateLibraryLayout` pro aktuálně vybranou konfiguraci a platformu sestavení na hodnotu true.</span><span class="sxs-lookup"><span data-stu-id="236f4-114">This will modify the project file and set the `GenerateLibraryLayout` flag to true for your currently selected build configuration and platform.</span></span>

<span data-ttu-id="236f4-115">Případně upravte soubor projektu pro přidání `<GenerateLibraryLayout>true</GenerateLibraryLayout>` do první nepodmíněné skupiny vlastností.</span><span class="sxs-lookup"><span data-stu-id="236f4-115">Alternately, edit the the project file to add `<GenerateLibraryLayout>true</GenerateLibraryLayout>` to the first unconditional property group.</span></span> <span data-ttu-id="236f4-116">Tato vlastnost by se použila bez ohledu na konfiguraci sestavení a platformu.</span><span class="sxs-lookup"><span data-stu-id="236f4-116">This would apply the property irrespective of the build configuration and platform.</span></span>

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a><span data-ttu-id="236f4-117">Přidání podpory nástrojů/panelu nástrojů pro ovládací prvky XAML</span><span class="sxs-lookup"><span data-stu-id="236f4-117">Add toolbox/assets pane support for XAML controls</span></span>

<span data-ttu-id="236f4-118">Chcete-li, aby se ovládací prvek XAML zobrazil v sadě nástrojů návrháře XAML v sadě Visual Studio a v podokně assets (prostředky), vytvořte soubor `VisualStudioToolsManifest.xml` v kořenu složky `tools` projektu balíčku.</span><span class="sxs-lookup"><span data-stu-id="236f4-118">To have a XAML control appear in the XAML designer’s toolbox in Visual Studio and the Assets pane of Blend, create a `VisualStudioToolsManifest.xml` file in the root of the `tools` folder of your package project.</span></span> <span data-ttu-id="236f4-119">Tento soubor není povinný, pokud nepotřebujete, aby se ovládací prvek zobrazoval v podokně nástrojů nebo aktiv.</span><span class="sxs-lookup"><span data-stu-id="236f4-119">This file is not required if you don’t need the control to appear in the toolbox or Assets pane.</span></span>

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

<span data-ttu-id="236f4-120">Struktura souboru je následující:</span><span class="sxs-lookup"><span data-stu-id="236f4-120">The structure of the file is as follows:</span></span>

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

<span data-ttu-id="236f4-121">kde:</span><span class="sxs-lookup"><span data-stu-id="236f4-121">where:</span></span>

- <span data-ttu-id="236f4-122">*your_package_file*: název řídicího souboru, například `ManagedPackage.winmd` ("ManagedPackage" je libovolný název, který se používá pro tento příklad a nemá žádný jiný význam).</span><span class="sxs-lookup"><span data-stu-id="236f4-122">*your_package_file*: the name of your control file, such as `ManagedPackage.winmd` ("ManagedPackage" is an arbitrary named used for this example and has no other meaning).</span></span>
- <span data-ttu-id="236f4-123">*vs_category*: popisek skupiny, ve které by se měl ovládací prvek zobrazit v sadě nástrojů Visual Studio designer.</span><span class="sxs-lookup"><span data-stu-id="236f4-123">*vs_category*: The label for the group in which the control should appear in the Visual Studio designer’s toolbox.</span></span> <span data-ttu-id="236f4-124">`VSCategory` je nutné, aby se ovládací prvek zobrazoval v sadě nástrojů.</span><span class="sxs-lookup"><span data-stu-id="236f4-124">A `VSCategory` is necessary for the control to appear in the toolbox.</span></span>
- <span data-ttu-id="236f4-125">*blend_category*: popisek skupiny, ve které by se měl ovládací prvek zobrazit v podokně assets návrháře Blendu.</span><span class="sxs-lookup"><span data-stu-id="236f4-125">*blend_category*: The label for the group in which the control should appear in the Blend designer’s Assets pane.</span></span> <span data-ttu-id="236f4-126">`BlendCategory` je nutné, aby se ovládací prvek objevil v prostředcích.</span><span class="sxs-lookup"><span data-stu-id="236f4-126">A `BlendCategory` is necessary for the control to appear in Assets.</span></span>
- <span data-ttu-id="236f4-127">*type_full_name_n*: plně kvalifikovaný název pro každý ovládací prvek, včetně oboru názvů, jako je například `ManagedPackage.MyCustomControl`.</span><span class="sxs-lookup"><span data-stu-id="236f4-127">*type_full_name_n*: The fully-qualified name for each control, including the namespace, such as `ManagedPackage.MyCustomControl`.</span></span> <span data-ttu-id="236f4-128">Všimněte si, že formát tečky se používá pro spravované i nativní typy.</span><span class="sxs-lookup"><span data-stu-id="236f4-128">Note that the dot format is used for both managed and native types.</span></span>

<span data-ttu-id="236f4-129">V pokročilejších scénářích můžete také zahrnout více `<File>` prvků v rámci `<FileList>`, pokud jeden balíček obsahuje více sestavení ovládacích prvků.</span><span class="sxs-lookup"><span data-stu-id="236f4-129">In more advanced scenarios, you can also include multiple `<File>` elements within `<FileList>` when a single package contains multiple control assemblies.</span></span> <span data-ttu-id="236f4-130">Můžete mít také více `<ToolboxItems>` uzlů v rámci jednoho `<File>`, pokud chcete uspořádat ovládací prvky do samostatných kategorií.</span><span class="sxs-lookup"><span data-stu-id="236f4-130">You can also have multiple `<ToolboxItems>` nodes within a single `<File>` if you want to organize your controls into separate categories.</span></span>

<span data-ttu-id="236f4-131">V následujícím příkladu se ovládací prvek implementovaný v `ManagedPackage.winmd` zobrazí v aplikaci Visual Studio a Blend ve skupině s názvem "Managed Package" a "MyCustomControl" se zobrazí v této skupině.</span><span class="sxs-lookup"><span data-stu-id="236f4-131">In the following example, the control implemented in `ManagedPackage.winmd` will appear in Visual Studio and Blend in a group named “Managed Package”, and “MyCustomControl” will appear in that group.</span></span> <span data-ttu-id="236f4-132">Všechny tyto názvy jsou libovolné.</span><span class="sxs-lookup"><span data-stu-id="236f4-132">All these names are arbitrary.</span></span>

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
> <span data-ttu-id="236f4-135">Každý ovládací prvek, který byste chtěli zobrazit v podokně Sada nástrojů/prostředky, musíte explicitně zadat.</span><span class="sxs-lookup"><span data-stu-id="236f4-135">You must explicitly specify every control that you would like to see in the toolbox/assets pane.</span></span> <span data-ttu-id="236f4-136">Ujistěte se, že je zadáte ve formátu `Namespace.ControlName`.</span><span class="sxs-lookup"><span data-stu-id="236f4-136">Ensure you specify them in the format `Namespace.ControlName`.</span></span>

## <a name="add-custom-icons-to-your-controls"></a><span data-ttu-id="236f4-137">Přidat vlastní ikony do ovládacích prvků</span><span class="sxs-lookup"><span data-stu-id="236f4-137">Add custom icons to your controls</span></span>

<span data-ttu-id="236f4-138">Chcete-li zobrazit vlastní ikonu v podokně Sada nástrojů/assets, přidejte do projektu obrázek nebo odpovídající projekt `design.dll` s názvem "obor názvů. Control. Extension" a nastavte akci sestavení na "Integrovaný prostředek".</span><span class="sxs-lookup"><span data-stu-id="236f4-138">To display a custom icon in the toolbox/assets pane, add an image to your project or the corresponding `design.dll` project with the name “Namespace.ControlName.extension” and set the build action to “Embedded Resource”.</span></span> <span data-ttu-id="236f4-139">Musíte také zajistit, aby související `AssemblyInfo.cs` určovala `[assembly: ProvideMetadata(typeof(RegisterMetadata))]`atributu ProvideMetadata.</span><span class="sxs-lookup"><span data-stu-id="236f4-139">You must also ensure that the associated `AssemblyInfo.cs` specifies the ProvideMetadata attribute - `[assembly: ProvideMetadata(typeof(RegisterMetadata))]`.</span></span> <span data-ttu-id="236f4-140">Podívejte se na tuto [ukázku](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20).</span><span class="sxs-lookup"><span data-stu-id="236f4-140">See this [sample](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20).</span></span>

<span data-ttu-id="236f4-141">Podporované formáty jsou `.png`, `.jpg`, `.jpeg`, `.gif`a `.bmp`.</span><span class="sxs-lookup"><span data-stu-id="236f4-141">Supported formats are `.png`, `.jpg`, `.jpeg`, `.gif`, and `.bmp`.</span></span> <span data-ttu-id="236f4-142">Doporučený formát je BMP24 v rozmezí 16 × 16 pixelů.</span><span class="sxs-lookup"><span data-stu-id="236f4-142">The recommended format is BMP24 in 16 pixels by 16 pixels.</span></span>

![Ukázka ikony pole nástrojů](https://raw.githubusercontent.com/NuGet/docs.microsoft.com-nuget/live/docs/guides/media/ColorPicker_16x16x24.bmp)

<span data-ttu-id="236f4-144">Růžová pozadí je nahrazena za běhu.</span><span class="sxs-lookup"><span data-stu-id="236f4-144">The pink background is replaced at runtime.</span></span> <span data-ttu-id="236f4-145">Když se změní motiv sady Visual Studio a očekává se barva pozadí, jsou ikony Přebarvené.</span><span class="sxs-lookup"><span data-stu-id="236f4-145">The icons are recolored when the Visual Studio theme is changed and that background color is expected.</span></span> <span data-ttu-id="236f4-146">Další informace najdete v referenčních [obrázcích a ikonách pro Visual Studio](https://docs.microsoft.com/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="236f4-146">For more information, please reference [Images and Icons for Visual Studio](https://docs.microsoft.com/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio).</span></span>

<span data-ttu-id="236f4-147">V následujícím příkladu obsahuje projekt soubor s obrázkem s názvem "ManagedPackage. MyCustomControl. png".</span><span class="sxs-lookup"><span data-stu-id="236f4-147">In the example below, the project contains an image file named “ManagedPackage.MyCustomControl.png”.</span></span>

![Nastavení vlastní ikony v projektu](media/UWP-control-custom-icon.png)

> [!Note]
> <span data-ttu-id="236f4-149">Pro nativní ovládací prvky je nutné umístit ikonu jako prostředek v projektu `design.dll`.</span><span class="sxs-lookup"><span data-stu-id="236f4-149">For native controls, you must put the icon as a resource in the `design.dll` project.</span></span>

## <a name="support-specific-windows-platform-versions"></a><span data-ttu-id="236f4-150">Podporují konkrétní verze platformy Windows.</span><span class="sxs-lookup"><span data-stu-id="236f4-150">Support specific Windows platform versions</span></span>

<span data-ttu-id="236f4-151">Balíčky UWP mají TargetPlatformVersion (TPV) a TargetPlatformMinVersion (TPMinV), které definují horní a dolní meze verze operačního systému, kde se dá aplikace nainstalovat.</span><span class="sxs-lookup"><span data-stu-id="236f4-151">UWP packages have a TargetPlatformVersion (TPV) and TargetPlatformMinVersion (TPMinV) that define the upper and lower bounds of the OS version where the app can be installed.</span></span> <span data-ttu-id="236f4-152">TPV dále určuje verzi sady SDK, proti které je aplikace sestavena.</span><span class="sxs-lookup"><span data-stu-id="236f4-152">TPV further specifies the version of the SDK against which the app is built.</span></span> <span data-ttu-id="236f4-153">Nezapomeňte na tyto vlastnosti při vytváření balíčku UWP: použití rozhraní API mimo hranice verzí platforem definované v aplikaci způsobí selhání sestavení nebo selhání aplikace za běhu.</span><span class="sxs-lookup"><span data-stu-id="236f4-153">Be mindful of these properties when authoring a UWP package: using APIs outside the bounds of the platform versions defined in the app will cause either the build to fail or the app to fail at runtime.</span></span>

<span data-ttu-id="236f4-154">Řekněme například, že jste nastavili TPMinV pro balíček Controls na Windows 10 výročí Edition (10,0; Sestavení 14393), aby bylo zajištěno, že balíček je spotřebován pouze projekty UWP, které odpovídají danému dolnímu omezení.</span><span class="sxs-lookup"><span data-stu-id="236f4-154">For example, let’s say you’ve set the TPMinV for your controls package to Windows 10 Anniversary Edition (10.0; Build 14393), so you want to ensure that the package is consumed only by UWP projects that match that lower bound.</span></span> <span data-ttu-id="236f4-155">Chcete-li, aby bylo možné balíček využívat v projektech UWP, je nutné zabalit ovládací prvky s následujícími názvy složek:</span><span class="sxs-lookup"><span data-stu-id="236f4-155">To allow your package to be consumed by UWP projects, you must package your controls with the following folder names:</span></span>

    \lib\uap10.0.14393\*
    \ref\uap10.0.14393\*

<span data-ttu-id="236f4-156">NuGet bude automaticky kontrolovat TPMinV projektu, a pokud je nižší než Windows 10 výročí Edition (10,0;), instalace selže. Sestavení 14393)</span><span class="sxs-lookup"><span data-stu-id="236f4-156">NuGet will automatically check the TPMinV of the consuming project, and fail installation if it is lower than Windows 10 Anniversary Edition (10.0; Build 14393)</span></span>

<span data-ttu-id="236f4-157">V případě WPF řekněme, že chcete, aby váš balíček WPF Controls byly spotřebované projekty, které cílí na .NET Framework v 4.6.1 nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="236f4-157">In case of WPF, let's say you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher.</span></span> <span data-ttu-id="236f4-158">Aby bylo možné tento postup vyhovět, je nutné zabalit ovládací prvky s následujícími názvy složek:</span><span class="sxs-lookup"><span data-stu-id="236f4-158">To enforce that, you must package your controls with the following folder names:</span></span>

    \lib\net461\*
    \ref\net461\*

## <a name="add-design-time-support"></a><span data-ttu-id="236f4-159">Přidání podpory pro dobu návrhu</span><span class="sxs-lookup"><span data-stu-id="236f4-159">Add design-time support</span></span>

<span data-ttu-id="236f4-160">Chcete-li nakonfigurovat, kde se vlastnosti ovládacího prvku zobrazí v inspektoru vlastností, přidejte vlastní doplňky atd., umístěte soubor `design.dll` do složky `lib\uap10.0.14393\Design` tak, aby odpovídala cílové platformě.</span><span class="sxs-lookup"><span data-stu-id="236f4-160">To configure where the control properties show up in the property inspector, add custom adorners, etc., place your `design.dll` file inside the `lib\uap10.0.14393\Design` folder as appropriate to the target platform.</span></span> <span data-ttu-id="236f4-161">Aby bylo zajištěno, že funkce **[Upravit šablonu > upravit kopírování](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** funguje, je nutné zahrnout `Generic.xaml` a všechny slovníky prostředků, které se sloučí do složky `<your_assembly_name>\Themes` (znovu pomocí vlastního názvu sestavení).</span><span class="sxs-lookup"><span data-stu-id="236f4-161">Also, to ensure that the **[Edit Template > Edit a Copy](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** feature works, you must include the `Generic.xaml` and any resource dictionaries that it merges in the `<your_assembly_name>\Themes` folder (again, using your actual assembly name).</span></span> <span data-ttu-id="236f4-162">(Tento soubor nemá žádný vliv na chování za běhu ovládacího prvku.) Struktura složek by tedy vypadala takto:</span><span class="sxs-lookup"><span data-stu-id="236f4-162">(This file has no impact on the runtime behavior of a control.) The folder structure would thus appear as follows:</span></span>

    \lib
      \uap10.0.14393
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml


<span data-ttu-id="236f4-163">V případě WPF pokračuje v příkladu, kde chcete, aby byl balíček WPF ovládací prvky spotřebován projekty cílené na .NET Framework v 4.6.1 nebo vyšší:</span><span class="sxs-lookup"><span data-stu-id="236f4-163">For WPF, continuing with the example where you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher:</span></span>

    \lib
      \net461
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> <span data-ttu-id="236f4-164">Ve výchozím nastavení se vlastnosti ovládacího prvku zobrazí pod kategorií různé v inspektoru vlastností.</span><span class="sxs-lookup"><span data-stu-id="236f4-164">By default, control properties will show up under the Miscellaneous category in the property inspector.</span></span>

## <a name="use-strings-and-resources"></a><span data-ttu-id="236f4-165">Použití řetězců a prostředků</span><span class="sxs-lookup"><span data-stu-id="236f4-165">Use strings and resources</span></span>

<span data-ttu-id="236f4-166">Do balíčku můžete vkládat řetězcové prostředky (`.resw`), které lze použít pro ovládací prvek nebo zpracování projektu UWP, nastavením vlastnosti **Akce sestavení** `.resw` souboru na **PRIResource**.</span><span class="sxs-lookup"><span data-stu-id="236f4-166">You can embed string resources (`.resw`) in your package that can be used by your control or the consuming UWP project, set the **Build Action** property of the `.resw` file to **PRIResource**.</span></span>

<span data-ttu-id="236f4-167">Příklad naleznete v tématu [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) v ukázce ExtensionSDKasNuGetPackage.</span><span class="sxs-lookup"><span data-stu-id="236f4-167">For an example, refer to [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) in the ExtensionSDKasNuGetPackage sample.</span></span>

> [!Note]
> <span data-ttu-id="236f4-168">To platí pouze pro ovládací prvky UWP.</span><span class="sxs-lookup"><span data-stu-id="236f4-168">This is applicable only to UWP controls.</span></span>

## <a name="see-also"></a><span data-ttu-id="236f4-169">Viz také:</span><span class="sxs-lookup"><span data-stu-id="236f4-169">See also</span></span>

- [<span data-ttu-id="236f4-170">Vytvoření balíčků UPW</span><span class="sxs-lookup"><span data-stu-id="236f4-170">Create UWP Packages</span></span>](create-uwp-packages.md)
- [<span data-ttu-id="236f4-171">Ukázka ExtensionSDKasNuGetPackage</span><span class="sxs-lookup"><span data-stu-id="236f4-171">ExtensionSDKasNuGetPackage sample</span></span>](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
