---
title: Zpráva k vydání verze NuGet 5,5
description: Poznámky k verzi pro NuGet 5,5, včetně nových funkcí, oprav chyb a chcete odeslat obecnou.
author: karann-msft
ms.author: karann
ms.date: 03/19/2020
ms.topic: conceptual
ms.openlocfilehash: 0e8ab66c937058e84420bc3e3a5031cbc133aad7
ms.sourcegitcommit: 1a63a84da2719c8141823ac89a20bf507fd22b00
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/24/2020
ms.locfileid: "80148295"
---
# <a name="nuget-55-release-notes"></a><span data-ttu-id="2ddd0-103">Zpráva k vydání verze NuGet 5,5</span><span class="sxs-lookup"><span data-stu-id="2ddd0-103">NuGet 5.5 Release Notes</span></span>

<span data-ttu-id="2ddd0-104">Prostředky pro distribuci NuGet:</span><span class="sxs-lookup"><span data-stu-id="2ddd0-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="2ddd0-105">Verze NuGet</span><span class="sxs-lookup"><span data-stu-id="2ddd0-105">NuGet version</span></span> | <span data-ttu-id="2ddd0-106">K dispozici ve verzi sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2ddd0-106">Available in Visual Studio version</span></span>| <span data-ttu-id="2ddd0-107">K dispozici v sadě .NET SDK</span><span class="sxs-lookup"><span data-stu-id="2ddd0-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="2ddd0-108">**5.5.0**</span><span class="sxs-lookup"><span data-stu-id="2ddd0-108">**5.5.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="2ddd0-109">Visual Studio 2019 verze 16,5</span><span class="sxs-lookup"><span data-stu-id="2ddd0-109">Visual Studio 2019 version 16.5</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="2ddd0-110">[3.1.200](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="2ddd0-110">[3.1.200](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="2ddd0-111"><sup>1</sup> Nainstalováno se sadou Visual Studio 2019 s úlohou .NET Core</span><span class="sxs-lookup"><span data-stu-id="2ddd0-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-55"></a><span data-ttu-id="2ddd0-112">Shrnutí: Novinky v 5,5</span><span class="sxs-lookup"><span data-stu-id="2ddd0-112">Summary: What's New in 5.5</span></span>

* <span data-ttu-id="2ddd0-113">Vylepšené možnosti usnadnění přístupu a čtečky obrazovky pro uživatelské rozhraní Správce balíčků NuGet v aplikaci Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2ddd0-113">Improved accessibility and screen reader experience for the NuGet package manager UI in Visual Studio</span></span>
    * <span data-ttu-id="2ddd0-114">Problémy s přístupností v prostředí čtečky obrazovky, chybějící altText a přístupný název pro nainstalované textové pole atd. [#9059](https://github.com/NuGet/Home/issues/9059)</span><span class="sxs-lookup"><span data-stu-id="2ddd0-114">Accessibility issues in Screen Reader experiences, missing altText and accessible name for Installed textbox, etc., - [#9059](https://github.com/NuGet/Home/issues/9059)</span></span>
    * <span data-ttu-id="2ddd0-115">Problémy s přístupností v prostředí čtečky obrazovky v seznamu balíčků – [#9077](https://github.com/NuGet/Home/issues/9077)</span><span class="sxs-lookup"><span data-stu-id="2ddd0-115">Accessibility issues in Screen Reader experiences in Packages List - [#9077](https://github.com/NuGet/Home/issues/9077)</span></span>
    * <span data-ttu-id="2ddd0-116">Problémy s přístupností v prostředí čtečky obrazovky související s kartami "Procházet", "instalace", "aktualizace" – [#9078](https://github.com/NuGet/Home/issues/9078)</span><span class="sxs-lookup"><span data-stu-id="2ddd0-116">Accessibility issues in Screen Reader experiences related to "browse","install","update" Tabs - [#9078](https://github.com/NuGet/Home/issues/9078)</span></span>
    * <span data-ttu-id="2ddd0-117">Narrator neoznamuje "prázdné", "No Dependencies", "NuGet. org", "MIT" popisek odkazu [#9157](https://github.com/NuGet/Home/issues/9157)</span><span class="sxs-lookup"><span data-stu-id="2ddd0-117">Narrator does not announce "Blank","No Dependencies","nuget.org","MIT" link label [#9157](https://github.com/NuGet/Home/issues/9157)</span></span>

* <span data-ttu-id="2ddd0-118">Podpora pro zpřístupnění samostatné ikony v uživatelském rozhraní Správce balíčků sady Visual Studio pro balíčky hostované v místních informačních kanálech – [#8189](https://github.com/NuGet/Home/issues/8189)</span><span class="sxs-lookup"><span data-stu-id="2ddd0-118">Support for surfacing self-contained icons in Visual Studio package manager UI for packages hosted on local feeds - [#8189](https://github.com/NuGet/Home/issues/8189)</span></span>

* <span data-ttu-id="2ddd0-119">Výrazně se zvýšil výkon při obnovení no-op pomocí `RestoreUseStaticGraphEvaluation`, které urychlují hodnocení voláním rozhraní API statického grafu nástroje MSBuild – [8791](https://github.com/NuGet/Home/issues/8791)</span><span class="sxs-lookup"><span data-stu-id="2ddd0-119">Significantly improved no-op restore performance using `RestoreUseStaticGraphEvaluation` which speeds up evaluations by calling MSBuild Static Graph APIs - [8791](https://github.com/NuGet/Home/issues/8791)</span></span>

* <span data-ttu-id="2ddd0-120">Vylepšená funkce dotnet. exe při ověřování pomocí modulů plug-in pro různé platformy</span><span class="sxs-lookup"><span data-stu-id="2ddd0-120">Improved dotnet.exe reliability with cross-platform authentication plugins</span></span>
    * <span data-ttu-id="2ddd0-121">selhání dotnet restore s TaskCanceledException- [#7842](https://github.com/NuGet/Home/issues/7842)</span><span class="sxs-lookup"><span data-stu-id="2ddd0-121">dotnet restore failing with TaskCanceledException - [#7842](https://github.com/NuGet/Home/issues/7842)</span></span>
    * <span data-ttu-id="2ddd0-122">Modul plug-in: úloha byla zrušena. došlo k problému s ověřováním ADO.</span><span class="sxs-lookup"><span data-stu-id="2ddd0-122">Plugin:  "A task was cancelled" - problem with ADO authentication due to this.</span></span><span data-ttu-id="2ddd0-123"> - [#8528](https://github.com/NuGet/Home/issues/8528)</span><span class="sxs-lookup"><span data-stu-id="2ddd0-123"> - [#8528](https://github.com/NuGet/Home/issues/8528)</span></span>

* <span data-ttu-id="2ddd0-124">Přidat `dotnet nuget <add|remove|update|disable|enable|list> source` příkaz- [#4126](https://github.com/NuGet/Home/issues/4126)</span><span class="sxs-lookup"><span data-stu-id="2ddd0-124">add `dotnet nuget <add|remove|update|disable|enable|list> source` command - [#4126](https://github.com/NuGet/Home/issues/4126)</span></span>

* <span data-ttu-id="2ddd0-125">Podpory for `--skip-duplicate` pomocí příkazu dotnet NuGet push- [#8778](https://github.com/NuGet/Home/issues/8778)</span><span class="sxs-lookup"><span data-stu-id="2ddd0-125">Suport for `--skip-duplicate`  using dotnet nuget push - [#8778](https://github.com/NuGet/Home/issues/8778)</span></span>

* <span data-ttu-id="2ddd0-126">Podpora `packages.config` s MSBuild/Restore – [#8506](https://github.com/NuGet/Home/issues/8506)</span><span class="sxs-lookup"><span data-stu-id="2ddd0-126">Support `packages.config` with msbuild /restore - [#8506](https://github.com/NuGet/Home/issues/8506)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="2ddd0-127">Chyby opravené v této verzi</span><span class="sxs-lookup"><span data-stu-id="2ddd0-127">Issues fixed in this release</span></span>

<span data-ttu-id="2ddd0-128">**Štěnic**</span><span class="sxs-lookup"><span data-stu-id="2ddd0-128">**Bugs**</span></span>

* <span data-ttu-id="2ddd0-129">Opětovné fungování samoobslužné aktualizace s rozhraními API V3- [#4197](https://github.com/NuGet/Home/issues/4197)</span><span class="sxs-lookup"><span data-stu-id="2ddd0-129">Rework Self-Updater with V3 Apis - [#4197](https://github.com/NuGet/Home/issues/4197)</span></span>

* <span data-ttu-id="2ddd0-130">Nesprávná verze závislostí balíčku, pokud je verze závislosti balíčku nastavená na \*- [#6697](https://github.com/NuGet/Home/issues/6697)</span><span class="sxs-lookup"><span data-stu-id="2ddd0-130">Wrong package dependency version If package dependency version is set to '\*' - [#6697](https://github.com/NuGet/Home/issues/6697)</span></span>

* <span data-ttu-id="2ddd0-131">ErrorUnsafePackageEntry chybové zprávy neukazují na zdroj potíží – [#7505](https://github.com/NuGet/Home/issues/7505)</span><span class="sxs-lookup"><span data-stu-id="2ddd0-131">ErrorUnsafePackageEntry error message is not pointing to source of problem - [#7505](https://github.com/NuGet/Home/issues/7505)</span></span>

* <span data-ttu-id="2ddd0-132">Soubor zámku se nedodržuje ve scénářích "\*" – [#8073](https://github.com/NuGet/Home/issues/8073)</span><span class="sxs-lookup"><span data-stu-id="2ddd0-132">Lock file is not honored in "\*" scenarios  - [#8073](https://github.com/NuGet/Home/issues/8073)</span></span>

* <span data-ttu-id="2ddd0-133">Nástroj NuGet. exe neumožňuje překládat na nejnovější verzi balíčku při použití \* v PackageReference (MSBuild/dotnet/VS Restore) – [#8432](https://github.com/NuGet/Home/issues/8432)</span><span class="sxs-lookup"><span data-stu-id="2ddd0-133">NuGet.exe does not resolve to the latest version of a package when using \* in PackageReference (MSBuild/Dotnet/VS restore do) - [#8432](https://github.com/NuGet/Home/issues/8432)</span></span>

* <span data-ttu-id="2ddd0-134">balíček seznamu dotnet s cíleným projektem WPF – [#8463](https://github.com/NuGet/Home/issues/8463)</span><span class="sxs-lookup"><span data-stu-id="2ddd0-134">dotnet list package with multi targeting WPF project - [#8463](https://github.com/NuGet/Home/issues/8463)</span></span>

* <span data-ttu-id="2ddd0-135">Zvýšení ConcurrencyUtilities (snížení využití CPU) – [#8653](https://github.com/NuGet/Home/issues/8653)</span><span class="sxs-lookup"><span data-stu-id="2ddd0-135">Improve ConcurrencyUtilities (reduce CPU usage) - [#8653](https://github.com/NuGet/Home/issues/8653)</span></span>

* <span data-ttu-id="2ddd0-136">Specifikace DG pro Neuvolněné projektové scénáře by se neměly zapisovat do obnovení verze Preview- [#8793](https://github.com/NuGet/Home/issues/8793)</span><span class="sxs-lookup"><span data-stu-id="2ddd0-136">DG Spec for unloaded project scenarios should not be written in preview restores - [#8793](https://github.com/NuGet/Home/issues/8793)</span></span>

* <span data-ttu-id="2ddd0-137">Balíčky NuGet sady Visual Studio (RestoreManagerPackage) musí automaticky načíst při událostech sestavení řešení – [#8796](https://github.com/NuGet/Home/issues/8796)</span><span class="sxs-lookup"><span data-stu-id="2ddd0-137">The Visual Studio NuGet packages (RestoreManagerPackage) needs to auto load on solution build events - [#8796](https://github.com/NuGet/Home/issues/8796)</span></span>

* <span data-ttu-id="2ddd0-138">Zablokování v VSSettings init- [#8842](https://github.com/NuGet/Home/issues/8842)</span><span class="sxs-lookup"><span data-stu-id="2ddd0-138">Deadlock in VSSettings init - [#8842](https://github.com/NuGet/Home/issues/8842)</span></span>

* <span data-ttu-id="2ddd0-139">Sada nástrojů VisualStudio není naplněna z balíčku NuGet, pokud je projekt umístěn ve složce řešení – [#8868](https://github.com/NuGet/Home/issues/8868)</span><span class="sxs-lookup"><span data-stu-id="2ddd0-139">VisualStudio ToolBox is not populated from a NuGet package if a project is placed in a solution folder - [#8868](https://github.com/NuGet/Home/issues/8868)</span></span>

* <span data-ttu-id="2ddd0-140">VS: obnovení řešení se trvale nezdařilo z důvodu konfliktu časování – [#8881](https://github.com/NuGet/Home/issues/8881)</span><span class="sxs-lookup"><span data-stu-id="2ddd0-140">VS:  solution restore perpetually fails due to race condition - [#8881](https://github.com/NuGet/Home/issues/8881)</span></span>

* <span data-ttu-id="2ddd0-141">Konstanta "načítání.." na nainstalované kartě a "hledání</span><span class="sxs-lookup"><span data-stu-id="2ddd0-141">Constant "loading.." on installed tab, and "searching</span></span> <term><span data-ttu-id="2ddd0-142">.. "na kartě aktualizace – [#8890](https://github.com/NuGet/Home/issues/8890)</span><span class="sxs-lookup"><span data-stu-id="2ddd0-142">.." on updates tab - [#8890](https://github.com/NuGet/Home/issues/8890)</span></span>

* <span data-ttu-id="2ddd0-143">Chybějící vložené ikony v uživatelském rozhraní VS PM po vypršení platnosti mezipaměti – [#9069](https://github.com/NuGet/Home/issues/9069)</span><span class="sxs-lookup"><span data-stu-id="2ddd0-143">Missing Embedded Icons in VS PM UI after cache expires - [#9069](https://github.com/NuGet/Home/issues/9069)</span></span>

* <span data-ttu-id="2ddd0-144">Spuštění uživatelského rozhraní FireAndForget PM – [#9112](https://github.com/NuGet/Home/issues/9112)</span><span class="sxs-lookup"><span data-stu-id="2ddd0-144">FireAndForget PM UI startup - [#9112](https://github.com/NuGet/Home/issues/9112)</span></span>

* <span data-ttu-id="2ddd0-145">Obnovení: implementace IncludeExcludeFiles. Equals (...) je nesprávná – [#9167](https://github.com/NuGet/Home/issues/9167)</span><span class="sxs-lookup"><span data-stu-id="2ddd0-145">Restore: IncludeExcludeFiles.Equals(...) implementation is incorrect - [#9167](https://github.com/NuGet/Home/issues/9167)</span></span>

* <span data-ttu-id="2ddd0-146">Restore: PackageSpec. Clone () vytvoří neshodnou kopii [#9211](https://github.com/NuGet/Home/issues/9211)</span><span class="sxs-lookup"><span data-stu-id="2ddd0-146">Restore: PackageSpec.Clone() creates unequal clone - [#9211](https://github.com/NuGet/Home/issues/9211)</span></span>

* <span data-ttu-id="2ddd0-147">Seznam chyb zobrazený, přestože při dokončení sestavení s chybami není zaškrtnuto- [#8190](https://github.com/NuGet/Home/issues/8190) "Always show seznam chyb</span><span class="sxs-lookup"><span data-stu-id="2ddd0-147">Error list shown although "Always show Error List if build finishes with errors" is not checked - [#8190](https://github.com/NuGet/Home/issues/8190)</span></span>

* <span data-ttu-id="2ddd0-148">Statické obnovení grafu by nemělo předávat prázdné SolutionPath- [#9061](https://github.com/NuGet/Home/issues/9061)</span><span class="sxs-lookup"><span data-stu-id="2ddd0-148">Static Graph restore should not pass empty SolutionPath - [#9061](https://github.com/NuGet/Home/issues/9061)</span></span>

* <span data-ttu-id="2ddd0-149">Obnovení: vypočítáno uzavření pro každý projekt 4 časy – [#9042](https://github.com/NuGet/Home/issues/9042)</span><span class="sxs-lookup"><span data-stu-id="2ddd0-149">Restore: closure computed for each project 4 times - [#9042](https://github.com/NuGet/Home/issues/9042)</span></span>

* <span data-ttu-id="2ddd0-150">Restore: DependencyGraphSpec. Load (...) nepotřebuje JObject- [#9040](https://github.com/NuGet/Home/issues/9040)</span><span class="sxs-lookup"><span data-stu-id="2ddd0-150">Restore: DependencyGraphSpec.Load(...) does not need JObject - [#9040](https://github.com/NuGet/Home/issues/9040)</span></span>

* <span data-ttu-id="2ddd0-151">Obnovení: velké řetězce vytvořené v haldě pro velké objekty (LOH) – [#9031](https://github.com/NuGet/Home/issues/9031)</span><span class="sxs-lookup"><span data-stu-id="2ddd0-151">Restore: large strings created on large object heap (LOH) - [#9031](https://github.com/NuGet/Home/issues/9031)</span></span>

* <span data-ttu-id="2ddd0-152">Vlastní nástroj NuGet. exe na novější mono může být přerušený kvůli Překladači sady MSBuild SDK – [8848](https://github.com/NuGet/Home/issues/8848)</span><span class="sxs-lookup"><span data-stu-id="2ddd0-152">Custom nuget.exe on newer mono might break due to the MSBuild SDK Resolver - [8848](https://github.com/NuGet/Home/issues/8848)</span></span>

* <span data-ttu-id="2ddd0-153">obnovení se nepovede, když NuGet. argument dgspec. JSON používá jiný proces – [8692](https://github.com/NuGet/Home/issues/8692) .</span><span class="sxs-lookup"><span data-stu-id="2ddd0-153">restore fails when nuget.dgspec.json is "used by another process" - [8692](https://github.com/NuGet/Home/issues/8692)</span></span>

<span data-ttu-id="2ddd0-154">**Chcete odeslat obecnou**</span><span class="sxs-lookup"><span data-stu-id="2ddd0-154">**DCRs**</span></span>

* <span data-ttu-id="2ddd0-155">Logika v _GetRestoreProjectStyle musí být v rámci úlohy – [#8804](https://github.com/NuGet/Home/issues/8804)</span><span class="sxs-lookup"><span data-stu-id="2ddd0-155">Logic in _GetRestoreProjectStyle should be in a task - [#8804](https://github.com/NuGet/Home/issues/8804)</span></span>

* <span data-ttu-id="2ddd0-156">Ve výchozím nastavení přidejte informace o zastaralosti na kartě installed – [#8541](https://github.com/NuGet/Home/issues/8541)</span><span class="sxs-lookup"><span data-stu-id="2ddd0-156">Add deprecation information by default on the installed tab - [#8541](https://github.com/NuGet/Home/issues/8541)</span></span>

<span data-ttu-id="2ddd0-157">**[Seznam všech problémů opravených v této verzi – 5,5](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e0e5fbd021f7aa0ec95db18)**</span><span class="sxs-lookup"><span data-stu-id="2ddd0-157">**[List of all issues fixed in this release - 5.5](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e0e5fbd021f7aa0ec95db18)**</span></span>
