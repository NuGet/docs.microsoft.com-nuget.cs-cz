---
title: Příkaz zdroje NuGet rozhraní příkazového řádku
description: Referenční dokumentace pro nuget.exe zdroje příkaz
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7c416d92c11328ecb020154981b0ddcc5ba9c5e8
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818344"
---
# <a name="sources-command-nuget-cli"></a>Příkaz sources (NuGet CLI)

**Platí pro:** spotřeba balíčku, publikování &bullet; **podporované verze:** všechny

Spravuje seznam zdrojů, na které se nacházejí v oboru konfigurační soubor uživatele nebo v určeném konfiguračním souboru. Konfigurační soubor uživatele rozsah se nachází v `%appdata%\NuGet\NuGet.Config` (Windows) a `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).

Všimněte si, že je adresa URL zdroje pro nuget.org `https://api.nuget.org/v3/index.json`.

## <a name="usage"></a>Použití

```cli
nuget sources <operation> -Name <name> -Source <source>
```

kde `<operation>` je jedním z *seznamu, přidat, odebrat, povolit, zakázat,* nebo *aktualizace*, `<name>` je název zdroje, a `<source>` je adresa URL zdroje.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| ConfigFile | Konfigurační soubor NuGet použít. Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.|
| ForceEnglishOutput | *(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze. |
| Formát | Platí pro `list` akce a může být `Detailed` (výchozí) nebo `Short`. |
| Nápověda | Zobrazí nápovědu pro příkaz. |
| Neinteraktivní | Potlačí výzvy pro vstup uživatele nebo potvrzení. |
| Heslo | Určuje heslo pro ověřování se zdrojem. |
| StorePasswordInClearText | Označuje uložit heslo v nezašifrované text namísto výchozího chování ukládání šifrovaném formátu. |
| UserName | Určuje uživatelské jméno pro ověřování se zdrojem. |
| Podrobnosti | Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*. |

> [!Note]
> Nezapomeňte přidat heslo u zdrojů ve stejném kontextu uživatele, jako nuget.exe se později používá pro přístup ke zdroji balíčku. Heslo se uloží zašifrované v konfiguračním souboru a mohou ho dešifrovat jenom v kontextu stejného uživatele jako byla zašifrovaná. Takže například při použití sestavení serveru pro obnovení balíčků NuGet, které heslo musí být šifrovaný se stejným uživatelem systému Windows, ve kterém se spustí úlohu serveru sestavení.

Viz také [proměnné prostředí](cli-ref-environment-variables.md)

## <a name="examples"></a>Příklady

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
