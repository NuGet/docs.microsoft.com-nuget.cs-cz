---
title: Poznámky k verzi NuGet 3.4.4
description: Poznámky k verzi pro včetně NuGet 3.4.4 – známé problémy, opravy chyb, přidaných funkcí a chcete.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 891d5c7ee884d31f405118739b57a169b9cd93b3
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-344-release-notes"></a><span data-ttu-id="0db29-103">Poznámky k verzi NuGet 3.4.4</span><span class="sxs-lookup"><span data-stu-id="0db29-103">NuGet 3.4.4 Release Notes</span></span>

<span data-ttu-id="0db29-104">[Poznámky k verzi NuGet 3.4.3](../release-notes/nuget-3.4.3.md) | [poznámky k verzi 3.5 Beta NuGet](../release-notes/nuget-3.5-Beta.md)</span><span class="sxs-lookup"><span data-stu-id="0db29-104">[NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md) | [NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md)</span></span>

<span data-ttu-id="0db29-105">Hlavním cílem této verze byla vylepšení kvality 3.4.3 verzi nuget.exe s několika opravy také rozšíření sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0db29-105">The primary focus of this release was improvements to the quality of 3.4.3 version of nuget.exe with a few fixes to the Visual Studio extension as well.</span></span>

<span data-ttu-id="0db29-106">Si můžete stáhnout VSIX i nuget.exe [zde](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="0db29-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a><span data-ttu-id="0db29-107">[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span><span class="sxs-lookup"><span data-stu-id="0db29-107">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span></span>

[<span data-ttu-id="0db29-108">Úplné protokol změn</span><span class="sxs-lookup"><span data-stu-id="0db29-108">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[<span data-ttu-id="0db29-109">Seznam problémů</span><span class="sxs-lookup"><span data-stu-id="0db29-109">List of Issues</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a><span data-ttu-id="0db29-110">Změny</span><span class="sxs-lookup"><span data-stu-id="0db29-110">Changes</span></span>

- <span data-ttu-id="0db29-111">Vylepšení aktualizací Service Pack: Vylepšení balení symboly, balení s `project.json` a další [ \#606](https://github.com/NuGet/NuGet.Client/pull/606)</span><span class="sxs-lookup"><span data-stu-id="0db29-111">Pack Improvements: Improvements to packing symbols, packing with `project.json` and more [\#606](https://github.com/NuGet/NuGet.Client/pull/606)</span></span>
- <span data-ttu-id="0db29-112">Zobrazit výjimky, když dojde k selhání hledání projekty v příkazu update [\#605] ()https://github.com/NuGet/NuGet.Client/pull/605</span><span class="sxs-lookup"><span data-stu-id="0db29-112">Display exception when there is a failure finding projects in update command [\#605](https://github.com/NuGet/NuGet.Client/pull/605</span></span>
- <span data-ttu-id="0db29-113">Typ balíčku číst ze vstupu `.nuspec` a `project.json` při balení [ \#603](https://github.com/NuGet/NuGet.Client/pull/603)</span><span class="sxs-lookup"><span data-stu-id="0db29-113">Read package type from input `.nuspec` and `project.json` when packing [\#603](https://github.com/NuGet/NuGet.Client/pull/603)</span></span>
- <span data-ttu-id="0db29-114">Zkontrolujte NuGet.Shared není projektu.</span><span class="sxs-lookup"><span data-stu-id="0db29-114">Make NuGet.Shared not a project.</span></span> [<span data-ttu-id="0db29-115">\#602</span><span class="sxs-lookup"><span data-stu-id="0db29-115">\#602</span></span>](https://github.com/NuGet/NuGet.Client/pull/602)
- <span data-ttu-id="0db29-116">Použít nabízenou časový limit jako časový limit odpovědi HTTP [ \#599](https://github.com/NuGet/NuGet.Client/pull/599)</span><span class="sxs-lookup"><span data-stu-id="0db29-116">Use the push timeout as the HTTP response timeout [\#599](https://github.com/NuGet/NuGet.Client/pull/599)</span></span>
- <span data-ttu-id="0db29-117">Soubory balíčků s budoucí časy nebude mít časy jejich použít [ \#597](https://github.com/NuGet/NuGet.Client/pull/597)</span><span class="sxs-lookup"><span data-stu-id="0db29-117">Package files with future times will not have their times used [\#597](https://github.com/NuGet/NuGet.Client/pull/597)</span></span>
- <span data-ttu-id="0db29-118">Aktualizace `NuGet.Core.dll` verzi 2.12.0 opravu problému XML [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)</span><span class="sxs-lookup"><span data-stu-id="0db29-118">Updating `NuGet.Core.dll` version to 2.12.0 to fix XML issue [\#594](https://github.com/NuGet/NuGet.Client/pull/594)</span></span>
- <span data-ttu-id="0db29-119">Podpora./NuGet.CommandLine.XPlat - v \<podrobností\> \<režimu\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)</span><span class="sxs-lookup"><span data-stu-id="0db29-119">Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)</span></span>
- <span data-ttu-id="0db29-120">Zobrazení Chyba při obnově bez `project.json` nebo `packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)</span><span class="sxs-lookup"><span data-stu-id="0db29-120">Display error restoring without `project.json` or `packages.config` [\#590](https://github.com/NuGet/NuGet.Client/pull/590)</span></span>
- <span data-ttu-id="0db29-121">Stanovení závislost verze při požadované verze se liší [ \#559](https://github.com/NuGet/NuGet.Client/pull/559)</span><span class="sxs-lookup"><span data-stu-id="0db29-121">Fixing dependency versions when required versions differ [\#559](https://github.com/NuGet/NuGet.Client/pull/559)</span></span>