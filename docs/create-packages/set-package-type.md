---
title: Nastavit typ balíčku NuGet
description: Popisuje typy balíčků k označení zamýšlené použití souboru balíčku.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 8a3ba6af19125b75af17cab8c093e89485e20324
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/12/2019
ms.locfileid: "67843533"
---
# <a name="set-a-nuget-package-type"></a>Nastavit typ balíčku NuGet

Nuget 3.5 +, může být označený balíčky s konkrétním *typ balíčku* označující jeho zamýšlené použití. Balíčky není označena jako s typem, včetně všech balíčků, které jsou vytvořené pomocí starší verze balíčku nuget, ve výchozím nastavení `Dependency` typu.

- `Dependency` balíčky typ sestavení nebo runtime prostředky přidat do knihovny a aplikace a může být nainstalován v libovolným typem projektu (za předpokladu, že jsou kompatibilní).

- `DotnetCliTool` Typ balíčky jsou rozšíření [rozhraní příkazového řádku dotnet](/dotnet/articles/core/tools/index) a jsou vyvolány z příkazového řádku. Tyto balíčky můžete nainstalovat jenom v projektech .NET Core a nemají žádný vliv na operace obnovení. Další podrobnosti o těchto rozšířeních jednotlivých projektů jsou dostupné v [rozšiřitelnost .NET Core](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) dokumentaci.

- Vlastní typ balíčky pomocí libovolného typu identifikátor, který odpovídá stejná pravidla formát jako ID balíčku. Jakýkoli typ jiný než `Dependency` a `DotnetCliTool`, ale nejsou rozpoznány v aplikaci Správce balíčků NuGet v sadě Visual Studio.

Typy balíčků jsou nastaveny `.nuspec` souboru. Je nejvhodnější pro zpětnou kompatibilitu s *není* explicitně nastaveno `Dependency` zadejte a místo toho přináší setrvávání u NuGet tohoto typu, pokud žádný typ za předpokladu, že je zadán.

- `.nuspec`: Označuje typ balíčku v rámci `packageTypes\packageType` pod uzlem `<metadata>` element:

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetCliTool" />
        </packageTypes>
        </metadata>
    </package>
    ```
