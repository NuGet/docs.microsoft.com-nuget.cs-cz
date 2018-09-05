---
title: Referenční informace prostředí PowerShell odinstalujte NuGet-Package
description: Referenční informace pro příkaz Powershellu Uninstall-Package v konzole Správce balíčků NuGet v sadě Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: ae60473fbb716b23f40b0605be8aaa8515802315
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551640"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (konzola Správce balíčků v sadě Visual Studio)

*Toto téma popisuje příkaz v rámci [Konzola správce balíčků NuGet](package-manager-console.md) v sadě Visual Studio ve Windows. Obecný příkaz Powershellu Uninstall-Package, najdete v článku [odkazu modulu Powershellu PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Odebere balíček z projektu, případně odebrání jeho závislostí. Pokud na tento balíček jsou závislé jiné balíčky, příkaz se nezdaří, pokud – Force je zadána možnost.

## <a name="syntax"></a>Syntaxe

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

Pokud na tento balíček jsou závislé jiné balíčky, příkaz se nezdaří, pokud – Force je zadána možnost.

## <a name="parameters"></a>Parametry

| Parametr | Popis |
| --- | --- |
| ID | (Povinné) Identifikátor balíčku, který se odinstalovat. -Id je volitelný přepínač samotný. |
| Version | Verze balíčku k odinstalaci, jako výchozí se použije aktuálně nainstalovanou verzi. |
| RemoveDependencies | Odinstalujte balíček a jeho nepoužité závislé součásti. To znamená pokud má závislost na něm závisí jiný balíček, se přeskočí. |
| ProjectName | Projekt, ze kterého chcete odinstalovat balíček, jako výchozí se použije výchozí projekt. |
| Platnost | Vynutí balíčku tak, že se odinstalují, i v případě, že jsou na ní závislé jiné balíčky. |
| WhatIf | Ukazuje, co by se stalo při spuštění příkazu bez ve skutečnosti provádí odinstalaci. |

Žádná z těchto parametrů přijímat kanálu vstup nebo zástupné znaky.

## <a name="common-parameters"></a>Společné parametry

`Uninstall-Package` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction a WarningVariable.

## <a name="examples"></a>Příklady

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
