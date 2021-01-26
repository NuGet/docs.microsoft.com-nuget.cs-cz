---
title: Poznámky k verzi NuGet 3.4.4
description: Poznámky k verzi pro NuGet 3.4.4, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4e5e635432147afba4809562035bc8c762d31af4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780225"
---
# <a name="nuget-344-release-notes"></a><span data-ttu-id="3aa70-103">Poznámky k verzi NuGet 3.4.4</span><span class="sxs-lookup"><span data-stu-id="3aa70-103">NuGet 3.4.4 Release Notes</span></span>

<span data-ttu-id="3aa70-104">Poznámky k verzi [NuGet 3.4.3](../release-notes/nuget-3.4.3.md)  |  [NuGet 3,5 – poznámky k verzi beta](../release-notes/nuget-3.5-Beta.md)</span><span class="sxs-lookup"><span data-stu-id="3aa70-104">[NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md) | [NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md)</span></span>

<span data-ttu-id="3aa70-105">Hlavním cílem této verze bylo zvýšení kvality 3.4.3 verze nuget.exe s několika opravami rozšíření sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3aa70-105">The primary focus of this release was improvements to the quality of 3.4.3 version of nuget.exe with a few fixes to the Visual Studio extension as well.</span></span>

<span data-ttu-id="3aa70-106">VSIX i nuget.exe si můžete stáhnout [tady](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="3aa70-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="344-rtm-2016-05-19"></a><span data-ttu-id="3aa70-107">[3.4.4 – RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span><span class="sxs-lookup"><span data-stu-id="3aa70-107">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span></span>

[<span data-ttu-id="3aa70-108">Úplný protokol změn</span><span class="sxs-lookup"><span data-stu-id="3aa70-108">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[<span data-ttu-id="3aa70-109">Seznam problémů</span><span class="sxs-lookup"><span data-stu-id="3aa70-109">List of Issues</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a><span data-ttu-id="3aa70-110">Změny</span><span class="sxs-lookup"><span data-stu-id="3aa70-110">Changes</span></span>

- <span data-ttu-id="3aa70-111">Vylepšení sady: vylepšení zabalení symbolů, balení s `project.json` a dalších [ \# 606](https://github.com/NuGet/NuGet.Client/pull/606)</span><span class="sxs-lookup"><span data-stu-id="3aa70-111">Pack Improvements: Improvements to packing symbols, packing with `project.json` and more [\#606](https://github.com/NuGet/NuGet.Client/pull/606)</span></span>
- <span data-ttu-id="3aa70-112">Zobrazit výjimku, pokud dojde k selhání při hledání projektů v příkazu Update [ \# 605] (https://github.com/NuGet/NuGet.Client/pull/605</span><span class="sxs-lookup"><span data-stu-id="3aa70-112">Display exception when there is a failure finding projects in update command [\#605](https://github.com/NuGet/NuGet.Client/pull/605</span></span>
- <span data-ttu-id="3aa70-113">Číst typ balíčku ze vstupu `.nuspec` a `project.json` při balení [ \# 603](https://github.com/NuGet/NuGet.Client/pull/603)</span><span class="sxs-lookup"><span data-stu-id="3aa70-113">Read package type from input `.nuspec` and `project.json` when packing [\#603](https://github.com/NuGet/NuGet.Client/pull/603)</span></span>
- <span data-ttu-id="3aa70-114">Udělejte NuGet. Shared není projekt.</span><span class="sxs-lookup"><span data-stu-id="3aa70-114">Make NuGet.Shared not a project.</span></span> [<span data-ttu-id="3aa70-115">\#602</span><span class="sxs-lookup"><span data-stu-id="3aa70-115">\#602</span></span>](https://github.com/NuGet/NuGet.Client/pull/602)
- <span data-ttu-id="3aa70-116">Použít časový limit nabízených oznámení jako časový limit odpovědi HTTP [ \# 599](https://github.com/NuGet/NuGet.Client/pull/599)</span><span class="sxs-lookup"><span data-stu-id="3aa70-116">Use the push timeout as the HTTP response timeout [\#599](https://github.com/NuGet/NuGet.Client/pull/599)</span></span>
- <span data-ttu-id="3aa70-117">V souborech balíčku s budoucím časem nebudou použity časy [ \# 597](https://github.com/NuGet/NuGet.Client/pull/597)</span><span class="sxs-lookup"><span data-stu-id="3aa70-117">Package files with future times will not have their times used [\#597](https://github.com/NuGet/NuGet.Client/pull/597)</span></span>
- <span data-ttu-id="3aa70-118">Aktualizace `NuGet.Core.dll` verze na 2.12.0 pro opravu problému XML [ \# 594](https://github.com/NuGet/NuGet.Client/pull/594)</span><span class="sxs-lookup"><span data-stu-id="3aa70-118">Updating `NuGet.Core.dll` version to 2.12.0 to fix XML issue [\#594](https://github.com/NuGet/NuGet.Client/pull/594)</span></span>
- <span data-ttu-id="3aa70-119">Support./NuGet.CommandLine.XPlat-v \<verbosity\> \<mode\> [ \# 593](https://github.com/NuGet/NuGet.Client/pull/593)</span><span class="sxs-lookup"><span data-stu-id="3aa70-119">Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)</span></span>
- <span data-ttu-id="3aa70-120">Zobrazit chyby při obnovení bez `project.json` nebo `packages.config` [ \# 590](https://github.com/NuGet/NuGet.Client/pull/590)</span><span class="sxs-lookup"><span data-stu-id="3aa70-120">Display error restoring without `project.json` or `packages.config` [\#590](https://github.com/NuGet/NuGet.Client/pull/590)</span></span>
- <span data-ttu-id="3aa70-121">Oprava verzí závislostí, pokud se požadované verze liší [ \# 559](https://github.com/NuGet/NuGet.Client/pull/559)</span><span class="sxs-lookup"><span data-stu-id="3aa70-121">Fixing dependency versions when required versions differ [\#559](https://github.com/NuGet/NuGet.Client/pull/559)</span></span>