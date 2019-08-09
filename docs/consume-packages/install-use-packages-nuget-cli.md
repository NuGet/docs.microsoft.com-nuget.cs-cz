---
title: Správa balíčků NuGet pomocí rozhraní příkazového řádku NuGet. exe
description: Pokyny k použití rozhraní příkazového řádku NuGet. exe pro práci s balíčky NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 9ef990c16cca62a1fbad25ff1582bfa543135fab
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860563"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a>Správa balíčků pomocí rozhraní příkazového řádku NuGet. exe

Nástroj rozhraní příkazového řádku umožňuje snadno aktualizovat a obnovovat balíčky NuGet v projektech a řešeních. Tento nástroj poskytuje všechny funkce NuGet ve Windows a poskytuje i většinu funkcí v systémech Mac a Linux, když běží v mono.

Rozhraní `nuget.exe` příkazového řádku je pro vaše .NET Framework projektů a projektů, které nejsou ve stylu sady SDK (například projekt bez sady SDK, který cílí na .NET Standard knihovny). Pokud používáte projekt, který není ve stylu sady SDK, který byl migrován do `PackageReference`, `dotnet` použijte místo toho příkaz CLI. Rozhraní `nuget.exe` příkazového řádku vyžaduje soubor [Packages. config](../reference/packages-config.md) pro odkazy na balíčky.

> [!NOTE]
> Ve většině scénářů doporučujeme [migrovat projekty, které nejsou ve stylu sady SDK](../reference/migrate-packages-config-to-package-reference.md) , `packages.config` které používají PackageReference, a pak můžete použít rozhraní `dotnet` příkazového řádku namísto `nuget.exe` rozhraní příkazového řádku. Migrace není aktuálně k dispozici C++ pro projekty a ASP.NET.

Tento článek popisuje základní použití pro několik nejběžnějších příkazů rozhraní `nuget.exe` příkazového řádku. Pro většinu těchto příkazů nástroj CLI vyhledá soubor projektu v aktuálním adresáři, pokud není v příkazu zadaný soubor projektu. Úplný seznam příkazů a argumenty, které můžete použít, najdete v referenčních informacích k [NuGet. exe CLI](../reference/nuget-exe-cli-reference.md).

## <a name="prerequisites"></a>Požadavky

- Nainstalujte rozhraní `nuget.exe` příkazového řádku stažením z [NuGet.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), uložte tento `.exe` soubor do vhodné složky a přidejte tuto složku do proměnné prostředí PATH.

## <a name="install-a-package"></a>Instalace balíčku

Příkaz [install](../reference/cli-reference/cli-ref-install.md) stáhne a nainstaluje balíček do projektu, přičemž použije výchozí nastavení pro aktuální složku pomocí zadaných zdrojů balíčků. Nainstalujte nové balíčky do složky *Packages* v kořenovém adresáři projektu.

> [!IMPORTANT]
> Příkaz neupraví soubor projektu nebo Packages *. config*; tímto způsobem je podobný `restore` jako v tom, že přidává pouze balíčky na disk, ale nemění závislosti projektu. `install` Chcete-li přidat závislost, buď přidejte balíček prostřednictvím uživatelského rozhraní nebo konzoly Správce balíčků v aplikaci Visual Studio, nebo upravte soubor *Packages. config* a `install` potom `restore`spusťte nebo.

1. Otevřete příkazový řádek a přejděte do adresáře, který obsahuje soubor projektu.

2. K instalaci balíčku NuGet do složky Packages použijte následující příkaz .

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    Chcete-li `Newtonsoft.json` balíček nainstalovat do složky Packages, použijte následující příkaz:

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

Případně můžete použít následující příkaz k instalaci balíčku NuGet pomocí existujícího `packages.config` souboru do složky *Packages* . Tím se balíček nepřidá do závislostí projektu, ale nainstaluje se místně.

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a>Instalace konkrétní verze balíčku

Pokud při použití příkazu [install](../reference/cli-reference/cli-ref-install.md) není zadána verze, NuGet nainstaluje nejnovější verzi balíčku. Můžete také nainstalovat specifickou verzi balíčku NuGet:

```cli
nuget install <packageID | configFilePath> -Version <version>
```

Pokud například chcete přidat 12.0.1 `Newtonsoft.json` verze balíčku, použijte tento příkaz:

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

Další informace o omezeních a chování `install`nástroje najdete v tématu [instalace balíčku](#install-a-package).

## <a name="remove-a-package"></a>Odebrat balíček

Chcete-li odstranit jeden nebo více balíčků, odstraňte balíčky, které chcete odebrat ze složky Packages.

Pokud chcete balíčky znovu nainstalovat, použijte `restore` příkaz nebo. `install`

## <a name="list-packages"></a>Výpis balíčků

Seznam balíčků z daného zdroje můžete zobrazit pomocí příkazu [list](../reference/cli-reference/cli-ref-list.md) . K omezení vyhledávání použijte možnost.`-Source`

```cli
nuget list -Source <source>
```

Například vypíšete balíčky ve složce *Packages* .

```cli
nuget list -Source C:\Users\username\source\repos\MyProject\packages
```

Pokud používáte hledaný termín, hledání zahrnuje názvy balíčků, značek a popisů balíčků.

```cli
nuget list <search term>
```

## <a name="update-an-individual-package"></a>Aktualizace jednotlivého balíčku

NuGet nainstaluje nejnovější verzi balíčku, když použijete `install` příkaz, pokud nezadáte verzi balíčku.

## <a name="update-all-packages"></a>Aktualizovat všechny balíčky

Pomocí příkazu [Update](../reference/cli-reference/cli-ref-update.md) aktualizujte všechny balíčky. Aktualizuje všechny balíčky v projektu (pomocí `packages.config`) na nejnovější dostupné verze. Doporučuje se spustit `restore` před spuštěním `update`.

```cli
nuget update
```

## <a name="restore-packages"></a>Obnovit balíčky

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]