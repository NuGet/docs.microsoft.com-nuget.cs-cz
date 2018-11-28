---
title: Příkaz balíčku NuGet rozhraní příkazového řádku
description: Referenční informace pro příkaz pack nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b5bd8bd30ad134f36433b8e4721ce131425a1483
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453361"
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="93da6-103">Příkaz Pack (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="93da6-103">pack command (NuGet CLI)</span></span>

<span data-ttu-id="93da6-104">**Platí pro:** vytvoření balíčku &bullet; **podporované verze:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="93da6-104">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="93da6-105">Vytvoří balíček NuGet stanoveného `.nuspec` nebo soubor projektu.</span><span class="sxs-lookup"><span data-stu-id="93da6-105">Creates a NuGet package based on the specified `.nuspec` or project file.</span></span> <span data-ttu-id="93da6-106">`dotnet pack` Příkazu (naleznete v tématu [příkazy dotnet](dotnet-Commands.md)) a `msbuild -t:pack` (naleznete v tématu [cíle nástroje MSBuild](../reference/msbuild-targets.md)) mohou být použity jako alternativní úložiště.</span><span class="sxs-lookup"><span data-stu-id="93da6-106">The `dotnet pack` command (see [dotnet Commands](dotnet-Commands.md)) and `msbuild -t:pack` (see [MSBuild targets](../reference/msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="93da6-107">Mono se nepodporuje vytváření balíčku ze souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="93da6-107">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="93da6-108">Budete také muset upravit jiné než místní cesty v `.nuspec` sdílené cesty stylu systému Unix, jak nuget.exe nepřevádí Windows cesty, samotného.</span><span class="sxs-lookup"><span data-stu-id="93da6-108">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="93da6-109">Použití</span><span class="sxs-lookup"><span data-stu-id="93da6-109">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

<span data-ttu-id="93da6-110">kde `<nuspecPath>` a `<projectPath>` zadejte `.nuspec` nebo souboru, resp. projektu.</span><span class="sxs-lookup"><span data-stu-id="93da6-110">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="93da6-111">Možnosti</span><span class="sxs-lookup"><span data-stu-id="93da6-111">Options</span></span>

| <span data-ttu-id="93da6-112">Možnost</span><span class="sxs-lookup"><span data-stu-id="93da6-112">Option</span></span> | <span data-ttu-id="93da6-113">Popis</span><span class="sxs-lookup"><span data-stu-id="93da6-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="93da6-114">BasePath</span><span class="sxs-lookup"><span data-stu-id="93da6-114">BasePath</span></span> | <span data-ttu-id="93da6-115">Nastaví základní cestu k souborům definovaným v `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="93da6-115">Sets the base path of the files defined in the `.nuspec` file.</span></span> |
| <span data-ttu-id="93da6-116">Sestavení</span><span class="sxs-lookup"><span data-stu-id="93da6-116">Build</span></span> | <span data-ttu-id="93da6-117">Určuje, zda by měly být sestaveny projektu před vytvořením balíčku.</span><span class="sxs-lookup"><span data-stu-id="93da6-117">Specifies that the project should be built before building the package.</span></span> |
| <span data-ttu-id="93da6-118">Vyloučení</span><span class="sxs-lookup"><span data-stu-id="93da6-118">Exclude</span></span> | <span data-ttu-id="93da6-119">Určuje nejméně jeden vzor zástupných znaků pro vyloučení při vytváření balíčku.</span><span class="sxs-lookup"><span data-stu-id="93da6-119">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="93da6-120">Chcete-li zadat více než jeden vzor, opakujte příznak - vyloučení.</span><span class="sxs-lookup"><span data-stu-id="93da6-120">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="93da6-121">Viz následující příklad.</span><span class="sxs-lookup"><span data-stu-id="93da6-121">See example below.</span></span> |
| <span data-ttu-id="93da6-122">ExcludeEmptyDirectories</span><span class="sxs-lookup"><span data-stu-id="93da6-122">ExcludeEmptyDirectories</span></span> | <span data-ttu-id="93da6-123">Zabraňuje zahrnovaly prázdné adresáře při sestavování balíčku.</span><span class="sxs-lookup"><span data-stu-id="93da6-123">Prevents inclusion of empty directories when building the package.</span></span> |
| <span data-ttu-id="93da6-124">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="93da6-124">ForceEnglishOutput</span></span> | <span data-ttu-id="93da6-125">*(3.5 +)*  Vynutí nuget.exe pro spuštění pomocí neutrální, základem je angličtina jazyková verze.</span><span class="sxs-lookup"><span data-stu-id="93da6-125">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="93da6-126">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="93da6-126">ConfigFile</span></span> | <span data-ttu-id="93da6-127">Zadejte konfigurační soubor pro příkaz pack.</span><span class="sxs-lookup"><span data-stu-id="93da6-127">Specify the configuration file for the pack command.</span></span> |
| <span data-ttu-id="93da6-128">Nápověda</span><span class="sxs-lookup"><span data-stu-id="93da6-128">Help</span></span> | <span data-ttu-id="93da6-129">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="93da6-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="93da6-130">IncludeReferencedProjects</span><span class="sxs-lookup"><span data-stu-id="93da6-130">IncludeReferencedProjects</span></span> | <span data-ttu-id="93da6-131">Označuje, že sestavení balíčku by měl zahrnovat odkazované projekty buď jako závislosti, nebo jako součást balíčku.</span><span class="sxs-lookup"><span data-stu-id="93da6-131">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="93da6-132">Pokud odkazovaný projekt má odpovídající `.nuspec` soubor, který má stejný název jako projekt, pak tento Odkazovaný projekt je přidán jako závislost.</span><span class="sxs-lookup"><span data-stu-id="93da6-132">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="93da6-133">V opačném případě Odkazovaný projekt je přidán jako součást balíčku.</span><span class="sxs-lookup"><span data-stu-id="93da6-133">Otherwise, the referenced project is added as part of the package.</span></span> |
| <span data-ttu-id="93da6-134">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="93da6-134">MinClientVersion</span></span> | <span data-ttu-id="93da6-135">Nastavte *minClientVersion* atribut pro vytvořený balíček.</span><span class="sxs-lookup"><span data-stu-id="93da6-135">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="93da6-136">Tato hodnota se přepíše stávající hodnotu *minClientVersion* atribut (pokud existuje) `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="93da6-136">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span> |
| <span data-ttu-id="93da6-137">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="93da6-137">MSBuildPath</span></span> | <span data-ttu-id="93da6-138">*(4.0 +)*  Určuje cestu k používání pomocí příkazu, přednost `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="93da6-138">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="93da6-139">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="93da6-139">MSBuildVersion</span></span> | <span data-ttu-id="93da6-140">*(3.2 +)*  Určuje verzi Msbuildu, který se má použít tento příkaz.</span><span class="sxs-lookup"><span data-stu-id="93da6-140">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="93da6-141">Podporované hodnoty jsou 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="93da6-141">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="93da6-142">Ve výchozím nastavení se vybere MSBuild na vaší cestě jinak je výchozí hodnotou nejvyšší nainstalovaná verze Msbuildu.</span><span class="sxs-lookup"><span data-stu-id="93da6-142">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="93da6-143">NoDefaultExcludes</span><span class="sxs-lookup"><span data-stu-id="93da6-143">NoDefaultExcludes</span></span> | <span data-ttu-id="93da6-144">Zabraňuje standardně vylučovaly NuGet balíček soubory a soubory a složky, které začínají tečkou, jako například `.svn` a `.gitignore`.</span><span class="sxs-lookup"><span data-stu-id="93da6-144">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span> |
| <span data-ttu-id="93da6-145">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="93da6-145">NoPackageAnalysis</span></span> | <span data-ttu-id="93da6-146">Určuje, že balíček by neměl balíčku spustit jeho analýzu po sestavení.</span><span class="sxs-lookup"><span data-stu-id="93da6-146">Specifies that pack should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="93da6-147">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="93da6-147">OutputDirectory</span></span> | <span data-ttu-id="93da6-148">Určuje složku, ve kterém je uložený vytvořený balíček.</span><span class="sxs-lookup"><span data-stu-id="93da6-148">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="93da6-149">Pokud není zadána žádná složka, použije se aktuální složce.</span><span class="sxs-lookup"><span data-stu-id="93da6-149">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="93da6-150">Vlastnosti</span><span class="sxs-lookup"><span data-stu-id="93da6-150">Properties</span></span> | <span data-ttu-id="93da6-151">By se zobrazit poslední na příkazovém řádku po další možnosti.</span><span class="sxs-lookup"><span data-stu-id="93da6-151">Should appear last on the command line after other options.</span></span> <span data-ttu-id="93da6-152">Určuje seznam vlastností, které přepisují hodnoty v souboru projektu. Zobrazit [obecné vlastnosti projektu nástroje MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) pro názvy vlastností.</span><span class="sxs-lookup"><span data-stu-id="93da6-152">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="93da6-153">Vlastnosti argumentu tady je seznam token = dvojice hodnot oddělených středníkem, ve kterém každý výskyt `$token$` v `.nuspec` soubor se nahradí zadanou hodnotu.</span><span class="sxs-lookup"><span data-stu-id="93da6-153">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="93da6-154">Hodnoty mohou být řetězce v uvozovkách.</span><span class="sxs-lookup"><span data-stu-id="93da6-154">Values can be strings in quotation marks.</span></span> <span data-ttu-id="93da6-155">Všimněte si, že pro vlastnost "Konfigurace" Výchozí hodnota je "Debug".</span><span class="sxs-lookup"><span data-stu-id="93da6-155">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="93da6-156">Chcete-li změnit konfiguraci vydané verze, použijte `-Properties Configuration=Release`.</span><span class="sxs-lookup"><span data-stu-id="93da6-156">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> |
| <span data-ttu-id="93da6-157">Přípona</span><span class="sxs-lookup"><span data-stu-id="93da6-157">Suffix</span></span> | <span data-ttu-id="93da6-158">*(3.4.4+)*  Připojí přípona interně vygenerovanému číslu verze, obvykle se používá pro připojování sestavení nebo jiné předběžné verze identifikátory.</span><span class="sxs-lookup"><span data-stu-id="93da6-158">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="93da6-159">Například použití `-suffix nightly` vytvoří balíček s lajk číslo verze `1.2.3-nightly`.</span><span class="sxs-lookup"><span data-stu-id="93da6-159">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="93da6-160">Přípony musí začínat písmenem, aby se zabránilo upozornění a chyby, kde najdete potenciální nekompatibility s různými verzemi nástroje NuGet a Správce balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="93da6-160">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span> |
| <span data-ttu-id="93da6-161">Symboly</span><span class="sxs-lookup"><span data-stu-id="93da6-161">Symbols</span></span> | <span data-ttu-id="93da6-162">Určuje, zda balíček obsahuje zdroje a symbolů.</span><span class="sxs-lookup"><span data-stu-id="93da6-162">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="93da6-163">Při použití s `.nuspec` soubor, vytvoří běžný soubor balíčku NuGet a odpovídající balíček symbolů.</span><span class="sxs-lookup"><span data-stu-id="93da6-163">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> <span data-ttu-id="93da6-164">Ve výchozím nastavení vytvoří [symbol starší verze balíčku](../create-packages/Symbol-Packages.md).</span><span class="sxs-lookup"><span data-stu-id="93da6-164">By default it creates a [legacy symbol package](../create-packages/Symbol-Packages.md).</span></span> <span data-ttu-id="93da6-165">Nové doporučený formát pro balíčky symbolů je .snupkg.</span><span class="sxs-lookup"><span data-stu-id="93da6-165">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="93da6-166">Zobrazit [vytváření balíčků symbolů (.snupkg)](../create-packages/Symbol-Packages-snupkg.md).</span><span class="sxs-lookup"><span data-stu-id="93da6-166">See [Creating symbol packages (.snupkg)](../create-packages/Symbol-Packages-snupkg.md).</span></span> |
| <span data-ttu-id="93da6-167">Nástroj</span><span class="sxs-lookup"><span data-stu-id="93da6-167">Tool</span></span> | <span data-ttu-id="93da6-168">Určuje, že výstupní soubory projektu musí být umístěné ve `tool` složky.</span><span class="sxs-lookup"><span data-stu-id="93da6-168">Specifies that the output files of the project should be placed in the `tool` folder.</span></span> |
| <span data-ttu-id="93da6-169">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="93da6-169">Verbosity</span></span> | <span data-ttu-id="93da6-170">Určuje množství podrobností, na které se zobrazí ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="93da6-170">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="93da6-171">Version</span><span class="sxs-lookup"><span data-stu-id="93da6-171">Version</span></span> | <span data-ttu-id="93da6-172">Přepíše číslo verze z `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="93da6-172">Overrides the version number from the `.nuspec` file.</span></span> |

<span data-ttu-id="93da6-173">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="93da6-173">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="93da6-174">Kromě závislosti vývoj</span><span class="sxs-lookup"><span data-stu-id="93da6-174">Excluding development dependencies</span></span>

<span data-ttu-id="93da6-175">Některé balíčky NuGet jsou užitečné jako vývoj závislosti, které umožňují vytvářet vlastní knihovny, ale nutně nevyžadují jako závislosti skutečného balíčku.</span><span class="sxs-lookup"><span data-stu-id="93da6-175">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="93da6-176">`pack` Ignoruje příkaz `package` položky v `packages.config` , které mají `developmentDependency` atribut nastaven na `true`.</span><span class="sxs-lookup"><span data-stu-id="93da6-176">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="93da6-177">Tyto položky nesmí obsahovat jako závislosti v vytvořený balíček.</span><span class="sxs-lookup"><span data-stu-id="93da6-177">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="93da6-178">Představte si třeba následující `packages.config` soubor zdrojového projektu:</span><span class="sxs-lookup"><span data-stu-id="93da6-178">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="93da6-179">Pro tento projekt vytvořil balíček `nuget pack` bude mít závislost na `jQuery` a `microsoft-web-helpers` , ale ne `netfx-Guard`.</span><span class="sxs-lookup"><span data-stu-id="93da6-179">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="examples"></a><span data-ttu-id="93da6-180">Příklady</span><span class="sxs-lookup"><span data-stu-id="93da6-180">Examples</span></span>

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -MSBuildVersion 12 -Properties owners=janedoe,xiaop;version="1.0.5

# Create a package from project foo.nuspec and the corresponding symbol package using the new recommended format .snupkg
nuget pack foo.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
