---
title: zpráva k vydání verze 3,5 beta2
description: Poznámky k verzi pro NuGet 3,5 beta 2, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 2aa92d4ef97acb2b4b70388cd4d580e7094aea45
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776391"
---
# <a name="nuget-35-beta2-release-notes"></a><span data-ttu-id="4e0b1-103">Poznámky k verzi NuGet 3,5 beta2</span><span class="sxs-lookup"><span data-stu-id="4e0b1-103">NuGet 3.5 Beta2 Release Notes</span></span>

<span data-ttu-id="4e0b1-104">[NuGet 3,5 – poznámky](../release-notes/nuget-3.5-Beta.md)  |  k verzi beta [Poznámky k verzi pro NuGet 3,5 – RC](../release-notes/nuget-3.5-RC.md)</span><span class="sxs-lookup"><span data-stu-id="4e0b1-104">[NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md)</span></span>

<span data-ttu-id="4e0b1-105">NuGet 3,5 beta 2 RTM byl vydán 27. června 2016 pro Visual Studio 2013 a nuget.exe</span><span class="sxs-lookup"><span data-stu-id="4e0b1-105">NuGet 3.5 Beta 2 RTM was released June 27, 2016 for Visual Studio 2013 and nuget.exe</span></span>

[<span data-ttu-id="4e0b1-106">Úplný protokol změn</span><span class="sxs-lookup"><span data-stu-id="4e0b1-106">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[<span data-ttu-id="4e0b1-107">Seznam problémů</span><span class="sxs-lookup"><span data-stu-id="4e0b1-107">Issues List</span></span>](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a><span data-ttu-id="4e0b1-108">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="4e0b1-108">Bug Fixes</span></span>

* <span data-ttu-id="4e0b1-109">Aktualizovaná chybová zpráva pro nedostatečné podpoře pro decrpytion hesla v .NET Core pro ověřené informační kanály – [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="4e0b1-109">Updated error message to lack of support for password decrpytion in .NET Core for authenticated feeds  - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="4e0b1-110">Konzola správce balíčků Get-Package se nezdařila, pokud je projekt .NET Core otevřený – [#2932](https://github.com/NuGet/Home/issues/2932)</span><span class="sxs-lookup"><span data-stu-id="4e0b1-110">Package Manager Console Get-Package fails if .NET Core project is open - [#2932](https://github.com/NuGet/Home/issues/2932)</span></span>

* <span data-ttu-id="4e0b1-111">Opravte nesprávné zpracování 403 v příkazu NuGet push Command [#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="4e0b1-111">Fix incorrect handling of 403 in NuGet push command [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="4e0b1-112">Opravte problémy při odinstalaci balíčků v řešení, které je vázané na správu zdrojového kódu TFS, pokud je disableSourceControlIntegration nastavené na true – [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="4e0b1-112">Fix issues in uninstalling packages in a solution bound to TFS source control when disableSourceControlIntegration is set to true - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="4e0b1-113">Oprava aktualizace balíčku pro zohlednění necílových balíčků – [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="4e0b1-113">Fix package update to take into account non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="4e0b1-114">Použití úrovně podrobností MSBuild k nastavení úrovně protokolovacího nástroje pro akce uživatelského rozhraní Správce balíčků NuGet – [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="4e0b1-114">Use MSBuild verbosity level to set logger level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="4e0b1-115">Oprava konfigurace NuGet je neplatná chyba v projektech webů – VS 2015 VSIX (v 3.4.3) – [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="4e0b1-115">Fix NuGet configuration is invalid error in WebSite projects - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="4e0b1-116">Oprava problémů s balíčkem `.csproj` Při zahrnutí souborů obsahu – [#2658](https://github.com/NuGet/Home/issues/2658)</span><span class="sxs-lookup"><span data-stu-id="4e0b1-116">Fix pack issues from `.csproj` when content files are included - [#2658](https://github.com/NuGet/Home/issues/2658)</span></span>

* <span data-ttu-id="4e0b1-117">DefaultPushSource in `NuGetDefaults.Config` ( `ProgramData\NuGet` ) nefunguje [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="4e0b1-117">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="4e0b1-118">Oprava problému v 3.4.3 vydaných verzí NuGet nemůže mít při vytváření balíčku hodnotu null – [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="4e0b1-118">Fix issue in Nuget 3.4.3 release - Value cannot be null on package creation - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="4e0b1-119">Příkaz Restore používá uložená pověření Nuget.Config pro informační kanály VSTS- [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="4e0b1-119">Restore uses stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="4e0b1-120">Výkon – oprava nadměrných přidělení ve verzi comparsion Code- [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="4e0b1-120">Performance - Fix excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="4e0b1-121">Oprava problémů, když se více instancí nuget.exe pokusí nainstalovat stejný balíček paralelně [#2628](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="4e0b1-121">Fix issues when multiple instances of nuget.exe tries to install the same package in parallel - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="4e0b1-122">Informace o závislostech v mezipaměti výkonu pro operace s více projekty – [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="4e0b1-122">Performance - Cache dependency information for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="4e0b1-123">Oprava potíží, kdy se zdroje balíčků nejde do nastavení, když je zdrojový seznam prázdný – [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="4e0b1-123">Fix issue where package sources cannnot be added from settings when source list is empty - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="4e0b1-124">Oprava zavádějící chyby při pokusu o instalaci balíčku, který závisí na době návrhu Facade- [#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="4e0b1-124">Fix Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="4e0b1-125">Instalace balíčku z konzoly PackageManager s nastavením "vše" se snaží pouze první zdroj – [#2557](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="4e0b1-125">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="4e0b1-126">Opravte problémy s balíčky, které mají soubory s časem zápisu v budoucnosti (mono) – [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="4e0b1-126">Fix issues with packages that have files with write times in the future (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="4e0b1-127">Zobrazit výjimku, pokud dojde k selhání při hledání projektů v příkazu Update- [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="4e0b1-127">Display exception when there is a failure finding projects in update command - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="4e0b1-128">Obsah balíčku se neobnovil správně při instalaci balíčku z kanálu NuGet v 3.3 + s argumentem-bez mezipaměti, když balíček obsahuje `.nupkg` soubory – [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="4e0b1-128">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="4e0b1-129">Oprava potíží při instalaci balíčku (všechny zdroje), když chybí balíček v 1 zdroji – [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="4e0b1-129">Fix issue with package install (All Sources) when package is missing from 1 source - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="4e0b1-130">Nainstalovat bloky v případě neúspěšného ověření u jednoho zdroje – [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="4e0b1-130">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="4e0b1-131">`.nuspec` Rozsah verze by měl přepsat-IncludeReferencedProjects verze- [#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="4e0b1-131">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="4e0b1-132">Aktualizace NuGet 3.3.0 se nezdařila s dodatečným omezením... definované v packages.config zabrání této operaci. '</span><span class="sxs-lookup"><span data-stu-id="4e0b1-132">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="4e0b1-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="4e0b1-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="4e0b1-134">nuget.exe Update zruší silný název sestavení a soukromý atribut.</span><span class="sxs-lookup"><span data-stu-id="4e0b1-134">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="4e0b1-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="4e0b1-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="4e0b1-136">Opravte problémy s relativní cestou k souboru pro "DefaultPushSource". [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="4e0b1-136">Fix issues with relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="4e0b1-137">Vylepšit zprávy o chybách překladače aktualizace – [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="4e0b1-137">Improve Update resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

## <a name="features-and-behavior-changes"></a><span data-ttu-id="4e0b1-138">Změny funkcí a chování</span><span class="sxs-lookup"><span data-stu-id="4e0b1-138">Features and Behavior Changes</span></span>

* <span data-ttu-id="4e0b1-139">Parametr push-timeout nuget.exe nefunguje – [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="4e0b1-139">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="4e0b1-140">nuget.exe obnovení nevytváří `.props` a `.targets` soubory pro `.nuproj` projekty (regrese v v 3.4.3.855) – [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="4e0b1-140">nuget.exe restore doesn't produce `.props` and `.targets` files for `.nuproj` projects (regression in v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="4e0b1-141">Pro porovnání platforem s importy je nutné rozšiřující rozhraní API [#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="4e0b1-141">Need extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="4e0b1-142">Skrýt možnosti závislosti při použití `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="4e0b1-142">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="4e0b1-143">Vytisknout nuget.exe záhlaví verze v podrobném výstupu – [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="4e0b1-143">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="4e0b1-144">NuGet by měl přidat podporu pro/runtimes/{RID}/nativeassets/{TXM}/- [#2782](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="4e0b1-144">NuGet should add support for /runtimes/{rid}/nativeassets/{txm}/ - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>