---
title: Příkaz NuGet CLI push
description: Odkaz na příkaz nuget.exe push
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 54a09361173ae10040433b05fcfae7304e39452e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779189"
---
# <a name="push-command-nuget-cli"></a>Push – příkaz (NuGet CLI)

**Platí pro:** publikování &bullet; **podporovaných verzí balíčku:** All; 4.1.0 + Required for NuGet.org

> [!Important]
> Pokud chcete nabízet balíčky do nuget.org, musíte použít nuget.exe v 4.1.0 +, která implementuje požadované [protokoly NuGet](../../api/nuget-protocols.md).

Vloží balíček do zdroje balíčku a publikuje ho.

Výchozí konfigurace NuGet se získá načtením `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) a následným načtením všech `Nuget.Config` `.nuget\Nuget.Config` souborů, které začínají z kořene jednotky a končí v aktuálním adresáři (viz [společné konfigurace NuGet](../../consume-packages/configuring-nuget-behavior.md)).

## <a name="usage"></a>Využití

```cli
nuget push <packagePath> [options]
```

kde `<packagePath>` identifikuje balíček, který se má vložit na server.

## <a name="options"></a>Možnosti

- **`-ApiKey`**

  Klíč rozhraní API pro cílové úložiště Pokud není k dispozici, použije se ten, který je zadaný v konfiguračním souboru.

- **`-ConfigFile`**

  Konfigurační soubor NuGet, který se má použít Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows) nebo `~/.nuget/NuGet/NuGet.Config` nebo `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-DisableBuffering`**

  Zakáže ukládání do vyrovnávací paměti při odesílání na server HTTP (s), aby se snížilo využití paměti. Upozornění: při použití této možnosti nemusí fungovat integrované ověřování systému Windows.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Vynutí spuštění nuget.exe s využitím neutrální jazykové verze založené na angličtině.

- **`-?|-help`**

  Zobrazí informace o nápovědě k příkazu.

- **`-NonInteractive`**

  Potlačí výzvy pro vstup uživatele nebo potvrzení.

- **`-NoServiceEndpoint`**

  Nepřipojí `api/v2/packages` se ke zdrojové adrese URL.

- **`-NoSymbols`**

  *(3.5 +)* Pokud balíček symbolů existuje, nebude vložen na server symbolů.

- **`-src|-Source`**

  Určuje adresu URL serveru. NuGet identifikuje zdroj v konvenci UNC nebo místní složky a jednoduše zkopíruje soubor místo vložení pomocí protokolu HTTP.  Kromě toho, počínaje NuGet 3.4.2, se jedná o povinný parametr, pokud `NuGet.Config` soubor neurčuje hodnotu *DefaultPushSource* (viz [Konfigurace chování NuGet](../../consume-packages/configuring-nuget-behavior.md)).

- **`-SkipDuplicate`**

  *(5.1 +)* Pokud balíček a verze již existují, přeskočte je a pokračujte dalším balíčkem v nabízené kopii, pokud nějaká existuje.

- **`-SymbolSource`**

  *(3.5 +)* Určuje adresu URL serveru symbolů; nuget.smbsrc.net se používá při vkládání do nuget.org.

- **`-SymbolApiKey`**

  *(3.5 +)* Určuje klíč rozhraní API pro adresu URL určenou v `-SymbolSource` .

- **`-Timeout`**

  Určuje časový limit pro doručování na server v sekundách. Výchozí hodnota je 300 sekund (5 minut).

- **`-Verbosity [normal|quiet|detailed]`**

  Určuje množství podrobností zobrazených ve výstupu: `normal` (výchozí), `quiet` nebo `detailed` .


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
