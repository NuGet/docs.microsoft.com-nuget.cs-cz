---
title: Spravovat balíčky NuGet pomocí rozhraní příkazového řádku nuget.exe
description: Pokyny k používání rozhraní příkazového řádku nuget.exe pro práci s balíčky NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: e60bca8fe2f80b044e466db2a100d6c6d167edb7
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427629"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a>Správa balíčků s využitím rozhraní příkazového řádku nuget.exe

Nástroj příkazového řádku můžete snadno aktualizovat a obnovení balíčků NuGet do projektů a řešení. Tento nástroj poskytuje všechny funkce NuGet pro Windows a také poskytuje většinu funkcí na Mac a Linux, když je spuštěno mono.

Rozhraní příkazového řádku nuget.exe je pro projekty SDK styl, (například jeden, který cílí na knihovny .NET Standard) a rozhraní .NET Framework projektu. Pokud používáte sadu SDK styl projektu, který se migroval na `PackageReference`, místo toho použijte rozhraní příkazového řádku dotnet. Vyžaduje se rozhraní příkazového řádku NuGet [souboru packages.config](../reference/packages-config.md) soubor pro odkazy na balíček.

> [!NOTE]
> Ve většině scénářů doporučujeme [migraci projektů SDK styl](../reference/migrate-packages-config-to-package-reference.md) , které používají `packages.config` na PackageReference, a pak můžete použít rozhraní příkazového řádku dotnet místo `nuget.exe` rozhraní příkazového řádku. Migrace není aktuálně k dispozici pro projekty jazyka C++ a technologií ASP.NET.

Tento článek popisuje základní informace o využití pro některé z nejčastěji používané příkazy rozhraní příkazového řádku nuget.exe. Pro většinu těchto příkazů nástroje rozhraní příkazového řádku hledá soubor projektu do aktuálního adresáře, pokud soubor projektu je zadané v příkazu. Úplný seznam příkazů a argumenty, které můžete použít, najdete v článku [referenční informace o rozhraní příkazového řádku nuget.exe](../tools/nuget-exe-cli-reference.md).

## <a name="prerequisites"></a>Požadavky

- Nainstalujte `nuget.exe` rozhraní příkazového řádku, stáhněte si ji z [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), ukládání, který `.exe` soubor vhodný složky a přidání složky do proměnné prostředí PATH.

## <a name="install-a-package"></a>Instalace balíčku

[Nainstalovat](../tools/cli-ref-install.md) příkaz stáhne a nainstaluje balíček do projektu, jako výchozí se použije aktuální složku, pomocí zadaného balíčku zdroje. Nainstalovat nové balíčky do *balíčky* složku v kořenovém adresáři projektu.

> [!IMPORTANT]
> `install`Příkaz neprovede žádné změny souboru projektu nebo *souboru packages.config*; tímto způsobem je podobný `restore` , pouze na disk přidá balíčky ale nedojde ke změně závislosti projektu. Můžete přidat závislost, přidejte balíček přes uživatelské rozhraní Správce balíčků nebo konzoly v sadě Visual Studio, nebo upravte *souboru packages.config* a spustit některý `install` nebo `restore`.

1. Otevřete příkazový řádek a přejděte do adresáře, který obsahuje váš soubor projektu.

2. Použijte následující příkaz k instalaci balíčku NuGet *balíčky* složky.

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    K instalaci `Newtonsoft.json` balíček do *balíčky* složky, použijte následující příkaz:

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

Alternativně slouží následující příkaz k instalaci balíčku NuGet pomocí existující `packages.config` do souboru *balíčky* složky. Nedojde k přidání balíčku do závislostí vašeho projektu, ale nainstaluje místně.

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a>Instalace konkrétní verze balíčku

Pokud neurčíte verzi, při použití [nainstalovat](../tools/cli-ref-install.md) příkaz nainstaluje nejnovější verzi balíčku NuGet. Můžete také nainstalovat určitou verzi balíčku Nuget:

```cli
nuget install <packageID | configFilePath> -Version <version>
```

Chcete-li například přidat verzi 12.0.1 `Newtonsoft.json` balíček, použijte tento příkaz:

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

Další informace o omezeních a chování `install`, naleznete v tématu [nainstalovat balíček](#install-a-package).

## <a name="remove-a-package"></a>Odebrat balíček

Pokud chcete odstranit jeden nebo více balíčků, odstraňte balíčky, které chcete odebrat z *balíčky* složky.

Pokud chcete znovu nainstaluje balíčky, použijte `restore` nebo `install` příkazu.

## <a name="list-packages"></a>Seznam balíčků

Můžete zobrazit seznam balíčků z daného zdroje pomocí [seznamu](../tools/cli-ref-list.md) příkazu. Použití `-Source` pro omezení hledání.

```cli
nuget list -Source <source>
```

Například balíčků v seznamu *balíčky* složky.

```cli
nuget list -Source C:\Users\username\source\repos\MyProject\packages
```

Pokud používáte hledaný termín, hledání zahrnuje názvy balíčků, značky a Popis balíčku.

```cli
nuget list <search term>
```

## <a name="update-an-individual-package"></a>Jednotlivé aktualizace

NuGet nainstaluje nejnovější verzi balíčku, při použití `install` příkazu, pokud neurčíte verzi balíčku.

## <a name="update-all-packages"></a>Aktualizovat všechny balíčky

Použití [aktualizovat](../tools/cli-ref-update.md) příkaz k aktualizaci všech balíčků. Aktualizuje všechny balíčky v projektu (pomocí `packages.config`) jejich nejnovější dostupné verze. Doporučuje se spouštět `restore` dřív, než spustíte `update`.

```cli
nuget update
```

## <a name="restore-packages"></a>Obnovení balíčků

Použití [obnovení](../tools/cli-ref-restore.md) příkaz, který se stáhne a nainstaluje všechny balíčky, které chybí *balíčky* složky.

`restore` pouze balíčky přidá na disk, ale nedojde ke změně závislosti projektu. Chcete-li obnovit závislosti projektu, upravte `packages.config`, pak použít `restore` příkaz.

Chcete-li obnovit balíček pomocí `restore`:

```cli
nuget restore MySolution.sln
```