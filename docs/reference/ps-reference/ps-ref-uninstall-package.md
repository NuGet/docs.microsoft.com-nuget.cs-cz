---
title: Referenční dokumentace prostředí PowerShell pro odinstalaci NuGet
description: Reference k příkazu Uninstall-Package PowerShell v konzole správce balíčků NuGet v aplikaci Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 5c963588d28cab42e5fb6a43b31a17e26e49d0d2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328186"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (konzola Správce balíčků v sadě Visual Studio)

*Toto téma popisuje příkaz v [konzole správce balíčků](../../consume-packages/install-use-packages-powershell.md) v sadě Visual Studio ve Windows. Obecný příkaz pro odinstalaci do PowerShellu najdete v tématu [referenční informace](/powershell/module/packagemanagement/?view=powershell-6)k PowerShellu pro PackageManagement.*

Odebere balíček z projektu, volitelně odebere jeho závislosti. Pokud jsou na tomto balíčku závislé jiné balíčky, příkaz se nezdaří, pokud není zadána možnost – Force.

## <a name="syntax"></a>Syntaxe

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

Pokud jsou na tomto balíčku závislé jiné balíčky, příkaz se nezdaří, pokud není zadána možnost – Force.

## <a name="parameters"></a>Parametry

| Parametr | Popis |
| --- | --- |
| Id | Požadovanou Identifikátor balíčku, který se má odinstalovat Samotný přepínač-ID je nepovinný. |
| Version | Verze balíčku, který se má odinstalovat, se zastaví jako aktuálně nainstalovaná verze. |
| RemoveDependencies | Odinstalujte balíček a jeho nepoužívané závislosti. To znamená, že pokud má nějaká závislost jiný balíček, který na něm závisí, přeskočí se. |
| ProjectName | Projekt, ze kterého má být balíček odinstalován, výchozí nastavení projektu. |
| Ode | Vynutí odinstalaci balíčku, a to i v případě, že na něm závisí jiné balíčky. |
| WhatIf | Ukazuje, co se stane při spuštění příkazu, aniž by se skutečně prováděla odinstalace. |

Žádný z těchto parametrů nepřijímají vstupní ani zástupné znaky kanálu.

## <a name="common-parameters"></a>Společné parametry

`Uninstall-Package`podporuje následující [běžné parametry PowerShellu](http://go.microsoft.com/fwlink/?LinkID=113216): Ladit, Error Action, ErrorVariable, unbuffer, subvariable, PipelineVariable, verbose, WarningAction a WarningVariable.

## <a name="examples"></a>Příklady

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
