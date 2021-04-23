---
title: Přehled NuGet.org
description: Přehled NuGet.org
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 2dac6ebd6367f3ed1a5ef9e81d843867a4a22f62
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901873"
---
# <a name="overview-of-nugetorg"></a><span data-ttu-id="0b641-103">Přehled NuGet.org</span><span class="sxs-lookup"><span data-stu-id="0b641-103">Overview of NuGet.org</span></span>

<span data-ttu-id="0b641-104">NuGet.org je veřejným hostitelem balíčků NuGet, které každý den pracují s miliony vývojářů .NET a .NET Core.</span><span class="sxs-lookup"><span data-stu-id="0b641-104">NuGet.org is a public host of NuGet packages that are employed by millions of .NET and .NET Core developers every day.</span></span>

## <a name="role-of-nugetorg-in-the-nuget-ecosystem"></a><span data-ttu-id="0b641-105">Role NuGet.org v ekosystému NuGet</span><span class="sxs-lookup"><span data-stu-id="0b641-105">Role of NuGet.org in the NuGet ecosystem</span></span>

<span data-ttu-id="0b641-106">NuGet.org sám v roli jako veřejný hostitel udržuje centrální úložiště více než 100 000 jedinečných balíčků na [NuGet.org](https://www.nuget.org). NuGet.org není jediným možným hostitelem pro balíčky.</span><span class="sxs-lookup"><span data-stu-id="0b641-106">In its role as a public host, NuGet.org itself maintains the central repository of over 100,000 unique packages at [nuget.org](https://www.nuget.org). NuGet.org is not the only possible host for packages.</span></span> <span data-ttu-id="0b641-107">Technologie NuGet také umožňuje hostovat balíčky soukromě v cloudu (například na Azure DevOps), v privátní síti nebo dokonce jenom v místním systému souborů.</span><span class="sxs-lookup"><span data-stu-id="0b641-107">The NuGet technology also enables you to host packages privately in the cloud (such as on Azure DevOps), on a private network, or even on just your local file system.</span></span> <span data-ttu-id="0b641-108">Pokud vás zajímá jiný hostitel nebo možnost hostování, přečtěte si téma [hostování vlastních kanálů NuGet](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="0b641-108">If you are interested in a different host or hosting option, see [Hosting your own NuGet feeds](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="0b641-109">NuGet.org, podobně jako jakýkoli hostitel pro balíčky NuGet, slouží jako bod připojení mezi *tvůrci* balíčků a *uživatele* balíčku.</span><span class="sxs-lookup"><span data-stu-id="0b641-109">NuGet.org, like any host for NuGet packages, serves as the point of connection between package *creators* and package *consumers*.</span></span> <span data-ttu-id="0b641-110">Tvůrci sestavují užitečné balíčky NuGet a publikují je.</span><span class="sxs-lookup"><span data-stu-id="0b641-110">Creators build useful NuGet packages and publish them.</span></span> <span data-ttu-id="0b641-111">Příjemci pak hledají užitečné a kompatibilní balíčky na dostupných hostitelích, stahují a zahrnují tyto balíčky v jejich projektech.</span><span class="sxs-lookup"><span data-stu-id="0b641-111">Consumers then search for useful and compatible packages on accessible hosts, downloading and including those packages in their projects.</span></span> <span data-ttu-id="0b641-112">Po instalaci v projektu jsou balíčky rozhraní API k dispozici pro zbytek kódu projektu.</span><span class="sxs-lookup"><span data-stu-id="0b641-112">Once installed in a project, the packages' APIs are available to the rest of the project code.</span></span>

![Vztah mezi tvůrci balíčků, hostiteli balíčků a příjemci balíčku](media/nuget-roles.png)

## <a name="accounts"></a><span data-ttu-id="0b641-114">Účty</span><span class="sxs-lookup"><span data-stu-id="0b641-114">Accounts</span></span>

<span data-ttu-id="0b641-115">Pokud chcete publikovat balíčky na NuGet.org, musíte nejdřív vytvořit [individuální (uživatelský) účet](individual-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="0b641-115">To publish packages on NuGet.org, you first create an [individual (user) account](individual-accounts.md).</span></span> <span data-ttu-id="0b641-116">Tím se vaše identita bude NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="0b641-116">This becomes your identity on NuGet.org.</span></span>

<span data-ttu-id="0b641-117">NuGet.org také umožňuje vytvořit [účet organizace](organizations-on-nuget-org.md).</span><span class="sxs-lookup"><span data-stu-id="0b641-117">NuGet.org also allows you to create an [organization account](organizations-on-nuget-org.md).</span></span> <span data-ttu-id="0b641-118">Účet organizace má jako členy jeden nebo více jednotlivých účtů.</span><span class="sxs-lookup"><span data-stu-id="0b641-118">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="0b641-119">Členové mohou spravovat sadu balíčků a přitom zachovat jedinou identitu pro vlastnictví.</span><span class="sxs-lookup"><span data-stu-id="0b641-119">Members can manage a set of packages while maintaining a single identity for ownership.</span></span> <span data-ttu-id="0b641-120">Prostřednictvím individuálního účtu můžete být členem libovolného počtu organizací.</span><span class="sxs-lookup"><span data-stu-id="0b641-120">Through your individual account, you can be a member of any number of organizations.</span></span>

<span data-ttu-id="0b641-121">Balíček může patřit k účtu organizace, jako by mohl patřit k individuálnímu účtu.</span><span class="sxs-lookup"><span data-stu-id="0b641-121">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="0b641-122">Uživatelé balíčku nevidí žádný rozdíl mezi jednotlivými účty nebo účtem organizace: obě se zobrazí jako balíčky `owners` .</span><span class="sxs-lookup"><span data-stu-id="0b641-122">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

## <a name="api-keys"></a><span data-ttu-id="0b641-123">Klíče rozhraní API</span><span class="sxs-lookup"><span data-stu-id="0b641-123">API keys</span></span>

<span data-ttu-id="0b641-124">Jakmile budete mít k publikování balíček NuGet (soubor *. nupkg* ), publikujete ho do NuGet.org pomocí rozhraní příkazového řádku nuget.exe nebo rozhraní příkazového řádku dotnet.exe, společně s [klíčem rozhraní API](scoped-api-keys.md) získaným z NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="0b641-124">Once you have a NuGet package (*.nupkg* file) to publish, you publish it to NuGet.org using either the nuget.exe CLI or the dotnet.exe CLI, along with an [API key](scoped-api-keys.md) acquired from NuGet.org.</span></span>

<span data-ttu-id="0b641-125">Když [publikujete balíček](../create-packages/creating-a-package.md), zahrnete do příkazu CLI hodnotu klíče rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="0b641-125">When you [publish a package](../create-packages/creating-a-package.md), you include the API key value in the CLI command.</span></span>

## <a name="id-prefixes"></a><span data-ttu-id="0b641-126">Předpony ID</span><span class="sxs-lookup"><span data-stu-id="0b641-126">ID prefixes</span></span>

<span data-ttu-id="0b641-127">Když publikujete balíčky, můžete si vyhradit a chránit svoji identitu tím, že si [zachováte předpony ID](id-prefix-reservation.md).</span><span class="sxs-lookup"><span data-stu-id="0b641-127">When you publish packages, you can reserve and protect your identity by [reserving ID prefixes](id-prefix-reservation.md).</span></span> <span data-ttu-id="0b641-128">Při instalaci balíčku jsou k dispozici příjemci balíčku s dalšími informacemi, které označují, že daný balíček je neklamný v jeho identifikačních vlastnostech.</span><span class="sxs-lookup"><span data-stu-id="0b641-128">When installing a package, package consumers are provided with additional information indicating that the package they are consuming is not deceptive in its identifying properties.</span></span>

## <a name="api-endpoint-for-nugetorg"></a><span data-ttu-id="0b641-129">Koncový bod rozhraní API pro NuGet.org</span><span class="sxs-lookup"><span data-stu-id="0b641-129">API endpoint for NuGet.org</span></span>

<span data-ttu-id="0b641-130">Pokud chcete používat NuGet.org jako úložiště balíčků s klienty NuGet, měli byste použít následující koncový bod rozhraní API V3:</span><span class="sxs-lookup"><span data-stu-id="0b641-130">To use NuGet.org as a package repository with NuGet clients, you should use the following V3 API endpoint:</span></span> 

`https://api.nuget.org/v3/index.json`

<span data-ttu-id="0b641-131">Starší klienti stále můžou k přístupu k NuGet.org používat protokol v2. Upozorňujeme však, že klienti NuGet 3,0 nebo novější budou mít pomalejší a méně spolehlivější službu pomocí protokolu v2:</span><span class="sxs-lookup"><span data-stu-id="0b641-131">Older clients can still use the V2 protocol to reach NuGet.org. However, please note, NuGet clients 3.0 or later will have slower and less reliable service using the V2 protocol:</span></span>

<span data-ttu-id="0b641-132">`https://www.nuget.org/api/v2` (**Protokol v2 je zastaralý!**)</span><span class="sxs-lookup"><span data-stu-id="0b641-132">`https://www.nuget.org/api/v2` (**The V2 protocol is deprecated!**)</span></span>
