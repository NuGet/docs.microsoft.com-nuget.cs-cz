---
title: Poznámky k verzi NuGet 3.2.1
description: Poznámky k verzi pro NuGet 3.2.1 včetně – známé problémy, opravy chyb, přidaných funkcí a chcete.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 039fabaaacfdffd76fa88ff8183548e97cd4719b
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-321-release-notes"></a><span data-ttu-id="a26d9-103">Poznámky k verzi NuGet 3.2.1</span><span class="sxs-lookup"><span data-stu-id="a26d9-103">NuGet 3.2.1 Release Notes</span></span>

<span data-ttu-id="a26d9-104">[Poznámky k verzi NuGet 3.2](../release-notes/nuget-3.2.md) | [NuGet 3.3 poznámky k verzi](../release-notes/nuget-3.3.md)</span><span class="sxs-lookup"><span data-stu-id="a26d9-104">[NuGet 3.2 Release Notes](../release-notes/nuget-3.2.md) | [NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md)</span></span>

<span data-ttu-id="a26d9-105">3.2.1 NuGet pro příkazového řádku byla vydána 12. října 2015 s několik optimalizací a opravy pro verzi 3.2 a je dostupné v [dist.nuget.org](http://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="a26d9-105">NuGet 3.2.1 for the command-line was released October 12, 2015 with a handful of optimizations and fixes for the 3.2 release and is available from [dist.nuget.org](http://dist.nuget.org/index.html).</span></span>

## <a name="improvements"></a><span data-ttu-id="a26d9-106">Vylepšení</span><span class="sxs-lookup"><span data-stu-id="a26d9-106">Improvements</span></span>

* <span data-ttu-id="a26d9-107">NuGet teď používá konfigurační soubor s původní malá a velká písmena `NuGet.Config`.</span><span class="sxs-lookup"><span data-stu-id="a26d9-107">NuGet now uses the configuration file with the original casing of `NuGet.Config`.</span></span>  <span data-ttu-id="a26d9-108">To je důležité malá a velká písmena v operačních systémech [1427](https://github.com/NuGet/Home/issues/1427)</span><span class="sxs-lookup"><span data-stu-id="a26d9-108">This is important on case-sensitive operating systems [1427](https://github.com/NuGet/Home/issues/1427)</span></span>
* <span data-ttu-id="a26d9-109">Obnovení NuGet teď bude ignorovat projektů dnx (`*.xproj`), měla by být zpracována s `dnu` [. 1227](https://github.com/NuGet/Home/issues/1227)</span><span class="sxs-lookup"><span data-stu-id="a26d9-109">NuGet restore will now ignore dnx projects (`*.xproj`) that should be processed with `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span></span>
* <span data-ttu-id="a26d9-110">Optimalizované využití sítě při práci s `index.json` a balíčku registrační data [1426](https://github.com/NuGet/Home/issues/1426)</span><span class="sxs-lookup"><span data-stu-id="a26d9-110">Optimized network utilization when working with `index.json` and package registration data [1426](https://github.com/NuGet/Home/issues/1426)</span></span>
* <span data-ttu-id="a26d9-111">Stahování prostředků vylepšené zpracování být robustnější službou v2 [1448](https://github.com/NuGet/Home/issues/1448)</span><span class="sxs-lookup"><span data-stu-id="a26d9-111">Improved resource download handling to be more robust with v2 services [1448](https://github.com/NuGet/Home/issues/1448)</span></span>

## <a name="fixes"></a><span data-ttu-id="a26d9-112">Opravy</span><span class="sxs-lookup"><span data-stu-id="a26d9-112">Fixes</span></span>

* <span data-ttu-id="a26d9-113">Aktualizace NuGet správně aktualizuje `.csproj` / `.vcxproj` odkazy [1483](https://github.com/NuGet/Home/issues/1483)</span><span class="sxs-lookup"><span data-stu-id="a26d9-113">NuGet update correctly updates `.csproj`/`.vcxproj` references [1483](https://github.com/NuGet/Home/issues/1483)</span></span>
* <span data-ttu-id="a26d9-114">Nyní složka místní .nuget brání vytváří při SpecialFolders.UserProfile nejde najít [1531](https://github.com/NuGet/Home/issues/1531)</span><span class="sxs-lookup"><span data-stu-id="a26d9-114">Now preventing a local .nuget folder from being created when a SpecialFolders.UserProfile cannot be located [1531](https://github.com/NuGet/Home/issues/1531)</span></span>
* <span data-ttu-id="a26d9-115">Vylepšené zpracování balíčky v místní mezipaměti, které jsou poškozené během stahování [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span><span class="sxs-lookup"><span data-stu-id="a26d9-115">Improved handling of packages in local cache that are corrupted during download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span></span>

<span data-ttu-id="a26d9-116">Úplný seznam problémů řešit pro rozšíření příkazového řádku a Visual Studio naleznete na webu NuGet GitHub [3.2.1 milník](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span><span class="sxs-lookup"><span data-stu-id="a26d9-116">A complete list of issues addressed for the command-line and Visual Studio extension can be found in the NuGet GitHub [3.2.1 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span></span>

## <a name="known-issues"></a><span data-ttu-id="a26d9-117">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="a26d9-117">Known Issues</span></span>

<span data-ttu-id="a26d9-118">Abychom mohli pokračovat ke sledování problémů na našich seznamu Githubu problémy, které najdete na: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="a26d9-118">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>