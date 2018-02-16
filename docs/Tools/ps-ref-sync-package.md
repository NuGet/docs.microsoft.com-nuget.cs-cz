---
title: "Referenční informace prostředí PowerShell synchronizace balíček NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenční dokumentace pro příkaz prostředí PowerShell synchronizace balíčku v konzole Správce balíčků NuGet v sadě Visual Studio."
keywords: "NuGet konzoly Správce balíčků, příkazy prostředí NuGet Powershell, NuGet Powershell odkaz, synchronizace balíčku"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8e4b627cff01a353440c47883b98cd93f9edd6cb
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/14/2018
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a>Synchronizace Package (konzola Správce balíčků v sadě Visual Studio)

*Verze 3.0 +; k dispozici pouze v rámci [Konzola správce balíčků NuGet](package-manager-console.md) v sadě Visual Studio v systému Windows.*

Získá verzi instalovaného balíčku z zadané (nebo výchozí) projektu a synchronizuje ji s ostatními projekty v řešení.

## <a name="syntax"></a>Syntaxe

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a>Parametry

| Parametr | Popis |
| --- | --- |
| ID | (Povinné) Identifikátor balíček, který chcete synchronizovat. -Id je volitelný přepínač sám sebe. |
| IgnoreDependencies | Nainstalujte pouze tento balíček a bez jeho závislých součástí. |
| ProjectName | Projekt pro synchronizaci balíčku, jako výchozí bude použit výchozí projekt. |
| Version | Verze balíčku k synchronizaci, jako výchozí bude použit aktuálně nainstalované verze. |
| Zdroj | Cestu adresy URL nebo ke složce zdroji balíčků pro vyhledávání. Cesty k místní složce může být absolutní, nebo relativně vzhledem k aktuální složce. Pokud tento parametr vynechán, `Sync-Package` hledá aktuálně vybraném zdroji balíčku. |
| IncludePrerelease | Obsahuje předběžné verze balíčků v synchronizace. |
| FileConflictAction | Akce, který se má provést, když se zobrazí výzva k přepsání nebo ignorovat existující soubory, které se odkazuje na projekt. Možné hodnoty jsou *přepsat, ignorovat, None, OverwriteAll*, a *(3.0 +)* *IgnoreAll*. |
| DependencyVersion | Verze závislosti balíčků chcete použít, které může být jedna z následujících akcí:<br/><ul><li>*Nejnižší* (výchozí): nejnižší verze</li><li>*HighestPatch*: oprava nejnižší hlavní, vedlejší nejnižší, nejvyšší verze</li><li>*HighestMinor*: verze se hlavní nejnižší, nejvyšší opravy menších, nejvyšší</li><li>*Nejvyšší* (výchozí nastavení pro balíček aktualizace bez parametrů): nejvyšší verze</li></ul>Můžete nastavit výchozí hodnotu používanou [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) nastavení v `Nuget.Config` souboru. |
| WhatIf | Zobrazuje, co by se stalo při spuštění příkazu bez ve skutečnosti provádí synchronizaci. |

Žádná z těchto parametrů přijmout kanálu vstup nebo zástupné znaky.

## <a name="common-parameters"></a>Společné parametry

`Sync-Package` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, podrobná, WarningAction a WarningVariable.

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
