---
title: příkazy pro balíčky NuGet DotNet.
description: Krátký odkaz pro související NuGet příkazy, pomocí rozhraní příkazového řádku dotnet.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/23/2018
ms.topic: conceptual
ms.openlocfilehash: fe49274af339c987d5e090c99edd78f62f59ce47
ms.sourcegitcommit: 5fcd6d664749aa720359104ef7a66d38aeecadc2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/27/2018
---
# <a name="dotnet-commands"></a><span data-ttu-id="bef4d-103">příkazy DotNet.</span><span class="sxs-lookup"><span data-stu-id="bef4d-103">dotnet commands</span></span>

<span data-ttu-id="bef4d-104">`dotnet` Rozhraní příkazového řádku, který běží na systému Windows a Mac OS X, Linux, poskytuje řadu příkazy nezbytné nuget.exe, jak je uvedeno dále.</span><span class="sxs-lookup"><span data-stu-id="bef4d-104">The `dotnet` command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="bef4d-105">Pokud dotnet nevyhovuje vašim požadavkům, není nutné používat `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="bef4d-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="bef4d-106">Úplné informace o `dotnet`, najdete v části [nástrojů rozhraní příkazového řádku (CLI) .NET Core](/dotnet/core/tools/?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="bef4d-106">For complete information on `dotnet`, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="bef4d-107">Balíček spotřeba</span><span class="sxs-lookup"><span data-stu-id="bef4d-107">Package consumption</span></span>

- <span data-ttu-id="bef4d-108">[**DotNet. Přidejte balíček**](/dotnet/core/tools/dotnet-add-package): Přidá odkaz na soubor projektu balíček a potom spustí `dotnet restore` k instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="bef4d-108">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="bef4d-109">[**DotNet. odeberte balíček**](/dotnet/core/tools/dotnet-remove-package): Odebere odkaz balíčku ze souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="bef4d-109">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="bef4d-110">[**obnovení DotNet**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Obnoví závislosti a nástroje projektu.</span><span class="sxs-lookup"><span data-stu-id="bef4d-110">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="bef4d-111">Od verze NuGet 4.0, toto spouští stejný kód jako `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="bef4d-111">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="bef4d-112">[**místní hodnoty nuget DotNet**](/dotnet/core/tools/dotnet-nuget-locals): uvádí umístění *globální balíčky*, *http mezipaměti*, a *temp* složek a vymaže obsah Tyto složky.</span><span class="sxs-lookup"><span data-stu-id="bef4d-112">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>

## <a name="package-creation"></a><span data-ttu-id="bef4d-113">Vytvoření balíčku</span><span class="sxs-lookup"><span data-stu-id="bef4d-113">Package creation</span></span>

- <span data-ttu-id="bef4d-114">[**DotNet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): sady kód do balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="bef4d-114">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="bef4d-115">Od verze NuGet 4.0, toto spouští stejný kód jako `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="bef4d-115">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="bef4d-116">[**DotNet nuget nabízené**](/dotnet/core/tools/dotnet-nuget-push): nabízených oznámení balíček na server a vydává je pro nuget.org, Visual Studio Team Services a servery NuGet třetích stran.</span><span class="sxs-lookup"><span data-stu-id="bef4d-116">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="bef4d-117">[**Odstranit DotNet nuget**](/dotnet/core/tools/dotnet-nuget-delete): Odstraní nebo unlists balíček z hostitele, platí pro nuget.org, Visual Studio Team Services a servery NuGet třetích stran.</span><span class="sxs-lookup"><span data-stu-id="bef4d-117">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
