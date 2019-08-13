---
title: NuGet – příkaz packu CLI
description: Reference k příkazu NuGet. exe Pack
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: cab56cb87f46335f9fdebdbc1649fead16459877
ms.sourcegitcommit: 9803981c90a1ed954dc11ed71731264c0e75ea0a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2019
ms.locfileid: "68959727"
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="f12d4-103">Příkaz Pack (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="f12d4-103">pack command (NuGet CLI)</span></span>

<span data-ttu-id="f12d4-104">**Platí pro:** vytváření &bullet; balíčků **podporuje verze:** 2.7+</span><span class="sxs-lookup"><span data-stu-id="f12d4-104">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="f12d4-105">Vytvoří balíček NuGet založený na zadaném souboru [. nuspec](../nuspec.md) nebo projektu.</span><span class="sxs-lookup"><span data-stu-id="f12d4-105">Creates a NuGet package based on the specified [.nuspec](../nuspec.md) or project file.</span></span> <span data-ttu-id="f12d4-106">Příkaz (viz [příkazy dotnet](../dotnet-Commands.md)) a `msbuild -t:pack` (viz [cíle nástroje MSBuild](../msbuild-targets.md)) lze použít jako alternativy. `dotnet pack`</span><span class="sxs-lookup"><span data-stu-id="f12d4-106">The `dotnet pack` command (see [dotnet Commands](../dotnet-Commands.md)) and `msbuild -t:pack` (see [MSBuild targets](../msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="f12d4-107">V rámci mono není podporováno vytváření balíčku ze souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="f12d4-107">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="f12d4-108">Také je nutné upravit jiné než místní cesty v `.nuspec` souboru na cesty ve stylu systému UNIX, protože NuGet. exe nepřevádí samotné cesty systému Windows.</span><span class="sxs-lookup"><span data-stu-id="f12d4-108">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="f12d4-109">Použití</span><span class="sxs-lookup"><span data-stu-id="f12d4-109">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

<span data-ttu-id="f12d4-110">kde `<nuspecPath>` a `<projectPath>` Zadejte`.nuspec` soubor projektu, v uvedeném pořadí.</span><span class="sxs-lookup"><span data-stu-id="f12d4-110">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="f12d4-111">Možnosti</span><span class="sxs-lookup"><span data-stu-id="f12d4-111">Options</span></span>

| <span data-ttu-id="f12d4-112">Možnost</span><span class="sxs-lookup"><span data-stu-id="f12d4-112">Option</span></span> | <span data-ttu-id="f12d4-113">Popis</span><span class="sxs-lookup"><span data-stu-id="f12d4-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f12d4-114">BasePath</span><span class="sxs-lookup"><span data-stu-id="f12d4-114">BasePath</span></span> | <span data-ttu-id="f12d4-115">Nastaví základní cestu souborů definovaných v souboru [. nuspec](../nuspec.md) .</span><span class="sxs-lookup"><span data-stu-id="f12d4-115">Sets the base path of the files defined in the [.nuspec](../nuspec.md) file.</span></span> |
| <span data-ttu-id="f12d4-116">Sestavení</span><span class="sxs-lookup"><span data-stu-id="f12d4-116">Build</span></span> | <span data-ttu-id="f12d4-117">Určuje, že projekt by měl být sestaven před sestavením balíčku.</span><span class="sxs-lookup"><span data-stu-id="f12d4-117">Specifies that the project should be built before building the package.</span></span> |
| <span data-ttu-id="f12d4-118">Slevy</span><span class="sxs-lookup"><span data-stu-id="f12d4-118">Exclude</span></span> | <span data-ttu-id="f12d4-119">Určuje jeden nebo více vzorových zástupných znaků, které se mají vyloučit při vytváření balíčku.</span><span class="sxs-lookup"><span data-stu-id="f12d4-119">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="f12d4-120">Chcete-li zadat více než jeden vzor, opakujte příznak-Exclude.</span><span class="sxs-lookup"><span data-stu-id="f12d4-120">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="f12d4-121">Viz následující příklad.</span><span class="sxs-lookup"><span data-stu-id="f12d4-121">See example below.</span></span> |
| <span data-ttu-id="f12d4-122">ExcludeEmptyDirectories</span><span class="sxs-lookup"><span data-stu-id="f12d4-122">ExcludeEmptyDirectories</span></span> | <span data-ttu-id="f12d4-123">Zabrání zahrnutí prázdných adresářů při sestavování balíčku.</span><span class="sxs-lookup"><span data-stu-id="f12d4-123">Prevents inclusion of empty directories when building the package.</span></span> |
| <span data-ttu-id="f12d4-124">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f12d4-124">ForceEnglishOutput</span></span> | <span data-ttu-id="f12d4-125">*(3.5 +)* Vynutí, aby soubor NuGet. exe běžel pomocí neutrální jazykové verze určené pro angličtinu.</span><span class="sxs-lookup"><span data-stu-id="f12d4-125">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f12d4-126">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f12d4-126">ConfigFile</span></span> | <span data-ttu-id="f12d4-127">Zadejte konfigurační soubor pro příkaz Pack.</span><span class="sxs-lookup"><span data-stu-id="f12d4-127">Specify the configuration file for the pack command.</span></span> |
| <span data-ttu-id="f12d4-128">Help</span><span class="sxs-lookup"><span data-stu-id="f12d4-128">Help</span></span> | <span data-ttu-id="f12d4-129">Zobrazí informace o nápovědě k příkazu.</span><span class="sxs-lookup"><span data-stu-id="f12d4-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="f12d4-130">IncludeReferencedProjects</span><span class="sxs-lookup"><span data-stu-id="f12d4-130">IncludeReferencedProjects</span></span> | <span data-ttu-id="f12d4-131">Označuje, že sestavený balíček by měl zahrnovat odkazované projekty buď jako závislosti, nebo jako součást balíčku.</span><span class="sxs-lookup"><span data-stu-id="f12d4-131">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="f12d4-132">Pokud má odkazovaný projekt odpovídající `.nuspec` soubor, který má stejný název jako projekt, pak je odkaz na projekt přidán jako závislost.</span><span class="sxs-lookup"><span data-stu-id="f12d4-132">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="f12d4-133">V opačném případě se odkazovaný projekt přidá jako součást balíčku.</span><span class="sxs-lookup"><span data-stu-id="f12d4-133">Otherwise, the referenced project is added as part of the package.</span></span> |
| <span data-ttu-id="f12d4-134">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="f12d4-134">MinClientVersion</span></span> | <span data-ttu-id="f12d4-135">Nastavte atribut *minClientVersion* pro vytvořený balíček.</span><span class="sxs-lookup"><span data-stu-id="f12d4-135">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="f12d4-136">Tato hodnota přepíše hodnotu existujícího atributu *minClientVersion* (pokud existuje) v `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="f12d4-136">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span> |
| <span data-ttu-id="f12d4-137">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="f12d4-137">MSBuildPath</span></span> | <span data-ttu-id="f12d4-138">*(4.0 +)* Určuje cestu nástroje MSBuild, který má být použit s příkazem, přičemž přednost `-MSBuildVersion`využije.</span><span class="sxs-lookup"><span data-stu-id="f12d4-138">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="f12d4-139">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="f12d4-139">MSBuildVersion</span></span> | <span data-ttu-id="f12d4-140">*(3.2 +)* Určuje verzi nástroje MSBuild, která má být použita s tímto příkazem.</span><span class="sxs-lookup"><span data-stu-id="f12d4-140">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="f12d4-141">Podporované hodnoty jsou 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="f12d4-141">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="f12d4-142">Ve výchozím nastavení je nástroj MSBuild v cestě vybrán, jinak má výchozí nejvyšší nainstalovanou verzi nástroje MSBuild.</span><span class="sxs-lookup"><span data-stu-id="f12d4-142">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="f12d4-143">NoDefaultExcludes</span><span class="sxs-lookup"><span data-stu-id="f12d4-143">NoDefaultExcludes</span></span> | <span data-ttu-id="f12d4-144">Zabraňuje výchozímu vyloučení souborů a souborů balíčku NuGet počínaje tečkou, například `.svn` a. `.gitignore`</span><span class="sxs-lookup"><span data-stu-id="f12d4-144">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span> |
| <span data-ttu-id="f12d4-145">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="f12d4-145">NoPackageAnalysis</span></span> | <span data-ttu-id="f12d4-146">Určuje, že sada by neměla po sestavení balíčku spustit analýzu balíčku.</span><span class="sxs-lookup"><span data-stu-id="f12d4-146">Specifies that pack should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="f12d4-147">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="f12d4-147">OutputDirectory</span></span> | <span data-ttu-id="f12d4-148">Určuje složku, ve které je vytvořený balíček uložený.</span><span class="sxs-lookup"><span data-stu-id="f12d4-148">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="f12d4-149">Pokud není zadána žádná složka, je použita aktuální složka.</span><span class="sxs-lookup"><span data-stu-id="f12d4-149">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="f12d4-150">Vlastnosti</span><span class="sxs-lookup"><span data-stu-id="f12d4-150">Properties</span></span> | <span data-ttu-id="f12d4-151">By měl být na příkazovém řádku zobrazen na konci dalších možností.</span><span class="sxs-lookup"><span data-stu-id="f12d4-151">Should appear last on the command line after other options.</span></span> <span data-ttu-id="f12d4-152">Určuje seznam vlastností, které přepíší hodnoty v souboru projektu. názvy vlastností najdete v tématu [běžné vlastnosti projektu nástroje MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) .</span><span class="sxs-lookup"><span data-stu-id="f12d4-152">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="f12d4-153">Argument vlastnosti tady je seznam párů token = hodnota oddělený středníky, kde každý výskyt `$token$` `.nuspec` v souboru bude nahrazen danou hodnotou.</span><span class="sxs-lookup"><span data-stu-id="f12d4-153">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="f12d4-154">Hodnoty mohou být řetězce v uvozovkách.</span><span class="sxs-lookup"><span data-stu-id="f12d4-154">Values can be strings in quotation marks.</span></span> <span data-ttu-id="f12d4-155">Všimněte si, že pro vlastnost "konfigurace" je výchozí hodnota "ladit".</span><span class="sxs-lookup"><span data-stu-id="f12d4-155">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="f12d4-156">Chcete-li přejít na konfiguraci vydané verze `-Properties Configuration=Release`, použijte.</span><span class="sxs-lookup"><span data-stu-id="f12d4-156">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> |
| <span data-ttu-id="f12d4-157">Auditování</span><span class="sxs-lookup"><span data-stu-id="f12d4-157">Suffix</span></span> | <span data-ttu-id="f12d4-158">*(3.4.4 +)* Připojí příponu k interně vygenerovanému číslu verze, které se obvykle používá pro připojení buildu nebo jiné identifikátory předběžného vydání.</span><span class="sxs-lookup"><span data-stu-id="f12d4-158">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="f12d4-159">Například pomocí `-suffix nightly` vytvoříte balíček s číslem verze, jako `1.2.3-nightly`je.</span><span class="sxs-lookup"><span data-stu-id="f12d4-159">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="f12d4-160">Přípony musí začínat písmenem, aby se předešlo varováním, chybám a potenciálním nekompatibilitám s různými verzemi NuGet a správcem balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="f12d4-160">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span> |
| <span data-ttu-id="f12d4-161">Symboly</span><span class="sxs-lookup"><span data-stu-id="f12d4-161">Symbols</span></span> | <span data-ttu-id="f12d4-162">Určuje, že balíček obsahuje zdroje a symboly.</span><span class="sxs-lookup"><span data-stu-id="f12d4-162">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="f12d4-163">Při použití se `.nuspec` souborem se vytvoří pravidelný soubor balíčku NuGet a odpovídající balíček symbolů.</span><span class="sxs-lookup"><span data-stu-id="f12d4-163">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> <span data-ttu-id="f12d4-164">Ve výchozím nastavení vytvoří [starší verzi balíčku symbolů](../../create-packages/Symbol-Packages.md).</span><span class="sxs-lookup"><span data-stu-id="f12d4-164">By default it creates a [legacy symbol package](../../create-packages/Symbol-Packages.md).</span></span> <span data-ttu-id="f12d4-165">Nový doporučený formát pro balíčky symbolů je. snupkg.</span><span class="sxs-lookup"><span data-stu-id="f12d4-165">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="f12d4-166">Viz [vytváření balíčků symbolů (. snupkg)](../../create-packages/Symbol-Packages-snupkg.md).</span><span class="sxs-lookup"><span data-stu-id="f12d4-166">See [Creating symbol packages (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md).</span></span> |
| <span data-ttu-id="f12d4-167">Nástroj</span><span class="sxs-lookup"><span data-stu-id="f12d4-167">Tool</span></span> | <span data-ttu-id="f12d4-168">Určuje, že výstupní soubory projektu by měly být umístěny do `tool` složky.</span><span class="sxs-lookup"><span data-stu-id="f12d4-168">Specifies that the output files of the project should be placed in the `tool` folder.</span></span> |
| <span data-ttu-id="f12d4-169">Verbosity</span><span class="sxs-lookup"><span data-stu-id="f12d4-169">Verbosity</span></span> | <span data-ttu-id="f12d4-170">Určuje množství podrobností zobrazených ve výstupu: *normální*, tichéa *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="f12d4-170">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="f12d4-171">Version</span><span class="sxs-lookup"><span data-stu-id="f12d4-171">Version</span></span> | <span data-ttu-id="f12d4-172">Přepíše číslo verze ze `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="f12d4-172">Overrides the version number from the `.nuspec` file.</span></span> |

<span data-ttu-id="f12d4-173">Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="f12d4-173">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="f12d4-174">Vyloučení závislostí vývoje</span><span class="sxs-lookup"><span data-stu-id="f12d4-174">Excluding development dependencies</span></span>

<span data-ttu-id="f12d4-175">Některé balíčky NuGet jsou užitečné jako závislosti na vývoji, které vám pomůžou vytvářet vlastní knihovny, ale nutně se nevyžadují jako skutečné závislosti balíčků.</span><span class="sxs-lookup"><span data-stu-id="f12d4-175">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="f12d4-176">`package` Příkazbude`packages.config` ignorovat položkyv`true`, které mají atributnastavennahodnotu.`developmentDependency` `pack`</span><span class="sxs-lookup"><span data-stu-id="f12d4-176">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="f12d4-177">Tyto položky nebudou do vytvořeného balíčku zahrnovat jako závislosti.</span><span class="sxs-lookup"><span data-stu-id="f12d4-177">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="f12d4-178">Zvažte například následující `packages.config` soubor ve zdrojovém projektu:</span><span class="sxs-lookup"><span data-stu-id="f12d4-178">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="f12d4-179">Pro tento projekt bude mít balíček vytvořen pomocí `nuget pack` závislost na `jQuery` , `microsoft-web-helpers` ale ne `netfx-Guard`.</span><span class="sxs-lookup"><span data-stu-id="f12d4-179">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="examples"></a><span data-ttu-id="f12d4-180">Příklady</span><span class="sxs-lookup"><span data-stu-id="f12d4-180">Examples</span></span>

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
