---
title: NuGet – příkaz help CLI
description: Reference k příkazu nuget.exe Help
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5d91638c4a6f167ea8a04e5dfa2905cb55084ddd
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779349"
---
# <a name="help-or--command-nuget-cli"></a>help nebo ? – příkaz (NuGet CLI)

**Platí pro:** všechny &bullet; **podporované verze**: vše

Zobrazí obecné informace o nápovědě a nápovědu k určitým příkazům.

## <a name="usage"></a>Využití

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

WHERE [příkaz] identifikuje konkrétní příkaz, pro který chcete zobrazit nápovědu.

> [!Warning]
> U některých příkazů Nezapomeňte zadat nejprve *help* , jako je `nuget help install` například, protože v NuGet.org je balíček s názvem "Help". Pokud příkaz přiřadíte, nebudete `nuget install help` mít k příkazu install nápovědu, ale místo toho se nainstaluje balíček s názvem Nápověda.

## <a name="options"></a>Možnosti

- **`-All`**

  Vytiskne podrobnou nápovědu pro všechny dostupné příkazy. ignoruje se, pokud je zadaný konkrétní příkaz.

- **`-ConfigFile`**

  Konfigurační soubor NuGet, který se má použít Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows) nebo `~/.nuget/NuGet/NuGet.Config` nebo `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-ForceEnglishOutput`**

  *(3.5 +)* Vynutí spuštění nuget.exe s využitím neutrální jazykové verze založené na angličtině.

- **`-?|-help`**

  Zobrazí informace o nápovědě k příkazu.

- **`-Markdown`**

  Při použití s nástrojem tisknout podrobnou podporu ve formátu Markdownu `-All` V opačném případě ignorována.

- **`-NonInteractive`**

  Potlačí výzvy pro vstup uživatele nebo potvrzení.

- **`-Verbosity [normal|quiet|detailed]`**

  Určuje množství podrobností zobrazených ve výstupu: `normal` (výchozí), `quiet` nebo `detailed` .

Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .

## <a name="examples"></a>Příklady

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
