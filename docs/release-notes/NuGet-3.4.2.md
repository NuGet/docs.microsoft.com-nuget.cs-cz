---
title: Poznámky k verzi NuGet 3.4.2
description: Poznámky k verzi pro NuGet 3.4.2, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6e6aa174582d059faa5bef9469cd83b19da51cf3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780257"
---
# <a name="nuget-342-release-notes"></a><span data-ttu-id="5eb77-103">Poznámky k verzi NuGet 3.4.2</span><span class="sxs-lookup"><span data-stu-id="5eb77-103">NuGet 3.4.2 Release Notes</span></span>

<span data-ttu-id="5eb77-104">Poznámky k verzi [NuGet 3.4.1](../release-notes/nuget-3.4.1.md)  |  [Poznámky k verzi NuGet 3.4.3](../release-notes/nuget-3.4.3.md)</span><span class="sxs-lookup"><span data-stu-id="5eb77-104">[NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md)</span></span>

<span data-ttu-id="5eb77-105">3.4.2 NuGet byl vydaný 8. dubna 2016, který řeší několik problémů, které byly zjištěny ve verzi 3,4 a 3.4.1.</span><span class="sxs-lookup"><span data-stu-id="5eb77-105">NuGet 3.4.2 was released on April 8, 2016 to address several issues that were identified in the 3.4 and 3.4.1 release.</span></span>

## <a name="nugetexe-342-rc-is-now-available"></a><span data-ttu-id="5eb77-106">nuget.exe 3.4.2 RC je teď k dispozici</span><span class="sxs-lookup"><span data-stu-id="5eb77-106">nuget.exe 3.4.2 RC is now available</span></span>

<span data-ttu-id="5eb77-107">Release Candidate nuget.exe 3.4.2 si můžete stáhnout [tady](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="5eb77-107">You can download the release candidate of nuget.exe 3.4.2 [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="5eb77-108">Aktualizace a vylepšení</span><span class="sxs-lookup"><span data-stu-id="5eb77-108">Updates and Improvements</span></span>

* <span data-ttu-id="5eb77-109">Výrazně jsme vylepšili výkon aktualizací v konkrétním scénáři, kdy aktualizace balíčků s grafy s hloubkou závislostí trvaly hodně času a reagují na Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5eb77-109">We have significantly improved the performance of updates in a specific scenario, where updates on packages with deep dependency graphs took a really long time and hung Visual Studio.</span></span>
* <span data-ttu-id="5eb77-110">obnovení NuGet bez síťového provozu je 2,5 × – 3x rychlejší v rámci sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5eb77-110">nuget restore without network traffic is 2.5x – 3x faster within Visual Studio.</span></span>
* <span data-ttu-id="5eb77-111">Kromě této změny jsme vyřešili problém, kdy jsme při načítání počtu aktualizací v uživatelském rozhraní VS používali síť dvakrát.</span><span class="sxs-lookup"><span data-stu-id="5eb77-111">In addition to this change, we have fixed an issue where we were hitting the network twice when fetching the update count in the VS UI.</span></span> <span data-ttu-id="5eb77-112">Toto bylo částečně zodpovědné za určitý časový limit pro zákazníky, kteří se setkali v 3.4/3.4.1.</span><span class="sxs-lookup"><span data-stu-id="5eb77-112">This was partially responsible for some timeout issues customers experienced in 3.4/3.4.1.</span></span>
* <span data-ttu-id="5eb77-113">Přidání podpory pro no_proxy nastavení</span><span class="sxs-lookup"><span data-stu-id="5eb77-113">Added support for no_proxy setting</span></span>

## <a name="fixes"></a><span data-ttu-id="5eb77-114">Opravy</span><span class="sxs-lookup"><span data-stu-id="5eb77-114">Fixes</span></span>

* <span data-ttu-id="5eb77-115">Opravili jsme problém, kdy v nastaveních NuGet nebo v konfiguraci 3.4.1 chybí zdroj nuget.org po aktualizaci na.</span><span class="sxs-lookup"><span data-stu-id="5eb77-115">Fixed an issue where nuget.org source was missing in NuGet settings or config after updating to 3.4.1.</span></span>
* <span data-ttu-id="5eb77-116">Opravili jsme problém, kdy se velká a malá písmena mění na FindPackagesById v 3.4.1 Breaks Artifactory.</span><span class="sxs-lookup"><span data-stu-id="5eb77-116">Fixed an issue where a casing change to FindPackagesById in 3.4.1 breaks Artifactory.</span></span>
* <span data-ttu-id="5eb77-117">Byl opraven problém se standardem FIPS, který způsobil selhání při obnovení NuGet s nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="5eb77-117">Corrected an issue with FIPS that caused failures with NuGet restore with nuget.exe.</span></span>
* <span data-ttu-id="5eb77-118">Při procházení zdrojů s neplatnou adresou URL ikony došlo k chybě.</span><span class="sxs-lookup"><span data-stu-id="5eb77-118">Fixed a crash when browsing sources with invalid icon URL.</span></span>
* <span data-ttu-id="5eb77-119">Opravili jsme problémy se sloučením verzí a záznamů ze všech zdrojů.</span><span class="sxs-lookup"><span data-stu-id="5eb77-119">Fixed issues with merging versions and entries from 'All Sources'.</span></span>

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a><span data-ttu-id="5eb77-120">Známé problémy v příkazovém řádku 3.4.2 Windows x86 (RC)</span><span class="sxs-lookup"><span data-stu-id="5eb77-120">Known Issues in 3.4.2 Windows x86 Commandline (RC)</span></span>

<span data-ttu-id="5eb77-121">Tyto problémy budou v brzkém příštím týdnu opraveny, než zahájíme RTM.</span><span class="sxs-lookup"><span data-stu-id="5eb77-121">These issues will be fixed early next week before we hit RTM.</span></span>

*  <span data-ttu-id="5eb77-122">Pokud je soubor řešení umístěný v nižší hierarchii složky než soubory projektu, spuštění obnovení NuGet na řešení se nezdaří.</span><span class="sxs-lookup"><span data-stu-id="5eb77-122">Running nuget restore on a solution will fail if the solution file is placed in a lower folder hierarchy than the project files.</span></span>
*  <span data-ttu-id="5eb77-123">Spuštění příkazu NuGet DELETE na balíčku pomocí informačního kanálu v2 se nezdaří.</span><span class="sxs-lookup"><span data-stu-id="5eb77-123">Running nuget delete command on a package using the V2 feed will fail.</span></span> <span data-ttu-id="5eb77-124">Místo toho použijte informační kanál v3.</span><span class="sxs-lookup"><span data-stu-id="5eb77-124">Use V3 feed instead.</span></span>


<span data-ttu-id="5eb77-125">Úplný seznam oprav a vylepšení v této [verzi najdete v seznamu problémů.](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+)</span><span class="sxs-lookup"><span data-stu-id="5eb77-125">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span></span>