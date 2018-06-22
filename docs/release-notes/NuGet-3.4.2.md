---
title: Poznámky k verzi NuGet 3.4.2
description: Poznámky k verzi pro NuGet 3.4.2 včetně – známé problémy, opravy chyb, přidaných funkcí a chcete.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 88d29a84e280433663ab6c1c04ae16e1329420f7
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819663"
---
# <a name="nuget-342-release-notes"></a><span data-ttu-id="af502-103">Poznámky k verzi NuGet 3.4.2</span><span class="sxs-lookup"><span data-stu-id="af502-103">NuGet 3.4.2 Release Notes</span></span>

<span data-ttu-id="af502-104">[Poznámky k verzi NuGet 3.4.1](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 poznámky k verzi](../release-notes/nuget-3.4.3.md)</span><span class="sxs-lookup"><span data-stu-id="af502-104">[NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md)</span></span>

<span data-ttu-id="af502-105">NuGet 3.4.2 byla vydána 8. dubna 2016 několik problémů, které byly identifikovány 3.4 a 3.4.1 verzi.</span><span class="sxs-lookup"><span data-stu-id="af502-105">NuGet 3.4.2 was released on April 8, 2016 to address several issues that were identified in the 3.4 and 3.4.1 release.</span></span>

## <a name="nugetexe-342-rc-is-now-available"></a><span data-ttu-id="af502-106">nuget.exe 3.4.2 RC je nyní k dispozici</span><span class="sxs-lookup"><span data-stu-id="af502-106">nuget.exe 3.4.2 RC is now available</span></span>

<span data-ttu-id="af502-107">Si můžete stáhnout na verzi release candidate z nuget.exe 3.4.2 [zde](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="af502-107">You can download the release candidate of nuget.exe 3.4.2 [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="af502-108">Aktualizace a vylepšení</span><span class="sxs-lookup"><span data-stu-id="af502-108">Updates and Improvements</span></span>

* <span data-ttu-id="af502-109">Významně jsme vylepšili výkon aktualizace v konkrétní scénář, kde aktualizace na balíčky s grafy hloubkové závislostí trvalo skutečně dlouhou dobu a přestala Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="af502-109">We have significantly improved the performance of updates in a specific scenario, where updates on packages with deep dependency graphs took a really long time and hung Visual Studio.</span></span>
* <span data-ttu-id="af502-110">nuget restore bez síťový provoz je 2,5 x – 3 x rychlejší v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="af502-110">nuget restore without network traffic is 2.5x – 3x faster within Visual Studio.</span></span>
* <span data-ttu-id="af502-111">Kromě tuto změnu vyřešili jsme problém kde jsme byly dvakrát při načítání aktualizace počet v uživatelském rozhraní VS stiskne sítě.</span><span class="sxs-lookup"><span data-stu-id="af502-111">In addition to this change, we have fixed an issue where we were hitting the network twice when fetching the update count in the VS UI.</span></span> <span data-ttu-id="af502-112">To je částečně zodpovědná za někteří zákazníci problémy časový limit zkušenosti s 3.4 nebo 3.4.1.</span><span class="sxs-lookup"><span data-stu-id="af502-112">This was partially responsible for some timeout issues customers experienced in 3.4/3.4.1.</span></span>
* <span data-ttu-id="af502-113">Přidaná podpora pro no_proxy nastavení</span><span class="sxs-lookup"><span data-stu-id="af502-113">Added support for no_proxy setting</span></span>

## <a name="fixes"></a><span data-ttu-id="af502-114">Opravy</span><span class="sxs-lookup"><span data-stu-id="af502-114">Fixes</span></span>

* <span data-ttu-id="af502-115">Kde nuget.org zdroje nebyl nalezen v NuGet nastavení nebo konfigurace po aktualizaci 3.4.1 opraven problém.</span><span class="sxs-lookup"><span data-stu-id="af502-115">Fixed an issue where nuget.org source was missing in NuGet settings or config after updating to 3.4.1.</span></span>
* <span data-ttu-id="af502-116">Kde se malá a velká písmena změnu FindPackagesById v 3.4.1 dělí Artifactory opraven problém.</span><span class="sxs-lookup"><span data-stu-id="af502-116">Fixed an issue where a casing change to FindPackagesById in 3.4.1 breaks Artifactory.</span></span>
* <span data-ttu-id="af502-117">Opraven problém se standardem FIPS, která způsobila selhání s obnovením NuGet s nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="af502-117">Corrected an issue with FIPS that caused failures with NuGet restore with nuget.exe.</span></span>
* <span data-ttu-id="af502-118">Pevné havárie, při procházení zdroje s adresou URL ikona neplatné.</span><span class="sxs-lookup"><span data-stu-id="af502-118">Fixed a crash when browsing sources with invalid icon URL.</span></span>
* <span data-ttu-id="af502-119">Opravené problémy s slučování verze a záznamy z 'Všechny zdroje'.</span><span class="sxs-lookup"><span data-stu-id="af502-119">Fixed issues with merging versions and entries from 'All Sources'.</span></span>

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a><span data-ttu-id="af502-120">Známé problémy v 3.4.2 příkazového řádku Windows x86 (RC)</span><span class="sxs-lookup"><span data-stu-id="af502-120">Known Issues in 3.4.2 Windows x86 Commandline (RC)</span></span>

<span data-ttu-id="af502-121">Tyto problémy budou opraveny časná příští týden před jsme dosáhl RTM.</span><span class="sxs-lookup"><span data-stu-id="af502-121">These issues will be fixed early next week before we hit RTM.</span></span>

*  <span data-ttu-id="af502-122">Spuštěné nuget obnovení řešení se nezdaří, pokud soubor řešení je umístěn v hierarchii složek nižší než soubory projektu.</span><span class="sxs-lookup"><span data-stu-id="af502-122">Running nuget restore on a solution will fail if the solution file is placed in a lower folder hierarchy than the project files.</span></span>
*  <span data-ttu-id="af502-123">Příkaz delete nuget systémem balíčku pomocí informačního kanálu V2 se nezdaří.</span><span class="sxs-lookup"><span data-stu-id="af502-123">Running nuget delete command on a package using the V2 feed will fail.</span></span> <span data-ttu-id="af502-124">Místo toho použijte V3 informačního kanálu.</span><span class="sxs-lookup"><span data-stu-id="af502-124">Use V3 feed instead.</span></span>


<span data-ttu-id="af502-125">Úplný seznam oprav a vylepšení v této verzi najdete seznam problémů [zde](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span><span class="sxs-lookup"><span data-stu-id="af502-125">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span></span>