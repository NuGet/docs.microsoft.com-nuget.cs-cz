---
title: Vytváření balíčků pomocí sestavení zprostředkovatele komunikace s objekty COM
description: Popisuje, jak vytvořit balíčky obsahující sestavení Interop modelu COM.
author: JonDouglas
ms.author: jodou
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: b12672e81a974e113ffbda80560c9d3eede9c69d
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859119"
---
# <a name="create-nuget-packages-that-contain-com-interop-assemblies"></a><span data-ttu-id="c65aa-103">Vytváření balíčků NuGet obsahujících sestavení Interop modelu COM</span><span class="sxs-lookup"><span data-stu-id="c65aa-103">Create NuGet packages that contain COM interop assemblies</span></span>

<span data-ttu-id="c65aa-104">Balíčky obsahující sestavení zprostředkovatele komunikace s objekty COM musí obsahovat [soubor](creating-a-package.md#include-msbuild-props-and-targets-in-a-package) s odpovídajícími cíli, aby se `EmbedInteropTypes` do projektů přidala správná metadata pomocí formátu PackageReference.</span><span class="sxs-lookup"><span data-stu-id="c65aa-104">Packages that contain COM interop assemblies must include an appropriate [targets file](creating-a-package.md#include-msbuild-props-and-targets-in-a-package) so that the correct `EmbedInteropTypes` metadata is added to projects using the PackageReference format.</span></span> <span data-ttu-id="c65aa-105">Ve výchozím nastavení `EmbedInteropTypes` jsou metadata vždy false pro všechna sestavení při použití PackageReference, takže soubor targets tato metadata přidá explicitně.</span><span class="sxs-lookup"><span data-stu-id="c65aa-105">By default, the `EmbedInteropTypes` metadata is always false for all assemblies when PackageReference is used, so the targets file adds this metadata explicitly.</span></span> <span data-ttu-id="c65aa-106">Aby nedocházelo ke konfliktům, cílový název by měl být jedinečný; v ideálním případě použijte kombinaci názvu balíčku a sestavení, které je vloženo, a nahraďte `{InteropAssemblyName}` v příkladu níže tuto hodnotu.</span><span class="sxs-lookup"><span data-stu-id="c65aa-106">To avoid conflicts, the target name should be unique; ideally, use a combination of your package name and the assembly being embedded, replacing the `{InteropAssemblyName}` in the example below with that value.</span></span> <span data-ttu-id="c65aa-107">(Příklad najdete v tématu [NuGet. Samples. Interop](https://github.com/NuGet/Samples/tree/main/NuGet.Samples.Interop) .)</span><span class="sxs-lookup"><span data-stu-id="c65aa-107">(Also see [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/main/NuGet.Samples.Interop) for an example.)</span></span>

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

<span data-ttu-id="c65aa-108">Všimněte si, že při použití `packages.config` formátu správy, přidání odkazů na sestavení z balíčků způsobí, že nástroj NuGet a sada Visual Studio zkontrolují sestavení zprostředkovatele komunikace s objekty COM a nastaví na `EmbedInteropTypes` hodnotu true v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="c65aa-108">Note that when using the `packages.config` management format, adding references to the assemblies from the packages causes NuGet and Visual Studio to check for COM interop assemblies and set the `EmbedInteropTypes` to true in the project file.</span></span> <span data-ttu-id="c65aa-109">V tomto případě jsou cíle přepsány.</span><span class="sxs-lookup"><span data-stu-id="c65aa-109">In this case, the targets are overridden.</span></span>

<span data-ttu-id="c65aa-110">Kromě toho se ve výchozím nastavení [prostředky sestavení neflowují](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="c65aa-110">Additionally, by default the [build assets do not flow transitively](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span> <span data-ttu-id="c65aa-111">Balíčky vytvořené tak, jak je zde popsáno, fungují jinak, když jsou získány jako přenositelné závislosti z projektu na odkaz na projekt.</span><span class="sxs-lookup"><span data-stu-id="c65aa-111">Packages authored as described here work differently when they are pulled as a transitive dependency from a project to project reference.</span></span> <span data-ttu-id="c65aa-112">Příjemce balíčku může těmto uživatelům poskytnout tok úpravou výchozí hodnoty PrivateAssets, která nezahrnuje Build.</span><span class="sxs-lookup"><span data-stu-id="c65aa-112">The package consumer can allow them to flow by modifying the PrivateAssets default value to not include build.</span></span>

<a name="creating-the-package"></a>