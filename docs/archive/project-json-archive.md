---
title: Obsah archivu Project. JSON pro NuGet
description: Různé bity obsahu Project. JSON se odebraly z jiných oblastí dokumentace k NuGetu.
author: karann-msft
ms.author: karann
ms.date: 01/17/2018
ms.topic: conceptual
ms.openlocfilehash: 8d732e87f01c55bde87da0a2e382fd6d509886a3
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317015"
---
# <a name="projectjson-archive"></a><span data-ttu-id="fca62-103">Archiv Project. JSON</span><span class="sxs-lookup"><span data-stu-id="fca62-103">project.json archive</span></span>

<span data-ttu-id="fca62-104">Formát `project.json` správy byl představen s NuGet 3. x a používá se pro určité typy projektů.</span><span class="sxs-lookup"><span data-stu-id="fca62-104">The `project.json` management format was introduced with NuGet 3.x and used for certain project types.</span></span> <span data-ttu-id="fca62-105">Byla zastaralá s představením formátu PackageReference, ve kterém jsou závislosti uvedeny přímo v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="fca62-105">It was deprecated with the introduction of the PackageReference format, in which dependencies are listed directly in a project file.</span></span>

<span data-ttu-id="fca62-106">Viz také:</span><span class="sxs-lookup"><span data-stu-id="fca62-106">Also see:</span></span>

- [<span data-ttu-id="fca62-107">project.json schema</span><span class="sxs-lookup"><span data-stu-id="fca62-107">project.json schema</span></span>](project-json.md)
- [<span data-ttu-id="fca62-108">dopad Project. JSON na autory balíčku</span><span class="sxs-lookup"><span data-stu-id="fca62-108">project.json impact on package authors</span></span>](project-json-impact.md)
- [<span data-ttu-id="fca62-109">project.json a UPW</span><span class="sxs-lookup"><span data-stu-id="fca62-109">project.json and UWP</span></span>](project-json-and-uwp.md)

## <a name="projectjson-management-format"></a><span data-ttu-id="fca62-110">Formát souboru pro správu project.json</span><span class="sxs-lookup"><span data-stu-id="fca62-110">project.json management format</span></span>

<span data-ttu-id="fca62-111">*Původně v [balíčku pro obnovení](../what-is-nuget.md).*</span><span class="sxs-lookup"><span data-stu-id="fca62-111">*Originally in [Package restore](../what-is-nuget.md).*</span></span>

<span data-ttu-id="fca62-112">V seznamu formátů správy:</span><span class="sxs-lookup"><span data-stu-id="fca62-112">In the list of management formats:</span></span>

- <span data-ttu-id="fca62-113">[`project.json`](project-json.md): *(nepoužívané)* soubor JSON, který uchovává seznam závislostí projektu s celkovým grafem balíčku v přidruženém souboru `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="fca62-113">[`project.json`](project-json.md): *(deprecated)* A JSON file that maintains a list of the project's dependencies with an overall package graph in an associated file, `project.lock.json`.</span></span> <span data-ttu-id="fca62-114">Tento formát je zastaralý a má přednost před PackageReference.</span><span class="sxs-lookup"><span data-stu-id="fca62-114">This format is deprecated in favor of PackageReference.</span></span>

## <a name="nuget-restore-on-mono"></a><span data-ttu-id="fca62-115">obnovení nugetu na mono</span><span class="sxs-lookup"><span data-stu-id="fca62-115">nuget restore on Mono</span></span>

<span data-ttu-id="fca62-116">*Původně se [nainstalovaly klientské nástroje NuGet](../install-nuget-client-tools.md).*</span><span class="sxs-lookup"><span data-stu-id="fca62-116">*Originally in [Install NuGet client tools](../install-nuget-client-tools.md).*</span></span>

<span data-ttu-id="fca62-117">Pracuje s `project.json`.</span><span class="sxs-lookup"><span data-stu-id="fca62-117">Works with `project.json`.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="fca62-118">Omezení verzí balíčku s obnovením</span><span class="sxs-lookup"><span data-stu-id="fca62-118">Constraining package versions with restore</span></span>

<span data-ttu-id="fca62-119">*Původně v [balíčku pro obnovení](../consume-packages/package-restore.md#constrain-package-versions-with-restore).*</span><span class="sxs-lookup"><span data-stu-id="fca62-119">*Originally in [Package restore](../consume-packages/package-restore.md#constrain-package-versions-with-restore).*</span></span>

- <span data-ttu-id="fca62-120">`project.json`: Zadejte rozsah verzí přímo s číslem verze závislosti.</span><span class="sxs-lookup"><span data-stu-id="fca62-120">`project.json`: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="fca62-121">Příklad:</span><span class="sxs-lookup"><span data-stu-id="fca62-121">For example:</span></span>

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

## <a name="nuget-cli-commands"></a><span data-ttu-id="fca62-122">Příkazy NuGet CLI</span><span class="sxs-lookup"><span data-stu-id="fca62-122">NuGet CLI commands</span></span>

- <span data-ttu-id="fca62-123">`nuget install`nefunguje s `project.json`.</span><span class="sxs-lookup"><span data-stu-id="fca62-123">`nuget install` does not work with `project.json`.</span></span>
- <span data-ttu-id="fca62-124">`nuget restore`: s projekty používající `project.json`, `project.lock.json` vygeneruje v případě potřeby `<project>.nuget.props` soubor a soubor.</span><span class="sxs-lookup"><span data-stu-id="fca62-124">`nuget restore`: with projects using `project.json`, generates a `project.lock.json` file and a `<project>.nuget.props` file, if needed.</span></span> <span data-ttu-id="fca62-125">(Oba soubory mohou být vynechány ze správy zdrojového kódu.) Argument může odkazovat na soubor a má stejné `packages.config` chování jako odkazuje na soubor projektu nebo. `project.json` `<projectPath>`</span><span class="sxs-lookup"><span data-stu-id="fca62-125">(Both files can be omitted from source control.) The `<projectPath>` argument can point a `project.json` file and has the same behavior as pointing to a `packages.config` or project file.</span></span> <span data-ttu-id="fca62-126">V pořadí podle priority pro složky `%userprofile%\.nuget\packages` balíčku se při použití `project.json`prohledává jako první.</span><span class="sxs-lookup"><span data-stu-id="fca62-126">In the priority order for package folders, `%userprofile%\.nuget\packages` is searched first when using `project.json`.</span></span>
- <span data-ttu-id="fca62-127">`nuget update`: V mono tento příkaz nefunguje s projekty pomocí `project.json`.</span><span class="sxs-lookup"><span data-stu-id="fca62-127">`nuget update`: On Mono, this command does not work with projects using `project.json`.</span></span>

## <a name="dependency-resolution-with-packagereference"></a><span data-ttu-id="fca62-128">Rozlišení závislosti s PackageReference</span><span class="sxs-lookup"><span data-stu-id="fca62-128">Dependency resolution with PackageReference</span></span>

<span data-ttu-id="fca62-129">*Původně v [řešení závislostí](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).*</span><span class="sxs-lookup"><span data-stu-id="fca62-129">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).*</span></span>

<span data-ttu-id="fca62-130">Chování PackageReference se vztahuje také na `project.json`.</span><span class="sxs-lookup"><span data-stu-id="fca62-130">The behavior of PackageReference applies also to `project.json`.</span></span> <span data-ttu-id="fca62-131">NuGet Restore uloží graf závislosti do souboru s názvem `project.lock.json` společně `project.json`.</span><span class="sxs-lookup"><span data-stu-id="fca62-131">NuGet restore writes the dependency graph into a file named `project.lock.json` alongside `project.json`.</span></span>

## <a name="managing-dependency-assets"></a><span data-ttu-id="fca62-132">Správa prostředků závislosti</span><span class="sxs-lookup"><span data-stu-id="fca62-132">Managing dependency assets</span></span>

<span data-ttu-id="fca62-133">*Původně v [řešení závislostí](../consume-packages/dependency-resolution.md#managing-dependency-assets).*</span><span class="sxs-lookup"><span data-stu-id="fca62-133">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#managing-dependency-assets).*</span></span>

<span data-ttu-id="fca62-134">Při použití `project.json` formátu můžete řídit, které prostředky se mají směrovat do projektu nejvyšší úrovně.</span><span class="sxs-lookup"><span data-stu-id="fca62-134">When using the `project.json` format, you can control which assets from dependencies flow into the top-level project.</span></span> <span data-ttu-id="fca62-135">Podrobnosti naleznete v tématu [Project. JSON](project-json.md).</span><span class="sxs-lookup"><span data-stu-id="fca62-135">For details, see [project.json](project-json.md).</span></span>

## <a name="excluding-references"></a><span data-ttu-id="fca62-136">Vyloučení odkazů</span><span class="sxs-lookup"><span data-stu-id="fca62-136">Excluding references</span></span>

<span data-ttu-id="fca62-137">*Původně v [řešení závislostí](../consume-packages/dependency-resolution.md#excluding-references).*</span><span class="sxs-lookup"><span data-stu-id="fca62-137">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#excluding-references).*</span></span>

- <span data-ttu-id="fca62-138">`project.json`: přidejte `"exclude" : "all"` v závislosti pro PackageC:</span><span class="sxs-lookup"><span data-stu-id="fca62-138">`project.json`: add `"exclude" : "all"` in the dependency for PackageC:</span></span>

    ```json
    {
        "dependencies": {
            "PackageC": {
            "version": "1.0.0",
            "exclude": "all"
            }
        }
    }
    ```

## <a name="resolving-incompatible-package-errors"></a><span data-ttu-id="fca62-139">Řešení chyb nekompatibilních balíčků</span><span class="sxs-lookup"><span data-stu-id="fca62-139">Resolving incompatible package errors</span></span>

<span data-ttu-id="fca62-140">*Původně v [řešení závislostí](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors).*</span><span class="sxs-lookup"><span data-stu-id="fca62-140">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors).*</span></span>

<span data-ttu-id="fca62-141">Přidaný způsob řešení chyb:</span><span class="sxs-lookup"><span data-stu-id="fca62-141">An added means of resolving errors:</span></span>

- <span data-ttu-id="fca62-142">**Nedoporučuje**se: jako dočasné řešení, když pracujete s autorem balíčku, projekty `netcore`, `netstandard`které cílí `netcoreapp` na, a můžou navšimnout dalších platforem jako kompatibility, takže balíčky cílí na tyto jiné. rozhraní, která se mají použít.</span><span class="sxs-lookup"><span data-stu-id="fca62-142">**Not recommended**: as a temporary solution while you work with the package author, projects targeting `netcore`, `netstandard`, and `netcoreapp` can denote other frameworks as being compatible, thereby allowing packages targeting those other frameworks to be used.</span></span> <span data-ttu-id="fca62-143">Viz [importy Project. JSON](project-json.md#imports) a [PackageTargetFallback cíl obnovení nástroje MSBuild](../reference/msbuild-targets.md#packagetargetfallback).</span><span class="sxs-lookup"><span data-stu-id="fca62-143">See [project.json imports](project-json.md#imports) and [MSBuild restore target PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback).</span></span> <span data-ttu-id="fca62-144">To může způsobit neočekávané chování, takže znovu je vhodné vyřešit nekompatibilitu balíčků pomocí práce s autorem balíčku při aktualizaci.</span><span class="sxs-lookup"><span data-stu-id="fca62-144">This can cause unexpected behaviors, so again, it's best to resolve package incompatibilities by working with the package author on an update.</span></span>

## <a name="target-frameworks"></a><span data-ttu-id="fca62-145">Cílové architektury</span><span class="sxs-lookup"><span data-stu-id="fca62-145">Target frameworks</span></span>

<span data-ttu-id="fca62-146">*Původně v [cílových rozhraních](../reference/target-frameworks.md).*</span><span class="sxs-lookup"><span data-stu-id="fca62-146">*Originally in [Target frameworks](../reference/target-frameworks.md).*</span></span>

- <span data-ttu-id="fca62-147">[project.json](project-json.md): `frameworks` Uzel Určuje verze rozhraní, pro které může být projekt zkompilován.</span><span class="sxs-lookup"><span data-stu-id="fca62-147">[project.json](project-json.md): The `frameworks` node specifies the framework versions that the project can be compiled against.</span></span>

## <a name="creating-a-package"></a><span data-ttu-id="fca62-148">Vytvoření balíčku</span><span class="sxs-lookup"><span data-stu-id="fca62-148">Creating a package</span></span>

<span data-ttu-id="fca62-149">*Původně v [vytváření balíčku](../create-packages/creating-a-package.md)*</span><span class="sxs-lookup"><span data-stu-id="fca62-149">*Originally in [Creating a package](../create-packages/creating-a-package.md)*</span></span>

### <a name="setting-a-package-type"></a><span data-ttu-id="fca62-150">Nastavení typu balíčku</span><span class="sxs-lookup"><span data-stu-id="fca62-150">Setting a package type</span></span>

<span data-ttu-id="fca62-151">Pokud je v rozhraní .NET Core 1. x nainstalován balíček DotnetCliTool, sada Visual Studio umístí balíček místo `project.json` `dependencies` uzlu do `tools` uzlu.</span><span class="sxs-lookup"><span data-stu-id="fca62-151">With .NET Core 1.x, when a DotnetCliTool package is installed, Visual Studio places the package in the `project.json` `tools` node instead of the `dependencies` node.</span></span>

<span data-ttu-id="fca62-152">Typy balíčků jsou nastaveny v `project.json`.</span><span class="sxs-lookup"><span data-stu-id="fca62-152">Package types are set in `project.json`.</span></span>

- <span data-ttu-id="fca62-153">`project.json`: Určete typ balíčku v rámci `packOptions.packageType` JSON vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="fca62-153">`project.json`: Indicate the package type within a `packOptions.packageType` property json:</span></span>

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

### <a name="adding-targets-and-props-for-msbuild"></a><span data-ttu-id="fca62-154">Přidání cílů a vlastností pro MSBuild</span><span class="sxs-lookup"><span data-stu-id="fca62-154">Adding targets and props for MSBuild</span></span>

<span data-ttu-id="fca62-155">*Původně v [rámci vytváření .NET Standard balíčků NuGet pomocí sady Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*</span><span class="sxs-lookup"><span data-stu-id="fca62-155">*Originally in [Create .NET Standard NuGet Packages with Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*</span></span>

<span data-ttu-id="fca62-156">Při použití `project.json`nejsou cíle přidány do projektu, ale jsou zpřístupněny `project.lock.json`prostřednictvím.</span><span class="sxs-lookup"><span data-stu-id="fca62-156">When using `project.json`, targets are not added to the project but are made available through the `project.lock.json`.</span></span>

### <a name="package-versioning"></a><span data-ttu-id="fca62-157">Správa verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="fca62-157">Package versioning</span></span>

<span data-ttu-id="fca62-158">*Původně ve [verzi balíčku](../reference/package-versioning.md).*</span><span class="sxs-lookup"><span data-stu-id="fca62-158">*Originally in [Package versioning](../reference/package-versioning.md).*</span></span>

<span data-ttu-id="fca62-159">Při použití `project.json` formátu NuGet podporuje také použití zástupných znaků \*, v případě částí čísla hlavní, dílčí, opravné a předběžné verze.</span><span class="sxs-lookup"><span data-stu-id="fca62-159">When using the `project.json` format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span>

### <a name="nugetconfig-reference"></a><span data-ttu-id="fca62-160">Referenční dokumentace NuGet. config</span><span class="sxs-lookup"><span data-stu-id="fca62-160">NuGet.Config reference</span></span>

<span data-ttu-id="fca62-161">*Původně v [odkazu NuGet. config](../reference/nuget-config-file.md).*</span><span class="sxs-lookup"><span data-stu-id="fca62-161">*Originally in [NuGet.Config reference](../reference/nuget-config-file.md).*</span></span>

<span data-ttu-id="fca62-162">`globalPackagesFolder`platí pouze pro `project.json`.</span><span class="sxs-lookup"><span data-stu-id="fca62-162">`globalPackagesFolder` applies only to `project.json`.</span></span> <span data-ttu-id="fca62-163">(Přidání poznámky: platí také pro PackageReference.)</span><span class="sxs-lookup"><span data-stu-id="fca62-163">(Added note: also applies to PackageReference.)</span></span>

### <a name="nuspec-file-reference"></a><span data-ttu-id="fca62-164">odkaz na soubor nuspec</span><span class="sxs-lookup"><span data-stu-id="fca62-164">nuspec file reference</span></span>

<span data-ttu-id="fca62-165">*Původně v [nuspec reference](../reference/nuspec.md).*</span><span class="sxs-lookup"><span data-stu-id="fca62-165">*Originally in [nuspec reference](../reference/nuspec.md).*</span></span>

<span data-ttu-id="fca62-166">Element je použit `<files>` místo s `project.json`. `<contentFiles>`</span><span class="sxs-lookup"><span data-stu-id="fca62-166">The `<contentFiles>` element is used instead of `<files>` with `project.json`.</span></span>

### <a name="package-manager-options-control"></a><span data-ttu-id="fca62-167">Řízení možností Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="fca62-167">Package manager options control</span></span>

<span data-ttu-id="fca62-168">*Původně v [odkazu na uživatelské rozhraní Správce balíčků](../consume-packages/install-use-packages-visual-studio.md).*</span><span class="sxs-lookup"><span data-stu-id="fca62-168">*Originally in [Package Manager UI reference](../consume-packages/install-use-packages-visual-studio.md).*</span></span>

<span data-ttu-id="fca62-169">Projekty, `project.json` které používají formát správy, zobrazují pouze možnost **Zobrazit okno náhledu** .</span><span class="sxs-lookup"><span data-stu-id="fca62-169">Projects using `project.json` management format show only the **Show preview window** option.</span></span>

### <a name="visual-studio-templates"></a><span data-ttu-id="fca62-170">Šablony aplikace Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fca62-170">Visual Studio Templates</span></span>

<span data-ttu-id="fca62-171">*Původně v [balíčcích NuGet v šablonách sady Visual Studio](../visual-studio-extensibility/visual-studio-templates.md).*</span><span class="sxs-lookup"><span data-stu-id="fca62-171">*Originally in [NuGet Packages in Visual Studio templates](../visual-studio-extensibility/visual-studio-templates.md).*</span></span>

<span data-ttu-id="fca62-172">Osvědčené postupy: šablony `project.json` neobsahují soubor a neobsahují ani žádné odkazy nebo obsah, které by se přidaly při instalaci balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="fca62-172">Best practices: templates do not include a `project.json` file, and do not include or any references or content that would be added when NuGet packages are installed.</span></span>