---
title: Aktualizace příkazu rozhraní příkazového řádku NuGet
description: Referenční informace pro příkaz update nuget.exe
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: ded9b571324d810c2f0e1a46ea76375a28940406
ms.sourcegitcommit: d5a35a097e6b461ae791d9f66b3a85d5219d7305
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/12/2019
ms.locfileid: "56145602"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="d34f3-103">Příkaz update (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="d34f3-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="d34f3-104">**Platí pro:** balíček spotřeby &bullet; **podporované verze:** všechny</span><span class="sxs-lookup"><span data-stu-id="d34f3-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="d34f3-105">Aktualizuje všechny balíčky v projektu (pomocí `packages.config`) jejich nejnovější dostupné verze.</span><span class="sxs-lookup"><span data-stu-id="d34f3-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="d34f3-106">Doporučuje se spouštět ["obnovit"](cli-ref-restore.md) dřív, než spustíte `update`.</span><span class="sxs-lookup"><span data-stu-id="d34f3-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="d34f3-107">(K aktualizaci jednotlivých balíčků, použijte [ `nuget install` ](cli-ref-install.md) bez zadání číslo verze, ve kterém případu NuGet nainstaluje nejnovější verzi.)</span><span class="sxs-lookup"><span data-stu-id="d34f3-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="d34f3-108">Poznámka: `update` nefunguje pro rozhraní příkazového řádku s mono (Mac OS x nebo Linux) nebo při použití formátu PackageReference.</span><span class="sxs-lookup"><span data-stu-id="d34f3-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="d34f3-109">`update` Příkaz aktualizuje také odkazy na sestavení v souboru projektu, pokud jsou již odkazuje existovat.</span><span class="sxs-lookup"><span data-stu-id="d34f3-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="d34f3-110">Pokud aktualizovaný balíček má přidání sestavení, je nový odkaz *není* přidán.</span><span class="sxs-lookup"><span data-stu-id="d34f3-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="d34f3-111">Nové závislosti balíčků také nemají přidání jejich odkazů na sestavení.</span><span class="sxs-lookup"><span data-stu-id="d34f3-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="d34f3-112">Chcete-li zahrnout tyto operace aktualizace, aktualizujte balíček v sadě Visual Studio pomocí uživatelského rozhraní Správce balíčků nebo konzole Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="d34f3-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="d34f3-113">Tento příkaz slouží také k aktualizaci nuget.exe samotný pomocí *-self* příznak.</span><span class="sxs-lookup"><span data-stu-id="d34f3-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="d34f3-114">Použití</span><span class="sxs-lookup"><span data-stu-id="d34f3-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="d34f3-115">kde `<configPath>` identifikuje buď `packages.config` nebo soubor řešení, která obsahuje seznam závislostí projektu.</span><span class="sxs-lookup"><span data-stu-id="d34f3-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="d34f3-116">Možnosti</span><span class="sxs-lookup"><span data-stu-id="d34f3-116">Options</span></span>

| <span data-ttu-id="d34f3-117">Možnost</span><span class="sxs-lookup"><span data-stu-id="d34f3-117">Option</span></span> | <span data-ttu-id="d34f3-118">Popis</span><span class="sxs-lookup"><span data-stu-id="d34f3-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d34f3-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="d34f3-119">ConfigFile</span></span> | <span data-ttu-id="d34f3-120">Konfigurační soubor NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="d34f3-120">The NuGet configuration file to apply.</span></span> <span data-ttu-id="d34f3-121">Pokud není zadán, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.</span><span class="sxs-lookup"><span data-stu-id="d34f3-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="d34f3-122">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="d34f3-122">FileConflictAction</span></span> | <span data-ttu-id="d34f3-123">Určuje akce má být provedena, když se zobrazí výzva k přepsání nebo ignorovat existující soubory, které jsou odkazované projektem.</span><span class="sxs-lookup"><span data-stu-id="d34f3-123">Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="d34f3-124">Hodnoty jsou *přepsat, ignorovat, none*.</span><span class="sxs-lookup"><span data-stu-id="d34f3-124">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="d34f3-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="d34f3-125">ForceEnglishOutput</span></span> | <span data-ttu-id="d34f3-126">*(3.5 +)*  Vynutí nuget.exe pro spuštění pomocí neutrální, základem je angličtina jazyková verze.</span><span class="sxs-lookup"><span data-stu-id="d34f3-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="d34f3-127">Nápověda</span><span class="sxs-lookup"><span data-stu-id="d34f3-127">Help</span></span> | <span data-ttu-id="d34f3-128">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="d34f3-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="d34f3-129">ID</span><span class="sxs-lookup"><span data-stu-id="d34f3-129">Id</span></span> | <span data-ttu-id="d34f3-130">Určuje seznam ID k aktualizaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="d34f3-130">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="d34f3-131">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="d34f3-131">MSBuildPath</span></span> | <span data-ttu-id="d34f3-132">*(4.0 +)*  Určuje cestu k používání pomocí příkazu, přednost `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="d34f3-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="d34f3-133">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="d34f3-133">MSBuildVersion</span></span> | <span data-ttu-id="d34f3-134">*(3.2 +)*  Určuje verzi Msbuildu, který se má použít tento příkaz.</span><span class="sxs-lookup"><span data-stu-id="d34f3-134">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="d34f3-135">Podporované hodnoty jsou 4, 12, 14, 15.1, 15.3, 15.4, 15.5, verzi 15.6, 15.7, 15.8, 15.9.</span><span class="sxs-lookup"><span data-stu-id="d34f3-135">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="d34f3-136">Ve výchozím nastavení se vybere MSBuild na vaší cestě jinak je výchozí hodnotou nejvyšší nainstalovaná verze Msbuildu.</span><span class="sxs-lookup"><span data-stu-id="d34f3-136">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="d34f3-137">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="d34f3-137">NonInteractive</span></span> | <span data-ttu-id="d34f3-138">Potlačí vyzve k zadání uživatele o vstup ani potvrzení.</span><span class="sxs-lookup"><span data-stu-id="d34f3-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="d34f3-139">Platnost předběžné verze</span><span class="sxs-lookup"><span data-stu-id="d34f3-139">PreRelease</span></span> | <span data-ttu-id="d34f3-140">Umožňuje aktualizaci pro předběžné verze.</span><span class="sxs-lookup"><span data-stu-id="d34f3-140">Allows updating to prerelease versions.</span></span> <span data-ttu-id="d34f3-141">Tento příznak není potřeba při aktualizaci předběžné verze balíčků, které jsou již nainstalovány.</span><span class="sxs-lookup"><span data-stu-id="d34f3-141">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="d34f3-142">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="d34f3-142">RepositoryPath</span></span> | <span data-ttu-id="d34f3-143">Určuje místní složku, ve kterém jsou nainstalované balíčky.</span><span class="sxs-lookup"><span data-stu-id="d34f3-143">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="d34f3-144">Bezpečné</span><span class="sxs-lookup"><span data-stu-id="d34f3-144">Safe</span></span> | <span data-ttu-id="d34f3-145">Určuje, která aktualizuje pouze s nejvyšší verze k dispozici v rámci stejné hlavní a dílčí verze jako nainstalovaného balíčku se nainstaluje.</span><span class="sxs-lookup"><span data-stu-id="d34f3-145">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="d34f3-146">Vlastní</span><span class="sxs-lookup"><span data-stu-id="d34f3-146">Self</span></span> | <span data-ttu-id="d34f3-147">Aktualizuje na nejnovější verzi; nuget.exe Další argumenty jsou ignorovány.</span><span class="sxs-lookup"><span data-stu-id="d34f3-147">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="d34f3-148">Zdroj</span><span class="sxs-lookup"><span data-stu-id="d34f3-148">Source</span></span> | <span data-ttu-id="d34f3-149">Určuje seznam zdrojů balíčků (jako adresy URL) použít pro aktualizace.</span><span class="sxs-lookup"><span data-stu-id="d34f3-149">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="d34f3-150">Pokud tento parametr vynechán, příkaz používá zdroje k dispozici v konfiguračních souborech naleznete v tématu [konfigurace NuGet chování](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="d34f3-150">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="d34f3-151">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="d34f3-151">Verbosity</span></span> | <span data-ttu-id="d34f3-152">Určuje množství podrobností, na které se zobrazí ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="d34f3-152">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="d34f3-153">Version</span><span class="sxs-lookup"><span data-stu-id="d34f3-153">Version</span></span> | <span data-ttu-id="d34f3-154">Zadáním jednoho ID balíčku, určuje verzi balíčku aktualizace.</span><span class="sxs-lookup"><span data-stu-id="d34f3-154">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="d34f3-155">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d34f3-155">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d34f3-156">Příklady</span><span class="sxs-lookup"><span data-stu-id="d34f3-156">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
