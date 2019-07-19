---
title: Referenční dokumentace prostředí NuGet Open-PackagePage
description: Reference pro příkaz Open-PackagePage PowerShell v konzole správce balíčků NuGet v aplikaci Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 0237c23d81000a1d58264cc0ab48c73d819d0e5a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328216"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Open-PackagePage (konzola Správce balíčků v sadě Visual Studio)

*Zastaralé v 3.0 +; k dispozici pouze v rámci [konzoly Správce balíčků](../../consume-packages/install-use-packages-powershell.md) v sadě Visual Studio ve Windows.*

Spustí výchozí prohlížeč s adresou URL projektu, licence nebo sestavy pro zneužití zadaného balíčku.

## <a name="syntax"></a>Syntaxe

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>Parametry

| Parametr | Popis |
| --- | --- |
| Id | ID balíčku požadovaného balíčku. Samotný přepínač-ID je nepovinný. |
| Version | Verze balíčku, výchozí nastavení na nejnovější verzi. |
| Source | Zdroj balíčku, výchozí nastavení pro vybraný zdroj v rozevíracím seznamu zdroje |
| Licence | Otevře prohlížeč na adresu URL licence balíčku. Pokud není zadána žádná licence ani parametr-ReportAbuse, prohlížeč otevře adresu URL projektu balíčku. |
| ReportAbuse | Otevře prohlížeč na adrese URL pro zneužití sestavy balíčku. Pokud není zadána žádná licence ani parametr-ReportAbuse, prohlížeč otevře adresu URL projektu balíčku. |
| PassThru | Zobrazí adresu URL. pro potlačení otevírání prohlížeče použijte příkaz with-WhatIf. |

Žádný z těchto parametrů nepřijímají vstupní ani zástupné znaky kanálu.

## <a name="common-parameters"></a>Společné parametry

`Open-PackagePage`podporuje následující [běžné parametry PowerShellu](http://go.microsoft.com/fwlink/?LinkID=113216): Ladit, Error Action, ErrorVariable, unbuffer, subvariable, PipelineVariable, verbose, WarningAction a WarningVariable.

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