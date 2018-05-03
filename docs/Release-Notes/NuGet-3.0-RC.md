---
title: Poznámky k verzi RC NuGet 3.0
description: Poznámky k verzi pro RC 3.0 NuGet včetně známé problémy, opravy chyb, přidaných funkcí a chcete.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 28ac49d9e9071d16d20b24808abb0acaab214ffd
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-30-rc-release-notes"></a><span data-ttu-id="e0512-103">Poznámky k verzi RC NuGet 3.0</span><span class="sxs-lookup"><span data-stu-id="e0512-103">NuGet 3.0 RC Release Notes</span></span>

<span data-ttu-id="e0512-104">[Poznámky k verzi Beta NuGet 3.0](../release-notes/nuget-3.0-beta.md) | [poznámky k verzi RC2 NuGet 3.0](../release-notes/nuget-3.0-RC2.md)</span><span class="sxs-lookup"><span data-stu-id="e0512-104">[NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md)</span></span>

<span data-ttu-id="e0512-105">NuGet 3.0 RC byla vydána 29. dubna 2015 ve verzi Visual Studio 2015 RC.</span><span class="sxs-lookup"><span data-stu-id="e0512-105">NuGet 3.0 RC was released on April 29, 2015 with the Visual Studio 2015 RC release.</span></span> <span data-ttu-id="e0512-106">Tato verze obsahuje několik důležitých oprav chyb, vylepšení výkonu a aktualizace pro podporu nového rozhraní.</span><span class="sxs-lookup"><span data-stu-id="e0512-106">This release has a number of important bug fixes, performance improvements and updates to support the new frameworks.</span></span>  <span data-ttu-id="e0512-107">Je k dispozici pouze pro Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="e0512-107">It is only available for Visual Studio 2015.</span></span>

### <a name="continued-focus-on-performance"></a><span data-ttu-id="e0512-108">Trvalá zaměřit se na výkon</span><span class="sxs-lookup"><span data-stu-id="e0512-108">Continued Focus on Performance</span></span>

<span data-ttu-id="e0512-109">Stability a výkonu dotazů NuGet nadále aktivní téma, které jsme se zaměřením na.</span><span class="sxs-lookup"><span data-stu-id="e0512-109">Stability and performance of NuGet queries continue to be a hot topic that we are focusing on.</span></span>  <span data-ttu-id="e0512-110">V této verzi měli byste začít zobrazíte operace velmi rychlé hledání v NuGet uživatelského rozhraní a webu.</span><span class="sxs-lookup"><span data-stu-id="e0512-110">With this release, you should start to see very quick search operations in the NuGet UI and website.</span></span>  <span data-ttu-id="e0512-111">Probíhá sledování služby a jak používat službu, aby jsme můžete nadále vyladění těchto operací.</span><span class="sxs-lookup"><span data-stu-id="e0512-111">We're monitoring the service and how you use the service so that we can continue to tune these operations.</span></span>

## <a name="significant-issues-resolved"></a><span data-ttu-id="e0512-112">Významné vyřešení problémů</span><span class="sxs-lookup"><span data-stu-id="e0512-112">Significant Issues Resolved</span></span>

<span data-ttu-id="e0512-113">Stabilizovat klienty NuGet jsme vyřešit řadu problémů v rámci této verze.</span><span class="sxs-lookup"><span data-stu-id="e0512-113">In order to stabilize the NuGet clients, we resolved many issues as part of this release.</span></span>  <span data-ttu-id="e0512-114">Tady je právě stručný seznam některých důležitější vyřešení problémů:</span><span class="sxs-lookup"><span data-stu-id="e0512-114">Here is just a brief list of some of the more important issues resolved:</span></span>

* <span data-ttu-id="e0512-115">Jako součást přejmenování tisíc framework pro ASP.NET 5, byly aktualizovány monikery framework pro zpracování dnx a dnxcore [odkaz](https://github.com/NuGet/Home/issues/215)</span><span class="sxs-lookup"><span data-stu-id="e0512-115">As part of the rename of the K framework for ASP.NET 5, framework monikers have been updated to handle dnx and dnxcore [link](https://github.com/NuGet/Home/issues/215)</span></span>
* <span data-ttu-id="e0512-116">Nápovědě přidají odkazy ve Visual Studiu [odkaz](https://github.com/NuGet/Home/issues/232)</span><span class="sxs-lookup"><span data-stu-id="e0512-116">Added help documentation from links in the Visual Studio UI [link](https://github.com/NuGet/Home/issues/232)</span></span>
* <span data-ttu-id="e0512-117">Lepší zpracování složitých odkazů v `.nuspec` s oddělovači framework odkazy [odkaz](https://github.com/NuGet/Home/issues/276)</span><span class="sxs-lookup"><span data-stu-id="e0512-117">Better handling of complex references in `.nuspec` with comma-delimited framework references [link](https://github.com/NuGet/Home/issues/276)</span></span>
* <span data-ttu-id="e0512-118">Pevné podporu pro jazykové japonské verze [odkaz](https://github.com/NuGet/Home/issues/253)</span><span class="sxs-lookup"><span data-stu-id="e0512-118">Fixed support for Japanese cultures [link](https://github.com/NuGet/Home/issues/253)</span></span>
* <span data-ttu-id="e0512-119">Aktualizovaného klienta povolit projekty ASP.NET 5, aby používaly nové koncové body v3 [odkaz](https://github.com/NuGet/Home/issues/219)</span><span class="sxs-lookup"><span data-stu-id="e0512-119">Updated client to allow ASP.NET 5 projects to use new v3 endpoints [link](https://github.com/NuGet/Home/issues/219)</span></span>
* <span data-ttu-id="e0512-120">Aktualizováno za účelem lepší popisovač balíčky složka se správa zdrojového kódu [odkaz](https://github.com/NuGet/Home/issues/56)</span><span class="sxs-lookup"><span data-stu-id="e0512-120">Updated to better handle packages folder with source control [link](https://github.com/NuGet/Home/issues/56)</span></span>
* <span data-ttu-id="e0512-121">Pevné podporu pro balíčky satelitní [odkaz](https://github.com/NuGet/Home/issues/17)</span><span class="sxs-lookup"><span data-stu-id="e0512-121">Fixed support for satellite packages [link](https://github.com/NuGet/Home/issues/17)</span></span>
* <span data-ttu-id="e0512-122">Opravě podporu pro soubory obsahu pro konkrétní rozhraní [odkaz](https://github.com/NuGet/Home/issues/18)</span><span class="sxs-lookup"><span data-stu-id="e0512-122">Corrected support for framework-specific content files [link](https://github.com/NuGet/Home/issues/18)</span></span>

## <a name="github-presence-overhaul"></a><span data-ttu-id="e0512-123">Generální opravu přítomnosti Githubu</span><span class="sxs-lookup"><span data-stu-id="e0512-123">GitHub presence overhaul</span></span>

<span data-ttu-id="e0512-124">Provedli jsme některé změny naše [zdrojového kódu úložiště na Githubu](http://github.com/nuget/home).</span><span class="sxs-lookup"><span data-stu-id="e0512-124">We've made some changes to our [source code repositories on GitHub](http://github.com/nuget/home).</span></span>  <span data-ttu-id="e0512-125">Pokud máte problémy s klienta NuGet sady Visual Studio, příkazy prostředí Powershell nebo příkazového řádku spustitelného souboru můžete protokolu tyto problémy a jejich průběh sledovat na našem [seznam problémů úložiště GitHub domovské](http://github.com/nuget/home/issues).</span><span class="sxs-lookup"><span data-stu-id="e0512-125">If you have any issues with the NuGet Visual Studio client, the Powershell commands, or the command-line executable you can log those issues and monitor their progress on our [GitHub Home repository issues list](http://github.com/nuget/home/issues).</span></span>  <span data-ttu-id="e0512-126">Sledujeme problémy pro galerii v našem [úložiště GitHub NuGetGallery](http://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="e0512-126">We are tracking issues for the gallery in our [GitHub NuGetGallery repository](http://github.com/nuget/NuGetGallery/issues).</span></span>


## <a name="stay-tuned"></a><span data-ttu-id="e0512-127">Nenechte ujít</span><span class="sxs-lookup"><span data-stu-id="e0512-127">Stay Tuned</span></span>

<span data-ttu-id="e0512-128">Prosím dohlížet na [náš blog](http://blog.nuget.org) další průběh a hlášení pro NuGet 3.0!</span><span class="sxs-lookup"><span data-stu-id="e0512-128">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>