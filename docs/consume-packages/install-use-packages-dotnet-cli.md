---
title: Instalace a Správa balíčků NuGet pomocí rozhraní příkazového řádku dotnet
description: Pokyny pro použití rozhraní příkazového řádku dotnet pro práci s balíčky NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: fecf14f0f04d5063f89080b2756f988739c1412c
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859262"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a>Instalace a Správa balíčků pomocí rozhraní příkazového řádku dotnet

Nástroj rozhraní příkazového řádku umožňuje snadno nainstalovat, odinstalovat a aktualizovat balíčky NuGet v projektech a řešeních. Běží na Windows, Mac OS X a Linux.

Rozhraní příkazového řádku dotnet je pro použití ve vašem projektu .NET Core a .NET Standard (typy projektů ve stylu sady SDK) a pro všechny další projekty ve stylu sady SDK (například projekt sady SDK, který cílí na .NET Framework). Další informace najdete v tématu [atribut sady SDK](/dotnet/core/tools/csproj#additions).

Tento článek popisuje základní použití pro několik nejběžnějších příkazů příkazového řádku dotnet. Pro většinu těchto příkazů nástroj CLI vyhledá soubor projektu v aktuálním adresáři, pokud soubor projektu není zadán v příkazu (soubor projektu je volitelný přepínač). Úplný seznam příkazů a argumenty, které můžete použít, najdete v tématu [nástroje rozhraní příkazového řádku (CLI) .NET Core](../reference/dotnet-commands.md).

## <a name="prerequisites"></a>Předpoklady

- [.NET Core SDK](https://www.microsoft.com/net/download/), která poskytuje `dotnet` Nástroj příkazového řádku. Počínaje sadou Visual Studio 2017 se rozhraní příkazového řádku dotnet automaticky nainstaluje se všemi úlohami souvisejícími s .NET Core.

## <a name="install-a-package"></a>Instalace balíčku

[dotnet Add Package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) přidá odkaz na balíček do souboru projektu a potom spustí `dotnet restore` instalaci balíčku.

1. Otevřete příkazový řádek a přejděte do adresáře, který obsahuje soubor projektu.

2. K instalaci balíčku NuGet použijte následující příkaz:

    ```dotnetcli
    dotnet add package <PACKAGE_NAME>
    ```

    Pokud například chcete `Newtonsoft.Json` balíček nainstalovat, použijte následující příkaz.

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

3. Po dokončení příkazu si prohlédněte soubor projektu a ujistěte se, že byl balíček nainstalován.

   Tento soubor můžete otevřít `.csproj` a zobrazit tak přidaný odkaz:

    ```xml
    <ItemGroup>
      <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
    </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a>Instalace konkrétní verze balíčku

Pokud není zadaná verze, NuGet nainstaluje nejnovější verzi balíčku. K instalaci konkrétní verze balíčku NuGet můžete použít taky příkaz [dotnet Add Package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) :

```dotnetcli
dotnet add package <PACKAGE_NAME> --version <VERSION>
```

Pokud například chcete přidat 12.0.1 verze `Newtonsoft.Json` balíčku, použijte tento příkaz:

```dotnetcli
dotnet add package Newtonsoft.Json --version 12.0.1
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

Chcete-li například odebrat `Newtonsoft.Json` balíček, použijte následující příkaz

```dotnetcli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a>Aktualizace balíčku

NuGet nainstaluje nejnovější verzi balíčku, když použijete `dotnet add package` příkaz, pokud nezadáte verzi balíčku ( `-v` přepínač).

## <a name="restore-packages"></a>Obnovení balíčků

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]
