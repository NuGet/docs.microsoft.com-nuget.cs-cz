---
title: Reference k NuGet Install-Package PowerShellu
description: Referenční informace k příkazu Install-Package PowerShellu v konzole správce balíčků NuGet v aplikaci Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: ad551b8701cfc2061f7721fb050ed9b5a4fede32
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901691"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a>Install-Package (konzola správce balíčků v aplikaci Visual Studio)

*Toto téma popisuje příkaz v [konzole správce balíčků](../../consume-packages/install-use-packages-powershell.md) v sadě Visual Studio ve Windows. Obecný příkaz Install-Package PowerShellu najdete v [referenčních informacích k PowerShellu PackageManagement](/powershell/module/packagemanagement).*

Nainstaluje balíček a jeho závislosti do projektu.

## <a name="syntax"></a>Syntax

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

V NuGet 2.8 + `Install-Package` může downgradovat existující balíček v projektu. Například pokud máte nainstalovanou aplikaci Microsoft. AspNet. MVC 5.1.0-RC1, následující příkaz by ho měl downgradovat na 5.0.0:

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Parametry

| Parametr | Popis |
| --- | --- |
| Id | Požadovanou Identifikátor balíčku, který se má nainstalovat (*3.0 +*) Identifikátor může být cesta nebo adresa URL `packages.config` souboru nebo `.nupkg` souboru. Samotný přepínač-ID je nepovinný. |
| IgnoreDependencies | Nainstalujte jenom tento balíček a ne jeho závislosti. |
| ProjectName | Projekt, do kterého má být balíček nainstalován, je nastaven výchozí projekt. |
| Zdroj | Adresa URL nebo cesta ke složce pro zdroj balíčku, který má být prohledán. Cesty k místní složce můžou být absolutní nebo relativní vzhledem k aktuální složce. Pokud tento parametr vynecháte, `Install-Package` vyhledá aktuálně vybraný zdroj balíčku. |
| Verze | Verze balíčku, který se má nainstalovat, ve výchozím nastavení na nejnovější verzi |
| IncludePrerelease | Bere v úvahu předběžné verze balíčků pro instalaci. Pokud tento parametr vynecháte, budou se brát v úvahu jenom stabilní balíčky. |
| FileConflictAction | Akce, která se má provést, když se zobrazí výzva k přepsání nebo ignorování existujících souborů, na které se odkazuje v projektu Možné hodnoty jsou *overwrite, ignore, None, OverwriteAll* a *(3.0 +)* *IgnoreAll*. |
| DependencyVersion | Verze balíčků závislostí, které se mají použít, což může být jedna z následujících:<br/><ul><li>*Nejnižší* (výchozí): nejnižší verze</li><li>*HighestPatch*: verze, která má nejnižší hlavní, nejnižší podverzi, nejvyšší opravu</li><li>*HighestMinor*: verze s nejnižší hlavní, nejvyšší podverze a nejvyšší opravou</li><li>*Nejvyšší* (výchozí pro Update-Package bez parametrů): nejvyšší verze</li></ul>Výchozí hodnotu můžete nastavit pomocí [`dependencyVersion`](../nuget-config-file.md#config-section) nastavení v `Nuget.Config` souboru. |
| WhatIf | Ukazuje, co se stane při spuštění příkazu, aniž by bylo nutné instalaci skutečně provést. |

Žádný z těchto parametrů nepřijímají vstupní ani zástupné znaky kanálu.

## <a name="common-parameters"></a>Společné parametry

`Install-Package` podporuje následující [běžné parametry PowerShellu](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, inbuffer, subvariable, PipelineVariable, verbose, WarningAction a WarningVariable.

## <a name="examples"></a>Příklady

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
# Note: the URL must end with "packages.config"
Install-Package https://raw.githubusercontent.com/linked-data-dotnet/json-ld.net/master/.nuget/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-Package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
# Note: the URL must end with ".nupkg"
Install-Package https://globalcdn.nuget.org/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```