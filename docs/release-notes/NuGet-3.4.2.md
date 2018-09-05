---
title: Zpráva k vydání verze NuGet 3.4.2
description: Zpráva k vydání verze pro NuGet 3.4.2 včetně – známé problémy, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4c8aa75df822ca5b2f1c4bd274272218f16ad917
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549148"
---
# <a name="nuget-342-release-notes"></a><span data-ttu-id="bddd4-103">Zpráva k vydání verze NuGet 3.4.2</span><span class="sxs-lookup"><span data-stu-id="bddd4-103">NuGet 3.4.2 Release Notes</span></span>

<span data-ttu-id="bddd4-104">[Zpráva k vydání verze NuGet 3.4.1](../release-notes/nuget-3.4.1.md) | [zpráva k vydání verze NuGet 3.4.3](../release-notes/nuget-3.4.3.md)</span><span class="sxs-lookup"><span data-stu-id="bddd4-104">[NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md)</span></span>

<span data-ttu-id="bddd4-105">8. dubna 2016 několik problémů, které jste identifikovali 3.4 a 3.4.1 byla vydána NuGet 3.4.2 release.</span><span class="sxs-lookup"><span data-stu-id="bddd4-105">NuGet 3.4.2 was released on April 8, 2016 to address several issues that were identified in the 3.4 and 3.4.1 release.</span></span>

## <a name="nugetexe-342-rc-is-now-available"></a><span data-ttu-id="bddd4-106">nuget.exe 3.4.2 RC je teď k dispozici</span><span class="sxs-lookup"><span data-stu-id="bddd4-106">nuget.exe 3.4.2 RC is now available</span></span>

<span data-ttu-id="bddd4-107">Můžete si stáhnout verzi Release candidate programu nuget.exe 3.4.2 [tady](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="bddd4-107">You can download the release candidate of nuget.exe 3.4.2 [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="bddd4-108">Aktualizace a vylepšení</span><span class="sxs-lookup"><span data-stu-id="bddd4-108">Updates and Improvements</span></span>

* <span data-ttu-id="bddd4-109">Výrazně jsme vylepšili provádění aktualizací v konkrétní scénář, ve kterém aktualizací na balíčky pomocí grafů závislosti hloubkové trvalo skutečně dlouhou dobu a zablokování sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bddd4-109">We have significantly improved the performance of updates in a specific scenario, where updates on packages with deep dependency graphs took a really long time and hung Visual Studio.</span></span>
* <span data-ttu-id="bddd4-110">obnovení nuget bez síťový provoz je 2,5 × – 3 x rychlejší v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bddd4-110">nuget restore without network traffic is 2.5x – 3x faster within Visual Studio.</span></span>
* <span data-ttu-id="bddd4-111">Kromě této změny jsme vyřešili problém kde jsme byly dvakrát při načítání aktualizace v Uživatelském rozhraní VS počet dosažení sítě.</span><span class="sxs-lookup"><span data-stu-id="bddd4-111">In addition to this change, we have fixed an issue where we were hitting the network twice when fetching the update count in the VS UI.</span></span> <span data-ttu-id="bddd4-112">Toto je částečně odpovědná za časový limit problémy zákazníci, kteří zkušenosti s 3.4/3.4.1.</span><span class="sxs-lookup"><span data-stu-id="bddd4-112">This was partially responsible for some timeout issues customers experienced in 3.4/3.4.1.</span></span>
* <span data-ttu-id="bddd4-113">Přidání podpory pro nastavení no_proxy</span><span class="sxs-lookup"><span data-stu-id="bddd4-113">Added support for no_proxy setting</span></span>

## <a name="fixes"></a><span data-ttu-id="bddd4-114">Opravy</span><span class="sxs-lookup"><span data-stu-id="bddd4-114">Fixes</span></span>

* <span data-ttu-id="bddd4-115">Opravili jsme problém, kdy nuget.org zdroj nebyl nalezen v nastavení NuGet config po aktualizaci verze 3.4.1.</span><span class="sxs-lookup"><span data-stu-id="bddd4-115">Fixed an issue where nuget.org source was missing in NuGet settings or config after updating to 3.4.1.</span></span>
* <span data-ttu-id="bddd4-116">Opravili jsme problém, pokud malá a velká písmena změnu FindPackagesById v 3.4.1 přeruší Artifactory.</span><span class="sxs-lookup"><span data-stu-id="bddd4-116">Fixed an issue where a casing change to FindPackagesById in 3.4.1 breaks Artifactory.</span></span>
* <span data-ttu-id="bddd4-117">Byl opraven problém s FIPS, která způsobovala chyby s obnovení NuGet se nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="bddd4-117">Corrected an issue with FIPS that caused failures with NuGet restore with nuget.exe.</span></span>
* <span data-ttu-id="bddd4-118">Oprava chyby při procházení zdroje se neplatná ikona adresy URL.</span><span class="sxs-lookup"><span data-stu-id="bddd4-118">Fixed a crash when browsing sources with invalid icon URL.</span></span>
* <span data-ttu-id="bddd4-119">Opravené problémy s sloučení verze a položky z "Všechny zdroje".</span><span class="sxs-lookup"><span data-stu-id="bddd4-119">Fixed issues with merging versions and entries from 'All Sources'.</span></span>

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a><span data-ttu-id="bddd4-120">Známé problémy v 3.4.2 příkazového řádku Windows x86 (RC)</span><span class="sxs-lookup"><span data-stu-id="bddd4-120">Known Issues in 3.4.2 Windows x86 Commandline (RC)</span></span>

<span data-ttu-id="bddd4-121">Tyto problémy budou vyřešeny předčasné příští týden před nedosáhne RTM.</span><span class="sxs-lookup"><span data-stu-id="bddd4-121">These issues will be fixed early next week before we hit RTM.</span></span>

*  <span data-ttu-id="bddd4-122">Spuštění obnovení nuget v řešení se nezdaří, pokud v hierarchii složek nižší než soubory projektu je umístěn soubor řešení.</span><span class="sxs-lookup"><span data-stu-id="bddd4-122">Running nuget restore on a solution will fail if the solution file is placed in a lower folder hierarchy than the project files.</span></span>
*  <span data-ttu-id="bddd4-123">Spuštění příkazu delete nuget na balíčku pomocí kanálu V2 se nezdaří.</span><span class="sxs-lookup"><span data-stu-id="bddd4-123">Running nuget delete command on a package using the V2 feed will fail.</span></span> <span data-ttu-id="bddd4-124">Místo toho použijte V3 informačního kanálu.</span><span class="sxs-lookup"><span data-stu-id="bddd4-124">Use V3 feed instead.</span></span>


<span data-ttu-id="bddd4-125">Pro úplný seznam oprav chyb a vylepšení v této verzi, projděte si seznam problémů [tady](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span><span class="sxs-lookup"><span data-stu-id="bddd4-125">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span></span>