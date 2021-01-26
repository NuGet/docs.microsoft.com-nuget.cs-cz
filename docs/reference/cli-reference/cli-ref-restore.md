---
title: NuGet CLI – příkaz obnovení
description: Referenční informace pro příkaz nuget.exe Restore
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 49fabbd0ef0c1c0c16f13bdf741296575fa72359
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780034"
---
# <a name="restore-command-nuget-cli"></a><span data-ttu-id="401c6-103">příkaz Restore (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="401c6-103">restore command (NuGet CLI)</span></span>

<span data-ttu-id="401c6-104">**Platí pro:** &bullet; **podporované verze balíčku:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="401c6-104">**Applies to:** package consumption &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="401c6-105">Stáhne a nainstaluje ze složky chybějící balíčky `packages` .</span><span class="sxs-lookup"><span data-stu-id="401c6-105">Downloads and installs any packages missing from the `packages` folder.</span></span> <span data-ttu-id="401c6-106">Při použití s NuGet 4.0 + a formátem PackageReference vygeneruje `<project>.nuget.props` v případě potřeby soubor ve `obj` složce.</span><span class="sxs-lookup"><span data-stu-id="401c6-106">When used with NuGet 4.0+ and the PackageReference format, generates a `<project>.nuget.props` file, if needed, in the `obj` folder.</span></span> <span data-ttu-id="401c6-107">(Soubor může být vynechán ze správy zdrojového kódu.)</span><span class="sxs-lookup"><span data-stu-id="401c6-107">(The file can be omitted from source control.)</span></span>

<span data-ttu-id="401c6-108">V systému Mac OSX a Linux s rozhraním příkazového řádku pro mono není obnovení balíčků podporováno v PackageReference.</span><span class="sxs-lookup"><span data-stu-id="401c6-108">On Mac OSX and Linux with the CLI on Mono, restoring packages is not supported with PackageReference.</span></span>

## <a name="usage"></a><span data-ttu-id="401c6-109">Využití</span><span class="sxs-lookup"><span data-stu-id="401c6-109">Usage</span></span>

```cli
nuget restore <projectPath> [options]
```

<span data-ttu-id="401c6-110">kde `<projectPath>` Určuje umístění řešení nebo `packages.config` souboru.</span><span class="sxs-lookup"><span data-stu-id="401c6-110">where `<projectPath>` specifies the location of a solution or a `packages.config` file.</span></span> <span data-ttu-id="401c6-111">Podrobnosti o chování najdete níže v části [poznámky](#remarks) .</span><span class="sxs-lookup"><span data-stu-id="401c6-111">See [Remarks](#remarks) below for behavioral details.</span></span>

## <a name="options"></a><span data-ttu-id="401c6-112">Možnosti</span><span class="sxs-lookup"><span data-stu-id="401c6-112">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="401c6-113">Konfigurační soubor NuGet, který se má použít</span><span class="sxs-lookup"><span data-stu-id="401c6-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="401c6-114">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows) nebo `~/.nuget/NuGet/NuGet.Config` nebo `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="401c6-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-DirectDownload`**

  <span data-ttu-id="401c6-115">*(4.0 +)* Stáhne balíčky přímo bez doplňování mezipamětí s libovolnými binárními soubory nebo metadaty.</span><span class="sxs-lookup"><span data-stu-id="401c6-115">*(4.0+)* Downloads packages directly without populating caches with any binaries or metadata.</span></span>

- **`-DisableParallelProcessing`**

   <span data-ttu-id="401c6-116">Zakáže obnovení více balíčků paralelně.</span><span class="sxs-lookup"><span data-stu-id="401c6-116">Disables restoring multiple packages in parallel.</span></span>

- **`-FallbackSource`**

  <span data-ttu-id="401c6-117">*(3.2 +)* Seznam zdrojů balíčků, které se použijí jako záložní pro případ, že se balíček nenajde v primárním nebo výchozím zdroji.</span><span class="sxs-lookup"><span data-stu-id="401c6-117">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> <span data-ttu-id="401c6-118">K oddělení položek seznamu použijte středník.</span><span class="sxs-lookup"><span data-stu-id="401c6-118">Use a semicolon to separate list entries.</span></span>

- **`-Force`**

  <span data-ttu-id="401c6-119">V projektech založených na PackageReference vynutí vyřešení všech závislostí i v případě, že bylo poslední obnovení úspěšné.</span><span class="sxs-lookup"><span data-stu-id="401c6-119">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="401c6-120">Zadání tohoto příznaku se podobá odstranění `project.assets.json` souboru.</span><span class="sxs-lookup"><span data-stu-id="401c6-120">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="401c6-121">To neobejde mezipaměť HTTP-cache.</span><span class="sxs-lookup"><span data-stu-id="401c6-121">This does not bypass the http-cache.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="401c6-122">*(3.5 +)* Vynutí spuštění nuget.exe s využitím neutrální jazykové verze založené na angličtině.</span><span class="sxs-lookup"><span data-stu-id="401c6-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-ForceEvaluate`**

  <span data-ttu-id="401c6-123">Vynutí obnovení, aby se znovu vyhodnotily všechny závislosti i v případě, že soubor zámku již existuje.</span><span class="sxs-lookup"><span data-stu-id="401c6-123">Forces restore to reevaluate all dependencies even if a lock file already exists.</span></span>

- **`-?|-help`**

  <span data-ttu-id="401c6-124">Zobrazí informace o nápovědě k příkazu.</span><span class="sxs-lookup"><span data-stu-id="401c6-124">Displays help information for the command.</span></span>

- **`-LockFilePath`**

  <span data-ttu-id="401c6-125">Výstupní umístění, kde je zapsán soubor zámku projektu.</span><span class="sxs-lookup"><span data-stu-id="401c6-125">Output location where project lock file is written.</span></span> <span data-ttu-id="401c6-126">Ve výchozím nastavení je to `PROJECT_ROOT\packages.lock.json` .</span><span class="sxs-lookup"><span data-stu-id="401c6-126">By default, this is `PROJECT_ROOT\packages.lock.json`.</span></span>

- **`-LockedMode`**

  <span data-ttu-id="401c6-127">Nepovolujte aktualizaci souboru zámku projektu.</span><span class="sxs-lookup"><span data-stu-id="401c6-127">Don't allow updating project lock file.</span></span>

- **`-MSBuildPath`**

   <span data-ttu-id="401c6-128">*(4.0 +)* Určuje cestu nástroje MSBuild, který má být použit s příkazem, přičemž přednost využije `-MSBuildVersion` .</span><span class="sxs-lookup"><span data-stu-id="401c6-128">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="401c6-129">*(3.2 +)* Určuje verzi nástroje MSBuild, která má být použita s tímto příkazem.</span><span class="sxs-lookup"><span data-stu-id="401c6-129">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="401c6-130">Podporované hodnoty jsou 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="401c6-130">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="401c6-131">Ve výchozím nastavení je nástroj MSBuild v cestě vybrán, jinak má výchozí nejvyšší nainstalovanou verzi nástroje MSBuild.</span><span class="sxs-lookup"><span data-stu-id="401c6-131">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NoCache`**

  <span data-ttu-id="401c6-132">Zabraňuje balíčku NuGet v použití balíčků v mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="401c6-132">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="401c6-133">Viz [Správa globálních balíčků a složek mezipaměti](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="401c6-133">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="401c6-134">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="401c6-134">Suppresses prompts for user input or confirmations.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="401c6-135">Určuje složku, ve které jsou balíčky nainstalované.</span><span class="sxs-lookup"><span data-stu-id="401c6-135">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="401c6-136">Pokud není zadána žádná složka, je použita aktuální složka.</span><span class="sxs-lookup"><span data-stu-id="401c6-136">If no folder is specified, the current folder is used.</span></span> <span data-ttu-id="401c6-137">Vyžaduje se při obnovení `packages.config` souboru se souborem, pokud `PackagesDirectory` `SolutionDirectory` se nepoužívá nebo.</span><span class="sxs-lookup"><span data-stu-id="401c6-137">Required when restoring with a `packages.config` file unless `PackagesDirectory` or `SolutionDirectory` is used.</span></span>

- **`-PackageSaveMode`**

  <span data-ttu-id="401c6-138">Určuje typy souborů, které se uloží po instalaci balíčku: jedna z hodnot `nuspec` , `nupkg` nebo `nuspec;nupkg` .</span><span class="sxs-lookup"><span data-stu-id="401c6-138">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span>

- **`-PackagesDirectory`**

  <span data-ttu-id="401c6-139">Stejné jako `OutputDirectory` .</span><span class="sxs-lookup"><span data-stu-id="401c6-139">Same as `OutputDirectory`.</span></span> <span data-ttu-id="401c6-140">Vyžaduje se při obnovení `packages.config` souboru se souborem, pokud `OutputDirectory` `SolutionDirectory` se nepoužívá nebo.</span><span class="sxs-lookup"><span data-stu-id="401c6-140">Required when restoring with a `packages.config` file unless `OutputDirectory` or `SolutionDirectory` is used.</span></span>

- **`-Project2ProjectTimeOut`**

  <span data-ttu-id="401c6-141">Časový limit v sekundách pro řešení odkazů mezi projekty.</span><span class="sxs-lookup"><span data-stu-id="401c6-141">Timeout in seconds for resolving project-to-project references.</span></span>

- **`-Recursive`**

  <span data-ttu-id="401c6-142">*(4.0 +)* Obnoví všechny odkazy na projekty UWP a .NET Core.</span><span class="sxs-lookup"><span data-stu-id="401c6-142">*(4.0+)* Restores all references projects for UWP and .NET Core projects.</span></span> <span data-ttu-id="401c6-143">Neplatí pro projekty používající `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="401c6-143">Does not apply to projects using `packages.config`.</span></span>

- **`-RequireConsent`**

  <span data-ttu-id="401c6-144">Ověřuje, jestli je před stažením a instalací balíčků povolený obnovování balíčků.</span><span class="sxs-lookup"><span data-stu-id="401c6-144">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="401c6-145">Podrobnosti najdete v tématu věnovaném [obnovení balíčků](../../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="401c6-145">For details, see [Package Restore](../../consume-packages/package-restore.md).</span></span>

- **`-SolutionDirectory`**

  <span data-ttu-id="401c6-146">Určuje složku řešení.</span><span class="sxs-lookup"><span data-stu-id="401c6-146">Specifies the solution folder.</span></span> <span data-ttu-id="401c6-147">Neplatný při obnovování balíčků pro řešení.</span><span class="sxs-lookup"><span data-stu-id="401c6-147">Not valid when restoring packages for a solution.</span></span> <span data-ttu-id="401c6-148">Vyžaduje se při obnovení `packages.config` souboru se souborem, pokud `PackagesDirectory` `OutputDirectory` se nepoužívá nebo.</span><span class="sxs-lookup"><span data-stu-id="401c6-148">Required when restoring with a `packages.config` file unless `PackagesDirectory` or `OutputDirectory` is used.</span></span>

- **`-Source`**

  <span data-ttu-id="401c6-149">Určuje seznam zdrojů balíčků (jako adresy URL), které se mají použít pro obnovení.</span><span class="sxs-lookup"><span data-stu-id="401c6-149">Specifies the list of package sources (as URLs) to use for the restore.</span></span> <span data-ttu-id="401c6-150">Pokud tento příkaz vynecháte, použije se zdroje zadané v konfiguračních souborech, viz téma [Konfigurace chování NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="401c6-150">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="401c6-151">K oddělení položek seznamu použijte středník.</span><span class="sxs-lookup"><span data-stu-id="401c6-151">Use a semicolon to separate list entries.</span></span>

- **`-UseLockFile`**

  <span data-ttu-id="401c6-152">Povoluje vygenerování souboru zámku projektu a jeho použití s obnovením.</span><span class="sxs-lookup"><span data-stu-id="401c6-152">Enables project lock file to be generated and used with restore.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="401c6-153">Určuje množství podrobností zobrazených ve výstupu: `normal` (výchozí), `quiet` nebo `detailed` .</span><span class="sxs-lookup"><span data-stu-id="401c6-153">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="401c6-154">Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="401c6-154">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="remarks"></a><span data-ttu-id="401c6-155">Poznámky</span><span class="sxs-lookup"><span data-stu-id="401c6-155">Remarks</span></span>

<span data-ttu-id="401c6-156">Příkaz Restore provede následující kroky:</span><span class="sxs-lookup"><span data-stu-id="401c6-156">The restore command performs the following steps:</span></span>

1. <span data-ttu-id="401c6-157">Určete režim operace příkazu Restore.</span><span class="sxs-lookup"><span data-stu-id="401c6-157">Determine the operation mode of the restore command.</span></span>

   | <span data-ttu-id="401c6-158">typ souboru projectPath</span><span class="sxs-lookup"><span data-stu-id="401c6-158">projectPath file type</span></span> | <span data-ttu-id="401c6-159">Chování</span><span class="sxs-lookup"><span data-stu-id="401c6-159">Behavior</span></span> |
   | --- | --- |
   | <span data-ttu-id="401c6-160">Řešení (složka)</span><span class="sxs-lookup"><span data-stu-id="401c6-160">Solution (folder)</span></span> | <span data-ttu-id="401c6-161">NuGet vyhledá `.sln` soubor a použije ho, pokud se najde. v opačném případě se zobrazí chyba.</span><span class="sxs-lookup"><span data-stu-id="401c6-161">NuGet looks for a `.sln` file and uses that if found; otherwise gives an error.</span></span> <span data-ttu-id="401c6-162">`(SolutionDir)\.nuget` slouží jako spouštěcí složka.</span><span class="sxs-lookup"><span data-stu-id="401c6-162">`(SolutionDir)\.nuget` is used as the starting folder.</span></span> |
   | <span data-ttu-id="401c6-163">`.sln` souborů</span><span class="sxs-lookup"><span data-stu-id="401c6-163">`.sln` file</span></span> | <span data-ttu-id="401c6-164">Obnovit balíčky identifikované řešením; obsahuje chybu, pokud `-SolutionDirectory` se používá.</span><span class="sxs-lookup"><span data-stu-id="401c6-164">Restore packages identified by the solution; gives an error if `-SolutionDirectory` is used.</span></span> <span data-ttu-id="401c6-165">`$(SolutionDir)\.nuget` slouží jako spouštěcí složka.</span><span class="sxs-lookup"><span data-stu-id="401c6-165">`$(SolutionDir)\.nuget` is used as the starting folder.</span></span> |
   | <span data-ttu-id="401c6-166">`packages.config` nebo soubor projektu</span><span class="sxs-lookup"><span data-stu-id="401c6-166">`packages.config` or project file</span></span> | <span data-ttu-id="401c6-167">Obnovte balíčky uvedené v souboru, vyřešte je a nainstalujte závislosti.</span><span class="sxs-lookup"><span data-stu-id="401c6-167">Restore packages listed in the file, resolving and installing dependencies.</span></span> |
   | <span data-ttu-id="401c6-168">Jiný typ souboru</span><span class="sxs-lookup"><span data-stu-id="401c6-168">Other file type</span></span> | <span data-ttu-id="401c6-169">Předpokládá se, že se jedná o `.sln` soubor, který je uvedený výše. Pokud se nejedná o řešení, NuGet vyvolá chybu.</span><span class="sxs-lookup"><span data-stu-id="401c6-169">File is assumed to be a `.sln` file as above; if it's not a solution, NuGet gives an error.</span></span> |
   | <span data-ttu-id="401c6-170">(projectPath není zadáno)</span><span class="sxs-lookup"><span data-stu-id="401c6-170">(projectPath not specified)</span></span> | <ul><li><span data-ttu-id="401c6-171">NuGet vyhledá soubory řešení v aktuální složce.</span><span class="sxs-lookup"><span data-stu-id="401c6-171">NuGet looks for solution files in the current folder.</span></span> <span data-ttu-id="401c6-172">Pokud se najde jeden soubor, použije se k obnovení balíčků. Pokud je nalezeno více řešení, NuGet vyvolá chybu.</span><span class="sxs-lookup"><span data-stu-id="401c6-172">If a single file is found, that one is used to restore packages; if multiple solutions are found, NuGet gives an error.</span></span></li><li><span data-ttu-id="401c6-173">Pokud neexistují žádné soubory řešení, NuGet vyhledá `packages.config` a použije k obnovení balíčků.</span><span class="sxs-lookup"><span data-stu-id="401c6-173">If there are no solution files, NuGet looks for a `packages.config` and uses that to restore packages.</span></span></li><li><span data-ttu-id="401c6-174">Pokud se nenajde žádné řešení nebo `packages.config` soubor, NuGet vyvolá chybu.</span><span class="sxs-lookup"><span data-stu-id="401c6-174">If no solution or `packages.config` file is found, NuGet gives an error.</span></span></ul> |

2. <span data-ttu-id="401c6-175">Určení složky balíčků pomocí následujícího pořadí priorit (Pokud žádná z těchto složek nenalezne, vyvolá chybu NuGet):</span><span class="sxs-lookup"><span data-stu-id="401c6-175">Determine the packages folder using the following priority order (NuGet gives an error if none of these folders are found):</span></span>

    - <span data-ttu-id="401c6-176">Složka zadaná s parametrem `-PackagesDirectory` .</span><span class="sxs-lookup"><span data-stu-id="401c6-176">The folder specified with `-PackagesDirectory`.</span></span>
    - <span data-ttu-id="401c6-177">`repositoryPath`Hodnota v`Nuget.Config`</span><span class="sxs-lookup"><span data-stu-id="401c6-177">The `repositoryPath` value in `Nuget.Config`</span></span>
    - <span data-ttu-id="401c6-178">Složka zadaná s `-SolutionDirectory`</span><span class="sxs-lookup"><span data-stu-id="401c6-178">The folder specified with `-SolutionDirectory`</span></span>
    - `$(SolutionDir)\packages`

3. <span data-ttu-id="401c6-179">Při obnovování balíčků pro řešení provede NuGet následující:</span><span class="sxs-lookup"><span data-stu-id="401c6-179">When restoring packages for a solution, NuGet does the following:</span></span>
    - <span data-ttu-id="401c6-180">Načte soubor řešení.</span><span class="sxs-lookup"><span data-stu-id="401c6-180">Loads the solution file.</span></span>
    - <span data-ttu-id="401c6-181">Obnoví balíčky na úrovni řešení uvedené v `$(SolutionDir)\.nuget\packages.config` části do `packages` složky.</span><span class="sxs-lookup"><span data-stu-id="401c6-181">Restores solution level packages listed in `$(SolutionDir)\.nuget\packages.config` into the `packages` folder.</span></span>
    - <span data-ttu-id="401c6-182">Obnovte balíčky uvedené v `$(ProjectDir)\packages.config` části do `packages` složky.</span><span class="sxs-lookup"><span data-stu-id="401c6-182">Restore packages listed in `$(ProjectDir)\packages.config` into the `packages` folder.</span></span> <span data-ttu-id="401c6-183">Pro každý zadaný balíček obnovte balíček paralelně, pokud `-DisableParallelProcessing` není zadaný.</span><span class="sxs-lookup"><span data-stu-id="401c6-183">For each package specified, restore the package in parallel unless `-DisableParallelProcessing` is specified.</span></span>

## <a name="examples"></a><span data-ttu-id="401c6-184">Příklady</span><span class="sxs-lookup"><span data-stu-id="401c6-184">Examples</span></span>

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
