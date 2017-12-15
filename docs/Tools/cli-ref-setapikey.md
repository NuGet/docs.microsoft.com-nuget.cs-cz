---
title: "Příkaz setapikey NuGet rozhraní příkazového řádku | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: a64c0462-973d-4100-ba3f-8902a2b127f7
description: "Referenční dokumentace pro příkaz setapikey nuget.exe"
keywords: "referenční dokumentace setapikey nuget, setapikey příkaz"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a07c35b8bdd57157391e391e04a90204342b1d5c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
## <a name="setapikey-command-nuget-cli"></a>příkaz setapikey (NuGet CLI)

**Platí pro:** spotřeba balíčku, publikování &bullet; **podporované verze:** všechny

Uloží klíč rozhraní API pro adresu URL daného serveru do `NuGet.Config` tak, aby nemusí být zadaný pro následné příkazy.

## <a name="usage"></a>Použití

```
nuget setapikey <key> -Source <url> [options]
```

kde `<source>` identifikuje server a `<key>` je klíč nebo heslo, abyste uložili. Pokud `<source>` je tento parametr vynechán, předpokládá se nuget.org.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| ConfigFile | *(2.5 +)*  NuGet konfiguračním souboru chcete upravit. Pokud není zadaný, *%AppData%\NuGet\NuGet.Config* se používá. |
| ForceEnglishOutput | *(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze. |
| Nápověda | Zobrazí nápovědu pro příkaz. |
| Neinteraktivní | Potlačí výzvy pro vstup uživatele nebo potvrzení. |
| Podrobnosti | Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné (2.5 +)*. |

Viz také [proměnné prostředí](cli-ref-environment-variables.md)

## <a name="examples"></a>Příklady

```
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
