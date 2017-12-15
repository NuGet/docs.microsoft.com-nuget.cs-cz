---
title: "Rozhraní příkazového řádku NuGet aktualizovat příkaz | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 61fde945-6983-46a5-8636-da0fada4e641
description: "Referenční dokumentace pro příkaz nuget.exe aktualizace"
keywords: "referenční dokumentace aktualizace nuget, příkaz balíčku aktualizace"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 654144e93a99a4a4f8d79c0db5660cfb7c6c308e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="6e5ed-104">příkaz aktualizace (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="6e5ed-104">update command (NuGet CLI)</span></span>

<span data-ttu-id="6e5ed-105">**Platí pro:** balíček spotřeba &bullet; **podporované verze:** všechny</span><span class="sxs-lookup"><span data-stu-id="6e5ed-105">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="6e5ed-106">Aktualizuje všechny balíčky v projektu (pomocí `packages.config`) na jejich nejnovější verze, k dispozici.</span><span class="sxs-lookup"><span data-stu-id="6e5ed-106">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="6e5ed-107">Doporučuje se spouštět ['Obnovení'](#restore) dřív, než spustíte `update`.</span><span class="sxs-lookup"><span data-stu-id="6e5ed-107">It is recommended to run ['restore'](#restore) before running the `update`.</span></span> <span data-ttu-id="6e5ed-108">(Chcete-li aktualizovat jednotlivých balíčků, použijte [ `nuget install` ](cli-ref-install.md) bez zadání číslem verze, ve kterém případu NuGet nainstaluje nejnovější verzi.)</span><span class="sxs-lookup"><span data-stu-id="6e5ed-108">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="6e5ed-109">Poznámka: `update` nefunguje s rozhraní příkazového řádku spuštěna pod Mono (Mac OSX nebo Linux).</span><span class="sxs-lookup"><span data-stu-id="6e5ed-109">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux).</span></span> <span data-ttu-id="6e5ed-110">Příkaz také nefunguje s projektů pomocí `project.json` nebo PackageReference správu formáty.</span><span class="sxs-lookup"><span data-stu-id="6e5ed-110">The command also does not work with projects using `project.json` or PackageReference management formats.</span></span>

<span data-ttu-id="6e5ed-111">`update` Příkaz aktualizuje také odkazy na sestavení v souboru projektu, zadaný těch, které odkazuje již existuje.</span><span class="sxs-lookup"><span data-stu-id="6e5ed-111">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="6e5ed-112">Pokud aktualizovaný balíček přidané sestavení, nový odkaz je *není* přidat.</span><span class="sxs-lookup"><span data-stu-id="6e5ed-112">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="6e5ed-113">Nové závislosti balíčků také nemají jejich odkazy na sestavení, který je přidán.</span><span class="sxs-lookup"><span data-stu-id="6e5ed-113">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="6e5ed-114">Chcete-li zahrnout tyto operace aktualizace, aktualizujte balíček v sadě Visual Studio pomocí uživatelského rozhraní Správce balíčků nebo konzole Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="6e5ed-114">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="6e5ed-115">Tento příkaz lze použít také k aktualizaci nuget.exe samotné pomocí *-self* příznak.</span><span class="sxs-lookup"><span data-stu-id="6e5ed-115">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="6e5ed-116">Použití</span><span class="sxs-lookup"><span data-stu-id="6e5ed-116">Usage</span></span>

```
nuget update <configPath> [options]
```

<span data-ttu-id="6e5ed-117">kde `<configPath>` identifikuje buď `packages.config` nebo soubor řešení, která uvádí závislosti projektu.</span><span class="sxs-lookup"><span data-stu-id="6e5ed-117">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="6e5ed-118">Možnosti</span><span class="sxs-lookup"><span data-stu-id="6e5ed-118">Options</span></span>

| <span data-ttu-id="6e5ed-119">Možnost</span><span class="sxs-lookup"><span data-stu-id="6e5ed-119">Option</span></span> | <span data-ttu-id="6e5ed-120">Popis</span><span class="sxs-lookup"><span data-stu-id="6e5ed-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6e5ed-121">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="6e5ed-121">ConfigFile</span></span> | <span data-ttu-id="6e5ed-122">*(2.5 +)*  NuGet konfiguračním souboru použít.</span><span class="sxs-lookup"><span data-stu-id="6e5ed-122">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="6e5ed-123">Pokud není zadaný, *%AppData%\NuGet\NuGet.Config* se používá.</span><span class="sxs-lookup"><span data-stu-id="6e5ed-123">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="6e5ed-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="6e5ed-124">FileConflictAction</span></span> | <span data-ttu-id="6e5ed-125">*(2.5 +)*  Určuje akci, kterou provést, pokud se zobrazí výzva k přepsání nebo ignorovat existující soubory, které se odkazuje na projekt.</span><span class="sxs-lookup"><span data-stu-id="6e5ed-125">*(2.5+)* Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="6e5ed-126">Hodnoty jsou *přepsat, ignorovat, none*.</span><span class="sxs-lookup"><span data-stu-id="6e5ed-126">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="6e5ed-127">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="6e5ed-127">ForceEnglishOutput</span></span> | <span data-ttu-id="6e5ed-128">*(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze.</span><span class="sxs-lookup"><span data-stu-id="6e5ed-128">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="6e5ed-129">Nápověda</span><span class="sxs-lookup"><span data-stu-id="6e5ed-129">Help</span></span> | <span data-ttu-id="6e5ed-130">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="6e5ed-130">Displays help information for the command.</span></span> |
| <span data-ttu-id="6e5ed-131">ID</span><span class="sxs-lookup"><span data-stu-id="6e5ed-131">Id</span></span> | <span data-ttu-id="6e5ed-132">Určuje seznam balíčku ID aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="6e5ed-132">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="6e5ed-133">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="6e5ed-133">MSBuildPath</span></span> | <span data-ttu-id="6e5ed-134">*(4.0 +)*  Určuje cestu MSBuild používat pomocí příkazu, přednost před `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="6e5ed-134">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="6e5ed-135">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="6e5ed-135">MSBuildVersion</span></span> | <span data-ttu-id="6e5ed-136">*(3.2 +)*  Určuje verzi nástroje MSBuild k použití se tento příkaz.</span><span class="sxs-lookup"><span data-stu-id="6e5ed-136">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="6e5ed-137">Podporované hodnoty jsou 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="6e5ed-137">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="6e5ed-138">Ve výchozím nastavení je zachyceny MSBuild ve své cestě jinak bude výchozí nejvyšší nainstalovanou verzi nástroje MSBuild.</span><span class="sxs-lookup"><span data-stu-id="6e5ed-138">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="6e5ed-139">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="6e5ed-139">NonInteractive</span></span> | <span data-ttu-id="6e5ed-140">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="6e5ed-140">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="6e5ed-141">Předběžné verze</span><span class="sxs-lookup"><span data-stu-id="6e5ed-141">PreRelease</span></span> | <span data-ttu-id="6e5ed-142">Umožňuje aktualizaci na předprodejní verze.</span><span class="sxs-lookup"><span data-stu-id="6e5ed-142">Allows updating to prerelease versions.</span></span> <span data-ttu-id="6e5ed-143">Tento příznak se nevyžaduje při aktualizaci předběžné verze balíčků, které jsou již nainstalovány.</span><span class="sxs-lookup"><span data-stu-id="6e5ed-143">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="6e5ed-144">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="6e5ed-144">RepositoryPath</span></span> | <span data-ttu-id="6e5ed-145">Určuje místní složku, ve kterém jsou nainstalované balíčky.</span><span class="sxs-lookup"><span data-stu-id="6e5ed-145">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="6e5ed-146">Bezpečné</span><span class="sxs-lookup"><span data-stu-id="6e5ed-146">Safe</span></span> | <span data-ttu-id="6e5ed-147">Určuje, který aktualizuje pouze s nejvyšší verzi k dispozici v rámci stejnou hlavní a vedlejší verzi jako nainstaluje s nainstalovaným balíčkem.</span><span class="sxs-lookup"><span data-stu-id="6e5ed-147">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="6e5ed-148">Vlastní</span><span class="sxs-lookup"><span data-stu-id="6e5ed-148">Self</span></span> | <span data-ttu-id="6e5ed-149">*(1.4 +)*  Aktualizuje na nejnovější verzi; nuget.exe jsou ignorovány všechny další argumenty.</span><span class="sxs-lookup"><span data-stu-id="6e5ed-149">*(1.4+)* Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="6e5ed-150">Zdroj</span><span class="sxs-lookup"><span data-stu-id="6e5ed-150">Source</span></span> | <span data-ttu-id="6e5ed-151">Určuje seznam zdrojů balíčku (jako adresy URL) pro aktualizace.</span><span class="sxs-lookup"><span data-stu-id="6e5ed-151">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="6e5ed-152">Pokud tento parametr vynechán, příkaz používá zdrojů, součástí konfigurační soubory, najdete v části [konfigurace NuGet chování](../Consume-Packages/Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="6e5ed-152">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md).</span></span> |
| <span data-ttu-id="6e5ed-153">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="6e5ed-153">Verbosity</span></span> | <span data-ttu-id="6e5ed-154">Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="6e5ed-154">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |
| <span data-ttu-id="6e5ed-155">Version</span><span class="sxs-lookup"><span data-stu-id="6e5ed-155">Version</span></span> | <span data-ttu-id="6e5ed-156">Při použití s jedno ID balíčku, určuje verzi balíčku aktualizace.</span><span class="sxs-lookup"><span data-stu-id="6e5ed-156">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="6e5ed-157">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="6e5ed-157">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="6e5ed-158">Příklady</span><span class="sxs-lookup"><span data-stu-id="6e5ed-158">Examples</span></span>

```
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
