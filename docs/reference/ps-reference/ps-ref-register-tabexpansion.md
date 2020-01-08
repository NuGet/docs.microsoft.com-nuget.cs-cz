---
title: Registry NuGet – Reference k prostředí PowerShell TabExpansion
description: Reference k příkazu register-TabExpansion prostředí PowerShell v konzole správce balíčků NuGet v aplikaci Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 37aed96760e642b03c02bf31fe47a54f0e3cb74a
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384451"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>Register-TabExpansion (konzola správce balíčků v aplikaci Visual Studio)

*K dispozici pouze v rámci [konzoly Správce balíčků](../../consume-packages/install-use-packages-powershell.md) v sadě Visual Studio ve Windows.*

Zaregistruje rozšíření pro parametry zadaného příkazu, například když se při zadání příkazu použije karta, rozšíří se hodnoty jako dostupné možnosti pro daný parametr. Všechna předchozí rozšíření pro příkaz jsou přepsána.

## <a name="syntax"></a>Syntaxe

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>Parametry

| Parametr | Popis |
| --- | --- |
| Name | Požadovanou Příkaz, pro který mají být zaregistrována rozšíření. Samotný přepínač-Name je nepovinný. |
| Definice | Požadovanou Objekt popisující argument v syntaxi `@{'<parameter>' = {'<value1>', '<value2>', ...}}`, kde `<parameter>` je název parametru, který má být upraven, a každý `<value>` poskytuje konkrétní rozšíření. Jsou přijímány jednoduché i dvojité uvozovky. |

Žádný z těchto parametrů nepřijímají vstupní ani zástupné znaky kanálu.

## <a name="common-parameters"></a>Společné parametry

`Register-TabExpansion` podporuje následující [běžné parametry PowerShellu](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, inbuffer, subvariable, PipelineVariable, verbose, WarningAction a WarningVariable.

## <a name="examples"></a>Příklady

Vezměte v úvahu řešení, které obsahuje tři projekty s názvy EventManager, nástroje a SpecialParser. Vývojář často používá příkaz `Update-Package` v různých časech u každého z těchto projektů. Zjistí, že má příkaz `Update-Package` pro `-ProjectName` argumentu zadat rozšíření automatického dokončování, takže nemusí pokaždé zadávat název projektu. 

Následující příkaz zaregistruje tyto tři názvy projektů jako rozšíření pro `-ProjectName` parametr:

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

Vývojář pak může zadat `Update-Package -ProjectName `, stisknout klávesu TAB a zobrazit rozšíření nabízená jako možnosti automatického dokončování:

![Příklad použití Register-TabExpansion](media/Register-TabExpansion-Example.png)
