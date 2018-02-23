---
title: "Referenční informace prostředí PowerShell odinstalujte balíček NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 06/01/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenční dokumentace pro příkaz prostředí PowerShell odinstalace balíčku v konzole Správce balíčků NuGet v sadě Visual Studio."
keywords: "NuGet konzoly Správce balíčků, příkazy prostředí NuGet Powershell, NuGet Powershell odkaz, odinstalační balíček"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: db7cf9b2282bf40988eee2308c256381c4fd5124
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/20/2018
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Odinstalujte Package (konzola Správce balíčků v sadě Visual Studio)

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
