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
# <a name="creating-ui-controls-as-nuget-packages"></a><span data-ttu-id="a153f-103">Vytváření ovládacích prvků uživatelského rozhraní jako balíčků NuGet</span><span class="sxs-lookup"><span data-stu-id="a153f-103">Creating UI controls as NuGet packages</span></span>

<span data-ttu-id="a153f-104">Visual Studio 2017 můžete využít přidaných funkcí pro UPW a WPF ovládacích prvků, které doručit do balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="a153f-104">With Visual Studio 2017, you can take advantage of added capabilities for UWP and WPF controls that you deliver in NuGet packages.</span></span> <span data-ttu-id="a153f-105">Tento průvodce vás provede tyto funkce v kontextu UWP ovládacích prvků pomocí [ExtensionSDKasNuGetPackage ukázka](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span><span class="sxs-lookup"><span data-stu-id="a153f-105">This guide walks you through these capabilities in context of UWP controls using the [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span></span> <span data-ttu-id="a153f-106">Totéž platí i pro ovládacích prvků WPF Jestliže není uvedeno jinak.</span><span class="sxs-lookup"><span data-stu-id="a153f-106">The same applies to WPF controls unless mentioned otherwise.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a153f-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="a153f-107">Prerequisites</span></span>

1. <span data-ttu-id="a153f-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="a153f-108">Visual Studio 2017</span></span>
1. <span data-ttu-id="a153f-109">Přehled o tom, jak [vytvořit balíčky UWP](create-uwp-packages.md)</span><span class="sxs-lookup"><span data-stu-id="a153f-109">Understanding of how to [Create UWP Packages](create-uwp-packages.md)</span></span>

## <a name="generate-library-layout"></a><span data-ttu-id="a153f-110">Generovat knihovny rozložení</span><span class="sxs-lookup"><span data-stu-id="a153f-110">Generate Library Layout</span></span>

> [!Note]
> <span data-ttu-id="a153f-111">To se vztahuje pouze na UWP ovládací prvky.</span><span class="sxs-lookup"><span data-stu-id="a153f-111">This is applicable only to UWP controls.</span></span>

<span data-ttu-id="a153f-112">Nastavení `GenerateLibraryLayout` vlastnost zajistí, že je v rozložení, který je připraven k zabalené bez nutnosti položky jednotlivých souborů v soubor nuspec vygenerováno výstupu sestavení projektu.</span><span class="sxs-lookup"><span data-stu-id="a153f-112">Setting the `GenerateLibraryLayout` property ensures that the project build output is generated in a layout that is ready to be packaged without the need for individual file entries in the nuspec.</span></span>

<span data-ttu-id="a153f-113">Z vlastností projektu přejděte na kartu sestavení a zaškrtnutím políčka "Generovat knihovny rozložení".</span><span class="sxs-lookup"><span data-stu-id="a153f-113">From the project properties, go to the build tab and check the "Generate Library Layout" check box.</span></span> <span data-ttu-id="a153f-114">Tato akce upravit soubor projektu a nastavit `GenerateLibraryLayout` příznak na hodnotu true pro aktuálně vybrané konfigurace sestavení a platformu.</span><span class="sxs-lookup"><span data-stu-id="a153f-114">This will modify the project file and set the `GenerateLibraryLayout` flag to true for your currently selected build configuration and platform.</span></span>

<span data-ttu-id="a153f-115">Můžete také upravit souboru projektu přidejte `<GenerateLibraryLayout>true</GenerateLibraryLayout>` ke skupině první nepodmíněné vlastnost.</span><span class="sxs-lookup"><span data-stu-id="a153f-115">Alternately, edit the the project file to add `<GenerateLibraryLayout>true</GenerateLibraryLayout>` to the first unconditional property group.</span></span> <span data-ttu-id="a153f-116">To platí vlastnost bez ohledu na platformu a konfigurace sestavení.</span><span class="sxs-lookup"><span data-stu-id="a153f-116">This would apply the property irrespective of the build configuration and platform.</span></span>

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a><span data-ttu-id="a153f-117">Přidání podpory podokna nástrojů nebo prostředky pro ovládací prvky jazyka XAML</span><span class="sxs-lookup"><span data-stu-id="a153f-117">Add toolbox/assets pane support for XAML controls</span></span>

<span data-ttu-id="a153f-118">Pokud chcete, aby ovládacího prvku XAML, zobrazí v sadě nástrojů Návrhář XAML v sadě Visual Studio a podokně prostředky Blend, vytvořte `VisualStudioToolsManifest.xml` soubor v kořenovém `tools` složky balíčku projektu.</span><span class="sxs-lookup"><span data-stu-id="a153f-118">To have a XAML control appear in the XAML designer’s toolbox in Visual Studio and the Assets pane of Blend, create a `VisualStudioToolsManifest.xml` file in the root of the `tools` folder of your package project.</span></span> <span data-ttu-id="a153f-119">Tento soubor se nevyžaduje, pokud nepotřebujete, než se objeví v soupravy nástrojů nebo prostředky podokně ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="a153f-119">This file is not required if you don’t need the control to appear in the toolbox or Assets pane.</span></span>

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

<span data-ttu-id="a153f-120">Struktura souboru je následující:</span><span class="sxs-lookup"><span data-stu-id="a153f-120">The structure of the file is as follows:</span></span>

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

<span data-ttu-id="a153f-121">kde:</span><span class="sxs-lookup"><span data-stu-id="a153f-121">where:</span></span>

- <span data-ttu-id="a153f-122">*your_package_file*: soubor název vlastního ovládacího prvku, třeba `ManagedPackage.winmd` ("ManagedPackage" je libovolnou s názvem používá v tomto příkladu a nemá žádný další význam).</span><span class="sxs-lookup"><span data-stu-id="a153f-122">*your_package_file*: the name of your control file, such as `ManagedPackage.winmd` ("ManagedPackage" is an arbitrary named used for this example and has no other meaning).</span></span>
- <span data-ttu-id="a153f-123">*vs_category*: štítek pro skupinu, ve kterém by se měla objevit ovládací prvek v sadě nástrojů Visual Studio designer.</span><span class="sxs-lookup"><span data-stu-id="a153f-123">*vs_category*: The label for the group in which the control should appear in the Visual Studio designer’s toolbox.</span></span> <span data-ttu-id="a153f-124">A `VSCategory` je nezbytné pro ovládací prvek se objeví v panelu nástrojů.</span><span class="sxs-lookup"><span data-stu-id="a153f-124">A `VSCategory` is necessary for the control to appear in the toolbox.</span></span>
- <span data-ttu-id="a153f-125">*blend_category*: štítek pro skupinu, ve kterém by se měla objevit ovládacího prvku v podokně prostředky návrháře Blend.</span><span class="sxs-lookup"><span data-stu-id="a153f-125">*blend_category*: The label for the group in which the control should appear in the Blend designer’s Assets pane.</span></span> <span data-ttu-id="a153f-126">A `BlendCategory` je nezbytné pro ovládací prvek zobrazí v prostředky.</span><span class="sxs-lookup"><span data-stu-id="a153f-126">A `BlendCategory` is necessary for the control to appear in Assets.</span></span>
- <span data-ttu-id="a153f-127">*type_full_name_n*: plně kvalifikovaný název pro každý ovládací prvek, včetně oboru názvů, jako například `ManagedPackage.MyCustomControl`.</span><span class="sxs-lookup"><span data-stu-id="a153f-127">*type_full_name_n*: The fully-qualified name for each control, including the namespace, such as `ManagedPackage.MyCustomControl`.</span></span> <span data-ttu-id="a153f-128">Všimněte si, že formát tečkou se používá pro spravovaná a nativní typy.</span><span class="sxs-lookup"><span data-stu-id="a153f-128">Note that the dot format is used for both managed and native types.</span></span>

<span data-ttu-id="a153f-129">V pokročilejších scénářích, můžete použít také více `<File>` elementů v rámci `<FileList>` když jeden balíček obsahuje více sestavení ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="a153f-129">In more advanced scenarios, you can also include multiple `<File>` elements within `<FileList>` when a single package contains multiple control assemblies.</span></span> <span data-ttu-id="a153f-130">Také můžete mít více `<ToolboxItems>` uzly v rámci jednoho `<File>` Pokud budete chtít uspořádání ovládacích prvků do samostatných kategorií.</span><span class="sxs-lookup"><span data-stu-id="a153f-130">You can also have multiple `<ToolboxItems>` nodes within a single `<File>` if you want to organize your controls into separate categories.</span></span>

<span data-ttu-id="a153f-131">V následujícím příkladu ovládacího prvku implementované v `ManagedPackage.winmd` se zobrazí v sadě Visual Studio a přizpůsobte ve skupině s názvem "Spravované balíček" a "MyCustomControl" se zobrazí v této skupině.</span><span class="sxs-lookup"><span data-stu-id="a153f-131">In the following example, the control implemented in `ManagedPackage.winmd` will appear in Visual Studio and Blend in a group named “Managed Package”, and “MyCustomControl” will appear in that group.</span></span> <span data-ttu-id="a153f-132">Všechny tyto názvy jsou libovolný.</span><span class="sxs-lookup"><span data-stu-id="a153f-132">All these names are arbitrary.</span></span>

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
> <span data-ttu-id="a153f-135">Je třeba explicitně zadat každý ovládací prvek, který chcete zobrazit v podokně nástrojů nebo prostředky.</span><span class="sxs-lookup"><span data-stu-id="a153f-135">You must explicitly specify every control that you would like to see in the toolbox/assets pane.</span></span> <span data-ttu-id="a153f-136">Ujistěte se, zadejte ve formátu `Namespace.ControlName`.</span><span class="sxs-lookup"><span data-stu-id="a153f-136">Ensure you specify them in the format `Namespace.ControlName`.</span></span>

## <a name="add-custom-icons-to-your-controls"></a><span data-ttu-id="a153f-137">Přidat vlastní ikony pro vaše ovládací prvky</span><span class="sxs-lookup"><span data-stu-id="a153f-137">Add custom icons to your controls</span></span>

<span data-ttu-id="a153f-138">Vlastní ikonu na panelu nástrojů nebo prostředky zobrazíte přidat bitovou kopii do projektu nebo odpovídající `design.dll` projektu s názvem "Namespace.ControlName.extension" a nastavte akce sestavení "Vložený prostředek".</span><span class="sxs-lookup"><span data-stu-id="a153f-138">To display a custom icon in the toolbox/assets pane, add an image to your project or the corresponding `design.dll` project with the name “Namespace.ControlName.extension” and set the build action to “Embedded Resource”.</span></span> <span data-ttu-id="a153f-139">Podporované formáty jsou `.png`, `.jpg`, `.jpeg`, `.gif`, a `.bmp`.</span><span class="sxs-lookup"><span data-stu-id="a153f-139">Supported formats are `.png`, `.jpg`, `.jpeg`, `.gif`, and `.bmp`.</span></span> <span data-ttu-id="a153f-140">Doporučené obrázek je 64 × 64 pixelů.</span><span class="sxs-lookup"><span data-stu-id="a153f-140">The recommended image size is 64 pixels by 64 pixels.</span></span>

<span data-ttu-id="a153f-141">V následujícím příkladu projekt obsahuje soubor bitové kopie s názvem "ManagedPackage.MyCustomControl.png".</span><span class="sxs-lookup"><span data-stu-id="a153f-141">In the example below, the project contains an image file named “ManagedPackage.MyCustomControl.png”.</span></span>

![Nastavení vlastní ikonou v projektu](media/UWP-control-custom-icon.png)

> [!Note]
> <span data-ttu-id="a153f-143">Pro nativní ovládací prvky, musíte umístit na ikonu jako prostředek v `design.dll` projektu.</span><span class="sxs-lookup"><span data-stu-id="a153f-143">For native controls, you must put the icon as a resource in the `design.dll` project.</span></span>

## <a name="support-specific-windows-platform-versions"></a><span data-ttu-id="a153f-144">Podporují konkrétní verze platformy Windows</span><span class="sxs-lookup"><span data-stu-id="a153f-144">Support specific Windows platform versions</span></span>

<span data-ttu-id="a153f-145">Balíčky UWP mít TargetPlatformVersion (TPV) a TargetPlatformMinVersion (TPMinV), které definují horní a dolní meze verze operačního systému nainstalovanou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="a153f-145">UWP packages have a TargetPlatformVersion (TPV) and TargetPlatformMinVersion (TPMinV) that define the upper and lower bounds of the OS version where the app can be installed.</span></span> <span data-ttu-id="a153f-146">Další TPV Určuje verzi sady SDK, pro kterou je integrovaná aplikace.</span><span class="sxs-lookup"><span data-stu-id="a153f-146">TPV further specifies the version of the SDK against which the app is built.</span></span> <span data-ttu-id="a153f-147">Mějte na paměti tyto vlastnosti při vytváření balíčku UWP: použití rozhraní API mimo hranice verze platforem, které jsou definované v aplikaci způsobí selhání sestavení nebo aplikaci k selhání za běhu.</span><span class="sxs-lookup"><span data-stu-id="a153f-147">Be mindful of these properties when authoring a UWP package: using APIs outside the bounds of the platform versions defined in the app will cause either the build to fail or the app to fail at runtime.</span></span>

<span data-ttu-id="a153f-148">Například Řekněme, že jste nastavili TPMinV pro vaše ovládací prvky balíček do Windows 10 Anniversary Edition (10.0; Sestavení 14393), takže chcete zajistit, že balíček je spotřebovávají pouze UWP projekty odpovídající dolní mez.</span><span class="sxs-lookup"><span data-stu-id="a153f-148">For example, let’s say you’ve set the TPMinV for your controls package to Windows 10 Anniversary Edition (10.0; Build 14393), so you want to ensure that the package is consumed only by UWP projects that match that lower bound.</span></span> <span data-ttu-id="a153f-149">Povolit vašeho balíčku pro projekty UWP, musí balíček vaše ovládací prvky s následující názvy složek:</span><span class="sxs-lookup"><span data-stu-id="a153f-149">To allow your package to be consumed by UWP projects, you must package your controls with the following folder names:</span></span>

    \lib\uap10.0.14393\*
    \ref\uap10.0.14393\*

<span data-ttu-id="a153f-150">NuGet automaticky zkontroluje TPMinV náročné projektu a pokud je nižší než Windows 10 Anniversary Edition (10.0; selhat instalace Sestavení 14393)</span><span class="sxs-lookup"><span data-stu-id="a153f-150">NuGet will automatically check the TPMinV of the consuming project, and fail installation if it is lower than Windows 10 Anniversary Edition (10.0; Build 14393)</span></span>

<span data-ttu-id="a153f-151">V případě WPF Řekněme, že byste chtěli vašeho balíčku ovládacích prvků WPF spotřebované projekty cílení na rozhraní .NET Framework v4.6.1 nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="a153f-151">In case of WPF, let's say you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher.</span></span> <span data-ttu-id="a153f-152">Pokud chcete vynutit, který, musí balíček vaše ovládací prvky s následující názvy složek:</span><span class="sxs-lookup"><span data-stu-id="a153f-152">To enforce that, you must package your controls with the following folder names:</span></span>

    \lib\net461\*
    \ref\net461\*

## <a name="add-design-time-support"></a><span data-ttu-id="a153f-153">Přidání podpory návrhu</span><span class="sxs-lookup"><span data-stu-id="a153f-153">Add design-time support</span></span>

<span data-ttu-id="a153f-154">Konfigurace, kde vlastnosti ovládacích prvků zobrazí v inspector vlastnost, přidejte vlastní ozdobného prvku atd., umístěte vaše `design.dll` souboru uvnitř `lib\uap10.0.14393\Design` složku v závislosti na cílové platformy.</span><span class="sxs-lookup"><span data-stu-id="a153f-154">To configure where the control properties show up in the property inspector, add custom adorners, etc., place your `design.dll` file inside the `lib\uap10.0.14393\Design` folder as appropriate to the target platform.</span></span> <span data-ttu-id="a153f-155">Také zajistit, aby **[upravit šablonu > Upravit kopii](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** funkce funguje, je nutné zahrnout `Generic.xaml` a všechny slovnících prostředků, které se sloučí v `<your_assembly_name>\Themes` složky (znovu s použitím název vašeho skutečné sestavení).</span><span class="sxs-lookup"><span data-stu-id="a153f-155">Also, to ensure that the **[Edit Template > Edit a Copy](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** feature works, you must include the `Generic.xaml` and any resource dictionaries that it merges in the `<your_assembly_name>\Themes` folder (again, using your actual assembly name).</span></span> <span data-ttu-id="a153f-156">(Tento soubor nemá žádný vliv na modul runtime chování ovládacího prvku.) Struktura složek by proto vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="a153f-156">(This file has no impact on the runtime behavior of a control.) The folder structure would thus appear as follows:</span></span>

    \lib
      \uap10.0.14393
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml


<span data-ttu-id="a153f-157">Pro grafický subsystém WPF pokračování příkladu s, kam chcete vaší WPF prvky balíček spotřebované projekty cílení na rozhraní .NET Framework v4.6.1 nebo vyšší:</span><span class="sxs-lookup"><span data-stu-id="a153f-157">For WPF, continuing with the example where you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher:</span></span>

    \lib
      \net461
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> <span data-ttu-id="a153f-158">Ve výchozím nastavení vlastností ovládacího prvku se zobrazí na různé kategorie v inspector vlastnost.</span><span class="sxs-lookup"><span data-stu-id="a153f-158">By default, control properties will show up under the Miscellaneous category in the property inspector.</span></span>

## <a name="use-strings-and-resources"></a><span data-ttu-id="a153f-159">Použití řetězců a prostředky</span><span class="sxs-lookup"><span data-stu-id="a153f-159">Use strings and resources</span></span>

<span data-ttu-id="a153f-160">Můžete vložit řetězcové prostředky (`.resw`) do balíčku, který můžete použít vlastní ovládací prvek nebo využívání projektu UPW, nastavte **akce sestavení** vlastnost `.resw` do souboru **PRIResource**.</span><span class="sxs-lookup"><span data-stu-id="a153f-160">You can embed string resources (`.resw`) in your package that can be used by your control or the consuming UWP project, set the **Build Action** property of the `.resw` file to **PRIResource**.</span></span>

<span data-ttu-id="a153f-161">Příklad najdete v části [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) v ukázce ExtensionSDKasNuGetPackage.</span><span class="sxs-lookup"><span data-stu-id="a153f-161">For an example, refer to [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) in the ExtensionSDKasNuGetPackage sample.</span></span>

> [!Note]
> <span data-ttu-id="a153f-162">To se vztahuje pouze na UWP ovládací prvky.</span><span class="sxs-lookup"><span data-stu-id="a153f-162">This is applicable only to UWP controls.</span></span>

## <a name="see-also"></a><span data-ttu-id="a153f-163">Viz také:</span><span class="sxs-lookup"><span data-stu-id="a153f-163">See also</span></span>

- [<span data-ttu-id="a153f-164">Vytvoření balíčků UPW</span><span class="sxs-lookup"><span data-stu-id="a153f-164">Create UWP Packages</span></span>](create-uwp-packages.md)
- [<span data-ttu-id="a153f-165">Ukázka ExtensionSDKasNuGetPackage</span><span class="sxs-lookup"><span data-stu-id="a153f-165">ExtensionSDKasNuGetPackage sample</span></span>](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
