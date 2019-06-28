---
title: Příkaz rozhraní příkazového řádku NuGet delete
description: Referenční informace pro příkaz delete nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3ea2dc3e87d0a626704fe5623d39eaf5bd3f3446
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426112"
---
# <a name="delete-command-nuget-cli"></a>Odstranit příkazu (rozhraní příkazového řádku NuGet)

**Platí pro:** balíček publikování &bullet; **podporované verze:** všechny

Odstraní nebo unlists balíčku ze zdroje balíčku. Pro nuget.org, příkazem k odstranění [unlists balíček](../nuget-org/policies/deleting-packages.md).

## <a name="usage"></a>Použití

```cli
nuget delete <packageID> <packageVersion> [options]
```

kde `<packageID>` a `<packageVersion>` určit přesné balíček odstranit nebo vyjmutí ze seznamu. Přesné chování závisí na zdroji. Pro místní složky například balíček se odstraní; Tento balíček představuje pro nuget.org neuvedené v seznamu.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| ApiKey | Klíč rozhraní API pro cílového úložiště. Pokud není k dispozici, použije se verze zadaná v konfiguračním souboru. |
| ConfigFile | Konfigurační soubor NuGet použít. Pokud není zadán, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.|
| ForceEnglishOutput | *(3.5 +)*  Vynutí nuget.exe pro spuštění pomocí neutrální, základem je angličtina jazyková verze. |
| Help | Zobrazí nápovědu pro příkaz. |
| NonInteractive | Potlačí vyzve k zadání uživatele o vstup ani potvrzení. |
| Source | Určuje adresu URL serveru. Adresa URL nuget.org `https://api.nuget.org/v3/index.json`. Pro privátní kanály, nahraďte název hostitele, například *%hostname%/api/v3*. |
| Verbosity | Určuje množství podrobností, na které se zobrazí ve výstupu: *normální*, *quiet*, *podrobné*. |

Viz také [proměnné prostředí](cli-ref-environment-variables.md)

## <a name="examples"></a>Příklady

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
