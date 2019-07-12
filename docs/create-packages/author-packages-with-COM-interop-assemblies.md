---
title: Vytváření balíčků s sestavení vzájemné spolupráce COM
description: Popisuje, jak vytvořit balíčky, které obsahují sestavení vzájemné spolupráce COM
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: d0e368f43171ce71abc60b3e09d08b010d2d8880
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/12/2019
ms.locfileid: "67843530"
---
## <a name="create-nuget-packages-that-contain-com-interop-assemblies"></a>Vytvořit balíčky NuGet, které obsahují sestavení vzájemné spolupráce COM

Balíčky, které obsahují sestavení vzájemné spolupráce COM musí obsahovat odpovídající [soubor cílů](creating-a-package.md#include-msbuild-props-and-targets-in-a-package) tak, aby správné `EmbedInteropTypes` do projektů s použitím formátu PackageReference se přidají metadata. Ve výchozím nastavení `EmbedInteropTypes` metadat má vždy hodnotu false pro všechna sestavení zadáním PackageReference tak soubor cílů přidá tato metadata explicitně. Aby nedocházelo ke konfliktům, cílový název by měl být jedinečný; v ideálním případě by použít kombinaci váš název balíčku a sestavení jsou vložené a nahraďte `{InteropAssemblyName}` v níže uvedeném příkladu s danou hodnotou. (Viz také [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) příklad.)

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

Všimněte si, že při použití `packages.config` formátu správy přidávání odkazů na sestavení z balíčků způsobí, že NuGet a sady Visual Studio vyhledat sestavení vzájemné spolupráce COM a nastavit `EmbedInteropTypes` na hodnotu true v souboru projektu. V tomto případě cíle, které jsou přepsaný.

Kromě toho ve výchozím nastavení [tok prostředky sestavení není přechodně](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets). Balíčky vytvořené podle postupu popsaného tady pracovní odlišně při se berou jako přechodné závislosti z odkazu typu projekt na projekt. Příjemce balíčku můžete zajistí, aby tok tak, že upravíte výchozí hodnotu PrivateAssets tak, aby nezahrnovala sestavení.

<a name="creating-the-package"></a>