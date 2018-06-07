---
title: příkazy pro balíčky NuGet DotNet.
description: Krátký odkaz pro související NuGet příkazy, pomocí rozhraní příkazového řádku dotnet.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/23/2018
ms.topic: conceptual
ms.openlocfilehash: dd30c5d5e29ff7ef7c6622a9b93c32b908198d52
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817011"
---
# <a name="dotnet-commands"></a>příkazy DotNet.

`dotnet` Rozhraní příkazového řádku, který běží na systému Windows a Mac OS X, Linux, poskytuje řadu příkazy nezbytné nuget.exe, jak je uvedeno dále. Pokud dotnet nevyhovuje vašim požadavkům, není nutné používat `nuget.exe`.

Úplné informace o `dotnet`, najdete v části [nástrojů rozhraní příkazového řádku (CLI) .NET Core](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Balíček spotřeba

- [**DotNet. Přidejte balíček**](/dotnet/core/tools/dotnet-add-package): Přidá odkaz na soubor projektu balíček a potom spustí `dotnet restore` k instalaci balíčku.
- [**DotNet. odeberte balíček**](/dotnet/core/tools/dotnet-remove-package): Odebere odkaz balíčku ze souboru projektu.
- [**obnovení DotNet**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Obnoví závislosti a nástroje projektu. Od verze NuGet 4.0, toto spouští stejný kód jako `nuget restore`.
- [**místní hodnoty nuget DotNet**](/dotnet/core/tools/dotnet-nuget-locals): uvádí umístění *globální balíčky*, *http mezipaměti*, a *temp* složek a vymaže obsah Tyto složky.

## <a name="package-creation"></a>Vytvoření balíčku

- [**DotNet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): sady kód do balíčku NuGet. Od verze NuGet 4.0, toto spouští stejný kód jako `nuget pack`.
- [**DotNet nuget nabízené**](/dotnet/core/tools/dotnet-nuget-push): nabízených oznámení balíček na server a vydává je pro nuget.org, Visual Studio Team Services a servery NuGet třetích stran.
- [**Odstranit DotNet nuget**](/dotnet/core/tools/dotnet-nuget-delete): Odstraní nebo unlists balíček z hostitele, platí pro nuget.org, Visual Studio Team Services a servery NuGet třetích stran.
