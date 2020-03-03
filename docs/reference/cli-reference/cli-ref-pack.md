---
title: NuGet – příkaz packu CLI
description: Reference k příkazu NuGet. exe Pack
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 2358cedc05520a3ec82a39aef34b6d467e44460b
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231159"
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="61b77-103">Příkaz Pack (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="61b77-103">pack command (NuGet CLI)</span></span>

<span data-ttu-id="61b77-104">**Platí pro:** vytváření balíčků &bullet; **podporovaných verzích:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="61b77-104">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="61b77-105">Vytvoří balíček NuGet založený na zadaném souboru [. nuspec](../nuspec.md) nebo projektu.</span><span class="sxs-lookup"><span data-stu-id="61b77-105">Creates a NuGet package based on the specified [.nuspec](../nuspec.md) or project file.</span></span> <span data-ttu-id="61b77-106">Příkaz `dotnet pack` (viz [příkazy dotnet](../dotnet-Commands.md)) a `msbuild -t:pack` (viz [cíle nástroje MSBuild](../msbuild-targets.md)) mohou být použity jako alternativy.</span><span class="sxs-lookup"><span data-stu-id="61b77-106">The `dotnet pack` command (see [dotnet Commands](../dotnet-Commands.md)) and `msbuild -t:pack` (see [MSBuild targets](../msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="61b77-107">Pro projekty založené na [PackageReference](../../consume-packages/package-references-in-project-files.md) použijte [`dotnet pack`](../dotnet-Commands.md) nebo [`msbuild -t:pack`](../msbuild-targets.md) .</span><span class="sxs-lookup"><span data-stu-id="61b77-107">Use [`dotnet pack`](../dotnet-Commands.md) or [`msbuild -t:pack`](../msbuild-targets.md) for [PackageReference](../../consume-packages/package-references-in-project-files.md) based projects.</span></span>
> <span data-ttu-id="61b77-108">V rámci mono není podporováno vytváření balíčku ze souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="61b77-108">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="61b77-109">Také je nutné upravit jiné než místní cesty v souboru `.nuspec` na cesty ve stylu systému UNIX, protože NuGet. exe nepřevádí samotné cesty systému Windows.</span><span class="sxs-lookup"><span data-stu-id="61b77-109">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="61b77-110">Využití</span><span class="sxs-lookup"><span data-stu-id="61b77-110">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

<span data-ttu-id="61b77-111">kde `<nuspecPath>` a `<projectPath>` určit `.nuspec` nebo soubor projektu, v uvedeném pořadí.</span><span class="sxs-lookup"><span data-stu-id="61b77-111">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="61b77-112">Možnosti</span><span class="sxs-lookup"><span data-stu-id="61b77-112">Options</span></span>

| <span data-ttu-id="61b77-113">Možnost</span><span class="sxs-lookup"><span data-stu-id="61b77-113">Option</span></span> | <span data-ttu-id="61b77-114">Popis</span><span class="sxs-lookup"><span data-stu-id="61b77-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="61b77-115">BasePath</span><span class="sxs-lookup"><span data-stu-id="61b77-115">BasePath</span></span> | <span data-ttu-id="61b77-116">Nastaví základní cestu souborů definovaných v souboru [. nuspec](../nuspec.md) .</span><span class="sxs-lookup"><span data-stu-id="61b77-116">Sets the base path of the files defined in the [.nuspec](../nuspec.md) file.</span></span> |
| <span data-ttu-id="61b77-117">Sestavení</span><span class="sxs-lookup"><span data-stu-id="61b77-117">Build</span></span> | <span data-ttu-id="61b77-118">Určuje, že projekt by měl být sestaven před sestavením balíčku.</span><span class="sxs-lookup"><span data-stu-id="61b77-118">Specifies that the project should be built before building the package.</span></span> |
| <span data-ttu-id="61b77-119">Exclude</span><span class="sxs-lookup"><span data-stu-id="61b77-119">Exclude</span></span> | <span data-ttu-id="61b77-120">Určuje jeden nebo více vzorových zástupných znaků, které se mají vyloučit při vytváření balíčku.</span><span class="sxs-lookup"><span data-stu-id="61b77-120">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="61b77-121">Chcete-li zadat více než jeden vzor, opakujte příznak-Exclude.</span><span class="sxs-lookup"><span data-stu-id="61b77-121">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="61b77-122">Viz následující příklad.</span><span class="sxs-lookup"><span data-stu-id="61b77-122">See example below.</span></span> |
| <span data-ttu-id="61b77-123">ExcludeEmptyDirectories</span><span class="sxs-lookup"><span data-stu-id="61b77-123">ExcludeEmptyDirectories</span></span> | <span data-ttu-id="61b77-124">Zabrání zahrnutí prázdných adresářů při sestavování balíčku.</span><span class="sxs-lookup"><span data-stu-id="61b77-124">Prevents inclusion of empty directories when building the package.</span></span> |
| <span data-ttu-id="61b77-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="61b77-125">ForceEnglishOutput</span></span> | <span data-ttu-id="61b77-126">*(3.5 +)* Vynutí, aby soubor NuGet. exe běžel pomocí neutrální jazykové verze určené pro angličtinu.</span><span class="sxs-lookup"><span data-stu-id="61b77-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="61b77-127">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="61b77-127">ConfigFile</span></span> | <span data-ttu-id="61b77-128">Zadejte konfigurační soubor pro příkaz Pack.</span><span class="sxs-lookup"><span data-stu-id="61b77-128">Specify the configuration file for the pack command.</span></span> |
| <span data-ttu-id="61b77-129">Nápověda</span><span class="sxs-lookup"><span data-stu-id="61b77-129">Help</span></span> | <span data-ttu-id="61b77-130">Zobrazí informace o nápovědě k příkazu.</span><span class="sxs-lookup"><span data-stu-id="61b77-130">Displays help information for the command.</span></span> |
| <span data-ttu-id="61b77-131">IncludeReferencedProjects</span><span class="sxs-lookup"><span data-stu-id="61b77-131">IncludeReferencedProjects</span></span> | <span data-ttu-id="61b77-132">Označuje, že sestavený balíček by měl zahrnovat odkazované projekty buď jako závislosti, nebo jako součást balíčku.</span><span class="sxs-lookup"><span data-stu-id="61b77-132">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="61b77-133">Pokud má odkazovaný projekt odpovídající soubor `.nuspec`, který má stejný název jako projekt, pak je odkaz na projekt přidán jako závislost.</span><span class="sxs-lookup"><span data-stu-id="61b77-133">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="61b77-134">V opačném případě se odkazovaný projekt přidá jako součást balíčku.</span><span class="sxs-lookup"><span data-stu-id="61b77-134">Otherwise, the referenced project is added as part of the package.</span></span> |
| <span data-ttu-id="61b77-135">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="61b77-135">MinClientVersion</span></span> | <span data-ttu-id="61b77-136">Nastavte atribut *minClientVersion* pro vytvořený balíček.</span><span class="sxs-lookup"><span data-stu-id="61b77-136">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="61b77-137">Tato hodnota přepíše hodnotu existujícího atributu *minClientVersion* (pokud existuje) v souboru `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="61b77-137">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span> |
| <span data-ttu-id="61b77-138">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="61b77-138">MSBuildPath</span></span> | <span data-ttu-id="61b77-139">*(4.0 +)* Určuje cestu nástroje MSBuild, který má být použit s příkazem, přičemž má přednost před `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="61b77-139">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="61b77-140">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="61b77-140">MSBuildVersion</span></span> | <span data-ttu-id="61b77-141">*(3.2 +)* Určuje verzi nástroje MSBuild, která má být použita s tímto příkazem.</span><span class="sxs-lookup"><span data-stu-id="61b77-141">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="61b77-142">Podporované hodnoty jsou 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="61b77-142">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="61b77-143">Ve výchozím nastavení je nástroj MSBuild v cestě vybrán, jinak má výchozí nejvyšší nainstalovanou verzi nástroje MSBuild.</span><span class="sxs-lookup"><span data-stu-id="61b77-143">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="61b77-144">NoDefaultExcludes</span><span class="sxs-lookup"><span data-stu-id="61b77-144">NoDefaultExcludes</span></span> | <span data-ttu-id="61b77-145">Zabraňuje výchozímu vyloučení souborů a souborů balíčku NuGet začínajících tečkou, například `.svn` a `.gitignore`.</span><span class="sxs-lookup"><span data-stu-id="61b77-145">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span> |
| <span data-ttu-id="61b77-146">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="61b77-146">NoPackageAnalysis</span></span> | <span data-ttu-id="61b77-147">Určuje, že sada by neměla po sestavení balíčku spustit analýzu balíčku.</span><span class="sxs-lookup"><span data-stu-id="61b77-147">Specifies that pack should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="61b77-148">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="61b77-148">OutputDirectory</span></span> | <span data-ttu-id="61b77-149">Určuje složku, ve které je vytvořený balíček uložený.</span><span class="sxs-lookup"><span data-stu-id="61b77-149">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="61b77-150">Pokud není zadána žádná složka, je použita aktuální složka.</span><span class="sxs-lookup"><span data-stu-id="61b77-150">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="61b77-151">Vlastnosti</span><span class="sxs-lookup"><span data-stu-id="61b77-151">Properties</span></span> | <span data-ttu-id="61b77-152">By měl být na příkazovém řádku zobrazen na konci dalších možností.</span><span class="sxs-lookup"><span data-stu-id="61b77-152">Should appear last on the command line after other options.</span></span> <span data-ttu-id="61b77-153">Určuje seznam vlastností, které přepíší hodnoty v souboru projektu. názvy vlastností najdete v tématu [běžné vlastnosti projektu nástroje MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) .</span><span class="sxs-lookup"><span data-stu-id="61b77-153">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="61b77-154">Argument vlastnosti tady je seznam párů token = hodnota oddělený středníky, kde každý výskyt `$token$` v `.nuspec` souboru se nahradí zadanou hodnotou.</span><span class="sxs-lookup"><span data-stu-id="61b77-154">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="61b77-155">Hodnoty mohou být řetězce v uvozovkách.</span><span class="sxs-lookup"><span data-stu-id="61b77-155">Values can be strings in quotation marks.</span></span> <span data-ttu-id="61b77-156">Všimněte si, že pro vlastnost "konfigurace" je výchozí hodnota "ladit".</span><span class="sxs-lookup"><span data-stu-id="61b77-156">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="61b77-157">Chcete-li přejít na konfiguraci vydané verze, použijte `-Properties Configuration=Release`.</span><span class="sxs-lookup"><span data-stu-id="61b77-157">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> <span data-ttu-id="61b77-158">**Obecně**platí, že vlastnosti by měly být stejné, jaké byly použity během příslušných `nuget build`, aby se zabránilo potenciálně podivnému chování.</span><span class="sxs-lookup"><span data-stu-id="61b77-158">**In general**, Properties should be the same that were used during the corresponding `nuget build`, in order to avoid potentially strange behavior.</span></span> |
| <span data-ttu-id="61b77-159">Auditování</span><span class="sxs-lookup"><span data-stu-id="61b77-159">Suffix</span></span> | <span data-ttu-id="61b77-160">*(3.4.4 +)* Připojí příponu k interně vygenerovanému číslu verze, které se obvykle používá pro připojení buildu nebo jiné identifikátory předběžného vydání.</span><span class="sxs-lookup"><span data-stu-id="61b77-160">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="61b77-161">Například při použití `-suffix nightly` se vytvoří balíček s číslem verze, jako je `1.2.3-nightly`.</span><span class="sxs-lookup"><span data-stu-id="61b77-161">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="61b77-162">Přípony musí začínat písmenem, aby se předešlo varováním, chybám a potenciálním nekompatibilitám s různými verzemi NuGet a správcem balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="61b77-162">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span> |
| <span data-ttu-id="61b77-163">Symboly</span><span class="sxs-lookup"><span data-stu-id="61b77-163">Symbols</span></span> | <span data-ttu-id="61b77-164">Určuje, že balíček obsahuje zdroje a symboly.</span><span class="sxs-lookup"><span data-stu-id="61b77-164">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="61b77-165">Při použití s `.nuspec` souborem se vytvoří pravidelný soubor balíčku NuGet a odpovídající balíček symbolů.</span><span class="sxs-lookup"><span data-stu-id="61b77-165">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> <span data-ttu-id="61b77-166">Ve výchozím nastavení vytvoří [starší verzi balíčku symbolů](../../create-packages/Symbol-Packages.md).</span><span class="sxs-lookup"><span data-stu-id="61b77-166">By default it creates a [legacy symbol package](../../create-packages/Symbol-Packages.md).</span></span> <span data-ttu-id="61b77-167">Nový doporučený formát pro balíčky symbolů je. snupkg.</span><span class="sxs-lookup"><span data-stu-id="61b77-167">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="61b77-168">Viz [vytváření balíčků symbolů (. snupkg)](../../create-packages/Symbol-Packages-snupkg.md).</span><span class="sxs-lookup"><span data-stu-id="61b77-168">See [Creating symbol packages (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md).</span></span> |
| <span data-ttu-id="61b77-169">Nástroj</span><span class="sxs-lookup"><span data-stu-id="61b77-169">Tool</span></span> | <span data-ttu-id="61b77-170">Určuje, že výstupní soubory projektu by měly být umístěny do složky `tool`.</span><span class="sxs-lookup"><span data-stu-id="61b77-170">Specifies that the output files of the project should be placed in the `tool` folder.</span></span> |
| <span data-ttu-id="61b77-171">Verbosity</span><span class="sxs-lookup"><span data-stu-id="61b77-171">Verbosity</span></span> | <span data-ttu-id="61b77-172">Určuje množství podrobností zobrazených ve výstupu: *normální*, *tiché*a *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="61b77-172">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="61b77-173">Version</span><span class="sxs-lookup"><span data-stu-id="61b77-173">Version</span></span> | <span data-ttu-id="61b77-174">Přepíše číslo verze ze souboru `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="61b77-174">Overrides the version number from the `.nuspec` file.</span></span> |

<span data-ttu-id="61b77-175">Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="61b77-175">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="61b77-176">Vyloučení závislostí vývoje</span><span class="sxs-lookup"><span data-stu-id="61b77-176">Excluding development dependencies</span></span>

<span data-ttu-id="61b77-177">Některé balíčky NuGet jsou užitečné jako závislosti na vývoji, které vám pomůžou vytvářet vlastní knihovny, ale nutně se nevyžadují jako skutečné závislosti balíčků.</span><span class="sxs-lookup"><span data-stu-id="61b77-177">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="61b77-178">Příkaz `pack` bude ignorovat `package` záznamů v `packages.config`, které mají atribut `developmentDependency` nastaven na `true`.</span><span class="sxs-lookup"><span data-stu-id="61b77-178">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="61b77-179">Tyto položky nebudou do vytvořeného balíčku zahrnovat jako závislosti.</span><span class="sxs-lookup"><span data-stu-id="61b77-179">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="61b77-180">Zvažte například následující soubor `packages.config` ve zdrojovém projektu:</span><span class="sxs-lookup"><span data-stu-id="61b77-180">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="61b77-181">Pro tento projekt bude balíček vytvořený pomocí `nuget pack` mít závislost na `jQuery` a `microsoft-web-helpers`, ale ne `netfx-Guard`.</span><span class="sxs-lookup"><span data-stu-id="61b77-181">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="suppressing-pack-warnings"></a><span data-ttu-id="61b77-182">Potlačení upozornění balíčku</span><span class="sxs-lookup"><span data-stu-id="61b77-182">Suppressing pack warnings</span></span>

<span data-ttu-id="61b77-183">I když se vám doporučuje vyřešit všechna upozornění NuGet během operací s balíčkem, v některých případech je jejich potlačení oprávněné.</span><span class="sxs-lookup"><span data-stu-id="61b77-183">While it is recommended that you resolve all NuGet warnings during your pack operations, in certain situations suppressing them is warranted.</span></span>

<span data-ttu-id="61b77-184">Můžete to dosáhnout následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="61b77-184">You can achieve that in the following way:</span></span> 

> <span data-ttu-id="61b77-185">NuGet. exe Pack Package. nuspec-Properties-inwarn = NU5104</span><span class="sxs-lookup"><span data-stu-id="61b77-185">nuget.exe pack package.nuspec -Properties NoWarn=NU5104</span></span>

## <a name="examples"></a><span data-ttu-id="61b77-186">Příklady</span><span class="sxs-lookup"><span data-stu-id="61b77-186">Examples</span></span>

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
