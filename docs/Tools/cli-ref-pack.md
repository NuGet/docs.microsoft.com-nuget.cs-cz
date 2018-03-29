---
title: Příkaz pack NuGet rozhraní příkazového řádku | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referenční dokumentace pro příkaz nuget.exe pack
keywords: odkaz na pack nuget, příkaz pack
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 14ecf724477f652275eb68a090bb57b8640d4a8a
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="1e4e9-104">příkaz Pack (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="1e4e9-104">pack command (NuGet CLI)</span></span>

<span data-ttu-id="1e4e9-105">**Platí pro:** balíček vytvoření &bullet; **podporované verze:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="1e4e9-105">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="1e4e9-106">Vytvoří balíček NuGet založený na zadaný `.nuspec` nebo soubor projektu.</span><span class="sxs-lookup"><span data-stu-id="1e4e9-106">Creates a NuGet package based on the specified `.nuspec` or project file.</span></span> <span data-ttu-id="1e4e9-107">`dotnet pack` Příkazu (najdete v části [dotnet příkazy](dotnet-Commands.md)) a `msbuild /t:pack` (najdete v části [cíle MSBuild](../reference/msbuild-targets.md)) může být použita jako alternativ.</span><span class="sxs-lookup"><span data-stu-id="1e4e9-107">The `dotnet pack` command (see [dotnet Commands](dotnet-Commands.md)) and `msbuild /t:pack` (see [MSBuild targets](../reference/msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="1e4e9-108">V části Mono není podporováno vytváření balíčku ze souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="1e4e9-108">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="1e4e9-109">Také budete muset upravit jiné než místní cesty v `.nuspec` souborů na formátu UNIX cesty, jako jsou třeba nuget.exe nepřevádí názvy cest Windows sám sebe.</span><span class="sxs-lookup"><span data-stu-id="1e4e9-109">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="1e4e9-110">Použití</span><span class="sxs-lookup"><span data-stu-id="1e4e9-110">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options]
```

<span data-ttu-id="1e4e9-111">kde `<nuspecPath>` a `<projectPath>` zadejte `.nuspec` nebo projektu soubor, v uvedeném pořadí.</span><span class="sxs-lookup"><span data-stu-id="1e4e9-111">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="1e4e9-112">Možnosti</span><span class="sxs-lookup"><span data-stu-id="1e4e9-112">Options</span></span>

| <span data-ttu-id="1e4e9-113">Možnost</span><span class="sxs-lookup"><span data-stu-id="1e4e9-113">Option</span></span> | <span data-ttu-id="1e4e9-114">Popis</span><span class="sxs-lookup"><span data-stu-id="1e4e9-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1e4e9-115">BasePath</span><span class="sxs-lookup"><span data-stu-id="1e4e9-115">BasePath</span></span> | <span data-ttu-id="1e4e9-116">Nastaví základní cesta soubory definované v `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="1e4e9-116">Sets the base path of the files defined in the `.nuspec` file.</span></span> |
| <span data-ttu-id="1e4e9-117">Sestavení</span><span class="sxs-lookup"><span data-stu-id="1e4e9-117">Build</span></span> | <span data-ttu-id="1e4e9-118">Určuje, že projekt by měly být vytvořeny před vytvořením balíčku.</span><span class="sxs-lookup"><span data-stu-id="1e4e9-118">Specifies that the project should be built before building the package.</span></span> |
| <span data-ttu-id="1e4e9-119">Vyloučení</span><span class="sxs-lookup"><span data-stu-id="1e4e9-119">Exclude</span></span> | <span data-ttu-id="1e4e9-120">Určuje jeden nebo více vzory zástupných znaků, které chcete vyloučit při vytváření balíčku.</span><span class="sxs-lookup"><span data-stu-id="1e4e9-120">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="1e4e9-121">Chcete-li zadat více než jeden vzorek, opakujte příznak - vyloučení.</span><span class="sxs-lookup"><span data-stu-id="1e4e9-121">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="1e4e9-122">Viz následující příklad.</span><span class="sxs-lookup"><span data-stu-id="1e4e9-122">See example below.</span></span> |
| <span data-ttu-id="1e4e9-123">ExcludeEmptyDirectories</span><span class="sxs-lookup"><span data-stu-id="1e4e9-123">ExcludeEmptyDirectories</span></span> | <span data-ttu-id="1e4e9-124">Při vytváření balíčku, zabraňuje zahrnutí prázdných adresářů.</span><span class="sxs-lookup"><span data-stu-id="1e4e9-124">Prevents inclusion of empty directories when building the package.</span></span> |
| <span data-ttu-id="1e4e9-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="1e4e9-125">ForceEnglishOutput</span></span> | <span data-ttu-id="1e4e9-126">*(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze.</span><span class="sxs-lookup"><span data-stu-id="1e4e9-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="1e4e9-127">Nápověda</span><span class="sxs-lookup"><span data-stu-id="1e4e9-127">Help</span></span> | <span data-ttu-id="1e4e9-128">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="1e4e9-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="1e4e9-129">IncludeReferencedProjects</span><span class="sxs-lookup"><span data-stu-id="1e4e9-129">IncludeReferencedProjects</span></span> | <span data-ttu-id="1e4e9-130">Označuje, že balíček integrovaný by měla zahrnovat odkazované projekty jako závislosti nebo jako součást balíčku.</span><span class="sxs-lookup"><span data-stu-id="1e4e9-130">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="1e4e9-131">Pokud odkazované projekt má odpovídající `.nuspec` soubor, který má stejný název jako projekt, pak tento odkazovaný projektu se přidal jako závislost.</span><span class="sxs-lookup"><span data-stu-id="1e4e9-131">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="1e4e9-132">Odkazovaný projekt, jinak se přidá jako součást balíčku.</span><span class="sxs-lookup"><span data-stu-id="1e4e9-132">Otherwise, the referenced project is added as part of the package.</span></span> |
| <span data-ttu-id="1e4e9-133">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="1e4e9-133">MinClientVersion</span></span> | <span data-ttu-id="1e4e9-134">Nastavte *minClientVersion* atribut pro vytvoření balíčku.</span><span class="sxs-lookup"><span data-stu-id="1e4e9-134">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="1e4e9-135">Tato hodnota se přepíše stávající hodnotu *minClientVersion* atribut (pokud existuje) `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="1e4e9-135">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span> |
| <span data-ttu-id="1e4e9-136">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="1e4e9-136">MSBuildPath</span></span> | <span data-ttu-id="1e4e9-137">*(4.0 +)*  Určuje cestu MSBuild používat pomocí příkazu, přednost před `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="1e4e9-137">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="1e4e9-138">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="1e4e9-138">MSBuildVersion</span></span> | <span data-ttu-id="1e4e9-139">*(3.2 +)*  Určuje verzi nástroje MSBuild k použití se tento příkaz.</span><span class="sxs-lookup"><span data-stu-id="1e4e9-139">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="1e4e9-140">Podporované hodnoty jsou 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="1e4e9-140">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="1e4e9-141">Ve výchozím nastavení je zachyceny MSBuild ve své cestě jinak bude výchozí nejvyšší nainstalovanou verzi nástroje MSBuild.</span><span class="sxs-lookup"><span data-stu-id="1e4e9-141">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="1e4e9-142">NoDefaultExcludes</span><span class="sxs-lookup"><span data-stu-id="1e4e9-142">NoDefaultExcludes</span></span> | <span data-ttu-id="1e4e9-143">Zabraňuje výchozí vyloučení NuGet balíček soubory a soubory a složky začínající tečkou, jako například `.svn` a `.gitignore`.</span><span class="sxs-lookup"><span data-stu-id="1e4e9-143">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span> |
| <span data-ttu-id="1e4e9-144">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="1e4e9-144">NoPackageAnalysis</span></span> | <span data-ttu-id="1e4e9-145">Určuje, že sada by neměl spustit analysis balíčku po vytvoření balíčku.</span><span class="sxs-lookup"><span data-stu-id="1e4e9-145">Specifies that pack should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="1e4e9-146">Výstupnísložka</span><span class="sxs-lookup"><span data-stu-id="1e4e9-146">OutputDirectory</span></span> | <span data-ttu-id="1e4e9-147">Určuje složku, ve kterém je uložen balíček vytvořený.</span><span class="sxs-lookup"><span data-stu-id="1e4e9-147">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="1e4e9-148">Pokud není zadaný žádný složky, se používá aktuální složky.</span><span class="sxs-lookup"><span data-stu-id="1e4e9-148">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="1e4e9-149">Vlastnosti</span><span class="sxs-lookup"><span data-stu-id="1e4e9-149">Properties</span></span> | <span data-ttu-id="1e4e9-150">Určuje seznam vlastností, které potlačí hodnoty v souboru projektu; v tématu [běžné vlastnosti projektu nástroje MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) pro názvy vlastností.</span><span class="sxs-lookup"><span data-stu-id="1e4e9-150">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="1e4e9-151">Argument vlastnosti tady je seznam token = hodnota páry, oddělené středníky, kde každý výskyt `$token$` v `.nuspec` souboru se nahradí s danou hodnotou.</span><span class="sxs-lookup"><span data-stu-id="1e4e9-151">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="1e4e9-152">Hodnoty mohou být řetězce v uvozovkách.</span><span class="sxs-lookup"><span data-stu-id="1e4e9-152">Values can be strings in quotation marks.</span></span> <span data-ttu-id="1e4e9-153">Všimněte si, že pro vlastnost "Konfigurace" Výchozí hodnota je "Debug".</span><span class="sxs-lookup"><span data-stu-id="1e4e9-153">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="1e4e9-154">Můžete změnit konfiguraci verze `-Properties Configuration=Release`.</span><span class="sxs-lookup"><span data-stu-id="1e4e9-154">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> |
| <span data-ttu-id="1e4e9-155">Přípona</span><span class="sxs-lookup"><span data-stu-id="1e4e9-155">Suffix</span></span> | <span data-ttu-id="1e4e9-156">*(3.4.4+)*  Připojí příponu k číslo verze generované interně, obvykle se používá pro připojování sestavení nebo dalších identifikátorů předběžné verze.</span><span class="sxs-lookup"><span data-stu-id="1e4e9-156">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="1e4e9-157">Například pomocí `-suffix nightly` vytvoří balíček s jako číslo verze `1.2.3-nightly`.</span><span class="sxs-lookup"><span data-stu-id="1e4e9-157">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="1e4e9-158">Přípony musí začínat písmenem, aby se zabránilo upozornění, chyby a potenciální nekompatibilitu s různými verzemi nástroje NuGet a Správce balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="1e4e9-158">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span> |
| <span data-ttu-id="1e4e9-159">Symboly</span><span class="sxs-lookup"><span data-stu-id="1e4e9-159">Symbols</span></span> | <span data-ttu-id="1e4e9-160">Určuje, zda balíček obsahuje zdroje a symboly.</span><span class="sxs-lookup"><span data-stu-id="1e4e9-160">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="1e4e9-161">Při použití s `.nuspec` souboru, tím se vytvoří soubor regulární balíčku NuGet a odpovídající balíčku symbolů.</span><span class="sxs-lookup"><span data-stu-id="1e4e9-161">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> |
| <span data-ttu-id="1e4e9-162">Nástroj</span><span class="sxs-lookup"><span data-stu-id="1e4e9-162">Tool</span></span> | <span data-ttu-id="1e4e9-163">Určuje, že výstupních souborů projektu mají být umístěny v `tool` složky.</span><span class="sxs-lookup"><span data-stu-id="1e4e9-163">Specifies that the output files of the project should be placed in the `tool` folder.</span></span> |
| <span data-ttu-id="1e4e9-164">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="1e4e9-164">Verbosity</span></span> | <span data-ttu-id="1e4e9-165">Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="1e4e9-165">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="1e4e9-166">Version</span><span class="sxs-lookup"><span data-stu-id="1e4e9-166">Version</span></span> | <span data-ttu-id="1e4e9-167">Přepsání číslo verze z `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="1e4e9-167">Overrides the version number from the `.nuspec` file.</span></span> |

<span data-ttu-id="1e4e9-168">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="1e4e9-168">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="1e4e9-169">S výjimkou vývoj závislosti</span><span class="sxs-lookup"><span data-stu-id="1e4e9-169">Excluding development dependencies</span></span>

<span data-ttu-id="1e4e9-170">Některé balíčky NuGet jsou užitečné jako vývoj závislosti, které umožňují vytvářet vlastní knihovny, ale nejsou nezbytně potřebné jako závislosti skutečné balíčků.</span><span class="sxs-lookup"><span data-stu-id="1e4e9-170">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="1e4e9-171">`pack` Příkaz bude ignorovat `package` položek v `packages.config` mají `developmentDependency` atribut nastaven na `true`.</span><span class="sxs-lookup"><span data-stu-id="1e4e9-171">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="1e4e9-172">Tyto položky nebudou obsahovat jako závislosti v vytvořený balíčku.</span><span class="sxs-lookup"><span data-stu-id="1e4e9-172">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="1e4e9-173">Například vezměte v úvahu následující `packages.config` v projektu zdroje:</span><span class="sxs-lookup"><span data-stu-id="1e4e9-173">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="1e4e9-174">Pro tento projekt balíček vytvořený `nuget pack` bude mít závislost na `jQuery` a `microsoft-web-helpers` ale ne `netfx-Guard`.</span><span class="sxs-lookup"><span data-stu-id="1e4e9-174">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="examples"></a><span data-ttu-id="1e4e9-175">Příklady</span><span class="sxs-lookup"><span data-stu-id="1e4e9-175">Examples</span></span>

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5" -MSBuildVersion 12

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
