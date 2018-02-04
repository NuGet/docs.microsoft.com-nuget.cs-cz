---
title: "3.5 poznámky k verzi Beta2 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Poznámky k verzi pro NuGet 3.5 Beta 2 včetně známé problémy, opravy chyb, přidaných funkcí a chcete."
keywords: "NuGet 3.5 Beta 2 poznámky k verzi, opravy chyb známé problémy, přidat funkce, chcete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4073b669c19f9e96ebd35ba269919b5f42313e7c
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-35-beta2-release-notes"></a><span data-ttu-id="fd7c7-104">Poznámky k verzi 3.5 Beta2 NuGet</span><span class="sxs-lookup"><span data-stu-id="fd7c7-104">NuGet 3.5 Beta2 Release Notes</span></span>

<span data-ttu-id="fd7c7-105">[Poznámky k verzi 3.5 Beta NuGet](../release-notes/nuget-3.5-Beta.md) | [poznámky k verzi 3.5 RC NuGet](../release-notes/nuget-3.5-RC.md)</span><span class="sxs-lookup"><span data-stu-id="fd7c7-105">[NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md)</span></span>

<span data-ttu-id="fd7c7-106">NuGet 3.5 Beta 2 RTM byla vydána 27. června 2016 pro Visual Studio 2013 a nuget.exe</span><span class="sxs-lookup"><span data-stu-id="fd7c7-106">NuGet 3.5 Beta 2 RTM was released June 27, 2016 for Visual Studio 2013 and nuget.exe</span></span>

[<span data-ttu-id="fd7c7-107">Úplné protokol změn</span><span class="sxs-lookup"><span data-stu-id="fd7c7-107">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[<span data-ttu-id="fd7c7-108">Seznam problémů</span><span class="sxs-lookup"><span data-stu-id="fd7c7-108">Issues List</span></span>](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a><span data-ttu-id="fd7c7-109">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="fd7c7-109">Bug Fixes</span></span>

* <span data-ttu-id="fd7c7-110">Aktualizované chybová zpráva k nedostatečná podpora pro decrpytion heslo v .NET Core pro ověřený kanály - [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="fd7c7-110">Updated error message to lack of support for password decrpytion in .NET Core for authenticated feeds  - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="fd7c7-111">Get-balíček konzoly Správce balíčků selže, pokud je projekt .NET Core open - [#2932](https://github.com/NuGet/Home/issues/2932)</span><span class="sxs-lookup"><span data-stu-id="fd7c7-111">Package Manager Console Get-Package fails if .NET Core project is open - [#2932](https://github.com/NuGet/Home/issues/2932)</span></span>

* <span data-ttu-id="fd7c7-112">Opravte nesprávné zpracování 403 v příkaz nabízené NuGet [#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="fd7c7-112">Fix incorrect handling of 403 in NuGet push command [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="fd7c7-113">Opravte problémy v odinstalaci balíčky v řešení vázána k řízení zdrojů TFS disableSourceControlIntegration nastavena na hodnotu true - [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="fd7c7-113">Fix issues in uninstalling packages in a solution bound to TFS source control when disableSourceControlIntegration is set to true - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="fd7c7-114">Opravte aktualizace balíčku provést do balíčků jiný cílový účet - [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="fd7c7-114">Fix package update to take into account non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="fd7c7-115">Pomocí nástroje MSBuild úroveň podrobností můžete nastavit úroveň protokolování pro správce balíčků Nuget akcí uživatelského rozhraní – [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="fd7c7-115">Use MSBuild verbosity level to set logger level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="fd7c7-116">Oprava NuGet konfigurace je neplatná Chyba v projektech web - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="fd7c7-116">Fix NuGet configuration is invalid error in WebSite projects - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="fd7c7-117">Vyřešte potíže s aktualizací Service pack z `.csproj` když soubory obsahu jsou zahrnuty - [#2658](https://github.com/NuGet/Home/issues/2658)</span><span class="sxs-lookup"><span data-stu-id="fd7c7-117">Fix pack issues from `.csproj` when content files are included - [#2658](https://github.com/NuGet/Home/issues/2658)</span></span>

* <span data-ttu-id="fd7c7-118">DefaultPushSource v `NuGetDefaults.Config` (`ProgramData\NuGet`) nefunguje - [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="fd7c7-118">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="fd7c7-119">Odstraňte problém na verze Nuget 3.4.3 - hodnota nemůže být null při vytváření balíčku - [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="fd7c7-119">Fix issue in Nuget 3.4.3 release - Value cannot be null on package creation - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="fd7c7-120">Obnovení používá uložené přihlašovací údaje ze souboru Nuget.Config pro informační kanály služby VSTS - [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="fd7c7-120">Restore uses stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="fd7c7-121">Výkon - nadměrné přidělení pro opravu v kódu porovnání verze - [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="fd7c7-121">Performance - Fix excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="fd7c7-122">Oprava problémů se více instancí nuget.exe pokusí nainstalovat stejného balíčku paralelně - [#2628](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="fd7c7-122">Fix issues when multiple instances of nuget.exe tries to install the same package in parallel - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="fd7c7-123">Výkon - mezipaměti informace o závislostech pro operace vícenásobného projektu - [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="fd7c7-123">Performance - Cache dependency information for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="fd7c7-124">Vyřešte problém tam, kde nejde zdroje balíčku přidat z nastavení, pokud je seznam zdrojů je prázdný - [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="fd7c7-124">Fix issue where package sources cannnot be added from settings when source list is empty - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="fd7c7-125">Opravte chybu Misleading při pokusu o instalaci balíčku, který závisí na průčelí návrhu - [#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="fd7c7-125">Fix Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="fd7c7-126">Instalace balíčku z konzoly PackageManager s nastavení "Všechny" pokusí pouze první zdroj - [#2557](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="fd7c7-126">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="fd7c7-127">Oprava problémů se balíčky, které mají soubory s časy zápisu v budoucnu (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="fd7c7-127">Fix issues with packages that have files with write times in the future (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="fd7c7-128">Zobrazit výjimky, když dojde k selhání s vyhledáním projekty v příkazu update - [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="fd7c7-128">Display exception when there is a failure finding projects in update command - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="fd7c7-129">Obsah balíčku není správně obnoveny při instalaci balíčku z v3.3 nuget + kanálu s argumentem - NoCache, když balíček obsahuje `.nupkg` soubory – [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="fd7c7-129">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="fd7c7-130">Opravte problém s balíčkem instalaci (všechny zdroje) 1 zdroji – chybí balíček [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="fd7c7-130">Fix issue with package install (All Sources) when package is missing from 1 source - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="fd7c7-131">Nainstalovat bloky v případě, že jednoho zdroje vyvolá chybu autorizace - [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="fd7c7-131">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="fd7c7-132">`.nuspec`verze rozsahu by měly přepsat verze - IncludeReferencedProjects - [#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="fd7c7-132">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="fd7c7-133">NuGet 3.3.0 aktualizace nezdaří s ' dodatečné omezení... definované v souboru packages.config téhle operaci brání. "</span><span class="sxs-lookup"><span data-stu-id="fd7c7-133">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="fd7c7-134"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="fd7c7-134"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="fd7c7-135">aktualizace nuget.exe zahodí silný název sestavení a privátní atributu.</span><span class="sxs-lookup"><span data-stu-id="fd7c7-135">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="fd7c7-136"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="fd7c7-136"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="fd7c7-137">Oprava problémů se relativní cesta k souboru pro "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="fd7c7-137">Fix issues with relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="fd7c7-138">Zlepšení zprávy o selhání překladač aktualizace - [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="fd7c7-138">Improve Update resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

## <a name="features-and-behavior-changes"></a><span data-ttu-id="fd7c7-139">Funkce a změny chování</span><span class="sxs-lookup"><span data-stu-id="fd7c7-139">Features and Behavior Changes</span></span>

* <span data-ttu-id="fd7c7-140">nuget.exe nabízené - parametr časového limitu nefunguje - [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="fd7c7-140">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="fd7c7-141">obnovení nuget.exe neobsahuje `.props` a `.targets` soubory pro `.nuproj` projekty (Regrese v v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="fd7c7-141">nuget.exe restore doesn't produce `.props` and `.targets` files for `.nuproj` projects (regression in v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="fd7c7-142">Třeba rozšiřitelnost rozhraní API k porovnání rozhraní s importovanými daty - [#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="fd7c7-142">Need extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="fd7c7-143">Skrýt možnosti závislostí při použití `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="fd7c7-143">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="fd7c7-144">Tiskové out hlavičkou verze nuget.exe podrobný výstup - [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="fd7c7-144">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="fd7c7-145">NuGet měli přidat podporu pro /nativeassets/ /runtimes/ {rid} {txm} / - [#2782](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="fd7c7-145">NuGet should add support for /runtimes/{rid}/nativeassets/{txm}/ - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>