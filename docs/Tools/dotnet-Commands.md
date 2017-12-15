---
title: "příkazy pro balíčky NuGet dotNet. | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 0c81dbc4-2c14-4ec8-b87a-b802a899c3ea
description: "Krátký odkaz pro související NuGet příkazy, pomocí rozhraní příkazového řádku dotnet."
keywords: "příkazy pro balíčky NuGet DotNet, dotnet. pack, dotnet obnovení, dotnet nuget místní hodnoty –, dotnet nuget nabízené, odstranění nuget dotnet."
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7ff4779f46db102f1384650d82118b34fedd4413
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="dotnet-commands"></a>příkazy dotNet.

DotNet rozhraní příkazového řádku, který běží na systému Windows a Mac OS X, Linux, poskytuje řadu příkazů základní nuget.exe, jak je uvedeno dále. Kde dotnet poskytuje požadované příkazy, není nutné stáhnout nuget.exe.

- [**DotNet pack**](https://docs.microsoft.com/dotnet/core/tools/dotnet-pack?tabs=netcore2x): sady kód pro NETCore SDK projekty do balíčku NuGet. Všechny ostatní typy projektu měli používat.[`nuget pack`](cli-ref-pack.md)
- [**obnovení DotNet**](https://docs.microsoft.com/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Obnoví závislosti a nástroje projektu. Od verze NuGet 4.0, toto spouští stejný kód jako `nuget restore`.
- [**místní hodnoty nuget DotNet**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-locals): vymaže nebo vypíše místní prostředky NuGet, jako je například http-požadavek mezipaměti, dočasnou vyrovnávací paměť nebo složku globální balíčky celého systému.
- [**DotNet nuget nabízené**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-push): nabízených oznámení balíček na server a vydává je pro nuget.org, Visual Studio Team Services nebo všechny servery NuGet třetích stran.
- [**Odstranit DotNet nuget**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-delete): Odstraní nebo unlists balíčku ze serveru, platí pro nuget.org, Visual Studio Team Services nebo všechny servery NuGet třetích stran.
