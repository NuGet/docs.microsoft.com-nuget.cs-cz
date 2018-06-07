---
title: Příkaz seznamu NuGet rozhraní příkazového řádku
description: Referenční dokumentace pro příkaz nuget.exe seznamu
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b0f144d8abbba7388fe39cd113e4eeddccbca2c6
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818435"
---
# <a name="list-command-nuget-cli"></a>příkaz seznamu (NuGet CLI)

**Platí pro:** spotřeba balíčku, publikování &bullet; **podporované verze:** všechny

Zobrazí seznam balíčků z daného zdroje. Pokud nejsou zadány žádné zdroje, všechny zdroje definované v souboru globální konfiguraci `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config`, se používají. Pokud `NuGet.Config` žádné zdroje, pak určuje `list` používá výchozí informačního kanálu (nuget.org).

## <a name="usage"></a>Použití

```cli
nuget list [search terms] [options]
```

volitelné hledané výrazy, kde bude filtr pro zobrazený seznam. Hledaný text se použijí pro názvy balíčků, značky a popisy balíček stejně, jako jsou v případě, že jejich používání v nuget.org.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| AllVersions | Zobrazí seznam všech verze balíčku. Ve výchozím nastavení se zobrazí jenom nejnovější verzi balíčku. |
| ConfigFile | Konfigurační soubor NuGet použít. Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.|
| ForceEnglishOutput | *(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze. |
| Nápověda | Zobrazí nápovědu pro příkaz. |
| IncludeDelisted | *(3.2 +)*  Zobrazovat neuvedené balíčky. |
| Neinteraktivní | Potlačí výzvy pro vstup uživatele nebo potvrzení. |
| Předběžné verze | Obsahuje předběžné verze balíčků v seznamu. |
| Zdroj | Určuje seznam balíčků zdroje pro vyhledávání. |
| Podrobnosti | Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*. |

Viz také [proměnné prostředí](cli-ref-environment-variables.md)

## <a name="examples"></a>Příklady

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
