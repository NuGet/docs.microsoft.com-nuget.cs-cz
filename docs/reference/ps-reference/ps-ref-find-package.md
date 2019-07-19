---
title: Reference k PowerShellu pro vyhledání balíčků NuGet
description: Reference k příkazu najít-Package PowerShell v konzole správce balíčků NuGet v aplikaci Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 4bb6d090b97dd55fc1be0625855aab27a0d181c4
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328219"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-Package (konzola Správce balíčků v sadě Visual Studio)

*Verze 3.0 +; Toto téma popisuje příkaz v [konzole správce balíčků](../../consume-packages/install-use-packages-powershell.md) v sadě Visual Studio ve Windows. Obecný příkaz prostředí PowerShell Find-Package najdete v referenčních [informacích k PowerShellu PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Získá sadu vzdálených balíčků se zadaným ID nebo klíčovými slovy ze zdroje balíčku.

## <a name="syntax"></a>Syntaxe

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>Parametry

| Parametr | Popis |
| --- | --- |
| Klíčová slova ID &lt;&gt; | Požadovanou Klíčová slova, která se mají použít při vyhledávání zdroje balíčku Pomocí parametru-ExactMatch můžete vracet pouze ty balíčky, jejichž ID balíčku odpovídá klíčovým slovům. Pokud nejsou zadána žádná klíčová `Find-Package` slova, vrátí seznam prvních 20 balíčků ke stažení nebo číslo určené parametrem-First. Všimněte si, že-ID je volitelné a no-op. |
| Source | Adresa URL nebo cesta ke složce pro zdroj balíčku, který má být prohledán. Cesty k místní složce můžou být absolutní nebo relativní vzhledem k aktuální složce. Pokud tento parametr vynecháte, `Find-Package` vyhledá aktuálně vybraný zdroj balíčku. |
| AllVersions | Zobrazí všechny dostupné verze jednotlivých balíčků, nikoli jenom nejnovější verzi. |
| První | Počet balíčků, které mají být vráceny od začátku seznamu; Výchozí hodnota je 20. |
| Skip | Vynechává první &lt;&gt; celočíselné balíčky ze zobrazeného seznamu.  |
| IncludePrerelease | Zahrnuje předběžné verze balíčků ve výsledcích. |
| ExactMatch | Určili jste &lt;použití&gt; klíčových slov jako ID balíčku s rozlišováním velkých a malých písmen. |
| StartWith | Vrátí balíčky, jejichž ID balíčku začíná &lt;klíčovými slovy&gt;. |

Žádný z těchto parametrů nepřijímají vstupní ani zástupné znaky kanálu.

## <a name="common-parameters"></a>Společné parametry

`Find-Package`podporuje následující [běžné parametry PowerShellu](http://go.microsoft.com/fwlink/?LinkID=113216): Ladit, Error Action, ErrorVariable, unbuffer, subvariable, PipelineVariable, verbose, WarningAction a WarningVariable.

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
