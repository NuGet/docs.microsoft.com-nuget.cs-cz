---
title: Zpráva k vydání verze NuGet 2.8.1
description: Zpráva k vydání verze pro NuGet 2.8.1 včetně – známé problémy, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 39fb7db00e18e32eef15adc11764a122c97ddfd5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545236"
---
# <a name="nuget-281-release-notes"></a><span data-ttu-id="a7fbc-103">Zpráva k vydání verze NuGet 2.8.1</span><span class="sxs-lookup"><span data-stu-id="a7fbc-103">NuGet 2.8.1 Release Notes</span></span>

<span data-ttu-id="a7fbc-104">[Zpráva k vydání verze NuGet 2.8](../release-notes/nuget-2.8.md) | [zpráva k vydání verze NuGet ve verzi 2.8.2](../release-notes/nuget-2.8.2.md)</span><span class="sxs-lookup"><span data-stu-id="a7fbc-104">[NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 Release Notes](../release-notes/nuget-2.8.2.md)</span></span>

<span data-ttu-id="a7fbc-105">NuGet 2.8.1 byla vydána 2. dubna 2014.</span><span class="sxs-lookup"><span data-stu-id="a7fbc-105">NuGet 2.8.1 was released on April 2, 2014.</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="a7fbc-106">Důležité funkce ve verzi</span><span class="sxs-lookup"><span data-stu-id="a7fbc-106">Notable features in the release</span></span>

### <a name="support-for-windows-phone-81-projects"></a><span data-ttu-id="a7fbc-107">Podpora pro projekty Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="a7fbc-107">Support for Windows Phone 8.1 Projects</span></span>
<span data-ttu-id="a7fbc-108">Tato verze podporuje nyní následující nové cílové rozhraní framework zástupných názvů které je možné použít na cíl Windows Phone 8.1 projekty:</span><span class="sxs-lookup"><span data-stu-id="a7fbc-108">This release now supports the following new target framework monikers which can be used to target Windows Phone 8.1 projects:</span></span>

* <span data-ttu-id="a7fbc-109">WindowsPhone81 / WP81 (pro projekty založené na technologii Silverlight pro Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="a7fbc-109">WindowsPhone81 / WP81 (for Silverlight-based Windows Phone projects)</span></span>
* <span data-ttu-id="a7fbc-110">WindowsPhoneApp81 / WPA81 (pro projekty založené na WinRT aplikací Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="a7fbc-110">WindowsPhoneApp81 / WPA81 (for WinRT-based Windows Phone App projects)</span></span>

### <a name="update-of-the-nuget-webmatrix-extension"></a><span data-ttu-id="a7fbc-111">Aktualizace rozšíření prostředí WebMatrix NuGet</span><span class="sxs-lookup"><span data-stu-id="a7fbc-111">Update of the NuGet WebMatrix Extension</span></span>
<span data-ttu-id="a7fbc-112">Tato verze aktualizuje klienta NuGet v WebMatrix za účelem [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 a přichází s funkcí jako XDT transformace.</span><span class="sxs-lookup"><span data-stu-id="a7fbc-112">This release updates the NuGet client found in WebMatrix to [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 and brings with it features such as XDT transformations.</span></span> <span data-ttu-id="a7fbc-113">Důležitější je, 2.6.1 aktualizací core umožňuje klientovi služby WebMatrix instalace balíčků NuGet, které obsahují novějších verzích `.nuspec` schématu, která zahrnuje balíčky NuGet technologie ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="a7fbc-113">More importantly, the 2.6.1 core update enables the WebMatrix client to install NuGet packages which contain more recent versions of the `.nuspec` schema, which includes the ASP.NET NuGet packages.</span></span>

<span data-ttu-id="a7fbc-114">Další informace o aktualizaci rozšíření nástroje WebMatrix, zjistěte, jaké konkrétní [poznámky k verzi](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span><span class="sxs-lookup"><span data-stu-id="a7fbc-114">For more information about the WebMatrix Extension update, see those specific [release notes](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="a7fbc-115">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="a7fbc-115">Bug Fixes</span></span>
<span data-ttu-id="a7fbc-116">Kromě těchto funkcí tato verze NuGet obsahuje ostatní opravy chyb.</span><span class="sxs-lookup"><span data-stu-id="a7fbc-116">In addition to these features, this release of NuGet includes other bug fixes.</span></span> <span data-ttu-id="a7fbc-117">Došlo k 16 celkový problémy zákazníky a vyřešené ve verzi.</span><span class="sxs-lookup"><span data-stu-id="a7fbc-117">There were 16 total issues addressed in the release.</span></span> <span data-ttu-id="a7fbc-118">Úplný seznam pracovní položky opravených NuGet 2.8.1, prosím zobrazení [NuGet sledování problémů pro tuto verzi](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="a7fbc-118">For a full list of the work items fixed in NuGet 2.8.1, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>

### <a name="reshipping-with-visual-studio-14-ctp"></a><span data-ttu-id="a7fbc-119">Reshipping pomocí sady Visual Studio "14" CTP</span><span class="sxs-lookup"><span data-stu-id="a7fbc-119">Reshipping with Visual Studio "14" CTP</span></span>
<span data-ttu-id="a7fbc-120">Ve Visual Studiu "14" CTP vydala 3. června 2014 je v poli dodané NuGet 2.8.1.</span><span class="sxs-lookup"><span data-stu-id="a7fbc-120">In Visual Studio "14" CTP released on June 3rd 2014, NuGet 2.8.1 is shipped in the box.</span></span> <span data-ttu-id="a7fbc-121">Funkce se podporují zůstávají v pamětích s další 2.8.1 VSIXes, jako je třeba pro Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="a7fbc-121">The features it support remain in-par with other 2.8.1 VSIXes such as the one for Visual Studio 2013.</span></span>
