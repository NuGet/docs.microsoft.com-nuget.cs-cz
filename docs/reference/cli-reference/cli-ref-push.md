---
title: Příkaz NuGet CLI push
description: Referenční informace o příkazu NuGet. exe push
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 40b2b2970934bae82c46cbe69156948e90746f97
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328291"
---
# <a name="push-command-nuget-cli"></a>Push – příkaz (NuGet CLI)

**Platí pro:** publikování &bullet; **podporovaných verzí balíčku:** All; 4.1.0 + Required for NuGet.org

> [!Important]
> Pokud chcete nabízet balíčky do nuget.org, musíte použít NuGet. exe v 4.1.0 +, který implementuje požadované [protokoly NuGet](../../api/nuget-protocols.md).

Vloží balíček do zdroje balíčku a publikuje ho.

Výchozí konfigurace NuGet se získá načtením `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) a následným načtením všech `Nuget.Config` `.nuget\Nuget.Config` souborů, které začínají z kořene jednotky a končí v aktuálním adresáři (viz [Common NuGet Konfigurace](../../consume-packages/configuring-nuget-behavior.md))

## <a name="usage"></a>Použití

```cli
nuget push <packagePath> [options]
```

kde `<packagePath>` identifikuje balíček, který se má vložit na server.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| ApiKey | Klíč rozhraní API pro cílové úložiště Pokud není k dispozici, použije se ten, který je zadaný v konfiguračním souboru. |
| ConfigFile | Konfigurační soubor NuGet, který se má použít Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows `~/.nuget/NuGet/NuGet.Config` ) nebo (Mac/Linux).|
| DisableBuffering | Zakáže ukládání do vyrovnávací paměti při odesílání na server HTTP (s), aby se snížilo využití paměti. Upozornění: při použití této možnosti nemusí fungovat integrované ověřování systému Windows. |
| ForceEnglishOutput | *(3.5 +)* Vynutí, aby soubor NuGet. exe běžel pomocí neutrální jazykové verze určené pro angličtinu. |
| Help | Zobrazí informace o nápovědě k příkazu. |
| NonInteractive | Potlačí výzvy pro vstup uživatele nebo potvrzení. |
| Symboly symbolů | *(3.5 +)* Pokud balíček symbolů existuje, nebude vložen na server symbolů. |
| Source | Určuje adresu URL serveru. NuGet identifikuje zdroj v konvenci UNC nebo místní složky a jednoduše zkopíruje soubor místo vložení pomocí protokolu HTTP.  Kromě toho, počínaje NuGet 3.4.2, se jedná o povinný parametr, pokud `NuGet.Config` soubor neurčuje hodnotu *DefaultPushSource* (viz [Konfigurace chování NuGet](../../consume-packages/configuring-nuget-behavior.md)). |
| SkipDuplicate | *(5.1 +)* Pokud balíček a verze již existují, přeskočte je a pokračujte dalším balíčkem v nabízené kopii, pokud nějaká existuje. |
| SymbolSource | *(3.5 +)* Určuje adresu URL serveru symbolů; nuget.smbsrc.net se používá při vkládání do nuget.org. |
| SymbolApiKey | *(3.5 +)* Určuje klíč rozhraní API pro adresu URL určenou v `-SymbolSource`. |
| časový limit | Určuje časový limit pro doručování na server v sekundách. Výchozí hodnota je 300 sekund (5 minut). |
| Verbosity | Určuje množství podrobností zobrazených ve výstupu: *normální*, tiché a *podrobné*. |

Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .

## <a name="examples"></a>Příklady

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://customsource/

:: In the example below -SkipDuplicate will skip pushing the package if package "Foo" version "5.0.2" already exists on NuGet.org
nuget push Foo.5.0.2.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://api.nuget.org/v3/index.json -SkipDuplicate
```
