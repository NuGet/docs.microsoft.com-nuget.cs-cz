---
title: "příkazy pro balíčky NuGet dotNet. | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 0c81dbc4-2c14-4ec8-b87a-b802a899c3ea
description: "Krátký odkaz pro související NuGet příkazy, pomocí rozhraní příkazového řádku dotnet."
keywords: "příkazy pro balíčky NuGet DotNet, dotnet. pack, dotnet obnovení, dotnet nuget místní hodnoty –, dotnet nuget nabízené, odstranění nuget dotnet."
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7ff4779f46db102f1384650d82118b34fedd4413
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="dotnet-commands"></a><span data-ttu-id="4cb04-104">příkazy dotNet.</span><span class="sxs-lookup"><span data-stu-id="4cb04-104">dotNet commands</span></span>

<span data-ttu-id="4cb04-105">DotNet rozhraní příkazového řádku, který běží na systému Windows a Mac OS X, Linux, poskytuje řadu příkazů základní nuget.exe, jak je uvedeno dále.</span><span class="sxs-lookup"><span data-stu-id="4cb04-105">The DotNet command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="4cb04-106">Kde dotnet poskytuje požadované příkazy, není nutné stáhnout nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="4cb04-106">Where dotnet provides the desired commands, it is not necessary to download nuget.exe.</span></span>

- <span data-ttu-id="4cb04-107">[**DotNet pack**](https://docs.microsoft.com/dotnet/core/tools/dotnet-pack?tabs=netcore2x): sady kód pro NETCore SDK projekty do balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="4cb04-107">[**dotnet pack**](https://docs.microsoft.com/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs code for NETCore SDK projects into a NuGet package.</span></span> <span data-ttu-id="4cb04-108">Všechny ostatní typy projektu měli používat.[`nuget pack`](cli-ref-pack.md)</span><span class="sxs-lookup"><span data-stu-id="4cb04-108">All other project types should use [`nuget pack`](cli-ref-pack.md)</span></span>
- <span data-ttu-id="4cb04-109">[**obnovení DotNet**](https://docs.microsoft.com/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Obnoví závislosti a nástroje projektu.</span><span class="sxs-lookup"><span data-stu-id="4cb04-109">[**dotnet restore**](https://docs.microsoft.com/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="4cb04-110">Od verze NuGet 4.0, toto spouští stejný kód jako `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="4cb04-110">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="4cb04-111">[**místní hodnoty nuget DotNet**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-locals): vymaže nebo vypíše místní prostředky NuGet, jako je například http-požadavek mezipaměti, dočasnou vyrovnávací paměť nebo složku globální balíčky celého systému.</span><span class="sxs-lookup"><span data-stu-id="4cb04-111">[**dotnet nuget locals**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-locals): Clears or lists local NuGet resources such as http the -request cache, temporary cache, or machine-wide global packages folder.</span></span>
- <span data-ttu-id="4cb04-112">[**DotNet nuget nabízené**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-push): nabízených oznámení balíček na server a vydává je pro nuget.org, Visual Studio Team Services nebo všechny servery NuGet třetích stran.</span><span class="sxs-lookup"><span data-stu-id="4cb04-112">[**dotnet nuget push**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, or any third-party NuGet servers.</span></span>
- <span data-ttu-id="4cb04-113">[**Odstranit DotNet nuget**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-delete): Odstraní nebo unlists balíčku ze serveru, platí pro nuget.org, Visual Studio Team Services nebo všechny servery NuGet třetích stran.</span><span class="sxs-lookup"><span data-stu-id="4cb04-113">[**dotnet nuget delete**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a  server, applicable to nuget.org, Visual Studio Team Services, or any third-party NuGet servers.</span></span>
