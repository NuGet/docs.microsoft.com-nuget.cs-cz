---
title: Referenční informace prostředí PowerShell NuGet Open-PackagePage
description: Referenční dokumentace pro příkaz prostředí PowerShell PackagePage otevřete v konzole Správce balíčků NuGet v sadě Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: e64a83c01a7baac330c99fe40ba52f328a2133b8
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817717"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Open-PackagePage (konzola Správce balíčků v sadě Visual Studio)

*Zastaralé v 3.0 +; k dispozici pouze v rámci [Konzola správce balíčků NuGet](package-manager-console.md) v sadě Visual Studio v systému Windows.*

Spuštění výchozího prohlížeče s projektu, licence nebo adresy URL sestav zneužití pro zadaný balíček.

## <a name="syntax"></a>Syntaxe

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>Parametry

| Parametr | Popis |
| --- | --- |
| ID | ID balíčku požadované balíčku. -Id je volitelný přepínač sám sebe. |
| Version | Verze balíčku, jako výchozí bude použit na nejnovější verzi. |
| Zdroj | Zdroj balíčku jako výchozí bude použit zdroj vybraný v zdroji rozevíracího seznamu. |
| Licence | Otevře prohlížeč na adrese URL licence balíčku. Pokud je zadán - licence ani - ReportAbuse, prohlížeči se otevře adresa URL projektu balíčku. |
| ReportAbuse | Otevře prohlížeč na adresu URL zneužití sestavy balíčku. Pokud je zadán - licence ani - ReportAbuse, prohlížeči se otevře adresa URL projektu balíčku. |
| PassThru | Zobrazí adresu URL; pomocí s - WhatIf potlačit, otevřete v prohlížeči. |

Žádná z těchto parametrů přijmout kanálu vstup nebo zástupné znaky.

## <a name="common-parameters"></a>Společné parametry

`Open-PackagePage` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, podrobná, WarningAction a WarningVariable.

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