---
title: Odkaz na soubor Project.JSON pro NuGet
description: V některých typech projektů project.json udržuje seznam balíčky NuGet používané v projektu.
author: karann-msft
ms.author: karann
ms.date: 07/27/2017
ms.topic: reference
ms.openlocfilehash: e4d8b5b9ab4605516827ead8939f278d110c7a48
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547781"
---
# <a name="projectjson-reference"></a><span data-ttu-id="cf294-103">odkaz na Project.JSON</span><span class="sxs-lookup"><span data-stu-id="cf294-103">project.json reference</span></span>

<span data-ttu-id="cf294-104">*NuGet 3.x+*</span><span class="sxs-lookup"><span data-stu-id="cf294-104">*NuGet 3.x+*</span></span>

<span data-ttu-id="cf294-105">`project.json` Souboru udržuje seznam balíčků používá v projektu, označované jako formát správy balíčků.</span><span class="sxs-lookup"><span data-stu-id="cf294-105">The `project.json` file maintains a list of packages used in a project, known as a package management format.</span></span> <span data-ttu-id="cf294-106">Tato Smlouva nahrazuje `packages.config` ale zase nahrazována [PackageReference](../consume-packages/package-references-in-project-files.md) nuget 4.0 +.</span><span class="sxs-lookup"><span data-stu-id="cf294-106">It supersedes `packages.config` but is in turn superseded by [PackageReference](../consume-packages/package-references-in-project-files.md) with NuGet 4.0+.</span></span>

<span data-ttu-id="cf294-107">[ `project.lock.json` ](#projectlockjson) Souboru (popsaných níže) se také používá v projektech využívající `project.json`.</span><span class="sxs-lookup"><span data-stu-id="cf294-107">The [`project.lock.json`](#projectlockjson) file (described below) is also used in projects employing `project.json`.</span></span>

<span data-ttu-id="cf294-108">`project.json` má následující základní strukturou, kde každý z objektů čtyři nejvyšší úrovně může mít libovolný počet podřízených objektů:</span><span class="sxs-lookup"><span data-stu-id="cf294-108">`project.json` has the following basic structure, where each of the four top-level objects can have any number of child objects:</span></span>

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

## <a name="dependencies"></a><span data-ttu-id="cf294-109">Závislosti</span><span class="sxs-lookup"><span data-stu-id="cf294-109">Dependencies</span></span>

<span data-ttu-id="cf294-110">Zobrazí seznam závislosti balíčku NuGet projektu v následujícím tvaru:</span><span class="sxs-lookup"><span data-stu-id="cf294-110">Lists the NuGet package dependencies of your project in the following form:</span></span>

```json
"PackageID" : "version_constraint"
```

<span data-ttu-id="cf294-111">Příklad:</span><span class="sxs-lookup"><span data-stu-id="cf294-111">For example:</span></span>

```json
"dependencies": {
    "Microsoft.NETCore": "5.0.0",
    "System.Runtime.Serialization.Primitives": "4.0.10"
}
```

<span data-ttu-id="cf294-112">`dependencies` Je oddíl, kde dialogové okno Správce balíčků NuGet přidá závislosti balíčků do vašeho projektu.</span><span class="sxs-lookup"><span data-stu-id="cf294-112">The `dependencies` section is where the NuGet Package Manager dialog adds package dependencies to your project.</span></span>

<span data-ttu-id="cf294-113">Id balíčku, který odpovídá id balíčků na nuget.org, stejné jako id použít v konzole Správce balíčků: `Install-Package Microsoft.NETCore`.</span><span class="sxs-lookup"><span data-stu-id="cf294-113">The Package id corresponds to the id of the package on nuget.org , the same as the id used in the package manager console: `Install-Package Microsoft.NETCore`.</span></span>

<span data-ttu-id="cf294-114">Při obnovování balíčků, omezení verze `"5.0.0"` znamená `>= 5.0.0`.</span><span class="sxs-lookup"><span data-stu-id="cf294-114">When restoring packages, the version constraint of `"5.0.0"` implies `>= 5.0.0`.</span></span> <span data-ttu-id="cf294-115">To znamená pokud 5.0.0 není k dispozici na serveru, ale je – 5.0.1, nainstaluje – 5.0.1 NuGet a upozorňuje na inovace.</span><span class="sxs-lookup"><span data-stu-id="cf294-115">That is, if 5.0.0 is not available on the server but 5.0.1 is, NuGet installs  5.0.1 and warns you about the upgrade.</span></span> <span data-ttu-id="cf294-116">Jinak NuGet vybere nejnižší možné verze na serveru odpovídající omezení.</span><span class="sxs-lookup"><span data-stu-id="cf294-116">NuGet otherwise picks the lowest possible version on the server matching the constraint.</span></span>

<span data-ttu-id="cf294-117">Zobrazit [řešení závislostí](../consume-packages/dependency-resolution.md) podrobné informace o řešení pravidla.</span><span class="sxs-lookup"><span data-stu-id="cf294-117">See [Dependency resolution](../consume-packages/dependency-resolution.md) for more details on resolution rules.</span></span>

### <a name="managing-dependency-assets"></a><span data-ttu-id="cf294-118">Správa závislostí prostředky</span><span class="sxs-lookup"><span data-stu-id="cf294-118">Managing dependency assets</span></span>

<span data-ttu-id="cf294-119">Které prostředky od závislostí tok do nejvyšší úrovně projektu je řízen tak, že zadáte sadu klíčových slov do oddělených čárkou `include` a `exclude` vlastnosti odkazu na závislost.</span><span class="sxs-lookup"><span data-stu-id="cf294-119">Which assets from dependencies flow into the top-level project is controlled by specifying a comma-delimited set of tags in the `include` and `exclude` properties of the dependency reference.</span></span> <span data-ttu-id="cf294-120">Značky jsou uvedeny v následující tabulce:</span><span class="sxs-lookup"><span data-stu-id="cf294-120">The tags are listed the table below:</span></span>

| <span data-ttu-id="cf294-121">Zahrnutí a vyloučení značek</span><span class="sxs-lookup"><span data-stu-id="cf294-121">Include/Exclude tag</span></span> | <span data-ttu-id="cf294-122">Ovlivněné složky cíle</span><span class="sxs-lookup"><span data-stu-id="cf294-122">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="cf294-123">contentFiles</span><span class="sxs-lookup"><span data-stu-id="cf294-123">contentFiles</span></span> | <span data-ttu-id="cf294-124">Obsah</span><span class="sxs-lookup"><span data-stu-id="cf294-124">Content</span></span>  |
| <span data-ttu-id="cf294-125">modul runtime</span><span class="sxs-lookup"><span data-stu-id="cf294-125">runtime</span></span> | <span data-ttu-id="cf294-126">Modul runtime, prostředky a FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="cf294-126">Runtime, Resources, and FrameworkAssemblies</span></span>  |
| <span data-ttu-id="cf294-127">Kompilace</span><span class="sxs-lookup"><span data-stu-id="cf294-127">compile</span></span> | <span data-ttu-id="cf294-128">lib</span><span class="sxs-lookup"><span data-stu-id="cf294-128">lib</span></span> |
| <span data-ttu-id="cf294-129">sestavení</span><span class="sxs-lookup"><span data-stu-id="cf294-129">build</span></span> | <span data-ttu-id="cf294-130">sestavení (cíle a vlastnosti nástroje MSBuild)</span><span class="sxs-lookup"><span data-stu-id="cf294-130">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="cf294-131">nativní</span><span class="sxs-lookup"><span data-stu-id="cf294-131">native</span></span> | <span data-ttu-id="cf294-132">nativní</span><span class="sxs-lookup"><span data-stu-id="cf294-132">native</span></span> |
| <span data-ttu-id="cf294-133">žádná</span><span class="sxs-lookup"><span data-stu-id="cf294-133">none</span></span> | <span data-ttu-id="cf294-134">Žádné složky</span><span class="sxs-lookup"><span data-stu-id="cf294-134">No folders</span></span> |
| <span data-ttu-id="cf294-135">všechny</span><span class="sxs-lookup"><span data-stu-id="cf294-135">all</span></span> | <span data-ttu-id="cf294-136">Všechny složky</span><span class="sxs-lookup"><span data-stu-id="cf294-136">All folders</span></span> |

<span data-ttu-id="cf294-137">Značky s `exclude` přednost zadaným `include`.</span><span class="sxs-lookup"><span data-stu-id="cf294-137">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="cf294-138">Například `include="runtime, compile" exclude="compile"` je stejný jako `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="cf294-138">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span>

<span data-ttu-id="cf294-139">Například chcete zahrnout `build` a `native` složky závislosti, použijte následující:</span><span class="sxs-lookup"><span data-stu-id="cf294-139">For example, to include the `build` and `native` folders of a dependency, use the following:</span></span>

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

<span data-ttu-id="cf294-140">Chcete-li vyloučit `content` a `build` složky závislosti, použijte následující:</span><span class="sxs-lookup"><span data-stu-id="cf294-140">To exclude the `content` and `build` folders of a dependency, use the following:</span></span>

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

## <a name="frameworks"></a><span data-ttu-id="cf294-141">Rozhraní</span><span class="sxs-lookup"><span data-stu-id="cf294-141">Frameworks</span></span>

<span data-ttu-id="cf294-142">Obsahuje seznam rozhraní projektu, na kterých běží, jako například `net45`, `netcoreapp`, `netstandard`.</span><span class="sxs-lookup"><span data-stu-id="cf294-142">Lists the frameworks that the project runs on, such as `net45`, `netcoreapp`, `netstandard`.</span></span>

```json
"frameworks": {
    "netcore50": {}
    }
 ```

<span data-ttu-id="cf294-143">Je povolena pouze jedna položka `frameworks` oddílu.</span><span class="sxs-lookup"><span data-stu-id="cf294-143">Only a single entry is allowed in the `frameworks` section.</span></span> <span data-ttu-id="cf294-144">(Výjimkou je `project.json` souborů pro projekty ASP.NET, které jsou sestavení s nepoužívané DNX nástroj řetězce, která umožňuje více cílů.)</span><span class="sxs-lookup"><span data-stu-id="cf294-144">(An exception is `project.json` files for ASP.NET projects that are build with deprecated DNX tool chain, which allows for multiple targets.)</span></span>

## <a name="runtimes"></a><span data-ttu-id="cf294-145">Moduly runtime</span><span class="sxs-lookup"><span data-stu-id="cf294-145">Runtimes</span></span>

<span data-ttu-id="cf294-146">Obsahuje seznam operačních systémů a architektur, které vaše aplikace běží na serveru, jako například `win10-arm`, `win8-x64`, `win8-x86`.</span><span class="sxs-lookup"><span data-stu-id="cf294-146">Lists the operating systems and architectures that your app runs on, such as `win10-arm`, `win8-x64`, `win8-x86`.</span></span>

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

<span data-ttu-id="cf294-147">Balíček, který obsahuje, můžete spustit na libovolné runtime PCL nepotřebuje k určení modulu runtime.</span><span class="sxs-lookup"><span data-stu-id="cf294-147">A package containing a PCL that can run on any runtime doesn't need to specify a runtime.</span></span> <span data-ttu-id="cf294-148">Musí být také platí pro všechny závislosti, jinak je nutné zadat moduly runtime.</span><span class="sxs-lookup"><span data-stu-id="cf294-148">This must also be true of any dependencies, otherwise you must specify runtimes.</span></span>


## <a name="supports"></a><span data-ttu-id="cf294-149">Podporuje</span><span class="sxs-lookup"><span data-stu-id="cf294-149">Supports</span></span>

<span data-ttu-id="cf294-150">Definuje sadu kontroluje pro závislosti balíčků.</span><span class="sxs-lookup"><span data-stu-id="cf294-150">Defines a set of checks for package dependencies.</span></span> <span data-ttu-id="cf294-151">Můžete definovat, kdy očekáváte PCL nebo na spuštění aplikace.</span><span class="sxs-lookup"><span data-stu-id="cf294-151">You can define where you expect the PCL or app to run.</span></span> <span data-ttu-id="cf294-152">Definice nejsou omezující, jak váš kód může být možné spouštět jinde.</span><span class="sxs-lookup"><span data-stu-id="cf294-152">The definitions are not restrictive, as your code may be able to run elsewhere.</span></span> <span data-ttu-id="cf294-153">Ale zadáte tyto kontroly díky NuGet, zkontrolujte, že jsou splněny všechny závislosti na uvedené TxMs.</span><span class="sxs-lookup"><span data-stu-id="cf294-153">But specifying these checks makes NuGet check that all dependencies are satisfied on the listed TxMs.</span></span> <span data-ttu-id="cf294-154">Příklady hodnot jsou: `net46.app`, `uwp.10.0.app`atd.</span><span class="sxs-lookup"><span data-stu-id="cf294-154">Examples of the values for this are: `net46.app`, `uwp.10.0.app`, etc.</span></span>

<span data-ttu-id="cf294-155">Tato část by měl vyplní automaticky, když vyberete položku v dialogovém okně knihovny přenosných tříd cíle.</span><span class="sxs-lookup"><span data-stu-id="cf294-155">This section should be populated automatically when you select an entry in the Portable Class Library targets dialog.</span></span>

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a><span data-ttu-id="cf294-156">Importy</span><span class="sxs-lookup"><span data-stu-id="cf294-156">Imports</span></span>

<span data-ttu-id="cf294-157">Importy jsou navržené tak, aby balíčky, které používají `dotnet` TxM pracovat s balíčky, které není deklarovat dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="cf294-157">Imports are designed to allow packages that use the `dotnet` TxM to operate with packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="cf294-158">Pokud váš projekt používá `dotnet` TxM pak všechny balíčky, které závisí na musí mít také `dotnet` TxM, pokud přidejte následující text do vašeho `project.json` umožňující bez `dotnet` platformy se kvůli kompatibilitě s `dotnet`:</span><span class="sxs-lookup"><span data-stu-id="cf294-158">If your project is using the `dotnet` TxM then all the packages you depend on must also have a `dotnet` TxM, unless you add the following to your `project.json` to allow non `dotnet` platforms to be compatible with `dotnet`:</span></span>

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

<span data-ttu-id="cf294-159">Pokud používáte `dotnet` TxM pak systém projektu PCL přidá odpovídající `imports` příkaz na základě podporovaných cílů.</span><span class="sxs-lookup"><span data-stu-id="cf294-159">If you are using the `dotnet` TxM then the PCL project system adds the appropriate `imports` statement based on the supported targets.</span></span>

## <a name="differences-from-portable-apps-and-web-projects"></a><span data-ttu-id="cf294-160">Rozdíl oproti přenosné aplikace a webové projekty</span><span class="sxs-lookup"><span data-stu-id="cf294-160">Differences from portable apps and web projects</span></span>

<span data-ttu-id="cf294-161">`project.json` Soubor používaný NuGet je podmnožinou nalezeným v projektech ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="cf294-161">The `project.json` file used by NuGet is a subset of that found in ASP.NET Core projects.</span></span> <span data-ttu-id="cf294-162">V ASP.NET Core `project.json` se používá pro metadata projektu, informace o kompilaci a závislosti.</span><span class="sxs-lookup"><span data-stu-id="cf294-162">In ASP.NET Core `project.json` is used for project metadata, compilation information, and dependencies.</span></span> <span data-ttu-id="cf294-163">Při použití v jiných systémech projektu, jsou tyto tři věci rozdělit na samostatné soubory a `project.json` obsahuje méně informací.</span><span class="sxs-lookup"><span data-stu-id="cf294-163">When used in other project systems, those three things are split into separate files and `project.json` contains less information.</span></span> <span data-ttu-id="cf294-164">Významný rozdíl patří:</span><span class="sxs-lookup"><span data-stu-id="cf294-164">Notable differences include:</span></span>

- <span data-ttu-id="cf294-165">Může existovat pouze jedno rozhraní v `frameworks` oddílu.</span><span class="sxs-lookup"><span data-stu-id="cf294-165">There can only be one framework in the `frameworks` section.</span></span>

- <span data-ttu-id="cf294-166">Soubor nesmí obsahovat závislosti, možnosti kompilace, atd., které se zobrazí v DNX `project.json` soubory.</span><span class="sxs-lookup"><span data-stu-id="cf294-166">The file cannot contain dependencies, compilation options, etc. that you see in DNX `project.json` files.</span></span> <span data-ttu-id="cf294-167">Vzhledem k tomu, že může existovat pouze jeden rámec ho nemá smysl zadejte závislosti pro konkrétní rozhraní.</span><span class="sxs-lookup"><span data-stu-id="cf294-167">Given that there can only be a single framework it doesn't make sense to enter framework-specific dependencies.</span></span>

- <span data-ttu-id="cf294-168">Kompilace se zpracovává souborem MSBuild tak definuje možnosti kompilace, preprocesoru, atd. jsou všechny části souboru projektu MSBuild, ne `project.json`.</span><span class="sxs-lookup"><span data-stu-id="cf294-168">Compilation is handled by MSBuild so compilation options, preprocessor defines, etc. are all part of the MSBuild project file and not `project.json`.</span></span>

<span data-ttu-id="cf294-169">Ve Správci NuGet 3 +, vývojáři nepředpokládá ručně upravit `project.json`, protože uživatelské rozhraní Správce balíčků v sadě Visual Studio pracuje obsah.</span><span class="sxs-lookup"><span data-stu-id="cf294-169">In NuGet 3+, developers are not expected to manually edit the `project.json`, as the Package Manager UI in Visual Studio manipulates the content.</span></span> <span data-ttu-id="cf294-170">Ale nutné dodat, určitě můžete upravit soubor, ale musíte sestavit projekt ke spuštění obnovení balíčku nebo vyvolat obnovení jiným způsobem.</span><span class="sxs-lookup"><span data-stu-id="cf294-170">That said, you can certainly edit the file, but you must build the project to start a package restore or invoke restore in another way.</span></span> <span data-ttu-id="cf294-171">Zobrazit [obnovení balíčku](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="cf294-171">See [Package restore](../consume-packages/package-restore.md).</span></span>


## <a name="projectlockjson"></a><span data-ttu-id="cf294-172">project.lock.json</span><span class="sxs-lookup"><span data-stu-id="cf294-172">project.lock.json</span></span>

<span data-ttu-id="cf294-173">`project.lock.json` Soubor se generuje Probíhá obnovování balíčků NuGet v projektech, které používají `project.json`.</span><span class="sxs-lookup"><span data-stu-id="cf294-173">The `project.lock.json` file is generated in the process of restoring the NuGet packages in projects that use `project.json`.</span></span> <span data-ttu-id="cf294-174">Obsahuje snímek všech informace, které jsou generovány podle vás grafu balíčky NuGet a obsahuje verze, obsah a všech balíčků závislostí ve vašem projektu.</span><span class="sxs-lookup"><span data-stu-id="cf294-174">It holds a snapshot of all the information that is generated as NuGet walks the graph of packages and includes the version, contents, and dependencies of all the packages in your project.</span></span> <span data-ttu-id="cf294-175">Systém sestavení používá toto vybrat balíčky z globálního místa, které jsou relevantní, při sestavování projektu namísto v závislosti na balíčky místní složky v projektu.</span><span class="sxs-lookup"><span data-stu-id="cf294-175">The build system uses this to choose packages from a global location that are relevant when building the project instead of depending on a local packages folder in the project itself.</span></span> <span data-ttu-id="cf294-176">Výsledkem je rychlejší výkon sestavení vzhledem k tomu je potřeba jen pro čtení `project.lock.json` místo mnoho oddělení `.nuspec` soubory.</span><span class="sxs-lookup"><span data-stu-id="cf294-176">This results in faster build performance because it's necessary to read only `project.lock.json` instead of many separate `.nuspec` files.</span></span>

<span data-ttu-id="cf294-177">`project.lock.json` není automaticky vygenerován při obnovování balíčků, tak ho lze vynechat ze správy zdrojového kódu tak, že ji přidáte `.gitignore` a `.tfignore` soubory (viz [balíčky a Správa zdrojového kódu](../consume-packages/packages-and-source-control.md).</span><span class="sxs-lookup"><span data-stu-id="cf294-177">`project.lock.json` is automatically generated on package restore, so it can be omitted from source control by adding it to `.gitignore` and `.tfignore` files (see [Packages and source control](../consume-packages/packages-and-source-control.md).</span></span> <span data-ttu-id="cf294-178">Ale pokud ho zahrnete ve správě zdrojového kódu, historii změn zobrazí změny v závislosti vyřešených v průběhu času.</span><span class="sxs-lookup"><span data-stu-id="cf294-178">However, if you include it in source control, the change history shows changes in dependencies resolved over time.</span></span>
