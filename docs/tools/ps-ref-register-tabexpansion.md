---
title: Referenční informace prostředí PowerShell NuGet Register-TabExpansion
description: Referenční informace pro příkaz Powershellu zaregistrujte TabExpansion v konzole Správce balíčků NuGet v sadě Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8adb80af85e2e32fa8c35e5272cf90ff0c0ddcbb
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842486"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>Register-TabExpansion (konzola Správce balíčků v sadě Visual Studio)

*K dispozici pouze v rámci [Konzola správce balíčků](package-manager-console.md) v sadě Visual Studio ve Windows.*

Zaregistruje rozšíření tab pro parametry zadaný příkaz tak, aby při karta se používá při zadání příkazu, rozšířené hodnoty se zobrazí jako dostupné možnosti pro parametr nejistá. Všechny předchozí rozšíření příkazu jsou přepsány.

## <a name="syntax"></a>Syntaxe

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>Parametry

| Parametr | Popis |
| --- | --- |
| Name | (Povinné) Příkaz pro registraci rozšíření. -Název je volitelný přepínač samotný. |
| Definice | (Povinné) Objekt popisující argument v syntaxi `@{'<parameter>' = {'<value1>', '<value2>', ...}}` kde `<parameter>` je název parametru k úpravě a každý `<value>` poskytuje konkrétní rozšíření. Jednoduché i dvojité uvozovky jsou přijaty. |

Žádná z těchto parametrů přijímat kanálu vstup nebo zástupné znaky.

## <a name="common-parameters"></a>Společné parametry

`Register-TabExpansion` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction a WarningVariable.

## <a name="examples"></a>Příklady

Vezměte v úvahu řešení, které obsahuje tři projekty názvy EventManager, nástroje a SpecialParser. Vývojář se často používá `Update-Package` příkaz v různých časech s každým z těchto projektech. Vyhledá je výhodné mít `Update-Package` příkaz poskytují rozšíření automatické dokončování pro `-ProjectName` argument, takže nepotřebuje zadejte název projektu pokaždé, když. 

Následující příkaz, pak zaregistruje jako rozšíření pro názvy těchto tří projektů `-ProjectName` parametr:

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

Vývojář potom můžete zadat `Update-Package -ProjectName `, stiskněte klávesu Tab a zobrazit rozšíření nabízeny jako možnosti automatického dokončování:

![Příklad použití TabExpansion registru](media/Register-TabExpansion-Example.png)
