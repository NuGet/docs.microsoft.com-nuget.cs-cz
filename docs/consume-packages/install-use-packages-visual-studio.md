---
title: Instalace a Správa balíčků NuGet v aplikaci Visual Studio
description: Pokyny k používání uživatelského rozhraní Správce balíčků NuGet v aplikaci Visual Studio pro práci s balíčky NuGet.
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
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231004"
---
# <a name="install-and-manage-packages-in-visual-studio-using-the-nuget-package-manager"></a><span data-ttu-id="390f8-103">Instalace a Správa balíčků v aplikaci Visual Studio pomocí Správce balíčků NuGet</span><span class="sxs-lookup"><span data-stu-id="390f8-103">Install and manage packages in Visual Studio using the NuGet Package Manager</span></span>

<span data-ttu-id="390f8-104">Uživatelské rozhraní Správce balíčků NuGet v aplikaci Visual Studio ve Windows umožňuje snadno nainstalovat, odinstalovat a aktualizovat balíčky NuGet v projektech a řešeních.</span><span class="sxs-lookup"><span data-stu-id="390f8-104">The NuGet Package Manager UI in Visual Studio on Windows allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="390f8-105">Informace o zkušenostech v Visual Studio pro Mac najdete v tématu [zahrnutí balíčku NuGet do projektu](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json).</span><span class="sxs-lookup"><span data-stu-id="390f8-105">For the experience in Visual Studio for Mac, see [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json).</span></span> <span data-ttu-id="390f8-106">Uživatelské rozhraní Správce balíčků není součástí Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="390f8-106">The Package Manager UI is not included with Visual Studio Code.</span></span>

> [!NOTE]
> <span data-ttu-id="390f8-107">Pokud ve Visual Studiu 2015 chybí správce balíčků NuGet, podívejte se na **nástroje > rozšíření a aktualizace...** a vyhledejte rozšíření *Správce balíčků NuGet* .</span><span class="sxs-lookup"><span data-stu-id="390f8-107">If you're missing the NuGet Package Manager in Visual Studio 2015, check **Tools > Extensions and Updates...** and search for the *NuGet Package Manager* extension.</span></span> <span data-ttu-id="390f8-108">Pokud nemůžete použít instalační program rozšíření v aplikaci Visual Studio, stáhněte rozšíření přímo z [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="390f8-108">If you're unable to use the extensions installer in Visual Studio, download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>
>
> <span data-ttu-id="390f8-109">Od sady Visual Studio 2017 se NuGet a správce balíčků NuGet automaticky nainstalují se všemi. Úlohy týkající se netto.</span><span class="sxs-lookup"><span data-stu-id="390f8-109">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed with any .NET-related workloads.</span></span> <span data-ttu-id="390f8-110">Nainstalujte ji jednotlivě, a to tak, že vyberete **jednotlivé komponenty > nástrojů kódu >** v instalačním programu sady Visual Studio možnost Správce balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="390f8-110">Install it individually by selecting the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

## <a name="find-and-install-a-package"></a><span data-ttu-id="390f8-111">Vyhledání a instalace balíčku</span><span class="sxs-lookup"><span data-stu-id="390f8-111">Find and install a package</span></span>

1. <span data-ttu-id="390f8-112">V **Průzkumník řešení**klikněte pravým tlačítkem myši buď na **odkaz** , nebo na projekt a vyberte **Spravovat balíčky NuGet...**.</span><span class="sxs-lookup"><span data-stu-id="390f8-112">In **Solution Explorer**, right-click either **References**  or a project and select **Manage NuGet Packages...**.</span></span>

    ![Možnost spravovat balíčky NuGet – možnost nabídky](media/ManagePackagesUICommand.png)

1. <span data-ttu-id="390f8-114">Karta **Procházet** zobrazuje balíčky podle oblíbenosti z aktuálně vybraného zdroje (viz [zdroje balíčků](#package-sources)).</span><span class="sxs-lookup"><span data-stu-id="390f8-114">The **Browse** tab displays packages by popularity from the currently selected source (see [package sources](#package-sources)).</span></span> <span data-ttu-id="390f8-115">Vyhledejte konkrétní balíček pomocí vyhledávacího pole v levém horním rohu.</span><span class="sxs-lookup"><span data-stu-id="390f8-115">Search for a specific package using the search box on the upper left.</span></span> <span data-ttu-id="390f8-116">Výběrem balíčku ze seznamu zobrazíte jeho informace, což také umožňuje **nainstalovat tlačítko instalovat** společně s rozevíracím seznamem výběru verze.</span><span class="sxs-lookup"><span data-stu-id="390f8-116">Select a package from the list to display its information, which also enables the **Install** button along with a version-selection drop-down.</span></span>

    ![Dialogové okno Spravovat balíčky NuGet – karta Procházet](media/Search.png)

1. <span data-ttu-id="390f8-118">V rozevíracím seznamu vyberte požadovanou verzi a vyberte **nainstalovat**.</span><span class="sxs-lookup"><span data-stu-id="390f8-118">Select the desired version from the drop-down and select **Install**.</span></span> <span data-ttu-id="390f8-119">Visual Studio nainstaluje balíček a jeho závislosti do projektu.</span><span class="sxs-lookup"><span data-stu-id="390f8-119">Visual Studio installs the package and its dependencies into the project.</span></span> <span data-ttu-id="390f8-120">Může se zobrazit výzva, abyste přijali Licenční podmínky.</span><span class="sxs-lookup"><span data-stu-id="390f8-120">You may be asked to accept license terms.</span></span> <span data-ttu-id="390f8-121">Po dokončení instalace se přidané balíčky zobrazí na kartě **nainstalované** . balíčky jsou také uvedeny v uzlu **odkazy** Průzkumník řešení, který označuje, že se na ně můžete odkazovat v projektu pomocí příkazů `using`.</span><span class="sxs-lookup"><span data-stu-id="390f8-121">When installation is complete, the added packages appear on the **Installed** tab. Packages are also listed in the **References** node of Solution Explorer, indicating that you can refer to them in the project with `using` statements.</span></span>

    ![Odkazy v Průzkumník řešení](media/References.png)

> [!Tip]
> <span data-ttu-id="390f8-123">Chcete-li do hledání zahrnout předběžné verze předprodejní verze a v rozevíracím seznamu verze zpřístupnit předprodejní verze, vyberte možnost **Zahrnout předběžnou** verzi.</span><span class="sxs-lookup"><span data-stu-id="390f8-123">To include prerelease versions in the search, and to make prerelease versions available in the version drop-down, select the **Include prerelease** option.</span></span>

> [!Note]
> <span data-ttu-id="390f8-124">NuGet má dva formáty, ve kterých může projekt používat balíčky: [`PackageReference`](package-references-in-project-files.md) a [`packages.config`](../reference/packages-config.md).</span><span class="sxs-lookup"><span data-stu-id="390f8-124">NuGet has two formats in which a project may use packages: [`PackageReference`](package-references-in-project-files.md) and [`packages.config`](../reference/packages-config.md).</span></span> <span data-ttu-id="390f8-125">[Výchozí nastavení lze nastavit v okně Možnosti aplikace Visual Studio](Package-Restore.md#choose-default-package-management-format).</span><span class="sxs-lookup"><span data-stu-id="390f8-125">[The default can be set in Visual Studio's options window](Package-Restore.md#choose-default-package-management-format).</span></span>

## <a name="uninstall-a-package"></a><span data-ttu-id="390f8-126">Odinstalace balíčku</span><span class="sxs-lookup"><span data-stu-id="390f8-126">Uninstall a package</span></span>

1. <span data-ttu-id="390f8-127">V **Průzkumník řešení**klikněte pravým tlačítkem myši buď na **odkaz** , nebo na požadovaný projekt a vyberte **Spravovat balíčky NuGet...**.</span><span class="sxs-lookup"><span data-stu-id="390f8-127">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="390f8-128">Vyberte kartu **Nainstalováno**.</span><span class="sxs-lookup"><span data-stu-id="390f8-128">Select the **Installed** tab.</span></span>
1. <span data-ttu-id="390f8-129">Vyberte balíček, který chcete odinstalovat (Pokud je to nutné, pomocí hledání vyfiltrujte seznam) a vyberte **odinstalovat**.</span><span class="sxs-lookup"><span data-stu-id="390f8-129">Select the package to uninstall (using search to filter the list if necessary) and select **Uninstall**.</span></span>

    ![Odinstalace balíčku](media/UninstallPackage.png)

1. <span data-ttu-id="390f8-131">Všimněte si, že **zahrnuté předběžné verze** a zdrojové ovládací prvky **balíčku** nemají žádný vliv na odinstalaci balíčků.</span><span class="sxs-lookup"><span data-stu-id="390f8-131">Note that the **Include prerelease** and **Package source** controls have no effect when uninstalling packages.</span></span>

## <a name="update-a-package"></a><span data-ttu-id="390f8-132">Aktualizace balíčku</span><span class="sxs-lookup"><span data-stu-id="390f8-132">Update a package</span></span>

1. <span data-ttu-id="390f8-133">V **Průzkumník řešení**klikněte pravým tlačítkem myši buď na **odkaz** , nebo na požadovaný projekt a vyberte **Spravovat balíčky NuGet...**. (V projektech webu klikněte pravým tlačítkem myši na složku **bin** .)</span><span class="sxs-lookup"><span data-stu-id="390f8-133">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**. (In web site projects, right-click the **Bin** folder.)</span></span>
1. <span data-ttu-id="390f8-134">Kliknutím na kartu **aktualizace** zobrazíte balíčky, které mají dostupné aktualizace z vybraných zdrojů balíčků.</span><span class="sxs-lookup"><span data-stu-id="390f8-134">Select the **Updates** tab to see packages that have available updates from the selected package sources.</span></span> <span data-ttu-id="390f8-135">V seznamu aktualizace zvolte **Zahrnout předprodejní** verze pro zahrnutí předprodejních balíčků.</span><span class="sxs-lookup"><span data-stu-id="390f8-135">Select **Include prerelease** to include prerelease packages in the update list.</span></span>
1. <span data-ttu-id="390f8-136">Vyberte balíček, který chcete aktualizovat, vyberte požadovanou verzi v rozevíracím seznamu napravo a vyberte **aktualizovat**.</span><span class="sxs-lookup"><span data-stu-id="390f8-136">Select the package to update, select the desired version from the drop-down on the right, and select **Update**.</span></span>

    ![Aktualizace balíčku](media/UpdatePackages.png)

1. <a name="implicit_reference"></a><span data-ttu-id="390f8-138">U některých balíčků je tlačítko **aktualizovat** zakázané a zobrazí se zpráva s oznámením, že se jedná o "implicitně odkazované sadu SDK" (nebo "autoreferenced").</span><span class="sxs-lookup"><span data-stu-id="390f8-138">For some packages, the **Update** button is disabled and a message appears saying that it's "Implicitly referenced by an SDK" (or "AutoReferenced").</span></span> <span data-ttu-id="390f8-139">Tato zpráva znamená, že balíček je součástí větší architektury nebo sady SDK a neměli byste ho aktualizovat nezávisle.</span><span class="sxs-lookup"><span data-stu-id="390f8-139">This message indicates that the package is part of a larger framework or SDK and should not be updated independently.</span></span> <span data-ttu-id="390f8-140">(Tyto balíčky jsou interně označené `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) Například `Microsoft.NETCore.App` je součástí .NET Core SDK a verze balíčku není stejná jako verze rozhraní modulu runtime používaného aplikací.</span><span class="sxs-lookup"><span data-stu-id="390f8-140">(Such packages are internally marked with `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) For example, `Microsoft.NETCore.App` is part of the .NET Core SDK, and the package version is not the same as the version of the runtime framework used by the application.</span></span> <span data-ttu-id="390f8-141">Musíte [aktualizovat instalaci .NET Core](https://aka.ms/dotnet-download) a získat nové verze ASP.NET Core a modulu runtime .NET Core.</span><span class="sxs-lookup"><span data-stu-id="390f8-141">You need to [update your .NET Core installation](https://aka.ms/dotnet-download) to get new versions of the ASP.NET Core and .NET Core runtime.</span></span> <span data-ttu-id="390f8-142">[Další podrobnosti o .NET Core metabalíčky a verzích najdete v tomto dokumentu](/dotnet/core/packages).</span><span class="sxs-lookup"><span data-stu-id="390f8-142">[See this document for more details on .NET Core metapackages and versioning](/dotnet/core/packages).</span></span> <span data-ttu-id="390f8-143">To platí pro následující běžně používané balíčky:</span><span class="sxs-lookup"><span data-stu-id="390f8-143">This applies to the following commonly used packages:</span></span>
    * <span data-ttu-id="390f8-144">Microsoft.AspNetCore.All</span><span class="sxs-lookup"><span data-stu-id="390f8-144">Microsoft.AspNetCore.All</span></span>
    * <span data-ttu-id="390f8-145">Microsoft.AspNetCore.App</span><span class="sxs-lookup"><span data-stu-id="390f8-145">Microsoft.AspNetCore.App</span></span>
    * <span data-ttu-id="390f8-146">Microsoft.NETCore.App</span><span class="sxs-lookup"><span data-stu-id="390f8-146">Microsoft.NETCore.App</span></span>
    * <span data-ttu-id="390f8-147">NETStandard. Library</span><span class="sxs-lookup"><span data-stu-id="390f8-147">NETStandard.Library</span></span>

    ![Ukázkový balíček označený jako implicitně odkazující nebo automaticky odkazovaný](media/PackageManagerUIAutoReferenced.png)

1. <span data-ttu-id="390f8-149">Pokud chcete aktualizovat více balíčků na nejnovější verze, vyberte je v seznamu a klikněte na tlačítko **aktualizovat** nad seznamem.</span><span class="sxs-lookup"><span data-stu-id="390f8-149">To update multiple packages to their newest versions, select  them in the list and select the **Update** button above the list.</span></span>
1. <span data-ttu-id="390f8-150">Jednotlivé balíčky můžete také aktualizovat na kartě **nainstalované** . V takovém případě podrobnosti balíčku zahrnují selektor verze (podléhající možnosti **předprodejní zahrnutí** ) a tlačítko **aktualizovat** .</span><span class="sxs-lookup"><span data-stu-id="390f8-150">You can also update an individual package from the **Installed** tab. In this case, the details for the package include a version selector (subject to the **Include prerelease** option) and an **Update** button.</span></span>

## <a name="manage-packages-for-the-solution"></a><span data-ttu-id="390f8-151">Spravovat balíčky pro řešení</span><span class="sxs-lookup"><span data-stu-id="390f8-151">Manage packages for the solution</span></span>

<span data-ttu-id="390f8-152">Správa balíčků pro řešení je pohodlný způsob práce s více projekty současně.</span><span class="sxs-lookup"><span data-stu-id="390f8-152">Managing packages for a solution is a convenient means to work with multiple projects simultaneously.</span></span>

1. <span data-ttu-id="390f8-153">Vyberte **nástroje > správce balíčků nuget > spravovat balíčky NuGet pro řešení...** příkaz nabídky nebo klikněte pravým tlačítkem na řešení a vyberte **Spravovat balíčky NuGet...**:</span><span class="sxs-lookup"><span data-stu-id="390f8-153">Select the **Tools > NuGet Package Manager > Manage NuGet Packages for Solution...** menu command, or right-click the solution and select **Manage NuGet Packages...**:</span></span>

    ![Spravovat balíčky NuGet pro řešení](media/ManagePackagesSolutionUICommand.png)

1. <span data-ttu-id="390f8-155">Při správě balíčků pro řešení vám uživatelské rozhraní umožní vybrat projekty, které jsou ovlivněné operacemi:</span><span class="sxs-lookup"><span data-stu-id="390f8-155">When managing packages for the solution, the UI lets you select the projects that are affected by the operations:</span></span>

    ![Selektor projektu při správě balíčků pro řešení](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a><span data-ttu-id="390f8-157">Karta konsolidovat</span><span class="sxs-lookup"><span data-stu-id="390f8-157">Consolidate tab</span></span>

<span data-ttu-id="390f8-158">Vývojáři obvykle považují za chybné postupy použití různých verzí stejného balíčku NuGet v různých projektech ve stejném řešení.</span><span class="sxs-lookup"><span data-stu-id="390f8-158">Developers typically consider it bad practice to use different versions of the same NuGet package across different projects in the same solution.</span></span> <span data-ttu-id="390f8-159">Pokud se rozhodnete spravovat balíčky pro řešení, uživatelské rozhraní Správce balíčků poskytuje kartu **konsolidace** , na které můžete snadno zjistit, kde jsou balíčky s různými čísly verzí používány různými projekty v řešení:</span><span class="sxs-lookup"><span data-stu-id="390f8-159">When you choose to manage packages for a solution, the Package Manager UI provides a **Consolidate** tab on which you can easily see where packages with distinct version numbers are used by different projects in the solution:</span></span>

![Karta konsolidace uživatelského rozhraní Správce balíčků](media/ConsolidateTab.png)

<span data-ttu-id="390f8-161">V tomto příkladu projekt ClassLibrary1 používá EntityFramework 6.2.0, zatímco ConsoleApp1 používá EntityFramework 6.1.0.</span><span class="sxs-lookup"><span data-stu-id="390f8-161">In this example, the ClassLibrary1 project is using EntityFramework 6.2.0, whereas ConsoleApp1 is using EntityFramework 6.1.0.</span></span> <span data-ttu-id="390f8-162">Chcete-li konsolidovat verze balíčků, postupujte následovně:</span><span class="sxs-lookup"><span data-stu-id="390f8-162">To consolidate package versions, do the following:</span></span>

- <span data-ttu-id="390f8-163">Vyberte projekty, které chcete aktualizovat v seznamu projektu.</span><span class="sxs-lookup"><span data-stu-id="390f8-163">Select the projects to update in the project list.</span></span>
- <span data-ttu-id="390f8-164">Vyberte verzi, která má být použita ve všech projektech v rámci správy **verzí** , například EntityFramework 6.2.0.</span><span class="sxs-lookup"><span data-stu-id="390f8-164">Select the version to use in all those projects in the **Version** control, such as EntityFramework 6.2.0.</span></span>
- <span data-ttu-id="390f8-165">Vyberte tlačítko **instalovat** .</span><span class="sxs-lookup"><span data-stu-id="390f8-165">Select the **Install** button.</span></span>

<span data-ttu-id="390f8-166">Správce balíčků nainstaluje vybranou verzi balíčku do všech vybraných projektů, po kterém se balíček už nebude zobrazovat na kartě **konsolidace** .</span><span class="sxs-lookup"><span data-stu-id="390f8-166">The Package Manager installs the selected package version into all selected projects, after which the package no longer appears on the **Consolidate** tab.</span></span>

## <a name="package-sources"></a><span data-ttu-id="390f8-167">Zdroje balíčků</span><span class="sxs-lookup"><span data-stu-id="390f8-167">Package sources</span></span>

<span data-ttu-id="390f8-168">Chcete-li změnit zdroj, ze kterého aplikace Visual Studio získává balíčky, vyberte jeden z voliče zdroje:</span><span class="sxs-lookup"><span data-stu-id="390f8-168">To change the source from which Visual Studio obtains packages, select one from the source selector:</span></span>

![Selektor zdrojů balíčku v uživatelském rozhraní Správce balíčků](media/PackageSourceDropDown.png)

<span data-ttu-id="390f8-170">Správa zdrojů balíčků:</span><span class="sxs-lookup"><span data-stu-id="390f8-170">To manage package sources:</span></span>

1. <span data-ttu-id="390f8-171">V uživatelském rozhraní Správce balíčků vyberte ikonu **Nastavení** , která je níže uvedená níže, nebo použijte příkaz **Nástroje > Možnosti** a přejděte na **Správce balíčků NuGet**:</span><span class="sxs-lookup"><span data-stu-id="390f8-171">Select the **Settings** icon in the Package Manager UI outlined below or use the **Tools > Options** command and scroll to **NuGet Package Manager**:</span></span>

    ![Ikona nastavení uživatelského rozhraní Správce balíčků](media/PackageSourceSettings.png)

1. <span data-ttu-id="390f8-173">Vyberte uzel **zdroje balíčků** :</span><span class="sxs-lookup"><span data-stu-id="390f8-173">Select the **Package Sources** node:</span></span>

    ![Možnosti zdrojů balíčků](media/options.png)

1. <span data-ttu-id="390f8-175">Chcete-li přidat zdroj, vyberte **+**, upravte název, zadejte adresu URL nebo cestu ve správě **zdrojového kódu** a vyberte **aktualizovat**.</span><span class="sxs-lookup"><span data-stu-id="390f8-175">To add a source, select **+**, edit the name, enter the URL or path in the **Source** control, and select  **Update**.</span></span> <span data-ttu-id="390f8-176">Zdroj se nyní zobrazí v rozevíracím seznamu selektoru.</span><span class="sxs-lookup"><span data-stu-id="390f8-176">The source now appears in the selector drop-down.</span></span>
1. <span data-ttu-id="390f8-177">Chcete-li změnit zdroj balíčku, vyberte jej, proveďte úpravy v polích **název** a **zdroj** a vyberte možnost **aktualizovat**.</span><span class="sxs-lookup"><span data-stu-id="390f8-177">To change a package source, select it, make edits in the **Name** and **Source** boxes, and select **Update**.</span></span>
1. <span data-ttu-id="390f8-178">Chcete-li zakázat zdroj balíčku, zrušte zaškrtnutí políčka nalevo od názvu v seznamu.</span><span class="sxs-lookup"><span data-stu-id="390f8-178">To disable a package source, clear the box to the left of the name in the list.</span></span>
1. <span data-ttu-id="390f8-179">Pokud chcete odebrat zdroj balíčku, vyberte ho a pak klikněte na tlačítko **X** .</span><span class="sxs-lookup"><span data-stu-id="390f8-179">To remove a package source, select it and then select the **X** button.</span></span>
1. <span data-ttu-id="390f8-180">Pomocí tlačítek se šipkami nahoru a dolů se nezmění pořadí priorit zdrojů balíčku.</span><span class="sxs-lookup"><span data-stu-id="390f8-180">Using the up and down arrow buttons does not change the priority order of the package sources.</span></span> <span data-ttu-id="390f8-181">Sada Visual Studio ignoruje pořadí zdrojů balíčku. při použití balíčku z libovolného zdroje je nejprve nutné reagovat na požadavky.</span><span class="sxs-lookup"><span data-stu-id="390f8-181">Visual Studio ignores the order of package sources, using the package from whichever source is first to respond to requests.</span></span> <span data-ttu-id="390f8-182">Další informace najdete v tématu věnovaném [obnovení balíčků](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="390f8-182">For more information, see [Package restore](../consume-packages/package-restore.md).</span></span>

> [!Tip]
> <span data-ttu-id="390f8-183">Pokud se po odstranění zobrazí zdroj balíčku, může být uveden v souborech `NuGet.Config` na úrovni počítače nebo na úrovni uživatele.</span><span class="sxs-lookup"><span data-stu-id="390f8-183">If a package source reappears after deleting it, it may be listed in a computer-level or user-level `NuGet.Config` files.</span></span> <span data-ttu-id="390f8-184">V tématu [běžné konfigurace NuGet](../consume-packages/configuring-nuget-behavior.md) pro umístění těchto souborů odstraňte zdroj úpravou souborů ručně nebo pomocí [příkazu NuGet sources](../reference/nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="390f8-184">See [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md) for the location of these files, then remove the source by editing the files manually or using the [nuget sources command](../reference/nuget-exe-CLI-reference.md).</span></span>

## <a name="package-manager-options-control"></a><span data-ttu-id="390f8-185">Řízení možností Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="390f8-185">Package manager Options control</span></span>

<span data-ttu-id="390f8-186">Když je vybraný balíček, v uživatelském rozhraní Správce balíčků se pod selektorem verzí zobrazí malý ovládací prvek **možností s možností** rozšíření (tady se zobrazí sbalená i rozbalená).</span><span class="sxs-lookup"><span data-stu-id="390f8-186">When a package is selected, the Package Manager UI displays a small, expandable **Options** control below the version selector (shown here both collapsed and expanded).</span></span> <span data-ttu-id="390f8-187">Všimněte si, že u některých typů projektů je k dispozici pouze možnost **Zobrazit okno náhledu** .</span><span class="sxs-lookup"><span data-stu-id="390f8-187">Note that for some project types, only the **Show preview window** option is provided.</span></span>

![Možnosti Správce balíčků](media/PackageManagerUIOptions.png)

<span data-ttu-id="390f8-189">Tyto možnosti jsou vysvětleny v následujících částech.</span><span class="sxs-lookup"><span data-stu-id="390f8-189">The following sections explain these options.</span></span>

### <a name="show-preview-window"></a><span data-ttu-id="390f8-190">Zobrazit okno náhledu</span><span class="sxs-lookup"><span data-stu-id="390f8-190">Show preview window</span></span>

<span data-ttu-id="390f8-191">Když se tato možnost vybere, otevře se modální okno, které obsahuje závislosti vybraného balíčku před instalací balíčku:</span><span class="sxs-lookup"><span data-stu-id="390f8-191">When selected, a modal window displays which the dependencies of a chosen package before the package is installed:</span></span>

![Ukázka náhledu – dialogové okno](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a><span data-ttu-id="390f8-193">Možnosti instalace a aktualizace</span><span class="sxs-lookup"><span data-stu-id="390f8-193">Install and Update Options</span></span>

<span data-ttu-id="390f8-194">(Není k dispozici pro všechny typy projektů.)</span><span class="sxs-lookup"><span data-stu-id="390f8-194">(Not available for all project types.)</span></span>

<span data-ttu-id="390f8-195">**Chování závislostí** konfiguruje, jak NuGet určuje, které verze závislých balíčků nainstalovat:</span><span class="sxs-lookup"><span data-stu-id="390f8-195">**Dependency behavior** configures how NuGet decides which versions of dependent packages to install:</span></span>

- <span data-ttu-id="390f8-196">*Ignorovat závislosti* přeskočí instalaci všech závislostí, což obvykle přeruší instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="390f8-196">*Ignore dependencies* skips installing any dependencies, which typically breaks the package being installed.</span></span>
- <span data-ttu-id="390f8-197">*Nejnižší* [výchozí] nainstaluje závislost s minimálním číslem verze, který splňuje požadavky primárního vybraného balíčku.</span><span class="sxs-lookup"><span data-stu-id="390f8-197">*Lowest* [Default] installs the dependency with the minimal version number that meets the requirements of the primary chosen package.</span></span>
- <span data-ttu-id="390f8-198">*Nejvyšší oprava* nainstaluje verzi se stejnými čísly hlavní verze a podverze, ale nejvyšší číslo opravy.</span><span class="sxs-lookup"><span data-stu-id="390f8-198">*Highest Patch* installs the version with the same major and minor version numbers, but the highest patch number.</span></span> <span data-ttu-id="390f8-199">Pokud je například zadána verze 1.2.2, bude nainstalována nejvyšší verze, která začíná 1,2.</span><span class="sxs-lookup"><span data-stu-id="390f8-199">For example, if version 1.2.2 is specified then the highest version that starts with 1.2 will be installed</span></span>
- <span data-ttu-id="390f8-200">*Nejvyšší* verze nainstaluje verzi se stejným číslem hlavní verze, ale s nejvyšším podčíslem a číslem opravy.</span><span class="sxs-lookup"><span data-stu-id="390f8-200">*Highest Minor* installs the version with the same major version number but the highest minor number and patch number.</span></span> <span data-ttu-id="390f8-201">Je-li zadána verze 1.2.2, bude nainstalována nejvyšší verze, která začíná 1.</span><span class="sxs-lookup"><span data-stu-id="390f8-201">If version 1.2.2 is specified, then the highest version that starts with 1 will be installed</span></span>
- <span data-ttu-id="390f8-202">*Nejvyšší* verze nainstaluje nejvyšší dostupnou verzi balíčku.</span><span class="sxs-lookup"><span data-stu-id="390f8-202">*Highest* installs the highest available version of the package.</span></span>

<span data-ttu-id="390f8-203">**Akce konfliktu souborů** určuje, jak má NuGet zpracovat balíčky, které už existují v projektu nebo na místním počítači:</span><span class="sxs-lookup"><span data-stu-id="390f8-203">**File conflict action** specifies how NuGet should handle packages that already exist in the project or local machine:</span></span>

- <span data-ttu-id="390f8-204">*Prompt* vydá pokyn pro dotaz, jestli chcete zachovat nebo přepsat stávající balíčky.</span><span class="sxs-lookup"><span data-stu-id="390f8-204">*Prompt* instructs NuGet to ask whether to keep or overwrite existing packages.</span></span>
- <span data-ttu-id="390f8-205">*Ignorovat všechny* pokyny NuGet pro přeskočení přepsání existujících balíčků</span><span class="sxs-lookup"><span data-stu-id="390f8-205">*Ignore All* instructs NuGet to skip overwriting any existing packages.</span></span>
- <span data-ttu-id="390f8-206">Příkaz *přepsat vše* instruuje balíček NuGet, aby přepsal všechny existující balíčky.</span><span class="sxs-lookup"><span data-stu-id="390f8-206">*Overwrite All* instructs NuGet to overwrite any existing packages.</span></span>

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a><span data-ttu-id="390f8-207">Možnosti odinstalace</span><span class="sxs-lookup"><span data-stu-id="390f8-207">Uninstall Options</span></span>

<span data-ttu-id="390f8-208">(Není k dispozici pro všechny typy projektů.)</span><span class="sxs-lookup"><span data-stu-id="390f8-208">(Not available for all project types.)</span></span>

<span data-ttu-id="390f8-209">**Odebrat závislosti**: Pokud je vybraná, odebere všechny závislé balíčky, pokud se na ně neodkazují jinde v projektu.</span><span class="sxs-lookup"><span data-stu-id="390f8-209">**Remove dependencies**: when selected, removes any dependent packages if they're not referenced elsewhere in the project.</span></span>

<span data-ttu-id="390f8-210">**Vynutit odinstalaci i v případě, že jsou k dispozici závislosti**: Pokud je vybrána, odinstaluje balíček i v případě, že je stále odkazován v projektu.</span><span class="sxs-lookup"><span data-stu-id="390f8-210">**Force uninstall even if there are dependencies on it**: when selected, uninstalls a package even if it's still being referenced in the project.</span></span> <span data-ttu-id="390f8-211">Obvykle se používá v kombinaci s **odebráním závislostí** pro odebrání balíčku a libovolné závislosti, které nainstaloval.</span><span class="sxs-lookup"><span data-stu-id="390f8-211">This is typically used in combination with **Remove dependencies** to remove a package and whatever dependencies it installed.</span></span> <span data-ttu-id="390f8-212">Použití této možnosti může však vést k nefunkčním odkazům v projektu.</span><span class="sxs-lookup"><span data-stu-id="390f8-212">Using this option may, however, lead to broken references in the project.</span></span> <span data-ttu-id="390f8-213">V takových případech bude pravděpodobně nutné [přeinstalovat tyto balíčky](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="390f8-213">In such cases, you may need to [reinstall those other packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>
