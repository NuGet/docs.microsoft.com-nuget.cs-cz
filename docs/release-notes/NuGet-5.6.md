---
title: Zpráva k vydání verze NuGet 5,6
description: Poznámky k verzi pro NuGet 5,6, včetně nových funkcí, oprav chyb a chcete odeslat obecnou.
author: chgill-msft
ms.author: chgill
ms.date: 05/19/2020
ms.topic: conceptual
ms.openlocfilehash: e8d80a247da1cd18b53b35c51fb3d3dcf1cf68fa
ms.sourcegitcommit: 3529348ed394595d0fa01271486b831af9c97597
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/21/2020
ms.locfileid: "83727819"
---
# <a name="nuget-56-release-notes"></a><span data-ttu-id="3ba94-103">Zpráva k vydání verze NuGet 5,6</span><span class="sxs-lookup"><span data-stu-id="3ba94-103">NuGet 5.6 Release Notes</span></span>

<span data-ttu-id="3ba94-104">Prostředky pro distribuci NuGet:</span><span class="sxs-lookup"><span data-stu-id="3ba94-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="3ba94-105">Verze NuGet</span><span class="sxs-lookup"><span data-stu-id="3ba94-105">NuGet version</span></span> | <span data-ttu-id="3ba94-106">K dispozici ve verzi sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3ba94-106">Available in Visual Studio version</span></span>| <span data-ttu-id="3ba94-107">K dispozici v sadě .NET SDK</span><span class="sxs-lookup"><span data-stu-id="3ba94-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="3ba94-108">**5.6.0**</span><span class="sxs-lookup"><span data-stu-id="3ba94-108">**5.6.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="3ba94-109">Visual Studio 2019 verze 16,6</span><span class="sxs-lookup"><span data-stu-id="3ba94-109">Visual Studio 2019 version 16.6</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="3ba94-110">[3.1.300](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="3ba94-110">[3.1.300](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="3ba94-111"><sup>1</sup> Nainstalováno se sadou Visual Studio 2019 s úlohou .NET Core</span><span class="sxs-lookup"><span data-stu-id="3ba94-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-56"></a><span data-ttu-id="3ba94-112">Shrnutí: Novinky v 5,6</span><span class="sxs-lookup"><span data-stu-id="3ba94-112">Summary: What's New in 5.6</span></span>

* <span data-ttu-id="3ba94-113">Podporuje předběžné verze balíčků s plovoucími verzemi.</span><span class="sxs-lookup"><span data-stu-id="3ba94-113">Support prerelease packages with floating versions.</span></span> <span data-ttu-id="3ba94-114">`Version="*-*"`, `Version="1.*-*"` a podobného typu float na nejnovější verze, včetně předprodejních verzí, v rámci zadaného rozsahu – [#912](https://github.com/NuGet/Home/issues/912)</span><span class="sxs-lookup"><span data-stu-id="3ba94-114">`Version="*-*"`, `Version="1.*-*"`, and similar float to latest versions, including prerelease versions, within specified range  - [#912](https://github.com/NuGet/Home/issues/912)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="3ba94-115">Chyby opravené v této verzi</span><span class="sxs-lookup"><span data-stu-id="3ba94-115">Issues fixed in this release</span></span>

<span data-ttu-id="3ba94-116">**Chyby:**</span><span class="sxs-lookup"><span data-stu-id="3ba94-116">**Bugs:**</span></span>

* <span data-ttu-id="3ba94-117">`nuget push *.nupkg`dojde k chybě, pokud snupkg neexistuje – [#8148](https://github.com/NuGet/Home/issues/8148)</span><span class="sxs-lookup"><span data-stu-id="3ba94-117">`nuget push *.nupkg` fails when snupkg does not exist - [#8148](https://github.com/NuGet/Home/issues/8148)</span></span>

* <span data-ttu-id="3ba94-118">A několik dalších cest kódu, které selžou, závisí na národním prostředí.</span><span class="sxs-lookup"><span data-stu-id="3ba94-118">Pack, and several other code paths, fail dependent on locale.</span></span> <span data-ttu-id="3ba94-119">Použití RegexOptions. CultureInvariant- [#8246](https://github.com/NuGet/Home/issues/8246)</span><span class="sxs-lookup"><span data-stu-id="3ba94-119">Use RegexOptions.CultureInvariant - [#8246](https://github.com/NuGet/Home/issues/8246)</span></span>

* <span data-ttu-id="3ba94-120">Výkon: specifikace DG pro Neuvolněné projektové scénáře by se neměly zapisovat do obnovení verze Preview- [#8793](https://github.com/NuGet/Home/issues/8793)</span><span class="sxs-lookup"><span data-stu-id="3ba94-120">Perf: DG Spec for unloaded project scenarios should not be written in preview restores - [#8793](https://github.com/NuGet/Home/issues/8793)</span></span>

* <span data-ttu-id="3ba94-121">Obnovení: zlepšení výkonu ukládáním specifikací grafu závislostí řešení do mezipaměti – [#9201](https://github.com/NuGet/Home/issues/9201)</span><span class="sxs-lookup"><span data-stu-id="3ba94-121">Restore: Improve performance by caching solution dependency graph spec - [#9201](https://github.com/NuGet/Home/issues/9201)</span></span>

* <span data-ttu-id="3ba94-122">Uživatelské rozhraní PM nefunguje pro projekty stylu sady SDK po instalaci balíčku pomocí konzoly PM – [#9203](https://github.com/NuGet/Home/issues/9203)</span><span class="sxs-lookup"><span data-stu-id="3ba94-122">PM UI doesn't work for SDK style projects after installing a package with PM Console - [#9203](https://github.com/NuGet/Home/issues/9203)</span></span>

* <span data-ttu-id="3ba94-123">Vložená ikona se nedá zobrazit v uživatelském rozhraní PM s informačním kanálem místního balíčku – v závislosti na zapnutém/vs \- [#9225](https://github.com/NuGet/Home/issues/9225)</span><span class="sxs-lookup"><span data-stu-id="3ba94-123">Embedded icon can’t be shown in PM UI with local package feed - depending on / vs \ - [#9225](https://github.com/NuGet/Home/issues/9225)</span></span>

* <span data-ttu-id="3ba94-124">NuGetVersion. TryParseStrict () by měl vrátit hodnotu false, pokud se nepovede analyzovat – [#9255](https://github.com/NuGet/Home/issues/9255)</span><span class="sxs-lookup"><span data-stu-id="3ba94-124">NuGetVersion.TryParseStrict() should return false if it fails to parse - [#9255](https://github.com/NuGet/Home/issues/9255)</span></span>

* <span data-ttu-id="3ba94-125">`nuget.exe push`nápovědu pro `-source` , by měla navrhovat použití názvu zdroje, nikoli zdrojového URL – [#9265](https://github.com/NuGet/Home/issues/9265)</span><span class="sxs-lookup"><span data-stu-id="3ba94-125">`nuget.exe push` help for `-source`, should suggest usage of source name, not source URL - [#9265](https://github.com/NuGet/Home/issues/9265)</span></span>

* <span data-ttu-id="3ba94-126">`dotnet nuget add package SourceUri`Vytvoří chybný výchozí název zdroje balíčku – [#9277](https://github.com/NuGet/Home/issues/9277)</span><span class="sxs-lookup"><span data-stu-id="3ba94-126">`dotnet nuget add package SourceUri`  creates bad default package source name - [#9277](https://github.com/NuGet/Home/issues/9277)</span></span>

* <span data-ttu-id="3ba94-127">Čtečka obrazovky neoznamuje hledání... zpráva při přepínání karet – [#9307](https://github.com/NuGet/Home/issues/9307)</span><span class="sxs-lookup"><span data-stu-id="3ba94-127">Screen reader doesn't announce "Searching..." message when switching tabs - [#9307](https://github.com/NuGet/Home/issues/9307)</span></span>

* <span data-ttu-id="3ba94-128">Usnadnění: barva pro výběr – obdélník není dostupná na kartách uživatelského rozhraní PM v tmavém motivu – [#9336](https://github.com/NuGet/Home/issues/9336)</span><span class="sxs-lookup"><span data-stu-id="3ba94-128">Accessibility: Focus-rectangle color is not accessible PM UI tabs in dark theme - [#9336](https://github.com/NuGet/Home/issues/9336)</span></span>

* <span data-ttu-id="3ba94-129">Nástroj NuGet. exe 5,5 se nemůže obnovit pomocí nástroje MSBuild 14 nebo nižšího [#9458](https://github.com/NuGet/Home/issues/9458)</span><span class="sxs-lookup"><span data-stu-id="3ba94-129">nuget.exe 5.5 fails to restore with MSBuild 14 or below - [#9458](https://github.com/NuGet/Home/issues/9458)</span></span>

* <span data-ttu-id="3ba94-130">V příkazech obnovit zprávy se neprotokolují časy milisekund – [#8977](https://github.com/NuGet/Home/issues/8977)</span><span class="sxs-lookup"><span data-stu-id="3ba94-130">Don't log millisecond times in restore messages - [#8977](https://github.com/NuGet/Home/issues/8977)</span></span>

* <span data-ttu-id="3ba94-131">Převést IOutputConsole na asynchronní [#9268](https://github.com/NuGet/Home/issues/9268)</span><span class="sxs-lookup"><span data-stu-id="3ba94-131">Make IOutputConsole async - [#9268](https://github.com/NuGet/Home/issues/9268)</span></span>

* <span data-ttu-id="3ba94-132">Vyzvednutí verze nástroje MSBuild v některých jazykových kulturách nefunguje správně – [#9322](https://github.com/NuGet/Home/issues/9322)</span><span class="sxs-lookup"><span data-stu-id="3ba94-132">MSBuild version picking works poorly on some non-english cultures - [#9322](https://github.com/NuGet/Home/issues/9322)</span></span>

* <span data-ttu-id="3ba94-133">Chybějící výchozí formát pro `dotnet nuget list source`  -  [#9337](https://github.com/NuGet/Home/issues/9337)</span><span class="sxs-lookup"><span data-stu-id="3ba94-133">Missing format default on `dotnet nuget list source` - [#9337](https://github.com/NuGet/Home/issues/9337)</span></span>

* <span data-ttu-id="3ba94-134">Výkon: RestoreOperationLogger má nepotřebnou spřažení vlákna – [#9288](https://github.com/NuGet/Home/issues/9288)</span><span class="sxs-lookup"><span data-stu-id="3ba94-134">Perf: RestoreOperationLogger has unnecessary thread affinity - [#9288](https://github.com/NuGet/Home/issues/9288)</span></span>

* <span data-ttu-id="3ba94-135">Automatizované vytváření dokumentů pro `dotnet nuget` příkazy – [#9146](https://github.com/NuGet/Home/issues/9146)</span><span class="sxs-lookup"><span data-stu-id="3ba94-135">Automated creation of docs for `dotnet nuget` commands - [#9146](https://github.com/NuGet/Home/issues/9146)</span></span>

* <span data-ttu-id="3ba94-136">Výchozí podrobnost by neměla oznamovat NoOp obnovení jednotlivých projektů – [#8792](https://github.com/NuGet/Home/issues/8792)</span><span class="sxs-lookup"><span data-stu-id="3ba94-136">Default verbosity should not report each project's noop restore - [#8792](https://github.com/NuGet/Home/issues/8792)</span></span>

* <span data-ttu-id="3ba94-137">`-DependencyVersion`Parametr podpory pro příkaz `NuGet.exe update` podobný příkazu install- [#7694](https://github.com/NuGet/Home/issues/7694)</span><span class="sxs-lookup"><span data-stu-id="3ba94-137">Support `-DependencyVersion` parameter for `NuGet.exe update`, similar to install command - [#7694](https://github.com/NuGet/Home/issues/7694)</span></span>


<span data-ttu-id="3ba94-138">**Chcete odeslat obecnou**</span><span class="sxs-lookup"><span data-stu-id="3ba94-138">**DCRs:**</span></span>

* <span data-ttu-id="3ba94-139">Přidat počáteční podporu pro NET 5.0 Target Framework – [#9584](https://github.com/NuGet/Home/issues/9584)</span><span class="sxs-lookup"><span data-stu-id="3ba94-139">Add initial support for net5.0 target framework - [#9584](https://github.com/NuGet/Home/issues/9584)</span></span>

* <span data-ttu-id="3ba94-140">Seřaďte balíčky podle ID na kartě aktualizace uživatelského rozhraní PM – [#9278](https://github.com/NuGet/Home/issues/9278)</span><span class="sxs-lookup"><span data-stu-id="3ba94-140">Sort packages by ID in the Updates tab of the PM UI - [#9278](https://github.com/NuGet/Home/issues/9278)</span></span>


<span data-ttu-id="3ba94-141">**[Seznam všech problémů opravených v této verzi – 5,6](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e3b2080c4b30708e48bf9f3)**</span><span class="sxs-lookup"><span data-stu-id="3ba94-141">**[List of all issues fixed in this release - 5.6](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e3b2080c4b30708e48bf9f3)**</span></span>
