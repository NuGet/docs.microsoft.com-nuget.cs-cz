---
title: NuGet – příkaz packu CLI
description: Referenční informace k příkazu nuget.exe Pack
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0483a75c7ee1fd851f935f44d96a417e2e86bf20
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622951"
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="c5843-103">příkaz Pack (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="c5843-103">pack command (NuGet CLI)</span></span>

<span data-ttu-id="c5843-104">**Platí pro:** vytváření balíčků &bullet; **podporuje verze:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="c5843-104">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="c5843-105">Vytvoří balíček NuGet založený na zadaném souboru [. nuspec](../nuspec.md) nebo projektu.</span><span class="sxs-lookup"><span data-stu-id="c5843-105">Creates a NuGet package based on the specified [.nuspec](../nuspec.md) or project file.</span></span> <span data-ttu-id="c5843-106">`dotnet pack`Příkaz (viz [příkazy dotnet](../dotnet-Commands.md)) a `msbuild -t:pack` (viz cíle nástroje [MSBuild](../msbuild-targets.md)) lze použít jako alternativy.</span><span class="sxs-lookup"><span data-stu-id="c5843-106">The `dotnet pack` command (see [dotnet Commands](../dotnet-Commands.md)) and `msbuild -t:pack` (see [MSBuild targets](../msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="c5843-107">Použijte [`dotnet pack`](../dotnet-Commands.md) nebo [`msbuild -t:pack`](../msbuild-targets.md) pro projekty založené na [PackageReference](../../consume-packages/package-references-in-project-files.md) .</span><span class="sxs-lookup"><span data-stu-id="c5843-107">Use [`dotnet pack`](../dotnet-Commands.md) or [`msbuild -t:pack`](../msbuild-targets.md) for [PackageReference](../../consume-packages/package-references-in-project-files.md) based projects.</span></span>
> <span data-ttu-id="c5843-108">V rámci mono není podporováno vytváření balíčku ze souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="c5843-108">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="c5843-109">V souboru je také nutné upravit jiné než místní cesty `.nuspec` k cestám ve stylu systému UNIX, jak nuget.exe nepřevádí samotné cesty systému Windows.</span><span class="sxs-lookup"><span data-stu-id="c5843-109">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="c5843-110">Využití</span><span class="sxs-lookup"><span data-stu-id="c5843-110">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

<span data-ttu-id="c5843-111">kde `<nuspecPath>` a `<projectPath>` Zadejte `.nuspec` soubor projektu, v uvedeném pořadí.</span><span class="sxs-lookup"><span data-stu-id="c5843-111">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="c5843-112">Možnosti</span><span class="sxs-lookup"><span data-stu-id="c5843-112">Options</span></span>
- **`-BasePath`**

   <span data-ttu-id="c5843-113">Nastaví základní cestu souborů definovaných v souboru [. nuspec](../nuspec.md) .</span><span class="sxs-lookup"><span data-stu-id="c5843-113">Sets the base path of the files defined in the [.nuspec](../nuspec.md) file.</span></span>

- **`-Build`**

  <span data-ttu-id="c5843-114">Určuje, že projekt by měl být sestaven před sestavením balíčku.</span><span class="sxs-lookup"><span data-stu-id="c5843-114">Specifies that the project should be built before building the package.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="c5843-115">Konfigurační soubor NuGet, který se má použít</span><span class="sxs-lookup"><span data-stu-id="c5843-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="c5843-116">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows) nebo `~/.nuget/NuGet/NuGet.Config` nebo `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="c5843-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-Exclude`**

  <span data-ttu-id="c5843-117">Určuje jeden nebo více vzorových zástupných znaků, které se mají vyloučit při vytváření balíčku.</span><span class="sxs-lookup"><span data-stu-id="c5843-117">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="c5843-118">Chcete-li zadat více než jeden vzor, opakujte příznak-Exclude.</span><span class="sxs-lookup"><span data-stu-id="c5843-118">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="c5843-119">Viz následující příklad.</span><span class="sxs-lookup"><span data-stu-id="c5843-119">See example below.</span></span>

- **`-ExcludeEmptyDirectories`**

  <span data-ttu-id="c5843-120">Zabrání zahrnutí prázdných adresářů při sestavování balíčku.</span><span class="sxs-lookup"><span data-stu-id="c5843-120">Prevents inclusion of empty directories when building the package.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="c5843-121">*(3.5 +)* Vynutí spuštění nuget.exe s využitím neutrální jazykové verze založené na angličtině.</span><span class="sxs-lookup"><span data-stu-id="c5843-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="c5843-122">Zobrazí informace o nápovědě k příkazu.</span><span class="sxs-lookup"><span data-stu-id="c5843-122">Displays help information for the command.</span></span>

- **`-IncludeReferencedProjects`**

  <span data-ttu-id="c5843-123">Označuje, že sestavený balíček by měl zahrnovat odkazované projekty buď jako závislosti, nebo jako součást balíčku.</span><span class="sxs-lookup"><span data-stu-id="c5843-123">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="c5843-124">Pokud má odkazovaný projekt odpovídající `.nuspec` soubor, který má stejný název jako projekt, pak je odkaz na projekt přidán jako závislost.</span><span class="sxs-lookup"><span data-stu-id="c5843-124">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="c5843-125">V opačném případě se odkazovaný projekt přidá jako součást balíčku.</span><span class="sxs-lookup"><span data-stu-id="c5843-125">Otherwise, the referenced project is added as part of the package.</span></span>

- **`-InstallPackageToOutputPath`**

  <span data-ttu-id="c5843-126">Určete, zda má příkaz připravit adresář výstupu balíčku pro podporu sdílení jako kanálu.</span><span class="sxs-lookup"><span data-stu-id="c5843-126">Specify if the command should prepare the package output directory to support share as feed.</span></span>

- **`-MinClientVersion`**

  <span data-ttu-id="c5843-127">Nastavte atribut *minClientVersion* pro vytvořený balíček.</span><span class="sxs-lookup"><span data-stu-id="c5843-127">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="c5843-128">Tato hodnota přepíše hodnotu existujícího atributu *minClientVersion* (pokud existuje) v `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="c5843-128">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span>

- **`-MSBuildPath`**

  <span data-ttu-id="c5843-129">*(4.0 +)* Určuje cestu nástroje MSBuild, který má být použit s příkazem, přičemž přednost využije `-MSBuildVersion` .</span><span class="sxs-lookup"><span data-stu-id="c5843-129">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="c5843-130">*(3.2 +)* Určuje verzi nástroje MSBuild, která má být použita s tímto příkazem.</span><span class="sxs-lookup"><span data-stu-id="c5843-130">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="c5843-131">Podporované hodnoty jsou 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="c5843-131">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="c5843-132">Ve výchozím nastavení je nástroj MSBuild v cestě vybrán, jinak má výchozí nejvyšší nainstalovanou verzi nástroje MSBuild.</span><span class="sxs-lookup"><span data-stu-id="c5843-132">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NoDefaultExcludes`**

  <span data-ttu-id="c5843-133">Zabraňuje výchozímu vyloučení souborů a souborů balíčku NuGet počínaje tečkou, například `.svn` a `.gitignore` .</span><span class="sxs-lookup"><span data-stu-id="c5843-133">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="c5843-134">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="c5843-134">Suppresses prompts for user input or confirmations.</span></span>

- **`-NoPackageAnalysis`**

  <span data-ttu-id="c5843-135">Určuje, že sada by neměla po sestavení balíčku spustit analýzu balíčku.</span><span class="sxs-lookup"><span data-stu-id="c5843-135">Specifies that pack should not run package analysis after building the package.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="c5843-136">Určuje složku, ve které je vytvořený balíček uložený.</span><span class="sxs-lookup"><span data-stu-id="c5843-136">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="c5843-137">Pokud není zadána žádná složka, je použita aktuální složka.</span><span class="sxs-lookup"><span data-stu-id="c5843-137">If no folder is specified, the current folder is used.</span></span>

- **`-OutputFileNamesWithoutVersion`**

  <span data-ttu-id="c5843-138">Určete, zda má příkaz připravit název výstupu balíčku bez verze.</span><span class="sxs-lookup"><span data-stu-id="c5843-138">Specify if the command should prepare the package output name without the version.</span></span>

- **`-PackagesDirectory`**

  <span data-ttu-id="c5843-139">Určuje složku Packages.</span><span class="sxs-lookup"><span data-stu-id="c5843-139">Specifies the packages folder.</span></span>

- **`-p|-Properties`**

  <span data-ttu-id="c5843-140">By měl být na příkazovém řádku zobrazen na konci dalších možností.</span><span class="sxs-lookup"><span data-stu-id="c5843-140">Should appear last on the command line after other options.</span></span> <span data-ttu-id="c5843-141">Určuje seznam vlastností, které přepíší hodnoty v souboru projektu. názvy vlastností najdete v tématu [běžné vlastnosti projektu nástroje MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) .</span><span class="sxs-lookup"><span data-stu-id="c5843-141">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="c5843-142">Argument vlastnosti tady je seznam párů token = hodnota oddělený středníky, kde každý výskyt `$token$` v `.nuspec` souboru bude nahrazen danou hodnotou.</span><span class="sxs-lookup"><span data-stu-id="c5843-142">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="c5843-143">Hodnoty mohou být řetězce v uvozovkách.</span><span class="sxs-lookup"><span data-stu-id="c5843-143">Values can be strings in quotation marks.</span></span> <span data-ttu-id="c5843-144">Všimněte si, že pro vlastnost "konfigurace" je výchozí hodnota "ladit".</span><span class="sxs-lookup"><span data-stu-id="c5843-144">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="c5843-145">Chcete-li přejít na konfiguraci vydané verze, použijte `-Properties Configuration=Release` .</span><span class="sxs-lookup"><span data-stu-id="c5843-145">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> <span data-ttu-id="c5843-146">**Obecně**platí, že vlastnosti by měly být stejné, jaké byly použity během sestavení odpovídajícího projektu, aby se zabránilo potenciálně podivnému chování.</span><span class="sxs-lookup"><span data-stu-id="c5843-146">**In general**, Properties should be the same that were used during the corresponding project build, in order to avoid potentially strange behavior.</span></span>

- **`-SolutionDirectory`**

  <span data-ttu-id="c5843-147">Určuje adresář řešení.</span><span class="sxs-lookup"><span data-stu-id="c5843-147">Specifies the solution directory.</span></span>

- **`-Suffix`**

  <span data-ttu-id="c5843-148">*(3.4.4 +)* Připojí příponu k interně vygenerovanému číslu verze, které se obvykle používá pro připojení buildu nebo jiné identifikátory předběžného vydání.</span><span class="sxs-lookup"><span data-stu-id="c5843-148">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="c5843-149">Například pomocí vytvoříte `-suffix nightly` balíček s číslem verze, jako je `1.2.3-nightly` .</span><span class="sxs-lookup"><span data-stu-id="c5843-149">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="c5843-150">Přípony musí začínat písmenem, aby se předešlo varováním, chybám a potenciálním nekompatibilitám s různými verzemi NuGet a správcem balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="c5843-150">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span>

- **`-SymbolPackageFormat`**

  <span data-ttu-id="c5843-151">Při vytváření balíčku symbolů umožňuje zvolit mezi `snupkg` `symbols.nupkg` formátem a.</span><span class="sxs-lookup"><span data-stu-id="c5843-151">When creating a symbols package, allows to choose between the `snupkg` and `symbols.nupkg` format.</span></span>

- **`-Symbols`**

  <span data-ttu-id="c5843-152">Určuje, že balíček obsahuje zdroje a symboly.</span><span class="sxs-lookup"><span data-stu-id="c5843-152">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="c5843-153">Při použití se `.nuspec` souborem se vytvoří pravidelný soubor balíčku NuGet a odpovídající balíček symbolů.</span><span class="sxs-lookup"><span data-stu-id="c5843-153">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> <span data-ttu-id="c5843-154">Ve výchozím nastavení vytvoří [starší verzi balíčku symbolů](../../create-packages/Symbol-Packages.md).</span><span class="sxs-lookup"><span data-stu-id="c5843-154">By default it creates a [legacy symbol package](../../create-packages/Symbol-Packages.md).</span></span> <span data-ttu-id="c5843-155">Nový doporučený formát pro balíčky symbolů je. snupkg.</span><span class="sxs-lookup"><span data-stu-id="c5843-155">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="c5843-156">Viz [vytváření balíčků symbolů (. snupkg)](../../create-packages/Symbol-Packages-snupkg.md).</span><span class="sxs-lookup"><span data-stu-id="c5843-156">See [Creating symbol packages (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md).</span></span>

- **`-Tool`**

   <span data-ttu-id="c5843-157">Určuje, že výstupní soubory projektu by měly být umístěny do `tool` složky.</span><span class="sxs-lookup"><span data-stu-id="c5843-157">Specifies that the output files of the project should be placed in the `tool` folder.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="c5843-158">Určuje množství podrobností zobrazených ve výstupu: `normal` (výchozí), `quiet` nebo `detailed` .</span><span class="sxs-lookup"><span data-stu-id="c5843-158">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="c5843-159">Přepíše číslo verze ze `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="c5843-159">Overrides the version number from the `.nuspec` file.</span></span>

<span data-ttu-id="c5843-160">Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="c5843-160">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="c5843-161">Vyloučení závislostí vývoje</span><span class="sxs-lookup"><span data-stu-id="c5843-161">Excluding development dependencies</span></span>

<span data-ttu-id="c5843-162">Některé balíčky NuGet jsou užitečné jako závislosti na vývoji, které vám pomůžou vytvářet vlastní knihovny, ale nutně se nevyžadují jako skutečné závislosti balíčků.</span><span class="sxs-lookup"><span data-stu-id="c5843-162">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="c5843-163">`pack`Příkaz bude ignorovat `package` položky v `packages.config` , které mají `developmentDependency` atribut nastaven na hodnotu `true` .</span><span class="sxs-lookup"><span data-stu-id="c5843-163">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="c5843-164">Tyto položky nebudou do vytvořeného balíčku zahrnovat jako závislosti.</span><span class="sxs-lookup"><span data-stu-id="c5843-164">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="c5843-165">Zvažte například následující `packages.config` soubor ve zdrojovém projektu:</span><span class="sxs-lookup"><span data-stu-id="c5843-165">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="c5843-166">Pro tento projekt bude mít balíček vytvořen pomocí `nuget pack` závislost na `jQuery` , `microsoft-web-helpers` ale ne `netfx-Guard` .</span><span class="sxs-lookup"><span data-stu-id="c5843-166">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="suppressing-pack-warnings"></a><span data-ttu-id="c5843-167">Potlačení upozornění balíčku</span><span class="sxs-lookup"><span data-stu-id="c5843-167">Suppressing pack warnings</span></span>

<span data-ttu-id="c5843-168">I když se vám doporučuje vyřešit všechna upozornění NuGet během operací s balíčkem, v některých případech je jejich potlačení oprávněné.</span><span class="sxs-lookup"><span data-stu-id="c5843-168">While it is recommended that you resolve all NuGet warnings during your pack operations, in certain situations suppressing them is warranted.</span></span>

<span data-ttu-id="c5843-169">Můžete to dosáhnout následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="c5843-169">You can achieve that in the following way:</span></span> 

> <span data-ttu-id="c5843-170">Balíček nuget.exe Pack. nuspec-Properties inwarn = NU5104</span><span class="sxs-lookup"><span data-stu-id="c5843-170">nuget.exe pack package.nuspec -Properties NoWarn=NU5104</span></span>

## <a name="examples"></a><span data-ttu-id="c5843-171">Příklady</span><span class="sxs-lookup"><span data-stu-id="c5843-171">Examples</span></span>

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -MSBuildVersion 12 -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.nuspec and the corresponding symbol package using the new recommended format .snupkg
nuget pack foo.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
