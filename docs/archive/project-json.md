---
title: Odkaz na soubor Project.JSON pro NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 07/27/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "V některých typů projektu project.json udržuje seznam balíčky NuGet použité v projektu."
keywords: "Balíček NuGet NuGet project.json, odkazy, závislostí NuGet, project.lock.json"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2e2c521b18dd67e49942cc20eafef0be7f91573a
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
---
# <a name="projectjson-reference"></a><span data-ttu-id="a9f17-104">odkaz na Project.JSON</span><span class="sxs-lookup"><span data-stu-id="a9f17-104">project.json reference</span></span>

<span data-ttu-id="a9f17-105">*NuGet 3.x+*</span><span class="sxs-lookup"><span data-stu-id="a9f17-105">*NuGet 3.x+*</span></span>

<span data-ttu-id="a9f17-106">`project.json` Souboru udržuje seznam balíčků používat v projektu, označuje jako formátu odkaz na balíček.</span><span class="sxs-lookup"><span data-stu-id="a9f17-106">The `project.json` file maintains a list of packages used in a project, known as a package reference format.</span></span> <span data-ttu-id="a9f17-107">Nahrazuje `packages.config` ale zase nahrazena [PackageReference](../consume-packages/package-references-in-project-files.md) s NuGet 4.0 +.</span><span class="sxs-lookup"><span data-stu-id="a9f17-107">It supersedes `packages.config` but is in turn superseded by [PackageReference](../consume-packages/package-references-in-project-files.md) with NuGet 4.0+.</span></span>

<span data-ttu-id="a9f17-108">[ `project.lock.json` ](#projectlockjson) Souboru (popsaný níže) se také používá v projektech nasazení `project.json`.</span><span class="sxs-lookup"><span data-stu-id="a9f17-108">The [`project.lock.json`](#projectlockjson) file (described below) is also used in projects employing `project.json`.</span></span>

<span data-ttu-id="a9f17-109">`project.json`má následující základní strukturu, kde každý z čtyři nejvyšší úrovně objektů může mít libovolný počet podřízených objektů:</span><span class="sxs-lookup"><span data-stu-id="a9f17-109">`project.json` has the following basic structure, where each of the four top-level objects can have any number of child objects:</span></span>

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

## <a name="dependencies"></a><span data-ttu-id="a9f17-110">Závislosti</span><span class="sxs-lookup"><span data-stu-id="a9f17-110">Dependencies</span></span>

<span data-ttu-id="a9f17-111">Uvádí závislosti balíčků NuGet projektu v následující podobě:</span><span class="sxs-lookup"><span data-stu-id="a9f17-111">Lists the NuGet package dependencies of your project in the following form:</span></span>

```json
"PackageID" : "version_constraint"
```

<span data-ttu-id="a9f17-112">Příklad:</span><span class="sxs-lookup"><span data-stu-id="a9f17-112">For example:</span></span>

```json
"dependencies": {
    "Microsoft.NETCore": "5.0.0",
    "System.Runtime.Serialization.Primitives": "4.0.10"
}
```

<span data-ttu-id="a9f17-113">`dependencies` Část je, kde dialogové okno Správce balíčků NuGet přidá k projektu závislosti balíčků.</span><span class="sxs-lookup"><span data-stu-id="a9f17-113">The `dependencies` section is where the NuGet Package Manager dialog adds package dependencies to your project.</span></span>

<span data-ttu-id="a9f17-114">Id balíčku, který odpovídá id balíčku v nuget.org, stejná jako číslo id použité v konzole Správce balíčků: `Install-Package Microsoft.NETCore`.</span><span class="sxs-lookup"><span data-stu-id="a9f17-114">The Package id corresponds to the id of the package on nuget.org , the same as the id used in the package manager console: `Install-Package Microsoft.NETCore`.</span></span>

<span data-ttu-id="a9f17-115">Při obnovování balíčků, omezení verze `"5.0.0"` znamená `>= 5.0.0`.</span><span class="sxs-lookup"><span data-stu-id="a9f17-115">When restoring packages, the version constraint of `"5.0.0"` implies `>= 5.0.0`.</span></span> <span data-ttu-id="a9f17-116">To znamená pokud 5.0.0 není k dispozici na serveru, ale je – 5.0.1, nainstaluje – 5.0.1 NuGet a upozorňuje na upgrade.</span><span class="sxs-lookup"><span data-stu-id="a9f17-116">That is, if 5.0.0 is not available on the server but 5.0.1 is, NuGet installs  5.0.1 and warns you about the upgrade.</span></span> <span data-ttu-id="a9f17-117">Jinak NuGet vybere nejnižší možné verze na serveru odpovídající omezení.</span><span class="sxs-lookup"><span data-stu-id="a9f17-117">NuGet otherwise picks the lowest possible version on the server matching the constraint.</span></span>

<span data-ttu-id="a9f17-118">V tématu [řešení závislostí](../consume-packages/dependency-resolution.md) další podrobnosti o pravidel řešení.</span><span class="sxs-lookup"><span data-stu-id="a9f17-118">See [Dependency resolution](../consume-packages/dependency-resolution.md) for more details on resolution rules.</span></span>

### <a name="managing-dependency-assets"></a><span data-ttu-id="a9f17-119">Správa závislostí prostředky</span><span class="sxs-lookup"><span data-stu-id="a9f17-119">Managing dependency assets</span></span>

<span data-ttu-id="a9f17-120">Jaké prostředky z závislosti toku do nejvyšší úrovně projektu je řízena zadáním sadu značky v oddělených čárkou `include` a `exclude` vlastnosti závislý odkaz.</span><span class="sxs-lookup"><span data-stu-id="a9f17-120">Which assets from dependencies flow into the top-level project is controlled by specifying a comma-delimited set of tags in the `include` and `exclude` properties of the dependency reference.</span></span> <span data-ttu-id="a9f17-121">Zadané značky jsou uvedeny v následující tabulce:</span><span class="sxs-lookup"><span data-stu-id="a9f17-121">The tags are listed the table below:</span></span>

| <span data-ttu-id="a9f17-122">Zahrnutí a vyloučení značky</span><span class="sxs-lookup"><span data-stu-id="a9f17-122">Include/Exclude tag</span></span> | <span data-ttu-id="a9f17-123">Ovlivněné složky cíle</span><span class="sxs-lookup"><span data-stu-id="a9f17-123">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="a9f17-124">contentFiles</span><span class="sxs-lookup"><span data-stu-id="a9f17-124">contentFiles</span></span> | <span data-ttu-id="a9f17-125">Obsah</span><span class="sxs-lookup"><span data-stu-id="a9f17-125">Content</span></span>  |
| <span data-ttu-id="a9f17-126">modul runtime</span><span class="sxs-lookup"><span data-stu-id="a9f17-126">runtime</span></span> | <span data-ttu-id="a9f17-127">Modul runtime, prostředky a FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="a9f17-127">Runtime, Resources, and FrameworkAssemblies</span></span>  |
| <span data-ttu-id="a9f17-128">compile</span><span class="sxs-lookup"><span data-stu-id="a9f17-128">compile</span></span> | <span data-ttu-id="a9f17-129">lib</span><span class="sxs-lookup"><span data-stu-id="a9f17-129">lib</span></span> |
| <span data-ttu-id="a9f17-130">sestavení</span><span class="sxs-lookup"><span data-stu-id="a9f17-130">build</span></span> | <span data-ttu-id="a9f17-131">sestavení (MSBuild props a cíle)</span><span class="sxs-lookup"><span data-stu-id="a9f17-131">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="a9f17-132">nativní</span><span class="sxs-lookup"><span data-stu-id="a9f17-132">native</span></span> | <span data-ttu-id="a9f17-133">nativní</span><span class="sxs-lookup"><span data-stu-id="a9f17-133">native</span></span> |
| <span data-ttu-id="a9f17-134">žádná</span><span class="sxs-lookup"><span data-stu-id="a9f17-134">none</span></span> | <span data-ttu-id="a9f17-135">Žádné složky</span><span class="sxs-lookup"><span data-stu-id="a9f17-135">No folders</span></span> |
| <span data-ttu-id="a9f17-136">všechny</span><span class="sxs-lookup"><span data-stu-id="a9f17-136">all</span></span> | <span data-ttu-id="a9f17-137">Všechny složky</span><span class="sxs-lookup"><span data-stu-id="a9f17-137">All folders</span></span> |

<span data-ttu-id="a9f17-138">Značky s `exclude` mají přednost před uvedenými s `include`.</span><span class="sxs-lookup"><span data-stu-id="a9f17-138">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="a9f17-139">Například `include="runtime, compile" exclude="compile"` je stejný jako `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="a9f17-139">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span>

<span data-ttu-id="a9f17-140">Chcete-li například zahrnout `build` a `native` složky závislost, použijte následující:</span><span class="sxs-lookup"><span data-stu-id="a9f17-140">For example, to include the `build` and `native` folders of a dependency, use the following:</span></span>

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

<span data-ttu-id="a9f17-141">Vyloučit `content` a `build` složky závislost, použijte tento příkaz:</span><span class="sxs-lookup"><span data-stu-id="a9f17-141">To exclude the `content` and `build` folders of a dependency, use the following:</span></span>

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

## <a name="frameworks"></a><span data-ttu-id="a9f17-142">rozhraní</span><span class="sxs-lookup"><span data-stu-id="a9f17-142">Frameworks</span></span>

<span data-ttu-id="a9f17-143">Uvádí rozhraní, které spouští projektu, například `net45`, `netcoreapp`, `netstandard`.</span><span class="sxs-lookup"><span data-stu-id="a9f17-143">Lists the frameworks that the project runs on, such as `net45`, `netcoreapp`, `netstandard`.</span></span>

```json
"frameworks": {
    "netcore50": {}
    }
 ```

<span data-ttu-id="a9f17-144">V je povolen pouze jeden záznam `frameworks` oddílu.</span><span class="sxs-lookup"><span data-stu-id="a9f17-144">Only a single entry is allowed in the `frameworks` section.</span></span> <span data-ttu-id="a9f17-145">(Výjimkou je `project.json` soubory pro projekty ASP.NET, které jsou sestavení s nepoužívané sada DNX, který umožňuje více cílů.)</span><span class="sxs-lookup"><span data-stu-id="a9f17-145">(An exception is `project.json` files for ASP.NET projects that are build with deprecated DNX toolchain, which allows for multiple targets.)</span></span>

## <a name="runtimes"></a><span data-ttu-id="a9f17-146">Moduly runtime</span><span class="sxs-lookup"><span data-stu-id="a9f17-146">Runtimes</span></span>

<span data-ttu-id="a9f17-147">Obsahuje operační systémy a architektury, které běží vaše aplikace, jako například `win10-arm`, `win8-x64`, `win8-x86`.</span><span class="sxs-lookup"><span data-stu-id="a9f17-147">Lists the operating systems and architectures that your app runs on, such as `win10-arm`, `win8-x64`, `win8-x86`.</span></span>

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

<span data-ttu-id="a9f17-148">Balíček obsahující PCL, který můžete spustit na jakékoli runtime nebude muset zadat modulu runtime.</span><span class="sxs-lookup"><span data-stu-id="a9f17-148">A package containing a PCL that can run on any runtime doesn't need to specify a runtime.</span></span> <span data-ttu-id="a9f17-149">Toto musí být také platí všechny závislosti, v opačném případě je nutné zadat moduly runtime.</span><span class="sxs-lookup"><span data-stu-id="a9f17-149">This must also be true of any dependencies, otherwise you must specify runtimes.</span></span>


## <a name="supports"></a><span data-ttu-id="a9f17-150">Podporuje</span><span class="sxs-lookup"><span data-stu-id="a9f17-150">Supports</span></span>

<span data-ttu-id="a9f17-151">Definuje sadu kontroluje pro závislosti balíčků.</span><span class="sxs-lookup"><span data-stu-id="a9f17-151">Defines a set of checks for package dependencies.</span></span> <span data-ttu-id="a9f17-152">Můžete definovat, kdy očekáváte PCL nebo aplikace spustit.</span><span class="sxs-lookup"><span data-stu-id="a9f17-152">You can define where you expect the PCL or app to run.</span></span> <span data-ttu-id="a9f17-153">Definice nejsou omezující, jak váš kód pravděpodobně bude moci spustit jinde.</span><span class="sxs-lookup"><span data-stu-id="a9f17-153">The definitions are not restrictive, as your code may be able to run elsewhere.</span></span> <span data-ttu-id="a9f17-154">Ale zadání těchto kontrol provádí NuGet, zkontrolujte, že jsou splněny všechny závislosti na uvedené TxMs.</span><span class="sxs-lookup"><span data-stu-id="a9f17-154">But specifying these checks makes NuGet check that all dependencies are satisfied on the listed TxMs.</span></span> <span data-ttu-id="a9f17-155">Příklady hodnot pro tyto: `net46.app`, `uwp.10.0.app`atd.</span><span class="sxs-lookup"><span data-stu-id="a9f17-155">Examples of the values for this are: `net46.app`, `uwp.10.0.app`, etc.</span></span>

<span data-ttu-id="a9f17-156">V této části by měl naplněny automaticky, když vyberete položku v dialogovém okně knihovny přenosných tříd cíle.</span><span class="sxs-lookup"><span data-stu-id="a9f17-156">This section should be populated automatically when you select an entry in the Portable Class Library targets dialog.</span></span>

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a><span data-ttu-id="a9f17-157">Importy</span><span class="sxs-lookup"><span data-stu-id="a9f17-157">Imports</span></span>

<span data-ttu-id="a9f17-158">Importy jsou navržené tak, aby balíčky, které používají `dotnet` TxM pracovat s balíčky, které nejsou deklarovat dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="a9f17-158">Imports are designed to allow packages that use the `dotnet` TxM to operate with packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="a9f17-159">Pokud je váš projekt pomocí `dotnet` TxM pak všechny balíčky, které závisí na musí také mít `dotnet` TxM, pokud přidejte následující vaše `project.json` umožňující bez `dotnet` platformy, aby byl kompatibilní s `dotnet`:</span><span class="sxs-lookup"><span data-stu-id="a9f17-159">If your project is using the `dotnet` TxM then all the packages you depend on must also have a `dotnet` TxM, unless you add the following to your `project.json` to allow non `dotnet` platforms to be compatible with `dotnet`:</span></span>

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

<span data-ttu-id="a9f17-160">Pokud používáte `dotnet` TxM pak systém projektu PCL přidá odpovídající `imports` příkaz na základě podporované cílů.</span><span class="sxs-lookup"><span data-stu-id="a9f17-160">If you are using the `dotnet` TxM then the PCL project system adds the appropriate `imports` statement based on the supported targets.</span></span>

## <a name="differences-from-portable-apps-and-web-projects"></a><span data-ttu-id="a9f17-161">Rozdíl oproti přenosné aplikace a webové projekty</span><span class="sxs-lookup"><span data-stu-id="a9f17-161">Differences from portable apps and web projects</span></span>

<span data-ttu-id="a9f17-162">`project.json` Soubor používaný NuGet je podmnožinou který nalézt projektů ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="a9f17-162">The `project.json` file used by NuGet is a subset of that found in ASP.NET Core projects.</span></span> <span data-ttu-id="a9f17-163">V ASP.NET Core `project.json` se používá pro projekt metadata, kompilace informace a závislosti.</span><span class="sxs-lookup"><span data-stu-id="a9f17-163">In ASP.NET Core `project.json` is used for project metadata, compilation information, and dependencies.</span></span> <span data-ttu-id="a9f17-164">Pokud se použije v ostatních systémech projektu, jsou tyto tři věci rozdělit do samostatných souborů a `project.json` menší informacemi.</span><span class="sxs-lookup"><span data-stu-id="a9f17-164">When used in other project systems, those three things are split into separate files and `project.json` contains less information.</span></span> <span data-ttu-id="a9f17-165">Významné rozdíly patří:</span><span class="sxs-lookup"><span data-stu-id="a9f17-165">Notable differences include:</span></span>

- <span data-ttu-id="a9f17-166">Může existovat pouze jedna framework v `frameworks` oddílu.</span><span class="sxs-lookup"><span data-stu-id="a9f17-166">There can only be one framework in the `frameworks` section.</span></span>

- <span data-ttu-id="a9f17-167">Soubor nemůže obsahovat závislosti, možnosti kompilace, atd., které se zobrazí v DNX `project.json` soubory.</span><span class="sxs-lookup"><span data-stu-id="a9f17-167">The file cannot contain dependencies, compilation options, etc. that you see in DNX `project.json` files.</span></span> <span data-ttu-id="a9f17-168">Vzhledem k tomu, že může existovat jenom jeden framework nemá smysl zadat závislosti konkrétní rozhraní.</span><span class="sxs-lookup"><span data-stu-id="a9f17-168">Given that there can only be a single framework it doesn't make sense to enter framework-specific dependencies.</span></span>

- <span data-ttu-id="a9f17-169">Kompilace se zpracovává souborem MSBuild tak kompilace možnosti preprocesoru definuje atd., jsou všechny součástí soubor projektu nástroje MSBuild a není `project.json`.</span><span class="sxs-lookup"><span data-stu-id="a9f17-169">Compilation is handled by MSBuild so compilation options, preprocessor defines, etc. are all part of the MSBuild project file and not `project.json`.</span></span>

<span data-ttu-id="a9f17-170">V NuGet 3 + vývojáři neočekává se ručně upravit, pokud `project.json`, protože uživatelské rozhraní Správce balíčků v sadě Visual Studio zpracovává obsah.</span><span class="sxs-lookup"><span data-stu-id="a9f17-170">In NuGet 3+, developers are not expected to manually edit the `project.json`, as the Package Manager UI in Visual Studio manipulates the content.</span></span> <span data-ttu-id="a9f17-171">Ale nutné dodat, jistě můžete upravit soubor, ale musí sestavte projekt a spusťte obnovení balíčků nebo vyvolat obnovení jiným způsobem.</span><span class="sxs-lookup"><span data-stu-id="a9f17-171">That said, you can certainly edit the file, but you must build the project to start a package restore or invoke restore in another way.</span></span> <span data-ttu-id="a9f17-172">V tématu [obnovení balíčků](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="a9f17-172">See [Package restore](../consume-packages/package-restore.md).</span></span>


## <a name="projectlockjson"></a><span data-ttu-id="a9f17-173">project.lock.json</span><span class="sxs-lookup"><span data-stu-id="a9f17-173">project.lock.json</span></span>

<span data-ttu-id="a9f17-174">`project.lock.json` Soubor je generován právě probíhá obnovení balíčků NuGet v projektech, které používají `project.json`.</span><span class="sxs-lookup"><span data-stu-id="a9f17-174">The `project.lock.json` file is generated in the process of restoring the NuGet packages in projects that use `project.json`.</span></span> <span data-ttu-id="a9f17-175">Drží snímek všechny informace, které jsou generovány jako provede grafu balíčků NuGet a zahrnuje verze, obsah a závislých součástí pro všechny balíčky v projektu.</span><span class="sxs-lookup"><span data-stu-id="a9f17-175">It holds a snapshot of all the information that is generated as NuGet walks the graph of packages and includes the version, contents, and dependencies of all the packages in your project.</span></span> <span data-ttu-id="a9f17-176">Systém sestavení pomocí to balíčky z globální umístění, které jsou relevantní při sestavování projektu místo v závislosti na složku místní balíčky v projektu.</span><span class="sxs-lookup"><span data-stu-id="a9f17-176">The build system uses this to choose packages from a global location that are relevant when building the project instead of depending on a local packages folder in the project itself.</span></span> <span data-ttu-id="a9f17-177">Výsledkem je vyšší výkon sestavení vzhledem k tomu, že je potřeba jen pro čtení `project.lock.json` místo mnoho oddělení `.nuspec` soubory.</span><span class="sxs-lookup"><span data-stu-id="a9f17-177">This results in faster build performance because it's necessary to read only `project.lock.json` instead of many separate `.nuspec` files.</span></span>

<span data-ttu-id="a9f17-178">`project.lock.json`se automaticky vygeneroval na obnovení balíčků, tak ho lze vynechat od správy zdrojového kódu, přidejte je do `.gitignore` a `.tfignore` soubory (viz [balíčky a Správa zdrojového kódu](../consume-packages/packages-and-source-control.md).</span><span class="sxs-lookup"><span data-stu-id="a9f17-178">`project.lock.json` is automatically generated on package restore, so it can be omitted from source control by adding it to `.gitignore` and `.tfignore` files (see [Packages and source control](../consume-packages/packages-and-source-control.md).</span></span> <span data-ttu-id="a9f17-179">Ale pokud zahrnete ji do správy zdrojového kódu, historii změn zobrazuje změny v závislosti přeložit v čase.</span><span class="sxs-lookup"><span data-stu-id="a9f17-179">However, if you include it in source control, the change history shows changes in dependencies resolved over time.</span></span>
