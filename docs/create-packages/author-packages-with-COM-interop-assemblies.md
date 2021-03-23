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
# <a name="create-nuget-packages-that-contain-com-interop-assemblies"></a>Vytváření balíčků NuGet obsahujících sestavení Interop modelu COM

Balíčky obsahující sestavení zprostředkovatele komunikace s objekty COM musí obsahovat [soubor](creating-a-package.md#include-msbuild-props-and-targets-in-a-package) s odpovídajícími cíli, aby se `EmbedInteropTypes` do projektů přidala správná metadata pomocí formátu PackageReference. Ve výchozím nastavení `EmbedInteropTypes` jsou metadata vždy false pro všechna sestavení při použití PackageReference, takže soubor targets tato metadata přidá explicitně. Aby nedocházelo ke konfliktům, cílový název by měl být jedinečný; v ideálním případě použijte kombinaci názvu balíčku a sestavení, které je vloženo, a nahraďte `{InteropAssemblyName}` v příkladu níže tuto hodnotu. (Příklad najdete v tématu [NuGet. Samples. Interop](https://github.com/NuGet/Samples/tree/main/NuGet.Samples.Interop) .)

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

Všimněte si, že při použití `packages.config` formátu správy, přidání odkazů na sestavení z balíčků způsobí, že nástroj NuGet a sada Visual Studio zkontrolují sestavení zprostředkovatele komunikace s objekty COM a nastaví na `EmbedInteropTypes` hodnotu true v souboru projektu. V tomto případě jsou cíle přepsány.

Kromě toho se ve výchozím nastavení [prostředky sestavení neflowují](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets). Balíčky vytvořené tak, jak je zde popsáno, fungují jinak, když jsou získány jako přenositelné závislosti z projektu na odkaz na projekt. Příjemce balíčku může těmto uživatelům poskytnout tok úpravou výchozí hodnoty PrivateAssets, která nezahrnuje Build.

<a name="creating-the-package"></a>