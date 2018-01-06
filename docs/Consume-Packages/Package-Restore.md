---
title: "Obnovení balíčku NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a7bf21da-86ae-4c2d-8750-04ff53f41967
description: "Popis jak NuGet obnoví balíčky, na kterých závisí na projekt včetně postup zakázání obnovení a omezit verze."
keywords: "Obnovení balíčku NuGet, instalace balíčku NuGet, instalace balíčku, Probíhá obnovení balíčků, verze závislosti, zakázat automatické obnovení chovaly verze balíčku"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4e819a2bb34bbe70f0f11d5adeed82b976a8cb65
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/05/2018
---
# <a name="package-restore"></a><span data-ttu-id="34d49-104">Obnovení balíčku</span><span class="sxs-lookup"><span data-stu-id="34d49-104">Package Restore</span></span>

<span data-ttu-id="34d49-105">Ke zvýšení úrovně čisticí vývojového prostředí a zmenšit velikost úložiště, NuGet **obnovení balíčků** nainstaluje všechny odkazované balíčky, než je založený na projekt.</span><span class="sxs-lookup"><span data-stu-id="34d49-105">To promote a cleaner development environment and to reduce repository size, NuGet **Package Restore** installs all referenced packages before a project is built.</span></span> <span data-ttu-id="34d49-106">Tato funkce se často používá zajistí, že všechny závislosti jsou k dispozici v projektu bez nutnosti tyto balíčky k uložení do správy zdrojového kódu (v tématu [balíčky a Správa zdrojového kódu](../consume-packages/packages-and-source-control.md) na tom, jak nakonfigurovat úložiště k vyloučení binární soubory balíčku).</span><span class="sxs-lookup"><span data-stu-id="34d49-106">This widely-used feature ensures that all dependencies are available in a project without requiring those packages to be stored in source control (see [Packages and Source Control](../consume-packages/packages-and-source-control.md) on how to configure your repository to exclude package binaries).</span></span>

<span data-ttu-id="34d49-107">V tomto tématu:</span><span class="sxs-lookup"><span data-stu-id="34d49-107">In this topic:</span></span>
- [<span data-ttu-id="34d49-108">Obnovení Stručná příručka k balíčku</span><span class="sxs-lookup"><span data-stu-id="34d49-108">Quick guide to package restore</span></span>](#quick-guide-to-package-restore)
- [<span data-ttu-id="34d49-109">Přehled obnovení balíčku</span><span class="sxs-lookup"><span data-stu-id="34d49-109">Package restore overview</span></span>](#package-restore-overview)
- [<span data-ttu-id="34d49-110">Povolení a zákaz obnovení balíčků</span><span class="sxs-lookup"><span data-stu-id="34d49-110">Enabling and disabling package restore</span></span>](#enabling-and-disabling-package-restore)
- [<span data-ttu-id="34d49-111">Omezení verze balíčku s obnovením</span><span class="sxs-lookup"><span data-stu-id="34d49-111">Constraining package versions with restore</span></span>](#constraining-package-versions-with-restore)
- <span data-ttu-id="34d49-112">[Příkazového řádku obnovení](#command-line-restore), pro všechny verze systému NuGet</span><span class="sxs-lookup"><span data-stu-id="34d49-112">[Command-line restore](#command-line-restore), for all versions of NuGet</span></span>
- <span data-ttu-id="34d49-113">[Automatické obnovení v sadě Visual Studio](#automatic-restore-in-visual-studio)pro NuGet 2.7 a později.</span><span class="sxs-lookup"><span data-stu-id="34d49-113">[Automatic restore in Visual Studio](#automatic-restore-in-visual-studio), for NuGet 2.7 and later.</span></span>
- <span data-ttu-id="34d49-114">[Integrované nástroje MSBuild obnovení v sadě Visual Studio](#msbuild-integrated-restore)pro NuGet 2.6 a dříve.</span><span class="sxs-lookup"><span data-stu-id="34d49-114">[MSBuild-integrated restore in Visual Studio](#msbuild-integrated-restore), for NuGet 2.6 and earlier.</span></span>
- [<span data-ttu-id="34d49-115">Obnovení balíčku s Team Foundation Build</span><span class="sxs-lookup"><span data-stu-id="34d49-115">Package restore with Team Foundation Build</span></span>](#package-restore-with-team-foundation-build)

<span data-ttu-id="34d49-116">Obnovit chování se liší podle verze; Pokud chcete zkontrolovat verzi vaší NuGet, jednoduše spusťte `nuget.exe` příkazového řádku a podívejte se na první řádek výstupu.</span><span class="sxs-lookup"><span data-stu-id="34d49-116">Restore behavior does vary by version; to check your NuGet version, simply run `nuget.exe` on the command line and look at the first line of output.</span></span>

<span data-ttu-id="34d49-117">Další informace o obnovení balíčků na serverech sestavení v [obnovení balíčků s TFBuild](../consume-packages/team-foundation-build.md).</span><span class="sxs-lookup"><span data-stu-id="34d49-117">For additional details on package restore on build servers, see [Package restore with TFBuild](../consume-packages/team-foundation-build.md).</span></span>

> [!Note]
> <span data-ttu-id="34d49-118">Projekty, které jsou nakonfigurované pro balíček obnovit také práci s xbuild na Mono.</span><span class="sxs-lookup"><span data-stu-id="34d49-118">Projects configured for package restore also work with xbuild on Mono.</span></span>

## <a name="quick-guide-to-package-restore"></a><span data-ttu-id="34d49-119">Obnovení Stručná příručka k balíčku</span><span class="sxs-lookup"><span data-stu-id="34d49-119">Quick guide to package restore</span></span>

[!INCLUDE[package-restore](../includes/package-restore.md)]

> [!Note]
> <span data-ttu-id="34d49-120">Pokud se zobrazí chyba "Tento projekt odkazuje na balíčky NuGet, které nejsou v tomto počítači" nebo "jeden nebo více balíčků NuGet je potřeba, ale nebylo možné, protože nebyl udělen souhlas", zapněte automatické obnovení podle pokynů v části [Povolení a zákaz obnovení balíčků](#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="34d49-120">If you see the error "This project references NuGet package(s) that are missing on this computer" or "One or more NuGet packages need to be restored but couldn't be because consent has not been granted," turn on automatic restore by following the instructions under [Enabling and disabling package restore](#enabling-and-disabling-package-restore).</span></span>

## <a name="package-restore-overview"></a><span data-ttu-id="34d49-121">Přehled obnovení balíčku</span><span class="sxs-lookup"><span data-stu-id="34d49-121">Package restore overview</span></span>

<span data-ttu-id="34d49-122">Nejprve balíček odkazuje udržované v jednom z následujících formátů správu balíčku, v závislosti na typu projektu a verze NuGet.</span><span class="sxs-lookup"><span data-stu-id="34d49-122">First, package references are maintained in one of the following package management formats, depending on project type and NuGet version.</span></span> <span data-ttu-id="34d49-123">(Všimněte si, že NuGet 4 a MSBuild 15.1 je instalován s Visual Studio 2017.)</span><span class="sxs-lookup"><span data-stu-id="34d49-123">(Note that NuGet 4 and MSBuild 15.1 are installed with Visual Studio 2017.)</span></span>

| <span data-ttu-id="34d49-124">Metoda</span><span class="sxs-lookup"><span data-stu-id="34d49-124">Method</span></span> | <span data-ttu-id="34d49-125">Verze NuGet</span><span class="sxs-lookup"><span data-stu-id="34d49-125">NuGet Version</span></span> | <span data-ttu-id="34d49-126">Popis</span><span class="sxs-lookup"><span data-stu-id="34d49-126">Description</span></span> | 
| --- | --- | --- |
| `packages.config` | <span data-ttu-id="34d49-127">2.x +</span><span class="sxs-lookup"><span data-stu-id="34d49-127">2.x+</span></span> | <span data-ttu-id="34d49-128">Uvádí hloubkové kompletní sadu závislosti.</span><span class="sxs-lookup"><span data-stu-id="34d49-128">Lists the complete deep set of dependencies.</span></span> <span data-ttu-id="34d49-129">Přidat do balíčků `packages.config` musíte přidat i k souboru projektu a cílů a Props musíte přidat i do souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="34d49-129">Packages added to `packages.config` must also be added to the project file, and Targets and Props must also be added to the project file.</span></span> <span data-ttu-id="34d49-130">Toto je metoda standardních hodnot pro všechny verze balíčku nuget, ale má nižší výkon ve srovnání s jinými možnostmi.</span><span class="sxs-lookup"><span data-stu-id="34d49-130">This is the baseline method for all versions of NuGet, but has slower performance compared with the other options.</span></span> <span data-ttu-id="34d49-131">(Viz [souboru packages.config schématu](../schema/packages-config.md).)</span><span class="sxs-lookup"><span data-stu-id="34d49-131">(See [packages.config schema](../schema/packages-config.md).)</span></span> | 
| `project.json` | <span data-ttu-id="34d49-132">3.x +</span><span class="sxs-lookup"><span data-stu-id="34d49-132">3.x+</span></span> | <span data-ttu-id="34d49-133">Použít pouze ve výchozím nastavení s projekty UWP, ale projekty mohou být převedeny z `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="34d49-133">Used only by default with UWP projects, but projects can be converted from `packages.config`.</span></span> <span data-ttu-id="34d49-134">`project.json`uvádí jenom nejvyšší úrovně závislosti.</span><span class="sxs-lookup"><span data-stu-id="34d49-134">`project.json` lists only top-level dependencies.</span></span> <span data-ttu-id="34d49-135">Odkazy, cílů a Props se dynamicky k projektu nepřidají během vytváření sestavení, což vede k lepší výkon ve srovnání s `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="34d49-135">References, Targets, and Props are added dynamically to the project during build, resulting in better performance compared with `packages.config`.</span></span> <span data-ttu-id="34d49-136">(Viz [project.json schématu](../schema/project-json.md).)</span><span class="sxs-lookup"><span data-stu-id="34d49-136">(See [project.json schema](../schema/project-json.md).)</span></span>|
| <span data-ttu-id="34d49-137">PackageReference</span><span class="sxs-lookup"><span data-stu-id="34d49-137">PackageReference</span></span> | <span data-ttu-id="34d49-138">4.x +</span><span class="sxs-lookup"><span data-stu-id="34d49-138">4.x+</span></span> | <span data-ttu-id="34d49-139">Uvádí přímo v souboru projektu v závislosti `<PackageReference>` uzlu, alongside `<Reference>` a `<ProjectReference>`.</span><span class="sxs-lookup"><span data-stu-id="34d49-139">Lists dependencies directly in the project file in the `<PackageReference>` node, alongside `<Reference>` and `<ProjectReference>`.</span></span> <span data-ttu-id="34d49-140">Podobně jako funguje `project.json`; najdete v části [balíček odkazy v souborech projektu](../Consume-Packages/Package-References-in-Project-Files.md).</span><span class="sxs-lookup"><span data-stu-id="34d49-140">Works similarly to `project.json`; see [Package references in project files](../Consume-Packages/Package-References-in-Project-Files.md).</span></span> |

<span data-ttu-id="34d49-141">Druhý spustit obnovení pomocí seznamu odkaz v mnoha různými způsoby:</span><span class="sxs-lookup"><span data-stu-id="34d49-141">Second, you start a restore using the reference list in a variety of ways:</span></span>

<span data-ttu-id="34d49-142">Z příkazového řádku nebo [Konzola správce balíčků](../tools/Package-Manager-Console.md):</span><span class="sxs-lookup"><span data-stu-id="34d49-142">From the command line or [Package Manager Console](../tools/Package-Manager-Console.md):</span></span>

| <span data-ttu-id="34d49-143">Příkaz</span><span class="sxs-lookup"><span data-stu-id="34d49-143">Command</span></span> | <span data-ttu-id="34d49-144">Použít scénáře</span><span class="sxs-lookup"><span data-stu-id="34d49-144">Applicable scenarios</span></span> |
| --- | --- | 
| `nuget restore` | <span data-ttu-id="34d49-145">Všechny verze NuGet a všechny odkazové typy.</span><span class="sxs-lookup"><span data-stu-id="34d49-145">All versions of NuGet and all reference types.</span></span> <span data-ttu-id="34d49-146">V tématu [příkazového řádku obnovení](#command-line-restore) níže.</span><span class="sxs-lookup"><span data-stu-id="34d49-146">See [Command-line restore](#command-line-restore) below.</span></span> | 
| `dotnet restore` | <span data-ttu-id="34d49-147">Stejné jako `nuget restore` pro projekty .NET Core.</span><span class="sxs-lookup"><span data-stu-id="34d49-147">Same as `nuget restore` for .NET Core projects.</span></span> <span data-ttu-id="34d49-148">V tématu [dotnet obnovení](/dotnet/articles/core/tools/dotnet-restore).</span><span class="sxs-lookup"><span data-stu-id="34d49-148">See [dotnet restore](/dotnet/articles/core/tools/dotnet-restore).</span></span> |
| `msbuild /t:restore` | <span data-ttu-id="34d49-149">Nuget 4.x+ a MSBuild 15.1 + s [balíček odkazy v souborech projektu](../Consume-Packages/Package-References-in-Project-Files.md) pouze.</span><span class="sxs-lookup"><span data-stu-id="34d49-149">Nuget 4.x+ and MSBuild 15.1+ with [package references in project files](../Consume-Packages/Package-References-in-Project-Files.md) only.</span></span> <span data-ttu-id="34d49-150">`nuget restore`a `dotnet restore` obě tento příkaz použijte pro příslušné projekty.</span><span class="sxs-lookup"><span data-stu-id="34d49-150">`nuget restore` and `dotnet restore` both use this command for applicable projects.</span></span> <span data-ttu-id="34d49-151">V tématu [NuGet pack a obnovení jako MSBuild cíle obnovení cíl](../schema/msbuild-targets.md#restore-target).</span><span class="sxs-lookup"><span data-stu-id="34d49-151">See [NuGet pack and restore as MSBuild targets- restore target](../schema/msbuild-targets.md#restore-target).</span></span>|

<span data-ttu-id="34d49-152">Visual Studio, samotné také obnoví balíčky v různých časech:</span><span class="sxs-lookup"><span data-stu-id="34d49-152">Visual Studio itself also restores packages at different times:</span></span>

| <span data-ttu-id="34d49-153">Typ</span><span class="sxs-lookup"><span data-stu-id="34d49-153">Type</span></span> | <span data-ttu-id="34d49-154">Když se stane obnovení</span><span class="sxs-lookup"><span data-stu-id="34d49-154">When restore happens</span></span> |
| --- | --- |
| <span data-ttu-id="34d49-155">Obnovení šablony</span><span class="sxs-lookup"><span data-stu-id="34d49-155">Template restore</span></span> | <span data-ttu-id="34d49-156">Při vytvoření nového projektu jako některé šablony závisí na externí balíčky.</span><span class="sxs-lookup"><span data-stu-id="34d49-156">During creation of a new project, as some templates depend on external packages.</span></span> |
| <span data-ttu-id="34d49-157">Sestavení obnovení</span><span class="sxs-lookup"><span data-stu-id="34d49-157">Build restore</span></span> | <span data-ttu-id="34d49-158">Jako první krok sestavení.</span><span class="sxs-lookup"><span data-stu-id="34d49-158">As the first step of a build.</span></span> |
| <span data-ttu-id="34d49-159">Řešení obnovení</span><span class="sxs-lookup"><span data-stu-id="34d49-159">Solution restore</span></span> | <span data-ttu-id="34d49-160">Když uživatel klikne pravým tlačítkem myši řešení a vybírá **obnovení balíčků NuGet**.</span><span class="sxs-lookup"><span data-stu-id="34d49-160">When user right-clicks a solution and selects **Restore NuGet Packages**.</span></span> |
| <span data-ttu-id="34d49-161">Obnovit na změnu projektu</span><span class="sxs-lookup"><span data-stu-id="34d49-161">Restore on project change</span></span> | <span data-ttu-id="34d49-162">*(NuGet 4.x pouze)*  Projektu na základě při .NET Core SDK se používá, včetně při projektu změny stavu.</span><span class="sxs-lookup"><span data-stu-id="34d49-162">*(NuGet 4.x only)* When a .NET Core SDK-based project is used, including when project state changes.</span></span> |

## <a name="enabling-and-disabling-package-restore"></a><span data-ttu-id="34d49-163">Povolení a zákaz obnovení balíčků</span><span class="sxs-lookup"><span data-stu-id="34d49-163">Enabling and disabling package restore</span></span>

<span data-ttu-id="34d49-164">Obnovení balíčku je primárně povolená díky **nástroje > Možnosti > Správce balíčků NuGet** v sadě Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="34d49-164">Package restore is primarily enabled through **Tools > Options > NuGet Package Manager** in Visual Studio:</span></span>

![Řízení chování obnovení balíčku prostřednictvím možnosti Správce balíčků NuGet](media/Restore-01-AutoRestoreOptions.png)

- <span data-ttu-id="34d49-166">**Povolit aplikaci NuGet stáhnout chybějící balíčky**: řídí všechny formy obnovení balíčků změnou `packageRestore/enabled` nastavení v `%AppData%\NuGet\NuGet.Config` souboru, jak je uvedeno níže.</span><span class="sxs-lookup"><span data-stu-id="34d49-166">**Allow NuGet to download missing packages**: controls all forms of package restore by changing the `packageRestore/enabled` setting in the `%AppData%\NuGet\NuGet.Config` file as shown below.</span></span>

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-Integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    <br/>
    > [!Note]
    >  <span data-ttu-id="34d49-167">`packageRestore/enabled` Nastavení je možné přepsat globálně nastavením proměnné prostředí názvem **EnableNuGetPackageRestore** s hodnotou PRAVDA nebo NEPRAVDA před spuštění sady Visual Studio nebo spuštění sestavení.</span><span class="sxs-lookup"><span data-stu-id="34d49-167">The `packageRestore/enabled` setting can be overridden globally by setting an environment variable called **EnableNuGetPackageRestore** with a value of TRUE or FALSE before launching Visual Studio or starting a build.</span></span>
    

- <span data-ttu-id="34d49-168">**Automaticky Zkontrolujte chybějící balíčky během sestavení v sadě Visual Studio**: Automatické obnovení NuGet 2.7 a později změnou ovládací prvky `packageRestore/automatic` nastavení v `%AppData%\NuGet\NuGet.Config` souboru, jak je uvedeno níže.</span><span class="sxs-lookup"><span data-stu-id="34d49-168">**Automatically check for missing packages during build in Visual Studio**: controls automatic restore for NuGet 2.7 and later by changing the `packageRestore/automatic` setting in the `%AppData%\NuGet\NuGet.Config` file as shown below.</span></span>
            
    ```xml
    ...
    <configuration>
        <packageRestore>
            <!-- The 'automatic' key is set to True when the "Automatically check for missing packages during
                 build in Visual Studio" checkbox is set. Clearing the box sets this to False and disables
                 automatic restore. -->
            <add key="automatic" value="True" />
        </packageRestore>
    </configuration>
    ```

<span data-ttu-id="34d49-169">Odkaz, najdete v článku [NuGet konfiguračního souboru – část packageRestore](../Schema/nuget-config-file.md#packagerestore-section).</span><span class="sxs-lookup"><span data-stu-id="34d49-169">For reference, see the [NuGet config file - packageRestore section](../Schema/nuget-config-file.md#packagerestore-section).</span></span>

<span data-ttu-id="34d49-170">V některých případech vývojáře nebo společnosti chtít povolit nebo zakázat obnovení balíčku na počítači, ve výchozím nastavení pro všechny uživatele.</span><span class="sxs-lookup"><span data-stu-id="34d49-170">In some cases, a developer or company might want to enable or disable package restore on a machine by default for all users.</span></span> <span data-ttu-id="34d49-171">To lze provést přidáním globální NuGet konfigurační soubor umístěný ve stejné nastavení výše `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`.</span><span class="sxs-lookup"><span data-stu-id="34d49-171">This can be done by adding the same settings above to the global NuGet configuration file located in `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`.</span></span> <span data-ttu-id="34d49-172">Jednotlivým uživatelům můžete selektivně povolte obnovení podle potřeby na úrovni projektu.</span><span class="sxs-lookup"><span data-stu-id="34d49-172">Individual users can then selectively enable restore as needed on a project level.</span></span> <span data-ttu-id="34d49-173">V tématu [konfigurace chování NuGet](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) přesné informace o tom, jak NuGet upřednostňuje více konfigurační soubory.</span><span class="sxs-lookup"><span data-stu-id="34d49-173">See [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) for exact details on how NuGet prioritizes multiple config files.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="34d49-174">Omezení verze balíčku s obnovením</span><span class="sxs-lookup"><span data-stu-id="34d49-174">Constraining package versions with restore</span></span>

<span data-ttu-id="34d49-175">Když NuGet obnoví balíčky pomocí libovolné metody, dodrží žádná omezení, zadaný v `packages.config`, `project.json`, nebo soubor projektu:</span><span class="sxs-lookup"><span data-stu-id="34d49-175">When NuGet restores packages through any method, it will honor any constraints specified in `packages.config`, `project.json`, or the project file:</span></span>

- <span data-ttu-id="34d49-176">`packages.config`: Určete rozsah verze v `allowedVersion` vlastnost závislosti.</span><span class="sxs-lookup"><span data-stu-id="34d49-176">`packages.config`: Specify a version range in the `allowedVersion` property of the dependency.</span></span> <span data-ttu-id="34d49-177">V tématu [přeinstalovat a aktualizaci balíčků](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span><span class="sxs-lookup"><span data-stu-id="34d49-177">See [Reinstalling and Updating Packages](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="34d49-178">Příklad:</span><span class="sxs-lookup"><span data-stu-id="34d49-178">For example:</span></span>

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- <span data-ttu-id="34d49-179">`project.json`: Určete rozsah verze přímo s číslem verze této závislosti.</span><span class="sxs-lookup"><span data-stu-id="34d49-179">`project.json`: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="34d49-180">Příklad:</span><span class="sxs-lookup"><span data-stu-id="34d49-180">For example:</span></span>

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

- <span data-ttu-id="34d49-181">Balíček odkazy v souborech projektu: Zadejte verzi rozsah přímo s číslem verze této závislosti.</span><span class="sxs-lookup"><span data-stu-id="34d49-181">Package references in project files: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="34d49-182">Příklad:</span><span class="sxs-lookup"><span data-stu-id="34d49-182">For example:</span></span>
 
    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />  
    ```

<span data-ttu-id="34d49-183">Ve všech případech, použijte zápis popsané v [Správa verzí balíčku](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="34d49-183">In all cases, use the notation described in [Package versioning](../reference/package-versioning.md).</span></span>

## <a name="command-line-restore"></a><span data-ttu-id="34d49-184">Obnovení příkazového řádku</span><span class="sxs-lookup"><span data-stu-id="34d49-184">Command-line restore</span></span>

<span data-ttu-id="34d49-185">NuGet 2.7 a výše, použijte [obnovení](../tools/cli-ref-restore.md) příkazu obnovte všechny balíčky v řešení (jestli používá `packages.config`, `project.json`, nebo balíčku odkazy v souborech projektu).</span><span class="sxs-lookup"><span data-stu-id="34d49-185">For NuGet 2.7 and above, use the [Restore](../tools/cli-ref-restore.md) command to restore all packages in a solution (whether it uses `packages.config`, `project.json`, or package references in project files).</span></span> <span data-ttu-id="34d49-186">Pro daný projekt složku jako `c:\proj\app`, běžné varianty níže každý obnovení balíčků:</span><span class="sxs-lookup"><span data-stu-id="34d49-186">For a given project folder such as `c:\proj\app`, the common variations below each restore the packages:</span></span>

```
c:\proj\app\> nuget restore
c:\proj\app\> nuget.exe restore app.sln
c:\proj\> nuget restore app
```

<span data-ttu-id="34d49-187">Pro NuGet 4.0 + a MSBuild 15.1 +, můžete také použít `MSBuild /t:restore` jak je popsáno na [NuGet pack a obnovit jako cíle MSBuild](../schema/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="34d49-187">For NuGet 4.0+ and MSBuild 15.1+, you can also use `MSBuild /t:restore` as described on [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md).</span></span>

## <a name="build-time-restore-in-visual-studio"></a><span data-ttu-id="34d49-188">Obnovení době sestavení v sadě Visual Studio</span><span class="sxs-lookup"><span data-stu-id="34d49-188">Build-time restore in Visual Studio</span></span>

<span data-ttu-id="34d49-189">Visual Studio automaticky obnoví chybějící balíčky ve výchozím nastavení na začátku sestavení.</span><span class="sxs-lookup"><span data-stu-id="34d49-189">Visual Studio automatically restores missing packages by default at the beginning of a build.</span></span> <span data-ttu-id="34d49-190">Toto chování lze změnit tak, že smažete **nástroje > Možnosti > Správce balíčků NuGet > Obecné > automaticky Zkontrolujte chybějící balíčky během sestavení v sadě Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="34d49-190">This behavior can be changed by clearing **Tools > Options > NuGet Package Manager > General > Automatically check for missing packages during build in Visual Studio**.</span></span>

<span data-ttu-id="34d49-191">Když je povolené, automatické obnovení funguje takto:</span><span class="sxs-lookup"><span data-stu-id="34d49-191">When enabled, automatic restore works as follows:</span></span>

1. <span data-ttu-id="34d49-192">Po zahájení sestavení sady Visual Studio dá pokyn k obnovení balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="34d49-192">When a build begins, Visual Studio instructs NuGet to restore packages.</span></span>
1. <span data-ttu-id="34d49-193">Rekurzivní NuGet hledá všechny `packages.config` soubory v řešení, hledá `project.json`, nebo hledá v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="34d49-193">NuGet recursively looks for all `packages.config` files in the solution, looks for `project.json`, or looks in the project file.</span></span>
1. <span data-ttu-id="34d49-194">Pro každý balíčky uvedené v referenčních souborů, NuGet kontroly Pokud již existuje v řešení ( `packages` složky, `project.lock.json`, nebo `project.assets.json` v závislosti na tom, jestli je projekt pomocí `packages.config`, `project.json`, nebo na odkazy v balíčku soubory projektu).</span><span class="sxs-lookup"><span data-stu-id="34d49-194">For each packages listed in the reference files, NuGet checks if it already exists in the solution (the `packages` folder, `project.lock.json`, or `project.assets.json` depending on whether the project is using `packages.config`, `project.json`, or package references in project files).</span></span>
1. <span data-ttu-id="34d49-195">Pokud daný balíček nebyl nalezen, NuGet pokusí načíst balíček ze své mezipaměti nejprve (viz [Správa mezipaměti NuGet](../consume-packages/managing-the-nuget-cache.md).</span><span class="sxs-lookup"><span data-stu-id="34d49-195">If the package is not found, NuGet attempts to retrieve the package from its cache first (see [Managing the NuGet cache](../consume-packages/managing-the-nuget-cache.md).</span></span> <span data-ttu-id="34d49-196">Pokud balíček není v mezipaměti, NuGet pokusí stáhnout balíček z povolených zdrojů, jak je uvedeno v **nástroje > Možnosti > Správce balíčků NuGet > zdroje balíčků**, v pořadí, ve kterém se zobrazí zdroje.</span><span class="sxs-lookup"><span data-stu-id="34d49-196">If the package is not in the cache, NuGet attempts to download the package from the enabled sources as listed in **Tools > Options > NuGet Package Manager > Package Sources**, in the order that the sources appear.</span></span> <span data-ttu-id="34d49-197">V takovém případě NuGet neindikuje selhání najít balíčku, dokud nebude provedena kontrola všech zdrojů, po kterých oznámí selhání jenom pro poslední zdroj v seznamu.</span><span class="sxs-lookup"><span data-stu-id="34d49-197">In this case, NuGet does not indicate a failure to find the package until all the sources have been checked, at which time it reports the failure only for the last source in the list.</span></span> <span data-ttu-id="34d49-198">Nepřímo takové chyby také znamená, že balíček nebyl k dispozici na žádném z jiných zdrojů buď, i v případě, že chyby nebyly zobrazeny pro tyto zdroje jednotlivě.</span><span class="sxs-lookup"><span data-stu-id="34d49-198">By implication such an error also means that the package wasn't present on any of the other sources either, even though errors were not shown for those sources individually.</span></span>
1. <span data-ttu-id="34d49-199">Pokud stahování úspěšné, ukládá do mezipaměti balíček NuGet a nainstaluje do řešení (znovu do buď `packages` složky, `project.lock.json`, nebo `project.assets.json`); jinak selže NuGet a sestavení selže.</span><span class="sxs-lookup"><span data-stu-id="34d49-199">If the download is successful, NuGet caches the package and installs it into the solution (again, into either the `packages` folder, `project.lock.json`, or `project.assets.json`); otherwise NuGet fails and the build fails.</span></span>

<span data-ttu-id="34d49-200">Během tohoto procesu se zobrazí dialogové okno průběhu s možností zrušit obnovení balíčků.</span><span class="sxs-lookup"><span data-stu-id="34d49-200">During this process, you see a progress dialog with the option to cancel package restore.</span></span>

## <a name="package-restore-with-team-foundation-build"></a><span data-ttu-id="34d49-201">Obnovení balíčku s Team Foundation Build</span><span class="sxs-lookup"><span data-stu-id="34d49-201">Package Restore with Team Foundation Build</span></span>

<span data-ttu-id="34d49-202">Obnovení balíčku se obvykle používá při sestavování projektů na serverech, sestavení, stejně jako u Team Foundation Server (TFS) a Visual Studio Team Services (stejně jako jiné systémy sestavení, které nejsou zde popsané).</span><span class="sxs-lookup"><span data-stu-id="34d49-202">Package restore is commonly used when building projects on build servers, as with Team Foundation Server (TFS) and Visual Studio Team Services (as well as other build systems, which are not covered here).</span></span>

### <a name="visual-studio-team-services"></a><span data-ttu-id="34d49-203">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="34d49-203">Visual Studio Team Services</span></span>

<span data-ttu-id="34d49-204">Při vytváření definice sestavení v Team Services, jednoduše zahrnují úlohu obnovení balíčků NuGet v definici před všechny úlohy sestavení.</span><span class="sxs-lookup"><span data-stu-id="34d49-204">When creating a build definition on Team Services, simply include the Restore NuGet Packages task in the definition before any build task.</span></span> <span data-ttu-id="34d49-205">Tato úloha je zahrnutá ve výchozím nastavení v počet šablony sestavení.</span><span class="sxs-lookup"><span data-stu-id="34d49-205">This task is included by default in a number of build templates.</span></span>

![Úloha obnovení balíčku NuGet v definici sestavení Visual Studio Team Service](media/Restore-02-VSTSBuild.png)

### <a name="team-foundation-server"></a><span data-ttu-id="34d49-207">Team Foundation Server</span><span class="sxs-lookup"><span data-stu-id="34d49-207">Team Foundation Server</span></span>

<span data-ttu-id="34d49-208">Se sadou TFS 2013 a novější balíčky se automaticky obnoví ve výchozím nastavení během vytváření sestavení, za předpokladu, že používáte-li vytvořit šablonu Team pro Team Foundation Server 2013 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="34d49-208">With TFS 2013 and later, packages are automatically restored by default during build, provided that you're using a Team Build Template for Team Foundation Server 2013 or later.</span></span>

<span data-ttu-id="34d49-209">Pokud používáte předchozí verzi šablony sestavení (například v projektu, který se migroval z dřívějších verzí sady TFS), budete muset taky migrovat ty sestavení šablony do sady TFS 2013.</span><span class="sxs-lookup"><span data-stu-id="34d49-209">If you're using a previous version of build templates (such as in a project that's been migrated from earlier versions of TFS), you'll need to also migrate those build templates to TFS 2013.</span></span> <span data-ttu-id="34d49-210">To v podstatě znamená znovu vytvořit vlastní části šablony sestavení pomocí příslušné šablony pro vašeho zdrojového kódu (TFVC nebo Git).</span><span class="sxs-lookup"><span data-stu-id="34d49-210">This essentially means recreating the custom parts of the Build Templates using the appropriate template for your source control (TFVC or Git).</span></span>

<span data-ttu-id="34d49-211">Pro starší verzi sady TFS, můžete jednoduše zahrnout krok sestavení, který má být vyvolán [příkazového řádku obnovení](#command-line-restore) jak bylo popsáno výše.</span><span class="sxs-lookup"><span data-stu-id="34d49-211">For earlier version of TFS, you can simply include a build step to invoke [command-line restore](#command-line-restore) as described earlier.</span></span>

<span data-ttu-id="34d49-212">Podrobnosti najdete v části pak [návod balíček obnovit pomocí Team Foundation Build](../consume-packages/team-foundation-build.md).</span><span class="sxs-lookup"><span data-stu-id="34d49-212">For more details see then [Walkthrough of Package Restore with Team Foundation Build](../consume-packages/team-foundation-build.md).</span></span>    
