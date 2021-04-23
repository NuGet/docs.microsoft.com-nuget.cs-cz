---
title: Reference k NuGet Uninstall-Package PowerShellu
description: Referenční informace k příkazu Uninstall-Package PowerShellu v konzole správce balíčků NuGet v aplikaci Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 371e95c341efbce1c4a15facefc15cd51b266141
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901782"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (konzola správce balíčků v aplikaci Visual Studio)

*Toto téma popisuje příkaz v [konzole správce balíčků](../../consume-packages/install-use-packages-powershell.md) v sadě Visual Studio ve Windows. Obecný příkaz Uninstall-Package PowerShellu najdete v [referenčních informacích k PowerShellu PackageManagement](/powershell/module/packagemanagement).*

Odebere balíček z projektu, volitelně odebere jeho závislosti. Pokud jsou na tomto balíčku závislé jiné balíčky, příkaz se nezdaří, pokud není zadána možnost – Force.

## <a name="syntax"></a>Syntax

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

Pokud jsou na tomto balíčku závislé jiné balíčky, příkaz se nezdaří, pokud není zadána možnost – Force.

## <a name="parameters"></a>Parametry

| Parametr | Popis |
| --- | --- |
| Id | Požadovanou Identifikátor balíčku, který se má odinstalovat Samotný přepínač-ID je nepovinný. |
| Verze | Verze balíčku, který se má odinstalovat, se zastaví jako aktuálně nainstalovaná verze. |
| RemoveDependencies | Odinstalujte balíček a jeho nepoužívané závislosti. To znamená, že pokud má nějaká závislost jiný balíček, který na něm závisí, přeskočí se. |
| ProjectName | Projekt, ze kterého má být balíček odinstalován, výchozí nastavení projektu. |
| Force | Vynutí odinstalaci balíčku, a to i v případě, že na něm závisí jiné balíčky. |
| WhatIf | Ukazuje, co se stane při spuštění příkazu, aniž by se skutečně prováděla odinstalace. |

Žádný z těchto parametrů nepřijímají vstupní ani zástupné znaky kanálu.

## <a name="common-parameters"></a>Společné parametry

`Uninstall-Package` podporuje následující [běžné parametry PowerShellu](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, inbuffer, subvariable, PipelineVariable, verbose, WarningAction a WarningVariable.

## <a name="examples"></a>Příklady

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```