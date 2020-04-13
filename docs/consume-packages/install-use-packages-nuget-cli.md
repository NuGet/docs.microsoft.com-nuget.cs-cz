---
title: Správa balíčků NuGet pomocí cli nuget.exe
description: Pokyny pro použití cli nuget.exe pro práci s balíčky NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 7039dd27f2dddebc3c84e5ad35d5efec59547792
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428686"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a>Správa balíčků pomocí cli nuget.exe

Nástroj CLI umožňuje snadno aktualizovat a obnovit balíčky NuGet v projektech a řešeních. Tento nástroj poskytuje všechny funkce NuGet v systému Windows a také poskytuje většinu funkcí na Mac a Linux při spuštění pod Mono.

Rozhraní `nuget.exe` se konstatování je pro projekty rozhraní .NET Framework a projekty, které nejsou ve stylu sady SDK (například projekt bez sdk stylu, který cílí na knihovny .NET Standard). Pokud používáte projekt, který nebyl ve stylu sady SDK, který byl migrován , `PackageReference`použijte místo toho `dotnet` cli. ClI `nuget.exe` vyžaduje [soubor packages.config](../reference/packages-config.md) pro odkazy na balíčky.

> [!NOTE]
> Ve většině scénářů doporučujeme [migrovat projekty,](../consume-packages/migrate-packages-config-to-package-reference.md) které `packages.config` se nepoužívají ve stylu `dotnet` sady SDK, a pak můžete místo `nuget.exe` cli použít zapínací úsečkové číslo. Migrace není v současné době k dispozici pro projekty jazyka C++ a ASP.NET.

Tento článek ukazuje základní použití pro několik `nuget.exe` nejběžnějších příkazů příkazového příkazu. U většiny těchto příkazů nástroj příkazcli hledá soubor projektu v aktuálním adresáři, pokud není v příkazu zadán soubor projektu. Úplný seznam příkazů a argumentů, které můžete použít, naleznete v [odkazu cli nuget.exe](../reference/nuget-exe-cli-reference.md).

## <a name="prerequisites"></a>Požadavky

- Nainstalujte `nuget.exe` rozhraní se konstatování pomocí `.exe` nuget.org [,](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe)uložíte jej do vhodné složky a přidáte tuto složku do proměnné prostředí PATH.

## <a name="install-a-package"></a>Instalace balíčku

Příkaz [install](../reference/cli-reference/cli-ref-install.md) stáhne a nainstaluje balíček do projektu, který je výchozí pro aktuální složku pomocí určených zdrojů balíčků. Nainstalujte nové balíčky do složky *balíčky* v kořenovém adresáři projektu.

> [!IMPORTANT]
> Příkaz `install`nezmění soubor projektu nebo *soubor packages.config*; tímto způsobem je podobný `restore` v tom, že pouze přidává balíčky na disk, ale nemění závislosti projektu. Chcete-li přidat závislost, přidejte balíček prostřednictvím uzly Správce balíčků nebo konzoly v `install` `restore`sadě Visual Studio nebo upravte *soubor packages.config* a spusťte buď nebo .

1. Otevřete příkazový řádek a přepněte do adresáře, který obsahuje soubor projektu.

2. Pomocí následujícího příkazu nainstalujte balíček NuGet do složky *packages.*

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    Chcete-li `Newtonsoft.json` balíček nainstalovat do složky *balíčky,* použijte následující příkaz:

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

Alternativně můžete použít následující příkaz k instalaci balíčku NuGet pomocí existujícího `packages.config` souboru do složky *balíčky.* To nepřidá balíček do závislostí projektu, ale nainstaluje místně.

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a>Instalace konkrétní verze balíčku

Pokud verze není zadána při použití příkazu [install,](../reference/cli-reference/cli-ref-install.md) NuGet nainstaluje nejnovější verzi balíčku. Můžete také nainstalovat konkrétní verzi balíčku Nuget:

```cli
nuget install <packageID | configFilePath> -Version <version>
```

Chcete-li například přidat verzi `Newtonsoft.json` balíčku 12.0.1, použijte tento příkaz:

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

Další informace o omezeních a `install`chování aplikace naleznete v [tématu Instalace balíčku](#install-a-package).

## <a name="remove-a-package"></a>Odebrání balíčku

Chcete-li odstranit jeden nebo více balíčků, odstraňte balíčky, které chcete odebrat ze složky *balíčky.*

Pokud chcete přeinstalovat balíčky, `restore` `install` použijte příkaz nebo.

## <a name="list-packages"></a>Seznam balíčků

Seznam balíčků z daného zdroje můžete zobrazit pomocí příkazu [seznam.](../reference/cli-reference/cli-ref-list.md) Pomocí `-Source` možnosti můžete hledání omezit.

```cli
nuget list -Source <source>
```

Například seznam balíčků ve složce *balíčky.*

```cli
nuget list -Source C:\Users\username\source\repos\MyProject\packages
```

Pokud používáte hledaný výraz, hledání obsahuje názvy balíčků, značek a popisů balíčků.

```cli
nuget list <search term>
```

## <a name="update-an-individual-package"></a>Aktualizace jednotlivého balíčku

NuGet nainstaluje nejnovější verzi balíčku při `install` použití příkazu, pokud zadáte verzi balíčku.

## <a name="update-all-packages"></a>Aktualizovat všechny balíčky

Pomocí příkazu [update](../reference/cli-reference/cli-ref-update.md) aktualizujte všechny balíčky. Aktualizuje všechny balíčky v `packages.config`projektu (pomocí) na jejich nejnovější dostupné verze. Před spuštěním `update` `restore` se doporučuje spustit .

```cli
nuget update
```

## <a name="restore-packages"></a>Obnovení balíčků

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]

## <a name="get-the-cli-version"></a>Získání verze CLI

Pomocí tohoto příkazu:

```cli
nuget help
```

První řádek ve výstupu nápovědy zobrazuje verzi. Chcete-li se vyhnout `nuget help | more` posouvání nahoru, použijte místo toho.