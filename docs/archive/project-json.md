---
title: Odkaz na soubor Project.JSON pro NuGet
description: V některých typů projektu project.json udržuje seznam balíčky NuGet použité v projektu.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 07/27/2017
ms.topic: reference
ms.openlocfilehash: e558bdb969d4c70f85a3c89a426f1c7b11525402
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817122"
---
# <a name="projectjson-reference"></a><span data-ttu-id="f5258-103">odkaz na Project.JSON</span><span class="sxs-lookup"><span data-stu-id="f5258-103">project.json reference</span></span>

<span data-ttu-id="f5258-104">*NuGet 3.x+*</span><span class="sxs-lookup"><span data-stu-id="f5258-104">*NuGet 3.x+*</span></span>

<span data-ttu-id="f5258-105">`project.json` Souboru udržuje seznam balíčků používat v projektu, označuje jako balíček správy formátu.</span><span class="sxs-lookup"><span data-stu-id="f5258-105">The `project.json` file maintains a list of packages used in a project, known as a package management format.</span></span> <span data-ttu-id="f5258-106">Nahrazuje `packages.config` ale zase nahrazena [PackageReference](../consume-packages/package-references-in-project-files.md) s NuGet 4.0 +.</span><span class="sxs-lookup"><span data-stu-id="f5258-106">It supersedes `packages.config` but is in turn superseded by [PackageReference](../consume-packages/package-references-in-project-files.md) with NuGet 4.0+.</span></span>

<span data-ttu-id="f5258-107">[ `project.lock.json` ](#projectlockjson) Souboru (popsaný níže) se také používá v projektech nasazení `project.json`.</span><span class="sxs-lookup"><span data-stu-id="f5258-107">The [`project.lock.json`](#projectlockjson) file (described below) is also used in projects employing `project.json`.</span></span>

<span data-ttu-id="f5258-108">`project.json` má následující základní strukturu, kde každý z čtyři nejvyšší úrovně objektů může mít libovolný počet podřízených objektů:</span><span class="sxs-lookup"><span data-stu-id="f5258-108">`project.json` has the following basic structure, where each of the four top-level objects can have any number of child objects:</span></span>

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

## <a name="dependencies"></a><span data-ttu-id="f5258-109">Závislosti</span><span class="sxs-lookup"><span data-stu-id="f5258-109">Dependencies</span></span>

<span data-ttu-id="f5258-110">Uvádí závislosti balíčků NuGet projektu v následující podobě:</span><span class="sxs-lookup"><span data-stu-id="f5258-110">Lists the NuGet package dependencies of your project in the following form:</span></span>

```json
"PackageID" : "version_constraint"
```

<span data-ttu-id="f5258-111">Příklad:</span><span class="sxs-lookup"><span data-stu-id="f5258-111">For example:</span></span>

```json
"dependencies": {
    "Microsoft.NETCore": "5.0.0",
    "System.Runtime.Serialization.Primitives": "4.0.10"
}
```

<span data-ttu-id="f5258-112">`dependencies` Část je, kde dialogové okno Správce balíčků NuGet přidá k projektu závislosti balíčků.</span><span class="sxs-lookup"><span data-stu-id="f5258-112">The `dependencies` section is where the NuGet Package Manager dialog adds package dependencies to your project.</span></span>

<span data-ttu-id="f5258-113">Id balíčku, který odpovídá id balíčku v nuget.org, stejná jako číslo id použité v konzole Správce balíčků: `Install-Package Microsoft.NETCore`.</span><span class="sxs-lookup"><span data-stu-id="f5258-113">The Package id corresponds to the id of the package on nuget.org , the same as the id used in the package manager console: `Install-Package Microsoft.NETCore`.</span></span>

<span data-ttu-id="f5258-114">Při obnovování balíčků, omezení verze `"5.0.0"` znamená `>= 5.0.0`.</span><span class="sxs-lookup"><span data-stu-id="f5258-114">When restoring packages, the version constraint of `"5.0.0"` implies `>= 5.0.0`.</span></span> <span data-ttu-id="f5258-115">To znamená pokud 5.0.0 není k dispozici na serveru, ale je – 5.0.1, nainstaluje – 5.0.1 NuGet a upozorňuje na upgrade.</span><span class="sxs-lookup"><span data-stu-id="f5258-115">That is, if 5.0.0 is not available on the server but 5.0.1 is, NuGet installs  5.0.1 and warns you about the upgrade.</span></span> <span data-ttu-id="f5258-116">Jinak NuGet vybere nejnižší možné verze na serveru odpovídající omezení.</span><span class="sxs-lookup"><span data-stu-id="f5258-116">NuGet otherwise picks the lowest possible version on the server matching the constraint.</span></span>

<span data-ttu-id="f5258-117">V tématu [řešení závislostí](../consume-packages/dependency-resolution.md) další podrobnosti o pravidel řešení.</span><span class="sxs-lookup"><span data-stu-id="f5258-117">See [Dependency resolution](../consume-packages/dependency-resolution.md) for more details on resolution rules.</span></span>

### <a name="managing-dependency-assets"></a><span data-ttu-id="f5258-118">Správa závislostí prostředky</span><span class="sxs-lookup"><span data-stu-id="f5258-118">Managing dependency assets</span></span>

<span data-ttu-id="f5258-119">Jaké prostředky z závislosti toku do nejvyšší úrovně projektu je řízena zadáním sadu značky v oddělených čárkou `include` a `exclude` vlastnosti závislý odkaz.</span><span class="sxs-lookup"><span data-stu-id="f5258-119">Which assets from dependencies flow into the top-level project is controlled by specifying a comma-delimited set of tags in the `include` and `exclude` properties of the dependency reference.</span></span> <span data-ttu-id="f5258-120">Zadané značky jsou uvedeny v následující tabulce:</span><span class="sxs-lookup"><span data-stu-id="f5258-120">The tags are listed the table below:</span></span>

| <span data-ttu-id="f5258-121">Zahrnutí a vyloučení značky</span><span class="sxs-lookup"><span data-stu-id="f5258-121">Include/Exclude tag</span></span> | <span data-ttu-id="f5258-122">Ovlivněné složky cíle</span><span class="sxs-lookup"><span data-stu-id="f5258-122">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="f5258-123">contentFiles</span><span class="sxs-lookup"><span data-stu-id="f5258-123">contentFiles</span></span> | <span data-ttu-id="f5258-124">Obsah</span><span class="sxs-lookup"><span data-stu-id="f5258-124">Content</span></span>  |
| <span data-ttu-id="f5258-125">modul runtime</span><span class="sxs-lookup"><span data-stu-id="f5258-125">runtime</span></span> | <span data-ttu-id="f5258-126">Modul runtime, prostředky a FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="f5258-126">Runtime, Resources, and FrameworkAssemblies</span></span>  |
| <span data-ttu-id="f5258-127">Kompilace</span><span class="sxs-lookup"><span data-stu-id="f5258-127">compile</span></span> | <span data-ttu-id="f5258-128">Lib</span><span class="sxs-lookup"><span data-stu-id="f5258-128">lib</span></span> |
| <span data-ttu-id="f5258-129">sestavení</span><span class="sxs-lookup"><span data-stu-id="f5258-129">build</span></span> | <span data-ttu-id="f5258-130">sestavení (MSBuild props a cíle)</span><span class="sxs-lookup"><span data-stu-id="f5258-130">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="f5258-131">nativní</span><span class="sxs-lookup"><span data-stu-id="f5258-131">native</span></span> | <span data-ttu-id="f5258-132">nativní</span><span class="sxs-lookup"><span data-stu-id="f5258-132">native</span></span> |
| <span data-ttu-id="f5258-133">žádná</span><span class="sxs-lookup"><span data-stu-id="f5258-133">none</span></span> | <span data-ttu-id="f5258-134">Žádné složky</span><span class="sxs-lookup"><span data-stu-id="f5258-134">No folders</span></span> |
| <span data-ttu-id="f5258-135">všechny</span><span class="sxs-lookup"><span data-stu-id="f5258-135">all</span></span> | <span data-ttu-id="f5258-136">Všechny složky</span><span class="sxs-lookup"><span data-stu-id="f5258-136">All folders</span></span> |

<span data-ttu-id="f5258-137">Značky s `exclude` mají přednost před uvedenými s `include`.</span><span class="sxs-lookup"><span data-stu-id="f5258-137">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="f5258-138">Například `include="runtime, compile" exclude="compile"` je stejný jako `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="f5258-138">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span>

<span data-ttu-id="f5258-139">Chcete-li například zahrnout `build` a `native` složky závislost, použijte následující:</span><span class="sxs-lookup"><span data-stu-id="f5258-139">For example, to include the `build` and `native` folders of a dependency, use the following:</span></span>

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

<span data-ttu-id="f5258-140">Vyloučit `content` a `build` složky závislost, použijte tento příkaz:</span><span class="sxs-lookup"><span data-stu-id="f5258-140">To exclude the `content` and `build` folders of a dependency, use the following:</span></span>

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

## <a name="frameworks"></a><span data-ttu-id="f5258-141">rozhraní</span><span class="sxs-lookup"><span data-stu-id="f5258-141">Frameworks</span></span>

<span data-ttu-id="f5258-142">Uvádí rozhraní, které spouští projektu, například `net45`, `netcoreapp`, `netstandard`.</span><span class="sxs-lookup"><span data-stu-id="f5258-142">Lists the frameworks that the project runs on, such as `net45`, `netcoreapp`, `netstandard`.</span></span>

```json
"frameworks": {
    "netcore50": {}
    }
 ```

<span data-ttu-id="f5258-143">V je povolen pouze jeden záznam `frameworks` oddílu.</span><span class="sxs-lookup"><span data-stu-id="f5258-143">Only a single entry is allowed in the `frameworks` section.</span></span> <span data-ttu-id="f5258-144">(Výjimkou je `project.json` soubory pro projekty ASP.NET, které jsou sestavení s nepoužívané DNX nástroj řetězec, který umožňuje více cílů.)</span><span class="sxs-lookup"><span data-stu-id="f5258-144">(An exception is `project.json` files for ASP.NET projects that are build with deprecated DNX tool chain, which allows for multiple targets.)</span></span>

## <a name="runtimes"></a><span data-ttu-id="f5258-145">Moduly runtime</span><span class="sxs-lookup"><span data-stu-id="f5258-145">Runtimes</span></span>

<span data-ttu-id="f5258-146">Obsahuje operační systémy a architektury, které běží vaše aplikace, jako například `win10-arm`, `win8-x64`, `win8-x86`.</span><span class="sxs-lookup"><span data-stu-id="f5258-146">Lists the operating systems and architectures that your app runs on, such as `win10-arm`, `win8-x64`, `win8-x86`.</span></span>

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

<span data-ttu-id="f5258-147">Balíček obsahující PCL, který můžete spustit na jakékoli runtime nebude muset zadat modulu runtime.</span><span class="sxs-lookup"><span data-stu-id="f5258-147">A package containing a PCL that can run on any runtime doesn't need to specify a runtime.</span></span> <span data-ttu-id="f5258-148">Toto musí být také platí všechny závislosti, v opačném případě je nutné zadat moduly runtime.</span><span class="sxs-lookup"><span data-stu-id="f5258-148">This must also be true of any dependencies, otherwise you must specify runtimes.</span></span>


## <a name="supports"></a><span data-ttu-id="f5258-149">Podporuje</span><span class="sxs-lookup"><span data-stu-id="f5258-149">Supports</span></span>

<span data-ttu-id="f5258-150">Definuje sadu kontroluje pro závislosti balíčků.</span><span class="sxs-lookup"><span data-stu-id="f5258-150">Defines a set of checks for package dependencies.</span></span> <span data-ttu-id="f5258-151">Můžete definovat, kdy očekáváte PCL nebo aplikace spustit.</span><span class="sxs-lookup"><span data-stu-id="f5258-151">You can define where you expect the PCL or app to run.</span></span> <span data-ttu-id="f5258-152">Definice nejsou omezující, jak váš kód pravděpodobně bude moci spustit jinde.</span><span class="sxs-lookup"><span data-stu-id="f5258-152">The definitions are not restrictive, as your code may be able to run elsewhere.</span></span> <span data-ttu-id="f5258-153">Ale zadání těchto kontrol provádí NuGet, zkontrolujte, že jsou splněny všechny závislosti na uvedené TxMs.</span><span class="sxs-lookup"><span data-stu-id="f5258-153">But specifying these checks makes NuGet check that all dependencies are satisfied on the listed TxMs.</span></span> <span data-ttu-id="f5258-154">Příklady hodnot pro tyto: `net46.app`, `uwp.10.0.app`atd.</span><span class="sxs-lookup"><span data-stu-id="f5258-154">Examples of the values for this are: `net46.app`, `uwp.10.0.app`, etc.</span></span>

<span data-ttu-id="f5258-155">V této části by měl naplněny automaticky, když vyberete položku v dialogovém okně knihovny přenosných tříd cíle.</span><span class="sxs-lookup"><span data-stu-id="f5258-155">This section should be populated automatically when you select an entry in the Portable Class Library targets dialog.</span></span>

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a><span data-ttu-id="f5258-156">Importy</span><span class="sxs-lookup"><span data-stu-id="f5258-156">Imports</span></span>

<span data-ttu-id="f5258-157">Importy jsou navržené tak, aby balíčky, které používají `dotnet` TxM pracovat s balíčky, které nejsou deklarovat dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="f5258-157">Imports are designed to allow packages that use the `dotnet` TxM to operate with packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="f5258-158">Pokud je váš projekt pomocí `dotnet` TxM pak všechny balíčky, které závisí na musí také mít `dotnet` TxM, pokud přidejte následující vaše `project.json` umožňující bez `dotnet` platformy, aby byl kompatibilní s `dotnet`:</span><span class="sxs-lookup"><span data-stu-id="f5258-158">If your project is using the `dotnet` TxM then all the packages you depend on must also have a `dotnet` TxM, unless you add the following to your `project.json` to allow non `dotnet` platforms to be compatible with `dotnet`:</span></span>

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

<span data-ttu-id="f5258-159">Pokud používáte `dotnet` TxM pak systém projektu PCL přidá odpovídající `imports` příkaz na základě podporované cílů.</span><span class="sxs-lookup"><span data-stu-id="f5258-159">If you are using the `dotnet` TxM then the PCL project system adds the appropriate `imports` statement based on the supported targets.</span></span>

## <a name="differences-from-portable-apps-and-web-projects"></a><span data-ttu-id="f5258-160">Rozdíl oproti přenosné aplikace a webové projekty</span><span class="sxs-lookup"><span data-stu-id="f5258-160">Differences from portable apps and web projects</span></span>

<span data-ttu-id="f5258-161">`project.json` Soubor používaný NuGet je podmnožinou který nalézt projektů ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="f5258-161">The `project.json` file used by NuGet is a subset of that found in ASP.NET Core projects.</span></span> <span data-ttu-id="f5258-162">V ASP.NET Core `project.json` se používá pro projekt metadata, kompilace informace a závislosti.</span><span class="sxs-lookup"><span data-stu-id="f5258-162">In ASP.NET Core `project.json` is used for project metadata, compilation information, and dependencies.</span></span> <span data-ttu-id="f5258-163">Pokud se použije v ostatních systémech projektu, jsou tyto tři věci rozdělit do samostatných souborů a `project.json` menší informacemi.</span><span class="sxs-lookup"><span data-stu-id="f5258-163">When used in other project systems, those three things are split into separate files and `project.json` contains less information.</span></span> <span data-ttu-id="f5258-164">Významné rozdíly patří:</span><span class="sxs-lookup"><span data-stu-id="f5258-164">Notable differences include:</span></span>

- <span data-ttu-id="f5258-165">Může existovat pouze jedna framework v `frameworks` oddílu.</span><span class="sxs-lookup"><span data-stu-id="f5258-165">There can only be one framework in the `frameworks` section.</span></span>

- <span data-ttu-id="f5258-166">Soubor nemůže obsahovat závislosti, možnosti kompilace, atd., které se zobrazí v DNX `project.json` soubory.</span><span class="sxs-lookup"><span data-stu-id="f5258-166">The file cannot contain dependencies, compilation options, etc. that you see in DNX `project.json` files.</span></span> <span data-ttu-id="f5258-167">Vzhledem k tomu, že může existovat jenom jeden framework nemá smysl zadat závislosti konkrétní rozhraní.</span><span class="sxs-lookup"><span data-stu-id="f5258-167">Given that there can only be a single framework it doesn't make sense to enter framework-specific dependencies.</span></span>

- <span data-ttu-id="f5258-168">Kompilace se zpracovává souborem MSBuild tak kompilace možnosti preprocesoru definuje atd., jsou všechny součástí soubor projektu nástroje MSBuild a není `project.json`.</span><span class="sxs-lookup"><span data-stu-id="f5258-168">Compilation is handled by MSBuild so compilation options, preprocessor defines, etc. are all part of the MSBuild project file and not `project.json`.</span></span>

<span data-ttu-id="f5258-169">V NuGet 3 + vývojáři neočekává se ručně upravit, pokud `project.json`, protože uživatelské rozhraní Správce balíčků v sadě Visual Studio zpracovává obsah.</span><span class="sxs-lookup"><span data-stu-id="f5258-169">In NuGet 3+, developers are not expected to manually edit the `project.json`, as the Package Manager UI in Visual Studio manipulates the content.</span></span> <span data-ttu-id="f5258-170">Ale nutné dodat, jistě můžete upravit soubor, ale musí sestavte projekt a spusťte obnovení balíčků nebo vyvolat obnovení jiným způsobem.</span><span class="sxs-lookup"><span data-stu-id="f5258-170">That said, you can certainly edit the file, but you must build the project to start a package restore or invoke restore in another way.</span></span> <span data-ttu-id="f5258-171">V tématu [obnovení balíčků](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="f5258-171">See [Package restore](../consume-packages/package-restore.md).</span></span>


## <a name="projectlockjson"></a><span data-ttu-id="f5258-172">project.lock.json</span><span class="sxs-lookup"><span data-stu-id="f5258-172">project.lock.json</span></span>

<span data-ttu-id="f5258-173">`project.lock.json` Soubor je generován právě probíhá obnovení balíčků NuGet v projektech, které používají `project.json`.</span><span class="sxs-lookup"><span data-stu-id="f5258-173">The `project.lock.json` file is generated in the process of restoring the NuGet packages in projects that use `project.json`.</span></span> <span data-ttu-id="f5258-174">Drží snímek všechny informace, které jsou generovány jako provede grafu balíčků NuGet a zahrnuje verze, obsah a závislých součástí pro všechny balíčky v projektu.</span><span class="sxs-lookup"><span data-stu-id="f5258-174">It holds a snapshot of all the information that is generated as NuGet walks the graph of packages and includes the version, contents, and dependencies of all the packages in your project.</span></span> <span data-ttu-id="f5258-175">Systém sestavení pomocí to balíčky z globální umístění, které jsou relevantní při sestavování projektu místo v závislosti na složku místní balíčky v projektu.</span><span class="sxs-lookup"><span data-stu-id="f5258-175">The build system uses this to choose packages from a global location that are relevant when building the project instead of depending on a local packages folder in the project itself.</span></span> <span data-ttu-id="f5258-176">Výsledkem je vyšší výkon sestavení vzhledem k tomu, že je potřeba jen pro čtení `project.lock.json` místo mnoho oddělení `.nuspec` soubory.</span><span class="sxs-lookup"><span data-stu-id="f5258-176">This results in faster build performance because it's necessary to read only `project.lock.json` instead of many separate `.nuspec` files.</span></span>

<span data-ttu-id="f5258-177">`project.lock.json` se automaticky vygeneroval na obnovení balíčků, tak ho lze vynechat od správy zdrojového kódu, přidejte je do `.gitignore` a `.tfignore` soubory (viz [balíčky a Správa zdrojového kódu](../consume-packages/packages-and-source-control.md).</span><span class="sxs-lookup"><span data-stu-id="f5258-177">`project.lock.json` is automatically generated on package restore, so it can be omitted from source control by adding it to `.gitignore` and `.tfignore` files (see [Packages and source control](../consume-packages/packages-and-source-control.md).</span></span> <span data-ttu-id="f5258-178">Ale pokud zahrnete ji do správy zdrojového kódu, historii změn zobrazuje změny v závislosti přeložit v čase.</span><span class="sxs-lookup"><span data-stu-id="f5258-178">However, if you include it in source control, the change history shows changes in dependencies resolved over time.</span></span>
