---
title: Seznam CLI NuGet – příkaz
description: Reference k příkazu NuGet. exe list
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94228521b3be85277990bca2da69518b7070bbdf
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813335"
---
# <a name="list-command-nuget-cli"></a>list – příkaz (NuGet CLI)

**Platí pro:** spotřeba balíčku, publikování &bullet; **podporovaných verzích:** vše

Zobrazí seznam balíčků z daného zdroje. Pokud nejsou zadány žádné zdroje, budou použity všechny zdroje definované v globálním konfiguračním souboru `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config`. Pokud `NuGet.Config` neurčuje žádné zdroje, `list` použije výchozí kanál (nuget.org).

## <a name="usage"></a>Použití

```cli
nuget list [search terms] [options]
```

kde volitelné hledané výrazy budou filtrovat zobrazený seznam. Hledané výrazy se aplikují na názvy balíčků, značek a popisů balíčků stejně jako při jejich použití v nuget.org.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| AllVersions | Zobrazí seznam všech verzí balíčku. Ve výchozím nastavení se zobrazí pouze nejnovější verze balíčku. |
| ConfigFile | Konfigurační soubor NuGet, který se má použít Pokud není zadaný, použije se `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).|
| ForceEnglishOutput | *(3.5 +)* Vynutí, aby soubor NuGet. exe běžel pomocí neutrální jazykové verze určené pro angličtinu. |
| Nápověda | Zobrazí informace o nápovědě k příkazu. |
| IncludeDelisted | *(3.2 +)* Zobrazí neuvedené balíčky. |
| NonInteractive | Potlačí výzvy pro vstup uživatele nebo potvrzení. |
| PreRelease | Obsahuje předběžné verze balíčků v seznamu. |
| Zdroj | Určuje seznam zdrojů balíčků, které se mají hledat. |
| Podrobnosti | Určuje množství podrobností zobrazených ve výstupu: *normální*, *tiché*a *podrobné*. |

Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .

## <a name="examples"></a>Příklady

Vypsat všechny balíčky z nakonfigurovaných informačních kanálů:
```
nuget list
```
Seznamte se s podrobnými podrobnostmi pro balíčky související s Azure:
```
nuget list Azure -Verbosity detailed
```
Vypíše všechny verze balíčků souvisejících s Azure z nakonfigurovaných informačních kanálů:
```
nuget list Azure -AllVersions
```
Vypíše všechny verze balíčků souvisejících s JSON ze zadaného zdroje nebo kanálu:
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
Vypíše balíčky související s JSON z několika zdrojů nebo kanálů:
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```

