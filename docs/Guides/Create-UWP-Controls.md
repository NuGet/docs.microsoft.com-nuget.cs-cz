---
title: "Jak zabalit UWP ovládací prvky s NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 3/21/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 1f9de20a-f394-4cf2-8e40-ba0f4239cd5e
description: "Postup vytvoření balíčků NuGet, které obsahují UWP řídí včetně nezbytné metadata a podpůrné soubory pro Visual Studio a nástroj Blend návrháře."
keywords: "Ovládací prvky NuGet UWP, Návrhář Visual Studio XAML, Návrhář Blend, vlastní ovládací prvky"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8756ce472c11a05370914841245295361b3f179b
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/05/2018
---
# <a name="creating-uwp-controls-as-nuget-packages"></a><span data-ttu-id="91a70-104">Vytváření ovládacích prvků UPW jako balíčků NuGet</span><span class="sxs-lookup"><span data-stu-id="91a70-104">Creating UWP controls as NuGet packages</span></span>

<span data-ttu-id="91a70-105">Visual Studio 2017 můžete využít přidané možnosti pro ovládací prvky UWP přinášející balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="91a70-105">With Visual Studio 2017, you can take advantage of added capabilities for UWP controls that you deliver in NuGet packages.</span></span> <span data-ttu-id="91a70-106">Tento průvodce vás provede tyto možnosti [ExtensionSDKasNuGetPackage ukázka](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span><span class="sxs-lookup"><span data-stu-id="91a70-106">This guide walks you through these capabilities using the [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span></span> 

## <a name="pre-requisites"></a><span data-ttu-id="91a70-107">Předpoklady:</span><span class="sxs-lookup"><span data-stu-id="91a70-107">Pre-requisites:</span></span>

1.  <span data-ttu-id="91a70-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="91a70-108">Visual Studio 2017</span></span>
1.  <span data-ttu-id="91a70-109">Přehled o tom, jak [vytvořit balíčky UWP](create-uwp-packages.md)</span><span class="sxs-lookup"><span data-stu-id="91a70-109">Understanding of how to [Create UWP Packages](create-uwp-packages.md)</span></span>

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a><span data-ttu-id="91a70-110">Přidání podpory podokna nástrojů nebo prostředky pro ovládací prvky jazyka XAML</span><span class="sxs-lookup"><span data-stu-id="91a70-110">Add toolbox/assets pane support for XAML controls</span></span>

<span data-ttu-id="91a70-111">Pokud chcete, aby ovládacího prvku XAML, zobrazí v sadě nástrojů Návrhář XAML v sadě Visual Studio a podokně prostředky Blend, vytvořte `VisualStudioToolsManifest.xml` soubor v kořenovém `tools` složky balíčku projektu.</span><span class="sxs-lookup"><span data-stu-id="91a70-111">To have a XAML control appear in the XAML designer’s toolbox in Visual Studio and the Assets pane of Blend, create a `VisualStudioToolsManifest.xml` file in the root of the `tools` folder of your package project.</span></span> <span data-ttu-id="91a70-112">Tento soubor se nevyžaduje, pokud nepotřebujete, než se objeví v soupravy nástrojů nebo prostředky podokně ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="91a70-112">This file is not required if you don’t need the control to appear in the toolbox or Assets pane.</span></span>

```
\build
\lib
\tools
    \VisualStudioToolsManifest.xml
```    

<span data-ttu-id="91a70-113">Struktura souboru je následující:</span><span class="sxs-lookup"><span data-stu-id="91a70-113">The structure of the file is as follows:</span></span>

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

<span data-ttu-id="91a70-114">kde:</span><span class="sxs-lookup"><span data-stu-id="91a70-114">where:</span></span>

- <span data-ttu-id="91a70-115">*your_package_file*: soubor název vlastního ovládacího prvku, třeba `ManagedPackage.winmd` ("ManagedPackage" je libovolnou s názvem používá v tomto příkladu a nemá žádný další význam).</span><span class="sxs-lookup"><span data-stu-id="91a70-115">*your_package_file*: the name of your control file, such as `ManagedPackage.winmd` ("ManagedPackage" is an arbitrary named used for this example and has no other meaning).</span></span>
- <span data-ttu-id="91a70-116">*vs_category*: štítek pro skupinu, ve kterém by se měla objevit ovládací prvek v sadě nástrojů Visual Studio designer.</span><span class="sxs-lookup"><span data-stu-id="91a70-116">*vs_category*: The label for the group in which the control should appear in the Visual Studio designer’s toolbox.</span></span> <span data-ttu-id="91a70-117">A `VSCategory` je nezbytné pro ovládací prvek se objeví v panelu nástrojů.</span><span class="sxs-lookup"><span data-stu-id="91a70-117">A `VSCategory` is necessary for the control to appear in the toolbox.</span></span>
- <span data-ttu-id="91a70-118">*blend_category*: štítek pro skupinu, ve kterém by se měla objevit ovládacího prvku v podokně prostředky návrháře Blend.</span><span class="sxs-lookup"><span data-stu-id="91a70-118">*blend_category*: The label for the group in which the control should appear in the Blend designer’s Assets pane.</span></span> <span data-ttu-id="91a70-119">A `BlendCategory` je nezbytné pro ovládací prvek zobrazí v prostředky.</span><span class="sxs-lookup"><span data-stu-id="91a70-119">A `BlendCategory` is necessary for the control to appear in Assets.</span></span>
- <span data-ttu-id="91a70-120">*type_full_name_n*: plně kvalifikovaný název pro každý ovládací prvek, včetně oboru názvů, jako například `ManagedPackage.MyCustomControl`.</span><span class="sxs-lookup"><span data-stu-id="91a70-120">*type_full_name_n*: The fully-qualified name for each control, including the namespace, such as `ManagedPackage.MyCustomControl`.</span></span> <span data-ttu-id="91a70-121">Všimněte si, že formát tečkou se používá pro spravovaná a nativní typy.</span><span class="sxs-lookup"><span data-stu-id="91a70-121">Note that the dot format is used for both managed and native types.</span></span>

<span data-ttu-id="91a70-122">V pokročilejších scénářích, můžete použít také více `<File>` elementů v rámci `<FileList>` když jeden balíček obsahuje více sestavení ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="91a70-122">In more advanced scenarios, you can also include multiple `<File>` elements within `<FileList>` when a single package contains multiple control assemblies.</span></span> <span data-ttu-id="91a70-123">Také můžete mít více `<ToolboxItems>` uzly v rámci jednoho `<File>` Pokud budete chtít uspořádání ovládacích prvků do samostatných kategorií.</span><span class="sxs-lookup"><span data-stu-id="91a70-123">You can also have multiple `<ToolboxItems>` nodes within a single `<File>` if you want to organize your controls into separate categories.</span></span>

<span data-ttu-id="91a70-124">V následujícím příkladu ovládacího prvku implementované v `ManagedPackage.winmd` se zobrazí v sadě Visual Studio a přizpůsobte ve skupině s názvem "Spravované balíček" a "MyCustomControl" se zobrazí v této skupině.</span><span class="sxs-lookup"><span data-stu-id="91a70-124">In the following example, the control implemented in `ManagedPackage.winmd` will appear in Visual Studio and Blend in a group named “Managed Package”, and “MyCustomControl” will appear in that group.</span></span> <span data-ttu-id="91a70-125">Všechny tyto názvy jsou libovolný.</span><span class="sxs-lookup"><span data-stu-id="91a70-125">All these names are arbitrary.</span></span>

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
> <span data-ttu-id="91a70-128">Je třeba explicitně zadat každý ovládací prvek, který chcete zobrazit v podokně nástrojů nebo prostředky.</span><span class="sxs-lookup"><span data-stu-id="91a70-128">You must explicitly specify every control that you would like to see in the toolbox/assets pane.</span></span> <span data-ttu-id="91a70-129">Ujistěte se, zadejte ve formátu `Namespace.ControlName`.</span><span class="sxs-lookup"><span data-stu-id="91a70-129">Ensure you specify them in the format `Namespace.ControlName`.</span></span>

## <a name="add-custom-icons-to-your-controls"></a><span data-ttu-id="91a70-130">Přidat vlastní ikony pro vaše ovládací prvky</span><span class="sxs-lookup"><span data-stu-id="91a70-130">Add custom icons to your controls</span></span>

<span data-ttu-id="91a70-131">Vlastní ikonu na panelu nástrojů nebo prostředky zobrazíte přidat bitovou kopii do projektu nebo odpovídající `design.dll` projektu s názvem "Namespace.ControlName.extension" a nastavte akce sestavení "Vložený prostředek".</span><span class="sxs-lookup"><span data-stu-id="91a70-131">To display a custom icon in the toolbox/assets pane, add an image to your project or the corresponding `design.dll` project with the name “Namespace.ControlName.extension” and set the build action to “Embedded Resource”.</span></span> <span data-ttu-id="91a70-132">Podporované formáty jsou `.png`, `.jpg`, `.jpeg`, `.gif`, a `.bmp`.</span><span class="sxs-lookup"><span data-stu-id="91a70-132">Supported formats are `.png`, `.jpg`, `.jpeg`, `.gif`, and `.bmp`.</span></span> <span data-ttu-id="91a70-133">Doporučené obrázek je 64 × 64 pixelů.</span><span class="sxs-lookup"><span data-stu-id="91a70-133">The recommended image size is 64 pixels by 64 pixels.</span></span>

<span data-ttu-id="91a70-134">V následujícím příkladu projekt obsahuje soubor bitové kopie s názvem "ManagedPackage.MyCustomControl.png".</span><span class="sxs-lookup"><span data-stu-id="91a70-134">In the example below, the project contains an image file named “ManagedPackage.MyCustomControl.png”.</span></span>

![Nastavení vlastní ikonou v projektu](media/UWP-control-custom-icon.png)

> [!Note]
> <span data-ttu-id="91a70-136">Pro nativní ovládací prvky, musíte umístit na ikonu jako prostředek v `design.dll` projektu.</span><span class="sxs-lookup"><span data-stu-id="91a70-136">For native controls, you must put the icon as a resource in the `design.dll` project.</span></span>

## <a name="support-specific-windows-platform-versions"></a><span data-ttu-id="91a70-137">Podporují konkrétní verze platformy Windows</span><span class="sxs-lookup"><span data-stu-id="91a70-137">Support specific Windows platform versions</span></span>

<span data-ttu-id="91a70-138">Balíčky UWP mít TargetPlatformVersion (TPV) a TargetPlatformMinVersion (TPMinV), které definují horní a dolní meze verze operačního systému nainstalovanou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="91a70-138">UWP packages have a TargetPlatformVersion (TPV) and TargetPlatformMinVersion (TPMinV) that define the upper and lower bounds of the OS version where the app can be installed.</span></span> <span data-ttu-id="91a70-139">Další TPV Určuje verzi sady SDK, pro kterou je integrovaná aplikace.</span><span class="sxs-lookup"><span data-stu-id="91a70-139">TPV further specifies the version of the SDK against which the app is built.</span></span> <span data-ttu-id="91a70-140">Mějte na paměti tyto vlastnosti při vytváření balíčku UWP: použití rozhraní API mimo hranice verze platforem, které jsou definované v aplikaci způsobí selhání sestavení nebo aplikaci k selhání za běhu.</span><span class="sxs-lookup"><span data-stu-id="91a70-140">Be mindful of these properties when authoring a UWP package: using APIs outside the bounds of the platform versions defined in the app will cause either the build to fail or the app to fail at runtime.</span></span>

<span data-ttu-id="91a70-141">Například Řekněme, že jste nastavili TPMinV pro ovládací prvky balíček Windows 10 Anniversary Edition (10.0; Sestavení 14393), takže chcete zajistit, že balíček je spotřebovávají pouze UWP projekty odpovídající dolní mez.</span><span class="sxs-lookup"><span data-stu-id="91a70-141">For example, let’s say you’ve set the TPMinV for you controls package to Windows 10 Anniversary Edition (10.0; Build 14393), so you want to ensure that the package is consumed only by UWP projects that match that lower bound.</span></span> <span data-ttu-id="91a70-142">Umožňuje vašemu balíčku uplatníte `project.json` UWP projekty založené na vaše ovládací prvky s následující názvy složek musí balíčku:</span><span class="sxs-lookup"><span data-stu-id="91a70-142">To allow your package to be consumed by `project.json` based UWP projects, you must package your controls with the following folder names:</span></span>

```
\lib\uap10.0\*
\ref\uap10.0\*
```

<span data-ttu-id="91a70-143">Chcete-li vynutit příslušné kontroly TPMinV, vytvořit [souboru cíle MSBuild](/visualstudio/msbuild/msbuild-targets) a balíčků ve složce sestavení (nahrazení "your_assembly_name" s název vaší konkrétní sestavení):</span><span class="sxs-lookup"><span data-stu-id="91a70-143">To enforce the appropriate TPMinV check, create an [MSBuild targets file](/visualstudio/msbuild/msbuild-targets) and package it under the build folder (replacing "your_assembly_name" with the name of your specific assembly):</span></span>

```
\build
    \uap10.0
        your_assembly_name.targets
\lib
\tools
```

<span data-ttu-id="91a70-144">Tady je příklad, jak by měla vypadat soubor cíle:</span><span class="sxs-lookup"><span data-stu-id="91a70-144">Here is an example of what the targets file should look like:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

  <Target Name="TPMinVCheck" BeforeTargets="Build;ReBuild" Condition="'$(TargetPlatformMinVersion)' != ''">
    <PropertyGroup>
      <RequiredTPMinV>10.0.14393</RequiredTPMinV>
      <ActualTPMinV>$(TargetPlatformMinVersion)</ActualTPMinV>
    </PropertyGroup>
    <Error Condition=" '$([System.Version]::Parse($(ActualTPMinV)).CompareTo($([System.Version]::Parse($(RequiredTPMinV)))))' == '-1' "        Text = "The INSERT_PACKAGE_ID_HERE nuget package cannot be used in the $(MSBuildProjectName) project since the project's TargetPlatformMinVersion - $(ActualTPMinV) does not match the Minimum Version - $(RequiredTPMinV) supported by the package" />
  </Target>
</Project>
```

## <a name="add-design-time-support"></a><span data-ttu-id="91a70-145">Přidání podpory návrhu</span><span class="sxs-lookup"><span data-stu-id="91a70-145">Add design-time support</span></span>

<span data-ttu-id="91a70-146">Konfigurace, kde vlastnosti ovládacích prvků zobrazí v inspector vlastnost, přidejte vlastní ozdobného prvku atd., umístěte vaše `design.dll` souboru uvnitř `lib\<platform>\Design` složku v závislosti na cílové platformy.</span><span class="sxs-lookup"><span data-stu-id="91a70-146">To configure where the control properties show up in the property inspector, add custom adorners, etc., place your `design.dll` file inside the `lib\<platform>\Design` folder as appropriate to the target platform.</span></span> <span data-ttu-id="91a70-147">Také zajistit, aby  **[upravit šablonu > Upravit kopii](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)**  funkce funguje, je nutné zahrnout `Generic.xaml` a všechny slovnících prostředků, které se sloučí v `<AssemblyName>\Themes` složky.</span><span class="sxs-lookup"><span data-stu-id="91a70-147">Also, to ensure that the **[Edit Template > Edit a Copy](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** feature works, you must include the `Generic.xaml` and any resource dictionaries that it merges in the `<AssemblyName>\Themes` folder.</span></span> <span data-ttu-id="91a70-148">(Tento soubor nemá žádný vliv na modul runtime chování ovládacího prvku.)</span><span class="sxs-lookup"><span data-stu-id="91a70-148">(This file has no impact on the runtime behavior of a control.)</span></span>


```
\build
\lib
    \uap10.0.14393.0
        \Design
            \MyControl.design.dll
        \your_assembly_name
            \Themes     
                Generic.xaml
\tools
```

> [!Note]
> <span data-ttu-id="91a70-149">Ve výchozím nastavení vlastností ovládacího prvku se zobrazí na různé kategorie v inspector vlastnost.</span><span class="sxs-lookup"><span data-stu-id="91a70-149">By default, control properties will show up under the Miscellaneous category in the property inspector.</span></span>


## <a name="use-strings-and-resources"></a><span data-ttu-id="91a70-150">Použití řetězců a prostředky</span><span class="sxs-lookup"><span data-stu-id="91a70-150">Use strings and resources</span></span>

<span data-ttu-id="91a70-151">Můžete vložit řetězcové prostředky (`.resw`) do balíčku, který můžete použít vlastní ovládací prvek nebo využívání projektu UPW, nastavte **akce sestavení** vlastnost `.resw` do souboru **PRIResource**.</span><span class="sxs-lookup"><span data-stu-id="91a70-151">You can embed string resources (`.resw`) in your package that can be used by your control or the consuming UWP project, set the **Build Action** property of the `.resw` file to **PRIResource**.</span></span>

<span data-ttu-id="91a70-152">Příklad najdete v části [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) v ukázce ExtensionSDKasNuGetPackage.</span><span class="sxs-lookup"><span data-stu-id="91a70-152">For an example, refer to [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) in the ExtensionSDKasNuGetPackage sample.</span></span>

## <a name="package-content-such-as-images"></a><span data-ttu-id="91a70-153">Obsah balíčku, jako jsou bitové kopie</span><span class="sxs-lookup"><span data-stu-id="91a70-153">Package content such as images</span></span>

<span data-ttu-id="91a70-154">Obsah balíčku, například bitové kopie, které mohou být využívána vlastní ovládací prvek nebo využívání projektu UPW.</span><span class="sxs-lookup"><span data-stu-id="91a70-154">To package content such as images that can be used by your control or the consuming UWP project.</span></span> <span data-ttu-id="91a70-155">Přidejte tyto soubory `lib\uap10.0.14393.0` složky následujícím způsobem ("your_assembly_name" znovu shodovat s vaší konkrétní ovládací prvek):</span><span class="sxs-lookup"><span data-stu-id="91a70-155">add those files `lib\uap10.0.14393.0` folder as follows ("your_assembly_name" should again match your particular control):</span></span>

```
\build
\lib
    \uap10.0.14393.0
        \Design
        \your_assembly_name
\contosoSampleImage.jpg
\tools
```

<span data-ttu-id="91a70-156">Mohou také vytvářet[souboru cíle MSBuild](/visualstudio/msbuild/msbuild-targets) zajistit asset se zkopíruje do výstupní složky náročné projektu:</span><span class="sxs-lookup"><span data-stu-id="91a70-156">You may also author an[MSBuild targets file](/visualstudio/msbuild/msbuild-targets) to ensure the asset is copied to the consuming project’s output folder:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Content Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0.14393.0\contosoSampleImage.jpg">
            <CopyToOutputDirectory>Always</CopyToOutputDirectory>
        </Content>
    </ItemGroup>
</Project>
```

## <a name="see-also"></a><span data-ttu-id="91a70-157">Viz také</span><span class="sxs-lookup"><span data-stu-id="91a70-157">See also</span></span>

- [<span data-ttu-id="91a70-158">Vytvoření balíčků UPW</span><span class="sxs-lookup"><span data-stu-id="91a70-158">Create UWP Packages</span></span>](create-uwp-packages.md)
- [<span data-ttu-id="91a70-159">Ukázka ExtensionSDKasNuGetPackage</span><span class="sxs-lookup"><span data-stu-id="91a70-159">ExtensionSDKasNuGetPackage sample</span></span>](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
