---
title: Poznámky k verzi NuGet 5,2 RTM
description: Poznámky k verzi pro NuGet 5,2, včetně nových funkcí, oprav chyb a chcete odeslat obecnou.
author: karann-msft
ms.author: karann
ms.date: 07/23/2019
ms.topic: conceptual
ms.openlocfilehash: f94bd8ddb8fac8bf47c2826bf5b417595b0efa8b
ms.sourcegitcommit: f291ff91561a6b58c2aec41c624d798e00ce41fa
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/24/2019
ms.locfileid: "68471199"
---
# <a name="nuget-52-release-notes"></a><span data-ttu-id="6507e-103">Zpráva k vydání verze NuGet 5,2</span><span class="sxs-lookup"><span data-stu-id="6507e-103">NuGet 5.2 Release Notes</span></span>

<span data-ttu-id="6507e-104">Prostředky pro distribuci NuGet:</span><span class="sxs-lookup"><span data-stu-id="6507e-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="6507e-105">Verze NuGet</span><span class="sxs-lookup"><span data-stu-id="6507e-105">NuGet version</span></span> | <span data-ttu-id="6507e-106">K dispozici ve verzi sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6507e-106">Available in Visual Studio version</span></span>| <span data-ttu-id="6507e-107">K dispozici v sadě .NET SDK</span><span class="sxs-lookup"><span data-stu-id="6507e-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="6507e-108">**5.2.0**</span><span class="sxs-lookup"><span data-stu-id="6507e-108">**5.2.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="6507e-109">Visual Studio 2019 verze 16,2</span><span class="sxs-lookup"><span data-stu-id="6507e-109">Visual Studio 2019 version 16.2</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="6507e-110">[2.1.80 X](https://dotnet.microsoft.com/download/dotnet-core/2.1) <sup>1</sup>, [2.2.40 ×](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="6507e-110">[2.1.80X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.40X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="6507e-111"><sup>1</sup> Nainstalováno se sadou Visual Studio 2019 s úlohou .NET Core</span><span class="sxs-lookup"><span data-stu-id="6507e-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="6507e-112"><sup>2</sup> . K dispozici jako volitelná instalace se sadou Visual Studio 2019 s úlohou .NET Core</span><span class="sxs-lookup"><span data-stu-id="6507e-112"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-52"></a><span data-ttu-id="6507e-113">Shrnut Co je nového v 5,2</span><span class="sxs-lookup"><span data-stu-id="6507e-113">Summary: What's New in 5.2</span></span>

* <span data-ttu-id="6507e-114">Opravili jsme kritickou chybu, která způsobila občasné selhání operací NuGet z důvodu potíží s cestou na platformě Linux & Mac – [#7341](https://github.com/NuGet/Home/issues/7341)</span><span class="sxs-lookup"><span data-stu-id="6507e-114">Fixed a critical bug that caused occasional NuGet operation failures due to path issues on Linux & Mac - [#7341](https://github.com/NuGet/Home/issues/7341)</span></span>

* <span data-ttu-id="6507e-115">Vylepšená rychlost odezvy uživatelského rozhraní při procházení balíčků pomocí uživatelského rozhraní Správce balíčků NuGet v aplikaci Visual Studio, obzvláště pro pomalé zdroje – [#8039](https://github.com/NuGet/Home/issues/8039)</span><span class="sxs-lookup"><span data-stu-id="6507e-115">Improved UI responsiveness when browsing packages using the NuGet package manager UI in Visual Studio especially noticeable for slow sources - [#8039](https://github.com/NuGet/Home/issues/8039)</span></span>

* <span data-ttu-id="6507e-116">Tuny oprav spolehlivosti pro soubor zámku ([#8187](https://github.com/NuGet/Home/issues/8187),[#8160](https://github.com/NuGet/Home/issues/8160),[#8114](https://github.com/NuGet/Home/issues/8114),[#7840](https://github.com/NuGet/Home/issues/7840)) a ověřovací modul plug-in ([#8300](https://github.com/NuGet/Home/issues/8300),[#8271](https://github.com/NuGet/Home/issues/8271),[#8269](https://github.com/NuGet/Home/issues/8269),[#8210](https://github.com/NuGet/Home/issues/8210),[#8198](https://github.com/NuGet/Home/issues/8198),[#7845](https://github.com/NuGet/Home/issues/7845))</span><span class="sxs-lookup"><span data-stu-id="6507e-116">Tons of reliability fixes for lock file ([#8187](https://github.com/NuGet/Home/issues/8187),[#8160](https://github.com/NuGet/Home/issues/8160),[#8114](https://github.com/NuGet/Home/issues/8114),[#7840](https://github.com/NuGet/Home/issues/7840)) and authentication plugin ([#8300](https://github.com/NuGet/Home/issues/8300),[#8271](https://github.com/NuGet/Home/issues/8271),[#8269](https://github.com/NuGet/Home/issues/8269),[#8210](https://github.com/NuGet/Home/issues/8210),[#8198](https://github.com/NuGet/Home/issues/8198),[#7845](https://github.com/NuGet/Home/issues/7845))</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="6507e-117">Chyby opravené v této verzi</span><span class="sxs-lookup"><span data-stu-id="6507e-117">Issues fixed in this release</span></span>

<span data-ttu-id="6507e-118">**Štěnic**</span><span class="sxs-lookup"><span data-stu-id="6507e-118">**Bugs**</span></span>

* <span data-ttu-id="6507e-119">Výkon Konzola správce balíčků:  Zpožděná aktualizace uživatelského rozhraní se seznamem výchozích hodnot pro výchozí projekt [#8235](https://github.com/NuGet/Home/issues/8235)</span><span class="sxs-lookup"><span data-stu-id="6507e-119">Perf: Package Manager Console:  UI delay updating "Default project" combobox selected value - [#8235](https://github.com/NuGet/Home/issues/8235)</span></span>

* <span data-ttu-id="6507e-120">Výkon Vylepšení výkonu v uživatelském rozhraní PM – [#8039](https://github.com/NuGet/Home/issues/8039)</span><span class="sxs-lookup"><span data-stu-id="6507e-120">Perf: Performance improvements in the PM UI - [#8039](https://github.com/NuGet/Home/issues/8039)</span></span>

* <span data-ttu-id="6507e-121">Výkon Zpoždění uživatelského rozhraní při čtení výchozího projektu v PMC- [#6824](https://github.com/NuGet/Home/issues/6824)</span><span class="sxs-lookup"><span data-stu-id="6507e-121">Perf: UI Delay when reading Default Project in PMC - [#6824](https://github.com/NuGet/Home/issues/6824)</span></span>

* <span data-ttu-id="6507e-122">Perf: [vsfeedback] karta aktualizace NuGet se zablokuje pro zdroj místního balíčku [#6470](https://github.com/NuGet/Home/issues/6470)</span><span class="sxs-lookup"><span data-stu-id="6507e-122">Perf: [vsfeedback] NuGet Update tab freezes for a local package source - [#6470](https://github.com/NuGet/Home/issues/6470)</span></span>

* <span data-ttu-id="6507e-123">Zobecněn  NuGet čeká plný časový limit handshake, pokud se nepovede modul plug-in spustit nebo ukončí [#8300](https://github.com/NuGet/Home/issues/8300) .</span><span class="sxs-lookup"><span data-stu-id="6507e-123">Plugins:  NuGet waits full handshake timeout if plugin fails to launch or terminates early - [#8300](https://github.com/NuGet/Home/issues/8300)</span></span>

* <span data-ttu-id="6507e-124">Moduly plug-in: vylepšení diagnostiky selhání spuštění modulu plug-in – [#8271](https://github.com/NuGet/Home/issues/8271)</span><span class="sxs-lookup"><span data-stu-id="6507e-124">Plugins:  improve diagnosability of plugin launch failure - [#8271](https://github.com/NuGet/Home/issues/8271)</span></span>

* <span data-ttu-id="6507e-125">Zobecněn Problém se zjišťováním integrovaných modulů plug-in v NuGet. exe – [#8269](https://github.com/NuGet/Home/issues/8269)</span><span class="sxs-lookup"><span data-stu-id="6507e-125">Plugins: Issue with nuget.exe discovery of built in plugins - [#8269](https://github.com/NuGet/Home/issues/8269)</span></span>

* <span data-ttu-id="6507e-126">Moduly plug-in: soubor Cache není nikdy čten – [#8210](https://github.com/NuGet/Home/issues/8210)</span><span class="sxs-lookup"><span data-stu-id="6507e-126">Plugins:  cache file is never read - [#8210](https://github.com/NuGet/Home/issues/8210)</span></span>

* <span data-ttu-id="6507e-127">Zobecněn  Úloha byla zrušena.</span><span class="sxs-lookup"><span data-stu-id="6507e-127">Plugins:  "A task was canceled."</span></span> <span data-ttu-id="6507e-128">chyby s modulem plug-in ověřování při obnovení – [#8198](https://github.com/NuGet/Home/issues/8198)</span><span class="sxs-lookup"><span data-stu-id="6507e-128">errors with authentication plugin during restore - [#8198](https://github.com/NuGet/Home/issues/8198)</span></span>

* <span data-ttu-id="6507e-129">Nezjistitelná mezipaměť modulů plug-in na platformách Linux – [#7845](https://github.com/NuGet/Home/issues/7845)</span><span class="sxs-lookup"><span data-stu-id="6507e-129">Plugins cache not discoverable intermittently on linux platforms - [#7845](https://github.com/NuGet/Home/issues/7845)</span></span>

* <span data-ttu-id="6507e-130">LockFile: s ATF má nepravdivé NU1004 z důvodu chybné kontroly rovnosti cílového rozhraní [#8187](https://github.com/NuGet/Home/issues/8187)</span><span class="sxs-lookup"><span data-stu-id="6507e-130">LockFile: with ATF, it has false NU1004 due to a bad target framework equality check - [#8187](https://github.com/NuGet/Home/issues/8187)</span></span>

* <span data-ttu-id="6507e-131">LockFile: příznak obnovení uzamčeného režimu se nerespektuje, pokud je soubor zámku prázdný nebo je poškozený – [#8160](https://github.com/NuGet/Home/issues/8160)</span><span class="sxs-lookup"><span data-stu-id="6507e-131">LockFile: '--locked-mode' restore flag not respected if lock file is empty or malformed - [#8160](https://github.com/NuGet/Home/issues/8160)</span></span>

* <span data-ttu-id="6507e-132">LockFile: Nejedná se o projekty s názvy vlastních sestavení v balíčcích soubor zámku- [#8114](https://github.com/NuGet/Home/issues/8114)</span><span class="sxs-lookup"><span data-stu-id="6507e-132">LockFile: Don't lowercase projects with custom assembly names in packages lock file - [#8114](https://github.com/NuGet/Home/issues/8114)</span></span>

* <span data-ttu-id="6507e-133">LockFile: Vytvořit odkaz na projekt v případě souboru zámku malými písmeny – [#7840](https://github.com/NuGet/Home/issues/7840)</span><span class="sxs-lookup"><span data-stu-id="6507e-133">LockFile: Make project reference lower case in lock file  - [#7840](https://github.com/NuGet/Home/issues/7840)</span></span>

* <span data-ttu-id="6507e-134">Obnovení: při instalaci úmyslně podepsaného balíčku dojde k několika neúspěšným pokusům o instalaci (s opakovaným výstupem) – [#8175](https://github.com/NuGet/Home/issues/8175)</span><span class="sxs-lookup"><span data-stu-id="6507e-134">Restore:  installing a tampered signed package results in multiple failed install attempts (with repeated output) - [#8175](https://github.com/NuGet/Home/issues/8175)</span></span>

* <span data-ttu-id="6507e-135">VS: Nepodařilo se deserializovat možnosti uživatele řešení po aktualizaci NuGet – [#8166](https://github.com/NuGet/Home/issues/8166)</span><span class="sxs-lookup"><span data-stu-id="6507e-135">VS: solution user options fail to deserialize after NuGet update - [#8166](https://github.com/NuGet/Home/issues/8166)</span></span>

* <span data-ttu-id="6507e-136">dotnet-list-Package v projektu UnitTest vrátí chybu – [#8154](https://github.com/NuGet/Home/issues/8154)</span><span class="sxs-lookup"><span data-stu-id="6507e-136">dotnet-list-package in a UnitTest project returns an error - [#8154](https://github.com/NuGet/Home/issues/8154)</span></span>

* <span data-ttu-id="6507e-137">Vytvořit skupinu balíčků NuGet pro instalační program VS – oprava některých problémů s instalací VSIX – [#8033](https://github.com/NuGet/Home/issues/8033)</span><span class="sxs-lookup"><span data-stu-id="6507e-137">Create NuGet package group for VS installer - fixing some VSIX setup problems - [#8033](https://github.com/NuGet/Home/issues/8033)</span></span>

* <span data-ttu-id="6507e-138">GeneratePackageOnBuild by neměl nastavovat Build.</span><span class="sxs-lookup"><span data-stu-id="6507e-138">GeneratePackageOnBuild should not set NoBuild.</span></span><span data-ttu-id="6507e-139"> - [#7801](https://github.com/NuGet/Home/issues/7801)</span><span class="sxs-lookup"><span data-stu-id="6507e-139"> - [#7801](https://github.com/NuGet/Home/issues/7801)</span></span>

* <span data-ttu-id="6507e-140">Nová možnost "-SymbolPackageFormat snupkg" vygeneruje chybu, pokud soubor. nuspec obsahuje explicitní element odkazu na sestavení- [#7638](https://github.com/NuGet/Home/issues/7638)</span><span class="sxs-lookup"><span data-stu-id="6507e-140">The new option "-SymbolPackageFormat snupkg" generates an error when the .nuspec file contains an explicit assembly reference element - [#7638](https://github.com/NuGet/Home/issues/7638)</span></span>

* <span data-ttu-id="6507e-141">NuGet. TARGETS (498; 5): Chyba: Nepovedlo se najít část cesty/tmp/NuGetScratch- [#7341](https://github.com/NuGet/Home/issues/7341) .</span><span class="sxs-lookup"><span data-stu-id="6507e-141">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - [#7341](https://github.com/NuGet/Home/issues/7341)</span></span>

<span data-ttu-id="6507e-142">**DCR**</span><span class="sxs-lookup"><span data-stu-id="6507e-142">**DCR:**</span></span>

* <span data-ttu-id="6507e-143">Přidání vlastnosti MSBuild, která indikuje, že je PackageDownload podporovaný – [#8106](https://github.com/NuGet/Home/issues/8106)</span><span class="sxs-lookup"><span data-stu-id="6507e-143">Add an msbuild property that indicates that PackageDownload is supported - [#8106](https://github.com/NuGet/Home/issues/8106)</span></span>

* <span data-ttu-id="6507e-144">FrameworkReference potlačí tok závislostí prostřednictvím FrameworkReference. PrivateAssets- [#7988](https://github.com/NuGet/Home/issues/7988)</span><span class="sxs-lookup"><span data-stu-id="6507e-144">FrameworkReference suppress dependency flow via FrameworkReference.PrivateAssets - [#7988](https://github.com/NuGet/Home/issues/7988)</span></span>

* <span data-ttu-id="6507e-145">Mechanismus pro dodávání modulu runtime. JSON mimo balíček – [#7351](https://github.com/NuGet/Home/issues/7351)</span><span class="sxs-lookup"><span data-stu-id="6507e-145">Mechanism for supplying runtime.json outside of a package - [#7351](https://github.com/NuGet/Home/issues/7351)</span></span>

<span data-ttu-id="6507e-146">**[Seznam všech problémů opravených v této verzi – 5,2 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.2")**</span><span class="sxs-lookup"><span data-stu-id="6507e-146">**[List of all issues fixed in this release - 5.2 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.2")**</span></span>


