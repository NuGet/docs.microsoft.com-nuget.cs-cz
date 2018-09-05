---
title: Referenční informace prostředí PowerShell pro aktualizaci balíčku NuGet
description: Referenční informace pro příkaz Powershellu Update-Package v konzole Správce balíčků NuGet v sadě Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d47e1978ab7d827e0b8b97cd4e7237019185b50f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546073"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a>Update-Package (konzola Správce balíčků v sadě Visual Studio)

*K dispozici pouze v rámci [Konzola správce balíčků NuGet](package-manager-console.md) v sadě Visual Studio ve Windows.*

Aktualizuje balíček a jeho závislosti nebo všechny balíčky v projektu, na novější verzi.

## <a name="syntax"></a>Syntaxe

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

Ve Správci NuGet 2.8 + `Update-Package` je možné přejít na nižší verzi existujícího balíčku ve vašem projektu. Například pokud máte nainstalovaný 5.1.0-rc1 Microsoft.AspNet.MVC následujícího příkazu by downgradovat ho 5.0.0:

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Parametry

|  Parametr | Popis |
| --- | --- |
| ID | Identifikátor balíčku aktualizace. Pokud tento parametr vynechán, aktualizuje všechny balíčky. -Id je volitelný přepínač samotný. |
| IgnoreDependencies | Přeskočí aktualizace závislosti balíčku. |
| ProjectName | Název projektu, který obsahuje balíčky pro, jako výchozí se použije na všechny projekty. |
| Version | Verze, který se má použít k upgradu, jako výchozí se použije na nejnovější verzi. Ve Správci NuGet 3.0, hodnota verze musí být jeden z *nejnižší, nejvyšší, HighestMinor*, nebo *HighestPatch* (ekvivalentní – bezpečné). |
| Bezpečné | Omezí upgrade na pouze verze se stejnou verzí hlavní a podverze jako nainstalovaný balíček. |
| Zdroj | Cesta URL nebo složku zdroje balíčku. Chcete-li hledat. Cesty k místní složce může být absolutní nebo relativní vzhledem k aktuální složky. Pokud tento parametr vynechán, `Update-Package` hledá aktuálně vybraném zdroji balíčku. |
| IncludePrerelease | Obsahuje předběžné verze balíčků aktualizace. |
| Znovu nainstalujte | Resintalls balíčků pomocí jejich aktuálně nainstalované verze. Zobrazit [Reinstalling a aktualizace balíčků](../consume-packages/reinstalling-and-updating-packages.md). |
| FileConflictAction | Akce, který se má provést, když se zobrazí výzva k přepsání nebo ignorovat existující soubory, které jsou odkazované projektem. Možné hodnoty jsou *přepsat, ignorovat, None, OverwriteAll*, a *IgnoreAll* (3.0 +). |
| DependencyVersion | Verze závislé balíčky použití, které může být jedna z následujících akcí:<br/><ul><li>*Nejnižší* (výchozí): nejnižší verze</li><li>*HighestPatch*: verze s nejnižší hlavní, vedlejší nejnižší, nejvyšší oprava</li><li>*HighestMinor*: verze s hlavní nejnižší, nejvyšší podverze, nejvyšší oprava</li><li>*Nejvyšší* (výchozí pro Update-Package bez parametrů): nejvyšší verze</li></ul>Můžete nastavit výchozí hodnotu používanou [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) nastavení `Nuget.Config` souboru. |
| ToHighestPatch | Omezí upgrade na pouze verze s využitím stejné podverze jako nainstalovaný balíček. |
| ToHighestMinor | Omezí upgrade na pouze verze se stejnou hlavní verzí jako nainstalovaný balíček. |
| WhatIf | Ukazuje, co by se stalo při spuštění příkazu bez samotnému provedení aktualizace. |

Žádná z těchto parametrů přijímat kanálu vstup nebo zástupné znaky.

### <a name="common-parameters"></a>Společné parametry

`Update-Package` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction a WarningVariable.

### <a name="examples"></a>Příklady

```ps
# Updates all packages in every project of the solution
Update-Package

# Updates every package in the MvcApplication1 project
Update-Package -ProjectName MvcApplication1

# Updates the Elmah package in every project to the latest version
Update-Package Elmah

# Updates the Elmah package to version 1.1.0 in every project showing optional -Id usage
Update-Package -Id Elmah -Version 1.1.0

# Updates the Elmah package within the MvcApplication1 project to the highest "safe" version.
# For example, if Elmah version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2,
# and 1.1 are available in the feed, the -Safe parameter updates the package to 1.0.2 instead
# of 1.1 as it would otherwise.
Update-Package Elmah -ProjectName MvcApplication1 -Safe

# Reinstall the same version of the original package, but with the latest version of dependencies
# (subject to version constraints). If this command rolls a dependency back to an earlier version,
# use Update-Package <dependency_name> to reinstall that one dependency without affecting the
# dependent package.
Update-Package ELmah –reinstall 

# Reinstall the Elmah package in just MyProject
Update-Package Elmah -ProjectName MyProject -reinstall

# Reinstall the same version of the original package without touching dependencies.
Update-Package ELmah –reinstall -ignoreDependencies
```
