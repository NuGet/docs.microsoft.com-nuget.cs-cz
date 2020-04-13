---
title: Vícenásobné cílení pro balíčky NuGet v souboru projektu
description: Popis různých metod, které mají cílit na více verzí rozhraní .NET Framework z jednoho balíčku NuGet.
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: 1d23759433efb405fa5f0035049befced2c43d6b
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "72380677"
---
# <a name="support-multiple-net-framework-versions-in-your-project-file"></a><span data-ttu-id="6847c-103">Podpora více verzí rozhraní .NET Framework v souboru projektu</span><span class="sxs-lookup"><span data-stu-id="6847c-103">Support multiple .NET Framework versions in your project file</span></span>

<span data-ttu-id="6847c-104">Při prvním vytvoření projektu doporučujeme vytvořit knihovnu tříd .NET Standard, protože poskytuje kompatibilitu s nejširší škálou náročných projektů.</span><span class="sxs-lookup"><span data-stu-id="6847c-104">When you first create a project, we recommend you create a .NET Standard class library, as it provides compatibility with the widest range of consuming projects.</span></span> <span data-ttu-id="6847c-105">Pomocí standardu .NET Standard přidáte ve výchozím nastavení [podporu pro více platforem](/dotnet/standard/library-guidance/cross-platform-targeting) do knihovny .NET.</span><span class="sxs-lookup"><span data-stu-id="6847c-105">By using .NET Standard, you add [cross-platform support](/dotnet/standard/library-guidance/cross-platform-targeting) to a .NET library by default.</span></span> <span data-ttu-id="6847c-106">V některých případech však může být také nutné zahrnout kód, který se zaměřuje na konkrétní rámec.</span><span class="sxs-lookup"><span data-stu-id="6847c-106">However, in some scenarios, you may also need to include code that targets a particular framework.</span></span> <span data-ttu-id="6847c-107">Tento článek ukazuje, jak to udělat pro projekty [ve stylu sady SDK.](../resources/check-project-format.md)</span><span class="sxs-lookup"><span data-stu-id="6847c-107">This article shows you how to do that for [SDK-style](../resources/check-project-format.md) projects.</span></span>

<span data-ttu-id="6847c-108">Pro projekty ve stylu sady SDK můžete nakonfigurovat podporu pro více cílů `dotnet pack` rozhraní `msbuild /t:pack` [(TFM)](/dotnet/standard/frameworks)v souboru projektu, pak použít nebo vytvořit balíček.</span><span class="sxs-lookup"><span data-stu-id="6847c-108">For SDK-style projects, you can configure support for multiple targets frameworks ([TFM](/dotnet/standard/frameworks)) in your project file, then use `dotnet pack` or `msbuild /t:pack` to create the package.</span></span>

> [!NOTE]
> <span data-ttu-id="6847c-109">nuget.exe CLI nepodporuje balení projektů ve stylu sady SDK, takže byste měli používat `dotnet pack` pouze nebo `msbuild /t:pack`.</span><span class="sxs-lookup"><span data-stu-id="6847c-109">nuget.exe CLI does not support packing SDK-style projects, so you should only use `dotnet pack` or `msbuild /t:pack`.</span></span> <span data-ttu-id="6847c-110">Doporučujeme [zahrnout všechny vlastnosti,](../reference/msbuild-targets.md#pack-target) které `.nuspec` jsou obvykle v souboru v souboru projektu místo.</span><span class="sxs-lookup"><span data-stu-id="6847c-110">We recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="6847c-111">Chcete-li cílit na více verzí rozhraní .NET Framework v projektu, který není ve stylu sady SDK, naleznete v [tématu Podpora více verzí rozhraní .NET Framework](supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="6847c-111">To target multiple .NET Framework versions in a non-SDK-style project, see [Supporting multiple .NET Framework versions](supporting-multiple-target-frameworks.md).</span></span>

## <a name="create-a-project-that-supports-multiple-net-framework-versions"></a><span data-ttu-id="6847c-112">Vytvoření projektu, který podporuje více verzí rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="6847c-112">Create a project that supports multiple .NET Framework versions</span></span>

1. <span data-ttu-id="6847c-113">Vytvořte novou knihovnu tříd .NET Standard `dotnet new classlib`v sadě Visual Studio nebo použijte .</span><span class="sxs-lookup"><span data-stu-id="6847c-113">Create a new .NET Standard class library either in Visual Studio or use `dotnet new classlib`.</span></span>

   <span data-ttu-id="6847c-114">Doporučujeme vytvořit knihovnu tříd .NET Standard pro nejlepší kompatibilitu.</span><span class="sxs-lookup"><span data-stu-id="6847c-114">We recommend that you create a .NET Standard class library for best compatibility.</span></span>

2. <span data-ttu-id="6847c-115">Upravte soubor *.csproj* pro podporu cílových architektur.</span><span class="sxs-lookup"><span data-stu-id="6847c-115">Edit the *.csproj* file to support the target frameworks.</span></span> <span data-ttu-id="6847c-116">Například změna</span><span class="sxs-lookup"><span data-stu-id="6847c-116">For example, change</span></span>
   
   `<TargetFramework>netstandard2.0</TargetFramework>`
   
   <span data-ttu-id="6847c-117">na:</span><span class="sxs-lookup"><span data-stu-id="6847c-117">to:</span></span>
   
   `<TargetFrameworks>netstandard2.0;net45</TargetFrameworks>`

   <span data-ttu-id="6847c-118">Ujistěte se, že změníte element XML změněný z jednotného čísla na množné číslo (přidejte "s" do otevřených i blízkých značek).</span><span class="sxs-lookup"><span data-stu-id="6847c-118">Make sure that you change the XML element changed from singular to plural (add the "s" to both the open and close tags).</span></span>

3. <span data-ttu-id="6847c-119">Pokud máte jakýkoli kód, který funguje pouze v `#if NET45` `#if NETSTANDARD2_0` jednom TFM, můžete použít nebo oddělit kód závislý na TFM.</span><span class="sxs-lookup"><span data-stu-id="6847c-119">If you have any code that only works in one TFM, you can use `#if NET45` or `#if NETSTANDARD2_0` to separate TFM-dependent code.</span></span> <span data-ttu-id="6847c-120">(Další informace naleznete v tématu [How to multitarget](/dotnet/core/tutorials/libraries#how-to-multitarget).) Můžete například použít následující kód:</span><span class="sxs-lookup"><span data-stu-id="6847c-120">(For more information, see [How to multitarget](/dotnet/core/tutorials/libraries#how-to-multitarget).) For example, you can use the following code:</span></span>

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

4. <span data-ttu-id="6847c-121">Přidejte všechna metadata NuGet, která chcete, do *vlastností .csproj* jako MSBuild.</span><span class="sxs-lookup"><span data-stu-id="6847c-121">Add any NuGet metadata you want to the *.csproj* as MSBuild properties.</span></span>

   <span data-ttu-id="6847c-122">Seznam dostupných metadat balíčku a názvy vlastností MSBuild naleznete v tématu [pack target](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="6847c-122">For the list of available package metadata and the MSBuild property names, see [pack target](../reference/msbuild-targets.md#pack-target).</span></span> <span data-ttu-id="6847c-123">Viz Také [zobrazení Řízení prostředků závislostí](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="6847c-123">Also see [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

   <span data-ttu-id="6847c-124">Pokud chcete oddělit vlastnosti související se sestavením od metadat `PropertyGroup`NuGet, můžete použít jinou vlastnosti nebo umístit `Import` vlastnosti NuGet do jiného souboru a použít direktivu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="6847c-124">If you want to separate build-related properties from NuGet metadata, you can use a different `PropertyGroup`, or put the NuGet properties in another file and use MSBuild's `Import` directive to include it.</span></span> <span data-ttu-id="6847c-125">`Directory.Build.Props`a `Directory.Build.Targets` jsou také podporovány počínaje MSBuild 15.0.</span><span class="sxs-lookup"><span data-stu-id="6847c-125">`Directory.Build.Props` and `Directory.Build.Targets` are also supported starting with MSBuild 15.0.</span></span>

5. <span data-ttu-id="6847c-126">Nyní použití `dotnet pack` a výsledné *.nupkg* cíle .NET Standard 2.0 a .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="6847c-126">Now, use `dotnet pack` and the resulting *.nupkg* targets both .NET Standard 2.0 and .NET Framework 4.5.</span></span>

<span data-ttu-id="6847c-127">Zde je soubor *.csproj,* který je generován pomocí předchozích kroků a .NET Core SDK 2.2.</span><span class="sxs-lookup"><span data-stu-id="6847c-127">Here is the *.csproj* file that is generated using the preceding steps and .NET Core SDK 2.2.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFrameworks>netstandard2.0;net45</TargetFrameworks>
    <Description>Sample project that targets multiple TFMs</Description>
  </PropertyGroup>

</Project>
```

## <a name="see-also"></a><span data-ttu-id="6847c-128">Viz také</span><span class="sxs-lookup"><span data-stu-id="6847c-128">See also</span></span>

* [<span data-ttu-id="6847c-129">Jak určit cílové rámce</span><span class="sxs-lookup"><span data-stu-id="6847c-129">How to specify target frameworks</span></span>](/dotnet/standard/frameworks#how-to-specify-target-frameworks)
* [<span data-ttu-id="6847c-130">Cílení na více platforem</span><span class="sxs-lookup"><span data-stu-id="6847c-130">Cross-platform targeting</span></span>](/dotnet/standard/library-guidance/cross-platform-targeting)
