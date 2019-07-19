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
# <a name="dotnet-cli-commands"></a><span data-ttu-id="4c848-103">dotnet – příkazy rozhraní příkazového řádku</span><span class="sxs-lookup"><span data-stu-id="4c848-103">dotnet CLI commands</span></span>

<span data-ttu-id="4c848-104">Rozhraní `dotnet` příkazového řádku (CLI), které běží ve Windows, Mac OS X a Linux, poskytuje řadu základních příkazů, jako je instalace, obnovení a publikování balíčků.</span><span class="sxs-lookup"><span data-stu-id="4c848-104">The `dotnet` command-line interface (CLI), which runs on Windows, Mac OS X, and Linux, provides a number of essential commands such as installing, restoring, and publishing packages.</span></span> <span data-ttu-id="4c848-105">Pokud dotnet vyhovuje vašim potřebám, není nutné používat `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="4c848-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="4c848-106">Příklady použití těchto příkazů ke spotřebě balíčků najdete v tématu [instalace a Správa balíčků pomocí rozhraní příkazového řádku dotnet](../consume-packages/install-use-packages-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="4c848-106">For examples of using these commands to consume packages, see [Install and manage packages using the dotnet CLI](../consume-packages/install-use-packages-dotnet-cli.md).</span></span> <span data-ttu-id="4c848-107">Příklady použití těchto příkazů k vytváření balíčků najdete v tématu [Vytvoření a publikování balíčku pomocí rozhraní příkazového řádku dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="4c848-107">For examples of using these commands to create packages, see [Create and publish a package using the dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

<span data-ttu-id="4c848-108">Úplný odkaz na `dotnet` příkazy pro rozhraní příkazového řádku naleznete v tématu [.NET Core Command-line interface (CLI) Tools](/dotnet/core/tools/?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="4c848-108">For the complete command reference on `dotnet` CLI, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="4c848-109">Spotřeba balíčku</span><span class="sxs-lookup"><span data-stu-id="4c848-109">Package consumption</span></span>

- <span data-ttu-id="4c848-110">[**dotnet – přidat balíček**](/dotnet/core/tools/dotnet-add-package): Přidá odkaz na balíček do souboru projektu a potom spustí `dotnet restore` instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="4c848-110">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="4c848-111">[**dotnet odebrat balíček**](/dotnet/core/tools/dotnet-remove-package): Odebere odkaz na balíček ze souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="4c848-111">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="4c848-112">[**dotnet Restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Obnoví závislosti a nástroje projektu.</span><span class="sxs-lookup"><span data-stu-id="4c848-112">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="4c848-113">Od NuGet 4,0 to spustí stejný kód jako `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="4c848-113">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="4c848-114">[**dotnet – národní prostředí NuGet**](/dotnet/core/tools/dotnet-nuget-locals): Zobrazí seznam umístění *globálních balíčků*, *HTTP cache*a *dočasných* složek a vymaže obsah těchto složek.</span><span class="sxs-lookup"><span data-stu-id="4c848-114">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>
- <span data-ttu-id="4c848-115">[**dotnet New nugetconfig**](/dotnet/core/tools/dotnet-new): [`nuget.config`](../reference/nuget-config-file.md) Vytvoří soubor pro konfiguraci chování NuGet.</span><span class="sxs-lookup"><span data-stu-id="4c848-115">[**dotnet new nugetconfig**](/dotnet/core/tools/dotnet-new): Creates a [`nuget.config`](../reference/nuget-config-file.md) file to configure NuGet's behavior.</span></span>

## <a name="package-creation"></a><span data-ttu-id="4c848-116">Vytvoření balíčku</span><span class="sxs-lookup"><span data-stu-id="4c848-116">Package creation</span></span>

- <span data-ttu-id="4c848-117">[**sada dotnet Pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Zabalí kód do balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="4c848-117">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span>
- <span data-ttu-id="4c848-118">[**dotnet – vložení nugetu**](/dotnet/core/tools/dotnet-nuget-push): Publikuje balíček na server NuGet.</span><span class="sxs-lookup"><span data-stu-id="4c848-118">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Publishes a package to a NuGet server.</span></span> <span data-ttu-id="4c848-119">Platí pro nuget.org, Azure Artifacts a [servery NuGet třetích stran](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="4c848-119">Applicable to nuget.org, Azure Artifacts, and [third-party NuGet servers](../hosting-packages/overview.md).</span></span>
- <span data-ttu-id="4c848-120">[**dotnet NuGet Delete**](/dotnet/core/tools/dotnet-nuget-delete): Odstraní nebo zruší výpis balíčku ze serveru NuGet.</span><span class="sxs-lookup"><span data-stu-id="4c848-120">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a NuGet server.</span></span> <span data-ttu-id="4c848-121">Platí pro nuget.org, Azure Artifacts a [servery NuGet třetích stran](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="4c848-121">Applicable to nuget.org, Azure Artifacts, and [third-party NuGet servers](../hosting-packages/overview.md).</span></span>
