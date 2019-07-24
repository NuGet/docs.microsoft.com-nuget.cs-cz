---
title: Příkaz NuGet CLI Update
description: Referenční informace k příkazu NuGet. exe Update
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: b5da09c3dd6ffa0ce1b7b44731ed67ddd0336c58
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328255"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="e3c2d-103">Příkaz update (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="e3c2d-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="e3c2d-104">**Platí pro:** &bullet; **podporované verze balíčku:** vše</span><span class="sxs-lookup"><span data-stu-id="e3c2d-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="e3c2d-105">Aktualizuje všechny balíčky v projektu (pomocí `packages.config`) na nejnovější dostupné verze.</span><span class="sxs-lookup"><span data-stu-id="e3c2d-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="e3c2d-106">Před spuštěním `update` [nástroje](cli-ref-restore.md) se doporučuje spustit příkaz Restore.</span><span class="sxs-lookup"><span data-stu-id="e3c2d-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="e3c2d-107">(Pokud chcete aktualizovat jednotlivý balíček, [`nuget install`](cli-ref-install.md) použijte bez zadání čísla verze. v takovém případě NuGet nainstaluje nejnovější verzi.)</span><span class="sxs-lookup"><span data-stu-id="e3c2d-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="e3c2d-108">Poznámka: `update` nefunguje s rozhraním příkazového řádku spuštěným v mono (Mac OSX nebo Linux) nebo při použití formátu PackageReference.</span><span class="sxs-lookup"><span data-stu-id="e3c2d-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="e3c2d-109">`update` Příkaz také aktualizuje odkazy na sestavení v souboru projektu za předpokladu, že tyto odkazy již existují.</span><span class="sxs-lookup"><span data-stu-id="e3c2d-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="e3c2d-110">Pokud aktualizovaný balíček obsahuje přidané sestavení, nový odkaz se *nepřidá.*</span><span class="sxs-lookup"><span data-stu-id="e3c2d-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="e3c2d-111">Nové závislosti balíčků také nemají přidané odkazy na sestavení.</span><span class="sxs-lookup"><span data-stu-id="e3c2d-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="e3c2d-112">Chcete-li zahrnout tyto operace jako součást aktualizace, aktualizujte balíček v aplikaci Visual Studio pomocí uživatelského rozhraní Správce balíčků nebo konzoly Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="e3c2d-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="e3c2d-113">Tento příkaz lze také použít k aktualizaci souboru NuGet. exe pomocí příznaku *-vlastní* .</span><span class="sxs-lookup"><span data-stu-id="e3c2d-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="e3c2d-114">Použití</span><span class="sxs-lookup"><span data-stu-id="e3c2d-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="e3c2d-115">kde `<configPath>` identifikuje`packages.config` buď soubor řešení nebo, který obsahuje seznam závislostí projektu.</span><span class="sxs-lookup"><span data-stu-id="e3c2d-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="e3c2d-116">Možnosti</span><span class="sxs-lookup"><span data-stu-id="e3c2d-116">Options</span></span>

| <span data-ttu-id="e3c2d-117">Možnost</span><span class="sxs-lookup"><span data-stu-id="e3c2d-117">Option</span></span> | <span data-ttu-id="e3c2d-118">Popis</span><span class="sxs-lookup"><span data-stu-id="e3c2d-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e3c2d-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="e3c2d-119">ConfigFile</span></span> | <span data-ttu-id="e3c2d-120">Konfigurační soubor NuGet, který se má použít</span><span class="sxs-lookup"><span data-stu-id="e3c2d-120">The NuGet configuration file to apply.</span></span> <span data-ttu-id="e3c2d-121">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows `~/.nuget/NuGet/NuGet.Config` ) nebo (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="e3c2d-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="e3c2d-122">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="e3c2d-122">FileConflictAction</span></span> | <span data-ttu-id="e3c2d-123">Určuje akci, která se má provést, když se zobrazí výzva k přepsání nebo ignorování existujících souborů, na které se odkazuje v projektu.</span><span class="sxs-lookup"><span data-stu-id="e3c2d-123">Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="e3c2d-124">Hodnoty jsou *přepisované, ignore, None*.</span><span class="sxs-lookup"><span data-stu-id="e3c2d-124">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="e3c2d-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="e3c2d-125">ForceEnglishOutput</span></span> | <span data-ttu-id="e3c2d-126">*(3.5 +)* Vynutí, aby soubor NuGet. exe běžel pomocí neutrální jazykové verze určené pro angličtinu.</span><span class="sxs-lookup"><span data-stu-id="e3c2d-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="e3c2d-127">Help</span><span class="sxs-lookup"><span data-stu-id="e3c2d-127">Help</span></span> | <span data-ttu-id="e3c2d-128">Zobrazí informace o nápovědě k příkazu.</span><span class="sxs-lookup"><span data-stu-id="e3c2d-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="e3c2d-129">Id</span><span class="sxs-lookup"><span data-stu-id="e3c2d-129">Id</span></span> | <span data-ttu-id="e3c2d-130">Určuje seznam ID balíčků, které se mají aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="e3c2d-130">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="e3c2d-131">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="e3c2d-131">MSBuildPath</span></span> | <span data-ttu-id="e3c2d-132">*(4.0 +)* Určuje cestu nástroje MSBuild, který má být použit s příkazem, přičemž přednost `-MSBuildVersion`využije.</span><span class="sxs-lookup"><span data-stu-id="e3c2d-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="e3c2d-133">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="e3c2d-133">MSBuildVersion</span></span> | <span data-ttu-id="e3c2d-134">*(3.2 +)* Určuje verzi nástroje MSBuild, která má být použita s tímto příkazem.</span><span class="sxs-lookup"><span data-stu-id="e3c2d-134">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="e3c2d-135">Podporované hodnoty jsou 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="e3c2d-135">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="e3c2d-136">Ve výchozím nastavení je nástroj MSBuild v cestě vybrán, jinak má výchozí nejvyšší nainstalovanou verzi nástroje MSBuild.</span><span class="sxs-lookup"><span data-stu-id="e3c2d-136">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="e3c2d-137">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="e3c2d-137">NonInteractive</span></span> | <span data-ttu-id="e3c2d-138">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="e3c2d-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="e3c2d-139">Předběžné verze</span><span class="sxs-lookup"><span data-stu-id="e3c2d-139">PreRelease</span></span> | <span data-ttu-id="e3c2d-140">Umožňuje aktualizaci předprodejních verzí.</span><span class="sxs-lookup"><span data-stu-id="e3c2d-140">Allows updating to prerelease versions.</span></span> <span data-ttu-id="e3c2d-141">Tento příznak není požadován při aktualizaci předprodejních balíčků, které jsou již nainstalovány.</span><span class="sxs-lookup"><span data-stu-id="e3c2d-141">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="e3c2d-142">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="e3c2d-142">RepositoryPath</span></span> | <span data-ttu-id="e3c2d-143">Určuje místní složku, ve které jsou balíčky nainstalované.</span><span class="sxs-lookup"><span data-stu-id="e3c2d-143">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="e3c2d-144">Odvod</span><span class="sxs-lookup"><span data-stu-id="e3c2d-144">Safe</span></span> | <span data-ttu-id="e3c2d-145">Určuje, že se budou instalovat jenom aktualizace s nejvyšší verzí dostupnou v rámci stejné hlavní a dílčí verze, jako je nainstalovaný balíček.</span><span class="sxs-lookup"><span data-stu-id="e3c2d-145">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="e3c2d-146">Samorozbalující</span><span class="sxs-lookup"><span data-stu-id="e3c2d-146">Self</span></span> | <span data-ttu-id="e3c2d-147">Aktualizuje NuGet. exe na nejnovější verzi. všechny ostatní argumenty jsou ignorovány.</span><span class="sxs-lookup"><span data-stu-id="e3c2d-147">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="e3c2d-148">Source</span><span class="sxs-lookup"><span data-stu-id="e3c2d-148">Source</span></span> | <span data-ttu-id="e3c2d-149">Určuje seznam zdrojů balíčků (jako adresy URL), které se mají použít pro aktualizace.</span><span class="sxs-lookup"><span data-stu-id="e3c2d-149">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="e3c2d-150">Pokud je tato hodnota vynechána, příkaz použije zdroje zadané v konfiguračních souborech, viz [běžné konfigurace NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="e3c2d-150">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="e3c2d-151">Verbosity</span><span class="sxs-lookup"><span data-stu-id="e3c2d-151">Verbosity</span></span> | <span data-ttu-id="e3c2d-152">Určuje množství podrobností zobrazených ve výstupu: *normální*, tiché a *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="e3c2d-152">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="e3c2d-153">Version</span><span class="sxs-lookup"><span data-stu-id="e3c2d-153">Version</span></span> | <span data-ttu-id="e3c2d-154">Při použití s jedním ID balíčku určuje verzi balíčku, který se má aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="e3c2d-154">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="e3c2d-155">Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="e3c2d-155">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="e3c2d-156">Příklady</span><span class="sxs-lookup"><span data-stu-id="e3c2d-156">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
