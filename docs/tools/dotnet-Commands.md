---
title: příkazy rozhraní příkazového řádku NuGet DotNet
description: Krátký odkaz pro příkazy související s NuGet pomocí rozhraní příkazového řádku dotnet.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: ff011e60d3de3b0999db56e1e30e97e538bd9fb4
ms.sourcegitcommit: 2a9d149bc6f5ff76b0b657324820bd0429cddeef
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/01/2019
ms.locfileid: "67496470"
---
# <a name="dotnet-cli-commands"></a>příkazy rozhraní příkazového řádku DotNet

`dotnet` Rozhraní příkazového řádku (CLI), který běží na Windows, Mac OS X a Linux, nabízí celou řadu základních příkazech, jako je instalace, obnovení a publikování balíčků. Pokud se příkaz dotnet vyhovuje vašim potřebám, není nutné používat `nuget.exe`.

Příklady použití těchto příkazů pro využívání balíčků naleznete v tématu [nainstalovat a spravovat balíčky pomocí rozhraní příkazového řádku dotnet](../consume-packages/install-use-packages-dotnet-cli.md). Příklady používání těchto příkazů k vytváření balíčků, najdete v článku [vytvoření a publikování balíčku pomocí rozhraní příkazového řádku dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).

Pro úplný příkaz odkaz na `dotnet` rozhraní příkazového řádku, naleznete v tématu [nástroje rozhraní příkazového řádku (CLI) pro .NET Core](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Využití balíčků

- [**příkaz DotNet add package**](/dotnet/core/tools/dotnet-add-package): Přidá odkaz na balíček do souboru projektu a pak spustí `dotnet restore` k instalaci balíčku.
- [**DotNet odebrat balíček**](/dotnet/core/tools/dotnet-remove-package): Odebere odkaz na balíček ze souboru projektu.
- [**DotNet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Obnoví závislostí a nástrojů projektu. Od verze NuGet 4.0, toto řešení běží stejný kód jako `nuget restore`.
- [**DotNet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Uvádí umístění *global-packages*, *http-cache*, a *temp* složky a vymaže obsah těchto složek.
- [**nové nugetconfig DotNet**](/dotnet/core/tools/dotnet-new): Vytvoří [ `nuget.config` ](../reference/nuget-config-file.md) souboru konfigurace chování Nugetu.

## <a name="package-creation"></a>Vytvoření balíčku

- [**balíčku DotNet**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Sbalit kód do balíčku NuGet.
- [**DotNet nuget nabízených**](/dotnet/core/tools/dotnet-nuget-push): Publikuje balíček NuGet server. Lze použít na nuget.org, artefaktů Azure, a [servery NuGet třetích stran](../hosting-packages/overview.md).
- [**Odstranit DotNet nuget**](/dotnet/core/tools/dotnet-nuget-delete): Odstraní nebo unlists balíček NuGet server. Lze použít na nuget.org, artefaktů Azure, a [servery NuGet třetích stran](../hosting-packages/overview.md).
