---
title: dotnet CLI – příkazy NuGet
description: Krátký odkaz na příkazy týkající se NuGetu pomocí rozhraní příkazového řádku dotnet.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: ff011e60d3de3b0999db56e1e30e97e538bd9fb4
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328249"
---
# <a name="dotnet-cli-commands"></a>dotnet – příkazy rozhraní příkazového řádku

Rozhraní `dotnet` příkazového řádku (CLI), které běží ve Windows, Mac OS X a Linux, poskytuje řadu základních příkazů, jako je instalace, obnovení a publikování balíčků. Pokud dotnet vyhovuje vašim potřebám, není nutné používat `nuget.exe`.

Příklady použití těchto příkazů ke spotřebě balíčků najdete v tématu [instalace a Správa balíčků pomocí rozhraní příkazového řádku dotnet](../consume-packages/install-use-packages-dotnet-cli.md). Příklady použití těchto příkazů k vytváření balíčků najdete v tématu [Vytvoření a publikování balíčku pomocí rozhraní příkazového řádku dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).

Úplný odkaz na `dotnet` příkazy pro rozhraní příkazového řádku naleznete v tématu [.NET Core Command-line interface (CLI) Tools](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Spotřeba balíčku

- [**dotnet – přidat balíček**](/dotnet/core/tools/dotnet-add-package): Přidá odkaz na balíček do souboru projektu a potom spustí `dotnet restore` instalaci balíčku.
- [**dotnet odebrat balíček**](/dotnet/core/tools/dotnet-remove-package): Odebere odkaz na balíček ze souboru projektu.
- [**dotnet Restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Obnoví závislosti a nástroje projektu. Od NuGet 4,0 to spustí stejný kód jako `nuget restore`.
- [**dotnet – národní prostředí NuGet**](/dotnet/core/tools/dotnet-nuget-locals): Zobrazí seznam umístění *globálních balíčků*, *HTTP cache*a *dočasných* složek a vymaže obsah těchto složek.
- [**dotnet New nugetconfig**](/dotnet/core/tools/dotnet-new): [`nuget.config`](../reference/nuget-config-file.md) Vytvoří soubor pro konfiguraci chování NuGet.

## <a name="package-creation"></a>Vytvoření balíčku

- [**sada dotnet Pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Zabalí kód do balíčku NuGet.
- [**dotnet – vložení nugetu**](/dotnet/core/tools/dotnet-nuget-push): Publikuje balíček na server NuGet. Platí pro nuget.org, Azure Artifacts a [servery NuGet třetích stran](../hosting-packages/overview.md).
- [**dotnet NuGet Delete**](/dotnet/core/tools/dotnet-nuget-delete): Odstraní nebo zruší výpis balíčku ze serveru NuGet. Platí pro nuget.org, Azure Artifacts a [servery NuGet třetích stran](../hosting-packages/overview.md).
