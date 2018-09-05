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
# <a name="dotnet-commands"></a><span data-ttu-id="2689f-103">příkazy DotNet</span><span class="sxs-lookup"><span data-stu-id="2689f-103">dotnet commands</span></span>

<span data-ttu-id="2689f-104">`dotnet` Rozhraní příkazového řádku, který běží na Windows, Mac OS X a Linux, nabízí celou řadu základních nuget.exe příkazy, jak je uvedeno níže.</span><span class="sxs-lookup"><span data-stu-id="2689f-104">The `dotnet` command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="2689f-105">Pokud se příkaz dotnet vyhovuje vašim potřebám, není nutné používat `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="2689f-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="2689f-106">Úplné informace o `dotnet`, naleznete v tématu [nástroje rozhraní příkazového řádku (CLI) pro .NET Core](/dotnet/core/tools/?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="2689f-106">For complete information on `dotnet`, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="2689f-107">Využití balíčků</span><span class="sxs-lookup"><span data-stu-id="2689f-107">Package consumption</span></span>

- <span data-ttu-id="2689f-108">[**příkaz DotNet add package**](/dotnet/core/tools/dotnet-add-package): Přidá odkaz na balíček do souboru projektu a pak spustí `dotnet restore` k instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="2689f-108">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="2689f-109">[**DotNet odebrat balíček**](/dotnet/core/tools/dotnet-remove-package): Odebere odkaz na balíček ze souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="2689f-109">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="2689f-110">[**DotNet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Obnoví závislostí a nástrojů projektu.</span><span class="sxs-lookup"><span data-stu-id="2689f-110">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="2689f-111">Od verze NuGet 4.0, toto řešení běží stejný kód jako `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="2689f-111">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="2689f-112">[**DotNet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): uvádí umístění *global-packages*, *http-cache*, a *temp* složky a vymaže obsah Tyto složky.</span><span class="sxs-lookup"><span data-stu-id="2689f-112">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>

## <a name="package-creation"></a><span data-ttu-id="2689f-113">Vytvoření balíčku</span><span class="sxs-lookup"><span data-stu-id="2689f-113">Package creation</span></span>

- <span data-ttu-id="2689f-114">[**balíčku DotNet**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): balíčky kódu do balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="2689f-114">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="2689f-115">Od verze NuGet 4.0, toto řešení běží stejný kód jako `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="2689f-115">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="2689f-116">[**DotNet nuget nabízených**](/dotnet/core/tools/dotnet-nuget-push): odešle balíček na server a publikuje ji lze použít na nuget.org, Visual Studio Team Services a NuGet servery třetích stran.</span><span class="sxs-lookup"><span data-stu-id="2689f-116">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="2689f-117">[**Odstranit DotNet nuget**](/dotnet/core/tools/dotnet-nuget-delete): Odstraní nebo unlists balíček z hostitele, lze použít na nuget.org, Visual Studio Team Services a NuGet servery třetích stran.</span><span class="sxs-lookup"><span data-stu-id="2689f-117">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
