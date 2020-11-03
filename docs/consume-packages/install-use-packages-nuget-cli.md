---
title: Správa balíčků NuGet pomocí nuget.exe CLI
description: Pokyny pro použití rozhraní příkazového řádku nuget.exe pro práci s balíčky NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 7039dd27f2dddebc3c84e5ad35d5efec59547792
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237384"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a>Správa balíčků pomocí rozhraní příkazového řádku nuget.exe

Nástroj rozhraní příkazového řádku umožňuje snadno aktualizovat a obnovovat balíčky NuGet v projektech a řešeních. Tento nástroj poskytuje všechny funkce NuGet ve Windows a poskytuje i většinu funkcí v systémech Mac a Linux, když běží v mono.

Rozhraní příkazového `nuget.exe` řádku je pro vaše .NET Framework projektů a projektů, které nejsou ve stylu sady SDK (například projekt bez sady SDK, který cílí na .NET Standard knihovny). Pokud používáte projekt, který není ve stylu sady SDK, který byl migrován do `PackageReference` , použijte `dotnet` místo toho příkaz CLI. Rozhraní příkazového `nuget.exe` řádku vyžaduje soubor [packages.config](../reference/packages-config.md) pro odkazy na balíčky.

> [!NOTE]
> Ve většině scénářů doporučujeme [migrovat projekty, které nejsou ve stylu sady SDK](../consume-packages/migrate-packages-config-to-package-reference.md) , které používají `packages.config` PackageReference, a pak můžete použít rozhraní příkazového `dotnet` řádku namísto rozhraní příkazového `nuget.exe` řádku. Migrace není aktuálně k dispozici pro projekty v jazyce C++ a ASP.NET.

Tento článek popisuje základní použití pro několik nejběžnějších `nuget.exe` příkazů rozhraní příkazového řádku. Pro většinu těchto příkazů nástroj CLI vyhledá soubor projektu v aktuálním adresáři, pokud není v příkazu zadaný soubor projektu. Úplný seznam příkazů a argumenty, které můžete použít, najdete v tématu [nuget.exe odkaz CLI](../reference/nuget-exe-cli-reference.md).

## <a name="prerequisites"></a>Požadavky

- Nainstalujte rozhraní `nuget.exe` příkazového řádku stažením z [NuGet.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), uložte tento `.exe` soubor do vhodné složky a přidejte tuto SLOŽKU do proměnné prostředí PATH.

## <a name="install-a-package"></a>Instalace balíčku

Příkaz [install](../reference/cli-reference/cli-ref-install.md) stáhne a nainstaluje balíček do projektu, přičemž použije výchozí nastavení pro aktuální složku pomocí zadaných zdrojů balíčků. Nainstalujte nové balíčky do složky *Packages* v kořenovém adresáři projektu.

> [!IMPORTANT]
> `install`Příkaz neupraví soubor projektu ani *packages.config* ; v tomto případě je to podobné jako `restore` v tom, že přidává pouze balíčky na disk, ale nemění závislosti projektu. Chcete-li přidat závislost, přidejte balíček prostřednictvím uživatelského rozhraní nebo konzoly Správce balíčků v aplikaci Visual Studio, nebo upravte *packages.config* a pak spusťte buď `install` nebo `restore` .

1. Otevřete příkazový řádek a přejděte do adresáře, který obsahuje soubor projektu.

2. K instalaci balíčku NuGet do složky *Packages* použijte následující příkaz.

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    Chcete-li `Newtonsoft.json` balíček nainstalovat do složky *Packages* , použijte následující příkaz:

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

Pokud například chcete přidat 12.0.1 verze `Newtonsoft.json` balíčku, použijte tento příkaz:

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

Další informace o omezeních a chování nástroje najdete `install` v tématu [instalace balíčku](#install-a-package).

## <a name="remove-a-package"></a>Odebrat balíček

Chcete-li odstranit jeden nebo více balíčků, odstraňte balíčky, které chcete odebrat ze složky *Packages* .

Pokud chcete balíčky znovu nainstalovat, použijte `restore` `install` příkaz nebo.

## <a name="list-packages"></a>Výpis balíčků

Seznam balíčků z daného zdroje můžete zobrazit pomocí příkazu [list](../reference/cli-reference/cli-ref-list.md) . `-Source`K omezení vyhledávání použijte možnost.

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

Pomocí příkazu [Update](../reference/cli-reference/cli-ref-update.md) aktualizujte všechny balíčky. Aktualizuje všechny balíčky v projektu (pomocí `packages.config` ) na nejnovější dostupné verze. Doporučuje se spustit `restore` před spuštěním `update` .

```cli
nuget update
```

## <a name="restore-packages"></a>Obnovení balíčků

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]

## <a name="get-the-cli-version"></a>Získat verzi rozhraní příkazového řádku

Použijte tento příkaz:

```cli
nuget help
```

První řádek ve výstupu pro Help zobrazuje verzi. Chcete-li se vyhnout posunu nahoru, použijte `nuget help | more` místo toho.