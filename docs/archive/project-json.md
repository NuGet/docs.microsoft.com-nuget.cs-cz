---
title: Referenční dokumentace souborů Project. JSON pro NuGet
description: V některých typech projektů udržuje Project. JSON seznam balíčků NuGet použitých v projektu.
author: karann-msft
ms.author: karann
ms.date: 07/27/2017
ms.topic: reference
ms.openlocfilehash: 5ecbcd4855de8ea7b6301a5e307779216baf96fc
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488285"
---
# <a name="projectjson-reference"></a><span data-ttu-id="cd6f4-103">Reference k Project. JSON</span><span class="sxs-lookup"><span data-stu-id="cd6f4-103">project.json reference</span></span>

<span data-ttu-id="cd6f4-104">*NuGet 3. x +*</span><span class="sxs-lookup"><span data-stu-id="cd6f4-104">*NuGet 3.x+*</span></span>

<span data-ttu-id="cd6f4-105">`project.json` Soubor uchovává seznam balíčků použitých v projektu, označovaných jako formát správy balíčků.</span><span class="sxs-lookup"><span data-stu-id="cd6f4-105">The `project.json` file maintains a list of packages used in a project, known as a package management format.</span></span> <span data-ttu-id="cd6f4-106">Nahrazuje `packages.config` , ale je zase nahrazen PackageReferenceem s NuGet [](../consume-packages/package-references-in-project-files.md) 4.0 +.</span><span class="sxs-lookup"><span data-stu-id="cd6f4-106">It supersedes `packages.config` but is in turn superseded by [PackageReference](../consume-packages/package-references-in-project-files.md) with NuGet 4.0+.</span></span>

<span data-ttu-id="cd6f4-107">Soubor [`project.lock.json`](#projectlockjson) (popsaný níže) se používá také v projektech `project.json`, které používají.</span><span class="sxs-lookup"><span data-stu-id="cd6f4-107">The [`project.lock.json`](#projectlockjson) file (described below) is also used in projects employing `project.json`.</span></span>

<span data-ttu-id="cd6f4-108">`project.json`má následující základní strukturu, kde každý ze čtyř objektů nejvyšší úrovně může mít libovolný počet podřízených objektů:</span><span class="sxs-lookup"><span data-stu-id="cd6f4-108">`project.json` has the following basic structure, where each of the four top-level objects can have any number of child objects:</span></span>

```json
{
    "dependencies": {
        "PackageID" : "{version_constraint}"
    },
    "frameworks" : {
        "TxM" : {}
    },
    "runtimes" : {
        "RID": {}
    },
    "supports" : {
        "CompatibilityProfile" : {}
    }
}
```

## <a name="dependencies"></a><span data-ttu-id="cd6f4-109">Závislosti</span><span class="sxs-lookup"><span data-stu-id="cd6f4-109">Dependencies</span></span>

<span data-ttu-id="cd6f4-110">Zobrazí seznam závislostí balíčku NuGet v projektu v následujícím tvaru:</span><span class="sxs-lookup"><span data-stu-id="cd6f4-110">Lists the NuGet package dependencies of your project in the following form:</span></span>

```json
"PackageID" : "version_constraint"
```

<span data-ttu-id="cd6f4-111">Příklad:</span><span class="sxs-lookup"><span data-stu-id="cd6f4-111">For example:</span></span>

```json
"dependencies": {
    "Microsoft.NETCore": "5.0.0",
    "System.Runtime.Serialization.Primitives": "4.0.10"
}
```

<span data-ttu-id="cd6f4-112">V `dependencies` tomto oddílu se v dialogovém okně Správce balíčků NuGet do projektu přidají závislosti balíčků.</span><span class="sxs-lookup"><span data-stu-id="cd6f4-112">The `dependencies` section is where the NuGet Package Manager dialog adds package dependencies to your project.</span></span>

<span data-ttu-id="cd6f4-113">ID balíčku odpovídá ID balíčku v nuget.org, stejné jako ID použité v konzole správce balíčků: `Install-Package Microsoft.NETCore`.</span><span class="sxs-lookup"><span data-stu-id="cd6f4-113">The Package id corresponds to the id of the package on nuget.org , the same as the id used in the package manager console: `Install-Package Microsoft.NETCore`.</span></span>

<span data-ttu-id="cd6f4-114">Při obnovování balíčků má omezení `"5.0.0"` verze implikuje. `>= 5.0.0`</span><span class="sxs-lookup"><span data-stu-id="cd6f4-114">When restoring packages, the version constraint of `"5.0.0"` implies `>= 5.0.0`.</span></span> <span data-ttu-id="cd6f4-115">To znamená, že pokud 5.0.0 není na serveru k dispozici, ale 5.0.1 je, NuGet nainstaluje 5.0.1 a upozorní vás na upgrade.</span><span class="sxs-lookup"><span data-stu-id="cd6f4-115">That is, if 5.0.0 is not available on the server but 5.0.1 is, NuGet installs  5.0.1 and warns you about the upgrade.</span></span> <span data-ttu-id="cd6f4-116">NuGet v opačném případě vybere nejnižší možnou verzi serveru, který odpovídá omezení.</span><span class="sxs-lookup"><span data-stu-id="cd6f4-116">NuGet otherwise picks the lowest possible version on the server matching the constraint.</span></span>

<span data-ttu-id="cd6f4-117">Další podrobnosti o pravidlech řešení najdete v tématu věnovaném [řešení závislostí](../concepts/dependency-resolution.md) .</span><span class="sxs-lookup"><span data-stu-id="cd6f4-117">See [Dependency resolution](../concepts/dependency-resolution.md) for more details on resolution rules.</span></span>

### <a name="managing-dependency-assets"></a><span data-ttu-id="cd6f4-118">Správa prostředků závislosti</span><span class="sxs-lookup"><span data-stu-id="cd6f4-118">Managing dependency assets</span></span>

<span data-ttu-id="cd6f4-119">Které prostředky ze závislostí toků do projektu nejvyšší úrovně jsou kontrolovány zadáním sady značek oddělených čárkami ve `include` vlastnostech a `exclude` odkazu na závislost.</span><span class="sxs-lookup"><span data-stu-id="cd6f4-119">Which assets from dependencies flow into the top-level project is controlled by specifying a comma-delimited set of tags in the `include` and `exclude` properties of the dependency reference.</span></span> <span data-ttu-id="cd6f4-120">Značky jsou uvedeny v následující tabulce:</span><span class="sxs-lookup"><span data-stu-id="cd6f4-120">The tags are listed the table below:</span></span>

| <span data-ttu-id="cd6f4-121">Značka include/Exclude</span><span class="sxs-lookup"><span data-stu-id="cd6f4-121">Include/Exclude tag</span></span> | <span data-ttu-id="cd6f4-122">Ovlivněné složky v cíli</span><span class="sxs-lookup"><span data-stu-id="cd6f4-122">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="cd6f4-123">contentFiles</span><span class="sxs-lookup"><span data-stu-id="cd6f4-123">contentFiles</span></span> | <span data-ttu-id="cd6f4-124">Obsah</span><span class="sxs-lookup"><span data-stu-id="cd6f4-124">Content</span></span>  |
| <span data-ttu-id="cd6f4-125">modul runtime</span><span class="sxs-lookup"><span data-stu-id="cd6f4-125">runtime</span></span> | <span data-ttu-id="cd6f4-126">Modul runtime, prostředky a FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="cd6f4-126">Runtime, Resources, and FrameworkAssemblies</span></span>  |
| <span data-ttu-id="cd6f4-127">sestavení</span><span class="sxs-lookup"><span data-stu-id="cd6f4-127">compile</span></span> | <span data-ttu-id="cd6f4-128">Knihovna</span><span class="sxs-lookup"><span data-stu-id="cd6f4-128">lib</span></span> |
| <span data-ttu-id="cd6f4-129">sestavení</span><span class="sxs-lookup"><span data-stu-id="cd6f4-129">build</span></span> | <span data-ttu-id="cd6f4-130">Build (MSBuild props and targets)</span><span class="sxs-lookup"><span data-stu-id="cd6f4-130">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="cd6f4-131">nativní</span><span class="sxs-lookup"><span data-stu-id="cd6f4-131">native</span></span> | <span data-ttu-id="cd6f4-132">nativní</span><span class="sxs-lookup"><span data-stu-id="cd6f4-132">native</span></span> |
| <span data-ttu-id="cd6f4-133">žádná</span><span class="sxs-lookup"><span data-stu-id="cd6f4-133">none</span></span> | <span data-ttu-id="cd6f4-134">Žádné složky</span><span class="sxs-lookup"><span data-stu-id="cd6f4-134">No folders</span></span> |
| <span data-ttu-id="cd6f4-135">všechny</span><span class="sxs-lookup"><span data-stu-id="cd6f4-135">all</span></span> | <span data-ttu-id="cd6f4-136">Všechny složky</span><span class="sxs-lookup"><span data-stu-id="cd6f4-136">All folders</span></span> |

<span data-ttu-id="cd6f4-137">Zadané značky s `exclude` prioritou mají přednost před hodnotami určenými pomocí. `include`</span><span class="sxs-lookup"><span data-stu-id="cd6f4-137">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="cd6f4-138">Například `include="runtime, compile" exclude="compile"` je stejný jako `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="cd6f4-138">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span>

<span data-ttu-id="cd6f4-139">Pokud například chcete zahrnout `build` složky a `native` pro závislost, použijte následující:</span><span class="sxs-lookup"><span data-stu-id="cd6f4-139">For example, to include the `build` and `native` folders of a dependency, use the following:</span></span>

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "include": "build, native"
    }
  }
}
```

<span data-ttu-id="cd6f4-140">Pokud chcete vyloučit `content` složky `build` a v závislosti, použijte následující:</span><span class="sxs-lookup"><span data-stu-id="cd6f4-140">To exclude the `content` and `build` folders of a dependency, use the following:</span></span>

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "exclude": "contentFiles, build"
    }
  }
}
```

## <a name="frameworks"></a><span data-ttu-id="cd6f4-141">Architektury</span><span class="sxs-lookup"><span data-stu-id="cd6f4-141">Frameworks</span></span>

<span data-ttu-id="cd6f4-142">Obsahuje seznam rozhraní, na kterých je projekt spuštěn, například `net45`, `netcoreapp`, `netstandard`.</span><span class="sxs-lookup"><span data-stu-id="cd6f4-142">Lists the frameworks that the project runs on, such as `net45`, `netcoreapp`, `netstandard`.</span></span>

```json
"frameworks": {
    "netcore50": {}
    }
 ```

<span data-ttu-id="cd6f4-143">V `frameworks` části je povolená jenom jedna položka.</span><span class="sxs-lookup"><span data-stu-id="cd6f4-143">Only a single entry is allowed in the `frameworks` section.</span></span> <span data-ttu-id="cd6f4-144">(Výjimkou jsou `project.json` soubory pro projekty ASP.NET, které jsou sestaveny pomocí zastaralého řetězce nástroje DNX, který umožňuje více cílů.)</span><span class="sxs-lookup"><span data-stu-id="cd6f4-144">(An exception is `project.json` files for ASP.NET projects that are build with deprecated DNX tool chain, which allows for multiple targets.)</span></span>

## <a name="runtimes"></a><span data-ttu-id="cd6f4-145">Moduly runtime</span><span class="sxs-lookup"><span data-stu-id="cd6f4-145">Runtimes</span></span>

<span data-ttu-id="cd6f4-146">Obsahuje seznam operačních systémů a architektur, na kterých běží vaše aplikace, `win10-arm` `win8-x64` `win8-x86`jako je například,.</span><span class="sxs-lookup"><span data-stu-id="cd6f4-146">Lists the operating systems and architectures that your app runs on, such as `win10-arm`, `win8-x64`, `win8-x86`.</span></span>

```json
"runtimes": {
    "win10-arm": { },
    "win10-arm-aot": { },
    "win10-x86": { },
    "win10-x86-aot": { },
    "win10-x64": { },
    "win10-x64-aot": { }
}
```

<span data-ttu-id="cd6f4-147">Balíček obsahující PCL, který může běžet v jakémkoli modulu runtime, nemusí určovat modul runtime.</span><span class="sxs-lookup"><span data-stu-id="cd6f4-147">A package containing a PCL that can run on any runtime doesn't need to specify a runtime.</span></span> <span data-ttu-id="cd6f4-148">Tato hodnota musí být také pravdivá pro jakékoli závislosti, jinak musíte zadat moduly runtime.</span><span class="sxs-lookup"><span data-stu-id="cd6f4-148">This must also be true of any dependencies, otherwise you must specify runtimes.</span></span>


## <a name="supports"></a><span data-ttu-id="cd6f4-149">Podporovaných</span><span class="sxs-lookup"><span data-stu-id="cd6f4-149">Supports</span></span>

<span data-ttu-id="cd6f4-150">Definuje sadu kontrol pro závislosti balíčku.</span><span class="sxs-lookup"><span data-stu-id="cd6f4-150">Defines a set of checks for package dependencies.</span></span> <span data-ttu-id="cd6f4-151">Můžete definovat, kde očekáváte, že se má jazyk PCL nebo aplikace spustit.</span><span class="sxs-lookup"><span data-stu-id="cd6f4-151">You can define where you expect the PCL or app to run.</span></span> <span data-ttu-id="cd6f4-152">Definice nejsou omezující, protože váš kód může být možné spustit jinde.</span><span class="sxs-lookup"><span data-stu-id="cd6f4-152">The definitions are not restrictive, as your code may be able to run elsewhere.</span></span> <span data-ttu-id="cd6f4-153">Ale zadáním těchto kontrol vrátí NuGet kontrolu nad tím, že všechny závislosti jsou splněné na uvedených TxMs.</span><span class="sxs-lookup"><span data-stu-id="cd6f4-153">But specifying these checks makes NuGet check that all dependencies are satisfied on the listed TxMs.</span></span> <span data-ttu-id="cd6f4-154">Příklady hodnot pro tyto hodnoty jsou: `net46.app`, `uwp.10.0.app`, atd.</span><span class="sxs-lookup"><span data-stu-id="cd6f4-154">Examples of the values for this are: `net46.app`, `uwp.10.0.app`, etc.</span></span>

<span data-ttu-id="cd6f4-155">Tato část by měla být naplněna automaticky při výběru položky v dialogovém okně cíle knihovny tříd.</span><span class="sxs-lookup"><span data-stu-id="cd6f4-155">This section should be populated automatically when you select an entry in the Portable Class Library targets dialog.</span></span>

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a><span data-ttu-id="cd6f4-156">Objem</span><span class="sxs-lookup"><span data-stu-id="cd6f4-156">Imports</span></span>

<span data-ttu-id="cd6f4-157">Importy jsou navržené tak, aby umožňovaly `dotnet` balíčkům, které používají TxM k práci s balíčky, které nedeklarují dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="cd6f4-157">Imports are designed to allow packages that use the `dotnet` TxM to operate with packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="cd6f4-158">`dotnet` Pokud váš projekt používá TxM, pak všechny balíčky, na kterých závisí, musí `dotnet` mít také TxM, pokud do své služby `project.json` nepřidáte následující, aby `dotnet` bylo možné nekompatibilní s `dotnet`platformou:</span><span class="sxs-lookup"><span data-stu-id="cd6f4-158">If your project is using the `dotnet` TxM then all the packages you depend on must also have a `dotnet` TxM, unless you add the following to your `project.json` to allow non `dotnet` platforms to be compatible with `dotnet`:</span></span>

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

<span data-ttu-id="cd6f4-159">Pokud používáte TxM, `dotnet` pak systém projektu PCL přidá příslušný `imports` příkaz na základě podporovaných cílů.</span><span class="sxs-lookup"><span data-stu-id="cd6f4-159">If you are using the `dotnet` TxM then the PCL project system adds the appropriate `imports` statement based on the supported targets.</span></span>

## <a name="differences-from-portable-apps-and-web-projects"></a><span data-ttu-id="cd6f4-160">Rozdíly mezi přenosnými aplikacemi a webovými projekty</span><span class="sxs-lookup"><span data-stu-id="cd6f4-160">Differences from portable apps and web projects</span></span>

<span data-ttu-id="cd6f4-161">`project.json` Soubor používaný NuGet je podmnožina nástroje, která se nachází v ASP.NET Corech projektech.</span><span class="sxs-lookup"><span data-stu-id="cd6f4-161">The `project.json` file used by NuGet is a subset of that found in ASP.NET Core projects.</span></span> <span data-ttu-id="cd6f4-162">V ASP.NET Core `project.json` se používá pro metadata projektu, informace o kompilaci a závislosti.</span><span class="sxs-lookup"><span data-stu-id="cd6f4-162">In ASP.NET Core `project.json` is used for project metadata, compilation information, and dependencies.</span></span> <span data-ttu-id="cd6f4-163">Při použití v jiných systémech projektů jsou tyto tři věci rozděleny do samostatných souborů a `project.json` obsahují méně informací.</span><span class="sxs-lookup"><span data-stu-id="cd6f4-163">When used in other project systems, those three things are split into separate files and `project.json` contains less information.</span></span> <span data-ttu-id="cd6f4-164">Mezi významné rozdíly patří:</span><span class="sxs-lookup"><span data-stu-id="cd6f4-164">Notable differences include:</span></span>

- <span data-ttu-id="cd6f4-165">V `frameworks` části může být pouze jedna architektura.</span><span class="sxs-lookup"><span data-stu-id="cd6f4-165">There can only be one framework in the `frameworks` section.</span></span>

- <span data-ttu-id="cd6f4-166">Soubor nemůže obsahovat závislosti, možnosti kompilace atd., které vidíte v souborech DNX `project.json` .</span><span class="sxs-lookup"><span data-stu-id="cd6f4-166">The file cannot contain dependencies, compilation options, etc. that you see in DNX `project.json` files.</span></span> <span data-ttu-id="cd6f4-167">Vzhledem k tomu, že může existovat pouze jeden rámec, nemá smysl zadat závislosti specifické pro rozhraní.</span><span class="sxs-lookup"><span data-stu-id="cd6f4-167">Given that there can only be a single framework it doesn't make sense to enter framework-specific dependencies.</span></span>

- <span data-ttu-id="cd6f4-168">Kompilace je zpracována nástrojem MSBuild, takže možnosti kompilace, definice preprocesoru atd. jsou všechny součástí souboru projektu MSBuild a nikoli `project.json`.</span><span class="sxs-lookup"><span data-stu-id="cd6f4-168">Compilation is handled by MSBuild so compilation options, preprocessor defines, etc. are all part of the MSBuild project file and not `project.json`.</span></span>

<span data-ttu-id="cd6f4-169">V NuGet 3 + se vývojáři neočekávají ruční úpravou `project.json`, protože uživatelské rozhraní Správce balíčků v aplikaci Visual Studio pracuje s obsahem.</span><span class="sxs-lookup"><span data-stu-id="cd6f4-169">In NuGet 3+, developers are not expected to manually edit the `project.json`, as the Package Manager UI in Visual Studio manipulates the content.</span></span> <span data-ttu-id="cd6f4-170">V takovém případě můžete soubor upravovat, ale je nutné sestavit projekt, aby bylo možné spustit obnovení balíčku nebo vyvolat obnovení jiným způsobem.</span><span class="sxs-lookup"><span data-stu-id="cd6f4-170">That said, you can certainly edit the file, but you must build the project to start a package restore or invoke restore in another way.</span></span> <span data-ttu-id="cd6f4-171">Viz [obnovení balíčku](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="cd6f4-171">See [Package restore](../consume-packages/package-restore.md).</span></span>


## <a name="projectlockjson"></a><span data-ttu-id="cd6f4-172">project.lock.json</span><span class="sxs-lookup"><span data-stu-id="cd6f4-172">project.lock.json</span></span>

<span data-ttu-id="cd6f4-173">Soubor se vygeneruje v procesu obnovení balíčků NuGet v projektech, které používají `project.json`. `project.lock.json`</span><span class="sxs-lookup"><span data-stu-id="cd6f4-173">The `project.lock.json` file is generated in the process of restoring the NuGet packages in projects that use `project.json`.</span></span> <span data-ttu-id="cd6f4-174">Obsahuje snímek všech informací, které jsou generovány s tím, že NuGet projde graf balíčků a obsahuje verzi, obsah a závislosti všech balíčků v projektu.</span><span class="sxs-lookup"><span data-stu-id="cd6f4-174">It holds a snapshot of all the information that is generated as NuGet walks the graph of packages and includes the version, contents, and dependencies of all the packages in your project.</span></span> <span data-ttu-id="cd6f4-175">Systém sestavení používá tuto možnost k výběru balíčků z globálního umístění, které je relevantní při sestavování projektu, nikoli v závislosti na místní složce balíčků v samotném projektu.</span><span class="sxs-lookup"><span data-stu-id="cd6f4-175">The build system uses this to choose packages from a global location that are relevant when building the project instead of depending on a local packages folder in the project itself.</span></span> <span data-ttu-id="cd6f4-176">Výsledkem je rychlejší sestavování výkonu, protože je nutné číst pouze `project.lock.json` místo mnoha samostatných `.nuspec` souborů.</span><span class="sxs-lookup"><span data-stu-id="cd6f4-176">This results in faster build performance because it's necessary to read only `project.lock.json` instead of many separate `.nuspec` files.</span></span>

<span data-ttu-id="cd6f4-177">`project.lock.json`se automaticky generuje při obnovení balíčku, takže ho můžete vypustit ze správy zdrojového kódu, a to tak `.gitignore` , `.tfignore` že ho přidáte do souborů a (viz [balíčky a Správa zdrojového kódu](../consume-packages/packages-and-source-control.md).</span><span class="sxs-lookup"><span data-stu-id="cd6f4-177">`project.lock.json` is automatically generated on package restore, so it can be omitted from source control by adding it to `.gitignore` and `.tfignore` files (see [Packages and source control](../consume-packages/packages-and-source-control.md).</span></span> <span data-ttu-id="cd6f4-178">Pokud však zahrnete je do správy zdrojového kódu, zobrazí se v historii změn v průběhu času změny v závislostech.</span><span class="sxs-lookup"><span data-stu-id="cd6f4-178">However, if you include it in source control, the change history shows changes in dependencies resolved over time.</span></span>
