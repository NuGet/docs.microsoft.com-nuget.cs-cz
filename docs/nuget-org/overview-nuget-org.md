---
title: Přehled NuGet.org
description: Přehled NuGet.org
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 9a75ecbc589afa664e5684005e077b02913e8039
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427521"
---
# <a name="overview-of-nugetorg"></a><span data-ttu-id="88de9-103">Přehled NuGet.org</span><span class="sxs-lookup"><span data-stu-id="88de9-103">Overview of NuGet.org</span></span>

<span data-ttu-id="88de9-104">NuGet.org je veřejný hostitel balíčků NuGet, které se použijí podle miliony vývojářů .NET a .NET Core každý den.</span><span class="sxs-lookup"><span data-stu-id="88de9-104">NuGet.org is a public host of NuGet packages that are employed by millions of .NET and .NET Core developers every day.</span></span>

## <a name="role-of-nugetorg-in-the-nuget-ecosystem"></a><span data-ttu-id="88de9-105">Role NuGet.org do ekosystému a NuGet</span><span class="sxs-lookup"><span data-stu-id="88de9-105">Role of NuGet.org in the NuGet ecosystem</span></span>

<span data-ttu-id="88de9-106">V jeho role jako veřejný hostitel NuGet.org, sama udržuje centrálním úložišti víc než 100 000 jedinečné balíčky v [nuget.org](https://www.nuget.org). NuGet.org není možné dosáhnout pouze hostitelem pro balíčky.</span><span class="sxs-lookup"><span data-stu-id="88de9-106">In its role as a public host, NuGet.org itself maintains the central repository of over 100,000 unique packages at [nuget.org](https://www.nuget.org). NuGet.org is not the only possible host for packages.</span></span> <span data-ttu-id="88de9-107">Technologie NuGet také umožňuje hostování balíčků soukromě v cloudu (například na Azure DevOps), v privátní síti, nebo dokonce i na právě vašeho místního systému souborů.</span><span class="sxs-lookup"><span data-stu-id="88de9-107">The NuGet technology also enables you to host packages privately in the cloud (such as on Azure DevOps), on a private network, or even on just your local file system.</span></span> <span data-ttu-id="88de9-108">Pokud vás zajímají jiného hostitele nebo možnost hostování, přečtěte si téma [hostování vlastní kanály NuGet](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="88de9-108">If you are interested in a different host or hosting option, see [Hosting your own NuGet feeds](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="88de9-109">NuGet.org, stejně jako všechny hostitele pro balíčky NuGet, slouží jako bod připojení mezi balíček *creators* a balíček *příjemci*.</span><span class="sxs-lookup"><span data-stu-id="88de9-109">NuGet.org, like any host for NuGet packages, serves as the point of connection between package *creators* and package *consumers*.</span></span> <span data-ttu-id="88de9-110">Tvůrce sestavení užitečné balíčky NuGet a publikujte je.</span><span class="sxs-lookup"><span data-stu-id="88de9-110">Creators build useful NuGet packages and publish them.</span></span> <span data-ttu-id="88de9-111">Příjemci vyhledejte balíčky užitečné a kompatibilní na hostitelích přístupné, stahování a včetně těchto balíčků ve svých projektech.</span><span class="sxs-lookup"><span data-stu-id="88de9-111">Consumers then search for useful and compatible packages on accessible hosts, downloading and including those packages in their projects.</span></span> <span data-ttu-id="88de9-112">Po instalaci v projektu, rozhraní API balíčky jsou k dispozici pro zbývající část kódu projektu.</span><span class="sxs-lookup"><span data-stu-id="88de9-112">Once installed in a project, the packages' APIs are available to the rest of the project code.</span></span>

![Vztah mezi Tvůrce balíčku, balíčku hostitele a spotřebitele balíčku](media/nuget-roles.png)

## <a name="accounts"></a><span data-ttu-id="88de9-114">Účty</span><span class="sxs-lookup"><span data-stu-id="88de9-114">Accounts</span></span>

<span data-ttu-id="88de9-115">Publikování balíčků na NuGet.org, je třeba nejprve vytvořit [osoba (uživatel) účtu](individual-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="88de9-115">To publish packages on NuGet.org, you first create an [individual (user) account](individual-accounts.md).</span></span> <span data-ttu-id="88de9-116">To se stane svoji identitu na NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="88de9-116">This becomes your identity on NuGet.org.</span></span>

<span data-ttu-id="88de9-117">NuGet.org také umožňuje vytvořit [účet organizace](organizations-on-nuget-org.md).</span><span class="sxs-lookup"><span data-stu-id="88de9-117">NuGet.org also allows you to create an [organization account](organizations-on-nuget-org.md).</span></span> <span data-ttu-id="88de9-118">Účet organizace má jeden nebo více samostatné účty jako členy.</span><span class="sxs-lookup"><span data-stu-id="88de9-118">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="88de9-119">Členové mohou spravovat sadu balíčků při zachování jedinou identitu pro vlastnictví.</span><span class="sxs-lookup"><span data-stu-id="88de9-119">Members can manage a set of packages while maintaining a single identity for ownership.</span></span> <span data-ttu-id="88de9-120">Pomocí svého individuálního účtu může být členem jakékoli číslo organizace.</span><span class="sxs-lookup"><span data-stu-id="88de9-120">Through your individual account, you can be a member of any number of organizations.</span></span>

<span data-ttu-id="88de9-121">Balíček může patřit k účtu organizace jako můžou patřit do individuálního účtu.</span><span class="sxs-lookup"><span data-stu-id="88de9-121">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="88de9-122">Balíček příjemci nezobrazuje žádný rozdíl mezi samostatný účet nebo účet organizace: oba se objeví jako balíček `owners`.</span><span class="sxs-lookup"><span data-stu-id="88de9-122">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

## <a name="api-keys"></a><span data-ttu-id="88de9-123">Klíče rozhraní API</span><span class="sxs-lookup"><span data-stu-id="88de9-123">API keys</span></span>

<span data-ttu-id="88de9-124">Jakmile budete mít balíčku NuGet ( *.nupkg* souboru) k publikování, ji publikujete do pomocí rozhraní příkazového řádku nuget.exe nebo dotnet.exe rozhraní příkazového řádku, spolu s NuGet.org [klíč rozhraní API](scoped-api-keys.md) získaných z NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="88de9-124">Once you have a NuGet package (*.nupkg* file) to publish, you publish it to NuGet.org using either the nuget.exe CLI or the dotnet.exe CLI, along with an [API key](scoped-api-keys.md) acquired from NuGet.org.</span></span>

<span data-ttu-id="88de9-125">Pokud jste [publikování balíčku](../create-packages/creating-a-package.md), zahrnují hodnotu klíče rozhraní API v příkazu rozhraní příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="88de9-125">When you [publish a package](../create-packages/creating-a-package.md), you include the API key value in the CLI command.</span></span>

## <a name="id-prefixes"></a><span data-ttu-id="88de9-126">Předpony ID</span><span class="sxs-lookup"><span data-stu-id="88de9-126">ID prefixes</span></span>

<span data-ttu-id="88de9-127">Při publikování balíčků si můžete rezervovat a chránit vaši identitu pomocí [rezervace předpony ID](id-prefix-reservation.md).</span><span class="sxs-lookup"><span data-stu-id="88de9-127">When you publish packages, you can reserve and protect your identity by [reserving ID prefixes](id-prefix-reservation.md).</span></span> <span data-ttu-id="88de9-128">Při instalaci balíčku, balíčku příjemci jsou k dispozici společně s dalšími informacemi označující, že balíček, který se spotřebovávají není podvodný v jeho identifikující vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="88de9-128">When installing a package, package consumers are provided with additional information indicating that the package they are consuming is not deceptive in its identifying properties.</span></span>

## <a name="api-endpoint-for-nugetorg"></a><span data-ttu-id="88de9-129">Koncový bod rozhraní API pro NuGet.org</span><span class="sxs-lookup"><span data-stu-id="88de9-129">API endpoint for NuGet.org</span></span>

<span data-ttu-id="88de9-130">Pokud chcete použít jako úložiště balíčků s klienty NuGet NuGet.org, měli byste použít následující koncový bod rozhraní API V3:</span><span class="sxs-lookup"><span data-stu-id="88de9-130">To use NuGet.org as a package repository with NuGet clients, you should use the following V3 API endpoint:</span></span> 

`https://api.nuget.org/v3/index.json`

<span data-ttu-id="88de9-131">Starší klienti stále může použít protokol V2 k dosažení NuGet.org. Upozorňujeme, klienti 3.0 nebo vyšší budou mít nižší a méně spolehlivé služby pomocí protokolu V2 NuGet:</span><span class="sxs-lookup"><span data-stu-id="88de9-131">Older clients can still use the V2 protocol to reach NuGet.org. However, please note, NuGet clients 3.0 or later will have slower and less reliable service using the V2 protocol:</span></span>

<span data-ttu-id="88de9-132">`https://www.nuget.org/api/v2` (**Protokol the V2 sítě se již nepoužívá.** )</span><span class="sxs-lookup"><span data-stu-id="88de9-132">`https://www.nuget.org/api/v2` (**The V2 prototcol is deprecated!**)</span></span>
