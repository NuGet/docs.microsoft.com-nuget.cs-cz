---
title: Migrace z package.config do formátů PackageReference | Microsoft Docs
author: karann-msft
ms.author: karann
manager: unniravindranathan
ms.date: 03/27/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Podrobnosti o tom, jak migrovat projektu z formátu package.config správy do PackageReference podporuje NuGet 4.0 + a VS2017 a .NET Core 2.0
keywords: NuGet migrator migrovat, balíček odkazy, projektu soubory, PackageReference, souboru packages.config, VS2017, Visual Studio 2017, NuGet 4, .NET Core 2.0
ms.reviewer:
- karann
- unnir
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 10bd2fe95a6af11806a7edd7a43eaa497486fd80
ms.sourcegitcommit: ecb598c790d4154366bc92757ec7db1a51c34faf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/03/2018
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a><span data-ttu-id="5a9cb-104">Migrovat ze souboru packages.config PackageReference</span><span class="sxs-lookup"><span data-stu-id="5a9cb-104">Migrate from packages.config to PackageReference</span></span>

<span data-ttu-id="5a9cb-105">Visual Studio 2017 verze 15.7 Preview 3 a novějších verzích podporuje migraci z projektu [packages.config](./packages-config.md) správu formát, který se [PackageReference](../consume-packages/Package-References-in-Project-Files.md) formátu.</span><span class="sxs-lookup"><span data-stu-id="5a9cb-105">Visual Studio 2017 Version 15.7 Preview 3 and later supports migrating a project from the [packages.config](./packages-config.md) management format to the [PackageReference](../consume-packages/Package-References-in-Project-Files.md) format.</span></span>

## <a name="benefits-of-using-packagereference"></a><span data-ttu-id="5a9cb-106">Výhody použití PackageReference</span><span class="sxs-lookup"><span data-stu-id="5a9cb-106">Benefits of using PackageReference</span></span>

* <span data-ttu-id="5a9cb-107">**Spravovat všechny závislosti projektu na jednom místě**: stejně jako odkazy na projekt na projekt a odkazy na sestavení, odkazuje na balíček NuGet (pomocí `PackageReference` uzlu) spravuje přímo v rámci soubory projektu, nikoli pomocí samostatné soubor Packages.config.</span><span class="sxs-lookup"><span data-stu-id="5a9cb-107">**Manage all project dependencies in one place**: Just like project to project references and assembly references, NuGet package references (using the `PackageReference` node) are managed directly within project files rather than using a separate packages.config file.</span></span>
* <span data-ttu-id="5a9cb-108">**Přeplněná zobrazení nejvyšší úrovně závislosti**: na rozdíl od souboru packages.config, PackageReference uvádí jenom tyto balíčky NuGet, které jsou přímo nainstalované v projektu.</span><span class="sxs-lookup"><span data-stu-id="5a9cb-108">**Uncluttered view of top-level dependencies**: Unlike packages.config, PackageReference lists only those NuGet packages you directly installed in the project.</span></span> <span data-ttu-id="5a9cb-109">V důsledku toho uživatelského rozhraní Správce balíčků NuGet a soubor projektu nejsou zaplněny závislosti nižší úrovně.</span><span class="sxs-lookup"><span data-stu-id="5a9cb-109">As a result, the NuGet Package Manager UI and the project file aren't cluttered with down-level dependencies.</span></span>
* <span data-ttu-id="5a9cb-110">**Vylepšení výkonu**: při použití PackageReference, balíčky jsou zachována ve *globální balíčky* složky (jak je popsáno na [správy globální balíčky a složky mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md) spíše než v `packages` složku v rámci řešení.</span><span class="sxs-lookup"><span data-stu-id="5a9cb-110">**Performance improvements**: When using PackageReference, packages are maintained in the *global-packages* folder (as described on [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md) rather than in a `packages` folder within the solution.</span></span> <span data-ttu-id="5a9cb-111">V důsledku toho PackageReference rychlejší a odebírá méně místa na disku.</span><span class="sxs-lookup"><span data-stu-id="5a9cb-111">As a result, PackageReference performs faster and consumes less disk space.</span></span>
* <span data-ttu-id="5a9cb-112">**Přesně řídit závislosti a obsahu toku**: použití stávajících funkcí nástroje MSBuild umožňuje [podmíněně odkazují na balíček NuGet](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) a vyberte balíček odkazuje na cílové rozhraní, konfiguraci, platformy, nebo jiné pivotů.</span><span class="sxs-lookup"><span data-stu-id="5a9cb-112">**Fine control over dependencies and content flow**: Using the existing features of MSBuild allows you to [conditionally reference a NuGet package](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) and choose package references per target framework, configuration, platform, or other pivots.</span></span>
* <span data-ttu-id="5a9cb-113">**PackageReference je ve vývoji active**: najdete v části [PackageReference problémy na Githubu](https://aka.ms/nuget-pr-improvements).</span><span class="sxs-lookup"><span data-stu-id="5a9cb-113">**PackageReference is under active development**: See [PackageReference issues on GitHub](https://aka.ms/nuget-pr-improvements).</span></span> <span data-ttu-id="5a9cb-114">soubor Packages.config se už vyvíjí aktivní.</span><span class="sxs-lookup"><span data-stu-id="5a9cb-114">packages.config is no longer under active development.</span></span>

### <a name="limitations"></a><span data-ttu-id="5a9cb-115">Omezení</span><span class="sxs-lookup"><span data-stu-id="5a9cb-115">Limitations</span></span>

* <span data-ttu-id="5a9cb-116">NuGet PackageReference není k dispozici v sadě Visual Studio 2015 a starší.</span><span class="sxs-lookup"><span data-stu-id="5a9cb-116">NuGet PackageReference is not available in Visual Studio 2015 and earlier.</span></span> <span data-ttu-id="5a9cb-117">Migrované projekty může otevřít pouze v Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="5a9cb-117">Migrated projects can be opened only in Visual Studio 2017.</span></span>
* <span data-ttu-id="5a9cb-118">Migrace není aktuálně k dispozici pro projekt C++ a ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="5a9cb-118">Migration is not currently available for C++ and ASP.NET project.</span></span>
* <span data-ttu-id="5a9cb-119">Některé balíčky nemusí být plně kompatibilní s PackageReference.</span><span class="sxs-lookup"><span data-stu-id="5a9cb-119">Some packages may not be fully compatible with PackageReference.</span></span> <span data-ttu-id="5a9cb-120">Další informace najdete v tématu [balíček problémy s kompatibilitou](#package-compatibility-issues).</span><span class="sxs-lookup"><span data-stu-id="5a9cb-120">For more information, see [package compatibility issues](#package-compatibility-issues).</span></span>

## <a name="migration-steps"></a><span data-ttu-id="5a9cb-121">Kroky migrace</span><span class="sxs-lookup"><span data-stu-id="5a9cb-121">Migration steps</span></span>

> [!Note]
> <span data-ttu-id="5a9cb-122">Před zahájením migrace, Visual Studio vytvoří zálohu projektu umožňují [vrácení zpět do souboru packages.config](#how-to-roll-back-to-packagesconfig) v případě potřeby.</span><span class="sxs-lookup"><span data-stu-id="5a9cb-122">Before migration begins, Visual Studio creates a backup of the project to allow you to [roll back to packages.config](#how-to-roll-back-to-packagesconfig) if necessary.</span></span>

1. <span data-ttu-id="5a9cb-123">Otevřete řešení obsahující projekt pomocí `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="5a9cb-123">Open a solution containing project using `packages.config`.</span></span>

1. <span data-ttu-id="5a9cb-124">V **Průzkumníku řešení**, klikněte pravým tlačítkem na **odkazy** uzlu nebo `packages.config` soubor a vyberte **migrovat souboru packages.config PackageReference...** .</span><span class="sxs-lookup"><span data-stu-id="5a9cb-124">In **Solution Explorer**, right-click on the **References** node or the `packages.config` file and select **Migrate packages.config to PackageReference...**.</span></span>

1. <span data-ttu-id="5a9cb-125">Migrator analyzuje odkazy na balíček NuGet projektu a pokusí se zařadit do **nejvyšší úrovně závislosti** (balíčky NuGet tento adresář můžete nainstalovat) a **přenositelné závislosti**(balíčky, které byly nainstalovány jako závislých součástí pro balíčky nejvyšší úrovně).</span><span class="sxs-lookup"><span data-stu-id="5a9cb-125">The migrator analyzes the project's NuGet package references and attempts to categorize them into **Top-level dependencies** (NuGet packages that you installed directory) and **Transitive dependencies** (packages that were installed as dependencies of top-level packages).</span></span>

   > [!Note]
   > <span data-ttu-id="5a9cb-126">PackageReference podporuje obnovení přenositelné balíčku a přeloží závislosti dynamicky, což znamená, že explicitně nemusí nainstalované přenositelné závislosti.</span><span class="sxs-lookup"><span data-stu-id="5a9cb-126">PackageReference supports transitive package restore and resolves dependencies dynamically, meaning that transitive dependencies need not be installed explicitly.</span></span>

1. <span data-ttu-id="5a9cb-127">(Volitelné) Můžete se rozhodnout zacházet s balíčku NuGet jsou klasifikovány jako závislost přenositelné jako závislost nejvyšší úrovně výběrem **nejvyšší úrovně** možnost pro balíček.</span><span class="sxs-lookup"><span data-stu-id="5a9cb-127">(Optional) You may choose to treat a NuGet package classified as a transitive dependency as a top-level dependency by selecting the **Top-Level** option for the package.</span></span> <span data-ttu-id="5a9cb-128">Tato možnost bude automaticky nastavena pro balíčky, které obsahují prostředky, které není toku přechodně (ty v `build`, `buildCrossTargeting`, `contentFiles`, nebo `analyzers` složky) a ty označen jako závislost vývoj (`developmentDependency = "true"`).</span><span class="sxs-lookup"><span data-stu-id="5a9cb-128">This option is automatically set for packages containing assets that do not flow transitively (those in the `build`, `buildCrossTargeting`, `contentFiles`, or `analyzers` folders) and those marked as a development dependency (`developmentDependency = "true"`).</span></span>

1. <span data-ttu-id="5a9cb-129">Zkontrolujte všechny [balíček problémy s kompatibilitou](#package-compatibility-issues).</span><span class="sxs-lookup"><span data-stu-id="5a9cb-129">Review any [package compatibility issues](#package-compatibility-issues).</span></span>

1. <span data-ttu-id="5a9cb-130">Vyberte **OK** zahájíte migrace.</span><span class="sxs-lookup"><span data-stu-id="5a9cb-130">Select **OK** to begin the migration.</span></span>

1. <span data-ttu-id="5a9cb-131">Na konci migrace Visual Studio poskytuje sestavy s cestou k zálohování, seznam balíčků nainstalovaných (nejvyšší úrovně závislosti), seznam balíčků na něj odkazuje jako přenositelné závislosti a seznam na začátku identifikovat problémy s kompatibilitou migrace.</span><span class="sxs-lookup"><span data-stu-id="5a9cb-131">At the end of the migration, Visual Studio provides a report with a path to the backup, the list of installed packages (top-level dependencies), a list of packages referenced as transitive dependencies, and a list of compatibility issues identified at the start of migration.</span></span> <span data-ttu-id="5a9cb-132">Sestava je uložena v zálohovací složce.</span><span class="sxs-lookup"><span data-stu-id="5a9cb-132">The report is saved to the backup folder.</span></span>

1. <span data-ttu-id="5a9cb-133">Ověřte, zda řešení vytvoří a spustí.</span><span class="sxs-lookup"><span data-stu-id="5a9cb-133">Validate that the solution builds and runs.</span></span> <span data-ttu-id="5a9cb-134">Pokud narazíte na potíže, [souboru problém na Githubu](https://github.com/NuGet/Home/issues/).</span><span class="sxs-lookup"><span data-stu-id="5a9cb-134">If you encounter problems, [file an issue on GitHub](https://github.com/NuGet/Home/issues/).</span></span>

## <a name="how-to-roll-back-to-packagesconfig"></a><span data-ttu-id="5a9cb-135">Postup vrácení souboru Packages.config je.</span><span class="sxs-lookup"><span data-stu-id="5a9cb-135">How to roll back to packages.config</span></span>

1. <span data-ttu-id="5a9cb-136">Zavřete migrované projektu.</span><span class="sxs-lookup"><span data-stu-id="5a9cb-136">Close the migrated project.</span></span>

1. <span data-ttu-id="5a9cb-137">Zkopírujte soubor projektu a `packages.config` ze zálohy (obvykle `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) ke složce projektu.</span><span class="sxs-lookup"><span data-stu-id="5a9cb-137">Copy the project file and `packages.config` from the backup (typically `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) to the project folder.</span></span>

1. <span data-ttu-id="5a9cb-138">Otevřete projekt.</span><span class="sxs-lookup"><span data-stu-id="5a9cb-138">Open the project.</span></span>

1. <span data-ttu-id="5a9cb-139">Otevřete konzolu Správce balíčků pomocí **nástroje > Správce balíčků NuGet > Konzola správce balíčků** příkazu nabídky.</span><span class="sxs-lookup"><span data-stu-id="5a9cb-139">Open the Package Manager Console using the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="5a9cb-140">V konzole, spusťte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="5a9cb-140">Run the following command in the Console:</span></span>

   ```ps
   update-package -reinstall
   ```

## <a name="package-compatibility-issues"></a><span data-ttu-id="5a9cb-141">Problémy s kompatibilitou balíčku</span><span class="sxs-lookup"><span data-stu-id="5a9cb-141">Package compatibility issues</span></span>

<span data-ttu-id="5a9cb-142">PackageReference nepodporuje některé aspekty, které byly k dispozici v souboru Packages.config je.</span><span class="sxs-lookup"><span data-stu-id="5a9cb-142">Some aspects that were supported in packages.config are not supported in PackageReference.</span></span> <span data-ttu-id="5a9cb-143">Migrator analyzuje a zjistí tyto problémy.</span><span class="sxs-lookup"><span data-stu-id="5a9cb-143">The migrator analyzes and detects such issues.</span></span> <span data-ttu-id="5a9cb-144">Všechny balíček, který má jeden nebo více z následujících důvodů nefungují dle očekávání po migraci.</span><span class="sxs-lookup"><span data-stu-id="5a9cb-144">Any package that has one or more of the following issues may not behave as expected after the migration.</span></span>

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="5a9cb-145">"install.ps1" skripty jsou ignorovány, při instalaci balíčku po migraci</span><span class="sxs-lookup"><span data-stu-id="5a9cb-145">"install.ps1" scripts are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5a9cb-146">**Popis**</span><span class="sxs-lookup"><span data-stu-id="5a9cb-146">**Description**</span></span> | <span data-ttu-id="5a9cb-147">S PackageReference nejsou při instalování nebo odinstalování balíčku provést install.ps1 a uninstall.ps1 skriptů prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5a9cb-147">With PackageReference, install.ps1 and uninstall.ps1 PowerShell scripts are not executed while installing or uninstalling a package.</span></span> |
| <span data-ttu-id="5a9cb-148">**Potenciální dopad**</span><span class="sxs-lookup"><span data-stu-id="5a9cb-148">**Potential impact**</span></span> | <span data-ttu-id="5a9cb-149">Balíčky, které jsou závislé na tyto skripty ke konfiguraci některých chování v cílovém projektu nemusí fungovat podle očekávání.</span><span class="sxs-lookup"><span data-stu-id="5a9cb-149">Packages that depend on these scripts to configure some behavior in the destination project might not work as expected.</span></span> |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="5a9cb-150">"obsah" prostředky nejsou k dispozici při instalaci balíčku po migraci</span><span class="sxs-lookup"><span data-stu-id="5a9cb-150">"content" assets are not available when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5a9cb-151">**Popis**</span><span class="sxs-lookup"><span data-stu-id="5a9cb-151">**Description**</span></span> | <span data-ttu-id="5a9cb-152">Prostředky v balíčku na `content` složky nejsou podporovány s PackageReference a budou ignorovány.</span><span class="sxs-lookup"><span data-stu-id="5a9cb-152">Assets in a package's `content` folder are not supported with PackageReference and are ignored.</span></span> <span data-ttu-id="5a9cb-153">PackageReference přidává podporu pro `contentFiles` lépe přenositelné podporu a sdíleného obsahu.</span><span class="sxs-lookup"><span data-stu-id="5a9cb-153">PackageReference adds support for `contentFiles` to have better transitive support and shared content.</span></span>  |
| <span data-ttu-id="5a9cb-154">**Potenciální dopad**</span><span class="sxs-lookup"><span data-stu-id="5a9cb-154">**Potential impact**</span></span> | <span data-ttu-id="5a9cb-155">Prostředky v `content` nebudou zkopírovány do projekt a projekt vyžaduje refaktoring kód, který závisí na přítomnost tyto prostředky.</span><span class="sxs-lookup"><span data-stu-id="5a9cb-155">Assets in `content` are not copied into the project and project code that depends on the presence of those assets requires refactoring.</span></span>  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a><span data-ttu-id="5a9cb-156">Při instalaci balíčku po upgradu neaplikují XDT transformací</span><span class="sxs-lookup"><span data-stu-id="5a9cb-156">XDT transforms are not applied when the package is installed after the upgrade</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5a9cb-157">**Popis**</span><span class="sxs-lookup"><span data-stu-id="5a9cb-157">**Description**</span></span> | <span data-ttu-id="5a9cb-158">Transformace XDT nepodporuje PackageReference a `.xdt` soubory jsou při instalování nebo odinstalování balíčku ignorovány.</span><span class="sxs-lookup"><span data-stu-id="5a9cb-158">XDT transforms are not supported with PackageReference and `.xdt` files are ignored when installing or uninstalling a package.</span></span>   |
| <span data-ttu-id="5a9cb-159">**Potenciální dopad**</span><span class="sxs-lookup"><span data-stu-id="5a9cb-159">**Potential impact**</span></span> | <span data-ttu-id="5a9cb-160">Transformace XDT nejsou použity pro všechny soubory XML projektu nejčastěji `web.config.install.xdt` a `web.config.uninstall.xdt`, což znamená, že projektu` web.config` souboru nebudou aktualizovány, jestliže tento balíček je nainstalována nebo odinstalována.</span><span class="sxs-lookup"><span data-stu-id="5a9cb-160">XDT transforms are not applied to any project XML files, most commonly, `web.config.install.xdt` and `web.config.uninstall.xdt`, which means the project's` web.config` file is not updated when the package is installed or uninstalled.</span></span> |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="5a9cb-161">Při instalaci balíčku po migraci jsou ignorovány sestavení v kořenovém adresáři lib</span><span class="sxs-lookup"><span data-stu-id="5a9cb-161">Assemblies in the lib root are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5a9cb-162">**Popis**</span><span class="sxs-lookup"><span data-stu-id="5a9cb-162">**Description**</span></span> | <span data-ttu-id="5a9cb-163">Sestavení s PackageReference, k dispozici v kořenovém adresáři `lib` bez cílový framework konkrétní dílčí složku složky jsou ignorovány.</span><span class="sxs-lookup"><span data-stu-id="5a9cb-163">With PackageReference, assemblies present at the root of `lib` folder without a target framework specific sub-folder are ignored.</span></span> <span data-ttu-id="5a9cb-164">NuGet hledá podsložky odpovídající odpovídající cílový framework projektu na Přezdívka cílový framework (TFM) a nainstaluje odpovídající sestavení do projektu.</span><span class="sxs-lookup"><span data-stu-id="5a9cb-164">NuGet looks for a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework and installs the matching assemblies into the project.</span></span> |
| <span data-ttu-id="5a9cb-165">**Potenciální dopad**</span><span class="sxs-lookup"><span data-stu-id="5a9cb-165">**Potential impact**</span></span> | <span data-ttu-id="5a9cb-166">Balíčky, které nemají odpovídající Přezdívka cílový framework (TFM) odpovídající cílový framework projektu na podsložku nemusí chovat podle očekávání po přechodu nebo selhání instalace během migrace</span><span class="sxs-lookup"><span data-stu-id="5a9cb-166">Packages that do not have a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework may not behave as expected after the transition or fail installation during the migration</span></span> |

## <a name="found-an-issue-report-it"></a><span data-ttu-id="5a9cb-167">Našel problém?</span><span class="sxs-lookup"><span data-stu-id="5a9cb-167">Found an issue?</span></span> <span data-ttu-id="5a9cb-168">Nahlaste to!</span><span class="sxs-lookup"><span data-stu-id="5a9cb-168">Report it!</span></span>

<span data-ttu-id="5a9cb-169">Pokud narazíte na potíže s prostředím migrace, [souborů problém v úložišti NuGet GitHub](https://github.com/NuGet/Home/issues/).</span><span class="sxs-lookup"><span data-stu-id="5a9cb-169">If you run into a problem with the migration experience, please [file an issue on the NuGet GitHub repository](https://github.com/NuGet/Home/issues/).</span></span>
