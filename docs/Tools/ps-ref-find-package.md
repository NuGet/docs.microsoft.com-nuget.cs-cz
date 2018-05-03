---
title: Referenční informace prostředí PowerShell najít balíček NuGet
description: Referenční dokumentace pro příkaz prostředí PowerShell najít balíčku v konzole Správce balíčků NuGet v sadě Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 0faf5c5cf9ae99105e3d76a4f5e37f164c4f4ff3
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Najít Package (konzola Správce balíčků v sadě Visual Studio)

*Verze 3.0 +; Toto téma popisuje příkaz v rámci [Konzola správce balíčků NuGet](package-manager-console.md) v sadě Visual Studio v systému Windows. Příkaz Obecné najít balíčků prostředí PowerShell najdete v článku [odkaz na prostředí PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Získá ze zdroje balíčků sadu vzdálených balíčků se zadané ID nebo klíčová slova.

## <a name="syntax"></a>Syntaxe

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>Parametry

| Parametr | Popis |
| --- | --- |
| ID &lt;klíčová slova&gt; | (Povinné) Klíčová slova pro hledání zdroji balíčku. Pomocí - ExactMatch vrátit pouze balíčky, jehož ID balíčku odpovídá klíčová slova. Je-li zadána žádná klíčová slova `Find-Package` vrátí seznam balíčků prvních 20 počítačů podle stahování nebo číslo určeného - nejdřív. Všimněte si, že - Id je volitelné a žádná operace. |
| Zdroj | Cestu adresy URL nebo ke složce zdroji balíčků pro vyhledávání. Cesty k místní složce může být absolutní, nebo relativně vzhledem k aktuální složce. Pokud tento parametr vynechán, `Find-Package` hledá aktuálně vybraném zdroji balíčku. |
| AllVersions | Zobrazí všechny dostupné verze jednotlivých balíčků místo pouze nejnovější verzi. |
| první | Počet balíčků, které mají být vráceny od začátku seznamu; Výchozí hodnota je 20. |
| Skip | Vynechá první &lt;int&gt; balíčky ze seznamu zobrazených.  |
| IncludePrerelease | Obsahuje předběžné verze balíčků ve výsledcích. |
| ExactMatch | Zadaný používat &lt;klíčová slova&gt; jako ID malá a velká písmena balíčku. |
| StartWith | Vrátí balíčky balíčku, jehož ID začíná &lt;klíčová slova&gt;. |

Žádná z těchto parametrů přijmout kanálu vstup nebo zástupné znaky.

## <a name="common-parameters"></a>Společné parametry

`Find-Package` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, podrobná, WarningAction a WarningVariable.

## <a name="examples"></a>Příklady

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```
