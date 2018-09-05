---
title: příkazy DotNet NuGet
description: Krátký odkaz pro příkazy související s NuGet pomocí rozhraní příkazového řádku dotnet.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: conceptual
ms.openlocfilehash: 88e058be674ecddc500665bfa3517f19acde0cd7
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546313"
---
# <a name="dotnet-commands"></a>příkazy DotNet

`dotnet` Rozhraní příkazového řádku, který běží na Windows, Mac OS X a Linux, nabízí celou řadu základních nuget.exe příkazy, jak je uvedeno níže. Pokud se příkaz dotnet vyhovuje vašim potřebám, není nutné používat `nuget.exe`.

Úplné informace o `dotnet`, naleznete v tématu [nástroje rozhraní příkazového řádku (CLI) pro .NET Core](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Využití balíčků

- [**příkaz DotNet add package**](/dotnet/core/tools/dotnet-add-package): Přidá odkaz na balíček do souboru projektu a pak spustí `dotnet restore` k instalaci balíčku.
- [**DotNet odebrat balíček**](/dotnet/core/tools/dotnet-remove-package): Odebere odkaz na balíček ze souboru projektu.
- [**DotNet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Obnoví závislostí a nástrojů projektu. Od verze NuGet 4.0, toto řešení běží stejný kód jako `nuget restore`.
- [**DotNet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): uvádí umístění *global-packages*, *http-cache*, a *temp* složky a vymaže obsah Tyto složky.

## <a name="package-creation"></a>Vytvoření balíčku

- [**balíčku DotNet**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): balíčky kódu do balíčku NuGet. Od verze NuGet 4.0, toto řešení běží stejný kód jako `nuget pack`.
- [**DotNet nuget nabízených**](/dotnet/core/tools/dotnet-nuget-push): odešle balíček na server a publikuje ji lze použít na nuget.org, Visual Studio Team Services a NuGet servery třetích stran.
- [**Odstranit DotNet nuget**](/dotnet/core/tools/dotnet-nuget-delete): Odstraní nebo unlists balíček z hostitele, lze použít na nuget.org, Visual Studio Team Services a NuGet servery třetích stran.
