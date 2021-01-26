---
title: Reference k NuGet Get-Package PowerShellu
description: Referenční informace k příkazu Get-Package PowerShellu v konzole správce balíčků NuGet v aplikaci Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8394f888ec3d5e57eacd351a4867173da1070ead
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777498"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>Get-Package (konzola správce balíčků v aplikaci Visual Studio)

*Toto téma popisuje příkaz v [konzole správce balíčků](../../consume-packages/install-use-packages-powershell.md) v sadě Visual Studio ve Windows. Obecný příkaz Get-Package PowerShellu najdete v [referenčních informacích k PowerShellu PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Načte seznam balíčků nainstalovaných v místním úložišti, vypíše balíčky dostupné ze zdroje balíčku při použití s přepínačem-ListAvailable nebo zobrazí seznam dostupných aktualizací, pokud se používá s přepínačem-Update.

## <a name="syntax"></a>Syntax

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

Bez parametrů `Get-Package` zobrazí seznam balíčků nainstalovaných ve výchozím projektu.

## <a name="parameters"></a>Parametry

| Parametr | Popis |
| --- | --- |
| Zdroj | Adresa URL nebo cesta ke složce pro balíček Cesty k místní složce můžou být absolutní nebo relativní vzhledem k aktuální složce. Pokud tento parametr vynecháte, `Get-Package` vyhledá aktuálně vybraný zdroj balíčku. Při použití s-ListAvailable se výchozí hodnoty nuget.org. |
| ListAvailable | Vypíše balíčky dostupné ze zdroje balíčku, přičemž se jako výchozí nuget.org. Zobrazuje výchozí 50 balíčků, pokud nejsou zadány hodnoty-PageSize a/nebo-First. |
| Aktualizace | Vypíše balíčky, které mají k dispozici aktualizaci ze zdroje balíčku. |
| ProjectName | Projekt, ze kterého se mají získat nainstalované balíčky Je-li tento parametr vynechán, vrátí instalované projekty pro celé řešení. |
| Filtrovat | Řetězec filtru, který slouží k zúžení seznamu balíčků jeho použitím na ID, popis a značky balíčku. |
| První | Počet balíčků, které mají být vráceny od začátku seznamu. Pokud není zadaný, použije se výchozí hodnota 50. |
| Přeskočit | Vynechává první celočíselné &lt; &gt; balíčky ze zobrazeného seznamu.  |
| AllVersions | Zobrazí všechny dostupné verze jednotlivých balíčků, nikoli jenom nejnovější verzi. |
| IncludePrerelease | Zahrnuje předběžné verze balíčků ve výsledcích. |
| PageSize | *(3.0 +)* Pokud se při použití s-ListAvailable (povinné), počet balíčků, které se mají zobrazit, před tím, než se zobrazí výzva k pokračování. |

Žádný z těchto parametrů nepřijímají vstupní ani zástupné znaky kanálu.

## <a name="common-parameters"></a>Společné parametry

`Get-Package` podporuje následující [běžné parametry PowerShellu](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, inbuffer, subvariable, PipelineVariable, verbose, WarningAction a WarningVariable.

## <a name="examples"></a>Příklady

```ps
# Lists the packages installed in the current solution
Get-Package

# Lists the packages installed in a project
Get-Package -ProjectName MyProject

# Lists packages available in the current package source
Get-Package -ListAvailable

# Lists 30 packages at a time from the current source, and prompts to continue if more are available
Get-Package -ListAvailable -PageSize 30

# Lists packages with the Ninject keyword in the current source, up to 50
Get-Package -ListAvailable -Filter Ninject

# List all versions of packages matching the filter "jquery"
Get-Package -ListAvailable -Filter jquery -AllVersions

# Lists packages installed in the solution that have available updates
Get-Package -Updates

# Lists packages installed in a specific project that have available updates
Get-Package -Updates -ProjectName MyProject
```