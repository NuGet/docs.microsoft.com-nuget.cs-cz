---
title: "Poznámky k verzi NuGet 3.1 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 0fc4d89a-ccca-4d63-85bf-461cd9ced882
description: "Poznámky k verzi pro včetně známé problémy, opravy chyb, přidaných funkcí a chcete 3.1 NuGet."
keywords: "NuGet 3.1 poznámky k verzi, opravy chyb známé problémy, přidat funkce, chcete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: eef2b2c1af99671c7ae3874c2c12130f104e88eb
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-31-release-notes"></a><span data-ttu-id="a5e6b-104">Poznámky k verzi 3.1 NuGet</span><span class="sxs-lookup"><span data-stu-id="a5e6b-104">NuGet 3.1 Release Notes</span></span>

<span data-ttu-id="a5e6b-105">[Poznámky k verzi NuGet 3.0](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 poznámky k verzi](../release-notes/nuget-3.1.1.md)</span><span class="sxs-lookup"><span data-stu-id="a5e6b-105">[NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 Release Notes](../release-notes/nuget-3.1.1.md)</span></span>

<span data-ttu-id="a5e6b-106">NuGet 3.1 byla vydána 27. července 2015 jako připojené rozšíření pro univerzální platformu Windows SDK pro Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="a5e6b-106">NuGet 3.1 was released on July 27, 2015 as a bundled extension to the Universal Windows Platform SDK for Visual Studio 2015.</span></span> <span data-ttu-id="a5e6b-107">Tato verze sada Windows SDK pro platformu poskytneme tak, aby vývojového prostředí systému Windows může využít pracovní NuGet a platformy, která již byla dříve spuštěna.</span><span class="sxs-lookup"><span data-stu-id="a5e6b-107">We delivered this release with the Windows Platform SDK so that the Windows development experience could take advantage of the NuGet cross-platform work that had been previously started.</span></span> <span data-ttu-id="a5e6b-108">Tato verze rozšíření NuGet je dostupná jenom pro Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="a5e6b-108">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="a5e6b-109">Doporučujeme, abyste tyto vývojáři, kteří mají přístup k sadě Visual Studio Galerie aktualizaci na nejnovější verzi, která je k dispozici, protože jsme se vždy publikování aktualizace s oprav chyb a nové funkce.</span><span class="sxs-lookup"><span data-stu-id="a5e6b-109">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are always publishing updates with bug fixes and new features.</span></span>

## <a name="nuget-visual-studio-extension"></a><span data-ttu-id="a5e6b-110">Rozšíření NuGet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a5e6b-110">NuGet Visual Studio Extension</span></span>

<span data-ttu-id="a5e6b-111">Problémy a funkce v této verzi jsou označené na Githubu se ["3.1 přenositelné podpora RTM UWP" milník](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+) celkem, jsme uzavřený 67 problémů v 3.1 vydání.</span><span class="sxs-lookup"><span data-stu-id="a5e6b-111">Issues and features in this release are tagged on GitHub with the ["3.1 RTM UWP transitive support" milestone](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  In total, we closed 67 issues in the 3.1 release.</span></span>

### <a name="new-features"></a><span data-ttu-id="a5e6b-112">Nové funkce</span><span class="sxs-lookup"><span data-stu-id="a5e6b-112">New Features</span></span>

* <span data-ttu-id="a5e6b-113">`project.json`Podpora pro podporu Windows UWP a ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="a5e6b-113">`project.json` support for Windows UWP and ASP.NET 5 support</span></span>
* <span data-ttu-id="a5e6b-114">Instalace přenositelné balíčku</span><span class="sxs-lookup"><span data-stu-id="a5e6b-114">Transitive package installation</span></span>

<span data-ttu-id="a5e6b-115">Popis a definice těchto funkcí jinde v dokumentaci.</span><span class="sxs-lookup"><span data-stu-id="a5e6b-115">Description and definition of these features can be found elsewhere in the documentation.</span></span>

### <a name="deprecated"></a><span data-ttu-id="a5e6b-116">Zastaralé</span><span class="sxs-lookup"><span data-stu-id="a5e6b-116">Deprecated</span></span>

<span data-ttu-id="a5e6b-117">Již nejsou k dispozici pro Visual Studio 2015 následující funkce:</span><span class="sxs-lookup"><span data-stu-id="a5e6b-117">The following features are no longer available for Visual Studio 2015:</span></span>

* <span data-ttu-id="a5e6b-118">Úrovně balíčků řešení už ji instalovat</span><span class="sxs-lookup"><span data-stu-id="a5e6b-118">Solution level packages can no longer be installed</span></span>

<span data-ttu-id="a5e6b-119">Již nejsou k dispozici pro Visual Studio 2015 a projekty, které používají následující funkce `project.json` specifikace</span><span class="sxs-lookup"><span data-stu-id="a5e6b-119">The following features are no longer available for Visual Studio 2015 and projects that use the `project.json` specification</span></span>

* <span data-ttu-id="a5e6b-120">`install.ps1`a `uninstall.ps1` -tyto skripty během instalace balíčku se bude ignorovat, obnovit, aktualizovat a odinstalace</span><span class="sxs-lookup"><span data-stu-id="a5e6b-120">`install.ps1` and `uninstall.ps1` - These scripts will be ignored during package install, restore, update, and uninstall</span></span>
* <span data-ttu-id="a5e6b-121">Konfigurace transformací budou ignorovány.</span><span class="sxs-lookup"><span data-stu-id="a5e6b-121">Configuration transforms will be ignored</span></span>
* <span data-ttu-id="a5e6b-122">Obsah se provádí, ale není zkopírovat do projektu.</span><span class="sxs-lookup"><span data-stu-id="a5e6b-122">Content will be carried, but not copied into a project.</span></span>
    * <span data-ttu-id="a5e6b-123">Tým pracuje na znovu implementací této funkce, postupujte podle diskuse a v průběhu: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span><span class="sxs-lookup"><span data-stu-id="a5e6b-123">The team is working to re-implement this feature, follow the discussion and progress at: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span></span>


### <a name="known-issues"></a><span data-ttu-id="a5e6b-124">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="a5e6b-124">Known Issues</span></span>

<span data-ttu-id="a5e6b-125">Došlo k několika známých problémů doručit v této verzi.</span><span class="sxs-lookup"><span data-stu-id="a5e6b-125">There were a number of known issues delivered with this release.</span></span>

* <span data-ttu-id="a5e6b-126">Instalace verze 3.1 s Windows 10 SDK se downgradovat verzi rozšíření NuGet, který byl dříve nainstalován</span><span class="sxs-lookup"><span data-stu-id="a5e6b-126">Installation of the 3.1 release with the Windows 10 SDK will downgrade any version of NuGet extension that was previously installed</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="a5e6b-127">NuGet příkazového řádku</span><span class="sxs-lookup"><span data-stu-id="a5e6b-127">NuGet Command-line</span></span>

<span data-ttu-id="a5e6b-128">Spustitelný soubor příkazového řádku NuGet byl aktualizován a přesunout do nového umístění distribuovatelného, aby mohl pokračovat historických verzích nuget.exe bylo k dispozici.</span><span class="sxs-lookup"><span data-stu-id="a5e6b-128">The NuGet command-line executable was updated and moved to a new distributable location so that historical versions of nuget.exe can continue to be made available.</span></span>  <span data-ttu-id="a5e6b-129">3.1 beta verzi nuget.exe můžete stáhnout pro Windows v: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="a5e6b-129">You can download the 3.1 beta version of nuget.exe for Windows at: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span></span>

<span data-ttu-id="a5e6b-130">Nové distribuovatelného umístění se nachází na hostiteli dist.nuget.org s strukturu složek, která následuje tuto šablonu:</span><span class="sxs-lookup"><span data-stu-id="a5e6b-130">The new distributable location resides on the dist.nuget.org host, with a folder structure that follows this template:</span></span>

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a><span data-ttu-id="a5e6b-131">Nové funkce</span><span class="sxs-lookup"><span data-stu-id="a5e6b-131">New Features</span></span>

* <span data-ttu-id="a5e6b-132">můžete obnovit a nainstalovat balíčky do projektů, které používají nuget.exe `project.json` souboru.</span><span class="sxs-lookup"><span data-stu-id="a5e6b-132">nuget.exe can restore and install packages into projects that use a `project.json` file.</span></span>
* <span data-ttu-id="a5e6b-133">připojení a využívat protokol NuGet v3 na nuget.exe lze: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span><span class="sxs-lookup"><span data-stu-id="a5e6b-133">nuget.exe can connect to and consume the NuGet v3 protocol at: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span></span>

## <a name="known-issues"></a><span data-ttu-id="a5e6b-134">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="a5e6b-134">Known Issues</span></span> ##

1.    <span data-ttu-id="a5e6b-135">Nelze provést pack proti `project.json` soubor - [928](https://github.com/NuGet/Home/issues/928)</span><span class="sxs-lookup"><span data-stu-id="a5e6b-135">Cannot execute pack against a `project.json` file - [928](https://github.com/NuGet/Home/issues/928)</span></span>
2.    <span data-ttu-id="a5e6b-136">Není podporována na Mono - [. 1059](https://github.com/NuGet/Home/issues/1059)</span><span class="sxs-lookup"><span data-stu-id="a5e6b-136">Is not supported on Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span></span>
3.    <span data-ttu-id="a5e6b-137">Nelokalizovaný - [1058](https://github.com/NuGet/Home/issues/1058), [1057](https://github.com/NuGet/Home/issues/1057)</span><span class="sxs-lookup"><span data-stu-id="a5e6b-137">Is not localized - [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span></span>
4.    <span data-ttu-id="a5e6b-138">Není podepsaný, stejně jako existující http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)</span><span class="sxs-lookup"><span data-stu-id="a5e6b-138">Is not signed, just like the existing http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)</span></span>
