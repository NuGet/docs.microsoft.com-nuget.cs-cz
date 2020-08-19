---
title: NuGet CLI – příkaz odstranění
description: Odkaz na příkaz nuget.exe DELETE
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: bec1a778d4986a4cb7ee87e1ef8a98550c96ed57
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622860"
---
# <a name="delete-command-nuget-cli"></a>DELETE – příkaz (NuGet CLI)

**Platí pro:** publikování &bullet; **podporovaných verzí balíčku:** vše

Odstraní nebo zruší výpis balíčku ze zdroje balíčku. V případě nuget.org příkaz DELETE [odpíše balíček](../../nuget-org/policies/deleting-packages.md).

## <a name="usage"></a>Využití

```cli
nuget delete <packageID> <packageVersion> [options]
```

kde `<packageID>` a `<packageVersion>` Identifikujte přesný balíček pro odstranění nebo odseznamování. Přesné chování závisí na zdroji. Pro místní složky se například odstraní balíček. pro nuget.org balíček není v seznamu.

## <a name="options"></a>Možnosti

- **`-ApiKey`**

  Klíč rozhraní API pro cílové úložiště Pokud není k dispozici, použije se ten, který je zadaný v konfiguračním souboru.

- **`-ConfigFile`**

  Konfigurační soubor NuGet, který se má použít Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows) nebo `~/.nuget/NuGet/NuGet.Config` nebo `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-ForceEnglishOutput`**

  *(3.5 +)* Vynutí spuštění nuget.exe s využitím neutrální jazykové verze založené na angličtině.

- **`-?|-help`**

  Zobrazí informace o nápovědě k příkazu.

- **`-NonInteractive`**

  Potlačí výzvy pro vstup uživatele nebo potvrzení.

 - **`-np|-NoPrompt`**

   Nedotazovat se při odstraňování

 - **`-NoServiceEndpoint`** Nepřipojí k zdrojové adrese URL rozhraní API/v2/Packages.

- **`-src|-Source`**

  Určuje adresu URL serveru. Adresa URL pro nuget.org je `https://api.nuget.org/v3/index.json` . V případě privátních informačních kanálů nahraďte název hostitele, například *% hostname%/API/V3*.

- **`-Verbosity [normal|quiet|detailed]`**

  Určuje množství podrobností zobrazených ve výstupu: `normal` (výchozí), `quiet` nebo `detailed` .

Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .

## <a name="examples"></a>Příklady

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
