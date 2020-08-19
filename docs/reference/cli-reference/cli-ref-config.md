---
title: NuGet CLI – příkaz konfigurace
description: Odkaz na příkaz nuget.exe config
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7d0c1c51f40cba9a5b69f209ffbd995451bfeb9f
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622873"
---
# <a name="config-command-nuget-cli"></a>příkaz config (NuGet CLI)

**Platí pro:** všechny &bullet; **podporované verze**: vše

Získá nebo nastaví hodnoty konfigurace NuGet. Další informace o využití najdete v tématu [běžné konfigurace NuGet](../../consume-packages/configuring-nuget-behavior.md). Podrobnosti o přípustných názvech klíčů najdete v odkazu na [konfigurační soubor NuGet](../nuget-config-file.md).

## <a name="usage"></a>Využití

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

kde `<name>` a `<value>` určuje dvojici klíč-hodnota, která má být nastavena v konfiguraci. Můžete zadat libovolný počet párů podle potřeby. Chcete-li odebrat hodnotu, zadejte název a `=` znaménko, ale žádnou hodnotu.

Informace o přípustných klíčích klíčů najdete v referenční dokumentaci k [konfiguračnímu souboru NuGet](../nuget-config-file.md).

V NuGet 3.4 + `<value>` může použít [proměnné prostředí](cli-ref-environment-variables.md).

## <a name="options"></a>Možnosti


- **`AsPath`**

  Vrátí hodnotu konfigurace jako cestu, při `-Set` použití se ignoruje.

- **`-ConfigFile`**

  Konfigurační soubor NuGet, který se má použít Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows) nebo `~/.nuget/NuGet/NuGet.Config` nebo `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-ForceEnglishOutput`**

  *(3.5 +)* Vynutí spuštění nuget.exe s využitím neutrální jazykové verze založené na angličtině.

- **`-?|-help`**

  Zobrazí informace o nápovědě k příkazu.

- **`-NonInteractive`**

  Potlačí výzvy pro vstup uživatele nebo potvrzení.

- **`-Set`**

  Jedna na další páry klíč-hodnota se nastaví v konfiguraci.

- **`-Verbosity [normal|quiet|detailed]`**

  Určuje množství podrobností zobrazených ve výstupu: `normal` (výchozí), `quiet` nebo `detailed` .

Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .

### <a name="examples"></a>Příklady

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
