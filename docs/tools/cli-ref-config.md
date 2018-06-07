---
title: Příkaz config NuGet rozhraní příkazového řádku
description: Referenční dokumentace pro příkaz nuget.exe konfigurace
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 9deab9fcca740ea99da61b7d54700a29c1813e88
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818162"
---
# <a name="config-command-nuget-cli"></a>příkaz config (NuGet CLI)

**Platí pro:** všechny &bullet; **podporované verze**: všechny

Získá nebo nastaví hodnoty konfigurace NuGet. Další využití, najdete v části [konfigurace chování NuGet](../consume-packages/configuring-nuget-behavior.md). Podrobnosti na povolené názvy klíčů najdete [odkaz na soubor konfigurace NuGet](../reference/nuget-config-file.md).

## <a name="usage"></a>Použití

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

kde `<name>` a `<value>` zadejte pár klíč hodnota v konfiguraci nastavit. Podle potřeby můžete zadat libovolný počet párů. Odebrat hodnotu, zadejte název a `=` přihlášení, ale žádná hodnota.

Povolené názvy klíčů najdete v článku [odkaz na soubor konfigurace NuGet](../reference/nuget-config-file.md).

V NuGet 3.4 + `<value>` můžete použít [proměnné prostředí](cli-ref-environment-variables.md).

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| AsPath | Vrátí hodnotu konfigurace jako cesta, ignorovat při `-Set` se používá. |
| ConfigFile | Konfigurační soubor NuGet chcete upravit. Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.|
| ForceEnglishOutput | *(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze. |
| Nápověda | Zobrazí nápovědu pro příkaz. |
| Neinteraktivní | Potlačí výzvy pro vstup uživatele nebo potvrzení. |
| Podrobnosti | Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*. |

Viz také [proměnné prostředí](cli-ref-environment-variables.md)

### <a name="examples"></a>Příklady

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
