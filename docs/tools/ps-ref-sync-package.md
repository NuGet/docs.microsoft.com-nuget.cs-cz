---
title: Referenční informace prostředí PowerShell synchronizace balíček NuGet
description: Referenční informace pro příkaz Powershellu synchronizace-Package v konzole Správce balíčků NuGet v sadě Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8119664b1bafe9238b12b1819cc46dc1ee7bdd00
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547991"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a>Sync-Package (konzola Správce balíčků v sadě Visual Studio)

*Verze 3.0 a; k dispozici pouze v rámci [Konzola správce balíčků NuGet](package-manager-console.md) v sadě Visual Studio ve Windows.*

Získá verzi nainstalovaného balíčku ze zadané (nebo výchozí) projektu a synchronizuje na verzi, aby Zbývající projekty v řešení.

## <a name="syntax"></a>Syntaxe

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a>Parametry

| Parametr | Popis |
| --- | --- |
| ID | (Povinné) Identifikátor balíčku, který se synchronizuje. -Id je volitelný přepínač samotný. |
| IgnoreDependencies | Nainstalujte pouze tento balíček a nikoli jeho závislé. |
| ProjectName | Projekt pro synchronizaci balíčku, jako výchozí se použije výchozí projekt. |
| Version | Verze balíčku k synchronizaci, jako výchozí se použije aktuálně nainstalovanou verzi. |
| Zdroj | Cesta URL nebo složku zdroje balíčku. Chcete-li hledat. Cesty k místní složce může být absolutní nebo relativní vzhledem k aktuální složky. Pokud tento parametr vynechán, `Sync-Package` hledá aktuálně vybraném zdroji balíčku. |
| IncludePrerelease | Obsahuje předběžné verze balíčků v synchronizace. |
| FileConflictAction | Akce, který se má provést, když se zobrazí výzva k přepsání nebo ignorovat existující soubory, které jsou odkazované projektem. Možné hodnoty jsou *přepsat, ignorovat, None, OverwriteAll*, a *(3.0 +)* *IgnoreAll*. |
| DependencyVersion | Verze závislé balíčky použití, které může být jedna z následujících akcí:<br/><ul><li>*Nejnižší* (výchozí): nejnižší verze</li><li>*HighestPatch*: verze s nejnižší hlavní, vedlejší nejnižší, nejvyšší oprava</li><li>*HighestMinor*: verze s hlavní nejnižší, nejvyšší podverze, nejvyšší oprava</li><li>*Nejvyšší* (výchozí pro Update-Package bez parametrů): nejvyšší verze</li></ul>Můžete nastavit výchozí hodnotu používanou [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) nastavení `Nuget.Config` souboru. |
| WhatIf | Ukazuje, co by se stalo při spuštění příkazu bez samotnému provedení synchronizace. |

Žádná z těchto parametrů přijímat kanálu vstup nebo zástupné znaky.

## <a name="common-parameters"></a>Společné parametry

`Sync-Package` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction a WarningVariable.

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
