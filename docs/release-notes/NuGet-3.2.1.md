---
title: Poznámky k verzi NuGet 3.2.1
description: Zpráva k vydání verze pro NuGet 3.2.1 včetně – známé problémy, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e5ddbb8aa52ef85c823404364a3aca79fd16f3b1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548187"
---
# <a name="nuget-321-release-notes"></a><span data-ttu-id="942c0-103">Poznámky k verzi NuGet 3.2.1</span><span class="sxs-lookup"><span data-stu-id="942c0-103">NuGet 3.2.1 Release Notes</span></span>

<span data-ttu-id="942c0-104">[Zpráva k vydání verze NuGet 3.2](../release-notes/nuget-3.2.md) | [poznámkách k verzi NuGet 3.3](../release-notes/nuget-3.3.md)</span><span class="sxs-lookup"><span data-stu-id="942c0-104">[NuGet 3.2 Release Notes](../release-notes/nuget-3.2.md) | [NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md)</span></span>

<span data-ttu-id="942c0-105">Bylo vydáno 12. října 2015 se sadou několik optimalizací a oprav pro 3.2 verzi NuGet 3.2.1 pro příkazový řádek a je k dispozici [dist.nuget.org](http://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="942c0-105">NuGet 3.2.1 for the command-line was released October 12, 2015 with a handful of optimizations and fixes for the 3.2 release and is available from [dist.nuget.org](http://dist.nuget.org/index.html).</span></span>

## <a name="improvements"></a><span data-ttu-id="942c0-106">Vylepšení</span><span class="sxs-lookup"><span data-stu-id="942c0-106">Improvements</span></span>

* <span data-ttu-id="942c0-107">NuGet teď používá konfigurační soubor s původní použití malých a velkých `NuGet.Config`.</span><span class="sxs-lookup"><span data-stu-id="942c0-107">NuGet now uses the configuration file with the original casing of `NuGet.Config`.</span></span>  <span data-ttu-id="942c0-108">To je důležité malá a velká písmena v operačních systémech [1427](https://github.com/NuGet/Home/issues/1427)</span><span class="sxs-lookup"><span data-stu-id="942c0-108">This is important on case-sensitive operating systems [1427](https://github.com/NuGet/Home/issues/1427)</span></span>
* <span data-ttu-id="942c0-109">Obnovení NuGet teď bude ignorovat projekty dnx (`*.xproj`), který by se měly zpracovat s `dnu` [. 1227](https://github.com/NuGet/Home/issues/1227)</span><span class="sxs-lookup"><span data-stu-id="942c0-109">NuGet restore will now ignore dnx projects (`*.xproj`) that should be processed with `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span></span>
* <span data-ttu-id="942c0-110">Optimalizované využití sítě při práci s `index.json` a balíček registrační data [1426](https://github.com/NuGet/Home/issues/1426)</span><span class="sxs-lookup"><span data-stu-id="942c0-110">Optimized network utilization when working with `index.json` and package registration data [1426](https://github.com/NuGet/Home/issues/1426)</span></span>
* <span data-ttu-id="942c0-111">Stažení vylepšené prostředku zpracování být robustnější službami v2 [1448](https://github.com/NuGet/Home/issues/1448)</span><span class="sxs-lookup"><span data-stu-id="942c0-111">Improved resource download handling to be more robust with v2 services [1448](https://github.com/NuGet/Home/issues/1448)</span></span>

## <a name="fixes"></a><span data-ttu-id="942c0-112">Opravy</span><span class="sxs-lookup"><span data-stu-id="942c0-112">Fixes</span></span>

* <span data-ttu-id="942c0-113">NuGet správně aktualizace `.csproj` / `.vcxproj` odkazy [1483](https://github.com/NuGet/Home/issues/1483)</span><span class="sxs-lookup"><span data-stu-id="942c0-113">NuGet update correctly updates `.csproj`/`.vcxproj` references [1483](https://github.com/NuGet/Home/issues/1483)</span></span>
* <span data-ttu-id="942c0-114">Nyní složka .nuget místní brání vytváří při SpecialFolders.UserProfile nejde najít [1531](https://github.com/NuGet/Home/issues/1531)</span><span class="sxs-lookup"><span data-stu-id="942c0-114">Now preventing a local .nuget folder from being created when a SpecialFolders.UserProfile cannot be located [1531](https://github.com/NuGet/Home/issues/1531)</span></span>
* <span data-ttu-id="942c0-115">Vylepšené zpracování balíčky v místní mezipaměti, které jsou poškozeny během stahování [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span><span class="sxs-lookup"><span data-stu-id="942c0-115">Improved handling of packages in local cache that are corrupted during download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span></span>

<span data-ttu-id="942c0-116">Úplný seznam všech problémech, které řeší pro rozšíření příkazového řádku a Visual Studio najdete na webu NuGet GitHub [3.2.1 milník](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span><span class="sxs-lookup"><span data-stu-id="942c0-116">A complete list of issues addressed for the command-line and Visual Studio extension can be found in the NuGet GitHub [3.2.1 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span></span>

## <a name="known-issues"></a><span data-ttu-id="942c0-117">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="942c0-117">Known Issues</span></span>

<span data-ttu-id="942c0-118">Pokračujeme v sledování problémů v našem seznamu problémů na Githubu najdete je na: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="942c0-118">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>