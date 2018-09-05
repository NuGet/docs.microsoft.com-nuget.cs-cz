---
title: Referenční informace prostředí PowerShell NuGet BindingRedirect
description: Referenční informace pro příkaz prostředí PowerShell Add-BindingRedirect v konzole Správce balíčků NuGet v sadě Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: dec7db04c5cf239863b9c00e9f5bc0dde42c7e47
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551654"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>Add-BindingRedirect (konzola Správce balíčků v sadě Visual Studio)

*K dispozici pouze v rámci [Konzola správce balíčků NuGet](package-manager-console.md) v sadě Visual Studio ve Windows.*

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

`Add-BindingRedirect` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction a WarningVariable.

## <a name="examples"></a>Příklady

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```