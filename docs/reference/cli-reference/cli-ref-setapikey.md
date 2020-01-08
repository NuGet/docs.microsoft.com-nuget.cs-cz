---
title: NuGet CLI – příkaz setapikey
description: Referenční informace o příkazu NuGet. exe setapikey
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0e2119953e6d07cd3571f156fa0b2665de49f963
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383966"
---
# <a name="setapikey-command-nuget-cli"></a>setapikey – příkaz (NuGet CLI)

**Platí pro:** spotřeba balíčku, publikování &bullet; **podporovaných verzích:** vše

Uloží klíč rozhraní API pro danou adresu URL serveru do `NuGet.Config`, aby se nemusel zadat pro následné příkazy.

## <a name="usage"></a>Použití

```cli
nuget setapikey <key> -Source <url> [options]
```

kde `<source>` identifikuje server a `<key>` je klíč nebo heslo, které se má uložit. Pokud je hodnota `<source>` vynechána, předpokládá se nuget.org.

> [!NOTE]
> Klíč rozhraní API se nepoužívá pro ověřování pomocí privátního informačního kanálu. Pokud chcete spravovat přihlašovací údaje pro ověřování ve zdroji, přečtěte si [`nuget sources` příkaz](../cli-reference/cli-ref-sources.md) .

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| ConfigFile | Konfigurační soubor NuGet, který se má použít Pokud není zadaný, použije se `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).|
| ForceEnglishOutput | *(3.5 +)* Vynutí, aby soubor NuGet. exe běžel pomocí neutrální jazykové verze určené pro angličtinu. |
| Nápověda | Zobrazí informace o nápovědě k příkazu. |
| NonInteractive | Potlačí výzvy pro vstup uživatele nebo potvrzení. |
| Podrobnosti | Určuje množství podrobností zobrazených ve výstupu: *normální*, *tiché*a *podrobné*. |

Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .

## <a name="examples"></a>Příklady

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
