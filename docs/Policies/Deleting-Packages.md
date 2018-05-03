---
title: Odstranění balíčků NuGet z nuget.org
description: Zásady pro unlisting balíčky z nuget.org; trvalé odstranění nepodporuje kromě při balíčky porušují jiné zásady.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: bea4f1589f184d38da27e5d82c3ce17a183fbdd1
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
---
# <a name="deleting-packages"></a><span data-ttu-id="941cc-103">Odstraněním balíčků</span><span class="sxs-lookup"><span data-stu-id="941cc-103">Deleting packages</span></span>

<span data-ttu-id="941cc-104">nuget.org nepodporuje trvalé odstranění balíčků.</span><span class="sxs-lookup"><span data-stu-id="941cc-104">nuget.org does not support permanent deletion of packages.</span></span> <span data-ttu-id="941cc-105">Tím by došlo k přerušení všechny projekty v závislosti na dostupnost balíčku, zejména s pracovními postupy sestavení, které zahrnují obnovení balíčků.</span><span class="sxs-lookup"><span data-stu-id="941cc-105">Doing so would break every project depending on the availability of the package, especially with build workflows that involve package restore.</span></span>

<span data-ttu-id="941cc-106">nuget.org nemá podporuje *unlisting* balíček, což lze provést na stránce Správa balíčku na webu.</span><span class="sxs-lookup"><span data-stu-id="941cc-106">nuget.org does supports *unlisting* a package, which can be done in the package management page on the web site.</span></span> <span data-ttu-id="941cc-107">Neuvedené balíčky nezobrazí v nuget.org nebo ve Visual Studiu a se nezobrazí ve výsledcích hledání.</span><span class="sxs-lookup"><span data-stu-id="941cc-107">Unlisted packages don't appear on nuget.org or in the Visual Studio UI, and do not appear in search results.</span></span> <span data-ttu-id="941cc-108">Neuvedené balíčků, ale je stále možné stáhnout a nainstalovat pomocí čísla přesnou verzi, která podporuje obnovení balíčků.</span><span class="sxs-lookup"><span data-stu-id="941cc-108">Unlisted packages, however, can still be downloaded and installed by using an exact version number, which supports package restore.</span></span> <span data-ttu-id="941cc-109">Kromě toho může neuvedené balíčky zjištěná stále v následujícím konkrétním scénářům:</span><span class="sxs-lookup"><span data-stu-id="941cc-109">In addition, unlisted packages may still be discovered in the following specific scenarios:</span></span>

- <span data-ttu-id="941cc-110">Obnovení pomocí plovoucí verzí balíčků (například `1.0.0-*`), pokud nejnovější dostupné balíček odpovídající omezení verze nebo závislost je balíček není uveden v seznamu.</span><span class="sxs-lookup"><span data-stu-id="941cc-110">Package restore using floating versions (for example, `1.0.0-*`), if the latest available package matching the version or dependency constraints is an unlisted package.</span></span>
- <span data-ttu-id="941cc-111">Replikace balíčků pomocí katalogu (jak katalogu také obsahuje neuvedené balíčků).</span><span class="sxs-lookup"><span data-stu-id="941cc-111">Replication of packages through the catalog (as the catalog also contains unlisted packages).</span></span>

## <a name="exceptions"></a><span data-ttu-id="941cc-112">Výjimky</span><span class="sxs-lookup"><span data-stu-id="941cc-112">Exceptions</span></span>

<span data-ttu-id="941cc-113">Ve výjimečných případech například věci porušení autorských práv a potenciálně nebezpečný obsah balíčků můžete odstranit ručně týmem NuGet.</span><span class="sxs-lookup"><span data-stu-id="941cc-113">In exceptional situations such as copyright infringement and potentially harmful content, packages can be deleted manually by the NuGet team.</span></span> <span data-ttu-id="941cc-114">Odeslání žádosti o podporu prostřednictvím [Galerie NuGet](http://www.nuget.org) ke spuštění procesu.</span><span class="sxs-lookup"><span data-stu-id="941cc-114">Submit a support request through [NuGet Gallery](http://www.nuget.org) to start the process.</span></span>

## <a name="prohibited-use"></a><span data-ttu-id="941cc-115">Zakázané používání</span><span class="sxs-lookup"><span data-stu-id="941cc-115">Prohibited use</span></span>

<span data-ttu-id="941cc-116">Balíčky, které splnit některý z následujících kritérií nejsou povoleny ve veřejné galerii NuGet a bude odebrán okamžitě bez diskuzi.</span><span class="sxs-lookup"><span data-stu-id="941cc-116">Packages that meet any of the following criteria are not allowed on the public NuGet gallery and will be immediately removed without discussion.</span></span> <span data-ttu-id="941cc-117">Balíček bude vlastníky, ale, informováni o odebrání.</span><span class="sxs-lookup"><span data-stu-id="941cc-117">Package owners will, however, be notified of the removal.</span></span>

- <span data-ttu-id="941cc-118">Obsahuje malwaru, adwaru nebo jakýkoli druh spyware.</span><span class="sxs-lookup"><span data-stu-id="941cc-118">Contains malware, adware, or any kind of spyware.</span></span>
- <span data-ttu-id="941cc-119">Jsou navrženy pro poškodit pracovní stanice pro vývojáře nebo jejich organizace.</span><span class="sxs-lookup"><span data-stu-id="941cc-119">Are designed to harm a developer's workstation or their organization.</span></span>
- <span data-ttu-id="941cc-120">Porušuje autorská práva nebo porušuje licence.</span><span class="sxs-lookup"><span data-stu-id="941cc-120">Infringes copyrights or violates licenses.</span></span>
- <span data-ttu-id="941cc-121">Obsahuje neplatný obsah.</span><span class="sxs-lookup"><span data-stu-id="941cc-121">Contains illegal content.</span></span>
- <span data-ttu-id="941cc-122">Jsou používány k přikrčené na identifikátory balíček, včetně balíčků, které obsahují nulové produktivní obsah.</span><span class="sxs-lookup"><span data-stu-id="941cc-122">Are being used to squat on package identifiers, including packages that have zero productive content.</span></span> <span data-ttu-id="941cc-123">Balíčky musí obsahovat kód nebo vlastníci musí protihráči postoupit identifikátor někomu, kdo má ve skutečnosti produktu pro odeslání.</span><span class="sxs-lookup"><span data-stu-id="941cc-123">Packages must contain code or the owners must concede the identifier to someone who actually has a product to ship.</span></span>
- <span data-ttu-id="941cc-124">Pokusí se provést akci, která je určený není explicitně udělat galerie.</span><span class="sxs-lookup"><span data-stu-id="941cc-124">Attempt to make the gallery do something that it's not explicitly designed to do.</span></span>

<span data-ttu-id="941cc-125">Pokud zjistíte, balíček, který je v rozporu s některou z těchto položek, klikněte na tlačítko **oznámení zneužití** odkaz na stránku podrobností balíčku a odeslání zprávy.</span><span class="sxs-lookup"><span data-stu-id="941cc-125">If you find a package that is in violation of any of these items, click the **Report Abuse** link on the package details page and submit a report.</span></span>

<span data-ttu-id="941cc-126">Všimněte si, že tým NuGet a .NET Foundation si vyhrazuje právo kdykoli změnit tato kritéria.</span><span class="sxs-lookup"><span data-stu-id="941cc-126">Note that the NuGet team and the .NET Foundation reserves the right to change these criteria at any time.</span></span>
