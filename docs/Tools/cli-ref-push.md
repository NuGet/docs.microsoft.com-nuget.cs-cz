---
title: "Příkaz nabízené NuGet rozhraní příkazového řádku | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: a9709eee-add2-47fb-98e6-eec0697087f6
description: "Referenční dokumentace pro příkaz nabízené nuget.exe"
keywords: "referenční dokumentace nabízené nuget, nabízené příkaz"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2828cdc41903d8a948870155b23721724bfa781e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="push-command-nuget-cli"></a>příkaz nabízené (NuGet CLI)

**Platí pro:** balíček publikování &bullet; **podporované verze:** všechny; 4.1.0+ požadované pro nuget.org

> [!Important]
> Pro uložení balíčků do nuget.org je nutné použít nuget.exe v4.1.0 +, která implementuje požadovaná [NuGet protokoly](../api/nuget-protocols.md).

Nabízených oznámení balíček ke zdroji balíčku a vydává je.

NuGet výchozí konfiguraci se získávají načtením `%AppData%\NuGet\NuGet.Config`, pak všechny načítání `Nuget.Config` nebo `.nuget\Nuget.Config` soubory z kořenové složky jednotky počáteční a koncovou v aktuálním adresáři (najdete v části [konfigurace chování NuGet](../consume-packages/configuring-nuget-behavior.md))

## <a name="usage"></a>Použití

```
nuget push <packagePath> [options]
```

kde `<packagePath>` identifikuje balíček k replikaci na server.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| apiKey | Klíč rozhraní API pro cílové úložiště. Pokud není přítomný, ten zadat *%AppData%\NuGet\NuGet.Config* se používá. |
| ConfigFile | *(2.5 +)*  NuGet konfiguračním souboru použít. Pokud není zadaný, *%AppData%\NuGet\NuGet.Config* se používá. |
| DisableBuffering | Zakáže ukládání do vyrovnávací paměti při nabízení do serveru http (s), aby se snížila paměti. Upozornění: Pokud tato možnost se používá, nemusí fungovat integrované ověřování systému Windows. |
| ForceEnglishOutput | *(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze. |
| Nápověda | Zobrazí nápovědu pro příkaz. |
| Neinteraktivní | Potlačí výzvy pro vstup uživatele nebo potvrzení. |
| NoSymbols | *(3.5 +)*  Pokud balíčku symbolů existuje, nebude instaluje na server symbol. |
| Zdroj | Určuje adresu URL serveru. U balíčku NuGet 2.5 + bude NuGet identifikovat UNC nebo místní složky zdroje a jednoduše zkopírovat soubor existuje místo vkládání pomocí protokolu HTTP.  Od verze NuGet 3.4.2, to je taky povinný parametr. Pokud `NuGet.Config` Určuje soubor *DefaultPushSource* hodnotu (najdete v části [konfigurace NuGet chování](../Consume-Packages/Configuring-NuGet-Behavior.md)). |
| SymbolSource | *(3.5 +)*  Určuje adresu URL serveru symbol; nuget.smbsrc.net se používá při nabízení do nuget.org |
| SymbolApiKey | *(3.5 +)*  Určuje klíč rozhraní API pro zadat adresu URL v `-SymbolSource`. |
| Časový limit | Určuje časový limit v sekundách pro vkládání na server. Výchozí hodnota je 300 sekund (5 minut). |
| Podrobnosti | Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné (2.5 +)*. |

Viz také [proměnné prostředí](cli-ref-environment-variables.md)

## <a name="examples"></a>Příklady

```
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://customsource/
```
