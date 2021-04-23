---
title: Reference k NuGet Find-Package PowerShellu
description: Referenční informace k příkazu Find-Package PowerShellu v konzole správce balíčků NuGet v aplikaci Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 263835da64340a13737b32ab54ab057cb640a080
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901756"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-Package (konzola správce balíčků v aplikaci Visual Studio)

*Verze 3.0 +; Toto téma popisuje příkaz v [konzole správce balíčků](../../consume-packages/install-use-packages-powershell.md) v sadě Visual Studio ve Windows. Obecný příkaz Find-Package PowerShellu najdete v [referenčních informacích k PowerShellu PackageManagement](/powershell/module/packagemanagement).*

Získá sadu vzdálených balíčků se zadaným ID nebo klíčovými slovy ze zdroje balíčku.

## <a name="syntax"></a>Syntaxe

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>Parametry

| Parametr | Popis |
| --- | --- |
| &lt;Klíčová slova ID&gt; | Požadovanou Klíčová slova, která se mají použít při vyhledávání zdroje balíčku Pomocí parametru-ExactMatch můžete vracet pouze ty balíčky, jejichž ID balíčku odpovídá klíčovým slovům. Pokud nejsou zadána žádná klíčová slova, `Find-Package` vrátí seznam prvních 20 balíčků ke stažení nebo číslo určené parametrem-First. Všimněte si, že-ID je volitelné a no-op. |
| Zdroj | Adresa URL nebo cesta ke složce pro zdroj balíčku, který má být prohledán. Cesty k místní složce můžou být absolutní nebo relativní vzhledem k aktuální složce. Pokud tento parametr vynecháte, `Find-Package` vyhledá aktuálně vybraný zdroj balíčku. |
| AllVersions | Zobrazí všechny dostupné verze jednotlivých balíčků, nikoli jenom nejnovější verzi. |
| První | Počet balíčků, které mají být vráceny od začátku seznamu; Výchozí hodnota je 20. |
| Přeskočit | Vynechává první celočíselné &lt; &gt; balíčky ze zobrazeného seznamu.  |
| IncludePrerelease | Zahrnuje předběžné verze balíčků ve výsledcích. |
| ExactMatch | Určili jste použití &lt; klíčových slov &gt; jako ID balíčku s rozlišováním velkých a malých písmen. |
| StartWith | Vrátí balíčky, jejichž ID balíčku začíná &lt; klíčovými slovy &gt; . |

Žádný z těchto parametrů nepřijímají vstupní ani zástupné znaky kanálu.

## <a name="common-parameters"></a>Společné parametry

`Find-Package` podporuje následující [běžné parametry PowerShellu](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, inbuffer, subvariable, PipelineVariable, verbose, WarningAction a WarningVariable.

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