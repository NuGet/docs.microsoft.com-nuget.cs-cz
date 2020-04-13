---
title: Instalace a správa balíčků NuGet pomocí rozhraní SE konstatování dotnet
description: Pokyny pro použití dotnet CLI pro práci s balíčky NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 67cca81c48970c7f2e2cf0a64ee5ba57704a31e2
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "74825154"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a>Instalace a správa balíčků pomocí rozhraní SE kontinua dotnet

Nástroj CLI umožňuje snadno nainstalovat, odinstalovat a aktualizovat balíčky NuGet v projektech a řešeních. Běží na Windows, Mac OS X a Linux.

Rozhraní SE konstatování dotnet cli je pro použití v projektu .NET Core a .NET Standard (typy projektů ve stylu sady SDK) a pro všechny ostatní projekty ve stylu sady SDK (například projekt ve stylu sady SDK, který cílí na rozhraní .NET Framework). Další informace naleznete v [atributu SDK](/dotnet/core/tools/csproj#additions).

Tento článek ukazuje základní použití pro několik nejběžnějších příkazů příkazového příkazu příkazu příkazu příkazu příkazu příkazu dotnet. U většiny těchto příkazů nástroj příkazcli hledá soubor projektu v aktuálním adresáři, pokud není v příkazu zadán soubor projektu (soubor projektu je volitelný přepínač). Úplný seznam příkazů a argumentů, které můžete použít, naleznete v [nástrojích rozhraní CLI (.NET Core) rozhraní příkazového řádku (CLI).](../reference/dotnet-commands.md)

## <a name="prerequisites"></a>Požadavky

- Sada [.NET Core SDK](https://www.microsoft.com/net/download/) `dotnet` , která poskytuje nástroj příkazového řádku. Počínaje Visual Studio 2017, dotnet CLI se automaticky nainstaluje s všechny úlohy související s jádrem .NET.

## <a name="install-a-package"></a>Instalace balíčku

[dotnet přidat balíček](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) přidá odkaz na balíček do souboru projektu, pak spustí `dotnet restore` k instalaci balíčku.

1. Otevřete příkazový řádek a přepněte do adresáře, který obsahuje soubor projektu.

2. K instalaci balíčku Nuget použijte následující příkaz:

    ```dotnetcli
    dotnet add package <PACKAGE_NAME>
    ```

    Chcete-li například `Newtonsoft.Json` nainstalovat balíček, použijte následující příkaz

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

3. Po dokončení příkazu se podívejte na soubor projektu a ujistěte se, že byl balíček nainstalován.

   Soubor můžete `.csproj` otevřít a zobrazit tak přidanou referenci:

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a>Instalace konkrétní verze balíčku

Pokud není zadána verze, NuGet nainstaluje nejnovější verzi balíčku. Příkaz [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) můžete také použít k instalaci konkrétní verze balíčku Nuget:

```dotnetcli
dotnet add package <PACKAGE_NAME> -v <VERSION>
```

Chcete-li například přidat verzi `Newtonsoft.Json` balíčku 12.0.1, použijte tento příkaz:

```dotnetcli
dotnet add package Newtonsoft.Json -v 12.0.1
```

## <a name="list-package-references"></a>Seznam odkazů na balíčky

Můžete seznam odkazů na balíček pro váš projekt pomocí příkazu [balíček seznamu dotnet.](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x)

```dotnetcli
dotnet list package
```

## <a name="remove-a-package"></a>Odebrání balíčku

Pomocí příkazu [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) odeberte odkaz na balíček ze souboru projektu.

```dotnetcli
dotnet remove package <PACKAGE_NAME>
```

Chcete-li například `Newtonsoft.Json` balíček odebrat, použijte následující příkaz

```dotnetcli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a>Aktualizace balíčku

NuGet nainstaluje nejnovější verzi balíčku při `dotnet add package` použití příkazu, pokud`-v` nezadáte verzi balíčku (přepínač).

## <a name="restore-packages"></a>Obnovení balíčků

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]
