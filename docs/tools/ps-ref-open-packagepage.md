---
title: Referenční informace prostředí PowerShell NuGet Open-PackagePage
description: Referenční informace pro příkaz Powershellu otevřít PackagePage v konzole Správce balíčků NuGet v sadě Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: fd738f15b461051c4e9413b3035456c687979b97
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842268"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Open-PackagePage (konzola Správce balíčků v sadě Visual Studio)

*Zastaralé v 3.0 +; k dispozici pouze v rámci [Konzola správce balíčků](package-manager-console.md) v sadě Visual Studio ve Windows.*

Spustí výchozí prohlížeč s projektem, licenci nebo adresa URL sestavy zneužití pro zadaný balíček.

## <a name="syntax"></a>Syntaxe

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>Parametry

| Parametr | Popis |
| --- | --- |
| Id | ID balíčku požadovaný balíček. -Id je volitelný přepínač samotný. |
| Version | Verze balíčku, jako výchozí se použije na nejnovější verzi. |
| Source | Zdroj balíčku jako výchozí se použije zdroj vybraný ve zdroji rozevíracího seznamu. |
| Licence | Otevře prohlížeč na adresu URL licence balíčku. Pokud není zadána - licence ani - ReportAbuse, prohlížeči otevře adresa URL projektu daného balíčku. |
| ReportAbuse | Otevře se prohlížeč, aby adresa URL balíčku sestavy zneužití. Pokud není zadána - licence ani - ReportAbuse, prohlížeči otevře adresa URL projektu daného balíčku. |
| PassThru | Zobrazí adresu URL; pomocí - WhatIf potlačit, otevřete v prohlížeči. |

Žádná z těchto parametrů přijímat kanálu vstup nebo zástupné znaky.

## <a name="common-parameters"></a>Společné parametry

`Open-PackagePage` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction a WarningVariable.

## <a name="examples"></a>Příklady

```ps
# Opens a browser with the Ninject package's project page
Open-PackagePage Ninject

# Opens a browser with the Ninject package's license page
Open-PackagePage Ninject -License

# Opens a browser with the Ninject package's report abuse page  
Open-PackagePage Ninject -ReportAbuse

# Assigns the license URL to the variable, $url, without launching the browser
$url = Open-PackagePage Ninject -License -PassThru -WhatIf
```