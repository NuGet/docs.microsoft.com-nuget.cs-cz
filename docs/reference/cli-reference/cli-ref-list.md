---
title: Seznam CLI NuGet – příkaz
description: Reference k příkazu NuGet. exe list
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328324"
---
# <a name="list-command-nuget-cli"></a>list – příkaz (NuGet CLI)

**Platí pro:** spotřeba balíčku, publikování &bullet; **podporovaných verzí:** vše

Zobrazí seznam balíčků z daného zdroje. Pokud nejsou zadány žádné zdroje, budou použity všechny zdroje definované v globálním konfiguračním `%AppData%\NuGet\NuGet.Config` souboru (Windows) `~/.nuget/NuGet/NuGet.Config`nebo. Pokud `NuGet.Config` neurčuje žádné zdroje `list` , použije výchozí kanál (NuGet.org).

## <a name="usage"></a>Použití

```cli
nuget list [search terms] [options]
```

kde volitelné hledané výrazy budou filtrovat zobrazený seznam. Hledané výrazy se aplikují na názvy balíčků, značek a popisů balíčků stejně jako při jejich použití v nuget.org.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| AllVersions | Zobrazí seznam všech verzí balíčku. Ve výchozím nastavení se zobrazí pouze nejnovější verze balíčku. |
| ConfigFile | Konfigurační soubor NuGet, který se má použít Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows `~/.nuget/NuGet/NuGet.Config` ) nebo (Mac/Linux).|
| ForceEnglishOutput | *(3.5 +)* Vynutí, aby soubor NuGet. exe běžel pomocí neutrální jazykové verze určené pro angličtinu. |
| Help | Zobrazí informace o nápovědě k příkazu. |
| IncludeDelisted | *(3.2 +)* Zobrazí neuvedené balíčky. |
| NonInteractive | Potlačí výzvy pro vstup uživatele nebo potvrzení. |
| Předběžné verze | Obsahuje předběžné verze balíčků v seznamu. |
| Source | Určuje seznam zdrojů balíčků, které se mají hledat. |
| Verbosity | Určuje množství podrobností zobrazených ve výstupu: *normální*, tiché a *podrobné*. |

Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .

## <a name="examples"></a>Příklady

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
