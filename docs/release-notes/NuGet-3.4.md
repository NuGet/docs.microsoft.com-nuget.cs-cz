---
title: NuGet 3.4 poznámky
description: Poznámky k verzi pro NuGet 3.4, včetně známé problémy, opravy chyb, přidaných funkcí a chcete.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3f2a945b628022bdcc6e69a7a4b1be6c53b65626
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820469"
---
# <a name="nuget-34-release-notes"></a><span data-ttu-id="65463-103">NuGet 3.4 poznámky</span><span class="sxs-lookup"><span data-stu-id="65463-103">NuGet 3.4 Release Notes</span></span>

<span data-ttu-id="65463-104">[Poznámky k verzi 3.4 RC NuGet](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 poznámky k verzi](../release-notes/nuget-3.4.1.md)</span><span class="sxs-lookup"><span data-stu-id="65463-104">[NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md)</span></span>

<span data-ttu-id="65463-105">NuGet 3.4 byl vydané 30. března 2016 jako součást sady Visual Studio 2015 Update 2 a Visual Studio 15 Preview verze a byl sestaven s několika principů v rozhodnutí:</span><span class="sxs-lookup"><span data-stu-id="65463-105">NuGet 3.4 was released March 30, 2016 as part of the Visual Studio 2015 Update 2 and Visual Studio 15 Preview Release and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="65463-106">Podpora více platforem</span><span class="sxs-lookup"><span data-stu-id="65463-106">Cross-Platform support</span></span>
* <span data-ttu-id="65463-107">Vylepšení výkonu</span><span class="sxs-lookup"><span data-stu-id="65463-107">Performance improvements</span></span>
* <span data-ttu-id="65463-108">Méně závažné vylepšení uživatelského rozhraní</span><span class="sxs-lookup"><span data-stu-id="65463-108">Minor UI improvements</span></span>

<span data-ttu-id="65463-109">Následující funkce byly dříve přidány v RC a byly aktualizovány nebo dokončit 3,4 verzi:</span><span class="sxs-lookup"><span data-stu-id="65463-109">The following features were previously added in the RC and have been updated or completed for the 3.4 release:</span></span>

## <a name="new-features"></a><span data-ttu-id="65463-110">Nové funkce</span><span class="sxs-lookup"><span data-stu-id="65463-110">New Features</span></span>

* <span data-ttu-id="65463-111">Klienti NuGet nyní podporují gzip kódování obsahu z úložiště</span><span class="sxs-lookup"><span data-stu-id="65463-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="65463-112">Podpora pro soubory PDB z balíčků projektů xproj</span><span class="sxs-lookup"><span data-stu-id="65463-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="65463-113">Podpora pro iOS a Android akce v elementu contentFiles sestavení</span><span class="sxs-lookup"><span data-stu-id="65463-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="65463-114">Podpora monikerů netstandard a netstandardapp monikery framework</span><span class="sxs-lookup"><span data-stu-id="65463-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="65463-115">Nové funkce uživatelského rozhraní</span><span class="sxs-lookup"><span data-stu-id="65463-115">New User Interface Features</span></span>

* <span data-ttu-id="65463-116">Významné zlepšení výkonu hlavně na kartách nainstalovaná, aktualizace a konsolidace</span><span class="sxs-lookup"><span data-stu-id="65463-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="65463-117">Je k dispozici s slučování výsledek hledání správné agregovaného zdroje 'všechny zdroje balíčků.</span><span class="sxs-lookup"><span data-stu-id="65463-117">Aggregate 'All Package Sources' Source is available with proper search result merging</span></span>
* <span data-ttu-id="65463-118">Nainstalovaná a aktualizace karty jsou teď řadí abecedně</span><span class="sxs-lookup"><span data-stu-id="65463-118">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="65463-119">Přidat tlačítko Aktualizovat, která umožňuje vyhledávání nutné aktualizovat</span><span class="sxs-lookup"><span data-stu-id="65463-119">Added a Refresh button that allows a search to be refreshed</span></span>
* <span data-ttu-id="65463-120">Nejnovější sestavení možnosti v horní části seznamu verze</span><span class="sxs-lookup"><span data-stu-id="65463-120">Latest Build options at the top of the Version list</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="65463-121">Aktualizace a vylepšení</span><span class="sxs-lookup"><span data-stu-id="65463-121">Updates and Improvements</span></span>

* <span data-ttu-id="65463-122">Balíčky, kterou se odkazuje v `project.json` mají plovoucí verze nebude aktualizovat na každé sestavení.</span><span class="sxs-lookup"><span data-stu-id="65463-122">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="65463-123">Místo toho bude aktualizovat pouze v případě, že vynutit obnovení, vyčistit, znovu sestavit nebo upravit `project.json`.</span><span class="sxs-lookup"><span data-stu-id="65463-123">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="65463-124">nuget.org úložiště zdrojů již nebude, vynuceně přesunuty do konfigurace projektu při použití konfigurace NuGet uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="65463-124">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="65463-125">NuGet už obnoví balíčků ve sdílených projektů ani zapisuje do souboru zámku.</span><span class="sxs-lookup"><span data-stu-id="65463-125">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="65463-126">Jsme jste vylepšené selhání sítě a opakujte zpracování pro nedostupné nebo pomalé na reakce serverů.</span><span class="sxs-lookup"><span data-stu-id="65463-126">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="65463-127">Chování klávesnici a myš jsou vylepšení v uživatelském rozhraní Správce balíčků Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="65463-127">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="65463-128">Teď podporujeme nejnovější `project.json` schéma v DNX.</span><span class="sxs-lookup"><span data-stu-id="65463-128">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="breaking-changes"></a><span data-ttu-id="65463-129">Nejnovější změny</span><span class="sxs-lookup"><span data-stu-id="65463-129">Breaking Changes</span></span>

* <span data-ttu-id="65463-130">Čísla verzí balíčku jsou nyní normalizovány na formát *hlavní*. *méně závažné*. *oprava*-*předprodejní* každé hlavní, malé a opravy se považují za celá čísla a vyřadit všechny úvodní nuly.</span><span class="sxs-lookup"><span data-stu-id="65463-130">Package version numbers are now normalized to the format *major*.*minor*.*patch*-*prerelease*   Each of major, minor, and patch are treated as integers and drop any leading zeroes.</span></span>  <span data-ttu-id="65463-131">Předběžné informace se považuje za řetězec a žádné změny se použijí k němu.</span><span class="sxs-lookup"><span data-stu-id="65463-131">The prerelease information is treated as a string and no changes are applied to it.</span></span> <span data-ttu-id="65463-132">Tato čísla se používají v dotazech klienti NuGet a hledání poskytovaný službou nuget.org.</span><span class="sxs-lookup"><span data-stu-id="65463-132">These numbers are used in queries by the NuGet clients and the search provided by the nuget.org service.</span></span>  <span data-ttu-id="65463-133">Další podrobnosti naleznete v dokumentaci NuGet v rámci [vydanou verzí](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="65463-133">More details can be found in the NuGet Docs under [Prerelease Versions](../create-packages/prerelease-packages.md).</span></span>

## <a name="known-issues"></a><span data-ttu-id="65463-134">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="65463-134">Known Issues</span></span>

* <span data-ttu-id="65463-135">**Problém:** Windows 10 v1511, můžou uživatelé zaznamenat potíže nebo i Visual Studio havárie v prostředí Powershell v sadě Visual Studio v následujících scénářích:</span><span class="sxs-lookup"><span data-stu-id="65463-135">**Issue:** Windows 10 v1511 users may experience issues or even a Visual Studio crash with Powershell in Visual Studio in the following scenarios:</span></span>
    * <span data-ttu-id="65463-136">Instalace / Odinstalace balíčky, které mají install.ps1 / uninstall.ps1 skriptů</span><span class="sxs-lookup"><span data-stu-id="65463-136">Installing / Uninstalling packages that have install.ps1 / uninstall.ps1 scripts</span></span>
    * <span data-ttu-id="65463-137">Načítání projekty, které mají skript Init.ps1, způsobí (např. EntityFramework)</span><span class="sxs-lookup"><span data-stu-id="65463-137">Loading projects that have an init.ps1 script (like EntityFramework)</span></span>
    * <span data-ttu-id="65463-138">Publikování webového obsahu</span><span class="sxs-lookup"><span data-stu-id="65463-138">Publishing web content</span></span>

* <span data-ttu-id="65463-139">**Alternativní řešení:** zajistěte, aby vaše instalace systému Windows 10 nejnovější použitých, expecially leden 2016 (KB 3124263) nebo novější aktualizace.</span><span class="sxs-lookup"><span data-stu-id="65463-139">**Workaround:** Ensure that your Windows 10 install has the latest patches applied, expecially the January 2016 (KB 3124263) or a later update.</span></span>  <span data-ttu-id="65463-140">Další podrobnosti jsou dostupné na [potíže Githubu #1638](http://github.com/nuget/home/issues/1638)</span><span class="sxs-lookup"><span data-stu-id="65463-140">More details are available on [GitHub issue #1638](http://github.com/nuget/home/issues/1638)</span></span>

* <span data-ttu-id="65463-141">**Problém:** Přesměrování protokolu NuGet v2 jsou přerušená.</span><span class="sxs-lookup"><span data-stu-id="65463-141">**Issue:** NuGet v2 protocol redirects are broken.</span></span>
<span data-ttu-id="65463-142">Vlastní úložiště NuGet, které směrují požadavky na alternativního hostitele, nerespektují požadavky přesměrování.</span><span class="sxs-lookup"><span data-stu-id="65463-142">Custom NuGet repositories that redirect requests to an alternative host do not honor the redirect request.</span></span>
* <span data-ttu-id="65463-143">**Alternativní řešení:** tento problém obejít, nakonfigurujte identifikátor URI úložiště balíčků tak, aby odkazoval na přesměrované umístění serveru.</span><span class="sxs-lookup"><span data-stu-id="65463-143">**Workaround:**  To work around this issue, configure the package repository URI in settings to point to the redirected server location.</span></span>
<span data-ttu-id="65463-144">Další informace najdete v tématu [Githubu žádost o přijetí změn #387](https://github.com/NuGet/NuGet.Client/pull/387).</span><span class="sxs-lookup"><span data-stu-id="65463-144">For more information, see [GitHub pull request #387](https://github.com/NuGet/NuGet.Client/pull/387).</span></span>

<span data-ttu-id="65463-145">Abychom mohli pokračovat ke sledování problémů na našich seznamu Githubu problémy, které najdete na: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="65463-145">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>