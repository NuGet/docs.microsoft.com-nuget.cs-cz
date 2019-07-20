---
title: Cílení na více platforem pro balíčky NuGet v souboru projektu
description: Popis různých metod, které cílí na více .NET Framework verzí z jednoho balíčku NuGet.
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: 1ff02871872cee9e8cbf8c7d7c74d804f7dc5b99
ms.sourcegitcommit: 0f5363353f9dc1c3d68e7718f51b7ff92bb35e21
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/19/2019
ms.locfileid: "68346151"
---
# <a name="support-multiple-net-framework-versions-in-your-project-file"></a><span data-ttu-id="dd3fe-103">Podpora více verzí .NET Framework v souboru projektu</span><span class="sxs-lookup"><span data-stu-id="dd3fe-103">Support multiple .NET Framework versions in your project file</span></span>

<span data-ttu-id="dd3fe-104">Při prvním vytvoření projektu doporučujeme vytvořit knihovnu tříd .NET Standard, protože poskytuje kompatibilitu s nejširší škálou náročných projektů.</span><span class="sxs-lookup"><span data-stu-id="dd3fe-104">When you first create a project, we recommend you create a .NET Standard class library, as it provides compatibility with the widest range of consuming projects.</span></span> <span data-ttu-id="dd3fe-105">Pomocí .NET Standard přidáte do knihovny .NET standardně [podporu více platforem](/dotnet/standard/library-guidance/cross-platform-targeting) .</span><span class="sxs-lookup"><span data-stu-id="dd3fe-105">By using .NET Standard, you add [cross-platform support](/dotnet/standard/library-guidance/cross-platform-targeting) to a .NET library by default.</span></span> <span data-ttu-id="dd3fe-106">V některých scénářích však může být také nutné zahrnout kód, který cílí na konkrétní rozhraní.</span><span class="sxs-lookup"><span data-stu-id="dd3fe-106">However, in some scenarios, you may also need to include code that targets a particular framework.</span></span> <span data-ttu-id="dd3fe-107">V tomto článku se dozvíte, jak to udělat pro projekty ve [stylu sady SDK](../resources/check-project-format.md) .</span><span class="sxs-lookup"><span data-stu-id="dd3fe-107">This article shows you how to do that for [SDK-style](../resources/check-project-format.md) projects.</span></span>

<span data-ttu-id="dd3fe-108">Pro projekty ve stylu sady SDK můžete v souboru projektu nakonfigurovat podporu pro více cílů architektury ([TFM](/dotnet/standard/frameworks)) a potom pomocí `dotnet pack` nebo `msbuild /t:pack` vytvořit balíček.</span><span class="sxs-lookup"><span data-stu-id="dd3fe-108">For SDK-style projects, you can configure support for multiple targets frameworks ([TFM](/dotnet/standard/frameworks)) in your project file, then use `dotnet pack` or `msbuild /t:pack` to create the package.</span></span>

> [!NOTE]
> <span data-ttu-id="dd3fe-109">NuGet. exe CLI nepodporuje projekty ve stylu balíčku sady SDK, takže byste měli použít `dotnet pack` jenom nebo. `msbuild /t:pack`</span><span class="sxs-lookup"><span data-stu-id="dd3fe-109">nuget.exe CLI does not support packing SDK-style projects, so you should only use `dotnet pack` or `msbuild /t:pack`.</span></span> <span data-ttu-id="dd3fe-110">Doporučujeme, abyste místo toho [zahrnuli všechny vlastnosti](../reference/msbuild-targets.md#pack-target) , které jsou obvykle `.nuspec` v souboru v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="dd3fe-110">We recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="dd3fe-111">Chcete-li cílit na více .NET Framework verzí v projektu ve stylu mimo sadu SDK, přečtěte si téma [Podpora více verzí .NET Framework](supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="dd3fe-111">To target multiple .NET Framework versions in a non-SDK-style project, see [Supporting multiple .NET Framework versions](supporting-multiple-target-frameworks.md).</span></span>

## <a name="create-a-project-that-supports-multiple-net-framework-versions"></a><span data-ttu-id="dd3fe-112">Vytvořit projekt, který podporuje více verzí .NET Framework</span><span class="sxs-lookup"><span data-stu-id="dd3fe-112">Create a project that supports multiple .NET Framework versions</span></span>

1. <span data-ttu-id="dd3fe-113">Vytvořte novou knihovnu tříd .NET Standard v aplikaci Visual Studio nebo ji použijte `dotnet new classlib`.</span><span class="sxs-lookup"><span data-stu-id="dd3fe-113">Create a new .NET Standard class library either in Visual Studio or use `dotnet new classlib`.</span></span>

   <span data-ttu-id="dd3fe-114">Pro zajištění nejlepší kompatibility doporučujeme vytvořit knihovnu tříd .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="dd3fe-114">We recommend that you create a .NET Standard class library for best compatibility.</span></span>

2. <span data-ttu-id="dd3fe-115">Upravte soubor *. csproj* pro podporu cílových rozhraní.</span><span class="sxs-lookup"><span data-stu-id="dd3fe-115">Edit the *.csproj* file to support the target frameworks.</span></span>

   <span data-ttu-id="dd3fe-116">Například změňte `<TargetFramework>netstandard2.0</TargetFramework>` na `<TargetFrameworks>netstandard2.0;net45</TargetFrameworks>`.</span><span class="sxs-lookup"><span data-stu-id="dd3fe-116">For example, change `<TargetFramework>netstandard2.0</TargetFramework>` to `<TargetFrameworks>netstandard2.0;net45</TargetFrameworks>`.</span></span>

   <span data-ttu-id="dd3fe-117">Ujistěte se, že změníte element XML změněn z čísla v množném čísle na plural (přidejte "s" do počátečních a uzavíracích značek).</span><span class="sxs-lookup"><span data-stu-id="dd3fe-117">Make sure that you change the XML element changed from singular to plural (add the "s" to both the open and close tags).</span></span>

3. <span data-ttu-id="dd3fe-118">Pokud máte nějaký kód, který funguje pouze v jednom TFM, můžete použít `#if NET45` nebo `#if NETSTANDARD20` k oddělení kódu závislého na TFM.</span><span class="sxs-lookup"><span data-stu-id="dd3fe-118">If you have any code that only works in one TFM, you can use `#if NET45` or `#if NETSTANDARD20` to separate TFM-dependent code.</span></span> <span data-ttu-id="dd3fe-119">(Další informace najdete v tématu [jak cílit na více cílů](/dotnet/core/tutorials/libraries#how-to-multitarget).) Například můžete použít následující kód:</span><span class="sxs-lookup"><span data-stu-id="dd3fe-119">(For more information, see [How to multitarget](/dotnet/core/tutorials/libraries#how-to-multitarget).) For example, you can use the following code:</span></span>

   ```csharp
   public string Platform {
      get {
   #if NET45
         return ".NET Framework"
   #elif NETSTANDARD2_0
         return ".NET Standard"
   #else
   #error This code block does not match csproj TargetFrameworks list
   #endif
      }
   }
   ```

4. <span data-ttu-id="dd3fe-120">Přidejte jakákoli metadata NuGet, která chcete, do vlastností *. csproj* jako vlastnosti MSBuild.</span><span class="sxs-lookup"><span data-stu-id="dd3fe-120">Add any NuGet metadata you want to the *.csproj* as MSBuild properties.</span></span>

   <span data-ttu-id="dd3fe-121">Seznam dostupných metadat balíčku a názvů vlastností MSBuild naleznete v tématu [targeting pack](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="dd3fe-121">For the list of available package metadata and the MSBuild property names, see [pack target](../reference/msbuild-targets.md#pack-target).</span></span> <span data-ttu-id="dd3fe-122">Viz také [řízení prostředků závislosti](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="dd3fe-122">Also see [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

   <span data-ttu-id="dd3fe-123">Pokud chcete oddělit vlastnosti týkající se sestavení z metadat NuGet, můžete použít jinou `PropertyGroup`vlastnost nebo umístit vlastnosti NuGet do jiného souboru a použít `Import` direktivu MSBuild k jejímu zahrnutí.</span><span class="sxs-lookup"><span data-stu-id="dd3fe-123">If you want to separate build-related properties from NuGet metadata, you can use a different `PropertyGroup`, or put the NuGet properties in another file and use MSBuild's `Import` directive to include it.</span></span> <span data-ttu-id="dd3fe-124">`Directory.Build.Props`a `Directory.Build.Targets` jsou podporované i od MSBuild 15,0.</span><span class="sxs-lookup"><span data-stu-id="dd3fe-124">`Directory.Build.Props` and `Directory.Build.Targets` are also supported starting with MSBuild 15.0.</span></span>

5. <span data-ttu-id="dd3fe-125">Nyní použijte `dotnet pack` a výsledný *nupkg* cílí na .NET Standard 2,0 i .NET Framework 4,5.</span><span class="sxs-lookup"><span data-stu-id="dd3fe-125">Now, use `dotnet pack` and the resulting *.nupkg* targets both .NET Standard 2.0 and .NET Framework 4.5.</span></span>

<span data-ttu-id="dd3fe-126">Zde je soubor *. csproj* , který je generován pomocí předchozích kroků a .NET Core SDK 2,2.</span><span class="sxs-lookup"><span data-stu-id="dd3fe-126">Here is the *.csproj* file that is generated using the preceding steps and .NET Core SDK 2.2.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFrameworks>netstandard2.0;net45</TargetFrameworks>
    <Description>Sample project that targets multiple TFMs</Description>
  </PropertyGroup>

</Project>
```

## <a name="see-also"></a><span data-ttu-id="dd3fe-127">Viz také:</span><span class="sxs-lookup"><span data-stu-id="dd3fe-127">See also</span></span>

<span data-ttu-id="dd3fe-128">[Určení cílových rozhraní](/dotnet/standard/frameworks#how-to-specify-target-frameworks)
cílících na[více platforem](/dotnet/standard/library-guidance/cross-platform-targeting)</span><span class="sxs-lookup"><span data-stu-id="dd3fe-128">[How to specify target frameworks](/dotnet/standard/frameworks#how-to-specify-target-frameworks)
[Cross-platform targeting](/dotnet/standard/library-guidance/cross-platform-targeting)</span></span>
