---
title: Referenční informace prostředí PowerShell NuGet Open-PackagePage | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referenční dokumentace pro příkaz prostředí PowerShell PackagePage otevřete v konzole Správce balíčků NuGet v sadě Visual Studio.
keywords: NuGet konzoly Správce balíčků, příkazy prostředí NuGet Powershell, odkaz NuGet Powershell, otevřete PackagePage
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 5e0955e58daacf381666c676c8fcf22c698e9db6
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Otevřete PackagePage (konzola Správce balíčků v sadě Visual Studio)

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
| License | Otevře prohlížeč na adrese URL licence balíčku. Pokud je zadán - licence ani - ReportAbuse, prohlížeči se otevře adresa URL projektu balíčku. |
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