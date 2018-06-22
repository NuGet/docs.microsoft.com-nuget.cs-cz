---
title: Poznámky k verzi 3.1 NuGet
description: Poznámky k verzi pro včetně známé problémy, opravy chyb, přidaných funkcí a chcete 3.1 NuGet.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d14455da6f8af4db92f7105ea1b0e88eb9e71600
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820863"
---
# <a name="nuget-31-release-notes"></a><span data-ttu-id="7beca-103">Poznámky k verzi 3.1 NuGet</span><span class="sxs-lookup"><span data-stu-id="7beca-103">NuGet 3.1 Release Notes</span></span>

<span data-ttu-id="7beca-104">[Poznámky k verzi NuGet 3.0](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 poznámky k verzi](../release-notes/nuget-3.1.1.md)</span><span class="sxs-lookup"><span data-stu-id="7beca-104">[NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 Release Notes](../release-notes/nuget-3.1.1.md)</span></span>

<span data-ttu-id="7beca-105">NuGet 3.1 byla vydána 27. července 2015 jako připojené rozšíření pro univerzální platformu Windows SDK pro Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="7beca-105">NuGet 3.1 was released on July 27, 2015 as a bundled extension to the Universal Windows Platform SDK for Visual Studio 2015.</span></span> <span data-ttu-id="7beca-106">Tato verze sada Windows SDK pro platformu poskytneme tak, aby vývojového prostředí systému Windows může využít pracovní NuGet a platformy, která již byla dříve spuštěna.</span><span class="sxs-lookup"><span data-stu-id="7beca-106">We delivered this release with the Windows Platform SDK so that the Windows development experience could take advantage of the NuGet cross-platform work that had been previously started.</span></span> <span data-ttu-id="7beca-107">Tato verze rozšíření NuGet je dostupná jenom pro Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="7beca-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="7beca-108">Doporučujeme, abyste tyto vývojáři, kteří mají přístup k sadě Visual Studio Galerie aktualizaci na nejnovější verzi, která je k dispozici, protože jsme se vždy publikování aktualizace s oprav chyb a nové funkce.</span><span class="sxs-lookup"><span data-stu-id="7beca-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are always publishing updates with bug fixes and new features.</span></span>

## <a name="nuget-visual-studio-extension"></a><span data-ttu-id="7beca-109">Rozšíření NuGet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7beca-109">NuGet Visual Studio Extension</span></span>

<span data-ttu-id="7beca-110">Problémy a funkce v této verzi jsou označené na Githubu se ["3.1 přenositelné podpora RTM UWP" milník](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+) celkem, jsme uzavřený 67 problémů v 3.1 vydání.</span><span class="sxs-lookup"><span data-stu-id="7beca-110">Issues and features in this release are tagged on GitHub with the ["3.1 RTM UWP transitive support" milestone](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  In total, we closed 67 issues in the 3.1 release.</span></span>

### <a name="new-features"></a><span data-ttu-id="7beca-111">Nové funkce</span><span class="sxs-lookup"><span data-stu-id="7beca-111">New Features</span></span>

* <span data-ttu-id="7beca-112">`project.json` Podpora pro podporu Windows UWP a ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="7beca-112">`project.json` support for Windows UWP and ASP.NET 5 support</span></span>
* <span data-ttu-id="7beca-113">Instalace přenositelné balíčku</span><span class="sxs-lookup"><span data-stu-id="7beca-113">Transitive package installation</span></span>

<span data-ttu-id="7beca-114">Popis a definice těchto funkcí jinde v dokumentaci.</span><span class="sxs-lookup"><span data-stu-id="7beca-114">Description and definition of these features can be found elsewhere in the documentation.</span></span>

### <a name="deprecated"></a><span data-ttu-id="7beca-115">Zastaralé</span><span class="sxs-lookup"><span data-stu-id="7beca-115">Deprecated</span></span>

<span data-ttu-id="7beca-116">Již nejsou k dispozici pro Visual Studio 2015 následující funkce:</span><span class="sxs-lookup"><span data-stu-id="7beca-116">The following features are no longer available for Visual Studio 2015:</span></span>

* <span data-ttu-id="7beca-117">Úrovně balíčků řešení už ji instalovat</span><span class="sxs-lookup"><span data-stu-id="7beca-117">Solution level packages can no longer be installed</span></span>

<span data-ttu-id="7beca-118">Již nejsou k dispozici pro Visual Studio 2015 a projekty, které používají následující funkce `project.json` specifikace</span><span class="sxs-lookup"><span data-stu-id="7beca-118">The following features are no longer available for Visual Studio 2015 and projects that use the `project.json` specification</span></span>

* <span data-ttu-id="7beca-119">`install.ps1` a `uninstall.ps1` -tyto skripty během instalace balíčku se bude ignorovat, obnovit, aktualizovat a odinstalace</span><span class="sxs-lookup"><span data-stu-id="7beca-119">`install.ps1` and `uninstall.ps1` - These scripts will be ignored during package install, restore, update, and uninstall</span></span>
* <span data-ttu-id="7beca-120">Konfigurace transformací budou ignorovány.</span><span class="sxs-lookup"><span data-stu-id="7beca-120">Configuration transforms will be ignored</span></span>
* <span data-ttu-id="7beca-121">Obsah se provádí, ale není zkopírovat do projektu.</span><span class="sxs-lookup"><span data-stu-id="7beca-121">Content will be carried, but not copied into a project.</span></span>
    * <span data-ttu-id="7beca-122">Tým pracuje na znovu implementací této funkce, postupujte podle diskuse a v průběhu: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span><span class="sxs-lookup"><span data-stu-id="7beca-122">The team is working to re-implement this feature, follow the discussion and progress at: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span></span>


### <a name="known-issues"></a><span data-ttu-id="7beca-123">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="7beca-123">Known Issues</span></span>

<span data-ttu-id="7beca-124">Došlo k několika známých problémů doručit v této verzi.</span><span class="sxs-lookup"><span data-stu-id="7beca-124">There were a number of known issues delivered with this release.</span></span>

* <span data-ttu-id="7beca-125">Instalace verze 3.1 s Windows 10 SDK se downgradovat verzi rozšíření NuGet, který byl dříve nainstalován</span><span class="sxs-lookup"><span data-stu-id="7beca-125">Installation of the 3.1 release with the Windows 10 SDK will downgrade any version of NuGet extension that was previously installed</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="7beca-126">NuGet příkazového řádku</span><span class="sxs-lookup"><span data-stu-id="7beca-126">NuGet Command-line</span></span>

<span data-ttu-id="7beca-127">Spustitelný soubor příkazového řádku NuGet byl aktualizován a přesunout do nového umístění distribuovatelného, aby mohl pokračovat historických verzích nuget.exe bylo k dispozici.</span><span class="sxs-lookup"><span data-stu-id="7beca-127">The NuGet command-line executable was updated and moved to a new distributable location so that historical versions of nuget.exe can continue to be made available.</span></span>  <span data-ttu-id="7beca-128">3.1 beta verzi nuget.exe můžete stáhnout pro Windows na: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="7beca-128">You can download the 3.1 beta version of nuget.exe for Windows at: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span></span>

<span data-ttu-id="7beca-129">Nové distribuovatelného umístění se nachází na hostiteli dist.nuget.org s strukturu složek, která následuje tuto šablonu:</span><span class="sxs-lookup"><span data-stu-id="7beca-129">The new distributable location resides on the dist.nuget.org host, with a folder structure that follows this template:</span></span>

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a><span data-ttu-id="7beca-130">Nové funkce</span><span class="sxs-lookup"><span data-stu-id="7beca-130">New Features</span></span>

* <span data-ttu-id="7beca-131">můžete obnovit a nainstalovat balíčky do projektů, které používají nuget.exe `project.json` souboru.</span><span class="sxs-lookup"><span data-stu-id="7beca-131">nuget.exe can restore and install packages into projects that use a `project.json` file.</span></span>
* <span data-ttu-id="7beca-132">nuget.exe můžete připojit k a využívat protokol NuGet v3 na: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span><span class="sxs-lookup"><span data-stu-id="7beca-132">nuget.exe can connect to and consume the NuGet v3 protocol at: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span></span>

## <a name="known-issues"></a><span data-ttu-id="7beca-133">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="7beca-133">Known Issues</span></span> ##

1.    <span data-ttu-id="7beca-134">Nelze provést pack proti `project.json` soubor - [928](https://github.com/NuGet/Home/issues/928)</span><span class="sxs-lookup"><span data-stu-id="7beca-134">Cannot execute pack against a `project.json` file - [928](https://github.com/NuGet/Home/issues/928)</span></span>
2.    <span data-ttu-id="7beca-135">Není podporována na Mono - [. 1059](https://github.com/NuGet/Home/issues/1059)</span><span class="sxs-lookup"><span data-stu-id="7beca-135">Is not supported on Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span></span>
3.    <span data-ttu-id="7beca-136">Nelokalizovaný - [1058](https://github.com/NuGet/Home/issues/1058), [1057](https://github.com/NuGet/Home/issues/1057)</span><span class="sxs-lookup"><span data-stu-id="7beca-136">Is not localized - [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span></span>
4.    <span data-ttu-id="7beca-137">Není podepsaný, stejně jako existující http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)</span><span class="sxs-lookup"><span data-stu-id="7beca-137">Is not signed, just like the existing http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)</span></span>
