---
title: Zpráva k vydání verze NuGet 4.5 RTM
description: Zpráva k vydání verze pro NuGet 4.5 RTM, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: anangaur
ms.author: anangaur
ms.date: 12/4/2017
ms.topic: conceptual
ms.openlocfilehash: 01ecd8c7de1a0f713766e3c413d889038522bac7
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548293"
---
# <a name="nuget-45-rtm-release-notes"></a><span data-ttu-id="4919f-103">Zpráva k vydání verze NuGet 4.5 RTM</span><span class="sxs-lookup"><span data-stu-id="4919f-103">NuGet 4.5 RTM Release Notes</span></span>

<span data-ttu-id="4919f-104">[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) součástí [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="4919f-104">[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).</span></span>

## <a name="known-issues"></a><span data-ttu-id="4919f-105">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="4919f-105">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="4919f-106">Problémy s .NET Standard 2.0 pomocí rozhraní .NET Framework a NuGet</span><span class="sxs-lookup"><span data-stu-id="4919f-106">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="4919f-107">.NET standard a jeho nástroje je navržená tak, že projekty cílené na rozhraní .NET Framework 4.6.1 může spotřebovat balíčky NuGet & projekty cílené na .NET Standard 2.0 nebo dřívější.</span><span class="sxs-lookup"><span data-stu-id="4919f-107">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="4919f-108">[Tento dokument](https://github.com/dotnet/standard/issues/481) shrnuje problémy kolem tohoto scénáře plánu pro účely řešení a alternativní řešení můžete nasadit s dnešní stavu nástrojů.</span><span class="sxs-lookup"><span data-stu-id="4919f-108">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="4919f-109">Nejde zobrazit, přidat ani aktualizovat DotNetCLITools pomocí Správce balíčků Nuget</span><span class="sxs-lookup"><span data-stu-id="4919f-109">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="4919f-110">Problém</span><span class="sxs-lookup"><span data-stu-id="4919f-110">Issue</span></span>

<span data-ttu-id="4919f-111">Správce balíčků NuGet nezobrazuje a nepovoluje přidat nebo aktualizovat DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="4919f-111">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="4919f-112">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="4919f-112">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="4919f-113">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="4919f-113">Workaround</span></span>

<span data-ttu-id="4919f-114">V souboru projektu se musí ručně upravit DotNetCLIToolReferences.</span><span class="sxs-lookup"><span data-stu-id="4919f-114">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="4919f-115">Změna cílení cílové verze rozhraní může vést k nekompletnímu IntelliSense</span><span class="sxs-lookup"><span data-stu-id="4919f-115">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="4919f-116">Problém</span><span class="sxs-lookup"><span data-stu-id="4919f-116">Issue</span></span>

<span data-ttu-id="4919f-117">Změna cílení cílové verze rozhraní v sadě Visual Studio může vést k nekompletnímu IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="4919f-117">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="4919f-118">To se stává, když jako formát správce balíčků používáte PackageReferences.</span><span class="sxs-lookup"><span data-stu-id="4919f-118">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="4919f-119">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="4919f-119">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="4919f-120">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="4919f-120">Workaround</span></span>

<span data-ttu-id="4919f-121">Proveďte ruční obnovení.</span><span class="sxs-lookup"><span data-stu-id="4919f-121">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="4919f-122">Balíček v projektu .NET Core, který obsahuje sestavení s neplatným podpisem, může aktivovat nekonečnou smyčku obnovení</span><span class="sxs-lookup"><span data-stu-id="4919f-122">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="4919f-123">Problém</span><span class="sxs-lookup"><span data-stu-id="4919f-123">Issue</span></span>

<span data-ttu-id="4919f-124">V některých případech použijete balíček, který obsahuje sestavení s neplatným podpisem, nebo když se verze balíčku nastaví pomocí časovače "DateTime, může to způsobí, že automaticky – obnovení balíčku občas způsobit nekonečnou smyčku [dotnet/project-system #1457](https://github.com/dotnet/project-system/issues/1457).</span><span class="sxs-lookup"><span data-stu-id="4919f-124">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="4919f-125">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="4919f-125">Workaround</span></span>

<span data-ttu-id="4919f-126">Pro tento problém zatím neexistuje alternativní řešení.</span><span class="sxs-lookup"><span data-stu-id="4919f-126">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a><span data-ttu-id="4919f-127">Problémy opravené ve verzi RTM 4.5 NuGet časový rámec</span><span class="sxs-lookup"><span data-stu-id="4919f-127">Issues fixed in NuGet 4.5 RTM timeframe</span></span>

<span data-ttu-id="4919f-128">Problémy opravené ve verzi RTM 4.4 NuGet, najdete [4.4 RTM poznámkách k verzi NuGet](../release-notes/nuget-4.4-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="4919f-128">For issues fixed in NuGet 4.4 RTM, please refer to [NuGet 4.4 RTM Release Notes](../release-notes/nuget-4.4-RTM.md)</span></span> 

### <a name="features"></a><span data-ttu-id="4919f-129">Funkce</span><span class="sxs-lookup"><span data-stu-id="4919f-129">Features</span></span>

- <span data-ttu-id="4919f-130">Zakázat automatické nabízené oznámení balíčku symbolů - [#6113](https://github.com/NuGet/Home/issues/6113)</span><span class="sxs-lookup"><span data-stu-id="4919f-130">Disable auto-push of symbols package - [#6113](https://github.com/NuGet/Home/issues/6113)</span></span>

### <a name="bugs"></a><span data-ttu-id="4919f-131">Chyby</span><span class="sxs-lookup"><span data-stu-id="4919f-131">Bugs</span></span>

- <span data-ttu-id="4919f-132">[Regrese] v 15.5p1: Portable0.0 se přeskočila - [#6105](https://github.com/NuGet/Home/issues/6105)</span><span class="sxs-lookup"><span data-stu-id="4919f-132">[Regression] in 15.5p1: Portable0.0 is skipped - [#6105](https://github.com/NuGet/Home/issues/6105)</span></span>
- <span data-ttu-id="4919f-133">Po obnovení – chybí prostředky z balíčků [#5995](https://github.com/NuGet/Home/issues/5995)</span><span class="sxs-lookup"><span data-stu-id="4919f-133">Assets from packages are missing after restore - [#5995](https://github.com/NuGet/Home/issues/5995)</span></span>
- <span data-ttu-id="4919f-134">Poskytovatelé přihlašovacích údajů modulu plug-in, nebudou fungovat s identifikátory URI obsahující mezery – [#5982](https://github.com/NuGet/Home/issues/5982)</span><span class="sxs-lookup"><span data-stu-id="4919f-134">Plugin credential providers do not work with URIs containing spaces - [#5982](https://github.com/NuGet/Home/issues/5982)</span></span>
- <span data-ttu-id="4919f-135">Pokud balíček se nepovedlo obnovit, chyba by měl vytisknout ve výstupu i s minimální úroveň podrobností ON - [#5658](https://github.com/NuGet/Home/issues/5658)</span><span class="sxs-lookup"><span data-stu-id="4919f-135">If package failed to restore, error should be printed in the output even with Minimal verbosity ON - [#5658](https://github.com/NuGet/Home/issues/5658)</span></span>
- <span data-ttu-id="4919f-136">DotNet</span><span class="sxs-lookup"><span data-stu-id="4919f-136">dotnet</span></span>
  - <span data-ttu-id="4919f-137">dotnetcore obnovení na úrovni řešení není postupujte z ProjectReference s ReferenceOutputAssembly false nejlepší náhodné sestavení selhání - [#5490](https://github.com/NuGet/Home/issues/5490)</span><span class="sxs-lookup"><span data-stu-id="4919f-137">dotnetcore restore at solution-level doesn't follow ProjectReference with ReferenceOutputAssembly of false leading to random build failures - [#5490](https://github.com/NuGet/Home/issues/5490)</span></span>
- <span data-ttu-id="4919f-138">Automatické dokončování ve PMC funguje správně pomocí metody objektu - [#4800](https://github.com/NuGet/Home/issues/4800)</span><span class="sxs-lookup"><span data-stu-id="4919f-138">Auto-complete in PMC works incorrectly with object methods - [#4800](https://github.com/NuGet/Home/issues/4800)</span></span>
- <span data-ttu-id="4919f-139">nuget.exe obnovení se nezdaří pomocí nástrojů Visual Studio 2015 – [#4713](https://github.com/NuGet/Home/issues/4713)</span><span class="sxs-lookup"><span data-stu-id="4919f-139">nuget.exe restore fails with Visual Studio 2015 toolset - [#4713](https://github.com/NuGet/Home/issues/4713)</span></span>
- <span data-ttu-id="4919f-140">výkonu – pmc je náročné vytvořit instanci v vs2017 - [#4205](https://github.com/NuGet/Home/issues/4205)</span><span class="sxs-lookup"><span data-stu-id="4919f-140">perf - pmc is expensive to instantiate in vs2017 - [#4205](https://github.com/NuGet/Home/issues/4205)</span></span>
- <span data-ttu-id="4919f-141">Pomalá závislost informace o pomalé připojení - [#4089](https://github.com/NuGet/Home/issues/4089)</span><span class="sxs-lookup"><span data-stu-id="4919f-141">Slow to get dependency information on slow connection - [#4089](https://github.com/NuGet/Home/issues/4089)</span></span>
- <span data-ttu-id="4919f-142">odinstalovat balíček plánovaným bodem obnovení kratším - RemoveDependencies selže, pokud více balíčků sdílejí společné závislosti - [#4026](https://github.com/NuGet/Home/issues/4026)</span><span class="sxs-lookup"><span data-stu-id="4919f-142">uninstall-package w/ -RemoveDependencies will fail if multiple packages share a common dependency - [#4026](https://github.com/NuGet/Home/issues/4026)</span></span>
- <span data-ttu-id="4919f-143">Dokončení NuGet.Core.nupkg pro publikování – [#3581](https://github.com/NuGet/Home/issues/3581)</span><span class="sxs-lookup"><span data-stu-id="4919f-143">Finalize NuGet.Core.nupkg for publishing - [#3581](https://github.com/NuGet/Home/issues/3581)</span></span>
- <span data-ttu-id="4919f-144">Balíček NuGet řeší závislosti ID z názvu adresáře v případě - IncludeProjectReferences se používá pro csproj + project.json - [#3566](https://github.com/NuGet/Home/issues/3566)</span><span class="sxs-lookup"><span data-stu-id="4919f-144">NuGet pack resolves dependency ID from directory name when -IncludeProjectReferences is used for csproj + project.json - [#3566](https://github.com/NuGet/Home/issues/3566)</span></span>
- <span data-ttu-id="4919f-145">Inicializační metoda typu 'NuGet.ProxyCache' došlo k výjimce – [#3144](https://github.com/NuGet/Home/issues/3144)</span><span class="sxs-lookup"><span data-stu-id="4919f-145">The type initializer for 'NuGet.ProxyCache' threw an exception - [#3144](https://github.com/NuGet/Home/issues/3144)</span></span>
- <span data-ttu-id="4919f-146">problémy s výkonem obnovení nuget pomocí kudu - [#3087](https://github.com/NuGet/Home/issues/3087)</span><span class="sxs-lookup"><span data-stu-id="4919f-146">nuget restore performance issue with kudu - [#3087](https://github.com/NuGet/Home/issues/3087)</span></span>
- <span data-ttu-id="4919f-147">Uživatelské rozhraní klienta nepovede zobrazíte všechny chyby nebo upozornění při hledání náskok před registrací objekty BLOB – [#2149](https://github.com/NuGet/Home/issues/2149)</span><span class="sxs-lookup"><span data-stu-id="4919f-147">UI Client fails to show any error or warning when search is ahead of registration blobs - [#2149](https://github.com/NuGet/Home/issues/2149)</span></span>
- <span data-ttu-id="4919f-148">-Aktualizace generuje nesprávný - Get-Packages [#2135](https://github.com/NuGet/Home/issues/2135)</span><span class="sxs-lookup"><span data-stu-id="4919f-148">Get-Packages -Updates generates an incorrect query - [#2135](https://github.com/NuGet/Home/issues/2135)</span></span>

## <a name="links-to-github-issues-fixed-in-45-rtm"></a><span data-ttu-id="4919f-149">Odkazy na problémy Githubu Vyřešeno ve verzi 4.5 RTM</span><span class="sxs-lookup"><span data-stu-id="4919f-149">Links to GitHub issues fixed in 4.5 RTM</span></span>

[<span data-ttu-id="4919f-150">Seznam problémů</span><span class="sxs-lookup"><span data-stu-id="4919f-150">Issues list</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)
