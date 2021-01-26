---
title: project.jsodkaz na soubor pro NuGet
description: V některých typech projektů project.jszachovává seznam balíčků NuGet použitých v projektu.
author: JonDouglas
ms.author: jodou
ms.date: 07/27/2017
ms.topic: reference
ms.openlocfilehash: 6665f4f3e688cb4a3989216c8c8f1a8655b61ed8
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775201"
---
# <a name="projectjson-reference"></a><span data-ttu-id="720c9-103">project.jsna referenci</span><span class="sxs-lookup"><span data-stu-id="720c9-103">project.json reference</span></span>

<span data-ttu-id="720c9-104">*NuGet 3. x +*</span><span class="sxs-lookup"><span data-stu-id="720c9-104">*NuGet 3.x+*</span></span>

<span data-ttu-id="720c9-105">`project.json`Soubor uchovává seznam balíčků použitých v projektu, označovaných jako formát správy balíčků.</span><span class="sxs-lookup"><span data-stu-id="720c9-105">The `project.json` file maintains a list of packages used in a project, known as a package management format.</span></span> <span data-ttu-id="720c9-106">Nahrazuje, `packages.config` ale je zase nahrazen [PackageReferenceem](../consume-packages/package-references-in-project-files.md) s NuGet 4.0 +.</span><span class="sxs-lookup"><span data-stu-id="720c9-106">It supersedes `packages.config` but is in turn superseded by [PackageReference](../consume-packages/package-references-in-project-files.md) with NuGet 4.0+.</span></span>

<span data-ttu-id="720c9-107">[`project.lock.json`](#projectlockjson)Soubor (popsaný níže) se používá také v projektech, které používají `project.json` .</span><span class="sxs-lookup"><span data-stu-id="720c9-107">The [`project.lock.json`](#projectlockjson) file (described below) is also used in projects employing `project.json`.</span></span>

<span data-ttu-id="720c9-108">`project.json` má následující základní strukturu, kde každý ze čtyř objektů nejvyšší úrovně může mít libovolný počet podřízených objektů:</span><span class="sxs-lookup"><span data-stu-id="720c9-108">`project.json` has the following basic structure, where each of the four top-level objects can have any number of child objects:</span></span>

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

## <a name="dependencies"></a><span data-ttu-id="720c9-109">Závislosti</span><span class="sxs-lookup"><span data-stu-id="720c9-109">Dependencies</span></span>

<span data-ttu-id="720c9-110">Zobrazí seznam závislostí balíčku NuGet v projektu v následujícím tvaru:</span><span class="sxs-lookup"><span data-stu-id="720c9-110">Lists the NuGet package dependencies of your project in the following form:</span></span>

```json
"PackageID" : "version_constraint"
```

<span data-ttu-id="720c9-111">Například:</span><span class="sxs-lookup"><span data-stu-id="720c9-111">For example:</span></span>

```json
"dependencies": {
    "Microsoft.NETCore": "5.0.0",
    "System.Runtime.Serialization.Primitives": "4.0.10"
}
```

<span data-ttu-id="720c9-112">V tomto `dependencies` oddílu se v dialogovém okně Správce balíčků NuGet do projektu přidají závislosti balíčků.</span><span class="sxs-lookup"><span data-stu-id="720c9-112">The `dependencies` section is where the NuGet Package Manager dialog adds package dependencies to your project.</span></span>

<span data-ttu-id="720c9-113">ID balíčku odpovídá ID balíčku v nuget.org, stejné jako ID použité v konzole správce balíčků: `Install-Package Microsoft.NETCore` .</span><span class="sxs-lookup"><span data-stu-id="720c9-113">The Package id corresponds to the id of the package on nuget.org , the same as the id used in the package manager console: `Install-Package Microsoft.NETCore`.</span></span>

<span data-ttu-id="720c9-114">Při obnovování balíčků má omezení verze `"5.0.0"` implikuje `>= 5.0.0` .</span><span class="sxs-lookup"><span data-stu-id="720c9-114">When restoring packages, the version constraint of `"5.0.0"` implies `>= 5.0.0`.</span></span> <span data-ttu-id="720c9-115">To znamená, že pokud 5.0.0 není na serveru k dispozici, ale 5.0.1 je, NuGet nainstaluje 5.0.1 a upozorní vás na upgrade.</span><span class="sxs-lookup"><span data-stu-id="720c9-115">That is, if 5.0.0 is not available on the server but 5.0.1 is, NuGet installs  5.0.1 and warns you about the upgrade.</span></span> <span data-ttu-id="720c9-116">NuGet v opačném případě vybere nejnižší možnou verzi serveru, který odpovídá omezení.</span><span class="sxs-lookup"><span data-stu-id="720c9-116">NuGet otherwise picks the lowest possible version on the server matching the constraint.</span></span>

<span data-ttu-id="720c9-117">Další podrobnosti o pravidlech řešení najdete v tématu věnovaném [řešení závislostí](../concepts/dependency-resolution.md) .</span><span class="sxs-lookup"><span data-stu-id="720c9-117">See [Dependency resolution](../concepts/dependency-resolution.md) for more details on resolution rules.</span></span>

### <a name="managing-dependency-assets"></a><span data-ttu-id="720c9-118">Správa prostředků závislosti</span><span class="sxs-lookup"><span data-stu-id="720c9-118">Managing dependency assets</span></span>

<span data-ttu-id="720c9-119">Které prostředky ze závislostí toků do projektu nejvyšší úrovně jsou kontrolovány zadáním sady značek oddělených čárkami ve `include` `exclude` vlastnostech a odkazu na závislost.</span><span class="sxs-lookup"><span data-stu-id="720c9-119">Which assets from dependencies flow into the top-level project is controlled by specifying a comma-delimited set of tags in the `include` and `exclude` properties of the dependency reference.</span></span> <span data-ttu-id="720c9-120">Značky jsou uvedeny v následující tabulce:</span><span class="sxs-lookup"><span data-stu-id="720c9-120">The tags are listed the table below:</span></span>

| <span data-ttu-id="720c9-121">Značka include/Exclude</span><span class="sxs-lookup"><span data-stu-id="720c9-121">Include/Exclude tag</span></span> | <span data-ttu-id="720c9-122">Ovlivněné složky v cíli</span><span class="sxs-lookup"><span data-stu-id="720c9-122">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="720c9-123">contentFiles</span><span class="sxs-lookup"><span data-stu-id="720c9-123">contentFiles</span></span> | <span data-ttu-id="720c9-124">Content</span><span class="sxs-lookup"><span data-stu-id="720c9-124">Content</span></span>  |
| <span data-ttu-id="720c9-125">modul runtime</span><span class="sxs-lookup"><span data-stu-id="720c9-125">runtime</span></span> | <span data-ttu-id="720c9-126">Modul runtime, prostředky a FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="720c9-126">Runtime, Resources, and FrameworkAssemblies</span></span>  |
| <span data-ttu-id="720c9-127">kompilovat</span><span class="sxs-lookup"><span data-stu-id="720c9-127">compile</span></span> | <span data-ttu-id="720c9-128">Knihovna</span><span class="sxs-lookup"><span data-stu-id="720c9-128">lib</span></span> |
| <span data-ttu-id="720c9-129">sestavení</span><span class="sxs-lookup"><span data-stu-id="720c9-129">build</span></span> | <span data-ttu-id="720c9-130">Build (MSBuild props and targets)</span><span class="sxs-lookup"><span data-stu-id="720c9-130">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="720c9-131">nativní</span><span class="sxs-lookup"><span data-stu-id="720c9-131">native</span></span> | <span data-ttu-id="720c9-132">nativní</span><span class="sxs-lookup"><span data-stu-id="720c9-132">native</span></span> |
| <span data-ttu-id="720c9-133">žádné</span><span class="sxs-lookup"><span data-stu-id="720c9-133">none</span></span> | <span data-ttu-id="720c9-134">Žádné složky</span><span class="sxs-lookup"><span data-stu-id="720c9-134">No folders</span></span> |
| <span data-ttu-id="720c9-135">Vše</span><span class="sxs-lookup"><span data-stu-id="720c9-135">all</span></span> | <span data-ttu-id="720c9-136">Všechny složky</span><span class="sxs-lookup"><span data-stu-id="720c9-136">All folders</span></span> |

<span data-ttu-id="720c9-137">Zadané značky s `exclude` prioritou mají přednost před hodnotami určenými pomocí `include` .</span><span class="sxs-lookup"><span data-stu-id="720c9-137">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="720c9-138">Například `include="runtime, compile" exclude="compile"` je stejný jako `include="runtime"` .</span><span class="sxs-lookup"><span data-stu-id="720c9-138">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span>

<span data-ttu-id="720c9-139">Pokud například chcete zahrnout `build` složky a pro `native` závislost, použijte následující:</span><span class="sxs-lookup"><span data-stu-id="720c9-139">For example, to include the `build` and `native` folders of a dependency, use the following:</span></span>

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

<span data-ttu-id="720c9-140">Pokud chcete vyloučit `content` složky a v `build` závislosti, použijte následující:</span><span class="sxs-lookup"><span data-stu-id="720c9-140">To exclude the `content` and `build` folders of a dependency, use the following:</span></span>

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

## <a name="frameworks"></a><span data-ttu-id="720c9-141">Rozhraní</span><span class="sxs-lookup"><span data-stu-id="720c9-141">Frameworks</span></span>

<span data-ttu-id="720c9-142">Obsahuje seznam rozhraní, na kterých je projekt spuštěn, například `net45` , `netcoreapp` , `netstandard` .</span><span class="sxs-lookup"><span data-stu-id="720c9-142">Lists the frameworks that the project runs on, such as `net45`, `netcoreapp`, `netstandard`.</span></span>

```json
"frameworks": {
    "netcore50": {}
    }
 ```

<span data-ttu-id="720c9-143">V části je povolená jenom jedna položka `frameworks` .</span><span class="sxs-lookup"><span data-stu-id="720c9-143">Only a single entry is allowed in the `frameworks` section.</span></span> <span data-ttu-id="720c9-144">(Výjimkou jsou `project.json` soubory pro projekty ASP.NET, které jsou sestaveny pomocí zastaralého řetězce nástroje DNX, který umožňuje více cílů.)</span><span class="sxs-lookup"><span data-stu-id="720c9-144">(An exception is `project.json` files for ASP.NET projects that are build with deprecated DNX tool chain, which allows for multiple targets.)</span></span>

## <a name="runtimes"></a><span data-ttu-id="720c9-145">Moduly runtime</span><span class="sxs-lookup"><span data-stu-id="720c9-145">Runtimes</span></span>

<span data-ttu-id="720c9-146">Obsahuje seznam operačních systémů a architektur, na kterých běží vaše aplikace, jako je například, `win10-arm` `win8-x64` `win8-x86` .</span><span class="sxs-lookup"><span data-stu-id="720c9-146">Lists the operating systems and architectures that your app runs on, such as `win10-arm`, `win8-x64`, `win8-x86`.</span></span>

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

<span data-ttu-id="720c9-147">Balíček obsahující PCL, který může běžet v jakémkoli modulu runtime, nemusí určovat modul runtime.</span><span class="sxs-lookup"><span data-stu-id="720c9-147">A package containing a PCL that can run on any runtime doesn't need to specify a runtime.</span></span> <span data-ttu-id="720c9-148">Tato hodnota musí být také pravdivá pro jakékoli závislosti, jinak musíte zadat moduly runtime.</span><span class="sxs-lookup"><span data-stu-id="720c9-148">This must also be true of any dependencies, otherwise you must specify runtimes.</span></span>


## <a name="supports"></a><span data-ttu-id="720c9-149">Podporuje</span><span class="sxs-lookup"><span data-stu-id="720c9-149">Supports</span></span>

<span data-ttu-id="720c9-150">Definuje sadu kontrol pro závislosti balíčku.</span><span class="sxs-lookup"><span data-stu-id="720c9-150">Defines a set of checks for package dependencies.</span></span> <span data-ttu-id="720c9-151">Můžete definovat, kde očekáváte, že se má jazyk PCL nebo aplikace spustit.</span><span class="sxs-lookup"><span data-stu-id="720c9-151">You can define where you expect the PCL or app to run.</span></span> <span data-ttu-id="720c9-152">Definice nejsou omezující, protože váš kód může být možné spustit jinde.</span><span class="sxs-lookup"><span data-stu-id="720c9-152">The definitions are not restrictive, as your code may be able to run elsewhere.</span></span> <span data-ttu-id="720c9-153">Ale zadáním těchto kontrol vrátí NuGet kontrolu nad tím, že všechny závislosti jsou splněné na uvedených TxMs.</span><span class="sxs-lookup"><span data-stu-id="720c9-153">But specifying these checks makes NuGet check that all dependencies are satisfied on the listed TxMs.</span></span> <span data-ttu-id="720c9-154">Příklady hodnot pro tyto hodnoty jsou: `net46.app` , `uwp.10.0.app` , atd.</span><span class="sxs-lookup"><span data-stu-id="720c9-154">Examples of the values for this are: `net46.app`, `uwp.10.0.app`, etc.</span></span>

<span data-ttu-id="720c9-155">Tato část by měla být naplněna automaticky při výběru položky v dialogovém okně cíle knihovny tříd.</span><span class="sxs-lookup"><span data-stu-id="720c9-155">This section should be populated automatically when you select an entry in the Portable Class Library targets dialog.</span></span>

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a><span data-ttu-id="720c9-156">Objem</span><span class="sxs-lookup"><span data-stu-id="720c9-156">Imports</span></span>

<span data-ttu-id="720c9-157">Importy jsou navržené tak, aby umožňovaly balíčkům, které používají `dotnet` TxM k práci s balíčky, které nedeklarují dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="720c9-157">Imports are designed to allow packages that use the `dotnet` TxM to operate with packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="720c9-158">Pokud váš projekt používá `dotnet` TxM, pak všechny balíčky, na kterých závisí, musí mít také `dotnet` TxM, pokud do své služby nepřidáte následující, aby bylo možné `project.json` `dotnet` nekompatibilní s platformou `dotnet` :</span><span class="sxs-lookup"><span data-stu-id="720c9-158">If your project is using the `dotnet` TxM then all the packages you depend on must also have a `dotnet` TxM, unless you add the following to your `project.json` to allow non `dotnet` platforms to be compatible with `dotnet`:</span></span>

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

<span data-ttu-id="720c9-159">Pokud používáte `dotnet` TxM, pak systém projektu PCL přidá příslušný `imports` příkaz na základě podporovaných cílů.</span><span class="sxs-lookup"><span data-stu-id="720c9-159">If you are using the `dotnet` TxM then the PCL project system adds the appropriate `imports` statement based on the supported targets.</span></span>

## <a name="differences-from-portable-apps-and-web-projects"></a><span data-ttu-id="720c9-160">Rozdíly mezi přenosnými aplikacemi a webovými projekty</span><span class="sxs-lookup"><span data-stu-id="720c9-160">Differences from portable apps and web projects</span></span>

<span data-ttu-id="720c9-161">`project.json`Soubor používaný NuGet je podmnožina nástroje, která se nachází v ASP.NET Corech projektech.</span><span class="sxs-lookup"><span data-stu-id="720c9-161">The `project.json` file used by NuGet is a subset of that found in ASP.NET Core projects.</span></span> <span data-ttu-id="720c9-162">V ASP.NET Core `project.json` se používá pro metadata projektu, informace o kompilaci a závislosti.</span><span class="sxs-lookup"><span data-stu-id="720c9-162">In ASP.NET Core `project.json` is used for project metadata, compilation information, and dependencies.</span></span> <span data-ttu-id="720c9-163">Při použití v jiných systémech projektů jsou tyto tři věci rozděleny do samostatných souborů a `project.json` obsahují méně informací.</span><span class="sxs-lookup"><span data-stu-id="720c9-163">When used in other project systems, those three things are split into separate files and `project.json` contains less information.</span></span> <span data-ttu-id="720c9-164">Mezi významné rozdíly patří:</span><span class="sxs-lookup"><span data-stu-id="720c9-164">Notable differences include:</span></span>

- <span data-ttu-id="720c9-165">V části může být pouze jedna architektura `frameworks` .</span><span class="sxs-lookup"><span data-stu-id="720c9-165">There can only be one framework in the `frameworks` section.</span></span>

- <span data-ttu-id="720c9-166">Soubor nemůže obsahovat závislosti, možnosti kompilace atd., které vidíte v `project.json` souborech DNX.</span><span class="sxs-lookup"><span data-stu-id="720c9-166">The file cannot contain dependencies, compilation options, etc. that you see in DNX `project.json` files.</span></span> <span data-ttu-id="720c9-167">Vzhledem k tomu, že může existovat pouze jeden rámec, nemá smysl zadat závislosti specifické pro rozhraní.</span><span class="sxs-lookup"><span data-stu-id="720c9-167">Given that there can only be a single framework it doesn't make sense to enter framework-specific dependencies.</span></span>

- <span data-ttu-id="720c9-168">Kompilace je zpracována nástrojem MSBuild, takže možnosti kompilace, definice preprocesoru atd. jsou všechny součástí souboru projektu MSBuild a nikoli `project.json` .</span><span class="sxs-lookup"><span data-stu-id="720c9-168">Compilation is handled by MSBuild so compilation options, preprocessor defines, etc. are all part of the MSBuild project file and not `project.json`.</span></span>

<span data-ttu-id="720c9-169">V NuGet 3 + se vývojáři neočekávají ruční úpravou `project.json` , protože uživatelské rozhraní Správce balíčků v aplikaci Visual Studio pracuje s obsahem.</span><span class="sxs-lookup"><span data-stu-id="720c9-169">In NuGet 3+, developers are not expected to manually edit the `project.json`, as the Package Manager UI in Visual Studio manipulates the content.</span></span> <span data-ttu-id="720c9-170">V takovém případě můžete soubor upravovat, ale je nutné sestavit projekt, aby bylo možné spustit obnovení balíčku nebo vyvolat obnovení jiným způsobem.</span><span class="sxs-lookup"><span data-stu-id="720c9-170">That said, you can certainly edit the file, but you must build the project to start a package restore or invoke restore in another way.</span></span> <span data-ttu-id="720c9-171">Viz [obnovení balíčku](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="720c9-171">See [Package restore](../consume-packages/package-restore.md).</span></span>


## <a name="projectlockjson"></a><span data-ttu-id="720c9-172">project.lock.jsna</span><span class="sxs-lookup"><span data-stu-id="720c9-172">project.lock.json</span></span>

<span data-ttu-id="720c9-173">`project.lock.json`Soubor se vygeneruje v procesu obnovení balíčků NuGet v projektech, které používají `project.json` .</span><span class="sxs-lookup"><span data-stu-id="720c9-173">The `project.lock.json` file is generated in the process of restoring the NuGet packages in projects that use `project.json`.</span></span> <span data-ttu-id="720c9-174">Obsahuje snímek všech informací, které jsou generovány s tím, že NuGet projde graf balíčků a obsahuje verzi, obsah a závislosti všech balíčků v projektu.</span><span class="sxs-lookup"><span data-stu-id="720c9-174">It holds a snapshot of all the information that is generated as NuGet walks the graph of packages and includes the version, contents, and dependencies of all the packages in your project.</span></span> <span data-ttu-id="720c9-175">Systém sestavení používá tuto možnost k výběru balíčků z globálního umístění, které je relevantní při sestavování projektu, nikoli v závislosti na místní složce balíčků v samotném projektu.</span><span class="sxs-lookup"><span data-stu-id="720c9-175">The build system uses this to choose packages from a global location that are relevant when building the project instead of depending on a local packages folder in the project itself.</span></span> <span data-ttu-id="720c9-176">Výsledkem je rychlejší sestavování výkonu, protože je nutné číst pouze `project.lock.json` místo mnoha samostatných `.nuspec` souborů.</span><span class="sxs-lookup"><span data-stu-id="720c9-176">This results in faster build performance because it's necessary to read only `project.lock.json` instead of many separate `.nuspec` files.</span></span>

<span data-ttu-id="720c9-177">`project.lock.json` se automaticky generuje při obnovení balíčku, takže ho můžete vypustit ze správy zdrojového kódu, a to tak, že ho přidáte do `.gitignore` `.tfignore` souborů a (viz [balíčky a Správa zdrojového kódu](../consume-packages/packages-and-source-control.md).</span><span class="sxs-lookup"><span data-stu-id="720c9-177">`project.lock.json` is automatically generated on package restore, so it can be omitted from source control by adding it to `.gitignore` and `.tfignore` files (see [Packages and source control](../consume-packages/packages-and-source-control.md).</span></span> <span data-ttu-id="720c9-178">Pokud však zahrnete je do správy zdrojového kódu, zobrazí se v historii změn v průběhu času změny v závislostech.</span><span class="sxs-lookup"><span data-stu-id="720c9-178">However, if you include it in source control, the change history shows changes in dependencies resolved over time.</span></span>
