---
title: NuGet CLI – příkaz konfigurace
description: Referenční informace k příkazu NuGet. exe config
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 384e708187a747221de103720cc51af07acf713e
ms.sourcegitcommit: f9e39ff9ca19ba4a26e52b8a5e01e18eb0de5387
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/24/2019
ms.locfileid: "68433319"
---
# <a name="config-command-nuget-cli"></a>příkaz config (NuGet CLI)

**Platí pro:** všechny &bullet; **podporované verze**: vše

Získá nebo nastaví hodnoty konfigurace NuGet. Další informace o využití najdete v tématu [běžné konfigurace NuGet](../../consume-packages/configuring-nuget-behavior.md). Podrobnosti o přípustných názvech klíčů najdete v odkazu na [konfigurační soubor NuGet](../nuget-config-file.md).

## <a name="usage"></a>Použití

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

kde `<name>` a`<value>` určuje dvojici klíč-hodnota, která má být nastavena v konfiguraci. Můžete zadat libovolný počet párů podle potřeby. Chcete-li odebrat hodnotu, zadejte název a `=` znaménko, ale žádnou hodnotu.

Informace o přípustných klíčích klíčů najdete v referenční dokumentaci k [konfiguračnímu souboru NuGet](../nuget-config-file.md).

V NuGet 3.4 + `<value>` může použít [proměnné prostředí](cli-ref-environment-variables.md).

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| AsPath | Vrátí hodnotu konfigurace jako cestu, při `-Set` použití se ignoruje. |
| ConfigFile | Konfigurační soubor NuGet, který se má upravit. Pokud tento parametr nezadáte, použije se výchozí soubor`%AppData%\NuGet\NuGet.Config` – (Windows) `~/.config/NuGet/NuGet.Config` nebo (Mac/Linux) `~/.nuget/NuGet/NuGet.Config` nebo (závisí na distribuci OS).|
| ForceEnglishOutput | *(3.5 +)* Vynutí, aby soubor NuGet. exe běžel pomocí neutrální jazykové verze určené pro angličtinu. |
| Help | Zobrazí informace o nápovědě k příkazu. |
| NonInteractive | Potlačí výzvy pro vstup uživatele nebo potvrzení. |
| Verbosity | Určuje množství podrobností zobrazených ve výstupu: *normální*, tiché a *podrobné*. |

Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .

### <a name="examples"></a>Příklady

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
