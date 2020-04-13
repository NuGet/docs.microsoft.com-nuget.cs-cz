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
# <a name="support-multiple-net-framework-versions-in-your-project-file"></a>Podpora více verzí rozhraní .NET Framework v souboru projektu

Při prvním vytvoření projektu doporučujeme vytvořit knihovnu tříd .NET Standard, protože poskytuje kompatibilitu s nejširší škálou náročných projektů. Pomocí standardu .NET Standard přidáte ve výchozím nastavení [podporu pro více platforem](/dotnet/standard/library-guidance/cross-platform-targeting) do knihovny .NET. V některých případech však může být také nutné zahrnout kód, který se zaměřuje na konkrétní rámec. Tento článek ukazuje, jak to udělat pro projekty [ve stylu sady SDK.](../resources/check-project-format.md)

Pro projekty ve stylu sady SDK můžete nakonfigurovat podporu pro více cílů `dotnet pack` rozhraní `msbuild /t:pack` [(TFM)](/dotnet/standard/frameworks)v souboru projektu, pak použít nebo vytvořit balíček.

> [!NOTE]
> nuget.exe CLI nepodporuje balení projektů ve stylu sady SDK, takže byste měli používat `dotnet pack` pouze nebo `msbuild /t:pack`. Doporučujeme [zahrnout všechny vlastnosti,](../reference/msbuild-targets.md#pack-target) které `.nuspec` jsou obvykle v souboru v souboru projektu místo. Chcete-li cílit na více verzí rozhraní .NET Framework v projektu, který není ve stylu sady SDK, naleznete v [tématu Podpora více verzí rozhraní .NET Framework](supporting-multiple-target-frameworks.md).

## <a name="create-a-project-that-supports-multiple-net-framework-versions"></a>Vytvoření projektu, který podporuje více verzí rozhraní .NET Framework

1. Vytvořte novou knihovnu tříd .NET Standard `dotnet new classlib`v sadě Visual Studio nebo použijte .

   Doporučujeme vytvořit knihovnu tříd .NET Standard pro nejlepší kompatibilitu.

2. Upravte soubor *.csproj* pro podporu cílových architektur. Například změna
   
   `<TargetFramework>netstandard2.0</TargetFramework>`
   
   na:
   
   `<TargetFrameworks>netstandard2.0;net45</TargetFrameworks>`

   Ujistěte se, že změníte element XML změněný z jednotného čísla na množné číslo (přidejte "s" do otevřených i blízkých značek).

3. Pokud máte jakýkoli kód, který funguje pouze v `#if NET45` `#if NETSTANDARD2_0` jednom TFM, můžete použít nebo oddělit kód závislý na TFM. (Další informace naleznete v tématu [How to multitarget](/dotnet/core/tutorials/libraries#how-to-multitarget).) Můžete například použít následující kód:

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

4. Přidejte všechna metadata NuGet, která chcete, do *vlastností .csproj* jako MSBuild.

   Seznam dostupných metadat balíčku a názvy vlastností MSBuild naleznete v tématu [pack target](../reference/msbuild-targets.md#pack-target). Viz Také [zobrazení Řízení prostředků závislostí](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).

   Pokud chcete oddělit vlastnosti související se sestavením od metadat `PropertyGroup`NuGet, můžete použít jinou vlastnosti nebo umístit `Import` vlastnosti NuGet do jiného souboru a použít direktivu MSBuild. `Directory.Build.Props`a `Directory.Build.Targets` jsou také podporovány počínaje MSBuild 15.0.

5. Nyní použití `dotnet pack` a výsledné *.nupkg* cíle .NET Standard 2.0 a .NET Framework 4.5.

Zde je soubor *.csproj,* který je generován pomocí předchozích kroků a .NET Core SDK 2.2.

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFrameworks>netstandard2.0;net45</TargetFrameworks>
    <Description>Sample project that targets multiple TFMs</Description>
  </PropertyGroup>

</Project>
```

## <a name="see-also"></a>Viz také

* [Jak určit cílové rámce](/dotnet/standard/frameworks#how-to-specify-target-frameworks)
* [Cílení na více platforem](/dotnet/standard/library-guidance/cross-platform-targeting)
