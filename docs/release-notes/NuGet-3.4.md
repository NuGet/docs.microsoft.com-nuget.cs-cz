---
title: NuGet 3.4 poznámky
description: Zpráva k vydání verze pro NuGet 3.4, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 77c0117fc40031a327e8dcb0aac5cd4045239e97
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551188"
---
# <a name="nuget-34-release-notes"></a><span data-ttu-id="31d56-103">NuGet 3.4 poznámky</span><span class="sxs-lookup"><span data-stu-id="31d56-103">NuGet 3.4 Release Notes</span></span>

<span data-ttu-id="31d56-104">[Poznámky k verzi 3.4 RC NuGet](../release-notes/nuget-3.4-RC.md) | [zpráva k vydání verze NuGet 3.4.1](../release-notes/nuget-3.4.1.md)</span><span class="sxs-lookup"><span data-stu-id="31d56-104">[NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md)</span></span>

<span data-ttu-id="31d56-105">NuGet 3.4 30. března 2016 byla vydána jako součást Visual Studio 2015 Update 2 a Preview verze sady Visual Studio 15 a byl sestaven s několika zásady v mozky:</span><span class="sxs-lookup"><span data-stu-id="31d56-105">NuGet 3.4 was released March 30, 2016 as part of the Visual Studio 2015 Update 2 and Visual Studio 15 Preview Release and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="31d56-106">Podporu pro různé platformy</span><span class="sxs-lookup"><span data-stu-id="31d56-106">Cross-Platform support</span></span>
* <span data-ttu-id="31d56-107">Vylepšení výkonu</span><span class="sxs-lookup"><span data-stu-id="31d56-107">Performance improvements</span></span>
* <span data-ttu-id="31d56-108">Menší vylepšení uživatelského rozhraní</span><span class="sxs-lookup"><span data-stu-id="31d56-108">Minor UI improvements</span></span>

<span data-ttu-id="31d56-109">Následující funkce byly dříve přidány do verze RC a byly aktualizovány nebo dokončení verze 3.4:</span><span class="sxs-lookup"><span data-stu-id="31d56-109">The following features were previously added in the RC and have been updated or completed for the 3.4 release:</span></span>

## <a name="new-features"></a><span data-ttu-id="31d56-110">Nové funkce</span><span class="sxs-lookup"><span data-stu-id="31d56-110">New Features</span></span>

* <span data-ttu-id="31d56-111">Klienti NuGet nyní podporují kódování obsahu gzip z úložišť</span><span class="sxs-lookup"><span data-stu-id="31d56-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="31d56-112">Podpora pro soubory PDB z balíčků v projektech xproj</span><span class="sxs-lookup"><span data-stu-id="31d56-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="31d56-113">Podpora pro iOS a akce sestavení pro Android v elementu contentFiles</span><span class="sxs-lookup"><span data-stu-id="31d56-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="31d56-114">Podpora rozhraní framework monikerů netstandard a netstandardapp</span><span class="sxs-lookup"><span data-stu-id="31d56-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="31d56-115">Nové funkce uživatelského rozhraní</span><span class="sxs-lookup"><span data-stu-id="31d56-115">New User Interface Features</span></span>

* <span data-ttu-id="31d56-116">Výrazné zlepšení výkonu zejména na kartách instalace, aktualizace a konsolidaci</span><span class="sxs-lookup"><span data-stu-id="31d56-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="31d56-117">Je k dispozici ke slučování výsledků hledání správné agregovaného zdroje 'všechny zdroje balíčků.</span><span class="sxs-lookup"><span data-stu-id="31d56-117">Aggregate 'All Package Sources' Source is available with proper search result merging</span></span>
* <span data-ttu-id="31d56-118">Nainstalovaný a karty aktualizace jsou teď seřazené podle abecedy</span><span class="sxs-lookup"><span data-stu-id="31d56-118">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="31d56-119">Přidat tlačítko pro aktualizaci, která umožňuje vyhledávání aktualizovat</span><span class="sxs-lookup"><span data-stu-id="31d56-119">Added a Refresh button that allows a search to be refreshed</span></span>
* <span data-ttu-id="31d56-120">Nejnovější sestavení možnosti v horní části seznamu verze</span><span class="sxs-lookup"><span data-stu-id="31d56-120">Latest Build options at the top of the Version list</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="31d56-121">Aktualizace a vylepšení</span><span class="sxs-lookup"><span data-stu-id="31d56-121">Updates and Improvements</span></span>

* <span data-ttu-id="31d56-122">Balíčky odkazuje `project.json` , které mají plovoucí verze nebude aktualizovat při každém sestavení.</span><span class="sxs-lookup"><span data-stu-id="31d56-122">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="31d56-123">Místo toho bude aktualizovat jenom v případě, že vynutit obnovení, vyčistit, znovu vytvořit nebo upravit `project.json`.</span><span class="sxs-lookup"><span data-stu-id="31d56-123">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="31d56-124">nuget.org úložišť zdroje jsou již vynutit do konfigurace projektu při použití konfigurace NuGet uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="31d56-124">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="31d56-125">NuGet už obnoví balíčky ve sdílených projektech ani zapíše soubor zámku.</span><span class="sxs-lookup"><span data-stu-id="31d56-125">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="31d56-126">Jsme vylepšili selhání sítě a opakujte zpracování pro servery nedostupné nebo pomalé reakce.</span><span class="sxs-lookup"><span data-stu-id="31d56-126">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="31d56-127">Vylepšené chování klávesnice a myši v Uživatelském rozhraní Správce balíčků Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="31d56-127">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="31d56-128">Nyní podporujeme nejnovější `project.json` schéma v DNX.</span><span class="sxs-lookup"><span data-stu-id="31d56-128">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="breaking-changes"></a><span data-ttu-id="31d56-129">Nejnovější změny</span><span class="sxs-lookup"><span data-stu-id="31d56-129">Breaking Changes</span></span>

* <span data-ttu-id="31d56-130">Čísla verzí balíčku jsou nyní normalizovány na formát *hlavní*. *vedlejší*. *oprava*-*předběžnou verzi* všech hlavních, podverze a oprava jsou považovány za celých čísel a vyřadit všechny úvodní nuly.</span><span class="sxs-lookup"><span data-stu-id="31d56-130">Package version numbers are now normalized to the format *major*.*minor*.*patch*-*prerelease*   Each of major, minor, and patch are treated as integers and drop any leading zeroes.</span></span>  <span data-ttu-id="31d56-131">Informace o předběžnou verzi je považován za řetězcový a žádné změny se použijí k němu.</span><span class="sxs-lookup"><span data-stu-id="31d56-131">The prerelease information is treated as a string and no changes are applied to it.</span></span> <span data-ttu-id="31d56-132">Tyto hodnoty se používají v dotazech klienti NuGet a vyhledávání poskytovaných službou nuget.org.</span><span class="sxs-lookup"><span data-stu-id="31d56-132">These numbers are used in queries by the NuGet clients and the search provided by the nuget.org service.</span></span>  <span data-ttu-id="31d56-133">Další podrobnosti najdete v dokumentaci NuGet v rámci [zkušební verze](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="31d56-133">More details can be found in the NuGet Docs under [Prerelease Versions](../create-packages/prerelease-packages.md).</span></span>

## <a name="known-issues"></a><span data-ttu-id="31d56-134">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="31d56-134">Known Issues</span></span>

* <span data-ttu-id="31d56-135">**Problém:** Windows 10 v1511, můžou uživatelé zaznamenat potíže nebo dokonce i sady Visual Studio selhání pomocí Powershellu v sadě Visual Studio v následujících scénářích:</span><span class="sxs-lookup"><span data-stu-id="31d56-135">**Issue:** Windows 10 v1511 users may experience issues or even a Visual Studio crash with Powershell in Visual Studio in the following scenarios:</span></span>
    * <span data-ttu-id="31d56-136">Instalace / Odinstalace balíčky, které mají install.ps1 / uninstall.ps1 skriptů</span><span class="sxs-lookup"><span data-stu-id="31d56-136">Installing / Uninstalling packages that have install.ps1 / uninstall.ps1 scripts</span></span>
    * <span data-ttu-id="31d56-137">Načítají se projekty, které mají skriptu init.ps1 (např. EntityFramework)</span><span class="sxs-lookup"><span data-stu-id="31d56-137">Loading projects that have an init.ps1 script (like EntityFramework)</span></span>
    * <span data-ttu-id="31d56-138">Publikování webového obsahu</span><span class="sxs-lookup"><span data-stu-id="31d56-138">Publishing web content</span></span>

* <span data-ttu-id="31d56-139">**Alternativní řešení:** zajistěte, aby vaše instalace Windows 10 nejnovějších oprav použít, expecially leden 2016 (KB 3124263) nebo novější aktualizace.</span><span class="sxs-lookup"><span data-stu-id="31d56-139">**Workaround:** Ensure that your Windows 10 install has the latest patches applied, expecially the January 2016 (KB 3124263) or a later update.</span></span>  <span data-ttu-id="31d56-140">Další podrobnosti jsou dostupné na [problém Githubu #1638](http://github.com/nuget/home/issues/1638)</span><span class="sxs-lookup"><span data-stu-id="31d56-140">More details are available on [GitHub issue #1638](http://github.com/nuget/home/issues/1638)</span></span>

* <span data-ttu-id="31d56-141">**Problém:** Přesměrování protokolu NuGet v2 jsou přerušená.</span><span class="sxs-lookup"><span data-stu-id="31d56-141">**Issue:** NuGet v2 protocol redirects are broken.</span></span>
<span data-ttu-id="31d56-142">Vlastní úložiště NuGet, které směrují požadavky na alternativního hostitele, nerespektují požadavky přesměrování.</span><span class="sxs-lookup"><span data-stu-id="31d56-142">Custom NuGet repositories that redirect requests to an alternative host do not honor the redirect request.</span></span>
* <span data-ttu-id="31d56-143">**Alternativní řešení:** Pokud chcete tento problém obejít, nakonfigurujte identifikátor URI úložiště balíčků tak, aby odkazoval na přesměrované umístění serveru.</span><span class="sxs-lookup"><span data-stu-id="31d56-143">**Workaround:**  To work around this issue, configure the package repository URI in settings to point to the redirected server location.</span></span>
<span data-ttu-id="31d56-144">Další informace najdete v tématu [žádosti o přijetí změn Githubu #387](https://github.com/NuGet/NuGet.Client/pull/387).</span><span class="sxs-lookup"><span data-stu-id="31d56-144">For more information, see [GitHub pull request #387](https://github.com/NuGet/NuGet.Client/pull/387).</span></span>

<span data-ttu-id="31d56-145">Pokračujeme v sledování problémů v našem seznamu problémů na Githubu najdete je na: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="31d56-145">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>