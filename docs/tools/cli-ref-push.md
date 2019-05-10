---
title: Rozhraní příkazového řádku NuGet nabízených oznámení
description: Referenční informace pro nuget.exe příkazu push
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4a9460944e2c232e2a72195434a491d26eee3559
ms.sourcegitcommit: 3fc93f7a64be040699fe12125977dd25a7948470
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/29/2019
ms.locfileid: "64877961"
---
# <a name="push-command-nuget-cli"></a>příkazu push (rozhraní příkazového řádku NuGet)

**Platí pro:** balíček publikování &bullet; **podporované verze:** všechny; 4.1.0+ vyžadované pro nuget.org

> [!Important]
> Vložit balíčky nuget.org je nutné použít nuget.exe verze 4.1.0 +, která implementuje požadované [NuGet protokoly](../api/nuget-protocols.md).

Odešle balíček ke zdroji balíčku a publikuje ji.

Výchozí konfigurace NuGet se získá načítání `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), pak načítání všechny `Nuget.Config` nebo `.nuget\Nuget.Config` souborů od kořenové jednotky a končící na aktuální adresář (naleznete v tématu [konfigurace Chování Nugetu](../consume-packages/configuring-nuget-behavior.md))

## <a name="usage"></a>Použití

```cli
nuget push <packagePath> [options]
```

kde `<packagePath>` identifikuje balíček nainstalovat do serveru.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| ApiKey | Klíč rozhraní API pro cílového úložiště. Pokud není k dispozici, použije se verze zadaná v konfiguračním souboru. |
| ConfigFile | Konfigurační soubor NuGet použít. Pokud není zadán, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.|
| DisableBuffering | Zakáže ukládání do vyrovnávací paměti při odesílání na server http (s) ke snížení využití paměti. Upozornění: když tuto možnost použít, nemusí fungovat integrované ověřování Windows. |
| ForceEnglishOutput | *(3.5 +)*  Vynutí nuget.exe pro spuštění pomocí neutrální, základem je angličtina jazyková verze. |
| Help | Zobrazí nápovědu pro příkaz. |
| NonInteractive | Potlačí vyzve k zadání uživatele o vstup ani potvrzení. |
| NoSymbols | *(3.5 +)*  Pokud balíček symbolů existuje, neodešle se na server symbolů. |
| Source | Určuje adresu URL serveru. Určuje název UNC nebo místní složku zdroje a jednoduše zkopíruje soubor existuje místo doručením (push) pomocí protokolu HTTP NuGet.  Také, počínaje NuGet 3.4.2, je to povinný parametr Pokud `NuGet.Config` Určuje soubor *DefaultPushSource* hodnotu (naleznete v tématu [konfigurace NuGet chování](../consume-packages/configuring-nuget-behavior.md)). |
| SymbolSource | *(3.5 +)*  Určuje adresu URL serveru symbolů; při odesílání do nuget.org se použije nuget.smbsrc.net |
| SymbolApiKey | *(3.5 +)*  Určuje klíč rozhraní API pro adresu URL zadané v `-SymbolSource`. |
| časový limit | Určuje časový limit v sekundách pro odesílání na server. Výchozí hodnota je 300 sekund (5 minut). |
| Verbosity | Určuje množství podrobností, na které se zobrazí ve výstupu: *normální*, *quiet*, *podrobné*. |

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

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://customsource/
```
