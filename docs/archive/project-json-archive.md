---
title: Obsah archivu project.json NuGet
description: Různé bity project.json obsah byl odebrán z jiných oblastí v dokumentaci NuGet.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/17/2018
ms.topic: conceptual
ms.openlocfilehash: cd0f4bc44c1acaeed3b3ed0241c501ddd281628d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
---
# <a name="projectjson-archive"></a><span data-ttu-id="fa1f0-103">Project.JSON archivu</span><span class="sxs-lookup"><span data-stu-id="fa1f0-103">project.json archive</span></span>

<span data-ttu-id="fa1f0-104">`project.json` Formátu správy byla zavedena v systému NuGet 3.x a použít pro určité typy projektů.</span><span class="sxs-lookup"><span data-stu-id="fa1f0-104">The `project.json` management format was introduced with NuGet 3.x and used for certain project types.</span></span> <span data-ttu-id="fa1f0-105">Byl již nepoužívá, se zavedením PackageReference formát, ve kterém jsou uvedeny závislosti přímo v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="fa1f0-105">It was deprecated with the introduction of the PackageReference format, in which dependencies are listed directly in a project file.</span></span>

<span data-ttu-id="fa1f0-106">Viz také:</span><span class="sxs-lookup"><span data-stu-id="fa1f0-106">Also see:</span></span>

- [<span data-ttu-id="fa1f0-107">project.json schema</span><span class="sxs-lookup"><span data-stu-id="fa1f0-107">project.json schema</span></span>](project-json.md)
- [<span data-ttu-id="fa1f0-108">Project.JSON dopad na autoři balíčku</span><span class="sxs-lookup"><span data-stu-id="fa1f0-108">project.json impact on package authors</span></span>](project-json-impact.md)
- [<span data-ttu-id="fa1f0-109">project.json a UPW</span><span class="sxs-lookup"><span data-stu-id="fa1f0-109">project.json and UWP</span></span>](project-json-and-uwp.md)

## <a name="projectjson-management-format"></a><span data-ttu-id="fa1f0-110">Formát souboru Project.JSON správy</span><span class="sxs-lookup"><span data-stu-id="fa1f0-110">project.json management format</span></span>

<span data-ttu-id="fa1f0-111">*Původně v [obnovení balíčků](../what-is-nuget.md).*</span><span class="sxs-lookup"><span data-stu-id="fa1f0-111">*Originally in [Package restore](../what-is-nuget.md).*</span></span>

<span data-ttu-id="fa1f0-112">V seznamu správy formátů:</span><span class="sxs-lookup"><span data-stu-id="fa1f0-112">In the list of management formats:</span></span>

- <span data-ttu-id="fa1f0-113">[`project.json`](project-json.md): *(nepoužívané)* A JSON soubor, který udržuje seznam závislosti projektu s celkové balíček grafu v přidružený soubor, `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="fa1f0-113">[`project.json`](project-json.md): *(deprecated)* A JSON file that maintains a list of the project's dependencies with an overall package graph in an associated file, `project.lock.json`.</span></span> <span data-ttu-id="fa1f0-114">Tento formát je zastaralý považuje PackageReference.</span><span class="sxs-lookup"><span data-stu-id="fa1f0-114">This format is deprecated in favor of PackageReference.</span></span>

## <a name="nuget-restore-on-mono"></a><span data-ttu-id="fa1f0-115">nuget restore na Mono</span><span class="sxs-lookup"><span data-stu-id="fa1f0-115">nuget restore on Mono</span></span>

<span data-ttu-id="fa1f0-116">*Původně v [nástrojích klienta nainstalovat NuGet](../install-nuget-client-tools.md).*</span><span class="sxs-lookup"><span data-stu-id="fa1f0-116">*Originally in [Install NuGet client tools](../install-nuget-client-tools.md).*</span></span>

<span data-ttu-id="fa1f0-117">Funguje s `project.json`.</span><span class="sxs-lookup"><span data-stu-id="fa1f0-117">Works with `project.json`.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="fa1f0-118">Omezení verze balíčku s obnovením</span><span class="sxs-lookup"><span data-stu-id="fa1f0-118">Constraining package versions with restore</span></span>

<span data-ttu-id="fa1f0-119">*Původně v [obnovení balíčků](../consume-packages/package-restore.md#constraining-package-versions-with-restore).*</span><span class="sxs-lookup"><span data-stu-id="fa1f0-119">*Originally in [Package restore](../consume-packages/package-restore.md#constraining-package-versions-with-restore).*</span></span>

- <span data-ttu-id="fa1f0-120">`project.json`: Určete rozsah verze přímo s číslem verze této závislosti.</span><span class="sxs-lookup"><span data-stu-id="fa1f0-120">`project.json`: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="fa1f0-121">Příklad:</span><span class="sxs-lookup"><span data-stu-id="fa1f0-121">For example:</span></span>

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

## <a name="nuget-cli-commands"></a><span data-ttu-id="fa1f0-122">NuGet rozhraní příkazového řádku</span><span class="sxs-lookup"><span data-stu-id="fa1f0-122">NuGet CLI commands</span></span>

- <span data-ttu-id="fa1f0-123">`nuget install` nefunguje s `project.json`.</span><span class="sxs-lookup"><span data-stu-id="fa1f0-123">`nuget install` does not work with `project.json`.</span></span>
- <span data-ttu-id="fa1f0-124">`nuget restore`: pomocí projektů pomocí `project.json`, generuje `project.lock.json` souboru a `<project>.nuget.props` souborů, v případě potřeby.</span><span class="sxs-lookup"><span data-stu-id="fa1f0-124">`nuget restore`: with projects using `project.json`, generates a `project.lock.json` file and a `<project>.nuget.props` file, if needed.</span></span> <span data-ttu-id="fa1f0-125">(Oba soubory lze vynechat od správy zdrojového kódu.) `<projectPath>` Argument může ukazovat `project.json` souborů a má stejné chování jako odkazující na `packages.config` nebo soubor projektu.</span><span class="sxs-lookup"><span data-stu-id="fa1f0-125">(Both files can be omitted from source control.) The `<projectPath>` argument can point a `project.json` file and has the same behavior as pointing to a `packages.config` or project file.</span></span> <span data-ttu-id="fa1f0-126">V pořadí podle priority pro složky balíčku `%userprofile%\.nuget\packages` prohledají se nejprve při použití `project.json`.</span><span class="sxs-lookup"><span data-stu-id="fa1f0-126">In the priority order for package folders, `%userprofile%\.nuget\packages` is searched first when using `project.json`.</span></span>
- <span data-ttu-id="fa1f0-127">`nuget update`: Na Mono, tento příkaz nefunguje s projektů pomocí `project.json`.</span><span class="sxs-lookup"><span data-stu-id="fa1f0-127">`nuget update`: On Mono, this command does not work with projects using `project.json`.</span></span>

## <a name="dependency-resolution-with-packagereference"></a><span data-ttu-id="fa1f0-128">Řešení závislostí s PackageReference</span><span class="sxs-lookup"><span data-stu-id="fa1f0-128">Dependency resolution with PackageReference</span></span>

<span data-ttu-id="fa1f0-129">*Původně v [řešení závislostí](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).*</span><span class="sxs-lookup"><span data-stu-id="fa1f0-129">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).*</span></span>

<span data-ttu-id="fa1f0-130">Chování PackageReference platí také pro `project.json`.</span><span class="sxs-lookup"><span data-stu-id="fa1f0-130">The behavior of PackageReference applies also to `project.json`.</span></span> <span data-ttu-id="fa1f0-131">NuGet restore zapisuje do souboru s názvem graf závislostí `project.lock.json` spolu s `project.json`.</span><span class="sxs-lookup"><span data-stu-id="fa1f0-131">NuGet restore writes the dependency graph into a file named `project.lock.json` alongside `project.json`.</span></span>

## <a name="managing-dependency-assets"></a><span data-ttu-id="fa1f0-132">Správa závislostí prostředky</span><span class="sxs-lookup"><span data-stu-id="fa1f0-132">Managing dependency assets</span></span>

<span data-ttu-id="fa1f0-133">*Původně v [řešení závislostí](../consume-packages/dependency-resolution.md#managing-dependency-assets).*</span><span class="sxs-lookup"><span data-stu-id="fa1f0-133">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#managing-dependency-assets).*</span></span>

<span data-ttu-id="fa1f0-134">Při použití `project.json` formátu, můžete řídit, které prostředky z toku závislosti do nejvyšší úrovně projektu.</span><span class="sxs-lookup"><span data-stu-id="fa1f0-134">When using the `project.json` format, you can control which assets from dependencies flow into the top-level project.</span></span> <span data-ttu-id="fa1f0-135">Podrobnosti najdete v tématu [project.json](project-json.md).</span><span class="sxs-lookup"><span data-stu-id="fa1f0-135">For details, see [project.json](project-json.md).</span></span>

## <a name="excluding-references"></a><span data-ttu-id="fa1f0-136">S výjimkou odkazy</span><span class="sxs-lookup"><span data-stu-id="fa1f0-136">Excluding references</span></span>

<span data-ttu-id="fa1f0-137">*Původně v [řešení závislostí](../consume-packages/dependency-resolution.md#excluding-references).*</span><span class="sxs-lookup"><span data-stu-id="fa1f0-137">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#excluding-references).*</span></span>

- <span data-ttu-id="fa1f0-138">`project.json`: Přidejte `"exclude" : "all"` v závislost PackageC:</span><span class="sxs-lookup"><span data-stu-id="fa1f0-138">`project.json`: add `"exclude" : "all"` in the dependency for PackageC:</span></span>

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

## <a name="resolving-incompatible-package-errors"></a><span data-ttu-id="fa1f0-139">Řešení chyb při nekompatibilní balíčku</span><span class="sxs-lookup"><span data-stu-id="fa1f0-139">Resolving incompatible package errors</span></span>

<span data-ttu-id="fa1f0-140">*Původně v [řešení závislostí](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors).*</span><span class="sxs-lookup"><span data-stu-id="fa1f0-140">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors).*</span></span>

<span data-ttu-id="fa1f0-141">Přidání způsob řešení chyb:</span><span class="sxs-lookup"><span data-stu-id="fa1f0-141">An added means of resolving errors:</span></span>

- <span data-ttu-id="fa1f0-142">**Nedoporučuje se**: jako dočasné řešení při práci s autora balíčku projekty cílení na `netcore`, `netstandard`, a `netcoreapp` mohou ostatní platformy jako kompatibilní, a tím umožní balíčky cílené na těch, které označují ostatní platformy, který se má použít.</span><span class="sxs-lookup"><span data-stu-id="fa1f0-142">**Not recommended**: as a temporary solution while you work with the package author, projects targeting `netcore`, `netstandard`, and `netcoreapp` can denote other frameworks as being compatible, thereby allowing packages targeting those other frameworks to be used.</span></span> <span data-ttu-id="fa1f0-143">V tématu [project.json importuje](project-json.md#imports) a [cíl obnovení MSBuild PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback).</span><span class="sxs-lookup"><span data-stu-id="fa1f0-143">See [project.json imports](project-json.md#imports) and [MSBuild restore target PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback).</span></span> <span data-ttu-id="fa1f0-144">To může způsobit neočekávané chování, proto znovu, je vhodné řešení nekompatibility balíček ve spolupráci s autora balíčku na aktualizace.</span><span class="sxs-lookup"><span data-stu-id="fa1f0-144">This can cause unexpected behaviors, so again, it's best to resolve package incompatibilities by working with the package author on an update.</span></span>

## <a name="target-frameworks"></a><span data-ttu-id="fa1f0-145">Cílové rozhraní</span><span class="sxs-lookup"><span data-stu-id="fa1f0-145">Target frameworks</span></span>

<span data-ttu-id="fa1f0-146">*Původně v [cílové rozhraní](../reference/target-frameworks.md).*</span><span class="sxs-lookup"><span data-stu-id="fa1f0-146">*Originally in [Target frameworks](../reference/target-frameworks.md).*</span></span>

- <span data-ttu-id="fa1f0-147">[Project.JSON](project-json.md): `frameworks` uzlu určuje framework verze, které mohou být zkompilovány projektu proti.</span><span class="sxs-lookup"><span data-stu-id="fa1f0-147">[project.json](project-json.md): The `frameworks` node specifies the framework versions that the project can be compiled against.</span></span>

## <a name="creating-a-package"></a><span data-ttu-id="fa1f0-148">Vytváření balíčku</span><span class="sxs-lookup"><span data-stu-id="fa1f0-148">Creating a package</span></span>

<span data-ttu-id="fa1f0-149">*Původně v [vytváření balíčku](../create-packages/creating-a-package.md)*</span><span class="sxs-lookup"><span data-stu-id="fa1f0-149">*Originally in [Creating a package](../create-packages/creating-a-package.md)*</span></span>

### <a name="setting-a-package-type"></a><span data-ttu-id="fa1f0-150">Balíček typ nastavení</span><span class="sxs-lookup"><span data-stu-id="fa1f0-150">Setting a package type</span></span>

<span data-ttu-id="fa1f0-151">S .NET Core 1.x, když je nainstalovaný balíček DotnetCliTool, Visual Studio umístí balíčku `project.json` `tools` uzlu místo `dependencies` uzlu.</span><span class="sxs-lookup"><span data-stu-id="fa1f0-151">With .NET Core 1.x, when a DotnetCliTool package is installed, Visual Studio places the package in the `project.json` `tools` node instead of the `dependencies` node.</span></span>

<span data-ttu-id="fa1f0-152">Balíček typy jsou nastaveny v `project.json`.</span><span class="sxs-lookup"><span data-stu-id="fa1f0-152">Package types are set in `project.json`.</span></span>

- <span data-ttu-id="fa1f0-153">`project.json`: Označuje typ balíčku v rámci `packOptions.packageType` vlastnosti json:</span><span class="sxs-lookup"><span data-stu-id="fa1f0-153">`project.json`: Indicate the package type within a `packOptions.packageType` property json:</span></span>

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

### <a name="adding-targets-and-props-for-msbuild"></a><span data-ttu-id="fa1f0-154">Přidání cíle a props pro nástroje MSBuild</span><span class="sxs-lookup"><span data-stu-id="fa1f0-154">Adding targets and props for MSBuild</span></span>

<span data-ttu-id="fa1f0-155">*Původně v [vytvořit balíčky NuGet standardní .NET s Visual Studiem 2015](../guides/create-net-standard-packages-vs2015.md).*</span><span class="sxs-lookup"><span data-stu-id="fa1f0-155">*Originally in [Create .NET Standard NuGet Packages with Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*</span></span>

<span data-ttu-id="fa1f0-156">Při použití `project.json`, cíle nejsou přidány do projektu, ale jsou k dispozici prostřednictvím `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="fa1f0-156">When using `project.json`, targets are not added to the project but are made available through the `project.lock.json`.</span></span>

### <a name="package-versioning"></a><span data-ttu-id="fa1f0-157">Správa verzí balíčku</span><span class="sxs-lookup"><span data-stu-id="fa1f0-157">Package versioning</span></span>

<span data-ttu-id="fa1f0-158">*Původně v [Správa verzí balíčku](../reference/package-versioning.md).*</span><span class="sxs-lookup"><span data-stu-id="fa1f0-158">*Originally in [Package versioning](../reference/package-versioning.md).*</span></span>

<span data-ttu-id="fa1f0-159">Při použití `project.json` formátu, NuGet také podporuje notaci zástupný znak, \*, pro hlavní, vedlejší, opravy a příponu předběžné verze součástí číslo.</span><span class="sxs-lookup"><span data-stu-id="fa1f0-159">When using the `project.json` format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span>

### <a name="nugetconfig-reference"></a><span data-ttu-id="fa1f0-160">Odkaz na soubor nuget.config.</span><span class="sxs-lookup"><span data-stu-id="fa1f0-160">NuGet.Config reference</span></span>

<span data-ttu-id="fa1f0-161">*Původně v [NuGet.Config odkaz](../reference/nuget-config-file.md).*</span><span class="sxs-lookup"><span data-stu-id="fa1f0-161">*Originally in [NuGet.Config reference](../reference/nuget-config-file.md).*</span></span>

<span data-ttu-id="fa1f0-162">`globalPackagesFolder` platí pouze pro `project.json`.</span><span class="sxs-lookup"><span data-stu-id="fa1f0-162">`globalPackagesFolder` applies only to `project.json`.</span></span> <span data-ttu-id="fa1f0-163">(Byla přidána poznámka: platí také pro PackageReference.)</span><span class="sxs-lookup"><span data-stu-id="fa1f0-163">(Added note: also applies to PackageReference.)</span></span>

### <a name="nuspec-file-reference"></a><span data-ttu-id="fa1f0-164">odkaz na soubor nuspec</span><span class="sxs-lookup"><span data-stu-id="fa1f0-164">nuspec file reference</span></span>

<span data-ttu-id="fa1f0-165">*Původně v [odkaz na soubor nuspec](../reference/nuspec.md).*</span><span class="sxs-lookup"><span data-stu-id="fa1f0-165">*Originally in [nuspec reference](../reference/nuspec.md).*</span></span>

<span data-ttu-id="fa1f0-166">`<contentFiles>` Element se používá namísto `<files>` s `project.json`.</span><span class="sxs-lookup"><span data-stu-id="fa1f0-166">The `<contentFiles>` element is used instead of `<files>` with `project.json`.</span></span>

### <a name="package-manager-options-control"></a><span data-ttu-id="fa1f0-167">Balíček správce možnosti řízení</span><span class="sxs-lookup"><span data-stu-id="fa1f0-167">Package manager options control</span></span>

<span data-ttu-id="fa1f0-168">*Původně v [reference k uživatelskému rozhraní Správce balíčků](../tools/package-manager-ui.md).*</span><span class="sxs-lookup"><span data-stu-id="fa1f0-168">*Originally in [Package Manager UI reference](../tools/package-manager-ui.md).*</span></span>

<span data-ttu-id="fa1f0-169">Projekty pomocí `project.json` správu formátu zobrazit pouze **zobrazit okno náhledu** možnost.</span><span class="sxs-lookup"><span data-stu-id="fa1f0-169">Projects using `project.json` management format show only the **Show preview window** option.</span></span>

### <a name="visual-studio-templates"></a><span data-ttu-id="fa1f0-170">Šablony aplikace Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fa1f0-170">Visual Studio Templates</span></span>

<span data-ttu-id="fa1f0-171">*Původně v [balíčky NuGet ve šablony sady Visual Studio](../visual-studio-extensibility/visual-studio-templates.md).*</span><span class="sxs-lookup"><span data-stu-id="fa1f0-171">*Originally in [NuGet Packages in Visual Studio templates](../visual-studio-extensibility/visual-studio-templates.md).*</span></span>

<span data-ttu-id="fa1f0-172">Osvědčené postupy: šablony neobsahují `project.json` souboru a nezahrnují nebo žádné odkazy nebo obsah, který by byl přidán, když se instalují balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="fa1f0-172">Best practices: templates do not include a `project.json` file, and do not include or any references or content that would be added when NuGet packages are installed.</span></span>