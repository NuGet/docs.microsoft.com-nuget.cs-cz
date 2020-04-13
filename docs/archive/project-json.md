---
title: project.json File Reference pro NuGet
description: V některých typech projektu project.json udržuje seznam balíčků NuGet použitých v projektu.
author: karann-msft
ms.author: karann
ms.date: 07/27/2017
ms.topic: reference
ms.openlocfilehash: 5ecbcd4855de8ea7b6301a5e307779216baf96fc
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "69488285"
---
# <a name="projectjson-reference"></a><span data-ttu-id="929c7-103">odkaz na project.json</span><span class="sxs-lookup"><span data-stu-id="929c7-103">project.json reference</span></span>

<span data-ttu-id="929c7-104">*NuGet 3.x+*</span><span class="sxs-lookup"><span data-stu-id="929c7-104">*NuGet 3.x+*</span></span>

<span data-ttu-id="929c7-105">Soubor `project.json` udržuje seznam balíčků používaných v projektu, známý jako formát správy balíčků.</span><span class="sxs-lookup"><span data-stu-id="929c7-105">The `project.json` file maintains a list of packages used in a project, known as a package management format.</span></span> <span data-ttu-id="929c7-106">Nahrazuje, `packages.config` ale je zase nahrazen [PackageReference](../consume-packages/package-references-in-project-files.md) s NuGet 4.0 +.</span><span class="sxs-lookup"><span data-stu-id="929c7-106">It supersedes `packages.config` but is in turn superseded by [PackageReference](../consume-packages/package-references-in-project-files.md) with NuGet 4.0+.</span></span>

<span data-ttu-id="929c7-107">Soubor [`project.lock.json`](#projectlockjson) (popsaný níže) se také používá `project.json`v projektech využívajících .</span><span class="sxs-lookup"><span data-stu-id="929c7-107">The [`project.lock.json`](#projectlockjson) file (described below) is also used in projects employing `project.json`.</span></span>

<span data-ttu-id="929c7-108">`project.json`má následující základní strukturu, kde každý ze čtyř objektů nejvyšší úrovně může mít libovolný počet podřízených objektů:</span><span class="sxs-lookup"><span data-stu-id="929c7-108">`project.json` has the following basic structure, where each of the four top-level objects can have any number of child objects:</span></span>

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

## <a name="dependencies"></a><span data-ttu-id="929c7-109">Závislosti</span><span class="sxs-lookup"><span data-stu-id="929c7-109">Dependencies</span></span>

<span data-ttu-id="929c7-110">Zobrazí seznam závislostí balíčku NuGet projektu v následujícím formuláři:</span><span class="sxs-lookup"><span data-stu-id="929c7-110">Lists the NuGet package dependencies of your project in the following form:</span></span>

```json
"PackageID" : "version_constraint"
```

<span data-ttu-id="929c7-111">Příklad:</span><span class="sxs-lookup"><span data-stu-id="929c7-111">For example:</span></span>

```json
"dependencies": {
    "Microsoft.NETCore": "5.0.0",
    "System.Runtime.Serialization.Primitives": "4.0.10"
}
```

<span data-ttu-id="929c7-112">Část `dependencies` je, kde dialogové okno NuGet Package Manager přidá závislosti balíčků do projektu.</span><span class="sxs-lookup"><span data-stu-id="929c7-112">The `dependencies` section is where the NuGet Package Manager dialog adds package dependencies to your project.</span></span>

<span data-ttu-id="929c7-113">ID balíčku odpovídá id balíčku na nuget.org , stejné jako id použité v `Install-Package Microsoft.NETCore`konzole správce balíčků: .</span><span class="sxs-lookup"><span data-stu-id="929c7-113">The Package id corresponds to the id of the package on nuget.org , the same as the id used in the package manager console: `Install-Package Microsoft.NETCore`.</span></span>

<span data-ttu-id="929c7-114">Při obnovování balíčků, verze `"5.0.0"` `>= 5.0.0`omezení implikuje .</span><span class="sxs-lookup"><span data-stu-id="929c7-114">When restoring packages, the version constraint of `"5.0.0"` implies `>= 5.0.0`.</span></span> <span data-ttu-id="929c7-115">To znamená, že pokud 5.0.0 není k dispozici na serveru, ale 5.0.1 je, NuGet nainstaluje 5.0.1 a upozorní vás na upgrade.</span><span class="sxs-lookup"><span data-stu-id="929c7-115">That is, if 5.0.0 is not available on the server but 5.0.1 is, NuGet installs  5.0.1 and warns you about the upgrade.</span></span> <span data-ttu-id="929c7-116">NuGet jinak vybere nejnižší možnou verzi na serveru odpovídající omezení.</span><span class="sxs-lookup"><span data-stu-id="929c7-116">NuGet otherwise picks the lowest possible version on the server matching the constraint.</span></span>

<span data-ttu-id="929c7-117">Další podrobnosti o pravidlech řešení problémů najdete v [tématu Řešení závislostí.](../concepts/dependency-resolution.md)</span><span class="sxs-lookup"><span data-stu-id="929c7-117">See [Dependency resolution](../concepts/dependency-resolution.md) for more details on resolution rules.</span></span>

### <a name="managing-dependency-assets"></a><span data-ttu-id="929c7-118">Správa prostředků závislostí</span><span class="sxs-lookup"><span data-stu-id="929c7-118">Managing dependency assets</span></span>

<span data-ttu-id="929c7-119">Prostředky ze závislostí toku do projektu nejvyšší úrovně je řízen a zadáním čárka oddělené sadu značek v `include` a `exclude` vlastnosti odkazu na závislost.</span><span class="sxs-lookup"><span data-stu-id="929c7-119">Which assets from dependencies flow into the top-level project is controlled by specifying a comma-delimited set of tags in the `include` and `exclude` properties of the dependency reference.</span></span> <span data-ttu-id="929c7-120">Značky jsou uvedeny v následující tabulce:</span><span class="sxs-lookup"><span data-stu-id="929c7-120">The tags are listed the table below:</span></span>

| <span data-ttu-id="929c7-121">Značka Zahrnout/vyloučit</span><span class="sxs-lookup"><span data-stu-id="929c7-121">Include/Exclude tag</span></span> | <span data-ttu-id="929c7-122">Ovlivněné složky cíle</span><span class="sxs-lookup"><span data-stu-id="929c7-122">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="929c7-123">contentFiles</span><span class="sxs-lookup"><span data-stu-id="929c7-123">contentFiles</span></span> | <span data-ttu-id="929c7-124">Obsah</span><span class="sxs-lookup"><span data-stu-id="929c7-124">Content</span></span>  |
| <span data-ttu-id="929c7-125">modul runtime</span><span class="sxs-lookup"><span data-stu-id="929c7-125">runtime</span></span> | <span data-ttu-id="929c7-126">Runtime, prostředky a frameworkassemblies</span><span class="sxs-lookup"><span data-stu-id="929c7-126">Runtime, Resources, and FrameworkAssemblies</span></span>  |
| <span data-ttu-id="929c7-127">kompilovat</span><span class="sxs-lookup"><span data-stu-id="929c7-127">compile</span></span> | <span data-ttu-id="929c7-128">Lib</span><span class="sxs-lookup"><span data-stu-id="929c7-128">lib</span></span> |
| <span data-ttu-id="929c7-129">sestavení</span><span class="sxs-lookup"><span data-stu-id="929c7-129">build</span></span> | <span data-ttu-id="929c7-130">sestavení (rekvizity a cíle MSBuild)</span><span class="sxs-lookup"><span data-stu-id="929c7-130">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="929c7-131">nativní</span><span class="sxs-lookup"><span data-stu-id="929c7-131">native</span></span> | <span data-ttu-id="929c7-132">nativní</span><span class="sxs-lookup"><span data-stu-id="929c7-132">native</span></span> |
| <span data-ttu-id="929c7-133">Žádná</span><span class="sxs-lookup"><span data-stu-id="929c7-133">none</span></span> | <span data-ttu-id="929c7-134">Žádné složky</span><span class="sxs-lookup"><span data-stu-id="929c7-134">No folders</span></span> |
| <span data-ttu-id="929c7-135">Vše</span><span class="sxs-lookup"><span data-stu-id="929c7-135">all</span></span> | <span data-ttu-id="929c7-136">Všechny složky</span><span class="sxs-lookup"><span data-stu-id="929c7-136">All folders</span></span> |

<span data-ttu-id="929c7-137">Značky `exclude` zadané s předností `include`před těmi, které jsou zadány s .</span><span class="sxs-lookup"><span data-stu-id="929c7-137">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="929c7-138">Například `include="runtime, compile" exclude="compile"` je stejný `include="runtime"`jako .</span><span class="sxs-lookup"><span data-stu-id="929c7-138">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span>

<span data-ttu-id="929c7-139">Chcete-li například `build` `native` zahrnout složky a závislost, použijte následující:</span><span class="sxs-lookup"><span data-stu-id="929c7-139">For example, to include the `build` and `native` folders of a dependency, use the following:</span></span>

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

<span data-ttu-id="929c7-140">Chcete-li `content` `build` vyloučit složky a závislost, použijte následující:</span><span class="sxs-lookup"><span data-stu-id="929c7-140">To exclude the `content` and `build` folders of a dependency, use the following:</span></span>

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

## <a name="frameworks"></a><span data-ttu-id="929c7-141">Rozhraní</span><span class="sxs-lookup"><span data-stu-id="929c7-141">Frameworks</span></span>

<span data-ttu-id="929c7-142">Uvádí architektury, na kterých je `net45`projekt `netcoreapp` `netstandard`spuštěn, například , .</span><span class="sxs-lookup"><span data-stu-id="929c7-142">Lists the frameworks that the project runs on, such as `net45`, `netcoreapp`, `netstandard`.</span></span>

```json
"frameworks": {
    "netcore50": {}
    }
 ```

<span data-ttu-id="929c7-143">V `frameworks` sekci je povolena pouze jedna položka.</span><span class="sxs-lookup"><span data-stu-id="929c7-143">Only a single entry is allowed in the `frameworks` section.</span></span> <span data-ttu-id="929c7-144">(Výjimkou jsou `project.json` soubory pro ASP.NET projekty, které jsou vytvářeny se zastaralou řetězcem nástrojů DNX, která umožňuje více cílů.)</span><span class="sxs-lookup"><span data-stu-id="929c7-144">(An exception is `project.json` files for ASP.NET projects that are build with deprecated DNX tool chain, which allows for multiple targets.)</span></span>

## <a name="runtimes"></a><span data-ttu-id="929c7-145">Runtime</span><span class="sxs-lookup"><span data-stu-id="929c7-145">Runtimes</span></span>

<span data-ttu-id="929c7-146">Uvádí seznam operačních systémů a architektur, na `win10-arm` `win8-x64`kterých vaše aplikace běží, například , . `win8-x86`</span><span class="sxs-lookup"><span data-stu-id="929c7-146">Lists the operating systems and architectures that your app runs on, such as `win10-arm`, `win8-x64`, `win8-x86`.</span></span>

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

<span data-ttu-id="929c7-147">Balíček obsahující PCL, který lze spustit v libovolném běhu, nemusí zadávat za běhu.</span><span class="sxs-lookup"><span data-stu-id="929c7-147">A package containing a PCL that can run on any runtime doesn't need to specify a runtime.</span></span> <span data-ttu-id="929c7-148">To musí být také true všech závislostí, jinak je nutné zadat runtimes.</span><span class="sxs-lookup"><span data-stu-id="929c7-148">This must also be true of any dependencies, otherwise you must specify runtimes.</span></span>


## <a name="supports"></a><span data-ttu-id="929c7-149">Podporuje</span><span class="sxs-lookup"><span data-stu-id="929c7-149">Supports</span></span>

<span data-ttu-id="929c7-150">Definuje sadu kontrol pro závislosti balíčků.</span><span class="sxs-lookup"><span data-stu-id="929c7-150">Defines a set of checks for package dependencies.</span></span> <span data-ttu-id="929c7-151">Můžete definovat, kde očekáváte spuštění pcl nebo aplikace.</span><span class="sxs-lookup"><span data-stu-id="929c7-151">You can define where you expect the PCL or app to run.</span></span> <span data-ttu-id="929c7-152">Definice nejsou omezující, protože váš kód může být možné spustit jinde.</span><span class="sxs-lookup"><span data-stu-id="929c7-152">The definitions are not restrictive, as your code may be able to run elsewhere.</span></span> <span data-ttu-id="929c7-153">Ale zadání těchto kontrol způsobí, že NuGet zkontrolovat, že všechny závislosti jsou splněny na uvedených TxMs.</span><span class="sxs-lookup"><span data-stu-id="929c7-153">But specifying these checks makes NuGet check that all dependencies are satisfied on the listed TxMs.</span></span> <span data-ttu-id="929c7-154">Příklady hodnot pro `net46.app`tojsou: `uwp.10.0.app`, , atd.</span><span class="sxs-lookup"><span data-stu-id="929c7-154">Examples of the values for this are: `net46.app`, `uwp.10.0.app`, etc.</span></span>

<span data-ttu-id="929c7-155">Tato část by měla být vyplněna automaticky, když vyberete položku v dialogovém okně Cíle knihovny přenosných tříd.</span><span class="sxs-lookup"><span data-stu-id="929c7-155">This section should be populated automatically when you select an entry in the Portable Class Library targets dialog.</span></span>

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a><span data-ttu-id="929c7-156">Dovoz</span><span class="sxs-lookup"><span data-stu-id="929c7-156">Imports</span></span>

<span data-ttu-id="929c7-157">Importy jsou navrženy tak, `dotnet` aby balíčky, které používají TxM pracovat s balíčky, které nedeklarují dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="929c7-157">Imports are designed to allow packages that use the `dotnet` TxM to operate with packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="929c7-158">Pokud váš projekt `dotnet` používá TxM, pak všechny balíčky, `dotnet` na kterých jste závislí, `project.json` musí `dotnet` mít také TxM, pokud nepřidáte následující do vašeho, abyste umožnili kompatibilitu s neplatformami `dotnet`:</span><span class="sxs-lookup"><span data-stu-id="929c7-158">If your project is using the `dotnet` TxM then all the packages you depend on must also have a `dotnet` TxM, unless you add the following to your `project.json` to allow non `dotnet` platforms to be compatible with `dotnet`:</span></span>

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

<span data-ttu-id="929c7-159">Pokud používáte `dotnet` TxM, pak pcl projektový `imports` systém přidá příslušný příkaz založený na podporovaných cílech.</span><span class="sxs-lookup"><span data-stu-id="929c7-159">If you are using the `dotnet` TxM then the PCL project system adds the appropriate `imports` statement based on the supported targets.</span></span>

## <a name="differences-from-portable-apps-and-web-projects"></a><span data-ttu-id="929c7-160">Rozdíly od přenosných aplikací a webových projektů</span><span class="sxs-lookup"><span data-stu-id="929c7-160">Differences from portable apps and web projects</span></span>

<span data-ttu-id="929c7-161">Soubor `project.json` používaný NuGet je podmnožinou, která se nachází v ASP.NET základní projekty.</span><span class="sxs-lookup"><span data-stu-id="929c7-161">The `project.json` file used by NuGet is a subset of that found in ASP.NET Core projects.</span></span> <span data-ttu-id="929c7-162">V ASP.NET `project.json` Jádro se používá pro metadata projektu, informace kompilace a závislosti.</span><span class="sxs-lookup"><span data-stu-id="929c7-162">In ASP.NET Core `project.json` is used for project metadata, compilation information, and dependencies.</span></span> <span data-ttu-id="929c7-163">Při použití v jiných projektových systémech jsou tyto `project.json` tři věci rozděleny do samostatných souborů a obsahují méně informací.</span><span class="sxs-lookup"><span data-stu-id="929c7-163">When used in other project systems, those three things are split into separate files and `project.json` contains less information.</span></span> <span data-ttu-id="929c7-164">Mezi významné rozdíly patří:</span><span class="sxs-lookup"><span data-stu-id="929c7-164">Notable differences include:</span></span>

- <span data-ttu-id="929c7-165">V `frameworks` sekci může být pouze jeden rámec.</span><span class="sxs-lookup"><span data-stu-id="929c7-165">There can only be one framework in the `frameworks` section.</span></span>

- <span data-ttu-id="929c7-166">Soubor nemůže obsahovat závislosti, možnosti kompilace atd., `project.json` které vidíte v souborech DNX.</span><span class="sxs-lookup"><span data-stu-id="929c7-166">The file cannot contain dependencies, compilation options, etc. that you see in DNX `project.json` files.</span></span> <span data-ttu-id="929c7-167">Vzhledem k tomu, že může existovat pouze jeden rámec nemá smysl zadávat závislosti specifické pro architekturu.</span><span class="sxs-lookup"><span data-stu-id="929c7-167">Given that there can only be a single framework it doesn't make sense to enter framework-specific dependencies.</span></span>

- <span data-ttu-id="929c7-168">Kompilace je zpracována MSBuild, takže možnosti kompilace, preprocesor definuje, atd. `project.json`</span><span class="sxs-lookup"><span data-stu-id="929c7-168">Compilation is handled by MSBuild so compilation options, preprocessor defines, etc. are all part of the MSBuild project file and not `project.json`.</span></span>

<span data-ttu-id="929c7-169">V NuGet 3+ vývojáři se neočekává, `project.json`že ručně upravit , jako správce balíčků ujhává s obsahem.</span><span class="sxs-lookup"><span data-stu-id="929c7-169">In NuGet 3+, developers are not expected to manually edit the `project.json`, as the Package Manager UI in Visual Studio manipulates the content.</span></span> <span data-ttu-id="929c7-170">To znamená, že můžete určitě upravit soubor, ale musíte vytvořit projekt pro spuštění obnovení balíčku nebo vyvolání obnovení jiným způsobem.</span><span class="sxs-lookup"><span data-stu-id="929c7-170">That said, you can certainly edit the file, but you must build the project to start a package restore or invoke restore in another way.</span></span> <span data-ttu-id="929c7-171">Viz [Obnovení balíčku](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="929c7-171">See [Package restore](../consume-packages/package-restore.md).</span></span>


## <a name="projectlockjson"></a><span data-ttu-id="929c7-172">project.lock.json</span><span class="sxs-lookup"><span data-stu-id="929c7-172">project.lock.json</span></span>

<span data-ttu-id="929c7-173">Soubor `project.lock.json` je generován v procesu obnovení NuGet balíčky `project.json`v projektech, které používají .</span><span class="sxs-lookup"><span data-stu-id="929c7-173">The `project.lock.json` file is generated in the process of restoring the NuGet packages in projects that use `project.json`.</span></span> <span data-ttu-id="929c7-174">Obsahuje snímek všechny informace, které jsou generovány jako NuGet procházky grafu balíčků a zahrnuje verzi, obsah a závislosti všech balíčků v projektu.</span><span class="sxs-lookup"><span data-stu-id="929c7-174">It holds a snapshot of all the information that is generated as NuGet walks the graph of packages and includes the version, contents, and dependencies of all the packages in your project.</span></span> <span data-ttu-id="929c7-175">Systém sestavení používá k výběru balíčků z globálního umístění, které jsou relevantní při vytváření projektu namísto v závislosti na místní složky balíčků v samotném projektu.</span><span class="sxs-lookup"><span data-stu-id="929c7-175">The build system uses this to choose packages from a global location that are relevant when building the project instead of depending on a local packages folder in the project itself.</span></span> <span data-ttu-id="929c7-176">To má za následek rychlejší výkon sestavení, `project.lock.json` protože je `.nuspec` nutné číst pouze namísto mnoha samostatných souborů.</span><span class="sxs-lookup"><span data-stu-id="929c7-176">This results in faster build performance because it's necessary to read only `project.lock.json` instead of many separate `.nuspec` files.</span></span>

<span data-ttu-id="929c7-177">`project.lock.json`je automaticky generovánpři obnovení balíčku, takže jej lze vynechat ze `.gitignore` `.tfignore` správy zdrojového kódu přidáním a souborů (viz [Balíčky a správa zdrojového kódu](../consume-packages/packages-and-source-control.md).</span><span class="sxs-lookup"><span data-stu-id="929c7-177">`project.lock.json` is automatically generated on package restore, so it can be omitted from source control by adding it to `.gitignore` and `.tfignore` files (see [Packages and source control](../consume-packages/packages-and-source-control.md).</span></span> <span data-ttu-id="929c7-178">Pokud jej však zahrnete do správy zdrojového kódu, historie změn zobrazí změny v závislostech vyřešených v průběhu času.</span><span class="sxs-lookup"><span data-stu-id="929c7-178">However, if you include it in source control, the change history shows changes in dependencies resolved over time.</span></span>
