---
title: Reference k prostředí PowerShell NuGet
description: Úplný odkaz na příkazy prostředí PowerShell, který je k dispozici v konzole správce balíčků NuGet v aplikaci Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 7bc0395a98e75fe006e048b91d84cb5c17220161
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901886"
---
# <a name="powershell-reference"></a>Referenční informace prostředí

Konzola správce balíčků poskytuje rozhraní PowerShellu v sadě Visual Studio ve Windows pro interakci s nástrojem NuGet přes konkrétní příkazy uvedené níže. (Konzola není v Visual Studio pro Mac v současnosti dostupná.) Průvodce pro používání konzoly najdete v tématu [instalace a Správa balíčků pomocí tématu konzoly Správce balíčků](../consume-packages/install-use-packages-powershell.md) .

> [!Tip]
> Všechny příkazy prostředí PowerShell se týkají pouze spotřeby balíčku. Žádné příkazy PowerShellu nesouvisí s vytvářením a publikováním balíčků s výjimkou toho, že balíček může být také příjemcem jiných balíčků.

> [!Important]
> Níže uvedené příkazy jsou specifické pro konzolu Správce balíčků v aplikaci Visual Studio a liší se od [příkazů modulu Správa balíčků](/powershell/module/packagemanagement) , které jsou k dispozici v obecném prostředí PowerShell. Konkrétně každé prostředí obsahuje příkazy, které nejsou k dispozici v druhém a příkazy se stejným názvem se mohou v jejich specifických argumentech také lišit. Při použití konzoly Správa balíčků v aplikaci Visual Studio platí příkazy a argumenty popsané v tomto stávajícím tématu.

| Běžné příkazy | Description | Verze NuGet |
| --- | --- | --- |
| [Install-Package](ps-reference/ps-ref-install-package.md) | Nainstaluje balíček a jeho závislosti do projektu. | Vše |
| [Update-Package](ps-reference/ps-ref-update-package.md) | Aktualizuje balíček a jeho závislosti nebo všechny balíčky v projektu. | Vše |
| [Find-Package](ps-reference/ps-ref-find-package.md) | Vyhledá zdroj balíčku pomocí ID balíčku nebo klíčových slov. | 3.0 + |
| [Get-Package](ps-reference/ps-ref-get-package.md) | Načte seznam balíčků nainstalovaných v místním úložišti nebo vypíše balíčky dostupné ze zdroje balíčku. | Vše |

| Sekundární příkazy | Description | Verze NuGet |
| --- | --- | --- |
| [Add-BindingRedirect](ps-reference/ps-ref-add-bindingredirect.md) | Prověřuje všechna sestavení v rámci výstupní cesty pro projekt a přidá přesměrování vazby do `app.config` nebo v `web.config` případě potřeby. | Vše |
| [Get-Project](ps-reference/ps-ref-get-project.md) | Zobrazí informace o výchozím nebo zadaném projektu. | 3.0 + |
| [Open-PackagePage](ps-reference/ps-ref-open-packagepage.md) | Spustí výchozí prohlížeč s adresou URL projektu, licence nebo sestavy pro zneužití zadaného balíčku. | Zastaralé v 3.0 + |
| [Registrovat – TabExpansion](ps-reference/ps-ref-register-tabexpansion.md) | Registruje rozšíření karet pro parametry příkazu, což vám umožní vytvořit přizpůsobené rozšíření pro běžně používané hodnoty parametrů. | Vše |
| [Sync-Package](ps-reference/ps-ref-sync-package.md) | Získat verzi nainstalovaného balíčku ze zadaného projektu a synchronizovat verzi s ostatními projekty v řešení. | 3.0 + |
| [Uninstall-Package](ps-reference/ps-ref-uninstall-package.md) | Odebere balíček z projektu, volitelně odebere jeho závislosti. | Vše |

Pro úplnou a podrobnou nápovědu k některým z těchto příkazů v konzole nástroje stačí spustit následující s názvem příkazu:

```ps
Get-Help <command> -full
```

Všechny příkazy konzoly Správce balíčků podporují tyto [běžné parametry PowerShellu](/powershell/module/microsoft.powershell.core/about/about_commonparameters):

- Ladění
- ErrorAction
- ErrorVariable
- OutBuffer
- OutVariable
- PipelineVariable
- Verbose
- WarningAction
- WarningVariable

Podrobnosti najdete v dokumentaci k prostředí PowerShell v tématu [about_CommonParameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters) .