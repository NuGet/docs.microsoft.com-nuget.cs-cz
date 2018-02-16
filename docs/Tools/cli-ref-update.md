---
title: "Rozhraní příkazového řádku NuGet aktualizovat příkaz | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenční dokumentace pro příkaz nuget.exe aktualizace"
keywords: "referenční dokumentace aktualizace nuget, příkaz balíčku aktualizace"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6a788244d23354b980e8fa86fa170740c18f17b2
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/14/2018
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="1700b-104">příkaz aktualizace (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="1700b-104">update command (NuGet CLI)</span></span>

<span data-ttu-id="1700b-105">**Platí pro:** balíček spotřeba &bullet; **podporované verze:** všechny</span><span class="sxs-lookup"><span data-stu-id="1700b-105">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="1700b-106">Aktualizuje všechny balíčky v projektu (pomocí `packages.config`) na jejich nejnovější verze, k dispozici.</span><span class="sxs-lookup"><span data-stu-id="1700b-106">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="1700b-107">Doporučuje se spouštět ['Obnovení'](cli-ref-restore.md) dřív, než spustíte `update`.</span><span class="sxs-lookup"><span data-stu-id="1700b-107">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="1700b-108">(Chcete-li aktualizovat jednotlivých balíčků, použijte [ `nuget install` ](cli-ref-install.md) bez zadání číslem verze, ve kterém případu NuGet nainstaluje nejnovější verzi.)</span><span class="sxs-lookup"><span data-stu-id="1700b-108">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="1700b-109">Poznámka: `update` pomocí rozhraní příkazového řádku při použití formátu PackageReference spuštěna pod Mono (Mac OSX nebo Linux) nebo nefunguje.</span><span class="sxs-lookup"><span data-stu-id="1700b-109">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="1700b-110">`update` Příkaz aktualizuje také odkazy na sestavení v souboru projektu, zadaný těch, které odkazuje již existuje.</span><span class="sxs-lookup"><span data-stu-id="1700b-110">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="1700b-111">Pokud aktualizovaný balíček přidané sestavení, nový odkaz je *není* přidat.</span><span class="sxs-lookup"><span data-stu-id="1700b-111">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="1700b-112">Nové závislosti balíčků také nemají jejich odkazy na sestavení, který je přidán.</span><span class="sxs-lookup"><span data-stu-id="1700b-112">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="1700b-113">Chcete-li zahrnout tyto operace aktualizace, aktualizujte balíček v sadě Visual Studio pomocí uživatelského rozhraní Správce balíčků nebo konzole Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="1700b-113">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="1700b-114">Tento příkaz lze použít také k aktualizaci nuget.exe samotné pomocí *-self* příznak.</span><span class="sxs-lookup"><span data-stu-id="1700b-114">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="1700b-115">Použití</span><span class="sxs-lookup"><span data-stu-id="1700b-115">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="1700b-116">kde `<configPath>` identifikuje buď `packages.config` nebo soubor řešení, která uvádí závislosti projektu.</span><span class="sxs-lookup"><span data-stu-id="1700b-116">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="1700b-117">Možnosti</span><span class="sxs-lookup"><span data-stu-id="1700b-117">Options</span></span>

| <span data-ttu-id="1700b-118">Možnost</span><span class="sxs-lookup"><span data-stu-id="1700b-118">Option</span></span> | <span data-ttu-id="1700b-119">Popis</span><span class="sxs-lookup"><span data-stu-id="1700b-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1700b-120">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="1700b-120">ConfigFile</span></span> | <span data-ttu-id="1700b-121">Konfigurační soubor NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="1700b-121">The NuGet configuration file to apply.</span></span> <span data-ttu-id="1700b-122">Pokud není zadaný, *%AppData%\NuGet\NuGet.Config* se používá.</span><span class="sxs-lookup"><span data-stu-id="1700b-122">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="1700b-123">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="1700b-123">FileConflictAction</span></span> | <span data-ttu-id="1700b-124">Určuje akci, kterou provést, pokud se zobrazí výzva k přepsání nebo ignorovat existující soubory, které se odkazuje na projekt.</span><span class="sxs-lookup"><span data-stu-id="1700b-124">Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="1700b-125">Hodnoty jsou *přepsat, ignorovat, none*.</span><span class="sxs-lookup"><span data-stu-id="1700b-125">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="1700b-126">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="1700b-126">ForceEnglishOutput</span></span> | <span data-ttu-id="1700b-127">*(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze.</span><span class="sxs-lookup"><span data-stu-id="1700b-127">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="1700b-128">Nápověda</span><span class="sxs-lookup"><span data-stu-id="1700b-128">Help</span></span> | <span data-ttu-id="1700b-129">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="1700b-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="1700b-130">ID</span><span class="sxs-lookup"><span data-stu-id="1700b-130">Id</span></span> | <span data-ttu-id="1700b-131">Určuje seznam balíčku ID aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="1700b-131">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="1700b-132">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="1700b-132">MSBuildPath</span></span> | <span data-ttu-id="1700b-133">*(4.0 +)*  Určuje cestu MSBuild používat pomocí příkazu, přednost před `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="1700b-133">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="1700b-134">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="1700b-134">MSBuildVersion</span></span> | <span data-ttu-id="1700b-135">*(3.2 +)*  Určuje verzi nástroje MSBuild k použití se tento příkaz.</span><span class="sxs-lookup"><span data-stu-id="1700b-135">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="1700b-136">Podporované hodnoty jsou 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="1700b-136">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="1700b-137">Ve výchozím nastavení je zachyceny MSBuild ve své cestě jinak bude výchozí nejvyšší nainstalovanou verzi nástroje MSBuild.</span><span class="sxs-lookup"><span data-stu-id="1700b-137">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="1700b-138">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="1700b-138">NonInteractive</span></span> | <span data-ttu-id="1700b-139">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="1700b-139">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="1700b-140">Předběžné verze</span><span class="sxs-lookup"><span data-stu-id="1700b-140">PreRelease</span></span> | <span data-ttu-id="1700b-141">Umožňuje aktualizaci na předprodejní verze.</span><span class="sxs-lookup"><span data-stu-id="1700b-141">Allows updating to prerelease versions.</span></span> <span data-ttu-id="1700b-142">Tento příznak se nevyžaduje při aktualizaci předběžné verze balíčků, které jsou již nainstalovány.</span><span class="sxs-lookup"><span data-stu-id="1700b-142">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="1700b-143">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="1700b-143">RepositoryPath</span></span> | <span data-ttu-id="1700b-144">Určuje místní složku, ve kterém jsou nainstalované balíčky.</span><span class="sxs-lookup"><span data-stu-id="1700b-144">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="1700b-145">Bezpečné</span><span class="sxs-lookup"><span data-stu-id="1700b-145">Safe</span></span> | <span data-ttu-id="1700b-146">Určuje, který aktualizuje pouze s nejvyšší verzi k dispozici v rámci stejnou hlavní a vedlejší verzi jako nainstaluje s nainstalovaným balíčkem.</span><span class="sxs-lookup"><span data-stu-id="1700b-146">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="1700b-147">Vlastní</span><span class="sxs-lookup"><span data-stu-id="1700b-147">Self</span></span> | <span data-ttu-id="1700b-148">Nuget.exe aktualizace na nejnovější verzi; všechny další argumenty se ignorují.</span><span class="sxs-lookup"><span data-stu-id="1700b-148">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="1700b-149">Zdroj</span><span class="sxs-lookup"><span data-stu-id="1700b-149">Source</span></span> | <span data-ttu-id="1700b-150">Určuje seznam zdrojů balíčku (jako adresy URL) pro aktualizace.</span><span class="sxs-lookup"><span data-stu-id="1700b-150">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="1700b-151">Pokud tento parametr vynechán, příkaz používá zdrojů, součástí konfigurační soubory, najdete v části [konfigurace NuGet chování](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="1700b-151">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="1700b-152">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="1700b-152">Verbosity</span></span> | <span data-ttu-id="1700b-153">Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="1700b-153">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="1700b-154">Version</span><span class="sxs-lookup"><span data-stu-id="1700b-154">Version</span></span> | <span data-ttu-id="1700b-155">Při použití s jedno ID balíčku, určuje verzi balíčku aktualizace.</span><span class="sxs-lookup"><span data-stu-id="1700b-155">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="1700b-156">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="1700b-156">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="1700b-157">Příklady</span><span class="sxs-lookup"><span data-stu-id="1700b-157">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
