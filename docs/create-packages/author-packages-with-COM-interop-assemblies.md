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
# <a name="create-nuget-packages-that-contain-com-interop-assemblies"></a>Vytvořit balíčky NuGet, které obsahují meziop sestavení COM

Balíčky, které obsahují meziop sestavení com musí obsahovat odpovídající [cíle soubor](creating-a-package.md#include-msbuild-props-and-targets-in-a-package) tak, aby správná `EmbedInteropTypes` metadata je přidán do projektů pomocí formátu PackageReference. Ve výchozím `EmbedInteropTypes` nastavení metadata je vždy false pro všechna sestavení při PackageReference se používá, takže soubor cílů přidá tato metadata explicitně. Chcete-li se vyhnout konfliktům, cílový název by měl být jedinečný; v ideálním případě použijte kombinaci názvu balíčku a sestavení, `{InteropAssemblyName}` které je vloženo, a nahradí v níže uvedeném příkladu tuto hodnotu. (Viz také [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) pro příklad.)

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

Všimněte si, `packages.config` že při použití formátu pro správu, přidání odkazů na sestavení z balíčků způsobí NuGet a Visual Studio ke kontrole sestavení mezi opop COM a nastavit `EmbedInteropTypes` na true v souboru projektu. V tomto případě jsou cíle přepsány.

Navíc ve výchozím nastavení [sestavení prostředky netokují přechodně](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets). Balíčky vytvořené tak, jak je zde popsáno, fungují jinak, když jsou vytaženy jako přenositá závislost z projektu na odkaz na projekt. Příjemce balíčku může povolit jejich tok úpravou privateAssets výchozí hodnotu nezahrnuje sestavení.

<a name="creating-the-package"></a>