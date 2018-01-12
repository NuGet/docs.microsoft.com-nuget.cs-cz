---
title: "Příkaz config NuGet rozhraní příkazového řádku | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: a50295ff-8be9-47d9-a260-822e899334cb
description: "Referenční dokumentace pro příkaz nuget.exe konfigurace"
keywords: "referenční dokumentace týkající se konfigurace nuget, příkazu config"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f49751d9747687177e3b6c1890ee9d2919be8d0e
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/10/2018
---
# <a name="config-command-nuget-cli"></a>příkaz config (NuGet CLI)

**Platí pro:** všechny &bullet; **podporované verze**: všechny

Získá nebo nastaví hodnoty konfigurace NuGet. Další využití, najdete v části [konfigurace chování NuGet](../consume-packages/configuring-nuget-behavior.md). Podrobnosti na povolené názvy klíčů najdete [odkaz na soubor konfigurace NuGet](../Schema/nuget-config-file.md).

## <a name="usage"></a>Použití

```
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

kde `<name>` a `<value>` zadejte pár klíč hodnota v konfiguraci nastavit. Podle potřeby můžete zadat libovolný počet párů. Odebrat hodnotu, zadejte název a `=` přihlášení, ale žádná hodnota.

Povolené názvy klíčů najdete v článku [odkaz na soubor konfigurace NuGet](../Schema/nuget-config-file.md).

V NuGet 3.4 + `<value>` můžete použít [proměnné prostředí](cli-ref-environment-variables.md).

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| AsPath | Vrátí hodnotu konfigurace jako cesta, ignorovat při `-Set` se používá. |
| ConfigFile | *(2.5 +)*  NuGet konfiguračním souboru chcete upravit. Pokud není zadaný, *%AppData%\NuGet\NuGet.Config* se používá. |
| ForceEnglishOutput | *(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze. |
| Nápověda | Zobrazí nápovědu pro příkaz. |
| Neinteraktivní | Potlačí výzvy pro vstup uživatele nebo potvrzení. |
| Podrobnosti | Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné (2.5 +)*. |

Viz také [proměnné prostředí](cli-ref-environment-variables.md)

### <a name="examples"></a>Příklady

```
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
