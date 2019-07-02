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
# <a name="dotnet-cli-commands"></a><span data-ttu-id="25d83-103">příkazy rozhraní příkazového řádku DotNet</span><span class="sxs-lookup"><span data-stu-id="25d83-103">dotnet CLI commands</span></span>

<span data-ttu-id="25d83-104">`dotnet` Rozhraní příkazového řádku (CLI), který běží na Windows, Mac OS X a Linux, nabízí celou řadu základních příkazech, jako je instalace, obnovení a publikování balíčků.</span><span class="sxs-lookup"><span data-stu-id="25d83-104">The `dotnet` command-line interface (CLI), which runs on Windows, Mac OS X, and Linux, provides a number of essential commands such as installing, restoring, and publishing packages.</span></span> <span data-ttu-id="25d83-105">Pokud se příkaz dotnet vyhovuje vašim potřebám, není nutné používat `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="25d83-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="25d83-106">Příklady použití těchto příkazů pro využívání balíčků naleznete v tématu [nainstalovat a spravovat balíčky pomocí rozhraní příkazového řádku dotnet](../consume-packages/install-use-packages-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="25d83-106">For examples of using these commands to consume packages, see [Install and manage packages using the dotnet CLI](../consume-packages/install-use-packages-dotnet-cli.md).</span></span> <span data-ttu-id="25d83-107">Příklady používání těchto příkazů k vytváření balíčků, najdete v článku [vytvoření a publikování balíčku pomocí rozhraní příkazového řádku dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="25d83-107">For examples of using these commands to create packages, see [Create and publish a package using the dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

<span data-ttu-id="25d83-108">Pro úplný příkaz odkaz na `dotnet` rozhraní příkazového řádku, naleznete v tématu [nástroje rozhraní příkazového řádku (CLI) pro .NET Core](/dotnet/core/tools/?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="25d83-108">For the complete command reference on `dotnet` CLI, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="25d83-109">Využití balíčků</span><span class="sxs-lookup"><span data-stu-id="25d83-109">Package consumption</span></span>

- <span data-ttu-id="25d83-110">[**příkaz DotNet add package**](/dotnet/core/tools/dotnet-add-package): Přidá odkaz na balíček do souboru projektu a pak spustí `dotnet restore` k instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="25d83-110">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="25d83-111">[**DotNet odebrat balíček**](/dotnet/core/tools/dotnet-remove-package): Odebere odkaz na balíček ze souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="25d83-111">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="25d83-112">[**DotNet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Obnoví závislostí a nástrojů projektu.</span><span class="sxs-lookup"><span data-stu-id="25d83-112">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="25d83-113">Od verze NuGet 4.0, toto řešení běží stejný kód jako `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="25d83-113">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="25d83-114">[**DotNet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Uvádí umístění *global-packages*, *http-cache*, a *temp* složky a vymaže obsah těchto složek.</span><span class="sxs-lookup"><span data-stu-id="25d83-114">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>
- <span data-ttu-id="25d83-115">[**nové nugetconfig DotNet**](/dotnet/core/tools/dotnet-new): Vytvoří [ `nuget.config` ](../reference/nuget-config-file.md) souboru konfigurace chování Nugetu.</span><span class="sxs-lookup"><span data-stu-id="25d83-115">[**dotnet new nugetconfig**](/dotnet/core/tools/dotnet-new): Creates a [`nuget.config`](../reference/nuget-config-file.md) file to configure NuGet's behavior.</span></span>

## <a name="package-creation"></a><span data-ttu-id="25d83-116">Vytvoření balíčku</span><span class="sxs-lookup"><span data-stu-id="25d83-116">Package creation</span></span>

- <span data-ttu-id="25d83-117">[**balíčku DotNet**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Sbalit kód do balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="25d83-117">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span>
- <span data-ttu-id="25d83-118">[**DotNet nuget nabízených**](/dotnet/core/tools/dotnet-nuget-push): Publikuje balíček NuGet server.</span><span class="sxs-lookup"><span data-stu-id="25d83-118">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Publishes a package to a NuGet server.</span></span> <span data-ttu-id="25d83-119">Lze použít na nuget.org, artefaktů Azure, a [servery NuGet třetích stran](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="25d83-119">Applicable to nuget.org, Azure Artifacts, and [third-party NuGet servers](../hosting-packages/overview.md).</span></span>
- <span data-ttu-id="25d83-120">[**Odstranit DotNet nuget**](/dotnet/core/tools/dotnet-nuget-delete): Odstraní nebo unlists balíček NuGet server.</span><span class="sxs-lookup"><span data-stu-id="25d83-120">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a NuGet server.</span></span> <span data-ttu-id="25d83-121">Lze použít na nuget.org, artefaktů Azure, a [servery NuGet třetích stran](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="25d83-121">Applicable to nuget.org, Azure Artifacts, and [third-party NuGet servers](../hosting-packages/overview.md).</span></span>
