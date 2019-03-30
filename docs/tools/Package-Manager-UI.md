---
title: Odkaz uživatelského rozhraní Správce balíčků NuGet
description: Pokyny k používání uživatelského rozhraní Správce balíčků NuGet v sadě Visual Studio pro práci s balíčky NuGet.
author: karann-msft
ms.author: karann
ms.date: 12/08/2017
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 422faf99e58e058d86db774a8f3c1c576b3dc393
ms.sourcegitcommit: 2af17c8bb452a538977794bf559cdd78d58f2790
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/29/2019
ms.locfileid: "58637620"
---
# <a name="nuget-package-manager-ui"></a><span data-ttu-id="92130-103">Uživatelské rozhraní Správce balíčků NuGet</span><span class="sxs-lookup"><span data-stu-id="92130-103">NuGet Package Manager UI</span></span>

<span data-ttu-id="92130-104">Uživatelské rozhraní Správce balíčků NuGet v sadě Visual Studio ve Windows umožňuje snadno nainstalování, odinstalování a aktualizace balíčků NuGet do projektů a řešení.</span><span class="sxs-lookup"><span data-stu-id="92130-104">The NuGet Package Manager UI in Visual Studio on Windows allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="92130-105">Prostředí sady Visual Studio pro Mac, najdete v části [balíček včetně NuGet ve vašem projektu](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="92130-105">For the experience in Visual Studio for Mac, see [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span> <span data-ttu-id="92130-106">Uživatelské rozhraní Správce balíčků není součástí systému Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="92130-106">The Package Manager UI is not included with Visual Studio Code.</span></span>

<span data-ttu-id="92130-107">V tomto tématu:</span><span class="sxs-lookup"><span data-stu-id="92130-107">In this topic:</span></span>

- [<span data-ttu-id="92130-108">Vyhledání a instalace balíčku (Karta Procházet)</span><span class="sxs-lookup"><span data-stu-id="92130-108">Finding and installing a package (Browse tab)</span></span>](#finding-and-installing-a-package)
- [<span data-ttu-id="92130-109">Odinstalovává se balíček (stiskněte klávesu tab nainstalováno)</span><span class="sxs-lookup"><span data-stu-id="92130-109">Uninstalling a package (Installed tab)</span></span>](#uninstalling-a-package)
- <span data-ttu-id="92130-110">[Aktualizuje se balíček (karty nainstalováno a aktualizace)](#updating-a-package) (zahrnuje ["Implicitně odkazovaná sadu SDK" nebo "AutoReferenced" zpráva](#implicit_reference))</span><span class="sxs-lookup"><span data-stu-id="92130-110">[Updating a package (Installed and Updates tabs)](#updating-a-package) (includes the ["Implicitly referenced by an SDK" or "AutoReferenced" message](#implicit_reference))</span></span>
- <span data-ttu-id="92130-111">[Správa balíčků pro řešení](#managing-packages-for-the-solution) (práce s více projektů současně).</span><span class="sxs-lookup"><span data-stu-id="92130-111">[Managing packages for the solution](#managing-packages-for-the-solution) (working with multiple projects at the same time).</span></span>
- [<span data-ttu-id="92130-112">Zdroje balíčků</span><span class="sxs-lookup"><span data-stu-id="92130-112">Package sources</span></span>](#package-sources)
- [<span data-ttu-id="92130-113">Ovládací prvek možnosti Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="92130-113">Package manager Options control</span></span>](#package-manager-options-control)

> [!Note]
> <span data-ttu-id="92130-114">Pokud jste chybí Správce balíčků NuGet v sadě Visual Studio 2015, zkontrolujte **nástroje > rozšíření a aktualizace...**  , vyhledejte *Správce balíčků NuGet* rozšíření.</span><span class="sxs-lookup"><span data-stu-id="92130-114">If you're missing the NuGet Package Manager in Visual Studio 2015, check **Tools > Extensions and Updates...** and search for the *NuGet Package Manager* extension.</span></span> <span data-ttu-id="92130-115">Pokud nemůžete použít instalační program rozšíření v sadě Visual Studio, stáhněte si rozšíření přímo z [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="92130-115">If you're unable to use the extensions installer in Visual Studio, download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>
>
> <span data-ttu-id="92130-116">V sadě Visual Studio 2017 NuGet a Správce balíčků NuGet se instalují automaticky s žádné. NET související úlohy.</span><span class="sxs-lookup"><span data-stu-id="92130-116">In Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed with any .NET-related workloads.</span></span> <span data-ttu-id="92130-117">Instalovat jednotlivě tak, že vyberete **jednotlivé komponenty > kód nástroje > Správce balíčků NuGet** možnost v instalačním programu sady Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="92130-117">Install it individually by selecting the **Individual components > Code tools > NuGet package manager** option in the Visual Studio 2017 installer.</span></span>

## <a name="finding-and-installing-a-package"></a><span data-ttu-id="92130-118">Vyhledání a instalace balíčku</span><span class="sxs-lookup"><span data-stu-id="92130-118">Finding and installing a package</span></span>

1. <span data-ttu-id="92130-119">V **Průzkumníka řešení**, pravým tlačítkem myši buď **odkazy** nebo projekt a vyberte **spravovat balíčky NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="92130-119">In **Solution Explorer**, right-click either **References**  or a project and select **Manage NuGet Packages...**.</span></span>

    ![Spravovat balíčky NuGet nabídky](media/ManagePackagesUICommand.png)

1. <span data-ttu-id="92130-121">**Procházet** karta zobrazuje i podle popularity z aktuálně vybraného zdroje balíčků (naleznete v tématu [balíček zdroje](#package-sources)).</span><span class="sxs-lookup"><span data-stu-id="92130-121">The **Browse** tab displays packages by popularity from the currently selected source (see [package sources](#package-sources)).</span></span> <span data-ttu-id="92130-122">Vyhledejte konkrétní balíček pomocí vyhledávacího pole v levém horním rohu.</span><span class="sxs-lookup"><span data-stu-id="92130-122">Search for a specific package using the search box on the upper left.</span></span> <span data-ttu-id="92130-123">Vyberte balíček ze seznamu zobrazíte její informace, které umožňuje **nainstalovat** tlačítko spolu s rozevírací výběr verze.</span><span class="sxs-lookup"><span data-stu-id="92130-123">Select a package from the list to display its information, which also enables the **Install** button along with a version-selection drop-down.</span></span>

    ![Správa kartu Procházet dialogové okno balíčků NuGet](media/Search.png)

1. <span data-ttu-id="92130-125">Vyberte požadovanou verzi z rozevíracího seznamu a vyberte **nainstalovat**.</span><span class="sxs-lookup"><span data-stu-id="92130-125">Select the desired version from the drop-down and select **Install**.</span></span> <span data-ttu-id="92130-126">Visual Studio nainstaluje do projektu balíček a jeho závislosti.</span><span class="sxs-lookup"><span data-stu-id="92130-126">Visual Studio installs the package and its dependencies into the project.</span></span> <span data-ttu-id="92130-127">Můžete být vyzváni k potvrzení licenčních podmínek.</span><span class="sxs-lookup"><span data-stu-id="92130-127">You may be asked to accept license terms.</span></span> <span data-ttu-id="92130-128">Po dokončení instalace se zobrazí přidání balíčků na **nainstalováno** kartu. Balíčky jsou uvedené také na **odkazy** uzlu Průzkumníka řešení, která udává, najdete je v projektu s `using` příkazy.</span><span class="sxs-lookup"><span data-stu-id="92130-128">When installation is complete, the added packages appear on the **Installed** tab. Packages are also listed in the **References** node of Solution Explorer, indicating that you can refer to them in the project with `using` statements.</span></span>

    ![Odkazy v Průzkumníku řešení](media/References.png)

> [!Tip]
> <span data-ttu-id="92130-130">Chcete-li do hledání zahrnout předběžné verze a aby předběžné verze k dispozici ve verzi rozevíracího seznamu, vyberte **zahrnout předběžné verze** možnost.</span><span class="sxs-lookup"><span data-stu-id="92130-130">To include prerelease versions in the search, and to make prerelease versions available in the version drop-down, select the **Include prerelease** option.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="92130-131">Odinstalace balíčku</span><span class="sxs-lookup"><span data-stu-id="92130-131">Uninstalling a package</span></span>

1. <span data-ttu-id="92130-132">V **Průzkumníka řešení**, pravým tlačítkem myši buď **odkazy** nebo požadovaný projekt a vyberte **spravovat balíčky NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="92130-132">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="92130-133">Vyberte **nainstalováno** kartu.</span><span class="sxs-lookup"><span data-stu-id="92130-133">Select the **Installed** tab.</span></span>
1. <span data-ttu-id="92130-134">Vyberte balíček odinstalovat (použití vyhledávání k filtrování seznamu v případě potřeby) a vyberte **odinstalovat**.</span><span class="sxs-lookup"><span data-stu-id="92130-134">Select the package to uninstall (using search to filter the list if necessary) and select **Uninstall**.</span></span>

    ![Odinstalace balíčku](media/UninstallPackage.png)

1. <span data-ttu-id="92130-136">Všimněte si, že **zahrnout předběžné verze** a **zdroj balíčku** ovládací prvky nemají žádný vliv při odinstalaci balíčků.</span><span class="sxs-lookup"><span data-stu-id="92130-136">Note that the **Include prerelease** and **Package source** controls have no effect when uninstalling packages.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="92130-137">Aktualizace balíčku</span><span class="sxs-lookup"><span data-stu-id="92130-137">Updating a package</span></span>

1. <span data-ttu-id="92130-138">V **Průzkumníka řešení**, pravým tlačítkem myši buď **odkazy** nebo požadovaný projekt a vyberte **spravovat balíčky NuGet...** . (V projektech webových stránek, klikněte pravým tlačítkem myši **Bin** složky.)</span><span class="sxs-lookup"><span data-stu-id="92130-138">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**. (In web site projects, right-click the **Bin** folder.)</span></span>
1. <span data-ttu-id="92130-139">Vyberte **aktualizace** kartu pro zobrazení balíčky, které jsou dostupné aktualizace z vybraného balíčku zdrojů.</span><span class="sxs-lookup"><span data-stu-id="92130-139">Select the **Updates** tab to see packages that have available updates from the selected package sources.</span></span> <span data-ttu-id="92130-140">Vyberte **zahrnout předběžné verze** zahrnout předběžné verze balíčků v seznamu aktualizací.</span><span class="sxs-lookup"><span data-stu-id="92130-140">Select **Include prerelease** to include prerelease packages in the update list.</span></span>
1. <span data-ttu-id="92130-141">Vyberte balíček, který chcete aktualizovat, vyberte požadovanou verzi z rozevíracího seznamu na pravé straně a vyberte **aktualizovat**.</span><span class="sxs-lookup"><span data-stu-id="92130-141">Select the package to update, select the desired version from the drop-down on the right, and select **Update**.</span></span>

    ![Aktualizace balíčku](media/UpdatePackages.png)

1. <a name="implicit_reference"></a><span data-ttu-id="92130-143">Pro některé balíčky **aktualizace** je tlačítko neaktivní a zobrazí se zpráva s informacemi o tom, že jej je "implicitně odkazovat pomocí sady SDK" (nebo "AutoReferenced").</span><span class="sxs-lookup"><span data-stu-id="92130-143">For some packages, the **Update** button is disabled and a message appears saying that it's "Implicitly referenced by an SDK" (or "AutoReferenced").</span></span> <span data-ttu-id="92130-144">Tato zpráva znamená, že balíček je součástí větší platforma nebo sada SDK a by neměly být aktualizovány nezávisle na sobě.</span><span class="sxs-lookup"><span data-stu-id="92130-144">This message indicates that the package is part of a larger framework or SDK and should not be updated independently.</span></span> <span data-ttu-id="92130-145">(Tyto balíčky jsou označené interně `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) Například `Microsoft.NETCore.App` je součástí sady .NET Core SDK, a verze balíčku není stejná jako verze rozhraní framework modulu runtime aplikace používá.</span><span class="sxs-lookup"><span data-stu-id="92130-145">(Such packages are internally marked with `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) For example, `Microsoft.NETCore.App` is part of the .NET Core SDK, and the package version is not the same as the version of the runtime framework used by the application.</span></span> <span data-ttu-id="92130-146">Je potřeba [aktualizaci instalace .NET Core](https://aka.ms/dotnet-download) získat nové verze modulu runtime ASP.NET Core a .NET Core.</span><span class="sxs-lookup"><span data-stu-id="92130-146">You need to [update your .NET Core installation](https://aka.ms/dotnet-download) to get new versions of the ASP.NET Core and .NET Core runtime.</span></span> <span data-ttu-id="92130-147">[Najdete v tomto dokumentu podrobné informace o .NET Core metabalíčky a správy verzí](/dotnet/core/packages).</span><span class="sxs-lookup"><span data-stu-id="92130-147">[See this document for more details on .NET Core metapackages and versioning](/dotnet/core/packages).</span></span> <span data-ttu-id="92130-148">To platí pro běžně používané následujících balíčků:</span><span class="sxs-lookup"><span data-stu-id="92130-148">This applies to the following commonly used packages:</span></span>
    * <span data-ttu-id="92130-149">Microsoft.AspNetCore.All</span><span class="sxs-lookup"><span data-stu-id="92130-149">Microsoft.AspNetCore.All</span></span>
    * <span data-ttu-id="92130-150">Microsoft.AspNetCore.App</span><span class="sxs-lookup"><span data-stu-id="92130-150">Microsoft.AspNetCore.App</span></span>
    * <span data-ttu-id="92130-151">Microsoft.NETCore.App</span><span class="sxs-lookup"><span data-stu-id="92130-151">Microsoft.NETCore.App</span></span>
    * <span data-ttu-id="92130-152">NETStandard.Library</span><span class="sxs-lookup"><span data-stu-id="92130-152">NETStandard.Library</span></span>

    ![Příklad balíček označen jako implicitně odkazy nebo AutoReferenced](media/PackageManagerUIAutoReferenced.png)

1. <span data-ttu-id="92130-154">K aktualizaci více balíčků na jejich nejnovější verze, vyberte je v seznamu a vyberte **aktualizovat** tlačítko nad seznamem.</span><span class="sxs-lookup"><span data-stu-id="92130-154">To update multiple packages to their newest versions, select  them in the list and select the **Update** button above the list.</span></span>
1. <span data-ttu-id="92130-155">Můžete také aktualizovat v nějakém balíčku **nainstalováno** kartu. V takovém případě podrobnosti balíčku zahrnují volič verze (vztahuje **zahrnout předběžné verze** možnost) a **aktualizace** tlačítko.</span><span class="sxs-lookup"><span data-stu-id="92130-155">You can also update an individual package from the **Installed** tab. In this case, the details for the package include a version selector (subject to the **Include prerelease** option) and an **Update** button.</span></span>

## <a name="managing-packages-for-the-solution"></a><span data-ttu-id="92130-156">Správa balíčků pro řešení</span><span class="sxs-lookup"><span data-stu-id="92130-156">Managing packages for the solution</span></span>

<span data-ttu-id="92130-157">Správa balíčků pro řešení je pohodlný způsob pro práci s více projektů současně.</span><span class="sxs-lookup"><span data-stu-id="92130-157">Managing packages for a solution is a convenient means to work with multiple projects simultaneously.</span></span>

1. <span data-ttu-id="92130-158">Vyberte **nástroje > Správce balíčků NuGet > spravovat balíčky NuGet pro řešení...**  nabídky příkazu, nebo klikněte pravým tlačítkem na řešení a vyberte **spravovat balíčky NuGet...** :</span><span class="sxs-lookup"><span data-stu-id="92130-158">Select the **Tools > NuGet Package Manager > Manage NuGet Packages for Solution...** menu command, or right-click the solution and select **Manage NuGet Packages...**:</span></span>

    ![Spravovat balíčky NuGet pro řešení](media/ManagePackagesSolutionUICommand.png)

1. <span data-ttu-id="92130-160">Při správě balíčků pro řešení, uživatelské rozhraní vám umožní vybrat projekty, které jsou ovlivněny operace:</span><span class="sxs-lookup"><span data-stu-id="92130-160">When managing packages for the solution, the UI lets you select the projects that are affected by the operations:</span></span>

    ![Selektor projektu při správě balíčků řešení](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a><span data-ttu-id="92130-162">Konsolidace kartu</span><span class="sxs-lookup"><span data-stu-id="92130-162">Consolidate tab</span></span>

<span data-ttu-id="92130-163">Vývojáři obvykle považuje za špatný postup používají různé verze stejného balíčku NuGet v různých projektech ve stejném řešení.</span><span class="sxs-lookup"><span data-stu-id="92130-163">Developers typically consider it bad practice to use different versions of the same NuGet package across different projects in the same solution.</span></span> <span data-ttu-id="92130-164">Pokud budete chtít spravovat balíčky pro řešení, poskytuje uživatelské rozhraní Správce balíčků **konsolidovat** karta, na které můžete snadno zobrazit kde balíčky s čísly odlišné verze používají různé projekty v řešení:</span><span class="sxs-lookup"><span data-stu-id="92130-164">When you choose to manage packages for a solution, the Package Manager UI provides a **Consolidate** tab on which you can easily see where packages with distinct version numbers are used by different projects in the solution:</span></span>

![Karta konsolidovat uživatelského rozhraní Správce balíčků](media/ConsolidateTab.png)

<span data-ttu-id="92130-166">V tomto příkladu je projekt ClassLibrary1 využitím objektu EntityFramework 6.2.0, zatímco ConsoleApp1 je využitím objektu EntityFramework 6.1.0.</span><span class="sxs-lookup"><span data-stu-id="92130-166">In this example, the ClassLibrary1 project is using EntityFramework 6.2.0, whereas ConsoleApp1 is using EntityFramework 6.1.0.</span></span> <span data-ttu-id="92130-167">Pro konsolidaci verze balíčků, postupujte takto:</span><span class="sxs-lookup"><span data-stu-id="92130-167">To consolidate package versions, do the following:</span></span>

- <span data-ttu-id="92130-168">Vyberte projekty, které chcete aktualizovat v seznamu projektu.</span><span class="sxs-lookup"><span data-stu-id="92130-168">Select the projects to update in the project list.</span></span>
- <span data-ttu-id="92130-169">Vyberte verze se má použít ve všech projektech v **verze** ovládacího prvku, třeba 6.2.0 objektu EntityFramework.</span><span class="sxs-lookup"><span data-stu-id="92130-169">Select the version to use in all those projects in the **Version** control, such as EntityFramework 6.2.0.</span></span>
- <span data-ttu-id="92130-170">Vyberte **nainstalovat** tlačítko.</span><span class="sxs-lookup"><span data-stu-id="92130-170">Select the **Install** button.</span></span>

<span data-ttu-id="92130-171">Správce balíčků nainstaluje do všech vybraných projektů, po jejichž uplynutí již nezobrazuje balíček na verze vybraného balíčku **konsolidovat** kartu.</span><span class="sxs-lookup"><span data-stu-id="92130-171">The Package Manager installs the selected package version into all selected projects, after which the package no longer appears on the **Consolidate** tab.</span></span>

## <a name="package-sources"></a><span data-ttu-id="92130-172">Zdroje balíčků</span><span class="sxs-lookup"><span data-stu-id="92130-172">Package sources</span></span>

<span data-ttu-id="92130-173">Chcete-li změnit zdroj, ze kterého sady Visual Studio získá balíčky, vyberte jednu z modulu pro výběr zdroje:</span><span class="sxs-lookup"><span data-stu-id="92130-173">To change the source from which Visual Studio obtains packages, select one from the source selector:</span></span>

![Výběr zdroje balíčku v uživatelské rozhraní Správce balíčků](media/PackageSourceDropDown.png)

<span data-ttu-id="92130-175">Správa zdroje balíčků:</span><span class="sxs-lookup"><span data-stu-id="92130-175">To manage package sources:</span></span>

1. <span data-ttu-id="92130-176">Vyberte **nastavení** ikony v Uživatelském rozhraní Správce balíčků uvedených níže nebo pomocí **nástroje > Možnosti** příkazů a přejděte k položce **Správce balíčků NuGet**:</span><span class="sxs-lookup"><span data-stu-id="92130-176">Select the **Settings** icon in the Package Manager UI outlined below or use the **Tools > Options** command and scroll to **NuGet Package Manager**:</span></span>

    ![Ikona nastavení uživatelského rozhraní Správce balíčků](media/PackageSourceSettings.png)

1. <span data-ttu-id="92130-178">Vyberte **zdroje balíčků** uzlu:</span><span class="sxs-lookup"><span data-stu-id="92130-178">Select the **Package Sources** node:</span></span>

    ![Možnosti zdroje balíčku](media/options.png)

1. <span data-ttu-id="92130-180">Chcete-li přidat zdroj **+**, upravte název, zadejte adresu URL nebo cestu **zdroj** ovládací prvek a vyberte **aktualizace**.</span><span class="sxs-lookup"><span data-stu-id="92130-180">To add a source, select **+**, edit the name, enter the URL or path in the **Source** control, and select  **Update**.</span></span> <span data-ttu-id="92130-181">Zdroj se teď zobrazí v rozevírací seznam pro výběr.</span><span class="sxs-lookup"><span data-stu-id="92130-181">The source now appears in the selector drop-down.</span></span>
1. <span data-ttu-id="92130-182">Chcete-li změnit zdroj balíčku, vyberte ho, proveďte úpravy v **název** a **zdroj** pole a vyberte **aktualizace**.</span><span class="sxs-lookup"><span data-stu-id="92130-182">To change a package source, select it, make edits in the **Name** and **Source** boxes, and select **Update**.</span></span>
1. <span data-ttu-id="92130-183">Zakázat zdroje balíčku, zrušte zaškrtnutí políčka nalevo od názvu v seznamu.</span><span class="sxs-lookup"><span data-stu-id="92130-183">To disable a package source, clear the box to the left of the name in the list.</span></span>
1. <span data-ttu-id="92130-184">Odebrat zdroj balíčku, vyberte ho a pak vyberte **X** tlačítko.</span><span class="sxs-lookup"><span data-stu-id="92130-184">To remove a package source, select it and then select the **X** button.</span></span>
1. <span data-ttu-id="92130-185">Nahoru a Šipka dolů tlačítka nemění pořadí priority zdroje balíčků.</span><span class="sxs-lookup"><span data-stu-id="92130-185">Using the up and down arrow buttons does not change the priority order of the package sources.</span></span> <span data-ttu-id="92130-186">Visual Studio bude ignorovat pořadí zdroje balíčků pomocí balíčku od toho zdroje je nejprve reagovat na požadavky.</span><span class="sxs-lookup"><span data-stu-id="92130-186">Visual Studio ignores the order of package sources, using the package from whichever source is first to respond to requests.</span></span> <span data-ttu-id="92130-187">Další informace najdete v tématu [obnovení balíčku](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="92130-187">For more information, see [Package restore](../consume-packages/package-restore.md).</span></span>

> [!Tip]
> <span data-ttu-id="92130-188">Pokud po jejím odstranění znovu objeví zdroj balíčku, mohou být uvedeny v úrovni počítače nebo individuální `NuGet.Config` soubory.</span><span class="sxs-lookup"><span data-stu-id="92130-188">If a package source reappears after deleting it, it may be listed in a computer-level or user-level `NuGet.Config` files.</span></span> <span data-ttu-id="92130-189">Naleznete v tématu [konfigurace NuGet chování](../consume-packages/configuring-nuget-behavior.md) pro umístění tyto soubory pak odebrat zdrojový úprava souborů ručně nebo pomocí [nuget zdrojů příkaz](../tools/nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="92130-189">See [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md) for the location of these files, then remove the source by editing the files manually or using the [nuget sources command](../tools/nuget-exe-CLI-reference.md).</span></span>

## <a name="package-manager-options-control"></a><span data-ttu-id="92130-190">Ovládací prvek možnosti Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="92130-190">Package manager Options control</span></span>

<span data-ttu-id="92130-191">Při výběru balíčku, uživatelské rozhraní Správce balíčků zobrazí malá, rozšiřitelné **možnosti** ovládacího prvku pod volič verze (zobrazuje se zde i sbalení a rozbalení).</span><span class="sxs-lookup"><span data-stu-id="92130-191">When a package is selected, the Package Manager UI displays a small, expandable **Options** control below the version selector (shown here both collapsed and expanded).</span></span> <span data-ttu-id="92130-192">Všimněte si, že některé projektu typy pouze **zobrazit okno náhledu** možnost je k dispozici.</span><span class="sxs-lookup"><span data-stu-id="92130-192">Note that for some project types, only the **Show preview window** option is provided.</span></span>

![Možnosti Správce balíčků](media/PackageManagerUIOptions.png)

<span data-ttu-id="92130-194">Následující části popisují tyto možnosti.</span><span class="sxs-lookup"><span data-stu-id="92130-194">The following sections explain these options.</span></span>

### <a name="show-preview-window"></a><span data-ttu-id="92130-195">Zobrazit okno náhledu</span><span class="sxs-lookup"><span data-stu-id="92130-195">Show preview window</span></span>

<span data-ttu-id="92130-196">Vyberete-li, modální okno zobrazí které závislosti zvolené balíček před instalací balíčku:</span><span class="sxs-lookup"><span data-stu-id="92130-196">When selected, a modal window displays which the dependencies of a chosen package before the package is installed:</span></span>

![Dialogové okno náhledu příklad](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a><span data-ttu-id="92130-198">Možnosti instalace a aktualizace</span><span class="sxs-lookup"><span data-stu-id="92130-198">Install and Update Options</span></span>

<span data-ttu-id="92130-199">(Není k dispozici pro všechny typy projektů.)</span><span class="sxs-lookup"><span data-stu-id="92130-199">(Not available for all project types.)</span></span>

<span data-ttu-id="92130-200">**Chování závislostí** konfiguruje jak NuGet rozhodne, která verze závislé balíčky pro instalaci:</span><span class="sxs-lookup"><span data-stu-id="92130-200">**Dependency behavior** configures how NuGet decides which versions of dependent packages to install:</span></span>

- <span data-ttu-id="92130-201">*Ignorovat závislosti* přeskočí instalaci všechny závislosti, přerušíte obvykle probíhá instalace balíčku.</span><span class="sxs-lookup"><span data-stu-id="92130-201">*Ignore dependencies* skips installing any dependencies, which typically breaks the package being installed.</span></span>
- <span data-ttu-id="92130-202">*Nejnižší* [výchozí] instaluje závislost s minimální verze číslo, které splňuje požadavky na primární zvolené balíčku.</span><span class="sxs-lookup"><span data-stu-id="92130-202">*Lowest* [Default] installs the dependency with the minimal version number that meets the requirements of the primary chosen package.</span></span>
- <span data-ttu-id="92130-203">*Nejvyšší oprava* nainstaluje verzi s stejná čísla hlavní verze a podverze, ale nejvyšší číslo opravy.</span><span class="sxs-lookup"><span data-stu-id="92130-203">*Highest Patch* installs the version with the same major and minor version numbers, but the highest patch number.</span></span> <span data-ttu-id="92130-204">Například pokud je zadaná verze 1.2.2 klikněte nejvyšší, který začíná 1.2 budou nainstalovány jejich verze</span><span class="sxs-lookup"><span data-stu-id="92130-204">For example, if version 1.2.2 is specified then the highest version that starts with 1.2 will be installed</span></span>
- <span data-ttu-id="92130-205">*Nejvyšší podverze* nainstaluje verzi stejné číslo hlavní verze, ale nejvyšší číslo podverze a oprava číslo.</span><span class="sxs-lookup"><span data-stu-id="92130-205">*Highest Minor* installs the version with the same major version number but the highest minor number and patch number.</span></span> <span data-ttu-id="92130-206">Pokud je zadaná verze 1.2.2, pak nejvyšší začínající hodnotou 1 budou nainstalovány jejich verze</span><span class="sxs-lookup"><span data-stu-id="92130-206">If version 1.2.2 is specified, then the highest version that starts with 1 will be installed</span></span>
- <span data-ttu-id="92130-207">*Nejvyšší* nainstaluje nejvyšší dostupnou verzi balíčku.</span><span class="sxs-lookup"><span data-stu-id="92130-207">*Highest* installs the highest available version of the package.</span></span>

<span data-ttu-id="92130-208">**Akce při konfliktu souborů** Určuje, jak NuGet pracovat s balíčky, které již existují v projektu nebo v místním počítači:</span><span class="sxs-lookup"><span data-stu-id="92130-208">**File conflict action** specifies how NuGet should handle packages that already exist in the project or local machine:</span></span>

- <span data-ttu-id="92130-209">*Příkazový řádek* dává pokyn k dotaz, jestli chcete zachovat nebo přepsat existující balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="92130-209">*Prompt* instructs NuGet to ask whether to keep or overwrite existing packages.</span></span>
- <span data-ttu-id="92130-210">*Přeskakovat vše* dá pokyn, chcete-li přeskočit přepíše všechny stávající balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="92130-210">*Ignore All* instructs NuGet to skip overwriting any existing packages.</span></span>
- <span data-ttu-id="92130-211">*Přepsat vše* dává pokyn k přepsání existujících balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="92130-211">*Overwrite All* instructs NuGet to overwrite any existing packages.</span></span>

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a><span data-ttu-id="92130-212">Možnosti odinstalace</span><span class="sxs-lookup"><span data-stu-id="92130-212">Uninstall Options</span></span>

<span data-ttu-id="92130-213">(Není k dispozici pro všechny typy projektů.)</span><span class="sxs-lookup"><span data-stu-id="92130-213">(Not available for all project types.)</span></span>

<span data-ttu-id="92130-214">**Odebrat závislosti**: Pokud je vybráno, odebere všechny závislé balíčky, pokud nejsou odkazovat kdekoli v projektu.</span><span class="sxs-lookup"><span data-stu-id="92130-214">**Remove dependencies**: when selected, removes any dependent packages if they're not referenced elsewhere in the project.</span></span>

<span data-ttu-id="92130-215">**Vynutit odinstalaci i v případě, že jsou na něm závislosti**: Pokud je vybráno, odinstaluje balíček i v případě, že je stále odkazovaný v projektu.</span><span class="sxs-lookup"><span data-stu-id="92130-215">**Force uninstall even if there are dependencies on it**: when selected, uninstalls a package even if it's still being referenced in the project.</span></span> <span data-ttu-id="92130-216">To se obvykle používá v kombinaci s **odebrat závislosti** odebrat balíček a cokoli, co je nainstalovat závislosti.</span><span class="sxs-lookup"><span data-stu-id="92130-216">This is typically used in combination with **Remove dependencies** to remove a package and whatever dependencies it installed.</span></span> <span data-ttu-id="92130-217">Pomocí této možnosti může, ale vést k poškození odkazů v projektu.</span><span class="sxs-lookup"><span data-stu-id="92130-217">Using this option may, however, lead to broken references in the project.</span></span> <span data-ttu-id="92130-218">V takovém případě budete muset [znovu nainstalujte tyto balíčky](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="92130-218">In such cases, you may need to [reinstall those other packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>
