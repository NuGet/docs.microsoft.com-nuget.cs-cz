---
title: NuGet 3.4 RC poznámky
description: Zpráva k vydání verze pro NuGet 3.4 RC, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 795bdcfaa2e22447856b60d05807aeb0992cdfa0
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546751"
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="8a228-103">NuGet 3.4 RC poznámky</span><span class="sxs-lookup"><span data-stu-id="8a228-103">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="8a228-104">[Zpráva k vydání verze NuGet 3.3](../release-notes/nuget-3.3.md) | [zpráva k vydání verze NuGet 3.4](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="8a228-104">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="8a228-105">NuGet 3.4-RC byla vydána 3. března 2016 souběžně s Visual Studio 2015 Update 2 RC a byl sestaven s několika zásady v mozky:</span><span class="sxs-lookup"><span data-stu-id="8a228-105">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="8a228-106">Podporu pro různé platformy</span><span class="sxs-lookup"><span data-stu-id="8a228-106">Cross-Platform support</span></span>
* <span data-ttu-id="8a228-107">Vylepšení výkonu</span><span class="sxs-lookup"><span data-stu-id="8a228-107">Performance improvements</span></span>
* <span data-ttu-id="8a228-108">Menší vylepšení uživatelského rozhraní</span><span class="sxs-lookup"><span data-stu-id="8a228-108">Minor UI improvements</span></span>

<span data-ttu-id="8a228-109">Následující funkce jsou dostupné v této verzi RC další plánované 3.4 finální verzi.</span><span class="sxs-lookup"><span data-stu-id="8a228-109">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="8a228-110">Nové funkce</span><span class="sxs-lookup"><span data-stu-id="8a228-110">New Features</span></span>

* <span data-ttu-id="8a228-111">Klienti NuGet nyní podporují kódování obsahu gzip z úložišť</span><span class="sxs-lookup"><span data-stu-id="8a228-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="8a228-112">Podpora pro soubory PDB z balíčků v projektech xproj</span><span class="sxs-lookup"><span data-stu-id="8a228-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="8a228-113">Podpora pro iOS a akce sestavení pro Android v elementu contentFiles</span><span class="sxs-lookup"><span data-stu-id="8a228-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="8a228-114">Podpora rozhraní framework monikerů netstandard a netstandardapp</span><span class="sxs-lookup"><span data-stu-id="8a228-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="8a228-115">Nové funkce uživatelského rozhraní</span><span class="sxs-lookup"><span data-stu-id="8a228-115">New User Interface Features</span></span>

* <span data-ttu-id="8a228-116">Výrazné zlepšení výkonu zejména na kartách instalace, aktualizace a konsolidaci</span><span class="sxs-lookup"><span data-stu-id="8a228-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="8a228-117">Nainstalovaný a karty aktualizace jsou teď seřazené podle abecedy</span><span class="sxs-lookup"><span data-stu-id="8a228-117">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="8a228-118">Přidat tlačítko pro aktualizaci, která umožňuje vyhledávání aktualizovat</span><span class="sxs-lookup"><span data-stu-id="8a228-118">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="8a228-119">Aktualizace a vylepšení</span><span class="sxs-lookup"><span data-stu-id="8a228-119">Updates and Improvements</span></span>

* <span data-ttu-id="8a228-120">Balíčky odkazuje `project.json` , které mají plovoucí verze nebude aktualizovat při každém sestavení.</span><span class="sxs-lookup"><span data-stu-id="8a228-120">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="8a228-121">Místo toho bude aktualizovat jenom v případě, že vynutit obnovení, vyčistit, znovu vytvořit nebo upravit `project.json`.</span><span class="sxs-lookup"><span data-stu-id="8a228-121">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="8a228-122">nuget.org úložišť zdroje jsou již vynutit do konfigurace projektu při použití konfigurace NuGet uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="8a228-122">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="8a228-123">NuGet už obnoví balíčky ve sdílených projektech ani zapíše soubor zámku.</span><span class="sxs-lookup"><span data-stu-id="8a228-123">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="8a228-124">Jsme vylepšili selhání sítě a opakujte zpracování pro servery nedostupné nebo pomalé reakce.</span><span class="sxs-lookup"><span data-stu-id="8a228-124">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="8a228-125">Vylepšené chování klávesnice a myši v Uživatelském rozhraní Správce balíčků Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8a228-125">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="8a228-126">Nyní podporujeme nejnovější `project.json` schéma v DNX.</span><span class="sxs-lookup"><span data-stu-id="8a228-126">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="8a228-127">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="8a228-127">Known Issues</span></span>

<span data-ttu-id="8a228-128">Pokračujeme v sledování problémů v našem seznamu problémů na Githubu najdete je na: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="8a228-128">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>