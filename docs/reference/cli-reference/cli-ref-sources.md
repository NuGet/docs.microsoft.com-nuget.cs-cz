---
title: NuGet – příkaz zdrojů CLI
description: Referenční informace o příkazu NuGet. exe sources
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328282"
---
# <a name="sources-command-nuget-cli"></a>Příkaz sources (NuGet CLI)

**Platí pro:** spotřeba balíčku, publikování &bullet; **podporovaných verzí:** vše

Spravuje seznam zdrojů nacházejících se v konfiguračním souboru oboru uživatele nebo v zadaném konfiguračním souboru. Konfigurační soubor oboru uživatele se nachází v `%appdata%\NuGet\NuGet.Config` (Windows) a `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).

Všimněte si, že zdrojová adresa URL pro `https://api.nuget.org/v3/index.json`NuGet.org je.

## <a name="usage"></a>Použití

```cli
nuget sources <operation> -Name <name> -Source <source>
```

kde `<operation>` je jedna z *seznamů, přidat, odebrat, povolit, zakázat* nebo *aktualizovat*, `<name>` je název zdroje a `<source>` je adresa URL zdroje. V jednom okamžiku můžete pracovat jenom s jedním zdrojem.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| ConfigFile | Konfigurační soubor NuGet, který se má použít Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows `~/.nuget/NuGet/NuGet.Config` ) nebo (Mac/Linux).|
| ForceEnglishOutput | *(3.5 +)* Vynutí, aby soubor NuGet. exe běžel pomocí neutrální jazykové verze určené pro angličtinu. |
| Formát | Platí pro `list` akci a může být `Detailed` (výchozí) nebo `Short`. |
| Help | Zobrazí informace o nápovědě k příkazu. |
| NonInteractive | Potlačí výzvy pro vstup uživatele nebo potvrzení. |
| Heslo | Určuje heslo pro ověřování ve zdroji. |
| StorePasswordInClearText | Určuje, že se má uložit heslo v nešifrovaném textu namísto výchozího chování při ukládání šifrovaného formuláře. |
| UserName | Určuje uživatelské jméno pro ověřování ve zdroji. |
| Verbosity | Určuje množství podrobností zobrazených ve výstupu: *normální*, tiché a *podrobné*. |

> [!Note]
> Nezapomeňte přidat "heslo zdrojů" v rámci stejného uživatelského kontextu, jako je soubor NuGet. exe, se později používá pro přístup ke zdroji balíčku. Heslo bude uloženo v konfiguračním souboru jako šifrované a lze ho dešifrovat pouze v kontextu stejného uživatele, který byl zašifrován. Pokud například použijete sestavovací Server k obnovení balíčků NuGet, heslo musí být šifrované se stejným uživatelem systému Windows, pod kterým bude úloha sestavení serveru spuštěna.

Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .

## <a name="examples"></a>Příklady

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
