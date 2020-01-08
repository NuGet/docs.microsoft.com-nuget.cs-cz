---
title: Vytváření balíčků pomocí sestavení zprostředkovatele komunikace s objekty COM
description: Popisuje, jak vytvořit balíčky obsahující sestavení Interop modelu COM.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: de164b136a1636b89f674b8626613094fc53e04c
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/25/2019
ms.locfileid: "75385569"
---
# <a name="create-nuget-packages-that-contain-com-interop-assemblies"></a><span data-ttu-id="31d37-103">Vytváření balíčků NuGet obsahujících sestavení Interop modelu COM</span><span class="sxs-lookup"><span data-stu-id="31d37-103">Create NuGet packages that contain COM interop assemblies</span></span>

<span data-ttu-id="31d37-104">Balíčky obsahující sestavení zprostředkovatele komunikace s objekty COM musí obsahovat [soubor](creating-a-package.md#include-msbuild-props-and-targets-in-a-package) s odpovídajícími cíli, aby byly do projektů přidány správné metadata `EmbedInteropTypes` pomocí formátu PackageReference.</span><span class="sxs-lookup"><span data-stu-id="31d37-104">Packages that contain COM interop assemblies must include an appropriate [targets file](creating-a-package.md#include-msbuild-props-and-targets-in-a-package) so that the correct `EmbedInteropTypes` metadata is added to projects using the PackageReference format.</span></span> <span data-ttu-id="31d37-105">Ve výchozím nastavení jsou metadata `EmbedInteropTypes` vždy false pro všechna sestavení při použití PackageReference, takže soubor targets tato metadata přidá explicitně.</span><span class="sxs-lookup"><span data-stu-id="31d37-105">By default, the `EmbedInteropTypes` metadata is always false for all assemblies when PackageReference is used, so the targets file adds this metadata explicitly.</span></span> <span data-ttu-id="31d37-106">Aby nedocházelo ke konfliktům, cílový název by měl být jedinečný; v ideálním případě použijte kombinaci názvu balíčku a sestavení, které je vloženo, a nahraďte `{InteropAssemblyName}` v níže uvedeném příkladu s touto hodnotou.</span><span class="sxs-lookup"><span data-stu-id="31d37-106">To avoid conflicts, the target name should be unique; ideally, use a combination of your package name and the assembly being embedded, replacing the `{InteropAssemblyName}` in the example below with that value.</span></span> <span data-ttu-id="31d37-107">(Příklad najdete v tématu [NuGet. Samples. Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) .)</span><span class="sxs-lookup"><span data-stu-id="31d37-107">(Also see [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) for an example.)</span></span>

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

<span data-ttu-id="31d37-108">Všimněte si, že při použití formátu správy `packages.config`, přidání odkazů na sestavení z balíčků způsobí, že nástroj NuGet a sada Visual Studio zkontrolují sestavení zprostředkovatele komunikace s objekty COM a nastaví `EmbedInteropTypes` na hodnotu true v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="31d37-108">Note that when using the `packages.config` management format, adding references to the assemblies from the packages causes NuGet and Visual Studio to check for COM interop assemblies and set the `EmbedInteropTypes` to true in the project file.</span></span> <span data-ttu-id="31d37-109">V tomto případě jsou cíle přepsány.</span><span class="sxs-lookup"><span data-stu-id="31d37-109">In this case, the targets are overridden.</span></span>

<span data-ttu-id="31d37-110">Kromě toho se ve výchozím nastavení [prostředky sestavení neflowují](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="31d37-110">Additionally, by default the [build assets do not flow transitively](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span> <span data-ttu-id="31d37-111">Balíčky vytvořené tak, jak je zde popsáno, fungují jinak, když jsou získány jako přenositelné závislosti z projektu na odkaz na projekt.</span><span class="sxs-lookup"><span data-stu-id="31d37-111">Packages authored as described here work differently when they are pulled as a transitive dependency from a project to project reference.</span></span> <span data-ttu-id="31d37-112">Příjemce balíčku může těmto uživatelům poskytnout tok úpravou výchozí hodnoty PrivateAssets, která nezahrnuje Build.</span><span class="sxs-lookup"><span data-stu-id="31d37-112">The package consumer can allow them to flow by modifying the PrivateAssets default value to not include build.</span></span>

<a name="creating-the-package"></a>