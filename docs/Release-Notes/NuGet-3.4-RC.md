---
title: "Poznámky k verzi 3.4 RC NuGet | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 239d3d95-5a72-4fac-8389-b6deac27884d
description: "Poznámky k verzi pro NuGet 3.4 RC včetně známé problémy, opravy chyb, přidaných funkcí a chcete."
keywords: "NuGet 3.4 k vydání verze RC, opravy chyb známé problémy, přidat funkce, chcete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 86c37d516eede2ac5e6e5e842f687a8f3b17c0a4
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="7a695-104">Poznámky k verzi 3.4 RC NuGet</span><span class="sxs-lookup"><span data-stu-id="7a695-104">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="7a695-105">[Poznámky k verzi NuGet 3.3](../release-notes/nuget-3.3.md) | [NuGet 3.4 poznámky k verzi](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="7a695-105">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="7a695-106">NuGet 3.4-RC byla vydána 3. března 2016 spolu s Visual Studio 2015 Update 2 RC a byl sestaven s několika principů v rozhodnutí:</span><span class="sxs-lookup"><span data-stu-id="7a695-106">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

*  <span data-ttu-id="7a695-107">Podpora více platforem</span><span class="sxs-lookup"><span data-stu-id="7a695-107">Cross-Platform support</span></span>
*  <span data-ttu-id="7a695-108">Vylepšení výkonu</span><span class="sxs-lookup"><span data-stu-id="7a695-108">Performance improvements</span></span>
*  <span data-ttu-id="7a695-109">Méně závažné vylepšení uživatelského rozhraní</span><span class="sxs-lookup"><span data-stu-id="7a695-109">Minor UI improvements</span></span>

<span data-ttu-id="7a695-110">Následující funkce jsou k dispozici v této RC s více plánované pro 3,4 finální verzi.</span><span class="sxs-lookup"><span data-stu-id="7a695-110">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="7a695-111">Nové funkce</span><span class="sxs-lookup"><span data-stu-id="7a695-111">New Features</span></span>

* <span data-ttu-id="7a695-112">Klienti NuGet nyní podporují gzip kódování obsahu z úložiště</span><span class="sxs-lookup"><span data-stu-id="7a695-112">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="7a695-113">Podpora pro soubory PDB z balíčků projektů xproj</span><span class="sxs-lookup"><span data-stu-id="7a695-113">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="7a695-114">Podpora pro iOS a Android akce v elementu contentFiles sestavení</span><span class="sxs-lookup"><span data-stu-id="7a695-114">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="7a695-115">Podpora monikerů netstandard a netstandardapp monikery framework</span><span class="sxs-lookup"><span data-stu-id="7a695-115">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="7a695-116">Nové funkce uživatelského rozhraní</span><span class="sxs-lookup"><span data-stu-id="7a695-116">New User Interface Features</span></span>

* <span data-ttu-id="7a695-117">Významné zlepšení výkonu hlavně na kartách nainstalovaná, aktualizace a konsolidace</span><span class="sxs-lookup"><span data-stu-id="7a695-117">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="7a695-118">Nainstalovaná a aktualizace karty jsou teď řadí abecedně</span><span class="sxs-lookup"><span data-stu-id="7a695-118">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="7a695-119">Přidat tlačítko Aktualizovat, která umožňuje vyhledávání nutné aktualizovat</span><span class="sxs-lookup"><span data-stu-id="7a695-119">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="7a695-120">Aktualizace a vylepšení</span><span class="sxs-lookup"><span data-stu-id="7a695-120">Updates and Improvements</span></span>

* <span data-ttu-id="7a695-121">Balíčky, kterou se odkazuje v `project.json` mají plovoucí verze nebude aktualizovat na každé sestavení.</span><span class="sxs-lookup"><span data-stu-id="7a695-121">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="7a695-122">Místo toho bude aktualizovat pouze v případě, že vynutit obnovení, vyčistit, znovu sestavit nebo upravit `project.json`.</span><span class="sxs-lookup"><span data-stu-id="7a695-122">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="7a695-123">nuget.org úložiště zdrojů již nebude, vynuceně přesunuty do konfigurace projektu při použití konfigurace NuGet uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="7a695-123">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="7a695-124">NuGet už obnoví balíčků ve sdílených projektů ani zapisuje do souboru zámku.</span><span class="sxs-lookup"><span data-stu-id="7a695-124">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="7a695-125">Jsme jste vylepšené selhání sítě a opakujte zpracování pro nedostupné nebo pomalé na reakce serverů.</span><span class="sxs-lookup"><span data-stu-id="7a695-125">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="7a695-126">Chování klávesnici a myš jsou vylepšení v uživatelském rozhraní Správce balíčků Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7a695-126">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="7a695-127">Teď podporujeme nejnovější `project.json` schéma v DNX.</span><span class="sxs-lookup"><span data-stu-id="7a695-127">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="7a695-128">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="7a695-128">Known Issues</span></span>

<span data-ttu-id="7a695-129">Abychom mohli pokračovat ke sledování problémů na našich seznamu problémy Githubu, které naleznete na adrese: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="7a695-129">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>