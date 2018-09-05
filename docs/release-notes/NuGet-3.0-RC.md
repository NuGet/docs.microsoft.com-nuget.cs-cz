---
title: Zpráva k vydání verze NuGet 3.0 RC
description: Zpráva k vydání verze pro NuGet 3.0 RC, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0575cb1598f259a1cf1597f67123b644d67c31b5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551716"
---
# <a name="nuget-30-rc-release-notes"></a><span data-ttu-id="2d024-103">Zpráva k vydání verze NuGet 3.0 RC</span><span class="sxs-lookup"><span data-stu-id="2d024-103">NuGet 3.0 RC Release Notes</span></span>

<span data-ttu-id="2d024-104">[Zpráva k vydání verze NuGet 3.0 Beta](../release-notes/nuget-3.0-beta.md) | [zpráva k vydání verze NuGet 3.0 RC2](../release-notes/nuget-3.0-RC2.md)</span><span class="sxs-lookup"><span data-stu-id="2d024-104">[NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md)</span></span>

<span data-ttu-id="2d024-105">NuGet 3.0 RC byla vydána verze Visual Studio 2015 RC 29. dubna 2015.</span><span class="sxs-lookup"><span data-stu-id="2d024-105">NuGet 3.0 RC was released on April 29, 2015 with the Visual Studio 2015 RC release.</span></span> <span data-ttu-id="2d024-106">Tato verze obsahuje řadu oprav chyb, vylepšení výkonu a aktualizace pro podporu nového rozhraní.</span><span class="sxs-lookup"><span data-stu-id="2d024-106">This release has a number of important bug fixes, performance improvements and updates to support the new frameworks.</span></span>  <span data-ttu-id="2d024-107">Je dostupná jenom pro Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="2d024-107">It is only available for Visual Studio 2015.</span></span>

### <a name="continued-focus-on-performance"></a><span data-ttu-id="2d024-108">Trvalé zaměřením na výkon</span><span class="sxs-lookup"><span data-stu-id="2d024-108">Continued Focus on Performance</span></span>

<span data-ttu-id="2d024-109">Stability a výkonu dotazů NuGet dál, který se Zaměřujeme na žhavým tématem.</span><span class="sxs-lookup"><span data-stu-id="2d024-109">Stability and performance of NuGet queries continue to be a hot topic that we are focusing on.</span></span>  <span data-ttu-id="2d024-110">V této vydané verzi měli byste začít zobrazit operace velmi rychlé vyhledávání v uživatelském rozhraní NuGet a Web.</span><span class="sxs-lookup"><span data-stu-id="2d024-110">With this release, you should start to see very quick search operations in the NuGet UI and website.</span></span>  <span data-ttu-id="2d024-111">Sledujeme, služby a jak použít službu tak, aby nám můžete dále ladit tyto operace.</span><span class="sxs-lookup"><span data-stu-id="2d024-111">We're monitoring the service and how you use the service so that we can continue to tune these operations.</span></span>

## <a name="significant-issues-resolved"></a><span data-ttu-id="2d024-112">Vyřešené významné problémy</span><span class="sxs-lookup"><span data-stu-id="2d024-112">Significant Issues Resolved</span></span>

<span data-ttu-id="2d024-113">Stabilizovat klienty NuGet vyřešili jsme řadu problémů jako součást této verze.</span><span class="sxs-lookup"><span data-stu-id="2d024-113">In order to stabilize the NuGet clients, we resolved many issues as part of this release.</span></span>  <span data-ttu-id="2d024-114">Tady je právě krátký seznam některých důležitější vyřešení problémů:</span><span class="sxs-lookup"><span data-stu-id="2d024-114">Here is just a brief list of some of the more important issues resolved:</span></span>

* <span data-ttu-id="2d024-115">Jako součást přejmenovat K framework pro ASP.NET 5, byly aktualizovány monikery framework pro zpracování dnx a dnxcore [odkaz](https://github.com/NuGet/Home/issues/215)</span><span class="sxs-lookup"><span data-stu-id="2d024-115">As part of the rename of the K framework for ASP.NET 5, framework monikers have been updated to handle dnx and dnxcore [link](https://github.com/NuGet/Home/issues/215)</span></span>
* <span data-ttu-id="2d024-116">Přidání dokumentaci nápovědy z odkazů v Uživatelském rozhraní aplikace Visual Studio [odkaz](https://github.com/NuGet/Home/issues/232)</span><span class="sxs-lookup"><span data-stu-id="2d024-116">Added help documentation from links in the Visual Studio UI [link](https://github.com/NuGet/Home/issues/232)</span></span>
* <span data-ttu-id="2d024-117">Lepší zpracování složitých odkazů v `.nuspec` s odkazy na rozhraní oddělených čárkou [odkaz](https://github.com/NuGet/Home/issues/276)</span><span class="sxs-lookup"><span data-stu-id="2d024-117">Better handling of complex references in `.nuspec` with comma-delimited framework references [link](https://github.com/NuGet/Home/issues/276)</span></span>
* <span data-ttu-id="2d024-118">Oprava podporu pro japonské jazykové verze [odkaz](https://github.com/NuGet/Home/issues/253)</span><span class="sxs-lookup"><span data-stu-id="2d024-118">Fixed support for Japanese cultures [link](https://github.com/NuGet/Home/issues/253)</span></span>
* <span data-ttu-id="2d024-119">Aktualizace klienta povolit projekty ASP.NET 5 používaly nové koncové body v3 [odkaz](https://github.com/NuGet/Home/issues/219)</span><span class="sxs-lookup"><span data-stu-id="2d024-119">Updated client to allow ASP.NET 5 projects to use new v3 endpoints [link](https://github.com/NuGet/Home/issues/219)</span></span>
* <span data-ttu-id="2d024-120">Aktualizováno za účelem lepší popisovač složku packages se správou zdrojového kódu [odkaz](https://github.com/NuGet/Home/issues/56)</span><span class="sxs-lookup"><span data-stu-id="2d024-120">Updated to better handle packages folder with source control [link](https://github.com/NuGet/Home/issues/56)</span></span>
* <span data-ttu-id="2d024-121">Oprava podporu pro satelitní balíčky [odkaz](https://github.com/NuGet/Home/issues/17)</span><span class="sxs-lookup"><span data-stu-id="2d024-121">Fixed support for satellite packages [link](https://github.com/NuGet/Home/issues/17)</span></span>
* <span data-ttu-id="2d024-122">Oprava podpory pro soubory obsahu pro konkrétní rozhraní [odkaz](https://github.com/NuGet/Home/issues/18)</span><span class="sxs-lookup"><span data-stu-id="2d024-122">Corrected support for framework-specific content files [link](https://github.com/NuGet/Home/issues/18)</span></span>

## <a name="github-presence-overhaul"></a><span data-ttu-id="2d024-123">Generální Githubu přítomnost opravu</span><span class="sxs-lookup"><span data-stu-id="2d024-123">GitHub presence overhaul</span></span>

<span data-ttu-id="2d024-124">Provedli jsme některé změny naše [úložiště zdrojového kódu na Githubu](http://github.com/nuget/home).</span><span class="sxs-lookup"><span data-stu-id="2d024-124">We've made some changes to our [source code repositories on GitHub](http://github.com/nuget/home).</span></span>  <span data-ttu-id="2d024-125">Pokud máte nějaké problémy s klienta NuGet sady Visual Studio, příkazy prostředí Powershell nebo příkazového řádku spustitelný soubor můžete protokolovat těchto problémů a sledovat jejich průběh na naše [seznamu problémů na úložiště Domovská stránka úložiště GitHub](http://github.com/nuget/home/issues).</span><span class="sxs-lookup"><span data-stu-id="2d024-125">If you have any issues with the NuGet Visual Studio client, the Powershell commands, or the command-line executable you can log those issues and monitor their progress on our [GitHub Home repository issues list](http://github.com/nuget/home/issues).</span></span>  <span data-ttu-id="2d024-126">Sledujeme problémy v galerii v našich [úložiště GitHub NuGetGallery](http://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="2d024-126">We are tracking issues for the gallery in our [GitHub NuGetGallery repository](http://github.com/nuget/NuGetGallery/issues).</span></span>


## <a name="stay-tuned"></a><span data-ttu-id="2d024-127">Nenechte si ujít</span><span class="sxs-lookup"><span data-stu-id="2d024-127">Stay Tuned</span></span>

<span data-ttu-id="2d024-128">Prosím dohlížet na [náš blog o](http://blog.nuget.org) další průběh a oznámení pro NuGet 3.0!</span><span class="sxs-lookup"><span data-stu-id="2d024-128">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>