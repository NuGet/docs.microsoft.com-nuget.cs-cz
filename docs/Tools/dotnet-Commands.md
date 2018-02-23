---
title: "příkazy pro balíčky NuGet dotNet. | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Krátký odkaz pro související NuGet příkazy, pomocí rozhraní příkazového řádku dotnet."
keywords: "příkazy pro balíčky NuGet DotNet, dotnet. pack, dotnet obnovení, dotnet nuget místní hodnoty –, dotnet nuget nabízené, odstranění nuget dotnet."
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2851938cd43b35454d8e4ad595fbd93229d4dd72
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/20/2018
---
# <a name="dotnet-commands"></a>příkazy dotNet.

`dotnet` Rozhraní příkazového řádku, který běží na systému Windows a Mac OS X, Linux, poskytuje řadu příkazy nezbytné nuget.exe, jak je uvedeno dále. Pokud dotnet nevyhovuje vašim požadavkům, není nutné používat `nuget.exe`.

Úplné informace o `dotnet`, najdete v části [nástrojů rozhraní příkazového řádku (CLI) .NET Core](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Balíček spotřeba

- [**DotNet. Přidejte balíček**](/dotnet/core/tools/dotnet-add-package): Přidá odkaz na soubor projektu balíček a potom spustí `dotnet restore` k instalaci balíčku.
- [**DotNet. odeberte balíček**](/dotnet/core/tools/dotnet-remove-package): Odebere odkaz balíčku ze souboru projektu.
- [**obnovení DotNet**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Obnoví závislosti a nástroje projektu. Od verze NuGet 4.0, toto spouští stejný kód jako `nuget restore`.
- [**místní hodnoty nuget DotNet**](/dotnet/core/tools/dotnet-nuget-locals): vymaže nebo vypíše místní prostředky NuGet například mezipaměti požadavek http, dočasnou vyrovnávací paměť a složce globální balíčky celého systému.

## <a name="package-creation"></a>Vytvoření balíčku

- [**DotNet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): sady kód do balíčku NuGet. Od verze NuGet 4.0, toto spouští stejný kód jako `nuget pack`.
- [**DotNet nuget nabízené**](/dotnet/core/tools/dotnet-nuget-push): nabízených oznámení balíček na server a vydává je pro nuget.org, Visual Studio Team Services a servery NuGet třetích stran.
- [**Odstranit DotNet nuget**](/dotnet/core/tools/dotnet-nuget-delete): Odstraní nebo unlists balíček z hostitele, platí pro nuget.org, Visual Studio Team Services a servery NuGet třetích stran.
