---
title: Referenční informace prostředí PowerShell NuGet BindingRedirect | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referenční dokumentace pro příkaz prostředí PowerShell přidat BindingRedirect v konzole Správce balíčků NuGet v sadě Visual Studio.
keywords: NuGet konzoly Správce balíčků, příkazy prostředí NuGet Powershell, NuGet Powershell odkaz, přidat BindingRedirect
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 2a337bd61295f436b49c56c1680d07ccc6a8c403
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>Přidat BindingRedirect (konzola Správce balíčků v sadě Visual Studio)

*K dispozici pouze v rámci [Konzola správce balíčků NuGet](package-manager-console.md) v sadě Visual Studio v systému Windows.*

Hledá ve všech sestaveních ve výstupní cestě pro projekt a potřeby přidá přesměrování vazby do konfiguračního souboru aplikace nebo webu. Tento příkaz spustí automaticky při instalaci balíčku.

Podrobnosti o vazby přesměrování a proč se používají, najdete v části [přesměrování verzí sestavení](/dotnet/framework/configure-apps/redirect-assembly-versions) v dokumentaci k rozhraní .NET.

## <a name="syntax"></a>Syntaxe

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a>Parametry

| Parametr | Popis |
| --- | --- |
| ProjectName | (Povinné) Projekt, pro které má být přidána přesměrování vazby. Je volitelný přepínač - ProjectName sám sebe. |

Žádná z těchto parametrů přijmout kanálu vstup nebo zástupné znaky.

## <a name="common-parameters"></a>Společné parametry

`Add-BindingRedirect` podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, podrobná, WarningAction a WarningVariable.

## <a name="examples"></a>Příklady

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```