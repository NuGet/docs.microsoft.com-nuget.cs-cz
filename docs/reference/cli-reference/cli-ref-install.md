---
title: Instalační příkaz NuGet CLI
description: Referenční informace k příkazu nuget.exe Install
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 34b79bfa7a0dddf5da6b5c465293caec49129f6c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779260"
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="ba72d-103">Install – příkaz (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="ba72d-103">install command (NuGet CLI)</span></span>

<span data-ttu-id="ba72d-104">**Platí pro:** &bullet; **podporované verze balíčku:** vše</span><span class="sxs-lookup"><span data-stu-id="ba72d-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="ba72d-105">Stáhne a nainstaluje balíček do projektu, přičemž se použije jako výchozí pro aktuální složku pomocí zadaných zdrojů balíčků.</span><span class="sxs-lookup"><span data-stu-id="ba72d-105">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="ba72d-106">Chcete-li stáhnout balíček přímo mimo kontext projektu, navštivte stránku balíčku na [NuGet.org](https://www.nuget.org) a vyberte odkaz **ke stažení** .</span><span class="sxs-lookup"><span data-stu-id="ba72d-106">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span>

<span data-ttu-id="ba72d-107">Pokud nejsou zadány žádné zdroje, budou použity hodnoty uvedené v globálním konfiguračním souboru `%appdata%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="ba72d-107">If no sources are specified, those listed in the global configuration file, `%appdata%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), are used.</span></span> <span data-ttu-id="ba72d-108">Další podrobnosti najdete v tématu [běžné konfigurace NuGet](../../consume-packages/configuring-nuget-behavior.md) .</span><span class="sxs-lookup"><span data-stu-id="ba72d-108">See [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="ba72d-109">Pokud nejsou zadány žádné konkrétní balíčky, aplikace `install` nainstaluje všechny balíčky uvedené v `packages.config` souboru projektu a bude tak vypadat podobně jako [`restore`](cli-ref-restore.md) .</span><span class="sxs-lookup"><span data-stu-id="ba72d-109">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](cli-ref-restore.md).</span></span>

<span data-ttu-id="ba72d-110">`install`Příkaz neupraví soubor projektu nebo `packages.config` ; tímto způsobem je podobný jako `restore` v tom, že přidá pouze balíčky na disk, ale nemění závislosti projektu.</span><span class="sxs-lookup"><span data-stu-id="ba72d-110">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="ba72d-111">Chcete-li přidat závislost, buď přidejte balíček prostřednictvím uživatelského rozhraní nebo konzoly Správce balíčků v aplikaci Visual Studio, nebo upravte `packages.config` a potom spusťte buď `install` nebo `restore` .</span><span class="sxs-lookup"><span data-stu-id="ba72d-111">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="ba72d-112">Využití</span><span class="sxs-lookup"><span data-stu-id="ba72d-112">Usage</span></span>

```cli
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="ba72d-113">kde `<packageID>` pojmenuje balíček k instalaci (pomocí nejnovější verze) nebo `<configFilePath>` identifikuje `packages.config` soubor, který obsahuje seznam balíčků, které se mají nainstalovat.</span><span class="sxs-lookup"><span data-stu-id="ba72d-113">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="ba72d-114">Můžete určit konkrétní verzi s `-Version` možností.</span><span class="sxs-lookup"><span data-stu-id="ba72d-114">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="ba72d-115">Možnosti</span><span class="sxs-lookup"><span data-stu-id="ba72d-115">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="ba72d-116">Konfigurační soubor NuGet, který se má použít</span><span class="sxs-lookup"><span data-stu-id="ba72d-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ba72d-117">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows) nebo `~/.nuget/NuGet/NuGet.Config` nebo `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="ba72d-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-DependencyVersion`**

  <span data-ttu-id="ba72d-118">*(4.4 +)* Verze balíčků závislostí, které se mají použít, což může být jedna z následujících:</span><span class="sxs-lookup"><span data-stu-id="ba72d-118">*(4.4+)* The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="ba72d-119">*Nejnižší* (výchozí): nejnižší verze</span><span class="sxs-lookup"><span data-stu-id="ba72d-119">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="ba72d-120">*HighestPatch*: verze, která má nejnižší hlavní, nejnižší podverzi, nejvyšší opravu</span><span class="sxs-lookup"><span data-stu-id="ba72d-120">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="ba72d-121">*HighestMinor*: verze s nejnižší hlavní, nejvyšší podverze a nejvyšší opravou</span><span class="sxs-lookup"><span data-stu-id="ba72d-121">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="ba72d-122">*Nejvyšší*: nejvyšší verze</span><span class="sxs-lookup"><span data-stu-id="ba72d-122">*Highest*: the highest version</span></span></li><li><span data-ttu-id="ba72d-123">*Ignorovat*: nebudou použity žádné balíčky závislostí.</span><span class="sxs-lookup"><span data-stu-id="ba72d-123">*Ignore*: No dependency packages will be used</span></span></li></ul>

- **`-DirectDownload`**

  <span data-ttu-id="ba72d-124">Přímo si stáhněte bez naplnění jakýchkoli mezipamětí s metadaty nebo binárními soubory.</span><span class="sxs-lookup"><span data-stu-id="ba72d-124">Download directly without populating any caches with metadata or binaries.</span></span>

- **`-DisableParallelProcessing`**

  <span data-ttu-id="ba72d-125">Zakáže instalaci více balíčků paralelně.</span><span class="sxs-lookup"><span data-stu-id="ba72d-125">Disables installing multiple packages in parallel.</span></span>

- **`-x|-ExcludeVersion`**

  <span data-ttu-id="ba72d-126">Nainstaluje balíček do složky s názvem pouze s názvem balíčku a číslem verze.</span><span class="sxs-lookup"><span data-stu-id="ba72d-126">Installs the package to a folder named with only the package name and not the version number.</span></span>

- **`-FallbackSource`**

  <span data-ttu-id="ba72d-127">*(3.2 +)* Seznam zdrojů balíčků, které se použijí jako záložní pro případ, že se balíček nenajde v primárním nebo výchozím zdroji.</span><span class="sxs-lookup"><span data-stu-id="ba72d-127">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="ba72d-128">*(3.5 +)* Vynutí spuštění nuget.exe s využitím neutrální jazykové verze založené na angličtině.</span><span class="sxs-lookup"><span data-stu-id="ba72d-128">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-Framework`**

  <span data-ttu-id="ba72d-129">*(4.4 +)* Cílové rozhraní, které se používá pro výběr závislostí.</span><span class="sxs-lookup"><span data-stu-id="ba72d-129">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="ba72d-130">Pokud není zadaný, použije se výchozí hodnota any.</span><span class="sxs-lookup"><span data-stu-id="ba72d-130">Defaults to 'Any' if not specified.</span></span>

- **`-?|-help`**

  <span data-ttu-id="ba72d-131">Zobrazí informace o nápovědě k příkazu.</span><span class="sxs-lookup"><span data-stu-id="ba72d-131">Displays help information for the command.</span></span>

- **`-NoCache`**

  <span data-ttu-id="ba72d-132">Zabraňuje balíčku NuGet v použití balíčků v mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="ba72d-132">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="ba72d-133">Viz [Správa globálních balíčků a složek mezipaměti](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="ba72d-133">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="ba72d-134">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="ba72d-134">Suppresses prompts for user input or confirmations.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="ba72d-135">Určuje složku, ve které jsou balíčky nainstalované.</span><span class="sxs-lookup"><span data-stu-id="ba72d-135">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="ba72d-136">Pokud není zadána žádná složka, je použita aktuální složka.</span><span class="sxs-lookup"><span data-stu-id="ba72d-136">If no folder is specified, the current folder is used.</span></span>

- **`-PackageSaveMode`**

  <span data-ttu-id="ba72d-137">Určuje typy souborů, které se uloží po instalaci balíčku: jedna z hodnot `nuspec` , `nupkg` nebo `nuspec;nupkg` .</span><span class="sxs-lookup"><span data-stu-id="ba72d-137">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="ba72d-138">Umožňuje instalaci předprodejních balíčků.</span><span class="sxs-lookup"><span data-stu-id="ba72d-138">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="ba72d-139">Tento příznak není požadován při obnovování balíčků pomocí `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="ba72d-139">This flag is not required when restoring packages with `packages.config`.</span></span>

- **`-RequireConsent`**

  <span data-ttu-id="ba72d-140">Ověřuje, jestli je před stažením a instalací balíčků povolený obnovování balíčků.</span><span class="sxs-lookup"><span data-stu-id="ba72d-140">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="ba72d-141">Podrobnosti najdete v tématu věnovaném [obnovení balíčků](../../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="ba72d-141">For details, see [Package Restore](../../consume-packages/package-restore.md).</span></span>

- **`-SolutionDirectory`**

  <span data-ttu-id="ba72d-142">Určuje kořenovou složku řešení, pro kterou mají být balíčky obnoveny.</span><span class="sxs-lookup"><span data-stu-id="ba72d-142">Specifies root folder of the solution for which to restore packages.</span></span>

- **`-Source`**

   <span data-ttu-id="ba72d-143">Určuje seznam zdrojů balíčků (jako adresy URL), které se mají použít.</span><span class="sxs-lookup"><span data-stu-id="ba72d-143">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="ba72d-144">Pokud je tato hodnota vynechána, příkaz použije zdroje zadané v konfiguračních souborech, viz [běžné konfigurace NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="ba72d-144">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="ba72d-145">Určuje množství podrobností zobrazených ve výstupu: `normal` (výchozí), `quiet` nebo `detailed` .</span><span class="sxs-lookup"><span data-stu-id="ba72d-145">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="ba72d-146">Určuje verzi balíčku, který se má nainstalovat.</span><span class="sxs-lookup"><span data-stu-id="ba72d-146">Specifies the version of the package to install.</span></span>

<span data-ttu-id="ba72d-147">Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="ba72d-147">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ba72d-148">Příklady</span><span class="sxs-lookup"><span data-stu-id="ba72d-148">Examples</span></span>

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
