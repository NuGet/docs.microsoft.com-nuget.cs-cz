---
title: Poznámky k verzi NuGet 3,0 RC
description: Poznámky k verzi pro NuGet 3,0 RC, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 19bc51a278425295811db253ca3f4ba4366ccf49
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776572"
---
# <a name="nuget-30-rc-release-notes"></a><span data-ttu-id="4a487-103">Poznámky k verzi NuGet 3,0 RC</span><span class="sxs-lookup"><span data-stu-id="4a487-103">NuGet 3.0 RC Release Notes</span></span>

<span data-ttu-id="4a487-104">Poznámky k verzi [NuGet 3,0 beta](../release-notes/nuget-3.0-beta.md)  |  [Poznámky k verzi NuGet 3,0 RC2](../release-notes/nuget-3.0-RC2.md)</span><span class="sxs-lookup"><span data-stu-id="4a487-104">[NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md)</span></span>

<span data-ttu-id="4a487-105">NuGet 3,0 RC byl vydán 29. dubna 2015 s vydáním sady Visual Studio 2015 RC.</span><span class="sxs-lookup"><span data-stu-id="4a487-105">NuGet 3.0 RC was released on April 29, 2015 with the Visual Studio 2015 RC release.</span></span> <span data-ttu-id="4a487-106">Tato verze přináší řadu důležitých oprav chyb, vylepšení výkonu a aktualizace pro podporu nových rozhraní.</span><span class="sxs-lookup"><span data-stu-id="4a487-106">This release has a number of important bug fixes, performance improvements and updates to support the new frameworks.</span></span>  <span data-ttu-id="4a487-107">Je k dispozici pouze pro Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="4a487-107">It is only available for Visual Studio 2015.</span></span>

### <a name="continued-focus-on-performance"></a><span data-ttu-id="4a487-108">Pokračující zaměření na výkon</span><span class="sxs-lookup"><span data-stu-id="4a487-108">Continued Focus on Performance</span></span>

<span data-ttu-id="4a487-109">Stabilita a výkon dotazů NuGet dál představují aktivní téma, které se zaměřujeme na.</span><span class="sxs-lookup"><span data-stu-id="4a487-109">Stability and performance of NuGet queries continue to be a hot topic that we are focusing on.</span></span>  <span data-ttu-id="4a487-110">V této verzi byste měli začít zobrazovat velmi rychlé operace vyhledávání v uživatelském rozhraní a na webu NuGet.</span><span class="sxs-lookup"><span data-stu-id="4a487-110">With this release, you should start to see very quick search operations in the NuGet UI and website.</span></span>  <span data-ttu-id="4a487-111">Sledujeme službu a jak službu používáte, abychom mohli i nadále ladit tyto operace.</span><span class="sxs-lookup"><span data-stu-id="4a487-111">We're monitoring the service and how you use the service so that we can continue to tune these operations.</span></span>

## <a name="significant-issues-resolved"></a><span data-ttu-id="4a487-112">Vyřešené významné problémy</span><span class="sxs-lookup"><span data-stu-id="4a487-112">Significant Issues Resolved</span></span>

<span data-ttu-id="4a487-113">Za účelem stabilizace klientů NuGet jsme v rámci této verze vyřešili spoustu problémů.</span><span class="sxs-lookup"><span data-stu-id="4a487-113">In order to stabilize the NuGet clients, we resolved many issues as part of this release.</span></span>  <span data-ttu-id="4a487-114">Tady je jenom stručný seznam některých z důležitějších problémů, které jsme vyřešili:</span><span class="sxs-lookup"><span data-stu-id="4a487-114">Here is just a brief list of some of the more important issues resolved:</span></span>

* <span data-ttu-id="4a487-115">V rámci přejmenování rozhraní K Framework pro ASP.NET 5 byly monikery rozhraní aktualizované pro zpracování [propojení](https://github.com/NuGet/Home/issues/215) DNX a dnxcore.</span><span class="sxs-lookup"><span data-stu-id="4a487-115">As part of the rename of the K framework for ASP.NET 5, framework monikers have been updated to handle dnx and dnxcore [link](https://github.com/NuGet/Home/issues/215)</span></span>
* <span data-ttu-id="4a487-116">Přidání dokumentace k nápovědě z odkazů v rámci [odkazu](https://github.com/NuGet/Home/issues/232) na uživatelské rozhraní sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4a487-116">Added help documentation from links in the Visual Studio UI [link](https://github.com/NuGet/Home/issues/232)</span></span>
* <span data-ttu-id="4a487-117">Lepší zacházení se složitými odkazy v `.nuspec` rámci [odkazu](https://github.com/NuGet/Home/issues/276) na odkazy rozhraní s oddělovači</span><span class="sxs-lookup"><span data-stu-id="4a487-117">Better handling of complex references in `.nuspec` with comma-delimited framework references [link](https://github.com/NuGet/Home/issues/276)</span></span>
* <span data-ttu-id="4a487-118">Pevná podpora pro japonské [odkazy](https://github.com/NuGet/Home/issues/253) na japonštinu</span><span class="sxs-lookup"><span data-stu-id="4a487-118">Fixed support for Japanese cultures [link](https://github.com/NuGet/Home/issues/253)</span></span>
* <span data-ttu-id="4a487-119">Aktualizovaný klient, aby povoloval ASP.NET 5 projektů používat nové [odkazy](https://github.com/NuGet/Home/issues/219) na koncové body V3</span><span class="sxs-lookup"><span data-stu-id="4a487-119">Updated client to allow ASP.NET 5 projects to use new v3 endpoints [link](https://github.com/NuGet/Home/issues/219)</span></span>
* <span data-ttu-id="4a487-120">Aktualizováno pro lepší zpracování složky balíčků pomocí [odkazu](https://github.com/NuGet/Home/issues/56) správy zdrojového kódu</span><span class="sxs-lookup"><span data-stu-id="4a487-120">Updated to better handle packages folder with source control [link](https://github.com/NuGet/Home/issues/56)</span></span>
* <span data-ttu-id="4a487-121">[Odkaz](https://github.com/NuGet/Home/issues/17) na fixní podporu pro satelitní balíčky</span><span class="sxs-lookup"><span data-stu-id="4a487-121">Fixed support for satellite packages [link](https://github.com/NuGet/Home/issues/17)</span></span>
* <span data-ttu-id="4a487-122">Opravená podpora pro [odkaz](https://github.com/NuGet/Home/issues/18) soubory obsahu pro konkrétní rozhraní</span><span class="sxs-lookup"><span data-stu-id="4a487-122">Corrected support for framework-specific content files [link](https://github.com/NuGet/Home/issues/18)</span></span>

## <a name="github-presence-overhaul"></a><span data-ttu-id="4a487-123">Renovace stavu GitHubu</span><span class="sxs-lookup"><span data-stu-id="4a487-123">GitHub presence overhaul</span></span>

<span data-ttu-id="4a487-124">Provedli jsme některé změny našich [úložišť zdrojového kódu na GitHubu](http://github.com/nuget/home).</span><span class="sxs-lookup"><span data-stu-id="4a487-124">We've made some changes to our [source code repositories on GitHub](http://github.com/nuget/home).</span></span>  <span data-ttu-id="4a487-125">Pokud máte nějaké problémy s klientem nástroje NuGet pro aplikaci Visual Studio, příkazy prostředí PowerShell nebo spustitelný soubor příkazového řádku, můžete tyto problémy zaprotokolovat a sledovat jejich průběh v našem [seznamu problémů domovského úložiště GitHub](http://github.com/nuget/home/issues).</span><span class="sxs-lookup"><span data-stu-id="4a487-125">If you have any issues with the NuGet Visual Studio client, the Powershell commands, or the command-line executable you can log those issues and monitor their progress on our [GitHub Home repository issues list](http://github.com/nuget/home/issues).</span></span>  <span data-ttu-id="4a487-126">Sledujeme problémy pro galerii v našem [úložišti GitHub NuGetGallery](http://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="4a487-126">We are tracking issues for the gallery in our [GitHub NuGetGallery repository](http://github.com/nuget/NuGetGallery/issues).</span></span>


## <a name="stay-tuned"></a><span data-ttu-id="4a487-127">Zůstat vyladěné</span><span class="sxs-lookup"><span data-stu-id="4a487-127">Stay Tuned</span></span>

<span data-ttu-id="4a487-128">Na [našem blogu](http://blog.nuget.org) prosím sledujte, kde najdete další informace o průběhu a oznámeních pro NuGet 3,0!</span><span class="sxs-lookup"><span data-stu-id="4a487-128">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>