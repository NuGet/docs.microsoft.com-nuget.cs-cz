---
title: Referenční informace prostředí PowerShell NuGet
description: Úplný odkaz na příkazy prostředí PowerShell, které jsou k dispozici v konzoli správce balíčků NuGet v sadě Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 455787d3c8701f5275ace4ed0dcb605213bfbf29
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
---
# <a name="powershell-reference"></a>Referenční informace prostředí PowerShell

Konzola správce balíčků poskytuje rozhraní PowerShell v sadě Visual Studio v systému Windows pro interakci s NuGet prostřednictvím určité příkazy uvedené níže. (Konzole není v současné době k dispozici v sadě Visual Studio for Mac.) Průvodce pomocí konzoly, najdete v článku [Konzola správce balíčků](../tools/package-manager-console.md) tématu.

> [!Tip]
> Všechny příkazy prostředí PowerShell se týkají pouze spotřeba balíčku. Žádné příkazy prostředí PowerShell se vztahují k vytváření a publikování balíčků s výjimkou, pokud balíček může být také příjemce další balíčky.

> [!Important]
> Zde uvedené příkazy jsou specifické pro konzolu Správce balíčků v sadě Visual Studio a liší od [příkazy modulu správy balíčků](/powershell/module/packagemanagement/?view=powershell-6) které jsou k dispozici v obecné prostředí PowerShell. Konkrétně každé prostředí má příkazy, které nejsou k dispozici v dalších a příkazy se stejným názvem, může se také liší v jejich konkrétní argumenty. Pokud používáte konzolu pro správu balíčku v sadě Visual Studio, příkazy a argumenty, které jsou popsané v tomto tématu přítomen použít.

| Běžné příkazy | Popis | Verze NuGet |
| --- | --- | --- |
| [Install-Package](ps-ref-install-package.md) | Nainstaluje do projektu balíček a jeho závislé součásti. | Všechny |
| [Update-Package](ps-ref-update-package.md) | Aktualizuje balíček a jeho závislosti nebo všechny balíčky v projektu. | Všechny |
| [Find-Package](ps-ref-find-package.md) | Vyhledá zdroji balíčku pomocí ID balíčku nebo klíčová slova. | 3.0+ |
| [Get-Package](ps-ref-get-package.md) | Načte seznam balíčků nainstalovaných v místním úložišti, nebo obsahuje seznam balíčků dostupných ze zdroje balíčku. | Všechny |

| Sekundární příkazy | Popis | Verze NuGet |
| --- | --- | --- |
| [Add-BindingRedirect](ps-ref-add-bindingredirect.md) | Hledá ve všech sestaveních ve výstupní cestě pro projekt a přidá přesměrování vazby `app.config` nebo `web.config` potřeby. | Všechny |
| [Get-Project](ps-ref-get-project.md) | Zobrazí informace o výchozí nebo zadaného projektu. | 3.0+ |
| [Open-PackagePage](ps-ref-open-packagepage.md) | Spuštění výchozího prohlížeče s projektu, licence nebo adresy URL sestav zneužití pro zadaný balíček. | Zastaralé v 3.0 + |
| [Registrace TabExpansion](ps-ref-register-tabexpansion.md) | Zaregistruje karta rozšíření pro parametry příkazu, umožňuje vytvářet vlastní rozšíření pro běžně používané parametr hodnoty. | Všechny |
| [Sync-Package](ps-ref-sync-package.md) | Nainstalovaná verze balíčku z Get zadané projektu a synchronizuje ji s ostatními projekty v řešení. | 3.0+ |
| [Uninstall-Package](ps-ref-uninstall-package.md) | Odebere balíček z projektu, případně odebrání jeho závislé součásti. | Všechny |

Pro dokončení, podrobné nápovědu k jakémukoli z těchto příkazů v rámci konzoly stačí spusťte následující s dotyčném název příkazu:

```ps
Get-Help <command> -full
```

Všechny příkazy Konzola správce balíčků podporují následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216):

- Ladit
- ErrorAction
- ErrorVariable
- OutBuffer
- OutVariable
- PipelineVariable
- Verbose
- WarningAction
- WarningVariable

Podrobnosti najdete v části [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) v dokumentaci k prostředí PowerShell.
