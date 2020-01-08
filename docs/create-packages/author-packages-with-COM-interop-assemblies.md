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
# <a name="create-nuget-packages-that-contain-com-interop-assemblies"></a>Vytváření balíčků NuGet obsahujících sestavení Interop modelu COM

Balíčky obsahující sestavení zprostředkovatele komunikace s objekty COM musí obsahovat [soubor](creating-a-package.md#include-msbuild-props-and-targets-in-a-package) s odpovídajícími cíli, aby byly do projektů přidány správné metadata `EmbedInteropTypes` pomocí formátu PackageReference. Ve výchozím nastavení jsou metadata `EmbedInteropTypes` vždy false pro všechna sestavení při použití PackageReference, takže soubor targets tato metadata přidá explicitně. Aby nedocházelo ke konfliktům, cílový název by měl být jedinečný; v ideálním případě použijte kombinaci názvu balíčku a sestavení, které je vloženo, a nahraďte `{InteropAssemblyName}` v níže uvedeném příkladu s touto hodnotou. (Příklad najdete v tématu [NuGet. Samples. Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) .)

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

Všimněte si, že při použití formátu správy `packages.config`, přidání odkazů na sestavení z balíčků způsobí, že nástroj NuGet a sada Visual Studio zkontrolují sestavení zprostředkovatele komunikace s objekty COM a nastaví `EmbedInteropTypes` na hodnotu true v souboru projektu. V tomto případě jsou cíle přepsány.

Kromě toho se ve výchozím nastavení [prostředky sestavení neflowují](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets). Balíčky vytvořené tak, jak je zde popsáno, fungují jinak, když jsou získány jako přenositelné závislosti z projektu na odkaz na projekt. Příjemce balíčku může těmto uživatelům poskytnout tok úpravou výchozí hodnoty PrivateAssets, která nezahrnuje Build.

<a name="creating-the-package"></a>