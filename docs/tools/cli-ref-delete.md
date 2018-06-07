---
title: Příkaz delete NuGet rozhraní příkazového řádku
description: Referenční dokumentace pro příkaz delete nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: c0f33dd5475521da47972a6f032ac6ea86d98c83
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817175"
---
# <a name="delete-command-nuget-cli"></a>Odstranit příkazu (NuGet CLI)

**Platí pro:** balíček publikování &bullet; **podporované verze:** všechny

Odstraní nebo unlists balíčku ze zdroje balíčku. Pro nuget.org, příkaz delete [unlists balíček](../policies/deleting-packages.md).

## <a name="usage"></a>Použití

```cli
nuget delete <packageID> <packageVersion> [options]
```

kde `<packageID>` a `<packageVersion>` přesný balíček odstranit nebo unlist identifikovat. Přesný postup závisí na zdroji. Pro místní složky, například daný balíček byl odstraněn; balíček není pro nuget.org neuvedené.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| apiKey | Klíč rozhraní API pro cílové úložiště. Pokud není přítomný, použije se verze zadaná v konfiguračním souboru. |
| ConfigFile | Konfigurační soubor NuGet použít. Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.|
| ForceEnglishOutput | *(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze. |
| Nápověda | Zobrazí nápovědu pro příkaz. |
| Neinteraktivní | Potlačí výzvy pro vstup uživatele nebo potvrzení. |
| Zdroj | Určuje adresu URL serveru. Adresa URL nuget.org je `https://api.nuget.org/v3/index.json`. Pro privátní informační kanály, nahraďte název hostitele, například *%hostname%/api/v3*. |
| Podrobnosti | Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*. |

Viz také [proměnné prostředí](cli-ref-environment-variables.md)

## <a name="examples"></a>Příklady

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
