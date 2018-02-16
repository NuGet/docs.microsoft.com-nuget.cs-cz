---
title: "Příkaz Obnovit NuGet rozhraní příkazového řádku | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenční dokumentace pro příkaz restore nuget.exe"
keywords: "nuget restore odkaz, balíčky příkazu Obnovit"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0ad5156a065e20dfced99da6b2e2860dbd748ad5
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/14/2018
---
# <a name="restore-command-nuget-cli"></a><span data-ttu-id="ad58d-104">příkaz Restore (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="ad58d-104">restore command (NuGet CLI)</span></span>

<span data-ttu-id="ad58d-105">**Platí pro:** balíček spotřeba &bullet; **podporované verze:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="ad58d-105">**Applies to:** package consumption &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="ad58d-106">Stáhne a nainstaluje všechny balíčky chybí `packages` složky.</span><span class="sxs-lookup"><span data-stu-id="ad58d-106">Downloads and installs any packages missing from the `packages` folder.</span></span> <span data-ttu-id="ad58d-107">Při použití s NuGet 4.0 + a formát PackageReference, generuje `<project>.nuget.props` v případě potřeby v souboru `obj` složky.</span><span class="sxs-lookup"><span data-stu-id="ad58d-107">When used with NuGet 4.0+ and the PackageReference format, generates a `<project>.nuget.props` file, if needed, in the `obj` folder.</span></span> <span data-ttu-id="ad58d-108">(Soubor lze vynechat od správy zdrojového kódu.)</span><span class="sxs-lookup"><span data-stu-id="ad58d-108">(The file can be omitted from source control.)</span></span>

<span data-ttu-id="ad58d-109">Na Mac OSX a Linux pomocí rozhraní příkazového řádku na Mono Probíhá obnovení balíčků nepodporuje PackageReference.</span><span class="sxs-lookup"><span data-stu-id="ad58d-109">On Mac OSX and Linux with the CLI on Mono, restoring packages is not supported with PackageReference.</span></span>

## <a name="usage"></a><span data-ttu-id="ad58d-110">Použití</span><span class="sxs-lookup"><span data-stu-id="ad58d-110">Usage</span></span>

```cli
nuget restore <projectPath> [options]
```

<span data-ttu-id="ad58d-111">kde `<projectPath>` Určuje umístění řešení nebo `packages.config` souboru.</span><span class="sxs-lookup"><span data-stu-id="ad58d-111">where `<projectPath>` specifies the location of a solution or a `packages.config` file.</span></span> <span data-ttu-id="ad58d-112">V tématu [poznámky](#remarks) níže chování podrobnosti.</span><span class="sxs-lookup"><span data-stu-id="ad58d-112">See [Remarks](#remarks) below for behavioral details.</span></span>

## <a name="options"></a><span data-ttu-id="ad58d-113">Možnosti</span><span class="sxs-lookup"><span data-stu-id="ad58d-113">Options</span></span>

| <span data-ttu-id="ad58d-114">Možnost</span><span class="sxs-lookup"><span data-stu-id="ad58d-114">Option</span></span> | <span data-ttu-id="ad58d-115">Popis</span><span class="sxs-lookup"><span data-stu-id="ad58d-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ad58d-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="ad58d-116">ConfigFile</span></span> | <span data-ttu-id="ad58d-117">Konfigurační soubor NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="ad58d-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ad58d-118">Pokud není zadaný, *%AppData%\NuGet\NuGet.Config* se používá.</span><span class="sxs-lookup"><span data-stu-id="ad58d-118">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="ad58d-119">DirectDownload</span><span class="sxs-lookup"><span data-stu-id="ad58d-119">DirectDownload</span></span> | <span data-ttu-id="ad58d-120">*(4.0 +)*  Balíčky stahuje přímo bez naplnění mezipaměti se binární soubory nebo metadata.</span><span class="sxs-lookup"><span data-stu-id="ad58d-120">*(4.0+)* Downloads packages directly without populating caches with any binaries or metadata.</span></span> |
| <span data-ttu-id="ad58d-121">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="ad58d-121">DisableParallelProcessing</span></span> | <span data-ttu-id="ad58d-122">Zakáže obnovení více balíčky současně.</span><span class="sxs-lookup"><span data-stu-id="ad58d-122">Disables restoring multiple packages in parallel.</span></span> |
| <span data-ttu-id="ad58d-123">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="ad58d-123">FallbackSource</span></span> | <span data-ttu-id="ad58d-124">*(3.2 +)*  Seznam zdroje balíčku pro použití jako případech přejít v případě, že daný balíček nebyl nalezen v primární nebo výchozí zdroj.</span><span class="sxs-lookup"><span data-stu-id="ad58d-124">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="ad58d-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="ad58d-125">ForceEnglishOutput</span></span> | <span data-ttu-id="ad58d-126">*(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze.</span><span class="sxs-lookup"><span data-stu-id="ad58d-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="ad58d-127">Nápověda</span><span class="sxs-lookup"><span data-stu-id="ad58d-127">Help</span></span> | <span data-ttu-id="ad58d-128">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="ad58d-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="ad58d-129">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="ad58d-129">MSBuildPath</span></span> | <span data-ttu-id="ad58d-130">*(4.0 +)*  Určuje cestu MSBuild používat pomocí příkazu, přednost před `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="ad58d-130">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="ad58d-131">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="ad58d-131">MSBuildVersion</span></span> | <span data-ttu-id="ad58d-132">*(3.2 +)*  Určuje verzi nástroje MSBuild k použití se tento příkaz.</span><span class="sxs-lookup"><span data-stu-id="ad58d-132">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="ad58d-133">Podporované hodnoty jsou 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="ad58d-133">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="ad58d-134">Ve výchozím nastavení je zachyceny MSBuild ve své cestě jinak bude výchozí nejvyšší nainstalovanou verzi nástroje MSBuild.</span><span class="sxs-lookup"><span data-stu-id="ad58d-134">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="ad58d-135">NoCache</span><span class="sxs-lookup"><span data-stu-id="ad58d-135">NoCache</span></span> | <span data-ttu-id="ad58d-136">NuGet bránit v použití balíčky z mezipaměti místního počítače.</span><span class="sxs-lookup"><span data-stu-id="ad58d-136">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="ad58d-137">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="ad58d-137">NonInteractive</span></span> | <span data-ttu-id="ad58d-138">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="ad58d-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="ad58d-139">Výstupnísložka</span><span class="sxs-lookup"><span data-stu-id="ad58d-139">OutputDirectory</span></span> | <span data-ttu-id="ad58d-140">Určuje složku, ve kterém jsou nainstalované balíčky.</span><span class="sxs-lookup"><span data-stu-id="ad58d-140">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="ad58d-141">Pokud není zadaný žádný složky, se používá aktuální složky.</span><span class="sxs-lookup"><span data-stu-id="ad58d-141">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="ad58d-142">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="ad58d-142">PackageSaveMode</span></span> | <span data-ttu-id="ad58d-143">Určuje typy souborů, uložte po instalaci balíčku: jeden z `nuspec`, `nupkg`, nebo `nuspec;nupkg`.</span><span class="sxs-lookup"><span data-stu-id="ad58d-143">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="ad58d-144">PackagesDirectory</span><span class="sxs-lookup"><span data-stu-id="ad58d-144">PackagesDirectory</span></span> | <span data-ttu-id="ad58d-145">Stejné jako `OutputDirectory`.</span><span class="sxs-lookup"><span data-stu-id="ad58d-145">Same as `OutputDirectory`.</span></span> |
| <span data-ttu-id="ad58d-146">Project2ProjectTimeOut</span><span class="sxs-lookup"><span data-stu-id="ad58d-146">Project2ProjectTimeOut</span></span> | <span data-ttu-id="ad58d-147">Časový limit v sekundách pro odkazy na projekt na projekt řešení.</span><span class="sxs-lookup"><span data-stu-id="ad58d-147">Timeout in seconds for resolving project-to-project references.</span></span> |
| <span data-ttu-id="ad58d-148">Rekurzivní</span><span class="sxs-lookup"><span data-stu-id="ad58d-148">Recursive</span></span> | <span data-ttu-id="ad58d-149">*(4.0 +)*  Obnoví všechny odkazy na projekty pro projekty UWP a .NET Core.</span><span class="sxs-lookup"><span data-stu-id="ad58d-149">*(4.0+)* Restores all references projects for UWP and .NET Core projects.</span></span> <span data-ttu-id="ad58d-150">Nelze použít u projektů pomocí `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="ad58d-150">Does not apply to projects using `packages.config`.</span></span> |
| <span data-ttu-id="ad58d-151">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="ad58d-151">RequireConsent</span></span> | <span data-ttu-id="ad58d-152">Ověří, že probíhá obnovení balíčků je zapnutá před stažením a instalací balíčky.</span><span class="sxs-lookup"><span data-stu-id="ad58d-152">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="ad58d-153">Podrobnosti najdete v tématu [obnovení balíčků](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="ad58d-153">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="ad58d-154">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="ad58d-154">SolutionDirectory</span></span> | <span data-ttu-id="ad58d-155">Určuje složku řešení.</span><span class="sxs-lookup"><span data-stu-id="ad58d-155">Specifies the solution folder.</span></span> <span data-ttu-id="ad58d-156">Není platný při obnovení balíčků pro řešení.</span><span class="sxs-lookup"><span data-stu-id="ad58d-156">Not valid when restoring packages for a solution.</span></span> |
| <span data-ttu-id="ad58d-157">Zdroj</span><span class="sxs-lookup"><span data-stu-id="ad58d-157">Source</span></span> | <span data-ttu-id="ad58d-158">Určuje seznam zdrojů balíčku (jako adresy URL) pro obnovení.</span><span class="sxs-lookup"><span data-stu-id="ad58d-158">Specifies the list of package sources (as URLs) to use for the restore.</span></span> <span data-ttu-id="ad58d-159">Pokud tento parametr vynechán, příkaz používá zdrojů, součástí konfigurační soubory, najdete v části [konfigurace NuGet chování](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="ad58d-159">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="ad58d-160">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="ad58d-160">Verbosity</span></span> |<span data-ttu-id="ad58d-161">> určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="ad58d-161">>Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="ad58d-162">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ad58d-162">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="remarks"></a><span data-ttu-id="ad58d-163">Poznámky</span><span class="sxs-lookup"><span data-stu-id="ad58d-163">Remarks</span></span>

<span data-ttu-id="ad58d-164">Příkaz restore provede následující kroky:</span><span class="sxs-lookup"><span data-stu-id="ad58d-164">The restore command performs the following steps:</span></span>

1. <span data-ttu-id="ad58d-165">Určení režimu operace příkazu restore.</span><span class="sxs-lookup"><span data-stu-id="ad58d-165">Determine the operation mode of the restore command.</span></span>
    <span data-ttu-id="ad58d-166">Typ souboru projectPath</span><span class="sxs-lookup"><span data-stu-id="ad58d-166">projectPath file type</span></span> | <span data-ttu-id="ad58d-167">Chování</span><span class="sxs-lookup"><span data-stu-id="ad58d-167">Behavior</span></span>
    | --- | --- |
    <span data-ttu-id="ad58d-168">Řešení (složka)</span><span class="sxs-lookup"><span data-stu-id="ad58d-168">Solution (folder)</span></span> | <span data-ttu-id="ad58d-169">Hledá NuGet `.sln` souborů a použije je-li nalezen; jinak vrátí chybu.</span><span class="sxs-lookup"><span data-stu-id="ad58d-169">NuGet looks for a `.sln` file and uses that if found; otherwise gives an error.</span></span> <span data-ttu-id="ad58d-170">`(SolutionDir)\.nuget` slouží jako výchozí složku.</span><span class="sxs-lookup"><span data-stu-id="ad58d-170">`(SolutionDir)\.nuget` is used as the starting folder.</span></span>
    <span data-ttu-id="ad58d-171">`.sln` Soubor</span><span class="sxs-lookup"><span data-stu-id="ad58d-171">`.sln` file</span></span> | <span data-ttu-id="ad58d-172">Obnovení balíčků se identifikovanou pomocí řešení; Vrátí chybu, pokud `-SolutionDirectory` se používá.</span><span class="sxs-lookup"><span data-stu-id="ad58d-172">Restore packages identified by the solution; gives an error if `-SolutionDirectory` is used.</span></span> <span data-ttu-id="ad58d-173">`$(SolutionDir)\.nuget` slouží jako výchozí složku.</span><span class="sxs-lookup"><span data-stu-id="ad58d-173">`$(SolutionDir)\.nuget` is used as the starting folder.</span></span>
    <span data-ttu-id="ad58d-174">`packages.config` nebo soubor projektu</span><span class="sxs-lookup"><span data-stu-id="ad58d-174">`packages.config` or project file</span></span> | <span data-ttu-id="ad58d-175">Obnovte balíčky uvedené v souboru, řešení a instalování závislostí.</span><span class="sxs-lookup"><span data-stu-id="ad58d-175">Restore packages listed in the file, resolving and installing dependencies.</span></span>
    <span data-ttu-id="ad58d-176">Další typ souboru</span><span class="sxs-lookup"><span data-stu-id="ad58d-176">Other file type</span></span> | <span data-ttu-id="ad58d-177">Soubor se předpokládá, že se `.sln` souboru jak je uvedeno výše; Pokud není řešením, nabízí NuGet se chyba.</span><span class="sxs-lookup"><span data-stu-id="ad58d-177">File is assumed to be a `.sln` file as above; if it's not a solution, NuGet gives an error.</span></span>
    <span data-ttu-id="ad58d-178">(není zadaný projectPath)</span><span class="sxs-lookup"><span data-stu-id="ad58d-178">(projectPath not specified)</span></span> | <span data-ttu-id="ad58d-179">-NuGet vyhledá soubory řešení v aktuální složce.</span><span class="sxs-lookup"><span data-stu-id="ad58d-179">- NuGet looks for solution files in the current folder.</span></span> <span data-ttu-id="ad58d-180">Pokud je nalezen jeden soubor, než se používá k obnovení balíčků; Pokud je nalezeno více řešení, NuGet obsahuje chybu.</span><span class="sxs-lookup"><span data-stu-id="ad58d-180">If a single file is found, that one is used to restore packages; if multiple solutions are found, NuGet gives an error.</span></span>
    |<span data-ttu-id="ad58d-181">– Pokud nejsou žádné soubory řešení, hledá NuGet `packages.config` a použije ho k obnovení balíčků.</span><span class="sxs-lookup"><span data-stu-id="ad58d-181">- If there are no solution files, NuGet looks for a `packages.config` and uses that to restore packages.</span></span>
    |<span data-ttu-id="ad58d-182">– Pokud žádné řešení nebo `packages.config` je nalezeno, vrátí chybu NuGet.</span><span class="sxs-lookup"><span data-stu-id="ad58d-182">- If no solution or `packages.config` file is found, NuGet gives an error.</span></span>

1. <span data-ttu-id="ad58d-183">Můžete určete složky balíčků v následujícím pořadí priority (NuGet vrátí chybu, pokud se nenajdou žádné z těchto složek):</span><span class="sxs-lookup"><span data-stu-id="ad58d-183">Determine the packages folder using the following priority order (NuGet gives an error if none of these folders are found):</span></span>

    - <span data-ttu-id="ad58d-184">Zadaná složka s `-PackagesDirectory`.</span><span class="sxs-lookup"><span data-stu-id="ad58d-184">The folder specified with `-PackagesDirectory`.</span></span>
    - <span data-ttu-id="ad58d-185">`repositoryPath` Vale v `Nuget.Config`</span><span class="sxs-lookup"><span data-stu-id="ad58d-185">The `repositoryPath` vale in `Nuget.Config`</span></span>
    - <span data-ttu-id="ad58d-186">Zadaná složka s `-SolutionDirectory`</span><span class="sxs-lookup"><span data-stu-id="ad58d-186">The folder specified with `-SolutionDirectory`</span></span>
    - `$(SolutionDir)\packages`

1. <span data-ttu-id="ad58d-187">Při obnovování balíčků pro řešení, NuGet provede následující akce:</span><span class="sxs-lookup"><span data-stu-id="ad58d-187">When restoring packages for a solution, NuGet does the following:</span></span>
    - <span data-ttu-id="ad58d-188">Načte soubor řešení.</span><span class="sxs-lookup"><span data-stu-id="ad58d-188">Loads the solution file.</span></span>
    - <span data-ttu-id="ad58d-189">Obnoví řešení úrovně balíčky uvedené v `$(SolutionDir)\.nuget\packages.config` do `packages` složky.</span><span class="sxs-lookup"><span data-stu-id="ad58d-189">Restores solution level packages listed in `$(SolutionDir)\.nuget\packages.config` into the `packages` folder.</span></span>
    - <span data-ttu-id="ad58d-190">Obnovení balíčků, které jsou uvedené v `$(ProjectDir)\packages.config` do `packages` složky.</span><span class="sxs-lookup"><span data-stu-id="ad58d-190">Restore packages listed in `$(ProjectDir)\packages.config` into the `packages` folder.</span></span> <span data-ttu-id="ad58d-191">Pro každý balíček určený obnovení balíčku paralelně, pokud `-DisableParallelProcessing` je zadán.</span><span class="sxs-lookup"><span data-stu-id="ad58d-191">For each package specified, restore the package in parallel unless `-DisableParallelProcessing` is specified.</span></span>

## <a name="examples"></a><span data-ttu-id="ad58d-192">Příklady</span><span class="sxs-lookup"><span data-stu-id="ad58d-192">Examples</span></span>

```cli
# Restore packages for a solution file
nuget restore a.sln

# Restore packages for a solution file, using MSBuild version 14.0 to load the solution and its project(s)
nuget restore a.sln -MSBuildVersion 14

# Restore packages for a project's packages.config file, with the packages folder at the parent
nuget restore proj1\packages.config -PackagesDirectory ..\packages

# Restore packages for the solution in the current folder, specifying package sources
nuget restore -source "https://api.nuget.org/v3/index.json;https://www.myget.org/F/nuget"
```
