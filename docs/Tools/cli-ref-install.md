---
title: Příkaz instalovat NuGet rozhraní příkazového řádku | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referenční dokumentace pro příkaz nuget.exe instalace
keywords: nuget nainstalujte odkaz, nainstalujte balíček příkaz
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 121d7b50767f1d466d6d0d8494f324b02d8ff6f1
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="19821-104">nainstalovat příkaz (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="19821-104">install command (NuGet CLI)</span></span>

<span data-ttu-id="19821-105">**Platí pro:** balíček spotřeba &bullet; **podporované verze:** všechny</span><span class="sxs-lookup"><span data-stu-id="19821-105">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="19821-106">Stáhne a nainstaluje balíček do projektu, jako výchozí bude použit na aktuální složku, pomocí zadaného balíčku zdroje.</span><span class="sxs-lookup"><span data-stu-id="19821-106">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="19821-107">Stažení balíčku přímo mimo kontext projektu, navštivte stránku balíčku na [nuget.org](https://www.nuget.org) a vyberte **Stáhnout** odkaz.</span><span class="sxs-lookup"><span data-stu-id="19821-107">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span>

<span data-ttu-id="19821-108">Pokud nejsou zadány žádné zdroje, ty uvedené v souboru globální konfiguraci `%appdata%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), se používají.</span><span class="sxs-lookup"><span data-stu-id="19821-108">If no sources are specified, those listed in the global configuration file, `%appdata%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), are used.</span></span> <span data-ttu-id="19821-109">V tématu [konfigurace NuGet chování](../consume-packages/configuring-nuget-behavior.md) další podrobnosti.</span><span class="sxs-lookup"><span data-stu-id="19821-109">See [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="19821-110">Pokud nejsou zadány žádné konkrétní balíčky, `install` nainstaluje všechny balíčky uvedené v projektu `packages.config` souboru, takže je podobná [ `restore` ](cli-ref-restore.md).</span><span class="sxs-lookup"><span data-stu-id="19821-110">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](cli-ref-restore.md).</span></span>

<span data-ttu-id="19821-111">`install` Příkaz nedojde ke změně souboru projektu nebo `packages.config`; tímto způsobem je podobná `restore` v tom pouze přidá balíčky na disk ale nemění závislosti projektu.</span><span class="sxs-lookup"><span data-stu-id="19821-111">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="19821-112">Pokud chcete přidat závislost, přidejte projektu přes uživatelské rozhraní Správce balíčků nebo konzoly v sadě Visual Studio nebo upravit `packages.config` a spusťte buď `install` nebo `restore`.</span><span class="sxs-lookup"><span data-stu-id="19821-112">To add a dependency, either add a project through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="19821-113">Použití</span><span class="sxs-lookup"><span data-stu-id="19821-113">Usage</span></span>

```cli
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="19821-114">kde `<packageID>` názvy balíček k instalaci (pomocí nejnovější verze), nebo `<configFilePath>` identifikuje `packages.config` soubor, který obsahuje seznam balíčků, chcete-li nainstalovat.</span><span class="sxs-lookup"><span data-stu-id="19821-114">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="19821-115">Můžete určit, na konkrétní verzi pomocí `-Version` možnost.</span><span class="sxs-lookup"><span data-stu-id="19821-115">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="19821-116">Možnosti</span><span class="sxs-lookup"><span data-stu-id="19821-116">Options</span></span>

| <span data-ttu-id="19821-117">Možnost</span><span class="sxs-lookup"><span data-stu-id="19821-117">Option</span></span> | <span data-ttu-id="19821-118">Popis</span><span class="sxs-lookup"><span data-stu-id="19821-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="19821-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="19821-119">ConfigFile</span></span> | <span data-ttu-id="19821-120">Konfigurační soubor NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="19821-120">The NuGet configuration file to apply.</span></span> <span data-ttu-id="19821-121">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.</span><span class="sxs-lookup"><span data-stu-id="19821-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="19821-122">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="19821-122">DependencyVersion</span></span> | <span data-ttu-id="19821-123">*(4.4 +)*  Určuje konkrétní verzi, přepisování výchozího chování řešení závislostí.</span><span class="sxs-lookup"><span data-stu-id="19821-123">*(4.4+)* Specifies a specific version, overriding the default dependency resolution behavior.</span></span> |
| <span data-ttu-id="19821-124">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="19821-124">DisableParallelProcessing</span></span> | <span data-ttu-id="19821-125">Zakáže instalaci více balíčků paralelně.</span><span class="sxs-lookup"><span data-stu-id="19821-125">Disables installing multiple packages in parallel.</span></span> |
| <span data-ttu-id="19821-126">ExcludeVersion</span><span class="sxs-lookup"><span data-stu-id="19821-126">ExcludeVersion</span></span> | <span data-ttu-id="19821-127">Nainstaluje balíček do složky s názvem se pouze název balíčku a není číslo verze.</span><span class="sxs-lookup"><span data-stu-id="19821-127">Installs the package to a folder named with only the package name and not the version number.</span></span> |
| <span data-ttu-id="19821-128">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="19821-128">FallbackSource</span></span> | <span data-ttu-id="19821-129">*(3.2 +)*  Seznam zdroje balíčku pro použití jako případech přejít v případě, že daný balíček nebyl nalezen v primární nebo výchozí zdroj.</span><span class="sxs-lookup"><span data-stu-id="19821-129">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="19821-130">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="19821-130">ForceEnglishOutput</span></span> | <span data-ttu-id="19821-131">*(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze.</span><span class="sxs-lookup"><span data-stu-id="19821-131">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="19821-132">Rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="19821-132">Framework</span></span> | <span data-ttu-id="19821-133">*(4.4 +)*  Cílovém Frameworku, který slouží k výběru závislosti.</span><span class="sxs-lookup"><span data-stu-id="19821-133">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="19821-134">Výchozí hodnota je 'Libovolný' není-li zadána.</span><span class="sxs-lookup"><span data-stu-id="19821-134">Defaults to 'Any' if not specified.</span></span> |
| <span data-ttu-id="19821-135">Nápověda</span><span class="sxs-lookup"><span data-stu-id="19821-135">Help</span></span> | <span data-ttu-id="19821-136">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="19821-136">Displays help information for the command.</span></span> |
| <span data-ttu-id="19821-137">NoCache</span><span class="sxs-lookup"><span data-stu-id="19821-137">NoCache</span></span> | <span data-ttu-id="19821-138">NuGet bránit v použití balíčky v mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="19821-138">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="19821-139">V tématu [správy globální balíčky a složky mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="19821-139">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="19821-140">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="19821-140">NonInteractive</span></span> | <span data-ttu-id="19821-141">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="19821-141">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="19821-142">Výstupnísložka</span><span class="sxs-lookup"><span data-stu-id="19821-142">OutputDirectory</span></span> | <span data-ttu-id="19821-143">Určuje složku, ve kterém jsou nainstalované balíčky.</span><span class="sxs-lookup"><span data-stu-id="19821-143">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="19821-144">Pokud není zadaný žádný složky, se používá aktuální složky.</span><span class="sxs-lookup"><span data-stu-id="19821-144">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="19821-145">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="19821-145">PackageSaveMode</span></span> | <span data-ttu-id="19821-146">Určuje typy souborů, uložte po instalaci balíčku: jeden z `nuspec`, `nupkg`, nebo `nuspec;nupkg`.</span><span class="sxs-lookup"><span data-stu-id="19821-146">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="19821-147">Předběžné verze</span><span class="sxs-lookup"><span data-stu-id="19821-147">PreRelease</span></span> | <span data-ttu-id="19821-148">Umožňuje předběžné verze balíčků k instalaci.</span><span class="sxs-lookup"><span data-stu-id="19821-148">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="19821-149">Tento příznak není požadována, když probíhá obnovení balíčků s `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="19821-149">This flag is not required when restoring packages with `packages.config`.</span></span> |
| <span data-ttu-id="19821-150">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="19821-150">RequireConsent</span></span> | <span data-ttu-id="19821-151">Ověří, že probíhá obnovení balíčků je zapnutá před stažením a instalací balíčky.</span><span class="sxs-lookup"><span data-stu-id="19821-151">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="19821-152">Podrobnosti najdete v tématu [obnovení balíčků](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="19821-152">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="19821-153">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="19821-153">SolutionDirectory</span></span> | <span data-ttu-id="19821-154">Určuje kořenové složky řešení pro pro obnovení balíčků.</span><span class="sxs-lookup"><span data-stu-id="19821-154">Specifies root folder of the solution for which to restore packages.</span></span> |
| <span data-ttu-id="19821-155">Zdroj</span><span class="sxs-lookup"><span data-stu-id="19821-155">Source</span></span> | <span data-ttu-id="19821-156">Určuje seznam zdrojů balíčku (jako adresy URL) používat.</span><span class="sxs-lookup"><span data-stu-id="19821-156">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="19821-157">Pokud tento parametr vynechán, příkaz používá zdrojů, součástí konfigurační soubory, najdete v části [konfigurace NuGet chování](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="19821-157">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="19821-158">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="19821-158">Verbosity</span></span> | <span data-ttu-id="19821-159">Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="19821-159">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="19821-160">Version</span><span class="sxs-lookup"><span data-stu-id="19821-160">Version</span></span> | <span data-ttu-id="19821-161">Určuje verzi balíčku pro instalaci.</span><span class="sxs-lookup"><span data-stu-id="19821-161">Specifies the version of the package to install.</span></span> |

<span data-ttu-id="19821-162">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="19821-162">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="19821-163">Příklady</span><span class="sxs-lookup"><span data-stu-id="19821-163">Examples</span></span>

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
