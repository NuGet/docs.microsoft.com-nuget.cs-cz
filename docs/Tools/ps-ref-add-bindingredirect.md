---
title: "Referenční informace prostředí PowerShell NuGet BindingRedirect | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 90f4dcb0-6e5a-4948-8ea9-62e0d061d95a
description: "Referenční dokumentace pro příkaz prostředí PowerShell přidat BindingRedirect v konzole Správce balíčků NuGet v sadě Visual Studio."
keywords: "NuGet konzoly Správce balíčků, příkazy prostředí NuGet Powershell, NuGet Powershell odkaz, přidat BindingRedirect"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6a3232af925f75713168421e68f2773060c5ebaa
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/05/2018
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>Přidat BindingRedirect (konzola Správce balíčků v sadě Visual Studio)

*K dispozici pouze v rámci [Konzola správce balíčků NuGet](Package-Manager-Console.md) v sadě Visual Studio v systému Windows.*

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

`Add-BindingRedirect`podporuje následující [společné parametry prostředí PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): ladění, Chyba akce, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, podrobná, WarningAction a WarningVariable.

## <a name="examples"></a>Příklady

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```