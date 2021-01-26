---
title: Zpráva k vydání verze NuGet 3,1
description: Poznámky k verzi pro NuGet 3,1, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e1dc31e2543610b1da395f77fd2424bd85d985ef
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776535"
---
# <a name="nuget-31-release-notes"></a><span data-ttu-id="93938-103">Zpráva k vydání verze NuGet 3,1</span><span class="sxs-lookup"><span data-stu-id="93938-103">NuGet 3.1 Release Notes</span></span>

<span data-ttu-id="93938-104">Zpráva k [vydání verze](../release-notes/nuget-3.0.0.md)  |  NuGet 3,0 [Poznámky k verzi NuGet 3.1.1](../release-notes/nuget-3.1.1.md)</span><span class="sxs-lookup"><span data-stu-id="93938-104">[NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 Release Notes](../release-notes/nuget-3.1.1.md)</span></span>

<span data-ttu-id="93938-105">Balíčky NuGet 3,1 byly vydány 27. července 2015 jako rozšíření Univerzální platforma Windows SDK pro sadu Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="93938-105">NuGet 3.1 was released on July 27, 2015 as a bundled extension to the Universal Windows Platform SDK for Visual Studio 2015.</span></span> <span data-ttu-id="93938-106">Tuto verzi jsme dodali pomocí sady Windows Platform SDK, aby prostředí pro vývoj systému Windows mohlo využít výhod sady NuGet pro více platforem, kterou jste dříve spustili.</span><span class="sxs-lookup"><span data-stu-id="93938-106">We delivered this release with the Windows Platform SDK so that the Windows development experience could take advantage of the NuGet cross-platform work that had been previously started.</span></span> <span data-ttu-id="93938-107">Tato verze rozšíření NuGet je dostupná jenom pro Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="93938-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="93938-108">Doporučujeme vývojářům, kteří mají přístup k aktualizaci galerie sady Visual Studio, k nejnovější verzi, která je k dispozici, protože vždy publikujete aktualizace s opravami chyb a novými funkcemi.</span><span class="sxs-lookup"><span data-stu-id="93938-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are always publishing updates with bug fixes and new features.</span></span>

## <a name="nuget-visual-studio-extension"></a><span data-ttu-id="93938-109">Rozšíření sady Visual Studio NuGet</span><span class="sxs-lookup"><span data-stu-id="93938-109">NuGet Visual Studio Extension</span></span>

<span data-ttu-id="93938-110">Problémy a funkce v této verzi jsou označené na GitHubu s celkovým [milníkem "3,1 RTM UWP pro přenosnou podporu"](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  . v této verzi jsme uzavřeli 67 3,1 problémy.</span><span class="sxs-lookup"><span data-stu-id="93938-110">Issues and features in this release are tagged on GitHub with the ["3.1 RTM UWP transitive support" milestone](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  In total, we closed 67 issues in the 3.1 release.</span></span>

### <a name="new-features"></a><span data-ttu-id="93938-111">Nové funkce</span><span class="sxs-lookup"><span data-stu-id="93938-111">New Features</span></span>

* <span data-ttu-id="93938-112">`project.json` Podpora pro Windows UWP a ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="93938-112">`project.json` support for Windows UWP and ASP.NET 5 support</span></span>
* <span data-ttu-id="93938-113">Instalace přenosného balíčku</span><span class="sxs-lookup"><span data-stu-id="93938-113">Transitive package installation</span></span>

<span data-ttu-id="93938-114">Popis a definice těchto funkcí najdete jinde v dokumentaci.</span><span class="sxs-lookup"><span data-stu-id="93938-114">Description and definition of these features can be found elsewhere in the documentation.</span></span>

### <a name="deprecated"></a><span data-ttu-id="93938-115">Zastaralé</span><span class="sxs-lookup"><span data-stu-id="93938-115">Deprecated</span></span>

<span data-ttu-id="93938-116">Pro Visual Studio 2015 již nejsou k dispozici následující funkce:</span><span class="sxs-lookup"><span data-stu-id="93938-116">The following features are no longer available for Visual Studio 2015:</span></span>

* <span data-ttu-id="93938-117">Balíčky na úrovni řešení již nelze instalovat.</span><span class="sxs-lookup"><span data-stu-id="93938-117">Solution level packages can no longer be installed</span></span>

<span data-ttu-id="93938-118">Následující funkce již nejsou k dispozici pro Visual Studio 2015 a projekty, které používají `project.json` specifikaci.</span><span class="sxs-lookup"><span data-stu-id="93938-118">The following features are no longer available for Visual Studio 2015 and projects that use the `project.json` specification</span></span>

* <span data-ttu-id="93938-119">`install.ps1` a `uninstall.ps1` – tyto skripty se během instalace, obnovení, aktualizace a odinstalace balíčku budou ignorovat</span><span class="sxs-lookup"><span data-stu-id="93938-119">`install.ps1` and `uninstall.ps1` - These scripts will be ignored during package install, restore, update, and uninstall</span></span>
* <span data-ttu-id="93938-120">Transformace konfigurace budou ignorovány.</span><span class="sxs-lookup"><span data-stu-id="93938-120">Configuration transforms will be ignored</span></span>
* <span data-ttu-id="93938-121">Obsah se přenese, ale nezkopíruje do projektu.</span><span class="sxs-lookup"><span data-stu-id="93938-121">Content will be carried, but not copied into a project.</span></span>
    * <span data-ttu-id="93938-122">Tým pracuje na opětovné implementaci této funkce, a to po diskuzi a postupu na: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span><span class="sxs-lookup"><span data-stu-id="93938-122">The team is working to re-implement this feature, follow the discussion and progress at: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span></span>


### <a name="known-issues"></a><span data-ttu-id="93938-123">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="93938-123">Known Issues</span></span>

<span data-ttu-id="93938-124">V této verzi se dodávalo několik známých problémů.</span><span class="sxs-lookup"><span data-stu-id="93938-124">There were a number of known issues delivered with this release.</span></span>

* <span data-ttu-id="93938-125">Instalace verze 3,1 s Windows 10 SDK se bude downgradovat na všechny verze rozšíření NuGet, které se dřív nainstalovaly.</span><span class="sxs-lookup"><span data-stu-id="93938-125">Installation of the 3.1 release with the Windows 10 SDK will downgrade any version of NuGet extension that was previously installed</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="93938-126">Příkazový řádek NuGet</span><span class="sxs-lookup"><span data-stu-id="93938-126">NuGet Command-line</span></span>

<span data-ttu-id="93938-127">Spustitelný soubor příkazového řádku NuGet byl aktualizován a přesunut do nového distribuovatelnýho umístění, aby bylo možné nadále zpřístupnit historické verze nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="93938-127">The NuGet command-line executable was updated and moved to a new distributable location so that historical versions of nuget.exe can continue to be made available.</span></span>  <span data-ttu-id="93938-128">Verzi 3,1 beta nuget.exe pro Windows si můžete stáhnout v: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="93938-128">You can download the 3.1 beta version of nuget.exe for Windows at: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span></span>

<span data-ttu-id="93938-129">Nové Distribuovatelný umístění se nachází na hostiteli dist.nuget.org se strukturou složek, která následuje po této šabloně:</span><span class="sxs-lookup"><span data-stu-id="93938-129">The new distributable location resides on the dist.nuget.org host, with a folder structure that follows this template:</span></span>

```
{platform supported}/{version}/nuget.exe
```

### <a name="new-features"></a><span data-ttu-id="93938-130">Nové funkce</span><span class="sxs-lookup"><span data-stu-id="93938-130">New Features</span></span>

* <span data-ttu-id="93938-131">nuget.exe může obnovit a nainstalovat balíčky do projektů, které používají `project.json` soubor.</span><span class="sxs-lookup"><span data-stu-id="93938-131">nuget.exe can restore and install packages into projects that use a `project.json` file.</span></span>
* <span data-ttu-id="93938-132">nuget.exe se může připojit k protokolu NuGet v3 a využívat ho v těchto umístěních: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span><span class="sxs-lookup"><span data-stu-id="93938-132">nuget.exe can connect to and consume the NuGet v3 protocol at: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span></span>

## <a name="known-issues"></a><span data-ttu-id="93938-133">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="93938-133">Known Issues</span></span> ##

1.    <span data-ttu-id="93938-134">Nelze provést balíček proti `project.json` souboru – [928](https://github.com/NuGet/Home/issues/928)</span><span class="sxs-lookup"><span data-stu-id="93938-134">Cannot execute pack against a `project.json` file - [928](https://github.com/NuGet/Home/issues/928)</span></span>
2.    <span data-ttu-id="93938-135">Není podporováno v mono- [1059](https://github.com/NuGet/Home/issues/1059)</span><span class="sxs-lookup"><span data-stu-id="93938-135">Is not supported on Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span></span>
3.    <span data-ttu-id="93938-136">Není lokalizováno- [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span><span class="sxs-lookup"><span data-stu-id="93938-136">Is not localized - [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span></span>
4.    <span data-ttu-id="93938-137">Není podepsáno, stejně jako stávající http://nuget.org/nuget.exe  -  [1073](https://github.com/NuGet/Home/issues/1073)</span><span class="sxs-lookup"><span data-stu-id="93938-137">Is not signed, just like the existing http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)</span></span>
