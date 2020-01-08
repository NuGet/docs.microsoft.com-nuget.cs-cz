---
title: Referenční dokumentace PowerShellu pro synchronizaci balíčků NuGet
description: Reference k příkazu Sync-Package PowerShell v konzole správce balíčků NuGet v aplikaci Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 12a3d5f32056539a75da9e17b15d67e72a8a42c2
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384900"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a>Sync-Package (konzola Správce balíčků v sadě Visual Studio)

*Verze 3.0 +; k dispozici pouze v rámci [konzoly Správce balíčků](../../consume-packages/install-use-packages-powershell.md) v sadě Visual Studio ve Windows.*

Získá verzi nainstalovaného balíčku z určeného (nebo výchozího) projektu a synchronizuje verzi s ostatními projekty v řešení.

## <a name="syntax"></a>Syntaxe

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a>Parametry

| Parametr | Popis |
| --- | --- |
| Id | Požadovanou Identifikátor balíčku, který se má synchronizovat Samotný přepínač-ID je nepovinný. |
| IgnoreDependencies | Nainstalujte jenom tento balíček a ne jeho závislosti. |
| ProjectName | Projekt, z něhož má být balíček synchronizován, výchozí nastavení projektu. |
| Version | Verze balíčku, který se má synchronizovat, je nastavená verze na aktuálně nainstalovanou verzi. |
| Zdroj | Adresa URL nebo cesta ke složce pro zdroj balíčku, který má být prohledán. Cesty k místní složce můžou být absolutní nebo relativní vzhledem k aktuální složce. Pokud tento parametr vynecháte, `Sync-Package` prohledá aktuálně vybraný zdroj balíčku. |
| IncludePrerelease | Zahrnuje předprodejní balíčky v synchronizaci. |
| FileConflictAction | Akce, která se má provést, když se zobrazí výzva k přepsání nebo ignorování existujících souborů, na které se odkazuje v projektu Možné hodnoty jsou *overwrite, ignore, None, OverwriteAll*a *(3.0 +)* *IgnoreAll*. |
| DependencyVersion | Verze balíčků závislostí, které se mají použít, což může být jedna z následujících:<br/><ul><li>*Nejnižší* (výchozí): nejnižší verze</li><li>*HighestPatch*: verze, která má nejnižší hlavní, nejnižší podverzi, nejvyšší opravu</li><li>*HighestMinor*: verze s nejnižší hlavní, nejvyšší podverze a nejvyšší opravou</li><li>*Nejvyšší* (výchozí pro balíček Update-Package bez parametrů): nejvyšší verze</li></ul>Výchozí hodnotu můžete nastavit pomocí nastavení [`dependencyVersion`](../nuget-config-file.md#config-section) v souboru `Nuget.Config`. |
| WhatIf | Ukazuje, co se stane při spuštění příkazu, aniž by došlo ke skutečnému provedení synchronizace. |

Žádný z těchto parametrů nepřijímají vstupní ani zástupné znaky kanálu.

## <a name="common-parameters"></a>Společné parametry

`Sync-Package` podporuje následující [běžné parametry PowerShellu](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, inbuffer, subvariable, PipelineVariable, verbose, WarningAction a WarningVariable.

## <a name="examples"></a>Příklady

```ps
# Sync the Elmah package installed in the default project into the other projects in the solution
Sync-Package Elmah

# Sync the Elmah package installed in the ClassLibrary1 project into other projects in the solution
Sync-Package Elmah -ProjectName ClassLibrary1

# Sync Microsoft.Aspnet.package but not its dependencies into the other projects in the solution
Sync-Package Microsoft.Aspnet.Mvc -IgnoreDependencies

# Sync jQuery.Validation and install the highest version of jQuery (a dependency) from the package source    
Sync-Package jQuery.Validation -DependencyVersion highest
```
