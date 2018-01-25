---
title: "příkazy pro balíčky NuGet dotNet. | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Krátký odkaz pro související NuGet příkazy, pomocí rozhraní příkazového řádku dotnet."
keywords: "příkazy pro balíčky NuGet DotNet, dotnet. pack, dotnet obnovení, dotnet nuget místní hodnoty –, dotnet nuget nabízené, odstranění nuget dotnet."
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d06e4590ab87b68e7846a13b2eba0f59eb9529d6
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
---
# <a name="dotnet-commands"></a><span data-ttu-id="22b96-104">příkazy dotNet.</span><span class="sxs-lookup"><span data-stu-id="22b96-104">dotNet commands</span></span>

<span data-ttu-id="22b96-105">DotNet rozhraní příkazového řádku, který běží na systému Windows a Mac OS X, Linux, poskytuje řadu příkazů základní nuget.exe, jak je uvedeno dále.</span><span class="sxs-lookup"><span data-stu-id="22b96-105">The DotNet command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="22b96-106">Kde dotnet poskytuje požadované příkazy, není nutné stáhnout nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="22b96-106">Where dotnet provides the desired commands, it's not necessary to download nuget.exe.</span></span>

- <span data-ttu-id="22b96-107">[**DotNet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): sady kód do balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="22b96-107">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="22b96-108">Od verze NuGet 4.0, toto spouští stejný kód jako `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="22b96-108">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="22b96-109">[**obnovení DotNet**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Obnoví závislosti a nástroje projektu.</span><span class="sxs-lookup"><span data-stu-id="22b96-109">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="22b96-110">Od verze NuGet 4.0, toto spouští stejný kód jako `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="22b96-110">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="22b96-111">[**místní hodnoty nuget DotNet**](/dotnet/core/tools/dotnet-nuget-locals): vymaže nebo vypíše místní prostředky NuGet, jako je například http-požadavek mezipaměti, dočasnou vyrovnávací paměť nebo složku globální balíčky celého systému.</span><span class="sxs-lookup"><span data-stu-id="22b96-111">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Clears or lists local NuGet resources such as http the -request cache, temporary cache, or machine-wide global packages folder.</span></span>
- <span data-ttu-id="22b96-112">[**DotNet nuget nabízené**](/dotnet/core/tools/dotnet-nuget-push): nabízených oznámení balíček na server a vydává je pro nuget.org, Visual Studio Team Services nebo všechny servery NuGet třetích stran.</span><span class="sxs-lookup"><span data-stu-id="22b96-112">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, or any third-party NuGet servers.</span></span>
- <span data-ttu-id="22b96-113">[**Odstranit DotNet nuget**](/dotnet/core/tools/dotnet-nuget-delete): Odstraní nebo unlists balíčku ze serveru, platí pro nuget.org, Visual Studio Team Services nebo všechny servery NuGet třetích stran.</span><span class="sxs-lookup"><span data-stu-id="22b96-113">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a  server, applicable to nuget.org, Visual Studio Team Services, or any third-party NuGet servers.</span></span>
