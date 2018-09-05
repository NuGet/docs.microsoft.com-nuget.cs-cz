---
title: Jak ovládacích prvků uživatelského rozhraní balíčku nuget
description: Jak vytvořit balíčky NuGet, které obsahují UPW nebo WPF ovládací prvky, včetně potřebná metadata a podpůrné soubory pro návrháře Visual Studio a Blend.
author: karann-msft
ms.author: karann
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: ce5ad07209a06010150b14092aa1b15ee6f84146
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548735"
---
# <a name="creating-ui-controls-as-nuget-packages"></a><span data-ttu-id="9a531-103">Vytvoření ovládacích prvků uživatelského rozhraní jako balíčků NuGet</span><span class="sxs-lookup"><span data-stu-id="9a531-103">Creating UI controls as NuGet packages</span></span>

<span data-ttu-id="9a531-104">Pomocí sady Visual Studio 2017 můžete využít výhod přidané možnosti pro UPW a WPF ovládací prvky, které jsou užitečné v balíčcích NuGet.</span><span class="sxs-lookup"><span data-stu-id="9a531-104">With Visual Studio 2017, you can take advantage of added capabilities for UWP and WPF controls that you deliver in NuGet packages.</span></span> <span data-ttu-id="9a531-105">Tento průvodce vás provede tyto možnosti v souvislosti s použitím ovládacích prvků UPW [ExtensionSDKasNuGetPackage ukázka](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span><span class="sxs-lookup"><span data-stu-id="9a531-105">This guide walks you through these capabilities in context of UWP controls using the [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span></span> <span data-ttu-id="9a531-106">Totéž platí pro ovládací prvky WPF, pokud není uvedeno jinak.</span><span class="sxs-lookup"><span data-stu-id="9a531-106">The same applies to WPF controls unless mentioned otherwise.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a531-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="9a531-107">Prerequisites</span></span>

1. <span data-ttu-id="9a531-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="9a531-108">Visual Studio 2017</span></span>
1. <span data-ttu-id="9a531-109">Přehled o tom, jak [vytvoření balíčků UPW](create-uwp-packages.md)</span><span class="sxs-lookup"><span data-stu-id="9a531-109">Understanding of how to [Create UWP Packages](create-uwp-packages.md)</span></span>

## <a name="generate-library-layout"></a><span data-ttu-id="9a531-110">Generovat rozložení knihovny</span><span class="sxs-lookup"><span data-stu-id="9a531-110">Generate Library Layout</span></span>

> [!Note]
> <span data-ttu-id="9a531-111">To se vztahuje pouze na ovládacích prvků UPW.</span><span class="sxs-lookup"><span data-stu-id="9a531-111">This is applicable only to UWP controls.</span></span>

<span data-ttu-id="9a531-112">Nastavení `GenerateLibraryLayout` vlastnost zajistí, že se výstupní sestavení projektu vygeneruje v rozložení, který je připraven k zabalit, bez nutnosti položky jednotlivých souborů v souboru nuspec.</span><span class="sxs-lookup"><span data-stu-id="9a531-112">Setting the `GenerateLibraryLayout` property ensures that the project build output is generated in a layout that is ready to be packaged without the need for individual file entries in the nuspec.</span></span>

<span data-ttu-id="9a531-113">Z vlastnosti projektu přejděte na kartu sestavení a zaškrtnutím políčka "Generovat rozložení knihovny".</span><span class="sxs-lookup"><span data-stu-id="9a531-113">From the project properties, go to the build tab and check the "Generate Library Layout" check box.</span></span> <span data-ttu-id="9a531-114">To bude úpravu souboru projektu a nastavte `GenerateLibraryLayout` příznak na hodnotu true pro aktuálně vybraná konfigurace sestavení a platformu.</span><span class="sxs-lookup"><span data-stu-id="9a531-114">This will modify the project file and set the `GenerateLibraryLayout` flag to true for your currently selected build configuration and platform.</span></span>

<span data-ttu-id="9a531-115">Můžete také upravit soubor projektu a přidejte `<GenerateLibraryLayout>true</GenerateLibraryLayout>` do první skupiny vlastností Nepodmíněný.</span><span class="sxs-lookup"><span data-stu-id="9a531-115">Alternately, edit the the project file to add `<GenerateLibraryLayout>true</GenerateLibraryLayout>` to the first unconditional property group.</span></span> <span data-ttu-id="9a531-116">To platí bez ohledu na konfiguraci sestavení a platformu vlastnost.</span><span class="sxs-lookup"><span data-stu-id="9a531-116">This would apply the property irrespective of the build configuration and platform.</span></span>

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a><span data-ttu-id="9a531-117">Přidání podpory podokna nástrojů a prostředků pro ovládací prvky XAML</span><span class="sxs-lookup"><span data-stu-id="9a531-117">Add toolbox/assets pane support for XAML controls</span></span>

<span data-ttu-id="9a531-118">Pokud chcete, aby se zobrazí v panelu nástrojů návrháře XAML v sadě Visual Studio a v podokně prostředků aplikace Blend ovládacího prvku XAML, vytvořte `VisualStudioToolsManifest.xml` soubor v kořenové složce `tools` složce balíčku projektu.</span><span class="sxs-lookup"><span data-stu-id="9a531-118">To have a XAML control appear in the XAML designer’s toolbox in Visual Studio and the Assets pane of Blend, create a `VisualStudioToolsManifest.xml` file in the root of the `tools` folder of your package project.</span></span> <span data-ttu-id="9a531-119">Tento soubor není povinný, pokud už nepotřebujete ovládací prvek se zobrazí v okně nástrojů nebo prostředky.</span><span class="sxs-lookup"><span data-stu-id="9a531-119">This file is not required if you don’t need the control to appear in the toolbox or Assets pane.</span></span>

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

<span data-ttu-id="9a531-120">Struktura souboru je následující:</span><span class="sxs-lookup"><span data-stu-id="9a531-120">The structure of the file is as follows:</span></span>

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

<span data-ttu-id="9a531-121">kde:</span><span class="sxs-lookup"><span data-stu-id="9a531-121">where:</span></span>

- <span data-ttu-id="9a531-122">*your_package_file*: soubor název vašeho ovládacího prvku, třeba `ManagedPackage.winmd` ("ManagedPackage" je libovolnou s názvem používá pro účely tohoto příkladu a nemá žádný význam).</span><span class="sxs-lookup"><span data-stu-id="9a531-122">*your_package_file*: the name of your control file, such as `ManagedPackage.winmd` ("ManagedPackage" is an arbitrary named used for this example and has no other meaning).</span></span>
- <span data-ttu-id="9a531-123">*vs_category*: Popisek skupiny, ve kterém by se měla zobrazit ovládací prvek v panelu nástrojů návrháře aplikace Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9a531-123">*vs_category*: The label for the group in which the control should appear in the Visual Studio designer’s toolbox.</span></span> <span data-ttu-id="9a531-124">A `VSCategory` je nezbytné pro ovládací prvek se zobrazí na panelu nástrojů.</span><span class="sxs-lookup"><span data-stu-id="9a531-124">A `VSCategory` is necessary for the control to appear in the toolbox.</span></span>
- <span data-ttu-id="9a531-125">*blend_category*: Popisek skupiny, ve kterém ovládací prvek by se měla zobrazit v podokně návrháře Blendu prostředky.</span><span class="sxs-lookup"><span data-stu-id="9a531-125">*blend_category*: The label for the group in which the control should appear in the Blend designer’s Assets pane.</span></span> <span data-ttu-id="9a531-126">A `BlendCategory` je nezbytné pro ovládací prvek se zobrazí v majetku.</span><span class="sxs-lookup"><span data-stu-id="9a531-126">A `BlendCategory` is necessary for the control to appear in Assets.</span></span>
- <span data-ttu-id="9a531-127">*type_full_name_n*: plně kvalifikovaný název pro každý ovládací prvek, včetně oboru názvů, jako například `ManagedPackage.MyCustomControl`.</span><span class="sxs-lookup"><span data-stu-id="9a531-127">*type_full_name_n*: The fully-qualified name for each control, including the namespace, such as `ManagedPackage.MyCustomControl`.</span></span> <span data-ttu-id="9a531-128">Všimněte si, že formát tečka se používá pro spravovaný i nativní typy.</span><span class="sxs-lookup"><span data-stu-id="9a531-128">Note that the dot format is used for both managed and native types.</span></span>

<span data-ttu-id="9a531-129">V pokročilejších scénářích, může také obsahovat více `<File>` elementů v rámci `<FileList>` Pokud jeden balíček obsahuje více sestavení ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="9a531-129">In more advanced scenarios, you can also include multiple `<File>` elements within `<FileList>` when a single package contains multiple control assemblies.</span></span> <span data-ttu-id="9a531-130">Můžete mít také více `<ToolboxItems>` uzly v jednom `<File>` Pokud budete chtít uspořádání ovládacích prvků do samostatných kategorií.</span><span class="sxs-lookup"><span data-stu-id="9a531-130">You can also have multiple `<ToolboxItems>` nodes within a single `<File>` if you want to organize your controls into separate categories.</span></span>

<span data-ttu-id="9a531-131">V následujícím příkladu, ovládací prvek implementované v `ManagedPackage.winmd` se zobrazí v sadě Visual Studio a Vmísil skupina s názvem "Spravované balíček" a "MyCustomControl" se zobrazí v této skupině.</span><span class="sxs-lookup"><span data-stu-id="9a531-131">In the following example, the control implemented in `ManagedPackage.winmd` will appear in Visual Studio and Blend in a group named “Managed Package”, and “MyCustomControl” will appear in that group.</span></span> <span data-ttu-id="9a531-132">Tyto názvy jsou libovolného.</span><span class="sxs-lookup"><span data-stu-id="9a531-132">All these names are arbitrary.</span></span>

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
> <span data-ttu-id="9a531-135">Je nutné explicitně zadat každý ovládací prvek, který chcete zobrazit na panelu nástrojů a prostředků.</span><span class="sxs-lookup"><span data-stu-id="9a531-135">You must explicitly specify every control that you would like to see in the toolbox/assets pane.</span></span> <span data-ttu-id="9a531-136">Ujistěte se, zadejte ve formátu `Namespace.ControlName`.</span><span class="sxs-lookup"><span data-stu-id="9a531-136">Ensure you specify them in the format `Namespace.ControlName`.</span></span>

## <a name="add-custom-icons-to-your-controls"></a><span data-ttu-id="9a531-137">Přidat vlastní ikony k ovládacím prvkům</span><span class="sxs-lookup"><span data-stu-id="9a531-137">Add custom icons to your controls</span></span>

<span data-ttu-id="9a531-138">K zobrazení vlastní ikony na panelu nástrojů a prostředků, přidat bitovou kopii do projektu nebo odpovídající `design.dll` projektu s názvem "Namespace.ControlName.extension" a nastavte akci sestavení na "Integrovaný prostředek".</span><span class="sxs-lookup"><span data-stu-id="9a531-138">To display a custom icon in the toolbox/assets pane, add an image to your project or the corresponding `design.dll` project with the name “Namespace.ControlName.extension” and set the build action to “Embedded Resource”.</span></span> <span data-ttu-id="9a531-139">Podporované formáty jsou `.png`, `.jpg`, `.jpeg`, `.gif`, a `.bmp`.</span><span class="sxs-lookup"><span data-stu-id="9a531-139">Supported formats are `.png`, `.jpg`, `.jpeg`, `.gif`, and `.bmp`.</span></span> <span data-ttu-id="9a531-140">Doporučená velikost je 64 x 64 pixelů.</span><span class="sxs-lookup"><span data-stu-id="9a531-140">The recommended image size is 64 pixels by 64 pixels.</span></span>

<span data-ttu-id="9a531-141">V následujícím příkladu projektu obsahuje soubor image s názvem "ManagedPackage.MyCustomControl.png".</span><span class="sxs-lookup"><span data-stu-id="9a531-141">In the example below, the project contains an image file named “ManagedPackage.MyCustomControl.png”.</span></span>

![Nastavení vlastní ikony v projektu](media/UWP-control-custom-icon.png)

> [!Note]
> <span data-ttu-id="9a531-143">Pro nativní ovládací prvky, je nutné umístit na ikonu jako prostředek v `design.dll` projektu.</span><span class="sxs-lookup"><span data-stu-id="9a531-143">For native controls, you must put the icon as a resource in the `design.dll` project.</span></span>

## <a name="support-specific-windows-platform-versions"></a><span data-ttu-id="9a531-144">Podporují konkrétní verze platformy Windows</span><span class="sxs-lookup"><span data-stu-id="9a531-144">Support specific Windows platform versions</span></span>

<span data-ttu-id="9a531-145">Balíčků UPW mít TargetPlatformVersion (TPV) a prvkem TargetPlatformMinVersion (TPMinV), které definují horní a dolní meze zápisu verze operačního systému nainstalovanou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="9a531-145">UWP packages have a TargetPlatformVersion (TPV) and TargetPlatformMinVersion (TPMinV) that define the upper and lower bounds of the OS version where the app can be installed.</span></span> <span data-ttu-id="9a531-146">Další TPV Určuje verzi sady SDK, proti kterému byla sestavena.</span><span class="sxs-lookup"><span data-stu-id="9a531-146">TPV further specifies the version of the SDK against which the app is built.</span></span> <span data-ttu-id="9a531-147">Mějte na paměti tyto vlastnosti při vytváření balíčků UPW: pomocí rozhraní API mimo hranice verze platformy, které jsou definovány v aplikaci způsobí, že aby sestavení selhalo, nebo aplikaci, aby v době běhu selhat.</span><span class="sxs-lookup"><span data-stu-id="9a531-147">Be mindful of these properties when authoring a UWP package: using APIs outside the bounds of the platform versions defined in the app will cause either the build to fail or the app to fail at runtime.</span></span>

<span data-ttu-id="9a531-148">Například Řekněme, že jste nastavili TPMinV pro balíček sady ovládacích prvků Windows 10 Anniversary Edition (10.0; Sestavení 14393), tak, že chcete mít jistotu, že balíček je využívá jenom UPW projekty, které odpovídají, který dolní mez.</span><span class="sxs-lookup"><span data-stu-id="9a531-148">For example, let’s say you’ve set the TPMinV for your controls package to Windows 10 Anniversary Edition (10.0; Build 14393), so you want to ensure that the package is consumed only by UWP projects that match that lower bound.</span></span> <span data-ttu-id="9a531-149">Aby váš balíček pro projekty UWP, musíte sestavit balíček své ovládací prvky s následující názvy složek:</span><span class="sxs-lookup"><span data-stu-id="9a531-149">To allow your package to be consumed by UWP projects, you must package your controls with the following folder names:</span></span>

    \lib\uap10.0.14393\*
    \ref\uap10.0.14393\*

<span data-ttu-id="9a531-150">NuGet automaticky zkontroluje TPMinV náročné projektu a instalace selhat, pokud je nižší než Windows 10 Anniversary Edition (10.0; Sestavení 14393)</span><span class="sxs-lookup"><span data-stu-id="9a531-150">NuGet will automatically check the TPMinV of the consuming project, and fail installation if it is lower than Windows 10 Anniversary Edition (10.0; Build 14393)</span></span>

<span data-ttu-id="9a531-151">V případě WPF Řekněme, že byste chtěli balíčku ovládacích prvků WPF spotřebované podle projekty cílené na rozhraní .NET Framework v4.6.1 nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="9a531-151">In case of WPF, let's say you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher.</span></span> <span data-ttu-id="9a531-152">K vynucení, který, musíte sestavit balíček své ovládací prvky s následující názvy složek:</span><span class="sxs-lookup"><span data-stu-id="9a531-152">To enforce that, you must package your controls with the following folder names:</span></span>

    \lib\net461\*
    \ref\net461\*

## <a name="add-design-time-support"></a><span data-ttu-id="9a531-153">Přidání podpory během návrhu</span><span class="sxs-lookup"><span data-stu-id="9a531-153">Add design-time support</span></span>

<span data-ttu-id="9a531-154">Ke konfiguraci, kde vlastnosti ovládacího prvku zobrazí v okně Inspektor. vlastnosti, přidejte vlastní doplňky apod., umístěte vaše `design.dll` soubor uvnitř `lib\uap10.0.14393\Design` složky v závislosti na cílové platformě.</span><span class="sxs-lookup"><span data-stu-id="9a531-154">To configure where the control properties show up in the property inspector, add custom adorners, etc., place your `design.dll` file inside the `lib\uap10.0.14393\Design` folder as appropriate to the target platform.</span></span> <span data-ttu-id="9a531-155">Také zajistit, aby **[upravit šablonu > Upravit kopii](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** funkce funguje, je nutné uvést `Generic.xaml` a sloučení v slovníky prostředků `<your_assembly_name>\Themes` složky (znovu s použitím název vašeho sestavení skutečné).</span><span class="sxs-lookup"><span data-stu-id="9a531-155">Also, to ensure that the **[Edit Template > Edit a Copy](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** feature works, you must include the `Generic.xaml` and any resource dictionaries that it merges in the `<your_assembly_name>\Themes` folder (again, using your actual assembly name).</span></span> <span data-ttu-id="9a531-156">(Tento soubor nemá žádný vliv na chování modulu runtime ovládacího prvku.) Struktura složek by tak vypadat následovně:</span><span class="sxs-lookup"><span data-stu-id="9a531-156">(This file has no impact on the runtime behavior of a control.) The folder structure would thus appear as follows:</span></span>

    \lib
      \uap10.0.14393
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml


<span data-ttu-id="9a531-157">Pro WPF pokračování příkladu s, kde chcete vaše WPF – ovládací prvky balíček spotřebované podle projekty cílené na rozhraní .NET Framework v4.6.1 nebo vyšší:</span><span class="sxs-lookup"><span data-stu-id="9a531-157">For WPF, continuing with the example where you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher:</span></span>

    \lib
      \net461
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> <span data-ttu-id="9a531-158">Ve výchozím nastavení vlastností ovládacích prvků se zobrazí v rámci různé kategorie v inspektoru.</span><span class="sxs-lookup"><span data-stu-id="9a531-158">By default, control properties will show up under the Miscellaneous category in the property inspector.</span></span>

## <a name="use-strings-and-resources"></a><span data-ttu-id="9a531-159">Použití řetězců a prostředků</span><span class="sxs-lookup"><span data-stu-id="9a531-159">Use strings and resources</span></span>

<span data-ttu-id="9a531-160">Můžete vložit řetězcové prostředky (`.resw`) v balíčku, který lze použít ovládací prvek nebo náročné projektu UPW, nastavte **akce sestavení** vlastnost `.resw` do souboru **PRIResource**.</span><span class="sxs-lookup"><span data-stu-id="9a531-160">You can embed string resources (`.resw`) in your package that can be used by your control or the consuming UWP project, set the **Build Action** property of the `.resw` file to **PRIResource**.</span></span>

<span data-ttu-id="9a531-161">Příklad najdete v tématu [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) v ukázce ExtensionSDKasNuGetPackage.</span><span class="sxs-lookup"><span data-stu-id="9a531-161">For an example, refer to [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) in the ExtensionSDKasNuGetPackage sample.</span></span>

> [!Note]
> <span data-ttu-id="9a531-162">To se vztahuje pouze na ovládacích prvků UPW.</span><span class="sxs-lookup"><span data-stu-id="9a531-162">This is applicable only to UWP controls.</span></span>

## <a name="see-also"></a><span data-ttu-id="9a531-163">Viz také:</span><span class="sxs-lookup"><span data-stu-id="9a531-163">See also</span></span>

- [<span data-ttu-id="9a531-164">Vytvoření balíčků UPW</span><span class="sxs-lookup"><span data-stu-id="9a531-164">Create UWP Packages</span></span>](create-uwp-packages.md)
- [<span data-ttu-id="9a531-165">Ukázka ExtensionSDKasNuGetPackage</span><span class="sxs-lookup"><span data-stu-id="9a531-165">ExtensionSDKasNuGetPackage sample</span></span>](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
