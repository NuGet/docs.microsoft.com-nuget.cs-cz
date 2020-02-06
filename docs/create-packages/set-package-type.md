---
title: Nastavení typu balíčku NuGet
description: Popisuje typy balíčků k označení zamýšleného použití balíčku.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 22e8ac2e9e2086a1280c5b0c3be8a032b7998b36
ms.sourcegitcommit: 415c70d7014545c1f65271a2debf8c3c1c5eb688
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/06/2020
ms.locfileid: "77036913"
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
    <package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetTool" />
        </packageTypes>
        </metadata>
    </package>
    ```
