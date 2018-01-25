---
title: "Obnovení balíčku NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a7bf21da-86ae-4c2d-8750-04ff53f41967
description: "Popis jak NuGet obnoví balíčky, na kterých závisí na projekt včetně postup zakázání obnovení a omezit verze."
keywords: "Obnovení balíčku NuGet, instalace balíčku NuGet, instalace balíčku, Probíhá obnovení balíčků, verze závislosti, zakázat automatické obnovení chovaly verze balíčku"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8af70cff522e1f6c285d17ad0bbc20d23a0734a4
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
---
# <a name="package-restore"></a><span data-ttu-id="c4f9d-104">Obnovení balíčku</span><span class="sxs-lookup"><span data-stu-id="c4f9d-104">Package Restore</span></span>

<span data-ttu-id="c4f9d-105">Ke zvýšení úrovně čisticí vývojového prostředí a zmenšit velikost úložiště, NuGet **obnovení balíčků** nainstaluje všechny odkazované balíčky, než je založený na projekt.</span><span class="sxs-lookup"><span data-stu-id="c4f9d-105">To promote a cleaner development environment and to reduce repository size, NuGet **Package Restore** installs all referenced packages before a project is built.</span></span> <span data-ttu-id="c4f9d-106">Tato funkce se často používá&mdash;k dispozici v sadě Visual Studio .NET Core 2.0 + a xbuild na Mono&mdash;zajistí, že všechny závislosti jsou k dispozici v projektu bez nutnosti tyto balíčky k uložení do správy zdrojového kódu (viz [ Balíčky a Správa zdrojového kódu](../consume-packages/packages-and-source-control.md) na tom, jak nakonfigurovat úložiště vyloučit binární soubory balíčku).</span><span class="sxs-lookup"><span data-stu-id="c4f9d-106">This widely-used feature&mdash;available in Visual Studio, .NET Core 2.0+, and xbuild on Mono&mdash;ensures that all dependencies are available in a project without requiring those packages to be stored in source control (see [Packages and Source Control](../consume-packages/packages-and-source-control.md) on how to configure your repository to exclude package binaries).</span></span> <span data-ttu-id="c4f9d-107">Balíčky můžete obnovit také ručně kdykoli.</span><span class="sxs-lookup"><span data-stu-id="c4f9d-107">You can also manually restore packages at any time.</span></span>

<span data-ttu-id="c4f9d-108">Další informace o obnovení balíčků na serverech sestavení v [obnovení balíčků s TFBuild](../consume-packages/team-foundation-build.md).</span><span class="sxs-lookup"><span data-stu-id="c4f9d-108">For additional details on package restore on build servers, see [Package restore with TFBuild](../consume-packages/team-foundation-build.md).</span></span>

## <a name="package-restore-overview"></a><span data-ttu-id="c4f9d-109">Přehled obnovení balíčku</span><span class="sxs-lookup"><span data-stu-id="c4f9d-109">Package restore overview</span></span>

<span data-ttu-id="c4f9d-110">Obnovují se balíčky nejdřív nainstaluje přímé závislosti projektu, podle potřeby, pak instalace všechny závislosti tyto balíčky v rámci celého závislost grafu.</span><span class="sxs-lookup"><span data-stu-id="c4f9d-110">Restoring packages first installs the direct dependencies of a project as needed, then installing any dependencies of those packages throughout the entire dependency graph.</span></span>

<span data-ttu-id="c4f9d-111">Pokud ještě není nainstalovaný balíček, NuGet se nejprve pokusí načíst z [mezipaměti](../consume-packages/managing-the-nuget-cache.md).</span><span class="sxs-lookup"><span data-stu-id="c4f9d-111">If a package is not already installed, NuGet first attempts to retrieve it from the [cache](../consume-packages/managing-the-nuget-cache.md).</span></span> <span data-ttu-id="c4f9d-112">Pokud balíček není v mezipaměti, NuGet se potom pokusí stáhnout balíček z povolených zdrojů, jak je uvedeno v **nástroje > Možnosti > Správce balíčků NuGet > zdroje balíčků**, v pořadí, ve kterém se zobrazí zdroje.</span><span class="sxs-lookup"><span data-stu-id="c4f9d-112">If the package is not in the cache, NuGet then attempts to download the package from the enabled sources as listed in **Tools > Options > NuGet Package Manager > Package Sources**, in the order that the sources appear.</span></span> <span data-ttu-id="c4f9d-113">Stažené balíčky jsou uloženy v mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="c4f9d-113">Downloaded packages are stored in the cache.</span></span>

> [!Note]
> <span data-ttu-id="c4f9d-114">NuGet neindikuje selhání najít balíčku, dokud nebude provedena kontrola všech zdrojů, po kterých oznámí selhání jenom pro poslední zdroj v seznamu.</span><span class="sxs-lookup"><span data-stu-id="c4f9d-114">NuGet does not indicate a failure to find the package until all the sources have been checked, at which time it reports the failure only for the last source in the list.</span></span> <span data-ttu-id="c4f9d-115">Nepřímo takové chyby také znamená, že balíček nebyl k dispozici na žádném z jiných zdrojů buď, i v případě, že chyby nebyly zobrazeny pro tyto zdroje jednotlivě.</span><span class="sxs-lookup"><span data-stu-id="c4f9d-115">By implication such an error also means that the package wasn't present on any of the other sources either, even though errors were not shown for those sources individually.</span></span>

<span data-ttu-id="c4f9d-116">Obnovení balíčku se aktivuje následujícími způsoby:</span><span class="sxs-lookup"><span data-stu-id="c4f9d-116">Package restore is triggered in the following ways:</span></span>

- <span data-ttu-id="c4f9d-117">**Uživatelského rozhraní Správce balíčků (Visual Studio v systému Windows)**: balíčky jsou automaticky neobnoví, při vytváření projektů z šablony a při sestavení projektu (s výjimkou možnosti popsané v [povolení a zakázání balíček obnovit](#enabling-and-disabling-package-restore)).</span><span class="sxs-lookup"><span data-stu-id="c4f9d-117">**Package Manager UI (Visual Studio on Windows)**: Packages are restored automatically when creating a project from a template and when building a project (subject to the option described in [Enabling and disabling package restore](#enabling-and-disabling-package-restore)).</span></span> <span data-ttu-id="c4f9d-118">V NuGet 4.0 + obnovení také dochází vždy při provedení změn projektu na základě rozhraní .NET Core SDK.</span><span class="sxs-lookup"><span data-stu-id="c4f9d-118">In NuGet 4.0+, restore also happens automatically when changes are made to a .NET Core SDK-based project.</span></span>

    <span data-ttu-id="c4f9d-119">Chcete-li obnovit ručně, klikněte pravým tlačítkem v Průzkumníku řešení a vyberte **obnovení balíčků NuGet**.</span><span class="sxs-lookup"><span data-stu-id="c4f9d-119">To restore manually, right-click the solution in Solution Explorer and select **Restore NuGet Packages**.</span></span> <span data-ttu-id="c4f9d-120">Pokud jeden nebo více jednotlivých balíčků jsou stále není správně nainstalován (tj. že Průzkumník řešení se zobrazuje ikona chyby) a pak použít uživatelské rozhraní Správce balíčků odinstalovat a znovu nainstalovat ovlivněných balíčků.</span><span class="sxs-lookup"><span data-stu-id="c4f9d-120">If one or more individual packages are still not installed properly (meaning that Solution Explorer shows an error icon), then use the Package Manager UI to uninstall and reinstall the affected packages.</span></span> <span data-ttu-id="c4f9d-121">V tématu [Reinstalling a aktualizaci balíčků](../Consume-Packages/Reinstalling-and-Updating-Packages.md)</span><span class="sxs-lookup"><span data-stu-id="c4f9d-121">See [Reinstalling and updating packages](../Consume-Packages/Reinstalling-and-Updating-Packages.md)</span></span>

    <span data-ttu-id="c4f9d-122">Pokud se zobrazí chyba "Tento projekt odkazuje na balíčky NuGet, které nejsou v tomto počítači" nebo "jeden nebo více balíčků NuGet je potřeba, ale nebylo možné, protože nebyl udělen souhlas", zapněte automatické obnovení podle pokynů v části [Povolení a zákaz obnovení balíčků](#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="c4f9d-122">If you see the error "This project references NuGet package(s) that are missing on this computer" or "One or more NuGet packages need to be restored but couldn't be because consent has not been granted," turn on automatic restore by following the instructions under [Enabling and disabling package restore](#enabling-and-disabling-package-restore).</span></span>

- <span data-ttu-id="c4f9d-123">**Rozhraní příkazového řádku NuGet**: použijte [obnovení nuget](../tools/cli-ref-restore.md) příkaz, který obnoví balíčky uvedené v souboru projektu (najdete v části [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md)) nebo v [packages.config](../schema/packages-config.md)souboru.</span><span class="sxs-lookup"><span data-stu-id="c4f9d-123">**NuGet CLI**: use the [nuget restore](../tools/cli-ref-restore.md) command, which restores packages listed in the project file (see [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md)) or in a [packages.config](../schema/packages-config.md) file.</span></span> <span data-ttu-id="c4f9d-124">Můžete také určit soubor řešení.</span><span class="sxs-lookup"><span data-stu-id="c4f9d-124">You can also specify a solution file.</span></span>

- <span data-ttu-id="c4f9d-125">**DotNet rozhraní příkazového řádku**: použijte [dotnet obnovení](/dotnet/core/tools/dotnet-restore.md?tabs=netcore2x) příkaz, který obnoví balíčky uvedené v souboru projektu (najdete v části [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md)).</span><span class="sxs-lookup"><span data-stu-id="c4f9d-125">**dotnet CLI**: use the [dotnet restore](/dotnet/core/tools/dotnet-restore.md?tabs=netcore2x) command, which restores packages listed in the project file (see [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md)).</span></span> <span data-ttu-id="c4f9d-126">S .NET Core 2.0 nebo novější, je automaticky provést obnovení s `dotnet build` a `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="c4f9d-126">With .NET Core 2.0 and later, restore is done automatically with `dotnet build` and `dotnet run`.</span></span>

- <span data-ttu-id="c4f9d-127">**MSBuild**: použijte [msbuild /t:restore](../schema/msbuild-targets.md#restore-target) příkaz, který obnovení balíčků balíčky uvedené v souboru projektu (najdete v části [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md)).</span><span class="sxs-lookup"><span data-stu-id="c4f9d-127">**MSBuild**: use the [msbuild /t:restore](../schema/msbuild-targets.md#restore-target) command, which restores packages packages listed in the project file (see [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md)).</span></span> <span data-ttu-id="c4f9d-128">K dispozici pouze v NuGet 4.x+ a MSBuild 15.1 +, které jsou součástí Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="c4f9d-128">Available only in NuGet 4.x+ and MSBuild 15.1+, which are included with Visual Studio 2017.</span></span> <span data-ttu-id="c4f9d-129">`nuget restore`a `dotnet restore` obě tento příkaz použijte pro příslušné projekty.</span><span class="sxs-lookup"><span data-stu-id="c4f9d-129">`nuget restore` and `dotnet restore` both use this command for applicable projects.</span></span>

- <span data-ttu-id="c4f9d-130">**Visual Studio Team Services**: při vytváření definice sestavení v Team Services, zahrnují [obnovení NuGet](/vsts/build-release/tasks/package/nuget#restore-nuget-packages) nebo [.NET Core obnovit](/vsts/build-release/tasks/build/dotnet-core#restore-nuget-packages) úloh v definici před všechny úloze sestavení.</span><span class="sxs-lookup"><span data-stu-id="c4f9d-130">**Visual Studio Team Services**: When creating a build definition on Team Services, include the [NuGet restore](/vsts/build-release/tasks/package/nuget#restore-nuget-packages) or [.NET Core Restore](/vsts/build-release/tasks/build/dotnet-core#restore-nuget-packages) task in the definition before any build task.</span></span> <span data-ttu-id="c4f9d-131">Tato úloha je zahrnutá ve výchozím nastavení v počet šablony sestavení.</span><span class="sxs-lookup"><span data-stu-id="c4f9d-131">This task is included by default in a number of build templates.</span></span>

- <span data-ttu-id="c4f9d-132">**Team Foundation Server**: TFS 2013 a novější automaticky obnoví balíčky během vytváření sestavení, za předpokladu, že používáte-li vytvořit šablonu Team sady TFS 2013 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="c4f9d-132">**Team Foundation Server**: TFS 2013 and later automatically restores packages during build, provided that you're using a Team Build Template for TFS 2013 or later.</span></span> <span data-ttu-id="c4f9d-133">Pro starší verzi sady TFS můžete zahrnout krok sestavení vyvolat jeden z výše uvedených možností příkazového řádku obnovení.</span><span class="sxs-lookup"><span data-stu-id="c4f9d-133">For earlier version of TFS, you can include a build step to invoke one of the command-line restore options above.</span></span> <span data-ttu-id="c4f9d-134">Volitelně můžete migrovat šablony sestavení TFS 2013.</span><span class="sxs-lookup"><span data-stu-id="c4f9d-134">You can optionally migrate the build template to TFS 2013.</span></span> <span data-ttu-id="c4f9d-135">Další informace najdete v tématu [návod obnovení balíčků s Team Foundation Build](../consume-packages/team-foundation-build.md).</span><span class="sxs-lookup"><span data-stu-id="c4f9d-135">For more information, see the [Walkthrough of package restore with Team Foundation Build](../consume-packages/team-foundation-build.md).</span></span>

## <a name="enabling-and-disabling-package-restore"></a><span data-ttu-id="c4f9d-136">Povolení a zákaz obnovení balíčků</span><span class="sxs-lookup"><span data-stu-id="c4f9d-136">Enabling and disabling package restore</span></span>

<span data-ttu-id="c4f9d-137">Obnovení balíčku je primárně povolená díky **nástroje > Možnosti > Správce balíčků NuGet** v sadě Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="c4f9d-137">Package restore is primarily enabled through **Tools > Options > NuGet Package Manager** in Visual Studio:</span></span>

![Řízení chování obnovení balíčku prostřednictvím možnosti Správce balíčků NuGet](media/Restore-01-AutoRestoreOptions.png)

- <span data-ttu-id="c4f9d-139">**Povolit aplikaci NuGet stáhnout chybějící balíčky**: řídí všechny formy obnovení balíčků změnou `packageRestore/enabled` nastavení v `%AppData%\NuGet\NuGet.Config` souboru, jak je uvedeno níže.</span><span class="sxs-lookup"><span data-stu-id="c4f9d-139">**Allow NuGet to download missing packages**: controls all forms of package restore by changing the `packageRestore/enabled` setting in the `%AppData%\NuGet\NuGet.Config` file as shown below.</span></span>

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
    >  <span data-ttu-id="c4f9d-140">`packageRestore/enabled` Nastavení je možné přepsat globálně nastavením proměnné prostředí názvem **EnableNuGetPackageRestore** s hodnotou PRAVDA nebo NEPRAVDA před spuštění sady Visual Studio nebo spuštění sestavení.</span><span class="sxs-lookup"><span data-stu-id="c4f9d-140">The `packageRestore/enabled` setting can be overridden globally by setting an environment variable called **EnableNuGetPackageRestore** with a value of TRUE or FALSE before launching Visual Studio or starting a build.</span></span>

- <span data-ttu-id="c4f9d-141">**Automaticky Zkontrolujte chybějící balíčky během sestavení v sadě Visual Studio**: ovládací prvky Automatické obnovení změnou `packageRestore/automatic` nastavení v `%AppData%\NuGet\NuGet.Config` souboru, jak je uvedeno níže.</span><span class="sxs-lookup"><span data-stu-id="c4f9d-141">**Automatically check for missing packages during build in Visual Studio**: controls automatic restore by changing the `packageRestore/automatic` setting in the `%AppData%\NuGet\NuGet.Config` file as shown below.</span></span>

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

<span data-ttu-id="c4f9d-142">Odkaz, najdete v článku [NuGet konfiguračního souboru – část packageRestore](../Schema/nuget-config-file.md#packagerestore-section).</span><span class="sxs-lookup"><span data-stu-id="c4f9d-142">For reference, see the [NuGet config file - packageRestore section](../Schema/nuget-config-file.md#packagerestore-section).</span></span>

<span data-ttu-id="c4f9d-143">V některých případech vývojáře nebo společnosti chtít povolit nebo zakázat obnovení balíčku pro všechny uživatele v počítači.</span><span class="sxs-lookup"><span data-stu-id="c4f9d-143">In some cases, a developer or company might want to enable or disable package restore for all users on a computer.</span></span> <span data-ttu-id="c4f9d-144">To se provádí přidáním globální NuGet konfigurační soubor umístěný ve stejné nastavení výše `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`.</span><span class="sxs-lookup"><span data-stu-id="c4f9d-144">This is done by adding the same settings above to the global NuGet configuration file located in `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`.</span></span> <span data-ttu-id="c4f9d-145">Jednotlivým uživatelům můžete selektivně povolte obnovení podle potřeby na úrovni projektu.</span><span class="sxs-lookup"><span data-stu-id="c4f9d-145">Individual users can then selectively enable restore as needed on a project level.</span></span> <span data-ttu-id="c4f9d-146">V tématu [konfigurace NuGet chování](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) přesné informace o tom, jak NuGet upřednostňuje více konfigurační soubory.</span><span class="sxs-lookup"><span data-stu-id="c4f9d-146">See [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) for exact details on how NuGet prioritizes multiple config files.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="c4f9d-147">Omezení verze balíčku s obnovením</span><span class="sxs-lookup"><span data-stu-id="c4f9d-147">Constraining package versions with restore</span></span>

<span data-ttu-id="c4f9d-148">Při obnovování balíčků pomocí libovolné metody, NuGet ctí žádná omezení, zadaný v `packages.config` nebo souboru projektu:</span><span class="sxs-lookup"><span data-stu-id="c4f9d-148">When restoring packages through any method, NuGet honors any constraints specified in `packages.config` or the project file:</span></span>

- <span data-ttu-id="c4f9d-149">`packages.config`: Určete rozsah verze v `allowedVersion` vlastnost závislosti.</span><span class="sxs-lookup"><span data-stu-id="c4f9d-149">`packages.config`: Specify a version range in the `allowedVersion` property of the dependency.</span></span> <span data-ttu-id="c4f9d-150">V tématu [Reinstalling a aktualizaci balíčků](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span><span class="sxs-lookup"><span data-stu-id="c4f9d-150">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="c4f9d-151">Příklad:</span><span class="sxs-lookup"><span data-stu-id="c4f9d-151">For example:</span></span>

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- <span data-ttu-id="c4f9d-152">PackageReference: Zadejte verzi rozsah přímo s číslem verze této závislosti.</span><span class="sxs-lookup"><span data-stu-id="c4f9d-152">PackageReference: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="c4f9d-153">Příklad:</span><span class="sxs-lookup"><span data-stu-id="c4f9d-153">For example:</span></span>

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

<span data-ttu-id="c4f9d-154">Ve všech případech, použijte zápis popsané v [Správa verzí balíčku](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="c4f9d-154">In all cases, use the notation described in [Package versioning](../reference/package-versioning.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="c4f9d-155">Poradce při potížích</span><span class="sxs-lookup"><span data-stu-id="c4f9d-155">Troubleshooting</span></span>

<span data-ttu-id="c4f9d-156">V tématu [řešení potíží s obnovení balíčků](Package-restore-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="c4f9d-156">See [Troubleshooting package restore](Package-restore-troubleshooting.md).</span></span>