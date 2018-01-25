---
title: "Poznámky k verzi RC NuGet 3.0 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Poznámky k verzi pro RC 3.0 NuGet včetně známé problémy, opravy chyb, přidaných funkcí a chcete."
keywords: "NuGet 3.0 k vydání verze RC, opravy chyb známé problémy, přidat funkce, chcete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4693fd8884283e01d3c0a8ad74e0692c1ca00659
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-30-rc-release-notes"></a><span data-ttu-id="24f2c-104">Poznámky k verzi RC NuGet 3.0</span><span class="sxs-lookup"><span data-stu-id="24f2c-104">NuGet 3.0 RC Release Notes</span></span>

<span data-ttu-id="24f2c-105">[Poznámky k verzi Beta NuGet 3.0](../release-notes/nuget-3.0-beta.md) | [poznámky k verzi RC2 NuGet 3.0](../release-notes/nuget-3.0-RC2.md)</span><span class="sxs-lookup"><span data-stu-id="24f2c-105">[NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md)</span></span>

<span data-ttu-id="24f2c-106">NuGet 3.0 RC byla vydána 29. dubna 2015 ve verzi Visual Studio 2015 RC.</span><span class="sxs-lookup"><span data-stu-id="24f2c-106">NuGet 3.0 RC was released on April 29, 2015 with the Visual Studio 2015 RC release.</span></span> <span data-ttu-id="24f2c-107">Tato verze obsahuje několik důležitých oprav chyb, vylepšení výkonu a aktualizace pro podporu nového rozhraní.</span><span class="sxs-lookup"><span data-stu-id="24f2c-107">This release has a number of important bug fixes, performance improvements and updates to support the new frameworks.</span></span>  <span data-ttu-id="24f2c-108">Je k dispozici pouze pro Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="24f2c-108">It is only available for Visual Studio 2015.</span></span>

### <a name="continued-focus-on-performance"></a><span data-ttu-id="24f2c-109">Trvalá zaměřit se na výkon</span><span class="sxs-lookup"><span data-stu-id="24f2c-109">Continued Focus on Performance</span></span>

<span data-ttu-id="24f2c-110">Stability a výkonu dotazů NuGet nadále aktivní téma, které jsme se zaměřením na.</span><span class="sxs-lookup"><span data-stu-id="24f2c-110">Stability and performance of NuGet queries continue to be a hot topic that we are focusing on.</span></span>  <span data-ttu-id="24f2c-111">V této verzi měli byste začít zobrazíte operace velmi rychlé hledání v NuGet uživatelského rozhraní a webu.</span><span class="sxs-lookup"><span data-stu-id="24f2c-111">With this release, you should start to see very quick search operations in the NuGet UI and website.</span></span>  <span data-ttu-id="24f2c-112">Probíhá sledování služby a jak používat službu, aby jsme můžete nadále vyladění těchto operací.</span><span class="sxs-lookup"><span data-stu-id="24f2c-112">We're monitoring the service and how you use the service so that we can continue to tune these operations.</span></span>

## <a name="significant-issues-resolved"></a><span data-ttu-id="24f2c-113">Významné vyřešení problémů</span><span class="sxs-lookup"><span data-stu-id="24f2c-113">Significant Issues Resolved</span></span>

<span data-ttu-id="24f2c-114">Stabilizovat klienty NuGet jsme vyřešit řadu problémů v rámci této verze.</span><span class="sxs-lookup"><span data-stu-id="24f2c-114">In order to stabilize the NuGet clients, we resolved many issues as part of this release.</span></span>  <span data-ttu-id="24f2c-115">Tady je právě stručný seznam některých důležitější vyřešení problémů:</span><span class="sxs-lookup"><span data-stu-id="24f2c-115">Here is just a brief list of some of the more important issues resolved:</span></span>

* <span data-ttu-id="24f2c-116">Jako součást přejmenování tisíc framework pro ASP.NET 5, byly aktualizovány monikery framework pro zpracování dnx a dnxcore [odkaz](https://github.com/NuGet/Home/issues/215)</span><span class="sxs-lookup"><span data-stu-id="24f2c-116">As part of the rename of the K framework for ASP.NET 5, framework monikers have been updated to handle dnx and dnxcore [link](https://github.com/NuGet/Home/issues/215)</span></span>
* <span data-ttu-id="24f2c-117">Nápovědě přidají odkazy ve Visual Studiu [odkaz](https://github.com/NuGet/Home/issues/232)</span><span class="sxs-lookup"><span data-stu-id="24f2c-117">Added help documentation from links in the Visual Studio UI [link](https://github.com/NuGet/Home/issues/232)</span></span>
* <span data-ttu-id="24f2c-118">Lepší zpracování složitých odkazů v `.nuspec` s oddělovači framework odkazy [odkaz](https://github.com/NuGet/Home/issues/276)</span><span class="sxs-lookup"><span data-stu-id="24f2c-118">Better handling of complex references in `.nuspec` with comma-delimited framework references [link](https://github.com/NuGet/Home/issues/276)</span></span>
* <span data-ttu-id="24f2c-119">Pevné podporu pro jazykové japonské verze [odkaz](https://github.com/NuGet/Home/issues/253)</span><span class="sxs-lookup"><span data-stu-id="24f2c-119">Fixed support for Japanese cultures [link](https://github.com/NuGet/Home/issues/253)</span></span>
* <span data-ttu-id="24f2c-120">Aktualizovaného klienta povolit projekty ASP.NET 5, aby používaly nové koncové body v3 [odkaz](https://github.com/NuGet/Home/issues/219)</span><span class="sxs-lookup"><span data-stu-id="24f2c-120">Updated client to allow ASP.NET 5 projects to use new v3 endpoints [link](https://github.com/NuGet/Home/issues/219)</span></span>
* <span data-ttu-id="24f2c-121">Aktualizováno za účelem lepší popisovač balíčky složka se správa zdrojového kódu [odkaz](https://github.com/NuGet/Home/issues/56)</span><span class="sxs-lookup"><span data-stu-id="24f2c-121">Updated to better handle packages folder with source control [link](https://github.com/NuGet/Home/issues/56)</span></span>
* <span data-ttu-id="24f2c-122">Pevné podporu pro balíčky satelitní [odkaz](https://github.com/NuGet/Home/issues/17)</span><span class="sxs-lookup"><span data-stu-id="24f2c-122">Fixed support for satellite packages [link](https://github.com/NuGet/Home/issues/17)</span></span>
* <span data-ttu-id="24f2c-123">Opravě podporu pro soubory obsahu pro konkrétní rozhraní [odkaz](https://github.com/NuGet/Home/issues/18)</span><span class="sxs-lookup"><span data-stu-id="24f2c-123">Corrected support for framework-specific content files [link](https://github.com/NuGet/Home/issues/18)</span></span>

## <a name="github-presence-overhaul"></a><span data-ttu-id="24f2c-124">Generální opravu přítomnosti Githubu</span><span class="sxs-lookup"><span data-stu-id="24f2c-124">GitHub presence overhaul</span></span>

<span data-ttu-id="24f2c-125">Provedli jsme některé změny naše [zdrojového kódu úložiště na Githubu](http://github.com/nuget/home).</span><span class="sxs-lookup"><span data-stu-id="24f2c-125">We've made some changes to our [source code repositories on GitHub](http://github.com/nuget/home).</span></span>  <span data-ttu-id="24f2c-126">Pokud máte problémy s klienta NuGet sady Visual Studio, příkazy prostředí Powershell nebo příkazového řádku spustitelného souboru můžete protokolu tyto problémy a jejich průběh sledovat na našem [seznam problémů úložiště GitHub domovské](http://github.com/nuget/home/issues).</span><span class="sxs-lookup"><span data-stu-id="24f2c-126">If you have any issues with the NuGet Visual Studio client, the Powershell commands, or the command-line executable you can log those issues and monitor their progress on our [GitHub Home repository issues list](http://github.com/nuget/home/issues).</span></span>  <span data-ttu-id="24f2c-127">Sledujeme problémy pro galerii v našem [úložiště GitHub NuGetGallery](http://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="24f2c-127">We are tracking issues for the gallery in our [GitHub NuGetGallery repository](http://github.com/nuget/NuGetGallery/issues).</span></span>


## <a name="stay-tuned"></a><span data-ttu-id="24f2c-128">Nenechte ujít</span><span class="sxs-lookup"><span data-stu-id="24f2c-128">Stay Tuned</span></span>

<span data-ttu-id="24f2c-129">Prosím dohlížet na [náš blog](http://blog.nuget.org) další průběh a hlášení pro NuGet 3.0!</span><span class="sxs-lookup"><span data-stu-id="24f2c-129">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>