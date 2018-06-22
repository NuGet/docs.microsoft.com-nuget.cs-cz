---
title: Poznámky k verzi 4.5 RTM NuGet
description: Poznámky k verzi pro NuGet 4.5 RTM, včetně známé problémy, opravy chyb, přidaných funkcí a chcete.
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 12/4/2017
ms.topic: conceptual
ms.openlocfilehash: 1d04c508d029a6d92bbd480fe3bd7dc14727970e
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820713"
---
# <a name="nuget-45-rtm-release-notes"></a><span data-ttu-id="3241d-103">Poznámky k verzi 4.5 RTM NuGet</span><span class="sxs-lookup"><span data-stu-id="3241d-103">NuGet 4.5 RTM Release Notes</span></span>

<span data-ttu-id="3241d-104">[Visual Studio 2017 15,5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) se dodává s [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="3241d-104">[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).</span></span>

## <a name="known-issues"></a><span data-ttu-id="3241d-105">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="3241d-105">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="3241d-106">Problémy s .NET standardní 2.0 pomocí rozhraní .NET Framework & NuGet</span><span class="sxs-lookup"><span data-stu-id="3241d-106">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="3241d-107">.NET standard & jeho nástrojů je navržené tak, aby projektech zacílených na rozhraní .NET Framework 4.6.1 může využívat balíčky NuGet & projektech zacílených na standardní rozhraní .NET 2.0 nebo dřívější.</span><span class="sxs-lookup"><span data-stu-id="3241d-107">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="3241d-108">[Tento dokument](https://github.com/dotnet/standard/issues/481) shrnuje problémy kolem tento scénář, plán pro adresování a alternativní řešení můžete nasadit s je aktuální stav nástrojů.</span><span class="sxs-lookup"><span data-stu-id="3241d-108">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="3241d-109">Nelze zobrazit, přidat nebo aktualizovat DotNetCLITools pomocí Správce balíčků Nuget</span><span class="sxs-lookup"><span data-stu-id="3241d-109">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="3241d-110">Problém</span><span class="sxs-lookup"><span data-stu-id="3241d-110">Issue</span></span>

<span data-ttu-id="3241d-111">Správce balíčků NuGet nezobrazuje a nepovoluje přidat nebo aktualizovat DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="3241d-111">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="3241d-112">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="3241d-112">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="3241d-113">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="3241d-113">Workaround</span></span>

<span data-ttu-id="3241d-114">V souboru projektu se musí ručně upravit DotNetCLIToolReferences.</span><span class="sxs-lookup"><span data-stu-id="3241d-114">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="3241d-115">Změna cílení cílové verze rozhraní může vést k nekompletnímu IntelliSense</span><span class="sxs-lookup"><span data-stu-id="3241d-115">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="3241d-116">Problém</span><span class="sxs-lookup"><span data-stu-id="3241d-116">Issue</span></span>

<span data-ttu-id="3241d-117">Změna cílení cílové verze rozhraní v sadě Visual Studio může vést k nekompletnímu IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="3241d-117">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="3241d-118">To se stává, když jako formát správce balíčků používáte PackageReferences.</span><span class="sxs-lookup"><span data-stu-id="3241d-118">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="3241d-119">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="3241d-119">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="3241d-120">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="3241d-120">Workaround</span></span>

<span data-ttu-id="3241d-121">Proveďte ruční obnovení.</span><span class="sxs-lookup"><span data-stu-id="3241d-121">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="3241d-122">Balíček v projektu .NET Core, který obsahuje sestavení s neplatným podpisem, může aktivovat nekonečnou smyčku obnovení</span><span class="sxs-lookup"><span data-stu-id="3241d-122">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="3241d-123">Problém</span><span class="sxs-lookup"><span data-stu-id="3241d-123">Issue</span></span>

<span data-ttu-id="3241d-124">V některých případech při použití balíček, který obsahuje sestavení s neplatným podpisem nebo pokud verze balíčku nastavena, DateTime, burzovní způsobuje, že auto obnovení balíčku ke spuštění v nekonečné smyčce [dotnet/projektu systému #1457](https://github.com/dotnet/project-system/issues/1457).</span><span class="sxs-lookup"><span data-stu-id="3241d-124">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="3241d-125">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="3241d-125">Workaround</span></span>

<span data-ttu-id="3241d-126">Pro tento problém zatím neexistuje alternativní řešení.</span><span class="sxs-lookup"><span data-stu-id="3241d-126">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a><span data-ttu-id="3241d-127">Chyby v období NuGet 4.5 RTM</span><span class="sxs-lookup"><span data-stu-id="3241d-127">Issues fixed in NuGet 4.5 RTM timeframe</span></span>

<span data-ttu-id="3241d-128">Chyby v NuGet 4.4 RTM, naleznete v [NuGet 4.4 RTM poznámky](../release-notes/nuget-4.4-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="3241d-128">For issues fixed in NuGet 4.4 RTM, please refer to [NuGet 4.4 RTM Release Notes](../release-notes/nuget-4.4-RTM.md)</span></span> 

### <a name="features"></a><span data-ttu-id="3241d-129">Funkce</span><span class="sxs-lookup"><span data-stu-id="3241d-129">Features</span></span>

- <span data-ttu-id="3241d-130">Zakázat automatické nabízené symboly balíčku - [#6113](https://github.com/NuGet/Home/issues/6113)</span><span class="sxs-lookup"><span data-stu-id="3241d-130">Disable auto-push of symbols package - [#6113](https://github.com/NuGet/Home/issues/6113)</span></span>

### <a name="bugs"></a><span data-ttu-id="3241d-131">Chyby</span><span class="sxs-lookup"><span data-stu-id="3241d-131">Bugs</span></span>

- <span data-ttu-id="3241d-132">[Regrese] v 15.5p1: bylo přeskočeno Portable0.0 - [#6105](https://github.com/NuGet/Home/issues/6105)</span><span class="sxs-lookup"><span data-stu-id="3241d-132">[Regression] in 15.5p1: Portable0.0 is skipped - [#6105](https://github.com/NuGet/Home/issues/6105)</span></span>
- <span data-ttu-id="3241d-133">Po obnovení – chybí prostředky z balíčků [#5995](https://github.com/NuGet/Home/issues/5995)</span><span class="sxs-lookup"><span data-stu-id="3241d-133">Assets from packages are missing after restore - [#5995](https://github.com/NuGet/Home/issues/5995)</span></span>
- <span data-ttu-id="3241d-134">Poskytovatelé přihlašovacích údajů modulu plug-in nefungují s identifikátory URI obsahující mezery - [#5982](https://github.com/NuGet/Home/issues/5982)</span><span class="sxs-lookup"><span data-stu-id="3241d-134">Plugin credential providers do not work with URIs containing spaces - [#5982](https://github.com/NuGet/Home/issues/5982)</span></span>
- <span data-ttu-id="3241d-135">Pokud balíček se nepodařilo obnovit, chyba by měl být vytištěn v výstupu i s minimálním podrobností ON - [#5658](https://github.com/NuGet/Home/issues/5658)</span><span class="sxs-lookup"><span data-stu-id="3241d-135">If package failed to restore, error should be printed in the output even with Minimal verbosity ON - [#5658](https://github.com/NuGet/Home/issues/5658)</span></span>
- <span data-ttu-id="3241d-136">DotNet.</span><span class="sxs-lookup"><span data-stu-id="3241d-136">dotnet</span></span>
  - <span data-ttu-id="3241d-137">dotnetcore obnovení na úrovni řešení není podle ProjectReference s ReferenceOutputAssembly false úvodní náhodných sestavení chyby - [#5490](https://github.com/NuGet/Home/issues/5490)</span><span class="sxs-lookup"><span data-stu-id="3241d-137">dotnetcore restore at solution-level doesn't follow ProjectReference with ReferenceOutputAssembly of false leading to random build failures - [#5490](https://github.com/NuGet/Home/issues/5490)</span></span>
- <span data-ttu-id="3241d-138">Automatické dokončování v funguje pomocí PMC nesprávně pomocí metod objektu - [#4800](https://github.com/NuGet/Home/issues/4800)</span><span class="sxs-lookup"><span data-stu-id="3241d-138">Auto-complete in PMC works incorrectly with object methods - [#4800](https://github.com/NuGet/Home/issues/4800)</span></span>
- <span data-ttu-id="3241d-139">nuget.exe obnovení se nezdaří pomocí nástrojů Visual Studio 2015 - [#4713](https://github.com/NuGet/Home/issues/4713)</span><span class="sxs-lookup"><span data-stu-id="3241d-139">nuget.exe restore fails with Visual Studio 2015 toolset - [#4713](https://github.com/NuGet/Home/issues/4713)</span></span>
- <span data-ttu-id="3241d-140">výkonu - pomocí pmc je nákladné doložit v vs2017 - [#4205](https://github.com/NuGet/Home/issues/4205)</span><span class="sxs-lookup"><span data-stu-id="3241d-140">perf - pmc is expensive to instantiate in vs2017 - [#4205](https://github.com/NuGet/Home/issues/4205)</span></span>
- <span data-ttu-id="3241d-141">Pomalé získat informace o závislostech na pomalé připojení - [#4089](https://github.com/NuGet/Home/issues/4089)</span><span class="sxs-lookup"><span data-stu-id="3241d-141">Slow to get dependency information on slow connection - [#4089](https://github.com/NuGet/Home/issues/4089)</span></span>
- <span data-ttu-id="3241d-142">Odinstalace balíčku s - RemoveDependencies se nezdaří, pokud více balíčků sdílejí společné závislost - [#4026](https://github.com/NuGet/Home/issues/4026)</span><span class="sxs-lookup"><span data-stu-id="3241d-142">uninstall-package w/ -RemoveDependencies will fail if multiple packages share a common dependency - [#4026](https://github.com/NuGet/Home/issues/4026)</span></span>
- <span data-ttu-id="3241d-143">Dokončení NuGet.Core.nupkg pro publikování - [#3581](https://github.com/NuGet/Home/issues/3581)</span><span class="sxs-lookup"><span data-stu-id="3241d-143">Finalize NuGet.Core.nupkg for publishing - [#3581](https://github.com/NuGet/Home/issues/3581)</span></span>
- <span data-ttu-id="3241d-144">NuGet pack řeší ID závislost z název adresáře v případě - IncludeProjectReferences používá pro csproj + project.json - [#3566](https://github.com/NuGet/Home/issues/3566)</span><span class="sxs-lookup"><span data-stu-id="3241d-144">NuGet pack resolves dependency ID from directory name when -IncludeProjectReferences is used for csproj + project.json - [#3566](https://github.com/NuGet/Home/issues/3566)</span></span>
- <span data-ttu-id="3241d-145">Typ inicializátoru pro 'NuGet.ProxyCache' došlo k výjimce - [#3144](https://github.com/NuGet/Home/issues/3144)</span><span class="sxs-lookup"><span data-stu-id="3241d-145">The type initializer for 'NuGet.ProxyCache' threw an exception - [#3144](https://github.com/NuGet/Home/issues/3144)</span></span>
- <span data-ttu-id="3241d-146">nuget restore výkonu problém s kudu - [#3087](https://github.com/NuGet/Home/issues/3087)</span><span class="sxs-lookup"><span data-stu-id="3241d-146">nuget restore performance issue with kudu - [#3087](https://github.com/NuGet/Home/issues/3087)</span></span>
- <span data-ttu-id="3241d-147">Uživatelské rozhraní klienta nepodaří zobrazit všechny chyby nebo upozornění při hledání je před registrace objekty BLOB - [#2149](https://github.com/NuGet/Home/issues/2149)</span><span class="sxs-lookup"><span data-stu-id="3241d-147">UI Client fails to show any error or warning when search is ahead of registration blobs - [#2149](https://github.com/NuGet/Home/issues/2149)</span></span>
- <span data-ttu-id="3241d-148">-Aktualizace generuje dotaz nesprávný - Get-balíčky [#2135](https://github.com/NuGet/Home/issues/2135)</span><span class="sxs-lookup"><span data-stu-id="3241d-148">Get-Packages -Updates generates an incorrect query - [#2135](https://github.com/NuGet/Home/issues/2135)</span></span>

## <a name="links-to-github-issues-fixed-in-45-rtm"></a><span data-ttu-id="3241d-149">Odkazy na Githubu chyby v 4.5 RTM</span><span class="sxs-lookup"><span data-stu-id="3241d-149">Links to GitHub issues fixed in 4.5 RTM</span></span>

[<span data-ttu-id="3241d-150">Seznam problémů</span><span class="sxs-lookup"><span data-stu-id="3241d-150">Issues list</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)
