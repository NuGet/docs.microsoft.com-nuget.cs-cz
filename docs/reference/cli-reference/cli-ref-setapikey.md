---
title: NuGet CLI – příkaz setapikey
description: Referenční informace o příkazu NuGet. exe setapikey
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: e06cfb5b355dfae8104090db7babdecdf9e9fec1
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231224"
---
# <a name="setapikey-command-nuget-cli"></a>setapikey – příkaz (NuGet CLI)

**Platí pro:** spotřeba balíčku, publikování &bullet; **podporovaných verzích:** vše

Uloží klíč rozhraní API pro danou adresu URL serveru do `NuGet.Config`, aby se nemusel zadat pro následné příkazy.

## <a name="usage"></a>Využití

```cli
nuget setapikey <key> -Source <url> [options]
```

kde `<source>` identifikuje server a `<key>` je klíč, který se má uložit. Pokud je hodnota `<source>` vynechána, předpokládá se nuget.org. 

> [!NOTE]
> Klíč rozhraní API se nepoužívá pro ověřování pomocí privátního informačního kanálu. Pokud chcete spravovat přihlašovací údaje pro ověřování ve zdroji, přečtěte si [`nuget sources` příkaz](../cli-reference/cli-ref-sources.md) .
> Klíče rozhraní API lze získat z jednotlivých serverů NuGet. Pokud chcete vytvořit a spravovat APIKeys pro nuget.org, přečtěte si téma [Publishing-API-Key](../../quickstart/includes/publish-api-key.md) .

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| ConfigFile | Konfigurační soubor NuGet, který se má použít Pokud není zadaný, použije se `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).|
| ForceEnglishOutput | *(3.5 +)* Vynutí, aby soubor NuGet. exe běžel pomocí neutrální jazykové verze určené pro angličtinu. |
| Nápověda | Zobrazí informace o nápovědě k příkazu. |
| NonInteractive | Potlačí výzvy pro vstup uživatele nebo potvrzení. |
| Verbosity | Určuje množství podrobností zobrazených ve výstupu: *normální*, *tiché*a *podrobné*. |

Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .

## <a name="examples"></a>Příklady

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
