---
title: "Příkaz nabízené NuGet rozhraní příkazového řádku | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenční dokumentace pro příkaz nabízené nuget.exe"
keywords: "referenční dokumentace nabízené nuget, nabízené příkaz"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 095e81406df3db5fbfc6c5202362894b2c6d7cf8
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2018
---
# <a name="push-command-nuget-cli"></a>příkaz nabízené (NuGet CLI)

**Platí pro:** balíček publikování &bullet; **podporované verze:** všechny; 4.1.0+ požadované pro nuget.org

> [!Important]
> Pro uložení balíčků do nuget.org je nutné použít nuget.exe v4.1.0 +, která implementuje požadovaná [NuGet protokoly](../api/nuget-protocols.md).

Nabízených oznámení balíček ke zdroji balíčku a vydává je.

NuGet výchozí konfiguraci se získávají načtením `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), pak načítání všechny `Nuget.Config` nebo `.nuget\Nuget.Config` soubory z kořenové složky jednotky počáteční a koncovou v aktuálním adresáři (viz [konfigurace Chování NuGet](../consume-packages/configuring-nuget-behavior.md))

## <a name="usage"></a>Použití

```cli
nuget push <packagePath> [options]
```

kde `<packagePath>` identifikuje balíček k replikaci na server.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| ApiKey | Klíč rozhraní API pro cílové úložiště. Pokud není přítomný, použije se verze zadaná v konfiguračním souboru. |
| ConfigFile | Konfigurační soubor NuGet použít. Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.|
| DisableBuffering | Zakáže ukládání do vyrovnávací paměti při nabízení do serveru http (s), aby se snížila paměti. Upozornění: Pokud tato možnost se používá, nemusí fungovat integrované ověřování systému Windows. |
| ForceEnglishOutput | *(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze. |
| Nápověda | Zobrazí nápovědu pro příkaz. |
| Neinteraktivní | Potlačí výzvy pro vstup uživatele nebo potvrzení. |
| NoSymbols | *(3.5 +)*  Pokud balíčku symbolů existuje, nebude instaluje na server symbol. |
| Zdroj | Určuje adresu URL serveru. NuGet identifikuje UNC nebo místní složky zdroje a jednoduše zkopíruje soubor existuje místo vkládání pomocí protokolu HTTP.  Od verze NuGet 3.4.2, to je taky povinný parametr. Pokud `NuGet.Config` Určuje soubor *DefaultPushSource* hodnotu (najdete v části [konfigurace NuGet chování](../consume-packages/configuring-nuget-behavior.md)). |
| SymbolSource | *(3.5 +)*  Určuje adresu URL serveru symbol; nuget.smbsrc.net se používá při nabízení do nuget.org |
| SymbolApiKey | *(3.5 +)*  Určuje klíč rozhraní API pro zadat adresu URL v `-SymbolSource`. |
| Časový limit | Určuje časový limit v sekundách pro vkládání na server. Výchozí hodnota je 300 sekund (5 minut). |
| Podrobnosti | Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*. |

Viz také [proměnné prostředí](cli-ref-environment-variables.md)

## <a name="examples"></a>Příklady

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://customsource/
```
