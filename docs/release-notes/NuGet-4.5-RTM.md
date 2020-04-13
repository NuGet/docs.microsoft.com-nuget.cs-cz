---
title: NuGet 4,5 RTM poznámky k verzi
description: Poznámky k verzi pro NuGet 4.5 RTM včetně známých problémů, oprav chyb, přidaných funkcí a řadičů domény.
author: anangaur
ms.author: anangaur
ms.date: 12/4/2017
ms.topic: conceptual
ms.openlocfilehash: 321aedb471bc6f86e9c03878093b199267e31195
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496573"
---
# <a name="nuget-45-release-notes"></a><span data-ttu-id="1b01a-103">NuGet 4.5 Poznámky k verzi</span><span class="sxs-lookup"><span data-stu-id="1b01a-103">NuGet 4.5 Release Notes</span></span>

<span data-ttu-id="1b01a-104">[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) přichází s [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="1b01a-104">[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).</span></span>

## <a name="summary-whats-new-in-450"></a><span data-ttu-id="1b01a-105">Shrnutí: Co je nového v 4.5.0</span><span class="sxs-lookup"><span data-stu-id="1b01a-105">Summary: What's New in 4.5.0</span></span>

## <a name="summary-whats-new-in-452"></a><span data-ttu-id="1b01a-106">Shrnutí: Co je nového v 4.5.2</span><span class="sxs-lookup"><span data-stu-id="1b01a-106">Summary: What's New in 4.5.2</span></span>

* <span data-ttu-id="1b01a-107">Oprava zabezpečení: Oprávnění k souborům vytvořeným uvnitř ~/.nuget jsou příliš otevřená [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span><span class="sxs-lookup"><span data-stu-id="1b01a-107">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>

## <a name="summary-whats-new-in-453"></a><span data-ttu-id="1b01a-108">Shrnutí: Co je nového v 4.5.3</span><span class="sxs-lookup"><span data-stu-id="1b01a-108">Summary: What's New in 4.5.3</span></span>

* <span data-ttu-id="1b01a-109">Oprava zabezpečení: Soubory uvnitř NUPKGs mohou mít relativní cestu nad adresářem NUPKG [#7906](https://github.com/NuGet/Home/issues/7906)</span><span class="sxs-lookup"><span data-stu-id="1b01a-109">Security Fix: Files inside of NUPKGs can have a relative path above the NUPKG directory [#7906](https://github.com/NuGet/Home/issues/7906)</span></span>

## <a name="known-issues"></a><span data-ttu-id="1b01a-110">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="1b01a-110">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="1b01a-111">Problémy s rozhraním .NET Standard 2.0 s rozhraním .NET Framework & NuGet</span><span class="sxs-lookup"><span data-stu-id="1b01a-111">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="1b01a-112">.NET Standard & jeho nástroje byly navrženy tak, že projekty zaměřené na rozhraní .NET Framework 4.6.1 mohou využívat balíčky NuGet & projekty zaměřené na standard .NET Standard 2.0 nebo starší.</span><span class="sxs-lookup"><span data-stu-id="1b01a-112">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="1b01a-113">[Tento dokument](https://github.com/dotnet/standard/issues/481) shrnuje problémy kolem tohoto scénáře, plán pro jejich řešení a řešení, která můžete nasadit s dnešním stavem nástrojů.</span><span class="sxs-lookup"><span data-stu-id="1b01a-113">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="1b01a-114">Pomocí Nástroje pro balení Nuget nelze zobrazit, přidat nebo aktualizovat nástroje DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="1b01a-114">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="1b01a-115">Problém</span><span class="sxs-lookup"><span data-stu-id="1b01a-115">Issue</span></span>

<span data-ttu-id="1b01a-116">Správce balíčků NuGet nezobrazuje a nepovoluje přidat nebo aktualizovat DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="1b01a-116">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="1b01a-117">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="1b01a-117">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="1b01a-118">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="1b01a-118">Workaround</span></span>

<span data-ttu-id="1b01a-119">V souboru projektu se musí ručně upravit DotNetCLIToolReferences.</span><span class="sxs-lookup"><span data-stu-id="1b01a-119">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="1b01a-120">Změna cílení verze cílové architektury může vést k nekompletnímu IntelliSense</span><span class="sxs-lookup"><span data-stu-id="1b01a-120">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="1b01a-121">Problém</span><span class="sxs-lookup"><span data-stu-id="1b01a-121">Issue</span></span>

<span data-ttu-id="1b01a-122">Změna cílení verze cílové architektury v sadě Visual Studio může vést k nekompletnímu IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="1b01a-122">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="1b01a-123">To se stává, když jako formát správce balíčků používáte PackageReferences.</span><span class="sxs-lookup"><span data-stu-id="1b01a-123">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="1b01a-124">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="1b01a-124">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="1b01a-125">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="1b01a-125">Workaround</span></span>

<span data-ttu-id="1b01a-126">Proveďte ruční obnovení.</span><span class="sxs-lookup"><span data-stu-id="1b01a-126">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="1b01a-127">Balíček v projektu .NET Core, který obsahuje sestavení s neplatným podpisem, může aktivovat nekonečnou smyčku obnovení</span><span class="sxs-lookup"><span data-stu-id="1b01a-127">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="1b01a-128">Problém</span><span class="sxs-lookup"><span data-stu-id="1b01a-128">Issue</span></span>

<span data-ttu-id="1b01a-129">V některých případech při použití balíčku, který obsahuje sestavení s neplatným podpisem nebo když je verze balíčku nastavena s panelem DateTime, způsobí, že automatické obnovení balíčku bude spuštěno v nekonečné smyčce [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457).</span><span class="sxs-lookup"><span data-stu-id="1b01a-129">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="1b01a-130">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="1b01a-130">Workaround</span></span>

<span data-ttu-id="1b01a-131">Pro tento problém zatím neexistuje alternativní řešení.</span><span class="sxs-lookup"><span data-stu-id="1b01a-131">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a><span data-ttu-id="1b01a-132">Problémy opravené v časovém rámci NuGet 4.5 RTM</span><span class="sxs-lookup"><span data-stu-id="1b01a-132">Issues fixed in NuGet 4.5 RTM timeframe</span></span>

<span data-ttu-id="1b01a-133">Problémy opravené v NuGet 4.4 RTM naleznete v [nuget4.4 RTM poznámky k verzi](../release-notes/nuget-4.4-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="1b01a-133">For issues fixed in NuGet 4.4 RTM, please refer to [NuGet 4.4 RTM Release Notes](../release-notes/nuget-4.4-RTM.md)</span></span> 

### <a name="features"></a><span data-ttu-id="1b01a-134">Funkce</span><span class="sxs-lookup"><span data-stu-id="1b01a-134">Features</span></span>

- <span data-ttu-id="1b01a-135">Zakázat automatické nabízení symbolů - [#6113](https://github.com/NuGet/Home/issues/6113)</span><span class="sxs-lookup"><span data-stu-id="1b01a-135">Disable auto-push of symbols package - [#6113](https://github.com/NuGet/Home/issues/6113)</span></span>

### <a name="bugs"></a><span data-ttu-id="1b01a-136">Chyby</span><span class="sxs-lookup"><span data-stu-id="1b01a-136">Bugs</span></span>

- <span data-ttu-id="1b01a-137">[Regrese] v 15.5p1: Portable0.0 je přeskočeno - [#6105](https://github.com/NuGet/Home/issues/6105)</span><span class="sxs-lookup"><span data-stu-id="1b01a-137">[Regression] in 15.5p1: Portable0.0 is skipped - [#6105](https://github.com/NuGet/Home/issues/6105)</span></span>
- <span data-ttu-id="1b01a-138">Prostředky z balíčků chybí po obnovení - [#5995](https://github.com/NuGet/Home/issues/5995)</span><span class="sxs-lookup"><span data-stu-id="1b01a-138">Assets from packages are missing after restore - [#5995](https://github.com/NuGet/Home/issues/5995)</span></span>
- <span data-ttu-id="1b01a-139">Poskytovatelé pověření pluginů nepracují s identifikátory URI obsahujícími mezery - [#5982](https://github.com/NuGet/Home/issues/5982)</span><span class="sxs-lookup"><span data-stu-id="1b01a-139">Plugin credential providers do not work with URIs containing spaces - [#5982](https://github.com/NuGet/Home/issues/5982)</span></span>
- <span data-ttu-id="1b01a-140">Pokud se balíček nepodařilo obnovit, chyba by měla být vytištěna ve výstupu i s minimální podrobností ON - [#5658](https://github.com/NuGet/Home/issues/5658)</span><span class="sxs-lookup"><span data-stu-id="1b01a-140">If package failed to restore, error should be printed in the output even with Minimal verbosity ON - [#5658](https://github.com/NuGet/Home/issues/5658)</span></span>
- <span data-ttu-id="1b01a-141">dotnet</span><span class="sxs-lookup"><span data-stu-id="1b01a-141">dotnet</span></span>
  - <span data-ttu-id="1b01a-142">dotnetcore obnovení na úrovni řešení nedodržuje ProjectReference s ReferenceOutputAssembly false vedoucí k selhání náhodné sestavení - [#5490](https://github.com/NuGet/Home/issues/5490)</span><span class="sxs-lookup"><span data-stu-id="1b01a-142">dotnetcore restore at solution-level doesn't follow ProjectReference with ReferenceOutputAssembly of false leading to random build failures - [#5490](https://github.com/NuGet/Home/issues/5490)</span></span>
- <span data-ttu-id="1b01a-143">Automatické dokončování v PMC pracuje nesprávně s objektovými metodami - [#4800](https://github.com/NuGet/Home/issues/4800)</span><span class="sxs-lookup"><span data-stu-id="1b01a-143">Auto-complete in PMC works incorrectly with object methods - [#4800](https://github.com/NuGet/Home/issues/4800)</span></span>
- <span data-ttu-id="1b01a-144">Obnovení nástroje nuget.exe se nezdaří pomocí sady nástrojů sady nástrojů Sady nástrojů Visual Studio 2015 – [#4713](https://github.com/NuGet/Home/issues/4713)</span><span class="sxs-lookup"><span data-stu-id="1b01a-144">nuget.exe restore fails with Visual Studio 2015 toolset - [#4713](https://github.com/NuGet/Home/issues/4713)</span></span>
- <span data-ttu-id="1b01a-145">perf - pmc je drahé na konkretizovat v vs2017 - [#4205](https://github.com/NuGet/Home/issues/4205)</span><span class="sxs-lookup"><span data-stu-id="1b01a-145">perf - pmc is expensive to instantiate in vs2017 - [#4205](https://github.com/NuGet/Home/issues/4205)</span></span>
- <span data-ttu-id="1b01a-146">Pomalé získání informací o závislostech na pomalém připojení - [#4089](https://github.com/NuGet/Home/issues/4089)</span><span class="sxs-lookup"><span data-stu-id="1b01a-146">Slow to get dependency information on slow connection - [#4089](https://github.com/NuGet/Home/issues/4089)</span></span>
- <span data-ttu-id="1b01a-147">uninstall-package w/ -RemoveDependencies se nezdaří, pokud více balíčků sdílí společnou závislost - [#4026](https://github.com/NuGet/Home/issues/4026)</span><span class="sxs-lookup"><span data-stu-id="1b01a-147">uninstall-package w/ -RemoveDependencies will fail if multiple packages share a common dependency - [#4026](https://github.com/NuGet/Home/issues/4026)</span></span>
- <span data-ttu-id="1b01a-148">Finalize NuGet.Core.nupkg pro publikování - [#3581](https://github.com/NuGet/Home/issues/3581)</span><span class="sxs-lookup"><span data-stu-id="1b01a-148">Finalize NuGet.Core.nupkg for publishing - [#3581](https://github.com/NuGet/Home/issues/3581)</span></span>
- <span data-ttu-id="1b01a-149">Sada NuGet pack řeší ID závislostí z názvu adresáře, když se pro csproj + project.js [#3566on](https://github.com/NuGet/Home/issues/3566) používá -IncludeProjectReferences</span><span class="sxs-lookup"><span data-stu-id="1b01a-149">NuGet pack resolves dependency ID from directory name when -IncludeProjectReferences is used for csproj + project.json - [#3566](https://github.com/NuGet/Home/issues/3566)</span></span>
- <span data-ttu-id="1b01a-150">Inicializátor typu pro "NuGet.ProxyCache" vyvolal výjimku - [#3144](https://github.com/NuGet/Home/issues/3144)</span><span class="sxs-lookup"><span data-stu-id="1b01a-150">The type initializer for 'NuGet.ProxyCache' threw an exception - [#3144](https://github.com/NuGet/Home/issues/3144)</span></span>
- <span data-ttu-id="1b01a-151">nuget obnovení výkonu problém s kudu - [#3087](https://github.com/NuGet/Home/issues/3087)</span><span class="sxs-lookup"><span data-stu-id="1b01a-151">nuget restore performance issue with kudu - [#3087](https://github.com/NuGet/Home/issues/3087)</span></span>
- <span data-ttu-id="1b01a-152">Klient ui nezobrazí žádnou chybu nebo upozornění, pokud je hledání před objekty BLOB registrace - [#2149](https://github.com/NuGet/Home/issues/2149)</span><span class="sxs-lookup"><span data-stu-id="1b01a-152">UI Client fails to show any error or warning when search is ahead of registration blobs - [#2149](https://github.com/NuGet/Home/issues/2149)</span></span>
- <span data-ttu-id="1b01a-153">Get-Packages -Updates generuje nesprávný dotaz - [#2135](https://github.com/NuGet/Home/issues/2135)</span><span class="sxs-lookup"><span data-stu-id="1b01a-153">Get-Packages -Updates generates an incorrect query - [#2135](https://github.com/NuGet/Home/issues/2135)</span></span>

## <a name="links-to-github-issues-fixed-in-45-rtm"></a><span data-ttu-id="1b01a-154">Odkazy na problémy GitHubu opravené v 4.5 RTM</span><span class="sxs-lookup"><span data-stu-id="1b01a-154">Links to GitHub issues fixed in 4.5 RTM</span></span>

[<span data-ttu-id="1b01a-155">Seznam problémů</span><span class="sxs-lookup"><span data-stu-id="1b01a-155">Issues list</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)
