---
title: Referenční informace prostředí PowerShell odinstalujte balíček NuGet
description: Referenční dokumentace pro příkaz prostředí PowerShell odinstalace balíčku v konzole Správce balíčků NuGet v sadě Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 860a58c359c9b723564a70f83aee4eee5cebf16d
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818864"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (konzola Správce balíčků v sadě Visual Studio)

*Toto téma popisuje příkaz v rámci [Konzola správce balíčků NuGet](package-manager-console.md) v sadě Visual Studio v systému Windows. Příkaz Obecné odinstalace balíčků prostředí PowerShell najdete v článku [odkaz na prostředí PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Odebere balíček z projektu, případně odebrání jeho závislé součásti. Pokud jsou na tomto balíčku závislé jiné balíčky, příkaz se nezdaří, pokud není zadán parametr – Force.

## <a name="syntax"></a>Syntaxe

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

Pokud jsou na tomto balíčku závislé jiné balíčky, příkaz se nezdaří, pokud není zadán parametr – Force.

## <a name="parameters"></a>Parametry

| Parametr | Popis |
| --- | --- |
| ID | (Povinné) Identifikátor balíček, který chcete odinstalovat. -Id je volitelný přepínač sám sebe. |
| Version | Verze balíčku, které chcete odinstalovat, jako výchozí bude použit aktuálně nainstalované verze. |
| RemoveDependencies | Odinstalujte balíček a jeho nepoužité závislé součásti. To znamená pokud některé závislé na něm závisí jiný balíček, se přeskočí. |
| ProjectName | Projekt, ze kterého pro odinstalaci balíčku, jako výchozí bude použit výchozí projekt. |
| Platnost | Balíček, který se má odinstalovat, vynutí i v případě, že jsou na ní závislé jiné balíčky. |
| WhatIf | Zobrazuje, co by se stalo při spuštění příkazu bez ve skutečnosti provádí odinstalaci. |

Žádná z těchto parametrů přijmout kanálu vstup nebo zástupné znaky.

## <a name="common-parameters"></a>Společné parametry

`Uninstall-Package` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, podrobná, WarningAction a WarningVariable.

## <a name="examples"></a>Příklady

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
