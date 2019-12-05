---
title: Instalace a Správa balíčků NuGet pomocí rozhraní příkazového řádku dotnet
description: Pokyny pro použití rozhraní příkazového řádku dotnet pro práci s balíčky NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 67cca81c48970c7f2e2cf0a64ee5ba57704a31e2
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825154"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a>Instalace a Správa balíčků pomocí rozhraní příkazového řádku dotnet

Nástroj rozhraní příkazového řádku umožňuje snadno nainstalovat, odinstalovat a aktualizovat balíčky NuGet v projektech a řešeních. Běží na Windows, Mac OS X a Linux.

Rozhraní příkazového řádku dotnet je pro použití ve vašem projektu .NET Core a .NET Standard (typy projektů ve stylu sady SDK) a pro všechny další projekty ve stylu sady SDK (například projekt sady SDK, který cílí na .NET Framework). Další informace najdete v tématu [atribut sady SDK](/dotnet/core/tools/csproj#additions).

Tento článek popisuje základní použití pro několik nejběžnějších příkazů příkazového řádku dotnet. Pro většinu těchto příkazů nástroj CLI vyhledá soubor projektu v aktuálním adresáři, pokud soubor projektu není zadán v příkazu (soubor projektu je volitelný přepínač). Úplný seznam příkazů a argumenty, které můžete použít, najdete v tématu [nástroje rozhraní příkazového řádku (CLI) .NET Core](../reference/dotnet-commands.md).

## <a name="prerequisites"></a>Požadavky

- [.NET Core SDK](https://www.microsoft.com/net/download/), který poskytuje nástroj příkazového řádku `dotnet`. Počínaje sadou Visual Studio 2017 se rozhraní příkazového řádku dotnet automaticky nainstaluje se všemi úlohami souvisejícími s .NET Core.

## <a name="install-a-package"></a>Instalace balíčku

[dotnet Add Package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) přidá odkaz na balíček do souboru projektu a potom spustí `dotnet restore` pro instalaci balíčku.

1. Otevřete příkazový řádek a přejděte do adresáře, který obsahuje soubor projektu.

2. K instalaci balíčku NuGet použijte následující příkaz:

    ```dotnetcli
    dotnet add package <PACKAGE_NAME>
    ```

    Například pro instalaci balíčku `Newtonsoft.Json` použijte následující příkaz.

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

3. Po dokončení příkazu si prohlédněte soubor projektu a ujistěte se, že byl balíček nainstalován.

   Pokud chcete zobrazit přidaný odkaz, můžete otevřít soubor `.csproj`:

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a>Instalace konkrétní verze balíčku

Pokud není zadaná verze, NuGet nainstaluje nejnovější verzi balíčku. K instalaci konkrétní verze balíčku NuGet můžete použít taky příkaz [dotnet Add Package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) :

```dotnetcli
dotnet add package <PACKAGE_NAME> -v <VERSION>
```

Pokud například chcete přidat 12.0.1 verze balíčku `Newtonsoft.Json`, použijte tento příkaz:

```dotnetcli
dotnet add package Newtonsoft.Json -v 12.0.1
```

## <a name="list-package-references"></a>Výpis odkazů na balíčky

Odkazy na balíček pro svůj projekt můžete zobrazit pomocí příkazu pro [Výpis balíčku dotnet](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) .

```dotnetcli
dotnet list package
```

## <a name="remove-a-package"></a>Odebrat balíček

Pomocí příkazu [dotnet Remove Package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) odeberte odkaz na balíček ze souboru projektu.

```dotnetcli
dotnet remove package <PACKAGE_NAME>
```

Chcete-li například odebrat balíček `Newtonsoft.Json`, použijte následující příkaz

```dotnetcli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a>Aktualizace balíčku

Pokud nezadáte verzi balíčku (`-v` přepínač), nainstaluje balíček NuGet nejnovější verzi balíčku, když použijete příkaz `dotnet add package`.

## <a name="restore-packages"></a>Obnovit balíčky

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]
