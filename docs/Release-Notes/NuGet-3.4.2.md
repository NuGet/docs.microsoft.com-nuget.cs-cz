---
title: "Poznámky k verzi NuGet 3.4.2 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Poznámky k verzi pro NuGet 3.4.2 včetně – známé problémy, opravy chyb, přidaných funkcí a chcete."
keywords: "NuGet 3.4.2 poznámky k verzi, opravy chyb známé problémy, přidat funkce, chcete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 892a965e67762af2ae42c2d6ee75d2838104d1c2
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-342-release-notes"></a><span data-ttu-id="b2808-104">Poznámky k verzi NuGet 3.4.2</span><span class="sxs-lookup"><span data-stu-id="b2808-104">NuGet 3.4.2 Release Notes</span></span>

<span data-ttu-id="b2808-105">[Poznámky k verzi NuGet 3.4.1](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 poznámky k verzi](../release-notes/nuget-3.4.3.md)</span><span class="sxs-lookup"><span data-stu-id="b2808-105">[NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md)</span></span>

<span data-ttu-id="b2808-106">NuGet 3.4.2 byla vydána 8. dubna 2016 několik problémů, které byly identifikovány 3.4 a 3.4.1 verzi.</span><span class="sxs-lookup"><span data-stu-id="b2808-106">NuGet 3.4.2 was released on April 8, 2016 to address several issues that were identified in the 3.4 and 3.4.1 release.</span></span>

## <a name="nugetexe-342-rc-is-now-available"></a><span data-ttu-id="b2808-107">nuget.exe 3.4.2 RC je nyní k dispozici</span><span class="sxs-lookup"><span data-stu-id="b2808-107">nuget.exe 3.4.2 RC is now available</span></span>

<span data-ttu-id="b2808-108">Si můžete stáhnout na verzi release candidate z nuget.exe 3.4.2 [zde](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="b2808-108">You can download the release candidate of nuget.exe 3.4.2 [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="b2808-109">Aktualizace a vylepšení</span><span class="sxs-lookup"><span data-stu-id="b2808-109">Updates and Improvements</span></span>

* <span data-ttu-id="b2808-110">Významně jsme vylepšili výkon aktualizace v konkrétní scénář, kde aktualizace na balíčky s grafy hloubkové závislostí trvalo skutečně dlouhou dobu a přestala Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b2808-110">We have significantly improved the performance of updates in a specific scenario, where updates on packages with deep dependency graphs took a really long time and hung Visual Studio.</span></span>
* <span data-ttu-id="b2808-111">nuget restore bez síťový provoz je 2,5 x – 3 x rychlejší v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b2808-111">nuget restore without network traffic is 2.5x – 3x faster within Visual Studio.</span></span>
* <span data-ttu-id="b2808-112">Kromě tuto změnu vyřešili jsme problém kde jsme byly dvakrát při načítání aktualizace počet v uživatelském rozhraní VS stiskne sítě.</span><span class="sxs-lookup"><span data-stu-id="b2808-112">In addition to this change, we have fixed an issue where we were hitting the network twice when fetching the update count in the VS UI.</span></span> <span data-ttu-id="b2808-113">To je částečně zodpovědná za někteří zákazníci problémy časový limit zkušenosti s 3.4 nebo 3.4.1.</span><span class="sxs-lookup"><span data-stu-id="b2808-113">This was partially responsible for some timeout issues customers experienced in 3.4/3.4.1.</span></span>
* <span data-ttu-id="b2808-114">Přidaná podpora pro no_proxy nastavení</span><span class="sxs-lookup"><span data-stu-id="b2808-114">Added support for no_proxy setting</span></span>

## <a name="fixes"></a><span data-ttu-id="b2808-115">Opravy</span><span class="sxs-lookup"><span data-stu-id="b2808-115">Fixes</span></span>

* <span data-ttu-id="b2808-116">Kde nuget.org zdroje nebyl nalezen v NuGet nastavení nebo konfigurace po aktualizaci 3.4.1 opraven problém.</span><span class="sxs-lookup"><span data-stu-id="b2808-116">Fixed an issue where nuget.org source was missing in NuGet settings or config after updating to 3.4.1.</span></span>
* <span data-ttu-id="b2808-117">Kde se malá a velká písmena změnu FindPackagesById v 3.4.1 dělí Artifactory opraven problém.</span><span class="sxs-lookup"><span data-stu-id="b2808-117">Fixed an issue where a casing change to FindPackagesById in 3.4.1 breaks Artifactory.</span></span>
* <span data-ttu-id="b2808-118">Opraven problém se standardem FIPS, která způsobila selhání s obnovením NuGet s nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="b2808-118">Corrected an issue with FIPS that caused failures with NuGet restore with nuget.exe.</span></span>
* <span data-ttu-id="b2808-119">Pevné havárie, při procházení zdroje s adresou URL ikona neplatné.</span><span class="sxs-lookup"><span data-stu-id="b2808-119">Fixed a crash when browsing sources with invalid icon URL.</span></span>
* <span data-ttu-id="b2808-120">Opravené problémy s slučování verze a záznamy z 'Všechny zdroje'.</span><span class="sxs-lookup"><span data-stu-id="b2808-120">Fixed issues with merging versions and entries from 'All Sources'.</span></span>

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a><span data-ttu-id="b2808-121">Známé problémy v 3.4.2 příkazového řádku Windows x86 (RC)</span><span class="sxs-lookup"><span data-stu-id="b2808-121">Known Issues in 3.4.2 Windows x86 Commandline (RC)</span></span>

<span data-ttu-id="b2808-122">Tyto problémy budou opraveny časná příští týden před jsme dosáhl RTM.</span><span class="sxs-lookup"><span data-stu-id="b2808-122">These issues will be fixed early next week before we hit RTM.</span></span>

*  <span data-ttu-id="b2808-123">Spuštěné nuget obnovení řešení se nezdaří, pokud soubor řešení je umístěn v hierarchii složek nižší než soubory projektu.</span><span class="sxs-lookup"><span data-stu-id="b2808-123">Running nuget restore on a solution will fail if the solution file is placed in a lower folder hierarchy than the project files.</span></span>
*  <span data-ttu-id="b2808-124">Příkaz delete nuget systémem balíčku pomocí informačního kanálu V2 se nezdaří.</span><span class="sxs-lookup"><span data-stu-id="b2808-124">Running nuget delete command on a package using the V2 feed will fail.</span></span> <span data-ttu-id="b2808-125">Místo toho použijte V3 informačního kanálu.</span><span class="sxs-lookup"><span data-stu-id="b2808-125">Use V3 feed instead.</span></span>


<span data-ttu-id="b2808-126">Úplný seznam oprav a vylepšení v této verzi najdete seznam problémů [zde](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span><span class="sxs-lookup"><span data-stu-id="b2808-126">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span></span>