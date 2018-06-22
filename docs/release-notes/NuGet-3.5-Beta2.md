---
title: 3.5 poznámky k verzi Beta2
description: Poznámky k verzi pro NuGet 3.5 Beta 2 včetně známé problémy, opravy chyb, přidaných funkcí a chcete.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 08bbae00a3e63c2a1ff42d5cc04981eb02966850
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822341"
---
# <a name="nuget-35-beta2-release-notes"></a><span data-ttu-id="a9f0e-103">Poznámky k verzi 3.5 Beta2 NuGet</span><span class="sxs-lookup"><span data-stu-id="a9f0e-103">NuGet 3.5 Beta2 Release Notes</span></span>

<span data-ttu-id="a9f0e-104">[Poznámky k verzi 3.5 Beta NuGet](../release-notes/nuget-3.5-Beta.md) | [poznámky k verzi 3.5 RC NuGet](../release-notes/nuget-3.5-RC.md)</span><span class="sxs-lookup"><span data-stu-id="a9f0e-104">[NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md)</span></span>

<span data-ttu-id="a9f0e-105">NuGet 3.5 Beta 2 RTM byla vydána 27. června 2016 pro Visual Studio 2013 a nuget.exe</span><span class="sxs-lookup"><span data-stu-id="a9f0e-105">NuGet 3.5 Beta 2 RTM was released June 27, 2016 for Visual Studio 2013 and nuget.exe</span></span>

[<span data-ttu-id="a9f0e-106">Úplné protokol změn</span><span class="sxs-lookup"><span data-stu-id="a9f0e-106">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[<span data-ttu-id="a9f0e-107">Seznam problémů</span><span class="sxs-lookup"><span data-stu-id="a9f0e-107">Issues List</span></span>](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a><span data-ttu-id="a9f0e-108">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="a9f0e-108">Bug Fixes</span></span>

* <span data-ttu-id="a9f0e-109">Aktualizované chybová zpráva k nedostatečná podpora pro decrpytion heslo v .NET Core pro ověřený kanály - [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="a9f0e-109">Updated error message to lack of support for password decrpytion in .NET Core for authenticated feeds  - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="a9f0e-110">Get-balíček konzoly Správce balíčků selže, pokud je projekt .NET Core open - [#2932](https://github.com/NuGet/Home/issues/2932)</span><span class="sxs-lookup"><span data-stu-id="a9f0e-110">Package Manager Console Get-Package fails if .NET Core project is open - [#2932](https://github.com/NuGet/Home/issues/2932)</span></span>

* <span data-ttu-id="a9f0e-111">Opravte nesprávné zpracování 403 v příkaz nabízené NuGet [#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="a9f0e-111">Fix incorrect handling of 403 in NuGet push command [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="a9f0e-112">Opravte problémy v odinstalaci balíčky v řešení vázána k řízení zdrojů TFS disableSourceControlIntegration nastavena na hodnotu true - [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="a9f0e-112">Fix issues in uninstalling packages in a solution bound to TFS source control when disableSourceControlIntegration is set to true - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="a9f0e-113">Opravte aktualizace balíčku provést do balíčků jiný cílový účet - [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="a9f0e-113">Fix package update to take into account non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="a9f0e-114">Pomocí nástroje MSBuild úroveň podrobností můžete nastavit úroveň protokolování pro správce balíčků Nuget akcí uživatelského rozhraní – [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="a9f0e-114">Use MSBuild verbosity level to set logger level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="a9f0e-115">Oprava NuGet konfigurace je neplatná Chyba v projektech web - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="a9f0e-115">Fix NuGet configuration is invalid error in WebSite projects - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="a9f0e-116">Vyřešte potíže s aktualizací Service pack z `.csproj` když soubory obsahu jsou zahrnuty - [#2658](https://github.com/NuGet/Home/issues/2658)</span><span class="sxs-lookup"><span data-stu-id="a9f0e-116">Fix pack issues from `.csproj` when content files are included - [#2658](https://github.com/NuGet/Home/issues/2658)</span></span>

* <span data-ttu-id="a9f0e-117">DefaultPushSource v `NuGetDefaults.Config` (`ProgramData\NuGet`) nefunguje - [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="a9f0e-117">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="a9f0e-118">Odstraňte problém na verze Nuget 3.4.3 - hodnota nemůže být null při vytváření balíčku - [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="a9f0e-118">Fix issue in Nuget 3.4.3 release - Value cannot be null on package creation - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="a9f0e-119">Obnovení používá uložené přihlašovací údaje ze souboru Nuget.Config pro informační kanály služby VSTS - [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="a9f0e-119">Restore uses stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="a9f0e-120">Výkon - nadměrné přidělení pro opravu v kódu porovnání verze - [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="a9f0e-120">Performance - Fix excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="a9f0e-121">Oprava problémů se více instancí nuget.exe pokusí nainstalovat stejného balíčku paralelně - [#2628](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="a9f0e-121">Fix issues when multiple instances of nuget.exe tries to install the same package in parallel - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="a9f0e-122">Výkon - mezipaměti informace o závislostech pro operace vícenásobného projektu - [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="a9f0e-122">Performance - Cache dependency information for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="a9f0e-123">Vyřešte problém tam, kde nejde zdroje balíčku přidat z nastavení, pokud je seznam zdrojů je prázdný - [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="a9f0e-123">Fix issue where package sources cannnot be added from settings when source list is empty - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="a9f0e-124">Opravte chybu Misleading při pokusu o instalaci balíčku, který závisí na průčelí návrhu - [#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="a9f0e-124">Fix Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="a9f0e-125">Instalace balíčku z konzoly PackageManager s nastavení "Všechny" pokusí pouze první zdroj - [#2557](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="a9f0e-125">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="a9f0e-126">Oprava problémů se balíčky, které mají soubory s časy zápisu v budoucnu (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="a9f0e-126">Fix issues with packages that have files with write times in the future (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="a9f0e-127">Zobrazit výjimky, když dojde k selhání s vyhledáním projekty v příkazu update - [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="a9f0e-127">Display exception when there is a failure finding projects in update command - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="a9f0e-128">Obsah balíčku není správně obnoveny při instalaci balíčku z v3.3 nuget + kanálu s argumentem - NoCache, když balíček obsahuje `.nupkg` soubory – [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="a9f0e-128">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="a9f0e-129">Opravte problém s balíčkem instalaci (všechny zdroje) 1 zdroji – chybí balíček [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="a9f0e-129">Fix issue with package install (All Sources) when package is missing from 1 source - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="a9f0e-130">Nainstalovat bloky v případě, že jednoho zdroje vyvolá chybu autorizace - [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="a9f0e-130">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="a9f0e-131">`.nuspec` verze rozsahu by měly přepsat verze - IncludeReferencedProjects - [#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="a9f0e-131">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="a9f0e-132">NuGet 3.3.0 aktualizace nezdaří s ' dodatečné omezení... definované v souboru packages.config téhle operaci brání. "</span><span class="sxs-lookup"><span data-stu-id="a9f0e-132">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="a9f0e-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="a9f0e-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="a9f0e-134">aktualizace nuget.exe zahodí silný název sestavení a privátní atributu.</span><span class="sxs-lookup"><span data-stu-id="a9f0e-134">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="a9f0e-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="a9f0e-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="a9f0e-136">Oprava problémů se relativní cesta k souboru pro "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="a9f0e-136">Fix issues with relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="a9f0e-137">Zlepšení zprávy o selhání překladač aktualizace - [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="a9f0e-137">Improve Update resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

## <a name="features-and-behavior-changes"></a><span data-ttu-id="a9f0e-138">Funkce a změny chování</span><span class="sxs-lookup"><span data-stu-id="a9f0e-138">Features and Behavior Changes</span></span>

* <span data-ttu-id="a9f0e-139">nuget.exe nabízené - parametr časového limitu nefunguje - [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="a9f0e-139">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="a9f0e-140">obnovení nuget.exe neobsahuje `.props` a `.targets` soubory pro `.nuproj` projekty (Regrese v v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="a9f0e-140">nuget.exe restore doesn't produce `.props` and `.targets` files for `.nuproj` projects (regression in v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="a9f0e-141">Třeba rozšiřitelnost rozhraní API k porovnání rozhraní s importovanými daty - [#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="a9f0e-141">Need extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="a9f0e-142">Skrýt možnosti závislostí při použití `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="a9f0e-142">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="a9f0e-143">Tiskové out hlavičkou verze nuget.exe podrobný výstup - [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="a9f0e-143">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="a9f0e-144">NuGet měli přidat podporu pro /nativeassets/ /runtimes/ {rid} {txm} / - [#2782](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="a9f0e-144">NuGet should add support for /runtimes/{rid}/nativeassets/{txm}/ - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>