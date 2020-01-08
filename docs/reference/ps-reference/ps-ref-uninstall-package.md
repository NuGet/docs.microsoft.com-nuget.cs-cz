---
title: Referenční dokumentace prostředí PowerShell pro odinstalaci NuGet
description: Reference k příkazu Uninstall-Package PowerShell v konzole správce balíčků NuGet v aplikaci Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 05b7bf0e8abad0904b9e851ea6b7a5317e74229d
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384412"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (konzola Správce balíčků v sadě Visual Studio)

*Toto téma popisuje příkaz v [konzole správce balíčků](../../consume-packages/install-use-packages-powershell.md) v sadě Visual Studio ve Windows. Obecný příkaz pro odinstalaci do PowerShellu najdete v tématu [referenční informace k PowerShellu pro PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Odebere balíček z projektu, volitelně odebere jeho závislosti. Pokud jsou na tomto balíčku závislé jiné balíčky a není zadán parametr –Force, příkaz se nezdaří.

## <a name="syntax"></a>Syntaxe

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

Pokud jsou na tomto balíčku závislé jiné balíčky a není zadán parametr –Force, příkaz se nezdaří.

## <a name="parameters"></a>Parametry

| Parametr | Popis |
| --- | --- |
| Id | Požadovanou Identifikátor balíčku, který se má odinstalovat Samotný přepínač-ID je nepovinný. |
| Version | Verze balíčku, který se má odinstalovat, se zastaví jako aktuálně nainstalovaná verze. |
| RemoveDependencies | Odinstalujte balíček a jeho nepoužívané závislosti. To znamená, že pokud má nějaká závislost jiný balíček, který na něm závisí, přeskočí se. |
| ProjectName | Projekt, ze kterého má být balíček odinstalován, výchozí nastavení projektu. |
| Force | Vynutí odinstalaci balíčku, a to i v případě, že na něm závisí jiné balíčky. |
| WhatIf | Ukazuje, co se stane při spuštění příkazu, aniž by se skutečně prováděla odinstalace. |

Žádný z těchto parametrů nepřijímají vstupní ani zástupné znaky kanálu.

## <a name="common-parameters"></a>Společné parametry

`Uninstall-Package` podporuje následující [běžné parametry PowerShellu](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, inbuffer, subvariable, PipelineVariable, verbose, WarningAction a WarningVariable.

## <a name="examples"></a>Příklady

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
