---
title: 3.5 zpráva k vydání verze Beta2
description: Zpráva k vydání verze NuGet 3.5 Beta 2, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4b47939e2fafc11823c41a849b3c58bbf0800ada
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551988"
---
# <a name="nuget-35-beta2-release-notes"></a><span data-ttu-id="c06c8-103">Zpráva k vydání verze NuGet 3.5 Beta2</span><span class="sxs-lookup"><span data-stu-id="c06c8-103">NuGet 3.5 Beta2 Release Notes</span></span>

<span data-ttu-id="c06c8-104">[Poznámky k verzi 3.5 Beta verze NuGet](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5 RC poznámky](../release-notes/nuget-3.5-RC.md)</span><span class="sxs-lookup"><span data-stu-id="c06c8-104">[NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md)</span></span>

<span data-ttu-id="c06c8-105">NuGet 3.5 Beta 2 RTM bylo vydáno 27. června 2016 pro Visual Studio 2013 a nuget.exe</span><span class="sxs-lookup"><span data-stu-id="c06c8-105">NuGet 3.5 Beta 2 RTM was released June 27, 2016 for Visual Studio 2013 and nuget.exe</span></span>

[<span data-ttu-id="c06c8-106">Úplný protokol změn</span><span class="sxs-lookup"><span data-stu-id="c06c8-106">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[<span data-ttu-id="c06c8-107">Seznam problémů</span><span class="sxs-lookup"><span data-stu-id="c06c8-107">Issues List</span></span>](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a><span data-ttu-id="c06c8-108">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="c06c8-108">Bug Fixes</span></span>

* <span data-ttu-id="c06c8-109">Aktualizované chybové zprávy chybějící podpora jazyků decrpytion heslo v .NET Core pro ověřené informační kanály - [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="c06c8-109">Updated error message to lack of support for password decrpytion in .NET Core for authenticated feeds  - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="c06c8-110">Konzola správce balíčků Get-balíčku selže, pokud projekt .NET Core je open - [#2932](https://github.com/NuGet/Home/issues/2932)</span><span class="sxs-lookup"><span data-stu-id="c06c8-110">Package Manager Console Get-Package fails if .NET Core project is open - [#2932](https://github.com/NuGet/Home/issues/2932)</span></span>

* <span data-ttu-id="c06c8-111">Opravte nesprávné zpracování 403 v příkazu push NuGet [#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="c06c8-111">Fix incorrect handling of 403 in NuGet push command [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="c06c8-112">Opravte problémy v odinstalaci balíčky v řešení připojit ke správě zdrojů TFS při disableSourceControlIntegration je nastavena na hodnotu true - [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="c06c8-112">Fix issues in uninstalling packages in a solution bound to TFS source control when disableSourceControlIntegration is set to true - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="c06c8-113">Oprava aktualizace balíčku bude trvat do balíčků bez cílového účtu – [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="c06c8-113">Fix package update to take into account non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="c06c8-114">Pomocí nástroje MSBuild s úrovní podrobností můžete nastavit úroveň protokolování pro správce balíčků Nuget akce uživatelského rozhraní – [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="c06c8-114">Use MSBuild verbosity level to set logger level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="c06c8-115">Oprava NuGet konfigurace je neplatná chyby v projektech web - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="c06c8-115">Fix NuGet configuration is invalid error in WebSite projects - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="c06c8-116">Opravte problémy s aktualizací Service pack z `.csproj` když soubory obsahu jsou zahrnuty - [#2658](https://github.com/NuGet/Home/issues/2658)</span><span class="sxs-lookup"><span data-stu-id="c06c8-116">Fix pack issues from `.csproj` when content files are included - [#2658](https://github.com/NuGet/Home/issues/2658)</span></span>

* <span data-ttu-id="c06c8-117">DefaultPushSource v `NuGetDefaults.Config` (`ProgramData\NuGet`) nefunguje - [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="c06c8-117">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="c06c8-118">Odstraňte problém na vydání Nuget 3.4.3 - hodnota nemůže být null při vytváření balíčku - [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="c06c8-118">Fix issue in Nuget 3.4.3 release - Value cannot be null on package creation - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="c06c8-119">Obnovení používá uložené přihlašovací údaje ze souboru Nuget.Config pro informační kanály VSTS - [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="c06c8-119">Restore uses stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="c06c8-120">Výkon - nadměrného přidělení pro opravu v porovnání kód verze - [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="c06c8-120">Performance - Fix excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="c06c8-121">Řešení problémů, pokud více instancí nuget.exe pokusí nainstalovat stejného balíčku paralelně - [#2628](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="c06c8-121">Fix issues when multiple instances of nuget.exe tries to install the same package in parallel - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="c06c8-122">Výkon - mezipaměť informací o závislostech pro operace více projektů - [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="c06c8-122">Performance - Cache dependency information for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="c06c8-123">Tento problém vyřešit tam, kde balíček zdrojů nelze přidat z nastavení, pokud seznam zdrojů je prázdný - [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="c06c8-123">Fix issue where package sources cannnot be added from settings when source list is empty - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="c06c8-124">Opravte chybu Misleading při pokusu o instalaci balíčku, který závisí na návrhu fasády - [#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="c06c8-124">Fix Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="c06c8-125">Instalace balíčku z konzoly PackageManager s nastavením "All" pokusí pouze první zdroj - [#2557](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="c06c8-125">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="c06c8-126">Řešení problémů s balíčky, které mají soubory s časem zápisu v budoucnu (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="c06c8-126">Fix issues with packages that have files with write times in the future (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="c06c8-127">Zobrazit výjimky, když dojde k selhání vyhledávání projektů v příkazu update - [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="c06c8-127">Display exception when there is a failure finding projects in update command - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="c06c8-128">Balíček obsahu není správně obnovena, při instalaci balíčku z nuget v3.3 + informačního kanálu s argumentem - NoCache, když balíček obsahuje `.nupkg` soubory – [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="c06c8-128">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="c06c8-129">Oprava potíží s balíček nainstalovat (všechny zdroje), když ze zdroje 1 - chybí balíček [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="c06c8-129">Fix issue with package install (All Sources) when package is missing from 1 source - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="c06c8-130">Nainstalovat bloky, pokud je jediným zdrojem selhání autorizace – [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="c06c8-130">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="c06c8-131">`.nuspec` verze rozsah by měl přepsat - IncludeReferencedProjects verze - [#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="c06c8-131">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="c06c8-132">Aktualizace NuGet 3.3.0 selže s '... Další omezení definované v souboru packages.config téhle operaci brání. "</span><span class="sxs-lookup"><span data-stu-id="c06c8-132">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="c06c8-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="c06c8-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="c06c8-134">aktualizace nuget.exe zahodí silný název sestavení a privátní atribut.</span><span class="sxs-lookup"><span data-stu-id="c06c8-134">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="c06c8-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="c06c8-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="c06c8-136">Oprava problémů se relativní cesta k souboru pro "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="c06c8-136">Fix issues with relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="c06c8-137">Zlepšení zprávy o neúspěchu překladač Update - [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="c06c8-137">Improve Update resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

## <a name="features-and-behavior-changes"></a><span data-ttu-id="c06c8-138">Funkce a změny chování</span><span class="sxs-lookup"><span data-stu-id="c06c8-138">Features and Behavior Changes</span></span>

* <span data-ttu-id="c06c8-139">nabízené nuget.exe – parametr časového limitu nefunguje - [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="c06c8-139">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="c06c8-140">obnovení nuget.exe nevytvoří `.props` a `.targets` soubory pro `.nuproj` projekty (Regrese v v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="c06c8-140">nuget.exe restore doesn't produce `.props` and `.targets` files for `.nuproj` projects (regression in v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="c06c8-141">Třeba rozšíření rozhraní API pro porovnání architektur s importovanými daty – [#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="c06c8-141">Need extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="c06c8-142">Skrýt možnosti závislostí při použití `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="c06c8-142">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="c06c8-143">Vytiskne nuget.exe verze záhlaví podrobný výstup - [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="c06c8-143">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="c06c8-144">NuGet by měl přidat podporu pro /nativeassets/ /runtimes/ {identifikátorů rid} {txm} / – [#2782](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="c06c8-144">NuGet should add support for /runtimes/{rid}/nativeassets/{txm}/ - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>