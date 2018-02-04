---
title: "Poznámky k verzi NuGet 3.2.1 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Poznámky k verzi pro NuGet 3.2.1 včetně – známé problémy, opravy chyb, přidaných funkcí a chcete."
keywords: "NuGet 3.2.1 poznámky k verzi, opravy chyb známé problémy, přidat funkce, chcete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7c9c2457c33eb3630f632c98bf0cf96703c3a548
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-321-release-notes"></a><span data-ttu-id="121f5-104">Poznámky k verzi NuGet 3.2.1</span><span class="sxs-lookup"><span data-stu-id="121f5-104">NuGet 3.2.1 Release Notes</span></span>

<span data-ttu-id="121f5-105">[Poznámky k verzi NuGet 3.2](../release-notes/nuget-3.2.md) | [NuGet 3.3 poznámky k verzi](../release-notes/nuget-3.3.md)</span><span class="sxs-lookup"><span data-stu-id="121f5-105">[NuGet 3.2 Release Notes](../release-notes/nuget-3.2.md) | [NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md)</span></span>

<span data-ttu-id="121f5-106">3.2.1 NuGet pro příkazového řádku byla vydána 12. října 2015 s několik optimalizací a opravy pro verzi 3.2 a je dostupné v [dist.nuget.org](http://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="121f5-106">NuGet 3.2.1 for the command-line was released October 12, 2015 with a handful of optimizations and fixes for the 3.2 release and is available from [dist.nuget.org](http://dist.nuget.org/index.html).</span></span>

## <a name="improvements"></a><span data-ttu-id="121f5-107">Vylepšení</span><span class="sxs-lookup"><span data-stu-id="121f5-107">Improvements</span></span>

* <span data-ttu-id="121f5-108">NuGet teď používá konfigurační soubor s původní malá a velká písmena `NuGet.Config`.</span><span class="sxs-lookup"><span data-stu-id="121f5-108">NuGet now uses the configuration file with the original casing of `NuGet.Config`.</span></span>  <span data-ttu-id="121f5-109">To je důležité malá a velká písmena v operačních systémech [1427](https://github.com/NuGet/Home/issues/1427)</span><span class="sxs-lookup"><span data-stu-id="121f5-109">This is important on case-sensitive operating systems [1427](https://github.com/NuGet/Home/issues/1427)</span></span>
* <span data-ttu-id="121f5-110">Obnovení NuGet teď bude ignorovat projektů dnx (`*.xproj`), měla by být zpracována s `dnu` [. 1227](https://github.com/NuGet/Home/issues/1227)</span><span class="sxs-lookup"><span data-stu-id="121f5-110">NuGet restore will now ignore dnx projects (`*.xproj`) that should be processed with `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span></span>
* <span data-ttu-id="121f5-111">Optimalizované využití sítě při práci s `index.json` a balíčku registrační data [1426](https://github.com/NuGet/Home/issues/1426)</span><span class="sxs-lookup"><span data-stu-id="121f5-111">Optimized network utilization when working with `index.json` and package registration data [1426](https://github.com/NuGet/Home/issues/1426)</span></span>
* <span data-ttu-id="121f5-112">Stahování prostředků vylepšené zpracování být robustnější službou v2 [1448](https://github.com/NuGet/Home/issues/1448)</span><span class="sxs-lookup"><span data-stu-id="121f5-112">Improved resource download handling to be more robust with v2 services [1448](https://github.com/NuGet/Home/issues/1448)</span></span>

## <a name="fixes"></a><span data-ttu-id="121f5-113">Opravy</span><span class="sxs-lookup"><span data-stu-id="121f5-113">Fixes</span></span>

* <span data-ttu-id="121f5-114">Aktualizace NuGet správně aktualizuje `.csproj` / `.vcxproj` odkazy [1483](https://github.com/NuGet/Home/issues/1483)</span><span class="sxs-lookup"><span data-stu-id="121f5-114">NuGet update correctly updates `.csproj`/`.vcxproj` references [1483](https://github.com/NuGet/Home/issues/1483)</span></span>
* <span data-ttu-id="121f5-115">Nyní složka místní .nuget brání vytváří při SpecialFolders.UserProfile nejde najít [1531](https://github.com/NuGet/Home/issues/1531)</span><span class="sxs-lookup"><span data-stu-id="121f5-115">Now preventing a local .nuget folder from being created when a SpecialFolders.UserProfile cannot be located [1531](https://github.com/NuGet/Home/issues/1531)</span></span>
* <span data-ttu-id="121f5-116">Vylepšené zpracování balíčky v místní mezipaměti, které jsou poškozené během stahování [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span><span class="sxs-lookup"><span data-stu-id="121f5-116">Improved handling of packages in local cache that are corrupted during download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span></span>

<span data-ttu-id="121f5-117">Úplný seznam problémů řešit pro rozšíření příkazového řádku a Visual Studio naleznete na webu NuGet GitHub [3.2.1 milník](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span><span class="sxs-lookup"><span data-stu-id="121f5-117">A complete list of issues addressed for the command-line and Visual Studio extension can be found in the NuGet GitHub [3.2.1 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span></span>

## <a name="known-issues"></a><span data-ttu-id="121f5-118">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="121f5-118">Known Issues</span></span>

<span data-ttu-id="121f5-119">Abychom mohli pokračovat ke sledování problémů na našich seznamu problémy Githubu, které naleznete na adrese: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="121f5-119">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>