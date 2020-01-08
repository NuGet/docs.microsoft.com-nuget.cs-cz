---
title: Aktualizace NuGet – Reference k balíčku PowerShell
description: Reference k příkazu Update-Package PowerShell v konzole správce balíčků NuGet v aplikaci Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: e1bff9d4b7391d8be87afa4b8f2fbd51ae922140
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384853"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a>Update-Package (konzola Správce balíčků v sadě Visual Studio)

*K dispozici pouze v rámci [konzoly Správce balíčků NuGet](../../consume-packages/install-use-packages-powershell.md) v sadě Visual Studio ve Windows.*

Aktualizuje balíček a jeho závislosti nebo všechny balíčky v projektu na novější verzi.

## <a name="syntax"></a>Syntaxe

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

V NuGet 2.8 + můžete `Update-Package` použít k downgradování existujícího balíčku v projektu. Například pokud máte nainstalovanou aplikaci Microsoft. AspNet. MVC 5.1.0-RC1, následující příkaz by ho měl downgradovat na 5.0.0:

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Parametry

|  Parametr | Popis |
| --- | --- |
| Id | Identifikátor balíčku, který se má aktualizovat Pokud tento parametr vynecháte, aktualizuje všechny balíčky. Samotný přepínač-ID je nepovinný. |
| IgnoreDependencies | Přeskočí aktualizaci závislostí balíčku. |
| ProjectName | Název projektu obsahujícího balíčky, které se mají aktualizovat – výchozí nastavení pro všechny projekty |
| Version | Verze, která se má použít pro upgrade, ve výchozím nastavení na nejnovější verzi. V NuGet 3.0 + musí být hodnota verze jedna z *nejnižší, nejvyšší, HighestMinor*nebo *HighestPatch* (ekvivalentní k bezpečnému). |
| Odvod | Omezuje upgrady jenom na verze se stejnou hlavní a dílčí verzí jako aktuálně nainstalovaný balíček. |
| Zdroj | Adresa URL nebo cesta ke složce pro zdroj balíčku, který má být prohledán. Cesty k místní složce můžou být absolutní nebo relativní vzhledem k aktuální složce. Pokud tento parametr vynecháte, `Update-Package` prohledá aktuálně vybraný zdroj balíčku. |
| IncludePrerelease | Zahrnuje předběžné verze balíčků pro aktualizace. |
| Přeinstalace | Resintalls balíčky pomocí jejich aktuálně nainstalovaných verzí. Viz [Přeinstalace a aktualizace balíčků](../../consume-packages/reinstalling-and-updating-packages.md). |
| FileConflictAction | Akce, která se má provést, když se zobrazí výzva k přepsání nebo ignorování existujících souborů, na které se odkazuje v projektu Možné hodnoty jsou *overwrite, ignore, None, OverwriteAll*a *IgnoreAll* (3.0 +). |
| DependencyVersion | Verze balíčků závislostí, které se mají použít, což může být jedna z následujících:<br/><ul><li>*Nejnižší* (výchozí): nejnižší verze</li><li>*HighestPatch*: verze, která má nejnižší hlavní, nejnižší podverzi, nejvyšší opravu</li><li>*HighestMinor*: verze s nejnižší hlavní, nejvyšší podverze a nejvyšší opravou</li><li>*Nejvyšší* (výchozí pro balíček Update-Package bez parametrů): nejvyšší verze</li></ul>Výchozí hodnotu můžete nastavit pomocí nastavení [`dependencyVersion`](../nuget-config-file.md#config-section) v souboru `Nuget.Config`. |
| ToHighestPatch | ekvivalent – Safe. |
| ToHighestMinor | Omezuje upgrady jenom na verze se stejnou hlavní verzí jako aktuálně nainstalovaný balíček. |
| WhatIf | Ukazuje, co se stane při spuštění příkazu bez toho, aby se aktualizace skutečně prováděla. |

Žádný z těchto parametrů nepřijímají vstupní ani zástupné znaky kanálu.

### <a name="common-parameters"></a>Společné parametry

`Update-Package` podporuje následující [běžné parametry PowerShellu](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, inbuffer, subvariable, PipelineVariable, verbose, WarningAction a WarningVariable.

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
