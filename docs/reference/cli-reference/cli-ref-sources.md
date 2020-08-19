---
title: NuGet – příkaz zdrojů CLI
description: Referenční informace o příkazu nuget.exech zdrojů
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 73c9cea8200a1ab1937d25a9a611ae7f2a943dba
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622587"
---
# <a name="sources-command-nuget-cli"></a>sources – příkaz (NuGet CLI)

**Platí pro:** spotřeba balíčku, publikování &bullet; **podporovaných verzí:** vše

Spravuje seznam zdrojů nacházejících se v konfiguračním souboru oboru uživatele nebo v zadaném konfiguračním souboru. Konfigurační soubor oboru uživatele se nachází v `%appdata%\NuGet\NuGet.Config` (Windows) a `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).

Všimněte si, že zdrojová adresa URL pro nuget.org je `https://api.nuget.org/v3/index.json` .

## <a name="usage"></a>Využití

```cli
nuget sources <operation> -Name <name> -Source <source>
```

kde `<operation>` je jedna z *seznamů, přidat, odebrat, povolit, zakázat* nebo *aktualizovat*, `<name>` je název zdroje a `<source>` je adresa URL zdroje. V jednom okamžiku můžete pracovat jenom s jedním zdrojem.

## <a name="options"></a>Možnosti

- **`-ConfigFile`**

  Konfigurační soubor NuGet, který se má použít Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows) nebo `~/.nuget/NuGet/NuGet.Config` nebo `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-ForceEnglishOutput`**

  *(3.5 +)* Vynutí spuštění nuget.exe s využitím neutrální jazykové verze založené na angličtině.

- **`-Format`**

  Platí pro `list` akci a může být `Detailed` (výchozí) nebo `Short` .

- **`-?|-help`**

  Zobrazí informace o nápovědě k příkazu.

- **`-Name`**

  Název zdroje

- **`-NonInteractive`**

  Potlačí výzvy pro vstup uživatele nebo potvrzení.

- **`-Password`**

  Určuje heslo pro ověřování ve zdroji.

- **`-src|-Source`**

  Cesta ke zdroji balíčku (ů)

- **`-StorePasswordInClearText`**

  Určuje, že se má uložit heslo v nešifrovaném textu namísto výchozího chování při ukládání šifrovaného formuláře.

- **`-UserName`**

  Určuje uživatelské jméno pro ověřování ve zdroji.

- **`-ValidAuthenticationTypes`**

  Čárkami oddělený seznam platných typů ověřování pro tento zdroj. Ve výchozím nastavení jsou všechny typy ověřování platné. Příklad: `basic,negotiate`.

- **`-Verbosity [normal|quiet|detailed]`**

  Určuje množství podrobností zobrazených ve výstupu: `normal` (výchozí), `quiet` nebo `detailed` .

> [!Note]
> Nezapomeňte přidat "heslo zdrojů" pod stejným uživatelským kontextem, protože nuget.exe se později používá pro přístup ke zdroji balíčku. Heslo bude uloženo v konfiguračním souboru jako šifrované a lze ho dešifrovat pouze v kontextu stejného uživatele, který byl zašifrován. Pokud například použijete sestavovací Server k obnovení balíčků NuGet, heslo musí být šifrované se stejným uživatelem systému Windows, pod kterým bude úloha sestavení serveru spuštěna.

Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .

## <a name="examples"></a>Příklady

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
