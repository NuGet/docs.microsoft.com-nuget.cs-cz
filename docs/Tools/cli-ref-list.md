---
title: Příkaz seznamu NuGet rozhraní příkazového řádku | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referenční dokumentace pro příkaz nuget.exe seznamu
keywords: odkaz na seznam nuget, seznam balíčků příkaz
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 61ad02eb99d6c56968c38841498df8aa9f74159d
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
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
