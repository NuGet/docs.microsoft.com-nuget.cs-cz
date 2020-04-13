---
title: Nastavení typu balíčku NuGet
description: Popisuje typy balíčků označující zamýšlené použití balíčku.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 1d869f616ce0291cf1c0a17b7ff20fc61e6a3bd5
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "78230821"
---
# <a name="set-a-nuget-package-type"></a>Nastavení typu balíčku NuGet

S NuGet 3.5+, balíčky mohou být označeny určitým *typem balíčku* k označení jeho zamýšlené použití. Balíčky, které nejsou označeny typem, včetně všech balíčků vytvořených s dřívějšími verzemi NuGet, výchozí `Dependency` typ.

- `Dependency`typy balíčků přidat sestavení nebo run-time datové zdroje do knihoven a aplikací a lze nainstalovat v libovolném typu projektu (za předpokladu, že jsou kompatibilní).

- `DotnetTool`typy balíčků jsou rozšíření [dotnet CLI](/dotnet/articles/core/tools/index) a jsou vyvolány z příkazového řádku. Tyto balíčky lze nainstalovat pouze v projektech .NET Core a nemají žádný vliv na operace obnovení. Další podrobnosti o těchto rozšíření chod projektu jsou k dispozici v dokumentaci [rozšiřitelnosti jádra .NET.](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility)

- `Template`balíčky typů poskytují [vlastní šablony,](/dotnet/core/tools/custom-templates) které lze použít k vytvoření souborů nebo projektů, jako je aplikace, služba, nástroj nebo knihovna tříd.

- Balíčky vlastních typů používají libovolný identifikátor typu, který odpovídá stejným pravidlům formátu jako ID balíčků. Všechny typy `Dependency` než `DotnetTool`a , však nejsou rozpoznány NuGet Package Manager v sadě Visual Studio.

Typy balíčků jsou `.nuspec` nastaveny v souboru. Je nejvhodnější pro zpětnou *not* kompatibilitu není `Dependency` explicitně nastavit typ a místo toho spoléhat na NuGet za předpokladu, že tento typ, když není zadán žádný typ.

- `.nuspec`: Označte typ `packageTypes\packageType` balíčku v `<metadata>` uzlu pod elementem:

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetTool" />
        </packageTypes>
        </metadata>
    </package>
    ```
