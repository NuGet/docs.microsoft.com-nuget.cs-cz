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
ms.openlocfilehash: 12a8b51dd11b9bc3a496e02e869cdeb95e67b9e3
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
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
