---
title: "Příkaz Obnovit NuGet rozhraní příkazového řádku | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 6ee41020-e548-4e61-b8cd-c82b77ac6af7
description: "Referenční dokumentace pro příkaz restore nuget.exe"
keywords: "nuget restore odkaz, balíčky příkazu Obnovit"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b435a3c2ffe08e3c2f8fc6a4dacb06cf674e4fb9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="restore-command-nuget-cli"></a><span data-ttu-id="64090-104">příkaz Restore (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="64090-104">restore command (NuGet CLI)</span></span>

<span data-ttu-id="64090-105">**Platí pro:** balíček spotřeba &bullet; **podporované verze:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="64090-105">**Applies to:** package consumption &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="64090-106">NuGet 2.7 +: Stáhne a nainstaluje všechny balíčky chybí `packages` složky.</span><span class="sxs-lookup"><span data-stu-id="64090-106">NuGet 2.7+: Downloads and installs any packages missing from the `packages` folder.</span></span>

<span data-ttu-id="64090-107">NuGet 3.3 + s projekty pomocí `project.json`: generuje `project.lock.json` souboru a `<project>.nuget.props` souborů, v případě potřeby.</span><span class="sxs-lookup"><span data-stu-id="64090-107">NuGet 3.3+ with projects using `project.json`: Generates a `project.lock.json` file and a `<project>.nuget.props` file, if needed.</span></span> <span data-ttu-id="64090-108">(Oba soubory lze vynechat od správy zdrojového kódu.)</span><span class="sxs-lookup"><span data-stu-id="64090-108">(Both files can be omitted from source control.)</span></span>

<span data-ttu-id="64090-109">NuGet 4.0 + s projektem v balíčky, které odkazy jsou zahrnuty v souboru projektu přímo: generuje `<project>.nuget.props` v případě potřeby v souboru `obj` složky.</span><span class="sxs-lookup"><span data-stu-id="64090-109">NuGet 4.0+ with project in which package references are included in the project file directly: Generates a `<project>.nuget.props` file, if needed, in the `obj` folder.</span></span> <span data-ttu-id="64090-110">(Soubor lze vynechat od správy zdrojového kódu.)</span><span class="sxs-lookup"><span data-stu-id="64090-110">(The file can be omitted from source control.)</span></span>

<span data-ttu-id="64090-111">Na Mac OSX a Linux pomocí rozhraní příkazového řádku na Mono obnovení balíčků není podporováno ve formátu PackageReference.</span><span class="sxs-lookup"><span data-stu-id="64090-111">On Mac OSX and Linux with the CLI on Mono, restoring packages is not supported with the PackageReference format.</span></span>

## <a name="usage"></a><span data-ttu-id="64090-112">Použití</span><span class="sxs-lookup"><span data-stu-id="64090-112">Usage</span></span>

```
nuget restore <projectPath> [options]
```

<span data-ttu-id="64090-113">kde `<projectPath>` Určuje umístění řešení, `packages.config` souboru, nebo `project.json` souboru.</span><span class="sxs-lookup"><span data-stu-id="64090-113">where `<projectPath>` specifies the location of a solution, a `packages.config` file, or a `project.json` file.</span></span> <span data-ttu-id="64090-114">V tématu [poznámky](#remarks) níže chování podrobnosti.</span><span class="sxs-lookup"><span data-stu-id="64090-114">See [Remarks](#remarks) below for behavioral details.</span></span>

## <a name="options"></a><span data-ttu-id="64090-115">Možnosti</span><span class="sxs-lookup"><span data-stu-id="64090-115">Options</span></span>

| <span data-ttu-id="64090-116">Možnost</span><span class="sxs-lookup"><span data-stu-id="64090-116">Option</span></span> | <span data-ttu-id="64090-117">Popis</span><span class="sxs-lookup"><span data-stu-id="64090-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="64090-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="64090-118">ConfigFile</span></span> | <span data-ttu-id="64090-119">Konfigurační soubor NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="64090-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="64090-120">Pokud není zadaný, *%AppData%\NuGet\NuGet.Config* se používá.</span><span class="sxs-lookup"><span data-stu-id="64090-120">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="64090-121">DirectDownload</span><span class="sxs-lookup"><span data-stu-id="64090-121">DirectDownload</span></span> | <span data-ttu-id="64090-122">*(4.0 +)*  Balíčky stahuje přímo bez naplnění mezipaměti se binární soubory nebo metadata.</span><span class="sxs-lookup"><span data-stu-id="64090-122">*(4.0+)* Downloads packages directly without populating caches with any binaries or metadata.</span></span> |
| <span data-ttu-id="64090-123">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="64090-123">DisableParallelProcessing</span></span> | <span data-ttu-id="64090-124">Zakáže obnovení více balíčky současně.</span><span class="sxs-lookup"><span data-stu-id="64090-124">Disables restoring multiple packages in parallel.</span></span> |
| <span data-ttu-id="64090-125">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="64090-125">FallbackSource</span></span> | <span data-ttu-id="64090-126">*(3.2 +)*  Seznam zdroje balíčku pro použití jako případech přejít v případě, že daný balíček nebyl nalezen v primární nebo výchozí zdroj.</span><span class="sxs-lookup"><span data-stu-id="64090-126">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="64090-127">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="64090-127">ForceEnglishOutput</span></span> | <span data-ttu-id="64090-128">*(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze.</span><span class="sxs-lookup"><span data-stu-id="64090-128">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="64090-129">Nápověda</span><span class="sxs-lookup"><span data-stu-id="64090-129">Help</span></span> | <span data-ttu-id="64090-130">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="64090-130">Displays help information for the command.</span></span> |
| <span data-ttu-id="64090-131">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="64090-131">MSBuildPath</span></span> | <span data-ttu-id="64090-132">*(4.0 +)*  Určuje cestu MSBuild používat pomocí příkazu, přednost před `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="64090-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="64090-133">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="64090-133">MSBuildVersion</span></span> | <span data-ttu-id="64090-134">*(3.2 +)*  Určuje verzi nástroje MSBuild k použití se tento příkaz.</span><span class="sxs-lookup"><span data-stu-id="64090-134">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="64090-135">Podporované hodnoty jsou 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="64090-135">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="64090-136">Ve výchozím nastavení je zachyceny MSBuild ve své cestě jinak bude výchozí nejvyšší nainstalovanou verzi nástroje MSBuild.</span><span class="sxs-lookup"><span data-stu-id="64090-136">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="64090-137">NoCache</span><span class="sxs-lookup"><span data-stu-id="64090-137">NoCache</span></span> | <span data-ttu-id="64090-138">NuGet bránit v použití balíčky z mezipaměti místního počítače.</span><span class="sxs-lookup"><span data-stu-id="64090-138">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="64090-139">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="64090-139">NonInteractive</span></span> | <span data-ttu-id="64090-140">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="64090-140">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="64090-141">Výstupnísložka</span><span class="sxs-lookup"><span data-stu-id="64090-141">OutputDirectory</span></span> | <span data-ttu-id="64090-142">Určuje složku, ve kterém jsou nainstalované balíčky.</span><span class="sxs-lookup"><span data-stu-id="64090-142">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="64090-143">Pokud není zadaný žádný složky, se používá aktuální složky.</span><span class="sxs-lookup"><span data-stu-id="64090-143">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="64090-144">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="64090-144">PackageSaveMode</span></span> | <span data-ttu-id="64090-145">Určuje typy souborů, uložte po instalaci balíčku: jeden z `nuspec`, `nupkg`, nebo `nuspec;nupkg`.</span><span class="sxs-lookup"><span data-stu-id="64090-145">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="64090-146">PackagesDirectory</span><span class="sxs-lookup"><span data-stu-id="64090-146">PackagesDirectory</span></span> | <span data-ttu-id="64090-147">Stejné jako `OutputDirectory`.</span><span class="sxs-lookup"><span data-stu-id="64090-147">Same as `OutputDirectory`.</span></span> |
| <span data-ttu-id="64090-148">Project2ProjectTimeOut</span><span class="sxs-lookup"><span data-stu-id="64090-148">Project2ProjectTimeOut</span></span> | <span data-ttu-id="64090-149">Časový limit v sekundách pro odkazy na projekt na projekt řešení.</span><span class="sxs-lookup"><span data-stu-id="64090-149">Timeout in seconds for resolving project-to-project references.</span></span> |
| <span data-ttu-id="64090-150">Rekurzivní</span><span class="sxs-lookup"><span data-stu-id="64090-150">Recursive</span></span> | <span data-ttu-id="64090-151">*(4.0 +)*  Obnoví všechny odkazy na projekty pro projekty UWP a .NET Core.</span><span class="sxs-lookup"><span data-stu-id="64090-151">*(4.0+)* Restores all references projects for UWP and .NET Core projects.</span></span> <span data-ttu-id="64090-152">Nelze použít u projektů pomocí `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="64090-152">Does not apply to projects using `packages.config`.</span></span> |
| <span data-ttu-id="64090-153">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="64090-153">RequireConsent</span></span> | <span data-ttu-id="64090-154">Ověří, že probíhá obnovení balíčků je zapnutá před stažením a instalací balíčky.</span><span class="sxs-lookup"><span data-stu-id="64090-154">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="64090-155">Podrobnosti najdete v tématu [obnovení balíčků](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="64090-155">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="64090-156">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="64090-156">SolutionDirectory</span></span> | <span data-ttu-id="64090-157">Určuje složku řešení.</span><span class="sxs-lookup"><span data-stu-id="64090-157">Specifies the solution folder.</span></span> <span data-ttu-id="64090-158">Není platný při obnovení balíčků pro řešení.</span><span class="sxs-lookup"><span data-stu-id="64090-158">Not valid when restoring packages for a solution.</span></span> |
| <span data-ttu-id="64090-159">Zdroj</span><span class="sxs-lookup"><span data-stu-id="64090-159">Source</span></span> | <span data-ttu-id="64090-160">Určuje seznam zdrojů balíčku (jako adresy URL) pro obnovení.</span><span class="sxs-lookup"><span data-stu-id="64090-160">Specifies the list of package sources (as URLs) to use for the restore.</span></span> <span data-ttu-id="64090-161">Pokud tento parametr vynechán, příkaz používá zdrojů, součástí konfigurační soubory, najdete v části [konfigurace NuGet chování](../Consume-Packages/Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="64090-161">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md).</span></span> |
| <span data-ttu-id="64090-162">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="64090-162">Verbosity</span></span> |<span data-ttu-id="64090-163">> určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="64090-163">>Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="64090-164">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="64090-164">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="remarks"></a><span data-ttu-id="64090-165">Poznámky</span><span class="sxs-lookup"><span data-stu-id="64090-165">Remarks</span></span>

<span data-ttu-id="64090-166">Příkaz restore provede následující kroky:</span><span class="sxs-lookup"><span data-stu-id="64090-166">The restore command performs the following steps:</span></span>

1. <span data-ttu-id="64090-167">Určení režimu operace příkazu restore.</span><span class="sxs-lookup"><span data-stu-id="64090-167">Determine the operation mode of the restore command.</span></span>
    <span data-ttu-id="64090-168">Typ souboru projectPath</span><span class="sxs-lookup"><span data-stu-id="64090-168">projectPath file type</span></span> | <span data-ttu-id="64090-169">Chování</span><span class="sxs-lookup"><span data-stu-id="64090-169">Behavior</span></span>
    | --- | --- |
    <span data-ttu-id="64090-170">Řešení (složka)</span><span class="sxs-lookup"><span data-stu-id="64090-170">Solution (folder)</span></span> | <span data-ttu-id="64090-171">Hledá NuGet `.sln` souborů a použije je-li nalezen; jinak vrátí chybu.</span><span class="sxs-lookup"><span data-stu-id="64090-171">NuGet looks for a `.sln` file and uses that if found; otherwise gives an error.</span></span> <span data-ttu-id="64090-172">`(SolutionDir)\.nuget`slouží jako výchozí složku.</span><span class="sxs-lookup"><span data-stu-id="64090-172">`(SolutionDir)\.nuget` is used as the starting folder.</span></span>
    <span data-ttu-id="64090-173">`.sln`soubor</span><span class="sxs-lookup"><span data-stu-id="64090-173">`.sln` file</span></span> | <span data-ttu-id="64090-174">Obnovení balíčků se identifikovanou pomocí řešení; Vrátí chybu, pokud `-SolutionDirectory` se používá.</span><span class="sxs-lookup"><span data-stu-id="64090-174">Restore packages identified by the solution; gives an error if `-SolutionDirectory` is used.</span></span> <span data-ttu-id="64090-175">`$(SolutionDir)\.nuget`slouží jako výchozí složku.</span><span class="sxs-lookup"><span data-stu-id="64090-175">`$(SolutionDir)\.nuget` is used as the starting folder.</span></span>
    <span data-ttu-id="64090-176">`packages.config`, `project.json`, nebo soubor projektu</span><span class="sxs-lookup"><span data-stu-id="64090-176">`packages.config`, `project.json`, or project file</span></span> | <span data-ttu-id="64090-177">Obnovte balíčky uvedené v souboru, řešení a instalování závislostí.</span><span class="sxs-lookup"><span data-stu-id="64090-177">Restore packages listed in the file, resolving and installing dependencies.</span></span>
    <span data-ttu-id="64090-178">Další typ souboru</span><span class="sxs-lookup"><span data-stu-id="64090-178">Other file type</span></span> | <span data-ttu-id="64090-179">Soubor se předpokládá, že se `.sln` souboru jak je uvedeno výše; Pokud není řešením, nabízí NuGet se chyba.</span><span class="sxs-lookup"><span data-stu-id="64090-179">File is assumed to be a `.sln` file as above; if it's not a solution, NuGet gives an error.</span></span>
    <span data-ttu-id="64090-180">(není zadaný projectPath)</span><span class="sxs-lookup"><span data-stu-id="64090-180">(projectPath not specified)</span></span> | <span data-ttu-id="64090-181">-NuGet vyhledá soubory řešení v aktuální složce.</span><span class="sxs-lookup"><span data-stu-id="64090-181">- NuGet looks for solution files in the current folder.</span></span> <span data-ttu-id="64090-182">Pokud je nalezen jeden soubor, než se používá k obnovení balíčků; Pokud je nalezeno více řešení, NuGet obsahuje chybu.</span><span class="sxs-lookup"><span data-stu-id="64090-182">If a single file is found, that one is used to restore packages; if multiple solutions are found, NuGet gives an error.</span></span>
    |<span data-ttu-id="64090-183">– Pokud nejsou žádné soubory řešení, hledá NuGet `packages.config` nebo `project.json` a použije ho k obnovení balíčků.</span><span class="sxs-lookup"><span data-stu-id="64090-183">- If there are no solution files, NuGet looks for a `packages.config` or `project.json` and uses that to restore packages.</span></span>
    |<span data-ttu-id="64090-184">– Pokud žádný soubor řešení `packages.config`, nebo `project.json` nenajde, NuGet obsahuje chybu.</span><span class="sxs-lookup"><span data-stu-id="64090-184">- If no solution file, `packages.config`, or `project.json` is found, NuGet gives an error.</span></span>

1. <span data-ttu-id="64090-185">Můžete určete složky balíčků v následujícím pořadí priority (NuGet vrátí chybu, pokud se nenajdou žádné z těchto složek):</span><span class="sxs-lookup"><span data-stu-id="64090-185">Determine the packages folder using the following priority order (NuGet gives an error if none of these folders are found):</span></span>

    - <span data-ttu-id="64090-186">`%userprofile%\.nuget\packages` Hodnotu `project.json`.</span><span class="sxs-lookup"><span data-stu-id="64090-186">The `%userprofile%\.nuget\packages` value in `project.json`.</span></span>
    - <span data-ttu-id="64090-187">Zadaná složka s `-PackagesDirectory`.</span><span class="sxs-lookup"><span data-stu-id="64090-187">The folder specified with `-PackagesDirectory`.</span></span>
    - <span data-ttu-id="64090-188">`repositoryPath` Vale v`Nuget.Config`</span><span class="sxs-lookup"><span data-stu-id="64090-188">The `repositoryPath` vale in `Nuget.Config`</span></span>
    - <span data-ttu-id="64090-189">Zadaná složka s`-SolutionDirectory`</span><span class="sxs-lookup"><span data-stu-id="64090-189">The folder specified with `-SolutionDirectory`</span></span>
    - `$(SolutionDir)\packages`

1. <span data-ttu-id="64090-190">Při obnovování balíčků pro řešení, NuGet provede následující akce:</span><span class="sxs-lookup"><span data-stu-id="64090-190">When restoring packages for a solution, NuGet does the following:</span></span>
    - <span data-ttu-id="64090-191">Načte soubor řešení.</span><span class="sxs-lookup"><span data-stu-id="64090-191">Loads the solution file.</span></span>
    - <span data-ttu-id="64090-192">Obnoví řešení úrovně balíčky uvedené v `$(SolutionDir)\.nuget\packages.config` do `packages` složky.</span><span class="sxs-lookup"><span data-stu-id="64090-192">Restores solution level packages listed in `$(SolutionDir)\.nuget\packages.config` into the `packages` folder.</span></span>
    - <span data-ttu-id="64090-193">Obnovení balíčků, které jsou uvedené v `$(ProjectDir)\packages.config` do `packages` složky.</span><span class="sxs-lookup"><span data-stu-id="64090-193">Restore packages listed in `$(ProjectDir)\packages.config` into the `packages` folder.</span></span> <span data-ttu-id="64090-194">Pro každý balíček určený obnovení balíčku paralelně, pokud `-DisableParallelProcessing` je zadán.</span><span class="sxs-lookup"><span data-stu-id="64090-194">For each package specified, restore the package in parallel unless `-DisableParallelProcessing` is specified.</span></span>

## <a name="examples"></a><span data-ttu-id="64090-195">Příklady</span><span class="sxs-lookup"><span data-stu-id="64090-195">Examples</span></span>

```
# Restore packages for a solution file
nuget restore a.sln

# Restore packages for a solution file, using MSBuild version 14.0 to load the solution and its project(s)
nuget restore a.sln -MSBuildVersion 14

# Restore packages for a project's packages.config file, with the packages folder at the parent
nuget restore proj1\packages.config -PackagesDirectory ..\packages

# Restore packages for the solution in the current folder, specifying package sources
nuget restore -source "https://api.nuget.org/v3/index.json;https://www.myget.org/F/nuget"
```
