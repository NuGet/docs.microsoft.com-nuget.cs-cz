---
title: Poznámky k verzi NuGet 2.8.1
description: Poznámky k verzi pro NuGet 2.8.1 včetně – známé problémy, opravy chyb, přidaných funkcí a chcete.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 8787aee36d31ed5d8071b35a8c243823029d135f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820518"
---
# <a name="nuget-281-release-notes"></a><span data-ttu-id="76caa-103">Poznámky k verzi NuGet 2.8.1</span><span class="sxs-lookup"><span data-stu-id="76caa-103">NuGet 2.8.1 Release Notes</span></span>

<span data-ttu-id="76caa-104">[Poznámky k verzi NuGet 2.8](../release-notes/nuget-2.8.md) | [NuGet ve verzi 2.8.2 poznámky k verzi](../release-notes/nuget-2.8.2.md)</span><span class="sxs-lookup"><span data-stu-id="76caa-104">[NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 Release Notes](../release-notes/nuget-2.8.2.md)</span></span>

<span data-ttu-id="76caa-105">NuGet 2.8.1 byla vydána 2. dubna 2014.</span><span class="sxs-lookup"><span data-stu-id="76caa-105">NuGet 2.8.1 was released on April 2, 2014.</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="76caa-106">Upozorňují na důležité funkce ve verzi</span><span class="sxs-lookup"><span data-stu-id="76caa-106">Notable features in the release</span></span>

### <a name="support-for-windows-phone-81-projects"></a><span data-ttu-id="76caa-107">Podpora pro projekty Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="76caa-107">Support for Windows Phone 8.1 Projects</span></span>
<span data-ttu-id="76caa-108">Tato verze podporuje nyní následující nové monikery framework cíl které se dají použít na cíl Windows Phone 8.1 projekty:</span><span class="sxs-lookup"><span data-stu-id="76caa-108">This release now supports the following new target framework monikers which can be used to target Windows Phone 8.1 projects:</span></span>

* <span data-ttu-id="76caa-109">WindowsPhone81 / WP81 (pro projekty založeného na technologii Silverlight pro Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="76caa-109">WindowsPhone81 / WP81 (for Silverlight-based Windows Phone projects)</span></span>
* <span data-ttu-id="76caa-110">WindowsPhoneApp81 / WPA81 (pro projekty založené na WinRT aplikací Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="76caa-110">WindowsPhoneApp81 / WPA81 (for WinRT-based Windows Phone App projects)</span></span>

### <a name="update-of-the-nuget-webmatrix-extension"></a><span data-ttu-id="76caa-111">Aktualizuje se rozšíření prostředí WebMatrix NuGet</span><span class="sxs-lookup"><span data-stu-id="76caa-111">Update of the NuGet WebMatrix Extension</span></span>
<span data-ttu-id="76caa-112">Tato verze aktualizuje klienta NuGet nalezen ve službě WebMatrix k [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 a přináší s funkce jako je například XDT transformace.</span><span class="sxs-lookup"><span data-stu-id="76caa-112">This release updates the NuGet client found in WebMatrix to [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 and brings with it features such as XDT transformations.</span></span> <span data-ttu-id="76caa-113">Je důležité, 2.6.1 základní aktualizace umožňuje, aby klient služby WebMatrix instalace balíčků NuGet, které obsahují novějších verzích `.nuspec` schématu, která zahrnuje balíčků ASP.NET NuGet.</span><span class="sxs-lookup"><span data-stu-id="76caa-113">More importantly, the 2.6.1 core update enables the WebMatrix client to install NuGet packages which contain more recent versions of the `.nuspec` schema, which includes the ASP.NET NuGet packages.</span></span>

<span data-ttu-id="76caa-114">Další informace o aktualizaci rozšíření prostředí WebMatrix, zjistěte, jaké konkrétní [poznámky k verzi](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span><span class="sxs-lookup"><span data-stu-id="76caa-114">For more information about the WebMatrix Extension update, see those specific [release notes](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="76caa-115">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="76caa-115">Bug Fixes</span></span>
<span data-ttu-id="76caa-116">Kromě těchto funkcích tato verze NuGet obsahuje ostatní opravy chyb.</span><span class="sxs-lookup"><span data-stu-id="76caa-116">In addition to these features, this release of NuGet includes other bug fixes.</span></span> <span data-ttu-id="76caa-117">Nebyly 16 celkový problémy řešeny v verze.</span><span class="sxs-lookup"><span data-stu-id="76caa-117">There were 16 total issues addressed in the release.</span></span> <span data-ttu-id="76caa-118">Úplný seznam pracovní položky pevná ve NuGet 2.8.1, prosím zobrazení [sledovací modul problém NuGet pro tuto verzi](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="76caa-118">For a full list of the work items fixed in NuGet 2.8.1, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>

### <a name="reshipping-with-visual-studio-14-ctp"></a><span data-ttu-id="76caa-119">Reshipping pomocí sady Visual Studio "14" CTP</span><span class="sxs-lookup"><span data-stu-id="76caa-119">Reshipping with Visual Studio "14" CTP</span></span>
<span data-ttu-id="76caa-120">V sadě Visual Studio "14" CTP vydala 2014 3. června je dodáván NuGet 2.8.1 v poli.</span><span class="sxs-lookup"><span data-stu-id="76caa-120">In Visual Studio "14" CTP released on June 3rd 2014, NuGet 2.8.1 is shipped in the box.</span></span> <span data-ttu-id="76caa-121">Funkce se podporují zůstávají v nominální s další 2.8.1 VSIXes, jako je třeba pro Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="76caa-121">The features it support remain in-par with other 2.8.1 VSIXes such as the one for Visual Studio 2013.</span></span>
