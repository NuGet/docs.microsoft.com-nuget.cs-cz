---
title: Referenční informace k Powershellu nainstalujte balíček NuGet
description: Referenční informace pro příkaz Powershellu Install-Package v konzole Správce balíčků NuGet v sadě Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 755c87bbc68d3b688c81e16edbc1faabdc9e0520
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842502"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a>Install-Package (konzola Správce balíčků v sadě Visual Studio)

*Toto téma popisuje příkaz v rámci [Konzola správce balíčků](package-manager-console.md) v sadě Visual Studio ve Windows. Obecný příkaz prostředí PowerShell Install-Package, najdete v článku [odkazu modulu Powershellu PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Nainstaluje do projektu balíček a jeho závislosti.

## <a name="syntax"></a>Syntaxe

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

Ve Správci NuGet 2.8 + `Install-Package` můžou provést downgrade existující balíček ve vašem projektu. Například pokud máte nainstalovaný 5.1.0-rc1 Microsoft.AspNet.MVC následujícího příkazu by downgradovat ho 5.0.0:

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Parametry

| Parametr | Popis |
| --- | --- |
| Id | (Povinné) Identifikátor balíčku pro instalaci. (*3.0 +* ) identifikátor může být cesta nebo adresa URL `packages.config` souboru nebo `.nupkg` souboru. -Id je volitelný přepínač samotný. |
| IgnoreDependencies | Nainstalujte pouze tento balíček a nikoli jeho závislé. |
| ProjectName | Projekt, do kterého chcete balíček nainstalovat, jako výchozí se použije výchozí projekt. |
| Source | Cesta URL nebo složku zdroje balíčku. Chcete-li hledat. Cesty k místní složce může být absolutní nebo relativní vzhledem k aktuální složky. Pokud tento parametr vynechán, `Install-Package` hledá aktuálně vybraném zdroji balíčku. |
| Version | Verze balíčku k instalaci, jako výchozí se použije na nejnovější verzi. |
| IncludePrerelease | Bere v úvahu předběžné verze balíčků pro instalaci. Pokud tento parametr vynechán, jsou považovány za pouze stabilní balíčky. |
| FileConflictAction | Akce, který se má provést, když se zobrazí výzva k přepsání nebo ignorovat existující soubory, které jsou odkazované projektem. Možné hodnoty jsou *přepsat, ignorovat, None, OverwriteAll*, a *(3.0 +)* *IgnoreAll*. |
| DependencyVersion | Verze závislé balíčky použití, které může být jedna z následujících akcí:<br/><ul><li>*Nejnižší* (výchozí): nejnižší verze</li><li>*HighestPatch*: verze s nejnižší hlavní, vedlejší nejnižší, nejvyšší oprava</li><li>*HighestMinor*: verze s hlavní nejnižší, nejvyšší podverze, nejvyšší oprava</li><li>*Nejvyšší* (výchozí pro Update-Package bez parametrů): nejvyšší verze</li></ul>Můžete nastavit výchozí hodnotu používanou [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) nastavení `Nuget.Config` souboru. |
| WhatIf | Ukazuje, co by se stalo při spuštění příkazu bez samotnému provedení instalace. |

Žádná z těchto parametrů přijímat kanálu vstup nebo zástupné znaky.

## <a name="common-parameters"></a>Společné parametry

`Install-Package` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction a WarningVariable.

## <a name="examples"></a>Příklady

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
Install-package https://raw.githubusercontent.com/json-ld.net/master/src/JsonLD/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
Install-package https://az320820.vo.msecnd.net/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
