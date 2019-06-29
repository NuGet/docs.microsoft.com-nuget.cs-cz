---
title: Obsah archivu project.json NuGet
description: Různé části project.json obsah odstraněný z jiných oblastí dokumentace pro NuGet.
author: karann-msft
ms.author: karann
ms.date: 01/17/2018
ms.topic: conceptual
ms.openlocfilehash: d43f002b740b669de13f5872844ac0df97fc8fdc
ms.sourcegitcommit: b9a134a6e10d7d8502613f389f7d5f9b9e206ec8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67467787"
---
# <a name="projectjson-archive"></a><span data-ttu-id="b4f98-103">Archiv Project.JSON</span><span class="sxs-lookup"><span data-stu-id="b4f98-103">project.json archive</span></span>

<span data-ttu-id="b4f98-104">`project.json` Formátu správy byla zavedena v systému NuGet 3.x a používanou pro konkrétní typy projektů.</span><span class="sxs-lookup"><span data-stu-id="b4f98-104">The `project.json` management format was introduced with NuGet 3.x and used for certain project types.</span></span> <span data-ttu-id="b4f98-105">Se přestala nabízet, se zavedením PackageReference formát, ve kterém jsou uvedené závislosti přímo v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="b4f98-105">It was deprecated with the introduction of the PackageReference format, in which dependencies are listed directly in a project file.</span></span>

<span data-ttu-id="b4f98-106">Viz také:</span><span class="sxs-lookup"><span data-stu-id="b4f98-106">Also see:</span></span>

- [<span data-ttu-id="b4f98-107">project.json schema</span><span class="sxs-lookup"><span data-stu-id="b4f98-107">project.json schema</span></span>](project-json.md)
- [<span data-ttu-id="b4f98-108">dopad Project.JSON autory balíčku</span><span class="sxs-lookup"><span data-stu-id="b4f98-108">project.json impact on package authors</span></span>](project-json-impact.md)
- [<span data-ttu-id="b4f98-109">project.json a UPW</span><span class="sxs-lookup"><span data-stu-id="b4f98-109">project.json and UWP</span></span>](project-json-and-uwp.md)

## <a name="projectjson-management-format"></a><span data-ttu-id="b4f98-110">Formát souboru pro správu project.json</span><span class="sxs-lookup"><span data-stu-id="b4f98-110">project.json management format</span></span>

<span data-ttu-id="b4f98-111">*Původně v [obnovení balíčku](../what-is-nuget.md).*</span><span class="sxs-lookup"><span data-stu-id="b4f98-111">*Originally in [Package restore](../what-is-nuget.md).*</span></span>

<span data-ttu-id="b4f98-112">V seznamu management formáty:</span><span class="sxs-lookup"><span data-stu-id="b4f98-112">In the list of management formats:</span></span>

- <span data-ttu-id="b4f98-113">[`project.json`](project-json.md): *(zastaralé)* souboru A JSON, který udržuje seznam závislostí projektu s celkový graf balíčku v souboru přidružené `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="b4f98-113">[`project.json`](project-json.md): *(deprecated)* A JSON file that maintains a list of the project's dependencies with an overall package graph in an associated file, `project.lock.json`.</span></span> <span data-ttu-id="b4f98-114">Tento formát je zastaralé a místo toho použití PackageReference.</span><span class="sxs-lookup"><span data-stu-id="b4f98-114">This format is deprecated in favor of PackageReference.</span></span>

## <a name="nuget-restore-on-mono"></a><span data-ttu-id="b4f98-115">obnovení nuget v Mono</span><span class="sxs-lookup"><span data-stu-id="b4f98-115">nuget restore on Mono</span></span>

<span data-ttu-id="b4f98-116">*Původně v [klientských nástrojů Nugetu nainstalovat](../install-nuget-client-tools.md).*</span><span class="sxs-lookup"><span data-stu-id="b4f98-116">*Originally in [Install NuGet client tools](../install-nuget-client-tools.md).*</span></span>

<span data-ttu-id="b4f98-117">Funguje s `project.json`.</span><span class="sxs-lookup"><span data-stu-id="b4f98-117">Works with `project.json`.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="b4f98-118">Omezující verze balíčků pomocí obnovení</span><span class="sxs-lookup"><span data-stu-id="b4f98-118">Constraining package versions with restore</span></span>

<span data-ttu-id="b4f98-119">*Původně v [obnovení balíčku](../consume-packages/package-restore.md#constrain-package-versions-with-restore).*</span><span class="sxs-lookup"><span data-stu-id="b4f98-119">*Originally in [Package restore](../consume-packages/package-restore.md#constrain-package-versions-with-restore).*</span></span>

- <span data-ttu-id="b4f98-120">`project.json`: Přímo s číslem verze závislosti uvádět rozsah verzí.</span><span class="sxs-lookup"><span data-stu-id="b4f98-120">`project.json`: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="b4f98-121">Příklad:</span><span class="sxs-lookup"><span data-stu-id="b4f98-121">For example:</span></span>

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

## <a name="nuget-cli-commands"></a><span data-ttu-id="b4f98-122">Příkazy rozhraní příkazového řádku NuGet</span><span class="sxs-lookup"><span data-stu-id="b4f98-122">NuGet CLI commands</span></span>

- <span data-ttu-id="b4f98-123">`nuget install` nefunguje s `project.json`.</span><span class="sxs-lookup"><span data-stu-id="b4f98-123">`nuget install` does not work with `project.json`.</span></span>
- <span data-ttu-id="b4f98-124">`nuget restore`: pomocí projektů s použitím `project.json`, generuje `project.lock.json` souboru a `<project>.nuget.props` souboru, v případě potřeby.</span><span class="sxs-lookup"><span data-stu-id="b4f98-124">`nuget restore`: with projects using `project.json`, generates a `project.lock.json` file and a `<project>.nuget.props` file, if needed.</span></span> <span data-ttu-id="b4f98-125">(Oba soubory může vynechat ze správy zdrojového kódu.) `<projectPath>` Argument může odkazovat `project.json` souborů a má stejné chování jako odkazující `packages.config` nebo soubor projektu.</span><span class="sxs-lookup"><span data-stu-id="b4f98-125">(Both files can be omitted from source control.) The `<projectPath>` argument can point a `project.json` file and has the same behavior as pointing to a `packages.config` or project file.</span></span> <span data-ttu-id="b4f98-126">V pořadí podle priority pro složky balíčku `%userprofile%\.nuget\packages` prohledáván jako první při použití `project.json`.</span><span class="sxs-lookup"><span data-stu-id="b4f98-126">In the priority order for package folders, `%userprofile%\.nuget\packages` is searched first when using `project.json`.</span></span>
- <span data-ttu-id="b4f98-127">`nuget update`: V Mono, tento příkaz nefunguje s projekty pomocí `project.json`.</span><span class="sxs-lookup"><span data-stu-id="b4f98-127">`nuget update`: On Mono, this command does not work with projects using `project.json`.</span></span>

## <a name="dependency-resolution-with-packagereference"></a><span data-ttu-id="b4f98-128">Řešení závislostí s PackageReference</span><span class="sxs-lookup"><span data-stu-id="b4f98-128">Dependency resolution with PackageReference</span></span>

<span data-ttu-id="b4f98-129">*Původně v [řešení závislostí](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).*</span><span class="sxs-lookup"><span data-stu-id="b4f98-129">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).*</span></span>

<span data-ttu-id="b4f98-130">Chování PackageReference platí také pro `project.json`.</span><span class="sxs-lookup"><span data-stu-id="b4f98-130">The behavior of PackageReference applies also to `project.json`.</span></span> <span data-ttu-id="b4f98-131">Obnovení NuGet zapisuje do souboru s názvem grafu závislostí `project.lock.json` spolu s `project.json`.</span><span class="sxs-lookup"><span data-stu-id="b4f98-131">NuGet restore writes the dependency graph into a file named `project.lock.json` alongside `project.json`.</span></span>

## <a name="managing-dependency-assets"></a><span data-ttu-id="b4f98-132">Správa závislostí prostředky</span><span class="sxs-lookup"><span data-stu-id="b4f98-132">Managing dependency assets</span></span>

<span data-ttu-id="b4f98-133">*Původně v [řešení závislostí](../consume-packages/dependency-resolution.md#managing-dependency-assets).*</span><span class="sxs-lookup"><span data-stu-id="b4f98-133">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#managing-dependency-assets).*</span></span>

<span data-ttu-id="b4f98-134">Při použití `project.json` formátu, můžete určit, jaké prostředky z toku závislostí do nejvyšší úrovně projektu.</span><span class="sxs-lookup"><span data-stu-id="b4f98-134">When using the `project.json` format, you can control which assets from dependencies flow into the top-level project.</span></span> <span data-ttu-id="b4f98-135">Podrobnosti najdete v tématu [project.json](project-json.md).</span><span class="sxs-lookup"><span data-stu-id="b4f98-135">For details, see [project.json](project-json.md).</span></span>

## <a name="excluding-references"></a><span data-ttu-id="b4f98-136">Kromě odkazů</span><span class="sxs-lookup"><span data-stu-id="b4f98-136">Excluding references</span></span>

<span data-ttu-id="b4f98-137">*Původně v [řešení závislostí](../consume-packages/dependency-resolution.md#excluding-references).*</span><span class="sxs-lookup"><span data-stu-id="b4f98-137">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#excluding-references).*</span></span>

- <span data-ttu-id="b4f98-138">`project.json`: přidání `"exclude" : "all"` v závislostí pro PackageC:</span><span class="sxs-lookup"><span data-stu-id="b4f98-138">`project.json`: add `"exclude" : "all"` in the dependency for PackageC:</span></span>

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

## <a name="resolving-incompatible-package-errors"></a><span data-ttu-id="b4f98-139">Řešení chyb nekompatibilní balíček</span><span class="sxs-lookup"><span data-stu-id="b4f98-139">Resolving incompatible package errors</span></span>

<span data-ttu-id="b4f98-140">*Původně v [řešení závislostí](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors).*</span><span class="sxs-lookup"><span data-stu-id="b4f98-140">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors).*</span></span>

<span data-ttu-id="b4f98-141">Přidání prostředků řešení chyb:</span><span class="sxs-lookup"><span data-stu-id="b4f98-141">An added means of resolving errors:</span></span>

- <span data-ttu-id="b4f98-142">**Není doporučeno**: jako dočasné řešení při práci s autora balíčku projekty cílení `netcore`, `netstandard`, a `netcoreapp` označit jako kompatibilní, což balíčky cílí na ty ostatní platformy Další architektury, který se má použít.</span><span class="sxs-lookup"><span data-stu-id="b4f98-142">**Not recommended**: as a temporary solution while you work with the package author, projects targeting `netcore`, `netstandard`, and `netcoreapp` can denote other frameworks as being compatible, thereby allowing packages targeting those other frameworks to be used.</span></span> <span data-ttu-id="b4f98-143">Zobrazit [project.json importuje](project-json.md#imports) a [cíl obnovení nástroje MSBuild PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback).</span><span class="sxs-lookup"><span data-stu-id="b4f98-143">See [project.json imports](project-json.md#imports) and [MSBuild restore target PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback).</span></span> <span data-ttu-id="b4f98-144">To může způsobit neočekávané chování, proto znovu, je nejlepší řešení nekompatibility balíček při práci s autora balíčku na aktualizace.</span><span class="sxs-lookup"><span data-stu-id="b4f98-144">This can cause unexpected behaviors, so again, it's best to resolve package incompatibilities by working with the package author on an update.</span></span>

## <a name="target-frameworks"></a><span data-ttu-id="b4f98-145">Cílové architektury</span><span class="sxs-lookup"><span data-stu-id="b4f98-145">Target frameworks</span></span>

<span data-ttu-id="b4f98-146">*Původně v [platforem](../reference/target-frameworks.md).*</span><span class="sxs-lookup"><span data-stu-id="b4f98-146">*Originally in [Target frameworks](../reference/target-frameworks.md).*</span></span>

- <span data-ttu-id="b4f98-147">[project.json](project-json.md): `frameworks` Uzlu určuje verze rozhraní framework projektu může být zkompilována proti.</span><span class="sxs-lookup"><span data-stu-id="b4f98-147">[project.json](project-json.md): The `frameworks` node specifies the framework versions that the project can be compiled against.</span></span>

## <a name="creating-a-package"></a><span data-ttu-id="b4f98-148">Vytvoření balíčku</span><span class="sxs-lookup"><span data-stu-id="b4f98-148">Creating a package</span></span>

<span data-ttu-id="b4f98-149">*Původně v [vytvoření balíčku](../create-packages/creating-a-package.md)*</span><span class="sxs-lookup"><span data-stu-id="b4f98-149">*Originally in [Creating a package](../create-packages/creating-a-package.md)*</span></span>

### <a name="setting-a-package-type"></a><span data-ttu-id="b4f98-150">Nastavení typ balíčku</span><span class="sxs-lookup"><span data-stu-id="b4f98-150">Setting a package type</span></span>

<span data-ttu-id="b4f98-151">S .NET Core 1.x, když DotnetCliTool balíček nainstalován, Visual Studio umístí v balíčku `project.json` `tools` uzel místo `dependencies` uzlu.</span><span class="sxs-lookup"><span data-stu-id="b4f98-151">With .NET Core 1.x, when a DotnetCliTool package is installed, Visual Studio places the package in the `project.json` `tools` node instead of the `dependencies` node.</span></span>

<span data-ttu-id="b4f98-152">Balíček typy mají nastavený `project.json`.</span><span class="sxs-lookup"><span data-stu-id="b4f98-152">Package types are set in `project.json`.</span></span>

- <span data-ttu-id="b4f98-153">`project.json`: Označuje typ balíčku v rámci `packOptions.packageType` vlastnosti json:</span><span class="sxs-lookup"><span data-stu-id="b4f98-153">`project.json`: Indicate the package type within a `packOptions.packageType` property json:</span></span>

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

### <a name="adding-targets-and-props-for-msbuild"></a><span data-ttu-id="b4f98-154">Přidání cíle a vlastnosti pro MSBuild</span><span class="sxs-lookup"><span data-stu-id="b4f98-154">Adding targets and props for MSBuild</span></span>

<span data-ttu-id="b4f98-155">*Původně v [vytvořit balíčky .NET NuGet standardní pomocí sady Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*</span><span class="sxs-lookup"><span data-stu-id="b4f98-155">*Originally in [Create .NET Standard NuGet Packages with Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*</span></span>

<span data-ttu-id="b4f98-156">Při použití `project.json`, cíle nebyly přidány do projektu, ale jsou k dispozici prostřednictvím `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="b4f98-156">When using `project.json`, targets are not added to the project but are made available through the `project.lock.json`.</span></span>

### <a name="package-versioning"></a><span data-ttu-id="b4f98-157">Správa verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="b4f98-157">Package versioning</span></span>

<span data-ttu-id="b4f98-158">*Původně v [Správa verzí balíčků](../reference/package-versioning.md).*</span><span class="sxs-lookup"><span data-stu-id="b4f98-158">*Originally in [Package versioning](../reference/package-versioning.md).*</span></span>

<span data-ttu-id="b4f98-159">Při použití `project.json` formátování, NuGet také podporuje notaci zástupný znak, \*pro hlavní, vedlejší, opravy a příponu předběžné verze část čísla.</span><span class="sxs-lookup"><span data-stu-id="b4f98-159">When using the `project.json` format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span>

### <a name="nugetconfig-reference"></a><span data-ttu-id="b4f98-160">Odkaz na soubor NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="b4f98-160">NuGet.Config reference</span></span>

<span data-ttu-id="b4f98-161">*Původně v [odkaz na soubor NuGet.Config](../reference/nuget-config-file.md).*</span><span class="sxs-lookup"><span data-stu-id="b4f98-161">*Originally in [NuGet.Config reference](../reference/nuget-config-file.md).*</span></span>

<span data-ttu-id="b4f98-162">`globalPackagesFolder` platí jenom pro `project.json`.</span><span class="sxs-lookup"><span data-stu-id="b4f98-162">`globalPackagesFolder` applies only to `project.json`.</span></span> <span data-ttu-id="b4f98-163">(Přidání poznámky: platí také pro PackageReference.)</span><span class="sxs-lookup"><span data-stu-id="b4f98-163">(Added note: also applies to PackageReference.)</span></span>

### <a name="nuspec-file-reference"></a><span data-ttu-id="b4f98-164">odkaz na soubor nuspec</span><span class="sxs-lookup"><span data-stu-id="b4f98-164">nuspec file reference</span></span>

<span data-ttu-id="b4f98-165">*Původně v [odkaz na soubor nuspec](../reference/nuspec.md).*</span><span class="sxs-lookup"><span data-stu-id="b4f98-165">*Originally in [nuspec reference](../reference/nuspec.md).*</span></span>

<span data-ttu-id="b4f98-166">`<contentFiles>` Element se použije namísto `<files>` s `project.json`.</span><span class="sxs-lookup"><span data-stu-id="b4f98-166">The `<contentFiles>` element is used instead of `<files>` with `project.json`.</span></span>

### <a name="package-manager-options-control"></a><span data-ttu-id="b4f98-167">Ovládací prvek možnosti Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="b4f98-167">Package manager options control</span></span>

<span data-ttu-id="b4f98-168">*Původně v [Reference k uživatelskému rozhraní Správce balíčků](../tools/package-manager-ui.md).*</span><span class="sxs-lookup"><span data-stu-id="b4f98-168">*Originally in [Package Manager UI reference](../tools/package-manager-ui.md).*</span></span>

<span data-ttu-id="b4f98-169">Projekty pomocí `project.json` správu formátu zobrazit pouze **zobrazit okno náhledu** možnost.</span><span class="sxs-lookup"><span data-stu-id="b4f98-169">Projects using `project.json` management format show only the **Show preview window** option.</span></span>

### <a name="visual-studio-templates"></a><span data-ttu-id="b4f98-170">Šablony aplikace Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b4f98-170">Visual Studio Templates</span></span>

<span data-ttu-id="b4f98-171">*Původně v [balíčky NuGet v sadě Visual Studio šablony](../visual-studio-extensibility/visual-studio-templates.md).*</span><span class="sxs-lookup"><span data-stu-id="b4f98-171">*Originally in [NuGet Packages in Visual Studio templates](../visual-studio-extensibility/visual-studio-templates.md).*</span></span>

<span data-ttu-id="b4f98-172">Osvědčené postupy: šablony nezahrnují `project.json` souboru a nezahrnuje nebo odkazy nebo obsah, který se přidá při instalaci balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="b4f98-172">Best practices: templates do not include a `project.json` file, and do not include or any references or content that would be added when NuGet packages are installed.</span></span>