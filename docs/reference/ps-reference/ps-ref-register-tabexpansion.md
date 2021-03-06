---
title: Reference k NuGet Register-TabExpansion PowerShellu
description: Referenční informace k příkazu Register-TabExpansion PowerShellu v konzole správce balíčků NuGet v aplikaci Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 6ad0da0e84fc2e31499c06bde013d2a256987d9a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777456"
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
| Název | Požadovanou Příkaz, pro který mají být zaregistrována rozšíření. Samotný přepínač-Name je nepovinný. |
| Definice | Požadovanou Objekt popisující argument v syntaxi, `@{'<parameter>' = {'<value1>', '<value2>', ...}}` kde `<parameter>` je název parametru, který má být upraven, a každý `<value>` z nich poskytuje konkrétní rozšíření. Jsou přijímány jednoduché i dvojité uvozovky. |

Žádný z těchto parametrů nepřijímají vstupní ani zástupné znaky kanálu.

## <a name="common-parameters"></a>Společné parametry

`Register-TabExpansion` podporuje následující [běžné parametry PowerShellu](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, inbuffer, subvariable, PipelineVariable, verbose, WarningAction a WarningVariable.

## <a name="examples"></a>Příklady

Vezměte v úvahu řešení, které obsahuje tři projekty s názvy EventManager, nástroje a SpecialParser. Vývojář často používá `Update-Package` příkaz v různých časech s každým z těchto projektů. Zjistí, že má `Update-Package` příkaz k dispozici rozšíření automatického dokončování pro `-ProjectName` argument, takže nemusí pokaždé zadávat název projektu. 

Následující příkaz zaregistruje tyto tři názvy projektů jako rozšíření pro `-ProjectName` parametr:

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

Vývojář pak může zadat `Update-Package -ProjectName ` , stisknout klávesu TAB a zobrazit rozšíření nabízená jako možnosti automatického dokončování:

![Příklad použití Register-TabExpansion](media/Register-TabExpansion-Example.png)