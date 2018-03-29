---
title: Referenční informace prostředí PowerShell Get balíček NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referenční dokumentace pro příkaz prostředí PowerShell Get-balíčku v konzole Správce balíčků NuGet v sadě Visual Studio.
keywords: NuGet konzoly Správce balíčků, příkazy prostředí NuGet Powershell, NuGet Powershell odkaz, Get-Package
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: ca80d95df309d8afce2ce6cff26c19980affde7a
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>Get-Package (konzola Správce balíčků v sadě Visual Studio)

*Toto téma popisuje příkaz v rámci [Konzola správce balíčků NuGet](package-manager-console.md) v sadě Visual Studio v systému Windows. Příkaz prostředí PowerShell Get-Package obecné najdete v článku [odkaz na prostředí PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Načte seznam balíčků nainstalovaných v místním úložišti, obsahuje seznam balíčků dostupné z balíčku zdroje při použití s přepínačem - ListAvailable nebo vypíše dostupné aktualizace, které při použití s přepínačem - Update.

## <a name="syntax"></a>Syntaxe

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

Bez parametrů `Get-Package` zobrazí seznam balíčků nainstalovaných ve výchozím projektu.

## <a name="parameters"></a>Parametry

| Parametr | Popis |
| --- | --- |
| Zdroj | Adresu URL nebo cestu složky pro balíček. Cesty k místní složce může být absolutní, nebo relativně vzhledem k aktuální složce. Pokud tento parametr vynechán, `Get-Package` hledá aktuálně vybraném zdroji balíčku. Při použití s příznakem-ListAvailable, výchozí hodnota je nuget.org. |
| ListAvailable | Zobrazí seznam balíčků dostupné z balíčku zdroje, jako výchozí bude použit nuget.org. Výchozí hodnota je 50 balíčky ukazuje, pokud jsou zadány - PageSize nebo - první. |
| Aktualizace | Zobrazí seznam balíčků, které mají k dispozici aktualizace ze zdroje balíčků. |
| ProjectName | Projekt, ze kterého mají být získány nainstalované balíčky. Pokud tento parametr vynechán, vrátí nainstalované projekty pro celé řešení. |
| Filtr | Řetězec filtru sloužící k upřesnění seznamu balíčků použitím do ID balíčku, popisu a značkách. |
| první | Počet balíčků, které mají být vráceny od začátku seznamu. Pokud není zadáno, bude jako výchozí nastavena na 50. |
| Skip | Vynechá první &lt;int&gt; balíčky ze seznamu zobrazených.  |
| AllVersions | Zobrazí všechny dostupné verze jednotlivých balíčků místo pouze nejnovější verzi. |
| IncludePrerelease | Obsahuje předběžné verze balíčků ve výsledcích. |
| PageSize | *(3.0 +)*  Při použití s příznakem-ListAvailable (povinné), počet balíčků, seznam, než se předá výzvy a pokračujte. |

Žádná z těchto parametrů přijmout kanálu vstup nebo zástupné znaky.

## <a name="common-parameters"></a>Společné parametry

`Get-Package` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, podrobná, WarningAction a WarningVariable.

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
