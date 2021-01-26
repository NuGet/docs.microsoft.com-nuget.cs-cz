---
title: dotnet CLI – příkazy NuGet
description: Krátký odkaz na příkazy týkající se NuGetu pomocí rozhraní příkazového řádku dotnet.
author: JonDouglas
ms.author: jodou
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: 5438354729ccc851bbbae6c0e7b9394d4226da52
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779998"
---
# <a name="dotnet-cli-commands"></a>Příkazy příkazového řádku dotnet

`dotnet`Rozhraní příkazového řádku (CLI), které běží ve Windows, Mac OS X a Linux, poskytuje řadu základních příkazů, jako je instalace, obnovení a publikování balíčků. Pokud dotnet vyhovuje vašim potřebám, není nutné používat `nuget.exe` .

Příklady použití těchto příkazů ke spotřebě balíčků najdete v tématu [instalace a Správa balíčků pomocí rozhraní příkazového řádku dotnet](../consume-packages/install-use-packages-dotnet-cli.md). Příklady použití těchto příkazů k vytváření balíčků najdete v tématu [Vytvoření a publikování balíčku pomocí rozhraní příkazového řádku dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).

Úplný odkaz na příkazy pro `dotnet` [rozhraní příkazového řádku naleznete v tématu .NET Core Command-line interface (CLI) Tools](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Spotřeba balíčku

- [**dotnet Add Package**](/dotnet/core/tools/dotnet-add-package): přidá odkaz na balíček do souboru projektu a potom spustí `dotnet restore` instalaci balíčku.
- [**dotnet odebrat balíček**](/dotnet/core/tools/dotnet-remove-package): Odebere odkaz na balíček ze souboru projektu.
- [**dotnet Restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): obnoví závislosti a nástroje projektu. Od NuGet 4,0 to spustí stejný kód jako `nuget restore` .
- [**dotnet – místní prostředí NuGet**](/dotnet/core/tools/dotnet-nuget-locals): vypisuje umístění *globálních balíčků*, *HTTP cache* a *dočasných* složek a vymaže obsah těchto složek.
- [**dotnet New nugetconfig**](/dotnet/core/tools/dotnet-new): vytvoří [`nuget.config`](../reference/nuget-config-file.md) soubor pro konfiguraci chování NuGet.

## <a name="package-creation"></a>Vytvoření balíčku

- [**dotnet Pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): sbalí kód do balíčku NuGet.
- [**dotnet – push NuGet**](/dotnet/core/tools/dotnet-nuget-push): publikuje balíček na server NuGet. Platí pro nuget.org, Azure Artifacts a [servery NuGet třetích stran](../hosting-packages/overview.md).
- [**dotnet NuGet Delete**](/dotnet/core/tools/dotnet-nuget-delete): odstraní nebo zruší výpis balíčku ze serveru NuGet. Platí pro nuget.org, Azure Artifacts a [servery NuGet třetích stran](../hosting-packages/overview.md).
- [**dotnet NuGet ověřit**](/dotnet/core/tools/dotnet-nuget-verify): ověří podepsaný balíček NuGet.
