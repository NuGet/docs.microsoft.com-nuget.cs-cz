---
title: Rozhraní příkazového řádku NuGet config
description: Referenční informace pro příkaz config nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 376b69186ad22d4d94a1df51146b833a1f6f9bd9
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546475"
---
# <a name="config-command-nuget-cli"></a>příkaz config (rozhraní příkazového řádku NuGet)

**Platí pro:** všechny &bullet; **podporované verze**: všechny

Získá nebo nastaví NuGet konfigurační hodnoty. Další využití, naleznete v tématu [konfigurace chování Nugetu](../consume-packages/configuring-nuget-behavior.md). Podrobnosti o povolené názvy klíčů najdete [odkaz na soubor NuGet config](../reference/nuget-config-file.md).

## <a name="usage"></a>Použití

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

kde `<name>` a `<value>` zadejte pár klíč hodnota v konfiguraci. Podle potřeby můžete zadat libovolný počet párů. Pokud chcete odebrat hodnotu, zadejte název a `=` přihlašování, ale žádná hodnota.

Povolené názvy klíčů, najdete v článku [odkaz na soubor NuGet config](../reference/nuget-config-file.md).

Ve Správci NuGet 3.4 + `<value>` můžete použít [proměnné prostředí](cli-ref-environment-variables.md).

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| AsPath | Vrátí hodnotu konfigurace jako cestu, ignoruje při `-Set` se používá. |
| ConfigFile | Konfigurační soubor NuGet upravit. Pokud není zadán, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.|
| ForceEnglishOutput | *(3.5 +)*  Vynutí nuget.exe pro spuštění pomocí neutrální, základem je angličtina jazyková verze. |
| Help | Zobrazí nápovědu pro příkaz. |
| NonInteractive | Potlačí vyzve k zadání uživatele o vstup ani potvrzení. |
| Verbosity | Určuje množství podrobností, na které se zobrazí ve výstupu: *normální*, *quiet*, *podrobné*. |

Viz také [proměnné prostředí](cli-ref-environment-variables.md)

### <a name="examples"></a>Příklady

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
