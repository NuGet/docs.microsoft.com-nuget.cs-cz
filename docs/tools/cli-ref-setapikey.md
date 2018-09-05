---
title: Příkaz setapikey NuGet rozhraní příkazového řádku
description: Referenční informace pro příkaz nuget.exe setapikey
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b00e8b1f7a6fda9c1a0c079069fa8ee08a45b419
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549217"
---
# <a name="setapikey-command-nuget-cli"></a>příkaz setapikey (rozhraní příkazového řádku NuGet)

**Platí pro:** využití balíčků, publikováním &bullet; **podporované verze:** všechny

Uloží klíč rozhraní API pro adresu URL daného serveru do `NuGet.Config` tak, že není nutné zadat pro následné příkazy.

## <a name="usage"></a>Použití

```cli
nuget setapikey <key> -Source <url> [options]
```

kde `<source>` identifikuje server a `<key>` je klíč nebo heslo uložte. Pokud `<source>` je vynechána, předpokládá se nuget.org.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| ConfigFile | Konfigurační soubor NuGet použít. Pokud není zadán, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.|
| ForceEnglishOutput | *(3.5 +)*  Vynutí nuget.exe pro spuštění pomocí neutrální, základem je angličtina jazyková verze. |
| Nápověda | Zobrazí nápovědu pro příkaz. |
| Neinteraktivní | Potlačí vyzve k zadání uživatele o vstup ani potvrzení. |
| Podrobnosti | Určuje množství podrobností, na které se zobrazí ve výstupu: *normální*, *quiet*, *podrobné*. |

Viz také [proměnné prostředí](cli-ref-environment-variables.md)

## <a name="examples"></a>Příklady

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
