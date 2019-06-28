---
title: Aktualizace příkazu rozhraní příkazového řádku NuGet
description: Referenční informace pro příkaz update nuget.exe
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a242d02a54fd86899cbe274ab63538b53307c1bb
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67425922"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="2c8f5-103">Příkaz update (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="2c8f5-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="2c8f5-104">**Platí pro:** balíček spotřeby &bullet; **podporované verze:** všechny</span><span class="sxs-lookup"><span data-stu-id="2c8f5-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="2c8f5-105">Aktualizuje všechny balíčky v projektu (pomocí `packages.config`) jejich nejnovější dostupné verze.</span><span class="sxs-lookup"><span data-stu-id="2c8f5-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="2c8f5-106">Doporučuje se spouštět ["obnovit"](cli-ref-restore.md) dřív, než spustíte `update`.</span><span class="sxs-lookup"><span data-stu-id="2c8f5-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="2c8f5-107">(K aktualizaci jednotlivých balíčků, použijte [ `nuget install` ](cli-ref-install.md) bez zadání číslo verze, ve kterém případu NuGet nainstaluje nejnovější verzi.)</span><span class="sxs-lookup"><span data-stu-id="2c8f5-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="2c8f5-108">Poznámka: `update` nefunguje pro rozhraní příkazového řádku s mono (Mac OS x nebo Linux) nebo při použití formátu PackageReference.</span><span class="sxs-lookup"><span data-stu-id="2c8f5-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="2c8f5-109">`update` Příkaz aktualizuje také odkazy na sestavení v souboru projektu, pokud jsou již odkazuje existovat.</span><span class="sxs-lookup"><span data-stu-id="2c8f5-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="2c8f5-110">Pokud aktualizovaný balíček má přidání sestavení, je nový odkaz *není* přidán.</span><span class="sxs-lookup"><span data-stu-id="2c8f5-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="2c8f5-111">Nové závislosti balíčků také nemají přidání jejich odkazů na sestavení.</span><span class="sxs-lookup"><span data-stu-id="2c8f5-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="2c8f5-112">Chcete-li zahrnout tyto operace aktualizace, aktualizujte balíček v sadě Visual Studio pomocí uživatelského rozhraní Správce balíčků nebo konzole Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="2c8f5-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="2c8f5-113">Tento příkaz slouží také k aktualizaci nuget.exe samotný pomocí *-self* příznak.</span><span class="sxs-lookup"><span data-stu-id="2c8f5-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="2c8f5-114">Použití</span><span class="sxs-lookup"><span data-stu-id="2c8f5-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="2c8f5-115">kde `<configPath>` identifikuje buď `packages.config` nebo soubor řešení, která obsahuje seznam závislostí projektu.</span><span class="sxs-lookup"><span data-stu-id="2c8f5-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="2c8f5-116">Možnosti</span><span class="sxs-lookup"><span data-stu-id="2c8f5-116">Options</span></span>

| <span data-ttu-id="2c8f5-117">Možnost</span><span class="sxs-lookup"><span data-stu-id="2c8f5-117">Option</span></span> | <span data-ttu-id="2c8f5-118">Popis</span><span class="sxs-lookup"><span data-stu-id="2c8f5-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2c8f5-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="2c8f5-119">ConfigFile</span></span> | <span data-ttu-id="2c8f5-120">Konfigurační soubor NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="2c8f5-120">The NuGet configuration file to apply.</span></span> <span data-ttu-id="2c8f5-121">Pokud není zadán, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.</span><span class="sxs-lookup"><span data-stu-id="2c8f5-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="2c8f5-122">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="2c8f5-122">FileConflictAction</span></span> | <span data-ttu-id="2c8f5-123">Určuje akce má být provedena, když se zobrazí výzva k přepsání nebo ignorovat existující soubory, které jsou odkazované projektem.</span><span class="sxs-lookup"><span data-stu-id="2c8f5-123">Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="2c8f5-124">Hodnoty jsou *přepsat, ignorovat, none*.</span><span class="sxs-lookup"><span data-stu-id="2c8f5-124">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="2c8f5-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="2c8f5-125">ForceEnglishOutput</span></span> | <span data-ttu-id="2c8f5-126">*(3.5 +)*  Vynutí nuget.exe pro spuštění pomocí neutrální, základem je angličtina jazyková verze.</span><span class="sxs-lookup"><span data-stu-id="2c8f5-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="2c8f5-127">Help</span><span class="sxs-lookup"><span data-stu-id="2c8f5-127">Help</span></span> | <span data-ttu-id="2c8f5-128">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="2c8f5-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="2c8f5-129">Id</span><span class="sxs-lookup"><span data-stu-id="2c8f5-129">Id</span></span> | <span data-ttu-id="2c8f5-130">Určuje seznam ID k aktualizaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="2c8f5-130">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="2c8f5-131">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="2c8f5-131">MSBuildPath</span></span> | <span data-ttu-id="2c8f5-132">*(4.0 +)*  Určuje cestu k používání pomocí příkazu, přednost `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="2c8f5-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="2c8f5-133">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="2c8f5-133">MSBuildVersion</span></span> | <span data-ttu-id="2c8f5-134">*(3.2 +)*  Určuje verzi Msbuildu, který se má použít tento příkaz.</span><span class="sxs-lookup"><span data-stu-id="2c8f5-134">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="2c8f5-135">Podporované hodnoty jsou 4, 12, 14, 15.1, 15.3, 15.4, 15.5, verzi 15.6, 15.7, 15.8, 15.9.</span><span class="sxs-lookup"><span data-stu-id="2c8f5-135">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="2c8f5-136">Ve výchozím nastavení se vybere MSBuild na vaší cestě jinak je výchozí hodnotou nejvyšší nainstalovaná verze Msbuildu.</span><span class="sxs-lookup"><span data-stu-id="2c8f5-136">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="2c8f5-137">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="2c8f5-137">NonInteractive</span></span> | <span data-ttu-id="2c8f5-138">Potlačí vyzve k zadání uživatele o vstup ani potvrzení.</span><span class="sxs-lookup"><span data-stu-id="2c8f5-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="2c8f5-139">Platnost předběžné verze</span><span class="sxs-lookup"><span data-stu-id="2c8f5-139">PreRelease</span></span> | <span data-ttu-id="2c8f5-140">Umožňuje aktualizaci pro předběžné verze.</span><span class="sxs-lookup"><span data-stu-id="2c8f5-140">Allows updating to prerelease versions.</span></span> <span data-ttu-id="2c8f5-141">Tento příznak není potřeba při aktualizaci předběžné verze balíčků, které jsou již nainstalovány.</span><span class="sxs-lookup"><span data-stu-id="2c8f5-141">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="2c8f5-142">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="2c8f5-142">RepositoryPath</span></span> | <span data-ttu-id="2c8f5-143">Určuje místní složku, ve kterém jsou nainstalované balíčky.</span><span class="sxs-lookup"><span data-stu-id="2c8f5-143">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="2c8f5-144">Bezpečné</span><span class="sxs-lookup"><span data-stu-id="2c8f5-144">Safe</span></span> | <span data-ttu-id="2c8f5-145">Určuje, která aktualizuje pouze s nejvyšší verze k dispozici v rámci stejné hlavní a dílčí verze jako nainstalovaného balíčku se nainstaluje.</span><span class="sxs-lookup"><span data-stu-id="2c8f5-145">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="2c8f5-146">Vlastní</span><span class="sxs-lookup"><span data-stu-id="2c8f5-146">Self</span></span> | <span data-ttu-id="2c8f5-147">Aktualizuje na nejnovější verzi; nuget.exe Další argumenty jsou ignorovány.</span><span class="sxs-lookup"><span data-stu-id="2c8f5-147">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="2c8f5-148">Source</span><span class="sxs-lookup"><span data-stu-id="2c8f5-148">Source</span></span> | <span data-ttu-id="2c8f5-149">Určuje seznam zdrojů balíčků (jako adresy URL) použít pro aktualizace.</span><span class="sxs-lookup"><span data-stu-id="2c8f5-149">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="2c8f5-150">Pokud tento parametr vynechán, příkaz používá zdroje k dispozici v konfiguračních souborech naleznete v tématu [konfigurace běžných NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="2c8f5-150">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="2c8f5-151">Verbosity</span><span class="sxs-lookup"><span data-stu-id="2c8f5-151">Verbosity</span></span> | <span data-ttu-id="2c8f5-152">Určuje množství podrobností, na které se zobrazí ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="2c8f5-152">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="2c8f5-153">Version</span><span class="sxs-lookup"><span data-stu-id="2c8f5-153">Version</span></span> | <span data-ttu-id="2c8f5-154">Zadáním jednoho ID balíčku, určuje verzi balíčku aktualizace.</span><span class="sxs-lookup"><span data-stu-id="2c8f5-154">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="2c8f5-155">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="2c8f5-155">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="2c8f5-156">Příklady</span><span class="sxs-lookup"><span data-stu-id="2c8f5-156">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
