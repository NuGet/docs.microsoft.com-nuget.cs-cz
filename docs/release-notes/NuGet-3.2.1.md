---
title: Poznámky k verzi NuGet 3.2.1
description: Poznámky k verzi pro NuGet 3.2.1, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cbbef3517122ceda91cb4b4463fe8be43d204db4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776524"
---
# <a name="nuget-321-release-notes"></a><span data-ttu-id="882fe-103">Poznámky k verzi NuGet 3.2.1</span><span class="sxs-lookup"><span data-stu-id="882fe-103">NuGet 3.2.1 Release Notes</span></span>

<span data-ttu-id="882fe-104">Zpráva k [vydání verze](../release-notes/nuget-3.2.md)  |  NuGet 3,2 Zpráva k [vydání verze NuGet 3,3](../release-notes/nuget-3.3.md)</span><span class="sxs-lookup"><span data-stu-id="882fe-104">[NuGet 3.2 Release Notes](../release-notes/nuget-3.2.md) | [NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md)</span></span>

<span data-ttu-id="882fe-105">Verze NuGet 3.2.1 pro příkazový řádek byla vydána 12. října 2015 s několik optimalizacemi a opravami pro vydání 3,2 a je k dispozici z [DIST.NuGet.org](http://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="882fe-105">NuGet 3.2.1 for the command-line was released October 12, 2015 with a handful of optimizations and fixes for the 3.2 release and is available from [dist.nuget.org](http://dist.nuget.org/index.html).</span></span>

## <a name="improvements"></a><span data-ttu-id="882fe-106">Vylepšen</span><span class="sxs-lookup"><span data-stu-id="882fe-106">Improvements</span></span>

* <span data-ttu-id="882fe-107">NuGet teď používá konfigurační soubor s původními velkými písmeny `NuGet.Config` .</span><span class="sxs-lookup"><span data-stu-id="882fe-107">NuGet now uses the configuration file with the original casing of `NuGet.Config`.</span></span>  <span data-ttu-id="882fe-108">To je důležité pro operační systémy s rozlišováním velkých a malých písmen [1427](https://github.com/NuGet/Home/issues/1427)</span><span class="sxs-lookup"><span data-stu-id="882fe-108">This is important on case-sensitive operating systems [1427](https://github.com/NuGet/Home/issues/1427)</span></span>
* <span data-ttu-id="882fe-109">Obnovení NuGet teď bude ignorovat projekty DNX ( `*.xproj` ), které by se měly zpracovat pomocí `dnu` [1227](https://github.com/NuGet/Home/issues/1227) .</span><span class="sxs-lookup"><span data-stu-id="882fe-109">NuGet restore will now ignore dnx projects (`*.xproj`) that should be processed with `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span></span>
* <span data-ttu-id="882fe-110">Optimalizované využití sítě při práci s `index.json` a registračními daty balíčku [1426](https://github.com/NuGet/Home/issues/1426)</span><span class="sxs-lookup"><span data-stu-id="882fe-110">Optimized network utilization when working with `index.json` and package registration data [1426](https://github.com/NuGet/Home/issues/1426)</span></span>
* <span data-ttu-id="882fe-111">Vylepšené zpracování stahování prostředků pro zajištění větší robustnosti se službou v2 Services [1448](https://github.com/NuGet/Home/issues/1448)</span><span class="sxs-lookup"><span data-stu-id="882fe-111">Improved resource download handling to be more robust with v2 services [1448](https://github.com/NuGet/Home/issues/1448)</span></span>

## <a name="fixes"></a><span data-ttu-id="882fe-112">Opravy</span><span class="sxs-lookup"><span data-stu-id="882fe-112">Fixes</span></span>

* <span data-ttu-id="882fe-113">Aktualizace NuGet – odkazy jsou správné aktualizace `.csproj` / `.vcxproj` [1483](https://github.com/NuGet/Home/issues/1483)</span><span class="sxs-lookup"><span data-stu-id="882fe-113">NuGet update correctly updates `.csproj`/`.vcxproj` references [1483](https://github.com/NuGet/Home/issues/1483)</span></span>
* <span data-ttu-id="882fe-114">Nyní brání vytvoření místní složky. NuGet, když nelze najít SpecialFolders. UserProfile [1531](https://github.com/NuGet/Home/issues/1531)</span><span class="sxs-lookup"><span data-stu-id="882fe-114">Now preventing a local .nuget folder from being created when a SpecialFolders.UserProfile cannot be located [1531](https://github.com/NuGet/Home/issues/1531)</span></span>
* <span data-ttu-id="882fe-115">Vylepšené zpracování balíčků v místní mezipaměti, které jsou během stahování poškozené [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span><span class="sxs-lookup"><span data-stu-id="882fe-115">Improved handling of packages in local cache that are corrupted during download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span></span>

<span data-ttu-id="882fe-116">Úplný seznam problémů řešených pro rozšíření příkazového řádku a sady Visual Studio najdete v [milníku](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed) NuGet GitHubu.</span><span class="sxs-lookup"><span data-stu-id="882fe-116">A complete list of issues addressed for the command-line and Visual Studio extension can be found in the NuGet GitHub [3.2.1 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span></span>

## <a name="known-issues"></a><span data-ttu-id="882fe-117">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="882fe-117">Known Issues</span></span>

<span data-ttu-id="882fe-118">Pořád sledujeme problémy v našem seznamu problémů GitHubu, které najdete na adrese: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="882fe-118">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>