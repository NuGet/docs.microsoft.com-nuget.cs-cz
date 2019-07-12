---
title: Referenční informace prostředí PowerShell najít balíček NuGet
description: Referenční informace pro příkaz Powershellu Find-Package v konzole Správce balíčků NuGet v sadě Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: fee0ad0496f27d0796eddf177edc235bcb10da70
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842524"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-Package (konzola Správce balíčků v sadě Visual Studio)

*Verze 3.0 a; Toto téma popisuje příkaz v rámci [Konzola správce balíčků](package-manager-console.md) v sadě Visual Studio ve Windows. Obecný příkaz Find-balíčků v Powershellu najdete v článku [odkazu modulu Powershellu PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Získá sadu vzdálené balíčky pomocí zadaného ID nebo klíčová slova ze zdroje balíčku.

## <a name="syntax"></a>Syntaxe

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>Parametry

| Parametr | Popis |
| --- | --- |
| ID &lt;klíčová slova&gt; | (Povinné) Klíčová slova pro vyhledávání ve zdroji balíčku. Pomocí - ExactMatch vrátit pouze balíčky, jejichž ID balíčku shoduje s klíčovými slovy. Žádná klíčová slova směru, je-li `Find-Package` vrátí seznam balíčků prvních 20 soubory ke stažení nebo číslo zadané parametrem - první. Všimněte si, že – Id je volitelné a no-op. |
| Source | Cesta URL nebo složku zdroje balíčku. Chcete-li hledat. Cesty k místní složce může být absolutní nebo relativní vzhledem k aktuální složky. Pokud tento parametr vynechán, `Find-Package` hledá aktuálně vybraném zdroji balíčku. |
| AllVersions | Zobrazí všechny dostupné verze každého balíčku namísto pouze nejnovější verze. |
| první | Počet balíčků vrátit od začátku seznamu. Výchozí hodnota je 20. |
| Skip | Vynechá první &lt;int&gt; balíčky ze zobrazeného seznamu.  |
| IncludePrerelease | Obsahuje předběžné verze balíčků ve výsledcích. |
| ExactMatch | Zadané použití &lt;klíčová slova&gt; jako ID balíčku velká a malá písmena. |
| StartWith | Vrátí balíčky balíčku, jejichž ID začíná &lt;klíčová slova&gt;. |

Žádná z těchto parametrů přijímat kanálu vstup nebo zástupné znaky.

## <a name="common-parameters"></a>Společné parametry

`Find-Package` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction a WarningVariable.

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
