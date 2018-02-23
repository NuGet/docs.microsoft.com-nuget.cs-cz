---
title: "Příkaz zdroje NuGet rozhraní příkazového řádku | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenční dokumentace pro nuget.exe zdroje příkaz"
keywords: "nuget zdroje odkazu, zdroje příkaz"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 1e8204f5e1bf712f65d8efb14ca2a4bd802e3f90
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/20/2018
---
# <a name="sources-command-nuget-cli"></a>příkaz zdroje (NuGet CLI)

**Platí pro:** spotřeba balíčku, publikování &bullet; **podporované verze:** všechny

Spravuje seznam zdrojů, na které se nacházejí v oboru konfigurační soubor uživatele nebo v určeném konfiguračním souboru. Konfigurační soubor uživatele rozsah se nachází v `%APPDATA%\NuGet\NuGet.Config` v systému Windows a na `~/.nuget/NuGet.Config` v Mac/Linux.


Všimněte si, že je adresa URL zdroje pro nuget.org `https://api.nuget.org/v3/index.json`.

## <a name="usage"></a>Použití

```cli
nuget sources <operation> -Name <name> -Source <source>
```

kde `<operation>` je jedním z *seznamu, přidat, odebrat, povolit, zakázat,* nebo *aktualizace*, `<name>` je název zdroje, a `<source>` je adresa URL zdroje.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| ConfigFile | Konfigurační soubor NuGet použít. Pokud není zadaný, *%AppData%\NuGet\NuGet.Config* se používá. |
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

nuget source Enable -Source "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
