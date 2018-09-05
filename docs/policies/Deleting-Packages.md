---
title: Odstranění balíčků NuGet z webu nuget.org
description: Zásady pro unlisting balíčky z nuget.org; trvalé odstranění není podporováno s výjimkou při balíčky narušit jiné zásady.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 901eb09711a6e32740c70829028da66b782870a0
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548125"
---
# <a name="deleting-packages"></a><span data-ttu-id="05a95-103">Odstranění balíčků</span><span class="sxs-lookup"><span data-stu-id="05a95-103">Deleting packages</span></span>

<span data-ttu-id="05a95-104">nuget.org nepodporuje trvalé odstranění balíčků.</span><span class="sxs-lookup"><span data-stu-id="05a95-104">nuget.org does not support permanent deletion of packages.</span></span> <span data-ttu-id="05a95-105">Mohlo by narušil každý projekt v závislosti na dostupnost balíčku, zejména s pracovních postupech sestavení, které se týkají obnovení balíčků.</span><span class="sxs-lookup"><span data-stu-id="05a95-105">Doing so would break every project depending on the availability of the package, especially with build workflows that involve package restore.</span></span>

<span data-ttu-id="05a95-106">nuget.org nemá podporuje *unlisting* balíček, což lze provést na stránce Správa balíčků na webové stránce.</span><span class="sxs-lookup"><span data-stu-id="05a95-106">nuget.org does supports *unlisting* a package, which can be done in the package management page on the web site.</span></span> <span data-ttu-id="05a95-107">Neuvedené v seznamu balíčků se nezobrazují na nuget.org nebo v Uživatelském rozhraní aplikace Visual Studio a ve výsledcích hledání nezobrazí.</span><span class="sxs-lookup"><span data-stu-id="05a95-107">Unlisted packages don't appear on nuget.org or in the Visual Studio UI, and do not appear in search results.</span></span> <span data-ttu-id="05a95-108">Neuvedené v seznamu balíčků, ale můžete dál stáhnout a nainstalovat pomocí čísla přesnou verzi, která podporuje obnovení balíčků.</span><span class="sxs-lookup"><span data-stu-id="05a95-108">Unlisted packages, however, can still be downloaded and installed by using an exact version number, which supports package restore.</span></span> <span data-ttu-id="05a95-109">Kromě toho může neuvedené v seznamu balíčků zjištěné stále v těchto konkrétních scénářích:</span><span class="sxs-lookup"><span data-stu-id="05a95-109">In addition, unlisted packages may still be discovered in the following specific scenarios:</span></span>

- <span data-ttu-id="05a95-110">Obnovení pomocí plovoucí verze balíčků (například `1.0.0-*`), pokud je nejnovější dostupný balíček odpovídající omezení verze nebo závislost neuvedené v seznamu balíčků.</span><span class="sxs-lookup"><span data-stu-id="05a95-110">Package restore using floating versions (for example, `1.0.0-*`), if the latest available package matching the version or dependency constraints is an unlisted package.</span></span>
- <span data-ttu-id="05a95-111">Replikace balíčků prostřednictvím katalogu (jako v katalogu obsahuje také neuvedené v seznamu balíčků).</span><span class="sxs-lookup"><span data-stu-id="05a95-111">Replication of packages through the catalog (as the catalog also contains unlisted packages).</span></span>

## <a name="exceptions"></a><span data-ttu-id="05a95-112">Výjimky</span><span class="sxs-lookup"><span data-stu-id="05a95-112">Exceptions</span></span>

<span data-ttu-id="05a95-113">Ve výjimečných případech například porušení autorských práv a potenciálně nebezpečný obsah balíčků můžete odstranit ručně týmu NuGet.</span><span class="sxs-lookup"><span data-stu-id="05a95-113">In exceptional situations such as copyright infringement and potentially harmful content, packages can be deleted manually by the NuGet team.</span></span> <span data-ttu-id="05a95-114">Odeslat žádost o podporu prostřednictvím [Galerie NuGet](http://www.nuget.org) zahájíte proces.</span><span class="sxs-lookup"><span data-stu-id="05a95-114">Submit a support request through [NuGet Gallery](http://www.nuget.org) to start the process.</span></span>

## <a name="prohibited-use"></a><span data-ttu-id="05a95-115">Zakázané použití</span><span class="sxs-lookup"><span data-stu-id="05a95-115">Prohibited use</span></span>

<span data-ttu-id="05a95-116">Balíčky, které splnit některý z následujících kritérií nejsou povolené u veřejné Galerie NuGet a okamžitě odeberou bez diskuse.</span><span class="sxs-lookup"><span data-stu-id="05a95-116">Packages that meet any of the following criteria are not allowed on the public NuGet gallery and will be immediately removed without discussion.</span></span> <span data-ttu-id="05a95-117">Balíček se vlastníci, ale, informováni o odebrání.</span><span class="sxs-lookup"><span data-stu-id="05a95-117">Package owners will, however, be notified of the removal.</span></span>

- <span data-ttu-id="05a95-118">Obsahuje malwaru, adwaru nebo jakýkoli druh spyware.</span><span class="sxs-lookup"><span data-stu-id="05a95-118">Contains malware, adware, or any kind of spyware.</span></span>
- <span data-ttu-id="05a95-119">Jsou navržené k jejich poškození pracovní stanici vývojáře nebo jejich organizace.</span><span class="sxs-lookup"><span data-stu-id="05a95-119">Are designed to harm a developer's workstation or their organization.</span></span>
- <span data-ttu-id="05a95-120">Porušuje autorská práva nebo licence je v rozporu.</span><span class="sxs-lookup"><span data-stu-id="05a95-120">Infringes copyrights or violates licenses.</span></span>
- <span data-ttu-id="05a95-121">Obsahuje neplatný obsah.</span><span class="sxs-lookup"><span data-stu-id="05a95-121">Contains illegal content.</span></span>
- <span data-ttu-id="05a95-122">Používají se k přikrčené na identifikátory balíček, včetně balíčků, které nemají žádnou produktivní obsah.</span><span class="sxs-lookup"><span data-stu-id="05a95-122">Are being used to squat on package identifiers, including packages that have zero productive content.</span></span> <span data-ttu-id="05a95-123">Balíčky musí obsahovat kód nebo vlastníci musí protihráči postoupit identifikátor někomu, kdo má ve skutečnosti produktu k odeslání.</span><span class="sxs-lookup"><span data-stu-id="05a95-123">Packages must contain code or the owners must concede the identifier to someone who actually has a product to ship.</span></span>
- <span data-ttu-id="05a95-124">Pokus o galerii, která je navržená nejsou explicitně udělat něco udělat.</span><span class="sxs-lookup"><span data-stu-id="05a95-124">Attempt to make the gallery do something that it's not explicitly designed to do.</span></span>

<span data-ttu-id="05a95-125">Pokud zjistíte balíček, který je v rozporu s libovolnou z těchto položek, klikněte na tlačítko **ohlášení zneužití** odkaz na stránce s podrobnostmi balíčku a odeslat sestavu.</span><span class="sxs-lookup"><span data-stu-id="05a95-125">If you find a package that is in violation of any of these items, click the **Report Abuse** link on the package details page and submit a report.</span></span>

<span data-ttu-id="05a95-126">Všimněte si, že tým NuGet a .NET Foundation vyhrazuje právo kdykoli změnit tato kritéria.</span><span class="sxs-lookup"><span data-stu-id="05a95-126">Note that the NuGet team and the .NET Foundation reserves the right to change these criteria at any time.</span></span>
