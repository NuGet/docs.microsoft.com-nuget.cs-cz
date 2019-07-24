---
title: NuGet – příkaz init CLI
description: Referenční informace o příkazu NuGet. exe init
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328336"
---
# <a name="init-command-nuget-cli"></a>init – příkaz (NuGet CLI)

**Platí pro:** vytváření &bullet; balíčků **podporuje verze:** 3.3+

Zkopíruje všechny balíčky z ploché složky do cílové složky pomocí hierarchického rozložení, jak je popsáno v [příkazu přidat](cli-ref-add.md). To znamená, že `init` použití je ekvivalentní s `add` použitím příkazu na každém balíčku ve složce.

Stejně jako `add`v nástroji musí být cílem buď místní složka, nebo cesta UNC; Úložiště balíčků HTTP, jako je nuget.org nebo privátní servery, nejsou podporovaná.

## <a name="usage"></a>Použití

```cli
nuget init <source> <destination> [options]
```

kde `<source>` je složka obsahující balíčky a `<destination>` je místní složkou nebo cestou UNC, na kterou jsou balíčky zkopírovány.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| ConfigFile | Konfigurační soubor NuGet, který se má použít Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows `~/.nuget/NuGet/NuGet.Config` ) nebo (Mac/Linux).|
| ForceEnglishOutput | *(3.5 +)* Vynutí, aby soubor NuGet. exe běžel pomocí neutrální jazykové verze určené pro angličtinu. |
| Expand | Přidá všechny soubory v každém balíčku, který je přidán do zdroje balíčku. totéž jako `-Expand` `add` u příkazu. |
| Help | Zobrazí informace o nápovědě k příkazu. |
| NonInteractive | Potlačí výzvy pro vstup uživatele nebo potvrzení. |
| Verbosity | Určuje množství podrobností zobrazených ve výstupu: *normální*, tiché a *podrobné*. |

Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .

## <a name="examples"></a>Příklady

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
