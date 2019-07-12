---
title: Referenční informace prostředí PowerShell Get balíček NuGet
description: Referenční informace pro příkaz prostředí PowerShell Get-Package v konzole Správce balíčků NuGet v sadě Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d0d25cb6e21f6d0d42389e08340b6f1e1baf8a64
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842506"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>Get-Package (konzola Správce balíčků v sadě Visual Studio)

*Toto téma popisuje příkaz v rámci [Konzola správce balíčků](package-manager-console.md) v sadě Visual Studio ve Windows. Obecný příkaz prostředí PowerShell Get-Package, najdete v článku [odkazu modulu Powershellu PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Načte seznam balíčků nainstalovaných v místním úložišti, zobrazí seznam dostupných balíčků z balíčku zdroje při použití s přepínačem - ListAvailable nebo vypíše dostupné aktualizace při použití s přepínačem - Update.

## <a name="syntax"></a>Syntaxe

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

Bez parametrů `Get-Package` zobrazí seznam balíčků nainstalovaných ve výchozím nastavení projektu.

## <a name="parameters"></a>Parametry

| Parametr | Popis |
| --- | --- |
| Source | Cesta adresy URL nebo složka balíčku. Cesty k místní složce může být absolutní nebo relativní vzhledem k aktuální složky. Pokud tento parametr vynechán, `Get-Package` hledá aktuálně vybraném zdroji balíčku. Při použití s - ListAvailable, výchozí hodnota je nuget.org. |
| ListAvailable | Zobrazí seznam balíčků z balíčku zdroje, jako výchozí se použije na nuget.org. Ukazuje na výchozí hodnotu 50 balíčky jsou určena - PageSize nebo - první. |
| Aktualizace | Zobrazí seznam balíčků, které mají k dispozici aktualizace ze zdroje balíčku. |
| ProjectName | Projekt, ze kterého se mají balíčky nainstalovat. Pokud tento parametr vynechán, vrátí nainstalované projekty pro celé řešení. |
| Filtr | Řetězec filtru sloužící k zúžení seznamu balíčků použitím na ID balíčku, popisu a značkách. |
| první | Počet balíčků vrátit od začátku seznamu. Pokud není zadán, výchozí hodnota je 50. |
| Skip | Vynechá první &lt;int&gt; balíčky ze zobrazeného seznamu.  |
| AllVersions | Zobrazí všechny dostupné verze každého balíčku namísto pouze nejnovější verze. |
| IncludePrerelease | Obsahuje předběžné verze balíčků ve výsledcích. |
| PageSize | *(3.0 +)*  Při použití s - ListAvailable (povinné), počet balíčků do seznamu předtím, než poskytne výzvy a pokračujte. |

Žádná z těchto parametrů přijímat kanálu vstup nebo zástupné znaky.

## <a name="common-parameters"></a>Společné parametry

`Get-Package` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction a WarningVariable.

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
