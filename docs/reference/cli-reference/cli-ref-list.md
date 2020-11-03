---
title: Seznam CLI NuGet – příkaz
description: Referenční informace pro příkaz nuget.exe list
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: a6a4ee434c43ad4865dba12f039b5d545a90d3c4
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238163"
---
# <a name="list-command-nuget-cli"></a>list – příkaz (NuGet CLI)

**Platí pro:** spotřeba balíčku, publikování &bullet; **podporovaných verzí:** vše

Zobrazí seznam balíčků z daného zdroje. Pokud nejsou zadány žádné zdroje, budou použity všechny zdroje definované v globálním konfiguračním souboru `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` . Pokud `NuGet.Config` neurčuje žádné zdroje, `list` použije výchozí kanál (NuGet.org).

## <a name="usage"></a>Využití

```cli
nuget list [search terms] [options]
```

kde volitelné hledané výrazy budou filtrovat zobrazený seznam. [Hledané výrazy](../../consume-packages/finding-and-choosing-packages.md#search-syntax) se aplikují na názvy balíčků, značek a popisů balíčků stejně jako při jejich použití v NuGet.org. 

## <a name="options"></a>Možnosti

- **`-AllVersions`**

  Zobrazí seznam všech verzí balíčku. Ve výchozím nastavení se zobrazí pouze nejnovější verze balíčku.

- **`-ConfigFile`**

  Konfigurační soubor NuGet, který se má použít Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows) nebo `~/.nuget/NuGet/NuGet.Config` nebo `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-ForceEnglishOutput`**

  *(3.5 +)* Vynutí spuštění nuget.exe s využitím neutrální jazykové verze založené na angličtině.

- **`-?|-help`**

  Zobrazí informace o nápovědě k příkazu.

- **`-IncludeDelisted`**

  *(3.2 +)* Zobrazí neuvedené balíčky.

- **`-NonInteractive`**

  Potlačí výzvy pro vstup uživatele nebo potvrzení.

- **`-PreRelease`**

  Obsahuje předběžné verze balíčků v seznamu.

- **`-Source`**

  Určuje seznam zdrojů balíčků, které se mají hledat.

- **`-Verbosity [normal|quiet|detailed]`**

  Určuje množství podrobností zobrazených ve výstupu: `normal` (výchozí), `quiet` nebo `detailed` .

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