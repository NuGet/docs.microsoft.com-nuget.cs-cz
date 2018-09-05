---
title: Poznámky k verzi 3.1 NuGet
description: Zpráva k vydání verze pro NuGet 3.1, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 779567d94a5a9a1b3eacddaa4c882201a446cb4b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545344"
---
# <a name="nuget-31-release-notes"></a><span data-ttu-id="5a025-103">Poznámky k verzi 3.1 NuGet</span><span class="sxs-lookup"><span data-stu-id="5a025-103">NuGet 3.1 Release Notes</span></span>

<span data-ttu-id="5a025-104">[Zpráva k vydání verze NuGet 3.0](../release-notes/nuget-3.0.0.md) | [zpráva k vydání verze NuGet 3.1.1](../release-notes/nuget-3.1.1.md)</span><span class="sxs-lookup"><span data-stu-id="5a025-104">[NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 Release Notes](../release-notes/nuget-3.1.1.md)</span></span>

<span data-ttu-id="5a025-105">NuGet 3.1 byla vydána 27. července 2015 jako připojené rozšíření pro Universal Windows Platform SDK pro Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="5a025-105">NuGet 3.1 was released on July 27, 2015 as a bundled extension to the Universal Windows Platform SDK for Visual Studio 2015.</span></span> <span data-ttu-id="5a025-106">Tato verze sady Windows Platform SDK jsme doručili tak, že vývojové prostředí Windows by mohla využít výhod práce NuGet napříč platformami, která byla dříve spuštěna.</span><span class="sxs-lookup"><span data-stu-id="5a025-106">We delivered this release with the Windows Platform SDK so that the Windows development experience could take advantage of the NuGet cross-platform work that had been previously started.</span></span> <span data-ttu-id="5a025-107">Tato verze rozšíření NuGet dostupná jenom pro Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="5a025-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="5a025-108">Doporučujeme, abyste tyto vývojáře, kteří mají přístup ke službě update Galerie sady Visual Studio na nejnovější verzi, která je k dispozici, protože vždy publikujeme aktualizace s opravy chyb a nové funkce.</span><span class="sxs-lookup"><span data-stu-id="5a025-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are always publishing updates with bug fixes and new features.</span></span>

## <a name="nuget-visual-studio-extension"></a><span data-ttu-id="5a025-109">Rozšíření NuGet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5a025-109">NuGet Visual Studio Extension</span></span>

<span data-ttu-id="5a025-110">Problémy a funkce v této verzi jsou označené na Githubu s ["3.1 tranzitivní podpora RTM UWP" milník](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+) celkem, jsme uzavřeno 67 problémech ve verzi 3.1.</span><span class="sxs-lookup"><span data-stu-id="5a025-110">Issues and features in this release are tagged on GitHub with the ["3.1 RTM UWP transitive support" milestone](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  In total, we closed 67 issues in the 3.1 release.</span></span>

### <a name="new-features"></a><span data-ttu-id="5a025-111">Nové funkce</span><span class="sxs-lookup"><span data-stu-id="5a025-111">New Features</span></span>

* <span data-ttu-id="5a025-112">`project.json` Podpora pro podporu Windows UPW a ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="5a025-112">`project.json` support for Windows UWP and ASP.NET 5 support</span></span>
* <span data-ttu-id="5a025-113">Instalace přenositelné balíčku</span><span class="sxs-lookup"><span data-stu-id="5a025-113">Transitive package installation</span></span>

<span data-ttu-id="5a025-114">Popis a definice těchto funkcích najdete jinde v dokumentaci.</span><span class="sxs-lookup"><span data-stu-id="5a025-114">Description and definition of these features can be found elsewhere in the documentation.</span></span>

### <a name="deprecated"></a><span data-ttu-id="5a025-115">zastaralé</span><span class="sxs-lookup"><span data-stu-id="5a025-115">Deprecated</span></span>

<span data-ttu-id="5a025-116">Následující funkce už nejsou k dispozici pro sadu Visual Studio 2015:</span><span class="sxs-lookup"><span data-stu-id="5a025-116">The following features are no longer available for Visual Studio 2015:</span></span>

* <span data-ttu-id="5a025-117">Již nebude nainstalován úrovně balíčků řešení</span><span class="sxs-lookup"><span data-stu-id="5a025-117">Solution level packages can no longer be installed</span></span>

<span data-ttu-id="5a025-118">Už nejsou k dispozici pro Visual Studio 2015 a projekty, které používají tyto funkce `project.json` specifikace</span><span class="sxs-lookup"><span data-stu-id="5a025-118">The following features are no longer available for Visual Studio 2015 and projects that use the `project.json` specification</span></span>

* <span data-ttu-id="5a025-119">`install.ps1` a `uninstall.ps1` – tyto skripty se mají ignorovat během instalace balíčku, obnovení, aktualizovat a odinstalace</span><span class="sxs-lookup"><span data-stu-id="5a025-119">`install.ps1` and `uninstall.ps1` - These scripts will be ignored during package install, restore, update, and uninstall</span></span>
* <span data-ttu-id="5a025-120">Konfigurace transformace se bude ignorovat.</span><span class="sxs-lookup"><span data-stu-id="5a025-120">Configuration transforms will be ignored</span></span>
* <span data-ttu-id="5a025-121">Obsah se provádí, ale ne zkopírovat do projektu.</span><span class="sxs-lookup"><span data-stu-id="5a025-121">Content will be carried, but not copied into a project.</span></span>
    * <span data-ttu-id="5a025-122">Tým pracuje na znovu implementací této funkce, sledovat diskusi a průběh na: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span><span class="sxs-lookup"><span data-stu-id="5a025-122">The team is working to re-implement this feature, follow the discussion and progress at: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span></span>


### <a name="known-issues"></a><span data-ttu-id="5a025-123">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="5a025-123">Known Issues</span></span>

<span data-ttu-id="5a025-124">Došlo k několika problémech doručit v této vydané verzi.</span><span class="sxs-lookup"><span data-stu-id="5a025-124">There were a number of known issues delivered with this release.</span></span>

* <span data-ttu-id="5a025-125">Instalace verze 3.1 Windows 10 SDK se downgradovat verzi rozšíření NuGet, který byl dříve nainstalován</span><span class="sxs-lookup"><span data-stu-id="5a025-125">Installation of the 3.1 release with the Windows 10 SDK will downgrade any version of NuGet extension that was previously installed</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="5a025-126">NuGet příkazového řádku</span><span class="sxs-lookup"><span data-stu-id="5a025-126">NuGet Command-line</span></span>

<span data-ttu-id="5a025-127">Spustitelný soubor příkazového řádku NuGet byla aktualizován a přesunout do nového umístění Distribuovatelný tak, aby historických verzí tohoto nuget.exe nadále být k dispozici.</span><span class="sxs-lookup"><span data-stu-id="5a025-127">The NuGet command-line executable was updated and moved to a new distributable location so that historical versions of nuget.exe can continue to be made available.</span></span>  <span data-ttu-id="5a025-128">3.1 beta verze programu nuget.exe můžete stáhnout pro Windows na: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="5a025-128">You can download the 3.1 beta version of nuget.exe for Windows at: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span></span>

<span data-ttu-id="5a025-129">Nové Distribuovatelný umístění nachází na dist.nuget.org hostitel, s struktury složek, která následuje tuto šablonu:</span><span class="sxs-lookup"><span data-stu-id="5a025-129">The new distributable location resides on the dist.nuget.org host, with a folder structure that follows this template:</span></span>

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a><span data-ttu-id="5a025-130">Nové funkce</span><span class="sxs-lookup"><span data-stu-id="5a025-130">New Features</span></span>

* <span data-ttu-id="5a025-131">obnovit a nainstalujte balíčky do projektů, které používají nuget.exe `project.json` souboru.</span><span class="sxs-lookup"><span data-stu-id="5a025-131">nuget.exe can restore and install packages into projects that use a `project.json` file.</span></span>
* <span data-ttu-id="5a025-132">nuget.exe můžou připojit k a využívat protokol v3 NuGet na: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span><span class="sxs-lookup"><span data-stu-id="5a025-132">nuget.exe can connect to and consume the NuGet v3 protocol at: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span></span>

## <a name="known-issues"></a><span data-ttu-id="5a025-133">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="5a025-133">Known Issues</span></span> ##

1.    <span data-ttu-id="5a025-134">Nelze provést pack proti `project.json` soubor – [928](https://github.com/NuGet/Home/issues/928)</span><span class="sxs-lookup"><span data-stu-id="5a025-134">Cannot execute pack against a `project.json` file - [928](https://github.com/NuGet/Home/issues/928)</span></span>
2.    <span data-ttu-id="5a025-135">Není podporován v Mono - [. 1059](https://github.com/NuGet/Home/issues/1059)</span><span class="sxs-lookup"><span data-stu-id="5a025-135">Is not supported on Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span></span>
3.    <span data-ttu-id="5a025-136">Nelokalizovaný - [1058](https://github.com/NuGet/Home/issues/1058), [1057](https://github.com/NuGet/Home/issues/1057)</span><span class="sxs-lookup"><span data-stu-id="5a025-136">Is not localized - [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span></span>
4.    <span data-ttu-id="5a025-137">Není podepsaný, stejně jako stávající http://nuget.org/nuget.exe  -  [1073](https://github.com/NuGet/Home/issues/1073)</span><span class="sxs-lookup"><span data-stu-id="5a025-137">Is not signed, just like the existing http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)</span></span>
