---
title: Příkaz rozhraní příkazového řádku NuGet delete
description: Referenční informace pro příkaz delete nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 11eea6e806d7bfe364587db9c7ef8374da1819f9
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548507"
---
# <a name="delete-command-nuget-cli"></a>Odstranit příkazu (rozhraní příkazového řádku NuGet)

**Platí pro:** balíček publikování &bullet; **podporované verze:** všechny

Odstraní nebo unlists balíčku ze zdroje balíčku. Pro nuget.org, příkazem k odstranění [unlists balíček](../policies/deleting-packages.md).

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
| Neinteraktivní | Potlačí vyzve k zadání uživatele o vstup ani potvrzení. |
| Source | Určuje adresu URL serveru. Adresa URL nuget.org `https://api.nuget.org/v3/index.json`. Pro privátní kanály, nahraďte název hostitele, například *%hostname%/api/v3*. |
| Verbosity | Určuje množství podrobností, na které se zobrazí ve výstupu: *normální*, *quiet*, *podrobné*. |

Viz také [proměnné prostředí](cli-ref-environment-variables.md)

## <a name="examples"></a>Příklady

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
