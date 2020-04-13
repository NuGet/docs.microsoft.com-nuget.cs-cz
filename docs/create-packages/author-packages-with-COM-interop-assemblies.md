---
title: Vytváření balíčků pomocí meziop sestavení COM
description: Popisuje, jak vytvořit balíčky, které obsahují sestavení interop com
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: de164b136a1636b89f674b8626613094fc53e04c
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "75385569"
---
# <a name="create-nuget-packages-that-contain-com-interop-assemblies"></a><span data-ttu-id="b08de-103">Vytvořit balíčky NuGet, které obsahují meziop sestavení COM</span><span class="sxs-lookup"><span data-stu-id="b08de-103">Create NuGet packages that contain COM interop assemblies</span></span>

<span data-ttu-id="b08de-104">Balíčky, které obsahují meziop sestavení com musí obsahovat odpovídající [cíle soubor](creating-a-package.md#include-msbuild-props-and-targets-in-a-package) tak, aby správná `EmbedInteropTypes` metadata je přidán do projektů pomocí formátu PackageReference.</span><span class="sxs-lookup"><span data-stu-id="b08de-104">Packages that contain COM interop assemblies must include an appropriate [targets file](creating-a-package.md#include-msbuild-props-and-targets-in-a-package) so that the correct `EmbedInteropTypes` metadata is added to projects using the PackageReference format.</span></span> <span data-ttu-id="b08de-105">Ve výchozím `EmbedInteropTypes` nastavení metadata je vždy false pro všechna sestavení při PackageReference se používá, takže soubor cílů přidá tato metadata explicitně.</span><span class="sxs-lookup"><span data-stu-id="b08de-105">By default, the `EmbedInteropTypes` metadata is always false for all assemblies when PackageReference is used, so the targets file adds this metadata explicitly.</span></span> <span data-ttu-id="b08de-106">Chcete-li se vyhnout konfliktům, cílový název by měl být jedinečný; v ideálním případě použijte kombinaci názvu balíčku a sestavení, `{InteropAssemblyName}` které je vloženo, a nahradí v níže uvedeném příkladu tuto hodnotu.</span><span class="sxs-lookup"><span data-stu-id="b08de-106">To avoid conflicts, the target name should be unique; ideally, use a combination of your package name and the assembly being embedded, replacing the `{InteropAssemblyName}` in the example below with that value.</span></span> <span data-ttu-id="b08de-107">(Viz také [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) pro příklad.)</span><span class="sxs-lookup"><span data-stu-id="b08de-107">(Also see [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) for an example.)</span></span>

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

<span data-ttu-id="b08de-108">Všimněte si, `packages.config` že při použití formátu pro správu, přidání odkazů na sestavení z balíčků způsobí NuGet a Visual Studio ke kontrole sestavení mezi opop COM a nastavit `EmbedInteropTypes` na true v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="b08de-108">Note that when using the `packages.config` management format, adding references to the assemblies from the packages causes NuGet and Visual Studio to check for COM interop assemblies and set the `EmbedInteropTypes` to true in the project file.</span></span> <span data-ttu-id="b08de-109">V tomto případě jsou cíle přepsány.</span><span class="sxs-lookup"><span data-stu-id="b08de-109">In this case, the targets are overridden.</span></span>

<span data-ttu-id="b08de-110">Navíc ve výchozím nastavení [sestavení prostředky netokují přechodně](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="b08de-110">Additionally, by default the [build assets do not flow transitively](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span> <span data-ttu-id="b08de-111">Balíčky vytvořené tak, jak je zde popsáno, fungují jinak, když jsou vytaženy jako přenositá závislost z projektu na odkaz na projekt.</span><span class="sxs-lookup"><span data-stu-id="b08de-111">Packages authored as described here work differently when they are pulled as a transitive dependency from a project to project reference.</span></span> <span data-ttu-id="b08de-112">Příjemce balíčku může povolit jejich tok úpravou privateAssets výchozí hodnotu nezahrnuje sestavení.</span><span class="sxs-lookup"><span data-stu-id="b08de-112">The package consumer can allow them to flow by modifying the PrivateAssets default value to not include build.</span></span>

<a name="creating-the-package"></a>