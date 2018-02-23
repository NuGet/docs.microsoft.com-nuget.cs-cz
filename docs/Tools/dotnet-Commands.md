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
# <a name="dotnet-commands"></a><span data-ttu-id="96e20-104">příkazy dotNet.</span><span class="sxs-lookup"><span data-stu-id="96e20-104">dotNet commands</span></span>

<span data-ttu-id="96e20-105">`dotnet` Rozhraní příkazového řádku, který běží na systému Windows a Mac OS X, Linux, poskytuje řadu příkazy nezbytné nuget.exe, jak je uvedeno dále.</span><span class="sxs-lookup"><span data-stu-id="96e20-105">The `dotnet` command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="96e20-106">Pokud dotnet nevyhovuje vašim požadavkům, není nutné používat `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="96e20-106">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="96e20-107">Úplné informace o `dotnet`, najdete v části [nástrojů rozhraní příkazového řádku (CLI) .NET Core](/dotnet/core/tools/?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="96e20-107">For complete information on `dotnet`, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="96e20-108">Balíček spotřeba</span><span class="sxs-lookup"><span data-stu-id="96e20-108">Package consumption</span></span>

- <span data-ttu-id="96e20-109">[**DotNet. Přidejte balíček**](/dotnet/core/tools/dotnet-add-package): Přidá odkaz na soubor projektu balíček a potom spustí `dotnet restore` k instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="96e20-109">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="96e20-110">[**DotNet. odeberte balíček**](/dotnet/core/tools/dotnet-remove-package): Odebere odkaz balíčku ze souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="96e20-110">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="96e20-111">[**obnovení DotNet**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Obnoví závislosti a nástroje projektu.</span><span class="sxs-lookup"><span data-stu-id="96e20-111">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="96e20-112">Od verze NuGet 4.0, toto spouští stejný kód jako `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="96e20-112">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="96e20-113">[**místní hodnoty nuget DotNet**](/dotnet/core/tools/dotnet-nuget-locals): vymaže nebo vypíše místní prostředky NuGet například mezipaměti požadavek http, dočasnou vyrovnávací paměť a složce globální balíčky celého systému.</span><span class="sxs-lookup"><span data-stu-id="96e20-113">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Clears or lists local NuGet resources such as the http-request cache, the temporary cache, and the machine-wide global packages folder.</span></span>

## <a name="package-creation"></a><span data-ttu-id="96e20-114">Vytvoření balíčku</span><span class="sxs-lookup"><span data-stu-id="96e20-114">Package creation</span></span>

- <span data-ttu-id="96e20-115">[**DotNet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): sady kód do balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="96e20-115">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="96e20-116">Od verze NuGet 4.0, toto spouští stejný kód jako `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="96e20-116">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="96e20-117">[**DotNet nuget nabízené**](/dotnet/core/tools/dotnet-nuget-push): nabízených oznámení balíček na server a vydává je pro nuget.org, Visual Studio Team Services a servery NuGet třetích stran.</span><span class="sxs-lookup"><span data-stu-id="96e20-117">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="96e20-118">[**Odstranit DotNet nuget**](/dotnet/core/tools/dotnet-nuget-delete): Odstraní nebo unlists balíček z hostitele, platí pro nuget.org, Visual Studio Team Services a servery NuGet třetích stran.</span><span class="sxs-lookup"><span data-stu-id="96e20-118">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
