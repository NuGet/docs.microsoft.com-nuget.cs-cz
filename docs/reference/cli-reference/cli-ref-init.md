---
title: NuGet – příkaz init CLI
description: Odkaz na příkaz nuget.exe init
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f37572624cea744ce60a9a2e58ad3cbe2696cb9e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780071"
---
# <a name="init-command-nuget-cli"></a>init – příkaz (NuGet CLI)

**Platí pro:** vytváření balíčků &bullet; **podporuje verze:** 3.3 +

Zkopíruje všechny balíčky z ploché složky do cílové složky pomocí hierarchického rozložení, jak je popsáno v [příkazu přidat](cli-ref-add.md). To znamená, že použití `init` je ekvivalentní s použitím `add` příkazu na každém balíčku ve složce.

Stejně jako v nástroji `add` musí být cílem buď místní složka, nebo cesta UNC; Úložiště balíčků HTTP, jako je nuget.org nebo privátní servery, nejsou podporovaná.

## <a name="usage"></a>Využití

```cli
nuget init <source> <destination> [options]
```

kde `<source>` je složka obsahující balíčky a `<destination>` je místní složkou nebo cestou UNC, na kterou jsou balíčky zkopírovány.

## <a name="options"></a>Možnosti

- **`-ConfigFile`**

  Konfigurační soubor NuGet, který se má použít Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows) nebo `~/.nuget/NuGet/NuGet.Config` nebo `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-Expand`**

  Přidá všechny soubory v každém balíčku, který je přidán do zdroje balíčku. totéž jako `-Expand` u `add` příkazu.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Vynutí spuštění nuget.exe s využitím neutrální jazykové verze založené na angličtině.

- **`-?|-help`**

  Zobrazí informace o nápovědě k příkazu.

- **`-NonInteractive`**

  Potlačí výzvy pro vstup uživatele nebo potvrzení.

- **`-Verbosity [normal|quiet|detailed]`**

  Určuje množství podrobností zobrazených ve výstupu: `normal` (výchozí), `quiet` nebo `detailed` .

Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .

## <a name="examples"></a>Příklady

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
