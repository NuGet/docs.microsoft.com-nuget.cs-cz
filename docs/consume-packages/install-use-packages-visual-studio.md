---
title: Instalace a správa balíčků NuGet v sadě Visual Studio
description: Pokyny pro použití nuget správce balíčků ui v sadě Visual Studio pro práci s balíčky NuGet.
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 3adceac8c725d9ea1610aea090753c9c1d8bc818
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428693"
---
# <a name="install-and-manage-packages-in-visual-studio-using-the-nuget-package-manager"></a><span data-ttu-id="0b2db-103">Instalace a správa balíčků v sadě Visual Studio pomocí Správce balíčků NuGet</span><span class="sxs-lookup"><span data-stu-id="0b2db-103">Install and manage packages in Visual Studio using the NuGet Package Manager</span></span>

<span data-ttu-id="0b2db-104">NuGet Package Manager UI v sadě Visual Studio v systému Windows umožňuje snadno nainstalovat, odinstalovat a aktualizovat balíčky NuGet v projektech a řešeních.</span><span class="sxs-lookup"><span data-stu-id="0b2db-104">The NuGet Package Manager UI in Visual Studio on Windows allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="0b2db-105">Zkušenosti v Visual Studiu pro Mac najdete [v tématu zahrnutí balíčku NuGet v projektu](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json).</span><span class="sxs-lookup"><span data-stu-id="0b2db-105">For the experience in Visual Studio for Mac, see [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json).</span></span> <span data-ttu-id="0b2db-106">Ui Správce balíčků není součástí kódu sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0b2db-106">The Package Manager UI is not included with Visual Studio Code.</span></span>

> [!NOTE]
> <span data-ttu-id="0b2db-107">Pokud vám chybí Správce balíčků NuGet ve Visual Studiu 2015, zkontrolujte **nástroje > rozšíření a aktualizace...** a vyhledejte rozšíření *NuGet Package Manager.*</span><span class="sxs-lookup"><span data-stu-id="0b2db-107">If you're missing the NuGet Package Manager in Visual Studio 2015, check **Tools > Extensions and Updates...** and search for the *NuGet Package Manager* extension.</span></span> <span data-ttu-id="0b2db-108">Pokud se vám nedaří použít instalační program rozšíření v sadě [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)Visual Studio, stáhněte si rozšíření přímo z aplikace .</span><span class="sxs-lookup"><span data-stu-id="0b2db-108">If you're unable to use the extensions installer in Visual Studio, download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>
>
> <span data-ttu-id="0b2db-109">Počínaje Visual Studio 2017, NuGet a NuGet Správce balíčků jsou automaticky nainstalovány s libovolným . NET související s úlohami.</span><span class="sxs-lookup"><span data-stu-id="0b2db-109">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed with any .NET-related workloads.</span></span> <span data-ttu-id="0b2db-110">Nainstalujte ji jednotlivě výběrem **jednotlivých součástí > nástroje Code >** možnost i správce balíčků NuGet v instalačním programu sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0b2db-110">Install it individually by selecting the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

## <a name="find-and-install-a-package"></a><span data-ttu-id="0b2db-111">Vyhledání a instalace balíčku</span><span class="sxs-lookup"><span data-stu-id="0b2db-111">Find and install a package</span></span>

1. <span data-ttu-id="0b2db-112">V **Průzkumníku řešení**klepněte pravým tlačítkem myši na **odkazy** nebo na projekt a vyberte **spravovat balíčky NuGet...**.</span><span class="sxs-lookup"><span data-stu-id="0b2db-112">In **Solution Explorer**, right-click either **References**  or a project and select **Manage NuGet Packages...**.</span></span>

    ![Možnost nabídky Spravovat balíčky NuGet](media/ManagePackagesUICommand.png)

1. <span data-ttu-id="0b2db-114">Na kartě **Procházet** se zobrazí balíčky podle oblíbenosti z aktuálně vybraného zdroje (viz [zdroje balíčků](#package-sources)).</span><span class="sxs-lookup"><span data-stu-id="0b2db-114">The **Browse** tab displays packages by popularity from the currently selected source (see [package sources](#package-sources)).</span></span> <span data-ttu-id="0b2db-115">Vyhledejte konkrétní balíček pomocí vyhledávacího pole v levém horním rohu.</span><span class="sxs-lookup"><span data-stu-id="0b2db-115">Search for a specific package using the search box on the upper left.</span></span> <span data-ttu-id="0b2db-116">Vyberte balíček ze seznamu, chcete-li zobrazit jeho informace, což také umožňuje **tlačítko Instalovat** spolu s rozevíracím seznamem výběr verze.</span><span class="sxs-lookup"><span data-stu-id="0b2db-116">Select a package from the list to display its information, which also enables the **Install** button along with a version-selection drop-down.</span></span>

    ![Karta Procházet dialogové okno Spravovat balíčky nugetů](media/Search.png)

1. <span data-ttu-id="0b2db-118">V rozevíracím souboru vyberte požadovanou verzi a vyberte **Instalovat**.</span><span class="sxs-lookup"><span data-stu-id="0b2db-118">Select the desired version from the drop-down and select **Install**.</span></span> <span data-ttu-id="0b2db-119">Visual Studio nainstaluje balíček a jeho závislosti do projektu.</span><span class="sxs-lookup"><span data-stu-id="0b2db-119">Visual Studio installs the package and its dependencies into the project.</span></span> <span data-ttu-id="0b2db-120">Můžete být požádáni o přijetí licenčních podmínek.</span><span class="sxs-lookup"><span data-stu-id="0b2db-120">You may be asked to accept license terms.</span></span> <span data-ttu-id="0b2db-121">Po dokončení instalace se přidané balíčky zobrazí na kartě **Nainstalováno.** Balíčky jsou také **uvedeny** v uzlu Reference `using` průzkumníka řešení, což znamená, že na ně můžete odkazovat v projektu s příkazy.</span><span class="sxs-lookup"><span data-stu-id="0b2db-121">When installation is complete, the added packages appear on the **Installed** tab. Packages are also listed in the **References** node of Solution Explorer, indicating that you can refer to them in the project with `using` statements.</span></span>

    ![Odkazy v Průzkumníku řešení](media/References.png)

> [!Tip]
> <span data-ttu-id="0b2db-123">Chcete-li do hledání zahrnout předběžné verze a zpřístupnit předběžné verze v rozevíracím souboru verze, vyberte možnost **Zahrnout předběžnou verzi.**</span><span class="sxs-lookup"><span data-stu-id="0b2db-123">To include prerelease versions in the search, and to make prerelease versions available in the version drop-down, select the **Include prerelease** option.</span></span>

> [!Note]
> <span data-ttu-id="0b2db-124">NuGet má dva formáty, ve kterých může projekt používat balíčky: [`PackageReference`](package-references-in-project-files.md) a [`packages.config`](../reference/packages-config.md).</span><span class="sxs-lookup"><span data-stu-id="0b2db-124">NuGet has two formats in which a project may use packages: [`PackageReference`](package-references-in-project-files.md) and [`packages.config`](../reference/packages-config.md).</span></span> <span data-ttu-id="0b2db-125">[Výchozí nastavení lze nastavit v okně možností sady Visual Studio](Package-Restore.md#choose-default-package-management-format).</span><span class="sxs-lookup"><span data-stu-id="0b2db-125">[The default can be set in Visual Studio's options window](Package-Restore.md#choose-default-package-management-format).</span></span>

## <a name="uninstall-a-package"></a><span data-ttu-id="0b2db-126">Odinstalace balíčku</span><span class="sxs-lookup"><span data-stu-id="0b2db-126">Uninstall a package</span></span>

1. <span data-ttu-id="0b2db-127">V **Průzkumníku řešení**klepněte pravým tlačítkem myši na **odkazy** nebo na požadovaný projekt a vyberte **spravovat balíčky NuGet...**.</span><span class="sxs-lookup"><span data-stu-id="0b2db-127">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="0b2db-128">Vyberte kartu **Nainstalováno**.</span><span class="sxs-lookup"><span data-stu-id="0b2db-128">Select the **Installed** tab.</span></span>
1. <span data-ttu-id="0b2db-129">Vyberte balíček, který chcete odinstalovat (v případě potřeby pomocí hledání seznam vyfiltrujte) a vyberte **Odinstalovat**.</span><span class="sxs-lookup"><span data-stu-id="0b2db-129">Select the package to uninstall (using search to filter the list if necessary) and select **Uninstall**.</span></span>

    ![Odinstalace balíčku](media/UninstallPackage.png)

1. <span data-ttu-id="0b2db-131">Všimněte si, že **zahrnout předběžné verze** a **balíček zdrojové** ovládací prvky nemají žádný vliv při odinstalaci balíčků.</span><span class="sxs-lookup"><span data-stu-id="0b2db-131">Note that the **Include prerelease** and **Package source** controls have no effect when uninstalling packages.</span></span>

## <a name="update-a-package"></a><span data-ttu-id="0b2db-132">Aktualizace balíčku</span><span class="sxs-lookup"><span data-stu-id="0b2db-132">Update a package</span></span>

1. <span data-ttu-id="0b2db-133">V **Průzkumníku řešení**klepněte pravým tlačítkem myši na **odkazy** nebo na požadovaný projekt a vyberte **spravovat balíčky NuGet...**. (V projektech webu klikněte pravým tlačítkem myši na složku **Bin.)**</span><span class="sxs-lookup"><span data-stu-id="0b2db-133">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**. (In web site projects, right-click the **Bin** folder.)</span></span>
1. <span data-ttu-id="0b2db-134">Výběrem karty **Aktualizace** zobrazíte balíčky, které mají k dispozici aktualizace z vybraných zdrojů balíčků.</span><span class="sxs-lookup"><span data-stu-id="0b2db-134">Select the **Updates** tab to see packages that have available updates from the selected package sources.</span></span> <span data-ttu-id="0b2db-135">Vyberte **Zahrnout předběžnou verzi,** chcete-li do seznamu aktualizací zahrnout předběžné balíčky.</span><span class="sxs-lookup"><span data-stu-id="0b2db-135">Select **Include prerelease** to include prerelease packages in the update list.</span></span>
1. <span data-ttu-id="0b2db-136">Vyberte balíček, který chcete aktualizovat, vyberte požadovanou verzi z rozevíracího balíčku vpravo a vyberte **Aktualizovat**.</span><span class="sxs-lookup"><span data-stu-id="0b2db-136">Select the package to update, select the desired version from the drop-down on the right, and select **Update**.</span></span>

    ![Aktualizace balíčku](media/UpdatePackages.png)

1. <a name="implicit_reference"></a><span data-ttu-id="0b2db-138">U některých balíčků je zakázáno tlačítko **Aktualizovat** a zobrazí se zpráva, že je "Implicitně odkazováno sadou SDK" (nebo "AutoReferenced").</span><span class="sxs-lookup"><span data-stu-id="0b2db-138">For some packages, the **Update** button is disabled and a message appears saying that it's "Implicitly referenced by an SDK" (or "AutoReferenced").</span></span> <span data-ttu-id="0b2db-139">Tato zpráva označuje, že balíček je součástí větší rozhraní nebo sady SDK a by neměly být aktualizovány nezávisle.</span><span class="sxs-lookup"><span data-stu-id="0b2db-139">This message indicates that the package is part of a larger framework or SDK and should not be updated independently.</span></span> <span data-ttu-id="0b2db-140">(Tyto balíčky jsou `<IsImplicitlyDefined>True</IsImplicitlyDefined>`vnitřně označeny .) Například `Microsoft.NETCore.App` je součástí sady .NET Core SDK a verze balíčku není stejná jako verze rozhraní runtime, kterou používá aplikace.</span><span class="sxs-lookup"><span data-stu-id="0b2db-140">(Such packages are internally marked with `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) For example, `Microsoft.NETCore.App` is part of the .NET Core SDK, and the package version is not the same as the version of the runtime framework used by the application.</span></span> <span data-ttu-id="0b2db-141">Chcete-li získat nové verze ASP.NET core a .NET Core runtime, musíte [aktualizovat instalaci jádra .NET.](https://aka.ms/dotnet-download)</span><span class="sxs-lookup"><span data-stu-id="0b2db-141">You need to [update your .NET Core installation](https://aka.ms/dotnet-download) to get new versions of the ASP.NET Core and .NET Core runtime.</span></span> <span data-ttu-id="0b2db-142">[Další podrobnosti o metabalíčcích .NET Core a správě verzí](/dotnet/core/packages)naleznete v tomto dokumentu.</span><span class="sxs-lookup"><span data-stu-id="0b2db-142">[See this document for more details on .NET Core metapackages and versioning](/dotnet/core/packages).</span></span> <span data-ttu-id="0b2db-143">To platí pro následující běžně používané balíčky:</span><span class="sxs-lookup"><span data-stu-id="0b2db-143">This applies to the following commonly used packages:</span></span>
    * <span data-ttu-id="0b2db-144">Microsoft.AspNetCore.All</span><span class="sxs-lookup"><span data-stu-id="0b2db-144">Microsoft.AspNetCore.All</span></span>
    * <span data-ttu-id="0b2db-145">Microsoft.AspNetCore.App</span><span class="sxs-lookup"><span data-stu-id="0b2db-145">Microsoft.AspNetCore.App</span></span>
    * <span data-ttu-id="0b2db-146">Aplikace Microsoft.NETCore.App</span><span class="sxs-lookup"><span data-stu-id="0b2db-146">Microsoft.NETCore.App</span></span>
    * <span data-ttu-id="0b2db-147">NETStandard.Knihovna</span><span class="sxs-lookup"><span data-stu-id="0b2db-147">NETStandard.Library</span></span>

    ![Ukázkový balíček označený jako implicitně odkazy nebo AutoReferenced](media/PackageManagerUIAutoReferenced.png)

1. <span data-ttu-id="0b2db-149">Chcete-li aktualizovat více balíčků na jejich nejnovější verze, vyberte je v seznamu a vyberte tlačítko **Aktualizovat** nad seznamem.</span><span class="sxs-lookup"><span data-stu-id="0b2db-149">To update multiple packages to their newest versions, select  them in the list and select the **Update** button above the list.</span></span>
1. <span data-ttu-id="0b2db-150">Jednotlivé balíčky můžete také aktualizovat na kartě **Nainstalováno.** V tomto případě podrobnosti o balíčku zahrnují volič verze (s výhradou **include předběžné verze** možnost) a tlačítko **Aktualizovat.**</span><span class="sxs-lookup"><span data-stu-id="0b2db-150">You can also update an individual package from the **Installed** tab. In this case, the details for the package include a version selector (subject to the **Include prerelease** option) and an **Update** button.</span></span>

## <a name="manage-packages-for-the-solution"></a><span data-ttu-id="0b2db-151">Správa balíčků pro řešení</span><span class="sxs-lookup"><span data-stu-id="0b2db-151">Manage packages for the solution</span></span>

<span data-ttu-id="0b2db-152">Správa balíčků pro řešení je pohodlným prostředkem pro práci s více projekty současně.</span><span class="sxs-lookup"><span data-stu-id="0b2db-152">Managing packages for a solution is a convenient means to work with multiple projects simultaneously.</span></span>

1. <span data-ttu-id="0b2db-153">Vyberte **příkaz nabídky Nástroje > NuGet > Spravovat balíčky NuGet pro řešení...** nebo klepněte pravým tlačítkem myši na řešení a vyberte spravovat **balíčky NuGet...**:</span><span class="sxs-lookup"><span data-stu-id="0b2db-153">Select the **Tools > NuGet Package Manager > Manage NuGet Packages for Solution...** menu command, or right-click the solution and select **Manage NuGet Packages...**:</span></span>

    ![Správa balíčků NuGet pro řešení](media/ManagePackagesSolutionUICommand.png)

1. <span data-ttu-id="0b2db-155">Při správě balíčků pro řešení umožňuje unové oi vybrat projekty, které jsou ovlivněny operacemi:</span><span class="sxs-lookup"><span data-stu-id="0b2db-155">When managing packages for the solution, the UI lets you select the projects that are affected by the operations:</span></span>

    ![Výběr projektu při správě balíčků pro řešení](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a><span data-ttu-id="0b2db-157">Karta Konsolidovat</span><span class="sxs-lookup"><span data-stu-id="0b2db-157">Consolidate tab</span></span>

<span data-ttu-id="0b2db-158">Vývojáři obvykle považují za špatné praxe používat různé verze stejného balíčku NuGet napříč různými projekty ve stejném řešení.</span><span class="sxs-lookup"><span data-stu-id="0b2db-158">Developers typically consider it bad practice to use different versions of the same NuGet package across different projects in the same solution.</span></span> <span data-ttu-id="0b2db-159">Pokud se rozhodnete spravovat balíčky pro řešení, ui Správce balíčků poskytuje **kartu Konsolidovat,** na které můžete snadno zjistit, kde balíčky s odlišnými čísly verzí jsou používány různými projekty v řešení:</span><span class="sxs-lookup"><span data-stu-id="0b2db-159">When you choose to manage packages for a solution, the Package Manager UI provides a **Consolidate** tab on which you can easily see where packages with distinct version numbers are used by different projects in the solution:</span></span>

![Karta Konsolidovat ui správce balíčků](media/ConsolidateTab.png)

<span data-ttu-id="0b2db-161">V tomto příkladu classlibrary1 projekt používá EntityFramework 6.2.0, vzhledem k tomu, ConsoleApp1 používá EntityFramework 6.1.0.</span><span class="sxs-lookup"><span data-stu-id="0b2db-161">In this example, the ClassLibrary1 project is using EntityFramework 6.2.0, whereas ConsoleApp1 is using EntityFramework 6.1.0.</span></span> <span data-ttu-id="0b2db-162">Chcete-li konsolidovat verze balíčku, postupujte takto:</span><span class="sxs-lookup"><span data-stu-id="0b2db-162">To consolidate package versions, do the following:</span></span>

- <span data-ttu-id="0b2db-163">Vyberte projekty, které chcete aktualizovat v seznamu projektů.</span><span class="sxs-lookup"><span data-stu-id="0b2db-163">Select the projects to update in the project list.</span></span>
- <span data-ttu-id="0b2db-164">Vyberte verzi, která se má použít ve všech těchto projektech v ovládacím **prvku verze,** například EntityFramework 6.2.0.</span><span class="sxs-lookup"><span data-stu-id="0b2db-164">Select the version to use in all those projects in the **Version** control, such as EntityFramework 6.2.0.</span></span>
- <span data-ttu-id="0b2db-165">Vyberte tlačítko **Instalovat.**</span><span class="sxs-lookup"><span data-stu-id="0b2db-165">Select the **Install** button.</span></span>

<span data-ttu-id="0b2db-166">Správce balíčků nainstaluje vybranou verzi balíčku do všech vybraných projektů, po kterých se balíček již nezobrazí na kartě **Konsolidovat.**</span><span class="sxs-lookup"><span data-stu-id="0b2db-166">The Package Manager installs the selected package version into all selected projects, after which the package no longer appears on the **Consolidate** tab.</span></span>

## <a name="package-sources"></a><span data-ttu-id="0b2db-167">Zdroje balíčků</span><span class="sxs-lookup"><span data-stu-id="0b2db-167">Package sources</span></span>

<span data-ttu-id="0b2db-168">Chcete-li změnit zdroj, ze kterého Visual Studio získává balíčky, vyberte jeden z voliče zdroje:</span><span class="sxs-lookup"><span data-stu-id="0b2db-168">To change the source from which Visual Studio obtains packages, select one from the source selector:</span></span>

![Výběr zdroje balíčků v uzdu správce balíčků](media/PackageSourceDropDown.png)

<span data-ttu-id="0b2db-170">Správa zdrojů balíčků:</span><span class="sxs-lookup"><span data-stu-id="0b2db-170">To manage package sources:</span></span>

1. <span data-ttu-id="0b2db-171">Vyberte ikonu **Nastavení** v hlavním uživateli Správce balíčků uvedenéníže nebo použijte příkaz **Nástroje > možnosti** a přejděte na **NuGet Package Manager**:</span><span class="sxs-lookup"><span data-stu-id="0b2db-171">Select the **Settings** icon in the Package Manager UI outlined below or use the **Tools > Options** command and scroll to **NuGet Package Manager**:</span></span>

    ![Ikona nastavení ui správce balíčků](media/PackageSourceSettings.png)

1. <span data-ttu-id="0b2db-173">Vyberte uzel **Zdroje balíčků:**</span><span class="sxs-lookup"><span data-stu-id="0b2db-173">Select the **Package Sources** node:</span></span>

    ![Možnosti zdrojů balíčků](media/options.png)

1. <span data-ttu-id="0b2db-175">Chcete-li přidat **+** zdroj, vyberte , upravte název, zadejte adresu URL nebo cestu **do ovládacího prvku Zdroj** a vyberte **Aktualizovat**.</span><span class="sxs-lookup"><span data-stu-id="0b2db-175">To add a source, select **+**, edit the name, enter the URL or path in the **Source** control, and select  **Update**.</span></span> <span data-ttu-id="0b2db-176">Zdroj se nyní zobrazí v rozevíracím okně voliče.</span><span class="sxs-lookup"><span data-stu-id="0b2db-176">The source now appears in the selector drop-down.</span></span>
1. <span data-ttu-id="0b2db-177">Chcete-li změnit zdroj balíčku, vyberte jej, proveďte úpravy v polích **Název** a **Zdroj** a vyberte **Aktualizovat**.</span><span class="sxs-lookup"><span data-stu-id="0b2db-177">To change a package source, select it, make edits in the **Name** and **Source** boxes, and select **Update**.</span></span>
1. <span data-ttu-id="0b2db-178">Chcete-li zakázat zdroj balíčku, zrušte zaškrtnutí políčka nalevo od názvu v seznamu.</span><span class="sxs-lookup"><span data-stu-id="0b2db-178">To disable a package source, clear the box to the left of the name in the list.</span></span>
1. <span data-ttu-id="0b2db-179">Chcete-li odebrat zdroj balíčku, vyberte jej a pak vyberte tlačítko **X.**</span><span class="sxs-lookup"><span data-stu-id="0b2db-179">To remove a package source, select it and then select the **X** button.</span></span>
1. <span data-ttu-id="0b2db-180">Použití tlačítek se šipkami nahoru a dolů nezmění pořadí priorit zdrojů balíčků.</span><span class="sxs-lookup"><span data-stu-id="0b2db-180">Using the up and down arrow buttons does not change the priority order of the package sources.</span></span> <span data-ttu-id="0b2db-181">Visual Studio ignoruje pořadí zdrojů balíčků, pomocí balíčku z toho, který zdroj je první reagovat na požadavky.</span><span class="sxs-lookup"><span data-stu-id="0b2db-181">Visual Studio ignores the order of package sources, using the package from whichever source is first to respond to requests.</span></span> <span data-ttu-id="0b2db-182">Další informace naleznete v [tématu Obnovení balíčku](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="0b2db-182">For more information, see [Package restore](../consume-packages/package-restore.md).</span></span>

> [!Tip]
> <span data-ttu-id="0b2db-183">Pokud se zdroj balíčku po jeho odstranění znovu zobrazí, může být uveden `NuGet.Config` v souborech na úrovni počítače nebo na úrovni uživatele.</span><span class="sxs-lookup"><span data-stu-id="0b2db-183">If a package source reappears after deleting it, it may be listed in a computer-level or user-level `NuGet.Config` files.</span></span> <span data-ttu-id="0b2db-184">Viz [Běžné Konfigurace NuGet](../consume-packages/configuring-nuget-behavior.md) pro umístění těchto souborů, potom odebrat zdroj úpravou souborů ručně nebo pomocí [nuget zdroje příkazu](../reference/nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="0b2db-184">See [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md) for the location of these files, then remove the source by editing the files manually or using the [nuget sources command](../reference/nuget-exe-CLI-reference.md).</span></span>

## <a name="package-manager-options-control"></a><span data-ttu-id="0b2db-185">Ovládací prvek Možnosti správce balíčků</span><span class="sxs-lookup"><span data-stu-id="0b2db-185">Package manager Options control</span></span>

<span data-ttu-id="0b2db-186">Když je vybrán balíček, ui Správce balíčků zobrazí malý, rozbalitelný ovládací prvek **Možnosti** pod voličem verze (zobrazeno zde sbalené i rozšířené).</span><span class="sxs-lookup"><span data-stu-id="0b2db-186">When a package is selected, the Package Manager UI displays a small, expandable **Options** control below the version selector (shown here both collapsed and expanded).</span></span> <span data-ttu-id="0b2db-187">Všimněte si, že pro některé typy projektů je k dispozici pouze možnost **Zobrazit okno náhledu.**</span><span class="sxs-lookup"><span data-stu-id="0b2db-187">Note that for some project types, only the **Show preview window** option is provided.</span></span>

![Možnosti správce balíčků](media/PackageManagerUIOptions.png)

<span data-ttu-id="0b2db-189">Následující části vysvětlují tyto možnosti.</span><span class="sxs-lookup"><span data-stu-id="0b2db-189">The following sections explain these options.</span></span>

### <a name="show-preview-window"></a><span data-ttu-id="0b2db-190">Zobrazit okno náhledu</span><span class="sxs-lookup"><span data-stu-id="0b2db-190">Show preview window</span></span>

<span data-ttu-id="0b2db-191">Je-li tato možnost vybrána, zobrazí se modální okno, které jsou závislosti vybraného balíčku před instalací balíčku:</span><span class="sxs-lookup"><span data-stu-id="0b2db-191">When selected, a modal window displays which the dependencies of a chosen package before the package is installed:</span></span>

![Dialogové okno Náhled na příklad](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a><span data-ttu-id="0b2db-193">Možnosti instalace a aktualizace</span><span class="sxs-lookup"><span data-stu-id="0b2db-193">Install and Update Options</span></span>

<span data-ttu-id="0b2db-194">(Není k dispozici pro všechny typy projektů.)</span><span class="sxs-lookup"><span data-stu-id="0b2db-194">(Not available for all project types.)</span></span>

<span data-ttu-id="0b2db-195">**Chování závislostí** konfiguruje způsob, jakým nuget rozhoduje o tom, které verze závislých balíčků mají být nainstalovány:</span><span class="sxs-lookup"><span data-stu-id="0b2db-195">**Dependency behavior** configures how NuGet decides which versions of dependent packages to install:</span></span>

- <span data-ttu-id="0b2db-196">*Ignorovat závislosti přeskočí* instalaci všech závislostí, které obvykle přeruší balíček, který je nainstalován.</span><span class="sxs-lookup"><span data-stu-id="0b2db-196">*Ignore dependencies* skips installing any dependencies, which typically breaks the package being installed.</span></span>
- <span data-ttu-id="0b2db-197">*Nejnižší* [Výchozí] nainstaluje závislost s minimálním číslem verze, které splňuje požadavky primárního vybraného balíčku.</span><span class="sxs-lookup"><span data-stu-id="0b2db-197">*Lowest* [Default] installs the dependency with the minimal version number that meets the requirements of the primary chosen package.</span></span>
- <span data-ttu-id="0b2db-198">*Nejvyšší oprava* nainstaluje verzi se stejnými hlavními a dílčími čísly verzí, ale s nejvyšším číslem opravy.</span><span class="sxs-lookup"><span data-stu-id="0b2db-198">*Highest Patch* installs the version with the same major and minor version numbers, but the highest patch number.</span></span> <span data-ttu-id="0b2db-199">Pokud je například zadána verze 1.2.2, bude nainstalována nejvyšší verze začínající verzí 1.2.</span><span class="sxs-lookup"><span data-stu-id="0b2db-199">For example, if version 1.2.2 is specified then the highest version that starts with 1.2 will be installed</span></span>
- <span data-ttu-id="0b2db-200">*Nejvyšší vedlejší* nainstaluje verzi se stejným číslem hlavní verze, ale nejvyšší dílčí číslo a číslo opravy.</span><span class="sxs-lookup"><span data-stu-id="0b2db-200">*Highest Minor* installs the version with the same major version number but the highest minor number and patch number.</span></span> <span data-ttu-id="0b2db-201">Pokud je zadána verze 1.2.2, bude nainstalována nejvyšší verze začínající na 1.</span><span class="sxs-lookup"><span data-stu-id="0b2db-201">If version 1.2.2 is specified, then the highest version that starts with 1 will be installed</span></span>
- <span data-ttu-id="0b2db-202">*Nejvyšší* nainstaluje nejvyšší dostupnou verzi balíčku.</span><span class="sxs-lookup"><span data-stu-id="0b2db-202">*Highest* installs the highest available version of the package.</span></span>

<span data-ttu-id="0b2db-203">**Akce konfliktu souborů** určuje, jak by měl NuGet zpracovávat balíčky, které již existují v projektu nebo místním počítači:</span><span class="sxs-lookup"><span data-stu-id="0b2db-203">**File conflict action** specifies how NuGet should handle packages that already exist in the project or local machine:</span></span>

- <span data-ttu-id="0b2db-204">*Výzva* pokyn NuGet se zeptat, zda zachovat nebo přepsat existující balíčky.</span><span class="sxs-lookup"><span data-stu-id="0b2db-204">*Prompt* instructs NuGet to ask whether to keep or overwrite existing packages.</span></span>
- <span data-ttu-id="0b2db-205">*Ignorovat všechny* pokyny NuGet přeskočit přepsání všechny existující balíčky.</span><span class="sxs-lookup"><span data-stu-id="0b2db-205">*Ignore All* instructs NuGet to skip overwriting any existing packages.</span></span>
- <span data-ttu-id="0b2db-206">*Přepsat všechny* pokyny NuGet přepsat všechny existující balíčky.</span><span class="sxs-lookup"><span data-stu-id="0b2db-206">*Overwrite All* instructs NuGet to overwrite any existing packages.</span></span>

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a><span data-ttu-id="0b2db-207">Možnosti odinstalace</span><span class="sxs-lookup"><span data-stu-id="0b2db-207">Uninstall Options</span></span>

<span data-ttu-id="0b2db-208">(Není k dispozici pro všechny typy projektů.)</span><span class="sxs-lookup"><span data-stu-id="0b2db-208">(Not available for all project types.)</span></span>

<span data-ttu-id="0b2db-209">**Odebrat závislosti**: Pokud je tato možnost vybrána, odebere všechny závislé balíčky, pokud nejsou odkazovány jinde v projektu.</span><span class="sxs-lookup"><span data-stu-id="0b2db-209">**Remove dependencies**: when selected, removes any dependent packages if they're not referenced elsewhere in the project.</span></span>

<span data-ttu-id="0b2db-210">**Vynutit odinstalaci i v případě, že jsou na něm závislosti**: pokud je vybrána, odinstaluje balíček, i když je stále odkazován v projektu.</span><span class="sxs-lookup"><span data-stu-id="0b2db-210">**Force uninstall even if there are dependencies on it**: when selected, uninstalls a package even if it's still being referenced in the project.</span></span> <span data-ttu-id="0b2db-211">To se obvykle používá v kombinaci s **Remove závislosti** odebrat balíček a bez ohledu na závislosti, které nainstalován.</span><span class="sxs-lookup"><span data-stu-id="0b2db-211">This is typically used in combination with **Remove dependencies** to remove a package and whatever dependencies it installed.</span></span> <span data-ttu-id="0b2db-212">Použití této možnosti však může vést k přerušené odkazy v projektu.</span><span class="sxs-lookup"><span data-stu-id="0b2db-212">Using this option may, however, lead to broken references in the project.</span></span> <span data-ttu-id="0b2db-213">V takových případech může být nutné [přeinstalovat tyto další balíčky](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="0b2db-213">In such cases, you may need to [reinstall those other packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>
