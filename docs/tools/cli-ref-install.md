---
title: Příkaz instalace rozhraní příkazového řádku NuGet
description: Referenční dokumentace pro příkaz nuget.exe instalace
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 615f2beca1eb288417f2345fcdf25e323942d300
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="3c9fd-103">Příkaz install (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="3c9fd-103">install command (NuGet CLI)</span></span>

<span data-ttu-id="3c9fd-104">**Platí pro:** balíček spotřeba &bullet; **podporované verze:** všechny</span><span class="sxs-lookup"><span data-stu-id="3c9fd-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="3c9fd-105">Stáhne a nainstaluje balíček do projektu, jako výchozí bude použit na aktuální složku, pomocí zadaného balíčku zdroje.</span><span class="sxs-lookup"><span data-stu-id="3c9fd-105">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="3c9fd-106">Stažení balíčku přímo mimo kontext projektu, navštivte stránku balíčku na [nuget.org](https://www.nuget.org) a vyberte **Stáhnout** odkaz.</span><span class="sxs-lookup"><span data-stu-id="3c9fd-106">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span>

<span data-ttu-id="3c9fd-107">Pokud nejsou zadány žádné zdroje, ty uvedené v souboru globální konfiguraci `%appdata%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), se používají.</span><span class="sxs-lookup"><span data-stu-id="3c9fd-107">If no sources are specified, those listed in the global configuration file, `%appdata%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), are used.</span></span> <span data-ttu-id="3c9fd-108">V tématu [konfigurace NuGet chování](../consume-packages/configuring-nuget-behavior.md) další podrobnosti.</span><span class="sxs-lookup"><span data-stu-id="3c9fd-108">See [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="3c9fd-109">Pokud nejsou zadány žádné konkrétní balíčky, `install` nainstaluje všechny balíčky uvedené v projektu `packages.config` souboru, takže je podobná [ `restore` ](cli-ref-restore.md).</span><span class="sxs-lookup"><span data-stu-id="3c9fd-109">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](cli-ref-restore.md).</span></span>

<span data-ttu-id="3c9fd-110">`install` Příkaz nedojde ke změně souboru projektu nebo `packages.config`; tímto způsobem je podobná `restore` v tom pouze přidá balíčky na disk ale nemění závislosti projektu.</span><span class="sxs-lookup"><span data-stu-id="3c9fd-110">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="3c9fd-111">Pokud chcete přidat závislost, přidejte projektu přes uživatelské rozhraní Správce balíčků nebo konzoly v sadě Visual Studio nebo upravit `packages.config` a spusťte buď `install` nebo `restore`.</span><span class="sxs-lookup"><span data-stu-id="3c9fd-111">To add a dependency, either add a project through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="3c9fd-112">Použití</span><span class="sxs-lookup"><span data-stu-id="3c9fd-112">Usage</span></span>

```cli
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="3c9fd-113">kde `<packageID>` názvy balíček k instalaci (pomocí nejnovější verze), nebo `<configFilePath>` identifikuje `packages.config` soubor, který obsahuje seznam balíčků, chcete-li nainstalovat.</span><span class="sxs-lookup"><span data-stu-id="3c9fd-113">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="3c9fd-114">Můžete určit, na konkrétní verzi pomocí `-Version` možnost.</span><span class="sxs-lookup"><span data-stu-id="3c9fd-114">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="3c9fd-115">Možnosti</span><span class="sxs-lookup"><span data-stu-id="3c9fd-115">Options</span></span>

| <span data-ttu-id="3c9fd-116">Možnost</span><span class="sxs-lookup"><span data-stu-id="3c9fd-116">Option</span></span> | <span data-ttu-id="3c9fd-117">Popis</span><span class="sxs-lookup"><span data-stu-id="3c9fd-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3c9fd-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="3c9fd-118">ConfigFile</span></span> | <span data-ttu-id="3c9fd-119">Konfigurační soubor NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="3c9fd-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="3c9fd-120">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.</span><span class="sxs-lookup"><span data-stu-id="3c9fd-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="3c9fd-121">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="3c9fd-121">DependencyVersion</span></span> | <span data-ttu-id="3c9fd-122">*(4.4 +)*  Určuje konkrétní verzi, přepisování výchozího chování řešení závislostí.</span><span class="sxs-lookup"><span data-stu-id="3c9fd-122">*(4.4+)* Specifies a specific version, overriding the default dependency resolution behavior.</span></span> |
| <span data-ttu-id="3c9fd-123">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="3c9fd-123">DisableParallelProcessing</span></span> | <span data-ttu-id="3c9fd-124">Zakáže instalaci více balíčků paralelně.</span><span class="sxs-lookup"><span data-stu-id="3c9fd-124">Disables installing multiple packages in parallel.</span></span> |
| <span data-ttu-id="3c9fd-125">ExcludeVersion</span><span class="sxs-lookup"><span data-stu-id="3c9fd-125">ExcludeVersion</span></span> | <span data-ttu-id="3c9fd-126">Nainstaluje balíček do složky s názvem se pouze název balíčku a není číslo verze.</span><span class="sxs-lookup"><span data-stu-id="3c9fd-126">Installs the package to a folder named with only the package name and not the version number.</span></span> |
| <span data-ttu-id="3c9fd-127">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="3c9fd-127">FallbackSource</span></span> | <span data-ttu-id="3c9fd-128">*(3.2 +)*  Seznam zdroje balíčku pro použití jako případech přejít v případě, že daný balíček nebyl nalezen v primární nebo výchozí zdroj.</span><span class="sxs-lookup"><span data-stu-id="3c9fd-128">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="3c9fd-129">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="3c9fd-129">ForceEnglishOutput</span></span> | <span data-ttu-id="3c9fd-130">*(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze.</span><span class="sxs-lookup"><span data-stu-id="3c9fd-130">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="3c9fd-131">Rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="3c9fd-131">Framework</span></span> | <span data-ttu-id="3c9fd-132">*(4.4 +)*  Cílovém Frameworku, který slouží k výběru závislosti.</span><span class="sxs-lookup"><span data-stu-id="3c9fd-132">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="3c9fd-133">Výchozí hodnota je 'Libovolný' není-li zadána.</span><span class="sxs-lookup"><span data-stu-id="3c9fd-133">Defaults to 'Any' if not specified.</span></span> |
| <span data-ttu-id="3c9fd-134">Nápověda</span><span class="sxs-lookup"><span data-stu-id="3c9fd-134">Help</span></span> | <span data-ttu-id="3c9fd-135">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="3c9fd-135">Displays help information for the command.</span></span> |
| <span data-ttu-id="3c9fd-136">NoCache</span><span class="sxs-lookup"><span data-stu-id="3c9fd-136">NoCache</span></span> | <span data-ttu-id="3c9fd-137">NuGet bránit v použití balíčky v mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="3c9fd-137">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="3c9fd-138">V tématu [správy globální balíčky a složky mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="3c9fd-138">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="3c9fd-139">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="3c9fd-139">NonInteractive</span></span> | <span data-ttu-id="3c9fd-140">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="3c9fd-140">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="3c9fd-141">Výstupnísložka</span><span class="sxs-lookup"><span data-stu-id="3c9fd-141">OutputDirectory</span></span> | <span data-ttu-id="3c9fd-142">Určuje složku, ve kterém jsou nainstalované balíčky.</span><span class="sxs-lookup"><span data-stu-id="3c9fd-142">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="3c9fd-143">Pokud není zadaný žádný složky, se používá aktuální složky.</span><span class="sxs-lookup"><span data-stu-id="3c9fd-143">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="3c9fd-144">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="3c9fd-144">PackageSaveMode</span></span> | <span data-ttu-id="3c9fd-145">Určuje typy souborů, uložte po instalaci balíčku: jeden z `nuspec`, `nupkg`, nebo `nuspec;nupkg`.</span><span class="sxs-lookup"><span data-stu-id="3c9fd-145">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="3c9fd-146">Předběžné verze</span><span class="sxs-lookup"><span data-stu-id="3c9fd-146">PreRelease</span></span> | <span data-ttu-id="3c9fd-147">Umožňuje předběžné verze balíčků k instalaci.</span><span class="sxs-lookup"><span data-stu-id="3c9fd-147">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="3c9fd-148">Tento příznak není požadována, když probíhá obnovení balíčků s `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="3c9fd-148">This flag is not required when restoring packages with `packages.config`.</span></span> |
| <span data-ttu-id="3c9fd-149">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="3c9fd-149">RequireConsent</span></span> | <span data-ttu-id="3c9fd-150">Ověří, že probíhá obnovení balíčků je zapnutá před stažením a instalací balíčky.</span><span class="sxs-lookup"><span data-stu-id="3c9fd-150">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="3c9fd-151">Podrobnosti najdete v tématu [obnovení balíčků](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="3c9fd-151">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="3c9fd-152">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="3c9fd-152">SolutionDirectory</span></span> | <span data-ttu-id="3c9fd-153">Určuje kořenové složky řešení pro pro obnovení balíčků.</span><span class="sxs-lookup"><span data-stu-id="3c9fd-153">Specifies root folder of the solution for which to restore packages.</span></span> |
| <span data-ttu-id="3c9fd-154">Zdroj</span><span class="sxs-lookup"><span data-stu-id="3c9fd-154">Source</span></span> | <span data-ttu-id="3c9fd-155">Určuje seznam zdrojů balíčku (jako adresy URL) používat.</span><span class="sxs-lookup"><span data-stu-id="3c9fd-155">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="3c9fd-156">Pokud tento parametr vynechán, příkaz používá zdrojů, součástí konfigurační soubory, najdete v části [konfigurace NuGet chování](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="3c9fd-156">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="3c9fd-157">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="3c9fd-157">Verbosity</span></span> | <span data-ttu-id="3c9fd-158">Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="3c9fd-158">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="3c9fd-159">Version</span><span class="sxs-lookup"><span data-stu-id="3c9fd-159">Version</span></span> | <span data-ttu-id="3c9fd-160">Určuje verzi balíčku pro instalaci.</span><span class="sxs-lookup"><span data-stu-id="3c9fd-160">Specifies the version of the package to install.</span></span> |

<span data-ttu-id="3c9fd-161">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="3c9fd-161">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="3c9fd-162">Příklady</span><span class="sxs-lookup"><span data-stu-id="3c9fd-162">Examples</span></span>

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
