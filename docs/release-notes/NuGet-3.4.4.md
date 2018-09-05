---
title: Zpráva k vydání verze NuGet 3.4.4
description: Zpráva k vydání verze pro NuGet 3.4.4 včetně – známé problémy, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 44a9f21c61f0552fdc21aab24f48eee993654b01
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547470"
---
# <a name="nuget-344-release-notes"></a><span data-ttu-id="93352-103">Zpráva k vydání verze NuGet 3.4.4</span><span class="sxs-lookup"><span data-stu-id="93352-103">NuGet 3.4.4 Release Notes</span></span>

<span data-ttu-id="93352-104">[Zpráva k vydání verze NuGet 3.4.3](../release-notes/nuget-3.4.3.md) | [NuGet 3.5 betaverze poznámky](../release-notes/nuget-3.5-Beta.md)</span><span class="sxs-lookup"><span data-stu-id="93352-104">[NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md) | [NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md)</span></span>

<span data-ttu-id="93352-105">Hlavním cílem této verzi byla vylepšení kvality 3.4.3 verze programu nuget.exe pomocí rozšíření sady Visual Studio také několik oprav.</span><span class="sxs-lookup"><span data-stu-id="93352-105">The primary focus of this release was improvements to the quality of 3.4.3 version of nuget.exe with a few fixes to the Visual Studio extension as well.</span></span>

<span data-ttu-id="93352-106">Si můžete stáhnout VSIX i nuget.exe [tady](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="93352-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a><span data-ttu-id="93352-107">[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span><span class="sxs-lookup"><span data-stu-id="93352-107">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span></span>

[<span data-ttu-id="93352-108">Úplný protokol změn</span><span class="sxs-lookup"><span data-stu-id="93352-108">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[<span data-ttu-id="93352-109">Seznam problémů</span><span class="sxs-lookup"><span data-stu-id="93352-109">List of Issues</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a><span data-ttu-id="93352-110">Změny</span><span class="sxs-lookup"><span data-stu-id="93352-110">Changes</span></span>

- <span data-ttu-id="93352-111">Vylepšení aktualizací Service Pack: Vylepšení balení symbolů, balení s `project.json` a další [ \#606](https://github.com/NuGet/NuGet.Client/pull/606)</span><span class="sxs-lookup"><span data-stu-id="93352-111">Pack Improvements: Improvements to packing symbols, packing with `project.json` and more [\#606](https://github.com/NuGet/NuGet.Client/pull/606)</span></span>
- <span data-ttu-id="93352-112">Zobrazit výjimky, když dojde k selhání hledání projekty v příkazu update [\#605](https://github.com/NuGet/NuGet.Client/pull/605)</span><span class="sxs-lookup"><span data-stu-id="93352-112">Display exception when there is a failure finding projects in update command [\#605](https://github.com/NuGet/NuGet.Client/pull/605</span></span>
- <span data-ttu-id="93352-113">Přečíst typ balíčku ze vstupu `.nuspec` a `project.json` při balení [ \#603](https://github.com/NuGet/NuGet.Client/pull/603)</span><span class="sxs-lookup"><span data-stu-id="93352-113">Read package type from input `.nuspec` and `project.json` when packing [\#603](https://github.com/NuGet/NuGet.Client/pull/603)</span></span>
- <span data-ttu-id="93352-114">Ujistěte se, NuGet.Shared ne k projektu.</span><span class="sxs-lookup"><span data-stu-id="93352-114">Make NuGet.Shared not a project.</span></span> [<span data-ttu-id="93352-115">\#602</span><span class="sxs-lookup"><span data-stu-id="93352-115">\#602</span></span>](https://github.com/NuGet/NuGet.Client/pull/602)
- <span data-ttu-id="93352-116">Použít časový limit nabízených oznámení jako vypršení časového limitu odpovědi HTTP [ \#599](https://github.com/NuGet/NuGet.Client/pull/599)</span><span class="sxs-lookup"><span data-stu-id="93352-116">Use the push timeout as the HTTP response timeout [\#599](https://github.com/NuGet/NuGet.Client/pull/599)</span></span>
- <span data-ttu-id="93352-117">Soubory balíčku s budoucích časů nebude mít s úspěšností použít [ \#597](https://github.com/NuGet/NuGet.Client/pull/597)</span><span class="sxs-lookup"><span data-stu-id="93352-117">Package files with future times will not have their times used [\#597](https://github.com/NuGet/NuGet.Client/pull/597)</span></span>
- <span data-ttu-id="93352-118">Aktualizuje se `NuGet.Core.dll` verze, kterou chcete 2.12.0 k vyřešení problému XML [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)</span><span class="sxs-lookup"><span data-stu-id="93352-118">Updating `NuGet.Core.dll` version to 2.12.0 to fix XML issue [\#594](https://github.com/NuGet/NuGet.Client/pull/594)</span></span>
- <span data-ttu-id="93352-119">Podpora./NuGet.CommandLine.XPlat - v \<podrobností\> \<režimu\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)</span><span class="sxs-lookup"><span data-stu-id="93352-119">Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)</span></span>
- <span data-ttu-id="93352-120">Zobrazení chyby obnovení bez `project.json` nebo `packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)</span><span class="sxs-lookup"><span data-stu-id="93352-120">Display error restoring without `project.json` or `packages.config` [\#590](https://github.com/NuGet/NuGet.Client/pull/590)</span></span>
- <span data-ttu-id="93352-121">Stanovení verzí závislosti při požadované verze se liší [ \#559](https://github.com/NuGet/NuGet.Client/pull/559)</span><span class="sxs-lookup"><span data-stu-id="93352-121">Fixing dependency versions when required versions differ [\#559](https://github.com/NuGet/NuGet.Client/pull/559)</span></span>