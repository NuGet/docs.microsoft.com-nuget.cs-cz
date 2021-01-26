---
title: Nastavení typu balíčku NuGet
description: Popisuje typy balíčků k označení zamýšleného použití balíčku.
author: JonDouglas
ms.author: jodou
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 990ac580f4031615566d78e359a24eaedaaf3e07
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774368"
---
# <a name="set-a-nuget-package-type"></a>Nastavení typu balíčku NuGet

S NuGet 3.5 + můžete balíčky označit pomocí konkrétního *typu balíčku* , aby označovali zamýšlené použití. Balíčky, které nejsou označeny typem, včetně všech balíčků vytvořených v dřívějších verzích NuGet, jsou ve výchozím nastavení `Dependency` typu.

- `Dependency` balíčky typů přidávají prostředky pro sestavení nebo spuštění do knihoven a aplikací a mohou být nainstalovány v jakémkoli typu projektu (za předpokladu, že jsou kompatibilní).

- `DotnetTool` balíčky typů jsou rozšířením rozhraní příkazového řádku [dotnet](/dotnet/articles/core/tools/index) a jsou vyvolány z příkazového řádku. Takové balíčky lze nainstalovat pouze v projektech .NET Core a nemají žádný vliv na operace obnovení. Další podrobnosti o těchto rozšířeních pro jednotlivé projekty jsou k dispozici v dokumentaci  [rozšiřitelnosti .NET Core](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) .

- `Template` balíčky typů poskytují [vlastní šablony](/dotnet/core/tools/custom-templates) , které lze použít k vytvoření souborů nebo projektů, jako jsou aplikace, služby, nástroje nebo knihovny tříd.

- Balíčky vlastních typů používají libovolný identifikátor typu, který odpovídá stejným pravidlům formátu jako ID balíčků. `Dependency` `DotnetTool` Správce balíčků NuGet v aplikaci Visual Studio nerozpoznal jakýkoliv typ jiný než a.

Typy balíčků jsou nastaveny v `.nuspec` souboru. Je nejvhodnější pro zpětnou kompatibilitu, pokud *nechcete explicitně* nastavit `Dependency` typ a místo toho spoléhat na NuGet za předpokladu, že není zadán žádný typ.

- `.nuspec`: Označte typ balíčku v rámci `packageTypes\packageType` uzlu pod `<metadata>` prvkem:

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
