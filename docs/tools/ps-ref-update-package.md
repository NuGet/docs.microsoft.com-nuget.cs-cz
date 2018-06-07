---
title: Referenční informace prostředí PowerShell aktualizace balíčku NuGet
description: Referenční dokumentace pro příkaz prostředí PowerShell balíček aktualizace v konzole Správce balíčků NuGet v sadě Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: aa039f3ffcc0a7323178dae846733559c0f689b5
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817096"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a>Update-Package (konzola Správce balíčků v sadě Visual Studio)

*K dispozici pouze v rámci [Konzola správce balíčků NuGet](package-manager-console.md) v sadě Visual Studio v systému Windows.*

Aktualizuje balíček a jeho závislosti nebo všechny balíčky v projektu, na novější verzi.

## <a name="syntax"></a>Syntaxe

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

V NuGet 2.8 + `Update-Package` lze použít na starší verzi existující balíček v projektu. Například pokud máte nainstalovaný 5.1.0-rc1 Microsoft.AspNet.MVC, následující příkaz by přejděte na starší 5.0.0:

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Parametry

|  Parametr | Popis |
| --- | --- |
| ID | Identifikátor balíčku aktualizace. Pokud tento parametr vynechán, aktualizuje všechny balíčky. -Id je volitelný přepínač sám sebe. |
| IgnoreDependencies | Přeskočí aktualizace balíčku závislosti. |
| ProjectName | Název projektu obsahující balíčky aktualizace, jako výchozí bude použit na všechny projekty. |
| Version | Verze se má použít k upgradu, jako výchozí bude použit na nejnovější verzi. V NuGet 3.0 a pozdější verze hodnota musí být jeden z *nejnižší, nejvyšší, HighestMinor*, nebo *HighestPatch* (ekvivalentní - bezpečné). |
| Bezpečné | Omezí upgrade na pouze verze se stejnou hlavní a vedlejší verzi jako s aktuálně nainstalovaným balíčkem. |
| Zdroj | Cestu adresy URL nebo ke složce zdroji balíčků pro vyhledávání. Cesty k místní složce může být absolutní, nebo relativně vzhledem k aktuální složce. Pokud tento parametr vynechán, `Update-Package` hledá aktuálně vybraném zdroji balíčku. |
| IncludePrerelease | Obsahuje předběžné verze balíčků aktualizací. |
| Přeinstalujte | Balíčky Resintalls pomocí jejich aktuálně nainstalované verze. V tématu [Reinstalling a aktualizaci balíčků](../consume-packages/reinstalling-and-updating-packages.md). |
| FileConflictAction | Akce, který se má provést, když se zobrazí výzva k přepsání nebo ignorovat existující soubory, které se odkazuje na projekt. Možné hodnoty jsou *přepsat, ignorovat, None, OverwriteAll*, a *IgnoreAll* (3.0 +). |
| DependencyVersion | Verze závislosti balíčků chcete použít, které může být jedna z následujících akcí:<br/><ul><li>*Nejnižší* (výchozí): nejnižší verze</li><li>*HighestPatch*: oprava nejnižší hlavní, vedlejší nejnižší, nejvyšší verze</li><li>*HighestMinor*: verze se hlavní nejnižší, nejvyšší opravy menších, nejvyšší</li><li>*Nejvyšší* (výchozí nastavení pro balíček aktualizace bez parametrů): nejvyšší verze</li></ul>Můžete nastavit výchozí hodnotu používanou [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) nastavení v `Nuget.Config` souboru. |
| ToHighestPatch | Omezí upgrade na pouze verze vedlejší verzi shodnou s aktuálně nainstalovaným balíčkem. |
| ToHighestMinor | Omezí upgrade na pouze verze se stejnou hlavní verzí jako s aktuálně nainstalovaným balíčkem. |
| WhatIf | Zobrazuje, co by se stalo při spuštění příkazu bez ve skutečnosti provádí aktualizace. |

Žádná z těchto parametrů přijmout kanálu vstup nebo zástupné znaky.

### <a name="common-parameters"></a>Společné parametry

`Update-Package` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, podrobná, WarningAction a WarningVariable.

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
