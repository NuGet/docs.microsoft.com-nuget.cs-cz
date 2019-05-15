---
title: Rozhraní příkazového řádku NuGet zdrojů příkaz
description: Odkaz nuget.exe zdrojů příkaz
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610619"
---
# <a name="sources-command-nuget-cli"></a>Příkaz sources (NuGet CLI)

**Platí pro:** využití balíčků, publikováním &bullet; **podporované verze:** všechny

Spravuje seznam zdrojů nacházejí v oboru konfigurační soubor uživatele nebo zadaný konfigurační soubor. Konfigurační soubor uživatele oboru se nachází v `%appdata%\NuGet\NuGet.Config` (Windows) a `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).

Všimněte si, že je adresa URL zdroje pro nuget.org `https://api.nuget.org/v3/index.json`.

## <a name="usage"></a>Použití

```cli
nuget sources <operation> -Name <name> -Source <source>
```

kde `<operation>` je jedním z *seznamu, přidávat, odstraňovat, povolit, zakázat,* nebo *aktualizace*, `<name>` je název zdroje, a `<source>` je zdrojové adrese URL. Najednou můžete provozovat na jenom jeden zdroj.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| ConfigFile | Konfigurační soubor NuGet použít. Pokud není zadán, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.|
| ForceEnglishOutput | *(3.5 +)*  Vynutí nuget.exe pro spuštění pomocí neutrální, základem je angličtina jazyková verze. |
| Formát | Platí pro `list` akce a může být `Detailed` (výchozí) nebo `Short`. |
| Help | Zobrazí nápovědu pro příkaz. |
| NonInteractive | Potlačí vyzve k zadání uživatele o vstup ani potvrzení. |
| Heslo | Určuje heslo pro ověřování ve zdroji. |
| StorePasswordInClearText | Označuje, že k uložení hesla v nešifrovaném textu místo výchozí chování ukládání zašifrované podobě. |
| UserName | Určuje uživatelské jméno pro ověřování ve zdroji. |
| Verbosity | Určuje množství podrobností, na které se zobrazí ve výstupu: *normální*, *quiet*, *podrobné*. |

> [!Note]
> Ujistěte se, že přidání hesla se zdroji ve stejném kontextu uživatele, protože nuget.exe se později používá pro přístup ke zdroji balíčku. Heslo bude uložen zašifrovaný v konfiguračním souboru a mohou ho dešifrovat jenom v rámci stejného uživatele jako byl zašifrován. Proto například při použití serveru sestavení pro obnovování balíčků NuGet, které heslo musí být zašifrován pomocí stejného uživatele Windows, ve kterém se spustí úloha serveru sestavení.

Viz také [proměnné prostředí](cli-ref-environment-variables.md)

## <a name="examples"></a>Příklady

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
