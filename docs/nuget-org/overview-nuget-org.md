---
title: Přehled NuGet.org
description: Přehled NuGet.org
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 9a75ecbc589afa664e5684005e077b02913e8039
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427521"
---
# <a name="overview-of-nugetorg"></a><span data-ttu-id="d8e82-103">Přehled NuGet.org</span><span class="sxs-lookup"><span data-stu-id="d8e82-103">Overview of NuGet.org</span></span>

<span data-ttu-id="d8e82-104">NuGet.org je veřejný hostitel balíčků NuGet, které jsou zaměstnány miliony vývojářů .NET a .NET Core každý den.</span><span class="sxs-lookup"><span data-stu-id="d8e82-104">NuGet.org is a public host of NuGet packages that are employed by millions of .NET and .NET Core developers every day.</span></span>

## <a name="role-of-nugetorg-in-the-nuget-ecosystem"></a><span data-ttu-id="d8e82-105">Úloha NuGet.org v ekosystému NuGet</span><span class="sxs-lookup"><span data-stu-id="d8e82-105">Role of NuGet.org in the NuGet ecosystem</span></span>

<span data-ttu-id="d8e82-106">Ve své roli veřejného hostitele, NuGet.org sám udržuje centrální úložiště více než 100.000 unikátních balíčků na [nuget.org](https://www.nuget.org). NuGet.org není jediným možným hostitelem pro balíčky.</span><span class="sxs-lookup"><span data-stu-id="d8e82-106">In its role as a public host, NuGet.org itself maintains the central repository of over 100,000 unique packages at [nuget.org](https://www.nuget.org). NuGet.org is not the only possible host for packages.</span></span> <span data-ttu-id="d8e82-107">Technologie NuGet také umožňuje hostovat balíčky soukromě v cloudu (například na Azure DevOps), v privátní síti nebo dokonce pouze v místním systému souborů.</span><span class="sxs-lookup"><span data-stu-id="d8e82-107">The NuGet technology also enables you to host packages privately in the cloud (such as on Azure DevOps), on a private network, or even on just your local file system.</span></span> <span data-ttu-id="d8e82-108">Máte-li zájem o jiný hostitel nebo možnost hostování, viz [Hostování vlastních nugetových kanálů](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="d8e82-108">If you are interested in a different host or hosting option, see [Hosting your own NuGet feeds](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="d8e82-109">NuGet.org, stejně jako každý hostitel pro balíčky NuGet, slouží jako bod spojení mezi *tvůrci* balíčků a *příjemci*balíčků .</span><span class="sxs-lookup"><span data-stu-id="d8e82-109">NuGet.org, like any host for NuGet packages, serves as the point of connection between package *creators* and package *consumers*.</span></span> <span data-ttu-id="d8e82-110">Tvůrci vytvářet užitečné balíčky NuGet a publikovat je.</span><span class="sxs-lookup"><span data-stu-id="d8e82-110">Creators build useful NuGet packages and publish them.</span></span> <span data-ttu-id="d8e82-111">Spotřebitelé pak vyhledávají užitečné a kompatibilní balíčky na přístupných hostitelích, stahují a zařazují tyto balíčky do svých projektů.</span><span class="sxs-lookup"><span data-stu-id="d8e82-111">Consumers then search for useful and compatible packages on accessible hosts, downloading and including those packages in their projects.</span></span> <span data-ttu-id="d8e82-112">Po instalaci v projektu jsou rozhraní API balíčků k dispozici pro zbytek kódu projektu.</span><span class="sxs-lookup"><span data-stu-id="d8e82-112">Once installed in a project, the packages' APIs are available to the rest of the project code.</span></span>

![Vztah mezi tvůrci balíčků, hostiteli balíčků a příjemci balíčků](media/nuget-roles.png)

## <a name="accounts"></a><span data-ttu-id="d8e82-114">Účty</span><span class="sxs-lookup"><span data-stu-id="d8e82-114">Accounts</span></span>

<span data-ttu-id="d8e82-115">Chcete-li publikovat balíčky na NuGet.org, nejprve vytvořte [individuální (uživatelský) účet](individual-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="d8e82-115">To publish packages on NuGet.org, you first create an [individual (user) account](individual-accounts.md).</span></span> <span data-ttu-id="d8e82-116">To se stane vaší identitou na NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="d8e82-116">This becomes your identity on NuGet.org.</span></span>

<span data-ttu-id="d8e82-117">NuGet.org také umožňuje vytvořit [účet organizace](organizations-on-nuget-org.md).</span><span class="sxs-lookup"><span data-stu-id="d8e82-117">NuGet.org also allows you to create an [organization account](organizations-on-nuget-org.md).</span></span> <span data-ttu-id="d8e82-118">Účet organizace má jeden nebo více individuálních účtů jako své členy.</span><span class="sxs-lookup"><span data-stu-id="d8e82-118">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="d8e82-119">Členové mohou spravovat sadu balíčků při zachování jedné identity pro vlastnictví.</span><span class="sxs-lookup"><span data-stu-id="d8e82-119">Members can manage a set of packages while maintaining a single identity for ownership.</span></span> <span data-ttu-id="d8e82-120">Prostřednictvím svého individuálního účtu můžete být členem libovolného počtu organizací.</span><span class="sxs-lookup"><span data-stu-id="d8e82-120">Through your individual account, you can be a member of any number of organizations.</span></span>

<span data-ttu-id="d8e82-121">Balíček může patřit k účtu organizace, stejně jako může patřit k individuálnímu účtu.</span><span class="sxs-lookup"><span data-stu-id="d8e82-121">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="d8e82-122">Spotřebitelé balíčků nevidí žádný rozdíl mezi individuálním účtem nebo účtem organizace: oba se zobrazují jako balíček `owners`.</span><span class="sxs-lookup"><span data-stu-id="d8e82-122">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

## <a name="api-keys"></a><span data-ttu-id="d8e82-123">Klíče rozhraní API</span><span class="sxs-lookup"><span data-stu-id="d8e82-123">API keys</span></span>

<span data-ttu-id="d8e82-124">Jakmile máte balíček NuGet (*soubor .nupkg)* publikovat do NuGet.org pomocí rozhraní api nuget.exe nebo dotnet.exe CLI, spolu s [klíčem rozhraní API](scoped-api-keys.md) získaného z NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="d8e82-124">Once you have a NuGet package (*.nupkg* file) to publish, you publish it to NuGet.org using either the nuget.exe CLI or the dotnet.exe CLI, along with an [API key](scoped-api-keys.md) acquired from NuGet.org.</span></span>

<span data-ttu-id="d8e82-125">Při [publikování balíčku](../create-packages/creating-a-package.md)zahrnete hodnotu klíče rozhraní API do příkazu příkazu příkazu příkazu příkazu příkazu.</span><span class="sxs-lookup"><span data-stu-id="d8e82-125">When you [publish a package](../create-packages/creating-a-package.md), you include the API key value in the CLI command.</span></span>

## <a name="id-prefixes"></a><span data-ttu-id="d8e82-126">ID předpony</span><span class="sxs-lookup"><span data-stu-id="d8e82-126">ID prefixes</span></span>

<span data-ttu-id="d8e82-127">Při publikování balíčků můžete rezervovat a chránit svou identitu [rezervací předponek ID](id-prefix-reservation.md).</span><span class="sxs-lookup"><span data-stu-id="d8e82-127">When you publish packages, you can reserve and protect your identity by [reserving ID prefixes](id-prefix-reservation.md).</span></span> <span data-ttu-id="d8e82-128">Při instalaci balíčku jsou příjemci balíčku opatřeni dalšími informacemi, které označují, že balíček, který spotřebovávají, neklame ve svých identifikačních vlastnostech.</span><span class="sxs-lookup"><span data-stu-id="d8e82-128">When installing a package, package consumers are provided with additional information indicating that the package they are consuming is not deceptive in its identifying properties.</span></span>

## <a name="api-endpoint-for-nugetorg"></a><span data-ttu-id="d8e82-129">Koncový bod rozhraní API pro NuGet.org</span><span class="sxs-lookup"><span data-stu-id="d8e82-129">API endpoint for NuGet.org</span></span>

<span data-ttu-id="d8e82-130">Chcete-li použít NuGet.org jako úložiště balíčků s klienty NuGet, měli byste použít následující koncový bod rozhraní API V3:</span><span class="sxs-lookup"><span data-stu-id="d8e82-130">To use NuGet.org as a package repository with NuGet clients, you should use the following V3 API endpoint:</span></span> 

`https://api.nuget.org/v3/index.json`

<span data-ttu-id="d8e82-131">Starší klienti mohou stále používat protokol V2 k dosažení NuGet.org. Upozorňujeme však, že klienti NuGet 3.0 nebo novější budou mít pomalejší a méně spolehlivé služby pomocí protokolu V2:</span><span class="sxs-lookup"><span data-stu-id="d8e82-131">Older clients can still use the V2 protocol to reach NuGet.org. However, please note, NuGet clients 3.0 or later will have slower and less reliable service using the V2 protocol:</span></span>

<span data-ttu-id="d8e82-132">`https://www.nuget.org/api/v2`**(Prototcol V2 je zastaralá!**)</span><span class="sxs-lookup"><span data-stu-id="d8e82-132">`https://www.nuget.org/api/v2` (**The V2 prototcol is deprecated!**)</span></span>
