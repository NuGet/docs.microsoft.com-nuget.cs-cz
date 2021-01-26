---
title: Poznámky k verzi NuGet 2.8.1
description: Poznámky k verzi pro NuGet 2.8.1, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4dcd8ab140026c39345f850ac00a7a5f26a0e62c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776772"
---
# <a name="nuget-281-release-notes"></a><span data-ttu-id="20d48-103">Poznámky k verzi NuGet 2.8.1</span><span class="sxs-lookup"><span data-stu-id="20d48-103">NuGet 2.8.1 Release Notes</span></span>

<span data-ttu-id="20d48-104">Zpráva k [vydání verze](../release-notes/nuget-2.8.md)  |  NuGet 2,8 [Poznámky k verzi NuGet ve verzi 2.8.2](../release-notes/nuget-2.8.2.md)</span><span class="sxs-lookup"><span data-stu-id="20d48-104">[NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 Release Notes](../release-notes/nuget-2.8.2.md)</span></span>

<span data-ttu-id="20d48-105">2.8.1 NuGet byl vydaný 2. dubna 2014.</span><span class="sxs-lookup"><span data-stu-id="20d48-105">NuGet 2.8.1 was released on April 2, 2014.</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="20d48-106">Významné funkce v této verzi</span><span class="sxs-lookup"><span data-stu-id="20d48-106">Notable features in the release</span></span>

### <a name="support-for-windows-phone-81-projects"></a><span data-ttu-id="20d48-107">Podpora pro projekty Windows Phone 8,1</span><span class="sxs-lookup"><span data-stu-id="20d48-107">Support for Windows Phone 8.1 Projects</span></span>
<span data-ttu-id="20d48-108">Tato verze teď podporuje následující nové monikery cílového rozhraní, které se dají použít k cílení na projekty Windows Phone 8,1:</span><span class="sxs-lookup"><span data-stu-id="20d48-108">This release now supports the following new target framework monikers which can be used to target Windows Phone 8.1 projects:</span></span>

* <span data-ttu-id="20d48-109">WindowsPhone81/WP81 (pro projekty Windows Phone založené na technologii Silverlight)</span><span class="sxs-lookup"><span data-stu-id="20d48-109">WindowsPhone81 / WP81 (for Silverlight-based Windows Phone projects)</span></span>
* <span data-ttu-id="20d48-110">WindowsPhoneApp81/WPA81 (pro projekty aplikací Windows Phone založené na WinRT)</span><span class="sxs-lookup"><span data-stu-id="20d48-110">WindowsPhoneApp81 / WPA81 (for WinRT-based Windows Phone App projects)</span></span>

### <a name="update-of-the-nuget-webmatrix-extension"></a><span data-ttu-id="20d48-111">Aktualizace rozšíření WebMatrix NuGet</span><span class="sxs-lookup"><span data-stu-id="20d48-111">Update of the NuGet WebMatrix Extension</span></span>
<span data-ttu-id="20d48-112">Tato verze aktualizuje klienta NuGet, který se našel v WebMatrixu, do [NuGet. Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 a přináší funkce IT, jako jsou třeba transformace xdt.</span><span class="sxs-lookup"><span data-stu-id="20d48-112">This release updates the NuGet client found in WebMatrix to [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 and brings with it features such as XDT transformations.</span></span> <span data-ttu-id="20d48-113">Důležitější je, že aktualizace 2.6.1 Core umožňuje klientovi WebMatrix instalovat balíčky NuGet, které obsahují novější verze `.nuspec` schématu, včetně balíčků nuget ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="20d48-113">More importantly, the 2.6.1 core update enables the WebMatrix client to install NuGet packages which contain more recent versions of the `.nuspec` schema, which includes the ASP.NET NuGet packages.</span></span>

<span data-ttu-id="20d48-114">Další informace o aktualizaci rozšíření WebMatrix najdete v těchto [poznámkách k verzi](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span><span class="sxs-lookup"><span data-stu-id="20d48-114">For more information about the WebMatrix Extension update, see those specific [release notes](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="20d48-115">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="20d48-115">Bug Fixes</span></span>
<span data-ttu-id="20d48-116">Kromě těchto funkcí obsahuje tato verze NuGet i další opravy chyb.</span><span class="sxs-lookup"><span data-stu-id="20d48-116">In addition to these features, this release of NuGet includes other bug fixes.</span></span> <span data-ttu-id="20d48-117">V této verzi bylo vyřešeno 16 celkových problémů.</span><span class="sxs-lookup"><span data-stu-id="20d48-117">There were 16 total issues addressed in the release.</span></span> <span data-ttu-id="20d48-118">Úplný seznam pracovních položek opravených ve 2.8.1 NuGet najdete v [přehledu problémů NuGet pro tuto verzi](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="20d48-118">For a full list of the work items fixed in NuGet 2.8.1, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>

### <a name="reshipping-with-visual-studio-14-ctp"></a><span data-ttu-id="20d48-119">Redodávka pomocí sady Visual Studio "14" CTP</span><span class="sxs-lookup"><span data-stu-id="20d48-119">Reshipping with Visual Studio "14" CTP</span></span>
<span data-ttu-id="20d48-120">V aplikaci Visual Studio "14" CTP vydané 3. června 2014 se do boxu dodává 2.8.1 NuGet.</span><span class="sxs-lookup"><span data-stu-id="20d48-120">In Visual Studio "14" CTP released on June 3rd 2014, NuGet 2.8.1 is shipped in the box.</span></span> <span data-ttu-id="20d48-121">Funkce, které podporují, zůstávají stejné jako jiné 2.8.1 VSIX, jako je ta pro Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="20d48-121">The features it support remain in-par with other 2.8.1 VSIXes such as the one for Visual Studio 2013.</span></span>
