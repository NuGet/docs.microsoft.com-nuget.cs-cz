---
title: NuGet CLI – příkaz odstranění
description: Referenční informace o příkazu NuGet. exe DELETE
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5185bc8b89f645a0a0f4d3241b5fa04e09560ede
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328354"
---
# <a name="delete-command-nuget-cli"></a>DELETE – příkaz (NuGet CLI)

**Platí pro:** publikování &bullet; **podporovaných verzí balíčku:** vše

Odstraní nebo zruší výpis balíčku ze zdroje balíčku. V případě nuget.org příkaz DELETE [odpíše balíček](../../nuget-org/policies/deleting-packages.md).

## <a name="usage"></a>Použití

```cli
nuget delete <packageID> <packageVersion> [options]
```

kde `<packageID>` a`<packageVersion>` Identifikujte přesný balíček pro odstranění nebo odseznamování. Přesné chování závisí na zdroji. Pro místní složky se například odstraní balíček. pro nuget.org balíček není v seznamu.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| ApiKey | Klíč rozhraní API pro cílové úložiště Pokud není k dispozici, použije se ten, který je zadaný v konfiguračním souboru. |
| ConfigFile | Konfigurační soubor NuGet, který se má použít Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows `~/.nuget/NuGet/NuGet.Config` ) nebo (Mac/Linux).|
| ForceEnglishOutput | *(3.5 +)* Vynutí, aby soubor NuGet. exe běžel pomocí neutrální jazykové verze určené pro angličtinu. |
| Help | Zobrazí informace o nápovědě k příkazu. |
| NonInteractive | Potlačí výzvy pro vstup uživatele nebo potvrzení. |
| Source | Určuje adresu URL serveru. Adresa URL pro nuget.org je `https://api.nuget.org/v3/index.json`. V případě privátních informačních kanálů nahraďte název hostitele, například *% hostname%/API/V3*. |
| Verbosity | Určuje množství podrobností zobrazených ve výstupu: *normální*, tiché a *podrobné*. |

Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .

## <a name="examples"></a>Příklady

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
