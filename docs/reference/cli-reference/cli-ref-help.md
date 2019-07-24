---
title: NuGet – příkaz help CLI
description: Referenční informace o příkazu NuGet. exe help
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328342"
---
# <a name="help-or--command-nuget-cli"></a>help or ? Příkaz (NuGet CLI)

**Platí pro:** všechny &bullet; **podporované verze**: vše

Zobrazí obecné informace o nápovědě a nápovědu k určitým příkazům.

## <a name="usage"></a>Použití

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

WHERE [příkaz] identifikuje konkrétní příkaz, pro který chcete zobrazit nápovědu.

> [!Warning]
> U některých příkazů Nezapomeňte zadat nejprve *help* , jako `nuget help install`je například, protože v NuGet.org je balíček s názvem "Help". Pokud příkaz `nuget install help`přiřadíte, nebudete mít k příkazu install nápovědu, ale místo toho se nainstaluje balíček s názvem Nápověda.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| Všechny | Vytiskne podrobnou nápovědu pro všechny dostupné příkazy. ignoruje se, pokud je zadaný konkrétní příkaz. |
| ConfigFile | Konfigurační soubor NuGet, který se má použít Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows `~/.nuget/NuGet/NuGet.Config` ) nebo (Mac/Linux).|
| ForceEnglishOutput | *(3.5 +)* Vynutí, aby soubor NuGet. exe běžel pomocí neutrální jazykové verze určené pro angličtinu. |
| Help | Zobrazí informace o nápovědě k samotnému příkazu help. |
| Markdown | Při použití s nástrojem `-All`tisknout podrobnou podporu ve formátu Markdownu V opačném případě ignorována. |
| NonInteractive | Potlačí výzvy pro vstup uživatele nebo potvrzení. |
| Verbosity | Určuje množství podrobností zobrazených ve výstupu: *normální*, tiché a *podrobné*. |

Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .

## <a name="examples"></a>Příklady

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
