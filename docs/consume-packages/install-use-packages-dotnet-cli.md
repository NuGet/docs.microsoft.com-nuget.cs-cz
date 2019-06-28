---
title: Nainstalovat a spravovat balíčky NuGet pomocí rozhraní příkazového řádku dotnet
description: Pokyny k používání rozhraní příkazového řádku dotnet pro práci s balíčky NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: a8fd525f2446f9468664f1d80ef8808127a24be7
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427641"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a>Instalace a Správa balíčků s využitím rozhraní příkazového řádku dotnet

Nástroj příkazového řádku umožňuje snadno nainstalování, odinstalování a aktualizace balíčků NuGet do projektů a řešení. Běží na Windows, Mac OS X a Linux.

Rozhraní příkazového řádku dotnet je pro použití v projektu .NET Core a .NET Standard (typy SDK – vizuální styl projektu) a pro jakékoli jiné sady SDK – vizuální styl projekty (například SDK – vizuální styl projektu aplikace, které cílí na .NET Framework). Další informace najdete v tématu [SDK atribut](/dotnet/core/tools/csproj#additions).

Tento článek popisuje základní informace o využití pro některé z nejčastěji používané příkazy rozhraní příkazového řádku dotnet. Pro většinu těchto příkazů nástroje rozhraní příkazového řádku hledá soubor projektu do aktuálního adresáře, pokud soubor projektu je zadané v příkazu (soubor projektu je volitelný přepínač). Úplný seznam příkazů a argumenty, které můžete použít, najdete v článku [nástroje rozhraní příkazového řádku (CLI) pro .NET Core](../tools/dotnet-commands.md).

## <a name="prerequisites"></a>Požadavky

- [.NET Core SDK](https://www.microsoft.com/net/download/), která poskytuje `dotnet` nástroj příkazového řádku. Spouští se v sadě Visual Studio 2017, které pomocí libovolné platformy .NET Core se automaticky nainstaluje rozhraní příkazového řádku dotnet související úlohy.

## <a name="install-a-package"></a>Instalace balíčku

[příkaz DotNet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) přidá odkaz na balíček do souboru projektu a pak spustí `dotnet restore` k instalaci balíčku.

1. Otevřete příkazový řádek a přejděte do adresáře, který obsahuje váš soubor projektu.

2. Použijte následující příkaz k instalaci balíčku Nuget:

    ```cli
    dotnet add package <PACKAGE_NAME>
    ```

    Například, chcete-li nainstalovat `Newtonsoft.Json` balíček, použijte následující příkaz

    ```cli
    dotnet add package Newtonsoft.Json
    ```

3. Po dokončení příkazu, podívejte se na soubor projektu a ujistěte se, že byl nainstalován balíček.

   Můžete otevřít `.csproj` soubor přidaný odkaz:

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a>Instalace konkrétní verze balíčku

Pokud není zadána verze, NuGet nainstaluje nejnovější verzi balíčku. Můžete také použít [se příkaz dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) příkaz k instalaci na konkrétní verzi balíčku Nuget:

```cli
dotnet add package <PACKAGE_NAME> -v <VERSION>
```

Chcete-li například přidat verzi 12.0.1 `Newtonsoft.Json` balíček, použijte tento příkaz:

```cli
dotnet add package Newtonsoft.Json -v 12.0.1
```

## <a name="list-package-references"></a>Odkazy na balíček seznamu

Můžete zobrazit seznam odkazy na balíček pro váš projekt používá [uvedení balíčku dotnet](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) příkazu.

```cli
dotnet list package
```

## <a name="remove-a-package"></a>Odebrat balíček

Použití [dotnet odebrat balíček](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) příkazu odeberte odkaz na balíček ze souboru projektu.

```cli
dotnet remove package <PACKAGE_NAME>
```

Například, chcete-li odebrat `Newtonsoft.Json` balíček, použijte následující příkaz

```cli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a>Aktualizace balíčku

NuGet nainstaluje nejnovější verzi balíčku, při použití `dotnet add package` příkazu, pokud neurčíte verzi balíčku (`-v` přepínače).

## <a name="restore-packages"></a>Obnovení balíčků

Použití [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) příkaz, který obnoví balíčky uvedené v souboru projektu (viz [PackageReference](../consume-packages/package-references-in-project-files.md)). S .NET Core 2.0 nebo novější, obnovení se provádí automaticky pomocí `dotnet build` a `dotnet run`. Od verze NuGet 4.0, toto řešení běží stejný kód jako `nuget restore`.

Chcete-li obnovit balíček pomocí `dotnet restore`:

```cli
dotnet restore 
```
