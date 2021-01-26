---
title: Zpráva k vydání verze NuGet 3,4
description: Poznámky k verzi pro NuGet 3,4, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 794b25e2d81d7a2c297a185bdb34a7cf68535723
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776415"
---
# <a name="nuget-34-release-notes"></a><span data-ttu-id="3ddbe-103">Zpráva k vydání verze NuGet 3,4</span><span class="sxs-lookup"><span data-stu-id="3ddbe-103">NuGet 3.4 Release Notes</span></span>

<span data-ttu-id="3ddbe-104">Poznámky k verzi [pro NuGet 3,4 – RC](../release-notes/nuget-3.4-RC.md)  |  [Poznámky k verzi NuGet 3.4.1](../release-notes/nuget-3.4.1.md)</span><span class="sxs-lookup"><span data-stu-id="3ddbe-104">[NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md)</span></span>

<span data-ttu-id="3ddbe-105">NuGet 3,4 byl vydán 30. března 2016 jako součást verze Visual Studio 2015 Update 2 a Visual Studio 15 Preview a vytvořila se s několika principy v mozky:</span><span class="sxs-lookup"><span data-stu-id="3ddbe-105">NuGet 3.4 was released March 30, 2016 as part of the Visual Studio 2015 Update 2 and Visual Studio 15 Preview Release and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="3ddbe-106">Podpora pro různé platformy</span><span class="sxs-lookup"><span data-stu-id="3ddbe-106">Cross-Platform support</span></span>
* <span data-ttu-id="3ddbe-107">Vylepšení výkonu</span><span class="sxs-lookup"><span data-stu-id="3ddbe-107">Performance improvements</span></span>
* <span data-ttu-id="3ddbe-108">Vylepšení dílčího uživatelského rozhraní</span><span class="sxs-lookup"><span data-stu-id="3ddbe-108">Minor UI improvements</span></span>

<span data-ttu-id="3ddbe-109">Následující funkce byly dříve přidány ve verzi RC a byly aktualizovány nebo dokončeny pro vydání 3,4:</span><span class="sxs-lookup"><span data-stu-id="3ddbe-109">The following features were previously added in the RC and have been updated or completed for the 3.4 release:</span></span>

## <a name="new-features"></a><span data-ttu-id="3ddbe-110">Nové funkce</span><span class="sxs-lookup"><span data-stu-id="3ddbe-110">New Features</span></span>

* <span data-ttu-id="3ddbe-111">Klienti NuGet teď podporují kódování obsahu gzip z úložišť.</span><span class="sxs-lookup"><span data-stu-id="3ddbe-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="3ddbe-112">Podpora soubory PDB z balíčků v projektech xproj</span><span class="sxs-lookup"><span data-stu-id="3ddbe-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="3ddbe-113">Podpora pro akce sestavení pro iOS a Android v elementu contentFiles</span><span class="sxs-lookup"><span data-stu-id="3ddbe-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="3ddbe-114">Podpora pro monikery rozhraní netstandard a netstandardapp</span><span class="sxs-lookup"><span data-stu-id="3ddbe-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="3ddbe-115">Nové funkce uživatelského rozhraní</span><span class="sxs-lookup"><span data-stu-id="3ddbe-115">New User Interface Features</span></span>

* <span data-ttu-id="3ddbe-116">Významná vylepšení výkonu, zejména na kartách nainstalované, aktualizace a konsolidace</span><span class="sxs-lookup"><span data-stu-id="3ddbe-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="3ddbe-117">Zdroj všech zdrojů balíčků je k dispozici v rámci správného sloučení výsledků hledání.</span><span class="sxs-lookup"><span data-stu-id="3ddbe-117">Aggregate 'All Package Sources' Source is available with proper search result merging</span></span>
* <span data-ttu-id="3ddbe-118">Nainstalované a aktualizované karty jsou nyní seřazené abecedně.</span><span class="sxs-lookup"><span data-stu-id="3ddbe-118">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="3ddbe-119">Přidání tlačítka aktualizovat, které umožňuje aktualizovat hledání</span><span class="sxs-lookup"><span data-stu-id="3ddbe-119">Added a Refresh button that allows a search to be refreshed</span></span>
* <span data-ttu-id="3ddbe-120">Nejnovější možnosti sestavení v horní části seznamu verzí</span><span class="sxs-lookup"><span data-stu-id="3ddbe-120">Latest Build options at the top of the Version list</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="3ddbe-121">Aktualizace a vylepšení</span><span class="sxs-lookup"><span data-stu-id="3ddbe-121">Updates and Improvements</span></span>

* <span data-ttu-id="3ddbe-122">Balíčky, na které se odkazuje v `project.json` plovoucí verzi, se v každém sestavení neaktualizují.</span><span class="sxs-lookup"><span data-stu-id="3ddbe-122">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="3ddbe-123">Místo toho se aktualizují pouze v případě, že je vynuceno obnovení, vyčištění, opětovné sestavení nebo změna `project.json` .</span><span class="sxs-lookup"><span data-stu-id="3ddbe-123">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="3ddbe-124">zdroje úložiště nuget.org již nejsou vynuceny do konfigurace projektu, když použijete uživatelské rozhraní konfigurace NuGet.</span><span class="sxs-lookup"><span data-stu-id="3ddbe-124">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="3ddbe-125">NuGet už neobnovuje balíčky ve sdílených projektech ani nezapisuje soubor zámku.</span><span class="sxs-lookup"><span data-stu-id="3ddbe-125">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="3ddbe-126">Vylepšili jsme selhání sítě a zpracování opakování pro nedosažitelné nebo pomalé servery.</span><span class="sxs-lookup"><span data-stu-id="3ddbe-126">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="3ddbe-127">Vylepšení chování klávesnice a myši jsou vylepšena v uživatelském rozhraní Správce balíčků sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3ddbe-127">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="3ddbe-128">Nyní podporujeme nejnovější `project.json` schéma v DNX.</span><span class="sxs-lookup"><span data-stu-id="3ddbe-128">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="breaking-changes"></a><span data-ttu-id="3ddbe-129">Zásadní změny</span><span class="sxs-lookup"><span data-stu-id="3ddbe-129">Breaking Changes</span></span>

* <span data-ttu-id="3ddbe-130">Čísla verzí balíčků jsou nyní normalizována na formát *Hlavní*. *vedlejší*. *Oprava* - *Předběžná verze*   Každá z hlavních, vedlejších a oprav je považována za celá čísla a vynechá úvodní nuly.</span><span class="sxs-lookup"><span data-stu-id="3ddbe-130">Package version numbers are now normalized to the format *major*.*minor*.*patch*-*prerelease*   Each of major, minor, and patch are treated as integers and drop any leading zeroes.</span></span>  <span data-ttu-id="3ddbe-131">Předprodejní informace se považují za řetězec a na ni se nevztahují žádné změny.</span><span class="sxs-lookup"><span data-stu-id="3ddbe-131">The prerelease information is treated as a string and no changes are applied to it.</span></span> <span data-ttu-id="3ddbe-132">Tato čísla se používají v dotazech klientů NuGet a hledání poskytované službou nuget.org.</span><span class="sxs-lookup"><span data-stu-id="3ddbe-132">These numbers are used in queries by the NuGet clients and the search provided by the nuget.org service.</span></span>  <span data-ttu-id="3ddbe-133">Další podrobnosti najdete v dokumentaci NuGet v části [předprodejní verze](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="3ddbe-133">More details can be found in the NuGet Docs under [Prerelease Versions](../create-packages/prerelease-packages.md).</span></span>

## <a name="known-issues"></a><span data-ttu-id="3ddbe-134">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="3ddbe-134">Known Issues</span></span>

* <span data-ttu-id="3ddbe-135">**Problém:** Uživatelé v1511 s Windows 10 můžou zaznamenat problémy nebo dokonce chybu sady Visual Studio s prostředím PowerShell v aplikaci Visual Studio v následujících scénářích:</span><span class="sxs-lookup"><span data-stu-id="3ddbe-135">**Issue:** Windows 10 v1511 users may experience issues or even a Visual Studio crash with Powershell in Visual Studio in the following scenarios:</span></span>
    * <span data-ttu-id="3ddbe-136">Instalace/odinstalace balíčků, které mají skripty install.ps1/uninstall.ps1</span><span class="sxs-lookup"><span data-stu-id="3ddbe-136">Installing / Uninstalling packages that have install.ps1 / uninstall.ps1 scripts</span></span>
    * <span data-ttu-id="3ddbe-137">Načítání projektů, které mají skript init.ps1 (například EntityFramework)</span><span class="sxs-lookup"><span data-stu-id="3ddbe-137">Loading projects that have an init.ps1 script (like EntityFramework)</span></span>
    * <span data-ttu-id="3ddbe-138">Publikování webového obsahu</span><span class="sxs-lookup"><span data-stu-id="3ddbe-138">Publishing web content</span></span>

* <span data-ttu-id="3ddbe-139">**Alternativní řešení:** Ujistěte se, že instalace Windows 10 má nejnovější použité opravy, expecially 2016. ledna (KB 3124263) nebo novější aktualizace.</span><span class="sxs-lookup"><span data-stu-id="3ddbe-139">**Workaround:** Ensure that your Windows 10 install has the latest patches applied, expecially the January 2016 (KB 3124263) or a later update.</span></span>  <span data-ttu-id="3ddbe-140">Další podrobnosti jsou k dispozici v [problému na githubu #1638](http://github.com/nuget/home/issues/1638)</span><span class="sxs-lookup"><span data-stu-id="3ddbe-140">More details are available on [GitHub issue #1638](http://github.com/nuget/home/issues/1638)</span></span>

* <span data-ttu-id="3ddbe-141">**Problém:** Přesměrování protokolu NuGet v2 jsou přerušená.</span><span class="sxs-lookup"><span data-stu-id="3ddbe-141">**Issue:** NuGet v2 protocol redirects are broken.</span></span>
<span data-ttu-id="3ddbe-142">Vlastní úložiště NuGet, které směrují požadavky na alternativního hostitele, nerespektují požadavky přesměrování.</span><span class="sxs-lookup"><span data-stu-id="3ddbe-142">Custom NuGet repositories that redirect requests to an alternative host do not honor the redirect request.</span></span>
* <span data-ttu-id="3ddbe-143">**Alternativní řešení:**  Pokud chcete tento problém obejít, nakonfigurujte identifikátor URI úložiště balíčků v nastavení tak, aby odkazoval na přesměrované umístění serveru.</span><span class="sxs-lookup"><span data-stu-id="3ddbe-143">**Workaround:**  To work around this issue, configure the package repository URI in settings to point to the redirected server location.</span></span>
<span data-ttu-id="3ddbe-144">Další informace najdete v tématu [žádosti o přijetí změn githubu #387](https://github.com/NuGet/NuGet.Client/pull/387).</span><span class="sxs-lookup"><span data-stu-id="3ddbe-144">For more information, see [GitHub pull request #387](https://github.com/NuGet/NuGet.Client/pull/387).</span></span>

<span data-ttu-id="3ddbe-145">Pořád sledujeme problémy v našem seznamu problémů GitHubu, které najdete na adrese: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="3ddbe-145">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>