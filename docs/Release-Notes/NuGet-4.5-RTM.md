---
title: Poznámky k verzi RTM NuGet 4.5 | Microsoft Docs
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 12/4/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Poznámky k verzi pro NuGet 4.5 RTM, včetně známé problémy, opravy chyb, přidaných funkcí a chcete.
keywords: NuGet 4.5 RTM poznámky k verzi, opravy chyb známé problémy, přidat funkce, chcete
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: dbde7256ed5526761107272792d7c7cdc324a3ef
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-45-rtm-release-notes"></a><span data-ttu-id="53373-104">Poznámky k verzi 4.5 RTM NuGet</span><span class="sxs-lookup"><span data-stu-id="53373-104">NuGet 4.5 RTM Release Notes</span></span>

<span data-ttu-id="53373-105">[Visual Studio 2017 15,5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) se dodává s [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="53373-105">[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).</span></span>

## <a name="known-issues"></a><span data-ttu-id="53373-106">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="53373-106">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="53373-107">Problémy s .NET standardní 2.0 pomocí rozhraní .NET Framework & NuGet</span><span class="sxs-lookup"><span data-stu-id="53373-107">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="53373-108">.NET standard & jeho nástrojů je navržené tak, aby projektech zacílených na rozhraní .NET Framework 4.6.1 může využívat balíčky NuGet & projektech zacílených na standardní rozhraní .NET 2.0 nebo dřívější.</span><span class="sxs-lookup"><span data-stu-id="53373-108">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="53373-109">[Tento dokument](https://github.com/dotnet/standard/issues/481) shrnuje problémy kolem tento scénář, plán pro adresování a alternativní řešení můžete nasadit s je aktuální stav nástrojů.</span><span class="sxs-lookup"><span data-stu-id="53373-109">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="53373-110">Nelze zobrazit, přidat nebo aktualizovat DotNetCLITools pomocí Správce balíčků Nuget</span><span class="sxs-lookup"><span data-stu-id="53373-110">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="53373-111">Problém</span><span class="sxs-lookup"><span data-stu-id="53373-111">Issue</span></span>

<span data-ttu-id="53373-112">Správce balíčků NuGet nezobrazuje a nepovoluje přidat nebo aktualizovat DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="53373-112">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="53373-113">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="53373-113">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="53373-114">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="53373-114">Workaround</span></span>

<span data-ttu-id="53373-115">V souboru projektu se musí ručně upravit DotNetCLIToolReferences.</span><span class="sxs-lookup"><span data-stu-id="53373-115">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="53373-116">Změna cílení cílové verze rozhraní může vést k nekompletnímu IntelliSense</span><span class="sxs-lookup"><span data-stu-id="53373-116">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="53373-117">Problém</span><span class="sxs-lookup"><span data-stu-id="53373-117">Issue</span></span>

<span data-ttu-id="53373-118">Změna cílení cílové verze rozhraní v sadě Visual Studio může vést k nekompletnímu IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="53373-118">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="53373-119">To se stává, když jako formát správce balíčků používáte PackageReferences.</span><span class="sxs-lookup"><span data-stu-id="53373-119">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="53373-120">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="53373-120">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="53373-121">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="53373-121">Workaround</span></span>

<span data-ttu-id="53373-122">Proveďte ruční obnovení.</span><span class="sxs-lookup"><span data-stu-id="53373-122">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="53373-123">Balíček v projektu .NET Core, který obsahuje sestavení s neplatným podpisem, může aktivovat nekonečnou smyčku obnovení</span><span class="sxs-lookup"><span data-stu-id="53373-123">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="53373-124">Problém</span><span class="sxs-lookup"><span data-stu-id="53373-124">Issue</span></span>

<span data-ttu-id="53373-125">V některých případech při použití balíček, který obsahuje sestavení s neplatným podpisem nebo pokud verze balíčku nastavena, DateTime, burzovní způsobuje, že auto obnovení balíčku ke spuštění v nekonečné smyčce [dotnet/projektu systému #1457](https://github.com/dotnet/project-system/issues/1457).</span><span class="sxs-lookup"><span data-stu-id="53373-125">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="53373-126">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="53373-126">Workaround</span></span>

<span data-ttu-id="53373-127">Pro tento problém zatím neexistuje alternativní řešení.</span><span class="sxs-lookup"><span data-stu-id="53373-127">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a><span data-ttu-id="53373-128">Chyby v období NuGet 4.5 RTM</span><span class="sxs-lookup"><span data-stu-id="53373-128">Issues fixed in NuGet 4.5 RTM timeframe</span></span>

<span data-ttu-id="53373-129">Chyby v NuGet 4.4 RTM, naleznete v [NuGet 4.4 RTM poznámky](../release-notes/nuget-4.4-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="53373-129">For issues fixed in NuGet 4.4 RTM, please refer to [NuGet 4.4 RTM Release Notes](../release-notes/nuget-4.4-RTM.md)</span></span> 

### <a name="features"></a><span data-ttu-id="53373-130">Funkce</span><span class="sxs-lookup"><span data-stu-id="53373-130">Features</span></span>

- <span data-ttu-id="53373-131">Zakázat automatické nabízené symboly balíčku - [#6113](https://github.com/NuGet/Home/issues/6113)</span><span class="sxs-lookup"><span data-stu-id="53373-131">Disable auto-push of symbols package - [#6113](https://github.com/NuGet/Home/issues/6113)</span></span>

### <a name="bugs"></a><span data-ttu-id="53373-132">Chyby</span><span class="sxs-lookup"><span data-stu-id="53373-132">Bugs</span></span>

- <span data-ttu-id="53373-133">[Regrese] v 15.5p1: bylo přeskočeno Portable0.0 - [#6105](https://github.com/NuGet/Home/issues/6105)</span><span class="sxs-lookup"><span data-stu-id="53373-133">[Regression] in 15.5p1: Portable0.0 is skipped - [#6105](https://github.com/NuGet/Home/issues/6105)</span></span>
- <span data-ttu-id="53373-134">Po obnovení – chybí prostředky z balíčků [#5995](https://github.com/NuGet/Home/issues/5995)</span><span class="sxs-lookup"><span data-stu-id="53373-134">Assets from packages are missing after restore - [#5995](https://github.com/NuGet/Home/issues/5995)</span></span>
- <span data-ttu-id="53373-135">Poskytovatelé přihlašovacích údajů modulu plug-in nefungují s identifikátory URI obsahující mezery - [#5982](https://github.com/NuGet/Home/issues/5982)</span><span class="sxs-lookup"><span data-stu-id="53373-135">Plugin credential providers do not work with URIs containing spaces - [#5982](https://github.com/NuGet/Home/issues/5982)</span></span>
- <span data-ttu-id="53373-136">Pokud balíček se nepodařilo obnovit, chyba by měl být vytištěn v výstupu i s minimálním podrobností ON - [#5658](https://github.com/NuGet/Home/issues/5658)</span><span class="sxs-lookup"><span data-stu-id="53373-136">If package failed to restore, error should be printed in the output even with Minimal verbosity ON - [#5658](https://github.com/NuGet/Home/issues/5658)</span></span>
- <span data-ttu-id="53373-137">DotNet. obnovení na úrovni řešení není podle ProjectReference s ReferenceOutputAssembly false úvodní náhodných sestavení chyby - [#5490](https://github.com/NuGet/Home/issues/5490)</span><span class="sxs-lookup"><span data-stu-id="53373-137">dotnet restore at solution-level doesn't follow ProjectReference with ReferenceOutputAssembly of false leading to random build failures - [#5490](https://github.com/NuGet/Home/issues/5490)</span></span>
- <span data-ttu-id="53373-138">Automatické dokončování v funguje pomocí PMC nesprávně pomocí metod objektu - [#4800](https://github.com/NuGet/Home/issues/4800)</span><span class="sxs-lookup"><span data-stu-id="53373-138">Auto-complete in PMC works incorrectly with object methods - [#4800](https://github.com/NuGet/Home/issues/4800)</span></span>
- <span data-ttu-id="53373-139">nuget.exe obnovení se nezdaří pomocí nástrojů Visual Studio 2015 - [#4713](https://github.com/NuGet/Home/issues/4713)</span><span class="sxs-lookup"><span data-stu-id="53373-139">nuget.exe restore fails with Visual Studio 2015 toolset - [#4713](https://github.com/NuGet/Home/issues/4713)</span></span>
- <span data-ttu-id="53373-140">výkonu - pomocí pmc je nákladné doložit v vs2017 - [#4205](https://github.com/NuGet/Home/issues/4205)</span><span class="sxs-lookup"><span data-stu-id="53373-140">perf - pmc is expensive to instantiate in vs2017 - [#4205](https://github.com/NuGet/Home/issues/4205)</span></span>
- <span data-ttu-id="53373-141">Pomalé získat informace o závislostech na pomalé připojení - [#4089](https://github.com/NuGet/Home/issues/4089)</span><span class="sxs-lookup"><span data-stu-id="53373-141">Slow to get dependency information on slow connection - [#4089](https://github.com/NuGet/Home/issues/4089)</span></span>
- <span data-ttu-id="53373-142">Odinstalace balíčku s - RemoveDependencies se nezdaří, pokud více balíčků sdílejí společné závislost - [#4026](https://github.com/NuGet/Home/issues/4026)</span><span class="sxs-lookup"><span data-stu-id="53373-142">uninstall-package w/ -RemoveDependencies will fail if multiple packages share a common dependency - [#4026](https://github.com/NuGet/Home/issues/4026)</span></span>
- <span data-ttu-id="53373-143">Dokončení NuGet.Core.nupkg pro publikování - [#3581](https://github.com/NuGet/Home/issues/3581)</span><span class="sxs-lookup"><span data-stu-id="53373-143">Finalize NuGet.Core.nupkg for publishing - [#3581](https://github.com/NuGet/Home/issues/3581)</span></span>
- <span data-ttu-id="53373-144">NuGet pack řeší ID závislost z název adresáře v případě - IncludeProjectReferences používá pro csproj + project.json - [#3566](https://github.com/NuGet/Home/issues/3566)</span><span class="sxs-lookup"><span data-stu-id="53373-144">NuGet pack resolves dependency ID from directory name when -IncludeProjectReferences is used for csproj + project.json - [#3566](https://github.com/NuGet/Home/issues/3566)</span></span>
- <span data-ttu-id="53373-145">Typ inicializátoru pro 'NuGet.ProxyCache' došlo k výjimce - [#3144](https://github.com/NuGet/Home/issues/3144)</span><span class="sxs-lookup"><span data-stu-id="53373-145">The type initializer for 'NuGet.ProxyCache' threw an exception - [#3144](https://github.com/NuGet/Home/issues/3144)</span></span>
- <span data-ttu-id="53373-146">nuget restore výkonu problém s kudu - [#3087](https://github.com/NuGet/Home/issues/3087)</span><span class="sxs-lookup"><span data-stu-id="53373-146">nuget restore performance issue with kudu - [#3087](https://github.com/NuGet/Home/issues/3087)</span></span>
- <span data-ttu-id="53373-147">Uživatelské rozhraní klienta nepodaří zobrazit všechny chyby nebo upozornění při hledání je před registrace objekty BLOB - [#2149](https://github.com/NuGet/Home/issues/2149)</span><span class="sxs-lookup"><span data-stu-id="53373-147">UI Client fails to show any error or warning when search is ahead of registration blobs - [#2149](https://github.com/NuGet/Home/issues/2149)</span></span>
- <span data-ttu-id="53373-148">-Aktualizace generuje dotaz nesprávný - Get-balíčky [#2135](https://github.com/NuGet/Home/issues/2135)</span><span class="sxs-lookup"><span data-stu-id="53373-148">Get-Packages -Updates generates an incorrect query - [#2135](https://github.com/NuGet/Home/issues/2135)</span></span>

## <a name="links-to-github-issues-fixed-in-45-rtm"></a><span data-ttu-id="53373-149">Odkazy na Githubu chyby v 4.5 RTM</span><span class="sxs-lookup"><span data-stu-id="53373-149">Links to GitHub issues fixed in 4.5 RTM</span></span>

[<span data-ttu-id="53373-150">Seznam problémů</span><span class="sxs-lookup"><span data-stu-id="53373-150">Issues list</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)
