---
title: Referenční informace prostředí PowerShell NuGet BindingRedirect
description: Referenční informace pro příkaz prostředí PowerShell Add-BindingRedirect v konzole Správce balíčků NuGet v sadě Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a5f318ddfb2bb8498ab3e608f8036be05dcb0706
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842541"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>Add-BindingRedirect (konzola Správce balíčků v sadě Visual Studio)

*K dispozici pouze v rámci [Konzola správce balíčků](package-manager-console.md) v sadě Visual Studio ve Windows.*

Zkontroluje ve všech sestaveních ve výstupní cesta pro projekt a v případě potřeby přidá přesměrování vazby do konfiguračního souboru aplikace nebo web. Tento příkaz spustí automaticky při instalaci balíčku.

Podrobnosti o vazby přesměrování a proč se používají, najdete v části [přesměrování verze sestavení](/dotnet/framework/configure-apps/redirect-assembly-versions) v dokumentaci k rozhraní .NET.

## <a name="syntax"></a>Syntaxe

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a>Parametry

| Parametr | Popis |
| --- | --- |
| ProjectName | (Povinné) Projekt, do které chcete přidat přesměrování vazby. Je volitelný přepínač - ProjectName samotný. |

Žádná z těchto parametrů přijímat kanálu vstup nebo zástupné znaky.

## <a name="common-parameters"></a>Společné parametry

`Add-BindingRedirect` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction a WarningVariable.

## <a name="examples"></a>Příklady

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```