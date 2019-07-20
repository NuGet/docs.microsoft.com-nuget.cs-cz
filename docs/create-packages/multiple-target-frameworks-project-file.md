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
# <a name="support-multiple-net-framework-versions-in-your-project-file"></a>Podpora více verzí .NET Framework v souboru projektu

Při prvním vytvoření projektu doporučujeme vytvořit knihovnu tříd .NET Standard, protože poskytuje kompatibilitu s nejširší škálou náročných projektů. Pomocí .NET Standard přidáte do knihovny .NET standardně [podporu více platforem](/dotnet/standard/library-guidance/cross-platform-targeting) . V některých scénářích však může být také nutné zahrnout kód, který cílí na konkrétní rozhraní. V tomto článku se dozvíte, jak to udělat pro projekty ve [stylu sady SDK](../resources/check-project-format.md) .

Pro projekty ve stylu sady SDK můžete v souboru projektu nakonfigurovat podporu pro více cílů architektury ([TFM](/dotnet/standard/frameworks)) a potom pomocí `dotnet pack` nebo `msbuild /t:pack` vytvořit balíček.

> [!NOTE]
> NuGet. exe CLI nepodporuje projekty ve stylu balíčku sady SDK, takže byste měli použít `dotnet pack` jenom nebo. `msbuild /t:pack` Doporučujeme, abyste místo toho [zahrnuli všechny vlastnosti](../reference/msbuild-targets.md#pack-target) , které jsou obvykle `.nuspec` v souboru v souboru projektu. Chcete-li cílit na více .NET Framework verzí v projektu ve stylu mimo sadu SDK, přečtěte si téma [Podpora více verzí .NET Framework](supporting-multiple-target-frameworks.md).

## <a name="create-a-project-that-supports-multiple-net-framework-versions"></a>Vytvořit projekt, který podporuje více verzí .NET Framework

1. Vytvořte novou knihovnu tříd .NET Standard v aplikaci Visual Studio nebo ji použijte `dotnet new classlib`.

   Pro zajištění nejlepší kompatibility doporučujeme vytvořit knihovnu tříd .NET Standard.

2. Upravte soubor *. csproj* pro podporu cílových rozhraní.

   Například změňte `<TargetFramework>netstandard2.0</TargetFramework>` na `<TargetFrameworks>netstandard2.0;net45</TargetFrameworks>`.

   Ujistěte se, že změníte element XML změněn z čísla v množném čísle na plural (přidejte "s" do počátečních a uzavíracích značek).

3. Pokud máte nějaký kód, který funguje pouze v jednom TFM, můžete použít `#if NET45` nebo `#if NETSTANDARD20` k oddělení kódu závislého na TFM. (Další informace najdete v tématu [jak cílit na více cílů](/dotnet/core/tutorials/libraries#how-to-multitarget).) Například můžete použít následující kód:

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

4. Přidejte jakákoli metadata NuGet, která chcete, do vlastností *. csproj* jako vlastnosti MSBuild.

   Seznam dostupných metadat balíčku a názvů vlastností MSBuild naleznete v tématu [targeting pack](../reference/msbuild-targets.md#pack-target). Viz také [řízení prostředků závislosti](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).

   Pokud chcete oddělit vlastnosti týkající se sestavení z metadat NuGet, můžete použít jinou `PropertyGroup`vlastnost nebo umístit vlastnosti NuGet do jiného souboru a použít `Import` direktivu MSBuild k jejímu zahrnutí. `Directory.Build.Props`a `Directory.Build.Targets` jsou podporované i od MSBuild 15,0.

5. Nyní použijte `dotnet pack` a výsledný *nupkg* cílí na .NET Standard 2,0 i .NET Framework 4,5.

Zde je soubor *. csproj* , který je generován pomocí předchozích kroků a .NET Core SDK 2,2.

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFrameworks>netstandard2.0;net45</TargetFrameworks>
    <Description>Sample project that targets multiple TFMs</Description>
  </PropertyGroup>

</Project>
```

## <a name="see-also"></a>Viz také:

[Určení cílových rozhraní](/dotnet/standard/frameworks#how-to-specify-target-frameworks)
cílících na[více platforem](/dotnet/standard/library-guidance/cross-platform-targeting)
