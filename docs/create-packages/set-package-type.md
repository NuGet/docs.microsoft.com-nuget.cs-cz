---
title: Nastavení typu balíčku NuGet
description: Popisuje typy balíčků k označení zamýšleného použití balíčku.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 1d869f616ce0291cf1c0a17b7ff20fc61e6a3bd5
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230821"
---
# <a name="set-a-nuget-package-type"></a>Nastavení typu balíčku NuGet

S NuGet 3.5 + můžete balíčky označit pomocí konkrétního *typu balíčku* , aby označovali zamýšlené použití. Balíčky, které nejsou označeny typem, včetně všech balíčků vytvořených v dřívějších verzích NuGet, jsou ve výchozím nastavení typu `Dependency`.

- balíčky typů `Dependency` přidávají do knihoven a aplikací prostředky run-time a můžou být nainstalované v jakémkoli typu projektu (za předpokladu, že jsou kompatibilní).

- balíčky typů `DotnetTool` jsou rozšířením rozhraní příkazového řádku [dotnet](/dotnet/articles/core/tools/index) a jsou vyvolána z příkazového řádku. Takové balíčky lze nainstalovat pouze v projektech .NET Core a nemají žádný vliv na operace obnovení. Další podrobnosti o těchto rozšířeních pro jednotlivé projekty jsou k dispozici v dokumentaci [rozšiřitelnosti .NET Core](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) .

- balíčky typů `Template` poskytují [vlastní šablony](/dotnet/core/tools/custom-templates) , které lze použít k vytvoření souborů nebo projektů, jako je aplikace, služby, nástroje nebo knihovna tříd.

- Balíčky vlastních typů používají libovolný identifikátor typu, který odpovídá stejným pravidlům formátu jako ID balíčků. Správce balíčků NuGet v aplikaci Visual Studio však nerozpoznal jiný typ než `Dependency` a `DotnetTool`.

Typy balíčků jsou nastaveny v souboru `.nuspec`. Je nejvhodnější pro zpětnou *kompatibilitu, aby neexplicitně* nastavila typ `Dependency` a místo toho se spoléhá na NuGet za předpokladu, že není zadán žádný typ.

- `.nuspec`: Určete typ balíčku v rámci uzlu `packageTypes\packageType` pod prvkem `<metadata>`:

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
