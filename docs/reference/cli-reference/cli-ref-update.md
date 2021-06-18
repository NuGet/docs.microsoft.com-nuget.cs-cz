---
title: Příkaz NuGet CLI Update
description: Referenční informace k příkazu nuget.exe Update
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 5f244e4cf15ca7afa0e6318a8c20d464ff75bd8e
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323645"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="272b5-103">Update – příkaz (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="272b5-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="272b5-104">**Platí pro:** &bullet; **podporované verze balíčku:** vše</span><span class="sxs-lookup"><span data-stu-id="272b5-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="272b5-105">Aktualizuje všechny balíčky v projektu (pomocí `packages.config` ) na nejnovější dostupné verze.</span><span class="sxs-lookup"><span data-stu-id="272b5-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="272b5-106">Před spuštěním nástroje se doporučuje spustit příkaz [Restore](cli-ref-restore.md) `update` .</span><span class="sxs-lookup"><span data-stu-id="272b5-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="272b5-107">(Pokud chcete aktualizovat jednotlivý balíček, použijte [`nuget install`](cli-ref-install.md) bez zadání čísla verze. v takovém případě NuGet nainstaluje nejnovější verzi.)</span><span class="sxs-lookup"><span data-stu-id="272b5-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="272b5-108">Poznámka: `update` nefunguje s rozhraním příkazového řádku spuštěným v mono (Mac OSX nebo Linux) nebo při použití formátu PackageReference.</span><span class="sxs-lookup"><span data-stu-id="272b5-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="272b5-109">`update`Příkaz také aktualizuje odkazy na sestavení v souboru projektu za předpokladu, že tyto odkazy již existují.</span><span class="sxs-lookup"><span data-stu-id="272b5-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="272b5-110">Pokud aktualizovaný balíček obsahuje přidané sestavení, nový *odkaz se nepřidá.*</span><span class="sxs-lookup"><span data-stu-id="272b5-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="272b5-111">Nové závislosti balíčků také nemají přidané odkazy na sestavení.</span><span class="sxs-lookup"><span data-stu-id="272b5-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="272b5-112">Chcete-li zahrnout tyto operace jako součást aktualizace, aktualizujte balíček v aplikaci Visual Studio pomocí uživatelského rozhraní Správce balíčků nebo konzoly Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="272b5-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="272b5-113">Tento příkaz lze také použít k aktualizaci nuget.exe sebe sama pomocí příznaku *-vlastní* .</span><span class="sxs-lookup"><span data-stu-id="272b5-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="272b5-114">Využití</span><span class="sxs-lookup"><span data-stu-id="272b5-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="272b5-115">kde `<configPath>` identifikuje buď `packages.config` soubor řešení nebo, který obsahuje seznam závislostí projektu.</span><span class="sxs-lookup"><span data-stu-id="272b5-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="272b5-116">Možnosti</span><span class="sxs-lookup"><span data-stu-id="272b5-116">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="272b5-117">Konfigurační soubor NuGet, který se má použít</span><span class="sxs-lookup"><span data-stu-id="272b5-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="272b5-118">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows) nebo `~/.nuget/NuGet/NuGet.Config` nebo `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="272b5-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>
  
- **`-DependencyVersion [Lowest, HighestPatch, HighestMinor, Highest, Ignore]`**

  <span data-ttu-id="272b5-119">Určuje verzi balíčků závislostí, které se mají použít, což může být jedna z následujících:</span><span class="sxs-lookup"><span data-stu-id="272b5-119">Specifies the version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="272b5-120">*Nejnižší* (výchozí): nejnižší verze</span><span class="sxs-lookup"><span data-stu-id="272b5-120">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="272b5-121">*HighestPatch*: verze, která má nejnižší hlavní, nejnižší podverzi, nejvyšší opravu</span><span class="sxs-lookup"><span data-stu-id="272b5-121">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="272b5-122">*HighestMinor*: verze s nejnižší hlavní, nejvyšší podverze a nejvyšší opravou</span><span class="sxs-lookup"><span data-stu-id="272b5-122">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="272b5-123">*Nejvyšší*: nejvyšší verze</span><span class="sxs-lookup"><span data-stu-id="272b5-123">*Highest*: the highest version</span></span></li><li><span data-ttu-id="272b5-124">*Ignorovat*: nebudou použity žádné balíčky závislostí.</span><span class="sxs-lookup"><span data-stu-id="272b5-124">*Ignore*: No dependency packages will be used</span></span></li></ul>

- **`-FileConflictAction [PromptUser, Overwrite, Ignore]`**

  <span data-ttu-id="272b5-125">Určuje výchozí akci, pokud soubor z balíčku již v cílovém projektu existuje.</span><span class="sxs-lookup"><span data-stu-id="272b5-125">Specifies the default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="272b5-126">Nastavte na `Overwrite` vždycky přepsat soubory.</span><span class="sxs-lookup"><span data-stu-id="272b5-126">Set to `Overwrite` to always overwrite files.</span></span> <span data-ttu-id="272b5-127">Nastavte na `Ignore` Přeskočit soubory.</span><span class="sxs-lookup"><span data-stu-id="272b5-127">Set to `Ignore` to skip files.</span></span>

  <span data-ttu-id="272b5-128">Tato `PromptUser` akce, ve výchozím nastavení, zobrazí výzvu k zadání všech konfliktních souborů `OverwriteAll` , pokud ani `IgnoreAll` není zadáno, který bude platit pro všechny zbývající soubory.</span><span class="sxs-lookup"><span data-stu-id="272b5-128">The `PromptUser` action, the default, will prompt for each conflicting file unless `OverwriteAll` or `IgnoreAll` is provided, which will apply to all remaining files.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="272b5-129">*(3.5 +)* Vynutí spuštění nuget.exe s využitím neutrální jazykové verze založené na angličtině.</span><span class="sxs-lookup"><span data-stu-id="272b5-129">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="272b5-130">Zobrazí informace o nápovědě k příkazu.</span><span class="sxs-lookup"><span data-stu-id="272b5-130">Displays help information for the command.</span></span>

- **`-Id`**

  <span data-ttu-id="272b5-131">Určuje seznam ID balíčků, které se mají aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="272b5-131">Specifies a list of package IDs to update.</span></span>

- **`-MSBuildPath`**

  <span data-ttu-id="272b5-132">*(4.0 +)* Určuje cestu nástroje MSBuild, který má být použit s příkazem, přičemž přednost využije `-MSBuildVersion` .</span><span class="sxs-lookup"><span data-stu-id="272b5-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="272b5-133">*(3.2 +)* Určuje verzi nástroje MSBuild, která má být použita s tímto příkazem.</span><span class="sxs-lookup"><span data-stu-id="272b5-133">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="272b5-134">Podporované hodnoty jsou 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="272b5-134">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="272b5-135">Ve výchozím nastavení je nástroj MSBuild v cestě vybrán, jinak má výchozí nejvyšší nainstalovanou verzi nástroje MSBuild.</span><span class="sxs-lookup"><span data-stu-id="272b5-135">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="272b5-136">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="272b5-136">Suppresses prompts for user input or confirmations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="272b5-137">Umožňuje aktualizaci předprodejních verzí.</span><span class="sxs-lookup"><span data-stu-id="272b5-137">Allows updating to prerelease versions.</span></span> <span data-ttu-id="272b5-138">Tento příznak není požadován při aktualizaci předprodejních balíčků, které jsou již nainstalovány.</span><span class="sxs-lookup"><span data-stu-id="272b5-138">This flag is not required when updating prerelease packages that are already installed.</span></span>

- **`-RepositoryPath`**

  <span data-ttu-id="272b5-139">Určuje místní složku, ve které jsou balíčky nainstalované.</span><span class="sxs-lookup"><span data-stu-id="272b5-139">Specifies the local folder where packages are installed.</span></span>

- **`-Safe`**

  <span data-ttu-id="272b5-140">Určuje, že se budou instalovat jenom aktualizace s nejvyšší verzí dostupnou v rámci stejné hlavní a dílčí verze, jako je nainstalovaný balíček.</span><span class="sxs-lookup"><span data-stu-id="272b5-140">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span>

- **`-Self`**

  <span data-ttu-id="272b5-141">Aktualizuje `nuget.exe` na nejnovější verzi.</span><span class="sxs-lookup"><span data-stu-id="272b5-141">Updates `nuget.exe` to the latest version.</span></span> <span data-ttu-id="272b5-142">`-Source` dá se použít, ale všechny ostatní argumenty se ignorují.</span><span class="sxs-lookup"><span data-stu-id="272b5-142">`-Source` can be used however all other arguments are ignored.</span></span> <span data-ttu-id="272b5-143">Pokud není zadaný žádný zdroj, vyhledá `nuget.org` aktualizace bez ohledu na `NuGet.Config` nastavení.</span><span class="sxs-lookup"><span data-stu-id="272b5-143">If no source is provided, checks `nuget.org` for updates regardless of `NuGet.Config` settings.</span></span>

- **`-Source`**

  <span data-ttu-id="272b5-144">Určuje seznam zdrojů balíčků (jako adresy URL), které se mají použít pro aktualizace.</span><span class="sxs-lookup"><span data-stu-id="272b5-144">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="272b5-145">Pokud je tato hodnota vynechána, příkaz použije zdroje zadané v konfiguračních souborech, viz [běžné konfigurace NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="272b5-145">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="272b5-146">Určuje množství podrobností zobrazených ve výstupu: `normal` (výchozí), `quiet` nebo `detailed` .</span><span class="sxs-lookup"><span data-stu-id="272b5-146">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="272b5-147">Při použití s jedním ID balíčku určuje verzi balíčku, který se má aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="272b5-147">When used with one package ID, specifies the version of the package to update.</span></span>

<span data-ttu-id="272b5-148">Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="272b5-148">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="272b5-149">Příklady</span><span class="sxs-lookup"><span data-stu-id="272b5-149">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
