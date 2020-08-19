---
title: NuGet CLI – příkaz setapikey
description: Odkaz na příkaz nuget.exe setapikey
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b84d4257c580f6e734c26ebfc589be27bea10c82
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622808"
---
# <a name="setapikey-command-nuget-cli"></a>setapikey – příkaz (NuGet CLI)

**Platí pro:** spotřeba balíčku, publikování &bullet; **podporovaných verzí:** vše

Uloží klíč rozhraní API pro danou adresu URL serveru `NuGet.Config` tak, aby se nemusel zadat pro následné příkazy.

## <a name="usage"></a>Využití

```cli
nuget setapikey <key> -Source <url> [options]
```

kde `<source>` identifikuje server a `<key>` je klíč, který se má uložit. Pokud `<source>` je hodnota vynechána, předpokládá se NuGet.org. 

> [!NOTE]
> Klíč rozhraní API se nepoužívá pro ověřování pomocí privátního informačního kanálu. Pro správu přihlašovacích údajů pro ověřování ve zdroji použijte [ `nuget sources` příkaz](../cli-reference/cli-ref-sources.md) .
> Klíče rozhraní API lze získat z jednotlivých serverů NuGet. Pokud chcete vytvořit a spravovat APIKeys pro nuget.org, přečtěte si téma [získání-a-API-Key](../../nuget-org/scoped-api-keys.md#acquire-an-api-key) .

## <a name="options"></a>Možnosti

- **`-ConfigFile`**

  Konfigurační soubor NuGet, který se má použít Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows) nebo `~/.nuget/NuGet/NuGet.Config` nebo `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-ForceEnglishOutput`**

  *(3.5 +)* Vynutí spuštění nuget.exe s využitím neutrální jazykové verze založené na angličtině.

- **`-?|-help`**

  Zobrazí informace o nápovědě k příkazu.

- **`-NonInteractive`**

  Potlačí výzvy pro vstup uživatele nebo potvrzení.

- **`-src|-Source`**

  Adresa URL serveru, kde je klíč rozhraní API platný

- **`-Verbosity [normal|quiet|detailed]`**

  Určuje množství podrobností zobrazených ve výstupu: `normal` (výchozí), `quiet` nebo `detailed` .

Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .

## <a name="examples"></a>Příklady

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
